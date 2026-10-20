---
id: modele-donnees
title: "Modèle de données : MCD / MLD (MERISE)"
doc_type: reference
statut: active
version: 2.0
date: "20/10/2026"
auteur: Pierre MICHEL
tags: [architecture, donnees, mcd, mld, merise, erd, postgresql, flyway, e8]
---

# Modèle de données : MCD / MLD (MERISE)

> **Livrable E8** (dossier de conception, compétences C8 et C9). Modèle entité-association de la
> base TaskForce.
>
> **Ce document est GÉNÉRÉ**, il ne se modifie pas à la main. Source de vérité : le schéma réel de
> PostgreSQL, obtenu par introspection d'`information_schema` après application des migrations
> Flyway. Aucune table ni relation n'est inventée : tout provient du schéma exécuté.
>
> Régénération : `node scripts/generate-schema-docs.mjs` (voir §5).

## 1. Périmètre et méthode

- **67 tables** métier (hors `flyway_schema_history`), **705 colonnes**, **121 clés étrangères**.
- **101 migrations Flyway** appliquées avec succès.
- **MERISE** : le MCD (§3) décrit les domaines et leur poids ; le MLD (§4) est le schéma relationnel
  réel, table par table. Le MPD (physique) est PostgreSQL 18 avec l'extension pgvector.
- Diagrammes en **Mermaid**, rendus nativement par GitHub et Obsidian.

### Légende

| Marque | Signification |
|---|---|
| `PK` | Clé primaire |
| `FK` | Clé étrangère |
| `UK` | Contrainte d'unicité |
| `||--||` | Association obligatoire (colonne non nulle) |
| `||--o{` | Association facultative (colonne nullable) |

Chaque relation porte le nom de sa colonne porteuse et, le cas échéant, son comportement
`ON DELETE`. Ce comportement n'est pas cosmétique : c'est lui qui détermine si la suppression
d'un workspace emporte ses données ou si un journal d'audit survit à l'anonymisation d'un compte.

## 2. Conventions transverses

- Clés primaires techniques (`id`), auto-incrémentées ou UUID selon la table.
- Horodatage `created_at` et `updated_at` sur les entités auditables.
- Isolation multi-tenant : les tables métier portent un rattachement direct ou transitif au workspace.
- Les colonnes portant un secret sont chiffrées applicativement en AES-256-GCM avant persistance.

## 3. MCD : modèle conceptuel

Niveau **conceptuel** : les entités et leurs associations, sans détail technique. Le vocabulaire
est celui du cahier des charges, pas celui des tables, afin que le modèle reste lisible par le
demandeur. Les associations sont nommées par un verbe, conformément à MERISE.

```mermaid
erDiagram
  WORKSPACE ||--o{ PROJET : "contient"
  WORKSPACE ||--o{ EQUIPE : "organise"
  WORKSPACE ||--o{ UTILISATEUR : "réunit"
  WORKSPACE ||--o{ PAGE : "documente"
  EQUIPE }o--o{ UTILISATEUR : "regroupe"
  PROJET ||--o{ TACHE : "décompose en"
  PROJET ||--o{ CYCLE : "planifie"
  CYCLE }o--o{ TACHE : "cadence"
  UTILISATEUR ||--o| PROFIL_COMPETENCES : "possède"
  UTILISATEUR ||--o{ ABSENCE : "déclare"
  UTILISATEUR ||--o{ TACHE : "se voit affecter"
  UTILISATEUR ||--o{ NOTIFICATION : "reçoit"
  UTILISATEUR ||--o| ABONNEMENT : "souscrit"
  TACHE ||--o{ DECISION_AFFECTATION : "justifie"
  PROFIL_COMPETENCES ||--o{ DECISION_AFFECTATION : "pondère"
```

