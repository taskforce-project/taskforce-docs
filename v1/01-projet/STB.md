---
id: stb
title: STB — Spécification Technique du Besoin
doc_type: stb
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [stb, specification, technique, besoin, exigences, performance, securite, memoire, rncp]
---

# 📐 STB — Spécification Technique du Besoin

> **But** : traduire les besoins fonctionnels du [[CdCF_v2]] en **exigences techniques mesurables**
> (performances, capacités, contraintes d'intégration, qualité, sécurité). Pont entre le *quoi*
> (CdCF) et le *comment* (CdCT). Sert de critères d'acceptation technique pour la recette.
>
> **Périmètre** : V1 livrée (juillet 2026) — exigences **vérifiées ou vérifiables** à partir du code
> et des configurations. Aucun chiffre inventé ; les valeurs cibles sont issues du code
> (thresholds JaCoCo/Vitest), des règles Prometheus, ou de la documentation existante.

---

## 1. Exigences de performance

| ID | Exigence | Valeur cible | Preuve / mesure |
|---|---|---|---|
| PERF-01 | Temps de réponse API REST (p95, endpoints courants) | < 200 ms | Prometheus `http_server_requests_seconds` histogram |
| PERF-02 | Temps de réponse smart-assign (scoring + Groq) | < 3 s (appel LLM inclus) | Prometheus / SigNoz traces |
| PERF-03 | Débit WebSocket STOMP (messages chat) | Fonctionnel en temps réel | Tests E2E Playwright `chat` |
| PERF-04 | Chargement initial de l'application (LCP) | < 3 s (réseau normal) | Lighthouse / axe-core |
| PERF-05 | Temps de génération export RGPD JSON | < 5 s (données utilisateur standard) | `GdprServiceIntegrationTest` |

---

## 2. Exigences de capacité

| ID | Exigence | Valeur | Justification |
|---|---|---|---|
| CAP-01 | Workspaces simultanés supportés (env dev) | Illimité (PostgreSQL multi-tenant) | `workspace_id` sur toutes les entités |
| CAP-02 | Membres par workspace | Illimité (plan PRO) / limité plan FREE | `PlanFeature` enum + Stripe plans |
| CAP-03 | Fichiers stockés (MinIO) | Limité par espace disque VM (scalable S3) | `docker-compose.prod.yml` volumes |
| CAP-04 | Embeddings pgvector (Brain OS) | `vector(384)` — modèle `all-MiniLM-L6-v2` | Migration V52, `KnowledgeNode.embedding` |
| CAP-05 | Migrations Flyway | V1–V56 (schéma complet) | `db/migration/*.sql` |

---

## 3. Exigences de disponibilité et résilience

| ID | Exigence | Valeur | Implémentation |
|---|---|---|---|
| DISP-01 | Disponibilité cible (prod) | 99 % (hors maintenance) | PCA/PRA documenté — [[PS_PCA_PRA]] |
| DISP-02 | Temps de reprise après incident (RTO) | < 4 h | Procédure `scripts/backup.ps1` + restore |
| DISP-03 | Perte de données maximale acceptable (RPO) | < 24 h | Backup quotidien `pg_dump` |
| DISP-04 | Repli WebSocket si RabbitMQ indisponible | Automatique (`SimpleBroker` in-memory) | `WebSocketConfig` (repli déclaré) |
| DISP-05 | Idempotence webhooks Stripe | Garantie via `stripe_event_id UNIQUE` | Migration V36, `StripeWebhookService` |

---

## 4. Exigences de sécurité

| ID | Exigence | Valeur cible | Preuve |
|---|---|---|---|
| SEC-01 | Vulnérabilités critiques (scan SAST/SCA) | 0 (HIGH/CRITICAL) | Semgrep + Trivy (`scripts/security-scan.ps1`) |
| SEC-02 | Headers de sécurité HTTP (OWASP A05) | CSP, HSTS, X-Frame-Options, X-Content-Type présents | `SecurityHeadersWebMvcTest` |
| SEC-03 | Rate limiting API | Actif (filtre applicatif) | `RateLimitFilter` + `RateLimitFilterTest` |
| SEC-04 | Chiffrement secrets sensibles au repos | `EncryptedStringConverter` sur colonnes critiques | `EncryptedStringConverterTest` |
| SEC-05 | JWT — algorithme de signature | **RS256 (émis par Keycloak)** | `SecurityConfig`, `application-prod.yml` (issuer/jwk) |
| SEC-06 | Durée de vie tokens JWT | Access court (configurable) + refresh DB | `RefreshToken` table + nettoyage planifié |
| SEC-07 | Isolation multi-tenant | `workspace_id` vérifié à chaque requête | `WorkspaceAccessInterceptor` |
| SEC-08 | Protection log-forging (logs client) | Sanitisation `\n`/`\r` dans `ClientLogController` | `ClientLogController.java` |
| SEC-09 | Scan dynamique (DAST) | ZAP baseline (0 alerte HIGH) | `-Dast` dans `security-scan.ps1` |
| SEC-10 | Signature webhooks Stripe | `Webhook.constructEvent` HMAC | `StripeWebhookController` |

---

## 5. Exigences de qualité logicielle

| ID | Exigence | Valeur cible | Outil / preuve |
|---|---|---|---|
| QUAL-01 | Couverture de tests back-end (instructions) | ≥ 60 % (seuil JaCoCo) | `pom.xml` jacoco-maven-plugin |
| QUAL-02 | Couverture de tests front-end (statements) | ≥ 70 % | `vitest.config.ts` thresholds |
| QUAL-03 | Couverture de tests front-end (branches) | ≥ 75 % | `vitest.config.ts` thresholds |
| QUAL-04 | Couverture de tests front-end (fonctions) | ≥ 80 % | `vitest.config.ts` thresholds |
| QUAL-05 | Nombre de fichiers de tests back-end | 72 | `src/test/**/*Test.java` |
| QUAL-06 | Tests E2E automatisés | Auth, redistribution, a11y (3 specs) | `e2e/*.spec.ts` Playwright |
| QUAL-07 | Enveloppe de réponse API normalisée | 100 % des réponses `ApiResponse<T>` | `GlobalExceptionHandler` + convention |

---

## 6. Exigences de conformité

| ID | Exigence | Standard | Preuve |
|---|---|---|---|
| CONF-01 | Export portabilité données | RGPD Art. 20 | `GdprService.exportMyData` + `GdprServiceIntegrationTest` |
| CONF-02 | Droit à l'oubli / anonymisation | RGPD Art. 17 | `GdprService.anonymize` |
| CONF-03 | Accessibilité | WCAG 2.1 niveau AA | `a11y.spec.ts` (axe-core), `Accessibilite.md` |
| CONF-04 | Sécurité authentification | OWASP ASVS L1 | `SecurityConfig`, OTP, rate-limit |
| CONF-05 | Chiffrement communications (prod) | HTTPS/TLS via Nginx | `docker-compose.prod.yml` (Nginx) |

---

## 7. Exigences d'intégration

| ID | Intégration | Protocole / Mécanisme | Preuve |
|---|---|---|---|
| INT-01 | Keycloak (identité) | OIDC / OAuth2, admin API Java | `KeycloakService`, `KeycloakAuthService` |
| INT-02 | Stripe (facturation) | HTTPS REST + webhooks HMAC | `StripeService`, `StripeWebhookController` |
| INT-03 | Groq API (LLM) | HTTPS REST (HTTP client Java) | `GroqService` |
| INT-04 | GitHub (OAuth + liens issues) | OAuth2 + GitHub REST API | `GitHubIntegrationService` |
| INT-05 | Slack (OAuth + channels) | OAuth2 + Slack API | `SlackIntegrationService` |
| INT-06 | MinIO (stockage objets) | S3 SDK Java | `GedService`, `AttachmentService` |
| INT-07 | RabbitMQ (broker STOMP) | STOMP 1.2 + AMQP | `WebSocketConfig`, `RabbitMQ` |
| INT-08 | SMTP / Mailtrap (e-mails) | SMTP TLS | `EmailService` |
| INT-09 | OpenTelemetry → SigNoz | OTLP gRPC | `otel-collector-config.yaml` |

---

## 8. Contraintes techniques

| ID | Contrainte | Valeur | Raison |
|---|---|---|---|
| CT-01 | Version Java | 21 (LTS) | Spring Boot 4 exige Java 21+ |
| CT-02 | Version Node.js | Compatible Next.js 16.1 / React 19 | `package.json` engines |
| CT-03 | Version PostgreSQL | 18 + pgvector | `docker-compose.dev.yml` |
| CT-04 | Clés étrangères DB | 94 (toutes nommées) | Migrations Flyway V1–V56 |
| CT-05 | Secrets | Jamais dans le code source (`.env` non versionné) | Politique secrets — [[CdCT_v2]] §5.2 |
| CT-06 | Multi-tenant | Toute table métier porte `workspace_id` | `WorkspaceAccessInterceptor` |
| CT-07 | Enveloppe API | `ApiResponse<T>` obligatoire sur tous les endpoints | Convention + `GlobalExceptionHandler` |
| CT-08 | Dépendance modules | `shared ← core ← modules` (jamais l'inverse) | `backend/tf-api/ARCHITECTURE.md` |

---

## 9. Traçabilité

| Exigence STB | Preuve code | Livrable associé |
|---|---|---|
| PERF-01 | `prometheus-rules.yml` (latency alert) | [[Architecture_C4]] §8 |
| QUAL-01–06 | JaCoCo `pom.xml`, `vitest.config.ts` | [[Tests]] (`08-operations/Tests.md`) |
| SEC-01–10 | `SecurityHeadersWebMvcTest`, `security-scan.ps1` | [[Sécurité]] |
| CONF-01–02 | `GdprServiceIntegrationTest` | [[CdCF_v2]] §4.8 |
| INT-01–09 | Services `*Integration*`, `*Webhook*` | [[Diagrammes_Sequence_UML]] |

> 🔗 Voir aussi : [[Note_Cadrage]] · [[CdCF_v2]] · [[CdCT_v2]] · [[Sécurité]] · [[Tests]] ·
> [[Roadmap_Documentation|plan de production doc]].
