---
type: memoire-rncp
bloc: 2
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc2, frontend, ux, tests]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 2 — Développer la partie front-end

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 2](https://img.shields.io/badge/Bloc-2%20Front--end-blue?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]()

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

> Stack TaskForce front : Next.js 16 (App Router) · React 19 · TypeScript 5 strict · Tailwind 4 ·
> shadcn/Radix · Zustand · Axios · TipTap · STOMP. Détail : [Architecture §3](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Développement front-end (UX design)](#activité--développement-front-end-ux-design) (C13–C17)
2. [Activité — Tests front-end](#activité--tests-front-end) (C18, C19)
3. [Activité — SEO](#activité--seo) (C20)

---

## Activité — Développement front-end (UX design)

### C13 — Concevoir l'interface utilisateur
**Livrable :** E11 (présenté en soutenance).
**Critères d'évaluation :**
- [ ] Interface attrayante et fonctionnelle pour tous les utilisateurs.
- [ ] Intègre l'accessibilité et l'ergonomie, y compris pour les personnes en situation de handicap.
- [ ] Conforme aux maquettes précédemment validées.

**Preuve dans TaskForce :** `frontend/app` + `frontend/components`, refonte UI (esthétique Raycast, glassmorphism, dark/light), `assets/maquettes/`.

> _À rédiger :_ <!-- captures écrans vs maquettes, choix d'accessibilité (Radix = ARIA), thèmes -->

### C14 — Sélectionner les éléments graphiques (charte)
**Livrable :** E11.
**Critères d'évaluation :**
- [ ] Éléments graphiques fidèles à l'identité visuelle du client et respectant sa charte graphique.

**Preuve dans TaskForce :** `frontend/components/ui`, logos `assets/images/logo_taskforce*.png`, design system Tailwind/shadcn.

> _À rédiger :_ <!-- charte graphique, palette, typographie, composants -->

### C15 — Mettre en œuvre l'UX (parcours, accessibilité)
**Livrable :** E11 — intégrer et développer intégralement le front-end.
**Critères d'évaluation :**
- [ ] Développement conforme aux spécifications ; technologies/frameworks front adaptés.
- [ ] Code source valide et conforme aux référentiels des langages.
- [ ] Couvre l'ensemble des cas d'utilisation du dossier de conception.
- [ ] UX conforme aux usages actuels, bonnes pratiques et inclusion.

**Preuve dans TaskForce :** App Router, parcours auth 3 étapes, navigation workspace, [Architecture §3](../03-architecture/Architecture.md).

> _À rédiger :_ <!-- parcours utilisateurs clés (login → workspace → projet → issue), optimisations -->

### C16 — Langage front-end (qualité, sécurité, écoconception)
**Livrable :** E11.
**Critères d'évaluation :**
- [ ] Le code satisfait à une revue par analyse statique (ESLint).
- [ ] Mécanismes de sécurité standards : certificat SSL valide, en-têtes HTTP de sécurité, **CORS** et **CSP**.
- [ ] Composants tiers à jour, sans vulnérabilité connue.
- [ ] Démarche d'écoconception ; prise en compte des performances.
- [ ] Compatible avec plateformes et navigateurs actuels.

**Preuve dans TaskForce :** ESLint (`eslint.config.mjs`), CORS [Architecture §7](../03-architecture/Architecture.md), TS strict. ⚠️ Vérifier en-têtes HTTP sécurité / CSP (nginx prod), audit vulnérabilités (`npm audit`).

> _À rédiger :_ <!-- rapport ESLint, en-têtes sécurité, npm audit, Lighthouse perf -->

### C17 — Consommer une API de manière sécurisée
**Livrable :** E12 — consommer une API tierce depuis le front-end.
**Critères d'évaluation :**
- [ ] Format d'API adapté aux caractéristiques de l'application et de son environnement.
- [ ] Format d'échange de données adapté.
- [ ] Accès à l'API sécurisé ; mécanismes d'identification/authentification robustes.

**Preuve dans TaskForce :** `frontend/lib/api/client.ts` (Axios, bearer JWT, refresh), [Contrats API](../05-api/API.md). API tierce : Stripe (paiement), Dicebear (avatars).

> _À rédiger :_ <!-- consommation API REST sécurisée (JWT), exemple d'intégration tierce -->

## Activité — Tests front-end

### C18 — Tester le front-end
**Livrable :** E13 — plan de tests + exécution.
**Critères d'évaluation :**
- [ ] Plan de tests exhaustif.
- [ ] Le code des tests correspond au plan.
- [ ] Plan cohérent avec les exigences des spécifications.
- [ ] **Couverture du code source ≥ 50 %.**

**Preuve dans TaskForce :** `frontend/__tests__` + `*.test.tsx` (Vitest + RTL + MSW). ⚠️ **Mesurer et atteindre 50 %** (voir [PC-010](../09-audits/Problemes_Connus.md)).

> _À rédiger :_ <!-- plan de tests, rapport de couverture Vitest -->

### C19 — Industrialiser le front-end
**Livrable :** E14.
**Critères d'évaluation :**
- [ ] Outils QA cohérents avec les spécifications.
- [ ] Gestion des dépendances mise en œuvre.
- [ ] Chaîne de build améliorant effectivement les performances du front.

**Preuve dans TaskForce :** `.github/workflows/frontend-tests.yml`, build Next.js, `package.json`. Statut : ✅.

> _À rédiger :_ <!-- pipeline CI front, gestion deps, optimisations build -->

## Activité — SEO

### C20 — Améliorer les performances SEO
**Livrable :** — (intégré au front / landing).
**Critères d'évaluation :**
- [ ] Balises et densité de mots-clés suffisantes.
- [ ] Choix pertinent d'outils de mesure d'audience / performance marketing.
- [ ] Intégration fonctionnelle des outils de mesure.
- [ ] Application conforme à **≥ 70 %** des critères d'optimisation technique SEO.

**Preuve dans TaskForce :** `landing-page/` (Astro, orienté SEO/SSG). ⚠️ à mesurer (Lighthouse SEO), ajouter analytics. Statut : ⬜.

> _À rédiger :_ <!-- métadonnées, sitemap, Open Graph, score Lighthouse SEO, analytics -->

---

> **Note Brain OS** — Détails front dans [Architecture §3](../03-architecture/Architecture.md) et
> [Contrats API](../05-api/API.md). Lacunes (tests ≥50 %, SEO ≥70 %) suivies dans
> [Problèmes connus](../09-audits/Problemes_Connus.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
