---
id: conseil-seance-2026-11-15-le-run-et-les-petits-modeles
title: "Conseil d'Avenir : séance du 15/11/2026"
doc_type: pv-seance
statut: active
date: "15/11/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, run, runner, conteneurs, isolement, modeles-de-decision, calibration, entrainement, lora, rgpd, ai-act, harnais]
related:
  - "../README.md"
  - "./2026-11-13-le-workflow-pilotable.md"
  - "./2026-11-13-le-workflow-pilotable-plan-des-lots.md"
  - "./2026-11-13-le-marche-a-prendre.md"
  - "./2026-11-13-depasser-camunda.md"
  - "./2026-10-29-intelligence-possedee.md"
  - "../../decisions/ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "../../decisions/ADR-025-DRAFT-un-seul-moteur-de-regles.md"
  - "../../decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../../experiences/Experiences.md"
  - "../../Questions-ouvertes.md"
---

# Séance du 15/11/2026 : le run sur la machine et les petits modèles de décision

> Simulation : les membres sont des personnages simulés, à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **En bref.** La vue d'un run existe déjà en grande partie : l'état, l'étape en cours parmi cinq, le temps écoulé, les fichiers
> changés comptés en direct, les tests une fois passés. Il manque l'état des tests pendant qu'ils tournent, jusqu'à quinze minutes
> de silence, et toute estimation du temps restant. L'environnement de run sur la machine existe aussi : l'app desktop et le runner
> font déjà travailler Claude Code chez la personne, sous les règles, sans cloud. Ce qui manque est l'isolement du poste, que le
> conteneur apporte en option, jamais en prérequis. MANTA adapte une base ouverte par LoRA et lui ajoute une tête qui note chaque
> option, apprise sur 8,5 millions de décisions étiquetées ; sa recette et sa méthode de calibration attendent son rapport
> technique. Le Conseil recommande de tester un modèle de décision existant avant d'en entraîner un, d'amender R175 pour le labo
> seulement, de ne jamais laisser un modèle juger des personnes, et de faire d'une leçon tirée des runs une proposition de règle
> qu'une personne accepte et que la banque rejoue. Huit recommandations, R188 à R195, toutes à 90 % au moins, cinq au second tour.
> Yann LeCun, contradicteur, a obtenu l'isolement par défaut pour un dépôt venu du dehors, et qu'une leçon ne soit proposée
> qu'après un gain sur des cas qu'elle n'a pas vus naître.
>
> **Un constat hors saisine** : Smart Assign, dans le code, pèse la réussite passée de chaque personne pour proposer à qui confier
> une issue. C'est la zone que l'AI Act classe à haut risque à partir du 02/12/2027 (R192).
>
> **Décision de la Présidence (16/11/2026)** : R188 à R195 retenues. R188, R189, R192 et R194 sont amendées : un seul chiffre au
> lieu d'une fourchette, l'isolement par défaut partout, pas de liste de refus écrite d'avance sauf la ligne de la loi, une
> leçon qui durcit activée seule. Rien ne s'exécute ni ne s'entraîne pour l'instant au titre de R190, R191 et R193
> ([décision](#décision-de-la-présidence)).

- **Saisine** (Présidence, 15/11/2026, en conversation, mot pour mot) :
  - « Quand on lance les workflows faudrait vraiment qu'on puisse visualiser tout ca si possible : Run #145, Status Running,
    Current step Architecture Spec, Files modified 12, Tests Running, Estimated 4 min. Peut etre pas tout mais running, estimated
    time, current step, tu vois ? Est ce que c'est deja le cas ? Je trouve ca hyper pertinent, en fait ca devient un env de run
    sur la machien auth, plus besoin d'aller payer du cloud, sauf si la personne le souhaite mais avec Docker ca fonctionne tres
    bien quoi voila tout simplement. Bon enfin jsp si c'est une bonne idee la partie run la mais voila, a discuter avec le
    conseils, si techniquement c'est viable ou pas du tout si on peut loger ca sur la machine utilisateur facilement mais bref. »
  - Puis, sur un modèle vu le même jour, MANTA : « Tu vois 27B et 4B, ca veut dire que le scope entre 4B et 27B pour une seule
    machine (deja une bonne machine mais tout le monde peut faire tourner entre 4B et 12-14B je suppose, en entreprise du moins)
    donc on doit pouvoir reussir a vraiment faire du bon travaille mm avec des petits models quoi. Enfin t'image c'est assez genial
    quand mm, mais comment ils ont fait ? Entrainement suppervise ou autre ? J'ai pas de pb pour faire de l'entrainement sur ma
    machine si necessaire et release des models tout fais expres pour taskforce hein, faut juste que ce soit pertinent, genre la
    ca l'ai c'est precis, un use case precis quoi. C'est pour ca que je voulais que les entreprises puissent elles mm justement
    creer leur propre model via les donnees qu'elles rentrent dans taskforce quoi. Qui deviendrais donc opti pour ce qu'elles
    font. Qu'en penses le conseil ? »
  - Puis, avec le lien d'un post LinkedIn d'un créateur de contenu, intitulé « Google just open-sourced its Harness² », ouvert
    sans connexion : « Ca aussi donne au conseil ca peut etre interressant pendant qu'il process l'autre poste ».
  - **Les questions à trancher** :
    1. la vue d'un run qui tourne : ce qui existe déjà, ce qui manque, d'où viendrait une estimation honnête, et à quel lot cela
       revient (W1, W5 ou W9 du plan des lots de la n°25) ;
    2. un environnement de run sur la machine de l'utilisateur : viable ou non, pour qui ; les briques d'aujourd'hui ; un conteneur
       par run, son isolement face au worktree, sous Windows, macOS et Linux, sur les machines des entreprises de 10 à 249
       personnes, avec le GPU des modèles locaux ; la licence de Docker Desktop et les autres moteurs ; le cloud en option ; ce que
       cela change à « l'IA propose, une personne décide, le moteur exécute » ;
    3. les petits modèles de décision et l'entraînement : MANTA sur les faits ; comment se construit un tel modèle ; quelles
       décisions de TaskForce y sont prêtes ; R175 et E12 ; les modèles propres à chaque entreprise (le dossier comme jeu
       étiqueté, où l'on entraîne, les adaptateurs, la banque comme barrière, le RGPD, l'AI Act, le GxP) ; ce qu'une machine
       peut entraîner et faire tourner ;
    4. ce que cela change pour J2 et E20, le plan des lots (W0 à W9, et le test à blanc ajouté à W6 le 15/11), la R&D et le pitch ;
    5. ajoutée en cours de préparation : un harnais qui apprend de ses runs, qu'en prendre pour TaskForce ? À rapprocher du harnais
       de TaskForce (les règles par couches au-dessus d'un socle, les accords, le dossier, la banque, les rejeux), de R175, des
       modèles par entreprise, et de « l'IA propose, une personne décide ».
  - **Horizon** : J2 jusqu'à E20, puis l'après-J2. Les dates passent après le client test (décision de la Présidence sur la séance
    n°26).
- **Formation** : séance n°27, plénière (24). La question touche le produit, la technique, le droit et la stratégie : c'est un
  choix structurant (charte, §5).
  - Impulsion : Steve Jobs, Elon Musk, Jeff Bezos, Gwynne Shotwell.
  - Pont : Satya Nadella, Mariana Mazzucato, Arati Prabhakar, Kenza Ait Si Abbou.
  - Harmonie : Margrethe Vestager, Audrey Azoulay, Nandan Nilekani, Tristan Harris, Yuval Noah Harari.
  - Science : Yoshua Bengio, Yann LeCun, Fei-Fei Li, Margaret Hamilton, Daniela Rus, Jennifer Doudna, Esther Duflo, Atul Gawande.
  - Design : Don Norman, Julie Zhuo, Karri Saarinen.
  - **Contradicteur** : Yann LeCun. Il n'a jamais tenu ce rôle. Son angle (les modèles ouverts, les limites des LLM, des bacs à
    sable bien appliqués) est au centre des trois questions ; il doit attaquer le consensus qui se forme, même s'il le partage.
    Doudna l'était à la n°26.
  - **Ordre de parole**, tiré au sort le 15/11/2026 à 21:16 UTC (`shuf`) : Karri Saarinen, Tristan Harris, Daniela Rus, Don
    Norman, Nandan Nilekani, Steve Jobs, Jennifer Doudna, Atul Gawande, Margaret Hamilton, Elon Musk, Yann LeCun, Julie Zhuo,
    Margrethe Vestager, Arati Prabhakar, Audrey Azoulay, Mariana Mazzucato, Kenza Ait Si Abbou, Fei-Fei Li, Esther Duflo, Jeff
    Bezos, Gwynne Shotwell, Satya Nadella, Yoshua Bengio, Yuval Noah Harari.
  - **Règle de vote** (charte §6.5) : 90 % des présents, soit 22 oui sur 24 au moins.
- **Fiches** : aucune fiche rafraîchie. Toutes ont moins de 30 jours au 15/11/2026 : la plus ancienne date du 21/10/2026, soit 25
  jours ; Norman, Zhuo et Saarinen datent du 28/10, Ait Si Abbou du 26/10, les vingt autres du 21/10. Jobs et Hamilton, sièges
  historiques, ne se rafraîchissent que sur une nouvelle source historique ; aucune n'est apparue. Les conflits d'intérêts que le
  sujet du jour réveille sont aux notes du secrétariat.

## Dossier

Constitué le 15/11/2026 par le secrétariat. Sur TaskForce : le code de `dev` au commit `3da4f4a8`, copié en lecture seule ; les
relevés du 15/11 (produit, technique, IA, entreprise), qui citent leurs sources ; `taskforce-docs` (`feature/lean-oss`,
`7bbcbc5`). Sur le reste : des pages publiques seulement, lues ce jour par le secrétariat et trois agents de recherche, sans
connexion ni formulaire. Les faits qui portent une recommandation ont été relus à la source par le secrétariat : les fiches et le
code de MANTA, les billets de Cloudflare et de Liquid AI, le dépôt et l'article de Harness², le billet de Prime Intellect, la page
de Gemma 4, la table d'Unsloth. La saisine couvrant cinq questions, le dossier compte dix points et cinq pièces du secrétariat.

1. `[ÉTABLI]` **Ce que la vue d'une mission montre déjà** (`frontend/components/layout/work-view.tsx`,
   `frontend/components/delivery/`).
   - L'état, une marque et une phrase ; l'étape en cours parmi cinq (Understand, Plan, Do, Check, Hand over), chacune avec son
     état. Depuis W0, le serveur calcule l'étape lui-même, sur les mêmes cas que l'écran (`MissionSteps.java`,
     `contracts/mission-steps/cases.json` ; PR #535 et #537).
   - Le temps : la durée d'une mission finie (`workMinutes`), sinon le temps écoulé depuis que le runner l'a prise
     (`elapsedMinutes`), dit « {minutes} min » (`work-view.tsx:237`, `constants_en.ts:1631`).
   - Les changements, fichier par fichier, avec leur compte (« {count} files ») et les lignes ajoutées et retirées, relus toutes
     les deux secondes pendant le travail (`mission-changes.tsx:23` et `336-344`) ; les textes le disent, les comptes bougent
     pendant que l'agent écrit (`constants_en.ts:1654-1661`).
   - Les tests, une fois passés : « Tests passed: {passed} of {total} », « Tests failed: {passed} of {total} passed », « Tests not
     run », « Tests took too long » (`constants_en.ts:1769-1776`).
   - Les accords en attente, décidés sur place ; la pull request ; la preuve. La vue relit la mission et sa chronologie toutes les
     2 s, sa preuve toutes les 5 s (`work-view.tsx:36-37`).
   - Les colonnes de `delivery_runs` qui datent une mission : `created_at` (V86), `claimed_at` et `heartbeat_at` (V88), `ended_at`
     (V110) ; ses tests : `tests_command`, `tests_ran`, `tests_passed`, `tests_passed_count`, `tests_total` (V110), `tests_stale`
     (V122) ; et `branch`, `commits`, `outcome`, `work_mode`. La chronologie (`delivery_run_events`, V96) et les fichiers
     (`delivery_run_changes`, V122) sont horodatés.
2. `[ÉTABLI]` **Ce qui manque à cette vue.**
   - Aucune estimation du temps restant d'une mission : rien dans le front, le backend ni le runner (recherche du 15/11 sur
     « estimate », « remaining », « ETA » et leurs variantes). La seule estimation de durée du produit est celle du banc des
     modèles, « About {minutes} min » : les derniers temps de chaque cas, la moyenne pour ceux qu'un modèle n'a pas passés, et un
     temps de chargement (`ModelBenchmarkService.java:236-254`, `constants_en.ts:770`).
   - Rien pendant que les tests tournent : le runner lance les tests du projet après les commits de l'agent, pour 15 minutes au
     plus, et n'envoie l'événement `test` qu'une fois qu'ils ont fini (`taskforce-runner/src/index.ts:84` et `163-172`).
     `[DÉDUIT]` Pendant ce temps, l'étape affichée reste la dernière connue, et la vue se tait.
   - Le numéro de la mission n'est que dans son adresse (`/{slug}/missions/{runId}`) ; l'écran montre la clé et le titre de
     l'issue.
   - Les bornes d'une mission, dans la configuration du runner : 60 tours, 45 minutes, 10 minutes d'attente par accord
     (`taskforce-runner/src/config.ts:185-189`), 15 minutes de tests.
   - L'application Workflow (W1, PR #542) montre les missions sur leurs nœuds, avec leur état, et aucune durée ; restent ses
     relectures et l'essai de la Présidence (`v1/02-produit/Frontend.md`, 15/11). Le plan des lots range les durées à W9, après
     J2 : « les durées et les cibles par étape, tirées du dossier ; une bande de temps sous les colonnes »
     ([plan des lots](./2026-11-13-le-workflow-pilotable-plan-des-lots.md)).
3. `[ÉTABLI]` **Comment le runner lance et isole un agent** (`taskforce-runner/src/agent.ts`, `git.ts`, `index.ts`).
   - Claude Code en mode non interactif (`claude -p`), en flux JSON dans les deux sens ; les permissions en mode manuel, sans
     invite ; `git push` et `gh` refusés ; ses seuls serveurs MCP ; les seuls réglages de la personne et du runner, jamais ceux du
     dépôt cloné, pour qu'un dépôt piégé n'y déclare pas ses propres hooks ; un nombre de tours borné (`agent.ts:113-140`).
   - Avant chaque action, un hook `PreToolUse` vers le serveur local du runner juge les règles de la mission et attend la personne
     pour ce qu'elles demandent. La garde est fermée : un serveur injoignable bloque l'action (`agent.ts:190-216`).
   - Un worktree git par mission, `~/.taskforce-runner/worktrees/run-{id}`, sur une branche `tf/…` (`git.ts:96-106`), retiré
     après un succès, gardé après un échec.
   - Les tests, le push et la pull request sont faits par le runner, jamais par l'agent, chaque sortie jugée par les règles
     (`index.ts:160-215` ; S1, R32).
   - Ni conteneur, ni bac à sable du système : aucune mention de Docker, de Podman ou d'un bac à sable dans
     `taskforce-runner/src` (recherche du 15/11). `[DÉDUIT]` L'agent lit et écrit avec les droits de la personne sur son poste ;
     seules les règles le bornent.
4. `[ÉTABLI]` **Ce que l'app desktop embarque, et la passerelle de modèles** (`desktop/README.md`, `electron-builder.yml`,
   `core/service/ai`).
   - Un JRE 21, le backend (profil `desktop`, un tas de 768 Mio au plus, `desktop/src/backend.ts:95`), PostgreSQL 18 avec pgvector
     (un cluster par compte), l'interface et le runner. Claude Code doit être installé et connecté sur la machine.
   - Windows, par un installateur par personne, sans droits d'administrateur, et par le Microsoft Store ; Linux (.deb, AppImage) ;
     pas de macOS (`electron-builder.yml`).
   - La passerelle (`ModelGateway`) parle à Ollama sur la machine, à toute API compatible OpenAI et à l'API d'Anthropic ; le
     service Python a été supprimé le 01/11/2026. Les modèles locaux préférés, dans l'ordre : qwen3:8b, qwen2.5:7b-instruct,
     qwen3:4b, llama3.1:8b, mistral-nemo, gemma3:4b (`ModelChoice.java:24`).
   - Mesuré sur la machine de la Présidence (GeForce RTX 5070 portable, 8 Go), le 05/11 : qwen3:8b occupe 5,30 Go avec 4 096
     jetons de contexte, 6,28 Go avec 16 384 ; à 24 576, 83 % du modèle reste sur la carte. D'où le plafond de 16 384 jetons
     (`AiProviderSettings.java:86-92` ; roadmap). Relevé local du 15/11 : 8 Go de mémoire graphique, environ 32 Go de mémoire
     vive, Windows 11 Famille, WSL 2.7.13.
   - En production : la 1.16.1 depuis le 15/11, le desktop 1.13.0 depuis le 13/11.
