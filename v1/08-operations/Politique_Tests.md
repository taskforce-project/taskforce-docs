---
id: politique-tests
title: Politique de tests — TaskForce V1
doc_type: qualite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [tests, qualite, politique, jacoco, vitest, playwright, testcontainers, memoire, rncp]
---

# 🧪 Politique de tests — TaskForce V1

> Définition formelle de la stratégie de tests : niveaux, outils, seuils de couverture,
> règles de non-régression et intégration CI. Complémentaire à [[Tests]] (résultats chiffrés).
>
> **Résultats re-mesurés les 21 et 22/07/2026** : backend **786 tests / 73,71 %** · frontend **785 tests / 88,83 %**, les deux suites entièrement vertes. *(Les valeurs du 05/07 — « 670 / 78 % » et « 746 / 92 % » — étaient périmées ; voir [Tests.md](./Tests.md).)*

---

## 1. Principes directeurs

| Principe | Application |
|---|---|
| **No-mock infrastructure** | Testcontainers pour PostgreSQL réel — jamais H2 ni mocks repository (ADR-007) |
| **Sécurité = 100 %** | Auth, JWT, RBAC, headers OWASP couverts en priorité absolue |
| **Code as tests** | Un test qui passe est une preuve documentée — autant que le code |
| **CI bloquante** | Le build fail si la couverture descend sous le seuil configuré |
| **Pas de tests fantômes** | Un test qui teste un mock de mock n'apporte rien — on préfère moins de tests, meilleurs |

---

## 2. Pyramide de tests

```
         /\
        /E2E\          Playwright — 4 parcours complets
       /------\
      / Intégr.\       Testcontainers + Spring Boot — Postgres réel + Flyway
     /----------\
    / Composants \     @WebMvcTest (back) · RTL (front) — API surface + rendu
   /--------------\
  /   Unitaires    \   JUnit 5 + Mockito (back) · Vitest (front) — logique pure
 /------------------\
```

### 2.1 Tests unitaires

**Backend — JUnit 5 + Mockito + AssertJ**

- Cible : services, mappers, utilitaires, sécurité (`JwtIdentityResolver`, `AuthorizationService`,
  `OtpService`, `SmartAssignService`, `RedistributionService`)
- Pattern : `@ExtendWith(MockitoExtension.class)`, dépendances mockées
- Nommage : `<Classe>Test.java` dans le même package que la classe testée

**Frontend — Vitest + happy-dom**

- Cible : services API (`lib/api/`), stores Zustand (`lib/store/`), hooks, utils, contextes auth
- Pattern : `vi.mock()` pour les appels HTTP (MSW non encore utilisé) ; `renderHook` pour les hooks
- Nommage : `<fichier>.test.ts(x)` adjacent au fichier testé

### 2.2 Tests de composants / slice

**Backend — `@WebMvcTest`**

- Cible : contrôleurs REST (surface API, codes HTTP, format `ApiResponse<T>`, `@Valid` → 400, 401/403/404)
- Infrastructure : Spring MVC test slice, principal `Jwt` mocké (`SecurityMockMvcRequestPostProcessors.jwt`) + `AuthorizationService` mocké
- Chaque contrôleur a son propre `*WebMvcTest.java` :

```
AuthControllerWebMvcTest       IssueControllerWebMvcTest
ProjectControllerWebMvcTest    RedistributionControllerWebMvcTest
AssistantControllerWebMvcTest  SecurityHeadersWebMvcTest        ← OWASP headers
ChannelControllerWebMvcTest    AttachmentControllerWebMvcTest
...
```

**Frontend — React Testing Library**

- Cible : formulaires auth (`LoginForm`, `RegisterInfoForm`, `VerificationForm`, `PlanForm`)
- Pattern : `render()` + `userEvent`, assertions sur le DOM

### 2.3 Tests d'intégration

**Backend — Testcontainers + `AbstractIntegrationTest`**

```java
// util/AbstractIntegrationTest.java
@SpringBootTest
@Testcontainers
abstract class AbstractIntegrationTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:18-alpine");
    // Flyway appliqué automatiquement — ddl-auto=validate
}
```

- Postgres **réel** : contraintes FK, types pgvector, migrations Flyway V1–V56 incluses
- Services couverts : `WorkspaceService`, `ProjectService`, `IssueService`, `CycleService`,
  `GdprService`, `AnalyticsService`, `UserService`, `TeamService`, `PageService`,
  `DiscussionService`, `MemberLeaveService`, `MemberSkillProfileService`,
  `WorkspaceInvitationService`, `WebhookService`, `ChatService`, `AttachmentService`,
  `SalesService`, `GitHubIntegrationService`, `SlackIntegrationService`
- Tests de contrat : `GroqServiceContractTest`, `GitHubIntegrationContractTest`,
  `SlackIntegrationContractTest` (requêtes HTTP mockées côté API externe)

### 2.4 Tests E2E — Playwright

