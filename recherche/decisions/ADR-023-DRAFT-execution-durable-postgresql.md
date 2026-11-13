---
id: adr-023-execution-durable-postgresql
title: "ADR-023 (à promouvoir) : l'exécution durable sur PostgreSQL, les mécanismes de Temporal et d'Operaton refaits chez nous"
doc_type: adr
statut: active
version: 1.1
date: "13/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, execution-durable, temporal, operaton, postgresql, fiabilite, conseil]
related:
  - "../conseil/seances/2026-11-01-feuille-de-route.md"
  - "../conseil/seances/2026-11-13-depasser-camunda.md"
  - "../conseil/seances/2026-11-13-le-workflow-pilotable.md"
  - "./ADR-027-DRAFT-modele-des-processus.md"
  - "../experiences/Experiences.md"
  - "../../v1/road_to_v2/Specification_V2_Harnais.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-023 (à promouvoir) : l'exécution durable sur PostgreSQL, les mécanismes de Temporal et d'Operaton refaits chez nous

> **Ratifié par la Présidence le 01/11/2026** (séance n°15 du Conseil : R97 retenue). **Amendé le 13/11/2026** (séance n°24 :
> R167 retenue et amendée, pas de fork d'Operaton). Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 023 dès que
> l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 01/11/2026 ; amendé le 13/11/2026. La version 1 se mesure en J2, par les essais de coupure (E21), face à Operaton
pris comme témoin. Les seuils de l'essai sont recommandés par la séance n°25 (R177) et attendent la Présidence.

## Contexte

- `[ÉTABLI]` Les missions passent par une file en base, sans moteur durable ni reprise. Les événements du runner vivent
  en mémoire. Une mission perdue n'est déclarée que quand quelqu'un ouvre l'issue (séance n°14, Hamilton). Au 13/11/2026, une
  mission avance quand on la lit ; le travail de fond est `@Async` plus la réclamation et le battement du runner ; aucun
  processus n'existe (carte du code de `origin/dev`).
- `[ÉTABLI]` La feuille de route fait des processus (des étapes d'agents, de décisions humaines et d'outils) le cœur de
  la démo : ils doivent survivre à une coupure, à une mise en veille, à un redémarrage. Le critère 6 de J2 : le processus
  « intégrer un module » de bout en bout, repris après un redémarrage.
- `[ÉTABLI]` Temporal : son moteur d'exécution durable est sous licence MIT, gratuit à auto-héberger, avec un SDK Java
  natif ([Temporal](https://temporal.io/llm-info)). Il demande son propre serveur et sa propre base.
- `[ÉTABLI]` Ce que fait le moteur de Temporal ([workflows](https://docs.temporal.io/workflows),
  [reprises](https://docs.temporal.io/encyclopedia/retry-policies), lus le 13/11/2026) :
  - un historique d'événements, complet et ordonné, est la source de vérité d'une exécution ; après une panne, le code du
    workflow se rejoue depuis le début, guidé par cet historique, qui le ramène à son état ;
  - ce code doit donc être déterministe : l'heure, le hasard et les appels au monde passent par des API qui s'enregistrent ;
  - une activité (un appel d'API, de base, de modèle, un fichier) s'exécute, et son résultat entre à l'historique ; au rejeu, le
    résultat enregistré sert, l'activité ne se refait pas ;
  - la politique de reprise d'une activité, par défaut : 1 seconde d'abord, un facteur de 2, un plafond de 100 fois le premier
    délai, un nombre de tentatives illimité ; un workflow, lui, ne se reprend pas par défaut ; une activité doit être idempotente.
- `[ÉTABLI]` Operaton : issu de Camunda 7 Community, sous Apache 2.0, un moteur BPMN 2.0 qui tourne dans la JVM, embarquable dans
  une application Java ou Spring Boot, sur PostgreSQL entre autres, JDK 17 au moins (testé sur 17, 21 et 25)
  ([dépôt](https://github.com/operaton/operaton), lu le 13/11/2026). La séance n°24 relevait la version 2.2.1 du 07/11/2026.
- `[ÉTABLI]` Ce que fait le moteur d'Operaton (documentation, lue le 13/11/2026 :
  [transactions](https://docs.operaton.org/docs/documentation/user-guide/process-engine/transactions-in-processes),
  [exécuteur de travaux](https://docs.operaton.org/docs/documentation/user-guide/process-engine/the-job-executor),
  [incidents](https://docs.operaton.org/docs/documentation/user-guide/process-engine/incidents)) :
  - le moteur est un code passif qui travaille dans le fil de l'appelant ; à un état d'attente, il sauve l'exécution en base et
    attend d'être relancé ; le passage d'un état sauvé au suivant est une transaction ; une exception la défait, et l'instance
    revient au dernier état d'attente ;
  - `asyncBefore` et `asyncAfter` posent une frontière de transaction avant ou après une activité ; ces suites asynchrones sont
    toujours exécutées par l'exécuteur de travaux, dans une transaction à part ;
  - l'exécuteur lit la table `ACT_RU_JOB` : un travail est pris quand il est dû, déverrouillé, qu'il lui reste des reprises et
    qu'il n'est pas suspendu ; il le verrouille en deux temps (lire, puis poser `LOCK_EXP_TIME_` et `LOCK_OWNER_`), sous un verrou
    optimiste par la colonne `REV_` ; l'attente entre deux lectures double, jusqu'à 60 secondes par défaut ;
  - un travail échoué est repris deux fois par défaut (trois exécutions en tout), plus tard et non tout de suite ; un échec dû au
    verrou optimiste ne décompte pas de reprise ; à zéro, le moteur s'arrête sur ce travail, signale qu'il ne peut pas continuer,
    et un incident se crée ; il se résout quand le travail est relancé à la main ou que ses reprises remontent ;
  - les travaux d'une même instance sont exclusifs par défaut : l'exécuteur les passe l'un après l'autre ;
  - les effets hors de la transaction (un fichier, un service web) ne se défont pas : la documentation renvoie à une
    consolidation par les reprises.
- `[ÉTABLI]` La licence : l'ASF tient la licence Apache 2.0 pour compatible avec la GPLv3 dans un seul sens : du code sous Apache
  2.0 peut entrer dans un projet sous GPLv3, pas l'inverse ([ASF](https://www.apache.org/licenses/GPL-compatibility.html), lu le
  13/11/2026). TaskForce est sous AGPL v3.
- `[ÉTABLI]` L'app desktop embarque déjà PostgreSQL, le backend Java, l'interface et le runner sur la machine de la
  personne (`desktop/README.md`).
- `[ÉTABLI]` La Présidence, le 01/11/2026 : « on pourrait copier Temporal si jamais ». Le 13/11/2026, sur R167 : « Mais faire un
  fork direct, ça je suis pas fan. Parce que ça fait vraiment copier-coller pour le coup. » ; « je préfère que tu copies le code
  plutôt que tu fasses, enfin, que tu copies, que tu t'inspires du code, que tu ailles voir vraiment les fichiers, comment ça
  fonctionne, que tu reproduises la même chose chez nous, adapté évidemment à chez nous, plutôt que tu fasses un fork directement.
  Donc c'est peut-être plus de boulot, mais je préfère largement. »

## Décision

On reproduit chez nous, en Java, dans le backend, sur la base PostgreSQL qui existe déjà, ce que font les moteurs de Temporal et
d'Operaton, adapté à TaskForce. On ne forke pas Operaton et on ne l'embarque pas : on lit son code, on comprend ses mécanismes, on
les refait.

1. **Un journal d'événements par instance de processus** (Temporal). Après une panne, la logique du processus se rejoue sur le
   journal et reprend où elle s'était arrêtée ; rien n'est fait deux fois. La logique reste déterministe ; tout ce qui touche au
   monde passe par une étape.
2. **Les états d'attente sont les points de sauvegarde** (Operaton). Une instance avance d'un état d'attente au suivant dans une
   transaction ; une exception la ramène au dernier état sauvé. Chaque étape d'agent, chaque tâche humaine, chaque attente est un
   état d'attente : une coupure n'y perd rien.
3. **Une table des travaux** (Operaton). Chaque travail a son échéance, son propriétaire de verrou, l'expiration de ce verrou, ses
   reprises restantes et une révision pour le verrou optimiste. On le prend en deux temps : lire les travaux dus, puis les
   verrouiller. Un travail dont le verrou expire se reprend par un autre. Les travaux d'une même instance passent l'un après
   l'autre.
4. **Des reprises, puis l'incident** (Operaton). Un échec retire une reprise ; un conflit de verrou n'en retire pas. Par défaut,
   trois tentatives au plus, avec un délai qui croît : jamais de reprise illimitée sur une étape d'agent, qui coûte et agit. À
   zéro, le moteur s'arrête sur l'étape et crée un incident, un objet avec son étape, sa cause et son heure, que la vue montre sur
   le nœud. Une personne le résout : relancer, passer l'étape avec une raison quand elle n'est pas verrouillée, ou arrêter.
5. **Des effets idempotents** (Temporal). Chaque effet sur le monde (un appel d'agent, de modèle ou d'outil, une écriture chez
   l'entreprise) porte une clé d'idempotence ; avant de refaire une étape, le moteur vérifie au dossier si l'effet a déjà eu lieu.
6. **Des minuteries, des messages et des signaux.** Une attente est une minuterie ou un message : un document fourni, une
   réponse, un autre processus fini. Un accord humain est un signal ; l'échéance d'un accord est une minuterie de bordure, et ce
   qui suit l'échéance est écrit dans la définition (aujourd'hui : « No answer in time: refused »).
7. **Des baux, et la reprise des exécutions perdues par le serveur** (spécification de la v2, §13.2) ; **les événements du
   runner écrits sur disque d'abord**, puis renvoyés après une coupure.
8. **Les priorités, et ce que le système lâche d'abord quand il sature**, écrits avant (Hamilton).
9. **Chaque geste passe par les règles et entre au dossier** : relancer, passer une étape, arrêter, résoudre un incident. Chaque
   transition d'une instance est un événement du dossier, chaîné et scellé.
10. **Le modèle des processus ne dépend pas du moteur** ([ADR-027](./ADR-027-DRAFT-modele-des-processus.md)). L'export BPMN du
    sous-ensemble permet de changer de moteur ; Temporal reste possible pour un grand serveur.
11. **La licence.** Lire le code d'Operaton est libre. `[DÉDUIT]` Si un fichier ou un passage substantiel en est repris tel quel,
    il garde sa mention de droit d'auteur, la licence Apache 2.0 et le fichier NOTICE (Apache 2.0, §4), et il peut entrer dans
    TaskForce sous AGPL v3. La règle de la Présidence reste : reproduire le mécanisme, adapté, plutôt que copier.

## La preuve : les essais de coupure, Operaton en témoin (E21)

- **Le même processus** : celui d'E20, « intégrer un module », écrit dans le sous-ensemble et exporté en BPMN (E23), tourne sur
  notre moteur dans l'app desktop, et sur Operaton dans un banc d'essai seulement, à version figée, jamais livré ni modifié.
- **Les mêmes coupures** : le runner tué, le backend tué, la machine mise en veille, au milieu d'une étape d'agent, d'une tâche
  humaine et d'une attente.
- **Les seuils, écrits avant l'essai** (R167 et ses amendements ; recommandés par la séance n°25, R177, en attente de la
  Présidence) : aucune étape perdue ; aucun effet fait deux fois ; l'instance repart seule dans les 30 secondes qui suivent le
  retour du backend ou le réveil de la machine ; au repos, le moteur ajoute au plus 50 Mo de mémoire et 1 % d'un cœur à l'app
  desktop.
- **Ce que le témoin fait mieux** s'écrit, et le mécanisme qui fait la différence se reprend chez nous.
- L'activité du projet Operaton, critère de la séance n°24 pour choisir une dépendance, devient sans objet : Operaton n'est pas
  une dépendance de TaskForce.

## Alternatives considérées

| Alternative | Pourquoi écartée |
| --- | --- |
| Forker Operaton | La Présidence, le 13/11/2026 : « faire un fork direct, ça je suis pas fan » |
| Embarquer Operaton tel quel, comme dépendance | Un moteur BPMN complet à tenir dans l'app desktop, avec son modèle d'exécution (variables, délégués, tables d'historique) à côté de nos règles, de nos accords et de notre dossier ; la Présidence veut « que tu reproduises la même chose chez nous, adapté évidemment à chez nous ». Il reste le témoin des essais |
| Embarquer le serveur de Temporal | Un serveur de plus et sa base, sur chaque machine de l'app desktop |
| Zeebe (Camunda 8) | Sa production auto-hébergée exige une licence payante (séance n°24, dossier, point 7) |
| Garder la file en base | Ni reprise, ni minuterie, ni signal : les missions se perdent (séance n°14) |

## Conséquences

- **Positives**
  - Un processus ne se perd plus, et le dossier dit chaque coupure et chaque reprise.
  - Les accords humains deviennent des signaux durables : une décision attendue survit à un redémarrage.
  - L'incident devient un objet, montré là où il s'est produit, et résolu par une personne.
  - Les mécanismes de deux moteurs éprouvés, adaptés aux règles, aux accords et au dossier de TaskForce, sans dépendance de plus.
- **Négatives**
  - Plus de travail qu'un fork ; la Présidence l'accepte : « Donc c'est peut-être plus de boulot, mais je préfère largement. »
  - Un moteur à tenir : il se teste par des coupures provoquées à chaque jalon, et le témoin se garde à jour dans le banc.
  - La logique d'un processus doit rester déterministe ; tout ce qui touche au monde passe par une étape.
- **À surveiller** : une mission perdue découverte par une personne (le signal d'arrêt de R97) ; une étape perdue ou faite deux
  fois pendant un essai de coupure (le signal d'arrêt de R167).

## Plan de déploiement

- **J2** (le lot W3 de la séance n°25) : la version 1, réduite à ce qu'exige le processus d'E20 : le journal, les états
  d'attente, la table des travaux et ses verrous, les reprises et l'incident, les minuteries, les messages, les accords en
  signaux, les clés d'idempotence ; mesurée par E21, Operaton en témoin.
- **J5** : les baux et la reprise des exécutions perdues par le serveur, les priorités et le délestage, les événements du runner
  sur disque ; la modification et la migration d'une instance, et la compensation (la table de R165).

## Liens

- [PV de la séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md), R97
- [PV de la séance n°14](../conseil/seances/2026-10-31-souverainete-operationnelle.md), l'intervention de Hamilton
- [PV de la séance n°24](../conseil/seances/2026-11-13-depasser-camunda.md), R167 et la décision de la Présidence
- [PV de la séance n°25](../conseil/seances/2026-11-13-le-workflow-pilotable.md), R177
- [ADR-027](./ADR-027-DRAFT-modele-des-processus.md), le modèle des processus
- [Spécification de la v2](../../v1/road_to_v2/Specification_V2_Harnais.md), §13.2

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 13/11/2026 · **v1.1** · Projet Taskforce
