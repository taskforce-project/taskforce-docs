---
id: conseil-seance-2026-10-28-atelier-design
title: "Séance n°6 du 28/10/2026 : l'atelier design (Cortex, les flows, la carte de résultat)"
doc_type: pv-seance
statut: active
date: "28/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, cortex, carte-de-resultat, flows, test]
related:
  - "../README.md"
  - "./2026-10-28-revue-spec-v2.md"
  - "./2026-10-28-trajectoire-harnais.md"
  - "./2026-10-27-menage-spec-v2.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°6 du 28/10/2026 : l'atelier design (Cortex, les flows, la carte de résultat)

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle, et les décisions de Jobs sont celles d'un personnage simulé.

## Résumé

L'atelier design répond aux quatre questions de la Présidence. Cortex est utile et devient l'endroit où l'on demande et
où l'agent rend compte, à deux conditions : savoir ce qui est ouvert, et ne plus disparaître sous la fiche de l'issue. On
n'y décide pas : la décision se prend sur la carte de résultat, une seule, sur l'issue, où mènent Cortex et Signals. Jobs
classe douze flows selon la promesse : juger le résultat, puis confier et suivre, puis répondre à une demande, puis
demander. La carte est dessinée, zones, états et gestes : les trois gestes de R22 et un non, « Écarter », de même poids
qu'« Appliquer », puis « Défaire ». Le parcours de test de la Présidence tient en vingt-deux étapes, l'app desktop
d'abord, et annonce les défauts déjà connus. Désaccords conservés : Saarinen, contradicteur, refuse un chat comme surface
par défaut ; Zhuo voulait la carte dans le fil, et Zhuo comme Saarinen classent les flows autrement ; Jobs et Harris
refusent le palier d'autonomie à l'écran.

- **Saisine** (Présidence, 28/10/2026) : quatre questions à l'atelier design du Conseil.
  1. Cortex, l'assistant conversationnel de l'app, est-il utile ? Deviendrait-il le moyen de communication avec
     l'utilisateur, la surface principale : par où l'on demande, où l'agent rend compte, où la personne décide ?
  2. Quels sont les flows de l'app, du plus important au moins important ? Jobs tranche le classement.
  3. La carte de résultat (R13) : ce qu'elle montre, les trois gestes (R22), la délégation visible (R26), le mode dégradé
     (R23), dessinés en texte.
  4. Ce que la Présidence doit tester, dans l'app desktop et dans la webapp : un parcours concret, dans l'ordre, avec ce
     qu'elle doit voir et ce qui serait un échec.
  Horizon, lu par le secrétariat : la prochaine version, du jour 3 du sprint à la phase 2.
- **Délégation** : la Présidence délègue les décisions de design à Steve Jobs, « avec ses propres paradigmes ». **La
  Présidence garde le dernier mot** : chaque décision de Jobs vaut jusqu'à ce qu'elle la retienne, la modifie ou l'écarte.
- **Formation** : atelier design, restreinte (5), à la demande de la Présidence, qui a fixé les membres du plus important
  au moins important : Steve Jobs (mène et tranche), Don Norman, Julie Zhuo, Karri Saarinen, puis Tristan Harris. Ordre
  de parole tiré au sort par le secrétariat, hors Jobs qui conclut : Karri Saarinen, Tristan Harris, Julie Zhuo, Don
  Norman, puis Steve Jobs. Contradicteur, tiré au sort : Karri Saarinen.
- **Tristan Harris siège comme garde-fou, pas comme designer** : la charte le range au pôle Harmonie (§4), et sa fiche ne
  porte aucune position sur l'interface d'un outil de travail ; son ancien poste de design ethicist chez Google fonde sa
  voix sur l'attention, pas sur la mise en page. Ce qu'il dirait hors de l'attention est marqué « hors champ ».
- **Note de formation** : la charte veut un membre par pôle ; Pont et Science sont absents. Contrepoids : le dossier porte
  R16 à R26, retenues après la revue où siégeaient Bengio, Hamilton et LeCun ; l'atelier dessine dans ces limites et n'en
  amende aucune.
- **Fiches** : à jour (moins de 30 jours). Norman, Zhuo et Saarinen au 28/10/2026, Harris au 21/10/2026 ; Jobs, siège
  historique, ne se rafraîchit que sur une nouvelle source historique (§9). Aucune fiche rafraîchie avant la séance.

## Dossier