| Entité conceptuelle | Table support | Rôle |
|---|---|---|
| **UTILISATEUR** | `users` | Le collaborateur du cahier des charges |
| **WORKSPACE** | `workspaces` | Espace de travail d'une organisation |
| **EQUIPE** | `teams` | Regroupement de collaborateurs |
| **PROJET** | `projects` | Regroupement de tâches |
| **TACHE** | `issues` | L'unité de travail à répartir |
| **CYCLE** | `cycles` | Itération de travail bornée dans le temps |
| **PROFIL_COMPETENCES** | `member_skill_profiles` | Compétences, séniorité et capacité d'un collaborateur |
| **ABSENCE** | `member_leaves` | Indisponibilité déclarée, entrant dans le calcul de charge |
| **DECISION_AFFECTATION** | `assignment_events` | Trace d'une affectation et de son motif |
| **NOTIFICATION** | `notifications` | Alerte de surcharge ou d'échéance |
| **ABONNEMENT** | `subscriptions` | Plan souscrit par un utilisateur |
| **PAGE** | `pages` | Documentation collaborative |

Chaque entité conceptuelle est adossée à une table réelle, et ce rattachement est **vérifié à la
génération** : un concept sans support en base serait une invention, et le script refuserait de
produire le document.

### Répartition du schéma par domaine

Le passage au logique fait apparaître des tables de liaison, d'historisation et de configuration
qui n'ont pas d'existence conceptuelle. D'où l'écart entre 12 entités et
67 tables. Leur poids relatif dit où se concentre la complexité, et il correspond à
ce qu'on attend : le coeur métier des projets et des tâches est de loin le plus lourd.

| Domaine | Tables |
|---|:--:|
| 4.1 IAM et Workspace | 7 |
| 4.2 Projets et Issues (coeur métier) | 21 |
| 4.3 IA, affectation intelligente et graphe de connaissances | 14 |
| 4.4 Authentification et sécurité | 7 |
| 4.5 Facturation | 2 |
| 4.6 Intégrations et communications | 9 |
| 4.7 Documentation, tableaux de bord, prospects et retours | 4 |
| 4.8 Délégation aux agents de code | 3 |
| **Total métier** | **67** |

## 4. MLD : schéma relationnel réel, par domaine

Chaque diagramme ne montre que les **colonnes porteuses de clés** (primaire, étrangère, unicité) :
au-delà, le rendu devient illisible. Le détail exhaustif des colonnes vit dans le
[dictionnaire de données](./Dictionnaire_Donnees.md), généré par le même script.

### 4.1 IAM et Workspace

Le socle multi-tenant. Toute donnée métier est rattachée à un workspace, et l'appartenance à un workspace conditionne l'accès.

**7 tables** : `users`, `workspaces`, `workspace_members`, `workspace_invitations`, `teams`, `team_members`, `companies`.

```mermaid
erDiagram
  users {
    int8 id PK
    varchar keycloak_id UK
    varchar email UK
    int8 company_id FK
    varchar stripe_customer_id UK
    varchar stripe_subscription_id UK
    varchar passkey_handle UK
  }
  workspaces {
    int8 id PK
    varchar slug UK
    int8 owner_id FK
    uuid uuid UK
  }
  workspace_members {
    int8 id PK
    int8 workspace_id FK
    int8 user_id FK
    int8 invited_by FK
  }
  workspace_invitations {
    int8 id PK
    int8 workspace_id FK
    int8 invited_by FK
    varchar token UK
    int8 project_id FK
  }
  teams {
    int8 id PK
    int8 workspace_id FK
    int8 created_by FK
  }
  team_members {
    int8 id PK
    int8 team_id FK
    int8 user_id FK
  }
  companies {
    int8 id PK
  }
  companies ||--o{ users : "company_id / ON DELETE SET NULL"
  users ||--|{ workspaces : "owner_id / ON DELETE RESTRICT"
  workspaces ||--|{ workspace_members : "workspace_id / ON DELETE CASCADE"
  users ||--|{ workspace_members : "user_id / ON DELETE CASCADE"
  users ||--o{ workspace_members : "invited_by / ON DELETE SET NULL"
  projects ||--o{ workspace_invitations : "project_id / ON DELETE CASCADE"
  workspaces ||--|{ workspace_invitations : "workspace_id / ON DELETE CASCADE"
  users ||--o{ workspace_invitations : "invited_by / ON DELETE SET NULL"
  workspaces ||--|{ teams : "workspace_id / ON DELETE CASCADE"
  users ||--o{ teams : "created_by / ON DELETE SET NULL"
  teams ||--|{ team_members : "team_id / ON DELETE CASCADE"
  users ||--|{ team_members : "user_id / ON DELETE CASCADE"
```

