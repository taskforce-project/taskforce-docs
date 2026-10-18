---
id: direction-artistique-2026
title: Direction artistique 2026 - alignement sur le portfolio
doc_type: design
statut: applique
version: 0.2
date: "18/10/2026"
auteur: Pierre MICHEL
review_cycle: on-change
tags: [design, direction-artistique, tokens, typographie, couleurs, desktop, landing]
related:
  - "./Design_System.md"
  - "../12-decisions/Journal_Decisions_ADR.md"
  - "../13-roadmap/Plan_Release_Open_Source.md"
---

# Direction artistique 2026 : alignement sur le portfolio

**Version :** 0.2 (appliquée à l'application le 18/10/2026, branche `feature/lean-oss`, pas en prod ; site, doc Fern
et README au lot 8)
**Date :** 18/10/2026
**Auteur(s) :** Pierre MICHEL

## 1. Décision

Le CEO veut pour TaskForce la direction artistique de son portfolio
(<https://ai-portfolio-pierre-michel.vercel.app/>). Elle s'applique à l'application (web et desktop, qui partagent le
même front), au site, à la doc Fern et au README. Le [[Design_System]] (v2.0) décrit la charte appliquée.

## 2. Relevé du portfolio (18/10/2026)

Valeurs lues dans les feuilles de style du site en production (variables `:root` et `.dark`).

### 2.1 Typographie

| Rôle | Police | Réglages observés |
| ---- | ------ | ----------------- |
| Titres | Geist | graisse 550, interlettrage serré (environ -0,042 em), un mot clé en bleu |
| Texte | Geist | 18 px, interligne 1,625, couleur `#57534d` |
| Libellés, puces, numéros | Geist Mono | capitales, interlettrage large (« AVAILABLE FROM OCTOBER 2026 », « 01 · EMBED ») |

Geist et Geist Mono sont publiées par Vercel sous licence SIL Open Font License : libres d'usage, y compris
commercial et embarquées dans une app desktop.

### 2.2 Couleurs

| Jeton | Clair | Sombre | Rôle |
| ----- | ----- | ------ | ---- |
| `--background` | `#ffffff` | `#0b0e19` | fond |
| `--foreground` | `#191715` | `#f3f2f0` | texte (noir chaud) |
| `--muted-foreground` | `#57534d` | `#a3a8b8` | texte secondaire |
| `--subtle` | `#736e67` | `#8a8fa0` | texte tertiaire |
| `--primary` | `#2f6bf6` | `#2f6bf6` | action, accent |
| `--primary-hover` | `#1f57e0` | `#4a80ff` | survol |
| `--accent` / `--accent-foreground` | `#eef3ff` / `#1e4fc4` | `#121d3d` / `#a9c1ff` | fond teinté bleu |
| `--muted`, `--secondary` | `#f4f3f1` | `#171b2d`, `#1a1f33` | fonds discrets (gris chaud) |
| `--border` / `--input` / `--rule` | `#e6e4e0` / `#dcdad5` / `#d9d6d0` | `#242a40` / `#2c3350` / `#2a3149` | traits |
| `--sidebar`, `--paper-soft` | `#fbfaf9` | `#0e1221` | barre latérale, papier |
| `--destructive` | `#b8321a` | `#ff7a5c` | danger |
| `--night` | `#070a16` | `#04060e` | bandeaux sombres |

Palette d'appoint, par paires fond teinté et encre lisible (`--tint-*` / `--ink-*`) : bleu, ciel, vert, citron, jaune,
rouge, rose. Formes pleines (`--shape-*`) : bleu `#2f6bf6`, vert `#418b5c`, citron `#e2f78c`, rose `#f99bc3`,
rouge `#e14322`, ciel `#a9c6ff`, jaune `#ffaa0d`. Graphiques (`--chart-1` à `--chart-5`) : bleu, rouge, vert, jaune,
rose.

### 2.3 Formes et matières

