---
id: conseil-seance-2026-10-29-reserves-premier-lot
title: "Séance n°12 du 29/10/2026 : les réserves du premier lot de la boucle"
doc_type: pv-seance
statut: active
date: "29/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, evaluations, boucle, design]
related:
  - "../README.md"
  - "./2026-10-29-boucle-premier-lot.md"
  - "./2026-10-29-intelligence-possedee.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°12 du 29/10/2026 : les réserves du premier lot de la boucle

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

Les quatre réserves que la Présidence a faites siennes à la séance n°11 ont chacune une solution.

- **Un cas vieillit à vue.** Il garde les empreintes de ce qu'il a figé ; quand l'espace a changé, il passe « à revoir »
  et sort du score, et son adaptation, un nouveau cas, naît d'un clic. Un cas noté ne change jamais.
- **La banque est celle de l'entreprise, pas de Cortex.** Le cas se tire de tout dossier ; l'écran vit là où l'on change
  de modèle et là où une tâche échoue, dessiné par l'équipe de Jobs ; les réglages gardent l'interrupteur.
- **Confirmer d'un geste.** Les critères proposés s'acceptent d'un clic, et TaskForce propose lui-même les cas que les
  dossiers signalent (un refus, une action accordée qui échoue), à confirmer par lots.
- **La banque marche sans écran.** Chaque geste passe par l'API et par le serveur MCP de l'espace ; l'écran suit.

Quatre recommandations, R72 à R75, retenues par la Présidence le 30/10/2026, avec l'ordre de Jobs, qu'elle suit : pas de
surface nouvelle avant les écrans de base.

Désaccord conservé : pour Steve Jobs, contradicteur, une file de cas à confirmer et des outils MCP sont deux surfaces de
plus, alors que les écrans de base du produit ne sont pas livrés. Se concentrer, c'est d'abord dire non.

- **Saisine** (Présidence, 29/10/2026), en retenant R66 à R71 :
  - R66 : « on pourrait combiner les 2, faudrait pas qu un cas reste fige en gros, ou que quand l espace change une
    adaptation naisse » ;
  - R67 : « c'est pas Cortex notre produit, attention, ce sera surement un changement niveau UI/UX Jobs a faire » ;
  - R68 : « nous faut une solution pour ca » ;
  - R71 : « faut trouver une solution ».
  - Puis : « On y va ».
  - Question posée par le secrétariat : pour chacune des quatre réserves, quelle solution, prouvable en dix jours ?
- **Formation** : restreinte (7), un membre au moins par pôle :
  - Gwynne Shotwell et Steve Jobs (Impulsion), Satya Nadella (Pont), Margrethe Vestager (Harmonie) ;
  - Margaret Hamilton et Esther Duflo (Science) ;
  - Julie Zhuo (Design).
  - Shotwell et Duflo siègent parce que les réserves sont les leurs ; Jobs, parce que la Présidence le nomme pour l'UI/UX.
  - Ordre de parole tiré au sort le 29/10/2026 à 22:39 UTC (`shuf`) : Hamilton, Vestager, Duflo, Nadella, Shotwell, Jobs,
    Zhuo.
  - Contradicteur désigné : Steve Jobs. Duflo l'était à la n°11.
- **Fiches** : toutes à jour (moins de 30 jours). Hamilton et Jobs, sièges historiques, ne se rafraîchissent que sur une
  nouvelle source historique.

## Dossier

