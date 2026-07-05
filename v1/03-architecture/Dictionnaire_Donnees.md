---
id: dictionnaire-donnees
title: Dictionnaire de données — schéma PostgreSQL réel
doc_type: reference
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [dictionnaire, donnees, schema, postgresql, sql, reference, merise, mpd, memoire, rncp]
---

# 📚 Dictionnaire de données — schéma PostgreSQL réel

> **But** : référence exhaustive de **toutes** les tables, colonnes, types, contraintes et clés
> étrangères du schéma **réellement déployé** (MPD MERISE — voir [[Modele_Donnees_MCD_MLD]]).
>
> **Génération** : extrait **automatiquement** de `information_schema` sur la base
> `taskforce-db` (Postgres 18 + pgvector), à la date du **05/07/2026**. Aucune colonne inventée :
> ce document est un miroir du schéma produit par les migrations Flyway.
>
> **Périmètre** : **50 tables**, **483 colonnes**, **94 clés étrangères** (hors `flyway_schema_history`).
> Groupé par domaine fonctionnel (même découpage que le [[Modele_Donnees_MCD_MLD|MCD/MLD]]).

## Légende

| Symbole | Signification |
|---|---|
| **Null = —** | `NOT NULL` (obligatoire) |
| **Null = ✓** | colonne nullable |
| 🔑 **PK** | clé primaire |
| **FK** | clé étrangère (cible + règle `ON DELETE` en dernière colonne) |
| **U** | contrainte d'unicité |
| `seq` | défaut = séquence auto-incrément (`nextval`) |

> ℹ️ Les types `enum` correspondent à des types PostgreSQL `USER-DEFINED` (mappés depuis les enums Java
> `@Enumerated(STRING)`, cf. [[Diagramme_Etats_UML]]). `vector` = colonne pgvector (embeddings IA).

---

## IAM & Workspace

### `companies`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `name` | varchar(255) | — |  |  |  |
| 3 | `email` | varchar(255) | ✓ |  |  |  |
| 4 | `phone` | varchar(50) | ✓ |  |  |  |
| 5 | `address` | text | ✓ |  |  |  |
| 6 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 7 | `updated_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 8 | `created_by` | varchar(255) | ✓ |  |  |  |
| 9 | `updated_by` | varchar(255) | ✓ |  |  |  |

### `users` — Table des utilisateurs avec intégration Keycloak et Stripe

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `keycloak_id` | varchar(255) | — |  | U |  |
| 3 | `email` | varchar(255) | — |  | U |  |
| 4 | `company_id` | bigint | ✓ |  | FK | → `companies` (ON DELETE SET NULL) |
| 5 | `is_active` | boolean | — | `true` |  |  |
| 6 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 7 | `updated_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 8 | `created_by` | varchar(255) | ✓ |  |  |  |
| 9 | `updated_by` | varchar(255) | ✓ |  |  |  |
| 10 | `plan_type` | varchar(20) | — |  |  |  |
| 11 | `plan_status` | enum | ✓ |  |  |  |
| 12 | `stripe_customer_id` | varchar(255) | ✓ |  | U |  |
| 13 | `stripe_subscription_id` | varchar(255) | ✓ |  | U |  |
| 14 | `subscription_start_date` | timestamp | ✓ |  |  |  |
| 15 | `subscription_end_date` | timestamp | ✓ |  |  |  |
| 16 | `trial_end_date` | timestamp | ✓ |  |  |  |
| 17 | `enterprise_interest` | boolean | ✓ | `false` |  |  |
| 18 | `display_name` | varchar(150) | ✓ |  |  |  |
| 19 | `avatar_url` | varchar(500) | ✓ |  |  |  |

### `workspaces`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `name` | varchar(100) | — |  |  |  |
| 3 | `slug` | varchar(100) | — |  | U |  |
| 4 | `description` | varchar(500) | ✓ |  |  |  |
| 5 | `logo_url` | varchar(1000) | ✓ |  |  |  |
| 6 | `owner_id` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 7 | `created_at` | timestamp | — | `now()` |  |  |
| 8 | `updated_at` | timestamp | — | `now()` |  |  |
| 9 | `uuid` | uuid | — | `uuid_generate_v4()` | U |  |

