---
id: sop-developpement
title: SOP — Développement TaskForce
doc_type: sop
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [framework, sop, workflow, brain-os]
related:
  - "../Brain_OS.md"
  - "../v1/04-engineering/Conventions_Documentation.md"
  - "../v1/02-produit/README.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# SOP — Développement TaskForce

**Version :** 1.0 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: SOP](https://img.shields.io/badge/Type-SOP-purple?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides
- [🧠 Brain OS](../Brain_OS.md) · [🚧 État Produit](../v1/02-produit/README.md) · [📐 Conventions](../v1/04-engineering/Conventions_Documentation.md) · [📋 Backlog](../v1/13-roadmap/Roadmap_Backlog.md)

**Tags :** `#sop` `#workflow` `#brain-os`

<p class="lead">
Procédure standard pour toute intervention sur TaskForce (humain ou IA). Objectif : un travail traçable,
sans régression, qui fait avancer le produit vers le niveau des outils de référence (Plane, Linear, GitHub…). C'est la version longue ; la version
condensée vit dans <code>.github/copilot-instructions.md</code> (toujours chargée par Copilot).
</p>

> **Principes :** (1) le **Brain OS est la source de vérité** ; (2) on documente **la réalité du code**,
> pas l'intention ; (3) **priorité au produit** (niveau des outils de référence) avant le mémoire RNCP.

## 1. Avant de coder (LIRE)

1. Ouvrir le [Brain OS](../Brain_OS.md) → tableau de bord santé.
2. Localiser : [Architecture](../v1/03-architecture/Architecture.md) / [API](../v1/05-api/API.md) / [Modules](../v1/03-architecture/Modules.md) pour trouver le code.
3. État & tâche : [État Produit](../v1/02-produit/README.md) (fiche du répertoire concerné) + [Backlog](../v1/13-roadmap/Roadmap_Backlog.md) + [Problèmes connus](../v1/09-audits/Problemes_Connus.md).
4. Vérifier dans le code que l'info est à jour (les notes sont datées).

## 2. Pendant (CODER) — règles d'or

| # | Règle | Pourquoi |
| - | ----- | -------- |
| 1 | **Tout contrôleur backend porte `/api`** dans `@RequestMapping` (pas de context-path) | sinon 404 (PC-001) |
| 2 | Toute route front est déclarée dans `lib/config/api-routes.ts` puis consommée via un service `lib/api/*` | évite PC-002 |
| 3 | Client HTTP : `import { apiClient } from "@/lib/api/client"` (export nommé) | évite PC-003 |
| 4 | Lire les réponses via `response.data.data` (enveloppe `ApiResponse<T>`) | contrat backend |
| 5 | Couches backend `shared ← core ← modules` (jamais l'inverse) | architecture |
| 6 | Tout changement de schéma DB = migration **Flyway** `V{n}__...` (jamais éditer une migration appliquée) | `ddl-auto=validate` |
| 7 | TypeScript **strict**, pas de `any` ; un **store Zustand** par domaine | qualité front |
| 8 | Validation `@Valid` (back) / Zod (front) ; secrets via env, jamais en dur | sécurité |

## 3. Traçabilité & réf. croisée FE↔BE

- Toute tâche provient du [Backlog](../v1/13-roadmap/Roadmap_Backlog.md) (`TF-…`) ou d'une fiche [produit](../v1/02-produit/README.md) (`FE-…`/`BE-…`).
- **Si le front a besoin du back** : ajouter `[besoin-backend:: BE-xxx]` sur l'item dans [produit/Frontend.md](../v1/02-produit/Frontend.md), et créer/mettre à jour l'item `[id:: BE-xxx] [demande-par:: frontend]` dans [produit/Backend.md](../v1/02-produit/Backend.md).
- Citer l'ID dans le code/commit si pertinent.

## 4. Tester & vérifier

- Couverture **≥ 50 %** (front Vitest+RTL, back JUnit/Mockito) — exigence RNCP C18/C25.
- Lancer le linter avant commit (`npm run lint` / `mvn verify`).
- Critère de « fini » : la feature marche **bout-en-bout** (front appelle un endpoint réel, pas un mock).

## 5. Après (METTRE À JOUR)

1. Basculer l'item de la fiche [produit](../v1/02-produit/README.md) en `[statut:: done]` (ou `wip`).
2. Si l'architecture/le contrat change : mettre à jour [Architecture](../v1/03-architecture/Architecture.md) / [API](../v1/05-api/API.md) et le tableau de bord du [Brain OS](../Brain_OS.md).
3. Ajouter une entrée au [changelog](../v1/15-utilisateur/Release_Notes.md) si visible utilisateur.
4. Si une décision structurante : créer un ADR (`_templates/TPL_ADR.md`).

## 6. Git

`type(scope): description` (feat/fix/refactor/docs/test/chore/ci…). Branches depuis `dev`
(`feature/*`, `fix/*`). PR avec **un** label `release:{major|minor|patch}`. Détail :
[git-workflow](../v1/04-engineering/git-workflow/README.md). **Ne jamais commiter/exécuter sans accord de l'utilisateur.**

## 7. Ne jamais faire

- Lancer une commande / commit / push sans confirmation explicite.
- Ré-introduire `context-path`, du `any`, des données mock, des secrets en dur.
- Modifier `application.yml` au lieu de `application-dev.yml` pour la config dev.
- Éditer une migration Flyway déjà appliquée.

---

> **Note Brain OS** — Version condensée dans `.github/copilot-instructions.md`. Mettre à jour les deux si
> le workflow change.

**Dernière mise à jour :** 09/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
