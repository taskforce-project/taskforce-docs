---
id: recherche-axioms
title: Système d'axiomes Brain OS — spécification reproductible v0.1
doc_type: reference
statut: draft
version: 0.1
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, brain-os, axiomes, formalisme, world-model, specification]
related:
  - "./CLAUDE.md"
  - "./Mathematical_Model.md"
  - "./Experiments.md"
  - "./Open_Questions.md"
---

# 📏 Système d'axiomes Brain OS — spécification reproductible **v0.1**

> **Ce que ce document EST** : la « Brain OS Mathematical Specification » appelée par
> [`World Model.md`](../../World%20Model.md) (dernière ligne). Un jeu d'axiomes où **chaque axiome porte
> son propre test de réfutation exécutable** sur la base dev. [`Mathematical_Model.md`](../theorie/Modele-mathematique.md)
> est le **brouillon exploratoire** ; **ceci est la distillation disciplinée**.
>
> **Ce que ce document N'EST PAS** : « complet ». Et ce n'est pas un oubli — c'est la thèse du §0.

## 0. Pourquoi « complet » est le mauvais objectif (lire en premier)

Pierre a demandé un *« système d'axiomes complet et reproductible »*. Les deux mots tirent en sens opposé,
et **il faut choisir reproductible**.

Un système formel est **complet** au sens utile (cohérent + axiomes indépendants + **grounded**) seulement
si ses axiomes sont **vrais dans le domaine modélisé**. Or, sous C1–C4 ([`CLAUDE.md`](../CLAUDE.md) §3), la
plupart des axiomes candidats (il existe une transition $f$ ; les probabilités sont calibrées ; le
potentiel $\Phi$ est mesurable) ne sont **pas grounded** — ce sont des `[HYPOTHÈSE]`. **Un système
« complet » bâti sur des axiomes non grounded est exactement le piège du paysage d'énergie**
([`World_Model_Notes.md`](../revues/World-Model.md) §6) : il *a l'air* rigoureux et ne prédit rien.

> **Décision de méthode** — on ne livre pas un système complet. On livre un système **en deux couches** :
> un **NOYAU** d'axiomes grounded (peu nombreux, prouvés par une requête) + une **FRONTIÈRE** d'axiomes
> spéculatifs, **chacun étiqueté et muni de son test de réfutation**. La complétude est **différée**
> jusqu'à ce que la frontière soit *groundée* (un test passe) ou *abandonnée* (un test échoue).
> **C'est ça, « pousser le modèle à fond dans chaque retranchement » de façon honnête** : non pas tout
> affirmer, mais tout **soumettre à un test**.

**Définition opératoire de « reproductible »** (le mot qui porte tout) :

> Un axiome est **reproductible** ⟺ il existe une **requête SQL ou une mesure** que n'importe quel dev
> peut lancer sur la base dev pour le **confirmer ou le réfuter**. Pas de test → pas un axiome, une croyance.

Cela lie mécaniquement cette spec au registre [`Experiments.md`](../experiences/Experiences.md).

## Gabarit d'un axiome (à remplir pour chacun, sans exception)

```
### A<n> — <nom>
- Énoncé            : la proposition, en une phrase.
- Formalisation     : l'objet mathématique. Toujours. (consigne Pierre : « traduire en math à chaque fois »)
- Couche            : NOYAU (grounded) | FRONTIÈRE (hypothèse)
- Pour              : ce qui plaide pour.
- Contre            : ce qui plaide contre / où ça casse (opposer C1–C4).
- Axe d'amélioration: la version plus forte, ou la condition qui le sauverait.
- Test (repro)      : la requête / mesure qui tranche. Renvoie à Experiments.md.
- Calculable en l'état ? : ✅ / 🟡 / ❌ sur la base dev actuelle.
```

---

# NOYAU — axiomes grounded (un test les confirme *déjà*, ou presque)

## A1 — L'état est le graphe