### `workspace_members`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 4 | `role` | varchar(20) | — | `'MEMBER'` |  |  |
| 5 | `invited_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 6 | `joined_at` | timestamp | — | `now()` |  |  |

### `workspace_invitations`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `invited_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `email` | varchar(255) | — |  |  |  |
| 5 | `role` | varchar(20) | — | `'MEMBER'` |  |  |
| 6 | `token` | varchar(100) | — |  | U |  |
| 7 | `status` | varchar(20) | — | `'PENDING'` |  |  |
| 8 | `expires_at` | timestamp | — |  |  |  |
| 9 | `accepted_at` | timestamp | ✓ |  |  |  |
| 10 | `created_at` | timestamp | — | `now()` |  |  |
| 11 | `updated_at` | timestamp | — | `now()` |  |  |
| 12 | `created_by` | varchar(255) | ✓ |  |  |  |
| 13 | `updated_by` | varchar(255) | ✓ |  |  |  |

### `teams`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `created_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `name` | varchar(200) | — |  |  |  |
| 5 | `description` | text | ✓ |  |  |  |
| 6 | `emoji` | varchar(10) | — | `'👥'` |  |  |
| 7 | `color` | varchar(50) | — | `'bg-primary'` |  |  |
| 8 | `created_at` | timestamp | — | `now()` |  |  |
| 9 | `updated_at` | timestamp | — | `now()` |  |  |

### `team_members`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `team_id` | bigint | — |  | FK U | → `teams` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 4 | `role` | varchar(20) | — | `'MEMBER'` |  |  |
| 5 | `joined_at` | timestamp | — | `now()` |  |  |

### `member_leaves`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK | → `users` (ON DELETE CASCADE) |
| 4 | `type` | varchar(20) | — |  |  |  |
| 5 | `start_date` | date | — |  |  |  |
| 6 | `end_date` | date | — |  |  |  |
| 7 | `note` | text | ✓ |  |  |  |
| 8 | `created_at` | timestamp | — | `now()` |  |  |
| 9 | `updated_at` | timestamp | — | `now()` |  |  |
| 10 | `created_by` | varchar(255) | ✓ |  |  |  |
| 11 | `updated_by` | varchar(255) | ✓ |  |  |  |

## Projets & Issues

### `projects`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `name` | varchar(150) | — |  |  |  |
| 4 | `identifier` | varchar(10) | — |  | U |  |
| 5 | `description` | varchar(1000) | ✓ |  |  |  |
| 6 | `status` | enum | — | `'ACTIVE'` |  |  |
| 7 | `is_public` | boolean | — | `false` |  |  |
| 8 | `created_by` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 9 | `created_at` | timestamp | — | `now()` |  |  |
| 10 | `updated_at` | timestamp | — | `now()` |  |  |
| 11 | `icon_url` | text | ✓ |  |  |  |
| 12 | `color` | varchar(50) | — | `'bg-primary'` |  |  |
| 13 | `growth_mode` | boolean | — | `false` |  |  |

