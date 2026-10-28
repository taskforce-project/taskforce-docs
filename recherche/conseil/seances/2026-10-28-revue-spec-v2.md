---
id: conseil-seance-2026-10-28-revue-spec-v2
title: "Conseil d'Avenir : séance n°4 du 28/10/2026"
doc_type: pv-seance
statut: active
date: "28/10/2026"
auteur: Pierre MICHEL
formation: élargie
tags: [recherche, conseil, seance, v2, harnais, architecture, revue]
related:
  - "../README.md"
  - "./2026-10-27-menage-spec-v2.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°4 du 28/10/2026 : la revue de la spécification de la v2

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

Le Conseil relit la spécification de la v2 (version 0.2) et la valide dans son architecture : un monolithe modulaire,
un serveur qui garde, des ordinateurs qui calculent, une seule porte. Il demande d'écrire les contrats avant le code, un
garde fermé par défaut, un aperçu des effets avant toute décision, et une demande de décision conçue contre l'erreur
humaine. L'amendement de R1 (laisser un juge indépendant classer les actions inconnues) divise : pour, par paliers et
sur preuve ; contre tant que l'erreur du juge n'est pas mesurée. L'agent interne avec un petit modèle entre au sprint si
autre chose en sort.

- **Saisine** (Présidence) : vérifier la documentation de la v2, avec questions, retours, précisions et désaccords
  francs. Chantiers et responsables fixés par la Présidence : le harnais (Bengio en tête, LeCun en second, puis des
  contradicteurs techniques et l'UX) ; la décision humaine (Bengio en tête, LeCun, Bezos) ; les règles (Bengio, LeCun,
  Musk) ; le bac à sable (Jobs, Musk) ; le schéma (LeCun, Bengio, Musk) ; l'interface (Jobs, puis le pôle Design) ;
  les équipes (Musk) ; le vocabulaire (« une personne sensée » : le secrétariat a proposé Kenza Ait Si Abbou).
- **Formation** : élargie (11), à la demande de la Présidence : Elon Musk, Steve Jobs, Don Norman, Julie Zhuo, Karri
  Saarinen, Jeff Bezos, Yoshua Bengio, Margaret Hamilton, Kenza Ait Si Abbou, Yann LeCun, Tristan Harris. Ordre de
  parole tiré au sort, dans cet ordre. Contradictrice, tirée au sort : Margaret Hamilton.
- **Pôle Design** : Don Norman, Julie Zhuo et Karri Saarinen rejoignent le Conseil, « juste derrière Jobs »
  (Présidence, 28/10/2026) ; fiches rédigées et sourcées avant la séance.
- **Fiches** : à jour (moins de 30 jours).

## Dossier

1. `[ÉTABLI]` La spécification de la v2, version 0.2, et son schéma
   ([spécification](../../../v1/road_to_v2/Specification_V2_Harnais.md)).
2. `[ÉTABLI]` Les décisions de la Présidence du 28/10 : la webapp d'abord, en local, puis le .exe ; un code source,
   trois produits ; le front du Brain OS supprimé au profit d'un panneau de contexte ; l'équipe comme matrice des
   rôles ; un coffre à secrets ; l'agent qui propose des mises à jour sourcées ; R10 à R15 retenues ; l'approche A.
3. `[ÉTABLI]` Faits vérifiés le 28/10 (sources dans la spécification) : le hook `PreToolUse` de Claude Code passe avant
   chaque action ; un hook HTTP injoignable laisse passer l'appel, sauf avec `onFailure: "block"` (2.1.295) ; un « ask »
   finit en refus sans interface ; Claude Code n'a pas de bac à sable sous Windows natif ; Codex, Cursor et Gemini CLI
   n'ont pas de « demander » sans interface ; Ollama fait tourner Claude Code sur un modèle local, ce qu'Anthropic ne
   prend pas en charge ; Java 25 est la LTS en cours, Spring Boot 4.1.2 la dernière version ; le SDK Java de MCP
   (2.1.0) n'apporte pas l'autorisation.
4. `[ÉTABLI]` R1, ratifiée à la séance n°1 : « Aucun agent ne décide seul d'une action irréversible, ni de ce qui est
   irréversible. » La Présidence en conteste la seconde moitié : un agent qui ne décide jamais de ce qui est
   irréversible ne prendrait jamais seul une action ; elle évoque un seuil. Amendement proposé au §6.2 de la
   spécification.
