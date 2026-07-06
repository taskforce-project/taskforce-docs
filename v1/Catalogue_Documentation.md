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
| Auth & autorisation | OIDC RS256 (Keycloak), Admin API, RBAC, OTP, StompAuthInterceptor | ✅ | ⭐ | `07-securite/Auth_Autorisation.md` (v1.1, OIDC) |
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
| **PSSI (Politique de Sécurité SI)** | DICP, principes directeurs, IAM/RBAC, protection données, OWASP, audit, rôles, gestion vulnérabilités | ✅ | ⭐ | `07-securite/PSSI.md` (05/07) |
| **Plan de sécurisation (5 étapes) + S-SDLC** | Cycle de vie sécurisé 6 étapes, plan 5 étapes, DevSecOps, checklist 10 commandements | ✅ | ⭐ | `07-securite/Plan_Securisation_SSDLC.md` (05/07) |
| **Analyse de menaces (threat model / STRIDE)** | DFD + 4 gardes, 6 catégories STRIDE × flux réels + preuves, risques résiduels | ✅ | ⭐ | `07-securite/Threat_Model_STRIDE.md` (05/07) |
| **Audit / pentest** (OWASP ZAP, SAST/SCA) | Résultats + remédiation | ✅ | ⭐ | `07-securite/Sécurité.md` |
| Gestion des secrets | Variables d'env, `.env`, Keycloak | 🟡 | | `06-infra/` |
| **Conformité RGPD** (registre Art.30, politique, cookies, droits) | Traçabilité des traitements | 🟡 | ⭐ | à compléter (`07-securite/` + front) |
| Plan de réponse à incident | Procédure, escalade | 🟡 | | `10-runbooks/` |

## 8. Infra / DevOps / SRE

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| Architecture d'infrastructure / topologie | Conteneurs, réseau, volumes | 🟡 | ⭐ | `06-infra/Outils_Infra_Securite.md` — dépend choix hébergement |
| **Diagramme de déploiement** (E21) | Hébergement (Guacamole/VM école ou Render) | ⬜ | ⭐ | à créer — dépend choix hébergement |
| IaC / compose (dev/prod/tools) | `docker-compose.*`, `render.yaml` | ✅ | | `docker-compose.{yml,dev,prod,tools}.yml` + `render.yaml` |
| **CI/CD pipeline** | 7 workflows GitHub Actions : tests, release, versioning SemVer indépendant, images GHCR | ✅ | ⭐ | `08-operations/Pipeline_CICD.md` (05/07) |
| **Stratégie d'hébergement** | Option A : VM école + docker-compose.prod · Option B : Render · décision pendante | ✅ | ⭐ | `06-infra/Strategie_Hebergement.md` (05/07) |
| **DNS / TLS / domaine** | Certificats, reverse-proxy nginx | ⬜ | | à créer — dépend choix hébergement |
| **Observabilité** (logs/traces/métriques/alertes) | OTel→SigNoz→ClickHouse, 5 pipelines, 9 alertes Prometheus | ✅ | ⭐ | `06-infra/Observabilite.md` (05/07) |
| **Runbooks** (exploitation, incident, on-call) | Procédures d'ops | ⬜ | | `10-runbooks/` (vide) — TF-INFRA-009 |
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
| **Manuel utilisateur** | 12 sections UC-01→12 : inscription/OTP, RBAC, workspaces, projets, issues/Kanban, Smart Assign, cycles, pages, chat STOMP, Stripe, RGPD | ✅ | ⭐ | `15-utilisateur/Manuel_Utilisateur.md` (05/07) |
| Guide d'installation | Démarrage stack Docker Compose | ✅ | ⭐ | `15-utilisateur/Guid_Installation.md` |
| **FAQ** | 6 thèmes : compte, tâches/IA, collaboration, facturation, données/RGPD, techniques | ✅ | | `15-utilisateur/FAQ.md` (05/07) |
| **Release notes / CHANGELOG** (E29) | V1.0.0 soutenance RNCP — 15 catégories features, git history Oct 2025→Jul 2026, backlog prioritaire | ✅ | ⭐ | `15-utilisateur/Release_Notes.md` (05/07) |
| Guide d'administration | Config workspace/rôles/plans (ADMIN/OWNER) | ⬜ | | backlog |

