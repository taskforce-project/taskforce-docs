---
id: cdct-v2
title: CdCT v2 — Cahier des Charges Technique (stack réelle livrée)
doc_type: cdct
statut: valide
version: 2.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [cdct, technique, architecture, stack, securite, performance, infra, memoire, rncp, livrables]
---

# ⚙️ CdCT v2 — Cahier des Charges Technique

> **Version 2.0 — stack et architecture réellement livrées (juillet 2026)**
>
> Ce document **remplace et corrige** le [[02_CdCT|CdCT v1.1 (27/02/2026)]] pour les divergences
> entre la spécification initiale et l'implémentation finale. **Principe** : ne décrire que la
> stack **réellement déployée et démontrée**. Les évolutions envisagées restent en §9 (backlog).
>
> Pour le périmètre fonctionnel → [[CdCF_v2]]. Pour les diagrammes d'architecture → [[Architecture_C4]]
> · [[Diagramme_Classes_UML]] · [[Diagrammes_Sequence_UML]] · [[Modele_Donnees_MCD_MLD]].

---

## Sommaire

1. [Delta v1 → v2 (écarts majeurs)](#1-delta-v1--v2-écarts-majeurs)
2. [Stack technologique réelle](#2-stack-technologique-réelle)
3. [Architecture applicative (réelle)](#3-architecture-applicative-réelle)
4. [Modèle de données (synthèse)](#4-modèle-de-données-synthèse)
5. [Infrastructure & déploiement](#5-infrastructure--déploiement)
6. [Sécurité & conformité](#6-sécurité--conformité)
7. [Tests & qualité](#7-tests--qualité)
8. [Observabilité (réelle)](#8-observabilité-réelle)
9. [Backlog technique](#9-backlog-technique)

---

## 1. Delta v1 → v2 (écarts majeurs)

| Sujet | CdCT v1.1 (02/2026) | CdCT v2 (réel livré) |
|---|---|---|
| **Build back-end** | Gradle DSL Kotlin | **Maven** (`pom.xml`) — migration vers Maven |
| **Observabilité principale** | Grafana + Prometheus + Loki (futur) | **OpenTelemetry → SigNoz** (traces + métriques + logs). Prometheus additionnel pour alerting (9 règles) |
| **Tracing distribué** | « Non implémenté au MVP » | ✅ **OpenTelemetry opérationnel** (`otel-collector-config.yaml`, SigNoz clickhouse) |
| **AI/IA** | Non prévu | ✅ **Groq API** (Java direct, pas de service Python) : `llama-3.1-8b-instant` (smart-assign), `llama-3.3-70b-versatile` (assistant) + pgvector Brain OS |
| **AI service Python** | Prévu comme service IA | ⚠️ **Vestigial** (stub SHA256, non utilisé en prod) — DT-010 |
| **RabbitMQ** | Mentionné comme broker | ✅ **RabbitMQ 4 + relais STOMP** (temps réel chat) avec repli `SimpleBroker` |
| **pgvector** | Non prévu | ✅ PostgreSQL **+ extension pgvector** (`vector(384)` embeddings Brain OS) |
| **Modules optionnels** | Activables via config | ⬜ **Non implémentés** — architecture anticipe mais code absent |
| **Package structure back-end** | `core.auth`, `core.user`, `core.organization`… | **`shared ← core ← modules`** (règle stricte — `ARCHITECTURE.md`) |
| **Logs structurés (backend)** | JSON custom | **Slf4j** (`Logback`), journal audit via `AuditLog` JPA, logs client via `POST /api/logs/client` |

---

## 2. Stack technologique réelle

### 2.1 Back-end

| Composant | Version / détail | Rôle |
|---|---|---|
| **Spring Boot** | 4.0 · Java 21 | Framework API REST |
| **Maven** | 3.x (`pom.xml`) | Build & dépendances (⚠️ CdCT v1 disait Gradle) |
| **Spring Data JPA + Hibernate** | — | ORM, repositories |
| **Spring Security + OAuth2** | — | Chaînes sécurité (publique + JWT bearer) |
| **Flyway** | V1–V56 | Migrations schéma DB |
| **Spring WebSocket + STOMP** | — | WebSocket temps réel (repli SockJS) |
| **Micrometer + Prometheus** | (runtime) | Métriques `/actuator/prometheus` |
| **OpenTelemetry** | `opentelemetry-spring-boot-starter` | Traces + métriques → SigNoz |

### 2.2 Front-end

| Composant | Version | Rôle |
|---|---|---|
| **Next.js App Router** | 16.1 | SSR/SSG, routing file-based |
| **React** | 19.2 | UI |
| **TypeScript** | 5.x strict | Typage |
| **Zustand** | — | State management (stores par domaine) |
| **Axios** | — | Client HTTP (base URL SSR/CSR, refresh JWT, error mapping) |
| **`@stomp/stompjs`** | — | WebSocket STOMP (chat temps réel, repli SockJS) |
| **shadcn-ui + Radix** | — | Design system accessible |
| **Tailwind CSS** | 4 | Utilitaires CSS |
| **Vitest + RTL** | — | Tests unitaires/composants (coverage v8) |
| **Playwright** | — | Tests E2E |
| **axe-core** | — | Tests accessibilité WCAG 2.1 AA |

### 2.3 Landing page

| Composant | Version | Rôle |
|---|---|---|
| **Astro** | 5.x | Landing page statique (islands architecture) |

### 2.4 Infrastructure & tiers

| Composant | Version (dev) | Rôle |
|---|---|---|
| **PostgreSQL** | 18 + pgvector | Base de données (50 tables, 483 colonnes) |
| **Keycloak** | 26 (prod) / build custom (dev) | IdP OIDC, gestion utilisateurs, JWT |
| **RabbitMQ** | 4 + plugin STOMP | Broker messages + relais temps réel |
| **MinIO** | — | Stockage objets S3-compatible (avatars, pièces jointes) |
| **SigNoz** | — | Observabilité (traces + métriques + logs) via OTEL |
| **Groq API** | `llama-3.1-8b-instant` / `llama-3.3-70b-versatile` | LLM smart-assign + assistant IA |
| **Stripe** | — | Facturation SaaS (Checkout, webhooks, portail) |
| **Docker + Compose** | — | Conteneurisation dev (`docker-compose.dev.yml`) et prod (`docker-compose.prod.yml`) |
| **Nginx** | — | Reverse proxy (prod uniquement) |

---

## 3. Architecture applicative (réelle)

> Voir le détail complet → [[Architecture_C4]] (C4 contexte/conteneurs/composants) et [[Architecture]].

### 3.1 Back-end — structure des packages

```
com.taskforce.tf_api
├── shared/       ← transverse (AUCUNE logique métier)
│   ├── config/      Cors, Jpa, Keycloak, Mail, Minio, OAuth2, OpenApi, Otp, Stripe,
│   │                WebSocket, Groq, StompAuthInterceptor
│   ├── security/    SecurityConfig, JwtDecoderConfig, JwtIdentityResolver
│   ├── audit/       AuditableEntity (@MappedSuperclass, 4 entités)
│   ├── dto/         ApiResponse<T>, ErrorResponse, PageResponse<T>
│   └── exception/   GlobalExceptionHandler, BusinessException…
├── core/         ← domaine principal
│   ├── api/         33 contrôleurs REST
│   ├── service/     ~25 services (dont SmartAssignService, RedistributionService, GdprService…)
│   ├── repository/  Spring Data JPA
│   ├── model/       38 entités JPA
│   ├── dto/         request/ + response/
│   └── enums/       19 enums
└── modules/      ← features bornées (dépendent de core + shared)
    ├── chat/        canaux + messages + WebSocket
    ├── ged/         pièces jointes + MinIO + avatars
    └── sales/       leads entreprise
```

**Règle de dépendance stricte** : `shared ← core ← modules`. Jamais l'inverse.

### 3.2 Enveloppe de réponse API

Toutes les réponses API utilisent `ApiResponse<T>` :
```json
{ "success": true, "data": {...}, "message": "...", "statusCode": 200 }
```
Le frontend lit systématiquement `response.data.data`.

### 3.3 Cycle d'une requête

```
SecurityConfig (2 chaînes : publique + JWT bearer)
→ WorkspaceAccessInterceptor (extrait workspace slug)
→ Contrôleur @RequestMapping
→ Service (autorisation : requireMember / requireManager / assertIsOwner)
→ Repository → PostgreSQL
→ GlobalExceptionHandler (normalise toutes les erreurs en ApiResponse)
```

### 3.4 Temps réel

WebSocket Spring + STOMP relayé par **RabbitMQ** (topics `/topic/*`, queues `/queue/*`, `/user/*`).
Repli automatique sur `SimpleBroker` in-memory si RabbitMQ indisponible. Frontend : `@stomp/stompjs`
avec repli SockJS sur `/ws-sockjs`.

---

## 4. Modèle de données (synthèse)

> Voir le détail → [[Modele_Donnees_MCD_MLD]] (7 domaines MERISE, 50 tables) et
> [[Dictionnaire_Donnees]] (483 colonnes, 94 FK, types/contraintes générés d'`information_schema`).

| Statistique | Valeur |
|---|---|
| Tables | 50 (hors `flyway_schema_history`) |
| Colonnes | 483 |
| Clés étrangères | 94 |
| Migrations Flyway | V1–V56 |
| Entités JPA | 38 classes `@Entity` |
| Héritage `AuditableEntity` | 4 entités seulement (⚠️ correction v1) |
| Colonnes pgvector | `knowledge_nodes.embedding vector(384)` |
| Chiffrement au repos | `EncryptedStringConverter` (secrets sensibles) |

**Modèle hybride de références** (détaillé dans [[Diagramme_Classes_UML]]) : associations JPA `@ManyToOne` pour le graphe métier ; références par `Long id` pour les entités de sécurité/audit/facturation (survie à la suppression, découplage cycle de vie).

---

## 5. Infrastructure & déploiement

### 5.1 Environnements

| Env | Fichier Compose | Notes |
|---|---|---|
| **Dev** | `docker-compose.dev.yml` | Stack complète + pgadmin + ai-service stub |
| **Prod** | `docker-compose.prod.yml` | postgres 16-alpine, keycloak 23, temurin backend, nginx |
| **Outils** | `docker-compose.tools.yml` | SigNoz observability + Trivy/Semgrep security scan (profils optionnels) |

### 5.2 Gestion des secrets

Secrets injectés par variables d'environnement (fichiers `.env` non versionnés) :
`JWT_SECRET`, `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `GROQ_API_KEY`, `KEYCLOAK_CLIENT_SECRET`,
`MINIO_ACCESS_KEY`, `MINIO_SECRET_KEY`, `MAILTRAP_*`. Jamais en dur dans le code.

### 5.3 Déploiement cible (VM école)

Hébergement sur l'infrastructure **Guacamole** / VM fournies par Metz Numeric School.
Procédure de déploiement : → [[Roadmap_Documentation]] Phase 7 (en attente disponibilité VM).

### 5.4 PCA / PRA

Plan de Continuité et de Reprise documenté → [[PS_PCA_PRA]] (`11-pca-pra/PS_PCA_PRA.md`).
Script de backup : `scripts/backup.ps1` (PostgreSQL `pg_dump` + volumes MinIO).

---

## 6. Sécurité & conformité

> Détail complet → [[Sécurité]] (`07-securite/Sécurité.md`) et [[PS_PCA_PRA]].

| Aspect | Implémentation réelle |
|---|---|
| **Authentification** | Keycloak OIDC + JWT HS512, refresh tokens en DB, OTP email (inscription / reset pwd) |
| **Autorisation** | RBAC multi-tenant (`WorkspaceRole` OWNER/ADMIN/MEMBER) + `ProjectRole` — vérification à chaque requête |
| **OWASP A01 (broken access control)** | `requireMember`/`requireManager`/`assertIsOwner` + `WorkspaceAccessInterceptor` |
| **OWASP A02 (cryptographic failures)** | HTTPS (prod), `EncryptedStringConverter` secrets sensibles, JWT HS512 |
| **OWASP A03 (injection)** | Spring Data JPA paramétré, aucune concaténation SQL directe |
| **OWASP A05 (security misconfiguration)** | Headers sécurité (CSP, HSTS, X-Frame-Options…) — `SecurityHeadersWebMvcTest` |
| **OWASP A07 (auth failures)** | Rate limiting (`RateLimitFilter`), révocation refresh tokens |
| **SAST** | Semgrep (`scripts/security-scan.ps1`) |
| **SCA** | Trivy (dépendances + images Docker) |
| **DAST** | OWASP ZAP baseline (script `-Dast`) |
| **RGPD** | Export portabilité (Art. 20) + anonymisation (Art. 17) — `GdprService` |
| **Accessibilité** | axe-core Playwright `a11y.spec.ts`, `14-design/Accessibilite.md` |

---

## 7. Tests & qualité

> Détail → [[Tests]] (`08-operations/Tests.md`).

| Catégorie | Outil | Cible | État |
|---|---|---|---|
| **Tests unitaires back-end** | JUnit 5 + Mockito + AssertJ | — | ✅ |
| **Tests d'intégration back-end** | Testcontainers (`it.ps1`) | — | ✅ |
| **Slices contrôleurs** | `@WebMvcTest` | — | ✅ |
| **Couverture back-end** | JaCoCo | ≥ 60 % (seuil) | ✅ |
| **Tests unitaires front-end** | Vitest + RTL | ≥ 70 % (statements) | ✅ |
| **Tests E2E** | Playwright | Auth, redistribution, a11y | ✅ |
| **Tests accessibilité** | axe-core (Playwright) | WCAG 2.1 AA | ✅ |
| **Total fichiers de tests** | — | 72 (back) + e2e | ✅ |

**Politique de tests** : pas de mock frontend pour les données (seed DB via `dev_seed.sql`) ; tests
d'intégration sur vraie base Testcontainers (`AbstractIntegrationTest`).

---

## 8. Observabilité (réelle)

> ⚠️ **Correction CdCT v1** : la stack décrite (Grafana/Prometheus/Loki/Tempo) ne reflète **pas** la
> réalité livrée. La stack réelle est OpenTelemetry → **SigNoz** (traces + métriques + logs intégrés).

| Composant | Rôle | Config |
|---|---|---|
| **OpenTelemetry** | Instrumentation Spring Boot automatique | `opentelemetry-spring-boot-starter` |
| **SigNoz** | Backend OTEL tout-en-un (ClickHouse) | `observability/signoz/` + `otel-collector-config.yaml` |
| **Prometheus** | Métriques additionnelles + alerting | `/actuator/prometheus`, `micrometer-registry-prometheus` |
| **Règles d'alerte** | 9 règles Prometheus | `observability/alerts/prometheus-rules.yml` |
| **Logs client front-end** | `POST /api/logs/client` → Slf4j | `ClientLogController` (protection log-forging) |
| **Audit applicatif** | `AuditLog` JPA | Actions sensibles (login, redistribution, exports RGPD…) |

---

## 9. Backlog technique

Fonctionnalités techniques envisagées dans le CdCT v1 ou identifiées en cours de projet, **non livrées
en V1**. Tracées dans [[Roadmap_Backlog]] / [[Problemes_Connus]].

| Item | Contexte |
|---|---|
| CI/CD pipeline complet (GitHub Actions) | Workflows présents, déploiement prod non finalisé (VM école) |
| Migration service IA Python (DT-010) | `ai-service` vestigial — remplacé par Groq Java direct |
| CSP nonce dynamique (hardening) | Headers statiques actuels, nonce dynamique Next.js = complexité |
| Scalabilité horizontale (Kubernetes) | Anticipé, hors MVP |
| Loki (logs centralisés) | Remplacé par SigNoz en prod |
| Modules LIMS / Qualité / GED | Architecture anticipe, code absent |
| Rôle Invité | Non implémenté (3 rôles suffisants pour V1) |

> 🔗 Voir aussi : [[CdCF_v2]] · [[Architecture_C4]] · [[Sécurité]] · [[Tests]] ·
> [[Catalogue_Documentation]] · [[Roadmap_Documentation]].
