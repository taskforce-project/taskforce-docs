# Roadmap v2 — TaskForce « AI Delivery OS »

> **Statut : cible v2 (conception).** Traduit [[IDEA]] (vision) + [[Moteur_IA_World_Model_OODA]] (moteur) en tranches exécutables. Complète — ne remplace pas — [[Roadmap_Backlog]] (v1, produit actuel).
> Brainstorm du 07/07/2026. **⚠️ Piège n°1 = le scope** : la vision est un North Star sur 1–2 ans ; le **PFR doit démontrer UNE tranche verticale** (§3).

---

## 1. Deux tracks

### 🅿️ Track Produit (frontend + backend actuels)
| Épic | Description | Complexité | Dépend de |
|---|---|---|---|
| P1 — Flow AI-native création | Projet (intention) → génération cycles/jalons ; Issue → génération description/spec/liens/prompt | 🔴 élevée | IA-1, IA-2 |
| P2 — Cockpit issue | Panneau issue : **spec + prompt IA + suivi GitHub** (PR/commits/CI, ouvrir PR, tag) — cf. [[integrations-mapping]] | 🟠 moyenne | intégration GitHub (fait, lecture) |
| P3 — Runs & checkpoints | Pipeline `Vision→…→Deploy` en checkpoints validés ; « Run » live (logs/fichiers/tests) façon GitHub Actions (cf. [[IDEA]]) | 🔴 élevée | P1, IDE bridge |
| P4 — Human-in-the-loop UI | Valider/rejeter/retry/edit-prompt les propositions IA (gate rapide) | 🟠 moyenne | IA-3 |
| P5 — Chat-as-app | DM, threads, unread, présence (+ miroir Slack déjà là) | 🟠 moyenne | — |

### 🧠 Track IA (`ai-service` Python — à dockeriser proprement)
| Épic | Description | Complexité | Dépend de |
|---|---|---|---|
| **IA-1 — Retrieval Brain OS** | indexation + embeddings + graph ; API de retrieval scopée workspace. **La fondation de tout le reste.** | 🔴 élevée | [[Brain_OS]] (embeddings V51-56 existent) |
| IA-2 — Modèles hybride | intégration Groq/local + routing petit/fort ; (plus tard : fine-tune LoRA) | 🟠 moyenne | benchmark |
| IA-3 — Boucle World Model × OODA | predict → act → observe → reflect ; stockage des « expériences »/écarts ; ré-injection dans Orient | 🔴 élevée | IA-1 |
| IA-4 — Agents C-level | 1–2 agents (CTO/PO) avec outils + décisions par niveau ; garde-fous | 🔴 élevée | IA-1, IA-3 |
| IA-5 — Dockerisation & obs | `ai-service` propre (image, healthcheck, contrat API avec le backend Java) | 🟠 moyenne | — |

> **Dépendance racine : IA-1 (retrieval Brain OS).** Agents (IA-4) et boucle reflect (IA-3) en dépendent. **Côté IA, on commence par IA-1.**

---

## 2. Ordre conseillé (macro)

1. **IA-1** (retrieval Brain OS) — débloque tout.
2. **IA-2** (modèles) + `Benchmark_Modeles_IA.md`.
3. **P1** (génération projet→cycles, issue→spec/prompt) — la 1ʳᵉ vraie valeur AI-native visible.
4. **IA-3** (boucle World Model × OODA) sur 1 type d'action.
5. **P4** (human-in-the-loop) + **IA-4** (1 agent C-level).
6. **P2/P3/P5** au fil de l'eau.

---

## 3. 🎯 Tranche verticale PFR (le démontrable)

> Objectif : **prouver toute la thèse** avec le minimum, sans s'éparpiller.

```
Créer un projet (intention 2 lignes)
   → l'IA génère cycles + 3-4 issues                 [P1 + IA-1/IA-2]
Ouvrir une issue
   → l'IA rédige spec + prompt d'exécution           [P1]
1 agent C-level propose 1 décision                    [IA-4 minimal]
1 boucle predict/reflect sur 1 action                 [IA-3 minimal]
   → prédiction affichée, écart mesuré après coup
Suivi GitHub sur l'issue (PR/commits/CI en lecture)   [P2]
Human-in-the-loop : valider chaque étape              [P4]
```

Tout le reste (multi-agents, 2-way GitHub, runs IDE, fine-tune, chat-as-app complet) = **post-PFR**.

---

## 4. Threads à trancher (avant d'exécuter)

- [ ] **Benchmark modèles** (§IA-2) → `Benchmark_Modeles_IA.md`
- [ ] **Accès Brain OS** utilisateur (interne vs projection curée) → ADR — cf. [[Moteur_IA_World_Model_OODA]] §7
- [ ] **Refonte agents C-level + indexation Brain OS** (ce qui change concrètement)
- [ ] **Contrat API** backend Java ↔ `ai-service` Python (qui appelle qui, sync/async, events)
