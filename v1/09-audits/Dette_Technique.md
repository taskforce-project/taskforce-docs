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

**DT-001 🔴 — Cinq contrôleurs sans préfixe `/api` → 404.** `CycleController`, `TeamController`,
`PageController`, `DiscussionController`, `ChannelController` mappent `/workspaces/…` sans `/api`. Aucun
`context-path` n'étant configuré (vérifié dans les 3 `application*.yml`), les appels front `/api/workspaces/…`
tombent en 404. Indice trompeur : commentaire `shared/config/CorsConfig.java:65`. Impact : Cycles, Teams,
Pages, Discussions, Chat non fonctionnels bout-en-bout.

**DT-002 🟠 — Constantes de routes front absentes → erreur `undefined`.** `MESSAGE_ROUTES`,
`INTEGRATION_ROUTES`, `ATTACHMENT_ROUTES`, `ROADMAP_ROUTES` importées mais non déclarées dans
`frontend/lib/config/api-routes.ts`. Tout appel lève `Cannot read properties of undefined`. Les endpoints
back des intégrations/pièces jointes/roadmap existent (avec `/api`) ; seules les entrées du registre front
manquent.

**DT-003 🟡 — `profile-service.ts` importe un module inexistant.** `import apiClient from "./api-client";`
→ doit être `import { apiClient } from "./client";`. `getProfile()` échoue au runtime.

**DT-004 🟡 — Désalignement + non-implémentation du refresh auth.** Front poste `/api/auth/refresh` ; back
mappe `/api/auth/refresh-token` et le handler est un TODO. La séquence `401 → refresh → retry` échoue.

## 2. Endpoints stubés / incomplets (backend)

**DT-005 🟠 — Webhooks & écritures Stripe stubés.** Les handlers `customer.subscription.updated/deleted`,
`invoice.payment_succeeded/failed` de `StripeWebhookController` ne font que logger (aucune mutation DB) :
le cycle de vie d'abonnement post-checkout n'est pas reflété. Vérifier aussi que `create-checkout` /
`subscription` / `cancel` sont bien câblés côté `StripeController`.

**DT-006 🟡 — Inquiry Sales sans notification.** `modules/sales/service/SalesService.java` — TODO :
email de confirmation + alerte équipe sales. Les leads sont persistés mais personne n'est prévenu.

**DT-007 🟡 — Refresh-token & logout non implémentés.** `AuthController` — TODO refresh + révocation des
refresh tokens. `JwtService` existe mais la feature est inachevée.

**DT-008 🟡 — Streaming assistant simulé.** `AssistantController` découpe la réponse complète par groupes
de ~5 mots pour *imiter* le SSE au lieu de streamer les tokens Groq (latence = complétion totale).

## 3. Code mort / vestigial / mock

**DT-009 🟡 — Données mock chat résiduelles.** `frontend/components/messages/data.ts` contient des
canaux/messages statiques. Le chat étant cassé (DT-001/002), l'UI affiche probablement ce mock. À retirer
une fois le chat câblé.

**DT-010 🟡 — Service IA Python vestigial.** `ai-service/app/main.py` : embeddings = hash SHA256 16-dim (aucun
modèle), smart-assign = formule pondérée. `TODO.md` : « Remplacé par Groq direct ». Le service, son
Dockerfile et le câblage `AI_SERVICE_URL`/`EMBEDDING_MODEL` sont morts en prod. Garder en legacy ou supprimer.

**DT-011 🟢 — Export `API_ROUTES` agrégé mort.** `api-routes.ts` agrège 5 groupes sur 13+ ; les services
importent les groupes nommés directement. Inutilisé mais trompeur.

**DT-012 🟢 — Clé objet avatar en dur.** `modules/ged/api/FileController.java` construit
`"avatars/" + userId + "/avatar"` inline ; convention non centralisée.

## 4. Features incomplètes (frontend)

**DT-013 🟡 — `team-store` incomplet.** `frontend/lib/store/team-store.ts` n'a pas la parité CRUD des autres
stores. Combiné à DT-001, Teams est non fonctionnel.

**DT-014 🟢 — Command-palette « Create new issue » placeholder.** `frontend/components/command-palette.tsx`
déclenche `toast.info("New issue dialog coming soon")` au lieu d'ouvrir le dialog.

**DT-015 🟢 — Page `[ws]/agents` placeholder.** Route « agents » à l'état de coquille ; runtime assistant
partiellement via adaptateur local (cf. `TODO.md`).

## 5. Dette opérationnelle / config

**DT-016 🟡 — AI Insights sans cache.** `AnalyticsController /insights` régénère via Groq à chaque appel.
Les tables `ai_runs`/`insight_snapshots` (V35) existent mais ne sont pas réutilisées → latence + quota Groq.

**DT-017 🟡 — Pas de garde quota/timeout sur Groq / ai-service.** Résilience manquante (cf. `TODO.md`).

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

---

> **Note Brain OS** — Vue priorisée (priorité · impact · effort · confiance) :
> [Problèmes connus](./Problemes_Connus.md). Vérifié dans le code au 08/06/2026 (branche `feat/dashboard`).

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
