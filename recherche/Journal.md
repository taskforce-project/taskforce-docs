---
id: recherche-journal
title: Cahier de labo — R&D Brain OS
doc_type: register
statut: active
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, journal, cahier-de-labo, brain-os]
related:
  - "./README.md"
  - "./CLAUDE.md"
---

# 📓 Cahier de labo — R&D Brain OS

> **Le cahier de bord daté du laboratoire.** Une **entrée par session** de recherche, **la plus récente
> en haut**. À ouvrir en début de session (« où on en était »), à remplir en fin ([`CLAUDE.md`](./CLAUDE.md) §10).
>
> **Format d'entrée** (gabarit dans [`Gabarits.md`](./Gabarits.md)) : `Fait` · `Trouvé` · `Décidé` ·
> `Prochain coup`. On **date**, on **ne réécrit pas** le passé (une erreur reste, on la corrige dans une
> entrée suivante — c'est un cahier, pas un wiki).

---

## 2026-10-27 (ter) : état des lieux de la v1, séance n°3 du Conseil, spécification de la v2

**Fait** : état des lieux d'un jour de la v1, tiré du code et du journal daté
([état des lieux](../v1/09-audits/Etat_des_lieux_v1_avant_v2.md), PC-059 à PC-062) ; ménage tranché par la Présidence ;
spécification de la v2, version 0.1 ([spécification](../v1/road_to_v2/Specification_V2_Harnais.md)) ; séance n°3 en
formation restreinte, Jobs et Musk, sur le ménage et la spécification ([PV](./conseil/seances/2026-10-27-menage-spec-v2.md)).

**Trouvé**
- `[ÉTABLI]` La délégation de code marche de bout en bout dans l'app desktop (19/10) ; ce qui fera le harnais manque :
  documents et versions, règles en données, preuve exportable.
- `[ÉTABLI]` Pour le premier cas d'usage, deux étapes sur six sont absentes à la base : importer un document, le chercher
  par version.
- `[DÉDUIT]` L'architecture de la v1 a déjà la bonne forme : un serveur qui garde, un runner qui exécute ; la v2 la
  généralise au lieu de la remplacer.

**Décidé** (Présidence) : le .exe d'abord, le Store et la webapp ensuite ; l'équipe gardée, comme contexte ; Mentions
gardé ; Assignments à retravailler ; GitHub et Slack à faire marcher ; Public et Private gardés ; Status retiré de la
vue ; Pages supprimées au profit du Brain OS ; Copilot gardé, à essayer ; code mort supprimé ; dans le doute, masquer
plutôt que supprimer. Priorité de la v2 : le harnais et l'architecture, scalables et robustes.

**Prochain coup** : la Présidence relit la spécification et tranche son §20 (dont R10 à R15) ; puis le sprint de trois
jours avec la banque de tests, en mode développement.

---

## 2026-10-27 (bis) : séance n°2 du Conseil, la vision de la Présidence

**Fait** : plénière des 21 membres sur la vision de Pierre (le harnais comme principe fondamental de tout outil avec
IA), tour de table, confrontation, second tour à sa demande, dernier mot du Conseil
([PV](./conseil/seances/2026-10-27-vision.md)). Question ouverte Q11 (harnais embarqué). La règle zéro garde « prouve ».

**Trouvé**
- `[DÉDUIT]` Le Conseil converge : miser sur l'entreprise, jamais sur les défauts des modèles ; vendre un résultat, le
  harnais invisible pour l'utilisateur et lisible pour l'auditeur ; un plan de contrôle neutre et local plutôt qu'une
  interface générique.
- `[ÉTABLI]` L'écart principal avec la vision : pendant une délégation, l'agent ne voit que le serveur MCP de
  TaskForce, pas encore les outils externes de l'entreprise (`taskforce-runner/src/agent.ts`).

**Décidé** (Présidence) : vision validée à dix ans ; R5' (la promesse), R6, R7' (tout tracé, seul l'irréversible
attend), R8, R9' retenues ; I1 (assurable) et I2 (embarqué) gardées ; niches A puis B ; premier cas d'usage : un
standard de communication de vingt-cinq ans qui évolue ; le bac à sable plutôt que la branche ; « libre mais
encadré » ; les outils de Microsoft se branchent sur TaskForce, pas l'inverse. Séance close.

**Prochain coup** : résumé pour la Présidence, état des lieux d'un jour de la v1, spécification de la v2 relue par la
Présidence, puis sprint de trois jours avec la banque de tests (passage en mode développement).

---

## 2026-10-27 : séance n°1 du Conseil, la première règle non négociable

**Fait** : première séance du Conseil d'Avenir, en formation restreinte (7 membres, contradicteur : Elon Musk), sur
la saisine « quelle est la première règle non négociable de TaskForce ? »
([PV](./conseil/seances/2026-10-26-premiere-regle.md)). Expériences E7 à E10 déclarées
([`Experiences.md`](./experiences/Experiences.md)), question Q10 ouverte. Kenza Ait Si Abbou entre au pôle Pont, à la
demande de Pierre (fiche sourcée) : le Conseil compte 21 membres, dont 11 femmes. Margaret Hamilton, morte le
30/09/2026, passe en siège historique. La fiche de Satya Nadella le rangeait par erreur dans Impulsion : corrigée (Pont).

**Trouvé**
- `[ÉTABLI]` Le dossier tient sur des sources primaires : le rapport d'Anthropic du 16/10/2026 (environ 80 % des
  sessions interactives à attendre un humain, chez ses employés), le billet d'OpenAI sur le harness engineering, le
  rapport de la NASA sur les règles de mission d'Apollo, la checklist de l'OMS.
