---
id: landing-refonte
title: Refonte de la landing page — architecture & direction
doc_type: design
statut: en-cours
version: 0.1
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [landing, refonte, design, astro, tailwind, seo, inspiration, corpus]
---

# 🎨 Refonte landing page — architecture & direction artistique

> Cadre de la refonte de la landing (avant la génération des slides de soutenance). Objectif :
> une landing **niveau Linear / Attio / Ramp** — premium, sobre, animée avec parcimonie — sans
> repartir de zéro (on capitalise sur l'existant Astro).
>
> 👉 Le **guide du corpus d'inspiration** (sources, méthode, prompt Claude) est dans
> [Design_Corpus_Guide.md](./Design_Corpus_Guide.md). Les captures se déposent dans
> [`inspiration/`](./inspiration/) (un dossier par section).

## Documents

| Doc | Contenu |
|---|---|
| [[Spec_Master]] | **Ancre** — positionnement, badges d'honnêteté, message-map, règles transverses |
| [[Plan_Refonte_Site]] | **Plan de refonte 24/07/2026** — architecture complète du site (~49 pages), design system, kit de composants, **conformité UE** (RGPD, WCAG 2.2 AA, ePrivacy, LCEN, AI Act), plan de production L0→L9. Référence mesurée : `relevanceai.com`. |
| [[Scenario_Home]] | **Scénario de la home 24/07/2026** — la page devient **un seul run filmé en plan-séquence**. Diagnostic des 9 illustrations, décor partagé, 7 règles de motion, les 5 scènes traitées chacune par 6 questions (message, problème, démonstration, progression, moment « Aha », pourquoi mieux), et l'audit de ce qui est coupé. |
| [[Design_Corpus_Guide]] | Corpus d'inspiration — sources et méthode |

---

## 1. Point de départ (existant, à réutiliser)

La landing actuelle (`landing-page/`) est **déjà bien outillée** — la refonte est une **montée en
gamme**, pas une réécriture :

| Élément | État actuel |
|---|---|
| Framework | **Astro** (SSG → excellent SEO) + **React islands** (`@astrojs/react`) |
| UI | **Radix UI** (accessible) + **magicui** + composants `sections/` |
| Animations | **`@paper-design/shaders-react`** (shaders), magicui |
| Pages | index, pricing, enterprise, security, customers, about, docs, blog, changelog, contact, self-host, accessibility, privacy, terms, sitemap |
| i18n | EN/FR (`constants_en.ts` / `constants_fr.ts`) |
| Composants types | `hero115`, `feature72`, `logos3`, `process1`, `testimonial4` |

> ⚠️ À corriger pendant la refonte : `ChangelogPage.tsx` contient des versions **fictives**
> (v1.9.2→v2.4.0) — les remplacer par l'historique réel (cf. [[Release_Notes]]). *(décision : traité
> pendant la refonte, cf. round V1-hardening.)*

---

## 2. Direction artistique (le « langage visuel » cible)

Inspiration assumée : **Linear · Attio · Ramp · Vercel · Raycast**. Principes :

- **Sobriété premium** : beaucoup d'espace négatif, une seule idée forte par section.
- **Dark-first** (avec light propre), surfaces en **glassmorphism léger**, bordures fines lumineuses.
- **Typographie** : titres très grands, contrastés ; corps discret ; police variable (Inter / Geist).
  Réutiliser les tokens du [Design System](../Design_System.md) de l'app pour la cohérence produit↔landing.
- **Dégradés & lueurs** subtils (pas de saturation criarde) ; accents de marque maîtrisés.
- **Motion parcimonieux** : reveals au scroll, parallaxe légère, hover states soignés. Jamais gratuit,
  toujours au service de la lecture. Respecter `prefers-reduced-motion`.
- **Bento grids** pour présenter les features (tendance Linear/Vercel).
- **Preuve produit** : captures réelles de l'app (Kanban, Smart Assign) plutôt que des mockups vides.

---

## 3. Architecture des pages & sections

### 3.1 Page d'accueil (`index.astro`) — la vitrine

