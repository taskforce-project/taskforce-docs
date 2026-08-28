---
id: spec-api-openapi
title: Spécification API REST — TaskForce V1
doc_type: api-spec
statut: valide
version: 1.0
date: "28/08/2026"
auteur: Pierre MICHEL
tags: [api, rest, openapi, swagger, endpoints, backend, memoire, rncp, soutenance]
---

# 📡 Spécification API REST — TaskForce V1

> Référence des ~235 endpoints des 42 contrôleurs REST du backend Spring Boot.
> **Source** : annotations `@RequestMapping` / `@GetMapping` / `@PostMapping` /
> `@PatchMapping` / `@DeleteMapping` lues dans `backend/tf-api/src/main/java/…/core/api/`
> et `…/modules/*/api/`.
>
> **Swagger UI** : disponible à `http://localhost:8080/swagger-ui/index.html` (dev).
> **OpenAPI JSON** : `http://localhost:8080/v3/api-docs`.

---

## 1. Conventions

### 1.1 Enveloppe de réponse

Toutes les réponses sont encapsulées dans `ApiResponse<T>` :

```json
{
  "success": true,
  "data": { ... },
  "message": "Opération réussie",
  "statusCode": 200
}
```

Le frontend lit systématiquement `response.data.data` (double `.data`).

### 1.2 Authentification

- **Routes publiques** : aucun en-tête requis (liste complète §1.3).
- **Routes protégées** : `Authorization: Bearer <jwt>` (token **RS256 émis par Keycloak**, validé via JWK + issuer).
- **CSRF** : désactivé (API stateless, bearer token).

### 1.3 Routes publiques (sans JWT)

Définies dans `SecurityConfig.PUBLIC_MATCHERS` :

