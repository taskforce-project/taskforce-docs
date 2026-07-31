---
id: recherche-world-model-notes
title: Notes critiques — World Model.md
doc_type: reference
statut: active
version: 1.0
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, world-model, critique, brain-os, lecun]
related:
  - "../World Model.md"
  - "./Mathematical_Model.md"
  - "./References.md"
  - "../v1/road_to_v2/Moteur_IA_World_Model_OODA.md"
---

# 📖 Notes critiques — `World Model.md`

> **Objet** — revue critique du brainstorm [`World Model.md`](../../World%20Model.md) (30 Ko, commit
> `d139202`). Appliquer [`CLAUDE.md`](../CLAUDE.md) §5 : chercher où ça casse, pas approuver.
>
> **Verdict court** : le **cadrage produit** est juste et vaut d'être gardé. Le **projet de simulateur
> mathématique n'est pas réalisable ici**, et le document ne le sait pas — parce qu'il ne pose jamais
> la seule question qui compte (§2).

## 1. Ce qui tient

| # | Idée | Pourquoi ça tient |
| - | --- | --- |
| **T1** | **$S_t = G_t$** — l'état *est* le graphe | `[ÉTABLI]` Le graphe **existe déjà** (V51/V52 + HNSW). Le formalisme décrirait du réel, pas un vœu. C'est le meilleur argument du document. |
| **T2** | **$\hat S \neq S$** + croyances $B$ | Correct et nécessaire. C'est exactement le cadre POMDP ([`References.md`](../references/Bibliotheque.md) §2) — autant le nommer. |
| **T3** | **$\dot x$ — la dérivée** | **La meilleure idée du document.** Même $x$, $\dot x$ opposés ⟹ états différents. `[ÉTABLI]` **Calculable aujourd'hui en SQL pur.** → [`Experiments.md`](../experiences/Experiences.md) §E2 |
| **T4** | **Trajectoires plutôt que résultats** | Juger un chemin, pas un point. Conceptuellement solide. |
| **T5** | **Pipeline, pas une grosse formule** | Juste — et c'est l'architecture de LeCun 2022 (modules séparés). |
| **T6** | **Optionalité $\Phi$** | Vraie intuition. ⚠ Pas une invention : c'est la **théorie des options réelles** (Dixit & Pindyck, 1994). Le champ existe. |
| **T7** | **« Multiple futures », l'humain décide** | Bon cadrage produit, cohérent avec le gate human-in-the-loop **déjà décidé**. |
| **T8** | **« Hypothèse d'ingénierie, pas un résultat démontré »** | Bonne épistémologie. Le document se marque lui-même. Il faut l'honorer, pas juste l'écrire. |

## 2. ⚠️ Le trou central : personne ne calcule $f$

**Le document construit 30 Ko sur $S_{t+1} = f(S_t, a_t)$ sans jamais demander d'où vient $f$.**

Chaque raffinement ultérieur — les six composantes de $v_i$, l'arbre de mondes, le paysage d'énergie —
**suppose $f$ résolu**. Or, sous C1–C4 ([`CLAUDE.md`](../CLAUDE.md) §3), il n'y a que deux réponses :

- **(a)** $f$ **écrite à la main** → c'est une simulation de **nos croyances**. Elle sortira ce qu'on y
  a mis. Légitime comme outil de pensée, **jamais** comme oracle.
- **(b)** $f$ **produite par un LLM** → c'est de la **génération de texte avec des chiffres dessus**.
  C'est précisément ce que le document annonce dépasser (« *Simulation over generation* »).
- **(c)** $f$ **apprise** → ❌ **C1** : $N \approx 1$. LeCun, MuZero, Dreamer apprennent sur des millions
  de trajectoires **rejouables**. Nous avons un workspace et un monde non rejouable (**C2**).

> **La ligne à retenir** — ce n'est pas un manque d'ingéniosité qui nous exclut du club LeCun, c'est
> **C2** : leurs mondes (Atari, Go, MuJoCo) sont **rejouables à coût nul**. Le nôtre non. Aucune
> quantité de formalisme ne répare ça.
>
> **Et ajouter des composantes empire le problème** : chaque dimension de plus dans $v_i$ est une
> dynamique de plus à fournir. Le document §« il manque des composantes » **enrichit un modèle dont la
> base n'est pas testée** — l'interdit de [`CLAUDE.md`](../CLAUDE.md) §5.

## 3. ⚠️ L'exemple qui réfute le document

Le document illustre son moteur, à plusieurs reprises, par :

```text
Hire Developer  →  Velocity +30   Knowledge +40   Finance −20   Risk +15
```

`[ÉTABLI]` **C'est empiriquement faux.** **Loi de Brooks** (*The Mythical Man-Month*, 1975) : ajouter
des développeurs à un projet en retard le **retarde davantage** — coût de formation, et communication
en $O(n^2)$. La vélocité **baisse d'abord**, parfois durablement.