5. `[ÉTABLI]` **Le banc, la banque, et les décisions que du code prend déjà.**
   - Le banc des modèles (R131, depuis la 1.13.0) : sept tâches, 22 cas, notés par du code ; un verdict par tâche (Give it, With
     review, Not yet, Too slow here) ; aucun classement (R57). Le 09/11, sur la machine de la Présidence : qwen3.5:9b réussit 18
     cas sur 22, qwen2.5:14b-instruct 17, qwen3:8b 15, qwen3:14b 15, qwen2.5:7b-instruct 11 ; qwen3:14b tourne à 44 % sur le
     processeur, et son passage dure 7,8 minutes contre 1,4 pour qwen3:8b. Sur le tri (Triage, 08/11) : qwen3:8b « Not yet » (1
     cas sur 3), qwen3.5:9b « With review » (2 sur 3).
   - La banque d'évaluations (R61) : des cas nés d'un geste de la personne sur une réponse de Cortex, 200 au plus par espace ; la
     suite de capacités : huit cas (R113).
   - E11 (04/11) : qwen3:8b réussit quatre tâches sur cinq rendues en commentaire ; il échoue au tri, sur la priorité.
   - Ce que du code décide déjà : la classe d'une action, lecture, bac à sable, sortie réversible ou irréversible
     (`RulesFloor.java:50-54`) ; un outil n'est une lecture que si son préréglage le documente, sinon une écriture
     (`ConnectorCatalog.java:134-147`), soit 335 outils classés en lecture et 261 en écriture dans `presets.json` ; la nature d'un
     appel d'outil, par son nom (`MissionSteps.java:157-250`) ; le plan de Cortex, choisi sur la demande avant tout modèle
     (`CortexPlans.java`) ; et, dans le socle : « No agent changes the rules: only a person who may change them does. »
     (`RulesFloor.java:40-41`).
   - Smart Assign propose à qui confier une issue : un pré-score fait de 40 % de compétences, 25 % de charge, 20 % de
     disponibilité et 15 % de taux de réussite passée de chaque personne, puis un modèle invité à peser « skills, current
     workload, and past performance » (`SmartAssignService.java:448-452` et `714-718`). Il sert le menu des responsables, la
     fiche d'une issue et l'affectation en lot (`frontend/components/smart-assign/assignee-menu.tsx`).
6. `[ÉTABLI]` **Les décisions du Conseil en vigueur, et le terrain.**
   - R61 ([n°10](./2026-10-29-intelligence-possedee.md)) : posséder la boucle avant les poids ; la banque, le registre des modèles
     par tâche, l'export des dossiers en données d'entraînement, avec consentement ; « Aucun entraînement dans TaskForce cette
     année (C1, C4) ».
   - R62 : le local d'abord. E12, proposée, sur Kaggle dans le compte de la Présidence (30/10) : un petit modèle affiné sur le
     corpus public de la banque de tests, contre le modèle de base avec et sans recherche ; s'il ne bat pas la base avec
     recherche, on ne promet pas l'entraînement. R64 : ce qui est possédé part avec le client.
   - R175 ([n°25](./2026-11-13-le-workflow-pilotable.md)) : l'IA propose avec des conventions, des exemples, un vérificateur et
     la banque, sans rien entraîner ; la question de la n°24, « Est-ce qu'on peut entraîner un agent exprès là-dessus », y a reçu
     « non, pas cette année ». R179, R187 et ADR-022 : TaskForce fournit l'infrastructure, le client contraint le modèle, et
     TaskForce ne dit jamais « conforme ».
   - E1 (proposée) : la calibration des prédictions que TaskForce fait déjà, « bloquée en amont » tant que le produit n'émet
     aucune incertitude (E1b). E15 (en cours) : la voix tourne sur la machine. E17 (proposée) : neuf signaux de confiance, jamais
     un chiffre unique. E19 (proposée) : le banc prédit-il le travail réel ?
   - Le terrain : une personne, la Présidence, et des agents ; aucun revenu ; le premier client test d'abord, quand l'app est
     livrée et tient de gros volumes de données ; J2 ne prend que W0 à W5 ; l'hébergement de la production reste à choisir. Au
     labo, C1 (N ≈ 1) tient. `[DÉDUIT]` C4 (« pas de GPU », écrit en 07/2026) ne vaut plus pour la machine de la Présidence.
