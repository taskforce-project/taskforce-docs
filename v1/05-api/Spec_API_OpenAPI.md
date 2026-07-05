---
id: spec-api-openapi
title: Spécification API REST — TaskForce V1
doc_type: api-spec
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [api, rest, openapi, swagger, endpoints, backend, memoire, rncp, soutenance]
---

# 📡 Spécification API REST — TaskForce V1

> Référence des ~130 endpoints des 33 contrôleurs REST du backend Spring Boot.
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
| `/api/auth/**` | Inscription, login, OTP, forgot/reset password |
| `/api/files/brain/**` | Ressources Brain OS publiques |
| `/api/sales/**` | Capture de leads (landing) |
| `/api/stripe/**` | Vérification session Stripe post-checkout |
| `/actuator/**` | Health checks |
| `/swagger-ui/**` + `/v3/api-docs/**` | Documentation Swagger |
| `/ws/**` + `/ws-sockjs/**` | WebSocket STOMP (auth gérée au niveau protocole) |
| `/api/integrations/github/callback` | OAuth callback GitHub |
| `/api/integrations/slack/callback` | OAuth callback Slack |

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
| `POST` | `/api/auth/register` | Étape 1 inscription : données utilisateur + plan sélectionné | Public |
| `POST` | `/api/auth/select-plan` | Met à jour le plan sélectionné avant OTP | Public |
| `POST` | `/api/auth/verify-otp` | Vérifie le code OTP (6 chiffres, TTL 15 min) | Public |
| `POST` | `/api/auth/resend-otp` | Renvoi du code OTP | Public |
| `POST` | `/api/auth/login` | Login (email + password) → tokens Keycloak (RS256) | Public |
| `POST` | `/api/auth/forgot-password` | Envoi email reset password | Public |
| `POST` | `/api/auth/reset-password` | Reset password avec token email | Public |
| `POST` | `/api/auth/refresh-token` | Renouvellement access token via refresh token | Public |
| `POST` | `/api/auth/logout` | Invalidation du refresh token | JWT |

> ⚠️ **Dette technique (PC-004)** : le frontend appelle `/api/auth/refresh` mais le backend
> mappe `/api/auth/refresh-token`. La séquence 401→refresh→retry du client HTTP ne peut pas aboutir.

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
| `POST` | `/api/invitations/{token}/accept` | Accepte une invitation | Public |

---

## 5. Projets (`/api/workspaces/{slug}/projects`)

**Contrôleur** : `ProjectController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/workspaces/{slug}/projects` | Liste les projets | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects` | Crée un projet | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}` | Détail projet | MEMBER+ |
| `PATCH` | `/api/workspaces/{slug}/projects/{projectId}` | Modifie un projet | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}` | Supprime un projet | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/members` | Membres du projet | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/members` | Ajoute un membre | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/members/{userId}` | Retire un membre | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/labels` | Labels du projet | MEMBER+ |
| `POST` | `/api/workspaces/{slug}/projects/{projectId}/labels` | Crée un label | ADMIN+ |
| `PATCH` | `/api/workspaces/{slug}/projects/{projectId}/labels/{labelId}` | Modifie un label | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/projects/{projectId}/labels/{labelId}` | Supprime un label | ADMIN+ |
| `GET` | `/api/workspaces/{slug}/projects/{projectId}/activity` | Activité quotidienne (sparkline) | MEMBER+ |

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

---

## 13. Chat (`/api/workspaces/{slug}/channels`)

**Module** : `modules/chat/` — `ChannelController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les canaux | MEMBER+ |
| `POST` | (base) | Crée un canal | ADMIN+ |
| `GET` | `/{channelId}/messages` | Messages d'un canal | MEMBER+ |
| `POST` | `/{channelId}/messages` | Envoie un message | MEMBER+ |
| `PATCH` | `/{channelId}/messages/{messageId}` | Modifie un message | MEMBER+ |
| `DELETE` | `/{channelId}/messages/{messageId}` | Supprime un message | MEMBER+ |

**Temps réel** : `ChatWebSocketController` — `@MessageMapping` STOMP, topics
`/topic/workspace.{slug}.channel.{id}`.

---

## 14. Discussions (`/api/workspaces/{slug}/discussions`)

**Contrôleur** : `DiscussionController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | (base) | Liste les discussions | MEMBER+ |
| `GET` | `/{discussionId}` | Détail discussion | MEMBER+ |
| `POST` | (base) | Crée une discussion | MEMBER+ |
| `PATCH` | `/{discussionId}` | Modifie une discussion | MEMBER+ |
| `DELETE` | `/{discussionId}` | Supprime une discussion | ADMIN+ |
| `PATCH` | `/{discussionId}/pin` | Épingle / désépingle | ADMIN+ |
| `PATCH` | `/{discussionId}/lock` | Verrouille / déverrouille | ADMIN+ |

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

