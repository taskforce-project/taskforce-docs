# Cahier des Charges Technique (CdCT)

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Introduction](#1-introduction)
- [2. Architecture du système](#2-architecture-du-système)
- [3. Stack Technologique](#3-stack-technologique)
- [4. Modélisation des Données](#4-modélisation-des-données)
- [5. Interfaces et API](#5-interfaces-et-api)
- [6. Sécurité](#6-sécurité)
- [7. Stratégie de Tests](#7-stratégie-de-tests)
- [8. Déploiement et CI/CD](#8-déploiement-et-cicd)

---

## 1. Introduction
Ce document détaille les choix techniques, l'architecture et les normes de développement pour le projet **TaskForce**. Il guide l'équipe de développement dans la mise en œuvre de la solution.

---

## 2. Architecture du système

### 2.1 Architecture Globale
L'application repose sur une architecture **n-tiers** modulaire, facilitant la maintenance et l'évolution vers des microservices si nécessaire.

*   **Client (Front-end)** : Application Web SPA (Single Page Application).
*   **Serveur (Back-end)** : API RESTful exposant les services métiers.
*   **Service IA** : Microservice dédié aux calculs d'optimisation et d'analyse.
*   **Données** : Base de données relationnelle pour le stockage persistant.

### 2.2 Diagramme d'Architecture Logique
*(Voir schéma d'architecture dans le dossier `assets/diagrammes`)*
1.  Le client communique avec le Back-end via HTTPS/REST.
2.  Le Back-end gère l'authentification, la logique métier et la persistance.
3.  Pour les assignations complexes, le Back-end interroge le Service IA via gRPC ou REST interne.

---

## 3. Stack Technologique

### 3.1 Back-end (Core)
*   **Langage** : Java 21 (LTS).
*   **Framework** : Spring Boot 3.2.
*   **Sécurité** : Spring Security 6 (JWT, OAuth2 Resource Server).
*   **ORM** : Hibernate / Spring Data JPA.
*   **Build Tool** : Maven.

### 3.2 Front-end
*   **Framework** : Next.js 14 (App Router).
*   **Langage** : TypeScript.
*   **Styling** : Tailwind CSS.
*   **Composants** : Shadcn/ui (basé sur Radix UI).
*   **State Management** : React Context / Zustand / TanStack Query.

### 3.3 Service Intelligence Artificielle
*   **Langage** : Python 3.11.
*   **Framework API** : FastAPI (haute performance).
*   **Bibliothèques** :
    *   *Scikit-learn* : Pour les algorithmes de classification et de régression (matching compétences).
    *   *Pandas/NumPy* : Manipulation de données.
    *   *NLTK/Spacy* : Analyse sémantique des descriptions de tâches.

### 3.4 Base de Données
*   **SGBD** : PostgreSQL 16.
*   **Migration** : Flyway ou Liquibase pour le versionning du schéma.

### 3.5 Infrastructure & Outils
*   **Conteneurisation** : Docker, Docker Compose (pour le dev).
*   **Versionning** : Git (GitHub/GitLab).

---

## 4. Modélisation des Données

### 4.1 Schéma Conceptuel (Simplifié)
*   **User** (id, email, password, role, availability_score)
*   **Skill** (id, name, category)
*   **UserSkill** (user_id, skill_id, level)
*   **Project** (id, name, start_date, end_date, budget)
*   **Task** (id, title, description, status, priority, estimated_time, project_id, assigned_user_id)
*   **TaskSkillRequirement** (task_id, skill_id, min_level)

---

## 5. Interfaces et API

### 5.1 Standards API
*   Architecture **REST**.
*   Format d'échange : **JSON**.
*   Documentation : **OpenAPI 3.0 (Swagger)** générée automatiquement (SpringDoc).

### 5.2 Endpoints Principaux (Exemples)
*   `POST /api/auth/login` : Authentification.
*   `GET /api/tasks` : Liste des tâches (filtres, pagination).
*   `POST /api/tasks/{id}/assign` : Assigner une tâche (manuel).
*   `POST /api/ai/recommendations` : Demander des suggestions d'assignation.

---

## 6. Sécurité

### 6.1 Sécurité Applicative
*   **Authentification** : Stateless via **JWT (JSON Web Tokens)**.
*   **Autorisation** : RBAC (Role-Based Access Control) strict (Admin, Manager, User).
*   **Mots de passe** : Hachage fort (Argon2 ou BCrypt).
*   **Protection** : CSRF (si cookies utilisés), CORS configuré strictement, Input Sanitization (contre XSS/SQLi).

### 6.2 Sécurité des Données (RGPD)
*   Chiffrement des données sensibles au repos (si nécessaire).
*   Anonymisation des données pour les logs et les environnements de test.
*   Droit à l'oubli (suppression des données personnelles collaborateur).

---

## 7. Stratégie de Tests

*   **Tests Unitaires (Back)** : JUnit 5, Mockito (Couverture cible > 80%).
*   **Tests d'Intégration (Back)** : Spring Boot Test, Testcontainers (PostgreSQL).
*   **Tests Unitaires (Front)** : Jest, React Testing Library.
*   **Tests E2E** : Cypress ou Playwright (Parcours critiques : Login, Création tâche, Assignation).

---

## 8. Déploiement et CI/CD

### 8.1 Environnements
*   **Développement (Local)** : Docker Compose (App + DB + AI).
*   **Staging (Pré-prod)** : Réplique de la prod pour validation.
*   **Production** : Environnement stable et sécurisé.

### 8.2 Pipeline CI/CD (GitHub Actions / GitLab CI)
1.  **Build** : Compilation Java, Transpilation TS.
2.  **Test** : Exécution des tests unitaires.
3.  **Lint/Quality** : SonarQube (analyse statique).
4.  **Package** : Création des images Docker.
5.  **Deploy** : Déploiement automatique sur Staging, manuel sur Prod.
