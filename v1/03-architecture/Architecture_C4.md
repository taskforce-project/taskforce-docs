---
id: architecture-c4
title: Architecture logicielle — modèle C4
doc_type: conception
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [c4, architecture, contexte, conteneurs, composants, conception, memoire, rncp]
---

# 🏛️ Architecture logicielle — modèle C4

> **But** : formaliser l'architecture de TaskForce selon le **modèle C4** (Simon Brown) — trois niveaux
> de zoom : **Contexte** → **Conteneurs** → **Composants**. Complète [[Architecture]] (vue détaillée
> textuelle) en offrant la lecture normalisée attendue au jury.
>
> **Source de vérité** : [[Architecture]] (topologie, ports, stack vérifiés), `backend/tf-api/ARCHITECTURE.md`
> (règle de dépendance), fichiers Compose. **Rien n'est inventé** ; les éléments non déployés/vestigiaux
> sont annotés comme tels.

---

## Niveau 1 — Contexte système

Qui utilise TaskForce et avec quels systèmes externes il dialogue.

```mermaid
flowchart TB
    subgraph EXT_ACTORS[" "]
        direction LR
        MEMBER["🧑‍💻 Collaborateur<br/><i>membre d'un workspace</i>"]
        MANAGER["🧑‍💼 Gestionnaire / Propriétaire<br/><i>gère équipes, projets, abonnement</i>"]
    end

    TF{{"<b>TaskForce</b><br/>SaaS de gestion de projet<br/>multi-tenant + IA"}}

    KC["🔐 Keycloak<br/><i>identité / OIDC / JWT</i>"]
    STRIPE["💳 Stripe<br/><i>facturation / abonnements</i>"]
    OLLAMA["🤖 Ollama Qwen3<br/><i>modèle auto-hébergé, hors de tout tiers</i>"]
    OAUTH["🔗 GitHub / Slack<br/><i>OAuth intégrations</i>"]
    SMTP["✉️ SMTP / Mailtrap<br/><i>e-mails OTP & notifications</i>"]

    MEMBER -->|HTTPS / WebSocket| TF
    MANAGER -->|HTTPS / WebSocket| TF
    TF -->|OIDC, émission JWT| KC
    TF -->|paiement, webhooks| STRIPE
    TF -->|inférence locale, via ai-service| OLLAMA
    TF -->|OAuth, webhooks| OAUTH
    TF -->|envoi e-mail| SMTP
```

---

## Niveau 2 — Conteneurs

Les applications déployables et briques d'infrastructure (ports **dev**).

```mermaid
flowchart TB
    USER["🧑 Navigateur"]

    subgraph TF["TaskForce (monorepo)"]
        LAND["🪧 Landing<br/>Astro 5 · :4321"]
        FRONT["🖥️ Frontend app<br/>Next.js 16 · React 19 · :3000"]
        BACK["⚙️ Backend API<br/>Spring Boot 4 · Java 21 · :8080<br/>core + modules + shared"]
        AISVC["🐍 ai-service<br/>FastAPI · :8000<br/><i>⚠️ vestigial (stub, cf. DT-010)</i>"]
    end

    PG[("🐘 PostgreSQL 18<br/>+ pgvector · :5432")]
    KC["🔐 Keycloak · :8180"]
    MINIO[("🗄️ MinIO S3<br/>:9000")]
    RMQ["🐇 RabbitMQ<br/>relais STOMP · :61613"]
    NGINX["🌐 Nginx<br/><i>prod uniquement</i>"]

    STRIPE["💳 Stripe"]:::ext
    OLLAMA["🤖 Ollama Qwen3 (local)"]:::ext
    OAUTH["🔗 GitHub/Slack"]:::ext
    SMTP["✉️ SMTP"]:::ext

    USER -->|HTTPS| LAND
    USER -->|HTTPS| FRONT
    USER -.->|prod : reverse proxy| NGINX
    FRONT -->|REST /api/** + Bearer JWT| BACK
    FRONT <-->|WS/STOMP SockJS| BACK
    BACK -->|JDBC| PG
    BACK -->|OIDC / admin| KC
    FRONT -->|OIDC login| KC
    BACK -->|objets S3| MINIO
    BACK <-->|STOMP| RMQ
    BACK -->|via ai-service| OLLAMA
    BACK -->|paiement/webhooks| STRIPE
    BACK -->|OAuth| OAUTH
    BACK -->|e-mail| SMTP

    classDef ext fill:#eee,stroke:#999,stroke-dasharray:3 3;
```

