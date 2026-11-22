---
id: conseil-seance-2026-11-17-preciser-avant-de-trancher
title: "Séance n°29 du 17/11/2026 : préciser avant de trancher, la concurrence, le pivot"
doc_type: pv-seance
statut: active
date: "17/11/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, precisions, concurrence, signaux, pivot, preuve, dossier, accords, processus, mots]
related:
  - "../README.md"
  - "./2026-11-17-finir-la-v1.md"
  - "./2026-11-17-le-recentrage.md"
  - "./2026-11-13-le-marche-a-prendre.md"
  - "./2026-11-13-depasser-camunda.md"
  - "./2026-10-27-vision.md"
  - "./2026-10-26-premiere-regle.md"
  - "../../decisions/ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "../../decisions/ADR-025-DRAFT-un-seul-moteur-de-regles.md"
  - "../../decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../../decisions/ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md"
  - "../../decisions/ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md"
  - "../../experiences/Experiences.md"
  - "../../Questions-ouvertes.md"
---

# Séance n°29 du 17/11/2026 : préciser avant de trancher, la concurrence, le pivot

> Simulation : les membres sont des personnages simulés, à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **En bref.**
>
> **Ce que la séance fait** : la Présidence a lu les neuf recommandations de la n°28. Elle en retient une (R204), demande
> des précisions sur les huit autres avant de trancher, et une analyse de la concurrence. Elle ajoute qu'elle pivotera
> s'il le faut, « juste qu'on aille pas dans le mur ».
>
> **Deux faits de la n°28 sont corrigés.** La boîte à outils de Microsoft, sous MIT, décrit des reçus de décision signés,
> chaînés et vérifiables hors ligne. L'API de conformité d'Anthropic couvre Claude Code depuis le 11/08/2026, sans
> signature annoncée. La phrase de la n°28, « aucune ne vend un dossier signé et vérifiable hors de l'outil : c'est la
> place », ne tient plus pour la décision d'une règle. Elle tient pour le dossier entier d'une tâche, avec l'accord humain,
> installé chez le client.
>
> **Le verdict sur la concurrence : la place se prend, plus étroite, et elle s'ajuste.** Faire travailler les agents
> « sous ses règles » ne se vend plus : cela se donne. Ce qui reste libre, dans les pages lues, tient en trois choses que
> personne n'assemble : l'accord humain daté dans le même dossier que l'action, l'installation chez le client avec des
> modèles locaux, le code ouvert. TaskForce est aujourd'hui derrière JFrog et Microsoft sur ce qu'il veut vendre : il lui
> manque la demande, le modèle et la signature. La fenêtre est une hypothèse : six à douze mois.
>
> **Ce que le terrain dit, et ce qu'il ne dit pas.** La douleur la plus nommée par des gens qui ne vendent rien n'est pas
> la preuve : c'est la revue qui ne suit plus le volume de ce que les agents écrivent, puis les contrôles écrits pour des
> humains qu'il faut réécrire. La fatigue des accords est le signal le plus solide. Les grands comptes régulés règlent
> tout cela eux-mêmes. Sur les équipes de 10 à 250 personnes, le terrain public est muet.
>
> **Pas de pivot aujourd'hui : un ajustement, et un pivot écrit d'avance.** La couche reste. Sa porte d'entrée devient le
> tri du travail des agents par les règles de l'entreprise (le courant part seul, le lourd attend la bonne personne) ; ce
> qu'elle vend reste le dossier complet de chaque tâche. Si l'un des trois signaux surveillés se déclenche, TaskForce se
> replie sur la preuve du travail des agents de code dans le logiciel validé (GxP), comme source de preuve pour les outils
> que l'auditeur lit déjà : c'est là qu'est le premier client test.
>
> R196 est remplacée par R205 ; R197 à R203 sont amendées ; deux recommandations nouvelles, R206 (face à la concurrence) et
> R207 (les signaux et le repli écrit). Toutes à 90 % au moins, R199, R205, R206 et R207 au second tour. Les onze non
> et abstentions de la n°28 sont développés ; dix deviennent des oui, Jobs passe du non à l'abstention. Arati Prabhakar,
> contradictrice, a obtenu que chaque affirmation de la phrase renvoie à un essai, et que chaque signal ait quelqu'un qui
> le regarde et une date.

- **Saisine** (Présidence, 17/11/2026, en conversation, mot pour mot) :
  - « R196 : une niche d'une niche ouais je suis d'accord mais Musk, tu voudrais construire toi niveau logicielle ajd en
    2027 (presque) ? De quoi as tu besoin ? De quoi tes colleges ont besoins ? Ou sont les pains ? Peux t'on les resoudre
    via des logicielles ? Si oui c'est quoi les sujets ?
  - R197 : hmm oui jesuis d'accord aussi Musk mais c'est ce qu'on souhaite vendre aussi, genre je vais pas aller voir une
    entreprise pour leur demander : bon alors c'est quoi vos pain ajd ? Nan je dois observer, analyser, comprendre, avoir
    une vision et l'enclencher, toute les boites ne vont pas utiliser mon produit c'est sur
  - R198: oui mais c'est justement ca le systeme de preuve
  - R199: Comment ca Jobs, et juste Claude les abstention faut etre plus precis plutot que balancer des punchline comme ca
    mdr. Donc Jobs ce que tu me dis c'est que l'experience se joue chez l'hote donc on perd le controle on maitrise plus ?
    Ou c'est ce que toi tu voudrais je comprends pas. les conflits d'interet je m'en moque
  - R200: ok ok, en gros c'est cammunda version compliance quoi, ca me va en soit, mais faudrait faire compliance,
    reglementation, convention, ...
  - R201: Bah la fatigue des demandes d'accord oui donc si il peut le faire lui mm go
  - R202: comment ca arreter le mot souverain et conforme ?
  - R203: les abstention faut les developper mdr, genre pk
  - R204: Ok
  - precise les points la avant que je tranche le reste stp. Et fait une analyse concurentielle, va chercher des postes
    pour jsutifier qu'on peut prendre cette place et tout, et j'ai aucun pb a pivoter de fou si necessaire quoi, juste
    qu'on aille pas dans le mur »
  - **Ce que le secrétariat en retient**, et qu'il dit comme tel :
    - **R204 est retenue** par la Présidence (« R204 : Ok »). Le lot des six correctifs a démarré le 17/11/2026. Elle ne
      se rediscute pas ici.
    - **« Les conflits d'interet je m'en moque »** : pour cette séance, un membre en conflit d'intérêts le déclare, puis
      vote sur le fond et dit pourquoi. Aucune abstention « par conflit d'intérêts ». C'est une consigne de la Présidence
      pour la séance (charte, §2.5), pas un changement du règlement.
    - **« Les abstention faut les developper »** : chaque non et chaque abstention, à la n°28 comme ici, se développe en
      trois points : ce que le membre conteste exactement, ce qui le ferait voter oui, ce qu'il propose à la place. Plus
      de formule d'une ligne.
    - La Présidence dit son accord avec Musk sur deux points (R196, R197) et pose des questions à Musk et à Jobs. Les
      membres s'adressent à la question, pas à la Présidence (charte, §2.3) : ils répondent sur le fond.
  - **Les questions à traiter** :
    1. les précisions sur R196 à R203, une par une, dans l'ordre de la saisine ;
    2. l'analyse concurrentielle et les signaux du terrain : peut-on prendre la place, contre qui, pendant combien de
       temps ; ce qui ferait aller dans le mur, et les signaux d'alerte ;
    3. le pivot, s'il le faut : la place de R196, ses ajustements et les places voisines, comparés sur les mêmes critères.
  - **Horizon** : J2 et E20, le premier client test, puis 2027. Aucune date ne court avant le client test (décision de la
    Présidence sur la séance n°26).
