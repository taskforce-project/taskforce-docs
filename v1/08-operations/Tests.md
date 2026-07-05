---
id: tests
title: Stratégie & couverture de tests
doc_type: reference
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [tests, coverage, qa, jacoco, vitest, playwright]
---

# Tests — Stratégie & couverture

> Chantier **C18 (front) + C25 (back)** de la grille RNCP. Cible réglementaire ≥ 50 % lignes ;
> objectif projet **70 %** avec marge. **Atteint et dépassé** (voir résultats).

## Pyramide de tests

| Niveau | Back (Java) | Front (TS) |
| --- | --- | --- |
| **Unitaire** | JUnit 5 + Mockito + AssertJ (services, sécu, mappers) | Vitest + happy-dom (services API, stores Zustand, utils, hooks) |
| **Composant / slice** | `@WebMvcTest` (controllers : `/api`, `ApiResponse<T>`, `@Valid`→400, 401/403/404) | React Testing Library (formulaires auth, dialogs) |
| **Intégration** | Postgres **réel** (`AbstractIntegrationTest`) + Flyway + `ddl-auto=validate` | — |
| **E2E** | — | **Playwright** (parcours bout-en-bout sur la stack complète) |

## Résultats (05/07/2026)

| Périmètre | Tests | Couverture lignes | Outil |
| --- | --- | --- | --- |
| **Backend** | **670** (0 échec) | **78 %** (≈ 81 % hors Brain OS) | JaCoCo |
| **Frontend** (logique) | **746** (0 échec) | **92 %** | Vitest **v8** |
| **Frontend E2E** | **4/4** | parcours (pas de %) | Playwright |

**Priorisation par criticité** (exigence produit) : sécurité / session / JWT / auth / RGPD / paiement couverts à ~100 %.

### Périmètre coverage
- **Back** : exclut Brain OS (`brain/**`, stand-by) et adaptateurs SDK externes (Stripe/GitHub/Slack/Groq).
- **Front** : périmètre **logique** (`lib/**`, `hooks/**`, `components/auth/**`) ; les **pages `app/`** et l'**UI de présentation** sont couvertes par les **E2E Playwright**, pas par le coverage unitaire. (Le rapport HTML est rendu par `istanbul-reports`, mais la **collecte est V8**.)

### Sécurité (OWASP) testée
A01 IDOR (`AuthorizationService` + `WorkspaceAccessInterceptor`) · A02 chiffrement (`EncryptedStringConverter`) ·
**A05 en-têtes durcis** (`SecurityHeadersWebMvcTest` : CSP/HSTS/X-Frame/nosniff/Referrer/Permissions) ·
A07 (JWT/OTP/`RateLimitFilter`) · A09 (audit).

## Comment lancer

```bash
# Backend — unit + web (sans Docker)
cd backend/tf-api && ./mvnw test

# Backend — suite complète + intégration (Postgres réel) + coverage
.\scripts\it.ps1 -Full            # rapport JaCoCo -> target/site/jacoco-full/index.html

# Frontend — unit + coverage
cd frontend && npm run test:coverage   # rapport -> frontend/coverage/index.html

# Frontend — E2E (app docker-compose déjà up)
cd frontend && npm run e2e
```

## Journaux de suivi (repo `taskforce-fullstack`)
`.ai/tests-backend-journal.md` · `.ai/tests-frontend-journal.md` (parcours, problèmes, coverage).

## CI
Workflows `.github/workflows/{backend,frontend,e2e}-tests.yml`. Prochaine étape : rendre les **gates
JaCoCo/Vitest bloquants** + scan CVE (chantier CI, CERT-C19/C26).
