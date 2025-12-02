# Dossier Projet

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Contexte du projet](#1-contexte-du-projet)
- [2. Objectifs du projet](#2-objectifs-du-projet)
- [3. Parties prenantes](#3-parties-prenantes)
- [4. Périmètre Fonctionnel et Technique](#4-périmètre-fonctionnel-et-technique)
- [5. Organisation du Projet (WBS)](#5-organisation-du-projet-wbs)
- [6. Contraintes et Risques](#6-contraintes-et-risques)
- [7. Livrables attendus](#7-livrables-attendus)
- [8. Planning prévisionnel](#8-planning-prévisionnel)

---

## 1. Contexte du projet

### 1.1 Présentation
Le projet **TaskForce** consiste à créer une application innovante permettant de répartir automatiquement et dynamiquement les tâches au sein d'une équipe. Ce système intelligent se base sur les compétences, la charge de travail actuelle et les disponibilités de chaque collaborateur pour optimiser la productivité.

### 1.2 Problématique
Les entreprises modernes évoluent dans un environnement où la gestion des ressources humaines et la répartition des tâches sont critiques. Les managers peinent souvent à :
- Assurer une charge de travail équilibrée.
- Affecter les tâches aux profils les plus compétents.
- Anticiper les surcharges avant qu'elles ne deviennent critiques.

TaskForce vise à automatiser ce processus pour garantir que chaque collaborateur travaille sur les missions les plus adaptées, réduisant ainsi le stress et augmentant l'efficacité globale.

---

## 2. Objectifs du projet

L'application devra répondre aux objectifs stratégiques suivants, définis selon la méthode SMART :

![Objectifs SMART](../assets/diagrammes/SMART-taskforce.drawio.png)

1.  **Répartition automatique des tâches** : Algorithme d'assignation basé sur les compétences et la disponibilité.
2.  **Suivi en temps réel** : Monitoring de la charge de travail et ajustements dynamiques.
3.  **Optimisation des ressources** : Adéquation parfaite entre tâche et compétence.
4.  **Bien-être au travail** : Détection et prévention des surcharges (burn-out).
5.  **Interface collaborative** : Vue unifiée pour managers et équipes.

---

## 3. Parties prenantes

L'organisation du projet s'articule autour des acteurs suivants :

![Organigramme](../assets/diagrammes/Organigramme-taskforce.drawio.png)

*   **Maitrise d'Ouvrage (MOA)** : Metz Numeric School (MNS)
*   **Assistance à Maitrise d'Ouvrage (AMOA)** : Cédric Brasseur
*   **Maitrise d'Oeuvre (MOE) / Chef de Projet** : Pierre MICHEL
*   **Utilisateurs Finaux** :
    *   **Collaborateurs** : Reçoivent les tâches et mettent à jour leur avancement.
    *   **Managers** : Supervisent, ajustent les priorités et reçoivent les alertes.
    *   **Responsables de Projet** : Définissent les allocations initiales et les compétences requises.

---

## 4. Périmètre Fonctionnel et Technique

### 4.1 Product Breakdown Structure (PBS)
Le découpage fonctionnel du produit est le suivant :

![PBS](../assets/diagrammes/PBS-taskforce.drawio.png)

### 4.2 Fonctionnalités Clés
*   **Assignation Intelligente (IA)** : Moteur de règles et d'IA pour le dispatching des tâches.
*   **Gestion des Profils** : Cartographie des compétences et niveaux d'expérience.
*   **Tableau de Bord** : Vues Kanban, Gantt et indicateurs de charge.
*   **Système d'Alertes** : Notifications en cas de surcharge, retard ou blocage.
*   **Reporting** : Rapports de performance et d'utilisation des ressources.

### 4.3 Stack Technique
Le choix technologique s'oriente vers une architecture robuste et évolutive, capable de fonctionner en mode web et potentiellement hors-ligne (client lourd) à terme.

*   **Back-end** : Java Spring Boot (Robustesse, Sécurité, Architecture Hexagonale).
*   **Front-end** : Next.js (React), TypeScript, TailwindCSS (Interface moderne et réactive).
*   **Base de données** : PostgreSQL (Fiabilité, Gestion de données complexes).
*   **Intelligence Artificielle** : Python (Micro-service pour les algorithmes de classification et de summarization).
*   **Infrastructure** : Docker (Conteneurisation).

---

## 5. Organisation du Projet (WBS)

Le projet est découpé en plusieurs phases majeures pour assurer un suivi rigoureux :

![WBS](../assets/diagrammes/WBS-taskforce.drawio.png)

1.  **Cadrage & Planification** : Recueil des besoins, définition de l'architecture.
2.  **Conception** : UI/UX, Modélisation de la base de données (MCD/MLD).
3.  **Réalisation (Itérations)** : Développement Back-end, Front-end et intégration IA.
4.  **Tests & Recette** : Tests unitaires, d'intégration et validation utilisateur.
5.  **Déploiement & Bilan** : Mise en production, formation et documentation.

---

## 6. Contraintes et Risques

Une analyse des risques a été effectuée pour anticiper les points de blocage potentiels :

![Matrice des Risques](../assets/diagrammes/Matrice%20des%20risques-taskforce.drawio.png)

### Contraintes
*   **Réglementaires** : Respect strict du RGPD (données collaborateurs).
*   **Techniques** : Interopérabilité via API REST, Design Responsive.
*   **Qualité** : Sécurité des données, Performance sous forte charge.

---

## 7. Livrables attendus

*   **Documentation** : Dossier de projet, Spécifications techniques, Manuel utilisateur.
*   **Code Source** : Dépôt Git complet (Back, Front, IA).
*   **Application** : Version déployée et fonctionnelle.
*   **Support** : Plan de maintenance et suivi post-déploiement.

---

## 8. Planning prévisionnel

*   **Phase 1 : Cadrage** (Octobre)
*   **Phase 2 : Conception & Prototypage** (Novembre)
*   **Phase 3 : Développement MVP** (Décembre - Janvier)
*   **Phase 4 : Intégration IA & Fonctionnalités avancées** (Février - Mars)
*   **Phase 5 : Recette & Déploiement** (Avril)