| Pattern | Usage |
|---|---|
| `/api/auth/**` | Inscription, login, OTP, forgot/reset password, OAuth externe, refresh/logout |
| `/api/invitations/*` | Preview publique d'une invitation par token (1 seul segment ; `/accept` reste JWT) |
| `/api/files/brain/**` | Ressources Brain OS publiques |
| `/api/files/avatars/*` | Avatars servis en `<img>` (pas d'en-tête Bearer possible) |
| `/api/sales/**` | Capture de leads (landing) |
| `/api/stripe/**` | Vérification session Stripe post-checkout |
| `/api/webhooks/stripe` | Webhook Stripe serveur-à-serveur (signature vérifiée dans le contrôleur) |
| `/actuator/**` | Health checks |
| `/swagger-ui/**` + `/v3/api-docs/**` + `/api-docs/**` | Documentation Swagger / OpenAPI |
| `/ws/**` + `/ws-sockjs/**` | WebSocket STOMP (auth gérée au niveau protocole) |
| `/api/integrations/github/callback` | OAuth callback GitHub |
| `/api/integrations/slack/callback` | OAuth callback Slack |

> Source : `SecurityConfig.PUBLIC_MATCHERS` (`SecurityConfig.java:70-93`).

### 1.4 Autorisation au niveau service

La sécurité Spring ne fait qu'un `.anyRequest().authenticated()` — l'autorisation fine
se fait dans les services via `AuthorizationService` :

| Méthode | Rôle requis |
|---|---|
| `getMemberOrThrow(workspaceId)` | MEMBER+ (doit être membre du workspace) |
| `requireManager(workspaceId)` | ADMIN+ (OWNER ou ADMIN) |
| `assertIsOwner(workspaceId)` | OWNER uniquement |

---

## 2. Auth (`/api/auth`)

**Contrôleur** : `AuthController`

| Méthode | Chemin | Description | Auth |
|---|---|---|:---:|
| `GET` | `/api/auth/challenge` | Défi anti-robot au chargement de l'inscription (token + clé de site Turnstile) | Public |
| `POST` | `/api/auth/register` | Étape 1 inscription : données utilisateur + plan sélectionné (vérif. Turnstile) | Public |
| `POST` | `/api/auth/select-plan` | Met à jour le plan sélectionné avant OTP | Public |
| `POST` | `/api/auth/verify-otp` | Vérifie le code OTP (6 chiffres, TTL 15 min) | Public |
| `POST` | `/api/auth/resend-otp` | Renvoi du code OTP | Public |
| `POST` | `/api/auth/login` | Login (email + password) → `accessToken` en corps ; refresh token en cookie | Public |
| `POST` | `/api/auth/forgot-password` | Envoi email reset password | Public |
| `POST` | `/api/auth/reset-password` | Reset password avec token email | Public |
| `POST` | `/api/auth/refresh-token` | Renouvelle l'access token depuis le cookie `tf_refresh` (repli corps) | Public |
| `POST` | `/api/auth/logout` | Révoque les refresh tokens + purge le cookie | JWT |

### 2.1 Refresh token en cookie HttpOnly

Depuis la migration sécurité (OWASP A07), le **refresh token ne transite plus dans le corps JSON** :
il est posé en cookie `Set-Cookie: tf_refresh=…; Path=/api/auth; HttpOnly; Secure; SameSite=Lax`
(`RefreshTokenCookie.java:59-65` — `Secure` actif en prod, inactif en dev localhost).

- `POST /api/auth/login` renvoie `accessToken` dans le corps (`ApiResponse<AuthResponse>`) et met
  `refreshToken` à `null`, le refresh partant uniquement en cookie (`AuthController.java:218-227`).
  Cas 2FA en attente (aucun refresh émis) : réponse renvoyée inchangée, sans cookie.
- `POST /api/auth/refresh-token` lit le cookie `tf_refresh` en priorité, avec repli sur le corps
  `{ refreshToken }` pour les sessions créées avant la migration ; token vide/absent → **401**
  « Refresh token manquant » ; succès → nouveau cookie ; échec → cookie purgé + 401
  (`AuthController.java:281-310`).
- `POST /api/auth/logout` purge le cookie même en cas d'erreur (`AuthController.java:316-337`).

### 2.2 Connexion via un fournisseur externe (`/api/auth/oauth`)

**Contrôleur** : `OAuthLoginController` (endpoints publics — ils précèdent l'authentification).

| Méthode | Chemin | Description | Auth |
|---|---|---|:---:|
| `GET` | `/api/auth/oauth/{provider}/authorize` | URL d'autorisation signée (état anti-CSRF) — `provider` ∈ {github, google} | Public |
| `POST` | `/api/auth/oauth/callback` | Échange `{code, state, redirectUri}` contre une session TaskForce | Public |

Le callback pose le refresh token dans le même cookie `tf_refresh` HttpOnly que le login classique
(`OAuthLoginController.java:105-112`).

---

## 3. Workspace (`/api/workspaces`)

**Contrôleur** : `WorkspaceController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/workspaces` | Liste les workspaces de l'utilisateur | JWT |
| `POST` | `/api/workspaces` | Crée un workspace | JWT |
| `GET` | `/api/workspaces/{slug}` | Détail workspace | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}` | Modifie nom, slug, timezone | OWNER |
| `DELETE` | `/api/workspaces/{slug}` | Supprime le workspace | OWNER |
| `GET` | `/api/workspaces/{slug}/usage` | Métriques d'utilisation (quotas) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/audit` | Journal d'audit RGPD | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/members` | Liste des membres | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/members/invite` | Invite un membre (email + rôle) | ADMIN+ |
| `PATCH` | `/api/workspaces/{slug}/members/{memberId}/role` | Change le rôle d'un membre | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/members/{memberId}` | Retire un membre | ADMIN+ |
| `GET` | `/api/workspaces/current` | Workspace courant de la session | JWT |

---

## 4. Invitations (`/api/workspaces/{slug}/invitations`)

**Contrôleur** : `InvitationController` (`@RequestMapping("/api")`)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `POST` | `/api/workspaces/{slug}/invitations` | Crée une invitation | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/invitations` | Liste les invitations en attente | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/invitations/{invitationId}` | Révoque une invitation | ADMIN+ |
| `GET` | `/api/invitations/{token}` | Détail invitation par token (lien email) | Public |
| `POST` | `/api/invitations/{token}/accept` | Accepte une invitation (email doit matcher) | JWT |
| `GET` | `/api/invitations/mine` | Mes invitations PENDING reçues (bannière in-app) | JWT |
| `POST` | `/api/invitations/mine/{invitationId}/accept` | Accepte une de mes invitations par id | JWT |

> ⚠️ `POST /api/invitations/{token}/accept` exige un **JWT** (`InvitationController.java:90`) : le
> matcher public `/api/invitations/*` est à segment unique — seul `GET /{token}` est public
> (`SecurityConfig.java:75`).

---

## 5. Projets (`/api/workspaces/{slug}/projects`)

**Contrôleur** : `ProjectController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/workspaces/{slug}/projects` | Liste les projets | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects` | Crée un projet | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/health-history` | Projets à risque/critiques par jour (`?days=30`) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/projects/activity` | Activité de tous les projets visibles (`?days=14`) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}` | Détail projet | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/projects/{projectId}` | Modifie un projet | ADMIN+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/archive` | Archive un projet | ADMIN+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/favorite` | Ajoute aux favoris (utilisateur courant) | MEMBER+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/favorite` | Retire des favoris | MEMBER+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}` | Supprime un projet | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/activity` | Activité quotidienne du projet (sparkline, `?days=14`) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/members` | Membres du projet | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/members` | Ajoute un membre | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/members/{memberId}` | Retire un membre | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/teams` | Équipes associées au projet | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/teams` | Associe une équipe | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/teams/{teamId}` | Dissocie une équipe | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/labels` | Labels du projet | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/labels` | Crée un label | ADMIN+ |
| `PUT` | `/api/workspaces/{slug}/projects/{projectId}/labels/{labelId}` | Modifie un label | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/labels/{labelId}` | Supprime un label | ADMIN+ |

> ⚠️ Modification de label = **`PUT`** (`ProjectController.java:363`), pas `PATCH`. La suppression de
> membre projet cible `{memberId}` (`ProjectController.java:271`).

### 5.1 Export de projet

**Contrôleur** : `ProjectExportController` (`ProjectExportController.java:38-59`)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/export` | Export complet (issues + descriptions + commentaires + activité), `?format=json\|csv` | MEMBER+ |

