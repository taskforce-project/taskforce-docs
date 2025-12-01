# Liste complète des documents pour le projet TaskForce (agile solo style scrum)

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="assets/images/logo_taskforce_light.png" alt="TaskForce Logo" width="200"/>
    <img src="assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire

1. [Phase de cadrage & étude du besoin](#1-phase-de-cadrage--étude-du-besoin)
2. [Phase agile : planification et gestion du backlog](#2-phase-agile--planification-et-gestion-du-backlog)
3. [Phase de conception technique et développement](#3-phase-de-conception-technique-et-développement)
4. [Phase de test & validation](#4-phase-de-test--validation)
5. [Phase de déploiement & exploitation](#5-phase-de-déploiement--exploitation)
6. [Phase de suivi, pilotage et reporting](#6-phase-de-suivi-pilotage-et-reporting)
7. [Phase de clôture et soutenance](#7-phase-de-clôture-et-soutenance)

## 1. Phase de cadrage & étude du besoin

**Objectif :** définir la vision, les objectifs et les limites du projet.
Période : mois 1 à 2

| Document                                                 | Contenu                                                                                                       | Format conseillé |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------- |
| **1.1. Dossier projet**                                  | Objectif global, contexte, acteurs, enjeux, périmètre, livrables, planning macro, budget estimé (même fictif) | PDF et Markdown  |
| **1.2. Cahier des charges fonctionnel (CDCF)**           | Fonctions principales, utilisateurs, use cases, besoins exprimés en langage métier, critères d’acceptation    | PDF et Markdown  |
| **1.3. Cahier des charges technique (CDCT)**             | Architecture, stack technologique, contraintes techniques, sécurité, performance, intégrations externes       | PDF et Markdown  |
| **1.4. Spécifications fonctionnelles détaillées (SFD)**  | Description détaillée de chaque fonctionnalité, règles métier, workflow, maquettes d’écran                    | PDF et Markdown  |
| **1.5. Analyse de l’existant / benchmark concurrentiel** | Analyse de Trello, Jira, etc. (forces/faiblesses)                                                             | PDF et Markdown  |
| **1.6. Étude de faisabilité**                            | Faisabilité technique, humaine, temporelle, financière                                                        | PDF et Markdown  |
| **1.7. Modèle de données (MCD / MLD)**                   | Schéma des entités et relations                                                                               | Draw.io          |
| **1.8. Diagrammes UML**                                  | Cas d’utilisation, séquence, activité, classe, déploiement                                                    | Draw.io          |
| **1.9. User personas & parcours utilisateur**            | Profils types, motivations, scénarios d’usage                                                                 | PDF et Markdown  |

## 2. Phase agile : planification et gestion du backlog

**Objectif :** cadrer l’évolution du produit sur le long terme.
Période : en continu (dès le mois 2)

| Document                                 | Contenu                                                            | Format conseillé |
| ---------------------------------------- | ------------------------------------------------------------------ | ---------------- |
| **2.1. Vision produit (Product Vision)** | Pourquoi, pour qui, quoi, comment, succès attendu                  | PDF et Markdown  |
| **2.2. Product Backlog**                 | Liste complète des user stories + priorisation                     | Github Project   |
| **2.3. User stories**                    | Forme “En tant que … je veux … afin de …” + critères d’acceptation | Github Project   |
| **2.4. Roadmap produit**                 | Phases du projet, jalons, MVP → V1 → V2                            | Timeline Graph   |
| **2.5. Release plan / Sprint plan**      | Objectifs par itération, contenu du sprint                         | Sprint board     |
| **2.6. Burndown charts & KPI**           | Suivi de la vélocité, avancement                                   | Graph            |

## 3. Phase de conception technique et développement

**Objectif :** préparer et structurer le code proprement.

| Document                                                 | Contenu                                        | Format conseillé           |
| -------------------------------------------------------- | ---------------------------------------------- | -------------------------- |
| **3.1. Architecture logicielle (macro & microservices)** | Schéma des modules, API, flux, protocoles      | UML / Diag. d’architecture |
| **3.2. Contrat d’API / Documentation API**               | Swagger/OpenAPI, endpoints, payloads           | JSON + SwaggerUI           |
| **3.3. Convention de code / normes**                     | Formatage, nommage, branches Git, tests        | Markdown                   |
| **3.4. Plan de gestion du code source**                  | Organisation Git (branches, merge policy)      | README interne             |
| **3.5. Guide d’installation / configuration**            | Déploiement local, dépendances, environnements | README.md                  |
| **3.6. Journal de développement / changelog**            | Suivi des évolutions de version                | CHANGELOG.md               |

## 4. Phase de test & validation

**Objectif :** garantir la qualité et la conformité du produit.

| Document                                       | Contenu                                            | Format conseillé                  |
| ---------------------------------------------- | -------------------------------------------------- | --------------------------------- |
| **4.1. Plan de test**                          | Objectif, stratégie de test, outils utilisés       | Document formel                   |
| **4.2. Scénarios / cas de test**               | Pour chaque user story : inputs, outputs attendus  | Tableau Excel / Notion            |
| **4.3. Rapport de test / anomalies**           | Liste des bugs, statut, corrections                | Issue Tracker                     |
| **4.4. Tests unitaires & coverage report**     | Rapport de couverture automatisé                   | Généré par outil CI               |
| **4.5. Recette fonctionnelle / PV de recette** | Validation des fonctionnalités par rapport au CDCF | Document signé (même fictivement) |

## 5. Phase de déploiement & exploitation

**Objectif :** mettre l’app en ligne et assurer la continuité.

| Document                                      | Contenu                                                | Format conseillé       |
| --------------------------------------------- | ------------------------------------------------------ | ---------------------- |
| **5.1. Dossier d’exploitation / déploiement** | Environnements, scripts, pipeline CI/CD                | README + YAML pipeline |
| **5.2. Plan de mise en production (PMP)**     | Étapes, rollback, vérifications                        | Document PDF           |
| **5.3. PCA (Plan de Continuité d’Activité)**  | Procédures pour maintenir le service en cas d’incident | PDF                    |
| **5.4. PRA (Plan de Reprise d’Activité)**     | Scénarios de panne, restauration, sauvegardes          | PDF                    |
| **5.5. Politique de sécurité**                | Authentification, RGPD, gestion des droits, logs       | Document technique     |
| **5.6. Manuel utilisateur / aide en ligne**   | Guide pour les utilisateurs finaux                     | Doc / Notion / wiki    |

## 6. Phase de suivi, pilotage et reporting

**Objectif :** assurer le suivi et la communication projet.

| Document                                          | Contenu                                      | Format             |
| ------------------------------------------------- | -------------------------------------------- | ------------------ |
| **6.1. Journal de bord projet**                   | Synthèse des avancées par semaine/sprint     | PDF / Notion       |
| **6.2. Tableau de bord projet**                   | KPI, avancement, charge, vélocité            | Tableau / Notion   |
| **6.3. Compte-rendu de sprint review / rétro**    | Ce qui a marché, améliorations               | Notes              |
| **6.4. Rapport intermédiaire (milieu de projet)** | État d’avancement, difficultés, perspectives | PDF / présentation |

## 7. Phase de clôture et soutenance

**Objectif :** finaliser et évaluer le projet.

| Document                                        | Contenu                                                               | Format                      |
| ----------------------------------------------- | --------------------------------------------------------------------- | --------------------------- |
| **7.1. Rapport final / dossier projet complet** | Synthèse du projet, livrables, architecture, tests, résultats, bilans | PDF (dossier de soutenance) |
| **7.2. Présentation (pitch / soutenance)**      | Slides avec vision, démo, résultats, perspectives                     | PowerPoint / PDF            |
| **7.3. Guide d’évolution / maintenance**        | Comment faire évoluer ou maintenir le projet                          | Markdown                    |
| **7.4. Bilan personnel / rétrospective**        | Compétences acquises, points forts/faibles                            | Annexe                      |

## Bonus : Documents “vivants” à maintenir tout au long du projet

- README principal (à jour en permanence)
- Journal de bord / changelog dev
- Backlog produit
- Roadmap et KPI
- Doc API (auto-générée)





| Livrable / Cahier                    | Objectif                               | Graphes / Diagrammes associés                 |
| ------------------------------------ | -------------------------------------- | --------------------------------------------- |
| 📘 **Cahier des charges**            | Cadrage du projet                      | SMART, PBS, WBS, OBS, Risques, Planning macro |
| 📗 **Spécifications fonctionnelles** | Décrire ce que fait le produit         | Use Case, BPMN, Wireframes                    |
| 📙 **Spécifications techniques**     | Décrire comment c’est fait             | Architecture, MCD, Séquence, Stack            |
| 📒 **Plan de gestion de projet**     | Organiser le travail et les ressources | WBS, Gantt, PERT, RACI, OBS                   |
| 📕 **Cahier de tests**               | Valider la qualité                     | Plan de test, tableau, screenshots            |
| 📔 **Documentation utilisateur**     | Guider l’utilisation                   | Screens, navigation, API                      |
| 📓 **Rapport / soutenance**          | Synthétiser le tout                    | Résumé visuel + résultats                     |