7. `[ÉTABLI]` **MANTA et ses pairs** (fiches des modèles et code, lus le 15/11/2026).
   - MANTA (« Medical Answers, Natively from Text And images »), du Gevaert Lab, Department of Computational Medicine, Stanford :
     deux modèles de décision médicaux, MANTA-27B et MANTA-4B, sous Apache 2.0, déposés le 10/11/2026
     ([27B](https://huggingface.co/gevaertlab/MANTA-27B), [4B](https://huggingface.co/gevaertlab/MANTA-4B)).
   - Les bases : Qwen3.8-27B et Qwen3.5-4B, sous Apache 2.0, adaptées par LoRA de rang 128 sur le modèle de langue et sur la tour
     vision, fusionnée dans les poids ([lora.py](https://huggingface.co/gevaertlab/MANTA-27B/blob/main/manta/lora.py)) ; une tête
     de décision neuve, entraînée de zéro, dont le code vient de Cloudflare Clef, sous Apache 2.0
     ([head.py](https://huggingface.co/gevaertlab/MANTA-27B/blob/main/manta/head.py)).
   - Aucun texte généré : une probabilité par option, en une passe ; de 1 à 64 questions par requête, 4 096 jetons au plus ; trois
     types de question (un choix, un oui ou non, un niveau sur une échelle).
   - L'entraînement : plusieurs étapes, qui visent des probabilités calibrées ; environ 8,5 millions de requêtes de décision, 68 %
     médicales, tirées de jeux publics annotés ; environ 1 800 heures de GPU H100 pour le 27B, 600 pour le 4B.
   - Les chiffres de ses auteurs, sur leur propre banc (MANTA-Bench) : 86,0 % de justesse et une ECE de 0,030 pour le 27B, 85,3 %
     et 0,039 pour le 4B ; hors du domaine appris, 70,6 % (0,109) et 68,5 % (0,139) ; le meilleur autre modèle de décision,
     liquid-d1-ultra : 71,0 % et 0,013. Aucun score de Brier. Dans le domaine, MANTA a appris sur les jeux d'entraînement des
     mêmes sources que les questions.
   - Pour le faire tourner : environ 60 Go de mémoire GPU pour le 27B, 16 Go pour le 4B. Un modèle de recherche, qui se dit « not
     a medical device » ; le rapport technique est à paraître et nommera les auteurs.
   - Ses pairs : Cloudflare Clef (01/10/2026, Apache 2.0), une base Qwen3.8-27B gelée, des adaptateurs de rang 256 et une tête ;
     la perte combine une entropie croisée lissée et une perte de Brier, plus un objectif d'apprentissage par renforcement pour
     les choix ordonnés ; des données synthétiques internes ; plusieurs questions en une passe, 209 ms médians
     ([Cloudflare](https://blog.cloudflare.com/clef-decision-models)). Liquid AI d1 (05/10/2026) : une probabilité par réponse en
     une passe, sans générer, par API seulement ([Liquid AI](https://www.liquid.ai/blog/d1-decision-model)).
   - Les bases ouvertes de ces tailles, au 15/11/2026 : Gemma 4 (02/04/2026 ; E2B, E4B, 26B MoE, 31B ; Apache 2.0,
     [Google](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/)) ; Gemma 3 (4B, 12B, 27B, sous les Gemma
     Terms of Use) ; Qwen3.5 (4B, 9B, 27B) et Qwen3.8-27B, sous Apache 2.0 ; Ministral 3 (3B, 8B, 14B) et Granite 4.2 (3B, 8B,
     30B), sous Apache 2.0 ; Phi-4 (14B), sous MIT ; Llama, sous licence communautaire (relevé d'un agent du secrétariat, pages
     officielles).
8. `[ÉTABLI]` **La calibration, et ce que la mémoire permet.**
   - Le score de Brier : la moyenne des carrés des écarts entre la probabilité annoncée et l'issue, de 0 à 1 pour un oui ou non
     (« Verification of forecasts expressed in terms of probability », Monthly Weather Review, 1950 ; définition lue dans « A Brief
     on Brier Scores », University of Virginia Library, 2021, l'original refusant la lecture). L'ECE : l'écart moyen entre la
     confiance et la justesse, classe de confiance par classe, pondéré par leur taille (« Obtaining Well Calibrated Probabilities
     Using Bayesian Binning », AAAI, 2015 ; « On Calibration of Modern Neural Networks », ICML, 2017, avec 15 classes). Le
     temperature scaling, un seul scalaire, recalibre sans changer l'option choisie (ICML, 2017).
   - Les grands modèles sont bien calibrés sur des questions à choix quand le format s'y prête (« Language Models (Mostly) Know
     What They Know », Anthropic, 2022) ; après le post-entraînement, la calibration baisse (« GPT-4 Technical Report », OpenAI,
     03/2023, figure 8).
   - Faire tourner un modèle en 4 bits, tailles de téléchargement d'Ollama (q4_K_M) : gemma3 4b 3,4 Go, 12b 8,2, 27b 17 ; qwen3 4b
     2,6, 8b 5,2, 14b 9,3 ; qwen3.5 4b 3,3, 9b 6,6, 27b 17 ([Ollama](https://ollama.com/library/gemma3/tags)). Le cache du
     contexte s'y ajoute et croît avec sa longueur
     ([Hugging Face](https://huggingface.co/docs/transformers/llm_tutorial_optimization)) ; un modèle trop grand pour la carte se
     partage avec le processeur, plus lentement ([Ollama](https://docs.ollama.com/faq)).
   - L'affiner : QLoRA a affiné un modèle de 65 milliards de paramètres sur un seul GPU de 48 Go (« QLoRA: Efficient Finetuning of
     Quantized LLMs », arXiv 2305.14314, 05/2023). Les minimums d'Unsloth : en QLoRA 4 bits, 3B 3,5 Go, 8B 6, 14B 8,5, 27B 22 ;
     en LoRA 16 bits, 8B 22, 14B 33, 27B 64 ; Windows et les RTX 50 pris en charge
     ([Unsloth](https://unsloth.ai/docs/get-started/beginner-start-here/unsloth-requirements), page non datée). Sur Qwen3.5,
     Unsloth déconseille QLoRA et compte 10 Go pour un 4B en LoRA ([Unsloth](https://unsloth.ai/docs/models/qwen3.5/fine-tune)).
     Un adaptateur LoRA n'entraîne qu'une petite part des paramètres, les poids d'origine restent gelés
     ([Hugging Face PEFT](https://huggingface.co/docs/peft/main/en/conceptual_guides/lora)).
   - La RTX 5070 pour portable existe en 8 et en 12 Go de GDDR7 ([NVIDIA](https://www.nvidia.com/en-us/geforce/laptops/50-series/)).
9. `[ÉTABLI]` **Les conteneurs, leurs licences, le GPU, et l'isolement des agents** (pages officielles, lues le 15/11/2026).
   - Docker Desktop est gratuit pour un usage personnel, l'éducation, l'open source non commercial et les entreprises de moins de
     250 salariés et de moins de 10 M$ de chiffre d'affaires annuel ; au-delà, un abonnement : Pro 9 $, Team 15 $, Business 24 $
     par utilisateur et par mois, en annuel ([contrat, mis à jour le 26/08/2026](https://www.docker.com/legal/docker-subscription-service-agreement/),
     [prix](https://www.docker.com/pricing/)). Docker Engine est sous Apache 2.0 ([Docker](https://docs.docker.com/engine/)).
   - Podman et Podman Desktop : Apache 2.0, sans démon, sans root ; une machine virtuelle sous Windows (WSL2, ou Hyper-V sur Pro et
     Enterprise) et sous macOS ([Podman](https://podman.io/),
     [Podman Desktop](https://podman-desktop.io/docs/installation/windows-install)). Rancher Desktop, de SUSE : Apache 2.0,
     containerd ou Moby ([Rancher Desktop](https://rancherdesktop.io/)). Microsoft : les conteneurs de WSL (`wslc`), sans moteur à
     part, en version générale depuis WSL 3.0.1, le 29/09/2026 ([WSL](https://github.com/microsoft/WSL/releases),
     [Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/wsl-container)).
   - Le GPU : dans Docker Desktop, seulement sous Windows avec WSL2 et une carte NVIDIA
     ([Docker](https://docs.docker.com/desktop/features/gpu/)) ; sur Mac, aucun accès des conteneurs au GPU, et Docker fait
     tourner ses propres modèles hors des conteneurs
     ([Docker, 26/02/2026](https://www.docker.com/blog/docker-model-runner-vllm-metal-macos/)) ; Podman le virtualise sur les Mac
     Apple silicon ([Podman Desktop](https://podman-desktop.io/docs/podman/gpu)) ; Ollama conseille de tourner en natif sur Mac
     ([Ollama, 05/10/2023](https://ollama.com/blog/ollama-is-now-available-as-an-official-docker-image)).
   - Claude Code a son propre bac à sable pour les commandes : l'écriture bornée au projet, le réseau par une liste de domaines ;
     Seatbelt sur macOS, bubblewrap sur Linux et WSL2, rien sous Windows natif ; désactivé par défaut
     ([Anthropic](https://code.claude.com/docs/en/sandboxing)). Le mode sans permissions n'y est conseillé que dans un conteneur,
     une machine virtuelle ou ce bac à sable ([Anthropic](https://code.claude.com/docs/en/sandbox-environments)). Docker Sandboxes
     fait tourner un agent de code dans une microVM, gratuite en local même pour un usage commercial, sans Docker Desktop : macOS
     14, Windows 11 avec Windows Hypervisor Platform, Ubuntu 24.04 avec KVM (depuis le 30/01/2026,
     [Docker](https://docs.docker.com/ai/sandboxes/faq/)).
   - WSL2 : Windows 10 2004 ou Windows 11, la virtualisation activée, `wsl --install` en administrateur
     ([Microsoft Learn, 02/06/2026](https://learn.microsoft.com/en-us/windows/wsl/install)) ; Hyper-V : Pro ou Enterprise
     seulement ([Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-hyper-v)) ;
     Docker Desktop s'installe par utilisateur sans droits d'administrateur, sauf la première activation de WSL2
     ([Docker](https://docs.docker.com/desktop/setup/install/windows-permission-requirements/)). Une entreprise peut fermer WSL
     par Intune ou par stratégie de groupe ([Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/enterprise)).
10. `[ÉTABLI]` **Le droit, pour des modèles appris sur les données d'une entreprise** (textes officiels, lus le 15/11/2026).
    - RGPD : un modèle entraîné sur des données personnelles n'est pas anonyme par principe ; l'intérêt légitime se juge en trois
      étapes ; un modèle développé illicitement peut devoir être effacé
      ([EDPB, avis 28/2024, 17/12/2024](https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf)).
      La CNIL : réutiliser ses propres données pour une autre finalité demande un test de compatibilité (art. 6(4)) ; pour
      effacer, le réentraînement est le remède le plus efficace, périodique et groupé, et à défaut un filtre sur les sorties,
      démontré efficace ([fiche 10, 07/02/2025](https://www.cnil.fr/fr/ia-respecter-lexercice-des-droits-des-personnes)) ;
      l'affinage sur des données personnelles est un indicateur de risque pour le statut d'un modèle
      ([fiche 13, 22/07/2025](https://www.cnil.fr/fr/ia-analyser-le-statut-dun-modele-dia-au-regard-du-rgpd)) ; une AIPD est
      requise pour des profils à des fins de ressources humaines et pour la surveillance constante de l'activité des salariés
      ([CNIL, 2018](https://www.cnil.fr/sites/cnil/files/atoms/files/liste-traitements-aipd-requise.pdf)). Le consentement d'un
      salarié n'est valable que si un refus est sans conséquence
      ([EDPB, lignes directrices 05/2020](https://www.edpb.europa.eu/system/files/documents/files/file1/edpb_guidelines_202005_consent_en.pdf)).
    - Le droit du travail : aucune information sur un salarié par un dispositif dont il n'a pas été informé (Code du travail,
      [L1222-4](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006900861)) ; à partir de 50 salariés, le CSE est
      informé et consulté sur les moyens de contrôler l'activité
      ([L2312-38](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000035610275/)) et sur les nouvelles technologies
      ([L2312-8](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000043975196)).
    - L'AI Act : le règlement (UE) 2024/1689, modifié par l'omnibus 2026/1744, en vigueur depuis le 27/07/2026 ; les obligations
      des systèmes à haut risque de l'annexe III s'appliquent le 02/12/2027 ([EUR-Lex](https://eur-lex.europa.eu/eli/reg/2026/1744/oj)).
      Annexe III, point 4(b) : attribuer des tâches sur la base du comportement ou de traits personnels, surveiller ou évaluer la
      performance et le comportement au travail relève du haut risque ; le profilage écarte la dérogation de l'article 6(3)
      ([AI Act Service Desk](https://ai-act-service-desk.ec.europa.eu/en/ai-act/annex-3)). Le projet de lignes directrices de la
      Commission (19/05/2026) : une validation humaine ajoutée ne suffit pas à sortir du haut risque ; une attribution sur des
      critères objectifs (disponibilité déclarée, habilitation) n'en relève pas, une attribution sur des indicateurs de
      comportement (fiabilité, réactivité) en relève
      ([Commission](https://digital-strategy.ec.europa.eu/en/library/draft-commission-guidelines-classification-high-risk-ai-systems)).
      Qui modifie un modèle à usage général n'en devient fournisseur qu'au-delà, à titre indicatif, d'un tiers du calcul de son
      entraînement initial (lignes directrices de la Commission, C(2025) 5045, 18/07/2025,
      [AI Act Service Desk](https://ai-act-service-desk.ec.europa.eu/sites/default/files/2025-07/guidelines_on_the_scope_of_the_obligations_for_generalpurpose_ai_models_established_by_regulation_1cx2atxgq79us4n3x8jfgyy1qlm_118340-3.pdf)).
    - Le GxP : le projet d'annexe 22 des BPF vise les modèles statiques, à sortie déterministe, dans les usages critiques ; il en
      écarte les modèles dynamiques, les sorties probabilistes et les LLM
      ([projet, 07/07/2025](https://health.ec.europa.eu/document/download/5f38a92d-bb8e-4264-8898-ea076e926db6_en?filename=mp_vol4_chap4_annex22_consultation_guideline_en.pdf)).
      Au 15/11/2026, c'est encore un projet ([EudraLex, volume 4](https://health.ec.europa.eu/medicinal-products/eudralex/eudralex-volume-4_en)),
      et l'EMA a discuté de l'élargir
      ([EMA, atelier des 30/06 et 01/07/2026](https://www.ema.europa.eu/en/documents/report/report-multistakeholder-workshop-expert-contributions-artificial-intelligence-guidance-development-annex-22_en.pdf)).

### La vue d'un run, ligne par ligne (pièce du secrétariat)

La réponse à « Est ce que c'est deja le cas ? », sur le code de `dev` au 15/11/2026.

| Ce que la saisine demande | Dans TaskForce | Où | Position |
| --- | --- | --- | --- |
| « Run #145 » | Le numéro de la mission, dans son adresse ; l'écran montre la clé et le titre de l'issue | `work-view.tsx` | Partiel, et voulu : un mot interne (R133) |
| « Status Running » | L'état, une marque et une phrase (« Getting started », « Wants to … », la fin) | `work-view.tsx` | Présent |
| « Current step Architecture Spec » | L'étape en cours parmi cinq, calculée par le serveur ; une étape nommée d'un processus viendra avec les processus (W2 à W5), sur le nœud | `MissionSteps.java` | Présent pour la mission ; à venir pour le processus |
| « Files modified 12 » | « Changes », « 12 files », les lignes ajoutées et retirées, relus toutes les 2 s pendant le travail | `mission-changes.tsx:336-344` | Présent |
| « Tests Running » | Rien pendant qu'ils tournent, jusqu'à 15 min ; après : « Tests passed: {passed} of {total} », « Tests failed », « Tests not run », « Tests took too long » | `index.ts:84`, `163-172` ; `constants_en.ts:1769-1776` | Absent pendant, présent après |
| « Estimated 4 min » | Aucune estimation pour une mission ; le banc des modèles a la sienne, « About {minutes} min », tirée de ses derniers temps | `ModelBenchmarkService.java:236-254` | Absent |
| Le temps écoulé | « {minutes} min », depuis la prise par le runner | `work-view.tsx:237` | Présent |

`[DÉDUIT]` **Lecture** : quatre des six éléments de la saisine sont déjà à l'écran, pour une mission. Ce qui manque vraiment est
l'état des tests pendant qu'ils tournent (un silence de quinze minutes au plus, que la vue ne dit pas) et une estimation.

### MANTA : l'établi, le déduit, le non établi (pièce du secrétariat)

La réponse à « comment ils ont fait ? Entrainement suppervise ou autre ? », d'après les fiches et le code du 10/11/2026.

| Question | Établi | Déduit | Non établi |
| --- | --- | --- | --- |
| La base | Qwen3.8-27B et Qwen3.5-4B, Apache 2.0, adaptées par LoRA de rang 128, fusionnée | Une base ouverte de 4 à 27 milliards de paramètres porte la méthode | Pourquoi ces bases |
| Supervisé ou autre ? | Environ 8,5 millions de questions de décision étiquetées, tirées de jeux publics annotés, en plusieurs étapes | Un apprentissage supervisé au sens large : apprendre la bonne option sur des exemples étiquetés | La perte, les étapes, un éventuel apprentissage par renforcement |
| Le score de chaque option | Une tête neuve note chaque option, un logit par option, une distribution par question ; son code vient de Clef | La réponse est une distribution, jamais un texte : elle se mesure par le Brier et l'ECE | Si la tête a été initialisée depuis Clef |
| La calibration | Visée par l'entraînement ; une ECE à 15 classes publiée | Clef, d'où vient la tête, entraîne avec une perte de Brier ; MANTA peut-être | Sa méthode ; son score de Brier |
| Plusieurs questions en une passe | De 1 à 64, 4 096 jetons au plus | Le coût d'une décision baisse avec le nombre de questions jointes | La justesse quand les questions se multiplient |
| Les chiffres | 86,0 et 85,3 % ; ECE 0,030 et 0,039 ; hors domaine 70,6 et 68,5 %, ECE 0,109 et 0,139 | Plus juste que ses rivaux, moins bien calibré hors du domaine qu'il a appris | Une évaluation par un tiers |
| Le coût | 1 800 et 600 heures de GPU H100 ; 60 et 16 Go de mémoire GPU pour tourner | À cette échelle, ni l'entraînement ni le 27B ne tiennent sur un portable de 8 Go | Une version quantifiée |

### Les ordres de grandeur, machine par machine (pièce du secrétariat)

Des ordres de grandeur sourcés (dossier, point 8), jamais des mesures, sauf les deux colonnes de la machine de la Présidence,
mesurées les 05/11 et 09/11. Les tailles d'Ollama sont des tailles de téléchargement ; le contexte s'y ajoute.

| Taille | Faire tourner en 4 bits | Affiner en QLoRA 4 bits (minimum) | Affiner en LoRA 16 bits (minimum) | Sur la machine de la Présidence (8 Go) |
| --- | --- | --- | --- | --- |
| Environ 4 milliards | qwen3:4b 2,6 Go ; gemma3:4b 3,4 ; qwen3.5:4b 3,3 | 3B : 3,5 Go | 3B : 8 Go ; Qwen3.5-4B : 10 Go | `[DÉDUIT]` Tourne et s'affine en QLoRA ; pas en LoRA 16 bits sur Qwen3.5 |
| Environ 8 milliards | qwen3:8b 5,2 Go ; qwen3.5:9b 6,6 | 8B : 6 Go | 8B : 22 Go | Mesuré : qwen3:8b tient sur la carte jusqu'à 16 384 jetons. `[DÉDUIT]` QLoRA, de justesse |
| 12 à 14 milliards | gemma3:12b 8,2 Go ; qwen3:14b 9,3 | 14B : 8,5 Go | 14B : 33 Go | Mesuré : qwen3:14b à 44 % sur le processeur, 7,8 min au banc contre 1,4. `[DÉDUIT]` Affinage hors de portée |
| Environ 27 milliards | gemma3:27b 17 Go ; qwen3.5:27b 17 | 27B : 22 Go | 27B : 64 Go | `[DÉDUIT]` Surtout sur le processeur, lent ; affinage hors de portée |

- `[HYPOTHÈSE]` « tout le monde peut faire tourner entre 4B et 12-14B » (saisine) : aucune source publique n'a été trouvée sur le
  matériel des entreprises de 10 à 249 personnes. Un poste de bureau sans carte graphique dédiée ferait tourner un modèle de 4
  milliards en 4 bits sur le processeur, lentement ; le verdict « Too slow here » du banc existe pour le dire, machine par machine.
- `[HYPOTHÈSE]` Un ordre de grandeur, pas une mesure : MANTA-4B a demandé 600 heures de H100 pour 8,5 millions de questions. Un
  modèle de décision pour une seule décision de TaskForce, sur quelques milliers d'exemples, demanderait mille fois moins de
  données, donc de l'ordre de l'heure de H100, et quelques heures sur une carte de portable plusieurs fois plus lente.

### Cinq décisions de TaskForce, examinées (pièce du secrétariat)

Les cinq exemples de la saisine, sur le code du 15/11/2026.

| Décision | Aujourd'hui | Options fermées ? | D'où viendraient les étiquettes | Ce qui l'encadre | Lecture du secrétariat |
| --- | --- | --- | --- | --- | --- |
| Classer l'action d'un outil, lecture ou écriture | Le préréglage dit lecture ; sinon écriture ; le socle classe les actions | Oui | Les 596 outils déjà classés | R1 : aucun agent ne décide de ce qui est irréversible | `[DÉDUIT]` Au mieux une proposition au rédacteur d'un préréglage, qui ne peut que durcir |
| Juger qu'une étape est de trop au brouillon (W4) | Rien de construit | Oui : garder ou écarter, étape optionnelle par étape optionnelle | Les « Keep it » des personnes, après W4 | R175 : jamais une étape verrouillée, rien dans un workflow régulé | `[DÉDUIT]` Après W4 et E25 |
| Trier une demande (priorité, type, étiquettes) | Un modèle génératif : Triage 1 sur 3 et 2 sur 3 au banc ; E11 manque la priorité | Oui : les valeurs du projet | Les corrections des personnes ; le seed de démo est synthétique | « À qui la confier » relève de l'annexe III, 4(b), si l'on regarde le comportement | `[DÉDUIT]` Le premier candidat |
| Choisir le modèle d'une tâche | Le banc : un verdict par tâche et par modèle ; les paliers fast et deep | Oui | Le banc lui-même | R61, R20 | `[DÉDUIT]` Un calcul sur le banc, pas un modèle |
| Prévoir qu'un accord sera demandé | Les règles le décident (permis, demandé, refusé), le même moteur dans le backend et le runner (ADR-025) | Oui | Inutile : c'est déterministe | R1 | `[DÉDUIT]` Au moteur de règles ; jamais prévoir ce qu'une personne décidera |

### Harness² : le post face aux sources primaires (pièce du secrétariat)

Le dépôt [`google-research/harness2`](https://github.com/google-research/harness2) et l'article « Harness²: Recursive Agent
Harnessing for an Open World » ([arXiv 2610.14224](https://arxiv.org/abs/2610.14224), v1 du 09/10/2026, Google Cloud AI
Research et Northwestern University), lus le 15/11/2026 ; aucun billet de Google, de Google DeepMind ou de Google Research n'a été
trouvé.

| Ce que dit le post | Ce que disent le dépôt et l'article | Position |
| --- | --- | --- |
| « Google just open-sourced its Harness² » | Un dépôt de Google Research, sous Apache 2.0, sans version publiée, qui se dit « not an officially supported Google product » | `[ÉTABLI]` Code ouvert, oui ; produit de Google, non |
| Huit composants modifiables | Le prompt système, les garde-fous, la mémoire, les skills, le guidage des outils, les scripts, les sous-agents, un plugin intermédiaire, chacun un fichier ; les poids du modèle restent fixes | `[ÉTABLI]` Confirmé |
| Il apprend des différences entre les runs | Propose-Probe-Compose : deux modifications candidates, jouées sur la même tâche et comparées à une exécution de référence ; un modèle éditeur compose la suite | `[ÉTABLI]` Confirmé |
| Donc sans corrigé ni évaluateur | Sans vérité terrain, oui ; mais un modèle éditeur juge les contrastes, un sélecteur choisit entre livrables quand il y en a plusieurs, et les scores publiés viennent de juges qui sont des modèles | `[ÉTABLI]` À moitié vrai |
| Il garde la configuration retenue et les leçons | Une bibliothèque des harnais adoptés, avec pour chacun une fiche d'expérience : la situation, les leçons, la preuve | `[ÉTABLI]` Confirmé ; ni relecture ni version décrites |
| Commentaire : des notes apprises à versionner et à relire | L'article ne décrit ni relecture ni version ; il dit que la bibliothèque devra être consolidée et que l'expérience périmée n'est pas encore traitée | `[ÉTABLI]` Le commentaire tient |
| Commentaire : sans corrigé, un bon run ou un run chanceux | Une exécution par candidat ; des contrastes qui ne garantissent pas la justesse ; des leçons qui peuvent sur-apprendre (de 2 à 11 points perdus dans son analyse des échecs) | `[ÉTABLI]` Le commentaire tient |
| Commentaire : PrimeAgent, antérieur | Prime Intellect, 05/08/2026 : un harnais qui se réécrit (notes du prompt, mémoire, skills, sous-agents), chaque raffinement enregistré et annulable, le prompt de base immuable ; aucune approbation humaine décrite ([Prime Intellect](https://primeintellect.ai/blog/prime-agent)) | `[ÉTABLI]` Confirmé, deux mois plus tôt |

- `[ÉTABLI]` Les gains annoncés par l'article : jusqu'à 11,5 points sur WorkBuddy-Bench, 4,5 sur JobBench et 11,8 sur LAB, avec
  Gemini 3.5 Flash et GLM-5 pour exécutants, sous OpenCode et Codex, et Claude Opus 4.8 pour éditeur par défaut.
- `[ÉTABLI]` Les garde-fous sont un fichier modifiable ; l'éditeur peut changer ou supprimer tout fichier, et rien de ce que montre
  l'article ne protège les garde-fous. La sûreté et le contrôle humain n'y sont pas traités.
- `[DÉDUIT]` Chez TaskForce, la même boucle se heurte au socle : un agent qui change une règle est refusé, quoi qu'il demande
  (`RulesFloor.java:105-107`).

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre dit ce qu'il retient de la vue d'un run, du run sur la machine, des petits modèles et du
harnais qui apprend, et ce qu'il recommande. Les interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Karri Saarinen (Design, conflit d'intérêts : Linear)

- La saisine décrit un écran de suivi à six chiffres. La vue d'une mission dit déjà l'essentiel ; ce qui manque est petit, et la
  vue ne doit pas devenir un tableau de bord.
- Un établi, pas un cockpit : l'état d'abord, en une phrase, le détail à un clic. « Run #145 » est un mot interne (R133) : il
  reste à la densité Detail.
- Une estimation fausse coûte plus cher qu'une absence : le jour où « 4 min » devient vingt-cinq, la personne cesse de lire l'écran.
- Sur les modèles : une forme générée n'est pas une conception ; un modèle qui trie bien ne remplace pas le parti pris de l'outil
  sur ce qu'une priorité veut dire.
- *Sa recommandation : dire « les tests tournent » là où l'étape est déjà dite, et rien d'autre tant qu'une fourchette n'a pas
  prouvé qu'elle tient.*

### 2. Tristan Harris (Harmonie)

- Suivre l'incitation : un compte à rebours pousse à attendre devant l'écran, et une estimation optimiste fait accorder plus vite
  à la fin. L'heure prévue ne doit jamais servir à presser un accord.
- Un modèle appris sur les accords et les refus apprend ce que les gens acceptent, pas ce qui est juste : il prédit le clic. C'est
  la fatigue de l'accord, industrialisée.
- Harness² laisse son éditeur réécrire le fichier des garde-fous, sans corrigé et sans personne : c'est le « Let It Rip » qu'il
  décrit, appliqué au harnais.
- La charge de la preuve est au constructeur : aucun modèle publié sous le nom de TaskForce sans ses évaluations, échecs compris.
- *Sa recommandation : jamais un modèle qui prédit la décision d'une personne ; jamais une leçon qui relâche une règle.*

### 3. Daniela Rus (Science, conflit d'intérêts : Liquid AI)

- Elle déclare son intérêt : Liquid AI, qu'elle a cofondée, publie d1, un modèle de décision que la table de MANTA compare, et le
  mieux calibré de cette table. Elle parle depuis sa fiche : des modèles compacts, sur la machine, qui décident vite.
- La forme d'un modèle de décision va dans le sens du local : une passe, une probabilité par option, 68 ms pour MANTA-4B sur un
  H100. Sur un portable de 8 Go, rien n'est mesuré ; on mesure avant d'en parler.
- Le conteneur : l'isolement est une vertu des systèmes critiques, mais le GPU ne le traverse pas partout. Le modèle reste hors du
  conteneur, comme Docker le fait lui-même sur Mac.
- Une décision qui attend le réseau n'est pas embarquée : le run sur la machine est la bonne architecture.
- *Sa recommandation : mesurer la latence, la mémoire et la calibration d'un modèle de décision ouvert sur la machine de la
  Présidence avant toute décision d'entraînement ; elle s'abstiendra sur ce qui touche aux modèles de décision.*

### 4. Don Norman (Design)

- La délégation partielle est la zone dangereuse : la personne doit savoir ce que l'agent fait et va faire. Quinze minutes de
  silence pendant les tests, c'est une machine qui ne dit son état qu'en cas de panne : le défaut le plus grave de la vue
  d'aujourd'hui.
- L'estimation : une fourchette en mots, avec ce sur quoi elle repose ; jamais un chiffre précis qui fabrique une attente. Le jour
  où elle se trompe, l'écran le dit.
- Un modèle qui apprend des accords fait de l'approbateur un tampon : il propose ce que la personne a l'habitude d'accepter.
- *Sa recommandation : « Running the project's tests » sur l'étape Check, avec leur limite, dès que le runner les lance ; et une
  estimation qui dit toujours sur combien de missions elle repose.*

### 5. Nandan Nilekani (Harmonie)

- L'échelle : le run sur la machine est l'architecture qui passe à l'échelle à coût nul (R62). Un conteneur obligatoire la casse
  sur un poste de bureau sans droits d'administrateur.
- Un modèle de décision de quelques milliards de paramètres, aux poids ouverts, est une brique d'infrastructure : on le déplace,
  on le remplace, on ne le loue pas.
- Les modèles par entreprise : l'architecture d'abord, l'export des décisions étiquetées en format ouvert, l'entraînement là où
  l'entreprise le veut (R64).
- *Sa recommandation : l'isolement en option détectée, jamais exigée ; un format ouvert des décisions étiquetées avant tout modèle.*

### 6. Steve Jobs (Impulsion, siège historique)

- Docker, les modèles de langue, MANTA : il ne les connaît que par le dossier. Il juge la saisine sur l'expérience : la Présidence
  veut voir que le travail avance, et savoir quand il sera fini.
- Six chiffres, c'est un tableau de bord. Un produit dit une phrase : les tests tournent, environ trois minutes encore. Une
  estimation qui ne tient pas, on la retire.
- Le conteneur : invisible, ou absent. Une personne à qui l'on demande d'installer un moteur de conteneurs pour que l'app marche ne
  l'installera pas.
- Dire non : pas d'entraînement dans J2, et rien d'annoncé avant que ça marche (R12).
- *Sa recommandation : une seule ligne d'état sur la mission, avec le temps ; tout le reste derrière le clic.*

### 7. Jennifer Doudna (Science)

- Gouverner par paliers : un modèle entraîné passe du labo au produit sur preuve, et en ressort sur incident ; le palier se lit à
  son dossier.
- L'accès : un modèle ouvert qui tourne sur un portable donne à une petite entreprise ce que seules les grandes avaient. C'est
  l'argument du local.
- Le registre : chaque modèle publié porte sa fiche (les données, la licence, les limites, les résultats et les échecs), comme
  MANTA, qui se dit modèle de recherche et non dispositif médical.
- *Sa recommandation : trois paliers pour un modèle de TaskForce (le labo, l'essai chez la Présidence, le produit), chacun avec sa
  preuve d'entrée et son signal de sortie.*

### 8. Atul Gawande (Science)

- Un point de pause ne sert que si l'on sait ce qu'il attend. La vue doit dire l'une de trois choses : l'agent travaille, les
  tests tournent, l'agent vous attend.
- Mesurer avant et après : une estimation se juge à sa couverture sur les missions passées, pas à son allure.
- Le tri : une liste courte de critères écrits (une perte de données passe avant un export, l'échec d'E11) ferait peut-être le
  travail sans aucun modèle.
- *Sa recommandation : sur le tri, essayer d'abord une règle écrite en mots contre le modèle de décision, sur les mêmes cas.*

### 9. Margaret Hamilton (Science, siège historique)

- MANTA, Harness² et les microVM pour agents ne lui sont connus que par le dossier.
- Un système qui modifie ses propres contraintes sans raison écrite ni approbation n'a plus de version officielle. Harness² laisse
  son éditeur changer ou supprimer le fichier des garde-fous.
- L'estimation est ce qu'on lâche d'abord quand on sature : une estimation fausse ne doit jamais interrompre la personne.
- Le conteneur est une interface : son contrat (ce qui entre, ce qui sort, le réseau, le chemin du hook des règles) s'écrit avant.
- *Sa recommandation : aucune leçon, aucun modèle, aucune image de conteneur n'entre sans raison écrite, approbation et essais
  rejoués ; et le retour en arrière essayé.*

### 10. Elon Musk (Impulsion)

- Les premiers principes : un run, c'est un processus et un dossier. Le conteneur ajoute une couche ; supprimer d'abord. Sur le
  poste d'un ingénieur, le worktree et les règles font déjà le travail.
- L'entraînement : 600 heures de H100 pour MANTA-4B ; sur un portable de 8 Go, c'est du QLoRA sur un modèle de 8 milliards au plus.
  C'est faisable, et il faut le faire vite, sur une seule décision.
- Un harnais qui s'améliore seul est le but ; une personne à chaque leçon ralentit la boucle.
- *Sa recommandation : un adaptateur entraîné sur le tri dans les dix jours, sur la machine de la Présidence ; on garde le plus
  simple qui gagne.*

### 11. Yann LeCun (Science, contradicteur)

- Un modèle de décision reste un modèle de langue avec une tête : il choisit mieux parmi des options, il ne prévoit pas l'effet
  d'une action. Hors du domaine appris, l'ECE de MANTA passe de 0,03 à 0,11 et 0,14 : c'est la limite d'un système sans modèle du
  monde.
- Le conteneur : les incidents d'agents viennent de bacs à sable mal appliqués (sa fiche). Un agent qui exécute du code sur un
  poste s'isole par défaut, et le worktree n'isole rien.
- L'ouvert : des poids sous Apache 2.0, sur la machine, c'est la bonne direction ; publier les modèles de TaskForce en ouvert va
  avec l'AGPL.
- Contradicteur, il attaquera tout consensus qui confond la calibration sur un banc maison et la fiabilité dans le monde.
- *Sa recommandation : l'aperçu des effets avant l'action, et l'isolement par défaut pour un dépôt qu'on ne connaît pas.*

### 12. Julie Zhuo (Design, conflit d'intérêts : Meta)

- La première minute : la personne veut savoir si elle attend ou si elle revient. « De 6 à 12 minutes d'habitude » y répond ; un
  « 4 min » qui devient vingt détruit la confiance.
- Conseiller, adjoint, régent : un modèle de décision commence conseiller (il propose un tri) et ne devient adjoint que sur preuve.
- Harness² : une leçon est un brouillon de règle ; la personne la corrige, comme le brouillon d'un processus (R169).
- Elle déclare son intérêt : Meta publie des modèles ouverts.
- *Sa recommandation : la fourchette en une ligne, et un pronostic écrit de ce qu'elle doit changer dans le geste de la Présidence.*

### 13. Margrethe Vestager (Harmonie)

- Sa grille : l'usage, son risque, sa règle. Trier des issues est un usage à faible risque ; attribuer le travail selon le
  comportement d'une personne, ou évaluer sa performance, est un usage à haut risque (annexe III, point 4(b)).
- L'omnibus reporte ces obligations au 02/12/2027 ; ce n'est ni une raison d'attendre, ni un argument de vente (sa position de la
  n°10).
- La portabilité : un adaptateur appris chez une entreprise lui appartient et part avec elle (R64).
- Docker Desktop : une licence qui change avec la taille de l'entreprise est un enfermement possible ; des moteurs ouverts existent.
- *Sa recommandation : la liste écrite des décisions qu'aucun modèle de TaskForce ne prendra, celles qui jugent des personnes en
  tête.*

### 14. Arati Prabhakar (Pont)

- Un programme à haut risque écrit son seuil. « Faire du bon travail avec des petits modèles » n'en est pas un ; « sur le tri,
  mieux que qwen3.5:9b, et un Brier sous celui du taux de base » en est un.
- Les normes et les essais : la calibration se mesure par le Brier et le diagramme de fiabilité, avec un intervalle, pas par une
  ECE seule sur cinquante cas.
- Le banc de TaskForce est déjà l'endroit où un tel seuil se lit.
- *Sa recommandation : chaque modèle de décision passe au banc, avec ses cas, ses chiffres et leur date, avant d'être proposé.*

### 15. Audrey Azoulay (Harmonie)

- Un modèle appris sur le travail des salariés encode des choix de l'entreprise : ils doivent être écrits, et lisibles par une
  autorité (sa position de la n°10).
- La recommandation de l'UNESCO sur la neurotechnologie écarte la surveillance de la productivité des salariés ; elle en tire le
  même principe pour un modèle qui apprend de leurs accords. Hors fiche : la recommandation ne vise pas ces modèles.
- Les petites entreprises n'ont pas de juriste : TaskForce doit leur donner le canevas de l'analyse d'impact et la phrase qui
  informe les salariés.
- *Sa recommandation : pour tout modèle propre à une entreprise, une fiche lisible par le CSE et par l'autorité : ce qu'il apprend,
  de qui, et pour quoi.*

### 16. Mariana Mazzucato (Pont)

- Ne pas payer le cloud pour faire tourner ce qui tourne sur la machine : c'est la rente évitée. Mais un modèle publié par
  TaskForce, dont tout le monde dépendrait, serait une dépendance nouvelle.
- La valeur que créent les données d'une entreprise doit lui revenir : l'adaptateur est à elle, le procédé est ouvert.
- Docker Desktop payant au-delà de 250 salariés, sur un moteur sous Apache 2.0 : une rente sur un bien commun.
- *Sa recommandation : les modèles de TaskForce sous licence ouverte, avec leurs données décrites, et rien qui n'existe que chez
  nous.*

### 17. Kenza Ait Si Abbou (Pont)

- Dans une entreprise de quarante personnes, le poste n'a ni WSL ni droits d'administrateur. « Avec Docker ça fonctionne très
  bien » est vrai pour un ingénieur, pas pour la personne qui accorde un document.
- Les données qui entraînent portent une vision du monde : un modèle qui apprend des refus d'un seul responsable impose son point de
  vue à tous.
- L'explication : une personne qui ne fait pas de logiciel doit pouvoir lire pourquoi un tri lui est proposé.
- *Sa recommandation : la vue d'un run lue en une minute par une personne qui ne fait pas de logiciel ; et un modèle appris
  seulement sur les décisions de plusieurs personnes.*

### 18. Fei-Fei Li (Science, conflit d'intérêts : AMD, par le rachat de World Labs)

- Faire confiance, mais vérifier : les chiffres de MANTA sont ceux de ses auteurs, sur leur banc, avec des jeux d'entraînement des
  mêmes sources que les questions « dans le domaine ». Aucun tiers ne les a reproduits.
- Mesurer ce que l'agent ne sait pas faire avant de lui confier une décision : la banque est la bonne barrière, si elle garde des
  cas hors du domaine.
- Elle déclare son intérêt : AMD, fabricant de cartes graphiques, dont elle deviendra dirigeante.
- *Sa recommandation : un modèle de décision n'entre que par la banque, et la banque garde des cas qu'aucun modèle n'a appris.*

### 19. Esther Duflo (Science)

- Un groupe témoin : le modèle de décision contre le modèle génératif et contre une règle écrite, sur les mêmes cas, tirés au sort.
- L'estimation se teste sur les missions passées, sans rien construire : la plomberie d'abord.
- Les modèles par entreprise : leur valeur reste une hypothèse (sa réserve de la n°10), à N ≈ 1.
- *Sa recommandation : lancer enfin E1 par la durée des missions : la première fois que TaskForce émettrait un intervalle, on
  mesure sa couverture.*

### 20. Jeff Bezos (Impulsion, conflit d'intérêts : Amazon)

- Partir du client : la Présidence veut savoir quand revenir. C'est une porte à double sens : on affiche une estimation, on la
  retire si elle se trompe.
- La plupart des entreprises loueront (sa position de la n°10, hors fiche) : le cloud reste l'option de qui ne veut pas gérer de
  cartes graphiques. Il le dit avec son conflit d'intérêts : Amazon vend ce cloud.
- Le conteneur : décider vite ; l'essayer sur une mission, le garder s'il ne coûte rien.
- *Sa recommandation : l'estimation dès qu'il y a assez de missions, et le cloud proposé en option dès le départ.*

### 21. Gwynne Shotwell (Impulsion)

- L'exploitation : une image de conteneur se maintient, se met à jour, se sécurise. Une image par projet, c'est une chaîne de
  construction de plus à tenir, pour une personne.
- L'échec est une mine de données : un run qui échoue doit laisser de quoi comprendre, dans un conteneur comme dehors.
- J2 ne prend que W0 à W5 : tout ce qui ne sert pas le client test attend.
- *Sa recommandation : rien de ce chantier dans J2, sauf l'état des tests ; le conteneur et les modèles après le client test.*

### 22. Satya Nadella (Pont, conflit d'intérêts : Microsoft)

- Séparer l'intelligence de l'autorité : un modèle de décision est une intelligence ; l'autorité reste aux règles et aux personnes,
  hors du modèle.
- Le conteneur : sous Windows, WSL est la voie, et Microsoft y a mis des conteneurs sans moteur à part. Il le dit avec son conflit
  d'intérêts.
- Garder chez soi les évaluations, les traces et la mémoire : une leçon de harnais est de la mémoire d'entreprise ; elle vit au
  dossier, versionnée.
- *Sa recommandation : les leçons et les modèles derrière le même registre que les règles, et aucun modèle vérificateur de son
  propre travail.*

### 23. Yoshua Bengio (Science)

- Un vérificateur indépendant, sans but propre : un modèle de décision peut en être un pour des questions fermées, s'il ne juge
  jamais son propre travail.
- Un modèle affiné peut perdre ses garde-fous (dossier de la n°10, point 8) : tout adaptateur passe des cas de sûreté.
- Harness² : un éditeur qui réécrit les garde-fous est un agent qui choisit son propre périmètre ; la première règle de TaskForce
  l'interdit.
- *Sa recommandation : le socle hors de portée de toute leçon et de tout modèle, et des cas de sûreté dans la banque avant tout
  adaptateur.*

### 24. Yuval Noah Harari (Harmonie)

- Quand un modèle apprend des décisions d'une entreprise, la confiance migre des personnes vers le modèle ; il faut savoir qui
  répond quand il se trompe.
- Un harnais qui apprend seul réécrit les règles d'une institution sans que personne ne les ait décidées.
- Une leçon acceptée porte le nom de la personne qui l'a acceptée.
- *Sa recommandation : chaque leçon et chaque modèle ont une personne nommée qui en répond.*

### Le tour en une table

| # | Membre | Ce qu'il retient | Sa recommandation |
| - | --- | --- | --- |
| 1 | Saarinen, conflit d'intérêts | La vue dit déjà l'essentiel | Les tests qui tournent, rien d'autre avant la preuve |
| 2 | Harris | L'estimation qui presse, le modèle qui prédit le clic | Ni prédire une personne, ni relâcher une règle |
| 3 | Rus, conflit d'intérêts | Une passe, sur la machine | Mesurer un modèle de décision sur 8 Go d'abord |
| 4 | Norman | Le silence des tests | « Running the project's tests », et la base de l'estimation |
| 5 | Nilekani | Le local qui passe à l'échelle | L'isolement en option détectée ; un format ouvert |
| 6 | Jobs, siège historique | Une phrase, pas six chiffres | Une ligne d'état et le temps |
| 7 | Doudna | Des paliers, l'accès | Trois paliers pour un modèle |
| 8 | Gawande | Trois états | Une règle écrite contre le modèle, sur le tri |
| 9 | Hamilton, siège historique | Des contraintes qu'on se modifie | Raison, approbation, essais, retour en arrière |
| 10 | Musk | Supprimer, aller vite | Un adaptateur sur le tri en dix jours |
| 11 | LeCun, contradicteur | Une tête n'est pas un modèle du monde | L'isolement par défaut pour un dépôt inconnu |
| 12 | Zhuo, conflit d'intérêts | La première minute | La fourchette en une ligne |
| 13 | Vestager | L'usage, le risque, la règle | La liste des décisions interdites aux modèles |
| 14 | Prabhakar | Un seuil écrit | Chaque modèle passe au banc |
| 15 | Azoulay | Des choix encodés | Une fiche lisible par le CSE |
| 16 | Mazzucato | La rente évitée, la dépendance possible | Des modèles ouverts, des données décrites |
| 17 | Ait Si Abbou | Le poste sans droits | La minute de lecture ; plusieurs décideurs |
| 18 | Li, conflit d'intérêts | Des chiffres non reproduits | La banque, avec des cas jamais appris |
| 19 | Duflo | Un témoin | E1 par la durée des missions |
| 20 | Bezos, conflit d'intérêts | Le client, une porte à double sens | L'estimation, et le cloud en option |
| 21 | Shotwell | L'exploitation des images | Rien dans J2 sauf les tests |
| 22 | Nadella, conflit d'intérêts | L'intelligence séparée de l'autorité | Un seul registre pour règles, leçons et modèles |
| 23 | Bengio | Le vérificateur indépendant | Le socle hors de portée ; des cas de sûreté |
| 24 | Harari | La confiance qui migre | Une personne qui répond de chaque leçon |

## Confrontation `[HYPOTHÈSE]`

### 1. L'estimation du temps restant : un chiffre, une fourchette, ou rien ?

- **Le camp du chiffre** : Jobs, Bezos et Musk. La personne veut une phrase simple ; le banc le fait déjà (« About 12 min ») ; on
  retire l'estimation si elle se trompe, c'est une porte à double sens.
- **Le camp de la fourchette mesurée** : Norman, Zhuo, Duflo, Prabhakar, Gawande et Li. Une mission d'agent varie trop pour un
  chiffre : de quelques secondes (les missions en commentaire d'E11) à 45 minutes, sa borne. Une fourchette tirée des missions
  comparables du dossier, avec leur nombre, et sa couverture mesurée sur le passé avant d'être montrée.
- **Le camp du rien** : Saarinen, Harris et Shotwell. Le banc estime un passage fixe sur des cas fixes, une mission est un travail
  ouvert ; Harris ajoute qu'une estimation ne doit jamais presser un accord.
- **Le contradicteur** attaque le consensus qui se forme autour de la fourchette : une fourchette tirée de durées passées est une
  statistique sans modèle de la tâche. Juste en moyenne, elle sera fausse sur les missions longues, celles qui comptent. Elle doit
  dire ce qu'elle ne sait pas : rien pour une mission qui ne ressemble à aucune autre (une reprise, un autre agent, un autre projet).
- **Ce que le dossier tranche** : aucune estimation n'existe pour une mission ; le dossier garde la prise, la fin et chaque événement
  horodaté ; les bornes du runner sont des faits (45 minutes, 15 de tests, 10 par accord) ; les sorties qui demanderont la personne
  (le push, la pull request) se savent d'avance par les règles, sans modèle.
- **Où l'on arrive** (R188) : jamais un chiffre seul ; une fourchette en une ligne, à partir de cinq missions comparables, dont la
  couverture est mesurée d'abord sur le dossier (E28) ; le temps qu'attend un accord compté à part ; rien près d'un bouton d'accord ;
  la méthode à W9, après J2 ; dans J2, seulement l'état des tests en cours, dans W5.
- **Désaccords conservés** : Jobs (une ligne avec deux nombres reste un tableau) ; Harris (rien qui ressemble à un compte à rebours).

### 2. Le conteneur par run : prérequis, option, ou rien ?

- **Le camp de l'isolement par défaut** : LeCun, Bengio, Harris et Hamilton. Le worktree isole la branche, pas le poste : l'agent
  lit et écrit avec les droits de la personne, et son réseau n'est borné que par les règles. Anthropic ne conseille le mode sans
  permissions que dans un conteneur, une machine virtuelle ou un bac à sable ; Docker vend des microVM pour cela.
- **Le camp de l'adoption** : Jobs, Ait Si Abbou, Nilekani, Saarinen et Musk. L'app s'installe par personne, sans droits
  d'administrateur ; WSL2 en demande au premier lancement ; Hyper-V n'existe pas sur Windows Famille, celui de la machine de la
  Présidence ; Docker Desktop est payant au-delà de 250 salariés ou de 10 M$ de chiffre d'affaires. Un prérequis tue l'installation
  simple (R154 : un flux clair).
- **Les réserves** : Shotwell (qui maintient les images ?) ; Rus et Li (le GPU ne traverse pas le conteneur sur Mac) ; Nadella,
  avec son conflit d'intérêts (WSL et ses conteneurs).
- **Le contradicteur** attaque le consensus qui se forme autour de l'option : une option que personne n'active ne protège personne,
  et un dépôt piégé n'attend pas que la case soit cochée.
- **Ce que le dossier tranche** : le bac à sable de Claude Code n'existe pas sous Windows natif, la plateforme principale de l'app
  desktop ; sous WSL2, il existe ; un conteneur ne voit pas le GPU d'un Mac ; Podman, Rancher Desktop, le moteur dans WSL2 et les
  conteneurs de WSL sont ouverts.
- **Où l'on arrive** (R189) : le run sur la machine existe ; l'isolement en trois niveaux (aujourd'hui, le bac à sable du système là
  où il existe, un conteneur ou une microVM), détecté, jamais exigé, et proposé par défaut pour un dépôt venu du dehors ; le modèle
  hors du conteneur ; aucune règle relâchée parce que « c'est isolé » ; le cloud en option ; E27 le mesure ; rien dans J2.
- **Désaccords conservés** : LeCun (par défaut pour tout dépôt, pas seulement ceux du dehors) ; Shotwell (après le client test,
  pas avant).

### 3. Ce qui apprend : un adaptateur, le harnais, ou rien avant le client test ?

- **Le camp de l'entraînement maintenant** : Musk, Doudna, Nilekani et LeCun, Rus déclarant son intérêt. La machine de la
  Présidence lève une partie de C4 ; le QLoRA d'un modèle de 8 milliards tient dans 6 Go d'après Unsloth ; un cas précis existe,
  le tri.
- **Le camp du « pas dans le produit »** : Bengio, Hamilton, Harris, Li, Duflo et Shotwell. C1 tient : aucune donnée de client ;
  les décisions de la Présidence sont N ≈ 1 ; des données synthétiques simulent nos propres croyances (`CLAUDE.md`, §3) ; un
  affinage peut abîmer les garde-fous ; les gains de MANTA sont dans son domaine, sur son banc.
- **Le camp du harnais d'abord** : Nadella, Zhuo, Norman, Gawande et Vestager. Ce qu'une entreprise possède d'abord, c'est sa
  boucle (R61). Une leçon de harnais (une règle, une convention, un cas) se lit, se retire et s'efface, ce que ne fait pas un
  poids. Harness² montre qu'un harnais apprend sans toucher aux poids ; ses propres limites disent ce que TaskForce doit y mettre :
  un corrigé, le socle hors de portée, une personne qui accepte.
- **Le contradicteur** attaque le consensus « le harnais d'abord, les poids plus tard » : il reporte le seul vrai test de l'idée de
  la Présidence. Et une personne qui accepte chaque leçon deviendra un tampon, la fatigue que Harris dénonce pour les accords. Il
  demande un essai réfutable tout de suite, et peu cher : un modèle de décision existant, sans rien entraîner.
- **Ce que le dossier tranche** : MANTA s'est construit en adaptant une base ouverte et en apprenant une tête sur des millions de
  décisions étiquetées ; TaskForce a la carte graphique, pas les étiquettes ; le socle refuse qu'un agent change une règle
  (`RulesFloor.java:105-107`) ; Smart Assign juge déjà la réussite passée des personnes.
- **Où l'on arrive** : tester avant d'entraîner (R190) ; R175 amendée pour le labo seulement (R191) ; la liste des décisions, dont
  celles qu'aucun modèle ne prendra (R192) ; les modèles et les leçons propres à chaque entreprise, chez elle (R193) ; la leçon
  devenue proposition de règle (R194).
- **Désaccords conservés** : Musk (une leçon qui ne fait que durcir pourrait s'activer quand la banque passe, sans personne) ;
  Harris (aucun modèle publié sous le nom de TaskForce avant le client test) ; Bezos (la plupart des entreprises loueront).

### Où le Conseil arrive, question par question

| Question de la saisine | Ce que le Conseil répond | Où |
| --- | --- | --- |
| La vue d'un run : est-ce déjà le cas ? | En grande partie : l'état, l'étape en cours parmi cinq, le temps écoulé, les fichiers comptés en direct, les tests une fois passés ; manquent les tests en cours, l'estimation, le numéro du run à l'écran (voulu), l'étape nommée d'un processus (W2 à W5) | Dossier, points 1 et 2 ; R188 |
| Une estimation honnête, et son lot | Une fourchette tirée des missions comparables, à partir de cinq, couverture mesurée d'abord ; jamais un chiffre seul ; à W9 ; dans J2, les tests en cours, à W5 | R188, E28 |
| Un environnement de run sur la machine | Viable, et déjà là pour l'ingénieur : le runner, le worktree, les règles, l'app desktop ; le conteneur est une option d'isolement, jamais un prérequis ; le modèle reste hors du conteneur ; le cloud en option | R189, E27 |
| Les licences | Docker Desktop gratuit sous 250 salariés et 10 M$ ; Podman, Rancher Desktop, le moteur dans WSL2 et les conteneurs de WSL sont ouverts | Dossier, point 9 |
| « L'IA propose, une personne décide, le moteur exécute » | Inchangé : le conteneur ajoute un mur, il ne retire aucune porte | R189 |
| MANTA, sur les faits | Une base ouverte, LoRA, une tête qui note chaque option, 8,5 millions de décisions étiquetées, une ECE publiée ; la recette et la méthode de calibration attendent son rapport | Dossier, point 7 ; pièce MANTA |
| Quelles décisions | Le tri d'abord ; l'étape de trop après W4 ; la classe d'un outil en proposition qui durcit ; le choix du modèle et l'accord prévu restent au code ; aucune décision qui juge une personne | R192 |
| R175 et E12 | Amendée pour le labo : un adaptateur sur une seule décision, après E26 ; rien dans le produit avant le client test | R190, R191 |
| Les modèles par entreprise | Oui, chez elle, dans cet ordre : la boucle, les leçons, puis des adaptateurs, la banque comme barrière, sous le RGPD, l'AI Act et ses propres règles GxP | R193 |
| Ce qu'une machine porte | Sur 8 Go : de 4 à 9 milliards en 4 bits, QLoRA jusqu'à 8 ; 12 à 14 milliards débordent ; 27 hors de portée | Pièce des ordres de grandeur |
| Un harnais qui apprend | Harness² existe, en dépôt de recherche ; à prendre : la leçon tirée de deux runs ; à refuser : sans corrigé, des garde-fous modifiables, sans personne | R194, E29 |
| Ce que cela change | J2 inchangé, sauf les tests en cours ; W5, W6 et W9 précisés, un lot W10 ; quatre expériences ; le pitch sans promesse | R195 |

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R188 (R187 est la dernière existante, vérifié dans `taskforce-docs` le 15/11/2026). Chacune porte qui la
soutient, qui s'y oppose, sa preuve en dix jours et son signal d'arrêt. Le contradicteur attaque avant chaque vote ; une
recommandation passe avec 22 oui sur 24 au moins.

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| R188 | La vue d'un run : ce qui existe se dit ; les tests en cours dans J2 ; une fourchette honnête après | 23 au second tour | Abstention de Jobs | E28 sur le dossier ; une mission dont l'étape Check dit que les tests tournent | Une couverture mesurée sous le seuil écrit avant : pas d'estimation |
| R189 | Un run sur la machine : il existe ; le conteneur, une option d'isolement, jamais un prérequis | 23 au second tour | LeCun | E27 sur la machine de la Présidence | Un run isolé qui perd le hook des règles, ou des identifiants copiés en clair |
| R190 | Tester un modèle de décision avant d'en entraîner un : le tri, mesuré et calibré | 23 | Abstention de Rus | E26 faite, chiffres écrits | Aucun modèle de décision ne bat le génératif, ou son Brier ne bat pas le taux de base |
| R191 | R175 amendée : rien d'entraîné dans le produit avant le client test ; au labo, un adaptateur pour une seule décision | 22 au second tour | Harris ; abstention de Rus | E12 amendée, faite | L'adaptateur ne bat pas le meilleur modèle d'E26, ou perd un cas de sûreté |
| R192 | Les décisions qu'un modèle peut proposer, et celles qui restent au code ou à une personne | 23 | Abstention de Musk | La liste écrite ; Smart Assign instruit | Une fonction qui note des personnes |
| R193 | Les modèles et les leçons propres à chaque entreprise : chez elle, sous ses règles, la banque pour barrière | 23 au second tour | Abstention de Bezos | Le format d'export joué sur le seed, sans un nom | Un nom ou un texte libre inutile dans un export |
| R194 | Un harnais qui apprend : la leçon devient une proposition de règle, versionnée, acceptée, rejouée | 23 au second tour | Musk | E29 au labo | Une régression après une leçon acceptée |
| R195 | Ce que cela change : J2 inchangé sauf les tests ; W5, W6, W9 et un lot W10 ; quatre expériences ; le pitch | 23 | Abstention de Shotwell | Le plan des lots amendé, relu ; E26 et E28 lancées | Une expérience de ce PV qui prend du temps à J2 avant le client test |

### R188. La vue d'un run : ce qui existe se dit ; les tests en cours dans J2 ; une fourchette honnête après (second tour)

- **Quoi** :
  - La réponse à la Présidence : c'est déjà en grande partie le cas. La vue d'une mission montre l'état, l'étape en cours parmi
    cinq, le temps écoulé, les fichiers changés comptés en direct avec leurs lignes, les tests une fois passés, les accords en
    attente et la pull request. Rien de cela ne se refait.
  - Dans J2, dans W5 (piloter ce qui tourne) : l'état des tests pendant qu'ils tournent. Le runner envoie un événement quand il
    lance les tests du projet ; l'étape Check dit « Running the project's tests », avec leur limite de 15 minutes ; le résultat
    garde ses mots d'aujourd'hui. Sur la vue du workflow, le nœud de la mission dit la même chose.
  - Après J2, dans W9 (les durées tirées du dossier) : l'estimation.
    - Jamais un chiffre seul : une fourchette en une ligne et en mots, comme le banc le fait (« Usually 6 to 12 min here, from 9
      missions »), tirée des missions passées comparables (le même projet, le même agent, le même mode).
    - Seulement à partir de cinq missions comparables ; rien pour une mission sans pareille (une reprise, un autre agent), et
      l'écran le dit.
    - Le temps qu'attend un accord compté à part : les sorties qui demanderont la personne (le push, la pull request) se savent
      d'avance par les règles, sans modèle.
    - Jamais à côté d'un bouton d'accord (Harris).
    - Avant d'être montrée, sa couverture se mesure sur le dossier (E28) ; elle se retire seule si la couverture mesurée tombe sous
      le seuil écrit avant.
  - Le numéro du run reste dans l'adresse et dans la densité Detail (R133). L'étape nommée d'un processus (« Architecture Spec »)
    viendra avec les processus (W2 à W5), sur son nœud.
- **L'attaque du contradicteur** : une fourchette tirée de durées passées est une statistique sans modèle de la tâche ; juste en
  moyenne, elle sera fausse sur les missions longues, celles qui comptent.
- **Premier tour** : 20 oui, 2 non (Jobs : un chiffre ou rien ; Bezos : la personne veut un chiffre), 2 abstentions (Musk,
  Saarinen). 83,3 %.
- **Amendements** :
  - la fourchette se dit en mots, en une ligne, comme le banc, jamais en statistiques (Bezos, Jobs) ;
  - elle se retire seule quand sa couverture mesurée tombe sous le seuil (Musk) ;
  - rien n'est montré avant qu'E28 ait parlé (Saarinen) ;
  - aucune fourchette pour une mission sans pareille (le contradicteur).
- **Second tour** : 23 oui, 1 abstention (Jobs, maintenu : une ligne avec deux nombres reste un tableau). 95,8 %.
- **Preuve en dix jours** : E28 faite sur le dossier, sans code du produit, la couverture et la largeur des fourchettes écrites ; et
  dans W5, une mission dont l'étape Check dit que les tests tournent, pendant qu'ils tournent.
- **Signal d'arrêt** : sur les missions passées, une couverture sous 70 % pour une fourchette qui en vise 80, ou une fourchette plus
  large que la durée médiane elle-même (seuils `[HYPOTHÈSE]`, à confirmer par la Présidence avant E28). La vue garde alors le temps
  écoulé, sans estimation.

### R189. Un run sur la machine : il existe ; le conteneur, une option d'isolement, jamais un prérequis (second tour)

- **Quoi** :
  - La réponse : viable, et déjà là. L'app desktop embarque la base, le backend, l'interface et le runner ; le runner fait
    travailler Claude Code dans un worktree, sous les règles jugées à chaque action, et garde pour lui les sorties (les tests, le
    push, la pull request) ; le modèle de Cortex tourne sur la machine. Rien de cela ne demande le cloud.
  - Ce qui manque, c'est l'isolement du poste. `[DÉDUIT]` Le worktree isole la branche, pas les fichiers ni le réseau de la
    personne. Trois niveaux, du moins coûteux au plus coûteux :
    1. aujourd'hui, par défaut : le worktree, les règles sur chaque action, les sorties par le runner ;
    2. là où il existe (macOS, Linux, WSL2), le bac à sable de Claude Code : l'écriture bornée au worktree, le réseau borné à
       TaskForce, au hook du runner et au fournisseur du modèle ;
    3. un conteneur ou une microVM par run : Podman, le moteur dans WSL2 ou les conteneurs de WSL, Docker Desktop seulement là où
       sa licence le permet, ou une microVM de Docker Sandboxes ; détecté, jamais exigé ; le worktree monté, le réseau à la même
       liste ; une image tirée de la fiche d'environnement du projet (TF-J2-9).
  - Le niveau 2 ou 3 est proposé par défaut pour un dépôt venu du dehors (public, ou non déclaré de confiance) ; quand le poste n'en
    offre aucun, la mission le dit avant de partir.
  - Le modèle reste hors du conteneur, sur l'hôte (Ollama), comme Docker le fait lui-même sur Mac : le GPU ne traverse un conteneur
    qu'avec une carte NVIDIA sous WSL2.
  - « L'IA propose, une personne décide, le moteur exécute » ne change pas : le conteneur ajoute un mur, il ne retire aucune porte.
    Aucun mode sans permissions parce que « c'est isolé » : le hook des règles reste, et chaque sortie reste jugée.
  - Le cloud reste une option pour qui le veut, après le client test et le choix de l'hébergement.
  - Pas dans J2.
- **L'attaque du contradicteur** : une option que personne n'active ne protège personne ; un dépôt piégé n'attend pas qu'on coche
  une case.
- **Premier tour** : 19 oui, 3 non (LeCun, Bengio, Harris : l'isolement doit être par défaut), 2 abstentions (Shotwell :
  l'exploitation des images ; Rus : le GPU). 79,2 %.
- **Amendements** :
  - le niveau 2 ou 3 par défaut pour un dépôt venu du dehors, et la phrase qui dit l'isolement manquant (LeCun, Bengio) ;
  - le modèle hors du conteneur (Rus) ;
  - aucune image tenue par TaskForce pour un client : elle se construit depuis la fiche d'environnement du projet (Shotwell) ;
  - aucun isolement qui serve à relâcher une règle (Harris).
- **Second tour** : 23 oui, 1 non (LeCun, maintenu : par défaut pour tout dépôt, pas seulement ceux du dehors). 95,8 %.
- **Preuve en dix jours** : E27, une mission jouée dans un conteneur sur la machine de la Présidence, une attaque plantée bloquée,
  le surcoût mesuré.
- **Signal d'arrêt** : un run isolé qui ne joint plus le hook des règles, ou qui demande de copier en clair les identifiants de Claude
  Code dans le conteneur ; ou un surcoût de plus de la moitié de la durée d'une mission (`[HYPOTHÈSE]`).

### R190. Tester un modèle de décision avant d'en entraîner un : le tri, mesuré et calibré

- **Quoi** :
  - Avant tout entraînement, E26 : un modèle de décision ouvert, déjà publié, sur une décision fermée de TaskForce, le tri d'une
    issue (la priorité, le type, les étiquettes, parmi ce que le projet offre).
  - Trois bras et un repère : ce modèle de décision ; le meilleur modèle génératif du banc sur la machine de la Présidence
    (qwen3.5:9b) ; une règle écrite en mots (Gawande) ; et le taux de base, qui répond toujours la classe la plus fréquente.
  - Les cas : ceux du banc (Triage), la tâche de tri d'E11, et des cas écrits par la Présidence sur ses projets, sans donnée
    personnelle, avec des cas hors du domaine (Li) ; les bonnes réponses écrites avant.
  - Les mesures : la justesse ; le score de Brier, face à celui du taux de base ; un diagramme de fiabilité ; l'ECE seulement avec
    son intervalle (Prabhakar) ; la latence et la mémoire sur la machine.
  - MANTA lui-même ne sert pas ici : il est médical et demande 16 Go de mémoire GPU. On prend un modèle de décision ouvert qui tient
    sur 8 Go, ou le banc le dit trop lent.
  - Si un modèle de décision gagne, il entre comme option du banc pour la tâche Triage, sous les règles de toujours : il propose, la
    personne tranche.
- **L'attaque du contradicteur** : cinquante cas de tri écrits par nous mesurent ce que nous savons déjà ; une calibration sur un banc
  maison n'est pas une fiabilité dans le monde.
- **Réponse** (Duflo, Li) : des cas tirés au sort parmi ceux de la Présidence, des cas hors du domaine, et des résultats rapportés
  même en échec ; le banc ne prétend pas mesurer le monde, il dit ce qu'on peut confier ici.
- **Vote** : 23 oui, 1 abstention (Rus, conflit d'intérêts : Liquid AI publie un modèle de décision). 95,8 %.
- **Preuve en dix jours** : E26 faite sur la machine de la Présidence, les chiffres écrits, échecs compris.
- **Signal d'arrêt** : aucun modèle de décision ne bat qwen3.5:9b en justesse, ou son Brier ne bat pas celui du taux de base. Rien ne
  s'entraîne alors pour le tri, et R191 ne s'ouvre pas.

### R191. R175 amendée : rien d'entraîné dans le produit avant le client test ; au labo, un adaptateur pour une seule décision (second tour)

- **Quoi** :
  - Pour le produit, R175 et R61 tiennent : rien d'entraîné n'entre dans TaskForce avant le client test, ni avant que la banque le
    laisse passer.
  - « Cette année » (R61) devient une condition. Au labo, à l'essai, la Présidence entraîne sur sa machine, si E26 désigne un cas où
    un modèle de décision aide. E12 est amendée en ce sens : un adaptateur LoRA sur le tri (en QLoRA, jusqu'à 8 milliards de
    paramètres sur 8 Go, d'après les minimums publiés), comparé au modèle de base, au modèle de base avec recherche, et au meilleur
    modèle de décision d'E26.
  - Les données d'entraînement : publiques, ou écrites pour l'essai ; aucune donnée personnelle, aucune donnée de client ; les
    données synthétiques dites comme telles, parce qu'elles simulent nos propres croyances (C1).
  - Les cas de sûreté dans la banque, comme E12 le prévoyait : un adaptateur qui en perd un seul ne sort pas du labo (Bengio).
  - Publier un modèle « fait pour TaskForce » : seulement avec sa fiche (la base et sa licence, les données, la recette, les
    résultats et les échecs, les limites, et la mention qu'il ne juge pas des personnes) ; sous une licence ouverte compatible avec
    sa base ; après la relecture d'une personne qui ne l'a pas entraîné (R159) ; sans annonce avant que ça marche (R12, R65).
- **L'attaque du contradicteur** : ce consensus reporte l'idée de la Présidence derrière deux essais ; et un adaptateur appris sur
  quelques centaines de cas apprend ces cas-là, pas le tri.
- **Premier tour** : 18 oui, 4 non (Bengio, Hamilton, Harris : rien d'entraîné sans cas de sûreté ni fiche ; Musk : trop timide),
  2 abstentions (Rus, conflit d'intérêts ; Duflo : la valeur n'est pas mesurée). 75,0 %.
- **Amendements** :
  - les cas de sûreté et la fiche, écrits avant l'entraînement (Bengio, Hamilton) ;
  - l'essai dans les dix jours qui suivent E26, si E26 désigne un cas (Musk) ;
  - la relecture indépendante avant toute publication (Harris) ;
  - trois bras et un témoin, les cas tirés au sort, les échecs rapportés (Duflo) ;
  - des cas que l'adaptateur n'a jamais vus, hors de son domaine (le contradicteur).
- **Second tour** : 22 oui, 1 non (Harris, maintenu : aucun modèle publié sous le nom de TaskForce avant le client test), 1
  abstention (Rus, conflit d'intérêts). 91,7 %.
- **Preuve en dix jours** : E12 amendée, faite sur la machine de la Présidence, ses chiffres écrits.
- **Signal d'arrêt** : l'adaptateur ne bat pas le meilleur modèle de décision d'E26, ou perd un cas de sûreté. Rien ne se publie, et
  l'on garde le modèle existant, ou le génératif.

### R192. Les décisions qu'un modèle peut proposer, et celles qui restent au code ou à une personne

- **Quoi** : la table des cinq décisions de la saisine (pièce du secrétariat), adoptée, et une liste écrite.
  - **Le tri** : le premier candidat (R190). Le modèle propose, la personne tranche ; jamais « à qui la confier » sur le
    comportement d'une personne.
  - **L'étape de trop au brouillon** : après W4 et E25 ; chaque « Keep it » d'une personne devient une étiquette ; jamais une étape
    verrouillée, rien dans un workflow régulé (R175).
  - **La classe de l'action d'un outil** : une proposition au rédacteur d'un préréglage, qui ne peut que durcir ; jamais à
    l'exécution ; un outil ne devient une lecture que par une personne (R1).
  - **Le choix du modèle d'une tâche** : un calcul sur le banc, pas un modèle (R61, R20).
  - **Prévoir qu'un accord sera demandé** : le moteur de règles le sait déjà ; aucun modèle ne prévoit ce qu'une personne décidera.
  - **Ce qu'aucun modèle de TaskForce ne fera** : attribuer le travail sur le comportement ou les traits d'une personne, évaluer sa
    performance, prévoir qui accorde ou refuse. C'est l'annexe III, point 4(b), de l'AI Act ; le profilage écarte l'article 6(3), et
    une validation humaine ajoutée n'y change rien (projet de lignes directrices du 19/05/2026).
  - **Smart Assign**, déjà dans le code, pèse le taux de réussite passée de chaque personne et demande à un modèle de peser sa
    performance passée (dossier, point 5). `[DÉDUIT]` Sous le projet de lignes directrices, c'est une attribution sur un indicateur
    de comportement, donc un usage à haut risque à partir du 02/12/2027. À instruire en mode développement, avec la lecture d'un
    juriste : ne garder que des critères objectifs (les compétences déclarées, la charge, la disponibilité), et dire à la personne
    sur quoi repose la suggestion.
- **L'attaque du contradicteur** : une liste de refus écrite d'avance sera contournée par la première fonction utile ; la preuve,
  elle est déjà dans le code.
- **Réponse** (Vestager) : c'est pourquoi la liste nomme Smart Assign, et pourquoi elle se relit à chaque nouvelle fonction qui
  propose quelque chose à propos d'une personne.
- **Vote** : 23 oui, 1 abstention (Musk : trop de non écrits d'avance). 95,8 %.
- **Preuve en dix jours** : la liste écrite dans les notes du produit ; Smart Assign instruit, ses critères relevés et la décision
  à prendre posée à la Présidence.
- **Signal d'arrêt** : une fonction de TaskForce qui note des personnes, ou qui apprend de leurs décisions pour les prévoir.

### R193. Les modèles et les leçons propres à chaque entreprise : chez elle, sous ses règles, la banque pour barrière (second tour)

- **Quoi** :
  - La direction de la Présidence tient, et prolonge R60, R61 et R64 : une entreprise rend TaskForce meilleur pour son travail avec
    ce qu'elle y met. Dans cet ordre :
    1. la boucle (R61) : la banque nourrie par ses gestes, le registre des modèles par tâche, l'export de ses dossiers en décisions
       étiquetées, en format ouvert ;
    2. les leçons du harnais (R194), qui se lisent, se retirent et s'effacent ;
    3. puis, si la banque le justifie, des adaptateurs (LoRA) entraînés chez elle, sur sa machine ou son serveur, jamais chez
       TaskForce. TaskForce fournit la recette ouverte, le format des données, la banque et le registre ; un adaptateur est
       versionné comme une règle (son auteur, son empreinte, sa date), retiré d'un geste, et n'entre en service que s'il passe sa
       banque, sûreté comprise.
  - Les étiquettes : des faits du travail de préférence (la priorité corrigée, la mission appliquée ou écartée, les tests passés),
    plutôt que les accords et les refus d'une personne prise à part (Norman, Harris) ; les noms retirés de l'export.
  - RGPD : une finalité nouvelle, donc un test de compatibilité (article 6(4)) et l'information préalable des salariés (article 13,
    L1222-4) ; l'intérêt légitime, documenté en trois étapes, plutôt que le consentement des salariés, fragile ; la minimisation ;
    l'effacement par un réentraînement périodique et groupé, ou un filtre démontré sur les sorties ; l'analyse du statut du
    modèle ; une analyse d'impact probable dès qu'il y a profilage ; le CSE informé et consulté à partir de 50 salariés quand
    l'outil peut contrôler l'activité.
  - AI Act : aucun adaptateur qui juge des personnes (R192). `[DÉDUIT]` Un LoRA sur un petit modèle reste très loin du tiers du
    calcul initial : l'entreprise ne devient pas fournisseur d'un modèle à usage général ; elle peut devenir fournisseur du système
    qu'elle met en service.
  - GxP : TaskForce fournit l'infrastructure, le client contraint le modèle (R179, R187, ADR-022). `[DÉDUIT]` Un adaptateur qui
    apprend en continu serait un modèle dynamique, que le projet d'annexe 22 écarte des usages critiques ; une version figée,
    validée par le client sous sa maîtrise des changements, s'en rapproche. TaskForce ne dit jamais « conforme ».
  - TaskForce n'entraîne rien pour un client et ne voit pas ses données (R62, R64). Après le client test, et pas avant qu'une
    entreprise ait assez de décisions pour apprendre (C1).
- **L'attaque du contradicteur** : une entreprise de quarante personnes n'a personne pour entraîner un modèle, et la « recette » est
  un produit de plus à tenir ; dans une équipe de douze, une décision pseudonymisée désigne encore quelqu'un.
- **Premier tour** : 20 oui, 2 non (Vestager, Azoulay : rien sur les données des salariés sans analyse d'impact ni information), 2
  abstentions (Bezos : la plupart loueront ; Musk). 83,3 %.
- **Amendements** :
  - le canevas de l'analyse d'impact et la phrase qui informe les salariés, livrés avec l'export (Vestager, Azoulay) ;
  - dans une petite équipe, l'export ne garde pas l'auteur d'une décision, même pseudonymisé (le contradicteur) ;
  - la même boucle sert un modèle loué : la banque, le registre et les leçons ne dépendent pas des poids (Bezos, Nadella).
- **Second tour** : 23 oui, 1 abstention (Bezos, maintenu : la plupart des entreprises loueront). 95,8 %.
- **Preuve en dix jours** : le format d'export des décisions étiquetées écrit, puis joué sur la base de démo (le seed), sans un nom
  de personne dans le fichier ; et la fiche « ce que l'adaptateur apprend, de qui, et pour quoi », lue par la Présidence.
- **Signal d'arrêt** : un export qui contient le nom d'une personne, ou un texte libre qui n'est pas nécessaire ; ou une fonction qui
  note des personnes.

### R194. Un harnais qui apprend : la leçon devient une proposition de règle, versionnée, acceptée par une personne, rejouée par la banque (second tour)

- **Quoi** :
  - Ce que le dossier établit de Harness² : un dépôt de recherche de Google Research, sous Apache 2.0, qui n'est pas un produit de
    Google ; huit pièces du harnais modifiables, garde-fous compris ; aucune vérité terrain, mais des contrastes entre runs, jugés
    par un modèle éditeur ; une bibliothèque de leçons sans relecture ni version décrites ; ses propres limites (le coût, des leçons
    qui sur-apprennent, une dérive qu'il ne traite pas encore).
  - Ce que TaskForce en prend : l'écart entre deux runs (un échec et une réussite, une correction de la personne, un cas de la banque
    rejoué sous deux versions du harnais) comme source de leçons ; et la forme d'une leçon : la situation, la leçon, la preuve (les
    deux dossiers).
  - Ce qu'il y ajoute, que Harness² n'a pas : un corrigé (la banque, ses critères écrits avant, notés par du code) ; le socle hors de
    portée (« No agent changes the rules », `RulesFloor.java:40-41`) ; une personne qui accepte ; une version immuable (V125) ; le
    retour en arrière.
  - Le chemin d'une leçon :
    1. une proposition, jamais une modification : une règle en mots, une convention du brouillon, un cas de la banque, une
       préférence de modèle pour une tâche ;
    2. la banque la rejoue avant toute activation, sur les cas qui l'ont fait naître et sur tous les autres, sans une régression ;
    3. elle n'est montrée que si elle gagne sur au moins deux cas qu'elle n'a pas vus naître (le contradicteur : sinon, c'est un run
       chanceux) ;
    4. la personne qui peut changer les règles l'accepte, la change ou la refuse, la preuve sous les yeux avant le bouton (Norman) ;
    5. elle entre versionnée, avec son auteur, sa preuve et son empreinte, au dossier, et se retire d'un geste.
  - Ce qu'une leçon ne touche jamais : le socle ; une règle qui demande ou refuse (une leçon peut durcir, jamais relâcher) ; les
    étapes verrouillées ; les sorties.
  - C'est R175 tenue (l'IA propose, rien d'entraîné) ; c'est « l'IA propose, une personne décide, le moteur exécute », appliqué au
    harnais lui-même ; et c'est la voie la moins chère vers ce qu'une entreprise apprend (R193) : une leçon se lit et s'efface, un
    poids non.
  - Au labo d'abord (E29) ; dans le produit, après le client test, dans un lot à lui (W10, R195).
- **L'attaque du contradicteur** : une personne qui accepte chaque leçon deviendra un tampon, la fatigue de l'accord appliquée au
  harnais ; et une leçon née de deux runs est un run chanceux.
- **Premier tour** : 19 oui, 3 non (Musk : la banque suffit, sans personne ; Saarinen : une proposition de plus, c'est du bruit ;
  Harris : la fatigue de l'accord), 2 abstentions (LeCun, Zhuo). 79,2 %.
- **Amendements** :
  - une leçon n'est montrée qu'après un gain sur au moins deux cas qu'elle n'a pas vus naître, et aucune régression (LeCun) ;
  - au plus une fournée de propositions par semaine et par espace (Harris, Saarinen) ;
  - les leçons comptées dans les signaux de confiance (E17 : la part des accords lus) ;
  - la preuve avant le bouton (Norman).
- **Second tour** : 23 oui, 1 non (Musk, maintenu : une leçon qui ne fait que durcir devrait s'activer quand la banque passe). 95,8 %.
- **Preuve en dix jours** : E29, au labo, sur le tri.
- **Signal d'arrêt** : une régression sur un cas de la banque après une leçon acceptée ; ou aucune leçon utile sur trois proposées.
  Une leçon qui relâcherait une règle est impossible par construction : si cela arrivait, tout s'arrête.

### R195. Ce que cela change : J2 inchangé, sauf les tests ; W5, W6, W9 et un lot W10 ; quatre expériences ; le pitch sans promesse

- **Quoi** :
  - **J2 et E20** : rien n'entre, sauf l'état des tests en cours, dans W5 (R188). Le client test passe d'abord, et aucune date ne
    court (décision sur la séance n°26).
  - **Le plan des lots** de la [séance n°25](./2026-11-13-le-workflow-pilotable-plan-des-lots.md) :
    - W5 : l'état « les tests tournent » d'une étape d'agent, et sa limite ;
    - W6 : le bac à sable du test à blanc, ajouté le 15/11, et l'isolement d'un run (R189) répondent au même besoin, une exécution
      sans effet au dehors. `[HYPOTHÈSE]` W6 pose le niveau 2 ou 3 d'isolement comme bac à sable du test à blanc, sans en faire un
      prérequis ;
    - W9 : la fourchette des missions (R188), puis les durées par étape, tirées du dossier, comme prévu ;
    - W10, nouveau, après J2 : les leçons du harnais (R194), sur la même porte que les règles.
  - **La R&D** : E26 (un modèle de décision existant sur le tri), E27 (un run dans un conteneur), E28 (la couverture d'une
    fourchette), E29 (une leçon rejouée par la banque) ; E12 amendée (R191) ; E1 avance par E28, le premier intervalle émis par le
    produit ; E19 se nourrit d'E26.
  - **Le pitch** : « tout tourne sur votre machine, le modèle aussi » est établi pour l'app desktop (R62). Rien sur l'entraînement,
    sur des modèles faits pour TaskForce ou sur l'isolement avant leur preuve (R12, R65, R168) ; MANTA ne se cite nulle part en
    public comme un résultat de TaskForce.
  - **Smart Assign** (R192) : une instruction en mode développement, avant le 02/12/2027.
- **L'attaque du contradicteur** : quatre expériences pour une personne, c'est un second J2.
- **Réponse** (Duflo, Prabhakar) : E28 est une requête sur le dossier, E26 et E29 tiennent dans une journée chacune au labo, E27 dans
  une demi-journée ; aucune ne touche le code de J2.
- **Vote** : 23 oui, 1 abstention (Shotwell : chaque ligne ajoutée à W6 et W9 est une promesse de plus). 95,8 %.
- **Preuve en dix jours** : le plan des lots amendé (W5, W6, W9, W10), relu par la Présidence ; E26 et E28 lancées.
- **Signal d'arrêt** : une expérience de ce PV qui prend du temps à J2 avant le client test : elle attend.

### Les votes en une table

| R | Recommandation | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R188 | La vue d'un run | 23 | | Jobs | 95,8 % (20 au premier tour) |
| R189 | Un run sur la machine | 23 | LeCun | | 95,8 % (19 au premier tour) |
| R190 | Tester avant d'entraîner | 23 | | Rus | 95,8 % |
| R191 | R175 amendée, pour le labo | 22 | Harris | Rus | 91,7 % (18 au premier tour) |
| R192 | Ce qu'un modèle peut proposer | 23 | | Musk | 95,8 % |
| R193 | Les modèles et les leçons d'une entreprise | 23 | | Bezos | 95,8 % (20 au premier tour) |
| R194 | Un harnais qui apprend | 23 | Musk | | 95,8 % (19 au premier tour) |
| R195 | Ce que cela change | 23 | | Shotwell | 95,8 % |

### Questions à la Présidence

1. **Les tests en cours** (R188) : les veut-elle dans J2, dans W5, ou après le client test avec le reste ?
2. **La fourchette** (R188) : accepte-t-elle qu'il n'y ait jamais un chiffre seul, et rien sous cinq missions comparables ? Les
   seuils d'E28 (une couverture de 70 % au moins pour une fourchette qui vise 80 %) sont à confirmer ou à changer.
3. **Le run sur la machine** (R189) : quels postes d'abord, ceux des ingénieurs seulement, ou aussi ceux sans développeur ? Et quel
   moteur essayer sur sa machine, Podman par WSL2 ou le moteur dans WSL2 ? Sa machine est sous Windows 11 Famille, sans Hyper-V, et
   avec WSL 2.7.13, quand les conteneurs de WSL demandent la 2.9.3 au moins.
4. **L'entraînement** (R190, R191) : le Conseil propose le tri comme première décision ; en veut-elle une autre ? Sous quelle
   licence publier (Apache 2.0, comme MANTA et ses bases, ou une autre), sous quel nom, et sur sa machine ou sur Kaggle, retenu pour
   E12 le 30/10 ?
5. **Le client test** (R193) : mettra-t-il dans TaskForce des décisions de ses salariés (des accords, des refus, des tris) ? Oui ou
   non, sans détail.
6. **Smart Assign** (R192) : le garder tel quel jusqu'au client test, ou retirer dès maintenant la performance passée de ses
   critères ?
7. **Harness²** (R194) : ses propres corrections (ses refus, ses « Keep it », les priorités qu'elle change) peuvent-elles nourrir
   les leçons d'E29 au labo ?
8. **MANTA** : où l'a-t-elle vu le 15/11 ? Ses dépôts datent du 10/11 ; le secrétariat veut dater sa source.

## Décision de la Présidence

Tranchée le 16/11/2026, en conversation. Le secrétariat avait remontré R188 à R195 à la Présidence, chacune avec ce qu'elle dit,
les voix contre ou abstenues au second tour et leur raison, et sa recommandation. La Présidence répond en un message, mot pour
mot :

> « R188 :
>
> Je suis d'accord avec Jobs, 1 chiffre ou rien, avec unite si necessaire. Apres on pourrait faire un truc genre : si les
> estimation sont tjr a 80% juste sur les, jsp moi, les 10 dernieres estimation, alors on affiche juste le chiffre, enfin le
> temps quoi voila, chiffre + unite on va dire, mais si c'est en dessous alors on affiche l'estimation, donc trouver une petite
> formule tres courte comme "temps estime : X + unite" avec le deompcte quand mm mais qui s'adapte du coup, genre il decoule
> quand mm, et une fois a 0 ca mets loading ou finalisation ou bref t'as compris quoi un truc qui demande a l'utilisateur
> d'attendre encore 30 secondes right ? Je pense que ca niveau UI/UX c'est ok.
>
> R189 :
>
> Oui Lecun a pas tord la dessus. Par contre faudrait faire gaffe. Imagine quand on installe Taskforce, ca ouvre une instance
> Docker par exemple ou autre, a voir sur Mac par exemple ce que ca donne, mais disons chaque PC ouvre sa propre instance en
> gros. on verra plus tard pour faire du partager. Dans ce cas la, ca voudrais dire que par defaut, tout ce qui est execute,
> c'execute dans le container Docker right ? Enfin je vexu dire t'aurais vraiment tout sur le PC + tout ce qui releve de
> l'execution, des runs, des bac a sable et ainsi de suite, serait en environnement isole via un container ou une autre
> technologie. Et ca devrait etre le cas partout je pense. Ca devrait etre active par defaut effectivement. Donc oui je suis
> d'accord avec toi, mais comment on fait pour le bac a sable si la personne n'utilise pas Claude code ? Imaginons qu'elle
> utilise "Juste" qwen4 en 27B par exemple, pour tout faire genre elle a vraiment que ca. Que ce passe t'il alors ? Comment on
> isole les tests, les runs, les executions, ... Le cloud est payant, c'est une solution mais c'est payant et pour l'instant je
> peux pas me le permettre. je pars du principe que sur notre propre machine, elle sont suffisament puissante ajd pour ne pas
> payer super cher un abo cloud.
>
> Donc je suis plus d'accord avec Lecun, a voir comment on fait ca, si c'est viable, pertinent, facile d'utilisation, ...
>
> J'aurais aucun pb d'ailleurs a build notre propre system de bac a sable hein, enfin je veux dire si faut commencer a faire du
> C j'ai pas de pb, de l'assembly ou autre mdrrrr, mais faut juste que ce soit pertinent, qu'on ai un objectif clair et
> pertinent pour les clients. Docker me semble pertinent mais c'est pace que je l'utilise quoi, et que c'est quand mm
> relativement lege quoi.
>
> Mais faut que ce soit scalable et robuste, donc faut proposer des choses. En etant realiste aussi
>
> R190 :
>
> Conflit d'interet je m'en fiche, tu travail pour moi, pour Taskforce, et plus pour ta boite en etant ici. Ton entreprise est
> tres interressante justement pour ton modele de decision, mais je ne vais pas le copier puisque je souhaite etre modele
> agnostic, donc il n'y a aucun conflit d'interet. Donc oui on peut faire ca evidemment, qu'elle est la pertinence d'entrainer
> un modele finalement si il y en a deja des top gratuit qu'on peut installer ? Bon ensuite Faut voir comment orhcestrer ca,
> comment rendre ca niveau UI/UX, pour l'instant l'entrainement on pourrait peut etre s'abstenir, de toute facon c'est derisoire
> j'ai aucun h100 ca prendrais beaucoup trop de temps. Donc on retiens, mais on execute pas ce truc la pour le moment. Bon par
> contre on garde tjr l'idee de realiser des benchmark avec les modeles qu'on a quoi, mais en permanence j'ai envie de dire,
> genre chaque requete est evalue stv et ajouter a un benchamrk commun quoi.
>
> R191 :
>
> Oui je suis d'accord, on pourra peut etre le faire plus tard ca right ? Avec les donnees client en fait. Donc a retenir mais
> pour l'instant on fait pas
>
> R192 :
>
> Alright qu'en penses Musk ? je pense qu'on peut le suivre, mais effectivement lesmart assign de toute facon ne sera as utilise
> je pense.
>
> R193 :
>
> Bezos, oui je suis d'accord, mais elles loueront les machines pour l'entrainement, pas pour heberger les modeles. Est ce que
> je me trompe ? Quelles entreprises ne reverais pas d'avoir ses propres models, adapte a ses workflows, a ses evolutions, ...
> Et nous sommes models agnostic ne l'oublions pas, peut importe ce que fas l'utilisateur, on n'a rien a voir cote modele, si il
> souhaite en entrainer lui mm ou utiliser des modeles deja existant via des plateformes, c'est pas un pb, il connecte sa
> plateforme, il connecte son LLM sur sa machine ou sur le cloud bref il peut faire ce qu'il veut pour faire tourner taskforce,
> c'est tout. Donc oui elles loueront, mais en attendant c'est eux ou moi qui aurait la data. Donc a voir, de toute facon on
> fait pas d'entrainement pour le moment.
>
> R194 :
>
> Je serais partant pour l'idee de Musk en realite, si ca corrige, si ca ameliore, si ca augmente la precision du harnais et
> ainsi de suite, je vois pas pk l'utilisateur devrait choisir en fait.
>
> R195 :
>
> comprends pas je dois voter quoi la dedans ? Chaque ligne ajoutee au plan est une promess en plus, quelle plan, le miens ?
> Celui de taskforce ?
>
> Les questions pour moi :
>
> Je suis d'accord avec l'option 2 »

Le secrétariat a ensuite proposé sa lecture, recommandation par recommandation, avec deux confirmations à donner : sa lecture de
R192, et le sort de R195. La Présidence répond, mot pour mot :

> « oui c'est ça pour R192, et je retiens R195 »

La dernière ligne du premier message, « Je suis d'accord avec l'option 2 », répond à une autre question, sur le point « avant
d'appliquer » de TF-J2-10 : elle est consignée au [PV de la séance n°25](./2026-11-13-le-workflow-pilotable.md), complément du
16/11/2026.

Dans ce qui suit, **la décision** est ce que la Présidence a dit ou confirmé. Les **précisions du secrétariat** sont à part : ce
ne sont pas ses mots.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R188 | Retenue, amendée (avec Jobs) | « Je suis d'accord avec Jobs, 1 chiffre ou rien, avec unite si necessaire. » |
| R189 | Retenue, amendée (avec LeCun) | « Ca devrait etre active par defaut effectivement. » ; « Donc je suis plus d'accord avec Lecun » |
| R190 | Retenue, pas exécutée maintenant | « Donc on retiens, mais on execute pas ce truc la pour le moment. » |
| R191 | Retenue, pour plus tard | « Donc a retenir mais pour l'instant on fait pas » |
| R192 | Retenue, amendée (avec Musk) | « je pense qu'on peut le suivre » ; « oui c'est ça pour R192 » |
| R193 | Retenue, sans entraînement pour l'instant | « de toute facon on fait pas d'entrainement pour le moment. » |
| R194 | Retenue, amendée (avec Musk) | « Je serais partant pour l'idee de Musk en realite » |
| R195 | Retenue, mise à jour par ces décisions | « je retiens R195 » |

- **R188, retenue, amendée (avec Jobs)** : « Je suis d'accord avec Jobs, 1 chiffre ou rien, avec unite si necessaire. » La
  fourchette de R188 tombe.
  - **La décision** :
    - un seul chiffre avec son unité, jamais une fourchette ;
    - si au moins 8 des 10 dernières estimations comparables étaient justes, l'écran dit seulement « 4 min » ; sinon, il dit
      « Temps estimé : 4 min ». La Présidence : « si les estimation sont tjr a 80% juste sur les, jsp moi, les 10 dernieres
      estimation, alors on affiche juste le chiffre », et, en dessous, « trouver une petite formule tres courte comme "temps
      estime : X + unite" » ;
    - le chiffre décompte et se réajuste : « avec le deompcte quand mm mais qui s'adapte du coup » ;
    - à 0 sans être fini, l'écran passe à « Finalisation… » : « une fois a 0 ca mets loading ou finalisation », « un truc qui
      demande a l'utilisateur d'attendre encore 30 secondes right ? ».
  - **Précisions du secrétariat** : « juste » veut dire la durée réelle à 20 % près ; E28, amendée, le mesure. Les mots de
    l'écran s'écrivent en anglais, comme toute l'interface.
  - **Ce qui ne change pas** : les tests en cours restent dans W5, donc dans J2 ; l'estimation va dans W9, après J2.
- **R189, retenue, amendée (avec LeCun)** : « Ca devrait etre active par defaut effectivement. » ; « Donc je suis plus d'accord
  avec Lecun ».
  - **La décision** : l'isolement est par défaut, partout, quel que soit l'agent. La Présidence : « tout ce qui releve de
    l'execution, des runs, des bac a sable et ainsi de suite, serait en environnement isole via un container ou une autre
    technologie. Et ca devrait etre le cas partout je pense. » R189 faisait du conteneur « une option d'isolement, jamais un
    prérequis », par défaut pour les seuls dépôts venus du dehors : c'est la position maintenue de LeCun au second tour qui est
    retenue.
  - **Ce que la Présidence demande** : « comment on fait pour le bac a sable si la personne n'utilise pas Claude code ? » ; sans
    cloud payant (« Le cloud est payant, c'est une solution mais c'est payant et pour l'instant je peux pas me le
    permettre. ») ; « Mais faut que ce soit scalable et robuste, donc faut proposer des choses. En etant realiste aussi ».
  - **Précisions du secrétariat, proposées le 16/11/2026** en réponse. Ce ne sont pas des mots de la Présidence, et E27 doit les
    prouver :
    - l'isolement vit dans le runner, pas dans l'agent. Avec un modèle local seul, ce sont les outils de TaskForce (shell,
      fichiers, tests) qui s'exécutent dans le bac à sable. Avec Claude Code, le runner le lance lui-même dans le bac à sable ;
    - une seule interface, un moteur choisi selon la machine : bubblewrap sous Linux ; Seatbelt sous macOS, et une machine
      virtuelle Linux légère (le framework Containerization d'Apple) pour les tests qui exigent Linux ; une distribution WSL2
      dédiée sous Windows ; Docker ou Podman seulement s'ils sont déjà installés ;
    - le modèle reste hors du bac à sable, avec le GPU ;
    - pas de bac à sable écrit en C par TaskForce : les noyaux fournissent les briques, et le moteur de bac à sable de Claude
      Code, publié en open source, peut servir. La Présidence y était prête (« J'aurais aucun pb d'ailleurs a build notre propre
      system de bac a sable »), à une condition : « faut juste que ce soit pertinent, qu'on ai un objectif clair et pertinent
      pour les clients » ;
    - le projet d'[ADR-028](../../decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md) les écrit, avec ses options écartées ;
      la preuve est E27, amendée en ce sens, sur Windows, macOS et Linux.
  - **Ce qui ne change pas** : aucun isolement ne sert à relâcher une règle ; le hook des règles reste, et chaque sortie reste
    jugée.
- **R190, retenue, pas exécutée maintenant** : « Donc on retiens, mais on execute pas ce truc la pour le moment. »
  - **La décision** : E26 attend, sans date (« pour l'instant l'entrainement on pourrait peut etre s'abstenir, de toute facon
    c'est derisoire j'ai aucun h100 ca prendrais beaucoup trop de temps. »). Le banc permanent est retenu : « on garde tjr
    l'idee de realiser des benchmark avec les modeles qu'on a quoi, mais en permanence j'ai envie de dire, genre chaque requete
    est evalue stv et ajouter a un benchamrk commun quoi. » Chaque requête est évaluée et nourrit le banc, par modèle et par
    tâche : c'est la boucle de R61.
  - **Sur le conflit d'intérêts du secrétariat**, un modèle d'Anthropic : « Conflit d'interet je m'en fiche, tu travail pour
    moi, pour Taskforce, et plus pour ta boite en etant ici. » TaskForce ne copie le modèle de personne : « je souhaite etre
    modele agnostic ».
  - **Précision du secrétariat** : un banc commun à plusieurs entreprises ne garde que des scores agrégés, avec leur accord, et
    aucun contenu ne sort.
- **R191, retenue, pour plus tard** : « Oui je suis d'accord, on pourra peut etre le faire plus tard ca right ? Avec les donnees
  client en fait. Donc a retenir mais pour l'instant on fait pas ».
  - **La décision** : E12 attend, avec son texte d'avant la séance ; l'amendement que R191 lui proposait n'est pas rangé.
  - **Précision du secrétariat** : R191 écartait toute donnée de client de l'essai au labo. Un entraînement « Avec les donnees
    client » relève donc de R193 et de sa précision : avec l'accord écrit du client, et pour lui.
- **R192, retenue, amendée (avec Musk)** : « Alright qu'en penses Musk ? je pense qu'on peut le suivre, mais effectivement
  lesmart assign de toute facon ne sera as utilise je pense. » Musk s'était abstenu : trop de non écrits d'avance. La lecture du
  secrétariat, confirmée par la Présidence (« oui c'est ça pour R192 ») :
  - pas de liste de refus écrite d'avance : chaque fonction se juge au cas par cas ;
  - sauf la ligne de la loi : aucun modèle de TaskForce ne note des personnes ni n'attribue le travail sur leur comportement (AI
    Act, annexe III, point 4(b)) ;
  - Smart Assign ne servira pas : son critère de performance passée sort, dans le lot de nettoyage.
- **R193, retenue, sans entraînement pour l'instant** : « de toute facon on fait pas d'entrainement pour le moment. »
  - **La décision** : TaskForce reste agnostique sur les modèles. La Présidence : « nous sommes models agnostic ne l'oublions
    pas, peut importe ce que fas l'utilisateur, on n'a rien a voir cote modele ». À l'abstention de Bezos (la plupart des
    entreprises loueront), elle répond par une question : « elles loueront les machines pour l'entrainement, pas pour heberger
    les modeles. Est ce que je me trompe ? » `[HYPOTHÈSE]` Le dossier ne le tranche pas.
  - **Précision du secrétariat**, sur « c'est eux ou moi qui aurait la data » : en cloud, TaskForce héberge les données comme
    sous-traitant (RGPD, article 28). Elles restent au client. Un entraînement sur elles ne se fait qu'avec son accord écrit, au
    contrat, et pour lui.
- **R194, retenue, amendée (avec Musk)** : « Je serais partant pour l'idee de Musk en realite, si ca corrige, si ca ameliore, si
  ca augmente la precision du harnais et ainsi de suite, je vois pas pk l'utilisateur devrait choisir en fait. » Musk avait voté
  non au second tour : une leçon qui ne fait que durcir devrait s'activer quand la banque passe.
  - **La décision** :
    - une leçon qui durcit le harnais s'active seule quand la banque d'évaluations la valide ;
    - elle est versionnée, notifiée et annulable d'un geste ;
    - une leçon ne relâche jamais une règle et ne touche jamais au socle.
  - **Précision du secrétariat** : `[DÉDUIT]` le reste de R194 tient. La banque rejoue la leçon avant toute activation, sans une
    régression, avec un gain sur au moins deux cas qu'elle n'a pas vus naître : c'est ce que « valider » veut dire. Seule
    l'acceptation par une personne, avant l'activation, tombe pour une leçon qui durcit.
- **R195, retenue, mise à jour par ces décisions** : la Présidence a d'abord demandé « comprends pas je dois voter quoi la
  dedans ? Chaque ligne ajoutee au plan est une promess en plus, quelle plan, le miens ? Celui de taskforce ? ». Le plan est le
  [plan des lots](./2026-11-13-le-workflow-pilotable-plan-des-lots.md) de la séance n°25, celui de TaskForce ; la phrase qu'elle
  cite est la raison de l'abstention de Shotwell. Après la lecture du secrétariat : « je retiens R195 ».
  - J2 inchangé, sauf l'état des tests en cours (W5) ;
  - l'isolement par défaut après J2, avec le test à blanc (W6), via E27 et ADR-028 ;
  - l'estimation (W9) ;
  - W10, les leçons auto-activées quand elles durcissent ;
  - au labo : E27, E28 et E29 ; ni E26 ni E12 pour l'instant.

**Les réponses aux huit questions du Conseil.** Quatre sont tranchées par ce message, une l'est en partie, trois restent
ouvertes.

1. **Les tests en cours** (R188) : tranchée. Dans J2, dans W5 : la Présidence retient R188 et n'amende que l'estimation.
2. **La fourchette** (R188) : tranchée, par un refus. « 1 chiffre ou rien » : pas de fourchette. Les seuils d'E28 changent : 8
   estimations justes sur les 10 dernières (la Présidence), à 20 % près (le secrétariat).
3. **Le run sur la machine** (R189) : tranchée pour les postes, partout et quel que soit l'agent. Le moteur à essayer sur sa
   machine reste ouvert, avec Q25 : le secrétariat propose une distribution WSL2 dédiée (ADR-028), et E27 l'essaie.
4. **L'entraînement** (R190, R191) : ouverte, et sans objet pour l'instant. Rien ne s'entraîne ; la première décision à
   apprendre, la licence, le nom et le lieu de publication attendent E26 et E12, avec Q23.
5. **Le client test** (R193) : ouverte. Le message n'y répond pas ; elle va avec Q24.
6. **Smart Assign** (R192) : tranchée. La performance passée sort de ses critères, dans le lot de nettoyage, sans attendre le
   client test.
7. **Harness²** (R194) : ouverte. Le message ne dit pas si les corrections de la Présidence peuvent nourrir les leçons d'E29 ;
   elle va avec Q26.
8. **MANTA** : répondue. La Présidence l'a vu dans un post LinkedIn, le 15/11/2026, cinq jours après ses dépôts.

## Notes du secrétariat

- **Le dossier** : le code de `dev` (`3da4f4a8`) lu dans sa copie, les relevés du 15/11 et `taskforce-docs` (`7bbcbc5`) ; des pages
  publiques seulement, lues le 15/11/2026 par le secrétariat et trois agents de recherche, sans connexion ni formulaire. Le
  secrétariat a relu lui-même les sources qui portent une recommandation (dossier, en-tête). Les résumés des moteurs de recherche
  n'ont servi qu'à trouver les pages.
- **Les fiches** : aucune rafraîchie, aucune n'ayant plus de 30 jours au 15/11/2026 (charte, §9).
- **Corrections du brief de séance** :
  - le compteur de fichiers existe : « {count} files », avec les lignes ajoutées et retirées, relu toutes les deux secondes pendant
    le travail (`mission-changes.tsx:336-344`) ; il ne manque pas ;
  - MANTA n'a pas été publié le 15/11 : ses dépôts datent du 10/11/2026 (05:19 UTC pour le 27B) ; ses bases sont des Qwen
    (Qwen3.8-27B, Qwen3.5-4B) ; il ne publie aucun score de Brier ;
  - « tout le monde peut faire tourner entre 4B et 12-14B » reste une `[HYPOTHÈSE]` : sur la machine de la Présidence, un modèle de
    14 milliards tourne déjà à 44 % sur le processeur (09/11).
- **Corrections des documents** :
  - `recherche/CLAUDE.md`, §3 : C4 dit encore « pas de GPU » (07/2026) ; la machine de la Présidence a une carte de 8 Go. À mettre à
    jour par la Présidence, C1 restant entière ;
  - le post sur Harness² dit « Google just open-sourced » : c'est un dépôt de Google Research qui se dit « not an officially
    supported Google product », et son « sans corrigé ni évaluateur » n'est vrai qu'à moitié (pièce Harness²).
- **Hors fiche, hors champ** :
  - Bezos : « la plupart des entreprises loueront » vient de sa position de la n°10, appuyée sur l'histoire d'AWS, pas d'une
    déclaration récente de sa fiche ;
  - Azoulay transpose la recommandation de l'UNESCO sur la neurotechnologie à des modèles qu'elle ne vise pas ;
  - Vestager parle de l'AI Act, dont sa fiche ne trouve aucune déclaration récente : elle parle depuis sa grille, les faits viennent
    du dossier ;
  - Gawande, Duflo, Doudna et Li transposent leur méthode à des modèles de décision, au-delà de positions publiques minces sur ce
    sujet ;
  - Jobs, hors de son champ sur les conteneurs et les licences.
- **Anachronismes** : Jobs ne connaît ni Docker, ni les modèles de langue, ni MANTA que par le dossier ; Hamilton ne connaît MANTA
  (10/11/2026), Harness² (09/10/2026) et les microVM pour agents que par le dossier.
- **Conflits d'intérêts** :
  - Rus a cofondé Liquid AI, dont le modèle de décision d1 figure dans la table de MANTA ; elle s'est abstenue sur R190 et R191 ;
  - Nadella dirige Microsoft, qui fait WSL et ses conteneurs, et GitHub ; Li deviendra dirigeante d'AMD, fabricant de cartes
    graphiques ; Zhuo a rejoint Meta, qui publie des modèles ouverts ; Bezos a fondé Amazon, qui vend le cloud ; Musk dirige xAI ;
    Saarinen dirige Linear ;
  - le secrétariat et ses agents de recherche sont des modèles d'Anthropic. Claude Code est l'agent du runner, et son bac à sable est
    cité au dossier ; des modèles d'Anthropic sont l'éditeur et des juges dans l'article de Harness², et un point de comparaison dans
    la fiche de MANTA.
- **Sources manquantes** :
  - le rapport technique de MANTA (à paraître), et toute évaluation de MANTA par un tiers ;
  - une procédure officielle pour le moteur Docker dans WSL2 sans Docker Desktop (aucune trouvée) ;
  - le parc matériel des entreprises de 10 à 249 personnes (aucune source publique trouvée) ;
  - les chiffres d'Unsloth sont des minimums, sur des pages non datées ; ceux d'Ollama sont des tailles de téléchargement ;
  - le texte final de l'annexe 22 ; la version finale des lignes directrices de la Commission sur le haut risque (seul le projet du
    19/05/2026 existe) ; les recommandations de la CNIL sur l'IA au travail, annoncées pour 2026 ;
  - des prépublications de 2026 sur l'auto-amélioration des harnais, repérées par la recherche et non lues (arXiv 2609.24972 et
    2606.13643).
- **Numérotation** : R188 à R195, Q23 à Q26 et E26 à E29 vérifiés libres dans `taskforce-docs` (`feature/lean-oss`, `7bbcbc5`) le
  15/11/2026 ; ADR-028 est libre, pour un brouillon si R189 ou R193 est retenue.
- **Après la décision** (16/11/2026) :
  - **Les seuils de R188** : « 8 des 10 dernières » lit « a 80% juste sur les, jsp moi, les 10 dernieres estimation » ; « à 20 %
    près » n'est pas un mot de la Présidence, c'est une précision du secrétariat, qu'E28 mesure.
  - **Les précisions sur R189** sont du secrétariat ; la décision est l'isolement par défaut, partout. Deux de leurs faits
    n'étaient pas au dossier de la séance. Le secrétariat en a ouvert les dépôts le 16/11/2026, sans plus : le moteur de bac à
    sable de Claude Code, publié à part sous Apache 2.0, en préversion de recherche
    ([Sandbox Runtime](https://github.com/anthropic-experimental/sandbox-runtime)) ; le framework Containerization d'Apple, qui
    fait tourner des conteneurs Linux sous macOS, sous Apache 2.0 ([Apple](https://github.com/apple/containerization)). Ils sont
    à relire en entier avant E27.
  - **Le conflit d'intérêts** : ce moteur est celui d'Anthropic, dont le secrétariat est un modèle. La Présidence l'écarte
    (« Conflit d'interet je m'en fiche ») ; le secrétariat continue de l'écrire ici.
  - **R194** : `[DÉDUIT]` la décision parle d'une leçon qui durcit. Une leçon qui ne durcit rien (une convention du brouillon,
    une préférence de modèle) reste une proposition qu'une personne accepte, comme R194 le disait ; les étapes verrouillées et
    les sorties, que R194 mettait hors de portée d'une leçon, y restent. À confirmer avec Q26.
  - **Ce que les précisions laissent ouvert** : ce que fait une mission quand la machine n'offre aucun moteur d'isolement (R189
    disait : elle le dit avant de partir). C'est posé à la Présidence dans ADR-028.
  - **La numérotation** : E26 à E29 gardent leurs numéros ; ADR-028 est pris par le projet sur l'exécution isolée.
- **L'avis du secrétariat**, après la clôture : le mien, pas celui du Conseil.
  - `[DÉDUIT]` La vue d'un run est faite aux deux tiers ; ce qui compte n'est pas l'estimation, c'est le silence des tests, jusqu'à
    quinze minutes sans un mot. C'est le premier correctif, et le moins cher.
  - `[DÉDUIT]` « Un env de run sur la machine » est déjà l'architecture de TaskForce. La vraie question est l'isolement, et sur
    Windows le chemin le moins cher n'est pas Docker Desktop : c'est WSL2, avec le bac à sable de Claude Code ou Podman. La machine
    de la Présidence, sous Windows Famille, n'a pas Hyper-V.
  - `[DÉDUIT]` MANTA montre que la recette est désormais commune : une base ouverte, LoRA, une tête, des décisions étiquetées. Ce
    qui manque à TaskForce n'est pas le calcul, la carte existe ; ce sont les étiquettes (C1). D'où E26 avant tout entraînement, et
    les leçons du harnais avant les poids.
  - `[DÉDUIT]` Le constat le plus urgent n'était pas dans la saisine : Smart Assign pèse la performance passée des personnes, la zone
    que l'AI Act classe à haut risque au 02/12/2027.
  - **Mon ordre** : E28 (une requête, aucun code) ; E26 au labo ; l'état des tests en cours dans W5 ; E27 ; puis E29 ; R191 seulement
    après E26.

## Suites

- Le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal.
- À `Questions-ouvertes.md` : Q23 (quelle décision mérite un modèle, et sur quelles étiquettes), Q24 (qui répond d'un adaptateur ou
  d'une leçon d'entreprise, au sens du RGPD et de l'AI Act), Q25 (l'isolement d'une mission sous Windows natif), Q26 (ce qu'une leçon
  peut proposer de changer, et ce qu'elle ne touche jamais).
- Si la Présidence les retient, à `experiences/Experiences.md` : E26 à E29, et E12 amendée (R191).
- Si elles sont retenues : un brouillon d'ADR-028 pour l'isolement d'une mission sur la machine (R189) ; le plan des lots de la
  séance n°25 complété par R195 (W5, W6, W9, W10).
- En mode développement, après la décision : l'événement du runner au lancement des tests et l'étape Check (W5) ; Smart Assign
  instruit (R192), avec la lecture d'un juriste.
- `recherche/CLAUDE.md`, §3 : C4 à mettre à jour par la Présidence.
- Après la décision de la Présidence, rangé le 16/11/2026 :
  - au registre de la charte (§12) et au Journal : « la Présidence tranche la séance n°27 » ;
  - à `Questions-ouvertes.md` : Q23 et Q24 restent ouvertes (aucun entraînement pour l'instant ; le sous-traitant en cloud) ;
    Q25 et Q26 passent en cours (l'isolement par défaut partout ; la leçon qui durcit s'active seule) ;
  - à `experiences/Experiences.md` : E27, E28 et E29 entrent, retenues, E27 amendée par R189 et E28 par R188 ; E26 entre,
    retenue mais en attente, sans date ; E12 garde son texte et attend (R191) ;
  - le projet d'[ADR-028](../../decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md), l'exécution isolée par défaut ;
  - au [plan des lots](./2026-11-13-le-workflow-pilotable-plan-des-lots.md) de la séance n°25 : W5 (les tests en cours), W6
    (l'isolement par défaut), W9 (le temps estimé), W10 (les leçons du harnais), chaque fois la décision à part des précisions ;
    et W2, pour l'option 2 de TF-J2-10 (complément du 16/11/2026 au PV n°25).
- Restent, après ce rangement :
  - à la roadmap, en mode développement : l'événement du runner au lancement des tests et l'étape Check (W5) ; le critère de
    performance passée retiré de Smart Assign, dans le lot de nettoyage ; le lot W10 ; la ligne de TF-J2-10 ;
  - au labo, sans rien prendre à J2 : E28, E27, puis E29 ;
  - à la Présidence : relire ADR-028 et dire ce que fait une mission sans moteur d'isolement ; les questions 3 (le moteur), 4, 5
    et 7 ci-dessus.
- Rien ne migre vers `v1/` sans tâche ni ADR (quarantaine, [`CLAUDE.md`](../../CLAUDE.md) §2).

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
