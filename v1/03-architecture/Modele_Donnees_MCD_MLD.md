---
id: modele-donnees
title: Modèle de données — MCD / MLD (MERISE)
doc_type: reference
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [architecture, donnees, mcd, mld, merise, erd, postgresql, flyway, e8]
related:
  - "./Architecture.md"
  - "./Modules.md"
  - "../16-memoire-rncp/README.md"
---

# 🗄️ Modèle de données — MCD / MLD (MERISE)

> **Livrable E8** (dossier de conception, compétences **C8/C9**). Modèle **entité-association** de la base
> TaskForce. **Source de vérité** : le schéma **réel** de PostgreSQL, obtenu par introspection de
> `information_schema` sur la base après application des **migrations Flyway V1→V55** (`ddl-auto=validate`
> confirme l'alignement entités JPA ↔ schéma). **Aucune table/relation inventée** : tout provient du schéma exécuté.

## 1. Périmètre & méthode

- **50 tables** métier (hors `flyway_schema_history`), **483 colonnes**, **94 clés étrangères**.
- **MERISE** : le **MCD** (conceptuel, §3) décrit les entités et associations ; le **MLD** (logique, §4)
  est le schéma relationnel réel (tables, colonnes, PK/FK). Le **MPD** (physique) = PostgreSQL 18 + pgvector.
- Diagrammes en **Mermaid** (rendus nativement dans Obsidian/GitHub) générés depuis le schéma réel.

### Légende
| Notation | Sens |
| --- | --- |
| `PK` | Clé primaire |
| `FK` | Clé étrangère |
| `X ||--o{ Y : "col"` | **1–N** : une ligne de `X` référencée par N lignes de `Y` via `Y.col` |
| `enum` (dans les diagrammes) | Type PostgreSQL `USER-DEFINED` = soit un **enum** métier (`status`, `priority`, `role`, `category`, `action`, `relation_type`, `plan_status`), soit le type **`vector(384)`** (pgvector) pour les colonnes **`embedding`** |
| `jsonb` | Données semi-structurées (métadonnées, skills, features IA) |

> **Choix de présentation** : pour la lisibilité, chaque diagramme n'affiche que les relations **internes
> au domaine**. Deux clés étrangères sont **transversales et omniprésentes** (non redessinées partout) :
> `workspace_id → workspaces.id` (isolation **multi-tenant**) et `*_id → users.id` (auteur/acteur/assigné).

## 2. Conventions transverses (toutes tables)

- **Isolation multi-tenant** : la quasi-totalité des tables porte `workspace_id` → chaque donnée appartient
  à un workspace (frontière de sécurité, cf. `WorkspaceAccessInterceptor`).
- **Audit applicatif** : horodatage `created_at`/`updated_at` (et parfois `created_by`/`updated_by`)
  sur la majorité des entités — **déclaré directement dans l'entité (27 entités)** ou via la superclasse
  `AuditableEntity` (**4 entités** : `BrainWorkspace`, `KnowledgeNode`, `MemberLeave`, `WorkspaceInvitation`).
  **7 tables de jointure/compteurs n'en ont pas** (`workspace_members`, `team_members`, `project_members`,
  `cycle_issues`, `integrations`, `issue_github_links`, `issue_sequence_counters`). Traçabilité des actions
  sensibles = table dédiée `audit_logs` (cf. `07-securite/Sécurité.md` A09).
- **Identité** : `bigint id` auto-incrément en PK ; `uuid` en plus sur certaines entités exposées
  (`workspaces`, `knowledge_nodes`) ou en PK pour les jetons/événements (`refresh_tokens`, `otp_verification`,
  `subscription_history`, `enterprise_inquiries`).
- **RGPD** : le droit à l'effacement est une **anonymisation** (pas de hard-delete) ; `audit_logs.actor_user_id`
  est `ON DELETE SET NULL` pour survivre à l'anonymisation (cf. `GdprService`).
- **IA / sémantique** : colonnes `embedding vector(384)` (pgvector, index HNSW) sur `knowledge_nodes`,
  `ai_documents`, `member_skill_profiles` → recherche de similarité (Smart Assign / Brain OS).

## 3. MCD — vue conceptuelle (domaines)

Le modèle s'organise en **7 domaines** alignés sur les modules du code (`shared ← core ← modules`) :

