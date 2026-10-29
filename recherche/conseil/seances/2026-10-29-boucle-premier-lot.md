---
id: conseil-seance-2026-10-29-boucle-premier-lot
title: "Séance n°11 du 29/10/2026 : construire la boucle (R61), le premier lot"
doc_type: pv-seance
statut: active
date: "29/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, evaluations, boucle, cortex, modeles]
related:
  - "../README.md"
  - "./2026-10-29-intelligence-possedee.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°11 du 29/10/2026 : construire la boucle (R61), le premier lot

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

La boucle de R61 commence par Cortex et par des cas figés.

- **Le cas** : la question, ce que les outils de lecture ont rendu à l'époque (pris au dossier), et des critères qu'un
  programme vérifie.
- **Le rejeu** :
  - il ne touche jamais l'espace d'aujourd'hui (C2) ;
  - un outil de lecture reçoit la réponse gardée ;
  - toute écriture se joue à blanc : le noyau la propose, rien ne s'exécute.
- **L'attendu** vient de l'acte que la personne a validé, et ses critères sont figés avant toute comparaison.
- **Les notes** sont données par du code, pas par un modèle.
- **Le modèle** qui a répondu entre au dossier de chaque réponse.
- **La banque** n'entre au produit qu'avec son écran et son interrupteur : c'est la leçon de la capture retirée le
  18/10.

Six recommandations, R66 à R71, retenues par la Présidence le 29/10/2026, quatre avec la réserve d'un membre.

Désaccord conservé : pour Esther Duflo, contradictrice, dix cas écrits par une personne mesurent ses souvenirs, pas un
modèle. La banque vaut ce que vaut son protocole.

- **Saisine** (Présidence, 29/10/2026) : « go release, puis enchaîne sur R61 ». Puis : « Dis-moi après tout ce que je
  dois faire, répondre et pk stp qu'on avance en parrallele. Consulte le conseil a chaque fois stp ».
  - Question posée par le secrétariat : par quoi commencer la boucle, et qu'est-ce qu'un cas d'évaluation, pour qu'en
    dix jours un changement de modèle se décide sur preuve ?
- **Formation** : restreinte (7), un membre au moins par pôle :
  - Gwynne Shotwell (Impulsion), Satya Nadella (Pont), Margrethe Vestager (Harmonie) ;
  - Margaret Hamilton, Fei-Fei Li et Esther Duflo (Science) ;
  - Julie Zhuo (Design).
  - Ordre de parole tiré au sort le 29/10/2026 à 19:09 UTC : Vestager, Zhuo, Nadella, Duflo, Hamilton, Li, Shotwell.
  - Contradictrice désignée : Esther Duflo. Bezos l'était à la n°10.
- **Fiches** : toutes à jour (moins de 30 jours). Hamilton, siège historique, ne se rafraîchit que sur une nouvelle
  source historique.

## Dossier

1. `[ÉTABLI]` **Le noyau pour Cortex est en production** depuis la 1.6.5 (29/10/2026, migration V107 appliquée à 19:08).
   Chaque réponse qui appelle un outil garde un dossier chaîné : la question, l'outil demandé et ses arguments, la
   décision de la règle, le résultat, et l'accord de la personne quand il y en a un.
2. `[ÉTABLI]` **Le dossier d'une mission déléguée** (V103) garde les demandes, les décisions, les sorties des tests et
   les sorties de la copie.
3. `[ÉTABLI]` **`ai_runs`** (V35) garde, par appel, la fonction, le fournisseur, le modèle, la latence, les jetons et le
   statut. Seul Smart Assign l'écrit. Le dossier de Cortex ne garde pas le modèle qui a répondu.
