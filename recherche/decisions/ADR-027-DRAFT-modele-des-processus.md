---
id: adr-027-modele-des-processus
title: "ADR-027 (brouillon) : le modèle des processus, un sous-ensemble de BPMN 2.0 montré et édité dans TaskForce sans ses symboles"
doc_type: adr
statut: proposed
version: 0.1
date: "13/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, processus, bpmn, workflow, versions, conseil]
related:
  - "../conseil/seances/2026-11-13-depasser-camunda.md"
  - "../conseil/seances/2026-11-13-le-workflow-pilotable.md"
  - "./ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "./ADR-023-DRAFT-execution-durable-postgresql.md"
  - "./ADR-025-DRAFT-un-seul-moteur-de-regles.md"
  - "../../v1/13-roadmap/Roadmap_Backlog.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-027 (brouillon) : le modèle des processus, un sous-ensemble de BPMN 2.0 montré et édité dans TaskForce sans ses symboles

> **Brouillon, sans autorité avant sa promotion** ([Gabarits](../Gabarits.md) §6). Il naît de R165 et de R169, retenues par la
> Présidence le 13/11/2026 au soir (séance n°24), R165 élargie. Son détail suit la séance n°25 (R174 à R176), dont les
> recommandations attendent la Présidence. Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 027 après sa
> ratification.

## Statut

Proposé le 13/11/2026. Se construit en J2 pour le seul processus d'E20 (les lots W2 et W4 de la séance n°25), puis s'élargit
après J2 (W6, W8).

## Contexte

- `[ÉTABLI]` Aucun processus n'existe : TF-J2-2 (« un canevas modifiable, cinq types d'étapes, exécuté par le moteur durable
  v1 ») n'est pas commencé ; le code n'a que `RuleScope.PROCESS` et un champ de processus toujours vide (carte du code de
  `origin/dev`, 13/11/2026). La mission suit cinq étapes fixes en phrases : Understand, Plan, Do, Check, Hand over (R138,
  `lib/delivery/mission-sequence.ts`).
- `[ÉTABLI]` Les règles de l'entreprise sont des données versionnées : chaque version est immuable, avec son auteur et son
  empreinte (TF-J2-4, V125).
