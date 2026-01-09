# 📚 Documentation TaskForce - Architecture et Guide

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

> **Projet fil rouge** - Gestion de projets et assignation intelligente de tâches  
> **Étudiant** : Michel-Pierre  
> **Formation** : Développement Full Stack  
> **École** : Metz Numeric School  
> **Méthodologie** : Agile Solo (Scrum adapté)  
> **Période** : Décembre 2025 - Juin 2026

---

## 🎯 Objectif de ce repository

Ce repository `taskforce-docs` contient **toute la documentation** du projet TaskForce, séparée du code source (`taskforce-fullstack`). Il suit une approche méthodique et professionnelle de gestion de projet agile en solo.

---

## 📂 Architecture de la documentation

```
taskforce-docs/
├── 01_CADRAGE_ET_PLANIFICATION/       # Phase initiale : vision, besoins, planification
├── 02_REALISATION_ET_CONCEPTION/      # Phase de conception technique et UI/UX
├── 03_LIVRAISON_DEPLOIEMENT_ET_BILAN/ # Phase finale : déploiement, doc utilisateur, bilan
├── 04_SUIVI_PILOTAGE/                 # Suivi continu du projet (journal, sprints, KPI)
├── assets/                            # Ressources (images, diagrammes, charts, maquettes)
├── templates/                         # Templates réutilisables (US, tests, retro)
├── NOTES.md                           # Notes de travail et références
├── Rules.md                           # Règles et conventions du projet
└── README.md                          # Ce fichier
```

---

## 📋 Liste des documents par phase

### **Phase 1 : CADRAGE & PLANIFICATION**
> Période : Décembre 2025 - Janvier 2026  
> Objectif : Définir la vision, les objectifs, le périmètre et planifier le projet

| # | Document | Description | Statut | Priorité |
|---|----------|-------------|--------|----------|
| 01 | [Dossier Projet](01_CADRAGE_ET_PLANIFICATION/01_Dossier_Projet.md) | Contexte, objectifs SMART, parties prenantes, planning Gantt, PBS | 🔄 En cours | 🔴 Critique |
| 02 | [CdCF - Cahier des Charges Fonctionnel](01_CADRAGE_ET_PLANIFICATION/02_CdCF.md) | Vision produit, benchmark, user personas, fonctionnalités, règles métier | 🔄 En cours | 🔴 Critique |
| 03 | [CdCT - Cahier des Charges Technique](01_CADRAGE_ET_PLANIFICATION/03_CdCT.md) | Stack technique, architecture, contraintes, APIs, infrastructure | 🔄 En cours | 🔴 Critique |
| 04 | [Étude de Faisabilité](01_CADRAGE_ET_PLANIFICATION/04_Etude_Faisabilite.md) | Faisabilité technique/temporelle/humaine/financière, WBS, PERT | ⏳ À faire | 🔴 Critique |
| 05 | [Vision Produit & Roadmap](01_CADRAGE_ET_PLANIFICATION/05_Vision_Produit_Roadmap.md) | Vision long terme, roadmap par phase, milestones, release plan | ⏳ À faire | 🟡 Haute |
| 06 | [User Stories & Backlog](01_CADRAGE_ET_PLANIFICATION/06_User_Stories_Backlog.md) | 26 US exportées de GitHub, mapping epics/milestones, priorisation MoSCoW | ⏳ À faire | 🔴 Critique |

**Diagrammes associés** :
- Parties prenantes (Draw.io)
- Gantt planning (Draw.io)
- PBS - Product Breakdown Structure (Draw.io)
- WBS - Work Breakdown Structure (Draw.io)
- PERT (Draw.io)
- User Stories Excel (assets/charts/)

---

### **Phase 2 : RÉALISATION & CONCEPTION**
> Période : Janvier 2026 - Avril 2026  
> Objectif : Concevoir l'architecture, l'UI/UX, les APIs et développer

