---
id: recherche-a4-dynamique
title: A4 — La dynamique f (fiche approfondie)
doc_type: reference
statut: draft
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, brain-os, dynamique, transition, axiome, world-model, causalite]
related:
  - "./Axiomes.md"
  - "./A5-calibration.md"
  - "../experiences/Experiences.md"
  - "../revues/World-Model.md"
---

# 🌀 A4 — La dynamique $f$ *(fiche approfondie)*

> **Frontière solo, session 31/07 (suite).** A4 est **l'axiome central** — tout le simulateur, toute la
> planification en dépendent — et **le moins grounded**. On le pousse dans chaque retranchement.
>
> **Résultat en une ligne** : le $f$ « formule » est mort ; le seul $f$ honnête ici est **non
> paramétrique** (récupération d'épisodes passés), donc **A4 dépend de la table que A5 n'a pas encore**.
> A4 n'est pas *faux*, il est **mal posé** dans sa forme actuelle.

## 1. $f$ sur un graphe n'est pas $M \cdot S_t$

`[ÉTABLI]` L'état est un **graphe typé de dimension variable** (A1) : l'ingestion **crée des nœuds**
(Phase 4bis). Or [`World Model.md`](../revues/World-Model.md) écrit $S_{t+1} = M S_t$ (photo : matrice
des conséquences). **Une matrice $M$ de taille fixe ne peut pas ajouter un nœud** :
$\dim(G_{t+1}) \neq \dim(G_t)$ en général. → la forme algèbre-linéaire est **morte à la première
ingestion**. Le foyer mathématique correct est le **graph rewriting** / système dynamique sur graphe :

$$f : \mathcal{G} \longrightarrow \Delta(\mathcal{G}), \qquad G_{t+1} \sim f(\cdot \mid G_t, a_t).$$

## 2. Décomposer : $f = f_{\text{drift}} \circ f_{\text{action}}$

`[HYPOTHÈSE]` Deux dynamiques distinctes, que le brainstorm **confond** :

| Composante | Ce que c'est | État |
| --- | --- | --- |
| $f_{\text{drift}}(G_t, \Delta t)$ | le temps passe **sans action** : issues vieillissent, deadlines approchent, staleness monte | ✅ **groundable** — c'est **A3** ($\dot x$), arithmétique d'horloge, 0 LLM |
| $f_{\text{action}}(G_t, a)$ | une **décision** change le monde localement | ❌ le cœur du problème (§3–4) |

> **Retranchement** : la dérive est **gratuite et calculable** ; seul le terme d'action est spéculatif.
> Séparer les deux évite de jeter le bébé (drift) avec l'eau du bain (action).

Et $f_{\text{action}}$ est **local** : une action ne réécrit pas tout le graphe, elle touche un
**voisinage** du lieu de l'action. → pas un « transition du monde » global, mais une **bibliothèque
d'opérateurs locaux**, un par type d'action (créer issue, clôturer cycle, embaucher, refactorer…).

## 3. Le mur d'identifiabilité — plus profond que « pas assez de données »

Pour connaître $f_{\text{action}}$ (« qu'est-ce qu'embaucher **fait** ? ») on veut l'effet
**interventionnel** :

$$\mathbb{E}\big[G_{t+1} \mid G_t, \operatorname{do}(a)\big].$$

On n'observe que l'**associationnel** $\mathbb{E}[G_{t+1} \mid G_t, a]$. Les deux **diffèrent** parce que :

- **Confusion** `[DÉDUIT]` : l'action n'est **pas aléatoire**. On embauche **parce que** ça va mal (ou
  bien) — $P(a \mid G_t, U)$ dépend d'un $U$ (la *raison* d'agir), souvent **non observé**. La
  corrélation « embauche → résultat » est donc **confondue** par le motif de l'embauche.
- **C2** : le contrefactuel (« et si on n'avait pas embauché ») n'est **jamais** observé.

> **Le point dur** : ce n'est **pas** un manque de données que le temps réglerait. Même avec 100
> embauches observées, sans randomisation ni stratégie d'identification (instrument, expérience
> naturelle), $f_{\text{action}}$ **n'est pas identifiable** (Pearl — [`Bibliotheque.md`](../references/Bibliotheque.md) §3).
> C'est **A7** (causalité) qui revient : poser une flèche `hire → +velocity` par observation est une
> **corrélation confondue**, pas un $f$.

