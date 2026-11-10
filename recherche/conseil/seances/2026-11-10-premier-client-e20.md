---
id: conseil-seance-2026-11-10-premier-client-e20
title: "Séance n°21 du 10/11/2026 : où en est la première version qu'une entreprise peut utiliser, et E20, le premier client joué de bout en bout"
doc_type: pv-seance
statut: active
date: "10/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, roadmap, e20, entreprise, audit, macos]
related:
  - "../README.md"
  - "./2026-11-01-feuille-de-route.md"
  - "./2026-11-09-atelier-recette-113.md"
  - "../../experiences/Experiences.md"
  - "../../Questions-ouvertes.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°21 du 10/11/2026 : la première version qu'une entreprise peut utiliser, et E20

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

La release 1.14.0 et l'app desktop 1.11.0 sont en production depuis ce matin. J1 est livré : entre le 05/11 et le 10/11, cinq
releases ont porté un seul moteur en Java, la passerelle de modèles, les gestes du chat, la fenêtre, le banc, la voix, le contexte
selon le modèle et la passe UI/UX de la séance n°20. J2, la boucle complète mais mince, n'a pas commencé.

La Présidence redéfinit E20 : c'est le test qui dira « on a une application qu'on peut vendre ». Une entreprise, son outil de base,
un nouveau module à intégrer. TaskForce connaît l'outil, sa documentation, son environnement, ses contraintes et ses processus, et
aide tout le travail « de manière réglementée, de manière tracée, de manière auditable, et surtout en évitant de faire des erreurs
bêtes ».

Le Conseil partage cette vision et la rend mesurable :
- E20 devient le premier client joué de bout en bout, avec des critères écrits avant, un lecteur extérieur du dossier et un
  contre-essai : trois tâches refaites par le même agent sans TaskForce, pour voir ce qu'il évite (Esther Duflo, contradictrice).
- L'outil de base de l'essai est d'abord un logiciel de gestion public, qu'on peut rejouer et faire juger, puis l'outil réel du
  premier client possible, comme pilote. Jeff Bezos n'a voté qu'après l'ajout d'un entretien avec ce client avant E20.
- La première version pour une entreprise n'est pas un nouveau jalon : c'est J2 remis dans l'ordre d'E20, le contexte de
  l'entreprise et la fiche de son environnement d'abord.
- Les erreurs bêtes se préviennent par des listes courtes à trois moments et, mieux encore, par des contraintes (Atul Gawande,
  Don Norman).
- Hors du produit : le VPS avant le 31/12/2026, sans quoi plus aucune installation ne se connecte ; les données du client chez lui ;
  un accord d'une page.
- macOS : une version non signée seulement si le premier client travaille sur Mac ; l'adhésion d'Apple au premier contrat payé.
- J1 se ferme sur « continuer ». J2 est estimé à trois ou quatre semaines `[HYPOTHÈSE]`, ce qui place E20 dans la seconde quinzaine
  de décembre.

