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

## 2. Domaines existants (fait)

- [x] Workspaces / membres / rôles [id:: BE-WS-001] [statut:: done] [parite:: ok]
- [x] **Delete workspace** : `DELETE /api/workspaces/{slug}` (OWNER-only, cascade DB) [id:: BE-WS-002] [statut:: done] [parite:: ok] [ref:: WorkspaceService.deleteWorkspace] (PROD-3.3, 20/06/2026)
- [x] **Limites par plan** : workspaces (FREE 2/PRO 10) + membres (FREE 5/PRO 50) enforced → 409 [id:: BE-WS-003] [statut:: done] [parite:: ok] [ref:: WorkspaceService.checkMemberLimit] (PROD-4.2, 20/06/2026) ; reste teams/agents + endpoint d'usage
- [x] Projets / membres / labels / statuts / types [id:: BE-PRJ-001] [statut:: done] [parite:: ok]
- [x] Issues : CRUD, commentaires, activité, relations, smart-assign [id:: BE-ISS-001] [statut:: done] [parite:: ok]
- [x] Smart Assign **preview** (dry-run à la création) + **bulk** (multi-assign) [id:: BE-SA-001] [statut:: done] [parite:: extra] [demande-par:: frontend] [ref:: core/api/IssueController.java (POST …/issues/smart-assign/{preview,bulk}) + SmartAssignService.preview/bulkRecommend] (PROD-1.3/1.9, 20/06/2026)
- [x] Analytics (KPIs, burndown, throughput, capacité, insights) [id:: BE-ANA-001] [statut:: done] [parite:: ok]
- [x] Notifications [id:: BE-NOTIF-001] [statut:: done] [parite:: ok]
- [x] **Alertes de surcharge** : `OverloadAlertScheduler` (cron) + `NotificationService.notifyOverload` (seuil configurable, dédup, notifie OWNER/ADMIN) [id:: BE-NOTIF-002] [statut:: done] [parite:: extra] [ref:: core/service/OverloadAlertScheduler.java] (PROD-1.5, 20/06/2026)
- [x] **Temps réel issues** : `IssueService` publie `IssueRealtimeEvent` sur `/topic/projects.{id}` (create/update/delete) [id:: BE-RT-001] [statut:: done] [parite:: extra] [ref:: core/service/IssueService.java] (PROD-1.6, 20/06/2026 — reste topic workspace pour dashboard/analytics)
- [x] Intégrations GitHub/Slack + Webhooks (endpoints `/api`) [id:: BE-INT-001] [statut:: done] [parite:: ok] [ref:: core/api/IntegrationController.java]
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

- [ ] Couverture tests ≥ 50 % (JUnit/Mockito) + JaCoCo [id:: BE-QA-001] [statut:: todo] [prio:: P1] (TF-TEST-002)
- [ ] Tests d'intégration (Testcontainers PostgreSQL/Keycloak) [id:: BE-QA-002] [statut:: todo] [parite:: extra] [prio:: P2]
- [ ] Compléter OpenAPI + publier la doc API [id:: BE-QA-003] [statut:: todo] [prio:: P1]
- [ ] Revue OWASP + rate limiting + secrets management [id:: BE-SEC-002] [statut:: todo] [prio:: P1]
- [ ] Scan dépendances (OWASP Dependency-Check) bloquant en CI [id:: BE-SEC-003] [statut:: todo] [prio:: P2]
- [ ] Journalisation structurée + audit [id:: BE-OPS-001] [statut:: todo] [prio:: P1]

---

> **Note Brain OS** — Vérifier la cohérence des `id` avec les `besoin-backend` de [Frontend.md](./Frontend.md)
> (requête Dataview du [hub §4](./README.md)). Réparations P0 détaillées dans
> [`.ai/P0-fix-plan.md`](../../../taskforce-fullstack/.ai/P0-fix-plan.md).

**Dernière mise à jour :** 09/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
