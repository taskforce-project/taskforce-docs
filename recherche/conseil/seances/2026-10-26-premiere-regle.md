---
id: conseil-seance-2026-10-26-premiere-regle
title: "Conseil d'Avenir : séance du 26/10/2026"
doc_type: pv-seance
statut: active
date: "26/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance]
related:
  - "../README.md"
  - "../../experiences/Experiences.md"
---

# Séance du 26/10/2026 : la première règle non négociable de TaskForce

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.

- **Saisine** : *Quelle est la première règle non négociable de TaskForce ?* Proposée par le secrétariat (charte §2.1), la
  Présidence n'en ayant pas posé ; horizon : toutes les versions à venir.
- **Formation** : restreinte, 7 membres. Ordre de parole tiré au sort : Margaret Hamilton, Tristan Harris, Atul Gawande,
  Jeff Bezos, Satya Nadella, Elon Musk, Yoshua Bengio. Contradicteur : Elon Musk.
- **Fiches** : toutes à jour (21/10/2026, moins de 30 jours). Margaret Hamilton est morte le 30/09/2026
  ([AP](https://www.wbur.org/news/2026/10/09/margaret-hamilton-nasa-apollo-mit-software-engineering-obituary)) : son
  siège devient historique.

## Dossier

1. `[ÉTABLI]` Chez Anthropic, « Claude sessions amount to around 80% idly waiting for human input » ; la part des
   sessions consacrée à piloter des agents passe de 10 % à 22 % entre l'automne 2025 et le printemps 2026
   ([Anthropic](https://www.anthropic.com/research/employment-at-anthropic), 16/10/2026). Périmètre : ses employés.
2. `[ÉTABLI]` « Humans steer. Agents execute. » : OpenAI décrit un produit livré sans code écrit à la main, l'ingénieur
   concevant l'environnement et l'intention ([OpenAI](https://openai.com/index/harness-engineering/), 11/02/2026).
3. `[ÉTABLI]` Satya Nadella propose de séparer l'intelligence de l'autorité qui s'exerce sur elle : contrôles hors du
   modèle, frein d'urgence, trace lisible, aucun modèle qui valide son propre travail
   ([blog](https://snscratchpad.com/posts/models-as-insider-risks/), 10/10/2026).
4. `[ÉTABLI]` Les règles de mission d'Apollo étaient des décisions préparées avant le vol, qui guidaient les décisions en
   temps réel ([Keyser, NASA TN D-7822](https://ntrs.nasa.gov/citations/19750002893), 1974).
5. `[ÉTABLI]` Checklist chirurgicale de l'OMS : décès de 1,5 % à 0,8 %, complications de 11 % à 7 %, sur 7 688 patients
   ([Harvard Gazette](https://news.harvard.edu/gazette/story/2009/01/surgical-safety-checklist-drops-deaths-and-complications-by-more-than-one-third/), 2009).
6. `[ÉTABLI]` AI Act, annexe III, point 4 b) : est à haut risque une IA qui attribue des tâches selon le comportement des
   personnes ou évalue leur performance au travail ([Règlement (UE) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)).
   `[DÉDUIT]` Smart Assign pourrait être concerné selon son usage prévu ; avis juridique requis.
7. `[ÉTABLI]` TaskForce : hors du socle autorisé d'avance, chaque action de Claude Code attend une décision dans l'app, et
   sans décision c'est un refus (`taskforce-runner/src/agent.ts`) ; rien n'est fusionné sans la personne ; les données
   restent sur l'ordinateur.
8. `[ÉTABLI]` Le 25/10, une règle de Windows que personne ne voyait a bloqué la version Store depuis le 22/10 ; on l'a
   appris par une capture d'écran (PC-058).

## Tour de table `[HYPOTHÈSE]`

- **Margaret Hamilton** (Science, siège historique) : la règle existe avant la mission ; sur Apollo 11, les alarmes 1201
  et 1202 ont affiché l'essentiel et Houston savait déjà que c'était un go. L'interface la plus fragile est l'écran
  d'approbation. *Sa règle : rien ne part qui n'ait été prévu par écrit avant la mission ; l'imprévu s'arrête et pose
  une question binaire.*
- **Tristan Harris** (Harmonie) : si les agents attendent un humain 80 % du temps, le produit sera tenté de faire cliquer
  plus vite ; une approbation arrachée par fatigue n'est pas une décision. La charge de la preuve revient à l'agent.
  *Sa règle : TaskForce ne mesure jamais son succès au nombre de décisions qu'il obtient de l'humain.*
- **Atul Gawande** (Science) : l'échec vient de l'exécution ; trois points de pause courts (avant d'exécuter, de fusionner,
  de mettre en production), cinq à neuf points, un droit d'arrêt, une mesure avant/après. *Sa règle : des points de
  pause fixés d'avance, où n'importe qui peut dire stop.*
- **Jeff Bezos** (Impulsion) : une branche, un commit, un test se défont ; les traiter en portes à sens unique fabrique
  l'attente. *Sa règle : l'humain tranche les portes à sens unique, et seulement elles.*
- **Satya Nadella** (Pont) : la question est où vit la règle ; dans le prompt, elle vit dans le modèle, qui est un risque
  interne. Le runner de TaskForce est déjà entre l'agent et la machine ; il manque une trace infalsifiable et un audit
  indépendant du fournisseur. *Sa règle : l'autorité ne vit jamais dans l'agent.*
- **Elon Musk** (Impulsion, contradicteur) : une administration pour robots ; chaque règle doit avoir un auteur nommé,
  on supprime d'abord. Le danger est un produit trop lent. *Sa règle : toute règle a un auteur nommé, et une règle qui
  ne bloque jamais rien est candidate à la suppression.*
- **Yoshua Bengio** (Science) : une règle muette peut être celle qui bloquera le jour où l'agent apprend à la contourner ;
  la réversibilité ne se décrète pas (migration, e-mail, secret). *Sa règle : un agent n'est jamais juge de son propre
  risque.*

## Confrontation

1. **Qui décide de ce qui est réversible ?** Bezos : faire attendre le réversible fait perdre le client. Bengio : l'agent
   ne peut pas classer ses propres actions. Hamilton : la classification s'écrit avant la mission, en table versionnée
   appliquée par le runner. Accord sous conditions : table courte et réversible sans attente (Bezos), table hors de
   l'agent (Bengio).
2. **Supprimer les règles muettes ?** Musk : une règle qui ne bloque rien coûte. Gawande : un contrôle rare peut sauver
   une vie le jour où il sert. Synthèse : auteur, raison, date de revue, déclenchements comptés ; suppression sur
   preuve, jamais au silence.
3. **Que mesure-t-on ?** Bezos : le délai vu par le client. Harris : toute mesure de débit pousse au clic par fatigue.
   Synthèse : temps d'attention humaine par résultat accepté, avec les décisions regrettées en contre-mesure ; jamais le
   nombre d'approbations.

## Recommandations

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| - | --- | --- | --- | --- | --- |
| R1 | **Première règle : « Aucun agent ne décide seul d'une action irréversible, ni de ce qui est irréversible. »** Table des actions écrite d'avance, hors de l'agent, appliquée par le runner | Hamilton, Gawande, Bengio, Nadella, Harris ; Bezos sous condition | Musk | [E7](../../experiences/Experiences.md#e7--quelle-part-de-lattente-humaine-porte-sur-du-réversible-) | Moins de 30 % de l'attente sur du réversible |
| R2 | **Les règles sont du code** : auteur, raison, date de revue, déclenchements comptés, suppression sur preuve | Musk, Gawande, Hamilton, Nadella, Bengio | Aucun | [E8](../../experiences/Experiences.md#e8--des-règles-écrites-comme-du-code-sont-elles-relues-) | Fichier jamais relu en 10 jours |
| R3 | **Mesure nord** : temps d'attention humaine par résultat accepté, décisions regrettées en contre-mesure | Harris, Gawande, Bezos, Nadella | Musk (préfère le temps de cycle) | [E9](../../experiences/Experiences.md#e9--le-temps-dattention-par-résultat-accepté-se-mesure-t-il-) | Impossible à mesurer de façon fiable |
| R4 | **Le vérificateur n'est pas l'agent** : avant une porte à sens unique, une preuve que l'humain lit en deux minutes | Bengio, Nadella, Musk, Gawande, Hamilton | Bezos (seulement pour l'irréversible) | [E10](../../experiences/Experiences.md#e10--un-relecteur-dédié-trouve-t-il-de-vrais-défauts-) | Moins d'un défaut utile sur 10 pull requests |

**Désaccords conservés** : Musk tient que la première règle devrait porter sur la vitesse ; Bezos ne soutient R1 que si
le réversible n'attend jamais ; Harris refuse toute mesure de débit.

## Décision de la Présidence (27/10/2026)

| # | Décision | Raison, dans les mots de la Présidence |
| - | --- | --- |
| R1 | **Retenue** | « Le fait de pouvoir faire une branche avec les mises à jour peut permettre de trouver un compromis pour la vitesse, et rendre une action réversible et non impactante. » |
| R2 | **Retenue** | « Attention à mieux expliquer, parce que ça peut porter à confusion. » |
| R3 | **Retenue** | Le temps de cycle doit aussi être mesuré, il pourra servir. L'envoi de données n'est pas impossible : la Présidence peut le mettre en place. |
| R4 | **Retenue** | « On pourrait même entraîner un agent exprès, ou trouver un agent très bon en pratique sur l'analyse, et lui dire aussi quoi analyser, avec une partie libre. » |
| Règle zéro | **Ratifiée** | Formulation de la Présidence : « On vise dix ans, on justifie en dix jours. » |

**R2, dit plus simplement** (demande de la Présidence) : chaque règle qui encadre un agent (ce qu'il fait seul, ce qui
lui est interdit, ce qui demande ton accord) est écrite dans un fichier, avec qui l'a décidée, pourquoi et quand la
revoir. L'app compte combien de fois chaque règle a servi. On ne retire une règle que si les chiffres montrent qu'elle
est inutile, jamais parce qu'elle n'a pas encore servi.

## Notes du secrétariat

- Le chiffre de 80 % ne vaut que pour Anthropic.
- Le point AI Act (Smart Assign) demande un avis juridique avant toute conclusion.
- R3 : l'app promet aujourd'hui de n'envoyer aucune donnée d'usage (site, `llms.txt`). Mesurer d'abord sur l'ordinateur ;
  un envoi éventuel serait un choix de produit, avec consentement explicite et mise à jour de la politique de
  confidentialité ([Q10](../../Questions-ouvertes.md#q10--mesurer-lattention-humaine--sur-lordinateur-seulement-ou-avec-des-données-envoyées-)).
- R4 : entraîner un agent dédié bute sur la contrainte C4 (budget proche de zéro, aucun entraînement) ; choisir un modèle
  existant, bon en analyse, avec une liste de points à vérifier et une partie libre, est faisable tout de suite.
- R1 : la branche de travail rend réversible ce qui reste local ; ce qui en sort (push, fusion, migration, envoi
  externe, secret) reste irréversible et passe par l'humain.

## Suites

- Expériences E7 à E10 déclarées dans [`experiences/Experiences.md`](../../experiences/Experiences.md) ; elles
  s'exécutent en mode développement, après arbitrage de priorité.
- Question ouverte Q10 dans [`Questions-ouvertes.md`](../../Questions-ouvertes.md).
- Règle zéro ratifiée dans la [charte](../README.md) §11 ; séance au registre (§12).
- Prochaine séance : la vision de la Présidence, qui n'a pas encore été présentée au Conseil.
