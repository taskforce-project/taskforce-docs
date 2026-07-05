---
id: release-notes
title: Release Notes / CHANGELOG — TaskForce
doc_type: utilisateur
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [utilisateur, release-notes, changelog, versions, e29, rncp, soutenance]
---

# 📦 Release Notes / CHANGELOG — TaskForce

> Journal des livraisons de TaskForce, conformément au critère **E29** du référentiel RNCP DFS.
>
> **Convention** : versions `MAJOR.MINOR.PATCH` (SemVer). Versioning indépendant par service
> (`backend-vX.Y.Z`, `frontend-vX.Y.Z`, `landing-vX.Y.Z`) géré automatiquement par le
> workflow `version-management.yml` via labels de PR.
>
> **Note landing page** : la page `/changelog` de la landing présente des versions
> "v2.0.0–v2.4.0" à titre de **projection produit** (roadmap marketing). Ce document
> couvre la **livraison réelle V1.0** pour la soutenance RNCP (Metz Numeric School 2025-2026).

---

## v1.0.0 — 05/07/2026 — Livraison soutenance RNCP

> Version complète livrée pour la soutenance **Développeur Full Stack RNCP niveau 6**.
> Développée d'octobre 2025 à juillet 2026 (9 mois, ~1 développeur ETP).

---

### ✨ Authentification & sécurité

- **Inscription en 3 étapes** avec vérification OTP email (TTL 15 min, 3 essais) — UC-01
- **Connexion sécurisée** via Keycloak (référentiel identité) + JWT HS512 custom (`JwtService`) — UC-02
- Refresh tokens HttpOnly Secure SameSite=Strict avec rotation
- **Rate limiting Bucket4j** : 10 req/min (auth), 200 req/min (default), 20 req/min (IA)
- 6 **headers de sécurité OWASP** : CSP `default-src 'none'`, HSTS 31536000s, X-Frame DENY, nosniff, Referrer-Policy, Permissions-Policy
- Protection **log-forging** (`ClientLogController.sanitize`)
- Chiffrement **AES-256-GCM** sur PII sensibles (messages Enterprise, notes)

---

### 🏢 Workspaces & membres

- Création de workspace avec slug unique — UC-03
- RBAC 3 niveaux : **OWNER / ADMIN / MEMBER** avec `AuthorizationService` + `WorkspaceAccessInterceptor`
- Système d'**invitations par email** avec lien de 72h — UC-04
- Gestion des rôles inline (ADMIN → MEMBER, MEMBER → ADMIN)
- **Profils de compétences** membres : skills JSON, séniorité, capacité h/sem., objectifs de croissance

---

### 📋 Projets, issues & kanban

- Gestion de **projets** avec membres, identifiant, description — UC-05
- **Issues** : titre, description, type (7), priorité (5), statut, assigné, labels, cycle, module, dates — UC-06
- Statuts d'issue **personnalisables** par projet (catégories BACKLOG/UNSTARTED/STARTED/COMPLETED/CANCELLED)
- Vue **Kanban** drag-and-drop, vue **Liste** avec filtres multi-critères, vue **Backlog**
- Commentaires, activité, sous-issues, relations (`blocks`/`blocked-by`/`duplicate-of`)
- **Pièces jointes** (upload MinIO avec contrôle de scope workspace/project/issue)
- **Worklogs** (temps passé par issue) — alimentent les analytiques Smart Assign

---

### 🤖 Smart Assign — Assignation intelligente par IA

- **Moteur d'assignation** basé sur 3 axes : compétences × charge × disponibilité — UC-07
- Inférence LLM via **Groq API** (Java natif `GroqService`, pas de microservice Python)
- Stockage vectoriel **pgvector** (PostgreSQL 18) : embeddings profils membres (vector 384d) + documents RAG
- Explication en langage naturel pour chaque suggestion
- **Feedback** utilisateur (acceptation/rejet) → amélioration continue (`assignment_events`)
- Analytiques IA : `ai_runs`, `ai_insight_snapshots` (coût, latence, source décision)

---

### 🔄 Cycles (sprints)

- Création de **cycles** avec dates début/fin — UC-08
- Ajout/retrait d'issues dans un cycle
- Vue de progression : issues planifiées vs. terminées, barre de complétion, jours restants

---

### 📄 Pages wiki

- Création et organisation de **pages** hiérarchiques (parent/enfant) — UC-10
- Éditeur riche (ProseMirror) avec formatage Markdown, blocs de code, tableaux
- Navigation arborescente dans la sidebar

---

### 💬 Chat & discussions

- **Chat temps réel** par canaux liés aux projets (STOMP/SockJS + RabbitMQ 4) — UC-09
- Messages persistés avec historique complet
- Mentions `@utilisateur` avec notification inbox
- Authentification STOMP (`StompAuthInterceptor`) + vérification appartenance au canal
- Fallback SockJS automatique si WebSocket bloqué
- **Discussions** asynchrones (forum) avec sous-catégories

