---
id: matrice-tracabilite-tests
title: Matrice de traçabilité exigences ↔ tests — TaskForce V1
doc_type: tracabilite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [tracabilite, exigences, tests, stb, qualite, couverture, memoire, rncp, soutenance]
---

# 🔗 Matrice de traçabilité exigences ↔ tests — TaskForce V1

> Traçabilité complète entre les exigences du [[STB]] et les tests automatiques.
> Chaque ligne répond à la question : **"comment sait-on que cette exigence est satisfaite ?"**
>
> **Familles** : PERF (performance) · CAP (capacité) · DISP (disponibilité) · SEC (sécurité) ·
> QUAL (qualité) · CONF (conformité) · INT (intégration) · CT (contraintes techniques).
>
> **Légende** :
> - ✅ Couvert — test automatique couvre l'exigence
> - 🟡 Partiel — test existe mais couverture incomplète
> - ⬜ Manuel — vérifié par inspection/procédure, pas de test automatique
> - ❌ Gap — aucune couverture détectée (à noter dans la roadmap)

---

## PERF — Performance

| ID | Exigence | Valeur cible | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| PERF-01 | Temps de réponse API REST (p95) | < 200 ms | Prometheus `http_server_requests_seconds` (monitoring prod) | ⬜ |
| PERF-02 | Temps de réponse smart-assign (Groq) | < 3 s | `SmartAssignServiceTest` (vérifie le résultat, pas la latence) · SigNoz traces | 🟡 |
| PERF-03 | Débit WebSocket STOMP | Fonctionnel temps réel | `StompAuthInterceptorTest` · E2E `redistribution.spec.ts` (STOMP connect) | 🟡 |
| PERF-04 | Chargement initial LCP | < 3 s | E2E `a11y.spec.ts` (Lighthouse integration) | 🟡 |
| PERF-05 | Export RGPD JSON | < 5 s | `GdprServiceIntegrationTest` (assertion résultat, timer absent) | 🟡 |

**Bilan PERF** : aucune exigence de performance n'est vérifiée par test de charge dédié (k6/Gatling non configurés — TF-PERF-001). Les tests existants valident le *comportement* mais pas les *seuils latence*.

---

## CAP — Capacité