Sept recommandations, R145 à R151, à l'unanimité des sept, R145 et R146 au second tour.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 10/11/2026, en conversation, après la release 1.14.0) :
  - « concrètement, on en est où? Fais un petit tour avec le conseil aussi, j'aimerais voir où on en est dans la roadmap pour notre
    première version prête à l'emploi par une entreprise » ;
  - sur E20 : « Pour moi, c'est le test qui viendra vraiment quand tu me diras « Ok, là, on a une application qu'on peut vendre, on
    peut aller voir un client avec ça, lui proposer l'application. » » ; « J'imagine qu'on est une entreprise, […], par exemple,
    hein, […], qui pourrait potentiellement être notre premier client, du coup, d'ailleurs. Et puis tester vraiment sur un vrai
    projet. » ;
  - le scénario : « bon bah on a un nouveau module à intégrer sur notre outil de base. Taskforce est censé connaître l'outil de
    base, avoir les documentations, avoir tout l'environnement, setup et tout ça. On crée un nouveau projet intégration nouveau
    module, et c'est parti, on commence notre travail, et l'app doit vraiment nous aider dans tout le process de création, mais
    vraiment de manière réglementée, de manière tracée, de manière auditable, et surtout en évitant de faire des erreurs bêtes,
    justement parce qu'elle connaît l'environnement, elle connaît l'outil, elle connaît les documentations, elle connaît les
    contraintes, elle connaît les process » ;
  - la demande au Conseil : « Si t'as la même vision que moi là-dessus, et si le conseil a la même vision que moi là-dessus, bien
    évidemment, ce sera à faire passer au conseil. Il faut vraiment que le conseil discute d'un vrai projet, d'un test, d'un vrai
    test à faire sur cette base-là. » ;
  - sur macOS : « normalement avec le .exe ca devrait fonctionner quand mm nan sur MacOS ? J'imagine same thing avec les antivirus
    mais on s'en sort quoi, parce que temps que je suis pas paye je veux pas passer la certif IoS qui coute un bras pour pouvoir
    publier quelque chose sur l'Apple store ».
