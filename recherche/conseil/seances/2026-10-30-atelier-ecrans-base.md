---
id: conseil-seance-2026-10-30-atelier-ecrans-base
title: "Séance n°13 du 30/10/2026 : l'atelier des écrans de base"
doc_type: pv-seance
statut: active
date: "30/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, ecrans, voix, cortex]
related:
  - "../README.md"
  - "./2026-10-28-atelier-design.md"
  - "./2026-10-29-recette-132.md"
  - "./2026-10-29-atelier-design-carte.md"
  - "./2026-10-29-reserves-premier-lot.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°13 du 30/10/2026 : l'atelier des écrans de base

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

L'équipe de Jobs dessine les écrans de base que R54 demandait (créer, relire, accorder), avec la nouvelle direction de la
Présidence : une seule entrée, où l'on écrit ou parle, sur tous les écrans. Les dessins sont dans une
[maquette](https://claude.ai/artifact/THpWp7FCEA9RBU1Q4L1R6f), à valider par la Présidence avant tout code (R54).

- **Une seule entrée, partout** : une barre en bas de chaque écran, où l'on écrit ou parle pour demander n'importe quoi.
  La voix écrit dans la barre ; rien ne part sans que le texte soit vu et envoyé.
- **Ce qui se défait se fait, ce qui ne se défait pas se demande** : Cortex crée un projet ou une issue tout de suite,
  avec « Undo » sur la carte ; une action qui sort de la machine ou ne se reprend pas garde sa demande d'accord.
- **Les trois écrans des retours** : le brouillon de création dans la conversation, la carte de résultat sur l'issue, la
  demande d'accord en mots.
- **La banque au moment de décider** : un refus devient un cas (workflow 8) ; un changement de modèle passe par la banque
  (workflow 9).
- **La voix reste sur la machine** : transcrite dans l'app desktop, sans service en ligne ; dans la webapp, seulement si
  la personne l'accepte en sachant où va sa voix.

Cinq recommandations, R76 à R80, en attente de la décision de la Présidence.

Désaccords conservés :
- **Karri Saarinen** : un établi, pas un chat. Une seule entrée ne doit jamais devenir le seul chemin ; le board, la
  liste et les réglages restent des écrans entiers, et les gestes fréquents des boutons sur leur objet.
- **Don Norman**, contradicteur : une barre qui accepte tout ne dit pas ce qu'elle sait faire. Les suggestions sous la
  barre ne remplacent pas un menu qu'on peut parcourir.

- **Saisine** (Présidence, 30/10/2026), en réponse aux questions du secrétariat :
  - « Cortex peut creer un projet oui tout passera par un input de chat + vocal globalement » ;
  - puis : « lance l ateliers, et go release en mm temps ».
  - Question posée par le secrétariat : à quoi ressemblent les écrans de base (l'arrivée, créer, relire, accorder, la
    carte de résultat, la banque dans les workflows 8 et 9) quand tout passe par une seule entrée de texte et de voix ?
- **Formation** : restreinte (7), un membre au moins par pôle, l'équipe de Jobs au complet :
  - Steve Jobs (Impulsion), qui mène l'UX ;
  - Don Norman, Julie Zhuo et Karri Saarinen (Design) ;
  - Kenza Ait Si Abbou (Pont), Tristan Harris (Harmonie), Atul Gawande (Science).
  - Ordre de parole tiré au sort le 29/10/2026 à 23:15 UTC, le 30/10 à 00:15 à Paris (`shuf`) : Norman, Harris, Zhuo,
    Jobs, Ait Si Abbou, Saarinen, Gawande.
  - Contradicteur désigné : Don Norman. Jobs l'était à la n°12.
  - À la différence des ateliers n°6 et n°9, les cinq pôles siègent.
- **Fiches** : toutes à jour (moins de 30 jours). Jobs, siège historique, ne se rafraîchit que sur une nouvelle source
  historique ; ce qu'il dit des téléphones et des assistants vocaux d'aujourd'hui vient du dossier.

## Dossier

1. `[ÉTABLI]` **L'arrivée aujourd'hui** : l'app s'ouvre sur un tableau de bord de suivi (« Good evening », « Pick up
   where you left off », Operations, My queue, Recent, puis les cartes Operations health, Throughput, Needs attention,
   Cortex usage). Navigation : Dashboard, Signals, My Queue, Operations, Intelligence, Members, Settings
   (`components/layout/topbar/app-topbar.tsx`, build de développement du 29/10/2026). R55 a retenu une autre arrivée, pas
   encore construite.
2. `[ÉTABLI]` **Cortex** vit dans un panneau à droite, « Ask AI » (`components/agent/agent-chat.tsx`) : une zone de
   texte « Ask your question… », des étapes, des cartes d'outils, des sources. Depuis la 1.6.5, une action que les règles
   demandent s'accorde par « Approve and run » ; il n'y a pas de geste pour la refuser. Depuis la 1.6.7, « Add to test
   bank » sous une réponse qui a appelé un outil.
3. `[ÉTABLI]` **Aucune entrée vocale** : aucune occurrence de `SpeechRecognition`, `getUserMedia` ni « microphone » dans
   `frontend/` et `desktop/` le 30/10/2026.
4. `[ÉTABLI]` **Créer** : le dialogue « Create issue » (`components/dialogs/create-issue-dialog.tsx`) ; Cortex crée une
   issue seul (règle `create-issue`), propose une note (règle `propose-knowledge`) et un projet (aucune règle ne couvre
   `project.create`, d'où une demande), et attend « Approve and run ». La Présidence a dit le 30/10 que Cortex peut créer
   un projet.
5. `[ÉTABLI]` **Un projet arrive avec des pages** : en développement le 29/10/2026, le projet « Recette 135 », accordé
   depuis Cortex, est venu avec trois pages de connaissances (« Runbook », « Done & shipped », « Known issues »), servies
   ensuite à Cortex d'après son dossier. Défaire le projet doit les défaire aussi.
6. `[ÉTABLI]` **Relire et accorder, aujourd'hui** : sur l'issue déléguée, « Agent done - ready for your review »
   (`components/sheets/delegate-agent-control.tsx`) ; pendant une mission, « Claude Code asks to run … » avec Allow et
   Deny, et « Download the record » (`components/sheets/run-activity.tsx`). La carte de résultat de J3 n'est pas
   construite.
7. `[ÉTABLI]` **La banque** : Réglages > Test bank et « Add to test bank » (#437, en production depuis la 1.6.7). Les
   workflows 8 et 9 de la [carte](https://claude.ai/artifact/CzYEJ2xV4kHQpPzWCd8y4x) sont dessinés comme proposés.
8. `[ÉTABLI]` **Ce qui cadre l'atelier** : R46 et R49 (les accords), R47 (Cortex prépare l'issue entière), R50 (la revue),
   R54 (créer, relire, accorder, dessinés puis validés avant le code), R55 à R59 (l'arrivée, le résultat daté, l'invisible
   en une ligne, la carte, le noyau), J1 à J9 (Cortex n'est pas l'endroit où l'on décide), R72 à R75 et l'ordre de Jobs :
   aucune surface nouvelle avant les écrans de base.
9. `[ÉTABLI]` **Contraintes** : C4 (budget proche de zéro) ; dans l'app desktop, le modèle tourne sur la machine de la
   personne (R62). `[DÉDUIT]` Une voix transcrite par un service en ligne fait sortir la parole de la machine. Dans Chrome,
   la reconnaissance vocale du navigateur passerait par un serveur (page « Using the Web Speech API » de MDN, à vérifier).

## Tour de table `[HYPOTHÈSE]`

| # | Membre | L'essentiel | Ce qu'il dessine |
| - | --- | --- | --- |
| 1 | Don Norman (Design, contradicteur) | Une barre vide n'a pas d'affordance : la personne ne sait pas ce qu'elle peut demander, ni ce que la machine a compris. Et chaque action doit pouvoir se défaire ; une confirmation de plus ne remplace pas un « annuler » | Des suggestions sous la barre, ce que Cortex a compris avant d'agir, et « Undo » partout où c'est possible |
| 2 | Tristan Harris (Harmonie) | Un micro toujours ouvert sert celui qui écoute, pas celui qui parle. Pas de mot d'éveil, pas d'écoute en fond : on appuie pour parler, on relâche, c'est fini | Le micro à l'appui, la transcription visible, rien envoyé seul |
| 3 | Julie Zhuo (Design) | Les interfaces de conversation ont cinq problèmes, d'abord la page blanche. La conversation doit se marier aux contrôles classiques : la barre lance, mais la réponse est une carte qu'on modifie | La barre, des suggestions, et des réponses en cartes modifiables |
| 4 | Steve Jobs (Impulsion) | Partir de ce que vit la personne : elle veut dire ce qu'elle veut et voir que c'est fait. Une seule entrée, la même partout, et dire non à tout le reste. Sur la vie privée : dire en clair à quoi l'on consent, et redemander | La barre en bas de chaque écran ; la voix dit où elle va |
| 5 | Kenza Ait Si Abbou (Pont) | Expliquer l'IA à tous : la voix ouvre l'outil à ceux qui n'écrivent pas de requêtes. Mais la personne doit garder le contrôle, chacun, pas seulement l'administrateur | La voix, et ce que Cortex a compris écrit en clair |
| 6 | Karri Saarinen (Design) | Un établi, pas un chat. Le chat est une forme faible et générique ; l'IA doit se poser sur une application structurée, où l'on revoit et approuve des résultats. La barre peut lancer, jamais devenir le seul chemin | Les vues restent des écrans ; les gestes fréquents restent des boutons sur leur objet |
| 7 | Atul Gawande (Science) | Une liste de contrôle qui demande tout est ignorée. Peu de pauses, aux bons moments : avant ce qui sort, avant ce qui ne se reprend pas, à la fin de la mission | Trois moments d'accord, pas plus, et dits en mots |

## Confrontation `[HYPOTHÈSE]`

### Tout par la barre, ou un établi ?

- **Jobs** : une seule entrée, la même partout. La personne n'a pas à savoir où est le menu « créer un projet ».
- **Saarinen** : le chat est générique. Si tout passe par la barre, l'outil perd sa forme : le board, la liste, la
  carte de résultat sont l'établi, et la barre seulement une façon d'y lancer du travail.
- **Zhuo** : les deux tiennent si la réponse n'est jamais un paragraphe : c'est une carte, sur l'objet, qu'on modifie
  avec des contrôles.
- **Où l'on arrive** : une seule entrée, sur chaque écran, pour lancer ; les réponses sont des cartes ; les vues et les
  boutons restent. Saarinen garde sa réserve : la barre ne doit pas remplacer un écran.

### La voix : quand écoute-t-elle, et où va-t-elle ?

- **Harris** : jamais d'écoute en fond. On appuie, on parle, on relâche.
- **Norman** : et ce qui a été compris s'affiche avant d'agir. Une commande vocale mal entendue qui agit seule est une
  erreur de conception, pas de la personne.
- **Jobs** : dire en clair où va la voix, et redemander.
- **Ait Si Abbou** : la voix sert d'abord ceux qui n'écrivent pas de requêtes ; elle doit marcher en français.
- **Où l'on arrive** : la voix écrit dans la barre ; rien ne part sans que le texte soit vu et envoyé. Dans l'app
  desktop, la transcription se fait sur la machine. Dans la webapp, une phrase dit où va la voix avant le premier usage,
  et la personne choisit.

### Demander, ou défaire ?

- **Gawande** : un accord qui revient à chaque geste devient un réflexe, et ne protège plus rien.
- **Norman** : là où l'on peut défaire, on fait, et on montre « Undo ».
- **Harris**, en réserve : « Undo » doit tout défaire, le projet et ce qu'il a créé autour (dossier, point 5).
- **Où l'on arrive** : ce qui se défait se fait, avec « Undo » sur la carte ; ce qui sort de la machine ou ne se reprend
  pas se demande, en mots (R46, R49).

### Où vit la banque ?

- **Jobs** : là où l'on décide : quand on refuse un résultat, et quand on change de modèle. Nulle part ailleurs.
- **Saarinen** : et la liste des cas reste un écran, pour qui veut la parcourir.
- **Où l'on arrive** : un refus porte une ligne, « Make this a test case » (workflow 8) ; le choix d'un modèle passe par
  le rejeu de la banque (workflow 9) ; Réglages > Test bank garde la liste, l'interrupteur et la règle (R71, R73).

## Recommandations `[HYPOTHÈSE]`

### R76. Une seule entrée sur chaque écran : écrire ou parler

- **Ce que c'est** : une barre en bas de chaque écran, la même partout. On y écrit ou on y parle pour demander n'importe
  quoi : créer un projet ou une issue, poser une question, confier une tâche à un agent. Elle remplace « Ask AI » et le
  bouton « Create issue » ; la conversation s'ouvre à droite, avec l'objet (R55).
- **Exemple** : sur la page d'un projet, Pierre appuie sur le micro et dit « Crée une issue pour la page de prix, pour
  vendredi ». Le texte s'écrit dans la barre ; il le relit et l'envoie ; Cortex prépare l'issue entière (R47).
- **Ce que ça change** : plus de menu à chercher. Sous la barre, trois suggestions selon l'écran disent ce qu'on peut
  demander (Norman, Zhuo). Les vues (board, liste, résultats) et les boutons sur leur objet restent (Saarinen).
- **Pas encore fait** : la barre n'existe que dans le panneau Cortex ; aucune voix dans le code (dossier, point 3).

- **Pour** : Jobs, Zhuo, Ait Si Abbou, Gawande.
- **Contre** : Saarinen, en réserve : la barre lance, elle ne remplace aucun écran. Norman, contradicteur : des
  suggestions ne valent pas un menu qu'on parcourt.
- **Preuve en dix jours** : dans la maquette, la Présidence crée un projet, une issue et pose une question, par la voix et
  par le texte, depuis trois écrans différents, sans ouvrir un menu.
- **Signal d'arrêt** : une action lancée par la voix sans que son texte ait été vu.

### R77. Ce qui se défait se fait ; ce qui ne se défait pas se demande

- **Ce que c'est** : Cortex fait tout de suite ce qui se défait dans l'espace (créer un projet, créer une issue), et la
  réponse porte « Undo ». Ce qui sort de la machine ou ne se reprend pas (pousser, fusionner, envoyer, supprimer) garde
  la demande d'accord.
- **Exemple** : « Create a project Recette 136 ». Le projet est créé, avec ses trois pages ; la carte dit « Project
  created · RECETTE136 · Undo ». Aujourd'hui, il attend « Approve and run ».
- **Ce que ça change** : moins de clics pour ce qui est sans risque, et des accords qui gardent leur sens (Gawande).
  « Undo » défait tout ce que l'action a créé, pages comprises (Harris).
- **Pas encore fait** : la règle `project.create` doit passer en `allow` (la Présidence l'a dit le 30/10) ; « Undo »
  n'existe pour aucune création de Cortex. La note suit le même chemin seulement si la Présidence le décide : la règle
  `propose-knowledge` la demande aujourd'hui.

- **Pour** : Norman, Gawande, Jobs, Zhuo, Saarinen.
- **Contre** : Harris, en réserve : si « Undo » laisse une trace, il vaut moins qu'un accord.
- **Preuve en dix jours** : un projet créé par la voix, puis défait : ni le projet ni ses pages ne restent.
- **Signal d'arrêt** : un « Undo » qui laisse quelque chose derrière lui.

### R78. Les trois écrans des retours, dessinés : créer, relire, accorder (R54)

- **Ce que c'est** : les trois écrans que la recette a touchés, dessinés une fois, à valider avant le code (R54).
  - **Créer** : le brouillon de Cortex dans la conversation, une carte modifiable. Le projet, le titre, la description,
    les sous-tâches et l'échéance sont remplis quand la demande les justifie ; la visibilité se choisit ; « Create issue »
    (R47).
  - **Relire** : la carte de résultat, sur l'issue, sous le titre (J3, R50) : le résultat, les contrôles de l'espace, ce
    qui changera, ce qui reste incertain, puis « Discard », « Try again », « Apply ». Pour du code, « Apply » fusionne par
    GitHub.
  - **Accorder** : la demande en mots (R46, R49) : ce que l'agent veut faire, pourquoi on demande, ce qui se passe si l'on
    refuse ; la commande à la demande ; « Allow for this mission » ou « Refuse » ; sans réponse, c'est non.
- **Exemple** : Claude Code veut chercher « electron-updater progress » sur le web pour TF-31. La demande dit que la
  requête sortira de l'ordinateur, et qu'en refusant il continue sans.
- **Ce que ça change** : la personne juge et accorde sur l'objet, sans ouvrir AI Workflows ni lire une commande brute.
- **Pas encore fait** : seuls existent « Agent done - ready for your review » et « Claude Code asks to run … » avec Allow
  et Deny (dossier, point 6).

- **Pour** : Jobs, Norman, Zhuo, Saarinen, Gawande, Ait Si Abbou.
- **Contre** : Norman, contradicteur, sur un point : « sans réponse, c'est non » doit dire après coup ce qui s'est passé,
  sinon le refus se fait en silence.
- **Preuve en dix jours** : la Présidence valide les trois dessins, puis une non-ingénieure lit trois demandes d'accord et
  dit ce que fait chacune.
- **Signal d'arrêt** : un écran construit avant que son dessin soit validé (R54).

### R79. La banque se montre au moment de décider (workflows 8 et 9)

- **Ce que c'est** : la banque apparaît à deux moments, et seulement là (R73).
  - **Un refus devient un cas (workflow 8)** : quand la personne refuse une proposition de Cortex, ou écarte un
    résultat, une ligne propose « Make this a test case ». Le brouillon reprend la raison du refus comme attendu.
  - **Changer de modèle passe par la banque (workflow 9)** : choisir un autre modèle propose d'abord de rejouer les cas ;
    on voit les cas gagnés et perdus, et les cas de sûreté, avant « Switch » ou « Keep ».
- **Exemple** : Cortex propose une note de type « TEST ». Pierre refuse : « TEST n'est pas un type de note ». La ligne
  propose d'en faire un cas : « la prochaine fois, un vrai type ». Plus tard, en essayant `qwen2.5:7b-instruct`, la
  banque montre que ce modèle perd ce cas-là.
- **Ce que ça change** : la banque se nourrit des erreurs sans écran de plus, et aucun modèle ne change sans elle.
- **Pas encore fait** : Cortex n'a pas de geste pour refuser une proposition (dossier, point 2) ; le registre des modèles
  par tâche n'existe pas (le lot suivant de R61). Les cas « à revoir » (R72) ne comptent pas dans le score affiché.

- **Pour** : Jobs, Zhuo, Norman, Gawande.
- **Contre** : Saarinen, en réserve : la liste des cas reste un écran qu'on parcourt, pas seulement des moments.
- **Preuve en dix jours** : dans la maquette, la Présidence passe d'une proposition refusée à un cas en deux gestes, et
  décide un changement de modèle en voyant les cas gagnés et perdus.
- **Signal d'arrêt** : un changement de modèle fait sans que la banque ait été montrée.

### R80. La voix reste sur la machine

- **Ce que c'est** : dans l'app desktop, la voix se transcrit sur l'ordinateur de la personne, sans service en ligne et
  sans coût (R62). Dans la webapp, avant le premier usage, une phrase dit où ira la voix ; la personne active la voix ou
  continue au clavier. Jamais d'écoute en fond, jamais de mot d'éveil.
- **Exemple** : dans l'app desktop, une puce « Audio stays on this computer » à côté du micro. Dans la webapp : « Your
  browser sends your voice to its speech service. Turn on voice, or keep typing. »
- **Ce que ça change** : parler à TaskForce ne fait sortir aucune parole sans que la personne le sache.
- **Pas encore fait** : tout. La transcription locale est une expérience à déclarer (E15) : vingt commandes en français et
  en anglais sur la machine de la Présidence, l'erreur par mot et le délai mesurés.

- **Pour** : Harris, Jobs, Ait Si Abbou, Norman.
- **Contre** : Saarinen, en réserve : la voix vient après la barre écrite ; elle ne doit pas retarder les trois écrans.
- **Preuve en dix jours** : E15 mesurée ; les vingt commandes comprises avec moins d'une erreur sur dix mots, en moins de
  deux secondes.
- **Signal d'arrêt** : une parole envoyée hors de la machine sans que la personne l'ait choisi.

## Décision de la Présidence

Le 30/10/2026 : « on pourrait ecrire et parler, comme ici quoi, on clique on maintiens pas et on reclique pour launch,
rien ne part temps que la personne envoie pas elle mm avec enree ou le boutton d envoie. Oui pour R77 R78 R79 R80 hmm nan
comme la webapp je suppose, ca nous servira pour entrainer les models right ? »

| Recommandation | Décision | Ce que la décision veut dire |
| --- | --- | --- |
| R76 | Retenue, modifiée | La voix démarre d'un clic sur le micro et s'arrête d'un second clic, sans appui maintenu. Rien ne part tant que la personne n'envoie pas elle-même, avec Entrée ou le bouton d'envoi |
| R77 | Retenue | Ce qui se défait se fait, avec « Undo » ; ce qui ne se défait pas se demande |
| R78 | Retenue | Les trois écrans des retours : créer, relire, accorder |
| R79 | Retenue | La banque au refus d'une proposition (workflow 8) et au changement de modèle (workflow 9) |
| R80 | Non retenue telle quelle, à préciser | La Présidence préfère la voix « comme la webapp », et demande si elle servira à entraîner des modèles. Le secrétariat répond ci-dessous ; la Présidence choisit ensuite |

### Seconde décision : la voix, et les questions laissées ouvertes

Le 30/10/2026, après la réponse du secrétariat (ci-dessous) : « R80 choix 1 / La duree du undo tant que rien n'a bouge. /
La note comme un projet / Les libelles tu gardes, et go release ».

| Point | Décision | Ce que la décision veut dire |
| --- | --- | --- |
| R80 | Retenue telle quelle | Le premier des trois choix posés par le secrétariat : dans l'app desktop, la voix se transcrit sur l'ordinateur ; dans la webapp, elle passe par le service du navigateur, et une phrase le dit avant le premier usage. Les deux autres choix étaient le navigateur partout, ou notre propre transcription partout. Rien n'est entraîné sur la voix (R61) |
| La durée de « Undo » (R77) | Tant que rien n'a bougé | Un projet sans issue ni page ajoutée, une issue sans commentaire, une note sans page rangée dessous ni lien d'une autre note vers elle. Au-delà, un message dit pourquoi, et l'objet reste |
| La note | Comme un projet | Cortex écrit tout de suite la note qu'on lui demande, et la réponse porte « Undo ». Réécrire une note qui existe reste demandé |
| Les libellés de la maquette | Gardés | « Workspace » et « Collaborators only » pour la visibilité d'une issue (créer) ; « Apply » sur la carte de résultat (relire) |


- **Ordre de parole** tiré au sort le 29/10/2026 à 23:15 UTC (`shuf`). Contradicteur désigné : Don Norman.
- **La maquette** est dessinée par le secrétariat depuis le tour de table, la carte et le code du 30/10/2026. Les
  libellés anglais sont des propositions, à relire pour le glossaire de R22 ; les annotations, en français, disent ce qui
  existe et ce qui est proposé.
- **L'ordre de Jobs tient** : rien ici n'ajoute de file de cas proposés ni d'outil MCP (séance n°12). La barre remplace
  deux entrées existantes au lieu d'en ajouter une.
- **Une source à vérifier** : la reconnaissance vocale de Chrome par un serveur (dossier, point 9) ; elle ne fonde que
  R80, qui tient même si la source tombe.

- **La réponse du secrétariat sur la voix et l'entraînement** (30/10/2026), pour la décision sur R80 :
  - `[ÉTABLI]` R61 (séance n°10, retenue) : aucun entraînement dans TaskForce cette année ; R64 : ce qui est possédé
    part avec le client. Les données d'un espace sont celles de l'entreprise, pas celles de TaskForce.
  - `[ÉTABLI]` Dans la webapp proposée par R80, la voix passe par le service de reconnaissance du navigateur : TaskForce
    ne reçoit que le texte, comme quand la personne tape. Cette voie ne donne aucun enregistrement à TaskForce.
  - `[DÉDUIT]` Garder des enregistrements pour entraîner un modèle demanderait de faire passer la voix par nos serveurs
    (un coût, contre R62), et le consentement explicite de chaque personne pour cette finalité, avec une analyse
    d'impact (RGPD) : la voix est une donnée personnelle.
  - `[ÉTABLI]` Ce qui nourrit déjà la boucle de R61 : le texte des demandes et ce qui a suivi, gardés au dossier de chaque
    réponse ; la banque de tests en tire ses cas.
  - À vérifier : la reconnaissance du navigateur dans l'app desktop (Electron), qui n'est pas celle de Chrome.

## Suites

1. **La Présidence valide les dessins** (R54) : l'arrivée avec la barre, créer, relire, accorder, et la banque aux deux
   moments.
2. **Construire, dans l'ordre** : la barre écrite sur chaque écran (R76) et « Undo » avec la règle `project.create`
   (R77) ; les trois écrans (R78) ; le refus dans Cortex et la banque aux deux moments (R79).
3. **La voix** : R80 retenue le 30/10/2026 ; E15 se déclare, puis la voix entre dans la barre sans retarder les trois
   écrans (réserve de Saarinen).
4. **Ensuite** : le registre des modèles par tâche (R61), puis l'export (R64).