- `[ÉTABLI]` R165 (séance n°24) propose un sous-ensemble de BPMN 2.0 et cinq types d'étapes, « pour l'échange, jamais pour
  l'interface ». La Présidence, le 13/11/2026, l'élargit : « import-export seulement, bah, effectivement on peut rajouter un
  import-export, mais pas seulement » ; les workflows « qu'on va pouvoir afficher et éditer par les ingénieurs, les utilisateurs,
  etc. Et puis par les PM aussi » ; « on n'est pas orienté full code » ; sur la vue, « Je suis pas en train de faire des schémas
  d'ELEC ». Elle veut des workflows par défaut, l'IA qui juge ce qui est de trop, et des workflows créés par les utilisateurs
  (l'exemple du LIMS).
- `[ÉTABLI]` R169 : l'objectif propose un brouillon, une personne l'arrête, le moteur exécute ; le brouillon s'accepte étape par
  étape, sans « tout accepter ».
- `[ÉTABLI]` BPMN 2.0.2 (OMG, formal/2013-12-09) définit, à côté de la conformité complète, trois sous-classes de la modélisation :
  « Descriptive », « Analytic » et « Common Executable », cette dernière pour les outils qui produisent des modèles exécutables ;
  elle exige XML Schema, WSDL et XPath, et comprend notamment les tâches de service et humaines, les passerelles exclusive,
  parallèle et à événements, le sous-processus intégré, les événements de minuterie et de message ; la zone ad hoc n'en fait pas
  partie ([OMG](https://www.omg.org/spec/BPMN/2.0.2/PDF), chapitre 2, lu le 13/11/2026).
- `[ÉTABLI]` 21 CFR 11.10(f) demande des contrôles du système qui imposent l'ordre permis des étapes et des événements
  ([21 CFR 11.10](https://www.law.cornell.edu/cfr/text/21/11.10), lu le 13/11/2026). Le projet d'annexe 22 des BPF de l'UE écarte
  l'IA générative et les LLM des usages critiques, et veut une personne dans la boucle ailleurs (consultation close le 07/10/2025).
- `[ÉTABLI]` Rien n'est entraîné chez nous cette année (R61 ; C1, C4).

## Décision

1. **Un processus est une définition versionnée d'étapes**, dans la sémantique d'un sous-ensemble de BPMN 2.0. Sa forme de
   référence est notre propre modèle, en données ; le XML de BPMN 2.0 sert à l'import et à l'export. L'interface montre et
   édite le processus en mots, jamais avec la notation de BPMN.
2. **Il s'attache à un projet** : ses étapes de haut niveau (des colonnes de la vue) et ses portes. Une étape peut porter une
   issue ; une étape d'agent confie cette issue à un agent, et la mission garde à l'intérieur son déroulé en cinq étapes (R138).
3. **Cinq types d'étapes, pas de sixième avant qu'E20 en exige un** :

   | Type | BPMN 2.0 | Ce qu'il porte |
   | --- | --- | --- |
   | L'étape d'agent | `serviceTask` | l'agent, son modèle, ses outils permis, les règles qui s'appliquent, la personne qui en répond |
   | La tâche humaine | `userTask` | la personne ou le rôle, la question ; un accord, une saisie typée, une liste de contrôle de moins de dix lignes, une signature avec sa signification (revue, approbation, responsabilité, rédaction) |
   | La décision | `exclusiveGateway`, avec des flux conditionnels et un flux par défaut | une condition écrite comme une règle en mots, jugée par du code, jamais par un modèle |
   | L'attente | `intermediateCatchEvent` (minuterie, message) ; au besoin `eventBasedGateway` | ce qu'elle attend (une durée, un document fourni, une réponse, un autre processus fini) et qui doit le fournir |
   | La zone d'agent | `adHocSubProcess` | ce que l'agent peut faire dans l'ordre qu'il choisit, borné par les règles |

   La structure n'est pas un type : le début et la fin (`startEvent`, `endEvent`, dont l'arrêt de tout le processus), le
   partage et la jonction en parallèle (`parallelGateway`), les étapes de haut niveau (`subProcess` intégré), l'échéance d'une
   étape (minuterie de bordure) et le chemin d'un échec (erreur de bordure). L'incident, la liste d'attente et le manque ne sont
   pas des types : ce sont des états et des objets de l'exécution (ADR-023).
4. **Le sous-ensemble est une liste écrite**, prise surtout dans la sous-classe « Common Executable » de BPMN 2.0.2, plus la zone
   ad hoc et la minuterie de bordure, sans revendiquer la conformité de la sous-classe. Le sous-ensemble de J2 se fige sur ce
   qu'exige le processus d'E20 ; le reste suit la table de R165 (la compensation et l'appel d'un autre processus en J5).
   Hors du sous-ensemble : la passerelle inclusive et la complexe, le multi-instance, les sous-processus d'événement, la
   transaction, les signaux, l'escalade, les objets de données, les couloirs et les flux de message, la tâche de règle métier
   (DMN). Un élément hors du sous-ensemble est refusé à l'import, avec sa raison en mots.
5. **Ce que BPMN ne porte pas voyage dans une extension `tf:`**, documentée et publiée avec le code : qui répond de l'étape,
   l'agent et son modèle, les règles et leurs versions, le verrou et sa source, la signification d'une signature, la liste de
   contrôle, les documents attendus, l'issue portée. Un modeleur qui l'ignore garde le processus lisible ; l'aller et retour la
   garde (E23).
6. **Un seul vérificateur, en code**, pour tout ce qui entre : l'import, le brouillon de l'IA, l'éditeur, la publication. Il
   vérifie le sous-ensemble, qu'aucune étape ne reste sans personne qui en réponde, que chaque étape d'agent ait sa zone et ses
   règles, que les étapes verrouillées et les points de pause soient là, que chaque décision ait sa condition jugée par du code,
   que chaque attente dise ce qu'elle attend, et que toute étape mène à une fin. Ses refus sont des phrases.
7. **Des versions immuables**, comme les règles (V125) : chaque publication est une version, avec son auteur et son empreinte,
   calculée sur notre modèle et non sur le texte du XML. Une instance tourne sur sa version ; une nouvelle étape fait une nouvelle
   version ; une instance ne change de version qu'avec une raison écrite et approuvée (J5).
8. **Définir, exécuter, exploiter sont séparés** dans les données : la définition et ses versions ; l'instance, son état et son
   journal (ADR-023) ; les incidents, les attentes, les manques et les gestes. À l'écran, deux modes : « Run », par défaut, où
   l'on suit et où l'on agit sur l'instance, et « Edit », à part, qui ne change rien de ce qui tourne et publie une version.
9. **Des workflows par défaut, un par nature de travail** (R103) : la livraison logicielle d'abord, « intégrer un module » pour
   E20 ; la rédaction et la revue d'un document ; le traitement de demandes. Chacun porte ses étapes verrouillées, dont les points
   de pause de TF-J2-10 (avant une mission, avant d'appliquer, avant de livrer). Une personne en dérive un workflow à elle, y
   ajoute ses étapes ou ses blocs (l'exemple du LIMS : IQ, OQ, PQ, les documents de GAMP, une revue au titre de 21 CFR Part 11),
   les verrouille, et le publie.
10. **L'IA propose, une personne décide, le moteur exécute** (R169). Un agent propose un brouillon avec des conventions écrites,
    des exemples, le sous-ensemble donné comme schéma de sortie, et le vérificateur ; la banque d'évaluations mesure chaque
    modèle. Ce qui est de trop, l'IA le juge au brouillon seulement : elle n'écarte qu'une étape optionnelle, dit pourquoi, et la
    personne garde ou accepte ; une étape verrouillée ne s'écarte jamais ; à l'exécution, seule une personne passe une étape non
    verrouillée, avec une raison, au dossier. Dans un workflow marqué régulé, l'IA n'écarte rien.
11. **Pas orienté full code** : personne n'écrit de code, d'expression ni de XML. Une condition est une règle en mots, compilée et
    vérifiée par ses cas (TF-J2-4) ; l'ingénieur règle les détails dans des champs typés ; le XML est un format d'échange.

## Alternatives considérées

| Alternative | Pourquoi écartée |
| --- | --- |
| BPMN complet, comme Camunda | Un second produit ; des éléments que le processus d'E20 n'exige pas ; une notation que la Présidence refuse à l'écran |
| Une liste d'étapes en mots, sans BPMN (Musk, séance n°24) | Ni sémantique d'exécution écrite, ni échange avec d'autres outils, ni pont vers Camunda plus tard (Q18) ; reste possible comme point de départ d'un brouillon |
| Des processus écrits en code, comme Temporal | Contraire à « pas orienté full code » ; seuls les développeurs les liraient |
| L'éditeur bpmn-js | Son filigrane ne se retire ni ne se masque, et il dessine la notation que la vue refuse (séance n°24) |
| Les tables de décision DMN | Les règles en mots en tiennent lieu (R165) ; un import si un client en a |

## Conséquences

- **Positives**
  - Un processus s'exécute comme il se lit, se vérifie avant d'exister, s'exporte et s'importe.
  - L'ordre des étapes devient une propriété du moteur, ce que 21 CFR 11.10(f) demande d'un système, sans rien revendiquer
    (R168).
  - La même version, le même vérificateur et le même dossier pour une personne, un agent et l'import.
- **Négatives**
  - Un sous-ensemble, une extension et un vérificateur à tenir ; l'aller et retour à essayer à chaque version (E23).
  - Rendre simple un modèle précis coûte en interface : c'est le travail de la spécification d'UX de la séance n°25.
- **À surveiller** : le processus d'E20 qui exige un élément de plus (le signal d'arrêt de R165) ; une étape verrouillée écartée
  dans un brouillon montré à une personne.

## Plan de déploiement

- **J2** : le modèle, le vérificateur, l'import et l'export, et le processus d'E20 écrit (W2) ; le brouillon de l'IA et le premier
  workflow par défaut (W4).
- **Après J2** : l'édition complète et les workflows des utilisateurs (W6) ; la modification et la migration des instances, la
  compensation, l'appel d'un autre processus (W7, J5) ; l'import des processus de Camunda (W8, Q18).

## Liens

- [PV de la séance n°24](../conseil/seances/2026-11-13-depasser-camunda.md), R165, R169 et la décision de la Présidence
- [PV de la séance n°25](../conseil/seances/2026-11-13-le-workflow-pilotable.md), R174 à R176
- [ADR-023](./ADR-023-DRAFT-execution-durable-postgresql.md), le moteur
- [ADR-022](./ADR-022-DRAFT-infrastructure-pas-les-regles.md), les huit briques
- [ADR-025](./ADR-025-DRAFT-un-seul-moteur-de-regles.md), le moteur de règles

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 13/11/2026 · **v0.1** · Projet Taskforce
