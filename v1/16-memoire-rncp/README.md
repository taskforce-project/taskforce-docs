---
type: memoire-rncp
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, dossier-validation, dfs, brain-os]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# 🎓 Mémoire RNCP — Dossier de Validation

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]() [![Titre: Développeur Full Stack](https://img.shields.io/badge/Titre-D%C3%A9veloppeur%20Full%20Stack-blue?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Bloc 1 — Conception & modélisation](./Bloc1_Conception_Modelisation.md)
- [Bloc 2 — Front-end](./Bloc2_Frontend.md)
- [Bloc 3 — Back-end](./Bloc3_Backend.md)
- [Bloc 4 — Déploiement & production](./Bloc4_Deploiement_Production.md)
- [CDC initial](../01-projet/Dossier_Projet.md) · [Architecture technique](../03-architecture/Architecture.md)

**Tags :** `#memoire` `#rncp` `#dossier-validation` `#dfs`

<p class="lead">
Ce dossier est le <strong>mémoire de validation</strong> du titre <em>Développeur Full Stack</em> (RNCP,
Metz Numeric School 2025-2026), adossé au projet fil rouge <strong>TaskForce</strong>. Sa table des
matières <strong>colle volontairement à la structure du référentiel</strong> (blocs → activités →
compétences C1–C32), comme recommandé, afin que chaque compétence évaluée soit traçable et qu'aucun
critère de la grille ne soit oublié.
</p>

> **Comment l'utiliser** — La [matrice de couverture](#3-matrice-de-couverture-des-32-compétences) est ta
> checklist maître : tant qu'une ligne n'est pas ✅, le dossier n'est pas complet. Chaque compétence renvoie
> à sa section détaillée (critères + preuves) et à l'emplacement de la preuve dans TaskForce (via le
> [Brain OS](../../Brain_OS.md)).

## Table des matières

1. [Modalités d'évaluation](#1-modalités-dévaluation)
2. [Livrables attendus (E1–E29)](#2-livrables-attendus-e1e29)
3. [Matrice de couverture des 32 compétences](#3-matrice-de-couverture-des-32-compétences)
4. [Conventions de rédaction](#4-conventions-de-rédaction)

---

## 1. Modalités d'évaluation

<p class="lead">
Le titre se valide par trois modalités complémentaires. Le présent dossier alimente principalement la
première et appuie la deuxième.
</p>

| Modalité | Description | Blocs concernés |
| -------- | ----------- | --------------- |
| **Dossier de validation** | Ensemble des livrables (E1–E29) du projet fil rouge + réflexion personnelle (solutions originales, analyse, préconisations). Remis au jury, évalué à l'écrit et en soutenance. | 1 à 4 |
| **Soutenance** | Démonstration de l'application : partie front-end (bloc 2) + partie back-end (bloc 3). Présentation de synthèse PDF + prototype/démo/code. | 2 et 3 |
| **Mise en situation simulée** | Maintenance écrite et surveillée d'une application existante (bugs, failles, composants obsolètes). | 4 (+ C11 cas pro RGPD) |

<blockquote class="important">
<strong>Recommandation du référentiel :</strong> coller la table des matières à la structure en blocs et
activités. Ce dossier la respecte ; la <a href="#3-matrice-de-couverture-des-32-compétences">matrice</a>
joue en plus le rôle de « tableau d'équivalences » compétence ↔ partie du dossier.
</blockquote>

## 2. Livrables attendus (E1–E29)

Synthèse des livrables exigés par le référentiel, regroupés par bloc. Détail et critères dans chaque fiche bloc.

- **Bloc 1 :** E1 reformulation de la demande · E2 planification + budget prévisionnels · E3 note de
  préconisations techniques · E4 procédure d'environnement de dev · E5 note justifiant la méthode agile ·
  E6 trame de compte rendu d'activité · E7 maquette wireframe · E8 dossier de conception (cas d'usage,
  classes, MCD, archi logicielle) · E9 audit RGPD (cas pro hors fil rouge) · E10 méthodologie de veille.
- **Bloc 2 :** E11 développement intégral du front-end · E12 consommation d'une API tierce · E13 plan de
  tests front + exécution · E14 industrialisation front (QA, dépendances, build).
- **Bloc 3 :** E15 couche de persistance · E16 développement intégral du back-end · E17 système de
  paiement + monétisation · E18 API sécurisée · E19 plan de tests back · E20 industrialisation back.
- **Bloc 4 :** E21 choix d'hébergement cloud + diagramme de déploiement · E22 environnement de production
  sécurisé · E23 nom de domaine + DNS + certificats · E24 déploiement automatisé · E25 journalisation/audit ·
  E26 supervision + alertes · E27 détection de bugs + correctifs · E28 détection de failles + correctifs ·
  E29 génération de doc + changelog.

## 3. Matrice de couverture des 32 compétences

<p class="lead">
Légende statut : ✅ couvert (preuve prête) · 🟡 partiel (preuve existe, à formaliser) · ⬜ à produire.
Le statut initial ci-dessous est une <strong>estimation</strong> basée sur l'état du code (Brain OS) ; à
ajuster au fil de la rédaction.
</p>

### Bloc 1 — Concevoir et modéliser

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C1 | Analyser la demande initiale | E1 | [CDC](../01-projet/01_CdCF.md), [Dossier Projet](../01-projet/Dossier_Projet.md) | 🟡 |
| C2 | Conseil / expertise sur le CdCF | E1, E3 | [CdCF](../01-projet/01_CdCF.md) | 🟡 |
| C3 | Caractéristiques projet (public, SEO, sécu, délais, budget) | E2 | [Dossier Projet](../01-projet/Dossier_Projet.md), [Étude business](../01-projet/Etude_business.md) | 🟡 |
| C4 | Travailler en agile | E5, E6 | [Git Workflow](../04-engineering/git-workflow/README.md), app TaskForce (Issues/Cycles) | 🟡 |
| C5 | Environnement de dev collaboratif | E4 | [Quickstart](../06-infra/quickstart/README.md), [GHCR](../06-infra/docker/GHCR_USAGE.md) | ✅ |
| C6 | Maquettes wireframe | E7 | `assets/maquettes/` | 🟡 |
| C7 | STB → dossier de conception | E8 | [Architecture §4](../03-architecture/Architecture.md), [CdCT](../01-projet/02_CdCT.md) | 🟡 |
| C8 | Modélisation (entité-association, classes) | E8 | [Architecture §6](../03-architecture/Architecture.md), [Modules §4](../03-architecture/Modules.md) | 🟡 |
| C9 | Architecture des bases de données / persistance | E8 | [Architecture §6](../03-architecture/Architecture.md) (Flyway V1–V35) | ✅ |
| C10 | Architecture logicielle | E8 | [Architecture §4](../03-architecture/Architecture.md) | ✅ |
| C11 | Conformité RGPD / CNIL | E9 | ⚠️ cas pro hors fil rouge — à produire | ⬜ |
| C12 | Veille technologique | E10 | à rédiger (Groq, Next 16, Spring Boot 4…) | ⬜ |

### Bloc 2 — Front-end

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C13 | Concevoir l'interface utilisateur | E11 | `frontend/` (Next.js), `assets/maquettes/` | 🟡 |
| C14 | Éléments graphiques / charte | E11 | `frontend/components/ui`, logos `assets/images/` | 🟡 |
| C15 | Mettre en œuvre l'UX (parcours, accessibilité) | E11 | `frontend/app`, [Architecture §3](../03-architecture/Architecture.md) | 🟡 |
| C16 | Langage front (qualité, sécurité, écoconception) | E11 | headers/CORS/CSP — [Architecture §7](../03-architecture/Architecture.md) | 🟡 |
| C17 | Consommer une API de façon sécurisée | E12 | [API](../05-api/API.md), `frontend/lib/api/client.ts` | 🟡 |
| C18 | Tester le front-end (couverture ≥ 50 %) | E13 | `frontend/__tests__` (Vitest) — ⚠️ couverture à vérifier | 🟡 |
| C19 | Industrialiser le front-end | E14 | `.github/workflows/frontend-tests.yml` | ✅ |
| C20 | Performances SEO (≥ 70 %) | — | `landing-page/` (Astro) — ⚠️ à mesurer | ⬜ |

### Bloc 3 — Back-end

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C21 | Couche de persistance (sécurité en profondeur) | E15 | [Architecture §6](../03-architecture/Architecture.md), JPA/Flyway | ✅ |
| C22 | Langage back (qualité, sécurité, écoconception) | E16 | [Architecture §4](../03-architecture/Architecture.md) (Spring Boot 4) | ✅ |
| C23 | Système de paiement + monétisation | E17 | Stripe — ⚠️ webhooks stubés ([PC-005](../09-audits/Problemes_Connus.md)) | 🟡 |
| C24 | Développer une API sécurisée | E18 | [API](../05-api/API.md), `SecurityConfig`, Swagger/OpenAPI | 🟡 |
| C25 | Tester le back-end (couverture ≥ 50 %) | E19 | `backend/tf-api/src/test` — ⚠️ couverture à compléter | 🟡 |
| C26 | Industrialiser le back-end | E20 | `.github/workflows/backend-tests.yml`, `release.yml` | ✅ |

### Bloc 4 — Déploiement & production

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C27 | Documentation technique + base de connaissances | E29 | **Ce Brain OS**, [technique/](../03-architecture/Architecture.md), Swagger | 🟡 |
| C28 | Administration (domaine, DNS, certificats, sécurité) | E23 | `nginx/`, prod compose — ⚠️ à documenter | ⬜ |
| C29 | Sélectionner une plateforme d'hébergement | E21 | diagramme de déploiement — à produire | ⬜ |
| C30 | Administrer des services d'hébergement (cloud/conteneur) | E22 | `docker-compose.prod.yml`, Keycloak, bastion — ⚠️ à formaliser | 🟡 |
| C31 | Déploiement automatisé (DevOps / CI-CD) | E24 | `.github/workflows/release.yml`, `version-management.yml`, [GHCR](../06-infra/docker/GHCR_USAGE.md) | 🟡 |
| C32 | Supervision (sondes, alertes, journalisation) | E25–E28 | SigNoz (`docker-compose.tools.yml`), actuator/prometheus | 🟡 |

## 4. Conventions de rédaction

<p class="lead">
Chaque fiche bloc suit le même gabarit : par compétence, on trouve l'énoncé officiel, le(s) livrable(s)
attendu(s), les <strong>critères de la grille en cases à cocher</strong>, le pointeur vers la preuve dans
TaskForce, puis un espace de rédaction à compléter.
</p>

Règles : rédaction **narrative** (paragraphes, pas de listes sèches) conformément au
[template](../../templates/Template_Doc_Technique.md) ; chaque affirmation technique renvoyée vers une preuve
(capture, lien de code, lien Brain OS) ; cocher un critère uniquement quand la preuve est intégrée au dossier.

---

> **Note Brain OS** — Ce mémoire s'appuie sur les documents techniques vérifiés du
> [Brain OS](../../Brain_OS.md). Les écarts connus (tests, RGPD, SEO, déploiement) sont des **chantiers de
> rédaction**, tracés dans [Problèmes connus](../09-audits/Problemes_Connus.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