- **Horizon** : la première version qu'une entreprise peut utiliser, et le test qui le prouve.
- **Formation** : restreinte (7), au moins un membre par pôle.
  - Impulsion : Jeff Bezos (le client comme juge final).
  - Pont : Satya Nadella (les agents en entreprise, la gouvernance par les traces) ; Kenza Ait Si Abbou (l'adoption dans une
    entreprise qui ne fait pas du logiciel).
  - Harmonie : Margrethe Vestager (la règle, et la preuve qu'elle s'applique).
  - Science : Atul Gawande (les listes et les points de pause) ; Esther Duflo (la preuve causale).
  - Design : Don Norman (l'erreur humaine, et le défaut de conception derrière elle).
- **Ordre de parole**, tiré au sort à 14:17 UTC : Jeff Bezos, Esther Duflo, Satya Nadella, Atul Gawande, Margrethe Vestager, Don
  Norman, Kenza Ait Si Abbou.
- **Contradictrice** : Esther Duflo.
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à sept.
- **Fiches** : à jour (moins de 30 jours) : Norman au 28/10/2026, Ait Si Abbou au 26/10, Bezos, Nadella, Vestager, Gawande et Duflo
  au 21/10. Aucune fiche rafraîchie.

## Dossier

### 1. Où en est la feuille de route `[ÉTABLI]`

Sources : [Roadmap_Backlog](../../../v1/13-roadmap/Roadmap_Backlog.md) §0, le PV de la [séance n°15](./2026-11-01-feuille-de-route.md).

| Jalon | Ce qu'il donne | Prévu le 01/11 | État au 10/11/2026 |
| --- | --- | --- | --- |
| J0 Dire vrai, fermer les failles | Les droits de la recherche, « Apply » qui respecte les tests, les pages vraies, R78 publiée | 1 semaine | Fait ; reste TF-J0-4 (l'ADR-010 et l'ADR-021) |
| J1 Un seul moteur, un desktop qui tient seul | Décision, preuve et passerelle en Java ; plus de Python ni de doublon TypeScript | 2 à 3 semaines | En production le 10/11 (1.10.0 à 1.14.0) : TF-J1-1 à TF-J1-8 faits ; TF-J1-9 à TF-J1-20 en production, pas encore vus par la Présidence sur la dernière version ; E18 et E19 pas finies. L'app desktop se connecte toujours par la webapp (Présidence, 01/11) |
| J2 La boucle complète, mince | Processus modifiable, agents, règles éditables, documents cités, vue du travail, dossier signé, un échec devient un cas ; deux packs | 4 à 5 semaines | Pas commencé (TF-J2-1 à TF-J2-8) |
| J3 à J9 | Le métier construit son outil, le contexte complet, des agents robustes, les données souveraines, l'amélioration continue, la démo complète, la mise sur le marché | 22 semaines environ | Pas commencés |

Le calendrier indicatif du 01/11, `[HYPOTHÈSE]` à recaler à la fin de J1 : la démo mince vers le début de janvier 2027, la démo
complète vers la fin de mai 2027, la mise sur le marché en juin 2027.

### 2. Ce que la release du jour a prouvé `[ÉTABLI]`

- La release 1.14.0 (#519) est en production depuis 13:28 UTC : l'API redémarrée répond, donc les migrations V122 et V123 sont
  passées ; la webapp affiche 1.14.0 ; l'app desktop 1.11.0 est publiée, analyse de VirusTotal comprise.
- La liste de lancement de 1.10.0 à 1.11.0, sur un Windows neuf (run 42826392412) : installation, premier démarrage jusqu'à la
  connexion, mise à jour qui garde la base intégrée, ordinateur sans la runtime Visual C++, désinstallation.

### 3. Le scénario de la Présidence, face au produit

| Ce que la Présidence attend | Ce qui existe au 10/11 `[ÉTABLI]` | Ce qui est prévu |
| --- | --- | --- |
| « connaître l'outil de base, avoir les documentations » | Cortex lit les notes du Brain OS et dit sous sa réponse ce qu'il a lu ; l'agent (Claude Code, par le runner) travaille dans le dépôt du projet, cloné sur la machine | Des documents importés avec version, responsable et date de validité, cités au passage près (TF-J2-5) ; tous les formats, les droits, la recherche hybride (J4) |
| « avoir tout l'environnement, setup et tout ça » | Pas de fiche d'environnement du projet validée par une personne : l'agent relit le dépôt à chaque mission `[DÉDUIT]` | Rien d'écrit |
| « de manière réglementée » | Des règles dans le moteur Java (R90), une par geste (`delete-issue`), écrites dans le code ; des accords morceau par morceau (TF-J0-6) | Des règles écrites par l'entreprise (TF-J2-4) ; un processus modifiable (TF-J2-2) |
| « de manière tracée » | L'activité dit qui a fait quoi (TF-J0-7) ; la mission garde ses étapes, ses changements fichier par fichier et ses commandes (TF-J1-16, TF-J1-17) | Le journal des actions d'IA (TF-J2-7) |
| « de manière auditable » | « Apply » respecte les tests, et passer outre laisse sa raison au dossier (TF-J0-2) | Un dossier signé, qui survit à la suppression et se vérifie sans TaskForce (TF-J2-7) ; la preuve d'auditeur (J6) |
| « en évitant de faire des erreurs bêtes » | Cortex demande ce qui manque, en choix (R115), dit ce qui a été fait (R116), écrit son plan (R117) ; un échec devient un cas de la banque (R118) | L'agent qui demande (J4) ; le vérificateur indépendant (J5) |

### 4. Les contraintes du terrain `[ÉTABLI]`

- **L'hébergement** ([Q13](../../Questions-ouvertes.md#q13--les-moyens-de-la-direction--lhébergement-le-temps-un-partenaire-la-source-du-texte)) :
  les machines de l'école s'arrêtent le 31/12/2026 ; l'app desktop se connecte par la webapp ; la date du VPS n'est pas fixée. Sans
  lui, une nouvelle installation ne pourra plus se connecter après cette date.
- **Les mots de la cible** (R65, d'après la Présidence) : audit, traçabilité, IQ, OQ, PQ, réglementation, référentiel.
- **La distribution** : chaque release publie l'installeur Windows, non signé, et les paquets Linux (deb, AppImage) ; la version du
  Microsoft Store se construit (`dist:store`) mais n'est pas publiée ; il n'existe pas de version macOS.
- **macOS**, lu le 10/11/2026 :
  - un `.exe` est un programme pour Windows : macOS ne l'exécute pas. Il faut une version construite pour le Mac, avec la base
    intégrée, le JRE et la voix compilés pour lui ;
  - l'adhésion au programme des développeurs d'Apple coûte 99 dollars par an ; elle donne l'identifiant de développeur et la
    notarisation, pour distribuer hors du Mac App Store ([Apple](https://developer.apple.com/programs/)) ;
  - sans notarisation, la personne ouvre l'app une première fois par Réglages Système, Confidentialité et sécurité, « Ouvrir quand
    même », dans l'heure qui suit l'essai et avec son mot de passe ; l'app devient ensuite une exception
    ([Apple](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unknown-developer-mh40616/mac)) ;
  - la mise à jour automatique d'Electron exige une app signée : « Your application must be signed for automatic updates on macOS »
    ([Electron](https://www.electronjs.org/docs/latest/api/auto-updater)).

### 5. Notes de la Présidence du 10/11/2026, tranchées, hors débat

- **La runtime Visual C++** : « je pense qu'il faut qu'on l'installe en même temps, hein, parce que sinon c'est ultra chiant que
  l'utilisateur ait encore quelque chose à télécharger quand il arrive sur l'application ». C'est le cas depuis l'app desktop 1.10.0
  (#501), et la liste de lancement l'a prouvé encore aujourd'hui sur un ordinateur sans la runtime.
- **Le logo de Claude** : « Le logo Anthropic est open source, on peut l'utiliser sans problème. » ; « C'est juste un logo
  d'information, donc il n'y a pas de problème à ce niveau-là. » Q12 est tranchée : aucune demande à Anthropic. Le logo est dans
  l'app depuis la 1.14.0 (#513).
- **Le site** : « Faudra mettre a jour le site web aussi mais ca on fera plus tard egalement vraiment a la fin, quand la version
  desktop, et microsoft store seront publiees. »
- **Les dépendances** : « on checkera sur la release final je pense si on peut mettre tout ca a jour sauf les 7 high on pourrait les
  passer sur la prochaine release ». Les correctifs des sept alertes graves de Dependabot partent avec la prochaine release, le reste
  à la release finale.

## Tour de table `[HYPOTHÈSE]`

- **Jeff Bezos** (Impulsion) : on part du client et on remonte. Avant de construire J2, on écrit le communiqué du jour où le premier
  client signe, et sa foire aux questions : qu'est-ce que l'entreprise aura de plus le lundi matin ? TF-J2-1 le prévoit déjà ; il
  passe en premier. Et l'essai doit porter sur le vrai outil d'un vrai client, sinon on teste l'idée qu'on se fait du client. *Sa
  recommandation : le communiqué d'abord, et le premier client possible interrogé avant E20.*
- **Esther Duflo** (Science, contradictrice) : un essai conçu, joué et jugé par la personne qui a construit l'outil prouve surtout
  qu'elle sait s'en servir. La question de la Présidence est causale : TaskForce évite-t-il des erreurs qu'on ferait sans lui ? Il
  faut un témoin : les mêmes tâches, le même agent, sans le contexte, sans les règles, sans les listes. Et des indicateurs fixés
  avant de commencer. *Sa recommandation : un contre-essai, des critères écrits avant, un juge qui n'a pas construit l'outil.*
- **Satya Nadella** (Pont) : une entreprise n'adopte pas un agent, elle adopte un système de contrôle. Les contrôles vivent hors du
  modèle, le journal se lit sans l'agent, et quelqu'un peut arrêter une tâche en cours et le prouver. Le dossier signé de TF-J2-7
  n'est pas un luxe de J6 : c'est ce qu'un premier client demandera le premier jour. *Sa recommandation : le dossier signé et
  vérifiable dans la première version.*
- **Atul Gawande** (Science) : les erreurs bêtes ne viennent pas de l'ignorance, elles viennent de l'oubli sous la charge : la
  mauvaise commande, le test oublié, la convention qu'on connaissait pourtant. Une liste courte, à quelques moments où l'erreur coûte
  cher, tirée des processus de l'entreprise, les attrape. Une liste longue se coche sans se lire. *Sa recommandation : trois points
  de pause, moins de dix lignes chacun, et la mesure de ce qu'ils attrapent.*
- **Margrethe Vestager** (Harmonie) : « réglementé » veut dire que la règle exécutée est celle que l'entreprise a adoptée, et que
  quelqu'un d'extérieur peut le vérifier. Aujourd'hui les règles sont dans le code de TaskForce : c'est TaskForce qui règle
  l'entreprise, pas l'inverse. Et les données du client : où vont-elles, qui les voit, peut-il partir avec ? *Sa recommandation :
  des règles écrites par l'entreprise, et un accord d'une page avec le premier client sur ses données.*
- **Don Norman** (Design) : une erreur bête est une erreur de conception que personne n'a encore vue. La plupart sont des ratés : on
  sait ce qu'il faut faire, et on fait autre chose. Contre un raté, une liste aide peu ; une contrainte aide beaucoup : la commande
  de test est celle de la fiche, pas celle que l'agent imagine ; une branche protégée ne se touche pas. Et la personne doit voir ce
  que l'agent croit de l'environnement, pour le corriger avant qu'il agisse. *Sa recommandation : rendre impossibles les erreurs qui
  peuvent l'être, et rendre visible ce que l'agent sait de l'environnement.*
- **Kenza Ait Si Abbou** (Pont) : dans une entreprise qui ne fait pas du logiciel, l'outil de base est souvent un logiciel acheté
  puis adapté ; la connaissance est dans la tête de deux personnes et dans des documents qui se contredisent. L'essai doit garder ce
  désordre, et faire entrer une personne du métier qui ne code pas et doit comprendre ce qu'elle valide. Et une question simple au
  client : sur quelles machines travaillez-vous ? *Sa recommandation : le premier client possible interrogé tôt, ses documents tels
  qu'ils sont, et quelqu'un du métier dans l'essai.*

## Confrontation `[HYPOTHÈSE]`

1. **Le vrai client tout de suite, ou un essai qu'on peut rejouer ?** Bezos veut l'outil réel du premier client possible : c'est lui
   qui décidera d'acheter. Duflo répond qu'un essai sur un code privé ne se rejoue pas, ne se publie pas et ne se juge pas de
   l'extérieur, et qu'un client qui voit un premier essai raté ne revient pas. Ait Si Abbou déplace la question : il faut connaître
   l'outil réel du client avant de choisir son double. Accord (R146, second tour) : un entretien avec le premier client possible
   avant E20 ; E20 sur un logiciel de gestion public, choisi au plus près de son cas ; puis son outil réel, avec son accord, comme
   pilote.
2. **Un essai joué par celui qui a construit l'outil.** Duflo vote contre le premier texte de R145 (6 pour, 1 contre) : sans témoin
   ni critère fixé avant, E20 mesurerait le talent de la Présidence. Gawande défend la mesure avant et après, moins coûteuse qu'un
   tirage au sort. Accord : trois tâches du module refaites par le même agent sans TaskForce, la liste des erreurs bêtes écrite avant,
   et le dossier lu par quelqu'un qui ne connaît pas TaskForce.
3. **Ce qu'une entreprise exige le premier jour, contre le travail lui-même.** Nadella et Vestager veulent le dossier signé, les
   règles de l'entreprise et l'accord sur les données avant tout client. Norman et Gawande craignent une première version qui prouve
   tout et n'aide à rien. Accord (R147) : J2 garde tout son contenu, mais dans l'ordre du scénario ; le contexte et l'environnement
   d'abord, parce que sans eux il n'y a rien à prouver ; le dossier signé avant E20.
4. **macOS.** Ait Si Abbou rappelle que les petites entreprises ont souvent des parcs mélangés. Bezos refuse de construire pour un
   besoin qu'aucun client n'a encore exprimé. Nadella voudrait la version Mac dès J2, pour ne fermer aucune porte ; il vote R150 en le
   disant. Accord : la question va au premier client ; une version non signée seulement s'il travaille sur Mac.
5. **La vitesse de J1 vaut-elle pour J2 ?** Bezos lit neuf jours au lieu de deux à trois semaines, et veut avancer la démo. Duflo
   répond qu'une vitesse mesurée sur des écrans et des corrections ne dit rien d'un moteur durable ni d'une signature. Accord (R151) :
   J2 estimé à trois ou quatre semaines, recalé à la fin de sa première semaine sur ce qui est vraiment fini.

## Recommandations `[HYPOTHÈSE]`

### R145. E20, le premier client joué de bout en bout (second tour)

- **Quoi** : E20 devient le test qui dit « on peut aller voir un client ». La Présidence joue une entreprise : son outil de base,
  avec son code, sa documentation et son environnement ; un projet « Intégrer un nouveau module », mené de bout en bout dans
  TaskForce, de la demande à la livraison.
  - Écrits avant le début : ce que TaskForce doit savoir de l'outil avant la première mission, vérifié par dix questions dont on
    connaît la réponse ; la liste des erreurs bêtes guettées (une commande qui n'est pas celle du projet, la mauvaise branche, une
    convention ignorée, un test oublié, une documentation contredite, un accord sauté, une information inventée) ; les seuils de
    réussite.
  - Mesurés pendant et après : les sorties de l'outil ; les erreurs bêtes évitées et commises ; la part des résultats acceptés sans
    reprise ; le dossier, lu par une personne qui ne connaît pas TaskForce et qui doit dire qui a décidé quoi, sur quelle base.
  - Le contre-essai : trois tâches du module refaites par le même agent, sur le même modèle, sans le contexte, les règles ni les
    listes de TaskForce.
- **Premier tour** (sans contre-essai ni lecteur extérieur) : 6 pour, 1 contre (Duflo). **Second tour**, amendé : les sept.
- **Preuve en dix jours** : le protocole écrit et relu par la Présidence, avec la liste des erreurs bêtes et les dix questions.
- **Signal d'arrêt** : le contre-essai ne montre aucune erreur évitée sur les trois tâches. La promesse n'est pas tenue : on ne va
  voir aucun client avant de comprendre pourquoi.

### R146. L'outil de base de l'essai (second tour)

- **Quoi** :
  1. avant E20, un entretien avec le premier client possible : son outil de base (acheté, adapté ou écrit chez lui), ses documents,
     ses machines, ses règles, ce qu'il accepterait de montrer ;
  2. E20 sur un logiciel de gestion public utilisé par des PME, choisi au plus près de son cas : un vrai code, une vraie
     documentation et de vraies conventions ; un essai qu'on peut rejouer, publier et faire juger par un connaisseur de ce logiciel ;
  3. ensuite, avec l'accord écrit du client, le même scénario sur son outil réel, comme pilote, sur des modèles locaux : rien ne sort
     de sa machine.
- **Premier tour** (le logiciel public, sans entretien) : 6 pour, 1 contre (Bezos). **Second tour**, amendé : les sept.
- **Preuve en dix jours** : l'entretien a eu lieu ; le logiciel public est choisi, avec sa raison.
- **Signal d'arrêt** : le client n'a ni logiciel ni documents à faire évoluer. Le scénario « nouveau module » ne lui parle pas, et le
  pilote change de forme avant E20.

### R147. La première version pour une entreprise : J2, dans l'ordre d'E20

- **Quoi** : pas de nouveau jalon. J2 garde son contenu et se construit dans l'ordre du scénario :
  1. le communiqué et sa foire aux questions (TF-J2-1), écrits pour le premier client ;
  2. le contexte de l'entreprise (TF-J2-5) : le dépôt et la documentation de l'outil importés, avec version, responsable et date,
     cités au passage près ;
  3. la fiche d'environnement du projet : installer, construire, tester, lancer ; les conventions ; ce qu'on ne touche pas. TaskForce
     la propose depuis le dépôt, une personne la valide, chaque mission la lit ; elle reste visible et corrigeable ;
  4. le processus « intégrer un module » (TF-J2-2) : cadrage, spécification, découpage, réalisation, tests, revue, recette,
     livraison, et qui accorde chaque étape ;
  5. les règles écrites par l'entreprise (TF-J2-4) ;
  6. le dossier signé, vérifiable sans TaskForce (TF-J2-7) ;
  7. la vue du travail et les agents, en version mince (TF-J2-6, TF-J2-3).

  Le second pack (rédaction et revue de document, TF-J2-8) passe après E20, sauf si le premier client en a besoin.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : le contexte importé sur le logiciel choisi, et les dix questions de R145 : au moins huit réponses
  justes, avec le passage cité.
- **Signal d'arrêt** : moins de huit réponses justes et citées. Le contexte n'est pas prêt, et E20 attend.

### R148. Les erreurs bêtes, prévenues avant d'arriver

- **Quoi** : trois points de pause, avant de lancer une mission, avant d'appliquer, avant de livrer, chacun avec une liste de moins
  de dix lignes tirée du processus, des règles et de la fiche d'environnement. Ce qui peut être rendu impossible l'est, plutôt que
  d'être écrit dans une liste : la commande de test est celle de la fiche ; une branche protégée ne se touche pas ; un accord qui
  manque bloque. Chaque erreur bête vue en E20 devient un cas de la banque (R118).
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : trois missions sur le logiciel choisi, où au moins deux erreurs semées exprès sont attrapées avant
  d'arriver.
- **Signal d'arrêt** : une liste cochée sans être lue, ce que dit le temps passé dessus. On la raccourcit, ou on la remplace par une
  contrainte.

### R149. Ce qui conditionne un premier client, hors du produit

- **Quoi** :
  1. le VPS en service avant le 31/12/2026, avec les comptes, la webapp, l'API et les sauvegardes ; sa date est à fixer par la
     Présidence (Q13) ;
  2. les données du client restent chez lui : des modèles locaux par défaut pour le pilote, et une page qui dit ce qui sort et vers
     où ;
  3. un accord d'une page avec le client pilote : ce que TaskForce lit, ce qui sort, qui voit le dossier, comment il part avec ses
     données ;
  4. la distribution : l'installeur Windows et le Microsoft Store d'abord, le site mis à jour en dernier (note de la Présidence) ;
     macOS selon R150.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : la date du VPS ; l'accord en une page, relu par la Présidence.
- **Signal d'arrêt** : pas de VPS au 15/12/2026. Il faut alors que l'app desktop se connecte sans la webapp, sinon aucune
  installation ne marche après le 31/12.

### R150. macOS, sans payer Apple tant qu'aucun client ne paie

- **Quoi** : la question va au premier client (R146). S'il travaille sur Mac : une version non signée pour les Mac à puce Apple,
  avec la base intégrée, le JRE et la voix construits pour eux ; la page de téléchargement dit comment l'ouvrir la première fois ;
  l'app signale les nouvelles versions et renvoie au téléchargement, puisque la mise à jour automatique exige une signature.
  L'adhésion d'Apple se prend au premier contrat payé, comme la Présidence le pose. Sinon, macOS attend la fin d'E20.
- **Pour** : les sept ; Nadella l'aurait voulue dès J2. **Contre** : aucun.
- **Preuve en dix jours**, si le client travaille sur Mac : une version qui démarre jusqu'à la connexion sur une machine macOS de
  la CI, avec la base intégrée.
- **Signal d'arrêt** : la base intégrée ou la voix ne démarre pas sur macOS sans signature. macOS attend alors l'adhésion.

### R151. J1 se ferme : continuer

- **Quoi** : le Conseil juge J1 selon R105, et dit « continuer ».
  - Fait : le contenu de J1, en production ; les tests verts ; la liste de lancement verte aujourd'hui ; la recette de la Présidence
    (09/11) et ses corrections.
  - Réserves : TF-J1-9 à TF-J1-20 pas encore vus par la Présidence sur la 1.14 ; E18 et E19 pas finies ; les personnes extérieures
    et l'indice de confiance commencent à J2 (R105, E17).
  - Le calendrier se recale : J2 estimé à trois ou quatre semaines `[HYPOTHÈSE]` au lieu de quatre à cinq, ce qui place E20 dans
    la seconde quinzaine de décembre, avant l'échéance de l'hébergement ; la démo complète et la mise sur le marché ne bougent pas
    tant que la vitesse de J2 n'est pas connue.
- **Pour** : les sept ; Duflo note qu'une vitesse mesurée sur des écrans ne dit rien d'un moteur durable. **Contre** : aucun.
- **Preuve en dix jours** : à la fin de la première semaine de J2, la part de J2 vraiment finie, à comparer à un quart.
- **Signal d'arrêt** : moins d'un quart de J2 fini à la fin de sa première semaine. On revient à cinq semaines, et E20 glisse en
  janvier.

## Décision de la Présidence

En attente. Le secrétariat lui demande de trancher R145 à R151 : retenue, à l'essai, écartée ou reportée, avec sa raison, dans ses
mots.

## Notes du secrétariat

- **Le nom de l'entreprise** citée par la Présidence comme premier client possible, et son lien avec elle, sont retirés des
  citations (« […] ») : ce dépôt est public.
- **E20 change de définition.** La séance n°20 l'avait ouverte comme un vrai projet dans un domaine que la personne ne connaît pas ;
  la Présidence la redéfinit le 10/11. Le domaine inconnu demeure : c'est le métier de l'entreprise jouée.
- **Le logo** : Q12 se ferme sur la décision de la Présidence. Le dossier garde ce que le secrétariat avait lu le 29/10/2026 : les
  conditions d'Anthropic n'autorisent ses marques que sans parrainage ni affiliation sous-entendus ; l'usage que décrit la
  Présidence est un logo d'information, sans communication commerciale. La note de la séance n°20, qui parlait d'une autorisation
  écrite, est retirée.
- **La runtime Visual C++** : la note de la séance n°20 (« à vérifier ») est close par la décision de la Présidence ; l'installeur
  la porte depuis la 1.10.0.
- **Conflits d'intérêts** : Nadella dirige Microsoft, éditeur de Windows, du Microsoft Store et de GitHub, sur lesquels repose la
  distribution discutée. Le secrétariat est tenu par un modèle d'Anthropic, dont le logo est en question : la décision est celle de
  la Présidence.
- **Les durées** de J2 et la date d'E20 sont des `[HYPOTHÈSE]`.

## Suites

- Le PV au registre (§12) et au Journal.
- À [Experiences.md](../../experiences/Experiences.md) : E20 redéfinie par la Présidence ; son protocole (R145, R146) attend sa
  décision.
- À [Questions-ouvertes.md](../../Questions-ouvertes.md) : Q12 tranchée ; Q13 garde la date du VPS à fixer (R149) ; Q16 ouverte,
  macOS.
- Après la décision de la Présidence : J1 fermé à la roadmap ; les lignes de J2 remises dans l'ordre de R147, avec la fiche
  d'environnement et les points de pause en lignes à elles.
- La prochaine release porte les correctifs des alertes graves de Dependabot (note de la Présidence).

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- La Présidence et le Conseil voient la même chose : la valeur de TaskForce n'est pas dans ses écrans, elle est dans ce qu'il sait
  de l'entreprise et dans ce qu'il empêche. E20, avec son contre-essai, est le premier test qui mesure cela plutôt que l'interface.
- Le plus gros morceau est le contexte (R147, points 2 et 3) : aujourd'hui TaskForce lit des notes et un dépôt ; connaître un outil
  avec sa documentation, ses versions et ses contraintes, c'est du travail neuf.
- Le risque caché est l'hébergement : sans VPS au 31/12, même un client convaincu ne pourra pas installer.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