> Réponse en **téléchargement** (`Content-Disposition: attachment`, contenu brut) — exception assumée
> à l'enveloppe `ApiResponse` (c'est un fichier). Autorisation par visibilité projet.

---

## 6. Issues (`/api/workspaces/{slug}/projects/{projectId}/issues`)

**Contrôleur** : `IssueController`

| Méthode | Chemin (préfixe `/api/workspaces/{slug}/projects/{projectId}/issues`) | Description | Rôle |
|---|---|---|:---:|
| `GET` | `` (base) | Liste toutes les issues du projet | MEMBER+ |
| `GET` | `/paged` | Liste paginée (infinite scroll backlog) | MEMBER+ |
| `POST` | `` | Crée une issue | MEMBER+ |
| `GET` | `/{issueId}` | Détail issue | MEMBER+ |
| `PATCH` | `/{issueId}` | Modifie une issue | MEMBER+ |
| `DELETE` | `/{issueId}` | Supprime une issue | ADMIN+ |
| `PATCH` | `/{issueId}/archive` | Archive une issue | MEMBER+ |
| `PATCH` | `/{issueId}/unarchive` | Désarchive une issue | MEMBER+ |
| `PATCH` | `/{issueId}/pin` | Épingle / désépingle | MEMBER+ |
| `GET` | `/statuses` | Liste les statuts custom | MEMBER+ |
| `POST` | `/statuses` | Crée un statut | ADMIN+ |
| `PATCH` | `/statuses/{statusId}` | Modifie un statut | ADMIN+ |
| `DELETE` | `/statuses/{statusId}` | Supprime un statut | ADMIN+ |
| `POST` | `/statuses/reorder` | Réordonne les statuts | ADMIN+ |
| `GET` | `/types` | Types d'issues (bug/feature/task…) | MEMBER+ |
| `GET` | `/{issueId}/comments` | Commentaires d'une issue | MEMBER+ |
| `POST` | `/{issueId}/comments` | Ajoute un commentaire | MEMBER+ |
| `PATCH` | `/{issueId}/comments/{commentId}` | Modifie un commentaire | MEMBER+ |
| `DELETE` | `/{issueId}/comments/{commentId}` | Supprime un commentaire | MEMBER+ |
| `GET` | `/{issueId}/activity` | Journal d'activité | MEMBER+ |
| `POST` | `/{issueId}/smart-assign` | Smart-assign LLM (top-3 suggérés) | MEMBER+ |
| `POST` | `/smart-assign/preview` | Preview smart-assign multi-issues | MEMBER+ |
| `POST` | `/smart-assign/bulk` | Application bulk des suggestions | ADMIN+ |
| `GET` | `/{issueId}/children` | Sous-tâches d'une issue | MEMBER+ |
| `GET` | `/{issueId}/cycles` | Cycles auxquels l'issue est rattachée | MEMBER+ |
| `POST` | `/{issueId}/ai/spec` | Brouillon IA de spec + prompt d'exécution (`?deep=`, non persisté) | MEMBER+ |
| `POST` | `/{issueId}/ai/spec/approve` | Persiste la spec approuvée en nœud Brain OS | MEMBER+ |
| `GET` | `/{issueId}/checklist` | Items de checklist | MEMBER+ |
| `POST` | `/{issueId}/checklist` | Ajoute un item de checklist | MEMBER+ |
| `PATCH` | `/{issueId}/checklist/{itemId}` | Modifie un item de checklist | MEMBER+ |
| `DELETE` | `/{issueId}/checklist/{itemId}` | Supprime un item de checklist | MEMBER+ |
| `GET` | `/{issueId}/worklogs` | Temps passé (worklogs) | MEMBER+ |
| `POST` | `/{issueId}/worklogs` | Enregistre du temps | MEMBER+ |
| `DELETE` | `/{issueId}/worklogs/{worklogId}` | Supprime une entrée de temps | MEMBER+ |
| `GET` | `/{issueId}/relations` | Relations (bloque, est bloqué par…) | MEMBER+ |
| `POST` | `/{issueId}/relations` | Crée une relation | MEMBER+ |
| `DELETE` | `/{issueId}/relations/{relationId}` | Supprime une relation | MEMBER+ |

