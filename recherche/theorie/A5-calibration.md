---
id: recherche-a5-calibration
title: A5 — Calibration des croyances (fiche approfondie)
doc_type: reference
statut: draft
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, brain-os, calibration, axiome, world-model, incertitude]
related:
  - "./Axiomes.md"
  - "../experiences/Experiences.md"
  - "../Questions-ouvertes.md"
  - "../revues/World-Model.md"
---

# 📏 A5 — Calibration des croyances *(fiche approfondie)*

> **Frontière solo, session 31/07.** On pousse A5 dans chaque retranchement — parce que
> [`Axiomes.md`](./Axiomes.md) l'a désigné comme **le goulot** : sans savoir scorer une prédiction, ni
> A4 (dynamique), ni A8 (trajectoires), ni la moindre proba affichée ne se groundent.
>
> **Résultat en une ligne** : A5 **se scinde**, et même sa moitié « facile » est **bloquée en amont** —
> le système **n'émet aujourd'hui aucune croyance calibrable**. Détail ci-dessous.

## 1. De quoi parle-t-on ? — trois « croyances » qu'on confond

`[ÉTABLI]` Le système produit trois sorties chiffrées, et **aucune n'est une probabilité au sens de A5** :

| Sortie | Type | Exemple | Calibrable comme une proba ? |
| --- | --- | --- | --- |
| **Story points** | estimation ponctuelle (régression) | `story_points = 5` | ❌ un point n'a pas de distribution |
| **Score de similarité** | distance cosinus, ∈ [−1,1]→[0,1] | « déjà-vu WEB-1 **41 %** » | ❌ **erreur de catégorie** : une similarité **n'est pas** une probabilité |
| **Scores internes** | routing, smart-assign | « fast/deep », score d'assignation | ❌ ordonnancement, pas croyance |

> **Premier retranchement, et il est brutal** : A5 suppose des **croyances = probabilités attachées à
> une proposition à valeur de vérité**. Le système n'en émet **aucune**. Le « 41 % » du déjà-vu ressemble
> à une proba mais n'en est pas une — c'est un cosinus reskinné en pourcentage, ce qui est déjà **la
> faute** que A5 dénonce ([`World_Model_Notes.md`](../revues/World-Model.md) §4). **Avant de calibrer,
> il faut d'abord émettre une proba.**

## 2. La math — et le piège que « calibré » cache

**Calibration (binaire)** — un prédicteur $\hat p$ est calibré ssi

$$\mathbb{E}[\,Y \mid \hat p = p\,] = p \quad \forall p \in [0,1].$$

Diagramme de fiabilité : on *bin* les prédictions, on trace fréquence empirique vs proba prédite ; la
diagonale = calibré. Score de Brier $BS = \frac{1}{N}\sum_i (\hat p_i - y_i)^2$, avec la **décomposition
de Murphy** :

$$BS = \underbrace{\text{fiabilité}}_{\text{erreur de calibration (↓)}} \;-\; \underbrace{\text{résolution}}_{\text{pouvoir discriminant (↑)}} \;+\; \underbrace{\text{incertitude}}_{\bar y(1-\bar y),\ \text{fixe}}.$$

> **Le piège** `[DÉDUIT]` : **« calibré » est trivial à atteindre** — il suffit de **toujours prédire le
> taux de base** $\bar y$. Ce prédicteur est parfaitement calibré **et parfaitement inutile** (résolution
> nulle). Donc A5 ne doit pas viser « calibré » mais **« calibré ET tranchant »** (Gneiting : *maximiser
> la finesse sous contrainte de calibration*). Un test de calibration seul **validerait un prédicteur
> nul**. → conséquence directe sur E1 (§8).

**Régression (story points)** — un **point** $\hat s$ n'a pas de calibration définie. Il faut un
**intervalle prédictif** $[\ell, u]$ au niveau $1-\alpha$, calibré ssi la **couverture**
$\mathbb{P}(s \in [\ell,u]) = 1-\alpha$. Aujourd'hui le système émet un entier nu → on ne peut mesurer
que le **biais** $\mathbb{E}[\hat s - s]$ et la **dispersion** (MAE). **Ce n'est pas de la calibration,
c'est un diagnostic de régression.**

## 3. Opposition C1–C4 — calibrable où c'est inutile, incalculable où c'est vital