- **Angles droits partout** : `--radius: 0`. Seuls les éléments ronds par nature (avatars, pastilles) le restent.
- **Bouton principal** : bleu plein, angles droits, liseré d'ombre interne en bas
  (`inset 0 -2px 0 rgba(0,0,0,.18)`), qui donne un effet de touche.
- **Ombres douces et chaudes** (teinte `#191715`), plus une ombre « fenêtre » pour les panneaux flottants.
- **Illustrations isométriques** sur une grille isométrique fine : bâtiments, chantier, fusée.
- **Logo** : monogramme « PM » en lettres géométriques multicolores.

## 3. Correspondance avec TaskForce

L'application repose déjà sur des jetons shadcn (`frontend/app/globals.css`), les mêmes noms que le portfolio : la
refonte est d'abord un changement de valeurs.

| Aujourd'hui (TaskForce) | Cible |
| ----------------------- | ----- |
| Inter + JetBrains Mono (`app/layout.tsx`) | Geist + Geist Mono |
| Gris froids (`#fbfbfc`, `#1d1d1f`, `#6e6e73`) | Gris chauds du portfolio |
| Bleu `#2563eb` | Bleu `#2f6bf6` |
| `--radius: 0.625rem` (échelle `sm` à `xl` dérivée) | `0`, échelle bornée à 0 (`max(0px, …)`) |
| Couleurs d'état codées en dur | Paires `--tint-*` / `--ink-*` |

Ampleur mesurée le 18/10 dans `app/` et `components/` : 666 classes de couleur Tailwind codées en dur
(`bg-blue-500`, `text-amber-600`…), 127 couleurs hexadécimales dans les composants, et 664 classes `rounded-*`
(dont 149 `rounded-full`, à garder). Les classes `rounded-*` suivent l'échelle dérivée de `--radius` ; les couleurs
codées en dur demandent une passe composant par composant.

## 4. Ce qu'on reprend, ce qu'on ne reprend pas

**Repris** : Geist et Geist Mono, palette chaude et bleu `#2f6bf6`, angles droits, bouton à liseré, libellés en mono
capitales, paires teinte et encre, mode sombre bleu nuit, illustrations isométriques (les mêmes ou dans le même style,
selon leur licence, voir §5).

**Pas repris** : le monogramme multicolore. TaskForce garde son propre logo, recoloré si besoin dans le bleu de marque.
Raison au §5.

## 5. Ressemblance avec Dust : peut-on ?