1. `[ÉTABLI]` **La spécification de la v2, version 0.3**
   ([spécification](../../../v1/road_to_v2/Specification_V2_Harnais.md)). Au §15 : le harnais invisible pour
   l'utilisateur ; un panneau de contexte à droite, « à la manière de Claude » ; `/` et `@` depuis la demande ; la carte
   de résultat sur l'issue (le résultat, trois à cinq contrôles, une décision : accepter, refuser, demander une reprise ;
   « Défaire » quand c'est possible ; en dessous, la fabrication et l'export du dossier) ; les demandes de décision dans
   Mentions ; déléguer reste un choix du menu Assignee ; le dessin avant le code (R13). Au §18 : la carte se dessine au
   jour 1 par l'atelier design et se code au jour 3, au plus simple. Au §4.2 : la webapp sert aussi ceux qui utilisent
   TaskForce comme un outil de gestion de projet ou un chat d'IA classiques (Présidence, 28/10). En vigueur : R12 (on ne
   montre que ce qui marche), R19 (un aperçu des effets avant toute décision), R21 (une demande conçue contre l'erreur),
   R22 (trois gestes, essayer, voir ce qui changera, appliquer ; les mots du harnais restent internes ; un glossaire de
   l'interface relu par une personne non ingénieure), R23 (on garde la porte et la preuve, on lâche le fil, les vecteurs
   et le panneau, et on le dit en clair), R24 (un plafond de demandes par personne), R26 (la délégation se voit).
2. `[ÉTABLI]` **Le ménage et le jour 1 du sprint** (`.ai/roadmap.md` du dépôt `taskforce-fullstack`, bloc « MAJ
   28/10/2026 »). Retirés : le panneau Status, les Pages, le front du Brain OS (le moteur et `brain_search` restent) ;
   Assignments fondu dans My Work ; la visibilité nommée « Workspace » et « Collaborators only » ; GitHub et Slack cachés
   dans l'app desktop, revue au 30/11/2026. Harnais : chaque action de Claude Code jugée par les règles (`PreToolUse`),
   rien d'autorisé d'avance, garde fermée, Claude Code 2.1.295 exigé avant chaque mission ; « demander » passe par Allow
   ou Deny dans TaskForce ; un dossier de preuve chaîné, téléchargé par « Download the record » sous un run terminé. La
   table par défaut compte 31 règles (`contracts/rules/default.rules.json`) : lire, écrire dans la copie, committer,
   lancer `npm test`, `lint`, `build` ou `typecheck` sont autorisés ; chercher et lire sur le web sont demandés ; le
   `git push` et le `gh` de l'agent sont refusés ; pousser la branche `tf/` vers un dépôt privé et ouvrir la pull request
   sont autorisés, demandés si le dépôt est public ; fusionner, publier, envoyer, payer, se servir d'un secret sont
   demandés ; une commande qu'aucune règle ne classe, `npm install` par exemple, est demandée.
3. `[ÉTABLI]` **Cortex, aujourd'hui** (`agent-chat.tsx`, `assistant-service.ts`, `command-palette.tsx`,
   `AgentService.java`, `desktop/src/ai.ts`). Un panneau à droite, posé par-dessus le contenu, ouvert par « Ask AI »
   dans la barre du haut ; la palette Ctrl+K a aussi un mode « Ask AI », qui répond dans la palette. Il ne sait pas ce
   qui est ouvert : la requête ne porte que le message et la conversation. Ses outils : chercher dans les connaissances,
   lister et créer projets et issues, créer une note, trouver une intégration, et les outils des serveurs MCP connectés.
   Ses écritures internes partent tout de suite, au nom de la personne, sans règle ni dossier ; une écriture dans un
   outil externe attend un « Approve and run », réservé aux propriétaires et aux administrateurs. Il ne délègue pas, et ne
   montre ni run, ni demande, ni résultat. Sa boîte n'a ni `/` ni `@`, et trois suggestions fixes au départ. Sans modèle,
   il cherche quand même et cite les notes trouvées. Ses étapes et ses réponses de repli, écrites par le backend, disent
   encore « Brain OS » (« Searching the Brain OS »). Dans l'app desktop, il passe par le relais de la coque vers Ollama,
   avec un modèle de conversation pris parmi ceux installés (qwen3:8b d'abord) et des vecteurs de 1 024 dimensions
   (bge-m3). Sa boucle d'outils est celle que l'agent interne étendra au jour 3 (spécification §10.4 et §18).
4. `[ÉTABLI]` **La délégation, aujourd'hui** (`assignee-menu.tsx`, `issue-sheet.tsx`, `delegate-agent-control.tsx`,
   `run-activity.tsx`, `workflow-dock.tsx`, `panel-store.ts`, `sheet.tsx`, `DeliveryService.java`,
   `DeliveryRunner.java`, `inbox-view.tsx`). Elle part du menu Assignee (« Delegate to an agent ») et ne change pas
   l'assigné : une issue sans assigné le reste, et la personne qui a délégué n'est nommée nulle part à l'écran. Dans la
   colonne Details de la fiche d'issue, sous l'assigné : « Waiting for your runner to pick it up », « Agent working on
   it », « Show activity », les demandes « Claude Code asks to run … » avec Allow, Deny et « … min left, then it is
   denied » (10 minutes par défaut dans le runner), puis « Agent done - ready for your review », le résumé écrit par
   l'agent, « View result » et « Download the record: JSON · Markdown ». Les sorties du runner (`git push`, `gh pr
   create`) se présentent aussi en « Claude Code asks », alors que c'est TaskForce qui demande. À la fin, l'issue passe
   dans une colonne « In review by AI » ; aucun bouton n'applique, ne refuse ni ne relance. Le panneau AI Workflows
   liste délégations et analyses, en lecture seule, du même côté que Cortex, et un seul panneau tient par côté. La fiche
   d'issue est modale : un voile couvre la fenêtre, au-dessus des panneaux ; `[DÉDUIT]` Cortex ne se voit donc pas
   quand une issue est ouverte. Les demandes arrivent dans l'onglet All de Signals (« Approval needed »), pas dans
   Mentions, dont le filtre ne garde que les mentions ; dans l'app desktop, aussi en notification du système.
5. `[ÉTABLI]` **La navigation** (`app-sidebar.tsx`, `constants_en.ts`, `app-topbar.tsx`, `dashboard-hero.tsx`,
   `command-palette.tsx`). Le menu : Dashboard ; Signals (All Signals, Mentions, Alerts) ; My Queue (All my queues,
   Issues, Sprints) ; Operations ; Intelligence ; Members, dans la webapp seulement ; New Project ; Settings, qui ouvre
   une fenêtre ; Help. Une même chose porte plusieurs noms : « Signals », « Signal Center », « Inbox » ; « My Queue »,
   « My Work » ; « Operations », « Projects », « New Project », « Create an operation » ; « Sprints », « Cycles ».
   L'accueil ouvre sur « Pick up where you left off. » et une barre de recherche ; sa pilule « Connect your tools » montre
   les logos de GitHub et de Slack, y compris dans l'app desktop, où ces deux outils sont cachés. Un projet : Board,
   List, Roadmap, Backlog, Cycles, Teams (webapp), Settings ; l'issue s'ouvre en fiche latérale.
6. `[ÉTABLI]` **Les réglages et la version de Claude Code** (`settings/page.tsx`, `desktop-ai-panel.tsx`,
   `desktop-claude-code-setup.tsx`, `local-runner-setup.tsx`, `taskforce-runner/src/version.ts`). AI, dans l'app desktop
   seulement : Ollama sur l'ordinateur, une API compatible OpenAI, ou pas d'IA ; trois modèles (Conversation, Quick
   answers, Search) et leur état. Agents, dans l'app desktop : Claude Code, Git et GitHub vérifiés en direct ; la version
   de Claude Code s'affiche, mais son minimum n'est pas contrôlé, et une 2.1.293 paraît prête. Le runner, lui, le
   contrôle avant chaque mission et refuse de partir : « Claude Code 2.1.295 or later is needed for the rules to hold ».
   Dans la webapp, l'aide du runner dit encore « 2.1.293 or later ».
7. `[ÉTABLI]` **Ce qui n'existe pas encore** : l'agent interne sur un petit modèle (jour 3) ; l'import des documents et
   de leurs versions (jour 2) ; le panneau de contexte ; `/` et `@` ; la carte de résultat ; le relecteur ; Mentions comme
   appel d'un agent à un humain (phase 2). Un bloc de la roadmap, en cours d'écriture par une autre session et non commité
   au moment de la séance, annonce la release 1.5.0 (la v2 vers la prod), puis l'app desktop 1.3.0 (`455799a1`) ; la
   spécification (§18) prévoyait la webapp en local dans Docker. La séance n°5, tenue en parallèle
   ([PV](./2026-10-28-trajectoire-harnais.md), non commité au moment de la séance), relève que le dessin de la carte, dû
   au jour 1, manquait, et recommande de ne pas faire tourner de mission déléguée en prod sur un dépôt public avant S1
   (R33, en attente).
8. `[ÉTABLI]` **Les paradigmes de Jobs**, siège historique (fiche) : partir de l'expérience du client et remonter vers la
   technique (WWDC 1997, [Daring Fireball](https://daringfireball.net/2014/02/working_backwards), 25/02/2014) ; se
   concentrer, c'est savoir dire non (WWDC 1997, [TechCrunch](https://techcrunch.com/2011/10/06/jobs-focus-is-about-saying-no),
   06/10/2011) ; le design est le fonctionnement, pas l'apparence (New York Times Magazine, 30/11/2003, cité par
   [Marco Arment](https://marco.org/2007/11/28/most-people-make-the-mistake-of-thinking-design-is)) ; dire en clair à
   quoi l'on consent, et redemander (D8, 2010,
   [Fortune](https://fortune.com/2018/03/28/steve-jobs-facebook-cambridge-analytica-privacy), 28/03/2018) ; des règles
   d'admission publiques
   ([Apple](https://www.apple.com/newsroom/2010/09/09Statement-by-Apple-on-App-Store-Review-Guidelines/), 09/09/2010).
   Mort en 2011, il n'a aucune position sur les agents d'IA.
9. `[ÉTABLI]` **Les positions des autres membres** (fiches). Norman : une automatisation partielle doit donner un retour
   continu, et l'échange entre l'humain et la machine tient trop souvent de deux monologues
   ([jnd.org](https://jnd.org/problem-of-automation-inappropriate-feedback-and-interaction-not-over-automation/), 1990 ;
   [The Design of Future Things](https://jnd.org/books/the-design-of-future-things/), 2007) ; la découvrabilité et
   l'annulation ne se sacrifient pas à l'esthétique ([jnd.org](https://jnd.org/how-apple-is-giving-design-a-bad-name/),
   10/11/2015). Zhuo : les cinq problèmes des interfaces conversationnelles, et la conversation mariée aux contrôles
   ([The Looking Glass](https://lg.substack.com/p/conversational-interfaces-the-good), 12/05/2025) ; le contexte avant
   l'intelligence ([Opinionated Intelligence](https://opinionatedintelligence.substack.com/cp/192244974), 26/03/2026) ;
   l'échelle conseiller, adjoint, régent
   ([The Looking Glass](https://lg.substack.com/p/you-cannot-mandate-an-ai-transformation), 01/09/2026). Saarinen : le
   chat sert à explorer, mais pour le travail d'équipe répété c'est une page blanche
   ([Every](https://every.to/thesis/how-to-design-for-human-agent-interaction), 03/04/2026) ; l'humain reste assigné,
   l'agent est délégué, son état reste visible ([Linear](https://linear.app/developers/aig)) ; Linear Agent est un
   panneau de l'app ([changelog](https://linear.app/changelog/2026-03-24-introducing-linear-agent), 24/03/2026). Harris :
   la clarté donne la main ([Democracy Now!](https://www.democracynow.org/2026/10/8/the_ai_doc), 08/10/2026) ; les
   incitations expliquent les résultats ([CHT](https://www.humanetech.com/the-cht-perspective)).
10. `[ÉTABLI]` **Les contraintes du terrain** (`recherche/CLAUDE.md` §3) : une seule personne et un seul espace
    d'historique réel (C1), donc toute mesure tirée de cette séance est une première mesure ; un budget proche de zéro et
    des modèles locaux (C4).

## Tour de table `[HYPOTHÈSE]`

- **Karri Saarinen** (Design, contradicteur) : le travail d'une équipe vit dans des objets qui ont un responsable, un
  état et une échéance ; une conversation n'a rien de tout cela. Cortex sert à explorer, à interroger les connaissances
  de l'espace ; comme surface par défaut, c'est une page blanche qui laisse tout le poids à celui qui tape. Le dossier
  montre le vrai défaut : Cortex ignore l'issue ouverte, et la fiche de l'issue le recouvre. Il veut un établi ancré dans
  l'objet, pas un chat posé à côté. Il classe les flows par ce que les gens font chaque jour : l'issue et sa délégation,
  ce qui leur est assigné, puis le reste. La carte est le lieu du jugement : le résultat, les contrôles, la décision, et
  l'état de l'agent en quatre mots, au travail, en attente, en erreur, terminé. Pour le code, la revue ligne à ligne
  existe déjà dans la pull request : la carte ne la recopie pas. Au test, il mesure le temps entre « Delegate » et la
  première activité visible, parce qu'un outil lent perd la confiance. *Sa recommandation : l'issue est la surface ;
  Cortex s'y ancre et n'en est que la porte.*
- **Tristan Harris** (Harmonie, garde-fou) : il siège pour l'attention. Sa question : que maximisera Cortex devenu la
  surface principale ? Si c'est le nombre de messages ou le temps passé, l'outil apprendra à retenir. Il demande
  l'inverse : Cortex répond, rend compte et se tait, sans question de relance par défaut, sans série ni récompense, et il
  porte un nom sans jouer une personne. Une décision n'est jamais un message parmi d'autres : elle a sa forme, elle se
  regroupe, et le plafond de demandes par personne (R24) tient. On mesure le temps d'attention par résultat appliqué et
  les décisions regrettées (R3), jamais l'engagement. Le refus coûte le même geste que l'accord, et rien n'est
  présélectionné. Le compte à rebours d'une demande peut rester, puisque l'échéance vaut « non », mais sans alarme. Au
  test, il compte les notifications reçues quand rien n'attendait la Présidence. Sur le classement des flows, il
  s'abstient (hors champ). *Sa recommandation : Cortex ne retient pas ; une décision ne se noie jamais dans le fil.*
- **Julie Zhuo** (Design) : elle part du problème des personnes. L'ingénieur du premier cas d'usage, chez un éditeur de
  logiciels pour réseaux embarqués, ne veut pas converser : il veut son analyse d'impact. Une interface conversationnelle
  a cinq problèmes connus : la page blanche, l'itération, l'entrée et la sortie, le périmètre, la personnalisation.
  Cortex en traite deux à moitié, avec trois suggestions au départ et `find_integration` pour dire quel outil lui
  manque ; il ignore l'objet ouvert, alors que le même modèle répond bien mieux avec le contexte. Elle soutient Cortex
  comme surface principale à une condition : la conversation mariée à des contrôles, la carte posée dans le fil comme un
  objet qu'on manipule, et un Cortex qui dit ce qui dépasse sa compétence. Elle classe les flows par la première minute,
  où l'avis se forme : démarrer et donner le contexte passent avant Cortex. Elle propose d'afficher le palier de l'agent
  (conseiller, adjoint, régent) et, après des applications répétées sans regret, une règle proposée. Au test, un
  pronostic écrit avant l'essai, relu après. *Sa recommandation : une conversation mariée à des contrôles ; la carte vit
  aussi dans le fil.*
- **Don Norman** (Design) : un fil de conversation est un dialogue, donc une bonne forme, à deux conditions. L'état de
  l'agent se voit en continu hors du fil, qui défile ; et une décision ne se prend jamais par un « oui » tapé, où le raté
  guette : on approuve par habitude. Il relève trois mots qui trompent déjà. « In review by AI » fait croire que l'IA
  relit, quand c'est la personne qui doit relire. « Claude Code asks to run git push » prête à l'agent une demande que
  pose TaskForce. « AI is not configured », quand Ollama est seulement arrêté, ne dit pas la cause. Demander à l'IA se
  fait à deux endroits qui ne se comportent pas pareil, le panneau et la palette : une source d'erreurs de mode. La carte
  est un dialogue : ce qui a été fait, pourquoi, ce qui reste incertain, ce qu'on attend de la personne ; « Défaire »
  partout où c'est possible ; un geste forcé seulement devant une sortie sans retour. La demande de décision est le flow
  le plus dangereux : elle passe en tête de la conception, même si elle est rare. Au test, chaque hésitation s'écrit avec
  l'écran qui l'a causée : c'est un défaut de conception, pas une erreur de la Présidence. *Sa recommandation : l'état de
  l'agent se voit toujours, et chaque mot dit la vérité de l'état.*
- **Steve Jobs** (Impulsion, siège historique, mène et tranche) : il part de l'expérience. Une personne décrit un
  résultat, TaskForce le lui rend prouvé ; tout le reste est de la tuyauterie. Il compte les endroits où l'on demande à
  l'IA (le panneau, la palette, « AI Spec » sur l'issue) et ceux où l'agent attend la personne (la fiche de l'issue,
  Cortex pour les outils externes, AI Workflows pour les analyses) : trop. Un endroit pour demander, un objet pour
  décider. Il compte aussi les noms d'une même chose, « Signals », « Signal Center », « Inbox » : un seul suffit. La
  carte se comprend d'un regard : ce qui a été fait, si c'est bon, ce qui changera, et les gestes de R22 ; la fabrication
  reste repliée, sinon on empile des écrans de conformité. Ce qui ne marche pas ne se montre pas : la pilule de l'accueil
  montre Slack dans l'app desktop. Pour chaque chose ajoutée, une retirée : si Cortex devient l'entrée, la palette ne
  répond plus de son côté. La Présidence teste comme un client : le terminal seulement avant l'installation, et pour
  vérifier un dossier. *Sa recommandation : un endroit pour demander, un objet pour décider, un nom par chose.*

## Confrontation `[HYPOTHÈSE]`

1. **Cortex, surface principale ?** Zhuo répond à Saarinen que la promesse commence par « vous décrivez le résultat » :
   décrire, c'est du langage, et la boîte de Cortex est le chemin le plus court entre l'intention et la délégation ; la
   webapp sert aussi ceux qui veulent un chat d'IA classique (spécification §4.2). Saarinen, contradicteur, attaque le
   consensus qui se forme : le lendemain, on cherche le travail, pas la conversation ; un fil n'a ni responsable, ni état,
   ni échéance, et l'issue a les trois. Norman donne raison aux deux : le fil convient pour demander et pour rendre
   compte, pas pour garder l'état ni pour décider. Harris accepte un Cortex au centre si rien n'y est conçu pour retenir.
   Synthèse : Cortex pour demander et pour être tenu au courant ; l'issue garde le travail et sa carte ; la décision se
   prend sur la carte. Divergence : Zhuo veut la carte jusque dans le fil ; Saarinen refuse un chat comme surface par
   défaut.
2. **La carte et ses gestes.** Le tour s'accorde sur la carte : l'unanimité déclenche le contradicteur. Saarinen attaque :
   pour du code, la pull request porte déjà la revue, et une carte qui recopie un diff recopie GitHub ; les équipes
   connaissent « accepter » et « refuser », et « Appliquer » est un mot de plus à apprendre. Jobs répond que la carte ne
   recopie pas le diff : elle dit ce qui changera et mène à la pull request pour la lecture ligne à ligne ; « Appliquer »
   dit ce que fait le clic, « Accepter » dit ce que pense la personne. Norman le suit sur le verbe, qui doit décrire
   l'effet, et demande « Défaire » après coup, un geste forcé devant une sortie sans retour, et jamais la touche Entrée
   pour appliquer. Harris veut « Écarter » aussi visible qu'« Appliquer ». Zhuo veut juger les mots en une minute, avec
   une personne non ingénieure, et afficher le palier de l'agent ; Jobs et Harris refusent le palier à l'écran : c'est un
   mot du harnais (R22), et une règle proposée au moment de juger pousse à lâcher la main. Synthèse : trois gestes de R22
   et un non, de même poids ; « Défaire » ensuite ; chaque sortie sans retour demandée à part ; la revue ligne à ligne
   reste dans la pull request ; la règle proposée va au propriétaire de la règle, hors de la carte. Divergence : Saarinen
   préfère les mots de la revue.
3. **Le classement des flows.** Jobs classe par la promesse : juger, confier et suivre, répondre, demander. Saarinen
   objecte qu'un classement qui met le board au neuvième rang dit à ceux qui gèrent leurs projets dans la webapp que
   l'outil n'est plus pour eux. Zhuo objecte qu'une mauvaise première minute perd la personne avant qu'elle voie une
   carte : démarrer et donner le contexte passent avant Cortex. Norman met la demande de décision en tête de la
   conception, quel que soit son rang. Harris s'abstient (hors champ) et demande seulement que « ce qui m'attend » reste
   calme. Synthèse : le classement dit ce que l'atelier dessine et ce qu'on répare d'abord, pas ce qui sert le plus
   souvent ; le board marche et ne se refait pas. Divergence : Zhuo et Saarinen gardent leur ordre.

## Recommandations `[HYPOTHÈSE]`

| # | Recommandation | Pour | Contre | Preuve en dix jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| D1 | **Cortex, l'endroit où l'on demande et où l'agent rend compte ; on n'y décide pas** : une ligne par étape qui compte, et chaque décision se prend sur la carte | Jobs, Zhuo (avec la carte dans le fil), Norman (si l'état se voit hors du fil), Harris (sans relance) | Saarinen (contradicteur : l'issue reste la surface ; un chat par défaut est une page blanche) | Dix demandes réelles de la Présidence parties de Cortex : combien mènent à une carte sans passer par le board, combien de fois elle rouvre l'issue pour savoir où en est l'agent | Plus d'un retour sur deux à l'issue pour connaître l'état ; une seule décision prise par un message tapé |
| D2 | **Cortex sait ce qui est ouvert, et l'issue ne le recouvre plus** : l'objet ouvert part avec la demande ; Cortex et l'issue se voient ensemble | Saarinen, Zhuo, Norman, Jobs | Aucun | L'issue ouverte, « What is blocking this? » reçoit une réponse sur cette issue sans qu'on donne sa clé, Cortex et l'issue visibles ensemble | Le contexte ajouté fait sortir le petit modèle de sa fenêtre, ou allonge sa réponse de plus de moitié (famille 7 de la banque de tests) |
| D3 | **Une seule façon de demander** : le mode « Ask AI » de la palette ouvre Cortex avec la question ; `/` et `@` dans la boîte de Cortex, la liste ouverte dès le premier caractère | Jobs, Norman, Zhuo | Aucun (Saarinen veut aussi `@` dans les commentaires de l'issue, ce que vend Linear) | Une question posée par Ctrl+K arrive dans Cortex avec sa réponse, dans l'historique ; la Présidence appelle un agent et une source par `/` et `@` sans aide | `/` ou `@` se déclenchent dans un texte ordinaire (un chemin de fichier, une adresse e-mail) |
| D4 | **Les flows classés selon la promesse** (tableau de la décision J2) : c'est l'ordre de la conception et de la réparation | Jobs, Norman (la demande de décision en tête de la conception) | Saarinen (par fréquence : l'issue et My Queue d'abord), Zhuo (par la première minute : démarrer et le contexte avant Cortex) ; Harris s'abstient (hors champ) | Les défauts du parcours de test rangés par rang de flow ; les trois premiers rangs passent avant le reste dans la phase 2 | L'essai montre que la Présidence passe l'essentiel de son temps dans un flow classé bas : le classement se revoit |
| D5 | **Une seule carte de résultat, sur l'issue, telle que dessinée** ; Cortex et Signals y mènent ; pour le code, la revue ligne à ligne reste dans la pull request | Jobs, Norman, Zhuo, Harris, Saarinen (avec la pull request) | Aucun | La carte codée au plus simple au jour 3, sur le corpus public (MQTT 3.1.1 et 5.0) : une personne non ingénieure dit en une minute ce qui a été fait, si c'est bon et ce qui changera | Elle ne sait pas dire ce qui changera ; ou une application est regrettée parce que la carte taisait un effet |
| D6 | **Trois gestes et un non** : Voir ce qui changera, Essayer encore, Appliquer ; Écarter, de même poids ; Défaire ensuite ; jamais la touche Entrée pour appliquer ; chaque sortie sans retour demandée à part | Jobs, Norman, Harris, Zhuo (sous réserve du test d'une minute) | Saarinen (contradicteur : les mots de la revue, accepter et refuser, que les équipes connaissent) | Trois personnes, dont une non ingénieure, disent avant de cliquer ce que fera chaque bouton ; « Défaire » remet en l'état une issue créée et une branche poussée | Une seule erreur de prédiction sur « Appliquer » ou « Écarter » |
| D7 | **La délégation se voit, la personne nommée d'abord** : l'agent ensuite, l'état en quatre mots, l'étape en cours ; une issue déléguée sans assigné prend pour assigné la personne qui délègue ; chaque demande dit qui la pose | Saarinen, Norman, Jobs, Zhuo | Aucun | Sur cinq délégations, la carte nomme la personne et l'agent, l'état se lit sans ouvrir l'activité, et la Présidence dit qui pose chaque demande | Un écart entre l'état affiché et l'état réel du run |
| D8 | **Le mode dégradé dit la vraie cause** : ce qui est en pause, ce qui continue, ce que la personne peut faire ; jamais un indicateur qui tourne sans message | Norman, Jobs, Harris | Aucun (Saarinen : un bandeau sur la carte concernée, pas sur toute l'app) | Ollama arrêté, puis l'app fermée en plein run : chaque fois, l'écran dit la vraie cause et ce qui continue | Un écran qui dit « AI is not configured » quand le modèle est seulement arrêté ; un indicateur qui tourne plus de deux minutes sans message |
| D9 | **Un nom par chose, et des mots vrais** : les noms se choisissent dans le glossaire de R22 ; « In review by AI » et « Brain OS » quittent l'écran | Jobs, Norman, Zhuo | Aucun | Le glossaire tient sur une page et passe la relecture d'une personne non ingénieure ; une recherche dans le code ne trouve plus qu'un nom par chose | Un renommage qui casse une adresse, un raccourci ou le lien d'une notification |
| D10 | **Cortex ne retient pas** : aucune question de relance par défaut, aucune mesure du temps passé ; on compte le temps d'attention par résultat appliqué et les décisions regrettées | Harris, Norman, Zhuo, Jobs | Saarinen (contradicteur : à N≈1, la mesure ne prouve rien, le jugement suffit) | Dix jours d'usage sans relance non demandée ; le dossier de chaque mission donne le temps d'attention ; la Présidence marque ses décisions regrettées | Une notification reçue alors que rien n'attendait la Présidence |
| D11 | **Le palier d'autonomie sur la carte** (conseiller, adjoint, régent) et, après des applications répétées sans regret, une règle proposée | Zhuo, Norman (les rênes qu'on relâche quand la preuve est là) | Jobs (un mot du harnais à l'écran), Harris (une règle proposée au moment de juger pousse à lâcher la main) | Après dix applications sans regret d'un même type d'action, la proposition arrive au propriétaire de la règle, qui décide | Une proposition qui revient après un refus, ou qui arrive pendant une décision |

**Désaccords conservés** : Saarinen, contradicteur, refuse un chat comme surface par défaut : l'issue reste la surface et
Cortex n'en est que la porte (D1). Zhuo voulait la carte dans le fil, comme un contrôle de la conversation ; Jobs ne la
laisse qu'à un endroit (J1). Saarinen préfère les mots de la revue, accepter et refuser, à ceux de R22 (D6). Zhuo classe
le démarrage et le contexte avant Cortex, Saarinen classe par fréquence, l'issue et My Queue d'abord (D4). Saarinen juge
qu'à N≈1 la mesure ne prouve rien (D10). Jobs et Harris refusent le palier d'autonomie à l'écran, que Zhuo proposait
(D11).

## Décisions de Jobs (déléguées par la Présidence) `[HYPOTHÈSE]`

Par délégation de la Présidence, Steve Jobs tranche les questions de design selon ses paradigmes documentés (dossier,
point 8). Ce sont les décisions d'un personnage simulé : elles n'engagent pas la personne réelle et ne sortent pas du labo
sous son nom (charte §8). Elles valent par délégation ; **la Présidence garde le dernier mot** et peut retenir, modifier ou
écarter chacune.

| # | Décision | Sur | Le paradigme invoqué |
| --- | --- | --- | --- |
| J1 | **Cortex reste, et devient l'endroit où l'on demande et où l'agent rend compte ; on n'y décide pas.** Dans le fil, une ligne par étape qui compte (confié, en attente de vous, prêt à juger), qui mène à la carte. Cortex sait ce qui est ouvert. À droite, un seul panneau : Cortex et le contexte de ce qui est ouvert (le panneau de contexte du §15, dont le dessin reste à faire), que l'issue ne recouvre plus. La palette mène à Cortex. La carte n'entre pas dans le fil. | Question 1 ; D1, D2 et D3 retenues ; la carte dans le fil écartée | Partir de l'expérience : la personne décrit un résultat, à un seul endroit ; une chose ajoutée, une retirée |
| J2 | **Le classement des flows ci-dessous.** Il dit ce que l'atelier dessine et ce qu'on répare d'abord, pas ce qui sert le plus souvent. Le board marche : on ne le refait pas, on ne le casse pas. | Question 2 ; D4 retenue | La promesse d'abord : le résultat, prouvé |
| J3 | **La carte de résultat telle que dessinée ci-dessous**, une seule, sur l'issue, sous le titre. Les mots de R22 remplacent à l'écran ceux du §15 de la spécification : Appliquer pour accepter, Essayer encore pour demander une reprise, Écarter pour refuser. | Question 3 ; D5 et D6 retenues | Le design, c'est le fonctionnement : un bouton dit ce qu'il fait |
| J4 | **La délégation se voit**, la personne nommée d'abord ; une issue déléguée sans assigné prend pour assigné la personne qui délègue ; chaque demande dit qui la pose, l'agent ou TaskForce. | R26 ; D7 retenue | Dire en clair qui demande quoi, à chaque fois |
| J5 | **Le mode dégradé dit la vraie cause**, ce qui est en pause et ce qui continue ; jamais un indicateur qui tourne sans message. | R23 ; D8 retenue | La personne ne voit jamais un écran cassé (séance n°4, second tour) |
| J6 | **Un nom par chose, partout.** Les noms se choisissent dans le glossaire de R22 ; deux mots quittent l'écran d'office : « In review by AI », puisque c'est la personne qui relit, et « Brain OS » dans les étapes de Cortex. | D9 retenue | Se concentrer, c'est renoncer, jusque dans les mots |
| J7 | **Cortex ne retient pas.** Aucune relance par défaut ; on compte le temps d'attention par résultat appliqué et les décisions regrettées. | D10 retenue | Il suit Harris : ce que le produit maximise décide de ce qu'il devient |
| J8 | **Le palier d'autonomie ne s'affiche pas** : c'est un mot du harnais. La règle proposée après des applications répétées sans regret va au propriétaire de la règle, dans Signals, jamais sur la carte au moment de juger. | D11 modifiée : le palier écarté, la règle proposée retenue (spécification §6.5) | Les mots du harnais restent sous le capot (R22) |
| J9 | **Le parcours de test ci-dessous** : l'app desktop d'abord, où le harnais tourne en entier, puis la webapp pour ce qui diffère ; on ne teste que ce qui existe au jour 1, et les défauts connus sont annoncés. | Question 4 | Tester comme un client, du premier clic au résultat |

### Le classement des flows (J2)

Les colonnes « existe » et « manque » sont des faits lus dans le code le 28/10/2026 `[ÉTABLI]` ; le rang est la décision
de Jobs `[HYPOTHÈSE]`.

| Rang | Flow | Ce que la personne y fait | Ce qui existe dans le code aujourd'hui | Ce qui manque |
| --- | --- | --- | --- | --- |
| 1 | **Juger le résultat et décider** | Elle lit ce que l'agent a fait, voit si c'est bon et ce qui changera, puis applique, réessaie ou écarte | Sur la fiche de l'issue : « Agent done - ready for your review », le résumé écrit par l'agent, « View result », « Download the record: JSON · Markdown » ; l'issue passe dans « In review by AI » (`delegate-agent-control.tsx`, `run-activity.tsx`, `DeliveryRunner.java`) | La carte (D5, D6) : les contrôles tirés du dossier, ce qui changera, les gestes, « Défaire » ; aucun bouton n'applique ni n'écarte |
| 2 | **Confier un résultat et suivre l'agent** | Elle délègue une issue à l'agent de son choix, et voit où il en est sans l'interrompre | « Delegate to an agent » dans le menu Assignee, seuls les agents prêts proposés ; « Waiting for your runner to pick it up », « Agent working on it », « Show activity » relu en continu ; AI Workflows, section Delegations ; chaque action de Claude Code jugée par les 31 règles par défaut | Déléguer depuis Cortex (D1) ; le nom de la personne qui répond du travail, et un assigné humain quand l'issue n'en a pas (D7) ; l'état en quatre mots ; l'agent interne sur un petit modèle (jour 3) |
| 3 | **Répondre à une demande de décision** | Pendant la mission, elle dit oui ou non à une action que les règles demandent | « Claude Code asks to run … », la commande, Allow et Deny, « … min left, then it is denied », refus à l'échéance ; « Approval needed » dans l'onglet All de Signals ; une notification du système dans l'app desktop (`run-activity.tsx`, `NotificationService.java`) | La demande conçue contre l'erreur (R21) : pourquoi la règle demande, l'effet, l'action inverse ; qui demande, l'agent ou TaskForce (D7) ; l'arrivée dans Mentions ; le regroupement et le plafond (R24) |
| 4 | **Demander à Cortex** | Elle pose une question, cherche dans les connaissances de l'espace, fait faire une petite tâche | Le panneau « Cortex » (« Ask AI ») : conversations, sources citées, étapes, outils, « Approve and run » pour une écriture dans un outil externe, repli sans modèle ; le mode « Ask AI » de la palette ; Ollama dans l'app desktop (`agent-chat.tsx`, `AgentService.java`, `desktop/src/ai.ts`) | L'objet ouvert comme contexte, et Cortex visible avec l'issue (D2) ; une seule entrée, `/` et `@` (D3) ; ses écritures internes par la porte, tracées ; « Brain OS » retiré de ses étapes (D9) |
| 5 | **Donner le contexte** | Elle dépose des documents et leurs versions ; TaskForce calcule l'écart et cite ses sources | Le moteur du Brain OS et `brain_search` ; des notes créées par Cortex ou par « AI Spec » ; l'ingestion des cycles et des issues terminés et des projets créés (`BrainIngestionListener.java`) ; aucun écran d'import depuis le ménage | L'import, les versions, les passages et l'écart (jour 2) ; le panneau de contexte, que Cortex partage (J1) |
| 6 | **Savoir ce qui m'attend** | Elle voit d'un coup d'œil ce qui demande sa main : décisions, mentions, échéances, ce qui lui est assigné | Signals (All Signals, Mentions, Alerts), la cloche des notifications, My Queue (All my queues, Issues, Sprints), Assignments fondu dans My Queue (`inbox-view.tsx`, `my-work-view.tsx`) | Les demandes des agents dans Mentions (phase 2) ; un nom par chose (D9) ; une seule réponse à « qu'est-ce qui m'attend ? » (séance n°3) |
| 7 | **Démarrer et se mettre à jour** | Elle installe l'app ou ouvre la webapp, se connecte, crée son espace et son premier projet, choisit son modèle, met l'app à jour | La connexion, et `/auth/desktop` pour l'app ; l'accueil en quatre étapes sur la webapp, trois dans l'app desktop (You, Workspace, First project) ; la section AI de Settings, avec l'état d'Ollama et les commandes `ollama pull` ; « Check for updates » dans la section Account ; la notification « TaskForce … is installed » | Le contrôle de la version minimale de Claude Code avant la première délégation (D8) ; une première délégation guidée jusqu'à la carte |
| 8 | **Brancher ses agents et ses outils** | Elle relie Claude Code, Git, GitHub et des serveurs MCP | La section Agents de Settings : Claude Code, Git et GitHub vérifiés en direct dans l'app desktop, un runner à installer à la main pour la webapp ; dans la section Integrations, GitHub et Slack cachés dans l'app desktop jusqu'au 30/11/2026 | PC-059, PC-060 et le MCP local ; l'aide du runner de la webapp à jour (2.1.295) ; la pilule « Connect your tools » sans les logos cachés (R12) |
| 9 | **Organiser le travail** | Elle crée projets et issues, les range en board, liste, backlog, sprints et roadmap | « Operations », et dans un projet Board, List, Roadmap, Backlog, Cycles, Teams (webapp), Settings ; la fiche d'issue (description, AI Spec, sous-tâches, checklist, pièces jointes, relations, GitHub, activité) ; la visibilité « Workspace » et « Collaborators only » | Rien pour le parcours ; un nom par chose (« Operations », « Projects », « New Project ») |
| 10 | **Comprendre ses opérations** | Elle lit ce que l'IA observe de ses projets, et lance une analyse | Intelligence (« AI Signals », « Key metrics », un tableau de décision par projet) ; les analyses dans AI Workflows, avec la question posée à la personne | Rien pour le parcours ; la question d'une analyse arrive dans un troisième endroit, hors de Signals |
| 11 | **Travailler à plusieurs** | Elle invite, voit les membres, leurs compétences et leur charge, répartit le travail | Dans la webapp : Members, invitations, Teams, « Suggest best assignee » ; masqués dans l'app desktop | Le serveur d'équipe et les espaces d'équipe (phase 3) ; le fil de l'équipe (R24) |
| 12 | **Garder la main sur ses données** | Elle exporte, transfère un projet entre la webapp et l'app desktop, lit le journal d'audit, règle sa confidentialité | Privacy & Data, Audit log et son export CSV, le transfert de projet (l'original reste en place), le fichier d'espace, les textes de confidentialité propres à l'app desktop | Le dossier gardé après la suppression d'une issue (spécification §9.4) ; un résultat obtenu en local visible dans la webapp (spécification §4.2) |

### La carte de résultat (J3)

Le dessin de l'atelier, avant le code (R13). Les chiffres sont des exemples, sur le corpus public du premier cas d'usage
(MQTT 3.1.1 et 5.0). Les mots sont ceux du procès-verbal ; les libellés proposés pour l'interface, en anglais, suivent en
fin de section.

**Où elle vit** : sur l'issue, sous le titre, avant la description, dès qu'une mission existe. Cortex et Signals y mènent ;
il n'y en a pas d'autre copie. Pour le code, la lecture ligne à ligne reste dans la pull request.

```text
LA CARTE, état « Prêt à juger » (exemple)

