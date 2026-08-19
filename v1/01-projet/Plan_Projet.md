---
id: plan-projet
title: Plan de projet — TaskForce
doc_type: plan-projet
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [plan-projet, planning, jalons, wbs, gantt, agile, memoire, rncp]
---

# 📅 Plan de projet — TaskForce

> Planification du projet fil rouge RNCP Développeur Full Stack — Metz Numeric School 2025-2026.
> Porteur unique : Pierre MICHEL (multi-rôles : chef de projet, architecte, dev, DevOps, QA).
> Source : [[Dossier_Projet]] §12 + jalons réels observés en cours de réalisation.
>
> **Diagramme de Gantt détaillé** → [[Gantt_Planning]] · **PERT** → [[Diagramme_PERT]] ·
> **Budget** → [[Budget_Previsionnel]].

---

## 1. Phases et jalons

| Phase | Dates | Livrables clés | Statut |
|---|---|---|---|
| **0 — Initialisation & cadrage** | 04/11/25 – 15/11/25 | Dossier projet, CdCF v1, CdCT v1 | ✅ |
| **1 — Conception fonctionnelle** | 18/11/25 – 29/11/25 | CdCF enrichi, wireframes, PBS/WBS | ✅ |
| **2 — Conception technique** | 02/12/25 – 20/12/25 | CdCT détaillé, MCD/MLD, UML | ✅ |
| **3 — Dev M1 : Core** | 02/01/26 – 31/01/26 | Auth Keycloak, multi-tenant, Stripe | ✅ |
| **4 — Dev M2 : Métier** | 03/02/26 – 28/02/26 | Projets/issues/compétences/smart-assign | ✅ |
| **5 — Dev M3 : Enrichissement** | 03/03/26 – 28/03/26 | Chat, Brain OS, RGPD, intégrations | ✅ |
| **6 — Tests & validation** | 31/03/26 – 26/04/26 | Rapports JaCoCo, Vitest, ZAP, axe-core | ✅ |
| **7 — Déploiement & bilan** | 28/04/26 – 23/05/26 | Docker prod, guide déploiement | 🔄 (VM école) |
| **8 — Itérations & correctifs** | 26/05/26 – 20/06/26 | Tests complémentaires, correctifs QF | ✅ |
| **9 — Documentation finale** | 23/06/26 – 05/07/26 | ~97 docs (Catalogue), bundle PDF | 🔄 en cours |

---

## 2. Chemin critique

```
Cadrage → Conception → Dev M1 (Core) → Dev M2 (Métier) → Dev M3 → Tests → Documentation → Soutenance
```

Dépendances clés :
- **Dev M2 dépend de M1** (auth, multi-tenant obligatoires)
- **Smart-assign (M2) dépend de** `member_skill_profiles` + `IssueWorklog` (migrations V33, V44, V47)
- **Brain OS dépend de pgvector** (extension PostgreSQL + migrations V51–V56)
- **Tests d'intégration dépendent** du schéma DB stable (V56)
- **Documentation dépend** des fonctionnalités stables (feature freeze fin juin)

---

## 3. Périmètre & priorisation (MoSCoW V1)

| Must Have | Should Have | Could Have | Won't Have V1 |
|---|---|---|---|
| Auth + multi-tenant | Chat temps réel | Brain OS assistant | Modules LIMS/Qualité |
| Projets + issues | Intégrations GitHub/Slack | Redistribution auto | Rôle Invité |
| Smart-assign | Export RGPD | Alertes surcharge | Export PDF/Excel |
| Stripe FREE/PRO | Accessibilité WCAG | Worklogs + analytics | CI/CD complet prod |
| Tests ≥ 60 % JaCoCo | SAST/SCA/ZAP | — | Landing page refonte |

---

## 4. Organisation & rôles (projet solo)

| Rôle | Responsabilités |
|---|---|
| **Chef de projet** | Pilotage planning, arbitrages, jalons |
| **Architecte** | Choix techniques, modèle de données, archi modulaire |
| **Dev Full Stack** | Backend Spring Boot + Frontend Next.js |
| **DevOps** | Docker Compose, migrations Flyway, scripts CI |
| **QA / Sécurité** | Tests JUnit/Vitest/Playwright, ZAP, Semgrep, Trivy |

> Gestion des conflits de rôle : priorisation par matrice Eisenhower (urgence × importance),
> suivi hebdomadaire via GitHub Projects (Issues + Milestones).

---

## 5. Outils de suivi

| Outil | Usage |
|---|---|
| **GitHub Projects** | Issues, milestones, kanban |
| **GitHub Actions** | Pipelines CI (tests, build) |
| **TaskForce lui-même** | Suivi des issues du projet (dogfooding) |
| **Brain OS (taskforce-docs)** | Documentation centralisée + mémoire RNCP |

---

## 6. Gestion des risques

> Voir [[Registre_Risques]] pour la matrice complète. Risques principaux identifiés :
>
> - **Surcharge mono-acteur** (prob. haute) → priorisation stricte, gel features
> - **VM école non disponibles** (prob. moyenne) → démo locale documentée
> - **Scope creep** (prob. haute) → feature freeze acté fin juin 2026

> 🔗 Voir aussi : [[Note_Cadrage]] · [[Gantt_Planning]] · [[Diagramme_PERT]] ·
> [[Budget_Previsionnel]] · [[Note_Methode_Agile]] · [[Registre_Risques]].