4. `[ÉTABLI]` **La capture « data flywheel » a déjà été construite puis retirée.**
   - La table `ai_generations` (V81) gardait le brouillon de l'IA, ce que la personne retenait, et un signal : accepté,
     modifié ou rejeté (#213).
   - Elle a été retirée le 18/10/2026 (`5700e4b1`) : l'accord qui l'activait ne pouvait pas se donner, faute d'écran ou
     d'endpoint. La table est restée vide, et rien ne la lisait. La table et sa colonne restent en base.
   - La note [[Data_Flywheel_et_Apprentissage]] la dit encore faite (§5).
5. `[ÉTABLI]` **Le choix du modèle aujourd'hui.**
   - La passerelle traduit un tier (`fast`, `standard`, `deep`) en modèle. Sans réglage, c'est qwen3:8b sur Ollama
     pour les deux tiers de conversation (`ai-service/app/config.py`).
   - L'app desktop choisit le modèle de conversation et le modèle rapide parmi les modèles d'Ollama installés.
   - Cortex appelle le tier `fast`, ou celui des outils MCP. Il n'existe aucun registre par tâche.
6. `[ÉTABLI]` **Le noyau sait jouer une écriture à blanc** : une action demandée est proposée, rien ne s'exécute
   (`AgentService`, §13.11 de la spécification).
7. `[ÉTABLI]` **Les bancs qui existent** :
   - 44 cas de règles (`contracts/rules/cases.json`), rejoués par le serveur et par le runner ;
   - les suites de la porte du runner ;
   - la banque de tests de la spécification (§16.2), dont la famille « modèles » ;
   - les expériences E11 et E12.
8. `[ÉTABLI]` **Les contraintes du labo** :
   - C1 : un seul espace réel ;
   - C2 : le monde n'est pas rejouable, une tâche passée ne se rejoue pas dans le même état ;
   - C3 : l'horloge est lente.

## Tour de table `[HYPOTHÈSE]`

| # | Membre | L'essentiel | Par quoi commencer ? |
| - | --- | --- | --- |
| 1 | Margrethe Vestager (Harmonie) | La boucle appartient à l'entreprise : ce qui entre dans la banque se dit à la personne, avec un réglage qui se trouve, et en sort en format ouvert. Une capture sans interrupteur visible vaut un accord implicite | Par le consentement et l'export, dès le premier cas |
| 2 | Julie Zhuo (Design) | Partir d'une tâche que la personne fait vraiment : ses questions à Cortex. La confiance se gagne par des évaluations, mais une banque se nourrit d'un geste, « en faire un cas », à côté d'une réponse | Par Cortex, et un geste sur la réponse |
| 3 | Satya Nadella (Pont) | Garder chez soi évaluations et traces, découplées de tout modèle unique. Le premier lot doit montrer qu'on change de modèle sans perdre la mémoire : la banque, et le modèle noté au dossier de chaque réponse | Par la banque, et le modèle au dossier |
| 4 | Esther Duflo (Science, contradictrice) | Dix cas écrits après coup par une personne mesurent ses souvenirs : biais rétrospectif, et des cas choisis selon ce qui l'a marquée. Écrire les critères avant de voir le nouveau modèle, garder les réussites comme les échecs, dire d'avance ce qui ferait abandonner | Par un protocole, pas par une fonction |
| 5 | Margaret Hamilton (Science, historique) | Un cas est figé et vérifiable par du code : la demande, ce que l'agent a lu, ce qu'il devait faire. Rejouer dans l'espace d'aujourd'hui n'est pas un test (C2). Aucun changement de modèle sans la banque rejouée | Par des cas figés, notés par du code |
| 6 | Fei-Fei Li (Science) | Faire confiance, mais vérifier : pas de modèle juge tant que son erreur n'est pas mesurée ; d'abord des vérifications simples, et des cas de sûreté dans la banque | Par des notes déterministes, sûreté comprise |
| 7 | Gwynne Shotwell (Impulsion) | Un échec est une mine de données : les dossiers de Cortex en sont déjà pleins. Ne pas attendre un écran parfait : la banque rejouée d'un clic, sur deux modèles, cette semaine | Par les dossiers déjà écrits |

## Confrontation `[HYPOTHÈSE]`

### Rejouer le dossier, ou figer le cas ?

- **Shotwell** veut rejouer les dossiers tels quels.
- **Hamilton** objecte que le monde a bougé : rejouer `list_projects` aujourd'hui lit l'espace d'aujourd'hui, pas celui
  de la question (C2). Le cas mesurerait alors le changement de l'espace autant que le modèle.
- **Où l'on arrive** : le cas est figé.
  - Il garde la question, et ce que chaque outil de lecture a rendu à l'époque, déjà présent au dossier.
  - Au rejeu, le nouveau modèle reçoit la réponse gardée s'il appelle le même outil avec les mêmes arguments.
  - Un appel hors du cas est noté, jamais lancé sur l'espace.
  - Toute écriture se joue à blanc.

### Qui écrit l'attendu ?

- **Duflo** : une personne qui écrit l'attendu après avoir vu la réponse le réécrit selon ce qu'elle sait maintenant.
- **Zhuo** : sans un geste simple sur la réponse, personne n'écrira de cas.
- **Où l'on arrive** : l'attendu vient de l'acte que la personne a validé.
  - C'est l'outil et les arguments qu'elle a accordés, la réponse qu'elle a gardée, ou l'outil qui n'aurait pas dû
    partir.
  - TaskForce propose les critères à partir du dossier ; la personne les confirme.
  - Les critères sont figés et datés avant qu'un nouveau modèle soit rejoué, et réussites comme échecs entrent dans la
    banque.

### Un modèle peut-il noter ?

- **Nadella** : un juge d'un autre fournisseur noterait le texte libre, qu'un programme note mal.
- **Li et Hamilton** : pas de juge avant que son erreur soit mesurée (R15, R18).
- **Où l'on arrive** : au premier lot, des notes par du code seulement :
  - l'outil attendu ou interdit ;
  - les arguments ;
  - l'effet de la règle ;
  - les mots attendus ou interdits dans la réponse.

### Une banque sans interrupteur ?

- **Vestager** rappelle la capture de V81 : construite, jamais activable, jamais lue, puis retirée.
- **Où l'on arrive** : la banque n'entre au produit qu'avec son lecteur et son interrupteur. Le lecteur, c'est la liste
  des cas et le score par modèle. L'interrupteur, c'est le geste « en faire un cas » et un réglage qui se trouve.
  L'export en format ouvert vient ensuite (R64).

## Recommandations `[HYPOTHÈSE]`

### R66. Un cas est figé, pas rejoué

- La question, ce que les outils de lecture ont rendu à l'époque (pris au dossier), et des critères qu'un programme
  vérifie.
- Au rejeu, un outil de lecture appelé avec les mêmes arguments reçoit la réponse gardée ; un appel hors du cas est
  noté, jamais lancé sur l'espace d'aujourd'hui (C2).
- Toute écriture se joue à blanc : le noyau la propose, rien ne s'exécute.

- **Pour** : Hamilton, Li, Nadella, Duflo.
- **Contre** : Shotwell, en réserve : un cas figé vieillit, il se retire quand l'espace a changé.
- **Preuve en dix jours** : dix cas rejoués sans une écriture ni une lecture de l'espace.
- **Signal d'arrêt** : un rejeu qui écrit dans l'espace, ou qui lit l'espace d'aujourd'hui.

### R67. Le premier lot vise Cortex

- Ses tâches sont courtes, son modèle se choisit déjà par tier, et ses dossiers existent depuis la 1.6.5.
- La délégation (le code) viendra après, avec le bac à sable.

- **Pour** : Zhuo, Shotwell, Nadella, Hamilton.
- **Contre** : aucun. Réserve de Duflo : Cortex n'est pas le cas d'usage qui paie.
- **Preuve en dix jours** : dix cas tirés des étapes de la recette (le projet nommé, le projet ambigu, l'échéance, les
  issues bloquées, la note proposée), rejoués sur deux modèles de l'app desktop, avec leur score.
- **Signal d'arrêt** : moins de dix cas utiles en trente jours.

### R68. L'attendu vient de l'acte validé, figé avant la comparaison

- TaskForce propose les critères à partir du dossier : l'outil et les arguments accordés, la réponse gardée, ou l'outil
  qui n'aurait pas dû partir. La personne les confirme.
- Les critères sont datés et figés avant qu'un nouveau modèle soit rejoué.
- Réussites et échecs entrent tous deux dans la banque.

- **Pour** : Duflo, Zhuo, Hamilton, Li.
- **Contre** : Shotwell, en réserve : confirmer chaque cas ralentit la banque.
- **Preuve en dix jours** : chaque cas porte la date de ses critères, antérieure à tout rejeu.
- **Signal d'arrêt** : un critère changé après avoir vu le résultat d'un modèle.

### R69. Des notes par du code, pas par un modèle

- L'outil attendu ou interdit, ses arguments, l'effet de la règle, les mots attendus ou interdits dans la réponse.
- Des cas de sûreté : une demande hors du domaine, une écriture que personne n'a demandée.
- Un modèle juge viendra d'un autre fournisseur, son erreur mesurée avant qu'il note (R15, R18).

- **Pour** : Li, Hamilton, Duflo.
- **Contre** : Nadella, en réserve : le texte libre restera mal noté.
- **Preuve en dix jours** : chaque note se refait à l'identique sur les mêmes sorties.
- **Signal d'arrêt** : une note qui change alors que la sortie n'a pas changé.

### R70. Le modèle au dossier de chaque réponse

- Le début du dossier de Cortex garde le fournisseur, le modèle et le tier qui ont répondu.
- La comparaison de deux modèles cite les deux. Le registre par tâche (le lot suivant) part de là.

- **Pour** : Nadella, Hamilton, Vestager.
- **Contre** : aucun.
- **Preuve en dix jours** : chaque dossier de Cortex dit quel modèle a répondu.
- **Signal d'arrêt** : une réponse sans modèle à son dossier.

### R71. Pas de capture sans lecteur ni interrupteur

- La banque entre au produit avec son écran (les cas, le score par modèle, le geste « en faire un cas ») et sa règle
  (qui ajoute un cas, ce qui en sort).
- Elle reste dans l'espace. L'export en format ouvert vient ensuite (R64).
- C'est la leçon de V81 : une capture qu'on ne peut ni activer ni lire meurt vide.

- **Pour** : Vestager, Zhuo, Nadella, Duflo.
- **Contre** : Shotwell, en réserve : l'écran ne doit pas retarder la banque.
- **Preuve en dix jours** : la personne trouve la banque, ajoute un cas et la coupe, en moins d'une minute.
- **Signal d'arrêt** : une table que rien ne lit au bout de trente jours.

## Décision de la Présidence

Le 29/10/2026, R66 à R71 retenues. La Présidence fait siennes trois réserves de Shotwell et celle de Duflo, et demande
une solution pour chacune.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R66 | Retenue, avec la réserve de Shotwell | « on pourrait combiner les 2 » : un cas ne reste pas figé ; quand l'espace change, une adaptation naît |
| R67 | Retenue, avec la réserve de Duflo | « c'est pas Cortex notre produit, attention » : un changement d'UI/UX, côté Jobs |
| R68 | Retenue, avec la réserve de Shotwell | « nous faut une solution pour ca » : confirmer chaque cas ne doit pas ralentir la banque |
| R69 | Retenue | « d'accord » |
| R70 | Retenue | « d'accord » |
| R71 | Retenue, avec la réserve de Shotwell | « faut trouver une solution » : l'écran ne doit pas retarder la banque |

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 29/10/2026 à 19:09 UTC (`shuf`). Contradictrice désignée : Esther Duflo.
- **La Présidence a demandé d'enchaîner sur R61** en consultant le Conseil. Le premier lot se construit donc selon ces
  recommandations, sur une branche, et ne se fusionne pas avant sa décision.
- **Une note périmée** : [[Data_Flywheel_et_Apprentissage]] dit la capture de V81 faite, alors qu'elle a été retirée le
  18/10/2026. À corriger, avec la source (`5700e4b1`).

## Suites

- **Le premier lot** (R66 à R71) : les cas figés de Cortex, le rejeu à blanc, les notes par du code, le modèle au dossier,
  l'écran de la banque. Construit et vérifié en développement, `taskforce-fullstack` #437.
- **Les réserves retenues** : un cas qui s'adapte quand l'espace change (R66), un produit qui n'est pas Cortex (R67), une
  confirmation qui ne ralentit pas la banque (R68), un écran qui ne la retarde pas (R71). Le secrétariat les porte au
  Conseil.
- **Le lot suivant** : le registre des modèles par tâche, qui part du modèle au dossier (R70).
- **Ensuite** : l'export en format ouvert (R64), puis E12.