### 4.2 Projets et Issues (coeur métier)

Le domaine que le cahier des charges décrit : les tâches, leur affectation, la charge et les compétences qui la conditionnent.

**21 tables** : `projects`, `project_members`, `project_teams`, `project_labels`, `project_favorites`, `issues`, `issue_statuses`, `issue_types`, `issue_comments`, `issue_activity`, `issue_checklist_items`, `issue_relations`, `issue_label_assignments`, `issue_worklogs`, `issue_sequence_counters`, `cycles`, `cycle_issues`, `attachments`, `member_leaves`, `member_skill_profiles`, `assignment_events`.

```mermaid
erDiagram
  projects {
    int8 id PK
    int8 workspace_id FK
    varchar identifier UK
    int8 created_by FK
  }
  project_members {
    int8 id PK
    int8 project_id FK
    int8 user_id FK
    int8 added_by FK
  }
  project_teams {
    int8 id PK
    int8 project_id FK
    int8 team_id FK
  }
  project_labels {
    int8 id PK
    int8 project_id FK
    varchar name UK
  }
  project_favorites {
    int8 id PK
    int8 user_id FK
    int8 project_id FK
  }
  issues {
    int8 id PK
    int8 project_id FK
    int4 sequence_number UK
    int8 status_id FK
    int8 type_id FK
    int8 assignee_id FK
    int8 reporter_id FK
    int8 parent_id FK
    int8 assignment_assigned_by_id FK
  }
  issue_statuses {
    int8 id PK
    int8 project_id FK
    varchar name UK
  }
  issue_types {
    int8 id PK
    int8 project_id FK
    varchar name UK
  }
  issue_comments {
    int8 id PK
    int8 issue_id FK
    int8 author_id FK
  }
  issue_activity {
    int8 id PK
    int8 issue_id FK
    int8 actor_id FK
  }
  issue_checklist_items {
    int8 id PK
    int8 issue_id FK
  }
  issue_relations {
    int8 id PK
    int8 source_id FK
    int8 target_id FK
    vector relation_type UK
    int8 created_by FK
  }
  issue_label_assignments {
    int8 issue_id PK
    int8 label_id PK
  }
  issue_worklogs {
    int8 id PK
    int8 issue_id FK
    int8 user_id FK
  }
  issue_sequence_counters {
    int8 project_id PK
  }
  cycles {
    int8 id PK
    int8 project_id FK
    varchar name UK
    int8 created_by FK
  }
  cycle_issues {
    int8 id PK
    int8 cycle_id FK
    int8 issue_id FK
    int8 added_by FK
  }
  attachments {
    int8 id PK
    int8 issue_id FK
    int8 uploaded_by FK
    varchar stored_key UK
  }
  member_leaves {
    int8 id PK
    int8 workspace_id FK
    int8 user_id FK
  }
  member_skill_profiles {
    int8 id PK
    int8 workspace_id FK
    int8 user_id FK
  }
  assignment_events {
    int8 id PK
    int8 workspace_id FK
    int8 issue_id FK
    int8 assignee_user_id FK
    int8 assigned_by_user_id FK
  }
  workspaces ||--|{ projects : "workspace_id / ON DELETE CASCADE"
  users ||--|{ projects : "created_by / ON DELETE RESTRICT"
  projects ||--|{ project_members : "project_id / ON DELETE CASCADE"
  users ||--|{ project_members : "user_id / ON DELETE CASCADE"
  users ||--o{ project_members : "added_by / ON DELETE SET NULL"
  teams ||--|{ project_teams : "team_id / ON DELETE CASCADE"
  projects ||--|{ project_teams : "project_id / ON DELETE CASCADE"
  projects ||--|{ project_labels : "project_id / ON DELETE CASCADE"
  users ||--|{ project_favorites : "user_id / ON DELETE CASCADE"
  projects ||--|{ project_favorites : "project_id / ON DELETE CASCADE"
  users ||--o{ issues : "assignment_assigned_by_id / ON DELETE SET NULL"
  projects ||--|{ issues : "project_id / ON DELETE CASCADE"
  issue_statuses ||--|{ issues : "status_id / ON DELETE RESTRICT"
  issue_types ||--o{ issues : "type_id / ON DELETE SET NULL"
  users ||--o{ issues : "assignee_id / ON DELETE SET NULL"
  users ||--|{ issues : "reporter_id / ON DELETE RESTRICT"
  issues ||--o{ issues : "parent_id / ON DELETE SET NULL"
  projects ||--|{ issue_statuses : "project_id / ON DELETE CASCADE"
  projects ||--|{ issue_types : "project_id / ON DELETE CASCADE"
  users ||--|{ issue_comments : "author_id / ON DELETE RESTRICT"
  issues ||--|{ issue_comments : "issue_id / ON DELETE CASCADE"
  users ||--o{ issue_activity : "actor_id / ON DELETE SET NULL"
  issues ||--|{ issue_activity : "issue_id / ON DELETE CASCADE"
  issues ||--|{ issue_checklist_items : "issue_id / ON DELETE CASCADE"
  issues ||--|{ issue_relations : "target_id / ON DELETE CASCADE"
  issues ||--|{ issue_relations : "source_id / ON DELETE CASCADE"
  users ||--|{ issue_relations : "created_by / ON DELETE RESTRICT"
  project_labels ||--|{ issue_label_assignments : "label_id / ON DELETE CASCADE"
  issues ||--|{ issue_label_assignments : "issue_id / ON DELETE CASCADE"
  users ||--|{ issue_worklogs : "user_id / ON DELETE CASCADE"
  issues ||--|{ issue_worklogs : "issue_id / ON DELETE CASCADE"
  projects ||--|{ issue_sequence_counters : "project_id / ON DELETE CASCADE"
  users ||--|{ cycles : "created_by / ON DELETE RESTRICT"
  projects ||--|{ cycles : "project_id / ON DELETE CASCADE"
  cycles ||--|{ cycle_issues : "cycle_id / ON DELETE CASCADE"
  issues ||--|{ cycle_issues : "issue_id / ON DELETE CASCADE"
  users ||--|{ cycle_issues : "added_by / ON DELETE RESTRICT"
  issues ||--|{ attachments : "issue_id / ON DELETE CASCADE"
  users ||--o{ attachments : "uploaded_by / ON DELETE SET NULL"
  users ||--|{ member_leaves : "user_id / ON DELETE CASCADE"
  workspaces ||--|{ member_leaves : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ member_skill_profiles : "workspace_id / ON DELETE CASCADE"
  users ||--|{ member_skill_profiles : "user_id / ON DELETE CASCADE"
  workspaces ||--|{ assignment_events : "workspace_id / ON DELETE CASCADE"
  issues ||--o{ assignment_events : "issue_id / ON DELETE SET NULL"
  users ||--|{ assignment_events : "assignee_user_id / ON DELETE RESTRICT"
  users ||--o{ assignment_events : "assigned_by_user_id / ON DELETE SET NULL"
```

