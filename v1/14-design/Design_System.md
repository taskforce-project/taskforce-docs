---
id: design-system
title: Design system & charte graphique — TaskForce V1
doc_type: design
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [design, ui, ux, tokens, couleurs, typographie, shadcn, radix, tailwind, memoire, rncp, soutenance]
---

# 🎨 Design system & charte graphique — TaskForce V1

> Documentation du système de design de TaskForce : tokens CSS, palette, typographie,
> composants UI et principes visuels.
>
> **Source de vérité** : `frontend/app/globals.css` (tokens CSS), `frontend/components/ui/`
> (composants shadcn/Radix), `tailwind.config.ts`.
>
> **Librairie UI** : [shadcn/ui](https://ui.shadcn.com/) sur Radix UI — primitives accessibles,
> stylisées via Tailwind CSS 4 + variables CSS.

---

## 1. Identité visuelle

### 1.1 Positionnement

TaskForce adopte une esthétique **sobre et professionnelle**, proche de Cloudflare Dashboard
et Linear : fond near-white unifié (sidebar = contenu, pas de rupture visuelle),
typographie claire, icônes mono, accents discrets. Pas de bleu institutionnel — le noir
(`#1d1d1f`) est la couleur primaire.

**Inspiration** : Linear, Cloudflare Dashboard, Apple HIG (système de couleurs SF Pro).

### 1.2 Logo

| Usage | Fichier |
|---|---|
| Logo projet | `assets/images/logo_taskforce.png` |
| Logo établissement | `assets/images/logo_metz_numeric_school.svg` |

---

## 2. Palette de couleurs

Les couleurs sont définies comme **variables CSS** dans `globals.css`, appliquées via
Tailwind (`bg-background`, `text-foreground`, etc.). Support du **dark mode** (`prefers-color-scheme: dark`).

### 2.1 Mode clair (`:root`)

| Token | Valeur | Usage |
|---|---|---|
| `--background` | `#fbfbfc` | Fond de page + sidebar (unifié) |
| `--foreground` | `#1d1d1f` | Texte principal |
| `--primary` | `#1d1d1f` | Noir — boutons primaires |
| `--primary-foreground` | `#ffffff` | Texte sur fond primaire |
| `--secondary` | `#f2f2f4` | Fond secondaire / chips |
| `--secondary-foreground` | `#1d1d1f` | Texte secondaire |
| `--muted` | `#f2f2f4` | Zones atténuées |
| `--muted-foreground` | `#6e6e73` | Texte atténué (placeholders, métadonnées) |
| `--accent` | `#f2f2f4` | Hover states |
| `--border` | `#e6e6e9` | Bordures (gris clair solide) |
| `--input` | `#dededf` | Bordure des inputs |
| `--destructive` | `#d92d20` | Danger (rouge Stripe/shadcn) |
| `--ring` | `rgba(29,29,31,0.28)` | Focus ring |
| `--radius` | `0.375rem` | Border radius (~6px, Cloudflare style) |

### 2.2 Mode sombre (`.dark`)

| Token | Valeur | Usage |
|---|---|---|
| `--background` | `#0b0b0c` | Fond sombre profond |
| `--foreground` | `#f5f5f7` | Texte principal |
| `--primary` | `#ffffff` | Blanc — boutons primaires |
| `--primary-foreground` | `#0b0b0c` | Texte sur fond primaire |
| `--secondary` | `#202022` | Fond secondaire |
| `--border` | `#2a2a2c` | Bordures sombres |
| `--destructive` | `#f04438` | Danger (rouge plus vif sur fond sombre) |

### 2.3 Palette d'accents sémantiques

```css
--accent-green:   #34c759;  /* succès, online, résolu */
--accent-red:     #ff3b30;  /* erreur, bloqué */
--accent-pink:    #ff2d55;  /* urgent, attention */
--accent-purple:  #5856d6;  /* IA, Brain OS */
--accent-orange:  #ff9500;  /* avertissement, en cours */
```

---

## 3. Typographie

### 3.1 Police principale

```css
--font-sans: var(--font-inter), "SF Pro Text", -apple-system, system-ui, sans-serif;
```

**Inter** (chargée via `next/font/google`) comme police primaire, avec fallback vers
SF Pro Text sur macOS et la police système sur les autres plateformes.

### 3.2 Échelle typographique (Tailwind)

| Classe | Taille | Usage |
|---|---|---|
| `text-xs` | 12px | Labels, badges, métadonnées |
| `text-sm` | 14px | Corps de texte, sidebar |
| `text-base` | 16px | Paragraphes, descriptions |
| `text-lg` | 18px | Titres de section |
| `text-xl` | 20px | Titres de page |
| `text-2xl` | 24px | Titres principaux |
| `text-3xl` | 30px | Landing / hero |

---

## 4. Composants UI (shadcn/Radix)

Tous les composants UI sont dans `frontend/components/ui/` — générés par shadcn/ui
et personnalisés avec les tokens CSS du design system.

### 4.1 Primitives de base

| Composant | Fichier | Usage |
|---|---|---|
| `Button` | `button.tsx` | Actions primaires / secondaires / destructives |
| `Input` | `input.tsx` | Champs de formulaire |
| `Label` | `label.tsx` | Labels formulaire |
| `Badge` | `badge.tsx` | Statuts, rôles, labels |
| `Avatar` | `avatar.tsx` | Photo de profil (MinIO proxy) |
| `Separator` | `separator.tsx` | Dividers |
| `Skeleton` | `skeleton.tsx` | Loading states |
| `Spinner` | — | Indicateurs de chargement |

### 4.2 Navigation & Layout

| Composant | Usage |
|---|---|
| `Sidebar` (shadcn) | Navigation principale gauche |
| `Breadcrumb` | Fil d'ariane (workspace > projet > vue) |
| `NavigationMenu` | Menus de navigation |
| `Tabs` | Sous-vues (Issues / Board / Backlog / Cycles) |
| `Sheet` | Panneau coulissant (détail issue) |
| `Dialog` | Modales de création/confirmation |
| `DropdownMenu` | Menus contextuels (3-dots) |
| `Tooltip` | Info-bulles |

### 4.3 Saisie & Formulaire

| Composant | Usage |
|---|---|
| `Select` | Sélecteurs (statut, priorité, assigné, cycle) |
| `Textarea` | Éditeur de commentaires |
| `Checkbox` | Sélection multiple |
| `Switch` | Toggles (notifications, intégrations) |
| `Calendar` / `DatePicker` | Dates d'échéance |
| `Command` | Palette de commandes (Cmd+K) |
| `Popover` | Éditeurs inline (étiquettes, assignataires) |

### 4.4 Données

| Composant | Usage |
|---|---|
| `Table` | Listes paginées (membres, invitations) |
| `Card` | Cartes de projet, plans de prix |
| `Progress` | Progression des cycles |
| `Chart` (recharts) | Analytics (burndown, throughput, capacité) |

### 4.5 Feedback

| Composant | Usage |
|---|---|
| `Toast` (Sonner) | Notifications d'action (succès / erreur) |
| `Alert` | Bandeaux d'information (RGPD, quota) |
| `AlertDialog` | Confirmations destructives |

---

## 5. Icônes

**Librairie** : `lucide-react` — icônes SVG mono, 1px stroke, cohérentes avec Radix.

Exemples d'usage :
- Navigation : `Home`, `Folder`, `GitPullRequest`, `MessageSquare`, `Brain`, `BarChart`
- Issues : `Bug`, `Zap`, `CheckCircle2`, `AlertCircle`
- Actions : `Plus`, `MoreHorizontal`, `Filter`, `ArrowUpDown`, `Trash2`
- Status : `Circle`, `Timer`, `CheckCircle`, `XCircle`

---

## 6. Grille & Espacement

Tailwind CSS 4 avec espacement en multiples de 4px (`rem`) :

| Token | Valeur | Usage |
|---|---|---|
| `gap-1` | 4px | Espacement minimal (chips, badges) |
| `gap-2` | 8px | Espacement interne (icône + label) |
| `gap-4` | 16px | Espacement standard entre éléments |
| `gap-6` | 24px | Sections |
| `p-4` | 16px | Padding standard des cartes |
| `p-6` | 24px | Padding des pages |

**Layout** : `flex` + `grid` via Tailwind. Sidebar fixe à gauche (`w-60` ≈ 240px),
zone de contenu prend le reste.

---

## 7. Responsive & dark mode

**Responsive** : breakpoints Tailwind (`sm:640px`, `md:768px`, `lg:1024px`, `xl:1280px`).
L'application est conçue pour desktop (min 1024px) ; certaines vues sont accessibles mobile.

**Dark mode** : géré via la classe `.dark` sur `<html>` (Next.js `ThemeProvider`).
Tous les tokens CSS ont leur variante dark — aucune couleur hardcodée dans les composants.

---

## 8. Accessibilité

- **Radix UI** : composants accessibles par défaut (ARIA roles, keyboard navigation, focus management).
- **Audit axe-core** via Playwright : `a11y.spec.ts` (WCAG 2.1 AA).
- **Contrastes** : fond `#fbfbfc` / texte `#1d1d1f` → ratio ~19:1 (AAA).
- **Focus visible** : `--ring` défini pour tous les états focus.

> 🔗 [[Accessibilite.md]] — audit complet WCAG 2.1 AA

---

> 🔗 Voir aussi : [[Wireframes_Annotes]] — [[CdCT_v2]] §2 (stack frontend) —
> `frontend/app/globals.css` — `frontend/components/ui/`