**Pourquoi cet exemple est plus grave qu'une erreur de détail** : il **démontre le mode d'échec (a)**
en direct. L'intuition naïve est écrite à la main dans $f$, puis la « simulation » la **blanchit** en
un chiffre autoritaire assorti d'une probabilité. **La simulation n'a rien calculé : elle a habillé une
supposition.** Et le domaine avait déjà la réponse, publiée il y a 50 ans.

## 4. ⚠️ Les probabilités sont fabriquées

```text
Future A 63 %   Future B 21 %   Future C 11 %   Future D 5 %
Confidence: 94 % — Reason: Strong historical evidence
```

**D'où sort le 63 % ?** D'un LLM qui émet un nombre. Il n'est calibré contre **rien**.
`[ÉTABLI]` Il n'existe **aucune** table d'écart prédit/réel dans le schéma.

`[DÉDUIT]` Afficher un « 94 % » non calibré est **pire que ne rien afficher** : ça fabrique de la
confiance et transfère la responsabilité de la décision à un chiffre inventé. Deux décimales de
précision sur une opinion, c'est un mensonge de présentation.

> **Le comble** : le mécanisme correct **est déjà spécifié** — [Moteur_IA_World_Model_OODA](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §4
> décrit « prédire → observer le réel → **stocker l'écart** dans le Brain OS ». Il n'est pas construit,
> et `World Model.md` **ne le mentionne nulle part**. Le document réinvente en amont ce qui manque en aval.
>
> **Règle proposée** : *tant qu'on ne sait pas scorer ses prédictions, on n'affiche pas de probabilité.*
> Score de Brier / courbe de calibration d'abord ([`References.md`](../references/Bibliotheque.md) §5).

## 5. ⚠️ La fonction d'utilité se contredit elle-même

$$U = 0.4\,\text{Revenue} + 0.2\,\text{Knowledge} + 0.2\,\text{Velocity} - 0.3\,\text{Debt} - 0.1\,\text{Stress}$$

1. **Goodhart** — optimiser une somme pondérée de proxys optimise les **proxys**.
2. **Unités** — additionner des euros et de la « charge mentale » exige un taux de change inventé.
3. **La contradiction** — le document pose « *Brain OS ne décide jamais à la place de l'utilisateur* »
   **et** propose de tout réduire à un scalaire. **Choisir les poids, c'est prendre la décision.**
   Toute la substance de l'arbitrage est dans $0.4$ et $0.3$.

→ La sortie cohérente est un **front de Pareto** (trajectoires non dominées), pas un $\arg\max$.
Cf. [`Mathematical_Model.md`](../theorie/Modele-mathematique.md) §8.

## 6. ⚠️ Le paysage d'énergie est une métaphore, pas un modèle

> « *La dette technique ↑ l'énergie, la documentation ↓ l'énergie, le système cherche des états plus
> stables.* » · « *raisonner sur des invariants (comme l'énergie en physique)* »

**L'analogie est précisément fausse**, et pas seulement approximative :

- **Il n'y a aucun invariant.** En physique, les quantités conservées viennent de **symétries**
  (théorème de Noether) dans des systèmes **fermés**. Une entreprise est un système **ouvert**, loin de
  l'équilibre, peuplé d'**agents adaptatifs**, sans symétrie de translation temporelle (le marché de
  janvier ≠ celui de juin). L'argent n'est pas conservé (il est créé et détruit), la connaissance non
  plus, la confiance non plus.
- **Aucune fonction de Lyapunov, aucune preuve de convergence** n'est proposée. « Le système cherche
  des états stables » est une **affirmation esthétique**.

`[HYPOTHÈSE]` Ça **sonne** profond et n'achète **aucun** pouvoir prédictif. À déclasser explicitement
en « vocabulaire qu'on aime », ou à couper. Idem pour **§10 (théorie des jeux)** : modéliser
concurrents / marché / État comme agents avec utilités suppose d'**observer leur état et leur
utilité**. Ni l'un ni l'autre n'est accessible. C'est de la fiction avec des indices.

## 7. ⚠️ L'omission la plus coûteuse : System Dynamics

**Le document cite LeCun et réinvente Forrester — en moins bien.**

Tout ce qu'il cherche — stocks et flux, boucles de rétroaction, **délais** (« embaucher → +vélocité,
mais dans 3 mois »), la dette technique comme stock qui s'accumule — **est** la **System Dynamics**
(Forrester, *Industrial Dynamics*, **1961**). Champ mûr, outillé, avec une discipline de validation.

Et surtout : **Abdel-Hamid & Madnick, *Software Project Dynamics* (1991)** — la System Dynamics
appliquée **aux projets logiciels** : recrutement, formation, pression, qualité, retard. **Notre
domaine exact, modélisé il y a 35 ans**, y compris l'effet Brooks du §3.

`[DÉDUIT]` **Pourquoi c'est le meilleur candidat ici** : les modèles SD sont **écrits à la main**
(assumé : mode (a), pas déguisé en oracle), **petits**, **interprétables**, et se valident en
**ajustant des courbes historiques** — ce qui est faisable avec un seul workspace. **SD survit à C1.**
Le monde-modèle appris, non. → [`Open_Questions.md`](../Questions-ouvertes.md) Q1.

## 8. ⚠️ Dérive documentaire — deux moteurs concurrents dans le même vault

| | [Moteur_IA_World_Model_OODA](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) (07/07) | [`World Model.md`](../../World%20Model.md) (17/07) |
| --- | --- | --- |
| **Nature du world model** | **Mémoire / retrieval, sans gradient** | Simulateur mathématique + recherche arborescente |
| **Filiation** | Reflexion / Voyager / Generative Agents | LeCun / MuZero |
| **Ambition affichée** | « ~80 % de l'idée de LeCun **sans rien entraîner** » | Explorer des milliers de mondes |
| **Statut** | **Décidé** le 07/07 | Brainstorm, jamais rattaché |

`[ÉTABLI]` **Il y a maintenant deux réponses concurrentes à « quel est le moteur de décision du Brain
OS ? » dans le même vault**, et la plus récente **ne cite pas** la plus ancienne. Les
[Conventions](../../v1/04-engineering/Conventions_Documentation.md) §6 sont explicites : *« Major
(restructure/contredit l'existant) : créer un ADR-xxxx, puis appliquer. »* → **ADR requis**, ou
`World Model.md` reste une note de recherche sans autorité.

## 9. Problèmes de forme (à traiter séparément)

`[ÉTABLI]`, constaté dans le fichier :

- **LaTeX cassé partout** — `[  \n S_t \n ]` au lieu de `$$S_t$$`. Obsidian ne rend rien.
- **Des formules mangées par les titres markdown** — les `-` de début de ligne deviennent des `##` :
  `## 0.3Debt`, `# [ M_{hire}`, `## [ U= 0.4Revenue`. **La fonction d'utilité est illisible.**
- **Aucun front-matter** → viole [Conventions](../../v1/04-engineering/Conventions_Documentation.md) §1
  et la règle d'or n°4. Invisible aux Propriétés / au volet Tags / au RAG.
- **Fuite de contexte** : `O1 = Projet Plania` — vestige d'un autre projet.
- **C'est un transcript de chat brut**, à la racine du vault, à côté de `Brain_OS.md` et `AGENTS.md`.
  Un lecteur (ou un jury) ne distingue pas la spéculation de la doc de référence.

→ **Recommandation** : déplacer `World Model.md` dans `recherche/` comme **archive de brainstorm**
(front-matter `statut: draft`, `doc_type: reference`), le formalisme propre vivant dans
[`Mathematical_Model.md`](../theorie/Modele-mathematique.md). **Ne pas le supprimer** — c'est la trace de la
réflexion, et elle a de la valeur.

## 10. Ce que je ferais à la place — mesurer avant de simuler

Le document **commence à « simuler »**. L'ordre honnête est l'inverse, et chaque étape est
`[ÉTABLI]` faisable avec les données **déjà en base** :

| Ordre | Étape | Coût | Pourquoi d'abord |
| :-: | --- | --- | --- |
| **1** | **Dériver** — $\dot x$ par SQL : vélocité de cycle, tendance de dette, taux de complétion | ~1 j, **0 LLM** | La meilleure idée du document, gratuite, **zéro risque de fiction** |
| **2** | **Scorer les prédictions déjà faites** — les story points estimés par l'IA **sont** des prédictions ; comparer au réel. Construire la table des écarts (road_to_v2 §4) | ~2 j | Sans ça, **tout le reste est infalsifiable** |
| **3** | **Classe de référence** — « les sprints comme celui-ci finissent à 80 % » : un vrai chiffre, tiré de `cycles` | ~1 j | Bat un 63 % fabriqué, et c'est **honnête** |
| **4** | *Alors seulement* : se demander si un $f$ vaut le coût | — | La question devient répondable, avec des données |

> **Et l'angle stratégique** : le document dit « *simulation over generation* ». Mais le moat réel,
> **déjà à moitié construit**, c'est la **mémoire de ce qui s'est vraiment passé** — la Phase 4bis
> (faits tirés du **SQL**, LLM cantonné à la rédaction). Ce n'est pas de la simulation, c'est de
> l'**histoire instrumentée**. Une entreprise qui connaît son passé avec précision est plus rare, et
> plus défendable, qu'une qui simule des futurs fictifs. **Les rétros sont réelles ; l'arbre ne l'est
> pas.** Les taux de base sont ce qui prédit vraiment — et ils s'accumulent tout seuls à chaque cycle
> clôturé.

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [📐 Formalisme](../theorie/Modele-mathematique.md) · [❓ Questions](../Questions-ouvertes.md) · [🧪 Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 17/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