### 4.3 IA, affectation intelligente et graphe de connaissances

Le moteur d'affectation et sa mémoire. `knowledge_nodes` porte les vecteurs d'embedding utilisés par la recherche sémantique.

**14 tables** : `ai_conversation`, `ai_message`, `ai_documents`, `ai_runs`, `ai_generations`, `ai_token_usage`, `ai_insight_snapshots`, `brain_workspaces`, `knowledge_nodes`, `knowledge_edges`, `analysis_job`, `decision_brief`, `decision_priority`, `saved_chart`.

```mermaid
erDiagram
  ai_conversation {
    int8 id PK
    int8 workspace_id FK
    int8 user_id FK
  }
  ai_message {
    int8 id PK
    int8 conversation_id FK
  }
  ai_documents {
    int8 id PK
    int8 workspace_id FK
    varchar source_type UK
    int8 source_id UK
    int4 chunk_index UK
  }
  ai_runs {
    int8 id PK
    int8 workspace_id FK
  }
  ai_generations {
    int8 id PK
    int8 workspace_id FK
  }
  ai_token_usage {
    int8 id PK
    int8 account_id FK
  }
  ai_insight_snapshots {
    int8 id PK
    int8 workspace_id FK
    date snapshot_date UK
  }
  brain_workspaces {
    int8 id PK
    int8 workspace_id FK
  }
  knowledge_nodes {
    int8 id PK
    uuid uuid UK
    int8 workspace_id FK
    int8 brain_id FK
    int8 parent_node_id FK
  }
  knowledge_edges {
    int8 id PK
    int8 workspace_id FK
    int8 from_node_id FK
    int8 to_node_id FK
    varchar relation_type UK
  }
  analysis_job {
    int8 id PK
    int8 workspace_id FK
    int8 project_id FK
    int8 user_id FK
    int8 brief_id FK
  }
  decision_brief {
    int8 id PK
    int8 workspace_id FK
    int8 project_id FK
  }
  decision_priority {
    int8 id PK
    int8 brief_id FK
    int8 issue_id FK
  }
  saved_chart {
    int8 id PK
    int8 workspace_id FK
    int8 created_by_id FK
  }
  workspaces ||--|{ ai_conversation : "workspace_id / ON DELETE CASCADE"
  users ||--|{ ai_conversation : "user_id / ON DELETE CASCADE"
  ai_conversation ||--|{ ai_message : "conversation_id / ON DELETE CASCADE"
  workspaces ||--|{ ai_documents : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ ai_runs : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ ai_generations : "workspace_id / ON DELETE CASCADE"
  users ||--|{ ai_token_usage : "account_id / ON DELETE CASCADE"
  workspaces ||--|{ ai_insight_snapshots : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ brain_workspaces : "workspace_id / ON DELETE CASCADE"
  knowledge_nodes ||--o{ knowledge_nodes : "parent_node_id / ON DELETE SET NULL"
  brain_workspaces ||--o{ knowledge_nodes : "brain_id / ON DELETE CASCADE"
  workspaces ||--|{ knowledge_nodes : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ knowledge_edges : "workspace_id / ON DELETE CASCADE"
  knowledge_nodes ||--|{ knowledge_edges : "from_node_id / ON DELETE CASCADE"
  knowledge_nodes ||--|{ knowledge_edges : "to_node_id / ON DELETE CASCADE"
  workspaces ||--|{ analysis_job : "workspace_id / ON DELETE CASCADE"
  projects ||--|{ analysis_job : "project_id / ON DELETE CASCADE"
  users ||--o{ analysis_job : "user_id / ON DELETE SET NULL"
  decision_brief ||--o{ analysis_job : "brief_id / ON DELETE SET NULL"
  projects ||--|{ decision_brief : "project_id / ON DELETE CASCADE"
  workspaces ||--|{ decision_brief : "workspace_id / ON DELETE CASCADE"
  issues ||--o{ decision_priority : "issue_id / ON DELETE SET NULL"
  decision_brief ||--|{ decision_priority : "brief_id / ON DELETE CASCADE"
  workspaces ||--|{ saved_chart : "workspace_id / ON DELETE CASCADE"
  users ||--o{ saved_chart : "created_by_id / ON DELETE SET NULL"
```

