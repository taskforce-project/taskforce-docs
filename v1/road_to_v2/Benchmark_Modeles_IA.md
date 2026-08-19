# Benchmark modèles IA (v2)

> **Statut : cadre de décision + méthodo (conception).** Sert la stratégie **hybride** de [[Moteur_IA_World_Model_OODA]] §3 : petit modèle pour le volume, fort pour le raisonnement dur, embeddings solides pour le retrieval.
> ⚠️ **Cutoff de connaissance : janv. 2026.** Le paysage et les prix bougent vite → **re-vérifier avant tout choix ferme**. Les colonnes coût/contexte sont des **ordres de grandeur**, pas des chiffres contractuels.

---

## 1. Ce qu'on choisit, et pour quoi

| Besoin | Type de modèle | Volume d'appels |
|---|---|---|
| Extraction, routing, résumé, tags, reformulation | **petit** (7-14B) | 🔥 énorme |
| Découpage projet, specs, décisions C-level, prédictions | **fort** (frontier ou gros open) | modéré |
| **Embeddings** (le retrieval = le moat) | **modèle d'embedding dédié** | 🔥 énorme (indexation) |
| « Notre modèle » (plus tard) | **fine-tune QLoRA** d'un 7-8B sur notre data | — |

> ⚠️ Piège classique : mettre tout l'effort sur le LLM et négliger les **embeddings**. Or dans une archi *retrieval-first*, la qualité du retrieval (donc de l'embedding + du chunking + du graph) compte **autant** que le LLM.

---

## 2. Dimensions d'évaluation

Coût ($/M tokens in/out) · Latence (p50/p95) · Fenêtre de contexte · **Qualité de raisonnement** (découpage/décision) · **Fiabilité sortie structurée / tool-use** (%) · Hébergement (API vs self-host + VRAM) · Licence.

---

## 3. Candidats (ordre de grandeur — à re-vérifier)

### Petits (volume) — via Groq (déjà branché) ou local
| Modèle | ~Taille | Héberg. | Coût | Notes |
|---|---|---|---|---|
| Llama 3.1 8B | 8B | Groq / Ollama | ~gratuit (Groq free-tier) / GPU 8-12 Go | rapide, bon généraliste |
| Qwen2.5 7B/14B | 7-14B | Groq / local | idem | fort en structuré/code, multilingue |
| Mistral Nemo 12B | 12B | local | GPU ~12-16 Go | bon compromis |
| Phi-4 | ~14B | local | GPU ~16 Go | fort raisonnement pour la taille |

### Forts (raisonnement dur)
| Modèle | Héberg. | Coût | Notes |
|---|---|---|---|
| **DeepSeek** (V3/R1-style) | API | **très bas** | excellent rapport raisonnement/prix ; R1 = raisonnement explicite |
| Llama 3.3 70B / Qwen2.5 72B | Groq (70B) / self-host lourd | bas (Groq) / cher (self-host) | open, gros ; Groq sert le 70B vite |
| **Claude (Sonnet/Opus)** | API | plus élevé | top raisonnement + **tool-use fiable** (clé pour les agents) |
| GPT / Gemini | API | variable | alternatives frontier |

### Embeddings (retrieval)
| Modèle | Héberg. | Notes |
|---|---|---|
| **bge-m3 / e5-large** | local (léger) | open, multilingue, très bon rapport qualité/coût — **défaut recommandé** |
| Voyage / OpenAI embeddings | API | qualité haute, payant |

---

## 4. Recommandation (point de départ, à valider par §5)

- **Volume** → **Llama 3.1 8B ou Qwen2.5 7-14B sur Groq** (latence + quasi gratuit, zéro hardware).
- **Raisonnement dur** → démarrer avec **DeepSeek** (qualité/prix imbattable) et/ou **Claude Sonnet** (tool-use fiable pour les agents) ; on tranche avec le benchmark réel.
- **Embeddings** → **bge-m3 en local** (dans `ai-service`), suffisant et gratuit ; passer à une API embeddings seulement si le retrieval plafonne.
- **Fine-tune** → **plus tard** : QLoRA d'un 7-8B une fois qu'on a accumulé specs/décisions/écarts (la data du World Model).

> Principe : **hosted d'abord (Groq/DeepSeek/Claude), self-host/fine-tune quand la data et le besoin le justifient.** On n'achète pas de GPU pour commencer.

---

## 4bis. ✅ Décision retenue — stack IA locale (07/07, contrainte : ZÉRO coût v1)

Groq **gratuit mais bloqué** sur le réseau du poste (403) ; Anthropic/OpenAI **payants → exclus v1**. → **self-host local Ollama**, sur la machine (RTX 5070 **8 Go VRAM** + **32 Go RAM** + CPU 10 cœurs).