1. `[ÉTABLI]` **Le premier lot est construit** (`taskforce-fullstack` #437, vérifié en développement le 29/10/2026).
   - Un cas garde la question, sa date, les notes servies (titre, domaine, contenu), la cassette des lectures réussies et
     des critères datés (`criteria_at`), et son dossier source (`source_record`, mis à nul s'il disparaît).
   - Il ne garde ni l'identifiant des notes servies, ni la version des règles de l'espace.
   - Rien ne dit qu'un cas a vieilli : il sort de la banque quand quelqu'un l'archive.
2. `[ÉTABLI]` **Ce que l'espace sait de ses changements.**
   - Une note a sa date de mise à jour (`AuditableEntity.updatedAt`) ; un projet a son statut et sa date de mise à jour.
   - Les règles de l'espace ont un numéro de version (`RulesBundle.version`).
   - Le dossier d'une réponse garde l'identifiant des notes servies (`mission.started`, depuis #437).
3. `[ÉTABLI]` **Le geste d'aujourd'hui.**
   - « Add to test bank » ouvre le brouillon, puis « Add case » l'ajoute : deux clics et une lecture par réponse.
   - Il n'existe que sous une réponse qui a appelé un outil, et pas sous une réponse rouverte depuis l'historique.
   - TaskForce ne propose aucun cas de lui-même.
4. `[ÉTABLI]` **Les signaux déjà au dossier.**
   - Un refus par une règle (`refused`).
   - Une action accordée qui échoue : le 29/10/2026, `create_note` au type inventé, corrigé par `taskforce-fullstack` #438.
   - Une proposition restée sans accord (`pending` sans `human.decision`).
5. `[ÉTABLI]` **L'écran et les accès.**
   - L'écran : Réglages > Test bank (l'interrupteur et sa règle, les cas, le rejeu, les scores).
   - L'API : huit routes sous `/api/workspaces/{slug}/evals`.
   - Le serveur MCP de l'espace expose douze outils (issues, projets, Brain OS, `ask_cortex`, `smart_assign`, indicateurs),
     aucun de la banque.
6. `[ÉTABLI]` **La direction** (R60, séance n°10) : TaskForce aide une entreprise à posséder son intelligence, ses règles,
   ses dossiers, ses évaluations, demain ses modèles ; le premier terrain est la conformité, par un partenaire (R63).
   - Le dossier d'une mission déléguée (V103) suit la même chaîne que celui de Cortex (`EvidenceChain`).
7. `[ÉTABLI]` **Le design.**
   - La carte des workflows (séance n°9, version 14) : le workflow 8, « une erreur devient un cas d'essai », et le
     workflow 9, « changer de modèle ».
   - Les écrans de l'atelier (R54, séance n°8 ; R55 à R59, séance n°9) ne sont pas encore livrés.

## Tour de table `[HYPOTHÈSE]`

| # | Membre | L'essentiel | La solution |
| - | --- | --- | --- |
| 1 | Margaret Hamilton (Science) | Un cas qu'on modifie après l'avoir noté fausse toutes les notes passées. Un cas a des sources ; leur changement doit se détecter avant le rejeu, comme une alarme qui laisse un go/no-go | Des empreintes au cas ; un cas changé est un nouveau cas |
| 2 | Margrethe Vestager (Harmonie) | Des cas que TaskForce propose depuis les dossiers d'une personne restent les siens : elle les voit seule tant qu'elle ne les a pas confirmés, et la règle le dit | Proposer, oui ; publier dans la banque, seulement après accord |
| 3 | Esther Duflo (Science) | Ma réserve tient : Cortex n'est pas le cas d'usage qui paie. Le protocole d'évaluation doit valoir pour toute tâche, et les cas proposés par la machine doivent garder leur origine, pour qu'on mesure s'ils valent les cas choisis par une personne | Un cas indépendant de l'agent, et son origine notée |
| 4 | Satya Nadella (Pont) | Les évaluations sont une plateforme : elles se pilotent par API et par MCP, depuis les outils de l'entreprise, et suivent chaque tâche, pas un assistant | Les gestes de la banque dans l'API et le serveur MCP |
| 5 | Gwynne Shotwell (Impulsion) | Les échecs sont la mine : chaque refus, chaque action accordée qui échoue est un cas tout prêt. Il faut les ramasser sans demander à quelqu'un de tout écrire, et vérifier vite | La machine propose, la personne confirme en lot |
| 6 | Steve Jobs (Impulsion, contradicteur) | Partir de l'expérience : la personne ne pense pas « banque de tests », elle pense « ce modèle fera-t-il aussi bien ? ». La banque se montre au moment où l'on change de modèle, et nulle part ailleurs. Une file d'attente de plus est un écran de plus | La banque dans le workflow 9 ; dire non au reste |
| 7 | Julie Zhuo (Design) | Le geste doit coûter un clic, sinon personne ne le fera. Mais la personne doit voir ce qui entre et pourquoi | « Add as proposed », et le pourquoi sous chaque cas proposé |

## Confrontation `[HYPOTHÈSE]`

### Un cas qui change, ou un cas qui naît ?

- **Shotwell** : un cas figé vieillit ; il faut l'adapter quand l'espace bouge.
- **Hamilton** : adapter en place réécrit l'histoire. Un score de mars n'est plus comparable à un score d'avril si le cas
  a changé entre les deux.
- **Où l'on arrive** : le cas ne change jamais ; il vieillit à vue, et son adaptation est un nouveau cas.
  - Le cas garde les empreintes de ses sources : l'identifiant et la date des notes servies, les projets et les issues
    que sa cassette nomme, la version des règles.
  - Avant un rejeu, TaskForce les compare à l'espace d'aujourd'hui. Un cas dont une source a changé passe « à revoir »,
    avec ce qui a changé, et n'entre pas au score.
  - L'adaptation se propose d'un clic : un nouveau cas, figé sur l'espace d'aujourd'hui, avec les mêmes critères à
    confirmer. L'ancien est archivé avec ses notes.

### Où vit la banque, si Cortex n'est pas le produit ?

- **Duflo** : la banque mesure les tâches de l'entreprise ; Cortex n'en est qu'une.
- **Jobs** : la personne ne cherche pas une banque. Elle se demande si un autre modèle fera aussi bien. La banque doit
  apparaître là, au moment du choix, et quand une tâche vient d'échouer.
- **Nadella** : et elle doit être indépendante de l'agent, pour suivre les missions déléguées aussi.
- **Où l'on arrive** : le cas se tire de tout dossier, et l'écran vit dans les workflows 8 et 9.
  - Le cas ne dépend pas de l'agent : il se tire du dossier d'une réponse de Cortex ou de celui d'une mission. Le rejeu
    d'une mission attend le bac à sable (R67).
  - L'équipe de Jobs dessine la banque dans les workflows 8 et 9 de la carte, à son prochain atelier ; les réglages ne
    gardent que l'interrupteur et la règle.
  - Les mots disent « tâche » et « modèle », pas « Cortex ».

### Confirmer chaque cas, ou laisser la machine proposer ?

- **Shotwell** : les dossiers sont déjà pleins de cas ; personne n'aura le temps de les écrire un par un.
- **Vestager** : un cas tiré des dossiers d'une personne ne se montre pas aux autres avant qu'elle l'ait confirmé.
- **Duflo** : et un cas proposé par la machine garde son origine, pour qu'on mesure s'il vaut un cas choisi.
- **Zhuo** : la confirmation coûte un clic, avec le pourquoi sous les yeux.
- **Où l'on arrive** : la machine propose, la personne confirme vite.
  - Sous une réponse, « Add as proposed » ajoute le cas sans ouvrir le brouillon ; le brouillon reste pour corriger.
  - TaskForce propose lui-même des cas depuis les dossiers qui portent un signal : un refus par une règle, une action
    accordée qui a échoué, une proposition restée sans accord. Ils attendent « à confirmer », visibles de la seule
    personne du dossier, avec leur signal, et se confirment par lots.
  - Un cas n'entre au score qu'une fois confirmé et daté (R68 tient). Son origine, proposée ou choisie, est gardée.

### Un écran d'abord, ou l'API d'abord ?

- **Shotwell** : la banque ne doit pas attendre ses écrans.
- **Nadella** : l'API et le serveur MCP de l'espace suffisent pour commencer ; Claude Code s'en sert déjà.
- **Jobs**, contradicteur : un produit qui se pilote par API n'a pas de forme, et l'utilisateur ne la voit jamais.
- **Zhuo** : la personne doit voir ce qui entre dans la banque ; l'interrupteur et la règle restent à l'écran (R71).
- **Où l'on arrive** : chaque geste sort d'abord dans l'API et le serveur MCP, l'écran suit au plus simple.
  - En faire un cas, rejouer la banque sur un modèle, lire les scores : trois outils MCP de plus.
  - L'écran montre ensuite la même chose, au plus simple : une liste, un bouton, un score par modèle.

## Recommandations `[HYPOTHÈSE]`

### R72. Un cas vieillit à vue, et son adaptation naît d'un clic (R66, réserve de Shotwell)

- Le cas garde les empreintes de ses sources : l'identifiant et la date des notes servies, les projets et les issues
  que sa cassette nomme, la version des règles de l'espace.
- Avant un rejeu, un cas dont une source a changé passe « à revoir », avec ce qui a changé, et n'entre pas au score.
- Son adaptation se propose d'un clic : un nouveau cas, figé sur l'espace d'aujourd'hui, aux critères à confirmer.
  L'ancien est archivé avec ses notes : un cas noté ne change jamais.

- **Pour** : Hamilton, Shotwell, Nadella, Duflo.
- **Contre** : Jobs, en réserve : une alerte de plus sur un écran que personne ne regarde.
- **Preuve en dix jours** : renommer un projet qu'un cas nomme ; le cas passe « à revoir » avant le rejeu suivant, et
  son adaptation se confirme d'un clic.
- **Signal d'arrêt** : un cas « à revoir » compté dans un score, ou un cas noté modifié en place.

### R73. La banque est celle de l'entreprise, pas de Cortex (R67, réserve de Duflo)

- Le cas se tire de tout dossier, celui d'une réponse de Cortex ou celui d'une mission ; le rejeu d'une mission attend
  le bac à sable.
- L'écran vit là où l'on décide : au changement de modèle (workflow 9) et quand une tâche échoue (workflow 8), dessiné
  par l'équipe de Jobs à son prochain atelier. Les réglages ne gardent que l'interrupteur et la règle.
- Les mots disent « tâche » et « modèle », pas « Cortex ».

- **Pour** : Duflo, Jobs, Nadella, Zhuo.
- **Contre** : Shotwell, en réserve : ne pas attendre l'atelier pour figer des cas de missions.
- **Preuve en dix jours** : la carte montre la banque dans les workflows 8 et 9, et la Présidence la valide.
- **Signal d'arrêt** : un écran de la banque qui ne sert que Cortex.

### R74. La machine propose, la personne confirme d'un geste (R68, réserve de Shotwell)

- « Add as proposed » sous une réponse ajoute le cas d'un clic ; le brouillon reste pour corriger.
- TaskForce propose des cas depuis les dossiers qui portent un signal (un refus par une règle, une action accordée qui
  a échoué, une proposition restée sans accord). Ils attendent « à confirmer », visibles de la seule personne du
  dossier, avec leur signal, et se confirment par lots.
- Un cas n'entre au score qu'une fois confirmé et daté. Son origine, proposée ou choisie, est gardée.

- **Pour** : Shotwell, Zhuo, Hamilton, Nadella, Duflo.
- **Contre** : Vestager, en réserve : la règle de la banque doit dire, à l'écran, que TaskForce propose des cas depuis
  les dossiers, et la proposition se coupe avec l'interrupteur. Jobs, contradicteur : une file de plus.
- **Preuve en dix jours** : dix cas confirmés en moins de deux minutes, dont la moitié proposés par TaskForce.
- **Signal d'arrêt** : plus d'un cas confirmé sur dix archivé ensuite comme faux.

### R75. La banque marche sans écran, l'écran suit (R71, réserve de Shotwell)

- Chaque geste de la banque passe par l'API et par le serveur MCP de l'espace : en faire un cas, rejouer la banque sur
  un modèle, lire les scores.
- Une capacité nouvelle sort d'abord là ; l'écran la montre ensuite, au plus simple.
- L'interrupteur et la règle restent à l'écran (R71 tient).

- **Pour** : Shotwell, Nadella, Hamilton.
- **Contre** : Jobs, contradicteur : un produit sans forme. Zhuo, en réserve : la personne doit voir ce qui entre dans la
  banque, même quand un client MCP l'y met.
- **Preuve en dix jours** : la banque rejouée depuis Claude Code par le serveur MCP de l'espace, et ses scores lus au
  même endroit.
- **Signal d'arrêt** : une capacité de la banque qui attend son écran.

## Décision de la Présidence

Le 30/10/2026 : « je suis d'accord avec tout les R, et je suis aussi d'accord avec Jobs sur ses points donc on le suit ».
La Présidence demande aussi des explications plus explicites.

| Recommandation | Décision | Ce que la décision veut dire |
| --- | --- | --- |
| R72 | Retenue | Un cas dont l'espace a changé sort du score et s'adapte d'un clic. Avec Jobs : « à revoir » se lit dans la banque, au moment du rejeu, pas dans une alerte de plus |
| R73 | Retenue | La banque est celle de l'entreprise ; l'équipe de Jobs la dessine dans les workflows 8 et 9 |
| R74 | Retenue, dans l'ordre de Jobs | « Add as proposed » d'abord ; la file des cas que TaskForce propose attend les écrans de base |
| R75 | Retenue, dans l'ordre de Jobs | Les routes de l'API existent ; les outils MCP de la banque attendent les écrans de base |
| Désaccord de Jobs | Suivi | Se concentrer, c'est dire non : aucune surface nouvelle (une file, des outils MCP) avant les écrans de base du produit |

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 29/10/2026 à 22:39 UTC (`shuf`). Contradicteur désigné : Steve Jobs.
- **Le désaccord de Jobs** porte sur l'ordre, pas sur le fond : il ne refuse ni l'adaptation (R72) ni la banque hors de
  Cortex (R73), qu'il porte ; il refuse d'ajouter des surfaces (une file, des outils MCP) avant les écrans de base.
- **Ce que la séance ne tranche pas** : le format de l'export (R64), le registre des modèles par tâche (le lot suivant de
  R61), le rejeu des missions (le bac à sable).

## Suites

Dans l'ordre de Jobs, que la Présidence suit :

1. **L'atelier des écrans** de l'équipe de Jobs : les écrans de base du produit (R54, R55 à R59), et la banque dans les
   workflows 8 et 9 (R73).
2. **Le lot 2 de la banque** : les empreintes et l'adaptation, lues au moment du rejeu (R72) ; « Add as proposed » (R74).
3. **Après les écrans de base** : la file des cas proposés par TaskForce (R74) et les outils MCP de la banque (R75).
4. **Ensuite** : le registre des modèles par tâche (R61), puis l'export (R64).
