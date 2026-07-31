---
id: recherche-references
title: Bibliothèque mentale — cadres de référence
doc_type: reference
statut: active
version: 1.0
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, references, world-model, decision, systemes-complexes]
related:
  - "./CLAUDE.md"
  - "./World_Model_Notes.md"
---

# 📚 Bibliothèque mentale

> **Règle de ce fichier** — on n'écrit ici que des travaux dont l'existence est **certaine**. Un titre
> approximatif, une date incertaine ou un chiffre de mémoire se marquent **« ⚠ à vérifier »**. Une
> bibliographie fausse détruit la crédibilité de tout le reste, et c'est ce qu'un jury vérifie en premier.
>
> **Aucune de ces références n'a été lue intégralement dans le cadre du projet.** Ce fichier est une
> **carte** (« qui a déjà pensé à ce problème, et sous quel nom »), pas une revue de littérature.

## Comment s'en servir

Quand une idée émerge en session, chercher ici **si le champ existe déjà**. Le plus souvent, oui — et
la question devient « pourquoi ne pas prendre le cadre existant ? ». Les colonnes **« Ce que ça donne »**
et **« Applicable ici ? »** sont là pour trancher vite, en tenant compte des contraintes C1–C4
([`CLAUDE.md`](../CLAUDE.md) §3).

---

## 1. World models (le corpus revendiqué par le brainstorm)

| Travail | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Ha & Schmidhuber, *World Models* (2018)** — arXiv:1803.10122 | Un agent apprend un modèle compressé de son environnement (VAE + RNN) et **s'entraîne dans son rêve** | ❌ **C1** — apprentissage par millions de frames |
| **LeCun, *A Path Towards Autonomous Machine Intelligence* (2022)** — position paper, OpenReview (v0.9.2) | L'architecture modulaire : perception, **world model**, **cost**, actor, short-term memory, configurator. Le LLM n'est **qu'un module**. | 🟡 **L'architecture** (séparer modèle / coût / planificateur) est reprenable. **L'entraînement**, non (C1/C4). |
| **JEPA / I-JEPA (Assran et al., 2023) · V-JEPA (2024)** | Prédire dans l'**espace latent** plutôt que dans l'espace des pixels/tokens | ❌ **C1/C4** — nécessite un entraînement. Cité comme intuition, jamais comme plan. |
| **MuZero (Schrittwieser et al., 2020)** — *Mastering Atari, Go, Chess and Shogi by Planning with a Learned Model* | Apprend la **dynamique latente** et planifie dedans (MCTS), sans connaître les règles | ❌ **C1** — self-play massif. **Mais** : c'est la preuve que la recherche dans un modèle appris fonctionne *quand on peut rejouer le monde* (**C2**). |
| **Dreamer / DreamerV3 (Hafner et al.)** | Apprentissage d'un world model latent + « imagination » pour l'entraînement | ❌ **C1** |

> **Le point à retenir de ce bloc** : ces systèmes marchent parce que le monde est **rejouable à coût
> nul** (Atari, Go, MuJoCo). C'est **C2** qui nous exclut, pas un manque d'ingéniosité.

## 2. Décision & planification (les cadres classiques)

| Cadre | Objet | Applicable ici ? |
| --- | --- | --- |
| **MDP** — Bellman ; **Sutton & Barto, *Reinforcement Learning: An Introduction* (2ᵉ éd., 2018)** | $(S, A, P, R, \gamma)$ ; équation de Bellman ; $\pi^*$ | 🟡 **Vocabulaire** oui. **Algorithmes** non (exigent $P$ et des épisodes). |
| **POMDP** — Kaelbling, Littman & Cassandra (1998), *Planning and acting in partially observable stochastic domains* | L'agent ne connaît que $\hat S$ ; il maintient un **état de croyance** $b(s)$ | ✅ **Le bon cadre conceptuel** : formalise exactement le « $S$ vs $\hat S$ » du brainstorm. Résolution exacte intraitable — mais le **vocabulaire** est le bon. |
| **MCTS** — Coulom (2006) ; **UCT**, Kocsis & Szepesvári (2006) | Recherche arborescente guidée par simulation | ❌ Exige un simulateur fiable. Sans lui, on cherche dans une fiction. |
| **MPC** (Model Predictive Control) — théorie du contrôle | Optimiser sur un **horizon glissant**, ré-optimiser à chaque pas | 🟡 **L'idée du re-planning permanent** est saine et cousine d'OODA. |
| **Filtre de Kalman** / **filtre particulaire** | Estimer un état caché à partir d'observations bruitées | 🟡 Le bon réflexe pour $\hat S$ — mais suppose un modèle de transition connu. |
| **Bandits / Thompson sampling** | Explorer vs exploiter sous incertitude, **sans modèle du monde** | ✅ **Sous-estimé pour nous** : marche avec peu de données et **sans** $f$. |

## 3. Causalité

| Travail | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Pearl, *Causality* (2ᵉ éd., 2009)** ; **Pearl & Mackenzie, *The Book of Why* (2018)** | SCM, **do-calculus**, échelle : association → intervention → contrefactuel | 🟡 **Le cadre nomme précisément notre problème** : on veut le niveau 2/3 (intervention), on n'a que le niveau 1 (corrélation). |
| — | *Conséquence directe* | ⚠️ **C2** : sans contrefactuel observable, l'identification causale exige des hypothèses (graphe causal correct, pas de confondeur caché) **invérifiables** sur un projet unique. |

## 4. Systèmes complexes & dynamique — **le champ que le brainstorm ignore**

