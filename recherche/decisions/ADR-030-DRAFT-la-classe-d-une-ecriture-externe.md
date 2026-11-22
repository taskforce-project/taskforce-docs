---
id: adr-030-la-classe-d-une-ecriture-externe
title: "ADR-030 (brouillon) : la classe d'une écriture externe, déclarée outil par outil par une personne"
doc_type: adr
statut: proposed
version: 0.1
date: "22/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, regles, socle, accords, integrations, mcp, cortex, conseil]
related:
  - "../conseil/seances/2026-11-17-preciser-avant-de-trancher.md"
  - "../conseil/seances/2026-11-17-le-recentrage.md"
  - "../conseil/seances/2026-11-17-finir-la-v1.md"
  - "./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md"
  - "./ADR-031-DRAFT-une-source-de-travail-sans-copie.md"
  - "./ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "./ADR-025-DRAFT-un-seul-moteur-de-regles.md"
  - "./ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../experiences/Experiences.md"
  - "../Questions-ouvertes.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-030 (brouillon) : la classe d'une écriture externe, déclarée outil par outil par une personne

> **Brouillon, `DRAFT`, sans autorité avant sa promotion** ([Gabarits](../Gabarits.md) §6). Il naît de « R201, amendée »
> (séance n°29). Cette recommandation est **retenue le 22/11/2026 par délégation de la Présidence au Conseil, selon l'avis de
> sa majorité** : « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est partie ». C'est la
> recommandation qui est retenue : trois classes, et hors de TaskForce, outil par outil, après la v1. La façon de le faire,
> ci-dessous, reste une proposition du secrétariat, à relire par la Présidence, qu'E33 doit éprouver. Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 030 après sa
> ratification.

## Statut

Proposé le 17/11/2026 ; état de la décision inscrit le 22/11/2026. `DRAFT`, pas promu. Rien de ce projet ne se construit en
v1 : dans TaskForce, les trois classes sont déjà ce que font les règles par défaut ; hors de TaskForce, le changement du socle
vient après la v1, outil par outil, et pas avant E33.

## Contexte

- `[ÉTABLI]` La Présidence, sur R201 (saisine de la séance n°29, 17/11/2026) : « Bah la fatigue des demandes d'accord oui
  donc si il peut le faire lui mm go ».
- `[ÉTABLI]` R1 (séance n°1) : aucun agent ne décide seul d'une action irréversible, ni de ce qui est irréversible. R7'
  (séance n°2) : tout est tracé, seul l'irréversible attend.
- `[ÉTABLI]` Dans le code de `dev` (`067c577b`, lu le 17/11/2026), les trente règles par défaut
  (`resources/harness/default.rules.json`) laissent partir sans accord les lectures, les écritures dans la copie de l'agent
  et cinq écritures internes, chacune avec une action inverse nommée (créer ou modifier une issue, commenter, créer un
  projet, créer une note).
- `[ÉTABLI]` Le socle (`core/harness/rules/RulesFloor.java`) classe `mcp.write`, toute écriture dans un outil externe, parmi
  les actions à sens unique, quel que soit l'outil ou le geste. Il se juge après toutes les couches de l'entreprise et ne
  fait que durcir : aucune règle de l'entreprise ne peut faire partir seule une écriture externe. Une sortie déclarée
  réversible sans action inverse n'est pas tenue pour réversible.
- `[ÉTABLI]` Cortex classe un outil externe en lecture ou en écriture d'après ce que l'outil déclare
  (`core/service/agent/CortexGate.java`) : deux classes seulement.
- `[ÉTABLI]` (D5, séance n°29) La fatigue des accords est le signal le plus solide du terrain : l'éditeur d'un agent de code
  mesure 93 % de demandes acceptées ; son mode automatique, un classifieur, laisse passer 17 % des actions trop zélées ;
  des praticiens concluent qu'il faut laisser passer le courant, refuser en dur l'interdit et garder l'accord pour quelques
  actions lourdes.
- `[ÉTABLI]` L'ANSSI (10/2026) demande de classer chaque action : autonome, approbation obligatoire, interdite (dossier de la
  séance n°28).
- `[HYPOTHÈSE]` Bengio, à la séance : une action inverse, dans un outil externe, supprime l'objet et ne rappelle pas ce qui
  est parti (une notification, un courriel, un automatisme).
- `[ÉTABLI]` La [séance n°30](../conseil/seances/2026-11-17-finir-la-v1.md) (R209) fait dépendre de ce projet l'état que
  TaskForce écrit chez l'hôte d'où vient une demande : c'est une écriture externe, que le socle fait attendre aujourd'hui.
  R210 étend les trois classes au geste de fin, sans rien changer au socle.

## Décision

Le point 1 et le défaut du point 2 sont ce que « R201, amendée » dit et que la délégation du 22/11/2026 retient. Les points 3
à 9 sont la proposition du secrétariat pour l'extérieur, après la v1.

1. **Trois classes, décidées d'avance par une personne** : part seul, attend une carte, refusé. Jamais l'agent, jamais un
   modèle au moment d'agir, ne choisit la classe.
