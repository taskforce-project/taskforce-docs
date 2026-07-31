---
id: recherche-questions-ouvertes
title: Questions ouvertes — R&D Brain OS
doc_type: register
statut: active
version: 1.0
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, register, world-model, brain-os, questions]
related:
  - "./CLAUDE.md"
  - "./World_Model_Notes.md"
  - "./Experiments.md"
---

# ❓ Questions ouvertes

> **Registre vivant.** Une question entre ici quand elle est **non tranchée** et qu'elle **bloque** ou
> **oriente** une décision. Elle en sort par un **ADR** ([`v1/12-decisions/`](../v1/12-decisions/Journal_Decisions_ADR.md)),
> une **expérience** ([`Experiments.md`](./Experiments.md)), ou un **abandon assumé** (avec la raison).
>
> Format : `[statut:: ouverte|en-cours|tranchée|abandonnée]` · `[prio:: P0..P3]`

## Vue d'ensemble

| ID | Question | Prio | Statut |
| --- | --- | :--: | :--: |
| [Q1](#q1--pourquoi-pas-system-dynamics-) | Pourquoi pas System Dynamics ? | **P0** | ouverte |
| [Q2](#q2--doù-vient-f-) | D'où vient $f$ ? | **P0** | ouverte |
| [Q3](#q3--le-potentiel-φ-est-il-mesurable-) | Le potentiel Φ est-il mesurable ? | P2 | ouverte |
| [Q4](#q4--deux-moteurs-concurrents--lequel-) | Deux moteurs concurrents : lequel ? | **P0** | ouverte |
| [Q5](#q5--quel-grain-pour-létat-) | Quel grain pour l'état ? | P2 | ouverte |
| [Q6](#q6--le-brain-os-est-invisible--que-montre-t-on-alors-) | Brain OS invisible : que montre-t-on ? | P1 | ouverte |
| [Q7](#q7--causalité-sans-contrefactuel--que-signifie-caused_by-) | Que signifie `CAUSED_BY` sans contrefactuel ? | P1 | ouverte |
| [Q8](#q8--construire-vers-lintérieur-ou-vers-lextérieur-) | Écosystème : vers l'intérieur ou l'extérieur ? | **P0** | ouverte |
| [Q9](#q9--quel-flywheel-vend-on-) | Quel flywheel vend-on (F1/F2/F3) ? | P1 | ouverte |

---

## Q1 — Pourquoi pas System Dynamics ?

`[statut:: ouverte]` · `[prio:: P0]` · Ouverte le 17/07/2026

**La question** — La System Dynamics (Forrester, 1961) et surtout **Abdel-Hamid & Madnick,
*Software Project Dynamics* (1991)** modélisent *exactement* notre domaine (recrutement, formation,
pression, qualité, retard) : à la main, en petits modèles interprétables, validés par ajustement de
courbes historiques. **Ça survit à C1** (pas d'apprentissage), contrairement au world model appris.

**Pourquoi ça compte** — Si la réponse est « aucune bonne raison », alors 30 Ko de brainstorm réinventent
en moins bien un champ de 60 ans, et la piste LeCun est un **détour coûteux**.

**Ce qu'il faut pour trancher** — Lire Abdel-Hamid & Madnick. Question subsidiaire, plus intéressante :
**qu'est-ce que le graphe apporte que le SD classique n'a pas ?** (Hypothèse : la SD modélise des
**agrégats** — « le stock de dette » — là où nous avons des **entités reliées et typées**. Si c'est vrai,
c'est l'apport réel du Brain OS, et il faut le formuler comme tel.)

**Bloque** : [Q2](#q2--doù-vient-f-), et toute décision d'investir dans un simulateur.

---

## Q2 — D'où vient $f$ ?

`[statut:: ouverte]` · `[prio:: P0]` · Ouverte le 17/07/2026

**La question** — $S_{t+1} = f(S_t, a_t)$ est le cœur de toute la proposition, et **rien** ne dit d'où
$f$ sort. Trois origines, deux possibles : **(a)** écrite à la main (= simulation de nos croyances),
**(b)** produite par un LLM (= texte avec des chiffres), **(c)** apprise (❌ **C1**, $N \approx 1$).

**Pourquoi ça compte** — Sans réponse, tout le reste (arbre de futurs, $J(\pi)$, paysage d'énergie) est
**décoratif**. Cf. [`World_Model_Notes.md`](./World_Model_Notes.md) §2.

**Position actuelle** `[HYPOTHÈSE]` — la seule réponse défendable est **(a) assumée** : un modèle à la
main, petit, **présenté comme un outil de pensée** et jamais comme un oracle. Ce qui ramène à
[Q1](#q1--pourquoi-pas-system-dynamics-).

---

## Q3 — Le potentiel Φ est-il mesurable ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 17/07/2026

**La question** — Le brainstorm ajoute $\Phi$ (« les portes encore ouvertes »). L'intuition est bonne et
le champ existe déjà : **options réelles** (Dixit & Pindyck, 1994). Mais : **comment on mesure $\Phi$ sur
un projet logiciel, avec les données en base ?**

**Le problème** — En finance, $\Phi$ se valorise parce que le sous-jacent a un **prix observable** et une
**volatilité estimable**. Ici : ni l'un ni l'autre. Deux entreprises à `Cash: 100k` diffèrent par leur
potentiel — d'accord, mais l'exemple donné (« *l'une a OpenAI comme partenaire* ») n'est **pas une donnée
de notre système**. Il n'est pas dans le graphe, et il ne peut pas y être.

**Risque** — $\Phi$ devient un nombre inventé qui rend n'importe quelle recommandation justifiable
*a posteriori*. Une variable non observable dans une fonction d'objectif est un **levier d'arbitraire**.

---

## Q4 — Deux moteurs concurrents : lequel ?

`[statut:: ouverte]` · `[prio:: P0]` · Ouverte le 17/07/2026

**La question** — `[ÉTABLI]` Le vault contient **deux réponses incompatibles** à « quel est le moteur de
décision du Brain OS ? » :

| | [Moteur_IA_World_Model_OODA](../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) (07/07, **décidé**) | [`World Model.md`](../World%20Model.md) (17/07, brainstorm) |
| --- | --- | --- |
| Modèle | Mémoire / retrieval, **sans gradient** | Simulateur mathématique + arbre |
| Filiation | Reflexion / Voyager / Generative Agents | LeCun / MuZero |

**Pourquoi ça compte** — C'est exactement la dérive documentaire que les règles d'or interdisent. Les
[Conventions](../v1/04-engineering/Conventions_Documentation.md) §6 imposent un **ADR** quand une note
contredit l'existant.

**Ce qu'il faut** — Soit un **ADR** qui tranche, soit `World Model.md` reste explicitement une **note de
recherche sans autorité** (ce que fait ce dossier, par défaut, en attendant).

**Position actuelle** `[HYPOTHÈSE]` — la décision du 07/07 **tient** : elle est la seule compatible avec
C1–C4. Le brainstorm du 17/07 apporte **une** chose que le 07/07 n'a pas : la **dérivée $\dot x$**
(→ [`Experiments.md`](./Experiments.md) §E2). C'est peut-être tout ce qu'il faut en garder.

---

## Q5 — Quel grain pour l'état ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 17/07/2026

**La question** — `[ÉTABLI]` L'ingestion Phase 4bis a tranché **pour l'écriture** : le grain est **le lot**
(le cycle), jamais l'événement isolé — une fiche par cycle, upsert par `refType/refId`. Est-ce **aussi**
le bon grain pour un **état** et pour une **prédiction** ?

**Tension** — Le cycle est le grain où l'on a des **données de clôture** (donc de la vérité terrain,
donc de la calibration possible : ~20 points/an, **C3**). Mais une décision stratégique (« embaucher »)
opère à un grain **au-dessus** — où l'on a encore moins de points. `[DÉDUIT]` **Plus la décision est
importante, moins on a de données pour la valider.** C'est structurel, pas un défaut d'ingénierie.

---

## Q6 — Le Brain OS est invisible : que montre-t-on alors ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 17/07/2026

**La question** — `[ÉTABLI]` Décision du 07/07 ([Moteur_IA_World_Model_OODA](../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §7) :
*« le Brain OS est le moteur ; l'utilisateur voit la route, jamais le moteur. »* Or `World Model.md`
propose d'afficher des **scénarios comparés, avec coûts, risques et probabilités** — c'est-à-dire
**le moteur**.

**Tension** — `[ÉTABLI]` Et il y a un fait produit contradictoire : **l'UI Brain OS existe** et est riche
(explorateur 2 panneaux, graphe force-directed, éditeur, régions par projet — Phases 3 / 4ter). La
décision « invisible » et le code livré **ne disent pas la même chose**.

**À trancher** — Que voit l'utilisateur exactement ? La question n'est pas théorique : elle décide de ce
qu'on démontre en soutenance.

---

## Q7 — Causalité sans contrefactuel : que signifie `CAUSED_BY` ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 17/07/2026

**La question** — `[ÉTABLI]` L'enum `CAUSED_BY` **existe** dans `knowledge_edges.relation_type` (V51) et
**aucun code ne l'écrit**. Le brainstorm veut un graphe **causal** (Pearl). Mais **C2** : le
contrefactuel n'est jamais observable sur un projet unique.

**Le risque concret** — Une arête `CAUSED_BY` posée par un LLM n'est **pas** de la causalité : c'est de
la corrélation plausible **avec un nom qui ment**. Et le nom sera lu comme une démonstration par le
prochain lecteur — humain ou agent.

**Options** — (1) renommer en `SUSPECTED_CAUSE` / porter une confiance explicite ; (2) ne l'écrire que
depuis une **intervention réelle observée** (« on a réduit la dette, la vélocité est montée ») — rare,
mais honnête ; (3) laisser mort. **Ne pas** le remplir par LLM sans (1).

---

## Q8 — Construire vers l'intérieur ou vers l'extérieur ?

`[statut:: ouverte]` · `[prio:: P0]` · Ouverte le 31/07/2026

**La question** — La vision écosystème ([`Ecosystem_Notes.md`](./Ecosystem_Notes.md)) se **déploie vers
l'extérieur** : Core → Mind → Memory → Connectors → Simulation → Execution → Marketplace / Domain Packs.
`[HYPOTHÈSE]` L'ordre de **construction** honnête est l'inverse de l'ordre d'**excitation**.

**Pourquoi ça compte** — Construire vers l'extérieur (connecteurs, agents, marketplace) **avant** d'avoir
prouvé que le cœur pauvre (mémoire F2 + signaux $\dot x$ / taux de base) porte de la valeur, c'est
empiler des couches sur une fondation non testée — l'interdit de [`CLAUDE.md`](./CLAUDE.md) §5, à
l'échelle de l'archi.

**Position actuelle** `[HYPOTHÈSE]` — séquence proposée : (1) élargir la mémoire (Phase 4bis) →
(2) benchmarks E1–E3 → (3) ADR exposition (Q6) → (4) *alors* la question d'un $f$ écrit à la main →
(∞) Mind/Marketplace. Détail : [`Ecosystem_Notes.md`](./Ecosystem_Notes.md) §6.

**Bloque** : rien techniquement, mais **oriente tout l'usage du temps R&D**. C'est la question de
priorisation, pas de faisabilité.

---

## Q9 — Quel flywheel vend-on ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 31/07/2026

**La question** — Le pitch « more usage → better models → better decisions » `[ÉTABLI]` **fusionne trois
boucles** qui n'ont ni le même volume, ni le même grain, ni la même valeur
([`Ecosystem_Notes.md`](./Ecosystem_Notes.md) §3) :

| | Améliore | Volume | Réalité |
| - | --- | --- | --- |
| **F1** préférence/style (LoRA-DPO) | la rédaction | élevé (issue) | ✅ speccé — [Data_Flywheel](../v1/road_to_v2/Data_Flywheel_et_Apprentissage.md) |
| **F2** mémoire organisationnelle | la difficulté à te remplacer | moyen (cycle) | ✅✅ **le moat**, déjà à moitié bâti |
| **F3** modèle du monde (prédire les conséquences) | le simulateur | dérisoire (~20/an, isolé) | 🟡 étranglé par C1/C3 |

**Ce qu'il faut trancher** — Le discours commercial et la roadmap doivent viser **F2** (« la mémoire de
ton entreprise, instrumentée »), **pas F3** (« un modèle qui prédit mieux »). `[DÉDUIT]` Accélérer F3
exige d'apprendre **entre** workspaces → casse l'isolation décidée (road_to_v2 §1) **et** le garde-fou
RGPD (Data_Flywheel §5). **Mauvais troc à nommer explicitement** avant qu'une slide ne promette F3.

---

**Points d'entrée :** [🔬 R&D](./README.md) · [🤖 Mode recherche](./CLAUDE.md) · [🧪 Expériences](./Experiments.md) · [📖 Notes critiques](./World_Model_Notes.md)

**Dernière mise à jour :** 17/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