- `[DÉDUIT]` Les sept membres convergent sur un point : la règle doit vivre hors de l'agent, écrite avant la mission.
  Ils divergent sur la vitesse (Musk, Bezos) et sur ce qu'on mesure (Harris).

**Décidé** (Présidence, 27/10/2026) : R1 « Aucun agent ne décide seul d'une action irréversible, ni de ce qui est
irréversible » retenue (une branche de travail rend réversible ce qui reste local) ; R2 retenue, à mieux expliquer ;
R3 retenue, avec le temps de cycle en plus ; R4 retenue (un relecteur dédié, avec une liste et une partie libre). Règle
zéro ratifiée : « On vise dix ans, on prouve en dix jours. »

**Prochain coup** : séance n°2 sur la vision de la Présidence, pas encore présentée au Conseil. E7 à E10 demandent un
passage en mode développement, après arbitrage de priorité.

---

## 2026-10-21 : création du Conseil d'Avenir

**Fait** : le Conseil d'Avenir est créé à la demande de Pierre, pour faire émerger les versions futures de TaskForce.
Charte et règlement [`conseil/README.md`](./conseil/README.md) (présidence, secrétariat, composition, formations,
déroulé d'une séance, règles du débat et d'honnêteté, mise à jour des fiches, traçabilité, règle zéro, registre) ;
20 fiches sourcées dans [`conseil/membres/`](./conseil/membres/) ; gabarits §7 (fiche membre) et §8 (procès-verbal)
dans [`Gabarits.md`](./Gabarits.md) ; protocole [`CLAUDE.md`](./CLAUDE.md) v1.2 (§7 : le Conseil siège à chaque
session) ; carte du labo v2.1. Poussé le 25/10, après le correctif de la version Store de l'app desktop.

**Trouvé**
- `[ÉTABLI]` La proposition de départ, venue de ChatGPT, réunissait surtout des dirigeants de la tech, sans
  scientifique. Pierre a demandé des femmes, des conseillères scientifiques et Yoshua Bengio. Composition retenue :
  20 membres, 10 femmes et 10 hommes, en quatre pôles (Impulsion, Pont, Harmonie, Science).
- `[ÉTABLI]` Chaque position `[ÉTABLI]` d'une fiche porte sa source ; 151 liens sur 158 répondent, les 7 autres sont
  des refus de robot ou des murs payants, aucun lien mort. Sept fiches gardent des points « à vérifier », dont la
  fonction actuelle d'Arati Prabhakar.