Enchaînement de sections (chacune = un dossier d'inspiration) :

1. **Navbar** — logo, liens (Product, Pricing, Security, Docs), CTA « Get started » + bascule thème.
2. **Hero** — value prop en 1 phrase + sous-titre + CTA double (primaire/secondaire) + visuel produit
   (capture Smart Assign animée). *La section la plus travaillée.*
3. **Logos / social proof** — bandeau « propulsé par / compatible avec » ou clients (si assumable).
4. **Features (Bento grid)** — 4–6 tuiles : Smart Assign IA, temps réel, multi-projets, cycles,
   pages wiki, sécurité. Une tuile « héro » plus grande pour Smart Assign.
5. **Zoom Smart Assign** — section dédiée au différenciateur (les 5 signaux + explication LLM),
   avec animation/illustration.
6. **How it works (process)** — 3 étapes : créer → assigner intelligemment → suivre.
7. **Testimonials / cas d'usage** — citations (ou scénarios si pas de vrais clients).
8. **Pricing (aperçu)** — 3 plans FREE/PRO/ENTERPRISE, lien vers `/pricing`.
9. **Sécurité & conformité** — bandeau confiance (OWASP, RGPD, chiffrement) → lien `/security`.
10. **CTA final** — grande invitation « Start free ».
11. **Footer** — navigation complète, légal, langues, réseaux.

### 3.2 Pages secondaires (montée en gamme, pas refonte totale)

`pricing` · `security` · `enterprise` · `customers` · `docs` · `about` · `contact` · `changelog`
(→ vrai historique) · légal (`privacy`, `terms`, + **mentions légales** à créer, TF-RGPD-005).

### 3.3 Correspondance section ↔ dossier d'inspiration

Chaque section ci-dessus a son dossier dans [`inspiration/`](./inspiration/) : `Navbar/`, `Hero/`,
`Logos/`, `Features/`, `Bento-Grid/`, `Pricing/`, `Testimonials/`, `FAQ/`, `CTA/`, `Footer/`,
`Dashboard-Product/`, `Animations/`, `Cards/`, `Forms/`, `Typography/`, `Color-Palette/`,
`Empty-States/`, `Integrations/`, `Full-Pages/` (pages entières de référence).

---

## 4. Stack & contraintes techniques

- **Garder Astro** (SSG) : les pages restent statiques → SEO/perf maximales (critère **C20**).
  Les sections interactives/animées = **React islands** (`client:visible` / `client:load`).
- **Tailwind** pour toute la couche visuelle ; **Radix** pour l'accessibilité ; **magicui** +
  `@paper-design/shaders-react` pour les effets.
- **Tokens partagés** : réutiliser les variables du [Design System](../Design_System.md) (couleurs,
  radius, ombres) pour l'unité produit↔landing.
- **SEO (C20)** : `<title>`/meta/OG par page, sitemap, robots, `alt`, Lighthouse SEO ≥ 90 à mesurer,
  analytics respectueux RGPD (Plausible/Fathom) — cf. backlog TF-LP-001..005 / TF-SEO-001.
- **Accessibilité** : WCAG 2.1 AA, `prefers-reduced-motion`, contrastes — cf. [Accessibilité](../Accessibilite.md).
- **Perf** : lazy-load des visuels lourds, images WebP/AVIF, budget bundle des islands.

---

## 5. Méthode de travail avec Claude

1. Constituer le **corpus** (captures dans `inspiration/`, cf. [guide](./Design_Corpus_Guide.md)).
2. Définir les **tokens** (palette, typo, spacing) → un fichier de référence pour Claude.
3. Générer **section par section** (Hero d'abord), en fournissant à Claude le dossier d'inspiration
   correspondant + le prompt-type du guide.
4. Intégrer dans Astro, vérifier SEO/a11y/perf, itérer.

---

> 🔗 [[Design_System]] · [[Accessibilite]] · [[Wireframes_Annotes]] · [[Release_Notes]] ·
> [Guide du corpus](./Design_Corpus_Guide.md) · [[Roadmap_Backlog]] (TF-LP-*, TF-SEO-001)

**Dernière mise à jour :** 05/07/2026 · **Version :** 0.1
