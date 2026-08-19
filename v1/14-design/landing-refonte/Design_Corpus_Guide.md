---
id: design-corpus-guide
title: Guide du corpus d'inspiration — génération de landing avec Claude
doc_type: design
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [design, inspiration, corpus, claude, landing, sources, prompt]
---

# 📚 Guide du corpus d'inspiration

> Comment constituer et utiliser une **bibliothèque de références visuelles** pour faire générer à
> Claude des sections de landing **haut de gamme et cohérentes**. Les captures se déposent dans
> [`inspiration/`](./inspiration/).

---

## 1. Mon avis sur l'approche

**D'accord avec le principe du corpus curé** (l'option « je construis ma propre bibliothèque »).
C'est le bon choix, pour trois raisons :

1. **Cohérence & reproductibilité** — un LLM qui « improvise » son style varie d'une session à
   l'autre. En fournissant toujours les **mêmes références visuelles**, on stabilise le rendu.
2. **Précision** — Claude reproduit bien mieux des *proportions, spacing, hiérarchie typographique,
   rythme d'animation* qu'il **voit** que ceux qu'on décrit en mots.
3. **Réutilisable** — quelques heures d'investissement qui servent sur tous tes projets.

**Nuances / là où je diverge un peu :**

- **Pas besoin de 300 captures pour démarrer.** 300+ c'est le corpus « idéal permanent ». Pour la
  refonte TaskForce, **~60–100 captures bien choisies** (5–8 par section prioritaire) suffisent à
  obtenir un excellent résultat. Vise la **qualité et le classement**, pas le volume.
- **Claude peut chercher lui-même** (WebFetch/WebSearch dispo ici), mais je le déconseille comme
  source primaire : moins reproductible, et les sites premium (Linear/Attio) sont souvent en JS lourd
  → captures partielles. **Utilise Claude pour analyser TES captures**, pas pour les collecter.
- **Priorise par impact** : Hero > Features/Bento > Pricing > CTA > Navbar/Footer. Le Hero décide de
  80 % de la perception. Commence par lui.
- **Attention au droit d'auteur** : ces captures sont un **langage de référence privé** (moodboard
  interne), pas des éléments à copier tels quels. On reproduit le *niveau de qualité*, jamais le
  contenu/les visuels d'un concurrent.

**Verdict** : corpus curé, ~60–100 captures pour commencer, classées par section, avec des notes.
Génération **section par section** en donnant à Claude le dossier + le prompt-type (§4).

---

## 2. Sources recommandées (classées par usage)

### 2.1 Sites SaaS de référence (à capturer directement)

Les « dicteurs de tendance » — capture leur home + pricing + features :

- **Linear** · **Attio** · **Ramp** · **Stripe** · **Vercel** · **Raycast** · **Arc**
- **Supabase** · **Clerk** · **Resend** · **Retool** · **Cursor** · **Notion**
- IA : **OpenAI** · **Perplexity** · **Anthropic**

### 2.2 Galeries d'inspiration (pour piocher par section)

