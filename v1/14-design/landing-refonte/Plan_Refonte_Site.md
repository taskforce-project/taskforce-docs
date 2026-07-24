---
id: landing-plan-refonte
title: Plan de refonte — Site TaskForce (architecture, design system, conformité UE)
doc_type: spec
statut: en-cours
version: 1.0
date: "24/07/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [landing, refonte, architecture, sitemap, design-system, rgpd, wcag, conformite, ue, labs, v2]
related:
  - "./Spec_Master.md"
  - "./Design_Corpus_Guide.md"
  - "../Design_System.md"
  - "../Accessibilite.md"
  - "../../../v1/road_to_v2/README.md"
  - "../../../IDEA.md"
---

# 🏗️ Plan de refonte — Site TaskForce

[![Type: Plan](https://img.shields.io/badge/Type-Plan%20de%20refonte-8b5cf6?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]() [![Réf: Relevance AI](https://img.shields.io/badge/R%C3%A9f%C3%A9rence-Relevance%20AI-6056FF?style=for-the-badge)]()

**Tags :** `#landing` `#architecture` `#design-system` `#rgpd` `#wcag` `#conformite`

> **Rôle de ce document.** Il définit **l'architecture complète du site** (au-delà de la seule home),
> le **design system du site marketing**, et le **socle de conformité européenne** (RGPD, ePrivacy,
> WCAG 2.2 AA / EN 301 549, LCEN, AI Act).
> Il **complète** [[Spec_Master]] (positionnement, message-map, badges d'honnêteté) qui reste l'ancre.
>
> **Référence d'architecture :** `relevanceai.com`, crawlé le 24/07/2026 (308 URLs) puis mesuré au DOM.
> On reprend **leur architecture d'information et leur langage de composants**, avec **notre charte** et **notre contenu**.
>
> **Repo de dev :** `taskforce-fullstack/landing-page/` uniquement. **Repo de doc :** ici.

---

## 1. Décisions cadrées (24/07/2026)

| # | Décision | Choix retenu | Conséquences |
|---|---|---|---|
| **D5** | **Refonte totale** | On **repart des fondations** : les composants marketing actuels sont abandonnés | Purge de ~25 composants (§7). Le kit `ui/` shadcn est **conservé** (base saine). |
| **D6** | **Périmètre = vision, pas v1** | Le site présente **l'AI Delivery OS**, la v1 n'est qu'une **preuve** | Le narratif porte la vision ; les badges 🟢/🔵/🟣 de [[Spec_Master]] §1.1 restent la garantie d'honnêteté. |
| **D7** | **Section `/labs` publique** | La **R&D est publiée** (World Model × OODA, LLM local, benchmarks, data flywheel) | Différenciateur majeur : personne ne le fait. Transforme « pas encore livré » en **« recherche en public »**. |
| **D8** | **Conformité UE by design** | RGPD + WCAG 2.2 AA + ePrivacy + LCEN + **AI Act** dès le lot 0 | Analytics **sans cookie** ⇒ **aucun bandeau** (§8.2). A11y intégrée au kit, pas auditée après coup. |
| **D9** | **Zéro faux client** | Pas de logo client, pas de témoignage inventé, pas de note G2 | On remplace la preuve sociale par la **preuve technique** (§5, bloc 3) et le **dogfooding**. |

### 1.2 Décisions du 24/07 (soir) — portée et divulgation

| # | Décision | Choix retenu | Conséquences |
|---|---|---|---|
| **D10** | **Périmètre métier** | **Ouvrir au-delà de la tech** | On vend la vision (D6), donc le discours n'est plus « livraison logicielle » mais « du travail qui passe par des étapes relues et validées ». `Solutions` passe de *par rôle tech* à **par équipe** : Engineering · Product · Operations · Marketing · Client services. L'ingénierie reste le **seul métier prouvé** — les autres portent un badge de maturité sur leur page. |
| **D11** | **`/labs` — annulée** | **On publie la direction, pas le mécanisme** | ⚠️ **Renversement de D7.** Publier le fonctionnement de notre différenciateur **avant qu'il tourne**, c'est offrir la recette : n'importe qui peut l'implémenter d'abord. On garde la vente de la vision, on retire le mode d'emploi. |

#### Ce que D11 change concrètement

| Retiré | Motif |
|---|---|
| Entrée `Labs` de la barre de navigation | Invitait explicitement à venir lire comment c'est fait |
| `/labs/world-model-ooda` | **Le cœur du moat.** La boucle de raisonnement est ce qui nous distingue ; la décrire publiquement l'annule. |
| `/labs/benchmarks` | La méthode d'évaluation est un actif, pas du contenu marketing |
| `/labs/data-flywheel` | Idem — comment on apprend des retours |
| `/labs/local-llm`, `/labs/notes` | Détails d'implémentation |
| Badge public « Labs » | Devient **« Planned »** : annonce ce qui arrive sans inviter à la visite guidée |

| Conservé | Motif |
|---|---|
| **`/roadmap` public et daté** | Vend la direction, ne révèle aucun mécanisme. Une roadmap se tient, elle ne se copie pas. |
| Section « Where this goes » sur la home | Trois intentions (moins de rédaction, au-delà de l'ingénierie, votre infra), **zéro architecture** |
| Colonne « Planned » de la carte de maturité | L'honnêteté sur ce qui n'est pas livré reste ; c'est le *comment* qui disparaît |

> **La ligne à tenir :** une **vision** se vend et ne se copie pas — l'exécution est le travail.
> Un **mécanisme** se copie en une lecture. On publie donc le *quoi* et le *pourquoi*, jamais le *comment*.

### 1.1 Arbitrages utilisateur (24/07/2026)

| Question | Réponse | Conséquence |
|---|---|---|
| Police display | **Sora** (comme la référence), Inter pour le corps | Chargée via Google Fonts, exposée en `--font-display` / `font-display` |
| Hébergement | **À trancher** — Vercel, Render, ou **Hetzner (Allemagne)** | La politique de confidentialité reste **agnostique** : un seul paragraphe à renseigner. Hetzner DE = UE, supprime le chapitre transferts. |
| Identité de publication | **Placeholders** pour l'instant (éditeur = Pierre MICHEL) | `/legal/notice` est rédigeable, les champs RCS/SIREN/hébergeur restent à compléter avant mise en ligne. |

---

## 2. Ce qu'on a mesuré chez Relevance AI

### 2.1 Architecture (crawl 24/07/2026 — 308 URLs)

| Zone | Volume | Rôle |
|---|---|---|
| `/docs/**` | **171 pages** | Documentation produit — le socle SEO longue traîne |
| `/use-cases/**` | **39 pages** | Une page par **job-to-be-done** (`deal-reviewer`, `churn-risk-detector`…) |
| `/blog/**` | 13 | Contenu éditorial |
| `/customers/**` | 10 | Études de cas nommées (Canva, KPMG, Rakuten…) |
| `/vs/**` | 6 | **Comparatifs concurrents** (`/vs/clay`, `/vs/gemini-enterprise`…) — SEO d'intention d'achat |
| `/function/**` | 5 | Une page par **fonction métier** (sales, marketing, ops…) |
| Pages produit | ~20 | `/product`, `/agents`, `/workflows`, `/knowledge`, `/integrations`, `/approvals-escalations`, `/version-control`, `/collaboration`… |
| Agents nommés | ~10 | `/seo-agent`, `/phone-agent`, `/crm-enrichment-agent` — **landing SEO par persona d'agent** |
| Légal / trust | 3 + Trust Center | `/privacy-policy`, `/terms-and-conditions`, `/data-security-policy` |
| Entreprise | ~8 | `/pricing`, `/enterprise`, `/careers`, `/partners`, `/media-enquiries`, `/changelog`, `/api` |

**Enseignement n°1 :** leur volume vient de **3 gabarits répétés** (`use-case`, `function`, `vs`) alimentés par de la donnée. Ce n'est pas 300 pages écrites à la main — c'est **3 templates × N entrées**. C'est exactement reproductible chez nous, à moindre coût.

**Enseignement n°2 :** la navigation ne montre que **5 entrées** (Solutions · Customers · Product · Resources · Enterprise) + `Sign in` + `Talk to sales`. La profondeur est dans les méga-menus et le footer, pas dans la barre.

### 2.2 Direction artistique (mesurée au DOM)

| Token | Valeur relevée | Notre équivalent |
|---|---|---|
| Fond dominant | `#ffffff` (105 occurrences), bandes `#f8fafc` / `#f3f3f4` | `#ffffff` + bandes `#f6f6f8` |
| Accent | **`#6056FF`** (indigo/violet) | **`#2563eb`** — le primaire de l'app. Leur violet n'a pas à dicter le nôtre ; notre violet `#5856d6` reste l'**accent IA**, comme dans le produit. |
| Texte | `#0d162f` (titres) · `#868a97` (secondaire) | `#1d1d1f` · `#6e6e73` |
| Typo | **Inter** (corps, 2528 nœuds) + **Sora** (display, 128 nœuds) | Inter partout (cohérence app) |
| H1 | **48 px · 400 · −2.4 px (−0.05em) · lh 1.2 · aligné à gauche** | 48→56 px · 500 · −0.03em · lh 1.15 |
| H2 | 36 px · 400 · −0.9 px · lh 1.35 | 36→40 px · 500 · −0.025em |
| Boutons | **pill `border-radius: 9999px`** · h **42 px** · 14 px/400 · padding 10/20 | **identique** (changement fort vs notre `rounded-lg` actuel) |
| Rayons | pill (148×) ≫ 6 px (44×) > 8 / 12 / 16 px | pill boutons · 12–16 px cartes |
| Header | **65 px**, fond transparent, **sans bordure** | idem |
| Conteneur | **1265 px** | **1240 px** |
| Hauteur de home | **13 333 px** | cible **≥ 11 000 px** |

> **Le vrai écart avec notre landing actuelle** n'est pas la couleur : c'est le **bouton pill**, la **densité de mocks produit** (chaque bloc porte une carte de données réaliste) et la **longueur assumée**.

### 2.3 Narratif de leur home (23 blocs relevés)

Hero + onglets persona → bandeau KPI + **table de runs** → marquee preuves → **timeline de déploiement** → onglets par fonction (8 cartes agents, chacune avec son mini-visuel) → 3 études de cas chiffrées → comparatif concurrent → **feature blocks avec graphiques** (benchmarks, choix de modèle) → citation client → **grille entreprise/trust** (badges SOC2/GDPR + 3 colonnes) → intégrations → **« tout sur une seule pile » (remplace Zapier, Zep, Composio, Braintrust…)** → **grille de combinaisons (A + B = bénéfice)** → couche de contexte → **framework de maturité L1→L4** → presse → footer 6 colonnes.

---

## 3. Architecture du site TaskForce

### 3.1 Sitemap complet

```
/                                     Home
│
├── /product                          Hub — l'AI Delivery OS
│   ├── /product/orchestration        Pipeline Vision → Deploy en checkpoints        🟣
│   ├── /product/agents               Agents CPO / CTO / COO                          🟣
│   ├── /product/approvals            Human-in-the-loop, validations, escalades       🔵
│   ├── /product/brain-os             Couche de contexte / graphe de connaissance     🔵
│   ├── /product/smart-assign         Affectation raisonnée (5 signaux + LLM)         🟢
│   ├── /product/collaboration        Boards, issues, cycles, temps réel              🟢
│   ├── /product/analytics            Métriques de livraison                          🟢
│   └── /product/integrations         Catalogue (47 outils, 16 catégories)            🟢
│
├── /solutions                        Par rôle
│   ├── /solutions/cto
│   ├── /solutions/head-of-product
│   ├── /solutions/engineering-manager
│   ├── /solutions/founder
│   └── /solutions/agency
│
├── /use-cases                        Par job-to-be-done  ← gabarit répété
│   ├── /use-cases/product-spec           /use-cases/architecture-decision
│   ├── /use-cases/backlog-grooming       /use-cases/code-review
│   ├── /use-cases/qa-testing             /use-cases/documentation
│   ├── /use-cases/onboarding             /use-cases/incident-postmortem
│   └── /use-cases/release-notes          /use-cases/sprint-planning
│
├── /vs                               Comparatifs  ← gabarit répété
│   ├── /vs/jira    /vs/linear    /vs/notion
│   └── /vs/shortcut    /vs/devin    /vs/claude-code-alone
│
├── /labs                          ⭐ Hub R&D publique
│   ├── /labs/world-model-ooda        Le moteur de raisonnement
│   ├── /labs/local-llm               Ollama, souveraineté, coût zéro
│   ├── /labs/benchmarks              Comparatif de modèles sur golden set
│   ├── /labs/data-flywheel           RAG → LoRA, apprentissage produit
│   └── /labs/notes                   Journal de recherche (flux daté)
│
├── /pricing        /enterprise       /book-a-demo
│
├── /resources
│   ├── /docs                         Publication de taskforce-docs
│   ├── /blog                         /learn (glossaire SEO)
│   ├── /changelog                    /roadmap                /status
│
├── /company
│   ├── /company/about                /company/contact        /company/media
│
├── /trust                            Trust center (hub sécurité + conformité)
│
└── /legal
    ├── /legal/notice                 Mentions légales (LCEN)
    ├── /legal/privacy                Politique de confidentialité (RGPD)
    ├── /legal/cookies                Politique cookies + inventaire
    ├── /legal/terms                  CGU        /legal/subscription  CGV
    ├── /legal/dpa                    Accord de sous-traitance (art. 28)
    ├── /legal/subprocessors          Sous-traitants ultérieurs
    ├── /legal/security               Politique de sécurité
    ├── /legal/accessibility          Déclaration d'accessibilité
    └── /legal/ai-transparency        Transparence IA (AI Act art. 50)  ⭐

Techniques : /404 · /sitemap (HTML) · /sitemap.xml · /robots.txt · /.well-known/security.txt
```

**Volume cible :** ~28 pages écrites + ~21 pages générées par gabarit = **~49 pages**.

### 3.2 Barre de navigation (5 entrées, comme Relevance)

| Entrée | Type | Contenu |
|---|---|---|
| **Product** | Méga-menu 3 colonnes | *Plateforme* (Orchestration, Agents, Approvals, Brain OS) · *Delivery* (Smart Assign, Collaboration, Analytics, Integrations) · *encart* « Labs — la R&D en public » |
| **Solutions** | Méga-menu 2 colonnes | *Par rôle* (5) · *Par cas d'usage* (10 + « Voir tout ») |
| **Labs** | Lien direct | `/labs` — assumé comme entrée de nav, c'est notre signature |
| **Resources** | Méga-menu | Docs · Blog · Learn · Changelog · Roadmap · Status |
| **Enterprise** | Lien direct | `/enterprise` |
| *(droite)* | — | `Pricing` · `Sign in` · **`Get started`** (pill, accent) |

### 3.3 Footer (6 colonnes + barre basse)

`Product` · `Solutions` · `Labs` · `Resources` · `Company` · `Legal & Trust`
Barre basse : © 2026 TaskForce · langue (EN/FR) · **statut système** (pastille live) · **« Hébergé dans l'UE »** · liens sociaux.

---

## 4. Design system du site

### 4.1 Jetons — **copiés de la webapp**, pas réinventés

> **Règle.** Le `:root` du site est une **copie de `frontend/app/globals.css`** (palette
> Cloudflare-flat, light-only). Aucune couleur n'est créée pour le marketing : si la palette
> bouge dans le produit, elle bouge sur le site. Les `--site-*` ci-dessous ne sont que des
> **alias de lecture** pointant sur les jetons de l'app.
>
> ⚠️ **Le violet `#5856d6` n'est que le marquage IA / Labs.** Jamais un CTA, jamais un hover.
> Le hover d'une action primaire est `bg-primary/90`, dérivé du jeton — pas une valeur en dur.

```css
--site-bg:        #ffffff;   /* fond principal */
--site-band:      #f6f6f8;   /* bandes alternées */
--site-fg:        #1d1d1f;   /* texte principal */
--site-muted:     #6e6e73;   /* texte secondaire */
--site-border:    #e6e6e9;   /* bordures 1px */
--site-brand:     #2563eb;   /* = --primary de l'app : LA couleur TaskForce (CTA, liens) */
--site-brand-soft:#eff6ff;
--site-ai:        #5856d6;   /* = --accent-purple de l'app : marquage IA / Labs uniquement */
--site-ai-soft:   #efeefc;
--radius-card:    16px;
--radius-pill:    9999px;    /* tous les boutons */
--container:      1240px;
--section-y:      112px;     /* rythme vertical (py-28) */
```

### 4.1 bis — Les rails (la structure de la page)

> **La leçon du 24/07.** On a d'abord repris le *contenu* de Relevance au lieu de sa *structure*.
> Ce qui fait tenir leur page, ce n'est pas leurs textes : c'est une **grille visible**.

| Élément | Mise en œuvre |
|---|---|
| Filets verticaux | `.container-rail` — `border-inline` aux bords du conteneur 1240px |
| Séparateurs de section | `border-b` **pleine largeur** porté par chaque `<section>` |
| Filets internes de grille | `.rail-x` / `.rail-y` (colonnes de tableau, cartes accolées) |
| Cartes accolées | `gap-px` + `bg-border` sur le conteneur : les bordures deviennent la grille |

Appliqué au Hero, à toutes les sections et au footer. **Sans les rails, la page flotte** —
c'est le seul élément qui donne de la forme à un site en light-only très sobre.

### 4.2 Échelle typographique

| Niveau | Desktop | Poids | Tracking | Interligne |
|---|---|---|---|---|
| H1 | 56 px (`clamp(40px, 5vw, 56px)`) | 500 | −0.03em | 1.1 |
| H2 | 40 px | 500 | −0.025em | 1.15 |
| H3 | 20 px | 500 | −0.01em | 1.3 |
| Corps | 16 px | 400 | 0 | 1.6 |
| Petit / légende | 13–14 px | 400 | 0 | 1.5 |
| Eyebrow | 13 px | 600 | +0.08em, majuscules | 1 |

### 4.3 Kit de composants à construire (le cœur du chantier)

> **Règle d'implémentation.** Tout ce qui est **atomique** vient de **shadcn** et se fait par
> **extension** (nouvelle variante `cva`), jamais par réécriture : `Button` (variante `ink`,
> tailles `pill-*`), `Badge` (variantes `live` / `beta` / `labs`), `NavigationMenu`, `Sheet`,
> `Accordion`, `Tabs`… Les composants `site/*` ci-dessous sont des **assemblages** (sections,
> mocks, grilles), pas des primitives.
> Exception assumée : `.link-underline` est une **classe CSS** (soulignage animé du breadcrumb
> de l'app) et non un composant — un lien souligné n'a pas à être un composant React.

| # | Composant | Usage |
|---|---|---|
| 1 | `Button` (pill : primary / dark / ghost / link) | Partout — remplace les boutons `rounded-lg` |
| 2 | `SectionHeader` (eyebrow + titre + chapô, aligné gauche ou centré) | Toutes les sections |
| 3 | `Section` (bande blanche/grise, rythme vertical, conteneur) | Toutes les sections |
| 4 | **`MockCard`** (carte blanche, bordure 1 px, ombre douce, r16) | **Le composant clé** : chaque bloc porte un mock |
| 5 | `PersonaTabs` | Hero : le mock change selon le persona |
| 6 | `StatStrip` | Bandeau de 4 KPI |
| 7 | `RunTable` | Table de runs (Tâche · Agent · Modèle · Checkpoint · Coût) |
| 8 | `Marquee` | Défilement logos / preuves |
| 9 | `StepTimeline` | « De l'intention au déployé » en 3 temps |
| 10 | `PipelineViz` | Les 7 checkpoints (refonte du composant actuel) |
| 11 | `FeatureSplit` | Bloc texte + mock, alterné gauche/droite |
| 12 | `CardGrid` + `AgentCard` | Grille de cartes à mini-visuel |
| 13 | `ComparisonSplit` | Nous vs l'alternative |
| 14 | **`StackReplaces`** | « comme Jira », « comme Notion » — remplace la pile |
| 15 | **`ComboGrid`** | A + B = bénéfice |
| 16 | **`MaturityFramework`** | Niveaux d'autonomie L1→L4, en onglets |
| 17 | `TrustGrid` | Badges + 3 colonnes (sécurité / accès / supervision) |
| 18 | `IntegrationGrid` | Catalogue filtrable |
| 19 | `MaturityBadge` | 🟢 Live · 🔵 Beta · 🟣 Labs |
| 20 | `CtaBand` | Invitation finale |
| 21 | `SiteHeader` (méga-menus) + `SiteFooter` (6 col.) | Coquille |
| 22 | `LegalLayout` (sommaire ancré, dernière MAJ) | Les 10 pages légales |

> **Règle produit :** *aucune section sans preuve visuelle*. Un bloc = un texte + un mock. C'est ce qui fait la densité de Relevance.

---

## 5. Narratif de la home (18 blocs)

| # | Bloc | Composant | Preuve |
|---|---|---|---|
| 1 | **Hero** — « Describe the outcome. TaskForce orchestrates the execution. » + onglets persona | `PersonaTabs` | mock qui change par persona |
| 2 | **Bandeau KPI + table de runs** | `StatStrip` + `RunTable` | Runs, checkpoints validés, temps de cycle, **coût/run** |
| 3 | **Socle technique** (à la place des logos clients) | `Marquee` | Java/Spring · Postgres+pgvector · Ollama · Keycloak · MinIO · Docker + « EU-hosted / Self-host / Open » |
| 4 | **Thèse** — le problème en une phrase | `SectionHeader` XL | — |
| 5 | **De l'intention au déployé** — 3 temps | `StepTimeline` | — |
| 6 | **Le pipeline** — 7 checkpoints | `PipelineViz` | mock run |
| 7 | **Les agents** — CPO / CTO / COO en onglets | `CardGrid` | 1 mini-visuel par agent |
| 8 | **Human-in-the-loop** — validation, escalade, reprise | `FeatureSplit` | mock d'approbation |
| 9 | **Brain OS** — le contexte défini une fois | `FeatureSplit` | graphe |
| 10 | **Smart Assign** 🟢 | `FeatureSplit` | mock board |
| 11 | **Modèles & coût** — local ou cloud, routage | `FeatureSplit` | table de coût (0 € en local) |
| 12 | **Analytics de livraison** 🟢 | `FeatureSplit` | graphiques |
| 13 | **Tout le delivery sur une seule pile** | `StackReplaces` | « comme Jira », « comme Notion », « comme Linear »… |
| 14 | **Les combinaisons** | `ComboGrid` | Pipeline + Brain OS · Smart Assign + Analytics · Approvals + Audit |
| 15 | **Niveaux d'autonomie L1 → L4** + notre position honnête | `MaturityFramework` | — |
| 16 | **Entreprise & conformité** | `TrustGrid` | SSO · RBAC · audit · self-host · RGPD · UE |
| 17 | **Intégrations** — 47 outils | `IntegrationGrid` | catalogue réel |
| 18 | **Labs** — la R&D en public + **CTA final** | teaser + `CtaBand` | — |

**Cible :** ≥ 11 000 px de hauteur, 18 blocs, ≥ 12 mocks distincts.
**Livré (24/07/2026) :** 17 sections, 7 mocks, 26 vrais logos. Un seul îlot hydraté (le Hero, pour
ses onglets persona) ; les 16 autres sections sont du HTML statique.

> ### ⚠️ Correction — reprendre l'architecture, pas le contenu
>
> La première version décalquait Relevance : « All of your agents on one stack » avec les libellés
> « like Zapier », « On one platform, the pieces make each other better », et leur échelle
> d'autonomie L1→L4. Trois blocs remplacés par nos propres arguments :
>
> | Copié | Remplacé par |
> |---|---|
> | « one stack » + « like Jira » | **Le diagnostic** : où vit chaque chose aujourd'hui, et ce qui s'y perd |
> | « the pieces make each other better » | « Ce qu'on gagne à ne pas intégrer quatre outils » |
> | Échelle L1→L4 | **Carte de maturité** Shipped / Partial / Research avec **nos vraies features** |
> | « How it works » en 3 cartes | **Anatomie d'un run** : tableau *Checkpoint · Produced by · What lands in your workspace · What you decide*, dans le vrai ordre d'exécution |
>
> Ce qu'on leur reprend : **l'architecture, l'ordre logique, la densité, les rails**. Pas le texte.

**Ordre de la home :** problème → mécanisme → garantie → composants → conséquence → honnêteté →
preuve. Chaque section répond à la question que la précédente vient de poser.

> **Piège vérifié en test.** Radix Tabs commute sur `mousedown`, pas sur `click` : un
> `element.click()` scripté ne change rien et donne l'illusion d'un composant mort. Tester avec
> `dispatchEvent(new MouseEvent('mousedown', { bubbles: true, button: 0 }))`.

---

## 6. Conformité européenne

### 6.1 RGPD (Règl. UE 2016/679)

| Exigence | Mise en œuvre | Page |
|---|---|---|
| Information (art. 13/14) | Identité du responsable, finalités, **bases légales**, destinataires, durées, droits, réclamation CNIL, contact | `/legal/privacy` |
| Minimisation | Formulaires réduits au nécessaire ; pas de champ « téléphone » obligatoire | formulaires |
| Base légale prospection B2B | **Intérêt légitime** + opt-out visible à chaque envoi | `/legal/privacy` |
| Newsletter | **Double opt-in**, case **non pré-cochée**, désinscription 1 clic | formulaires |
| Sous-traitance (art. 28) | **DPA téléchargeable** + liste des **sous-traitants ultérieurs** avec préavis de changement | `/legal/dpa`, `/legal/subprocessors` |
| Transferts hors UE | Éviter par défaut → **hébergement UE** ; sinon CCT + mention DPF | `/legal/privacy`, `/trust` |
| Registre (art. 30) | Interne, non publié | vault |
| Droits | Adresse unique de contact + délai 1 mois annoncé | `/legal/privacy` |
| Sécurité (art. 32) | Chiffrement transit/repos, RBAC, journaux d'audit | `/legal/security` |

> **Choix structurant :** viser un **hébergement UE** (Scaleway / OVH / Hetzner) plutôt que Vercel US. Cela supprime le chapitre « transferts internationaux », et devient un **argument commercial** affiché en pied de page.

### 6.2 Cookies / ePrivacy (dir. 2002/58, art. 82 LIL, lignes directrices CNIL)

**Décision : analytics sans cookie ⇒ pas de bandeau.**

| Règle | Conséquence |
|---|---|
| Aucun dépôt non essentiel avant consentement | On n'en dépose **aucun** |
| « Tout refuser » aussi accessible que « Tout accepter » | *sans objet* si pas de traceur |
| Choix granulaire par finalité, preuve conservée, ≤ 13 mois | *sans objet* |
| Mesure d'audience exemptée (conditions CNIL) | **Plausible / Umami auto-hébergé** : pas d'identifiant persistant, pas de recoupement, données UE |
| Inventaire public des cookies | `/legal/cookies` liste **les cookies techniques uniquement** (session, préférence de langue) |

> Si un jour on ajoute un traceur marketing (Ads, Hotjar…), le bandeau devient **obligatoire** — prévoir le composant, ne pas le monter maintenant.

### 6.3 Accessibilité — **WCAG 2.2 niveau AA** (= EN 301 549 v3.2.1)

| Cadre | Applicabilité à nous | Position |
|---|---|---|
| **WCAG 2.2 AA** | Standard de référence | **Cible engagée** |
| **EN 301 549 v3.2.1** | Norme harmonisée UE (marchés publics) | Alignée sur WCAG AA |
| **European Accessibility Act** (dir. UE 2019/882, applicable depuis le **28/06/2025**) | Vise les services **aux consommateurs** (e-commerce, banque…). Un site B2B n'y est **pas directement** soumis ; le devient si vente en ligne en libre-service | **Conformité visée** — exigée en due diligence grands comptes |
| **RGAA 4.1** (FR) | Secteur public + entreprises > 250 M€ de CA | Hors périmètre — **déclaration volontaire** publiée |

**Definition of Done accessibilité (bloquante à chaque lot) :**

- `lang` correct + changement de langue annoncé ; **lien d'évitement** vers le contenu ;
- structure sémantique : `header/nav/main/footer`, un seul `h1`, hiérarchie sans saut ;
- **contrastes** ≥ 4.5:1 (texte), ≥ 3:1 (texte large et éléments d'interface) ;
- **focus visible** et **non masqué** par le header collant (WCAG 2.2 — 2.4.11) ;
- **cibles ≥ 24 × 24 px** (2.5.8) ;
- navigation clavier complète, méga-menus **utilisables au clavier** et fermés par `Échap` ;
- `prefers-reduced-motion` respecté sur **toutes** les animations ;
- jamais d'information portée **par la couleur seule** ; images décoratives en `alt=""` ;
- formulaires : `label` liés, erreurs identifiées **en texte**, aide cohérente (3.2.6) ;
- **tests** : `axe` en CI + parcours clavier + lecteur d'écran sur les 5 pages principales.

### 6.4 Mentions légales (LCEN art. 6-III) — `/legal/notice`

Dénomination et forme juridique · capital · siège · RCS/SIREN · TVA intracommunautaire · **directeur de la publication** · contact · **hébergeur** (raison sociale, adresse, téléphone).

### 6.5 AI Act (Règl. UE 2024/1689) — `/legal/ai-transparency` ⭐

Nous vendons un produit d'IA : l'obligation de **transparence (art. 50)** s'applique dès qu'un utilisateur interagit avec un système d'IA.

| Point | Mise en œuvre |
|---|---|
| Interaction IA signalée | Tout assistant/chat du site est explicitement identifié comme IA |
| Modèles utilisés | Page publique : quels modèles, où ils tournent (**local Ollama** / cloud), ce qui sort de l'UE |
| Entraînement sur les données clients | **Non** — affirmé et documenté |
| Supervision humaine | Le **human-in-the-loop** est le cœur produit : atout de conformité, pas une contrainte |
| Journalisation | Traçabilité des runs et des décisions d'agents |

> C'est un **argument de vente** autant qu'une obligation : très peu d'éditeurs IA publient cette page en 2026.

### 6.6 Autres exigences

| Sujet | Règle | Mise en œuvre |
|---|---|---|
| Prix B2B | Affichage **HT** explicite + devise | `/pricing` |
| CGV / abonnement | Durée, reconduction, résiliation, rétractation (14 j si B2C) | `/legal/subscription` |
| Contact et réclamation | Adresse électronique de contact fonctionnelle | `/company/contact` |
| Divulgation de vulnérabilité | **security.txt** (RFC 9116) + politique | `/.well-known/security.txt` |
| SEO technique | `sitemap.xml`, `robots.txt`, canonical, **hreflang en/fr**, JSON-LD (`Organization`, `SoftwareApplication`, `FAQPage`, `BreadcrumbList`), OG/Twitter | global |
| Performance | Budget : LCP < 2 s, CLS < 0.1, JS initial < 100 ko — **SSG Astro**, hydratation ciblée | global |
| NIS2 / DSA | **Hors périmètre** pour un site vitrine — à réévaluer si hébergement de contenus tiers | — |

---

## 7. Purge — composants supprimés ✅ (24/07/2026)

> **Fait.** 14 pages legacy + ~55 composants supprimés. Il ne reste que `/` et `/pricing` ;
> toutes les autres URLs sont à recréer par les lots L3→L8. Les dossiers
> `components/layout/`, `components/magicui/` et `contexts/` n'existent plus.
> `config/constants_{en,fr}.ts` sont **conservés** comme réservoir de copie rédigée.

**Sections marketing (obsolètes, DA abandonnée) :** `sections/AISection` · `BentoFeatures` · `CoreCapabilities` · `CTA` · `CtaSection` · `Developers` · `Enterprise` · `FeatureCards` · `Hero` · `HomeFeatures` · `HomeSections` · `HowItWorks` · `Integrations` · `LogosSection` · `Migration` · `Mobile` · `OrchestrationPipeline` · `PricingSection` · `SelfHosted`.

**Composants de démo importés :** `feature72` · `hero115` · `logos3` · `process1` · `testimonial4` · `ui/testimonials-columns-1` · `ui/bento-grid` · `ui/etheral-shadow` · `ui/iphone` · `ui/safari` · `ui/noise-texture` · `magicui/striped-pattern`.

**Doublons et pages legacy :** `AccessibilityPageNew` · `DocsPageNew` · `PrivacyPolicyPageNew` · `TermsPageNew` (fusionner avec l'original) · `App.tsx` · `layout/Header` · `layout/Footer` · `pages/hero-preview.astro`.

**À trancher :** `ThemeContext` / `ThemeSwitcher` (décision D2 = light-only ⇒ **supprimer**) · `AccessibilityContext` / `AccessibilityDropdown` (les préférences a11y maison sont **redondantes** avec le respect des réglages système — à remplacer par `prefers-reduced-motion` / `prefers-contrast`).

**À conserver :** tout `components/ui/**` shadcn (base saine) · `layout/SiteHeader` et `SiteFooter` (à refondre, pas à jeter) · `layouts/BaseLayout.astro` · `LanguageContext` · `lib/utils`.

---

## 8. Plan de production

| Lot | Contenu | Sortie vérifiable |
|---|---|---|
| **L0 — Fondations** ⏳ | ~~jetons (§4.1)~~ · ~~`Button` pill~~ · ~~`MaturityBadge`~~ · ~~`BaseLayout` a11y (skip link, landmark, focus)~~ · reste : `Section` / `SectionHeader` / `MockCard` + purge (§7) | Page `/kit` interne montrant tout le kit |
| **L1 — Coquille** ⏳ | ~~`SiteHeader` méga-menus accessibles + menu mobile~~ · reste : `SiteFooter` 6 colonnes · `/404` | Navigation complète au clavier |
| **L2 — Home** ✅ | Les 18 blocs (§5) + 7 mocks | **14 806 px, 18 sections, 1 `h1` / 21 `h2`** — cible dépassée (réf. Relevance : 13 333 px) |
| **L3 — Produit** | `/product` + 8 sous-pages (gabarit `FeatureSplit`) | 9 pages |
| **L4 — Conversion** | `/pricing` · `/enterprise` · `/book-a-demo` · `/trust` | 4 pages |
| **L5 — Labs** ⭐ | `/labs` + 5 pages (contenu tiré de `road_to_v2/`) | 6 pages |
| **L6 — Gabarits** | `/solutions` (5) · `/use-cases` (10) · `/vs` (6) pilotés par données | 21 pages, 3 templates |
| **L7 — Ressources** | `/changelog` · `/roadmap` · `/status` · `/blog` · `/learn` · `/docs` | 6 pages |
| **L8 — Légal & conformité** | Les 10 pages `/legal/**` + `security.txt` + `sitemap.xml` + JSON-LD + hreflang | Conformité §6 vérifiée point par point |
| **L9 — Audit** | axe + Lighthouse + clavier + lecteur d'écran + budget perf | Rapport d'audit dans le vault |

---

## 9. Dette de contenu (à fournir)

| Élément | Statut | Bloquant pour |
|---|---|---|
| Captures produit réelles | ❌ manquant | Hero, `/product/**` |
| Montants de tarification | ⚠️ provisoires ($12 / $10) | L4 |
| Témoignages / logos clients | ❌ **aucun** — décision D9 : ne rien inventer | remplacé par la preuve technique |
| Logos d'intégrations (SVGL) | ⚠️ initiales | L2, `/product/integrations` |
| Identité légale (SIREN, siège, hébergeur, directeur de publication) | ❌ manquant | **L8 — bloquant** |
| Contenu `/labs` | ✅ disponible dans `road_to_v2/` | L5 |
| Catalogue d'intégrations (47 outils) | ✅ disponible dans `Connecteurs_et_Catalogue.md` | L2 |

---

**Projet :** TaskForce — Metz Numeric School 2025-2026
