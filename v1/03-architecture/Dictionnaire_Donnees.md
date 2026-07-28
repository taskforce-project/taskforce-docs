---
id: dictionnaire-donnees
title: Dictionnaire de données
doc_type: reference
statut: active
version: 2.0
date: "24/07/2026"
auteur: Pierre MICHEL
tags: [architecture, donnees, dictionnaire, postgresql, e8]
---

# Dictionnaire de données

> **Document GÉNÉRÉ**, il ne se modifie pas à la main. Régénération :
> `node scripts/generate-schema-docs.mjs`.
>
> Périmètre : **55 tables** métier, **545 colonnes**, **104 clés étrangères**,
> **72 migrations Flyway** appliquées. Introspection d'`information_schema` sur la base réelle.

La colonne **ON DELETE** n'est renseignée que lorsqu'elle diffère du comportement par défaut.
C'est une information de conception, pas un détail : elle dit si la suppression d'un parent
emporte ses enfants, les détache, ou est refusée.

## 4.1 IAM et Workspace

Le socle multi-tenant. Toute donnée métier est rattachée à un workspace, et l'appartenance à un workspace conditionne l'accès.

### `users`

19 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('users_id_seq'::regclass)` |  |
| `keycloak_id` | varchar(255) | non | UK |  |  |
| `email` | varchar(255) | non | UK |  |  |
| `company_id` | int8 | oui | FK → `companies.id` |  | SET NULL |
| `is_active` | bool | non |  | `true` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |
| `plan_type` | varchar(20) | non |  |  |  |
| `plan_status` | vector | oui |  |  |  |
| `stripe_customer_id` | varchar(255) | oui | UK |  |  |
| `stripe_subscription_id` | varchar(255) | oui | UK |  |  |
| `subscription_start_date` | timestamp | oui |  |  |  |
| `subscription_end_date` | timestamp | oui |  |  |  |
| `trial_end_date` | timestamp | oui |  |  |  |
| `enterprise_interest` | bool | oui |  | `false` |  |
| `display_name` | varchar(150) | oui |  |  |  |
| `avatar_url` | varchar(500) | oui |  |  |  |

### `workspaces`

9 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('workspaces_id_seq'::regclass)` |  |
| `name` | varchar(100) | non |  |  |  |
| `slug` | varchar(100) | non | UK |  |  |
| `description` | varchar(500) | oui |  |  |  |
| `logo_url` | varchar(1000) | oui |  |  |  |
| `owner_id` | int8 | non | FK → `users.id` |  | RESTRICT |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `uuid` | uuid | non | UK | `uuid_generate_v4()` |  |

### `workspace_members`