| Domaine | Entités clés | Rôle |
| --- | --- | --- |
| **IAM & Workspace** | `users`, `workspaces`, `workspace_members`, `teams`, `companies` | Identité, tenants, appartenance, équipes |
| **Projets & Issues** | `projects`, `issues`, `issue_statuses/types/labels`, `cycles`, `pages` | Cœur gestion de projet |
| **IA / Smart Assign / Brain OS** | `member_skill_profiles`, `assignment_events`, `ai_runs`, `knowledge_nodes/edges` | Répartition intelligente + graphe de connaissance |
| **Auth & Sécurité** | `refresh_tokens`, `otp_verification`, `audit_logs` | Sessions, OTP, journal d'audit |
| **Facturation** | `subscriptions`, `subscription_history` | Stripe, plans, historique |
| **Intégrations & Comms** | `integrations`, `webhooks`, `channels`, `notifications` | GitHub/Slack, chat, notifications |
| **GED & Sales** | `attachments`, `enterprise_inquiries` | Pièces jointes (MinIO), leads |

**Entités-pivots** : `workspaces` (racine du tenant) et `users` (acteur universel) — quasiment toutes les
associations pointent vers l'une ou l'autre.

## 4. MLD — schéma relationnel réel (par domaine)
<!-- Diagrammes générés par introspection du schéma réel (information_schema) — ne pas éditer à la main :
     régénérer si le schéma change (nouvelle migration Flyway). -->

### 4.1 IAM & Workspace

```mermaid
erDiagram
  companies {
    bigint id PK
    varchar name
    varchar email
    varchar phone
    text address
  }
  users {
    bigint id PK
    varchar keycloak_id
    varchar email
    bigint company_id FK
    boolean is_active
    varchar plan_type
    enum plan_status
    varchar stripe_customer_id
    varchar display_name
    varchar avatar_url
  }
  workspaces {
    bigint id PK
    uuid uuid
    varchar name
    varchar slug
    varchar description
    bigint owner_id FK
  }
  workspace_members {
    bigint id PK
    bigint workspace_id FK
    bigint user_id FK
    varchar role
    bigint invited_by FK
    timestamp joined_at
  }
  workspace_invitations {
    bigint id PK
    bigint workspace_id FK
    bigint invited_by FK
    varchar email
    varchar role
    varchar token
    varchar status
    timestamp expires_at
  }
  teams {
    bigint id PK
    bigint workspace_id FK
    bigint created_by FK
    varchar name
    varchar emoji
    varchar color
  }
  team_members {
    bigint id PK
    bigint team_id FK
    bigint user_id FK
    varchar role
  }
  member_leaves {
    bigint id PK
    bigint workspace_id FK
    bigint user_id FK
    varchar type
    date start_date
    date end_date
  }
  companies ||--o{ users : "company_id"
  users ||--o{ workspaces : "owner_id"
  workspaces ||--o{ workspace_members : "workspace_id"
  users ||--o{ workspace_members : "user_id"
  workspaces ||--o{ workspace_invitations : "workspace_id"
  workspaces ||--o{ teams : "workspace_id"
  teams ||--o{ team_members : "team_id"
  users ||--o{ team_members : "user_id"
  workspaces ||--o{ member_leaves : "workspace_id"
  users ||--o{ member_leaves : "user_id"
```

**Règles de gestion** : `workspaces.slug` unique (routing) ; `workspace_members(workspace_id,user_id)`
unique (un membre = un rôle OWNER/ADMIN/MEMBER) ; invitations par **token** avec expiration ; les `teams`
regroupent des membres et se relient aux projets (`project_teams`, §4.2).

### 4.2 Projets & Issues (cœur)

