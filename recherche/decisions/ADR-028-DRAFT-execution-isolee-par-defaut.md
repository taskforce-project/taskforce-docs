---
id: adr-028-execution-isolee-par-defaut
title: "ADR-028 (brouillon) : l'exécution isolée par défaut, une interface de bac à sable dans le runner et un moteur par système"
doc_type: adr
statut: proposed
version: 0.1
date: "16/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, runner, isolement, bac-a-sable, execution, conseil]
related:
  - "../conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md"
  - "../conseil/seances/2026-11-13-le-workflow-pilotable-plan-des-lots.md"
  - "./ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "./ADR-025-DRAFT-un-seul-moteur-de-regles.md"
  - "../experiences/Experiences.md"
  - "../Questions-ouvertes.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-028 (brouillon) : l'exécution isolée par défaut, une interface de bac à sable dans le runner et un moteur par système

> **Brouillon, `DRAFT`, sans autorité avant sa promotion** ([Gabarits](../Gabarits.md) §6). Il naît de R189 (séance n°27),
> retenue et amendée par la Présidence le 16/11/2026 : l'isolement est par défaut, partout, quel que soit l'agent. C'est la
> seule part décidée. La façon de le faire, ci-dessous, est une proposition du secrétariat, du même jour, qu'E27 doit prouver.
> Il entre dans [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 028
> après sa ratification.

## Statut

Proposé le 16/11/2026, `DRAFT`. Rien ne se construit avant E27. Pas dans J2 : après J2, avec le bac à sable du test à blanc (le
lot W6 de la séance n°25).

## Contexte

- `[ÉTABLI]` Le runner fait travailler Claude Code dans un worktree, sous un hook qui juge les règles avant chaque action, garde
  fermée ; il garde pour lui les sorties (les tests, le push, la pull request). Il n'a ni conteneur ni bac à sable du système.
  Le worktree isole la branche, pas les fichiers ni le réseau de la personne (dossier de la
  [séance n°27](../conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), 15/11/2026).
- `[ÉTABLI]` R189 proposait trois niveaux d'isolement, « détecté, jamais exigé », le conteneur en option, par défaut pour les
  seuls dépôts venus du dehors. LeCun, contradicteur, a maintenu son non au second tour : par défaut pour tout dépôt.
- `[ÉTABLI]` La Présidence, le 16/11/2026, suit LeCun : « tout ce qui releve de l'execution, des runs, des bac a sable et ainsi
  de suite, serait en environnement isole via un container ou une autre technologie. Et ca devrait etre le cas partout je pense.
  Ca devrait etre active par defaut effectivement. »
- `[ÉTABLI]` Elle pose la question que R189 laissait de côté : « comment on fait pour le bac a sable si la personne n'utilise
  pas Claude code ? Imaginons qu'elle utilise "Juste" qwen4 en 27B par exemple, pour tout faire genre elle a vraiment que ca. »
- `[ÉTABLI]` Ses contraintes : pas de cloud payant (« Le cloud est payant, c'est une solution mais c'est payant et pour
  l'instant je peux pas me le permettre. ») ; Docker lui semble pertinent, sans l'imposer (« Docker me semble pertinent mais
  c'est pace que je l'utilise quoi ») ; un bac à sable fait maison seulement s'il le faut (« faut juste que ce soit pertinent,
  qu'on ai un objectif clair et pertinent pour les clients ») ; « Mais faut que ce soit scalable et robuste, donc faut proposer
  des choses. En etant realiste aussi ».
- `[ÉTABLI]` Les briques des systèmes (dossier de la séance n°27, point 9) :
  - le bac à sable de Claude Code borne l'écriture au projet et le réseau à une liste de domaines, par Seatbelt sous macOS et
    par bubblewrap sous Linux et WSL2 ; rien sous Windows natif ;
  - Hyper-V manque à Windows Famille ; WSL2 demande les droits d'administrateur au premier lancement, et une entreprise peut le
    fermer ;
  - Docker Desktop est payant au-delà de 250 salariés ou de 10 M$ de chiffre d'affaires ; Podman est ouvert et passe par WSL2
    sous Windows ;
  - le GPU ne traverse un conteneur qu'avec une carte NVIDIA sous WSL2.
- `[ÉTABLI]` Deux dépôts ouverts le 16/11/2026, à relire en entier avant E27 : le moteur de bac à sable de Claude Code est
  publié à part, sous Apache 2.0, en préversion de recherche, et borne des processus quelconques sans conteneur
  ([Sandbox Runtime](https://github.com/anthropic-experimental/sandbox-runtime)) ; le framework Containerization d'Apple fait
  tourner des conteneurs Linux sous macOS, sous Apache 2.0 ([Apple](https://github.com/apple/containerization)).
- `[ÉTABLI]` Le test à blanc de W6 (décision de la Présidence du 15/11/2026) demande déjà un bac à sable : jouer un workflow
  sans aucun effet au dehors.

## Décision

Le point 1 est la décision de la Présidence. Les points 2 à 8 sont la proposition du secrétariat.

1. **Tout ce qui s'exécute pour une mission tourne isolé, par défaut, partout, quel que soit l'agent** : les commandes, les
   écritures de fichiers, les tests, les runs, le bac à sable du test à blanc.
2. **L'isolement vit dans le runner, pas dans l'agent.** Le runner offre une seule interface de bac à sable : lancer une
   commande dans un périmètre, l'écriture bornée au worktree, le réseau borné à une liste (TaskForce, le hook du runner, le
   fournisseur du modèle).
3. **Deux entrées, la même interface** :
   - avec un modèle local seul, ce sont les outils de TaskForce (shell, fichiers, tests) qui s'exécutent dans le bac à sable ;
   - avec Claude Code, le runner le lance lui-même dans le bac à sable.
4. **Un moteur par système**, choisi par le runner selon la machine :

   | Système | Moteur | Ce qui reste à prouver (E27) |
   | --- | --- | --- |
   | Linux | bubblewrap | le hook des règles joint depuis le bac à sable |
   | macOS | Seatbelt ; une machine virtuelle Linux légère (Containerization) pour les tests qui exigent Linux | l'app desktop n'existe pas encore sous macOS (Q16) |
   | Windows | une distribution WSL2 dédiée à TaskForce | les droits d'administrateur au premier lancement ; WSL fermé par une entreprise |
   | Tous | Docker ou Podman, seulement s'ils sont déjà installés | le surcoût, mesuré à part |

5. **Le modèle reste hors du bac à sable, avec le GPU.** Le bac à sable le joint par le réseau, sur la liste.
6. **Les règles ne changent pas.** Le hook reste, chaque action est jugée, chaque sortie reste au runner et reste jugée. Aucun
   isolement ne sert à relâcher une règle, et aucun mode sans permissions n'existe parce que « c'est isolé » (R189).
7. **Le bac à sable du test à blanc est le même** (W6, R195) : une exécution sans effet au dehors.
8. **Pas de bac à sable écrit en C par TaskForce.** Les noyaux fournissent les briques, et un moteur ouvert existe. Quand un
   conteneur sert, son image se construit depuis la fiche d'environnement du projet (TF-J2-9) : TaskForce ne tient aucune image
   pour un client (R189).

**À trancher par la Présidence** : ce que fait une mission quand la machine n'offre aucun moteur. R189 disait qu'elle le dit
avant de partir. Avec l'isolement par défaut, deux lectures : elle ne part pas ; ou elle part sans isolement, après un accord
qui le dit en mots.

## Alternatives considérées

| Alternative | Pourquoi écartée |
| --- | --- |
| Docker obligatoire | Un prérequis de plus à installer et à tenir ; Docker Desktop payant au-delà de 250 salariés ou de 10 M$ ; sans Hyper-V sous Windows Famille, il passe par WSL2 de toute façon ; le GPU ne traverse un conteneur qu'avec une carte NVIDIA sous WSL2. Il reste un moteur accepté, s'il est déjà installé |
| Un bac à sable écrit en C par TaskForce | Les noyaux fournissent déjà les briques ; un moteur ouvert existe ; un bac à sable maison est un produit de sécurité de plus à tenir par une personne (C1). La Présidence y est prête si c'est pertinent : ce ne l'est pas tant qu'E27 tient |
| Le cloud par défaut | Payant, ce que la Présidence écarte pour l'instant ; contraire à « tout tourne sur votre machine » (R62). Il reste une option pour qui le veut, après le client test (R189) |
| L'isolement en option, par défaut pour les seuls dépôts venus du dehors (R189, second tour) | Écartée par la Présidence, avec LeCun : une option que personne n'active ne protège personne |
| S'en remettre au bac à sable de l'agent | Il n'existe que pour Claude Code, et pas sous Windows natif ; un modèle local seul n'en a pas |

## Conséquences

- **Positives**
  - Un dépôt piégé ne lit pas les fichiers de la personne et ne joint pas un domaine hors de la liste, quel que soit l'agent.
  - La même interface sert le run et le test à blanc de W6.
  - Aucun prérequis payant, et aucun cloud : le modèle garde le GPU de la machine.
- **Négatives**
  - Trois moteurs à tenir et à essayer, un par système, et un surcoût à chaque mission.
  - Sous Windows, WSL2 devient une dépendance de l'isolement : des droits d'administrateur une fois, et des entreprises qui le
    ferment.
  - Le moteur ouvert cité est une préversion de recherche, dont les interfaces peuvent changer.
- **À surveiller** (les signaux d'arrêt de R189) : un run isolé qui ne joint plus le hook des règles ; des identifiants de
  Claude Code à copier en clair dans le bac à sable ; un surcoût de plus de la moitié de la durée d'une mission.

## La preuve

E27 ([Expériences](../experiences/Experiences.md)), amendée par R189 : une même mission, avec et sans bac à sable, pour chaque
sorte d'agent, sous Windows, macOS et Linux ; une attaque plantée ; le surcoût mesuré. Si elle échoue sur un système, ce
brouillon se réécrit pour lui, et l'isolement ne s'y promet pas.

## Plan de déploiement

- **Au labo, sans rien prendre à J2** : E27, d'abord sur la machine de la Présidence (Windows 11 Famille, WSL2).
- **Après J2** : l'interface dans le runner et le premier moteur, avec le bac à sable du test à blanc (W6) ; puis les autres
  systèmes.
- **Avant toute annonce** : rien sur l'isolement dans le pitch avant sa preuve (R195).

## Liens

- [PV de la séance n°27](../conseil/seances/2026-11-15-le-run-et-les-petits-modeles.md), R189 et la décision de la Présidence
- [Plan des lots](../conseil/seances/2026-11-13-le-workflow-pilotable-plan-des-lots.md), W6
- [Questions ouvertes](../Questions-ouvertes.md), Q25 (l'isolement sous Windows natif) et Q16 (macOS)
- [ADR-022](./ADR-022-DRAFT-infrastructure-pas-les-regles.md), l'infrastructure, pas les règles
- [ADR-025](./ADR-025-DRAFT-un-seul-moteur-de-regles.md), le moteur de règles

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 16/11/2026 · **v0.1** · Projet Taskforce
