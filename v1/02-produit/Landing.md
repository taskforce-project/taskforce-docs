---
id: produit-landing
title: État Produit — Landing
doc_type: register
statut: active
version: 0.1
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, landing, seo]
related:
  - "./README.md"
---
<!-- Logo établissement : assets/images/logo_metz_numeric_school.svg | Logo projet : assets/images/logo_taskforce.png -->

# État Produit — Landing (`landing-page/`)

**Version :** 0.1 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: landing](https://img.shields.io/badge/R%C3%A9pertoire-landing-blue?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [🧠 Brain OS](../../Brain_OS.md) · [Backlog](../13-roadmap/Roadmap_Backlog.md)

**Tags :** `#produit` `#landing` `#seo`

> Stack : Astro 7 (SSG) + îlots React, déployé par Vercel (prod = `main`) sur taskforce-project.fr. Légende : ✅ `done` · 🔄 `wip` · ⬜ `todo`. Compétence RNCP dominante : **C20 (SEO)**.

## Version produit (footer)
- [x] **Version produit UNIFIÉE dans les footers app + landing (10/09/2026)** [id:: LP-VERSION-001] [statut:: done] [parite:: ok] [ref:: frontend/product-version.json + frontend/next.config.ts + frontend/components/layout/app-footer.tsx + landing-page/src/product-version.ts + scripts/bump-product-version.mjs] — Les 2 footers montraient `v0.3.23`, une **ancienne somme** front+back (`frontend/package.json` 0.3.8 + pom 0.0.15) jamais recalculée et **découplée des vrais tags git** (back 0.11 / front 0.17 / landing 1.1.5). Décision CEO : **un seul numéro, affichage unifié = `0.18.0`** (portée « affichage » : les tags Docker par service restent internes au déploiement). **Source de vérité** `frontend/product-version.json` (`version`, lu par `next.config` → `NEXT_PUBLIC_APP_SEMVER` → footer app) + **copie synchronisée** `landing-page/src/product-version.ts` (footer landing ; les 2 contextes de build Docker sont isolés). `scripts/bump-product-version.mjs <major|minor|patch|set x.y.z>` écrit **les deux** ; ancien `scripts/product-version.mjs` (la somme) **supprimé** ; la CI `release.yml` crée le **tag produit unique** `taskforce-v<version>`. **MAJ 10/09/2026 - bump AUTOMATIQUE** : le footer restait figé (bump manuel jamais fait). Désormais le workflow `.github/workflows/sync-product-version.yml` (`on: pull_request → main`) calcule la version = **le plus fort bump parmi les services touchés** (major > minor > patch, lu des labels de la PR) vs la version de `main`, et l'écrit dans les deux fichiers **sur la branche de la PR** (→ portée sur main par le squash, pas de push sur main protégée). Jamais de régression. Valeur courante backfillée à **0.19.1** (0.18.0 + #266 minor + #267 patch). Front tsc + build landing verts. **MAJ 25/09/2026** : sans pré-bump sur `dev`, le bot n'écrit la version que sur la branche de release, donc `dev` était resté en 0.38.0 pendant que la prod passait en 0.38.1 puis **0.39.0** ; réaligné par un commit `chore(version)` sur `dev`. Voir [PC-047](../09-audits/Problemes_Connus.md).

## SEO & performance
- [x] **Métadonnées, sitemap.xml, Open Graph, JSON-LD (09/2026, v0.36.x)** [id:: LP-SEO-001] [statut:: done] [parite:: ok] [prio:: P1] (TF-LP-001 · C20) : JSON-LD à source unique (`src/lib/structured-data.ts` : Organization, WebSite, SoftwareApplication, BreadcrumbList, FAQPage), `sitemap.xml` généré (lastmod / priority + fiches connecteurs), `llms.txt`, og:image absolue, canonical non-www ; propriété Search Console créée et sitemap soumis. **MAJ 25/09/2026 (v0.39.0)** : 30 metas réécrites à 155 caractères au plus (max mesuré 155), meta dédiée pour chaque fiche connecteur MCP (`metaDescription` dans `lib/connectors.ts`), `/docs` (redirection noindex) retiré du sitemap : 91 URLs, toutes en 200.
- [ ] Score Lighthouse SEO ≥ 70 % [id:: LP-SEO-002] [statut:: todo] [prio:: P1] (TF-LP-002 · C20)
- [ ] Lighthouse perf & a11y ≥ 90 [id:: LP-PERF-001] [statut:: todo] [prio:: P2] (TF-LP-005)

## Mesure & contenu
- [x] **Analytics respectueux RGPD (13/09/2026, v0.33.0)** [id:: LP-ANA-001] [statut:: done] [parite:: ok] [prio:: P2] [besoin-backend:: —] (TF-LP-003) — **PostHog en offre EU Cloud** (`eu.i.posthog.com`, aucune donnée hors UE), chargé **uniquement après consentement** (opt-in). Bandeau de consentement à catégories (`src/components/site/CookieConsent.tsx`, îlot `client:load`) : Nécessaires (exemptés) + Analytics (opt-in) ; module `src/lib/consent.ts` (miroir de l'app, choix versionné localStorage) + `src/lib/analytics.ts` (init PostHog gaté). Révocation par « Manage cookies » au footer (bouton statique → délégation `document.click` car le footer est SSR non hydraté). **Ancien plan Umami retiré** (`AudienceTracking.astro` supprimé). Vérifié live (astro dev) : rien avant consentement, egress EU confirmé après opt-in, opt-out à la révocation. Pages légales alignées (`legal/cookies.astro`, `legal/subprocessors.astro`, audit + registre RGPD). Fix CI au passage : job Lighthouse repassé en node 22 (Astro 7). Voir [[Audit_RGPD_Conformite]] + [[Registre_Traitements_RGPD]] (traitement n°9).
- [~] Contenu : pricing, CTA, proposition de valeur [id:: LP-CNT-001] [statut:: wip] [prio:: P2] (TF-LP-004) — pricing **aligné backend** (3 tiers, limites ws 2/10 + membres 5/50) 20/06 ; reste copy projets/integrations/storage non enforced
- [ ] i18n FR/EN (si cible bilingue) [id:: LP-I18N-001] [statut:: todo] [prio:: P3] (TF-LP-006)

## Design & tokens
- [x] **Grammaire de densité partagée avec l'app (20/09/2026)** [id:: LP-DESIGN-001] [statut:: done] [parite:: ok] [prio:: P2] (PROD-9.10) : tokens `--control-height-*` 32 / 36 / 40 (app : 28 / 32 / 36) + utilitaires `h-control*`, tailwind-merge étendu, kit ui + header + pricing tokenisés à valeur constante, formulaire de démo unifié à 40 ; deux redéclarations silencieuses corrigées dans `global.css` (`--radius`, 5 niveaux d'ombre : le flat de l'app redevient effectif) ; boutons pill inchangés ; visuels d'app recapturés (dashboard du hero, plan Auto-assign, menu Assignee actuel à la place de l'ancien panneau Smart Assign) ; image Docker de prod en Node 22. Vérifié par mesure DOM, lint et build prod. En prod depuis le 20/09 (PR #311, v0.37.0 ; `h-control*` présents dans le CSS de prod au 25/09). **MAJ 25/09/2026** : échelle de titres complétée par `t-h4` (titre de carte, 16 / 600) et `t-h5` (carte dense, 14 / 600), 48 titres convertis ; ponctuation sans tiret de liaison dans les titres, leads et metas. [ref:: landing-page/src/styles/global.css + landing-page/src/lib/utils.ts + .ai/design-grammar.md §7]

## Home & positionnement
- [x] **Hero repositionné sur le wedge « agents de code » (24/09/2026, v0.38.1)** [id:: LP-HERO-001] [statut:: done] [parite:: ok] [prio:: P1] : analyse concurrentielle de Dust (plateforme d'agents horizontale) ; le hero sonnait générique. Eyebrow « The governed layer above your coding agents », sous-titre qui nomme les agents (Claude Code, Cursor, Copilot) et la division du travail ; H1 « Describe the outcome. TaskForce runs the delivery. » conservé. PR #316. [ref:: landing-page/src/components/site/home/Hero.tsx]
- [x] **Passe de polish du site inspirée de relevanceai.com (25/09/2026, landing-v1.2.0, v0.39.0)** [id:: LP-HOME-001] [statut:: done] [parite:: ok] [prio:: P1] : audit mesuré d'abord (92 pages, 5 largeurs) puis 4 emprunts validés par le CEO. **Hero scindé** avec une île `HeroRuns.tsx` (`client:idle`) : table de runs animée, onglets par rôle (Engineering, Product, Operations, Client services), marquée « Illustrative », figée si reduced-motion. **Home 14,3 → 11,0 écrans** : Problem fusionné dans Before/After, Smart Assign dans « What ships today », mémoire dans « Why it's different », « The direction » sous « Who it's for », doublons retirés, 7 checkpoints de The run repliables (`<details>`). **Titres de section révélés au scroll** (`src/scripts/reveal-titles.ts`, plancher d'opacité 0,55 pour rester AA). **Mobile** : frise de The run verticale sous 640 px ([PC-048](../09-audits/Problemes_Connus.md)). 10 composants morts supprimés. Vérifié : lint (6 warnings préexistants), build 94 pages, sitemap 91 URLs en 200, marqueurs présents en prod. PR #317 → `dev`, PR #318 → `main`. Reste possible : Enterprise (1,9 écran) pour viser ~10, non validé. [ref:: landing-page/src/components/site/home/ + landing-page/src/pages/index.astro + .ai/design-grammar.md §7]

---
**Dernière mise à jour :** 25/09/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
