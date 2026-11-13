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
| [Q17](#q17--qui-est-le-concurrent-n1-de-taskforce-et-pour-quelle-cible-) | Qui est le concurrent n°1 de TaskForce, et pour quelle cible ? | P1 | en cours : la cible tenue « à peu près » (13/11) |
| [Q18](#q18--se-brancher-à-camunda-) | Se brancher à Camunda ? | P3 | tranchée (13/11) : oui, plus tard |
| [Q19](#q19--montrer-les-applications-de-taskforce-dans-dautres-hôtes-par-mcp-apps-) | Montrer les applications de TaskForce dans d'autres hôtes, par MCP Apps ? | P3 | ouverte |
| [Q20](#q20--la-signature-électronique-au-sens-de-21-cfr-11200--quand-et-comment-) | La signature électronique au sens de 21 CFR 11.200 : quand, et comment ? | P2 | ouverte |
| [Q21](#q21--un-fournisseur-dune-personne-passe-t-il-lévaluation-fournisseur-dun-client-gxp-) | Un fournisseur d'une personne passe-t-il l'évaluation fournisseur d'un client GxP ? | P1 | ouverte |

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

---

**Points d'entrée :** [🔬 R&D](./README.md) · [🤖 Mode recherche](./CLAUDE.md) · [🧪 Expériences](./experiences/Experiences.md) · [📖 Notes critiques](./revues/World-Model.md)

**Dernière mise à jour :** 10/11/2026 · **v1.3** · Projet Taskforce, Metz Numeric School 2025-2026