| # | Document | Description | Statut | Priorité |
|---|----------|-------------|--------|----------|
| 07 | [Dossier UI/UX](02_REALISATION_ET_CONCEPTION/07_Dossier_UI_UX.md) | Charte graphique, principes UX, wireframes, maquettes, design system | ⏳ À faire | 🟡 Haute |
| 08 | [Conception Technique](02_REALISATION_ET_CONCEPTION/08_Conception_Technique.md) | Architecture détaillée, MCD/MLD, diagrammes UML (classes, séquence, activité) | ⏳ À faire | 🔴 Critique |
| 09 | [Documentation API](02_REALISATION_ET_CONCEPTION/09_API_Documentation.md) | Endpoints REST, contrats d'API, schéma OpenAPI/Swagger | ⏳ À faire | 🟡 Haute |
| 10 | [Conventions de Code](02_REALISATION_ET_CONCEPTION/10_Convention_Code.md) | Standards Java/TypeScript, nomenclature, Git workflow, tests | ⏳ À faire | 🟡 Haute |
| 11 | [Cahier de Test & Recettes](02_REALISATION_ET_CONCEPTION/11_Cahier_Test_Recettes.md) | Stratégie de test, plan de test, cas de test par US, critères de validation | ⏳ À faire | 🔴 Critique |

**Diagrammes associés** :
- Use Case global (Draw.io)
- User Journey (Draw.io)
- Architecture logicielle (Draw.io)
- MCD - Modèle Conceptuel de Données (Draw.io)
- MLD - Modèle Logique de Données (Draw.io)
- Diagrammes de classes UML (Draw.io)
- Diagrammes de séquence UML (Draw.io)
- Wireframes & maquettes (Figma / assets/maquettes/)

---

### **Phase 3 : LIVRAISON, DÉPLOIEMENT & BILAN**
> Période : Mai 2026 - Juin 2026  
> Objectif : Déployer, documenter, former, bilan et soutenance

| # | Document | Description | Statut | Priorité |
|---|----------|-------------|--------|----------|
| 12 | [Plan de Déploiement](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/12_Plan_Deploiement.md) | Environnements (dev/staging/prod), CI/CD, Docker, procédures déploiement | ⏳ À faire | 🟡 Haute |
| 13 | [PS/PCA/PRA](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/13_PS_PCA_PRA.md) | Plan de Secours, Continuité d'Activité, Reprise d'Activité, sauvegarde | ⏳ À faire | 🟢 Moyenne |
| 14 | [Documentation Utilisateur](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/14_Documentation_Utilisateur.md) | Guide utilisateur, FAQ, tutoriels, prise en main | ⏳ À faire | 🟡 Haute |
| 15 | [Documentation Technique](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/15_Documentation_Technique.md) | Installation locale, configuration, maintenance, troubleshooting | ⏳ À faire | 🟡 Haute |
| 16 | [Bilan Projet](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/16_Bilan_Projet.md) | Rétrospective globale, KPI & métriques, ROI, retour d'expérience, perspectives | ⏳ À faire | 🔴 Critique |

**Diagrammes associés** :
- Diagramme de déploiement (Draw.io)
- Architecture CI/CD (Draw.io)

---

### **Phase 4 : SUIVI & PILOTAGE** (en continu)
> Période : Décembre 2025 - Juin 2026  
> Objectif : Suivre l'avancement, piloter les sprints, mesurer la vélocité

| # | Document | Description | Statut | Priorité |
|---|----------|-------------|--------|----------|
| 17 | [Journal de Bord](04_SUIVI_PILOTAGE/17_Journal_Bord.md) | Journal quotidien/hebdomadaire, avancement, blocages, décisions | ⏳ À faire | 🟡 Haute |
| 18 | [Comptes Rendus Sprint](04_SUIVI_PILOTAGE/18_Comptes_Rendus_Sprint.md) | CR de chaque sprint (planning, review, retrospective) | ⏳ À faire | 🟡 Haute |
| 19 | [Burndown & Vélocité](04_SUIVI_PILOTAGE/19_Burndown_Velocity.md) | Charts burndown, vélocité, KPI agiles | ⏳ À faire | 🟢 Moyenne |

**Charts associés** :
- Burndown chart par sprint (assets/charts/)
- Vélocité moyenne (assets/charts/)
- Cumulative flow diagram (assets/charts/)

---

## 🗂️ Templates réutilisables

Dans le dossier `templates/`, tu trouveras des modèles pour :