```mermaid
erDiagram
  projects {
    bigint id PK
    bigint workspace_id FK
    varchar name
    varchar identifier
    enum status
    boolean is_public
    bigint created_by FK
    varchar color
    boolean growth_mode
  }
  project_members {
    bigint id PK
    bigint project_id FK
    bigint user_id FK
    enum role
    bigint added_by FK
  }
  project_teams {
    bigint id PK
    bigint project_id FK
    bigint team_id FK
  }
  project_labels {
    bigint id PK
    bigint project_id FK
    varchar name
    varchar color
  }
  project_favorites {
    bigint id PK
    bigint user_id FK
    bigint project_id FK
  }
  cycles {
    bigint id PK
    bigint project_id FK
    varchar name
    date start_date
    date end_date
    enum status
  }
  cycle_issues {
    bigint id PK
    bigint cycle_id FK
    bigint issue_id FK
  }
  pages {
    bigint id PK
    bigint project_id FK
    bigint created_by FK
    varchar title
    text content
  }
  issues {
    bigint id PK
    bigint project_id FK
    integer sequence_number
    varchar title
    text description
    enum priority
    bigint status_id FK
    bigint type_id FK
    bigint assignee_id FK
    bigint reporter_id FK
    bigint parent_id FK
    date due_date
    integer story_points
    timestamp completed_at
  }
  issue_statuses {
    bigint id PK
    bigint project_id FK
    varchar name
    enum category
    smallint position
    boolean is_default
  }
  issue_types {
    bigint id PK
    bigint project_id FK
    varchar name
    boolean is_default
  }
  issue_label_assignments {
    bigint issue_id PK
    bigint label_id PK
  }
  issue_comments {
    bigint id PK
    bigint issue_id FK
    bigint author_id FK
    text content
  }
  issue_activity {
    bigint id PK
    bigint issue_id FK
    bigint actor_id FK
    enum action
    varchar old_value
    varchar new_value
  }
  issue_checklist_items {
    bigint id PK
    bigint issue_id FK
    varchar content
    boolean is_done
    integer position
  }
  issue_relations {
    bigint id PK
    bigint source_id FK
    bigint target_id FK
    enum relation_type
    bigint created_by FK
  }
  issue_worklogs {
    bigint id PK
    bigint issue_id FK
    bigint user_id FK
    integer minutes
    date logged_at
  }
  issue_sequence_counters {
    bigint project_id PK
    integer last_number
  }
  issue_github_links {
    bigint id PK
    bigint issue_id FK
    varchar link_type
    varchar repo_full_name
    integer pr_number
    bigint linked_by FK
  }
  projects ||--o{ project_members : "project_id"
  projects ||--o{ project_teams : "project_id"
  projects ||--o{ project_labels : "project_id"
  projects ||--o{ project_favorites : "project_id"
  projects ||--o{ cycles : "project_id"
  cycles ||--o{ cycle_issues : "cycle_id"
  issues ||--o{ cycle_issues : "issue_id"
  projects ||--o{ pages : "project_id"
  projects ||--o{ issues : "project_id"
  issue_statuses ||--o{ issues : "status_id"
  issue_types ||--o{ issues : "type_id"
  projects ||--o{ issue_statuses : "project_id"
  projects ||--o{ issue_types : "project_id"
  projects ||--o{ issue_sequence_counters : "project_id"
  issues ||--o{ issue_comments : "issue_id"
  issues ||--o{ issue_activity : "issue_id"
  issues ||--o{ issue_checklist_items : "issue_id"
  issues ||--o{ issue_worklogs : "issue_id"
  issues ||--o{ issue_github_links : "issue_id"
  issues ||--o{ issue_label_assignments : "issue_id"
  project_labels ||--o{ issue_label_assignments : "label_id"
  issues ||--o{ issue_relations : "source_id"
  issues ||--o{ issue_relations : "target_id"
```

**Règles de gestion** :
- **Numérotation par projet** : `issues.sequence_number` + table `issue_sequence_counters(project_id → last_number)`
  → identifiants stables type `WEB-1`, `API-2` (incrément atomique par projet).
- **Statuts/types propres au projet** : `issue_statuses`/`issue_types` sont **par projet** (colonnes/board
  configurables) ; `issue_statuses.category` (enum : BACKLOG/UNSTARTED/STARTED/COMPLETED/CANCELLED) sert aux
  filtres et à la logique (charge ouverte, redistribution).
- **Hiérarchie & liens** : `issues.parent_id` (auto-référence = sous-tâches) ; `issue_relations`
  (`source_id`/`target_id` + `relation_type` : BLOCKS/RELATES_TO…) = graphe entre issues.
- **Labels** : association N-N `issue_label_assignments(issue_id, label_id)` (PK composite).
- **Cycles** (sprints) : N-N `cycle_issues` ; **worklogs** = temps saisi (alimente le suivi + Smart Assign).