| ID | Exigence | Valeur | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| CAP-01 | Workspaces simultanés | Illimité (multi-tenant) | `WorkspaceServiceIntegrationTest` (création multiple) | ✅ |
| CAP-02 | Membres par workspace (FREE vs PRO) | Limité par `PlanFeature` | `WorkspaceServiceIntegrationTest` · `WorkspaceInvitationServiceIntegrationTest` | 🟡 |
| CAP-03 | Fichiers stockés MinIO | Limité disque VM | `AttachmentServiceTest` (upload/download) | 🟡 |
| CAP-04 | Embeddings pgvector `vector(384)` | Migration V52 | `AbstractIntegrationTest` — Flyway V52 appliqué sur Postgres réel | ✅ |
| CAP-05 | Migrations Flyway V1–V56 | Toutes appliquées | `AbstractIntegrationTest` — Testcontainers + Flyway (chaque test d'intégration valide les 56 migrations) | ✅ |

---

## DISP — Disponibilité & résilience

| ID | Exigence | Valeur | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| DISP-01 | Disponibilité cible 99 % | Procédure PCA/PRA | `scripts/backup.ps1` — aucun test auto | ⬜ |
| DISP-02 | RTO < 4 h | Procédure restore | Runbook `scripts/restore.ps1` — vérification manuelle | ⬜ |
| DISP-03 | RPO < 24 h | Backup quotidien pg_dump | Cron + vérification manuelle | ⬜ |
| DISP-04 | Repli WebSocket in-memory | Automatique SimpleBroker | `WebSocketConfig` — couverture par inspection | ⬜ |
| DISP-05 | Idempotence webhooks Stripe | `stripe_event_id UNIQUE` | `StripeWebhookServiceTest` (cas doublon testé) | ✅ |

**Bilan DISP** : seule DISP-05 a un test automatique. DISP-01 à DISP-04 relèvent de procédures opérationnelles documentées dans [[PS_PCA_PRA]] (à créer — Phase 7).

---

## SEC — Sécurité

| ID | Exigence | Valeur cible | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| SEC-01 | 0 vulnérabilité HIGH/CRITICAL (SAST/SCA) | 0 | `scripts/security-scan.ps1` (Semgrep + Trivy) — lancé manuellement | ⬜ |
| SEC-02 | Headers HTTP OWASP (CSP, HSTS, X-Frame, nosniff…) | Présents sur toutes routes | `SecurityHeadersWebMvcTest` | ✅ |
| SEC-03 | Rate limiting API | Actif | `RateLimitFilterTest` | ✅ |
| SEC-04 | Chiffrement données sensibles au repos | `EncryptedStringConverter` | `EncryptedStringConverterTest` | ✅ |
| SEC-05 | JWT HS512 | Signé HS512 | `JwtServiceTest` | ✅ |
| SEC-06 | Durée de vie tokens | Access court + refresh DB | `JwtServiceTest` · `AuthServiceTest` (logout révoque refresh) | ✅ |
| SEC-07 | Isolation multi-tenant | `workspace_id` vérifié | `AuthorizationServiceTest` · `CoreControllersWebMvcTest` (IDOR 403) | ✅ |
| SEC-08 | Protection log-forging | Sanitisation `\n`/`\r` | `ClientLogControllerWebMvcTest` | ✅ |
| SEC-09 | DAST ZAP baseline (0 alert HIGH) | 0 | `scripts/security-scan.ps1` (`-Dast`) — lancé manuellement | ⬜ |
| SEC-10 | Signature webhooks Stripe HMAC | `Webhook.constructEvent` | `PaymentAndDataControllersWebMvcTest` (signature invalide → 400) | ✅ |

**Bilan SEC** : 7/10 couvertes par tests automatiques. SEC-01 et SEC-09 dépendent du script Semgrep/Trivy/ZAP (lancé manuellement, à intégrer en CI — TF-SEC-012). SEC-08 supposé couvert — à confirmer si `ClientLogControllerWebMvcTest` teste bien la sanitisation.

---

## QUAL — Qualité logicielle

| ID | Exigence | Valeur cible | Fichier(s) de test / outil | Couverture |
|---|---|---|---|:---:|
| QUAL-01 | Couverture back-end (instructions) ≥ 60 % | 78 % actuel | JaCoCo `pom.xml` gate + rapport `jacoco-full/index.html` | ✅ |
| QUAL-02 | Couverture front-end statements ≥ 70 % | 92 % actuel | `vitest.config.ts` thresholds + `coverage/index.html` | ✅ |
| QUAL-03 | Couverture front-end branches ≥ 75 % | ~85 % (estimé) | `vitest.config.ts` | ✅ |
| QUAL-04 | Couverture front-end fonctions ≥ 80 % | ~88 % (estimé) | `vitest.config.ts` | ✅ |
| QUAL-05 | 72 fichiers de tests back | 72 confirmés | `src/test/**/*Test.java` + `find` CI | ✅ |
| QUAL-06 | Tests E2E automatisés (3 specs) | 3 specs Playwright | `e2e/auth.spec.ts` · `e2e/redistribution.spec.ts` · `e2e/a11y.spec.ts` | ✅ |
| QUAL-07 | Enveloppe `ApiResponse<T>` 100 % | Convention + gate | `CoreControllersWebMvcTest` (assertion format envelope) · `GlobalExceptionHandler` | ✅ |

---

## CONF — Conformité

| ID | Exigence | Standard | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| CONF-01 | Export portabilité données | RGPD Art. 20 | `GdprServiceIntegrationTest` (export JSON, readOnly) | ✅ |
| CONF-02 | Droit à l'oubli / anonymisation | RGPD Art. 17 | `GdprServiceIntegrationTest` (anonymize) | ✅ |
| CONF-03 | Accessibilité WCAG 2.1 AA | WCAG 2.1 | `e2e/a11y.spec.ts` (axe-core, 0 violation critique) | ✅ |
| CONF-04 | Sécurité authentification | OWASP ASVS L1 | `AuthControllerWebMvcTest` · `JwtServiceTest` · `RateLimitFilterTest` · `OtpServiceTest` | ✅ |
| CONF-05 | HTTPS/TLS en production | TLS via Nginx | `docker-compose.prod.yml` (vérification manuelle) | ⬜ |

---

## INT — Intégrations

| ID | Intégration | Mécanisme | Fichier(s) de test | Couverture |
|---|---|---|---|:---:|
| INT-01 | Keycloak (identité) | Admin REST API | `KeycloakAuthServiceTest` · `AuthServiceTest` | ✅ |
| INT-02 | Stripe (facturation) | REST + webhooks HMAC | `StripeServiceTest` · `StripeWebhookServiceTest` | ✅ |
| INT-03 | Groq API (LLM) | HTTP Java client | `GroqServiceContractTest` (mocked) · `SmartAssignServiceTest` | ✅ |
| INT-04 | GitHub (OAuth + issues) | OAuth2 + REST API | `GitHubIntegrationContractTest` (HTTP mocked) | ✅ |
| INT-05 | Slack (OAuth + channels) | OAuth2 + Slack API | `SlackIntegrationContractTest` (HTTP mocked) | ✅ |
| INT-06 | MinIO (stockage objets) | S3 SDK Java | `AttachmentServiceTest` | ✅ |
| INT-07 | RabbitMQ (STOMP) | STOMP 1.2 + AMQP | `StompAuthInterceptorTest` · `ChatServiceIntegrationTest` | ✅ |
| INT-08 | SMTP / Mailtrap | SMTP TLS | `EmailService` — utilisé dans `AuthServiceTest` (invite mock) | 🟡 |
| INT-09 | OpenTelemetry → SigNoz | OTLP gRPC | `otel-collector-config.yaml` — aucun test auto (infra) | ⬜ |

---

## CT — Contraintes techniques

| ID | Contrainte | Valeur | Vérification | Couverture |
|---|---|---|---|:---:|
| CT-01 | Java 21 | LTS | `pom.xml` `<java.version>21</java.version>` · CI compilé avec JDK 21 | ✅ |
| CT-02 | Node.js compatible Next.js 16.1 | `package.json` engines | `frontend-tests.yml` CI | ✅ |
| CT-03 | PostgreSQL 18 + pgvector | Testcontainers + Flyway | `AbstractIntegrationTest` (image `postgres:18-alpine`) | ✅ |
| CT-04 | 94 FK nommées | Migrations V1–V56 | `AbstractIntegrationTest` — Flyway validate + `ddl-auto=validate` | ✅ |
| CT-05 | Secrets hors code source | `.env` non versionné | `.gitignore` · CI secrets repository — vérification par inspection | ⬜ |
| CT-06 | Multi-tenant (`workspace_id` partout) | Toute table métier | `AuthorizationServiceTest` · `WorkspaceAccessInterceptorTest` | ✅ |
| CT-07 | Enveloppe `ApiResponse<T>` | 100 % endpoints | `CoreControllersWebMvcTest` | ✅ |
| CT-08 | Dépendance modules `shared←core←modules` | Règle architecture | `backend/tf-api/ARCHITECTURE.md` · Inspectable via `mvn dependency:analyze` | ⬜ |

---

## Synthèse de couverture

### Par famille

| Famille | Total | ✅ Couvert | 🟡 Partiel | ⬜ Manuel | ❌ Gap | Taux auto |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| PERF | 5 | 0 | 4 | 1 | 0 | **0 %** |
| CAP | 5 | 3 | 2 | 0 | 0 | **60 %** |
| DISP | 5 | 1 | 0 | 4 | 0 | **20 %** |
| SEC | 10 | 7 | 0 | 3 | 0 | **70 %** |
| QUAL | 7 | 7 | 0 | 0 | 0 | **100 %** |
| CONF | 5 | 4 | 0 | 1 | 0 | **80 %** |
| INT | 9 | 7 | 1 | 1 | 0 | **78 %** |
| CT | 8 | 5 | 0 | 3 | 0 | **63 %** |
| **TOTAL** | **54** | **34** | **7** | **13** | **0** | **76 %** |

### Gaps et actions recommandées

| Priorité | ID | Libellé | Action |
|:---:|---|---|---|
| 🟠 P1 | TF-PERF-001 | Aucun test de charge (k6/Gatling) — PERF-01..05 non vérifiées par test | Créer suite k6 pour endpoints critiques |
| 🟠 P1 | TF-SEC-012 | Semgrep/Trivy/ZAP non intégrés en CI — SEC-01/SEC-09 manuels | Ajouter job `security-scan` dans `backend-tests.yml` |
| 🟡 P2 | TF-INT-008 | Test SMTP limité — intégration email non testée bout-en-bout | Ajouter test d'intégration Mailtrap/SMTP avec Testcontainers `mailhog` |
| 🟡 P2 | TF-OPS-003 | DISP-01..04 sans test auto — PCA/PRA procédure uniquement | Créer runbook de restore testé + monitoring probe |
| 🟢 P3 | TF-CT-008 | Règle `shared←core←modules` non vérifiée en CI | Ajouter `mvn dependency:analyze` ou ArchUnit dans CI |

> ⚠️ **PC-019 / TF-SEC-009** : JWT émis par le backend (HS512) — une fois migré vers Keycloak
> (RS256 OIDC), SEC-05 et SEC-06 devront être remappés vers les tests de validation JWK endpoint.
> Voir [[Roadmap_Backlog]] TF-SEC-009.

---

> 🔗 [[STB]] (exigences source) — [[Cahier_Test_Recettes]] (scénarios UC) — [[Politique_Tests]] (stratégie) —
> [[Table_Reconciliation]] (UC ↔ entités ↔ migrations ↔ tests) — [[Roadmap_Backlog]] (gaps → backlog)