---

## 7. Cycles (`/api/workspaces/{slug}/projects/{projectId}/cycles`)

**Contrôleur** : `CycleController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les cycles du projet | MEMBER+ |
| `POST` | (base) | Crée un cycle | ADMIN+ |
| `GET` | `/{cycleId}` | Détail cycle | MEMBER+ |
| `PATCH` | `/{cycleId}` | Modifie un cycle | ADMIN+ |
| `DELETE` | `/{cycleId}` | Supprime un cycle | ADMIN+ |
| `GET` | `/{cycleId}/issues` | Issues du cycle | MEMBER+ |
| `POST` | `/{cycleId}/issues` | Ajoute une issue au cycle | MEMBER+ |
| `DELETE` | `/{cycleId}/issues/{issueId}` | Retire une issue du cycle | MEMBER+ |

---

## 8. Pages wiki (`/api/workspaces/{slug}/projects/{projectId}/pages`)

**Contrôleur** : `PageController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les pages du projet | MEMBER+ |
| `POST` | (base) | Crée une page | MEMBER+ |
| `GET` | `/{pageId}` | Contenu d'une page | MEMBER+ |
| `PATCH` | `/{pageId}` | Modifie une page (titre, contenu Markdown) | MEMBER+ |
| `DELETE` | `/{pageId}` | Supprime une page | ADMIN+ |

---

## 9. Équipes (`/api/workspaces/{slug}/teams`)

**Contrôleur** : `TeamController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les équipes | MEMBER+ |
| `POST` | (base) | Crée une équipe | ADMIN+ |
| `GET` | `/{teamId}` | Détail équipe | MEMBER+ |
| `PATCH` | `/{teamId}` | Modifie une équipe | ADMIN+ |
| `DELETE` | `/{teamId}` | Supprime une équipe | ADMIN+ |
| `GET` | `/{teamId}/members` | Membres de l'équipe | MEMBER+ |
| `POST` | `/{teamId}/members` | Ajoute un membre | ADMIN+ |
| `DELETE` | `/{teamId}/members/{userId}` | Retire un membre | ADMIN+ |

---

## 10. Redistribution automatique (`/api/workspaces/{slug}/redistribute`)

**Contrôleur** : `RedistributionController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `POST` | `/preview` | Calcule une redistribution (dry-run) | ADMIN+ |
| `POST` | `/apply` | Applique la redistribution validée | ADMIN+ |

