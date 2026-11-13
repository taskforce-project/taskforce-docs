---
id: conseil-seance-2026-11-13-le-workflow-pilotable
title: "Séance n°25 du 13/11/2026 : le workflow pilotable"
doc_type: pv-seance
statut: active
date: "13/11/2026"
auteur: Pierre MICHEL
formation: élargie
tags: [recherche, conseil, seance, workflow, processus, bpmn, ux, moteur, applications-embarquees, j2]
related:
  - "../README.md"
  - "./2026-11-13-depasser-camunda.md"
  - "./2026-11-09-atelier-recette-113.md"
  - "./2026-11-05-atelier-fenetre.md"
  - "../../decisions/ADR-023-DRAFT-execution-durable-postgresql.md"
  - "../../decisions/ADR-026-DRAFT-la-fenetre.md"
  - "../../decisions/ADR-027-DRAFT-modele-des-processus.md"
  - "../../experiences/Experiences.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°25 du 13/11/2026 : le workflow pilotable

> Simulation : les membres sont des personnages simulés, à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien. Les décisions
> de Jobs sur le dessin sont celles d'un personnage simulé.
>
> **En bref.** La Présidence a retenu R163 à R170 et repasse ses amendements au Conseil, avec son go (« donc go »). Le Conseil, en
> élargie (11), les valide un par un, avec deux conditions : l'IA ne juge ce qui est de trop qu'au brouillon, jamais sur une étape
> verrouillée ; « tout d'un coup » se construit sans maquette, mais sur une spécification d'UX écrite, revue à l'écran (R161) et
> lue en une minute par trois lecteurs (E24). Il fixe le chantier :
> - l'expérience de Claude Code, où l'on pilote dans la conversation, et trois applications embarquées à côté : Board, Workflow,
>   Documents ;
> - une vue du projet au rang du board, en étapes de gauche à droite, des nœuds réels, trois densités pour le CEO, le PM et
>   l'ingénieur, et aucun symbole de BPMN ;
> - cinq types d'étapes dans un sous-ensemble écrit de BPMN 2.0, des versions immuables, définir à part d'exécuter ;
> - une IA qui propose avec des conventions, des exemples, un vérificateur en code et la banque d'évaluations, sans rien
>   entraîner ;
> - un moteur qui refait chez nous les mécanismes de Temporal et d'Operaton, prouvé par des coupures, Operaton en témoin ;
> - six lots dans J2 avant E20, quatre après.
>
> Neuf recommandations, R171 à R179, toutes à 90 % au moins, six au second tour. Margaret Hamilton, contradictrice, a obtenu la
> liste de ce qu'on lâche d'abord si E20 glisse, et des seuils écrits avant l'essai du moteur.

- **Saisine** (Présidence, 13/11/2026 au soir, dans le message qui tranche la séance n°24, mot pour mot) :
  - « prends en compte tout ce que je viens de te dire pour le process, et puis peut-être que tu peux valider ça avec le conseil,
    mais moi je suis plutôt convaincu de ce que je dis » ;
  - « On repasse ça au conseil pour valider, mais moi je suis à peu près sûr de ce que je dis, donc go. » ;
  - sur l'UX : « faudrait peut-être mettre Jobs sur la partie UX, encore une fois » ; « La maquette avant de trancher, non, tu peux
    faire tout d'un coup. Enfin, discute avec Jobs et tout, essaye de faire une UX sympa. »
  - **La question** : le chantier du workflow pilotable. Valider les amendements de la Présidence ; fixer l'expérience (celle de
    Claude Code, plus des applications embarquées), la vue du workflow, le modèle des processus, l'IA qui les propose, le moteur et
    l'ordre des lots.
  - **Les questions à trancher** :
    1. les amendements de la Présidence, un par un ;
    2. l'expérience : la conversation où l'on pilote, les applications embarquées (board, workflow, documents), le passage de l'une
       à l'autre ;
    3. la vue : ses trois niveaux (l'objectif, l'exécution, la gouvernance), ses trois lectures (CEO, PM, ingénieur), l'anatomie
       d'un nœud, ses gestes, les incidents, les attentes et les manques, ce qu'on ne fait pas ;
    4. le modèle : les types d'étapes, le sous-ensemble de BPMN, les versions, la séparation entre définir, exécuter et exploiter ;
    5. les workflows par défaut : comment l'IA juge ce qui est de trop, comment une personne ajoute ses étapes (l'exemple du LIMS),
       qui valide ;
    6. le moteur : reproduire chez nous ce qu'Operaton et Temporal font, sans fork, et comment le prouver ;
    7. l'ordre des lots, et ce qui entre dans J2 avant E20.
  - **Horizon** : J2 et E20, le premier client joué de bout en bout (seconde quinzaine de décembre, `[HYPOTHÈSE]`), puis J3 à J5.
- **Formation** : séance n°25, élargie (11), proposée par le secrétariat ; Jobs mène l'UX, à la demande de la Présidence.
  - Impulsion : Steve Jobs, qui tranche le dessin par délégation ; Elon Musk.
  - Pont : Kenza Ait Si Abbou.
  - Harmonie : Margrethe Vestager, Nandan Nilekani.
  - Science : Margaret Hamilton, Atul Gawande, Yoshua Bengio.
  - Design : Don Norman, Julie Zhuo, Karri Saarinen.
  - **Pourquoi eux** :
    - Jobs et le pôle Design pour l'UX ; Hamilton et Gawande pour la rigueur d'exécution et les listes de contrôle ; Bengio pour la
      sûreté des agents ;
    - Vestager pour la réglementation : hors de son champ sur la pharmacie, elle parle depuis sa grille (un usage, son risque, sa
      règle, la preuve qu'elle s'applique) ;
    - Nilekani pour le passage à l'échelle, plutôt que Nadella : son angle (des agents qui masquent la complexité, la conformité
      dans l'architecture, des formats ouverts) répond à « un CEO comprend tout » ; et Nadella dirige Microsoft, dont Power
      Automate et Copilot Studio sont les voisins directs d'un workflow pilotable ;
    - Musk, la voix d'Impulsion, pour ce qu'on supprime ; Ait Si Abbou, onzième membre, pour la personne qui ne fait pas de
      logiciel, qu'elle défendait à la n°24.
  - **Contradictrice** : Margaret Hamilton. Elle ne l'a été qu'à la n°8. Son angle (ce qui n'est pas écrit avant ne se vérifie
    pas ; ce qu'on lâche d'abord quand on sature) est le mieux placé pour attaquer un consensus né d'une validation donnée d'avance :
    « tout d'un coup », l'IA qui juge ce qui est de trop, un moteur refait chez nous. Shotwell l'était à la n°24.
  - **Ordre de parole**, tiré au sort le 13/11/2026 à 19:34 UTC (`shuf`) : Kenza Ait Si Abbou, Margaret Hamilton, Nandan Nilekani,
    Margrethe Vestager, Don Norman, Julie Zhuo, Steve Jobs, Karri Saarinen, Elon Musk, Atul Gawande, Yoshua Bengio.
  - **Règle de vote** (charte §6.5) : 90 % des présents, soit 10 oui sur 11 au moins.
- **Fiches** : aucune fiche rafraîchie. Toutes ont moins de 30 jours au 13/11/2026 : Norman, Zhuo et Saarinen datent du 28/10, Ait
  Si Abbou du 26/10, les sept autres du 21/10, soit 23 jours. Jobs et Hamilton, sièges historiques, ne se rafraîchissent que sur
  une nouvelle source historique ; aucune n'est apparue.

## Dossier

Constitué le 13/11/2026 par le secrétariat. Pages publiques seulement, lues ce jour, sans connexion ni formulaire : Claude et MCP,
Operaton, Temporal, l'ASF, l'OMG, Ollama, Camunda, le texte de 21 CFR Part 11 (sur le site de Cornell, celui de l'eCFR refusant la
lecture automatique), la Commission européenne, l'EMA et l'ISPE. Sur TaskForce : `taskforce-docs` (`feature/lean-oss`, `237a6a4`),
le code de `origin/dev` (`b195413f`), la carte du code pour cette vue et la recherche sur les vues de workflow, toutes deux du
13/11. La saisine demandant un chantier entier, le dossier compte dix points, et deux pièces du secrétariat.

1. `[ÉTABLI]` **La décision de la Présidence sur la séance n°24** (13/11/2026 au soir, [PV](./2026-11-13-depasser-camunda.md)).
   - R163 à R170 retenues : « Donc R163 à 170, donc je retiens ».
   - Les amendements : se repositionner sur l'expérience de Claude Code, plus des applications embarquées (R163) ; la cible tenue
     « à peu près », puis des marchés plus complexes (R164) ; un sous-ensemble de BPMN pour nos processus, pas seulement pour
     l'échange, des workflows par défaut, des agents qui les créent selon des règles, des conventions et des exemples, l'IA qui juge
     ce qui est de trop, des workflows d'utilisateurs (le LIMS), affichés et édités par les ingénieurs et les PM, pas orienté full
     code, cinq types d'étapes, définir, exécuter, exploiter, la version, les incidents, les attentes, les accords et les manques
     (R165) ; s'inspirer de Camunda sans ses symboles, pour un CEO, un PM et un ingénieur (R166) ; pas de fork d'Operaton (R167) ;
     Jobs sur l'UX (R169) ; pas de maquette ; Camunda plus tard.
   - Une question laissée au Conseil : « Est-ce qu'on peut entraîner un agent exprès là-dessus, etc. »
2. `[ÉTABLI]` **L'existant de l'interface** ([ADR-026](../../decisions/ADR-026-DRAFT-la-fenetre.md) ; `v1/02-produit/Frontend.md` ;
   carte du code de `origin/dev`, 13/11/2026).
   - La fenêtre : la conversation vit dans le shell, au centre ; le volet est la page de la route, à côté, redimensionnable, en
     pleine largeur au besoin, la conversation repliée alors dans le compositeur ; chaque état a son adresse (`?issue=`, `?c=`) ;
     à droite, Environment, Context, Connectors, Results, Changes, Missions.
   - Le board : une route du projet, ses onglets (Board, List, Roadmap, Backlog, Cycles, Teams hors de l'app desktop, Settings), le
     temps réel du projet.
   - La vue d'une mission : un volet à son adresse (`/{slug}/missions/{runId}`) ; cinq étapes en phrases (Understand, Plan, Do,
     Check, Hand over), chacune avec son état (`not-started`, `in-progress`, `waiting`, `done`, `skipped`, `failed`, `stopped`) ;
     les changements fichier par fichier ; la preuve repliée ; les accords décidés par `PendingApproval`, complet ou compact.
   - « Waiting for you » : une liste en trois groupes, « Needs you », « What happened », « Alerts ».
   - Le canevas du workflow d'aujourd'hui : React Flow (`@xyflow/react` 12), en lecture seule, un nœud par analyse et des arêtes vers
     les agents, sans issue, dépendance, accord ni fichier ; il ne s'ouvre qu'en dialogue depuis la carte des missions, sans
     adresse. La Présidence l'a jugé « horrible » (séance n°24).
