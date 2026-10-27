---
id: conseil-seance-2026-10-27-menage-spec-v2
title: "Conseil d'Avenir : séance n°3 du 27/10/2026"
doc_type: pv-seance
statut: active
date: "27/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, menage, v2, harnais]
related:
  - "../README.md"
  - "./2026-10-27-vision.md"
  - "../../../v1/09-audits/Etat_des_lieux_v1_avant_v2.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°3 du 27/10/2026 : le ménage et la spécification de la v2

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

Jobs et Musk relisent le ménage tranché par la Présidence et la spécification de la v2. Ils approuvent le cap et
l'architecture (le serveur garde, l'ordinateur calcule ; une seule porte). Ils poussent trois choses : le ménage avant
le sprint, un seul parcours dans le sprint, et une règle d'affichage (on ne montre que ce qui marche). Désaccord
conservé : supprimer ce qui n'a pas d'usage mesuré (Musk) ou le masquer (Présidence, Jobs).

- **Saisine** (Présidence) : passer le ménage avec Jobs et Musk au début de la spécification de la v2, et les mettre sur
  la spécification. « Attention à ne pas virer ce qui pourrait nous servir. »
- **Formation** : restreinte, à la demande de la Présidence : Elon Musk, Steve Jobs. Ordre de parole tiré au sort :
  Musk, puis Jobs. Contradicteur, tiré au sort : Steve Jobs.
- **Note de formation** : la charte prévoit 5 à 7 membres, un par pôle au moins. Les deux membres viennent du pôle
  Impulsion, enclin à couper. Le contrepoids est la règle de la Présidence : supprimer le sûr, masquer le doute.
- **Fiches** : à jour (21/10/2026, moins de 30 jours).

## Dossier

1. `[ÉTABLI]` L'état des lieux de la v1 : 43 pages, dont 29 joignables dans l'app desktop ; ce qui est vérifié et ce qui
   ne l'est pas ; quatre problèmes, PC-059 à PC-062
   ([état des lieux](../../../v1/09-audits/Etat_des_lieux_v1_avant_v2.md)).