---

## 11. Brain OS (`/api/workspaces/{slug}/brain`)

**Contrôleur** : `KnowledgeController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Récupère le brain du workspace | MEMBER+ |
| `POST` | `/search` | Recherche sémantique (pgvector cosine) | MEMBER+ |
| `POST` | `/reseed` | Re-génère les embeddings | ADMIN+ |
| `GET` | `/nodes` | Liste les nœuds de connaissance | MEMBER+ |
| `GET` | `/nodes/{nodeId}` | Détail d'un nœud | MEMBER+ |
| `POST` | `/nodes` | Crée un nœud | MEMBER+ |
| `PATCH` | `/nodes/{nodeId}` | Modifie un nœud | MEMBER+ |
| `DELETE` | `/nodes/{nodeId}` | Supprime un nœud | ADMIN+ |
| `POST` | `/edges` | Crée un lien entre nœuds | MEMBER+ |
| `DELETE` | `/edges/{edgeId}` | Supprime un lien | MEMBER+ |

---

## 12. Analytics (`/api/workspaces/{slug}/analytics`)

**Contrôleur** : `AnalyticsController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/kpis` | KPIs du workspace | MEMBER+ |
| `GET` | `/throughput` | Débit (`?bucket=DAY\|WEEK`) | MEMBER+ |
| `GET` | `/burndown` | Burndown chart | MEMBER+ |
| `GET` | `/capacity` | Capacité par membre | MEMBER+ |
| `GET` | `/workload` | Charge de travail | MEMBER+ |
| `GET` | `/insights` | Insights IA (Groq) | MEMBER+ |
| `POST` | `/chart` | Génère un graphe depuis une demande en langage naturel | MEMBER+ |
| `POST` | `/breakdown` | Ré-exécute une répartition « X par Y » | MEMBER+ |
| `GET` | `/charts` | Graphes épinglés « Custom » | MEMBER+ |
| `POST` | `/charts` | Épingle un graphe | MEMBER+ |
| `DELETE` | `/charts/{chartId}` | Retire un graphe épinglé | MEMBER+ |

---

## 13. Analyse IA — workflows & décisions (`/api/workspaces/{slug}`)

**Contrôleur** : `AnalysisController` (boucle OODA asynchrone, `@Async` via `AnalysisJobRunner`)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `POST` | `/analysis` | Lance un workflow (`{projectId, depth}`) — retour immédiat, exécution en arrière-plan | MEMBER+ |
| `GET` | `/analysis` | Liste les workflows (dock) | MEMBER+ |
| `GET` | `/analysis/{jobId}` | Détail d'un workflow | MEMBER+ |
| `POST` | `/analysis/{jobId}/answer` | Répond à une clarification du modèle (HITL) → reprend le workflow | MEMBER+ |
| `DELETE` | `/analysis/{jobId}` | Retire le workflow du dock (historique conservé) | MEMBER+ |
| `GET` | `/projects/{projectId}/brief` | Dernier brief persisté (`data: null` si aucune analyse aboutie) | MEMBER+ |
| `POST` | `/priorities/{priorityId}/accept` | Accepte une priorité → crée l'issue liée | MEMBER+ |
| `POST` | `/priorities/{priorityId}/pin` | Épingle une priorité | MEMBER+ |
| `POST` | `/priorities/{priorityId}/dismiss` | Écarte une priorité | MEMBER+ |
| `PUT` | `/priorities/{priorityId}` | Édite une priorité | MEMBER+ |

> Le job publie son plan d'étapes sur `/topic/analysis.{workspaceId}` (STOMP). Remplace l'ancien
> `POST /projects/{projectId}/decision` (synchrone, supprimé le 10/07/2026 avec `DecisionController`).
> Source : `AnalysisController.java:57-169`.

---

## 14. IA — Conversations, Usage & hôte MCP

**Conversations** — `AiConversationController` (`/api/workspaces/{slug}/ai/conversations`)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les conversations IA de l'utilisateur | MEMBER+ |
| `POST` | (base) | Crée une conversation | MEMBER+ |
| `GET` | `/{id}` | Détail + historique d'une conversation | MEMBER+ |
| `DELETE` | `/{id}` | Supprime une conversation | MEMBER+ |

**Usage IA** — `AiUsageController` (`/api/workspaces/{slug}/ai`)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/usage` | Consommation de tokens IA du workspace | MEMBER+ |

