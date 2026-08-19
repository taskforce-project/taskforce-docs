---
id: accessibilite
title: Audit d'accessibilité (RGAA / WCAG 2.1 AA)
doc_type: reference
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [accessibilite, rgaa, wcag, a11y, axe, c13, c15]
---

# Audit d'accessibilité — RGAA / WCAG 2.1 AA

> Compétences **C13 (UI accessible)** / **C15 (UX, accessibilité)** — Bloc 2. Audit **automatisé**
> (axe-core) sur l'app en marche + revue des composants. Base : shadcn/ui sur **Radix UI**
> (accessible par construction : rôles ARIA, navigation clavier, focus management natifs).

## 1. Méthode

- **Outil** : **axe-core 4.11** (moteur des DevTools accessibilité) injecté dans les pages via Playwright,
  jeu de règles **WCAG 2.1 A + AA** (`wcag2a, wcag2aa, wcag21a, wcag21aa`).
- **Script** : `frontend/e2e/a11y.spec.ts` — scanne les pages clés sur la stack réelle, journalise les
  violations par impact (critical / serious / moderate / minor) et échoue sur les **critiques**.
- **Rejouer** : `cd frontend && npm run e2e -- a11y.spec.ts`.

## 2. Résultats (05/07/2026)

| Page | critical | serious | Verdict |
| --- | :--: | :--: | --- |
| `/auth/login` | 0 | 0 | ✅ conforme |
| Dashboard | 0 | 0 | ✅ conforme |
| **Membres** | **26 → 0** (corrigé) | 2 | 🟡 |

- **✅ login & dashboard : aucune violation** — bon signal (Radix/shadcn + bonnes pratiques).
- **🔴→✅ Membres — `button-name` × 26 (critique)** : le **menu d'actions** de chaque ligne membre
  (`DropdownMenuTrigger` → bouton icône `MoreHorizontal` **sans texte**) n'avait pas de nom accessible.
  → **Corrigé** : `aria-label={"Actions pour {nom}"}` ajouté (un lecteur d'écran annonce désormais l'action).
- **🟡 `color-contrast` × 2 (serious)** : 2 éléments sous le ratio minimal (4.5:1). À localiser + ajuster
  (probable texte secondaire `text-muted-foreground` sur fond clair). Non critique.

## 3. Acquis « accessible par construction »

- **Radix UI** (dialogs, dropdowns, selects, tooltips) : focus-trap, `Esc`, rôles ARIA, `aria-*` gérés nativement.
- **Focus visible** conservé (pas de `outline:none` global), **navigation clavier** des dialogs/menus.
- **Formulaires** : `<label htmlFor>` associés (login/register), messages d'erreur liés.
- **Images** : logos avec `alt` ; icônes décoratives non lues.

## 4. Remédiation

**✅ Fait (05/07)** — sweep des menus d'action (bouton `⋯` sans nom) sur les pages V1 :
Membres (×26), Issues, Cycles, Membres projet + **X de fermeture** de l'issue-sheet → `aria-label` ajouté.

**Reste :**
1. **Contraste** : localiser les 2 éléments (via `axe` node targets) + remonter à ≥ 4.5:1.
2. **Sweep résiduel** : `settings` (2), `pages/[pageId]`, `roadmap-gantt` (4), `calendar` (shadcn) —
   mêmes `aria-label`. `messages`/`discussions` = **coming-soon** (différés).
3. **Revue manuelle** : parcours complet au clavier + lecteur d'écran (NVDA/VoiceOver) sur 1 parcours clé.
4. **Écoconception** (C16) : à traiter avec la perf/SEO (landing, C20).
