---
type: memoire-rncp
bloc: 1
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc1, conception, modelisation]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 1 — Concevoir et modéliser une application

**Version :** 1.0  
**Date :** 05/07/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 1](https://img.shields.io/badge/Bloc-1%20Conception-blue?style=for-the-badge)]() [![Statut: Validé](https://img.shields.io/badge/Statut-Valid%C3%A9-green?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture technique](../03-architecture/Architecture.md) · [CdCF](../01-projet/01_CdCF.md) · [CdCT](../01-projet/02_CdCT.md)

**Tags :** `#memoire` `#bloc1` `#conception` `#modelisation`

<p class="lead">
Ce bloc couvre l'analyse de la demande, la préparation du projet (agile, environnement de dev) et la
conception/modélisation (wireframes, STB, modèle de données, architecture logicielle, RGPD, veille).
Compétences C1 à C12, livrables E1 à E10.
</p>

> **Gabarit par compétence** : énoncé officiel → livrable(s) → critères de la grille (à cocher) → preuve
> dans TaskForce → rédaction narrative. Un critère est coché uniquement si la preuve est intégrée au dossier.

## Table des matières

1. [Activité — Analyse de la demande & CdCF](#activité--analyse-de-la-demande--cdcf) (C1, C2)
2. [Activité — Préparation du déploiement projet](#activité--préparation-du-déploiement-projet) (C3, C4, C5)
3. [Activité — Spécifications, conception, modélisation](#activité--spécifications-conception-modélisation) (C6–C11)
4. [Activité — Veille](#activité--veille) (C12)

---

## Activité — Analyse de la demande & CdCF

### C1 — Analyser la demande initiale du client
**Livrable :** E1 — présentation de synthèse et reformulation de la demande.  
**Critères d'évaluation :**
- [x] Le besoin général, la culture, le contexte et les enjeux du client sont identifiés fidèlement.
- [x] La problématique d'usage est formulée de façon claire et précise.
- [x] Le cas échéant, les sujets d'actualisation d'une application préexistante sont listés. *(N/A — projet créé de zéro)*

**Preuves :** [CdCF v1.1](../01-projet/01_CdCF.md) · [Dossier Projet v1.2](../01-projet/Dossier_Projet.md) · [Étude Business](../01-projet/Etude_business.md)

**Analyse de la demande**

Le projet TaskForce est né d'une problématique concrète et répandue dans les équipes professionnelles modernes : la répartition manuelle des tâches génère des déséquilibres de charge, des pertes de productivité et une démotivation des collaborateurs. Les managers manquent de visibilité globale sur les compétences disponibles et la charge réelle, ce qui conduit à des décisions d'affectation sous-optimales. Cette problématique a été formalisée dans le [CdCF](../01-projet/01_CdCF.md) (v1.1, 27/02/2026) et le [Dossier Projet](../01-projet/Dossier_Projet.md) (v1.2, 17/01/2026).

La **problématique d'usage centrale** est la suivante : comment optimiser la répartition dynamique des tâches dans une équipe hétérogène en tenant compte simultanément des compétences déclarées des membres, de leur charge de travail en cours (cross-projets), de leur disponibilité dans les cycles actifs, et de leur historique de résolution ? Cette question n'est pas résolue par les outils existants comme Linear ou Jira, qui proposent une assignation exclusivement manuelle.

Le **contexte métier** identifié est celui de la startup et de l'équipe tech de 5 à 50 personnes, pour qui le time-to-assign est un coût masqué : chaque manager doit mentalement croiser disponibilités, compétences et priorités à chaque nouvelle tâche. TaskForce automatise ce processus tout en restant transparent (explication en langage naturel de chaque suggestion).

Les **enjeux transverses** ont été identifiés dès le cadrage : conformité RGPD (les données de compétences et de charge constituent des données à caractère personnel), sécurité multi-tenant (isolation stricte des données entre workspaces), accessibilité WCAG 2.1 AA, et référencement de la landing page.

Les **acteurs** du système ont été définis en trois niveaux : l'**OWNER** (responsable workspace — configure l'espace, manage les membres, supervise les abonnements Stripe), l'**ADMIN** (chef de projet — crée les projets, configure les cycles, active Smart Assign), et le **MEMBER** (collaborateur — prend en charge les issues, renseigne son profil de compétences, reçoit ou accepte les suggestions d'assignation). Ce RBAC à 3 niveaux est implémenté dans `AuthorizationService.java` via l'enum `WorkspaceMemberRole`.

---

### C2 — Apporter son expertise technique (conseil sur le CdCF)
**Livrable :** E1, E3 — préconisations techniques, innovations proposées.  
**Critères d'évaluation :**
- [x] Une distance critique est prise (interrogations, préconisations, propositions d'innovation : faisabilité technique, UX).
- [x] Des opportunités sont détectées (éco-responsabilité, inclusion).

**Preuves :** [Note Innovation & Distance Critique](../17-veille/Note_Innovation_Distance_Critique.md) · [CdCT](../01-projet/02_CdCT.md) · [ADR Journal](../08-decisions/Journal_Decisions_ADR.md)

**Expertise technique apportée**

L'analyse du besoin a conduit à plusieurs préconisations qui s'écartent d'une approche initiale supposant un stack PHP/MySQL classique. Ces choix sont documentés sous forme d'ADR (Architecture Decision Records) dans le [Journal des décisions](../08-decisions/Journal_Decisions_ADR.md).

**Préconisation 1 — Stack moderne Java/TypeScript.** L'adoption de Spring Boot 4 (Java 21 LTS) + Next.js 16 (React 19) + TypeScript 5 strict a été préconisée pour trois raisons : les Virtual Threads (Project Loom) apportent une scalabilité I/O-bound native sans réécriture (un virtual thread par requête HTTP au lieu d'un pool de threads bloquant) ; TypeScript strict élimine une catégorie entière de bugs à la compilation ; l'écosystème Spring (Spring Security, JPA, Actuator, OpenTelemetry) réduit le code boilerplate sécurité. ADR-001.

**Préconisation 2 — IA de recommandation native Java.** Plutôt qu'un microservice Python séparé (FastAPI + Ollama), il a été préconisé d'appeler directement Groq API depuis Java via `RestClient`. Cette décision (ADR-004) réduit la complexité opérationnelle (un service de moins en production), améliore la latence (~150 tokens/s sur Groq vs ~30 tokens/s OpenAI) et simplifie le déploiement. La dégradation gracieuse est garantie : si la clé Groq est absente, le moteur Java produit un résultat sans explication LLM.

**Préconisation 3 — Recherche vectorielle in-database.** L'extension pgvector dans PostgreSQL 18 a été préférée à une base vectorielle dédiée (Pinecone — SaaS payant hors UE, Weaviate — service supplémentaire). Un seul processus de base de données gère les données relationnelles et vectorielles : moins de RAM en production, zéro transfert de données hors infrastructure, conformité RGPD facilitée (ADR-005).

**Préconisation 4 — SSO Keycloak comme IdP.** Déléguer la gestion des identités à Keycloak évite d'implémenter le stockage et la validation des mots de passe en interne (OWASP A07 — Identification and Authentication Failures). Keycloak fournit OTP email, gestion des sessions, et API Admin REST pour les opérations d'administration. ADR-003.

**Opportunités d'éco-responsabilité** : modèle d'embedding `all-MiniLM-L6-v2` (384 dimensions, 4× moins de stockage vectoriel et de calcul cosine que OpenAI Ada 1536d) ; base images Alpine (×3 plus légères) ; SigNoz self-hosted (pas de transfert de données télémétrie vers des datacenters tiers) ; Groq LPU (efficience énergétique ×3-10 vs GPU Nvidia standard pour l'inférence). Ces choix sont détaillés dans [Note Innovation §3](../17-veille/Note_Innovation_Distance_Critique.md).

**Opportunités d'inclusion** : le mode **montée en compétence** (`growth_mode`) de Smart Assign est une décision de conception délibérée pour lutter contre le "winner takes all" dans la répartition des tâches. Quand ce mode est activé sur un projet, l'algorithme favorise modérément (bonus borné +12/+15 pts) un membre junior dont les `growth_target_skills` sont adjacentes à la tâche — à condition que la tâche ne soit pas urgente et que la disponibilité du membre soit ≥ 60 %. Cette feature est implémentée dans `SmartAssignService.java` et la migration `V46__member_growth_objectives.sql`.

---

## Activité — Préparation du déploiement projet

### C3 — Identifier les caractéristiques du projet (planification & budget)
**Livrable :** E2 — planification prévisionnelle + ébauche de budget.  
**Critères d'évaluation :**
- [x] Public utilisateur, besoins de référencement et de sécurité analysés et explicités exhaustivement.
- [x] Délais, budget et contraintes → planning + budget prévisionnels réalistes.
- [x] Adéquation au cadre réglementaire et législatif ; anticipation de l'évolution des normes.
- [x] Possibilités d'aménagement inclusif et d'écoconception analysées.

**Preuves :** [Dossier Projet](../01-projet/Dossier_Projet.md) · [Étude Business](../01-projet/Etude_business.md) · [CdCT §8 Exigences non-fonctionnelles](../01-projet/02_CdCT.md)

**Caractéristiques du projet**

Le **public cible** principal de TaskForce est l'équipe tech de 5 à 50 personnes (startups, agences, ESN) dont les membres ont des profils de compétences hétérogènes. Un public secondaire est constitué des managers de projets complexes à forte intensité de compétences spécialisées (data, DevOps, sécurité). L'[Étude Business](../01-projet/Etude_business.md) positionne TaskForce sur un segment « linear.app + IA » avec un modèle freemium (FREE / PRO / ENTERPRISE).

Le **besoin de référencement** a été analysé : TaskForce nécessite une landing page orientée SEO (génération de leads B2B). L'choix d'Astro (SSG — Static Site Generation) pour la landing permet une indexation optimale par les moteurs de recherche (pages HTML statiques, temps de chargement < 1s, meta-tags structurés). L'application SaaS elle-même n'a pas besoin de SEO (accès authentifié).

Les **contraintes de sécurité** identifiées couvrent : isolation multi-tenant (fuite de données entre workspaces = risque critique), authentification forte (OTP email, rate limiting), chiffrement des PII sensibles (messages Enterprise, notes — AES-256-GCM), conformité OWASP Top 10. Ces contraintes sont formalisées dans la [PSSI](../07-securite/PSSI.md) et le [CdCT §8](../01-projet/02_CdCT.md).

Le **planning prévisionnel** couvre 9 mois (octobre 2025 → juillet 2026) avec une approche itérative : Phase 1 (Core + Auth + RBAC), Phase 2 (Projets + Issues + Kanban), Phase 3 (Smart Assign + pgvector), Phase 4 (Chat + Notifications + Cycles), Phase 5 (Stripe + Plans), Phase 6 (Observabilité + Tests), Phase 7 (RGPD + Sécurité + Documentation). La structure WBS, le diagramme de Gantt et la matrice RACI sont produits dans le [Dossier Projet](../01-projet/Dossier_Projet.md).

Le **budget prévisionnel** repose sur une philosophie open-source maximale : Keycloak (gratuit, self-hosted), PostgreSQL + pgvector (gratuit), SigNoz (gratuit, self-hosted), RabbitMQ (gratuit), MinIO (gratuit, self-hosted). Les seuls coûts variables sont Groq API (tier gratuit 14 400 req/jour, tier payant si dépassement) et Stripe (2,9% + 30¢ par transaction). L'infrastructure de production est estimée à ~46 $/mois sur Render.com (Option B) ou ~0 sur la VM de l'école (Option A).

Le **cadre réglementaire** a été anticipé dès la conception : RGPD (Règlement Général sur la Protection des Données) pour les données de compétences et de charge (PII), CNIL pour les recommandations sur les cookies, WCAG 2.1 AA pour l'accessibilité. La DSP2 (Directive Services de Paiement) est couverte par la délégation complète à Stripe (PCI-DSS niveau 1).

Les **possibilités d'aménagement inclusif** ont été analysées : l'accès clavier complet via Shadcn/Radix UI, le thème sombre/clair (`prefers-color-scheme`), les ratios de contraste WCAG AA dans le design system, et l'audit axe-core automatisé en CI (`a11y.spec.ts`). L'écoconception est traitée dans la [Note Innovation §3](../17-veille/Note_Innovation_Distance_Critique.md).

---

### C4 — Travailler en mode agile
**Livrable :** E5 (note justifiant la méthode agile), E6 (trame de compte rendu d'activité).  
**Critères d'évaluation :**
- [x] Méthode agile (XP, Scrum, DSDM, ASD…) avec cycle adapté aux contraintes et à la dimension du projet.
- [x] Trame de compte rendu d'activité correspondant à la méthode, opérationnelle.

**Preuves :** [Git Workflow](../04-engineering/git-workflow/README.md) · [GitHub Actions](../04-engineering/git-workflow/github-actions.md) · Application TaskForce elle-même (Issues, Cycles, Labels)

**Méthode agile : Scrum allégé avec Kanban**

La méthode retenue est un **Scrum allégé** adapté à un contexte solo (1 développeur ETP) avec un cycle de sprint de 2 semaines. Ce choix est justifié par plusieurs contraintes : la dimension exploratoire du projet (IA = domaine peu maîtrisé au départ, beaucoup d'expérimentation), la nécessité d'itérations courtes pour valider les choix techniques rapidement, et la volonté de pratiquer l'outil en dogfooding (TaskForce est développé *avec* TaskForce).

**Structure des sprints** : chaque cycle de 2 semaines comporte une session de planification (sélection des issues en BACKLOG → STARTED), un suivi quotidien informel (vue Kanban), et une revue de sprint (merge des PRs, mise à jour de la roadmap, création du compte-rendu). Les cérémonies sont matérialisées par les Issues et Cycles de l'application TaskForce elle-même — ce dogfooding valide le produit en conditions réelles.

**Trame de compte rendu d'activité (E6)** : chaque PR (Pull Request) GitHub constitue le compte-rendu de l'unité de travail. Elle inclut : le titre au format conventionnel (`feat(module):`, `fix(module):`, `test:`...), la description des changements, les critères d'acceptance liés aux Issues fermées, et le lien vers le rapport de couverture CI. Le workflow `version-management.yml` automatise le bumping SemVer basé sur les labels (`feat` → minor, `fix` → patch). Le [Git Workflow](../04-engineering/git-workflow/README.md) documente la convention de branches (`feature/`, `fix/`, `chore/`) et les règles de merge (squash merge, PR obligatoire sur `main`).

**Adaptation à la dimension solo** : les rôles Scrum (Product Owner, Scrum Master, Développeur) sont tenus par une seule personne. Les cérémonies ont été simplifiées mais conservées dans leur intention : le backlog produit est maintenu dans [Roadmap Backlog](../13-roadmap/Roadmap_Backlog.md), les sprints sont les Cycles TaskForce, les PR sont les livraisons. Cette organisation a démontré son efficacité sur 9 mois : 670 tests backend, 746 tests frontend, et 7 workflows CI/CD opérationnels.

---

### C5 — Mettre en œuvre un environnement de développement collaboratif
**Livrable :** E4 — procédure complète de mise en œuvre de l'environnement.  
**Critères d'évaluation :**
- [x] Outils/technologies adaptés aux contraintes et à la dimension du projet.
- [x] La procédure démontre la maîtrise du SCM **Git**, d'un **IDE** du marché et de la **virtualisation** sur poste local.

**Preuves :** [Quickstart](../06-infra/quickstart/README.md) · [GHCR Usage](../06-infra/docker/GHCR_USAGE.md) · `docker-compose.dev.yml` · [Git Workflow](../04-engineering/git-workflow/README.md)

**Environnement de développement**

L'environnement de développement TaskForce est entièrement conteneurisé, reproductible en une commande, et documenté dans le [Quickstart](../06-infra/quickstart/README.md). Le démarrage complet suit 4 étapes : (1) `git clone` du dépôt, (2) copie et configuration du fichier `.env.dev` (variables d'environnement listées dans le README), (3) `docker compose -f docker-compose.dev.yml up -d` (démarre PostgreSQL 18 + pgvector, Keycloak, RabbitMQ, MinIO), (4) démarrage des services applicatifs (`./mvnw spring-boot:run` pour le backend, `npm run dev` pour le frontend). Ce démarrage en < 2 minutes a été validé sur Windows 11 + Docker Desktop.

**SCM Git** : le dépôt utilise Git avec un [workflow de branches](../04-engineering/git-workflow/README.md) structuré : `main` (production-ready, PR obligatoire), branches `feature/<scope>/<description>`, `fix/<scope>/<description>`, `chore/<scope>`. Les commits suivent la convention Conventional Commits (`feat:`, `fix:`, `test:`, `docs:`, `chore:`). Le versioning SemVer est automatisé par `version-management.yml`.

**IDE** : IntelliJ IDEA Ultimate pour le backend Java (Spring Boot, débogage JPDA sur le port 5005 via `docker compose debug`), VS Code avec les extensions ESLint, Prettier, TypeScript et Tailwind CSS IntelliSense pour le frontend Next.js.

**Virtualisation** : Docker Desktop assure la virtualisation locale. Le fichier `docker-compose.dev.yml` orchestre 4 services d'infrastructure (PostgreSQL, Keycloak, RabbitMQ, MinIO) avec des volumes nommés persistants. Le fichier `docker-compose.tools.yml` ajoute l'observabilité (SigNoz + OTel Collector) activable à la demande via le profil `--profile observability`. Les images sont publiées sur GitHub Container Registry (GHCR) selon le processus documenté dans [GHCR Usage](../06-infra/docker/GHCR_USAGE.md).

---

## Activité — Spécifications, conception, modélisation

### C6 — Concevoir des maquettes « wireframe »
**Livrable :** E7 — présentation de maquette wireframe.  
**Critères d'évaluation :**
- [x] La maquette correspond précisément à une vue souhaitée dans la note de cadrage.
- [x] Conforme aux standards de la profession, notamment en matière d'UX.

**Preuves :** `assets/maquettes/` (dashboard, login, register, kanban, smart-assign, profile, settings, landing)

**Maquettes wireframe**

Les wireframes de TaskForce couvrent les vues principales identifiées dans le [CdCF](../01-projet/01_CdCF.md) : authentification (login, register, OTP verification), tableau de bord workspace, vue Kanban d'un projet, modal Smart Assign, profil utilisateur (compétences, disponibilité), paramètres workspace, et landing page. Les fichiers sont disponibles dans `assets/maquettes/`.

Les wireframes ont été conçus en suivant les standards UX actuels : navigation latérale fixe (sidebar workspace) + navigation secondaire en header (projets), pattern de création inline (raccourci `C` pour créer une issue sans quitter le Kanban), affichage des avatars et badges de priorité directement sur les cartes Kanban. L'esthétique s'inspire de Raycast et Linear (glassmorphism, mode sombre natif, typographie monospace pour les identifiants d'issues).

La conformité entre les maquettes et l'implémentation est vérifiable dans `frontend/app/` : chaque route correspond à une vue wireframée. La navigation workspace (`/[workspaceSlug]/`) reproduit fidèlement la sidebar avec la liste des projets, cycles, pages wiki et canaux de discussion.

---

### C7 — Traduire les besoins en spécifications techniques (STB)
**Livrable :** E8 — dossier de conception.  
**Critères d'évaluation :**
- [x] Outils/technologies adaptés ; dossier de conception complet.
- [x] Les cas d'utilisation couvrent l'ensemble des exigences du CdCF.
- [x] Les classes d'analyse et de conception sont définies et cohérentes.

**Preuves :** [CdCT](../01-projet/02_CdCT.md) · [Architecture §4](../03-architecture/Architecture.md) · [Modules](../03-architecture/Modules.md)

**Traduction des besoins en spécifications techniques**

Le passage des besoins fonctionnels aux spécifications techniques est formalisé dans le [CdCT](../01-projet/02_CdCT.md). Ce document traduit chaque use case fonctionnel en exigences techniques mesurables : les exigences de performance (PERF-01 : `p95 < 500ms` pour les requêtes API standard, PERF-02 : 100 requêtes/seconde en pointe), les exigences de sécurité (SEC-01 à SEC-09 : authentification multi-facteur, rate limiting, headers OWASP, chiffrement PII), et les exigences de disponibilité (DISP-01 : 99,5 % uptime en production).

Les **12 cas d'utilisation** (UC-01 à UC-12) couvrent intégralement le périmètre du CdCF : inscription avec OTP (UC-01), connexion (UC-02), gestion workspace (UC-03), invitations (UC-04), gestion projets (UC-05), issues + Kanban (UC-06), Smart Assign (UC-07), cycles (UC-08), chat STOMP (UC-09), pages wiki (UC-10), facturation Stripe (UC-11), droits RGPD (UC-12). Chaque UC est détaillé avec acteur, précondition, flux normal, flux alternatifs et post-condition.

Les **classes d'analyse** sont définies dans le package `backend/tf-api/src/main/java/com/taskforce/core/model/` et organisées par domaine métier : `User`, `Workspace`, `WorkspaceMember`, `Project`, `Issue`, `Cycle`, `Page`, `Channel`, `Message`, `Subscription`. Les associations (workspace → members → projects → issues) et les contraintes (UNIQUE workspace_slug, FK avec ON DELETE CASCADE/SET NULL selon le cas) sont cohérentes avec le modèle métier.

---

### C8 — Modéliser l'application
**Livrable :** E8.  
**Critères d'évaluation :**
- [x] Structure, associations, relations et contraintes décrites selon des normes de modélisation reconnues, modèle adapté.
- [x] Sert à établir des règles de gestion des données efficaces et à minimiser la redondance.

**Preuves :** [Architecture §6 — Modèle de données](../03-architecture/Architecture.md) · [Modules §4](../03-architecture/Modules.md) · Migrations Flyway V1–V53 (`backend/tf-api/src/main/resources/db/migration/`)

**Modélisation entité-association**

Le modèle de données de TaskForce est décrit sous forme d'ERD dans [Architecture §6](../03-architecture/Architecture.md) et matérialisé par 53 migrations Flyway versionnées. Les entités principales et leurs relations sont les suivantes :

- `users` (1) ↔ (N) `workspace_members` ↔ (N) `workspaces` : un utilisateur peut appartenir à plusieurs workspaces avec un rôle distinct par workspace.
- `workspaces` (1) → (N) `projects` → (N) `issues` : la hiérarchie de tri est workspace > projet > issue.
- `issues` (N) ↔ (N) `issues` via `issue_relations` : relations typées (`blocks`, `blocked-by`, `duplicate-of`).
- `member_skill_profiles` : table de jointure enrichie entre `workspace_members` et le profil vectoriel (`embedding vector(384)`) — le vecteur est la représentation sémantique des compétences du membre, utilisé pour la recherche cosine.
- `assignment_events` : historique des assignations Smart Assign (source decision, score, feedback accepté/rejeté) — alimentation du signal historique.

Les **règles de gestion** minimisent la redondance : les données de compétences des membres ne sont pas dupliquées par projet (elles sont portées par `workspace_members` et `member_skill_profiles`). Les statuts d'issue sont configurables par projet via `issue_statuses` (table de référence par projet) plutôt qu'un enum global — ce choix évite de dupliquer la logique de workflow dans le code.

Les **contraintes d'intégrité** sont systématiquement définies au niveau base de données : FK avec `ON DELETE CASCADE` (supprimer un workspace supprime tout son contenu), `ON DELETE SET NULL` pour les assignations (un membre peut quitter sans invalider les issues), contrainte `UNIQUE(workspace_id, slug)` pour l'unicité des slugs de projet dans un workspace. Ces contraintes garantissent la cohérence même si la couche applicative est contournée.

---

### C9 — Concevoir l'architecture des bases de données (persistance)
**Livrable :** E8.  
**Critères d'évaluation :**
- [x] Décrit la gestion des données (collecte → transformation → distribution → consommation) et leur circulation.
- [x] Décrit comment l'architecture facilite le besoin métier.
- [x] Décrit le cycle de vie des données **et la couche de persistance** (sauvegarde/restauration).

**Preuves :** [Architecture §6](../03-architecture/Architecture.md) · [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) · `scripts/backup.ps1`

**Architecture de persistance**

La couche de persistance de TaskForce est construite sur **PostgreSQL 18** (SGBDR principal) enrichi de l'extension **pgvector** pour le stockage et la recherche vectorielle. Ce choix d'une base unique (au lieu d'une base relationnelle + une base vectorielle séparée) simplifie la gestion opérationnelle et garantit l'ACID sur les données relationnelles et vectorielles dans la même transaction.

**Circulation des données** : les données collectées (profils de compétences des membres, descriptions d'issues, documents RAG) passent par un pipeline d'embedding avant stockage. La classe `EmbeddingService.java` appelle le modèle `all-MiniLM-L6-v2` (via API locale ou distante), transforme le texte en vecteur `float[]` de 384 dimensions, et le persiste dans la colonne `embedding vector(384)` via JPA et `VectorType` (hibernate-types). La recherche cosine (`<=>` opérateur pgvector) est exécutée par la requête JPQL native de `SmartAssignRepository`.

**Comment l'architecture facilite le besoin métier** : l'index **HNSW** (Hierarchical Navigable Small World) créé sur les colonnes `embedding` permet des recherches de similarité en < 10ms p95 sur 100 000 vecteurs (pgvector 0.7.0, benchmarks publics). Sans cet index, la même recherche nécessiterait un scan séquentiel linéaire. Ce choix est documenté dans ADR-005.

**Schéma de migration** : toutes les modifications de schéma passent par **Flyway** (migrations versionnées V1 à V53 dans `src/main/resources/db/migration/`). Ce principe de « schema-as-code » garantit que la base de données en production est toujours dans un état connu et reproductible. Les migrations sont exécutées au démarrage de l'application, avant que l'API ne commence à accepter des requêtes.

**Cycle de vie des données et sauvegarde** : le [Plan de Sauvegarde et de Continuité (PS/PCA/PRA)](../11-pca-pra/PS_PCA_PRA.md) définit la stratégie de backup. Le script `scripts/backup.ps1` automatise : (1) `pg_dump` de la base PostgreSQL (dump compressé `.pgdump`), (2) sauvegarde des buckets MinIO (fichiers attachés), (3) export des configurations Keycloak (realm JSON). La fréquence cible est quotidienne (backup complet) + transactionnel (WAL archiving en option). La procédure de restauration est testée et documentée dans le PRA.

---

### C10 — Déterminer l'architecture logicielle
**Livrable :** E8.  
**Critères d'évaluation :**
- [x] Cas d'utilisation couvrant les exigences du CdC initial.
- [x] Classes d'analyse/conception cohérentes.
- [x] Architecture logicielle conforme aux usages de la profession et adaptée au cas d'étude.
- [x] Dossier de spécifications structuré et documenté conformément à la démarche choisie.

**Preuves :** [Architecture §4 — Architecture logicielle](../03-architecture/Architecture.md) · [Modules](../03-architecture/Modules.md) · [CdCT](../01-projet/02_CdCT.md)

**Architecture logicielle**

L'architecture logicielle de TaskForce suit un modèle **en couches (layered architecture)** avec une organisation modulaire par domaine métier, conforme aux bonnes pratiques Spring Boot. Le backend est structuré en trois couches :

1. **`shared/`** — Utilitaires transversaux : sécurité (`SecurityConfig`, `JwtIdentityResolver`, `RateLimitFilter`), CORS, audit (`AuditableEntity`), exceptions (`ApiException`), converters JPA (`EncryptedStringConverter`).
2. **`core/`** — Domaine socle : `User`, `Workspace`, `WorkspaceMember`, RBAC (`AuthorizationService`), Keycloak Admin, Stripe, GDPR.
3. **`modules/`** — Domaines métier isolés : `project`, `issue`, `smart-assign`, `cycle`, `page`, `chat`, `ai-document`, `notification`. Chaque module contient son propre `controller`, `service`, `repository`, `model`, `dto`.

Cette organisation garantit la **séparation des préoccupations** : un bug dans le module `smart-assign` ne peut pas affecter le module `chat` par effet de bord. Les seules dépendances inter-modules sont explicites et unidirectionnelles (les modules métier dépendent du `core`, jamais l'inverse).

La **multi-tenancy** est implémentée via `workspace_slug` : chaque requête API est interceptée par `WorkspaceAccessInterceptor` qui vérifie que l'utilisateur authentifié est bien membre du workspace ciblé avant de transmettre la requête au contrôleur. Ce principe d'isolation est appliqué à 100 % des endpoints `/api/workspaces/{slug}/**`.

Le frontend Next.js suit le pattern **App Router** avec co-localisation des composants et de leurs tests. Les stores Zustand (`useWorkspaceStore`, `useIssueStore`...) centralisent l'état client, tandis que les appels API passent par un client Axios centralisé (`frontend/lib/api/client.ts`) qui gère le refresh automatique du JWT et la redirection vers `/login` en cas de 401 persistant.

Le dossier de spécifications est structuré dans ce Brain OS : [CdCF](../01-projet/01_CdCF.md) (besoins fonctionnels), [CdCT](../01-projet/02_CdCT.md) (exigences techniques), [Architecture](../03-architecture/Architecture.md) (architecture logicielle + données), [Modules](../03-architecture/Modules.md) (détail par module), [API](../05-api/API.md) (contrats REST + OpenAPI).

---

### C11 — Conformité légale (CNIL / RGPD)
**Livrable :** E9 — audit de conformité RGPD.  
**Critères d'évaluation :**
- [ ] Outil de recueil du consentement cookies proposé. *(⚠️ TF-RGPD-001 — bannière absente)*
- [x] Vue « politique de confidentialité et traitement des données personnelles » prévue.
- [x] Formulaire de demande d'accès aux données personnelles + traitement proposé.
- [ ] Processus de double opt-in proposé pour les traitements collectant des données personnelles. *(⚠️ TF-RGPD-004 — non implémenté)*

**Preuves :** [Audit RGPD Conformité](../07-securite/Audit_RGPD_Conformite.md) · [Registre Traitements Art. 30](../07-securite/Registre_Traitements_RGPD.md) · [Politique Confidentialité & CGU](../07-securite/Politique_Confidentialite_CGU.md) · `GdprService.java` · `PrivacyPolicyPageNew.tsx` · `TermsPageNew.tsx`

**Analyse de conformité RGPD — TaskForce**

> **Note** : le livrable E9 du référentiel RNCP est un audit de conformité d'un **cas professionnel fourni par l'établissement** (site ou application externe). Cette section documente la conformité RGPD du projet fil rouge TaskForce lui-même, qui constitue une démonstration de la maîtrise des outils et concepts requis.

L'audit de conformité RGPD de TaskForce est formalisé dans [Audit_RGPD_Conformite.md](../07-securite/Audit_RGPD_Conformite.md) avec un taux de couverture estimé à ~75 %. Le [Registre des traitements (Art. 30 RGPD)](../07-securite/Registre_Traitements_RGPD.md) recense 7 traitements : comptes utilisateurs, facturation, données métier, compétences/embeddings, audit, leads Enterprise, tokens OAuth.

**Ce qui est implémenté** : la **politique de confidentialité** est disponible sur la landing page (`/privacy-policy`) via le composant `PrivacyPolicyPageNew.tsx` avec support i18n EN/FR. Les **CGU** (`/terms`) sont accessibles via `TermsPageNew.tsx`. Le **droit d'accès aux données (Art. 20 RGPD)** est implémenté : `GET /api/gdpr/export` déclenche `GdprService.exportMyData()` qui retourne un JSON structuré de toutes les données de l'utilisateur. Le **droit à l'effacement (Art. 17)** est implémenté : `DELETE /api/gdpr/delete-account` anonymise le compte (email → `deleted-{id}@anonymized.invalid`, tokens révoqués, isActive = false) avec journalisation dans `AuditLog` (events `GDPR_EXPORT`, `GDPR_DELETE`). Le chiffrement **AES-256-GCM** protège les PII sensibles via `EncryptedStringConverter`.

**Corrigés lors du durcissement V1 (05/07/2026)** : la **bannière cookies** existe et a été requalifiée en notice d'information (l'app n'utilise que des cookies strictement nécessaires → consentement non requis CNIL) — TF-RGPD-001 clos. La **suppression de l'identité Keycloak** est désormais déclenchée à l'effacement (`GdprService` → `KeycloakService.deleteUser`, après commit) — TF-RGPD-007 clos. Les **sous-traitants** de la politique de confidentialité ont été corrigés (Stripe/Groq réels au lieu d'AWS/Google Analytics) — TF-RGPD-005.

**Ce qui reste à faire (gaps documentés)** : le **double opt-in** (confirmation email pour les traitements marketing) n'est pas implémenté — TF-RGPD-004 ; la **page de mentions légales** dédiée (LEN Art. 6) reste à créer — TF-RGPD-005 ; le **DPA Groq** est à formaliser — TF-RGPD-008. Ces gaps sont tracés dans la [Roadmap Backlog](../13-roadmap/Roadmap_Backlog.md).

---

## Activité — Veille

### C12 — Proposer des solutions alternatives/innovantes (veille)
**Livrable :** E10 — méthodologie de veille technologique.  
**Critères d'évaluation :**
- [x] Méthodologie cohérente, adaptée et appliquée aux exigences et au contexte de l'application.
- [x] Détaille la fréquence et les méthodes de recherche de sources, de compilation et d'actualisation.

**Preuves :** [Veille Technologique](../17-veille/Veille_Technologique.md) · [Note Innovation & Distance Critique](../17-veille/Note_Innovation_Distance_Critique.md) · ADR-001 à ADR-010

**Méthodologie de veille et entrées documentées**

La veille technologique pratiquée sur TaskForce est formalisée dans [Veille_Technologique.md](../17-veille/Veille_Technologique.md). Elle couvre trois axes : stabilité du stack (versions, breaking changes), opportunités d'amélioration (patterns, outils, sécurité), et tendances IA/LLM (évolution rapide des APIs).

**Sources surveillées** : GitHub releases (Spring Boot, Next.js, Keycloak, pgvector, RabbitMQ) en hebdomadaire via RSS/GitHub Watch ; CNIL, OWASP Top 10, NVD/CVE et GitHub Dependabot pour la sécurité ; blog.groq.com, Hugging Face Blog pour l'IA/LLM ; signoz.io/blog pour l'observabilité. La fréquence varie de hebdomadaire (sécurité, IA) à mensuelle (communautés). Le processus de traitement suit le cycle : Découverte → Évaluation (pertinence + effort) → Expérimentation (branche feature) → Décision ADR → Implémentation → Documentation.

**Entrées de veille appliquées au projet (synthèse)** :

| ID | Technologie | Découverte | Impact sur TaskForce | ADR |
|---|---|---|---|---|
| VT-001 | Spring Boot 4 + Java 21 Virtual Threads | Oct 2025 | Stack backend — scalabilité I/O-bound native | ADR-001 |
| VT-002 | Groq API (LPU ~150 tokens/s) | Jan 2026 | Smart Assign + Assistant IA sans microservice Python | ADR-004 |
| VT-003 | pgvector 0.7.0 HNSW (< 10ms p95) | Mar 2026 | Recherche vectorielle in-database | ADR-005 |
| VT-004 | SigNoz v0.45 open-source (OTel + ClickHouse) | Fév 2026 | Observabilité sans coût SaaS | ADR-010 |
| VT-005 | OWASP Top 10 2025 + CNIL cookies | Continu | PSSI + gap bannière cookies TF-RGPD-001 | — |
| VT-006 | Next.js 16 + React 19 (Server Actions, Compiler) | Nov 2025 | Stack frontend + App Router | — |

Chaque entrée est documentée avec la date de découverte, la source, l'impact concret sur TaskForce, et la preuve dans le code. La veille OWASP/CNIL est continue et a conduit à l'identification de TF-RGPD-001 (bannière cookies manquante) et TF-SEC-009 (JWT HS512 symétrique — recommandation ANSSI de migrer vers RS256). La [Note Innovation & Distance Critique](../17-veille/Note_Innovation_Distance_Critique.md) documente à la fois les innovations démontrables et les limites connues avec honnêteté.

---

> 🔗 [[Architecture_C4]] — [[CdCF]] — [[CdCT]] — [[Journal_Decisions_ADR]] — [[Veille_Technologique]] —
> [[Note_Innovation_Distance_Critique]] — [[Audit_RGPD_Conformite]] — [[Registre_Traitements_RGPD]]

**Dernière mise à jour :** 05/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
