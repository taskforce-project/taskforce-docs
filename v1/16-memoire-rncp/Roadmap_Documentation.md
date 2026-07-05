---
id: roadmap-documentation
title: Roadmap de production de la documentation
doc_type: roadmap
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [roadmap, documentation, production, memoire, rncp, soutenance]
---

# 🗺️ Roadmap Documentation — plan de production

> **But** : produire **TOUS** les documents du [Catalogue exhaustif](../Catalogue_Documentation.md)
> (~97 docs), **1 par 1**, dans un **ordre efficace** (les fondations réutilisables d'abord — elles
> alimentent plusieurs docs — l'assemblage du mémoire à la fin).
>
> **Légende** : `[ ]` à produire · `[~]` en cours · `[x]` fait. ✅ = déjà existant/couvert dans le Brain OS.
> ⭐ = va dans le **bundle PDF soutenance**. Croisé avec le **référentiel DFS** (E1–E29) + slides école.
>
> **Process par doc** : (1) rédiger/générer en Markdown dans le Brain OS → (2) lier aux preuves (code,
> captures, autres docs) → (3) cocher ici + statut dans le [Catalogue](../Catalogue_Documentation.md) →
> (4) MAJ du [mémoire](./README.md) si preuve d'une compétence.

---

## Phase 0 — Fondations réutilisables (GÉNÉRABLES DU CODE) 🏗️ ✅ **TERMINÉE (05/07)**
> À faire **en premier** : ces artefacts sont réutilisés dans le CdCT, le dossier de conception, le mémoire.
> **8/8 faits** — tous dérivés du code/schéma réel (`03-architecture/`), aucune donnée inventée.

- [x] ⭐ **MERISE — MCD / MLD** — **fait (05/07)** : `03-architecture/Modele_Donnees_MCD_MLD.md` (7 diagrammes Mermaid par domaine, dérivés du schéma réel `information_schema` — 50 tables/94 FK — + règles de gestion justifiées). MPD = PostgreSQL 18 + pgvector.
- [x] ⭐ **Diagramme de classes (UML)** — **fait (05/07)** : `03-architecture/Diagramme_Classes_UML.md` (5 diagrammes Mermaid par domaine, dérivés des 38 entités JPA réelles — 4 héritages `AuditableEntity`, 60 associations `@ManyToOne` ; documente le **modèle hybride** association JPA vs FK par `Long` id, justifié par le Javadoc `AuditLog`).
- [x] ⭐ **Diagramme de cas d'usage (UML)** — **fait (05/07)** : `03-architecture/Diagramme_Cas_Usage_UML.md` (3 acteurs hiérarchiques MEMBER⊂ADMIN⊂OWNER + Stripe/Ordonnanceur, cas gardés par le code `AuthorizationService`/`assertIsOwner` ; cœur CDC = redistribution auto tracé).
- [x] ⭐ **Diagrammes de séquence (UML)** — **fait (05/07)** : `03-architecture/Diagrammes_Sequence_UML.md` (6 séquences réelles : inscription+OTP, login Keycloak, smart-assign, redistribution, Stripe checkout/webhooks, export RGPD — chaque flèche = appel présent dans le code).
- [x] **Diagramme d'activité / d'états** — **fait (05/07)** : `03-architecture/Diagramme_Etats_UML.md` (5 machines à états réelles : issue/invitation/cycle/abonnement + activité redistribution ; documente l'absence de contrainte de transition sur les issues et l'absence de statut workspace).
- [x] **Dictionnaire de données** — **fait (05/07)** : `03-architecture/Dictionnaire_Donnees.md` (exhaustif, généré d'`information_schema` — 50 tables/483 colonnes/94 FK, avec types/nullable/défauts/clés/ON DELETE, groupé par domaine).
- [x] ⭐ **Architecture C4** (contexte → conteneurs → composants) — **fait (05/07)** : `03-architecture/Architecture_C4.md` (3 niveaux Mermaid dérivés de `Architecture.md`/`ARCHITECTURE.md` ; ai-service marqué vestigial DT-010, règle `shared←core←modules`).
- [x] **Table de réconciliation** UC ↔ entité ↔ migration ↔ test — **fait (05/07)** : `03-architecture/Table_Reconciliation.md` (matrice de traçabilité complète : ~30 UC × entités × 56 migrations Flyway × 72 fichiers de tests + cas transverses sécu/qualité).

## Phase 1 — Cadrage & Produit 📌 ✅ **TERMINÉE (05/07)**
- [x] ⭐ **Note de cadrage** — **fait (05/07)** : `01-projet/Note_Cadrage.md` (origine/problématique/périmètre/SMART/contraintes/risques/parties prenantes — synthèse fondée sur `Dossier_Projet.md`).
- [x] 🔄 ⭐ **CdCF v2** — **fait (05/07)** : `01-projet/CdCF_v2.md` (périmètre réel livré : delta v1→v2, acteurs OWNER/ADMIN/MEMBER, 12 UC mis à jour, 3 scénarios, hors-périmètre V1 documenté).
- [x] 🔄 ⭐ **CdCT v2** — **fait (05/07)** : `01-projet/CdCT_v2.md` (delta v1→v2, stack réelle Maven/SigNoz/Groq/pgvector, architecture packages, modèle de données, infra, sécurité OWASP, tests, observabilité OTEL→SigNoz).
- [x] ⭐ **STB** — **fait (05/07)** : `01-projet/STB.md` (9 familles d'exigences : perf/capacité/dispo/sécu/qualité/conformité/intégration/contraintes/traçabilité — toutes fondées sur le code ou les configs réels).
- [ ] **Expression de besoin** + **Analyse fonctionnelle** + **Analyse technique**
- [x] ⭐ **PRD / Vision produit** — **fait (05/07)** : `01-projet/PRD_Vision_Produit.md` (personas, objectifs SMART, features V1, métriques de succès, backlog produit).
- [x] ⭐ **Business model / pricing / monétisation** — **fait (05/07)** : `01-projet/Business_Model_Pricing.md` (freemium 3 niveaux FREE/PRO/Enterprise, unit economics CAC/LTV, Stripe V1 implémenté, concurrents, projection).
- [ ] Personas + user stories / epics
- ✅ Roadmap produit · Étude de marché · Stratégie marketing/vente

## Phase 2 — Gestion de projet 📊
- [x] ⭐ **Plan de projet** — **fait (05/07)** : `01-projet/Plan_Projet.md` (phases/jalons/MoSCoW/organisation/outils).
- [x] ⭐ **Planning prévisionnel (Gantt)** — **fait (05/07)** : `01-projet/Gantt_Planning.md` (Mermaid gantt 9 phases + jalons J1–J6).
- [x] ⭐ **Diagramme de PERT** — **fait (05/07)** : `01-projet/Diagramme_PERT.md` (dépendances + chemin critique + marges).
- [ ] **Rétroplanning** — ⬜ backlog (optionnel soutenance)
- [x] ⭐ **Budget prévisionnel + réel** — **fait (05/07)** : `01-projet/Budget_Previsionnel.md` (~38 k€ valeur travail + 0 € infra dev + ~900 €/an prod).
- [x] ⭐ **Note méthode agile** — **fait (05/07)** : `01-projet/Note_Methode_Agile.md` (Scrum allégé + Kanban, DoD, feature freeze).
- [ ] **Trame de compte-rendu** + ≥1 CR d'exemple — ⬜ backlog (optionnel)
- [x] ⭐ **Registre des risques** — **fait (05/07)** : `01-projet/Registre_Risques.md` (12 risques, matrice Prob×Impact, statuts).
- [x] ⭐ **Journal de décisions (ADR)** — **fait (05/07)** : `12-decisions/Journal_Decisions_ADR.md` (10 ADR : stack Maven, multi-tenant, Keycloak, Groq Java, pgvector, RabbitMQ/STOMP, no-mock Testcontainers, hybride FK, Brain OS @OneToOne, SigNoz/OTEL).
- ✅ RACI · Organigramme · WBS · PBS · SMART

## Phase 3 — Conception (assemblage) 🧩 ✅ **TERMINÉE (05/07)**
- [x] ⭐ **Dossier de conception** (E8) — **fait (05/07)** : `03-architecture/Dossier_Conception.md` (synthèse narrative Phase 0 : UC/classes/MCD/séquences/C4/ADR + traçabilité exigences→conception + bilan gaps).
- [x] ⭐ **Wireframes annotés** — **fait (05/07)** : `14-design/Wireframes_Annotes.md` (dérivés des 48 routes réelles `frontend/app/**/page.tsx` + layouts ASCII annotés UC + endpoints + rôles requis).

## Phase 4 — Réalisation (documentation) 🛠️ ✅ **TERMINÉE (05/07)**
- [x] ⭐ **Spec API OpenAPI/Swagger** — **fait (05/07)** : `05-api/Spec_API_OpenAPI.md` (33 contrôleurs / ~130 endpoints, groupés par domaine, avec auth/rôle requis par endpoint).
- [x] ⭐ **Auth & autorisation** — **fait (05/07)** : `07-securite/Auth_Autorisation.md` (JWT HS512 custom via JwtService, Keycloak comme référentiel identité, 3 chaînes SecurityFilterChain, RBAC OWNER/ADMIN/MEMBER, OTP inscription, StompAuthInterceptor).
- [x] ⭐ **Système de paiement** — **fait (05/07)** : `04-engineering/Systeme_Paiement_Stripe.md` (Checkout, 5 webhooks, FSM PlanStatus, portail billing, idempotence stripe_event_id, variables d'env).
- [ ] Gestion des erreurs / codes — ⬜ backlog (GlobalExceptionHandler documenté dans CdCT v2)
- [x] ⭐ **Design system / charte graphique** — **fait (05/07)** : `14-design/Design_System.md` (tokens CSS globals.css, palette light/dark, shadcn/Radix composants, Inter + SF Pro, Lucide icons, a11y).
- [ ] i18n / traductions — ⬜ backlog (FR/EN constants documentés dans CdCT v2)
- ✅ Accessibilité (`14-design/Accessibilite.md`) · Conventions front/back · Fiches Backend/Frontend (à finaliser 🟡)

## Phase 5 — Qualité & Tests ✅ **TERMINÉE (05/07)**
- [x] ⭐ **Politique de tests** — **fait (05/07)** : `08-operations/Politique_Tests.md` (pyramide unitaire/composant/intégration/E2E, no-mock Testcontainers ADR-007, gate JaCoCo 60 % / actuel 78 %, frontend 92 % Vitest, règles non-régression, CI 3 workflows).
- [x] ⭐ **Cahier de recettes** — **fait (05/07)** : `08-operations/Cahier_Test_Recettes.md` (79 scénarios × UC-01 à UC-12 + cas transverses sécu — critères d'acceptation, fichiers de test tracés, 97 % automatisés).
- [x] ⭐ **Matrice de traçabilité** exigences ↔ tests — **fait (05/07)** : `08-operations/Matrice_Tracabilite_Tests.md` (54 exigences STB × 8 familles PERF/CAP/DISP/SEC/QUAL/CONF/INT/CT — 76 % couvertes automatiquement, 5 gaps prioritisés).
- [ ] **FeatureFiles Gherkin (BDD)** + documentation vivante
- [ ] **Rapport de recette / validation jury** (remplace le PV client — N/A projet solo)
- ✅ Stratégie & plan de tests (`Tests.md`) · Rapport de couverture (78/92 %) · Dossier d'anomalies (`Problemes_Connus.md`)

## Phase 6 — Sécurité 🔐 ✅ **TERMINÉE (05/07)**
- [x] ⭐ **PSSI** — **fait (05/07)** : `07-securite/PSSI.md` (DICP, 6 principes directeurs, IAM/RBAC, protection données + RGPD, couverture OWASP, journalisation/audit, rôles & responsabilités, gestion vulnérabilités — chaque règle ancrée dans le code réel).
- [x] ⭐ **Plan de sécurisation (5 étapes)** + **S-SDLC** — **fait (05/07)** : `07-securite/Plan_Securisation_SSDLC.md` (S-SDLC 6 étapes conception→exploitation, plan 5 étapes cartographie→vérification, outillage DevSecOps Semgrep/Trivy/ZAP, checklist « 10 commandements », revue de code sécu).
- [x] **Threat model (STRIDE)** — **fait (05/07)** : `07-securite/Threat_Model_STRIDE.md` (DFD + 4 gardes, 6 catégories STRIDE × flux réels avec preuves code, synthèse risques résiduels tracés au backlog, couverture STRIDE↔OWASP↔tests). Documente TF-SEC-007.
- [x] Gestion des secrets · Références conformité — **couvert** dans PSSI §3.3 + §5 (ISO 27034/OWASP ASVS L1). Config WAF → renvoyée Phase 7 (infra).
- ✅ Politique de sécurité + posture OWASP (`Sécurité.md`) · Pentest ZAP/SAST/SCA · Plan réponse incident (🟡)

## Phase 7 — Infra / DevOps / Prod 🚀
- [ ] ⭐ **Architecture d'infrastructure / topologie**
- [ ] ⭐ **Diagramme de déploiement** (E21)
- [ ] ⭐ **Stratégie d'hébergement** (Guacamole / VM école)
- [ ] **DNS / TLS / domaine + certificats** (E23)
- [ ] ⭐ **Plan de déploiement** (procédure MEP) + **CI/CD pipeline**
- [ ] ⭐ **Runbooks / Dossier d'exploitation** (`10-runbooks/` — vide)
- [ ] Capacity planning / scaling
- ✅ Observabilité + alertes (`observability/alerts/`) · PCA/PRA (`PS_PCA_PRA.md`)
> ⚠️ Plusieurs items dépendent des **VM de l'école** (à préparer).

## Phase 8 — Conformité & Légal ⚖️
- [ ] ⭐ **Registre des traitements (Art. 30 RGPD)**
- [ ] ⭐ **Audit RGPD cas pro** (sujet externe imposé — E9)
- [ ] **Politique de confidentialité** (doc, depuis la page front) · **Politique cookies**
- [ ] **CGU / CGV** · **Mentions légales**

## Phase 9 — Utilisateur & Support 👥
- [ ] ⭐ **Manuel utilisateur** (finaliser)
- [ ] **FAQ** · **Guide d'administration**
- [ ] ⭐ **Release notes / CHANGELOG** (E29, consolider)
- ✅ Guide d'installation

## Phase 10 — Veille & Innovation 🔭
- [ ] ⭐ **Méthodologie de veille** + ≥3 entrées tracées (Groq, Next, Spring Boot 4…)
- [ ] ⭐ **Note d'innovation / distance critique** (éco-responsabilité, inclusion, solutions originales)

## Phase 11 — Assemblage du dossier de validation 🎓
- [ ] **Rédaction narrative** des 4 Blocs (`Bloc1..4`) — assembler les preuves par compétence
- [ ] **Tableau d'équivalences** compétence ↔ partie du dossier (matrice `README.md` — maintenir à jour)
- [ ] ⭐ **Présentation de synthèse (diapositives) au format PDF** (annexe obligatoire)
- [ ] **Export & regroupement du bundle PDF** (tous les ⭐, ordre : Cadrage → Gestion → Conception → Réalisation → Qualité → Prod → Conformité → Utilisateur)

---

## Séquencement conseillé
**0 → 1 → 3 → 2** (fondations, puis cadrage, puis conception qui les assemble, puis gestion de projet en parallèle),
puis **4/5/6/7** (réalisation/qualité/sécu/prod — beaucoup déjà couverts), **8/9/10** (conformité/user/veille),
et enfin **11** (assemblage + PDF). Le **déploiement (Phase 7)** attend les VM.

> Estimation : ~20–25 documents **à créer** (⬜) + ~15 à **finaliser** (🟡) + 2 à **refaire** (CdCF/CdCT v2).
> Le reste (~30) est **déjà couvert**. On coche ici au fur et à mesure.
