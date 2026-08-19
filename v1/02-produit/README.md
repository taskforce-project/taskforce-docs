---
id: produit-home
title: État Produit — Suivi & Couverture Fonctionnelle
doc_type: moc
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, parite, plane, backlog]
related:
  - "../../Brain_OS.md"
  - "../13-roadmap/Roadmap_Backlog.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# 🚧 État Produit — Suivi & Couverture Fonctionnelle

**Version :** 1.0  
**Date :** 09/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Cible: Niveau catégorie](https://img.shields.io/badge/Cible-Niveau%20cat%C3%A9gorie-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Fiche Frontend](./Frontend.md) · [Fiche Backend](./Backend.md)
- [Fiche Landing](./Landing.md) · [Fiche IA](./IA.md) · [Fiche Infra](./Infra.md)
- [Backlog technique](../13-roadmap/Roadmap_Backlog.md) · [Problèmes connus](../09-audits/Problemes_Connus.md)

**Tags :** `#produit` `#suivi` `#parite` `#plane`

<p class="lead">
Objectif : amener TaskForce au niveau des <strong>outils de gestion de projet de référence</strong>
(Plane, Linear, GitHub Projects, Jira…) — gérer un projet complet avec tous
les à-côtés — <strong>avant</strong> de finaliser le mémoire. Ce dossier est le système de suivi du
produit : une <strong>fiche par répertoire</strong> (Frontend, Backend, Landing, IA, Infra) qui recense
ce qui est <strong>fait</strong>, <strong>en cours</strong>, <strong>à faire</strong>, avec des
<strong>références croisées FE↔BE</strong> permettant de générer automatiquement les tâches backend dont
le frontend a besoin.
</p>

> **Priorité actuelle : PRODUIT.** Le [mémoire RNCP](../16-memoire-rncp/README.md) reste en attente : on documente
> une fois que les preuves (features finies, tests, déploiement) existent.

## ▶ État & prochaine action

<div class="highlight-box">

**Bloc maintenu par l'agent** (cf. [`AGENTS.md`](../../AGENTS.md) §2-3) — recalculé après chaque tâche.

- **État (05/07/2026) — phase CLÔTURE V1 :** décision 30/06 : **arrêt du dev de features**, focus tests + RGPD + sécu + déploiement (cf. `.ai/roadmap.md` §4). Branche `test/v1-hardening`. **CDC 100 % couvert** : le dernier reste de code (trou #4 « ajustements dynamiques ») est livré via **PROD-1.12 — redistribution proposée/validée** (`RedistributionService`/`Controller`, dialog « Rééquilibrer la charge », validé **e2e** + tests).
- **Tests (C18/C25) ✅ :** **backend 670 tests, 78 % lignes** (≈81 % hors Brain OS) ; **frontend 746 tests, 92 % lignes** (périmètre logique) + **E2E Playwright 4/4** (auth + redistribution) ; JaCoCo + Vitest v8. Priorisation par criticité respectée (sécu/session/JWT/RGPD/paiement ~100 %).
- **Sécurité :** OWASP A01 (IDOR `AuthorizationService`+interceptor), A02 (chiffrement `EncryptedStringConverter`), **A05 en-têtes durcis testés** (`SecurityHeadersWebMvcTest` — CSP/HSTS/X-Frame/nosniff), A07 (JWT/OTP/rate-limit), A09 (audit).
- **RGPD (C11) ✅ cœur :** export portabilité **corrigé** (était 500 → 200, bug QF-5) **et complété** (profil + memberships + skill profiles + worklogs) ; **anonymisation validée** (`GdprServiceIntegrationTest` 3/3). Reste : chiffrement disque (déploiement), registre Art.30, purge Keycloak.
- **Bugs trouvés & corrigés (QA/validation) :** **QF-1** `canManage` toujours faux (page Membres — id number vs string) masquait rôles/invitation/redistribution ; **QF-5** export RGPD 500 ; `JwtServiceTest` ne compilait plus (méthode supprimée). Détail : [Problèmes connus](../09-audits/Problemes_Connus.md).
- **Lot 20/07/2026 (branche `chore/v1-closure`) :** 3 problèmes remontés par l'usage, **tous résolus et vérifiés en live**, et dans les 3 cas **l'hypothèse de départ était fausse** — aperçu des pièces jointes (cause : notre **CSP**, pas MinIO), lignes mortes du Signal Center (liens de notification `NULL` en base → migration `V71`, **265/266** résolues), blocages de rate limiting (les préflights CORS `OPTIONS` consommaient le quota ; `Retry-After` désormais émis **et exposé au JS**). Contrat API : 2 endpoints agrégés `GET …/my-cycles` + `GET …/my-pages` — « Ma file » passe de `3+2N` à **3 appels**. Détail : [PC-031/032/033](../09-audits/Problemes_Connus.md).
- **UI en anglais — EN COURS (décision produit 20/07) :** l'**interface applicative** passe en anglais ; **commentaires de code et documentation restent en français**. Fait : Signal Center, « Ma file », notifications (back + seed). Reste **mesuré** : ~1000 chaînes dans ~110 fichiers front, messages back, catalogue de connecteurs, seed, **prompts LLM**. **Bloqueur identifié** : deux systèmes i18n concurrents (`lib/i18n/index.tsx`, défaut `en` / `lib/store/preferences-store.ts`, défaut `fr`) — le sélecteur de langue des réglages ne pilote que le premier, et ~95 % des fichiers codent leurs chaînes en dur.
- **▶ Prochaine action :** **unifier les deux systèmes i18n** (FE-CORE-015) **avant** de traduire à grande échelle — sinon la contradiction est figée dans ~110 fichiers de plus ; puis **config & hors-app** — PCA/PRA **opérationnel** (cron backup + restauration testée) + **audit sécu/pentest** (OWASP ZAP) → **CI** (gates JaCoCo/Vitest bloquants + scan CVE) → **déploiement** (Guacamole/VM école) → **doc** (conception C1–C12, registre RGPD).
- **Backlog « plus » :** hors chemin V1, cf. `.ai/backlog-post-v1.md` (Brain OS Phases 4/5, niveau Plane, RBAC granulaire, intégrations…).

</div>

## Table des matières

1. [Comment ça marche (réf. croisée FE↔BE)](#1-comment-ça-marche-réf-croisée-febe)
2. [Matrice de couverture fonctionnelle](#2-matrice-de-couverture-fonctionnelle)
3. [Fiches par répertoire](#3-fiches-par-répertoire)
4. [Tableaux de bord (Dataview)](#4-tableaux-de-bord-dataview)

---

## 1. Comment ça marche (réf. croisée FE↔BE)

<p class="lead">
Chaque élément de travail est une case à cocher portant des <strong>champs inline Dataview</strong>. C'est
ce qui rend le suivi requêtable et permet la génération automatique de tâches.
</p>

**Convention d'un item :**

```md
- [ ] Vue calendrier des issues [id:: FE-VIEW-003] [statut:: todo] [parite:: gap] [besoin-backend:: BE-ISSUE-014] [ref:: frontend/app/(protected)/[workspace]/issues]
```

Champs :

| Champ | Valeurs | Rôle |
| ----- | ------- | ---- |
| `id` | `FE-<DOMAINE>-NNN` / `BE-<DOMAINE>-NNN` | identifiant stable, citable depuis le code/commits |
| `statut` | `done` / `wip` / `todo` / `broken` | avancement |
| `parite` | `ok` / `partial` / `gap` / `extra` | vs outils de référence (`extra` = au-delà du standard) |
| `besoin-backend` | `BE-xxx` | **(côté FE)** déclare une dépendance backend → tâche à créer/synchroniser |
| `demande-par` | `frontend` / `landing` / `ia` | **(côté BE)** origine de la demande |
| `prio` | `P0`–`P3` | priorité |
| `ref` | chemin de code | localisation |

**Boucle de génération de tâches :** un item Frontend avec `[besoin-backend:: BE-xxx]` doit avoir un item
correspondant `[id:: BE-xxx]` dans [Backend.md](./Backend.md). La [requête Dataview §4](#4-tableaux-de-bord-dataview)
liste les `besoin-backend` **sans** tâche backend en face → ce sont les tâches backend à créer.
(Un agent/Copilot peut scanner ces champs et ouvrir les tickets correspondants.)

## 2. Matrice de couverture fonctionnelle

> **Plane.so n'est pas un modèle à copier** — c'est une référence parmi d'autres (Linear, GitHub Projects,
> Jira…). On vise le **niveau fonctionnel de la catégorie**, pas un clone. La liste ci-dessous emprunte les
> features de Plane comme **checklist concrète** (elles sont bien documentées et communes au marché).

Légende : ✅ fait · 🔄 en cours · ⬜ à faire · ❌ cassé (P0) · ➕ extra (au-delà du standard).
Sources Plane : [core concepts](https://docs.plane.so/introduction/core-concepts), [work items](https://plane.so/work-items), [modules](https://docs.plane.so/core-concepts/modules).

| Domaine (réf. marché) | TaskForce | État | Action / gap |
| ------------- | --------- | :--: | ------------ |
| Workspaces | ✓ | ✅ | — |
| Projects | ✓ | ✅ | — |
| Work items (CRUD, statuts, types, priorités, labels) | ✓ | ✅ | — |
| Commentaires / activité / relations | ✓ | ✅ | — |
| **Sous-issues** (hiérarchie parent/enfant) | ✓ | 🔄 | relations existent ; hiérarchie parent/enfant à confirmer/ajouter |
| **Estimates** (points/charge) | ✓ | ⬜ | champ estimate + agrégat cycle |
| Cycles (sprints) | ✓ | ❌ | route `/api` cassée → P0 (PC-001), puis burndown |
| **Modules** (regroupement de features) | ✓ | ⬜ | **GAP majeur** — domaine entier à créer (BE+FE) |
| **Views** (vues sauvegardées + filtres) | ✓ | ⬜ | **GAP** — persistance de filtres/tri/affichage |
| Layouts : Liste | ✓ | ✅ | — |
| Layouts : Kanban (board) | ✓ | ✅ | — |
| Layouts : Backlog | — | ➕ | extra TaskForce |
| Layouts : **Calendrier** | ✓ | ⬜ | GAP |
| Layouts : **Tableur (spreadsheet)** | ✓ | ⬜ | GAP |
| Layouts : **Gantt / Timeline** | ✓ | 🔄 | roadmap existe (partielle) → étendre en gantt |
| Pages (wiki) | ✓ | ❌ | route `/api` cassée → P0 |
| **Intake / triage** | ✓ | ⬜ | **GAP** — capture & triage de demandes externes |
| Dashboards / Analytics | ✓ | ✅ | KPIs, burndown, throughput, capacité, AI insights ➕ |
| Notifications / Inbox | ✓ | ✅ | — |
| Membres / rôles | ✓ | ✅ | — |
| REST API | ✓ | ✅ | compléter doc OpenAPI |
| Webhooks | ✓ | 🔄 | back OK ; routes front manquantes (PC-002) |
| Intégrations GitHub / Slack | ✓ | 🔄 | back OK ; routes front manquantes (PC-002) ; GitLab ⬜ |
| **Import / Export** | ✓ | ⬜ | GAP (CSV/JSON, import Jira/Plane) |
| **Templates** (issue/projet) | ✓ | ⬜ | GAP |
| Command palette | ✓ | 🔄 | existe ; « create issue » placeholder (PC-013) |
| Temps réel | ✓ | 🔄 | STOMP OK ; chat cassé (PC-001) |
| **Time tracking** (worklogs) | ✓ | ⬜ | GAP |
| Guests / accès externes | ✓ | ⬜ | rôle GUEST partiel |
| IA (Smart Assign, Assistant, Insights) | (basique) | ➕ | au-delà de Plane |
| Chat / Discussions / Teams | — | ➕❌ | extra TaskForce, mais cassés (P0) |
| Billing (Stripe) | (cloud) | ➕ | extra (webhooks à finir, PC-005) |

**Synthèse :** bases ✅, mais pour « gérer un projet complet » (niveau Plane / Linear / GitHub) il manque surtout
**Modules, Views (+ layouts calendrier/tableur/gantt), Intake, Estimates, Templates, Import/Export**, et
il faut **réparer** Cycles/Pages/Chat/Intégrations (P0).

## 3. Fiches par répertoire

| Fiche | Répertoire | Contenu |
| ----- | ---------- | ------- |
| [Frontend](./Frontend.md) | `frontend/` | UI, stores, services, vues, layouts |
| [Backend](./Backend.md) | `backend/tf-api/` | API, domaines, persistance, IA |
| [Landing](./Landing.md) | `landing-page/` | SEO, contenu, perf *(à créer)* |
| [IA](./IA.md) | `ai-service/` + Groq | Smart Assign, Assistant, Insights *(à créer)* |
| [Infra](./Infra.md) | racine, `docker-*`, `nginx/` | déploiement, CI/CD, observabilité *(à créer)* |

## 4. Tableaux de bord (Dataview)

> Nécessite le plugin **Dataview** (cf. [Conventions](../04-engineering/Conventions_Documentation.md) §7).
> Sur GitHub ces blocs s'affichent en code — c'est normal.

**Toutes les tâches frontend bloquées par le backend :**

````md
```dataview
TASK
FROM "produit"
WHERE !completed AND besoin-backend
GROUP BY besoin-backend
```
````

**Backlog backend demandé par le front (à transformer en tickets) :**

````md
```dataview
TASK
FROM "produit/Backend"
WHERE !completed AND demande-par = "frontend"
SORT prio
```
````

**Gaps fonctionnels restants :**

````md
```dataview
TASK
FROM "produit"
WHERE !completed AND parite = "gap"
SORT prio
```
````

---

> **Note Brain OS** — Registre vivant, revue hebdomadaire. Quand un domaine atteint la parité, basculer
> ses items en `[statut:: done]` et mettre à jour la matrice §2.

**Dernière mise à jour :** 20/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
