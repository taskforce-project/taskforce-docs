---
id: recherche-a6-a7-frontiere
title: A6 (Φ) & A7 (causalité) — les enrichissements non observables
doc_type: reference
statut: draft
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, brain-os, potentiel, causalite, axiome, frontiere, pearl]
related:
  - "./Axiomes.md"
  - "./A4-dynamique.md"
  - "./A5-calibration.md"
  - "../Questions-ouvertes.md"
---

# 🚧 A6 (Φ) & A7 (causalité) — les enrichissements non observables *(clôture de frontière)*

> **Frontière solo, session 31/07 (fin).** On traite A6 et A7 **ensemble** parce que c'est **le même
> geste** : attacher au graphe une grandeur **absente des données**. Les deux **s'échouent sur le même
> rocher (C2)**, et les deux ont le **même sauvetage** : une couche observable (structure / précédence),
> jamais le nombre inféré.
>
> **Résultat en une ligne** : A6 et A7 **ferment la frontière par déclassement, pas par test.** Leur
> « expérience » serait malhonnête (§4). Ce qu'on garde d'eux est **structurel**, pas causal/optionnel.

## 1. Le motif commun

`[DÉDUIT]` A6 veut un **potentiel** (valeur des futurs ouverts) ; A7 veut une **cause**. Aucun des deux
n'est dans le graphe : le potentiel est une valeur de futurs **non énumérés** (A4 bloqué) ; la cause est
un contrefactuel **non observé** (C2). **Décorer le graphe d'une grandeur non observable ne la fait pas
exister — ça donne à une invention l'apparence d'une donnée.** C'est la faute-mère de tout `World Model.md`.

---

## 2. A6 — Le potentiel $\Phi$

**Math.** La valeur d'option est $V = V(S, \sigma, K, T, r)$ — sous-jacent $S$, **volatilité** $\sigma$,
strike $K$, horizon $T$. **La valeur vient de $\sigma$** : $\sigma \to 0 \Rightarrow$ plus d'option, juste
l'intrinsèque. Or ici **ni prix $S$, ni volatilité $\sigma$**. `[DÉDUIT]` $\Phi$ est donc **dérivé de deux
choses qu'on n'a pas** — et on a déjà montré (A5) qu'on ne sait même pas estimer une **probabilité**, *a
fortiori* pas une volatilité.

**Tous les proxys candidats échouent** `[HYPOTHÈSE]` :

| Proxy proposé | Ce qu'il mesure vraiment | Verdict |
| --- | --- | --- |
| Degré / connectivité du nœud | la parenté **actuelle**, pas l'ouverture future | ❌ |
| Taille du backlog atteignable | de l'**inventaire** (travail non fait), pas de la flexibilité | ❌ |
| Runway (budget/temps restant) | une **ressource existante** (« cash ») **renommée** | ❌ (rien de neuf) |

> **Retranchement décisif** : chaque proxy est **soit** une métrique de graphe qui **ne mesure pas
> l'optionalité**, **soit** une grandeur qui existe déjà (le runway) **relabellisée**. Et surtout : $\Phi$
> **présuppose A4** (énumérer les futurs) **et A5** (les valoriser) — **doublement bloqué**. C'est
> l'axiome le **plus en aval**, donc le **plus bloqué**.

**Verdict A6 : hors modèle.** Pas « difficile » — **structurellement impossible** avec les données.

**Le fragment sauvable (honnête)** `[HYPOTHÈSE]` : **l'irréversibilité**, elle, est **structurelle et
calculable**. Un nœud vers lequel **beaucoup dépendent** est coûteux à changer → peu d'options restantes
*autour* de lui :

$$\text{irr}(v) = \deg^-_{\texttt{DEPENDS\_ON}}(v) \quad (\text{degré entrant sur les arêtes } \texttt{DEPENDS\_ON}).$$

Ce **n'est pas** $\Phi$ (ce n'est pas une valeur), mais ça capture **une moitié** de l'intuition (« c'est
devenu dur à défaire »), et c'est une **requête**. → on garde **l'irréversibilité**, on jette $\Phi$.

---

## 3. A7 — Les arêtes causales

**Math — l'échelle de Pearl** ([`Bibliotheque.md`](../references/Bibliotheque.md) §3) : association
$P(Y\mid X)$ → intervention $P(Y\mid \operatorname{do}(X))$ → contrefactuel. `CAUSED_BY` revendique le
**barreau 2/3**. On n'a que le **barreau 1** (corrélation). Grimper exige **soit** des interventions
randomisées (on ne randomise pas les décisions), **soit** un **critère de porte-dérobée** satisfait
(graphe causal correct, **aucun confondeur caché**) — une hypothèse **invérifiable** à $n=1$ (C1/C2).

