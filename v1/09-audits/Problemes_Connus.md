---
type: documentation-technique
statut: draft
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [technique, problèmes-connus, triage, priorités, roadmap]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Problèmes Connus — Triage

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Priorité: Critique](https://img.shields.io/badge/Priorité-Critique-red?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Dette technique (inventaire)](./Dette_Technique.md)
- [Contrats API](../05-api/API.md)
- [Architecture globale](../03-architecture/Architecture.md)

**Tags :** `#technique` `#problèmes-connus` `#triage` `#priorités`

## Table des matières

1. [File de priorités](#1-file-de-priorités)
2. [Détails par problème](#2-détails-par-problème)
3. [Notes pour les agents IA](#3-notes-pour-les-agents-ia)

---

<p class="lead">
Vue priorisée et scorée des problèmes catalogués dans <a href="./Dette_Technique.md">Dette technique</a>.
Chaque entrée : <strong>Priorité · Impact · Effort · Confiance</strong>, avec le lieu du correctif (non
appliqué). Échelle d'effort : S ≤2h · M ½–1j · L 1–3j · XL &gt;3j.
</p>

## 1. File de priorités

> **▶ MAJ 05/07/2026 (branche `test/v1-hardening`).** Le triage ci-dessous datait du snapshot `feat/dashboard` (08/06).
> Vérifié sur le code actuel : **PC-001, PC-002, PC-003, PC-005 sont ✅ résolus** (préfixes `/api`, groupes de routes front,
> import `profile-service`, webhooks Stripe câblés). **PC-004 & PC-019 ✅ résolus** par la migration auth **Keycloak OIDC**
> (refresh/logout natifs IdP, décodeur RS256, `JwtService` custom supprimé — 658 tests backend verts). Restent surtout
> les P2/P3 (PC-006/007/009/011/014).

> **▶ MAJ 20/07/2026 (branche `chore/v1-closure`).** Trois problèmes remontés par l'usage, **tous résolus et
> vérifiés en live** : **PC-031** (aperçu des pièces jointes cassé — cause **CSP**, pas MinIO), **PC-032**
> (lignes mortes du Signal Center — liens de notification `NULL` en base), **PC-033** (blocages de rate
> limiting — les préflights CORS consommaient le quota). Point commun des trois : **l'hypothèse de départ
> était fausse** et seule la mesure a désigné la vraie cause.

> **▶ MAJ 20/07/2026 (suite).** **PC-034** — **contrôle d'accès manquant sur les pièces jointes d'issue**,
> résolu et vérifié de bout en bout. Le service ne vérifiait que le **scope** de la ressource (« l'issue
> est-elle bien dans ce projet et ce workspace ? »), ce qui ne dit **rien de qui demande**. Portée réelle
> **plus étroite** que soupçonné au départ — `WorkspaceAccessInterceptor` arrêtait déjà les comptes
> étrangers au workspace — mais bien réelle : un **membre du workspace** pouvait lire et téléverser les
> pièces jointes d'un **projet privé dont il n'est pas membre**. Suite backend : **759 tests, 0 échec**.

> **▶ MAJ 17/08/2026 — durcissement prod P0 (config + déploiement).** Vérifié par
> `it.ps1 -Verify` = **874 tests, 0 échec, gate vert** ; la chaîne de migration a tourné **sans les seeds**
> (= chemin prod), plus haute version appliquée `V73`, aucun `V17/18/31/40` migré, aucune erreur Flyway.
> - **PC-024 — profil prod ✅** : `docker-compose.prod.yml` posait déjà le bon `SPRING_PROFILES_ACTIVE: prod`
>   (la faute `SPRING_PROFILE` de l'audit a été corrigée depuis). Restait le **défaut de l'image** :
>   `Dockerfile` gravait `ENV SPRING_PROFILES_ACTIVE=dev` → un `docker run` nu tournait en dev. Basculé en
>   **`prod` (fail-safe)** : sans les secrets prod, le conteneur échoue au démarrage au lieu de tourner
>   permissif ; le dev surcharge explicitement (`docker-compose.dev.yml`).
> - **PC-026 — seeds hors prod ✅** : les 4 migrations de seed (`V17`/`V18`/`V31`/`V40`, mots de passe en
>   clair) déplacées de `db/migration` vers **`db/seed`** (contenu inchangé → checksum inchangé). La base
>   `application.yml` ne liste que `classpath:db/migration` → **prod ET profil `it` ne voient plus les
>   seeds** ; `application-dev.yml` ajoute `classpath:db/seed` → le dev/démo les garde. Flyway ignore sans
>   erreur les versions absentes sur base neuve (prouvé par le run ci-dessus).
> - **PC-027 — CORS ✅** : `CorsConfig` lit désormais **`cors.allowed-origins`** (`@Value`, CSV) au lieu de
>   la liste codée en dur → `CORS_ALLOWED_ORIGINS` (application-prod.yml / compose / render) n'est plus de la
>   **config morte** ; un front déployé hors `*.taskforce.com` n'est plus bloqué par le navigateur.
> - **PC-025 — pgvector partout ✅** : la prod (`docker-compose.prod.yml`) et le dev utilisaient **déjà**
>   `pgvector/pgvector:pg18` (+ `db/init-prod/02-init-pgvector.sql`) — le vrai chemin prod était donc sain.
>   Restait le compose « par défaut » (`docker-compose.yml`) sur `postgres:16-alpine` → un `docker compose up`
>   nu plantait sur `CREATE EXTENSION vector` (V32). Aligné sur **`pgvector/pgvector:pg18`** + profil `dev`
>   explicite (companion PC-024, sinon défaut `prod` sans secrets). `docker compose config` OK.

> **▶ MAJ 16/08/2026 (session paiement + CI + IA, WIP).** Trois changements factuels, vérifiés dans le code.
>
> **PC-028 — partiellement adressé.** `backend-tests.yml` reçoit désormais un **service Postgres
> `pgvector/pgvector:pg16`** + les variables `SPRING_DATASOURCE_URL`/`USERNAME`/`PASSWORD`
> (`jdbc:postgresql://localhost:5432/tf`, `tf`/`tf`) — réplique de `scripts/it.ps1`. Avant : la CI lançait
> `mvn test` **sans** Postgres → les tests d'intégration (`@SpringBootTest` + pgvector + Flyway) tombaient en
> erreur, JaCoCo sur disque ~4 %, job « Backend Tests » rouge. Désormais les tests d'intégration **tournent
> en CI**. **RÉSOLU (17/08).** `backend-tests.yml` passe de `mvn test jacoco:report` à **`mvn verify`** → le
> **gate JaCoCo (0,70) de la phase `verify` bloque** enfin la CI (jusqu'ici inerte). Vérifié en local :
> `it.ps1 -Verify` = `mvn clean verify` → **865 tests, 0 échec, « All coverage checks have been met »**
> (périmètre gate 73,64 %). Les scans **SAST/SCA sont intégrés** au nouveau workflow **`security-scan.yml`**
> (Trivy deps/secrets/misconfig + Semgrep SAST, rapport en artefact + gate CRITICAL/ERROR + run hebdo).
> **Restent hors périmètre** : ZAP DAST (manuel, exige la stack levée), et les points (c) E2E éteint et
> (d) lint `continue-on-error` de la description d'origine.
>
> **PC-035 (nouveau) — rétrogradation d'abonnement corrigée.** Bug :
> `STRIPE_PRICE_ID_BASIC == STRIPE_PRICE_ID_BUSINESS` (**même price-id** dans `.env.dev`, vérifié) → sur
> `customer.subscription.updated`, le reverse-mapping price-id→plan renvoyait Basic pour un abonné Business
> → **rétrogradation Business→Basic**. **Corrigé (16/08)** : `StripeService.getPlanForPriceId` compte les
> correspondances et renvoie **`null` si un price-id matche plusieurs forfaits** (ambigu) → le webhook ne
> resynchronise pas depuis un signal non fiable ; le plan reste celui posé par
> `checkout.session.completed` (metadata `planType`). Test `StripeServiceTest`
> (cas ambigu `getPlanForPriceId_ambiguous_returnsNull`) au vert, suite Stripe **10/10**. **RESTE action
> config** : créer un **price Business distinct** côté Stripe + `stripe listen` pour rejouer de vrais
> événements en démo.
>
> **Note secrets.** `.env.dev` (racine, **non suivi par git** — sorti du suivi au commit `63cb1d2b`,
> aujourd'hui dans `.gitignore`) porte de **vraies credentials** : 2 secrets OAuth GitHub
> (`GITHUB_LOGIN_CLIENT_SECRET`, `GITHUB_CLIENT_SECRET`) et des clés Stripe **test** (`sk_test…`,
> `whsec_…`) ; la clé Groq y est **vidée** (l'ancienne `gsk_…` renvoyait 403 au test du 16/08 → morte).
> **Absents de l'historique git — vérifié** (`git log -S` sur chaque valeur courante = 0 occurrence). À
> **roter** malgré tout avant remise du dossier.

À traiter dans cet ordre.

| ID | Prio | Titre | Impact | Effort | Conf. |
| -- | :--: | ----- | ------ | :----: | :---: |
| PC-001 | 🔴 P0 | 5 contrôleurs sans `/api` → Cycles/Teams/Pages/Discussions/Chat en 404 | Pans entiers HS | M | Haute |
| PC-002 | 🟠 P1 | Constantes de routes front absentes → Messages/Intégrations/PJ/Roadmap crash | 4 features plantent | S | Haute |
| PC-003 | 🟠 P1 | Import cassé `profile-service.ts` | Page profil en erreur | S | Haute |
| PC-004 | 🟠 P1 | Refresh auth désaligné + non implémenté | Sessions non renouvelables → reconnexion forcée | M | Haute |
| PC-005 | 🟠 P1 | Webhooks Stripe abonnement/facture stubés | État facturation désynchronisé de Stripe | L | Haute |
| PC-006 | 🟡 P2 | `team-store` incomplet | UI Teams HS même après PC-001 | M | Moy. |
| PC-007 | 🟡 P2 | AI Insights sans cache + pas de garde quota/timeout Groq | Latence + épuisement quota | M | Haute |
| PC-008 | 🟡 P2 | Inquiry Sales sans email/notification | Leads captés en silence | S | Haute |
| PC-009 | 🟡 P2 | Streaming assistant simulé | Latence perçue ; pas de vrai token-stream | M | Haute |
| PC-010 | 🟡 P2 | QA manuelle (QA.1–6) & tests auto (T.1–6) en attente | Risque release, régressions | XL | Haute |
| PC-011 | 🟢 P3 | Mock chat résiduel (`messages/data.ts`) | Faux contenu affiché | S | Moy. |
| PC-012 | 🟢 P3 | Service IA Python vestigial | Service mort, confusion ops | M | Haute |
| PC-013 | 🟢 P3 | Command-palette « Create new issue » placeholder | Petit manque UX | S | Haute |
| PC-014 | 🟢 P3 | Pas de feature flags IA | Ops ne peut pas toggler l'IA | M | Haute |
| PC-015 | 🟢 P3 | Commentaire `context-path` périmé + chemin healthcheck | Induit en erreur ; bruit healthcheck | S | Moy. |
| PC-019 | ✅ Résolu (05/07) | **JWT émis par le backend** → **migré vers Keycloak OIDC (RS256)** : `JwtService`/HS512 supprimés, décodeur JWK + validation issuer, refresh/logout natifs IdP. Cf. TF-SEC-009. | Sécurité auth alignée OIDC | L | Haute |
| PC-016 | ✅ Résolu (04/07) | **`canManage` toujours faux** page Membres (`/users/me` renvoie `id` en number, comparé en string → `"1"===1` faux) → gestion rôles/invitation/**redistribution** masquées **pour le OWNER** | Feature manager invisible | S | Haute |
| PC-017 | ✅ Résolu (04/07) | **Export RGPD 500** : `GdprService.exportMyData` en `@Transactional(readOnly)` + INSERT audit → SQLSTATE 25006 (même pattern que FIX-006). Droit de portabilité **cassé** | Droit RGPD HS | S | Haute |
| PC-018 | ✅ Résolu (30/06) | **Module test ne compilait plus** : `JwtServiceTest` appelait `JwtService.refreshAccessToken` (méthode supprimée, refresh migré dans `AuthService`) → toute la suite bloquée en silence | CI aveugle | S | Haute |
| PC-024 | ✅ **Résolu (17/08)** | **La prod démarre en profil `dev`** (audit 16/07, vérifié) : `backend/tf-api/Dockerfile:60` grave `ENV SPRING_PROFILES_ACTIVE=dev` dans l'image ; `docker-compose.prod.yml:86` passe `SPRING_PROFILE: prod` — **mauvais nom de variable**. La variable d'env de l'image l'emporte dans la précédence Spring → `application-prod.yml` **jamais chargé**. Conséquences (toutes tirées d'`application-dev.yml`) : **`clean-disabled: false` → `flyway clean` ARMÉ contre la base de prod** (`:34`, alors que prod a `true`) ; **pas de `resourceserver.jwt` → validation des tokens en HS512 maison au lieu de RS256/JWKS Keycloak** (`:42-43`) ; `validate-on-migrate: false` (`:35`) ; realm `taskforce-dev` (`:57`) ; `show-sql: true` (`:24`) ; mot de passe DB par défaut (`:15`). ⚠️ `render.yaml:28` utilise le **bon** nom → si Render est la vraie cible, le fusil est chargé mais pas tiré. | Destruction possible de la base + auth dégradée | S | Haute |
| PC-025 | ✅ **Résolu (17/08)** | **La prod ne peut pas migrer** (audit 16/07, vérifié) : `docker-compose.prod.yml:13` et `docker-compose.yml:9` utilisent `postgres:16-alpine`, **sans pgvector**. Or `V32__ai_documents.sql`, `V33__member_skill_profiles.sql` et `V52__brain_embeddings.sql` font `CREATE EXTENSION vector` — `IF NOT EXISTS` ne sauve rien, l'extension doit être **présente sur l'image**. Seul le dev a `pgvector/pgvector:pg18` (`docker-compose.dev.yml:19`). Déploiement neuf → Flyway plante sur **V32** → le backend ne démarre jamais. Bonus : dev en **pg18**, prod en **pg16**. | Déploiement impossible | S | Haute |
| PC-026 | ✅ **Résolu (17/08)** | **Les seeds de dev s'exécutent en production** (audit 16/07, vérifié) : `application.yml:27` déclare `locations: classpath:db/migration` — **une seule location, jamais surchargée** par dev ni prod. La prod exécute donc `V17__seed_dev_users.sql` (**mots de passe en clair dans le fichier, `:9-10` : `Admin@2024` / `Test@2024`**), `V31__seed_extended_dev_qa_users.sql` (`:9` : `Taskforce@2024`) et `V40__dev_admin_pro.sql` (passe `admin@taskforce.dev` en **plan PRO**). Le garde-fou de V40 (« no-op si le compte n'existe pas ») est **neutralisé par V17 qui vient de le créer**. Aggravant : `docker-compose.prod.yml:66` monte `./keycloak/realms` (parent de `dev/` **et** `prod/`) avec `--import-realm` → soit le realm dev est importé en prod avec ses credentials, soit aucun realm ne l'est (les JSON sont en sous-dossiers) → auth morte. Les deux issues sont mauvaises. | Comptes admin à credentials publiés en prod | M | Haute |
| PC-027 | ✅ **Résolu (17/08)** | **CORS en dur : le navigateur bloquera tous les appels API en prod** (audit 16/07, vérifié) : `shared/config/CorsConfig.java:27-31` fait `setAllowedOriginPatterns(List.of("http://localhost:3000", "http://localhost:5173", "http://localhost:4200", "https://*.taskforce.com"))`. **Aucune ligne de code Java ne lit `cors.allowed-origins`** (grep `@Value`/`@ConfigurationProperties` : zéro consommateur) → `application-prod.yml:69`, `docker-compose.prod.yml:102` et `render.yaml:64` sont de la **config morte**. Déploiement sur `taskforce.onrender.com` ou tout domaine de VPS → aucune origine ne matche → **tous les appels API bloqués par le navigateur**, et on perd des heures à corriger une variable inopérante. Accessoirement les `localhost` restent autorisés en prod, avec `setAllowCredentials(true)`. | Front déployé totalement inopérant | S | Haute |
| PC-028 | 🟠 **Partiel (16/08)** | **▶ Partiellement adressé (16/08)** — CI backend réparée (service Postgres `pgvector`), tests d'intégration en CI ; **reste** le gate JaCoCo (`verify`, 0,70) + scans hors CI (voir bloc daté du 16/08 en tête de §1). Description d'origine conservée : **4 portes CI sur 6 ne mordent pas** (audit 16/07, vérifié) : **(a)** le gate JaCoCo 84 % **ne s'exécute jamais** — `pom.xml:342` déclare `jacoco-check` **sans `<phase>`**, la phase par défaut du goal `check` est `verify`, or la CI lance `./mvnw clean test jacoco:report` (`backend-tests.yml:56`) qui s'arrête à `test` ; **(b)** le seuil global Vitest est de la **config morte** — `vitest.config.ts:49` utilise la syntaxe **Jest** `thresholds: { global: {...} }`, que Vitest interprète comme un **glob** ne matchant aucun fichier ; **(c)** l'**E2E est éteint par défaut** (`e2e-tests.yml:30` `if: vars.E2E_ENABLED == 'true'`) et un job skippé remonte **« success »** à la branch protection ; **(d)** lint front en `continue-on-error: true`. **Et la release ne dépend d'aucun test** : les jobs de build n'ont que `needs: detect-and-version`, et `Dockerfile:23` `ARG SKIP_TESTS=true` sans `build-args` passé → **l'image de prod est buildée tests désactivés**. Le job Lighthouse ne teste rien non plus (pointe `localhost:4321` **sans démarrer de serveur**, échec avalé). | Les preuves de qualité (C19/C26) sont fictives | M | Haute |
| PC-029 | 🟠 P1 | **Un faux assistant IA est servi aux utilisateurs** (audit 16/07, vérifié) : `components/command-palette.tsx:43-74` — `useAIStream` est **entièrement mocké** (réponse figée « Cette réponse sera bientôt connectée à l'API Taskforce. » + faux streaming `setInterval` 40 ms/mot). Le fichier est **vivant** : importé par `components/layout/topbar/app-topbar.tsx:22` et monté. Cmd+K → question → réponse inventée présentée comme de l'IA. **Viole la règle d'or n°7 (« pas de données mock »)**, en production, sur le différenciateur du produit. | Mock livré aux utilisateurs | S | Haute |
| PC-030 | 🟠 P1 | **La page `/agents` sert des chiffres financiers inventés** (audit 16/07) : la roadmap la dit « supprimée » ; le fichier `app/(protected)/[workspace]/agents/page.tsx` (31 Ko) **existe toujours** et Next sert la route par URL directe (le fil d'Ariane lui donne même un titre : `app-topbar.tsx:46`). Contenu : 6 faux agents C-level avec burn « $42k », runway « 14 months », « 3 high-severity CVEs », « Team health 7.4/10 » — **rendus à l'écran**. Son chat est de toute façon cassé : `:175` lit `localStorage.getItem("access_token")` alors que toute l'app utilise `accessToken` (17 sites) → toujours `null` → 401 → throw sans UI d'erreur. **Risque de soutenance** : un juré ouvre l'URL et tombe sur des métriques fabriquées. Trancher : supprimer (~56 Ko + 5 deps) ou brancher sur `lib/api/assistant-service.ts` qui fait déjà le travail. | Contenu fabriqué atteignable en démo | S | Haute |
| PC-021 | ✅ **Résolu (16/07)** | **IDOR inter-tenant sur les Pages** — **correctif** : `PageService` résout désormais le projet **via le slug** (`workspaceRepository.findBySlug(slug).flatMap(ws -> projectRepository.findByIdAndWorkspaceId(projectId, ws.getId()))`) puis délègue à `ProjectVisibilityGuard` (`assertCanView` en lecture, `assertCanWrite` en écriture) — le patron d'`IssueService`. Les 5 méthodes prennent `slug` + `userId` ; `PageController` les passe (il recevait déjà le `slug` **sans jamais l'utiliser**) et passe par `JwtIdentityResolver` (corrige au passage `TF-JWT-IDENTITY` sur les pages). **Non-régression ajoutée** : `PageServiceIntegrationTest.CrossWorkspaceIdor` — 4 tests rejouant l'exploit exact (slug de Mallory + `projectId` d'autrui → 404, en lecture / suppression / listing) + défense en profondeur (bon slug mais projet privé → 404). ⚠️ **L'ancien test « IDOR » était trompeur** : il ne testait qu'un autre projet **du même workspace** (déjà couvert par `findByIdAndProjectId`) — il donnait une fausse confiance sur exactement ce qui était troué. ⚠️ **Piège de seed corrigé** : les projets sont **privés par défaut** (`Project.isPublic = false`) → le test devait créer la ligne `WorkspaceMember` de l'owner, comme le fait `WorkspaceService` en prod. `test-compile` **BUILD SUCCESS**. **Reste : lancer `it.ps1 -Test ALL`.** | Fuite + destruction de données inter-tenant | S | Haute |
| PC-021bis | 🔴 **P0** | **~~IDOR inter-tenant sur les Pages~~ — description d'origine (conservée pour trace)** (audit 16/07, vérifié) : `PageService` ne fait **aucune** vérification — 0 occurrence de `resolveProject`/`assertWorkspaceMember`/`visibilityGuard`. `PageController` reçoit `@PathVariable String slug` et **ne s'en sert jamais** : il passe le seul `projectId` au service. `WorkspaceAccessInterceptor:75` ne valide que `existsByWorkspaceIdAndUserId(workspaceId du slug, userId)` — il **ne vérifie jamais que `projectId` appartient à ce workspace** (son javadoc `:24` prétend pourtant couvrir « Pages »). **Exploit** : Mallory crée son workspace `mallory-ws` (membre légitime) → `DELETE /api/workspaces/mallory-ws/projects/42/pages/7` où 42 est un projet **privé d'autrui** → l'intercepteur passe → `findByIdAndProjectId(7,42)` → **page supprimée**. Lecture/création/modification/suppression de n'importe quelle page. `PageService` est le **seul** outlier : `CycleService:56-57`, `ProjectService:222-224`, `IssueService:228` font tous `resolveProject(slug, projectId)`. Patron à copier : `AttachmentService.findScopedIssue:100-114`. | **Fuite + destruction de données inter-tenant** | S | Haute |
| PC-022 | 🔴 **P0** | **`AgentService.run` tient une connexion DB pendant tout le LLM** (audit 16/07, vérifié) : `@Transactional` en `AgentService:78` englobe `runToolLoop:253-254`, soit jusqu'à `MAX_TOOL_ITERS=5` appels `llm.rawChat` **séquentiels**. Read-timeout du gateway = **300 000 ms** (`AiGatewayClient:40`) → **jusqu'à 25 min de connexion retenue**. Pool Hikari = **20** en prod (`application-prod.yml:12`), 10 en dev, `connection-timeout: 30000`. **20 chats Cortex simultanés = pool épuisé = toute l'API tombe** (chaque requête attend 30 s puis échoue). Même famille : `PlaneIntegrationService:103` (`sync` = N appels HTTP d'embedding non bornés dans 1 tx), `SmartAssignService:128` (`bulkRecommend` = N LLM dans 1 tx). **Le patron correct existe déjà dans le repo** : `BrainIngestionListener:43-57` (tx courte → LLM hors tx → tx courte) et `AnalysisJobRunner:44`. | API entière indisponible sous charge modérée | M | Haute |
| PC-023 | 🟠 P1 | **Récidive n°5 de l'écriture en tx `readOnly`, en embuscade** : `SmartAssignService.logAiRun:645-664` et `logAssignmentEvent:677-693` font un `jdbcTemplate.update` (INSERT) sous `try/catch(Exception)` **sans `REQUIRES_NEW`** — la forme exacte de PC-020/FIX-006. Sains **uniquement** parce que `recommend:64`/`preview:99`/`bulkRecommend:128` sont read-write. **Le piège est amorcé** : le javadoc de `preview:166` affirme « Ne persiste aucun `assignment_events` » — c'est **faux** (`computeRecommendation` écrit `ai_runs`), ce qui invite le prochain dev à la passer en `readOnly`. Correctif préventif : router ces 2 INSERT via un bean `REQUIRES_NEW` (cf. `BrainEmbeddingWriter`, `AuditService`). | Bombe à retardement : 25006 silencieux puis 25P02 | S | Haute |
| PC-020 | ✅ Résolu (16/07) | **Le RAG du Brain OS n'avait jamais fonctionné** : `DecisionService.retrieveContext` en `@Transactional(readOnly)` → `BrainSearchService.retrieveRelevant` → `backfillMissingEmbeddings` → **`UPDATE`** dans la tx en lecture seule → Postgres avorte la tx → le `SELECT … <=> …` suivant meurt en **25P02**. Le `try/catch` masquait la cause. **19 nodes du seed n'ont jamais pu s'indexer** ; l'analyse tombait en repli **sans le dire**. Correctif : `BrainEmbeddingWriter` (bean séparé, `REQUIRES_NEW` → 1 tx par vecteur). Vérifié : 78/78 indexés, job 10 `DONE` vs jobs 8/9 `FAILED`. **4ᵉ occurrence du motif** (FIX-006 a+b, PC-017, celle-ci). | RAG décoratif : l'IA répondait sans le contexte | S | Haute |
| PC-031 | ✅ **Résolu (20/07)** | **L'aperçu des pièces jointes était bloqué par notre propre CSP** (vérifié en live) : vignette cassée dans le sheet d'issue, `fetch` de l'URL présignée en `TypeError: Failed to fetch`. **Tout ce qu'on soupçonnait était sain** : `/attachments` → 200, MinIO joignable, signature présignée **valide** (URL générée avec `mc` → HTTP 200, 1449 octets), CORS MinIO renvoyant `Access-Control-Allow-Origin: http://localhost:3000`. **Vraie cause** : `frontend/next.config.ts` construisait la CSP **sans l'origine du stockage objet** — `img-src 'self' data: blob: https: ${API_ORIGIN}`, or le mot-clé `https:` **ne couvre pas** un MinIO local en `http://localhost:9000`, et `connect-src` ne le listait pas non plus → le navigateur bloquait **avant** tout échange réseau. **Correctif** : constante `STORAGE_ORIGIN` (`NEXT_PUBLIC_STORAGE_URL`, défaut `http://localhost:9000`) ajoutée à **`img-src` ET `connect-src`**, variable passée au service `frontend` dans `docker-compose.dev.yml`. ⚠️ **Invariant** : doit rester **aligné sur `MINIO_PUBLIC_ENDPOINT`** côté backend (c'est l'hôte signé). **Preuve** : vignette du logo affichée sur l'issue 4826. | Pièces jointes illisibles à l'écran | S | Haute |
| PC-032 | ✅ **Résolu (20/07)** | **Lignes mortes dans le Signal Center — liens de notification `NULL`** : la table `notifications` ne porte **aucune clé étrangère** vers `issues`/`projects` ; `issue_url`/`project_url` sont **dénormalisées à l'écriture** par `NotificationService.buildNotification`. Toute ligne insérée **hors du code Java** (en pratique le seed) arrive donc avec des liens `NULL` — **impossible à reconstruire à la lecture**. **Mesure** : **35 lignes sur 266** sans lien, exactement celles du seed ; elles affichaient un identifiant (« WEB-3 ») mais le clic ne faisait rien. **Correctifs** : (a) migration Flyway **`V71__backfill_notification_urls.sql`** — reconstruit les liens en décomposant `issue_identifier` (« WEB-3 » → identifiant projet + n° de séquence) puis en rejoignant `projects`/`issues`, avec un filet ramenant **au moins au projet** (idempotente, ne touche que les `NULL`) ; (b) `seed/dev_seed.sql` — bloc de résolution des liens en fin de seed (même règle), identifiants du bloc de volume tirés d'issues **réelles** au lieu d'être fabriqués par concaténation (`'WEB-'` + numéro de boucle), signal de surcharge aligné sur la convention Java `overload-<userId>` ; (c) garde front — `DataTable` accepte `isRowClickable`, une ligne **sans destination** n'est ni cliquable ni pourvue du bouton « ouvrir ». **Résultat mesuré** : **265/266** résolues ; reste **1 ligne** (`overload` du seed historique, `issue_identifier` `NULL`), irrécupérable par jointure, corrigée au prochain reseed. | Signaux affichés mais non actionnables | S | Haute |
| PC-033 | ✅ **Résolu (20/07)** | **Blocages de rate limiting — les préflights CORS consommaient le quota** : `RateLimitFilter` (bucket4j, par IP, `OncePerRequestFilter` monté sur `/api/*` **avant** Spring Security) comptait **aussi** les `OPTIONS`. Le front étant sur une autre origine (`localhost:3000` → `localhost:8080`), chaque requête non simple en générait un → **quota réel divisé par deux**. Aggravants : la vue « Ma file » émettait **`3 + 2N`** requêtes par affichage (un appel cycles **et** un appel pages **par projet**) ; le profil `DEFAULT` est de **200 req/60 s** et `refillIntervally` rend **tous les jetons d'un coup** en fin de fenêtre → attente réelle de **0 à 60 s** (et non ~10 s) ; **aucun `Retry-After`** n'était émis et le front n'avait **aucun traitement du 429** (les stores avalaient l'erreur → application figée en apparence). **Correctifs** : `shouldNotFilter` exclut `OPTIONS` ; émission de `Retry-After` + `X-RateLimit-Remaining`, **exposés via `CorsConfig.setExposedHeaders`** (sinon masqués au JS en cross-origin) ; endpoints agrégés `GET …/my-cycles` et `GET …/my-pages` ; toast dédié au 429 dans `client.ts` avec le délai réel. **Mesures live** : 20 préflights `OPTIONS` → **0 jeton** consommé (199 → 198, seul le GET réel compte) ; 429 → `Retry-After: 57` ; « Ma file » passe de `3+2N` à **3 appels agrégés** (0 appel par projet mesuré). | Application figée sous usage normal | M | Haute |
| PC-034 | ✅ **Résolu (20/07)** | **Contrôle d'accès manquant sur les pièces jointes d'issue** : `AttachmentService` ne faisait qu'une vérification de **scope** (`findScopedIssue` — « l'issue appartient-elle bien au projet et au workspace de l'URL ? »), qui ne dit **rien de qui** demande. `AttachmentController.list` injectait `@AuthenticationPrincipal Jwt jwt` **sans jamais le lire**, et `listByIssue` ne recevait **aucun `userId`** ; un grep de `WorkspaceMember\|ProjectMember\|hasAccess\|assertMember` sur tout l'arbre `modules/ged` ne renvoyait **aucun résultat** — en contravention de la règle du projet « autorisation au niveau service : vérifier `WorkspaceMember`/`ProjectMember` + rôles ». **Portée réelle, plus étroite que soupçonné au départ** : un compte **totalement étranger au workspace** était **déjà** bloqué en amont par `WorkspaceAccessInterceptor` (mesuré : **403** « Accès refusé : vous n'êtes pas membre de cet espace de travail », en lecture **comme** en upload, avec le compte `test@taskforce.dev`). L'exploitable était donc : **un membre du workspace pouvait lire et téléverser les pièces jointes d'un projet PRIVÉ dont il n'est pas membre** — aggravé par l'**URL présignée MinIO**, qui n'exige ensuite **plus aucune authentification pendant une heure** : la fuite **survit à la requête**. **Correctif** : deux helpers explicites au-dessus de `findScopedIssue`, sur le modèle déjà en place dans `PageService` — lecture (`listByIssue`) → `ProjectVisibilityGuard.assertCanView` (projet invisible = **404, jamais 403** : on ne révèle pas son existence) ; écriture (`upload`) → `assertCanWrite` (404 si invisible, refus si rôle `VIEWER`, en lecture seule) ; `delete` → garde placée **AVANT** le contrôle de propriété existant, car un non-membre recevait auparavant un 403 « vous n'êtes pas le propriétaire » qui **confirmait l'existence** de la pièce jointe. `listByIssue` prend désormais un `userId`, transmis par le contrôleur (signature passée de **3 à 4 arguments**). **Vérification** : suite backend complète verte — **759 tests, 0 échec, 0 erreur** (contre **755** avant, soit **+4 cas**) ; nouveau bloc `@Nested` « Contrôle d'accès (IDOR) » dans `AttachmentServiceIntegrationTest` (non-membre en lecture → 404, non-membre en upload → 404, membre du projet → lecture OK, `VIEWER` → lecture OK mais upload refusé, `BusinessException`). **Preuve end-to-end en dev**, compte `admin@taskforce.dev` (MEMBER du workspace `pierre`, **non-membre** du projet privé 84) : `GET /api/workspaces/pierre/projects/84/issues/4828/attachments` → **404 « Projet introuvable »** ; `GET /api/workspaces/taskforce-demo/projects/78/issues/4826/attachments` → **200** avec 1 pièce jointe — le chemin légitime est **intact**. ⚠️ **Piège de seed corrigé** (le même qu'en PC-021) : le seed du test d'intégration existant créait un workspace **sans ligne `WorkspaceMember` pour son propriétaire**, ce qui rendait même l'owner **non-admin** aux yeux de `ProjectVisibilityGuard` ; repris du helper documenté de `PageServiceIntegrationTest`. | Fuite de pièces jointes de projet privé | S | Haute |
| PC-035 | ✅ **Résolu (16/08)** | **Rétrogradation d'abonnement Business→Basic par le webhook Stripe** : `STRIPE_PRICE_ID_BASIC == STRIPE_PRICE_ID_BUSINESS` (même price-id en `.env.dev`) → sur `customer.subscription.updated`, le reverse-mapping price-id→plan renvoyait Basic pour un Business. **Corrigé (16/08)** : `StripeService.getPlanForPriceId` renvoie **`null` si le price-id est ambigu** (matche plusieurs forfaits) → pas de resync depuis un signal non fiable ; le plan reste celui posé par `checkout.session.completed` (metadata). `StripeServiceTest` cas ambigu, suite **10/10**. Reste config : price Business distinct + `stripe listen`. Cf. bloc daté 16/08 en tête de §1. | Facturation faussée (downgrade non voulu) | S | Haute |

## 2. Détails par problème

### PC-001 🔴 — Préfixe `/api` manquant (5 contrôleurs)
**Symptôme :** appels front vers cycles, teams, pages, discussions, chat → 404.
**Cause :** aucun `context-path` configuré, et ces 5 contrôleurs omettent `/api` dans `@RequestMapping`.
**Correctif :** ajouter `/api` à ces 5 `@RequestMapping` **ou** poser `context-path: /api` et retirer `/api`
des 16 autres contrôleurs (la 1ère option est moins risquée).
**Vérif :** `GET /api/workspaces/{slug}/teams` renvoie 200, pas 404. → DT-001, [API §4.1](../05-api/API.md).

### PC-002 🟠 — Constantes de routes front absentes
**Symptôme :** `Cannot read properties of undefined` à l'ouverture de Messages, Intégrations, upload de PJ,
ou Roadmap. **Cause :** `MESSAGE_ROUTES`/`INTEGRATION_ROUTES`/`ATTACHMENT_ROUTES`/`ROADMAP_ROUTES` non
déclarées. **Correctif :** déclarer les 4 groupes dans `api-routes.ts` (chemins avec `/api` ; messages
nécessite aussi PC-001). → DT-002.

### PC-003 🟠 — Import `profile-service.ts`
`frontend/lib/api/profile-service.ts:1` → `import { apiClient } from "./client";`. → DT-003.

### PC-004 🟠 — Refresh auth
Aligner le chemin (`/api/auth/refresh` vs `/api/auth/refresh-token`) et implémenter refresh/révocation dans
`AuthController`/`AuthService`/`JwtService`. → DT-004, DT-007.

### PC-005 🟠 — Webhooks Stripe
Implémenter les handlers de `StripeWebhookController` (subscription.updated/deleted, invoice.*) → mise à jour
`Subscription`/`SubscriptionHistory`. → DT-005.

### PC-006 → PC-015 (résumé)
PC-006 `team-store` parité CRUD (dépend de PC-001) · PC-007 réutiliser `ai_runs`/`insight_snapshots` (V35) +
gardes timeout/quota `GroqService` · PC-008 câbler `EmailService` dans `SalesService` · PC-009 vrai SSE Groq
dans `AssistantController` · PC-010 épopée QA/tests (QA.1–6, T.1–6) · PC-011 retirer `messages/data.ts` après
chat OK · PC-012 décider garder/supprimer `ai-service/` · PC-013 câbler le dialog create-issue · PC-014
introduire les flags IA · PC-015 corriger commentaire `CorsConfig.java:65` + vérifier chemin actuator.
Références : voir [Dette technique](./Dette_Technique.md) (DT-006 → DT-022).

## 3. Notes pour les agents IA

<blockquote class="important">
<strong>Confirmés dans le code</strong> (confiance haute) : PC-001, 002, 003, 004, 008, 009, 012.
<strong>Rapportés / à re-vérifier</strong> (moyenne) : PC-006, PC-011, PC-015.
</blockquote>

Corriger **PC-001 + PC-002 ensemble** débloque la plus grande surface (5+ domaines) pour le moindre effort —
meilleur ROI, à faire en premier, puis re-passer les vérifs de [Contrats API](../05-api/API.md). Ce tableau reflète
le dépôt au 08/06/2026 sur la branche `feat/dashboard` : re-vérifier les références ligne/chemin avant d'éditer.

---

> **Note Brain OS** — Inventaire source : [Dette technique](./Dette_Technique.md).

**Dernière mise à jour :** 16/08/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
