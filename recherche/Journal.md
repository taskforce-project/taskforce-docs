---
id: recherche-journal
title: Cahier de labo — R&D Brain OS
doc_type: register
statut: active
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, journal, cahier-de-labo, brain-os]
related:
  - "./README.md"
  - "./CLAUDE.md"
---

# 📓 Cahier de labo — R&D Brain OS

> **Le cahier de bord daté du laboratoire.** Une **entrée par session** de recherche, **la plus récente
> en haut**. À ouvrir en début de session (« où on en était »), à remplir en fin ([`CLAUDE.md`](./CLAUDE.md) §10).
>
> **Format d'entrée** (gabarit dans [`Gabarits.md`](./Gabarits.md)) : `Fait` · `Trouvé` · `Décidé` ·
> `Prochain coup`. On **date**, on **ne réécrit pas** le passé (une erreur reste, on la corrige dans une
> entrée suivante — c'est un cahier, pas un wiki).

---

## 2026-07-31 (bis) — A5 (calibration) poussée à fond · frontière solo

**Fait** — Première frontière poussée en solo : **A5 → fiche dédiée** [`theorie/A5-calibration.md`](./theorie/A5-calibration.md)
(pattern « un axiome poussé = une fiche »). Entrée A5 de [`Axiomes.md`](./theorie/Axiomes.md) réduite à un
résumé. E1 raffiné en 3 régimes ([`experiences/Experiences.md`](./experiences/Experiences.md)). `issue_worklogs`
(V47) lu.

**Trouvé**
- `[ÉTABLI]` **Le système n'émet aujourd'hui aucune croyance calibrable** : story points = **point** (pas
  de distribution), « déjà-vu 41 % » = **cosinus déguisé en proba** (l'erreur même que A5 dénonce). Donc
  A5 est **bloqué en amont** : avant de calibrer, il faut que le **produit émette une incertitude**.
- `[DÉDUIT]` **« Calibré » est trivial** (prédire le taux de base y arrive) → viser **calibré ET tranchant**
  (décomposition de Murphy : fiabilité *et* résolution). Un test de calibration seul validerait un prédicteur nul.
- `[DÉDUIT]` **A5 se scinde** : **A5a** (scoreable, groundable) / **A5b** (contrefactuel, **infalsifiable
  par C2** → jamais de proba, un scénario). Groundable où c'est le moins précieux, impossible où ça compte le plus.
- `[DÉDUIT]` Au grain cycle, ~4 points/bin → **IC de Wilson ≈ [0,30 ; 0,95]** : calibration **indécidable** (C3).
- `[ÉTABLI]` Le « réel » d'un story point = **effort** = `SUM(issue_worklogs.minutes)` (V47) ; **si** peuplé,
  sinon proxy **latence** (biaisé). Le prédicteur calibré **existe déjà** : le **taux de base** (`GROUP BY`).

**Décidé** — A5 acté comme **scindé A5a/A5b** dans la spec. La vraie question de A5 n'est pas « calibrer le
LLM » mais « **quelque chose bat-il le taux de base ?** » (E3).

**Prochain coup**
- Frontière solo suivante : **A4** (dynamique `f`) — ou **A8** (Pareto sur trajectoires *passées*, faisable sans A4).
- Point dev en attente : vérifier si `issue_worklogs` est peuplé (décide si E1 mesure l'effort ou la latence).

---

## 2026-07-31 — Écosystème, grounding E2, système d'axiomes, structuration du labo

**Fait**
- Revue critique du **dump « écosystème en couches »** + 4 croquis → [`revues/Ecosysteme.md`](./revues/Ecosysteme.md).
- **E2 mis au cordeau** contre le **schéma réel** (V16/V23/V38 lus) : requête SQL exécutable, pièges
  documentés (pas de `completed_at` sur `cycles`, lien via `cycle_issues`, `story_points` nullable).
  → [`experiences/Experiences.md`](./experiences/Experiences.md#e2--la-dérivée-dot-x-apporte-t-elle-de-linformation-).
- **Système d'axiomes v0.1** créé → [`theorie/Axiomes.md`](./theorie/Axiomes.md) : noyau A1–A3 (grounded),
  frontière A4–A8 (chacun avec son test), carte de dépendances.
- **Brouillon ADR-012** (exposition du Brain OS, réponse à Q6) → [`decisions/`](./decisions/ADR-012-DRAFT-brain-os-exposition.md).
- Deux questions ajoutées : **Q8** (construire vers l'intérieur/extérieur), **Q9** (quel flywheel : F1/F2/F3).
- **Restructuration du dossier en laboratoire** : stations `theorie/ experiences/ revues/ references/
  decisions/`, paillasse racine (README/CLAUDE/Journal/Gabarits/Questions), ce cahier de bord.

**Trouvé**
- `[DÉDUIT]` **A5 (calibration) est le goulot** : sans savoir scorer une prédiction, ni A4 (dynamique),
  ni les probabilités, ni A8 (trajectoires) ne se groundent. Le grand système se réduit, aujourd'hui,
  à **une question à un jour** : sait-on scorer nos propres prédictions ? → **E1**.
- `[ÉTABLI]` Trois choses s'appellent « flywheel » et une seule est faible : **F1** (style, speccé),
  **F2** (mémoire organisationnelle = **le moat**, déjà à moitié bâti), **F3** (modèle du monde, étranglé
  par C1/C3). Le pitch « more usage → better models » vend **F3**, le plus faible. → vendre **F2**.
- `[ÉTABLI]` Le simulateur `MCTS/Monte-Carlo` du schéma est infaisable (C1 : rien à apprendre ; C2 :
  monde non rejouable). Ne survit qu'un **modèle System Dynamics à la main, assumé outil de pensée**.
- `[ÉTABLI]` Schéma : `cycles` n'a **pas** de `completed_at` (clôture non datée) ; seed = ~8 issues en
  cycle sur 267 → E2 sur ~4 cycles = **plomberie**, pas validation statistique (C3).

**Décidé** *(en attente de ratification humaine)*
- Reco **ADR-012 = option B** : la **connaissance** est un produit exposé (UI Brain OS déjà livrée), le
  **raisonnement** (croyances, trajectoires, écarts) reste **interne**. → à ratifier pour promotion en `v1/12-decisions/`.
- « Complet » abandonné au profit de « **reproductible** » pour le système d'axiomes (un axiome = un test SQL).

**Prochain coup**
- **E1** (grounder A5 : story points prédits vs réel, score de Brier) — **nécessite un passage en mode
  dev** + arbitrage priorité vs clôture V1.
- Option parallèle en R&D pur : **pousser la frontière A4–A8** dans le gabarit (solo, ou workflow ~7–8 agents).
- ⏳ **Ratifier ou non l'ADR-012.**

> **Intendance** — un auto-committer (probable `obsidian-git`) balaie les fichiers du labo en commits
> non déclenchés par l'agent. Sans danger, mais la section se construit en commits « fantômes ».

---

## 2026-07-17 — Amorçage du laboratoire

**Fait** — Création de la section R&D : protocole [`CLAUDE.md`](./CLAUDE.md) (contrat épistémique,
contraintes C1–C4, comité, cinq altitudes), formalisme [`theorie/Modele-mathematique.md`](./theorie/Modele-mathematique.md),
revue [`revues/World-Model.md`](./revues/World-Model.md), registres [`Questions-ouvertes.md`](./Questions-ouvertes.md)
et [`experiences/Experiences.md`](./experiences/Experiences.md), bibliothèque [`references/Bibliotheque.md`](./references/Bibliotheque.md).

**Trouvé** — Le trou central de `World Model.md` : **personne ne calcule `f`**. Sous C1–C4, `f` est soit
écrite à la main (simulation de nos croyances), soit produite par un LLM (texte chiffré) — jamais apprise.
La meilleure idée récupérable : **`ẋ`, la dérivée** (calculable en SQL).

**Décidé** — La direction retenue reste celle du 07/07 (mémoire/retrieval, sans gradient) ; `World Model.md`
est une note de recherche **sans autorité** tant qu'aucun ADR ne tranche.

**Prochain coup** — Préciser E2, esquisser l'ADR de Q6. *(fait le 31/07)*

---

**Points d'entrée :** [🔬 Labo](./README.md) · [📋 Protocole](./CLAUDE.md) · [🧰 Gabarits](./Gabarits.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
