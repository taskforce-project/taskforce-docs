---
id: rapport-tests
title: Rapport de tests & couverture — TaskForce V1
doc_type: operations
statut: valide
version: 1.0
date: "16/08/2026"
auteur: Pierre MICHEL
tags: [tests, couverture, coverage, jacoco, vitest, playwright, rncp, c18, c25, memoire]
---

# 🧪 Rapport de tests & couverture — TaskForce V1

> Rapport d'exécution **daté** de la campagne de tests TaskForce (back + front), avec **chiffres réels
> mesurés le 16/08/2026** et pointeurs vers les **artefacts** (rapports JaCoCo / Vitest). Complète la
> [[Politique_Tests]] (stratégie) et le [[Cahier_Test_Recettes]] (scénarios). Répond aux exigences de
> couverture **≥ 50 %** (C18 front, C25 back) du référentiel RNCP.

---

## 1. Synthèse (run du 16/08/2026)

| Périmètre | Tests | Échecs | Couverture lignes | Seuil | Verdict |
|---|---|---|---|---|---|
| **Backend** (Java / Spring Boot) | **874** | **0** (1 skip = contexte) | **74,11 %** (périmètre gate) · ~68 % sans exclusions | ≥ 50 % (RNCP) · gate 70 % | ✅ **> seuil** |
| **Frontend** (TypeScript / React) | **821** | **0** | **90,03 %** (87,3 % branches, 87,6 % fonctions) | ≥ 50 % (RNCP) · gate par chemin | ✅ **> seuil, gate VERT** |

**Total : 1 695 tests automatisés, 0 échec.** Branches back (périmètre gate) 52,96 %.

> **Note de périmètre back** : le chiffre « sans exclusions » (68,24 %) inclut le package `core.service.brain`
> (knowledge-graph, volumineux et volontairement peu couvert en unitaire) ; le **périmètre du gate JaCoCo**
> (brain exclu, = ce que le référentiel évalue) est à **74,11 %** (run `mvn verify` du 17/08). Les deux sont > 50 %.

---

## 2. Backend — détail

### 2.1 Exécution
- **Commande** : `.\scripts\it.ps1 -Full` (suite complète + rapport sans exclusions). Faute de JDK local,
  les tests tournent dans un conteneur Maven contre un **Postgres pgvector réel** (sibling Docker) +
  **Flyway** + `ddl-auto=validate` (équivalent fonctionnel prod). En CI : service `pgvector/pgvector:pg16`
  (ajouté le 16/08 — cf. [[Problemes_Connus]] PC-028).
- **Résultat** : `Tests run: 874, Failures: 0, Errors: 0, Skipped: 1` — dont **+22 slices `@WebMvcTest`**
  (2 lots, 15 contrôleurs qui étaient à ~0 % : Analytics/Knowledge/Analysis/Cortex/User/OAuth/webhook Stripe,
  puis Cycle/Page/DashboardCard/MemberLeave/MemberSkill/AiUsage/SkillSuggestion/Webhook) ajoutées le 17/08.
  Le gate s'exécute via `mvn verify` (`it.ps1 -Verify`) → « **All coverage checks have been met** » (74,11 %).

### 2.2 Types de tests
- **Unitaires** (Mockito) : `*ServiceTest` (Auth, Otp, Stripe, SmartAssign, Redistribution, agents…),
  sécurité (`RateLimitFilterTest`, `JwtIdentityResolverTest`, `AuthorizationServiceTest`,
  `EncryptedStringConverterTest`, `TurnstileServiceTest`, `HumanChallengeServiceTest`).
- **Slices contrôleurs** (`@WebMvcTest`) : `*WebMvcTest` (Auth, Issue, Project, Payment, SecurityHeaders…).
- **Intégration** (`@SpringBootTest` + vrai Postgres) : `*IntegrationTest`, `IntegrationSocleTest`,
  `GdprServiceIntegrationTest`.

### 2.3 Couverture (JaCoCo, rapport `target/site/jacoco-full/index.html`)
| Métrique | Périmètre gate (brain exclu) | Sans exclusions |
|---|---|---|
| **Lignes** | **74,11 %** (6413/8653) | 68,24 % (6494/9516) |
| **Branches** | 52,96 % | 49,38 % |

---

## 3. Frontend — détail

### 3.1 Exécution
- **Commande** : `npx vitest run --coverage` (⚠️ `npm run test:coverage` = `vitest --coverage` reste en
  **mode watch** — utiliser `vitest run` pour un one-shot CI/rapport). Env : Vitest + React Testing Library,
  `happy-dom`.
- **Résultat** : `Test Files 66 passed (66) · Tests 821 passed (821)`, durée ~80 s.