### 4.3 IA / Smart Assign / Brain OS

```mermaid
erDiagram
  member_skill_profiles {
    bigint id PK
    bigint workspace_id FK
    bigint user_id FK
    text profile_text
    jsonb skills_json
    integer capacity_hours_per_week
    varchar seniority
    boolean growth_enabled
    jsonb growth_target_skills
    enum embedding
  }
  assignment_events {
    bigint id PK
    bigint workspace_id FK
    bigint issue_id FK
    bigint assignee_user_id FK
    bigint assigned_by_user_id FK
    varchar decision_source
    boolean accepted
    boolean resolved_successfully
    jsonb features_json
  }
  ai_runs {
    bigint id PK
    bigint workspace_id FK
    varchar feature_name
    varchar provider
    varchar model_name
    integer latency_ms
    varchar status
    boolean fallback_used
  }
  ai_documents {
    bigint id PK
    bigint workspace_id FK
    varchar source_type
    bigint source_id
    text content
    enum embedding
  }
  ai_insight_snapshots {
    bigint id PK
    bigint workspace_id FK
    date snapshot_date
    text summary_text
    jsonb exceptions_json
  }
  brain_workspaces {
    bigint id PK
    bigint workspace_id FK
    varchar template_type
    varchar version_label
  }
  knowledge_nodes {
    bigint id PK
    uuid uuid
    bigint workspace_id FK
    bigint brain_id FK
    varchar type
    varchar domain
    varchar title
    text content
    varchar ref_type
    bigint ref_id
    jsonb metadata
    enum embedding
    bigint parent_node_id FK
  }
  knowledge_edges {
    bigint id PK
    bigint workspace_id FK
    bigint from_node_id FK
    bigint to_node_id FK
    varchar relation_type
    double weight
    boolean auto
  }
  brain_workspaces ||--o{ knowledge_nodes : "brain_id"
  knowledge_nodes ||--o{ knowledge_edges : "from_node_id"
  knowledge_nodes ||--o{ knowledge_edges : "to_node_id"
```

**Règles de gestion** :
- **Smart Assign** : `member_skill_profiles` (compétences JSONB, capacité, séniorité, mode montée en
  compétence) + `assignment_events` (features JSONB + `accepted`/`resolved_successfully`) = signaux du
  scoring ; `ai_runs` = journal des appels IA (latence, provider, fallback) pour observabilité/coût.
- **Brain OS** : `brain_workspaces` (1 brain par workspace) → `knowledge_nodes` (graphe, `embedding`
  vecteur pgvector, `ref_type/ref_id` pointant optionnellement vers issues/projets) reliés par
  `knowledge_edges` (`relation_type`, `auto` = arête dérivée des `[[wikilinks]]`/`#tags`).

### 4.4 Auth & Sécurité

```mermaid
erDiagram
  users {
    bigint id PK
  }
  refresh_tokens {
    uuid id PK
    bigint user_id FK
    varchar token
    timestamp expires_at
    boolean revoked
    varchar ip_address
    timestamp last_used_at
  }
  otp_verification {
    uuid id PK
    bigint user_id FK
    varchar otp_code
    varchar otp_type
    varchar otp_status
    varchar email
    integer attempts
    timestamp expires_at
  }
  audit_logs {
    bigint id PK
    bigint workspace_id FK
    bigint actor_user_id FK
    varchar action
    varchar entity_type
    varchar entity_id
    text details
    varchar ip_address
  }
  users ||--o{ refresh_tokens : "user_id"
  users ||--o{ otp_verification : "user_id"
  users ||--o{ audit_logs : "actor_user_id"
```