### `project_members`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 4 | `role` | enum | — | `'MEMBER'` |  |  |
| 5 | `added_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 6 | `joined_at` | timestamp | — | `now()` |  |  |

### `project_teams`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `team_id` | bigint | — |  | FK U | → `teams` (ON DELETE CASCADE) |
| 4 | `created_at` | timestamp | — | `now()` |  |  |

### `project_labels`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `name` | varchar(50) | — |  | U |  |
| 4 | `color` | varchar(30) | — | `'#6366f1'` |  |  |
| 5 | `description` | varchar(200) | ✓ |  |  |  |
| 6 | `created_at` | timestamp | — | `now()` |  |  |

### `project_favorites`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 3 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 4 | `created_at` | timestamp | — | `now()` |  |  |

### `cycles`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `name` | varchar(255) | — |  | U |  |
| 4 | `description` | text | ✓ |  |  |  |
| 5 | `start_date` | date | ✓ |  |  |  |
| 6 | `end_date` | date | ✓ |  |  |  |
| 7 | `status` | enum | — | `'DRAFT'` |  |  |
| 8 | `created_by` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 9 | `created_at` | timestamp | — | `now()` |  |  |
| 10 | `updated_at` | timestamp | — | `now()` |  |  |

### `cycle_issues`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `cycle_id` | bigint | — |  | FK U | → `cycles` (ON DELETE CASCADE) |
| 3 | `issue_id` | bigint | — |  | FK U | → `issues` (ON DELETE CASCADE) |
| 4 | `added_by` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 5 | `added_at` | timestamp | — | `now()` |  |  |

### `pages`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK | → `projects` (ON DELETE CASCADE) |
| 3 | `created_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `title` | varchar(500) | — |  |  |  |
| 5 | `emoji` | varchar(10) | — | `'📄'` |  |  |
| 6 | `content` | text | ✓ |  |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |
| 8 | `updated_at` | timestamp | — | `now()` |  |  |

### `issues`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `sequence_number` | integer | — |  | U |  |
| 4 | `title` | varchar(500) | — |  |  |  |
| 5 | `description` | text | ✓ |  |  |  |
| 6 | `priority` | enum | — | `'NONE'` |  |  |
| 7 | `status_id` | bigint | — |  | FK | → `issue_statuses` (ON DELETE RESTRICT) |
| 8 | `type_id` | bigint | ✓ |  | FK | → `issue_types` (ON DELETE SET NULL) |
| 9 | `assignee_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 10 | `reporter_id` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 11 | `parent_id` | bigint | ✓ |  | FK | → `issues` (ON DELETE SET NULL) |
| 12 | `start_date` | date | ✓ |  |  |  |
| 13 | `due_date` | date | ✓ |  |  |  |
| 14 | `completed_at` | timestamp | ✓ |  |  |  |
| 15 | `created_at` | timestamp | — | `now()` |  |  |
| 16 | `updated_at` | timestamp | — | `now()` |  |  |
| 17 | `position` | integer | — | `0` |  |  |
| 18 | `story_points` | integer | ✓ |  |  |  |
| 19 | `archived_at` | timestamp | ✓ |  |  |  |
| 20 | `pinned` | boolean | — | `false` |  |  |

### `issue_statuses`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `name` | varchar(50) | — |  | U |  |
| 4 | `color` | varchar(30) | — | `'#6366f1'` |  |  |
| 5 | `category` | enum | — |  |  |  |
| 6 | `position` | smallint | — | `0` |  |  |
| 7 | `is_default` | boolean | — | `false` |  |  |
| 8 | `created_at` | timestamp | — | `now()` |  |  |

### `issue_types`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `project_id` | bigint | — |  | FK U | → `projects` (ON DELETE CASCADE) |
| 3 | `name` | varchar(50) | — |  | U |  |
| 4 | `color` | varchar(30) | — | `'#6366f1'` |  |  |
| 5 | `icon` | varchar(50) | — | `'circle-dot'` |  |  |
| 6 | `is_default` | boolean | — | `false` |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |

### `issue_label_assignments`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `issue_id` | bigint | — |  | 🔑 PK FK | → `issues` (ON DELETE CASCADE) |
| 2 | `label_id` | bigint | — |  | 🔑 PK FK | → `project_labels` (ON DELETE CASCADE) |

### `issue_comments`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `author_id` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 4 | `content` | text | — |  |  |  |
| 5 | `is_edited` | boolean | — | `false` |  |  |
| 6 | `created_at` | timestamp | — | `now()` |  |  |
| 7 | `updated_at` | timestamp | — | `now()` |  |  |

### `issue_activity`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `actor_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `action` | enum | — |  |  |  |
| 5 | `old_value` | varchar(500) | ✓ |  |  |  |
| 6 | `new_value` | varchar(500) | ✓ |  |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |

