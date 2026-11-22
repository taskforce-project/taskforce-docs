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
> une **expérience** ([`Experiments.md`](./experiences/Experiences.md)), ou un **abandon assumé** (avec la raison).
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
| [Q10](#q10--mesurer-lattention-humaine--sur-lordinateur-seulement-ou-avec-des-données-envoyées-) | Mesurer l'attention humaine : sur la machine, ou avec des données envoyées ? | P2 | ouverte |
| [Q11](#q11--un-harnais-embarqué-pour-le-monde-physique-) | Un harnais embarqué pour le monde physique ? | P3 | ouverte |
| [Q12](#q12--demander-à-anthropic-dafficher-le-logo-de-claude-) | Demander à Anthropic d'afficher le logo de Claude ? | P3 | tranchée (10/11) |
| [Q13](#q13--les-moyens-de-la-direction--lhébergement-le-temps-un-partenaire-la-source-du-texte) | Les moyens : l'hébergement, le temps, un partenaire, la source du texte | P2 | ouverte |
| [Q14](#q14--se-brancher-à-n8n-) | Se brancher à n8n ? | P3 | ouverte |
| [Q15](#q15--quel-modèle-de-revenus-quand-le-produit-cessera-dêtre-gratuit-) | Quel modèle de revenus, quand le produit cessera d'être gratuit ? | P2 | ouverte |
| [Q16](#q16--macos--quand-et-sans-payer-apple-) | macOS : quand, et sans payer Apple ? | P3 | ouverte |
| [Q17](#q17--qui-est-le-concurrent-n1-de-taskforce-et-pour-quelle-cible-) | Qui est le concurrent n°1 de TaskForce, et pour quelle cible ? | P1 | en cours : la cible, le client test d'abord (13/11) |
| [Q18](#q18--se-brancher-à-camunda-) | Se brancher à Camunda ? | P3 | tranchée (13/11) : oui, plus tard |
| [Q19](#q19--montrer-les-applications-de-taskforce-dans-dautres-hôtes-par-mcp-apps-) | Montrer les applications de TaskForce dans d'autres hôtes, par MCP Apps ? | P3 | ouverte : après J2, avec le lot W8 (13/11) |
| [Q20](#q20--la-signature-électronique-au-sens-de-21-cfr-11200--quand-et-comment-) | La signature électronique au sens de 21 CFR 11.200 : quand, et comment ? | P2 | ouverte : une option des accords, que le client choisit, après J2 (13/11) |
| [Q21](#q21--un-fournisseur-dune-personne-passe-t-il-lévaluation-fournisseur-dun-client-gxp-) | Un fournisseur d'une personne passe-t-il l'évaluation fournisseur d'un client GxP ? | P1 | ouverte : attend le client test (13/11) |
| [Q22](#q22--les-questions-du-marché-qui-attendent-le-client-test) | Les questions du marché qui attendent le client test | P1 | ouverte : six questions de la séance n°26 (13/11) |
| [Q23](#q23--quelle-décision-de-taskforce-mérite-un-modèle-de-décision-et-sur-quelles-étiquettes-lapprendre-sans-données-de-client-) | Quelle décision de TaskForce mérite un modèle de décision, et sur quelles étiquettes l'apprendre sans données de client ? | P2 | ouverte : aucun entraînement pour l'instant, E26 et E12 attendent (16/11) |
| [Q24](#q24--qui-répond-dun-adaptateur-ou-dune-leçon-appris-chez-une-entreprise-au-sens-du-rgpd-et-de-lai-act-) | Qui répond d'un adaptateur ou d'une leçon appris chez une entreprise, au sens du RGPD et de l'AI Act ? | P2 | ouverte : attend la lecture d'un juriste ; aucun entraînement pour l'instant (16/11) |
| [Q25](#q25--comment-isoler-une-mission-sous-windows-natif-sans-prérequis-) | Comment isoler une mission sous Windows natif, sans prérequis ? | P2 | en cours : l'isolement par défaut partout, ADR-028 en projet, E27 (16/11) |
| [Q26](#q26--ce-quune-leçon-du-harnais-peut-proposer-de-changer-et-ce-quelle-ne-touche-jamais) | Ce qu'une leçon du harnais peut proposer de changer, et ce qu'elle ne touche jamais | P2 | en cours : une leçon qui durcit s'active seule ; jamais le socle, jamais une règle relâchée (16/11) |
| [Q27](#q27--la-demande-dune-preuve-sur-site-existe-t-elle-chez-les-entreprises-de-10-à-250-personnes-) | La demande d'une preuve sur site existe-t-elle chez les entreprises de 10 à 250 personnes ? | P1 | ouverte : se lit au point de décision ; les entretiens ne sont plus une condition (22/11) |
| [Q28](#q28--le-cra-et-la-licence--libre-non-monétisé-ou-édition-payante--lagpl-seule-ou-avec-une-licence-commerciale-) | Le CRA et la licence : libre non monétisé, ou édition payante ; l'AGPL seule, ou avec une licence commerciale ? | P2 | en cours : la licence commerciale et le prix avant toute annonce large, le juriste avant l'édition payante ; quelle licence et quel prix restent ouverts (22/11) |
| [Q29](#q29--le-format-du-dossier--saligner-sur-la-rfc-8785-et-le-brouillon-de-lietf-ou-garder-le-sien-) | Le format du dossier : s'aligner sur la RFC 8785 et le brouillon de l'IETF, ou garder le sien ? | P2 | tranchée (22/11) : aucun format propre ; RFC 8785, in-toto et DSSE à instruire par E34 |
| [Q30](#q30--le-sort-des-surfaces-gelées-et-quand-le-décider) | Le sort des surfaces gelées, et quand le décider | P2 | en cours : le sort se décide au point de décision, sur l'usage observé (22/11) |
| [Q31](#q31--le-témoin--où-ancrer-lempreinte-de-tête-du-dossier-hors-de-lopérateur-) | Le témoin : où ancrer l'empreinte de tête du dossier, hors de l'opérateur ? | P1 | en cours : l'empreinte de tête dans la pull request quand il y en a une ; le reste ouvert (22/11) |
| [Q32](#q32--qui-écrit-les-processus-et-les-paquets-de-règles-et-que-donne-taskforce-comme-exemples-) | Qui écrit les processus et les paquets de règles, et que donne TaskForce comme exemples ? | P2 | en cours : TaskForce fournit le moteur et des exemples marqués ; qui publie les paquets reste ouvert (22/11) |
| [Q33](#q33--la-classe-dune-écriture-externe--qui-la-déclare-et-comment-prouver-son-action-inverse-) | La classe d'une écriture externe : qui la déclare, et comment prouver son action inverse ? | P1 | en cours : ADR-030 en projet, E33 ; hors de TaskForce, outil par outil, après la v1 (22/11) |
| [Q34](#q34--à-qui-appartient-le-code-et-comment-le-garder-cessible-) | À qui appartient le code, et comment le garder cessible ? | P1 | en cours : tous les droits chez un seul titulaire ; l'inventaire reste à faire (22/11) |
| [Q35](#q35--le-vérificateur--un-autre-modèle-suffit-il-ou-faut-il-un-juge-qui-nest-pas-un-agent-) | Le vérificateur : un autre modèle suffit-il, ou faut-il un juge qui n'est pas un agent ? | P2 | ouverte : le vérificateur est écrit, pas construit en v1 ; E36 (22/11) |
| [Q36](#q36--que-garde-le-dossier-dune-machine-quand-laction-nattend-pas-un-accord-) | Que garde le dossier d'une machine, quand l'action n'attend pas un accord ? | P3 | ouverte : rien ne se construit avant le point de décision (22/11) |
| [Q37](#q37--lapp-web-hébergée--quel-seuil-rouvrirait-un-hébergement-pour-des-clients-) | L'app web hébergée : quel seuil rouvrirait un hébergement pour des clients ? | P2 | ouverte : le seuil revient à la Présidence, aucun n'est fixé (22/11) |
| [Q38](#q38--action-de-la-présidence--poser-sans-campagne-la-question-de-fait-de-la-séance-n29) | Action de la Présidence : poser, sans campagne, la question de fait de la séance n°29 | P2 | ouverte : action de la Présidence, sans date (22/11) |
| [Q39](#q39--action-de-la-présidence--lire-une-fois-reddit-et-linkedin-connectée-avec-les-mots-de-la-recherche-d5) | Action de la Présidence : lire une fois Reddit et LinkedIn, connectée, avec les mots de la recherche D5 | P3 | ouverte : action de la Présidence, sans date (22/11) |

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
**décoratif**. Cf. [`World_Model_Notes.md`](./revues/World-Model.md) §2.

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
(→ [`Experiments.md`](./experiences/Experiences.md) §E2). C'est peut-être tout ce qu'il faut en garder.

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

**La question** — La vision écosystème ([`Ecosystem_Notes.md`](./revues/Ecosysteme.md)) se **déploie vers
l'extérieur** : Core → Mind → Memory → Connectors → Simulation → Execution → Marketplace / Domain Packs.
`[HYPOTHÈSE]` L'ordre de **construction** honnête est l'inverse de l'ordre d'**excitation**.

**Pourquoi ça compte** — Construire vers l'extérieur (connecteurs, agents, marketplace) **avant** d'avoir
prouvé que le cœur pauvre (mémoire F2 + signaux $\dot x$ / taux de base) porte de la valeur, c'est
empiler des couches sur une fondation non testée — l'interdit de [`CLAUDE.md`](./CLAUDE.md) §5, à
l'échelle de l'archi.

**Position actuelle** `[HYPOTHÈSE]` — séquence proposée : (1) élargir la mémoire (Phase 4bis) →
(2) benchmarks E1–E3 → (3) ADR exposition (Q6) → (4) *alors* la question d'un $f$ écrit à la main →
(∞) Mind/Marketplace. Détail : [`Ecosystem_Notes.md`](./revues/Ecosysteme.md) §6.

**Bloque** : rien techniquement, mais **oriente tout l'usage du temps R&D**. C'est la question de
priorisation, pas de faisabilité.

---

## Q9 — Quel flywheel vend-on ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 31/07/2026

**La question** — Le pitch « more usage → better models → better decisions » `[ÉTABLI]` **fusionne trois
boucles** qui n'ont ni le même volume, ni le même grain, ni la même valeur
([`Ecosystem_Notes.md`](./revues/Ecosysteme.md) §3) :

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

## Q10 : Mesurer l'attention humaine : sur l'ordinateur seulement, ou avec des données envoyées ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°1](./conseil/seances/2026-10-26-premiere-regle.md), R3

- **La question** : la mesure nord retenue (temps d'attention humaine par résultat accepté, temps de cycle) peut se
  calculer sur l'ordinateur de chaque personne, ou à partir de données envoyées à TaskForce.
- **Pourquoi ça compte** : `[ÉTABLI]` l'app promet aujourd'hui de n'envoyer aucune donnée d'usage (site, `llms.txt`).
  La Présidence indique qu'un envoi serait possible techniquement. Comparer les équipes et améliorer le produit
  demanderait des données agrégées ; la promesse locale est un argument de confiance.
- **Position actuelle** : `[HYPOTHÈSE]` mesurer d'abord sur l'ordinateur (E9) ; un envoi éventuel serait opt-in, avec
  consentement explicite, données agrégées, et mise à jour de la politique de confidentialité et du site.
- **Ce qu'il faut pour trancher** : le résultat d'E9, puis une décision de la Présidence (ADR si l'envoi est retenu).

---

## Q11 : Un harnais embarqué pour le monde physique ?

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°2](./conseil/seances/2026-10-27-vision.md), I2

- **La question** : les trois pièces du harnais (règles, preuve, décision humaine) peuvent-elles vivre dans une machine
  ou un robot, sans réseau, avec des décisions en millisecondes ?
- **Pourquoi ça compte** : le premier cas d'usage (un standard de communication embarqué) touche déjà des systèmes qui,
  demain, exécuteront ces protocoles eux-mêmes. La Présidence y voit une piste « très intéressante » : un TaskForce
  embarqué.
- **Position actuelle** : `[HYPOTHÈSE]` horizon, pas chantier ; rien à construire avant que la v2 tienne sur le
  logiciel.
- **Ce qu'il faut pour trancher** : des clients de la niche B qui le demandent, et une contrainte de temps réel chiffrée.

---

## Q12 : Demander à Anthropic d'afficher le logo de Claude ?

`[statut:: tranchée]` · `[prio:: P3]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°8](./conseil/seances/2026-10-29-recette-132.md), R53

- **La question** : TaskForce montre Claude Code par son seul nom (R53, retenue). Faut-il demander à Anthropic
  l'autorisation d'afficher le logo de Claude, dans l'app et sur le site ?
- **Pourquoi ça compte** : `[ÉTABLI]` les conditions d'Anthropic (en vigueur depuis le 01/08/2024) n'autorisent ses
  marques que de la façon qu'il permet, sans parrainage ni affiliation sous-entendus, et ne décrivent aucun programme
  de partenaires. La Présidence avait voulu le logo sur le site le 19/10/2026.
- **Position actuelle** : `[HYPOTHÈSE]` le nom seul tant qu'aucune autorisation écrite n'existe ; la demande est au choix
  de la Présidence.
- **Ce qu'il faut pour trancher** : la décision de la Présidence de demander ou non, puis la réponse d'Anthropic.
- **Tranchée par la Présidence le 10/11/2026** ([séance n°21](./conseil/seances/2026-11-10-premier-client-e20.md)) : « Le logo Anthropic est open source, on peut l'utiliser sans problème. » ; « C'est juste un logo d'information, donc il n'y a pas de problème à ce niveau-là. » Aucune demande à Anthropic ; le logo est dans l'app depuis la 1.14.0.

## Q13 : Les moyens de la direction : l'hébergement, le temps, un partenaire, la source du texte

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°10](./conseil/seances/2026-10-29-intelligence-possedee.md), R60 à R65

- **La question** :
  - Ce que coûte l'hébergement actuel, et jusqu'à quand il tient.
  - Combien d'heures par semaine la Présidence peut donner.
  - Qui serait le partenaire de conception, dans le secteur du premier cas d'usage.
  - D'où vient le texte apporté à la séance n°10.
- **Pourquoi ça compte** : `[DÉDUIT]` les paliers 0 à 3 de la séance ne coûtent que du temps ; le palier 4 demande un
  partenaire ; si le texte vient d'un appel d'investisseurs, y répondre devient une suite.
- **Position actuelle** :
  - `[ÉTABLI]` les machines virtuelles de l'école s'arrêtent (spécification de la v2, ordre de livraison décidé le
    28/10/2026) : la webapp a besoin d'un autre hébergement.
  - `[HYPOTHÈSE]` l'offre toujours gratuite d'Oracle (2 OCPU, 12 Go) pourrait la porter pour 0 €, à vérifier : images
    arm64, capacité disponible, mémoire réelle de la prod à mesurer ; sinon un petit serveur, de l'ordre de dix euros
    par mois (devis à refaire).
- **Réponses de la Présidence, le 30/10/2026** :
  - L'hébergement : « pour l instant aucun mais je prendrais un VPS OVH des que possible, VPS-3 pour etre precis ».
    `[ÉTABLI]` Le VPS-3 d'OVH : 6 vCores, 12 Go de mémoire, 100 Go de disque, 10,40 € HT par mois (page d'OVH lue le
    19/10/2026, avec l'empreinte de la prod mesurée le même jour : environ 2,2 Go).
  - Reformulées, les trois autres réponses : le temps, « j y passe mes journee » ; le texte, « un gars de YC qui disais
    ca dans un poste [...] sur instagram, donc oui on pourrait leur ecrire » ; le partenaire de conception, plus tard.
  - Les mots de la cible (R65), d'après la Présidence : audit, traçabilité, IQ, OQ, PQ, réglementation, référentiel.
    `[DÉDUIT]` IQ, OQ et PQ sont les étapes de la qualification d'un équipement ou d'un système dans les industries
    réglementées (pharmacie, dispositifs médicaux) : à confirmer avec la Présidence.
  - L'auteur du post, d'après la Présidence : Jon Xu. `[ÉTABLI]` Jon Xu est General Partner de Y Combinator depuis mai
    2025 ([YC](https://www.ycombinator.com/blog/welcome-jon-and-andrew)). Le post lui-même n'a pas été retrouvé en ligne
    par le secrétariat : à citer avec son lien quand la Présidence l'a.
- **Ce qu'il faut pour trancher** : la date du VPS ; le lien du post.
- **Réponses de la Présidence, le 01/11/2026** ([séance n°15](./conseil/seances/2026-11-01-feuille-de-route.md), R91) :
  - la webapp reste en ligne et reçoit chaque release, mais on n'y teste rien pour l'instant : « pas de serveur, pas
    d'API Claude ou autre, pas de connexion possible avec des agent ou autre a moins de payer » ;
  - l'app desktop continue de se connecter par la webapp ; elle est le banc d'essai, avec Claude Code et Ollama.
- **Réponses de la Présidence, le 01/11/2026, après la release 1.7.0** :
  - les machines de l'école s'arrêtent le 31/12/2026 ;
  - l'adresse de l'hébergeur pour les mentions légales attend le VPS : « on attend le VPS globalement ».
- `[DÉDUIT]` Le VPS doit être en service avant le 31/12/2026, avec les comptes, la webapp, l'API et les sauvegardes :
  sans lui, une nouvelle installation de l'app desktop ne peut plus se connecter, puisqu'elle passe par la webapp.
- **Ce qui manque encore** : la date de mise en service du VPS.
- **10/11/2026** ([séance n°21](./conseil/seances/2026-11-10-premier-client-e20.md), R149) : un premier client en dépend. Le Conseil demande la date du VPS ; s'il n'est pas en service au 15/12/2026, l'app desktop doit pouvoir se connecter sans la webapp.
- **Réponse de la Présidence, le 10/11/2026** : R149 reportée après J2 et les vidéos de démo (« on verra une fois que J2 sera sorti ») ; plutôt un grand fournisseur qu'un VPS : « GCP, ça me paraît correct », la base de données à chiffrer. `[ÉTABLI]` L'app desktop se connecte par ce serveur (`desktop/src/account.ts`) : l'échéance du 31/12/2026 tient pour elle aussi.
- **13/11/2026** ([séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), R182, R183, R184) : le partenaire de
  conception a désormais un profil : l'éditeur ou l'intégrateur de logiciel de laboratoire ou de dispositif médical, de 10 à 50
  personnes, ou un cabinet de validation qui vend au forfait. Le réseau GxP de la Présidence ouvre les premiers entretiens, quatre
  sur dix au moins hors de lui. `[DÉDUIT]` Les objectifs du premier trimestre (trois partenaires actifs en janvier) dépendent d'un
  serveur en service avant le 31/12/2026, puisque l'app desktop se connecte par lui. R63 fixait trente jours pour trouver un
  partenaire dans un secteur régulé : le délai tombe le 28/11/2026, à trancher par la Présidence.

## Q14 : Se brancher à n8n ?

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 01/11/2026 · issue du [Conseil, séance n°15](./conseil/seances/2026-11-01-feuille-de-route.md), R99 (point 5, reporté)

- **La question** : faut-il ouvrir le point de décision de TaskForce à n8n, pour que ses agents demandent la décision aux
  règles d'un espace et écrivent au dossier ?
- **Pourquoi ça compte** : `[ÉTABLI]` n8n se présente comme une plateforme pour construire et déployer des agents IA et
  des flux, avec des accords humains, des journaux d'audit et l'auto-hébergement ([GitHub](https://github.com/n8n-io/n8n),
  lu le 01/11/2026). `[DÉDUIT]` Se brancher ferait de TaskForce la couche de règles et de preuve d'outils déjà en place ;
  ne pas le faire garde TaskForce entière, sans dépendre d'un autre éditeur.
- **Position actuelle** : la Présidence, le 01/11/2026 : « On va pas se brancher a n8n je pense, enfin jsp a voir ».
- **Ce qu'il faut pour trancher** : le point de décision ouvert de R99, construit en J5 pour les agents que TaskForce
  connaît ; puis une demande réelle d'un client qui utilise n8n.

## Q15 : Quel modèle de revenus, quand le produit cessera d'être gratuit ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 01/11/2026 · issue du [Conseil, séance n°15](./conseil/seances/2026-11-01-feuille-de-route.md), R106

- **La question** : double licence (l'AGPL, et une licence commerciale), open core (des fonctions d'entreprise payantes),
  installation et support payants, ou une version hébergée ?
- **Pourquoi ça compte** : la Présidence, le 01/11/2026 : « Pour l instant c est gratuit mais ca va pas le rester ».
  `[ÉTABLI]` Stripe et les offres payantes ont été retirés le 18/10/2026.
- **Position actuelle** : rien de payant ne se construit avant J9 ; les trois options s'instruisent avant J8 et se
  testent pendant les démos ; le cœur reste sous AGPL (R106).
- **Ce qu'il faut pour trancher** : les réponses des démos de J8 ; une vérification juridique, puisque la double licence
  suppose de détenir les droits sur tout le code.
- **La Présidence, le 10/11/2026** : le coût du serveur viendra avec le monde (« ça va commencer à chiffrer s'il y a beaucoup de monde qui vont dessus »), sans revenu à ce stade ; le prix se discute au moment d'ouvrir l'app à tous, après J2 et les vidéos.
- **13/11/2026** ([séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), R185) : quatre hypothèses posées, rien de
  payant avant J9. H1, le cœur reste gratuit sous AGPL ; H2, la part payante éventuelle porte sur la preuve et le soutien du
  fournisseur (un pack de validation par version, un canal de support), par entreprise et par an, pas par siège ; H3,
  l'installation et l'aide à la validation par la Présidence, que sa capacité borne ; H4, une version hébergée plus tard.
  `[ÉTABLI]` Les repères publics, lus le 13/11/2026 : Qualio « Plans start at $25,000 per year » ([Qualio](https://www.qualio.com/pricing)) ;
  Ketryx gratuit pour les entreprises avant mise sur le marché qui ont levé moins de 2 M$ ([Ketryx](https://www.ketryx.com/pricing)) ;
  Linear 10 et 16 $ par personne et par mois ([Linear](https://linear.app/pricing)) ; aucun prix public chez Camunda, Kneat ou
  ValGenesis. Deux questions entrent dans chaque entretien : ce que coûte aujourd'hui la validation d'une modification, et si un
  pack de validation se paierait.

## Q16 : macOS : quand, et sans payer Apple ?

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 10/11/2026 · issue du [Conseil, séance n°21](./conseil/seances/2026-11-10-premier-client-e20.md), R150

- **La question** : faut-il une version macOS de l'app desktop, et quand, tant que la Présidence ne veut pas payer l'adhésion d'Apple ? Ses mots : « temps que je suis pas paye je veux pas passer la certif IoS qui coute un bras pour pouvoir publier quelque chose sur l'Apple store ».
- **Pourquoi ça compte** : `[ÉTABLI]` un `.exe` ne s'exécute pas sur macOS ; l'adhésion d'Apple coûte 99 dollars par an et donne la notarisation ([Apple](https://developer.apple.com/programs/), lu le 10/11/2026) ; sans elle, l'app s'ouvre une première fois par « Ouvrir quand même » ([Apple](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unknown-developer-mh40616/mac), lu le 10/11/2026) et ne se met pas à jour seule ([Electron](https://www.electronjs.org/docs/latest/api/auto-updater), lu le 10/11/2026).
- **Position actuelle** : R150, en attente de la Présidence : la question va au premier client ; une version non signée pour les Mac à puce Apple s'il travaille sur Mac ; l'adhésion au premier contrat payé.
- **Ce qu'il faut pour trancher** : les machines du premier client ; la décision de la Présidence sur R150.
- **Décision de la Présidence, le 10/11/2026** (R150 modifiée) : le premier client possible travaille sur Mac, mais ne recevra pas de version non signée (« j'ai pas envie d'aller leur faire désactiver des trucs dans leurs paramètres ») ; une démo d'abord, puis l'adhésion d'Apple s'il montre une vraie intention. `[ÉTABLI]` Le Mac App Store impose le bac à sable et interdit de télécharger des ressources qui ajoutent une fonction ([Apple](https://developer.apple.com/app-store/review/guidelines/), règle 2.4.5, lue le 10/11/2026) ; la même adhésion permet la distribution directe, notarisée.


## Q17 : Qui est le concurrent n°1 de TaskForce, et pour quelle cible ?

`[statut:: en-cours]` · `[prio:: P1]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°24](./conseil/seances/2026-11-13-depasser-camunda.md), R164

- **La question** : la Présidence tient Camunda pour le concurrent n°1 (« je pense que c'est notre concurrent n1 en fait »). Sur
  quelle cible ? Les documents disent « n'importe quelle entreprise » (R103, ADR-022), choisissent le catalogue pour « une
  entreprise de 10 à 500 personnes » (12/11) et jouent E20 sur l'intégration d'un module dans un logiciel ; ils ne disent pas qui
  configure TaskForce, avec ou sans développeur.
- **Pourquoi ça compte** : le pitch (TF-J2-1), la page de comparaison (R163) et l'ordre des emprunts (R165) en dépendent.
  `[ÉTABLI]` Camunda vise les grandes organisations : ses nouveaux clients de plus de 10 000 salariés sont son segment le plus
  rapide ([Camunda](https://camunda.com/press-releases/camunda-closing-in-on-200m-in-arr-doubling-revenue-in-record-time/), 04/08/2026) ;
  Forrester le juge le mieux adapté aux grandes entreprises ([Camunda](https://camunda.com/press_release/camunda-named-a-leader-in-adaptive-process-orchestration-software-evaluation-q3-2026/), 25/09/2026) ;
  sa page des prix n'en affiche aucun ([Camunda](https://camunda.com/pricing/), lu le 13/11/2026). Microsoft et n8n publient leurs
  prix ([Copilot Studio](https://www.microsoft.com/en-us/microsoft-365-copilot/pricing/copilot-studio), [n8n](https://n8n.io/pricing/), lus le 13/11/2026).
- **Réponse de la Présidence, le 13/11/2026 au soir** (R164 retenue) :
  - la cible en une ligne, que l'agent lui avait proposée, et qu'elle tient « à peu près » : « des entreprises de 10 à 500
    personnes, sans développeur dédié pour configurer, dont le premier travail est la livraison logicielle et les documents » ;
    ses mots : « Bon bah la cible en une ligne, tu l'as aussi, à peu près, hein. » ;
  - des marchés plus complexes ensuite : « on peut peut-être faire la même chose, mais nous partir sur vraiment des marchés un
    petit peu plus complexes » ; sur IQ, OQ et PQ : « j'ai déjà un petit peu d'expérience là-dessus, donc on pourra limite presque
    tester en fait » ;
  - sur Camunda : « si on est concurrent par rapport à Camunda, c'est pas non plus dégueu. Ils ont 700 clients, mais il y a
    certainement des millions d'entreprises encore qui n'ont pas ce genre de choses et qui demandent ce genre de choses. »
- **Position actuelle** : `[DÉDUIT]` sur la cible tenue « à peu près », sans développeur dédié pour configurer, Camunda, dont le code
  est le « cœur » et le low-code une option ([billet du 08/12/2023](https://camunda.com/blog/2023/12/pro-code-low-code-role-of-camunda/)),
  reste la barre de la rigueur d'exécution, pas le concurrent le plus proche ; Microsoft et n8n le restent. `[HYPOTHÈSE]` Il le
  redevient sur les marchés plus complexes, si leurs clients ont des développeurs.
- **Ce qu'il faut pour trancher** : E14, élargie le 13/11, avec la question « à quoi le compareriez-vous ? » posée avant toute
  formule, et les noms cités ; le marché, ses chiffres et la part visée, à la séance n°26.
- **13/11/2026** : la Présidence tient « à peu près » la cible proposée : « des entreprises de 10 à 500 personnes, sans
  développeur dédié pour configurer, dont le premier travail est la livraison logicielle et les documents », les métiers régulés
  ensuite. `[ÉTABLI]` Elle compte 47 477 entreprises du logiciel de 10 à 249 personnes dans l'UE et 5 703 en France
  ([Eurostat](https://ec.europa.eu/eurostat/databrowser/view/sbs_sc_ovw/default/table?lang=en), 2024) ; la classe de 250 à 499
  n'est pas publiée. `[HYPOTHÈSE]` Sur la niche régulée, le concurrent n'est pas Camunda, qui n'en dit rien sur ses pages, mais le
  spécialiste validé (Veeva, Kneat, ValGenesis, Qualio), le cabinet de validation, et les documents faits à la main ; sur le
  logiciel des dispositifs médicaux, Ketryx ([séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), R181).
- **Décision de la Présidence, le 13/11/2026 au soir** ([séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), R180 à
  R187 retenues sauf les délais) : la cible passe d'abord par le client test, le premier client possible, quand l'app est livrée et
  tient de gros volumes de données. Ses mots : « Tout me convient, sauf les delais » ; « me faut l'app avant evidemment qu'on
  testera avec des gros batch de donnees ». La Présidence revient avec ses retours, et le Conseil en discute. E14 et les entretiens
  de R186, qui devaient trancher Q17, attendent ce retour (Q22).

## Q18 : Se brancher à Camunda ?

`[statut:: tranchée]` · `[prio:: P3]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°24](./conseil/seances/2026-11-13-depasser-camunda.md), confrontation 3

- **La question** : faut-il instruire TaskForce comme couche de règles et de preuve qu'un processus Camunda appelle par MCP, et
  l'import des processus d'un client qui a déjà Camunda ?
- **Pourquoi ça compte** : `[ÉTABLI]` Camunda est client et serveur MCP, et un point d'arrêt humain peut retenir l'appel d'un outil
  ([Camunda](https://camunda.com/blog/2026/08/three-ways-camunda-speaks-mcp-and-why-the-direction-matters/), 18/08/2026) ; son journal
  d'audit ne décrit aucune garantie d'intégrité ([Camunda](https://docs.camunda.io/docs/components/audit-log/overview/), lu le
  13/11/2026). `[DÉDUIT]` Se brancher ferait de TaskForce la règle et la preuve des agents de Camunda chez ses clients ; ne pas le
  faire garde TaskForce entière, sans dépendre d'un éditeur dont la production auto-hébergée est payante.
- **Tranchée par la Présidence le 13/11/2026 au soir** (séance n°24, sa cinquième question) : oui, plus tard, une fois notre propre
  système de workflow en place.
  - « Donc se brancher à Camunda, effectivement, plus tard, pour essayer de récupérer un petit peu ce qu'ils font de bien aussi, et
    ce que nous, bah, on va pas refaire non plus. » ; « Donc se brancher à Camuda, ça tu le feras plus tard. »
  - Le but : « pourquoi pas s'intégrer après à Camunda pour vraiment faire la séparation entre les deux et vraiment montrer ce que
    nous, on apporte en plus à Camunda et ce qui représente effectivement une partie supérieure à Camunda qui ne le ferait pas, par
    exemple. »
- **Ce qui reste** : le moment et la forme. `[HYPOTHÈSE]` Après J2 : l'import d'un processus Camunda dans notre sous-ensemble de
  BPMN (R165), et TaskForce appelée par MCP depuis un processus Camunda, avec le point de décision ouvert de R99 (J5). La séance
  n°25 en fait un lot, après J2.

## Q19 : Montrer les applications de TaskForce dans d'autres hôtes, par MCP Apps ?

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°25](./conseil/seances/2026-11-13-le-workflow-pilotable.md), R172 et R178 (lot W8)

- **La question** : TaskForce expose déjà ses gestes par son serveur MCP (ADR-024). Faut-il offrir aussi ses applications
  embarquées (la carte d'un nœud, d'un accord, d'un brouillon, puis l'application Workflow) comme des applications MCP, pour que
  Claude, Claude Desktop, VS Code GitHub Copilot ou Microsoft 365 Copilot les rendent dans leurs conversations ?
- **Pourquoi ça compte** : `[ÉTABLI]` avec MCP Apps, un outil déclare une ressource `ui://`, que l'hôte rend dans un cadre isolé,
  dans la conversation ; l'application et l'hôte se parlent en JSON-RPC par `postMessage` ; elle peut appeler des outils et mettre
  à jour le contexte du modèle ; l'hôte contrôle ce qu'elle peut faire, et passe par le consentement de la personne
  ([MCP](https://modelcontextprotocol.io/extensions/apps/overview), lu le 13/11/2026). `[DÉDUIT]` Ce serait, pour l'expérience, ce
  que Q18 est pour Camunda : les règles et la preuve de TaskForce dans la conversation d'un autre outil. Le risque : un accord rendu
  par un hôte tiers ; les règles doivent le juger côté serveur, comme aujourd'hui, et la signification de la signature doit
  survivre au passage.
- **Position actuelle** : `[HYPOTHÈSE]` après J2, avec le lot W8 (J5), une fois la surface MCP de TaskForce complète (ADR-024).
- **Ce qu'il faut pour trancher** : une demande réelle d'un client qui travaille dans un de ces hôtes ; la version de MCP Apps que
  les hôtes prennent en charge ; un essai d'attaque sur les appels d'outils de l'application (R158).
- **13/11/2026 au soir** : R172 et R178 retenues par la Présidence, « Tout me convient »
  ([séance n°25](./conseil/seances/2026-11-13-le-workflow-pilotable.md)). J2 ne prend que W0 à W5, pour le seul processus d'E20 ;
  Q19 reste ouverte, après J2, avec le lot W8.

## Q20 : La signature électronique au sens de 21 CFR 11.200 : quand, et comment ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°25](./conseil/seances/2026-11-13-le-workflow-pilotable.md), R179

- **La question** : dans TaskForce, un accord se donne d'un clic, dans une session ouverte. Faut-il, pour un workflow marqué
  régulé, redemander l'identité de la personne au moment de signer, et quand le construire ?
- **Pourquoi ça compte** : `[ÉTABLI]` 21 CFR 11.200 demande, hors d'une session continue, chaque signature avec tous ses éléments,
  et, dans une session, la première avec tous ses éléments ; 11.50 veut le nom imprimé du signataire, la date, l'heure et la
  signification de la signature ; 11.70 la lie à son enregistrement
  ([Cornell LII](https://www.law.cornell.edu/cfr/text/21/11.200), lu le 13/11/2026). `[ÉTABLI]` Un accord de TaskForce porte qui
  peut décider, les signatures, s'il engage, son échéance, et entre au dossier, chaîné et scellé, pas encore signé (TF-J2-7).
  `[DÉDUIT]` Sans identité redemandée, un accord n'est pas une signature électronique au sens de Part 11, et le LIMS de la
  Présidence en aurait besoin. Un agent ne tape jamais d'identifiant : la nouvelle demande d'identité reste à la personne.
- **Position actuelle** : `[HYPOTHÈSE]` après J2, avec les workflows régulés (W6) et la séance n°26 sur le marché ; dans J2,
  seulement la signification de la signature sur chaque tâche humaine (R179). Le service de connexion déjà en place pourrait
  redemander l'identité avant une action : à vérifier.
- **Ce qu'il faut pour trancher** : l'expérience de la validation de la Présidence ; un premier projet régulé réel ; la façon de
  redemander l'identité, vérifiée sur l'app desktop.
- **13/11/2026 au soir** : R179 retenue, avec la précision de la Présidence
  ([séance n°25](./conseil/seances/2026-11-13-le-workflow-pilotable.md)) : « nous on a rien a faire techniquement pour GxP, c'est le
  client qui devra contraindre le model a ca, parce que notre app le permet ». TaskForce fournit l'infrastructure, dont les accords
  et leurs signatures ; le client contraint le modèle. `[DÉDUIT]` La signature qui redemande l'identité serait donc une option
  générique des accords, que le client choisit pour ses workflows, comme les quatre yeux d'un workflow régulé ; pas un mode
  « Part 11 ». Elle reste après J2. Le premier projet régulé réel peut être celui du client test, s'il travaille sous GxP (Q22).

## Q21 : Un fournisseur d'une personne passe-t-il l'évaluation fournisseur d'un client GxP ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), R181

- **La question** : une entreprise régulée qui valide un système évalue son fournisseur. TaskForce est fait par une personne et
  des agents, sans système qualité, sans support et sans certification. Peut-il passer cette évaluation pour un pilote, et à
  quelles conditions ?
- **Pourquoi ça compte** : la niche de R181 en dépend. `[ÉTABLI]` Pour une application Power Platform en GxP, Microsoft demande
  de qualifier la plateforme, dont une évaluation du fournisseur, avant de valider l'application
  ([Microsoft Learn](https://learn.microsoft.com/en-us/dynamics365/mixed-reality/guides/gxp-guidance/purpose-of-validation-and-traceability), 15/01/2026) ;
  GAMP 5, seconde édition, encourage à s'appuyer sur la documentation des fournisseurs et traite de l'open source
  ([ISPE](https://ispe.org/publications/guidance-documents/gamp-5-guide-2nd-edition), 07/2022) ; la FDA a accepté et reproduit des
  soumissions faites en R, open source ([R Consortium](https://r-consortium.org/posts/news-from-r-submissions-working-group-pilot-3/), 26/08/2024).
- **Position actuelle** : `[HYPOTHÈSE]` un dossier fournisseur public (le code sous AGPL, la façon de publier, les essais, les
  versions signées, la gestion des incidents, et ce qu'une personne seule peut garantir et ne peut pas) suffit pour un pilote
  sur un travail de documentation et de livraison de logiciel, pas pour un système BPF critique ; un partenaire qui porte la
  qualité (un cabinet de validation) peut combler le reste.
- **Ce qu'il faut pour trancher** : les cinq entretiens GxP de R186, avec la question « qu'est-ce qui vous ferait refuser un
  fournisseur ? » ; le sommaire du dossier fournisseur lu par une personne d'assurance qualité. Signal d'arrêt de R181 : trois
  personnes GxP sur cinq qui excluent un fournisseur d'une personne.
- **13/11/2026 au soir** : R181 retenue ; R186 reportée après le client test
  ([séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md)). Les cinq entretiens GxP qui devaient trancher Q21 attendent
  ce retour (Q22). `[DÉDUIT]` Si le client test travaille sous GxP, le dossier fournisseur de R181 passe avant lui.

## Q22 : Les questions du marché qui attendent le client test

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 13/11/2026 · issue du [Conseil, séance n°26](./conseil/seances/2026-11-13-le-marche-a-prendre.md), ses questions à la Présidence, et de sa décision du 13/11/2026 au soir

- **La question** : la Présidence retient R180 à R187, sauf les délais. Le client test passe d'abord, quand l'app est livrée et
  tient de gros volumes de données ; elle revient avec ses retours, et le Conseil en discute. Six des huit questions de la séance
  attendent ce retour :
  - la cible (R180) : les codes d'activité qui la comptent (J62 et J58.2 ; M69, M70.2, M71 et M72), et « sans développeur dédié
    pour configurer », éprouvé en entretien ;
  - le premier client possible (R184) : travaille-t-il sous GxP ? Oui ou non, sans nom ;
  - le réseau GxP (R182, R186) : combien de personnes joignables, dans quels rôles, combien hors du réseau de la Présidence ;
  - son expérience (R181, R187) : ce qu'on peut en dire en public, sans nom d'entreprise ;
  - le post LinkedIn (R182) : après la démo et la page, ou le jour des résultats du diplôme (OSS-J.5), et à quelle date ;
  - le prix (R185, Q15) : la disposition à payer demandée dès les entretiens, rien de payant avant J9.
- **Pourquoi ça compte** : les objectifs pas à pas (R183, à l'essai pour son ordre) et les trois preuves en dix jours (R186,
  reportée) partent de ces réponses ; E14 élargie et l'expérience de la niche aussi. La Présidence, le 13/11/2026 au soir : « ce
  sera mon cas client test stv, une fois fait je te donnerais les retour et on en discutera avec le conseil » ; « Effectivement le
  prix faudra voir. »
- **Position actuelle** : les six restent ouvertes, comme Q21, qui attend les entretiens GxP de R186. `[DÉDUIT]` Si le client test
  travaille sous GxP (la deuxième question), le dossier fournisseur de R181 passe avant lui.
- **Ce qui n'attend pas** : les deux autres questions de la séance ont leur propre échéance. R63, dont le délai de trente jours tombe
  le 28/11/2026 (Q13, le partenaire) ; un serveur en service avant le 31/12/2026 (Q13, l'hébergement), dont le client test dépend
  aussi `[DÉDUIT]`, puisque l'app desktop se connecte par lui.
- **Ce qu'il faut pour trancher** : l'app livrée et essayée sur de gros volumes de données (« me faut l'app avant evidemment qu'on
  testera avec des gros batch de donnees ») ; le cas du client test fait ; ses retours, discutés au Conseil.

## Q23 : Quelle décision de TaskForce mérite un modèle de décision, et sur quelles étiquettes l'apprendre sans données de client ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 15/11/2026 · issue du [Conseil, séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), R190 à R192

- **La question** : MANTA montre une recette désormais commune : une base ouverte, adaptée par LoRA, une tête qui note chaque
  option, des millions de décisions étiquetées. La Présidence est prête à entraîner sur sa machine et à publier des modèles faits
  pour TaskForce, sur un cas précis. Lequel, et avec quelles étiquettes, quand C1 tient (N ≈ 1, aucune donnée de client) ?
- **Pourquoi ça compte** : R191 (un adaptateur au labo) et toute publication d'un modèle en dépendent. Des données synthétiques
  simulent nos propres croyances ([`CLAUDE.md`](./CLAUDE.md), §3) ; des étiquettes tirées des accords et des refus apprennent ce que
  les personnes acceptent, pas ce qui est juste (Norman, Harris, séance n°27).
- **Position actuelle** : `[HYPOTHÈSE]` le tri d'une issue (la priorité, le type, les étiquettes, parmi ce que le projet offre) :
  des options fermées ; une faiblesse mesurée des petits modèles génératifs (Triage, 1 cas sur 3 pour qwen3:8b et 2 sur 3 pour
  qwen3.5:9b au banc, le 08/11/2026 ; le tri manqué d'E11, le 04/11/2026) ; des étiquettes que les personnes corrigent. Jamais
  « à qui la confier » (R192).
- **Ce qu'il faut pour trancher** : E26 (un modèle de décision existant contre le génératif, une règle écrite et le taux de base),
  puis E12 amendée si E26 désigne le cas ; la licence, le nom et le lieu de publication, demandés à la Présidence.
- **16/11/2026** : R190 retenue, pas exécutée maintenant ; R191 retenue, pour plus tard, avec les données des clients ; R192
  retenue, amendée avec Musk ([séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md)). La Présidence :
  « Donc on retiens, mais on execute pas ce truc la pour le moment. » Rien ne s'entraîne pour l'instant : E26 et E12 attendent,
  sans date. Le banc permanent est retenu : chaque requête est évaluée et nourrit le banc, par modèle et par tâche (la boucle de
  R61). Pas de liste de refus écrite d'avance, sauf la ligne de la loi : aucun modèle de TaskForce ne note des personnes ni
  n'attribue le travail sur leur comportement. Q23 reste ouverte : la décision à apprendre, ses étiquettes, la licence, le nom
  et le lieu de publication attendent E26 et E12.

## Q24 : Qui répond d'un adaptateur ou d'une leçon appris chez une entreprise, au sens du RGPD et de l'AI Act ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 15/11/2026 · issue du [Conseil, séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), R193 et R194

- **La question** : l'entreprise entraîne chez elle, sur ses données, avec la recette, le format d'export et la banque de TaskForce.
  Est-elle seule responsable du traitement, ou TaskForce en devient-il coresponsable parce qu'il en fixe des moyens essentiels ? Qui
  est fournisseur du système qu'elle met en service ? Et que devient l'effacement d'une personne dans des poids appris ?
- **Pourquoi ça compte** : R193 en dépend, comme la fiche d'un adaptateur et ce qu'un client peut signer. Le premier client test
  pourrait mettre dans TaskForce des décisions de ses salariés (question n°5 du PV à la Présidence).
- **Position actuelle** : `[HYPOTHÈSE]` l'entreprise est responsable de ce traitement et fournisseur du système qu'elle met en
  service ; TaskForce, qui ne voit ni ses données ni ses poids, fournit un outil. Un LoRA sur un petit modèle reste loin du tiers du
  calcul initial : l'entreprise ne devient pas fournisseur d'un modèle à usage général (lignes directrices de la Commission,
  18/07/2025). Les leçons, lisibles et effaçables, passent avant les poids ; l'effacement dans des poids passe par un réentraînement
  périodique ou un filtre démontré sur les sorties (CNIL, fiche 10, 07/02/2025).
- **Ce qu'il faut pour trancher** : la lecture d'un juriste ou d'un délégué à la protection des données sur le schéma de R193 ; l'avis
  28/2024 de l'EDPB et les fiches 10 et 13 de la CNIL ; les recommandations de la CNIL sur l'IA au travail, annoncées pour 2026,
  quand elles paraîtront.
- **16/11/2026** : R193 retenue, sans entraînement pour l'instant ; R194 retenue, amendée avec Musk
  ([séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md)). TaskForce reste agnostique sur les modèles :
  « on n'a rien a voir cote modele ». **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : sur « c'est eux
  ou moi qui aurait la data », en cloud, TaskForce héberge les données comme sous-traitant (RGPD, article 28) ; elles restent au
  client, et un entraînement sur elles ne se fait qu'avec son accord écrit, au contrat, et pour lui ; un banc commun à plusieurs
  entreprises ne garde que des scores agrégés, avec leur accord, et aucun contenu ne sort. `[DÉDUIT]` La position du 15/11
  (« TaskForce, qui ne voit ni ses données ni ses poids ») ne vaut que pour une installation chez le client ; en cloud, le rôle
  de sous-traitant s'y ajoute. Q24 reste ouverte : elle attend la lecture d'un juriste, et la réponse sur les décisions des
  salariés du client test (question n°5 du PV).

## Q25 : Comment isoler une mission sous Windows natif, sans prérequis ?

`[statut:: en-cours]` · `[prio:: P2]` · Ouverte le 15/11/2026 · issue du [Conseil, séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), R189

- **La question** : le worktree isole la branche, pas le poste. Sous Windows natif, la plateforme principale de l'app desktop, le bac
  à sable de Claude Code n'existe pas ; WSL2 demande les droits d'administrateur au premier lancement ; Hyper-V manque à Windows
  Famille ; Docker Desktop est payant au-delà de 250 salariés ou de 10 M$ de chiffre d'affaires. Quel chemin tient sur le poste
  d'une entreprise de 10 à 249 personnes : WSL2 et le bac à sable de Claude Code, Podman, le moteur dans WSL2, les conteneurs de WSL,
  ou une microVM de Docker Sandboxes ?
- **Pourquoi ça compte** : R189 propose un isolement par défaut pour un dépôt venu du dehors, et le bac à sable du test à blanc de
  W6 répond au même besoin (R195).
- **Position actuelle** : `[HYPOTHÈSE]` WSL2 d'abord, parce que Claude Code y tourne et que son bac à sable y existe ; un conteneur
  ensuite, Podman de préférence pour sa licence ; une microVM là où Windows Hypervisor Platform est permis. Aucun de ces chemins
  n'est un prérequis de l'app.
- **Ce qu'il faut pour trancher** : E27 sur la machine de la Présidence ; ce que la politique informatique du client test permet
  (WSL fermé ou non par Intune ou par stratégie de groupe), sans nom ni détail.
- **16/11/2026** : R189 retenue, amendée avec LeCun
  ([séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md)) : « Ca devrait etre active par defaut
  effectivement. » L'isolement est par défaut, partout, quel que soit l'agent. `[DÉDUIT]` La position du 15/11 (« Aucun de ces
  chemins n'est un prérequis de l'app ») ne tient plus telle quelle : il faut sur chaque système un moteur que l'app pose
  elle-même. **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence
  ([ADR-028](./decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md), en projet) : sous Windows, une distribution WSL2
  dédiée ; Docker ou Podman seulement s'ils sont déjà installés ; l'isolement dans le runner, pour que les outils d'un modèle
  local seul soient isolés comme Claude Code. Q25 passe en cours. Restent, pour E27 : les droits d'administrateur au premier
  lancement de WSL2, WSL fermé par une entreprise, et ce que fait une mission quand la machine n'offre aucun moteur.

## Q26 : Ce qu'une leçon du harnais peut proposer de changer, et ce qu'elle ne touche jamais

`[statut:: en-cours]` · `[prio:: P2]` · Ouverte le 15/11/2026 · issue du [Conseil, séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), R194

- **La question** : R194 fait d'une leçon tirée des runs une proposition, rejouée par la banque et acceptée par une personne. Quelles
  pièces du harnais une leçon peut-elle viser : une règle en mots, une convention du brouillon, un plan de Cortex, un cas de la
  banque, la préférence de modèle d'une tâche, la fiche d'environnement ? Et lesquelles jamais : le socle, une règle qui relâche,
  les étapes verrouillées, les sorties ?
- **Pourquoi ça compte** : Harness² modifie jusqu'à son fichier de garde-fous, et rien de ce que montre son article ne les protège
  (arXiv 2610.14224, 09/10/2026). Sans liste écrite, une leçon utile peut élargir un périmètre sans qu'on le voie.
- **Position actuelle** : `[HYPOTHÈSE]` une leçon ne fait que proposer, et ne peut que durcir une règle ; elle vise d'abord les
  conventions et les cas de la banque, qui ne changent aucune permission. Le socle refuse déjà qu'un agent change une règle
  (`RulesFloor.java:105-107`).
- **Ce qu'il faut pour trancher** : E29 ; la table écrite des pièces visées, relue par la Présidence ; un brouillon d'ADR si le lot
  W10 est retenu.
- **16/11/2026** : R194 retenue, amendée avec Musk
  ([séance n°27](./conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md)) : « je vois pas pk l'utilisateur devrait choisir
  en fait ». Une leçon qui durcit le harnais s'active seule quand la banque d'évaluations la valide ; elle est versionnée,
  notifiée et annulable d'un geste ; une leçon ne relâche jamais une règle et ne touche jamais au socle. La position du 15/11
  (« une leçon ne fait que proposer ») change donc pour les leçons qui durcissent. Q26 passe en cours. Restent : la table écrite
  des pièces qu'une leçon peut viser ; `[DÉDUIT]` ce que « durcir » veut dire pour une convention du brouillon, un cas de la
  banque ou une préférence de modèle, qui restent des propositions tant que ce n'est pas écrit ; les étapes verrouillées et les
  sorties, que R194 mettait hors de portée et que le secrétariat y laisse. E29, puis le lot W10.

## Q27 : La demande d'une preuve sur site existe-t-elle chez les entreprises de 10 à 250 personnes ?

`[statut:: ouverte]` · `[prio:: P1]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°28](./conseil/seances/2026-11-17-le-recentrage.md), R196

- **La question** : la place que la séance n°28 donne à TaskForce (un dossier par tâche, vérifiable hors de l'outil, installé
  chez l'entreprise) se déduit de ce que les plateformes ne vendent pas. Une absence d'offre peut être une absence de demande.
  Aucune enquête lue ne chiffre la demande d'une gouvernance d'agents sur site, aucune ne porte sur les entreprises européennes
  de 10 à 250 personnes, et aucun exemple public ne montre une personne seule vendant cela à des entreprises régulées.
- **Pourquoi ça compte** : R196 fonde la phrase du produit sur cette place ; R181 y prend sa niche. Si la demande n'existe que
  chez les grands comptes, servis en ligne par les plateformes, la couche n'a pas d'acheteur à sa taille.
- **Position actuelle** : `[HYPOTHÈSE]` la demande existe là où un audit contrôle déjà (BPF, Part 11, SOC 2, les
  questionnaires fournisseurs), et elle se dit dans les mots de l'audit, pas dans ceux des agents. Elle passe par un
  partenaire qui porte la qualité plus sûrement que par une vente directe (R63, Q21).
- **17/11/2026**, séance n°29 :
  - `[ÉTABLI]` D5 a lu Hacker News, des blogs, la presse professionnelle, des conférences rapportées et des offres d'emploi.
    Reddit et LinkedIn n'ont pas été lus. Le terrain public est muet sur ce segment : deux fils qui demandent ce qu'une
    entreprise paierait ne citent ni conformité, ni audit, ni agents ; sur les onze signaux de preuve, sept viennent de
    vendeurs ; aucun auditeur ni responsable qualité ne parle à la première personne.
  - `[ÉTABLI]` La Présidence écarte la méthode des entretiens (saisine de la n°29). R197 amendée propose cinq sources
    d'observation, le client test en tête ; les entretiens de R186 ne sont plus une condition.
- **17/11/2026**, séance n°30 :
  - `[ÉTABLI]` (D7) Aucune source lue ne montre un acheteur qui paie pour un dossier de preuve par tâche, ni une personne
    seule vendant à un compte régulé. Les listes d'un grand accélérateur ne demandent pas cette couche sous ce nom ; celle
    d'hiver 2027 demande l'IA derrière les murs, là où sont « the largest budgets ». Une enquête de fonds (28/10/2026) :
    47 % des responsables de la sécurité prendraient une jeune pousse pour un trou que leur plateforme ne couvre pas.
- **Ce qu'il faut pour trancher** : les retours du premier client test ; puis les entretiens de R186, qui attendent après
  lui. Trois acheteurs sur cinq qui décrivent une preuve qu'ils ne savent pas produire aujourd'hui, dans leurs mots.
  Complète Q21 et Q22.
- **17/11/2026**, séance n°29, **ce qu'il faut pour trancher**, complété : le client test observé (ouvre-t-il le
  dossier, à qui le montre-t-il) ; un acheteur autre que lui qui demande, installe ou paie ; si la Présidence l'accepte,
  une question de fait posée sans campagne (question 11 du PV) ; une lecture de Reddit et de LinkedIn par une personne
  connectée.
- **17/11/2026**, séance n°30, **ce qu'il faut pour trancher**, complété : les sept critères du point de décision
  (R218), observés chez le premier client test trente jours après la remise de la v1.
- **22/11/2026**, décision de la Présidence sur les séances n°28 à n°30 : « Alright ecoute prends les meilleurs decision
  avec le conseille pour cette v1 et c'est partie ». La Présidence délègue : les dix-huit points de la
  [séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md) sont tranchés selon l'avis de la majorité du Conseil.
  - **La décision** : R196, dont Q27 est issue, est remplacée par R205, la place ajustée, retenue par délégation de la
    Présidence au Conseil, selon l'avis de sa majorité (point 1). R197 amendée est retenue : le premier client test
    observé passe en tête, et les entretiens de R186 ne sont plus une condition. Les sept critères du point de décision
    (R218) sont retenus ; ils se lisent trente jours après la remise de la v1 au premier client test, au plus tard le
    31/03/2027 (point 17). La question de fait et la lecture de Reddit et de LinkedIn sont retenues (point 18) et
    inscrites comme des actions de la Présidence, sans date : Q38 et Q39.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : la décision retient une place et une
    façon de l'observer ; elle ne dit pas que la demande existe. R205 garde comme hypothèse que des équipes de 10 à 250
    personnes paient cela. Le butoir du 31/03/2027 revient sur la décision de la Présidence sur la séance n°26 (aucune
    date avant le client test) : il est retenu par la délégation, et la Présidence peut le retirer d'une ligne.
    `[DÉDUIT]` Q27 se lit au point de décision, sur les critères b, c et e de R218, et sur les réponses de Q38 et de Q39
    si elles viennent. Q27 reste ouverte.

## Q28 : Le CRA et la licence : libre non monétisé, ou édition payante ; l'AGPL seule, ou avec une licence commerciale ?

`[statut:: en-cours]` · `[prio:: P2]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°28](./conseil/seances/2026-11-17-le-recentrage.md), R203

- **La question** : deux choix se tiennent. Le Cyber Resilience Act s'applique en entier le 11/12/2027, et ses déclarations
  de vulnérabilités exploitées depuis le 11/09/2026 ; `[À VÉRIFIER]` selon un seul commentaire d'avocat sur les lignes
  directrices de la Commission (27/07/2026), un logiciel libre n'est « mis sur le marché » que s'il est monétisé, et une même
  entité peut être intendante d'une édition communautaire et fabricante d'une édition payante. Et l'AGPL sert l'audit du code
  mais gêne l'achat : la politique publique de Google l'interdit chez lui, et d'autres directions juridiques auraient une
  règle semblable `[À VÉRIFIER]`.
- **Pourquoi ça compte** : le modèle de revenus (Q15) passe presque partout par une édition payante (Plane, Mattermost,
  Sidekiq). Le jour où TaskForce en a une, il change de statut au sens du CRA, avec des obligations datées.
- **17/11/2026**, séance n°29 :
  - `[ÉTABLI]` (D4) Des outils de développement libres adoptés sans être payés ont fermé ou été repris : Earthly a cessé de
    maintenir son projet libre et cite la cannibalisation par son propre outil gratuit ; Kite a fermé avec 500 000
    développeurs actifs ; Continue a été repris en 06/2026. `[HYPOTHÈSE]` Le mur le plus probable est d'être adopté sans être
    payé. R206 propose qu'une licence commerciale et un prix soient écrits avant toute annonce large ; la Présidence a dit
    « le prix faudra voir » : la question lui revient (question 10 du PV).
- **17/11/2026**, séance n°30 :
  - `[ÉTABLI]` La Présidence tient un rachat pour une issue acceptable. `[ÉTABLI]` (D7) Un éditeur d'une seule personne vend
    depuis plus de dix ans des éditions commerciales d'une bibliothèque libre, installées chez le client. `[HYPOTHÈSE]` La
    licence commerciale répond au risque d'être installé sans être payé ; elle suppose tous les droits chez un seul
    titulaire (Q34).
- **Position actuelle** : `[HYPOTHÈSE]` tant que TaskForce est gratuit (R106), rien ne presse. Prévoir tôt une licence
  commerciale à côté de l'AGPL, pour les acheteurs dont la politique l'interdit ; ne rien écrire sur le CRA en public avant
  une lecture qualifiée.
- **Ce qu'il faut pour trancher** : la lecture du texte primaire des lignes directrices (communication C(2026) 5252) ; un
  juriste, avant toute édition payante ; Q15.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 13 de la liste à trancher ; R206 et R216
  retenues) :
  - **La décision** : la licence commerciale et le prix sont écrits avant toute annonce large ; tous les droits du code
    sont chez un seul titulaire ; le juriste passe avant l'édition payante. La Présidence, le 17/11/2026, sur le
    rachat : « si je peux me faire acheter par une boite qui veut mon truc j'ai aucun pb avec ca ».
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : l'ordre est tranché, le contenu ne l'est
    pas. Restent ouverts : quelle licence commerciale à côté de l'AGPL, quel prix (Q15), quel juriste, et la lecture du
    texte primaire sur le CRA. `[DÉDUIT]` La position du 17/11 (« rien ne presse ») ne tient plus telle quelle : la
    licence et le prix précèdent toute annonce large, et le critère 9 de « la v1 est finie » (R218) les demande écrits
    dans le dossier fournisseur. Les droits du code sont suivis en Q34. Q28 passe en cours.

## Q29 : Le format du dossier : s'aligner sur la RFC 8785 et le brouillon de l'IETF, ou garder le sien ?

`[statut:: tranchée]` · `[prio:: P2]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°28](./conseil/seances/2026-11-17-le-recentrage.md), R198

- **La question** : le dossier de TaskForce est une chaîne SHA-256 sur un JSON canonique écrit dans son code
  (`CanonicalJson.java`), exportée au format `taskforce-evidence/1`. Un brouillon individuel à l'IETF (« Agent Audit Trail »,
  version 09, 26/10/2026) décrit un journal d'agent chaîné par SHA-256 selon la RFC 8785, signatures en option ; il n'est
  « not endorsed by the IETF ». Faut-il s'aligner sur la RFC 8785, reprendre les champs du brouillon, ou publier son propre
  format comme une spécification ouverte ?
- **Pourquoi ça compte** : aucun standard adopté ne dit comment prouver ce qu'un agent a fait (Forrester, 20/03/2026). Un
  format publié peut servir de référence à de petites entreprises ; un format isolé oblige chaque auditeur à apprendre le
  nôtre. Les normes du JTC 21, attendues d'ici le 28/02/2027, peuvent démentir l'un comme l'autre.
- **Position actuelle** : `[HYPOTHÈSE]` s'aligner sur la RFC 8785 pour la canonisation coûte peu et ne lie à rien ; le
  brouillon de l'IETF se lit, sans s'y attacher tant qu'il n'a aucun statut ; le format et son vérificateur se publient
  (Mazzucato, LeCun, R64).
- **17/11/2026**, séance n°29 :
  - `[ÉTABLI]` (D4, relu par le secrétariat) La boîte à outils de Microsoft émet des reçus signés en Ed25519 sur JSON
    canonique (RFC 8785) ; JFrog annonce un enregistrement signé en in-toto et DSSE ; six brouillons individuels à l'IETF,
    aucun adopté ; une proposition de prédicat à l'OpenSSF close sans adoption le 29/09/2026.
  - `[HYPOTHÈSE]` Un format propre à TaskForce serait le septième. R198 amendée et R206 : la canonisation selon la RFC 8785,
    la signature dans une enveloppe que d'autres lisent déjà, le schéma de ce que le dossier ajoute publié avec son
    vérificateur. E34 l'éprouve.
- **Ce qu'il faut pour trancher** : comparer `CanonicalJson.java` à la RFC 8785 sur ses cas d'essai (il refuse les décimaux) ;
  lire le brouillon en entier ; un brouillon d'ADR avec TF-J2-7.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 9 de la liste à trancher ; R198 amendée, R206 et
  R212 retenues) :
  - **La décision** : aucun format propre. La canonisation suit la RFC 8785 ; la signature entre dans une enveloppe que
    d'autres lisent déjà (in-toto et DSSE), à instruire avec TF-J2-7 par E34, inscrite ce jour ; le schéma de ce que le
    dossier ajoute et son vérificateur se publient, ouverts (R206). La page de vérification s'écrit d'abord, et rien ne
    s'ajoute au commit.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : Q29 est tranchée sur son principe,
    TaskForce ne garde pas un format à lui. Le brouillon individuel de l'IETF ne devient pas la référence : un brouillon
    adopté par un groupe de travail est un des quatre signaux notés de R207 (s'y aligner, sans pivoter). Restent, pour
    E34 et non pour la Présidence : l'écart de `CanonicalJson.java` avec la RFC 8785 (il refuse les décimaux) ; les
    champs du dossier qui ne trouveraient pas leur place dans l'énoncé ; le signal d'arrêt de R198 amendée (si le format
    déborde, le dossier garde son format d'aujourd'hui, signé, et l'enveloppe attend). E34 est l'essai du critère 3 de
    « la v1 est finie » (R218). Le témoin reste en Q31.

## Q30 : Le sort des surfaces gelées, et quand le décider

`[statut:: en-cours]` · `[prio:: P2]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°28](./conseil/seances/2026-11-17-le-recentrage.md), R202

- **La question** : R202 gèle le Board et sa famille (List, Backlog, Cycles, Roadmap, Teams, Dashboard, Analytics, Members,
  le suivi du temps), la vue Workflow en cartes, les préréglages non connectés, l'app web hébergée. Un gel coûte : des
  migrations à porter, de la sécurité à tenir, des écrans à expliquer à un client qui évalue son fournisseur. Lesquelles
  supprimer, lesquelles reprendre, et sur quel signal ?
- **Pourquoi ça compte** : Musk a maintenu que geler est le pire des trois états ; Ait Si Abbou, que le gel retire au
  non-ingénieur la seule vue qu'il lit. Sans date, un gel devient un abandon qui ne dit pas son nom.
- **Position actuelle** : `[HYPOTHÈSE]` la décision se prend au retour du premier client test, surface par surface : ce qu'il
  a ouvert reste, ce qu'il n'a pas ouvert s'en va. L'issue et une liste simple du travail ne sont pas en cause.
- **Ce qu'il faut pour trancher** : E32 (ce qui dépend de l'issue interne) ; ce que le client test ouvre et n'ouvre pas, sans
  nom ni détail ; la décision de la Présidence sur la question 2 du PV.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), points 2, 10 et 12 de la liste à trancher ; R199 et R202
  amendées, R209 retenues) :
  - **La décision** : le Board et sa famille gèlent, l'issue reste l'ancre, et leur sort se décide au point de décision,
    sur l'usage observé, celui des non-ingénieurs compris. Une liste du travail d'un projet, par état, en langage clair,
    reste hors du gel. Dans la v1 se masquent Smart Assign, l'agent Copilot tant qu'il n'ouvre pas de dossier et « Show
    all links » ; les 97 préréglages jamais connectés portent la mention « pas encore essayé ». L'app web hébergée
    devient une démonstration en données d'exemple et l'espace de la Présidence. R202 était retenue dès le 17/11/2026 :
    « R202: ok je comprends oui on s'engage pas, on fourni juste le necessaire pour augmenter la confiance ».
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : le « quand » est tranché, le sort ne
    l'est pas. La position du 17/11 (« au retour du premier client test ») devient : au point de décision, trente jours
    après la remise de la v1 au premier client test, au plus tard le 31/03/2027. Rien ne se supprime d'ici là (R209 :
    tout le reste demeure gelé, sans suppression) ; le critère 10 de « la v1 est finie » demande que les surfaces
    arrêtées soient masquées et qu'aucune surface gelée n'ait reçu de travail depuis le 17/11/2026. L'app web hébergée
    sort de cette question : son seuil de réouverture est en Q37. E32 est inscrite ce jour. Q30 passe en cours.
    Restent : surface par surface, supprimer ou reprendre, sur ce que le client test ouvre et n'ouvre pas, sans nom ni
    détail.

## Q31 : Le témoin : où ancrer l'empreinte de tête du dossier, hors de l'opérateur ?

`[statut:: en-cours]` · `[prio:: P1]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°29](./conseil/seances/2026-11-17-preciser-avant-de-trancher.md), R198 amendée

- **La question** : le dossier d'une mission est une chaîne SHA-256 que TF-J2-7 doit signer. La chaîne, sa racine et la clé
  vivent chez le même opérateur, qui peut tout récrire et tout resigner. Un fil de discussion public le dit d'un outil
  voisin : une chaîne que l'opérateur détient ne prouve rien à un tiers (D5, C5). Où écrire l'empreinte de tête pour qu'un
  autre que l'opérateur la détienne aussi ?
- **Pourquoi ça compte** : sans témoin, « vérifiable sans TaskForce » veut dire « cohérent », pas « inchangé ». Hamilton
  s'est abstenue sur R198 amendée pour cette raison, Bengio la partage.
- **Position actuelle** : `[HYPOTHÈSE]` le moins cher d'abord : l'empreinte de tête écrite dans la pull request ou le commit
  chez l'hôte quand il y en a un, et dite dans le dossier. Un service d'horodatage ou un registre de transparence attendent
  qu'un acheteur les demande.
- **Ce qu'il faut pour trancher** : la décision sur la clé dans l'app de bureau (ADR-028, E27) ; lire comment les
  enveloppes in-toto et DSSE et le profil SCITT prévoient un témoin ; un brouillon d'ADR avec TF-J2-7. Complète Q29.
- **17/11/2026**, séance n°30 :
  - Le point 9 de la liste à trancher pose la question à la Présidence : l'empreinte de tête écrite dans la pull request
    quand il y en a une, avec TF-J2-7. R212 : rien d'autre ne s'ajoute au commit ni à la pull request qu'un lien et cette
    empreinte.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 9 de la liste à trancher ; R198 amendée et R212
  retenues) :
  - **La décision** : oui pour le témoin, le moins cher : l'empreinte de tête du dossier s'écrit dans la pull request
    quand il y en a une, avec TF-J2-7. Rien d'autre ne s'ajoute au commit ni à la pull request qu'un lien et cette
    empreinte. La Présidence, le 17/11/2026, écarte la session de l'agent dans le commit : « Enregistrer la session de
    l'agent dans le commit ? C'est du bruit je suis clairement d'accord. »
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : Q31 est tranchée pour ce seul témoin, et
    passe en cours. Restent ouverts : `[DÉDUIT]` une mission sans pull request, qui n'a pas de témoin hors de
    l'opérateur ; un service d'horodatage ou un registre de transparence, qui attendent qu'un acheteur les demande (R198
    amendée, précision 5) ; la clé de signature dans l'app de bureau (ADR-028, E27). E34, inscrite ce jour, ne tranche
    pas le témoin.

## Q32 : Qui écrit les processus et les paquets de règles, et que donne TaskForce comme exemples ?

`[statut:: en-cours]` · `[prio:: P2]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°29](./conseil/seances/2026-11-17-preciser-avant-de-trancher.md), R200 amendée

- **La question** : la Présidence étend le workflow à « compliance, reglementation, convention ». TaskForce fournit le
  moteur, jamais le contenu réglementaire (R179, R187, ADR-022). Une entreprise moyenne n'a personne pour écrire ses
  processus ; les grands comptes écrivent les leurs avec une équipe plateforme (D5, S15). Qui écrit : l'entreprise, un
  partenaire qui en répond, une communauté ? Sous quelle forme un processus et ses règles se partagent-ils ? Jusqu'où vont
  les exemples que TaskForce donne ?
- **Pourquoi ça compte** : un moteur vide ne montre rien ; un paquet réglementaire signé TaskForce contredit R187. D5 voit
  dans « le paquet de règles prêt » une des trois directions que le terrain porte.
- **Position actuelle** : `[HYPOTHÈSE]` TaskForce donne des exemples de conventions d'ingénierie, marqués comme des exemples
  (les quatre yeux sur un changement d'agent, aucun push direct, les tests avant la fusion). Une réglementation est écrite
  par l'entreprise ou par un partenaire qui en répond. TaskForce ne certifie aucun paquet.
- **Ce qu'il faut pour trancher** : la page du processus d'E20 avec une étape de chaque famille ; ce que le premier client
  test écrit lui-même et ce qu'il demande qu'on lui donne ; Q21 (le partenaire).
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), points 5 et 14 de la liste à trancher ; R200 amendée
  retenue, « R200: ok » dès le 17/11/2026) :
  - **La décision** : un processus porte une réglementation, une convention d'ingénierie ou une norme interne. TaskForce
    fournit le moteur, et des exemples de conventions marqués comme des exemples ; jamais le contenu réglementaire,
    jamais un paquet « prévalidé » ; il ne certifie aucun paquet. Le dessin du processus est délégué à l'équipe de Jobs.
    Le premier client test est partenaire de conception, avec un accord écrit qui dit ce que chacun donne et reçoit.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : la position du 17/11 devient la décision
    pour ce que TaskForce fournit. Q32 passe en cours. Restent ouverts, comme R200 amendée l'écrit : qui publie les
    paquets (l'entreprise, un partenaire, une communauté) ; sous quelle forme ils circulent d'une installation à l'autre
    (l'abstention de Nilekani sur R213) ; ce que le premier client test écrit lui-même (le critère d du point de
    décision, R218). La page du processus d'E20, avec une étape de chaque famille, tient au critère 5 de « la v1 est
    finie ».

## Q33 : La classe d'une écriture externe : qui la déclare, et comment prouver son action inverse ?

`[statut:: en-cours]` · `[prio:: P1]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°29](./conseil/seances/2026-11-17-preciser-avant-de-trancher.md), R201 amendée

- **La question** : la Présidence dit « si il peut le faire lui mm go ». Dans TaskForce, c'est le cas : cinq écritures
  internes partent sans accord, chacune avec son action inverse (`default.rules.json`). Hors de TaskForce, le socle classe
  toute écriture externe irréversible (`RulesFloor.java`, `mcp.write`), quel que soit l'outil. Peut-on déclarer réversible
  une écriture dans un outil externe, qui le déclare, et qu'est-ce qui prouve que l'inverse défait vraiment ?
- **Pourquoi ça compte** : la fatigue des accords est le signal le plus solide du terrain (D5, S26 à S32). Mais R1 interdit
  qu'un agent décide de ce qui est irréversible, et Bengio rappelle qu'une inverse qui supprime l'objet ne rappelle pas la
  notification partie.
- **Position actuelle** : `[HYPOTHÈSE]` outil par outil ; une personne qui administre l'espace déclare, nomme l'inverse,
  l'essai la prouve ; le défaut reste la carte ; la garde « jamais les trois à la fois » ne se relâche pas.
- **Ce qu'il faut pour trancher** : E33 ; le brouillon d'ADR-030 ; la décision de la Présidence sur la question 5 du PV.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 6 de la liste à trancher ; R201 amendée retenue) :
  - **La décision** : trois classes décidées d'avance par une personne (part seul, attend une carte, refusé). Dans
    TaskForce, rien ne change. Hors de TaskForce, outil par outil, après la v1.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : Q33 passe en cours. Le projet
    d'[ADR-030](./decisions/ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md) est rangé ce jour et E33 est inscrite. Ce
    que la décision fixe : une personne qui administre l'espace déclare, nomme l'inverse, et l'essai la prouve ; le
    défaut reste la carte ; jamais un agent ni un modèle au moment d'agir. Rien du socle ne change en v1 : l'état écrit
    chez un hôte ([ADR-031](./decisions/ADR-031-DRAFT-une-source-de-travail-sans-copie.md), en projet) en dépend et
    n'est pas dans la v1 (R218). Restent : la première partie d'E33, le geste qui annule les cinq écritures internes,
    que le secrétariat n'a pas trouvé dans le code (critère 6 de « la v1 est finie ») ; sa seconde partie, sur un outil
    réel, après la v1 ; la réserve de Bengio, ce qui est sorti de l'outil ne se rappelle pas.

## Q34 : À qui appartient le code, et comment le garder cessible ?

`[statut:: en-cours]` · `[prio:: P1]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), R216

- **La question** : TaskForce est sous AGPL-3.0. Une licence commerciale, et un jour une cession, ne sont possibles que si
  tous les droits du code sont chez un seul titulaire. Le sont-ils aujourd'hui ? Qu'advient-il d'une contribution
  extérieure, et des dépendances dont la licence limite la revente ?
- **Pourquoi ça compte** : la Présidence tient un rachat pour une issue acceptable, et R206 demande une licence commerciale
  avant toute annonce large. Dans les cas lus (D7), on rachète un outil dont on dépend ou une équipe ; un dépôt dont les
  droits sont partagés ne se vend ni ne se licencie.
- **Position actuelle** : `[HYPOTHÈSE]` aucune contribution extérieure n'est fusionnée sans un accord écrit qui laisse au
  titulaire le droit de licencier autrement ; l'inventaire des droits se fait une fois, maintenant.
- **Ce qu'il faut pour trancher** : l'inventaire des auteurs du dépôt et des licences des dépendances ; l'avis du juriste
  (Q28) ; la décision de la Présidence sur le point 13 de la liste.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 13 de la liste à trancher ; R216 retenue) :
  - **La décision** : tous les droits du code chez un seul titulaire ; la licence commerciale et le prix écrits avant
    toute annonce large ; le juriste avant l'édition payante. La Présidence, le 17/11/2026 : « si je peux me faire
    acheter par une boite qui veut mon truc j'ai aucun pb avec ca ». R216 ajoute que le rachat ne se vise pas.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : le principe est tranché, le fait ne l'est
    pas. Q34 passe en cours. Restent : l'inventaire des auteurs du dépôt et des licences des dépendances, au labo (la
    preuve en dix jours de R216) ; la forme de l'accord écrit demandé à une contribution extérieure, dont l'absence est
    un signal d'arrêt de R216 ; l'avis du juriste (Q28) ; l'engagement envers les clients si l'éditeur change de mains,
    que Vestager demande dans la licence commerciale et non dans une page.

## Q35 : Le vérificateur : un autre modèle suffit-il, ou faut-il un juge qui n'est pas un agent ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), R210

- **La question** : R210 place, entre les contrôles déterministes et la personne, un vérificateur qui n'est pas l'auteur.
  Un second modèle est-il assez indépendant pour laisser passer un changement ? Ou ne peut-il que renvoyer à une
  personne ?
- **Pourquoi ça compte** : `[ÉTABLI]` (D8) un modèle qui évalue favorise ses productions ; l'auto-correction ne marche
  qu'avec un retour externe fiable ; ces travaux ne portent pas sur le code, et aucune étude trouvée ne compare, sur du
  code, un agent qui se relit à un vérificateur indépendant. Sur le terrain, cinq revues d'IA sur six viennent du même
  produit que l'auteur. Bengio s'est abstenu sur R210 pour cette raison.
- **Position actuelle** : `[HYPOTHÈSE]` en v1, le vérificateur n'existe pas. Quand il existera, il ne fera jamais partir
  seul un changement que les contrôles déterministes n'ont pas déjà prouvé.
- **Ce qu'il faut pour trancher** : E36 ; un essai où des changements fautifs connus passent devant un modèle relecteur,
  devant le même modèle que l'auteur, et devant les seuls contrôles déterministes.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 7 de la liste à trancher ; R210 retenue) :
  - **La décision** : pour le geste de fin, la vérification automatique, puis la décision d'une personne, rendue courte
    et possible par lot ; la fusion sans personne est écrite, éteinte, pas construite en v1.
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : la décision ne tranche pas Q35, elle la
    place après la v1. Le vérificateur, l'étage 3 de R210, est écrit et pas construit : la position du 17/11 tient. R210
    retenue fixe deux bornes : un contrôle déterministe précède toujours le vérificateur, et si un contrôle ou le
    vérificateur échoue, le changement revient à une personne. E36 est inscrite ce jour. `[DÉDUIT]` Elle mesure après
    coup ce qui serait parti seul, pas ce que vaut un modèle relecteur : l'essai des changements fautifs connus reste à
    écrire. Q35 reste ouverte.

## Q36 : Que garde le dossier d'une machine, quand l'action n'attend pas un accord ?

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 17/11/2026 · issue du [Conseil, séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), R215

- **La question** : le dossier d'une mission lie une demande, une règle, un accord humain, une action et un résultat. Une
  machine décide en millisecondes, sans réseau. Qu'est-ce qui tient lieu d'accord : la règle en vigueur, la reprise en
  main, une autorisation donnée d'avance ? Et que peut-on dire honnêtement de la décision d'un réseau de neurones ?
- **Pourquoi ça compte** : `[ÉTABLI]` (D6) le règlement (UE) 2023/1230 exige dès le 20/01/2027, pour certaines machines,
  l'enregistrement des données du processus de décision lié à la sécurité ; les normes harmonisées n'existent pas. Une
  prépublication de 07/2026 montre qu'un raisonnement affiché ne reflète pas forcément la décision interne du modèle.
  C'est le rêve que la Présidence a posé.
- **Position actuelle** : `[HYPOTHÈSE]` le dossier dit quelle règle, quelle demande, quel accord ou quelle reprise en main ;
  jamais « pourquoi ». Rien ne se construit avant le point de décision.
- **Ce qu'il faut pour trancher** : la v1 finie ; puis une demi-journée au labo sur un enregistrement public ; un
  partenaire qui a un vrai robot, ou un texte qui nomme un format.
- **22/11/2026**, décision de la Présidence, par délégation de la Présidence au Conseil, selon l'avis de sa majorité
  ([séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 16 de la liste à trancher ; R215 retenue) :
  - **La décision** : la phrase du rêve est une direction ; rien ne se construit avant le point de décision ; le
    chantier ne s'ouvre que sur une des deux conditions (un partenaire qui a un vrai robot ou une flotte et accepte un
    essai ; un texte, acte délégué ou norme, qui nomme un format).
  - **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : la position du 17/11 devient la décision
    pour « rien ne se construit ». Le premier pas, une demi-journée au labo, ne vient que la v1 finie. Au 17/11/2026,
    aucune des deux conditions n'est remplie (R215). Q36 reste ouverte, et attend.

## Q37 : L'app web hébergée : quel seuil rouvrirait un hébergement pour des clients ?

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 22/11/2026 · issue du [Conseil, séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), R213, et de la décision de la Présidence du 22/11/2026 (point 12 de la liste à trancher)

- **La question** : l'app web hébergée change de rôle. Elle devient une démonstration en données d'exemple et l'espace
  de travail de la Présidence ; elle n'accueille plus les données d'aucun client. R213 ajoute que le seuil qui
  rouvrirait un hébergement pour des clients se fixe par la Présidence, d'avance. Ce seuil n'est pas fixé. Quel fait,
  compté comment, rouvrirait un hébergement ?
- **Pourquoi ça compte** : la Présidence a fait de l'installation chez le client la voie principale, le 17/11/2026 :
  « la version installe en on premise ecoute ca m'arrange moi c'est parfait, installer chez lui c'est good, je veux pas
  avoir a gerer ca en vrai de vrai, si plein de gens le veulenet que je controlle plus alors oui mais c'est sinon c'est
  entreprise grade donc on premise principalement ca me va ». Les données d'un client sur l'instance hébergée sont un
  signal d'arrêt de R213. Un seuil écrit d'avance évite que la réouverture se décide à la première demande. Complète Q13
  (l'hébergement).
- **La décision** (22/11/2026, par délégation de la Présidence au Conseil, selon l'avis de sa majorité) : la
  démonstration est retenue, plus aucun client n'est hébergé, et le seuil de réouverture revient à la Présidence.
- **Position actuelle** : aucune. **Précision du secrétariat** : le Conseil n'a proposé aucun seuil et le secrétariat
  n'en propose pas. Les mots de la Présidence donnent un sens (« si plein de gens le veulenet »), pas un chiffre.
- **Ce qu'il faut pour trancher** : une ligne de la Présidence, qui dit quel fait et combien, écrite avant la première
  demande d'hébergement ; `[HYPOTHÈSE]` les demandes d'hébergement, notées quand elles viennent, parmi les usages que
  R197 amendée observe ; ce que coûte un hébergement tenu par une personne seule (Q13).

## Q38 : Action de la Présidence : poser, sans campagne, la question de fait de la séance n°29

`[statut:: ouverte]` · `[prio:: P2]` · Ouverte le 22/11/2026 · issue du [Conseil, séance n°29](./conseil/seances/2026-11-17-preciser-avant-de-trancher.md), R197 amendée et question 11, et de la [séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 18 de la liste à trancher · action de la Présidence, sans date

- **La question** : c'est une action, pas un choix à instruire. La Présidence pose, quand l'occasion vient et sans
  campagne, à des personnes qu'elle connaît déjà, une seule question : « votre auditeur ou votre client vous a-t-il déjà
  demandé quelque chose sur vos agents de code, et qu'avez-vous montré ? ».
- **Pourquoi ça compte** : le segment visé n'écrit pas en public (Q27). La question porte sur un acte passé, pas sur une
  douleur (Duflo, son abstention sur R197 amendée). Prabhakar note qu'un signal de R207 qui porte sur des acheteurs ne
  peut pas se produire si personne ne les approche.
- **La décision** (22/11/2026, par délégation de la Présidence au Conseil, selon l'avis de sa majorité) : oui
  (point 18).
- **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : c'est un geste de la Présidence elle-même,
  inscrit sans date. Ce n'est une condition d'aucune recommandation (avis de la majorité, question 11 de la n°29). Duflo
  parlait de cinq personnes ; la décision n'en fixe pas le nombre. Les réponses se notent sans nom de personne ni
  d'entreprise.
- **Ce qu'il faut pour clore** : les réponses notées (demandé ou non, par un auditeur ou par un client, ce qui a été
  montré), rapportées au Conseil ; ou une ligne de la Présidence qui y renonce.

## Q39 : Action de la Présidence : lire une fois Reddit et LinkedIn, connectée, avec les mots de la recherche D5

`[statut:: ouverte]` · `[prio:: P3]` · Ouverte le 22/11/2026 · issue du [Conseil, séance n°29](./conseil/seances/2026-11-17-preciser-avant-de-trancher.md), question 13, et de la [séance n°30](./conseil/seances/2026-11-17-finir-la-v1.md), point 18 de la liste à trancher · action de la Présidence, sans date

- **La question** : c'est une action, pas un choix à instruire. D5 n'a lu ni Reddit ni LinkedIn : les deux étaient
  fermés à la recherche, et seule une personne connectée peut les lire. La Présidence les lit une fois, connectée, avec
  les mêmes mots que D5 (dossier de la séance n°29).
- **Pourquoi ça compte** : D5 trouve le terrain public muet sur les entreprises de 10 à 250 personnes, mais ces deux
  terrains n'ont pas été lus (Q27). Sur les onze signaux de preuve lus, sept viennent de vendeurs, et aucun auditeur ni
  responsable qualité ne parle à la première personne.
- **La décision** (22/11/2026, par délégation de la Présidence au Conseil, selon l'avis de sa majorité) : oui
  (point 18).
- **Précisions du secrétariat**, qui ne sont pas des mots de la Présidence : le PV n°30 écrivait « avant le
  17/12/2026 » ; l'action est inscrite ici sans date, comme un geste de la Présidence. La relecture mensuelle des
  signaux de R207 commence le 17/12/2026 : c'est le rythme du secrétariat, pas une échéance de la Présidence. `[DÉDUIT]`
  Une lecture faite avant cette date entre dans la première relecture ; une lecture faite après, dans la suivante. Un
  signal se note par son support, sa date et le rôle de son auteur, sans adresse ni nom ; les textes de vendeurs se
  comptent à part (R197 amendée).
- **Ce qu'il faut pour clore** : la lecture faite et sa note (les mots cherchés, la date, ce qui a été trouvé, absences
  comprises), versée à la grille des signaux ; ou une ligne de la Présidence qui y renonce.

---

**Points d'entrée :** [🔬 R&D](./README.md) · [🤖 Mode recherche](./CLAUDE.md) · [🧪 Expériences](./experiences/Experiences.md) · [📖 Notes critiques](./revues/World-Model.md)

**Dernière mise à jour :** 22/11/2026 · **v1.4** · Projet Taskforce, Metz Numeric School 2025-2026
