---
id: adr-023-execution-durable-postgresql
title: "ADR-023 (à promouvoir) : l'exécution durable sur PostgreSQL, sur le modèle de Temporal"
doc_type: adr
statut: active
version: 1.0
date: "01/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, execution-durable, temporal, postgresql, fiabilite, conseil]
related:
  - "../conseil/seances/2026-11-01-feuille-de-route.md"
  - "../../v1/road_to_v2/Specification_V2_Harnais.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-023 (à promouvoir) : l'exécution durable sur PostgreSQL, sur le modèle de Temporal

> **Ratifié par la Présidence le 01/11/2026** (séance n°15 du Conseil : R97 retenue). Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 023 dès que
> l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 01/11/2026. La version 1 se mesure en J2 (l'abstention de Musk : un moteur maison doit prouver qu'il vaut
mieux que Temporal).

## Contexte

- `[ÉTABLI]` Les missions passent par une file en base, sans moteur durable ni reprise. Les événements du runner vivent
  en mémoire. Une mission perdue n'est déclarée que quand quelqu'un ouvre l'issue (séance n°14, Hamilton).
- `[ÉTABLI]` La feuille de route fait des processus (des étapes d'agents, de décisions humaines et d'outils) le cœur de
  la démo : ils doivent survivre à une coupure, à une mise en veille, à un redémarrage.
- `[ÉTABLI]` Temporal : son moteur d'exécution durable est sous licence MIT, gratuit à auto-héberger, avec un SDK Java
  natif ([Temporal](https://temporal.io/llm-info)). Il demande son propre serveur et sa propre base.
- `[ÉTABLI]` L'app desktop embarque déjà PostgreSQL, le backend Java, l'interface et le runner sur la machine de la
  personne (`desktop/README.md`).
- `[ÉTABLI]` La Présidence, le 01/11/2026 : « on pourrait copier Temporal si jamais ».

## Décision

On copie le modèle de Temporal, pas son serveur : un moteur d'exécution durable en Java, dans le backend, sur la base
PostgreSQL qui existe déjà.

1. **Un journal d'événements par exécution de processus.** Après une panne, la logique du processus se rejoue sur le
   journal et reprend où elle s'était arrêtée ; rien n'est fait deux fois.
2. **Des étapes avec délais, reprises et clé d'idempotence.** Un appel d'agent, de modèle ou d'outil est une étape.
3. **Des minuteries et des signaux.** Un accord humain est un signal ; une attente est une minuterie.
4. **Des baux, et la reprise des exécutions perdues par le serveur** (spécification de la v2, §13.2).
5. **Les priorités, et ce que le système lâche d'abord quand il sature**, écrits avant (Hamilton).
6. **Les événements du runner écrits sur disque d'abord**, puis renvoyés après une coupure.
7. **Temporal reste possible pour un grand serveur** : la logique des processus ne dépend pas du stockage du journal.

## Alternatives considérées

| Alternative | Pourquoi écartée |
| --- | --- |
| Embarquer le serveur de Temporal | Un serveur de plus et sa base, sur chaque machine de l'app desktop |
| Garder la file en base | Ni reprise, ni minuterie, ni signal : les missions se perdent (séance n°14) |
| Une bibliothèque d'exécution durable existante sur PostgreSQL | À évaluer en J2, face au moteur maison, sur les mêmes essais de coupure |

## Conséquences

- **Positives**
  - Un processus ne se perd plus, et le dossier dit chaque coupure et chaque reprise.
  - Les accords humains deviennent des signaux durables : une décision attendue survit à un redémarrage.
- **Négatives**
  - Un moteur à tenir : il se teste par des coupures provoquées à chaque jalon.
  - La logique d'un processus doit rester déterministe ; tout ce qui touche au monde passe par une étape.
- **À surveiller** : une mission perdue découverte par une personne (le signal d'arrêt de R97).

## Plan de déploiement

- **J2** : la version 1 (le journal, la reprise, les accords en signaux), mesurée par des coupures provoquées ; la
  comparaison avec une bibliothèque existante.
- **J5** : les délais, les reprises, les minuteries, les baux, la reprise des missions perdues, les priorités et le
  délestage ; les événements du runner sur disque.

## Liens

- [PV de la séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md), R97
- [PV de la séance n°14](../conseil/seances/2026-10-31-souverainete-operationnelle.md), l'intervention de Hamilton
- [Spécification de la v2](../../v1/road_to_v2/Specification_V2_Harnais.md), §13.2
