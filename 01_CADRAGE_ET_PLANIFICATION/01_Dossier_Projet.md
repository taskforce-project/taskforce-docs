# DOSSIER DE PROJET - [NOM DU PROJET]

**Version :** 1.0  
**Date :** [15/11/2025]  
**Statut :** [Brouillon / **En cours** / Validé]  
**Equipe :** Pierre MICHEL

---

## TABLE DES MATIÈRES

1. [Contexte et Expression du Besoin](#1-contexte-et-expression-du-besoin)
2. [Présentation de l'Équipe Projet](#2-présentation-de-léquipe-projet)
3. [Organisation de l'Équipe](#3-organisation-de-léquipe)
4. [Méthodologie de Projet](#4-méthodologie-de-projet)
5. [Veille Technologique](#5-veille-technologique)
6. [Analyse Fonctionnelle](#6-analyse-fonctionnelle)
7. [Choix Technologiques](#7-choix-technologiques)
8. [Modélisation Projet](#8-modélisation-projet)
9. [Modélisation UML](#9-modélisation-uml)
10. [Modélisation Base de Données](#10-modélisation-base-de-données)
11. [Parties Prenantes](#11-parties-prenantes)
12. [Planification](#12-planification)
13. [Analyse des Risques](#13-analyse-des-risques)
14. [Architecture Logicielle](#14-architecture-logicielle)
15. [Infrastructure Logicielle](#15-infrastructure-logicielle)
16. [Budgétisation](#16-budgétisation)
17. [Maquettage et Design](#17-maquettage-et-design)
18. [Conformité et Normes](#18-conformité-et-normes)
19. [Stratégie de Tests](#19-stratégie-de-tests)
20. [Documentation Technique](#20-documentation-technique)
21. [Plan de Déploiement](#21-plan-de-déploiement)
22. [Maintenance et Support](#22-maintenance-et-support)
23. [Bilans de Projet](#23-bilans-de-projet)
24. [Annexes](#24-annexes)

---

## 1. CONTEXTE ET EXPRESSION DU BESOIN

### 1.1 Contexte du Projet

- **Origine du projet** : [Description de la genèse du projet]
- **Problématique identifiée** : [Quel problème résout le projet ?]
- **Enjeux** : [Business, techniques, organisationnels]
- **Périmètre** : [Ce qui est inclus / exclu du projet]

### 1.2 Expression du Besoin Initial

[Besoin brut tel qu'exprimé par le commanditaire]

### 1.3 Reformulation du Besoin

[Besoin reformulé de manière claire et structurée]

### 1.4 Objectifs du Projet

- **Objectif principal** :
- **Objectifs secondaires** :
  - Objectif 1
  - Objectif 2
  - Objectif 3

### 1.5 Livrables Attendus

- Livrable 1 : [Description]
- Livrable 2 : [Description]
- Livrable 3 : [Description]

---

## 2. PRÉSENTATION DE L'ÉQUIPE PROJET

### 2.1 Composition de l'Équipe

| Nom   | Rôle                  | Compétences Clés              | Contact           |
| ----- | --------------------- | ----------------------------- | ----------------- |
| [Nom] | Chef de Projet        | Gestion de projet, Scrum      | email@exemple.com |
| [Nom] | Développeur Front-End | React, TypeScript, CSS        | email@exemple.com |
| [Nom] | Développeur Back-End  | Node.js, PostgreSQL, API REST | email@exemple.com |
| [Nom] | DevOps                | Docker, CI/CD, AWS            | email@exemple.com |
| [Nom] | Designer UX/UI        | Figma, Accessibilité          | email@exemple.com |

### 2.2 Organigramme

```
[Insérer organigramme hiérarchique]
```

### 2.3 Disponibilité de l'Équipe

| Membre | Disponibilité (%) | Période |
| ------ | ----------------- | ------- |
| [Nom]  | 100%              | [Dates] |
| [Nom]  | 50%               | [Dates] |

---

## 3. ORGANISATION DE L'ÉQUIPE

### 3.1 Rôles et Responsabilités

#### Chef de Projet

- Pilotage global du projet
- Gestion des risques et du planning
- Communication avec les parties prenantes

#### Développeurs Front-End

- Développement des interfaces utilisateur
- Intégration des maquettes
- Optimisation des performances front

#### Développeurs Back-End

- Développement des API
- Gestion de la base de données
- Sécurité et authentification

#### DevOps

- Configuration des environnements
- Mise en place du CI/CD
- Monitoring et maintenance

### 3.2 Modes de Communication

- **Réunions quotidiennes** : Daily Stand-up (15 min) - 9h30
- **Réunions hebdomadaires** : Revue de sprint - Vendredi 16h
- **Outils** : Slack, Jira, Confluence, GitHub

### 3.3 Processus de Décision

[Décrire comment les décisions sont prises dans l'équipe]

---

## 4. MÉTHODOLOGIE DE PROJET

### 4.1 Méthodologie Choisie

**[Agile Scrum / Kanban / Cycle en V / Autre]**

### 4.2 Justification du Choix

[Pourquoi cette méthodologie a été retenue]

### 4.3 Application Concrète

#### Sprints

- **Durée** : [2 semaines / 3 semaines]
- **Nombre de sprints prévisionnels** : [X sprints]
- **Cérémonies** :
  - Sprint Planning : [Jour et horaire]
  - Daily Stand-up : [Jour et horaire]
  - Sprint Review : [Jour et horaire]
  - Sprint Retrospective : [Jour et horaire]

#### User Stories

- Format : "En tant que [rôle], je veux [action] afin de [bénéfice]"
- Critères d'acceptance : [DoD - Definition of Done]

### 4.4 Workflow de Développement

```
[Diagramme du workflow :  Backlog → To Do → In Progress → Review → Testing → Done]
```

### 4.5 Gestion de Version (Git Flow)

- **Branches principales** :
  - `main` : Production
  - `develop` : Développement
- **Branches secondaires** :
  - `feature/*` : Nouvelles fonctionnalités
  - `hotfix/*` : Corrections urgentes
  - `release/*` : Préparation des releases

---

## 5. VEILLE TECHNOLOGIQUE

### 5.1 Objectifs de la Veille

- Rester informé des dernières technologies
- Identifier les meilleures pratiques
- Anticiper les évolutions du secteur

### 5.2 Moyens et Sources de Veille

#### Sources Techniques

| Source              | Type               | Fréquence    | Thématique                   |
| ------------------- | ------------------ | ------------ | ---------------------------- |
| dev. to             | Blog communautaire | Quotidienne  | Développement web            |
| Medium Engineering  | Articles           | Hebdomadaire | Architecture, Best practices |
| GitHub Trending     | Répertoires        | Hebdomadaire | Projets open source          |
| Stack Overflow Blog | Blog               | Hebdomadaire | Technologies émergentes      |

#### Newsletters

- JavaScript Weekly : https://javascriptweekly.com/
- Node Weekly : https://nodeweekly.com/
- CSS-Tricks : https://css-tricks.com/

#### Podcasts

- Syntax. fm : https://syntax.fm/
- The Changelog : https://changelog.com/podcast

#### Conférences et Meetups

- [Nom de la conférence] - [Date]
- [Meetup local] - [Fréquence]

#### Réseaux Sociaux

- Twitter/X : Suivi de [@influenceur1], [@influenceur2]
- LinkedIn : Groupes professionnels

### 5.3 Outils de Veille

- **Feedly** : Agrégateur de flux RSS
- **Pocket** : Sauvegarde d'articles
- **Notion** : Base de connaissance partagée

### 5.4 Synthèse de Veille

[Tableau de synthèse des découvertes récentes applicables au projet]

---

## 6. ANALYSE FONCTIONNELLE

### 6.1 Objectifs SMART

| Critère                   | Description                                     |
| ------------------------- | ----------------------------------------------- |
| **S**pécifique            | [Objectif précis et clairement défini]          |
| **M**esurable             | [Indicateurs chiffrés : KPI, métriques]         |
| **A**cceptable            | [Objectif ambitieux mais réaliste]              |
| **R**éaliste              | [Ressources disponibles, faisabilité technique] |
| **T**emporellement défini | [Date de fin : JJ/MM/AAAA]                      |

**Exemple :**

- **S** : Développer une application web de gestion de tâches collaborative
- **M** : Supporter 1000 utilisateurs simultanés avec un temps de réponse < 2s
- **A** : Améliorer la productivité des équipes de 30%
- **R** : Équipe de 5 développeurs, budget de X€, technologies maîtrisées
- **T** : Livraison en production le 30/06/2026

### 6.2 Exigences Fonctionnelles

#### Epic 1 : [Nom de l'Epic]

**User Stories :**

- US01 : En tant que [rôle], je veux [action] afin de [bénéfice]
  - Critères d'acceptance : [Liste]
  - Priorité : [Haute / Moyenne / Basse]
  - Estimation : [X points]

#### Epic 2 : [Nom de l'Epic]

[...]

### 6.3 Exigences Non-Fonctionnelles

| Catégorie     | Exigence                | Critère de Mesure             |
| ------------- | ----------------------- | ----------------------------- |
| Performance   | Temps de réponse        | < 2 secondes                  |
| Disponibilité | Uptime                  | 99.9%                         |
| Sécurité      | Chiffrement             | HTTPS, AES-256                |
| Scalabilité   | Utilisateurs simultanés | 10 000                        |
| Compatibilité | Navigateurs             | Chrome, Firefox, Safari, Edge |
| Accessibilité | Normes                  | WCAG 2.1 niveau AA            |

### 6.4 Cas d'Usage Principaux

[Liste des principaux cas d'usage avec description]

---

## 7. CHOIX TECHNOLOGIQUES

### 7.1 Technologies Front-End

#### Tableau Comparatif

| Critère                    | React             | Vue.js          | Angular           | Choix Final |
| -------------------------- | ----------------- | --------------- | ----------------- | ----------- |
| **Courbe d'apprentissage** | Moyenne           | Facile          | Difficile         | ✅ React    |
| **Performance**            | Excellente        | Excellente      | Bonne             |             |
| **Écosystème**             | Très riche        | Riche           | Complet           |             |
| **Communauté**             | Très large        | Large           | Large             |             |
| **TypeScript**             | Excellent support | Bon support     | Natif             |             |
| **Taille du bundle**       | Moyenne           | Petite          | Grande            |             |
| **Entreprises utilisant**  | Facebook, Netflix | Alibaba, GitLab | Google, Microsoft |             |

**Justification du choix :** [Explication détaillée]

#### Stack Front-End Retenue

- **Framework** : React 18+
- **Langage** : TypeScript
- **Gestion d'état** : Redux Toolkit / Zustand
- **Routing** : React Router
- **UI Library** : Material-UI / Tailwind CSS
- **Forms** : React Hook Form
- **HTTP Client** : Axios
- **Tests** : Jest + React Testing Library

### 7.2 Technologies Back-End

#### Tableau Comparatif

| Critère                    | Node.js (Express) | Django (Python) | Spring Boot (Java) | Choix Final |
| -------------------------- | ----------------- | --------------- | ------------------ | ----------- |
| **Performance**            | Excellente        | Bonne           | Excellente         | ✅ Node.js  |
| **Scalabilité**            | Excellente        | Bonne           | Excellente         |             |
| **Écosystème**             | Très riche        | Riche           | Très riche         |             |
| **Courbe d'apprentissage** | Moyenne           | Facile          | Difficile          |             |
| **Async/Real-time**        | Natif             | Avec channels   | Avec WebFlux       |             |
| **Typage**                 | TypeScript        | Python (typing) | Natif              |             |

**Justification du choix :** [Explication détaillée]

#### Stack Back-End Retenue

- **Runtime** : Node.js 20+ LTS
- **Framework** : Express.js / NestJS
- **Langage** : TypeScript
- **Validation** : Joi / Zod
- **ORM** : Prisma / TypeORM
- **Authentication** : JWT + Passport.js
- **Documentation API** : Swagger / OpenAPI
- **Tests** : Jest + Supertest

### 7.3 Base de Données

#### Tableau Comparatif

| Critère          | PostgreSQL    | MySQL             | MongoDB     | Choix Final   |
| ---------------- | ------------- | ----------------- | ----------- | ------------- |
| **Type**         | SQL           | SQL               | NoSQL       | ✅ PostgreSQL |
| **Performance**  | Excellente    | Excellente        | Excellente  |               |
| **ACID**         | Oui           | Oui               | Partiel     |               |
| **Scalabilité**  | Verticale++   | Verticale+        | Horizontale |               |
| **JSON Support** | Natif (JSONB) | Limité            | Natif       |               |
| **Open Source**  | Oui           | Oui (avec limite) | Oui         |               |
| **Robustesse**   | Très haute    | Haute             | Haute       |               |

**Justification du choix :** [Explication détaillée]

#### Configuration BDD

- **SGBD** : PostgreSQL 15+
- **Connexion** : pg / pg-pool
- **Migrations** : Prisma Migrate / Knex.js
- **Backup** : [Stratégie de sauvegarde]

### 7.4 DevOps et Infrastructure

| Outil                | Technologie                 | Usage                        |
| -------------------- | --------------------------- | ---------------------------- |
| **Conteneurisation** | Docker                      | Isolation des environnements |
| **Orchestration**    | Docker Compose / Kubernetes | Gestion multi-conteneurs     |
| **CI/CD**            | GitHub Actions / GitLab CI  | Automatisation déploiement   |
| **Cloud Provider**   | AWS / Azure / GCP           | Hébergement                  |
| **Monitoring**       | Prometheus + Grafana        | Surveillance performance     |
| **Logs**             | ELK Stack / Loki            | Centralisation des logs      |
| **Serveur Web**      | Nginx                       | Reverse proxy                |

### 7.5 Outils de Développement

| Catégorie             | Outil              | Justification               |
| --------------------- | ------------------ | --------------------------- |
| **IDE**               | VS Code            | Léger, extensible, gratuit  |
| **Versioning**        | Git + GitHub       | Standard industrie          |
| **Gestion de projet** | Jira / Trello      | Suivi agile                 |
| **Design**            | Figma              | Collaboration en temps réel |
| **API Testing**       | Postman / Insomnia | Test des endpoints          |
| **Qualité code**      | ESLint + Prettier  | Cohérence du code           |

---

## 8. MODÉLISATION PROJET

### 8.1 Product Breakdown Structure (PBS)

```
[NOM DU PROJET]
│
├── Module 1 :  [Nom]
│   ├── Sous-module 1.1
│   ├── Sous-module 1.2
│   └── Sous-module 1.3
│
├── Module 2 : [Nom]
│   ├── Sous-module 2.1
│   └── Sous-module 2.2
│
└── Module 3 : [Nom]
    ├── Sous-module 3.1
    ├── Sous-module 3.2
    └── Sous-module 3.3
```

**Exemple concret :**

```
Application de Gestion de Tâches
│
├── Authentification
│   ├── Inscription
│   ├── Connexion
│   └── Réinitialisation mot de passe
│
├── Gestion des Tâches
│   ├── Création de tâches
│   ├── Modification de tâches
│   ├── Suppression de tâches
│   └── Assignation de tâches
│
├── Collaboration
│   ├── Commentaires
│   ├── Notifications
│   └── Partage de projets
│
└── Administration
    ├── Gestion des utilisateurs
    ├── Statistiques
    └── Configuration système
```

### 8.2 Work Breakdown Structure (WBS)

```
[NOM DU PROJET]
│
├── 1. Initialisation du Projet
│   ├── 1.1 Étude de faisabilité
│   ├── 1.2 Constitution de l'équipe
│   └── 1.3 Setup environnement
│
├── 2. Conception
│   ├── 2.1 Analyse fonctionnelle
│   ├── 2.2 Modélisation UML
│   ├── 2.3 Modélisation BDD
│   └── 2.4 Maquettage
│
├── 3. Développement
│   ├── 3.1 Sprint 1 - Authentification
│   ├── 3.2 Sprint 2 - CRUD Tâches
│   ├── 3.3 Sprint 3 - Collaboration
│   └── 3.4 Sprint 4 - Administration
│
├── 4. Tests
│   ├── 4.1 Tests unitaires
│   ├── 4.2 Tests d'intégration
│   ├── 4.3 Tests e2e
│   └── 4.4 Tests de charge
│
├── 5. Déploiement
│   ├── 5.1 Environnement staging
│   ├── 5.2 Migration données
│   └── 5.3 Mise en production
│
└── 6. Clôture
    ├── 6.1 Documentation finale
    ├── 6.2 Formation utilisateurs
    └── 6.3 Bilan de projet
```

### 8.3 Estimation des Charges

| Tâche WBS                 | Durée (j) | Ressources | Dépendances |
| ------------------------- | --------- | ---------- | ----------- |
| 1.1 Étude de faisabilité  | 3         | CDP        | -           |
| 1.2 Constitution équipe   | 2         | CDP        | 1.1         |
| 2.1 Analyse fonctionnelle | 5         | CDP + Dev  | 1.2         |
| [... ]                    | [...]     | [...]      | [...]       |

---

## 9. MODÉLISATION UML

### 9.1 Diagramme de Cas d'Utilisation

```
[Insérer diagramme des cas d'utilisation]

Acteurs :
- Utilisateur
- Administrateur
- Système

Cas d'utilisation :
- S'authentifier
- Gérer les tâches
- Collaborer
- etc.
```

**Description des cas d'utilisation principaux :**

#### CU01 : S'authentifier

- **Acteur principal** : Utilisateur
- **Préconditions** : L'utilisateur possède un compte
- **Scénario nominal** :
  1. L'utilisateur accède à la page de connexion
  2. L'utilisateur saisit ses identifiants
  3. Le système vérifie les identifiants
  4. Le système redirige vers le tableau de bord
- **Scénarios alternatifs** :
  - 3a. Identifiants incorrects : Message d'erreur
- **Postconditions** : L'utilisateur est authentifié

### 9.2 Diagramme d'Activité

```
[Insérer diagrammes d'activité pour les processus métier clés]

Exemple :  Processus de création d'une tâche
- Début
- Saisie des informations
- Validation des données
- Enregistrement en BDD
- Notification assigné
- Fin
```

### 9.3 Diagramme de Séquence

```
[Insérer diagrammes de séquence pour les interactions importantes]

Exemple : Séquence d'authentification
Utilisateur -> UI : Saisie identifiants
UI -> API : POST /auth/login
API -> BDD : Vérification utilisateur
BDD -> API : Données utilisateur
API -> API : Génération JWT
API -> UI : Token + User data
UI -> Utilisateur : Redirection dashboard
```

### 9.4 Diagramme de Classes

```
[Insérer diagramme de classes complet]

Classes principales :
- User
- Task
- Project
- Comment
- Notification
- etc.

Avec attributs, méthodes et relations
```

**Exemple de classe détaillée :**

```typescript
class User {
  - id: string
  - email:  string
  - password: string (hashed)
  - firstName: string
  - lastName: string
  - role: Role
  - createdAt: Date
  - updatedAt: Date

  + authenticate(password: string): boolean
  + generateToken(): string
  + updateProfile(data: ProfileData): void
}
```

### 9.5 Diagramme d'États-Transitions

```
[Insérer diagramme d'états pour les entités avec cycle de vie]

Exemple : États d'une tâche
- Créée (nouveau)
- En cours
- En révision
- Terminée
- Archivée
```

---

## 10. MODÉLISATION BASE DE DONNÉES

### 10.1 Modèle Conceptuel de Données (MCD)

```
[Insérer MCD avec entités et associations]

Entités :
- USER
- TASK
- PROJECT
- COMMENT
- etc.

Associations :
- USER crée TASK (1,n)
- TASK appartient à PROJECT (n,1)
- etc.
```

### 10.2 Modèle Logique de Données (MLD)

```
USER (id_user, email, password, first_name, last_name, role, created_at)
PROJECT (id_project, name, description, #id_owner, created_at)
TASK (id_task, title, description, status, priority, #id_project, #id_assignee, created_at)
COMMENT (id_comment, content, #id_task, #id_author, created_at)
```

### 10.3 Modèle Physique de Données (MPD)

```sql
-- Table users
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role VARCHAR(50) DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table projects
CREATE TABLE projects (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    owner_id UUID REFERENCES users(id) ON DELETE CASCADE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table tasks
CREATE TABLE tasks (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    title VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'todo',
    priority VARCHAR(50) DEFAULT 'medium',
    project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
    assignee_id UUID REFERENCES users(id) ON DELETE SET NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Indexes pour optimisation
CREATE INDEX idx_tasks_project ON tasks(project_id);
CREATE INDEX idx_tasks_assignee ON tasks(assignee_id);
CREATE INDEX idx_projects_owner ON projects(owner_id);
```

### 10.4 Dictionnaire de Données

| Table  | Champ    | Type         | Contraintes      | Description            |
| ------ | -------- | ------------ | ---------------- | ---------------------- |
| users  | id       | UUID         | PK               | Identifiant unique     |
| users  | email    | VARCHAR(255) | UNIQUE, NOT NULL | Email de l'utilisateur |
| users  | password | VARCHAR(255) | NOT NULL         | Mot de passe hashé     |
| [... ] | [...]    | [...]        | [...]            | [...]                  |

### 10.5 Stratégie d'Indexation

| Index             | Table | Colonnes   | Justification                        |
| ----------------- | ----- | ---------- | ------------------------------------ |
| idx_tasks_project | tasks | project_id | Requêtes fréquentes par projet       |
| idx_users_email   | users | email      | Recherche lors de l'authentification |

---

## 11. PARTIES PRENANTES

### 11.1 Identification des Parties Prenantes

| Partie Prenante    | Rôle                 | Intérêt    | Influence | Stratégie d'Engagement     |
| ------------------ | -------------------- | ---------- | --------- | -------------------------- |
| Direction Générale | Sponsor              | Élevé      | Élevée    | Comité de pilotage mensuel |
| Équipe Métier      | Utilisateur final    | Très élevé | Moyenne   | Démos régulières, feedback |
| Équipe IT          | Support technique    | Moyen      | Moyenne   | Réunions techniques        |
| DSI                | Validateur technique | Élevé      | Élevée    | Revues architecture        |
| Clients            | Bénéficiaire         | Très élevé | Faible    | Beta testing               |

### 11.2 Matrice RACI

**R** = Responsible (Réalise)  
**A** = Accountable (Autorité)  
**C** = Consulted (Consulté)  
**I** = Informed (Informé)

| Tâche / Activité                 | Chef de Projet | Dev Front | Dev Back | DevOps | Designer | Sponsor |
| -------------------------------- | -------------- | --------- | -------- | ------ | -------- | ------- |
| **Cadrage projet**               | A              | I         | I        | I      | I        | C       |
| **Analyse fonctionnelle**        | R/A            | C         | C        | I      | C        | I       |
| **Maquettage**                   | C              | C         | I        | I      | R/A      | I       |
| **Développement Front**          | A              | R         | I        | I      | C        | I       |
| **Développement Back**           | A              | I         | R        | C      | I        | I       |
| **Configuration infrastructure** | C              | I         | C        | R/A    | I        | I       |
| **Tests unitaires**              | I              | R         | R        | I      | I        | I       |
| **Tests utilisateurs**           | A              | C         | C        | I      | C        | C       |
| **Déploiement production**       | A              | I         | I        | R      | I        | C       |
| **Formation utilisateurs**       | R              | C         | I        | I      | C        | I       |
| **Validation finale**            | C              | I         | I        | I      | I        | R/A     |

### 11.3 Plan de Communication

| Partie Prenante | Fréquence       | Canal              | Contenu                     |
| --------------- | --------------- | ------------------ | --------------------------- |
| Sponsor         | Mensuel         | Comité de pilotage | Avancement, budget, risques |
| Équipe Métier   | Bi-hebdomadaire | Démo + email       | Nouvelles fonctionnalités   |
| Équipe Projet   | Quotidien       | Stand-up           | Avancement quotidien        |
| DSI             | Mensuel         | Réunion technique  | Architecture, sécurité      |

---

## 12. PLANIFICATION

### 12.1 Diagramme de Gantt - Planning Prévisionnel

```
[Insérer diagramme de Gantt]

Phases principales :
- Initialisation :  [Dates]
- Conception : [Dates]
- Développement : [Dates]
- Tests : [Dates]
- Déploiement : [Dates]
- Clôture : [Dates]
```

**Format tabulaire :**

| Phase      | Tâche                 | Début    | Fin      | Durée | Ressource | Dépendances |
| ---------- | --------------------- | -------- | -------- | ----- | --------- | ----------- |
| Init       | Kickoff meeting       | 01/02/26 | 01/02/26 | 1j    | Équipe    | -           |
| Init       | Setup environnement   | 02/02/26 | 05/02/26 | 4j    | DevOps    | 1           |
| Conception | Analyse fonctionnelle | 06/02/26 | 12/02/26 | 5j    | CDP       | 2           |
| Conception | Maquettage            | 06/02/26 | 15/02/26 | 8j    | Designer  | 3           |
| [... ]     | [...]                 | [...]    | [...]    | [...] | [...]     | [...]       |

### 12.2 Jalons (Milestones)

| Jalon                  | Date Cible | Livrables               | Critères de Validation |
| ---------------------- | ---------- | ----------------------- | ---------------------- |
| M1 : Fin de conception | 28/02/26   | Maquettes, BDD, UML     | Validation sponsor     |
| M2 : MVP               | 30/04/26   | Fonctionnalités de base | Tests passés           |
| M3 : Beta              | 31/05/26   | Application complète    | UAT réussis            |
| M4 : Production        | 30/06/26   | Déploiement final       | Go-live                |

### 12.3 Chemin Critique

```
[Identifier les tâches du chemin critique qui ne peuvent être retardées]

Tâches critiques :
- Setup environnement → Développement → Tests → Déploiement
```

### 12.4 Planning Réel (À compléter pendant le projet)

| Phase  | Tâche | Prévu | Réel  | Écart | Raison |
| ------ | ----- | ----- | ----- | ----- | ------ |
| [... ] | [...] | [...] | [...] | [...] | [...]  |

### 12.5 Analyse des Écarts (Post-projet)

[À compléter en fin de projet pour analyser les différences entre prévisionnel et réel]

---

## 13. ANALYSE DES RISQUES

### 13.1 Méthodologie d'Évaluation

**Probabilité :**

- Faible : < 20%
- Moyenne : 20-60%
- Élevée : > 60%

**Impact :**

- Faible : Retard < 1 semaine, coût < 5%
- Moyen : Retard 1-4 semaines, coût 5-15%
- Élevé : Retard > 4 semaines, coût > 15%

**Criticité = Probabilité × Impact**

### 13.2 Registre des Risques

| ID  | Risque                      | Catégorie      | Probabilité | Impact | Criticité   | Mitigation                       | Plan de Contingence               | Responsable |
| --- | --------------------------- | -------------- | ----------- | ------ | ----------- | -------------------------------- | --------------------------------- | ----------- |
| R01 | Départ d'un membre clé      | RH             | Moyenne     | Élevé  | **Élevée**  | Documentation, knowledge sharing | Recrutement rapide, formations    | CDP         |
| R02 | Retard livraison API tier   | Technique      | Faible      | Moyen  | **Moyenne** | Suivi régulier fournisseur       | Mock API, développement parallèle | Dev Lead    |
| R03 | Changement périmètre        | Scope creep    | Élevée      | Moyen  | **Élevée**  | Validation formelle changements  | Priorisation stricte              | CDP         |
| R04 | Faille de sécurité          | Sécurité       | Moyenne     | Élevé  | **Élevée**  | Audits sécurité, code review     | Patch d'urgence                   | Tech Lead   |
| R05 | Dépassement budget          | Financier      | Moyenne     | Élevé  | **Élevée**  | Suivi budgétaire hebdomadaire    | Réduction périmètre               | CDP         |
| R06 | Problème de performance     | Technique      | Moyenne     | Moyen  | **Moyenne** | Tests de charge réguliers        | Optimisation, scaling             | DevOps      |
| R07 | Incompatibilité navigateurs | Technique      | Faible      | Faible | **Faible**  | Tests multi-navigateurs          | Polyfills, fallbacks              | Dev Front   |
| R08 | Indisponibilité cloud       | Infrastructure | Faible      | Élevé  | **Moyenne** | SLA provider, monitoring         | Plan de reprise                   | DevOps      |

### 13.3 Matrice des Risques

```
Impact
  Élevé   │  R05   │  R03   │  R01, R04  │
          │        │        │            │
  Moyen   │        │  R07   │  R02, R06  │
          │        │        │            │
  Faible  │        │  R07   │            │
          └────────┴────────┴────────────┘
            Faible  Moyenne   Élevée
                  Probabilité

🔴 Risque critique (rouge) : Action immédiate
🟠 Risque important (orange) : Surveillance étroite
🟡 Risque modéré (jaune) : Surveillance régulière
🟢 Risque faible (vert) : Surveillance périodique
```

### 13.4 Plan d'Actions

| Risque | Action                             | Échéance | Statut   | Responsable |
| ------ | ---------------------------------- | -------- | -------- | ----------- |
| R01    | Mise en place documentation projet | 15/02/26 | En cours | CDP         |
| R04    | Audit sécurité par expert externe  | 30/03/26 | Planifié | Tech Lead   |
| R05    | Revue budgétaire hebdomadaire      | Hebdo    | En place | CDP         |

### 13.5 Suivi des Risques

[Tableau à mettre à jour régulièrement tout au long du projet]

| Date   | Risque | Évolution | Actions prises |
| ------ | ------ | --------- | -------------- |
| [... ] | [...]  | [...]     | [...]          |

---

## 14. ARCHITECTURE LOGICIELLE

### 14.1 Pattern Architectural Principal

**Architecture choisie : [MVC / MVVM / Clean Architecture / Microservices / etc.]**

### 14.2 Architecture Monolithique / Microservices

#### Option retenue : [Choix et justification]

**Pour un monolithe modulaire :**

```
Application
│
├── Presentation Layer (Controllers, Views)
├── Business Logic Layer (Services)
├── Data Access Layer (Repositories)
└── Database
```

**Pour des microservices :**

```
Gateway API
│
├── Auth Service
├── User Service
├── Task Service
├── Notification Service
└── Analytics Service

Chaque service possède :
- API REST
- Base de données dédiée
- Logique métier isolée
```

### 14.3 Architecture Détaillée

#### Front-End Architecture

```
src/
├── assets/              # Images, fonts, styles
├── components/          # Composants réutilisables
│   ├── common/         # Boutons, inputs, etc.
│   └── features/       # Composants métier
├── pages/              # Pages de l'application
├── hooks/              # Custom React hooks
├── services/           # API calls
├── store/              # State management
├── utils/              # Fonctions utilitaires
├── types/              # TypeScript types
├── config/             # Configuration
└── App.tsx             # Point d'entrée
```

#### Back-End Architecture (MVC)

```
src/
├── controllers/        # Gestion des requêtes HTTP
├── models/            # Modèles de données (ORM)
├── services/          # Logique métier
├── repositories/      # Accès aux données
├── middlewares/       # Auth, validation, erreurs
├── routes/            # Définition des routes
├── validators/        # Schémas de validation
├── utils/             # Fonctions utilitaires
├── config/            # Configuration (DB, env)
├── types/             # TypeScript types
└── server.ts          # Point d'entrée
```

### 14.4 Flux de Données

```
Client (Browser)
    ↓ HTTP Request
API Gateway / Load Balancer
    ↓
Route Handlers (Controllers)
    ↓
Middlewares (Auth, Validation)
    ↓
Business Logic (Services)
    ↓
Data Access (Repositories)
    ↓
Database (PostgreSQL)
```

### 14.5 Principes de Conception

- **SOLID Principles**

  - Single Responsibility
  - Open/Closed
  - Liskov Substitution
  - Interface Segregation
  - Dependency Inversion

- **DRY** : Don't Repeat Yourself
- **KISS** : Keep It Simple, Stupid
- **YAGNI** : You Aren't Gonna Need It
- **Separation of Concerns**

### 14.6 Design Patterns Utilisés

| Pattern    | Usage                           | Localisation             |
| ---------- | ------------------------------- | ------------------------ |
| Singleton  | Instance unique de connexion DB | `database. ts`           |
| Factory    | Création d'objets complexes     | `services/factory/`      |
| Repository | Abstraction accès données       | `repositories/`          |
| Middleware | Gestion requêtes HTTP           | `middlewares/`           |
| Observer   | Système de notifications        | `services/notification/` |

---

## 15. INFRASTRUCTURE LOGICIELLE

### 15.1 Architecture Cible

```
                    Internet
                       │
                       ▼
              [Cloudflare CDN]
                       │
                       ▼
            [Load Balancer / Nginx]
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
   [Web Server 1] [Web Server 2] [Web Server 3]
        │              │              │
        └──────────────┼──────────────┘
                       ▼
              [Application Server]
              (Node.js + Express)
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
   [PostgreSQL]  [Redis Cache]  [S3 Storage]
   (Primary)
        │
        ▼
   [PostgreSQL]
   (Replica - Read)
```

### 15.2 Environnements

#### Environnement de Développement (DEV)

| Composant           | Configuration          | Localisation        |
| ------------------- | ---------------------- | ------------------- |
| **Serveur**         | Local / Docker         | Machine développeur |
| **Base de données** | PostgreSQL 15 (Docker) | localhost:5432      |
| **Cache**           | Redis (Docker)         | localhost:6379      |
| **URL**             | http://localhost:3000  | Local               |
| **CI/CD**           | -                      | -                   |

#### Environnement de Staging (PREPROD)

| Composant           | Configuration           | Localisation     |
| ------------------- | ----------------------- | ---------------- |
| **Serveur**         | AWS EC2 t3.medium       | eu-west-1        |
| **Base de données** | AWS RDS PostgreSQL      | db. t3.small     |
| **Cache**           | AWS ElastiCache Redis   | cache. t3.micro  |
| **URL**             | https://staging.app.com | -                |
| **CI/CD**           | GitHub Actions          | Déploiement auto |

#### Environnement de Production (PROD)

| Composant           | Configuration         | Localisation               |
| ------------------- | --------------------- | -------------------------- |
| **Serveur Web**     | AWS EC2 t3.large (x3) | Multi-AZ                   |
| **Load Balancer**   | AWS ALB               | -                          |
| **Base de données** | AWS RDS PostgreSQL    | db.t3.large + Read Replica |
| **Cache**           | AWS ElastiCache Redis | cache. t3.medium (cluster) |
| **Storage**         | AWS S3                | Standard + Glacier         |
| **CDN**             | CloudFlare            | Global                     |
| **URL**             | https://app.com       | -                          |
| **Monitoring**      | CloudWatch + Grafana  | -                          |

### 15.3 Serveurs et Ressources

#### Dimensionnement Production

| Ressource          | Type              | Specs            | Quantité      | Coût Mensuel   |
| ------------------ | ----------------- | ---------------- | ------------- | -------------- |
| Application Server | EC2 t3.large      | 2 vCPU, 8 GB RAM | 3             | 3 × 75€ = 225€ |
| Database           | RDS PostgreSQL    | db.t3.large      | 1 + 1 replica | 150€ + 75€     |
| Cache              | ElastiCache Redis | cache.t3.medium  | 1             | 60€            |
| Load Balancer      | AWS ALB           | -                | 1             | 25€            |
| Storage            | S3                | 100 GB           | -             | 3€             |
| CDN                | CloudFlare        | Pro plan         | -             | 20€            |
| **TOTAL**          |                   |                  |               | **~558€/mois** |

### 15.4 Protocoles et Communication

#### Protocoles Utilisés

| Communication     | Protocole  | Port | Chiffrement |
| ----------------- | ---------- | ---- | ----------- |
| Client ↔ Server   | HTTPS      | 443  | TLS 1.3     |
| Server ↔ Database | PostgreSQL | 5432 | SSL         |
| Server ↔ Cache    | Redis      | 6379 | TLS         |
| Server ↔ S3       | HTTPS      | 443  | TLS 1.3     |
| Inter-services    | REST API   | 443  | TLS 1.3     |

#### API Communication

- **REST API** : Communication principale
- **WebSocket** : Notifications temps réel
- **GraphQL** : (Optionnel) Requêtes complexes

### 15.5 Flux de Données

```
1.  Requête Client
   Client → CDN (CloudFlare) → Load Balancer → Web Server

2. Authentification
   Web Server → Redis (vérification session)

3. Lecture Données
   Web Server → PostgreSQL (Read Replica)

4. Écriture Données
   Web Server → PostgreSQL (Primary) → Réplication → Replica

5. Cache
   Web Server → Redis (get/set) → Si miss → PostgreSQL

6. Upload Fichiers
   Client → Web Server → S3 Storage
```

### 15.6 Sécurité Infrastructure

| Niveau              | Mesure de Sécurité                   |
| ------------------- | ------------------------------------ |
| **Réseau**          | VPC isolé, Security Groups, WAF      |
| **Transport**       | HTTPS/TLS 1.3 obligatoire            |
| **Application**     | Validation inputs, Rate limiting     |
| **Base de données** | Encryption at rest, SSL connections  |
| **Accès**           | IAM roles, MFA, SSH keys only        |
| **Secrets**         | AWS Secrets Manager / Vault          |
| **Logs**            | Centralisés, chiffrés, rétention 90j |

### 15.7 Stratégie de Backup

| Ressource       | Fréquence           | Rétention   | Localisation      |
| --------------- | ------------------- | ----------- | ----------------- |
| Base de données | Quotidien           | 30 jours    | AWS RDS Snapshots |
| Fichiers (S3)   | Incrémental continu | Versionning | S3 + Glacier      |
| Configuration   | À chaque changement | Git history | GitHub            |
| Logs            | Temps réel          | 90 jours    | CloudWatch Logs   |

### 15.8 Scalabilité

**Stratégie de scaling :**

- **Horizontal** : Auto-scaling des EC2 (min: 2, max: 10)
- **Vertical** : Upgrade instances si besoin
- **Database** : Read replicas pour lecture, sharding si nécessaire
- **Cache** : Redis cluster pour haute disponibilité
- **CDN** : Distribution globale automatique

**Triggers d'auto-scaling :**

- CPU > 70% pendant 5 min → +1 instance
- CPU < 30% pendant 10 min → -1 instance

---

## 16. BUDGÉTISATION

### 16.1 Estimation des Charges de Travail

#### Décomposition par Tâche

| Phase              | Tâche                 | Dev Front | Dev Back | DevOps   | Designer | CDP      | Total (h) |
| ------------------ | --------------------- | --------- | -------- | -------- | -------- | -------- | --------- |
| **Initialisation** | Setup projet          | 8h        | 8h       | 16h      | 4h       | 16h      | 52h       |
| **Conception**     | Analyse fonctionnelle | -         | -        | -        | -        | 40h      | 40h       |
| **Conception**     | Maquettage            | -         | -        | -        | 60h      | 10h      | 70h       |
| **Conception**     | Modélisation BDD      | -         | 16h      | -        | -        | 8h       | 24h       |
| **Dev Sprint 1**   | Auth (Front)          | 32h       | -        | -        | 8h       | -        | 40h       |
| **Dev Sprint 1**   | Auth (Back)           | -         | 40h      | 8h       | -        | -        | 48h       |
| **Dev Sprint 2**   | CRUD Tâches (Front)   | 48h       | -        | -        | 16h      | -        | 64h       |
| **Dev Sprint 2**   | API Tâches (Back)     | -         | 40h      | 4h       | -        | -        | 44h       |
| **Dev Sprint 3**   | Collaboration (Front) | 40h       | -        | -        | 12h      | -        | 52h       |
| **Dev Sprint 3**   | Notifications (Back)  | -         | 32h      | 8h       | -        | -        | 40h       |
| **Tests**          | Tests unitaires       | 24h       | 24h      | -        | -        | -        | 48h       |
| **Tests**          | Tests e2e             | 16h       | 8h       | -        | -        | 8h       | 32h       |
| **Tests**          | Tests charge          | -         | -        | 16h      | -        | 4h       | 20h       |
| **Déploiement**    | CI/CD                 | -         | 8h       | 32h      | -        | 8h       | 48h       |
| **Déploiement**    | Production            | -         | 8h       | 24h      | -        | 16h      | 48h       |
| **Documentation**  | Technique             | 16h       | 16h      | 8h       | -        | 24h      | 64h       |
| **Formation**      | Utilisateurs          | 8h        | -        | -        | 4h       | 16h      | 28h       |
| **TOTAL**          |                       | **192h**  | **200h** | **116h** | **104h** | **150h** | **762h**  |

### 16.2 Coût de la Main d'Œuvre

#### Taux Journaliers Moyens (TJM)

| Rôle                  | TJM  | Base horaire | Source                 |
| --------------------- | ---- | ------------ | ---------------------- |
| Chef de Projet        | 550€ | 69€/h        | Moyenne marché FR 2026 |
| Développeur Front-End | 480€ | 60€/h        | Moyenne marché FR 2026 |
| Développeur Back-End  | 500€ | 63€/h        | Moyenne marché FR 2026 |
| DevOps                | 580€ | 73€/h        | Moyenne marché FR 2026 |
| Designer UX/UI        | 450€ | 56€/h        | Moyenne marché FR 2026 |

_Base : 8h/jour_

#### Calcul des Coûts RH

| Rôle           | Heures   | Taux Horaire | Coût Total  |
| -------------- | -------- | ------------ | ----------- |
| Chef de Projet | 150h     | 69€/h        | **10 350€** |
| Dev Front-End  | 192h     | 60€/h        | **11 520€** |
| Dev Back-End   | 200h     | 63€/h        | **12 600€** |
| DevOps         | 116h     | 73€/h        | **8 468€**  |
| Designer UX/UI | 104h     | 56€/h        | **5 824€**  |
| **TOTAL RH**   | **762h** |              | **48 762€** |

### 16.3 Coût de l'Infrastructure

#### Coûts d'Hébergement (12 mois)

| Ressource                    | Coût Mensuel  | Coût Annuel (12 mois) |
| ---------------------------- | ------------- | --------------------- |
| Application Servers (3×)     | 225€          | 2 700€                |
| Database (Primary + Replica) | 225€          | 2 700€                |
| Cache (Redis)                | 60€           | 720€                  |
| Load Balancer                | 25€           | 300€                  |
| Storage S3                   | 3€            | 36€                   |
| CDN (CloudFlare Pro)         | 20€           | 240€                  |
| Monitoring (Grafana Cloud)   | 15€           | 180€                  |
| Backup & Snapshots           | 10€           | 120€                  |
| **TOTAL Infrastructure**     | **583€/mois** | **6 996€/an**         |

#### Coûts de Domaine et Certificats

| Poste                          | Coût Annuel  |
| ------------------------------ | ------------ |
| Nom de domaine (. com)         | 15€          |
| Certificat SSL (Let's Encrypt) | 0€ (gratuit) |
| **TOTAL**                      | **15€**      |

#### Coûts Logiciels et Licences

| Outil              | Utilisateurs | Coût/mois | Coût Annuel |
| ------------------ | ------------ | --------- | ----------- |
| GitHub Team        | 5            | 4€ × 5    | 240€        |
| Jira Software      | 5            | 7€ × 5    | 420€        |
| Figma Professional | 2            | 12€ × 2   | 288€        |
| Postman Team       | 5            | 12€ × 5   | 720€        |
| **TOTAL Licences** |              |           | **1 668€**  |

### 16.4 Budget Total du Projet

| Catégorie                          | Montant     | %      |
| ---------------------------------- | ----------- | ------ |
| **Ressources Humaines**            | 48 762€     | 84. 1% |
| **Infrastructure (12 mois)**       | 6 996€      | 12.1%  |
| **Licences logicielles (12 mois)** | 1 668€      | 2.9%   |
| **Nom de domaine**                 | 15€         | 0.0%   |
| **Sous-total**                     | 57 441€     |        |
| **Marge de risque (10%)**          | 5 744€      |        |
| **BUDGET TOTAL**                   | **63 185€** |        |

### 16.5 Répartition Budgétaire par Phase

| Phase                | Coût        | % du Total |
| -------------------- | ----------- | ---------- |
| Initialisation       | 3 588€      | 5.7%       |
| Conception           | 9 282€      | 14.7%      |
| Développement        | 31 896€     | 50.5%      |
| Tests                | 6 900€      | 10.9%      |
| Déploiement          | 6 624€      | 10.5%      |
| Formation & Doc      | 4 692€      | 7.4%       |
| Infrastructure (12m) | 8 679€      | 13.7%      |
| **TOTAL**            | **63 185€** | **100%**   |

### 16.6 Échéancier de Paiement

| Jalon                 | Date     | Montant       | Cumul   |
| --------------------- | -------- | ------------- | ------- |
| Signature contrat     | 01/02/26 | 15 796€ (25%) | 15 796€ |
| Fin conception        | 28/02/26 | 12 637€ (20%) | 28 433€ |
| MVP validé            | 30/04/26 | 18 956€ (30%) | 47 389€ |
| Mise en production    | 30/06/26 | 12 637€ (20%) | 60 026€ |
| Fin garantie (3 mois) | 30/09/26 | 3 159€ (5%)   | 63 185€ |

### 16.7 Analyse de Rentabilité (ROI)

**À compléter selon le contexte business :**

| Indicateur                   | Valeur       |
| ---------------------------- | ------------ |
| Coût total projet            | 63 185€      |
| Gains estimés (année 1)      | [À définir]  |
| Économies estimées (année 1) | [À définir]  |
| ROI prévu                    | [À calculer] |
| Break-even point             | [À calculer] |

### 16.8 Suivi Budgétaire

**Tableau de suivi (à mettre à jour mensuellement) :**

| Mois   | Budget Prévisionnel | Dépenses Réelles | Écart | Cumul Écart |
| ------ | ------------------- | ---------------- | ----- | ----------- |
| Fév 26 | 15 796€             | [... ]           | [...] | [...]       |
| Mar 26 | 12 637€             | [...]            | [...] | [...]       |
| [... ] | [...]               | [...]            | [...] | [...]       |

---

## 17. MAQUETTAGE ET DESIGN

### 17.1 Charte Graphique

#### Palette de Couleurs

```
Couleurs Principales :
- Primary:  #3B82F6 (Bleu)
- Secondary: #8B5CF6 (Violet)
- Success: #10B981 (Vert)
- Warning: #F59E0B (Orange)
- Danger: #EF4444 (Rouge)

Couleurs Neutres :
- Gray 50: #F9FAFB
- Gray 100: #F3F4F6
- Gray 200: #E5E7EB
- Gray 800: #1F2937
- Gray 900: #111827

Texte :
- Primary Text: #111827
- Secondary Text: #6B7280
- Disabled Text: #9CA3AF
```

#### Typographie

```
Police Principale : Inter
- Headings: Inter Bold (700)
- Body: Inter Regular (400)
- Emphasis: Inter Medium (500)

Tailles :
- H1: 2.5rem (40px)
- H2: 2rem (32px)
- H3: 1.5rem (24px)
- Body: 1rem (16px)
- Small: 0.875rem (14px)
```

#### Espacements

```
Système d'espacement (multiples de 4px) :
- xs: 4px
- sm: 8px
- md: 16px
- lg: 24px
- xl: 32px
- 2xl: 48px
```

### 17.2 Wireframes

#### Pages Principales

**Page de Connexion**

```
[Insérer wireframe :  Logo + Formulaire email/password + CTA]
```

**Tableau de Bord**

```
[Insérer wireframe :  Header + Sidebar + Liste tâches + Widgets]
```

**Page Détail Tâche**

```
[Insérer wireframe : Détails + Commentaires + Historique]
```

### 17.3 Maquettes Haute-Fidélité

[Insérer lien Figma ou images des maquettes finales]

- Lien Figma : https://figma.com/file/[...]
- Lien prototype : https://figma.com/proto/[...]

#### Écrans Principaux

1.  Authentification (Login/Register)
2.  Dashboard
3.  Liste des projets
4.  Détail projet
5.  Création/Édition tâche
6.  Profil utilisateur
7.  Paramètres

### 17.4 Accessibilité (RGAA / WCAG)

#### Conformité WCAG 2.1 - Niveau AA

| Critère                         | Implémentation                | Statut |
| ------------------------------- | ----------------------------- | ------ |
| **1.1 Alternatives textuelles** | Attributs alt sur images      | ✅     |
| **1.3 Adaptable**               | Structure sémantique HTML5    | ✅     |
| **1.4 Distinguable**            | Contraste min 4.5:1           | ✅     |
| **2.1 Accessible au clavier**   | Navigation Tab, Focus visible | ✅     |
| **2.4 Navigable**               | Skip links, landmarks ARIA    | ✅     |
| **3.1 Lisible**                 | lang="fr", textes clairs      | ✅     |
| **3.2 Prévisible**              | Navigation cohérente          | ✅     |
| **3.3 Assistance à la saisie**  | Labels, messages d'erreur     | ✅     |
| **4.1 Compatible**              | HTML valide, rôles ARIA       | ✅     |

#### Outils de Test Accessibilité

- **axe DevTools** : Tests automatisés
- **WAVE** : Évaluation visuelle
- **Lighthouse** : Audit Chrome
- **Tests manuels** : Navigation clavier, lecteurs d'écran (NVDA, JAWS)

#### Checklist Accessibilité

- [x] Contraste des couleurs ≥ 4.5:1
- [x] Taille de texte minimum 16px
- [x] Zones cliquables ≥ 44×44px
- [x] Navigation au clavier complète
- [x] Focus visible sur tous les éléments interactifs
- [x] Alternatives textuelles pour les images
- [x] Labels sur tous les formulaires
- [x] Messages d'erreur explicites
- [x] Structure HTML sémantique
- [x] ARIA labels quand nécessaire

### 17.5 Responsive Design

#### Breakpoints

```css
/* Mobile First */
- Mobile: < 640px
- Tablet: 640px - 1024px
- Desktop: > 1024px
- Large Desktop: > 1280px
```

#### Grille Responsive

- Mobile : 1 colonne
- Tablet : 2 colonnes
- Desktop : 3-4 colonnes

[Insérer captures écran responsive]

### 17.6 Système de Design (Design System)

**Composants de base :**

- Buttons (Primary, Secondary, Tertiary, Danger)
- Inputs (Text, Email, Password, Textarea)
- Select / Dropdown
- Checkbox / Radio
- Cards
- Modals
- Tooltips
- Notifications / Toasts
- Loading states
- Empty states

[Lien vers Storybook ou documentation complète]

---

## 18. CONFORMITÉ ET NORMES

### 18.1 RGPD (Règlement Général sur la Protection des Données)

#### Principes Appliqués

| Principe RGPD                    | Application dans le Projet                                |
| -------------------------------- | --------------------------------------------------------- |
| **Licéité**                      | Consentement explicite lors de l'inscription              |
| **Limitation des finalités**     | Données collectées uniquement pour gestion des tâches     |
| **Minimisation**                 | Collecte strictement des données nécessaires              |
| **Exactitude**                   | Possibilité de modification des données par l'utilisateur |
| **Limitation de conservation**   | Suppression données 3 ans après inactivité                |
| **Intégrité et confidentialité** | Chiffrement, HTTPS, accès contrôlé                        |

#### Données Personnelles Traitées

| Donnée               | Finalité                        | Base Légale      | Durée Conservation      |
| -------------------- | ------------------------------- | ---------------- | ----------------------- |
| Nom, Prénom          | Identification                  | Consentement     | Durée du compte + 3 ans |
| Email                | Authentification, communication | Consentement     | Durée du compte + 3 ans |
| Mot de passe (hashé) | Authentification                | Consentement     | Durée du compte         |
| Logs de connexion    | Sécurité                        | Intérêt légitime | 6 mois                  |

#### Droits des Utilisateurs

- ✅ **Droit d'accès** : Export de toutes les données personnelles
- ✅ **Droit de rectification** : Modification du profil
- ✅ **Droit à l'effacement** : Suppression du compte et données
- ✅ **Droit à la limitation** : Suspension temporaire des données
- ✅ **Droit à la portabilité** : Export des données au format JSON/CSV
- ✅ **Droit d'opposition** : Opposition au traitement pour marketing

### 18.1 CNIL (Commission Nationale de l'Informatique et des Libertés)

#### CNIL Recommandations Suivies

| Recommandation CNIL                           | Application dans le Projet                 |
| --------------------------------------------- | ------------------------------------------ |
| **Information claire**                        | Politique de confidentialité détaillée     |
| **Consentement explicite**                    | Cases à cocher non pré-cochées             |
| **Sécurité des données**                      | Chiffrement, audits réguliers              |
| **Notification des violations**               | Processus interne de gestion des incidents |
| **Délégué à la protection des données (DPO)** | Nomination d'un DPO interne                |

### 18.2 Normes de Sécurité

#### Normes Appliquées

| Norme             | Description                                           | Application dans le Projet                         |
| ----------------- | ----------------------------------------------------- | -------------------------------------------------- |
| **ISO/IEC 27001** | Système de management de la sécurité de l'information | Politiques de sécurité, audits réguliers           |
| **OWASP Top 10**  | Principales vulnérabilités web                        | Revues de code, tests de pénétration               |
| **CIS Controls**  | Meilleures pratiques de sécurité                      | Mise en œuvre des contrôles de sécurité essentiels |

#### Mesures de Sécurité Implémentées

| Mesure                             | Description                                                        | Application dans le Projet                          |
| ---------------------------------- | ------------------------------------------------------------------ | --------------------------------------------------- | ---------------------------------------------- |
| **Chiffrement des données**        | Utilisation de TLS pour les communications et chiffrement au repos | Toutes les données sensibles sont chiffrées         |
| **Authentification forte**         | Mécanismes de mot de passe sécurisé et MFA                         |                                                     | Politique de mot de passe strict et option MFA |
| **Gestion des accès**              | Contrôle d'accès basé sur les rôles (RBAC)                         | Accès aux données limité selon les rôles            |
| **Surveillance et journalisation** | Logs d'accès et d'activité                                         | Surveillance continue et alertes en cas d'anomalies |
| **Tests de sécurité**              | Tests de pénétration réguliers                                     | Identification et correction des vulnérabilités     |

### 18.3 Conformité aux Normes Industrielles

#### Normes Industrielles Respectées

| Norme       | Description                                                 | Application dans le Projet                              |
| ----------- | ----------------------------------------------------------- | ------------------------------------------------------- |
| **PCI-DSS** | Norme de sécurité pour les données de cartes de paiement    | Si traitement des paiements, conformité PCI-DSS assurée |
| **HIPAA**   | Norme de sécurité pour les données de santé (si applicable) | Si données de santé, conformité HIPAA assurée           |
| **GDPR**    | Règlement général sur la protection des données             | Conformité RGPD assurée                                 |

### 18.4 Audits et Vérifications

| Type d'Audit          | Fréquence   | Responsable     | Objectif                             |
| --------------------- | ----------- | --------------- | ------------------------------------ |
| **Audit de sécurité** | Annuel      | Équipe Sécurité | Vérification des mesures de sécurité |
| **Audit RGPD**        | Bi-annuel   | DPO             | Vérification de la conformité RGPD   |
| **Audit interne**     | Trimestriel | Équipe Projet   | Revue des processus et pratiques     |

## 19. Bilan projet

[À compléter à la fin du projet]