5. `[ÉTABLI]` L'hypothèse rappelée par la Présidence : quand la décision vit dans l'architecture, un petit modèle local
   doit suffire à tout ou partie des tâches.

## Tour de table `[HYPOTHÈSE]`

- **Elon Musk** (Impulsion) : pour les équipes, l'approche A sans hésiter : une seule interface à maintenir, la webapp
  existe ; B met tout en double. Le monolithe modulaire, d'accord : chaque service en plus est une pièce qui casse ;
  Embabel attendra tant que la boucle de Cortex suffit, on supprime avant d'ajouter. Les règles : un moteur petit, une
  table par défaut qui tient sur une page, chaque classe justifiée par un cas réel, chaque règle avec un auteur nommé.
  Le bac à sable vaut par le temps de cycle, le workflow complet rejoué en minutes : il le veut mesuré dès le sprint,
  et plus tard plusieurs essais en parallèle. L'amendement de R1 : pour, avec un propriétaire nommé du seuil, sinon les
  agents attendront toujours. Le sprint est trop chargé si l'agent interne s'ajoute : il ne l'accepte que si autre
  chose en sort. *Sa recommandation : le moins de pièces possible ; rien de neuf dans le sprint sans retirer autre
  chose.*
- **Steve Jobs** (Impulsion, siège historique) : le panneau de contexte, un seul endroit, c'est juste ; il ne doit pas
  devenir un second Brain OS et ne montre que ce qui sert la tâche en cours. Le bac à sable est peut-être la fonction
  la plus forte, à condition que la personne n'ait jamais à comprendre ce qu'est un bac à sable : elle voit
  « Essayer », puis « Voir ce qui changera », puis « Appliquer » ; le mot reste interne. Les secrets : demander en
  clair, à chaque fois ; la détection dit pourquoi elle arrête un texte et propose le coffre en un geste. Les règles
  d'admission publiques (R14) sur le modèle des règles d'examen de l'App Store. `/` et `@`, oui, s'ils se découvrent :
  la liste apparaît dès qu'on tape `/`. La spécification laisse voir trop de mots internes (porte, classe, mission) :
  aucun ne doit arriver à l'écran. *Sa recommandation : essayer, voir ce qui changera, appliquer ; les mots du harnais
  restent sous le capot.*
- **Don Norman** (Design) : derrière chaque erreur, chercher le défaut de conception. La demande de décision est conçue
  contre les deux erreurs : contre le raté, elle montre l'action exacte et son effet irréversible, pas un « oui »
  générique validé par habitude ; contre la méprise, elle montre ce que l'agent a compris du but avant d'agir. La
  délégation partielle est la zone dangereuse : chacun doit savoir ce que l'autre fait et va faire, donc l'état de
  l'agent se voit en continu dans le panneau, pas seulement par des alarmes. La carte de résultat est un dialogue : ce
  qui a été fait, pourquoi, ce qui reste incertain, ce qu'on attend de la personne. `/` et `@` doivent se découvrir,
  et « Annuler » existe partout où le bac à sable le permet. Le dossier de preuve remonte aux causes de conception, pas
  à un fautif ; l'autonomie se règle comme des rênes, que les règles tendent ou relâchent selon le risque. *Sa
  recommandation : chaque demande montre l'action exacte, son effet et ce que l'agent a compris du but ; tout ce qui se
  défait porte un « Annuler ».*
- **Julie Zhuo** (Design) : l'amendement de R1 a déjà une forme, une échelle d'autonomie : conseiller ; adjoint, qui
  agit mais dont chaque action est revue avant de s'appliquer ; régent, qui agit seul dans un domaine borné, surveillé
  et réversible. Chaque promotion se gagne par des preuves proportionnées au risque, domaine par domaine. Le contexte
  avant l'intelligence : le même modèle passe d'un peu plus de 80 % à 98 % de bonnes réponses quand on lui donne le
  contexte, un argument pour l'hypothèse des petits modèles, qui reste à mesurer. La carte de résultat se juge comme une
  critique de produit : la première minute, le premier usage, les semaines suivantes, avec un pronostic écrit. Contre
  la boîte de saisie vide : des modèles de demandes et des suggestions, et un agent qui dit ce qui dépasse sa
  compétence. Le fil de l'équipe doit servir le travail, pas déplacer du temps passé. *Sa recommandation : une échelle
  d'autonomie par domaine, chaque promotion gagnée par la preuve.*