> ⚠️ **Cette note affirmait l'inverse de la réalité. Corrigée le 23/07/2026.**
>
> Elle décrivait `ai-service` comme « vestigial, non utilisé en production », l'IA tournant « en Java
> via `GroqService` appelant directement Groq ». **Les deux propositions sont fausses aujourd'hui**,
> et la seconde l'est doublement : `GroqService` **n'existe plus dans le code**.
>
> Le chemin réel est l'inverse : `SmartAssignService` appelle l'interface `LlmClient`, dont l'unique
> implémentation `AiGatewayClient` s'adresse à la **passerelle Python `ai-service`**, elle-même
> devant un modèle **Qwen3 exécuté localement par Ollama**. `ai-service` est un service déclaré de
> la composition, dont le backend dépend explicitement (`AI_SERVICE_URL`).
>
> Groq a été retiré le 16/07 (`TF-AI-GROQ-CLEANUP`) : il était bloqué par le réseau de l'école (403),
> et son implémentation n'enregistrait pas la consommation de jetons, ce qui désarmait silencieusement
> la facturation de l'IA. Conséquence pour la conformité, et c'est l'argument le plus fort du
> registre des traitements : **aucun contenu de travail ne quitte l'infrastructure**.

---

## Niveau 3 — Composants du backend

Zoom dans le conteneur **Backend API**. Règle de dépendance **stricte** : `shared ← core ← modules`
(preuve : `backend/tf-api/ARCHITECTURE.md`).

```mermaid
flowchart TB
    subgraph MODULES["📦 modules/ (features bornées)"]
        CHAT["chat<br/>canaux + WebSocket"]
        GED["ged<br/>pièces jointes + MinIO"]
        SALES["sales<br/>leads entreprise"]
    end

    subgraph CORE["🎯 core/ (domaine principal)"]
        API["api/<br/>contrôleurs REST"]
        SVC["service/<br/>logique métier<br/>(SmartAssign, Redistribution,<br/>Auth, Gdpr, Stripe…)"]
        REPO["repository/<br/>Spring Data JPA"]
        MODEL["model/<br/>entités JPA + enums"]
        API --> SVC --> REPO --> MODEL
    end

    subgraph SHARED["🧰 shared/ (transverse, sans métier)"]
        SEC["security/<br/>SecurityConfig, JwtDecoder"]
        CFG["config/<br/>Cors, Keycloak, Stripe, LlmConfig,<br/>WebSocket, Otp, Minio…"]
        DTO["dto/<br/>ApiResponse&lt;T&gt;"]
        EXC["exception/<br/>GlobalExceptionHandler"]
        AUD["audit/<br/>AuditableEntity"]
    end

    MODULES -->|dépend de| CORE
    CORE -->|dépend de| SHARED
    MODULES -.->|dépend de| SHARED

    PG[("🐘 PostgreSQL")]
    REPO --> PG
```

**Cycle d'une requête** (preuve [[Architecture]] §4) :
`SecurityConfig` (chaîne publique + chaîne JWT) → contrôleur `@RequestMapping` → service
(autorisation : appelant = `WorkspaceMember`/`ProjectMember`, rôle via `WorkspaceRole`/`ProjectRole`)
→ repository → PostgreSQL. Erreurs normalisées par `GlobalExceptionHandler` ; réponse encapsulée dans
`ApiResponse<T> = { success, data, message, statusCode }`.

---

## Traçabilité

| Niveau | Éléments | Preuve |
|---|---|---|
| Contexte | 2 acteurs + 5 systèmes externes | [[Architecture]] §5, [[Diagramme_Cas_Usage_UML]] |
| Conteneurs | 4 apps + 5 infra + Nginx prod | [[Architecture]] §1–2, fichiers Compose |
| Composants | `core`/`modules`/`shared` + règle de dépendance | `backend/tf-api/ARCHITECTURE.md` |
| ai-service vestigial | stub SHA256, IA en Java | [[Architecture]] §5, DT-010 |

> 🔗 Voir aussi : [[Architecture]] (détail textuel) · [[Diagramme_Classes_UML]] ·
> [[Diagrammes_Sequence_UML]] · [[Roadmap_Documentation|plan de production doc]].