| Site | Fort pour |
|---|---|
| **Land-book** (land-book.com) | Le plus large ; filtres AI / SaaS / Dark / Minimal / Enterprise |
| **Lapa Ninja** (lapa.ninja) | Classé par section (Hero, Pricing, CTA, Footer, Login…) — idéal |
| **SaaS Landing Page** (saaslandingpage.com) | B2B / startup / IA / productivité |
| **One Page Love** (onepagelove.com) | Hero, storytelling, startup |
| **Godly** (godly.website) | Moderne : IA, 3D, gradients, animations |
| **Maxibestof** (maxibestof.one) | SaaS, agences, produits IA |
| **Mobbin** (mobbin.com) | Des milliers de captures de vrais produits (Stripe, Notion, Slack…) |
| **UI Garage** | Recherche par pattern (Pricing, Hero, Dashboard, Tables…) |
| **Awwwards** | Animations/transitions (pour idées, pas pour l'UX) |

### 2.3 Design systems & composants (cohérence + détails)

- **shadcn/ui** (ui.shadcn.com) · **Radix UI** · **Tailwind UI** · **Material 3**
- **Aceternity UI** · **Magic UI** · **Origin UI** — composants animés « landing-ready »
- Animations : **Motion.dev** · **Motion Primitives** · **React Bits** · **21st.dev**
- Icônes : **Lucide** (déjà utilisé) · **Heroicons** · **Phosphor**

> 🎯 **Pour TaskForce** : shadcn/Radix (déjà dans le stack) + magicui/Aceternity pour les effets +
> Lucide pour les icônes = base cohérente avec l'app.

---

## 3. Comment stocker (convention)

Dépose les captures dans le bon dossier de [`inspiration/`](./inspiration/) et **nomme-les** :

```
<section>-<source>-NN.png
```

Exemples : `hero-linear-01.png` · `pricing-ramp-01.png` · `bento-grid-vercel-02.png` ·
`cta-stripe-01.png` · `navbar-attio-01.png`.

Dans chaque dossier, un `notes.md` (déjà créé) : remplis le tableau « ce qui est intéressant »
(spacing, typo, couleur, animation, structure) — **c'est ce qui rend le corpus utile à Claude**.

Cible de départ par dossier prioritaire :

| Dossier | Captures visées |
|---|---|
| `Hero/` | 8–12 |
| `Features/` + `Bento-Grid/` | 8–12 |
| `Pricing/` | 5–8 |
| `CTA/` · `Navbar/` · `Footer/` | 4–6 chacun |
| `Testimonials/` · `Logos/` · `FAQ/` | 3–5 chacun |
| `Full-Pages/` (pages entières de réf.) | 5–10 |
| `Animations/` · `Color-Palette/` · `Typography/` | 3–5 chacun |

---

## 4. Prompt-type pour Claude (génération d'une section)

> À adapter par section. On donne à Claude le **dossier d'inspiration** correspondant + ce cadrage.

```
Rôle : tu es designer/intégrateur front senior.

Références : analyse les captures du dossier `inspiration/Hero/` (+ notes.md). Déduis les patterns
communs — spacing, hiérarchie typographique, proportions, palette, rythme d'animation, structure.
NE COPIE PAS le contenu ni les visuels ; reproduis le NIVEAU DE QUALITÉ.

Contraintes techniques :
- Stack : Astro (island React `client:visible`) + Tailwind + Radix + magicui + Lucide.
- Réutilise les tokens du Design System TaskForce (couleurs/radius/ombres) — cohérence produit↔landing.
- Dark-first, glassmorphism léger, motion parcimonieux, respecte prefers-reduced-motion.
- Accessible (WCAG 2.1 AA), responsive mobile-first, perf (lazy-load des visuels lourds).

Produit : le composant de la section Hero pour TaskForce, avec :
- value prop : « [ta phrase] », sous-titre, double CTA,
- un visuel produit (placeholder pour capture Smart Assign),
- du copywriting orienté bénéfice (pas de jargon).

Livrable : code du composant + où l'insérer dans `index.astro`. Explique tes choix en 3 lignes.
```

**Bonnes pratiques de prompting** :
- Une section à la fois (Hero d'abord), on itère.
- Fournir les tokens **explicitement** (palette hex, échelle typo, spacing) une fois pour toutes.
- Demander à Claude de **justifier** ses choix (spacing/typo) → force la cohérence.
- Refuser le « joli mais générique » : renvoyer vers les références quand ça dévie.

---

## 5. Ordre de production conseillé

1. Remplir `Hero/`, `Features/`, `Bento-Grid/`, `Pricing/` (les 4 prioritaires).
2. Définir les **tokens** (palette + typo + spacing) dans un fichier de réf.
3. Générer **Hero** → intégrer → valider le langage visuel.
4. Décliner les autres sections avec le **même** vocabulaire visuel.
5. Passe finale : SEO (C20), a11y, perf, cohérence, contenu réel (changelog, mentions légales).

---

> 🔗 [Architecture de la refonte](./README.md) · [[Design_System]] · [[Accessibilite]] ·
> [[Roadmap_Backlog]] (TF-LP-*, TF-SEO-001)

**Dernière mise à jour :** 05/07/2026 · **Version :** 1.0