+--------------------------------------------------------------------------------------------
| [ bandeau du mode dégradé : absent quand tout va bien ]
+--------------------------------------------------------------------------------------------
| 1. EN-TÊTE
|    Analyse d'impact de la version 5.0 sur le projet P
|    Pierre en répond · confié à Claude Code · Terminé · 23 min
+--------------------------------------------------------------------------------------------
| 2. LE RÉSULTAT
|    Un rapport : 14 impacts, et 31 sections sans impact, chacune justifiée.
|    [ Ouvrir le rapport ]
+--------------------------------------------------------------------------------------------
| 3. EST-CE BON ?                                    (contrôles choisis par l'espace, 3 à 5)
|    [vert]  Affirmations sourcées ................................. 47 sur 47
|    [vert]  Sections modifiées du standard traitées ............... 45 sur 45
|    [vert]  Aucune action définitive sans votre accord ............ 0
+--------------------------------------------------------------------------------------------
| 4. CE QUI CHANGERA si vous appliquez
|    Une note ajoutée aux connaissances de l'espace ................ se défait
|    14 issues créées dans le projet P ............................. se défait
|    [ Voir ce qui changera ]
+--------------------------------------------------------------------------------------------
| 5. CE QUI RESTE INCERTAIN
|    Deux sections ont changé de structure : leur alignement est à relire.
+--------------------------------------------------------------------------------------------
| 6. LES GESTES
|    [ Écarter ]                  [ Essayer encore ]                  [ Appliquer ]
+--------------------------------------------------------------------------------------------
| 7. COMMENT C'EST FAIT (replié)
|    Règles v12 · 38 actions · 2 demandes, 2 réponses · 52 sources citées
|    Télécharger le dossier : JSON · Markdown
+--------------------------------------------------------------------------------------------
```

**Ce que montre chaque zone**

- **1, l'en-tête** : le titre de la mission, qui est celui de l'issue ; la personne qui en répond, puis l'agent délégué ;
  l'état en un mot ; la durée.
- **2, le résultat** : ce qui a été fait, en une phrase, et le livrable (un rapport, une pull request), avec un lien pour
  l'ouvrir.
- **3, est-ce bon** : trois à cinq contrôles choisis par l'espace, chacun vert, rouge ou en attente, avec le chiffre qui le
  prouve. Ils viennent du dossier (sorties des tests, sources vérifiées), jamais du résumé de l'agent (spécification
  §8.3). Pour le premier cas d'usage, les trois contrôles par défaut du §15.
- **4, ce qui changera** : chaque sortie, marquée « se défait » ou « définitive ». C'est l'aperçu des effets (R19),
  toujours visible avant les gestes. Pour du code : les fichiers, les lignes ajoutées et retirées, la branche, la pull
  request.
- **5, ce qui reste incertain** : ce que l'agent n'a pas pu vérifier, ce qu'il a laissé de côté, ce qui lui a été refusé
  en route. Vide, la zone disparaît.
- **6, les gestes** : voir le bloc « Les gestes ».
- **7, comment c'est fait**, repliée, pour qui le demande : la version des règles, les étapes, les sources lues, les
  demandes et leurs réponses, et l'export du dossier (aujourd'hui « Download the record »).

```text
LES ÉTATS : un seul à la fois, dit dans l'en-tête

Au travail           L'en-tête et une ligne : l'étape en cours (« Lit la section 3.1.2.4 Keep Alive »).
                     Geste : [ Arrêter ]. Rien à juger encore.
En attente de vous   La demande en tête de carte (bloc « La demande »). Le reste de la carte attend.
Prêt à juger         Toutes les zones. Gestes : Écarter, Essayer encore, Appliquer.
Appliqué             Ce qui est sorti, quand et par qui. [ Défaire ] si chaque sortie a son inverse ;
                     sinon, la carte dit ce qui est définitif.
Écarté               « Rien n'est sorti. » La raison, si la personne l'a donnée. Geste : [ Essayer encore ].
En échec             La cause, en clair ; ce qui est gardé ; rien n'est sorti. Geste : [ Essayer encore ].
```

```text
LA DEMANDE (état « En attente de vous »), en tête de carte (R21)

  Claude Code demande à chercher sur le web : « MQTT 5.0 session expiry »
  Ce qu'elle fera : envoyer cette requête à un moteur de recherche, hors de l'ordinateur.
                    Une requête partie ne se reprend pas.
  Pourquoi on vous demande : une recherche sur le web fait sortir des mots de votre projet.
  Ce que l'agent a compris du but : relever les changements de la version 5.0 qui touchent le projet P.
  Si vous refusez : l'agent continue sans cette recherche.

  [ Refuser ]                 [ Autoriser ]                 Sans réponse dans 9 min, c'est non.
```

```text
LES GESTES : les trois de R22, et un non

Voir ce qui changera  Ouvre le détail de la zone 4 : la note telle qu'elle sera écrite, la liste des
                      issues, ou la pull request pour du code. Le résumé de la zone 4 reste toujours
                      visible : ce geste n'est jamais obligatoire pour une sortie qui se défait.
Appliquer             Fait sortir tout ce qui se défait, et le trace. Une sortie définitive est
                      demandée à part, une par une, par une question binaire (R1, R21).
                      Jamais sélectionné d'avance, jamais déclenché par la touche Entrée.
Essayer encore        Un champ d'une ligne, « Ce qui doit changer », puis l'agent reprend dans la même
                      copie. La nouvelle carte remplace l'ancienne, qui reste au dossier.
Écarter               Rien ne sort. Une raison facultative, d'une ligne. Même taille et même rangée
                      qu'Appliquer.
Défaire               Après Appliquer seulement : les actions inverses, dans l'ordre inverse des
                      sorties, et tracées (spécification §7.5).
```

```text
LA DÉLÉGATION VISIBLE (R26)

Qui en répond   La personne d'abord, l'agent ensuite : « Pierre en répond · confié à Claude Code ».
                Une issue déléguée sans assigné prend pour assigné la personne qui délègue.
L'état          Quatre mots : Au travail, En attente de vous, En échec, Terminé.
L'activité      Une ligne : l'étape en cours. « Voir l'activité » ouvre la chronologie entière.
Qui demande     « Claude Code demande » pour une action de l'agent ; « TaskForce demande » pour une
                sortie (pousser la branche, ouvrir la pull request).
Où              Sur l'issue, sous le titre. Dans Cortex, une ligne par étape qui compte (confié, en
                attente de vous, prêt à juger), qui ouvre l'issue sur sa carte. Dans Signals, la
                demande mène à la carte. Une seule carte, un seul état, partout.