### `issue_checklist_items`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `content` | varchar(500) | — |  |  |  |
| 4 | `is_done` | boolean | — | `false` |  |  |
| 5 | `position` | integer | — | `0` |  |  |
| 6 | `created_at` | timestamp | — | `now()` |  |  |
| 7 | `updated_at` | timestamp | — | `now()` |  |  |

### `issue_relations`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `source_id` | bigint | — |  | FK U | → `issues` (ON DELETE CASCADE) |
| 3 | `target_id` | bigint | — |  | FK U | → `issues` (ON DELETE CASCADE) |
| 4 | `relation_type` | enum | — |  | U |  |
| 5 | `created_by` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 6 | `created_at` | timestamp | — | `now()` |  |  |

### `issue_worklogs`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK | → `users` (ON DELETE CASCADE) |
| 4 | `minutes` | integer | — |  |  |  |
| 5 | `description` | varchar(500) | ✓ |  |  |  |
| 6 | `logged_at` | date | — |  |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |

### `issue_sequence_counters`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `project_id` | bigint | — |  | 🔑 PK FK | → `projects` (ON DELETE CASCADE) |
| 2 | `last_number` | integer | — | `0` |  |  |

### `issue_github_links`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `link_type` | varchar(16) | — |  |  |  |
| 4 | `repo_full_name` | varchar(255) | — |  |  |  |
| 5 | `pr_number` | integer | ✓ |  |  |  |
| 6 | `pr_url` | varchar(512) | ✓ |  |  |  |
| 7 | `commit_sha` | varchar(40) | ✓ |  |  |  |
| 8 | `commit_url` | varchar(512) | ✓ |  |  |  |
| 9 | `title` | varchar(500) | ✓ |  |  |  |
| 10 | `status` | varchar(16) | — | `'OPEN'` |  |  |
| 11 | `linked_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 12 | `linked_at` | timestamp | — | `now()` |  |  |

## IA / Smart Assign / Brain OS

### `member_skill_profiles`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 4 | `profile_text` | text | ✓ |  |  |  |
| 5 | `skills_json` | jsonb | — | `'{}'` |  |  |
| 6 | `stats_json` | jsonb | — | `'{}'` |  |  |
| 7 | `embedding` | enum | ✓ |  |  |  |
| 8 | `updated_at` | timestamp | — | `now()` |  |  |
| 9 | `capacity_hours_per_week` | integer | ✓ |  |  |  |
| 10 | `seniority` | varchar(20) | ✓ |  |  |  |
| 11 | `growth_enabled` | boolean | — | `false` |  |  |
| 12 | `growth_target_skills` | jsonb | — | `'[]'` |  |  |

### `assignment_events`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `issue_id` | bigint | ✓ |  | FK | → `issues` (ON DELETE SET NULL) |
| 4 | `assignee_user_id` | bigint | — |  | FK | → `users` (ON DELETE RESTRICT) |
| 5 | `assigned_by_user_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 6 | `decision_source` | varchar(32) | — |  |  |  |
| 7 | `accepted` | boolean | ✓ |  |  |  |
| 8 | `resolved_successfully` | boolean | ✓ |  |  |  |
| 9 | `features_json` | jsonb | — | `'{}'` |  |  |
| 10 | `created_at` | timestamp | — | `now()` |  |  |

### `ai_runs`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `feature_name` | varchar(64) | — |  |  |  |
| 4 | `provider` | varchar(32) | — |  |  |  |
| 5 | `model_name` | varchar(128) | — |  |  |  |
| 6 | `latency_ms` | integer | ✓ |  |  |  |
| 7 | `input_tokens` | integer | ✓ |  |  |  |
| 8 | `output_tokens` | integer | ✓ |  |  |  |
| 9 | `status` | varchar(32) | — |  |  |  |
| 10 | `fallback_used` | boolean | — | `false` |  |  |
| 11 | `request_hash` | varchar(128) | ✓ |  |  |  |
| 12 | `meta_json` | jsonb | — | `'{}'` |  |  |
| 13 | `created_at` | timestamp | — | `now()` |  |  |
| 14 | `expires_at` | timestamp | — | `(now() + '90 days')` |  |  |

