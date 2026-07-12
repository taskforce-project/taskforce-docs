---
id: produit-ia
title: État Produit — IA
doc_type: register
statut: active
version: 0.1
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, ia, groq]
related:
  - "./README.md"
  - "./Backend.md"
---
<!-- Logo établissement : assets/images/logo_metz_numeric_school.svg | Logo projet : assets/images/logo_taskforce.png -->

# État Produit — IA (`ai-service/` + Groq)

**Version :** 0.1 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: IA](https://img.shields.io/badge/R%C3%A9pertoire-IA-blue?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [Fiche Backend](./Backend.md) · [🧠 Brain OS](../../Brain_OS.md)

**Tags :** `#produit` `#ia` `#groq`

> Prod : Groq direct depuis le backend Java (`GroqService`). `ai-service` Python = **vestigial**.
> Légende : ✅ `done` · 🔄 `wip` · ⬜ `todo`. Atout différenciant (➕ au-delà du standard).

## Existant
- [x] Smart Assign (pré-filtre Java + scoring Groq, repli) [id:: IA-SA-001] [statut:: done] [parite:: extra] [ref:: core/service/SmartAssignService.java]
- [x] **Serveur MCP TaskForce (v0.1)** : service Node `taskforce-mcp/` (SDK `@modelcontextprotocol/sdk`, stdio) exposant le workspace comme **tools MCP** à Claude / tout client — `taskforce_ask_cortex` (Brain OS RAG + agent), `taskforce_workspace_kpis`, `taskforce_list_projects`, `taskforce_list_my_issues`. Auth Keycloak (password grant dev, override Host) + enveloppe ApiResponse. Vérifié end-to-end (client MCP → KPIs/projets réels). Positionnement : TaskForce = étape de réflexion/process pour l'agent. Reste : tools d'écriture, `brain_search`, transport Streamable HTTP, volet **client MCP** (piloter Linear & co via TaskForce). [id:: IA-MCP-001] [statut:: wip] [parite:: extra] [ref:: taskforce-mcp/src/index.ts] (11/07/2026)
- [x] Assistant IA (chat contextualisé) [id:: IA-AS-001] [statut:: wip] [parite:: extra]
- [x] **Consommation IA persistante + modal « façon Claude »** : ledger mensuel réel (`ai_token_usage`, migration `V63`, agrégat par workspace) alimenté par `AgentService` → `AiUsageService.record` ; exposé par `GET /api/workspaces/{slug}/ai/usage` (used / limit / plan / reset). Front : modal `CortexUsage` sous l'input du chat (jauge de **contexte** + barre de **consommation mensuelle** + plan + CTA Détails/Upgrade) + page **Settings « Usage IA »**. Plafonds par plan = placeholders (FREE 1M / PRO 20M / ENTERPRISE illimité) à calibrer avec le pricing. Vérifié end-to-end (conso incrémentée du coût exact du message + persistée). [id:: IA-AS-004] [statut:: done] [parite:: extra] [ref:: core/service/AiUsageService.java + components/agent/cortex-usage.tsx] (11/07/2026)
- [x] **Consommation de tokens en direct (façon Claude)** — usage **réel** de bout en bout : Ollama renvoie `usage` → `ollama_gateway.chat` le remonte `(model, message, usage)` → `ChatResponse.usage` → `AiGatewayClient` **accumule par thread** (`LlmUsage` + `ThreadLocal`, sommé sur les itérations de la boucle de tool-calling) → `AgentService` injecte `AssistantAnswer.AssistantUsage {promptTokens, completionTokens, totalTokens}`. Front : compteur `TokenMeter` **animé** (count-up) — header du panneau Cortex « N tokens » (total session) + footer par message « MODE · N tokens (prompt↑ completion↓) ». Le modèle se nomme **Cortex** (system prompt + UI). Vérifié live (msg réel → 870 tokens : 589↑/281↓). Quota/plafond = à venir (dépend des plans). [id:: IA-AS-003] [statut:: done] [parite:: extra] [ref:: ai-service/app/services/ollama_gateway.py + core/service/{AiGatewayClient,LlmUsage}.java + core/service/agent/AgentService.java + frontend/components/chat/token-meter.tsx] (11/07/2026)
- [x] AI Insights (analytics) [id:: IA-IN-001] [statut:: wip] [parite:: extra]
- [x] Décision par projet (boucle OODA) : métriques réelles + RAG Brain OS → situation, risques, 3 priorités ; repli déterministe si LLM absent [id:: IA-DEC-001] [statut:: done] [parite:: extra] [ref:: core/service/agent/DecisionService.java]
- [x] **Workflows d'analyse asynchrones** : le job tourne en arrière-plan, son plan d'étapes est persisté et observable en direct (dock « Workflows IA ») ; le brief produit est persisté et ses 3 priorités sont **actionnables** (accepter → issue, épingler, éditer, écarter) [id:: IA-DEC-002] [statut:: done] [parite:: extra] [ref:: core/service/agent/AnalysisJobRunner.java] (10/07/2026)
- [x] **HITL** : en mode approfondi le modèle peut suspendre le workflow (`WAITING_FOR_INPUT`) pour poser **une** question de clarification ; la réponse est réinjectée dans le prompt et lui interdit d'en poser une seconde [id:: IA-DEC-003] [statut:: done] [parite:: extra] (10/07/2026)
- [x] **Génération de graphe par l'IA — deux modes, retrieval DB réel** : `POST /analytics/chart`. Le modèle a un **vrai accès aux données**, sans jamais écrire de SQL :
  - **Répartition « X par Y »** (`AnalyticsQueryService`) : le modèle choisit une **dimension** (PROJECT/STATUS/ASSIGNEE/PRIORITY/TYPE) × **mesure** (COUNT/POINTS) × **périmètre** (ALL/OPEN/DONE) dans une **whitelist** ; ces choix sont mappés à des fragments SQL figés, seuls les `projectIds` du workspace sont des paramètres liés → **aucune injection**, données 100 % réelles. Couvre une large classe de questions (« nombre d'issues par projet », « ouvertes par assigné », « story points par statut »…).
  - **Série temporelle** : datasets fixes (throughput / burndown / capacity / workload / projects), chargés par le front.
  - Hors périmètre → `unsupported` explicite ; repli déterministe par mots-clés si LLM absent.
  [id:: IA-CHART-001] [statut:: done] [parite:: extra] [ref:: core/service/agent/{ChartSpecService,AnalyticsQueryService}.java] (10/07/2026)
  - **Motivation terrain** : « nombre d'issues par projet » renvoyait `unsupported` (approche « dataset fixe » = whack-a-mole). Le moteur de requête sûr remplace l'ajout d'un dataset par question. Preuves : « nombre d'issues par projet » → breakdown PROJECT/COUNT/ALL avec données réelles (Solo 150, Web 43…) ; « ouvertes par assigné » → ASSIGNEE/OPEN.
  - **Anti-refus + suggestions (10/07/2026)** : le modèle refusait à tort (« les plus chargés sur 14 jours » → `unsupported` alors que = workload/heatmap). Prompt durci : **répondre par la vue la plus proche** plutôt que refuser (charge/personne → ASSIGNEE ou capacity ; « sur N jours » → workload ; une fenêtre temporelle n'est pas un obstacle). Et quand la demande est **vraiment** hors-périmètre (revenus, marketing…), la réponse `unsupported` porte des **`suggestions`** (2-3 reformulations `{label, prompt}` répondables) que le front affiche en **chips cliquables** → relance la génération. Preuves : « les plus chargés sur 14 jours » → workload/heatmap ; « chiffre d'affaires » → unsupported + 3 suggestions IA cliquables.
- [x] **Prédictions pilotées par le modèle** : 3ᵉ capacité de `POST /analytics/chart` — `"predict": "SUCCESS"` → **score de succès 0-100 par projet** calculé sur **données réelles** (70 % taux de complétion + 30 % ponctualité, via `AnalyticsQueryService.predict`, un seul `IN (?)` lié → anti-injection). Déterministe et explicable (« pas de la voyance »), jamais inventé ; **le modèle décide quand l'utiliser** (retour user : « laisser le modèle décider »). Rendu comme une répartition (barres), instantané (donnée dans le spec). Preuve : « predictions de succès des projets » → « Chances de succès par projet », Infra 73 / Solo 69 / API 69 / Web 60 (= requête psql). `ChartSpecServiceTest` +6 cas. [id:: IA-CHART-002] [statut:: done] [parite:: extra] [ref:: core/service/agent/{ChartSpecService,AnalyticsQueryService}.java] (11/07/2026)

## À faire
- [ ] Abonner le front à `/topic/analysis.{workspaceId}` (STOMP) — le backend publie déjà, le dock retombe sur un polling 5 s [id:: IA-DEC-004] [statut:: todo] [prio:: P2] [besoin-backend:: néant] (10/07/2026)
- [ ] Exploiter les priorités `DISMISSED` comme signal de feedback (mesurer les recommandations suivies vs écartées) [id:: IA-DEC-005] [statut:: todo] [prio:: P3]
- [ ] Vrai streaming SSE de l'assistant [id:: IA-AS-002] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-001] (PC-009)
- [ ] Cache Insights (`ai_runs`/`insight_snapshots`) + garde quota/timeout Groq [id:: IA-IN-002] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-002] (PC-007)
- [ ] Feature flags IA [id:: IA-CFG-001] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-003] (PC-014)
- [ ] Décision `ai-service` Python : supprimer ou documenter legacy [id:: IA-LEG-001] [statut:: todo] [prio:: P3] [besoin-backend:: BE-IA-004] (PC-012)

## ▶ Prochaine action
Brancher le dock sur STOMP (`IA-DEC-004`) : le backend publie déjà chaque transition de plan sur
`/topic/analysis.{workspaceId}`, mais `lib/hooks/use-stomp.ts` ne sait s'abonner qu'aux canaux de chat.
Extraire la connexion/fallback SockJS du hook avant d'ajouter un second abonnement (ne pas dupliquer les ~90 lignes).

---
**Dernière mise à jour :** 11/07/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