### 3.2 Couverture (rapport `frontend/coverage/`)
- **All files : 90,03 % lignes · 87,26 % branches · 87,56 % fonctions.** (85,19 → 90,03 le 17/08 :
  exclusion du généré/déco/barrels — `*.generated.ts`, `floating-paths.tsx`, `index.ts` — plutôt que
  de les compter à 0 %, **+ tests** `client-logger.ts` **0 → 100 %** et `turnstile-widget.tsx`.)
- **Périmètre** : la couverture unitaire cible la **logique** (`lib/**`, `hooks/**`, `components/auth/**`) ;
  les **pages/UI** (`app/**`, `components/ui`) sont couvertes par les **E2E Playwright** (hors coverage unitaire).
- **Gate par chemin — VERT (exit 0).** Deux chemins étaient sous leur seuil (préexistants) puis **re-couverts
  le 16/08** : **`lib/api/auth-service.ts`** 81,69 % → **98,69 %** (100 % fonctions ; +12 tests : OAuth
  authorize/callback, challenge, fallbacks forgot/reset, logout best-effort, JSON corrompu) ;
  **`lib/contexts/auth-context.tsx`** 89,32 % → **95,14 %** lignes, branches 71,87 % → **85,29 %** (+3 tests :
  init sans token, garde d'onboarding, sortie de `/auth/login`).
- **Validation Zod** : `lib/validation/auth-schemas.ts` **couvert** — `auth-schemas.test.ts` (12 tests :
  login + register, cas valides et d'échec email/nom/jetable/robustesse/concordance, `firstZodError`).

### 3.3 E2E
- **Playwright** : `e2e/{a11y,auth,redistribution}.spec.ts` (accessibilité, parcours d'auth, redistribution).
  Gatés en CI via `E2E_ENABLED`.

---

## 4. Couverture des cas RGPD / sécurité (succès **et** échec)

Le référentiel demande des cas nominaux ET d'erreur. Extraits réellement présents :
- **RGPD** : `GdprServiceIntegrationTest` (export OK ; export utilisateur inconnu → 404 ; effacement/anonymisation).
- **Sécurité** : `SecurityHeadersWebMvcTest` (5), `EncryptedStringConverterTest` (11), `RateLimitFilterTest` (8),
  `TurnstileServiceTest` (9), `HumanChallengeServiceTest` (10), `StripeWebhookServiceTest` (signature invalide → 400),
  contrôle d'accès (IDOR inter-tenant → 403).
- **Paiement** : `StripeServiceTest` (10) — dont le cas **price-id ambigu → pas de rétrogradation** (16/08).
- Détail exigence↔test → [[Matrice_Tracabilite_Tests]] ; scénarios succès/échec → [[Cahier_Test_Recettes]].

---

## 5. Artefacts (preuves horodatées)
- **Back** : `backend/tf-api/target/site/jacoco-full/index.html` (+ `jacoco.csv`).
- **Front** : `frontend/coverage/` (rapport HTML v8).
- **Sécurité** (scans du 16/08) : `security-reports/2026-08-16_18-54-07/` (Trivy JSON/HTML/SARIF, Semgrep) +
  `…_18-49-21/` (ZAP HTML/JSON). Synthèse → [[Rapport_Securite]] §5.
- **CI (portes bloquantes)** : `.github/workflows/backend-tests.yml` (`mvn verify` → JaCoCo ≥ 70 %),
  `frontend-tests.yml` (Vitest, gate par chemin), `security-scan.yml` (Trivy + Semgrep, gate CRITICAL/ERROR).

## 6. Gaps connus (traités / à traiter)
- **Gate JaCoCo EN CI (fait 17/08)** : `backend-tests.yml` appelle désormais **`mvn verify`** → l'exécution
  `jacoco-check` (BUNDLE LINE ≥ 70 %) **bloque** la CI (PC-028 résolu — jusqu'ici inerte car la CI ne faisait
  que `test jacoco:report`). Service Postgres CI en place depuis le 16/08.
- **Scans sécurité EN CI (fait 17/08)** : nouveau `security-scan.yml` (Trivy deps/secrets/misconfig + Semgrep
  SAST), rapport complet en artefact + gate sur le plus haut niveau (CRITICAL / ERROR) + run hebdo. ZAP DAST manuel.
- **Front** : gate par chemin **au vert (16/08)** — `auth-service.ts` et `auth-context.tsx` re-couverts ;
  Zod couvert. Reliquat sans impact seuil : quelques branches SSR/`fetchMe`-truthy (`auth-context` 64,114-116,153).
- **Manques ciblés** : `DueDateAlertScheduler` sans test dédié ; `GdprServiceIntegrationTest` ne vérifie pas
  l'appel `KeycloakService.deleteUser` (`afterCommit`) ; pas de **test de charge** (TF-TEST-009).

---
**Références** : [[Politique_Tests]] · [[Cahier_Test_Recettes]] · [[Matrice_Tracabilite_Tests]] ·
[[Rapport_Securite]] · [[Problemes_Connus]] · seuils RNCP C18/C25 (≥ 50 %).
