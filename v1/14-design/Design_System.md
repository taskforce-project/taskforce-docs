---
id: design-system
title: Design system et charte graphique de TaskForce
doc_type: design
statut: valide
version: 2.0
date: "18/10/2026"
auteur: Pierre MICHEL
tags: [design, ui, ux, tokens, couleurs, typographie, shadcn, radix, tailwind]
related:
  - "./Direction_Artistique_2026.md"
  - "./Accessibilite.md"
---

# Design system et charte graphique de TaskForce

> Documentation du système de design de l'application : jetons CSS, palette, typographie, formes, composants.
>
> **Source de vérité** : `frontend/app/globals.css` (jetons et correspondance Tailwind), `frontend/components/ui/`
> (composants shadcn sur Radix), `frontend/lib/palette.ts` (couleurs d'accent partagées).
>
> **Historique** : la version 1 (Inter, gris froids, primaire noir, rayon 6 px) a été remplacée le 18/10/2026 par la
> [[Direction_Artistique_2026]], celle du portfolio du CEO.

---

## 1. Identité visuelle

Un outil pro, sobre : Geist, gris chauds, un seul bleu d'action (`#2f6bf6`), angles droits, ombres douces et chaudes.
Le thème sombre est bleu nuit, avec les mêmes rôles de couleur.

**Logo** : le monogramme « F » monochrome (`frontend/public/assets/logo/logo_taskforce_tp.png`), noir sur fond clair,
inversé (`dark:invert`) en thème sombre. Pas de logo multicolore (raison : [[Direction_Artistique_2026]] §5).

---

## 2. Couleurs

Les couleurs sont des **variables CSS** dans `globals.css` (`:root` pour le clair, `.dark` pour le sombre), exposées à
Tailwind par `@theme inline` (`bg-background`, `text-ink-green`, `bg-shape-blue`…).

### 2.1 Jetons de base

| Jeton | Clair | Sombre | Rôle |
| ----- | ----- | ------ | ---- |
| `--background` | `#ffffff` | `#0b0e19` | fond de page |
| `--card`, `--popover` | `#ffffff` | `#121627` | surfaces |
| `--sidebar`, `--paper-soft` | `#fbfaf9` | `#0e1221` | barre latérale, papier doux |
| `--foreground` | `#191715` | `#f3f2f0` | texte principal (noir chaud) |
| `--muted-foreground` | `#57534d` | `#a3a8b8` | texte secondaire |
| `--subtle` | `#736e67` | `#8a8fa0` | texte tertiaire |
| `--primary` | `#2f6bf6` | `#2f6bf6` | action principale, focus, case cochée |
| `--primary-hover` | `#1f57e0` | `#4a80ff` | survol du bouton principal |
| `--muted`, `--secondary` | `#f4f3f1` | `#171b2d`, `#1a1f33` | fonds discrets |
| `--accent` / `--accent-foreground` | `#eef3ff` / `#1e4fc4` | `#121d3d` / `#a9c1ff` | survol, sélection |
| `--destructive` / `--destructive-foreground` | `#b8321a` / `#ffffff` | `#ff7a5c` / `#0b0e19` | danger |
| `--border` / `--input` / `--rule` | `#e6e4e0` / `#dcdad5` / `#d9d6d0` | `#242a40` / `#2c3350` / `#2a3149` | traits |
| `--ring` | `#2f6bf6` | `#4a80ff` | anneau de focus |
| `--night` | `#070a16` | `#04060e` | bandeaux et voiles sombres |

### 2.2 Palette d'accent

- **Formes pleines** `--shape-*`, identiques dans les deux thèmes : bleu `#2f6bf6`, rouge `#e14322`, vert `#418b5c`,
  citron `#e2f78c`, jaune `#ffaa0d`, rose `#f99bc3`, ciel `#a9c6ff`.
- **Paires fond teinté et encre lisible** `--tint-*` / `--ink-*`, redéfinies en sombre :

| Famille | Teinte (clair) | Encre (clair) | Teinte (sombre) | Encre (sombre) |
| ------- | -------------- | ------------- | --------------- | -------------- |
| bleu | `#eef3ff` | `#1e4fc4` | `#111d3d` | `#9db8ff` |
| rouge | `#fff0ec` | `#b8321a` | `#33170f` | `#ff9479` |
| vert | `#eef7f1` | `#2d6b45` | `#0f2a1c` | `#7fd39e` |
| citron | `#f7fce3` | `#4b6412` | `#1d2610` | `#cfe985` |
| jaune | `#fff6de` | `#8a5300` | `#2e220a` | `#ffc25a` |
| rose | `#fff1f6` | `#a3336c` | `#321527` | `#ff9ccb` |
| ciel | `#f0f5ff` | `#2a55b0` | `#0d2536` | `#b3c9ff` |

- **Graphiques** `--chart-1` à `--chart-5` : bleu, rouge, vert, jaune, rose (plus clairs en sombre).

### 2.3 Règles d'usage

| Besoin | Règle |
| ------ | ----- |
| Texte ou icône d'état | encre de la famille (`text-ink-green`, `text-ink-yellow`…) ; rouge = `text-destructive` |
| Fond teinté, bordure d'état | `bg-tint-*`, ou la forme avec opacité (`bg-shape-green/10`, `border-shape-yellow/30`) ; bleu = `primary`, rouge = `destructive` |
| Pastille, barre, point | forme pleine (`bg-shape-*`) ; jauge = aplat `bg-primary`, sans dégradé |
| Priorité d'une issue | `PRIORITY_DOT` (`lib/palette.ts`) : urgente rouge, haute jaune, moyenne bleu, basse gris |
| Série (projet sur la feuille de route, membre) | `seriesColor(id)` : `bg-chart-1` à `bg-chart-5` |
| Encre posée sur une forme pleine | `inkOnShape` / `shapeFill` : blanc sur le bleu, bleu nuit sur les autres formes (contraste AA) |
| Couleur d'accent d'un projet ou d'une équipe (stockée) | une classe : `bg-primary` (sans teinte) ou `bg-shape-*` ; l'ancienne palette a été convertie par V93 |
| Couleur d'un statut, type ou libellé (stockée) | un hex libre ; préréglages de la palette (`COLOR_PRESETS`, `components/ui/color-picker.tsx`) |

Aucune classe de la palette Tailwind par défaut (`bg-blue-500`…) ni couleur hexadécimale dans `app/` et
`components/`. Exceptions : logos de marque tiers (connexion Google et GitHub), couleurs stockées en hex et leurs
préréglages, écran d'erreur global (rendu sans la feuille de style de l'app).

