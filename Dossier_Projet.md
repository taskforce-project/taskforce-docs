<!--
Logo établissement (placeholder)
Logo projet (placeholder)
-->

# Dossier Projet

**Version :** 1.0  
**Date :** 17/01/2026  
**Auteur(s) :** [Nom Prénom]

---

[![Type: Dossier Projet](https://img.shields.io/badge/Type-Dossier%20Projet-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

---

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Business & Analyse de marché](./04_Etude_Faisabilite.md)
- [Documentation GitHub](https://github.com/...) <!-- À compléter -->
- [Repository GitHub](https://github.com/...)

---

**Tags :** `#gestion-de-projet` `#documentation` `#webapp` `#architecture` `#erp` `#saas`

---

## 1. Contexte et vision du projet

Ce document présente une synthèse du contexte et de la vision du projet. Pour une description fonctionnelle détaillée, se référer au [CdCF - Cahier des Charges Fonctionnel](./02_CdCF.md).

### Contexte général

Le projet **Taskforce** vise la conception et le développement d'une plateforme de gestion de projet professionnelle, positionnée comme un ERP modulaire et extensible. Au cœur de cette plateforme se trouve un système de répartition dynamique et automatisée des tâches au sein d'équipes de travail. L'objectif principal est d'optimiser l'allocation des missions en prenant en compte les compétences, la charge de travail, les disponibilités, les priorités et d'autres critères, afin d'améliorer la performance collective et de réduire les situations de surcharge individuelle.

**Vision produit** : Une plateforme modulaire composée d'un Core applicatif et de modules optionnels, permettant une extensibilité vers des usages réglementés (ex : LIMS, qualité). Cette architecture anticipe les contraintes réglementaires futures tout en offrant une scalabilité maximale.

### Problématique adressée

Dans un contexte professionnel moderne, les entreprises font face à une complexité croissante dans la gestion des ressources humaines et la coordination des équipes. La répartition manuelle des tâches devient très vite inefficace, source de déséquilibres de charge, de perte de productivité et de démotivation. Le projet répond à ce besoin en proposant un outil "intelligent" d’aide à la décision pour les managers, tout en offrant une visibilité partagée aux collaborateurs.

### Objectifs fonctionnels majeurs

L’application devra notamment permettre :

- L’assignation automatique des tâches en fonction des compétences, de la charge, des priorités et autre critères définis.
- Le suivi en temps réel de la charge de travail des collaborateurs.
- L’optimisation de l’utilisation des ressources humaines, en privilégiant les profils les plus adaptés tout en garantissant une répartition équitable.
- Une interface collaborative offrant une vue globale de l’état d’avancement des tâches.
- La détection et l’alerte en cas de surcharge, avec possibilité de réajustement.

### Démarche projet attendue

Le projet s’inscrit dans une approche structurée, comprenant :

- L’analyse des besoins et la définition des priorités et compétences.
- La conception de l’architecture logicielle et du modèle de données.
- Le développement des fonctionnalités cœur (gestion des compétences, assignation automatique).
- Une phase de tests auprès d’un groupe pilote.
- La mise en production et l’accompagnement des utilisateurs.

### Livrables et évaluation

Les livrables attendus incluent :

- Une documentation technique complète.
- Le code source de l’application.
- Un manuel utilisateur (collaborateurs et managers).
- Un support post-déploiement.

Le projet sera évalué sur sa capacité à automatiser et simplifier la gestion des tâches, prévenir les surcharges de travail et améliorer durablement la productivité des équipes, avec une logique d’amélioration continue basée sur les retours utilisateurs.

## 2. Présentation de l’équipe projet

### Composition et profil

Le projet est porté par un seul membre, assumant l’ensemble des fonctions stratégiques et opérationnelles :

- **Chef de projet** : pilotage global, gestion des plannings, arbitrage des priorités, suivi des livrables.
- **Architecte applicatif** : définition de l’architecture logicielle, choix des technologies, veille technique.
- **Développeur fullstack** : conception et réalisation des modules front-end et back-end, intégration continue.
- **DevOps** : gestion des environnements, automatisation des déploiements, supervision et observabilité.
- **Responsable qualité** : mise en place des tests, contrôle qualité, documentation.

### Compétences mobilisées

- Expertise en développement web (Java, Kotlin, Next.js, Astro, TypeScript)
- Maîtrise des architectures modulaires et des pratiques DevOps
- Connaissance des normes réglementaires (RGPD, WCAG, RGAA, ...)
- Gestion de projet agile et outils collaboratifs (GitHub, CI/CD)

### Organisation du travail

- Répartition du temps selon les phases projet
- Utilisation d’outils de gestion de tâches et de documentation
- Adaptation continue des priorités selon les jalons et les risques

_Image ici (organigramme mono-acteur)_

## 3. Organisation de l’équipe projet

### Structure organisationnelle

L’organisation repose sur la gestion multi-rôles du porteur de projet, avec une formalisation claire des responsabilités :

- **Responsabilités** : chaque rôle est défini avec ses missions principales (pilotage, conception, développement, qualité, déploiement).
- **Gestion des conflits de rôle** : priorisation des tâches selon l’urgence et l’importance, arbitrage par le porteur.
- **Suivi des responsabilités** : utilisation d’une matrice RACI pour clarifier les responsabilités et les livrables associés.

### Outils et méthodes

- Matrice RACI détaillée (voir [Matrice RACI](../05_Suivi_Agile_Roadmap.md))
- Tableaux de suivi des tâches et des jalons (utilisation de la matrice d'Eisenhower pour la priorisation)
- Documentation centralisée sur GitHub

_Image ici (schéma RACI)_

## 4. Méthodologie de projet employée

### Approche méthodologique

Le projet s’appuie sur une méthodologie agile adaptée au contexte mono-acteur :

- **Cycle de vie projet** : initialisation, conception, développement, tests, déploiement, bilan.
- **Itérations courtes (sprints)** : chaque sprint vise un livrable fonctionnel ou technique, avec une durée adaptée à la charge.
- **Gestion des tâches** : utilisation de GitHub Projects pour le suivi des tâches, des jalons, des issues et des User Stories avec les Milestones.
- **Gestion documentaire** : documentation continue sur GitHub, versionnement des documents et du code.
- **Gestion des versions** : branches Git dédiées par fonctionnalité ou lot, intégration continue via GitHub Actions.
- **Gestion des priorités** : arbitrage hebdomadaire selon l’avancement, les risques et les retours éventuels.

### Outils utilisés

- GitHub Projects (Issues, Milestones)
- Outils de CI/CD (GitHub Actions)

Pour plus de détails, consulter la [documentation GitHub](https://github.com/...).

_Image ici (cycle de vie projet)_

## 5. Veille technologique et moyens de veille

Synthèse :

- Veille active sur les technologies front-end (Next.js, Astro, Zustand, etc.) et back-end (Spring Boot, Kotlin)
- Suivi des évolutions réglementaires (RGPD, LIMS, SaaS)
- Utilisation de sources spécialisées, newsletters, et communautés open source

Pour la démarche complète, se référer au [CdCT](./03_CdCT.md) et à l’analyse de marché ([Business](./04_Etude_Faisabilite.md)).

## 6. Analyse fonctionnelle et objectifs (SMART)

Les objectifs du projet sont formalisés selon la méthode SMART (Spécifique, Mesurable, Atteignable, Réaliste, Temporellement défini) :

| Objectif                                        | Spécifique                                                                            | Mesurable                                                                                                                                               | Atteignable                                                     | Réaliste                                                        | Temporel       |
| ----------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | -------------- |
| **Développer le Core applicatif fonctionnel**   | Livrer un MVP avec gestion de projets, tâches, compétences et assignation automatique | - Authentification fonctionnelle (Keycloak)<br>- CRUD projets/tâches<br>- Algorithme d'assignation opérationnel<br>- Tests unitaires > 70% couverture   | Porteur unique avec stack maîtrisée (Spring Boot, Next.js)      | Architecture modulaire limitant la complexité initiale          | **31/01/2026** |
| **Assurer la conformité réglementaire de base** | Mettre en place les mécanismes RGPD et accessibilité WCAG 2.1 niveau AA               | - Consentement cookies<br>- Droit à l'oubli implémenté<br>- Tests accessibilité automatisés (axe-core)<br>- Score Lighthouse accessibility > 90         | Solutions éprouvées (design system accessible, librairies RGPD) | Obligation légale, frameworks supportant l'accessibilité        | **28/03/2026** |
| **Déployer l'application en production**        | Mettre en ligne l'application avec CI/CD et observabilité                             | - Pipeline GitHub Actions opérationnel<br>- Environnements dev/prod séparés<br>- Monitoring Grafana configuré<br>- Déploiement automatisé via Docker    | Infrastructure Docker maîtrisée, hébergement simple             | Pas de contraintes haute disponibilité initiales                | **26/04/2026** |
| **Implémenter le modèle SaaS multi-tenant**     | Proposer un plan gratuit et un plan payant avec limitation de fonctionnalités         | - Intégration Stripe fonctionnelle<br>- 2 plans tarifaires actifs<br>- Limitations par plan appliquées<br>- Workflow de souscription testé              | API Stripe bien documentée, nombreux exemples                   | Modèle économique SaaS standard                                 | **28/02/2026** |
| **Garantir la qualité et la maintenabilité**    | Obtenir une base de code propre, testée et documentée                                 | - Couverture tests > 70%<br>- 0 vulnérabilité critique (scan sécurité)<br>- Documentation API (OpenAPI/Swagger)<br>- Dette technique < 5% (SonarQube)   | Pratiques DevOps intégrées dès le départ                        | Tests et documentation continus évitent l'accumulation de dette | **20/06/2026** |
| **Préparer l'extensibilité modulaire**          | Architecturer le système pour permettre l'ajout de modules optionnels                 | - Interface de module définie<br>- Au moins 1 module externe activable<br>- Documentation architecture modulaire<br>- Gestion dépendances inter-modules | Architecture modulaire planifiée dès la conception              | Pas de nécessité d'implémentation complète au MVP               | **28/03/2026** |

Pour l'analyse fonctionnelle détaillée (cas d'usage, exigences, règles métier), se référer au [CdCF](./02_CdCF.md).

## 7. Choix technologiques – vue d’ensemble

Le choix des technologies s'appuie sur des critères stratégiques :

- **Évolutivité** : Support de l'architecture modulaire et de la scalabilité horizontale
- **Modularité** : Faciliter l'ajout de modules optionnels sans refonte majeure
- **Conformité** : Technologies compatibles avec les exigences réglementaires (RGPD, accessibilité, anticipation 21 CFR Part 11)
- **Écosystème** : Solutions open source éprouvées, communauté active, documentation abondante
- **Maîtrise** : Stack compatible avec l'expertise du porteur de projet (Java/Kotlin, TypeScript)
- **Performance** : Capacité à gérer une charge croissante avec des temps de réponse optimaux

**Stack retenue** : Spring Boot (Kotlin) + Next.js + PostgreSQL + Keycloak + Docker + GitHub Actions.

Pour la justification détaillée des choix techniques, l'architecture complète et les alternatives évaluées, consulter le [CdCT](./03_CdCT.md).

## 8. Modélisation du projet (PBS / WBS)

Synthèse de la décomposition du projet en modules et lots de travail. Pour la modélisation complète, se référer au [CdCF](./02_CdCF.md).

## 9. Modélisation UML – vue synthétique

Présentation synthétique des principaux diagrammes UML (cas d’utilisation, classes, séquence). Les diagrammes détaillés sont disponibles dans le [CdCF](./02_CdCF.md) et le [CdCT](./03_CdCT.md).

## 10. Modélisation des données

**Entités principales du modèle de données** :

- **Organisation** : structure multi-tenant, contient équipes et utilisateurs
- **Utilisateur** : collaborateurs, managers, administrateurs avec rôles et permissions
- **Projet** : entité centrale de gestion, contient tâches et jalons
- **Tâche** : unité de travail, assignée à un utilisateur, liée à des compétences requises
- **Compétence** : référentiel de compétences avec niveaux de maîtrise
- **Équipe** : regroupement d'utilisateurs, rattachée à une organisation
- **Abonnement** : gestion des plans tarifaires (gratuit/payant) via Stripe
- **Module** : modules optionnels activables par organisation

**Relations principales** : Organisation 1-N Équipes 1-N Utilisateurs 1-N Tâches, Tâches N-N Compétences.

Pour la modélisation complète (MCD, MLD, MPD, diagrammes de classes), consulter le [CdCT](./03_CdCT.md).

## 11. Identification des parties prenantes

Synthèse des parties prenantes (utilisateurs finaux, porteur de projet, parties académiques). La matrice RACI détaille les responsabilités (voir [Matrice RACI](../05_Suivi_Agile_Roadmap.md)).

## 12. Planification du projet

### Roadmap et calendrier prévisionnel

La planification du projet s’articule autour de jalons majeurs, chacun associé à des livrables et des critères de réussite :

| Phase                                 | Objectifs principaux                             | Livrables clés                       | Début    | Fin      |
| ------------------------------------- | ------------------------------------------------ | ------------------------------------ | -------- | -------- |
| Initialisation & cadrage              | Définir le périmètre, les besoins, les risques   | Dossier projet, CdCF, CdCT           | 04/11/25 | 15/11/25 |
| Conception fonctionnelle              | Formaliser les fonctionnalités, les modules      | CdCF, wireframes, PBS/WBS            | 18/11/25 | 29/11/25 |
| Conception technique                  | Définir l’architecture, les choix technologiques | CdCT, diagrammes UML, modèles        | 02/12/25 | 20/12/25 |
| Développement incrémental – Module 1  | Réaliser les modules, intégrer les services      | Code source, tests, documentation    | 02/01/26 | 31/01/26 |
| Développement incrémental – Module 2  | Réaliser les modules, intégrer les services      | Code source, tests, documentation    | 03/02/26 | 28/02/26 |
| Développement incrémental – Module 3  | Réaliser les modules, intégrer les services      | Code source, tests, documentation    | 03/03/26 | 28/03/26 |
| Tests et validation                   | Vérifier la conformité, la qualité               | Rapports de tests, documentation     | 31/03/26 | 26/04/26 |
| Déploiement & bilan                   | Mise en production, retour d’expérience          | Images Docker, bilan projet          | 28/04/26 | 23/05/26 |
| Itérations / Améliorations            | Optimisation, retours utilisateurs, UX           | Code amélioré, tests supplémentaires | 26/05/26 | 20/06/26 |
| Clôture projet / Documentation finale | Bilan complet, livrables consolidés              | Dossier final, CdCF/CdCT mis à jour  | 23/06/26 | 28/06/26 |

Module 1 : Partie Core de l'application
Module 2 : Outil de gestion de projet
Module 3 : Amélioration générale

- **Outils de suivi** : GitHub Projects pour la gestion des tâches, des jalons et du reporting.
- **Gestion des retards** : réévaluation des priorités et adaptation du calendrier en cas d’aléas.
- **Livrables intermédiaires** : validation à chaque étape avant passage au jalon suivant.

_Image ici (diagramme de Gantt ou roadmap)_

## 13. Analyse des risques

### Identification et gestion des risques

| Risque principal                                                             | Probabilité | Impact | Plan d’atténuation                                |
| ---------------------------------------------------------------------------- | ----------- | ------ | ------------------------------------------------- |
| Surcharge liée à la gestion multi-rôles                                      | Élevée      | Fort   | Planification rigoureuse, priorisation stricte    |
| Complexité technique (architecture modulaire, intégration de services tiers) | Moyenne     | Fort   | Prototypage, documentation, recours à la veille   |
| Contraintes réglementaires (RGPD et autre)                                   | Moyenne     | Fort   | Veille réglementaire, documentation, tests dédiés |
| Dépendance à des technologies open source                                    | Faible      | Moyen  | Sélection de solutions éprouvées, veille continue |
| Risques liés à la sécurité et à la conformité                                | Moyenne     | Fort   | Mise en place de tests, audits, documentation     |
| Retard sur les livrables                                                     | Moyenne     | Moyen  | Suivi hebdomadaire, adaptation du planning        |
| Perte de motivation / isolement                                              | Faible      | Moyen  | Suivi personnel, valorisation des jalons atteints |

- **Suivi des risques** : revue régulière à chaque étape du projet, adaptation des plans d’atténuation.
- **Documentation** : traçabilité des risques et des actions dans la documentation projet.

_Image ici (matrice des risques)_

## 14. Architecture logicielle – vue conceptuelle

Synthèse de l’architecture logicielle (core applicatif, modules, API, sécurité). Pour la description détaillée, se référer au [CdCT](./03_CdCT.md).

## 15. Infrastructure logicielle

Vue d’ensemble de l’infrastructure (Docker, CI/CD, environnements dev/prod, observabilité). Les détails sont disponibles dans le [CdCT](./03_CdCT.md).

## 16. Budgétisation du projet (vue synthétique)

### Modèle économique SaaS

**Plans tarifaires proposés** :

| Plan           | Prix          | Utilisateurs | Projets          | Modules                     | Support           | Cible                                     |
| -------------- | ------------- | ------------ | ---------------- | --------------------------- | ----------------- | ----------------------------------------- |
| **Gratuit**    | 0€/mois       | Jusqu'à 5    | 3 projets actifs | Core uniquement             | Community (email) | TPE, essai produit                        |
| **Pro**        | 29€/mois/user | Illimité     | Illimité         | Core + 2 modules optionnels | Email + chat      | PME, équipes projet                       |
| **Enterprise** | Sur devis     | Illimité     | Illimité         | Tous modules + custom       | Dédié + SLA       | Grandes entreprises, secteurs réglementés |

**Coûts d'infrastructure estimés (production)** :

- Hébergement : ~100-200€/mois (cloud, évolutif selon charge)
- Services tiers (Stripe, monitoring) : ~50€/mois
- Nom de domaine / SSL : ~50€/an
- **Total mensuel estimé** : ~150-250€

Pour la budgétisation détaillée (coûts de développement, ROI prévisionnel, analyse de rentabilité), consulter l'analyse [Business](./04_Etude_Faisabilite.md).

## 17. Wireframes, maquettage et accessibilité

**Approche de conception UX/UI** :

- **Wireframes basse fidélité** : Définition des parcours utilisateurs et arborescence de navigation
- **Design system** : Utilisation de shadcn-ui + Tailwind CSS pour cohérence visuelle
- **Accessibilité** : Conformité WCAG 2.1 niveau AA, tests automatisés et manuels
- **Responsive design** : Support mobile, tablette, desktop

**Parcours utilisateurs clés** :

1. Inscription et souscription à un plan
2. Création de projet et ajout de tâches
3. Consultation de la charge de travail
4. Activation de modules optionnels

Pour les wireframes détaillés et les maquettes fonctionnelles, consulter le [CdCF - Section 11](./02_CdCF.md#11-parcours-utilisateurs-et-maquettes-fonctionnelles).

Pour l'implémentation technique du design system, l'optimisation des performances front-end et les tests d'accessibilité, consulter le [CdCT](./03_CdCT.md).

## 18. Normes et conformité

**Normes et référentiels applicables au MVP** :

- **RGPD** (protection des données personnelles) : consentement, droit à l'oubli, portabilité, privacy by design
- **WCAG 2.1 niveau AA** (accessibilité web) : interfaces accessibles, navigation clavier, lecteurs d'écran
- **RGAA** (référentiel français d'accessibilité) : conformité avec les obligations légales françaises
- **CNIL** : conformité avec les recommandations de la Commission Nationale Informatique et Libertés
- **OWASP Top 10** : protection contre les vulnérabilités web critiques
- **ISO 27001** (sécurité de l'information) : bonnes pratiques de sécurité applicative

**Anticipation réglementaire (environnements réglementés)** :

- **21 CFR Part 11** (FDA - Electronic Records) : réglementation pour signatures électroniques et intégrité des données
- **GAMP 5** (Good Automated Manufacturing Practice) : validation des systèmes informatisés en pharma

**Approche** : L'architecture modulaire de type ERP permet d'**anticiper** ces contraintes réglementaires sans les implémenter au MVP. La séparation Core / Modules optionnels facilite l'ajout futur de modules conformes (ex : LIMS) avec traçabilité renforcée, audit trails et validation selon ces référentiels. Cette approche garantit une **scalabilité maximale** vers des secteurs réglementés.

Pour la conformité technique détaillée, l'implémentation des mécanismes de sécurité et la stratégie d'anticipation réglementaire complète, se référer au [CdCT - Section 12 et 13](./03_CdCT.md).

## 19. Bilan et perspectives du projet

Le projet pose les bases d’une plateforme ERP modulaire, adaptée à des contextes professionnels exigeants. Les perspectives incluent l’extension fonctionnelle, l’ouverture à de nouveaux marchés et l’intégration de modules réglementés.

---

_Fin du Dossier Projet – Phase de documentation_
