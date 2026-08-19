---
id: note-cadrage
title: Note de cadrage — TaskForce
doc_type: cadrage
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [cadrage, projet, rncp, dfs, contexte, perimetre, objectifs, contraintes, risques, memoire]
---

# 📌 Note de cadrage — TaskForce

> Document de référence **court** synthétisant l'origine, le périmètre, les objectifs mesurables,
> les contraintes et les risques du projet. Pivot du référentiel DFS (cité dans presque tous les
> livrables). Pour le détail fonctionnel → [[01_CdCF|CdCF v1]] ; pour le détail technique → [[02_CdCT|CdCT v1]].

---

## 1. Origine & commanditaire

| Champ | Valeur |
|---|---|
| **Projet** | TaskForce — SaaS de gestion de projet avec répartition intelligente des tâches |
| **Porteur** | Pierre MICHEL |
| **Établissement** | Metz Numeric School — Titre RNCP « Développeur Full Stack » (DFS), année 2025-2026 |
| **Nature** | Projet fil rouge de certification · solo toutes fonctions (chef de projet, architecte, dev, DevOps, QA) |
| **Date de lancement** | Septembre 2025 |
| **Horizon V1** | Juillet 2026 (soutenance RNCP) |

---

## 2. Problématique

Dans un contexte professionnel moderne, la répartition **manuelle** des tâches est une source de
déséquilibres de charge, de perte de productivité et de démotivation. Les managers passent jusqu'à
40 % de leur temps sur des tâches administratives de coordination (McKinsey 2023) ; 44 % des salariés
sont en stress chronique (Gallup 2023). Les outils existants (Jira, Linear, Asana) gèrent **l'état**
des tâches mais n'assistent pas la **décision d'affectation** en tenant compte des compétences réelles,
de la charge courante et des disponibilités.

---

## 3. Vision produit & positionnement

**TaskForce** est un SaaS de gestion de projet multi-tenant (famille Linear/Jira), différencié par un
**moteur de répartition intelligente** des tâches piloté par l'IA (scoring compétences × charge ×
disponibilité, affiné par LLM Groq). Le gestionnaire conserve le contrôle : l'outil **propose**, le
gestionnaire **valide**.

Positionnement cible : PME 50–250 collaborateurs · plan Free (fonctionnel limité) + plan Pro
(13 €/user/mois) · hébergement cloud SaaS.

---

## 4. Périmètre fonctionnel V1 (livré)

| Domaine | Fonctionnalités clés livrées |
|---|---|
| **Identité & workspace** | Inscription + OTP, login Keycloak/JWT, multi-tenant workspace, RBAC (OWNER/ADMIN/MEMBER) |
| **Projets & issues** | CRUD projets, issues avec statuts/types/priorités/cycles, sous-tâches, relations, checklist, worklogs |
| **⭐ Répartition intelligente** | Smart-assign (compétences + charge + dispo + LLM), redistribution auto (preview → validation manager) |
| **Collaboratif** | Chat temps réel STOMP, discussions, notifications, pages wiki |
| **Intégrations** | GitHub (liens issues), Slack (channels), webhooks entrants |
| **Facturation** | Stripe Checkout + webhooks + portail client (plans FREE/PRO) |
| **IA / Brain OS** | Knowledge graph natif (pgvector), assistant conversationnel Groq |
| **RGPD** | Export portabilité (Art. 20), anonymisation (droit à l'oubli) |
| **Observabilité** | OpenTelemetry → SigNoz, Prometheus/Grafana, 9 règles d'alerte |
| **Sécurité** | OWASP A01–A10, SAST (Semgrep), SCA (Trivy), DAST (ZAP baseline) |

**Hors périmètre V1** (backlog) : modules LIMS/Qualité, CI/CD déployé, landing page finale, i18n.

---

## 5. Objectifs mesurables (SMART)

| # | Objectif | Indicateur cible | Échéance |
|---|---|---|---|
| O1 | Core applicatif fonctionnel | Authentification + CRUD + smart-assign opérationnel | 31/01/2026 ✅ |
| O2 | Modèle SaaS multi-tenant | Stripe intégré, 2 plans actifs | 28/02/2026 ✅ |
| O3 | Conformité RGPD & a11y | Export portabilité, axe-core < 10 violations | 28/03/2026 ✅ |
| O4 | Déploiement (Guacamole / VM école) | Environnements dev/prod séparés | 26/04/2026 🔄 |
| O5 | Qualité & maintenabilité | Couverture tests ≥ 60 % (JaCoCo) + 70 % (Vitest), 0 vuln. critique | 20/06/2026 ✅ |
| O6 | Documentation complète | ~97 documents (Catalogue_Documentation.md) | 05/07/2026 🔄 |

---

## 6. Contraintes

| Type | Contrainte | Impact |
|---|---|---|
| **Délai** | Soutenance RNCP juillet 2026 (non négociable) | Gel des features fin juin, priorité docs |
| **Ressources** | Projet solo (1 développeur = toutes fonctions) | Pas de parallélisme équipe, arbitrages constants |
| **Infra** | VM fournies par l'école (Guacamole) pour la prod | Déploiement conditionné à la disponibilité des VM |
| **Légal** | RGPD (CNIL), WCAG 2.1 AA, OWASP Top 10 | Non-conformité = blocage soutenance |
| **Budget** | Projet pédagogique sans financement externe | Services tiers en tier gratuit/dev (Groq, Mailtrap, Stripe test) |

---

## 7. Risques principaux

| Risque | Probabilité | Impact | Mitigation |
|---|---|---|---|
| VM école non disponibles à temps | Moyen | Fort | Documentation déploiement prête ; démo sur environnement local |
| Scope creep (features vs docs) | Fort | Fort | Feature freeze acté ; phase doc prioritaire juin-juillet |
| Dépendance Groq API (LLM externe) | Faible | Moyen | Smart-assign dégradé sans LLM (scoring local seul) |
| Couverture tests insuffisante JaCoCo | Faible | Moyen | JaCoCo configuré, seuil 60 % + 10 % atteint |

---

## 8. Parties prenantes

| Rôle | Personne / Entité | Responsabilité |
|---|---|---|
| Porteur / maître d'œuvre | Pierre MICHEL | Conception, réalisation, documentation, soutenance |
| Commanditaire | Metz Numeric School | Évaluation RNCP, jury de certification |
| Utilisateurs cibles | PME / équipes projet | Validation UX, retours fonctionnels (prototype) |

---

## 9. Livrables principaux (hors code)

Documents référencés dans le [[Catalogue_Documentation|Catalogue exhaustif (~97 docs)]] ; les livrables
⭐ font partie du **bundle PDF soutenance** selon le [[Roadmap_Documentation|plan de production]].

- Note de cadrage *(ce document)* · CdCF v2 · CdCT v2 · STB · Dossier de conception · Plan de projet
- MCD/MLD/UML (Phase 0 ✅) · Dictionnaire de données ✅ · C4 ✅ · Table de réconciliation ✅
- Stratégie tests · Rapport de recette · PSSI · Plan déploiement · Registre RGPD Art. 30
- Manuel utilisateur · Mémoire RNCP + présentation PDF

> 🔗 Voir aussi : [[Dossier_Projet]] · [[01_CdCF]] · [[02_CdCT]] · [[Roadmap_Documentation]].
