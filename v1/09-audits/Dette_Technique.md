---
type: documentation-technique
statut: draft
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [technique, dette-technique, bugs, code-mort, qualité]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Dette Technique

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Source vérifiée: code](https://img.shields.io/badge/Source-code%20v%C3%A9rifi%C3%A9-brightgreen?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Problèmes connus (triage priorisé)](./Problemes_Connus.md)
- [Contrats API](../05-api/API.md)
- [Architecture globale](../03-architecture/Architecture.md)

**Tags :** `#technique` `#dette-technique` `#bugs` `#code-mort`

## Table des matières

1. [Routes cassées (front → back)](#1-routes-cassées-front--back)
2. [Endpoints stubés / incomplets (backend)](#2-endpoints-stubés--incomplets-backend)
3. [Code mort / vestigial / mock](#3-code-mort--vestigial--mock)
4. [Features incomplètes (frontend)](#4-features-incomplètes-frontend)
5. [Dette opérationnelle / config](#5-dette-opérationnelle--config)
6. [Dette de tests & QA](#6-dette-de-tests--qa)

---

<p class="lead">
Inventaire technique exhaustif : bugs, incohérences, code mort, endpoints manquants, routes cassées et
données mock résiduelles. <strong>Constats uniquement — aucun correctif appliqué.</strong> La vue
priorisée et scorée est dans <a href="./Problemes_Connus.md">Problèmes connus</a>.
</p>

Légende sévérité : 🔴 bloquant · 🟠 haute · 🟡 moyenne · 🟢 basse.

## 1. Routes cassées (front → back)

**DT-001 ✅ Résolu — Cinq contrôleurs sans préfixe `/api` → 404.** **→ Corrigé :** les 3 contrôleurs subsistants portent `/api` (`CycleController:33`, `TeamController:33`, `PageController:39`) ; `DiscussionController`/`ChannelController` supprimés (chat retiré) — tous les contrôleurs `core/api` sont préfixés. `CycleController`, `TeamController`,
`PageController`, `DiscussionController`, `ChannelController` mappent `/workspaces/…` sans `/api`. Aucun
`context-path` n'étant configuré (vérifié dans les 3 `application*.yml`), les appels front `/api/workspaces/…`
tombent en 404. Indice trompeur : commentaire `shared/config/CorsConfig.java:65`. Impact : Cycles, Teams,
Pages, Discussions, Chat non fonctionnels bout-en-bout.

**DT-002 ✅ Résolu — Constantes de routes front absentes → erreur `undefined`.** **→ Corrigé :** `INTEGRATION_ROUTES`/`ATTACHMENT_ROUTES`/`ROADMAP_ROUTES` déclarées (`frontend/lib/config/api-routes.ts:375/412/422`) ; `MESSAGE_ROUTES` volontairement absente (chat retiré). `MESSAGE_ROUTES`,
`INTEGRATION_ROUTES`, `ATTACHMENT_ROUTES`, `ROADMAP_ROUTES` importées mais non déclarées dans
`frontend/lib/config/api-routes.ts`. Tout appel lève `Cannot read properties of undefined`. Les endpoints
back des intégrations/pièces jointes/roadmap existent (avec `/api`) ; seules les entrées du registre front
manquent.

**DT-003 ✅ Résolu — `profile-service.ts` importe un module inexistant.** **→ Corrigé :** `frontend/lib/api/profile-service.ts:1` = `import { apiClient } from "./client";`. `import apiClient from "./api-client";`
→ doit être `import { apiClient } from "./client";`. `getProfile()` échoue au runtime.

**DT-004 ✅ Résolu — Désalignement + non-implémentation du refresh auth.** **→ Corrigé :** refresh/logout Keycloak OIDC (`AuthService.refreshToken`) ; durci en cookie HttpOnly `RefreshTokenCookie` (`AuthController:54`, endpoint `/refresh-token` `:281`). Cf. DT-007/DT-025. Front poste `/api/auth/refresh` ; back
mappe `/api/auth/refresh-token` et le handler est un TODO. La séquence `401 → refresh → retry` échoue.

## 2. Endpoints stubés / incomplets (backend)

**DT-005 ✅ Résolu — Webhooks & écritures Stripe stubés.** **→ Corrigé :** `StripeWebhookController:64-70` délègue à `StripeWebhookService` qui mute `Subscription`/`SubscriptionHistory` (handlers idempotents, `StripeWebhookService.java:41-43`). Les handlers `customer.subscription.updated/deleted`,
`invoice.payment_succeeded/failed` de `StripeWebhookController` ne font que logger (aucune mutation DB) :
le cycle de vie d'abonnement post-checkout n'est pas reflété. Vérifier aussi que `create-checkout` /
`subscription` / `cancel` sont bien câblés côté `StripeController`.

**DT-006 ✅ Résolu — Inquiry Sales sans notification.** **→ Corrigé :** `modules/sales/service/SalesService.java:71` appelle `emailService.sendInternalNotification(...)` (champ `:26`). `modules/sales/service/SalesService.java` — TODO :
email de confirmation + alerte équipe sales. Les leads sont persistés mais personne n'est prévenu.

**DT-007 ✅ Résolu (05/07/2026) — Refresh-token & logout.** Migrés sur **Keycloak OIDC natif** (ADR-011) :
`AuthService.refreshToken()` (grant `refresh_token`) et `logout()` (`KeycloakService.logoutUser` → révocation
de toutes les sessions IdP). Le `JwtService` custom a été supprimé.

**DT-008 🟡 — Streaming assistant simulé.** `AssistantController` découpe la réponse complète par groupes
de ~5 mots pour *imiter* le SSE au lieu de streamer les tokens Groq (latence = complétion totale).

## 3. Code mort / vestigial / mock

**DT-009 ✅ Résolu — Données mock chat résiduelles.** **→ Corrigé :** `frontend/components/messages/data.ts` et tout le dossier `components/messages/` supprimés (chat retiré). `frontend/components/messages/data.ts` contient des
canaux/messages statiques. Le chat étant cassé (DT-001/002), l'UI affiche probablement ce mock. À retirer
une fois le chat câblé.

**DT-010 🟢 — Passerelle IA Python = LIVE (constat d'origine périmé).** ⚠️ Le service a été **ravivé**, pas
supprimé : `ai-service/` est aujourd'hui une **passerelle FastAPI active en prod** (routers `chat`/`embeddings`/
`smart_assign`/`health`, `core/vector_math.py`). `docker-compose.prod.yml:158` passe
`AI_SERVICE_URL: http://ai-service:8000` au backend, qui en `depends_on` (`:214`) ; image buildée depuis
`./ai-service` (`:239`). Ce n'est **pas** du code mort. Dette résiduelle = **documenter** le rôle de passerelle
(Ollama/Groq via `config.py`) dans l'architecture ; l'ancien constat « hash SHA256 / formule pondérée / morts
en prod » ne tient plus.

**DT-011 🟢 — Export `API_ROUTES` agrégé mort.** `api-routes.ts` agrège 5 groupes sur 13+ ; les services
importent les groupes nommés directement. Inutilisé mais trompeur.

**DT-012 🟢 — Clé objet avatar en dur.** `modules/ged/api/FileController.java` construit
`"avatars/" + userId + "/avatar"` inline ; convention non centralisée.

## 4. Features incomplètes (frontend)

**DT-013 ✅ Résolu — `team-store` incomplet.** **→ Corrigé :** parité CRUD (`createTeam`/`updateTeam`/`deleteTeam`/`addMember`/`removeMember`) — `frontend/lib/store/team-store.ts` l.21-25, impl. 47-80. `frontend/lib/store/team-store.ts` n'a pas la parité CRUD des autres
stores. Combiné à DT-001, Teams est non fonctionnel.

**DT-014 ✅ Résolu — Command-palette « Create new issue » placeholder.** **→ Corrigé :** `frontend/components/command-palette.tsx:152` — action « Create issue » réelle ; le `toast.info(...coming soon)` a disparu. `frontend/components/command-palette.tsx`
déclenche `toast.info("New issue dialog coming soon")` au lieu d'ouvrir le dialog.

**DT-015 🟢 — Page `[ws]/agents` placeholder.** Route « agents » à l'état de coquille ; runtime assistant
partiellement via adaptateur local (cf. `TODO.md`).

## 5. Dette opérationnelle / config

**DT-016 🟡 — AI Insights sans cache.** `AnalyticsController /insights` régénère via Groq à chaque appel.
Les tables `ai_runs`/`insight_snapshots` (V35) existent mais ne sont pas réutilisées → latence + quota Groq.

**DT-017 ✅ Résolu — Pas de garde quota/timeout sur Groq / ai-service.** **→ Corrigé :** `AiMeter.metered(...)` gate le quota sur les 6 chemins IA (`AiUsageService.assertWithinQuota`, `AiUsageService.java:130`) + timeout côté client passerelle. (Le cache des insights V35 reste NON branché → DT-016 ouvert.) Résilience manquante (cf. `TODO.md`).

**DT-018 🟡 — Pas de feature flags IA.** Toggles souhaités (`enabled`, `smartAssign`, `assistant`,
`insights`) absents ; l'IA n'est gatée que par la présence de `GROQ_API_KEY`.

**DT-019 🟡 — Commentaire `context-path` périmé dans `CorsConfig`.** `CorsConfig.java:65` affirme
`context-path=/api` (non configuré). Cause racine probable de DT-001 ; à corriger (commentaire).

**DT-020 🟢 — Chemin healthcheck actuator possiblement erroné** *(rapporté)*. Le healthcheck dev vise
`/api/actuator/health` alors que sans context-path l'actuator est sur `/actuator/health`. À vérifier.

## 6. Dette de tests & QA

**DT-021 🟠 — QA manuelle en attente (QA.1–QA.6).** Smart Assign, streaming assistant, cohérence Insights,
chat temps réel, CRUD pièces jointes + URLs signées MinIO + scope, upload/affichage avatars.

**DT-022 🟠 — Tests automatisés en attente (T.1–T.6).** Units `SmartAssignService`, pytest `ai-service`,
contrôleurs IA, front SmartAssignPanel/assistant (Vitest+RTL), intégration pgvector/migrations, E2E Playwright.

## 7. Sécurité — durcissement pré-bêta (résolu, QA-49/50/51)

> Audit OWASP Top 10 + revue sécu avant bêta fermée. Toutes vérifiées dans le code **committé** (la note
> « écrit en local, non commité » du journal QA-51 est **périmée** : `SsrfGuard`, `RefreshTokenCookie`, etc.
> sont bien présents dans l'arbre). Vue priorisée : [Problèmes connus](./Problemes_Connus.md) PC-036 → PC-046.

**DT-023 ✅ Résolu (A10 — SSRF sur webhooks sortants).** `WebhookService.fireOne` POSTait vers une URL
utilisateur **sans validation** (réseau Docker/Tailscale/localhost/métadonnées cloud joignable). Fix :
`shared/security/SsrfGuard.java` (rejet des schémas non-http(s) + résolution DNS, blocage loopback/privé/
link-local `169.254`/CGNAT `100.64/10` Tailscale/ULA `fc00::/7`), câblé à `WebhookService.java:52` (create),
`:87` (update) et `:120` (fireOne, défense en profondeur).

**DT-024 ✅ Résolu (A03 — XSS markdown `javascript:`).** `lightweight-markdown.tsx` (chat IA + notes Brain)
rendait `<a href>` sans valider le schéma → `[x](javascript:…)` s'exécutait au clic (React ne neutralise pas
`javascript:`). Fix : `safeLinkUrl` (`components/ui/lightweight-markdown.tsx:62`) / `safeImageUrl` (`:68`),
appliqués aux liens (`:120`) et images (`:91`) → schéma dangereux rendu en texte inerte.

**DT-025 ✅ Résolu (A07 — refresh token en cookie HttpOnly).** Le refresh token partait dans le corps JSON
(vol possible par XSS). Fix : `shared/security/RefreshTokenCookie.java` (HttpOnly, `Path=/api/auth`,
`SameSite=Lax`, `Secure` piloté par profil), câblé `AuthController:54` ; le front ne le stocke plus en
`localStorage`. Cf. DT-004.

**DT-026 ✅ Résolu (H1 — IDOR cross-tenant sur les liens GitHub).** `GitHubIntegrationService.addLink/getLinks/
deleteLink` résolvaient l'issue/lien par ID brut sans scope workspace. Fix : `scopedIssue(slug, issueId)`
(`GitHubIntegrationService.java:197`, 404 hors slug) + `visibilityGuard.assertCanWrite/assertCanView`
(`:209/:231/:246`).

**DT-027 ✅ Résolu (H2 — souscriptions WebSocket cross-tenant).** `StompAuthInterceptor` n'autorisait que
`/topic/notifications.{userId}` ; `projects.{id}`/`analysis.{ws}` n'exigeaient qu'une session authentifiée. Fix :
nouveau `RealtimeAuthorizationService` (`StompAuthInterceptor.java:57,123` → `canSubscribeProject:146` /
`canSubscribeWorkspace:151`).

**DT-028 ✅ Résolu (M3 — sous-lectures d'issue en projet privé).** 6 sous-lectures vérifiaient l'appartenance
workspace mais pas `assertCanView`. Fix : garde ajoutée dans `IssueService.java` — listChildren (`:588`),
checklist (`:650`), listTypes (`:853`), listComments (`:867`), listActivity (`:966`), listRelations (`:986`).

**DT-029 ✅ Résolu (M4 — token capability fichier Brain).** Le proxy public `/api/files/brain/…` utilisait une
clé `UUID.substring(0,8)` = **32 bits** sur un `workspaceId` séquentiel (brute-forçable). Fix : UUID complet
(122 bits), `BrainAttachmentController.java:57`.

**DT-030 ✅ Résolu (M5 — spoofing IP du rate-limit).** `resolveClientIp` faisait confiance à la 1re valeur de
`X-Forwarded-For` (spoofable). Fix : `CF-Connecting-IP` (Cloudflare) → `X-Real-IP` → **dernier** hop XFF →
`remoteAddr`, `RateLimitFilter.java:145`.

**DT-031 ✅ Résolu (M7 — OAuth `email_verified`).** `completeOAuthLogin` liait un compte par e-mail sans
vérifier `email_verified` (prise de contrôle par identité e-mail). Fix : refus si explicitement `false`,
`AuthService.java:674-681`.

**DT-032 ✅ Résolu (L12 — fuite de message d'exception).** `application-prod.yml:55` `include-message: never`
(+ `:52` `include-stacktrace: never`) — les erreurs métier via `ApiResponse.error` restent inchangées.

**DT-033 ✅ Résolu (L8 — oracle d'énumération via l'avatar).** `getAvatar` renvoyait un 404 JSON (utilisateur
inconnu) distinct du 404 vide (pas d'avatar) → oracle. Fix : même 404 vide des deux côtés,
`modules/ged/api/FileController.java:36-51`.

---

> **Note Brain OS** — Vue priorisée (priorité · impact · effort · confiance) :
> [Problèmes connus](./Problemes_Connus.md). Vérifié dans le code au 08/06/2026 (branche `feat/dashboard`).

**Dernière mise à jour :** 28/08/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