### 4.4 Authentification et sécurité

Les comptes et les mots de passe sont délégués à Keycloak. L'application garde ce qu'elle gère elle-même : double authentification (TOTP), clés d'accès (passkeys), jetons d'accès personnels, sessions de l'app desktop, codes à usage unique, jetons anti-CSRF et journal d'audit.

**7 tables** : `otp_verification`, `oauth_states`, `audit_logs`, `user_two_factor`, `user_credentials`, `personal_access_tokens`, `desktop_sessions`.

```mermaid
erDiagram
  otp_verification {
    uuid id PK
    int8 user_id FK
  }
  oauth_states {
    varchar state PK
    int8 workspace_id FK
    int8 user_id FK
  }
  audit_logs {
    int8 id PK
    int8 workspace_id FK
    int8 actor_user_id FK
  }
  user_two_factor {
    int8 id PK
    int8 user_id FK
  }
  user_credentials {
    varchar credential_id PK
    varchar user_entity_user_id FK
  }
  personal_access_tokens {
    int8 id PK
    int8 user_id FK
    varchar token_hash UK
  }
  desktop_sessions {
    int8 id PK
    int8 user_id FK
    varchar token_hash UK
  }
  users ||--o{ otp_verification : "user_id / ON DELETE CASCADE"
  users ||--o{ oauth_states : "user_id / ON DELETE SET NULL"
  workspaces ||--|{ oauth_states : "workspace_id / ON DELETE CASCADE"
  workspaces ||--o{ audit_logs : "workspace_id / ON DELETE SET NULL"
  users ||--o{ audit_logs : "actor_user_id / ON DELETE SET NULL"
  users ||--|{ user_two_factor : "user_id / ON DELETE CASCADE"
  users ||--|{ user_credentials : "user_entity_user_id / ON DELETE CASCADE"
  users ||--|{ personal_access_tokens : "user_id / ON DELETE CASCADE"
  users ||--|{ desktop_sessions : "user_id / ON DELETE CASCADE"
```