| Template | Usage |
|----------|-------|
| [User Story Template](templates/user_story_template.md) | Créer une nouvelle user story |
| [Test Case Template](templates/test_case_template.md) | Créer un cas de test |
| [Sprint Retrospective Template](templates/sprint_retrospective_template.md) | Rédiger une rétrospective de sprint |

---

## 🔄 Ordre de lecture recommandé

### Pour comprendre le projet :
1. **[Dossier Projet](01_CADRAGE_ET_PLANIFICATION/01_Dossier_Projet.md)** - Vue d'ensemble
2. **[CdCF](01_CADRAGE_ET_PLANIFICATION/02_CdCF.md)** - Fonctionnalités et besoins métier
3. **[User Stories](01_CADRAGE_ET_PLANIFICATION/06_User_Stories_Backlog.md)** - Détail des fonctionnalités
4. **[CdCT](01_CADRAGE_ET_PLANIFICATION/03_CdCT.md)** - Choix techniques

### Pour développer :
1. **[Conception Technique](02_REALISATION_ET_CONCEPTION/08_Conception_Technique.md)** - Architecture et modèle de données
2. **[API Documentation](02_REALISATION_ET_CONCEPTION/09_API_Documentation.md)** - Contrats d'API
3. **[Conventions de Code](02_REALISATION_ET_CONCEPTION/10_Convention_Code.md)** - Standards et bonnes pratiques

### Pour déployer :
1. **[Plan de Déploiement](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/12_Plan_Deploiement.md)** - Procédures de déploiement
2. **[Documentation Technique](03_LIVRAISON_DEPLOIEMENT_ET_BILAN/15_Documentation_Technique.md)** - Installation et configuration

---

## 🛠️ Stack Technique

**Backend :**
- Java 17+ avec Spring Boot
- PostgreSQL
- Maven
- Docker

**Frontend :**
- Nuxt 3 (Vue.js)
- TypeScript
- Tailwind CSS
- Shadcn-vue (Design System)

**DevOps :**
- Docker & Docker Compose
- GitHub Actions (CI/CD)
- GitHub Projects (gestion agile)

---

## 📊 Méthodologie Agile Solo

- **Sprints** : 2 semaines
- **User Stories** : 26 US réparties sur 5 milestones
- **Epics** : auth, teams, projects, tasks, dashboard, notifications, admin
- **Milestones** :
  - M1 : Auth & Profils
  - M2 : Projets & Tâches
  - M3 : Dashboards
  - M4 : Collaboration
  - M5 : MVP Complet

**GitHub Projects** : [taskforce-fullstack](https://github.com/Miche1-Pierre/taskforce-fullstack)

---

## 📝 Conventions

### Statut des documents :
- ✅ **Complété** : Document terminé et validé
- 🔄 **En cours** : Document en rédaction
- ⏳ **À faire** : Document à rédiger
- ❌ **Bloqué** : Document bloqué (dépendances)

### Priorités :
- 🔴 **Critique** : À faire en priorité absolue
- 🟡 **Haute** : Important pour l'avancement
- 🟢 **Moyenne** : Peut attendre
- ⚪ **Basse** : Nice to have

### Nomenclature des fichiers :
- Numérotation séquentielle : `01_`, `02_`, etc.
- Snake_case pour les noms de fichiers
- Extensions : `.md` pour docs, `.drawio` pour diagrammes

---

## 📞 Contacts & Ressources

- **Repository code** : [taskforce-fullstack](https://github.com/Miche1-Pierre/taskforce-fullstack)
- **Repository docs** : [taskforce-docs](https://github.com/Miche1-Pierre/taskforce-docs)
- **GitHub Projects** : Backlog & suivi des US

---

## 🚀 Prochaines étapes

1. ✅ Structurer la documentation (fait)
2. 🔄 Rédiger le Dossier Projet avec diagrammes
3. 🔄 Compléter le CdCF avec benchmark et personas
4. 🔄 Finaliser le CdCT avec architecture détaillée
5. ⏳ Créer les diagrammes Draw.io (Gantt, PERT, WBS, MCD, UML)
6. ⏳ Rédiger l'étude de faisabilité
7. ⏳ Exporter les User Stories dans le backlog
8. ⏳ Démarrer le développement des premières US du M1

---

**Dernière mise à jour** : 4 janvier 2026  
**Version** : 1.0
