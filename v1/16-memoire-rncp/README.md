---
type: memoire-rncp
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, dossier-validation, dfs, brain-os]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# 🎓 Mémoire RNCP — Dossier de Validation

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]() [![Titre: Développeur Full Stack](https://img.shields.io/badge/Titre-D%C3%A9veloppeur%20Full%20Stack-blue?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Bloc 1 — Conception & modélisation](./Bloc1_Conception_Modelisation.md)
- [Bloc 2 — Front-end](./Bloc2_Frontend.md)
- [Bloc 3 — Back-end](./Bloc3_Backend.md)
- [Bloc 4 — Déploiement & production](./Bloc4_Deploiement_Production.md)
- 📚 **[Catalogue exhaustif de la documentation](../Catalogue_Documentation.md)** · 🗺️ **[Roadmap Documentation](./Roadmap_Documentation.md)** · 📝 [Stratégie de documentation](./Strategie_Documentation.md)
- [CDC initial](../01-projet/Dossier_Projet.md) · [Architecture technique](../03-architecture/Architecture.md)

**Tags :** `#memoire` `#rncp` `#dossier-validation` `#dfs`

<p class="lead">
Ce dossier est le <strong>mémoire de validation</strong> du titre <em>Développeur Full Stack</em> (RNCP,
Metz Numeric School 2025-2026), adossé au projet fil rouge <strong>TaskForce</strong>. Sa table des
matières <strong>colle volontairement à la structure du référentiel</strong> (blocs → activités →
compétences C1–C32), comme recommandé, afin que chaque compétence évaluée soit traçable et qu'aucun
critère de la grille ne soit oublié.
</p>

> **Comment l'utiliser** — La [matrice de couverture](#3-matrice-de-couverture-des-32-compétences) est ta
> checklist maître : tant qu'une ligne n'est pas ✅, le dossier n'est pas complet. Chaque compétence renvoie
> à sa section détaillée (critères + preuves) et à l'emplacement de la preuve dans TaskForce (via le
> [Brain OS](../../Brain_OS.md)).

## Table des matières

1. [Modalités d'évaluation](#1-modalités-dévaluation)
2. [Livrables attendus (E1–E29)](#2-livrables-attendus-e1e29)
3. [Matrice de couverture des 32 compétences](#3-matrice-de-couverture-des-32-compétences)
4. [Conventions de rédaction](#4-conventions-de-rédaction)

---

## 1. Modalités d'évaluation

<p class="lead">
Le titre se valide par trois modalités complémentaires. Le présent dossier alimente principalement la
première et appuie la deuxième.
</p>

| Modalité | Description | Blocs concernés |
| -------- | ----------- | --------------- |
| **Dossier de validation** | Ensemble des livrables (E1–E29) du projet fil rouge + réflexion personnelle (solutions originales, analyse, préconisations). Remis au jury, évalué à l'écrit et en soutenance. | 1 à 4 |
| **Soutenance** | Démonstration de l'application : partie front-end (bloc 2) + partie back-end (bloc 3). Présentation de synthèse PDF + prototype/démo/code. | 2 et 3 |
| **Mise en situation simulée** | Maintenance écrite et surveillée d'une application existante (bugs, failles, composants obsolètes). | 4 (+ C11 cas pro RGPD) |

<blockquote class="important">
<strong>Recommandation du référentiel :</strong> coller la table des matières à la structure en blocs et
activités. Ce dossier la respecte ; la <a href="#3-matrice-de-couverture-des-32-compétences">matrice</a>
joue en plus le rôle de « tableau d'équivalences » compétence ↔ partie du dossier.
</blockquote>

## 2. Livrables attendus (E1–E29)

Synthèse des livrables exigés par le référentiel, regroupés par bloc. Détail et critères dans chaque fiche bloc.

- **Bloc 1 :** E1 reformulation de la demande · E2 planification + budget prévisionnels · E3 note de
  préconisations techniques · E4 procédure d'environnement de dev · E5 note justifiant la méthode agile ·
  E6 trame de compte rendu d'activité · E7 maquette wireframe · E8 dossier de conception (cas d'usage,
  classes, MCD, archi logicielle) · E9 audit RGPD (cas pro hors fil rouge) · E10 méthodologie de veille.
- **Bloc 2 :** E11 développement intégral du front-end · E12 consommation d'une API tierce · E13 plan de
  tests front + exécution · E14 industrialisation front (QA, dépendances, build).
- **Bloc 3 :** E15 couche de persistance · E16 développement intégral du back-end · E17 système de
  paiement + monétisation · E18 API sécurisée · E19 plan de tests back · E20 industrialisation back.
- **Bloc 4 :** E21 choix d'hébergement cloud + diagramme de déploiement · E22 environnement de production
  sécurisé · E23 nom de domaine + DNS + certificats · E24 déploiement automatisé · E25 journalisation/audit ·
  E26 supervision + alertes · E27 détection de bugs + correctifs · E28 détection de failles + correctifs ·
  E29 génération de doc + changelog.

## 3. Matrice de couverture des 32 compétences

<p class="lead">
Légende statut : ✅ couvert (preuve prête) · 🟡 partiel (preuve existe, à formaliser) · ⬜ à produire.
Le statut initial ci-dessous est une <strong>estimation</strong> basée sur l'état du code (Brain OS) ; à
ajuster au fil de la rédaction.
</p>

> **▶ RÉCONCILIATION DU 23/07/2026 — à lire avant le tableau.** Les chiffres ci-dessous remplacent
> **tous** ceux qui circulaient dans le corpus. Trois jeux de valeurs différents coexistaient (92/78,
> puis 92,33/71,3, puis les valeurs mesurées cette semaine), ce qui faisait que deux pages du dossier
> se contredisaient. Une seule mesure fait désormais foi, avec sa date et son périmètre.
>
> | Indicateur | Valeur retenue | Mesuré le |
> |---|---|---|
> | Couverture front | **89,55 % de lignes** sur le périmètre logique (`lib`, `hooks`, `components/auth`) | 23/07/2026 |
> | Suite front | **805 tests / 63 fichiers**, 0 échec | 23/07/2026 |
> | Couverture back | **73,71 % de lignes** (JaCoCo) | 22/07/2026 |
> | Suite back | **792 tests**, 0 échec | 23/07/2026 |
>
> Une réserve à porter avec le chiffre front, plutôt qu'à taire : le périmètre **exclut** les 48
> routes et les composants de présentation, couverts par Playwright. À annoncer avant qu'on le
> demande, sans quoi le chiffre se lit comme une couverture globale du front, ce qu'il n'est pas.
>
> La mesure **sort désormais en code 0**, tous seuils par chemin compris. Elle échouait encore le
> matin du 23/07 sur `lib/utils` (71,01 % pour 72 % attendus), faute de test sur l'export CSV :
> 20 tests paramétrés ont été écrits, portant ce module à 93,23 % de lignes.
>
> **▶ État au 05/07/2026 (les statuts du tableau datent du 08/06).**
> - **C21/C24 sécurité 🟢** : en-têtes durcis **testés** (OWASP A05), IDOR fermés (`AuthorizationService`), chiffrement PII (AES-256-GCM). RGPD **de TaskForce** (audit + export/effacement) livré & validé — ⚠️ distinct de **C11/E9** (audit RGPD d'un **cas pro externe**, toujours ⬜).
> - **C28/E28 détection de failles ✅** : pentest **OWASP ZAP** (0 HIGH, 4 MEDIUM CSP dev) + SAST Semgrep + SCA/images Trivy (`scripts/security-scan.ps1`).
> - **C32/E25 journalisation ✅** : **audit backend** (`AuditLog`, 7 events) + **observabilité OTEL → SigNoz** + **logs front → serveur** (`ClientLogController` + `client-logger.ts`, 05/07) + **PS/PCA-PRA opérationnel testé** (`scripts/backup.ps1`). **E26 supervision ✅** : sondes actuator `health`/`prometheus` (corrigé : registry manquant) + OTEL→SigNoz + **9 règles d'alerte** (`observability/alerts/`, format Prometheus portable).
> - **Reste prioritaire** : conception formalisée (C6 wireframes, C7/C8 UML/MCD/MLD, cas d'usage), **C11/E9 RGPD cas pro**, **C12/E10 veille**, **C20 SEO landing**, **Bloc 4** (C28–C31 déploiement : hébergement, DNS/TLS, prod sécurisée), gestion projet (E1–E6). CI (C19/C26 gates bloquants) reportée.

### Bloc 1 — Concevoir et modéliser

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C1 | Analyser la demande initiale | E1 | [CdCF v1.1](../01-projet/01_CdCF.md), [Dossier Projet](../01-projet/Dossier_Projet.md), [Bloc1 §C1](./Bloc1_Conception_Modelisation.md) | ✅ |
| C2 | Conseil / expertise sur le CdCF | E1, E3 | [Note Innovation](../17-veille/Note_Innovation_Distance_Critique.md), [ADR](../08-decisions/Journal_Decisions_ADR.md), [Bloc1 §C2](./Bloc1_Conception_Modelisation.md) | ✅ |
| C3 | Caractéristiques projet (public, SEO, sécu, délais, budget) | E2 | [Budget](../01-projet/Budget_Previsionnel.md), [Gantt](../01-projet/Gantt_Planning.md), [Registre Risques](../01-projet/Registre_Risques.md), [Bloc1 §C3](./Bloc1_Conception_Modelisation.md) | ✅ |
| C4 | Travailler en agile | E5, E6 | [Note Agile](../01-projet/Note_Methode_Agile.md), [Git Workflow](../04-engineering/git-workflow/README.md), app TaskForce (Cycles), [Bloc1 §C4](./Bloc1_Conception_Modelisation.md) | ✅ |
| C5 | Environnement de dev collaboratif | E4 | [Quickstart](../06-infra/quickstart/README.md), [GHCR](../06-infra/docker/GHCR_USAGE.md), `docker-compose.dev.yml`, [Bloc1 §C5](./Bloc1_Conception_Modelisation.md) | ✅ |
| C6 | Maquettes wireframe | E7 | `assets/maquettes/`, [Wireframes annotés](../14-design/Wireframes_Annotes.md), [Bloc1 §C6](./Bloc1_Conception_Modelisation.md) | ✅ |
| C7 | STB → dossier de conception | E8 | [Dossier Conception](../03-architecture/Dossier_Conception.md), [CdCT v2](../01-projet/CdCT_v2.md), [Diag. UC](../03-architecture/Diagramme_Cas_Usage_UML.md), [Bloc1 §C7](./Bloc1_Conception_Modelisation.md) | ✅ |
| C8 | Modélisation (entité-association, classes) | E8 | [MCD/MLD](../03-architecture/Modele_Donnees_MCD_MLD.md), [Diag. Classes](../03-architecture/Diagramme_Classes_UML.md), [Bloc1 §C8](./Bloc1_Conception_Modelisation.md) | ✅ |
| C9 | Architecture des bases de données / persistance | E8 | [Architecture C4](../03-architecture/Architecture_C4.md), [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md), Flyway V1–V53, [Bloc1 §C9](./Bloc1_Conception_Modelisation.md) | ✅ |
| C10 | Architecture logicielle | E8 | [Architecture C4](../03-architecture/Architecture_C4.md), [Modules](../03-architecture/Modules.md), [Bloc1 §C10](./Bloc1_Conception_Modelisation.md) | ✅ |
| C11 | Conformité RGPD / CNIL | **E9 ⬜** | ⚠️ **Compétence NON acquise, et l'erreur inverse a été commise le 23/07.** Le référentiel (p. 8) rattache C11 à un « cas professionnel individuel écrit **hors projet fil rouge** », à partir d'« un site web marchand existant **fourni** ». Les 4 critères (consentement cookies, vue de confidentialité, formulaire d'accès, double opt-in) s'évaluent donc sur **ce site**, pas sur TaskForce. Ils avaient été cochés au vert sur la foi de l'implémentation TaskForce : corrigé. Le RGPD de TaskForce reste une preuve de **capacité** réelle ([Audit](../07-securite/Audit_RGPD_Conformite.md), [Registre Art.30](../07-securite/Registre_Traitements_RGPD.md), `GdprService`, `RetentionScheduler`, double opt-in) mais **ne se substitue pas au livrable**. Sujet à réclamer à l'école | ⬜ |
| C12 | Veille technologique | E10 | [Veille Technologique](../17-veille/Veille_Technologique.md) (VT-001→006 avec ADR + preuves code), [Bloc1 §C12](./Bloc1_Conception_Modelisation.md) | ✅ |

### Bloc 2 — Front-end

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C13 | Concevoir l'interface utilisateur | E11 | `frontend/app/`, Radix/shadcn ARIA natif, axe-core CI, [Bloc2 §C13](./Bloc2_Frontend.md) | ✅ |
| C14 | Éléments graphiques / charte | E11 | [Design System](../14-design/Design_System.md), `globals.css`, logos `assets/images/`, [Bloc2 §C14](./Bloc2_Frontend.md) | ✅ |
| C15 | Mettre en œuvre l'UX (parcours, accessibilité) | E11 | 12 UC couverts, App Router. **WCAG 2.1 AA vérifié le 22/07 : 0 violation axe-core sur 3 pages, tous impacts confondus.** Le test ne bloquait auparavant que sur `critical` alors que les manquements AA remontent en `serious` : 10 violations passaient inaperçues, corrigées depuis, [Bloc2 §C15](./Bloc2_Frontend.md) | ✅ |
| C16 | Langage front (qualité, sécurité, écoconception) | E11 | ESLint, TypeScript strict, CSP/CORS/HSTS headers, React Compiler, [Bloc2 §C16](./Bloc2_Frontend.md) | ✅ |
| C17 | Consommer une API de façon sécurisée | E12 | `client.ts` (Axios+JWT+refresh), Stripe redirect, STOMP+auth, [Bloc2 §C17](./Bloc2_Frontend.md) | ✅ |
| C18 | Tester le front-end (couverture ≥ 50 %) | E13 | **89,55 % Vitest** (périmètre logique), 805 tests, 3 fichiers Playwright, [Bloc2 §C18](./Bloc2_Frontend.md) | ✅ |
| C19 | Industrialiser le front-end | E14 | `frontend-tests.yml`, `e2e-tests.yml`, Dependabot, [Bloc2 §C19](./Bloc2_Frontend.md) | ✅ |
| C20 | Performances SEO (≥ 70 %) | — | **Mesuré le 22/07 : SEO 92 % sur l'accueil, 100 % sur les 4 autres pages** (seuil 70 %). Le site n'a jamais eu de défaut de SEO, c'est le job Lighthouse qui ne mesurait rien ; corrigé, il audite les 5 pages, [Bloc2 §C20](./Bloc2_Frontend.md) | ✅ |

### Bloc 3 — Back-end

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C21 | Couche de persistance (sécurité en profondeur) | E15 | `WorkspaceAccessInterceptor`, `AuditableEntity`, `EncryptedStringConverter`, [Bloc3 §C21](./Bloc3_Backend.md) | ✅ |
| C22 | Langage back (qualité, sécurité, écoconception) | E16 | Architecture `shared/core/modules`, Virtual Threads Java 21, Trivy/Semgrep, [Bloc3 §C22](./Bloc3_Backend.md) | ✅ |
| C23 | Système de paiement + monétisation | E17 | Stripe Checkout, **5 webhooks réellement implémentés** (signature `Webhook.constructEvent`, idempotence par `stripe_event_id UNIQUE`, rejeu en différé sur erreur), portail de facturation. La mention « stubés » (PC-005) était périmée, vérifié le 22/07. Reste : un passage avec de vrais événements Stripe, [Bloc3 §C23](./Bloc3_Backend.md) | ✅ |
| C24 | Développer une API sécurisée | E18 | JWT+Keycloak, `@Valid` DTOs, AES-256-GCM, OpenAPI `/swagger-ui.html`, [Bloc3 §C24](./Bloc3_Backend.md) | ✅ |
| C25 | Tester le back-end (couverture ≥ 50 %) | E19 | **73,71 % JaCoCo**, 792 tests, vrai Postgres sans simulacre (**pas** Testcontainers, cf. Bloc3), [Bloc3 §C25](./Bloc3_Backend.md) | ✅ |
| C26 | Industrialiser le back-end | E20 | `backend-tests.yml`, `release.yml`, images GHCR, Trivy+Semgrep+ZAP, [Bloc3 §C26](./Bloc3_Backend.md) | ✅ |

### Bloc 4 — Déploiement & production

| Comp. | Intitulé court | Livrable | Où dans TaskForce | Statut |
| :---: | -------------- | :------: | ----------------- | :----: |
| C27 | Documentation technique + base de connaissances | E29 | Ce Brain OS, OpenAPI auto-généré, `version-management.yml`, [Release Notes](../15-utilisateur/Release_Notes.md), [Bloc4 §C27](./Bloc4_Deploiement_Production.md) | ✅ |
| C28 | Administration (domaine, DNS, certificats, sécurité) | E23 | ⚠️ **Décoché le 23/07 : rien n'est déployé.** Aucun domaine réservé, aucune zone DNS, aucun certificat émis. `nginx/nginx.conf.example` est **prêt et validé** (TLS 1.2/1.3, HSTS, OCSP, limitation de débit) mais non déployé, [Bloc4 §C28](./Bloc4_Deploiement_Production.md) | ⬜ |
| C29 | Sélectionner une plateforme d'hébergement | E21 | [Diagramme de déploiement](../06-infra/Diagramme_Deploiement.md) **(produit le 23/07)** + [Stratégie Hébergement](../06-infra/Strategie_Hebergement.md), `render.yaml`, [Bloc4 §C29](./Bloc4_Deploiement_Production.md) — ⚠️ déploiement prod stand-by | 🟡 |
| C30 | Administrer des services d'hébergement (cloud/conteneur) | E22 | `docker-compose.prod.yml` (9 services, réécrit le 22/07), réseaux Docker isolés, [Bloc4 §C30](./Bloc4_Deploiement_Production.md). ⚠️ Composition **prête mais jamais exécutée en production** : à présenter comme telle | 🟡 |
| C31 | Déploiement automatisé (DevOps / CI-CD) | E24 | 7 workflows GitHub Actions, images GHCR versionnées, [Pipeline CI/CD](../08-operations/Pipeline_CICD.md), [Bloc4 §C31](./Bloc4_Deploiement_Production.md) | ✅ |
| C32 | Supervision (sondes, alertes, journalisation) | E25–E28 | OTel→SigNoz, 9 alertes Prometheus, `AuditService`, `backup.ps1`, ZAP/Trivy/Semgrep, [Bloc4 §C32](./Bloc4_Deploiement_Production.md) | ✅ |

## 4. Conventions de rédaction

<p class="lead">
Chaque fiche bloc suit le même gabarit : par compétence, on trouve l'énoncé officiel, le(s) livrable(s)
attendu(s), les <strong>critères de la grille en cases à cocher</strong>, le pointeur vers la preuve dans
TaskForce, puis un espace de rédaction à compléter.
</p>

Règles : rédaction **narrative** (paragraphes, pas de listes sèches) conformément au
[template](../../templates/Template_Doc_Technique.md) ; chaque affirmation technique renvoyée vers une preuve
(capture, lien de code, lien Brain OS) ; cocher un critère uniquement quand la preuve est intégrée au dossier.

---

> **Note Brain OS** — Ce mémoire s'appuie sur les documents techniques vérifiés du
> [Brain OS](../../Brain_OS.md). Les écarts connus (tests, RGPD, SEO, déploiement) sont des **chantiers de
> rédaction**, tracés dans [Problèmes connus](../09-audits/Problemes_Connus.md).

**Dernière mise à jour :** 05/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