- **Énoncé** : l'état du monde à l'instant $t$ *est* le graphe de connaissance, pas une abstraction posée dessus.
- **Formalisation** : $S_t = G_t = (V_t, E_t)$, chaque nœud $v_i$ portant un vecteur d'attributs $x_i$.
- **Couche** : **NOYAU**.
- **Pour** : `[ÉTABLI]` le graphe **existe en base** (`knowledge_nodes`, `knowledge_edges`, `embedding vector(384)`, HNSW — V51/V52). Le formalisme décrit du réel.
- **Contre** : un graphe capture la **structure**, pas la **dynamique**. $S_t = G_t$ ne dit rien de $S_{t+1}$ (c'est A4, frontière). Risque : croire qu'avoir l'état suffit à avoir le modèle.
- **Axe d'amélioration** : enrichir $v_i$ **seulement** avec des composantes *mesurables* (A3), pas décoratives ([`Mathematical_Model.md`](../theorie/Modele-mathematique.md) §4).
- **Test (repro)** : `SELECT count(*) FROM knowledge_nodes; SELECT count(*) FROM knowledge_edges;` → non vides ⇒ l'état-graphe est matériel, pas théorique.
- **Calculable ?** : ✅.

## A2 — Observabilité partielle

- **Énoncé** : le système ne connaît jamais l'état réel, seulement une **estimation**.
- **Formalisation** : $\hat S_t \neq S_t$ ; le raisonnement se fait sur $\hat S_t$, cadre **POMDP** ([`References.md`](../references/Bibliotheque.md) §2).
- **Couche** : **NOYAU** (conceptuel, non contestable).
- **Pour** : toute donnée du graphe est datée, partielle, parfois périmée. `[ÉTABLI]` l'ingestion ne couvre que cycles clôturés + issues finies → le graphe **sait qu'il ne sait pas tout**.
- **Contre** : reconnaître $\hat S \neq S$ ne dit **pas** de combien on se trompe. Sans A5 (croyances calibrées), $\hat S$ n'a pas de barre d'erreur.
- **Axe d'amélioration** : attacher une **fraîcheur/couverture** mesurable à $\hat S$ (ex. % d'issues ingérées, âge médian des nœuds).
- **Test (repro)** : `SELECT count(*) FILTER (WHERE ref_id IS NOT NULL)::float / count(*) FROM knowledge_nodes;` → taux d'ancrage au réel = une mesure de « à quel point $\hat S$ colle à $S$ ».
- **Calculable ?** : ✅ (la couverture ; pas encore la calibration → A5).

## A3 — Le rythme ($\dot x$)

- **Énoncé** : un nœud n'est pas caractérisé par son état seul, mais par son état **et sa tendance**.
- **Formalisation** : $v_i = (x_i, \dot x_i, \dots)$, où $\dot x_i = \frac{dx_i}{dt}$ estimé sur une fenêtre.
- **Couche** : **NOYAU** (le rythme est **calculable** ; que le rythme *prédise* est A3-bis, frontière).
- **Pour** : `[ÉTABLI]` la meilleure idée de `World Model.md`. Deux cycles à 70 % — l'un accélère, l'autre cale — ne sont pas dans le même état. Calculable **en SQL pur**, `completed_at` par issue donne la courbe.
- **Contre** : sur le seed, **~8 issues en cycle, ~4 cycles clôturés** → $\dot x$ se calcule mais ne se **valide** pas (n dérisoire, **C3**).
- **Axe d'amélioration** : burn-up par cycle (pente = $\dot x$ réel) plutôt qu'un point à mi-fenêtre.
- **Test (repro)** : **[Experiments.md E2](../experiences/Experiences.md#e2--la-dérivée-dot-x-apporte-t-elle-de-linformation-)** — requête fournie, schéma vérifié. Réfute si $\rho \leq 0$.
- **Calculable ?** : ✅ (mesure) · 🟡 (validation prédictive : bloquée par C3).

---

# FRONTIÈRE — axiomes spéculatifs (chacun vit ou meurt par son test)

> Ici, **rien n'est affirmé**. Chaque axiome est une **hypothèse datée d'un test**. C'est le programme
> R&D des prochaines sessions : en prendre un, le pousser dans le gabarit, lancer son test, le **grounder
> ou l'abandonner**. Ordre conseillé : celui des dépendances (A5 avant A4, car sans calibration on ne
> peut pas juger une transition).

## A4 — Il existe une dynamique $f$

> **Poussé à fond le 31/07 → fiche dédiée [`A4-dynamique.md`](./A4-dynamique.md).** Résultat : le $f$ « formule » est mort ; le $f$ honnête est **non paramétrique** et **dépend de A5**.