### 4.5 Facturation

Abonnements et historique. Aucune donnée de carte n'est stockée : la facturation est déléguée au prestataire de paiement.

**2 tables** : `subscriptions`, `subscription_history`.

```mermaid
erDiagram
  subscriptions {
    int8 id PK
    int8 user_id FK
    varchar stripe_subscription_id UK
  }
  subscription_history {
    uuid id PK
    int8 user_id FK
  }
  users ||--|{ subscriptions : "user_id / ON DELETE CASCADE"
  users ||--|{ subscription_history : "user_id / ON DELETE CASCADE"
```

### 4.6 Intégrations et communications

Connecteurs externes, webhooks et leurs envois, notifications et leurs préférences. Les identifiants de connecteurs sont chiffrés en base (AES-256-GCM).

**9 tables** : `integrations`, `connector_connection`, `mcp_oauth_states`, `webhooks`, `webhook_deliveries`, `slack_channels`, `issue_github_links`, `notifications`, `notification_preferences`.

```mermaid
erDiagram
  integrations {
    int8 id PK
    int8 workspace_id FK
    varchar provider UK
    int8 installed_by FK
  }
  connector_connection {
    int8 id PK
    int8 workspace_id FK
    int8 connected_by FK
  }
  mcp_oauth_states {
    varchar state PK
    int8 workspace_id FK
    int8 user_id FK
  }
  webhooks {
    int8 id PK
    int8 workspace_id FK
    int8 created_by FK
  }
  webhook_deliveries {
    int8 id PK
    int8 webhook_id FK
    uuid delivery_id UK
  }
  slack_channels {
    int8 id PK
    int8 workspace_id FK
  }
  issue_github_links {
    int8 id PK
    int8 issue_id FK
    int8 linked_by FK
  }
  notifications {
    int8 id PK
    int8 recipient_id FK
    int8 workspace_id FK
    int8 actor_id FK
  }
  notification_preferences {
    int8 id PK
    int8 user_id FK
    varchar event_key UK
  }
  users ||--o{ integrations : "installed_by / ON DELETE SET NULL"
  workspaces ||--|{ integrations : "workspace_id / ON DELETE CASCADE"
  users ||--o{ connector_connection : "connected_by / ON DELETE SET NULL"
  workspaces ||--|{ connector_connection : "workspace_id / ON DELETE CASCADE"
  users ||--o{ mcp_oauth_states : "user_id / ON DELETE SET NULL"
  workspaces ||--|{ mcp_oauth_states : "workspace_id / ON DELETE CASCADE"
  workspaces ||--|{ webhooks : "workspace_id / ON DELETE CASCADE"
  users ||--o{ webhooks : "created_by / ON DELETE SET NULL"
  webhooks ||--|{ webhook_deliveries : "webhook_id / ON DELETE CASCADE"
  workspaces ||--|{ slack_channels : "workspace_id / ON DELETE CASCADE"
  issues ||--|{ issue_github_links : "issue_id / ON DELETE CASCADE"
  users ||--o{ issue_github_links : "linked_by / ON DELETE SET NULL"
  workspaces ||--|{ notifications : "workspace_id / ON DELETE CASCADE"
  users ||--o{ notifications : "actor_id / ON DELETE SET NULL"
  users ||--|{ notifications : "recipient_id / ON DELETE CASCADE"
  users ||--|{ notification_preferences : "user_id / ON DELETE CASCADE"
```

