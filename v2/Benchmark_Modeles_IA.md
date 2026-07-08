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
