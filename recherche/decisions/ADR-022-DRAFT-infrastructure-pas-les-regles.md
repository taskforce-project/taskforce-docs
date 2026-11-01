---
id: adr-022-infrastructure-pas-les-regles
title: "ADR-022 (à promouvoir) : l'infrastructure, pas les règles. Le métamodèle et les packs"
doc_type: adr
statut: active
version: 1.0
date: "01/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, positionnement, metamodele, packs, metier, souverainete, conseil]
related:
  - "../conseil/seances/2026-11-01-feuille-de-route.md"
  - "../conseil/seances/2026-10-31-souverainete-operationnelle.md"
  - "../conseil/seances/2026-10-27-vision.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-022 (à promouvoir) : l'infrastructure, pas les règles. Le métamodèle et les packs

> **Ratifié par la Présidence le 01/11/2026** (séance n°15 du Conseil : R94 retenue, R103 retenue et modifiée). Il entre
> dans [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 022 dès
> que l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 01/11/2026. Remplace les niches A et B de la [séance n°2](../conseil/seances/2026-10-27-vision.md).

## Contexte

- `[ÉTABLI]` La séance n°2 (27/10/2026) visait la niche A (les équipes logicielles qui délèguent à des agents), puis la
  niche B (les industries régulées où le logiciel est le produit). La séance n°14 a ajouté que la pharmacie n'est pas le
  premier terrain (R85).
- `[ÉTABLI]` Un métier ne peut presque rien configurer aujourd'hui :
  - les objets sont fixes (projets, issues, cycles) ;
  - les 35 règles ne se modifient pas, la table par espace (V102) n'est jamais écrite ;
  - aucun processus ne se dessine, aucun vocabulaire ne se change.
- `[ÉTABLI]` La Présidence, le 01/11/2026 :
  - « nous on creer l'infra, pas les regles en elles mm » ;
  - « moi je connais pas les metiers, mais les metiers le connaissent mieux que n'importe qui, donc c'est a eux de
    construire l'outil » ;
  - « Je suis d'accord avec Zhuo, mais je n'ai pas la pretention de faire un produit pour tout les metiers pour le moment ».

## Décision

1. **TaskForce fournit un métamodèle**, huit briques que le métier assemble sans code :
   1. le profil de l'espace (la grille de variables : confidentialité, criticité, autonomie, hébergement,
      conservation...), qui règle les valeurs par défaut et se voit dans chaque décision ;
   2. le vocabulaire (le métier renomme les objets, dans l'interface et dans les consignes des agents) ;
   3. les types d'objets du métier, avec leurs champs et leurs états ;
   4. les règles, éditées en mots, avec un responsable, une raison, une date de revue et des cas d'essai ;
   5. les processus, sur un canevas modifiable ;
   6. les agents : un rôle, des consignes, des outils permis, un modèle, un palier d'autonomie ;
   7. les évaluations, qui disent ce qu'est un bon résultat dans ce métier ;
   8. les packs : la configuration entière en un fichier versionné, au format ouvert, sans les données.
2. **Chaque brique a un responsable nommé.** Personne ne part d'une page blanche : le parcours d'arrivée et les packs de
   démonstration donnent un départ.
3. **Aucune ligne de code propre à un métier**, vérifié par un contrôle de la CI.
4. **La généralité se montre sur trois natures de travail** : la livraison logicielle, la rédaction et la revue de
   document, le traitement de demandes. Ce n'est pas un produit pour tous les métiers pour le moment.
5. **Les besoins propres à un secteur viennent des clients**, et deviennent des packs. Aucun secteur n'est visé d'abord ;
   aucun n'est exclu.

## Alternatives considérées

| Alternative | Pourquoi écartée |
| --- | --- |
| Choisir un secteur d'abord (niche B, ou la pharmacie) | Il faudrait apprendre le métier avant de construire : « sinon jamais j'aurais fini de discuter avec les gens pour apprendre leur metier » (Présidence) |
| Un produit pour tous les métiers, tout de suite | « pas la pretention » (Présidence) ; le plus difficile à rendre bon (Zhuo, Saarinen) |
| Des packs écrits par TaskForce pour chaque métier | Ce serait écrire les règles des autres : l'inverse de la décision |

## Conséquences

- **Positives**
  - TaskForce s'étend sans connaître les métiers : le métier écrit ses règles, TaskForce fournit le moteur et la preuve.
  - Les packs rendent la configuration portable et propriété du client (R64).
- **Négatives**
  - Un outil qui sait tout configurer est le plus difficile à rendre simple : il exige le parcours d'arrivée (R102), des
    réglages par défaut tranchés et une seule grammaire d'interface (R95).
  - Le contrôle « zéro code par pack » doit tenir à chaque pack ajouté.
- **À surveiller** : un métier qui a besoin de code pour exprimer une règle ou un processus courant (le signal d'arrêt
  de R94).

## Plan de déploiement

- **J2** : les règles éditables, les processus et les agents en v1 ; deux packs (livraison logicielle, rédaction et
  revue de document).
- **J3** : le profil, le vocabulaire, les types, les packs, les règles complètes ; le troisième pack.
- **J8** : les trois packs montés par le parcours d'arrivée.

## Liens

- [PV de la séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md), R94 et R103
- [PV de la séance n°14](../conseil/seances/2026-10-31-souverainete-operationnelle.md), R85 et R86
- [PV de la séance n°2](../conseil/seances/2026-10-27-vision.md), les niches A et B
