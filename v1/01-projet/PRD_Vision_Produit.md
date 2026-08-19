---
id: prd-vision-produit
title: PRD — Product Requirements Document / Vision produit
doc_type: prd
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [prd, vision, produit, personas, smart, objectifs, memoire, rncp]
---

# 🚀 PRD — Vision produit TaskForce

> Synthèse orientée produit (format PRD). Pour le fonctionnel détaillé → [[CdCF_v2]] ;
> pour le business → [[Business_Model_Pricing]] ; pour le cadrage → [[Note_Cadrage]].
> Source : [[Dossier_Projet]] (v1.2, 17/01/2026).

---

## 1. Proposition de valeur

**TaskForce** élimine la surcharge managériale liée à la répartition manuelle des tâches.

> « *Les managers passent 40 % de leur temps sur des tâches administratives de coordination.
> 44 % des salariés sont en stress chronique. TaskForce automatise l'assignation et détecte
> la surcharge — le manager valide, le système propose.* »

**Différenciateur principal** : moteur d'assignation IA explicable (compétences × charge × disponibilité,
affiné par LLM Groq) — unique sur le segment PME. Les concurrents (Jira, Monday, Asana) gèrent
l'*état* des tâches mais n'assistent pas la *décision d'affectation*.

---

## 2. Personas

### 👩‍💼 Alice — Gestionnaire (ADMIN/OWNER)
**Profil** : Chef de projet dans une PME 20–100 personnes.  
**Douleur** : passe 2 h/jour à jongler entre les disponibilités, compétences et charges de son équipe.  
**Besoin** : voir en 1 clic qui peut prendre quelle tâche, sans se tromper sur la surcharge.  
**Gain TaskForce** : smart-assign en 3 secondes, redistribution en 1 clic validé, alertes de surcharge proactives.

### 🧑‍💻 Bob — Collaborateur (MEMBER)
**Profil** : Développeur ou technicien, membre d'équipe.  
**Douleur** : tâches tombées par mail, pas de visibilité globale sur sa charge.  
**Besoin** : voir ses tâches priorisées, loguer son temps, comprendre pourquoi il a été assigné.  
**Gain TaskForce** : MyWork dashboard, justification LLM de l'assignation, worklogs intégrés.

### 🏢 Paula — Propriétaire (OWNER)
**Profil** : Responsable / fondateur qui gère l'abonnement et les accès.  
**Besoin** : maîtrise complète du workspace, facturation simple, conformité RGPD garantie.  
**Gain TaskForce** : portail Stripe self-service, export RGPD one-click, rôle OWNER distinct.

---

## 3. Objectifs produit (SMART — V1)

| # | Objectif | Mesure | Statut V1 |
|---|---|---|---|
| O1 | Core applicatif (auth + CRUD + smart-assign) | Fonctionnel, testé | ✅ 31/01/2026 |
| O2 | SaaS multi-tenant + Stripe | 2 plans actifs (FREE/PRO) | ✅ 28/02/2026 |
| O3 | RGPD + accessibilité WCAG 2.1 AA | Export portabilité + axe-core | ✅ 28/03/2026 |
| O4 | Déploiement prod (VM école) | Env dev/prod séparés | 🔄 en cours |
| O5 | Qualité (tests + sécurité) | JaCoCo ≥ 60 %, 0 vuln. critique | ✅ 20/06/2026 |
| O6 | Documentation complète (97 docs) | Catalogue rempli | 🔄 en cours |

---

## 4. Fonctionnalités clés V1 (livrées)

> Détail complet → [[CdCF_v2]] §4. Résumé orienté valeur produit :

| Feature | Valeur utilisateur |
|---|---|
| **Smart-assign** | Recommandation d'assignation en ~3 s avec justification LLM |
| **Redistribution auto** | Plan de réaffectation complet en 1 clic → validation manager → apply |
| **Alertes de surcharge** | Détection automatique planifiée → notification ADMIN/OWNER |
| **Profils de compétences + croissance** | Matching précis + mode « junior progressant » (`growth_enabled`) |
| **Congés / disponibilités** | Données réelles dans le scoring (pas de surcharge sur congé) |
| **Chat temps réel** | Collaboration dans l'outil, sans Slack/Teams externe |
| **Brain OS** | Knowledge graph d'équipe, assistant IA contextualisé |
| **RGPD by design** | Export + anonymisation sans développement supplémentaire |

---

## 5. Architecture produit

```
Core applicatif
├── Identité & Workspace (multi-tenant, RBAC)
├── Projets & Issues (board, cycles/sprints, pages)
├── ⭐ Répartition intelligente (smart-assign + redistribution)
├── Collaboratif (chat STOMP, discussions, notifications)
├── IA / Brain OS (knowledge graph + assistant)
├── Intégrations (GitHub, Slack, webhooks)
└── Facturation (Stripe — FREE/PRO)

Modules futurs (backlog)
└── LIMS · Qualité ISO · GED réglementaire
```

---

## 6. Métriques de succès (indicateurs de validation)

| Métrique | Cible V1 | Mesure |
|---|---|---|
| Couverture tests back-end | ≥ 60 % (JaCoCo) | Rapport JaCoCo |
| Couverture tests front-end | ≥ 70 % (Vitest) | Rapport Vitest v8 |
| Temps de réponse API (p95) | < 200 ms | Prometheus histogram |
| Vulnérabilités critiques | 0 (SAST + SCA + ZAP) | `security-scan.ps1` |
| Violations accessibilité axe-core | < 10 | `a11y.spec.ts` |
| Docs produits (catalogue) | ~97 | [[Catalogue_Documentation]] |

---

## 7. Périmètre hors V1 (backlog produit)

- Modules sectoriels LIMS / Qualité ISO / GED
- Rôle Invité (accès lecture externe)
- Export rapport PDF/Excel
- SSO SAML / Active Directory
- CI/CD complet déployé en prod
- Landing page (refonte totale)

→ [[Roadmap_Backlog]] pour le détail priorisé.

> 🔗 Voir aussi : [[Note_Cadrage]] · [[CdCF_v2]] · [[Business_Model_Pricing]] ·
> [[Dossier_Projet]] · [[Etude_business]].