- **Karri Saarinen** (Design) : la confiance dans un agent se joue dans l'interface. La grammaire de la délégation :
  l'humain reste assigné et répond du travail ; l'agent apparaît comme délégué ; son état (actif, en attente, en
  erreur, terminé) et son activité restent visibles. Il refuse la validation pas à pas, qui réduit l'humain à un
  tampon : on conçoit l'environnement, on laisse l'agent travailler, on juge le résultat ; la carte de résultat est le
  lieu de ce jugement. Sa critique vise les étapes, pas les actions irréversibles. Le panneau de contexte est un établi
  ancré dans l'objet ouvert (l'issue, la mission), pas une boîte de chat générique ; `/` et `@` s'y rattachent. Les
  secrets se rangent dans les réglages, jamais collés dans la conversation : le coffre va dans ce sens. Un outil
  jamais lent, des réglages par défaut tranchés plutôt que des options sans fin, et le panneau refondu d'un bloc, pas
  module par module. *Sa recommandation : la délégation se voit ; l'humain juge le résultat, pas chaque étape.*
- **Jeff Bezos** (Impulsion) : la spécification suit sa règle : automatiser le réversible, l'humain tranche le sens
  unique. L'amendement de R1 : pour, c'est une porte à double sens bien dimensionnée, puisqu'une erreur du juge sur du
  réversible se défait. L'écran de décision donne l'essentiel pour décider avec environ 70 % de l'information, pas
  tout. Celui qui accepte peut noter son désaccord, et le désaccord est tracé. La mesure reste le délai vu par le
  client. *Sa recommandation : chaque demande dit si la porte est à sens unique, et pourquoi ; le reste ne demande
  rien.*
- **Yoshua Bengio** (Science, chef de file du harnais et de la décision humaine) : les invariants lui conviennent ; le 2,
  reformulé (« l'agent qui agit n'est pas juge de son propre risque »), en est le cœur. L'amendement de R1 : pour, à ses
  conditions. Le classificateur est un juge non agentique, sans objectif propre, sans outil, sans action ; il estime la
  probabilité d'un tort, pas seulement la réversibilité ; son seuil est prudent au départ et possédé par une personne ;
  son taux d'erreur se mesure sur la banque de tests avant qu'il décide quoi que ce soit ; la défense en profondeur reste
  derrière lui (bac à sable, action inverse, preuve). Des modèles distinguent un test d'un usage réel : la banque de
  tests doit contenir des cas qu'on ne distingue pas de l'usage réel. Contre le biais d'automatisation, l'écran de
  décision montre la preuve avant l'avis de l'IA. Un garde qui laisse passer quand il tombe n'est pas un garde :
  `onFailure: "block"` partout, et aucune mission sans garde joignable. *Sa recommandation : l'amendement, seulement
  avec un juge non agentique dont l'erreur est mesurée avant qu'il décide.*
- **Margaret Hamilton** (Science, siège historique, contradictrice) : contre l'amendement au départ : « cela n'arrivera
  jamais » n'est pas une raison ; une action inconnue reste humaine tant que le juge n'a pas prouvé son taux d'erreur, et
  aucun seuil ne se règle à l'intuition. Contre un sprint qui livre la porte sans contrats d'interface : les erreurs
  d'interface font l'essentiel des erreurs ; le paquet de règles, le format de preuve et l'adaptateur d'agent s'écrivent
  avant le code, avec leurs tests de contrat. Les priorités : quand l'ordinateur sature (un petit modèle, peu de
  mémoire), que lâche le harnais d'abord ? Elle le décide avant la mission : on garde la porte et la preuve, on lâche le
  fil, les vecteurs et le panneau. La demande de décision est un affichage prioritaire, comme les alarmes 1201 et 1202
  d'Apollo 11 : une question binaire, l'essentiel seulement. Le ménage : aucune suppression sans raison écrite ; la
  raison existe, c'est la décision de la Présidence, et elle va dans chaque commit. *Sa recommandation : les contrats
  d'abord ; l'inconnu reste humain jusqu'à la preuve ; le mode dégradé décidé avant la mission.*