**Règles de gestion** : `refresh_tokens` avec rotation + révocation (`revoked`, purge planifiée) ;
`otp_verification` (code + tentatives + expiration) pour la vérification email/actions sensibles ;
`audit_logs` = journal des actions sensibles (`action` : USER_LOGIN, ROLE_CHANGED, GDPR_EXPORT…),
`actor_user_id` **nullable** (survit à l'anonymisation RGPD).

### 4.5 Facturation

```mermaid
erDiagram
  users {
    bigint id PK
  }
  subscriptions {
    bigint id PK
    bigint user_id FK
    varchar plan_type
    enum status
    varchar stripe_subscription_id
    numeric amount
    varchar currency
    timestamp current_period_end
    boolean cancel_at_period_end
  }
  subscription_history {
    uuid id PK
    bigint user_id FK
    varchar plan_type
    enum plan_status
    varchar stripe_event_id
    varchar event_type
    jsonb event_data
  }
  users ||--o{ subscriptions : "user_id"
  users ||--o{ subscription_history : "user_id"
```

**Règles de gestion** : une `subscriptions` courante par user (état Stripe synchronisé par webhooks) ;
`subscription_history` = trace **idempotente** des événements Stripe (`stripe_event_id` unique →
anti-rejeu, cf. `StripeWebhookService`).

### 4.6 Intégrations & Communications

```mermaid
erDiagram
  workspaces {
    bigint id PK
  }
  integrations {
    bigint id PK
    bigint workspace_id FK
    varchar provider
    text access_token
    jsonb meta
    bigint installed_by FK
  }
  webhooks {
    bigint id PK
    bigint workspace_id FK
    varchar url
    varchar secret
    ARRAY event_types
    boolean active
  }
  slack_channels {
    bigint id PK
    bigint workspace_id FK
    varchar channel_id
    ARRAY event_types
  }
  channels {
    bigint id PK
    bigint workspace_id FK
    bigint project_id FK
    varchar kind
    varchar name
    boolean is_private
    bigint created_by FK
  }
  channel_members {
    bigint channel_id PK
    bigint user_id PK
  }
  chat_messages {
    bigint id PK
    bigint channel_id FK
    bigint author_id FK
    text content
  }
  discussions {
    bigint id PK
    bigint workspace_id FK
    bigint author_id FK
    varchar title
    text body
    varchar category
  }
  notifications {
    bigint id PK
    bigint recipient_id FK
    bigint workspace_id FK
    bigint actor_id FK
    varchar type
    varchar urgency
    boolean read
    text body
  }
  workspaces ||--o{ integrations : "workspace_id"
  workspaces ||--o{ webhooks : "workspace_id"
  workspaces ||--o{ slack_channels : "workspace_id"
  workspaces ||--o{ channels : "workspace_id"
  channels ||--o{ channel_members : "channel_id"
  channels ||--o{ chat_messages : "channel_id"
  workspaces ||--o{ discussions : "workspace_id"
  workspaces ||--o{ notifications : "workspace_id"
```

**Règles de gestion** : `integrations` (OAuth GitHub/Slack, token stocké) ; `webhooks`/`slack_channels`
avec `event_types` (tableau) et `secret` (signature) ; `channels`/`chat_messages`/`discussions` =
socle Comms (⚠️ certaines features **coming-soon**, cf. roadmap) ; `notifications` = inbox temps réel
(STOMP), `read`/`acknowledged`.

### 4.7 GED & Sales

```mermaid
erDiagram
  issues {
    bigint id PK
  }
  users {
    bigint id PK
  }
  attachments {
    bigint id PK
    bigint issue_id FK
    bigint uploaded_by FK
    varchar original_name
    varchar stored_key
    varchar content_type
    bigint file_size
  }
  enterprise_inquiries {
    uuid id PK
    varchar full_name
    varchar email
    varchar team_size
    text message
    varchar status
    boolean created_account
    varchar assigned_to
    text notes
  }
  issues ||--o{ attachments : "issue_id"
  users ||--o{ attachments : "uploaded_by"
```

**Règles de gestion** : `attachments` = métadonnées des fichiers (le binaire est dans **MinIO** via
`stored_key`) ; `enterprise_inquiries` = leads commerciaux (les PII libres `message`/`notes` sont
**chiffrées au repos** AES-256-GCM, cf. `07-securite/Sécurité.md`).

## 5. Régénération

Ce document est **dérivé du schéma réel**. En cas de nouvelle migration Flyway, régénérer les diagrammes
depuis `information_schema` (script d'introspection) plutôt que d'éditer à la main — garantit l'absence de
dérive doc ↔ base.

> **Voir aussi** : [[Architecture]] (§persistance), [[Modules]], et le [dossier de conception](../16-memoire-rncp/Bloc1_Conception_Modelisation.md).