## 4. D'où pourrait venir $f$ ? — les quatre origines, honnêtement

| Origine | Ce que c'est vraiment | Verdict |
| --- | --- | --- |
| **(a) écrite à la main** (System Dynamics) | simulation de **nos croyances** | 🟡 survit à C1, mais **agrège** le graphe en stocks (dette totale, vélocité totale) → **contredit A1** (l'état *est* le graphe). Outil de pensée, pas oracle. |
| **(b) LLM-comme-$f$** | génération de texte chiffré | ❌ **un LLM n'est pas une fonction** (§6) ; folklore (E4) ; non calibré (A5b) |
| **(c) apprise** | gradient sur trajectoires | ❌ **C1** ($N\approx1$) |
| **(d) récupération d'épisodes** (case-based) | « la dernière fois qu'on était dans un état proche et qu'on a fait ça, voici ce qui est arrivé » | ✅ **la seule honnête** — c'est la direction **décidée** (road_to_v2 §4, lignée Reflexion/Generative-Agents) |

> **Le vrai visage de A4** `[HYPOTHÈSE]` : $f$ n'est **pas une formule à dériver**, c'est une **requête
> non paramétrique** sur une table d'épisodes $(G, a, G')$ — voisins les plus proches dans l'espace des
> trajectoires, incertitude = dispersion des voisins (dégrade **gracieusement** sous C1 : peu de voisins
> → forte incertitude, honnêtement rapportée).
>
> **Conséquence structurante** : cette table d'épisodes **n'existe pas** — c'est la **table des écarts de
> A5**. Donc **A4 est bloqué derrière A5**. La carte de dépendances de [`Axiomes.md`](./Axiomes.md) tenait :
> A5 avant A4, et pas seulement pour « juger » $f$ — **A5 fournit la matière même de $f$.**

## 5. Ce qui existe déjà — A4 n'est pas du vent pur

`[ÉTABLI]` **Un opérateur local est déjà codé et bien formé** : l'ingestion Phase 4bis (clôture de cycle
→ nœud rétro). Mieux, il est **idempotent** — le verrou V69 + l'index unique `uq_knodes_cycle_ref`
garantissent $f_{\text{clôture}} \circ f_{\text{clôture}} = f_{\text{clôture}}$. C'est un **exemple
concret** de ce à quoi ressemble un opérateur local propre. A4 = **généraliser cet objet**, pas inventer
un monolithe.

## 6. Deux fondations qui craquent

