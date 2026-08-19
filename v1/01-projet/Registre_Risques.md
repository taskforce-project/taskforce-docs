---
id: registre-risques
title: Registre des risques — TaskForce V1
doc_type: registre-risques
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [risques, registre, mitigation, probabilite, impact, memoire, rncp]
---

# ⚠️ Registre des risques — TaskForce V1

> Identification, évaluation et plans de mitigation des risques du projet.
> Source : [[Dossier_Projet]] §13 + risques observés en cours de réalisation.
> **Légende** : Prob. (F=Faible/M=Moyen/H=Haut) · Impact (F/M/H) · Criticité = Prob × Impact.

---

## Matrice des risques

| ID | Risque | Prob. | Impact | Criticité | Plan de mitigation | Statut |
|---|---|:---:|:---:|:---:|---|:---:|
| R01 | **Surcharge mono-acteur** — concentration de tous les rôles sur une personne | H | H | 🔴 | Priorisation Eisenhower ; feature freeze acté ; aide Brain OS pour la doc | 🟡 Géré |
| R02 | **VM école non disponibles** à temps pour le déploiement prod | M | H | 🔴 | Démo locale documentée ; `docker-compose.prod.yml` prêt ; guide déploiement rédigé | 🔄 Actif |
| R03 | **Scope creep** (ajout features sans fin) | H | M | 🟠 | Feature freeze 20/06/2026 ; MoSCoW explicite ; backlog dédié | ✅ Résolu |
| R04 | **Complexité technique** (intégrations multiples : Keycloak, Stripe, Groq, pgvector) | M | H | 🔴 | Prototypage précoce M1 ; tests d'intégration Testcontainers ; docmentation ARCHITECTURE.md | ✅ Résolu |
| R05 | **Dépendance Groq API** (LLM externe, rate-limiting, pannes) | F | M | 🟡 | Smart-assign dégradé sans LLM (scoring local seul) ; `GroqServiceContractTest` | 🟢 Mitigé |
| R06 | **Contraintes RGPD non couvertes** (conformité CNIL) | M | H | 🔴 | Export portabilité + anonymisation livrés ; `GdprServiceIntegrationTest` | ✅ Résolu |
| R07 | **Sécurité — vulnérabilité critique** non détectée | M | H | 🔴 | SAST Semgrep + SCA Trivy + DAST ZAP baseline ; `SecurityHeadersWebMvcTest` | ✅ Résolu |
| R08 | **Couverture tests insuffisante** (JaCoCo < seuil) | F | M | 🟡 | Seuil JaCoCo 60 % configuré dans `pom.xml` ; build fails si < seuil | ✅ Résolu |
| R09 | **Dépendance technologique** (abandon d'une lib open source) | F | M | 🟡 | Stack mature (Spring Boot, Next.js, PostgreSQL) ; veille active | 🟢 Mitigé |
| R10 | **Perte de motivation / isolement** (projet solo 9 mois) | M | M | 🟠 | Jalons réguliers valorisés ; Brain OS comme mémoire externe ; dogfooding TaskForce | ✅ Résolu |
| R11 | **Données corrompues en migration** (Flyway V1→V56) | F | H | 🟠 | Migrations atomiques testées ; seed dev séparé ; `V10__rollback_OPTIONAL` | ✅ Résolu |
| R12 | **Accessibilité insuffisante** (WCAG 2.1 AA) | M | M | 🟠 | axe-core Playwright `a11y.spec.ts` ; shadcn/Radix accessible par défaut | ✅ Résolu |

---

## Risques résiduels actifs

| ID | Risque | Action en cours |
|---|---|---|
| R02 | VM école non disponibles | Guide déploiement prêt ; attente disponibilité VM |
| R01 | Surcharge documentation finale | Priorisation des docs ⭐ soutenance en premier |

---

## Légende criticité

| Couleur | Criticité | Action |
|---|:---:|---|
| 🔴 Rouge | Haut × Haut | Mitigation immédiate obligatoire |
| 🟠 Orange | Haut × Moyen ou Moyen × Haut | Surveillance active |
| 🟡 Jaune | Moyen × Moyen | Plan de mitigation défini |
| 🟢 Vert | Faible × Faible/Moyen | Acceptable, surveiller |

> 🔗 Voir aussi : [[Note_Cadrage]] §7 · [[Plan_Projet]] §6 · [[PS_PCA_PRA]] (risques opérationnels).
