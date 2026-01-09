# 📊 Étude de Faisabilité - TaskForce

> **Projet** : TaskForce - Plateforme de gestion de tâches avec assignation intelligente  
> **Version** : 1.0  
> **Date** : 04/01/2026  
> **Auteur** : Michel-Pierre  
> **Statut** : ✅ Validé

---

## 🎯 Objectif du document

Cette étude de faisabilité analyse la **viabilité technique, économique et organisationnelle** du projet TaskForce. Elle évalue les risques, les ressources nécessaires et la probabilité de succès du projet avant son lancement.

---

## 📋 Table des matières

1. [Synthèse exécutive](#1-synthèse-exécutive)
2. [Faisabilité technique](#2-faisabilité-technique)
3. [Faisabilité économique](#3-faisabilité-économique)
4. [Faisabilité organisationnelle](#4-faisabilité-organisationnelle)
5. [WBS - Work Breakdown Structure](#5-wbs---work-breakdown-structure)
6. [Planification PERT](#6-planification-pert)
7. [Analyse des risques et mitigation](#7-analyse-des-risques-et-mitigation)
8. [Conclusion et recommandations](#8-conclusion-et-recommandations)

---

## 1. Synthèse exécutive

### 1.1 Contexte

TaskForce est un projet pédagogique développé dans le cadre de la formation Concepteur Développeur d'Applications (Bac+3/4) à Metz Numeric School. L'objectif est de créer une plateforme SaaS de gestion de tâches avec assignation intelligente basée sur les compétences.

### 1.2 Résultat global de l'analyse

| Critère | Évaluation | Niveau de risque |
|---------|------------|------------------|
| **Faisabilité technique** | ✅ **Viable** | 🟢 Faible |
| **Faisabilité économique** | ✅ **Rentable** (contexte péda) | 🟢 Faible |
| **Faisabilité organisationnelle** | ⚠️ **Acceptable** (solo dev) | 🟡 Moyen |
| **Faisabilité temporelle** | ✅ **Réalisable en 3 mois** | 🟡 Moyen |

**🎯 Verdict** : **Projet FAISABLE** avec un niveau de risque **maîtrisable**.  
**📌 Recommandation** : Lancement du projet avec priorisation stricte (MVP-first) et suivi Agile rigoureux.

---

## 2. Faisabilité technique

### 2.1 Stack technologique

#### Technologies choisies

| Composant | Technologie | Niveau de maîtrise requis | Disponibilité |
|-----------|-------------|---------------------------|---------------|
| **Backend** | Java 17 + Spring Boot 3.2 | Intermédiaire | ✅ Open Source |
| **Frontend** | Nuxt 3 + TypeScript + Tailwind | Intermédiaire | ✅ Open Source |
| **Base de données** | PostgreSQL 16 | Basique | ✅ Open Source |
| **Conteneurisation** | Docker + Docker Compose | Basique | ✅ Open Source |
| **Versioning** | Git + GitHub | Maîtrisé | ✅ Gratuit |
| **CI/CD** | GitHub Actions | Basique | ✅ Gratuit |
| **Hébergement** | Render.com / Railway | Basique | ✅ Free tier |

#### Analyse de maturité des technologies

```
┌─────────────────────────────────────────┐
│ Spring Boot 3.2      [████████░] 90%   │ Mature, LTS
│ Nuxt 3               [███████░░] 85%   │ Stable, production-ready
│ PostgreSQL 16        [█████████] 99%   │ Très mature
│ Docker               [█████████] 99%   │ Standard industrie
│ GitHub Actions       [████████░] 88%   │ Mature, largement adopté
└─────────────────────────────────────────┘
```

**✅ Conclusion** : Stack moderne, mature et bien documentée. Pas de risque technologique majeur.

### 2.2 Complexité fonctionnelle

| Feature | Complexité | Technologies nécessaires | Risque |
|---------|------------|--------------------------|--------|
| **Auth JWT** | 🟢 Faible | Spring Security | 🟢 |
| **CRUD Teams/Projects** | 🟢 Faible | JPA, REST API | 🟢 |
| **Assignation manuelle** | 🟢 Faible | Relations BDD | 🟢 |
| **Gestion des compétences** | 🟡 Moyen | Modélisation many-to-many | 🟡 |
| **Matching intelligent** | 🟡 Moyen | Algorithme de scoring | 🟡 |
| **Dashboard temps réel** | 🟡 Moyen | Agrégation SQL complexe | 🟡 |
| **Notifications push** | 🔴 Élevé | WebSockets / SSE | 🔴 |
| **Analytics IA** | 🔴 Très élevé | ML/IA (non prévu MVP) | ⛔ |

**📊 Répartition** :
- **70% des features** : Complexité faible → Réalisable rapidement
- **25% des features** : Complexité moyenne → Requiert recherche/apprentissage
- **5% des features** : Complexité élevée → Repoussé en post-MVP

**✅ Conclusion** : MVP techniquement réalisable avec la stack choisie.

### 2.3 Environnement de développement

| Outil | Usage | Coût | Disponibilité |
|-------|-------|------|---------------|
| **IntelliJ IDEA** | IDE Java | Gratuit (Community) ou 0€ (étudiant) | ✅ |
| **VS Code** | IDE Frontend | Gratuit | ✅ |
| **DBeaver** | Client PostgreSQL | Gratuit | ✅ |
| **Postman** | Tests API | Gratuit | ✅ |
| **Draw.io** | Diagrammes | Gratuit | ✅ |
| **Git** | Versioning | Gratuit | ✅ |

**✅ Conclusion** : Tous les outils nécessaires sont disponibles gratuitement.

### 2.4 Dépendances critiques

#### Backend (Spring Boot)
```xml
<!-- Dépendances critiques (TOUTES open source et stables) -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
</dependency>
```

**🟢 Statut** : Aucune dépendance propriétaire, tout est open source et LTS.

#### Frontend (Nuxt 3)
```json
{
  "dependencies": {
    "nuxt": "^3.14.0",
    "vue": "^3.4.0",
    "@nuxt/ui": "^2.19.0",
    "pinia": "^2.2.0"
  }
}
```

**🟢 Statut** : Écosystème Vue.js mature et activement maintenu.

### 2.5 Scalabilité et performance

| Métrique | Cible MVP | Limite estimée (sans optimisation) | Verdict |
|----------|-----------|-------------------------------------|---------|
| **Utilisateurs concurrents** | < 100 | ~500 | ✅ Largement suffisant |
| **Tâches en BDD** | < 10 000 | ~1 million (avec indexes) | ✅ |
| **Temps de réponse API** | < 200ms | ~150ms (moyenne) | ✅ |
| **Uptime** | > 95% | 99% (Render.com) | ✅ |

**✅ Conclusion** : Performances largement suffisantes pour le MVP et la croissance initiale.

---

## 3. Faisabilité économique

### 3.1 Budget prévisionnel

#### Contexte pédagogique (MVP)

| Poste | Détail | Coût mensuel | Coût 3 mois | Coût réel |
|-------|--------|--------------|-------------|-----------|
| **Hébergement** | Render Free Tier (Backend + BDD) | 0€ | 0€ | ✅ 0€ |
| **Frontend** | Vercel Free Tier | 0€ | 0€ | ✅ 0€ |
| **Domaine** | .fr ou .com (optionnel) | - | ~10€ | ⚠️ 10€ |
| **Outils** | GitHub, VS Code, IntelliJ (étudiant) | 0€ | 0€ | ✅ 0€ |
| **Certificat SSL** | Let's Encrypt (automatique) | 0€ | 0€ | ✅ 0€ |
| **Monitoring** | Sentry Free Tier (optionnel) | 0€ | 0€ | ✅ 0€ |
| **Total MVP** | | **0€/mois** | **~10€** | **✅ 10€** |

#### Projection SaaS commercial (post-formation)

| Poste | Détail | Coût mensuel | Coût annuel |
|-------|--------|--------------|-------------|
| **Hébergement** | Railway Pro (1GB RAM, 5GB DB) | 20€ | 240€ |
| **Domaine** | .com renouvelé | 1€ | 12€ |
| **Email transactionnel** | SendGrid Essentials (40k/mois) | 15€ | 180€ |
| **Monitoring** | Sentry Team | 25€ | 300€ |
| **Backups** | Stockage externe | 5€ | 60€ |
| **Total Production** | | **66€/mois** | **~800€/an** |

### 3.2 Modèle économique SaaS (projection)

#### Pricing (exemple)

| Plan | Prix/mois | Utilisateurs | Projets | Support | Marge estimée |
|------|-----------|--------------|---------|---------|---------------|
| **Free** | 0€ | 5 | 3 | Community | - |
| **Starter** | 15€ | 15 | 10 | Email | ~10€ |
| **Pro** | 49€ | 50 | Illimité | Prioritaire | ~40€ |
| **Enterprise** | 199€ | Illimité | Illimité | Dédié | ~180€ |

#### ROI prévisionnel (1 an après lancement)

```
Scénario conservateur :
- 10 clients Starter (15€) = 150€/mois
- 5 clients Pro (49€) = 245€/mois
- 1 client Enterprise (199€) = 199€/mois

Revenus mensuels : 594€
Coûts mensuels : 66€
Bénéfice net : 528€/mois (~6 300€/an)

ROI = (6 300€ - 800€) / 800€ = 687% 🚀
```

**✅ Conclusion** : Modèle économique viable même avec une adoption modeste.

### 3.3 Coût de développement (valorisation pédagogique)

Si le projet était facturé à un client :

| Phase | Jours-homme | Taux journalier | Coût estimé |
|-------|-------------|-----------------|-------------|
| **Cadrage + Conception** | 10 jours | 400€ | 4 000€ |
| **Développement Backend** | 25 jours | 500€ | 12 500€ |
| **Développement Frontend** | 25 jours | 500€ | 12 500€ |
| **Tests + Intégration** | 10 jours | 400€ | 4 000€ |
| **Déploiement + Doc** | 5 jours | 400€ | 2 000€ |
| **Total valorisé** | **75 jours** | | **35 000€** |

**💡 Contexte pédagogique** : Ce coût est fictif, mais valorise l'expérience acquise.

---

## 4. Faisabilité organisationnelle

### 4.1 Ressources humaines

#### Équipe projet

| Rôle | Personne | Disponibilité | Niveau |
|------|----------|---------------|--------|
| **Product Owner** | Michel-Pierre | 100% | Confirmé |
| **Développeur Backend** | Michel-Pierre | 100% | Intermédiaire |
| **Développeur Frontend** | Michel-Pierre | 100% | Intermédiaire |
| **DevOps** | Michel-Pierre | 100% | Débutant |
| **Testeur** | Michel-Pierre | 100% | Débutant |

**⚠️ Risque** : **Solo dev** = pas de revue de code, risque de burnout, manque de perspectives externes.

**✅ Mitigation** :
- Utilisation de **GitHub Copilot** pour assistance code
- Revue de code différée (relecture après 2-3 jours)
- Pair programming avec **ChatGPT/Claude** sur problèmes complexes
- Limiter à **40h/semaine** pour éviter le burnout

### 4.2 Méthodologie Agile Solo

#### Adaptation Scrum pour solo dev

| Pratique Scrum | Adaptation solo |
|----------------|-----------------|
| **Daily Standup** | Journal de bord quotidien (5min) |
| **Sprint Planning** | Planning solo (1h tous les lundis) |
| **Sprint Review** | Auto-démo + screenshot/vidéo |
| **Sprint Retrospective** | Bilan écrit des points positifs/négatifs |
| **Backlog Refinement** | Mise à jour GitHub Projects (30min/semaine) |

#### Planning des sprints (10 sprints de 1 semaine)

| Sprint | Dates | Objectif | US incluses |
|--------|-------|----------|-------------|
| **S0** | 06-10/01 | Setup projet + Auth | US-001, US-002, US-003 |
| **S1** | 13-17/01 | Profils + Teams | US-004, US-011, US-012 |
| **S2** | 20-24/01 | Projets | US-013, US-014 |
| **S3** | 27-31/01 | Tâches CRUD | US-015, US-016, US-017 |
| **S4** | 03-07/02 | Assignation + Matching | US-018, US-019, US-020 |
| **S5** | 10-14/02 | Suivi temps + Commentaires | US-021, US-022, US-024 |
| **S6** | 17-21/02 | Dashboard + Stats | US-023, US-025 |
| **S7** | 24-28/02 | Notifications | US-026 |
| **S8** | 03-07/03 | Tests E2E + Bugs | - |
| **S9** | 10-14/03 | Déploiement + Doc finale | - |

**✅ Conclusion** : Méthodologie adaptée au contexte solo avec suivi rigoureux.

### 4.3 Gestion du temps

#### Disponibilité hebdomadaire

```
Lundi - Vendredi : 8h/jour (9h-12h + 13h-18h)
Week-end : Pas de dev (repos et récupération)

Total : 40h/semaine × 10 semaines = 400h
Marge de sécurité (-20%) : ~320h effectives
```

#### Répartition du temps par activité

| Activité | % du temps | Heures (10 semaines) |
|----------|------------|----------------------|
| **Développement** | 60% | 192h |
| **Tests** | 15% | 48h |
| **Documentation** | 10% | 32h |
| **Debugging** | 10% | 32h |
| **Meetings/Admin** | 5% | 16h |

**✅ Conclusion** : 320h suffisantes pour MVP avec 26 US (moyenne 12h/US).

---

## 5. WBS - Work Breakdown Structure

### 5.1 Décomposition du projet

```
TaskForce (Niveau 0)
│
├── 1. Cadrage et Planification (Niveau 1)
│   ├── 1.1 Dossier de projet
│   ├── 1.2 Cahier des charges fonctionnel
│   ├── 1.3 Cahier des charges technique
│   ├── 1.4 Étude de faisabilité
│   └── 1.5 Vision produit et roadmap
│
├── 2. Conception (Niveau 1)
│   ├── 2.1 Modélisation BDD (MCD/MLD)
│   ├── 2.2 Maquettage UI/UX (Figma)
│   ├── 2.3 Architecture technique (diagrammes)
│   └── 2.4 Spécifications API (Swagger)
│
├── 3. Développement Backend (Niveau 1)
│   ├── 3.1 Setup projet Spring Boot
│   ├── 3.2 Authentification JWT
│   │   ├── 3.2.1 Entités User
│   │   ├── 3.2.2 Service Auth
│   │   ├── 3.2.3 Controllers Login/Register
│   │   └── 3.2.4 Tests unitaires
│   ├── 3.3 Module Utilisateurs/Compétences
│   │   ├── 3.3.1 Entités User, Skill, UserSkill
│   │   ├── 3.3.2 Repositories JPA
│   │   ├── 3.3.3 Services métier
│   │   ├── 3.3.4 Controllers REST
│   │   └── 3.3.5 Tests intégration
│   ├── 3.4 Module Équipes
│   ├── 3.5 Module Projets
│   ├── 3.6 Module Tâches
│   ├── 3.7 Algorithme de matching
│   ├── 3.8 Dashboard et statistiques
│   └── 3.9 Notifications
│
├── 4. Développement Frontend (Niveau 1)
│   ├── 4.1 Setup Nuxt 3 + Tailwind
│   ├── 4.2 Authentification (Login/Register)
│   ├── 4.3 Pages Profil utilisateur
│   ├── 4.4 Gestion des équipes
│   ├── 4.5 Gestion des projets
│   ├── 4.6 Gestion des tâches (Kanban)
│   ├── 4.7 Dashboard
│   └── 4.8 Notifications temps réel
│
├── 5. Tests et Qualité (Niveau 1)
│   ├── 5.1 Tests unitaires backend (JUnit)
│   ├── 5.2 Tests intégration (Testcontainers)
│   ├── 5.3 Tests unitaires frontend (Vitest)
│   └── 5.4 Tests E2E (Playwright)
│
├── 6. Déploiement (Niveau 1)
│   ├── 6.1 Configuration Docker
│   ├── 6.2 CI/CD GitHub Actions
│   ├── 6.3 Déploiement Render.com
│   └── 6.4 Monitoring et logs
│
└── 7. Documentation (Niveau 1)
    ├── 7.1 Documentation technique
    ├── 7.2 Documentation utilisateur
    ├── 7.3 README et guides
    └── 7.4 Bilan de projet
```

### 5.2 Livrables par phase

| Phase | Livrables | Responsable | Durée |
|-------|-----------|-------------|-------|
| **Phase 1** | Dossiers projet, CdC, Étude faisabilité, Roadmap | Michel-Pierre | 1 semaine |
| **Phase 2** | MCD, Maquettes Figma, Diagrammes, Swagger | Michel-Pierre | 1 semaine |
| **Phase 3** | API REST fonctionnelle (26 endpoints) | Michel-Pierre | 4 semaines |
| **Phase 4** | Frontend SPA complet | Michel-Pierre | 3 semaines |
| **Phase 5** | Rapport de tests (>80% couverture) | Michel-Pierre | 1 semaine |
| **Phase 6** | App déployée en production | Michel-Pierre | 3 jours |
| **Phase 7** | Docs finales + Bilan | Michel-Pierre | 2 jours |

---

## 6. Planification PERT

### 6.1 Réseau PERT simplifié

> **📌 Note** : Diagramme PERT complet dans `assets/diagrammes/PERT.drawio`

```
Chemin critique (en gras) :

[A] Cadrage (5j)
    ↓
[B] Conception BDD (3j) ───────┐
    ↓                          │
[C] Setup Backend (2j) ────────┤
    ↓                          │
[D] Auth JWT (5j) ─────────────┤
    ↓                          │
[E] Module Users (5j) ─────────┤
    ↓                          │
[F] Module Teams (3j) ─────────┤
    ↓                          │
[G] Module Projects (3j) ──────┤
    ↓                          │
[H] Module Tasks (5j) ─────────┤
    ↓                          ├─→ [M] Setup Frontend (2j)
[I] Matching (4j) ─────────────┤       ↓
    ↓                          ├─→ [N] Frontend Auth (3j)
[J] Dashboard (3j) ────────────┤       ↓
    ↓                          ├─→ [O] Frontend Pages (10j)
[K] Notifications (3j) ────────┤       ↓
    ↓                          ├─→ [P] Frontend Dashboard (2j)
[L] Tests Backend (3j) ────────┘       ↓
                                   [Q] Tests E2E (3j)
                                       ↓
                                   [R] Déploiement (2j)
                                       ↓
                                   [S] Documentation (2j)
```

### 6.2 Chemin critique

**Chemin critique** (le plus long, détermine la durée minimale) :

```
A → B → C → D → E → F → G → H → I → J → K → L → M → N → O → P → Q → R → S

Durée totale : 5 + 3 + 2 + 5 + 5 + 3 + 3 + 5 + 4 + 3 + 3 + 3 + 2 + 3 + 10 + 2 + 3 + 2 + 2
             = 68 jours ouvrés
             ≈ 13-14 semaines (avec weekends)
             ≈ 3 mois
```

**⚠️ Attention** : Tout retard sur une tâche du chemin critique retarde le projet.

### 6.3 Marges et flexibilité

| Tâche | Durée | Marge libre | Criticité |
|-------|-------|-------------|-----------|
| A - Cadrage | 5j | 0j | 🔴 Critique |
| B - Conception BDD | 3j | 0j | 🔴 Critique |
| D - Auth JWT | 5j | 0j | 🔴 Critique |
| E - Module Users | 5j | 0j | 🔴 Critique |
| H - Module Tasks | 5j | 0j | 🔴 Critique |
| O - Frontend Pages | 10j | 0j | 🔴 Critique |
| L - Tests Backend | 3j | 2j | 🟡 Flexible |
| P - Frontend Dashboard | 2j | 1j | 🟡 Flexible |

**📊 Répartition** :
- **70% des tâches** : Critiques (chemin critique)
- **30% des tâches** : Flexibles (marge de 1-2 jours)

---

## 7. Analyse des risques et mitigation

### 7.1 Matrice des risques (complète)

| ID | Risque | Impact | Probabilité | Criticité | Mitigation |
|----|--------|--------|-------------|-----------|------------|
| **R1** | Retard sur le planning | 🔴 Élevé | 🟡 Moyen | **HAUTE** | Buffer de 2 semaines, priorisation MVP strict |
| **R2** | Bugs bloquants en production | 🔴 Élevé | 🟢 Faible | **MOYENNE** | Tests auto (>80%), CI/CD, monitoring Sentry |
| **R3** | Perte de données (BDD) | 🔴 Critique | 🟢 Faible | **MOYENNE** | Backups auto quotidiens, réplication PostgreSQL |
| **R4** | Complexité technique sous-estimée | 🟡 Moyen | 🟡 Moyen | **MOYENNE** | POCs sur features complexes (matching, notifs) |
| **R5** | Burnout (solo dev) | 🔴 Élevé | 🟡 Moyen | **HAUTE** | Limiter à 40h/semaine, pauses régulières |
| **R6** | Obsolescence techno (dépendances) | 🟢 Faible | 🟢 Faible | **FAIBLE** | Stack mature (Spring Boot LTS, Nuxt stable) |
| **R7** | Faille de sécurité (auth) | 🔴 Critique | 🟢 Faible | **MOYENNE** | JWT best practices, Spring Security, audits |
| **R8** | Coûts d'hébergement | 🟢 Faible | 🟢 Faible | **FAIBLE** | Free tier Render, scaling progressif |
| **R9** | Manque de feedback utilisateur | 🟡 Moyen | 🟡 Moyen | **MOYENNE** | Tests utilisateurs post-MVP, analytics |
| **R10** | Performance dégradée (scaling) | 🟡 Moyen | 🟢 Faible | **FAIBLE** | Indexes BDD, caching, pagination API |

### 7.2 Plan de mitigation prioritaire

#### Risque R1 : Retard sur le planning

**Actions** :
1. ✅ Prioriser **strictement** les US selon MoSCoW (Must/Should/Could/Won't)
2. ✅ Buffer de **2 semaines** avant date limite projet
3. ✅ Revue hebdomadaire du planning (Sprint Review)
4. ✅ Découper les US trop grandes (> 13h) en sous-tâches

**Indicateurs** :
- Vélocité moyenne par sprint (objectif : 3-4 US/sprint)
- Burndown chart (GitHub Projects)

#### Risque R5 : Burnout

**Actions** :
1. ✅ Journées limitées à **8h** (9h-12h + 13h-18h)
2. ✅ Weekends **sans code** (repos complet)
3. ✅ Pause déjeuner obligatoire (1h)
4. ✅ Pauses toutes les 2h (Pomodoro 2h ON / 15min OFF)
5. ✅ Activité physique 3×/semaine

**Indicateurs** :
- Nombre d'heures effectives par semaine (max 40h)
- Niveau de fatigue (échelle 1-10 en fin de journée)

#### Risque R7 : Faille de sécurité

**Actions** :
1. ✅ Utiliser Spring Security (framework éprouvé)
2. ✅ JWT avec expiration courte (24h) + refresh tokens
3. ✅ HTTPS obligatoire (TLS 1.3)
4. ✅ Validation stricte des inputs (@Valid)
5. ✅ Audit de sécurité avec SonarQube
6. ✅ Dépendances à jour (Dependabot GitHub)

**Indicateurs** :
- Score SonarQube Security Hotspots (0 critical)
- Nombre de vulnérabilités CVE (0)

---

## 8. Conclusion et recommandations

### 8.1 Synthèse de faisabilité

| Dimension | Évaluation | Justification |
|-----------|------------|---------------|
| **Technique** | ✅ **VIABLE** | Stack mature, pas de dépendance propriétaire, complexité maîtrisée |
| **Économique** | ✅ **RENTABLE** | Coût MVP ~10€, ROI projeté >600% en 1 an (mode SaaS) |
| **Organisationnelle** | ⚠️ **ACCEPTABLE** | Solo dev gérable avec méthodologie Agile adaptée et limites strictes |
| **Temporelle** | ✅ **RÉALISABLE** | 68 jours ouvrés (3 mois) avec marge de sécurité de 2 semaines |

### 8.2 Facteurs de succès

✅ **Points forts** :
1. Stack technologique moderne et bien documentée
2. Budget minimal (gratuité des outils)
3. Méthodologie Agile adaptée au solo dev
4. Planification détaillée (WBS, PERT, Gantt)
5. Priorisation claire des features (MVP-first)
6. Expérience pédagogique valorisante

### 8.3 Points de vigilance

⚠️ **Risques à surveiller** :
1. **Burnout** : Respecter strictement les 40h/semaine
2. **Scope creep** : Ne pas ajouter de features hors MVP
3. **Complexité sous-estimée** : Prévoir du temps pour recherche/debug
4. **Isolation** : Chercher du feedback externe (formateurs, pairs)

### 8.4 Recommandations stratégiques

#### Recommandation 1 : Approche MVP stricte

**Priorisation MoSCoW** :

| Catégorie | US incluses | Livraison |
|-----------|-------------|-----------|
| **MUST** (MVP) | US-001 à US-022 (auth, CRUD, assignation) | Sprint 0-6 |
| **SHOULD** (v1.1) | US-023 à US-026 (dashboard, notifs) | Sprint 7-8 |
| **COULD** (v2.0) | Analytics IA, exports PDF, webhooks | Post-formation |
| **WON'T** | Mobile app native, mode offline | Non prévu |

#### Recommandation 2 : Stratégie de tests

```
Tests unitaires (70%) : Développés en parallèle du code
Tests intégration (25%) : Sprint 8 (dédiés)
Tests E2E (5%) : Sprint 8-9 (parcours critiques)
```

#### Recommandation 3 : Déploiement continu

- **Staging** : Déploiement auto sur branche `develop` (GitHub Actions)
- **Production** : Déploiement manuel sur branche `main` (validation)
- **Monitoring** : Sentry gratuit pour tracking erreurs

#### Recommandation 4 : Documentation continue

- **README.md** : Mis à jour à chaque sprint
- **API Docs** : Swagger auto-généré
- **User Docs** : Rédigés en parallèle des features (Sprint 9)

### 8.5 Décision finale

**🎯 AVIS : PROJET VALIDÉ POUR LANCEMENT**

**Conditions** :
1. ✅ Respect strict du périmètre MVP (US-001 à US-022)
2. ✅ Planification Agile avec sprints de 1 semaine
3. ✅ Suivi hebdomadaire de la vélocité et du burndown
4. ✅ Limites strictes de temps (40h/semaine max)
5. ✅ Revues régulières avec formateurs (tous les 2 sprints)

**📅 Date de lancement prévue** : 06/01/2026 (Sprint 0)  
**📅 Date de livraison MVP** : 14/03/2026 (Sprint 9)  
**📅 Marge de sécurité** : 2 semaines (livraison finale 28/03/2026)

---

## 📎 Annexes

### A. Documents liés

- [01_Dossier_Projet.md](01_Dossier_Projet.md) - Contexte et objectifs
- [02_CdCF.md](02_CdCF.md) - Spécifications fonctionnelles
- [03_CdCT.md](03_CdCT.md) - Spécifications techniques
- [05_Vision_Produit_Roadmap.md](05_Vision_Produit_Roadmap.md) - Roadmap long terme

### B. Diagrammes à créer

- `assets/diagrammes/WBS.drawio` - Work Breakdown Structure complète
- `assets/diagrammes/PERT.drawio` - Réseau PERT avec chemins critiques
- `assets/diagrammes/Gantt.xlsx` - Planning Gantt détaillé (10 sprints)

### C. Outils de suivi

| Outil | Usage | Lien |
|-------|-------|------|
| **GitHub Projects** | Backlog + Kanban | https://github.com/users/[USERNAME]/projects |
| **GitHub Issues** | Suivi des 26 US | Repository issues |
| **GitHub Actions** | CI/CD | `.github/workflows/` |
| **Google Sheets** | Suivi vélocité | (optionnel) |

### D. Historique des versions

| Version | Date | Auteur | Modifications |
|---------|------|--------|---------------|
| 1.0 | 04/01/2026 | Michel-Pierre | Création complète de l'étude de faisabilité |

---

**Document validé par** : Michel-Pierre  
**Date de validation** : 04/01/2026  
**Prochaine revue prévue** : 20/01/2026 (après Sprint 2)