> **Retranchement n°1 — A7 est l'ombre statique de A4.** $f_{\text{action}}$ (A4 §3) *est* un modèle
> causal $P(G'\mid G,\operatorname{do}(a))$ ; `CAUSED_BY` est le même objet au grain de l'arête. Même
> confusion (l'action/le changement n'est pas aléatoire), même mur. **A7 et A4 tombent ensemble.** Ce ne
> sont pas deux axiomes indépendants.

> **Retranchement n°2 — le nom ment.** Un enum `CAUSED_BY` **posé par un LLM** sera **lu comme une cause
> établie** par le prochain agent/humain. Le nom fait des **dégâts épistémiques**. `[ÉTABLI]` aujourd'hui
> **personne ne l'écrit** (`count = 0`, Q7) — donc aucun mensonge n'est encore *live*. À garder ainsi
> tant qu'il n'y a pas **provenance + confiance obligatoires** sur toute arête causale.

**La seule écriture défendable** : depuis une **intervention délibérée, loggée, avec avant/après**
(« on a réduit la dette au sprint 3, la vélocité est montée au sprint 4 ») — **barreau 2 réel**, mais
**anecdote $n=1$**, pas identification. Jamais depuis une co-occurrence inférée par LLM.

**Le fragment sauvable** `[HYPOTHÈSE]` : une couche **barreau 1** honnête — **précédence + corrélation**
(« la dette a monté, PUIS la vélocité a baissé, même projet ») — comme **générateur d'hypothèses** qu'un
humain valide, **jamais** comme assertion. Renommer `SUSPECTED_CAUSE`, confiance explicite.

---

## 4. Pourquoi A6 et A7 n'ont **pas** d'expérience (point de méthode)

`[DÉDUIT]` A5, A4, A8 ont chacun engendré une expérience (E1, E5, E6). **A6 et A7, non — et c'est
volontaire.** Leur verdict est **« hors modèle »** ; leurs « tests » ([Q3](../Questions-ouvertes.md#q3--le-potentiel-φ-est-il-mesurable-) /
[Q7](../Questions-ouvertes.md#q7--causalité-sans-contrefactuel--que-signifie-caused_by-)) sont des
**décisions** (« peut-on seulement définir la grandeur ? »), pas des mesures. **Fabriquer une expérience
pour les faire paraître actifs serait exactement la malhonnêteté que le labo interdit.** Un axiome a le
droit de recevoir un **« non »**. C'est ça, fermer une frontière : **déclasser proprement**, pas tester à tout prix.

## 5. Le comité (combiné)

| Rôle | Verdict A6 / A7 |
| --- | --- |
| **Chercheur IA** | La découverte causale et la valorisation d'option existent — mais exigent **beaucoup d'échantillons / d'interventions**, ou un modèle de valeur. Rien de tout ça ici. |
| **Sceptique stats** | Les deux sont **non identifiés** depuis des données observationnelles confondues à $n{=}1$. **Ne rien affirmer.** |
| **Architecte** | Sauvetage **léger en schéma** : `irr(v)` = degré entrant `DEPENDS_ON` ; arêtes `SUSPECTED_CAUSE` + confiance + **provenance**. |
| **Entrepreneur** | Personne ne veut « $\Phi = 0{,}63$ ». On veut « cette décision est **dure à défaire** » (irréversibilité) et « voici des **causes candidates** à vérifier ». Le sauvetage se vend mieux que l'axiome. |
| **Philosophe** | Les deux **contrebandent** un barreau 2/3 depuis des données de barreau 1. **Erreur de catégorie.** Étiqueter le barreau. |

## 6. Décision de raffinement

`[HYPOTHÈSE]`

- **A6** : $\Phi$ **hors modèle** (pas de sous-jacent, pas de volatilité, doublement bloqué A4+A5).
  **Garder** un signal d'**irréversibilité** structurel ($\deg^-_{\texttt{DEPENDS\_ON}}$) — calculable, honnête, ≠ $\Phi$.
- **A7** : `CAUSED_BY` **non identifiable** (= ombre de A4). **Interdit** de le poser par LLM. **Garder**
  une couche **précédence/corrélation** (barreau 1) = **générateur d'hypothèses** ; si jamais écrite,
  `SUSPECTED_CAUSE` + confiance + provenance **obligatoires**.

## 7. Clôture de la frontière — le verdict unifié

Les **cinq** axiomes de frontière ont été poussés. Verdict :

| Axiome | Statut final | Fragment gardé |
| --- | --- | --- |
| **A4** dynamique $f$ | ❌ prescriptif (non identifiable, C2) · dépend de A5 | drift (= A3) + opérateurs locaux idempotents |
| **A5** calibration | 🟡 A5a groundable *si* le produit émet une incertitude · ❌ A5b (C2) | biais de régression + **taux de base** |
| **A6** potentiel $\Phi$ | ❌ hors modèle | **irréversibilité** structurelle |
| **A7** causalité | ❌ non identifiable (= ombre de A4) | **précédence** barreau 1 (hypothèses) |
| **A8** trajectoires | 🟢 descriptif (E6) · ❌ prescriptif | front **rétrospectif** + ε-contrainte |

> **Le rocher commun, c'est C2** (le contrefactuel inobservable). A4, A6, A7 et A5b s'y échouent tous.
> Et **tous ont le même repli honnête** : la **structure observée + la mémoire (F2)**, jamais le futur/la
> cause **inférés (F3)**. La frontière, poussée à fond, **redit ce que les revues disaient** : le moat
> n'est pas la prédiction, c'est la mémoire instrumentée. **→ prête pour la synthèse.**

## 8. Statut

- **A6** : ❌ hors modèle · fragment `irr(v)` calculable (🟢).
- **A7** : ❌ non identifiable · fragment précédence barreau 1 (🟢), sous provenance+confiance.
- **Frontière** : **entièrement poussée** (A4/A5/A6/A7/A8). Prochain livrable = **synthèse** (candidate à promotion : ADR ou note road_to_v2).

---

**Points d'entrée :** [📏 Axiomes](./Axiomes.md) · [🌀 A4](./A4-dynamique.md) · [📏 A5](./A5-calibration.md) · [🧭 A8](./A8-trajectoires.md) · [❓ Q3/Q7](../Questions-ouvertes.md) · [📓 Journal](../Journal.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
