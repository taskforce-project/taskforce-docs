---
id: landing-spec-master
title: Spécification maîtresse — Site marketing TaskForce
doc_type: spec
statut: en-cours
version: 0.1
date: "07/07/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [landing, refonte, spec, marketing, conversion, positionnement, ia, sitemap, i18n, seo, a11y, v2]
related:
  - "./README.md"
  - "./Design_Corpus_Guide.md"
  - "../Design_System.md"
  - "../Accessibilite.md"
  - "../../02-produit/Landing.md"
  - "../../13-roadmap/Roadmap_Backlog.md"
  - "../../../v2/README.md"
  - "../../../IDEA.md"
---

# 🧭 Spécification maîtresse — Site marketing TaskForce

[![Type: Spec](https://img.shields.io/badge/Type-Spec%20ma%C3%AEtresse-8b5cf6?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]() [![Cible: Conversion / MRR](https://img.shields.io/badge/Cible-Conversion%20%2F%20MRR-brightgreen?style=for-the-badge)]()

**Tags :** `#landing` `#spec` `#marketing` `#conversion` `#v2`

> **Rôle de ce document.** C'est l'**ancre unique** de la refonte du site marketing : positionnement,
> objectifs de conversion, architecture d'information (sitemap), message-map de la home, et les
> **règles transverses** (i18n, a11y, SEO, légal, status/changelog, analytics, composants).
> Il capitalise sur l'existant (`landing-page/` Astro) et sur le cadrage déjà posé dans
> [README](./README.md) + [Design_Corpus_Guide](./Design_Corpus_Guide.md).
>
> **Repo de dev** : `taskforce-fullstack/landing-page/`, branche **`feat/landing-refonte`** (depuis `feat/dashboard`).
> **Repo de doc** : ici. On spécifie ici, on implémente là-bas.

---

## 1. Décisions cadrées (07/07/2026)

| # | Décision | Choix retenu | Conséquences |
|---|---|---|---|
| D1 | **Positionnement** | **Full v2 — « AI Delivery Operating System »** | Narratif vision-led assumé (l'IA gère le projet, l'humain supervise). Voir [[v2/README]] + [[IDEA]]. |
| D2 | **Thème** | **Light-only** | On retire `ThemeSwitcher` + tokens dark. 1 seul thème clair (registre Attio/Stripe/Ramp/GitBook). |
| D3 | **Langue** | **EN-first** | `constants_en.ts` = source, `constants_fr.ts` = dérivé. SEO EN prioritaire, FR en `hreflang`. |
| D4 | **Périmètre extras** | **Les 4** | (a) Status + Changelog + Roadmap publique · (b) Démos interactives · (c) Trust/Security + suite légale · (d) Self-host / OSS / Developers. |

### 1.1 Garde-fou d'honnêteté (règle d'or du vault)

On **vend la vision v2** (D1) tout en respectant « ne rien affirmer de non démontrable ». Mécanisme :
un **système de badges de maturité** appliqué aux preuves/mentions de features.

| Badge | Sens | Exemples (au 07/07/2026) |
|---|---|---|
| 🟢 **Live** | Démontrable aujourd'hui | Smart Assign (5 signaux + LLM), Kanban/Issues, temps réel, Workspaces/Projets, Analytics |
| 🔵 **Beta** | Fonctionne mais dégradé/partiel | Assistant IA (streaming), AI Insights |
| 🟣 **Bientôt / Early access** | Roadmap crédible, non livré | Pipeline d'orchestration complet, Runs d'agents, intégration IDE, auto-remplissage Brain OS |

> Le **narratif** peut être aspirationnel ; la **preuve visuelle** (captures, démos) reste 🟢 Live.
> Toute promesse 🟣 porte un libellé explicite (« Coming », « Join the waitlist »). Zéro fausse capture.

---

## 2. Positionnement & narratif

### 2.1 Catégorie & pitch

- **Catégorie revendiquée** : *AI Delivery Operating System* (≠ « encore un outil de gestion de projet »).
- **One-liner (hero, EN)** : **« Describe the outcome. TaskForce orchestrates the execution. »** *(déjà en place)*
- **Sous-titre** : *The AI runs the delivery — planning, specs, assignment, agents, QA, ship. You supervise. Your IDE executes.*
- **Phrase de catégorie** : *The orchestration layer between your intent and your codebase.*

### 2.2 Piliers de message (les 6 « raisons de croire »)

1. **Outcome → execution** — un pipeline en checkpoints validés : `Vision → Product → Architecture → DB → API → Implementation → QA → Deploy`. On ne passe à l'étape suivante qu'après validation.
2. **Runs, pas prompts** — chaque étape = une *Run* (façon GitHub Actions) : logs, fichiers modifiés, tests, statut, ETA, en direct.
3. **Orchestrate any agent** — Claude Code, Cursor, Copilot, Windsurf, VS Code. **Model-agnostic = le moat** (indépendant du modèle IA du moment).
4. **Human-in-the-loop** — Approve / Reject / Retry / Edit prompt à chaque checkpoint. Garde-fou n°1.
5. **Brain OS — la doc s'écrit toute seule** — chaque étape enrichit un knowledge graph (1 workspace = 1 brain). À la fin, la doc existe sans l'avoir écrite.
6. **Smart Assign** — le différenciateur **démontrable** : 5 signaux + raisonnement LLM pour assigner la bonne tâche à la bonne personne.

### 2.3 Cible (ICP) & tension

- **ICP primaire** : *engineering leaders / founders techniques / équipes produit* qui livrent du logiciel avec de l'IA et veulent **standardiser la livraison**, pas juste « chatter avec un agent ».
- **Douleur** : les agents IA codent, mais **personne ne standardise comment une IA doit livrer un projet** (étapes oubliées, pas de mémoire, pas de supervision).
- **Promesse d'outcome** : *ship software predictably with AI — without losing control or context.*
- **Anti-positionnement** : pas « un IDE IA », pas « un meilleur agent ». **L'IDE exécute, TaskForce orchestre.**

### 2.4 Ton & style rédactionnel

Sobre, sûr, orienté bénéfice. Phrases courtes. Verbes d'action. Zéro jargon gratuit. Registre Linear/Attio :
« calme premium ». Toujours **outcome-first** (ce que l'utilisateur obtient), la feature vient après.

---

## 3. Objectifs & conversion

### 3.1 Objectif business

Générer du **MRR** : maximiser `visite → sign-up (self-serve)` et `visite → lead sales (enterprise)`.

### 3.2 Hiérarchie des CTA

| Priorité | CTA | Cible | Emplacements |
|---|---|---|---|
| Primaire | **Get started free** | self-serve | Nav, Hero, CTA final, sticky mobile |
| Secondaire | **Talk to sales** / **Book a demo** | enterprise | Nav (discret), Hero (secondaire), Enterprise, Pricing |
| Tertiaire | **Read the docs** / **View on GitHub** | technique/OSS | Developers, Footer |

### 3.3 KPIs à instrumenter

Taux de sign-up, clics CTA hero, scroll-depth par section, démo interactive engagée, vues `/pricing`,
soumissions `/contact` (sales), CTR docs/github. Cf. §7.6 (analytics privacy-first).

---

## 4. Architecture d'information (sitemap)

### 4.1 Arborescence cible

```
/ (Home)
├─ Product
│  ├─ /product/orchestration      🟣  (le pipeline Vision→Deploy, Runs)
│  ├─ /product/smart-assign       🟢  (différenciateur démontrable + démo)
│  ├─ /product/brain-os           🔵  (knowledge graph, doc auto)
│  ├─ /integrations               🟢/🟣 (agents + outils, logos SVGL)
│  ├─ /security                   (trust)
│  ├─ /mobile                     (responsive)
│  └─ /changelog                  (versionné + RSS)
├─ Solutions (option v0.2)
│  ├─ /solutions/founders  ├─ /solutions/engineering-teams  └─ /solutions/agencies
├─ Developers
│  ├─ /docs   ├─ /docs/api   ├─ /self-host   └─ /open-source
├─ /pricing
├─ Company
│  ├─ /about   ├─ /customers   ├─ /blog   └─ /contact
├─ /roadmap                       (publique — extra a)
├─ /status                        (uptime + incidents — extra a)
└─ Legal & Trust
   ├─ /trust (security/compliance center)  ├─ /privacy  ├─ /terms
   ├─ /cookies  ├─ /legal (mentions légales)  ├─ /dpa  ├─ /subprocessors
   └─ /accessibility (déclaration)
Utilitaires : /sitemap · /404 · robots.txt · sitemap.xml · rss.xml
i18n : miroir EN (racine) + FR (`/fr/...`), hreflang réciproque.
```

> **Existant** : la plupart des pages existent déjà (index, pricing, security, enterprise, customers,
> docs, blog, changelog, contact, self-host, accessibility, privacy, terms, sitemap). **À créer** :
> `/roadmap`, `/status`, `/trust`, `/cookies`, `/legal` (mentions légales, TF-RGPD-005), `/dpa`,
> `/subprocessors`, pages Product détaillées (orchestration, smart-assign, brain-os), `/open-source`, `/docs/api`.

### 4.2 Navigation (mega-menu)

`Logo` · **Product ▾** (Orchestration, Smart Assign, Brain OS, Integrations, Security, Changelog) ·
**Developers ▾** (Docs, API, Self-host, Open source) · **Pricing** · **Company ▾** (About, Customers, Blog, Contact) ·
→ droite : `Sign in` (ghost) · **Get started** (primaire) · sélecteur langue. **Light-only, pas de toggle thème.**

### 4.3 Footer

Colonnes : **Product** · **Developers** · **Company** · **Resources** (Docs, Changelog, Roadmap, Status, Blog) ·
**Legal & Trust** (Trust center, Privacy, Terms, Cookies, Mentions légales, DPA, Subprocessors, Accessibility).
Bas de footer : langue, réseaux, **badge Status live**, copyright.

---

## 5. Home — message-map section par section

> Base = ordre **validé PROD-9** (`App.tsx`), enrichi du narratif v2 (D1) et light-only (D2).
> Chaque section = un dossier de [`inspiration/`](./inspiration/) à remplir (corpus).

| # | Section (composant) | Objectif | Message clé (EN) | Preuve / visuel | CTA | Motion |
|---|---|---|---|---|---|---|
| 1 | **Hero** (`hero115`) | Catégorie + aspiration en 3 s | *Describe the outcome. TaskForce orchestrates the execution.* | Capture produit 🟢 (Smart Assign / Run) — **remplacer le placeholder cloudfront** | Get started · Talk to sales | reveal léger, shader subtil |
| 2 | **Logos** (`logos3`) | Crédibilité **honnête** | *Works with your stack* (≠ faux clients) | Logos **SVGL** : Claude, Cursor, VS Code, GitHub, Slack, Linear… | — | marquee lent |
| 3 | **Orchestration** (`OrchestrationPipeline`) | Expliquer la catégorie | *From intent to shipped — validated at every step.* 🟣 | Pipeline Vision→Deploy + Run (logs/tests/ETA) | See how it works | step-reveal au scroll |
| 4 | **Smart Assign / AI** (`AISection`) | Différenciateur démontrable | *The right task, to the right person — reasoned, not random.* 🟢 | **Démo interactive** (5 signaux → suggestion) | Try it | interaction directe |
| 5 | **Core capabilities** (`CoreCapabilities`) | Substance / ça existe | *A complete delivery workspace.* 🟢 | Bento : Projets, Issues, Cycles, Temps réel, Analytics, Pages | — | hover states soignés |
| 6 | **Features** (`feature72`) | Largeur fonctionnelle | *Everything teams need to ship.* | Grille features secondaires | — | reveal |
| 7 | **Integrations** (`Integrations`) | Moat model-agnostic | *Orchestrate any agent. Connect any tool.* | Logos agents/outils (SVGL) + map | Browse integrations | dotted-map / cobe |
| 8 | **Mobile** (`Mobile`) | Accessible partout | *Supervise from anywhere.* | Mockup iPhone (`iphone.tsx`) | — | parallax léger |
| 9 | **Developers** (`Developers`) | Confiance technique | *Built for engineers. Self-host, API, open source.* 🟣/🟢 | Snippet code + terminal | Read the docs · GitHub | typing/terminal |
| 10 | **Enterprise** (`Enterprise`) | Montée en gamme | *Security and control for teams that scale.* | SSO, RBAC, multi-tenant, audit | Talk to sales | — |
| 11 | **Migration** (`Migration`) | Réduire le coût de switch | *Bring your projects from Jira, Linear, Plane.* | Import illustré | — | — |
| 12 | **Self-host** (`SelfHosted`) | Souveraineté / OSS | *Own your data. Run it yourself.* | Docker/terminal | Self-host guide | — |
| 13 | **Testimonials** (`testimonial4`) | Preuve sociale | citations **réelles** ou scénarios balisés « scenario » | avatars | — | colonnes défilantes |
| 14 | **CTA final** (`Cta`) | Conversion | *Start shipping with AI — free.* | fond gradient maîtrisé | Get started free | glow |
| 15 | **Footer** | Nav + confiance | cf. §4.3 | badge status live | — | — |

---

## 6. Design language (résumé — doc dédié à venir)

> Détail complet → `Design_Language_Landing.md` (à créer). Ici : les invariants.

### 6.0 Métriques de référence (relevées au DOM sur linear.app & attio.com, 07/07/2026)

| Élément | Linear (dark) | Attio (light) | **TaskForce (retenu, light)** |
|---|---|---|---|
| Fonte | **Inter Variable** | Inter | **Inter Variable** (Google Fonts, à self-hoster en passe perf) |
| H1 | 64px · **510** · −0.022em · **lh 1.0** · gauche | 64px · 600 · −0.02em · lh 1.0 · centré | **64px · 510 · −0.022em · lh 1.0 · gauche** (2 lignes) |
| H2 sections | 48px · 510 · −0.022em · lh 1.0 | — | idem Linear |
| Sub hero | **15px** · 400 · #8a8f98 · lh 24px | — | 15px · 400 · muted |
| Bouton primaire | h-32 · pill · 13px/510 · micro-ombres | **h-36 · r-10 · 14px/500** · near-black | h-36 (h-9) · r-10 · 14px/500 (nav : h-32 pill) |
| Nav | fixe · blur(20px) · hairline 0.8px @8% | 15px/500 | fixe · blur · hairline `black/[0.06]` · liens 14px/500 |
| Sections | **py-128px** | — | py-128 (rythme) |
| Pattern hero | sub gauche + lien « New … → » droite ; **pas de gros CTA** ; fenêtre produit y≈527, ultra-dense | tabs produit au-dessus de la fenêtre ; CTA double centré | sub+lien Linear ; **CTA double conservé** (objectif MRR) ; tabs intégrés à la toolbar de la fenêtre |
| Détails | H2 gauche + paragraphe droite (2 col) ; hairlines partout ; densité app réelle (13px/11px) | dashed guides | hairlines + densité 13px/11px dans le mock |

**Règle motion (apprise en vérif)** : entrées de page en **CSS pur** (`.anim-rise`, délais échelonnés) → premier
paint sans JS (LCP/SEO, robuste au throttling rAF des onglets cachés) ; framer-motion **réservé à
l'interactif** (tabs layoutId, feed AnimatePresence, compteurs) ; simulations pausées sur `document.hidden`.

- **Light-only** dérivé du [[Design_System]] app : base `#fbfbfc`/blanc pur en alternance de sections,
  texte `#1d1d1f`, accents sémantiques (violet `#5856d6` = IA/Brain OS). Radius ~6 px. **Aucune couleur hardcodée.**
- **Typo** : Inter/Geist variable. Titres très grands et contrastés, corps discret. Échelle landing plus
  ample que l'app (hero jusqu'à `text-6xl`+).
- **Grille** : max-width contenu ~1200–1280 px, sections respirantes (beaucoup de blanc), bento pour features.
- **Motion parcimonieux** : reveals au scroll, parallaxe légère, hover soignés. `@paper-design/shaders-react`
  en accent, jamais gratuit. **`prefers-reduced-motion` obligatoire** partout.
- **Preuve produit réelle** (captures app) plutôt que mockups vides. Glassmorphism **léger**, gradients **subtils**.
- **Composants** : shadcn/Radix (a11y) + magicui + `sections/`. Élargir librement (Aceternity, React Bits,
  21st.dev, Origin UI) — cf. §7.7.

---

## 7. Règles transverses (rulings + pointeurs)

### 7.1 i18n — EN-first (D3)
- **Source** = `constants_en.ts` ; `constants_fr.ts` = traduction dérivée. Le contenu actuel (task-manager)
  est **obsolète** → réécriture v2 (cf. §8).
- **SEO** : un toggle client-side (`LanguageContext`) **ne suffit pas** pour l'indexation. Cible = **routes
  localisées prérendues** (Astro i18n : EN à la racine, FR sous `/fr/`) + `hreflang` réciproques + `lang` correct.
  → *décision : migrer de « context-only » vers routes i18n statiques* [id:: LP-I18N-002] [statut:: todo] [prio:: P2].

### 7.2 Accessibilité — WCAG 2.1 AA
- Conserver l'acquis (contexte a11y, `AccessibilityDropdown`, police **OpenDyslexic**, `accessibility.css`).
- `prefers-reduced-motion` sur **toutes** les animations/shaders ; focus-visible ; skip-link ; nav clavier ;
  contraste AA (attention au **texte en gradient** — garantir un fallback lisible). Cf. [[Accessibilite]].
- Page **/accessibility** = déclaration de conformité (extra c).

### 7.3 SEO & performance
- Par page : `<title>` unique, meta description, canonical, **OG + Twitter cards**, **JSON-LD**
  (`Organization`, `SoftwareApplication`, `BreadcrumbList`, `FAQPage` si FAQ).
- `sitemap.xml`, `robots.txt`, `rss.xml` (changelog/blog). Images **AVIF/WebP**, `alt` partout, `loading=lazy`.
- **Budget** : îlots React en `client:visible`/`client:idle`, subset des fonts. Cibles Lighthouse :
  **SEO ≥ 95, Perf ≥ 90, A11y ≥ 95, Best-practices ≥ 95** (C20). Cf. backlog TF-LP-001/002, TF-SEO-001.
- ⚠️ **Constat (07/07)** : `index.astro` monte tout via `<App client:only="react">` → **zéro HTML rendu côté serveur** (le crawler voit une page vide, JS requis). Ça **annule l'atout SSG** d'Astro et plombe SEO/perf. **Refonte du rendu** = sections statiques en `.astro` + îlots React ciblés (`client:visible`) uniquement là où il y a de l'interaction. [id:: LP-SSR-001] [statut:: todo] [prio:: P1]

### 7.4 Légal & RGPD (extra c)
- Suite : `/privacy`, `/terms`, `/cookies`, **`/legal` (mentions légales — TF-RGPD-005, à créer)**,
  `/dpa`, `/subprocessors`, `/accessibility`. Regroupées sous un **Trust center** (`/trust`).
- Remplacer tout contenu légal placeholder par du réel (juridiction, éditeur, hébergeur, contact DPO).

### 7.5 Status · Changelog · Versioning (extra a)
- **/status** : uptime + historique d'incidents (statique/edge au départ ; provider plus tard).
- **/changelog** : **brancher sur le vrai historique** ([[Release_Notes]]) + flux **RSS**. ⚠️ `ChangelogPage.tsx`
  contient aujourd'hui des versions **fictives** (v1.9→v2.4) → à corriger [id:: LP-CHG-001] [statut:: todo] [prio:: P1].
- **VersionSelector** (header) : données **fictives** (v0.7→v1.0). Décision : **le brancher sur les vraies
  versions** (versioning par service déjà en place) **ou le retirer** s'il crée de la confusion sur une landing.
- **/roadmap** publique : dérivée de la roadmap (balisée 🟢/🔵/🟣).

### 7.6 Analytics — privacy-first
- **Plausible/Fathom** (cookieless si possible → pas de bandeau consentement). Sinon consentement conforme.
  Événements : CTA hero, sign-up, démo engagée, vues pricing, contact sales. Cf. TF-LP-003.

### 7.7 Composants & assets
- **Logos** : **SVGL** (`svgl.app`) — récupérer les SVG (API/CDN), stocker dans `landing-page/public/logos/`,
  usage dans Integrations/Logos/Footer. Tech ciblées : Claude, Cursor, VS Code, GitHub, Slack, Linear, Docker, Vercel…
- **Librairies** : shadcn/Radix (base) + magicui + **Aceternity** + **React Bits** + **21st.dev** + **Origin UI**
  autorisées pour les effets « landing-ready ». Icônes **Lucide**. Mockups : `safari.tsx` / `iphone.tsx` présents.
- **Corpus d'inspiration** : 8 sites de référence (Attio, Linear, Raycast, Render, GitBook, Twingate, Wope,
  Evervault) → teardown dans [`inspiration/*/notes.md`](./inspiration/) (cf. §9, étape 3).

---

## 8. Dette de contenu à corriger (repérée dans le code)

| Élément | Problème | Action |
|---|---|---|
| `constants_fr.ts` / `constants_en.ts` | Copy **v1 task-manager** (« Gérez vos tâches ») incohérente avec le Hero v2 | Réécriture EN-first sur le narratif §2 [id:: LP-CNT-002] [statut:: todo] [prio:: P1] |
| `ChangelogPage.tsx` | Versions **fictives** | Brancher [[Release_Notes]] réel + RSS (LP-CHG-001) |
| `VersionSelector.tsx` | Versions **fictives** | Vraies versions ou retrait |
| `Hero.tsx` | Image **placeholder** (cloudfront shadcnblocks) | Capture produit réelle 🟢 |
| `ThemeSwitcher` / tokens dark | Contredit **light-only** (D2) | Retirer le toggle + les tokens dark de la landing |
| Sections `feature72`/`testimonial4`/`logos3` | Placeholders shadcnblocks | Contenu réel + langage visuel Nodus |

---

## 9. Plan de production (step by step)

1. 🟢 **Fait** — Branche `feat/landing-refonte` (depuis `feat/dashboard`).
2. 🟢 **Fait** — Cette spec maîtresse `Spec_Master.md` v0.1.
3. ⬜ **Corpus des 8 inspis** — teardown structuré (archi, sections, design, motion, copy) → remplir
   `inspiration/*/notes.md`. Pondéré **light** (Attio/Stripe/GitBook/Render en tête, D2). [id:: LP-CORPUS-001]
4. ⬜ **Design_Language_Landing.md** — tokens light-only, échelle typo, grille, motion, glass/gradient. [id:: LP-DL-001]
5. ⬜ **Copy v2 EN-first** — réécrire `constants_en.ts` (puis FR) sur le narratif §2. [id:: LP-CNT-002]
6. 🟡 **En cours** — Above-fold ✅ **v3** (07/07). `SiteHeader` avec **vrai logo** (`public/logo_taskforce_tp.png`) + nav fixe hairline + **mega-menus** (Product / Developers / Company en dropdowns accessibles : hover + clic + Escape + click-outside) — îlot `client:load` ; liens à **dupliquer au Footer** pour le SEO. Reste : menu mobile (hamburger). Hero sur **métriques Linear** (§6.0 : Inter Variable, H1 64/510/−0.022em/gauche). **Mock produit = écran browser vide** (fenêtre + URL `app.taskforce.dev`, placeholder « Product screenshot », ratio 16:9) — **décision utilisateur** : les vraies captures de l'app seront déposées plus tard dans `public/` (voir le `<img>` commenté dans `Hero.tsx`). Le mock DOM board+agent (pourtant fidèle au thème réel Cloudflare-flat, cf. `frontend/app/globals.css`) a été retiré au profit du placeholder. Entrées CSS-first. Vérifié (16:9, 0 overflow, 0 erreur console). **Réf. pour les futures captures** : app réelle = Cloudflare-flat #fbfbfc/#1d1d1f/violet #5856d6, PAS les maquettes navy « TaskFlow AI » périmées. Fondation light-only (retrait `.dark`, SEO home v2, retrait fausse note ★4.8). ⚠️ **Prérequis avant d'industrialiser** : rendu SSR (LP-SSR-001) — le pattern CSS-first du Hero est le modèle ; `App.tsx` doit adopter `SiteHeader` et sortir du `client:only`.
7. ⬜ **Pages Product détaillées** + pages extras (roadmap, status, trust, légal complet).
8. ⬜ **Sous-docs transverses** (i18n routes, SEO, légal, status) au fil de l'implémentation.
9. ⬜ **Passe finale** — SEO/a11y/perf (Lighthouse), contenu réel, reconciliation des docs
   (`README` dark-first→light-only ; fiche [[Landing]]).

> Réconciliation : ce document **prime** sur les mentions « dark-first » de [README](./README.md)
> (à mettre à jour) tant que D2 = light-only.

---

> 🔗 [[README]] (direction) · [[Design_Corpus_Guide]] · [[Design_System]] · [[Accessibilite]] ·
> [[Wireframes_Annotes]] · [[Release_Notes]] · [[Roadmap_Backlog]] (TF-LP-*) · [[IDEA]] · [[Moteur_IA_World_Model_OODA]]

**Dernière mise à jour :** 07/07/2026 · **Version :** 0.1 · **Projet :** Taskforce — Metz Numeric School 2025-2026