- `[DÉDUIT]` Le risque du dispositif est la fausse citation et l'aval implicite : d'où la règle « rien ne sort du labo
  sous le nom d'un membre » (charte §8).

**Décidé** : Pierre préside sans prendre part aux débats ; le Conseil siège à chaque session du labo ; l'agent tient
le secrétariat. En attente de ratification : la règle zéro « On vise dix ans, on prouve en dix jours ».

**Prochain coup** : première séance, avec le retour de ChatGPT que Pierre apporte. Saisine candidate : « quelle est
la première règle non négociable de TaskForce ? ». Aucun passage en mode dev.

---

## 2026-07-31 (quinquies) — A6 (Φ) + A7 (causalité) : clôture de la frontière

**Fait** — A6 et A7 traités **ensemble** → fiche commune [`theorie/A6-A7-frontiere.md`](./theorie/A6-A7-frontiere.md).
Entrées A6 et A7 de [`Axiomes.md`](./theorie/Axiomes.md) réduites. **Frontière A4–A8 entièrement poussée.**

**Trouvé**
- `[DÉDUIT]` A6 et A7 = **le même geste** : décorer le graphe d'une grandeur **absente des données**
  (potentiel / cause). Les deux **s'échouent sur C2**.
- `[DÉDUIT]` **A6 (Φ) hors modèle** : la valeur d'option vient de la **volatilité $\sigma$**, or ni prix ni
  $\sigma$ ici ; tout proxy = métrique de graphe qui ne mesure pas l'optionalité, ou **runway relabellisé**.
  Doublement bloqué (présuppose A4 + A5). **Sauvetage** : `irr(v)=\deg^-_{DEPENDS\_ON}(v)` (irréversibilité), calculable, ≠ Φ.