**Hôte MCP** — `McpActionController` (`/api/workspaces/{slug}/mcp`) — **Gate BUSINESS+** (`PlanFeature.INTEGRATIONS`, sinon 409)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `POST` | `/actions/execute` | Exécute une action d'outil MCP externe validée (`{toolRef, arguments}`) | MEMBER+ |
| `GET` | `/servers` | Statut des serveurs MCP connectés (joignabilité + outils) | MEMBER+ |
| `POST` | `/servers` | Connecte/reconfigure un serveur MCP (`{connectorKey, mcpUrl, mcpToken?, mcpAllow?}`, chiffré) | ADMIN+ |
| `DELETE` | `/servers/{connectorKey}` | Déconnecte un serveur MCP | ADMIN+ |

> Sources : `AiConversationController.java:50-74`, `AiUsageController.java:32`, `McpActionController.java:56-98`.

---

## 15. Assistant IA (`/api/workspaces/{slug}/assistant`)

**Contrôleur** : `AssistantController` (Groq LLM)

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `POST` | (base) `text/event-stream` | Chat IA en streaming SSE | MEMBER+ |
| `POST` | (base) `application/json` | Chat IA réponse complète (non-streaming) | MEMBER+ |

---

## 16. Intégrations (`/api/workspaces/{slug}/integrations`)

**Contrôleur** : `IntegrationController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/integrations/github/status` | Statut connexion GitHub | MEMBER+ |
| `GET` | `/integrations/github/repos` | Liste des repos | MEMBER+ |
| `GET` | `/integrations/github/issues` | Issues GitHub importées | MEMBER+ |
| `GET` | `/integrations/github/connect` | Initie OAuth GitHub | ADMIN+ |
| `GET` | `/api/integrations/github/callback` | Callback OAuth GitHub | Public |
| `DELETE` | `/integrations/github` | Déconnecte GitHub | ADMIN+ |
| `POST` | `/integrations/github/issues/{issueId}/links` | Lie une issue à GitHub | MEMBER+ |
| `GET` | `/integrations/github/issues/{issueId}/links` | Liens GitHub d'une issue | MEMBER+ |
| `DELETE` | `/integrations/github/links/{linkId}` | Supprime un lien GitHub | MEMBER+ |
| `GET` | `/integrations/slack/status` | Statut connexion Slack | MEMBER+ |
| `GET` | `/integrations/slack/connect` | Initie OAuth Slack | ADMIN+ |
| `GET` | `/api/integrations/slack/callback` | Callback OAuth Slack | Public |
| `DELETE` | `/integrations/slack` | Déconnecte Slack | ADMIN+ |
| `POST` | `/integrations/slack/channels` | Associe un canal Slack | ADMIN+ |
| `GET` | `/integrations/slack/channels` | Canaux Slack associés | MEMBER+ |
| `DELETE` | `/integrations/slack/channels/{channelId}` | Dissocie un canal | ADMIN+ |
| `GET` | `/integrations/catalog` | Catalogue des intégrations disponibles + état | MEMBER+ |
| `POST` | `/integrations/connectors/{key}` | Connecte un connecteur générique (config chiffrée) | ADMIN+ |
| `DELETE` | `/integrations/connectors/{key}` | Déconnecte un connecteur générique | ADMIN+ |
| `GET` | `/integrations/plane/status` | Statut connexion Plane | MEMBER+ |
| `POST` | `/integrations/plane/connect` | Connecte Plane (clé API) | ADMIN+ |
| `GET` | `/integrations/plane/projects` | Projets Plane accessibles | MEMBER+ |
| `POST` | `/integrations/plane/sync` | Ingestion d'un projet Plane dans le Brain OS (`?project=`) | ADMIN+ |
| `DELETE` | `/integrations/plane` | Déconnecte Plane | ADMIN+ |

> `IntegrationController` ne déclare pas de `@RequestMapping` de classe : chaque méthode porte son
> chemin absolu (les URL effectives sont bien celles ci-dessus). Le `connect`/config est **gate
> BUSINESS+** (`PlanFeature.INTEGRATIONS` → 409). Source : `IntegrationController.java:84-345`.

