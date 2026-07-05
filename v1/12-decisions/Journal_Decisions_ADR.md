---
id: journal-decisions-adr
title: Journal de décisions d'architecture (ADR) — TaskForce V1
doc_type: adr
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [adr, decisions, architecture, backend, frontend, ia, securite, memoire, rncp]
---

# 📋 Journal de décisions d'architecture (ADR) — TaskForce V1

> Registre des décisions structurantes prises durant la conception et le développement de TaskForce.
> Chaque ADR documente **le contexte**, **la décision retenue**, **les alternatives écartées** et
> **les conséquences observées**. Source de vérité : code + migrations Flyway + tests.
>
> **Format** : inspiré de [Michael Nygard's ADR template](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).
> Chaque décision est démontrée par une preuve dans le code.

---

## Index

| ID | Titre | Statut | Date |
|---|---|:---:|:---:|
| [ADR-001](#adr-001--stack-technique--spring-boot-4--maven--java-21) | Stack technique : Spring Boot 4 + Maven + Java 21 | ✅ Accepté | Nov 2025 |
| [ADR-002](#adr-002--multi-tenant-par-workspace--hiérarchie-owneradminmember) | Multi-tenant par workspace, hiérarchie OWNER/ADMIN/MEMBER | ✅ Accepté | Nov 2025 |
| [ADR-003](#adr-003--keycloak-comme-identity-provider--jwt-hs512) | Keycloak comme Identity Provider + JWT HS512 | ✅ Accepté | Nov 2025 |
| [ADR-004](#adr-004--groq-api-appelée-directement-en-java-pas-de-microservice-python) | Groq API appelée directement en Java, pas de microservice Python | ✅ Accepté | Mar 2026 |
| [ADR-005](#adr-005--pgvector-natif-postgresql-pas-de-base-vectorielle-séparée) | pgvector natif PostgreSQL, pas de base vectorielle séparée | ✅ Accepté | Avr 2026 |
| [ADR-006](#adr-006--rabbitmq--stomp-pour-le-temps-réel) | RabbitMQ + STOMP pour le temps réel | ✅ Accepté | Déc 2025 |
| [ADR-007](#adr-007--politique-no-mock--testcontainers-pour-les-tests-dintégration) | Politique no-mock : Testcontainers pour les tests d'intégration | ✅ Accepté | Jan 2026 |
| [ADR-008](#adr-008--modèle-hybride-fk--long-id-pour-authfacturation) | Modèle hybride FK : `Long id` pour Auth/Facturation | ✅ Accepté | Déc 2025 |
| [ADR-009](#adr-009--brain-os--architecture-1-workspace--1-brain-onetoone-unique) | Brain OS : 1 workspace = 1 brain, @OneToOne unique | ✅ Accepté | Avr 2026 |
| [ADR-010](#adr-010--observabilité--opentelemetry--signoz-prometheus-en-complément) | Observabilité : OpenTelemetry → SigNoz, Prometheus en complément | ✅ Accepté | Fév 2026 |

---

## ADR-001 — Stack technique : Spring Boot 4 + Maven + Java 21

**Date** : Novembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce nécessite un backend REST robuste, capable de gérer la multi-tenancy, une authentification
déléguée (Keycloak/OAuth2), des webhooks Stripe, la messagerie temps réel (STOMP/WebSocket) et 56
migrations de base de données. Le choix de l'écosystème backend est structurant pour toute la durée
du projet (9 mois, mono-développeur).

### Décision

**Spring Boot 4.0 (RC), Java 21 LTS, Maven** comme toolchain backend principale.

```xml
<!-- pom.xml — preuve -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>4.0.0-SNAPSHOT</version>
</parent>
<java.version>21</java.version>
```

**Preuve** : `backend/tf-api/pom.xml` — Maven (pas Gradle, aucun `build.gradle` présent).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Quarkus** | Moins mature pour OAuth2/Keycloak intégré ; courbe d'apprentissage en contexte solo |
| **Micronaut** | Moins d'intégrations natives Spring Security + Testcontainers |
| **Gradle** | Maven suffisant, projet mono-module ; cohérence avec les exemples Spring officiel |
| **Java 17** | Java 21 = LTS + Virtual Threads (Project Loom) ; Spring Boot 4 en requiert min 21 |

### Conséquences

- **✅ Positif** : Spring Security + OAuth2 ResourceServer natif pour Keycloak ; Testcontainers Spring Boot official support ; JaCoCo intégré Maven.
- **✅ Positif** : Java 21 Virtual Threads activables si besoin de scalabilité I/O-bound.
- **⚠️ Risque** : Spring Boot 4 était en RC lors du démarrage — risque de breaking changes (géré par veille active).
- **📝 Note** : Le `ARCHITECTURE.md` original du projet listait par erreur Gradle ; corrigé dans [[CdCT_v2]].

---

## ADR-002 — Multi-tenant par workspace, hiérarchie OWNER/ADMIN/MEMBER

**Date** : Novembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce doit supporter plusieurs organisations (entreprises/équipes) indépendantes sur la même
instance, avec un contrôle d'accès granulaire. Deux approches classiques : base de données séparée
par tenant (isolation maximale) ou schéma unique avec discriminant de tenant (multi-tenant logique).

### Décision

**Multi-tenant logique** : toutes les entités métier portent une FK `workspace_id`. L'isolation est
assurée au niveau applicatif par `AuthorizationService`. La hiérarchie de rôles est un enum Java :

```java
// WorkspaceRole.java
public enum WorkspaceRole {
    OWNER,   // accès total, gestion billing, suppression workspace
    ADMIN,   // gestion membres, projets, paramètres
    MEMBER   // participation aux projets assignés
}
```

Contrôle au niveau service :

```java
// AuthorizationService.java
public void requireManager(Long workspaceId) {
    WorkspaceMember member = getMemberOrThrow(workspaceId);
    if (member.getRole() == WorkspaceRole.MEMBER) {
        throw new ForbiddenException("Action réservée aux admins et owners");
    }
}
```

**Preuve** : `core/service/AuthorizationService.java` · `core/enums/WorkspaceRole.java` ·
migration `V4__workspace_members.sql` (colonne `role VARCHAR(20)`).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Base séparée par tenant** | Complexité opérationnelle hors de portée pour un projet académique solo |
| **Schéma PostgreSQL par tenant** | Migrations Flyway complexifiées ; overhead de connexion |
| **4 rôles** (Manager/Collaborateur/Admin/Invité) | Modèle du CdCF v1 — remplacé car MEMBER recouvre les collaborateurs, OWNER gère le billing, pas besoin de 4 niveaux |
| **RBAC basé sur permissions atomiques** | Sur-ingénierie pour V1 ; 3 rôles suffisent pour les UC réels |

### Conséquences

- **✅ Positif** : Schema unique, migrations simples, requêtes joins naturelles avec `workspace_id`.
- **✅ Positif** : Slug workspace unique (migration V3) → URLs propres (`/w/acme-corp/...`).
- **⚠️ Risque** : Isolation purement logique — une faille dans `AuthorizationService` expose tous les tenants. Mitigé par tests `WorkspaceMemberGuardTest`.
- **📝 Note** : Le CdCF v1 mentionnait les rôles `Manager/Collaborateur/Admin/Invité` — corrigé dans [[CdCF_v2]].

---

## ADR-003 — Keycloak comme Identity Provider + JWT HS512

**Date** : Novembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté · ⚠️ **partiellement superseded par [[#ADR-011 — Émission des tokens par Keycloak (OIDC RS256), retrait du JWT HS512 custom|ADR-011]]** (05/07/2026) — le volet « JWT HS512 émis par le backend » est abandonné au profit de tokens Keycloak RS256. Keycloak reste l'IdP.

### Contexte

TaskForce nécessite une authentification robuste avec gestion des sessions, refresh tokens, OTP
à l'inscription, et potentiellement SSO/SAML pour les clients Enterprise. Implémenter un système
d'auth maison présente un risque de sécurité élevé.

### Décision

**Keycloak** délégué comme IdP pour la gestion des sessions et l'émission de JWT. Le backend
Spring Boot valide les tokens via OAuth2 Resource Server. L'OTP est implémenté dans le backend
applicatif **avant** la création du compte Keycloak (étape d'inscription).

```java
// SecurityConfig.java
http.oauth2ResourceServer(oauth2 -> oauth2
    .jwt(jwt -> jwt.decoder(jwtDecoder())));
```

```yaml
# application.yml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: ${KEYCLOAK_ISSUER_URI}
```

**Preuve** : `shared/config/SecurityConfig.java` · `shared/config/KeycloakConfig.java` ·
`keycloak/` (realm config) · `core/service/AuthService.java` (login délègue à Keycloak).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Spring Security custom** (BCrypt + sessions) | Réimplémentation de roues — gestion refresh tokens, OIDC, revocation complexe |
| **Auth0 / Okta** | Coût ; dépendance service tiers externe pour un projet académique |
| **JWT maison sans IdP** | Pas de gestion de révocation ; risque sécurité élevé |
| **RS256** (asymétrique) | HS512 suffisant en monorepo où backend + Keycloak partagent le secret ; RS256 utile pour multi-service |

### Conséquences

- **✅ Positif** : Gestion refresh tokens, révocation, sessions multi-device déléguée à Keycloak.
- **✅ Positif** : Foundation SSO/SAML Enterprise disponible sans code supplémentaire.
- **⚠️ Complexité** : Keycloak dev = image build custom (`keycloak/Dockerfile`) ; nécessite une config realm exportée.
- **📝 Note** : OTP à l'inscription seulement — le login délègue entièrement à Keycloak (voir [[Diagrammes_Sequence_UML]] §2).

---

## ADR-004 — Groq API appelée directement en Java, pas de microservice Python

**Date** : Mars 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce intègre une fonctionnalité de **Smart Assign** (suggestion automatique d'assignataire
d'issue par LLM) et un **Assistant IA** (chat completion en streaming). Un service Python
(`ai-service/`, FastAPI) avait été créé comme stub initial mais n'a jamais été opérationnel.

### Décision

Appel **direct** à l'API Groq (compatible OpenAI) depuis le backend Java via `RestTemplate`
configuré. Le service Python est marqué vestigial (DT-010) et non utilisé en production.

```java
// GroqService.java
private static final String GROQ_BASE_URL = "https://api.groq.com/openai/v1";

public String chatCompletion(String model, String systemPrompt,
                              String userPrompt, boolean jsonMode) {
    assertApiKeyPresent();
    // RestTemplate vers api.groq.com/openai/v1/chat/completions
}

public void streamCompletion(String model, String systemPrompt,
                              String userPrompt, StreamCallback callback) {
    // SSE chunked response → WebSocket relay
}
```

**Preuve** : `core/service/GroqService.java` (appel HTTP direct) · `ai-service/` (stub vide, non
branché) · `Architecture.md` §5 (DT-010 documenté).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Microservice Python (FastAPI)** | Overhead opérationnel (2e service, 2e conteneur, IPC) pour V1 solo ; stub jamais complété |
| **LangChain4j** | Lib Java mature mais ajoute une abstraction inutile sur Groq qui est déjà compatible OpenAI |
| **OpenAI API** | Groq = gratuit sur tier développeur + latence plus faible (LPU inference) |
| **Modèle hébergé localement (Ollama)** | RAM requise incompatible avec contraintes VM école (~4 Go) |

### Conséquences

- **✅ Positif** : Zero déploiement additionnel ; `GroqService` injectable dans tout service Spring.
- **✅ Positif** : `streamCompletion()` relay via WebSocket STOMP pour l'assistant IA temps réel.
- **⚠️ Risque** : Dépendance API externe (rate-limit Groq) — mode dégradé prévu (scoring local seul) via `GroqServiceContractTest`.
- **📝 Note** : `ai-service/` reste dans le monorepo à des fins de documentation mais n'est pas démarré en prod (voir [[Architecture_C4]] §3, DT-010).

---

## ADR-005 — pgvector natif PostgreSQL, pas de base vectorielle séparée

**Date** : Avril 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

Brain OS nécessite le stockage et la recherche de vecteurs d'embeddings pour les `KnowledgeNode`
(recherche sémantique sur la base de connaissance du workspace). Les options classiques incluent
une base vectorielle dédiée (Pinecone, Weaviate, ChromaDB) ou une extension PostgreSQL.

### Décision

**pgvector** activé dans PostgreSQL 18 existant. Nouveau type `vector(1536)` pour les embeddings
dans la table `knowledge_nodes`.

```sql
-- V51__brain_os_foundation.sql
CREATE EXTENSION IF NOT EXISTS vector;

ALTER TABLE knowledge_nodes
    ADD COLUMN embedding vector(1536);

CREATE INDEX idx_knowledge_nodes_embedding
    ON knowledge_nodes USING ivfflat (embedding vector_cosine_ops)
    WITH (lists = 100);
```

`BrainWorkspace` lie le workspace à son brain via `@OneToOne` :

```java
// BrainWorkspace.java — "1 workspace = 1 brain"
@OneToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "workspace_id", nullable = false, unique = true)
private Workspace workspace;
```

**Preuve** : `V51__brain_os_foundation.sql` · `core/model/BrainWorkspace.java` ·
`core/model/KnowledgeNode.java` (colonne `embedding vector(1536)`).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Pinecone** | Service externe payant après free tier ; dépendance supplémentaire ; données sortant de l'infra |
| **ChromaDB** | Conteneur Python additionnel ; IPC REST entre Java et Python |
| **Weaviate** | Même problème + configuration GraphQL complexe |
| **Elasticsearch** | Surcharge significative (RAM) ; kNN search moins natif que pgvector cosine |

### Conséquences

- **✅ Positif** : Zero conteneur additionnel ; transactions ACID entre données métier et embeddings.
- **✅ Positif** : Migrations Flyway versionnées pour le schema vectoriel comme pour le reste.
- **✅ Positif** : `ivfflat` index sur `vector_cosine_ops` — recherche k-NN efficace pour 1 536 dimensions (OpenAI ada-002 / Groq compatible).
- **⚠️ Limite** : Moins scalable que Pinecone pour des millions de vecteurs — acceptable pour V1 mono-workspace.

---

## ADR-006 — RabbitMQ + STOMP pour le temps réel

**Date** : Décembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce propose un chat en temps réel et des notifications live (ex: mise à jour d'issue,
nouveau commentaire). La fonctionnalité nécessite un canal push du serveur vers les clients.

### Décision

**RabbitMQ 4** avec plugin STOMP activé comme broker de messages. Le frontend utilise
**SockJS + STOMP.js** ; le backend Spring utilise `spring-boot-starter-amqp` et
`spring-websocket`.

```yaml
# docker-compose.yml (extrait)
rabbitmq:
  image: rabbitmq:4-management
  ports:
    - "5672:5672"
    - "15672:15672"
    - "61613:61613"  # STOMP
```

**Preuve** : `docker-compose.yml` (service rabbitmq) · `shared/config/` (WebSocketConfig) ·
`frontend/lib/hooks/use-stomp.ts`.

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **SSE (Server-Sent Events)** | Unidirectionnel serveur→client ; pas adapté au chat bidirectionnel |
| **WebSocket natif (sans broker)** | Pas de persistence des messages ; scaling horizontal difficile |
| **Socket.io (Node.js)** | Exige un service Node séparé ; hors stack Java |
| **Kafka** | Sur-dimensionné ; persistence distribuée non requise pour V1 |
| **Redis Pub/Sub** | Option valable mais RabbitMQ couvre déjà la messagerie async (queues Stripe, emails) — double usage évite un 2e composant |

### Conséquences

- **✅ Positif** : RabbitMQ utilisé aussi pour les queues async (emails, webhooks Stripe) — un seul broker pour 2 usages.
- **✅ Positif** : STOMP = protocole standardisé, libs dispo pour tout client (browser, mobile, test).
- **⚠️ Risque** : Configuration STOMP + SockJS nécessite attention CORS (`CorsConfig.java:65`) — documenté comme DT-001-adjacent.

---

## ADR-007 — Politique no-mock : Testcontainers pour les tests d'intégration

**Date** : Janvier 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

Les tests d'intégration backend nécessitent PostgreSQL, RabbitMQ, parfois Keycloak. La pratique
courante de mocker le repository/datasource présente un risque : les mocks ne reproduisent pas
le comportement réel de la base (contraintes FK, triggers, types PostgreSQL spécifiques).

### Décision

**Testcontainers** pour démarrer des instances réelles PostgreSQL (et RabbitMQ si besoin) dans les
tests d'intégration. **Zéro mock** sur les couches d'infrastructure.

```java
// Exemple : WorkspaceServiceIntegrationTest.java (pattern)
@SpringBootTest
@Testcontainers
class WorkspaceServiceIntegrationTest {

    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:18-alpine")
            .withInitScript("db/migration"); // Flyway appliqué
    // ...
}
```

**Preuve** : 72 fichiers de tests dans `src/test/` · `pom.xml` (dépendance `testcontainers-bom`) ·
politique documentée dans [[Tests]].

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **H2 in-memory** | Dialecte SQL différent de PostgreSQL 18 ; pgvector non supporté ; `information_schema` diverge |
| **Mock repositories (@MockBean)** | Ne teste pas les requêtes JPQL, les contraintes DB, ni les migrations Flyway |
| **Base de test partagée (non-isolée)** | État persistant entre tests → flakiness ; parallélisation impossible |

### Conséquences

- **✅ Positif** : Tests de migration Flyway inclus dans chaque intégration test — si V{n} casse, le build casse.
- **✅ Positif** : pgvector testable (type `vector`, index `ivfflat`) — impossible avec H2.
- **⚠️ Coût** : Tests d'intégration plus lents (démarrage conteneur ~5–10 s) ; compensé par `@SpringBootTest` singleton pattern.
- **📝 Lien** : Mémoire auto-save [[taskforce-no-mock-seed]] — règle de session persistante.

---

## ADR-008 — Modèle hybride FK : `Long id` pour Auth/Facturation

**Date** : Décembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

Les entités d'audit et de facturation (`AuditLog`, `RefreshToken`, `OtpVerification`,
`Subscription`, `SubscriptionHistory`) référencent des `User` ou `Workspace`. Si ces entités
utilisent `@ManyToOne`, la suppression d'un utilisateur peut cascader et effacer l'historique
d'audit ou les données de facturation.

### Décision

**Modèle hybride** : les entités métier (projets, issues, membres) utilisent `@ManyToOne` + FK
pour les joins naturels ; les entités d'audit/auth/facturation stockent `Long userId` / `Long
workspaceId` comme simples identifiants — sans contrainte FK JPA, sans cascade.

```java
// AuditLog.java
/**
 * FK stockée en Long, pas en @ManyToOne.
 * Raison : le journal doit survivre à la suppression de l'utilisateur.
 * Un @ManyToOne avec ON DELETE CASCADE effacerait les traces d'audit.
 */
@Column(name = "user_id")
private Long userId;  // pas @ManyToOne User

// RefreshToken.java — même pattern
@Column(name = "user_id", nullable = false)
private Long userId;
```

**Preuve** : `core/model/AuditLog.java` (Javadoc explicite) · `core/model/RefreshToken.java` ·
`core/model/Subscription.java` · `core/model/SubscriptionHistory.java`.

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **@ManyToOne partout** | Cascade DELETE sur User effacerait l'historique d'audit et les données de facturation |
| **ON DELETE SET NULL** | AuditLog sans userId = log inexploitable pour la conformité RGPD |
| **Soft delete User** | Complexifie toutes les requêtes ; RGPD impose parfois la suppression physique |

### Conséquences

- **✅ Positif** : Suppression d'un utilisateur (`DELETE FROM users`) sans perte d'audit trail ni d'historique de paiement.
- **✅ Positif** : Cycle de vie découplé : données de facturation survivent à la désinscription.
- **⚠️ Limite** : Pas de join JPA automatique pour récupérer le détail de l'utilisateur depuis un `AuditLog` — requête manuelle si besoin.
- **📝 Documentation** : Modèle documenté dans [[Diagramme_Classes_UML]] §6 (note "Modèle hybride") et [[CdCT_v2]] §3.

---

## ADR-009 — Brain OS : 1 workspace = 1 brain, @OneToOne unique

**Date** : Avril 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

Brain OS est la fonctionnalité de knowledge graph de TaskForce. Lors de la conception, deux
modèles étaient envisageables : un brain global partagé entre workspaces, ou un brain par
workspace.

### Décision

**1 workspace = 1 brain**, contrainte d'unicité stricte (`@OneToOne unique = true`).

```java
// BrainWorkspace.java
/**
 * Brain OS d'un workspace : la mémoire de connaissance de l'entreprise/produit.
 * 1 workspace = 1 brain (contrainte d'unicité sur workspace_id).
 */
@OneToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "workspace_id", nullable = false, unique = true)
private Workspace workspace;
```

Structure des `KnowledgeNode` : chaque nœud appartient à un `BrainWorkspace` et peut avoir
des liens (`KnowledgeLink`) vers d'autres nœuds du même brain.

**Preuve** : `core/model/BrainWorkspace.java` · `V51__brain_os_foundation.sql` ·
`core/model/KnowledgeNode.java` · `core/model/KnowledgeLink.java`.

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Brain global cross-workspace** | Isolation tenants violée — les connaissances d'un workspace ne doivent pas être accessibles par un autre |
| **N brains par workspace** | Fragmentation inutile ; un brain unifié est plus cohérent pour la recherche sémantique |
| **Knowledge graph externe (Neo4j)** | Conteneur additionnel ; pgvector + JSON couvre les besoins V1 |

### Conséquences

- **✅ Positif** : Isolation totale entre tenants (workspace A ne voit jamais les nodes de workspace B).
- **✅ Positif** : Initialisation auto du brain à la création du workspace (service `BrainWorkspaceService`).
- **✅ Positif** : `@OneToOne` garantit l'unicité au niveau DB (contrainte `UNIQUE` sur `workspace_id`).
- **📝 Note** : Phase 0 du Brain OS livrée (structure de données) ; phases 1–3 (auto-sync, embeddings, search) en roadmap produit.

---

## ADR-010 — Observabilité : OpenTelemetry → SigNoz, Prometheus en complément

**Date** : Février 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce en production nécessite une observabilité couvrant les trois piliers : traces distribuées,
métriques, logs. Le CdCT v1 mentionnait Grafana + Prometheus comme stack principale — ce n'est
pas ce qui a été implémenté.

### Décision

**OpenTelemetry Collector** comme agrégateur central des signaux. **SigNoz** (self-hosted) comme
backend de visualisation (traces + métriques + logs en un seul outil). **Prometheus** conservé
en complément pour les 9 règles d'alerte opérationnelles.

```yaml
# observability/otel-collector-config.yaml (extrait)
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: "0.0.0.0:4317"
      http:
        endpoint: "0.0.0.0:4318"
exporters:
  otlp/signoz:
    endpoint: "signoz-otel-collector:4317"
  prometheus:
    endpoint: "0.0.0.0:8889"
```

**Preuve** : `observability/otel-collector-config.yaml` · `observability/signoz/` (compose +
config) · `observability/alerts/` (9 règles Prometheus).

### Alternatives écartées

| Alternative | Raison de rejet |
|---|---|
| **Grafana + Prometheus seul** | Stack traces (Tempo) et logs (Loki) nécessitent 2 composants additionnels ; SigNoz couvre les 3 en un |
| **Datadog** | Coût ; dépendance SaaS externe ; données telemetrie sortant de l'infra |
| **Elastic Stack (ELK)** | RAM requise (Elasticsearch ~2 Go min) incompatible avec VM école contrainte |
| **Zipkin** | Traces seules, pas de métriques ni logs ; stack incomplète |

### Conséquences

- **✅ Positif** : OpenTelemetry = standard CNCF ; exporters interchangeables si SigNoz remplacé.
- **✅ Positif** : SigNoz self-hosted = données restent sur l'infra (RGPD-friendly).
- **✅ Positif** : 9 règles Prometheus conservées car Prometheus AlertManager = notification ops mature.
- **⚠️ Risque** : SigNoz consomme ~1 Go RAM supplémentaire en prod — acceptable avec VM 8 Go.
- **📝 Note** : Le CdCT v1 listait "Grafana/Prometheus" comme stack primaire — corrigé dans [[CdCT_v2]] §6.

---

## ADR-011 — Émission des tokens par Keycloak (OIDC RS256), retrait du JWT HS512 custom

**Date** : Juillet 2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté — **supersède la partie « JWT HS512 » de [[#ADR-003 — Keycloak comme Identity Provider + JWT HS512|ADR-003]]**

### Contexte

L'ADR-003 avait retenu Keycloak comme IdP mais, par glissement pragmatique lors de l'implémentation de
l'OTP, le backend **émettait ses propres JWT HS512** (`JwtService`, clé symétrique `JWT_SECRET`) au lieu
de déléguer les tokens à Keycloak. Dette documentée **PC-019 / TF-SEC-009** : clé symétrique (fuite =
tous les tokens compromis), pas de révocation de session native, pas de rotation de clés, recommandation
ANSSI de préférer RS256/OIDC. Or `KeycloakAuthService` implémentait **déjà** le flux ROPC complet
(authenticate/refresh/revoke) — ses tokens étaient simplement jetés.

### Décision

**Le backend ne signe plus aucun token.** Keycloak émet les access/refresh tokens (RS256) ; l'API agit en
pur **Resource Server** :

- **Validation** : `NimbusJwtDecoder` sur le JWK Set Keycloak (`/protocol/openid-connect/certs`) +
  validation de l'`issuer` (`SecurityConfig.jwtDecoder`). Plus de décodeur HS512.
- **Login** : `AuthService.login` renvoie directement les tokens de `KeycloakAuthService.authenticate` (ROPC).
- **Refresh** : `KeycloakAuthService.refreshToken` (rotation gérée par l'IdP) — plus de table `refresh_tokens`.
- **Logout** : `KeycloakService.logoutUser` (`users().logout()`) invalide toutes les sessions côté IdP.
- **Identité courante** : inchangée — les contrôleurs résolvent l'utilisateur via le claim `email`
  (présent dans le token Keycloak), donc **aucun des ~21 contrôleurs n'a été modifié**.
- **Suppressions** : `JwtService`, `JwtDecoderConfig`, `TokenCleanupScheduler` (+ tests). Table
  `refresh_tokens` conservée (pas de migration destructive) mais inutilisée.

### Conséquence produit assumée

L'**auto-login après vérification OTP / paiement est retiré** : Keycloak ne peut émettre un token sans mot
de passe (absent à ce stade, l'OTP arrivant par email). Le parcours redirige désormais vers `/auth/login`
(décision produit validée le 05/07). Alternatives écartées : Token Exchange Keycloak (surface de sécurité
accrue — le back pourrait usurper n'importe qui) ; conserver un token HS512 pour ce seul cas (ne fermerait
pas PC-019).

### Preuve

`SecurityConfig.java` (décodeur RS256) · `AuthService.java` (login/refresh/logout) ·
`KeycloakAuthService.java` (ROPC déjà présent) · `KeycloakService.logoutUser` ·
`application-prod.yml` (resourceserver.jwt issuer/jwk). **Vérifié : 658 tests backend + 54 frontend verts.**

### Conséquences

- **✅ Positif** : plus de clé symétrique ; rotation de clés et révocation de session gérées par l'IdP (ferme PC-019).
- **✅ Positif** : surface de code auth réduite (3 classes + 2 tests supprimés) ; les tests contrôleurs, qui
  mockent déjà le principal `Jwt` avec un claim `email`, restent valides sans modification.
- **⚠️ Pré-requis déploiement** : le realm Keycloak doit émettre le claim `email` dans l'access token
  (scope `email` par défaut) — sinon la résolution d'utilisateur échoue.
- **📝 Note** : l'auto-login post-inscription est perdu (cf. ci-dessus) ; UX « login après inscription ».

---

> 🔗 Voir aussi : [[Architecture_C4]] · [[CdCT_v2]] · [[CdCF_v2]] · [[Table_Reconciliation]] ·
> [[Diagramme_Classes_UML]] · [[Diagrammes_Sequence_UML]] · [[Note_Cadrage]].
>
> Ce journal est la source de vérité pour les décisions non évidentes. Toute nouvelle décision
> structurante (migration Flyway majeure, changement de stack, nouveau pattern) doit être ajoutée ici.
