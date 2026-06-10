---
type: documentation-technique
statut: draft
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [technique, modules, domaines, dépendances, base-de-données]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Cartographie des Modules

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Source vérifiée: code](https://img.shields.io/badge/Source-code%20v%C3%A9rifi%C3%A9-brightgreen?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Architecture globale](./Architecture.md)
- [Contrats API](../05-api/API.md)
- [Dette technique](../09-audits/Dette_Technique.md)

**Tags :** `#technique` `#modules` `#domaines` `#dépendances`

## Table des matières

1. [Domaines fonctionnels](#1-domaines-fonctionnels)
2. [Règles de dépendance backend](#2-règles-de-dépendance-backend)
3. [Stores frontend](#3-stores-frontend)
4. [Chronologie des migrations](#4-chronologie-des-migrations)

---

## 1. Domaines fonctionnels

<p class="lead">
Chaque domaine est une tranche verticale : contrôleur → service → repository → entité côté backend, et
service → store → routes côté frontend. L'état « Santé » est réconcilié avec
<a href="../09-audits/Problemes_Connus.md">Problèmes connus</a>.
</p>

| Domaine | Backend (contrôleur · service) | Frontend (service · store) | Santé |
| ------- | ------------------------------ | -------------------------- | :---: |
| Auth & Inscription | `AuthController` · `AuthService`,`KeycloakService`,`OtpService`,`EmailService`,`JwtService` | `auth-service` · `auth-context` | ✅ (refresh/logout stubés) |
| Facturation | `Stripe*Controller` · `StripeService` | `stripe-service` | ⚠️ webhooks stubés |
| Profil utilisateur | `User`/`ProfileController` · `UserService`,`ProfileService` | `user`/`profile-service` · `user`/`profile-store` | ⚠️ import profile-service |
| Workspace (tenant) | `WorkspaceController` · `WorkspaceService` | `workspace-service` · `workspace-store` | ✅ |
| Projet | `ProjectController` · `ProjectService` | `project`/`label-service` · `project`/`label-store` | ✅ |
| Issues | `IssueController` · `IssueService`,`SmartAssignService` | `issue-service` · `issue-store` | ✅ |
| Cycles (sprints) | `CycleController` · `CycleService` | `cycle-service` · `cycle-store` | ❌ 404 (`/api`) |
| Roadmap | `RoadmapController` · `IssueService` | `issue-service.getScheduledIssues` | ❌ route front absente |
| Teams | `TeamController` · `TeamService` | `team-service` · `team-store` | ❌ 404 + store incomplet |
| Pages (wiki) | `PageController` · `PageService` | `page-service` · `page-store` | ❌ 404 (`/api`) |
| Discussions | `DiscussionController` · `DiscussionService` | `discussion-service` · `discussion-store` | ❌ 404 (`/api`) |
| Chat (temps réel) | `ChannelController`,`ChatWebSocketController` · `ChannelService`,`ChatMessageService` | `message-service` · `message-store` (+ mock `messages/data.ts`) | ❌ 404 + route absente + mock |
| Notifications/Inbox | `NotificationController` · `NotificationService` | `notification-service` · `notification-store` | ✅ |
| Analytics | `AnalyticsController` · `AnalyticsService` | `analytics-service` | ✅ |
| Assistant IA | `AssistantController` · `AssistantService`,`GroqService` | FAB / command palette | ⚠️ streaming simulé |
| AI Insights | `AnalyticsController /insights` · `AnalyticsService`,`GroqService` | `analytics-service.getAiInsights` | ⚠️ pas de cache |
| Smart Assign | `IssueController /smart-assign` · `SmartAssignService`,`GroqService` | `issue-service.smartAssignIssue` · `smart-assign-panel` | ✅ (repli Groq) |
| Pièces jointes (GED) | `AttachmentController`,`FileController` · `AttachmentService`,`MinioService` | `attachment-service` | ❌ route front absente |
| Intégrations | `IntegrationController`,`WebhookController` · `GitHub`/`Slack`/`WebhookService` | `integration-service` · `integration-store` | ❌ route front absente |
| Sales (leads) | `SalesController` · `SalesService` | dialog contact entreprise | ⚠️ notification stub |

## 2. Règles de dépendance backend

```
   modules/   (chat · ged · sales)        ← peuvent utiliser core + shared
      │
   core/      (services, entités, repos)  ← peut utiliser shared
      │
   shared/    (config · security · audit · dto · exception)
```

<blockquote class="important">
Les dépendances pointent vers le bas uniquement. <code>shared</code> ignore <code>core</code>/<code>modules</code> ;
<code>core</code> ignore <code>modules</code>.
</blockquote>

Couplages transverses notables dans `core` : `AnalyticsService`, `AssistantService`, `SmartAssignService`
lisent les données Issue/Cycle/membres ; `AuthService` orchestre `KeycloakService` + `StripeService` +
`OtpService`/`EmailService` ; tous les services scopés workspace dépendent de `WorkspaceService` pour
l'autorisation ; `GroqService` est le client Groq partagé (Assistant, SmartAssign, Insights). Côté infra :
`chat` → RabbitMQ/STOMP, `ged` → MinIO, `sales` → autonome.

## 3. Stores frontend

Stores **Zustand** dans `frontend/lib/store/`, un par domaine, appelant un (parfois deux) service(s) :
`user`, `workspace`, `project`, `issue`, `cycle`, `label`, `page`, `team` *(incomplet)*, `discussion`,
`message`, `notification`, `profile`, `integration`, `preferences` (local). La plupart indexent leurs
données par slug de workspace / `projectId` ; changer de workspace devrait réinitialiser les stores
dépendants. `auth-context` conditionne l'ensemble.

## 4. Chronologie des migrations

Migrations Flyway dans `backend/tf-api/src/main/resources/db/migration/`.

| Plage | Thème |
| ----- | ----- |
| V1–V12 | Bootstrap : users/companies, auth + abonnements + OTP, nettoyage plan-type (`PREMIUM`→`PRO`), champs contact entreprise, colonnes profil |
| V13–V16 | Cœur multi-tenant : workspaces (+UUID), projets/membres/labels, issues (+statuts/types/commentaires/activité/relations) |
| V17–V18, V31 | Données de seed dev/QA |
| V19–V22 | UX issues : icônes projet, ordre `position` (drag), relations enrichies |
| V23–V30 | Tables features : cycles, notifications, pages, teams, discussions, chat, pièces jointes, intégrations |
| V32–V35 | IA : `ai_documents` (pgvector), `member_skill_profiles`, `assignment_events`, `ai_runs` + `insight_snapshots` |

---

> **Note Brain OS** — Vérifié dans le code au 08/06/2026 (branche `feat/dashboard`).

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