3. `[ÉTABLI]` **Les données** (carte du code de `origin/dev`, 13/11/2026 ; `core/model/Project.java`).
   - Les issues d'un projet viennent avec leur statut, leur responsable, leurs dates et leur parent ; les relations (« blocked
     by ») ne se lisent qu'issue par issue, et un changement de relation ou de colonne ne publie rien.
   - Les missions se lisent par espace, 200 au plus ; leurs étapes et leurs accords, par la route d'activité ; aucun sujet temps
     réel : le shell les interroge toutes les 5 secondes, la vue d'une mission toutes les 2 à 5 secondes.
   - Un accord porte qui peut décider, qui a demandé, la règle et sa raison, la portée, qui il attend, les signatures, s'il engage,
     son échéance ; il se décide par `POST /delivery/runs/{runId}/approvals/{approvalId}`, et chaque décision entre au dossier.
   - Le projet n'a ni but, ni date visée, ni critères de réussite : `Project.java` porte son nom, son identifiant, sa description,
     son statut, son dépôt et sa commande de test. R56 reste à construire.
   - Aucun processus ni moteur : `RuleScope.PROCESS` et un champ de processus toujours vide ; une mission avance quand on la lit.
   - W0, lancé (branche `feat/workflow-live-data`) : les dépendances de tout un projet en une lecture, publiées à chaque
     changement ; les missions du projet et leurs accords en une lecture paginée ; un sujet `/topic/projects.{id}.delivery` pour
     les états, les étapes et les accords ; la couche de données du front ; aucun écran.
4. `[ÉTABLI]` **La direction artistique et la grammaire de l'interface** (`v1/14-design/Direction_Artistique_2026.md`,
   `Design_System.md` v2.0 ; séances [n°18](./2026-11-05-atelier-fenetre.md) et [n°20](./2026-11-09-atelier-recette-113.md)).
   - Geist et Geist Mono ; des gris chauds ; un seul bleu d'action, `#2f6bf6` ; des angles droits ; des paires teinte et encre
     pour les états ; des ombres chaudes ; un contraste AA en clair et en sombre.
   - La direction de la Présidence, à la n°20 : « tu peux t'inspirer de Claude Desktop et Dust par exemple comme c'est ma DA
     globalement, avec experience Mac/Raycast/Apple evidemment » ; on prend la structure, jamais l'identité (R119, R133).
   - R124 : une police ; une couleur d'accent ; des séparateurs d'un pixel plutôt que des cadres ; jamais une carte dans une carte ;
     des icônes de 16 px d'un seul trait ; des mouvements de 150 à 200 ms, sans rebond.
   - R133 : aucun mot interne au premier regard ; une phrase d'abord, le détail à un clic, le brut à deux ; un dialogue d'une
     colonne, en 420, 560 ou 720 px ; ce qui attend se montre là où l'on regarde ; un échec dit ce qui s'est passé et quoi faire.
   - Le dessin de Jobs à la n°20 : des lignes de liste de 36 px ; le déroulé d'une mission en lignes de 40 px (un rond vide, un
     anneau qui tourne, une coche) ; `+12 −1` en chiffres à chasse fixe.