| Travail | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Forrester, *Industrial Dynamics* (1961)** — System Dynamics | **Stocks & flux**, boucles de rétroaction, **délais**. Modèles **écrits à la main**, petits, interprétables, validés en **ajustant des courbes historiques**. | ✅✅ **Le meilleur candidat.** Fait exactement ce que le brainstorm réinvente en moins bien — et **survit à C1** (pas d'apprentissage). |
| **Abdel-Hamid & Madnick, *Software Project Dynamics* (1991)** | System Dynamics appliqué **aux projets logiciels** : recrutement, formation, pression, qualité, retard | ✅✅ **Notre domaine exact, modélisé il y a 35 ans.** À lire avant d'écrire une ligne de simulateur. |
| **Brooks, *The Mythical Man-Month* (1975)** | **Loi de Brooks** : ajouter des développeurs à un projet en retard le retarde davantage (formation + communication en $O(n^2)$) | ✅ **Contre-exemple direct** à l'exemple `Hire → Velocity +30` du brainstorm. Cf. [`World_Model_Notes.md`](../revues/World-Model.md). |
| **Théorie des jeux** — Nash | Plusieurs agents, utilités différentes | ❌ Exige d'observer l'état **et** l'utilité des concurrents. Ni l'un ni l'autre n'est accessible. |

## 5. Incertitude, calibration, prévision

| Travail / notion | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Score de Brier** ; **courbes de calibration** ; **règles de score propres** | Mesurer si un « 70 % » **veut dire** 70 % | ✅✅ **Le prérequis absolu** avant d'afficher la moindre probabilité. Peu coûteux. |
| **Kahneman & Tversky — *planning fallacy*** ; **Flyvbjerg — *reference class forecasting*** | Prédire par la **classe de référence** (« les projets comme celui-ci ont pris X ») bat le raisonnement causal détaillé | ✅✅ **Le plus rentable immédiatement** : la table `cycles` **contient déjà** notre classe de référence. |
| **Kahneman, *Thinking, Fast and Slow* (2011)** | Système 1 / système 2 | 🟡 Analogie utile avec le routing fast/deep déjà codé. Rien de plus. |
| **Goodhart** (« quand une mesure devient une cible… ») ; **loi de Campbell** | Optimiser un proxy détruit le proxy | ⚠️ **Objection directe** à la fonction d'utilité pondérée $U$ du brainstorm. |

## 6. Optionalité & risque (la piste « Φ »)

| Travail | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Dixit & Pindyck, *Investment under Uncertainty* (1994)** — options réelles | La **valeur d'attendre** ; garder des options ouvertes a une valeur quantifiable | ✅ **Le brainstorm réinvente ça sous le nom Φ.** Le champ existe, avec 30 ans de littérature. |
| **Taleb** — optionalité, antifragilité | Payer peu pour un accès à un gros gain ; asymétrie | 🟡 Intuition, pas outil. |
| **Markowitz** — moyenne-variance | Arbitrage rendement / risque via une aversion $\lambda$ | 🟡 Le $\max (U - \lambda R)$ du brainstorm **est** la moyenne-variance. Nommer le cadre au lieu de le réinventer. |
| **Optimisation multi-objectif** — **front de Pareto**, dominance | Ne **pas** scalariser des objectifs incommensurables : montrer les **non-dominés** | ✅✅ **La bonne réponse** au problème des poids de $U$ — et la seule cohérente avec « l'humain décide ». |

## 7. Agents LLM à mémoire (la lignée réellement retenue)

> `[ÉTABLI]` C'est la lignée qu'a choisie [Moteur_IA_World_Model_OODA](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §4
> (07/07/2026) : world model **mémoire / retrieval, sans gradient**.

| Travail | Idée centrale | Applicable ici ? |
| --- | --- | --- |
| **Reflexion (Shinn et al., 2023)** | L'agent **verbalise** ses échecs et les relit au tour suivant — apprentissage **sans gradient** | ✅ Directement transposable : c'est le « stocker l'écart prédit/réel » de road_to_v2 §4. |
| **Voyager (Wang et al., 2023)** | Agent LLM à **curriculum ouvert** + bibliothèque de compétences réutilisables | 🟡 Inspiration pour la croissance du graphe. |
| **Generative Agents (Park et al., 2023)** | Mémoire + **réflexion** + planification ; récupération par pertinence/récence/importance | ✅ Le **ranking** (récence + importance + similarité) est déjà l'esprit du pipeline de retrieval codé. |
| **Boyd — boucle OODA** | Observe, Orient, Decide, Act. Le **tempo** comme avantage. | ✅ `[ÉTABLI]` déjà retenu (road_to_v2 §4). ⚠ Corpus primaire = briefings (*A Discourse on Winning and Losing*), pas un livre canonique — **⚠ à vérifier** avant toute citation en soutenance. |

---

## Ce qui manque encore ici

- [ ] **Lire réellement** Abdel-Hamid & Madnick (§4) — le seul travail du corpus qui modélise *notre*
      domaine exact. Tout le reste est analogie.
- [ ] Vérifier les références **Boyd** avant citation publique (⚠ ci-dessus).
- [ ] Chercher la littérature sur la **calibration des prédictions d'estimation logicielle**
      (story points vs réel) — probablement abondante, non explorée. Lien direct avec
      [`Experiments.md`](../experiences/Experiences.md) §E1.

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [📖 Notes critiques](../revues/World-Model.md)

**Dernière mise à jour :** 17/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