**(i) Un LLM n'est pas une fonction.** Un $f$ digne de ce nom est **stable** : $f(G,a)$ ne dépend pas du
tirage. Un LLM donne $f_\omega(G, a)$ qui **varie avec le prompt/seed $\omega$** → $\operatorname{Var}_\omega[f] > 0$.
Sans contrainte lourde (échantillonner $N$ fois, agréger — coûteux, **C4**), l'« opérateur » n'est pas
bien défini. **Mesurable** → nouvelle expérience **[E5](../experiences/Experiences.md#e5--un-llm-est-il-une-fonction-stable-)**.

**(ii) L'hypothèse de Markov est probablement fausse.** La forme $S_{t+1} = f(S_t, a_t)$ suppose que
$G_t$ **résume tout le passé utile**. Or le résultat dépend de variables **non dans le graphe** (moral
de l'équipe, marché, historique hors-cycle). Donc $f(G_t, a)$ est **intrinsèquement partiel** (revient à
**A2**, $\hat S \neq S$). `[HYPOTHÈSE]` **$S_{t+1}=f(S_t,a_t)$ est un *choix* de modélisation, pas une
loi** — et un choix dont l'hypothèse centrale est douteuse ici.

## 7. L'horizon utilisable est court

`[DÉDUIT]` Même un $f$ correct par pas (erreur relative $\delta$) **compose** l'erreur sur un horizon $H$ :
$\text{erreur} \sim (1+\delta)^H - 1$. Pour $\delta = 0{,}2$, $H=3$ → **~73 %**. Et sans **fonction de
valeur** entraînée sur des retours réels (on n'en a pas — A5b), une recherche par $\arg\max$ **sélectionne
les branches où $f$ se trompe favorablement** (malédiction de l'optimiseur, [`World-Model.md`](../revues/World-Model.md) §… / [`Modele-mathematique.md`](./Modele-mathematique.md) §7). → **horizon $\leq 2$–$3$, aucune recherche agressive.**

## 8. Le comité (5 lentilles)

| Rôle | Verdict sur A4 |
| --- | --- |
| **Chercheur IA** | $f$ = le world model. Mais les $f$ du domaine sont **appris sur des sims rejouables** ; le tien ne l'est pas → tu fais du **case-based reasoning**, pas du world model. Assume-le. |
| **Sceptique contrôle/stats** | $f_{\text{action}}$ est **non identifiable** (confondu, sans contrefactuel). Ne le *fitte* pas. Usage **descriptif** (drift) seulement. |
| **Architecte** | Un opérateur existe (ingestion, idempotent). Construis $f$ = **bibliothèque d'opérateurs locaux + table d'épisodes** pour la récupération. Pas de monolithe. |
| **Entrepreneur** | Les gens veulent « et si… ». Ils **accepteront** « voici ce qui s'est passé dans des situations passées proches » (récupération) — honnête, moins cher. Vends la **mémoire**, pas la boule de cristal. |
| **Philosophe** | $S_{t+1}=f(S_t,a_t)$ **contrebande** Markov + déterminisme-au-bruit-près. Les deux sont faux ici. A4 est une **hypothèse**, pas une loi. |

## 9. Décision de raffinement — A4 se reformule

`[HYPOTHÈSE]`

1. **Scinder** $f = f_{\text{drift}}$ (= A3, groundable, gratuit) **+** $f_{\text{action}}$ (non identifiable en général).
2. $f_{\text{action}}$ **n'est pas une formule** → **récupération non paramétrique** sur une table
   d'épisodes $(G, a, G')$. **Donc A4 dépend de A5** (cette table = la table des écarts).
3. **Formes mortes** : la matrice $M S_t$ (graphe qui grandit) ; le $f$ **appris** (C1) ; le $f$ **global**
   (il est local).
4. **Markov douteux** → $f$ intrinsèquement partiel (A2). L'énoncer comme choix, jamais comme loi.
5. **Horizon $\leq 2$–$3$**, sans $\arg\max$ agressif (pas de fonction de valeur).
6. **Le seul $f$ groundable aujourd'hui** = le prédicteur **classe-de-référence** pour l'unique action
   fréquente (« faire tourner un cycle ») = **E3**. Tout le reste est hors d'atteinte.

## 10. Test (repro)

| Test | Question | Verdict si négatif |
| --- | --- | --- |
| **[E4 — Brooks](../experiences/Experiences.md#e4--un-llm-peut-il-produire-une-dynamique-non-triviale-)** | le LLM fait-il de la dynamique non triviale ? | option (b) morte |
| **[E3 — classe de référence](../experiences/Experiences.md#e3--la-classe-de-référence-bat-elle-le-llm-)** | quelque chose bat-il le taux de base pour l'opérateur « cycle » ? | $f$-« modèle » **inutile** |
| **[E5 — stabilité (NOUVEAU)](../experiences/Experiences.md#e5--un-llm-est-il-une-fonction-stable-)** | $\operatorname{Var}_\omega[f_\omega(G,a)]$ sur variantes de prompt | un LLM **n'est pas** un $f$ |
| **E7 — Markov** *(en principe, borné par $n$)* | $G_t$ seul prédit-il le résultat aussi bien que $G_t$ + historique ? | la forme $f(G_t,a)$ est **mal spécifiée** |

## 11. Statut

- **Couche** : FRONTIÈRE. **Reformulé** : $f$ = drift (A3, ✅) + action (récupération non paramétrique, **bloquée derrière A5**).
- **Calculable ?** : $f_{\text{drift}}$ ✅ · $f_{\text{action}}$ ❌ aujourd'hui (table d'épisodes absente + non-identifiabilité). Seul substitut groundable : la classe de référence (E3).
- **Prochain coup** : A4 ne débloque rien tant que **A5** n'a pas de table d'épisodes. La vraie séquence est **A5 (émettre l'incertitude + table des écarts) → A4 (récupération dessus)**. En attendant, A4 se teste **négativement** (E3/E4/E5).

---

**Points d'entrée :** [📏 Axiomes](./Axiomes.md) · [📏 A5 (dont A4 dépend)](./A5-calibration.md) · [🧪 Experiences](../experiences/Experiences.md) · [📓 Journal](../Journal.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