---

### 💳 Plans & facturation Stripe

- 3 plans : **FREE / PRO / ENTERPRISE** — UC-11
- Flux **Stripe Checkout** (création session, redirection, confirmation)
- 5 webhooks Stripe traités : `checkout.session.completed`, `invoice.*`, `customer.subscription.*`
- Machine à états `PlanStatus` : `ACTIVE → PAST_DUE → CANCELED`
- Idempotence des webhooks (`stripe_event_id UNIQUE`)
- Portail de facturation Stripe (modification paiement, annulation, téléchargement factures)
- Formulaire de contact **Enterprise** (leads sales) avec chiffrement AES-256-GCM

---

### ⚖️ RGPD & droits des personnes

- Export de données JSON (Art. 20 RGPD) : `GET /api/gdpr/export` — UC-12
- Suppression et anonymisation de compte (Art. 17) : `DELETE /api/gdpr/delete-account`
- Journalisation audit RGPD (`GDPR_EXPORT`, `GDPR_DELETE`)
- Politique de confidentialité + CGU dédiées sur la landing page

---

### 🔌 Intégrations

- **GitHub** : OAuth2, liens issues ↔ PR/commits
- **Slack** : OAuth2, notifications de canal
- **Webhooks** : configurable par workspace avec signature HMAC
- Configuration DNS pour les callbacks OAuth

---

### 🚀 CI/CD & infrastructure

- **7 workflows GitHub Actions** : `backend-tests.yml`, `frontend-tests.yml`, `e2e-tests.yml`, `release.yml`, `landing-tests.yml`, `sync-badges.yml`, `version-management.yml`
- Versioning SemVer **indépendant** par service (`backend-v*`, `frontend-v*`, `landing-v*`)
- Images Docker publiées sur **GHCR** à chaque release
- Stack **Docker Compose** complète : postgres, backend, frontend, keycloak, minio, rabbitmq, otel-collector, signoz
- **Option A** (VM école) : `docker-compose.prod.yml` + nginx TLS
- **Option B** (Render.com Frankfurt) : `render.yaml` — ~46 $/mois

---

### 📊 Observabilité

- **OTel → SigNoz → ClickHouse** : 5 pipelines (traces, métriques, métriques/prometheus, logs, meter)
- 9 règles d'alerte Prometheus : disponibilité, erreurs/latence p95, saturation JVM/pool DB/CPU, sécurité (rate-limit spike, auth failure spike)
- Logs conteneurs via `filelog` receiver (Docker JSON)
- Métriques Micrometer exposées sur `/actuator/prometheus`

---

### 🧪 Tests

- **Backend** : 72 fichiers de test / 670 tests / **78 % couverture JaCoCo** (gate 60 %)
  - Testcontainers (PostgreSQL + Keycloak) — pas de mocks
  - Tests paramétrés `@ParameterizedTest`
- **Frontend** : 55 fichiers / 746 tests / **92 % couverture Vitest** (gate 70 % lines)
- **E2E** : 3 specs Playwright (auth, routes, accessibilité WCAG 2.1 AA via axe-core)

---

### ♿ Accessibilité

- Audit **axe-core** en CI (spec Playwright `a11y.spec.ts`) — WCAG 2.1 AA
- `aria-label` sur tous les boutons iconiques
- Gestion du focus visible, navigation clavier

---

### 🌐 Landing page (Astro)

- Pages marketing complètes : accueil, pricing, enterprise, security, accessibility, about, blog (placeholder), changelog, contact
- Pages légales : Politique de confidentialité (`/privacy-policy`), CGU (`/terms`)
- i18n EN/FR (`LanguageContext`, `constants_en.ts`, `constants_fr.ts`)
- Formulaire de contact Enterprise (`POST /api/sales/inquiry`)

---

## Roadmap V1.x — Items en backlog prioritaire

> Pour le détail complet : [[Roadmap_Backlog]]

| ID | Description | Priorité |
|---|---|---|
| TF-SEC-009 | Migration JWT HS512 → Keycloak OIDC natif | P2 |
| TF-RGPD-001 | Bannière de consentement cookies (CNIL) | P2 |
| TF-SEC-010 | DAST ZAP en CI (bloquant sur HIGH) | P2 |
| TF-SEC-011 | Rate limiting distribué (Redis) pour multi-instances | P2 |
| TF-TEST-009 | Tests de charge k6/Gatling (validation seuils STB) | P2 |
| TF-INFRA-009 | Runbooks / Dossier d'exploitation | P2 |

---

> 🔗 [[Manuel_Utilisateur]] — [[Pipeline_CICD]] — [[Roadmap_Backlog]] — [[STB]] (exigences)
