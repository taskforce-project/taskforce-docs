---
id: produit-backend
title: État Produit — Backend
doc_type: register
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, backend]
related:
  - "./README.md"
  - "./Frontend.md"
  - "../03-architecture/Architecture.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# État Produit — Backend (`backend/tf-api/`)

**Version :** 1.0 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: backend](https://img.shields.io/badge/R%C3%A9pertoire-backend-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [Fiche Frontend](./Frontend.md) · [Architecture](../03-architecture/Architecture.md) · [🧠 Brain OS](../../Brain_OS.md)

**Tags :** `#produit` `#suivi` `#backend`

<p class="lead">
Stack : Spring Boot 4 · Java 21 · PostgreSQL 18 + pgvector · Keycloak · Stripe · MinIO · RabbitMQ/STOMP ·
Groq. Les items <code>[demande-par:: frontend]</code> répondent à un <code>besoin-backend</code> de la
<a href="./Frontend.md">fiche Frontend</a> (l'<code>id</code> doit correspondre).
</p>

## Table des matières
1. [Socle & sécurité](#1-socle--sécurité)
2. [Domaines existants](#2-domaines-existants-fait)
3. [P0 — réparations](#3-p0--réparations)
4. [Demandes du frontend (BE-xxx)](#4-demandes-du-frontend-be-xxx)
5. [Nouveaux domaines (gaps fonctionnels)](#5-nouveaux-domaines-gaps-fonctionnels)
6. [IA / Facturation](#6-ia--facturation)
7. [Qualité (tests, sécurité, API)](#7-qualité-tests-sécurité-api)

---

## 1. Socle & sécurité

**Fait :**
- [x] Architecture en couches `shared/core/modules` [id:: BE-CORE-001] [statut:: done] [parite:: ok] [ref:: backend/tf-api/src/main/java/com/taskforce/tf_api]
- [x] Sécurité Keycloak OAuth2/OIDC (resource server JWT) [id:: BE-SEC-CORE] [statut:: done] [parite:: ok] [ref:: shared/security/SecurityConfig.java]
- [x] **RBAC centralisé** : `AuthorizationService` + **`WorkspaceAccessInterceptor`** (exige l'appartenance pour tout `/api/workspaces/{slug}/…`) → ferme les IDOR globalement [id:: BE-AUTHZ-001] [statut:: done] [parite:: ok] [ref:: core/security/WorkspaceAccessInterceptor.java + core/config/WebMvcConfig.java] (PROD-3.2, 20/06/2026)
- [x] **IDOR Team/Page/Discussion/Analytics** : fermés par l'interceptor (+ Analytics aussi en défense en profondeur) [id:: BE-AUTHZ-002] [statut:: done] [prio:: P1] (20/06/2026)
- [ ] RBAC granulaire façon GitHub (rôles/permissions custom, par team/membre) [id:: BE-AUTHZ-003] [statut:: todo] [prio:: P2] (PROD-3.9, épic)
- [ ] Config entreprise/on-premise : realm Keycloak dédié [id:: BE-AUTHZ-004] [statut:: todo] [prio:: P3] (PROD-3.10, épic)
- [x] Persistance JPA + Flyway V1–V39 + AuditableEntity [id:: BE-DB-001] [statut:: done] [parite:: ok] [ref:: src/main/resources/db/migration]
- [x] **Checklist d'issue** : `V39__issue_checklist_items` + entité/repo + CRUD endpoints [id:: BE-CHK-001] [statut:: done] [parite:: ok] [ref:: core/service/IssueService (listChecklist/add/update/delete)] (PROD-2.3, 20/06/2026)
- [x] Enveloppe `ApiResponse<T>` + GlobalExceptionHandler (IllegalState→409 / IllegalArgument→400, plus de 500 métier) [id:: BE-CORE-002] [statut:: done] [parite:: ok] (PROD-4.8, 20/06/2026)
- [x] **Rate limiting : préflights exclus + contrat 429 exploitable** : `RateLimitFilter` (bucket4j, par IP, `OncePerRequestFilter` sur `/api/*` **avant** Spring Security) comptait **aussi** les préflights CORS `OPTIONS` — le front étant sur une autre origine (`localhost:3000` → `localhost:8080`), chaque requête non simple en générait un → **quota réel divisé par deux**. `shouldNotFilter` les exclut désormais. Le 429 était par ailleurs **muet** : aucun `Retry-After`, alors que le profil `DEFAULT` (200 req/60 s) utilise `refillIntervally` — tous les jetons rendus **d'un coup** en fin de fenêtre, donc une attente réelle de **0 à 60 s**, indevinable côté client. Le filtre émet `Retry-After` + `X-RateLimit-Remaining`, **déclarés dans `CorsConfig.setExposedHeaders`** (sans quoi le navigateur les masque au JS en cross-origin). **Mesures live** : 20 préflights → **0 jeton** consommé (199 → 198) ; 429 → `Retry-After: 57` [id:: BE-SEC-004] [statut:: done] [parite:: ok] [ref:: shared/security/RateLimitFilter.java + shared/config/CorsConfig.java] (PC-033, 20/07/2026)

## 2. Domaines existants (fait)

- [x] Workspaces / membres / rôles [id:: BE-WS-001] [statut:: done] [parite:: ok]
- [x] **Delete workspace** : `DELETE /api/workspaces/{slug}` (OWNER-only, cascade DB) [id:: BE-WS-002] [statut:: done] [parite:: ok] [ref:: WorkspaceService.deleteWorkspace] (PROD-3.3, 20/06/2026)
- [x] **Limites par plan** : workspaces (FREE 2/PRO 10) + membres (FREE 5/PRO 50) enforced → 409 [id:: BE-WS-003] [statut:: done] [parite:: ok] [ref:: WorkspaceService.checkMemberLimit] (PROD-4.2, 20/06/2026) ; reste teams/agents + endpoint d'usage
- [x] Projets / membres / labels / statuts / types [id:: BE-PRJ-001] [statut:: done] [parite:: ok]
- [x] Issues : CRUD, commentaires, activité, relations, smart-assign [id:: BE-ISS-001] [statut:: done] [parite:: ok] — **fix 02/07** : `addRelation` cassait contre PG (`operator does not exist: issue_relation_type = character varying`) car `IssueRelation.relationType` n'avait pas `@JdbcTypeCode(SqlTypes.NAMED_ENUM)` ; ajouté (+ retrait `length=20`), aligné sur `Issue.priority`/`IssueStatus.category` (aucune migration). Test d'intégration `should_add_relation` remis, vert.
- [x] Smart Assign **preview** (dry-run à la création) + **bulk** (multi-assign) [id:: BE-SA-001] [statut:: done] [parite:: extra] [demande-par:: frontend] [ref:: core/api/IssueController.java (POST …/issues/smart-assign/{preview,bulk}) + SmartAssignService.preview/bulkRecommend] (PROD-1.3/1.9, 20/06/2026)
- [x] Analytics (KPIs, burndown, throughput, capacité, insights) [id:: BE-ANA-001] [statut:: done] [parite:: ok]
- [x] **Throughput bucketable** : `GET /analytics/throughput?bucket=DAY|WEEK` — `WEEK` = 8 sem. (défaut, inchangé), `DAY` = 30 j glissants (tendance « 1 mois » du dashboard). Logique factorisée `buildThroughput(projectIds, points, daily)` [id:: BE-ANA-002] [statut:: done] [parite:: extra] [ref:: core/service/AnalyticsService.java + core/api/AnalyticsController.java] (26/06/2026)
- [x] **Seed démo enrichi** : +24 contributeurs « solo » (hors équipe) + projet « Solo Initiatives » + ~150 issues sur 30 j → throughput journalier/KPIs/capacité remplis (données réelles, pas de mock) [id:: BE-SEED-002] [statut:: done] [parite:: extra] [ref:: backend/tf-api/seed/dev_seed.sql] (26/06/2026)
- [x] **Seed — échéances + discussions** : `UPDATE` d'échéances **relatives à `CURRENT_DATE`** sur les issues ouvertes+assignées, réparties sur `[-3 j, +13 j]` → remplit la **heatmap de charge** (US-022, 69 cellules non-nulles vs 0) et les compteurs « en retard »/« échéance proche » du Decision Board, quel que soit le jour du re-run. Table `discussions` (auparavant vide) peuplée de 6 fils réalistes (catégories/états variés). *(Constat : le seed était déjà riche partout — seuls due dates, discussions et attachments manquaient ; attachments non seedés car exigent de vrais objets MinIO.)* [id:: BE-SEED-003] [statut:: done] [parite:: extra] [ref:: backend/tf-api/seed/dev_seed.sql] (10/07/2026)
- [x] Notifications [id:: BE-NOTIF-001] [statut:: done] [parite:: ok]
- [x] **Alertes de surcharge** : `OverloadAlertScheduler` (cron) + `NotificationService.notifyOverload` (seuil configurable, dédup, notifie OWNER/ADMIN) [id:: BE-NOTIF-002] [statut:: done] [parite:: extra] [ref:: core/service/OverloadAlertScheduler.java] (PROD-1.5, 20/06/2026)
- [x] **Liens de notification réparés (`V71`)** : la table `notifications` ne porte **aucune clé étrangère** vers `issues`/`projects` — `issue_url`/`project_url` sont **dénormalisées à l'écriture** par `NotificationService.buildNotification`, à partir du slug et des ids. Conséquence : toute ligne insérée **hors du code Java** (le seed) naît avec des liens `NULL` et **rien ne permet de les reconstruire à la lecture** → **35 lignes sur 266** affichaient « WEB-3 » sans que le clic ne mène nulle part. Migration **`V71__backfill_notification_urls.sql`** : décompose `issue_identifier` (« WEB-3 » → identifiant projet + n° de séquence), rejoint `projects`/`issues`, avec un filet ramenant **au moins au projet** ; idempotente (ne touche que les `NULL`). `seed/dev_seed.sql` corrigé en miroir (résolution des liens en fin de seed, identifiants du bloc de volume tirés d'issues **réelles** au lieu d'être fabriqués `'WEB-' || n`, signal de surcharge aligné sur la convention Java `overload-<userId>`). **Mesure post-migration : 265/266** ; reste 1 ligne (`overload` historique, `issue_identifier` `NULL`) irrécupérable par jointure, corrigée au prochain reseed [id:: BE-NOTIF-003] [statut:: done] [parite:: ok] [ref:: src/main/resources/db/migration/V71__backfill_notification_urls.sql + seed/dev_seed.sql] (PC-032, 20/07/2026)
- [x] **Temps réel issues** : `IssueService` publie `IssueRealtimeEvent` sur `/topic/projects.{id}` (create/update/delete) [id:: BE-RT-001] [statut:: done] [parite:: extra] [ref:: core/service/IssueService.java] (PROD-1.6, 20/06/2026 — reste topic workspace pour dashboard/analytics)
- [x] **Workflows d'analyse IA (async + HITL)** : `analysis_job` / `decision_brief` / `decision_priority` (Flyway **V60**) ; `AnalysisJobRunner` (`@Async`) joue observe → contexte → analyse → clarification → persistance, et publie chaque transition sur `/topic/analysis.{workspaceId}`. Le plan d'étapes est stocké en JSON (contrat `PlanTask` du front) : rouvrir le dock rejoue l'état exact du workflow. Priorités actionnables (`accept` → issue liée, `pin`/`dismiss` bascules, `edit`). [id:: BE-ANL-001] [statut:: done] [parite:: extra] [ref:: core/service/agent/{AnalysisJobService,AnalysisJobRunner,AnalysisPlan}.java + core/api/AnalysisController.java] (10/07/2026)
    - **Piège `@Async`** : le runner est un bean **séparé** (Spring n'applique pas `@Async` sur un auto-appel) et il est déclenché **par le contrôleur**, après le commit de la méthode `@Transactional` — sinon le thread async peut ne pas voir la ligne qu'elle vient d'écrire.
    - **Piège Jackson** : Spring Boot 4 sérialise en **Jackson 3** (`tools.jackson`) alors que les services manipulent un `ObjectMapper` **Jackson 2**. Un `JsonNode` Jackson 2 exposé dans un DTO ressort en `{"array":true,"bigDecimal":false,…}` (constaté puis corrigé le 10/07). Les DTO n'exposent que des types du JDK (`List<Map<String,Object>>`).
- [x] **`DecisionService` recentré** sur le raisonnement (observe / contexte RAG / analyse), sans autorisation ni persistance : réutilisable par le workflow. `analyze()` est volontairement **hors transaction** (l'appel LLM dure des minutes ; garder une connexion ouverte épuiserait le pool). [id:: BE-ANL-002] [statut:: done] [parite:: extra] [ref:: core/service/agent/DecisionService.java] (10/07/2026)
- [x] ~~`DecisionController` (`POST /projects/{id}/decision`, synchrone, non persisté)~~ — **supprimé**, remplacé par les workflows ci-dessus [id:: BE-DEC-001] [statut:: done] (10/07/2026)
- [x] **Génération de graphe par l'IA — 2 modes** : `POST /analytics/chart` (`ChartSpecService`) mappe une demande NL vers une `ChartSpecResponse` en mode `timeseries` (référence un dataset réel) **ou `breakdown`** (répartition « X par Y » calculée en base). Via `LlmClient` (LLM local), sortie validée ; hors périmètre → `unsupported`. Repli heuristique si LLM absent [id:: BE-CHART-001] [statut:: done] [parite:: extra] [ref:: core/service/agent/ChartSpecService.java + core/api/AnalyticsController.java] (10/07/2026)
- [x] **Moteur de requête sûr (retrieval DB pour le modèle)** : `AnalyticsQueryService` — le modèle interroge les vraies données sans écrire de SQL. **Whitelist** dimension (PROJECT/STATUS/ASSIGNEE/PRIORITY/TYPE) × mesure (COUNT/POINTS) × périmètre (ALL/OPEN/DONE) → fragments SQL **figés** ; seuls les `projectIds` du workspace sont des paramètres liés (JdbcTemplate) → **anti-injection par construction**, scope workspace garanti. `POST /analytics/breakdown` ré-exécute une répartition (rafraîchit un graphe épinglé) [id:: BE-CHART-002] [statut:: done] [parite:: extra] [ref:: core/service/agent/AnalyticsQueryService.java] (10/07/2026)
- [x] **Graphes épinglés (« Custom »)** : table `saved_chart` (Flyway **V62**, portée workspace) + `SavedChartService` (list/save/delete) + `GET|POST /analytics/charts`, `DELETE /analytics/charts/{id}`. On persiste la **spec** (`ChartSpec` JSON) — jamais les données, recalculées à l'affichage (les breakdowns via `/breakdown`, les timeseries via leurs endpoints) → graphes épinglés **vivants** [id:: BE-CHART-003] [statut:: done] [parite:: extra] [ref:: core/service/agent/SavedChartService.java] (10/07/2026)
- [x] Intégrations GitHub/Slack + Webhooks (endpoints `/api`) [id:: BE-INT-001] [statut:: done] [parite:: ok] [ref:: core/api/IntegrationController.java]
- [x] **Connecteurs génériques — tout le catalogue connectable** : les 44 outils `PLANNED` deviennent `AVAILABLE` via un flux générique. Table `connector_connection` (Flyway **V61**, découplée de l'enum `IntegrationProvider`) : une ligne = un connecteur connecté, `config` = champs (clé/token/endpoint) sérialisés JSON et **chiffrés au repos** (`EncryptedStringConverter`, comme `integrations.access_token`). `ConnectorConnectionService.connect/disconnect` (autorisation + validation des champs requis) ; endpoints génériques `POST|DELETE /integrations/connectors/{key}` (chemin dédié → aucune collision avec GitHub/Slack/Plane, refusés en générique). Champs déduits du mode d'auth (`ConnectorCatalog.defaultFields`). **Honnêteté** : « connecté » = identifiants stockés et état persisté ; la sync des données par service reste l'étape suivante (pas de fausses données). [id:: BE-INT-002] [statut:: done] [parite:: extra] [ref:: core/service/integration/{ConnectorConnectionService,ConnectorCatalog}.java + core/api/IntegrationController.java] (10/07/2026)
- [x] **Catalogue étendu 47 → 129 connecteurs** : ajout curé — dev/test (Postman, VS Code, Cursor, GitLab, Bitbucket, Sentry, Datadog, Grafana…), IA (OpenAI, Anthropic/Claude, Mistral, Gemini, Ollama, Perplexity…), **Google détaillé** (Gmail/Drive/Calendar/Sheets/Meet), **Microsoft** (Teams/Outlook/OneDrive/Azure), comms/paiement/analytics/CRM. Tous `connectable` (mode d'auth déduit, config chiffrée). Preuve : `GET /integrations/catalog` → **total 129, available 129**. Logos front via SVGL (83 réels, 37 absents → initiales). [id:: BE-INT-003] [statut:: done] [parite:: extra] [ref:: core/service/integration/ConnectorCatalog.java] (11/07/2026)
- [x] **Prédiction sur données réelles** : `AnalyticsQueryService.predict(SUCCESS)` → score de succès 0-100 par projet (70 % complétion + 30 % ponctualité), `IN (?)` lié → anti-injection. Exposé au modèle via `ChartSpecService` (`"predict": "SUCCESS"`). [id:: BE-CHART-004] [statut:: done] [parite:: extra] [ref:: core/service/agent/AnalyticsQueryService.java] (11/07/2026)
- [x] Pièces jointes + MinIO [id:: BE-ATT-001] [statut:: done] [parite:: ok] [ref:: modules/ged]
- [x] Roadmap (issues planifiées) [id:: BE-ROAD-001] [statut:: done] [parite:: ok]
- [x] Profils de compétences membres (CRUD `skills_json`, alimente Smart Assign) [id:: BE-SKILL-001] [statut:: done] [parite:: extra] [demande-par:: frontend] [ref:: core/api/MemberSkillController.java + core/service/MemberSkillProfileService.java] (PROD-1.2, 20/06/2026 — table V33 enfin exploitée via CRUD ; autz : soi-même ou ADMIN/OWNER)

## 3. P0 — réparations

- [ ] Ajouter `/api` à Cycle/Team/Page/Discussion/Channel [id:: BE-FIX-001] [statut:: broken] [prio:: P0] [ref:: core/api + modules/chat/api] (PC-001 — débloque BE-CYC-001, BE-PAGE-001, BE-DISC-001, BE-TEAM-001, BE-CHAT-001)
- [ ] Implémenter webhooks Stripe (subscription/invoice) [id:: BE-BILLING-001] [statut:: todo] [parite:: extra] [prio:: P1] [demande-par:: frontend] [ref:: core/api/StripeWebhookController.java] (PC-005)
- [x] **Stripe Customer Portal** : `BillingController POST /api/billing/portal` + `StripeService.createBillingPortalSession` (chemin protégé) [id:: BE-BILLING-002] [statut:: done] [parite:: extra] (PROD-4.5, 20/06/2026 ; nécessite clés Stripe réelles)
- [~] **Feature gating** : `PlanFeature` + `PlanFeatureService` ; **appliqué** aux AI insights (gate → message upgrade FREE) ; admin dev → PRO (V40). Reste : analytics avancées + intégrations [id:: BE-PLAN-001] [statut:: wip] [prio:: P2] (PROD-4.4, 20/06/2026)
- [ ] Refresh token + logout (révocation) [id:: BE-AUTH-001] [statut:: todo] [prio:: P1] [demande-par:: frontend] [ref:: core/api/AuthController.java] (PC-004)
- [x] Notifier l'équipe Sales (email) sur inquiry [id:: BE-SALES-001] [statut:: done] [parite:: ok] [ref:: SalesService + EmailService.sendInternalNotification] (PROD-4.7/KI-008, 20/06/2026 ; envoi réel = config SMTP)
- [x] **Écritures en tx readOnly corrigées** : 500 `/analytics/insights` (readOnly retiré de `generateInsights`) + `ai_runs`/`assignment_events` jamais persistés en smart-assign (`recommend`/`preview` passés read-write) [id:: BE-FIX-006] [statut:: done] [prio:: P1] [ref:: AnalyticsService + SmartAssignService] (FIX-006, 20/06/2026)
- [ ] **Clé Groq absente** (`GROQ_API_KEY` vide dans `.env`) → IA en fallback Java. Action user : ajouter la clé [id:: BE-FIX-007] [statut:: config] [prio:: P1] (FIX-007)
- [~] **Enrichir les signaux Smart Assign** — story points dans la charge ✅ + `historicalScore` calculé depuis `assignment_events` ✅ + expose `reason`/`matchedSkills` (pour le « wow ») ✅ (20/06) ; reste capacité h/sem, séniorité, charge cross-projets, time tracking [id:: BE-SA-002] [statut:: wip] [prio:: P2] [ref:: core/service/SmartAssignService.java] (PROD-1.8 + PROD-8.10)
- [ ] **Seed équipe de test** (realm Keycloak + DB) : users avec séniorité + compétences distinctes [id:: BE-SEED-001] [statut:: todo] [prio:: P2] (PROD-7.6)

## 4. Demandes du frontend (BE-xxx)

> Items générés par les `[besoin-backend::]` de [Frontend.md](./Frontend.md). Tous `[demande-par:: frontend]`.

- [ ] Cycles : exposer endpoints (après /api) + burndown par cycle [id:: BE-CYC-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Cycles : données vélocité/burndown [id:: BE-CYC-002] [statut:: todo] [prio:: P2] [demande-par:: frontend]
- [ ] Pages/wiki : endpoints (après /api) [id:: BE-PAGE-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Discussions : endpoints (après /api) [id:: BE-DISC-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Chat : endpoints + STOMP (après /api) [id:: BE-CHAT-001] [statut:: broken] [parite:: extra] [prio:: P0] [demande-par:: frontend]
- [ ] Teams : endpoints (après /api) [id:: BE-TEAM-001] [statut:: broken] [parite:: extra] [prio:: P1] [demande-par:: frontend]
- [x] Sous-issues : parentId (create/update) + `GET /issues/{id}/children` [id:: BE-ISS-010] [statut:: done] [parite:: ok] [demande-par:: frontend] [ref:: core/service/IssueService.listChildren] (PROD-2.1, 20/06/2026)
- [ ] Estimates : champ `estimate` sur Issue + agrégat cycle [id:: BE-ISS-011] [statut:: todo] [parite:: gap] [prio:: P1] [demande-par:: frontend] (migration Flyway)
- [ ] Time tracking : entité worklog + endpoints [id:: BE-ISS-012] [statut:: todo] [parite:: gap] [prio:: P3] [demande-par:: frontend]
- [ ] Templates de projet : entité + endpoints [id:: BE-PRJ-010] [statut:: todo] [parite:: gap] [prio:: P3] [demande-par:: frontend]
- [ ] Rôle GUEST / accès externes [id:: BE-WS-010] [statut:: todo] [parite:: gap] [prio:: P3] [demande-par:: frontend]
- [ ] Gantt/Timeline : endpoints dépendances/jalons [id:: BE-ROAD-002] [statut:: todo] [parite:: partial] [prio:: P2] [demande-par:: frontend]
- [ ] Assistant : vrai streaming SSE (tokens Groq) [id:: BE-IA-001] [statut:: todo] [parite:: extra] [prio:: P2] [demande-par:: frontend] (PC-009)
- [ ] En-têtes/CSP & sécurité transverse alignés avec le front [id:: BE-SEC-001] [statut:: todo] [prio:: P1] [demande-par:: frontend]
- [x] **« Ma file » : endpoints agrégés cross-projets** — la vue rappelait l'API **projet par projet** (`3 + 2N` requêtes par affichage), assez pour épuiser le rate limiting à l'usage normal. `GET /api/workspaces/{slug}/my-cycles` → `ApiResponse<List<MyWorkCycleResponse>>` (`{projectId, projectName, cycle}`, décompte d'issues **groupé en une requête** via `CycleIssueRepository.countByCycleIds`) et `GET /api/workspaces/{slug}/my-pages` → `ApiResponse<List<MyWorkPageResponse>>` (`{projectId, projectName, page}`, borné à **50 documents récents**). Périmètre des deux : `ProjectVisibilityGuard.viewableProjectIds`. L'enveloppe `{projectId, projectName}` est nécessaire car `CycleResponse`/`PageResponse` sont normalement servis depuis une route **déjà scopée par projet**. `MyWorkController` passe de `@RequestMapping("…/my-issues")` à `@RequestMapping("/api/workspaces/{slug}")` + `@GetMapping("/my-issues")` — **l'URL externe de `/my-issues` est inchangée**. Mesuré : `3+2N` → **3 appels** [id:: BE-MYW-010] [statut:: done] [parite:: ok] [demande-par:: frontend] [ref:: core/api/MyWorkController.java + core/service/{CycleService,PageService}.java] (PC-033, 20/07/2026)
- [~] **Passer les chaînes backend visibles en anglais** (décision produit 20/07/2026 : l'UI applicative est en anglais, **commentaires de code et documentation restent en français**). **Fait** : titres et corps des notifications (`NotificationService` — `— deadline breached` / `— due soon`, alerte de surcharge) + contenu des notifications du seed. **Reste** : messages d'erreur et de succès, catalogue de connecteurs, contenu du seed, et **prompts LLM** (qui génèrent du français à l'exécution) [id:: BE-I18N-001] [statut:: wip] [prio:: P2] [demande-par:: frontend] [ref:: core/service/NotificationService.java + seed/dev_seed.sql] (20/07/2026)

## 5. Nouveaux domaines (gaps fonctionnels)

- [ ] **Modules** : entité Module + rattachement issues + endpoints CRUD [id:: BE-MOD-001] [statut:: todo] [parite:: gap] [prio:: P1] [demande-par:: frontend] (migration Flyway + model + controller + service)
- [ ] **Views** : entité View (filtres/tri/affichage sérialisés) + endpoints [id:: BE-VIEW-001] [statut:: todo] [parite:: gap] [prio:: P1] [demande-par:: frontend]
- [ ] **Intake** : entité Intake/triage + endpoints (capture demandes) [id:: BE-INTK-001] [statut:: todo] [parite:: gap] [prio:: P2] [demande-par:: frontend]
- [ ] **Import/Export** : CSV/JSON + import Jira/Plane [id:: BE-IO-001] [statut:: todo] [parite:: gap] [prio:: P3]
- [ ] Intégration GitLab [id:: BE-INT-010] [statut:: todo] [parite:: gap] [prio:: P3]

## 6. IA / Facturation

- [ ] Cache AI Insights (`ai_runs`/`insight_snapshots`) + garde quota/timeout Groq [id:: BE-IA-002] [statut:: todo] [parite:: extra] [prio:: P2] (PC-007)
- [ ] Feature flags IA [id:: BE-IA-003] [statut:: todo] [prio:: P2] (PC-014)
- [ ] Décision `ai-service` Python : supprimer ou documenter legacy [id:: BE-IA-004] [statut:: todo] [prio:: P3] (PC-012)

## 7. Qualité (tests, sécurité, API)

- [x] Couverture tests ≥ 50 % (JUnit/Mockito) + JaCoCo [id:: BE-QA-001] [statut:: done] [prio:: P1] (TF-TEST-002) — **02/07 : 86,1 % ligne (hors-brain, 5361/6226), 668 tests, 0 échec**. Gate `jacoco:check` **BUNDLE LINE ≥ 0,84** bloquant (`mvn verify`). 3 couches : unitaire (Mockito), intégration (**vrai Postgres** pgvector, Flyway, `ddl-auto=validate`), web (`@WebMvcTest` + SecurityConfig réel). Sécurité/RGPD ~100 % (JWT/OTP/RBAC/RateLimit/chiffrement AES-GCM). **Contract tests wire** (`MockRestServiceServer`) sur les sortants HTTP (Groq/GitHub/Slack/embeddings). Journal détaillé : [`.ai/tests-backend-journal.md`](../../../taskforce-fullstack/.ai/tests-backend-journal.md).
- [x] Tests d'intégration (Postgres réel) [id:: BE-QA-002] [statut:: done] [parite:: extra] [prio:: P2] — **socle `@DataJpaTest` + Postgres pgvector sibling** (Testcontainers KO depuis conteneur vs Docker Desktop 29 → réseau Docker partagé via `scripts/it.ps1`). Keycloak/MinIO/Stripe = SDK non-RestTemplate → validés en **E2E** (non couvert par l'intégration back).
- [ ] Compléter OpenAPI + publier la doc API [id:: BE-QA-003] [statut:: todo] [prio:: P1]
- [ ] Revue OWASP + rate limiting + secrets management [id:: BE-SEC-002] [statut:: todo] [prio:: P1]
- [ ] Scan dépendances (OWASP Dependency-Check) bloquant en CI [id:: BE-SEC-003] [statut:: todo] [prio:: P2]
- [ ] Journalisation structurée + audit [id:: BE-OPS-001] [statut:: todo] [prio:: P1]

---

> **Note Brain OS** — Vérifier la cohérence des `id` avec les `besoin-backend` de [Frontend.md](./Frontend.md)
> (requête Dataview du [hub §4](./README.md)). Réparations P0 détaillées dans
> [`.ai/P0-fix-plan.md`](../../../taskforce-fullstack/.ai/P0-fix-plan.md).

**Dernière mise à jour :** 20/07/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
