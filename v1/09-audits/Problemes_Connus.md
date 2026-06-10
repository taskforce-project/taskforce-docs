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

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
