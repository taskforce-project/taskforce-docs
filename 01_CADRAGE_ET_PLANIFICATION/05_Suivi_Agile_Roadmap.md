# 🚀 Vision Produit & Roadmap - TaskForce

> **Projet** : TaskForce - Plateforme de gestion de tâches avec assignation intelligente  
> **Version** : 1.0  
> **Date** : 04/01/2026  
> **Auteur** : Michel-Pierre  
> **Statut** : Validé

---

## 🎯 Objectif du document

Ce document présente la **vision produit à long terme** de TaskForce, la **roadmap stratégique** sur 12-18 mois, et le **suivi Agile** avec la planification détaillée des sprints, releases et milestones.

---

## 📋 Table des matières

1. [Vision produit](#1-vision-produit)
2. [Stratégie produit et positionnement](#2-stratégie-produit-et-positionnement)
3. [Roadmap stratégique](#3-roadmap-stratégique)
4. [Planification Agile - Sprints et Milestones](#4-planification-agile---sprints-et-milestones)
5. [Backlog priorisé et User Stories](#5-backlog-priorisé-et-user-stories)
6. [OKRs et métriques de succès](#6-okrs-et-métriques-de-succès)
7. [Gestion du changement et évolution](#7-gestion-du-changement-et-évolution)

---

## 1. Vision produit

### 1.1 Vision statement

> **"TaskForce est la plateforme collaborative qui révolutionne l'assignation des tâches en entreprise en exploitant l'intelligence des compétences pour optimiser la productivité et l'engagement des équipes."**

### 1.2 Mission

Permettre aux **chefs de projet et managers** de :
- ✅ Assigner automatiquement les tâches aux collaborateurs les plus qualifiés
- ✅ Identifier instantanément les gaps de compétences dans leurs équipes
- ✅ Maximiser l'efficacité et la satisfaction des équipes
- ✅ Suivre en temps réel l'avancement des projets avec des métriques claires

### 1.3 Proposition de valeur unique (UVP)

| Cible | Problème actuel | Solution TaskForce | Bénéfice |
|-------|-----------------|-------------------|----------|
| **Chef de projet** | Assignation manuelle chronophage | Matching automatique par compétences | **-70% de temps** sur l'assignation |
| **Collaborateur** | Tâches inadaptées au profil | Recommandations basées sur skills | **+50% d'engagement** |
| **RH/Manager** | Visibilité limitée sur les compétences | Dashboard de compétences temps réel | **Décisions data-driven** |
| **Admin système** | Outils dispersés (Jira/Trello/Asana) | Solution all-in-one | **-30% coûts** outils |

### 1.4 Différenciation compétitive

**vs Trello/Asana/Monday.com** :

| Feature | Trello | Asana | Monday.com | **TaskForce** |
|---------|--------|-------|------------|---------------|
| **Assignation manuelle** | ✅ | ✅ | ✅ | ✅ |
| **Matching par compétences** | ❌ | ❌ | ⚠️ Basique | ✅ **Intelligent** |
| **Suivi des skills** | ❌ | ❌ | ❌ | ✅ **Natif** |
| **Analytics prédictifs** | ❌ | ⚠️ Payant | ⚠️ Premium | 🔜 **v2.0** |
| **Prix** | $5-12/user | $11-25/user | $9-16/user | **$3-10/user** |



---

## 2. Stratégie produit et positionnement

### 2.1 Segmentation marché

#### Marché cible (TAM/SAM/SOM)

```
┌─────────────────────────────────────────────────┐
│ TAM (Total Addressable Market)                  │
│ Toutes les PME/ETI en France                    │
│ ~3,9M entreprises × 20€/mois = 936M€/an         │
└─────────────────────────────────────────────────┘
           │
           ├─→ ┌──────────────────────────────────┐
           │   │ SAM (Serviceable Available Mkt)  │
           │   │ PME 10-250 salariés tech/services│
           │   │ ~150k entreprises × 20€ = 36M€/an│
           │   └──────────────────────────────────┘
           │              │
           └─→ ┌──────────▼───────────────────────┐
               │ SOM (Serviceable Obtainable Mkt) │
               │ 1% du SAM (réaliste an 1-2)      │
               │ ~1500 clients × 20€ = 360k€/an   │
               └──────────────────────────────────┘
```

#### Segments prioritaires

| Segment | Taille | Besoins | Priorité |
|---------|--------|---------|----------|
| **Agences digitales** | 10-50 p. | Projets multiples, skills variés | 🔴 **P0** (MVP) |
| **Startups tech** | 5-30 p. | Agilité, croissance rapide | 🔴 **P0** (MVP) |
| **ESN/Consulting** | 50-250 p. + | Staffing optimisé, multi-projets | 🟡 **P1** (v1.1) |
| **Départements IT** | 20-100 p. +| Gestion projets internes | 🟡 **P1** (v1.1) |
| **Freelance collectives** | 5-20 p. | Collaboration distribuée | 🟢 **P2** (v2.0) |

### 2.2 Go-to-Market (GTM)

#### Phase 1 : MVP (M1-M3) - Validation produit

**Objectif** : 10 early adopters (gratuit) → Feedback qualitatif

| Canal | Action | Coût | KPI |
|-------|--------|------|-----|
| **LinkedIn** | Posts organiques + demo vidéo | 0€ | 500 vues |
| **Product Hunt** | Lancement officiel | 0€ | 50 upvotes |
| **GitHub** | Open source partie frontend | 0€ | 100 stars |
| **Communautés** | DevFest, meetups tech Metz/Nancy | 0€ | 5 signups |

#### Phase 2 : v1.0 (M4-M6) - Acquisition payante

**Objectif** : 50 clients payants → 1000€ MRR

| Canal | Action | Budget | CAC cible |
|-------|--------|--------|-----------|
| **Google Ads** | Mots-clés "task management skills" | 300€/mois | <50€ |
| **LinkedIn Ads** | Ciblage chefs de projet | 200€/mois | <60€ |
| **Content Marketing** | Blog SEO (10 articles) | 0€ (DIY) | 0€ |
| **Affiliation** | Partenariats agences web | 0€ (rev share) | 0€ |

### 2.3 Modèle de revenus

#### Pricing par segment

| Plan | Cible | Prix/mois | Utilisateurs | Features clés | Marge |
|------|-------|-----------|--------------|---------------|-------|
| **Free** | Freelancers, tests | **0€** | 5 | Projets limités (3), support community | - |
| **Starter** | Petites équipes | **15€** | 15 | Projets illimités, matching basique | ~10€ |
| **Pro** | Agences, startups | **49€** | 50 | Analytics, API, matching avancé | ~40€ |
| **Enterprise** | ESN, grands comptes | **199€** | Illimité | SSO, support dédié, SLA 99.9% | ~180€ |

#### Projections revenus (18 mois)

| Mois | Clients Free | Starter | Pro | Enterprise | MRR | ARR |
|------|--------------|---------|-----|------------|-----|-----|
| M3 (MVP) | 10 | 0 | 0 | 0 | 0€ | 0€ |
| M6 (v1.0) | 50 | 20 | 3 | 0 | 447€ | 5,4k€ |
| M12 (v1.1) | 150 | 60 | 15 | 2 | 1633€ | 19,6k€ |
| M18 (v2.0) | 300 | 120 | 35 | 5 | 3610€ | 43,3k€ |

**🎯 Objectif M18** : **3,6k€ MRR** (~43k€ ARR) avec **160 clients payants**.

---

## 3. Roadmap stratégique

### 3.1 Vue d'ensemble (18 mois)

```
2026                           2027
├─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┤
│ JAN │ FEB │ MAR │ APR │ MAY │ JUN │ JUL │ AUG │ SEP │ OCT │ NOV │ DEC │ ...
├─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┤
│                                                                          │
│  🏗️ MVP (v0.9)        🚀 v1.0         📊 v1.1           🤖 v2.0        │
│  M1-M3                M4-M6            M7-M12            M13-M18         │
│                                                                          │
│  • Auth               • Dashboard     • Analytics       • IA prédictive │
│  • CRUD Tasks         • Notifs temps  • Intégrations   • Mobile app     │
│  • Matching basique     réel         • API publique    • Webhooks       │
│                       • Multi-langues • SSO/SAML       • Marketplace    │
└──────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Releases détaillées

#### 🏗️ MVP (v0.9) - Q1 2026 (Jan-Mar)

**Objectif** : Validation du concept avec early adopters

| Feature | Description | Priorité | Sprint |
|---------|-------------|----------|--------|
| **Authentification JWT** | Login/Register/Logout | 🔴 MUST | S0 |
| **Gestion utilisateurs** | Profil, compétences, avatar | 🔴 MUST | S1 |
| **Gestion équipes** | CRUD teams, ajout membres | 🔴 MUST | S1 |
| **Gestion projets** | CRUD projets, statuts | 🔴 MUST | S2 |
| **Gestion tâches** | CRUD tâches, Kanban | 🔴 MUST | S3 |
| **Assignation manuelle** | Assigner membre à tâche | 🔴 MUST | S4 |
| **Matching compétences (v1)** | Algorithme de scoring simple | 🔴 MUST | S4 |
| **Suivi du temps** | Tracking temps passé par tâche | 🟡 SHOULD | S5 |
| **Commentaires** | Commentaires sur tâches | 🟡 SHOULD | S5 |

**📅 Livraison** : 14/03/2026  
**🎯 Objectif** : 10 utilisateurs beta testeurs

---

#### 🚀 v1.0 - Q2 2026 (Apr-Jun)

**Objectif** : First public release avec monétisation

| Feature | Description | Priorité | Impact business |
|---------|-------------|----------|-----------------|
| **Dashboard avancé** | Métriques temps réel (tâches, charge, compétences) | 🔴 MUST | ⭐⭐⭐ |
| **Notifications temps réel** | WebSockets pour notifs instantanées | 🔴 MUST | ⭐⭐⭐ |
| **Matching v2** | Algorithme pondéré (compétences + dispo + historique) | 🔴 MUST | ⭐⭐⭐ |
| **Multi-langues (i18n)** | FR + EN | 🟡 SHOULD | ⭐⭐ |
| **Export PDF/Excel** | Export rapports projets/tâches | 🟡 SHOULD | ⭐⭐ |
| **Dark mode** | Thème sombre | 🟢 COULD | ⭐ |
| **Onboarding guidé** | Tour guidé nouveaux users | 🔴 MUST | ⭐⭐⭐ |

**📅 Livraison** : 30/06/2026  
**🎯 Objectif** : 50 clients payants, 1k€ MRR

---

#### 📊 v1.1 - Q3-Q4 2026 (Jul-Dec)

**Objectif** : Enterprise-ready features

| Feature | Description | Priorité | Plan cible |
|---------|-------------|----------|------------|
| **Analytics avancés** | Rapports custom, graphiques interactifs | 🔴 MUST | Pro+ |
| **API publique REST** | Webhooks, intégrations tierces | 🔴 MUST | Pro+ |
| **SSO/SAML** | Single Sign-On entreprise | 🔴 MUST | Enterprise |
| **Rôles personnalisés** | Création de rôles custom (au-delà de USER/MANAGER/ADMIN) | 🟡 SHOULD | Pro+ |
| **Intégrations** | Slack, Microsoft Teams, Google Calendar | 🟡 SHOULD | Pro+ |
| **Audit logs** | Logs détaillés toutes actions | 🟡 SHOULD | Enterprise |
| **Timesheet automatique** | Génération timesheet depuis temps trackés | 🟢 COULD | Pro+ |

**📅 Livraison** : 31/12/2026  
**🎯 Objectif** : 100 clients payants, 2k€ MRR

---

#### 🤖 v2.0 - Q1-Q2 2027 (Jan-Jun)

**Objectif** : IA et prédiction

| Feature | Description | Priorité | Impact |
|---------|-------------|----------|--------|
| **Prédiction de charge** | ML pour anticiper surcharge/sous-charge | 🔴 MUST | ⭐⭐⭐ |
| **Recommandations IA** | Suggestions de tâches basées sur l'historique | 🔴 MUST | ⭐⭐⭐ |
| **Détection des risques** | Alerte automatique projets en retard | 🟡 SHOULD | ⭐⭐ |
| **Mobile app (iOS/Android)** | Application native (React Native) | 🟡 SHOULD | ⭐⭐⭐ |
| **Mode offline** | Sync automatique quand reconnecté | 🟢 COULD | ⭐⭐ |
| **Marketplace plugins** | Extensions tierces | 🟢 COULD | ⭐ |
| **Gamification** | Badges, leaderboard, points | 🟢 COULD | ⭐ |

**📅 Livraison** : 30/06/2027  
**🎯 Objectif** : 200 clients payants, 4k€ MRR

---

## 4. Planification Agile - Sprints et Milestones

### 4.1 Méthodologie Scrum adaptée (solo dev)

| Pratique Scrum | Adaptation solo | Fréquence |
|----------------|-----------------|-----------|
| **Sprint Planning** | Planning écrit (GitHub Projects) | Lundi 9h (1h) |
| **Daily Standup** | Journal de bord (Notion/Markdown) | Chaque matin (5min) |
| **Sprint Review** | Auto-démo + screenshots | Vendredi 17h (30min) |
| **Sprint Retrospective** | Bilan écrit (Keep/Stop/Start) | Vendredi 17h30 (30min) |
| **Backlog Refinement** | Mise à jour US (estimation) | Mercredi 16h (30min) |

### 4.2 Définition of Done (DoD)

Une User Story est **Done** si :
- ✅ Code développé et fonctionnel
- ✅ Tests unitaires écrits (couverture >80%)
- ✅ Tests d'intégration passés (si applicable)
- ✅ Code reviewé (auto-review après 2 jours)
- ✅ Documentation API mise à jour (Swagger)
- ✅ Merge dans `develop` sans conflit
- ✅ Déployé sur environnement de staging
- ✅ Testé manuellement (parcours utilisateur)

### 4.3 Milestones et Sprints (MVP)

#### Milestone 1 : Authentification (M1)

**Durée** : 1 semaine (Sprint 0)  
**Dates** : 06/01 - 10/01/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S0** | US-001, US-002, US-003 | Auth JWT fonctionnelle | Login, Register, Logout + JWT |

**Demo** : User peut se connecter et voir son profil.

---

#### Milestone 2 : Gestion Utilisateurs & Équipes (M2)

**Durée** : 1 semaine (Sprint 1)  
**Dates** : 13/01 - 17/01/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S1** | US-004, US-011, US-012 | Profils + Teams CRUD | Gestion compétences, CRUD teams |

**Demo** : User peut ajouter des compétences et créer une équipe.

---

#### Milestone 3 : Gestion Projets & Tâches (M3)

**Durée** : 2 semaines (Sprint 2-3)  
**Dates** : 20/01 - 31/01/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S2** | US-013, US-014 | Projets CRUD | Création et gestion projets |
| **S3** | US-015, US-016, US-017 | Tâches CRUD + Statuts | Kanban fonctionnel |

**Demo** : Manager peut créer un projet avec 5 tâches et les déplacer en Kanban.

---

#### Milestone 4 : Assignation Intelligente (M4)

**Durée** : 1 semaine (Sprint 4)  
**Dates** : 03/02 - 07/02/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S4** | US-018, US-019, US-020 | Matching compétences v1 | Algorithme de scoring + assignation |

**Demo** : Système recommande les 3 meilleurs candidats pour une tâche.

---

#### Milestone 5 : Features Avancées (M5)

**Durée** : 3 semaines (Sprint 5-7)  
**Dates** : 10/02 - 28/02/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S5** | US-021, US-022, US-024 | Suivi temps + Commentaires | Time tracking + comments thread |
| **S6** | US-023, US-025 | Dashboard + Rapports | Métriques temps réel |
| **S7** | US-026 | Notifications | Système de notifications |

**Demo** : Dashboard affiche la charge de l'équipe en temps réel.

---

#### Milestone 6 : Stabilisation & Déploiement

**Durée** : 2 semaines (Sprint 8-9)  
**Dates** : 03/03 - 14/03/2026

| Sprint | US incluses | Objectif | Livrables |
|--------|-------------|----------|-----------|
| **S8** | - | Tests E2E, Corrections bugs | Suite de tests Playwright |
| **S9** | - | Déploiement prod + Doc | App en ligne, README, User Docs |

**Demo** : Application accessible publiquement sur taskforce.app (ou similaire).

---

### 4.4 Vélocité et capacité

#### Estimation des US (Planning Poker)

**Échelle Fibonacci** : 1, 2, 3, 5, 8, 13, 21

| Points | Complexité | Durée estimée | Exemple |
|--------|------------|---------------|---------|
| **1** | Triviale | 1-2h | Modifier un label |
| **2** | Simple | 2-4h | CRUD basique |
| **3** | Moyenne | 4-8h | Formulaire avec validation |
| **5** | Complexe | 1-2 jours | Relation many-to-many |
| **8** | Très complexe | 2-3 jours | Algorithme de matching |
| **13** | Épique | 3-5 jours | Dashboard complet |

#### Capacité par sprint

```
1 sprint = 1 semaine = 5 jours ouvrés
1 jour = 8h (théorique) - 20% (meetings, pauses) = 6h effectives

Capacité sprint = 5 jours × 6h = 30h effectives
Vélocité cible = 20-25 points/sprint (solo dev)
```

#### Backlog estimé (MVP)

| Epic | US | Points | Total |
|------|-----|--------|-------|
| **Authentification** | 3 | 2+3+2 | 7 pts |
| **Utilisateurs** | 2 | 3+5 | 8 pts |
| **Équipes** | 2 | 3+3 | 6 pts |
| **Projets** | 2 | 3+3 | 6 pts |
| **Tâches** | 5 | 3+3+2+5+3 | 16 pts |
| **Assignation** | 3 | 5+8+3 | 16 pts |
| **Dashboard** | 2 | 13+5 | 18 pts |
| **Notifications** | 1 | 8 | 8 pts |
| **Total MVP** | **20 US** | | **85 pts** |

**Durée estimée** : 85 pts ÷ 25 pts/sprint = **3,4 sprints** → **4 sprints** (avec marge)

---

## 5. Backlog priorisé et User Stories

### 5.1 Priorisation MoSCoW

| Catégorie | Définition | US incluses | Livraison |
|-----------|------------|-------------|-----------|
| **MUST have** | Critiques pour le MVP | US-001 à US-020 (20 US) | Sprint 0-4 |
| **SHOULD have** | Importantes mais non bloquantes | US-021 à US-024 (4 US) | Sprint 5-6 |
| **COULD have** | Améliorations souhaitables | US-025, US-026 (2 US) | Sprint 7 |
| **WON'T have** | Reportées en v1.1+ | Analytics IA, Mobile, SSO | v1.1-v2.0 |

### 5.2 Backlog ordonné (Top 26 US)

> **📌 Note** : Détail complet dans document suivant

| Rang | ID | Titre | Epic | Points | Priorité | Sprint |
|------|----|-------|------|--------|----------|--------|
| 1 | US-001 | Inscription utilisateur | Auth | 2 | 🔴 MUST | S0 |
| 2 | US-002 | Connexion utilisateur | Auth | 3 | 🔴 MUST | S0 |
| 3 | US-003 | Déconnexion | Auth | 2 | 🔴 MUST | S0 |
| 4 | US-004 | Gestion profil | Utilisateurs | 3 | 🔴 MUST | S1 |
| 5 | US-005 | Ajout compétences | Utilisateurs | 5 | 🔴 MUST | S1 |
| 6 | US-011 | Création équipe | Équipes | 3 | 🔴 MUST | S1 |
| 7 | US-012 | Ajout membres équipe | Équipes | 3 | 🔴 MUST | S1 |
| 8 | US-013 | Création projet | Projets | 3 | 🔴 MUST | S2 |
| 9 | US-014 | Gestion projet | Projets | 3 | 🔴 MUST | S2 |
| 10 | US-015 | Création tâche | Tâches | 3 | 🔴 MUST | S3 |
| 11 | US-016 | Modification tâche | Tâches | 3 | 🔴 MUST | S3 |
| 12 | US-017 | Changement statut | Tâches | 2 | 🔴 MUST | S3 |
| 13 | US-018 | Assignation manuelle | Tâches | 5 | 🔴 MUST | S4 |
| 14 | US-019 | Matching compétences | Tâches | 8 | 🔴 MUST | S4 |
| 15 | US-020 | Voir tâches assignées | Tâches | 3 | 🔴 MUST | S4 |
| 16 | US-021 | Suivi du temps | Tâches | 5 | 🟡 SHOULD | S5 |
| 17 | US-022 | Commentaires tâches | Tâches | 3 | 🟡 SHOULD | S5 |
| 18 | US-024 | Pièces jointes | Tâches | 5 | 🟡 SHOULD | S5 |
| 19 | US-023 | Dashboard manager | Dashboard | 13 | 🟡 SHOULD | S6 |
| 20 | US-025 | Rapports projets | Dashboard | 5 | 🟢 COULD | S6 |
| 21 | US-026 | Notifications temps réel | Notifications | 8 | 🟢 COULD | S7 |

**Total** : 85 points story

---

## 6. OKRs et métriques de succès

### 6.1 OKRs par phase

#### OKR 1 : MVP (Q1 2026)

**Objective** : Valider le product-market fit avec early adopters

| Key Result | Métrique | Cible | Statut |
|------------|----------|-------|--------|
| **KR1** | Utilisateurs beta testeurs actifs | 10 | 🔲 |
| **KR2** | Taux de rétention semaine 1 | >70% | 🔲 |
| **KR3** | NPS (Net Promoter Score) | >40 | 🔲 |
| **KR4** | Features MVP complètes | 100% (20 US) | 🔲 |

---

#### OKR 2 : v1.0 Public Launch (Q2 2026)

**Objective** : Atteindre 50 clients payants et 1k€ MRR

| Key Result | Métrique | Cible | Statut |
|------------|----------|-------|--------|
| **KR1** | Clients payants (Starter+Pro) | 50 | 🔲 |
| **KR2** | MRR (Monthly Recurring Revenue) | 1000€ | 🔲 |
| **KR3** | Taux de conversion Free→Paid | >15% | 🔲 |
| **KR4** | Uptime (disponibilité) | >99% | 🔲 |

---

#### OKR 3 : v1.1 Enterprise (Q3-Q4 2026)

**Objective** : Devenir Enterprise-ready et doubler le MRR

| Key Result | Métrique | Cible | Statut |
|------------|----------|-------|--------|
| **KR1** | Clients Enterprise | 3 | 🔲 |
| **KR2** | MRR | 2000€ | 🔲 |
| **KR3** | Intégrations actives (Slack, Teams) | 2 | 🔲 |
| **KR4** | API publique utilisée | >10 clients | 🔲 |

---

### 6.2 Métriques produit (Product Analytics)

#### Métriques d'activation

| Métrique | Définition | Cible | Outil |
|----------|------------|-------|-------|
| **Time to Value** | Temps avant 1ère tâche assignée | <10 min | Mixpanel |
| **Activation rate** | % users ayant créé ≥1 projet | >80% | Google Analytics |
| **Onboarding completion** | % users finissant le tour guidé | >60% | Heap |

#### Métriques d'engagement

| Métrique | Définition | Cible | Outil |
|----------|------------|-------|-------|
| **DAU/MAU** | Daily/Monthly Active Users | >30% | Mixpanel |
| **Session duration** | Durée moyenne session | >8 min | GA4 |
| **Tasks created/week** | Tâches créées par semaine | >50/team | Interne |
| **Matching usage** | % tâches assignées via matching | >40% | Interne |

#### Métriques de rétention

| Métrique | Définition | Cible | Outil |
|----------|------------|-------|-------|
| **Retention D7** | % users actifs après 7 jours | >50% | Mixpanel |
| **Retention D30** | % users actifs après 30 jours | >30% | Mixpanel |
| **Churn rate** | % clients annulant abonnement | <5%/mois | Stripe |

#### Métriques revenue

| Métrique | Définition | Cible | Outil |
|----------|------------|-------|-------|
| **MRR** | Monthly Recurring Revenue | 1k€ (M6) | Stripe |
| **ARPU** | Average Revenue Per User | 20€ | Stripe |
| **LTV** | Lifetime Value (client moyen) | 240€ (1 an) | Calculé |
| **CAC** | Customer Acquisition Cost | <50€ | Google Ads |
| **LTV/CAC ratio** | Ratio rentabilité | >3 | Calculé |

---

## 7. Gestion du changement et évolution

### 7.1 Processus de gestion du backlog

#### Ajout d'une nouvelle US

```
1. Demande (user feedback, bug, feature request)
   ↓
2. Création issue GitHub (template US)
   ↓
3. Estimation points (Planning Poker solo)
   ↓
4. Priorisation MoSCoW
   ↓
5. Ajout au backlog (position selon priorité)
   ↓
6. Sprint Planning : Si prioritaire → Sprint N+1
```

#### Template User Story

```markdown
## [US-XXX] Titre court (max 10 mots)

**En tant que** [ROLE],  
**Je veux** [ACTION],  
**Afin de** [BÉNÉFICE].

### Critères d'acceptation
- [ ] CA1 : Description précise
- [ ] CA2 : ...
- [ ] CA3 : ...

### Définition of Done
- [ ] Code développé
- [ ] Tests unitaires (>80%)
- [ ] Code reviewé
- [ ] Documentation API
- [ ] Déployé en staging

### Estimation
- Points : **[X]**
- Sprint : **[SX]**

### Dépendances
- Bloqué par : US-YYY
- Bloque : US-ZZZ
```

### 7.2 Gestion des bugs

#### Sévérité des bugs

| Sévérité | Définition | SLA Fix | Exemple |
|----------|------------|---------|---------|
| **P0 - Critical** | App inutilisable | <4h | Crash au login |
| **P1 - High** | Feature majeure cassée | <24h | Matching ne fonctionne pas |
| **P2 - Medium** | Feature mineure cassée | <1 semaine | Filtre de recherche bugué |
| **P3 - Low** | UI/UX mineur | <2 semaines | Typo dans label |

#### Process de résolution

```
Bug report (GitHub Issue)
   ↓
Triage (étiquette P0/P1/P2/P3)
   ↓
Si P0/P1 → Interruption sprint en cours
Si P2/P3 → Ajout backlog sprint suivant
   ↓
Fix + Tests
   ↓
Hotfix en prod (si P0/P1) ou Release normale
```

### 7.3 Rituel de revue roadmap

| Fréquence | Participants | Objectif | Durée |
|-----------|--------------|----------|-------|
| **Mensuelle** | Solo dev + mentor (optionnel) | Ajustement priorités | 1h |
| **Trimestrielle** | + Beta users (interviews) | Validation direction produit | 2h |

**Questions clés** :
- ✅ Les OKRs sont-ils en bonne voie ?
- ✅ Y a-t-il des nouvelles opportunités marché ?
- ✅ Faut-il dé-prioriser certaines features ?
- ✅ Les retours users nécessitent-ils un pivot ?

### 7.4 Stratégie de feature flags

Pour déployer progressivement les features :

```typescript
// Exemple : Feature flag pour matching v2
if (featureFlags.matchingV2Enabled) {
  return advancedMatching(task, users);
} else {
  return basicMatching(task, users);
}
```

**Usage** :
- Rollout progressif (10% users → 50% → 100%)
- A/B testing (comparer matching v1 vs v2)
- Kill switch (désactiver rapidement si bug)

---

## 📎 Annexes

### A. Documents liés

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Contexte général
- [02_CdCF.md](02_CdCF.md) - Spécifications fonctionnelles
- [03_CdCT.md](03_CdCT.md) - Spécifications techniques
- [04_Etude_Faisabilite.md](04_Etude_Faisabilite.md) - Faisabilité et WBS/PERT
- [GitHub Projects](https://github.com/users/[USERNAME]/projects) - Suivi temps réel

### B. Templates et outils

| Document | Lien |
|----------|------|
| **Template User Story** | `.github/ISSUE_TEMPLATE/user-story.md` |
| **Template Bug Report** | `.github/ISSUE_TEMPLATE/bug.md` |
| **Sprint Planning Template** | `templates/Sprint_Planning.md` |
| **Sprint Retrospective** | `templates/Sprint_Retro.md` |

### C. Roadmap visuelle

> **📌 Note** : Roadmap visuelle dans `assets/roadmap/Roadmap_18_Mois.png` (à créer)

**Outils recommandés** :
- **ProductPlan** (gratuit pour 1 roadmap)
- **Miro** (template roadmap)
- **Notion Timeline** (gratuit)

### D. Historique des versions

| Version | Date | Auteur | Modifications |
|---------|------|--------|---------------|
| 1.0 | 04/01/2026 | Michel-Pierre | Création complète Vision & Roadmap |

---

**Document validé par** : Michel-Pierre  
**Date de validation** : 04/01/2026  
**Prochaine revue roadmap** : 01/02/2026

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
