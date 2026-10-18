---
id: journal-decisions-adr
title: Journal de décisions d'architecture (ADR) — TaskForce V1
doc_type: adr
statut: valide
version: 1.1
date: "20/09/2026"
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
| [ADR-004](#adr-004--groq-api-appelée-directement-en-java-pas-de-microservice-python) | Groq API appelée directement en Java, pas de microservice Python | Remplacée par ADR-019 | Mar 2026 |
| [ADR-005](#adr-005--pgvector-natif-postgresql-pas-de-base-vectorielle-séparée) | pgvector natif PostgreSQL, pas de base vectorielle séparée | ✅ Accepté | Avr 2026 |
| [ADR-006](#adr-006--rabbitmq--stomp-pour-le-temps-réel) | RabbitMQ + STOMP pour le temps réel | ✅ Accepté | Déc 2025 |
| [ADR-007](#adr-007--politique-no-mock--testcontainers-pour-les-tests-dintégration) | Politique no-mock : Testcontainers pour les tests d'intégration | ✅ Accepté | Jan 2026 |
| [ADR-008](#adr-008--modèle-hybride-fk--long-id-pour-authfacturation) | Modèle hybride FK : `Long id` pour Auth/Facturation | ✅ Accepté | Déc 2025 |
| [ADR-009](#adr-009--brain-os--architecture-1-workspace--1-brain-onetoone-unique) | Brain OS : 1 workspace = 1 brain, @OneToOne unique | ✅ Accepté | Avr 2026 |
| [ADR-010](#adr-010--observabilité--opentelemetry--signoz-prometheus-en-complément) | Observabilité : OpenTelemetry → SigNoz, Prometheus en complément | ✅ Accepté | Fév 2026 |
| [[#ADR-011 — Émission des tokens par Keycloak (OIDC RS256), retrait du JWT HS512 custom\|ADR-011]] | Émission des tokens par Keycloak (OIDC RS256), retrait du JWT HS512 custom | ✅ Accepté | Juil 2026 |
| ADR-012 | Brain OS : moteur interne, produit-connaissance exposé (brouillon, `recherche/decisions/`) | 📝 Proposé | Juil 2026 |
| [[#ADR-013 - Runner local de délégation : Claude Code sur le poste de l'utilisateur\|ADR-013]] | Runner local de délégation : Claude Code sur le poste de l'utilisateur | ✅ Accepté (prototype) | Sept 2026 |
| [[#ADR-014 - TaskForce 1.0 : projet open source lean et auto-hébergeable\|ADR-014]] | TaskForce 1.0 : projet open source lean et auto-hébergeable | ✅ Accepté | Oct 2026 |
| [[#ADR-015 - Licence AGPL-3.0\|ADR-015]] | Licence AGPL-3.0 | ✅ Accepté, appliqué | Oct 2026 |
| [[#ADR-016 - Retrait de la facturation et des limites de plan\|ADR-016]] | Retrait de la facturation et des limites de plan | ✅ Mis en œuvre (lot 2, 18/10) | Oct 2026 |
| [[#ADR-017 - Brain OS réduit à son cœur\|ADR-017]] | Brain OS réduit à son cœur | ✅ Accepté, mis en œuvre (lot 3) | Oct 2026 |
| [[#ADR-018 - Agents de code : Claude Code et Copilot\|ADR-018]] | Agents de code : Claude Code et Copilot | ✅ Accepté (lot 5) | Oct 2026 |
| [[#ADR-019 - Fournisseur d'IA générique, Ollama par défaut\|ADR-019]] | Fournisseur d'IA générique, Ollama par défaut | ✅ Accepté, mis en œuvre (lot 4) | Oct 2026 |
| [[#ADR-020 - Connexion générale : MCP et webhooks sortants\|ADR-020]] | Connexion générale : MCP et webhooks sortants | ✅ Accepté (lot 6) | Oct 2026 |
| [[#ADR-021 - Application desktop locale, sur le modèle de Claude Desktop\|ADR-021]] | Application desktop locale, sur le modèle de Claude Desktop | ✅ Accepté (cap), essai à faire | Oct 2026 |

---

## ADR-001 — Stack technique : Spring Boot 4 + Maven + Java 21

**Date** : Novembre 2025 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté

### Contexte

TaskForce nécessite un backend REST robuste, capable de gérer la multi-tenancy, une authentification
déléguée (Keycloak/OAuth2), des webhooks Stripe, la messagerie temps réel (STOMP/WebSocket) et
**72 migrations** de base de données (chiffre au 23/07/2026 ; l'ADR portait 56, valeur de sa
rédaction). Le choix de l'écosystème backend est structurant pour toute la durée du projet
(9 mois, mono-développeur).

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

### Alternatives écartées, dans l'écosystème Java

| Alternative | Raison de rejet |
|---|---|
| **Quarkus** | Moins mature pour OAuth2/Keycloak intégré ; courbe d'apprentissage en contexte solo |
| **Micronaut** | Moins d'intégrations natives avec Spring Security |
| **Gradle** | Maven suffisant, projet mono-module ; cohérence avec les exemples officiels Spring |
| **Java 17** | Java 21 est LTS et apporte les threads virtuels ; Spring Boot 4 exige au minimum Java 21 |

### Alternatives écartées, face au cahier des charges

> **Section ajoutée le 23/07/2026.** Elle manquait, et c'est celle qui compte le plus : le cahier
> des charges (§5, « Exigences Techniques ») propose **PHP avec Symfony, ou Node.js** côté back-end.
> Ce sont donc ces deux options que le jury demandera d'écarter, pas Quarkus ni Micronaut.
>
> **Le cadre est clair et a été confirmé par l'école : le choix technique est libre, à condition de
> pouvoir l'argumenter.** Le critère C22-1 demande d'ailleurs littéralement « un choix de
> technologies et frameworks back-end **adaptés** », pas un choix conforme au cahier des charges.
> La grille récompense la pertinence, pas l'obéissance. Encore faut-il que l'argument soit écrit.

| Alternative du CDC | Raison du non-choix |
|---|---|
| **PHP avec Symfony** | Le cœur fonctionnel du produit est un moteur d'affectation qui combine similarité vectorielle, charge et historique, exécuté sur des lots d'issues. Java offre ici un typage fort sur un domaine riche (48 entités, 72 migrations), un écosystème mature pour la recherche vectorielle, et surtout les **threads virtuels** de Java 21, adaptés à un service dont le coût dominant est l'attente d'entrées-sorties : base de données, Keycloak, modèle de langage. Symfony aurait convenu pour la partie CRUD, moins pour ce cœur-là. |
| **Node.js** | Écarté pour une raison de cohérence, pas de performance : le front est déjà en TypeScript sur Next.js. Prendre Node au back aurait donné un projet mono-langage, séduisant sur le papier, mais qui n'aurait **rien démontré de plus**. Le titre visé est « Développeur Full Stack » : soutenir deux écosystèmes distincts, avec leurs outillages de test, de build et de sécurité propres, est un exercice plus complet et plus proche de la réalité d'une équipe. |
| **Argument transverse** | La contrainte réelle du projet n'était pas la performance brute mais **la sécurité et la traçabilité** : Spring Security en serveur de ressources OIDC, validation déclarative, Flyway avec `ddl-auto=validate`, JaCoCo. Cet outillage existe ailleurs, mais il est ici intégré et éprouvé, ce qui compte pour un développeur seul sur neuf mois. |

> **Ce qu'il ne faut PAS dire à l'oral** : que le cahier des charges donnerait ces technologies « à
> titre indicatif ». Il ne l'écrit nulle part. L'argument tient sur la pertinence technique et sur
> la liberté de choix confirmée, pas sur une réinterprétation du document.

### Conséquences

- **✅ Positif** : Spring Security et serveur de ressources OAuth2 natifs pour Keycloak ; JaCoCo intégré à Maven.
  <br>⚠️ *Corrigé le 23/07/2026 : la version initiale citait le support officiel de Testcontainers parmi les bénéfices. **Testcontainers n'est pas utilisé** — son client Docker embarqué est incompatible avec le mandataire de Docker Desktop lorsque les tests s'exécutent eux-mêmes en conteneur. Les tests d'intégration tournent contre un PostgreSQL voisin démarré par `scripts/it.ps1`, avec les vraies migrations Flyway. Ne pas invoquer Testcontainers à l'oral : le greffon n'est pas dans le `pom.xml`.*
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

**Date** : Mars 2026 | **Décideur** : Pierre MICHEL | **Statut** : Remplacée par [[#ADR-019 - Fournisseur d'IA générique, Ollama par défaut|ADR-019]] le 18/10/2026 (le code passait déjà par l'`ai-service` Python depuis juillet)

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

## ADR-013 - Runner local de délégation : Claude Code sur le poste de l'utilisateur

**Date** : 20/09/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, **prototype** (désactivé par défaut en production)

> Le numéro ADR-012 est réservé au brouillon `recherche/decisions/ADR-012-DRAFT-brain-os-exposition.md`.

### Contexte

La délégation d'une issue à un agent existe déjà ([[../road_to_v2/Agent_Delivery_Pipeline|Agent Delivery Pipeline]]) :
providers cloud (`claude-api`, `cursor`, `github-copilot`), run tracé, auto-move de l'issue. Le provider
`claude-code` n'était qu'un placeholder, en attente d'une exécution hébergée (Managed Agents).

Le besoin : déléguer une issue à **Claude Code installé sur le poste de la personne**, qui code dans un
vrai checkout, lit le contexte dans TaskForce, et revient avec une pull request.

Quatre contraintes cadrent la solution :

1. **Le backend ne peut pas joindre un poste local** (NAT, pas de port ouvert). L'échange part donc du poste.
2. **En production, Keycloak n'est pas joignable de l'extérieur** : seul nginx expose des ports, le backend
   est le seul interlocuteur de l'IdP (posture de l'ADR-011).
3. **Un agent lit du texte écrit par d'autres** (issues, commentaires, notes). Une instruction glissée
   dans ce texte ne doit pas pouvoir agir au-delà de la tâche.
4. **Conditions d'Anthropic** (page « Legal and compliance » de Claude Code, relue le 20/09/2026). Chaque
   personne peut se connecter au binaire Claude Code non modifié avec **son propre** abonnement. Un
   produit, lui, ne peut ni proposer le login claude.ai dans son application, ni collecter, stocker ou
   relayer les identifiants Claude de ses utilisateurs, ni payer ou intermédier leur usage. Les limites des
   abonnements supposent un usage ordinaire et individuel.

### Décision

**1. Provider « pull ».** `DeliveryAgentProvider.pullBased()` : pour `claude-code`, rien n'est dispatché. Le
run reste `QUEUED` ; un runner le **réclame** (mise à jour atomique : un seul gagnant), travaille, envoie
des signes de vie, puis **pousse** son résultat. Un runner muet plus de 10 min fait passer le run en échec
au lieu de le laisser « en cours » pour toujours. Migration `V88` : `claimed_by`, `claimed_at`, `heartbeat_at`.

**2. Identité machine Keycloak, jamais le mot de passe de la personne.** Un client confidentiel
`tf-runner-<nom>` réduit au grant `client_credentials` (aucun flux navigateur, aucun password grant). Un
jeton de runner cumule quatre preuves signées par Keycloak, toutes requises : le rôle de realm
`delivery-runner`, le préfixe du client, un sujet qui est bien le compte de service de ce client, et le
claim `tf_runner_owner` (mapper « hardcoded claim », modifiable par un administrateur du realm seulement).
Le jeton s'obtient par `POST /api/auth/runner/token`, que le backend relaie vers Keycloak : le runner ne
connaît qu'une URL. Ce relais refuse tout client hors préfixe et ne rend le jeton qu'après avoir vérifié
les quatre preuves. Provisionnement idempotent : `scripts/keycloak-runner.ps1`.

**3. Autorité bornée au propriétaire.** Un runner ne voit et ne réclame que les runs délégués **par son
propriétaire**. Les droits de celui-ci sont réévalués au claim : s'il a perdu l'écriture sur le projet
depuis la délégation, le run est clos en échec, pas exécuté.

**4. Session déléguée : deux bornes empilées.** Le temps d'un run, l'agent agit **au nom du délégant**.

| Borne | Règle |
|---|---|
| Plafond | Les droits de la personne. Chaque appel est évalué par les services existants comme s'il venait d'elle : un projet privé qu'elle ne voit pas reste invisible. |
| Workspace | Un seul : celui du run. |
| Lecture | Liste fermée de sous-arbres : `projects`, `brain`, `my-issues`, `analytics`, plus `POST brain/search` (une lecture portée par un POST). |
| Écriture | `POST/PATCH/PUT` sous `projects/{projet du run}/issues` uniquement. |
| Suppression | Jamais (D6 : la décision destructive reste humaine). |
| Durée | Tant que le run est `RUNNING`, réclamé par ce runner, et au plus 120 min après le claim. |

C'est une liste **d'autorisation** : tout chemin absent est refusé, futurs endpoints compris. Membres,
intégrations, clés, webhooks, serveurs MCP, facturation, profil et les autres workspaces sont hors d'atteinte.
Mise en œuvre : `DeliverySessionFilter`, placé juste après l'authentification du bearer. Transparent pour
un jeton d'utilisateur, **fail-closed** pour un jeton de runner : hors de ses endpoints machine, il lui
faut l'en-tête `X-TaskForce-Delivery-Run` désignant un run valide, sinon `403`. Un jeton qui ressemble à
un jeton de runner sans en porter toutes les preuves est refusé, jamais traité comme un utilisateur.

**5. Exécution locale bornée elle aussi.** Le dépôt est celui que le projet porte dans TaskForce (créé ou
lié à la création du projet). `taskforce-runner` le clone à la demande avec le `gh` de la personne, donc
avec SES droits GitHub, dans son propre dossier ; il n'y a aucun chemin à déclarer (MAJ 21/09/2026). Il y
crée un worktree git isolé sur une branche neuve ; le checkout de la personne n'est jamais touché. Claude Code tourne en mode `dontAsk` avec une liste
fermée d'outils : lire, éditer, `git status/diff/log/add/commit`. Pas de shell libre, pas de réseau, pas de
push. Le runner ne passe **jamais par un shell** pour lancer un processus (tableaux d'arguments ; le nom de modèle venu du serveur est validé avant d'atteindre une ligne de commande). Le **runner** pousse la branche et ouvre la PR après l'agent. **Rien n'est jamais fusionné** (D6).
Le MCP de l'agent reçoit un jeton de courte durée, jamais le secret du runner.

**6. Désactivé par défaut.** `delivery.local-runner.enabled` (vrai en dev, faux en prod). Désactivé,
`claude-code` reste « à venir », et ni les endpoints machine ni le filtre n'existent.

**7. Chacun son Claude Code, chacun son compte.** Le runner lance le Claude Code **de la personne**, non
modifié, sur son poste ; elle s'y est connectée elle-même, avec son abonnement (`agent.auth: "subscription"`)
ou sa clé API (`"api-key"`). TaskForce ne voit, ne stocke et ne relaie jamais ses identifiants Claude, et ne
paie ni n'intermédie son usage. C'est la forme que les conditions d'Anthropic admettent, pour Pierre comme
pour tout autre utilisateur. En mode abonnement, la clé API ambiante est retirée de l'environnement de
l'agent, pour ne pas facturer le compte API sans prévenir : c'est le choix de la personne, le runner ne
retire aucune méthode d'authentification.

> **Correction du 20/09/2026.** La première rédaction disait « abonnement = prototype personnel, un usage
> produit suppose une clé API ». C'était une lecture incomplète de la page d'Anthropic, qui prévoit
> explicitement qu'un utilisateur se connecte au binaire non modifié avec son propre abonnement. Ce qui
> reste interdit : un login claude.ai dans TaskForce, des jetons Claude côté serveur, un usage payé ou
> revendu par TaskForce. Avant une mise sur le marché : accepter les Commercial Terms d'Anthropic, vérifier
> l'usage du nom et du logo (on peut écrire que le produit fait tourner Claude Code, pas en faire un nom de
> fonctionnalité ni afficher le logo sans permission), et faire confirmer le cas d'usage par écrit. Cette
> lecture n'est pas un avis juridique.

### Écart assumé à la décision D2 de la spec

D2 dit : « l'exécution tourne dans le cloud du provider, TaskForce n'héberge aucun runtime lourd ». La
seconde moitié reste vraie : TaskForce n'héberge rien, le runtime est chez la personne. L'esprit de D2 et
D3 est tenu (exécution sous le compte et le plan de l'utilisateur, coût porté par lui). La lettre ne l'est
pas : ce n'est pas le cloud du provider. La spec (§7) citait déjà ce « runner léger » comme alternative
« à éviter au début » ; elle devient un prototype, à côté des providers cloud, sans les remplacer.

### Pourquoi ce n'est pas l'usurpation écartée par l'ADR-011

L'ADR-011 a écarté le Token Exchange parce que « le back pourrait usurper n'importe qui ». Ici l'identité
empruntée est **unique et fixée dans l'IdP** (claim signé), elle n'existe que pendant un run que la personne
a **elle-même** délégué, et elle est bornée en durée comme en périmètre. Aucun jeton n'est émis au nom de
la personne : le principal délégué ne vit que le temps d'une requête, dans le contexte de sécurité, et ne
reprend aucun claim du jeton machine. Fuite du secret d'un runner : l'attaquant peut, au plus, réclamer les
tâches que CE propriétaire délègue à Claude Code et agir dans le périmètre ci-dessus pendant ces runs.

### Alternatives écartées

| Alternative | Raison du rejet |
|---|---|
| Jeton ou mot de passe de la personne dans le runner (ce que fait `taskforce-mcp` en dev) | Mot de passe sur disque, droits complets sans borne, pas révocable à part |
| Device flow OAuth | Suppose que le navigateur joigne Keycloak : faux en production |
| Token Exchange Keycloak | Déjà écarté par l'ADR-011 (usurpation générale) |
| API dédiée étroite, sans délégation | Duplique toute la surface de lecture, ne donne pas « les droits de la personne », à réécrire à chaque extension (inter-projets) |
| Workspace entier en écriture, borné par les seuls droits de la personne | Rayon d'action trop large face à une instruction glissée dans une issue : on commence par un projet |
| Webhook du backend vers le runner | Impossible derrière un NAT, et ouvrirait un port sur le poste |
| Managed Agents (exécution hébergée) | Reste la cible produit ; suppose une clé API |

### Preuve

`V88__delivery_runs_local_runner.sql` · `core/service/delivery/{ClaudeCodeProvider, LocalRunnerService,
RunnerIdentityResolver, DeliverySessionScope, RunnerTokenService, LocalRunnerSettings}.java` ·
`core/security/DeliverySessionFilter.java` · `core/api/{DeliveryRunnerController, RunnerAuthController}.java` ·
`shared/security/{SecurityConfig, PostAuthenticationFilter}.java` · `scripts/keycloak-runner.ps1` ·
`taskforce-mcp` 0.3.0 (`taskforce_get_issue`, `taskforce_add_comment`, en-tête de session) · `taskforce-runner/`.

**Vérifié le 20/09/2026 sur la stack dev** : suite backend complète verte (1264 tests, 0 échec), dont 131 tests ciblés sur le runner (dont 57 cas de périmètre et 15 du
filtre) et 59 tests du runner verts ; CI verte sur `dev` (tests backend, CodeQL, Semgrep) ; 34 sondes HTTP en direct, toutes conformes (proxy de jeton, runner
hors session, session en cours, session d'un run terminé) ; un run complet
`délégation -> claim -> worktree -> MCP en session déléguée -> commit -> push -> DONE -> « In review by AI »`,
et le chemin d'échec `FAILED -> « Blocked »`. Le commentaire posté par l'agent porte bien l'identité du
délégant ; les deux écritures hors périmètre tentées par l'agent ont reçu `403`.

**Non vérifié** : l'agent était un substitut (`test/fixtures/stub-agent`), le CLI Claude Code n'étant pas
installé sur le poste de test. Restent donc à éprouver avec le vrai CLI : les options de `claude -p`
(tirées de la documentation officielle), et l'ouverture de la PR par `gh` (le test poussait vers un dépôt
local sans GitHub).

### Conséquences

- **✅ Positif** : aucun changement front. Le picker et le suivi du run existaient ; `claude-code` y devient
  simplement disponible.
- **✅ Positif** : aucun contrôleur ni garde RBAC modifié. La délégation se joue avant eux, dans un seul
  filtre, couvert par des tests de périmètre exhaustifs.
- **⚠️ Limite** : le jeton remis au MCP de l'agent est le jeton machine du runner. Il ouvre aussi les
  endpoints machine (réclamer ou clore un run du même propriétaire). Durcissement prévu : un jeton de
  session **par run**, émis au claim, inutilisable hors de la session.
- **⚠️ Limite** : la durée d'un run est plafonnée par la durée de vie de ce jeton.
- **⚠️ Limite** : la révocation d'un runner n'est pas instantanée. Désactiver son client Keycloak arrête
  l'émission, mais un jeton déjà émis reste valide jusqu'à son expiration et peut encore réclamer un run du
  propriétaire. Le script donne donc au client sa **propre durée de vie de jeton, 60 min par défaut**
  (`-TokenLifespanMinutes`), au lieu d'hériter de celle du realm (480 min mesurées en dev). Coupure
  immédiate : `delivery.local-runner.enabled=false`.
- **✅ Résolu le 25/09/2026** : un run `QUEUED` sans runner à l'écoute attendait indéfiniment. Il est
  désormais clos en échec après `delivery.local-runner.claim-timeout-minutes` (15 min), avec un message qui
  dit quoi faire (voir la mise à jour ci-dessous). **⚠️ Reste** : pas d'annulation depuis l'interface.
- **⚠️ Limite** : un commentaire posté par l'agent apparaît au nom du délégant. Le modèle n'a pas d'auteur
  « agent ».
- **⚠️ Limite** : Cortex (`POST assistant`) est refusé en session, car il peut écrire une note de workspace.
- **📝 Hors périmètre** : gating par plan et métrage de la délégation ; écriture inter-projets ; script de
  provisionnement pour la production (les commandes `kcadm` sont celles du script dev).

### Mise à jour du 25/09/2026 : prod, file d'attente et marque

- **Constat en prod** : le flag était allumé par un override hors dépôt (test du 23/09). « Claude Code »
  était donc proposé à tous les utilisateurs, et une délégation sans runner restait `QUEUED` pour toujours
  (`DeliveryRunner.refresh` ne relisait que les runs `RUNNING`). Smart Assign ne recommande pas
  `claude-code` (ses préférences sont Cursor, Copilot, Claude API, toujours disponibles) : le piège suppose
  un choix manuel.
- **Expiration de file** : `DeliveryAgentProvider.claimTimeout()` (null pour un provider « push ») ;
  `DeliveryRunner.refresh` clôt un run « pull » encore en attente au-delà du délai, par une mise à jour
  **conditionnelle** (`DeliveryRunRepository.expireUnclaimed` : encore `QUEUED` et sans runner). Un claim
  concurrent gagne donc toujours, et rien n'écrase la copie réclamée. L'issue passe en « Blocked » avec le
  message « No runner picked this task up within 15 min… ». Un runner allumé avant toute relecture prend
  encore la tâche. La relecture vient du contrôleur (`DeliveryController.latestRun` et `listRuns`), qui
  relit désormais aussi les runs en attente : il ne relisait que les runs `RUNNING`, ce qui rendait la
  clôture inopérante malgré des tests unitaires verts.
- **Écarté** : une disponibilité par utilisateur (Claude Code proposé seulement quand son runner est en
  ligne). Plus juste, mais elle recouvre le chantier « Connect a runner » (libre-service), qui portera le
  statut du runner dans l'interface.
- **Flag durable** : `DELIVERY_LOCAL_RUNNER_ENABLED: ${DELIVERY_LOCAL_RUNNER_ENABLED:-false}` dans
  `docker-compose.prod.yml`, valeur posée dans `.env.prod` de la VM1. Elle survit aux rebuilds (l'auto-deploy
  passe `--env-file .env.prod`) ; l'override hors dépôt est supprimé.
- **Marque** : les conditions d'Anthropic, relues le 20/09, interdisent d'utiliser son logo sans
  permission et de faire de Claude Code un nom de fonctionnalité. Règle `NAME_ONLY` au seul point de rendu
  de chaque front (`frontend/components/ui/brand-logo.tsx`, `landing-page/src/components/site/BrandLogo.tsx`) :
  Anthropic est nommée en texte, avec un repli neutre à la place du logo. Sur le site, la fonctionnalité
  s'appelle « Local runner ».
- **Livré en prod le 25/09/2026 (v0.40.1, PR #321 puis #322)**, vérifié : conteneur backend recréé par
  l'auto-deploy, `DELIVERY_LOCAL_RUNNER_ENABLED=true` lu de `.env.prod`, override supprimé ensuite ; règle
  `NAME_ONLY` présente dans le bundle de l'app déployée ; aucun `/logos/anthropic` servi par le site. Suite
  backend complète verte (1311 tests), CodeQL sans alerte.

### Mise à jour du 28/09/2026 : identité de runner en libre-service

- **Décision** : l'identité machine d'un runner se crée désormais depuis l'application, par la personne
  elle-même (Réglages > Agents), au lieu du script d'admin. Endpoint utilisateur `GET/POST
  /api/delivery/runners` (`RunnerProvisioningController`), hors du préfixe machine, gaté par le même flag.
- **Ce qui ne change pas** : la forme de l'identité (client confidentiel en `client_credentials` seul, rôle
  `delivery-runner`, propriétaire signé `tf_runner_owner`) et les quatre preuves de `RunnerIdentityResolver`.
  Le service porte les étapes de `ops/kc-runner.sh` via le client admin Keycloak déjà présent.
- **Garde-fou** : le propriétaire est toujours l'e-mail de l'appelant authentifié, jamais une valeur venue
  du client ; une personne ne peut donc créer qu'un runner qui agit en son nom. Client `tf-runner-u<id>`,
  un par personne. Le secret est régénéré à chaque provisionnement et rendu une seule fois ; côté front, il
  ne passe jamais par l'état global.
- **Mode interactif** : un plugin Claude Code (`taskforce-plugin/`, commande `/taskforce`) branche le serveur
  MCP sur le jeton de l'utilisateur, sans en-tête de délégation : ce n'est pas une session déléguée, c'est la
  personne elle-même. v1 avec un jeton d'accès collé (court) ; un jeton personnel durable reste à faire.
- **Livré en prod le 28/09/2026 (v0.41.0, PR #323 puis #324)**, vérifié : backend reconstruit par l'auto-deploy
  (VM1 sur `365a8b86`), redémarré sain avec le flag, classe du contrôleur présente dans le jar, aucune erreur
  au démarrage ; app servie en 0.41.0 ; site passé au libre-service. Avant la release : bout-en-bout réel sur
  la stack dev contre Keycloak (identité créée, jeton machine émis pour elle par le relais, ancien secret
  refusé après régénération) ; suite backend complète (1317 tests) ; CodeQL sans alerte.

---

## ADR-014 - TaskForce 1.0 : projet open source lean et auto-hébergeable

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté (suivi : [[Plan_Release_Open_Source]])

### Contexte

La soutenance est passée. Constat du CEO : commercialement, la v1 ne résout presque aucun problème. Elle attaque la
gestion de projet, catégorie saturée où changer d'outil coûte cher, sans canal de distribution. La seule brique
vraiment distinctive est l'assignation intelligente.

Une recherche stratégique (04/10) a cherché un point d'entrée vendable tout de suite. Conclusion : la couche
« identité et autorité des agents » est déjà disputée par les éditeurs d'annuaires et les clouds, mauvais point
d'entrée pour une équipe de deux ; le choix d'un métier à vendre dépend d'un réseau commercial à cartographier. La
recherche est mise en pause.

Un audit complet du code (14/10, cinq passes en lecture seule) montre un cœur de gestion de projet qui fonctionne de
bout en bout, entouré de surfaces à moitié faites (agents factices, 138 tuiles d'intégration dont 3 réelles, webhooks
jamais envoyés), de failles à fermer, et d'une installation à neuf impossible.

### Décision

TaskForce est publié comme un projet open source fini, sur le modèle de Plane : on peut le forker, l'utiliser seul ou
en entreprise, et l'héberger chez soi avec son propre modèle d'IA ou son propre agent de code.

1. **Pas de fissure** : ce qui marche à moitié est fini ou supprimé, jamais laissé en l'état.
2. **IA locale d'abord** : Ollama et de petits modèles par défaut ; Groq ou tout fournisseur compatible OpenAI pour
   qui n'a pas la puissance (ADR-019).
3. **Agents** : Claude Code et Copilot, les deux que le CEO peut tester (ADR-018).
4. **Calendrier** : tout passe par `dev` et un test en Docker local. La production ne change que le jour des résultats
   du diplôme, avec le post LinkedIn ; d'ici là, le jury voit la version de la soutenance (v0.41.0). Le lancement est
   marqué 1.0.0.
5. **Signal de marché** : étoiles, forks, issues et demandes d'entreprises décideront d'en refaire un produit, avec la
   communauté.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Pivot commercial immédiat | Revenu possible | Aucun métier validé ni canal identifié ; des semaines d'analyse avant un premier client |
| Garder la v1 en l'état | Aucun travail | Fissures visibles, licence non libre, installation impossible : rien à montrer |
| Réécriture « v2 » | Architecture neuve | Des mois sans utilisateur, alors que le cœur actuel fonctionne |

### Conséquences

**Positives :** un produit montrable et utilisable par d'autres ; un vrai signal de marché ; moins de code à maintenir.

**Négatives / risques :** du travail sans revenu ; la prod doit rester stable jusqu'au jour J (déploiement automatique
depuis `main`) ; l'instance publique `taskforce-project.fr` devient gratuite et doit poser ses propres plafonds d'IA.

### Preuve

Plan et suivi item par item : [[Plan_Release_Open_Source]]. Branches `feature/lean-oss` du code et de la doc.

### Mise à jour du 16/10/2026 : fin des serveurs, cap sur le desktop

- **Contexte** : l'accès aux serveurs (VM1, VM2) prend fin après les résultats du diplôme. Il n'y aura donc plus
  d'instance hébergée : TaskForce se télécharge.
- **Décision** : la 1.0 se distribue en auto-hébergement Docker (lot 7), qui marche pour une équipe comme pour une
  personne seule, données sur sa machine. Ensuite, un essai de deux à trois jours d'un mode desktop (coque Tauri ou
  Electron, profil local sans Keycloak, base embarquée, Claude Code lancé directement par l'app) mesurera le poids et
  l'effort réels avant de s'y engager. À terme, le CEO veut une app desktop, sur le modèle de Claude Desktop.
- **Conséquence produit à trancher au moment de l'essai** : une app desktop est mono-utilisateur par défaut ; le côté
  équipe (membres, invitations, droits) ne revient qu'avec une synchronisation.
- **Release de sécurité anticipée** : les lots 0 et 1 partent en production dès qu'ils sont prêts, avant les résultats,
  car ils ne retirent rien de visible pour le jury et ferment des failles présentes en production. Les suppressions
  (lots 2 et suivants) restent pour le jour des résultats.
- **Veille** : l'outil open source le plus proche de l'idée desktop est Vibe Kanban (kanban qui lance Claude Code ou
  Codex dans des worktrees, distribué par `npx` et Tauri) ; aucun outil open source trouvé ne réunit gestion de
  projet, base de connaissance locale, Ollama et agents de code.
- **18/10/2026** : cap précisé par l'[[#ADR-021 - Application desktop locale, sur le modèle de Claude Desktop|ADR-021]] :
  la version desktop devient la cible, appelée à rester la seule ; le lot 7 (Docker multi-OS) est gelé au minimum.

---

## ADR-015 - Licence AGPL-3.0

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, appliqué

### Contexte

La licence maison « Fair Use License with Commercial Restrictions » interdisait l'usage commercial, l'hébergement
payant et l'intégration à un produit : exactement l'usage en entreprise que vise l'ADR-014. Ce n'était pas une licence
open source au sens de l'OSI, alors que le dépôt est public et que le site annonçait déjà « Open Source ».

### Décision

GNU Affero General Public License v3.0 (identifiant SPDX `AGPL-3.0-only`), texte copié tel quel depuis gnu.org, comme
Plane. Usage, modification et hébergement libres, y compris en entreprise ; quiconque fait tourner une version
modifiée pour des utilisateurs à travers un réseau doit leur en donner le code source. Le nom et le logo TaskForce
restent hors licence : une version modifiée distribuée prend un autre nom.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| MIT ou Apache-2.0 | Adoption maximale | Un concurrent peut en faire un service fermé sans rien rendre |
| Licence maison actuelle | Contrôle total | Pas open source ; une entreprise ne peut pas l'utiliser sereinement |
| BSL ou « fair source » | Protection commerciale | Pas open source ; contraire au but de l'ADR-014 |

### Conséquences

**Positives :** usage en entreprise autorisé sans négociation ; protection contre un fork fermé hébergé.

**Négatives / risques :** certaines entreprises interdisent l'AGPL en interne. Si une offre commerciale revient un
jour (double licence), il faudra l'accord des contributeurs : prévoir un accord de contribution avant d'accepter des
contributions externes importantes.

### Preuve

Commit `47c921b8` de `taskforce-fullstack` : `LICENSE` (texte officiel, 661 lignes), badge et section du README (et le
script qui régénère le badge), `pom.xml`, métadonnées OpenAPI, champ `license` des `package.json` et de leurs
lockfiles, manifeste du plugin Claude Code ; mentions « All rights reserved » retirées du site et des e-mails.

---

## ADR-016 - Retrait de la facturation et des limites de plan

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, mis en œuvre le 18/10/2026 (lot 2)

### Contexte

Facturation Stripe à quatre plans (en mode test), et limites codées en dur appliquées à tout compte sans abonnement :
2 workspaces par propriétaire, 250 issues par workspace, 5 collaborateurs sur un projet privé, 50 000 jetons d'IA par
mois, intégrations et MCP réservés au plan Business, analytics de capacité réservées, historique d'activité tronqué à
100 entrées. En auto-hébergement sans Stripe, tout le monde resterait bloqué au plan gratuit. Le profil de prod limite
en plus chaque compte à une requête d'IA par minute.

### Décision

Retirer la facturation (Stripe, pages de paiement, upgrades, badges, cadenas, module de contact commercial) et toutes
les limites de plan : chaque instance a toutes les fonctionnalités. Restent des protections d'exploitation réglables
par variables d'environnement, illimitées par défaut : quota mensuel de jetons d'IA par compte et limitation de débit
(`AiRateGuard`). L'instance publique fixe ses propres plafonds. Les tables de facturation restent en base (aucune
migration destructive dans cette release) ; le code reste dans l'historique git.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Facturation gardée mais désactivée | Offre cloud payante plus tard sans recoder | Code à maintenir et tester pour rien ; surface d'attaque |
| Plans gardés, limites réglables | Moins de changements | Une notion de « plan » sans facturation n'a pas de sens pour un utilisateur |

### Conséquences

**Positives :** produit complet pour tous ; moins de code dans le backend et le front.

**Négatives / risques :** l'instance publique doit poser des plafonds d'IA pour ne pas être abusée ; une offre payante
future repartira de l'historique git.

### Preuve

Lot 2 du [[Plan_Release_Open_Source]], PR [#341](https://github.com/taskforce-project/taskforce-fullstack/pull/341)
vers `dev` (18/10/2026) : limites retirées (`d30a51b1`), quota IA réglé par l'instance (`1d4ed5bf`), Stripe
et inscription payante retirés (`881cb666`), module commercial retiré (`1b1940f4`), front sans forfait
(`57a83a16`), configuration et docs (`6600906f`). Suite backend complète verte (1304 tests), front 864 tests.

Écart avec le texte de la décision : une migration a été nécessaire, non destructive. `users.plan_type` était
`NOT NULL` sans défaut depuis V6 ; une fois le champ sorti de l'entité, plus aucun compte ne se créait. **V90**
lui rend son défaut `'FREE'`. La purge RGPD efface toujours les identifiants Stripe hérités de la bêta hébergée.

---

## ADR-017 - Brain OS réduit à son cœur

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, mis en œuvre le 18/10/2026 (lot 3)

### Contexte

Brain OS (ADR-009) réunit un arbre de pages, un éditeur markdown (`#tags`, `[[wikilinks]]`), une recherche sémantique
(pgvector et embeddings `bge-m3` via Ollama), une ingestion automatique (cycles, issues, GitHub, Slack, Plane), un
graphe « cœur et galaxies », des gabarits de workspace (SaaS, e-commerce, marketplace, agentique) et l'étiquette
« Labs ». C'est la mémoire que lisent Cortex et les agents (outil MCP `brain_search`). Le graphe ignore le filtre par
tag, les notes initiales sont en français, et un workspace nommé `demo` reçoit un gabarit interne périmé.

### Décision

Garder le cœur : arbre de pages, éditeur, recherche, ingestion. Sans lui, Cortex perd sa recherche, les agents perdent
leur contexte, et les intégrations GitHub, Slack et Plane n'ont plus de destination. Couper le graphe, les galaxies,
les gabarits (un seul workspace vierge), le préremplissage `demo` et l'étiquette Labs. Notes initiales en anglais.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Tout supprimer | Plus léger | Emporte la recherche de Cortex, `brain_search` et trois intégrations |
| Tout garder | Aucun travail | Fonctions à moitié faites (filtre du graphe), étiquette expérimentale |

### Conséquences

**Positives :** ce qui distingue TaskForce de Plane reste (une base de connaissance que les agents lisent) ; moins de
surface à maintenir.

**Négatives / risques :** la recherche dépend d'un modèle d'embeddings (ADR-019) ; doublon partiel avec les pages de
projet, à consolider plus tard.

### Preuve

Lot 3 du [[Plan_Release_Open_Source]], branche `feature/lean-oss` (pas en prod) :

- `d68c71c1` : vue graphe, galaxies et en-tête « planète » retirés, avec `react-force-graph-2d` ; gabarits
  experts, préremplissage `demo` (`brain.demo-slugs`) et réamorçage retirés ; endpoints sans appelant retirés
  (lecture des pages à l'unité, liens créés à la main) ; `metadata.projects` retiré ; V92 convertit le type
  TEMPLATE en NOTE. Les liens viennent toujours des `#tags` et des `[[wikilinks]]`.
- `8327b697` : étiquette Labs retirée de l'app.
- `ddcd2b2f` : notes initiales (amorçage et ingestion) en anglais ; les relevés de cycle se raccrochent à la
  note « Done & shipped » du projet.
- `80b13ad8` : test d'ingestion aligné sur la fin de `metadata.projects`.

---

## ADR-018 - Agents de code : Claude Code et Copilot

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, à mettre en œuvre (lot 5) ; complète l'ADR-013

### Contexte

Cinq fournisseurs de délégation existent : `claude-code` (runner local de l'ADR-013, testé en réel), `claude-api` (un
appel au modèle, texte seul), `github-copilot` (en réalité un appel d'inférence GitHub Models, jamais testé), `cursor`
(API Background Agents, jamais testée, branche `main` écrite en dur) et `stub` (faux run avec un lien example.com,
visible en production).

Recherche du 14/10 sur les agents déclenchables par API : l'agent cloud de Copilot se voit assigner une issue via
l'API GitHub (`copilot-swe-agent[bot]`, préversion publique, jeton utilisateur, abonnement Copilot requis) ; Codex
cloud n'a pas d'API ; Devin exige un plan Teams ; Cursor est payant ; l'API de Jules est en alpha.

Vérification de la doc de Claude Code (14/10) : un produit tiers ne peut pas utiliser l'Agent SDK avec la connexion
d'un abonnement (page « Agent SDK overview », règle reprise par « Legal and compliance ») ; lancer le binaire `claude`
non modifié, connecté par la personne à son propre compte, reste admis.

### Décision

1. **Deux agents** : Claude Code (runner local) et Copilot, cette fois le vrai agent cloud : l'issue est assignée dans
   le dépôt lié avec le jeton GitHub du workspace, puis suivie par la PR qu'il ouvre. Le CEO peut tester les deux.
2. **Retirés** : `claude-api`, le faux `github-copilot`, `cursor` et `stub`.
3. **Le runner garde le CLI `claude`**, jamais l'Agent SDK avec un abonnement. Il gagne :
   - le suivi en direct (`--output-format stream-json --verbose` relayé au backend, chronologie dans l'app) ;
   - les validations : un hook `PermissionRequest` déclaré dans le fichier passé par `--settings` interroge TaskForce ;
     on autorise ou on refuse dans l'app, avec une notification ; sans réponse avant le délai, l'action est refusée ;
   - l'isolement des hooks du dépôt cloné : un dépôt piégé ne doit pas exécuter de commande sur la machine.
4. **Mode interactif** (plugin `/taskforce`) : jeton personnel durable et révocable, serveur MCP servi par l'instance en
   HTTP.
5. Les autres clients MCP (Copilot dans VS Code, Cursor, Codex CLI, Gemini CLI) se branchent sur ce même serveur, sans
   garantie : le README dit « testé avec Claude Code ».

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Garder les cinq fournisseurs | Liste impressionnante | Trois non testés et un factice : contraire à la règle « pas de fissure » |
| Runner sur l'Agent SDK | API plus confortable (`canUseTool`) | Interdit avec un abonnement ; exigerait une clé d'API payante |
| `--permission-prompt-tool` (outil MCP) | Tout reste dans le serveur MCP | Contrat d'entrée et de sortie non documenté officiellement |

### Conséquences

**Positives :** chaque agent affiché fonctionne vraiment ; l'humain garde la main sur les actions sensibles.

**Négatives / risques :** Copilot exige un abonnement et repose sur une API en préversion ; le délai maximal d'un hook
n'est pas documenté (à tester) ; la clause des conditions d'Anthropic sur « faire tourner Claude Code dans un
produit » reste à confirmer par écrit.

### Preuve

- Lot 3 (18/10/2026, `56ca4e0c`) : fournisseurs `stub`, `claude-api`, `github-copilot` (appel à GitHub Models)
  et `cursor` retirés, avec leurs clés d'API ; V91 supprime les clés stockées et clôt les runs bloqués. Seul
  `claude-code` reste.
- Le reste (validations dans l'app, vrai Copilot) : lot 5 du [[Plan_Release_Open_Source]].

---

## ADR-019 - Fournisseur d'IA générique, Ollama par défaut

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, mis en œuvre le 18/10/2026 (lot 4)

### Contexte

Le backend appelle le service Python `ai-service` (FastAPI, proxy mince) : chat vers Groq si `GROQ_API_KEY` est
posée, sinon vers Ollama ; embeddings toujours via Ollama (`bge-m3`, 1024 dimensions imposées par la migration V59),
avec un repli de mauvaise qualité. Les variables `GROQ_*` acceptent en fait tout fournisseur compatible OpenAI, mais
pas pour les embeddings. Plusieurs appels au modèle ont lieu dans une transaction de base : un modèle local lent peut
épuiser le pool de connexions. Le service n'a ni authentification ni tests. L'ADR-004 (« Groq appelé directement en
Java, pas de microservice Python ») ne décrit plus le code.

### Décision

1. Configuration générique compatible OpenAI pour le chat et les embeddings (URL de base, clé, modèles) ; les
   variables `GROQ_*` restent comme alias pour ne pas casser la prod.
2. Ollama par défaut avec de petits modèles qui gèrent les outils, embeddings `bge-m3` ; le suffixe `/no_think` ne
   s'applique qu'à Qwen3.
3. Les appels au modèle sortent des transactions de base.
4. Sans fournisseur configuré : échec immédiat et état « IA non configurée » dans l'interface, au lieu d'attendre un
   délai à chaque appel.
5. `ai-service` reste en Python, joignable seulement sur le réseau interne, protégé par un secret partagé.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Porter le service en Java (direction de l'ADR-004) | Un service de moins | Réécriture et risque avant le jour J |
| Rester sur Groq | Rapide | Contraire au positionnement local ; clé payante |

### Conséquences

**Positives :** l'IA tourne sur la machine de l'utilisateur ; un seul format de configuration couvre Ollama, Groq,
LM Studio, OpenRouter ; un modèle lent ne bloque plus l'application.

**Négatives / risques :** la qualité dépend du modèle choisi ; les petits modèles locaux gèrent moins bien les outils.

### Preuve

Lot 4 du [[Plan_Release_Open_Source]], branche `feature/lean-oss` (pas en prod) :

1. `ai-service/app/config.py` : `AI_BASE_URL`, `AI_API_KEY`, `AI_MODEL`, `AI_MODEL_FAST`, `AI_EMBED_*`, `AI_TIMEOUT`,
   `AI_PROVIDER=none` ; `GROQ_*` et `OLLAMA_*` en alias (testé par `tests/test_config.py`).
2. Ollama sur la machine hôte par défaut, `qwen3:8b` pour les deux tiers et `bge-m3` ; `/no_think` seulement pour
   Qwen3 (`with_no_think`, testé).
3. Plus aucun appel au modèle sous transaction : `IssueAiService`, `AiConversationService`, `SmartAssignService`,
   `BrainSearchService` lisent dans une transaction courte (`TransactionTemplate`), appellent le modèle, puis écrivent.
4. `AiStatusService` lit `GET /v1/status` (30 s) : sans IA, `AiGatewayClient` échoue tout de suite ; l'interface
   lit `GET /api/ai/status` et affiche « AI is not configured » dans Cortex.
5. Secret partagé obligatoire sur toutes les routes `/v1` (`ai-service/app/security.py`), service sans port publié,
   60 tests pytest et workflow `ai-service-tests.yml`.

Écart assumé : le repli « lexical » des embeddings est supprimé plutôt que gardé. Ses vecteurs de hachage étaient
rangés avec les vrais et rendaient les similarités incomparables ; la recherche passe en plein texte sans modèle
(V94 lie chaque vecteur à son modèle).

---

## ADR-020 - Connexion générale : MCP et webhooks sortants

**Date** : 14/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté, à mettre en œuvre (lot 6)

### Contexte

Le catalogue compte 138 tuiles : 3 intégrations réelles (GitHub, Slack, Plane), 129 tuiles qui demandent seulement
l'URL d'un serveur MCP (dont 25 avec une URL officielle préremplie) et 6 « bientôt ». Tout le MCP est réservé au plan
Business sans que l'interface le dise, et Cortex n'a pas accès aux outils MCP par défaut. Les webhooks sortants ont un
écran de gestion, mais rien n'est jamais envoyé ni signé.

### Décision

Deux méthodes générales plutôt qu'une tuile par outil :

1. **MCP pour les actions** : « connecter n'importe quel serveur MCP » (URL, OAuth en un clic ou en-tête), avec les 25
   préréglages officiels. Les 104 autres tuiles disparaissent. Les outils sont proposés à Cortex ; les écritures
   demandent une confirmation et sont réservées aux propriétaires et administrateurs.
2. **Webhooks sortants pour les événements** : issues et commentaires, signés HMAC, avec nouvelles tentatives. Ils
   branchent n8n, Zapier, Make ou un script maison.

GitHub, Slack et Plane restent des intégrations natives.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Garder les 138 tuiles | Catalogue impressionnant | 104 tuiles ne sont qu'un champ URL : promesse trompeuse |
| Supprimer les webhooks | Moins de code | Plus aucun moyen de pousser les événements vers un outil d'automatisation |

### Conséquences

**Positives :** deux méthodes qui couvrent tout l'écosystème au lieu d'un catalogue à maintenir ; l'interface ne
promet plus que ce qui marche.

**Négatives / risques :** un serveur MCP arbitraire est une surface d'attaque (garde anti-SSRF du lot 1, écritures
réservées) ; les webhooks demandent une file de nouvelles tentatives.

### Preuve

À venir (lot 6 du [[Plan_Release_Open_Source]]).

---

## ADR-021 - Application desktop locale, sur le modèle de Claude Desktop

**Date** : 18/10/2026 | **Décideur** : Pierre MICHEL | **Statut** : ✅ Accepté (cap) ; architecture à confirmer par l'essai OSS-D.1

### Contexte

Le 16/10, la fin des serveurs après les résultats du diplôme a fait de TaskForce un logiciel à télécharger : 1.0 en
auto-hébergement Docker, puis un essai de mode desktop (mise à jour du 16/10 de l'ADR-014). Le 18/10, le CEO va plus
loin : on prépare directement la version desktop, appelée à devenir la seule. L'app tourne sur le PC de
l'utilisateur, Brain OS et toutes les données y restent, l'IA dépend de sa machine, sur le modèle de Claude Desktop. Le
sort de la webapp sera tranché après la spécification.

La pile actuelle est une pile serveur : Keycloak pour l'identité (le mot de passe et le nom des utilisateurs n'existent
que chez lui), PostgreSQL avec pgvector (86 migrations, requêtes natives propres à Postgres), MinIO pour les fichiers,
un SMTP, un service Python devant les modèles et le serveur Next.js. RabbitMQ et Redis sont déjà facultatifs. Le
détail de ce que chaque brique devient est dans la [[Specification_App_Desktop]] (inventaire du code du 18/10).

### Décision

1. TaskForce devient une application desktop (Windows, macOS, Linux) : mono-utilisateur, sans compte, données sur la
   machine, utilisable hors ligne hors IA distante. IA locale par Ollama, ou par une clé d'API compatible OpenAI
   fournie par l'utilisateur.
2. Une seule base de code, deux profils : `desktop` (local) et `server` (l'édition d'équipe auto-hébergée actuelle).
   Le profil `desktop` remplace Keycloak, MinIO, le SMTP et le service Python par des équivalents locaux ; il se
   passe de RabbitMQ et de Redis, déjà facultatifs.
3. Architecture visée, à valider par l'essai : coque Electron, front Next.js existant servi en local, backend Spring
   Boot existant lancé par la coque avec un JRE embarqué, PostgreSQL embarqué (pgvector compris : quatre migrations
   en dépendent). Claude Code est lancé directement par l'app : plus de relais Keycloak ni de modèle « pull ».
4. La webapp n'est plus développée au-delà des lots en cours tant que la spécification n'a pas tranché son rôle. Son
   rôle candidat : combler les trous du desktop (travail en équipe, accès à distance, intégrations entrantes).
5. Le lot 7 (installation Docker multi-OS) est gelé au minimum : l'effort d'empaquetage va au desktop.

### Alternatives considérées

| Option | Avantages | Inconvénients |
| ------ | --------- | ------------- |
| Electron et pile actuelle embarquée (retenu) | Réutilise presque tout le code ; Chromium identique sur les trois OS ; Node inclus pour le serveur Next ; outillage mûr (paquets, mises à jour) ; Claude Desktop et VS Code sont faits ainsi | App lourde (environ 300 à 400 Mo installée, à mesurer) ; démarrage de quelques secondes (JVM) |
| Tauri et mêmes processus | Coque d'environ 10 Mo | WebView différente selon l'OS (WebKit sur macOS et Linux) ; Node à embarquer quand même pour Next ; glue en Rust à écrire |
| Réécriture local-first (TypeScript, SQLite) | App légère et simple | Réécrire un backend d'environ 520 classes Java et 86 migrations : hors de portée |
| Rester en web et Docker | Existe déjà | Docker Desktop requis, ce n'est pas une app grand public ; pas l'expérience « comme Claude Desktop » |

### Conséquences

**Positives :** plus d'hébergement ni de serveur à payer ; données privées par construction ; l'agent de code tourne à
côté du dépôt de l'utilisateur, sans runner ni jeton de service ; une seule interface à maintenir.

**Négatives / risques :** plus de collaboration à plusieurs tant qu'il n'y a pas de serveur d'équipe ou de
synchronisation ; plus d'intégrations entrantes (webhooks, événements) faute d'adresse publique ; la qualité de l'IA
dépend du matériel ; signature de code (certificat Windows, compte Apple Developer) et mises à jour à distribuer ; app
plus lourde qu'une app web.

### Preuve

Spécification : [[Specification_App_Desktop]]. Essai OSS-D.1 et ses critères chiffrés dans le
[[Plan_Release_Open_Source]].

---

> 🔗 Voir aussi : [[Architecture_C4]] · [[CdCT_v2]] · [[CdCF_v2]] · [[Table_Reconciliation]] ·
> [[Diagramme_Classes_UML]] · [[Diagrammes_Sequence_UML]] · [[Note_Cadrage]].
>
> Ce journal est la source de vérité pour les décisions non évidentes. Toute nouvelle décision
> structurante (migration Flyway majeure, changement de stack, nouveau pattern) doit être ajoutée ici.
