---
id: manuel-utilisateur
title: Manuel Utilisateur — TaskForce V1
doc_type: utilisateur
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [utilisateur, manuel, guide, onboarding, rncp, soutenance]
---

# 📖 Manuel Utilisateur — TaskForce V1

> Manuel destiné aux trois profils d'utilisateurs : **Membre**, **Admin** et **Owner**.
> Toutes les fonctionnalités décrites sont implémentées et fonctionnelles dans la V1.
> Sources : 48 routes `frontend/app/**/page.tsx` + contrôleurs backend + UC-01 à UC-12.

---

## Table des matières

1. [Premiers pas — Inscription & connexion](#1-premiers-pas--inscription--connexion)
2. [Rôles & permissions](#2-rôles--permissions)
3. [Espaces de travail (workspaces)](#3-espaces-de-travail-workspaces)
4. [Membres & invitations](#4-membres--invitations)
5. [Projets](#5-projets)
6. [Tâches (Issues)](#6-tâches-issues)
7. [Smart Assign — Assignation intelligente par IA](#7-smart-assign--assignation-intelligente-par-ia)
8. [Cycles (sprints)](#8-cycles-sprints)
9. [Pages wiki](#9-pages-wiki)
10. [Chat & discussions](#10-chat--discussions)
11. [Plans & facturation](#11-plans--facturation)
12. [Profil, données & RGPD](#12-profil-données--rgpd)

---

## 1. Premiers pas — Inscription & connexion

### 1.1 Inscription (UC-01)

L'inscription se déroule en **3 étapes** :

1. **Informations de compte** : adresse email + mot de passe (8 caractères minimum)
2. **Choix du plan** : FREE (gratuit) · PRO · ENTERPRISE
3. **Vérification OTP** : un code à 6 chiffres est envoyé par email
   - Durée de validité : **15 minutes**
   - Tentatives maximum : **3** (au-delà, un nouveau code est renvoyé)
   - Le compte n'est activé qu'une fois le code validé

**Route frontend** : `/auth/register` → `/auth/verify-email`

### 1.2 Connexion (UC-02)

- **URL** : `/auth/login`
- **Identifiants** : email + mot de passe
- **Session** : le token de session est géré automatiquement ; la reconnexion est transparente grâce au refresh token (cookie HttpOnly sécurisé)

### 1.3 Mot de passe oublié

La réinitialisation suit le même mécanisme OTP que l'inscription :
1. Aller sur `/auth/forgot-password`
2. Entrer l'adresse email du compte
3. Saisir le code reçu par email (15 min)
4. Choisir un nouveau mot de passe

---

## 2. Rôles & permissions

TaskForce utilise un système RBAC (contrôle d'accès basé sur les rôles) à l'échelle du workspace.

| Rôle | Signification | Capacités principales |
|---|---|---|
| **OWNER** | Propriétaire du workspace | Toutes les actions · Suppression du workspace · Transfert de propriété · Accès audit |
| **ADMIN** | Administrateur | Gestion des membres · Création de projets · Gestion des intégrations · Tout ce que MEMBER peut faire |
| **MEMBER** | Membre standard | Créer/éditer des issues · Commenter · Travailler sur les projets auxquels il est assigné |

**Règle importante** : un workspace a toujours exactement un OWNER. Les rôles ADMIN et MEMBER sont cumulables en nombre illimité.

**Permissions détaillées** :

| Action | MEMBER | ADMIN | OWNER |
|---|:---:|:---:|:---:|
| Créer une issue | ✅ | ✅ | ✅ |
| Modifier une issue (la sienne) | ✅ | ✅ | ✅ |
| Modifier une issue (n'importe laquelle) | ❌ | ✅ | ✅ |
| Inviter des membres | ❌ | ✅ | ✅ |
| Gérer les rôles | ❌ | ✅ | ✅ |
| Créer un projet | ❌ | ✅ | ✅ |
| Supprimer un projet | ❌ | ✅ | ✅ |
| Activer une intégration | ❌ | ✅ | ✅ |
| Voir les logs d'audit | ❌ | ❌ | ✅ |
| Supprimer le workspace | ❌ | ❌ | ✅ |

---

## 3. Espaces de travail (workspaces)

Un **workspace** est l'unité d'isolation principale : chaque workspace a ses propres membres, projets, données et plan de facturation.

### 3.1 Créer un workspace

1. Accéder à `/workspaces/create`
2. Renseigner :
   - **Nom** : affiché dans la navigation
   - **Slug** : identifiant URL unique (ex. `mon-equipe`) — ne peut plus être modifié après création
   - **Description** (optionnel)

### 3.2 Navigation entre workspaces

Depuis n'importe quelle page, le menu latéral gauche affiche le workspace actif. Un clic sur le logo du workspace ouvre le sélecteur permettant de passer d'un workspace à l'autre (si vous êtes membre de plusieurs).

### 3.3 Paramètres du workspace

Accessibles via `/workspaces/{slug}/settings` (réservé ADMIN/OWNER) :

- Modifier le nom et la description
- Téléverser une icône (avatar)
- Gérer les membres
- Configurer les intégrations (GitHub, Slack, webhooks)
- Paramètres de facturation

### 3.4 Fermer un workspace

Seul l'OWNER peut supprimer un workspace. Cette action est irréversible et supprime en cascade tous les projets, issues, pages et fichiers du workspace.

---

## 4. Membres & invitations

### 4.1 Inviter un membre (UC-04)

Depuis `/workspaces/{slug}/settings/members` (ADMIN/OWNER) :

1. Cliquer sur **Inviter** (`POST /api/workspaces/{slug}/invitations`)
2. Saisir l'adresse email + choisir le rôle (MEMBER ou ADMIN)
3. Un email d'invitation est envoyé — lien valable **72 heures**
4. La personne invitée clique sur le lien → crée un compte (ou se connecte) → rejoint le workspace

**Statuts d'invitation** : `PENDING` → `ACCEPTED` (ou `EXPIRED` au bout de 72h)

### 4.2 Modifier le rôle d'un membre

Dans la liste des membres, cliquer sur le rôle affiché pour le modifier (liste déroulante). Action réservée ADMIN/OWNER.

### 4.3 Retirer un membre

Bouton **Retirer** en regard du membre dans la liste. L'utilisateur retiré perd immédiatement l'accès au workspace. Ses contributions (issues, commentaires, pages) sont conservées.

> **Note Smart Assign** : le profil de compétences d'un membre (voir §7) peut être complété dans `/workspaces/{slug}/settings/members/{memberId}/skills` pour améliorer les suggestions d'assignation.

---

## 5. Projets

### 5.1 Créer un projet

Depuis la barre de navigation gauche → **+ Nouveau projet** (ou `/workspaces/{slug}/projects/create`) :

- **Nom** et **identifiant** (court, ex. `WEB`, `API`)
- **Description** (optionnel)
- **Réseau** : Internal (par défaut) ou Secret

### 5.2 Membres d'un projet

Chaque projet a ses propres membres (sous-ensemble des membres du workspace) avec un rôle au niveau projet (`MEMBER` ou `LEAD`). Les ADMIN/OWNER du workspace ont accès à tous les projets.

### 5.3 Paramètres d'un projet

Accessibles via `/workspaces/{slug}/projects/{projectId}/settings` :

- **Statuts d'issue** : chaque projet peut personnaliser ses propres statuts (catégories : `BACKLOG`, `UNSTARTED`, `STARTED`, `COMPLETED`, `CANCELLED`). Par défaut : Backlog, Todo, In Progress, In Review, Done.
- **Labels** : créer/gérer des labels colorés pour classer les issues
- **Modules** : regrouper les issues par thème

---

## 6. Tâches (Issues)

Les issues sont le cœur de TaskForce. Chaque issue appartient à un projet.

### 6.1 Créer une issue

Depuis la vue liste ou kanban d'un projet, cliquer sur **+ Nouvelle issue** :

| Champ | Description | Valeurs |
|---|---|---|
| **Titre** | Description courte (obligatoire) | Texte libre |
| **Description** | Détail riche (Markdown/ProseMirror) | Optionnel |
| **Type** | Catégorie de travail | `Bug` · `Feature` · `Task` · `Improvement` · `Story` · `Epic` · `Question` |
| **Priorité** | Ordre de traitement | `Urgent` · `High` · `Medium` · `Low` · `None` |
| **Statut** | Avancement | Selon les statuts configurés dans le projet |
| **Assigné** | Responsable | Membre du projet |
| **Labels** | Étiquettes | Labels du projet |
| **Cycle** | Sprint associé | Cycle actif ou futur |
| **Module** | Regroupement thématique | Module du projet |
| **Date d'échéance** | Due date | Date |

### 6.2 Vues disponibles

| Vue | Description |
|---|---|
| **Kanban** | Colonnes par statut, déplacer les issues par drag-and-drop |
| **Liste** | Tableau avec tri, filtres, groupements |
| **Backlog** | Vue plate de tout le backlog (non planifié) |

Les vues sont filtrables par priorité, assigné, label, cycle, module, et dates.

### 6.3 Détail d'une issue

La fiche d'une issue contient :
- Titre et description (éditables inline)
- Panneau latéral : métadonnées (priorité, statut, assigné, dates…)
- **Commentaires** : avec formatage Markdown
- **Activité** : historique de toutes les modifications
- **Sous-issues** : créer une hiérarchie parent/enfant
- **Relations** : `blocks` / `blocked-by` / `duplicate-of`
- **Pièces jointes** : upload de fichiers via MinIO

### 6.4 Tâches récurrentes et worklogs

- Une issue peut avoir plusieurs **worklogs** : saisir le temps passé (en minutes + description) via le bouton Chrono sur la fiche de l'issue.
- Les worklogs alimentent les analytiques de capacité dans le Smart Assign.

---

## 7. Smart Assign — Assignation intelligente par IA

Le **Smart Assign** (UC-07) est la fonctionnalité différenciante de TaskForce. Il suggère automatiquement le meilleur assigné pour une issue en analysant :

1. **Compétences** : les compétences requises pour la tâche vs. les compétences déclarées des membres
2. **Charge de travail** : nombre d'issues en cours × priorité vs. la capacité déclarée (heures/semaine)
3. **Disponibilité** : présence en cycle actif, congés renseignés

### 7.1 Activer le Smart Assign

Bouton **Smart Assign** sur la fiche d'une issue. L'IA (Groq) génère :
- Une liste de membres candidats classés par score
- Une **explication** en langage naturel pour chaque suggestion
- Le score de correspondance (compétences, charge, disponibilité)

### 7.2 Configurer son profil de compétences

Pour apparaître dans les suggestions (et y avoir un bon score), chaque membre devrait remplir son profil :

**Accès** : `/workspaces/{slug}/settings/members/{memberId}/skills` (ou depuis les Paramètres du workspace)

| Champ | Contenu |
|---|---|
| **Compétences** | Liste de compétences avec niveau (Débutant/Intermédiaire/Expert) |
| **Séniorité** | Junior · Mid · Senior · Lead · Staff |
| **Capacité** | Heures disponibles par semaine |
| **Objectifs de progression** | Compétences à développer (optionnel) |

> Le profil de compétences est facultatif. Si non renseigné, le membre n'apparaît pas dans les suggestions Smart Assign.

### 7.3 Feedback sur les suggestions

Après une suggestion, l'utilisateur peut **accepter** ou **rejeter** la suggestion. Ce feedback est enregistré (`assignment_events`) et améliore les suggestions futures pour le workspace.

---

## 8. Cycles (sprints)

Les **cycles** (UC-08) permettent d'organiser le travail en sprints ou itérations temporelles.

### 8.1 Créer un cycle

Depuis `/workspaces/{slug}/projects/{projectId}/cycles` → **+ Nouveau cycle** :

- **Nom** (ex. "Sprint 1")
- **Date de début** et **date de fin**

### 8.2 Ajouter des issues à un cycle

Dans la fiche d'une issue, champ **Cycle** → sélectionner le cycle cible.

Ou depuis la vue cycle : bouton **Ajouter des issues** → filtrer et sélectionner en masse.

### 8.3 Suivi d'avancement

La vue cycle affiche :
- Issues planifiées vs. terminées
- Barre de progression globale
- Décompte des jours restants
- Liste des issues par statut

---

## 9. Pages wiki

Les **pages** (UC-10) sont un wiki collaboratif intégré au workspace.

### 9.1 Créer une page

Depuis `/workspaces/{slug}/pages` → **+ Nouvelle page** :

- Titre
- Contenu avec l'éditeur riche (formatage Markdown, blocs de code, listes, tableaux)
- Une page peut être imbriquée sous une page parente (hiérarchie)

### 9.2 Organiser les pages

Les pages sont listées dans le menu latéral gauche (section Pages), avec leur hiérarchie. Il est possible de réorganiser l'ordre par drag-and-drop.

### 9.3 Visibilité

Les pages sont visibles par tous les membres du workspace. Elles ne sont pas spécifiques à un projet.

---

## 10. Chat & discussions

TaskForce intègre deux modes de communication :

### 10.1 Chat temps réel (UC-09)

Le **chat** fonctionne par **canaux** attachés à des projets. Les messages sont envoyés en temps réel via WebSocket (STOMP/SockJS + RabbitMQ).

**Accès** : `/workspaces/{slug}/projects/{projectId}/channels`

- Créer un canal (#backend, #général…)
- Envoyer des messages avec support Markdown
- Mentions `@utilisateur` (l'utilisateur reçoit une notification)
- Les messages sont persistés — l'historique est accessible après reconnexion

### 10.2 Discussions (forum)

Les **discussions** sont des fils de conversation asynchrones liés à un projet, avec sous-catégories.

**Accès** : `/workspaces/{slug}/projects/{projectId}/discussions`

Idéales pour les décisions d'architecture, annonces d'équipe ou questions techniques hors issue.

---

## 11. Plans & facturation

### 11.1 Plans disponibles

| Plan | Public cible | Fonctionnalités |
|---|---|---|
| **FREE** | Particuliers, petites équipes | Workspaces basiques, projets, issues, pages, chat |
| **PRO** | Équipes professionnelles | Toutes les fonctionnalités FREE + Smart Assign avancé, analytiques, intégrations |
| **ENTERPRISE** | Grandes organisations | Toutes les fonctionnalités PRO + support dédié, configuration sur mesure, SLA |

### 11.2 Passer à un plan payant (UC-11)

1. Aller dans `/profile/billing` (ou depuis Paramètres du workspace → Facturation)
2. Cliquer sur **Mettre à niveau**
3. Paiement sécurisé via Stripe (carte bancaire)
4. Le plan est activé immédiatement après paiement

**Facturation** : abonnement mensuel avec renouvellement automatique. Un email de facture est envoyé à chaque renouvellement.

### 11.3 Portail de facturation

Accessible depuis `/profile/billing` → **Gérer mon abonnement** : visualiser les factures, modifier les informations de paiement, annuler l'abonnement.

> La gestion du paiement est entièrement déléguée à Stripe. TaskForce ne stocke jamais de données de carte bancaire.

---

## 12. Profil, données & RGPD

### 12.1 Paramètres du profil

**Accès** : `/profile/settings`

- Modifier le nom d'affichage
- Changer l'avatar (upload via MinIO)
- Préférences de thème (clair/sombre)
- Préférences de notifications

### 12.2 Exporter ses données (UC-12 — Art. 20 RGPD)

**Accès** : `/profile/settings` → **Exporter mes données**

Cette action déclenche `GET /api/gdpr/export` et télécharge un fichier JSON contenant :
- Profil (email, nom, dates)
- Memberships et rôles
- Profil de compétences
- Worklogs

### 12.3 Supprimer son compte (UC-12 — Art. 17 RGPD)

**Accès** : `/profile/settings` → **Supprimer mon compte**

> ⚠️ Cette action est **irréversible**. Elle déclenche `DELETE /api/gdpr/delete-account` et :
> - Anonymise l'email → `deleted-{id}@anonymized.invalid`
> - Supprime le nom d'affichage et l'avatar
> - Révoque tous les tokens de session
> - Désactive le compte (`isActive = false`)

Pour des raisons légales (comptabilité), les historiques de facturation sont conservés selon les obligations légales (10 ans).

---

> 🔗 [[FAQ]] — [[Guid_Installation]] — [[Release_Notes]] — [[Spec_API_OpenAPI]] (endpoints)