---

## 3. Typographie

**Geist** (texte et titres) et **Geist Mono** (code), chargées par `next/font/google` dans `app/layout.tsx`. Leurs
variables (`--font-geist`, `--font-geist-mono`) sont posées sur `<html>` : posées sur `<body>`, `--font-sans` (défini
sur `:root`) ne les voyait pas et retombait sur la police de repli.

| Réglage | Valeur |
| ------- | ------ |
| `font-medium` | 450 (boutons, libellés) |
| `font-semibold` | 550 (titres) |
| `h1`, `h2` | interlettrage -0,025 em |

Échelle Tailwind :

| Classe | Taille | Usage |
| ------ | ------ | ----- |
| `text-xs` | 12 px | libellés, badges, métadonnées |
| `text-sm` | 14 px | corps de texte, barre latérale |
| `text-base` | 16 px | paragraphes, descriptions |
| `text-lg` | 18 px | titres de section |
| `text-xl` | 20 px | titres de page |
| `text-2xl` | 24 px | titres principaux |

---

## 4. Formes, ombres, densité

- **Angles droits** : `--radius: 0` ; toute l'échelle `rounded-xs` à `rounded-4xl` vaut 0. `rounded-full` reste rond
  (avatars, pastilles, interrupteurs, barres de progression).
- **Ombres chaudes** (teinte `#191715`) de `shadow-2xs` à `shadow-2xl`, plus `shadow-window` (panneaux flottants,
  capture du panneau de connexion) et `shadow-key` (liseré bas du bouton principal, effet de touche).
