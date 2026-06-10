---
type: documentation-technique
statut: draft
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [technique, architecture, backend, frontend, infrastructure]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Architecture Globale

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Source vérifiée: code](https://img.shields.io/badge/Source-code%20v%C3%A9rifi%C3%A9-brightgreen?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Contrats API](../05-api/API.md)
- [Cartographie des modules](./Modules.md)
- [Dette technique](../09-audits/Dette_Technique.md)
- [Problèmes connus](../09-audits/Problemes_Connus.md)

**Tags :** `#technique` `#architecture` `#backend` `#frontend` `#infrastructure`

## Table des matières

1. [Vue d'ensemble](#1-vue-densemble)
2. [Topologie globale](#2-topologie-globale)
3. [Frontend](#3-frontend)
4. [Backend](#4-backend)
5. [Infrastructure & déploiement](#5-infrastructure--déploiement)
6. [Modèle de données](#6-modèle-de-données)
7. [Sécurité & authentification](#7-sécurité--authentification)

---

## 1. Vue d'ensemble

<p class="lead">
Taskforce est un SaaS de gestion de projet multi-tenant (de la famille de Linear/Jira) organisé en
workspaces → projets → issues/cycles, enrichi de chat, discussions, pages wiki, analytics, assistance
IA, facturation et intégrations externes. Le dépôt est un monorepo regroupant quatre applications
déployables et leur infrastructure de support.
</p>

| Couche | Stack | Emplacement | Port (dev) |
| ------ | ----- | ----------- | ---------- |
| Landing | Astro 5.x | `landing-page/` | 18081→4321 |
| Frontend (app) | Next.js 16.1 · React 19.2 · TS 5 · Tailwind 4 | `frontend/` | 3000 |
| Backend API | Spring Boot 4.0 · Java 21 · Maven | `backend/tf-api/` | 8080 (debug 5005) |
| Service IA | FastAPI 0.115 · Python 3.12 — **vestigial** (cf. §5) | `ai-service/` | 8000 |
| Base de données | PostgreSQL 18 + `pgvector` | conteneur | 5432 |
| Identité | Keycloak (26 prod / build custom dev) | `keycloak/` | 8180→8080 |
| Stockage objet | MinIO (S3) | conteneur | 9000 / 9001 |
| Broker messages | RabbitMQ 4 + relais STOMP | conteneur | 5672 / 15672 / 61613 |
| Reverse proxy | Nginx (prod uniquement) | `nginx/` | 80 / 443 |

## 2. Topologie globale

```
                                  ┌──────────────┐
                          OIDC    │   Keycloak   │  (identité, émetteur JWT)
                       ┌─────────▶│   :8180      │
                       │          └──────────────┘
┌──────────┐  HTTPS    │   ┌───────────────────────────┐  JDBC   ┌────────────────────┐
│ Browser  │──────────▶├──▶│  Frontend (Next.js :3000) │         │ PostgreSQL 18      │
│          │           │   │  Axios · Zustand · STOMP   │         │ + pgvector :5432   │
│          │ WS/STOMP  │   └─────────────┬─────────────┘         └─────────▲──────────┘
└──────────┘           │                 │ REST  /api/**                   │
                       │                 ▼                                 │
                       │   ┌───────────────────────────┐  JDBC            │
                       │   │  Backend (Spring Boot)     │──────────────────┘
                       │   │  :8080  /api/**            │
                       │   │  core + modules + shared   │
                       │   └──┬───┬───┬───┬───┬─────────┘
        STOMP 61613 ───┘      │   │   │   │   └──▶ SMTP / Mailtrap (OTP, mails)
        ┌──────────────┐      │   │   │   └──────▶ MinIO :9000 (avatars, pièces jointes)
        │ RabbitMQ     │◀─────┘   │   └──────────▶ Groq API (LLM : smart-assign, assistant, insights)
        │ relais STOMP │          └──────────────▶ Stripe · GitHub/Slack OAuth
        └──────────────┘
```

<blockquote class="important">
<strong>Temps réel :</strong> le backend relaie le protocole STOMP via RabbitMQ (<code>/topic/*</code>,
<code>/queue/*</code>, <code>/user/*</code>), avec repli sur un <code>SimpleBroker</code> en mémoire si
RabbitMQ est indisponible. Le frontend se connecte via <code>@stomp/stompjs</code> (repli SockJS sur
<code>/ws-sockjs</code>).
</blockquote>

## 3. Frontend

Application **Next.js App Router** (`frontend/app/`), organisée en groupes de routes :
le produit authentifié sous `(protected)/[workspace]/…` (scopé par slug de workspace), l'authentification
sous `auth/…` (inscription en 3 étapes : infos → plan → vérification OTP), les retours de paiement Stripe
sous `payment/{success,cancel}`, et un proxy avatar via `app/api/avatar/route.ts`.

Les couches, du haut vers le bas : les **pages** (`app/**/page.tsx`), les **composants**
(`components/`, dont `ui/` pour les primitives shadcn/Radix et des dossiers métier comme `messages/`,
`pricing/`, `smart-assign/`, `inbox/`), l'**état** via des stores **Zustand** (`lib/store/*.ts`, un par
domaine), les **services API** typés (`lib/api/*-service.ts`), le **client HTTP** Axios
(`lib/api/client.ts`) et le **registre de routes** (`lib/config/api-routes.ts`).

Le flux nominal : page → action de store → fonction de service → client Axios → `/api/**` → réponse →
store → re-render. Les mises à jour temps réel arrivent via `lib/hooks/use-stomp.ts` qui mute le store.

<div class="highlight-box">

**Client HTTP (`lib/api/client.ts`)** — base SSR `http://backend:8080`, base CSR `http://localhost:8080`
(variables `NEXT_PUBLIC_API_URL[_SSR]`), injection du bearer JWT, séquence `401 → refresh → retry`, et
mapping des erreurs en toasts. Le registre `api-routes.ts` est **incomplet** : quatre groupes de routes
manquent (cf. [Contrats API](../05-api/API.md)).

</div>

## 4. Backend

Spring Boot en couches, orienté modules. Racine de package `com.taskforce.tf_api`.

```
com.taskforce.tf_api
├── core/          # domaine principal (auth, workspace, project, issue, cycle, team, analytics…)
│   ├── api/         contrôleurs REST (18)
│   ├── service/     logique métier (~25 services)
│   ├── repository/  repositories Spring Data JPA
│   ├── model/       entités JPA (~35)
│   ├── dto/         request/ + response/
│   └── enums/       (19 enums)
├── modules/       # features bornées (api/domain/service/repository/dto propres)
│   ├── chat/        canaux + messages + WebSocket
│   ├── ged/         gestion documentaire (pièces jointes + MinIO + service avatars)
│   └── sales/       capture de leads entreprise
└── shared/        # transverse (AUCUNE logique métier)
    ├── config/      Cors, Jpa, Keycloak, Mail, Minio, OAuth2, OpenApi, Otp, Stripe,
    │                WebSocket, Groq, StompAuthInterceptor
    ├── security/    SecurityConfig, JwtDecoderConfig, JwtIdentityResolver
    ├── audit/       AuditableEntity
    ├── dto/         ApiResponse<T>, ErrorResponse, PageResponse<T>
    └── exception/   GlobalExceptionHandler, BusinessException, ResourceNotFoundException…
```

<blockquote class="important">
<strong>Règle de dépendance</strong> (cf. <code>backend/tf-api/ARCHITECTURE.md</code>) :
<code>shared ← core ← modules</code>. Les modules peuvent dépendre de core/shared ; core dépend de
shared ; <strong>jamais l'inverse</strong>.
</blockquote>

Cycle d'une requête : `SecurityConfig` (deux chaînes : publique + JWT) → contrôleur (`@RequestMapping`)
→ service (autorisation : l'appelant doit être `WorkspaceMember`/`ProjectMember` ; vérifs de rôle via
`WorkspaceRole`/`ProjectRole`) → repository → PostgreSQL. Les erreurs sont normalisées par
`GlobalExceptionHandler`. **Enveloppe de réponse** : `ApiResponse<T>` = `{ success, data, message,
statusCode }` ; le frontend lit systématiquement `response.data.data`.

## 5. Infrastructure & déploiement

Le dépôt fournit plusieurs fichiers Compose à la racine : `docker-compose.dev.yml` (stack dev complète :
postgres pgvector, keycloak custom, backend hot-reload, frontend, ai-service, landing, rabbitmq, minio,
pgadmin), `docker-compose.prod.yml` (postgres 16-alpine, keycloak 23, backend temurin, frontend, nginx),
et `docker-compose.tools.yml` (profils optionnels : observabilité SigNoz et scanners de sécurité
`trivy`/`semgrep`). Le CI/CD repose sur GitHub Actions (`.github/workflows/` : tests par app, release
vers GHCR, gestion sémantique des versions).

<div style="background-color: #f8f9fa; padding: 1rem; border-left: 4px solid #dc3545; margin: 1rem 0;">
<strong>⚠️ Service IA Python vestigial</strong><br>
<code>ai-service/app/main.py</code> est un <em>stub</em> : ses embeddings sont des vecteurs déterministes
de hash SHA256 (16 dimensions, aucun modèle ML) et le scoring smart-assign est une formule pondérée
manuelle. Le <code>TODO.md</code> indique « Remplacé par Groq direct » : en production, l'IA tourne en
Java (<code>core/service/GroqService.java</code>) appelant directement l'API Groq
(<code>llama-3.1-8b-instant</code> pour smart-assign, <code>llama-3.3-70b-versatile</code> pour
l'assistant). Le backend ne dépend pas du service Python en prod. Voir
<a href="../09-audits/Dette_Technique.md">Dette technique (DT-010)</a>.
</div>

Dépendances externes : Keycloak (identité), Stripe (facturation), Groq (LLM), GitHub & Slack (OAuth
intégrations), MinIO (stockage), RabbitMQ (temps réel), SMTP/Mailtrap (email).

## 6. Modèle de données

Persistance gérée par Hibernate en `ddl-auto=validate` + **migrations Flyway** `V1`→`V35`
(`backend/tf-api/src/main/resources/db/migration/`). Le schéma appartient aux migrations ; les entités
doivent rester synchronisées. Scripts d'init : `01-init-keycloak-db.sql`, `02-init-pgvector.sql`.

```
User 1─N Workspace(owner) ;  Workspace 1─N WorkspaceMember ─ User
Workspace 1─N { Project, Team, Cycle, Discussion, Channel }
Project   1─N { ProjectMember, ProjectLabel, Issue, Cycle, Page, Channel }
Issue     1─N { IssueComment, IssueActivity, IssueRelation, IssueGitHubLink, Attachment }
Issue     N─M ProjectLabel ;  Issue N─M Cycle (via CycleIssue)
Team      1─N TeamMember ─ User ;  Channel 1─N ChatMessage ; Channel N─M ChannelMember ─ User
Integration 1─N { IssueGitHubLink | SlackChannel }
User 1─1 OtpVerification ; User 1─N { Subscription, RefreshToken, Notification }
```

Chronologie des migrations détaillée dans [Modules §4](./Modules.md). Les 19 énumérations vivent dans
`core/enums/` (plan/abonnement, OTP, rôles, issue, cycle, discussion, chat, intégrations).

## 7. Sécurité & authentification

Modèle **OAuth2 / OIDC via Keycloak**. Le backend est un **resource server** JWT (RS256, validé contre
le JWKS Keycloak). Le frontend stocke `accessToken`/`refreshToken` et tente un refresh automatique sur
401. En dev, l'auth peut être contournée avec `keycloak.enabled=false`.

`SecurityConfig` définit deux chaînes : **publique** (`/api/auth/**`, `/api/sales/**`, `/api/stripe/**`,
`/api/webhooks/**`, `/api/integrations/*/callback`, `/api/files/**`, `/ws/**`, `/actuator/**`,
`/swagger-ui/**`) et **protégée** (tout le reste → validation JWT). CSRF désactivé, sessions stateless.

<blockquote class="important">
<strong>⚠️ Aucun <code>server.servlet.context-path</code> n'est configuré</strong> (vérifié dans les trois
<code>application*.yml</code>). Un commentaire dans <code>shared/config/CorsConfig.java:65</code> évoque
<code>context-path=/api</code> mais ce n'est <strong>pas</strong> appliqué : chaque contrôleur doit donc
inclure le préfixe <code>/api</code> explicitement — or 5 ne le font pas. Cause racine de
<a href="../09-audits/Problemes_Connus.md">PC-001</a>.
</blockquote>

---

> **Note Brain OS** — Document vérifié dans le code au 08/06/2026 (branche `feat/dashboard`).
> Divergences tracées dans [Dette technique](../09-audits/Dette_Technique.md) et [Problèmes connus](../09-audits/Problemes_Connus.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
