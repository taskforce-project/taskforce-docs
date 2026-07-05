---
id: catalogue-documentation
title: Catalogue exhaustif de la documentation projet
doc_type: moc
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [documentation, catalogue, livrables, senior, fullstack, soutenance, pdf]
---

# 📚 Catalogue exhaustif de la documentation — TaskForce

> **But** : la liste **complète** des documents d'un projet fullstack SaaS de qualité pro (comme les
> produirait une **équipe senior** : PO, PM, architecte, back, front, data, sécu, DevOps/SRE, QA,
> designer, tech writer, juriste). Chaque doc = un **sujet traité** + **comment on le résout / ce qu'on
> met en place**. Ces docs vivent dans le **Brain OS** ; on **regroupe** ensuite ceux marqués ⭐ pour
> **export PDF soutenance**.
>
> Légende statut : ✅ existe · 🟡 partiel/à finaliser · ⬜ à créer · 🔄 **à refaire (v2)**.
> Colonne **⭐** = à inclure dans le dossier PDF de soutenance.

---

## 1. Cadrage & Produit (PO / Product Manager)

| Doc | Sujet / ce qu'on met en place | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **CdCF v2 — Cahier des Charges Fonctionnel** | Delta v1→v2, acteurs OWNER/ADMIN/MEMBER, 12 UC livrés, hors-périmètre documenté | ✅ | ⭐ | `01-projet/CdCF_v2.md` (05/07) |
| **CdCT v2 — Cahier des Charges Technique** | Delta v1→v2, stack réelle (Maven/SigNoz/Groq/pgvector), sécurité OWASP, observabilité OTEL | ✅ | ⭐ | `01-projet/CdCT_v2.md` (05/07) |
| Vision produit / PRD | Personas, objectifs SMART, features V1, métriques de succès, backlog produit | ✅ | ⭐ | `01-projet/PRD_Vision_Produit.md` (05/07) |
| Personas + user stories / epics | Collaborateur / Manager / Responsable projet | 🟡 | | `01-projet/` |
| Roadmap produit | Fait / en cours / backlog | ✅ | | `13-roadmap/Roadmap_Backlog.md` |
| Étude de marché / concurrence | Plane, Linear, Jira, Asana | ✅ | | `01-projet/Etude_business.md` |
| Business model / pricing / monétisation | Freemium 3 niveaux, unit economics, Stripe V1, concurrents, projection | ✅ | ⭐ | `01-projet/Business_Model_Pricing.md` (05/07) |
| Stratégie marketing & go-to-market | Acquisition, positionnement | ✅ | | `01-projet/Strategie_Marketing.md`, `Strategie_Vente_LLM.md` |

## 2. Gestion de projet (PM / Scrum Master)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| Note de cadrage / charte projet | Objectifs, périmètre, parties prenantes, contraintes, risques | ✅ | ⭐ | `01-projet/Note_Cadrage.md` (05/07) |
| **Planning prévisionnel** (Gantt, jalons DFS, chemin critique) | 9 phases + jalons J1–J6 (Mermaid gantt) | ✅ | ⭐ | `01-projet/Gantt_Planning.md` (05/07) |
| **Diagramme PERT** (chemin critique) | Dépendances inter-phases + marges | ✅ | ⭐ | `01-projet/Diagramme_PERT.md` (05/07) |
| **Budget prévisionnel + réel** | ~38 k€ valeur travail + 0 € infra dev + ~900 €/an prod | ✅ | ⭐ | `01-projet/Budget_Previsionnel.md` (05/07) |
| Méthodologie agile (Scrum/Kanban) + rituels | Scrum allégé + Kanban, DoD, feature freeze 20/06/2026 | ✅ | ⭐ | `01-projet/Note_Methode_Agile.md` (05/07) |
| Trame de compte-rendu + ≥1 CR | Suivi d'activité | ⬜ | | backlog optionnel |
| Matrice RACI | Rôles/responsabilités | ✅ | | `assets/diagrammes/IC-ITIL-RACI-*` |
| Organigramme | Équipe | ✅ | | `assets/diagrammes/Organigramme-*` |
| WBS / PBS / SMART | Découpage travail/produit + objectifs | ✅ | | `assets/diagrammes/{WBS,PBS,SMART}-*` |
| **Registre des risques** (matrice) | 12 risques, matrice Prob×Impact, statuts, 2 actifs | ✅ | ⭐ | `01-projet/Registre_Risques.md` (05/07) |
| Journal de décisions (ADR log) | 10 ADR : stack, multi-tenant, Keycloak, Groq Java, pgvector, STOMP, no-mock, hybride FK, Brain OS, SigNoz | ✅ | ⭐ | `12-decisions/Journal_Decisions_ADR.md` (05/07) |