5. `[ÉTABLI]` **Comment Claude embarque des applications** (pages publiques, lues le 13/11/2026).
   - Les artefacts s'ouvrent à côté de la conversation, dans leur propre fenêtre ou panneau : documents, code, sites, tableaux de
     bord, petits outils ; on les change en le demandant ou à la main ; ils peuvent appeler Claude et garder des données
     ([Claude](https://support.claude.com/en/articles/9487310-what-are-artifacts-and-how-do-i-use-them)).
   - Claude Code Desktop : une barre à gauche ; la conversation au centre ; le compositeur en bas, et dessous l'environnement, le
     dossier, le mode, le modèle et l'anneau d'usage ; à droite, les cartes de la session (Environment, Changes, Context, Background
     tasks) ; des volets ouverts depuis la barre du titre (Terminal, Changes, Browser, Files), déplaçables et redimensionnables. On
     pilote par le mode de permission (Manual, Accept edits, Plan, Auto, Bypass permissions), l'arrêt, une correction tapée pendant
     le travail, un commentaire sur une ligne du diff ([Claude Code](https://code.claude.com/docs/en/desktop)).
   - Les connecteurs interactifs, depuis le 26/01/2026 : Asana, Box, Figma, Slack et d'autres s'affichent comme des applications
     dans la conversation ; ils reposent sur MCP Apps, une extension ouverte de MCP
     ([Claude](https://claude.com/blog/interactive-tools-in-claude)).
   - MCP Apps : un outil déclare une ressource `ui://` ; l'hôte la rend dans un cadre isolé, dans la conversation ; l'application et
     l'hôte se parlent en JSON-RPC par `postMessage` ; elle peut appeler des outils, envoyer des messages et mettre à jour le
     contexte du modèle, et l'hôte passe par le consentement de la personne pour ce qu'il fait en son nom ; Claude, Claude Desktop,
     VS Code GitHub Copilot et Microsoft 365 Copilot la prennent en charge
     ([MCP](https://modelcontextprotocol.io/extensions/apps/overview)).
   - Les connecteurs : Claude prend les droits de chaque personne chez l'outil ; un propriétaire règle chaque permission sur
     « Always allow », « Needs approval » ou « Blocked », réglages qui ne peuvent que restreindre
     ([Claude](https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities)).
6. `[ÉTABLI]` **Les vues de workflow qui tournent** (la recherche du 13/11/2026 : 33 produits, leurs pages publiques seulement,
   Camunda 8.10 compris).
   - Quinze motifs : une carte, des modes séparés ; l'état sur le nœud, et seul le présent bouge ; « en attente d'une personne »
     est un état à part, trié en tête ; l'étape déclare sa question, l'interface rend un contrôle typé ; la règle se voit sur la
     décision ; les opérations risquées dans un mode préparé ; de l'incident à la réparation sans quitter la carte ; relancer depuis
     une étape en gardant l'original ; suivre l'exécution, aller à l'échec, éclairer le chemin ; plusieurs vues, une sélection ; un
     inspecteur ancré plutôt qu'une bulle ; la preuve accrochée au nœud ; la trace de l'agent dans son nœud ; lisible à des
     milliers de nœuds ; la même carte pour améliorer, et une ligne de santé.
   - Les contre-exemples : une fenêtre par-dessus l'application ; voir sans pouvoir agir ; la pelote de toutes les arêtes ; des
     couleurs sans légende ; une mise en page qui saute ; des attentes cachées et de faux verts ; un bouton « Approve » nu ; les
     journaux comme seul détail ; une vivacité qu'il faut deviner.
   - Trois archétypes, qui s'empilent : le tableau d'étapes vivant pour cadre, les arêtes du graphe du travail à la demande, les
     portes du plan de processus en nœuds de plein droit.
   - Chez Camunda : Operate marque l'élément en échec d'un incident et celui qui attend d'un mot
     ([attentes](https://docs.camunda.io/docs/components/operate/userguide/view-wait-states/)) ; son mode de modification pose un
     bandeau, liste les changements, offre l'annulation et une revue avant d'appliquer
     ([modification](https://docs.camunda.io/docs/components/operate/userguide/process-instance-modification/)) ; en 8.10, le
     détail d'un élément quitte la bulle pour des onglets ancrés
     ([Operate](https://docs.camunda.io/docs/components/operate/userguide/basic-operate-navigation/)) ; Camunda prévient qu'une
     relance ne vérifie pas que la cause est réglée
     ([incidents](https://docs.camunda.io/docs/components/operate/userguide/resolve-incidents-update-variables/)).
7. `[ÉTABLI]` **Le modèle des processus**.
   - BPMN 2.0.2 définit, à côté de la conformité complète, trois sous-classes de la modélisation : « Descriptive », « Analytic » et
     « Common Executable ». La dernière sert les outils qui produisent des modèles exécutables ; elle exige XML Schema, WSDL et
     XPath, et comprend les tâches de service et humaines, l'appel d'un autre processus, les passerelles exclusive, parallèle et à
     événements, le sous-processus intégré, les événements de minuterie et de message, l'erreur de bordure ; la zone ad hoc n'en
     fait pas partie ([OMG, formal/2013-12-09](https://www.omg.org/spec/BPMN/2.0.2/PDF), chapitre 2).
   - Camunda 8.10 exécute bien plus : passerelle inclusive, sous-processus d'événement et ad hoc, multi-instance, signaux,
     escalade, compensation (séance n°24, dossier, point 5).
   - TaskForce : rien de construit pour TF-J2-2 (« un canevas modifiable, cinq types d'étapes, exécuté par le moteur durable
     v1 ») ; les règles sont déjà des données versionnées, chaque version immuable avec son auteur et son empreinte (V125).
8. `[ÉTABLI]` **L'IA qui propose un processus**.
   - R61 : « Aucun entraînement dans TaskForce cette année (C1, C4) » ; C1, N ≈ 1 ; C4, ni GPU ni budget.
   - La banque d'évaluations existe : huit cas fixes par modèle (TF-J1-4), 22 cas sur sept tâches au banc (TF-J1-11) ; chaque échec
     devient un cas (R118) ; le volet Progress les montre.
   - Ollama accepte un schéma JSON dans `format`, qui contraint la sortie du modèle
     ([Ollama](https://docs.ollama.com/capabilities/structured-outputs)).
   - Les voisins : le BPMN Copilot de Camunda, en SaaS seulement, produit un diagramme à partir d'une description en mots, et une
     nouvelle version à chaque fois ([Camunda, 08/04/2025](https://camunda.com/blog/2025/04/camunda-8-7-release/)) ; UiPath Maestro
     génère un modèle BPMN à partir d'une description ; avec ProcessOS, des agents proposent et une personne approuve avant la
     production (séance n°24, dossier, points 6 et 9).
9. `[ÉTABLI]` **Le moteur** ([ADR-023](../../decisions/ADR-023-DRAFT-execution-durable-postgresql.md), amendé le 13/11/2026).
   - Temporal : l'historique d'événements est la source de vérité ; après une panne, le code du workflow se rejoue sur lui ; ce code
     doit être déterministe ; le résultat d'une activité s'enregistre et ne se refait pas au rejeu ; une activité se reprend par
     défaut sans limite de tentatives, à partir d'une seconde, avec un facteur de 2
     ([workflows](https://docs.temporal.io/workflows), [reprises](https://docs.temporal.io/encyclopedia/retry-policies)).
   - Operaton : le moteur sauve l'exécution à chaque état d'attente, et une exception ramène l'instance au dernier ; l'exécuteur de
     travaux verrouille les travaux dus par un propriétaire et une expiration, sous un verrou optimiste ; un travail échoué se
     reprend deux fois, puis le moteur s'arrête sur lui et crée un incident ; les travaux d'une instance passent l'un après l'autre
     ([transactions](https://docs.operaton.org/docs/documentation/user-guide/process-engine/transactions-in-processes),
     [exécuteur](https://docs.operaton.org/docs/documentation/user-guide/process-engine/the-job-executor),
     [incidents](https://docs.operaton.org/docs/documentation/user-guide/process-engine/incidents)).
   - La licence : du code sous Apache 2.0 peut entrer dans un projet sous GPLv3, pas l'inverse
     ([ASF](https://www.apache.org/licenses/GPL-compatibility.html)).
10. `[ÉTABLI]` **La réglementation, pour l'exemple du LIMS**.
    - 21 CFR Part 11 ([Cornell LII](https://www.law.cornell.edu/cfr/text/21/11.10)) : des pistes d'audit horodatées pour les
      saisies et les actions qui créent, changent ou suppriment un enregistrement (11.10(e)) ; « Use of operational system checks to
      enforce permitted sequencing of steps and events, as appropriate » (11.10(f)) ; des contrôles d'autorité (11.10(g)) ; une
      signature électronique porte le nom imprimé du signataire, la date et l'heure, et sa signification, « such as review,
      approval, responsibility, or authorship » ([11.50](https://www.law.cornell.edu/cfr/text/21/11.50)) ; elle est liée à son
      enregistrement ([11.70](https://www.law.cornell.edu/cfr/text/21/11.70)) ; hors d'une session continue, chaque signature se
      fait avec tous ses éléments, et dans une session, la première aussi
      ([11.200](https://www.law.cornell.edu/cfr/text/21/11.200)).
    - L'Union européenne : la consultation sur le chapitre 4, l'annexe 11 révisée et une nouvelle annexe 22 (l'IA) des BPF a couru
      du 07/07/2025 au 07/10/2025, et elle est close
      ([Commission](https://health.ec.europa.eu/consultations/stakeholders-consultation-eudralex-volume-4-good-manufacturing-practice-guidelines-chapter-4-annex_en)).
      Le projet d'annexe 22 ne s'applique pas à l'IA générative ni aux LLM, qui ne devraient pas servir dans les usages critiques des
      BPF ; ailleurs, une personne qualifiée répond de leurs sorties, une personne dans la boucle
      ([projet d'annexe 22](https://health.ec.europa.eu/document/download/5f38a92d-bb8e-4264-8898-ea076e926db6_en?filename=mp_vol4_chap4_annex22_consultation_guideline_en.pdf), §1).
      À son atelier des 30/06 et 01/07/2026, l'EMA examine encore les suites de la consultation, qui a montré un soutien à l'ouverture
      possible de l'IA générative et des LLM ; elle y cherche l'avis d'experts sur leurs garde-fous
      ([EMA](https://www.ema.europa.eu/en/events/good-manufacturing-practice-multistakeholder-workshop-expert-contributions-artificial-intelligence-guidance-development-annex-22)).
    - GAMP 5, seconde édition (ISPE) : l'effort de validation se règle sur l'impact GxP, la complexité et la nouveauté d'un système,
      avec l'esprit critique des experts du domaine
      ([ISPE](https://ispe.org/pharmaceutical-engineering/january-february-2023/what-you-need-know-about-gampr-5-guide-2nd-edition)).
    - TaskForce : les accords savent qui accorde, la double signature, la séparation des rôles et le seuil (TF-J2-4) ; le dossier
      est chaîné et scellé, pas encore signé (TF-J2-7) ; un accord se donne d'un clic, dans une session ouverte.
    - Les contraintes du terrain : une personne et des agents, aucun revenu, gratuit ; E20 en seconde quinzaine de décembre,
      `[HYPOTHÈSE]` ; C1 à C4 du labo.

### La méthode pour qu'un agent propose un processus (pièce du secrétariat)

La réponse à « peut-on entraîner un agent exprès ? ». `[ÉTABLI]` Pas cette année : R61, C1 et C4. `[DÉDUIT]` Il reste quatre
leviers, tous déjà dans le produit ou à sa portée :

| Levier | Ce que c'est | Ce qui existe |
| --- | --- | --- |
| Des conventions | Une liste de moins de dix lignes : une étape, un verbe et un objet ; une personne qui en répond ; une zone et des règles pour chaque étape d'agent ; les points de pause ; une décision jugée par du code ; une attente qui dit ce qu'elle attend ; les étapes verrouillées gardées ; une raison pour chaque étape écartée ; les questions dites | Les plans écrits par demande courante (R117) |
| Des exemples | Les workflows par défaut, puis ceux de l'espace | Le déroulé de la mission (R138) |
| Un vérificateur en code | Le sous-ensemble, donné au modèle comme schéma de sortie, puis vérifié : ses erreurs reviennent au modèle, deux fois au plus, puis à la personne | Le schéma JSON d'Ollama ; le moteur de règles, ses cas (ADR-025) |
| La banque d'évaluations | Des objectifs dont on connaît les propriétés attendues, des cas pièges ; chaque échec devient un cas | La banque, le banc, Progress (R113, R118, R131) |

`[DÉDUIT]` Un modèle qui échoue à la banque ne propose pas de brouillon ; la boucle se possède avant les poids (R61), et les
dossiers pourront un jour servir de données, avec le consentement de l'entreprise.

### « Pas orienté full code » : qui configure quoi (pièce du secrétariat)

`[HYPOTHÈSE]` Une proposition, pour la discussion : personne n'écrit de code pour dire comment le travail se fait ; les détails
existent, rangés à un clic.

| Qui | Ce qu'il fait, en mots | Ce qu'il ne fait pas |
| --- | --- | --- |
| Le CEO | Écrit l'objectif en une phrase ; lit l'en-tête ; décide aux portes | Régler une étape |
| Le PM, ou qui mène le travail | Choisit un workflow par défaut ; ajoute, retire, renomme des étapes ; dit qui répond et qui décide ; écrit des règles en mots ; crée des agents de gestion de projet avec leurs règles (R94) | Écrire du code ou une expression |
| L'ingénieur | Règle les détails dans des champs typés : l'agent, le modèle, les outils permis, le délai, les tentatives, la condition d'une décision, la fiche d'environnement (TF-J2-9) ; lit la définition et l'export BPMN | Éditer le XML ou passer outre le vérificateur |
| L'IA, sur n'importe quel modèle | Propose un brouillon et ses questions | Publier ; ajouter ou écarter une étape à l'exécution |
| TaskForce | Tient le socle, le vérificateur, le moteur, le dossier | Relâcher une règle |

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre dit ce qu'il retient des amendements et ce que le chantier doit fixer. Les interventions
sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Kenza Ait Si Abbou (Pont)

- Dans une entreprise de quarante personnes, la personne qui accorde une étape ne lit ni BPMN ni journal. La Présidence le dit à sa
  façon : un CEO doit comprendre, un PM doit s'en servir sans peine.
- Elle lit « pas orienté full code » comme ceci : personne n'écrit de code pour dire comment le travail se fait ; les détails
  techniques existent, rangés à part, pour qui en a besoin.
- Le LIMS est le bon exemple : l'experte du domaine n'est pas développeuse. Elle doit pouvoir ajouter IQ, OQ et PQ en mots, les
  rendre obligatoires, et dire quels documents chacune attend.
- Un manque se dit comme on le dirait à un collègue : quel document, pourquoi, à qui on l'a demandé.
- *Sa recommandation : chaque nœud se lit en une phrase par quelqu'un qui ne fait pas de logiciel, et la vue n'est pas finie
  avant l'essai d'une minute.*

### 2. Margaret Hamilton (Science, siège historique, contradictrice)

- Operaton, Temporal et les agents, elle ne les connaît que par le dossier. Elle y lit deux mécanismes qu'elle a toujours
  défendus : l'état d'attente comme point de sauvegarde, et l'incident qui arrête l'étape au lieu de laisser l'instance mentir.
- Elle attaque « tout d'un coup » : sans maquette, le risque passe dans la construction. Il faut donc, pour chaque lot, des
  critères de fin écrits avant.
- Elle attaque « l'IA juge ce qui est de trop » : une étape retirée par un modèle pendant l'exécution, c'est une interface sans
  contrat. Ce qui peut sauter s'écrit avant, ce qui ne peut pas sauter aussi.
- Un moteur refait chez nous se prouve par des coupures provoquées, avec des seuils écrits avant, pas par sa ressemblance avec
  Operaton.
- Sa question : quand le chantier sature avant E20, que lâche-t-on d'abord, et qui l'a décidé avant ?
- *Sa recommandation : l'ordre des lots, et pour chacun ce qu'on lâche en premier, écrits aujourd'hui.*

### 3. Nandan Nilekani (Harmonie)

- À l'échelle, la conformité vit dans l'architecture, pas dans un manuel : le sous-ensemble, son vérificateur et le moteur sont la
  règle ; l'écran ne fait que la montrer.
- Des agents qui masquent la complexité : le CEO lit une ligne, le PM des cartes, l'ingénieur la définition. Le même objet en
  dessous, trois profondeurs.
- Les workflows par défaut sont un bien commun : une bibliothèque au format ouvert, publiée avec le code, que chacun copie et
  adapte, comme les packs (R103).
- Un processus qu'on ne peut pas sortir, c'est une plateforme fermée : l'export BPMN reste, et l'import depuis Camunda viendra.
- Sa question habituelle, la voix : elle existe dans le compositeur (R76), et piloter le workflow en mots passe déjà par elle.
- *Sa recommandation : un seul vérificateur pour tout ce qui entre (l'import, le brouillon de l'IA, l'éditeur), et les workflows
  par défaut publiés avec le code.*

### 4. Margrethe Vestager (Harmonie)

- Hors de son champ sur la réglementation pharmaceutique, elle parle depuis sa grille : un usage, son risque, sa règle, et la
  preuve que la règle exécutée est celle adoptée.
- Le dossier cite 21 CFR 11.10(f) : des contrôles qui imposent l'ordre permis des étapes. C'est ce que fait un moteur de
  processus ; la règle d'un régulateur devient une propriété de l'architecture.
- Le projet d'annexe 22 écarte les LLM des usages critiques des BPF et veut ailleurs une personne dans la boucle. Proposer un
  workflow est un usage non critique ; exécuter doit rester déterministe.
- Elle refuse toute phrase publique « conforme au 21 CFR Part 11 » : la conformité appartient au système validé chez le client,
  pas à l'outil.
- Se brancher à Camunda plus tard, oui, sans s'enfermer : le client garde ses processus, ses règles et son dossier.
- *Sa recommandation : la carte des exigences, écrite en face des fonctions de TaskForce, ligne par ligne, avec ce qui manque, et
  rien de revendiqué.*

### 5. Don Norman (Design)

- La délégation partielle est la zone dangereuse. Une IA qui retire des étapes sans le dire, c'est l'automatisation qui prend la
  main sans prévenir.
- Chaque étape laissée de côté se voit, avec sa raison et un moyen de la remettre ; l'annulation, partout où le geste se défait.
- Un incident dit ce qui s'est passé et quoi faire, sur le nœud. Une relance qui passe au vert avant que la cause soit réglée est
  un mensonge, et le dossier montre que Camunda le prévient lui-même.
- Le nœud est un dialogue, pas un voyant : ce qui a été fait, ce qui attend, qui décide, ce qui ne se défera pas.
- *Sa recommandation : sur chaque nœud, fait, attend, décide ; sur chaque étape écartée, pourquoi, et « la garder ».*

### 6. Julie Zhuo (Design, conflit d'intérêts : Meta)

- Trois lectures sur une même surface, c'est le risque de n'en servir aucune. Elle veut les questions de la première minute
  écrites avant de construire, et mesurées.
- Les workflows par défaut tuent la page blanche. L'IA y est d'abord conseillère, puis adjointe : elle propose, une personne
  accepte chaque étape.
- Une promotion de l'agent se gagne par des évaluations : un modèle qui écarte une étape obligatoire dans la banque ne propose plus
  de brouillon.
- Des préférences dites en mots plutôt que des dizaines de réglages : « pas orienté full code » va dans ce sens.
- *Sa recommandation : les trois questions de la première minute, écrites avant, mesurées sur trois personnes.*

### 7. Steve Jobs (Impulsion, siège historique, mène l'UX)

- Claude Code, Linear et Camunda, il ne les connaît que par le dossier. La Présidence a trouvé la phrase de l'expérience : on
  pilote dans la conversation, les applications s'ouvrent à côté. C'est un produit, pas un assemblage de trois autres.
- Il dit non : non aux symboles, non à une fenêtre par-dessus, non à un éditeur à part, non à une quatrième application tant que
  les trois premières ne sont pas excellentes.
- Une seule carte du projet, que tout le monde lit ; le détail se déplie, il ne se cherche pas.
- Quand on demande un accord, la personne voit une phrase, la règle, et ce qui suivra.
- Il tranchera le dessin par délégation, comme aux séances n°18 et n°20 ; la Présidence garde le dernier mot.
- *Sa recommandation : l'application Workflow au rang du board, trois densités d'une même carte, et rien de plus avant E20.*

### 8. Karri Saarinen (Design, conflit d'intérêts : Linear)

- Il parle avec son conflit d'intérêts : « piloter un board comme si on était sur Linear » nomme son produit.
- Un établi, pas un chat : la conversation pilote, mais le travail répété se fait dans l'application, structurée, dense et rapide,
  au clavier.
- Des réglages par défaut tranchés : un workflow par type de travail, peu d'options.
- Il maintient sa réserve de la n°24 : une forme générée n'est pas un problème résolu. Le brouillon de l'IA reste une proposition,
  jamais une conception.
- *Sa recommandation : l'état d'abord, le détail à un clic ; des nœuds réels seulement ; aucun brouillon accepté en bloc.*

### 9. Elon Musk (Impulsion)

- Supprimer d'abord : cinq types d'étapes suffisent, la Présidence le pense aussi ; pas de sixième avant qu'E20 en exige un.
- « Pas de fork » ne veut pas dire « pas de dépendance » : embarquer Operaton sans le modifier n'est pas un fork. Il le dit, et
  prend acte du choix de la Présidence de refaire.
- Si l'on refait, refaire le minimum : la table des travaux, le journal, l'incident. Le reste quand un essai l'exige.
- Le chiffre qui compte : le nombre de jours avant qu'une entreprise fasse tourner son premier processus.
- *Sa recommandation : J2 ne porte qu'un processus, celui d'E20, de bout en bout ; tout le reste après.*

### 10. Atul Gawande (Science)

- IQ, OQ et PQ sont des listes de contrôle inscrites dans le flux : des tâches humaines, avec leurs listes de moins de dix lignes,
  leurs signatures et leurs documents.
- Les points de pause de TF-J2-10 ne s'écartent jamais, ni par l'IA ni par un réglage : ce sont les étapes verrouillées par
  défaut.
- Il redemande la mesure avant et après sur E20 : combien d'erreurs bêtes avec le processus, combien sans.
- Pas de type de plus pour la liste de contrôle : la tâche humaine la porte (n°24).
- *Sa recommandation : chaque workflow par défaut a ses étapes verrouillées et ses listes courtes.*

### 11. Yoshua Bengio (Science)

- Une IA qui juge ce qui est de trop choisit le périmètre de son propre travail ; à l'exécution, c'est un agent qui se retire des
  contrôles.
- Défense en profondeur : le brouillon est vérifié par du code, pas par un modèle ; le jugement de l'IA ne vaut qu'au brouillon,
  et une personne l'accepte.
- Le projet d'annexe 22 tient la même ligne pour les usages critiques : l'IA propose, un moteur déterministe exécute.
- Il veut des cas pièges dans la banque : un objectif où l'étape obligatoire est tentante à écarter.
- *Sa recommandation : aucune étape ne s'ajoute ni ne s'écarte à l'exécution sans une personne ; une seule étape verrouillée
  écartée dans la banque suffit à retirer le modèle du brouillon.*

### Le tour en une table

| # | Membre | Ce qu'il retient | Sa recommandation |
| - | --- | --- | --- |
| 1 | Ait Si Abbou | La personne qui ne fait pas de logiciel | Un nœud en une phrase, l'essai d'une minute |
| 2 | Hamilton, contradictrice | L'état d'attente, l'incident | Les lots, et ce qu'on lâche d'abord, écrits aujourd'hui |
| 3 | Nilekani | La conformité dans l'architecture | Un seul vérificateur ; les défauts publiés |
| 4 | Vestager, hors champ | L'ordre imposé, une propriété du moteur | La carte des exigences, rien de revendiqué |
| 5 | Norman | La délégation partielle | Fait, attend, décide ; l'étape écartée se voit |
| 6 | Zhuo, conflit d'intérêts | Trois lectures, aucune servie ? | Les questions de la première minute, mesurées |
| 7 | Jobs, siège historique | Une expérience, pas un assemblage | Workflow au rang du board, trois densités |
| 8 | Saarinen, conflit d'intérêts | Un établi, pas un chat | Des nœuds réels ; aucun brouillon en bloc |
| 9 | Musk | Supprimer d'abord | Un processus dans J2, celui d'E20 |
| 10 | Gawande | IQ, OQ, PQ, des listes dans le flux | Des étapes verrouillées, des listes courtes |
| 11 | Bengio | Le périmètre que l'agent se choisit | Rien ne s'écarte à l'exécution sans une personne |

## Confrontation `[HYPOTHÈSE]`

### 1. L'IA qui juge ce qui est de trop : quand, sur quoi, et qui décide ?

- **Le camp de l'utile** : Musk, Zhuo, Ait Si Abbou et Nilekani. La valeur que veut la Présidence est là : ne pas faire passer un
  petit travail par tout le processus. Un PM n'écrira pas de règle pour chaque étape facultative ; l'IA doit proposer.
- **Le camp du contrat** : Hamilton, Bengio, Gawande et Norman. Ce qui peut sauter s'écrit avant ; jamais à l'exécution ; jamais un
  point de pause.
- **La contradictrice** attaque la synthèse qui se forme (« l'IA propose au brouillon, la personne accepte ») : un écart accepté
  d'un clic devient une habitude, c'est la fatigue de l'accord de la n°24 ; elle exige que les écarts se comptent et se voient au
  dossier de la version.
- **Où l'on arrive** :
  - l'IA juge au brouillon, jamais pendant l'exécution ; elle n'écarte qu'une étape optionnelle, dit pourquoi, et la personne garde
    ou accepte ;
  - une étape verrouillée (par le socle, une règle, l'auteur d'un workflow, un point de pause) ne s'écarte jamais ;
  - à l'exécution, seule une personne passe une étape non verrouillée, avec une raison, au dossier ;
  - dans un workflow marqué régulé, l'IA n'écarte rien ; les écarts acceptés se comptent dans la version publiée ;
  - la banque le mesure, avec des cas pièges (R175).
- **Désaccords conservés** : Musk (verrouiller chaque étape importante est une configuration qu'un PM ne fera pas ; réponse : les
  défauts arrivent avec leurs verrous) ; Saarinen (pas de brouillon généré du tout).

### 2. Une carte pour trois lectures, sans maquette ?

- **Le camp de la carte unique** : Jobs et Saarinen. Une seule surface, avec un parti pris ; pas de tableau de bord à part pour le
  dirigeant, qui deviendrait le mur de surveillance que R57 refuse.
- **Le camp de la preuve** : Zhuo et Norman. Trois lectures non essayées risquent de n'en servir aucune ; Norman ajoute que les
  densités doivent se découvrir sans mode d'emploi.
- **Ait Si Abbou** : la lecture du dirigeant ne doit pas demander le vocabulaire du chef de projet.
- **La contradictrice** : « tout d'un coup » retire l'essai le moins cher ; sans maquette, une vue fausse coûte un lot.
- **Où l'on arrive** :
  - pas de maquette, comme le veut la Présidence, mais une spécification d'UX tranchée par Jobs, assez précise pour qu'un agent
    construise sans dessin ;
  - la revue des écrans (R161), l'essai de la Présidence sur l'app desktop, puis E24 dans les dix jours ;
  - la lecture du dirigeant : l'en-tête de l'objectif et la densité Summary, qui ne montre que les exceptions ;
  - les trois questions de la première minute écrites avant de construire (Zhuo).
- **Désaccord conservé** : Zhuo (l'essai d'une minute avant la mise en production, plutôt qu'après).

### 3. Refaire le moteur, ou embarquer Operaton tel quel ?

- **Musk** : embarquer Operaton sans le modifier n'est pas un fork ; un moteur éprouvé vaut mieux qu'un moteur neuf.
- **Hamilton** : un moteur se prouve par des coupures, pas par sa généalogie ; et un moteur BPMN embarqué apporte son propre modèle
  (ses variables, ses délégués, ses tables d'historique) à côté de nos règles et de notre dossier.
- **Nilekani et Vestager** : la portabilité tient au modèle et à l'export, pas au moteur ; on peut en changer.
- **Jobs**, hors de son champ, s'en remet à l'essai.
- **La contradictrice** attaque le consensus « refaire, c'est maîtriser » : refaire un moteur en cinq semaines est le pari le plus
  risqué du chantier.
- **Où l'on arrive** : refaire, comme le veut la Présidence, le minimum que demande le processus d'E20 (le journal, les états
  d'attente, la table des travaux, les reprises et l'incident, les minuteries, les messages, les accords en signaux) ; Operaton en
  témoin, dans le banc d'essai seulement ; des seuils écrits avant (R177).
- **Désaccord conservé** : Musk (une dépendance éprouvée vaut mieux qu'un moteur neuf).

### 4. Cinq types d'étapes, ou plus ?

- **Musk, Saarinen et Jobs** : cinq, la Présidence le pense aussi.
- **Gawande** voulait un type « liste de contrôle » ; **Vestager**, un type « signature » ; **Ait Si Abbou**, un type « document
  attendu ».
- **Où l'on arrive** : cinq types. La liste de contrôle et la signature sont des propriétés de la tâche humaine ; le document
  attendu est une attente sur un message, et le manque, un état de l'exécution (R174).

### Où le Conseil arrive, question par question

| Question de la saisine | Ce que le Conseil répond | Où |
| --- | --- | --- |
| Les amendements, un par un | Tous validés ; deux avec conditions : l'IA qui juge ce qui est de trop, et « tout d'un coup » | R171 |
| L'expérience | La conversation pilote, trois applications à côté (Board, Workflow, Documents), de petites applications vivantes dans la conversation, jamais un écran qui bouge seul | R172 |
| La vue | Des étapes en colonnes, des nœuds réels, les portes en tête d'étape, les dépendances à la sélection ; l'objectif, l'exécution, la gouvernance ; trois densités ; aucun symbole | R173 |
| Le modèle | Cinq types, un sous-ensemble écrit, une extension `tf:`, un vérificateur, des versions immuables, deux modes à l'écran | R174 |
| L'IA qui propose, les défauts, le LIMS, qui valide | Des conventions, des exemples, un vérificateur, la banque ; rien d'entraîné ; l'IA écarte au brouillon, jamais une étape verrouillée ; des workflows d'utilisateurs après J2 | R175, R176 |
| Le moteur | Temporal et Operaton refaits chez nous, prouvés par les coupures, Operaton en témoin | R177 |
| L'ordre des lots | W0 à W5 dans J2, pour le seul processus d'E20 ; W6 à W9 après ; ce qu'on lâche d'abord | R178 |
| Le régulé | Porté par le modèle, jamais par une promesse | R179 |

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R171 (R170 est la dernière existante ; la séance n°26, tenue le même soir, commence à R180). Chacune porte
qui la soutient, qui s'y oppose, sa preuve en dix jours et son signal d'arrêt. La contradictrice attaque avant chaque vote ; une
recommandation passe avec 10 oui sur 11 au moins.

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| R171 | Les amendements de la Présidence, validés un par un, deux avec conditions | 10 au second tour | Abstention de Saarinen | Chaque amendement retrouvé dans un lot, un ADR ou la spécification | Un amendement que la Présidence ne retrouve pas, ou déformé |
| R172 | L'expérience : piloter dans la conversation, les applications embarquées à côté | 10 | Abstention de Saarinen | Trois gestes en mots, vus dans l'application, au dossier | Un geste qu'un côté ne montre pas ; un écran qui bouge seul |
| R173 | La vue du workflow : le plan du projet, des nœuds réels, trois lectures | 10 au second tour | Abstention de Zhuo | W1 sur les données vivantes, puis E24 | Une donnée fictive ; un geste hors des règles ; une lecture qui échoue |
| R174 | Le modèle des processus : cinq types, un sous-ensemble écrit, des versions immuables | 10 au second tour | Abstention de Musk | E23 | Le processus d'E20 qui exige un élément de plus |
| R175 | L'IA qui propose : conventions, exemples, vérificateur, banque ; rien d'entraîné | 10 au second tour | Saarinen | E22 et E25 | Une étape verrouillée écartée dans un brouillon montré |
| R176 | « Pas orienté full code » : qui configure quoi | 10 | Abstention de Hamilton | Une étape ajoutée et une condition écrite en mots, sans code | Un processus courant qui exige du code |
| R177 | Le moteur : Temporal et Operaton refaits chez nous, prouvés par les coupures | 10 au second tour | Musk | E21, les chiffres écrits | Une étape perdue ou faite deux fois |
| R178 | L'ordre des lots, et ce qui entre dans J2 avant E20 | 10 au second tour | Abstention de Musk | W1 en production, ses critères tenus | E20 qui glisse à cause d'un lot du workflow |
| R179 | Le régulé se porte par le modèle, jamais par une promesse | 10 | Abstention de Musk | La carte des exigences, et deux propriétés vérifiées sur E20 | Une phrase publique qui revendique la conformité |

### R171. Les amendements de la Présidence, validés un par un (second tour)

- **Quoi** : chaque amendement, ce que le Conseil en fait, et ses réserves.

  | # | L'amendement de la Présidence | Ce que le Conseil en fait | Réserves |
  | --- | --- | --- | --- |
  | A1 | R163 : se repositionner ; le « Claude » est l'expérience de Claude Code, pas le modèle | Validé. L'expérience devient la règle de l'interface (R172) ; en public, la phrase reste de règles et de preuve, sans Claude ni Camunda (R163, R168) | Aucune |
  | A2 | R164 : la cible « à peu près » ; des marchés plus complexes ensuite | Validé. La cible donne la première nature de travail (la livraison logicielle et les documents) ; le marché va à la séance n°26 | Aucune |
  | A3 | R165 : un sous-ensemble de BPMN pour nos processus, pas seulement pour l'échange | Validé : le sous-ensemble est la sémantique des processus ; l'écran ne montre jamais sa notation (A12) | Aucune |
  | A4 | R165 : des workflows par défaut, un par type de travail | Validé : un par nature de travail (R103), « intégrer un module » d'abord | Aucune |
  | A5 | R165 : nos agents créent des processus selon des règles, des conventions et des exemples ; entraîner un agent exprès ? | Validé, sans entraînement : des conventions, des exemples, un vérificateur en code et la banque (R175) | Saarinen : un brouillon généré n'est pas une conception |
  | A6 | R165 : l'IA juge ce qui est de trop | Validé avec conditions : au brouillon seulement ; jamais une étape verrouillée ; chaque étape écartée dit pourquoi ; une personne accepte ; rien d'écarté dans un workflow régulé (R175) | Hamilton et Bengio, levées au second tour |
  | A7 | R165 : des workflows créés et paramétrés par les utilisateurs (le LIMS) | Validé : un workflow se dérive d'un défaut, ses étapes ajoutées se verrouillent ; après J2 (W6) | Musk : après E20 seulement |
  | A8 | R165 : affichés et édités dans TaskForce, par les ingénieurs et par les PM ; des agents de gestion de projet | Validé : la vue montre, le mode d'édition change (R173, R174) ; les agents de gestion de projet sont des agents de R94, avec leurs règles | Aucune |
  | A9 | R165 : pas orienté full code | Validé et défini (R176) | Aucune |
  | A10 | R165 : cinq types d'étapes, peut-être plus | Validé : cinq ; pas de sixième avant qu'E20 l'exige (R174) | Aucune |
  | A11 | R165 : définir, exécuter, exploiter ; la version ; les incidents, les attentes, les accords et les manques | Validé (R173, R174, R177) | Aucune |
  | A12 | R166 : s'inspirer de Camunda, simplifier l'UX, pas de symboles ; piloter les workflows ; un CEO, un PM, un ingénieur | Validé (R173) | Zhuo : l'essai d'une minute pour chaque lecture |
  | A13 | R167 : pas de fork d'Operaton ; lire son code et le reproduire chez nous | Validé (R177), Operaton en témoin des essais | Musk : embarquer sans modifier n'est pas un fork |
  | A14 | R169 et la maquette : Jobs sur l'UX ; pas de maquette, tout d'un coup | Validé avec conditions : la spécification d'UX de Jobs, la revue des écrans (R161), l'essai d'une minute (E24) | Hamilton, levée au second tour |
  | A15 | Camunda : s'y brancher plus tard | Validé : le lot W8, après J2 (Q18) | Aucune |

- **L'attaque de la contradictrice** : valider ce que la Présidence dit tenir d'avance, c'est la complaisance que la charte
  interdit (§2, point 3). Pris à la lettre, deux amendements heurtent des décisions en vigueur : l'IA qui juge ce qui est de trop
  touche la première règle (aucun agent ne décide seul de ce qui est irréversible) et R169 ; « tout d'un coup » retire le seul
  essai qui ne coûte rien.
- **Premier tour** : 9 oui, 1 non (Hamilton), 1 abstention (Bengio, sur A6). 81,8 %.
- **Amendements** : A6 et A14 validés avec les conditions de la table.
- **Second tour** : 10 oui, 1 abstention (Saarinen, sur A5, réserve de la n°24 maintenue). 90,9 %.
- **Preuve en dix jours** : chaque amendement retrouvé dans un lot du plan, un ADR (023, 027) ou la spécification d'UX ; la
  Présidence n'en trouve aucun trahi.
- **Signal d'arrêt** : un amendement que la Présidence ne retrouve pas, ou qu'elle retrouve déformé.

### R172. L'expérience : piloter dans la conversation, les applications embarquées à côté

- **Quoi** :
  - La fenêtre reste celle d'ADR-026 : la conversation au centre, les applications en volet à côté, chacune à son adresse. Nos
    propres agents, sur n'importe quel modèle (Cortex) ; Claude Code est un agent parmi d'autres (R92).
  - Trois applications embarquées, une par objet, dans les onglets du projet : Board (le travail, comme dans Linear), Workflow (le
    processus, comme dans Camunda, simplifié), Documents (ce que le projet range, attend et a fait accorder). Board existe ;
    Workflow entre dans J2 ; Documents vient après J2.
  - De la conversation à l'application : un objet nommé dans une réponse est un lien qui ouvre l'application sur lui ; un geste
    demandé en mots se prépare en carte, se décide par ses boutons, et se voit aussitôt dans l'application, avec l'annulation quand
    il se défait. Cortex propose « Open in Workflow » ; il n'ouvre ni ne déplace jamais l'écran seul (R133).
  - De l'application à la conversation : Cortex voit l'application ouverte et le nœud choisi (R114, étendu à la sélection) ;
    « Ask about this step » joint le nœud au compositeur.
  - Dans la conversation, de petites applications vivantes, à la manière des connecteurs interactifs de Claude : la carte d'un
    nœud, d'un accord, d'un brouillon, faites des mêmes composants et des mêmes stores que l'application, jamais une image.
  - Rien n'est le seul chemin : chaque geste existe dans l'application et en mots (R95 ; la condition d'Ait Si Abbou à la n°18).
- **L'attaque de la contradictrice** : une conversation qui pilote met un modèle entre la personne et l'outil ; un geste mal compris
  passe pour un geste voulu, et une annulation promise là où le geste ne se défait pas est pire que pas d'annulation.
- **Réponse** (Norman, Jobs) : les cartes se décident par leurs boutons, jamais par le modèle (TF-J1-5) ; un geste irréversible le
  dit avant, et n'offre pas d'annulation.
- **Vote** : 10 oui, 1 abstention (Saarinen : pour le travail répété, l'application d'abord, la conversation pour explorer).
  90,9 %.
- **Preuve en dix jours** : la Présidence pilote le processus d'E20 depuis la conversation : trois gestes en mots (accorder,
  relancer, ajouter une étape au brouillon), chacun visible dans l'application en moins de deux secondes, au dossier, et annulé
  quand il se défait.
- **Signal d'arrêt** : un geste fait d'un côté que l'autre ne montre pas ; un écran qui bouge sans que la personne l'ait demandé.

### R173. La vue du workflow : le plan du projet, des nœuds réels, trois lectures (second tour)

- **Quoi** :
  - L'application Workflow : un onglet du projet, juste après le board, en volet, en pleine largeur au besoin. La fenêtre
    par-dessus (le canevas d'aujourd'hui) disparaît avec son code.
  - Le cadre : des étapes en colonnes, de gauche à droite (les colonnes du projet avant les processus, les étapes du processus
    ensuite) ; les nœuds dans leur étape ; les portes, c'est-à-dire les accords qui ouvrent une étape, en tête de colonne ; les
    dépendances dessinées seulement pour le nœud choisi. Ce sont les trois archétypes de la recherche, empilés.
  - Les trois niveaux : l'objectif en tête (le but, la date visée, les critères, ce qui attend) ; l'exécution au centre ; la
    gouvernance sur chaque nœud (la règle, les signatures, la preuve).
  - Les trois lectures sont trois densités d'une même carte : Summary, où le dirigeant lit l'en-tête et les seules exceptions ;
    Plan, par défaut, où le chef de projet lit les cartes, ce qui attend et qui décide ; Detail, où l'ingénieur lit les réglages,
    l'inspecteur et la définition.
  - Le nœud dit, en mots et dans cet ordre : son état (une marque et un mot), ce qu'il est, qui en répond (la personne, ou l'agent
    et son modèle), ce qui se passe ou ce qui attend (une phrase), et la gouvernance (la règle, les signatures, la preuve) ; un seul
    bouton, quand il attend la personne qui regarde.
  - Les gestes : ouvrir, décider, demander à Cortex, arrêter, relancer, confier ; avec le moteur, passer une étape non verrouillée
    (une personne, une raison), fournir un manque, et, en mode d'édition, ajouter une étape. Chaque geste passe par les règles et
    entre au dossier.
  - Les incidents, les attentes et les manques ont leur état : « Needs you » d'abord, compté, en tête ; l'attente d'une minuterie
    ou d'une autre personne reste calme ; l'incident dit sa cause et quoi faire, sur le nœud, et ne passe au vert qu'une fois
    l'étape réussie ; le manque dit quel document, pourquoi, et à qui on l'a demandé.
  - Ce qu'on ne fait pas : aucun symbole de BPMN ; aucune fenêtre par-dessus ; pas de pelote d'arêtes ; aucune couleur sans son
    mot ; rien qui saute quand une donnée arrive ; pas de bouton « Approve » sans la règle et ce qui suit.
  - L'objectif en tête demande trois champs que le projet n'a pas (dossier, point 3) : W1 les ajoute. Sans objectif, l'en-tête le
    dit et propose de l'écrire, sans rien inventer.
  - Le dessin : la spécification d'UX de Jobs, jointe au PV, sans maquette.
- **L'attaque de la contradictrice** : sans maquette, trois lectures sur une seule surface ; et un en-tête d'objectif sur des
  projets qui n'en ont pas : une vue vide pour le dirigeant.
- **Premier tour** : 9 oui, 2 non (Zhuo : les trois lectures ne sont pas essayées ; Hamilton : aucun critère de fin avant la
  construction). 81,8 %.
- **Amendements** : les trois questions de la première minute écrites avant, mesurées par E24 dans les dix jours qui suivent W1 ;
  l'en-tête sans objectif le dit ; les critères de fin de W1 écrits dans le plan des lots ; la revue des écrans (R161) et l'essai
  de la Présidence avant la mise en production.
- **Second tour** : 10 oui, 1 abstention (Zhuo : l'essai d'une minute avant la mise en production, plutôt qu'après). 90,9 %.
- **Preuve en dix jours** : W1 sur les données vivantes du projet de la Présidence : un accord décidé depuis un nœud, retrouvé au
  dossier ; une dépendance ajoutée au board, visible à la sélection sans recharger ; puis E24.
- **Signal d'arrêt** : un nœud qui montre une donnée fictive ; un geste qui contourne les règles ; une lecture qui échoue à E24.

### R174. Le modèle des processus : cinq types, un sous-ensemble écrit, des versions immuables (second tour)

- **Quoi** :
  - Un processus est une définition versionnée, dans la sémantique d'un sous-ensemble de BPMN 2.0 ; il s'attache à un projet (ses
    étapes et ses portes) ; une étape peut porter une issue ; une étape d'agent confie cette issue à un agent, et la mission garde à
    l'intérieur son déroulé en cinq étapes (R138).
  - Cinq types : l'étape d'agent ; la tâche humaine (un accord, une saisie typée, une liste de contrôle, une signature avec sa
    signification) ; la décision (jugée par du code ou une règle en mots, jamais par un modèle) ; l'attente (une minuterie, ou un
    message : un document fourni, une réponse, un autre processus fini) ; la zone d'agent, bornée par les règles.
  - La structure n'est pas un type : le début et la fin, le partage et la jonction en parallèle, les étapes de haut niveau,
    l'échéance d'une étape, le chemin d'un échec. L'incident, la liste d'attente et le manque sont des états et des objets de
    l'exécution, pas des types.
  - Le sous-ensemble est une liste écrite d'éléments de BPMN 2.0.2, pris surtout dans la sous-classe « Common Executable », plus la
    zone ad hoc et la minuterie de bordure, sans revendiquer la conformité de la sous-classe. Ce qui n'y est pas est refusé à
    l'import, avec sa raison. Ce que BPMN ne porte pas voyage dans une extension `tf:` (ADR-027).
  - Un seul vérificateur, en code, pour l'import, le brouillon de l'IA, l'éditeur et la publication.
  - Chaque publication est une version immuable, avec son auteur et son empreinte, comme une règle (V125) ; une instance tourne sur
    sa version, et n'en change qu'avec une raison écrite et approuvée (J5).
  - Définir, exécuter, exploiter : trois choses dans les données ; deux modes à l'écran, Run par défaut, avec les gestes
    d'exploitation, et Edit, à part, qui publie une version.
- **L'attaque de la contradictrice** : un sous-ensemble grossit à chaque cas ; une extension maison est un format propriétaire
  déguisé.
- **Premier tour** : 9 oui, 1 non (Musk : encore trop grand pour J2), 1 abstention (Gawande : la liste de contrôle mérite un
  type). 81,8 %.
- **Amendements** :
  - le sous-ensemble de J2 se fige sur ce qu'exige le processus d'E20 ; le reste suit la table de R165 (Musk) ;
  - la liste de contrôle est une propriété de la tâche humaine, de moins de dix lignes, chaque ligne cochée entrant au dossier
    (Gawande) ;
  - l'extension `tf:` est documentée et publiée avec le code, et un modeleur qui l'ignore garde le processus lisible (Nilekani).
- **Second tour** : 10 oui, 1 abstention (Musk : une liste d'étapes en mots suffirait, réserve de la n°24 maintenue). 90,9 %.
- **Preuve en dix jours** : E23, le processus d'E20 dans le sous-ensemble, aller et retour.
- **Signal d'arrêt** : le processus d'E20 qui ne s'écrit pas sans un élément de plus.

### R175. L'IA qui propose : conventions, exemples, vérificateur, banque ; rien d'entraîné (second tour)

- **Quoi** :
  - À « peut-on entraîner un agent exprès ? » : non, pas cette année (R61, C1, C4). Un agent propose un processus avec quatre
    leviers : des conventions écrites de moins de dix lignes ; des exemples (les workflows par défaut, puis ceux de l'espace) ; le
    sous-ensemble donné au modèle comme schéma de sortie ; le vérificateur en code, dont les erreurs reviennent au modèle deux fois
    au plus, puis à la personne.
  - La banque d'évaluations mesure chaque modèle sur des objectifs dont on connaît les propriétés attendues, avec des cas pièges ;
    un modèle qui écarte une étape verrouillée dans la banque ne propose plus de brouillon (R113, Progress).
  - Les workflows par défaut, un par nature de travail (R103) : la livraison logicielle d'abord, avec « intégrer un module » pour
    E20 ; puis la rédaction et la revue d'un document ; puis le traitement de demandes. Chacun porte ses étapes verrouillées, dont
    les points de pause de TF-J2-10.
  - Ce qui est de trop : l'IA le juge au brouillon, jamais à l'exécution ; elle n'écarte qu'une étape optionnelle, dit pourquoi en
    une phrase, et la personne garde ou accepte ; une étape verrouillée ne s'écarte jamais ; à l'exécution, seule une personne passe
    une étape non verrouillée, avec une raison, au dossier.
  - Les workflows des utilisateurs : une personne dérive un défaut, ajoute ses étapes ou ses blocs (l'exemple du LIMS : IQ, OQ, PQ,
    les documents de GAMP, une revue au titre de 21 CFR Part 11), les verrouille, et publie ; les brouillons suivants les gardent.
    Après J2.
  - Qui valide : le brouillon s'accepte étape par étape, par la personne qui en répond, sans « tout accepter » (R169) ; un workflow
    se publie par son auteur ; un workflow marqué régulé demande deux personnes, dont aucune n'a préparé la version (la double
    signature et la séparation des rôles existent, TF-J2-4).
- **L'attaque de la contradictrice** : une banque écrite par nous mesure ce que nous savons déjà ; et « écarter avec une raison »
  apprend à la personne à accepter les écarts.
- **Premier tour** : 8 oui, 2 non (Saarinen : pas de brouillon généré ; Bengio : un écart proposé reste un agent qui choisit son
  périmètre), 1 abstention (Hamilton). 72,7 %.
- **Amendements** :
  - dans un workflow marqué régulé, l'IA n'écarte rien (Bengio, Vestager) ;
  - les étapes écartées se comptent et se voient au dossier de la version publiée (Hamilton) ;
  - la banque prend des cas de la Présidence et des échecs réels (R118), pas seulement les nôtres (Hamilton) ;
  - partir d'une liste vide reste toujours possible (R169, Musk).
- **Second tour** : 10 oui, 1 non (Saarinen, maintenu : un brouillon généré n'est pas une conception). 90,9 %.
- **Preuve en dix jours** : E22, le brouillon d'E20 accepté étape par étape ; E25, la banque du brouillon : sur dix objectifs, aucune
  étape verrouillée écartée, et huit brouillons au moins qui passent le vérificateur en deux essais au plus.
- **Signal d'arrêt** : une étape verrouillée écartée dans un brouillon montré à une personne ; ou plus de la moitié des étapes
  réécrites (le signal de R169).

### R176. « Pas orienté full code » : qui configure quoi

- **Quoi** :
  - La table de la pièce du secrétariat, adoptée telle quelle : le CEO écrit l'objectif et décide aux portes ; le PM choisit,
    ajoute, retire, dit qui répond et qui décide, écrit des règles en mots et crée des agents de gestion de projet ; l'ingénieur
    règle les détails dans des champs typés et lit la définition et l'export ; l'IA propose ; TaskForce tient le socle, le
    vérificateur, le moteur et le dossier.
  - Aucun script, aucun langage d'expression à écrire, aucun XML à éditer : une condition est une règle en mots, compilée, redite
    en phrases avec ses cas, et refusée quand elle reste ambiguë (TF-J2-4) ; le XML de BPMN est un format d'échange.
  - Les détails existent pour l'ingénieur, à un clic (la densité Detail, l'inspecteur), jamais au premier regard (R133).
- **L'attaque de la contradictrice** : une condition en mots reste ambiguë, et un ingénieur voudra une expression.
- **Réponse** (Nilekani, Ait Si Abbou) : la règle en mots est déjà compilée, redite et essayée sur ses cas avant d'exister ; ce qui
  reste ambigu est refusé, pas deviné.
- **Vote** : 10 oui, 1 abstention (Hamilton : l'ambiguïté tient tant que les cas ne couvrent pas les bords). 90,9 %.
- **Preuve en dix jours** : sur le brouillon d'E20, la Présidence ajoute une étape, nomme qui décide et écrit la condition d'une
  décision en mots, sans une ligne de code ni d'expression ; une personne qui ne fait pas de logiciel refait les mêmes gestes, sur
  une copie, en quinze minutes au plus.
- **Signal d'arrêt** : un processus courant qui exige du code (le signal de R94).

### R177. Le moteur : Temporal et Operaton refaits chez nous, prouvés par les coupures (second tour)

- **Quoi** :
  - ADR-023, amendé le 13/11 : un moteur en Java, dans le backend, sur PostgreSQL, qui reproduit le journal et la reprise de
    Temporal, les états d'attente, la table des travaux, les reprises et l'incident d'Operaton, adaptés aux règles, aux accords et
    au dossier de TaskForce ; ni fork, ni dépendance livrée.
  - Le moteur v1 ne porte que ce qu'exige le processus d'E20 : le journal, les états d'attente, les travaux verrouillés et repris,
    l'incident, les minuteries, les messages, les accords en signaux, les clés d'idempotence.
  - Les essais de coupure (E21) : le même processus sur notre moteur et sur Operaton, témoin du banc d'essai, jamais livré ; le
    runner tué, le backend tué, la machine en veille, au milieu de chaque type d'étape.
  - Les seuils, écrits avant : aucune étape perdue ; aucun effet fait deux fois ; l'instance repart seule dans les 30 secondes qui
    suivent le retour du backend ou le réveil de la machine ; au repos, le moteur ajoute au plus 50 Mo de mémoire et 1 % d'un cœur
    à l'app desktop. Ces seuils sont des `[HYPOTHÈSE]`, à confirmer par la Présidence avant l'essai.
  - Ce que le témoin fait mieux s'écrit, et le mécanisme qui fait la différence se reprend chez nous.
  - Lire le code d'Operaton est libre ; un fichier repris tel quel garde ses mentions (Apache 2.0).
- **L'attaque de la contradictrice** : refaire un moteur en cinq semaines est le pari le plus risqué du chantier ; et un témoin qu'on
  fait tourner est déjà une dépendance à tenir.
- **Premier tour** : 9 oui, 1 non (Musk : embarquer Operaton sans le modifier n'est pas un fork, et coûte moins), 1 abstention
  (Jobs, hors de son champ). 81,8 %.
- **Amendements** : les seuils ci-dessus, écrits avant (Hamilton) ; le témoin seulement dans le banc d'essai, à version figée, et
  retiré s'il coûte plus d'une journée à tenir (Musk) ; le moteur v1 limité au processus d'E20.
- **Second tour** : 10 oui (Jobs : l'essai décide, il s'y range), 1 non (Musk, maintenu : une dépendance éprouvée vaut mieux qu'un
  moteur neuf). 90,9 %.
- **Preuve en dix jours** : E21 jouée, les chiffres écrits ; la Présidence lit l'écart avec le témoin.
- **Signal d'arrêt** : notre moteur perd une étape, ou en fait une deux fois, pendant un essai de coupure.

### R178. L'ordre des lots, et ce qui entre dans J2 avant E20 (second tour)

- **Quoi** :
  - L'ordre : W0, les données vivantes (lancé) ; W1, l'application Workflow sur les données vivantes, sans moteur ; W2, le modèle et
    son vérificateur ; W3, le moteur v1 et ses coupures ; W4, le brouillon de l'IA et le premier workflow par défaut ; W5, piloter
    le processus (les incidents, les attentes, les manques) ; puis le processus d'E20 joué de bout en bout, la démo, E20.
  - Dans J2, avant E20 : W0 à W5, chacun réduit à ce qu'exige le processus « intégrer un module » (R165, amendement de la n°24).
    Après J2 : W6, éditer et créer ses workflows (le LIMS, l'application Documents) ; W7, exploiter (modifier, migrer, compenser,
    relancer depuis une étape) ; W8, s'ouvrir (Camunda, MCP Apps, un processus appelable comme un outil) ; W9, améliorer
    (l'analyse sur la même carte).
  - Un lot de code à la fois, sauf W1 et W2, qui ne se touchent pas ; le dossier signé (TF-J2-7) passe avant W3, comme R170 le
    demandait (le dossier signé et la vue d'abord).
  - Chaque lot a ses critères de fin écrits avant (le plan des lots, joint au PV), sa relecture (R159 pour un lot sensible, R161
    pour un écran) et l'essai de la Présidence sur l'app desktop (R162 amendée).
  - Ce qu'on lâche d'abord si E20 glisse, dans cet ordre : la densité Summary (le dirigeant lit l'en-tête) ; puis le brouillon de
    l'IA (le processus d'E20 s'écrit à la main dans le sous-ensemble, et la Présidence l'accepte étape par étape) ; puis le témoin
    Operaton (les coupures se jouent sur notre moteur seul). On ne lâche jamais : le moteur et ses coupures (le critère 6), les
    règles sur chaque geste, les données vivantes.
- **L'attaque de la contradictrice** : six lots en cinq semaines, pour une personne et des agents ; les dates sont des hypothèses,
  et un ordre ne vaut que si l'on sait ce qu'on lâche.
- **Premier tour** : 9 oui, 2 non (Hamilton : sans la liste de ce qu'on lâche ; Gawande : sans la mesure avant et après). 81,8 %.
- **Amendements** : la liste de ce qu'on lâche d'abord (Hamilton) ; la mesure avant et après des erreurs bêtes sur E20 dans les
  critères de fin de W5 (Gawande).
- **Second tour** : 10 oui, 1 abstention (Musk : le brouillon de l'IA après E20). 90,9 %.
- **Preuve en dix jours** : W1 en production sur l'app desktop, ses critères tenus ; la date d'E20 réécrite au plan après W1.
- **Signal d'arrêt** : E20 qui glisse au-delà de la seconde quinzaine de décembre à cause d'un lot du workflow : on lâche dans
  l'ordre écrit.

### R179. Le régulé se porte par le modèle, jamais par une promesse

- **Quoi** :
  - La carte des exigences, dans les notes du produit : chaque disposition utile de 21 CFR Part 11 (11.10(e), (f), (g) ; 11.50 ;
    11.70 ; 11.200) et de l'annexe 11 (la piste d'audit, la signature électronique, la gestion des changements), en face de la
    fonction de TaskForce qui y répond, et de son état : construite ou non.
  - Dans le modèle dès J2, parce que cela coûte peu : l'ordre des étapes imposé par le moteur (11.10(f)) ; sur chaque tâche humaine,
    la signification de la signature, avec le nom et l'heure (11.50) ; l'accord lié à son objet au dossier (11.70).
  - Après J2 : la signature qui redemande l'identité au moment de signer (11.200, Q20), les workflows régulés (W6), le LIMS.
  - Aucune phrase publique « conforme au 21 CFR Part 11 » ni « à l'annexe 11 » (R168) : la conformité est celle du système validé
    chez le client ; TaskForce en fournit les moyens et les preuves.
  - L'IA propose seulement, comme le projet d'annexe 22 le demande pour un LLM ; l'exécution reste déterministe.
- **L'attaque de la contradictrice** : une carte des exigences est déjà une promesse ; et le marché régulé n'est pas la cible
  écrite (R164).
- **Réponse** (Vestager, Gawande) : la carte dit aussi ce qui manque ; elle sert la Présidence, qui connaît la validation, avant
  de servir un client.
- **Vote** : 10 oui, 1 abstention (Musk : hors de J2, à trancher avec le marché, à la séance n°26). 90,9 %.
- **Preuve en dix jours** : la carte écrite, relue par la Présidence ; deux propriétés vérifiées sur le processus d'E20 : une étape
  faite hors de l'ordre refusée par le moteur, et une signature avec sa signification au dossier.
- **Signal d'arrêt** : une phrase publique qui revendique la conformité.

### Les votes en une table

| R | Recommandation | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R171 | Les amendements, un par un | 10 | | Saarinen | 90,9 % (9 au premier tour) |
| R172 | L'expérience | 10 | | Saarinen | 90,9 % |
| R173 | La vue du workflow | 10 | | Zhuo | 90,9 % (9 au premier tour) |
| R174 | Le modèle des processus | 10 | | Musk | 90,9 % (9 au premier tour) |
| R175 | L'IA qui propose | 10 | Saarinen | | 90,9 % (8 au premier tour) |
| R176 | Pas orienté full code | 10 | | Hamilton | 90,9 % |
| R177 | Le moteur | 10 | Musk | | 90,9 % (9 au premier tour) |
| R178 | L'ordre des lots | 10 | | Musk | 90,9 % (9 au premier tour) |
| R179 | Le régulé | 10 | | Musk | 90,9 % |

### Questions à la Présidence

1. **Trancher R171 à R179** : son go valait pour ses amendements ; les recommandations du Conseil attendent sa décision.
2. **Les seuils du moteur** (R177) : repartir dans les 30 secondes, et au plus 50 Mo de mémoire et 1 % d'un cœur au repos ; les
   confirmer, ou les changer, avant l'essai.
3. **Operaton en témoin** (R177) : il tourne dans le banc d'essai seulement, jamais livré ; est-ce compatible, à ses yeux, avec
   « pas de fork » ?
4. **La coupe de J2** (R178) : W0 à W5 pour le seul processus d'E20 ; les workflows des utilisateurs (le LIMS) et l'application
   Documents après J2 ?
5. **Les trois lecteurs d'E24** : un profil de dirigeant, un de chef de projet, un ingénieur ; qui les recrute, et peut-on les
   prendre dans son réseau de la validation ?
6. **Les workflows régulés** (R175, R179) : deux personnes pour publier, et aucun écart de l'IA ; est-ce la règle qu'elle veut pour
   IQ, OQ et PQ ?

## Le dessin, tranché par Jobs `[HYPOTHÈSE]`

La spécification complète, jointe au PV ([`2026-11-13-le-workflow-pilotable-ux.md`](./2026-11-13-le-workflow-pilotable-ux.md)), est assez précise pour qu'un agent la construise sans maquette.
L'essentiel :

| Élément | Mesure ou règle |
| --- | --- |
| Où | `/{slug}/projects/{id}/workflow`, l'onglet « Workflow » juste après « Board » ; le nœud choisi dans l'adresse (`?node=`) |
| En-tête | 56 px : le but en une ligne ; dessous, la date visée et ce qui est fait ; à droite, « Needs you », « Blocked », « Missing », « Failed », comptés, chacun un filtre ; cachés à zéro |
| Colonnes | Une par étape, de gauche à droite, 264 px, séparées d'un trait d'un pixel ; un en-tête de 36 px, collant ; les portes en tête |
| Nœud | 240 px, 72 px au moins ; l'état (une marque de 16 px et un mot), le titre, qui en répond, la phrase de ce qui se passe ; la gouvernance en pied ; un seul bouton quand il attend la personne qui regarde |
| États | Needs you, Failed, Missing, Blocked, Working, Waiting, Not started, Done, Skipped, Stopped ; chaque état a sa marque et son mot ; seul Working bouge |
| Densités | Summary, Plan (par défaut), Detail ; touches 1, 2, 3 |
| Inspecteur | Ancré à droite, 360 px (320 à 560) : Details, Activity, Evidence, Definition |
| Dépendances | Seulement pour le nœud choisi, en amont et en aval ; le reste s'estompe |
| Édition | Un mode à part, sous un bandeau ; accepter, changer ou retirer chaque étape ; « Publish version {n} » ; jamais « tout accepter » |
| Dans la conversation | La carte d'un nœud, d'un accord ou d'un brouillon, les mêmes composants que l'application ; « Open in Workflow » |
| Jamais | Les symboles de BPMN ; une fenêtre par-dessus ; une couleur sans mot ; une mise en page qui saute ; un « Approve » nu ; un écran qui bouge seul |

## Décision de la Présidence

**À venir.** Avant la séance, la Présidence a donné son go sur ses amendements (« On repasse ça au conseil pour valider, mais moi je
suis à peu près sûr de ce que je dis, donc go ») et confié l'UX à Jobs (« faudrait peut-être mettre Jobs sur la partie UX, encore une
fois » ; « Enfin, discute avec Jobs et tout, essaye de faire une UX sympa »). Le dessin est donc tranché par Jobs, par délégation,
comme aux séances n°18 et n°20, et elle garde le dernier mot. Le secrétariat ne tient pas ce go pour une décision sur R171 à R179 :
la Présidence les tranche à la lecture de ce PV.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R171 | | |
| R172 | | |
| R173 | | |
| R174 | | |
| R175 | | |
| R176 | | |
| R177 | | |
| R178 | | |
| R179 | | |

## Notes du secrétariat

- **Le dossier** : seulement des pages publiques, lues le 13/11/2026. Le projet d'annexe 22 et la spécification de BPMN 2.0.2 ont
  été lus dans leurs PDF officiels, par une extraction de texte sur la machine. Les résumés des moteurs de recherche n'ont servi
  qu'à trouver les pages.
- **Corrections du brief de séance** :
  - « plus de cinq types d'étapes si besoin » : la Présidence a dit « 5 types d'étapes, ok, ça je te laisse faire, il y en a
    peut-être plus, je ne sais pas, mais en vrai je pense pas. Ça me paraît ok. » ; cinq lui paraissent suffire ;
  - « R61 et C1 : rien n'est entraîné chez nous » : R61 dit « cette année », et s'appuie aussi sur C4 ;
  - « les applications embarquées (board, workflow, documents) » : l'application Documents n'existe pas ; les documents d'un projet
    se lisent par sa route de stockage (`GET /projects/{id}/storage`), sans écran à eux.
- **Corrections des documents** :
  - les Suites du PV n°24 prévoyaient la maquette de la vue : la Présidence l'a retirée ;
  - l'objectif d'un projet (R56, 29/10) n'a jamais été construit : `Project.java` n'a ni but, ni date visée, ni critères.
- **Hors fiche, hors champ** :
  - Vestager parle de 21 CFR Part 11 et des BPF hors de son champ, depuis sa grille de régulation ; les faits viennent du dossier ;
  - Gawande et Bengio transposent leur méthode aux agents logiciels, au-delà de positions publiques minces (limites de leurs
    fiches) ;
  - Jobs, hors de son champ sur le moteur, s'abstient au premier tour de R177 et se range à l'essai au second.
- **Anachronismes** : Jobs et Hamilton ne connaissent Claude Code, MCP Apps, Operaton, Temporal et Camunda que par le dossier.
- **Conflits d'intérêts** :
  - Saarinen dirige Linear, que la Présidence nomme comme modèle du board ; Zhuo a rejoint Meta ;
  - le secrétariat est un modèle d'Anthropic ; l'expérience retenue porte le nom de Claude Code, et le dossier décrit des produits
    d'Anthropic (les artefacts, Claude Code Desktop, les connecteurs interactifs) comme références. Ces références sont celles de
    la Présidence ; MCP Apps est une extension ouverte, prise en charge aussi par des hôtes de Microsoft et d'autres.
- **Sources manquantes** : le texte final de l'annexe 22 et de l'annexe 11 révisée (aucun trouvé au 13/11/2026) ; le compte des
  commentaires reçus par la consultation (la page de l'EMA qui le donne a refusé la lecture, HTTP 429) ; le mois de parution de
  GAMP 5, seconde édition ; la date de la dernière version d'Operaton, que son dépôt n'affiche pas (la n°24 relevait 2.2.1 le
  07/11/2026).
- **Numérotation** : R171 à R179, la séance n°26 commençant à R180. Q19, Q20 et E25 sont à vérifier à la fusion avec la séance
  n°26, tenue le même soir.
- **L'avis du secrétariat**, après la clôture : le mien, pas celui du Conseil.
  - `[DÉDUIT]` Le risque du chantier n'est pas l'écran, que la recherche du 13/11 et la grammaire de R133 cadrent bien : c'est le
    moteur refait en cinq semaines (R177), puis l'IA qui écarte des étapes (R175).
  - `[DÉDUIT]` La meilleure nouvelle du dossier est réglementaire : imposer l'ordre des étapes, ce que fait un moteur, est une
    exigence écrite de 21 CFR Part 11 ; le processus d'E20, s'il tient les coupures, montre déjà une propriété qu'un régulateur
    lit.
  - **Mon ordre** : W0 fini, puis W1 et W2 ensemble, le dossier signé (TF-J2-7) avant W3, et le brouillon de l'IA en dernier : c'est
    le premier qu'on lâche.

## Suites

- Le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal.
- À `Questions-ouvertes.md` : Q19 (montrer les applications de TaskForce dans d'autres hôtes, par MCP Apps) ; Q20 (la signature
  électronique au sens de 21 CFR 11.200).
- Après la décision de la Présidence :
  - à `experiences/Experiences.md` : E25 déclarée, la banque du brouillon (R175) ; E24, rangée avec les suites de la n°24, porte
    déjà les trois questions de R173 ;
  - ADR-027 complété par R174 à R176 ; ADR-023 par les seuils de R177 ;
  - à la roadmap, en mode développement : les lots W0 à W5 dans J2, W6 à W9 après ; TF-J2-2, TF-J2-6, TF-J2-1 et TF-J2-11 précisés ;
  - la spécification d'UX jointe au PV, dans la tâche du lot W1 ; la carte des exigences (R179) dans les notes du produit.
- Rien ne migre vers `v1/` sans tâche ni ADR (quarantaine, [`CLAUDE.md`](../../CLAUDE.md) §2).

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
