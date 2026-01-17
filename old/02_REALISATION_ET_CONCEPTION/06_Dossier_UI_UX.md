# Dossier UI/UX

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire

- [1. Introduction](#1-introduction)
- [2. Recherche utilisateur](#2-recherche-utilisateur)
- [3. Personas](#3-personas)
- [4. Parcours utilisateur (User Journey)](#4-parcours-utilisateur-user-journey)
- [5. Wireframes](#5-wireframes)
- [6. Prototypes](#6-prototypes)
- [7. Tests utilisateur](#7-tests-utilisateur)
- [8. Conclusion et recommandations](#8-conclusion-et-recommandations)
- [9. Annexes](#9-annexes)

---

## 1. Introduction

### 1.1 Objectif du Document
Ce dossier présente la démarche UX/UI suivie pour concevoir l'interface de **TaskForce**. Il documente la recherche utilisateur, les personas, les parcours, les wireframes et les prototypes finaux.

### 1.2 Méthodologie Design Thinking
La conception a suivi les 5 étapes du Design Thinking :
1. **Empathize** : Recherche utilisateur et analyse des besoins
2. **Define** : Définition des personas et problématiques
3. **Ideate** : Brainstorming et croquis d'interfaces
4. **Prototype** : Maquettes haute fidélité (Figma)
5. **Test** : Tests utilisateurs et itérations

---

## 2. Recherche utilisateur

### 2.1 Contexte et Problématique

**Problème identifié** :
Les managers perdent beaucoup de temps à assigner manuellement les tâches en se basant sur leur connaissance partielle des compétences de l'équipe. Les collaborateurs, de leur côté, se retrouvent parfois avec des tâches inadaptées à leurs compétences ou une charge inégalement répartie.

### 2.2 Études de Marché

**Analyse des Concurrents** :
| Outil | Forces | Faiblesses | Différenciation TaskForce |
|:------|:-------|:-----------|:--------------------------|
| **Jira** | Très complet, intégrations | Complexe, courbe d'apprentissage | Interface simple, matching auto |
| **Trello** | Simple, visuel (Kanban) | Pas d'assignation intelligente | Algorithme de suggestion |
| **Asana** | Collaboration, timeline | Assignation manuelle uniquement | Automatisation basée sur skills |
| **Monday.com** | Personnalisable, coloré | Prix élevé, pas de matching | Focus sur les compétences |

**Conclusion** : Aucun concurrent ne propose d'**assignation automatique basée sur les compétences**.

### 2.3 Interviews Utilisateurs (Fictives - Phase Cadrage)

**Profils Interrogés** :
- 3 Managers / Chefs de Projet
- 5 Développeurs / Collaborateurs

**Besoins Exprimés** :

**Managers** :
- ✅ "Je voudrais savoir instantanément qui est disponible et compétent pour une tâche"
- ✅ "Visualiser la charge de travail de mon équipe en un coup d'œil"
- ✅ "Éviter les surcharges qui mènent au burn-out"

**Collaborateurs** :
- ✅ "Recevoir des tâches qui correspondent à mes compétences"
- ✅ "Savoir clairement ce que j'ai à faire aujourd'hui"
- ✅ "Communiquer facilement sur les tâches (commentaires, fichiers)"

---

## 3. Personas

### 3.1 Persona 1 : Sophie Martins - Manager de Projet

![Persona Manager](../assets/images/persona-manager.png)

**Profil** :
- **Âge** : 38 ans
- **Rôle** : Chef de Projet Web
- **Expérience** : 12 ans dans la gestion de projet
- **Environnement** : Équipe de 8 développeurs (full-stack, front, back, design)

**Objectifs** :
- Livrer les projets dans les temps et dans le budget
- Optimiser la productivité de l'équipe
- Maintenir un bon climat de travail (éviter les surcharges)

**Frustrations** :
- ❌ Difficulté à savoir qui est disponible et compétent en temps réel
- ❌ Temps perdu à réassigner des tâches mal distribuées
- ❌ Manque de visibilité sur la charge de chacun

**Comportement Digital** :
- Utilise quotidiennement : Jira, Slack, Excel
- Apprécie les interfaces épurées et rapides
- Consulte l'app plusieurs fois par jour (mobile + desktop)

**Citation** :
> "J'aimerais que l'outil me suggère la bonne personne au lieu de deviner moi-même."

---

### 3.2 Persona 2 : Lucas Dubois - Développeur Backend

![Persona Collaborateur](../assets/images/persona-collaborateur.png)

**Profil** :
- **Âge** : 28 ans
- **Rôle** : Développeur Backend (Java/Spring)
- **Expérience** : 5 ans
- **Environnement** : Travaille sur 2-3 projets simultanément

**Objectifs** :
- Travailler sur des tâches qui correspondent à ses compétences
- Progresser techniquement (nouvelles technos)
- Avoir une charge de travail équilibrée

**Frustrations** :
- ❌ Recevoir des tâches pour lesquelles il n'est pas qualifié
- ❌ Ne pas savoir quelle tâche prioriser (trop de notifications)
- ❌ Passer du temps à chercher les infos éparpillées (emails, Slack, Trello)

**Comportement Digital** :
- Utilise : VS Code, GitHub, Notion, Spotify
- Préfère les interfaces dark mode
- Aime les raccourcis clavier

**Citation** :
> "Donnez-moi juste la liste de ce que j'ai à faire aujourd'hui, et laissez-moi coder."

---

### 3.3 Persona 3 : Admin Système (Bonus)

**Profil** :
- **Rôle** : Administrateur IT
- **Objectifs** : Sécuriser l'application, gérer les accès utilisateurs, maintenir la disponibilité
- **Besoins** : Logs d'activité, gestion des rôles, monitoring

---

## 4. Parcours utilisateur (User Journey)

### 4.1 User Journey - Manager : "Création de Projet et Assignation de Tâches"

```
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 1 : Connexion                                            │
├─────────────────────────────────────────────────────────────────┤
│  Action : Sophie se connecte à TaskForce                        │
│  Émotion : 😐 Neutre                                            │
│  Pensée : "Voyons ce que je dois faire aujourd'hui"            │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 2 : Dashboard Manager                                    │
├─────────────────────────────────────────────────────────────────┤
│  Action : Voir vue d'ensemble des projets actifs               │
│  Émotion : 🙂 Satisfait                                         │
│  Pensée : "Bon, le projet X est en retard, je dois agir"       │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 3 : Création d'une Nouvelle Tâche                        │
├─────────────────────────────────────────────────────────────────┤
│  Action : Créer tâche "Implémenter API paiement Stripe"        │
│  Émotion : 🤔 Concentré                                         │
│  Pensée : "Qui a les compétences API + Payment ?"              │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 4 : Suggestions d'Assignation (🎯 Moment clé)            │
├─────────────────────────────────────────────────────────────────┤
│  Action : Voir top 3 candidats avec scores                     │
│  Émotion : 😍 Ravi !                                            │
│  Pensée : "Wow, Lucas a 95% de match ! C'est parfait"         │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 5 : Assignation en 1 Clic                                │
├─────────────────────────────────────────────────────────────────┤
│  Action : Cliquer sur "Assigner à Lucas"                       │
│  Émotion : ✅ Satisfait                                         │
│  Pensée : "Terminé en 30 secondes, génial !"                   │
└─────────────────────────────────────────────────────────────────┘
```

**Points de Friction Identifiés** : Aucun (parcours optimisé)

**Points de Satisfaction** :
- 🎯 Suggestions pertinentes
- ⚡ Rapidité (< 1 minute pour créer et assigner)
- 📊 Visibilité sur la charge de l'équipe

---

### 4.2 User Journey - Collaborateur : "Gestion de Mes Tâches Quotidiennes"

```
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 1 : Connexion & Dashboard                                │
├─────────────────────────────────────────────────────────────────┤
│  Action : Lucas se connecte le matin                            │
│  Émotion : 🙂 Motivé                                            │
│  Pensée : "Voyons ce que j'ai à faire aujourd'hui"            │
│  Interface : Dashboard avec section "Mes tâches du jour" (3)   │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 2 : Notification de Nouvelle Tâche                       │
├─────────────────────────────────────────────────────────────────┤
│  Action : Badge 🔴 1 apparaît                                   │
│  Émotion : 🤔 Curieux                                           │
│  Pensée : "Une nouvelle tâche ? Voyons..."                     │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 3 : Consultation de la Tâche                             │
├─────────────────────────────────────────────────────────────────┤
│  Action : Ouvre la tâche "API paiement Stripe"                 │
│  Émotion : 😊 Satisfait                                         │
│  Pensée : "Cool, c'est dans mes compétences !"                 │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 4 : Mise à Jour du Statut                                │
├─────────────────────────────────────────────────────────────────┤
│  Action : Clic "Démarrer" (TODO → IN_PROGRESS)                 │
│  Émotion : ⚡ Actif                                             │
│  Pensée : "Allez, on code !"                                    │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  ÉTAPE 5 : Ajout d'un Commentaire (+ tard)                      │
├─────────────────────────────────────────────────────────────────┤
│  Action : "Besoin de la clé API Stripe de prod"                │
│  Émotion : 💬 Communicatif                                      │
│  Pensée : "Plus besoin de Slack, tout est centralisé"         │
└─────────────────────────────────────────────────────────────────┘
```

**Points de Friction** :
- ⚠️ Si trop de notifications → Surcharge cognitive (à gérer avec filtres)

**Points de Satisfaction** :
- ✅ Clarté : "Mes tâches du jour" bien visible
- ✅ Notifications pertinentes (pas de spam)
- ✅ Tout centralisé (pas besoin d'aller sur Slack/Email)

---

## 5. Wireframes

### 5.1 Wireframes Basse Fidélité (Croquis)

**Landing Page** :
```
┌──────────────────────────────────────────────────┐
│  [Logo] TaskForce         [Login] [Sign Up]     │
├──────────────────────────────────────────────────┤
│                                                  │
│      Gérez vos projets intelligemment            │
│      avec l'assignation automatique              │
│                                                  │
│          [Try for Free]  [Watch Demo]            │
│                                                  │
│      [Image Hero : Dashboard Preview]            │
│                                                  │
├──────────────────────────────────────────────────┤
│  Features : 🎯 Matching | 📊 Kanban | 🔔 Notif   │
└──────────────────────────────────────────────────┘
```

**Dashboard Collaborateur** :
```
┌─────────┬──────────────────────────────────────┐
│ Sidebar │  Mes Tâches                    🔔 3  │
│         ├──────────────────────────────────────┤
│ 🏠 Home │  📌 Aujourd'hui                       │
│ 📁 Proj │  ┌──────────────────────────────────┐ │
│ 👤 Prof │  │ [CARD] API Payment (IN_PROGRESS)│ │
│ 🔔 Not  │  │ Priorité: Haute | 8h | J-2       │ │
│         │  └──────────────────────────────────┘ │
│         │  ┌──────────────────────────────────┐ │
│         │  │ [CARD] Fix Bug Login (TODO)     │ │
│         │  └──────────────────────────────────┘ │
└─────────┴──────────────────────────────────────┘
```

### 5.2 Wireframes Moyenne Fidélité

*(Ces wireframes seraient normalement créés dans Figma, Balsamiq ou Sketch avec plus de détails : typographie, espacements, hiérarchie visuelle)*

**Vue Kanban Projet** :
```
┌─────────────────────────────────────────────────┐
│  Projet: E-commerce Refonte          [+ Task]  │
├──────────────┬──────────────┬─────────────────┤
│  TODO (5)    │ IN_PROGRESS  │  DONE (12)      │
├──────────────┼──────────────┼─────────────────┤
│ [Card]       │ [Card]       │ [Card]          │
│ Setup DB     │ API Users    │ Login Page      │
│ 👤 Unassigned│ 👤 Lucas     │ 👤 Marie        │
│ ⏰ 5j        │ ⏰ 2j        │ ✅ 29/11        │
├──────────────┼──────────────┼─────────────────┤
│ [Card]       │              │                 │
│ Design UI    │              │                 │
│ 👤 Sophie    │              │                 │
└──────────────┴──────────────┴─────────────────┘
```

---

## 6. Prototypes

**Landing page**
![Landing page - taskforce](../assets/maquettes/landing_page_01.png)
![Landing page - taskforce](../assets/maquettes/landing_page_02.png)
![Landing page - taskforce](../assets/maquettes/landing_page_03.png)
![Landing page - taskforce](../assets/maquettes/landing_page_04.png)
![Landing page - taskforce](../assets/maquettes/landing_page_05.png)

**Portail de connexion et création de compte:**
![Portail de connexion - taskforce](../assets/maquettes/login.png)
![Portail de connexion - taskforce](../assets/maquettes/register.png)

**Dashboard :**
![Dashboard - taskforce](../assets/maquettes/dashboard.png)

**Modules - Utilisateurs**
![Utilisateurs - taskforce](../assets/maquettes/module_utilisateurs.png)

**Modules - Projets 1**
![Projets 1 - taskforce](../assets/maquettes/module_projets_1.png)

**Modules - Projets 2**
![Projets 2 - taskforce](../assets/maquettes/module_projets_2.png)

**Paramètres**
![Paramètres - taskforce](../assets/maquettes/parametres.png)

**Profil**
![Profil - taskforce](../assets/maquettes/profile.png)

---

## 7. Tests utilisateur

### 7.1 Méthodologie de Test

**Phase** : Sprint 21-22 (Recette)

**Participants** :
- 2 Managers (enseignants MNS)
- 3 Collaborateurs (étudiants)

**Format** :
1. **Briefing** (5 min) : Présentation de l'app
2. **Test libre** (15 min) : Exploration sans contrainte
3. **Scénarios guidés** (30 min) :
   - Scénario 1 : Créer un projet et une tâche
   - Scénario 2 : Assigner une tâche avec matching
   - Scénario 3 : Collaborateur met à jour une tâche
4. **Debriefing** (10 min) : Questions + questionnaire

### 7.2 Grille d'Évaluation

| Critère | Score (1-5) | Commentaires |
|:--------|:------------|:-------------|
| **Facilité d'utilisation** | ⭐⭐⭐⭐⭐ | Très intuitif |
| **Clarté de l'interface** | ⭐⭐⭐⭐⭐ | Lisible, pas surchargé |
| **Pertinence des suggestions** | ⭐⭐⭐⭐☆ | Matching bon mais perfectible |
| **Rapidité** | ⭐⭐⭐⭐⭐ | Très réactif |
| **Design visuel** | ⭐⭐⭐⭐☆ | Moderne, quelques ajustements couleurs |

### 7.3 Retours Principaux

**Points Positifs** :
- ✅ "L'assignation suggérée est un vrai gain de temps !"
- ✅ "Le dashboard collaborateur est clair, je sais quoi faire"
- ✅ "Le design est épuré, pas de distraction"

**Points d'Amélioration** :
- ⚠️ "Ajouter un filtre par priorité dans le Kanban"
- ⚠️ "Permettre de trier les tâches par date"
- ⚠️ "Mode sombre serait apprécié"

### 7.4 Itérations Post-Test

**Changements appliqués** :
1. ✅ Ajout du filtre priorité (Sprint 22)
2. ✅ Tri des tâches par date/priorité (Sprint 22)
3. 🔄 Mode sombre → Backlog v1.1 (post-MVP)

---

## 8. Conclusion et recommandations

### 8.1 Bilan UX

**Forces** :
- 🎯 **Innovation** : Matching compétences unique sur le marché
- ⚡ **Simplicité** : Parcours utilisateurs fluides (< 3 clics pour l'essentiel)
- 📊 **Visibilité** : Informations importantes bien mises en avant

**Axes d'Amélioration** :
- Enrichir le système de matching avec historique de performance (v2)
- Ajouter des animations micro-interactions pour plus de feedback
- Améliorer l'accessibilité (lecteurs d'écran, navigation clavier)

### 8.2 Recommandations pour la v2

1. **Personnalisation** : Permettre aux users de choisir leur layout (Kanban, Liste, Gantt)
2. **Mobile App** : Version native iOS/Android pour notifications push
3. **Gamification** : Badges, points pour encourager l'utilisation
4. **Intégrations** : Slack, Microsoft Teams, GitHub

### 8.3 Design System

**Palette de Couleurs** :
- **Primary** : Bleu (#3B82F6) - Actions principales
- **Success** : Vert (#10B981) - Validations
- **Warning** : Orange (#F59E0B) - Alertes
- **Danger** : Rouge (#EF4444) - Erreurs
- **Neutral** : Gris (#6B7280) - Textes secondaires

**Typographie** :
- **Headings** : Inter Bold
- **Body** : Inter Regular
- **Code** : JetBrains Mono

**Composants** : Utilisation de **Shadcn/ui** (basé sur Radix UI) pour cohérence et accessibilité.

---

## 9. Annexes

### 9.1 Lien Figma

**Prototypes interactifs** : [Figma - TaskForce Prototypes](https://figma.com/taskforce-prototypes)

*(Lien fictif - à remplacer par le lien réel)*

### 9.2 Charte Graphique

**Logo** :
- Versions : Couleur, Noir & Blanc, Monochrome
- Formats : SVG, PNG (512x512, 256x256, 128x128)

**Iconographie** :
- **Bibliothèque** : Lucide Icons (cohérent avec Shadcn/ui)
- **Style** : Outline, 24x24px

### 9.3 Inspiration & Benchmarks

**Sites Analysés** :
- Linear.app (UI minimaliste, shortcuts clavier)
- Notion.so (Hiérarchie claire, personnalisation)
- Asana (Vues multiples, couleurs)

---

**Version du document** : 1.0  
**Dernière mise à jour** : Décembre 2025  
**Designer UX/UI** : Pierre MICHEL  
**Outils utilisés** : Figma, FigJam, Balsamiq

**Landing page**
![Landing page - taskforce](../assets/maquettes/landing_page_01.png)
![Landing page - taskforce](../assets/maquettes/landing_page_02.png)
![Landing page - taskforce](../assets/maquettes/landing_page_03.png)
![Landing page - taskforce](../assets/maquettes/landing_page_04.png)
![Landing page - taskforce](../assets/maquettes/landing_page_05.png)

**Portail de connexion et création de compte:**
![Portail de connexion - taskforce](../assets/maquettes/login.png)
![Portail de connexion - taskforce](../assets/maquettes/register.png)

**Dashboard :**
![Dashboard - taskforce](../assets/maquettes/dashboard.png)

**Modules - Utilisateurs**
![Utilisateurs - taskforce](../assets/maquettes/module_utilisateurs.png)

**Modules - Projets 1**
![Projets 1 - taskforce](../assets/maquettes/module_projets_1.png)

**Modules - Projets 2**
![Projets 2 - taskforce](../assets/maquettes/module_projets_2.png)

**Paramètres**
![Paramètres - taskforce](../assets/maquettes/parametres.png)

**Profil**
![Profil - taskforce](../assets/maquettes/profile.png)
