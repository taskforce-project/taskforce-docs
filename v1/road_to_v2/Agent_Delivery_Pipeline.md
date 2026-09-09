---
id: agent-delivery-pipeline
title: Agent Delivery Pipeline - deleguer une tache a un coding agent (provider-agnostic)
doc_type: spec
statut: draft
version: 0.1
date: "09/09/2026"
auteur: Pierre MICHEL
backlog_id: TF-AGENT-DELIVERY
tags: [road-to-v2, spec, ia, coding-agent, claude-code, copilot, cursor, github, ooda]
related:
  - "README.md"
  - "Roadmap_Consolidee.md"
  - "Moteur_IA_World_Model_OODA.md"
  - "Benchmark_Modeles_IA.md"
  - "Connecteurs_et_Catalogue.md"
  - "../02-produit/Backend.md"
  - "../02-produit/Frontend.md"
---

# Agent Delivery Pipeline

> **Thèse.** Aujourd'hui l'humain **copie** le prompt généré par l'IA et le **colle** lui-meme dans Claude Code (Phase B lot 1). Ce spec **ferme la boucle** : on **délègue** la tache au coding agent de son **choix** (Claude Code, GitHub Copilot, Cursor, autre), qui a **tout le contexte** (repo cloné + Brain OS), fait le travail, ouvre une **PR**, et l'issue **remonte en colonne Review** jusqu'a validation humaine. C'est le **lot 2b déja planifié** ([[Roadmap_Consolidee]] Phase B), rendu **autonome + provider-agnostic**, PAS un refactor. La feature est **invisible tant qu'on n'assigne pas une tache a un agent** : zéro impact sur les flux existants.

## 1. Ce qui existe déja (ne PAS reconstruire)

