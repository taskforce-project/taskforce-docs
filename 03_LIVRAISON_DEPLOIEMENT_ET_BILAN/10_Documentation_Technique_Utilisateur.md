# Documentation Technique et Utilisateur

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire

- [1. Introduction](#1-introduction)
- [2. Présentation de l'application](#2-présentation-de-lapplication)
- [3. Installation et configuration](#3-installation-et-configuration)
- [4. Utilisation de l'application](#4-utilisation-de-lapplication)
  - [4.1. Connexion et inscription](#41-connexion-et-inscription)
  - [4.2. Navigation dans l'application](#42-navigation-dans-lapplication)
  - [4.3. Fonctionnalités principales](#43-fonctionnalités-principales)
  - [4.4. Gestion du compte utilisateur](#44-gestion-du-compte-utilisateur)
  - [4.5. Autres fonctionnalités](#45-autres-fonctionnalités)
- [5. FAQ et dépannage](#5-faq-et-dépannage)
- [6. Support et contact](#6-support-et-contact)
- [7. Annexes](#7-annexes)

---

## 1. Introduction

### 1.1 À propos de TaskForce
**TaskForce** est une application de gestion de projets intelligente qui optimise la répartition des tâches au sein des équipes. Grâce à un système de matching basé sur les compétences, TaskForce propose automatiquement les collaborateurs les plus adaptés pour chaque tâche.

### 1.2 Public Cible
Ce document s'adresse à :
- **Administrateurs système** : Installation et configuration
- **Managers / Chefs de projet** : Gestion d'équipes et de projets
- **Collaborateurs** : Utilisation quotidienne

### 1.3 Conventions
- 🔒 : Nécessite des droits spécifiques
- ⚠️ : Point d'attention important
- 💡 : Conseil / Bonne pratique
- 🎯 : Fonctionnalité clé

---

## 2. Présentation de l'application

### 2.1 Fonctionnalités Principales

#### Pour les Managers
- 🎯 **Création de projets et tâches**
- 🎯 **Assignation intelligente** : Suggestions basées sur les compétences
- 📊 **Tableaux de bord** : Vue Kanban, suivi de la charge de travail
- 👥 **Gestion d'équipes** : Ajout/retrait de membres
- 📈 **Heatmap de charge** : Visualisation de la répartition du travail

#### Pour les Collaborateurs
- ✅ **Tableau de bord personnel** : Mes tâches en cours
- 🔄 **Mise à jour de statuts** : Avancement des tâches
- 💬 **Commentaires** : Discussion sur les tâches
- 📎 **Fichiers joints** : Upload/download de documents
- 🔔 **Notifications temps réel** : Nouvelles assignations, commentaires

#### Pour les Administrateurs
- 🔒 **Gestion des utilisateurs** : Activation/désactivation
- 📋 **Logs d'activité** : Traçabilité des actions

### 2.2 Architecture Technique

```
Frontend (Next.js + TypeScript) ←→ Backend (Spring Boot) ←→ PostgreSQL
                    ↑
              WebSocket (Notifications)
```

### 2.3 Prérequis Système

**Pour les Utilisateurs** :
- Navigateur moderne (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Connexion Internet stable
- Résolution d'écran : Min 1280x720 (responsive mobile)

**Pour les Développeurs / Admins** :
- Docker 24.x+
- Docker Compose 2.x+
- Java 21 (pour dev backend)
- Node.js 20+ (pour dev frontend)

---

## 3. Installation et configuration

### 3.1 Installation en Production (Serveur)

**Voir le document** : `09_Plan_Deploiement.md` pour la procédure complète.

**Résumé rapide** :
```bash
# Cloner le repository
git clone https://github.com/taskforce-project/taskforce-fullstack.git
cd taskforce-fullstack

# Configurer les variables d'environnement
cp .env.example .env.prod
nano .env.prod  # Éditer les secrets

# Lancer avec Docker Compose
docker-compose -f docker-compose.prod.yml up -d
```

### 3.2 Installation en Développement (Local)

#### Backend

```bash
cd backend/tf-api

# Avec Maven
./mvnw spring-boot:run

# Ou avec Docker
docker-compose -f ../../docker-compose-dev.yml up postgres backend
```

**Port** : http://localhost:8080

#### Frontend

```bash
cd frontend

# Installer les dépendances
npm install

# Lancer en mode dev
npm run dev
```

**Port** : http://localhost:3000

### 3.3 Configuration Initiale

#### Première Connexion (Administrateur)

1. Accéder à l'application : https://taskforce.local
2. Créer le premier compte (sera automatiquement ADMIN)
3. Se connecter
4. Accéder aux paramètres pour configurer :
   - Nom de l'organisation
   - Logo
   - Fuseau horaire

#### Création des Compétences (Skills)

💡 **Bonne pratique** : Définir les compétences **avant** de créer des utilisateurs.

1. Aller dans **Paramètres** → **Compétences**
2. Cliquer sur **+ Nouvelle compétence**
3. Renseigner :
   - Nom (ex: "Java", "React", "Management")
   - Catégorie (ex: "Backend", "Frontend", "Soft Skills")
4. Répéter pour toutes les compétences de votre organisation

---

## 4. Utilisation de l'application

### 4.1. Connexion et inscription

#### Inscription

1. Accéder à l'URL de l'application
2. Cliquer sur **"S'inscrire"**
3. Remplir le formulaire :
   - Email professionnel
   - Mot de passe (min 8 caractères, 1 majuscule, 1 chiffre)
   - Confirmer le mot de passe
4. Cliquer sur **"Créer un compte"**
5. Vous êtes redirigé vers le **Dashboard**

#### Connexion

1. Saisir votre **email**
2. Saisir votre **mot de passe**
3. (Optionnel) Cocher **"Se souvenir de moi"**
4. Cliquer sur **"Se connecter"**

⚠️ **Mot de passe oublié** :
- Cliquer sur "Mot de passe oublié ?"
- Saisir votre email
- Suivre les instructions reçues par email

### 4.2. Navigation dans l'application

#### Menu Principal (Sidebar)

| Icône | Section | Description |
|:------|:--------|:------------|
| 🏠 | **Dashboard** | Vue d'ensemble de vos tâches |
| 📁 | **Projets** | Liste de tous vos projets |
| 👥 | **Équipes** | Gestion des équipes (Managers) |
| 👤 | **Profil** | Votre profil et compétences |
| 🔔 | **Notifications** | Centre de notifications |
| ⚙️ | **Paramètres** | Configuration (Admins) |

#### Barre Supérieure

- **Recherche globale** : Rechercher projets, tâches, utilisateurs
- **Badge notifications** : Nombre de notifications non lues
- **Avatar utilisateur** : Menu déroulant (Profil, Déconnexion)

### 4.3. Fonctionnalités principales

#### A. Pour les Managers

##### 📁 Créer un Projet

1. Aller dans **Projets** → **+ Nouveau Projet**
2. Remplir le formulaire :
   - **Nom** : Nom du projet
   - **Description** : Objectifs et contexte
   - **Équipe** : Sélectionner l'équipe assignée
   - **Dates** : Date de début et de fin
   - **Budget** (optionnel)
3. Cliquer sur **"Créer le projet"**

##### ✅ Créer une Tâche

1. Ouvrir un projet
2. Cliquer sur **+ Nouvelle Tâche**
3. Remplir :
   - **Titre** : Titre court et descriptif
   - **Description** : Détails de la tâche (format Markdown supporté)
   - **Compétences requises** : Sélectionner les skills + niveau minimum
   - **Priorité** : Basse / Moyenne / Haute / Critique
   - **Estimation** : Nombre d'heures estimées
   - **Date limite** : Deadline
4. Cliquer sur **"Créer"**

🎯 **Suggestions d'assignation** : Après création, TaskForce affiche les **top 3 collaborateurs** les mieux adaptés avec leur score de matching.

##### 👤 Assigner une Tâche

**Option 1 : Assignation suggérée**
1. Cliquer sur un des candidats suggérés
2. Confirmer l'assignation

**Option 2 : Assignation manuelle**
1. Cliquer sur **"Assigner manuellement"**
2. Sélectionner un collaborateur dans la liste
3. Confirmer

⚠️ **Note** : Le collaborateur reçoit une notification immédiatement.

##### 📊 Vue Kanban

1. Ouvrir un projet
2. Sélectionner l'onglet **"Kanban"**
3. Les colonnes par défaut :
   - **À faire** (TODO)
   - **En cours** (IN_PROGRESS)
   - **En revue** (IN_REVIEW)
   - **Terminé** (DONE)
   - **Bloqué** (BLOCKED)

💡 **Drag & Drop** : Glisser-déposer les cartes pour changer les statuts.

##### 📈 Heatmap de Charge

1. Aller dans **Équipes** → Sélectionner votre équipe
2. Cliquer sur l'onglet **"Charge de travail"**
3. Visualiser :
   - 🟢 **Vert** : Disponible (< 30h/semaine)
   - 🟡 **Jaune** : Charge normale (30-40h)
   - 🟠 **Orange** : Chargé (40-50h)
   - 🔴 **Rouge** : Surcharge (> 50h)

#### B. Pour les Collaborateurs

##### 🏠 Dashboard Personnel

Au login, vous arrivez sur votre **Dashboard** qui affiche :
- **Mes tâches du jour** : Tâches prioritaires
- **Tâches en cours** : Toutes vos tâches IN_PROGRESS
- **Tâches à venir** : Tâches TODO assignées
- **Statistiques** : Nombre de tâches complétées ce mois

##### 🔄 Mettre à Jour le Statut d'une Tâche

1. Ouvrir une tâche depuis votre dashboard
2. Cliquer sur le **bouton de statut actuel**
3. Sélectionner le nouveau statut :
   - **Démarrer** (TODO → IN_PROGRESS)
   - **Mettre en revue** (IN_PROGRESS → IN_REVIEW)
   - **Terminer** (IN_REVIEW → DONE)
   - **Bloquer** (si problème)

⚠️ **Tâches bloquées** : Si vous bloquez une tâche, laissez un commentaire pour expliquer le blocage.

##### 💬 Ajouter un Commentaire

1. Scroller vers la section **"Discussion"**
2. Saisir votre commentaire (Markdown supporté)
3. (Optionnel) Mentionner un utilisateur avec `@nom`
4. Cliquer sur **"Envoyer"**

💡 **Notifications** : Tous les participants de la tâche (créateur + assigné + commentateurs) reçoivent une notification.

##### 📎 Joindre un Fichier

1. Cliquer sur **"📎 Joindre un fichier"**
2. Sélectionner le fichier (max 10 MB)
3. Types acceptés :
   - Images : JPG, PNG, GIF
   - Documents : PDF, TXT
   - Tableurs : XLS, XLSX
4. Le fichier apparaît dans la liste des pièces jointes

💡 **Télécharger** : Cliquer sur le nom du fichier pour télécharger.

#### C. Notifications

##### 🔔 Centre de Notifications

1. Cliquer sur l'icône **🔔** dans la barre supérieure
2. Types de notifications :
   - ✅ **Tâche assignée** : Une tâche vous a été assignée
   - 💬 **Nouveau commentaire** : Commentaire sur une de vos tâches
   - ⏰ **Deadline proche** : Échéance dans moins de 24h
   - 🔴 **Surcharge détectée** : Alerte si > 50h de travail

##### Actions
- **Cliquer sur une notification** : Ouvre la tâche/projet concerné et marque comme lu
- **Marquer toutes comme lues** : Bouton en haut du panneau
- **Filtrer** : Par type ou date

### 4.4. Gestion du compte utilisateur

#### 👤 Compléter son Profil

1. Cliquer sur votre **Avatar** → **Profil**
2. Sections :
   - **Informations personnelles** :
     - Prénom, Nom
     - Photo de profil (upload)
     - Biographie (250 caractères max)
   - **Compétences** :
     - Cliquer sur **+ Ajouter une compétence**
     - Sélectionner la compétence
     - Définir votre niveau (1-5 étoiles)
     - (Optionnel) Années d'expérience
   - **Disponibilité** :
     - Heures par semaine (temps plein = 35-40h)
     - Congés à venir

💡 **Importance des compétences** : Plus votre profil est complet, meilleures sont les suggestions d'assignation.

#### 🔒 Changer son Mot de Passe

1. Aller dans **Profil** → **Sécurité**
2. Cliquer sur **"Changer mon mot de passe"**
3. Saisir :
   - Mot de passe actuel
   - Nouveau mot de passe (min 8 caractères)
   - Confirmer le nouveau mot de passe
4. Cliquer sur **"Valider"**

### 4.5. Autres fonctionnalités

#### 👥 Gestion des Équipes (Managers)

##### Créer une Équipe

1. Aller dans **Équipes** → **+ Nouvelle Équipe**
2. Remplir :
   - Nom de l'équipe
   - Description
3. Cliquer sur **"Créer"**

##### Ajouter des Membres

1. Ouvrir l'équipe
2. Onglet **"Membres"**
3. Cliquer sur **+ Ajouter un membre**
4. Sélectionner l'utilisateur
5. Confirmer

##### Retirer un Membre

1. Cliquer sur **⋮** à côté du membre
2. Sélectionner **"Retirer de l'équipe"**
3. Confirmer

⚠️ **Attention** : Retirer un membre le désassigne de toutes les tâches en cours dans les projets de cette équipe.

---

## 5. FAQ et dépannage

### 5.1 Questions Fréquentes

#### Q1 : Comment fonctionne le matching de compétences ?

**R** : TaskForce compare les compétences requises par la tâche avec celles déclarées par les utilisateurs. Un score est calculé :
- **100%** : Toutes les compétences requises + niveau suffisant
- **< 50%** : Compétences manquantes (non affiché dans les suggestions)

Le niveau de compétence (1-5) et le caractère obligatoire/optionnel influencent le score.

#### Q2 : Puis-je modifier une tâche après l'avoir créée ?

**R** : Oui. Ouvrez la tâche et cliquez sur **✏️ Modifier**. Les changements sont sauvegardés automatiquement.

#### Q3 : Les notifications sont-elles envoyées par email ?

**R** : Dans la v1.0 (MVP), les notifications sont **uniquement in-app** (temps réel via WebSocket). Les notifications email seront disponibles dans la v2.0.

#### Q4 : Puis-je assigner une tâche à plusieurs personnes ?

**R** : Non, dans la v1.0, une tâche = un assigné. Si le travail nécessite plusieurs personnes, créez des sous-tâches.

#### Q5 : Que faire si je ne reçois pas les notifications temps réel ?

**R** :
1. Vérifier que votre navigateur autorise les notifications
2. Rafraîchir la page (F5)
3. Vérifier votre connexion Internet
4. Si le problème persiste, contacter le support

### 5.2 Dépannage

#### Problème : Je ne peux pas me connecter

**Solutions** :
1. Vérifier que l'email et le mot de passe sont corrects
2. Utiliser "Mot de passe oublié ?" si nécessaire
3. Vider le cache du navigateur (Ctrl+Shift+Del)
4. Essayer en navigation privée
5. Contacter l'administrateur si votre compte est désactivé

#### Problème : Les tâches ne s'affichent pas dans le Kanban

**Solutions** :
1. Rafraîchir la page (F5)
2. Vérifier que vous êtes bien membre de l'équipe du projet
3. Vérifier les filtres appliqués (statut, assigné)
4. Vider le cache du navigateur

#### Problème : Impossible d'uploader un fichier

**Causes possibles** :
- Fichier > 10 MB → Compresser ou utiliser un lien externe
- Type de fichier non supporté → Vérifier la liste des types acceptés
- Connexion Internet instable → Réessayer

#### Problème : Performance lente

**Solutions** :
1. Vérifier votre connexion Internet
2. Fermer les onglets inutilisés
3. Vider le cache du navigateur
4. Utiliser un navigateur récent (Chrome/Firefox)
5. Contacter l'administrateur si le problème persiste (charge serveur ?)

---

## 6. Support et contact

### 6.1 Assistance

**Email** : support@taskforce.local  
**Heures de support** : Lundi-Vendredi, 9h-18h

**Temps de réponse** :
- 🔴 Critique (app inaccessible) : < 4h
- 🟠 Majeur (fonctionnalité bloquée) : < 24h
- 🟡 Mineur (question, amélioration) : < 48h

### 6.2 Signaler un Bug

**Via GitHub** :
1. Aller sur https://github.com/taskforce-project/taskforce-fullstack/issues
2. Cliquer sur **"New Issue"**
3. Utiliser le template "🐛 Bug Report"
4. Remplir tous les champs (étapes de reproduction, environnement)

**Via Email** :
Envoyer à support@taskforce.local avec :
- Titre descriptif
- Étapes de reproduction
- Captures d'écran si possible
- Navigateur et OS

### 6.3 Demander une Fonctionnalité

**Via GitHub** :
1. Issues → New Issue → "✨ Feature Request"
2. Décrire le besoin et le bénéfice attendu

---

## 7. Annexes

### 7.1 Raccourcis Clavier

| Raccourci | Action |
|:----------|:-------|
| `Ctrl + K` | Ouvrir la recherche globale |
| `Ctrl + N` | Nouvelle tâche (dans un projet) |
| `Ctrl + ,` | Ouvrir les paramètres |
| `Esc` | Fermer une modale |
| `Ctrl + Enter` | Envoyer un commentaire |

### 7.2 Glossaire

- **Assignation** : Action d'attribuer une tâche à un collaborateur
- **Heatmap** : Carte de chaleur visualisant la charge de travail
- **Kanban** : Méthode de gestion visuelle avec des colonnes (TODO, IN_PROGRESS, DONE)
- **Matching** : Algorithme de correspondance compétences requises / compétences utilisateurs
- **MVP** : Minimum Viable Product (version 1.0)
- **Skill** : Compétence technique ou soft skill
- **Sprint** : Itération de développement (1 semaine dans ce projet)
- **WebSocket** : Protocole de communication temps réel (notifications)

### 7.3 API Documentation (Pour Développeurs)

**Swagger UI** : https://taskforce.local/swagger-ui.html

**Endpoints principaux** :
- `POST /api/auth/register` : Inscription
- `POST /api/auth/login` : Connexion
- `GET /api/tasks` : Liste des tâches
- `POST /api/tasks` : Créer une tâche
- `GET /api/tasks/{id}/suggestions` : Suggestions d'assignation
- `PUT /api/tasks/{id}/assign` : Assigner une tâche

**Authentification** : Bearer Token (JWT) dans le header `Authorization`

### 7.4 Liens Utiles

- **Repository GitHub** : https://github.com/taskforce-project/taskforce-fullstack
- **Documentation Développeur** : Voir `README.md` et `07_Dossier_Conception_Technique.md`
- **Roadmap** : Voir `05_Suivi_Agile_Roadmap.md`

---

**Version du document** : 1.0  
**Dernière mise à jour** : Juin 2026  
**Auteur** : Pierre MICHEL  
**Contact** : pierre.michel@taskforce.local