- **Kenza Ait Si Abbou** (Pont, vocabulaire) : elle valide le vocabulaire du §3 pour les ingénieurs, pas pour
  l'utilisateur : « porte », « classe », « paquet » n'apparaissent jamais à l'écran. Il faut deux glossaires : un
  interne, celui de la spécification, et un pour l'interface, en anglais, relu par une personne qui n'est pas
  ingénieure. La matrice des rôles est la gouvernance de l'IA d'une entreprise moyenne : elle demande un modèle prêt à
  l'emploi pour une PME (qui décide de quoi), modifiable. Le fil de l'équipe ne doit jamais devenir un agent qui
  « lit » les humains : il montre le travail, pas un score des personnes. *Sa recommandation : un glossaire de
  l'interface relu par une personne non ingénieure, et une matrice des rôles prête à l'emploi.*
- **Yann LeCun** (Science, second du harnais) : il soutient l'hypothèse des petits modèles : un agent n'est fiable que
  s'il prévoit l'effet de ses actions ; si l'architecture porte le plan, les contraintes et la vérification, le modèle
  remplit des étapes, et un petit modèle suffit souvent. Cela se mesure tâche par tâche. Il demande un composant
  explicite, l'aperçu des effets (plan, diff, exécution à blanc), entre la proposition d'une sortie et la décision :
  c'est le modèle du monde du harnais, au sens d'un ingénieur, et il le veut dans le schéma. Les règles sont des
  contraintes vérifiables, pas des consignes dans un prompt : chacune a son cas dans la banque de tests. Le sprint doit
  porter l'agent interne avec un petit modèle local sur le parcours, sinon l'hypothèse ne se teste pas au .exe ; Claude
  Code sert de comparaison. Le harnais reste ouvert, comme l'AGPL, avec des formats documentés. Il conteste le cadrage
  de « perte de contrôle » pour des agents de bureau : les incidents viennent de bacs à sable mal appliqués, et S1
  suffit au sprint. *Sa recommandation : un aperçu des effets avant toute décision, et l'agent interne avec un petit
  modèle sur le parcours du sprint.*
- **Tristan Harris** (Harmonie) : contre la fatigue du clic, un plafond de demandes par personne et par jour, et des
  demandes regroupées ; on mesure les décisions regrettées, jamais le nombre de décisions obtenues. Le fil de l'équipe,
  « chacun sait ce que chacun fait », peut devenir de la surveillance : il montre le travail et les résultats, pas
  l'activité minute par minute, et aucun score individuel. L'AI Act classe à haut risque une IA qui évalue la
  performance des travailleurs (annexe III, point 4 b, dossier de la séance n°1) : un avis juridique passe avant de
  construire le fil. Pas d'habillage humain des agents : « un agent vous appelle » imite l'humain ; « Décision demandée
  par » suivi du nom de l'agent le dit sans l'imiter. *Sa recommandation : un plafond de demandes par personne, et un
  fil qui montre le travail sans noter les gens.*

## Confrontation

1. **L'amendement de R1** : pour, Bengio (à ses conditions), Zhuo (par paliers), Bezos, Musk ; contre au départ,
   Hamilton. Synthèse : l'échelle de Zhuo appliquée au juge. D'abord il propose seulement, et aucune action ne part sur
   son avis ; son erreur se mesure sur la banque de tests et sur les décisions humaines réelles. Ensuite seulement il
   décide, domaine par domaine, au-dessus d'un seuil possédé par une personne, une fois son erreur passée sous une borne
   fixée d'avance.