La calibration est une propriété **fréquentiste** : elle exige beaucoup de paires $(\hat p, y)$ pour
estimer $\mathbb{E}[Y\mid\hat p{=}p]$. Or le volume dépend du **grain** :

| Grain | Exemple | Volume / an | Scoreable ? |
| --- | --- | --- | --- |
| **Effort d'issue** | story points | **centaines** | ✅ (worklogs, ou proxy) |
| **Issue « finie ce cycle »** | binaire | centaines | ✅ *si* on émet la proba |
| **Résultat de cycle** | complétion % | **~20** (C3) | 🟡 réel mais rare |
| **Décision stratégique** | « embaucher ⇒ +2 sem » | **1 coup** | ❌ **C2** |

> `[DÉDUIT]` **Résultat structurel** (même forme que [Q5](../Questions-ouvertes.md)) : A5 est **groundable
> au grain le moins précieux** (effort d'issue) et **impossible au grain le plus précieux** (décision).
> Plus une croyance compte, moins on peut la calibrer.

**Le mur C2, à énoncer sans détour** — pour une croyance **contrefactuelle** (« si on embauche… »), le
résultat de l'alternative **n'est jamais observé** : on ne joue qu'**une** branche. Ce n'est pas une
pénurie de données (que le temps règle), c'est une **inobservabilité de principe**. On ne pourra
**jamais** calculer le Brier d'une décision stratégique. → **pour ces croyances, aucune proba : un
scénario.**

**Et le peu de données qu'on a est inexploitable** `[DÉDUIT]` — au grain cycle (~20/an), un bin de
fiabilité contient ~4 points. Une fréquence observée 3/4 a un **intervalle de Wilson à 95 % ≈ [0,30 ;
0,95]**. On ne peut **pas distinguer** calibré de non-calibré. La calibration au grain cycle est
**statistiquement indécidable** sous C3.

## 4. Le « réel » — que compare-t-on, exactement ?

`[ÉTABLI]` Pour un story point (une **estimation d'effort**), le « réel » honnête est l'**effort réalisé**
= $\sum \texttt{issue\_worklogs.minutes}$ (V47, `minutes INT` par entrée/issue/user).

⚠️ **Deux pièges** :
1. **Worklogs probablement non peuplés** dans le seed/scénario (le time-tracking est rarement seedé —
   **à vérifier en base**). S'ils sont vides, le seul « réel » disponible est la **latence**
   $\Delta t = \texttt{completed\_at} - \texttt{created\_at}$ — qui mesure **le temps écoulé, pas
   l'effort** (contaminé par l'attente, le WIP, le week-end). C'est un **estimateur biaisé de l'effort**.
2. Comparer story points (échelle ordinale, Fibonacci) à des minutes suppose une **fonction de
   correspondance** non triviale (un « 5 » = combien de minutes ?). → on calibre plutôt le **rang** ou on
   régresse points → minutes et on regarde les **résidus**.

## 5. La règle de score — proper, et laquelle

Si un jour on optimise un prédicteur, utiliser une **règle de score propre** (le prédicteur est
incité à dire sa **vraie** croyance) — sinon Goodhart. Choix :

- **Brier** (quadratique) : borné, doux, pénalise peu la sur-confiance.
- **Log-loss** $-\big(y\log\hat p + (1{-}y)\log(1{-}\hat p)\big)$ : **punit sévèrement le confiant-et-faux**.

> `[HYPOTHÈSE]` Pour un outil d'**aide à la décision**, la sur-confiance est le danger n°1 → **log-loss**
> (ou un score **pondéré par le coût** de l'erreur) est plus fidèle que Brier. Un « 94 % » faux doit
> faire très mal au score, sinon le système apprend à bluffer.

## 6. L'échappatoire — le prédicteur calibré existe déjà

`[ÉTABLI]` Le **taux de base d'une classe de référence** est **calibré par construction** (c'est une
fréquence empirique) : « les cycles comme celui-ci finissent à 80 % », `SELECT avg(...) ... GROUP BY`.

> **Retranchement décisif** : la question de A5 **n'est pas** « comment calibrer le LLM ? » mais **« quelque
> chose bat-il le taux de base sur un score propre ? »** ([E3](../experiences/Experiences.md#e3--la-classe-de-référence-bat-elle-le-llm-)).
> Si non → le prédicteur calibré **est une requête SQL**, et A4/A5 « modèle » sont inutiles. C'est
> l'issue la plus probable, et la moins chère.

## 7. Non-stationnarité

`[DÉDUIT]` Même calibré sur le passé, le monde est **adaptatif** (C2) : équipe, produit, marché changent.
La calibration **dérive**, et avec ~20 points/an (C3) on ne peut **pas** la ré-estimer assez vite pour
détecter la dérive. → une calibration au grain stratégique n'est même pas **stable**.

## 8. Le comité (5 lentilles)

| Rôle | Verdict sur A5 |
| --- | --- |
| **Chercheur IA** | Table-stakes : sans calibration, le world model est un générateur de nombres avec une UI. |
| **Sceptique stats** | À ton $n$, la courbe de fiabilité au grain cycle est un nuage ; rapporte des **IC de Wilson**, pas des points. |
| **Architecte** | La table des écarts = ~1 migration + écrire la prédiction à l'émission et le réel à la clôture. Cheap. Mais « réel effort » exige des **worklogs peuplés**. |
| **Entrepreneur** | Personne ne paie « confiance calibrée ». C'est un **moyen invisible**. Ne pas le vendre. |
| **Philosophe** | Une classe entière de tes croyances (contrefactuelles) est **infalsifiable** → pas de la science. Interdit de les habiller en probas. |

## 9. Décision de raffinement — A5 se scinde

`[HYPOTHÈSE]`

- **A5a — croyances scoreables** (effort d'issue, complétion de cycle). **Groundable**, mais :
  **(i)** exige que le produit **émette une proba/un intervalle**, pas un point ; **(ii)** son baseline
  obligatoire est le **taux de base** (calibré gratis) ; **(iii)** score **propre** (log-loss) ;
  **(iv)** au grain cycle, rapporter des **IC**, ne pas sur-lire.
- **A5b — croyances contrefactuelles/stratégiques** (« si on embauche… »). **Infalsifiable par C2.**
  → **aucune probabilité affichée. Jamais.** On émet un **scénario** (options, coûts, risques nommés),
  pas un nombre. Cohérent avec l'ADR-012 (le moteur reste interne) et avec « l'humain garde le choix ».

**Amélioration structurante** : avant toute calibration, **faire émettre au produit une incertitude**
(intervalle sur les story points, proba sur « fini ce cycle »). Sans ça, A5a reste au stade
**diagnostic de biais**, pas calibration.

## 10. Test (repro) — ce que devient E1

Raffinement porté dans [`experiences/Experiences.md` E1](../experiences/Experiences.md#e1--nos-prédictions-sont-elles-calibrées-) :

1. **Grain issue uniquement** (volume). Grain cycle = mesuré **pour mémoire**, avec IC de Wilson, **non concluant** par C3.
2. **Mesurer d'abord le biais** $\mathbb{E}[\hat s - s]$ et la dispersion des story points (régression) — c'est tout ce que permet un point.
3. **Réel = worklogs** si peuplés ; sinon **latence**, en **déclarant le biais**.
4. **Exiger que le modèle batte le taux de base** (résolution, pas seulement fiabilité — décomposition de Murphy). Sinon A5 « modèle » tombe.
5. **Zone interdite** : au grain décision (A5b), **ne pas produire de score** — c'est le mur C2.
6. **Bloqué en amont** : la vraie calibration (couverture d'intervalle) attend que le **produit émette des intervalles** → sous-expérience **E1b**, non lançable en l'état.

## 11. Statut

- **Couche** : FRONTIÈRE, **scindée** A5a / A5b.
- **Calculable ?** : **A5a** 🟡 (biais mesurable maintenant ; calibration vraie bloquée sur « produit émet une incertitude » ; réel-effort bloqué sur worklogs peuplés) · **A5b** ❌ **par principe** (C2).
- **Prochain coup** : vérifier en base si `issue_worklogs` est peuplé (décide si E1 mesure l'effort ou la latence), **en mode dev**.

---

**Points d'entrée :** [📏 Axiomes](./Axiomes.md) · [🧪 Experiences (E1/E3)](../experiences/Experiences.md) · [❓ Questions](../Questions-ouvertes.md) · [📓 Journal](../Journal.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