2. **Le défaut ne change pas.** Une écriture dans un outil externe attend une carte. Une action de classe inconnue aussi.
3. **Une écriture externe peut être déclarée réversible, outil par outil et geste par geste**, par une personne qui
   administre l'espace. La déclaration nomme le connecteur, le geste de l'outil, et l'action inverse de ce geste.
4. **La déclaration ne vaut que si l'inverse a été essayée** sur cet outil, et l'essai est gardé avec la règle.
5. **Le socle distingue alors deux écritures externes** : celle qui est déclarée, avec son inverse, devient une sortie
   réversible ; toute autre reste à sens unique. C'est le seul changement du socle.
6. **Les autres gardes du socle ne se relâchent pas** : aucun secret ne sort ; aucun agent ne change les règles, donc aucun
   agent ne fait cette déclaration ; jamais les trois à la fois (un contenu non fiable, des données sensibles, une sortie)
   sans une personne.
7. **Ce qui part seul est tracé, dit et annulable** : au dossier (R7'), dans la réponse de Cortex (où, et quoi), et par un
   geste qui exécute l'inverse.
8. **La carte se mesure** : par règle, la part des cartes acceptées. Une règle presque toujours acceptée est signalée à une
   personne ; le système ne reclasse jamais seul.
9. **Changer une classe est un changement de règle** : versionné, avec son auteur et sa raison, comme toute règle.

### Ce que les projets ADR-029 et ADR-031 en attendent

- L'état et le lien que TaskForce écrit chez l'hôte d'où vient une demande
  ([ADR-031](./ADR-031-DRAFT-une-source-de-travail-sans-copie.md), point 5) sont une écriture externe comme une autre. Tant que
  ce projet n'est pas construit, ou tant qu'une personne n'a pas déclaré ce geste pour cet outil, chaque état écrit chez un
  hôte attend une carte.
- La carte d'accord, elle, ne s'affiche jamais chez un hôte
  ([ADR-029](./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md), amendement de la n°29) : ce projet ne change que ce
  qui part seul, pas le lieu où une personne décide.
- Les événements de mission émis par les webhooks sortants de TaskForce ne sont pas des écritures dans un outil externe au
  sens du socle : ce projet ne les touche pas. `[DÉDUIT]` de R209, à vérifier quand ils s'écriront.

## État de la décision au 22/11/2026

**La décision.** Après la séance n°30, la Présidence, à qui le secrétariat avait remonté les dix-huit points à trancher avec
l'avis de la majorité, répond : « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est
partie ». La Présidence délègue : les points sont tranchés selon l'avis de la majorité du Conseil, tel que le
[PV n°30](../conseil/seances/2026-11-17-finir-la-v1.md) l'écrit (« La liste à trancher pour finir la v1 »). Pour ce projet :

- « R201, amendée » (n°29) est retenue par délégation de la Présidence au Conseil, selon l'avis de sa majorité ;
- point 6, les accords pendant la mission : trois classes ; hors de TaskForce, outil par outil, après la v1 (ADR-030, E33) ;
- point 7, le geste de fin (R210) : les trois classes s'y étendent ; la fusion sans personne est écrite, éteinte, pas
  construite en v1.

**Précisions du secrétariat.**

- Ce qui existe en v1, sans rien construire de ce projet : les lectures, les écritures dans la copie de l'agent et les cinq
  écritures internes réversibles partent seules ; toute écriture externe attend une carte. R204, qui fait dire à Cortex où il
  écrit et ce qu'il a fait, est faite (PR #548, fusionnée dans `dev` le 19/11/2026, pas encore en production).
- Ce qui vient après la v1 : le geste d'annulation pour les écritures internes ; la déclaration d'un geste externe, sur un
  premier outil, avec son essai ; la mesure des cartes acceptées.
- Le projet lui-même n'est pas ratifié : les Suites du PV n°29 le donnent « à relire par la Présidence ». Rien ne va dans
  `v1/12-decisions/` avant cette relecture.
- Désaccord conservé au PV : Bengio (une écriture externe n'est jamais tout à fait réversible : ce qui est notifié est parti).

## Alternatives considérées

- **Garder une carte par écriture**, comme R201 de la séance n°28. Écartée par la séance : c'est la fatigue que le terrain
  décrit, et la Présidence la refuse.
- **Un classifieur qui juge chaque action**, comme le mode automatique de l'agent de code le plus utilisé. Écartée : c'est
  un modèle qui décide au moment d'agir, contre R1 ; 17 % d'actions trop zélées passent, selon son éditeur.
- **Laisser l'entreprise relâcher le socle par une règle ordinaire.** Écartée : le socle ne fait que durcir (R157), et c'est
  ce qui permet de dire ce que TaskForce garantit dans son code.
- **Déclarer réversible un connecteur entier.** Écartée : dans un même outil, créer un commentaire et supprimer un espace ne
  pèsent pas pareil.
- **L'extérieur dès la v1** (point 6, option C). Écartée par la majorité : pas avant E33.
- **Que TaskForce déclare lui-même les gestes réversibles des outils qu'il a essayés.** À instruire : cela ferait de
  TaskForce l'auteur d'un contenu que l'entreprise devrait décider
  ([ADR-022](./ADR-022-DRAFT-infrastructure-pas-les-regles.md)) ; un exemple à reprendre, marqué comme tel, resterait
  possible. La question revient à la Présidence, ci-dessous.

## Conséquences

- Les cartes deviennent rares pour ce qu'une personne a déclaré courant ; elles gardent leur poids pour le reste.
- Le socle gagne une distinction, donc une surface d'erreur : une déclaration fausse fait partir seule une action qui ne se
  défait pas. C'est pourquoi l'essai de l'inverse est une condition, et non une option.
- Il faut un geste d'annulation dans l'app, qui exécute l'inverse : le secrétariat ne l'a pas trouvé dans la copie du code
  pour les cinq écritures internes. `[À VÉRIFIER]` avec E33.
- Il faut un troisième état pour un outil externe, au-delà de « lecture » et « écriture ».
- `[DÉDUIT]` Le changement vit dans le moteur de règles unique ([ADR-025](./ADR-025-DRAFT-un-seul-moteur-de-regles.md)) : il vaut pour
  Cortex comme pour le runner, sans seconde écriture.
- Tant qu'il n'est pas fait, l'état écrit chez un hôte (ADR-031) coûte une carte à chaque changement d'état.
- La table de correspondance (R197) gagne une ligne vérifiable face au principe de l'ANSSI sur les classes d'actions.
- Désaccord conservé : Bengio (une écriture externe n'est jamais tout à fait réversible : ce qui est notifié est parti).

## La preuve

E33 ([Expériences](../experiences/Experiences.md)) : d'abord les cinq écritures internes, sans code du produit (existe-t-il
un geste qui les défait, et reste-t-il quelque chose ?) ; puis, après la v1, une écriture dans un outil réel. Si l'inverse
laisse sortir ou subsister quoi que ce soit, ce projet se réécrit ou s'abandonne, et la carte reste la règle dehors.

Signal d'arrêt de la séance n°29 : une action partie seule dont l'inverse échoue ou laisse une trace dehors ; une classe
changée sans qu'une personne l'ait décidé. La classe revient alors à la carte.

## Plan de déploiement

- **Maintenant, au labo, sans code du produit** : la première partie d'E33.
- **En v1** : rien de ce projet. Cortex dit où il écrit et ce qu'il a fait, par les correctifs de R204, déjà fusionnés dans
  `dev`.
- **Après la v1** : le geste d'annulation pour les écritures internes ; puis la déclaration d'un geste externe, sur un
  premier outil, avec son essai. Le premier geste utile est l'état écrit chez l'hôte de la première source externe (GitHub,
  selon ADR-029 et ADR-031).
- **Ensuite** : la mesure des cartes acceptées, par règle.

## Questions à la Présidence

Le secrétariat ne répond pas à sa place.

1. **La relecture.** Ce projet dit-il ce que la Présidence veut de « si il peut le faire lui mm go » ? Une ligne suffit pour le
   corriger ou le retirer.
2. **Qui déclare** (Q33). Le projet dit : une personne qui administre l'espace. Est-ce la bonne personne, ou faut-il un rôle à
   part ?
3. **TaskForce donne-t-il des déclarations en exemple**, pour les outils qu'il a essayés, marquées comme telles, ou
   l'entreprise part-elle toujours d'une page blanche (ADR-022) ?
4. **Ce qui notifie** (désaccord de Bengio). Un geste qui prévient des personnes ou déclenche un automatisme chez l'hôte
   peut-il être déclaré réversible, ou reste-t-il toujours à la carte ? E33 dira ce qui sort ; la règle revient à la
   Présidence.

## Liens

- [PV de la séance n°29](../conseil/seances/2026-11-17-preciser-avant-de-trancher.md), « R201, amendée », et la décision de la
  Présidence
- [PV de la séance n°28](../conseil/seances/2026-11-17-le-recentrage.md), R201
- [PV de la séance n°30](../conseil/seances/2026-11-17-finir-la-v1.md), R209, R210 et la liste à trancher (points 6 et 7)
- [ADR-029](./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md), la couche : qui possède quel moment
- [ADR-031](./ADR-031-DRAFT-une-source-de-travail-sans-copie.md), une source de travail sans copie : l'état écrit chez un hôte
  dépend de ce projet
- [ADR-025](./ADR-025-DRAFT-un-seul-moteur-de-regles.md), un seul moteur de règles
- [ADR-022](./ADR-022-DRAFT-infrastructure-pas-les-regles.md), l'infrastructure, pas les règles
- [ADR-028](./ADR-028-DRAFT-execution-isolee-par-defaut.md), l'exécution isolée par défaut : aucun isolement ne sert à
  relâcher une règle
- [Expériences](../experiences/Experiences.md), E33
- [Questions ouvertes](../Questions-ouvertes.md), Q33

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 22/11/2026 · **v0.1** · Projet Taskforce
