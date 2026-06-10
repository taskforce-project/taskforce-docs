---
type: memoire-rncp
bloc: 1
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc1, conception, modelisation]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 1 — Concevoir et modéliser une application

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 1](https://img.shields.io/badge/Bloc-1%20Conception-blue?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture technique](../03-architecture/Architecture.md) · [CdCF](../01-projet/01_CdCF.md) · [CdCT](../01-projet/02_CdCT.md)

**Tags :** `#memoire` `#bloc1` `#conception` `#modelisation`

<p class="lead">
Ce bloc couvre l'analyse de la demande, la préparation du projet (agile, environnement de dev) et la
conception/modélisation (wireframes, STB, modèle de données, architecture logicielle, RGPD, veille).
Compétences C1 à C12, livrables E1 à E10.
</p>

> **Gabarit par compétence** : énoncé officiel → livrable(s) → critères de la grille (à cocher) → preuve
> dans TaskForce → espace de rédaction. Cocher un critère uniquement quand la preuve est intégrée au dossier.

## Table des matières

1. [Activité — Analyse de la demande & CdCF](#activité--analyse-de-la-demande--cdcf) (C1, C2)
2. [Activité — Préparation du déploiement projet](#activité--préparation-du-déploiement-projet) (C3, C4, C5)
3. [Activité — Spécifications, conception, modélisation](#activité--spécifications-conception-modélisation) (C6–C11)
4. [Activité — Veille](#activité--veille) (C12)

---

## Activité — Analyse de la demande & CdCF

### C1 — Analyser la demande initiale du client
**Livrable :** E1 — présentation de synthèse et reformulation de la demande (public utilisateur, besoins de référencement, de sécurité, autres contraintes).
**Critères d'évaluation :**
- [ ] Le besoin général, la culture, le contexte et les enjeux du client sont identifiés fidèlement.
- [ ] La problématique d'usage est formulée de façon claire et précise.
- [ ] Le cas échéant, les sujets d'actualisation d'une application préexistante sont listés.

**Preuve dans TaskForce :** [CDC initial](../01-projet/01_CdCF.md), [Dossier Projet](../01-projet/Dossier_Projet.md). Reformuler le besoin TaskForce (répartition dynamique des tâches : compétences × charge × disponibilités).

> _À rédiger :_ <!-- reformulation de la demande, problématique d'usage, acteurs (Collaborateur, Manager, Responsable de projet) -->

### C2 — Apporter son expertise technique (conseil sur le CdCF)
**Livrable :** E1, E3.
**Critères d'évaluation :**
- [ ] Une distance critique est prise (interrogations, préconisations, propositions d'innovation : faisabilité technique, UX).
- [ ] Des opportunités sont détectées (éco-responsabilité, inclusion).

**Preuve dans TaskForce :** choix d'écarter PHP/MySQL du CDC initial au profit de Spring Boot/PostgreSQL/Next.js ; ajout de l'IA (Smart Assign Groq), du temps réel (STOMP), du SSO Keycloak.

> _À rédiger :_ <!-- préconisations et innovations vs CDC initial, arguments -->

## Activité — Préparation du déploiement projet

### C3 — Identifier les caractéristiques du projet (planification & budget)
**Livrable :** E2 — planification prévisionnelle + ébauche de budget.
**Critères d'évaluation :**
- [ ] Public utilisateur, besoins de référencement et de sécurité analysés et explicités exhaustivement.
- [ ] Délais, budget et contraintes → planning + budget prévisionnels réalistes (interactions et charges des acteurs).
- [ ] Adéquation au cadre réglementaire et législatif ; anticipation de l'évolution des normes.
- [ ] Possibilités d'aménagement inclusif et d'écoconception analysées.

**Preuve dans TaskForce :** [Dossier Projet](../01-projet/Dossier_Projet.md), [Étude business](../01-projet/Etude_business.md), diagrammes `assets/diagrammes/` (WBS, PBS, Gantt RACI, SMART, risques).

> _À rédiger :_ <!-- planning (Gantt), budget, analyse réglementaire (RGPD), écoconception -->

### C4 — Travailler en mode agile
**Livrable :** E5 (note justifiant la méthode agile), E6 (trame de compte rendu d'activité).
**Critères d'évaluation :**
- [ ] Méthode agile (XP, Scrum, DSDM, ASD…) avec cycle adapté aux contraintes et à la dimension du projet.
- [ ] Trame de compte rendu d'activité correspondant à la méthode, opérationnelle.

**Preuve dans TaskForce :** [Git Workflow](../04-engineering/git-workflow/README.md) (branches, PR, versioning), et **l'application elle-même** (gestion d'Issues, Cycles/sprints, labels) qui matérialise Scrum.

> _À rédiger :_ <!-- méthode retenue + justification, cérémonies, trame de CR -->

### C5 — Mettre en œuvre un environnement de développement collaboratif
**Livrable :** E4 — procédure complète de mise en œuvre de l'environnement.
**Critères d'évaluation :**
- [ ] Outils/technologies adaptés aux contraintes et à la dimension du projet.
- [ ] La procédure démontre la maîtrise du SCM **Git**, d'un **IDE** du marché et de la **virtualisation** sur poste local.

**Preuve dans TaskForce :** [Quickstart](../06-infra/quickstart/README.md), [GHCR](../06-infra/docker/GHCR_USAGE.md), Docker Compose (`docker-compose.dev.yml`), Git workflow. Statut : ✅ preuve solide.

> _À rédiger :_ <!-- capture procédure : clone, .env, docker compose up, IDE, debug 5005 -->

## Activité — Spécifications, conception, modélisation

### C6 — Concevoir des maquettes « wireframe »
**Livrable :** E7 — présentation de maquette wireframe.
**Critères d'évaluation :**
- [ ] La maquette correspond précisément à une vue souhaitée dans la note de cadrage.
- [ ] Conforme aux standards de la profession, notamment en matière d'UX.

**Preuve dans TaskForce :** `assets/maquettes/` (dashboard, login, register, modules projets/utilisateurs, paramètres, profil, landing).

> _À rédiger :_ <!-- wireframes annotés + correspondance aux vues -->

### C7 — Traduire les besoins en spécifications techniques (STB)
**Livrable :** E8 — dossier de conception.
**Critères d'évaluation :**
- [ ] Outils/technologies adaptés ; dossier de conception complet.
- [ ] Les cas d'utilisation couvrent l'ensemble des exigences du CdCF.
- [ ] Les classes d'analyse et de conception sont définies et cohérentes.

**Preuve dans TaskForce :** [CdCT](../01-projet/02_CdCT.md), [Architecture §4](../03-architecture/Architecture.md), [Modules](../03-architecture/Modules.md).

> _À rédiger :_ <!-- diagrammes de cas d'usage, diagramme de classes -->

### C8 — Modéliser l'application
**Livrable :** E8.
**Critères d'évaluation :**
- [ ] Structure, associations, relations et contraintes décrites selon des normes de modélisation reconnues, modèle adapté.
- [ ] Sert à établir des règles de gestion des données efficaces et à minimiser la redondance.

**Preuve dans TaskForce :** [Architecture §6](../03-architecture/Architecture.md) (ERD), [Modules §4](../03-architecture/Modules.md) (migrations V1–V35), `backend/tf-api/.../core/model`.

> _À rédiger :_ <!-- MCD/diagramme entité-association, règles de gestion -->

### C9 — Concevoir l'architecture des bases de données (persistance)
**Livrable :** E8.
**Critères d'évaluation :**
- [ ] Décrit la gestion des données (collecte → transformation → distribution → consommation) et leur circulation.
- [ ] Décrit comment l'architecture facilite le besoin métier.
- [ ] Décrit le cycle de vie des données **et la couche de persistance** (sauvegarde/restauration).

**Preuve dans TaskForce :** PostgreSQL 18 + pgvector, Flyway, [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) pour sauvegarde/restauration. Statut : ✅.

> _À rédiger :_ <!-- schéma flux de données, stratégie de persistance et backup -->

### C10 — Déterminer l'architecture logicielle
**Livrable :** E8.
**Critères d'évaluation :**
- [ ] Cas d'utilisation couvrant les exigences du CdC initial.
- [ ] Classes d'analyse/conception cohérentes.
- [ ] Architecture logicielle conforme aux usages de la profession et adaptée au cas d'étude.
- [ ] Dossier de spécifications structuré et documenté conformément à la démarche choisie.

**Preuve dans TaskForce :** [Architecture §4](../03-architecture/Architecture.md) (couches `shared/core/modules`, multi-tenant), [Modules](../03-architecture/Modules.md). Statut : ✅.

> _À rédiger :_ <!-- diagramme d'architecture, justification des choix (modulaire, layered) -->

### C11 — Conformité légale (CNIL / RGPD)
**Livrable :** E9 — audit de conformité RGPD (⚠️ cas professionnel **hors** projet fil rouge).
**Critères d'évaluation :**
- [ ] Outil de recueil du consentement cookies proposé, caractéristiques techniques détaillées.
- [ ] Vue « politique de confidentialité et traitement des données personnelles » prévue.
- [ ] Formulaire de demande d'accès aux données personnelles + traitement proposé.
- [ ] Processus de double opt-in proposé pour les traitements collectant des données personnelles.

**Preuve dans TaskForce :** ⬜ à produire (cas pro fourni par l'école). Pistes côté TaskForce : Keycloak (gestion des identités), données collaborateurs (compétences/charge) → analyse RGPD.

> _À rédiger :_ <!-- audit RGPD du site fourni + mapping sur TaskForce -->

## Activité — Veille

### C12 — Proposer des solutions alternatives/innovantes (veille)
**Livrable :** E10 — méthodologie de veille technologique.
**Critères d'évaluation :**
- [ ] Méthodologie cohérente, adaptée et appliquée aux exigences et au contexte de l'application.
- [ ] Détaille la fréquence et les méthodes de recherche de sources, de compilation et d'actualisation.

**Preuve dans TaskForce :** choix technos récentes (Next.js 16, React 19, Spring Boot 4, Groq LLM, pgvector) = résultat d'une veille. ⬜ formaliser la méthodologie.

> _À rédiger :_ <!-- sources, fréquence, outils de veille, exemples d'application au projet -->

---

> **Note Brain OS** — Preuves techniques dans [Architecture](../03-architecture/Architecture.md) /
> [Modules](../03-architecture/Modules.md). Chantiers ouverts (RGPD, veille) suivis dans le [hub mémoire](./README.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