Ce qu'on évite  Valider chaque étape : la personne juge le résultat, sauf ce qui est définitif.
```

```text
LE MODE DÉGRADÉ (R23) : un bandeau en tête de la carte concernée, jamais un écran figé

La règle  On garde la porte et la preuve ; on met en pause le fil, la recherche par le sens et le
          panneau. Le bandeau dit la vraie cause, ce qui est en pause, ce qui continue, et ce que la
          personne peut faire.

Le modèle local ne répond plus
          « Le modèle de cet ordinateur ne répond pas (Ollama). L'agent est en pause, rien n'est
          sorti ; il reprend quand le modèle répond. »
L'app s'est fermée pendant le travail
          « Le travail s'est arrêté à la fermeture de l'app, à l'étape X. Rien n'est sorti. »
          Geste : [ Essayer encore ].
Claude Code est trop ancien
          « Claude Code doit être en 2.1.295 au moins pour que vos règles tiennent. Mettez-le à
          jour, puis Essayer encore. »
Les règles sont injoignables
          « La mission n'a pas démarré : TaskForce ne peut pas vérifier vos règles. Rien n'a été
          lancé. »
La recherche par le sens est indisponible
          « La recherche se fait sur le texte exact, en attendant le modèle de recherche. »
Le serveur d'équipe est injoignable (plus tard, phase 3)
          « L'agent continue dans sa copie ; les sorties et les décisions attendent le réseau. »