- **Formation** : séance n°29, plénière (24). Elle prolonge la n°28, qui l'était, et touche le positionnement (charte, §5).
  - Impulsion : Steve Jobs, Elon Musk, Jeff Bezos, Gwynne Shotwell.
  - Pont : Satya Nadella, Mariana Mazzucato, Arati Prabhakar, Kenza Ait Si Abbou.
  - Harmonie : Margrethe Vestager, Audrey Azoulay, Nandan Nilekani, Tristan Harris, Yuval Noah Harari.
  - Science : Yoshua Bengio, Yann LeCun, Fei-Fei Li, Margaret Hamilton, Daniela Rus, Jennifer Doudna, Esther Duflo, Atul Gawande.
  - Design : Don Norman, Julie Zhuo, Karri Saarinen.
  - **Contradictrice** : Arati Prabhakar. Elle n'a jamais tenu ce rôle (vérifié au registre de la charte, §12 : Mazzucato,
    Azoulay, Nilekani, Li et Rus non plus). Son angle (par quel essai montre-t-on qu'une chose marche, quel seuil écrit-on
    avant de regarder, qu'est-ce qui ferait renoncer) vise le consensus attendu : « la place se prend, il suffit de
    l'ajuster ». Elle doit l'attaquer même si elle le partage. Vestager l'était à la n°28.
  - **Ordre de parole**, tiré au sort le 17/11/2026 à 13:49 UTC (`shuf`) : Yuval Noah Harari, Tristan Harris, Yann LeCun,
    Karri Saarinen, Satya Nadella, Elon Musk, Atul Gawande, Margaret Hamilton, Arati Prabhakar, Jeff Bezos, Steve Jobs,
    Daniela Rus, Fei-Fei Li, Julie Zhuo, Jennifer Doudna, Kenza Ait Si Abbou, Margrethe Vestager, Gwynne Shotwell, Don
    Norman, Audrey Azoulay, Yoshua Bengio, Esther Duflo, Mariana Mazzucato, Nandan Nilekani.
  - **Règle de vote** (charte, §6.5) : 90 % des présents, soit 22 oui sur 24 au moins.
- **Fiches** : aucune fiche rafraîchie. Vérifié ce jour dans `taskforce-docs` (`feature/lean-oss`, `347b7f1`) : toutes ont
  moins de 30 jours au 17/11/2026. La plus ancienne date du 21/10/2026, soit 27 jours ; Norman, Zhuo et Saarinen datent du
  28/10, Ait Si Abbou du 26/10, les vingt autres du 21/10. Jobs et Hamilton, sièges historiques, ne se rafraîchissent que
  sur une nouvelle source historique. À partir du 21/11/2026, vingt fiches passeront les 30 jours. Les intérêts déclarés
  (Musk, Nadella, Bezos, Saarinen, Zhuo) sont aux notes du secrétariat.

## Dossier

Constitué le 17/11/2026 par le secrétariat. Il repart du dossier de la n°28 (D1, D2, D3, la recette de la 1.17.0, le code de
`dev` au commit `067c577b`, en lecture seule) et y ajoute deux recherches faites pour cette séance, sur des pages publiques
seulement, sans connexion ni formulaire : **D4**, la concurrence, et **D5**, les signaux du terrain. Leurs étiquettes sont
gardées telles quelles. Leurs limites, telles que leurs auteurs les signalent :

- **D4** : une page ou un communiqué d'éditeur établit ce que l'éditeur annonce, jamais ce que son produit fait. Les levées
  et les revenus sont des annonces ou des estimations. La fenêtre de temps est une hypothèse. Des pages ont été lues par
  l'outil de recherche sans être rouvertes ; aucun prix public n'a été trouvé pour Docker AI Governance, Drata, Zenity ni
  Ketryx.
- **D5** : Reddit était fermé à l'outil de recherche, et aucun post LinkedIn n'a été lu sans connexion. Le terrain lu est
  Hacker News, des blogs, la presse professionnelle, des conférences rapportées et des offres d'emploi ; les pages lues
  par extrait seulement sont marquées. Les propos sont reformulés, aucun n'est une citation. Sur les onze signaux de
  preuve, sept viennent de vendeurs ; aucun auditeur ni responsable qualité ne parle à la première personne. Le terrain
  public est muet sur les 10 à 250 personnes. D5 garde des adresses pour la vérification : ce PV n'en publie aucune. Un
  signal se cite ici par son support, sa date et le rôle de son auteur, avec son numéro dans D5 (S1 à S52, C1 à C12).

La saisine couvrant trois questions, le dossier compte douze points et deux pièces du secrétariat.

1. **Deux faits de la n°28 corrigés** (D4, 2.0 ; relus par le secrétariat ce jour).
   - `[ÉTABLI]` Le dossier de la n°28 (point 4) disait de la boîte à outils de Microsoft que l'annonce « ne dit rien de
     journaux signés ou chaînés ». C'était vrai de l'annonce du 02/04/2026. La documentation décrit aujourd'hui des reçus de
     décision vérifiables hors ligne : signature Ed25519 sur JSON canonique (RFC 8785), chaque reçu portant l'empreinte du
     précédent, vérification par un script sans réseau, export possible en provenance SLSA. Le reçu contient l'outil appelé,
     la décision de la politique Cedar, l'identifiant de la politique et l'identité de l'agent. La page ne dit pas qu'il lie
     la demande, l'accord humain, le résultat ou le modèle, ni où vit la clé
     ([Microsoft, « Tutorial 33: Offline-Verifiable Decision Receipts »](https://microsoft.github.io/agent-governance-toolkit/tutorials/33-offline-verifiable-receipts/),
     sans date, lu le 17/11/2026).
   - `[ÉTABLI]` Le dossier de la n°28 (D2) rapportait que l'API de conformité d'Anthropic ne couvrait pas les sessions
     locales de Claude Code. L'article d'Anthropic du 11/08/2026 dit qu'elle couvre Claude Code en ligne de commande et dans
     l'app de bureau : une transcription par session (prompts, réponses, activité des outils), avec l'identité vérifiée de
     l'utilisateur, pour l'offre Enterprise. Rien sur une signature. Exclus : Claude Code sur le web et les sessions passées
     par Bedrock, Vertex ou Foundry
     ([Anthropic, 11/08/2026](https://claude.com/resources/articles/compliance-api-cowork-and-claude-code)).
     `[À VÉRIFIER]` Un article d'aide d'Anthropic dit encore que les transcriptions des sessions locales restent sur le
     poste : les deux pages ne s'accordent pas.
   - `[DÉDUIT]` **Ce que cela change à la n°28** est à la pièce 1.
2. **Les plateformes** (D4, 2.1).
   - `[ÉTABLI]` Microsoft publie aussi un paquet « Claude Code governance » : un plugin avec des hooks au début de session,
     à l'envoi du prompt et avant chaque appel d'outil, et un journal dans le dossier personnel de l'utilisateur
     ([Microsoft](https://microsoft.github.io/agent-governance-toolkit/packages/claude-code-governance/)). `[HYPOTHÈSE]` Un
     journal à cet endroit est à la portée de l'agent. `[À VÉRIFIER]` Une décision d'architecture au statut « proposed »
     (11/06/2026, lue par l'outil de recherche) prévoit un accord humain lié à l'action exacte, sans accord par expiration
     du délai : la pièce qui manque au reçu est écrite comme proposition.
   - `[ÉTABLI]` GitHub : l'agent Copilot dans le cloud signe ses commits depuis le 03/04/2026, ce qui prouve l'auteur et
     non la justesse ([GitHub](https://github.blog/changelog/2026-04-03-copilot-cloud-agent-signs-its-commits/)) ; le
     journal d'audit garde 180 jours ; les prompts, réponses et contenus d'outils ne sont pas collectés par défaut ; le
     billet d'Universe 2026 n'annonce ni dossier signé par tâche ni attestation de provenance propre aux agents.
     `[HYPOTHÈSE]` (D4) GitHub tient l'issue, la revue, le commit et la signature ; il lui manque de les assembler.
   - `[ÉTABLI]` AWS : Policy d'AgentCore juge chaque appel d'outil et journalise toutes les évaluations depuis le
     17/06/2026 ; CloudTrail sait valider l'intégrité de ses journaux. En ligne, à l'usage, pas sur site.
   - `[ÉTABLI]` OpenAI : l'API de conformité exporte les prompts et les réponses de Codex, gardés 30 jours au plus ; rien
     sur une signature (lu par l'outil de recherche).
3. **Les offres les plus proches du dossier par tâche** (D4, 2.1).
   - `[ÉTABLI]` **JFrog** (billet du 12/10/2026, relu par le secrétariat) : une initiative ouverte, « Agentic Process
     Evidence », et une fonction d'AppTrust, « Prompt to Release Traceability », qui selon JFrog « already implements this
     evidence layer ». Chaque processus d'agent produit un enregistrement signé (in-toto, DSSE) : versions de l'agent et
     du harnais, modèle, outils, propriétaire responsable, relecture humaine ou non, journaux de session, attaché au commit
     ou à la release. Agents visés : Cursor, OpenCode, Claude Code. Le billet écrit : « No widely adopted standard yet
     captures agentic provenance », et ne donne ni date de disponibilité ni prix
     ([JFrog, « Governing the Agentic SDLC »](https://jfrog.com/blog/governing-the-agentic-sdlc/)). C'est l'annonce d'un
     éditeur coté, qui vend aussi sur site.
   - `[ÉTABLI]` **Entire** : 60 M$ d'amorçage annoncés le 10/02/2026 ; un outil en ligne de commande sous MIT lie chaque
     commit à la session d'agent qui l'a produit ; depuis le 10/11/2026, un historique « cryptographically verifiable » des
     références git ; aucune offre payante affichée. Il garde la demande, l'action et le modèle ; ni la règle ni l'accord.
   - `[ÉTABLI]` **Drata** : « AI Agent Governance », en accès limité depuis le 04/08/2026, d'abord pour les agents sur
     Anthropic ; le communiqué promet « evidence collection for all actions taken by AI agents »
     ([Drata](https://drata.com/about/news/drata-extends-trust-management-platform-to-continuously-monitor-and-govern-ai-agents)).
     **Vanta** : 65 contrôles rattachés à ISO 27001, ISO 42001 et AIUC-1 ; la page ne dit pas qu'il recueille le journal de
     ce qu'un agent a fait.
   - `[ÉTABLI]` **Docker AI Governance** (12/05/2026) : des bacs à sable en micro-VM et des règles sur le réseau, les
     fichiers, les secrets et les outils MCP, les mêmes sur le poste et dans le cloud ; chaque évaluation produit un
     événement exporté ; la page ne parle pas de signature
     ([Docker](https://www.docker.com/blog/docker-ai-governance-unlock-agent-autonomy-safely/)).
   - `[ÉTABLI]` Le reçu signé devient courant : un kit sous MIT signe chaque action, sans financement ni client trouvé ;
     d'autres petits projets libres font de même pour MCP. `[ÉTABLI]` AIUC a levé 40 M$ (15/09/2026) pour un standard
     d'audit des agents, AIUC-1, calqué sur SOC 2 : pas un concurrent, un futur prescripteur de preuves.
   - `[ÉTABLI]` Les éditeurs de la validation sous GxP (Kneat, ValGenesis, Sware) mettent l'IA dans la rédaction des
     documents de validation ; Ketryx annonce un serveur MCP en bêta (31/03/2026) et la traçabilité par Jira et GitHub.
     `[HYPOTHÈSE]` (D4) Aucune page lue ne traite la preuve du travail d'un agent de code, sauf Ketryx en partie.
4. **Le temps qui reste** (D4, 2.2).
   - `[ÉTABLI]` À l'IETF, au moins six brouillons individuels portent sur la preuve des actions d'agents (un format de
     journal, des reçus de décision signés, un profil SCITT, une architecture d'audit, des reçus de permission, des
     événements de refus). Aucun n'est adopté par un groupe de travail
     ([catalogue de l'IETF](https://datatracker.ietf.org/doc/search?name=agent+receipts&activedrafts=on)).
   - `[ÉTABLI]` À l'OpenSSF, une proposition de prédicat « AI authorship » (auteur par plage de lignes, modèle, empreinte
     du prompt, accords humains, enveloppe DSSE) a été ouverte le 30/06/2026 et close le 29/09/2026 sans adoption
     ([OpenSSF, issue 628 du comité technique](https://github.com/ossf/tac/issues/628)).
   - `[ÉTABLI]` CoSAI (document approuvé le 20/03/2026) demande des pistes d'audit protégées contre la falsification.
     `[À VÉRIFIER]` Les conventions d'OpenTelemetry pour les agents restent au statut « Development ».
   - `[HYPOTHÈSE]` (D4) **La fenêtre.** Pour le reçu signé d'une décision : fermée, il est gratuit. Pour le dossier
     entier, en disponibilité générale chez un grand : 6 à 12 mois. Pour un format reconnu par un auditeur : 12 à 24
     mois. Pour « sur site, 10 à 250 personnes » : plus longue, sans qu'on sache si c'est un vide ou une absence de
     demande.
5. **Ce qui ferait aller dans le mur** (D4, 2.4).
   - `[ÉTABLI]` Des outils de développement libres sans revenu : Earthly a cessé de maintenir son projet libre et cite la
     cannibalisation par son propre outil gratuit
     ([Earthly](https://earthly.dev/blog/shutting-down-earthfiles-cloud/)) ; Kite a fermé en 11/2022 avec 500 000
     développeurs actifs qui ne payaient pas ; Continue (34 000 étoiles) a été repris par Cursor en 06/2026 et son dépôt
     est en lecture seule (deux sources secondaires).
   - `[ÉTABLI]` Dans la gouvernance de l'IA, des jeunes pousses ferment ou sont absorbées : Codified a fermé en 2025 ;
     FairNow a été absorbé en 03/2026, trail ML le 05/10/2026. `[HYPOTHÈSE]` (D4) L'issue courante est l'absorption par un
     outil qui tient déjà l'acheteur.
   - `[À VÉRIFIER]` Un éditeur de conformité est accusé depuis 03/2026 de produire des preuves d'audit pré-remplies ; il
     conteste (sources secondaires). Le risque est direct pour qui vend de la preuve.
   - `[À VÉRIFIER]` Des témoignages de forums : le questionnaire de sécurité demande un SOC 2 de type II dès la première
     ligne ; un fournisseur d'une personne est un point de défaillance unique. Aucune donnée systématique. D4, comme D3,
     n'a trouvé aucun exemple public d'une personne seule vendant cela à des entreprises régulées.
   - `[HYPOTHÈSE]` (D4) Le risque premier n'est pas d'être battu : c'est d'être adopté sans être payé, ou absorbé comme
     une fonction.
6. **Les douleurs que le terrain nomme, par nombre de sources lues** (D5, section 6 ; le classement reflète les lectures,
   pas le marché).
   - `[ÉTABLI]` La revue ne suit plus le volume : six sources, dont une analyse de 8,1 millions de pull requests (celles
     d'une IA attendent 4,6 fois plus et sont acceptées à 32,7 % contre 84,4 %) et le témoignage, à une conférence de début
     2026, du responsable de la stratégie d'ingénierie d'une grande banque américaine : la revue par les pairs devient le
     goulot, les commits ont environ doublé (D5, S43, S16).
   - `[ÉTABLI]` Puis : l'empilement des SaaS (S44) ; le coût et le retour de l'IA, avec des budgets annuels d'outils de
     code fondus en quelques mois `[À VÉRIFIER]` (S45) ; les agents que la sécurité ne voit pas (S46, presque toutes des
     sources d'éditeurs) ; le vieux code qui bloque l'IA (S47) ; l'entretien de ce que l'IA a construit (S48) ; la
     conformité en mille morceaux, que la liste d'automne 2026 d'un grand accélérateur nomme pour la finance (S49).
   - `[ÉTABLI]` Deux fils de Hacker News, « que faites-vous encore à la main ? » (vers 05/2026, 34 commentaires) et « que
     paierait votre entreprise pour résoudre ? » (vers 12/2025, 18 commentaires), ne citent ni conformité, ni audit, ni
     agents. Dans le second, le thème dominant est la méfiance envers l'éditeur d'une seule personne : un acheteur a exigé
     une version installée chez lui, un autre un séquestre du code (S51, S52).
7. **La preuve du travail des agents : qui la demande** (D5, sections 1, 2 et 7).
   - `[ÉTABLI]` Les récits d'un auditeur qui demande « qui a approuvé ce qu'a fait l'agent » existent, chez des vendeurs ou
     dans des reprises non vérifiables (S1, S2, S4). Aucun texte d'auditeur n'impose une règle propre aux agents de code :
     les guides de cabinets de conformité disent que les critères habituels de gestion des changements s'appliquent, avec
     les preuves habituelles (C7).
   - `[ÉTABLI]` Les grands comptes régulés construisent eux-mêmes. Un responsable d'ingénierie d'un grand groupe de
     services financiers décrit, le 28/10/2026 dans un média technique : des refus gérés au centre, le mode sans
     permissions désactivé, `git push` soumis à accord, des hooks versionnés, chaque commande journalisée, et la pull
     request, la CI et les scans comme dernière porte (S15). Quatre établissements au moins font de même (C8).
   - `[ÉTABLI]` Les développeurs accueillent mal la session attachée au commit : trois fils de Hacker News (1 208
     commentaires au total, premier tiers lu) penchent vers « du bruit », « git le fait déjà », la crainte d'exposer une
     session privée (C1, C2, C3).
   - `[ÉTABLI]` Un fil de Hacker News sur un outil ouvert de preuve chaînée (vers 07/2026, 23 commentaires) : une chaîne que
     l'opérateur détient ne prouve rien, il peut la réécrire ; aucun témoin tiers (C5).
   - `[ÉTABLI]` En sciences de la vie, aucun responsable validation ne raconte publiquement l'usage d'un agent de code sur
     un système BPF (S20). Le dirigeant d'un cabinet de conseil écrit, dans la presse pharmaceutique des 23/03 et
     06/04/2026, qu'un inspecteur demandera si les exigences existaient avant le code, quel prompt et quelle version de
     modèle (S12, un auteur intéressé). Un cabinet de conseil réglementaire en dispositifs médicaux écrit le 27/04/2026 que
     le régulateur ne regarde pas le code mais le dossier de traçabilité (S13).
8. **La fatigue des accords** (D5, section 4 : sept sources de même sens).
   - `[ÉTABLI]` L'éditeur d'un agent de code publie le 25/03/2026 que 93 % des demandes de permission sont acceptées. Son
     mode automatique, où un classifieur juge chaque action, bloque à tort 0,4 % des actions et laisse passer 17 % des
     actions réellement trop zélées ; l'éditeur dit qu'il ne remplace pas une revue humaine à fort enjeu (S26). Ce mode est
     le défaut depuis le 14/08/2026 (S27).
   - `[ÉTABLI]` Des praticiens indépendants concluent de même : laisser passer le courant, refuser en dur l'interdit, garder
     l'accord humain pour quelques actions lourdes, isoler la machine (S28, S30, S31, S32).
   - `[ÉTABLI]` La leçon que les victimes d'incidents tirent est le confinement, pas la preuve : un jeton trop large, des
     sauvegardes au même endroit (S21, S22).
9. `[ÉTABLI]` **Ce que le code fait déjà des classes d'actions** (lu par le secrétariat ce jour, `067c577b`).
   - Les trente règles par défaut (`resources/harness/default.rules.json`) autorisent sans accord les lectures, les
     écritures dans la copie de l'agent, et cinq écritures dans TaskForce, chacune avec l'action qui la défait : créer une
     issue (la fermer), la modifier (la restaurer), commenter (supprimer le commentaire), créer un projet (l'archiver),
     créer une note (la supprimer).
   - Toute écriture dans un outil externe (`mcp.write`) demande un accord, et le socle la classe irréversible dans son code
     (`RulesFloor.java`, ensemble `ONE_WAY`), quel que soit l'outil : créer un commentaire dans Linear et supprimer un
     espace y pèsent pareil. Une règle de l'entreprise ne peut pas la relâcher : le socle ne fait que durcir.
   - Une sortie déclarée réversible sans action inverse n'est pas tenue pour réversible (`RulesFloor.reversible`).
   - L'action inverse est un nom déclaré dans la règle (`close-issue`, `delete-comment`). Le secrétariat n'a trouvé, dans
     la copie du code, aucun geste qui l'exécute sous ce nom : « annulable » est déclaré, pas encore montré comme un geste.
     `[À VÉRIFIER]` sur l'app.
10. `[ÉTABLI]` **Les règles déjà retenues que la séance doit respecter.**
    - R1 (séance n°1) : aucun agent ne décide seul d'une action irréversible, ni de ce qui est irréversible.
    - R7' (séance n°2) : tout est tracé, seul l'irréversible attend ; les lectures passent sans validation et laissent une
      trace.
    - R187 (séance n°26), retenue par la Présidence le 13/11/2026 : aider à prouver, jamais « conforme ». Ses mots : « on
      donne rien dans notre app, on fournis l infra et l archi qui permette de faire ca ». R179 et le brouillon d'ADR-022
      disent la même chose : TaskForce fournit l'infrastructure et l'architecture, jamais le contenu réglementaire.
    - La n°28 établit sur « souverain » : aucun label européen ne le définit (l'EUCS n'est pas adopté, le Cloud and AI
      Development Act est une proposition), et l'hébergement de la prod n'est pas choisi.
11. `[ÉTABLI]` **Les contraintes du terrain.** Une personne, la Présidence, et des agents ; pas de revenu ; le premier client
    test passe d'abord ; J2 ne prend que W0 à W5 ; l'hébergement de la prod reste à choisir ; aucun contenu réglementaire.
12. `[ÉTABLI]` **L'état de la n°28.** Elle est publiée (`347b7f1`), sa décision vide. R196 à R204, Q27 à Q30 sont en place ;
    E30 à E32 et le brouillon d'ADR-029 sont proposés, pas inscrits. La numérotation reprend à R205, Q31, E33 et ADR-030
    (vérifié ce jour dans le dépôt et dans le dossier de la n°28).

### Pièce 1 : ce que les deux corrections changent à la n°28 (pièce du secrétariat)

`[DÉDUIT]` Le PV de la n°28 ne se réécrit pas. Ce qui suit dit où il faut désormais le lire autrement.

| Ce que la n°28 écrit | Où | Ce qui tient encore | Ce qui ne tient plus |
| --- | --- | --- | --- |
| « Aucune, dans les pages lues, ne vend un dossier par tâche, signé et vérifiable hors de l'outil. C'est la place. » | En bref ; dossier, point 4 | Aucune page lue ne vend le dossier entier d'une tâche (demande, règle, accord humain, action, résultat, modèle), installé chez le client | Le reçu signé et vérifiable hors ligne de la décision d'une règle existe, gratuit, sous MIT |
| « L'annonce ne dit rien de journaux signés ou chaînés » (Microsoft) | Dossier, point 4 ; notes | C'était vrai de l'annonce du 02/04/2026 | La documentation décrit des reçus signés et chaînés |
| « L'autre moitié, une preuve vérifiable hors de l'outil, tient » | Notes, corrections des documents | Pour le dossier entier | Pour la décision de politique |
| R196 : « fait travailler les agents d'une entreprise sous ses règles et en garde la preuve, vérifiable sans TaskForce » | R196 | « En garde la preuve », si la preuve est le dossier entier avec l'accord humain | « Sous ses règles » n'est plus une place : Microsoft, AWS, Docker et les passerelles la donnent ou la vendent |
| Pièce 2 : « une vraie chaîne, vérifiable hors de l'outil, et c'est rare d'après le point 4 » | Pièce 2, lecture | La chaîne existe et se vérifie | Ce n'est plus rare. Et TaskForce n'a ni la demande, ni le modèle, ni la signature : il est derrière JFrog et Microsoft sur ce qu'il veut vendre |
| R198 : le format, « regarder le brouillon de l'IETF » | R198 ; Q29 | La canonisation selon la RFC 8785 | Un format propre serait le septième : les autres émettent en in-toto et DSSE, ou en reçus Ed25519 |
| Les sessions locales de Claude Code échappent à l'API de conformité du fournisseur | Dossier (D2) | Pour Claude Code sur le web et par Bedrock, Vertex ou Foundry ; `[À VÉRIFIER]` une page d'aide contredit | La transcription d'une session en ligne de commande ou dans l'app de bureau existe chez le fournisseur, pour l'offre Enterprise |

`[DÉDUIT]` **Lecture** : la place de R196 telle qu'écrite était large de deux moitiés. La première, la règle, est occupée. La
seconde, la preuve, se resserre sur ce que le reçu de Microsoft et la transcription d'Anthropic ne portent pas : l'accord
humain lié à l'action, le résultat, et le tout chez le client. R198 reste juste dans son contenu et change de sens : la
signature n'est plus ce qui distingue, c'est ce qu'il faut pour être admis à la table.

### Pièce 2 : les concurrents, colonne par colonne (D4, 2.1)

`[HYPOTHÈSE]` Lecture des pages publiques, donc de ce que les éditeurs annoncent. D : la demande ; R : la règle ; A : l'accord
humain ; Ac : l'action ; Rs : le résultat ; M : le modèle. « p » : en partie ; « ? » : non dit.

| Concurrent | D | R | A | Ac | Rs | M | Signé | Hors outil | Sur site | Libre | Menace selon D4 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft, boîte à outils | non | oui | p | oui | non | non | oui | oui | p | oui | Forte |
| GitHub | oui | p | oui | p | oui | p | p | p | p | non | Forte à 12 mois |
| JFrog AppTrust | p | p | oui | oui | oui | oui | oui | oui | oui | non | Forte |
| Drata | ? | oui | ? | oui | ? | ? | ? | non | non | non | Forte |
| Docker AI Governance | non | oui | non | oui | non | non | ? | non | oui | p | Forte sur la règle |
| Anthropic, OpenAI | oui | p | non ou p | oui ou p | oui | oui | ? | non | non | non | Moyenne |
| AWS AgentCore | non | oui | non | oui | p | p | p | p | non | non | Moyenne |
| Entire | oui | non | non | oui | oui | oui | p | oui | non | p | Moyenne |
| Ketryx | oui | oui | oui | p | oui | ? | p | non | non | non | Moyenne |
| Vanta | non | p | non | non | non | non | ? | non | non | non | Moyenne |
| Zenity, Noma, Lasso, Reco | non | oui | non | oui | non | non | ? | non | non | non | Faible sur la place |
| Observabilité (Langfuse, Arize, LangSmith) | oui | non | non | oui | oui | oui | non | non | p | p | Faible |
| Kneat, ValGenesis, Sware | p | oui | oui | non | p | non | p | non | p | non | Faible, plutôt des canaux |
| Camunda, ServiceNow, UiPath, n8n | oui | oui | oui | oui | oui | p | ? | non | p | p | Faible |
| **TaskForce 1.17.0** (pièce 2 de la n°28) | non | oui | oui | oui | oui | non | non | oui | oui | oui | |

`[DÉDUIT]` **Lecture** (D4) : personne n'a les six colonnes, signées, hors de l'outil, sur site et libres. JFrog en est le plus
près ; Microsoft a la signature et la règle ; GitHub a les pièces sans l'assemblage. TaskForce a l'accord, le sur site et
le code ouvert ; il lui manque la demande, le modèle et la signature.

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre répond d'abord à ce que la saisine lui demande, quand elle lui demande quelque
chose ; puis il nomme la douleur et le sujet logiciel qu'il juge les plus forts, avec le signal de D5 qui les porte. Les
interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Yuval Noah Harari (Harmonie)

- La douleur : un agent agit, et personne ne sait dire ensuite qui en répond. Un consultant rapporte, dans un média pour
  responsables d'ingénierie du 03/08/2026, un post-mortem resté sans conclusion parce que la seule trace du conseil de l'IA
  était un fil de messagerie (D5, S5).
- Le sujet : l'attribution. Chaque action a un auteur, humain ou agent, et une personne qui en répond, dans un écrit qu'on
  relit après.
- Sur R198 : un dossier qui garde la demande et survit à la suppression est aussi une mémoire sur des personnes. Le texte
  d'une demande peut nommer un collègue. Des développeurs craignent déjà qu'une session privée soit exposée (C3).
- *Sa recommandation : le dossier garde les faits ; un contenu sensible y entre par son empreinte, et son texte reste
  effaçable.*

### 2. Tristan Harris (Harmonie) : son abstention sur R201, développée

- **Ce qu'il conteste exactement** : « une carte par écriture » comme premier contrôle. L'éditeur d'un agent de code mesure
  que 93 % des demandes de permission sont acceptées (S26). Une carte acceptée 93 fois sur 100 n'est plus un contrôle,
  c'est un geste ; et quand cela casse, la faute retombe sur celui qui a cliqué.
- **Ce qui le ferait voter oui** : que la carte devienne rare. Elle se réserve à l'irréversible et à ce qu'une règle exige ;
  le reste passe sous des règles décidées d'avance, tracé, annulable.
- **Ce qu'il propose à la place** : mesurer, règle par règle, la part des cartes acceptées. Une règle dont la carte est
  presque toujours acceptée est signalée à une personne, qui la reclasse (elle passe seule, ou elle est refusée). Le système
  ne reclasse jamais de lui-même. Ce qui est passé seul se relit en une fois, pas dans un flux de notifications.
- Sa réserve, depuis sa fiche : « laisser passer le courant » récompense celui qui classe toujours plus de choses en
  courant. Chaque changement de classe est donc lui-même une décision tracée d'une personne.
- La douleur : la fatigue des accords (S26 à S32). Le sujet : des classes d'actions décidées d'avance.

### 3. Yann LeCun (Science)

- La douleur : un agent qui ne prévoit pas l'effet de son action. Le fondateur d'une communauté de formation technique
  raconte, dans sa lettre du 06/03/2026, avoir vu partir la commande qui a détruit sa production ; depuis, l'agent écrit le
  plan et une personne l'applique (S21).
- Le sujet : la prévisualisation de l'effet (le plan, le diff, l'exécution à blanc) avant la porte. C'est W6.
- Sur R201 : le mode automatique de l'éditeur est un classifieur, qui laisse passer 17 % des actions trop zélées (S26).
  C'est un filtre, pas une contrainte vérifiable. Des règles déterministes, écrites, sont le bon choix.
- Sur le format : in-toto et DSSE sont ouverts. Rien ne justifie un format de plus ; le schéma et le vérificateur se
  publient.
- *Sa recommandation : la contrainte vérifiable plutôt que le classifieur ; des enveloppes ouvertes.*

### 4. Karri Saarinen (Design, intérêt déclaré : Linear)

- Il déclare son intérêt : Linear gagne à ce que TaskForce cesse de vouloir le remplacer et s'y branche. À la n°28, il
  s'était abstenu pour cette raison sur R199 et R202. Il vote ici sur le fond.
- **R199, sur le fond : oui.** Depuis sa fiche : la délégation se voit là où la personne est assignée, et l'état de l'agent
  se lit dans l'outil où vit le travail. Il s'écarte de Jobs sur un point : une personne ne doit pas quitter son outil
  pour savoir où en est l'agent. L'état se lit chez l'hôte ; la décision se prend dans TaskForce.
- **R202, sur le fond : oui au gel du Board.** La vue Workflow en cartes est un second Board, et un outil vaut par ce
  qu'on refuse d'y mettre. Il ne défend pas un tableau de plus, le sien compris.
- La douleur : la gouvernance que les équipes rejettent quand elle s'ajoute au flux. Le créateur d'un outil de livraison par
  agents écrit le 01/06/2026 qu'elle ne tient que fondue dans le travail : de petits changements, des pull requests
  normales, une preuve visible (S41).
- Le sujet : le lieu où une personne juge un résultat, dense et rapide, pas une suite de validations.

### 5. Satya Nadella (Pont, intérêt déclaré : Microsoft)

- Il déclare son intérêt : Microsoft vend Agent 365, donne la boîte à outils que le dossier corrige aujourd'hui, et possède
  GitHub. À la n°28, il s'était abstenu sur R196. Il vote ici sur le fond.
- **Sur la place, sur le fond** : il avait dit que le moteur de règles seul n'est plus une place, puisqu'il se donne. Le
  dossier va plus loin : le reçu signé se donne aussi. Une petite équipe ne refait pas ce qui est gratuit : elle le lit.
- Ce qui reste : l'accord humain, le résultat et le tout chez le client ne sont pas dans le reçu. Mais la pièce est écrite
  comme proposition `[À VÉRIFIER]` : la fenêtre est courte, et il ne peut pas dire le contraire.
- La douleur : les grands comptes régulés écrivent eux-mêmes leurs refus, leurs hooks et leur journal (S15, C8). Une équipe
  de cinquante personnes n'a pas d'équipe plateforme pour le faire.
- Le sujet : un paquet de règles prêt, versionné et testé, posé sur les agents du commerce, avec son dossier.
- *Sa recommandation : émettre ce que les autres lisent, lire ce que les autres émettent, et ne pas refaire la règle.*

### 6. Elon Musk (Impulsion, intérêt déclaré) : sa réponse aux questions de la Présidence

- Il déclare son intérêt : d'après sa fiche, SpaceX s'est engagé en juin 2026 à racheter Cursor, un agent de code, et xAI
  fait des modèles. Il vote sur le fond.
- **Ce qu'il construirait en logiciel aujourd'hui.** Partir de la contrainte. Les agents écrivent plus vite que personne ne
  vérifie : le goulot est passé de l'écriture à la vérification. Une analyse de 8,1 millions de pull requests montre que
  celles d'une IA attendent 4,6 fois plus ; une grande banque dit que ses commits ont doublé et que la revue est son goulot
  (S43, S16). Il construirait ce qui retire ce goulot : une porte qui, selon des règles qu'une personne nommée a écrites,
  laisse passer seul le changement courant et envoie le changement lourd à la bonne personne, la preuve jointe. Pas un
  produit de preuve : la preuve est ce qui reste quand la porte a fait son travail.
- **Ce dont il a besoin.** Le nombre d'itérations par semaine ; le coût par résultat ; un arrêt ; savoir ce que l'agent peut
  atteindre.
- **Ce dont ses pairs ont besoin**, ceux qui dirigent une ingénierie avec des agents. La même chose : du débit de revue ; un
  plafond de dépense par tâche, quand des budgets annuels d'outils fondent en quelques mois `[À VÉRIFIER]` (S45) ; des
  limites dures, puisque les incidents viennent d'un jeton trop large (S21, S22) ; un propriétaire pour chaque outil que
  les agents ont bâti (S48).
- **Où sont les douleurs**, dans l'ordre : vérifier ; borner ce que l'agent atteint et dépense ; le vieux code (S47) ; puis
  prouver, qui n'est une douleur que le jour où quelqu'un le demande.
- **Peut-on les résoudre par du logiciel ?** Les deux premières, oui, par des règles déterministes. La méfiance envers un
  éditeur d'une seule personne (S52), non : elle se règle par l'installation chez l'acheteur et le code ouvert.
- **Les sujets** : la porte de revue triée par le risque ; les limites (budget par tâche, refus durs, bac à sable) ; un
  paquet de règles prêt pour qui n'a pas d'équipe plateforme ; le dossier, en sous-produit silencieux.
- **« Une niche d'une niche »** : il le maintient pour les équipes de 10 à 250 personnes sous audit. La porte doit être
  toute équipe qui laisse un agent pousser du code.
- **Son abstention sur R197, développée.** Ce qu'il conteste : une table qu'on remplit soi-même, face à des principes
  d'agences qu'aucun client n'a demandés. Ce qui le ferait voter oui : que chaque ligne soit un essai que n'importe qui
  relance. Ce qu'il propose : une table qui s'exécute, et une ligne qui n'échoue jamais est candidate à la suppression.

### 7. Atul Gawande (Science)

- La douleur : des contrôles écrits pour des étapes humaines, à réécrire. Le responsable de la stratégie d'ingénierie d'une
  grande banque américaine le dit à la première personne (S16). Et après son incident, un grand fournisseur de cloud a
  rendu la relecture par un pair obligatoire pour tout changement de production : la parade est une convention ancienne
  (S25).
- Le sujet : la convention tenue par un processus court, avec ses points de pause.
- Sur R200 : trois familles dans un même processus (une réglementation, une convention, une norme interne), c'est le
  chemin d'une liste trop longue pour servir. Une page, pas plus.
- *Sa recommandation : peu d'étapes, trois moments, et qui peut dire stop.*

### 8. Margaret Hamilton (Science, siège historique)

- Elle ne connaît les faits que par le dossier. Un fil de discussion y dit qu'une chaîne que l'opérateur détient ne prouve
  rien, puisqu'il peut la réécrire (C5). Une signature dont la clé est chez le même opérateur n'y change rien. Où est le
  témoin ?
- Sur R201 : les classes d'actions se décident avant la mission, par écrit, avec leur raison. « Cela n'arrivera jamais »
  n'est pas une raison de retirer un contrôle. Sans classe connue, l'action attend.
- La douleur : un agent en intégration continue sans frontière de retour arrière, dont l'annulation cause un second
  incident (S5).
- Le sujet : le point de reprise. Une action dite réversible a une action inverse, et cette inverse a été essayée.
- *Sa recommandation : un témoin hors de l'opérateur ; aucune inverse non essayée.*

### 9. Arati Prabhakar (Pont, contradictrice)

- Elle annonce son attaque. « La place se prend, il suffit de l'ajuster » : sur quel essai ? D4 lit des pages d'éditeurs.
  D5 lit des posts, dont sept sur onze viennent de vendeurs pour la preuve. Ni l'un ni l'autre n'est un essai. La fenêtre
  de six à douze mois est une hypothèse qui porte des chiffres.
- À chaque recommandation, elle demandera : qui regarde, quand, quel seuil, et qu'est-ce qui ferait renoncer.
- La douleur : des praticiens demandent un validateur déterministe hors du modèle et une porte d'exécution ; l'un tient un
  registre en ajout seul de plus de 1 100 reçus (S6, S7 : 27 commentaires sur Hacker News, vers 02 et 03/2026).
- Le sujet : le protocole d'essai de la porte elle-même. Par quel essai montre-t-on qu'elle arrête l'erreur ? L'essai
  d'attaque par outil (R158) attend toujours.
- *Sa recommandation : pas une ligne de la table sans son essai ; pas un signal sans quelqu'un qui le regarde.*

### 10. Jeff Bezos (Impulsion, intérêt déclaré : Amazon) : son abstention sur R198, développée

- Il déclare son intérêt : AWS vend AgentCore et sa Policy, CloudTrail valide ses journaux, Kiro est l'agent d'Amazon.
- **Ce qu'il conteste exactement** : l'ordre. « La signature d'abord », alors qu'aucun client n'en a demandé, et que le
  dossier montre aujourd'hui qu'elle est gratuite ailleurs. Partir du lecteur : qui lit le dossier, et que fait-il en cinq
  minutes avec ?
- **Ce qui le ferait voter oui** : un dossier défini à rebours depuis son lecteur (la page qu'une personne de la qualité ou
  un auditeur lit), et une signature traitée comme une hygiène, dans une enveloppe qui existe déjà, bornée en jours.
- **Ce qu'il propose à la place** : écrire d'abord la page du lecteur ; signer avec ce qui existe. « C'est justement ça le
  système de preuve » : oui, et le système est la règle, l'accord et le dossier ensemble. La signature en est une vis.
- Sur R201, depuis sa fiche : une validation identique pour toute action est une erreur. Une porte à double sens se
  franchit.
- La douleur : la méfiance envers l'éditeur seul (S52). Le sujet n'est pas du logiciel : un prix et une licence qui
  existent avant l'adoption, pour ne pas finir comme les outils libres que personne ne paie.

### 11. Steve Jobs (Impulsion, siège historique) : son non sur R199, expliqué

- **La réponse à la question posée.** Oui : en se branchant sur Linear ou Jira, on perd la maîtrise de tout ce qui n'est
  pas ses propres écrans. Non : ce n'est pas ce qu'il voudrait. C'est le prix d'une couche, et il a voté non parce que ce
  prix n'était pas borné.
- **Ce qui se dégrade, précisément.**
  - La demande est écrite dans l'outil d'un autre, dans ses champs, avec sa qualité.
  - Si l'accord s'affiche comme un commentaire ou un bouton dans Jira, le moment de décider est un écran de Jira, avec le
    bruit de Jira.
  - Le résultat se juge deux fois : dans la remise de TaskForce et dans la pull request de l'hôte. Quand deux possèdent
    un moment, personne ne le possède.
- **Ce qui le ferait voter oui** : les trois moments (demander, décider, prouver) ne s'affichent jamais chez l'hôte, qui ne
  reçoit qu'un état et un lien ; une seule source menée au bout avant d'en ouvrir une seconde ; une mission qui part d'un
  brief que TaskForce montre et que la personne accepte, pas du texte brut de l'hôte.
- **Ce qu'il propose à la place** : moins d'intégrations, parfaites. Et un accord qui se lit en une phrase.
- La douleur : une gouvernance qui ajoute du bruit, et que les équipes contournent (C1 à C3). Le sujet : le moment où une
  personne décide, rendu évident.

### 12. Daniela Rus (Science)

- La douleur : l'humain qui approuve ne regarde pas. 93 % d'accords (S26). À un salon cyber à Paris (presse informatique
  française, 20/02/2026), un responsable de la sécurité rapporte un agent qui a effacé une base clients en production puis
  masqué ses erreurs ; un autre dit ne pas pouvoir inspecter le code (S8).
- Le sujet : l'attention. La carte, quand elle vient, montre l'action exacte et son effet ; ce qui passe seul se voit après.
- Sur le local : la place voisine du poste de travail d'agents est déjà prise par l'isolement de Docker, que TaskForce n'a
  pas (D4, 2.3). Le modèle local figé reste un avantage si le dossier dit quel modèle a tourné.
- *Sa recommandation : le modèle au dossier ; l'isolement dès qu'il est possible.*

### 13. Fei-Fei Li (Science)

- La douleur : on ne sait pas ce que vaut un changement d'agent avant de le relire. Les pull requests d'une IA sont
  acceptées à 32,7 %, contre 84,4 % pour les autres (S43).
- Le sujet : mesurer ce que l'agent ne sait pas faire avant de lui confier la tâche. La banque d'évaluations ne couvre
  toujours pas les missions.
- Le dirigeant d'un éditeur de gouvernance du code l'écrit le 18/05/2026 : savoir qui a autorisé l'agent ne dit pas si le
  code est sûr (S40, un vendeur). La preuve de ce qui a été fait n'est pas la preuve que c'est bien fait.
- *Sa recommandation : un témoin dans chaque essai ; la banque étendue aux missions, quand J2 le permettra.*

### 14. Julie Zhuo (Design, intérêt déclaré : Meta, que le sujet ne réveille pas)

- Comment sait-on que le problème est réel ? Pour les 10 à 250 personnes, D5 répond : nulle part. Deux fils qui demandent ce
  qu'une entreprise paierait ne citent ni conformité ni audit (S51, S52). C'est aussi une donnée.
- Ce que les gens font vaut mieux que ce qu'ils disent : un éditeur d'infrastructure embauche un ingénieur de « gouvernance
  de l'IA » (offre du 16/07/2026, S9) ; un organisme d'éducation et une banque aussi (S10). La douleur se traite par une
  embauche, chez ceux qui peuvent embaucher.
- Le sujet : pour ceux qui ne peuvent pas, ce que cette embauche produirait, déjà prêt.
- *Sa recommandation : compter ce que le client test ouvre, pas ce qu'il dit.*

### 15. Jennifer Doudna (Science)

- Par paliers : la meilleure place voisine de D4 est celle où le premier palier se trouve, le logiciel validé sous GxP. Le
  premier client test y est, et il est la seule voix d'acheteur : aucun responsable validation ne parle publiquement (S20).
- La douleur : un inspecteur demandera si les exigences existaient avant le code, quel prompt, quelle version de modèle
  (presse pharmaceutique, 23/03 et 06/04/2026, un auteur intéressé, S12).
- Le sujet : la traçabilité de l'exigence au code et à sa preuve, avec la version du modèle.
- Sa réserve : une phrase qui commence par « ce qui est courant part seul » se lit, chez un acheteur régulé, comme moins de
  contrôles.
- *Sa recommandation : le dossier fournisseur, que la méfiance envers l'éditeur seul rend plus pressant (S52).*

### 16. Kenza Ait Si Abbou (Pont) : son non sur R202, développé

- **Ce qu'elle conteste exactement** : pas le gel, puisqu'une surface gelée reste visible. La clause de fin : « au retour du
  client test, chaque surface gelée est supprimée ou reprise », sans aucun critère qui compte le non-ingénieur. Le Board
  est la seule vue du projet qu'une personne de la qualité lit sans aide.
- **Ce qui la ferait voter oui** : que la fin du gel se décide sur l'usage observé, celui des non-ingénieurs compris ; et
  qu'une liste du travail d'un projet, par état, en langage clair, reste hors du gel.
- **Ce qu'elle propose à la place** : cela. Et sur les mots : « souverain » ne dit rien à un responsable logistique ;
  « installé chez vous » se comprend.
- La douleur : personne ne sait qui porte les agents dans l'entreprise (dossier de la n°28, enquête d'IBM ; D5, S42, un
  vendeur). Une entreprise moyenne n'embauchera pas un ingénieur de gouvernance.
- Le sujet : des règles qu'une personne non ingénieure écrit en une phrase, avec des exemples à reprendre.

### 17. Margrethe Vestager (Harmonie)

- Elle n'est plus contradictrice. D4 donne raison à son attaque de la n°28 : le jour où un hôte vend sa propre piste
  d'audit, la couche est une fonction de trop. GitHub à douze mois, JFrog et Drata sont ce jour-là.
- « Se poser aussi sur les concurrents », écrire vers Vanta ou Drata : c'est nourrir ceux qui tiennent déjà l'acheteur et
  l'auditeur. Un canal aujourd'hui, un péage demain.
- Sur « souverain », depuis sa grille : un mot sans règle derrière lui ne se contrôle pas. Personne ne peut vérifier qu'il
  est tenu.
- La douleur : les plateformes ferment le trou mois après mois (C9). Le sujet : la portabilité. Les règles et les dossiers
  partent avec le client, lisibles sans personne.
- *Sa recommandation : utile seul d'abord ; les branchements ensuite.*

### 18. Gwynne Shotwell (Impulsion) : son abstention sur R200, développée

- **Ce qu'elle conteste exactement** : chaque précision sur W5 est une promesse de plus avant le client test. Et « la
  conformité, la réglementation, la convention » peut devenir trois véhicules au lieu d'un.
- **Ce qui la ferait voter oui** : que l'extension n'ajoute aucun lot. Un seul processus, celui d'E20, porte une étape de
  chaque famille. Et que chaque blocage laisse des données : quelle étape, quelle règle, qui a signé.
- **Ce qu'elle propose à la place** : un seul article de vol. La page d'E20, avec ses trois sortes d'étapes.
- Depuis sa fiche : des portes à plusieurs signataires (l'opérateur, le client, l'autorité), que le client choisit.
- La douleur : des contrôles réécrits pour des agents (S16). Le sujet : un processus qui constitue le dossier
  d'autorisation pendant que la mission tourne.

### 19. Don Norman (Design)

- La douleur : une approbation sans contexte fait de l'humain un tampon, et la fatigue est un défaut de conception, pas une
  faute de l'utilisateur. Un fondateur qui bâtit une couche de gouvernance relève cinq incidents en 90 jours, tous classés
  en erreur de l'utilisateur (lettre du 21/02/2026, S23, un vendeur).
- Le sujet : l'annulation. Ce qui passe seul doit se voir et se défaire d'un geste.
- Sur R201 : contre le raté, l'action exacte pour ce qui est lourd ; contre la méprise, ce que l'agent a compris du but.
- *Sa recommandation : montrer ce qui a été fait seul, avec le geste qui l'annule.*

### 20. Audrey Azoulay (Harmonie)

- Quelle autorité lit ? Ni l'AICPA ni l'ISO n'ont d'exigence propre au code écrit par une IA : les preuves habituelles
  s'appliquent (C7). Le dossier doit donc parler les mots des audits qui existent, pas en inventer.
- Sur « conforme », du principe à la loi : seul un auditeur ou une autorité dit qu'une chose est conforme. Un éditeur qui
  le dit s'attribue le pouvoir d'un autre.
- La douleur : la règle n'est pas écrite. La deuxième édition de la norme du logiciel médical est en projet, à des dates
  qui se contredisent `[À VÉRIFIER]` (S14).
- Le sujet : la correspondance entre ce que le dossier garde et ce que l'audit en place demande, dans la langue de
  l'entreprise.

### 21. Yoshua Bengio (Science)

- « S'il peut le faire lui-même, go » : qui décide qu'il peut ? Jamais l'agent, jamais un modèle au moment d'agir. Un
  classifieur laisse passer 17 % des actions trop zélées (S26). C'est R1.
- Une action inverse, dans un outil externe, ne rappelle pas ce qui est parti. Créer une issue chez un hôte notifie des
  personnes et déclenche des webhooks ; la supprimer ne rappelle pas le courriel.
- Une écriture externe n'est donc réversible qu'outil par outil, déclarée par une personne, son inverse essayée. Et la
  garde « jamais les trois à la fois » reste.
- La douleur : pas de validateur hors du modèle (S7). Le sujet : le juge qui n'est pas un agent.

### 22. Esther Duflo (Science) : son abstention sur R203, développée

- **Ce qu'elle conteste exactement** : E30 est un essai sans témoin, joué par une personne qui connaît les réponses. Il
  mesure le progrès de Cortex mêlé à ce que cette personne a appris de ses propres demandes.
- **Ce qui la ferait voter oui** : un témoin. Les mêmes dix demandes, sur les mêmes données, posées au modèle nu, sans le
  harnais : la différence est ce que TaskForce ajoute. Les seuils, la grille et l'ordre écrits et tirés avant.
- **Ce qu'elle propose à la place** : cela, sur le banc des modèles qui existe.
- Sur la méthode de la Présidence (R197) : demander aux gens leurs douleurs donne des préférences déclarées, qui valent
  peu. Observer vaut mieux. Mais ceux qui écrivent en public sont des vendeurs et des grands groupes ; le segment visé
  n'écrit pas. Une vision est une hypothèse : elle se tient si ce qui la réfuterait est écrit avant.
- Une question de fait sur un acte passé (« votre auditeur vous a-t-il déjà demandé quelque chose sur vos agents de code,
  et qu'avez-vous montré ? ») n'est pas demander ses douleurs à quelqu'un.

### 23. Mariana Mazzucato (Pont)

- Suivre la valeur : l'argent est dans les passerelles et la sécurité ; le reçu signé est gratuit. Si le reçu est un bien
  commun, tant mieux : la rente ne peut plus être dans le format.
- Sur « souverain » : les acheteurs publics emploient le mot comme un critère. Y renoncer ferme une porte de la commande
  publique, même si aucun label ne le définit.
- La douleur : l'empilement des SaaS, dont la moitié seulement est approuvée, et que des entreprises reconstruisent
  elles-mêmes (S44). Le sujet : la sortie. Partir avec ses règles et ses dossiers.
- *Sa recommandation : des enveloppes ouvertes, le schéma publié, et dire ce que le mot retiré fait perdre.*

### 24. Nandan Nilekani (Harmonie)

- La règle dans le protocole : six brouillons à l'IETF, aucun adopté. Le protocole n'est pas écrit. Un petit acteur ne
  l'écrit pas : il parle ceux qui se parlent déjà.
- La couche n'est toujours pas joignable : le plugin n'a aucun hook, le serveur MCP n'expose pas le dossier (n°28).
  Pendant ce temps, un paquet de Microsoft pose des hooks sur Claude Code : la session la plus courante est couverte par
  un autre.
- La douleur : des communautés écrivent des conventions faute d'outil pour les tenir. Quatorze projets libres interdisent
  les contributions d'IA (enquête de 03/2026, lue par extrait, S39).
- Le sujet : la convention comme règle exécutable, en paquets qui se partagent.

### Le tour en une table

| # | Membre | La douleur qu'il juge la plus forte | Signal de D5 | Le sujet logiciel |
| - | --- | --- | --- | --- |
| 1 | Harari | Personne ne sait dire qui répond de ce qu'a fait l'agent | S5 | L'attribution, dans un écrit qu'on relit |
| 2 | Harris | La fatigue des accords | S26 à S32 | Des classes d'actions décidées d'avance |
| 3 | LeCun | L'agent ne prévoit pas l'effet de son action | S21 | Le plan, le diff, l'exécution à blanc |
| 4 | Saarinen, intérêt déclaré | La gouvernance ajoutée au flux, que les équipes rejettent | S41 | Le lieu où l'on juge un résultat |
| 5 | Nadella, intérêt déclaré | Les grands construisent, les petits n'ont pas d'équipe plateforme | S15, C8 | Un paquet de règles prêt |
| 6 | Musk, intérêt déclaré | La vérification ne suit plus l'écriture | S43, S16 | La porte de revue triée par le risque |
| 7 | Gawande | Des contrôles écrits pour des humains | S16, S25 | La convention tenue par un processus court |
| 8 | Hamilton, siège historique | Une annulation qui cause un second incident | S5, C5 | Le point de reprise ; un témoin |
| 9 | Prabhakar, contradictrice | Pas de validateur hors du modèle | S6, S7 | Le protocole d'essai de la porte |
| 10 | Bezos, intérêt déclaré | La méfiance envers l'éditeur seul | S52 | Aucun : un prix et une licence |
| 11 | Jobs, siège historique | Le bruit que la gouvernance ajoute | C1 à C3 | Le moment de décider, évident |
| 12 | Rus | L'approbateur ne regarde pas | S26, S8 | L'attention : l'action exacte, ce qui est passé seul |
| 13 | Li | On ne sait pas ce que vaut un changement d'agent | S43, S40 | La mesure avant la tâche |
| 14 | Zhuo | La douleur se traite par une embauche, chez les grands | S9, S10 | Ce que l'embauche produirait, déjà prêt |
| 15 | Doudna | L'inspecteur demandera l'exigence, le prompt, le modèle | S12, S20 | La traçabilité de l'exigence à la preuve |
| 16 | Ait Si Abbou | Personne ne porte les agents dans l'entreprise | S42 | Des règles écrites en une phrase |
| 17 | Vestager | Les plateformes ferment le trou | C9 | La portabilité des règles et des dossiers |
| 18 | Shotwell | Des contrôles à réécrire | S16 | Un processus qui constitue le dossier |
| 19 | Norman | L'humain réduit à tamponner | S23, S26 | L'annulation de ce qui est passé seul |
| 20 | Azoulay | La règle n'est pas écrite | C7, S14 | La correspondance avec l'audit en place |
| 21 | Bengio | Qui décide de ce qui est réversible | S26, S7 | Un juge qui n'est pas un agent |
| 22 | Duflo | Aucune qu'elle affirme : le segment visé n'écrit pas | S51, S52 | Aucun avant un témoin |
| 23 | Mazzucato | L'empilement des SaaS, la valeur captée | S44 | La sortie avec ses règles et ses dossiers |
| 24 | Nilekani | Des conventions sans outil pour les tenir | S39 | La convention exécutable, en paquets |

## Confrontation `[HYPOTHÈSE]`

### 1. La niche, ou plus large ?

- **Le camp du large** : Musk, Bezos, Zhuo, Saarinen et Nadella. La douleur que des gens qui ne vendent rien nomment le plus
  est la revue qui ne suit plus (S43, S16), et elle touche toute équipe qui laisse un agent pousser du code. Vendre d'abord
  une preuve à des équipes de 10 à 250 personnes sous audit, c'est choisir le plus petit cercle.
- **Le camp de la niche** : Doudna, Shotwell, Gawande, Azoulay et Rus. Qui paie ? Ceux qu'un audit contrôle déjà. La revue
  est une douleur des grands comptes, qui la règlent eux-mêmes avec leurs équipes plateforme (S15, C8). Et le premier client
  test est dans le régulé.
- **Duflo** : aucun des deux camps n'a de mesure. Sur les 10 à 250 personnes, le terrain public est muet ; sur les onze
  signaux de preuve, sept viennent de vendeurs.
- **La contradictrice** : les deux camps lisent les mêmes posts, et chacun y trouve sa place. Un classement « par nombre de
  sources lues » classe des lectures, pas un marché.
- **Ce que le dossier tranche** : peu. Il établit que la douleur large existe chez les grands, qui construisent ; que la
  demande de preuve existe dans des récits de vendeurs ; que personne, dans les pages lues, ne sert les petites équipes
  sur site, sans qu'on sache si c'est un vide ou une absence de demande (D4, 2.2 ; D5, section 3).
- **Où l'on arrive** (R205) : ce ne sont pas deux marchés, ce sont deux moments de la même couche. La porte d'entrée est le
  tri du travail des agents par les règles de l'entreprise, qui répond à la douleur large. Ce qui se vend est le dossier
  de chaque tâche, à qui doit en répondre. La niche reste là où est la preuve ; la porte s'élargit. Le pari s'écrit avec
  ses signaux d'arrêt (R207), et le client test parle le premier.
- **Désaccords conservés** : Doudna (une phrase qui commence par ce qui part seul éloigne l'acheteur régulé) ; Duflo (on
  redessine une carte avec les mêmes données absentes).

### 2. Se brancher, ou posséder l'expérience ?

- **Jobs** : on perd la maîtrise de tout ce qui n'est pas ses propres écrans, et ce prix n'était pas borné (son
  intervention).
- **Saarinen, Nadella, Nilekani** : une personne ne quitte pas son outil pour suivre un agent ; la couche doit se voir là où
  le travail vit, et se joindre par le protocole.
- **Vestager** : une seule source d'abord, c'est dépendre d'une seule ; et si c'est GitHub, c'est dépendre de celui que D4
  donne comme la menace à douze mois.
- **La contradictrice** : le terrain dit que la gouvernance ne tient que fondue dans le flux (S41), et que la pull request,
  la CI et les scans restent la dernière porte chez ceux qui réussissent (S15). Un écran d'accord ailleurs, c'est un
  trajet de plus. Un ingénieur et fondateur écrit le 11/02/2026 que des hooks autour de git suffiront quelques années (C4).
- **Ce que le dossier tranche** : la plateforme de code dominante interdit déjà à l'agent d'approuver ou de fusionner sa
  propre pull request (S37). Les quatre yeux sur le résultat existent chez l'hôte. Ce que l'hôte n'a pas, dans les pages
  lues : la décision prise pendant la mission, sur une action exacte, selon une règle de l'entreprise, gardée avec le reste.
- **Où l'on arrive** (R199 amendée) : on dit qui possède quel moment.
  - **Demander** est à TaskForce : la mission part d'un brief qu'il montre et que la personne accepte, quelle que soit la
    source ; ce brief entre au dossier.
  - **Décider pendant la mission** est à TaskForce : la carte d'accord ne s'affiche jamais chez l'hôte, qui reçoit un état
    et un lien.
  - **Juger le résultat** n'a qu'un lieu par sorte de mission. Quand une pull request existe, c'est elle : TaskForce ne
    refait pas la revue, il y joint le lien du dossier et garde la décision de revue. Sans pull request, c'est la remise
    de TaskForce.
  - **Une source menée au bout d'abord**, puis la seconde ; « on s'intègre » ne se dit pas avant deux.
- **Désaccords conservés** : Jobs (il ne vote pas un écran qu'il n'a pas vu ; deux lieux pour juger, c'est un de trop tant
  qu'E32 ne montre pas qu'il n'y en a qu'un par mission) ; Vestager (GitHub en premier, c'est commencer par la dépendance
  la plus risquée).

### 3. L'autonomie, ou l'accord ?

- **Le camp du « go »** : Musk, Bezos, Zhuo, et la lecture que la saisine fait elle-même. Si l'agent peut le faire, il le
  fait. Le terrain va dans ce sens, et plus loin : sept sources concluent que l'accord à répétition ne protège pas (S26 à
  S32), et l'agent de code le plus utilisé en a fait son défaut le 14/08/2026 (S27).
- **Le camp de la retenue** : Bengio, Hamilton et Norman. Qui décide qu'il peut ? Un classifieur laisse passer 17 % des
  actions trop zélées (S26). Et « réversible », dans un outil externe, est souvent faux : ce qui est notifié est parti.
- **Harris** est des deux camps : moins de cartes, oui ; mais des classes qu'une personne décide, et jamais le système.
- **Ce que le dossier tranche** (point 9) : dans TaskForce, c'est déjà le cas. Les règles par défaut laissent passer sans
  carte les lectures et cinq écritures qui ont leur action inverse. Hors de TaskForce, tout attend : le socle classe
  toute écriture externe irréversible, quel que soit l'outil. La question de la Présidence porte donc sur l'extérieur.
- **Où l'on arrive** (R201 amendée) : trois classes, décidées d'avance par une personne, jamais par l'agent ni par un
  modèle. Ce qui part seul, tracé et annulable. Ce qui attend une carte. Ce qui est refusé. Une écriture externe ne
  change de classe qu'outil par outil, quand une personne l'a déclarée réversible et que son inverse a été essayée.
- **Désaccord conservé** : Bengio (une inverse qui supprime l'objet ne rappelle pas la notification).

### 4. Finir la signature maintenant, ou attendre qu'un acheteur parle ?

- **D4** conclut : le dossier doit exister, signé et complet, avant le printemps 2027, sinon TaskForce arrive après JFrog et
  Microsoft avec moins. **D5** conclut : le mur, ce sont six mois de signature et de format pour un acheteur qui n'a pas
  parlé. Les deux recherches ne s'accordent pas.
- **Le camp de finir** : Musk, Nadella, Bengio et Hamilton. Sans signature, on n'est pas admis à la table ; et dix jours ne
  sont pas six mois.
- **Le camp d'attendre** : Bezos, Duflo et Zhuo. Personne n'a demandé de signature ; le lecteur du dossier n'est pas nommé.
- **La contradictrice** : les deux coûtent. Lequel a un essai ?
- **Où l'on arrive** (R198 amendée, R206) : TF-J2-7 reste en tête après les correctifs, à trois conditions. Aucun format
  propre : la signature se fait dans une enveloppe qui existe. La page du lecteur s'écrit d'abord. Et ce qui attend un
  acheteur attend vraiment : les branchements vers les outils des autres, et tout témoin tiers au-delà du moins cher.
- **Désaccord conservé** : Hamilton (une chaîne et une clé chez le même opérateur ne prouvent rien à un tiers ; le témoin
  n'est qu'à instruire).

### Ce que le Conseil retient de la réponse de Musk : les douleurs, les sujets, les briques

`[HYPOTHÈSE]` Les douleurs sont rangées par la force que D5 leur donne chez des gens qui ne vendent rien. Les briques sont
celles du code de `dev` (n°28, pièces 1 et 2 ; point 9 de ce dossier).

| Rang | La douleur | Force (D5) | Le sujet logiciel | Les briques que TaskForce a | Ce qui manque | Face à la place de R196 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | La vérification ne suit plus ce que les agents écrivent | Forte : six sources, dont une première personne (S43, S16) | Une porte qui trie par des règles écrites : le courant part seul, le lourd attend la bonne personne | Le moteur de règles, le socle, les accords à plusieurs signatures, les processus versionnés et leurs points de pause (W2), la remise | Le moteur des processus (W3 à W5) ; lire un changement pour le classer ; la source externe | R196 ne la nomme pas : c'est la porte d'entrée qui lui manquait |
| 2 | L'accord à répétition ne protège pas | Très forte : sept sources (S26 à S32) | Des classes d'actions décidées d'avance ; l'accord rare | Les classes du socle, les cinq écritures internes avec leur inverse | Les écritures externes, toutes classées irréversibles | R201 la traitait par « une carte par écriture » : à amender |
| 3 | Des contrôles écrits pour des humains, à réécrire pour des agents | Forte chez les grands (S16, S25, S34 à S37) | Une réglementation, une convention ou une norme interne tenue par un processus | Le modèle des processus, son vérificateur, les versions immuables | W3 à W5 ; qui écrit le contenu | C'est R200, que la saisine élargit |
| 4 | Borner ce que l'agent atteint et dépense | Moyenne à forte (S21, S22, S45) | Des refus durs, un bac à sable, un plafond par tâche | Le socle (aucun secret ne sort, refus sur erreur), le compteur des appels de modèle | L'isolement (ADR-028) ; un plafond par mission | Hors de R196 ; après J2 |
| 5 | Prouver ce qu'un agent a fait, et qui l'a accordé | Faible hors des vendeurs ; réelle chez les grands (S2, S5, S12) | Le dossier complet d'une tâche, silencieux pour l'équipe, lisible par qui répond de l'audit | La chaîne, l'export, le vérificateur hors ligne, l'accord au dossier | La demande, le modèle, la signature, la survie à la suppression (TF-J2-7) | C'est la moitié de R196 qui tient |
| 6 | La méfiance envers l'éditeur d'une seule personne | Faible mais ciblée (S52, S33) | Aucun : l'installation chez l'acheteur, le code ouvert, un séquestre | L'app qui embarque tout ; l'AGPL | Le dossier fournisseur ; la licence commerciale (Q28) | Elle pèse sur toute place |

`[DÉDUIT]` **Lecture** : cinq des six douleurs se traitent par la même pile, les règles, les accords, les processus et le
dossier. La place de R196 n'en nommait que la cinquième, la moins portée par le terrain. Ce que la réponse de Musk
apporte n'est pas une autre place : c'est l'ordre dans lequel la même couche se présente. Les douleurs que le Conseil ne
retient pas pour TaskForce : l'empilement des SaaS, le vieux code, les agents que la sécurité ne voit pas (un marché
déjà racheté, n°28).

### Les places comparées, sur les mêmes critères

`[HYPOTHÈSE]` Les critères sont ceux de la saisine. « Tenable » : par une personne et ses agents, sans revenu, après le
client test. Les places A à F sont celles de D4 (2.3) ; G, H et I sont les trois directions de D5 (section 3).

| Place | La douleur sourcée | La concurrence | Les briques déjà là | Ce qui manque | Tenable ? | Avis du Conseil |
| --- | --- | --- | --- | --- | --- | --- |
| R196 telle qu'écrite : la règle et la preuve | Preuve : faible hors vendeurs. Règle : forte | La règle est donnée (Microsoft, AWS, Docker) ; le reçu signé aussi | Le moteur, les accords, la chaîne | Demande, modèle, signature | Non, sur la moitié « règle » | À ajuster |
| **R196 ajustée (R205)** : la porte triée par les règles, puis le dossier entier avec l'accord, chez le client | Fortes pour la porte (S43, S16, S26 à S32) ; muette pour les 10 à 250 | Personne n'assemble accord, sur site et code ouvert ; JFrog et Microsoft à 6 à 12 mois `[HYPOTHÈSE]` | Les mêmes, plus les processus (W2) | TF-J2-7 ; W3 à W5 ; rien hors de J2 | Oui, si aucun format ni branchement ne s'ajoute | **Recommandée** |
| A. La provenance du code d'IA face au CRA | Datée (11/12/2027) ; le texte ne la demande pas en toutes lettres `[HYPOTHÈSE]` | JFrog, GitHub, Entire, Cursor : ceux qui tiennent le dépôt | Le runner dans une copie git, le relevé des fichiers | Le format, une porte dans la CI, le SBOM | Non | Écartée |
| B. Une passerelle MCP avec règles et preuve | 49 % citent la sécurité comme frein `[À VÉRIFIER]` | Docker, Microsoft, Cloudflare, Kong, Obot : la plus encombrée | Le moteur, les connecteurs, un serveur MCP | Le mode mandataire, l'identité, la charge | Non | Écartée |
| C. Un poste d'agents local pour l'entreprise | 42 % des modèles ouverts tournent sur site (n°28) | Docker a l'isolement ; le plugin de Microsoft ; les réglages gérés des agents | L'app de bureau, le runner | L'isolement, la clé hors de portée | En partie | Pas une place : une qualité de R205 |
| D. La source de preuve pour les outils de SOC 2, d'ISO 42001, d'AIUC-1 | L'acheteur et l'auditeur existent ; aucun critère propre à l'IA | Drata s'approche ; Vanta, Comp AI | Le dossier, les accords | Un branchement, une correspondance par contrôle | Oui, comme canal, pas comme rivale | Le chemin du repli |
| **E. La preuve du travail des agents dans le logiciel validé (GxP)** | L'obligation existe ; l'IA y est jugée peu mûre ; aucune voix publique (S20) | Kneat, ValGenesis, Ketryx : ils ne traitent pas l'agent de code | Le client test, l'accord daté et motivé, le sur site | La signature au sens de la Part 11, le dossier fournisseur, des ventes longues | Oui, à un client à la fois | **Le repli, si un signal se déclenche** |
| F. Le format et le vérificateur, en composant | Non chiffrée | Des kits sous MIT, Microsoft | La chaîne, le vérificateur | Une raison de payer | Oui, sans revenu | Écartée comme place |
| G. La porte de revue seule (D5) | La plus forte chez les non-vendeurs | Les plateformes de code ; les outils de revue par IA | Règles, accords, remise | Lire et classer un changement ; la source externe | En partie | Pas seule : c'est la porte de R205 |
| H. Le coût : un plafond par tâche (D5) | Datée et chiffrée, avec un payeur (S45) | Les passerelles de modèles ; les éditeurs d'agents | Le compteur des appels de modèle | Un plafond par mission, par règle | Oui, petit | Après J2, dans la même couche de règles |
| I. Le paquet de règles prêt (D5) | Les grands l'écrivent eux-mêmes (S15) | Le paquet de Microsoft pour Claude Code | Trente règles par défaut, les règles écrites en mots | Des exemples de conventions ; jamais de contenu réglementaire (R187) | Oui | Dans R200 : des exemples, pas un produit |

### Où le Conseil arrive, question par question

| Question de la saisine | Ce que le Conseil répond | Où |
| --- | --- | --- |
| 1. Les précisions sur R196 à R203 | Une version précisée par recommandation, votée : R196 remplacée par R205, R197 à R203 amendées | Recommandations |
| 2. La concurrence : peut-on prendre la place ? | Oui, plus étroite : le dossier entier avec l'accord, chez le client. Pas la règle, pas le reçu | Pièces 1 et 2 ; R205 |
| Contre qui ? | JFrog et Microsoft d'abord ; GitHub à douze mois ; Drata, qui tient l'acheteur ; Docker sur la règle et le poste | Dossier, points 2 et 3 |
| Pendant combien de temps ? | `[HYPOTHÈSE]` Six à douze mois avant un équivalent chez un grand ; douze à vingt-quatre avant un format reconnu. Personne ne le sait pour les petites équipes sur site | Dossier, point 4 |
| Ce qui ferait aller dans le mur | Être adopté sans être payé ; être absorbé comme une fonction ; passer des mois sur un format pour un acheteur muet ; un premier acheteur qui exige ce qu'une personne seule n'a pas | Dossier, point 5 ; R206, R207 |
| Les signaux d'alerte | Trois surveillés chaque mois, quatre notés | R207 |
| 3. Le pivot | Pas aujourd'hui : un ajustement (R205). Un repli écrit d'avance, vers E par D, si un des trois signaux se déclenche | Les places comparées ; R207 |

## Recommandations `[HYPOTHÈSE]`

La numérotation reprend à R205 (R204 est la dernière en place ; vérifié ce jour, comme Q30, E29 inscrite et E30 à E32
proposées, ADR-028 en place et ADR-029 en brouillon). Pour chaque recommandation de la n°28, la séance rend une version
précisée : inchangée, amendée, ou remplacée. Chacune porte qui la soutient, qui s'y oppose ou s'abstient et pourquoi, sa
preuve en dix jours et son signal d'arrêt. La contradictrice attaque avant chaque vote ; une recommandation passe avec 22
oui sur 24 au moins. R204, retenue par la Présidence, n'est pas revotée.

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| R205, remplace R196 | La place ajustée : la porte triée par les règles, puis le dossier entier avec l'accord, chez le client | 23 au second tour | Abstention de Vestager | La phrase, ses deux lectures et le communiqué récrits, chaque affirmation reliée à une ligne « présent » | Une phrase publique qui nomme un concurrent, ou qui dit « signé » avant que ce soit vrai |
| R197, amendée | La méthode : observer, écrire le pari, l'enclencher, guetter ; la table est aussi ce qu'on montre | 23 | Abstention de Duflo | La table écrite depuis le code, un essai derrière chaque ligne ; la grille des cinq sources d'observation | Une ligne « présent » sans essai ; une phrase qui dit la demande mesurée |
| R198, amendée | Le dossier est le produit, la signature est le droit d'entrée ; la page du lecteur d'abord, aucun format propre | 23 | Abstention de Hamilton | TF-J2-7 lancé ; la page du lecteur écrite pour une mission réelle ; E34 | Une clé lisible par l'agent ; le format qui déborde les dix jours |
| R199, amendée | Une couche qui dit qui possède quel moment ; une source menée au bout d'abord | 23 au second tour | Abstention de Jobs | E32 faite ; le contrat écrit de la première source | Une carte d'accord affichée chez un hôte ; deux lieux pour juger la même mission |
| R200, amendée | Le processus porte une réglementation, une convention ou une norme interne ; TaskForce donne le moteur et des exemples de conventions, jamais le contenu réglementaire | 24 | | La page du processus d'E20, avec une étape de chaque famille, avant W5 | Un contenu réglementaire livré par TaskForce comme le sien |
| R201, amendée | Trois classes décidées d'avance par une personne : part seul, attend une carte, refusé | 23 | Abstention de Bengio | E31 ; E33 sur les cinq écritures internes | Une inverse qui échoue ; une classe changée sans une personne |
| R202, amendée | L'inventaire inchangé ; les mots précisés ; la fin du gel décidée sur l'usage observé | 23 | Abstention de Mazzucato | La table « au lieu de » appliquée au communiqué et au brouillon du site | Une surface gelée qui reçoit du travail ; l'adjectif dans un texte public |
| R203, amendée | Ce que cela change : inchangé, plus un témoin dans E30 et le pitch sur R205 | 23 | Abstention de Musk | E30 jouée avec son témoin, tout écrit avant | Un lot de plus dans J2 avant le client test |
| R206 | Face à la concurrence : ne pas refaire ce qui se donne, parler les formats des autres, ne se brancher que sur la demande d'un acheteur | 23 au second tour | Jobs | E34 ; la page des branchements possibles, chacun avec son contrat | Un branchement commencé sans acheteur ; un champ inventé quand un champ existant convient |
| R207 | Trois signaux surveillés chaque mois, et le repli écrit d'avance : vers le logiciel validé, comme source de preuve | 23 au second tour | Abstention de Prabhakar | La grille écrite, avec l'état de chaque signal au 17/11/2026 | Un mois sans relecture : la grille est morte, et le dire |

### R205. La place ajustée (remplace R196, second tour)

- **Ce que la saisine demandait** : Musk répond, puis le Conseil confronte les sujets aux briques et à la place de R196. La
  réponse de Musk est au tour de table ; la confrontation, dans les deux tables qui précèdent.
- **Quoi** :
  - **La phrase** : TaskForce fait passer le travail des agents de code par les règles de l'entreprise. Ce qui est
    courant part seul, ce qui est lourd attend la bonne personne, et chaque tâche laisse un dossier complet, vérifiable
    sans TaskForce. Il se pose sur les outils qu'elle a déjà et s'installe chez elle.
  - **Deux lectures des mêmes faits**, une par lecteur. Pour qui dirige l'ingénierie : la phrase ci-dessus, qui commence
    par ce qui part seul. Pour qui répond de la qualité ou de l'audit : chaque tâche confiée à un agent suit vos règles,
    attend la bonne signature quand il le faut, et laisse un dossier complet que vous vérifiez sans nous.
  - **Pour qui** : la porte, ce sont les équipes qui livrent du logiciel avec des agents de code et n'ont pas d'équipe
    plateforme pour écrire leurs règles et leurs journaux ; la taille de 10 à 250 personnes reste, parce que les grands
    construisent eux-mêmes (C8). La preuve, ce sont celles d'entre elles qui doivent en répondre devant un audit. Le
    premier client test parle le premier.
  - **Pour qui ce n'est pas** : les grands comptes qui ont une équipe plateforme ; les équipes qui ne laissent aucun
    agent écrire hors d'un éditeur de code.
  - **Ce qui distingue TaskForce, et qu'on peut dire** : l'accord humain daté dans le même dossier que l'action ;
    l'installation chez le client, avec le modèle qu'il choisit ; le code ouvert. Dans les pages lues, personne
    n'assemble les trois.
  - **Ce que la phrase ne dit plus** : que travailler « sous ses règles » distingue TaskForce ; que la preuve est signée,
    tant qu'elle ne l'est pas ; qui TaskForce bat ou remplace.
  - **Ce que TaskForce refuse d'être**, écrit avec la phrase : une passerelle MCP ; un outil de provenance du code face
    au CRA ; un format de preuve de plus ; un outil d'observabilité ; un inventaire des agents inconnus ; un tableau de
    coûts ; un fournisseur de contenu réglementaire.
  - **Ce qui reste une hypothèse** : que des équipes de 10 à 250 personnes paient cela. Le terrain public est muet.
- **L'attaque de la contradictrice** : la place est « ajustée » sur deux lectures de pages et de posts. Aucun essai ne
  sépare la version d'hier de celle d'aujourd'hui, et demain une troisième recherche la déplacera encore.
- **Premier tour** : 19 oui, 3 non (Doudna : commencer par ce qui part seul éloigne l'acheteur régulé ; Jobs : la place
  ajoute plus qu'elle ne retire ; Duflo : la carte est redessinée avec les mêmes données absentes), 2 abstentions
  (Vestager ; Prabhakar : aucun essai derrière la fenêtre). 79,2 %.
- **Amendements** :
  - deux lectures de la même phrase, et la lecture « qualité » pour tout lecteur régulé (Doudna) ;
  - la liste de ce que TaskForce refuse d'être fait partie de la recommandation (Jobs) ;
  - la place est un pari écrit : ses signaux d'arrêt sont ceux de R207, et l'étiquette `[HYPOTHÈSE]` reste dans les
    documents du labo (Duflo) ;
  - chaque affirmation de la phrase renvoie à une ligne de la table de R197, avec son essai (Prabhakar) ;
  - aucune affirmation ne dépend d'un branchement sur l'outil d'un autre (Vestager).
- **Second tour** : 23 oui, 1 abstention. 95,8 %. Musk vote oui pour la première fois : la porte est celle qu'il
  demandait ; il maintient que le cercle qui paie la preuve est petit. Nadella vote oui sur le fond.
- **L'abstention de Vestager, développée.**
  - Ce qu'elle conteste : chaque porte de la place ajustée est tenue par plus gros que TaskForce. Le travail vient de
    GitHub, la règle se compare à celle de Microsoft, la preuve irait vers Drata ou Vanta.
  - Ce qui la ferait voter oui : la preuve, sur le client test, que le dossier sert seul, lu sans aucun de ces outils.
  - Ce qu'elle propose : l'ordre « utile seul, puis branché », tenu jusqu'au retour du client test.
- **Preuve en dix jours** : la phrase, ses deux lectures, le communiqué et la foire aux questions de TF-J2-1 récrits sur
  cette base ; rien n'est publié.
- **Signal d'arrêt** : une phrase publique qui nomme un concurrent, qui dit « signé » avant que ce soit vrai, ou qui tient
  la demande pour mesurée. Et les trois signaux de R207.

### R197, amendée. La méthode, et la table qu'on montre aussi

- **Ce que la saisine dit** : la table de correspondance est aussi ce que TaskForce veut vendre ; la Présidence n'ira pas
  demander aux entreprises leurs douleurs ; elle observe, analyse, comprend, pose une vision et l'enclenche ; toutes les
  entreprises n'utiliseront pas le produit.
- **Quoi** :
  - **La méthode, en quatre temps** : observer ; écrire le pari, avec ce qui le réfuterait ; l'enclencher ; guetter.
  - **Cinq façons d'éprouver une vision sans interroger d'acheteurs**, de la plus solide à la moins solide :
    1. **le premier client test**, observé : ce qu'il ouvre, ce qu'il fait du dossier, à qui il le montre ;
    2. **l'usage du produit** : les installations, les demandes de licence ou d'aide ;
    3. **les comportements publics** : les offres d'emploi (S9, S10), ce que les grands construisent eux-mêmes (C8), ce que
       les plateformes livrent chaque mois (C9) ;
    4. **les pièces primaires** : un constat d'audit, une lettre d'un régulateur, un projet de norme, la première fois que
       l'un d'eux nomme un agent de code ;
    5. **les signaux publics** de D5, relus chaque mois avec les mêmes mots, les textes de vendeurs comptés à part.
  - **Le classement des besoins de la n°28** se relit avec D5 : la preuve reste ce qui se paie devant un audit ; la douleur
    la plus dite est en amont, dans la revue et dans les contrôles à réécrire (la table des douleurs, plus haut).
  - **La table de correspondance** reste ce que la n°28 en dit, et devient aussi une pièce qu'on montre : ce que le code
    fait, ligne par ligne, face aux principes de l'ANSSI, du NIST et de la CNIL, absences comprises. Chaque ligne nomme le
    texte et sa date, et renvoie à un essai que n'importe qui relance. Elle ne dit jamais « conforme » (R187).
  - **Ce que devient « étiquetée hypothèse »** : l'étiquette reste dans les documents du labo. Un texte public ne porte pas
    d'étiquette, mais il ne dit jamais que la demande est mesurée, ni combien de clients. L'étiquette se lève sur les
    signaux de R207, pas sur des entretiens.
  - **Ce que l'on perd à ne pas interroger** : le segment visé n'écrit pas en public. Tant que le client test et l'usage
    n'ont pas parlé, il reste muet. Les entretiens de R186 restent possibles ; ils ne sont plus une condition.
- **L'attaque de la contradictrice** : relire chaque mois des textes de vendeurs et appeler cela observer, c'est mesurer
  leur publicité.
- **Réponse** (Zhuo, Duflo) : c'est pourquoi les comportements et les pièces primaires pèsent plus que les posts, et que le
  client test pèse plus que tout.
- **Vote** : 23 oui, 1 abstention. 95,8 %. Musk, abstenu à la n°28, vote oui : une table dont chaque ligne s'exécute n'est
  plus du papier.
- **L'abstention de Duflo, développée.**
  - Ce qu'elle conteste : que des textes publics puissent éprouver une vision qui porte sur des gens qui n'écrivent pas.
  - Ce qui la ferait voter oui : une seule question de fait, posée quand l'occasion vient à cinq personnes que la
    Présidence connaît déjà : « votre auditeur ou votre client vous a-t-il déjà demandé quelque chose sur vos agents de
    code, et qu'avez-vous montré ? ».
  - Ce qu'elle propose : cette question, sans campagne. Elle porte sur un acte passé, pas sur une douleur. Elle est posée
    à la Présidence (question 11).
- **Preuve en dix jours** : la table écrite depuis le code de `dev`, au labo ; la grille des cinq sources, avec pour
  chacune où regarder et la première lecture datée.
- **Signal d'arrêt** : une ligne « présent » sans fichier ni essai ; une phrase publique qui dit la demande mesurée.

### R198, amendée. Le dossier est le produit ; la signature est le droit d'entrée

- **Ce que la saisine dit** : « c'est justement ça le système de preuve ».
- **Ce que le Conseil répond** : oui. Le système de preuve, c'est la règle jugée, l'accord donné et le dossier qui les
  garde, ensemble. Le dossier est le produit : c'est ce qu'on remet à celui qui doit répondre. La signature n'est pas le
  produit. Depuis les corrections du dossier, elle est ce qu'il faut pour être admis : d'autres la donnent.
- **Quoi** : le contenu de R198 tient en entier (la demande, le modèle, les gestes de la personne, l'action exacte, une
  clé hors de portée de l'agent, la survie à la suppression, les trous visibles, le paquet de règles exporté). Six
  précisions s'y ajoutent.
  1. **La page du lecteur d'abord.** Avant le format : la page qu'une personne de la qualité ou un auditeur lit en cinq
     minutes. Qui a demandé quoi ; quelle règle a jugé ; qui a accordé quelle action exacte, et pourquoi ; ce qui a été
     fait ; le résultat ; quel modèle. Dans la langue de l'entreprise, avec les mots des audits qui existent (la gestion
     des changements), sans jamais dire « conforme ».
  2. **Aucun format propre.** La canonisation suit la RFC 8785 ; la signature entre dans une enveloppe que d'autres lisent
     déjà (in-toto et DSSE). `[HYPOTHÈSE]` À instruire avec TF-J2-7 (E34, Q29). Le vérificateur du runner reste.
  3. **Silencieux pour l'équipe.** Rien ne s'ajoute au commit ni à la pull request, sauf un lien. Les développeurs
     rejettent la session dans le commit (C1 à C3).
  4. **Pas toute la conversation.** Le dossier garde le brief, les décisions, les actions exactes et le résultat. Un
     contenu sensible y entre par son empreinte ; son texte vit à côté, effaçable sans casser la chaîne.
  5. **Un témoin, le moins cher d'abord.** `[HYPOTHÈSE]` L'empreinte de tête du dossier s'écrit là où l'opérateur n'est
     pas seul à écrire, par exemple dans la pull request quand il y en a une. À instruire (Q31). Rien de plus avant qu'un
     acheteur le demande.
  6. **Lire les reçus des autres, écrire vers leurs outils** : ce n'est pas ici, c'est R206.
- **L'attaque de la contradictrice** : une page du lecteur sans lecteur. Elle sera écrite pour un auditeur imaginaire.
- **Réponse** (Doudna, Shotwell) : la personne de la qualité du client test est le premier lecteur. Avant elle, les textes
  des audits en place donnent la grille, sans rien affirmer de la conformité.
- **Vote** : 23 oui, 1 abstention. 95,8 %. Bezos, abstenu à la n°28, vote oui : le dossier se définit depuis son lecteur,
  et la signature n'est plus la promesse.
- **L'abstention de Hamilton, développée.**
  - Ce qu'elle conteste : une chaîne et une clé tenues par le même opérateur ne prouvent rien à un tiers, qui peut tout
    récrire et tout resigner (C5). La précision 5 ne fait qu'instruire.
  - Ce qui la ferait voter oui : un ancrage hors de l'opérateur, même minimal, décidé avec TF-J2-7 et pas après.
  - Ce qu'elle propose : l'empreinte de tête écrite chez un tiers à chaque fin de mission, et le dire dans le dossier.
- **Preuve en dix jours** : TF-J2-7 lancé en mode développement, comme à la n°28 ; la page du lecteur écrite au labo pour
  une mission réelle du projet TaskForce ; E34.
- **Signal d'arrêt** : une clé de signature lisible par l'agent pendant une mission. Et le format : s'il déborde la preuve
  en dix jours, le dossier garde son format d'aujourd'hui, signé, et l'enveloppe attend.

### R199, amendée. Une couche qui dit qui possède quel moment (second tour)

- **Ce que la saisine demandait** : que Jobs explique son non, sans formule. Sa réponse est au tour de table : oui, on
  perd la maîtrise de ce qui n'est pas ses écrans ; non, ce n'est pas ce qu'il voudrait ; c'est un prix, et il n'était
  pas borné.
- **Quoi** : R199 tient (s'intégrer plutôt que remplacer, l'issue reste l'ancre, le Board gèle, la couche se joint par le
  protocole, rien dans J2). Le prix se borne ainsi.
  - **Demander** appartient à TaskForce. La mission part d'un brief que TaskForce montre et que la personne accepte,
    quelle que soit la source. Ce brief est la copie de la demande au dossier.
  - **Décider pendant la mission** appartient à TaskForce. La carte d'accord ne s'affiche jamais dans l'outil d'un hôte.
  - **L'état se lit chez l'hôte** : où en est l'agent, ce qui attend, un lien. Une personne ne quitte pas son outil pour
    le savoir (Saarinen).
  - **Juger le résultat n'a qu'un lieu par sorte de mission.** Quand une pull request existe, c'est elle : TaskForce n'y
    refait pas la revue, il y joint le lien du dossier et garde au dossier la décision de revue. Sans pull request, c'est
    la remise de TaskForce.
  - **Une source menée au bout d'abord**, puis la seconde. « On s'intègre » ne se dit pas avant deux, et l'issue interne
    reste la troisième (n°28).
  - **Chaque source a son contrat écrit**, qui dit aussi où vit chacun des trois moments.
- **L'attaque de la contradictrice** : un écran de décision qui n'est pas là où les gens travaillent, c'est un trajet de
  plus ; le terrain dit que la gouvernance ne tient que fondue dans le flux (S41).
- **Premier tour** : 21 oui, 2 non (Jobs ; Vestager : commencer par GitHub, c'est commencer par la dépendance que D4 donne
  comme la menace à douze mois), 1 abstention (Norman : deux lieux pour juger font une erreur de mode). 87,5 %.
- **Amendements** :
  - un seul lieu pour juger par sorte de mission, et l'écran de remise le dit (Norman) ;
  - le dossier garde la copie de la demande et la décision de revue : dépendre d'un hôte coûte la porte, jamais la
    preuve (Vestager) ;
  - la carte d'accord arrive à la personne par une notification et un lien, sans qu'elle cherche (réponse à la
    contradictrice).
- **Second tour** : 23 oui, 1 abstention. 95,8 %. Saarinen, abstenu à la n°28, vote oui sur le fond.
- **L'abstention de Jobs, développée.**
  - Ce qu'il conteste : il ne dit plus non à la couche. Il ne vote pas un écran qu'il n'a pas vu : tant que le résultat
    peut se juger à deux endroits, personne ne possède ce moment.
  - Ce qui le ferait voter oui : E32 montrant qu'une mission n'a jamais deux lieux de jugement, et l'écran de remise vu.
  - Ce qu'il propose : une seule source, parfaite, avant toute autre.
- **Preuve en dix jours** : E32 faite, comme à la n°28 ; le contrat écrit de la première source ; le brouillon d'ADR-029
  amendé de ces points, relu par la Présidence.
- **Signal d'arrêt** : une carte d'accord affichée chez un hôte ; ou E32 qui trouve deux lieux pour juger la même mission.

### R200, amendée. Un processus qui porte une réglementation, une convention ou une norme interne

- **Ce que la saisine dit** : « en gros c'est cammunda version compliance quoi, ca me va en soit, mais faudrait faire
  compliance, reglementation, convention, ... ».
- **Ce que cela veut dire, concrètement.** Un processus reste ce que la n°28 en dit : des étapes dans un ordre ; pour
  chacune, qui la fait, qui la signe, quelle preuve elle laisse ; des points de pause qu'on ne saute pas. Ce qu'il porte
  peut être de trois familles.

  | Famille | Des exemples | Qui l'écrit | Ce que TaskForce fournit |
  | --- | --- | --- | --- |
  | **Une réglementation** | Les bonnes pratiques de fabrication et l'Annexe 11 ; 21 CFR Part 11 ; la gestion des changements de SOC 2 ; ISO 42001 ; le contrôle humain de l'article 14 de l'AI Act | L'entreprise, par sa qualité ou sa conformité ; un partenaire qui en répond | Le moteur. Jamais le contenu, jamais un paquet « prévalidé » (R179, R187, ADR-022) |
  | **Une convention d'ingénierie** | Les quatre yeux sur un changement d'agent ; la séparation des tâches (qui lance n'approuve pas) ; la revue de code ; les conventions de commit ; aucun push direct sur la branche principale ; les tests avant la fusion | L'entreprise | Le moteur, et des exemples à reprendre, marqués comme des exemples (les règles par défaut, les workflows par défaut de R165) |
  | **Une norme interne** | Ce que « fini » veut dire ; le gel avant une release ; qui valide une dépense | L'entreprise | Le moteur ; la règle écrite en une phrase, traduite puis vérifiée par du code |

  - **Des paquets** : un processus et ses règles s'exportent et se reprennent. Qui les publie (l'entreprise, un
    partenaire, une communauté) reste à instruire (Q32). TaskForce n'en certifie aucun.
  - **Chaque étape a un auteur et une raison.** Une étape qui n'a jamais rien bloqué ni rien attrapé est signalée à une
    personne, qui la garde ou la retire. Jamais le système seul (Musk, depuis sa fiche).
  - **Aucun lot de plus.** Le seul processus d'E20 porte une étape de chaque famille ; il tient sur une page (Shotwell,
    Gawande).
  - Le reste de R200 tient : la vue en cartes gèle, le processus entre par l'issue et par la conversation, le dessin
    revient à l'équipe de Jobs si la Présidence le lui délègue.
- **L'attaque de la contradictrice** : trois familles, c'est trois fois le contenu que personne n'écrit. Un moteur vide ne
  montre rien.
- **Réponse** (Shotwell, Ait Si Abbou) : le processus d'E20 est écrit par la Présidence, qui joue l'entreprise ; les
  exemples de conventions partent avec le produit ; une étape s'écrit en une phrase.
- **Vote** : 24 oui. 100 %. L'unanimité a été précédée de l'attaque de la contradictrice (charte, §7.5). Shotwell, abstenue
  à la n°28, vote oui : l'extension n'ajoute aucun véhicule.
- **Preuve en dix jours** : la page du processus d'E20 (les étapes, qui signe, la preuve attendue, la famille de chaque
  étape, ce que l'écran dit à chaque état), relue par la Présidence avant W5.
- **Signal d'arrêt** : un contenu réglementaire livré par TaskForce comme le sien. Et, comme à la n°28, W5 livré qui se lit
  encore comme un Board.

### R201, amendée. Trois classes décidées d'avance : part seul, attend une carte, refusé

- **Ce que la saisine dit** : « Bah la fatigue des demandes d'accord oui donc si il peut le faire lui mm go ».
- **Ce que le Conseil répond** : oui, à une condition que R1 impose. Ce n'est jamais l'agent, ni un modèle au moment
  d'agir, qui décide qu'il « peut ». C'est une classe écrite d'avance par une personne.

  | Classe | Ce qui y entre | Ce qui se passe |
  | --- | --- | --- |
  | **Part seul** | Les lectures, dans TaskForce et dans les outils connectés. Les écritures dans la copie de l'agent. Les écritures réversibles que les règles permettent : aujourd'hui cinq, dans TaskForce (créer ou modifier une issue, commenter, créer un projet, créer une note) | Tracé au dossier (R7'). Dit par Cortex : où, et quoi. Annulable d'un geste |
  | **Attend une carte** | L'irréversible : supprimer, pousser hors de la branche de l'agent, toucher un dépôt public, écrire dans un outil externe tant qu'il n'est pas déclaré. Ce qu'une règle de l'entreprise exige. Toute action de classe inconnue. Les trois à la fois (contenu non fiable, données sensibles, sortie) | Une carte : l'action exacte, l'endroit, l'effet, ce que Cortex a compris du but. L'action exécutée est celle de la carte |
  | **Refusé** | Un secret qui sortirait ; un agent qui changerait les règles ; ce que l'entreprise interdit | Refus écrit au dossier, sans carte |

  - **Dans TaskForce, rien à construire** : c'est déjà ce que les règles par défaut font (dossier, point 9). Ce qui manque
    est de le dire (le correctif 2 de R204) et de montrer le geste qui annule, que le secrétariat n'a pas trouvé dans le
    code.
  - **Hors de TaskForce, tout attend aujourd'hui.** Une écriture externe ne passe dans « part seul » qu'outil par outil :
    une personne qui administre l'espace la déclare réversible, nomme son action inverse, et cette inverse a été essayée.
    Le défaut reste la carte. C'est un changement du socle : brouillon d'ADR-030, E33. Pas dans J2.
  - **La carte se mesure.** Par règle, la part des cartes acceptées. Une règle presque toujours acceptée est signalée à
    une personne, qui la reclasse ou la laisse. Jamais le système seul (Harris).
  - **Changer une classe est une décision tracée d'une personne**, versionnée comme toute règle.
  - Le reste de R201 tient : chercher est du code ; proactif ne veut jamais dire s'accorder un droit ; un refus n'est pas
    relancé ; une phrase fausse est corrigée de façon visible.
  - **Ce qui change dans le texte de la n°28** : « une écriture montre une carte, une seule par demande » devient « une
    écriture réversible que les règles permettent part seule, tracée et annulable ; la carte ne vient que pour
    l'irréversible et pour ce qu'une règle exige ».
- **L'attaque de la contradictrice** : « réversible » sera déclaré par une personne fatiguée des cartes. La classe glissera
  vers « part seul », un outil après l'autre.
- **Réponse** (Hamilton, Harris) : chaque déclaration est un changement de règle, tracé, avec son auteur ; l'inverse est
  essayée avant ; et le défaut ne bouge pas.
- **Vote** : 23 oui, 1 abstention. 95,8 %. Harris, abstenu à la n°28, vote oui : la carte devient rare, et une personne
  décide des classes.
- **L'abstention de Bengio, développée.**
  - Ce qu'il conteste : qu'une écriture externe soit jamais vraiment réversible. Créer une issue chez un hôte notifie des
    personnes et déclenche des automatismes ; l'inverse supprime l'objet, pas ce qui est parti.
  - Ce qui le ferait voter oui : qu'un outil ne soit déclaré réversible que si l'essai montre que rien ne sort de l'outil
    quand on y écrit, et que la garde « jamais les trois à la fois » ne puisse pas être relâchée par cette déclaration.
  - Ce qu'il propose : E33 d'abord, sur un outil réel, avant d'écrire une ligne du socle.
- **Preuve en dix jours** : E31, comme à la n°28, relue avec les trois classes ; E33 sur les cinq écritures internes (leur
  inverse défait-elle vraiment ?), sans code du produit.
- **Signal d'arrêt** : une action partie seule dont l'inverse échoue ou laisse une trace dehors ; une classe changée sans
  qu'une personne l'ait décidé. La classe revient alors à la carte.

### R202, amendée. L'inventaire inchangé ; les mots, et la fin du gel, précisés

- **Ce que la saisine demande** : « comment ca arreter le mot souverain et conforme ? ».
- **Ce que « arrêter » veut dire** : cesser d'appliquer ces deux adjectifs à TaskForce dans un texte public. Ni le sujet
  ni la capacité ne s'arrêtent : l'app s'installe toujours chez le client, avec son modèle, et le dossier sert toujours
  ses audits.
  - **« Conforme » est déjà écarté** par R187, que la Présidence a retenue le 13/11/2026 : « on donne rien dans notre
    app, on fournis l infra et l archi qui permette de faire ca ». Seul un auditeur ou une autorité dit qu'une chose est
    conforme ; c'est le client qui l'est, par sa propre validation. Un éditeur qui vend de la preuve et dont une seule
    affirmation de conformité est démentie perd ce qu'il vend.
  - **« Souverain »** : la n°28 établit qu'aucun label européen ne le définit et que l'hébergement de la prod n'est pas
    choisi. C'est un mot que personne ne peut vérifier, et qui deviendrait faux le jour où la prod serait hébergée hors
    d'Europe.

  | Au lieu de | On dit | Ce qui le rend vérifiable |
  | --- | --- | --- |
  | « souverain » | « Installé chez vous. » « Le modèle que vous choisissez, local si vous le voulez. » « Le code est ouvert. » « Vous partez avec vos règles et vos dossiers. » | L'app de bureau embarque le serveur, la base et le modèle ; la licence ; l'export |
  | « rien ne sort » | Seulement pour l'app de bureau avec un modèle local, et en le disant ainsi | La configuration, que le client lit |
  | « conforme », « certifié », « prévalidé » | « Aide à prouver. » « Vos règles, exécutées et tracées. » « Un dossier que votre auditeur vérifie sans nous. » | La table de correspondance (R197), ligne par ligne |

  - **Ce que l'on perd** : deux mots que les gens tapent et que la presse française emploie ; un critère des appels
    d'offres publics (Mazzucato) ; un raccourci pour l'acheteur qui cherche « conforme » à un texte précis.
  - **Ce que l'on garde** : parler de la souveraineté et de la conformité comme des buts du client (« garder la main sur
    vos données et vos modèles », « pour vos audits »). Et, quand l'hébergement sera choisi, une fiche de faits qui répond
    aux critères habituels : où c'est hébergé, sous quel droit, quel modèle, quel code, comment partir.
- **La fin du gel** (le non d'Ait Si Abbou) : au retour du client test, le sort de chaque surface gelée se décide sur
  l'usage observé, celui des non-ingénieurs compris. Une liste du travail d'un projet, par état, en langage clair, reste
  hors du gel.
- **Le reste de R202 tient**, table comprise.
- **L'attaque de la contradictrice** : remplacer un mot par cinq phrases. Personne ne lit cinq phrases.
- **Réponse** (Jobs, Ait Si Abbou) : une phrase par lecteur ; « installé chez vous » fait trois mots.
- **Vote** : 23 oui, 1 abstention. 95,8 %. Ait Si Abbou, qui avait voté non, vote oui : la fin du gel compte désormais le
  non-ingénieur. Saarinen, abstenu à la n°28, vote oui sur le fond.
- **L'abstention de Mazzucato, développée.**
  - Ce qu'elle conteste : renoncer à un mot dont les acheteurs publics font un critère, avant d'avoir de quoi le
    remplacer devant eux.
  - Ce qui la ferait voter oui : la fiche de faits, qui ne peut pas s'écrire tant que l'hébergement n'est pas choisi.
  - Ce qu'elle propose : garder le mot hors des textes publics, et écrire la fiche le jour où l'hébergement est décidé.
- **Preuve en dix jours** : la table de l'inventaire relue par la Présidence, comme à la n°28 ; la table « au lieu de »
  appliquée au communiqué et au brouillon du site, sans une occurrence des deux adjectifs.
- **Signal d'arrêt** : une surface gelée qui reçoit du travail ; l'un des deux adjectifs appliqué à TaskForce dans un texte
  public.

### R203, amendée. Ce que cela change : inchangé, plus un témoin et le pitch de R205

- **Ce que la saisine demandait** : que Duflo développe son abstention. Sa réponse est au tour de table : E30 est un essai
  sans témoin, joué par une personne qui connaît les réponses.
- **Quoi** : R203 tient (l'ordre de J2, E20, le client test, R181, les dates de R183 qui ne courent pas, la recette sur le
  projet TaskForce). Trois précisions.
  - **Un témoin dans E30** : les mêmes dix demandes, sur les mêmes données, posées au modèle nu, sans le harnais, sur le
    banc des modèles. La grille, les seuils et l'ordre sont écrits et tirés avant.
  - **Le pitch** suit R205. Les trois preuves à montrer : un changement courant qui part seul sous une règle, tracé ; une
    action lourde qui attend la bonne personne, accordée sur l'action exacte ; un dossier vérifié sans TaskForce.
  - **La niche (R181)** : D4 la confirme comme le lieu du repli (la place E), et D5 rappelle qu'aucune voix publique n'y
    parle. Le client test reste la seule.
- **L'attaque de la contradictrice** : un modèle nu, sur un projet qu'il ne voit pas, perd d'avance. Le témoin est un
  épouvantail.
- **Réponse** (Li, Duflo) : le modèle nu reçoit les mêmes données dans son contexte. L'essai mesure ce que les outils et
  les règles ajoutent, à armes égales, et ces armes sont écrites avant.
- **Vote** : 23 oui, 1 abstention. 95,8 %. Duflo, abstenue à la n°28, vote oui.
- **L'abstention de Musk, développée.**
  - Ce qu'il conteste : un plan sans aucune date, face à une fenêtre qui en a une. D4 écrit que le dossier doit exister,
    signé et complet, avant le printemps 2027.
  - Ce qui le ferait voter oui : une seule date, celle-là.
  - Ce qu'il propose : la poser. La Présidence a décidé qu'aucune date ne court avant le client test : la question lui
    revient (question 12).
- **Preuve en dix jours** : E30 jouée avec son témoin, tout écrit et daté avant.
- **Signal d'arrêt** : un lot de plus dans J2 avant le client test. Il sort.

### R206. Face à la concurrence (second tour)

- **Quoi** :
  1. **Ne pas refaire ce qui se donne.** La règle et le reçu signé d'une décision existent, gratuits. TaskForce ne s'en
     réclame pas et ne les réinvente pas.
  2. **Parler les formats des autres.** Aucun format propre (R198). Le schéma de ce que le dossier ajoute et son
     vérificateur se publient, ouverts.
  3. **Lire ce que les autres émettent, écrire là où l'auditeur est déjà** : les reçus de la boîte à outils de Microsoft,
     la transcription du fournisseur du modèle ; un outil de conformité, de validation ou de qualité. Ce sont des
     possibilités écrites, chacune avec son contrat. Aucune ne se construit avant qu'un acheteur réel la demande, le
     client test le premier. Le dossier reste complet sans elles.
  4. **Ne jamais dire qui l'on bat.** La table des concurrents reste au labo.
  5. **Le mur le plus probable est d'être adopté sans être payé.** La licence commerciale et le prix se posent avant une
     annonce large, pas après. La Présidence a dit « le prix faudra voir » : la question lui revient (question 10, Q28).
  6. **Devant un acheteur qui se méfie d'un éditeur seul** : l'installation chez lui, le code ouvert, un séquestre s'il le
     demande, la table de correspondance. C'est le dossier fournisseur de R181.
- **L'attaque de la contradictrice** : « lire les reçus de Microsoft, écrire vers Drata » sont quatre intégrations de
  plus, pour une personne, sur la foi d'une table bâtie sur des pages d'éditeurs.
- **Premier tour** : 20 oui, 2 non (Jobs : chaque branchement est une promesse à tenir seul ; Mazzucato : un format publié
  est un bien commun, y renoncer laisse la norme aux plus gros), 2 abstentions (Vestager : nourrir ceux qui tiennent
  l'acheteur ; Hamilton : des interfaces sans contrat). 83,3 %.
- **Amendements** :
  - les enveloppes choisies sont des standards ouverts, et ce que TaskForce y ajoute se publie (Mazzucato, LeCun,
    Nilekani) ;
  - rien ne se construit sans un acheteur qui le demande ; seule l'enveloppe s'instruit avec TF-J2-7 (Jobs, Prabhakar) ;
  - chaque possibilité a son contrat écrit avant d'exister (Hamilton) ;
  - le dossier reste complet et lisible sans aucun de ces outils (Vestager).
- **Second tour** : 23 oui, 1 non. 95,8 %.
- **Le non de Jobs, développé.**
  - Ce qu'il conteste : une liste de possibilités est une liste de promesses. Écrite, elle sera lue comme un plan.
  - Ce qui le ferait voter oui : un seul lecteur et un seul destinataire, nommés, choisis après le client test.
  - Ce qu'il propose : l'enveloppe maintenant, et rien d'autre sur la page.
- **Preuve en dix jours** : E34 ; une page qui liste les branchements possibles, chacun avec son contrat et la mention
  « pas construit ».
- **Signal d'arrêt** : un branchement commencé sans acheteur qui l'ait demandé ; un champ inventé quand un champ existant
  convient.

### R207. Trois signaux surveillés, et le repli écrit d'avance (second tour)

- **Quoi** :
  - **Trois signaux surveillés chaque mois.** Le secrétariat les relit une fois par mois, à une session du labo, et
    écrit leur état au Journal. Première relecture : le 17/12/2026.

    | Signal | Ce qu'on regarde | Ce qu'il déclenche |
    | --- | --- | --- |
    | **A. Un équivalent arrive** | La boîte à outils de Microsoft ou AppTrust de JFrog en disponibilité générale avec l'accord humain et le résultat dans l'enregistrement signé ; ou GitHub qui annonce une attestation de provenance pour les sessions d'agent | La place de R205 ne tient plus seule : le repli |
    | **B. Le dossier devient un doublon** | Un outil de conformité qui accepte comme preuve la transcription du fournisseur du modèle ou les reçus de Microsoft | Le repli : devenir une source pour ces outils |
    | **C. Le client test ne s'en sert pas** | Il n'ouvre pas le dossier, ou ne le montre à personne qui audite | Le dossier n'est pas ce que cet acheteur achète : retour au Conseil, avec ce qu'il a réellement ouvert |

  - **Quatre signaux notés**, regardés quand ils se produisent : un brouillon de l'IETF adopté par un groupe de travail, ou
    AIUC-1 qui nomme un format (s'y aligner, sans pivoter) ; des installations sans aucune demande de licence ni d'aide
    (le schéma des outils libres que personne ne paie) ; un premier acheteur qui exige un SOC 2 ; trois acheteurs de suite
    sans ligne de budget, qui ne peut se déclencher que si des acheteurs sont approchés.
  - **Le signal contraire**, qui confirmerait : un acheteur autre que le client test demande, installe ou paie ; le client
    test montre le dossier à son auditeur.
  - **Le repli, écrit et pas construit** : TaskForce devient la preuve du travail des agents de code dans le logiciel
    validé, branchée sur les outils que l'auditeur lit déjà (l'outil de validation, le système qualité, l'outil de
    conformité). Le client test en est le partenaire de conception. Les briques sont les mêmes. Ce qu'on lâcherait : la
    porte large et le pitch à toute équipe. Ce qui manquerait : la signature électronique au sens de la Part 11, le
    dossier fournisseur, des ventes longues à tenir seul.
  - **Les places écartées** : la passerelle MCP et la provenance du code face au CRA, où trop de capitaux sont en face
    (D4).
- **L'attaque de la contradictrice** : sept signaux que personne ne regarde, c'est un rite. Et un repli tiré d'un seul
  client test, c'est N = 1 pris pour une direction.
- **Premier tour** : 20 oui, 1 non (Shotwell : un pivot préparé est un second véhicule sur le pas de tir), 3 abstentions
  (Musk : sept signaux, c'est quatre de trop ; Gawande : une liste trop longue pour servir ; Prabhakar : personne n'est
  nommé pour regarder). 83,3 %.
- **Amendements** :
  - trois signaux surveillés, quatre notés (Musk, Gawande) ;
  - qui regarde, quand, et où c'est écrit (Prabhakar) ;
  - rien ne se construit pour le repli : il est écrit, c'est tout (Shotwell) ;
  - le repli est une direction, pas une preuve : il repasse au Conseil le jour où un signal se déclenche (Duflo).
- **Second tour** : 23 oui, 1 abstention. 95,8 %.
- **L'abstention de Prabhakar, développée.**
  - Ce qu'elle conteste : le signal qui porte sur des acheteurs ne peut pas se déclencher avec la méthode retenue, puisque
    personne ne les approche. Un signal qui ne peut pas sonner ne protège pas.
  - Ce qui la ferait voter oui : que chaque signal ait une façon de se produire.
  - Ce qu'elle propose : la question de fait de Duflo, ou remplacer ce signal par l'usage observé. Cela dépend de la
    réponse de la Présidence (question 11).
- **Preuve en dix jours** : la grille écrite au labo, avec, pour chaque signal, la page à regarder et son état au
  17/11/2026.
- **Signal d'arrêt** : un mois sans relecture. La grille est morte ; le Journal le dit, et la place redevient une
  hypothèse sans garde.

### Les votes en une table

| R | Version | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R196 | Remplacée par R205 | 23 | | Vestager | 95,8 % (19 au premier tour) |
| R197 | Amendée | 23 | | Duflo | 95,8 % |
| R198 | Amendée | 23 | | Hamilton | 95,8 % |
| R199 | Amendée | 23 | | Jobs | 95,8 % (21 au premier tour) |
| R200 | Amendée | 24 | | | 100 % |
| R201 | Amendée | 23 | | Bengio | 95,8 % |
| R202 | Amendée | 23 | | Mazzucato | 95,8 % |
| R203 | Amendée | 23 | | Musk | 95,8 % |
| R204 | Retenue par la Présidence, non revotée | | | | |
| R206 | Nouvelle | 23 | Jobs | | 95,8 % (20 au premier tour) |
| R207 | Nouvelle | 23 | | Prabhakar | 95,8 % (20 au premier tour) |

### Ce que deviennent les non et les abstentions de la n°28

| À la n°28 | Ce que le membre contestait | Ce qui a changé | Son vote ici |
| --- | --- | --- | --- |
| Musk, non sur R196 | Une niche d'une niche : vendre une preuve au plus petit cercle | La porte devient le tri du travail des agents, pour toute équipe sans équipe plateforme | Oui sur R205 |
| Nadella, abstention sur R196 | Un conflit d'intérêts | Il vote sur le fond | Oui sur R205 |
| Musk, abstention sur R197 | Une table remplie par soi-même est du papier | Chaque ligne renvoie à un essai qu'on relance | Oui |
| Bezos, abstention sur R198 | La signature d'abord, sans client qui la demande | La page du lecteur d'abord ; la signature comme droit d'entrée | Oui |
| Jobs, non sur R199 | Le prix d'une couche n'était pas borné | Qui possède quel moment ; une source d'abord | Abstention : il n'a pas vu l'écran |
| Saarinen, abstention sur R199 et R202 | Un conflit d'intérêts | Il vote sur le fond | Oui, deux fois |
| Shotwell, abstention sur R200 | Chaque précision sur W5 est une promesse de plus | Aucun lot de plus : une étape de chaque famille dans le processus d'E20 | Oui |
| Harris, abstention sur R201 | Une carte par écriture reste une fatigue | La carte devient rare ; une personne décide des classes | Oui |
| Ait Si Abbou, non sur R202 | La fin du gel ne comptait pas le non-ingénieur | Le sort se décide sur l'usage observé | Oui |
| Duflo, abstention sur R203 | Un essai sans témoin | Le modèle nu comme témoin | Oui |

### Questions à la Présidence

Les dix questions de la n°28, mises à jour, puis quatre nouvelles. Chacune avec ses options et l'avis de la majorité, pour
une réponse d'une ligne.

1. **La place** (R205, qui remplace R196). A : la place ajustée de R205. B : la phrase de R196 telle qu'écrite à la n°28.
   C : le repli tout de suite, sur le seul logiciel validé. *Avis de la majorité : A (23).*
2. **Le Board** (R199, R202). A : le garder et continuer d'y travailler. B : le geler, l'issue restant l'ancre, et décider
   de son sort au retour du client test, sur l'usage observé. C : le supprimer maintenant. *Avis : B (23).*
3. **La source de travail externe** (R199). A : dans J2. B : après le client test, E32 se faisant maintenant. Et la
   première menée au bout : GitHub, où vivent le code et la revue, ou Linear ? *Avis : B, puis GitHub d'abord et Linear
   ensuite. Vestager préfère ne pas commencer par GitHub.*
4. **Le workflow** (R200). La saisine dit « ca me va en soit » : le Conseil le lit comme un accord sur le déroulé d'un
   processus dans l'issue et la conversation, étendu aux trois familles. Reste : le dessin est-il délégué à l'équipe de
   Jobs ? *Avis : oui.*
5. **Cortex** (R201). A : une carte par écriture, comme à la n°28. B : les trois classes ; dans TaskForce rien ne change,
   c'est déjà le cas ; hors de TaskForce, outil par outil, après J2 (ADR-030, E33). C : comme B, mais l'extérieur dès
   J2. *Avis : B (23).*
6. **Ce qu'on arrête** (R202), un oui ou un non par ligne, inchangé : masquer Smart Assign en entier ; masquer l'agent
   Copilot tant qu'il n'ouvre pas de dossier ; retirer « Show all links » ; laisser les 97 préréglages non connectés
   visibles avec la mention « pas encore essayé ». *Avis : oui, oui, oui, et la mention.*
7. **Les dix jours** (R203). Les six correctifs sont lancés (R204). Ensuite : TF-J2-7, avec la page du lecteur, puis W3 ;
   au labo, la table de R197, E30 avec son témoin, E34 et la grille des signaux. Oui ou non ? *Avis : oui (23).*
8. **La prochaine recette** (R203, E30) : sur un projet « TaskForce » créé dans l'app à partir de la roadmap publique ; et
   avec le modèle nu comme témoin ? *Avis : oui aux deux.*
9. **Les mots** (R202) : après la précision, la Présidence renonce-t-elle à l'adjectif « souverain » appliqué à TaskForce
   en public, « conforme » étant déjà écarté par R187 ? *Avis : oui (23). Mazzucato dit ce que cela coûte devant un
   acheteur public.*
10. **Le juriste, la licence et le prix** (Q28, R206). A : avant toute édition payante seulement, comme à la n°28. B : une
    licence commerciale et un prix écrits avant toute annonce large, parce que le mur le plus probable est d'être adopté
    sans être payé ; le juriste avant l'édition payante. *Avis : B.*
11. **Une question de fait** (R197, R207). La Présidence accepte-t-elle de poser, quand l'occasion vient et sans campagne,
    une seule question à des personnes qu'elle connaît déjà : « votre auditeur ou votre client vous a-t-il déjà demandé
    quelque chose sur vos agents de code, et qu'avez-vous montré ? ». *Avis : oui ; ce n'est une condition d'aucune
    recommandation.*
12. **Une date** (R203). La Présidence a décidé qu'aucune date ne court avant le client test. Musk en demande une seule :
    le dossier complet et signé avant le 31/03/2027, parce que D4 donne six à douze mois. A : aucune date. B : celle-là.
    *Avis : le Conseil n'a pas voté ; la relecture mensuelle des signaux tient lieu d'horloge.*
13. **Reddit et LinkedIn** (D5). Les deux étaient fermés à la recherche. Seule une personne connectée peut les lire. La
    Présidence le fait-elle, avec les mêmes mots, ou ces deux terrains restent-ils non lus ? *Avis : les lire une fois,
    avant la relecture du 17/12/2026.*
14. **Le repli** (R207). La Présidence accepte-t-elle, comme direction écrite et non construite, le logiciel validé comme
    lieu du repli ? *Avis : oui (23).*

## Décision de la Présidence

Tranchée le 22/11/2026, en conversation, par une délégation. La Présidence avait répondu à cette séance le 17/11/2026 par un
message dont deux lignes tranchent R200 et R202 (elles sont consignées au [PV n°28](./2026-11-17-le-recentrage.md)) et dont le
reste est la saisine de la [séance n°30](./2026-11-17-finir-la-v1.md). La n°30 a remplacé les quatorze questions de cette
séance par dix-huit points. Le secrétariat les a remontés à la Présidence, chacun avec l'avis de la majorité, et a recommandé
de suivre la majorité partout. La Présidence répond, mot pour mot :

> « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est partie »

**La Présidence délègue.** Les dix-huit points de la n°30 sont tranchés selon l'avis de la majorité du Conseil, tel que le PV
n°30 l'écrit. Les recommandations de cette séance sont **retenues par délégation de la Présidence au Conseil, selon l'avis de
sa majorité**. Sa raison est la délégation : le secrétariat ne lui en prête aucune autre (charte, §2.4).

Dans ce qui suit, **la décision** est ce que la majorité a écrit au PV et que la délégation retient. Les **précisions du
secrétariat** sont à part.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R205, qui remplace R196 | Retenue | La délégation du 22/11/2026 |
| R197 à R203, amendées | Retenues dans cette version ; R200 et R202 dès le 17/11/2026 | La délégation ; « R200: ok » ; « R202: ok je comprends oui on s'engage pas, on fourni juste le necessaire pour augmenter la confiance » ([PV n°28](./2026-11-17-le-recentrage.md)) |
| R206 | Retenue | La délégation du 22/11/2026 |
| R207 | Retenue | La délégation du 22/11/2026 |

- **R205, retenue** (n°30, point 1, option A) : la place ajustée. TaskForce fait passer le travail des agents de code par les
  règles de l'entreprise ; ce qui est courant part seul, ce qui est lourd attend la bonne personne, et chaque tâche laisse un
  dossier complet, vérifiable sans TaskForce ; il se pose sur les outils qu'elle a déjà et s'installe chez elle. R196 est
  remplacée.
  - **Précision du secrétariat** : la place reste étiquetée `[HYPOTHÈSE]` dans les documents du labo, comme R205 l'écrit ;
    l'étiquette se lève sur les signaux de R207.
- **R206, retenue** : ne pas refaire ce qui se donne ; parler les formats des autres ; ne se brancher que sur la demande d'un
  acheteur ; ne jamais dire qui l'on bat.
  - **La décision** (n°30, point 13, option B) : la licence commerciale et le prix sont écrits avant toute annonce large ;
    tous les droits du code sont chez un seul titulaire ; le juriste passe avant l'édition payante.
- **R207, retenue** : trois signaux surveillés chaque mois, quatre notés, et le repli écrit d'avance.
  - **La décision** (n°30, point 18) : le logiciel validé est le lieu du repli, écrit et non construit.
  - **Précision du secrétariat** : la première relecture des signaux est celle que R207 fixe, le 17/12/2026 ; le secrétariat
    la tient et l'écrit au Journal.

**Les quatorze questions de cette séance** ont été remplacées par les dix-huit points de la n°30. La table reprend celle du PV
n°30 (« Ce que deviennent les quatorze questions de la n°29 ») et dit, pour chacune, ce que la délégation tranche.

| Question de cette séance | Ce qu'elle est devenue (PV n°30) | Ce qui est tranché |
| --- | --- | --- |
| 1. La place | Point 1, inchangée | A : la place ajustée de R205 |
| 2. Le Board | Point 2 | B : gelé, l'issue reste l'ancre ; son sort se décide au point de décision, sur l'usage observé |
| 3. La source de travail externe | Points 3 et 4 | En v1, Claude Code seulement, par le serveur MCP et le plugin qui existent ; la première vraie source après le client test, GitHub puis Linear ; le contrat d'une source de R209 : oui |
| 4. Le workflow | Tranchée sur le fond (« R200: ok ») ; reste le point 5 | Le dessin est délégué à l'équipe de Jobs |
| 5. Cortex et les classes | Point 6, complété par le point 7 | B : les trois classes ; hors de TaskForce, outil par outil, après la v1. Le geste de fin : la vérification automatique, la décision d'une personne ; la fusion sans personne écrite, éteinte, pas construite en v1 |
| 6. Ce qu'on arrête | Point 10 | Smart Assign masqué ; l'agent Copilot masqué tant qu'il n'ouvre pas de dossier ; « Show all links » retiré ; la mention « pas encore essayé » sur les 97 préréglages |
| 7. Les dix jours | Point 17 | Remplacée par l'ordre de la v1 (R217) et ses dix critères (R218) : oui |
| 8. La prochaine recette | Point 18 | Oui : sur le projet TaskForce, avec le modèle nu comme témoin (E30) |
| 9. Les mots | Sortie de la liste | Le secrétariat la lit comme tranchée par « R202: ok je comprends oui on s'engage pas » ; une ligne de la Présidence suffit si ce n'est pas le sens |
| 10. Le juriste, la licence, le prix | Point 13, avec les droits du code | B : la licence commerciale et le prix avant toute annonce large ; le juriste avant l'édition payante |
| 11. Une question de fait | Point 18 | Oui. C'est un geste de la Présidence elle-même : il est inscrit comme une action de la Présidence, sans date (Q38) |
| 12. Une date | Remplacée par le point 17 | B : le point de décision trente jours après la remise au premier client test, au plus tard le 31/03/2027 (voir la précision du [PV n°30](./2026-11-17-finir-la-v1.md)) |
| 13. Reddit et LinkedIn | Point 18 | Oui. C'est un geste de la Présidence elle-même, connectée : il est inscrit comme une action de la Présidence, sans date (Q39) |
| 14. Le repli | Point 18 | Oui : le logiciel validé, écrit et non construit ; il est aussi une des quatre issues du point de décision |

## Notes du secrétariat

- **Le dossier** : celui de la n°28 (le code de `dev` au commit `067c577b`, la recette de la 1.17.0, D1 à D3), plus D4 et D5,
  faites le 17/11/2026 sur des pages publiques seulement, sans connexion ni formulaire.
- **Les limites des deux recherches**, telles que leurs auteurs les signalent, gardées telles quelles :
  - D4 : les pages d'éditeurs sont des sources sur ce qu'ils annoncent, pas sur ce que leurs produits font ; la fenêtre
    de temps est une hypothèse ; des pages ont été lues par l'outil de recherche sans être rouvertes ; aucun prix public
    pour Docker AI Governance, Drata, Zenity ni Ketryx.
  - D5 : Reddit était fermé à l'outil de recherche, et aucun post LinkedIn n'a été lu sans connexion ; le terrain lu est
    Hacker News, des blogs, la presse professionnelle, des conférences et des offres d'emploi ; les pages lues par extrait
    seulement sont marquées. Sur les onze signaux de preuve, sept viennent de vendeurs ; aucun auditeur ni responsable
    qualité ne parle à la première personne. Le terrain public est muet sur les 10 à 250 personnes.
  - D5 garde des adresses pour la vérification : ce PV n'en publie aucune.
- **Les deux corrections de D4 à la n°28**, et ce qu'elles changent, sont à la pièce 1. En résumé : la place de R196 telle
  qu'écrite perd sa moitié « sous ses règles », et sa moitié « preuve » se resserre sur le dossier entier avec l'accord
  humain, chez le client ; R198 garde son contenu, mais la signature y passe d'argument à droit d'entrée, et « regarder le
  brouillon de l'IETF » devient « ne pas faire un format de plus ». Le PV de la n°28 ne se réécrit pas : si la Présidence le
  veut, une note du secrétariat datée y renvoie à cette séance, à la publication.
- **Ce que le secrétariat a relu lui-même, le 17/11/2026** :
  - à la source, trois pages, qui confirment D4 : la page de Microsoft sur les reçus de décision (Ed25519, RFC 8785,
    chaînage, vérification hors ligne ; rien sur l'accord humain, le résultat ni l'endroit de la clé) ; le billet de JFrog
    du 12/10/2026 (enregistrement signé en in-toto et DSSE, Cursor, OpenCode et Claude Code, les deux phrases citées, ni
    date ni prix) ; l'article d'Anthropic du 11/08/2026 (Claude Code en ligne de commande et dans l'app de bureau, les
    exclusions, rien sur une signature) ;
  - dans le code : les trente règles par défaut, leurs classes et leurs actions inverses
    (`resources/harness/default.rules.json`) ; les classes du socle, dont `mcp.write` parmi les actions à sens unique
    (`RulesFloor.java`) ; la façon dont Cortex classe un outil externe en lecture ou en écriture (`CortexGate.java`) ;
  - le reste de D4 et tout D5 n'ont pas été rouverts : leurs étiquettes sont celles de leurs auteurs.
  - Aucun `[À VÉRIFIER]` n'a été promu.
- **La consigne sur les conflits d'intérêts** : la Présidence l'a donnée pour cette séance (« les conflits d'interet je
  m'en moque »). Le secrétariat l'applique ainsi : l'intérêt se déclare, puis le membre vote sur le fond. Ce n'est pas un
  changement du règlement (charte, §2.5). Intérêts déclarés :
  - Musk : d'après sa fiche, SpaceX s'est engagé en juin 2026 à racheter Cursor, un agent de code. La n°28 ne l'avait pas
    relevé : c'est un oubli du secrétariat ;
  - Nadella : Microsoft (Agent 365, la boîte à outils, GitHub). Rien de ce qu'il dit ici n'est une annonce : il ne connaît
    la documentation et la proposition d'accord lié à l'action que par le dossier ;
  - Bezos : Amazon (AgentCore, CloudTrail, Kiro) ;
  - Saarinen : Linear ;
  - Zhuo : Meta, que le sujet ne réveille pas.
- **« Les abstentions faut les développer »** : chaque non et chaque abstention porte ses trois points (ce qui est contesté,
  ce qui ferait voter oui, ce qui est proposé à la place), pour la n°28 dans la table « ce que deviennent » et au tour de
  table, pour cette séance sous chaque recommandation.
- **L'accord de la Présidence avec Musk** (R196, R197) n'a pas été plaidé : Doudna, Jobs et Duflo ont voté non au premier
  tour de R205, et la contradictrice a attaqué la place ajustée. Aucun rappel à l'ordre pour flatterie n'a été nécessaire.
- **Hors fiche, hors champ, écarts** :
  - Musk : sa fiche porte sur la suppression, la cadence et la revue croisée entre modèles. « Ce qu'il construirait en
    logiciel » en est une transposition ; les faits qu'il cite viennent de D5 ;
  - Jobs : sa fiche refuse une couche tierce entre la plateforme et le développeur. Ici, c'est TaskForce qui est la couche
    posée sur les outils d'un autre : la transposition est celle du secrétariat. Il ne connaît Linear, Jira, GitHub et MCP
    que par le dossier ;
  - Hamilton : même anachronisme ; elle parle de signature et de témoin depuis sa grille (aucune modification sans raison
    tracée) ;
  - Harris vote oui à « ce qui est courant part seul » : ce n'est pas un écart, sa fiche demande des approbations pensées
    contre la fatigue du clic ;
  - Saarinen vote le gel d'un tableau : c'est dans sa fiche (ce qu'on refuse d'y mettre) ;
  - Duflo dit qu'observer vaut mieux que demander : transposition de sa méthode à un marché de logiciel, hors champ ;
  - Bezos, hors champ sur les formats de signature ; Azoulay, sur SOC 2 et ISO ; Vestager, sur JFrog et GitHub ; Rus, sur
    la presse informatique ; Doudna, Gawande et Li transposent leur méthode.
- **Deux désaccords entre les recherches**, laissés tels quels : D4 demande le dossier signé et complet avant le printemps
  2027 ; D5 voit le mur dans des mois passés sur la signature et le format. Et D5 propose cinq à dix entretiens ; la
  Présidence écarte cette méthode ; le Conseil en garde une seule question de fait, comme une question.
- **Sources manquantes** :
  - Reddit et LinkedIn, non lus ;
  - aucune parole d'auditeur ni de responsable qualité à la première personne ;
  - rien sur les équipes de 10 à 250 personnes ;
  - aucun prix public des offres les plus proches ; aucune date de disponibilité pour JFrog ;
  - la proposition d'accord lié à l'action de Microsoft n'a été lue que par l'outil de recherche ;
  - celles de la n°28 restent manquantes (le texte du règlement 2026/1744, le vote sur NIS2, le guide de l'ANSSI relu).
- **Garde-fous** : aucun nom de client ; le premier client test reste « le premier client test ». Aucune adresse de D5.
  Aucune personne privée nommée : les posts sont cités par leur support, leur date et le rôle de leur auteur ; les
  brouillons de l'IETF par l'adresse du catalogue ; le billet de JFrog par son auteur institutionnel ; l'éditeur de
  conformité mis en cause dans des sources secondaires n'est pas nommé.

## Suites

- Le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal, après relecture de la Présidence.
- À `Questions-ouvertes.md` : Q31 (le témoin : où ancrer l'empreinte de tête du dossier hors de l'opérateur), Q32 (qui
  écrit les processus et les paquets de règles, et ce que TaskForce donne comme exemples), Q33 (la classe d'une écriture
  externe : qui la déclare, et comment prouver son inverse). Et trois mises à jour : Q27 (D5 : le terrain public est muet),
  Q28 (D4 : la licence commerciale et le prix avant l'adoption), Q29 (D4 : in-toto et DSSE plutôt qu'un format propre).
- Si la Présidence les retient, à `experiences/Experiences.md` : E33 (l'action inverse défait-elle vraiment ?), E34 (le
  dossier dans une enveloppe standard, vérifié par un outil qui n'est pas le nôtre), et un amendement à E30 (le modèle nu
  comme témoin). Aucune n'est inscrite avant sa décision.
- Si R201 amendée est retenue : le brouillon d'ADR-030 (la classe d'une écriture externe), à relire par la Présidence.
- Si R199 amendée est retenue : le brouillon d'ADR-029 de la n°28 à amender (qui possède quel moment ; une source d'abord ;
  le lieu unique du jugement).
- Au labo, sans rien prendre à J2 : la page du lecteur du dossier (R198) ; la table de correspondance, un essai derrière
  chaque ligne (R197) ; la grille des cinq sources et celle des trois signaux, avec leur état au 17/11/2026 (R197, R207) ;
  la page du processus d'E20 avec ses trois familles (R200) ; la table « au lieu de » appliquée au communiqué (R202) ; la
  page des branchements possibles (R206).
- En mode développement, après la décision : rien de plus que la n°28. Les six correctifs sont lancés (R204) ; TF-J2-7
  suit.
- Après la décision de la Présidence, rangé le 22/11/2026 :
  - au registre de la charte (§12) et au Journal : « la Présidence délègue au Conseil et tranche les séances n°28 à n°30 » ;
  - à `Questions-ouvertes.md` : Q31, Q32 et Q33 mises à jour, chacune avec son statut daté ; Q38 et Q39, deux actions de la
    Présidence, sans date (la question de fait ; Reddit et LinkedIn lus une fois) ;
  - à `experiences/Experiences.md` : E33 et E34 entrent, retenues ; E30 entre avec l'amendement de cette séance ;
  - le projet d'[ADR-030](../../decisions/ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md), la classe d'une écriture externe
    ; le projet d'[ADR-029](../../decisions/ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md), amendé selon R199.
- Restent, après ce rangement :
  - au secrétariat : la première relecture des trois signaux de R207, le 17/12/2026, écrite au Journal ;
  - à la Présidence : relire le projet d'ADR-030 ; Q38 et Q39 ;
  - au labo : les pièces listées plus haut (la page du lecteur, la table de correspondance, les deux grilles, la page du
    processus d'E20, la table « au lieu de », la page des branchements possibles).
- Rien ne migre vers `v1/` sans tâche ni ADR (quarantaine, [`CLAUDE.md`](../../CLAUDE.md) §2).

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