- **Énoncé** : une action transforme le monde de façon modélisable.
- **Formalisation** : $f : \mathcal{G} \to \Delta(\mathcal{G})$, $G_{t+1} \sim f(\cdot \mid G_t, a_t)$ — **graph rewriting**, **pas** $M S_t$ (une matrice ne peut pas ajouter un nœud).
- **Couche** : **FRONTIÈRE** — l'axiome central. **Reformulé** : $f = f_{\text{drift}}$ (= A3, ✅ gratuit) **+** $f_{\text{action}}$ (le problème).
- **Pour / Contre** : sans lui, pas de simulation. Mais `[DÉDUIT]` $f_{\text{action}}$ est **non identifiable** (action non aléatoire → confondue ; contrefactuel jamais observé, C2) — plus profond que « pas assez de données ». Et l'hypothèse de **Markov** derrière $f(G_t,a)$ est douteuse (variables cachées → A2).
- **Axe d'amélioration** : $f$ **n'est pas une formule** → **récupération non paramétrique** d'épisodes $(G,a,G')$ (case-based, lignée road_to_v2 §4). **Donc A4 dépend de la table d'épisodes de A5.** Un opérateur local **existe déjà** et est **idempotent** (ingestion Phase 4bis, verrou V69).
- **Test (repro)** : **[E4](../experiences/Experiences.md#e4--un-llm-peut-il-produire-une-dynamique-non-triviale-)** (Brooks) · **[E3](../experiences/Experiences.md#e3--la-classe-de-référence-bat-elle-le-llm-)** (le taux de base le bat-il ? si oui → $f$-modèle **inutile**) · **[E5](../experiences/Experiences.md#e5--un-llm-est-il-une-fonction-stable-)** (un LLM est-il seulement une **fonction** ?).
- **Calculable ?** : $f_{\text{drift}}$ ✅ · $f_{\text{action}}$ ❌ (table d'épisodes absente + non-identifiabilité). Seul substitut : la classe de référence (E3).

## A5 — Croyances calibrées

> **Poussé à fond le 31/07 → fiche dédiée [`A5-calibration.md`](./A5-calibration.md).** Résultat : A5 **se scinde**, et le goulot est en amont.

- **Énoncé** : chaque estimation porte une confiance qui *veut dire ce qu'elle dit*.
- **Formalisation** : $\mathbb{E}[\,Y \mid \hat p = p\,] = p$ (calibration binaire) ; pour un point, il faut un **intervalle** et sa **couverture** ($\mathbb{P}(s\in[\ell,u])=1-\alpha$).
- **Couche** : **FRONTIÈRE**, **scindée** — **A5a** (croyances *scoreables* : effort d'issue, complétion de cycle) = **groundable** · **A5b** (croyances *contrefactuelles* : « si on embauche… ») = **infalsifiable par C2** → **jamais de proba, un scénario**.
- **Pour / Contre** : sans calibration, tout « 94 % » ment. Mais `[ÉTABLI]` le système **n'émet aujourd'hui aucune proba** (story points = point ; « déjà-vu 41 % » = cosinus déguisé). Et « calibré » seul est **trivial** (prédire le taux de base) → viser **calibré ET tranchant** (Murphy/Gneiting).
- **Axe d'amélioration** : d'abord **faire émettre une incertitude** (intervalle/proba) par le produit ; baseline obligatoire = **taux de base** (calibré gratis) ; score **propre** (log-loss).
- **Test (repro)** : **[E1 raffiné](../experiences/Experiences.md#e1--nos-prédictions-sont-elles-calibrées-)** — grain **issue** (volume), réel = `SUM(issue_worklogs.minutes)` (V47) sinon proxy latence ; **doit battre le taux de base** ; grain cycle **indécidable** (IC de Wilson, C3) ; grain décision = **zone interdite** (C2).
- **Calculable ?** : **A5a** 🟡 (biais mesurable ; calibration vraie bloquée sur « produit émet un intervalle » + worklogs peuplés) · **A5b** ❌ par principe.

## A6 — Le potentiel $\Phi$ est mesurable

- **Énoncé** : un nœud ouvre ou ferme des options futures, quantifiables.
- **Formalisation** : $\Phi_i$ = valeur d'option (cadre **options réelles**, Dixit & Pindyck — [`References.md`](../references/Bibliotheque.md) §6).
- **Couche** : **FRONTIÈRE** (la plus fragile).
- **Pour** : intuition juste — deux états identiques peuvent avoir des futurs différents.
- **Contre** : en finance $\Phi$ se valorise via un **prix** et une **volatilité** observables ; ici ni l'un ni l'autre. L'exemple du dump (« partenaire OpenAI ») **n'est pas une donnée du système**.
- **Axe d'amélioration** : chercher un **proxy calculable** (ex. nombre de dépendances *sortantes* libres d'un nœud) — ou déclasser $\Phi$ en variable non modélisée.
- **Test (repro)** : **[Q3](../Questions-ouvertes.md#q3--le-potentiel-φ-est-il-mesurable-)** — trouver **une** définition de $\Phi$ calculable en SQL sur le graphe. Aucune trouvée ⇒ $\Phi$ reste hors modèle.
- **Calculable ?** : ❌ (aucun proxy identifié).

## A7 — Les arêtes peuvent être causales

- **Énoncé** : le graphe encode des causes, pas seulement des associations.
- **Formalisation** : $e_{ij}$ de type `CAUSED_BY`, au sens SCM de Pearl ([`References.md`](../references/Bibliotheque.md) §3).
- **Couche** : **FRONTIÈRE**.
- **Pour** : `[ÉTABLI]` l'enum `CAUSED_BY` existe déjà (V51).
- **Contre** : **C2** — le contrefactuel n'est pas observable sur un projet unique. Une arête `CAUSED_BY` posée par LLM est une **corrélation avec un nom qui ment**. `[ÉTABLI]` aucun code ne l'écrit aujourd'hui.
- **Axe d'amélioration** : ne l'écrire que depuis une **intervention réelle observée**, ou la renommer `SUSPECTED_CAUSE` + confiance.
- **Test (repro)** : **[Q7](../Questions-ouvertes.md#q7--causalité-sans-contrefactuel--que-signifie-caused_by-)** — `SELECT count(*) FROM knowledge_edges WHERE relation_type='CAUSED_BY';` (= 0 attendu) + décider la règle d'écriture avant de le remplir.
- **Calculable ?** : ❌ (aucun écrivain ; et la sémantique causale n'est pas défendable sous C2).

## A8 — On juge des trajectoires, pas des états

> **Poussé à fond le 31/07 → fiche dédiée [`A8-trajectoires.md`](./A8-trajectoires.md).** Le **seul** axiome de frontière groundable **maintenant** (sur le passé, sans $f$).

- **Énoncé** : la valeur est celle d'un **chemin**, comparée sans tout réduire à un scalaire.
- **Formalisation** : ordre **partiel** (dominance de Pareto) sur $J(\pi)\in\mathbb{R}^m$ : $\pi_a \succ \pi_b \iff \forall k,\ J_k(\pi_a) \geq J_k(\pi_b)\ \land\ \exists k,\ J_k(\pi_a) > J_k(\pi_b)$. Une somme pondérée linéaire ne touche que le **bord convexe** → incomplète.
- **Couche** : **FRONTIÈRE**. **Principe** durable · **calcul** rétrospectif seulement.
- **Pour / Contre** : évite Goodhart, respecte « l'humain garde le choix ». Mais `[DÉDUIT]` **sur le passé, on compare des résultats réalisés, pas des futurs alternatifs** (A4 + C2) → A8 groundé est **descriptif (F2)**, pas prescriptif. Et à $m \gtrsim \log_2 n$ (ici $n{\approx}20$), **le front ≈ tout** → le rêve 6 axes est **inutile** ; seuls **2–3 axes** sont mesurables, ce qui le sauve.
- **Axe d'amélioration** : **ε-contrainte / lexicographique** (contraintes « runway > 6 mois », pas poids ; atteint le non convexe) ; **bootstrapper** le front ($n{=}20$ fragile) ; garder le **principe « jamais de score global unique »** comme étoile polaire même quand le calcul est bloqué.
- **Test (repro)** : **[E6](../experiences/Experiences.md#e6--le-front-de-pareto-des-cycles-passés-est-il-informatif-)** — front de Pareto bootstrappé des cycles passés sur (complétion, délai, débit). Si fraction non dominée ≈ 1 → n'informe pas ; si minorité nette → lentille rétrospective. **Lançable sans débloquer A4/A5.**
- **Calculable ?** : 🟢 **descriptif** (E6, sans $f$) · ❌ **prescriptif** (comparer des futurs).

---

## Carte de dépendances

```text
        A1 (état=graphe) ✅        A2 (Ŝ≠S) ✅        A3 (ẋ) ✅mesure / 🟡validé
             └──────────────┬──────────────┘
                            ▼
              A5 (calibration) 🟡  ── prérequis de tout ce qui affiche une proba
                            ▼
              A4 (dynamique f) ❌  ── E3/E4 décident s'il est même utile
                     ┌──────┴──────┐
                     ▼             ▼
              A8 (trajectoires)   A6 (Φ) ❌ , A7 (causal) ❌
              🟡 passé / ❌ simulé      (frontière lointaine)
```

**Lecture** : on ne descend pas plus bas que le noyau tant qu'A5 (calibration) n'a pas de résultat.
**Prochain coup grounding = E1 puis E2** ([`Experiments.md`](../experiences/Experiences.md)). Tout le reste attend.

## Journal de version

| Version | Date | Ce qui a bougé |
| --- | --- | --- |
| v0.1 | 31/07/2026 | Création. Noyau A1–A3 posé ; frontière A4–A8 stubée avec test par axiome. Rien de grounded au-delà d'A1–A2 ; A3 mesurable, non validé. |

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [📐 Formalisme (brouillon)](../theorie/Modele-mathematique.md) · [🧪 Expériences](../experiences/Experiences.md) · [❓ Questions](../Questions-ouvertes.md)

**Dernière mise à jour :** 31/07/2026 · **v0.1** · Projet Taskforce — Metz Numeric School 2025-2026
