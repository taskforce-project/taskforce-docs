# 02 - Cahier des Charges Fonctionnel (CdCF)

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

---

## 📋 Informations générales

| Champ | Valeur |
|-------|--------|
| **Projet** | TaskForce - Gestion de projets et assignation intelligente |
| **Document** | Cahier des Charges Fonctionnel (CdCF) |
| **Auteur** | Michel-Pierre |
| **Date de création** | 4 janvier 2026 |
| **Version** | 1.0 |
| **Statut** | 🔄 En cours de rédaction |

---

## 📖 Sommaire

1. [Introduction](#1-introduction)
2. [Vision produit](#2-vision-produit)
3. [Audit de marché et benchmark](#3-audit-de-marché-et-benchmark)
4. [User Personas](#4-user-personas)
5. [Fonctionnalités détaillées](#5-fonctionnalités-détaillées)
6. [Règles métier](#6-règles-métier)
7. [Exigences non fonctionnelles](#7-exigences-non-fonctionnelles)
8. [Critères d'acceptation globaux](#8-critères-dacceptation-globaux)

---

## 1. Introduction

### 1.1 Objet du document

Ce **Cahier des Charges Fonctionnel (CdCF)** définit de manière exhaustive les besoins fonctionnels et les spécifications de l'application **TaskForce**. Il sert de référence contractuelle entre :
- Le porteur du projet (Michel-Pierre)
- Les encadrants pédagogiques (Metz Numeric School)
- Les futurs utilisateurs de l'application

### 1.2 Portée du document

Ce document couvre :
- ✅ La vision produit et le positionnement marché
- ✅ L'analyse concurrentielle (benchmark)
- ✅ Les profils utilisateurs (personas)
- ✅ Les 26 fonctionnalités détaillées (User Stories)
- ✅ Les règles métier et contraintes fonctionnelles
- ✅ Les exigences non fonctionnelles (performance, sécurité, UX)

### 1.3 Références

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Dossier projet global
- [03_CdCT.md](03_CdCT.md) - Cahier des Charges Technique
- [06_User_Stories_Backlog.md](06_User_Stories_Backlog.md) - Backlog détaillé des US
- CDC fourni par Metz Numeric School (PDF)

---

## 2. Vision produit

### 2.1 Vision globale

**TaskForce** est une plateforme web moderne de **gestion de projets collaboratifs** qui révolutionne l'assignation des tâches grâce à un **système de matching intelligent basé sur les compétences**.

**Promesse de valeur** :
> *"Optimisez la productivité de votre équipe en assignant automatiquement les bonnes tâches aux bonnes personnes, au bon moment."*

### 2.2 Problème résolu

**Pour** les chefs de projet et managers d'équipes agiles  
**Qui** peinent à répartir efficacement les tâches selon les compétences réelles de chaque membre  
**TaskForce** est une **application de gestion de projets**  
**Qui** propose automatiquement les meilleurs collaborateurs pour chaque tâche en fonction de leurs compétences, disponibilité et charge de travail  
**Contrairement à** Trello, Asana ou Jira qui ne font que de l'assignation manuelle  
**Notre produit** optimise l'utilisation des ressources humaines et prévient la surcharge

### 2.3 Objectifs produit

| Objectif | Indicateur de succès |
|----------|---------------------|
| **Gain de temps** | Réduction de 50% du temps d'assignation manuelle |
| **Meilleure répartition** | Équilibre de charge à ±15% entre membres d'équipe |
| **Satisfaction utilisateurs** | NPS ≥ 40 (Net Promoter Score) |
| **Adoption** | 80% des tâches assignées via suggestions IA |
| **Prévention burn-out** | Alertes précoces avec 90% de précision |

### 2.4 Positionnement unique

**Fonctionnalité différenciante** : **Matching intelligent compétences/tâches**

TaskForce se positionne comme :
- 🎯 **Plus intelligent** que Trello (assignation basique)
- 💡 **Plus accessible** que Jira (complexité réduite)
- 🚀 **Plus agile** qu'Asana (focus sur les compétences)

---

## 3. Audit de marché et benchmark

### 3.1 Analyse concurrentielle

> **📌 Note** : Tableau comparatif détaillé à compléter dans `assets/charts/Benchmark_Concurrents.xlsx`

| Critère | Trello | Asana | Jira | Monday.com | **TaskForce** |
|---------|--------|-------|------|------------|---------------|
| **Gestion de tâches** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Vue Kanban** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Assignation manuelle** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Matching compétences** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Suggestions IA** | ❌ | ⚠️ Limité | ❌ | ⚠️ Limité | ✅ |
| **Heatmap de charge** | ❌ | ⚠️ Timeline | ⚠️ Workload | ✅ | ✅ |
| **Gestion compétences** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Alertes surcharge** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Prix (par user/mois)** | Gratuit-12€ | Gratuit-25€ | Gratuit-15€ | 8-16€ | **Gratuit** |
| **Courbe apprentissage** | Facile | Moyenne | Difficile | Moyenne | **Facile** |

### 3.2 Forces et faiblesses des concurrents

#### Trello
**Forces** : Simplicité, gratuité, adoption massive  
**Faiblesses** : Trop basique, pas de gestion avancée, assignation manuelle uniquement

#### Asana
**Forces** : Complet, vues multiples, intégrations  
**Faiblesses** : Complexe, cher, pas de matching compétences

#### Jira
**Forces** : Puissant pour le développement logiciel, personnalisable  
**Faiblesses** : Très complexe, courbe d'apprentissage longue, UI datée

#### Monday.com
**Forces** : Visuellement attrayant, automatisations  
**Faiblesses** : Cher, pas de focus sur les compétences

### 3.3 Opportunités de marché

✅ **Niche identifiée** : PME et startups agiles cherchant une solution simple mais intelligente  
✅ **Tendance croissante** : IA appliquée à la gestion de projets (+45% de recherches en 2025)  
✅ **Besoin non satisfait** : Outils existants ignorent les compétences réelles des équipes  
✅ **Télétravail** : Besoin accru de visibilité sur la charge et les compétences distribuées

---

## 4. User Personas

### 4.1 Persona 1 : Sophie - Chef de Projet Agile

<table>
<tr>
<td width="30%">
<img src="../assets/images/persona_sophie.jpg" alt="Sophie" width="150" style="border-radius: 50%"/>
</td>
<td>

**Âge** : 34 ans  
**Poste** : Chef de Projet Digital  
**Entreprise** : Agence web (25 personnes)  
**Expérience** : 8 ans en gestion de projets

</td>
</tr>
</table>

**Contexte** :
Sophie gère simultanément 4-6 projets clients avec une équipe de 12 développeurs, designers et rédacteurs. Elle passe 2h/jour à répartir les tâches manuellement sur Trello.

**Frustrations** :
- 😤 "Je ne sais pas toujours qui maîtrise quelle techno dans mon équipe"
- 😤 "Certains devs sont surchargés pendant que d'autres attendent du boulot"
- 😤 "J'aimerais automatiser l'assignation des tâches simples"

**Objectifs** :
- ✅ Gagner du temps sur l'assignation
- ✅ Mieux équilibrer la charge de travail
- ✅ Avoir une vue d'ensemble sur les compétences de l'équipe

**Utilisation de TaskForce** :
- Crée des projets et définit les compétences requises par tâche
- Utilise les suggestions IA pour assigner efficacement
- Surveille la heatmap de charge pour éviter les surcharges

---

### 4.2 Persona 2 : Karim - Développeur Full Stack

<table>
<tr>
<td width="30%">
<img src="../assets/images/persona_karim.jpg" alt="Karim" width="150" style="border-radius: 50%"/>
</td>
<td>

**Âge** : 28 ans  
**Poste** : Développeur Full Stack  
**Entreprise** : Startup SaaS  
**Expérience** : 5 ans (React, Node.js, PostgreSQL)

</td>
</tr>
</table>

**Contexte** :
Karim travaille dans une équipe de 8 développeurs. Il reçoit souvent des tâches qui ne correspondent pas à ses compétences principales, ce qui le ralentit.

**Frustrations** :
- 😤 "On m'assigne des tâches Python alors que je suis meilleur en React"
- 😤 "Je ne sais pas toujours sur quoi je vais travailler demain"
- 😤 "Parfois je suis submergé, parfois j'attends qu'on m'assigne quelque chose"

**Objectifs** :
- ✅ Recevoir des tâches alignées avec ses compétences
- ✅ Avoir une visibilité sur sa charge de travail
- ✅ Déclarer ses compétences et les faire évoluer

**Utilisation de TaskForce** :
- Maintient son profil de compétences à jour
- Consulte son dashboard personnel chaque matin
- Reçoit des notifications pour les nouvelles tâches

---

### 4.3 Persona 3 : Marie - Responsable RH

<table>
<tr>
<td width="30%">
<img src="../assets/images/persona_marie.jpg" alt="Marie" width="150" style="border-radius: 50%"/>
</td>
<td>

**Âge** : 42 ans  
**Poste** : Responsable RH & Formation  
**Entreprise** : ESN (200 personnes)  
**Expérience** : 15 ans en RH

</td>
</tr>
</table>

**Contexte** :
Marie supervise le bien-être et le développement des compétences des collaborateurs. Elle doit identifier les risques de burn-out et planifier les formations.

**Frustrations** :
- 😤 "Je découvre trop tard qu'un collaborateur est en surcharge"
- 😤 "Difficile d'avoir une vue d'ensemble des compétences de l'entreprise"
- 😤 "Les managers ne me remontent pas les signaux faibles"

**Objectifs** :
- ✅ Détecter précocement les surcharges
- ✅ Cartographier les compétences de l'organisation
- ✅ Identifier les besoins en formation

**Utilisation de TaskForce** :
- Consulte les logs d'activité et alertes surcharge
- Visualise les compétences agrégées par équipe
- Exporte les données pour les entretiens annuels

---

### 4.4 Persona 4 : Thomas - Admin Système (secondaire)

<table>
<tr>
<td width="30%">
<img src="../assets/images/persona_thomas.jpg" alt="Thomas" width="150" style="border-radius: 50%"/>
</td>
<td>

**Âge** : 31 ans  
**Poste** : Administrateur Système  
**Entreprise** : PME tech  
**Expérience** : 7 ans en DevOps

</td>
</tr>
</table>

**Contexte** :
Thomas gère l'infrastructure IT et les accès utilisateurs. Il doit activer/désactiver les comptes et surveiller l'usage de la plateforme.

**Objectifs** :
- ✅ Gérer les utilisateurs (activation, désactivation)
- ✅ Surveiller les logs d'activité
- ✅ Garantir la sécurité et la conformité RGPD

**Utilisation de TaskForce** :
- Accès au panel d'administration (v2)
- Gestion des droits et rôles
- Consultation des logs système

---

## 5. Fonctionnalités détaillées

> **📌 Note** : Les 26 User Stories complètes sont documentées dans [06_User_Stories_Backlog.md](06_User_Stories_Backlog.md)

### Résumé des fonctionnalités par Epic

| Epic | US# | Fonctionnalités clés | Priorité |
|------|-----|---------------------|----------|
| **Auth & Profils** | 001-007 | Inscription, connexion, profil, compétences, disponibilité, équipes | 🔴 Critique |
| **Équipes** | 008-009 | Gestion membres, compétences agrégées | 🔴 Critique |
| **Projets** | 010-012 | CRUD projets, vue projets assignés | 🔴 Critique |
| **Tâches** | 013-019 | CRUD tâches, assignation manuelle/intelligente, commentaires, fichiers | 🔴 Critique |
| **Dashboards** | 020-022 | Dashboard personnel, Kanban, heatmap charge | 🔴 Critique |
| **Notifications** | 023-024 | Notifications in-app, gestion lecture | 🔴 Critique |
| **Administration** | 025-026 | Gestion utilisateurs, logs d'activité | 🟡 Haute (v2) |

**Total** : **26 User Stories** réparties sur **7 Epics** et **5 Milestones**

Voir le document [06_User_Stories_Backlog.md](06_User_Stories_Backlog.md) pour le détail complet de chaque US avec critères d'acceptation.

---

## 6. Règles métier

### 6.1 Règles de gestion des compétences

| ID | Règle | Description |
|----|-------|-------------|
| RM-01 | **Compétence obligatoire** | Chaque utilisateur doit déclarer au minimum 3 compétences |
| RM-02 | **Niveau de compétence** | Échelle fixe : 1=Débutant, 2=Intermédiaire, 3=Avancé, 4=Expert, 5=Maître |
| RM-03 | **Catégorisation** | Compétences classées : Langages, Frameworks, Outils, Soft Skills |
| RM-04 | **Mise à jour** | Les utilisateurs peuvent modifier leurs compétences à tout moment |

### 6.2 Règles d'assignation de tâches

| ID | Règle | Description |
|----|-------|-------------|
| RM-05 | **Matching minimum** | Pour être suggéré, un collaborateur doit avoir ≥70% des compétences requises |
| RM-06 | **Disponibilité** | Les collaborateurs en congé ou indisponibles ne peuvent pas être assignés |
| RM-07 | **Charge maximale** | Un collaborateur ne peut pas dépasser 45h de charge/semaine (configurable) |
| RM-08 | **Priorité** | Les tâches "Critiques" sont toujours assignées avant les autres |
| RM-09 | **Auto-assignation** | Un collaborateur peut s'auto-assigner une tâche si elle est "Non assignée" |

### 6.3 Règles de workflow de tâches

| ID | Règle | Description |
|----|-------|-------------|
| RM-10 | **Statuts autorisés** | À faire → En cours → Terminé (workflow linéaire) |
| RM-11 | **Retour arrière** | Retour possible : Terminé → En cours (si erreur détectée) |
| RM-12 | **Tâche bloquée** | Si bloquée >3 jours, notification automatique au manager |
| RM-13 | **Deadline passée** | Tâche en retard = couleur rouge + alerte quotidienne |

### 6.4 Règles de notifications

| ID | Règle | Description |
|----|-------|-------------|
| RM-14 | **Nouvelle tâche** | Notification immédiate à l'assigné |
| RM-15 | **Deadline proche** | Alerte 24h avant l'échéance |
| RM-16 | **Surcharge** | Alerte manager si collaborateur >40h/semaine |
| RM-17 | **Commentaire** | Notification à tous les participants de la tâche |

### 6.5 Règles de sécurité et confidentialité

| ID | Règle | Description |
|----|-------|-------------|
| RM-18 | **RGPD** | Données personnelles exportables et supprimables à la demande |
| RM-19 | **Isolation** | Un utilisateur ne voit que ses projets et équipes |
| RM-20 | **Logs** | Toutes les actions sensibles sont tracées (admin uniquement) |
| RM-21 | **Mot de passe** | Longueur minimale 8 caractères, 1 majuscule, 1 chiffre |

---

## 7. Exigences non fonctionnelles

### 7.1 Performance

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Temps de réponse API** | < 200ms pour 95% des requêtes | 🔴 Critique |
| **Temps de calcul matching** | < 2s pour analyser 50 tâches | 🔴 Critique |
| **Chargement page** | < 1s (First Contentful Paint) | 🟡 Haute |
| **Upload fichier** | < 5s pour un fichier de 5MB | 🟢 Moyenne |

### 7.2 Scalabilité

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Utilisateurs simultanés** | Support de 100 utilisateurs actifs | 🔴 Critique |
| **Tâches par projet** | Support de 1000 tâches par projet | 🟡 Haute |
| **Projets par utilisateur** | Support de 50 projets actifs/utilisateur | 🟢 Moyenne |

### 7.3 Disponibilité et Fiabilité

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Uptime** | 99% (excluant maintenances planifiées) | 🟡 Haute |
| **Maintenance** | Fenêtre de maintenance : dim 2h-6h | 🟢 Moyenne |
| **Sauvegarde BDD** | Backup quotidien automatique | 🔴 Critique |
| **Récupération** | RTO = 4h, RPO = 24h | 🟢 Moyenne |

### 7.4 Sécurité

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Authentification** | JWT avec expiration 24h | 🔴 Critique |
| **Chiffrement** | HTTPS (TLS 1.3) obligatoire | 🔴 Critique |
| **Protection CSRF** | Tokens anti-CSRF sur toutes les mutations | 🔴 Critique |
| **Validation données** | Validation côté serveur systématique | 🔴 Critique |
| **Rate limiting** | Max 100 req/min par IP | 🟡 Haute |

### 7.5 Ergonomie et Accessibilité

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Responsive design** | Support mobile, tablette, desktop | 🔴 Critique |
| **Navigateurs** | Chrome, Firefox, Edge, Safari (2 dernières versions) | 🔴 Critique |
| **Accessibilité** | WCAG 2.1 niveau AA | 🟡 Haute |
| **Internationalisation** | Français uniquement (MVP) | 🟢 Basse |
| **Mode sombre** | Thème clair/sombre disponible | 🟢 Moyenne |

### 7.6 Maintenabilité

| Critère | Exigence | Priorité |
|---------|----------|----------|
| **Couverture tests** | ≥ 70% (unitaires + intégration) | 🔴 Critique |
| **Documentation code** | Commentaires sur fonctions complexes | 🟡 Haute |
| **Conventions** | Respect des conventions Java/TypeScript | 🔴 Critique |
| **Logs applicatifs** | Niveaux : DEBUG, INFO, WARN, ERROR | 🟡 Haute |

---

## 8. Critères d'acceptation globaux

### 8.1 Critères fonctionnels

✅ **Toutes les US critiques (M1-M3) implémentées** : 20/26 minimum  
✅ **Matching compétences opérationnel** avec taux de pertinence ≥ 80%  
✅ **Dashboards fonctionnels** : personnel, Kanban, heatmap  
✅ **Notifications temps réel** via WebSocket ou polling  
✅ **Gestion complète du cycle de vie** d'un projet (création → tâches → suivi → clôture)  

### 8.2 Critères techniques

✅ **API REST documentée** avec Swagger/OpenAPI  
✅ **Base de données PostgreSQL** normalisée (3NF)  
✅ **Authentification JWT** sécurisée  
✅ **Application conteneurisée** avec Docker  
✅ **Tests automatisés** : couverture ≥ 70%  
✅ **Code versionné** sur GitHub avec commits atomiques  

### 8.3 Critères de qualité

✅ **Zéro bug bloquant** en production  
✅ **Performance** : temps de réponse < 200ms (P95)  
✅ **UX fluide** : pas de freeze ou lag perceptible  
✅ **Responsive** : utilisable sur mobile et desktop  
✅ **Accessibilité** : navigation au clavier possible  

### 8.4 Critères documentaires

✅ **Documentation utilisateur** complète avec captures d'écran  
✅ **Documentation technique** : installation, configuration, API  
✅ **Diagrammes UML** : use case, séquence, classes  
✅ **MCD/MLD** validé et cohérent  

---

## 📎 Annexes

### A. Documents liés

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Contexte et enjeux du projet
- [03_CdCT.md](03_CdCT.md) - Spécifications techniques
- [06_User_Stories_Backlog.md](06_User_Stories_Backlog.md) - Backlog complet des 26 US
- [07_Dossier_UI_UX.md](../02_REALISATION_ET_CONCEPTION/07_Dossier_UI_UX.md) - Maquettes et design system

### B. Diagrammes à créer

- `assets/diagrammes/Use_Case_Global.drawio` - Diagramme de cas d'utilisation général
- `assets/diagrammes/User_Journey.drawio` - Parcours utilisateur type
- `assets/charts/Benchmark_Concurrents.xlsx` - Tableau comparatif concurrents

### C. Glossaire

| Terme | Définition |
|-------|------------|
| **Matching** | Algorithme de correspondance entre compétences requises et compétences possédées |
| **Heatmap** | Carte thermique visualisant la charge de travail (vert = dispo, rouge = surchargé) |
| **Epic** | Groupe thématique de User Stories (ex: "Authentification") |
| **User Story (US)** | Fonctionnalité exprimée du point de vue utilisateur |
| **Milestone** | Jalon regroupant plusieurs US pour une release |
| **Backlog** | Liste priorisée des fonctionnalités à développer |

### D. Historique des versions

| Version | Date | Auteur | Modifications |
|---------|------|--------|---------------|
| 1.0 | 04/01/2026 | Michel-Pierre | Création complète du CdCF |

---

**Document validé par** : Michel-Pierre  
**Date de validation** : 04/01/2026  
**Prochaine revue prévue** : 15/01/2026
