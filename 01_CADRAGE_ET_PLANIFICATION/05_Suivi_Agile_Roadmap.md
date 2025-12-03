# Suivi Agile et Roadmap

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Méthodologie Agile](#1-méthodologie-agile)
- [2. Organisation des Sprints](#2-organisation-des-sprints)
- [3. Backlog Produit](#3-backlog-produit)
- [4. Roadmap Produit](#4-roadmap-produit)
- [5. Définition of Done (DoD)](#5-définition-of-done-dod)
- [6. Rituels Agile](#6-rituels-agile)
- [7. Outils de Suivi](#7-outils-de-suivi)

---

## 1. Méthodologie Agile

### 1.1 Framework Choisi
**Scrum adapté en mode solo** avec gestion Kanban sur GitHub Projects.

### 1.2 Principes Appliqués
- **Itérations courtes** : Sprints d'une semaine pour un feedback rapide.
- **Livraison incrémentale** : Fonctionnalités déployables à chaque sprint.
- **Amélioration continue** : Rétrospective hebdomadaire pour ajuster le processus.
- **Priorisation** : Focus sur les fonctionnalités à haute valeur pour le MVP.

### 1.3 Rôles (Mode Solo)
- **Product Owner + Scrum Master + Développeur** : Pierre MICHEL
- **Stakeholder / AMOA** : Cédric Brasseur (validation des livrables)

---

## 2. Organisation des Sprints

### 2.1 Durée des Sprints
**1 semaine** (Lundi → Dimanche)

### 2.2 Capacité par Sprint
- **Développement** : ~30-35 heures effectives
- **Vélocité estimée** : 20-25 Story Points (à affiner après Sprint 1)

### 2.3 Cycle de Sprint
1. **Lundi matin** : Sprint Planning (définition des objectifs et sélection des User Stories)
2. **Mardi → Samedi** : Développement quotidien + Daily Standup personnel (bilan journalier)
3. **Dimanche** : Sprint Review (démonstration des fonctionnalités) + Sprint Retrospective

---

## 3. Backlog Produit

### 3.1 Priorisation (MoSCoW)
- **Must Have** : Fonctionnalités essentielles pour le MVP
- **Should Have** : Importantes mais reportables à la v2
- **Could Have** : Nice-to-have pour versions futures
- **Won't Have** : Hors scope pour ce projet

### 3.2 Backlog MVP (v1.0 - Juin 2026)

#### Epic 1 : Authentification & Gestion des Utilisateurs
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-001 : En tant qu'utilisateur, je peux créer un compte avec email/mot de passe | Must | 5 | Sprint 1 |
| US-002 : En tant qu'utilisateur, je peux me connecter et me déconnecter | Must | 3 | Sprint 1 |
| US-003 : En tant qu'utilisateur, je peux réinitialiser mon mot de passe | Should | 5 | Sprint 8 |
| US-004 : En tant qu'utilisateur, je peux compléter mon profil (nom, photo, bio) | Must | 3 | Sprint 2 |
| US-005 : En tant qu'utilisateur, je peux déclarer mes compétences avec niveau (tags) | Must | 8 | Sprint 2 |
| US-006 : En tant qu'utilisateur, je peux gérer ma disponibilité (congés, heures/semaine) | Should | 5 | Sprint 9 |

#### Epic 2 : Gestion des Équipes
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-007 : En tant que manager, je peux créer une équipe | Must | 5 | Sprint 3 |
| US-008 : En tant que manager, je peux ajouter/retirer des membres | Must | 3 | Sprint 3 |
| US-009 : En tant que manager, je peux voir les compétences agrégées de l'équipe | Should | 5 | Sprint 10 |

#### Epic 3 : Gestion des Projets
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-010 : En tant que manager, je peux créer un projet (nom, description, dates, équipe) | Must | 5 | Sprint 4 |
| US-011 : En tant que manager, je peux modifier/archiver un projet | Must | 3 | Sprint 4 |
| US-012 : En tant que collaborateur, je peux voir les projets auxquels je suis assigné | Must | 2 | Sprint 4 |

#### Epic 4 : Gestion des Tâches
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-013 : En tant que manager, je peux créer une tâche (titre, description, compétences requises, estimation) | Must | 8 | Sprint 5 |
| US-014 : En tant que manager, je peux définir la priorité et la deadline d'une tâche | Must | 3 | Sprint 5 |
| US-015 : En tant que manager, je peux assigner manuellement une tâche à un collaborateur | Must | 5 | Sprint 6 |
| US-016 : En tant que manager, je vois les suggestions d'assignation basées sur le matching compétences | Must | 13 | Sprint 7 |
| US-017 : En tant que collaborateur, je peux mettre à jour le statut d'une tâche (À faire, En cours, Terminé) | Must | 5 | Sprint 6 |
| US-018 : En tant qu'utilisateur, je peux ajouter des commentaires à une tâche | Must | 8 | Sprint 11 |
| US-019 : En tant qu'utilisateur, je peux attacher des fichiers à une tâche | Must | 8 | Sprint 12 |

#### Epic 5 : Tableau de Bord & Visualisation
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-020 : En tant que collaborateur, je vois mes tâches en cours et à venir sur mon dashboard | Must | 8 | Sprint 8 |
| US-021 : En tant que manager, je vois une vue Kanban des tâches du projet | Must | 13 | Sprint 9 |
| US-022 : En tant que manager, je vois la charge de travail de mon équipe (heatmap) | Should | 8 | Sprint 13 |

#### Epic 6 : Notifications
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-023 : En tant qu'utilisateur, je reçois des notifications in-app (nouvelle tâche, commentaire, deadline) | Must | 13 | Sprint 14 |
| US-024 : En tant qu'utilisateur, je peux marquer les notifications comme lues | Should | 3 | Sprint 15 |

#### Epic 7 : Administration
| User Story | Priorité | Story Points | Sprint |
|:-----------|:---------|:-------------|:-------|
| US-025 : En tant qu'admin, je peux gérer les utilisateurs (activation, désactivation) | Should | 5 | Sprint 16 |
| US-026 : En tant qu'admin, je peux voir les logs d'activité | Could | 8 | v2 |

### 3.3 Backlog v2.0 (Post-MVP)
- **IA d'assignation automatique** (algorithme ML avancé)
- **Chat in-app** entre collaborateurs du même projet
- **Exports/Rapports** (PDF, Excel)
- **Vues additionnelles** (Gantt, Timeline, Calendrier)
- **Intégrations** (Slack, Microsoft Teams, Jira)
- **Notifications Email**
- **Mode Hors-ligne**

---

## 4. Roadmap Produit

### 4.1 Timeline Globale

```
Décembre 2025 - Janvier 2026 : Phase Conception & Setup
│
├── Sprint 0 (02-08 Déc) : Setup environnement + MCD/MLD
├── Sprint 1 (09-15 Déc) : Authentification (Login/Register)
├── Sprint 2 (16-22 Déc) : Profils & Compétences
├── Sprint 3 (23-29 Déc) : Gestion Équipes
│
Janvier 2026 : Module Projets & Tâches
│
├── Sprint 4 (30 Déc - 05 Jan) : CRUD Projets
├── Sprint 5 (06-12 Jan) : CRUD Tâches (base)
├── Sprint 6 (13-19 Jan) : Assignation manuelle + Statuts
├── Sprint 7 (20-26 Jan) : Matching compétences (algorithme simple)
│
Février 2026 : Dashboards & UX
│
├── Sprint 8 (27 Jan - 02 Fév) : Dashboard Collaborateur
├── Sprint 9 (03-09 Fév) : Vue Kanban Projet
├── Sprint 10 (10-16 Fév) : Agrégation compétences équipe
├── Sprint 11 (17-23 Fév) : Système de commentaires
│
Mars 2026 : Fichiers & Notifications
│
├── Sprint 12 (24 Fév - 02 Mar) : Upload/Download fichiers
├── Sprint 13 (03-09 Mar) : Heatmap charge de travail
├── Sprint 14 (10-16 Mar) : Notifications in-app
├── Sprint 15 (17-23 Mar) : Gestion notifications (lues/non lues)
│
Avril 2026 : Finalisation & Tests
│
├── Sprint 16 (24-30 Mar) : Administration utilisateurs
├── Sprint 17 (31 Mar - 06 Avr) : Corrections bugs & optimisations
├── Sprint 18 (07-13 Avr) : Tests E2E complets
├── Sprint 19 (14-20 Avr) : Documentation utilisateur finale
│
Mai 2026 : Recette & Préparation Déploiement
│
├── Sprint 20 (21-27 Avr) : Tests de charge & sécurité
├── Sprint 21 (28 Avr - 04 Mai) : Recette utilisateur
├── Sprint 22 (05-11 Mai) : Corrections recette
├── Sprint 23 (12-18 Mai) : Setup environnement production
│
Juin 2026 : Déploiement MVP
│
├── Sprint 24 (19-25 Mai) : Déploiement production
└── Sprint 25 (26 Mai - 01 Juin) : Suivi post-déploiement & hotfixes
```

### 4.2 Jalons (Milestones)

| Milestone | Date Cible | Livrables |
|:----------|:-----------|:----------|
| **M1 : Auth & Profils** | 22 Décembre 2025 | Login/Register, Gestion profils & compétences |
| **M2 : Projets & Tâches** | 26 Janvier 2026 | CRUD Projets/Tâches, Assignation avec matching |
| **M3 : Dashboards** | 23 Février 2026 | Dashboard perso, Vue Kanban, Commentaires |
| **M4 : Collaboration** | 23 Mars 2026 | Fichiers, Notifications, Heatmap |
| **M5 : MVP Complet** | 20 Avril 2026 | Toutes fonctionnalités MVP + Tests E2E |
| **M6 : Déploiement Prod** | 01 Juin 2026 | Application en production stable |

---

## 5. Définition of Done (DoD)

Une User Story est considérée comme **Done** si :

### 5.1 Code
- ✅ Code implémenté et conforme aux spécifications
- ✅ Code respecte les conventions (linter sans erreur)
- ✅ Pas de dette technique introduite (ou documentée)
- ✅ Commit conventionnel avec gitmoji (`✨ feat(auth): add login endpoint`)

### 5.2 Tests
- ✅ Tests unitaires écrits (couverture > 80% sur la fonctionnalité)
- ✅ Tests d'intégration (si applicable)
- ✅ Tous les tests passent (CI/CD green)

### 5.3 Documentation
- ✅ Code commenté si logique complexe
- ✅ API documentée (Swagger si backend)
- ✅ README mis à jour si nécessaire

### 5.4 Review & Qualité
- ✅ Code self-review effectué
- ✅ Pas d'erreurs console/logs
- ✅ Responsive & Accessible (WCAG AA)

### 5.5 Démo
- ✅ Fonctionnalité déployée en environnement de dev
- ✅ Démonstrable lors de la Sprint Review

---

## 6. Rituels Agile

### 6.1 Sprint Planning (Lundi matin - 1h)
- Sélection des User Stories du backlog
- Estimation en Story Points
- Définition de l'objectif du sprint (Sprint Goal)

### 6.2 Daily Standup Personnel (Quotidien - 10 min)
**Format écrit dans NOTES.md :**
- ✅ Qu'ai-je fait hier ?
- 🎯 Que vais-je faire aujourd'hui ?
- 🚧 Y a-t-il des blocages ?

### 6.3 Sprint Review (Dimanche - 30 min)
- Démonstration des fonctionnalités complétées
- Validation par rapport au Sprint Goal
- Mise à jour de la roadmap si nécessaire

### 6.4 Sprint Retrospective (Dimanche - 30 min)
**Format :**
- ➕ Ce qui a bien fonctionné
- ➖ Ce qui peut être amélioré
- 🔄 Actions d'amélioration pour le prochain sprint

---

## 7. Outils de Suivi

### 7.1 GitHub Projects (Kanban Board)
**Colonnes :**
- 📋 **Backlog** : User Stories priorisées
- 🎯 **Sprint Actif** : Stories du sprint en cours
- 🏗️ **In Progress** : En cours de développement
- 👀 **In Review** : Code review / Tests
- ✅ **Done** : Terminé (DoD respectée)

### 7.2 Labels GitHub
- `priority:critical` / `priority:high` / `priority:medium` / `priority:low`
- `epic:auth` / `epic:tasks` / `epic:dashboard` (regroupement)
- `type:feature` / `type:bug` / `type:refactor`
- `status:blocked` / `status:needs-info`

### 7.3 Métriques de Suivi
- **Vélocité** : Story Points complétés par sprint (tracking pour ajuster les estimations)
- **Burndown Chart** : Progression du sprint (manuel ou via GitHub Projects)
- **Nombre de bugs** : Tracking pour améliorer la qualité

### 7.4 Documentation de Suivi
- **NOTES.md** : Journal de bord quotidien (Daily Standup écrit)
- **CHANGELOG.md** : Historique des versions
- **GitHub Releases** : Versions taguées à chaque milestone

---

## 8. Adaptation & Flexibilité

### 8.1 Gestion des Imprévus
- Si blocage technique > 4h : Pivot vers une autre User Story
- Si story trop complexe : Découpage en sous-tasks plus petites
- Réestimation en cours de sprint autorisée (avec justification)

### 8.2 Feedback Continu
- **Sprint 5** : Point AMOA (Cédric Brasseur) sur l'avancement
- **Sprint 10** : Démo intermédiaire pour validation fonctionnelle
- **Sprint 15** : Pré-recette interne avant phase de tests finale

---

**Dernière mise à jour** : Décembre 2025  
**Responsable** : Pierre MICHEL