```

**Libellés proposés pour l'interface, en anglais** (à relire pour le glossaire de R22, par une personne non ingénieure) :

| Dans ce procès-verbal | Libellé proposé |
| --- | --- |
| Voir ce qui changera, Appliquer, Essayer encore, Écarter, Défaire, Arrêter | See what will change, Apply, Try again, Discard, Undo, Stop |
| Au travail, En attente de vous, En échec, Terminé | Working, Waiting for you, Failed, Done |
| Pierre en répond · confié à Claude Code | Pierre · delegated to Claude Code |
| Est-ce bon ?, Ce qui changera, Ce qui reste incertain, Comment c'est fait | Checks, What will change, Still uncertain, How it was done |
| Se défait, définitive | Can be undone, Permanent |
| Refuser, Autoriser | Deny, Allow (déjà dans l'app) |

### Le parcours de test de la Présidence (J9)

Ce qu'il faut voir est lu dans le code du 28/10/2026 `[ÉTABLI]`, sauf mention « à vérifier » ; les libellés sont ceux de
l'interface, en anglais. Un « défaut connu » est déjà au dossier : il se constate, il ne se découvre pas. Rien n'est
attendu du jour 2 ni du jour 3.

**Avant**

1. Écrire un pronostic en trois lignes : ce que la Présidence pense voir dans la première minute, après la première
   délégation, et ce qui la gênera. Le relire à la fin (Zhuo).
2. Vérifier le poste, dans un terminal. À voir : `ollama list` montre un modèle de conversation (qwen3:8b ou un autre
   petit modèle) et `bge-m3` ; `claude --version` donne 2.1.295 au moins (sinon `npm install -g
   @anthropic-ai/claude-code`), et `claude` est connecté ; `git` répond ; `gh auth status` est connecté, pour un projet
   relié à un dépôt. Échec : aucun à ce stade ; noter ce qui manque.

**L'app desktop**

3. Installer la 1.3.0 : l'installeur construit par la CI de la branche, ou « Check for updates » dans la section Account
   de Settings, une fois « Desktop - Release » publiée. À voir, au premier lancement : la notification « TaskForce 1.3.0
   is installed », « Updated from version … » ; dans la section Account, « TaskForce Desktop » et « Version 1.3.0 ».
   Windows peut prévenir que l'app n'est pas signée : c'est attendu. Échec : l'app ne démarre pas, ou reste en 1.2.x.
4. Se connecter. À voir : la page de connexion s'ouvre dans le navigateur (`/auth/desktop`), puis l'app arrive sur « Pick
   up where you left off. ». Échec : une boucle de connexion, un écran de Keycloak.
5. Le ménage, menu par menu. À voir : Dashboard, Signals (All Signals, Mentions, Alerts), My Queue (All my queues, Issues,
   Sprints), Operations, Intelligence, New Project, Settings, Help ; ni Members ni aucune entrée Brain OS ; dans un
   projet, Board, List, Roadmap, Backlog, Cycles, Settings, sans Pages ; dans Signals, pas d'Assignments ; dans Settings,
   « Audit log » et pas de « Status » ; dans la section Integrations, ni GitHub ni Slack. Échec : l'un d'eux visible, ou
   une page vide au clic. Défaut connu : la pilule « Connect your tools » de l'accueil montre encore les logos de GitHub
   et de Slack.
6. La visibilité : créer un projet. À voir : « Workspace » et « Collaborators only ». Échec : « Public » ou « Private ».
7. Le modèle local, dans la section AI de Settings. À voir : « Ollama on this computer » choisi ; sous Models,
   « Automatic: qwen3:8b. » ou son modèle ; « Conversation ready with … » et « Search ready with … ». Choisir un modèle
   plus petit pour « Quick answers », puis « Save ». À voir : « Saved. TaskForce uses it right away. ». Échec : « Ollama
   isn't running on this computer » alors qu'Ollama tourne ; un modèle installé absent de la liste.
8. Cortex : « Ask AI », en haut à droite, puis « Which issues are blocked, and why? ». À voir : « Cortex is thinking » et
   les secondes, puis une réponse écrite par le modèle local, ses étapes, ses sources, les jetons et la durée en pied.
   Refaire avec un autre modèle et noter les deux durées : c'est la première mesure de l'hypothèse des petits modèles.
   Échec : « Sorry, I couldn't answer. », une source qui n'existe pas, plus de deux minutes sans réponse. Défaut connu :
   l'étape « Searching the Brain OS ».
9. Cortex écrit : « Create an issue "Cortex test" in », suivi du nom du projet. À voir : l'issue créée tout de suite, sans
   demande, à son nom. À noter : ni règle ni dossier pour cette écriture (notes du secrétariat). Échec : l'issue créée
   dans un autre projet que celui nommé.
10. Les agents, dans la section Agents de Settings. À voir : Claude Code (« version …, signed in »), Git, GitHub
    (« signed in as … »), et « Ready: delegate an issue to Claude Code… ». Défaut connu : la version minimale n'y est pas
    contrôlée ; si l'étape 2 a donné moins de 2.1.295, l'étape 11 finira en « Agent failed », avec « Claude Code 2.1.295
    or later is needed for the rules to hold ».
11. Déléguer : dans un projet relié à un dépôt privé de test, créer l'issue « Add a line to the README saying the harness
    is on », puis, dans le menu Assignee, « Delegate to an agent » et Claude Code. À voir : « Delegated to Claude Code »,
    « Waiting for your runner to pick it up (claude-code)… », puis « Agent working on it (claude-code)… » ; « Show
    activity » qui grandit ; un badge sur l'icône AI Workflows, et l'issue en « Running » dans la section Delegations
    d'AI Workflows. Noter le temps entre le clic et la première activité (Saarinen). Échec : rien après une minute ; une
    action faite qui n'apparaît pas dans l'activité.
12. Une demande : dans une deuxième issue, demander une tâche qui exige le web (« Search the web for what changed in MQTT
    5.0 and summarize it in a comment »). À voir : sur l'issue, « Claude Code asks to run … », avec Allow, Deny et « …
    min left, then it is denied » ; « Approval needed » dans l'onglet All de Signals ; une notification de Windows si la
    fenêtre n'est pas devant. Cliquer Deny. À voir : « Denied: the agent goes on without it », et l'agent continue sans
    le web. Échec : la recherche part sans demande ; la demande n'arrive nulle part ; Deny reste sans effet. À noter : la
    demande n'est pas dans Mentions (prévu en phase 2).
13. L'échéance : refaire l'étape 12 sans répondre. À voir, au bout de 10 minutes (valeur par défaut du runner, à vérifier
    dans l'app desktop) : « No answer in time: denied ». Échec : l'action part.
14. Le résultat, à la fin du run de l'étape 11. À voir : « Agent done - ready for your review », le résumé de l'agent,
    « View result » qui ouvre la pull request d'une branche `tf/…` poussée sur le dépôt privé, et l'issue dans la colonne
    « In review by AI ». Échec : une branche poussée hors de `tf/…` ; une pull request annoncée mais absente. À noter :
    aucun bouton pour appliquer, réessayer ou écarter (la carte vient au jour 3) ; « In review by AI » se lit à
    l'envers (Norman).
15. Facultatif, une sortie sans retour, dans l'app desktop seulement et jamais en prod tant que R33 (séance n°5) attend :
    refaire l'étape 11 sur un dépôt public créé pour l'essai. À voir : une demande avant le push ; cliquer Deny ; puis
    « not pushed » dans le résumé, et les commits restés sur la branche locale. Échec : un push vers le dépôt public sans
    demande. Défaut connu : la demande s'affiche « Claude Code asks to run git push », alors que c'est TaskForce qui
    demande.
16. Le dossier : sous le run, « Download the record: JSON · Markdown ». À voir, dans le Markdown : la demande, l'agent et
    son modèle, la version des règles, chaque action et sa règle, les demandes et leurs réponses, la fin, et si la chaîne
    tient. Puis, dans `taskforce-runner`, `npm run verify -- <fichier>.json` : vert ; changer un caractère du fichier et
    relancer : rouge, au bon événement. Échec : « No record for this run » ; une action de l'activité absente du dossier ;
    une copie modifiée acceptée.
17. Le mode dégradé d'aujourd'hui : quitter Ollama, puis reposer la question de l'étape 8. À voir : les notes trouvées et
    « AI unavailable », sans erreur. Relancer Ollama, déléguer une tâche, fermer l'app pendant qu'elle travaille, la
    rouvrir. À voir : le run en échec avec sa cause, rien de sorti, son dossier téléchargeable. Échec : un écran figé ; un
    run qui reste « Running » ; une sortie faite après la fermeture. Défaut connu : Cortex dit « AI is not configured »
    alors que le modèle est seulement arrêté.

**La webapp**

18. Ouvrir la webapp, en local dans Docker (`http://localhost:3000`, compte de test du seed), ou en prod une fois la
    release 1.5.0 déployée, et refaire les étapes 5 et 6. À voir en plus, ce qui n'existe que sur la webapp : Members dans
    le menu, Teams dans un projet, GitHub et Slack dans Integrations, Security dans Settings, et pas de section AI. Taper
    `/<espace>/brain` dans l'adresse. À voir : une page 404. Échec : un élément retiré qui revient ; « Brain OS » à
    l'écran ailleurs que dans les étapes de Cortex.