---

## 17. Facturation Stripe

**Contrôleurs** : `StripeController` · `StripeWebhookController` · `BillingController`

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/stripe/verify-session` | Vérifie session Stripe post-checkout | Public |
| `POST` | `/api/webhooks/stripe` | Reçoit les webhooks Stripe (signature vérifiée) | Public |
| `POST` | `/api/billing/portal` | Ouvre le portail client Stripe (self-service) | OWNER |

**Événements webhook gérés** :
- `checkout.session.completed` → finalise l'inscription + crée la subscription
- `customer.subscription.updated` → met à jour `PlanStatus`
- `customer.subscription.deleted` → passe à FREE
- `invoice.payment_succeeded` → renouvellement OK
- `invoice.payment_failed` → notification + downgrade potentiel

---

## 18. Utilisateur, Profil, Compétences

| Méthode | Chemin | Description | Rôle |
|---|---|---|:---:|
| `GET` | `/api/users/me` | Profil de l'utilisateur connecté | JWT |
| `PATCH` | `/api/users/me` | Modifie le profil | JWT |
| `POST` | `/api/users/me/avatar` | Upload avatar (multipart) | JWT |
| `GET` | `/api/users/search` | Recherche d'utilisateurs (autocomplete invite) | JWT |
| `POST` | `/api/users/me/data-request` | Demande d'export RGPD | JWT |
| `GET` | `/api/workspaces/{slug}/profile` | Profil dans le workspace | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/my-issues` | Issues assignées à l'utilisateur | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/skills` | Compétences du workspace | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/members/{userId}/skills` | Compétences d'un membre | MEMBER+ |
| `GET` | `/api/workspaces/{slug}/members/{userId}/leaves` | Congés d'un membre | ADMIN+ |
| `POST` | `/api/workspaces/{slug}/members/{userId}/leaves` | Déclare un congé | ADMIN+ |
| `DELETE` | `/api/workspaces/{slug}/members/{userId}/leaves/{leaveId}` | Annule un congé | ADMIN+ |

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
| `GET` | `/api/files/avatars/{userId}` | Avatar utilisateur (MinIO proxy) | Public |
| `POST` | `/api/workspaces/{slug}/brain/files` | Upload fichier dans Brain OS | MEMBER+ |
| `POST` | `/api/sales/inquiry` | Formulaire de contact (landing) | Public |

---

## 20. Récapitulatif — couverture

| Domaine | Contrôleurs | Endpoints (~) | Statut |
|---|:---:|:---:|:---:|
| Auth | 1 | 9 | ✅ |
| Workspace + Membres + Invitations | 2 | 17 | ✅ |
| Projets + Labels + Équipes | 2 | 20 | ✅ |
| Issues + Statuts + Relations | 1 | 27 | ✅ |
| Cycles | 1 | 9 | ✅ |
| Pages wiki | 1 | 5 | ✅ |
| Redistribution | 1 | 2 | ✅ |
| Brain OS | 2 | 11 | ✅ |
| Analytics | 1 | 6 | ✅ |
| Chat (canaux + messages) | 2 | 7 + STOMP | ✅ |
| Discussions | 1 | 7 | ✅ |
| Assistant IA | 1 | 2 | ✅ |
| Intégrations GitHub/Slack | 1 | 16 | ✅ |
| Facturation Stripe | 3 | 3 + 5 webhooks | ✅ |
| Utilisateur + Profil + Compétences | 4 | 13 | ✅ |
| Notifications + RGPD + Autres | 5 | 11 | ✅ |
| **TOTAL** | **33** | **~130** | ✅ |

> 🔗 Voir aussi : [[CdCT_v2]] §4 — [[Auth_Autorisation]] — [[Systeme_Paiement_Stripe]] —
> [[Architecture_C4]] — `API.md` (incohérences front/back documentées)
