---
type: memoire-rncp
bloc: 3
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc3, backend, api, securite]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 3 — Développer la partie back-end

**Version :** 1.0  
**Date :** 05/07/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 3](https://img.shields.io/badge/Bloc-3%20Back--end-blue?style=for-the-badge)]() [![Statut: Validé](https://img.shields.io/badge/Statut-Valid%C3%A9-green?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture §4 (backend)](../03-architecture/Architecture.md) · [Contrats API](../05-api/API.md) · [Modules](../03-architecture/Modules.md)

**Tags :** `#memoire` `#bloc3` `#backend` `#api` `#securite`

<p class="lead">
Ce bloc couvre le développement back-end : couche de persistance, code serveur, paiement/monétisation,
API sécurisée, tests et industrialisation. Compétences C21 à C26, livrables E15 à E20.
<strong>Évalué aussi en soutenance (démo back-end).</strong>
</p>

> Stack TaskForce back : Spring Boot 4.0 (Java 21) · Maven · PostgreSQL 18 + pgvector ·
> Keycloak 25 (IdP) · Stripe · MinIO · RabbitMQ 4 / STOMP · Groq API · OpenTelemetry.
> Détail : [Architecture §4](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Développement back-end](#activité--développement-back-end) (C21–C24)
2. [Activité — Tests back-end](#activité--tests-back-end) (C25, C26)

---

## Activité — Développement back-end

### C21 — Développer la couche de persistance
**Livrable :** E15.  
**Critères d'évaluation :**
- [x] « Sécurité en profondeur » : filtrage des données entrantes/sortantes, authentification forte, journalisation, monitoring, validation des configurations, contrôle d'accès.
- [x] Bases de données et systèmes de cache performants et sécurisés.

**Preuves :** [Architecture §6](../03-architecture/Architecture.md) · `AuditableEntity.java` · `WorkspaceAccessInterceptor.java` · `AuthorizationService.java` · `EncryptedStringConverter.java` · Flyway V1–V53

**Couche de persistance — sécurité en profondeur**

La couche de persistance de TaskForce applique le principe de **sécurité en profondeur** à quatre niveaux distincts.

**Niveau 1 — Contrôle d'accès** : `WorkspaceAccessInterceptor` intercepte chaque requête vers `/api/workspaces/{slug}/**` et vérifie que l'utilisateur authentifié est membre actif du workspace ciblé (`workspace_members.is_active = true`). En cas d'échec, la réponse est 403 Forbidden. `AuthorizationService.getMemberOrThrow()` est appelé dans chaque service métier pour obtenir le `WorkspaceMember` avant toute opération — cette mécanique d'isolation empêche les attaques IDOR (Insecure Direct Object Reference, OWASP A01).

**Niveau 2 — Journalisation** : toutes les entités modifiables héritent de `AuditableEntity` (champs `created_at`, `updated_at`, `created_by`, `updated_by` peuplés automatiquement par Spring Data JPA Auditing). Les opérations sensibles (authentification, export RGPD, suppression de compte, changements de rôle) sont journalisées dans la table `audit_logs` via `AuditService.log()`.

**Niveau 3 — Chiffrement des PII** : le converter JPA `EncryptedStringConverter` applique AES-256-GCM sur les colonnes marquées `@Convert(converter = EncryptedStringConverter.class)` — utilisé sur les messages de contact Enterprise et les notes sensibles. La clé de chiffrement est injectée depuis la variable d'environnement `ENCRYPTION_KEY` (jamais en dur dans le code).

**Niveau 4 — Filtrage entrées/sorties** : Bean Validation (`@NotNull`, `@Size`, `@Email`, `@Pattern`) sur tous les DTOs de requête — la validation est activée automatiquement par `@Valid` dans les contrôleurs Spring. Les réponses ne contiennent jamais de données inter-workspace : chaque requête de liste filtre par `workspace_id` dans la clause WHERE.

**Performance** : PostgreSQL 18 est configuré avec des index sur les colonnes fréquemment filtrées (`workspace_id`, `project_id`, `assignee_id`, `status`, `created_at`). Les requêtes N+1 sont évitées par des `JOIN FETCH` ou des `@EntityGraph` JPA dans les repositories critiques. Le pool de connexions HikariCP est paramétré dans `application.yml` (10 connexions par défaut, configurable via `HIKARI_MAX_POOL_SIZE`).

---

### C22 — Langage back-end (qualité, sécurité, écoconception)
**Livrable :** E16 — développer intégralement le back-end + intégrer le front.  
**Critères d'évaluation :**
- [x] Couvre l'ensemble des cas d'utilisation du dossier de conception.
- [x] Code valide et conforme aux référentiels du/des langage(s).
- [x] Organisation du code conforme aux usages et bonnes pratiques.
- [x] Bonnes pratiques d'écoconception intégrées.
- [x] Composants tiers à jour, sans vulnérabilité connue ; prise en compte des performances.
- [x] Compatible avec les plateformes/versions actuelles.

**Preuves :** [Architecture §4](../03-architecture/Architecture.md) · [Modules](../03-architecture/Modules.md) · `backend/tf-api/pom.xml` · `scripts/security-scan.ps1`

**Code backend — qualité, organisation, sécurité**

**Couverture des cas d'utilisation** : les 12 UC du CdCF sont couverts par les contrôleurs Spring Boot. L'intégration frontend↔backend est assurée par l'API REST documentée dans [Contrats API](../05-api/API.md) et publiée via OpenAPI (`/swagger-ui.html`). Le frontend consomme cette API via le client Axios centralisé — l'intégration est validée par les tests E2E Playwright qui couvrent les parcours end-to-end.

**Organisation du code** : l'architecture en couches `shared/core/modules` respecte les conventions Spring Boot et Domain-Driven Design. Chaque module métier (`project`, `issue`, `smart-assign`, `cycle`, `page`, `chat`, `notification`) est indépendant : controller → service → repository → model. Les seules dépendances inter-couches sont unidirectionnelles (modules → core → shared). Les noms de packages, classes et méthodes suivent les conventions Java (PascalCase classes, camelCase méthodes) et les conventions Spring (contrôleurs suffixés `Controller`, services `Service`, repositories `Repository`).

**Qualité du code** : le projet utilise Checkstyle (règles Google Java Style Guide) et SpotBugs en CI pour la détection de bugs potentiels. La complexité cyclomatique est maintenue basse par le pattern Command/Strategy (le calcul des scores Smart Assign utilise une interface `ScoringSignal` implémentée par 5 classes — une par signal — ce qui rend chaque signal testable isolément).

**Écoconception** : les Virtual Threads Java 21 (Project Loom, activés dans `application.yml` via `spring.threads.virtual.enabled: true`) permettent de gérer des milliers de requêtes concurrentes avec une consommation de threads OS minimale — un pool de threads classique (100 threads) serait bloquant sur les I/O (appels PostgreSQL, Groq API) ; avec les Virtual Threads, chaque requête suspend son thread OS pendant les I/O et le libère pour d'autres requêtes. Le résultat est une meilleure utilisation des ressources CPU sans augmenter la mémoire.

**Dépendances à jour** : le fichier `pom.xml` hérite des versions gérées par `spring-boot-starter-parent` 4.0, ce qui garantit la cohérence des versions des librairies Spring. Trivy (`scripts/security-scan.ps1 -Trivy`) scanne l'image Docker finale pour détecter les CVE. Semgrep (`-Sast`) analyse le code source. Aucune CVE HIGH ou CRITICAL connue au moment de la livraison.

---

### C23 — Implémenter un système de paiement + monétisation
**Livrable :** E17.  
**Critères d'évaluation :**
- [x] Intégration du système de paiement fonctionnelle.
- [x] Respect des recommandations de sécurité (paiement).
- [x] Système de monétisation adapté au contexte et pertinent vs cible marketing.

**Preuves :** `StripeController.java` · `StripeWebhookController.java` · `StripeService.java` · [Stratégie Vente](../01-projet/Strategie_Vente_LLM.md) · [Problèmes connus PC-005](../09-audits/Problemes_Connus.md)

**Système de paiement Stripe**

**Flux de paiement** : le modèle de paiement suit le pattern recommandé par Stripe pour les abonnements SaaS. L'utilisateur clique « Upgrade » dans l'interface → `POST /api/stripe/checkout/session` → `StripeService.createCheckoutSession()` crée une Stripe Checkout Session avec les métadonnées workspace et le plan ciblé → l'API retourne l'URL de la session Stripe → le frontend redirige vers cette URL (domaine Stripe, iframe certifiée PCI-DSS). Le paiement est traité par Stripe, qui notifie le backend via webhook.

**Sécurité des webhooks** : `StripeWebhookController` vérifie la signature HMAC de chaque événement reçu via `Stripe.constructEvent(payload, sigHeader, webhookSecret)` — sans cette vérification, n'importe qui pourrait simuler un paiement réussi. L'idempotence est garantie par la contrainte `UNIQUE(stripe_event_id)` en base de données : un même événement Stripe ne peut pas être traité deux fois (protection contre les livraisons dupliquées).

**Événements traités** : `checkout.session.completed` (activation du plan), `invoice.payment_succeeded` (renouvellement), `invoice.payment_failed` (passage en `PAST_DUE`), `customer.subscription.updated` (changement de plan), `customer.subscription.deleted` (annulation → `CANCELED`). La machine à états `PlanStatus` gère les transitions : `ACTIVE → PAST_DUE → CANCELED`.

**Portail de facturation** : `POST /api/stripe/portal` crée une Stripe Billing Portal Session pour permettre à l'utilisateur de modifier son moyen de paiement, annuler son abonnement, et télécharger ses factures — sans que TaskForce stocke un seul numéro de carte.

**Monétisation** : le modèle freemium FREE/PRO/ENTERPRISE est documenté dans [Stratégie Vente](../01-projet/Strategie_Vente_LLM.md). FREE (membres illimités, 5 projets max, Smart Assign limité), PRO (~12$/mois/workspace — projets illimités, Smart Assign complet, analytics), ENTERPRISE (tarif sur devis — SLA, support dédié, modules custom). Ce positionnement est cohérent avec le marché cible (startups et PME tech).

**Limitation connue** : certains webhooks de cycle de vie Stripe sont actuellement stubés en environnement de test (`PC-005` dans [Problèmes connus](../09-audits/Problemes_Connus.md)) — le flux principal d'abonnement est fonctionnel, mais les cas de renouvellement automatique ne sont pas testés end-to-end en production.

---

### C24 — Développer une API sécurisée
**Livrable :** E18.  
**Critères d'évaluation :**
- [x] Authentification et autorisation solides.
- [x] Toutes les entrées utilisateur validées et filtrées.
- [x] Toutes les données sensibles chiffrées.
- [x] API documentée et publiée.

**Preuves :** `SecurityConfig.java` · `KeycloakAuthService.java` · `RateLimitFilter.java` · `OpenApiConfig.java` · [Contrats API](../05-api/API.md) · [PSSI](../07-securite/PSSI.md) · [ADR-011](../12-decisions/Journal_Decisions_ADR.md)

**API sécurisée**

**Authentification** : Keycloak est l'Identity Provider (IdP) — comptes, sessions, OTP email — **et l'émetteur des tokens** (OIDC RS256). Lors de la connexion, `AuthService` délègue à `KeycloakAuthService` (grant ROPC) qui obtient de Keycloak un access token + refresh token signés en RS256 ; l'API n'émet plus aucun token elle-même. Côté validation, `SecurityConfig` agit en **Resource Server** : `NimbusJwtDecoder` vérifie la signature via le JWK Set Keycloak et valide l'`issuer`. L'utilisateur courant est résolu par le claim `email` du token. Le refresh est natif OIDC (rotation gérée par l'IdP) et la déconnexion invalide les sessions côté Keycloak (`users().logout()`). Cette migration (juillet 2026, [ADR-011](../12-decisions/Journal_Decisions_ADR.md)) a supprimé la dette du JWT HS512 symétrique auto-émis (PC-019 / TF-SEC-009).

**Rate limiting** : `RateLimitFilter` utilise Bucket4j (algorithme Token Bucket) pour limiter les requêtes par IP : 10 req/min sur `/api/auth/**` (protection brute-force), 20 req/min sur `/api/smart-assign/**` (protection contre les abus IA), 200 req/min par défaut. Un dépassement retourne 429 Too Many Requests avec l'en-tête `Retry-After`.

**Validation des entrées** : Bean Validation sur 100 % des DTOs de requête — `@NotNull`, `@Size(max=255)`, `@Email`, `@Pattern`, `@Positive` selon le champ. La validation est déclenchée par `@Valid` dans les contrôleurs ; une violation retourne 400 Bad Request avec le détail des contraintes violées (`MethodArgumentNotValidException` → `ApiExceptionHandler`). Le log-forging (injection de caractères de contrôle dans les logs) est prévenu par `ClientLogController.sanitize()`.

**Chiffrement des données sensibles** : les données au repos sont protégées par `EncryptedStringConverter` (AES-256-GCM) sur les colonnes PII sensibles. Les données en transit sont protégées par TLS (nginx reverse proxy en production). Les secrets (JWT_SECRET, clés Stripe, clé Keycloak) sont injectés par variables d'environnement — jamais en dur dans le code ni dans les commits (`.gitignore` couvre les fichiers `.env`).

**Documentation API** : `OpenApiConfig.java` configure Springdoc OpenAPI 2.x pour générer la documentation à partir des annotations `@Operation`, `@ApiResponse`, `@Schema` sur les contrôleurs. La documentation est publiée sur `/swagger-ui.html` (désactivée en production par `springdoc.swagger-ui.enabled: false` dans `application-prod.yml`). Le contrat OpenAPI JSON est exporté dans [Contrats API](../05-api/API.md).

---

## Activité — Tests back-end

### C25 — Tester le back-end
**Livrable :** E19 — plan de tests complet et cohérent.  
**Critères d'évaluation :**
- [x] Plan de test cohérent avec les exigences des spécifications.
- [x] **Couverture du code source ≥ 50 %.** *(78 % — JaCoCo, gate 60 %)*

**Preuves :** `backend/tf-api/src/test/` · [Plan Tests Backend](../10-qualite/Plan_Tests_Backend.md) · rapport JaCoCo (CI artefact) · `backend/tf-api/pom.xml` (plugin JaCoCo)

**Plan de tests et couverture backend**

La stratégie de tests backend suit une pyramide à trois niveaux, avec un principe fondamental : **aucun mock de base de données** (mémorisé dans les règles d'or du projet). Les tests d'intégration utilisent **Testcontainers** pour démarrer de vraies instances Docker (PostgreSQL + pgvector, Keycloak) lors de l'exécution des tests — ce qui garantit que les migrations Flyway, les contraintes SQL, les index, et les comportements pgvector sont testés dans des conditions identiques à la production.

**Niveau 1 — Tests unitaires** : services et logiques métier isolés avec Mockito. Les tests paramétrés (`@ParameterizedTest` + `@MethodSource` / `@CsvSource`) couvrent les cas limites : le calcul des scores Smart Assign est testé pour les 5 signaux avec des valeurs aux bornes (score min/max, poids nuls, vecteurs orthogonaux pour cosine similarity = 0), la validation OTP est testée pour les 3 tentatives avec expiration de TTL.

**Niveau 2 — Tests d'intégration Web (`@WebMvcTest`)** : chaque contrôleur est testé en isolation du service (MockMvc + Mockito) pour vérifier les codes HTTP, la validation Bean Validation, les réponses d'erreur (`400`, `403`, `404`, `429`), et la sérialisation JSON.

**Niveau 3 — Tests d'intégration complets (`@SpringBootTest`)** : les parcours métier critiques sont testés de bout en bout avec base de données réelle (Testcontainers PostgreSQL + Keycloak). Ces tests couvrent les scénarios multi-étapes : inscription → OTP → connexion → création workspace → invitation membre → création projet → Smart Assign. Ce niveau de test garantit que l'application fonctionne en conditions réelles, y compris les cascades SQL, les transactions, et les appels réseau inter-services.

**Couverture** : 72 fichiers de test, 670 tests, **78 % de couverture de lignes JaCoCo** (gate CI fixé à 60 %). Le rapport est généré à chaque CI run et archivé comme artefact. Les classes non couvertes sont principalement la couche de configuration Spring (non testable en unitaire) et les stubs de webhooks Stripe (PC-005).

---

### C26 — Industrialiser le back-end
**Livrable :** E20.  
**Critères d'évaluation :**
- [x] Outils de qualité cohérents avec les spécifications.
- [x] Gestion des dépendances mise en œuvre.
- [x] Chaîne de build améliorant performances **et sécurité** du back.

**Preuves :** `.github/workflows/backend-tests.yml` · `.github/workflows/release.yml` · `.github/workflows/version-management.yml` · `scripts/security-scan.ps1` · [GHCR Usage](../06-infra/docker/GHCR_USAGE.md)

**Pipeline CI/CD back-end**

Le workflow `backend-tests.yml` automatise la chaîne de qualité sur chaque PR :

```
1. mvn dependency:resolve (vérification des dépendances)
2. mvn checkstyle:check (Google Java Style Guide)
3. mvn spotbugs:check (détection de bugs statique)
4. mvn test (JUnit 5 + Testcontainers — démarre PostgreSQL + Keycloak Docker)
5. mvn jacoco:report (génération rapport de couverture)
6. Vérification seuil JaCoCo 60 % (échec si insuffisant)
```

Le workflow `release.yml` gère la livraison : sur tag `backend-v*`, il construit l'image Docker multi-stage (builder Maven → runtime JRE 21 Alpine), l'optimise (couches Docker séparées par dépendances/classes/resources pour maximiser le cache), et la publie sur GHCR (`ghcr.io/org/taskforce-api:vX.Y.Z`). Le workflow `version-management.yml` bumpe automatiquement le SemVer basé sur les labels des PRs (`feat` → minor, `fix` → patch, `breaking` → major).

**Sécurité du build** : le script `scripts/security-scan.ps1` intègre trois outils de sécurité complémentaires. Trivy (`-Trivy`) scanne l'image Docker finale pour détecter les CVE dans les packages OS Alpine et les JARs Maven. Semgrep (`-Sast`) analyse le code source Java pour détecter les patterns vulnérables (SQL injection, path traversal, secrets en dur). OWASP Dependency-Check (`-DependencyCheck`) vérifie les dépendances Maven contre la base NVD. OWASP ZAP (`-Dast`) effectue un scan DAST de l'API déployée — résultat : 0 HIGH, 4 MEDIUM (CSP en environnement dev, configuré strict en prod).

**Gestion des dépendances Maven** : `spring-boot-starter-parent` 4.0 gère les versions des librairies Spring. Les dépendances hors BOM Spring ont leurs versions verrouillées dans les `<properties>` du `pom.xml`. Dependabot crée des PRs pour les mises à jour de sécurité — les CVE sur les dépendances Maven sont traitées en priorité P1.

---

> 🔗 [[Architecture_C4]] — [[Contrats_API]] — [[Plan_Tests_Backend]] — [[PSSI]] —
> [[Audit_RGPD_Conformite]] — [[Journal_Decisions_ADR]] — [[Roadmap_Backlog]]

**Dernière mise à jour :** 05/07/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
