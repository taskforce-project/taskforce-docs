# Roadmap consolidée — TaskForce (RÉCONCILIÉE avec l'existant)

> **Master roadmap** post-pivot + **post-recon (07/07/2026)**.
> 🚨 **Correction majeure** : le moteur IA du v2 **existe déjà à ~80 %**, en **Java** (Brain OS, Phases 0→3 ✅, agent code-complet), **`env-gated`** (clé LLM + embeddings). On ne construit **pas** un service IA Python neuf → on **allume + on finit**. Le `ai-service` Python = fournisseur d'embeddings uniquement.
> Le **critère de fin (wow-demo)** = la **Phase 4** déjà planifiée du Brain OS.
> Détail moteur : `.ai/brain-os-roadmap.md` (repo app). Détail v2 : [[Moteur_IA_World_Model_OODA]]. Backlog v1 : [[Roadmap_Backlog]].

---

## Ce qui existe déjà (ne PAS reconstruire)

| Brique v2 que j'avais « à faire » | Réalité |
|---|---|
| IA-1 retrieval Brain OS | ✅ **fait** — `BrainSearchService` (pgvector cosine + ranking + compression) |
| Agent + tool-calling + write-back | ✅ **code-complet** — `AgentService` (routing fast/deep, `search_brain`/`create_note`, `AgentToolRegistry`) |
| Modèles hybride | ✅ **déjà l'archi** — Groq 8b (fast) + Claude Opus (deep), `env-gated` sur clé |
| Brain OS invisible (moteur) + graphe | ✅ — noyau `AGENTS` caché, 1 workspace = 1 brain |
| Node `ACTION_OODA` | ✅ **déjà prévu** dans les types de nodes |

→ Ma spec [[Contrat_API_et_Donnees]] (archi Python-centrée) est **partiellement caduque** : les agents vivent en **Java**, pas dans un service Python. À corriger.

---

## Phases (corrigées)

| Phase | Contenu réel | Effort |
|---|---|---|
| **A · Allumer le moteur (via AI Gateway)** | 🟢 **A1→A5 FAITS (08/07) — Phase A terminée.** Ollama local (Qwen2.5 14B) + Gateway Python `/v1/chat`, `LlmClient`/`AiGatewayClient`/sélecteur `LlmConfig`, `AgentService` rebranché (chat vérifié live, Qwen 14B GPU, **0 €**, ~14 s). **A4 fait** : embeddings **bge-m3 1024d** via Ollama (`EmbeddingService`→`OllamaGateway.embed`, repli lexical 1024d), `config.embedding_dim=1024`, `EmbeddingClient.DIMENSIONS=1024`, **migration V59** (`knowledge_nodes.embedding vector(384)→vector(1024)` + HNSW recréé). **Vérifié live** : `/health` bge-m3/1024, embed `real=true` 1024d, recherche brain = **5 hits** (cosine 0.44–0.51), **19/19 nodes ré-embeddés** en 1024d. | ✅ **DONE** |
| **B · 🎯 LE WOW = critère PFR** | **Phase 4 Brain OS** : issue → l'IA **propose** (spec + prompt + découpage + « déjà vu ? ») → **human-in-the-loop** (approve/reject/modify) → *(option)* **code agent** (Claude implémente → PR draft) → review. = *« ça avance tout seul, je copie le prompt, je valide »*. | 🔴 **L/XL** |
| **C · C-level + World Model × OODA** | étendre l'agent unique → **3 agents** (CPO/CTO/COO, [[Agents_C_Level]]) + boucle **predict/reflect** stockée en nodes `ACTION_OODA` + edges (dans le brain existant, pas une nouvelle base) | 🔴 **L** |
| **D · Reste** | marketplace (Agent Packs), GitHub 2-way, Slack sortant, fine-tune LoRA *(optionnel — le wow ne le nécessite pas)* | 🟡 |
| **∥ Socle RNCP** *(en parallèle A→B)* | tests front (TF-TEST-001), sécu P1, déploiement (TF-INFRA), **mémoire** (TF-DOC-001) — **non négociable pour la soutenance** | 🟠 |

---

## 🎯 Le critère de fin (ce que tu pourras dire « c'est fini »)

> **Démo de soutenance** : je crée un projet en 2 lignes → cycles + issues générés. J'ouvre une issue → l'IA a écrit la **spec** + le **prompt d'exécution**. Je **copie le prompt** (Claude Code), ça code → **PR draft**. Je **valide** (ou rejette/modifie). Le Brain OS s'est enrichi tout seul. **Effet waouw = le projet avance quasi seul, je copie + je valide.**

C'est **exactement la Phase 4** ci-dessus. Tout le reste (C/D) est bonus post-démo.

---

## Ordre d'exécution
1. **Phase A** (allumer — quelques heures).
2. **Phase B** (le wow — le gros du build restant).
3. **∥ Socle RNCP** en parallèle (obligatoire soutenance).
4. Phases **C/D** si le temps le permet (différenciation).

**Dernière MAJ :** 08/07/2026 · **Phase A terminée** (A4 embeddings bge-m3 1024d vérifiés live). **Prochaine : Phase B (le wow).**