### `ai_documents`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `source_type` | varchar(32) | — |  | U |  |
| 4 | `source_id` | bigint | — |  | U |  |
| 5 | `chunk_index` | integer | — | `0` | U |  |
| 6 | `title` | varchar(500) | ✓ |  |  |  |
| 7 | `content` | text | — |  |  |  |
| 8 | `metadata_json` | jsonb | — | `'{}'` |  |  |
| 9 | `embedding` | enum | ✓ |  |  |  |
| 10 | `created_at` | timestamp | — | `now()` |  |  |
| 11 | `updated_at` | timestamp | — | `now()` |  |  |

### `ai_insight_snapshots`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `snapshot_date` | date | — |  | U |  |
| 4 | `summary_text` | text | ✓ |  |  |  |
| 5 | `exceptions_json` | jsonb | — | `'[]'` |  |  |
| 6 | `agents_json` | jsonb | — | `'[]'` |  |  |
| 7 | `source_metrics_json` | jsonb | — | `'{}'` |  |  |
| 8 | `created_at` | timestamp | — | `now()` |  |  |
| 9 | `expires_at` | timestamp | — | `(now() + '180 days')` |  |  |

### `brain_workspaces`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `template_type` | varchar(40) | — | `'BLANK'` |  |  |
| 4 | `version_label` | varchar(20) | — | `'v1'` |  |  |
| 5 | `created_at` | timestamp | — | `now()` |  |  |
| 6 | `updated_at` | timestamp | — | `now()` |  |  |
| 7 | `created_by` | varchar(255) | ✓ |  |  |  |
| 8 | `updated_by` | varchar(255) | ✓ |  |  |  |

### `knowledge_nodes`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `uuid` | uuid | — | `gen_random_uuid()` | U |  |
| 3 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 4 | `brain_id` | bigint | ✓ |  | FK | → `brain_workspaces` (ON DELETE CASCADE) |
| 5 | `type` | varchar(40) | — |  |  |  |
| 6 | `domain` | varchar(40) | — |  |  |  |
| 7 | `title` | varchar(300) | — |  |  |  |
| 8 | `content` | text | ✓ |  |  |  |
| 9 | `content_url` | varchar(1000) | ✓ |  |  |  |
| 10 | `status` | varchar(20) | — | `'ACTIVE'` |  |  |
| 11 | `version_label` | varchar(20) | — | `'v1'` |  |  |
| 12 | `ref_type` | varchar(20) | ✓ |  |  |  |
| 13 | `ref_id` | bigint | ✓ |  |  |  |
| 14 | `metadata` | jsonb | — | `'{}'` |  |  |
| 15 | `created_at` | timestamp | — | `now()` |  |  |
| 16 | `updated_at` | timestamp | — | `now()` |  |  |
| 17 | `created_by` | varchar(255) | ✓ |  |  |  |
| 18 | `updated_by` | varchar(255) | ✓ |  |  |  |
| 19 | `embedding` | enum | ✓ |  |  |  |
| 20 | `parent_node_id` | bigint | ✓ |  | FK | → `knowledge_nodes` (ON DELETE SET NULL) |

### `knowledge_edges`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `from_node_id` | bigint | — |  | FK U | → `knowledge_nodes` (ON DELETE CASCADE) |
| 4 | `to_node_id` | bigint | — |  | FK U | → `knowledge_nodes` (ON DELETE CASCADE) |
| 5 | `relation_type` | varchar(40) | — |  | U |  |
| 6 | `weight` | double | — | `1.0` |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |
| 8 | `created_by` | varchar(255) | ✓ |  |  |  |
| 9 | `auto` | boolean | — | `false` |  |  |

## Auth & Securite