- `[DÉDUIT]` **A7 = l'ombre statique de A4** : `CAUSED_BY` est $P(G'|G,do(a))$ au grain de l'arête → même
  non-identifiabilité, **tombent ensemble**. `[ÉTABLI]` `count=0` (personne ne l'écrit). **Sauvetage** :
  couche **précédence barreau 1** = générateur d'hypothèses, `SUSPECTED_CAUSE` + confiance + provenance.
- `[DÉDUIT]` **Point de méthode** : A6/A7 **n'ont pas d'expérience** — leur verdict est « hors modèle »,
  fabriquer un test pour les faire paraître actifs serait malhonnête. **Un axiome a le droit à un « non ».**

**Décidé** — Frontière close. **Le rocher commun = C2** : A4, A6, A7, A5b s'y échouent, et tous ont le
**même repli** : structure observée + mémoire (**F2**), jamais futur/cause **inférés (F3)**.

**Méta (frontière complète A4–A8)** — Le système d'axiomes, poussé à fond, **redit ce que les revues
disaient** : le moat n'est pas la prédiction, c'est la **mémoire instrumentée**. Ce qui reste
constructible : **table d'épisodes/écarts**, **taux de base (E3)**, **front rétrospectif (E6, A8)**,
+ deux fragments structurels (`irr(v)`, précédence). Tout le reste est bloqué par C2.

**Prochain coup** — **Synthèse** : « ce à quoi le système d'axiomes s'est réduit » — candidate à
**promotion** (ADR, ou note dans `v1/road_to_v2/`). Point dev en attente inchangé (worklogs peuplés ?).

---

## 2026-07-31 (quater) — A8 (trajectoires / Pareto) poussée à fond · frontière solo

**Fait** — A8 → fiche dédiée [`theorie/A8-trajectoires.md`](./theorie/A8-trajectoires.md). Entrée A8 de
[`Axiomes.md`](./theorie/Axiomes.md) réduite. Nouvelle expérience **E6** (informativité du front de Pareto passé).

**Trouvé**
- `[DÉDUIT]` **Sur le passé, on compare des résultats réalisés, pas des futurs alternatifs** (générer des
  futurs = A4 bloqué ; contrefactuel = C2). → A8 groundé est **descriptif (F2)**, pas prescriptif. Ground
  la **math** de Pareto, pas l'**usage** (choisir un futur).
- `[ÉTABLI]` **Malédiction dimensionnelle** : à $m \gtrsim \log_2 n$ (ici $n{\approx}20$, seuil ~4,3) le
  **front ≈ tout** → le rêve **6 axes** est **inutile**. Inversion : seuls **2–3 objectifs sont
  mesurables**, ce qui garde $m$ petit et **sauve** A8 (mais tue l'ambition « riche arbitrage »).
- `[ÉTABLI]` Une **somme pondérée linéaire** ne touche que le **bord convexe** → prouvablement incomplète.
- `[HYPOTHÈSE]` **La forme utile n'est pas le front pur mais l'ε-contrainte** (« maximiser X s.c. runway
  > 6 mois ») : **contraintes, pas poids**, atteint le non convexe, et **produit une décision** (le front pur botte en touche).
- `[HYPOTHÈSE]` **Le noyau durable de A8 = refuser de scalariser l'incommensurable** — la partie la plus
  solide de tout le système, survit même quand le calcul est bloqué. Étoile polaire : **jamais de score global unique.**
- `[DÉDUIT]` Fragilité à $n{=}20$ + seed synthétique → **bootstrapper le front**.

**Décidé** — A8 reformulé : principe (durable) + calcul **rétrospectif** (2–3 axes, E6) + ε-contrainte
comme forme pratique. Le prescriptif reste bloqué (A4 + C2).

**Méta (3 axiomes de frontière poussés : A5, A4, A8)** — ils **convergent** : tout ce qui est groundable
est **F2/mémoire** (table d'épisodes, front rétrospectif) ; tout le **prescriptif** (simuler des futurs)
est bloqué par **A4 + C2**. Les deux seules briques buildables qui reviennent partout : **(a) la table
d'épisodes/écarts, (b) « quelque chose bat-il le taux de base ? » (E3).** A8 ajoute le **seul livrable
montrable sans rien débloquer** : le front rétrospectif (E6).

**Prochain coup** — frontière solo restante : **A6 (Φ)** et **A7 (causalité)** — les deux probablement
« hors modèle / bloqués », mais à documenter proprement pour fermer la frontière. Point dev inchangé (worklogs peuplés ?).

---

## 2026-07-31 (ter) — A4 (dynamique f) poussée à fond · frontière solo

**Fait** — A4 → fiche dédiée [`theorie/A4-dynamique.md`](./theorie/A4-dynamique.md). Entrée A4 de
[`Axiomes.md`](./theorie/Axiomes.md) réduite. Nouvelle expérience **E5** (stabilité du LLM-comme-$f$).

**Trouvé**
- `[ÉTABLI]` La forme **$M \cdot S_t$ est morte** : le graphe grandit (dimension variable), une matrice
  n'ajoute pas de nœud. $f$ = **graph rewriting**, pas algèbre linéaire.
- `[HYPOTHÈSE]` **Scinder $f = f_{\text{drift}}$** (= A3, gratuit, groundable) **+ $f_{\text{action}}$** (le problème).
- `[DÉDUIT]` **$f_{\text{action}}$ non identifiable** : l'action n'est pas aléatoire (confondue par le
  *motif* de la décision) + contrefactuel jamais observé (C2). **Plus profond que « pas assez de
  données »** — c'est **A7** (causalité) qui revient.
- `[HYPOTHÈSE]` **Le $f$ honnête n'est pas une formule** mais une **récupération non paramétrique**
  d'épisodes $(G,a,G')$. → **A4 dépend de la table des écarts de A5** : A5 ne *juge* pas $f$, **elle le
  nourrit**. Dépendance plus forte qu'on croyait.
- `[ÉTABLI]` **Un opérateur local existe déjà et est idempotent** (ingestion Phase 4bis, verrou V69).
  A4 = **généraliser**, pas inventer un monolithe.
- `[HYPOTHÈSE]` **Markov douteux** → $f(G_t,a)$ partiel (A2). **Horizon $\leq 2$–$3$** (erreur composée, pas de fonction de valeur).
- `[HYPOTHÈSE]` **Un LLM n'est pas une fonction** ($\operatorname{Var}_\omega$) → **E5**.

**Décidé** — A4 **reformulé** : drift + action, récupération non paramétrique, **bloqué derrière A5**. La
séquence réelle est **A5 (émettre l'incertitude + table d'épisodes) → A4 (récupération dessus)**.

**Prochain coup** — frontière solo suivante : **A8** (Pareto, grounding **gratuit** sur trajectoires
passées) ou **A7** (causalité, déjà à moitié traité en A4 §3) ou **A6** (Φ). Point dev inchangé (worklogs peuplés ?).

---

## 2026-07-31 (bis) — A5 (calibration) poussée à fond · frontière solo

**Fait** — Première frontière poussée en solo : **A5 → fiche dédiée** [`theorie/A5-calibration.md`](./theorie/A5-calibration.md)
(pattern « un axiome poussé = une fiche »). Entrée A5 de [`Axiomes.md`](./theorie/Axiomes.md) réduite à un
résumé. E1 raffiné en 3 régimes ([`experiences/Experiences.md`](./experiences/Experiences.md)). `issue_worklogs`
(V47) lu.

**Trouvé**
- `[ÉTABLI]` **Le système n'émet aujourd'hui aucune croyance calibrable** : story points = **point** (pas
  de distribution), « déjà-vu 41 % » = **cosinus déguisé en proba** (l'erreur même que A5 dénonce). Donc
  A5 est **bloqué en amont** : avant de calibrer, il faut que le **produit émette une incertitude**.
- `[DÉDUIT]` **« Calibré » est trivial** (prédire le taux de base y arrive) → viser **calibré ET tranchant**
  (décomposition de Murphy : fiabilité *et* résolution). Un test de calibration seul validerait un prédicteur nul.
- `[DÉDUIT]` **A5 se scinde** : **A5a** (scoreable, groundable) / **A5b** (contrefactuel, **infalsifiable
  par C2** → jamais de proba, un scénario). Groundable où c'est le moins précieux, impossible où ça compte le plus.
- `[DÉDUIT]` Au grain cycle, ~4 points/bin → **IC de Wilson ≈ [0,30 ; 0,95]** : calibration **indécidable** (C3).
- `[ÉTABLI]` Le « réel » d'un story point = **effort** = `SUM(issue_worklogs.minutes)` (V47) ; **si** peuplé,
  sinon proxy **latence** (biaisé). Le prédicteur calibré **existe déjà** : le **taux de base** (`GROUP BY`).

**Décidé** — A5 acté comme **scindé A5a/A5b** dans la spec. La vraie question de A5 n'est pas « calibrer le
LLM » mais « **quelque chose bat-il le taux de base ?** » (E3).

**Prochain coup**
- Frontière solo suivante : **A4** (dynamique `f`) — ou **A8** (Pareto sur trajectoires *passées*, faisable sans A4).
- Point dev en attente : vérifier si `issue_worklogs` est peuplé (décide si E1 mesure l'effort ou la latence).

---

## 2026-07-31 — Écosystème, grounding E2, système d'axiomes, structuration du labo

**Fait**
- Revue critique du **dump « écosystème en couches »** + 4 croquis → [`revues/Ecosysteme.md`](./revues/Ecosysteme.md).
- **E2 mis au cordeau** contre le **schéma réel** (V16/V23/V38 lus) : requête SQL exécutable, pièges
  documentés (pas de `completed_at` sur `cycles`, lien via `cycle_issues`, `story_points` nullable).
  → [`experiences/Experiences.md`](./experiences/Experiences.md#e2--la-dérivée-dot-x-apporte-t-elle-de-linformation-).
- **Système d'axiomes v0.1** créé → [`theorie/Axiomes.md`](./theorie/Axiomes.md) : noyau A1–A3 (grounded),
  frontière A4–A8 (chacun avec son test), carte de dépendances.
- **Brouillon ADR-012** (exposition du Brain OS, réponse à Q6) → [`decisions/`](./decisions/ADR-012-DRAFT-brain-os-exposition.md).
- Deux questions ajoutées : **Q8** (construire vers l'intérieur/extérieur), **Q9** (quel flywheel : F1/F2/F3).
- **Restructuration du dossier en laboratoire** : stations `theorie/ experiences/ revues/ references/
  decisions/`, paillasse racine (README/CLAUDE/Journal/Gabarits/Questions), ce cahier de bord.

**Trouvé**
- `[DÉDUIT]` **A5 (calibration) est le goulot** : sans savoir scorer une prédiction, ni A4 (dynamique),
  ni les probabilités, ni A8 (trajectoires) ne se groundent. Le grand système se réduit, aujourd'hui,
  à **une question à un jour** : sait-on scorer nos propres prédictions ? → **E1**.
- `[ÉTABLI]` Trois choses s'appellent « flywheel » et une seule est faible : **F1** (style, speccé),
  **F2** (mémoire organisationnelle = **le moat**, déjà à moitié bâti), **F3** (modèle du monde, étranglé
  par C1/C3). Le pitch « more usage → better models » vend **F3**, le plus faible. → vendre **F2**.
- `[ÉTABLI]` Le simulateur `MCTS/Monte-Carlo` du schéma est infaisable (C1 : rien à apprendre ; C2 :
  monde non rejouable). Ne survit qu'un **modèle System Dynamics à la main, assumé outil de pensée**.
- `[ÉTABLI]` Schéma : `cycles` n'a **pas** de `completed_at` (clôture non datée) ; seed = ~8 issues en
  cycle sur 267 → E2 sur ~4 cycles = **plomberie**, pas validation statistique (C3).

**Décidé** *(en attente de ratification humaine)*
- Reco **ADR-012 = option B** : la **connaissance** est un produit exposé (UI Brain OS déjà livrée), le
  **raisonnement** (croyances, trajectoires, écarts) reste **interne**. → à ratifier pour promotion en `v1/12-decisions/`.
- « Complet » abandonné au profit de « **reproductible** » pour le système d'axiomes (un axiome = un test SQL).

**Prochain coup**
- **E1** (grounder A5 : story points prédits vs réel, score de Brier) — **nécessite un passage en mode
  dev** + arbitrage priorité vs clôture V1.
- Option parallèle en R&D pur : **pousser la frontière A4–A8** dans le gabarit (solo, ou workflow ~7–8 agents).
- ⏳ **Ratifier ou non l'ADR-012.**

> **Intendance** — un auto-committer (probable `obsidian-git`) balaie les fichiers du labo en commits
> non déclenchés par l'agent. Sans danger, mais la section se construit en commits « fantômes ».

---

## 2026-07-17 — Amorçage du laboratoire

**Fait** — Création de la section R&D : protocole [`CLAUDE.md`](./CLAUDE.md) (contrat épistémique,
contraintes C1–C4, comité, cinq altitudes), formalisme [`theorie/Modele-mathematique.md`](./theorie/Modele-mathematique.md),
revue [`revues/World-Model.md`](./revues/World-Model.md), registres [`Questions-ouvertes.md`](./Questions-ouvertes.md)
et [`experiences/Experiences.md`](./experiences/Experiences.md), bibliothèque [`references/Bibliotheque.md`](./references/Bibliotheque.md).

**Trouvé** — Le trou central de `World Model.md` : **personne ne calcule `f`**. Sous C1–C4, `f` est soit
écrite à la main (simulation de nos croyances), soit produite par un LLM (texte chiffré) — jamais apprise.
La meilleure idée récupérable : **`ẋ`, la dérivée** (calculable en SQL).

**Décidé** — La direction retenue reste celle du 07/07 (mémoire/retrieval, sans gradient) ; `World Model.md`
est une note de recherche **sans autorité** tant qu'aucun ADR ne tranche.

**Prochain coup** — Préciser E2, esquisser l'ADR de Q6. *(fait le 31/07)*

---

**Points d'entrée :** [🔬 Labo](./README.md) · [📋 Protocole](./CLAUDE.md) · [🧰 Gabarits](./Gabarits.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
