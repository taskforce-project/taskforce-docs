---
id: agent-delivery-pipeline
title: Agent Delivery Pipeline - deleguer une tache a un agent (provider-agnostic)
doc_type: spec
statut: draft
version: 0.2
date: "09/09/2026"
auteur: Pierre MICHEL
backlog_id: TF-AGENT-DELIVERY
tags: [road-to-v2, spec, ia, coding-agent, claude-code, copilot, cursor, github, ooda, brain-os]
related:
  - "README.md"
  - "Roadmap_Consolidee.md"
  - "Moteur_IA_World_Model_OODA.md"
  - "Agents_C_Level.md"
  - "Benchmark_Modeles_IA.md"
  - "Connecteurs_et_Catalogue.md"
  - "UX_Actions_At_Scale.md"
  - "Scalabilite_et_Robustesse.md"
  - "../02-produit/Backend.md"
  - "../02-produit/Frontend.md"
---

# Agent Delivery Pipeline

> **Thèse.** Aujourd'hui l'humain **copie** le prompt généré par l'IA et le **colle** lui-meme dans Claude Code (Phase B lot 1). Ce spec **ferme la boucle** : on **délégue** la tache a l'agent de son **choix** (Claude Code, GitHub Copilot, Cursor, autre), qui a **tout le contexte** (repo + Brain OS + outils de l'entreprise), fait le travail **dans SON cloud sous le compte de l'utilisateur**, produit un **résultat** (PR, doc, résumé... selon la tache), et l'issue **remonte dans une colonne** avec le lien direct - **jusqu'a la décision humaine (1 clic)**. C'est le **lot 2b déja planifié** ([[Roadmap_Consolidee]] Phase B), rendu **autonome, provider-agnostic et task-agnostic**. Additif, PAS un refactor. Invisible tant qu'on ne délégue rien.

## 0. Décisions actées (09/09/2026)

| # | Décision |
|---|---|
| D1 | **Orchestration Java-native, provider-agnostic. PAS de Python / LangChain / LangGraph.** On s'inspire de leurs patrons (graphe d'étapes, checkpoints, interruptions HITL) - qu'on a **déja** dans `AnalysisJobRunner` - sans importer un 2e runtime. Cf. §3.1. |
| D2 | **L'exécution tourne dans le cloud du provider, sous le compte/plan de l'utilisateur** (Copilot/Cursor : nativement cloud ; Claude : clé Anthropic de l'utilisateur). **TaskForce n'héberge aucun runtime lourd** (VM1 = hors sujet). |
| D3 | **Le coût d'exécution est porté par le plan de l'utilisateur** (son Claude/Cursor/Copilot). TaskForce **récupere et affiche sa consommation** pour qu'il suive tout au meme endroit. Notre IA n'est facturée que sur nos usages (spec, résumé) via le quota existant. |
| D4 | **Task-agnostic** : pas que du code. Une tache déléguable peut etre « rédige ce mail », « analyse marketing », « écris cette doc ». Le **résultat** dépend de l'objectif (PR, doc, résumé + liens) + la **colonne** d'arrivée + le **lien direct**. |
| D5 | **Événementiel multi-source** : pas que GitHub. Le signal de fin vient idéalement de **l'agent lui-meme** (« workflow terminé ») ou de l'outil concerné, normalisé en un événement de délégation. |
| D6 | **La décision reste TOUJOURS humaine, en 1 clic.** Jamais d'auto-merge, jamais d'auto-exécution du critique. |
| D7 | **Colonnes custom + supprimables**, meme celles fournies par défaut. On peut étendre les statuts, mais l'utilisateur reste maitre de son board. |
| D8 | **UI/UX ouverte au refactor** partout, tant que ça sert l'utilisateur et reste cohérent. On **ne touche pas le métier** (sinon on casse la démo Smart Assign), seulement l'évolue. Approche a l'échelle : [[UX_Actions_At_Scale]]. |

## 1. Ce qui existe déja (ne PAS reconstruire)

| Brique nécessaire | Réalité v1 | Référence |
|---|---|---|
| Génération spec + **prompt d'exécution** + découpage + « déja vu » RAG | ✅ fait | `IssueAiService.generateSpec` / `approveSpec` |
| Moteur de **job async, streamé STOMP, reprennable** (HITL) | ✅ fait | `AnalysisJobRunner` |
| Framework **tool-calling** + registre + adaptateur externe | ✅ fait | `AgentService`, `AgentTool`, `ExternalMcpTool` |
| **Stockage de credentials chiffrés** + OAuth + refresh | ✅ fait | `McpTokenService`, `McpOAuthService`, `ConnectorCatalog` |
| **Hote MCP** (appeler des outils externes pendant le job) | ✅ fait | `McpClient`, `WorkspaceMcpService` |
| **Contexte métier/vision** (RAG) | ✅ fait | Brain OS (`search_brain`, ingestion auto) |
| **Scope GitHub write déja consenti** | ✅ scope OAuth `repo,read:org` | `GitHubIntegrationService` (autorise déja `POST /user/repos` + assign ; le code ne fait que du GET) |
| Point d'extension **exécution** anticipé | ✅ prévu | `AiGenerationKind.EXECUTION` (commenté, non implémenté) |
| **Webhook sortant** (a activer) | ⚠️ dead code | `WebhookService.fire()` jamais appelé |

> ~2/3 de la plomberie est la. Les ajouts sont **ciblés et additifs**.

## 2. Ce qui manque (les ajouts)

1. Contrat **`CodingAgentProvider`** + implémentations (Claude Code d'abord).
2. **Lien Projet ↔ repo GitHub** + bootstrap a la création de projet **et lien en cours de route** (§3.2) ; UI a l'échelle (§[[UX_Actions_At_Scale]]).
3. **Job de délégation** (patron `AnalysisJobRunner`).
4. **Assigné « agent »** (léger) **avec logo du provider** + lien du compte provider de l'utilisateur → **récupération de sa consommation**.
5. **Reco de modele + puissance** dans `generateSpec`.
6. **Ingestion d'événements multi-source** + **auto-move kanban** (statuts custom) ; activer `WebhookService.fire()`.
7. **Base d'onboarding entreprise** + contexte par **domaine C-level** (§3.5, [[Agents_C_Level]]).

## 3. Architecture

### 3.1 Orchestration : Java-native, agnostic (D1)

**On ne prend PAS Python/LangChain/LangGraph.** Raisons :
- Le moteur est **déja tout en Java** (`AgentService`, `AnalysisJobRunner`, `McpClient`) - un 2e runtime Python = split-brain, double sécurité, double déploiement, double montée en charge.
- On a **déja l'équivalent de LangGraph** : `AnalysisJobRunner` est une machine a états async, checkpointée, avec **interruption HITL** (suspend/resume) et streaming STOMP. C'est exactement le patron « graphe + checkpoint + interrupt ».
- Les agents (Claude Code/Cursor/Copilot) sont **externes** et tournent dans **leur** cloud (D2). L'orchestration ne fait que **composer → dispatcher → suivre → ingérer l'événement**. Elle n'a pas besoin d'un framework d'agents Python.

On **s'inspire** des bons patrons de LangGraph (noeuds, arretes conditionnelles, checkpoints, human-in-the-loop, reprise) et on les implémente proprement en Java, orienté **robustesse + scalabilité** (cf. [[Scalabilite_et_Robustesse]]).

### 3.2 Contrat provider-agnostic

```java
interface DeliveryAgentProvider {
    String key();                         // "claude-code" | "github-copilot" | "cursor" | ...
    ProviderBranding branding();          // nom + logo (Anthropic, OpenAI, Gemini...)
    CapabilityProfile capabilities();     // modeles, effort, cloud hébergé ?, types de tache
    AgentRun dispatch(AgentBrief brief);  // lance le run dans le cloud du provider (compte user)
    AgentRunStatus poll(AgentRun run);    // running | needs_input | done | failed + resultRef
    UsageSnapshot usage(Account account); // consommation a afficher dans TaskForce (D3)
}
```

- `AgentBrief` = spec + prompt (`generateSpec`) + **contexte** (Brain OS + repo + outils, §3.5) + **modele/effort recommandés** (§3.4) + **objectif/format de sortie attendu** (D4).
- `AgentRunResult` = **artefact selon la tache** : PR (code), doc/fichier (rédaction), résumé + liens (analyse) + **colonne cible** + **lien direct** pour consulter.
- Implémentations cibles :
  - **`ClaudeCodeProvider`** (priorité 1) : clé API Anthropic de l'utilisateur (facturée a l'usage sur son compte API). Exécution **hébergée par Anthropic** via **Managed Agents** (boucle + sandbox par session) OU **Claude Agent SDK** auto-hébergé sur un runner léger. Cf. §7.
  - **`CopilotProvider`** : assigne l'issue GitHub → Copilot coding agent → PR (**cloud GitHub, plan Copilot de l'utilisateur**).
  - **`CursorProvider`** : API background agents (**cloud Cursor, plan de l'utilisateur**).
  - **`…Provider`** : bring-your-own, meme patron.
- Choix **par workspace (défaut) ou par issue**, via un **picker façon Linear** (pas un dropdown géant, cf. [[UX_Actions_At_Scale]]).

### 3.3 Lien Projet ↔ repo GitHub (façon Linear)

- **A la création de projet** : étape optionnelle - **créer un repo** / **lier un existant** / **aucun** (« cocher les options GitHub comme d'hab »).
- **En cours de route** : lier/délier depuis le projet OU depuis une issue, **via le command menu / une action contextuelle**, jamais un dropdown qui gonfle (le vrai sujet UX, cf. [[UX_Actions_At_Scale]]).
- **Ajouts** : `Project.repoFullName` (+ `repoProvider` pour généraliser) ; `GitHubIntegrationService.createRepo()` → `POST /user/repos` (scope déja consenti).
- Comme Linear : le repo se lie **au niveau projet** (défaut hérité par les issues) et **au niveau issue** (surcharge ponctuelle) - jamais imposé, toujours découvrable a la demande.

### 3.4 Le job de délégation

Patron `AnalysisJobRunner` (async, streamé, reprennable) :

1. **COMPOSE** - `AgentBrief` = `generateSpec` + contexte (Brain OS + repo + outils) + objectif/format attendu.
2. **DISPATCH** - `provider.dispatch(brief)` dans le cloud du provider ; l'issue passe en **« Délégué / In progress by AI »**.
3. **TRACK** - `poll` et/ou **événement entrant** (l'agent signale la fin, cf. §3.6) ; blocages → statut **Blocked** / sous-issues.
4. **RESULT** - a la fin : artefact selon la tache (PR/doc/résumé + liens) + l'issue **remonte en colonne** avec **lien direct**.
5. **DÉCISION HUMAINE (1 clic, D6)** - l'humain valide/rejette/modifie. Jamais d'auto-merge.
6. **CLOSE** - outcome écrit en node **`AiGenerationKind.EXECUTION`** (le Brain OS grandit) + `assignment_events` (audit + [[Data_Flywheel_et_Apprentissage]]).

### 3.5 Contexte de l'agent (le nerf : tout est une question de données)

Le contexte n'est pas que « repo + texte Brain OS ». C'est **la donnée de l'entreprise, la ou elle vit** :

- **Base d'onboarding (obligatoire)** : c'est quoi l'entreprise, qui est qui, les grandes lignes. **Sans base, pas de contexte.** Le Brain OS **s'auto-alimente ensuite** au fil du travail, mais il faut une amorce (→ onboarding a spécifier, extension de [[../02-produit/Frontend.md]] onboarding).
- **Brain OS** : le « pourquoi » (métier, vision, produit), RAG existant.
- **Repo / doc tech** : le « comment » (l'agent clone et lit lui-meme).
- **Outils de l'entreprise = données externes** : CRM, Slack, Stripe... rattachés a des **domaines C-level** (CEO/COO/CFO/CTO/CGO...). Chaque Chief a **son contexte + ses outils du quotidien** ; l'agent doit pouvoir **tirer la bonne data au bon endroit** (via l'hote MCP + le catalogue de connecteurs déja la). Cf. [[Agents_C_Level]] et [[Connecteurs_et_Catalogue]].

> Cadre mental : **ou est la donnée, qui l'utilise, ou elle va, a quoi elle sert, comment je l'utilise, quel levier.** Le moteur (World Model × OODA, [[Moteur_IA_World_Model_OODA]]) raisonne sur cette carte de données.

### 3.6 Événements + résultat (multi-source, D5)

- Le signal de fin vient idéalement de **l'agent** (« workflow terminé : PR ouverte / tests passés / doc rédigée »), pas seulement d'un webhook GitHub.
- **Ingestion normalisée** : un endpoint entrant générique (`delivery-events`) qui accepte GitHub, mais aussi le rapport direct d'un provider ou d'un autre outil → un **événement de délégation** unique.
- **Sortie de l'agent** = résumé + artefact (doc, lien PR, ...) **selon l'objectif** + **colonne d'arrivée** + **lien direct**. C'est ce que TaskForce affiche a l'utilisateur.
- Côté **sortant**, activer `WebhookService.fire()` (dead code) pour notifier les outils tiers.

### 3.7 Assigné « agent » + suivi de consommation (D3)

- L'agent est une **cible assignable légere** (pas un membre lourd) affichée **avec le logo du provider** (Anthropic/OpenAI/Gemini...).
- **Lier le compte provider de l'utilisateur** → TaskForce **récupere sa consommation** et l'**affiche** : il suit tout au meme endroit, sans ouvrir Claude Desktop en parallele. Côté Anthropic, c'est l'**Admin API (usage & cost reports)** (raw HTTP, hors SDK) ; côté Copilot/Cursor, leurs endpoints d'usage respectifs.
- Vision : **on refait un Claude Desktop, mais sans GUI de chat** (ou minimaliste, découpé par secteur). Le cœur de valeur reste le **Brain OS** ; si l'utilisateur préfere son Claude, TaskForce devient **le hub ou Claude se branche** (« Claude → TaskForce » plutot que « TaskForce → Claude »). La feature est donc **peu coûteuse a dégager/pivoter** (§8).

## 4. Sécurité, coût, garde-fous

- **Décision humaine, 1 clic, toujours (D6).** Jamais d'auto-merge ni d'exécution auto du critique. Aligné human-in-the-loop du moteur ([[Moteur_IA_World_Model_OODA]]).
- **Coût porté par le plan de l'utilisateur (D3)** ; TaskForce affiche la conso récupérée. Notre IA n'est facturée que sur nos usages (spec/résumé) via `AiMeter`/`AiUsageService`.
- **Un max de sécurité + feedback + accés** (pas de GUI chat pour rattraper les erreurs) : repos/outils autorisés bornés par workspace, credentials chiffrés, scopes minimaux.
- **Audit a fond + historisation** : chaque run tracé (`assignment_events` + node `EXECUTION`), consultable.

## 5. Phases

| Phase | Contenu | Effort |
|---|---|---|
| **P1 - Claude Code bout-en-bout** (priorité user) | `DeliveryAgentProvider` + `ClaudeCodeProvider` (clé Anthropic user, cloud) + **bootstrap repo** + **lien repo en cours de route** + job de délégation + statut « In review » + reco de modele + **picker façon Linear** + affichage conso. | L |
| **P2 - Multi-provider** | `CopilotProvider` + `CursorProvider` + logos + comptes liés + conso par provider. | M |
| **P3 - Task-agnostic + auto** | taches non-code (mail, analyse, doc) + événements multi-source + machine a états (Result → colonne + lien) + sous-issues sur blocage. | M |
| **P4 - Hub / 2-way** | exposer TaskForce en **serveur MCP (inbound)** → Cursor/Claude Desktop/VSCode pull la tache nativement ; marketplace Agent Packs. | L |

## 6. Scope soutenance (v2 « qui ne se voit pas », démo-safe)

- **Câbler Claude Code pour de vrai** (priorité user) sur un repo de démo contrôlé, via la clé Anthropic de Pierre (cf. §7).
- **Picker présent** (Claude Code / Copilot / Cursor + logos), un seul pleinement branché.
- « Notre IA rédige la spec + le prompt + recommande le modele depuis le Brain OS » **marche déja** → moment fort.
- ⚠️ **Risque live** : un vrai run = minutes, réseau-dépendant. Repo **pré-chauffé**, tache **courte/déterministe**, filet = montrer spec → dispatch → remontée en Review meme si la PR est modeste.
- Task-agnostic complet + multi-provider = **post-soutenance**.

## 7. Questions ouvertes (a trancher avant P1)

- **Ou tourne Claude ? (résolu)** VM1 = hors sujet (RAM). L'option propre « cloud, rien a héberger » = **Anthropic Managed Agents** : Anthropic **exécute la boucle ET héberge un sandbox par session** (bash/fichiers/exécution de code). TaskForce ne fait qu'**orchestrer via l'API** (SDK **Java natif** `com.anthropic.*` → **pas de Python**, cf. D1). Alternative auto-hébergée = **Claude Agent SDK** (Claude Code packagé en librairie) sur un runner léger - plus d'infra, a éviter au début. Pour Copilot/Cursor, l'exécution est **déja** dans leur cloud.
- **Facturation Claude (a clarifier au user)** : l'**API Anthropic** (console.anthropic.com) est **séparée de l'abonnement claude.ai (Pro/Max)** et **facturée a l'usage (par token)** sur le **compte API**. Donc « connecter son compte » = **connecter une clé API** facturée a l'usage sur ce compte, PAS « gratuit parce qu'il a un abonnement chat ». C'est cohérent avec D3 (le compte de l'utilisateur porte le coût), mais ce n'est pas le meme portefeuille que sa souscription claude.ai. Copilot/Cursor : porté par leur abonnement respectif.
- **Auth Claude** : **clé API créée dans la console Anthropic** (login distinct de claude.ai). Flux « connect » par provider dans le catalogue.
- **Concurrence / charge** : stratégies startup-early mais **scalables et robustes** → spécifiées dans [[Scalabilite_et_Robustesse]] (file de runs, montée en charge DB verticale/horizontale).
- **Coût** : tranché (D3, plan de l'utilisateur).
- **Statuts** : extensibles + **custom + supprimables** (D7).

## 8. En une phrase

> On ne délegue plus a des humains **uniquement** : on délegue a **l'agent de son choix**, qui tourne **sous le compte de l'utilisateur**, avec le **repo créé au projet** et le **contexte nourri par le Brain OS + les outils de l'entreprise**, notre IA **recommande le modele**, l'agent **fait le travail** (code, mail, analyse...), rend un **résultat** et **remonte l'issue dans une colonne** - **la décision reste humaine, en 1 clic**. Le moat reste le **Brain OS** : si l'utilisateur préfere son Claude, TaskForce devient le **hub** ou Claude se branche.
