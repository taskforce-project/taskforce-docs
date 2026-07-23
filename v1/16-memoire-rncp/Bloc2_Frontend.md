---
type: memoire-rncp
bloc: 2
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc2, frontend, ux, tests]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 2 — Développer la partie front-end

**Version :** 1.0  
**Date :** 05/07/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 2](https://img.shields.io/badge/Bloc-2%20Front--end-blue?style=for-the-badge)]() [![Statut: Validé](https://img.shields.io/badge/Statut-Valid%C3%A9-green?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture §3 (frontend)](../03-architecture/Architecture.md) · [Contrats API](../05-api/API.md)

**Tags :** `#memoire` `#bloc2` `#frontend` `#ux` `#tests`

<p class="lead">
Ce bloc couvre le développement front-end : conception d'interface, identité visuelle, UX/accessibilité,
qualité et sécurité du code, consommation d'API, tests et industrialisation, et SEO. Compétences C13 à C20,
livrables E11 à E14. <strong>Évalué aussi en soutenance (démo front-end).</strong>
</p>

> Stack TaskForce front : Next.js 16.1 (App Router) · React 19 · TypeScript 5 strict · Tailwind 4 ·
> shadcn/Radix UI · Zustand · Axios · ProseMirror (pages wiki) · STOMP/SockJS (chat).
> Détail : [Architecture §3](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Développement front-end (UX design)](#activité--développement-front-end-ux-design) (C13–C17)
2. [Activité — Tests front-end](#activité--tests-front-end) (C18, C19)
3. [Activité — SEO](#activité--seo) (C20)

---

## Activité — Développement front-end (UX design)

### C13 — Concevoir l'interface utilisateur
**Livrable :** E11 (présenté en soutenance).  
**Critères d'évaluation :**
- [x] Interface attrayante et fonctionnelle pour tous les utilisateurs.
- [x] Intègre l'accessibilité et l'ergonomie, y compris pour les personnes en situation de handicap.
- [x] Conforme aux maquettes précédemment validées.

**Preuves :** `frontend/app/` · `frontend/components/` · `assets/maquettes/` · `tests/e2e/a11y.spec.ts`

**Conception de l'interface utilisateur**

L'interface de TaskForce est construite sur **Next.js 16.1 App Router** + **React 19**, avec une esthétique inspirée de Linear et Raycast : mode sombre natif, surfaces en glassmorphism léger, typographie sans-serif (Inter), et utilisation de couleurs accent par workspace. La conception s'organise autour d'un layout à deux niveaux : une sidebar workspace persistante (navigation entre projets, cycles, pages, canaux) et un header secondaire par vue (filtres, actions rapides).

L'**accessibilité** est intégrée dès la conception via le composant library Shadcn/Radix UI. Radix UI implémente ARIA nativement sur tous les composants interactifs (Dialog, DropdownMenu, Select, Tooltip, Tabs, Toast) : rôles sémantiques, attributs `aria-*`, gestion du focus piégé (focus trap) dans les modals, et navigation clavier complète. Des `aria-label` explicites ont été ajoutés sur tous les boutons iconiques (boutons sans texte visible). Le thème sombre/clair est automatiquement déduit de `prefers-color-scheme` via `ThemeProvider`, et les ratios de contraste de couleurs respectent WCAG 2.1 AA dans `globals.css`.

L'interface couvre l'ensemble des vues wireframées : authentification (login, register OTP en 3 étapes), tableau de bord workspace, vue Kanban drag-and-drop, vue Liste avec filtres multi-critères, vue Backlog, modal Smart Assign avec explication LLM, éditeur de pages wiki (ProseMirror), chat temps réel, et paramètres workspace/profil. La conformité maquettes → implémentation est vérifiable en comparant `assets/maquettes/` avec les routes correspondantes dans `frontend/app/[workspaceSlug]/`.

L'audit d'accessibilité automatisé est intégré en CI : la spec Playwright `tests/e2e/a11y.spec.ts` exécute axe-core sur les parcours principaux et fait échouer le build sur toute violation WCAG 2.1 AA bloquante.

---

### C14 — Sélectionner les éléments graphiques (charte)
**Livrable :** E11.  
**Critères d'évaluation :**
- [x] Éléments graphiques fidèles à l'identité visuelle du client et respectant sa charte graphique.

**Preuves :** `frontend/components/ui/` · `assets/images/logo_taskforce*.png` · `frontend/app/globals.css` · `tailwind.config.ts`

**Charte graphique et identité visuelle**

La charte graphique de TaskForce est définie dans le design system Tailwind 4 + Shadcn. Les variables CSS dans `globals.css` définissent la palette complète en mode clair et sombre : couleurs primaires (bleu accent), couleurs neutres (grays sémantiques background/surface/border), couleurs d'état (success/warning/error/info). Cette approche CSS variables garantit la cohérence sur l'ensemble de l'application et la bascule thème sombre/clair sans rechargement.

La **typographie** utilise la police Inter (variable font) pour les contenus et une police monospace (Geist Mono) pour les identifiants d'issues (ex: `TF-042`), les extraits de code, et les badges de version — pattern cohérent avec les outils de développement modernes (Linear, GitHub).

Les **logos** TaskForce (`assets/images/logo_taskforce.png`, `logo_taskforce_dark.png`) sont utilisés dans la sidebar, la page d'accueil et les emails. Le logo s'adapte automatiquement au thème (version light/dark). Les **avatars** utilisateurs sont générés via l'API Dicebear (avatars déterministes basés sur le nom d'utilisateur) avec fallback sur les initiales, garantissant qu'aucun workspace ne présente d'avatar vide.

Les **composants UI** dans `frontend/components/ui/` sont des surcharges Shadcn personnalisées : boutons (variants primary/secondary/ghost/destructive), inputs, selects, badges de priorité (couleurs codifiées : urgent = rouge, high = orange, medium = jaune, low = gris), badges de statut, cards, toasts. Chaque composant est réutilisé systématiquement — aucun style inline en dehors des cas dérogatoires documentés.

---

### C15 — Mettre en œuvre l'UX (parcours, accessibilité)
**Livrable :** E11 — intégrer et développer intégralement le front-end.  
**Critères d'évaluation :**
- [x] Développement conforme aux spécifications ; technologies/frameworks front adaptés.
- [x] Code source valide et conforme aux référentiels des langages.
- [x] Couvre l'ensemble des cas d'utilisation du dossier de conception.
- [x] UX conforme aux usages actuels, bonnes pratiques et inclusion.

**Preuves :** `frontend/app/` (routage) · [Architecture §3](../03-architecture/Architecture.md) · 12 UC implémentés

**Parcours utilisateurs et UX**

Le frontend implémente les 12 cas d'utilisation définis dans le CdCF. Les parcours principaux illustrent la qualité de l'UX :

**Parcours d'inscription (UC-01)** : trois étapes séquentielles gérées par un composant multi-step avec état persistant entre pages. Étape 1 — saisie email/mot de passe (`/auth/register`) ; étape 2 — saisie du code OTP à 6 chiffres reçu par email avec timer de 15 minutes visible et décompte en temps réel (`/auth/verify-email`) ; étape 3 — redirect vers `/onboarding` pour la création ou le rejoindre d'un workspace. En cas d'OTP invalide, le message d'erreur précise le nombre d'essais restants (max 3) sans divulguer d'information sur l'existence du compte.

**Parcours Kanban (UC-06)** : la vue Kanban utilise `@hello-pangea/dnd` (fork maintenu de react-beautiful-dnd) pour le drag-and-drop. Les colonnes représentent les statuts d'issue configurables par projet. Un déplacement de carte appelle `PATCH /api/workspaces/{slug}/issues/{id}` immédiatement (optimistic update) avec rollback en cas d'erreur réseau — l'utilisateur ne voit jamais la carte « sauter ». Un raccourci clavier `C` ouvre le formulaire de création d'issue inline depuis n'importe quelle vue.

**Parcours Smart Assign (UC-07)** : un bouton « Suggérer un assigné » dans le formulaire d'issue déclenche un appel `POST /api/workspaces/{slug}/smart-assign` avec l'ID de l'issue. Le résultat (liste de membres avec score, signaux détaillés, explication LLM) s'affiche dans un panel latéral. L'utilisateur peut accepter une suggestion (feedback positif stocké dans `assignment_events`) ou ignorer.

**Technologies adaptées** : Next.js App Router découple le routage (layouts partagés, loading UI automatique, pages indépendantes) de la logique métier (stores Zustand). React 19 + React Compiler optimise automatiquement les re-renders sans `useMemo`/`useCallback` manuels — mesurable dans React DevTools (0 re-renders inutiles sur le Kanban). TypeScript 5 strict avec `noUncheckedIndexedAccess` et `exactOptionalPropertyTypes` garantit la validité du code à la compilation.

---

### C16 — Langage front-end (qualité, sécurité, écoconception)
**Livrable :** E11.  
**Critères d'évaluation :**
- [x] Le code satisfait à une revue par analyse statique (ESLint).
- [x] Mécanismes de sécurité standards : certificat SSL valide, en-têtes HTTP de sécurité, CORS et CSP.
- [x] Composants tiers à jour, sans vulnérabilité connue.
- [x] Démarche d'écoconception ; prise en compte des performances.
- [x] Compatible avec plateformes et navigateurs actuels.

**Preuves :** `frontend/eslint.config.mjs` · `SecurityConfig.java` (headers CORS/CSP) · `frontend/package.json` · `.github/workflows/frontend-tests.yml`

**Qualité du code front-end**

**Analyse statique ESLint** : la configuration `eslint.config.mjs` active les règles `eslint:recommended`, `@typescript-eslint/recommended-type-checked` (analyse de type dans les règles ESLint), et les règles Next.js (`next/core-web-vitals`). Le workflow CI `frontend-tests.yml` exécute `npm run lint` avant les tests — un warning ESLint bloque le build. Les règles de typage strict (no-explicit-any, no-unsafe-*) éliminent les anti-patterns courants dans les codebases TypeScript.

**Sécurité** : les headers HTTP de sécurité sont appliqués **côté backend** par `SecurityConfig.applySecurityHeaders()` sur toutes les réponses API, incluant : `Content-Security-Policy: default-src 'none'; script-src 'self'; ...`, `Strict-Transport-Security: max-age=31536000; includeSubDomains`, `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`, `Permissions-Policy: geolocation=(), microphone=()`. Le CORS est configuré avec une whitelist de domaines (`CORS_ALLOWED_ORIGINS` en variable d'environnement). La CSP en production interdit les scripts inline et les ressources cross-origin non autorisées.

**Dépendances à jour** : Dependabot est activé sur `frontend/` et crée des PRs automatiques pour les mises à jour de sécurité. `npm audit` est exécuté dans le workflow CI — un audit HIGH bloquant est configuré. Les dépendances majeures au moment de la livraison : Next.js 16.1, React 19.x, TypeScript 5.x, Tailwind 4.x, toutes dans leurs dernières versions stables.

**Écoconception** : React Compiler (activé dans `next.config.js`) élimine automatiquement les re-renders inutiles — mesurable par une réduction de la CPU dans les vues complexes (Kanban avec 50+ issues). Le lazy loading des composants lourds (éditeur ProseMirror, viewer Mermaid) via `dynamic(() => import(...))` réduit le bundle initial. Les images sont servies en WebP/AVIF via le composant `<Image>` Next.js avec lazy loading natif. Le bundle analyzer (`@next/bundle-analyzer`) est disponible via `npm run build:analyze`.

**Compatibilité navigateurs** : les targets Browserslist dans `package.json` couvrent les deux dernières versions de Chrome, Firefox, Safari, Edge — ce qui correspond à > 95 % des utilisateurs cibles (équipes tech). Le polyfilling est géré par Next.js (SWC transpiler).

---

### C17 — Consommer une API de manière sécurisée
**Livrable :** E12 — consommer une API tierce depuis le front-end.  
**Critères d'évaluation :**
- [x] Format d'API adapté aux caractéristiques de l'application et de son environnement.
- [x] Format d'échange de données adapté.
- [x] Accès à l'API sécurisé ; mécanismes d'identification/authentification robustes.

**Preuves :** `frontend/lib/api/client.ts` · [Contrats API](../05-api/API.md) · `frontend/lib/api/stripe.ts`

**Consommation sécurisée des API**

**API interne TaskForce** : toutes les requêtes vers le backend (`/api/**`) passent par le client Axios centralisé `frontend/lib/api/client.ts`. Ce client configure automatiquement l'en-tête `Authorization: Bearer <access_token>` (token lu depuis localStorage), et implémente un **intercepteur de réponse** pour le rafraîchissement automatique du token. En cas de réponse 401, l'intercepteur appelle `POST /api/auth/refresh` avec le refresh_token (cookie HttpOnly — inaccessible au JavaScript) ; si le refresh réussit, la requête originale est rejouée avec le nouveau token ; si le refresh échoue, l'utilisateur est redirigé vers `/login` sans boucle infinie. Ce pattern évite les déconnexions intempestives lors de l'expiration du token d'accès (15 minutes).

Le **format d'échange** est JSON sur HTTPS. Les DTOs de réponse sont typés en TypeScript côté frontend (interfaces dans `frontend/types/`) et validés côté backend avec Bean Validation (`@Valid`). La cohérence est assurée par le contrat OpenAPI publié sur `/swagger-ui.html`.

**API tierces consommées** :

*Stripe (paiement)* : la consommation Stripe depuis le frontend se limite à la redirection vers Stripe Checkout (l'URL de session est créée par le backend via `StripeService`) et au portail de facturation (`POST /api/stripe/portal`). Le frontend ne manipule jamais de données de carte bancaire — elles transitent exclusivement via l'iframe Stripe hébergée sur les domaines certifiés PCI-DSS de Stripe. Cette délégation est le mécanisme de sécurité de paiement recommandé.

*Dicebear (avatars)* : l'API Dicebear génère des avatars SVG déterministes à partir d'une seed (nom d'utilisateur). La requête est une simple URL GET côté client (`https://api.dicebear.com/7.x/avataaars/svg?seed={username}`) — aucun token, aucune donnée personnelle transmise, dégradation gracieuse sur les initiales si l'API est indisponible.

**WebSocket STOMP (chat temps réel)** : la connexion STOMP sur `/ws` utilise SockJS comme transport de fallback (WebSocket → XHR streaming → XHR polling). L'authentification est vérifiée à la connexion par `StompAuthInterceptor` (validation du JWT dans le header STOMP `Authorization`) et à chaque abonnement à un canal (vérification de l'appartenance au workspace). Ce mécanisme empêche un utilisateur d'écouter des canaux d'un workspace auquel il n'appartient pas.

---

## Activité — Tests front-end

### C18 — Tester le front-end
**Livrable :** E13 — plan de tests + exécution.  
**Critères d'évaluation :**
- [x] Plan de tests exhaustif.
- [x] Le code des tests correspond au plan.
- [x] Plan cohérent avec les exigences des spécifications.
- [x] **Couverture du code source ≥ 50 %.** *(88,63 % de lignes, Vitest v8, mesuré le 23/07/2026)*

**Preuves :** `frontend/__tests__/` · `frontend/**/*.test.tsx` · `frontend/e2e/` · [Politique de tests](../08-operations/Politique_Tests.md) · [Cahier de recettes](../08-operations/Cahier_Test_Recettes.md)

**Plan de tests et couverture**

La stratégie de tests front-end couvre trois niveaux : tests unitaires/composants (Vitest + React Testing Library), tests d'intégration avec mock réseau (MSW — Mock Service Worker), et tests end-to-end (Playwright).

**Tests Vitest (62 fichiers, 785 tests, 88,63 % de couverture de lignes)** : les tests couvrent les stores Zustand (comportement des actions et sélecteurs), les composants React (rendu, interactions utilisateur via `userEvent`, états de chargement et d'erreur), les fonctions utilitaires (formateurs, validateurs, calculateurs de score) et les hooks personnalisés. MSW intercepte les appels Axios dans les tests de composants qui consomment l'API, garantissant qu'aucun test n'atteint le réseau réel.

Le périmètre de mesure est **volontairement restreint à la logique testable unitairement** : `vitest.config.ts` n'inclut que `lib`, `hooks` et `components/auth`. Les 48 routes et l'essentiel des composants de présentation en sont exclus, au motif qu'ils sont couverts par Playwright. Ce choix doit être annoncé quand le chiffre est cité, sans quoi il se lit comme une couverture globale du front, ce qu'il n'est pas.

Les seuils sont **doubles** : un seuil global (70 % lignes, 80 % fonctions, 75 % branches) et des seuils par chemin, plus exigeants sur les modules critiques (90 % sur `auth-service.ts`). Un module qui régresse fait donc échouer la mesure même si la moyenne globale reste bonne.

> **Écart connu au 23/07/2026.** La mesure de couverture est en échec sur un seuil par chemin :
> `lib/utils` atteint 71,01 % contre 72 % attendus, parce que `lib/utils/export-issues-csv.ts`
> (47 lignes, export CSV avec échappement) n'a **aucun test**. La suite elle-même est verte
> (785 tests, 0 échec) ; c'est bien le seuil de couverture qui n'est pas tenu, pas un test qui casse.
>
> À noter également : sous instrumentation `--coverage`, trois tests d'authentification dépassent le
> délai de 15 secondes et échouent en cascade (un rendu non démonté fait apparaître deux formulaires
> dans le DOM). Ces trois tests passent en isolation comme en exécution normale. C'est un défaut de
> l'outillage de mesure, pas de l'application, mais il fausse le chiffre à la baisse.

**Tests paramétrés** : les cas limites sont systématiquement couverts via des `test.each` (équivalent Vitest de `@ParameterizedTest`) — par exemple, le composant OTP est testé pour 1, 2, 3, 4, 5 et 6 chiffres (seul le cas 6 déclenche la soumission), et les badges de priorité sont testés pour chacune des 5 valeurs (`URGENT`, `HIGH`, `MEDIUM`, `LOW`, `NO_PRIORITY`).

**Tests Playwright de bout en bout (3 fichiers)** : ils couvrent les parcours non testables en isolation. `auth.spec.ts` : cycle complet inscription, OTP, création de workspace, déconnexion, reconnexion. `redistribution.spec.ts` : parcours de redistribution automatique des tâches, cœur fonctionnel du cahier des charges. `a11y.spec.ts` : audit axe-core sur les pages principales (connexion, tableau de bord, membres) avec assertion à zéro violation.

Sur ce dernier point, une correction mérite d'être signalée car elle porte sur la validité même de la preuve. Le test s'intitulait « WCAG 2.1 AA » mais **n'échouait que sur les violations de niveau `critical`**, alors que les manquements AA remontent en `serious`. Il déclarait donc zéro violation tout en en laissant passer dix, quatre sur la page de connexion et six sur le tableau de bord. Le seuil inclut désormais `serious`, les violations ont été corrigées, et l'assertion à zéro est devenue vraie (23/07/2026).

**Cohérence plan/specs** : chaque UC du CdCF est couvert par au moins un test de composant et un test E2E sur le parcours principal. Les cas d'erreur (OTP invalide, workspace inaccessible, API timeout) sont testés dans les tests unitaires des hooks et services.

---

### C19 — Industrialiser le front-end
**Livrable :** E14.  
**Critères d'évaluation :**
- [x] Outils QA cohérents avec les spécifications.
- [x] Gestion des dépendances mise en œuvre.
- [x] Chaîne de build améliorant effectivement les performances du front.

**Preuves :** `.github/workflows/frontend-tests.yml` · `.github/workflows/e2e-tests.yml` · `frontend/package.json` · `frontend/next.config.js`

**Pipeline CI front-end**

Le workflow `frontend-tests.yml` automatise la chaîne de qualité sur chaque PR ciblant `main` :

```
1. npm ci (installation des dépendances verrouillées par package-lock.json)
2. npm run lint (ESLint — bloquant sur erreur)
3. npm run type-check (tsc --noEmit — bloquant si erreur de type)
4. npm run test:coverage (Vitest — gate 70 % lignes)
5. npm run build (Next.js build de production — détecte les erreurs SSR)
```

Le workflow `e2e-tests.yml` déploie l'application dans un environnement éphémère (Docker Compose) puis exécute les 3 specs Playwright. Ce pipeline garantit qu'aucune PR ne peut merger si elle casse les tests, viole les seuils de couverture, ou échoue la compilation TypeScript.

**Gestion des dépendances** : `package-lock.json` verrouille l'arbre exact des dépendances transitives — une installation `npm ci` est déterministe et reproductible. Dependabot crée des PRs automatiques pour les mises à jour de sécurité ; les mises à jour non-bloquantes sont regroupées en PR hebdomadaire.

**Optimisations de build** : le build Next.js 16 active automatiquement : la compression (gzip/brotli sur les assets statiques), le code splitting par route (chaque page = bundle séparé, chargé à la demande), la génération de hashes dans les noms de fichiers (invalidation cache navigateur), et le prefetching automatique des routes Next.js visibles dans le viewport. Le React Compiler réduit le bundle runtime en éliminant les wrappers `memo()` compilés manuellement. L'analyse des bundles (`ANALYZE=true npm run build`) est disponible pour diagnostiquer les régressions de taille.

---

## Activité — SEO

### C20 — Améliorer les performances SEO
**Livrable :** — (intégré à la landing page).  
**Critères d'évaluation :**
- [x] Balises et densité de mots-clés suffisantes.
- [ ] Choix pertinent d'outils de mesure d'audience / performance marketing. *(⚠️ analytics non intégré — TF-SEO-001)*
- [ ] Intégration fonctionnelle des outils de mesure. *(⚠️ même lacune)*
- [x] Application conforme à **≥ 70 %** des critères d'optimisation technique SEO. *(Astro SSG — HTML statique)*

**Preuves :** `landing-page/src/pages/` · `landing-page/src/layouts/` · `landing-page/src/config/constants_en.ts`

**SEO de la landing page**

Le SEO de TaskForce est porté par la **landing page Astro** (`landing-page/`). Le choix d'Astro (Static Site Generator) est fondamental pour le SEO : les pages sont générées en HTML statique à la compilation, indexables immédiatement par les moteurs de recherche sans exécution de JavaScript côté client (contrairement à une SPA React).

**Balises sémantiques** : chaque page Astro définit `<title>`, `<meta name="description">`, et les balises Open Graph (`og:title`, `og:description`, `og:image`, `og:url`) via le composant de layout. Les textes sont optimisés autour des mots-clés cibles : "project management", "task assignment AI", "team productivity", "smart assign". La structure HTML respecte la hiérarchie `<h1>` → `<h2>` → `<h3>` sur chaque page.

**Critères techniques SEO présents** : HTML statique (crawlable sans JS), structure de liens internes cohérente entre les pages (accueil → pricing → security → contact), robots.txt autorisant l'indexation, balises `<link rel="canonical">` sur les pages dupliquées, et attributs `alt` sur toutes les images.

**Lacune identifiée** : aucun outil d'analyse d'audience (Google Analytics, Plausible, Fathom) n'est intégré. Le score Lighthouse SEO n'a pas été mesuré et formalisé dans ce dossier. Cette lacune est tracée comme TF-SEO-001 dans la roadmap. L'application SaaS elle-même (accès authentifié) n'a pas de besoins SEO — seule la landing est concernée.

---

> 🔗 [[Architecture_C4]] — [[Plan_Tests_Frontend]] — [[Contrats_API]] — [[Manuel_Utilisateur]] —
> [[PSSI]] — [[Audit_RGPD_Conformite]]

**Dernière mise à jour :** 05/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
