---
id: v2-index
title: TaskForce v2 — AI Delivery OS
doc_type: moc
statut: wip
version: 0.2
date: "07/07/2026"
auteur: Pierre MICHEL
tags: [v2, moc, index, future, ia, world-model, ooda]
related:
  - "../Brain_OS.md"
  - "../IDEA.md"
  - "../v1/README.md"
---

# 🔮 TaskForce — v2 (« AI Delivery Operating System »)

[![Version: v2](https://img.shields.io/badge/Version-v2%20(cible)-8b5cf6?style=for-the-badge)]() [![Statut: WIP](https://img.shields.io/badge/Statut-WIP-orange?style=for-the-badge)]()

> **Pivot** : TaskForce ne « gère pas des projets » — **l'IA gère le projet, l'humain exécute (avec Claude) et supervise (human-in-the-loop)**. L'IDE exécute, TaskForce orchestre. Le moteur d'orchestration piloté par le [[Brain_OS]] est le moat (indépendant du modèle).
> **⚠️ Le PFR démontre une tranche verticale, pas toute la vision** (cf. [[Roadmap_v2]] §3).

## Documents v2

| Doc | Contenu |
|---|---|
| [[IDEA]] | **Vision** — « AI Delivery OS », pipeline Vision→…→Deploy en checkpoints validés, Brain OS auto-rempli |
| [[Moteur_IA_World_Model_OODA]] | **Moteur IA** — retrieval-first, modèles hybride, boucle **World Model × OODA**, **Brain OS interne (invisible)** |
| [[Agents_C_Level]] | **3 agents** — CPO (quoi) / CTO (comment) / COO (quand-risque), rôles/décisions/garde-fous |
| [[Benchmark_Modeles_IA]] | **Benchmark** — candidats (Groq/DeepSeek/Claude/local), reco hybride, méthodo sur nos tâches |
| [[Contrat_API_et_Donnees]] | **Contrat technique** — API `backend↔ai-service`, schéma `brain` + « expériences » World Model, flux bout-en-bout |
| [[Roadmap_v2]] | **Roadmap v2** — 2 tracks (Produit + IA), complexité/dépendances, **tranche PFR** |
| [[Roadmap_Consolidee]] | **Master roadmap** — v2 en tête, backlog v1 à la fin (⚠️ socle RNCP en parallèle) |

## Idées-force (07/07/2026)

- **Retrieval-first** : petit modèle + Brain OS ultra-indexé = travail de « gros » modèle sur notre domaine. L'effort va dans l'**indexation**, pas la taille du modèle.
- **World Model × OODA** : décider vite (OODA) **et** apprendre de ses conséquences (predict→reflect, mémoire Brain OS) → l'agent devient « habile », sans entraînement gradient.
- **Hybride modèles** : petit (Groq/local) pour le volume, fort (hosted) pour le raisonnement dur ; fine-tune LoRA « notre modèle » plus tard.
- **Human-in-the-loop** = garde-fou n°1 des agents.

## Décisions prises (07/07/2026)
- **Brain OS = interne, invisible** à l'utilisateur (moteur, pas une vue produit). → [[Moteur_IA_World_Model_OODA]] §7
- **3 agents** C-level : CPO / CTO / COO. → [[Agents_C_Level]]
- Stratégie **hybride** + méthodo de benchmark. → [[Benchmark_Modeles_IA]]

## Threads ouverts
Mesurer le benchmark sur nos tâches (golden set) · **ADR** « Brain OS interne » + « World Model × OODA » · **Contrat API** `backend` (Java) ↔ `ai-service` (Python) · Refonte indexation Brain OS. (cf. [[Roadmap_v2]] §4)

---

**Projet :** Taskforce — Metz Numeric School 2025-2026
