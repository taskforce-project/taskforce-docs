---
id: recherche-a8-trajectoires
title: A8 — Juger des trajectoires (Pareto) — fiche approfondie
doc_type: reference
statut: draft
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, brain-os, trajectoires, pareto, multi-objectif, axiome, decision]
related:
  - "./Axiomes.md"
  - "./A4-dynamique.md"
  - "../experiences/Experiences.md"
  - "../decisions/ADR-012-DRAFT-brain-os-exposition.md"
---

# 🧭 A8 — Juger des trajectoires, pas des états *(fiche approfondie)*

> **Frontière solo, session 31/07 (suite).** A8 est **le seul axiome de frontière groundable
> aujourd'hui** — sur le passé, sans $f$. On le pousse.
>
> **Résultat en une ligne** : le **principe** (ne pas écraser des valeurs incommensurables en un
> scalaire) est la partie la plus solide de tout le système ; mais la **machinerie** (front de Pareto)
> se ground seulement en **descriptif rétrospectif**, et sa version « 6 axes » est **inutile à notre $n$**.
> La forme utile n'est pas le front pur, c'est l'**ε-contrainte**.

## 1. Ce que A8 dit, et ce qu'il refuse

- **Formalisation** — une trajectoire $\pi = (G_0, A_1, G_1, \dots)$, un vecteur d'objectifs $J(\pi) \in \mathbb{R}^m$, et un **ordre partiel** (dominance de Pareto) plutôt qu'un ordre total (scalaire) :

$$\pi_a \succ \pi_b \iff \forall k,\ J_k(\pi_a) \geq J_k(\pi_b)\ \land\ \exists k,\ J_k(\pi_a) > J_k(\pi_b).$$

Le **front de Pareto** = l'ensemble des $\pi$ non dominées.

- **Ce que A8 refuse** — la scalarisation $J = \sum_k w_k J_k$. Deux raisons, dont une mathématique
  **dure** : `[ÉTABLI]` une somme pondérée linéaire ne peut atteindre que les points du **bord convexe**
  du front — elle **rate structurellement** les zones **non convexes**. Donc même en voulant scalariser,
  des poids linéaires sont **prouvablement incomplets**. (L'autre raison : les poids *sont* la décision →
  Goodhart, [`World-Model.md`](../revues/World-Model.md) §5.)

## 2. Le retranchement n°1 : « trajectoire » sur le passé ≠ ce que A8 vise

`[DÉDUIT]` A8 est censé comparer des **futurs alternatifs** du même point de décision ($\pi_a$ vs $\pi_b$).
Mais :
- générer des futurs exige $f$ → **A4, bloqué** ;
- on n'observe qu'**une** trajectoire réalisée par projet, et jamais la contrefactuelle (**C2**).

> Donc le « front de Pareto des cycles passés » **ne compare pas des alternatives** : il compare les
> **résultats réalisés de projets/cycles différents**. Ça ground la **math** de Pareto, pas l'**usage**
> (choisir un futur). A8 groundé est **descriptif** (« quels sprints passés étaient non dominés ? »),
> pas **prescriptif** (« quel chemin prendre ? »). Le prescriptif reste doublement bloqué (A4 + C2).
> → c'est du **F2 (mémoire)**, pas du F3 (prédiction). Cohérent avec l'ADR-012 (le moteur reste interne).

## 3. Le retranchement n°2 : la malédiction dimensionnelle du front

`[ÉTABLI]` En grande dimension d'objectifs, **plus rien ne domine** : la fraction de points non dominés
$\to 1$ quand $m$ croît. Le seuil est autour de $m \gtrsim \log_2 n$.

Chez nous, $n \approx 20$ cycles clôturés (C3) → $\log_2 20 \approx 4{,}3$ :

| $m$ (objectifs) | Front à $n{=}20$ | Verdict |
| :-: | --- | --- |
| **6** (le rêve World Model : finance/humain/savoir/risque/temps/dette) | $n < 2^6{=}64$ → **au-delà de la falaise** → front ≈ **presque tout** | ❌ **inutile** : « voici les 18 sprints non dominés » n'informe pas |
| **2–3** (le mesurable réel) | minorité nette | ✅ informatif |

> **Inversion piquante** : la **pauvreté de données** qui **tue A4/A5** **sauve** ici A8 — car **seuls
> 2–3 objectifs sont mesurables** (§4), ce qui garde $m$ petit et le front informatif. Mais du même coup,
> le « riche arbitrage multi-axes » promis par le brainstorm est **fiction** : on aura un front 2–3D, pas
> le rêve 6D.

## 4. Le retranchement n°3 : quels $J_k$ sont mesurables ?

`[ÉTABLI]` Sur un cycle passé, calculables depuis la base :

| Objectif $J_k$ | Source | État |
| --- | --- | --- |
| Complétion (points/comptage) | E2 | ✅ |
| Respect du délai | `MAX(issues.completed_at)` du cycle vs `cycles.end_date` | 🟡 (pas de `completed_at` sur `cycles` — proxy) |
| Débit (points livrés) | `SUM(story_points)` des issues finies | ✅ |
| **Risque · stress · dette · savoir** | — | ❌ **non mesurés** |

→ **2–3 objectifs**, pile le régime où Pareto reste lisible. Les axes qui feraient exploser la dimension
sont, par chance, précisément les non mesurables.

## 5. Le retranchement n°4 : Pareto est muet sur l'arbitrage → la vraie forme = ε-contrainte