```
e2e/auth.spec.ts            — parcours inscription → login → déconnexion
e2e/redistribution.spec.ts  — smart-assign → preview redistribution → apply
e2e/a11y.spec.ts            — audit WCAG 2.1 AA (axe-core)
```

Stack complète requise (`docker-compose up`). Les E2E couvrent les cas que le coverage
unitaire ne peut pas — navigation multi-pages, STOMP temps réel, retours Stripe.

---

## 3. Seuils et gates

| Périmètre | Seuil minimum | Seuil actuel | Outil gate |
|---|:---:|:---:|---|
| Backend — lignes | **70 %** (configuré 22/07) | **73,71 %** | JaCoCo `<limit>` dans `pom.xml` — ⚠️ ne se déclenche que sur `mvn verify` (`PC-028`) |
| Backend — branches | Non configuré | **53,16 %** (mesuré) | — |
| Frontend — logique | Seuils par chemin (`vitest.config.ts`) | **88,83 %** | Vitest v8 |
| Couverture sécurité | **~100 % cible** | ~100 % | Revue manuelle |

**Gate JaCoCo** : configuré dans `pom.xml`. Le build Maven fail si la couverture
passe sous le seuil. Objectif post-V1 : relever le gate à 84 % (atteint ponctuellement).

```xml
<!-- pom.xml — extrait JaCoCo -->
<rule>
    <element>BUNDLE</element>
    <limits>
        <limit>
            <counter>LINE</counter>
            <value>COVEREDRATIO</value>
            <minimum>0.60</minimum>
        </limit>
    </limits>
</rule>
```

---

## 4. Domaines prioritaires

Les tests suivants couvrent les risques les plus élevés et sont maintenus en priorité :

| Domaine | Tests clés | Criticité |
|---|---|:---:|
| **Sécurité auth** | `AuthServiceTest`, `KeycloakAuthServiceTest`, `JwtIdentityResolverTest`, `RateLimitFilterTest` | 🔴 P0 |
| **Autorisation RBAC** | `AuthorizationServiceTest`, `CoreControllersWebMvcTest` (401/403) | 🔴 P0 |
| **Headers OWASP** | `SecurityHeadersWebMvcTest` (CSP, HSTS, X-Frame, nosniff) | 🔴 P0 |
| **JWT** | `JwtServiceTest`, `JwtIdentityResolverTest`, `StompAuthInterceptorTest` | 🔴 P0 |
| **Chiffrement** | `EncryptedStringConverterTest` | 🔴 P0 |
| **RGPD** | `GdprServiceIntegrationTest` | 🟠 P1 |
| **Stripe** | `StripeServiceTest`, `StripeWebhookServiceTest` | 🟠 P1 |
| **OTP** | `OtpServiceTest` | 🟠 P1 |
| **Smart-assign** | `SmartAssignServiceTest` | 🟠 P1 |
| **Redistribution** | `RedistributionServiceTest`, E2E `redistribution.spec.ts` | 🟠 P1 |

---

## 5. Règles de non-régression

1. **Aucun test ne peut être supprimé** sans justification tracée dans un ADR ou une issue.
2. **Un bug fixé = un test ajouté** couvrant le scénario défaillant.
3. **Les tests d'intégration tournent sur Postgres réel** — jamais de remplacement par H2.
4. **CI obligatoire** : toute PR doit avoir les tests verts avant merge (`.github/workflows/backend-tests.yml`, `frontend-tests.yml`).
5. **Les E2E bloquent la release** — les 4 parcours Playwright doivent passer sur la stack complète.

---

## 6. Commandes

```bash
# Backend — unitaires + WebMvc (rapide, sans Docker)
cd backend/tf-api && ./mvnw test

# Backend — suite complète + intégration + coverage JaCoCo
.\scripts\it.ps1 -Full
# rapport → target/site/jacoco-full/index.html

# Frontend — unitaires + coverage
cd frontend && npm run test:coverage
# rapport → frontend/coverage/index.html

# Frontend — E2E (stack Docker up requise)
cd frontend && npm run e2e

# Lancer seulement les tests de sécurité back
cd backend/tf-api && ./mvnw test -Dtest="*SecurityHeadersWebMvcTest,*AuthServiceTest,*AuthorizationServiceTest"
```

---

## 7. CI — GitHub Actions

| Workflow | Déclencheur | Contenu |
|---|---|---|
| `backend-tests.yml` | push + PR sur `main`/`dev` | `./mvnw test` (unitaires + WebMvc) |
| `frontend-tests.yml` | push + PR | `npm run test:coverage` (Vitest) |
| `e2e-tests.yml` | PR vers `main` | `npm run e2e` (Playwright, stack Docker) |

**Prochaine étape** : rendre les gates JaCoCo/Vitest bloquants en CI (TF-TEST-007).

> 🔗 [[Tests]] (résultats chiffrés) — [[Table_Reconciliation]] — [[Cahier_Test_Recettes]] —
> [[Matrice_Tracabilite_Tests]] — ADR-007 (no-mock Testcontainers)