19. Cortex sur la webapp : refaire l'étape 8. À voir : une réponse du fournisseur de l'instance (en local, Ollama de la
    machine par défaut ; en prod, celui de sa configuration, à vérifier), et la consommation dans la section Cortex usage
    de Settings. Échec : « Monthly AI limit reached » dès la première question ; une réponse sans source alors que des
    notes existent.
20. Si un runner est relié à cette instance (section Agents de Settings, runner lancé à la main) : refaire les étapes 11,
    12 et 16, en prod sur un dépôt privé seulement, tant que R33 (séance n°5) attend. À voir : le même comportement que
    dans l'app desktop. Défaut connu : l'aide du runner affiche « Needs Claude Code 2.1.293 or later ». Échec : une règle
    qui juge autrement que dans l'app desktop.
21. Ce qu'il ne faut pas attendre : le run fait dans l'app desktop n'apparaît pas dans la webapp (deux bases ; seul le
    transfert de projet copie un projet d'un côté à l'autre) ; ni l'import de documents (jour 2), ni l'agent interne sur
    un petit modèle (jour 3), ni la carte (jour 3).

**Après**

22. Écrire chaque hésitation avec l'écran qui l'a causée (Norman), compter les notifications reçues quand rien n'attendait
    (Harris), relire le pronostic (Zhuo). En cas d'échec : « Open logs folder », dans la section Account de Settings, et
    `runner.log` pour une délégation.

