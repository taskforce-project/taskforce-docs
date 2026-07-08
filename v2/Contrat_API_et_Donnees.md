# Contrat API `backend ↔ ai-service` + Modèle de données IA (v2)

> **Statut : conception (v2, non implémenté).** Spécifie le pont technique entre le **backend Java** (orchestrateur + système de vérité) et le **`ai-service` Python** (cerveau IA : retrieval, LLM, agents, boucle World Model). Support de [[Moteur_IA_World_Model_OODA]], [[Agents_C_Level]], [[Roadmap_v2]] (IA-1/IA-3/IA-5).

---

## 1. Répartition des responsabilités

| | **Backend Java** (`tf-api`) | **`ai-service` Python** (FastAPI) |
|---|---|---|
| Rôle | Orchestrateur, système de vérité, human-in-the-loop, sécurité/authz | Retrieval Brain OS, appels LLM, agents C-level, boucle predict/reflect |
| Possède | tables **app** (projects/issues/cycles/decisions…) | index **Brain OS** (embeddings/nodes/edges) + **expériences** (predict/outcome) |
| Ne fait pas | pas d'appel LLM direct (délègue) | pas d'écriture sur les tables app (renvoie des propositions) |

**Base partagée** : un seul Postgres (**pgvector** déjà là). Le backend possède le schéma app ; l'`ai-service` possède le schéma `brain` (nodes/embeddings/edges/experiences). Chacun écrit **son** schéma.

---

## 2. Transport

- **Synchrone (REST)** : le backend appelle l'`ai-service` en HTTP pour les tâches courtes (retrieve, spec, décision). Réseau Docker interne (`http://ai-service:8000`), **jamais exposé** publiquement.
- **Asynchrone (events)** : pour les tâches longues (run d'agent, réindexation) → **RabbitMQ** (déjà dans la stack). L'`ai-service` publie l'avancement ; le backend relaie en temps réel au front via **STOMP** (déjà là).
- **Auth inter-services** : secret partagé (`AI_SERVICE_TOKEN`) en header + isolation réseau. (mTLS plus tard.)
- **Toujours scopé workspace** : chaque appel porte `workspaceId` ; l'`ai-service` isole le retrieval sur ce brain (1 workspace = 1 brain).

---

## 3. Endpoints `ai-service` (contrat)

| Méthode | Endpoint | Entrée | Sortie | Sert |
|---|---|---|---|---|
| `POST` | `/ai/retrieve` | `{workspaceId, query, k}` | `{chunks[], nodes[], score}` | IA-1 (fondation) |
| `POST` | `/ai/decompose` | `{workspaceId, intention}` | `{cycles[], issues[], predictions}` | CPO (projet→découpage) |
| `POST` | `/ai/spec` | `{workspaceId, issueId, context}` | `{spec, acceptance[], prompt, links[]}` | CPO (issue→spec+prompt) |
| `POST` | `/ai/decide` | `{workspaceId, scope, subjectId, signals}` | `{decisions[]{agent, proposal, prediction, rationale}}` | Agents C-level |
| `POST` | `/ai/reflect` | `{predictionId, observed}` | `{delta, learned}` | Boucle World Model |
| `POST` | `/ai/index` | `{workspaceId, nodes[]}` | `{indexed}` | (ré)indexation Brain OS |
| `GET` | `/ai/health` | — | `{status, model, version}` | ops |

> **Règle d'or** : l'`ai-service` ne renvoie que des **propositions** (decisions/spec/predictions). **Rien n'est appliqué sans validation humaine** côté backend (gate `Act`).

---

## 4. Modèle de données — schéma `brain` (possédé par `ai-service`)

### Retrieval (existe en partie : embeddings V51-56)
- `brain_node` : unité de connaissance (spec, décision, doc, code-summary…) · `workspace_id`, `type`, `content`, `meta`
- `brain_embedding` : `node_id`, `vector` (pgvector), `model` — *existe déjà*
- `brain_edge` : `src`, `dst`, `relation` — graphe (auto-edges + hiérarchie existent)

### World Model — les « expériences » (nouveau)
```
ai_prediction
  id · workspace_id · agent (CPO|CTO|COO) · scope (issue|project|enterprise)
  subject_id · action_proposed (jsonb) · prediction (jsonb: conséquences attendues)
  created_at

ai_outcome
  id · prediction_id → ai_prediction · observed (jsonb: résultat réel)
  delta (jsonb: prédit vs réel) · created_at
```
- Le couple `(prediction, delta)` est **ré-indexé** (embedding sur la situation) → un `Orient` futur **retrouve** les écarts passés similaires → l'agent devient « habile ».
- **Métrique clé** : l'erreur moyenne de prédiction (agrégée sur `ai_outcome.delta`) doit **baisser** dans le temps (cf. [[Benchmark_Modeles_IA]] §5).

### Côté app (possédé par le backend) — nouveau
- `decision` : `workspace_id`, `scope`, `subject_id`, `agent`, `proposal (jsonb)`, `prediction_id`, `status (proposed|approved|rejected)`, `decided_by`, `decided_at` — c'est **l'objet produit visible** (le Brain reste invisible, cf. [[Moteur_IA_World_Model_OODA]] §7).

---

## 5. Flux de référence (création de projet, bout en bout)

```
1. User: intention "je veux X"                      (front → backend)
2. backend → ai-service POST /ai/decompose          (CPO)
3. ai-service: retrieve(brain) → LLM → cycles+issues + prediction (COO)
4. backend persiste en 'proposed' + crée 1 ai_prediction
5. front: human-in-the-loop → Approve/Reject/Edit    (gate Act)
6. si Approve → backend crée réellement cycles+issues (système de vérité)
7. plus tard: résultat réel observé
8. backend → ai-service POST /ai/reflect (observed)  → ai_outcome + delta
9. delta ré-indexé → améliore les prédictions futures
```

---

## 6. Dockerisation `ai-service` (IA-5)
- Image Python (FastAPI + uvicorn) ; deps IA **installées dans l'image** (pip marche dans le conteneur ; cf. contrainte « pip bloqué en local »).
- Healthcheck `/ai/health` ; variables : `AI_SERVICE_TOKEN`, `GROQ_API_KEY`, `DB_URL` (schéma brain), modèle(s) configurables.
- Accès Postgres restreint au schéma `brain`.

---

## 7. À trancher
- [ ] Nom exact du modèle par endpoint (dépend de [[Benchmark_Modeles_IA]]).
- [ ] Embeddings : local (bge-m3 dans l'image) vs API.
- [ ] Réindexation : synchrone à l'écriture, ou batch via RabbitMQ.
- [ ] ADR « contrat inter-services » à formaliser (`v1/12-decisions/`).