`[DÉDUIT]` Le front donne les options non dominées, **pas** laquelle choisir — ça exige des préférences,
que A8 refuse de fixer. Donc **A8 seul ne produit aucune recommandation** : il *structure* le choix,
il ne le *fait* pas. C'est honnête (« l'humain garde le choix ») mais ça **botte en touche**.

> **La forme réellement utile n'est pas le front pur, c'est l'ε-contrainte** — comment le métier décide
> *déjà* : optimiser un objectif **sous seuils** sur les autres.
> $$\max_\pi J_1(\pi) \quad \text{s.c.} \quad J_k(\pi) \geq \varepsilon_k \ \ \forall k \neq 1.$$
> « Maximiser la vélocité **en gardant** le runway > 6 mois **et** le risque < seuil. » Les $\varepsilon_k$
> sont des **contraintes** (que le métier sait poser), pas des **poids** (qu'il ne sait pas). Et
> l'ε-contrainte **atteint les points non convexes** que la somme pondérée rate. `[HYPOTHÈSE]` C'est
> l'amélioration centrale de A8 : **contraintes, pas poids ; ordre lexicographique quand il y a une
> priorité nette** (« ne jamais crever le budget, PUIS maximiser la complétion »).

## 6. Le retranchement n°5 : fragilité à $n = 20$

`[DÉDUIT]` Le front est un **estimateur ponctuel** sans barre d'erreur. À $n\approx20$ **avec un seed
synthétique bruité**, un seul point bruité **inverse** une domination. → il faut **bootstrapper le front**
(rééchantillonner, mesurer la fréquence à laquelle chaque cycle est non dominé) avant d'affirmer « ce
sprint était non dominé ». Sans ça, A8 **sur-affirme**.

## 7. Le noyau durable — ce qui survit même bloqué

`[HYPOTHÈSE]` Le **contenu philosophique** de A8 — *refuser de réduire des valeurs incommensurables à un
seul nombre* — est **la partie la plus défendable de tout le système d'axiomes**, et elle survit même là
où la machinerie est bloquée. C'est une **posture épistémique** (respecter la pluralité des valeurs), pas
un calcul. À garder comme **étoile polaire** de tout le produit décision : *ne jamais afficher un « score
global » unique.* Même quand on ne peut pas calculer le front, on peut refuser le scalaire.

## 8. Le comité (5 lentilles)

| Rôle | Verdict sur A8 |
| --- | --- |
| **Chercheur IA** | Le RL multi-objectif existe, mais exige le modèle (A4). Sans lui : Pareto rétrospectif = **benchmarking**, pas décision. |
| **Sceptique stats** | $n{=}20$, garde $m \leq 3$ ou le front = tout. **Bootstrappe-le** ou n'y crois pas. |
| **Architecte** | C'est un `WHERE` + un **filtre de dominance** $O(n^2)$ (trivial à $n{=}20$). La valeur est dans les **ε-contraintes** (`runway > X`). |
| **Entrepreneur** | « Voici tes 3 meilleurs sprints et pourquoi » = joli rétrospectif (F2). « Choisis entre des futurs » = le rêve, mais bloqué (moteur). |
| **Philosophe** | Le vrai A8, c'est le **refus de scalariser l'incommensurable**. Garde ça, même si le calcul est bloqué. La partie la plus solide. |

## 9. Décision de raffinement — A8 se reformule

`[HYPOTHÈSE]`

1. **Garder le principe** (jamais de score global unique) — le plus durable, survit au blocage.
2. **Remplacer « front pur » par ε-contrainte / lexicographique** (contraintes, pas poids ; atteint le non convexe ; produit une décision).
3. **Forme groundable = descriptive/rétrospective** (non-domination des cycles passés sur 2–3 axes), **pas** prescriptive (bloquée par A4 + C2).
4. **Le rêve 6 axes est mort à notre $n$** (front ≈ tout dès $m \gtrsim \log_2 n$). Le mesurable (2–3 axes) le sauve — mais réduit l'ambition.
5. **Bootstrapper le front** (fragilité $n{=}20$ + seed synthétique).

## 10. Test (repro)

**Nouvelle expérience [E6](../experiences/Experiences.md#e6--le-front-de-pareto-des-cycles-passés-est-il-informatif-)** : calculer le front de Pareto des cycles clôturés sur
(complétion, respect délai, débit), **bootstrappé**.

- **Falsification** — si la **fraction non dominée** est proche de 1 (front ≈ tout), A8 **n'informe pas**
  à notre $(m,n)$ ; si une **minorité nette** domine (front stable au bootstrap), A8 tient comme **lentille
  rétrospective**.
- Faisable **dès qu'E2 tourne**, **sans A4**. C'est le seul test de frontière lançable sans débloquer autre chose.

## 11. Statut

- **Couche** : FRONTIÈRE. **Principe** ✅ (durable) · **calcul rétrospectif** ✅ (2–3 axes) · **usage prescriptif** ❌ (A4 + C2).
- **Calculable ?** : 🟢 **descriptif** (front rétrospectif, E6, sans $f$) · ❌ **prescriptif** (comparer des futurs).
- **Prochain coup** : A8 est le **seul** à offrir un livrable groundé **sans** débloquer A5/A4 — le front rétrospectif + les ε-contraintes. À prioriser si on veut un résultat R&D **montrable** vite.

---

**Points d'entrée :** [📏 Axiomes](./Axiomes.md) · [🌀 A4 (dont dépend le prescriptif)](./A4-dynamique.md) · [🧪 Experiences (E6)](../experiences/Experiences.md) · [⚖️ ADR-012](../decisions/ADR-012-DRAFT-brain-os-exposition.md) · [📓 Journal](../Journal.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
