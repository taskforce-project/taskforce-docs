# 03 - Cahier des Charges Technique (CdCT)

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

---

## 📋 Informations générales

| Champ | Valeur |
|-------|--------|
| **Projet** | TaskForce - Gestion de projets et assignation intelligente |
| **Document** | Cahier des Charges Technique (CdCT) |
| **Auteur** | Michel-Pierre |
| **Date de création** | 4 janvier 2026 |
| **Version** | 1.0 |
| **Statut** | 🔄 En cours de rédaction |

---

## 📖 Sommaire

1. [Introduction](#1-introduction)
2. [Architecture du système](#2-architecture-du-système)
3. [Stack technologique détaillée](#3-stack-technologique-détaillée)
4. [Modélisation des données](#4-modélisation-des-données)
5. [Interfaces et API](#5-interfaces-et-api)
6. [Sécurité](#6-sécurité)
7. [Performance et scalabilité](#7-performance-et-scalabilité)
8. [Infrastructure et hébergement](#8-infrastructure-et-hébergement)
9. [Stratégie de tests](#9-stratégie-de-tests)
10. [CI/CD et déploiement](#10-cicd-et-déploiement)

---

## 1. Introduction

### 1.1 Objet du document

Ce **Cahier des Charges Technique (CdCT)** définit l'architecture, les choix technologiques, les contraintes techniques et les normes de développement du projet **TaskForce**. Il constitue le guide de référence pour :
- L'implémentation technique de l'application
- Les choix d'infrastructure et de déploiement
- Les standards de développement et de qualité
- La sécurité et la performance

### 1.2 Portée technique

Ce document couvre :
- ✅ L'architecture 3-tiers de l'application
- ✅ La stack technologique complète (backend, frontend, BDD)
- ✅ Le modèle de données (MCD/MLD)
- ✅ Les APIs et interfaces
- ✅ La sécurité applicative et des données
- ✅ L'infrastructure et le déploiement
- ✅ La stratégie de tests et de CI/CD

### 1.3 Références

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Contexte global du projet
- [02_CdCF.md](02_CdCF.md) - Spécifications fonctionnelles
- [08_Conception_Technique.md](../02_REALISATION_ET_CONCEPTION/08_Conception_Technique.md) - Architecture détaillée

---

## 2. Architecture du système

### 2.1 Vision globale - Architecture 3-tiers

> **📌 Note** : Diagramme d'architecture détaillé dans `assets/diagrammes/Architecture_Logicielle.drawio`

```
┌─────────────────────────────────────────────────────────────┐
│                     COUCHE PRÉSENTATION                      │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Frontend SPA (Nuxt 3 + TypeScript + Tailwind)      │   │
│  │  - Pages & Components (Shadcn-vue)                   │   │
│  │  - State Management (Pinia)                          │   │
│  │  - API Client (Fetch/Axios)                          │   │
│  └──────────────────────────────────────────────────────┘   │
└───────────────────────┬─────────────────────────────────────┘
                        │ HTTPS/REST (JSON)
                        │
┌───────────────────────▼─────────────────────────────────────┐
│                    COUCHE MÉTIER (API)                       │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Backend API REST (Spring Boot + Java 17)           │   │
│  │                                                       │   │
│  │  Controllers  →  Services  →  Repositories           │   │
│  │  - AuthController     - UserService                  │   │
│  │  - ProjectController  - ProjectService               │   │
│  │  - TaskController     - TaskService                  │   │
│  │  - TeamController     - SkillMatchingService ⭐      │   │
│  │                                                       │   │
│  │  Security: Spring Security + JWT                     │   │
│  └──────────────────────────────────────────────────────┘   │
└───────────────────────┬─────────────────────────────────────┘
                        │ JDBC/JPA
                        │
┌───────────────────────▼─────────────────────────────────────┐
│                    COUCHE DONNÉES                            │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  PostgreSQL 16                                        │   │
│  │  - Schéma relationnel normalisé (3NF)                │   │
│  │  - Indexes optimisés                                 │   │
│  │  - Contraintes d'intégrité                           │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### 2.2 Architecture applicative (layers)

#### Backend - Architecture en couches (Spring Boot)

```
┌─────────────────────────────────────────────────┐
│         LAYER: Controllers (REST API)           │
│  - Gère les requêtes HTTP                       │
│  - Validation des entrées (@Valid)              │
│  - Sérialisation JSON                           │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│         LAYER: Services (Business Logic)        │
│  - Logique métier                               │
│  - Orchestration des opérations                 │
│  - Gestion des transactions (@Transactional)    │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│         LAYER: Repositories (Data Access)       │
│  - Interface avec la BDD (Spring Data JPA)      │
│  - Requêtes JPQL/SQL                            │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│         LAYER: Entities (Domain Model)          │
│  - Modèle de domaine (JPA Entities)             │
│  - Relations entre entités                      │
└─────────────────────────────────────────────────┘
```

#### Frontend - Architecture composants (Nuxt)

```
┌─────────────────────────────────────────────────┐
│           Pages (app/...)                       │
│  - Routage automatique Nuxt                     │
│  - Layouts partagés                             │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│           Components (components/...)           │
│  - Composants réutilisables (Shadcn-vue)        │
│  - UI components atomiques                      │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│           Composables (composables/...)         │
│  - Logique réutilisable (useAuth, useTask...)   │
│  - Gestion d'état local                         │
└───────────────────┬─────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────┐
│           Stores (stores/...)                   │
│  - Pinia stores (state global)                  │
│  - Persistance locale (localStorage)            │
└─────────────────────────────────────────────────┘
```

### 2.3 Patterns et principes architecturaux

| Pattern/Principe | Application | Justification |
|------------------|-------------|---------------|
| **MVC (Model-View-Controller)** | Backend Spring Boot | Séparation des responsabilités |
| **Repository Pattern** | Accès aux données | Abstraction de la couche données |
| **Service Layer** | Logique métier | Découplage controllers/repositories |
| **DTO (Data Transfer Objects)** | Communication API | Contrôle des données exposées |
| **Dependency Injection** | Tout le backend | Inversion de contrôle, testabilité |
| **RESTful API** | Communication client-serveur | Standard web, stateless |
| **SPA (Single Page App)** | Frontend Nuxt | UX fluide, navigation rapide |

---

## 3. Stack technologique détaillée

### 3.1 Backend - API REST

| Technologie | Version | Rôle | Justification |
|-------------|---------|------|---------------|
| **Java** | 17 (LTS) | Langage principal | Stabilité, écosystème riche, performance |
| **Spring Boot** | 3.2+ | Framework applicatif | Productivité, convention over configuration |
| **Spring Data JPA** | Inclus | ORM | Abstraction de l'accès aux données |
| **Spring Security** | 6.2+ | Sécurité | Authentification JWT, autorisation RBAC |
| **Hibernate** | 6.x | Implémentation JPA | ORM mature et performant |
| **Maven** | 3.9+ | Build tool | Gestion des dépendances, build reproductible |
| **Lombok** | 1.18+ | Réduction boilerplate | Génération automatique getters/setters/@Builder |
| **MapStruct** | 1.5+ | Mapping DTO ↔ Entity | Performance, type-safety |
| **SpringDoc OpenAPI** | 2.3+ | Documentation API | Génération automatique Swagger UI |
| **Jackson** | 2.16+ | Sérialisation JSON | Parser JSON par défaut de Spring |

**Dépendances Maven clés** :
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-api</artifactId>
        <version>0.12.3</version>
    </dependency>
</dependencies>
```

### 3.2 Frontend - SPA

| Technologie | Version | Rôle | Justification |
|-------------|---------|------|---------------|
| **Nuxt** | 3.10+ | Framework Vue.js | SSR/SSG, routage auto, performance |
| **Vue.js** | 3.4+ | Framework UI | Réactivité, composition API, écosystème |
| **TypeScript** | 5.3+ | Langage | Type-safety, meilleure DX, moins de bugs |
| **Tailwind CSS** | 3.4+ | Framework CSS | Utility-first, rapide, customisable |
| **Shadcn-vue** | Latest | Design System | Composants accessibles (Radix-vue) |
| **Pinia** | 2.1+ | State management | Store officiel Vue 3, simple, performant |
| **VueUse** | 10.x | Composables utils | Utilitaires réactifs prêts à l'emploi |
| **Vite** | 5.x | Build tool | HMR ultra-rapide, build optimisé |
| **Zod** | 3.22+ | Validation schéma | Validation côté client type-safe |

**package.json clés** :
```json
{
  "dependencies": {
    "nuxt": "^3.10.0",
    "vue": "^3.4.0",
    "@nuxtjs/tailwindcss": "^6.11.0",
    "shadcn-vue": "latest",
    "pinia": "^2.1.0",
    "@vueuse/core": "^10.7.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "typescript": "^5.3.0",
    "@nuxt/test-utils": "^3.10.0"
  }
}
```

### 3.3 Base de données

| Technologie | Version | Rôle | Justification |
|-------------|---------|------|---------------|
| **PostgreSQL** | 16.x | SGBD relationnel | Fiabilité, ACID, fonctionnalités avancées (JSON, full-text search) |
| **Flyway** | 10.x | Migration BDD | Versionning du schéma, reproductibilité |

**Fonctionnalités PostgreSQL utilisées** :
- Contraintes d'intégrité référentielle
- Indexes B-tree pour performance
- Types JSON pour données flexibles (métadonnées tâches)
- Full-text search (recherche de tâches/projets)

### 3.4 Infrastructure et DevOps

| Technologie | Version | Rôle | Justification |
|-------------|---------|------|---------------|
| **Docker** | 24.x+ | Conteneurisation | Isolation, reproductibilité environnements |
| **Docker Compose** | 2.x+ | Orchestration dev | Multi-conteneurs (app, db, adminer) |
| **Git** | 2.43+ | Versionning | Standard de l'industrie |
| **GitHub** | - | Hosting Git + CI/CD | Gratuit, GitHub Actions intégré |
| **GitHub Actions** | - | CI/CD | Automatisation build/test/deploy |

### 3.5 Outils de développement

| Outil | Usage | Justification |
|-------|-------|---------------|
| **IntelliJ IDEA** | IDE Backend | Meilleur support Java/Spring |
| **VS Code** | IDE Frontend | Léger, excellent support Vue/TypeScript |
| **Postman / Insomnia** | Test API | Interface graphique pour tester les endpoints |
| **Adminer / pgAdmin** | Gestion PostgreSQL | Interface web pour explorer la BDD |
| **Draw.io** | Diagrammes | Gratuit, intégration VSCode possible |

---

## 4. Modélisation des données

> **📌 Note** : MCD et MLD détaillés dans `assets/diagrammes/MCD.drawio` et `assets/diagrammes/MLD.drawio`

### 4.1 Modèle Conceptuel de Données (MCD) - Entités principales

| Entité | Description | Attributs clés |
|--------|-------------|----------------|
| **User** | Utilisateur de la plateforme | id, email, password_hash, first_name, last_name, role, avatar_url, created_at |
| **Skill** | Compétence technique ou soft skill | id, name, category (LANGUAGE, FRAMEWORK, TOOL, SOFT_SKILL), description |
| **UserSkill** | Compétences d'un utilisateur avec niveau | user_id, skill_id, level (1-5), years_experience |
| **Team** | Équipe de collaborateurs | id, name, description, manager_id, created_at |
| **TeamMember** | Appartenance à une équipe | team_id, user_id, role (MANAGER, MEMBER), joined_at |
| **Project** | Projet contenant des tâches | id, name, description, start_date, end_date, status, team_id |
| **Task** | Tâche assignable à un utilisateur | id, title, description, status, priority, estimated_hours, deadline, project_id, assigned_user_id |
| **TaskSkill** | Compétences requises pour une tâche | task_id, skill_id, min_level |
| **Comment** | Commentaire sur une tâche | id, task_id, user_id, content, created_at |
| **Attachment** | Fichier joint à une tâche | id, task_id, filename, file_url, file_size, uploaded_at |
| **Notification** | Notification in-app | id, user_id, type, content, is_read, created_at |

### 4.2 Relations principales

```
User (1) ──── (N) UserSkill (N) ──── (1) Skill
User (1) ──── (N) TeamMember (N) ──── (1) Team
User (1) ──── (N) Task [assigned_user_id]
Team (1) ──── (N) Project
Project (1) ──── (N) Task
Task (1) ──── (N) TaskSkill (N) ──── (1) Skill
Task (1) ──── (N) Comment (N) ──── (1) User
Task (1) ──── (N) Attachment
User (1) ──── (N) Notification
```

### 4.3 Modèle Logique de Données (MLD) - Tables PostgreSQL

```sql
-- Table users
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    role VARCHAR(20) NOT NULL DEFAULT 'USER', -- USER, MANAGER, ADMIN
    avatar_url VARCHAR(500),
    bio TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table skills
CREATE TABLE skills (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    category VARCHAR(50) NOT NULL, -- LANGUAGE, FRAMEWORK, TOOL, SOFT_SKILL
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table user_skills
CREATE TABLE user_skills (
    user_id BIGINT REFERENCES users(id) ON DELETE CASCADE,
    skill_id BIGINT REFERENCES skills(id) ON DELETE CASCADE,
    level INTEGER CHECK (level BETWEEN 1 AND 5),
    years_experience DECIMAL(3,1),
    PRIMARY KEY (user_id, skill_id)
);

-- Table teams
CREATE TABLE teams (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    manager_id BIGINT REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table team_members
CREATE TABLE team_members (
    team_id BIGINT REFERENCES teams(id) ON DELETE CASCADE,
    user_id BIGINT REFERENCES users(id) ON DELETE CASCADE,
    role VARCHAR(20) DEFAULT 'MEMBER', -- MANAGER, MEMBER
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (team_id, user_id)
);

-- Table projects
CREATE TABLE projects (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    start_date DATE,
    end_date DATE,
    status VARCHAR(50) DEFAULT 'ACTIVE', -- ACTIVE, COMPLETED, ARCHIVED
    team_id BIGINT REFERENCES teams(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table tasks
CREATE TABLE tasks (
    id BIGSERIAL PRIMARY KEY,
    title VARCHAR(300) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'TODO', -- TODO, IN_PROGRESS, DONE
    priority VARCHAR(20) DEFAULT 'MEDIUM', -- LOW, MEDIUM, HIGH, CRITICAL
    estimated_hours DECIMAL(5,2),
    deadline TIMESTAMP,
    project_id BIGINT REFERENCES projects(id) ON DELETE CASCADE,
    assigned_user_id BIGINT REFERENCES users(id) ON DELETE SET NULL,
    created_by BIGINT REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table task_skills
CREATE TABLE task_skills (
    task_id BIGINT REFERENCES tasks(id) ON DELETE CASCADE,
    skill_id BIGINT REFERENCES skills(id) ON DELETE CASCADE,
    min_level INTEGER CHECK (min_level BETWEEN 1 AND 5),
    PRIMARY KEY (task_id, skill_id)
);

-- Table comments
CREATE TABLE comments (
    id BIGSERIAL PRIMARY KEY,
    task_id BIGINT REFERENCES tasks(id) ON DELETE CASCADE,
    user_id BIGINT REFERENCES users(id),
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table attachments
CREATE TABLE attachments (
    id BIGSERIAL PRIMARY KEY,
    task_id BIGINT REFERENCES tasks(id) ON DELETE CASCADE,
    filename VARCHAR(255) NOT NULL,
    file_url VARCHAR(500) NOT NULL,
    file_size BIGINT,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table notifications
CREATE TABLE notifications (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT REFERENCES users(id) ON DELETE CASCADE,
    type VARCHAR(50) NOT NULL, -- TASK_ASSIGNED, COMMENT_ADDED, DEADLINE_APPROACHING, etc.
    content TEXT NOT NULL,
    is_read BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Indexes pour performance
CREATE INDEX idx_tasks_project ON tasks(project_id);
CREATE INDEX idx_tasks_assigned_user ON tasks(assigned_user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_comments_task ON comments(task_id);
CREATE INDEX idx_notifications_user ON notifications(user_id);
CREATE INDEX idx_notifications_unread ON notifications(user_id, is_read);
```

### 4.4 Normalisation

- **1NF** : Tous les attributs sont atomiques ✅
- **2NF** : Pas de dépendances fonctionnelles partielles ✅
- **3NF** : Pas de dépendances transitives ✅

---

## 5. Interfaces et API

### 5.1 Standards et conventions API REST

| Convention | Implémentation |
|------------|----------------|
| **Format** | JSON (application/json) |
| **Versionning** | Préfixe `/api/v1/` |
| **HTTP Verbs** | GET (lecture), POST (création), PUT (update complet), PATCH (update partiel), DELETE (suppression) |
| **Status codes** | 200 (OK), 201 (Created), 204 (No Content), 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 500 (Internal Error) |
| **Pagination** | Query params: `?page=0&size=20&sort=createdAt,desc` |
| **Filtrage** | Query params: `?status=TODO&priority=HIGH` |
| **Naming** | camelCase pour JSON, kebab-case pour URLs |

### 5.2 Endpoints API - Authentification

| Méthode | Endpoint | Description | Req Body | Res Body |
|---------|----------|-------------|----------|----------|
| POST | `/api/v1/auth/register` | Inscription | `{email, password, firstName, lastName}` | `{id, email, message}` |
| POST | `/api/v1/auth/login` | Connexion | `{email, password}` | `{token, refreshToken, user}` |
| POST | `/api/v1/auth/refresh` | Refresh token | `{refreshToken}` | `{token}` |
| POST | `/api/v1/auth/logout` | Déconnexion | - | `{message}` |
| POST | `/api/v1/auth/forgot-password` | Réinit MDP | `{email}` | `{message}` |
| POST | `/api/v1/auth/reset-password` | Nouveau MDP | `{token, newPassword}` | `{message}` |

### 5.3 Endpoints API - Users & Skills

| Méthode | Endpoint | Description | Auth | Req Body |
|---------|----------|-------------|------|----------|
| GET | `/api/v1/users/me` | Profil utilisateur connecté | ✅ | - |
| PUT | `/api/v1/users/me` | Modifier mon profil | ✅ | `{firstName, lastName, bio, avatarUrl}` |
| POST | `/api/v1/users/me/skills` | Ajouter une compétence | ✅ | `{skillId, level, yearsExperience}` |
| PUT | `/api/v1/users/me/skills/{skillId}` | Modifier niveau compétence | ✅ | `{level, yearsExperience}` |
| DELETE | `/api/v1/users/me/skills/{skillId}` | Supprimer une compétence | ✅ | - |
| GET | `/api/v1/skills` | Liste des compétences | ✅ | - |
| POST | `/api/v1/skills` | Créer une compétence (Admin) | ✅ | `{name, category, description}` |

### 5.4 Endpoints API - Teams

| Méthode | Endpoint | Description | Auth | Req Body |
|---------|----------|-------------|------|----------|
| GET | `/api/v1/teams` | Liste des équipes | ✅ | - |
| POST | `/api/v1/teams` | Créer une équipe | ✅ | `{name, description}` |
| GET | `/api/v1/teams/{id}` | Détail équipe | ✅ | - |
| PUT | `/api/v1/teams/{id}` | Modifier équipe | ✅ | `{name, description}` |
| DELETE | `/api/v1/teams/{id}` | Supprimer équipe | ✅ | - |
| POST | `/api/v1/teams/{id}/members` | Ajouter membre | ✅ | `{userId, role}` |
| DELETE | `/api/v1/teams/{id}/members/{userId}` | Retirer membre | ✅ | - |
| GET | `/api/v1/teams/{id}/skills` | Compétences agrégées | ✅ | - |

### 5.5 Endpoints API - Projects

| Méthode | Endpoint | Description | Auth | Req Body |
|---------|----------|-------------|------|----------|
| GET | `/api/v1/projects` | Liste projets | ✅ | - |
| POST | `/api/v1/projects` | Créer projet | ✅ | `{name, description, startDate, endDate, teamId}` |
| GET | `/api/v1/projects/{id}` | Détail projet | ✅ | - |
| PUT | `/api/v1/projects/{id}` | Modifier projet | ✅ | `{name, description, startDate, endDate}` |
| PATCH | `/api/v1/projects/{id}/status` | Changer statut | ✅ | `{status}` |
| DELETE | `/api/v1/projects/{id}` | Archiver projet | ✅ | - |

### 5.6 Endpoints API - Tasks

| Méthode | Endpoint | Description | Auth | Req Body |
|---------|----------|-------------|------|----------|
| GET | `/api/v1/tasks` | Liste tâches (avec filtres) | ✅ | - |
| POST | `/api/v1/tasks` | Créer tâche | ✅ | `{title, description, projectId, estimatedHours, priority, deadline, skills[]}` |
| GET | `/api/v1/tasks/{id}` | Détail tâche | ✅ | - |
| PUT | `/api/v1/tasks/{id}` | Modifier tâche | ✅ | `{title, description, estimatedHours, deadline}` |
| PATCH | `/api/v1/tasks/{id}/status` | Changer statut | ✅ | `{status}` |
| POST | `/api/v1/tasks/{id}/assign` | Assigner manuellement | ✅ | `{userId}` |
| GET | `/api/v1/tasks/{id}/suggestions` | Suggestions assignation ⭐ | ✅ | - |
| POST | `/api/v1/tasks/{id}/comments` | Ajouter commentaire | ✅ | `{content}` |
| POST | `/api/v1/tasks/{id}/attachments` | Uploader fichier | ✅ | FormData |
| DELETE | `/api/v1/tasks/{id}` | Supprimer tâche | ✅ | - |

### 5.7 Endpoints API - Dashboards & Notifications

| Méthode | Endpoint | Description | Auth |
|---------|----------|-------------|------|
| GET | `/api/v1/dashboard/me` | Mon dashboard (tâches du jour, stats) | ✅ |
| GET | `/api/v1/dashboard/team/{teamId}` | Dashboard équipe (heatmap) | ✅ |
| GET | `/api/v1/notifications` | Mes notifications | ✅ |
| PATCH | `/api/v1/notifications/{id}/read` | Marquer comme lu | ✅ |
| PATCH | `/api/v1/notifications/read-all` | Tout marquer comme lu | ✅ |

### 5.8 Documentation automatique - Swagger/OpenAPI

**URL** : `http://localhost:8080/swagger-ui.html`

Configuration Spring Boot :
```yaml
springdoc:
  api-docs:
    path: /api-docs
  swagger-ui:
    path: /swagger-ui.html
    operations-sorter: method
    tags-sorter: alpha
```

---

## 6. Sécurité

---

## 6. Sécurité

### 6.1 Authentification - JWT (JSON Web Tokens)

**Flux d'authentification** :
1. User envoie `POST /api/v1/auth/login` avec `{email, password}`
2. Backend vérifie credentials (BCrypt)
3. Si OK : génération de 2 tokens
   - **Access Token** (JWT) : expire en 24h, contient {userId, email, role}
   - **Refresh Token** : expire en 7 jours, stocké en BDD
4. Retour : `{token, refreshToken, user: {...}}`
5. Client stocke le token (localStorage ou httpOnly cookie)
6. Chaque requête API inclut header : `Authorization: Bearer <token>`

**Structure JWT** :
```json
{
  "sub": "user@example.com",
  "userId": 123,
  "role": "USER",
  "iat": 1704360000,
  "exp": 1704446400
}
```

**Sécurité JWT** :
- Signature avec secret fort (HS256 ou RS256)
- Validation de l'expiration à chaque requête
- Révocation via blacklist (optionnel) ou rotation des secrets

### 6.2 Autorisation - RBAC (Role-Based Access Control)

**Rôles définis** :
- **USER** : Collaborateur standard (CRUD sur ses tâches, vue projets assignés)
- **MANAGER** : Chef d'équipe (+ création projets/tâches, assignation, vue équipe)
- **ADMIN** : Administrateur système (+ gestion utilisateurs, logs, configuration)

**Matrice de droits** :

| Resource | USER | MANAGER | ADMIN |
|----------|------|---------|-------|
| Lire ses tâches | ✅ | ✅ | ✅ |
| Créer une tâche | ❌ | ✅ | ✅ |
| Assigner une tâche | ❌ | ✅ | ✅ |
| Créer un projet | ❌ | ✅ | ✅ |
| Voir tous les utilisateurs | ❌ | ⚠️ Team only | ✅ |
| Gérer les utilisateurs | ❌ | ❌ | ✅ |
| Voir les logs système | ❌ | ❌ | ✅ |

**Implémentation Spring Security** :
```java
@PreAuthorize("hasRole('MANAGER')")
public ResponseEntity<TaskDTO> createTask(@RequestBody TaskDTO dto) {
    // ...
}

@PreAuthorize("hasRole('ADMIN')")
public ResponseEntity<List<UserDTO>> getAllUsers() {
    // ...
}
```

### 6.3 Protection des données

#### Hashage des mots de passe
- **Algorithme** : BCrypt (cost factor = 12)
- **Salage** : Automatique par BCrypt
- **Jamais de stockage en clair**

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder(12);
}
```

#### Validation et Sanitization
- **Côté backend** : Bean Validation (@Valid, @NotNull, @Email, @Size)
- **Contre XSS** : Échappement HTML automatique (Thymeleaf, Jackson)
- **Contre SQLi** : Utilisation exclusive de prepared statements (JPA)

#### CORS (Cross-Origin Resource Sharing)
```java
@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                    .allowedOrigins("http://localhost:3000") // Frontend dev
                    .allowedMethods("GET", "POST", "PUT", "PATCH", "DELETE")
                    .allowedHeaders("*")
                    .allowCredentials(true);
            }
        };
    }
}
```

#### Protection CSRF
- **API REST** : Désactivée (stateless avec JWT)
- **Si cookies utilisés** : Tokens CSRF obligatoires

#### Rate Limiting
- **Bucket4j** : Limite à 100 req/min par IP
- Protection contre brute-force sur `/api/v1/auth/login` : 5 tentatives/15min

### 6.4 HTTPS et Transport

- **TLS 1.3** obligatoire en production
- **Certificat SSL** : Let's Encrypt (gratuit) ou certificat payant
- **HSTS** : Header `Strict-Transport-Security: max-age=31536000`

### 6.5 Conformité RGPD

| Exigence RGPD | Implémentation |
|---------------|----------------|
| **Consentement** | Checkbox explicite à l'inscription |
| **Droit d'accès** | Endpoint `GET /api/v1/users/me/data` (export JSON) |
| **Droit à l'oubli** | Endpoint `DELETE /api/v1/users/me` (soft delete puis purge 30j) |
| **Portabilité** | Export JSON de toutes les données utilisateur |
| **Minimisation** | Collecte uniquement des données nécessaires |
| **Chiffrement** | TLS en transit, hachage BCrypt pour passwords |

---

## 7. Performance et scalabilité

### 7.1 Optimisations backend

| Technique | Implémentation | Gain |
|-----------|----------------|------|
| **Lazy Loading** | JPA `FetchType.LAZY` par défaut | Réduction requêtes N+1 |
| **Pagination** | `Pageable` Spring Data | Limite résultats API |
| **Caching** | Spring Cache (@Cacheable) sur skills, users | -50% requêtes BDD |
| **Indexes BDD** | Sur foreign keys et colonnes filtrées | Requêtes 10x plus rapides |
| **Connection Pooling** | HikariCP (default Spring Boot) | Réutilisation connexions |
| **Async Processing** | @Async pour emails, notifications | Non-bloquant |

**Configuration HikariCP** :
```yaml
spring:
  datasource:
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      connection-timeout: 30000
```

### 7.2 Optimisations frontend

| Technique | Implémentation | Gain |
|-----------|----------------|------|
| **Code Splitting** | Nuxt lazy loading routes | First Load < 200KB |
| **Tree Shaking** | Vite élimination dead code | Bundle -30% |
| **Image Optimization** | Nuxt Image avec formats WebP/AVIF | Images -60% |
| **Lazy Loading Images** | `loading="lazy"` | Faster initial paint |
| **Debouncing** | Sur recherche/autocomplete (300ms) | -80% requêtes API |
| **Client-side Caching** | TanStack Query avec staleTime | Moins de re-fetch |

### 7.3 Métriques de performance cibles

| Métrique | Valeur cible | Outil de mesure |
|----------|--------------|-----------------|
| **TTFB** (Time To First Byte) | < 100ms | Lighthouse |
| **FCP** (First Contentful Paint) | < 1s | Lighthouse |
| **LCP** (Largest Contentful Paint) | < 2.5s | Lighthouse |
| **API Response Time (P95)** | < 200ms | Spring Actuator |
| **Database Query Time** | < 50ms | PostgreSQL logs |
| **Lighthouse Score** | > 90 | Chrome DevTools |

---

## 8. Infrastructure et hébergement

### 8.1 Architecture de déploiement

> **📌 Note** : Diagramme de déploiement dans `assets/diagrammes/Diagramme_Deploiement.drawio`

**Environnement de développement (local)** :
```
Docker Compose:
├── tf-api (Spring Boot)       :8080
├── tf-frontend (Nuxt)          :3000
├── postgres                    :5432
└── adminer (DB admin)          :8081
```

**Environnement de production (cloud)** :
```
┌─────────────────────────────────────────┐
│  CDN / Static Assets (Vercel/Netlify)  │
│  - Frontend SSR/SSG                     │
└──────────────┬──────────────────────────┘
               │ HTTPS
┌──────────────▼──────────────────────────┐
│  Reverse Proxy / Load Balancer (Nginx) │
└──────────────┬──────────────────────────┘
               │
┌──────────────▼──────────────────────────┐
│  Backend API (Docker Container)         │
│  - Spring Boot sur port 8080            │
└──────────────┬──────────────────────────┘
               │ JDBC
┌──────────────▼──────────────────────────┐
│  PostgreSQL Database (Managed Service)  │
│  - Backups automatiques                 │
└─────────────────────────────────────────┘
```

### 8.2 Options d'hébergement (gratuites/low-cost)

| Service | Usage | Prix | Limites |
|---------|-------|------|---------|
| **Render.com** | Backend + BDD PostgreSQL | Gratuit | Sleep après 15min inactivité |
| **Railway.app** | Backend + BDD | $5/mois | 500h/mois d'exécution |
| **Vercel** | Frontend Nuxt (SSR/SSG) | Gratuit | 100GB bandwidth |
| **Netlify** | Frontend (alternative) | Gratuit | 100GB bandwidth |
| **Supabase** | PostgreSQL gratuit | Gratuit | 500MB DB, 2GB bandwidth |
| **Neon.tech** | PostgreSQL serverless | Gratuit | 3GB storage |

**Recommandation MVP** : **Render (Free tier)** pour tout-en-un ou **Vercel + Railway** pour séparer frontend/backend.

### 8.3 Conteneurisation - Docker

**Dockerfile Backend (Spring Boot)** :
```dockerfile
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/tf-api-*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Dockerfile Frontend (Nuxt)** :
```dockerfile
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=build /app/.output ./.output
EXPOSE 3000
CMD ["node", ".output/server/index.mjs"]
```

**docker-compose.yml (développement)** :
```yaml
version: '3.8'
services:
  postgres:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: taskforce
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  backend:
    build: ./backend
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/taskforce
      SPRING_DATASOURCE_USERNAME: admin
      SPRING_DATASOURCE_PASSWORD: secret
    depends_on:
      - postgres

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      API_BASE_URL: http://backend:8080

volumes:
  postgres_data:
```

---

## 9. Stratégie de tests

### 9.1 Pyramide des tests

```
           ┌─────────┐
           │   E2E   │  (5% - Parcours critiques)
           └─────────┘
         ┌─────────────┐
         │ Intégration │  (25% - APIs, BDD)
         └─────────────┘
      ┌──────────────────┐
      │    Unitaires     │  (70% - Logique métier)
      └──────────────────┘
```

### 9.2 Tests Backend (Spring Boot)

#### Tests unitaires (JUnit 5 + Mockito)
```java
@ExtendWith(MockitoExtension.class)
class TaskServiceTest {
    @Mock
    private TaskRepository taskRepository;
    
    @InjectMocks
    private TaskService taskService;
    
    @Test
    void shouldCreateTask() {
        // Given
        TaskDTO dto = new TaskDTO("New Task", ...);
        when(taskRepository.save(any())).thenReturn(taskEntity);
        
        // When
        TaskDTO result = taskService.createTask(dto);
        
        // Then
        assertNotNull(result.getId());
        verify(taskRepository, times(1)).save(any());
    }
}
```

#### Tests d'intégration (Testcontainers)
```java
@SpringBootTest
@Testcontainers
class TaskControllerIntegrationTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:16-alpine");
    
    @Autowired
    private MockMvc mockMvc;
    
    @Test
    void shouldCreateTaskViaAPI() throws Exception {
        mockMvc.perform(post("/api/v1/tasks")
                .contentType(MediaType.APPLICATION_JSON)
                .content("{\"title\":\"Test Task\"}"))
            .andExpect(status().isCreated())
            .andExpect(jsonPath("$.id").exists());
    }
}
```

### 9.3 Tests Frontend (Vitest + Vue Test Utils)

#### Test composant
```typescript
import { mount } from '@vue/test-utils'
import { describe, it, expect } from 'vitest'
import TaskCard from '@/components/TaskCard.vue'

describe('TaskCard.vue', () => {
  it('renders task title', () => {
    const wrapper = mount(TaskCard, {
      props: {
        task: { id: 1, title: 'Test Task', status: 'TODO' }
      }
    })
    expect(wrapper.text()).toContain('Test Task')
  })
})
```

### 9.4 Tests E2E (Playwright)

```typescript
import { test, expect } from '@playwright/test'

test('user can create a task', async ({ page }) => {
  await page.goto('http://localhost:3000/login')
  await page.fill('input[name="email"]', 'test@example.com')
  await page.fill('input[name="password"]', 'password123')
  await page.click('button[type="submit"]')
  
  await page.goto('http://localhost:3000/projects/1')
  await page.click('button:has-text("New Task")')
  await page.fill('input[name="title"]', 'My new task')
  await page.click('button:has-text("Create")')
  
  await expect(page.locator('text=My new task')).toBeVisible()
})
```

### 9.5 Couverture de tests cible

| Type | Couverture cible | Outil |
|------|------------------|-------|
| **Backend** | ≥ 80% | JaCoCo |
| **Frontend** | ≥ 70% | Vitest Coverage |
| **E2E** | Parcours critiques (auth, création tâche, assignation) | Playwright |

---

## 10. CI/CD et déploiement

### 10.1 Pipeline GitHub Actions

**.github/workflows/ci-cd.yml** :
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  backend-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
      - name: Run tests
        run: |
          cd backend
          mvn clean test
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  frontend-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      - name: Install and test
        run: |
          cd frontend
          npm ci
          npm run test
          npm run build

  deploy-staging:
    needs: [backend-tests, frontend-tests]
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Render (staging)
        run: |
          curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK_STAGING }}

  deploy-production:
    needs: [backend-tests, frontend-tests]
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Render (production)
        run: |
          curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK_PROD }}
```

### 10.2 Stratégie de branches Git

```
main (production)
  ├── develop (staging)
  │     ├── feature/US-001-auth
  │     ├── feature/US-002-profile
  │     └── bugfix/fix-login-issue
  └── hotfix/critical-security-patch
```

**Workflow** :
1. Feature branch depuis `develop` : `feature/US-XXX-description`
2. Pull Request vers `develop` → Tests automatiques
3. Merge → Déploiement auto sur staging
4. Tests manuels sur staging
5. PR de `develop` vers `main` → Déploiement production

### 10.3 Gestion des versions

- **Semantic Versioning** : `v1.0.0`, `v1.1.0`, `v2.0.0`
- **Tags Git** : `git tag -a v1.0.0 -m "First release"`
- **Changelog** : Fichier `CHANGELOG.md` mis à jour à chaque release

---

## 📎 Annexes

### A. Documents liés

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Vision globale du projet
- [02_CdCF.md](02_CdCF.md) - Spécifications fonctionnelles
- [08_Conception_Technique.md](../02_REALISATION_ET_CONCEPTION/08_Conception_Technique.md) - Architecture détaillée
- [09_API_Documentation.md](../02_REALISATION_ET_CONCEPTION/09_API_Documentation.md) - Documentation complète des APIs
- [10_Convention_Code.md](../02_REALISATION_ET_CONCEPTION/10_Convention_Code.md) - Standards de code

### B. Diagrammes techniques à créer

- `assets/diagrammes/Architecture_Logicielle.drawio` - Architecture 3-tiers
- `assets/diagrammes/Diagramme_Deploiement.drawio` - Infrastructure de déploiement
- `assets/diagrammes/MCD.drawio` - Modèle Conceptuel de Données
- `assets/diagrammes/MLD.drawio` - Modèle Logique de Données
- `assets/diagrammes/Diagrammes_Sequence.drawio` - Flux d'authentification, création tâche, matching

### C. Ressources et documentation

| Ressource | URL |
|-----------|-----|
| **Spring Boot Docs** | https://spring.io/projects/spring-boot |
| **Nuxt 3 Docs** | https://nuxt.com |
| **PostgreSQL Docs** | https://www.postgresql.org/docs/ |
| **JWT.io** | https://jwt.io |
| **Shadcn-vue** | https://www.shadcn-vue.com |

### D. Historique des versions

| Version | Date | Auteur | Modifications |
|---------|------|--------|---------------|
| 1.0 | 04/01/2026 | Michel-Pierre | Création complète du CdCT |

---

**Document validé par** : Michel-Pierre  
**Date de validation** : 04/01/2026  
**Prochaine revue prévue** : 15/01/2026
