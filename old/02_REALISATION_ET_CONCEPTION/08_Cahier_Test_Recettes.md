# Cahier de Tests et Recettes

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Introduction](#1-introduction)
- [2. Objectifs des tests](#2-objectifs-des-tests)
- [3. Stratégie de test](#3-stratégie-de-test)
- [4. Cas de test](#4-cas-de-test)
- [5. Critères d'acceptation](#5-critères-dacceptation)
- [6. Plan de recette](#6-plan-de-recette)
- [7. Annexes](#7-annexes)

---

## 1. Introduction

### 1.1 Objectif du Document
Ce document définit la stratégie, les méthodes et les cas de tests pour l'application **TaskForce**. Il garantit la qualité, la fiabilité et la conformité du produit avec les spécifications fonctionnelles et techniques.

### 1.2 Portée
Les tests couvrent :
- **Tests unitaires** (Backend & Frontend)
- **Tests d'intégration** (API, Base de données)
- **Tests End-to-End (E2E)** (Parcours utilisateurs complets)
- **Tests de sécurité** (Authentification, autorisation, injection)
- **Tests de performance** (Charge, stress)
- **Recette utilisateur** (Validation fonctionnelle)

---

## 2. Objectifs des tests

### 2.1 Objectifs Généraux
1. **Garantir la conformité** avec les spécifications du CdCF et CdCT
2. **Détecter les bugs** avant la mise en production
3. **Assurer la non-régression** lors des évolutions
4. **Valider l'expérience utilisateur** (UX/UI)
5. **Vérifier la sécurité** et la robustesse du système

### 2.2 Critères de Qualité
- **Couverture de code** : Minimum 80% pour le backend, 70% pour le frontend
- **Taux de succès** : 100% des tests doivent passer avant merge
- **Performance** : Temps de réponse API < 200ms (95e percentile)
- **Accessibilité** : Conformité WCAG 2.1 niveau AA

---

## 3. Stratégie de test

### 3.1 Pyramide de Tests

```
           /\
          /  \    E2E Tests (10%)
         /────\   Parcours critiques
        /      \
       /────────\  Integration Tests (30%)
      /          \ API, Database
     /────────────\
    /              \ Unit Tests (60%)
   /________________\ Logique métier
```

### 3.2 Types de Tests

#### 3.2.1 Tests Unitaires

**Backend (Java - JUnit 5 + Mockito)**
- Tests des Use Cases (application layer)
- Tests des services métier (domain layer)
- Tests des repositories (mocking)

**Frontend (TypeScript - Jest + React Testing Library)**
- Tests des composants React
- Tests des hooks personnalisés
- Tests des utilitaires

**Outils** :
- JUnit 5, Mockito, AssertJ (Backend)
- Jest, React Testing Library (Frontend)

**Exécution** : À chaque commit (pre-commit hook)

#### 3.2.2 Tests d'Intégration

**Backend**
- Tests des endpoints API (REST)
- Tests avec base de données réelle (Testcontainers PostgreSQL)
- Tests de sécurité (JWT, autorisations)

**Outils** :
- Spring Boot Test, Testcontainers, RestAssured

**Exécution** : CI/CD à chaque push

#### 3.2.3 Tests End-to-End (E2E)

**Parcours Utilisateur Complets**
- Authentification → Dashboard → Création tâche → Assignation
- Manager : Création projet → Ajout équipe → Vue Kanban
- Collaborateur : Mise à jour statut tâche → Ajout commentaire

**Outils** :
- **Cypress** (principal)
- Playwright (alternative)

**Environnement** : Staging (réplique de production)

**Exécution** : Avant chaque déploiement + quotidien (nightly build)

#### 3.2.4 Tests de Sécurité

- **OWASP Top 10** : Injection SQL, XSS, CSRF
- **Scan de vulnérabilités** : Dependabot, Snyk
- **Tests d'authentification** : Tentatives de bypass, brute force
- **Tests d'autorisation** : RBAC (accès non autorisés)

**Outils** :
- OWASP ZAP (scan automatisé)
- Burp Suite (tests manuels si nécessaire)

#### 3.2.5 Tests de Performance

- **Tests de charge** : 100 utilisateurs simultanés
- **Tests de stress** : Montée progressive jusqu'à 500 users
- **Tests de latence** : API < 200ms, Page load < 2s

**Outils** :
- JMeter, k6, Locust

**Exécution** : Sprint 20 (phase pré-production)

### 3.3 Environnements de Test

| Environnement | Usage | Base de données | URL |
|:--------------|:------|:----------------|:----|
| **Local** | Développement quotidien | PostgreSQL Docker | localhost:3000 |
| **CI/CD** | Tests automatisés | Testcontainers | - |
| **Staging** | Recette, Tests E2E | PostgreSQL Cloud | staging.taskforce.local |
| **Production** | Monitoring post-déploiement | PostgreSQL Prod | taskforce.local |

---

## 4. Cas de test

### 4.1 Epic 1 : Authentification

#### Test Case TC-AUTH-001 : Inscription Utilisateur

| ID | TC-AUTH-001 |
|:---|:------------|
| **Titre** | Inscription d'un nouvel utilisateur |
| **Priorité** | Critique |
| **Pré-requis** | Aucun utilisateur avec cet email |
| **Étapes** | 1. Accéder à `/authentication`<br>2. Cliquer sur "S'inscrire"<br>3. Saisir email valide<br>4. Saisir mot de passe (min 8 caractères)<br>5. Confirmer mot de passe<br>6. Cliquer sur "Créer un compte" |
| **Résultat attendu** | - Compte créé avec succès<br>- Redirection vers `/dashboard`<br>- Token JWT reçu et stocké |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-AUTH-002 : Connexion Utilisateur

| ID | TC-AUTH-002 |
|:---|:------------|
| **Titre** | Connexion avec credentials valides |
| **Priorité** | Critique |
| **Pré-requis** | Utilisateur existant (email: test@taskforce.com, pwd: Password123!) |
| **Étapes** | 1. Accéder à `/authentication`<br>2. Saisir email<br>3. Saisir mot de passe<br>4. Cliquer "Se connecter" |
| **Résultat attendu** | - Connexion réussie<br>- Redirection vers `/dashboard`<br>- Token JWT valide généré |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-AUTH-003 : Connexion Échouée (Credentials Invalides)

| ID | TC-AUTH-003 |
|:---|:------------|
| **Titre** | Tentative de connexion avec mot de passe incorrect |
| **Priorité** | Haute |
| **Pré-requis** | Utilisateur existant |
| **Étapes** | 1. Accéder à `/authentication`<br>2. Saisir email valide<br>3. Saisir mot de passe incorrect<br>4. Cliquer "Se connecter" |
| **Résultat attendu** | - Erreur affichée : "Email ou mot de passe incorrect"<br>- Pas de redirection<br>- Pas de token généré |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

### 4.2 Epic 2 : Gestion des Tâches

#### Test Case TC-TASK-001 : Création de Tâche

| ID | TC-TASK-001 |
|:---|:------------|
| **Titre** | Création d'une nouvelle tâche par un manager |
| **Priorité** | Critique |
| **Pré-requis** | - Utilisateur connecté (rôle MANAGER)<br>- Projet existant |
| **Étapes** | 1. Accéder au projet<br>2. Cliquer "Nouvelle tâche"<br>3. Saisir titre<br>4. Saisir description<br>5. Sélectionner compétences requises<br>6. Définir priorité<br>7. Cliquer "Créer" |
| **Résultat attendu** | - Tâche créée avec succès<br>- Apparaît dans la vue Kanban (colonne TODO)<br>- Suggestions d'assignation affichées |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-TASK-002 : Assignation Manuelle

| ID | TC-TASK-002 |
|:---|:------------|
| **Titre** | Assignation d'une tâche à un collaborateur |
| **Priorité** | Critique |
| **Pré-requis** | - Tâche non assignée existante<br>- Collaborateur membre de l'équipe |
| **Étapes** | 1. Ouvrir la tâche<br>2. Cliquer "Assigner"<br>3. Sélectionner collaborateur<br>4. Confirmer |
| **Résultat attendu** | - Tâche assignée au collaborateur<br>- Notification envoyée au collaborateur<br>- Avatar du collaborateur affiché sur la carte |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-TASK-003 : Matching Compétences (Top 3)

| ID | TC-TASK-003 |
|:---|:------------|
| **Titre** | Suggestions d'assignation basées sur les compétences |
| **Priorité** | Haute |
| **Pré-requis** | - Tâche avec compétences requises (ex: Java niveau 3, SQL niveau 4)<br>- Équipe avec plusieurs membres ayant des compétences variées |
| **Étapes** | 1. Créer une tâche avec compétences requises<br>2. Observer les suggestions |
| **Résultat attendu** | - Top 3 collaborateurs affichés<br>- Score de matching affiché (ex: "95% match")<br>- Explication du score (compétences possédées) |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-TASK-004 : Mise à Jour Statut

| ID | TC-TASK-004 |
|:---|:------------|
| **Titre** | Changement de statut d'une tâche (Collaborateur) |
| **Priorité** | Critique |
| **Pré-requis** | - Tâche assignée au collaborateur connecté |
| **Étapes** | 1. Ouvrir ma tâche<br>2. Cliquer "Passer en cours"<br>3. Cliquer "Terminer" |
| **Résultat attendu** | - Statut mis à jour (TODO → IN_PROGRESS → DONE)<br>- Date de complétion enregistrée<br>- Notification au manager |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

### 4.3 Epic 3 : Collaboration

#### Test Case TC-COLLAB-001 : Ajout de Commentaire

| ID | TC-COLLAB-001 |
|:---|:------------|
| **Titre** | Ajout d'un commentaire sur une tâche |
| **Priorité** | Haute |
| **Pré-requis** | - Utilisateur assigné ou créateur de la tâche |
| **Étapes** | 1. Ouvrir la tâche<br>2. Scroller vers section commentaires<br>3. Saisir un commentaire<br>4. Cliquer "Envoyer" |
| **Résultat attendu** | - Commentaire ajouté avec timestamp<br>- Avatar et nom de l'auteur affichés<br>- Notification aux participants de la tâche |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-COLLAB-002 : Upload de Fichier

| ID | TC-COLLAB-002 |
|:---|:------------|
| **Titre** | Joindre un fichier à une tâche |
| **Priorité** | Haute |
| **Pré-requis** | - Utilisateur assigné ou créateur<br>- Fichier < 10 MB |
| **Étapes** | 1. Ouvrir la tâche<br>2. Cliquer "Joindre un fichier"<br>3. Sélectionner fichier (PDF, image, etc.)<br>4. Confirmer upload |
| **Résultat attendu** | - Fichier uploadé avec succès<br>- Apparaît dans liste des pièces jointes<br>- Possibilité de télécharger |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-COLLAB-003 : Upload Fichier Trop Lourd (Erreur)

| ID | TC-COLLAB-003 |
|:---|:------------|
| **Titre** | Tentative d'upload fichier > 10 MB |
| **Priorité** | Moyenne |
| **Pré-requis** | - Fichier > 10 MB |
| **Étapes** | 1. Ouvrir la tâche<br>2. Tenter d'uploader fichier |
| **Résultat attendu** | - Erreur affichée : "Fichier trop volumineux (max 10 MB)"<br>- Upload annulé |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

### 4.4 Epic 4 : Notifications

#### Test Case TC-NOTIF-001 : Notification Assignation

| ID | TC-NOTIF-001 |
|:---|:------------|
| **Titre** | Réception notification lors d'assignation |
| **Priorité** | Haute |
| **Pré-requis** | - Collaborateur connecté<br>- WebSocket actif |
| **Étapes** | 1. Manager assigne une tâche au collaborateur<br>2. Observer le badge de notifications |
| **Résultat attendu** | - Badge notification s'affiche (ex: 🔴 1)<br>- Notification apparaît dans le panneau<br>- Son de notification (si activé) |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-NOTIF-002 : Marquer comme Lu

| ID | TC-NOTIF-002 |
|:---|:------------|
| **Titre** | Marquer une notification comme lue |
| **Priorité** | Moyenne |
| **Pré-requis** | - Notification non lue présente |
| **Étapes** | 1. Ouvrir panneau notifications<br>2. Cliquer sur la notification |
| **Résultat attendu** | - Notification marquée comme lue<br>- Badge de count décrémenté<br>- Style visuel change (grisé) |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

### 4.5 Tests de Sécurité

#### Test Case TC-SEC-001 : Accès Non Autorisé API

| ID | TC-SEC-001 |
|:---|:------------|
| **Titre** | Tentative d'accès à une API protégée sans token |
| **Priorité** | Critique |
| **Pré-requis** | - Aucun token JWT |
| **Étapes** | 1. Effectuer requête GET /api/tasks sans header Authorization |
| **Résultat attendu** | - HTTP 401 Unauthorized<br>- Pas de données retournées |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-SEC-002 : Injection SQL (Protection)

| ID | TC-SEC-002 |
|:---|:------------|
| **Titre** | Test d'injection SQL dans champ de recherche |
| **Priorité** | Critique |
| **Pré-requis** | - Endpoint de recherche de tâches |
| **Étapes** | 1. Envoyer requête GET /api/tasks?search='; DROP TABLE users;-- |
| **Résultat attendu** | - Pas d'exécution SQL malveillante<br>- Résultat vide ou erreur 400<br>- Table users intacte |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

#### Test Case TC-SEC-003 : RBAC (Rôles)

| ID | TC-SEC-003 |
|:---|:------------|
| **Titre** | Un collaborateur ne peut pas accéder aux fonctions admin |
| **Priorité** | Critique |
| **Pré-requis** | - Utilisateur connecté avec rôle COLLABORATOR |
| **Étapes** | 1. Tenter GET /api/admin/users |
| **Résultat attendu** | - HTTP 403 Forbidden<br>- Message : "Accès refusé" |
| **Résultat réel** | _(À remplir lors du test)_ |
| **Statut** | ✅ Pass / ❌ Fail |

---

## 5. Critères d'acceptation

### 5.1 Critères de Succès par Epic

#### Epic 1 : Authentification
- ✅ Inscription/Connexion fonctionnelles
- ✅ Tokens JWT valides et sécurisés
- ✅ Session maintenue après rafraîchissement page

#### Epic 2 : Gestion Tâches
- ✅ CRUD tâches complet
- ✅ Matching compétences affiche top 3 avec scores > 50%
- ✅ Statuts mis à jour en temps réel

#### Epic 3 : Collaboration
- ✅ Commentaires sauvegardés et affichés correctement
- ✅ Fichiers uploadés/téléchargés sans erreur
- ✅ Notifications temps réel fonctionnelles

### 5.2 Critères de Non-Régression
- Tous les tests automatisés passent (CI/CD green)
- Aucune régression de performance (< 200ms API)
- Pas de nouvelles vulnérabilités détectées (Snyk, Dependabot)

---

## 6. Plan de recette

### 6.1 Phase de Recette Interne (Sprint 21)

**Objectif** : Validation fonctionnelle complète par le développeur

**Durée** : 1 semaine (28 Avril - 04 Mai 2026)

**Parcours de Recette** :

| Jour | Parcours Testé | Responsable |
|:-----|:---------------|:------------|
| Lundi | Auth + Profils | Pierre |
| Mardi | Projets + Équipes | Pierre |
| Mercredi | Tâches + Assignation | Pierre |
| Jeudi | Commentaires + Fichiers | Pierre |
| Vendredi | Notifications + Dashboard | Pierre |

### 6.2 Phase de Recette Externe (Sprint 22 - Si possible)

**Objectif** : Validation par bêta-testeurs externes

**Durée** : 1 semaine (05-11 Mai 2026)

**Profils de Testeurs** :
- 1-2 enseignants MNS (rôle Manager)
- 2-3 étudiants (rôle Collaborateur)

**Méthode** :
1. Briefing : Présentation de l'app + scénarios à tester
2. Tests libres : Exploration guidée (30 min)
3. Tests scénarisés : Parcours prédéfinis (1h)
4. Feedback : Questionnaire + entretien (15 min)

**Questionnaire de Recette** :
- L'interface est-elle intuitive ? (1-5)
- Les fonctionnalités répondent-elles au besoin ? (1-5)
- Bugs rencontrés ? (description)
- Suggestions d'amélioration ?

### 6.3 Gestion des Anomalies

**Classification** :
- **Bloquant** : Fonctionnalité critique inutilisable → Fix immédiat
- **Majeur** : Fonctionnalité dégradée → Fix avant production
- **Mineur** : Bug cosmétique → Backlog v1.1

**Workflow** :
1. Création d'issue GitHub (label `type:bug`, priorité)
2. Assignation et estimation
3. Fix + tests
4. Re-test par le rapporteur

---

## 7. Annexes

### 7.1 Scripts de Tests E2E (Exemple Cypress)

```javascript
// cypress/e2e/auth.cy.ts
describe('Authentication Flow', () => {
  it('should register a new user', () => {
    cy.visit('/authentication');
    cy.get('[data-testid="register-email"]').type('newuser@test.com');
    cy.get('[data-testid="register-password"]').type('Password123!');
    cy.get('[data-testid="register-confirm"]').type('Password123!');
    cy.get('[data-testid="register-submit"]').click();
    
    cy.url().should('include', '/dashboard');
    cy.get('[data-testid="user-menu"]').should('contain', 'newuser@test.com');
  });
  
  it('should login with existing credentials', () => {
    cy.visit('/authentication');
    cy.get('[data-testid="login-email"]').type('test@taskforce.com');
    cy.get('[data-testid="login-password"]').type('Password123!');
    cy.get('[data-testid="login-submit"]').click();
    
    cy.url().should('include', '/dashboard');
  });
});

// cypress/e2e/tasks.cy.ts
describe('Task Management', () => {
  beforeEach(() => {
    cy.login('manager@test.com', 'Password123!'); // Custom command
  });
  
  it('should create a task with suggestions', () => {
    cy.visit('/projects/1');
    cy.get('[data-testid="new-task-btn"]').click();
    cy.get('[data-testid="task-title"]').type('Implement authentication API');
    cy.get('[data-testid="task-skill-select"]').select('Java');
    cy.get('[data-testid="task-create"]').click();
    
    cy.get('[data-testid="suggestions"]').should('have.length', 3);
    cy.get('[data-testid="suggestion-0"]').should('contain', 'match');
  });
});
```

### 7.2 Templates de Reporting

**Template de Bug Report** :
```markdown
## 🐛 Bug Report

**Titre** : [Titre court et descriptif]

**Priorité** : 🔴 Bloquant / 🟠 Majeur / 🟡 Mineur

**Description** :
[Description claire du bug]

**Étapes de Reproduction** :
1. 
2. 
3. 

**Comportement Attendu** :


**Comportement Observé** :


**Environnement** :
- OS : 
- Navigateur : 
- Version : 

**Captures d'écran** :
[Si applicable]
```

---

**Dernière mise à jour** : Décembre 2025  
**Responsable Tests** : Pierre MICHEL
