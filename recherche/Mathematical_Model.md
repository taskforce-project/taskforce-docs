---
id: recherche-modele-mathematique
title: Modèle mathématique candidat — Brain OS
doc_type: reference
statut: draft
version: 0.1
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, world-model, formalisme, brain-os, graphe]
related:
  - "./CLAUDE.md"
  - "./World_Model_Notes.md"
  - "./Open_Questions.md"
  - "../World Model.md"
---

# 📐 Modèle mathématique candidat — Brain OS

> **Statut : `[HYPOTHÈSE]` — v0.1, rien n'est implémenté.** Ce document met au propre le formalisme issu
> du brainstorm [`World Model.md`](../World%20Model.md) (LaTeX réparé, doublons fusionnés, marqueurs
> épistémiques ajoutés). **Le mettre au propre ne le valide pas.**
>
> Il **contredit** l'architecture décidée le 07/07 ([Moteur_IA_World_Model_OODA](../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §4 :
> mémoire/retrieval, sans gradient). Tant qu'aucun **ADR** ne tranche, ceci est une **piste**, pas une cible.

## Table des matières

1. [La question préalable](#1-la-question-préalable--qui-calcule-f)
2. [Ce qui est déjà là](#2-ce-qui-est-déjà-là-établi)
3. [L'état du monde](#3-létat-du-monde)
4. [Les objets](#4-les-objets)
5. [Les relations](#5-les-relations)
6. [Les actions](#6-les-actions)
7. [Les trajectoires](#7-les-trajectoires)
8. [L'évaluation](#8-lévaluation--et-pourquoi-elle-est-mal-posée)
9. [Le pipeline](#9-le-pipeline-plutôt-quune-formule)
10. [Ce que ce modèle ne dit pas](#10-ce-que-ce-modèle-ne-dit-pas)

---

## 1. La question préalable — qui calcule $f$ ?

Tout ce qui suit suppose une dynamique :

$$S_{t+1} = f(S_t, a_t, \epsilon)$$

**Cette fonction n'existe pas, et le document source ne dit jamais d'où elle viendrait.** C'est le
trou central : chaque raffinement ultérieur (composantes de $v_i$, arbre de futurs, paysage
d'énergie) **s'appuie dessus sans l'interroger**.

Sous les contraintes C1–C4 ([`CLAUDE.md`](./CLAUDE.md) §3), il n'y a que **deux** origines possibles :

| Origine | Ce que c'est réellement | Conséquence |
| --- | --- | --- |
| **(a) $f$ écrite à la main** | Une simulation de **nos propres croyances** | Elle confirmera ce qu'on y a mis. Utile comme *outil de pensée* (cf. System Dynamics, [`References.md`](./References.md) §4), **jamais** comme oracle. |
| **(b) $f$ produite par un LLM** | De la **génération de texte** avec des chiffres dessus | C'est exactement ce que le document dit vouloir dépasser. Le formalisme sert alors de **décor**. |
| ~~(c) $f$ apprise des données~~ | — | ❌ **C1** : $N \approx 1$. Impossible à notre échelle. |

> **Règle de lecture** — chaque fois que ce document écrit $f$, $P(G_{t+1} \mid G_t, a)$ ou « simuler »,
> **substituer mentalement « (a) ou (b) »**. La notation ne crée pas la connaissance.

## 2. Ce qui est déjà là `[ÉTABLI]`

Le seul argument sérieux en faveur de cette direction : **le graphe existe**, il n'est pas à inventer.
Source : `.ai/brain-os-roadmap.md`, migrations V51–V55, V69.

| Objet du formalisme | Réalité en base | Migration |
| --- | --- | --- |
| $G = (V, E)$ | `knowledge_nodes` + `knowledge_edges` | V51 |
| Attributs de nœud $x_i$ | `type`, `domain`, `status`, `metadata` (JSONB) | V51 |
| Similarité sémantique | `embedding vector(384)` + index HNSW cosine | V52 |
| Types de relations | `RELATES_TO · SUPERSEDES · CAUSED_BY · DECISION_OF · DEPENDS_ON · IMPLEMENTS · REFERENCES` | V51 |
| Ancrage au réel | `ref_type` / `ref_id` (→ `ISSUE`, `CYCLE`, `PROJECT`) | V51 |
| Appartenance multiple | `metadata.projects = [ids]` (une **liste**, pas un parent) | — (JSONB) |

**Ce qui n'existe pas** : aucune table de **prédiction**, aucune table d'**écart prédit/réel**, aucune
notion de **temps dérivé**, aucun opérateur d'action. `CAUSED_BY` existe comme enum mais **rien ne
l'écrit** `[ÉTABLI]`.

## 3. L'état du monde

`[HYPOTHÈSE]` L'état **est** le graphe :

$$S_t = G_t = (V_t, E_t)$$

Mais un graphe seul ne suffit pas. Le document source converge (§3 « Le vrai modèle ») vers un triplet,
qu'on retient :

$$S_t = (G_t,\; M_t,\; B_t)$$

| Symbole | Nom | Contenu | Réalité |
| --- | --- | --- | --- |
| $G_t$ | **Graphe** | Entités et relations typées | ✅ existe (V51) |
| $M_t$ | **Mémoire** | Documents, historique, artefacts | 🟡 partiel — ingestion limitée aux cycles clôturés |
| $B_t$ | **Croyances** | « le projet est probablement en retard : 0.63 » | ❌ n'existe pas |

**Distinction non négociable** (POMDP, cf. [`References.md`](./References.md) §2) — le système ne
connaît **jamais** $S$, seulement une estimation :

$$\hat S_t \neq S_t$$

`[DÉDUIT]` Donc toute sortie du moteur porte une incertitude **non réductible**, et le produit doit
l'afficher. Un système qui présente $\hat S$ comme $S$ ment par construction.

## 4. Les objets

`[HYPOTHÈSE]` Chaque nœud $v_i$ (le document source l'écrit aussi $O_i$) porte six composantes :

$$v_i = (x_i,\; \dot x_i,\; \sigma_i,\; \Phi_i,\; C_i,\; K_i)$$

| Symbole | Nom | Exemple | Calculable **aujourd'hui** ? |
| --- | --- | --- | --- |
| $x$ | **État** | `progress = 0.7`, `budget = 50000` | ✅ oui — colonnes + `metadata` |
| $\dot x$ | **Vitesse / tendance** | `dette +7 %/semaine` | ✅ **oui, par SQL pur** — `cycles`, `completedAt`, `assignment_events` |
| $\sigma$ | **Incertitude** | `deadline : confiance 0.4` | ❌ non — aucune source. Inventée = fausse. |
| $\Phi$ | **Potentiel** (options ouvertes) | « peut s'étendre : Europe, API » | ❌ non — et probablement **non mesurable** (cf. [`Open_Questions.md`](./Open_Questions.md) Q3) |
| $C$ | **Contraintes** | `budget < 100k`, `deadline < 3 mois` | 🟡 partiel — dates de cycle, rien de formalisé |
| $K$ | **Causalité connue** | `dette ↑ ⟹ vélocité ↓` | ❌ non — enum `CAUSED_BY` existe, **aucun écrivain** |

> **Le point le plus rentable du document source**, et de loin : **$\dot x$**. La dérivée. Deux projets
> avec le même $x$ mais des $\dot x$ opposés ne sont **pas dans le même état** — l'un accélère, l'autre
> meurt. `[ÉTABLI]` C'est la **seule** des six composantes calculable dès maintenant, sans LLM, sans
> modèle, sans invention : les données sont déjà en base. → [`Experiments.md`](./Experiments.md) §E2.
>
> **Le piège symétrique** : quatre des six composantes ne sont **pas mesurables ici**. Les inscrire dans
> le formalisme ne les fait pas exister — ça donne juste à leur invention future une **apparence de
> rigueur**. Un modèle à 6 composantes dont 4 sont fabriquées est **moins fiable** qu'un modèle à 2
> composantes vraies (règle : [`CLAUDE.md`](./CLAUDE.md) §5).

## 5. Les relations

`[ÉTABLI]` Une arête porte déjà un type et un poids :

$$e_{ij} = (\text{type},\; w,\; \text{confiance})$$

`[HYPOTHÈSE]` L'ambition du document source est que $E$ devienne **causal** (au sens de Pearl,
[`References.md`](./References.md) §3), pas seulement associatif :

$$\text{Dette} \uparrow \;\Rightarrow\; \text{Vélocité} \downarrow \;\Rightarrow\; \text{Retard} \uparrow$$

⚠️ **Objection C2** — une flèche causale ne s'établit pas par observation d'un seul projet. Sans
contrefactuel, `CAUSED_BY` posé par un LLM n'est **pas** de la causalité : c'est de la corrélation
plausible, avec un nom qui ment. **Le nom de l'enum ne fait pas la démonstration.**

## 6. Les actions

`[HYPOTHÈSE]` Une action est un **opérateur**, pas un texte :

$$A_i : G_t \longrightarrow G_{t+1}$$

Et, puisque le monde est incertain, elle ne produit pas un monde mais une **distribution** :

$$A_i(G_t) \;\longmapsto\; P(G_{t+1} \mid G_t, a)$$

> ⚠️ **Voir §1.** Cette distribution est le cœur du modèle — et personne ne sait la calculer ici.
> Le brainstorm illustre avec `Hire(Developer) → Vélocité +30 %`. **C'est empiriquement faux** :
> loi de Brooks, 1975 ([`References.md`](./References.md) §4). L'exemple choisi pour démontrer le
> modèle est le contre-exemple canonique du domaine. Analyse → [`World_Model_Notes.md`](./World_Model_Notes.md) §3.

## 7. Les trajectoires

`[HYPOTHÈSE]` L'apport conceptuel réel du document : **on ne juge pas une action, on juge un chemin**.

$$\pi = (G_0,\; A_1,\; G_1,\; A_2,\; G_2,\; \dots,\; G_n)$$

Deux décisions peuvent atteindre le même objectif par des trajectoires de coûts très différents.

`[DÉDUIT]` **Mais l'arbre amplifie l'erreur.** Si $f$ porte une erreur $\epsilon$ par pas, un arbre de
profondeur 5 la compose. Pire : prendre l'$\arg\max$ sur des futurs simulés sélectionne
**préférentiellement les branches où le modèle se trompe le plus favorablement** — c'est le
*model exploitation* / la malédiction de l'optimiseur, un échec connu du RL basé modèle.

MuZero s'en protège par une fonction de valeur entraînée sur des **retours réels**. `[ÉTABLI]` Nous
n'avons **aucun** retour réel : la table des écarts prédit/réel n'existe pas. **Chercher dans un arbre
non calibré, c'est optimiser une fiction.**

## 8. L'évaluation — et pourquoi elle est mal posée

Le document propose une utilité scalarisée :

$$J(\pi) = \sum_{t=0}^{T} \gamma^t \Big( U(S_t) - C(a_t) - R(S_t, a_t) + O(S_t) \Big)$$

$$U = \alpha F + \beta K + \gamma P - \delta R - \epsilon C$$

**Trois objections, dont une rédhibitoire :**

1. **Goodhart** ([`References.md`](./References.md) §5) — dès qu'on optimise une somme pondérée de
   proxys, on optimise les **proxys**, pas l'objectif.
2. **Unités incommensurables** — on ne peut pas additionner des euros et de la « charge mentale » sans
   inventer un taux de change. Les poids $\alpha \dots \epsilon$ ne sont **ni mesurables, ni stables**,
   et l'utilisateur ne les connaît pas lui-même.
3. **⚠️ Contradiction interne du document source** — il pose « *Brain OS ne décide jamais à la place de
   l'utilisateur* », **et** propose de scalariser en une utilité unique. Or **choisir les poids, c'est
   prendre la décision.** Toute la substance de l'arbitrage est dans $\alpha \dots \epsilon$. Les deux
   sections se contredisent.

`[HYPOTHÈSE]` **La réponse cohérente : ne pas scalariser.** L'optimisation multi-objectif traite ce cas
depuis longtemps → calculer le **front de Pareto** (les trajectoires **non dominées**) et laisser
l'humain choisir sur le front. C'est à la fois plus rigoureux **et** la seule version fidèle au principe
« l'humain garde le choix final ».

$$\pi_a \text{ domine } \pi_b \iff \forall k,\; J_k(\pi_a) \geq J_k(\pi_b) \;\land\; \exists k,\; J_k(\pi_a) > J_k(\pi_b)$$

## 9. Le pipeline plutôt qu'une formule

`[HYPOTHÈSE]` Le document a raison sur ce point : **pas une équation, une chaîne de modules** (c'est
aussi l'architecture de LeCun 2022 — modules séparés, cf. [`References.md`](./References.md) §1).

```text
Observations
     │
     ▼
World State Builder  ──── construit Ĝt        [🟢 existe : ingestion Phase 4bis, partielle]
     │
     ▼
State Normalization                            [❌]
     │
     ▼
Constraint Evaluation                          [❌]
     │
     ▼
Candidate Actions                              [❌]
     │
     ▼
World Simulator      ──── Gt → Gt+1 → …        [❌  ⚠️ = le trou du §1]
     │
     ▼
Utility Evaluation                             [❌  ⚠️ mal posé, cf. §8]
     │
     ▼
Risk Evaluation                                [❌]
     │
     ▼
Optionality Evaluation                         [❌  ⚠️ probablement non mesurable]
     │
     ▼
Recommendation Engine                          [🟡 il existe un agent LLM + RAG]
```

`[DÉDUIT]` **Neuf modules, un seul existe partiellement.** L'intérêt d'un pipeline est de pouvoir faire
évoluer chaque module isolément — mais ça suppose que les **primitives** soient fixées. Ici, ni l'état
normalisé, ni l'action, ni la prédiction n'ont de représentation en base. **Le pipeline décrit une cible
à ~3 ordres de grandeur du code actuel** (RAG réparé le 16/07, 78 vecteurs indexés).

## 10. Ce que ce modèle ne dit pas

Honnêteté du périmètre — ce formalisme est **muet** sur :

- **D'où vient $f$** (§1). C'est le seul point qui compte, et il n'est pas traité.
- **Comment on saurait qu'il a tort.** Aucun critère de falsification n'est proposé nulle part.
  → [`Experiments.md`](./Experiments.md)
- **Ce qu'il coûte.** Aucune estimation, ni en heures, ni en tokens (`AiMeter`), ni en latence.
- **Pourquoi ne pas prendre System Dynamics** (Forrester 1961 ; Abdel-Hamid & Madnick 1991), qui
  modélise *exactement* ce domaine, à la main, depuis 35 ans. → [`Open_Questions.md`](./Open_Questions.md) Q1.
- **Le rythme d'usage réel** : $\gamma^t$ suppose un horizon. Sur quelle durée ? (C3 : ~20 points/an.)

---

**Points d'entrée :** [🔬 R&D](./README.md) · [🤖 Mode recherche](./CLAUDE.md) · [📖 Notes critiques](./World_Model_Notes.md) · [❓ Questions](./Open_Questions.md) · [🧪 Expériences](./Experiments.md)

**Dernière mise à jour :** 17/07/2026 · **v0.1** · Projet Taskforce — Metz Numeric School 2025-2026
