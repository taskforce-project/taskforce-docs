<!--
Logo établissement : assets/images/logo_metz_numeric_school.sv

g
Logo projet        : assets/images/logo_taskforce.png
-->

# CdCT – Cahier des Charges Technique

**Version :** 1.1  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: CdCT](https://img.shields.io/badge/Type-CdCT-orange?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./01_CdCF.md)
- [CdCT – Cahier des Charges Technique](./02_CdCT.md)
- [Business & Analyse de marché](./Etude_business.md)
- [Stratégie Marketing & Commerciale](./Strategie_Marketing.md)
- [Repository GitHub](https://github.com/...)

**Tags :** `#cdct` `#technique` `#architecture` `#infrastructure` `#devops` `#securite`

<div class="section-intro">

## Sommaire

1. [Introduction et contexte](#1-introduction-et-contexte)
2. [Vue d'ensemble de l'architecture](#2-vue-densemble-de-larchitecture)
3. [Stack technologique](#3-stack-technologique)
4. [Architecture applicative](#4-architecture-applicative)
5. [Modélisation des données](#5-modélisation-des-données)
6. [Infrastructure et déploiement](#6-infrastructure-et-déploiement)
7. [CI/CD et automatisation](#7-cicd-et-automatisation)
8. [Stratégie de tests](#8-stratégie-de-tests)
9. [Sécurité et conformité](#9-sécurité-et-conformité)
10. [Performance et scalabilité](#10-performance-et-scalabilité)
11. [Monitoring et observabilité](#11-monitoring-et-observabilité)

</div>

<div class="section-main">

## 1. Introduction et contexte

### Objet du document

Ce Cahier des Charges Technique (CdCT) définit l'ensemble des spécifications techniques, choix technologiques et architecturaux pour la réalisation de la plateforme Taskforce. Le document s'adresse aux équipes de développement, d'infrastructure et de sécurité, et constitue la référence technique pour l'implémentation du système.

### Périmètre technique

Le périmètre couvre l'architecture applicative complète (front-end, back-end, base de données), l'infrastructure de déploiement (conteneurisation, environnements, réseau), les pipelines CI/CD et automatisation, la sécurité et conformité (authentification, autorisation, chiffrement, audits), et les stratégies de performance, scalabilité et monitoring. Les aspects fonctionnels détaillés sont traités dans le [CdCF](./01_CdCF.md).

### Références documentaires

Ce document s'appuie sur le [Dossier Projet](./Dossier_Projet.md) pour la vision globale et les objectifs, le [CdCF](./01_CdCF.md) pour les spécifications fonctionnelles, et l'[Étude Business](./Etude_business.md) pour les contraintes économiques. Les références techniques incluent la documentation officielle des technologies utilisées (Spring Boot, Next.js, PostgreSQL, Docker, Keycloak, Stripe), les normes de sécurité (OWASP Top 10, ISO 27001), et les bonnes pratiques DevOps.

### Glossaire technique

**API REST** : Interface de programmation applicative respectant les principes REST (Representational State Transfer) avec verbes HTTP standard (GET, POST, PUT, DELETE).

**CI/CD** : Continuous Integration / Continuous Deployment - Pratique d'automatisation des builds, tests et déploiements.

**Container** : Unité logicielle standardisée encapsulant le code et ses dépendances pour une exécution cohérente sur tous environnements.

**JWT** : JSON Web Token - Standard ouvert pour la transmission sécurisée d'informations d'authentification.

**Multi-tenant** : Architecture permettant de servir plusieurs clients (tenants) sur une infrastructure partagée avec isolation stricte des données.

**RBAC** : Role-Based Access Control - Modèle de contrôle d'accès basé sur les rôles utilisateurs.

**SSO** : Single Sign-On - Authentification unique permettant l'accès à plusieurs applications avec un seul jeu d'identifiants.

**ORM** : Object-Relational Mapping - Technique de mapping entre objets applicatifs et tables relationnelles.

</div>

<div class="section-architecture">

## 2. Vue d'ensemble de l'architecture

### Principes architecturaux

L'architecture repose sur plusieurs principes fondamentaux guidant les choix de conception. La **séparation des préoccupations** structure le code en couches distinctes (Présentation, Métier, Persistance) avec responsabilités clairement définies et couplage minimal. L'**architecture modulaire** permet l'isolation du Core applicatif et des modules métier avec interfaces standardisées facilitant l'extensibilité future. La **scalabilité horizontale** anticipe la montée en charge par ajout de ressources parallèles (stateless backend, cache distribué, load balancing). Le **principe de moindre privilège** applique les droits d'accès minimaux nécessaires à chaque acteur et composant. Enfin, la **fail-safe attitude** privilégie la sécurité et la stabilité avec gestion d'erreurs robuste et mécanismes de fallback.

### Vision globale

L'architecture adopte une approche **hybride monolithe modulaire / microservices potentiel**. Le MVP implémente un monolithe modulaire avec Core et Module Gestion de Projet dans une même application Spring Boot, offrant simplicité de développement et déploiement, transactions ACID natives, et debugging facilité. Cette approche est idéale pour une équipe mono-acteur tout en anticipant une éventuelle migration microservices si la croissance le justifie.

Le **front-end** se décompose en Landing Page statique (Astro) pour le marketing et SEO, et Application Web (Next.js) pour les fonctionnalités SaaS avec authentification. Le **back-end** utilise Spring Boot exposant une API REST consommée par le front-end, intégré à Keycloak pour l'authentification et Stripe pour les paiements. La **base de données** PostgreSQL stocke les données métier avec schéma multi-tenant. L'**infrastructure** Docker Compose orchestre les services (backend, frontend, postgres, keycloak, pgadmin) avec séparation stricte des environnements dev/prod.

### Schéma d'architecture général

```yml
┌──────────────────┐         ┌──────────────────┐
│  Landing Page    │         │  Application Web │
│  (Astro - SSG)   │         │  (Next.js - SSR) │
│  Port 3001       │         │  Port 3000       │
└────────┬─────────┘         └────────┬─────────┘
│                            │
│  HTTP/HTTPS                │  HTTP/HTTPS + JWT
│                            │
└────────────┬───────────────┘
│
┌───────▼────────┐
│   Nginx        │
│  (Reverse      │
│   Proxy)       │
└───────┬────────┘
│
┌────────────┼────────────┐
│            │            │
┌────▼─────┐ ┌───▼──────┐ ┌──▼─────────┐
│ Keycloak │ │ Backend  │ │  Stripe    │
│   Auth   │ │SpringBoot│ │ Webhooks   │
│ Port 8180│ │ Port 8080│ │  (Cloud)   │
└────┬─────┘ └───┬──────┘ └────────────┘
│           │
│      ┌────▼────────┐
│      │ PostgreSQL  │
│      │   Port 5432 │
│      └─────────────┘
│
┌────▼──────────┐
│ Keycloak DB   │
│ (Postgres)    │
└───────────────┘
```

### Flux de données principaux

**Authentification** : User → Frontend → Keycloak → JWT Token → Frontend (stockage) → Requêtes API avec JWT → Backend (vérification JWT) → Réponse.

**Création de tâche** : Manager → Frontend (formulaire) → Backend API (validation) → Service Métier (logique) → Repository (persistance) → PostgreSQL → Réponse → Frontend (mise à jour UI).

**Assignation automatique** : Manager (déclenchement) → Backend API → Service Assignation (algorithme) → Lecture BDD (compétences, charge) → Calcul → Proposition → Manager (validation) → Mise à jour BDD → Notifications.

**Paiement Stripe** : User (souscription) → Frontend → Backend (création session Stripe) → Redirect Stripe Payment → User (paiement) → Stripe Webhook → Backend (vérification signature) → Activation abonnement → Confirmation.

</div>

<div class="section-stack">

## 3. Stack technologique

### Choix technologiques globaux

Le choix de la stack privilégie les technologies open source éprouvées, matures et largement adoptées pour bénéficier d'une documentation abondante, d'une communauté active et d'un support long terme. L'expertise du porteur de projet en Java/TypeScript influence également les choix pour maximiser la productivité. La compatibilité avec les exigences réglementaires (RGPD, accessibilité, sécurité) est vérifiée pour chaque technologie retenue.

### Back-end

**Spring Boot 4.0+** (Java 21) constitue le framework back-end pour son écosystème mature et complet, son support natif de l'architecture modulaire, sa robustesse et sa sécurité éprouvées en environnement enterprise, son intégration native avec PostgreSQL et Keycloak, et sa performance optimale pour APIs REST. L'alternative NestJS (TypeScript) a été écartée pour privilégier la robustesse Java en contexte ERP réglementé.

**Gradle avec DSL Kotlin** gère le build et les dépendances avec une configuration concise et typée, une performance supérieure à Maven, et une flexibilité pour les builds complexes.

**Spring Data JPA** simplifie la persistance avec abstraction ORM propre, génération automatique des requêtes basiques, support natif des transactions ACID, et migration facile via Flyway.

**Spring Security + OAuth2** intègre Keycloak pour l'authentification avec support SSO, RBAC standard, et implémentation OWASP Top 10.

### Front-end

**Next.js 16** (React) propulse l'application web avec Server Components réduisant le JS côté client, SSR/SSG hybride optimisant SEO et performance, routing file-based simplifiant la navigation, et écosystème React mature. L'alternative Vue.js/Nuxt a été écartée par préférence de l'expertise React.

**Astro 5.17** génère la landing page statique avec performance optimale (islands architecture), SEO natif excellence, possibilité d'intégrer composants React/Vue au besoin, et build ultra-rapide.

**TypeScript strict** assure la qualité du code front-end avec typage fort éliminant les erreurs runtime, autocomplétion IDE améliorée, refactoring sécurisé, et documentation implicite.

**Zustand** gère le state management client-side avec API simple et minimaliste, performance supérieure à Redux, intégration native React, et bundle size réduit.

**TanStack Query** (React Query) optimise le data fetching avec cache automatique et intelligent, invalidation et revalidation, synchronisation multi-onglets, et offline support.

**Zod** valide les données côté client avec schémas TypeScript-first, validation runtime performante, messages d'erreur personnalisables, et intégration React Hook Form.

**shadcn-ui + Tailwind CSS 4** constituent le design system avec composants accessibles WCAG 2.1 AA, customisation aisée, bundle size optimisé, et adoption rapide.

### Base de données

**PostgreSQL 18** stocke les données métier pour sa robustesse et conformité ACID, son support natif JSON et types avancés, son extensibilité via extensions, sa performance en lecture/écriture, et sa conformité réglementaire (GDPR, audits). L'alternative MongoDB a été écartée au profit d'un modèle relationnel strict adapté à l'ERP.

**Flyway** gère les migrations de schéma avec versionnement SQL clair, rollback possible, validation à la compilation, et traçabilité.

### Authentification

**Keycloak 25** gère l'authentification et les identités avec SSO enterprise-grade, RBAC standard configurables, intégration OAuth2/OIDC, UI admin complète, support 2FA natif, et conformité GDPR. L'alternative Auth0 (SaaS payant) a été écartée pour garder la maîtrise totale des données identité.

### Paiements

**Stripe** traite les paiements et abonnements SaaS avec API moderne et documentation excellente, webhooks fiables pour synchronisation, support SaaS natif (subscriptions, invoices), sécurité PCI-DSS compliant, et écosystème riche.

### Infrastructure

**Docker + Docker Compose** conteneurise et orchestre les services avec portabilité multi-environnements garantie, isolation des services, reproductibilité des environnements, et simplicité pour équipe mono-acteur. L'alternative Kubernetes est anticipée pour la scalabilité future mais surdimensionnée pour le MVP.

**Nginx** sert de reverse proxy avec routing HTTP/HTTPS performant, terminaison SSL/TLS, load balancing futur, et serving assets statiques.

### CI/CD

**GitHub Actions** automatise les workflows avec intégration native GitHub, runners gratuits pour projets open source, marketplace d'actions réutilisables, et configuration YAML simple. L'alternative GitLab CI a été écartée pour rester dans l'écosystème GitHub du projet.

### Monitoring

**Grafana + Prometheus (a définir précisement)** assurent l'observabilité avec visualisations puissantes et configurables, alerting flexible, open source sans coûts, et écosystème d'exporters. L'alternative Datadog (SaaS onéreux) est reportée post-MVP.

### Comparatif des alternatives

Le [Dossier Projet - Section 7](./Dossier_Projet.md) présente le tableau comparatif détaillé des technologies avec justifications complètes des choix et alternatives évaluées (Maven vs Gradle, NestJS vs Spring Boot, Auth0 vs Keycloak, etc.).

</div>

<div class="section-application">

## 4. Architecture applicative

### Architecture modulaire Core + Modules

L'architecture modulaire structure l'application en composants cohérents et faiblement couplés. Le **Core applicatif** regroupe les packages `com.taskforce.tf_api.shared` (configuration globale, exceptions, DTOs communs, sécurité), `com.taskforce.tf_api.core.auth` (authentification, intégration Keycloak), `com.taskforce.tf_api.core.user` (gestion utilisateurs et permissions), `com.taskforce.tf_api.core.organization` (multi-tenant, organisations, équipes), et `com.taskforce.tf_api.core.subscription` (gestion abonnements, intégration Stripe).

Le **Module Gestion de Projet** s'organise en sous-packages `com.taskforce.tf_api.modules.project.api` (controllers REST), `.domain` (entités JPA), `.service` (logique métier), `.repository` (accès DB), et `.dto` (request/response). Ce module couvre les projets, tâches, compétences, assignation automatique, charge de travail, alertes et reporting.

Les **Modules optionnels futurs** (LIMS, Qualité, GED) suivront la même structure avec package dédié `com.taskforce.tf_api.modules.{nom_module}` et interfaces standardisées permettant l'activation/désactivation dynamique via configuration.

### Architecture Front-end

#### Landing Page (Astro)

La landing page utilise Astro avec génération statique (SSG) pour performance maximale, composants Astro natifs + composants React au besoin, styling Tailwind CSS, optimisation SEO automatique (meta tags, sitemap, robots.txt), et déploiement sur CDN.

Structure : `landing-page/src/pages/` (routes), `/components/` (composants réutilisables), `/layouts/` (layouts de page), `/assets/` (images, fonts), et `/styles/` (CSS global).

#### Application Web (Next.js)

L'application web repose sur Next.js 16 avec App Router (structure `app/` file-based), Server Components pour réduire le JS client, Client Components pour interactivité (formulaires, state), API Routes pour endpoints backend-for-frontend si nécessaires, et middleware pour authentification JWT.

Structure : `frontend/app/` (routes et pages), `/components/` (composants UI), `/lib/` (utilities, api clients, stores Zustand), `/hooks/` (custom React hooks), `/public/` (assets statiques), et `/styles/` (Tailwind config).

**State Management** : Zustand gère le state global (user profile, preferences, UI state) avec stores minimaux et performants.

**Data Fetching** : TanStack Query gère les requêtes API avec cache automatique, invalidation intelligente, retry logic, et optimistic updates.

**Validation** : Zod définit les schémas de validation avec intégration React Hook Form, messages d'erreur localisés, et typage TypeScript automatique.

**Design System** : shadcn-ui fournit les composants de base accessibles et customisables, Tailwind CSS 4 assure le styling avec configuration de la design tokens, et les composants respectent WCAG 2.1 AA.

### Architecture Back-end

#### Structure en couches

L'architecture suit le pattern classique en couches avec **Controllers** (package `.api`) exposant les endpoints REST, validant les entrées via `@Valid`, gérant les codes HTTP (200, 201, 400, 401, 403, 404, 500), et retournant des `ApiResponse<T>` standardisées. Les **Services** (package `.service`) encapsulent la logique métier, orchestrent les appels inter-services, gèrent les transactions via `@Transactional`, et sont injectés par constructeur (`@RequiredArgsConstructor`). Les **Repositories** (package `.repository`) étendent `JpaRepository<Entity, ID>`, génèrent automatiquement les CRUD basiques, incluent des requêtes custom JPQL/native au besoin, et gèrent la persistance.

#### API REST et documentation

L'API REST respecte les principes RESTful avec verbes HTTP appropriés (GET lecture, POST création, PUT/PATCH modification, DELETE suppression), URLs ressources (ex: `/api/projects/{id}/tasks`), codes de statut standards, et versionning dans l'URL (`/api/v1/...`).

**OpenAPI / Swagger** documente automatiquement l'API via annotations Spring (`@Operation`, `@ApiResponse`), interface Swagger UI accessible `/swagger-ui.html`, et export OpenAPI JSON `/v3/api-docs`.

**Format de réponse standardisé** :

```json
{
  "status": "success | error",
  "message": "Message descriptif",
  "data": {
    /* payload */
  },
  "timestamp": "2026-02-27T10:30:00Z"
}
```

#### Validation

La validation côté serveur utilise Bean Validation (`@NotNull`, `@Size`, `@Email`, etc.) sur les DTOs, validation déclenchée via `@Valid` dans controllers, messages d'erreur personnalisés dans messages.properties, et gestion globale via `@ControllerAdvice`.

#### Gestion des exceptions

Un `GlobalExceptionHandler` intercepte les exceptions avec mapping vers codes HTTP appropriés, logs structurés pour debugging, messages utilisateur localisés, et stack traces masquées en production.

### Multi-tenant

L'architecture multi-tenant repose sur la **séparation par schéma** (un schéma PostgreSQL par organisation) ou **séparation par colonne** (colonne `organization_id` dans chaque table avec filtre automatique). Le MVP privilégie la séparation par colonne pour simplicité avec un filtre Hibernate automatique (`@Filter`) appliqué sur toutes les entités, identification de l'organisation via JWT (claim `org_id`), et isolation stricte garantie au niveau ORM.

La migration future vers schémas séparés est anticipée pour conformité réglementaire renforcée (21 CFR Part 11) si modules LIMS activés.

### Intégration Keycloak

L'intégration Keycloak utilise Spring Security OAuth2 avec configuration `application.yml` (issuer-uri, client-id, client-secret), validation JWT automatique sur requêtes API, extraction des claims (user_id, roles, org_id), et mapping des rôles Keycloak vers permissions Spring Security.

Flux d'authentification : User → Frontend (formulaire login) → Redirect Keycloak → User (credentials) → Keycloak (vérification) → Redirect Frontend avec Authorization Code → Frontend → Backend (exchange code for JWT) → Backend (validation + création session) → JWT Token → Frontend (stockage sécurisé) → Requêtes avec JWT en header.

### Intégration Stripe

L'intégration Stripe gère les abonnements SaaS avec création de session de paiement via Stripe Checkout, redirection user vers Stripe hébergé, paiement sécurisé PCI-DSS, webhooks Stripe notifiant backend des événements (`checkout.session.completed`, `customer.subscription.updated`, `invoice.payment_failed`), vérification de signature webhook pour sécurité, et mise à jour BDD (statut abonnement, plan actif, limitations).

Configuration : Clés API (`STRIPE_SECRET_KEY`, `STRIPE_PUBLISHABLE_KEY`), webhook signing secret (`STRIPE_WEBHOOK_SECRET`), et endpoints webhook sécurisés (`/api/webhooks/stripe`).

</div>

<div class="section-data">

## 5. Modélisation des données

### Modèle Conceptuel de Données (MCD)

Schéma plus précis à venir, mais voici une première ébauche du MCD.

Le MCD identifie les entités métier et leurs relations conceptuelles sans considération technique.

**Entités principales** :

- **Organisation** (id, nom, planTarifaire, dateCreation)
- **Utilisateur** (id, email, nom, prenom, roles)
- **Équipe** (id, nom, description)
- **Projet** (id, nom, description, dateDebut, dateFin, statut)
- **Tâche** (id, titre, description, priorite, estimation, statut)
- **Compétence** (id, libelle, domaine, categorie)
- **Abonnement** (id, stripeSubscriptionId, plan, statut, montant)
- **Module** (id, nom, description, actif)

**Relations** :

- Organisation (1,n) — (0,n) Équipe
- Équipe (1,n) — (0,n) Utilisateur
- Organisation (1,1) — (0,1) Abonnement
- Projet (1,n) — (0,n) Tâche
- Utilisateur (1,n) — (0,n) Tâche (affectation)
- Tâche (0,n) — (0,n) Compétence (requiert)
- Utilisateur (0,n) — (0,n) Compétence (possède avec niveau)
- Organisation (0,n) — (0,n) Module (activation)

**[Diagramme MCD à intégrer]**

### Modèle Logique de Données (MLD)

Schéma plus détaillé à venir, mais voici une première ébauche du MLD.

Le MLD traduit le MCD en modèle relationnel avec tables, clés primaires et étrangères.

**Tables principales** :

```sql
organizations (
  id UUID PK,
  name VARCHAR(255) NOT NULL,
  plan_type ENUM('GRATUIT', 'PRO', 'ENTERPRISE'),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
)

users (
  id UUID PK,
  email VARCHAR(255) UNIQUE NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  organization_id UUID FK → organizations,
  keycloak_id VARCHAR(255) UNIQUE,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

teams (
  id UUID PK,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  organization_id UUID FK → organizations,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

projects (
  id UUID PK,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  start_date DATE,
  end_date DATE,
  status ENUM('PLANIFICATION', 'ACTIF', 'SUSPENDU', 'CLOTURE'),
  organization_id UUID FK → organizations,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

tasks (
  id UUID PK,
  title VARCHAR(500) NOT NULL,
  description TEXT,
  priority ENUM('BASSE', 'NORMALE', 'HAUTE', 'CRITIQUE'),
  estimated_hours DECIMAL(5,2),
  status ENUM('BROUILLON', 'EN_ATTENTE', 'EN_COURS', 'TERMINEE', 'ARCHIVEE'),
  project_id UUID FK → projects,
  assigned_to UUID FK → users,
  organization_id UUID FK → organizations,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

skills (
  id UUID PK,
  label VARCHAR(255) NOT NULL,
  domain VARCHAR(100),
  category VARCHAR(100),
  organization_id UUID FK → organizations,
  created_at TIMESTAMP
)

user_skills (
  user_id UUID FK → users,
  skill_id UUID FK → skills,
  level ENUM('DEBUTANT', 'INTERMEDIAIRE', 'CONFIRME', 'EXPERT'),
  PRIMARY KEY (user_id, skill_id)
)

task_skills (
  task_id UUID FK → tasks,
  skill_id UUID FK → skills,
  required_level ENUM('DEBUTANT', 'INTERMEDIAIRE', 'CONFIRME', 'EXPERT'),
  PRIMARY KEY (task_id, skill_id)
)

subscriptions (
  id UUID PK,
  organization_id UUID FK → organizations UNIQUE,
  stripe_subscription_id VARCHAR(255) UNIQUE,
  stripe_customer_id VARCHAR(255),
  plan ENUM('GRATUIT', 'PRO', 'ENTERPRISE'),
  status ENUM('ESSAI', 'ACTIF', 'SUSPENDU', 'RESILIE'),
  current_period_end TIMESTAMP,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

organization_modules (
  organization_id UUID FK → organizations,
  module_id UUID FK → modules,
  activated_at TIMESTAMP,
  PRIMARY KEY (organization_id, module_id)
)

modules (
  id UUID PK,
  name VARCHAR(100) UNIQUE NOT NULL,
  description TEXT,
  available_for_plans ENUM[] ('PRO', 'ENTERPRISE'),
  created_at TIMESTAMP
)
```

**[Diagramme MLD à intégrer]**

### Modèle Physique de Données (MPD)

Le MPD spécifie l'implémentation PostgreSQL avec types de données précis, indexes, contraintes et optimisations.

**Types PostgreSQL** : UUID pour les clés primaires (génération côté Hibernate), VARCHAR avec limites appropriées, TEXT pour contenus longs, TIMESTAMP WITH TIME ZONE pour dates, DECIMAL pour précision monétaire, et ENUM PostgreSQL pour types énumérés.

**Index** : Index sur foreign keys pour jointures performantes, index composés sur (organization_id, ...) pour requêtes multi-tenant, index sur colonnes de recherche fréquente (email, status, dates), et index BTREE par défaut.

**Contraintes** : CHECK constraints sur enumerations, UNIQUE constraints sur emails et IDs externes, NOT NULL sur champs obligatoires, et ON DELETE CASCADE/RESTRICT selon logique métier.

**Partitionnement** : Anticipé pour scalabilité future avec partitionnement horizontal par organization_id et archivage automatique des données anciennes (projets clôturés > 1 an).

**[Schéma MPD à intégrer]**

### Migrations

**Flyway** gère les migrations de schéma avec fichiers SQL versionnés `V1__Initial_schema.sql`, `V2__Add_modules_table.sql`, etc., exécution automatique au démarrage de l'application, validation de l'ordre et checksum, et rollback manuel si nécessaire.

Structure : `backend/tf-api/src/main/resources/db/migration/` contient les scripts SQL ordonnés. Chaque migration est atomique et testée en développement avant merge.

### Audit et traçabilité

Toutes les entités étendent `AuditableEntity` avec champs `createdAt`, `updatedAt`, `createdBy`, `updatedBy` gérés automatiquement par Spring Data JPA Auditing. Les actions sensibles (suppression, changement permissions, paiements) sont logguées dans une table `audit_logs` dédiée avec user_id, action, resource, timestamp, details JSON, et IP address.

</div>

<div class="section-infrastructure">

## 6. Infrastructure et déploiement

### Architecture infrastructure

L'infrastructure repose sur Docker avec orchestration Docker Compose pour simplifier le déploiement multi-services. La séparation stricte des environnements (dev, prod) utilise des fichiers de configuration dédiés (`docker-compose.dev.yml`, `docker-compose.prod.yml`, `.env.dev`, `.env.prod`).

**Environnement DEV** : Configurations permissives pour debugging (logs verbeux, hot-reload, ports exposés), données de test pré-chargées, outils de développement activés (Swagger UI, pgAdmin), et utilisation de localhost pour communication inter-services hors Docker.

**Environnement PROD** : Configurations sécurisées (secrets externalisés, logs structurés), terminaison SSL/TLS via Let's Encrypt, ports minimaux exposés, monitoring actif (Prometheus, Grafana), backups automatisés, et communication inter-services via noms Docker.

### Conteneurisation

**Docker** conteneurise chaque service avec image de base optimisée (ex: `eclipse-temurin:21-jre` pour backend Java, `node:22-alpine` pour frontend), multi-stage builds pour images légères, configuration via variables d'environnement, volumes pour persistence (base de données, uploads), et healthchecks pour monitoring.

Exemple Dockerfile backend :

```dockerfile
peut être mettre un exemple
```

### Orchestration Docker Compose

Docker Compose orchestre les services avec dépendances (`depends_on`), réseaux privés (`backend-network`), volumes nommés persistents, et variables d'environnement par fichier `.env`.

Services définis :

- **postgres** : Base de données (PostgreSQL 18, volume `postgres-data`, réseau backend)
- **keycloak** : Authentification (port 8180, volume `keycloak-data`, BDD Postgres dédiée)
- **backend** : API Spring Boot (port 8080, dépend de postgres + keycloak)
- **frontend** : App Next.js (port 3000, dépend de backend)
- **landing** : Site Astro (port 3001, indépendant)
- **pgadmin** : Admin DB (port 5050, DEV uniquement)
- **nginx** : Reverse proxy (ports 80/443, PROD uniquement)

### Gestion des secrets

Les secrets sont externalisés hors du code avec fichiers `.env` (gitignored), variables d'environnement injectées à runtime, secrets sensibles chiffrés en production (Vault ou AWS Secrets Manager à terme), et rotation régulière des credentials.

Configuration : `.env.example` versionné comme template, `.env.dev` et `.env.prod` locaux non versionnés, et documentation des variables requises dans README.

### Networking

Les services communiquent via réseau Docker privé avec résolution DNS automatique (nom du service = hostname), isolation réseau (frontend ne peut pas accéder directement à postgres), exposition sélective des ports vers l'hôte, et reverse proxy Nginx en production pour routage et SSL termination.

Configuration réseau :

```yaml
networks:
  backend-network:
    driver: bridge
  frontend-network:
    driver: bridge
```

### Volumes et persistence

Les données persistantes utilisent volumes nommés Docker avec `postgres-data` pour la base de données, `keycloak-data` pour Keycloak, `uploads` pour fichiers utilisateurs, et backups montés depuis l'hôte pour sauvegarde externe.

Politique de backup : Dumps quotidiens de PostgreSQL (script `pg_dump`), rotation 30 jours, copie sur S3 ou équivalent, et tests de restauration mensuels.

### Scalabilité et haute disponibilité

Le MVP cible une instance unique par service suffit pour charge anticipée (100 utilisateurs simultanés). La scalabilité future anticipe load balancing Nginx (round-robin, least connections), multiples instances backend stateless, cache distribué Redis pour sessions et données fréquentes, BDD en read replica pour répartir lectures, et migration Kubernetes pour orchestration avancée si croissance forte.

</div>

<div class="section-cicd">

## 7. CI/CD et automatisation

### Pipelines GitHub Actions

Les workflows GitHub Actions automatisent les processus de build, test et déploiement avec déclenchement automatique sur push/PR, runners GitHub gratuits, et feedback immédiat via checks et commentaires PR.

**Workflow Backend** (`.github/workflows/backend.yml`) :

1. Checkout code
2. Setup Java 21 + Gradle
3. Linter et formatage (Spotless check)
4. Build (`gradle build`)
5. Tests unitaires + intégration (`gradle test`)
6. Couverture de code (JaCoCo report)
7. Analyse SonarQube si configuré
8. Build image Docker
9. Push Docker registry (GHCR) si branche main

**Workflow Frontend** (`.github/workflows/frontend.yml`) :

1. Checkout code
2. Setup Node.js 22
3. Install dependencies (`npm ci`)
4. Linter ESLint (`npm run lint`)
5. Build Next.js (`npm run build`)
6. Tests Vitest (`npm test`)
7. Build image Docker
8. Push Docker registry si branche main

**Workflow E2E** (`.github/workflows/e2e.yml`) :

1. Spin up stack Docker Compose
2. Tests E2E Playwright
3. Capture screenshots/vidéos si échec
4. Upload artifacts

### Déploiement automatisé

Le déploiement production est déclenché manuellement avec approbation requise, workflow dédié `.github/workflows/deploy-prod.yml`, pull images Docker depuis GHCR, connexion SSH au serveur de production, docker-compose pull + up avec zero-downtime, smoke tests post-déploiement, et rollback automatique si tests échouent.

### Gestion des versions

Le versionnement suit Semantic Versioning (MAJOR.MINOR.PATCH) avec tags Git (v1.0.0, v1.1.0, v1.0.1), génération automatique du changelog, release notes sur GitHub Releases, et images Docker taguées par version + latest.

### Environnements de déploiement

Trois environnements sont maintenus : **dev** (mise à jour automatique sur push main, données de test, debugging activé), **staging** (mirror de prod, déploiement manuel, tests de validation), et **prod** (déploiement manuel avec approbation, monitoring actif, backups automatiques).

</div>

<div class="section-testing">

## 8. Stratégie de tests

### Philosophie et objectifs

La stratégie de tests suit la pyramide de tests avec une base solide de tests unitaires (70% des tests), des tests d'intégration ciblés (20%), et des tests E2E critiques (10%). L'objectif est de garantir la qualité du code, détecter les régressions tôt dans le cycle de développement, valider les fonctionnalités critiques métier, et assurer la maintenabilité du code. Les tests sont exécutés automatiquement dans les pipelines CI/CD avec feedback immédiat sur les Pull Requests.

### Tests Back-end

#### Tests unitaires (JUnit 5 + Mockito)

Les tests unitaires ciblent les services métier et la logique applicative avec isolation complète via mocks Mockito, un test par méthode publique en moyenne, une couverture minimale de 70% pour les services critiques (auth, assignation, paiements), et une structure Given-When-Then pour lisibilité.

**Structure standard** :

```java
@ExtendWith(MockitoExtension.class)
public class TaskServiceTest {

    @Mock
    private TaskRepository taskRepository;

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private TaskService taskService;

    @BeforeEach
    void setUp() {
        // Setup commun
    }

    @Test
    void createTask_ShouldReturnTask_WhenValidRequest() {
        // Given (Arrange)
        CreateTaskRequest request = new CreateTaskRequest(...);
        when(taskRepository.save(any())).thenReturn(mockTask);

        // When (Act)
        Task result = taskService.createTask(request);

        // Then (Assert)
        assertThat(result).isNotNull();
        assertThat(result.getTitle()).isEqualTo("Task title");
        verify(taskRepository).save(any());
    }

    @Test
    void createTask_ShouldThrowException_WhenProjectNotFound() {
        // Test des cas d'erreur
    }
}
```

**Outils** : JUnit 5 (annotations `@Test`, `@BeforeEach`, `@ParameterizedTest`), Mockito (`@Mock`, `@InjectMocks`, `when()`, `verify()`), AssertJ pour assertions fluides (`assertThat()`), et MockMvc pour tests controllers sans serveur.

**Commandes** :

```bash
# Lancer tous les tests unitaires
./mvnw test

# Lancer une classe spécifique
./mvnw test -Dtest=TaskServiceTest

# Lancer avec couverture
./mvnw clean test jacoco:report
```

#### Tests d'intégration (Spring Boot Test)

Les tests d'intégration valident l'interaction entre composants avec contexte Spring complet, base de données H2 en mémoire ou Testcontainers PostgreSQL, transactions rollback automatique après chaque test, et validation des repositories et requêtes custom.

**Structure** :

```java
@SpringBootTest
@Transactional
public class TaskRepositoryIntegrationTest {

    @Autowired
    private TaskRepository taskRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    void findByProjectId_ShouldReturnTasks_WhenProjectExists() {
        // Given
        Project project = createProject();
        Task task1 = createTask(project);
        Task task2 = createTask(project);
        entityManager.flush();

        // When
        List<Task> tasks = taskRepository.findByProjectId(project.getId());

        // Then
        assertThat(tasks).hasSize(2);
        assertThat(tasks).extracting("title")
            .containsExactlyInAnyOrder(task1.getTitle(), task2.getTitle());
    }
}
```

**Types de tests d'intégration** : Tests repositories (requêtes JPQL/native), tests controllers (MockMvc avec contexte complet), tests services avec dépendances réelles, et tests sécurité (authentification, autorisation).

**Annotations clés** : `@SpringBootTest` (contexte complet), `@WebMvcTest` (controllers uniquement), `@DataJpaTest` (repositories JPA), `@Transactional` (rollback automatique), et `@Testcontainers` (PostgreSQL conteneurisé).

#### Couverture de code (JaCoCo)

JaCoCo mesure la couverture de code avec génération automatique de rapports HTML, objectifs configurables par package, et échec du build si seuil non atteint.

**Objectifs de couverture** :

- Services métier : **≥ 70%**
- Controllers : **≥ 60%**
- Repositories : **≥ 50%** (requêtes custom)
- DTOs/Entities : **Optionnel** (pas de logique)
- Code global : **≥ 65%**

**Configuration** (`pom.xml`) :

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
        <execution>
            <id>jacoco-check</id>
            <goals>
                <goal>check</goal>
            </goals>
            <configuration>
                <rules>
                    <rule>
                        <element>PACKAGE</element>
                        <limits>
                            <limit>
                                <counter>LINE</counter>
                                <value>COVEREDRATIO</value>
                                <minimum>0.70</minimum>
                            </limit>
                        </limits>
                    </rule>
                </rules>
            </configuration>
        </execution>
    </executions>
</plugin>
```

**Rapport** : Généré dans `target/site/jacoco/index.html` avec visualisation par package, classe et ligne.

### Tests Front-end

#### Tests unitaires (Vitest + React Testing Library)

Les tests unitaires frontend valident les composants React avec rendu isolé, simulation interactions utilisateur, vérification accessibilité, et couverture ≥ 60%.

**Structure** :

```typescript
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import { describe, it, expect, vi } from 'vitest';
import { LoginForm } from './LoginForm';

describe('LoginForm', () => {
  it('should render email and password fields', () => {
    render(<LoginForm />);

    expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/mot de passe/i)).toBeInTheDocument();
    expect(screen.getByRole('button', { name: /se connecter/i })).toBeInTheDocument();
  });

  it('should show validation error for invalid email', async () => {
    render(<LoginForm />);

    const emailInput = screen.getByLabelText(/email/i);
    fireEvent.change(emailInput, { target: { value: 'invalid-email' } });
    fireEvent.blur(emailInput);

    await waitFor(() => {
      expect(screen.getByText(/email invalide/i)).toBeInTheDocument();
    });
  });

  it('should call onSubmit with form data when valid', async () => {
    const mockSubmit = vi.fn();
    render(<LoginForm onSubmit={mockSubmit} />);

    fireEvent.change(screen.getByLabelText(/email/i), {
      target: { value: 'test@example.com' }
    });
    fireEvent.change(screen.getByLabelText(/mot de passe/i), {
      target: { value: 'password123' }
    });
    fireEvent.click(screen.getByRole('button', { name: /se connecter/i }));

    await waitFor(() => {
      expect(mockSubmit).toHaveBeenCalledWith({
        email: 'test@example.com',
        password: 'password123'
      });
    });
  });
});
```

**Outils** : Vitest (runner de tests, compatible ESM), React Testing Library (rendu composants, queries accessibles), @testing-library/user-event (simulation interactions réalistes), et MSW (Mock Service Worker) pour mocker les API.

**Commandes** :

```bash
# Lancer tests
npm test

# Mode watch
npm test -- --watch

# Avec couverture
npm test -- --coverage

# UI interactive
npm test -- --ui
```

#### Tests d'intégration API (MSW)

MSW (Mock Service Worker) intercepte les requêtes API et retourne des réponses mockées avec simulation réaliste du comportement backend, tests des états loading/success/error, et validation du flow complet utilisateur.

**Configuration** :

```typescript
import { setupServer } from "msw/node";
import { http, HttpResponse } from "msw";

const handlers = [
  http.post("/api/auth/login", () => {
    return HttpResponse.json({
      status: "success",
      data: {
        token: "fake-jwt-token",
        user: { id: "1", email: "test@example.com" },
      },
    });
  }),

  http.get("/api/projects", () => {
    return HttpResponse.json({
      status: "success",
      data: [{ id: "1", name: "Projet Test" }],
    });
  }),
];

export const server = setupServer(...handlers);
```

#### Tests accessibilité (axe-core)

Les tests d'accessibilité valident automatiquement la conformité WCAG avec intégration vitest-axe, vérification contrastes/labels/ARIA, et exécution dans CI/CD.

```typescript
import { axe, toHaveNoViolations } from 'vitest-axe';

expect.extend(toHaveNoViolations);

it('should have no accessibility violations', async () => {
  const { container } = render(<LoginForm />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

### Tests End-to-End (Playwright)

Les tests E2E valident les parcours utilisateurs critiques avec navigateurs réels (Chromium, Firefox, WebKit), interactions complètes (clic, saisie, navigation), et validation fonctionnelle bout en bout.

**Scénarios prioritaires** :

1. **Authentification** : Login/Logout, création compte, reset password
2. **Gestion projets** : Créer/éditer/archiver projet
3. **Gestion tâches** : Créer tâche, assigner collaborateur, changer statut
4. **Assignation automatique** : Déclencher assignation, valider proposition, confirmer
5. **Abonnement** : Sélectionner plan, payer (Stripe test mode), activation compte

**Structure** :

```typescript
import { test, expect } from "@playwright/test";

test.describe("Task Management", () => {
  test.beforeEach(async ({ page }) => {
    // Login
    await page.goto("http://localhost:3000/auth/login");
    await page.fill('input[name="email"]', "manager@test.com");
    await page.fill('input[name="password"]', "password123");
    await page.click('button[type="submit"]');
    await expect(page).toHaveURL(/\/dashboard/);
  });

  test("should create a new task", async ({ page }) => {
    await page.goto("http://localhost:3000/projects/1");
    await page.click('button:has-text("Nouvelle tâche")');

    await page.fill('input[name="title"]', "Implémenter API REST");
    await page.fill(
      'textarea[name="description"]',
      "Endpoints CRUD pour projets",
    );
    await page.selectOption('select[name="priority"]', "HAUTE");
    await page.fill('input[name="estimatedHours"]', "8");

    await page.click('button[type="submit"]');

    await expect(page.locator("text=Tâche créée avec succès")).toBeVisible();
    await expect(page.locator("text=Implémenter API REST")).toBeVisible();
  });

  test("should assign task to collaborator", async ({ page }) => {
    await page.goto("http://localhost:3000/tasks/1");
    await page.click('button:has-text("Assigner")');
    await page.selectOption('select[name="assignee"]', "user-123");
    await page.click('button:has-text("Confirmer")');

    await expect(page.locator("text=Tâche assignée")).toBeVisible();
  });
});
```

**Configuration** (`playwright.config.ts`) :

```typescript
import { defineConfig } from "@playwright/test";

export default defineConfig({
  testDir: "./e2e",
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  reporter: "html",
  use: {
    baseURL: "http://localhost:3000",
    trace: "on-first-retry",
    screenshot: "only-on-failure",
  },
  projects: [
    {
      name: "chromium",
      use: { browserName: "chromium" },
    },
    {
      name: "firefox",
      use: { browserName: "firefox" },
    },
  ],
  webServer: {
    command: "docker-compose -f docker-compose.dev.yml up",
    url: "http://localhost:3000",
    reuseExistingServer: !process.env.CI,
  },
});
```

**Commandes** :

```bash
# Lancer tests E2E
npx playwright test

# Mode UI interactif
npx playwright test --ui

# Debug mode
npx playwright test --debug

# Générer rapport HTML
npx playwright show-report
```

### Tests de sécurité

#### Scan OWASP ZAP

OWASP ZAP (Zed Attack Proxy) effectue des scans de sécurité automatisés avec détection vulnérabilités OWASP Top 10, exécution dans CI/CD sur environnement staging, et rapports HTML/JSON des findings.

**Workflow GitHub Actions** :

```yaml
- name: OWASP ZAP Scan
  uses: zaproxy/action-full-scan@v0.4.0
  with:
    target: "http://staging.taskforce.app"
    rules_file_name: ".zap/rules.tsv"
    cmd_options: "-a"
```

#### Scan de dépendances (Dependabot + Snyk)

Dependabot GitHub scanne les vulnérabilités dans les dépendances Maven/npm avec alertes automatiques sur CVE, Pull Requests automatiques pour mises à jour de sécurité, et monitoring continu. Snyk (optionnel) complète avec analyse plus approfondie et suggestions de remédiation.

**Configuration** (`.github/dependabot.yml`) :

```yaml
version: 2
updates:
  - package-ecosystem: "maven"
    directory: "/backend/tf-api"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5

  - package-ecosystem: "npm"
    directory: "/frontend"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5
```

### Tests de performance

#### Tests de charge (JMeter ou k6)

Les tests de charge valident la scalabilité de l'API avec simulation de charge progressive (10 → 100 → 500 utilisateurs), mesure temps de réponse sous charge, identification bottlenecks (BDD, CPU, mémoire), et validation objectifs performance (p95 < 500ms).

**Scénarios** :

- Authentification (login massif)
- Consultation projets/tâches (lecture)
- Création tâches (écriture)
- Assignation automatique (calcul intensif)

**Outils** : JMeter (Java, UI riche) ou k6 (JavaScript, moderne, CI-friendly).

#### Monitoring performance continue

Le monitoring intègre Prometheus collectant métriques latency/throughput en production, alertes si dégradation (p95 > seuil), et dashboards Grafana pour analyse tendances.

### Intégration CI/CD

Les tests s'intègrent dans les pipelines GitHub Actions avec exécution automatique sur chaque Push/PR, feedback immédiat via checks GitHub, blocage merge si tests échouent ou couverture insuffisante, et rapports détaillés en artifacts.

**Workflow résumé** :

```yaml
name: Tests

on: [push, pull_request]

jobs:
  backend-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Java 21
        uses: actions/setup-java@v3
      - name: Run Tests
        run: ./mvnw clean test
      - name: JaCoCo Report
        run: ./mvnw jacoco:report
      - name: Upload Coverage
        uses: codecov/codecov-action@v3

  frontend-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node 22
        uses: actions/setup-node@v3
      - name: Install Dependencies
        run: npm ci
      - name: Run Tests
        run: npm test -- --coverage
      - name: Upload Coverage
        uses: codecov/codecov-action@v3

  e2e-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Docker
        run: docker-compose -f docker-compose.dev.yml up -d
      - name: Run Playwright
        run: npx playwright test
      - name: Upload Artifacts
        uses: actions/upload-artifact@v3
        if: failure()
        with:
          name: playwright-report
          path: playwright-report/
```

### Documentation et bonnes pratiques

Les bonnes pratiques incluent des tests lisibles (nommage explicite `should...When...`), des tests atomiques (un concept par test), une couverture des cas limites (edge cases, erreurs), des mocks minimaux (tester comportement réel si possible), un refactoring régulier des tests (éviter duplication), et une documentation inline (commentaires si logique complexe).

</div>

<div class="section-security">

## 9. Sécurité et conformité

### Authentification et autorisation

L'authentification utilise Keycloak comme Identity Provider avec OAuth2/OIDC, SSO pour expérience unifiée, tokens JWT avec expiration journalière, refresh tokens pour renouvellement, et logout propre (invalidation côté Keycloak).

L'autorisation s'appuie sur RBAC (Role-Based Access Control) avec rôles définis dans Keycloak (COLLABORATOR, MANAGER, ADMIN), permissions mappées dans Spring Security, vérification à chaque requête API via `@PreAuthorize`, et multi-tenant filtering automatique (colonne organization_id).

### Sécurité des communications

Les communications sont sécurisées par TLS 1.3 en production (certificats Let's Encrypt), HTTPS strict (redirect HTTP → HTTPS), CORS configuré restrictif (origins autorisées uniquement), headers de sécurité (HSTS, CSP, X-Frame-Options, X-Content-Type-Options), et cookies sécurisés (HttpOnly, Secure, SameSite).

### Protection contre les vulnérabilités OWASP Top 10

**Injection** : Requêtes paramétrées uniquement (JPA/JPQL), validation stricte des entrées, échappement automatique des sorties, et interdiction SQL brut.

**Broken Authentication** : Keycloak robuste et maintenu, tokens JWT signés et vérifiés, expiration courte tokens, et 2FA optionnel.

**Sensitive Data Exposure** : Chiffrement TLS en transit, chiffrement base de données au repos, hashing bcrypt pour passwords (géré Keycloak), masquage données sensibles dans logs, et pas de secrets dans code/Git.

**XML External Entities (XXE)** : Parsing XML désactivé ou sécurisé, validation stricte XML si nécessaire, préférence JSON sur XML.

**Broken Access Control** : Vérification permissions chaque endpoint, multi-tenant filtering automatique, tests compliance permissions, et audit logs actions sensibles.

**Security Misconfiguration** : Configuration par défaut durcie, environnements séparés (dev/prod), secrets externalisés, mises à jour régulières dépendances, et désactivation endpoints sensibles prod (Swagger, Actuator).

**Cross-Site Scripting (XSS)** : Échappement automatique React, CSP headers stricts, validation Zod côté client, et sanitization DOMPurify si HTML utilisateur.

**Insecure Deserialization** : Pas de deserialization non sécurisée, validation stricte JSON, et restriction types acceptés.

**Using Components with Known Vulnerabilities** : Scan Dependabot GitHub, mises à jour régulières, monitoring CVE liées aux technos, et remplacement librairies abandonnées.

**Insufficient Logging & Monitoring** : Logs structurés JSON, audit trail actions sensibles, monitoring Prometheus/Grafana, alerting anomalies, et rotation logs.

### Conformité RGPD

La conformité RGPD implémente le consentement explicite (cookies, traitement données), la minimisation de collecte (données strictement nécessaires), la portabilité (export données utilisateur JSON/CSV), le droit à l'oubli (anonymisation ou suppression), la sécurité by design (chiffrement, accès contrôlés), la transparence (politique de confidentialité claire), et les audits réguliers.

Implémentation technique : Endpoint `/api/users/me/export-data` (portabilité), endpoint `/api/users/me/delete-account` (droit à l'oubli), bannière cookies avec consentement explicite, et documentation privacy policy accessible.

### Conformité accessibilité

L'accessibilité WCAG 2.1 niveau AA garantit la navigation clavier complète (tabindex, focus visible), le support lecteurs d'écran (ARIA labels, roles, live regions), les contrastes conformes (4.5:1 minimum), les tailles texte ajustables, les formulaires accessibles (labels, errors, hints), et les tests automatisés (axe-core CI/CD) complétés de tests manuels.

Le RGAA complète avec spécificités françaises, déclaration accessibilité publiée, et schéma pluriannuel à définir.

### Audit et traçabilité

L'audit système enregistre les connexions/déconnexions utilisateurs, les actions sensibles (création/suppression/modification ressources critiques), les changements de permissions/rôles, les tentatives d'accès refusées, et les erreurs système critiques. Le format des logs est structuré JSON avec timestamp, user_id, organization_id, action, resource, details, et IP address. La rétention est de 1 an minimum avec archivage long terme.

### Tests de sécurité

Les tests de sécurité incluent des tests automatisés OWASP ZAP dans CI/CD, des scans de dépendances Dependabot, des audits manuels périodiques (penetration testing léger), des code reviews sécurité sur PRs sensibles, et des mises à jour proactives des dépendances vulnérables. (Sonarqube)

</div>

<div class="section-performance">

## 10. Performance et scalabilité

### Objectifs de performance

Les objectifs ciblent des temps de réponse API inférieurs à 200ms (p50) et 500ms (p95) pour endpoints simples, inférieurs à 1s (p95) pour endpoints complexes (assignation automatique, rapports), un temps de chargement initial page inférieur à 3s (Desktop) et 5s (Mobile 3G), et un support de 100 utilisateurs simultanés en MVP avec architecture scalable à 1000+.

### Optimisations Back-end

Les optimisations back-end utilisent des indexes PostgreSQL sur colonnes fréquemment requêtées, des requêtes JPQL optimisées (fetch joins, projections), une pagination systématique pour listes (Spring Data Pageable), un cache applicatif pour données statiques (Redis), batch operations pour traitements en masse.

### Optimisations Front-end

Les optimisations front-end implémentent Server Components Next.js réduisant le JS client, le code splitting automatique (lazy loading routes), l'optimisation images Next.js (WebP, sizes, lazy), le cache TanStack Query réduisant requêtes API redondantes, l'optimistic updates pour UX fluide, le debouncing recherches et inputs, et le bundle analysis régulier pour réduire la taille.

### Stratégies de cache

Le cache est géré à plusieurs niveaux : cache navigateur pour assets statiques (headers Cache-Control), cache TanStack Query pour données API côté client, cache applicatif Spring Boot (Caffeine) pour données référentielles, cache distribué Redis (futur) pour sessions et données partagées, et cache PostgreSQL (query cache, shared buffers).

### Monitoring performance

Le monitoring utilise Prometheus collectant métriques backend (throughput, latency, errors), Grafana visualisant dashboards performance, alerts sur dégradations (latency > seuil), et logs slow queries PostgreSQL (> 1s).

### Scalabilité horizontale

La scalabilité horizontale anticipe load balancing Nginx entre multiples instances backend, backend stateless (sessions dans Redis/JWT), BDD read replicas pour répartir lectures, cache distribué Redis partageant état entre instances, et migration Kubernetes pour orchestration avancée si besoin.

</div>

<div class="section-monitoring">

## 11. Monitoring et observabilité

### Stack de monitoring

La stack repose sur Prometheus pour collecte métriques (scraping endpoints `/actuator/prometheus`), Grafana pour visualisation dashboards et alerting, Loki pour agrégation logs (futur), et Tempo pour tracing distribué (futur).

### Métriques clés

Les métriques collectées incluent des métriques applicatives (throughput API requests/sec, latency par endpoint p50/p95/p99, error rate %, charge CPU/memory), des métriques métier (utilisateurs actifs, projets/tâches créés, assignations automatiques déclenchées, paiements Stripe), et des métriques infrastructure (CPU/memory containers, disk I/O, network traffic, database connections pool).

### Dashboards Grafana

Les dashboards Grafana couvrent le dashboard Application (overview métrique clés, throughput, latency, errors), le dashboard Infrastructure (ressources système, containers health, database stats), le dashboard Business (utilisateurs actifs, croissance projets, revenus), et le dashboard Security (tentatives connexion échouées, accès refusés, anomalies).

### Alerting

L'alerting configure des alertes sur métriques critiques (API error rate > 5%, latency p95 > 1s, CPU > 80%, disk usage > 85%, database connection pool exhausted) avec notifications via email/Slack, escalade si non-résolu sous 30 min, et runbooks documentant procédures de résolution.

### Logs structurés

Les logs utilisent un format JSON structuré avec timestamp, level (INFO, WARN, ERROR), logger (nom classe), message, user_id (si applicable), organization_id (multi-tenant), trace_id (pour correlation), et stack_trace (si ERROR). La centralisation avec Loki ou ELK est anticipée post-MVP pour recherche et analyse avancée. La rétention est de 30 jours en production avec archivage long terme des ERROR.

### Healthchecks

Les healthchecks exposent `/actuator/health` (Spring Boot Actuator) avec statut UP/DOWN, vérification dépendances (database, Keycloak), intégration Docker HEALTHCHECK, et monitoring externe (UptimeRobot ou équivalent) pingant endpoint chaque minute.

### Tracing distribué

Le tracing distribué est anticipé avec OpenTelemetry + Tempo pour tracer requêtes à travers microservices (si migration future), identifier bottlenecks, et debugger anomalies complexes. Non implémenté au MVP (monolithe simplifie le debugging).

</div>

<div class="section-conclusion">

## Conclusion

Ce Cahier des Charges Technique établit les fondations technologiques solides de la plateforme Taskforce en privilégiant des technologies open source éprouvées, une architecture modulaire extensible, et le respect des standards de qualité et de sécurité. L'approche hybride monolithe modulaire pour le MVP assure simplicité et productivité tout en anticipant une scalabilité future vers microservices si nécessaire.

Les choix technologiques (Spring Boot, Next.js, PostgreSQL, Keycloak, Docker) offrent un équilibre optimal entre robustesse, performance et maintenabilité, tout en respectant les contraintes projet (équipe mono-acteur, calendrier académique, budget limité). La conformité réglementaire (RGPD, WCAG, OWASP) est intégrée dès la conception guarantissant une base solide pour les évolutions futures.

L'implémentation suivra une démarche agile avec validation progressive, automatisation maximale via CI/CD, et monitoring continu pour garantir qualité et disponibilité. Les spécifications fonctionnelles détaillées sont disponibles dans le [CdCF](./01_CdCF.md), tandis que la vision globale et le pilotage projet sont présentés dans le [Dossier Projet](./Dossier_Projet.md).

</div>

**Dernière mise à jour :** 27/02/2026  
**Version :** 1.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