### 4.7 Documentation, tableaux de bord, prospects et retours

Pages de documentation collaborative, composition du tableau de bord par utilisateur, demandes commerciales, et retours envoyés depuis l'app.

**4 tables** : `pages`, `dashboard_cards`, `enterprise_inquiries`, `feedback`.

```mermaid
erDiagram
  pages {
    int8 id PK
    int8 project_id FK
    int8 created_by FK
  }
  dashboard_cards {
    int8 id PK
    int8 workspace_id FK
    int8 user_id FK
  }
  enterprise_inquiries {
    uuid id PK
  }
  feedback {
    int8 id PK
    int8 user_id FK
  }
  users ||--o{ pages : "created_by / ON DELETE SET NULL"
  projects ||--|{ pages : "project_id / ON DELETE CASCADE"
  users ||--|{ dashboard_cards : "user_id / ON DELETE CASCADE"
  workspaces ||--|{ dashboard_cards : "workspace_id / ON DELETE CASCADE"
  users ||--|{ feedback : "user_id / ON DELETE CASCADE"
```

### 4.8 Délégation aux agents de code

Les tickets confiés à un agent de code (Claude Code par le runner local, ou GitHub Copilot) : chaque exécution, sa chronologie, et les actions de l'agent qui attendent la décision de la personne qui a délégué.

**3 tables** : `delivery_runs`, `delivery_run_events`, `delivery_run_approvals`.

```mermaid
erDiagram
  delivery_runs {
    int8 id PK
    int8 issue_id FK
    int8 started_by FK
  }
  delivery_run_events {
    int8 id PK
    int8 run_id FK
    int4 seq UK
  }
  delivery_run_approvals {
    int8 id PK
    int8 run_id FK
    int8 decided_by FK
  }
  issues ||--|{ delivery_runs : "issue_id / ON DELETE CASCADE"
  users ||--o{ delivery_runs : "started_by / ON DELETE SET NULL"
  delivery_runs ||--|{ delivery_run_events : "run_id / ON DELETE CASCADE"
  users ||--o{ delivery_run_approvals : "decided_by / ON DELETE SET NULL"
  delivery_runs ||--|{ delivery_run_approvals : "run_id / ON DELETE CASCADE"
```

## 5. Régénération

```bash
node scripts/generate-schema-docs.mjs
```

Le script interroge la base de développement en cours d'exécution et réécrit ce document ainsi que
le dictionnaire de données. Il **échoue volontairement** si une table de la base n'est classée dans
aucun domaine, ou si un domaine référence une table disparue.

Ce blocage est la leçon du 23/07/2026 : la consigne « régénérer plutôt qu'éditer à la main »
figurait déjà ici, mais **aucun script ne l'accompagnait**. Entre le 05/07 et le 23/07,
10 tables ont été ajoutées sans jamais apparaître dans ces documents, une table supprimée y est
restée, et tous les totaux étaient faux. Une consigne sans outil dérive.

Variante non destructive, utilisable en intégration continue :

```bash
node scripts/generate-schema-docs.mjs --check
```

> Voir aussi : [[Dictionnaire_Donnees]] · [[Architecture]] · [[Modules]] · [[Diagramme_Classes_UML]].
