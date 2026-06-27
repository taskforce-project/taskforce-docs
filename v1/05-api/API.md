---
type: documentation-technique
statut: draft
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [technique, api, contrats, backend, frontend]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Contrats API — Frontend ↔ Backend

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Source vérifiée: code](https://img.shields.io/badge/Source-code%20v%C3%A9rifi%C3%A9-brightgreen?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Architecture globale](../03-architecture/Architecture.md)
- [Cartographie des modules](../03-architecture/Modules.md)
- [Problèmes connus](../09-audits/Problemes_Connus.md)

**Tags :** `#technique` `#api` `#contrats`

## Table des matières

1. [Convention de lecture](#1-convention-de-lecture)
2. [Chemins de base des contrôleurs](#2-chemins-de-base-des-contrôleurs)
3. [Cartographie par domaine](#3-cartographie-par-domaine)
4. [Incohérences détectées](#4-incohérences-détectées)
5. [Procédure pour câbler un nouvel endpoint](#5-procédure-pour-câbler-un-nouvel-endpoint)

---

## 1. Convention de lecture

<p class="lead">
Ce document met en correspondance chaque service API du frontend avec son contrôleur backend, et
signale chaque divergence. URL de base backend : <code>http://&lt;hôte&gt;:8080</code>. Comme
<strong>aucun <code>context-path</code> n'est configuré</strong>, l'URL réellement servie par un endpoint
est exactement la valeur de son <code>@RequestMapping</code>. Le frontend, lui, préfixe toujours
<code>/api</code>.
</p>

- **✅ Aligné** — chemin front == chemin back ; fonctionne.
- **❌ Cassé (404)** — l'endpoint existe côté back mais à un chemin différent de l'appel front.
- **❌ Cassé (undefined)** — le front importe une constante de route inexistante → erreur JS au runtime.

## 2. Chemins de base des contrôleurs

Vérité terrain (valeurs `@RequestMapping`, dans `backend/tf-api/src/main/java/.../core/api/` et `modules/*/api/`).

| Contrôleur | `@RequestMapping` | `/api` ? |
| ---------- | ----------------- | :------: |
| AuthController | `/api/auth` | ✅ |
| UserController | `/api/users` | ✅ |
| WorkspaceController | `/api/workspaces` | ✅ |
| ProjectController | `/api/workspaces/{slug}/projects` | ✅ |
| IssueController | `/api/workspaces/{slug}/projects/{projectId}/issues` | ✅ |
| AnalyticsController | `/api/workspaces/{slug}/analytics` | ✅ |
| AssistantController | `/api/workspaces/{slug}/assistant` | ✅ |
| ProfileController | `/api/workspaces/{slug}/profile` | ✅ |
| NotificationController | `/api/workspaces/{slug}/notifications` | ✅ |
| RoadmapController | `/api/workspaces/{slug}/roadmap` | ✅ |
| WebhookController | `/api/workspaces/{slug}/webhooks` | ✅ |
| IntegrationController | `/api/workspaces/{slug}/integrations/...` + `/api/integrations/*/callback` | ✅ |
| StripeController / StripeWebhookController | `/api/stripe` · `/api/webhooks` | ✅ |
| SalesController | `/api/sales` | ✅ |
| FileController / AttachmentController (ged) | `/api/files` · `/api/workspaces/{slug}/projects/{projectId}/issues/{issueId}/attachments` | ✅ |
| **CycleController** | `/workspaces/{slug}/projects/{projectId}/cycles` | ❌ **manquant** |
| **TeamController** | `/workspaces/{slug}/teams` | ❌ **manquant** |
| **PageController** | `/workspaces/{slug}/projects/{projectId}/pages` | ❌ **manquant** |
| **DiscussionController** | `/workspaces/{slug}/discussions` | ❌ **manquant** |
| **ChannelController** (chat) | `/workspaces/{slug}/channels` | ❌ **manquant** |

<blockquote class="important">
Les 5 contrôleurs sans <code>/api</code> sont injoignables aux URL appelées par le frontend → 404. Voir §4.1.
</blockquote>

## 3. Cartographie par domaine

Services front dans `frontend/lib/api/`. Lecture : `fonction front` → `méthode HTTP chemin` → contrôleur.

**Aligné ✅** — Auth (`auth-service` ↔ `AuthController`), Utilisateur (`user-service` ↔ `UserController`),
Workspace (`workspace-service`), Projet + Labels (`project-service`, `label-service` ↔ `ProjectController` :
CRUD, `/members`, `/teams`, `/labels`, **`GET /{id}/activity?days=N`** = activité quotidienne pour la sparkline carte projet, QA2-32),
Issue (`issue-service` ↔ `IssueController` : CRUD, **`GET /paged?page&size`** = liste paginée additive pour l'infinite-scroll backlog (QA2-33), `/statuses` + `/reorder`, `/types`, `/comments`,
`/activity`, `/smart-assign`, `/relations`), Analytics (`analytics-service` : `/kpis`, **`/throughput?bucket=DAY|WEEK`** = série throughput, `WEEK` (8 sem., défaut) ou `DAY` (30 j, tendance « 1 mois » du dashboard ; 26/06/2026),
`/burndown`, `/capacity`, `/insights`), Notifications (`notification-service`), Sales, Avatars (`FileController`).

**Cassé (404) ❌** — Cycles (`cycle-service` ↔ `CycleController`), Pages wiki (`page-service` ↔ `PageController`) :
le front appelle `/api/workspaces/…`, le back sert `/workspaces/…`. Voir §4.1.
> ⚠️ Note (24/06/2026) : **Discussions aligné** — `DiscussionController` porte bien `@RequestMapping("/api/workspaces/{slug}/discussions")`, feature fonctionnelle (list/create/pin/lock/state). Teams également corrigé (cf. Frontend.md FE-TEAM-*). Re-vérifier Cycles/Pages avant de les laisser ici.

**Cassé (undefined) ❌** — Messages (`message-service`, `MESSAGE_ROUTES`), Intégrations
(`integration-service`, `INTEGRATION_ROUTES`), Pièces jointes (`attachment-service`, `ATTACHMENT_ROUTES`),
Roadmap (`issue-service.getScheduledIssues`, `ROADMAP_ROUTES`) : constantes importées mais **non déclarées**
dans `api-routes.ts`. Les endpoints back des intégrations/pièces jointes/roadmap **existent** (avec `/api`) ;
pour les messages, le back est en plus mal préfixé (cf. §4.1). Voir §4.2.

**Dégradé ⚠️** — Profil (`profile-service` : chemin OK mais import cassé, §4.3), Refresh auth (§4.4),
écritures Stripe (handlers de webhook stubés — cf. [Dette technique DT-005](../09-audits/Dette_Technique.md)).

Groupes de routes **présents** dans `frontend/lib/config/api-routes.ts` : `AUTH`, `STRIPE`, `USER`,
`WORKSPACE`, `PROJECT`, `ISSUE`, `CYCLE`, `ANALYTICS`, `NOTIFICATION`, `PROFILE`, `PAGE`, `TEAM`,
`DISCUSSION`. **Absents** (importés mais jamais déclarés) : `MESSAGE_ROUTES`, `INTEGRATION_ROUTES`,
`ATTACHMENT_ROUTES`, `ROADMAP_ROUTES`.

## 4. Incohérences détectées

### 4.1 — Préfixe `/api` manquant sur 5 contrôleurs → 404 (HAUTE)

`CycleController`, `TeamController`, `PageController`, `DiscussionController`, `ChannelController`
déclarent des chemins **sans** `/api`. Aucun `context-path` n'étant configuré (vérifié dans
`application.yml`, `-dev`, `-prod`), ils sont servis sous `/workspaces/…` alors que le front appelle
`/api/workspaces/…`. **Résultat : Cycles, Teams, Pages, Discussions et Chat échouent en 404.** Cause :
hypothèse périmée (`CorsConfig.java:65` « avec context-path=/api ») jamais appliquée. → [PC-001](../09-audits/Problemes_Connus.md).

### 4.2 — Constantes de routes front absentes → erreur runtime (HAUTE)

`message-service.ts`, `integration-service.ts`, `attachment-service.ts` et
`issue-service.ts::getScheduledIssues` importent des constantes absentes de `api-routes.ts`. Tout appel
lève `Cannot read properties of undefined`. → [PC-002](../09-audits/Problemes_Connus.md).

### 4.3 — Import cassé dans `profile-service.ts` (MOYENNE)

Ligne 1 : `import apiClient from "./api-client";` — le module `./api-client` n'existe pas ; le vrai
client est l'export **nommé** `apiClient` de `./client`. `getProfile()` échoue au runtime. → [PC-003](../09-audits/Problemes_Connus.md).

### 4.4 — Désalignement du refresh auth (MOYENNE)

Front : `AUTH_ROUTES.REFRESH_TOKEN = /api/auth/refresh` ; back : méthode mappée sur
`/api/auth/refresh-token` **et** non implémentée (TODO). La séquence `401 → refresh → retry` du
`client.ts` ne peut pas aboutir. → [PC-004](../09-audits/Problemes_Connus.md).

## 5. Procédure pour câbler un nouvel endpoint

<div class="highlight-box">

1. Déclarer le chemin du contrôleur **avec `/api`** (`@RequestMapping`).
2. Ajouter la constante dans `frontend/lib/config/api-routes.ts`.
3. La consommer dans le service `lib/api/*-service.ts`.
4. Lire `response.data.data` (enveloppe `ApiResponse<T>`).
5. Mettre à jour [ce document](./API.md) et le [hub](../../Brain_OS.md).

</div>

---

> **Note Brain OS** — Vérifié dans le code au 08/06/2026 (branche `feat/dashboard`).

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
