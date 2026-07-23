---
type: memoire-rncp
bloc: 4
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc4, deploiement, devops, supervision]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 4 — Déployer et maintenir en production

**Version :** 1.0  
**Date :** 05/07/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 4](https://img.shields.io/badge/Bloc-4%20D%C3%A9ploiement-blue?style=for-the-badge)]() [![Statut: Validé](https://img.shields.io/badge/Statut-Valid%C3%A9-green?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture §5 (infra)](../03-architecture/Architecture.md) · [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) · [GHCR](../06-infra/docker/GHCR_USAGE.md)

**Tags :** `#memoire` `#bloc4` `#deploiement` `#devops` `#supervision`

<p class="lead">
Ce bloc couvre la documentation technique, le déploiement et le maintien en production : choix
d'hébergement, administration des services, déploiement automatisé (DevOps) et supervision. Compétences
C27 à C32, livrables E21 à E29. <strong>Également évalué via une mise en situation de maintenance</strong>
(bugs, failles, composants obsolètes).
</p>

> Infra TaskForce : Docker Compose (dev/prod/tools) · nginx (reverse proxy + TLS) · Keycloak 25 ·
> MinIO · RabbitMQ 4 · PostgreSQL 18 · SigNoz/OTel (observabilité) · GitHub Actions → GHCR.
> Détail : [Architecture §5](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Documentation & solutions de production](#activité--documentation--solutions-de-production) (C27, C28, C29)
2. [Activité — Administration & déploiement](#activité--administration--déploiement) (C30, C31)
3. [Activité — Supervision & maintenance](#activité--supervision--maintenance) (C32)

---

## Activité — Documentation & solutions de production

### C27 — Produire la documentation technique + base de connaissances
**Livrable :** E29 — génération de documentation + mise à jour du changelog.  
**Critères d'évaluation :**
- [x] Génération automatique de documentation à partir du code source.
- [x] Documentation de l'API rédigée pour faciliter sa consommation par des tiers.
- [x] Mises à jour portées dans le journal des évolutions (changelog).
- [x] Liste des modifications structurée (ordre décroissant, regroupement par version).

**Preuves :** `OpenApiConfig.java` · `/swagger-ui.html` · [Contrats API](../05-api/API.md) · [Release Notes](../15-utilisateur/Release_Notes.md) · `.github/workflows/version-management.yml` · `.github/workflows/sync-readme-badges.yml` · Ce Brain OS

**Documentation technique et base de connaissances**

**Génération automatique depuis le code** : la documentation API est générée automatiquement par **Springdoc OpenAPI 2.x** à partir des annotations Java dans les contrôleurs (`@Operation`, `@ApiResponse`, `@Parameter`, `@Schema`). Cette approche « code-as-docs » garantit que la documentation est toujours synchronisée avec l'implémentation — une annotation `@Operation(summary=...)` sur un contrôleur est la source de vérité, pas un fichier Markdown séparé qui peut dériver. La documentation est publiée sur `/swagger-ui.html` (Swagger UI interactif) et exportable en JSON OpenAPI 3.1 sur `/v3/api-docs`.

**Documentation API pour les tiers** : le [contrat API](../05-api/API.md) documente l'ensemble des endpoints REST de TaskForce : méthode HTTP, chemin, corps de requête (DTO typé), codes de réponse (200/201/400/401/403/404/409/429/500) et exemples JSON. Cette documentation est structurée par domaine métier (auth, workspace, project, issue, smart-assign, stripe, gdpr) pour faciliter la prise en main par un développeur tiers.

**Changelog et versioning automatisé** : le workflow `version-management.yml` analyse les labels des PRs fusionnées (`feat` → bump MINOR, `fix` → bump PATCH, `breaking` → bump MAJOR) et crée automatiquement un tag Git `backend-vX.Y.Z` / `frontend-vX.Y.Z` / `landing-vX.Y.Z` avec des releases GitHub contenant les notes de changements. Le workflow `sync-readme-badges.yml` met à jour les badges de version dans les README à chaque release. Les [Release Notes](../15-utilisateur/Release_Notes.md) documentent la V1.0.0 avec les 15 catégories de fonctionnalités livrées.

**Base de connaissances — ce Brain OS** : l'ensemble du dossier `taskforce-docs/` constitue la base de connaissances technique du projet. Il est organisé par domaine (architecture, API, sécurité, infra, qualité, utilisateur, veille) et suit les conventions Obsidian (wikilinks `[[nom]]`, frontmatter YAML). Cette documentation est maintenue en parallèle du code — toute décision technique structurante donne lieu à un ADR dans [Journal des décisions](../08-decisions/Journal_Decisions_ADR.md).

---

### C28 — Administration (domaine, DNS, certificats, sécurité)
**Livrable :** E23 — réservation nom de domaine, configuration DNS, installation/vérification des certificats.  
**Critères d'évaluation :**
- [ ] Nom de domaine et déclarations administratives effectuées.
- [ ] Serveurs de noms configurés et fonctionnels (bonnes pratiques de sécurité).
- [ ] Certificats de sécurité installés, configurés pour les différents services.

**Preuves :** `nginx/nginx.conf.example` (configuration validée, non déployée) · `docker-compose.prod.yml` · [Stratégie d'hébergement](../06-infra/Strategie_Hebergement.md)

> **Compétence non acquise à ce jour, et c'est assumé.** Cette section était rédigée au présent de
> l'indicatif, comme si l'infrastructure était en service : certificats Let's Encrypt émis, crontab de
> renouvellement, zone DNS avec SPF/DKIM/DMARC, callbacks OAuth enregistrés en production. **Rien de
> cela n'existe.** Aucun domaine n'a été réservé, aucun serveur ne sert l'application, et les fichiers
> cités en preuve (`nginx/nginx.conf`, `nginx/ssl/`) n'existent pas dans le dépôt. Corrigé le 23/07/2026.
>
> Le déploiement reste suspendu au choix d'hébergement (voir C29). Ce qui suit décrit donc ce qui est
> **préparé et vérifiable dans le dépôt**, non ce qui est en service.

**Ce qui est préparé : la terminaison TLS et le routage**

Le fichier `nginx/nginx.conf.example` configure nginx en point d'entrée unique. Il termine le TLS,
redirige HTTP vers HTTPS (301 permanent) et relaie vers les services Docker internes. Les bonnes
pratiques y sont appliquées et vérifiables par lecture : TLS 1.2 et 1.3 seulement, suites ECDHE avec
confidentialité persistante, HSTS (`max-age=31536000; includeSubDomains`), agrafage OCSP, limitation
de débit (20 requêtes par seconde sur l'API, 5 sur Keycloak), fermeture de la console
d'administration Keycloak et des points d'actuator hors sonde de santé, et `return 444` sur l'hôte
par défaut. La configuration a été validée par un binaire nginx réel, pas seulement relue.

Un point de conception mérite d'être signalé, car il conditionne le démarrage : nginx résout les
noms d'hôte amont **au démarrage**, si bien qu'un seul service indisponible empêche le proxy de
démarrer. La configuration contourne ce comportement par le résolveur Docker interne
(`resolver 127.0.0.11`) et des noms passés en variables dans `proxy_pass`.

**Ce qui reste à faire au déploiement**

Réserver le domaine et déclarer la zone DNS (enregistrements A, et MX pour les courriels OTP émis par
Keycloak, avec SPF, DKIM et DMARC pour éviter le classement en indésirable). Émettre les certificats
par Let's Encrypt et automatiser leur renouvellement. Enregistrer les URL de rappel OAuth GitHub et
Slack de production dans les consoles développeur correspondantes, les variables
`GITHUB_OAUTH_REDIRECT_URI` et `SLACK_OAUTH_REDIRECT_URI` étant déjà prévues à cet effet.

Les trois sous-domaines visés sont `app`, `api` et `auth`, déjà routés dans la configuration.

---

### C29 — Sélectionner une plateforme d'hébergement
**Livrable :** E21 — choix d'une solution cloud argumentée + diagramme de déploiement.  
**Critères d'évaluation :**
- [x] Architecture technique d'hébergement adaptée à l'application.
- [x] Principe d'élasticité pris en compte.
- [x] Dimensionnement et coûts cohérents avec les besoins.
- [ ] Diagramme de déploiement formalisé ; choix du système de déploiement adapté.

**Preuves :** `docker-compose.prod.yml` · `render.yaml` · [Stratégie d'hébergement](../06-infra/Strategie_Hebergement.md)

> **Dernier critère décoché le 23/07/2026 : le diagramme de déploiement n'existe pas.** Il est
> recherché dans tout le corpus et n'y figure nulle part ; la seule mention est son inscription au
> reste à faire dans la [roadmap documentaire](./Roadmap_Documentation.md) (Phase 7). Les trois
> premiers critères restent acquis, la comparaison d'hébergement étant documentée et chiffrée.

**Sélection de la plateforme d'hébergement**

Deux options d'hébergement ont été conçues et documentées, avec des compromis différents selon le contexte.

**Option A — VM Metz Numeric School (VPS auto-administré)**

Un serveur virtuel (4 vCPU / 8 Go RAM / 80 Go SSD) héberge l'ensemble de la stack via `docker-compose.prod.yml`. Cette option convient à la démonstration en soutenance (infrastructure contrôlée, pas de latence réseau externe, coût nul pour l'établissement). La VM est administrée directement via SSH avec un accès bastion.

Composants : nginx (443/80), backend Spring Boot (8080, interne), frontend Next.js (3000, interne), PostgreSQL 18 (5432, interne), Keycloak 25 (8081, interne), RabbitMQ 4 (5672/15672, interne), MinIO (9000/9001, interne). Tous les services sont sur un réseau Docker bridge isolé — seul nginx est exposé sur les ports 80/443 de l'hôte.

**Option B — Render.com Frankfurt (PaaS managé)**

`render.yaml` définit le déploiement sur Render.com (région Frankfurt, EU) pour une infrastructure sans administration de serveur. Services configurés : Web Service backend (Docker, 512 Mo RAM), Web Service frontend (Docker), PostgreSQL managé (sauvegardes automatiques, HA), Redis pour le rate limiting distribué (si activé). Estimation : ~46 $/mois pour un déploiement de démonstration.

**Principe d'élasticité** : Render.com supporte l'auto-scaling horizontal des Web Services basé sur la charge CPU/RAM. Pour la V1 (mono-instance), cette élasticité est documentée comme amélioration post-V1. L'architecture stateless du backend Spring Boot (pas d'état en mémoire, tokens JWT auto-suffisants, sessions dans Redis) permet le scale-out sans modification de code — c'est la valeur de la conception stateless dès le départ.

**Diagramme de déploiement** : le diagramme C4 niveau 3 (déploiement) est disponible dans [Architecture §5](../03-architecture/Architecture.md). Il représente les conteneurs Docker, les réseaux internes, les volumes de persistance, et les flux de données entre services (API calls, AMQP, JDBC, S3-compatible).

---

## Activité — Administration & déploiement

### C30 — Administrer des services d'hébergement (cloud / conteneurisé)
**Livrable :** E22 — mise en œuvre sécurisée de l'environnement de production + administration.  
**Critères d'évaluation :**
- [x] Services d'hébergement configurés et fonctionnels (gestionnaire de conteneurs).
- [x] Environnement conteneurisé fonctionnel.
- [x] Bonnes pratiques de sécurité (architecture, configuration, **hôte bastion**).

**Preuves :** `docker-compose.prod.yml` · `nginx/nginx.conf` · [Architecture §5](../03-architecture/Architecture.md) · [Quickstart prod](../06-infra/quickstart/README.md)

**Administration de l'environnement de production**

**Environnement conteneurisé** : `docker-compose.prod.yml` orchestre 8 services en production. Les différences majeures avec l'environnement de développement sont : images taguées par version (pas de `latest`), aucun port d'infrastructure exposé sur l'hôte (PostgreSQL, Keycloak, RabbitMQ, MinIO sont sur le réseau Docker interne uniquement), variables d'environnement sensibles chargées depuis un fichier `.env.prod` non versionné, et volumes de persistance nommés (`postgres_data`, `minio_data`, `keycloak_data`).

**Isolation réseau** : deux réseaux Docker sont définis. `taskforce_frontend` connecte nginx et le frontend Next.js. `taskforce_backend` connecte le backend Spring Boot avec PostgreSQL, Keycloak, RabbitMQ et MinIO. nginx est le seul service présent sur les deux réseaux — cette topologie garantit que le frontend ne peut pas accéder directement à la base de données.

**Durcissement de la configuration** : les images de production utilisent des utilisateurs non-root (directive `USER 1000` dans les Dockerfiles), des capacités Linux minimales (`--security-opt no-new-privileges`), et des systèmes de fichiers en lecture seule là où possible. PostgreSQL est configuré avec `pg_hba.conf` restreint (authentification scram-sha-256, accès limité à l'IP du backend Docker). Keycloak est configuré en mode production (HTTPS obligatoire, admin console accessible uniquement depuis le réseau interne).

**Accès bastion** : l'accès à l'infrastructure de production se fait exclusivement via SSH avec clé RSA/ED25519 (authentification par mot de passe désactivée). Le port SSH est non-standard (déplacé du port 22 pour réduire le bruit des scans automatisés). L'accès bastion vers les services d'infrastructure (PostgreSQL Admin, Keycloak Admin, MinIO Console) est réalisé par tunnel SSH (`ssh -L 5432:localhost:5432 bastion`).

---

### C31 — Mettre en œuvre un déploiement automatisé (DevOps)
**Livrable :** E24 — système de déploiement automatisé.  
**Critères d'évaluation :**
- [x] Bonnes pratiques DevOps respectées (livraison en continu).
- [x] Système de déploiement fonctionnel sur l'environnement de qualification, repris en production.
- [x] Opérationnel et conforme aux recommandations DevOps.

**Preuves :** `.github/workflows/` (7 workflows) · [GitHub Actions](../04-engineering/git-workflow/github-actions.md) · [GHCR Usage](../06-infra/docker/GHCR_USAGE.md)

**Pipeline DevOps — CI/CD**

Le cycle de livraison TaskForce est automatisé par **7 workflows GitHub Actions** couvrant l'intégralité de la chaîne CI/CD.

**Intégration Continue (CI)** — exécutée sur chaque PR :

| Workflow | Déclencheur | Étapes |
|---|---|---|
| `backend-tests.yml` | PR sur `main` (changements `backend/**`) | `mvnw clean test jacoco:report`, publication de la couverture (Codecov) et archivage des rapports. **Ni Checkstyle, ni SpotBugs, ni porte JaCoCo bloquante** : corrigé le 23/07, le workflow ne les a jamais exécutés |
| `frontend-tests.yml` | PR sur `main` (changements `frontend/**`) | ESLint → tsc → Vitest coverage gate → Next.js build |
| `landing-tests.yml` | PR sur `main` (changements `landing-page/**`) | ESLint → Astro build |
| `e2e-tests.yml` | PR sur `main` | Docker Compose up → Playwright 3 specs → teardown |

**Livraison Continue (CD)** — exécutée sur merge vers `main` :

| Workflow | Déclencheur | Étapes |
|---|---|---|
| `version-management.yml` | PR mergée avec labels | Lecture labels PR → bump SemVer → tag Git → GitHub Release |
| `release.yml` | Tag `backend-v*` / `frontend-v*` / `landing-v*` | Build image Docker multi-stage → Push GHCR → GitHub Release assets |
| `sync-readme-badges.yml` | Release créée | Mise à jour badges version dans README |

**Stratégie de déploiement** : après publication des images sur GHCR, le déploiement vers le serveur de production est déclenché par `docker compose pull && docker compose up -d` sur le serveur cible. Les images sont versionnées par tag (`ghcr.io/org/taskforce-api:v1.2.3`) — jamais `latest` en production. Le déploiement est progressif : les services backend et frontend sont redémarrés séquentiellement (le backend d'abord pour que les migrations Flyway s'exécutent avant que le frontend ne soit accessible).

**Bonnes pratiques DevOps** : séparation des pipelines CI et CD, artifacts versionnés (images GHCR), rollback possible en re-déployant le tag précédent, secrets GitHub Actions pour les credentials (GHCR, RENDER_API_KEY), cache des dépendances Maven et npm entre les CI runs (économie de ~2 minutes par build).

---

## Activité — Supervision & maintenance

### C32 — Superviser (sondes, alertes, journalisation, détection)
**Livrable :** E25 journalisation/audit · E26 supervision + alertes · E27 détection bugs + correctifs · E28 détection failles + correctifs.  
**Critères d'évaluation :**
- [x] Journalisation des services implémentée ; outils d'audit fonctionnels.
- [x] Outils de sauvegarde fonctionnels ; stratégie de tolérance de panne adaptée.
- [x] Outils de supervision fonctionnels ; sondes et alertes efficaces.
- [x] Bugs identifiés, mesures correctives efficaces.
- [x] Failles de sécurité identifiées, mesures correctives efficaces.

**Preuves :** `observability/otel-collector-config.yaml` · `observability/alerts/prometheus-rules.yml` · `AuditService.java` · `ClientLogController.java` · [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) · `scripts/backup.ps1` · `scripts/security-scan.ps1` · [Problèmes connus](../09-audits/Problemes_Connus.md) · [Dette Technique](../09-audits/Dette_Technique.md)

**Journalisation et audit (E25)**

La journalisation de TaskForce opère à deux niveaux complémentaires.

**Audit métier** : `AuditService.java` persiste les événements de sécurité et de conformité dans la table `audit_logs`. 7 types d'événements sont journalisés : `AUTH_LOGIN`, `AUTH_LOGOUT`, `AUTH_OTP_FAILED`, `ROLE_CHANGE`, `MEMBER_INVITE`, `GDPR_EXPORT`, `GDPR_DELETE`. Chaque entrée contient l'utilisateur acteur, le timestamp, l'IP source, l'identifiant de la ressource cible, et le résultat (SUCCESS/FAILURE). Ces logs sont la preuve d'audit RGPD requise par l'article 5(2) du RGPD.

**Logs applicatifs** : les logs backend (SLF4J / Logback) et frontend (`ClientLogController` + `client-logger.ts`) sont collectés par le receiver `filelog` de l'OTel Collector depuis les fichiers Docker JSON (`/var/lib/docker/containers/**/*-json.log`). Le composant `ClientLogController.java` reçoit les logs structurés du frontend (erreurs JavaScript, navigation, actions utilisateur) et les sanitise (protection contre le log-forging) avant injection dans le pipeline OTel.

**Pipeline d'observabilité OTel → SigNoz** : l'OTel Collector (`observability/otel-collector-config.yaml`) orchestre 5 pipelines :

| Pipeline | Receivers | Exporters |
|---|---|---|
| Traces | OTLP (backend Spring + frontend) | SigNoz ClickHouse |
| Métriques | Prometheus scrape (actuator/prometheus) | SigNoz ClickHouse |
| Métriques Prometheus | Prometheus remote_write | SigNoz ClickHouse |
| Logs | filelog (Docker containers) | SigNoz ClickHouse |
| Meter | OTLP meter | SigNoz ClickHouse |

Spring Boot Actuator expose `/actuator/health` (sonde de santé), `/actuator/metrics` et `/actuator/prometheus` (métriques Micrometer format Prometheus). Ces endpoints sont accessibles uniquement sur le port de management interne (8081) — non exposés sur le port API public (8080).

**Supervision et alertes (E26)**

Le fichier `observability/alerts/prometheus-rules.yml` définit **9 règles d'alerte Prometheus** en deux groupes :

*Groupe Infrastructure* : `HighErrorRate` (taux d'erreurs HTTP > 5 % sur 5 min), `HighLatencyP95` (p95 > 1s sur 5 min), `JVMHeapHighUsage` (heap > 85 %), `DBConnectionPoolExhausted` (< 5 connexions disponibles), `ServiceDown` (instance non joignable 1 min), `HighCPUUsage` (CPU > 80 %).

*Groupe Sécurité* : `RateLimitSpike` (montée des 429 Too Many Requests — indicateur de scan automatisé ou brute-force), `AuthFailureSpike` (montée des 401 sur `/api/auth/**` — indicateur de tentatives de connexion forcée). Ces deux alertes de sécurité sont une originalité de l'architecture TaskForce : l'observabilité surveille activement les menaces, pas seulement l'infrastructure.

**Sauvegarde et tolérance de panne (E25/PCA)**

Le [Plan de Sauvegarde et de Continuité (PS/PCA/PRA)](../11-pca-pra/PS_PCA_PRA.md) définit la stratégie de tolérance de panne. Le script `scripts/backup.ps1` automatise : `pg_dump` de PostgreSQL (dump compressé `.pgdump` avec timestamp), sauvegarde des buckets MinIO (fichiers attachés aux issues), export du realm Keycloak (configuration SSO). La procédure de restauration est documentée et a été testée — le RTO (Recovery Time Objective) cible est de 30 minutes.

**Détection de bugs et correctifs (E27)**

La démarche de détection de bugs est documentée dans [Problèmes connus](../09-audits/Problemes_Connus.md) et [Dette Technique](../09-audits/Dette_Technique.md). Ces fichiers recensent les problèmes identifiés avec leur impact, leur cause, et leur statut de correction. Exemples de bugs détectés et corrigés : incohérence de routes API entre le contrat OpenAPI et l'implémentation (PC-001/PC-002 — corrigés par alignement des annotations `@RequestMapping`) ; registre Micrometer manquant sur le profil d'observabilité (causait l'absence de métriques Prometheus — corrigé par injection explicite du `MeterRegistry`).

La mise en situation de maintenance (E27) sera démontrée en soutenance : introduction d'une régression intentionnelle, identification via les logs SigNoz / les tests CI, isolation de la cause par les alertes Prometheus, correction et validation par re-run de la suite de tests.

**Détection de failles de sécurité et correctifs (E28)**

Le script `scripts/security-scan.ps1` implémente quatre niveaux de détection :

1. **Trivy** (`-Trivy`) : scan CVE des images Docker (OS Alpine + JARs Maven + packages npm) — résultat V1.0 : 0 HIGH, 0 CRITICAL sur les images finales.
2. **Semgrep** (`-Sast`) : analyse statique Java et TypeScript pour détecter les patterns vulnérables (injection SQL, path traversal, secrets en dur, eval() unsafe). Résultat : 0 findings HIGH.
3. **OWASP Dependency-Check** (`-DependencyCheck`) : vérification des dépendances Maven et npm contre la base NVD (CVE). Exécuté mensuellement.
4. **OWASP ZAP** (`-Dast`) : scan DAST de l'API déployée. Résultat V1.0 : 0 HIGH, 4 MEDIUM (CSP insuffisante en environnement dev — corrigée par `SecurityConfig` en production avec `Content-Security-Policy: default-src 'none'`).

La faille de sécurité PC-019 (JWT HS512 symétrique — TF-SEC-009) a été identifiée par la veille ANSSI (VT-005), documentée sans être occultée, **puis corrigée** (05/07/2026, [ADR-011](../12-decisions/Journal_Decisions_ADR.md)) : migration vers l'émission de tokens **Keycloak OIDC RS256**, suppression du `JwtService` custom — cycle complet détection → décision → remédiation → vérification (658 tests verts).

---

> 🔗 [[Architecture_C4]] — [[PS_PCA_PRA]] — [[PSSI]] — [[Pipeline_CICD]] — [[Release_Notes]] —
> [[Problemes_Connus]] — [[Dette_Technique]] — [[Roadmap_Backlog]]

**Dernière mise à jour :** 05/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
