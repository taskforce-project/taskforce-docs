---
id: scalabilite-et-robustesse
title: Scalabilite et robustesse - strategie de montee en charge (startup early -> scale)
doc_type: spec
statut: draft
version: 0.1
date: "09/09/2026"
auteur: Pierre MICHEL
tags: [road-to-v2, spec, scalabilite, robustesse, db, postgres, redis, queue, ops]
related:
  - "Agent_Delivery_Pipeline.md"
  - "../02-produit/Infra.md"
  - "../03-architecture/Architecture.md"
---

# Scalabilité et robustesse

> **Principe.** On est **startup early** : on ne sur-ingénierie pas aujourd'hui, mais on **conçoit pour que scaler soit un changement de config/ops, pas une réécriture**. Chaque choix ci-dessous a un **état actuel** (v1) et un **cran suivant** activable a la demande. Objectif : **robuste + scalable**, sans dette prématurée.

## 0. Ce qui existe déja (socle)

| Brique | État | Réf |
|---|---|---|
| **Redis** | rate-limiting (bean eager) + cache dashboard (TTL 5 min) | [[../02-produit/Infra.md]] |
| **Prometheus + Grafana** | supervision infra + métriques produit | [[../02-produit/Infra.md]] |
| **Sauvegardes Postgres** | quotidiennes + rotation 14 + restore | ops/backup |
| **Déploiement 2 VM** | auto-deploy depuis main, rebuild par role | [[../02-produit/Infra.md]] |
| **pgvector** | HNSW, embeddings 1024d, pas de vector DB séparée (choix assumé) | migration V59 |

## 1. Base de données

### 1.1 Vertical d'abord (étape actuelle)

Le plus simple, suffisant maintenant : **grossir l'instance** (RAM/CPU) + **tuning Postgres**.
- Pool de connexions borné (le backend est le seul écrivain) ; ajouter **PgBouncer** (pooling transaction) des qu'on met plusieurs instances backend.
- `shared_buffers` / `work_mem` / `effective_cache_size` calibrés a la RAM.
- **pgvector HNSW** : `m` / `ef_construction` calibrés ; l'index vit en RAM → c'est souvent lui qui dicte le passage au cran suivant.
- Index sur les chemins chauds (workspace_id, project_id, status, assignee_id, created_at).

### 1.2 Read scaling (cran 2)

Charge surtout en **lecture** (dashboards, recherche Brain OS) :
- **Réplica(s) de lecture** : primaire = écritures, réplicas = dashboards + `BrainSearchService`. Routage read/write au niveau datasource.
- Le **cache Redis** existant absorbe déja les lectures chaudes (dashboard) ; l'étendre aux vues coûteuses.

### 1.3 Partition / shard (cran 3, seulement si besoin)

Quand une table chauffe (issues, `assignment_events`, `ai_usage`, événements de délégation) :
- **Partition** par `workspace_id` ou par **temps** (events/usage = time-series → partition mensuelle + purge/rotation, réutilise le patron rétention existant).
- **Shard** par workspace **en dernier recours** (le modele est déja workspace-scopé → le sharding logique est naturel, mais on ne le fait que contraint).

### 1.4 pgvector a l'échelle

pgvector reste le défaut (assumé). Si le volume d'embeddings explose : index séparé / table dédiée / réplica vectoriel avant d'envisager un store vectoriel externe. **Ne pas** migrer par anticipation.

## 2. Application (backend Spring)

- **Backend stateless** → **scale horizontal** derriere un load-balancer (N instances). Prérequis déja OK : rate-limit et sessions **externalisés dans Redis**, JWT stateless.
- **WebSocket / STOMP** (notifications, streaming des jobs) : nécessite **sticky sessions** OU un **relais de broker** (Redis/RabbitMQ) pour diffuser entre instances. A prévoir avant le multi-instance.
- **Travail async** : aujourd'hui `@Async` **in-process** (analysis, ingestion). Pour scaler + survivre aux redéploiements → passer a une **file durable** (cf. §3).

## 3. Concurrence des runs de délégation (le point clé)

Les runs d'agent sont **longs (minutes)** et **externes** (dans le cloud du provider, cf. [[Agent_Delivery_Pipeline]] D2). **Notre** charge = **orchestration** (dispatch + poll/webhook + persist), pas le calcul. Le sujet n'est donc pas le CPU mais le **nombre de runs suivis en parallele** + l'ingestion d'événements.

Conception :
- **File durable** (pas en mémoire) : DB-backed ou Redis Streams. Un run survit a un restart backend.
- **Concurrence bornée par workspace/plan** : backpressure (FREE < BASIC < BUSINESS), file d'attente au-dela.
- **Idempotence** : dédup des événements par id (déja fait pour les webhooks Stripe → meme patron).
- **Timeouts + retries + backoff** sur les APIs providers ; **dead-letter** pour les runs échoués.
- **Poll adaptatif** (les providers cloud n'émettent pas tous un webhook) : intervalle croissant, borné.
- **Circuit breaker** par provider (si Anthropic/Cursor/GitHub down → dégradation propre, pas de cascade).

> Comme l'exécution est **hors de notre infra**, on scale **beaucoup de runs légers** (état + événements), pas des conteneurs d'agents. C'est la bonne nouvelle du choix D2.

## 4. Robustesse (transverse)

- **Fail-open la ou c'est sur** (déja le cas : rate-limit sans Redis, LLM absent → repli déterministe).
- **Observabilité** : réutiliser Prometheus/Grafana → métriques de runs (durée, taux d'échec, file d'attente, conso providers).
- **Sauvegardes + restore** déja en place ; ajouter les nouvelles tables (runs, events) au périmetre.
- **Migrations Flyway** disciplinées (jamais éditer une migration appliquée).

## 5. Progression (staged, ne rien faire d'avance)

| Palier | Déclencheur | Action |
|---|---|---|
| **P0 (actuel)** | bêta, faible charge | vertical + tuning + Redis cache |
| **P1** | lectures qui chauffent | PgBouncer + réplica lecture ; file durable pour les runs |
| **P2** | trafic multi-instance | backend horizontal + relais STOMP (Redis) |
| **P3** | table(s) chaude(s) | partition time-series (events/usage) + purge |
| **P4** | très gros workspace | shard par workspace (dernier recours) |

## 6. Regle

> **On ne construit pas P3/P4 maintenant.** On **conçoit** pour qu'ils soient activables (backend stateless, workspace-scopé, events partitionnables, runs en file durable). Le coût d'aujourd'hui = quelques bonnes frontieres ; le bénéfice = **scaler sans réécrire**.