### `refresh_tokens` — Tokens de rafraîchissement JWT pour renouveler l'accès sans reconnexion

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | uuid | — | `uuid_generate_v4()` | 🔑 PK |  |
| 2 | `user_id` | bigint | — |  | FK | → `users` (ON DELETE CASCADE) |
| 3 | `token` | varchar(500) | — |  | U |  |
| 4 | `expires_at` | timestamp | — |  |  |  |
| 5 | `revoked` | boolean | — | `false` |  |  |
| 6 | `revoked_at` | timestamp | ✓ |  |  |  |
| 7 | `ip_address` | varchar(45) | ✓ |  |  |  |
| 8 | `user_agent` | varchar(500) | ✓ |  |  |  |
| 9 | `last_used_at` | timestamp | ✓ |  |  |  |
| 10 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |

### `otp_verification` — Codes OTP pour vérification email et réinitialisation mot de passe

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | uuid | — | `uuid_generate_v4()` | 🔑 PK |  |
| 2 | `user_id` | bigint | ✓ |  | FK | → `users` (ON DELETE CASCADE) |
| 3 | `otp_code` | varchar(10) | — |  |  |  |
| 4 | `otp_type` | varchar(30) | — |  |  |  |
| 5 | `otp_status` | varchar(20) | — | `'PENDING'` |  |  |
| 6 | `email` | varchar(255) | — |  |  |  |
| 7 | `attempts` | integer | — | `0` |  |  |
| 8 | `max_attempts` | integer | — | `5` |  |  |
| 9 | `expires_at` | timestamp | — |  |  |  |
| 10 | `verified_at` | timestamp | ✓ |  |  |  |
| 11 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 12 | `updated_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 13 | `keycloak_id` | varchar(100) | ✓ |  |  |  |
| 14 | `plan_type` | varchar(20) | ✓ |  |  |  |
| 15 | `company_name` | varchar(255) | ✓ |  |  |  |
| 16 | `phone_number` | varchar(20) | ✓ |  |  |  |
| 17 | `enterprise_message` | text | ✓ |  |  |  |

### `audit_logs`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | ✓ |  | FK | → `workspaces` (ON DELETE SET NULL) |
| 3 | `actor_user_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `action` | varchar(64) | — |  |  |  |
| 5 | `entity_type` | varchar(64) | ✓ |  |  |  |
| 6 | `entity_id` | varchar(64) | ✓ |  |  |  |
| 7 | `details` | text | ✓ |  |  |  |
| 8 | `ip_address` | varchar(45) | ✓ |  |  |  |
| 9 | `created_at` | timestamp | — | `now()` |  |  |

## Facturation

### `subscriptions` — Abonnements actifs des utilisateurs avec détails Stripe

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `user_id` | bigint | — |  | FK U | → `users` (ON DELETE CASCADE) |
| 3 | `plan_type` | varchar(20) | — |  |  |  |
| 4 | `status` | enum | — | `'ACTIVE'` |  |  |
| 5 | `stripe_subscription_id` | varchar(100) | ✓ |  | U |  |
| 6 | `stripe_customer_id` | varchar(100) | ✓ |  |  |  |
| 7 | `stripe_price_id` | varchar(100) | ✓ |  |  |  |
| 8 | `amount` | numeric(10,2) | ✓ |  |  |  |
| 9 | `currency` | varchar(3) | ✓ | `'EUR'` |  |  |
| 10 | `billing_interval` | varchar(20) | ✓ |  |  |  |
| 11 | `current_period_start` | timestamp | ✓ |  |  |  |
| 12 | `current_period_end` | timestamp | ✓ |  |  |  |
| 13 | `trial_end` | timestamp | ✓ |  |  |  |
| 14 | `cancel_at_period_end` | boolean | — | `false` |  |  |
| 15 | `canceled_at` | timestamp | ✓ |  |  |  |
| 16 | `started_at` | timestamp | ✓ |  |  |  |
| 17 | `ended_at` | timestamp | ✓ |  |  |  |
| 18 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 19 | `updated_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |

### `subscription_history` — Historique de tous les événements liés aux abonnements

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | uuid | — | `uuid_generate_v4()` | 🔑 PK |  |
| 2 | `user_id` | bigint | — |  | FK | → `users` (ON DELETE CASCADE) |
| 3 | `plan_type` | varchar(20) | — |  |  |  |
| 4 | `plan_status` | enum | — |  |  |  |
| 5 | `stripe_subscription_id` | varchar(255) | ✓ |  |  |  |
| 6 | `stripe_invoice_id` | varchar(255) | ✓ |  |  |  |
| 7 | `amount_paid` | numeric(10,2) | ✓ |  |  |  |
| 8 | `currency` | varchar(3) | ✓ | `'EUR'` |  |  |
| 9 | `period_start` | timestamp | ✓ |  |  |  |
| 10 | `period_end` | timestamp | ✓ |  |  |  |
| 11 | `event_type` | varchar(100) | — |  |  |  |
| 12 | `event_data` | jsonb | ✓ |  |  |  |
| 13 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 14 | `stripe_event_id` | varchar(100) | ✓ |  |  |  |

## Integrations & Comms

### `integrations`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK U | → `workspaces` (ON DELETE CASCADE) |
| 3 | `provider` | varchar(32) | — |  | U |  |
| 4 | `access_token` | text | — |  |  |  |
| 5 | `meta` | jsonb | — | `'{}'` |  |  |
| 6 | `installed_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 7 | `connected_at` | timestamp | — | `now()` |  |  |

