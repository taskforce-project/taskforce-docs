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
| AuthController | `/api/auth` (inscription : `otpSent=false` quand l'instance ne vérifie pas les adresses, `SIGNUP_EMAIL_VERIFICATION=false`, compte prêt ; mot de passe oublié sans SMTP : 400, 19/10/2026) | ✅ |
| UserController | `/api/users` | ✅ |
| WorkspaceController | `/api/workspaces` | ✅ |
| ProjectController | `/api/workspaces/{slug}/projects` | ✅ |
| IssueController | `/api/workspaces/{slug}/projects/{projectId}/issues` | ✅ |
| AnalyticsController | `/api/workspaces/{slug}/analytics` | ✅ |
| AnalysisController | `/api/workspaces/{slug}` (→ `/analysis`, `/projects/{id}/brief`, `/priorities/{id}`) | ✅ |
| AssistantController | `/api/workspaces/{slug}/assistant` | ✅ |
| PersonalAccessTokenController | `/api/users/me/tokens` (→ `GET` liste sans valeur, `POST` création, la valeur n'est rendue qu'ici, `DELETE /{id}` révocation) : jetons personnels, refusés partout sauf sur le serveur MCP (lot 5) | ✅ |
| McpServerController | `/api/workspaces/{slug}/mcp` (→ `POST` JSON-RPC 2.0, `GET` et `DELETE` 405) : serveur MCP de l'instance, 12 outils ; réponse JSON-RPC, pas l'enveloppe `ApiResponse` (lot 5) | ✅ |
| AiStatusController | `/api/ai/status` (→ `GET`) : état de l'IA de l'instance (configurée, chat et embeddings joignables, modèles), relu par le backend toutes les 30 s (lot 4, ADR-019) | ✅ |
| McpActionController · McpOAuthCallbackController | `/api/workspaces/{slug}/mcp` (`/actions/execute`, `/servers`, `/servers/{key}/oauth/start`) · public `/api/mcp/oauth/callback` | ✅ |
| ProfileController | `/api/workspaces/{slug}/profile` | ✅ |
| NotificationController | `/api/workspaces/{slug}/notifications` | ✅ |
| MyWorkController | `/api/workspaces/{slug}` (`/my-issues`, `/my-cycles` ; `/my-pages` retiré le 28/10/2026 avec les Pages) | ✅ |
| RoadmapController | `/api/workspaces/{slug}/roadmap` | ✅ |
| WebhookController | `/api/workspaces/{slug}/webhooks` (+ `/{id}/secret`, `/{id}/test`, `/{id}/deliveries`), propriétaires et admins seulement | ✅ |
| IntegrationController | `/api/workspaces/{slug}/integrations/...` + `/api/integrations/*/callback` (`code`, `state`, `error` facultatifs : toujours une redirection vers l'app, `github=` ou `slack=connected` ou `error`, 19/10/2026) ; `GET github/connect?returnTo=` (chemin applicatif où revenir après le consentement, validé, 21/09/2026) | ✅ |
| ~~Billing, Stripe, StripeWebhook, Sales~~ | `/api/billing`, `/api/stripe`, `/api/webhooks/stripe`, `/api/sales`, `/api/auth/select-plan`, `/api/workspaces/{slug}/usage` : retirés le 18/10/2026 (ADR-016) | ➖ |
| ~~Feedback et endpoints sans appelant~~ | `POST /api/feedback` ; `POST /api/users/me/password/reset`, `POST /api/users/me/data-request`, `GET /api/workspaces/current` ; sous `/api/workspaces/{slug}` : `POST /ai/conversations`, variante `text/event-stream` de `POST /assistant`, `GET /analysis/{jobId}`, `GET /notifications/unread-count`, `GET /projects/{id}/activity` (remplacé par `GET /projects/activity`) : retirés le 18/10/2026 (lot 3) | ➖ |
| FileController / AttachmentController (ged) | `/api/files` · `/api/workspaces/{slug}/projects/{projectId}/issues/{issueId}/attachments` | ✅ |
| CycleController | `/api/workspaces/{slug}/projects/{projectId}/cycles` | ✅ |
| TeamController | `/api/workspaces/{slug}/teams` | ✅ |
| PageController | Retiré le 28/10/2026 (ménage de la v2) : écrans, API et entité supprimés ; la table `pages` reste et voyage dans les fichiers de projet | retiré |
| KnowledgeController (Brain OS) | `/api/workspaces/{slug}/brain` (→ `GET` vue d'ensemble, `POST /search`, `POST /nodes`, `PATCH /nodes/{id}`, `PATCH /nodes/{id}/move`, `DELETE /nodes/{id}` ; `POST /files` dans `BrainAttachmentController`) ; `POST /reseed`, `GET /nodes`, `GET /nodes/{id}`, `POST /edges` et `DELETE /edges/{id}` retirés le 18/10/2026 (lot 3, ADR-017) : les liens viennent des `#tags` et des `[[wikilinks]]`. `POST /search` est sémantique au sein du modèle d'embeddings courant, en plein texte sans embeddings (lot 4, V94) | ✅ |
| ProjectExportController | `/api/workspaces/{slug}/projects/{projectId}/export` | ✅ |
| ProjectBundleController (transfer) | `/api/workspaces/{slug}/projects` (→ `GET /{projectId}/bundle` fichier de projet en zip, `POST /import` corps `application/zip`, 201 + projet créé) : un projet entier passe d'une instance à l'autre, webapp ou app desktop (20/10/2026) | ✅ |
| WorkspaceBundleController (transfer) | `/api/workspaces` (→ `GET /{slug}/bundle` fichier d'espace en zip : l'espace, son Brain OS et les projets visibles ; `POST /import` corps `application/zip`, 201 + nouvel espace dont la personne est propriétaire) : tout le travail passe d'une instance à l'autre, webapp ou app desktop (20/10/2026) | ✅ |
| DesktopTransferController (transfer) | `/api/auth/desktop/transfer` (→ `POST /projects` espaces et projets visibles, `POST /bundle` fichier d'un projet, `POST /import?workspace=` avec l'en-tête `X-TaskForce-Session`, `POST /workspace` fichier d'un espace entier, `POST /workspace-import` avec le même en-tête) : pour l'app desktop, avec sa seule session `tfa_`, 401 si elle est finie ; profil `!desktop` (20/10/2026) | ✅ |
| DeliveryController | `/api/workspaces/{slug}/delivery` (→ `GET /providers`, `POST /issues/{id}/delegate`, `GET /issues/{id}/run`, `GET /runs`, `GET /runs/{id}/activity?after=` chronologie et demandes, `POST /runs/{id}/approvals/{approvalId}` décision ; `GET /providers?projectId=` dit pour chaque agent `ready` et `reason`) ; un run renvoie aussi `issueKey`, `issueTitle`, `projectId`, `projectName` (21/09/2026) ; fournisseurs : `claude-code` (runner local) et `github-copilot` (lot 5) ; clés `GET/POST/DELETE /{anthropic\|cursor}` retirées le 18/10/2026 (lot 3) | ✅ |
| DeliveryRunnerController | `/api/delivery/runner` (→ `POST /claim`, `POST /runs/{id}/heartbeat`, `POST /runs/{id}/result`, `POST /runs/{id}/events`, `POST /runs/{id}/approvals`, `GET /runs/{id}/approvals/{approvalId}`) : endpoints **machine** du runner local (ADR-013), jeton de compte de service Keycloak, 403 pour un jeton utilisateur ; n'existent que si `delivery.local-runner.enabled=true` ; masqués de la doc Fern | ✅ |
| DesktopSignInController | `/api/auth/desktop` (`POST /token` code à usage unique + vérificateur PKCE → jeton `tfa_` ; `POST /session` relit le compte, 401 = session fermée ; `POST /revoke`) : public, limité comme un login (`/session` comme le renouvellement) ; profil `!desktop` (19/10/2026) | ✅ |
| DesktopSessionController | `/api/users/me/desktop-sessions` (`POST /authorize` → adresse de retour de l'app avec son code ; `GET` ordinateurs connectés ; `DELETE /{id}`) (19/10/2026) | ✅ |
| PasskeySignInController | `/api/auth/passkey` (`POST /options` défi, 30/min/IP ; `POST /login` réponse du navigateur → session, refresh en cookie, 10/min/IP) : public (19/10/2026) | ✅ |
| PasskeyController | `/api/users/me/passkeys` (`POST /options`, `POST` ajout, `GET` liste, `DELETE /{passkeyId}`) (19/10/2026) | ✅ |
| RunnerAuthController | `/api/auth/runner` (→ `POST /token`) : `client_credentials` relayé vers Keycloak pour un client `tf-runner-*` ; public, limité en débit comme un login ; même condition d'activation | ✅ |
| RunnerProvisioningController | `/api/delivery/runners` (→ `GET` état, `POST` provisionner) : **libre-service** « Connect a runner » (28/09/2026), jeton **utilisateur** ; crée ou met à jour l'identité du runner de l'appelant (client `tf-runner-u<id>` en `client_credentials` seul, rôle `delivery-runner`, propriétaire = e-mail de l'appelant) et rend le secret **une seule fois** (régénéré à chaque `POST`) ; `GET` ne renvoie jamais de secret ; hors du préfixe machine `/api/delivery/runner/` ; même condition d'activation | ✅ |

<blockquote class="important">
Tous les contrôleurs portent désormais <code>/api</code> (règle d'or n°1, vérifiée au 28/08/2026). Les anciens « Chat » (<code>ChannelController</code>) et « Discussions » (<code>DiscussionController</code>) n'existent plus dans le code : ni contrôleur, ni route. Voir §4.1.
</blockquote>

## 3. Cartographie par domaine

Services front dans `frontend/lib/api/`. Lecture : `fonction front` → `méthode HTTP chemin` → contrôleur.

**Aligné ✅** — Auth (`auth-service` ↔ `AuthController`), Utilisateur (`user-service` ↔ `UserController`),
Workspace (`workspace-service`), Projet + Labels (`project-service`, `label-service` ↔ `ProjectController` :
CRUD, `/members`, `/teams`, `/labels`, **`GET /activity?days=N`** = activité quotidienne de tous les projets visibles en un appel, pour les sparklines ; l'ancien `GET /{id}/activity` (QA2-32) est retiré le 18/10/2026),
Issue (`issue-service` ↔ `IssueController` : CRUD, **`GET /paged?page&size`** = liste paginée additive pour l'infinite-scroll backlog (QA2-33), `/statuses` + `/reorder`, `/types`, `/comments`,
`/activity`, `/smart-assign`, `/relations`), Analytics (`analytics-service` : `/kpis`, **`/throughput?bucket=DAY|WEEK`** = série throughput, `WEEK` (8 sem., défaut) ou `DAY` (30 j, tendance « 1 mois » du dashboard ; 26/06/2026),
`/burndown`, `/capacity`, `/insights`, **`POST /chart`** = génération de graphe par l'IA (2 modes : série temporelle ou **répartition « X par Y » calculée en base** via un moteur de requête whitelisté — le modèle interroge la vraie DB sans écrire de SQL ; 10/07/2026), **`POST /breakdown`** = ré-exécution d'une répartition, **`GET/POST /charts`** + **`DELETE /charts/{id}`** = graphes épinglés « Custom »), Notifications (`notification-service`), Sales, Avatars (`FileController`).

**Workflows d'analyse IA ✅** (10/07/2026) — `analysis-service` ↔ `AnalysisController`. L'analyse est **asynchrone** :
`POST /analysis` (`{projectId, depth}`) rend immédiatement un job, exécuté en `@Async` par `AnalysisJobRunner` ;
`GET /analysis` (dock) · `DELETE /analysis/{jobId}` (masquage) ·
`POST /analysis/{jobId}/answer` (HITL — reprise après clarification du modèle).
La décision produite est persistée : `GET /projects/{projectId}/brief` (→ `null` si aucune analyse aboutie), et chaque
priorité est actionnable : `POST /priorities/{id}/accept` (→ crée l'issue liée), `/pin`, `/dismiss` (bascules), `PUT /priorities/{id}` (édition).
Le job publie son plan d'étapes sur `/topic/analysis.{workspaceId}` (STOMP) ; **le front n'y est pas encore abonné** et
retombe sur un polling 5 s tant qu'un workflow est actif.
> Remplace l'ancien `POST /projects/{projectId}/decision` (synchrone, non persisté), **supprimé** le 10/07/2026 avec `DecisionController`.
> `GET /analysis/{jobId}` est retiré le 18/10/2026 (lot 3) : le panneau lit la liste.

**Hôte MCP ✅** (12/07/2026) — `McpActionController` (`/api/workspaces/{slug}/mcp`). TaskForce **consomme** des
serveurs MCP externes : un connecteur du workspace portant un `mcpUrl` (config chiffrée) expose ses outils à
Cortex (découverte `tools/list`, namespacing `<connecteur>__<outil>`, fusion dans la boucle de tool-calling).
Les **écritures externes** sont **proposées** (toolCall `pending`) puis exécutées après validation via
`POST /mcp/actions/execute` (`{toolRef, arguments}` ; `toolRef` sous le nom exposé à Cortex ou d'origine). Gestion
des serveurs : `GET /mcp/servers` (joignabilité, nom, outils après allow-list `mcpAllow`), `POST /mcp/servers`
(`{connectorKey, name?, mcpUrl, mcpToken?, headerName?, mcpAllow?}`, config **chiffrée**), `DELETE
/mcp/servers/{connectorKey}`. Clé : un préréglage du catalogue, `custom` pour un nouveau serveur personnalisé (nom
obligatoire, clé `custom-<slug>` tirée du nom), ou la clé `custom-…` d'un serveur existant ; les natives et les clés
inconnues sont refusées (lot 6). Le jeton part en `Authorization: Bearer`, ou tel quel dans `headerName`. Ouvert à tout
workspace (ADR-016) ; une écriture proposée par Cortex n'est offerte qu'à un propriétaire ou un admin, et toujours
validée. Catalogue : `GET /integrations/catalog` (3 natives, 25 préréglages, serveurs du workspace) ; les routes
`/integrations/connectors/{key}` sont retirées (lot 6). Détail : [IA-MCP-002](../02-produit/IA.md).

**OAuth MCP 1-clic ✅** (02/09/2026, `[TF-MCP-02]`) : connexion d'un serveur MCP **sans coller de token**, via OAuth 2.1 **générique** (valable pour tout serveur conforme, zéro code par service). `POST /mcp/servers/{key}/oauth/start` (`{mcpUrl, name?, returnTo?}`, propriétaire ou admin ; `name` gardé jusqu'au callback, V97) : **découverte** (probe `401`/`WWW-Authenticate` → Protected Resource Metadata RFC 9728 → Authorization Server Metadata RFC 8414) + **Dynamic Client Registration** RFC 7591 + **PKCE S256**, renvoie l'URL d'autorisation (le front y redirige). `GET /api/mcp/oauth/callback` (**public** : résout le workspace via le `state` anti-CSRF, jamais l'URL) : échange le code, stocke les tokens **chiffrés** dans le `config` de la connexion (**refresh auto** avant expiration via `McpTokenService`), redirige **toujours** vers l'UI. Table éphémère `mcp_oauth_states` (V82). **`SsrfGuard`** sur chaque fetch de découverte/DCR/token. Prouvé en live contre Linear (découverte + DCR + URL d'autorisation OK). Le champ URL + token reste en fallback bring-your-own. **Déployé en prod le 02/09/2026** (#218, `--admin --squash`, auto-deploy VM1+VM2 ; V82 appliquée, backend sain, callback public vérifié `302` vers le front prod). Durcissement (#217) : `SsrfGuard` valide aussi l'`authorization_endpoint` (issu de metadata semi-fiable) avant la redirection navigateur.

**Webhooks sortants ✅** (18/10/2026, lot 6, ADR-020) : `WebhookController` (`/api/workspaces/{slug}/webhooks`),
propriétaires et admins seulement, lecture comprise. `POST` (`{url, eventTypes, active?}`) renvoie `{webhook, secret}`,
le secret n'étant montré qu'une fois ; `PUT /{id}` (URL, événements, pause) ; `POST /{id}/secret` (nouveau secret) ;
`POST /{id}/test` (envoie `ping` et renvoie le résultat) ; `GET /{id}/deliveries` (20 derniers envois) ; `DELETE /{id}`.
Événements : `issue.created`, `issue.updated`, `issue.deleted`, `comment.created`, `cycle.completed` (liste vide = tous).
Chaque envoi est un POST JSON `{id, type, createdAt, url, workspace, actor, data}` avec `X-TaskForce-Event`,
`X-TaskForce-Delivery`, `X-TaskForce-Timestamp` et `X-TaskForce-Signature: sha256=HMAC-SHA256(secret, timestamp + "." +
corps)` ; sans réponse 2xx, nouvelles tentatives après 1 min, 5 min, 30 min, 2 h et 6 h.

**GitHub et Slack ✅** (19/10/2026, lot 6, ADR-020) : `POST /integrations/github/issues/{issueId}/links` vérifie
`repoFullName` (owner/name), `prNumber` (positif), `commitSha` (hash) et des liens `prUrl`, `commitUrl` limités à
`https://github.com/` (400 sinon) ; une PR demande son numéro, un commit son hash. `GET .../links` relit chez GitHub le
statut des PR non fusionnées (au plus toutes les 5 minutes par lien, 5 liens par appel) et l'enregistre. Une erreur de
GitHub devient un message lisible (reconnecter GitHub, dépôt introuvable, quota atteint, GitHub injoignable, nom déjà
pris à la création d'un dépôt). `DELETE /integrations/github` et `DELETE /integrations/slack` révoquent le jeton chez
le service (au mieux) ; Slack retire aussi les canaux. Slack demande les portées `chat:write`, `chat:write.public`,
`channels:read`, `channels:history`, `users:read` et `incoming-webhook` ; `POST /integrations/slack/channels` refuse un
identifiant mal formé, un événement inconnu ou un canal déjà configuré. Dépôt d'un projet : `PUT /projects/{id}/repo`
(`{mode: "LINK", repoFullName}` ou `{mode: "CREATE", repoName, privateRepo}`) et `DELETE /projects/{id}/repo`, appelés
par la création du projet et par ses réglages.

**« Ma file » — endpoints agrégés ✅** (20/07/2026) — `MyWorkController` (`/api/workspaces/{slug}`). La vue est
**cross-projets** : elle affichait ses cycles et ses documents en rappelant l'API **projet par projet**, soit
`3 + 2N` requêtes par affichage (N = nombre de projets) — assez pour épuiser le quota de rate limiting à
l'usage normal. Deux endpoints agrégés remplacent ces boucles :
`GET /my-cycles` → `ApiResponse<List<MyWorkCycleResponse>>` avec
`MyWorkCycleResponse = { projectId, projectName, cycle: CycleResponse }` (décompte d'issues groupé en **une**
requête, `CycleIssueRepository.countByCycleIds`) et `GET /my-pages` →
`ApiResponse<List<MyWorkPageResponse>>` avec `MyWorkPageResponse = { projectId, projectName, page: PageResponse }`
(borné à **50 documents récents**). Périmètre des deux : les projets visibles par l'appelant
(`ProjectVisibilityGuard.viewableProjectIds`). L'enveloppe `{projectId, projectName}` est nécessaire parce que
`CycleResponse`/`PageResponse` sont normalement servis depuis une route **déjà scopée par projet**.
Mesure : « Ma file » passe de `3+2N` à **3 appels**, 0 appel par projet.
> ⚠️ `MyWorkController` passe de `@RequestMapping("…/my-issues")` à `@RequestMapping("/api/workspaces/{slug}")`
> + `@GetMapping("/my-issues")` : **l'URL externe de `/my-issues` est inchangée**.

**En-têtes de rate limiting exposés ✅** (20/07/2026) — le 429 était muet côté client : `RateLimitFilter`
n'émettait aucun `Retry-After`, et le profil `DEFAULT` (200 req/60 s, `refillIntervally`) rend tous les jetons
d'un coup en fin de fenêtre — l'attente réelle va donc de **0 à 60 s**, indevinable. Le filtre émet désormais
**`Retry-After`** et **`X-RateLimit-Remaining`**, tous deux **listés dans `CorsConfig.setExposedHeaders`** :
sans cette déclaration, le navigateur les masque au JavaScript en cross-origin et le contrat reste inutilisable.
Les préflights `OPTIONS` sont par ailleurs **exclus du comptage** (`shouldNotFilter`) — ils consommaient un
jeton chacun, divisant le quota réel par deux. Cf. [PC-033](../09-audits/Problemes_Connus.md).
**Lisible par le navigateur depuis le 19/10/2026** ([PC-053](../09-audits/Problemes_Connus.md)) : le 429 partait
sans en-têtes CORS, le limiteur passant avant le filtre CORS ; le navigateur le bloquait et l'app affichait une
panne réseau. `CorsConfig` enregistre désormais le `CorsFilter` en tête de la chaîne servlet : un 429 porte
`Access-Control-Allow-Origin`, `Access-Control-Allow-Credentials` et `Retry-After` (exposé).

**Cycles / Pages / Teams — alignés ✅** (vérifié 28/08/2026) — `CycleController` (`CycleController.java:33`),
`PageController` (`PageController.java:39`) et `TeamController` (`TeamController.java:33`) portent tous
`@RequestMapping("/api/workspaces/…")`. L'ancien défaut de préfixe est corrigé.
> ⚠️ Note (28/08/2026) : **Chat et Discussions retirés du produit** — ni `ChannelController` ni
> `DiscussionController` n'existent dans le code (grep à blanc). Les entrées correspondantes ont été
> supprimées de ce document et de `Spec_API_OpenAPI.md`.

**Cassé (undefined) ❌** — Messages (`message-service`, `MESSAGE_ROUTES`), Intégrations
(`integration-service`, `INTEGRATION_ROUTES`), Pièces jointes (`attachment-service`, `ATTACHMENT_ROUTES`),
Roadmap (`issue-service.getScheduledIssues`, `ROADMAP_ROUTES`) : constantes importées mais **non déclarées**
dans `api-routes.ts`. Les endpoints back des intégrations/pièces jointes/roadmap **existent** (avec `/api`) ;
pour les messages, le back est en plus mal préfixé (cf. §4.1). Voir §4.2.

**Dégradé ⚠️** — Profil (`profile-service` : chemin OK mais import cassé, §4.3), Refresh auth (§4.4).

Groupes de routes **présents** dans `frontend/lib/config/api-routes.ts` : `AUTH`, `USER`,
`WORKSPACE`, `PROJECT`, `ISSUE`, `CYCLE`, `ANALYTICS`, `NOTIFICATION`, `PROFILE`, `PAGE`, `TEAM`,
`DISCUSSION`. **Absents** (importés mais jamais déclarés) : `MESSAGE_ROUTES`, `INTEGRATION_ROUTES`,
`ATTACHMENT_ROUTES`, `ROADMAP_ROUTES`.

## 4. Incohérences détectées

### 4.1 — Préfixe `/api` : résolu (au 28/08/2026)

**Plus d'écart.** Tous les contrôleurs existants déclarent `/api` dans leur `@RequestMapping`
(règle d'or n°1). Les 3 contrôleurs autrefois signalés sont corrigés — `CycleController.java:33`,
`TeamController.java:33`, `PageController.java:39` — et les 2 autres (`DiscussionController`,
`ChannelController`) n'existent plus dans le code. L'ancien risque 404 (PC-001) est clos.

### 4.2 — Constantes de routes front absentes → erreur runtime (HAUTE)

`message-service.ts`, `integration-service.ts`, `attachment-service.ts` et
`issue-service.ts::getScheduledIssues` importent des constantes absentes de `api-routes.ts`. Tout appel
lève `Cannot read properties of undefined`. → [PC-002](../09-audits/Problemes_Connus.md).

### 4.3 — Import cassé dans `profile-service.ts` (MOYENNE)

Ligne 1 : `import apiClient from "./api-client";` — le module `./api-client` n'existe pas ; le vrai
client est l'export **nommé** `apiClient` de `./client`. `getProfile()` échoue au runtime. → [PC-003](../09-audits/Problemes_Connus.md).

### 4.4 — Refresh auth : implémenté, refresh token en cookie HttpOnly (au 28/08/2026)

Le backend implémente `POST /api/auth/refresh-token` (`AuthController.java:281-310`) : il lit le
refresh token depuis le cookie `tf_refresh` (repli sur le corps pour les sessions d'avant migration),
renvoie **401** si le token est vide/absent, et re-pose le cookie à chaque succès. Le `login`
(`AuthController.java:218-227`) renvoie l'`accessToken` en corps et met le refresh token en cookie
`HttpOnly; Secure; SameSite=Lax; Path=/api/auth` (`RefreshTokenCookie.java:59-65`) — plus jamais dans
le corps JSON. Le `logout` purge le cookie ; le callback OAuth (`OAuthLoginController.java:105-112`)
pose le même cookie. Détail des contrats : `Spec_API_OpenAPI.md` §2.1–2.2.
> ▶ Reste côté front : vérifier que `AUTH_ROUTES.REFRESH_TOKEN` pointe sur `/api/auth/refresh-token`.

## 5. Procédure pour câbler un nouvel endpoint

<div class="highlight-box">

1. Déclarer le chemin du contrôleur **avec `/api`** (`@RequestMapping`).
2. Ajouter la constante dans `frontend/lib/config/api-routes.ts`.
3. La consommer dans le service `lib/api/*-service.ts`.
4. Lire `response.data.data` (enveloppe `ApiResponse<T>`).
5. Mettre à jour [ce document](./API.md) et le [hub](../../Brain_OS.md).

</div>

---

> **Note Brain OS** — Vérifié dans le code au 08/06/2026 (branche `feat/dashboard`), puis
> ré-audité contrôleur par contrôleur le 28/08/2026 (préfixe `/api` généralisé, Chat/Discussions
> retirés, flux refresh en cookie HttpOnly).

**Dernière mise à jour :** 18/10/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
