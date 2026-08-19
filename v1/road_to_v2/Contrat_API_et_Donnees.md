# AI Gateway + Modèle de données IA (v2)

> **Statut : conception (v2).** Corrigé le 07/07 après recon : le moteur (agent + retrieval) existe **en Java** ; on ajoute une **AI Gateway Python** comme **couche modèle** (pas comme cerveau). Décision : **gateway dès la v1** (pour pouvoir swap/scaler les modèles + héberger le ML : embeddings, reranking, fine-tune).
> Support de [[Moteur_IA_World_Model_OODA]], [[Benchmark_Modeles_IA]], [[Roadmap_Consolidee]].

---

## 1. Le principe : 3 couches, chacune à sa place

```
┌─────────────────────────────────────────────────────────────┐
│ BACKEND JAVA (tf-api)  — ORCHESTRATION + RETRIEVAL + VÉRITÉ  │
│   AgentService (routing fast/deep, tool-calling, write-back) │
│   BrainSearchService (pgvector kNN + graph-expansion)        │  ← lit Postgres DIRECTEMENT
│   Human-in-the-loop, authz, système de vérité (app tables)   │
└───────────────┬─────────────────────────────────────────────┘
                │  HTTP (réseau Docker interne)
                ▼
┌─────────────────────────────────────────────────────────────┐
│ AI GATEWAY (ai-service Python, FastAPI)  — COUCHE MODÈLE     │
│   /chat   → routing modèle → Ollama (Qwen 14B) [/Groq/…]     │
│   /embed  → Ollama (bge-m3)  [ou modèle d'embedding dédié]   │
│   /rerank → (futur) cross-encoder                            │
│   /health                                                    │
└───────────────┬─────────────────────────────────────────────┘
                │  HTTP OpenAI-compat
                ▼
        ┌───────────────┐
        │    OLLAMA      │  (local, RTX 5070, gratuit)
        │  Qwen 14B      │
        │  bge-m3        │
        └───────────────┘

POSTGRES (pgvector + knowledge_nodes/edges) ← lu par BrainSearchService (Java)
```

**Pourquoi cette répartition :**
- **Orchestration en Java** = on réutilise l'`AgentService` **code-complet** (routing, tools, write-back). On ne réécrit pas.
- **Retrieval en Java** = les vecteurs sont dans Postgres avec le graphe → `BrainSearchService` fait *vector + graph-expansion + filtres SQL* en **une requête** (impossible à déporter proprement).
- **Gateway en Python** = là où le ML vit (embeddings, reranking, éval, fine-tune plus tard). Le backend **ne connaît plus le modèle** : il parle au gateway. Swap Ollama→autre = zéro changement Java.

---

## 2. Contrat de l'AI Gateway (Python)

| Méthode | Endpoint | Entrée | Sortie | Rôle |
|---|---|---|---|---|
| `POST` | `/chat` | `{messages[], model?, tools?, json?}` | `{message, tool_calls?}` (format OpenAI) | génération / tool-calling |
| `POST` | `/embed` | `{texts[]}` | `{vectors[][1024]}` | embeddings (bge-m3) |
| `POST` | `/rerank` *(futur)* | `{query, docs[]}` | `{scores[]}` | reranking retrieval |
| `GET`  | `/health` | — | `{status, models[]}` | ops |

- **Auth interne** : `AI_GATEWAY_TOKEN` en header + réseau Docker (jamais exposé public).
- **Config** : le gateway lit `AI_PROVIDER` (ollama|groq), l'URL Ollama, les noms de modèles. Le **routing modèle vit dans le gateway**, pas dans Java.
- **Java** : un seul client `AiGatewayClient` remplace les appels Groq/Ollama directs dans `AgentService` + `EmbeddingClient`.

> `OllamaService.java` (déjà écrit) = **provient de l'ancienne approche directe** → soit il devient l'implémentation *interne* si on garde un fallback Java, soit on le retire au profit du gateway. À trancher à l'implémentation (A3).

---

## 3. Modèle de données — World Model (« expériences »)

*(Inchangé et toujours valable — stocké dans le schéma brain existant, pas une nouvelle base.)*
```
ai_prediction  (id, workspace_id, agent CPO|CTO|COO, scope, subject_id,
                action_proposed jsonb, prediction jsonb, created_at)
ai_outcome     (id, prediction_id→ai_prediction, observed jsonb, delta jsonb, created_at)
```
- Le couple `(prediction, delta)` ré-indexé (embedding) → `Orient` futur retrouve les écarts → l'agent devient « habile ».
- **Métrique** : erreur moyenne de prédiction (agrégée) doit baisser.
- Représentable en **nodes `ACTION_OODA` + edges** dans `knowledge_nodes`/`knowledge_edges` (type de node déjà prévu) — pas de table neuve si on préfère.

---

## 4. Flux de référence (issue → spec + prompt, le wow)

```
1. User ouvre une issue                                   (front → backend Java)
2. AgentService (deep) : besoin de contexte
   → BrainSearchService : embed(query) via Gateway /embed
                        → pgvector kNN + graph-expansion (Postgres)
   → chunks pertinents
3. AgentService → Gateway /chat (Qwen 14B) : "rédige spec + prompt d'exécution"
4. backend persiste en 'proposed' (+ ai_prediction pour le World Model)
5. front : human-in-the-loop → Approve/Reject/Modify
6. Approve → l'issue reçoit spec + prompt ; write-back node dans le brain
7. (option) prompt copié → Claude Code → PR draft → observé → /reflect (delta)
```

---

## 5. Migration à prévoir (bge-m3)
- **V59** : `knowledge_nodes.embedding vector(384)` → **`vector(1024)`** (bge-m3) + recréer l'index HNSW + ré-embed les nodes existants. (Cf. [[Benchmark_Modeles_IA]] §4bis.)

---

## 6. À trancher à l'implémentation
- [ ] `OllamaService.java` : le garder (fallback Java direct) ou tout passer par le gateway ?
- [ ] Réindexation embeddings : synchrone à l'écriture, ou batch (RabbitMQ).
- [ ] ADR « AI Gateway » (`v1/12-decisions/`).