## 3. Conception & Architecture (Architecte)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Dossier de conception** (E8) | Synthèse narrative Phase 0 : UC/classes/MCD/séquences/C4 + traçabilité + bilan | ✅ | ⭐ | `03-architecture/Dossier_Conception.md` (05/07) |
| **Diagramme de cas d'usage** (UML) | 3 acteurs RBAC hiérarchiques + cas gardés par le code | ✅ | ⭐ | `03-architecture/Diagramme_Cas_Usage_UML.md` (05/07) |
| **Diagramme de classes** (UML) | 38 entités JPA, 4 héritages, 60 associations + modèle hybride | ✅ | ⭐ | `03-architecture/Diagramme_Classes_UML.md` (05/07) |
| **Diagrammes de séquence** (UML) | 6 parcours réels (OTP, login, smart-assign, redistribution, Stripe, RGPD) | ✅ | ⭐ | `03-architecture/Diagrammes_Sequence_UML.md` (05/07) |
| Diagramme d'activité / états | 5 machines à états réelles (issue/invitation/cycle/abonnement) + activité | ✅ | | `03-architecture/Diagramme_Etats_UML.md` (05/07) |
| **MCD / MLD / MPD** | Modèle de données (dérivé du schéma réel — 50 tables/94 FK) | ✅ | ⭐ | `03-architecture/Modele_Donnees_MCD_MLD.md` (05/07) |
| Dictionnaire de données | 50 tables/483 colonnes/94 FK (généré d'information_schema) | ✅ | | `03-architecture/Dictionnaire_Donnees.md` (05/07) |
| Architecture logicielle (modèle **C4** : contexte/conteneurs/composants) | 3 niveaux C4 formalisés (Mermaid) | ✅ | ⭐ | `03-architecture/Architecture_C4.md` (05/07) + `Architecture.md` |
| Cartographie des modules | Découpage `shared/core/modules` | ✅ | | `03-architecture/Modules.md` |
| ADR (Architecture Decision Records) | 10 ADR fondateurs documentés (cf. §2 Gestion de projet) | ✅ | ⭐ | `12-decisions/Journal_Decisions_ADR.md` (05/07) |
| Table de réconciliation UC ↔ entité ↔ migration | ~30 UC × entités × 56 migrations × 72 tests | ✅ | | `03-architecture/Table_Reconciliation.md` (05/07) |

## 4. Back-end (Dev back-end)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Spec API (OpenAPI/Swagger)** | 33 contrôleurs / ~130 endpoints avec auth/rôle requis | ✅ | ⭐ | `05-api/Spec_API_OpenAPI.md` (05/07) |
| Fiche domaine Backend | Services, persistance, IA | 🟡 | | `02-produit/Backend.md` |
| Conventions de code back | `shared←core←modules`, `/api`, Flyway | ✅ | | `04-engineering/Conventions_Documentation.md` |
| Auth & autorisation | JWT HS512, Keycloak Admin API, RBAC, OTP, StompAuthInterceptor | ✅ | ⭐ | `07-securite/Auth_Autorisation.md` (05/07) |
| Système de paiement | Stripe : Checkout, 5 webhooks, FSM PlanStatus, portail, idempotence | ✅ | ⭐ | `04-engineering/Systeme_Paiement_Stripe.md` (05/07) |
| Gestion des erreurs / codes | `GlobalExceptionHandler`, 4xx/5xx | ⬜ | | backlog |

## 5. Front-end & Design (Dev front / Designer)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Design system / charte graphique** | Tokens CSS light/dark, palette, Inter+SF Pro, shadcn/Radix, Lucide, a11y | ✅ | ⭐ | `14-design/Design_System.md` (05/07) |
| **Wireframes annotés** | 48 routes réelles frontend, layouts annotés UC + endpoints + rôles | ✅ | ⭐ | `14-design/Wireframes_Annotes.md` (05/07) |
| Fiche domaine Frontend | Stores, services, vues, layouts | 🟡 | | `02-produit/Frontend.md` |
| Conventions front / state | Zustand, api-routes, TS strict | ✅ | | `04-engineering/` |
| **Accessibilité (RGAA/WCAG)** | Audit axe + remédiation | 🟡 | ⭐ | `14-design/Accessibilite.md` |
| i18n / traductions | FR/EN (`constants_*`) | 🟡 | | `02-produit/Frontend.md` |

## 6. Données (Data / DBA)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| Modèle de données détaillé (MCD/MLD) | *cf. §3* | ⬜ | ⭐ | à générer |
| Politique de rétention / cycle de vie | Durées, purge, anonymisation | 🟡 | | `07-securite/` + RGPD |
| **PS/PCA/PRA** (sauvegarde/reprise) | `backup.ps1`, RTO/RPO, test de reprise | ✅ | ⭐ | `11-pca-pra/PS_PCA_PRA.md` |
| Stratégie seed / migrations | Flyway + `dev_seed.sql` | 🟡 | | `03-architecture/` |

## 7. Sécurité (Security engineer)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Politique de sécurité (SSI)** + posture | Défense en profondeur, OWASP Top 10 | ✅ | ⭐ | `07-securite/Sécurité.md` |
| Analyse de menaces (threat model / STRIDE) | Surfaces d'attaque | ⬜ | | à créer |
| **Audit / pentest** (OWASP ZAP, SAST/SCA) | Résultats + remédiation | ✅ | ⭐ | `07-securite/Sécurité.md` |
| Gestion des secrets | Variables d'env, `.env`, Keycloak | 🟡 | | `06-infra/` |
| **Conformité RGPD** (registre Art.30, politique, cookies, droits) | Traçabilité des traitements | 🟡 | ⭐ | à compléter (`07-securite/` + front) |
| Plan de réponse à incident | Procédure, escalade | 🟡 | | `10-runbooks/` |

## 8. Infra / DevOps / SRE

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| Architecture d'infrastructure / topologie | Conteneurs, réseau, volumes | 🟡 | ⭐ | `06-infra/Outils_Infra_Securite.md` |
| **Diagramme de déploiement** | Hébergement (Guacamole/VM école) | ⬜ | ⭐ | à créer |
| IaC / compose (dev/prod/tools) | `docker-compose.*`, `render.yaml` | 🟡 | | `06-infra/` |
| **CI/CD pipeline** | Workflows GitHub, GHCR, release | 🟡 | ⭐ | `08-operations/DevOps.md` |
| Stratégie d'hébergement | Cloud / on-prem / VM | ⬜ | ⭐ | à créer |
| **DNS / TLS / domaine** | Certificats, reverse-proxy nginx | ⬜ | | à créer |
| **Observabilité** (logs/traces/métriques/alertes) | OTEL/SigNoz + `alerts/` | ✅ | ⭐ | `observability/alerts/README.md` |
| **Runbooks** (exploitation, incident, on-call) | Procédures d'ops | ⬜ | | `10-runbooks/` (vide) |
| Capacity planning / scaling | Estimation charge (100k users) | 🟡 | | `03-architecture/` |

## 9. Qualité & Tests (QA)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Stratégie & plan de tests** | Pyramide, couverture, outils | ✅ | ⭐ | `08-operations/Tests.md` |
| **Politique de tests** | Pyramide unitaire/composant/intégration/E2E, no-mock, gate JaCoCo 60 %/78 %, non-régression, CI | ✅ | ⭐ | `08-operations/Politique_Tests.md` (05/07) |
| **Cahier de recettes / cas de test** | 79 scénarios × UC-01→UC-12 + sécu transverse, critères d'acceptation, 97 % automatisés | ✅ | ⭐ | `08-operations/Cahier_Test_Recettes.md` (05/07) |
| Rapport de couverture | JaCoCo 78 % / Vitest 92 % | ✅ | ⭐ | `08-operations/Tests.md` |
| **Matrice de traçabilité exigences ↔ tests** | 54 exigences STB × 8 familles, 76 % automatisées, 5 gaps prioritisés | ✅ | ⭐ | `08-operations/Matrice_Tracabilite_Tests.md` (05/07) |
| **Problèmes connus + dette technique** | Triage + correctifs | ✅ | | `09-audits/{Problemes_Connus,Dette_Technique}.md` |

## 10. Utilisateur & Support (Tech writer)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Manuel utilisateur** | Prise en main (collaborateur/manager) | 🟡 | ⭐ | `15-utilisateur/Manuel_Utilisateur.md` |
| Guide d'installation | Démarrage stack | ✅ | ⭐ | `15-utilisateur/Guid_Installation.md` |
| FAQ | Questions fréquentes | 🟡 | | `15-utilisateur/FAQ.md` |
| **Release notes / CHANGELOG** | Historique versions | 🟡 | ⭐ | `15-utilisateur/Release_Notes.md` |
| Guide d'administration | Config workspace/rôles/plans | ⬜ | | à créer |

## 11. Légal & Conformité (Juriste)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Politique de confidentialité** | RGPD, données, droits | 🟡 | ⭐ | front (page) → doc |
| Politique cookies | Consentement | 🟡 | | front (bannière) → doc |
| CGU / CGV | Conditions d'utilisation/vente | ⬜ | | à créer |
| Mentions légales | Éditeur, hébergeur | ⬜ | | à créer |
| **Registre des traitements (Art. 30)** | RGPD | ⬜ | ⭐ | à créer |
| **Audit RGPD cas pro** (sujet externe) | Livrable E9 | ⬜ | ⭐ | à créer |

## 12. Veille & Innovation

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Méthodologie de veille** + ≥3 entrées | Sources, fréquence (Groq, Next, Spring Boot 4…) | ⬜ | ⭐ | à créer |
| Note d'innovation / distance critique | Éco-responsabilité, inclusion, solutions originales | 🟡 | ⭐ | à créer |

---

## 13. Synthèse — priorités & bundle PDF soutenance

### 🔄 À REFAIRE en priorité (v2 technique)
- **CdCF v2** + **CdCT v2** — refléter le vrai travail livré (fonctionnel **et** technique).

### ⬜ Gros morceaux à CRÉER
1. **Conception** : cas d'usage, **classes**, **séquence**, **MCD/MLD** (dérivables du code → je peux les générer).
2. **Gestion projet** : planning (Gantt), budget, note agile, trame CR, registre des risques formalisé.
3. **Infra/déploiement** : diagramme de déploiement, stratégie d'hébergement, DNS/TLS, runbooks.
4. **Légal/RGPD** : registre Art.30, CGU/CGV, mentions légales, audit RGPD cas pro.
5. **Veille** + note d'innovation.
6. **Consolidation** : matrice de traçabilité, ADR, changelog, manuel utilisateur.

### ⭐ Bundle PDF pour la soutenance (à regrouper)
Tous les docs marqués **⭐** ci-dessus, regroupés en un dossier ordonné :
**Cadrage** (CdCF/CdCT v2, PRD, business) → **Gestion projet** (planning, budget, agile, risques) →
**Conception** (UML, MCD/MLD, C4, dossier de conception) → **Réalisation** (API, sécurité, accessibilité,
paiement) → **Qualité** (tests, couverture, recettes) → **Prod** (déploiement, observabilité, PCA-PRA) →
**Conformité** (RGPD, légal, veille) → **Utilisateur** (manuel, installation).

> **Process** : rédiger/générer dans le Brain OS (Markdown) → export **PDF** (skill `docx`/`pdf` ou pandoc)
> des docs ⭐ → assemblage en un dossier de validation.

---

## 14. Compléments issus du référentiel école (slides C. Brasseur)

> Documents attendus par le cursus, à intégrer aux domaines ci-dessus. Sources : *Gestion de projet*,
> *Tests & recettes*, *Application security*.

### 14.1 Gestion de projet & conception
| Doc | Sujet | Statut | ⭐ |
| --- | --- | :--: | :--: |
| **Plan de projet** | Vue d'ensemble (périmètre, phases, ressources, jalons) | ⬜ | ⭐ |
| **Expression de besoin** | Besoin brut du client (amont du CdCF) | 🟡 | |
| **Analyse fonctionnelle** | Décomposition des fonctions attendues | 🟡 | ⭐ |
| **Analyse technique** | Décomposition technique des solutions | 🟡 | ⭐ |
| **STB — Spécification Technique du Besoin** | 9 familles d'exigences mesurables (perf/sécu/qualité/conformité/intégration) | ✅ | ⭐ | `01-projet/STB.md` (05/07) |
| **Diagramme de PERT** | Ordonnancement des tâches + chemin critique | ⬜ | ⭐ |
| **Rétroplanning** | Planning à rebours depuis l'échéance | ⬜ | |
| **MERISE** (MCD / MLD / MPD) | Modélisation données — **✅ fait** : `03-architecture/Modele_Donnees_MCD_MLD.md` (dérivé du schéma réel) | ✅ | ⭐ |
| **Plan de déploiement** | Procédure de mise en production | ⬜ | ⭐ |
| **Dossier d'exploitation** | Doc d'ops (démarrage, supervision, incidents) — consolide `10-runbooks/` | ⬜ | ⭐ |

### 14.2 Tests & recette
| Doc | Sujet | Statut | ⭐ |
| --- | --- | :--: | :--: |
| **Politique de tests** | Règles/normes qualité (≠ plan de tests) | ⬜ | |
| ~~PV de recette~~ (optionnel) | Procès-verbal signé par un **client** — **N/A ici** (projet solo, pas de client externe). Remplacé par un **rapport de recette / validation jury**. | ⬜ | |
| **Dossier d'anomalies** | Registre des bugs (ticketing) — recoupe `09-audits/Problemes_Connus.md` | 🟡 | |
| **Scénarios de tests + critères d'acceptation** | Cas détaillés + conditions de conformité | 🟡 | ⭐ |
| **FeatureFiles Gherkin (BDD)** | Comportements attendus (Given/When/Then) | ⬜ | |
| **Documentation vivante** | Générée par les tests automatisés | 🟡 | |
| **Matrice de traçabilité** exigences↔tests | Couverture des besoins | ⬜ | ⭐ |

### 14.3 Sécurité
| Doc | Sujet | Statut | ⭐ |
| --- | --- | :--: | :--: |
| **PSSI** (Politique de Sécurité SI) | Politique validée (DSI) | 🟡 | ⭐ |
| **Plan de sécurisation (5 étapes)** | Démarche de durcissement documentée | 🟡 | ⭐ |
| **Checklist « 10 commandements du code sécurisé »** | Bonnes pratiques codées | ⬜ | |
| **Revue de code documentée** (sécurité) | Traces des revues | 🟡 | |
| **S-SDLC** (Secure SDLC) | Sécurité intégrée au cycle de dev | 🟡 | ⭐ |
| **Configuration WAF** | Règles de pare-feu applicatif | ⬜ | |
| **Références conformité** (ISO 27034, PCI-DSS, CNIL/RGPD, ANSSI) | Cadre normatif | 🟡 | |
| **SAST / DAST / pentest** (white/black/grey-box) | Analyses statique/dynamique + intrusion | ✅ | ⭐ |

> ⚠️ **À confirmer avec les slides complets** : reveal.js charge parfois des slides en JS ; si des documents
> supplémentaires apparaissent (ex. livrables spécifiques par bloc), les ajouter ici.