### `webhooks`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `url` | varchar(512) | — |  |  |  |
| 4 | `secret` | varchar(128) | ✓ |  |  |  |
| 5 | `event_types` | array | — | `'{}'[]` |  |  |
| 6 | `active` | boolean | — | `true` |  |  |
| 7 | `last_fired_at` | timestamp | ✓ |  |  |  |
| 8 | `last_status` | integer | ✓ |  |  |  |
| 9 | `created_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 10 | `created_at` | timestamp | — | `now()` |  |  |

### `slack_channels`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `channel_id` | varchar(64) | — |  |  |  |
| 4 | `channel_name` | varchar(128) | — |  |  |  |
| 5 | `event_types` | array | — | `'{}'[]` |  |  |
| 6 | `active` | boolean | — | `true` |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |

### `channels`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `project_id` | bigint | ✓ |  | FK | → `projects` (ON DELETE SET NULL) |
| 4 | `kind` | varchar(20) | — | `'CHANNEL'` |  |  |
| 5 | `name` | varchar(100) | ✓ |  |  |  |
| 6 | `description` | varchar(500) | ✓ |  |  |  |
| 7 | `is_private` | boolean | — | `false` |  |  |
| 8 | `is_archived` | boolean | — | `false` |  |  |
| 9 | `created_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 10 | `created_at` | timestamp | — | `now()` |  |  |
| 11 | `updated_at` | timestamp | — | `now()` |  |  |

### `channel_members`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `channel_id` | bigint | — |  | 🔑 PK FK | → `channels` (ON DELETE CASCADE) |
| 2 | `user_id` | bigint | — |  | 🔑 PK FK | → `users` (ON DELETE CASCADE) |
| 3 | `joined_at` | timestamp | — | `now()` |  |  |

### `chat_messages`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `channel_id` | bigint | — |  | FK | → `channels` (ON DELETE CASCADE) |
| 3 | `author_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `content` | text | — |  |  |  |
| 5 | `is_edited` | boolean | — | `false` |  |  |
| 6 | `is_deleted` | boolean | — | `false` |  |  |
| 7 | `created_at` | timestamp | — | `now()` |  |  |
| 8 | `updated_at` | timestamp | — | `now()` |  |  |

### `discussions`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 3 | `author_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `title` | varchar(500) | — |  |  |  |
| 5 | `body` | text | ✓ |  |  |  |
| 6 | `category` | varchar(20) | — | `'GENERAL'` |  |  |
| 7 | `state` | varchar(20) | — | `'OPEN'` |  |  |
| 8 | `is_pinned` | boolean | — | `false` |  |  |
| 9 | `is_locked` | boolean | — | `false` |  |  |
| 10 | `reply_count` | integer | — | `0` |  |  |
| 11 | `reaction_count` | integer | — | `0` |  |  |
| 12 | `tags` | varchar(500) | ✓ |  |  |  |
| 13 | `created_at` | timestamp | — | `now()` |  |  |
| 14 | `updated_at` | timestamp | — | `now()` |  |  |