Constat (visite de <https://dust.tt> le 18/10/2026) : le site de Dust utilise lui aussi Geist et Geist Mono, des titres en
graisse 550 à interlettrage serré, un noir chaud, et un logo fait de formes géométriques multicolores (vert, jaune,
rouge, rose, ciel, bleu). Le portfolio partage ces traits ; il s'en distingue par ses angles droits, son bleu plus
soutenu et ses illustrations isométriques. Dust vend une plateforme d'agents IA pour les équipes, le même terrain que
TaskForce.

Ce que dit le droit français, en général (ceci n'est pas un avis juridique) :

- **Un style n'est pas protégé.** Le droit d'auteur protège une forme précise et originale, pas une idée ni une
  ambiance. Une palette, des angles droits, une police libre ou le genre « illustration isométrique » appartiennent à
  tout le monde.
- **Sont protégés** : les logos (droit d'auteur, et marque s'ils sont déposés), les illustrations, icônes, photos,
  textes et le code d'autrui.
- **Le risque réel vient de la concurrence déloyale et du parasitisme** (article 1240 du Code civil) : reprendre
  l'identité d'un concurrent au point de créer une confusion, ou profiter de ses investissements, peut être sanctionné
  même sans droit d'auteur. Le juge apprécie l'ensemble : même marché, mêmes clients, ressemblances cumulées.

Lecture pour nous :

- **Le portfolio** (site personnel, pas un produit concurrent) : risque faible, d'autant que la mise en page et les
  illustrations sont propres.
- **TaskForce**, sur le même marché que Dust : reprendre la DA du portfolio reste possible, à condition de ne pas
  cumuler les ressemblances. Le point le plus proche de Dust est le **logo en formes multicolores** : on ne le reprend
  pas (§4). On ne reprend pas non plus leurs formules (« multiplayer AI », « human-agent collaboration »).
- **À vérifier** : la licence des illustrations isométriques du portfolio (créées par Pierre, générées, ou issues d'un
  pack sous licence).
- Avant un usage commercial à grande échelle, un avis d'avocat en propriété intellectuelle reste la seule réponse sûre.

## 6. Plan d'application

Ordre proposé, après le lot 3 du [[Plan_Release_Open_Source]] (moins de composants à reprendre une fois les coupes
faites) :

1. Jetons clairs et sombres dans `globals.css`, polices Geist dans `app/layout.tsx`, rayon à 0.
2. Composants de base shadcn (`components/ui/`) : bouton à liseré, champs, badges en paires teinte et encre.
3. Passe sur les couleurs codées en dur (états, priorités, graphiques) vers les jetons.
4. Illustrations des états vides et de l'accueil, logo recoloré.
5. Site (Astro), doc Fern, bannière du README, nouvelles captures.
6. Mise à jour du [[Design_System]].

Critère de fin : aucune couleur hors jetons dans `app/` et `components/`, contraste AA vérifié en clair et en sombre.

## 7. Mise en œuvre (18/10/2026)

Branche `feature/lean-oss`, pas en prod. Étapes 1 à 3 du §6 faites, plus les écrans de connexion :

- `e4af23f1` : jetons clairs et sombres, Geist et Geist Mono, rayon 0, composants de base (bouton à liseré, badge
  teinte et encre, voiles bleu nuit, avatar de workspace en tuile pleine), `lib/palette.ts` ; le contraste élevé
  surcharge aussi les nouveaux jetons ; `hsl(var(--x))` sur des jetons hex corrigés (le navigateur les ignorait).
- `9679cbfe` : couleurs stockées. La couleur d'accent d'un projet ou d'une équipe est une classe Tailwind en base :
  V93 convertit l'ancienne palette (`bg-violet-500` vers `bg-shape-pink`…), sinon les projets perdaient leur
  couleur. Sélecteurs, valeurs par défaut du backend (statuts, types, libellés) et seeds sur la palette.
- `c50100a3` : 563 classes de couleur codées en dur et les hex des composants passés aux jetons, par une règle par
  famille de couleur (voir [[Design_System]] §2.3) ; palettes dupliquées regroupées, palettes mortes retirées.
- `788daa0a` : écrans de connexion. Panneau de marque en papier doux avec filet ; intro de connexion en aplat bleu
  (au lieu de la vague du Lab) ; `labs-wave.jpg` supprimée.

Choix faits en cours de route :

- La palette n'a pas de violet : administrateur et lecteur passent en bleu, « fusionnée » (PR) et mention en rose.
- Priorité moyenne en bleu : la palette n'a qu'un jaune, pris par la priorité haute.
- Initiales sur une forme verte ou rouge en bleu nuit : le blanc y est à 4,1:1, sous le seuil AA du petit texte.
- Logo inchangé : il est monochrome (noir, inversé en sombre), aucune recoloration nécessaire.
- Illustrations isométriques non reprises tant que leur licence n'est pas vérifiée (§5).

Reporté au lot 8 du [[Plan_Release_Open_Source]], qui retouche les mêmes fichiers : site Astro, doc Fern, bannière du
README et captures, dont celle du panneau de connexion (`frontend/public/screens/dashboard.webp`, encore à
l'ancienne charte). Les captures attendent aussi la fin des lots 4 à 7, qui changent encore des écrans.

Critère de fin atteint pour l'application : plus aucune classe de la palette Tailwind par défaut, hex limités aux
exceptions listées dans [[Design_System]] §2.3, contrastes AA calculés ([[Design_System]] §9).