## 11. Légal & Conformité (Juriste)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Registre des traitements (Art. 30)** | 7 traitements RGPD documentés avec base légale, sous-traitants, droits | ✅ | ⭐ | `07-securite/Registre_Traitements_RGPD.md` (05/07) |
| **Audit RGPD conformité** (E9) | Analyse conformité ~75%, droits personnes, Privacy by Design, 9 gaps tracés | ✅ | ⭐ | `07-securite/Audit_RGPD_Conformite.md` (05/07) |
| **Politique de confidentialité + CGU** | Pages réelles landing (`PrivacyPolicyPageNew.tsx`, `TermsPageNew.tsx`) + analyse cohérence code↔politique + gaps légaux | ✅ | ⭐ | `07-securite/Politique_Confidentialite_CGU.md` (05/07) |
| Politique cookies | Décrite dans Privacy Policy, pas de bannière interactive implémentée | 🟡 | | TF-RGPD-001 |
| Mentions légales | Email contact présent (legal@taskforce.app), page dédiée LEN Art. 6 absente | 🟡 | | TF-RGPD-005 |

## 12. Veille & Innovation

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Méthodologie de veille + 6 entrées tracées** | Sources/fréquence/processus, 6 entrées VT-001→006 (Spring Boot 4, Groq, pgvector HNSW, SigNoz, OWASP/CNIL, Next.js) avec ADR + preuves code | ✅ | ⭐ | `17-veille/Veille_Technologique.md` (05/07) |
| **Note d'innovation & distance critique** | 3 innovations (Smart Assign, Brain OS, observabilité sécu) · 5 distances critiques · éco-responsabilité · inclusion/a11y | ✅ | ⭐ | `17-veille/Note_Innovation_Distance_Critique.md` (05/07) |

## 13. Mémoire RNCP — Dossier de validation (32 compétences)

| Doc | Sujet | Statut | ⭐ | Emplacement |
| --- | --- | :--: | :--: | --- |
| **Bloc 1 — Concevoir et modéliser** | C1–C12 : analyse demande, agile, env dev, wireframes, STB, modélisation, RGPD, veille — preuves réelles + critères cochés | ✅ | ⭐ | `16-memoire-rncp/Bloc1_Conception_Modelisation.md` (05/07) |
| **Bloc 2 — Front-end** | C13–C20 : UI/UX/charte, parcours, qualité code front, API sécurisée, 92% Vitest, CI, SEO (Astro) | ✅ | ⭐ | `16-memoire-rncp/Bloc2_Frontend.md` (05/07) |
| **Bloc 3 — Back-end** | C21–C26 : persistance sécurité-en-profondeur, Spring Boot 4 Virtual Threads, Stripe, API sécurisée OpenAPI, 78% JaCoCo, Trivy/ZAP | ✅ | ⭐ | `16-memoire-rncp/Bloc3_Backend.md` (05/07) |
| **Bloc 4 — Déploiement & production** | C27–C32 : documentation auto-générée, nginx/TLS/DNS, hébergement (Option A VM + B Render), Docker, 7 workflows CI/CD, OTel→SigNoz 9 alertes, audit/backup/ZAP | ✅ | ⭐ | `16-memoire-rncp/Bloc4_Deploiement_Production.md` (05/07) |
| **Matrice de couverture 32 compétences** | C1–C32 statuts ✅/🟡/⬜ avec liens vers preuves | ✅ | ⭐ | `16-memoire-rncp/README.md` (05/07) |
| **Présentation de synthèse (slides PDF)** | Diapositives soutenance — annexe obligatoire dossier RNCP | ⬜ | ⭐ | à produire |

---

## 15. Synthèse — priorités & bundle PDF soutenance

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

## 16. Compléments issus du référentiel école (slides C. Brasseur)

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
