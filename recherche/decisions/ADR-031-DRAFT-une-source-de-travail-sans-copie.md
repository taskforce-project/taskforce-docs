---
id: adr-031-une-source-de-travail-sans-copie
title: "ADR-031 (brouillon) : une source de travail sans copie, un instantané, deux événements, un état en retour"
doc_type: adr
statut: proposed
version: 0.1
date: "22/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, integrations, mcp, webhooks, dossier, conseil]
related:
  - "../conseil/seances/2026-11-17-finir-la-v1.md"
  - "../conseil/seances/2026-11-17-preciser-avant-de-trancher.md"
  - "../conseil/seances/2026-11-17-le-recentrage.md"
  - "./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md"
  - "./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md"
  - "./ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
  - "./ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../experiences/Experiences.md"
  - "../Questions-ouvertes.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-031 (brouillon) : une source de travail sans copie, un instantané, deux événements, un état en retour

> **Brouillon, `DRAFT`, sans autorité avant sa promotion** ([Gabarits](../Gabarits.md) §6). Il naît de R209 (séance n°30).
> Cette recommandation est **retenue le 22/11/2026 par délégation de la Présidence au Conseil, selon l'avis de sa majorité** :
> « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est partie ». C'est le contrat d'une
> source qui est retenu ; son écriture, ci-dessous, reste une proposition du secrétariat, à relire par la Présidence. Il
> complète le projet [ADR-029](./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md) (la couche : le travail vient d'où
> il est) et dépend du projet [ADR-030](./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md) (la classe d'une écriture
> externe) pour l'état écrit chez un hôte. Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 031 après sa
> ratification.

## Statut

Proposé le 17/11/2026 ; état de la décision inscrit le 22/11/2026. `DRAFT`, pas promu. En v1, aucune source externe ne se
construit : seule la ligne Claude Code existe, par le serveur MCP et le plugin qui existent. Le contrat s'applique à la
première vraie source externe, après le premier client test : GitHub, puis Linear.

## Contexte

- `[ÉTABLI]` La Présidence, sur R199 (saisine de la séance n°30) : « Les integrations oui mais comment ? On allimente notre
  vue avec ? Ca foncitonne pas ca, trop lourd, trop de requete ».
- `[ÉTABLI]` Dans la copie du code de `dev` (lue le 17/11/2026) : aucun webhook entrant ; sur l'app de bureau, l'état d'une
  pull request se relit toutes les cinq minutes (`core/desktop/DesktopPullRequestWatch.java`) ; les connecteurs lisent à la
  demande ; aucune synchronisation continue ; les webhooks sortants émettent cinq types d'événements, aucun de mission.
- `[ÉTABLI]` TaskForce expose un serveur MCP de dix-sept outils, dont créer et déléguer une issue : un agent extérieur peut
  pousser une demande vers TaskForce ([ADR-024](./ADR-024-DRAFT-mcp-taskforce-surface-unique.md)).
- `[ÉTABLI]` Ce que l'agent reçoit est un brief de six champs (`AgentBrief.java`) ; il n'entre pas au dossier (TF-J2-7).
- `[ÉTABLI]` Le socle classe toute écriture externe (`mcp.write`) à sens unique : écrire un état chez un hôte demande
  aujourd'hui une carte à chaque fois.
- `[ÉTABLI]` « R199, amendée » (n°29) : demander et décider pendant la mission appartiennent à TaskForce ; l'état se lit chez
  l'hôte ; un seul lieu pour juger par sorte de mission ; chaque source a son contrat écrit.

## Décision

Les sept points sont le contrat que R209 écrit et que la délégation du 22/11/2026 retient. Leur mise en mots est celle du
secrétariat.

1. **Aucune vue alimentée.** TaskForce n'affiche pas la liste du travail d'un autre outil et ne relit aucun outil pour y
   chercher du travail. La demande lui est poussée, par une personne ou par un agent.