> **MAJ 09/07 — Qwen3 + routing par tiers.** Bench réel sur le poste (8 Go VRAM) : un **14B déborde en RAM → ~60-170s et TRÈS variable** ; le **8B = ~18s, régulier**, JSON propre, référence les vraies issues. Décision : **8B par défaut** (réactif), **14B « deep » en opt-in**. Le gateway route un *tier* logique → modèle + thinking.

| Tier | Modèle | Usage | Temps (poste) |
|---|---|---|---|
| **`fast`** *(défaut)* | **`qwen3:8b`** | spec, décision, agent, chat interactif — tout le courant | **~18-30s** |
| **`deep`** *(opt-in « Approfondir »)* | **`qwen3:14b` + thinking** | analyse approfondie quand la qualité prime et qu'on accepte d'attendre | ~90-170s |
| **`standard`** *(dispo)* | `qwen3:14b` sans thinking | palier intermédiaire | ~60-110s |

Détails : câblage côté gateway `OllamaGateway.resolve_tier` (fast→8b/no-think, deep→14b/think) + `/no_think` injecté (Qwen3) ; `OLLAMA_MODEL=qwen3:14b`, `OLLAMA_MODEL_FAST=qwen3:8b`. **Java** : `LlmClient.chatCompletion(..., tier)` ; endpoints `?deep=true` (spec, décision).

| Rôle | Choix | Justif |
|---|---|---|
| **Embeddings** | **BGE-M3** (1024d) — **inchangé** | l'embedding ne monte PAS de version avec Qwen3 ; bge-m3 reste le meilleur multilingue. ✅ **migration V59 faite** (`vector(1024)`, ré-embed effectué). |
| **Coder** *(plus tard)* | `qwen2.5-coder` **ou** délégation Claude Code | en v1 le code est **délégué à Claude Code** (flux « copie le prompt ») → pas de coder local nécessaire. Seam de routing prêt (ajouter un tier `code`). |
| ⚠️ **Swap VRAM** | 1 seul modèle tient dans 8 Go | alterner 8b↔14b recharge (~30s). Ollama garde le dernier chaud ~5 min → enchaîner les tâches du même tier reste rapide. |
| **Vector DB** | **pgvector (existant)** — **PAS** de Qdrant/Chroma | vecteurs co-localisés avec graphe + relationnel → vector + graph-expansion + filtres SQL en **1 requête** ; une DB séparée casserait le graph-expansion. Reconsidérer à 10M+ nodes. |
| **Vector DB** | **pgvector (existant)** — **PAS** de Qdrant/Chroma | vecteurs co-localisés avec graphe + relationnel → vector + graph-expansion + filtres SQL en **1 requête** ; une DB séparée casserait le graph-expansion + 2e source à synchroniser. Reconsidérer à 10M+ nodes. |

> ⚠️ **VRAM ≠ RAM** : la VRAM (8 Go) = vitesse (couches sur GPU) ; la RAM (32 Go) = capacité (débordement CPU). Le 14B *tient* grâce à la RAM, *ralentit* à cause de la VRAM — acceptable pour de la génération.
> Setup (install Ollama + `pull`) = **réseau propre 1×** (le proxy du poste corrompt les gros downloads), puis 100 % offline.

## 5. Le vrai benchmark : à mesurer sur NOS tâches (méthodo)

Les tableaux ci-dessus orientent ; **la décision se prend sur nos données**. Protocole :

1. **Golden set** (~20-50 cas réels tirés du [[Brain_OS]]) :
   - `intention → découpage attendu` (cycles/issues)
   - `spec → qualité` (rubrique)
   - `situation → décision C-level attendue`
   - `action → conséquence réelle` (pour évaluer la **prédiction** du World Model)
2. **Métriques** : qualité (rubrique + juge humain, ou LLM-judge en secours) · **validité JSON / tool-use** (%) · latence p50/p95 · **coût par tâche**.
3. **Protocole** : même prompt, N modèles, ≥3 runs (variance), tableau comparatif.
4. **Métrique spéciale World Model** : **erreur de prédiction** (prédit vs réel) suivie dans le temps — elle doit **baisser** (preuve que la boucle Reflect apprend).

▶ Livrable : un petit harness dans `ai-service` (script + golden set versionné) → rejouable à chaque changement de modèle.

---

## 6. Caveats
- Cutoff janv. 2026 : re-vérifier dispo/prix/licences (surtout Groq free-tier = rate limits, et les licences Llama/Qwen).
- « Gratuit » (Groq) a des **quotas** → prévoir un fallback (local ou API payante) pour la prod.
- Self-host d'un 70B = **coût GPU réel** (VRAM), pas « gratuit ».
