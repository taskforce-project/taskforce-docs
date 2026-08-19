---
id: road-to-v2-index
title: Road to v2 — AI Delivery OS (évolution de la v1)
doc_type: moc
statut: wip
version: 0.3
date: "07/07/2026"
auteur: Pierre MICHEL
tags: [road-to-v2, moc, ia, world-model, ooda, ollama]
related:
  - "../../Brain_OS.md"
  - "../../IDEA.md"
  - "../README.md"
---

# 🧭 Road to v2 — « AI Delivery Operating System »

> **On est en v1.** Ceci est la **direction produit + la roadmap d'exécution** vers la vision « AI Delivery OS ».
> C'est de l'**évolution du code v1 existant** (on *allume* le Brain OS Java + un LLM local Ollama, on finit la **Phase 4** du Brain OS), **pas** une réécriture v2 from-scratch.
> **Pivot** : l'IA gère le projet, l'humain **exécute (Claude Code) + supervise (human-in-the-loop)**. Le moat = l'**orchestration** ([[Brain_OS]]), pas le modèle.

## Documents

| Doc | Contenu |
|---|---|
| [[IDEA]] | **Vision** — « AI Delivery OS », pipeline Vision→…→Deploy en checkpoints validés |
| [[Guide_Ollama]] | **Guide setup Ollama** (install + pull modèles + vérif GPU/API) — à faire sur réseau propre |
| [[Moteur_IA_World_Model_OODA]] | **Moteur IA** — retrieval-first, boucle **World Model × OODA**, **Brain OS invisible** |
| [[Agents_C_Level]] | **3 agents** — CPO / CTO / COO |
| [[Benchmark_Modeles_IA]] | **Modèles** — décision : Ollama local (Qwen 14B) + bge-m3 + pgvector, gratuit |
| [[Contrat_API_et_Donnees]] | **AI Gateway** (Python) + schéma « expériences » World Model + flux bout-en-bout |
| [[Connecteurs_et_Catalogue]] | **Système d'intégrations** — catalogue déclaratif (47 outils, 16 catégories) + API/UI générique ; ajouter un outil = une ligne |
| [[Data_Flywheel_et_Apprentissage]] | **RAG→LoRA** — pourquoi on n'entraîne pas Qwen aujourd'hui ; collecter le corpus produit (draft vs final + signal) pour un LoRA de préférences demain |
| [[Roadmap_Consolidee]] | **Master roadmap** — phases A→D + socle RNCP en parallèle |

## Décisions actées (07/07/2026)
- **Zéro coût v1** → **LLM local Ollama** (Qwen2.5 14B Instruct sur RTX 5070) ; Groq bloqué (403), Anthropic/OpenAI payants exclus.
- **AI Gateway** (Python `ai-service`) devant Ollama ; le **Java garde l'orchestration** (`AgentService`) + le **retrieval** (`BrainSearchService` → pgvector). On ne réécrit pas l'existant.
- **Brain OS = interne, invisible** ; **pgvector** (pas de vector DB séparée) ; **BGE-M3** embeddings (→ migration V59 `vector(1024)`).
- **3 agents** CPO/CTO/COO ; boucle **World Model × OODA** (predict/reflect, mémoire).
- **Critère de fin (wow)** = **Phase 4 Brain OS** : intention → génération → **je copie le prompt (Claude Code) → je valide**.

## Threads ouverts
Benchmark sur golden set · ADR (Brain OS interne, World Model×OODA, AI Gateway) · reranking (`/rerank`) · modèle Coder dédié (post-wow).

---

**Projet :** Taskforce — Metz Numeric School 2025-2026