| Brique nécessaire | Réalité v1 | Référence |
|---|---|---|
| Génération spec + **prompt d'exécution** + découpage + « déja vu » RAG | ✅ fait | `IssueAiService.generateSpec` / `approveSpec` ; endpoints `ai/spec`, `ai/spec/approve` |
| Moteur de **job async, streamé STOMP, reprennable** (HITL) | ✅ fait | `AnalysisJobRunner` (OBSERVE→ANALYZE→CLARIFY→PERSIST) |
| Framework **tool-calling** + registre + adaptateur externe | ✅ fait | `AgentService` (Cortex), `AgentTool`, `ExternalMcpTool` |
| **Stockage de credentials chiffrés** + OAuth + refresh | ✅ fait | `McpTokenService`, `McpOAuthService`, `ConnectorCatalog` |
| **Hote MCP** (appeler des outils externes pendant le job) | ✅ fait | `McpClient`, `WorkspaceMcpService` |
| **Contexte métier/vision** (RAG) | ✅ fait | Brain OS (`search_brain`, ingestion auto) |
| **Scope GitHub write déja consenti** | ✅ le scope OAuth est `repo,read:org` | `GitHubIntegrationService` (le scope `repo` autorise déja `POST /user/repos` et l'assignation d'issue ; le code ne fait que du GET aujourd'hui) |
| Point d'extension **exécution** anticipé dans le modèle | ✅ prévu | `AiGenerationKind.EXECUTION` (commenté « outcome of an agent qui implémente la tache », non implémenté) |

> Conséquence : ~2/3 de la plomberie est la. Les ajouts sont **ciblés et additifs**, greffés sur ces coutures.

## 2. Ce qui manque (les ajouts, petits et localisés)

1. **Contrat `CodingAgentProvider`** + implémentations (Claude Code d'abord).
2. **Lien Projet ↔ repo GitHub** (le modèle `Project` n'a **aucun** champ repo aujourd'hui) + bootstrap a la création de projet (créer / lier / aucun).
3. **Job de délégation** (nouveau type, patron `AnalysisJobRunner`) : compose le brief, dispatch, suit, met a jour l'issue.
4. **Assigné « agent »** comme cible assignable (léger, pas un type de membre lourd).
5. **Reco de modèle + puissance** ajoutée a la sortie de `generateSpec`.
6. **Webhook GitHub entrant** + **auto-move kanban** (statuts « In review by AI » / « Blocked ») ; activer `WebhookService.fire()` (aujourd'hui **dead code**, jamais appelé) pour l'événementiel sortant.

## 3. Architecture

### 3.1 Contrat provider-agnostic

Une interface, N implémentations, façon connecteurs. Le marché bouge vite (Devin, Codex, Jules...) : l'abstraction est le bon pari.

```java
interface CodingAgentProvider {
    String key();                       // "claude-code" | "github-copilot" | "cursor" | ...
    CapabilityProfile capabilities();   // modeles dispo, effort/puissance, sandbox hébergé ?
    AgentRun dispatch(AgentBrief brief);// lance le run (async), renvoie un handle
    AgentRunStatus poll(AgentRun run);  // running | pr_opened | blocked | done + prUrl
    // + ingestion d'événements entrants (webhook) pour les providers qui en émettent
}
```

- `AgentBrief` = spec + prompt (de `generateSpec`) + **contexte Brain OS** (métier/vision) + **repoRef** (l'agent clone et lit la doc tech lui-meme) + modele/effort recommandés.
- Implémentations cibles :
  - **`ClaudeCodeProvider`** (priorité 1) : Claude Code **headless** dans un sandbox isolé (clone repo → exécute → PR). Utilise la clé Anthropic du workspace. C'est « ouvrir un nouveau chat qui a tout », automatisé.
  - **`CopilotProvider`** : assigne l'issue GitHub a **Copilot coding agent** → PR (GitHub héberge le sandbox, zéro runtime a exploiter).
  - **`CursorProvider`** : API **background agents** (lance un agent sur le repo → PR).
  - **`…Provider`** : bring-your-own, meme patron.
- Choix **par workspace (défaut) ou par issue**. Credentials dans l'infra chiffrée existante (`McpTokenService`).

### 3.2 Bootstrap Projet ↔ repo GitHub (façon Linear)

A la création d'un projet, une étape optionnelle : **créer un repo GitHub** / **lier un repo existant** / **aucun** - « on coche les options GitHub comme d'hab » via la connexion GitHub déja en place.

- **Ajout modèle** : `Project.repoFullName` (+ éventuellement `repoProvider` pour généraliser GitLab plus tard).
- **Ajout service** : `GitHubIntegrationService.createRepo(...)` → `POST /user/repos` (scope `repo` **déja consenti**) ; ou sélection dans `GET /user/repos` (déja implémenté).
- **Effet** : chaque projet a un repo → le coding agent sait **ou** travailler sans config manuelle. C'est ce qui rend « Claude a tout » vrai.

### 3.3 Le job de délégation

Nouveau type de job, patron `AnalysisJobRunner` (async, streamé, reprennable) :

1. **COMPOSE** - assemble le `AgentBrief` : `generateSpec` (spec + prompt) + récupération Brain OS (contexte métier/vision) + `repoRef` du projet.
2. **DISPATCH** - `provider.dispatch(brief)` ; l'issue passe en **« Delegated / In progress by AI »**.
3. **TRACK** - `poll` et/ou événements entrants (webhook) ; les sous-taches/blocages détectés deviennent des **sous-issues** ou un statut **Blocked**.
4. **REVIEW** - PR ouverte → l'issue remonte en **« In review by AI »** (jamais mergée sans humain).
5. **CLOSE** - merge humain → **Done** ; l'outcome est écrit en node **`AiGenerationKind.EXECUTION`** (le Brain OS grandit) + `assignment_events` (audit + data flywheel, cf. [[Data_Flywheel_et_Apprentissage]]).

### 3.4 Reco de modèle + puissance (par notre IA)

`generateSpec` (Groq/Qwen, cheap) enrichit sa sortie d'un bloc **recommandation** : « pour cette tache je recommande **tel provider / tel modele / tel niveau d'effort** ». Cheap model **planifie et route**, strong model **exécute** - le split que tu décris. Ancré sur [[Benchmark_Modeles_IA]] ; la reco reste **overridable** par l'humain (human-in-the-loop).

### 3.5 Contexte de l'agent (le découpage)

- **Brain OS** : entreprise, vision, produit, « le pourquoi » → contexte **métier** injecté dans le brief (RAG existant).
- **Repo / doc tech** : « le comment » → l'agent y accède **directement** en clonant.

Zéro refactor : on réutilise la récupération Brain OS existante comme bloc de contexte.

## 4. Sécurité / garde-fous

- **Jamais de merge auto** : la PR s'arrete en Review, validation humaine obligatoire (cohérent avec la philosophie human-in-the-loop du moteur, cf. [[Moteur_IA_World_Model_OODA]]).
- **Repos autorisés** bornés par workspace ; scope minimal ; credentials chiffrés (`McpTokenService`).
- **Sandbox isolé** par run (surtout Claude Code headless self-hosté : conteneur jetable).
- **Coût / débit** : réutiliser `AiMeter` + `AiUsageService` (quota par compte + garde-débit) pour plafonner les runs d'agent.
- **Audit** : chaque run tracé (`assignment_events` + node `EXECUTION`).

## 5. Phases

| Phase | Contenu | Effort |
|---|---|---|
| **P1 - Claude Code de bout en bout** (priorité user) | `CodingAgentProvider` + `ClaudeCodeProvider` (sandbox headless) + **bootstrap repo a la création de projet** + job de délégation + statut « In review » + reco de modele dans `generateSpec`. Tache créée dans l'app → dispatch → PR → Review. | L |
| **P2 - Multi-provider** | `CopilotProvider` (assign issue → PR) + `CursorProvider` (background agents) + picker de provider (workspace/issue). Copilot = le moins d'infra (sandbox hébergé par GitHub). | M |
| **P3 - Automatisation complete** | Webhook GitHub entrant → machine a états (PR opened→Review, merged→Done, failed→Blocked) ; auto-création de sous-issues sur blocage ; routage de modele **auto** ; activer `WebhookService.fire()` (sortant). | M |
| **P4 - Marketplace / 2-way** | Agent Packs, GitHub 2-way complet, exposer TaskForce en **serveur MCP** (inbound) pour que Cursor/Claude Desktop/VSCode pull la tache nativement. | L |

## 6. Scope soutenance (v2 « qui ne se voit pas », démo-safe)

- **Câbler UN provider pour de vrai** : **Claude Code** (priorité user) sur un repo de démo contrôlé, OU **Copilot** si on veut zéro runtime a héberger le jour J.
- **Le picker présent** (Claude Code / Copilot / Cursor visibles), meme si un seul est pleinement branché.
- La partie « notre IA rédige la spec + le prompt depuis le Brain OS » **marche déja** → moment fort de la démo.
- ⚠️ **Risque live** : un vrai run d'agent = minutes (clone/build/PR), dépend du réseau. Pour une démo fiable ET honnête (pas de mock) : repo de démo **pré-chauffé**, tache **courte et déterministe**, filet = montrer la spec + le dispatch + la remontée en Review meme si le code de la PR est modeste.
- Multi-provider complet + machine a états robuste = **post-soutenance**.

## 7. Questions ouvertes (a trancher avant P1)

- **Ou tourne Claude Code headless ?** Conteneur jetable sur VM1 (RAM ~3,8 Go, tension) vs runner dédié vs cloud. Impacte coût + concurrence.
- **Modele de coût** : runs d'agent = tokens externes (Anthropic/Cursor) hors quota Groq actuel → nouveau compteur / plafond.
- **Concurrence** : combien de runs simultanés (RAM/CPU) ; file d'attente.
- **Auth par provider** : Claude Code (clé Anthropic), Copilot (OAuth GitHub + activation Copilot sur le repo), Cursor (clé API) - flux distincts a modéliser dans le catalogue.
- **Statuts** : étendre `IssueStatusCategory` (enum figée : BACKLOG/UNSTARTED/STARTED/COMPLETED/CANCELLED) vs statuts nommés custom par projet.

## 8. En une phrase

> On ne délegue plus a des humains **uniquement** : on délegue a **l'agent de son choix**, avec le **repo créé a la création du projet** et le **contexte nourri par le Brain OS**, notre IA **recommande le modele**, l'agent **fait le travail**, et l'issue **remonte en Review** jusqu'a validation humaine. C'est le lot 2b de la Phase B, spécifié.