## Décision de la Présidence

Les décisions de Jobs valent par délégation ; la Présidence garde le dernier mot.

| # | Décision | Raison, dans les mots de la Présidence |
| --- | --- | --- |
| J1 à J9 | Retenues telles quelles | « les décisions de jobs on les garde tel quelle » |
| D1 à D11 | Comme Jobs les a tranchées (J1 à J9) | Même décision |

## Notes du secrétariat

- **Formation** : cinq membres de trois pôles ; Pont et Science manquent, contre la règle d'un membre par pôle (§5). Le
  dossier porte R16 à R26, retenues après la revue où siégeaient Bengio, Hamilton et LeCun : l'atelier dessine dans ces
  limites et n'en amende aucune.
- **Harris** siège comme garde-fou, et s'abstient sur le classement des flows (hors champ). Ses positions publiques
  visent l'IA grand public, peu les outils de travail (fiche) : leur transposition à Cortex est une hypothèse.
- **La délégation à Jobs** est un choix de la Présidence pour cette séance. Elle ne change pas la charte, où la Présidence
  décide seule (§2, point 4) : les décisions de Jobs sont déléguées, sous son dernier mot, et ne sortent pas du labo sous
  son nom (§8, point 3).
- **Siège historique et anachronismes** : Jobs, mort en 2011, ne connaît Cortex, Ollama, Claude Code ni les agents que
  par le dossier ; ses positions sont des transpositions de ses principes documentés. Tension relevée : il accepte qu'un
  seul geste applique toutes les sorties qui se défont, quand sa fiche porte « redemander à chaque fois ». Cette position
  de la fiche vise le consentement à l'usage des données, et chaque sortie définitive reste demandée à part :
  le secrétariat n'y voit pas d'écart à la fiche.