6 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('workspace_members_id_seq'::regc` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `role` | varchar(20) | non |  | `'MEMBER'::character varying` |  |
| `invited_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `joined_at` | timestamp | non |  | `now()` |  |

### `workspace_invitations`

13 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('workspace_invitations_id_seq'::` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `invited_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `email` | varchar(255) | non |  |  |  |
| `role` | varchar(20) | non |  | `'MEMBER'::character varying` |  |
| `token` | varchar(100) | non | UK |  |  |
| `status` | varchar(20) | non |  | `'PENDING'::character varying` |  |
| `expires_at` | timestamp | non |  |  |  |
| `accepted_at` | timestamp | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `teams`

9 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('teams_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `created_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `name` | varchar(200) | non |  |  |  |
| `description` | text | oui |  |  |  |
| `emoji` | varchar(10) | non |  | `'👥'::character varying` |  |
| `color` | varchar(50) | non |  | `'bg-primary'::character varying` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `team_members`

5 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('team_members_id_seq'::regclass)` |  |
| `team_id` | int8 | non | FK → `teams.id`, UK |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `role` | varchar(20) | non |  | `'MEMBER'::character varying` |  |
| `joined_at` | timestamp | non |  | `now()` |  |

### `companies`

9 colonnes · 0 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('companies_id_seq'::regclass)` |  |
| `name` | varchar(255) | non |  |  |  |
| `email` | varchar(255) | oui |  |  |  |
| `phone` | varchar(50) | oui |  |  |  |
| `address` | text | oui |  |  |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

## 4.2 Projets et Issues (coeur métier)

Le domaine que le cahier des charges décrit : les tâches, leur affectation, la charge et les compétences qui la conditionnent.

### `projects`

13 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('projects_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `name` | varchar(150) | non |  |  |  |
| `identifier` | varchar(10) | non | UK |  |  |
| `description` | varchar(1000) | oui |  |  |  |
| `status` | vector | non |  | `'ACTIVE'::project_status` |  |
| `is_public` | bool | non |  | `false` |  |
| `created_by` | int8 | non | FK → `users.id` |  | RESTRICT |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `icon_url` | text | oui |  |  |  |
| `color` | varchar(50) | non |  | `'bg-primary'::character varying` |  |
| `growth_mode` | bool | non |  | `false` |  |

### `project_members`

6 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('project_members_id_seq'::regcla` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `role` | vector | non |  | `'MEMBER'::project_role` |  |
| `added_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `joined_at` | timestamp | non |  | `now()` |  |

### `project_teams`

4 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('project_teams_id_seq'::regclass` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `team_id` | int8 | non | FK → `teams.id`, UK |  | CASCADE |
| `created_at` | timestamp | non |  | `now()` |  |

### `project_labels`

6 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('project_labels_id_seq'::regclas` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `name` | varchar(50) | non | UK |  |  |
| `color` | varchar(30) | non |  | `'#6366f1'::character varying` |  |
| `description` | varchar(200) | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `project_favorites`

4 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('project_favorites_id_seq'::regc` |  |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `created_at` | timestamp | non |  | `now()` |  |

### `issues`

20 colonnes · 6 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issues_id_seq'::regclass)` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `sequence_number` | int4 | non | UK |  |  |
| `title` | varchar(500) | non |  |  |  |
| `description` | text | oui |  |  |  |
| `priority` | vector | non |  | `'NONE'::issue_priority` |  |
| `status_id` | int8 | non | FK → `issue_statuses.id` |  | RESTRICT |
| `type_id` | int8 | oui | FK → `issue_types.id` |  | SET NULL |
| `assignee_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `reporter_id` | int8 | non | FK → `users.id` |  | RESTRICT |
| `parent_id` | int8 | oui | FK → `issues.id` |  | SET NULL |
| `start_date` | date | oui |  |  |  |
| `due_date` | date | oui |  |  |  |
| `completed_at` | timestamp | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `position` | int4 | non |  | `0` |  |
| `story_points` | int4 | oui |  |  |  |
| `archived_at` | timestamp | oui |  |  |  |
| `pinned` | bool | non |  | `false` |  |

### `issue_statuses`

8 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_statuses_id_seq'::regclas` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `name` | varchar(50) | non | UK |  |  |
| `color` | varchar(30) | non |  | `'#6366f1'::character varying` |  |
| `category` | vector | non |  |  |  |
| `position` | smallint | non |  | `0` |  |
| `is_default` | bool | non |  | `false` |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_types`

7 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_types_id_seq'::regclass)` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `name` | varchar(50) | non | UK |  |  |
| `color` | varchar(30) | non |  | `'#6366f1'::character varying` |  |
| `icon` | varchar(50) | non |  | `'circle-dot'::character varying` |  |
| `is_default` | bool | non |  | `false` |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_comments`

7 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_comments_id_seq'::regclas` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `author_id` | int8 | non | FK → `users.id` |  | RESTRICT |
| `content` | text | non |  |  |  |
| `is_edited` | bool | non |  | `false` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `issue_activity`

7 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_activity_id_seq'::regclas` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `actor_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `action` | vector | non |  |  |  |
| `old_value` | varchar(500) | oui |  |  |  |
| `new_value` | varchar(500) | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_checklist_items`

7 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_checklist_items_id_seq'::` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `content` | varchar(500) | non |  |  |  |
| `is_done` | bool | non |  | `false` |  |
| `position` | int4 | non |  | `0` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `issue_relations`

6 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_relations_id_seq'::regcla` |  |
| `source_id` | int8 | non | FK → `issues.id`, UK |  | CASCADE |
| `target_id` | int8 | non | FK → `issues.id`, UK |  | CASCADE |
| `relation_type` | vector | non | UK |  |  |
| `created_by` | int8 | non | FK → `users.id` |  | RESTRICT |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_label_assignments`

2 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `issue_id` | int8 | non | PK, FK → `issues.id` |  | CASCADE |
| `label_id` | int8 | non | PK, FK → `project_labels.id` |  | CASCADE |

### `issue_worklogs`

7 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_worklogs_id_seq'::regclas` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `minutes` | int4 | non |  |  |  |
| `description` | varchar(500) | oui |  |  |  |
| `logged_at` | date | non |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_sequence_counters`

2 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `project_id` | int8 | non | PK, FK → `projects.id` |  | CASCADE |
| `last_number` | int4 | non |  | `0` |  |

### `cycles`

10 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('cycles_id_seq'::regclass)` |  |
| `project_id` | int8 | non | FK → `projects.id`, UK |  | CASCADE |
| `name` | varchar(255) | non | UK |  |  |
| `description` | text | oui |  |  |  |
| `start_date` | date | oui |  |  |  |
| `end_date` | date | oui |  |  |  |
| `status` | vector | non |  | `'DRAFT'::cycle_status` |  |
| `created_by` | int8 | non | FK → `users.id` |  | RESTRICT |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `cycle_issues`

5 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('cycle_issues_id_seq'::regclass)` |  |
| `cycle_id` | int8 | non | FK → `cycles.id`, UK |  | CASCADE |
| `issue_id` | int8 | non | FK → `issues.id`, UK |  | CASCADE |
| `added_by` | int8 | non | FK → `users.id` |  | RESTRICT |
| `added_at` | timestamp | non |  | `now()` |  |

### `attachments`

8 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('attachments_id_seq'::regclass)` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `uploaded_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `original_name` | varchar(255) | non |  |  |  |
| `stored_key` | varchar(512) | non | UK |  |  |
| `content_type` | varchar(128) | non |  |  |  |
| `file_size` | int8 | non |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `member_leaves`

11 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('member_leaves_id_seq'::regclass` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `type` | varchar(20) | non |  |  |  |
| `start_date` | date | non |  |  |  |
| `end_date` | date | non |  |  |  |
| `note` | text | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `member_skill_profiles`

12 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('member_skill_profiles_id_seq'::` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `profile_text` | text | oui |  |  |  |
| `skills_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `stats_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `embedding` | vector | oui |  |  |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `capacity_hours_per_week` | int4 | oui |  |  |  |
| `seniority` | varchar(20) | oui |  |  |  |
| `growth_enabled` | bool | non |  | `false` |  |
| `growth_target_skills` | jsonb | non |  | `'[]'::jsonb` |  |

### `assignment_events`

10 colonnes · 4 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('assignment_events_id_seq'::regc` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `issue_id` | int8 | oui | FK → `issues.id` |  | SET NULL |
| `assignee_user_id` | int8 | non | FK → `users.id` |  | RESTRICT |
| `assigned_by_user_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `decision_source` | varchar(32) | non |  |  |  |
| `accepted` | bool | oui |  |  |  |
| `resolved_successfully` | bool | oui |  |  |  |
| `features_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `created_at` | timestamp | non |  | `now()` |  |

## 4.3 IA, affectation intelligente et graphe de connaissances

Le moteur d'affectation et sa mémoire. `knowledge_nodes` porte les vecteurs d'embedding utilisés par la recherche sémantique.

### `ai_conversation`

10 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_conversation_id_seq'::regcla` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `title` | varchar(200) | non |  | `'Nouvelle conversation'::character varyi` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |
| `summary` | text | oui |  |  |  |
| `summary_upto_id` | int8 | oui |  |  |  |

### `ai_message`

7 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_message_id_seq'::regclass)` |  |
| `conversation_id` | int8 | non | FK → `ai_conversation.id` |  | CASCADE |
| `role` | varchar(16) | non |  |  |  |
| `content` | text | non |  |  |  |
| `mode` | varchar(16) | oui |  |  |  |
| `total_tokens` | int8 | non |  | `0` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |

### `ai_documents`

11 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_documents_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `source_type` | varchar(32) | non | UK |  |  |
| `source_id` | int8 | non | UK |  |  |
| `chunk_index` | int4 | non | UK | `0` |  |
| `title` | varchar(500) | oui |  |  |  |
| `content` | text | non |  |  |  |
| `metadata_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `embedding` | vector | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `ai_runs`

14 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_runs_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `feature_name` | varchar(64) | non |  |  |  |
| `provider` | varchar(32) | non |  |  |  |
| `model_name` | varchar(128) | non |  |  |  |
| `latency_ms` | int4 | oui |  |  |  |
| `input_tokens` | int4 | oui |  |  |  |
| `output_tokens` | int4 | oui |  |  |  |
| `status` | varchar(32) | non |  |  |  |
| `fallback_used` | bool | non |  | `false` |  |
| `request_hash` | varchar(128) | oui |  |  |  |
| `meta_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `expires_at` | timestamp | non |  | `(now() + '90 days'::interval)` |  |

### `ai_token_usage`

11 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_token_usage_id_seq'::regclas` |  |
| `period` | varchar(7) | non |  |  |  |
| `prompt_tokens` | int8 | non |  | `0` |  |
| `completion_tokens` | int8 | non |  | `0` |  |
| `total_tokens` | int8 | non |  | `0` |  |
| `request_count` | int4 | non |  | `0` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |
| `account_id` | int8 | non | FK → `users.id` |  | CASCADE |

### `ai_insight_snapshots`

9 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('ai_insight_snapshots_id_seq'::r` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `snapshot_date` | date | non | UK |  |  |
| `summary_text` | text | oui |  |  |  |
| `exceptions_json` | jsonb | non |  | `'[]'::jsonb` |  |
| `agents_json` | jsonb | non |  | `'[]'::jsonb` |  |
| `source_metrics_json` | jsonb | non |  | `'{}'::jsonb` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `expires_at` | timestamp | non |  | `(now() + '180 days'::interval)` |  |

### `brain_workspaces`

8 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('brain_workspaces_id_seq'::regcl` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `template_type` | varchar(40) | non |  | `'BLANK'::character varying` |  |
| `version_label` | varchar(20) | non |  | `'v1'::character varying` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `knowledge_nodes`

20 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('knowledge_nodes_id_seq'::regcla` |  |
| `uuid` | uuid | non | UK | `gen_random_uuid()` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `brain_id` | int8 | oui | FK → `brain_workspaces.id` |  | CASCADE |
| `type` | varchar(40) | non |  |  |  |
| `domain` | varchar(40) | non |  |  |  |
| `title` | varchar(300) | non |  |  |  |
| `content` | text | oui |  |  |  |
| `content_url` | varchar(1000) | oui |  |  |  |
| `status` | varchar(20) | non |  | `'ACTIVE'::character varying` |  |
| `version_label` | varchar(20) | non |  | `'v1'::character varying` |  |
| `ref_type` | varchar(20) | oui |  |  |  |
| `ref_id` | int8 | oui |  |  |  |
| `metadata` | jsonb | non |  | `'{}'::jsonb` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |
| `embedding` | vector | oui |  |  |  |
| `parent_node_id` | int8 | oui | FK → `knowledge_nodes.id` |  | SET NULL |

### `knowledge_edges`

9 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('knowledge_edges_id_seq'::regcla` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `from_node_id` | int8 | non | FK → `knowledge_nodes.id`, UK |  | CASCADE |
| `to_node_id` | int8 | non | FK → `knowledge_nodes.id`, UK |  | CASCADE |
| `relation_type` | varchar(40) | non | UK |  |  |
| `weight` | float8 | non |  | `1.0` |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `auto` | bool | non |  | `false` |  |

### `analysis_job`

16 colonnes · 4 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('analysis_job_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `project_id` | int8 | non | FK → `projects.id` |  | CASCADE |
| `user_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `depth` | varchar(8) | non |  | `'QUICK'::character varying` |  |
| `status` | varchar(24) | non |  | `'QUEUED'::character varying` |  |
| `plan_json` | text | non |  | `'[]'::text` |  |
| `question` | text | oui |  |  |  |
| `answer` | text | oui |  |  |  |
| `error` | text | oui |  |  |  |
| `brief_id` | int8 | oui | FK → `decision_brief.id` |  | SET NULL |
| `dismissed` | bool | non |  | `false` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `decision_brief`

16 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('decision_brief_id_seq'::regclas` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `project_id` | int8 | non | FK → `projects.id` |  | CASCADE |
| `situation` | text | non |  | `''::text` |  |
| `risks_json` | text | non |  | `'[]'::text` |  |
| `snapshot_total` | int8 | non |  | `0` |  |
| `snapshot_open` | int8 | non |  | `0` |  |
| `snapshot_in_progress` | int8 | non |  | `0` |  |
| `snapshot_completed` | int8 | non |  | `0` |  |
| `snapshot_overdue` | int8 | non |  | `0` |  |
| `snapshot_due_soon` | int8 | non |  | `0` |  |
| `mode` | varchar(16) | non |  | `'generated'::character varying` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `decision_priority`

12 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('decision_priority_id_seq'::regc` |  |
| `brief_id` | int8 | non | FK → `decision_brief.id` |  | CASCADE |
| `level` | varchar(8) | non |  | `'MEDIUM'::character varying` |  |
| `title` | varchar(500) | non |  |  |  |
| `rationale` | text | non |  | `''::text` |  |
| `status` | varchar(16) | non |  | `'NEW'::character varying` |  |
| `issue_id` | int8 | oui | FK → `issues.id` |  | SET NULL |
| `position` | int4 | non |  | `0` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `saved_chart`

9 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('saved_chart_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `title` | varchar(200) | non |  |  |  |
| `spec_json` | text | non |  |  |  |
| `created_by_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

## 4.4 Authentification et sécurité

L'identité est déléguée à Keycloak. Ne subsistent ici que les données propres à l'application : codes à usage unique, jetons anti-CSRF, journal d'audit.

### `otp_verification`

17 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | uuid | non | PK | `uuid_generate_v4()` |  |
| `user_id` | int8 | oui | FK → `users.id` |  | CASCADE |
| `otp_code` | varchar(10) | non |  |  |  |
| `otp_type` | varchar(30) | non |  |  |  |
| `otp_status` | varchar(20) | non |  | `'PENDING'::otp_status` |  |
| `email` | varchar(255) | non |  |  |  |
| `attempts` | int4 | non |  | `0` |  |
| `max_attempts` | int4 | non |  | `5` |  |
| `expires_at` | timestamp | non |  |  |  |
| `verified_at` | timestamp | oui |  |  |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `keycloak_id` | varchar(100) | oui |  |  |  |
| `plan_type` | varchar(20) | oui |  |  |  |
| `company_name` | varchar(255) | oui |  |  |  |
| `phone_number` | varchar(20) | oui |  |  |  |
| `enterprise_message` | text | oui |  |  |  |

### `oauth_states`

6 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `state` | varchar(64) | non | PK |  |  |
| `provider` | varchar(32) | non |  |  |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `user_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `created_at` | timestamp | non |  | `now()` |  |
| `expires_at` | timestamp | non |  |  |  |

### `audit_logs`

9 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('audit_logs_id_seq'::regclass)` |  |
| `workspace_id` | int8 | oui | FK → `workspaces.id` |  | SET NULL |
| `actor_user_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `action` | varchar(64) | non |  |  |  |
| `entity_type` | varchar(64) | oui |  |  |  |
| `entity_id` | varchar(64) | oui |  |  |  |
| `details` | text | oui |  |  |  |
| `ip_address` | varchar(45) | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

## 4.5 Facturation

Abonnements et historique. Aucune donnée de carte n'est stockée : la facturation est déléguée au prestataire de paiement.

### `subscriptions`

19 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('subscriptions_id_seq'::regclass` |  |
| `user_id` | int8 | non | FK → `users.id`, UK |  | CASCADE |
| `plan_type` | varchar(20) | non |  |  |  |
| `status` | vector | non |  | `'ACTIVE'::plan_status` |  |
| `stripe_subscription_id` | varchar(100) | oui | UK |  |  |
| `stripe_customer_id` | varchar(100) | oui |  |  |  |
| `stripe_price_id` | varchar(100) | oui |  |  |  |
| `amount` | numeric | oui |  |  |  |
| `currency` | varchar(3) | oui |  | `'EUR'::character varying` |  |
| `billing_interval` | varchar(20) | oui |  |  |  |
| `current_period_start` | timestamp | oui |  |  |  |
| `current_period_end` | timestamp | oui |  |  |  |
| `trial_end` | timestamp | oui |  |  |  |
| `cancel_at_period_end` | bool | non |  | `false` |  |
| `canceled_at` | timestamp | oui |  |  |  |
| `started_at` | timestamp | oui |  |  |  |
| `ended_at` | timestamp | oui |  |  |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |

### `subscription_history`

14 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | uuid | non | PK | `uuid_generate_v4()` |  |
| `user_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `plan_type` | varchar(20) | non |  |  |  |
| `plan_status` | vector | non |  |  |  |
| `stripe_subscription_id` | varchar(255) | oui |  |  |  |
| `stripe_invoice_id` | varchar(255) | oui |  |  |  |
| `amount_paid` | numeric | oui |  |  |  |
| `currency` | varchar(3) | oui |  | `'EUR'::character varying` |  |
| `period_start` | timestamp | oui |  |  |  |
| `period_end` | timestamp | oui |  |  |  |
| `event_type` | varchar(100) | non |  |  |  |
| `event_data` | jsonb | oui |  |  |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `stripe_event_id` | varchar(100) | oui |  |  |  |

## 4.6 Intégrations et communications

Connecteurs externes et notifications. Les identifiants de connecteurs sont chiffrés en base (AES-256-GCM).

### `integrations`

7 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('integrations_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id`, UK |  | CASCADE |
| `provider` | varchar(32) | non | UK |  |  |
| `access_token` | text | non |  |  |  |
| `meta` | jsonb | non |  | `'{}'::jsonb` |  |
| `installed_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `connected_at` | timestamp | non |  | `now()` |  |

### `connector_connection`

9 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('connector_connection_id_seq'::r` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `connector_key` | varchar(64) | non |  |  |  |
| `config` | text | non |  | `'{}'::text` |  |
| `connected_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `webhooks`

10 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('webhooks_id_seq'::regclass)` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `url` | varchar(512) | non |  |  |  |
| `secret` | varchar(128) | oui |  |  |  |
| `event_types` | ARRAY | non |  | `'{}'::text[]` |  |
| `active` | bool | non |  | `true` |  |
| `last_fired_at` | timestamp | oui |  |  |  |
| `last_status` | int4 | oui |  |  |  |
| `created_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `created_at` | timestamp | non |  | `now()` |  |

### `slack_channels`

7 colonnes · 1 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('slack_channels_id_seq'::regclas` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `channel_id` | varchar(64) | non |  |  |  |
| `channel_name` | varchar(128) | non |  |  |  |
| `event_types` | ARRAY | non |  | `'{}'::text[]` |  |
| `active` | bool | non |  | `true` |  |
| `created_at` | timestamp | non |  | `now()` |  |

### `issue_github_links`

12 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('issue_github_links_id_seq'::reg` |  |
| `issue_id` | int8 | non | FK → `issues.id` |  | CASCADE |
| `link_type` | varchar(16) | non |  |  |  |
| `repo_full_name` | varchar(255) | non |  |  |  |
| `pr_number` | int4 | oui |  |  |  |
| `pr_url` | varchar(512) | oui |  |  |  |
| `commit_sha` | varchar(40) | oui |  |  |  |
| `commit_url` | varchar(512) | oui |  |  |  |
| `title` | varchar(500) | oui |  |  |  |
| `status` | varchar(16) | non |  | `'OPEN'::character varying` |  |
| `linked_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `linked_at` | timestamp | non |  | `now()` |  |

### `notifications`

15 colonnes · 3 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('notifications_id_seq'::regclass` |  |
| `recipient_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `actor_id` | int8 | oui | FK → `users.id` |  | SET NULL |
| `type` | varchar(50) | non |  |  |  |
| `urgency` | varchar(20) | non |  | `'info'::character varying` |  |
| `read` | bool | non |  | `false` |  |
| `acknowledged` | bool | non |  | `false` |  |
| `title` | varchar(512) | non |  |  |  |
| `body` | text | oui |  |  |  |
| `issue_identifier` | varchar(50) | oui |  |  |  |
| `issue_url` | varchar(512) | oui |  |  |  |
| `project_name` | varchar(255) | oui |  |  |  |
| `project_url` | varchar(512) | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |

## 4.7 Documentation, tableaux de bord et prospects

Pages de documentation collaborative, composition du tableau de bord par utilisateur, et demandes commerciales.

### `pages`

8 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('pages_id_seq'::regclass)` |  |
| `project_id` | int8 | non | FK → `projects.id` |  | CASCADE |
| `created_by` | int8 | oui | FK → `users.id` |  | SET NULL |
| `title` | varchar(500) | non |  |  |  |
| `emoji` | varchar(10) | non |  | `'📄'::character varying` |  |
| `content` | text | oui |  |  |  |
| `created_at` | timestamp | non |  | `now()` |  |
| `updated_at` | timestamp | non |  | `now()` |  |

### `dashboard_cards`

12 colonnes · 2 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | int8 | non | PK | `nextval('dashboard_cards_id_seq'::regcla` |  |
| `workspace_id` | int8 | non | FK → `workspaces.id` |  | CASCADE |
| `user_id` | int8 | non | FK → `users.id` |  | CASCADE |
| `card_type` | varchar(40) | non |  |  |  |
| `title` | varchar(200) | oui |  |  |  |
| `config` | jsonb | non |  | `'{}'::jsonb` |  |
| `time_range` | varchar(10) | oui |  |  |  |
| `position` | int4 | non |  | `0` |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

### `enterprise_inquiries`

16 colonnes · 0 clé(s) étrangère(s).

| Colonne | Type | Nullable | Clés | Défaut | ON DELETE |
|---|---|:--:|---|---|---|
| `id` | uuid | non | PK | `uuid_generate_v4()` |  |
| `full_name` | varchar(255) | non |  |  |  |
| `email` | varchar(255) | non |  |  |  |
| `team_size` | varchar(50) | non |  |  |  |
| `message` | text | oui |  |  |  |
| `status` | varchar(50) | non |  | `'NEW'::character varying` |  |
| `created_account` | bool | oui |  | `false` |  |
| `user_id` | int8 | oui |  |  |  |
| `assigned_to` | varchar(100) | oui |  |  |  |
| `notes` | text | oui |  |  |  |
| `created_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `updated_at` | timestamp | non |  | `CURRENT_TIMESTAMP` |  |
| `contacted_at` | timestamp | oui |  |  |  |
| `converted_at` | timestamp | oui |  |  |  |
| `created_by` | varchar(255) | oui |  |  |  |
| `updated_by` | varchar(255) | oui |  |  |  |

> Voir aussi : [[Modele_Donnees_MCD_MLD]] · [[Table_Reconciliation]].
