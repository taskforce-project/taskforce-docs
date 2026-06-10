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
- [x] Persistance JPA + Flyway V1–V35 + AuditableEntity [id:: BE-DB-001] [statut:: done] [parite:: ok] [ref:: src/main/resources/db/migration]
- [x] Enveloppe `ApiResponse<T>` + GlobalExceptionHandler [id:: BE-CORE-002] [statut:: done] [parite:: ok]

## 2. Domaines existants (fait)

- [x] Workspaces / membres / rôles [id:: BE-WS-001] [statut:: done] [parite:: ok]
- [x] Projets / membres / labels / statuts / types [id:: BE-PRJ-001] [statut:: done] [parite:: ok]
- [x] Issues : CRUD, commentaires, activité, relations, smart-assign [id:: BE-ISS-001] [statut:: done] [parite:: ok]
- [x] Analytics (KPIs, burndown, throughput, capacité, insights) [id:: BE-ANA-001] [statut:: done] [parite:: ok]
- [x] Notifications [id:: BE-NOTIF-001] [statut:: done] [parite:: ok]
- [x] Intégrations GitHub/Slack + Webhooks (endpoints `/api`) [id:: BE-INT-001] [statut:: done] [parite:: ok] [ref:: core/api/IntegrationController.java]
- [x] Pièces jointes + MinIO [id:: BE-ATT-001] [statut:: done] [parite:: ok] [ref:: modules/ged]
- [x] Roadmap (issues planifiées) [id:: BE-ROAD-001] [statut:: done] [parite:: ok]

## 3. P0 — réparations

- [ ] Ajouter `/api` à Cycle/Team/Page/Discussion/Channel [id:: BE-FIX-001] [statut:: broken] [prio:: P0] [ref:: core/api + modules/chat/api] (PC-001 — débloque BE-CYC-001, BE-PAGE-001, BE-DISC-001, BE-TEAM-001, BE-CHAT-001)
- [ ] Implémenter webhooks Stripe (subscription/invoice) [id:: BE-BILLING-001] [statut:: todo] [parite:: extra] [prio:: P1] [demande-par:: frontend] [ref:: core/api/StripeWebhookController.java] (PC-005)
- [ ] Refresh token + logout (révocation) [id:: BE-AUTH-001] [statut:: todo] [prio:: P1] [demande-par:: frontend] [ref:: core/api/AuthController.java] (PC-004)
- [ ] Notifier l'équipe Sales (email) sur inquiry [id:: BE-SALES-001] [statut:: todo] [prio:: P2] [ref:: modules/sales]

## 4. Demandes du frontend (BE-xxx)

> Items générés par les `[besoin-backend::]` de [Frontend.md](./Frontend.md). Tous `[demande-par:: frontend]`.

- [ ] Cycles : exposer endpoints (après /api) + burndown par cycle [id:: BE-CYC-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Cycles : données vélocité/burndown [id:: BE-CYC-002] [statut:: todo] [prio:: P2] [demande-par:: frontend]
- [ ] Pages/wiki : endpoints (après /api) [id:: BE-PAGE-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Discussions : endpoints (après /api) [id:: BE-DISC-001] [statut:: broken] [prio:: P0] [demande-par:: frontend]
- [ ] Chat : endpoints + STOMP (après /api) [id:: BE-CHAT-001] [statut:: broken] [parite:: extra] [prio:: P0] [demande-par:: frontend]
- [ ] Teams : endpoints (après /api) [id:: BE-TEAM-001] [statut:: broken] [parite:: extra] [prio:: P1] [demande-par:: frontend]
- [ ] Sous-issues : champ parent + endpoints hiérarchie [id:: BE-ISS-010] [statut:: todo] [parite:: partial] [prio:: P1] [demande-par:: frontend]
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