- **Écart à la fiche** : aucun relevé.
- **Conflits d'intérêts** : Saarinen dirige Linear, concurrent direct de TaskForce ; « l'issue est la surface », la
  grammaire de la délégation (D7) et un agent appelé par `@` dans les commentaires sont aussi ce que Linear vend. Zhuo
  rejoint Meta avec le rachat de Sundial (23/10/2026).
- **Extrapolations** : Zhuo n'a pas de position publique sur les outils professionnels ni sur les bacs à sable ; ses
  avis sur la carte prolongent sa critique de produit. Saarinen n'a pas de position trouvée sur les actions
  irréversibles ; sa critique vise la validation pas à pas.
- **Charte §6, point 5** : chaque recommandation porte sa preuve en dix jours et son signal d'arrêt.
- **La spécification** : si la Présidence retient J3, le §15 (« accepter, refuser, demander une reprise ») est à aligner
  sur les mots de R22, par une tâche ou un ADR, pas depuis le labo.
- **Hors du champ de l'atelier**, pour le chantier du harnais (Bengio, LeCun) : les écritures internes de Cortex (une
  issue, un projet, une note) ne passent ni par les règles ni par un dossier, et s'attribuent à la personne ; la table
  par défaut classe la création d'une issue en sortie réversible, autorisée et tracée. Le jour 3 étend la boucle de
  Cortex aux missions : la question se posera alors.
- **Écarts constatés dans le code au 28/10/2026**, qui sont des faits et non des recommandations : « Brain OS » dans les
  étapes et les réponses de repli de Cortex (R22 incomplète) ; l'aide du runner de la webapp à 2.1.293 ; l'écran Agents
  de l'app desktop sans contrôle de la version minimale ; les logos de GitHub et de Slack sur la pilule de l'accueil dans
  l'app desktop (R12) ; les demandes des agents hors de Mentions ; une issue déléguée sans assigné qui le reste ;
  « Claude Code asks » pour les sorties du runner ; « AI is not configured » quand le modèle est seulement arrêté.
- **Le dessin** : les chiffres de la carte sont des exemples. Il ne s'appuie sur aucune bibliothèque de références
  (Mobbin, Lapa Ninja), que cite la spécification (§15) : non consultées pendant la séance.
- **La release** : le bloc de la roadmap sur la 1.5.0 a été lu sur le disque, en cours d'écriture par une autre session,
  non commité.
- **Non vérifié par le secrétariat** :
  - l'app n'a pas été lancée : tout ce que le parcours dit voir est lu dans le code, aucun écran n'a été observé ;
  - que la fiche modale recouvre bien le panneau de Cortex à l'écran : déduit des classes du voile et du panneau ;
  - le fournisseur de Cortex dans la webapp : Ollama de la machine hôte par défaut en local (`docker-compose.dev.yml`),
    mais `.env.dev` peut le changer ; en prod, non lu ;
  - la publication de « Desktop - Release » 1.3.0 et la release 1.5.0, en cours ;
  - la durée d'une demande dans l'app desktop : 10 minutes par défaut dans le runner, aucun réglage trouvé dans la coque,
    rien d'observé ;
  - le message exact d'un run arrêté par la fermeture de l'app, et le rendu de « AI unavailable » dans la réponse de
    repli ;
  - la version de Claude Code installée sur le poste de la Présidence (2.1.293 selon la roadmap, avant mise à jour), et
    ses modèles Ollama ;
  - l'enchaînement réel de `PreToolUse` et de `PermissionRequest` avec Claude Code 2.1.295 ou plus (spécification §21) ;
  - les « vérifications de l'agent en PASS » vues le 28/10 dans le navigateur (roadmap) : le code n'a pas de composant
    de contrôles ; `[DÉDUIT]` c'était le texte du résumé de l'agent de substitution.

## Suites

- La Présidence tranche les décisions de Jobs (J1 à J9) et D1 à D11.
- Ce dessin solde le reliquat du jour 1 relevé par la séance n°5 : le jour 3 code la carte au plus simple d'après lui
  (R13, spécification §18) ; ce qui n'y tient pas va en phase 2, dans l'ordre du classement (D4).
- Le parcours de test se joue dès que l'app desktop 1.3.0 s'installe ; ses défauts se rangent par rang de flow.
- Après la décision, et hors de cette séance, qui ne devait produire que ce procès-verbal : l'entrée du Journal ; la ligne
  du registre (charte §12) ; les preuves en dix jours retenues, dans `experiences/Experiences.md` ; un brouillon d'ADR
  dans `decisions/` si J1 est retenue, puisqu'elle engage le produit (Cortex comme entrée, un seul panneau à droite) ; le
  glossaire de l'interface (R22).