### `notifications`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `recipient_id` | bigint | — |  | FK | → `users` (ON DELETE CASCADE) |
| 3 | `workspace_id` | bigint | — |  | FK | → `workspaces` (ON DELETE CASCADE) |
| 4 | `actor_id` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 5 | `type` | varchar(50) | — |  |  |  |
| 6 | `urgency` | varchar(20) | — | `'info'` |  |  |
| 7 | `read` | boolean | — | `false` |  |  |
| 8 | `acknowledged` | boolean | — | `false` |  |  |
| 9 | `title` | varchar(512) | — |  |  |  |
| 10 | `body` | text | ✓ |  |  |  |
| 11 | `issue_identifier` | varchar(50) | ✓ |  |  |  |
| 12 | `issue_url` | varchar(512) | ✓ |  |  |  |
| 13 | `project_name` | varchar(255) | ✓ |  |  |  |
| 14 | `project_url` | varchar(512) | ✓ |  |  |  |
| 15 | `created_at` | timestamp | — | `now()` |  |  |

## GED & Sales

### `attachments`

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | bigint | — | `seq` | 🔑 PK |  |
| 2 | `issue_id` | bigint | — |  | FK | → `issues` (ON DELETE CASCADE) |
| 3 | `uploaded_by` | bigint | ✓ |  | FK | → `users` (ON DELETE SET NULL) |
| 4 | `original_name` | varchar(255) | — |  |  |  |
| 5 | `stored_key` | varchar(512) | — |  | U |  |
| 6 | `content_type` | varchar(128) | — |  |  |  |
| 7 | `file_size` | bigint | — |  |  |  |
| 8 | `created_at` | timestamp | — | `now()` |  |  |

### `enterprise_inquiries` — Demandes de contact pour les plans ENTERPRISE

| # | Colonne | Type | Null | Défaut | Clé | Référence / ON DELETE |
|--:|---|---|:--:|---|---|---|
| 1 | `id` | uuid | — | `uuid_generate_v4()` | 🔑 PK |  |
| 2 | `full_name` | varchar(255) | — |  |  |  |
| 3 | `email` | varchar(255) | — |  |  |  |
| 4 | `team_size` | varchar(50) | — |  |  |  |
| 5 | `message` | text | ✓ |  |  |  |
| 6 | `status` | varchar(50) | — | `'NEW'` |  |  |
| 7 | `created_account` | boolean | ✓ | `false` |  |  |
| 8 | `user_id` | bigint | ✓ |  |  |  |
| 9 | `assigned_to` | varchar(100) | ✓ |  |  |  |
| 10 | `notes` | text | ✓ |  |  |  |
| 11 | `created_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 12 | `updated_at` | timestamp | — | `CURRENT_TIMESTAMP` |  |  |
| 13 | `contacted_at` | timestamp | ✓ |  |  |  |
| 14 | `converted_at` | timestamp | ✓ |  |  |  |
| 15 | `created_by` | varchar(255) | ✓ |  |  |  |
| 16 | `updated_by` | varchar(255) | ✓ |  |  |  |

---

## Notes de traçabilité

- **Source** : `information_schema.columns` / `.table_constraints` / `.referential_constraints`
  (requêtes du 05/07/2026 sur `taskforce-db`).
- **Cohérence** : 94 FK ↔ [[Modele_Donnees_MCD_MLD]] (94 FK) ↔ 60 associations JPA
  [[Diagramme_Classes_UML]] (l'écart = FK par `Long` id non mappées en association, cf. modèle hybride).
- **Évolution** : toute modification passe par une **migration Flyway** (`V*.sql`) ; régénérer ce
  dictionnaire après migration. Ne **jamais** éditer une colonne à la main ici sans migration correspondante.

> 🔗 Voir aussi : [[Modele_Donnees_MCD_MLD]] · [[Diagramme_Classes_UML]] · [[Diagramme_Etats_UML]].