2. **Un instantané au départ.** La demande est lue une fois ; TaskForce garde son titre, son texte, son auteur, sa
   référence d'origine et son adresse, sa date et son empreinte. C'est un contenu non fiable : une personne le lit, et
   l'accepte, avant qu'il devienne le brief ; la garde « jamais les trois à la fois » s'y applique. Un contenu sensible
   entre par son empreinte ; son texte reste effaçable.
3. **Rien pendant la mission.** TaskForce ne lit rien de la source.
4. **Deux événements reçus, pas plus** : la pull request fusionnée ou fermée ; la décision de revue. Sur un serveur
   installé, par un webhook entrant signé. Sur l'app de bureau, qu'on ne peut pas appeler de dehors, par la relecture
   espacée qui existe. Un troisième événement ne s'ajoute que par une décision écrite, source par source.
5. **Un état en retour.** Les changements d'état d'une mission (partie, attend quelqu'un, remise, finie) sortent par les
   webhooks sortants, que tout outil peut écouter. Chez l'hôte d'où vient la demande, TaskForce écrit un état et un lien,
   jamais la carte d'accord ; cette écriture suit la classe qu'ADR-030 lui donne : une carte par défaut.
6. **Un contrat par source**, écrit avant qu'elle existe : ce qui est lu, reçu, écrit, gardé, où vit chacun des trois moments
   (demander, décider pendant la mission, juger le résultat), et ce qui se passe quand la source change, disparaît ou ne
   répond plus. Dans ce cas, la mission continue sur le brief accepté.
7. **Aucune copie tenue à jour.** Le dossier garde l'instantané, devenu le brief accepté, et la décision de revue ; rien
   d'autre de la source.

Ce que TaskForce garde de la gestion du travail, les onze choses de R209, est écrit dans le projet ADR-029 (amendement de la
n°30) : la référence d'origine en est la ligne 7.

## État de la décision au 22/11/2026

**La décision.** Après la séance n°30, la Présidence, à qui le secrétariat avait remonté les dix-huit points à trancher avec
l'avis de la majorité, répond : « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est
partie ». La Présidence délègue : les points sont tranchés selon l'avis de la majorité du Conseil, tel que le
[PV n°30](../conseil/seances/2026-11-17-finir-la-v1.md) l'écrit (« La liste à trancher pour finir la v1 »). Pour ce projet :

- R209 est retenue par délégation de la Présidence au Conseil, selon l'avis de sa majorité ;
- point 4, le contrat d'une source : oui (un instantané, deux événements, un état en retour, aucune copie ; onze choses
  gardées de la gestion du travail) ;
- point 3, demander ailleurs en v1 : Claude Code seulement, par le serveur MCP et le plugin qui existent ; la première vraie
  source externe après le premier client test, GitHub puis Linear ;
- point 6 : hors de TaskForce, les écritures changent de classe outil par outil, après la v1 (ADR-030, E33).

**Précisions du secrétariat.**

- Ce qui se construit en v1 : le brief accepté au dossier, avec TF-J2-7. La ligne Claude Code tient par ce qui existe, et son
  contrat s'écrit au labo. Ni instantané d'une source externe, ni webhook entrant, ni état écrit chez un hôte.
- Ce qui vient après la v1 : la référence d'origine et l'instantané pour la première source, GitHub ; les événements de
  mission dans les webhooks sortants ; le webhook entrant signé sur un serveur installé ; puis Linear.
- L'ordre du plan de déploiement, plus bas, est une proposition du secrétariat : la délégation retient le contrat, pas un
  calendrier.
- Le projet lui-même n'est pas ratifié : les Suites du PV n°30 le donnent « à relire par la Présidence ». Rien ne va dans
  `v1/12-decisions/` avant cette relecture.