2. `[ÉTABLI]` Le ménage tranché par la Présidence le 27/10 : le .exe d'abord, le Store et la webapp ensuite ; l'équipe
   gardée (c'est du contexte) ; Mentions gardé ; Assignments à retravailler ; GitHub et Slack gardés, à faire
   marcher ; Public et Private gardés ; panneau Status retiré de la vue ; Pages supprimées (tout ira dans le Brain
   OS) ; Copilot gardé, à essayer ; code mort supprimé ; dans le doute, masquer plutôt que supprimer.
3. `[ÉTABLI]` La spécification de la v2, version 0.1
   ([spécification](../../../v1/road_to_v2/Specification_V2_Harnais.md)).

## Tour de table `[HYPOTHÈSE]`

- **Elon Musk** (Impulsion) : chaque élément gardé doit avoir un propriétaire nommé et une raison. Les Pages et le code
  mort partent, d'accord ; le panneau Status aussi, et il le supprimerait plutôt que de le masquer, car le code masqué
  coûte quand même (tests, mises à jour, failles). L'équipe est gardée, mais il demande une date pour le serveur
  d'équipe : sans date, c'est un entrepôt. Copilot : un essai dans les dix jours, sinon hors du menu. Sur la
  spécification : il approuve « le serveur garde, l'ordinateur calcule » et « tracer avant d'agir » limité aux sorties,
  qui garde la vitesse. Il passe chaque invariant à la question « qui l'a écrit, que se passe-t-il si on le retire ? »
  et n'en retire aucun ; il prévient que « inconnu, donc demandé » fera attendre au début, et l'accepte si le harnais
  propose une règle après des décisions répétées (§6.5). Il veut le temps de cycle mesuré dès le premier jour, et un
  relecteur d'un autre fournisseur que l'agent : des modèles concurrents se surveillent mieux. *Sa recommandation : le
  ménage d'abord, en une demi-journée ; on construit sur ce qui reste.*
- **Steve Jobs** (Impulsion, siège historique, contradicteur) : garder l'équipe lui convient, à une condition : l'app ne
  montre jamais une fonction qui ne marche pas. Les tuiles GitHub et Slack restent cachées tant qu'elles ne marchent pas
  dans l'app, l'équipe aussi jusqu'au serveur d'équipe ; masquer n'est pas supprimer, la règle de la Présidence lui
  va. L'Inbox pose une seule question, « qu'est-ce qui m'attend ? » : Mentions reçoit les appels des agents et des
  personnes ; Assignments se fond dans My Work. Public et Private doivent dire ce qu'ils font : « Tout l'espace »,
  « Collaborateurs seulement ». Sur la spécification : le produit, c'est la carte de résultat, pas le harnais ; il veut
  la carte dessinée avant le code, en langage clair, un geste. Il demande des règles publiques d'admission pour les
  agents et les connecteurs, sur le modèle des règles d'examen de l'App Store : ce qu'un connecteur déclare pour
  entrer (ses écritures, ses actions inverses, les données qu'il envoie). En contradicteur, il conteste un sprint sur
  trois fronts : un seul parcours parfait (importer deux versions, voir l'écart, déléguer, lire la carte) vaut mieux
  que trois briques à moitié. Il trouve la spécification longue : la page « En une page » doit suffire à un lecteur
  pressé. *Sa recommandation : on ne montre que ce qui marche ; ce qui ne marche pas encore est masqué, pas supprimé.*

## Confrontation

1. **Supprimer ou masquer** : Musk supprime ce qui n'a ni propriétaire ni usage mesuré, parce que le code masqué coûte ;
   Jobs masque ce qui ne marche pas encore et supprime ce qui ne servira jamais. Synthèse : supprimer le sûr ; masquer
   ce qui attend une condition (l'équipe attend le serveur, GitHub et Slack attendent PC-060), avec une date de revue ;
   un élément masqué sans date est candidat à la suppression.
2. **Le sprint** : Musk réduit le sprint au chemin critique ; Jobs veut un parcours parfait. Accord : un seul parcours,
   celui du premier cas d'usage ; ce qui n'y est pas sort du sprint. Divergence sur la carte : Musk se contente au
   sprint d'une liste de trois contrôles ; Jobs veut la carte dessinée d'abord.
3. **L'admission des connecteurs** : Jobs veut des règles publiques dès maintenant ; Musk les veut après les premiers
   clients, pour ne pas écrire de règles pour personne.

## Recommandations

| # | Recommandation | Pour | Contre |
| --- | --- | --- | --- |
| R10 | **Le ménage avant le sprint**, en une demi-journée : on construit sur ce qui reste | Musk, Jobs | Aucun |
| R11 | **Un seul parcours dans le sprint** : celui du premier cas d'usage ; ce qui n'y est pas sort du sprint | Jobs, Musk | Aucun |
| R12 | **On ne montre que ce qui marche** : ce qui attend une condition est masqué avec une date de revue ; masqué sans date, candidat à la suppression | Jobs ; Musk, avec la date | Aucun |
| R13 | **La carte de résultat dessinée avant d'être codée** | Jobs | Musk (au sprint, une liste de trois contrôles suffit) |
| R14 | **Des règles d'admission publiques pour les agents et les connecteurs** : ce qu'ils déclarent pour entrer (écritures, actions inverses, données envoyées) | Jobs | Musk (après les premiers clients) |
| R15 | **Un relecteur d'un autre fournisseur que l'agent** | Musk ; Jobs, si l'utilisateur n'en voit que le verdict | Aucun |

**Désaccords conservés** : Musk supprimerait le panneau Status au lieu de le masquer, et retirerait Copilot du menu sans
essai dans les dix jours ; la Présidence a gardé Copilot. Jobs cacherait les tuiles GitHub et Slack jusqu'à ce qu'elles
marchent ; la Présidence les a gardées, à faire marcher.

## Décision de la Présidence

En attente : la Présidence relit la spécification et ce procès-verbal.

## Notes du secrétariat

- La spécification intègre déjà, comme propositions, R11 (§18 : un seul parcours) et R15 (§7.6 : un relecteur d'un autre
  fournisseur quand c'est possible). Les autres attendent la décision de la Présidence (§20 de la spécification).
- La fiche de Musk signale que ses positions recoupent ses intérêts, Cursor compris (racheté par SpaceX) : son avis
  sur l'ordre des agents n'a pas été sollicité.
- Jobs est mort en 2011 : il n'a pris aucune position sur les agents d'IA ; ses positions ici sont des transpositions de
  ses positions documentées (se concentrer, c'est renoncer ; partir de l'expérience client ; les règles d'examen de
  l'App Store).
- R12 et la règle de la Présidence se rejoignent : la date de revue est ce qui empêche un masquage de devenir un
  oubli.

## Suites

- La Présidence relit la spécification de la v2 et tranche le §20, dont R10 à R15.
- Puis le sprint de trois jours, avec la banque de tests, en mode développement.