- **Voiles des modales** : `bg-night/50` (`bg-night/60` pour `Dialog`), sans flou.
- **Densité** (passe du 20/09/2026) : hauteurs de contrôle 28 / 32 / 36 px (`--control-height-sm`, `--control-height`,
  `--control-height-lg`), consommées par `h-control`, `size-control` et `h-row`.

---

## 5. Composants (shadcn sur Radix)

Tous dans `frontend/components/ui/`, générés par shadcn/ui et réglés sur les jetons.

| Composant | Réglage de la direction artistique |
| --------- | ---------------------------------- |
| `Button` | `default` : bleu plein, `shadow-key`, survol `primary-hover` ; `outline` : papier doux et bordure ; `destructive` : encre `destructive-foreground` ; `dangerGhost` : texte rouge |
| `Badge` | angles droits, paire teinte et encre (`default` bleu, `destructive` rouge) |
| `Progress` | aplat bleu |
| `WorkspaceAvatar` | tuile pleine de la palette (graine stable), initiales à l'encre lisible, ou logo |
| `ProjectIcon` | tuile teintée par la couleur du projet, glyphe à l'encre lisible ; neutre si `bg-primary` |
| `ColorPalettePicker` | les 8 couleurs d'accent de projet ; la pastille « sans teinte » s'affiche en gris |

Primitives de base : `Button`, `Input`, `Label`, `Badge`, `Avatar`, `Separator`, `Skeleton`. Navigation et mise en
page : `Sidebar`, `Breadcrumb`, `Tabs`, `Sheet`, `Dialog`, `DropdownMenu`, `Tooltip`. Saisie : `Select`, `Textarea`,
`Checkbox`, `Switch`, `Calendar`, `Command` (Ctrl+K), `Popover`. Données : `Table`, `Card`, `Progress`, graphiques
recharts. Retour : `Toast` (Sonner), `Alert`, `AlertDialog`.

---

## 6. Icônes

`lucide-react` : icônes SVG monochromes, trait fin, cohérentes avec Radix.

---

## 7. Grille et espacement

Tailwind CSS 4, espacement par multiples de 4 px (`gap-1` 4 px, `gap-2` 8 px, `gap-4` 16 px, `gap-6` 24 px ; `p-4`
pour les cartes, `p-6` pour les pages). Barre latérale fixe à gauche, contenu sur le reste.

---

## 8. Thème sombre et préférences d'affichage

- **Thème sombre** : classe `.dark` sur `<html>` (next-themes). Chaque jeton a sa valeur sombre.
- **Contraste élevé** (`html.high-contrast`) : surcharge les jetons pour un contraste maximal et force les valeurs
  claires, y compris en thème sombre (libellés, remplissages et paires teinte / encre compris, encres assombries).
- **Mode daltonien** : filtre SVG de correction posé sur `#app-root` (les portails Radix restent hors filtre).

---

## 9. Accessibilité

Contrastes calculés le 18/10/2026 (WCAG 2.1, seuil AA : 4,5:1 pour le texte, 3:1 pour les icônes et le grand texte).

| Paire | Clair | Sombre |
| ----- | ----- | ------ |
| texte principal sur fond | 17,9 | 17,2 |
| texte secondaire (`muted-foreground`) sur fond | 7,6 | 8,1 |
| texte tertiaire (`subtle`) sur fond | 5,1 | 6,0 |
| blanc sur `primary` | 4,6 | 4,6 |
| `destructive` sur fond | 6,0 | 7,5 |
| encres sur leurs teintes | 5,4 à 6,4 | 7,7 à 9,7 |
| bleu nuit sur formes jaune et rose | 10,4 et 9,9 | idem |
| blanc sur formes verte et rouge | 4,1 et 4,2 | idem |

Le blanc sur les formes verte et rouge ne passe que pour les icônes : les initiales des avatars de workspace y sont
donc écrites en bleu nuit. Radix fournit les rôles ARIA, la navigation clavier et la gestion du focus ; l'audit axe-core
tourne dans les tests Playwright (`a11y.spec.ts`).

> Voir aussi : [[Accessibilite]], [[Direction_Artistique_2026]], `frontend/app/globals.css`, `frontend/lib/palette.ts`.