- Réserves conservées au PV : Musk (huit choses gardées, pas onze) ; Rus, contradictrice (« deux événements, pas plus » tient
  jusqu'au premier client qui en demande un troisième).

## Alternatives considérées

- **Une copie miroir synchronisée** : écartée. C'est ce que la saisine refuse (« trop lourd, trop de requete »), et c'est
  refaire un outil de suivi.
- **Tout par webhooks entrants** : impossible sur l'app de bureau, qu'on ne peut pas appeler de dehors.
- **Rien d'externe** : c'est le cas en v1 pour tout sauf Claude Code. Écartée au-delà : la n°28 établit qu'une couche ne
  dépend pas d'une seule source de travail.
- **Afficher la carte d'accord chez l'hôte** : écartée par « R199, amendée » (ADR-029).

## Conséquences

- Une référence d'origine s'ajoute à l'issue ; le brief accepté entre au dossier (TF-J2-7).
- Des événements de mission s'ajoutent aux webhooks sortants.
- Un point d'entrée de webhook signé devient nécessaire sur un serveur installé, après la v1.
- L'état chez un hôte reste soumis à une carte tant qu'ADR-030 n'est pas construit et qu'une personne n'a pas déclaré ce
  geste.
- Ce qu'on ne saura pas : ce qui change dans la source après l'instantané. C'est voulu, et le contrat le dit.

## La preuve

- E35 (demander depuis Claude Code, avec ce qui existe) et E32 (ce qui dépend de l'issue interne), sans code du produit
  ([Expériences](../experiences/Experiences.md)). E33 pour l'état écrit chez un hôte, avec ADR-030.
- Signal d'arrêt : une table qui recopie les issues d'un hôte ; une relecture périodique d'un outil pour y chercher du
  travail ; un instantané devenu brief sans qu'une personne l'ait lu.

## Plan de déploiement

Proposition du secrétariat, dans l'ordre.

- **Maintenant, au labo, sans code du produit** : E35 et E32 ; le contrat écrit de la ligne Claude Code.
- **En v1** : le brief accepté au dossier, avec TF-J2-7.
- **Après le premier client test** : la référence d'origine et l'instantané ; les événements de mission sortants ; la première
  source externe, GitHub, et son webhook entrant sur un serveur installé ; puis Linear.
- **Avec ADR-030** : l'état écrit chez l'hôte sans carte, pour le geste qu'une personne aura déclaré.

## Questions à la Présidence

Le secrétariat ne répond pas à sa place.

1. **La relecture.** Ce contrat répond-il à « On allimente notre vue avec ? » comme la Présidence l'entend ? Une ligne suffit
   pour le corriger ou le retirer.
2. **Le troisième événement.** Le contrat dit qu'il ne s'ajoute que par une décision écrite, source par source. Qui la prend :
   la Présidence, ou le Conseil sur saisine ?
3. **L'instantané et les personnes.** Il garde un auteur et un texte venus d'ailleurs. Combien de temps, et qui peut demander
   l'effacement du texte, l'empreinte restant au dossier ?

## Liens

- [Séance n°30](../conseil/seances/2026-11-17-finir-la-v1.md), R208 et R209, les pièces 1 à 3, la liste à trancher (points 3,
  4 et 6) et la décision de la Présidence
- [Séance n°29](../conseil/seances/2026-11-17-preciser-avant-de-trancher.md), « R199, amendée » et « R201, amendée »
- [Séance n°28](../conseil/seances/2026-11-17-le-recentrage.md), R199
- [ADR-029](./ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md), la couche : ce projet en écrit le contrat d'une source
- [ADR-030](./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md), la classe d'une écriture externe : l'état écrit chez un hôte
  en dépend
- [ADR-024](./ADR-024-DRAFT-mcp-taskforce-surface-unique.md), le MCP TaskForce, par où la demande arrive
- [ADR-028](./ADR-028-DRAFT-execution-isolee-par-defaut.md), l'exécution isolée par défaut
- [Expériences](../experiences/Experiences.md), E32, E33 et E35
- [Questions ouvertes](../Questions-ouvertes.md), Q31 (le témoin dans la pull request) et Q33 (la classe d'une écriture
  externe)

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 22/11/2026 · **v0.1** · Projet Taskforce