---

## 17. Facturation Stripe

**Contrôleurs** : `StripeController` · `StripeWebhookController` · `BillingController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/stripe/verify-session` | Vérifie session Stripe post-checkout | Public |
| `POST` | `/api/webhooks/stripe` | Reçoit les webhooks Stripe (signature vérifiée) | Public |
| `GET` | `/api/billing/subscription` | Abonnement courant (lecture profil, repli FREE) | JWT |
| `POST` | `/api/billing/checkout` | Session Checkout upgrade in-app (par siège ; BASIC/BUSINESS) | JWT |
| `POST` | `/api/billing/portal` | Ouvre le portail client Stripe (self-service) | JWT (self) |

**Événements webhook gérés** :
- `checkout.session.completed` → finalise l'inscription + crée la subscription
- `customer.subscription.updated` → met à jour `PlanStatus`
- `customer.subscription.deleted` → passe à FREE
- `invoice.payment_succeeded` → renouvellement OK
- `invoice.payment_failed` → notification + downgrade potentiel

---

## 18. Utilisateur, Profil, Compétences, 2FA & compte

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/users/me` | Profil de l'utilisateur connecté | JWT |
| `PATCH` | `/api/users/me` | Modifie le profil (displayName, avatarUrl) | JWT |
| `POST` | `/api/users/me/onboarding` | Clôt l'onboarding (jobTitle + flag) | JWT |
| `POST` | `/api/users/me/avatar` | Upload avatar (multipart) | JWT |
| `POST` | `/api/users/me/password/reset` | Déclenche l'email reset (Keycloak) | JWT |
| `GET` | `/api/users/me/2fa` | Statut 2FA (TOTP) | JWT |
| `POST` | `/api/users/me/2fa/setup` | Démarre l'activation 2FA (secret + otpauth) | JWT |
| `POST` | `/api/users/me/2fa/confirm` | Confirme l'activation avec un code TOTP | JWT |
| `DELETE` | `/api/users/me/2fa` | Désactive le 2FA | JWT |
| `GET` | `/api/users/search` | Recherche d'utilisateurs (autocomplete invite) | JWT |
| `POST` | `/api/users/me/data-request` | Demande RGPD (accès ou suppression) | JWT |
| `POST` | `/api/me/assignments/{issueId}/accept` | Accepte une issue assignée | JWT |
| `POST` | `/api/me/assignments/{issueId}/decline` | Refuse une issue assignée | JWT |
| `GET` | `/api/me/notification-preferences` | Préférences de notification | JWT |
| `PUT` | `/api/me/notification-preferences` | Met à jour les préférences | JWT |
| `GET` | `/api/workspaces/{slug}/profile` | Profil dans le workspace | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/my-issues` | Issues assignées à l'utilisateur | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/my-cycles` | Cycles des projets visibles (agrégé, 1 appel) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/my-pages` | Pages récentes des projets visibles (agrégé, ≤50) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/skills` | Compétences du workspace | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/members/{userId}/skills` | Compétences d'un membre | MEMBER+ |
| `PUT` | `/api/workspaces/{slug}/members/{userId}/skills` | Upsert des compétences (soi-même ou ADMIN+) | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/skills/suggestions` | Suggestion IA de compétences (onboarding) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/members/{userId}/leaves` | Congés d'un membre | ADMIN+ |
| `POST` | `/api/workspaces/{slug}/members/{userId}/leaves` | Déclare un congé | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/members/{userId}/leaves/{leaveId}` | Annule un congé | ADMIN+ |

> Sources : `UserController.java:52-173`, `MyWorkController.java:51-87`, `MemberSkillController.java:41-72`,
> `SkillSuggestionController.java:40`, `AssignmentController.java:32-42`, `NotificationPreferenceController.java:41-54`.

---

## 19. Notifications, RGPD, Autres

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/workspaces/{slug}/notifications` | Notifications de l'utilisateur | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/notifications/unread-count` | Compteur non-lues | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/notifications/{id}/read` | Marque comme lue | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/notifications/{id}/acknowledge` | Acquitte | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/notifications/read-all` | Tout marquer comme lu | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/notifications/acknowledge-all` | Tout acquitter | MEMBER+ |
| `GET` | `/api/gdpr/export` | Export données RGPD (JSON) | JWT |
| `DELETE` | `/api/gdpr/account` | Suppression de compte (droit à l'oubli) | JWT |
| `GET` | `/api/workspaces/{slug}/roadmap` | Issues planifiées (roadmap) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/webhooks` | Webhooks sortants configurés | ADMIN+ |
| `POST` | `/api/workspaces/{slug}/webhooks` | Crée un webhook sortant | ADMIN+ |
| `PUT` | `/api/workspaces/{slug}/webhooks/{webhookId}` | Modifie un webhook | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/webhooks/{webhookId}` | Supprime un webhook | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/dashboard-cards` | Cartes de dashboard épinglées (4 par défaut au 1er accès) | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/dashboard-cards` | Ajoute une carte | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/dashboard-cards/{id}` | Modifie une carte | MEMBER+ |
| `PUT` | `/api/workspaces/{slug}/dashboard-cards/reorder` | Réordonne les cartes | MEMBER+ |
| `DELETE` | `/api/workspaces/{slug}/dashboard-cards/{id}` | Retire une carte | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/issues/{issueId}/attachments` | Ajoute une pièce jointe (multipart) | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/issues/{issueId}/attachments` | Liste les pièces jointes | MEMBER+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/issues/{issueId}/attachments/{attachmentId}` | Supprime une pièce jointe | MEMBER+ |
| `GET` | `/api/files/avatars/{userId}` | Avatar utilisateur (MinIO proxy) | Public |
| `GET` | `/api/files/brain/{workspaceId}/{name}` | Fichier Brain OS (MinIO proxy, clé UUID) | Public |
| `POST` | `/api/workspaces/{slug}/brain/files` | Upload fichier dans Brain OS | MEMBER+ |
| `POST` | `/api/sales/inquiry` | Formulaire de contact (landing) | Public |
| `POST` | `/api/feedback` | Envoi de feedback in-app | JWT |
| `POST` | `/api/logs/client` | Journalisation d'erreurs client | JWT |
| `GET` | `/api/status` | Sonde d'état de l'API | JWT |

> Sources : `WebhookController.java:37-73`, `DashboardCardController.java:44-92`,
> `AttachmentController.java:41-69`, `FileController.java:35-62`, `FeedbackController.java:32`,
> `ClientLogController.java:35`, `StatusController.java:36`.

---

## 20. Récapitulatif — couverture

| Domaine | Contrôleurs | Endpoints (~) | Statut |
|---|:---:|:---:|:---:|
| Auth (dont OAuth externe) | 2 | 12 | ✅ |
| Workspace + Membres + Invitations | 2 | 19 | ✅ |
| Projets + Labels + Équipes + Export | 3 | 30 | ✅ |
| Issues + Statuts + Relations + Checklist + Worklogs | 1 | 37 | ✅ |
| Cycles | 1 | 8 | ✅ |
| Pages wiki | 1 | 5 | ✅ |
| Redistribution | 1 | 2 | ✅ |
| Brain OS | 2 | 11 | ✅ |
| Analytics (dont graphes IA) | 1 | 11 | ✅ |
| Analyse IA (workflows OODA) | 1 | 10 | ✅ |
| Assistant + Conversations + Usage + MCP | 4 | 11 | ✅ |
| Intégrations (GitHub/Slack/Plane/connecteurs) | 1 | 24 | ✅ |
| Facturation Stripe | 3 | 5 + 5 webhooks | ✅ |
| Utilisateur + Profil + Compétences + 2FA | 8 | 26 | ✅ |
| Notifications + Webhooks + Dashboard + Fichiers + Divers | 11 | 27 | ✅ |
| **TOTAL** | **42** | **~235** | ✅ |

> Le récap ne compte plus « Chat » ni « Discussions » : les contrôleurs correspondants
> (`ChannelController`, `ChatWebSocketController`, `DiscussionController`) n'existent pas dans le code.

> 🔗 Voir aussi : [[CdCT_v2]] §4 — [[Auth_Autorisation]] — [[Systeme_Paiement_Stripe]] —
> [[Architecture_C4]] — `API.md` (incohérences front/back documentées)