2. **Le sprint** : LeCun veut l'agent interne sur le parcours ; Musk exige qu'autre chose en sorte ; Hamilton veut les
   contrats d'abord. Synthèse : le jour 1 commence par les contrats ; l'agent interne entre au jour 3 à la place du
   codage complet de la carte de résultat, qui se code au plus simple après son dessin (R13 tient : le dessin d'abord).
3. **Le fil de l'équipe** : la Présidence veut que chacun sache ce que chacun fait ; Harris et Kenza Ait Si Abbou
   craignent la surveillance ; Zhuo demande s'il sert le travail. Synthèse : le fil montre les missions, les résultats
   et les décisions, pas les personnes minute par minute, sans score individuel ; avis juridique sur l'AI Act avant de
   le construire.
4. **Le bac à sable, visible ou non** : Jobs ne montre jamais le mot ; LeCun et Bengio le veulent explicite pour
   l'auditeur. Synthèse : invisible pour l'utilisateur, lisible pour l'auditeur (séance n°2), avec les trois gestes
   « Essayer », « Voir ce qui changera », « Appliquer ».
5. **Corriger après coup, ou intervenir avant** : Saarinen signale les actions après coup, pour les annuler ; Bengio
   veut intervenir avant le dommage. Synthèse : après coup pour le réversible, qui part et se trace (R7') ; avant pour
   l'irréversible, qui attend (R1).

## Recommandations

| # | Recommandation | Pour | Contre |
| --- | --- | --- | --- |
| R16 | **Les contrats d'abord** : le paquet de règles, le format de preuve et l'adaptateur d'agent s'écrivent avant le code, avec leurs tests de contrat | Hamilton, Musk, LeCun | Aucun |
| R17 | **Un garde fermé par défaut** : `onFailure: "block"` (Claude Code 2.1.295 au moins), et aucune mission sans garde joignable | Bengio, Hamilton | Aucun |
| R18 | **L'amendement de R1 par paliers** : un juge non agentique, distinct de l'agent, propose d'abord, puis décide domaine par domaine au-dessus d'un seuil possédé par une personne, une fois son erreur mesurée | Bengio, Zhuo, Bezos, Musk | Hamilton (l'inconnu reste humain tant que la preuve manque) |
| R19 | **Un aperçu des effets** (plan, diff, exécution à blanc) avant toute décision humaine | LeCun, Norman, Jobs | Aucun |
| R20 | **L'agent interne avec un petit modèle local sur le parcours du sprint**, Claude Code en comparaison | LeCun, Bengio, Zhuo | Musk (seulement si autre chose sort du sprint) |
| R21 | **Une demande de décision conçue contre l'erreur** : l'action exacte, son effet, ce que l'agent a compris du but, la preuve avant l'avis de l'IA, une question binaire, la porte à sens unique dite comme telle | Norman, Bengio, Hamilton, Bezos | Aucun |
| R22 | **Les mots du harnais restent internes** : trois gestes pour l'utilisateur (essayer, voir ce qui changera, appliquer) et un glossaire de l'interface relu par une personne non ingénieure | Jobs, Kenza Ait Si Abbou, Norman | Aucun |
| R23 | **Un mode dégradé décidé d'avance** : on garde la porte et la preuve ; on lâche le fil, les vecteurs et le panneau | Hamilton | Aucun |
| R24 | **Un fil qui montre le travail, jamais un score des personnes** ; un plafond de demandes de décision par personne ; un avis juridique sur l'AI Act avant de construire le fil | Harris, Kenza Ait Si Abbou, Zhuo | Aucun |
| R25 | **Des cas indiscernables de l'usage réel** dans la banque de tests | Bengio | Aucun |
| R26 | **La délégation se voit** : l'humain reste assigné et répond du travail ; l'agent apparaît comme délégué, son état et son activité visibles en continu ; l'humain juge le résultat sur la carte, pas chaque étape, sauf l'irréversible | Saarinen, Norman, Zhuo | Aucun (Bengio : pour le sensible, intervenir avant le dommage) |

**Désaccords conservés** : Hamilton refuse que le juge décide quoi que ce soit avant que son erreur soit mesurée, même
par paliers ; Musk n'accepte R20 que contre un retrait dans le sprint ; Musk écarte Embabel tant que la boucle de
Cortex suffit.

## Décision de la Présidence

En attente : la Présidence relit ce procès-verbal et tranche R16 à R26, dont l'amendement de R1 (R18).

## Notes du secrétariat

- Formation élargie (11) à la demande de la Présidence, qui a nommé les chantiers et leurs responsables ; les cinq
  pôles sont présents.
- Conflits d'intérêts signalés : Musk (Cursor, racheté par SpaceX), Zhuo (Meta, qui rachète Sundial le 23/10/2026),
  Saarinen (Linear, concurrent direct de TaskForce et modèle revendiqué de son interface ; sa grammaire de la
  délégation, R26, est aussi ce que Linear vend).
- Le schéma de la spécification montre déjà l'aperçu des effets et le juge, comme propositions (R19, R18).
- R1 reste ratifiée telle qu'écrite tant que la Présidence n'a pas tranché R18.
- Jobs et Hamilton parlent depuis leurs principes documentés : leurs positions sur des agents d'IA sont des
  transpositions.

## Suites

- La Présidence tranche R16 à R26 ; la spécification passe en version 0.3.
- Puis la demi-journée de ménage (R10) et le sprint de trois jours, en mode développement.
