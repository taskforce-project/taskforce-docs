---
id: conseil-seance-2026-11-13-depasser-camunda
title: "Conseil d'Avenir : séance du 13/11/2026"
doc_type: pv-seance
statut: active
date: "13/11/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, camunda, bpmn, processus, workflow, positionnement, concurrence]
related:
  - "../README.md"
  - "./2026-11-12-revue-de-j2.md"
  - "./2026-11-11-se-brancher-a-l-entreprise.md"
  - "./2026-11-01-feuille-de-route.md"
  - "./2026-10-31-souverainete-operationnelle.md"
  - "../../decisions/ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "../../decisions/ADR-023-DRAFT-execution-durable-postgresql.md"
  - "../../decisions/ADR-027-DRAFT-modele-des-processus.md"
  - "./2026-11-13-le-workflow-pilotable.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance du 13/11/2026 : dépasser Camunda

> Simulation : les membres sont des personnages simulés, à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **En bref.** Camunda ne fait pas « exactement » ce que TaskForce veut faire. Il exécute des processus BPMN à grande échelle
> pour les grandes organisations, avec près de 200 M$ de revenu récurrent, et y met des agents IA depuis 10/2025. TaskForce
> délègue du travail à des agents sous des règles, avec une preuve, et n'a encore aucun processus. En produit livré, la distance
> est entière ; en intention, les deux se recouvrent. Le Conseil recommande de prendre à Camunda sa rigueur d'exécution, par un
> sous-ensemble de BPMN réservé à l'échange et un modèle d'interface refait, de n'affirmer « au-dessus » que ce qui est prouvé,
> et de refuser les deux cadres proposés. Le concurrent n°1 n'est pas tranché : sur la cible écrite, Microsoft et n8n sont plus
> proches que Camunda. Huit recommandations, R163 à R170, toutes à 90 % au moins, quatre au second tour. Gwynne Shotwell,
> contradictrice, a obtenu que rien de Camunda n'entre dans J2 s'il ne sert pas le processus d'E20.
>
> **Le soir même**, la Présidence les retient toutes, avec ses amendements : se repositionner sur l'expérience de Claude Code,
> où l'on pilote, plus des applications embarquées ; un sous-ensemble de BPMN qui sert aussi à afficher et à éditer nos
> processus, des workflows par défaut, et l'IA qui juge ce qui est de trop ; une vue inspirée de Camunda, sans ses symboles et
> sans maquette préalable ; un moteur refait chez nous, sans fork d'Operaton. Elle repasse le chantier au Conseil (séance n°25).

- **Saisine** (Présidence, 13/11/2026, en conversation, mot pour mot) :
  - « Oula la, c'est moi ou Camunda font exactement ce qu'on souhaite faire ??? Fais analyser ca par le conseil stp. On en est
    proche a quelle point ? Nous c'est une sorte de Claude x Camunda right ? » ;
  - « Alright, avec ce que t'as recuperer de tes agents, j'aimerais reunir a nouveau le conseil, pour pouvoir concurrencer
    Camuda, donc aspirer ce qu il fait de mieux, et nous on step up au dessus de camunda » ;
  - « je pense que c'est notre concurrent n1 en fait, apres je les vois pas dans des entreprises et des uses cases hyper
    specifique cote industrie ou autre mais bon peut etre que si, jsp a quel point ils ont pris le marche ».
  - **Le contexte** : le même jour, la Présidence juge « horrible » la vue du workflow de TaskForce. Elle veut « suivre un projet
    complet via workflow, style blueprint presque », les choix accessibles dessus, les ressources et les liens, « comme si on
    pouvait piloter le truc via workflow », intégré comme le board, pas dans une fenêtre par-dessus. La maquette attend la séance.
  - **Une pièce apportée** : une analyse rédigée par un assistant d'IA, collée par la Présidence ; ses thèses sont discutées comme
    tout apport extérieur, et ses affirmations sur Camunda restent des `[HYPOTHÈSE]` tant qu'une source ne les établit pas.
  - **Les questions à trancher** : ce que fait Camunda, sur les faits, et ses voisins ; ce qu'il fait de mieux et que TaskForce
    doit prendre, et comment ; où TaskForce va au-dessus, et ce qui reste à construire avant de l'affirmer ; à quel point nous
    en sommes proches ; le cadre (« Claude x Camunda », ou celui de la pièce) ; ce que cela change pour la vue du workflow,
    TF-J2-2, ADR-023, le pitch et E20 ; les preuves en dix jours. Et, sur le troisième message : jusqu'où Camunda a pris le
    marché, sa place dans les secteurs régulés ou très spécifiques, et s'il est vraiment le concurrent n°1 sur la cible de
    TaskForce.
  - **Horizon** : J2 et E20, le premier client joué de bout en bout à la fin de J2, puis la release majeure.
- **Formation** : séance n°24, plénière (24), parce que c'est une question de positionnement (charte, §5).
  - Impulsion : Steve Jobs, Elon Musk, Jeff Bezos, Gwynne Shotwell.
  - Pont : Satya Nadella, Mariana Mazzucato, Arati Prabhakar, Kenza Ait Si Abbou.
  - Harmonie : Margrethe Vestager, Audrey Azoulay, Nandan Nilekani, Tristan Harris, Yuval Noah Harari.
  - Science : Yoshua Bengio, Yann LeCun, Fei-Fei Li, Margaret Hamilton, Daniela Rus, Jennifer Doudna, Esther Duflo, Atul Gawande.
  - Design : Don Norman, Julie Zhuo, Karri Saarinen.
  - **Contradictrice** : Gwynne Shotwell. Elle n'a jamais tenu ce rôle. Son angle, l'exploitation (la cadence, les autorisations,
    les données d'essai), est le mieux placé pour attaquer le consensus « prendre le meilleur et passer au-dessus » sur ce que
    coûte l'exploitation d'un moteur de processus pour des entreprises, et sur une échéance annoncée comme certaine. Musk
    l'était à la n°23.
  - **Ordre de parole**, tiré au sort le 13/11/2026 à 16:24 UTC (`shuf`) : Esther Duflo, Audrey Azoulay, Fei-Fei Li, Daniela
    Rus, Satya Nadella, Yoshua Bengio, Margaret Hamilton, Yann LeCun, Arati Prabhakar, Nandan Nilekani, Jeff Bezos, Kenza Ait Si
    Abbou, Steve Jobs, Mariana Mazzucato, Jennifer Doudna, Don Norman, Yuval Noah Harari, Elon Musk, Gwynne Shotwell, Atul
    Gawande, Julie Zhuo, Karri Saarinen, Tristan Harris, Margrethe Vestager.
  - **Règle de vote** (charte §6.5) : 90 % des présents, soit 22 oui sur 24 au moins.
- **Fiches** : aucune fiche rafraîchie. Toutes ont moins de 30 jours au 13/11/2026 : la plus ancienne date du 21/10/2026, soit 23
  jours ; Norman, Zhuo et Saarinen datent du 28/10, Ait Si Abbou du 26/10, les vingt autres du 21/10. Jobs et Hamilton, sièges
  historiques, ne se rafraîchissent que sur une nouvelle source historique ; aucune n'est apparue.

## Dossier

Constitué le 13/11/2026 par le secrétariat. Sur Camunda, seulement ses pages publiques (camunda.com, docs.camunda.io, son blog,
ses communiqués, ses dépôts GitHub et leurs licences), lues ce jour ; sur ses voisins, leurs pages officielles, relevées ce jour
par un agent de recherche du secrétariat, sans connexion ni formulaire ; sur TaskForce, `taskforce-docs` (`feature/lean-oss`,
`a133d42`) et le code de `dev`. La saisine demandant un état complet, le dossier compte dix points.

1. `[ÉTABLI]` **TaskForce en production** (1.16.0 et desktop 1.13.0, release #533, note ▶ du 13/11 de la roadmap).
   - L'app desktop : une coque Electron qui embarque un JDK 21 pour le backend Java, PostgreSQL 18 avec pgvector et le runner
     (`desktop/README.md`) ; la webapp reçoit chaque release, on n'y teste rien (R91).
   - Cortex sur n'importe quel modèle : Ollama sur la machine, toute API compatible OpenAI, l'API d'Anthropic (TF-J1-2).
   - Les missions de code : Claude Code par le runner local, sous les règles rejugées à chaque action, avec les changements sous
     les yeux et la remise (TF-J1-16, TF-J1-17). GitHub Copilot, lui, est l'agent cloud de GitHub, lancé par l'API des tâches
     d'agent de GitHub, qui revient en pull request (`GitHubCopilotProvider.java`).
   - Les règles de l'entreprise par couches au-dessus d'un socle, un seul moteur en Java compilé en JavaScript pour le runner,
     chaque version immuable avec son auteur et son empreinte (TF-J2-4, V125, ADR-025) ; les accords, avec qui accorde, la double
     signature, la séparation des rôles et le seuil.
   - Le dossier de chaque action : chaîné, scellé, écrit avant l'effet, exporté, vérifié par le runner ; pas signé (Backend.md).
   - 104 préréglages d'outils (102 serveurs MCP, plus Google Drive et Microsoft 365 par leurs API), une connexion par personne, la
     lecture par défaut ; aucun encore essayé de bout en bout sur de vrais comptes (TF-J2-12, TF-J2-13). Les fichiers de
     l'entreprise lus en direct et rangés où elle le choisit (TF-J2-5, TF-J2-14). La licence AGPL v3.
2. `[ÉTABLI]` **Ce qui n'existe pas** (roadmap, J2) :
   - les processus (TF-J2-2 : « un canevas modifiable, cinq types d'étapes, exécuté par le moteur durable v1 ») et le moteur
     durable (ADR-023) : une mission avance quand on la lit ;
   - la vue du travail v1 (TF-J2-6). Le canevas d'aujourd'hui, en lecture seule, montre un nœud par analyse et des arêtes vers les
     agents, sans issue, dépendance, accord ni fichier ; il ne s'ouvre qu'en dialogue, depuis la carte des missions ;
   - le dossier signé et vérifié hors de TaskForce (TF-J2-7), les packs (TF-J2-8), la boucle d'agent de TaskForce sur n'importe
     quel modèle (TF-J2-3) ;
   - au 13/11, les critères de sortie 6 (le processus « intégrer un module », repris après un redémarrage) et 7 (le dossier
     signé vérifié hors de TaskForce) ne sont pas commencés.
3. `[ÉTABLI]` **Ce que la vue demandée exige**, d'après la carte du code de `origin/dev` au 13/11 :
   - elle s'insère comme le board : une route du projet, une entrée dans ses onglets, les mêmes points d'entrée, le temps réel du
     projet ; un accord peut se décider depuis un nœud avec la route existante ;
   - les manques, par ordre de blocage : les dépendances entre issues lisibles par projet ; un flux du projet pour les missions et
     leurs accords ; un fil d'événements par projet ; un modèle d'étapes (d'abord les colonnes et les cycles) ; l'exécution
     durable, qui bloque l'exécution des processus, pas leur vue.
4. `[ÉTABLI]` **Les décisions en vigueur.**
   - R5' : « Vous décrivez le résultat ; TaskForce le fait faire par l'agent de votre choix, avec vos outils et vos règles, et
     vous montre qu'il est bon. » Ce que TaskForce n'est pas : un modèle d'IA, un cabinet qui écrit les règles d'un métier, un
     tableau de surveillance des agents (R57), le client d'un seul fournisseur de modèles, d'abord un service en ligne.
   - L'image « n8n IA » (n°15) : une image de travail ; la différence doit se dire en une phrase qui ne parle que de règles et de
     preuve, à tester par E14, jamais menée.
   - R94 et ADR-022 : huit briques, dont « les processus, sur un canevas modifiable » ; dans la boucle complète de la n°15, le
     processus se dessine. R95 : la surface Processus en J2, la vue du travail comme on regarde Claude Code coder. R97 et
     ADR-023 : un moteur durable en Java sur PostgreSQL, sur le modèle de Temporal, mesuré en J2 « avec la comparaison avec une
     bibliothèque existante ». R99 : un point de décision ouvert à tout moteur d'agents extérieur (J5). R103 : aucun secteur
     d'abord, trois natures de travail.
5. `[ÉTABLI]` **Camunda 8.10, sorti le 13/10/2026** ([notes de version](https://docs.camunda.io/docs/reference/announcements-release-notes/8100/8100-release-notes/)).
   - L'Orchestration Cluster réunit le moteur Zeebe, Operate, Tasklist et Identity depuis la 8.8 ([communiqué du 07/10/2025](https://camunda.com/press_release/camunda-introduces-new-capabilities-to-build-enterprise-grade-ai-agents/)) ;
     à côté, Optimize, les connecteurs, le Desktop Modeler et Camunda Hub ; définir, exécuter et exploiter sont séparés
     ([composants](https://docs.camunda.io/docs/components/)).
   - BPMN exécuté : tâches, passerelles exclusive, parallèle, inclusive et à événements, sous-processus intégré, appelé,
     d'événement et ad hoc, multi-instance, minuteries, messages, erreurs, signaux, escalade, compensation ; pas la transaction, la
     passerelle complexe ni la boucle ([couverture BPMN](https://docs.camunda.io/docs/components/modeler/bpmn/bpmn-coverage/)). DMN avec FEEL ([DMN](https://docs.camunda.io/docs/components/modeler/dmn/)).
     Camunda se dit bâti sur des normes ouvertes, BPMN et DMN ([à propos](https://camunda.com/about/)).
   - L'exploitation : l'incident qui arrête l'instance jusqu'à l'intervention ([incidents](https://docs.camunda.io/docs/components/concepts/incidents/)) ;
     la modification d'une instance en cours, jetons déplacés, ajoutés ou annulés ([modification](https://docs.camunda.io/docs/components/operate/userguide/process-instance-modification/)) ;
     la migration vers une autre version, tout ou rien ([migration](https://docs.camunda.io/docs/components/concepts/process-instance-migration/)) ;
     ce qu'attend chaque instance, en 8.10 ; Tasklist pour les tâches humaines, avec Slack et Teams ([Tasklist](https://docs.camunda.io/docs/components/tasklist/introduction-to-tasklist/)) ;
     Optimize pour l'analyse, présenté comme réservé aux clients entreprise ([Optimize](https://docs.camunda.io/docs/components/optimize/what-is-optimize/)).
   - Un journal d'audit depuis la 8.9 (une personne, un client ou un agent ; quand ; sur quoi), sans garantie d'intégrité décrite
     ([journal d'audit](https://docs.camunda.io/docs/components/audit-log/overview/)).
6. `[ÉTABLI]` **L'orchestration agentique de Camunda.**
   - Le connecteur d'agent IA, en tâche ou en sous-processus : le modèle choisit l'outil, l'ordre et les paramètres ; chaque outil
     est une activité BPMN du sous-processus ad hoc, exécutée par le moteur avec ses reprises, ses incidents et ses tâches
     humaines ; aucun plafond d'itérations décrit ([agents IA, 8.10](https://docs.camunda.io/docs/components/agentic-orchestration/ai-agents/)).
     Modèles d'Anthropic, d'AWS, de Google, d'OpenAI, de Mistral, et un modèle fourni par Camunda sur SaaS.
   - MCP dans les deux sens : l'agent appelle des serveurs MCP, un point d'arrêt humain peut retenir un appel ; le cluster expose
     son serveur MCP (8.9) ; un processus devient un outil appelable (8.10) ([billet du 18/08/2026](https://camunda.com/blog/2026/08/three-ways-camunda-speaks-mcp-and-why-the-direction-matters/)).
     A2A en 8.9 ([billet du 14/04/2026](https://camunda.com/blog/2026/04/camunda-8-9-fastest-path-to-agentic-orchestration/)).
   - En 8.10 : l'état de l'agent et sa conversation en direct dans Operate, un tableau de bord des agents, le test des agents avec un
     juge qui est un modèle ([nouveautés de la 8.10](https://docs.camunda.io/docs/reference/announcements-release-notes/8100/whats-new-in-810/)). Aucun
     niveau de maturité n'est donné à ces fonctions.
   - ProcessOS, en accès anticipé depuis 05/2026 : des agents découvrent comment le travail se fait, le repensent autour d'un
     résultat décrit en mots, puis le construisent ; une personne approuve avant la production ([ProcessOS](https://camunda.com/process-os) ;
     [billet du 19/05/2026](https://camunda.com/blog/2026/05/the-great-process-re-engineering-has-begun/)).
7. `[ÉTABLI]` **L'hébergement, la licence, les prix.**
   - SaaS, ou Self-Managed sur Kubernetes, Docker ou par JAR ([Self-Managed](https://docs.camunda.io/docs/self-managed/about-self-managed/)) ;
     une base secondaire Elasticsearch, OpenSearch ou, depuis la 8.9, relationnelle ; Camunda 8 Run, sur H2, pour le
     développement ([nouveautés de la 8.9](https://docs.camunda.io/docs/reference/announcements-release-notes/890/whats-new-in-89/)).
   - Depuis la 8.6 (08/10/2024), la production auto-hébergée exige une licence ; le code source est sous la Camunda License v1 ;
     restent ouverts le SDK des connecteurs (Apache 2.0) et le Desktop Modeler (MIT) ([billet](https://camunda.com/blog/2024/10/camunda-licensing-what-you-need-to-know/) ;
     [licences](https://docs.camunda.io/docs/reference/licenses/)). bpmn-js exige que le filigrane de bpmn.io reste visible
     ([licence](https://github.com/bpmn-io/bpmn-js/blob/develop/LICENSE)).
   - Camunda 7 Community : dernière version le 14/10/2025, plus aucune ensuite, correctifs de sécurité compris ; l'édition
     Enterprise jusqu'au 09/04/2030 ([billet](https://camunda.com/blog/2025/02/camunda-7-enterprise-end-of-life-extension/)). Operaton, issu de
     Camunda 7 Community, sous Apache 2.0, embarquable dans une application Java, sur PostgreSQL entre autres, publie encore (2.2.1,
     le 07/11/2026) ([dépôt](https://github.com/operaton/operaton)).
   - Aucun prix public : la production et le SaaS sur devis ([prix](https://camunda.com/pricing/)) ; le plan Starter à 99 € par mois
     annoncé le 09/04/2024 n'y figure plus ([billet](https://camunda.com/blog/2024/04/licensing-update-camunda-8-self-managed/)).
8. `[ÉTABLI]` **Jusqu'où Camunda a pris le marché.**
   - Un revenu récurrent proche de 200 M$, une rétention nette au-dessus de 120 %, plus de 700 organisations dont neuf des dix
     premières banques américaines, aucune levée depuis 2021, une valorisation au-delà d'un milliard de dollars par un rachat
     d'actions des salariés ; les nouveaux clients viennent d'abord de la banque, puis de l'assurance et du secteur public ; ceux
     de plus de 10 000 salariés croissent le plus vite ([communiqué du 04/08/2026](https://camunda.com/press-releases/camunda-closing-in-on-200m-in-arr-doubling-revenue-in-record-time/)).
     Les effectifs ne sont pas publiés.
   - Des clients nommés : Goldman Sachs, BNY Mellon, Barclays, ING, ČSOB, Helsana, Kooperativa, le ministère américain des Anciens
     combattants, Swisscom, Deutsche Telekom, REWE digital, Atlassian ([à propos](https://camunda.com/about/) ;
     [secteurs](https://camunda.com/outcomes/industries/) ; [communiqués](https://camunda.com/about/press/)).
   - Forrester le nomme « Leader » de l'orchestration adaptative des processus (T3 2026), le mieux adapté aux grandes entreprises
     ([communiqué du 25/09/2026](https://camunda.com/press_release/camunda-named-a-leader-in-adaptive-process-orchestration-software-evaluation-q3-2026/)) ;
     IDC le nomme « Leader » des plateformes d'IA agentique (2026), moins adapté à qui veut une offre toute prête par secteur
     ([communiqué du 14/10/2026](https://camunda.com/press_release/camunda-named-a-leader-in-idc-marketscape-worldwide-agentic-ai-platforms-2026-vendor-assessment/)) ;
     Gartner l'a classé « Visionary » de son Magic Quadrant BOAT de 2025 ([communiqués](https://camunda.com/about/press/)).
   - Les secteurs : onze sur sa page, sans la pharmacie ; l'industrie et l'énergie avec des cas d'usage, sans client nommé ;
     rien trouvé sur ses sites sur les BPF, 21 CFR Part 11 ou la validation IQ, OQ, PQ ; ISO 27001, SOC 2 Type II et TISAX
     affichés. Le code est son « cœur », le low-code une option ([billet du 08/12/2023](https://camunda.com/blog/2023/12/pro-code-low-code-role-of-camunda/)).
9. `[ÉTABLI]` **Les voisins** (pages officielles, 13/11/2026).
   - UiPath : Maestro, disponible depuis le 30/04/2025, orchestre agents, robots et personnes en BPMN 2.0, en dossiers et en flux,
     avec DMN ; un modèle BPMN généré à partir d'une description ; sur site avec des modèles ouverts depuis le 05/05/2026 ;
     3 981 salariés ([Maestro](https://docs.uipath.com/maestro/automation-cloud/latest/user-guide/overview) ;
     [10-K](https://ir.uipath.com/financials/sec-filings/content/0001734722-26-000012/path-20260131.htm)).
   - Temporal, le modèle d'ADR-023 : MIT, 550 M$ levés à 12,55 Md$ le 14/09/2026 ([communiqué](https://temporal.io/news/temporal-raises-550m-at-a-12-55b-valuation)) ;
     le workflow est du code, aucune boîte de tâches humaines fournie.
   - n8n : fair-code, auto-hébergé, modèles locaux, approbation avant l'appel d'un outil, MCP dans les deux sens, prix publics de 20
     à 667 € par mois ; valorisé 5,2 Md$ avec SAP ([billet du 12/05/2026](https://blog.n8n.io/n8n-sap/) ; [prix](https://n8n.io/pricing/)).
   - Microsoft : Copilot Studio a un harnais qui part d'un but, le découpe et s'ajuste, disponible depuis le 03/08/2026
     ([harnais](https://learn.microsoft.com/en-us/microsoft-copilot-studio/harnesses-overview)) ; Agent 365, le plan de contrôle des agents, depuis le
     01/05/2026 ; prix publics ; en ligne seulement.
   - Pega raisonne à la conception et exécute un workflow conçu d'avance ; ServiceNow et Appian orchestrent agents et personnes ;
     Flowable et Orkes Conductor sont des moteurs ouverts sous Apache 2.0 ; Dapr 1.18 signe l'historique de ses workflows, en
     préversion, par l'identité de l'opérateur ([CNCF](https://www.cncf.io/blog/2026/06/11/introducing-verifiable-execution-in-dapr-1-18/)).
   - `[DÉDUIT]` Aucun ne revendique, dans les pages lues, une preuve vérifiée hors de l'outil par un tiers indépendant, ni des
     règles écrites en mots au-dessus d'un socle déterministe qu'aucune ne relâche.
10. **La cible de TaskForce, et les membres.**
    - `[ÉTABLI]` « N'importe quelle entreprise, dans n'importe quel métier » (n°15), aucun secteur d'abord (R103, ADR-022) ; un
      catalogue choisi pour « une entreprise de 10 à 500 personnes » (Backend.md, 12/11) ; E20, l'intégration d'un module dans un
      logiciel de gestion (n°21). `[DÉDUIT]` La cible reste floue : la taille n'est écrite qu'à propos du catalogue, et qui
      configure (avec ou sans développeur) ne l'est nulle part.
    - `[ÉTABLI]` Les contraintes du terrain : une personne et des agents, aucun revenu, gratuit, l'hébergement après J2, E20 en
      seconde quinzaine de décembre à l'état d'hypothèse ; C1 à C4 du labo.
    - `[ÉTABLI]` Des positions récentes utiles : Nadella veut séparer l'intelligence de l'autorité, des contrôles hors du modèle et
      une trace infalsifiable ([sn scratchpad](https://snscratchpad.com/posts/models-as-insider-risks/), 10/10/2026) ; Saarinen tient qu'une forme
      générée n'est pas un problème résolu ([Linear](https://linear.app/now/output-isn-t-design), 17/04/2026) ; Zhuo rejoint Meta avec le rachat de
      Sundial (fiche, 23/10/2026) ; Hamilton est décédée en 2026 (fiche).

### La pièce de la Présidence, thèse par thèse

| # | Ce que dit la pièce | Ce que le dossier en fait |
| - | --- | --- |
| 1 | Camunda orchestre des processus structurés à l'avance par BPMN | Confirmé, à corriger : depuis la 8.8, un agent y choisit ses outils à l'exécution dans un sous-processus ad hoc ; ProcessOS part d'un résultat visé (points 5, 6) |
| 2 | Camunda peut orchestrer des systèmes intégrant de l'IA | Confirmé, et en dessous du réel : agents, MCP client et serveur, A2A, visibilité et test des agents (point 6) |
| 3 | Les visions se rejoignent : orchestration, état en temps réel, intervention, traçabilité | Confirmé pour Camunda ; pour TaskForce, seulement sur les missions (point 2) |
| 4 | Camunda distingue définir, exécuter, exploiter | Confirmé (point 5) |
| 5 | Prendre Operate comme référence directe de la supervision | À nuancer : `[DÉDUIT]` Operate sert l'exploitation par des équipes techniques, et R57 refuse un écran qui surveille les agents |
| 6 | TaskForce est un système d'exécution du travail piloté par des objectifs, où les agents organisent les tâches | Non conforme à l'état réel : ni objectifs (R56), ni processus, ni agent qui organise un travail ; c'est une vision (points 1, 2) |
| 7 | Un « AI Operating System » | Déjà écarté comme feuille de route à la n°14 (R81) ; R5' reste la promesse |
| 8 | Trois niveaux : l'objectif, l'exécution, la gouvernance | `[HYPOTHÈSE]` Une grille utile pour la vue, pas un fait |
| 9 | La différence fonctionnelle exacte reste à établir | Confirmé : c'est la carte ci-dessous |

### La carte du secrétariat : TaskForce face à Camunda, brique par brique

| # | Brique de Camunda 8.10 | TaskForce (1.16.0, desktop 1.13.0) | Position |
| - | --- | --- | --- |
| 1 | Moteur BPMN, journal d'événements | Des missions en file, qui avancent à la lecture | **Absent** |
| 2 | Notation BPMN et DMN | Un canevas d'analyses, en lecture seule | **Absent** |
| 3 | Versions de processus, migration d'instance | Des règles versionnées et immuables ; aucun processus | **Absent** pour les processus |
| 4 | Operate : instances, incidents, attente, modification | La vue d'une mission : étapes, outils, changements, Stop | **Partiel**, sur les missions |
| 5 | Tasklist : tâches humaines | « Waiting for you » : les accords qui attendent chacun | **Partiel** |
| 6 | Optimize : l'analyse | Rien | **Absent** |
| 7 | Connecteurs | 104 préréglages, une connexion par personne, lecture par défaut | **Comparable**, autre modèle |
| 8 | Agents IA dans le processus | Missions de code sous les règles ; Cortex sur tout modèle | **Ailleurs** : des agents qui font le travail, pas des agents dans un processus |
| 9 | MCP client et serveur | Serveur MCP d'espace, client de 102 outils | **Comparable** |
| 10 | Règles sur les actions des agents | Couches au-dessus d'un socle, en production | **Devant** `[DÉDUIT]` : rien d'équivalent décrit chez Camunda |
| 11 | Journal d'audit, sans intégrité décrite | Dossier chaîné et scellé, vérifié par le runner ; pas signé | **Devant** sur l'intégrité ; pas encore vérifiable par un tiers |
| 12 | SaaS, Kubernetes ; le local pour le développement | Tout sur la machine, modèle local pour Cortex | **Ailleurs** : le local d'abord |
| 13 | Production sous licence payante | AGPL v3, gratuit | **Ailleurs** |
| 14 | 18 mois de maintenance par version, support jour et nuit, certifications | Une personne, aucune certification | **Absent** |
| 15 | Plus de 700 clients, près de 200 M$ de revenu récurrent | Aucun client, aucun revenu | **Absent** |

`[DÉDUIT]` **Lecture** : en produit livré, TaskForce n'a aucune des briques de processus de Camunda (lignes 1 à 6) ; la distance
est entière. En intention, les deux se recouvrent : orchestrer agents, personnes et systèmes sous un contrôle. TaskForce n'est
devant que sur des pièces étroites : la règle jugée hors du modèle à chaque action, le dossier chaîné, le local avec le modèle au
choix, la licence.

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre dit ce que Camunda fait de mieux, où TaskForce peut aller au-dessus, et ce qu'il
recommande. Les interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Esther Duflo (Science)

- « Au-dessus de Camunda » est une affirmation causale sans groupe témoin. Camunda tourne chez plus de 700 organisations ;
  TaskForce n'a ni client, ni expérience menée sur sa promesse : E14 attend depuis le 29/10.
- Le concurrent n°1 est une hypothèse : personne de la cible n'a dit à quoi il comparerait TaskForce.
- Pour chaque « au-dessus », un essai écrit avant et son contre-essai : la même tâche dans un moteur de processus ordinaire et
  dans TaskForce, l'écart mesuré.
- *Sa recommandation : E14 tout de suite, avec une question de plus, « à quoi le compareriez-vous ? ».*

### 2. Audrey Azoulay (Harmonie)

- Camunda vend aux grandes organisations, et le secteur public est l'un de ses trois premiers secteurs de nouveaux clients. Son
  journal d'audit ne décrit aucune garantie d'intégrité.
- À prendre : la notation standard, comme langue commune entre une entreprise et son contrôleur, si l'export existe.
- Au-dessus : un dossier qu'une autorité lit dans sa langue et vérifie sans TaskForce. Il n'est pas construit (TF-J2-7).
- *Sa recommandation : faire lire le dossier d'E20 par une personne d'un organisme de contrôle, et noter ce qu'elle n'a pas
  compris.*

### 3. Fei-Fei Li (Science)

- À prendre : Camunda met le test des agents dans le cycle de vie du processus (Camunda Process Test, 8.10). C'est la bonne place.
- Sa réserve : un juge qui est un modèle n'est pas un tiers. Elle préfère des cas notés par du code, comme la banque de TaskForce.
- TaskForce mesure des modèles (le banc, TF-J1-11), jamais un processus de bout en bout.
- *Sa recommandation : chaque processus porte ses cas d'essai, rejoués à chaque nouvelle version ; une version n'entre que s'ils
  passent.*

### 4. Daniela Rus (Science)

- Camunda se déploie sur Kubernetes avec une base secondaire ; son exécution locale sert au développement, sur H2. TaskForce fait
  tourner sur la machine la base, le backend, le runner et le modèle : l'architecture d'un système qui ne dépend pas du réseau.
- Sa réserve : sans moteur durable, le local ne tient pas un processus long. Une machine s'endort.
- Un moteur embarqué de plus pèse sur l'app desktop : son empreinte se mesure avant de le choisir.
- *Sa recommandation : l'essai de coupure d'ADR-023 sur l'app desktop, machine mise en veille au milieu d'un processus, avant
  toute autre fonction de processus.*

### 5. Satya Nadella (Pont, conflit d'intérêts : Microsoft)

- Camunda est une vraie plateforme : près de 200 M$ de revenu récurrent, une rétention nette au-dessus de 120 %, MCP dans les deux
  sens, un agent qui agit par des activités gouvernées. Le traiter en éditeur de diagrammes serait une erreur.
- Le concurrent n°1, sur la cible écrite d'une entreprise de 10 à 500 personnes : ce qui est déjà dans le locataire, Copilot
  Studio et Power Automate, à prix publics. Il le dit avec son conflit d'intérêts.
- Au-dessus : sa doctrine, des contrôles hors du modèle et une trace infalsifiable. Ni Camunda ni Microsoft ne décrivent une trace
  signée qu'un tiers vérifie : c'est la place de TaskForce.
- *Sa recommandation : se brancher plutôt que combattre, TaskForce comme couche de règles et de preuve qu'un processus Camunda
  appelle par MCP.*

### 6. Yoshua Bengio (Science)

- Chez Camunda, le modèle choisit l'outil, l'ordre et les paramètres dans le sous-processus ad hoc ; les garde-fous sont les
  frontières du processus et les arrêts humains. Rien ne chiffre le risque d'une action avant qu'elle parte.
- Au-dessus : TaskForce juge chaque action hors du modèle, sous un socle qu'aucune règle ne relâche, en production depuis la 1.15.0.
- Sa réserve : une structure qui émerge pendant l'exécution, c'est un agent qui choisit son propre périmètre.
- *Sa recommandation : l'agent ne choisit que dans une zone dessinée d'avance et bornée par les règles ; toute étape nouvelle passe
  par une personne.*

### 7. Margaret Hamilton (Science, siège historique)

- Elle ne connaît Camunda que par le dossier, et y lit ce qu'elle a toujours défendu : une sémantique d'exécution écrite, des
  incidents qui arrêtent l'instance au lieu de la laisser mentir, une version figée, une migration qui passe en entier ou pas.
- TaskForce n'a rien de cela : une mission avance quand on la lit, et une mission perdue se découvre par une personne.
- Une structure qui émerge est une interface sans contrat écrit.
- *Sa recommandation : prendre la sémantique, l'éprouver par des coupures provoquées, et ne modifier une instance en cours qu'avec
  une raison écrite et approuvée.*

### 8. Yann LeCun (Science)

- La pièce suppose que des agents « analysent le problème » et « organisent les tâches », donc qu'un LLM planifie. Il ne planifie
  pas de façon fiable. Camunda a fait le choix juste : la structure est dessinée, l'agent choisit dans une boîte à outils gouvernée.
- Sur l'ouverture : Camunda est passé d'un moteur libre à une production sous contrat, et Camunda 7 Community n'a plus de version
  depuis le 14/10/2025. L'AGPL de TaskForce, et Operaton, la suite communautaire de Camunda 7, sont du bon côté.
- *Sa recommandation : l'aperçu des effets avant chaque étape d'agent (le diff, la commande, l'exécution à blanc), et un plan
  proposé par un modèle vérifié par du code avant d'exister.*

### 9. Arati Prabhakar (Pont)

- « Dépasser Camunda » n'a pas de seuil. Un programme à haut risque écrit ses essais, ses chiffres, sa date.
- Trois seuils sont déjà écrits : un processus repris après coupure sans rien refaire (critère 6), un dossier vérifié par un
  programme indépendant (critère 7), une règle en mots qui arrête la bonne étape (critère 5).
- Ce que Camunda prouve et pas TaskForce : la tenue à l'échelle, que Forrester note au plus haut. Ce n'est pas l'objet de J2.
- *Sa recommandation : la barre de Camunda se mesure par les critères de J2, pas par une liste de fonctions.*

### 10. Nandan Nilekani (Harmonie)

- BPMN et DMN sont des normes ouvertes, et Camunda parle MCP dans les deux sens. Un processus qu'on ne peut pas exporter, c'est une
  plateforme fermée qui se dit infrastructure.
- À prendre : la notation comme format d'échange, pas comme interface : l'export et l'import d'un sous-ensemble.
- Au-dessus : la règle et la preuve dans l'architecture, et une connexion par personne, qui garde les droits de la source.
- *Sa recommandation : chaque processus de TaskForce s'exporte en BPMN 2.0 et s'ouvre dans un autre outil.*

### 11. Jeff Bezos (Impulsion)

- Le client juge. Aucun client n'a demandé de battre Camunda ; le premier client possible veut intégrer un module à son outil de
  base sans erreur bête, et le prouver (E20).
- Le terrain de Camunda, ce sont les grandes organisations : ses nouveaux clients de plus de 10 000 salariés sont son segment le
  plus rapide. Une personne n'y gagne pas.
- La plupart des choix du jour sont des portes à double sens (un sous-ensemble de BPMN, un moteur à l'essai) : décider vite.
- *Sa recommandation : écrire d'abord le communiqué d'E20, et ne prendre à Camunda que ce qu'il exige (hors fiche : c'est la
  méthode d'Amazon).*

### 12. Kenza Ait Si Abbou (Pont)

- BPMN est une langue d'analyste et de développeur ; Camunda dit lui-même que le code est son cœur et le low-code une option.
- Dans une entreprise moyenne de l'industrie ou des services, la personne qui accorde une étape ne lit pas un diagramme. La vue
  doit se lire comme un plan de projet : qui, quoi, quand, ce qui attend.
- Au-dessus : une interface qui n'oblige personne à penser en BPMN. Elle n'est pas construite.
- *Sa recommandation : la maquette montrée à une personne qui ne fait pas de logiciel, qui doit dire en une minute ce qui attend
  et qui décide.*

### 13. Steve Jobs (Impulsion, siège historique)

- Claude et Camunda, il ne les connaît que par le dossier. « Claude x Camunda » nomme deux produits qui ne sont pas TaskForce : un
  produit qui se décrit par deux autres n'a pas encore trouvé ce qu'il est.
- À prendre : ce qui sert le geste, voir le projet entier et décider là où l'on voit. Pas l'éditeur de diagrammes, pas les
  tableaux d'analyse.
- La vue est la bonne question : elle est jugée horrible, et c'est elle qui fera le produit. Une seule surface, intégrée comme le
  board.
- *Sa recommandation : dire non à la moitié de la liste des emprunts, et finir la vue avant le reste.*

### 14. Mariana Mazzucato (Pont)

- Camunda a fermé la production gratuite (8.6, 08/10/2024), puis arrêté son moteur libre (Camunda 7, 14/10/2025). La valeur d'une
  communauté de dix ans passe derrière une licence : un bien commun devenu rente.
- TaskForce, sous AGPL et gratuit, peut être l'autre direction, si cela dure : R106 garde le cœur sous AGPL.
- Une porte : le secteur public est l'un des trois premiers secteurs de nouveaux clients de Camunda. Une commande publique veut un
  processus ouvert, portable et vérifiable.
- *Sa recommandation : dire, dans la phrase de différence, que les processus, les règles et la preuve appartiennent au client et
  partent avec lui.*

### 15. Jennifer Doudna (Science)

- Camunda laisse le modèle choisir dans une zone ; il ne dit pas quelle preuve élargit la zone.
- À prendre : la séparation entre définir, exécuter et exploiter, qui donne un lieu à chaque palier. Une définition change par une
  nouvelle version, jamais en cours de route.
- Au-dessus : un palier qui s'ouvre sur preuve et se referme sur incident (R97). Il n'est pas construit.
- *Sa recommandation : chaque étape d'agent d'un processus porte son palier, et le dossier dit pourquoi il est ouvert.*

### 16. Don Norman (Design)

- À prendre : Operate est un bon modèle de dialogue entre l'opérateur et le système : ce que chaque instance attend, l'incident là
  où il s'est produit, la modification préparée puis appliquée.
- Sa réserve : Operate sert un ingénieur d'exploitation. La vue de TaskForce sert la personne qui délègue : ce que l'agent a
  compris, ce qu'il va faire, ce qui est irréversible.
- La pièce dit juste sur un point : rendre l'exécution visible sans imposer de penser en nœuds.
- *Sa recommandation : sur chaque étape, ce qui a été fait, ce qui attend et qui décide ; et l'annulation partout où elle existe.*

### 17. Yuval Noah Harari (Harmonie)

- Un « AI Operating System » déplace la responsabilité vers le système. Dans un processus, chaque étape nomme la personne qui en
  répond, même quand un agent la fait.
- Camunda attribue chaque opération à une personne, un client ou un agent ; il ne dit pas qui en répond.
- Une structure qui émerge sans un nom derrière chaque étape, c'est une organisation sans responsable.
- *Sa recommandation : une étape sans personne qui en répond ne se publie pas.*

### 18. Elon Musk (Impulsion)

- Il supprime la moitié des emprunts : pas d'Optimize, pas de DMN (les règles en mots le remplacent), pas de connecteurs (le
  catalogue MCP existe), pas d'éditeur BPMN.
- Le moteur : ADR-023 copie Temporal, alors qu'un moteur BPMN existe sous Apache 2.0, en Java, sur PostgreSQL, qui publie encore :
  Operaton. Ne pas écrire un moteur avant d'avoir essayé celui-là.
- « Au-dessus » se dit avec un chiffre : le nombre de jours avant qu'une entreprise fasse tourner son premier processus.
- *Sa recommandation : l'essai de coupure joué sur Operaton et sur le moteur maison ; on garde le plus simple qui tient.*

### 19. Gwynne Shotwell (Impulsion, contradictrice)

- Le meilleur de Camunda n'est pas dans ses diagrammes, il est dans son exploitation : 18 mois de maintenance par version, un
  support jour et nuit, ISO 27001, SOC 2 Type II, TISAX. C'est cela qu'une entreprise achète, et rien ne s'en construit en dix
  jours.
- E20 en seconde quinzaine de décembre est une hypothèse. Y ajouter la liste de Camunda en fait une échéance annoncée comme
  certaine.
- À prendre : la discipline de version (une version, sa durée de maintenance, son chemin de migration).
- *Sa recommandation : rien de Camunda qui ne serve un critère de sortie de J2 ; le reste en J5.*

### 20. Atul Gawande (Science)

- À prendre : la tâche humaine de BPMN est un point de pause. Le processus s'arrête et attend une personne : la liste de contrôle
  inscrite dans le flux.
- Les trois points de pause de TF-J2-10 (avant une mission, avant d'appliquer, avant de livrer) sont les tâches humaines du
  processus « intégrer un module ».
- Il demande une mesure avant et après sur E20 : combien d'erreurs bêtes avec le processus, combien sans.
- *Sa recommandation : les listes de moins de dix lignes portées par les tâches humaines, pas par une fenêtre à part.*

### 21. Julie Zhuo (Design, conflit d'intérêts : Meta, par Sundial)

- La première minute : la vue actuelle échoue, la Présidence l'a dit. Elle veut le pronostic écrit avant de construire la suivante.
- L'échelle conseiller, adjoint, régent se lit sur un processus : l'adjoint propose une étape, une personne l'accepte ; le régent
  agit dans sa zone et rend compte.
- La structure qui émerge : une bonne idée contre la page blanche, proposer un premier processus à partir de l'objectif ; une
  mauvaise pour l'exécution.
- *Sa recommandation : « décrire l'objectif » donne un brouillon que la personne corrige, jamais un processus qui tourne seul.*

### 22. Karri Saarinen (Design, conflit d'intérêts : Linear)

- Camunda est un outil pour concevoir et exploiter des processus ; TaskForce doit être l'outil où l'on fait le travail. Les deux ne
  doivent pas se ressembler.
- La vue : un établi structuré, dense et rapide, avec un parti pris. Pas un canevas libre où l'on dessine, mais la carte du projet
  que TaskForce tient à jour, comme le board. D'Operate, il retient l'état d'abord, le détail à un clic.
- Sa réserve : une forme générée n'est pas un problème résolu.
- *Sa recommandation : la vue s'ouvre comme le board, par l'onglet du projet, en pleine largeur ; chaque nœud est une issue, une
  mission ou un accord réel.*

### 23. Tristan Harris (Harmonie)

- Suivre l'incitation : « concurrencer Camunda » met TaskForce dans une course aux fonctions qu'un éditeur de près de 200 M$ de
  revenu récurrent gagnera.
- La pièce vient d'un assistant d'IA réglé pour être agréable à qui l'interroge : elle rend à la Présidence son ambition, un « AI
  Operating System », sans en dire le coût. Sa meilleure phrase est sa mise en garde finale.
- La charge de la preuve est au constructeur : aucun « au-dessus » ne sort sans son essai.
- *Sa recommandation : la phrase publique ne contient ni Camunda, ni « au-dessus », tant que la preuve n'est pas faite.*

### 24. Margrethe Vestager (Harmonie)

- Le changement de licence de Camunda est un cas d'école d'enfermement. Les utilisateurs de Camunda 7 Community restent sur une
  version sans correctif, migrent vers Camunda 8, paient l'édition Enterprise ou suivent un fork.
- La portabilité est l'argument de TaskForce, s'il est vrai : un processus exportable, des règles et un dossier qui partent avec
  le client.
- Sa question : qui vérifie que la règle exécutée est celle adoptée ? Chez Camunda, rien ne le dit hors de l'outil ; chez
  TaskForce, la version de la règle et son empreinte entrent au dossier.
- *Sa recommandation : l'export complet d'un processus, de ses règles et de son dossier, rejoué dans un espace neuf.*

### Le tour en une table

| # | Membre | Ce qu'il retient de Camunda | Sa recommandation |
| - | --- | --- | --- |
| 1 | Duflo | Une base installée, mesurée | E14, et « à quoi le compareriez-vous ? » |
| 2 | Azoulay | Une notation commune avec le contrôleur | Le dossier d'E20 lu par un organisme de contrôle |
| 3 | Li | Le test des agents dans le cycle de vie | Des cas par processus, rejoués à chaque version |
| 4 | Rus | Kubernetes, le local pour le développement | L'essai de coupure en veille, sur l'app desktop |
| 5 | Nadella, conflit d'intérêts | Une vraie plateforme | Se brancher : TaskForce appelée par MCP |
| 6 | Bengio | Le modèle choisit dans une zone | L'agent borné par les règles ; une étape nouvelle passe par une personne |
| 7 | Hamilton | La sémantique d'exécution | La prendre, l'éprouver par des coupures |
| 8 | LeCun | La structure dessinée, l'agent dans une boîte à outils | L'aperçu des effets ; un plan vérifié par du code |
| 9 | Prabhakar | La tenue à l'échelle | La barre mesurée par les critères de J2 |
| 10 | Nilekani | Des normes ouvertes | L'export en BPMN 2.0 |
| 11 | Bezos | Le terrain des grandes organisations | Le communiqué d'E20 d'abord |
| 12 | Ait Si Abbou | Le code d'abord | La maquette lue par une personne qui ne fait pas de logiciel |
| 13 | Jobs, siège historique | Voir le projet entier | Dire non à la moitié ; finir la vue |
| 14 | Mazzucato | Un bien commun devenu rente | Les processus, les règles et la preuve au client |
| 15 | Doudna | Définir, exécuter, exploiter | Un palier par étape d'agent |
| 16 | Norman | Le dialogue d'Operate | Fait, attend, décide ; l'annulation |
| 17 | Harari | L'attribution, sans responsable | Pas d'étape sans personne qui en répond |
| 18 | Musk | Un moteur ouvert existe | Operaton face au moteur maison |
| 19 | Shotwell, contradictrice | L'exploitation | Rien hors des critères de J2 |
| 20 | Gawande | La tâche humaine, point de pause | Les listes portées par les tâches humaines |
| 21 | Zhuo, conflit d'intérêts | La page blanche à éviter | Un brouillon corrigé, jamais un processus seul |
| 22 | Saarinen, conflit d'intérêts | L'état d'abord | La vue comme le board, des nœuds réels |
| 23 | Harris | Une course perdue d'avance | Ni Camunda, ni « au-dessus » en public |
| 24 | Vestager | Un cas d'enfermement | L'export complet rejoué ailleurs |

## Confrontation `[HYPOTHÈSE]`

### 1. Le cadre, et le concurrent n°1

- **Le camp du piège** : Jobs, Harris, Saarinen, Duflo, Bezos et Mazzucato.
  - Jobs : un produit qui se décrit par deux autres n'a pas encore trouvé ce qu'il est.
  - Saarinen : « Claude » lie TaskForce à un fournisseur, contre R92 ; « AI Operating System » est le texte générique que la
    séance n°14 a refusé comme feuille de route (R81).
  - Harris : l'analogie flatte ; elle promet ce que deux éditeurs ont construit en dix ans.
- **Le camp du cadre utile** : Nadella et Nilekani. Un acheteur classe d'abord, et un architecte lira « un Camunda pour agents »
  de toute façon : mieux vaut le dire soi-même que l'entendre dire.
- **La contradictrice** attaque le consensus qui se forme : refuser le cadre n'empêche pas la comparaison. Un acheteur qui connaît
  Camunda posera la question au premier rendez-vous ; il lui faut une réponse écrite et factuelle, pas une esquive.
- **Sur le concurrent n°1** :
  - Nadella, avec son conflit d'intérêts : Microsoft, déjà dans le locataire, à prix publics ;
  - Duflo : personne de la cible n'a été interrogé, c'est une hypothèse ;
  - Ait Si Abbou : pour une entreprise sans développeur, Camunda n'est pas sur la liste ;
  - Hamilton et Prabhakar : quel que soit le concurrent, Camunda est la barre de la rigueur d'exécution.
- **Où l'on arrive** :
  - ni « Claude x Camunda », ni « AI Operating System » ; Camunda est la barre d'exploitation et la référence technique, pas la
    catégorie ; la phrase ne parle que de règles et de preuve ; une page de comparaison factuelle répond à l'acheteur qui connaît
    Camunda (R163) ;
  - le concurrent n°1 n'est pas tranché : sur la cible écrite, Microsoft et n8n sont plus proches ; sur le scénario d'E20, la
    plateforme où vit le code ; E14 le demandera à la cible (R164).
- **Désaccords conservés** : Nadella (le cadre aide l'acheteur à classer) ; Nilekani (« parle BPMN » est un argument
  d'interopérabilité, à dire).

### 2. Une structure qui émerge, ou un processus dessiné ?

- **Le camp de l'émergence** : Zhuo, Ait Si Abbou et Musk, avec la pièce. Personne dans une entreprise de quarante personnes ne
  dessinera un processus en BPMN. Camunda lui-même va vers l'objectif : ProcessOS repense un processus autour d'un résultat décrit
  en mots.
- **Le camp du dessin** : Hamilton, LeCun, Bengio, Gawande et Doudna.
  - Hamilton : ce qui n'est pas écrit avant ne se vérifie pas, ne se reprend pas après une coupure, ne s'audite pas.
  - LeCun : un LLM ne planifie pas de façon fiable.
  - Bengio : à l'exécution, une structure qui émerge est un agent qui choisit son périmètre.
  - Le dossier les appuie : quand Camunda laisse le modèle choisir, c'est dans une zone dessinée, le sous-processus ad hoc ; et
    ProcessOS propose, une personne approuve avant la production.
- **La contradictrice** attaque la synthèse qui se forme (« l'objectif propose, la personne arrête ») : un brouillon généré, accepté
  d'un clic, devient un processus que personne n'a pensé. C'est la fatigue de l'accord, appliquée aux processus. Harris la
  rejoint ; Saarinen ajoute qu'une forme générée n'est pas un problème résolu.
- **Où l'on arrive** : l'objectif propose, la personne arrête, le moteur exécute (R169).
  - Le brouillon se lit en mots, dit ce qu'il ne sait pas, et s'accepte étape par étape, chacune avec la personne qui en répond.
  - À l'exécution, l'agent ne choisit que dans les zones ad hoc, sous les règles.
  - Une étape nouvelle fait une nouvelle version ; une instance en cours ne change qu'avec une raison écrite et approuvée.
- **Désaccords conservés** : Musk (une liste d'étapes en mots suffit, sans sous-ensemble de BPMN) ; Saarinen (pas de brouillon
  généré du tout).

### 3. Prendre BPMN et son moteur, ou les refaire ?

- **Le camp de l'intégration** : Musk (essayer Operaton avant d'écrire un moteur), Nilekani et Vestager (l'export pour la
  portabilité), Nadella (se brancher à Camunda par MCP).
- **Le camp du mince, chez nous** : Rus (l'app desktop doit rester légère), Hamilton (le moteur se prouve par nos coupures), Jobs et
  Saarinen (personne ne voit de BPMN).
- **La contradictrice** : un moteur qu'on embarque, on l'exploite. Qui corrige un défaut d'Operaton un dimanche ? Un fork
  communautaire n'a pas de support jour et nuit, et TaskForce non plus.
- **Ce que le dossier tranche** :
  - Zeebe est hors jeu : sa production exige une licence payante ; `[DÉDUIT]` il ne peut pas être distribué gratuitement avec
    TaskForce sous AGPL ;
  - bpmn-js impose son filigrane, ni retiré ni masqué ; et la vue ne montre pas de BPMN.
- **Où l'on arrive** :
  - la notation sert l'échange, jamais l'interface : un sous-ensemble de BPMN 2.0, exporté et importé (R165) ;
  - le moteur se choisit par la mesure : la comparaison déjà prévue par ADR-023 met Operaton face au moteur maison, sur les mêmes
    coupures, avec des critères écrits avant, l'activité du projet comprise (R167) ;
  - se brancher à Camunda reste une question (Q18).
- **Désaccords conservés** : Rus (l'empreinte d'un moteur embarqué) ; Shotwell (ni l'un ni l'autre avant le critère 6).

### Où le Conseil arrive, question par question

| Question de la saisine | Ce que le Conseil répond | Où |
| --- | --- | --- |
| Que fait Camunda, sur les faits ? | Il exécute des processus BPMN à grande échelle pour les grandes organisations, y met des agents depuis 10/2025, et part d'un résultat avec ProcessOS, en accès anticipé | Dossier, points 5 à 8 |
| Le meilleur à prendre | La sémantique d'un sous-ensemble, la séparation définir, exécuter, exploiter, l'incident et l'attente, la version, la tâche humaine, la zone ad hoc ; ni Optimize, ni DMN, ni les connecteurs, ni bpmn-js | R165 |
| Où TaskForce va au-dessus | Seulement là où c'est prouvé : les règles en mots sur un socle, en production ; la preuve vérifiée par un tiers, à construire ; le local, l'AGPL et la connexion par personne sont des faits ; partir de l'objectif n'est pas une avance | R168, R169 |
| À quel point proches | En produit livré, loin : aucune brique de processus ; en intention, proches ; devant sur des pièces étroites | Carte du secrétariat |
| Le cadre | Ni l'un ni l'autre ; une phrase de règles et de preuve ; R5' reste la promesse | R163 |
| Ce que cela change | La vue (R166), TF-J2-2 (R165), ADR-023 (R167), le pitch et E20 (R170) | Recommandations |
| Jusqu'où Camunda a pris le marché | Près de 200 M$ de revenu récurrent, plus de 700 organisations, la banque, l'assurance, le secteur public ; peu ou pas d'offre pour les petites structures et les équipes sans développeur ; rien trouvé sur la pharmacie validée | Dossier, point 8 |
| Le concurrent n°1 | Pas tranché ; pas Camunda sur la cible écrite ; la cible à écrire, puis à demander | R164 |

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R163 (R162 est la dernière existante). Chacune porte qui la soutient, qui s'y oppose, sa preuve en dix jours
et son signal d'arrêt. La contradictrice attaque avant chaque vote ; une recommandation passe avec 22 oui sur 24 au moins.

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| R163 | Ni « Claude x Camunda » ni « AI Operating System » : une phrase de règles et de preuve, et une page de comparaison factuelle | 23 au second tour | Nadella | E14 : trois personnes sur cinq redisent la phrase | Moins de trois, ou « un Camunda avec de l'IA » |
| R164 | Le concurrent n°1 : la cible écrite d'abord, puis demandée à la cible | 22 | Shotwell ; abstention de Bezos | La ligne de la cible, et les noms cités pendant E14 | Trois personnes sur cinq citent Camunda |
| R165 | Les emprunts à Camunda, un par un ; un sous-ensemble de BPMN pour l'échange, jamais pour l'interface | 23 au second tour | Abstention de Jobs | Le processus d'E20 exporté, ouvert dans un modeleur BPMN, réimporté à l'identique | Le processus d'E20 qui ne s'écrit pas sans un élément de plus |
| R166 | La vue du workflow : le projet entier, piloté là où on le voit, comme le board | 23 | Abstention de Shotwell | La maquette relue, puis une version sur les données vivantes | Une donnée fictive, ou un geste qui contourne les règles |
| R167 | Le moteur d'ADR-023 : mesurer avant de copier Temporal, Operaton face au moteur maison | 23 au second tour | Shotwell | L'essai de coupure joué sur les deux | Une étape perdue, ou faite deux fois |
| R168 | Au-dessus de Camunda : seulement ce qui est prouvé | 23 | Abstention de Nadella | La table des avances, et ses deux premières preuves | Une avance affirmée sans sa preuve |
| R169 | L'objectif propose, la personne arrête, le moteur exécute | 22 au second tour | Saarinen ; abstention de Jobs | Le brouillon d'E20 accepté étape par étape | Une étape acceptée que personne ne sait expliquer |
| R170 | E20 et le pitch : un processus, montré de bout en bout | 23 | Abstention de Bezos | Le processus d'E20 joué une fois, avec une coupure | E20 qui glisse à cause d'un emprunt |

### R163. Ni « Claude x Camunda », ni « AI Operating System » : une phrase de règles et de preuve (second tour)

- **Quoi** :
  - Aucun cadre public ne nomme Camunda ni Claude. Claude est un modèle parmi d'autres (R92) ; Camunda est la barre d'exploitation
    et la référence technique de TaskForce, pas sa catégorie.
  - La promesse reste R5'. La phrase de différence, mise à l'épreuve par E14, ne parle que de règles et de preuve. Une proposition à
    l'essai `[HYPOTHÈSE]` : « Vos règles s'appliquent à chaque action, d'une personne ou d'un agent, et chaque résultat laisse une
    preuve qu'un tiers vérifie sans nous. »
  - Les trois niveaux de la pièce (l'objectif, l'exécution, la gouvernance) servent de grille à la vue (R166), pas de slogan.
- **L'attaque de la contradictrice** : un cadre refusé reste celui de l'acheteur ; sans réponse écrite, l'esquive coûte la
  confiance au premier rendez-vous.
- **Premier tour** : 20 oui, 3 non (Nadella, Nilekani, Shotwell), 1 abstention (Bezos, qui veut décider après E14). 83,3 %.
- **Amendements** :
  - une page de comparaison factuelle, pour l'acheteur qui connaît Camunda : ce que Camunda fait et que TaskForce ne fait pas, et
    l'inverse, chaque ligne sourcée et datée (Shotwell) ;
  - dans la documentation technique, « parle BPMN » se dit comme un fait d'interopérabilité, une fois l'export construit
    (Nilekani).
- **Second tour** : 23 oui, 1 non (Nadella, maintenu : le cadre aide l'acheteur à classer). 95,8 %.
- **Preuve en dix jours** : E14 menée avec cinq personnes de la cible, dont deux au moins qui connaissent un moteur de processus et
  deux hors du réseau de la Présidence ; trois au moins redisent la phrase juste ; la page de comparaison relue par la Présidence.
- **Signal d'arrêt** : moins de trois sur cinq, ou trois au moins qui décrivent TaskForce comme « un Camunda avec de l'IA » : la
  phrase se réécrit avant le pitch.

### R164. Le concurrent n°1 : la cible écrite d'abord, puis demandée à la cible

- **Quoi** :
  - `[DÉDUIT]` Les documents laissent la cible floue : « n'importe quelle entreprise » (R103, ADR-022), un catalogue choisi pour
    « une entreprise de 10 à 500 personnes » (12/11), et E20, l'intégration d'un module dans un logiciel de gestion.
  - La Présidence écrit la cible en une ligne : la taille, qui configure (avec ou sans développeur), la première nature de travail.
  - Sur la cible écrite aujourd'hui, le Conseil ne tient pas Camunda pour le concurrent n°1 : Camunda vise les grandes
    organisations (Forrester, IDC, ses propres chiffres) ; Microsoft et n8n sont plus proches des entreprises de 10 à 500
    personnes ; pour le scénario d'E20, le concurrent est la plateforme où vit le code. Camunda reste la référence de la rigueur
    d'exécution, et devient le concurrent n°1 si la cible devient la grande organisation régulée qui a des développeurs.
  - E14 pose une question de plus : « à quoi le compareriez-vous ? » ; ses résultats gardent les noms cités.
- **L'attaque de la contradictrice** : classer les concurrents ne change rien à ce que J2 construit ; c'est une heure prise au
  travail.
- **Vote** : 22 oui, 1 non (Shotwell), 1 abstention (Bezos : le client le dira, inutile de classer d'avance). 91,7 %.
- **Preuve en dix jours** : la ligne de la cible écrite ; E14 menée avec la question des noms.
- **Signal d'arrêt** (qui ferait revenir sur R164) : trois personnes sur cinq au moins citent Camunda. Il devient alors le
  concurrent n°1, et le pitch se réécrit contre lui.

### R165. Les emprunts à Camunda, un par un (second tour)

- **Quoi** :
  - Les processus de TF-J2-2 suivent la sémantique d'un sous-ensemble de BPMN 2.0, exportable et importable. Les cinq types
    d'étapes, une proposition `[HYPOTHÈSE]` : l'étape d'agent (une tâche de service tenue par un agent), la tâche humaine (un
    accord ou une saisie), la décision (une passerelle exclusive, jugée par du code et jamais par un modèle), l'attente (une
    minuterie ou un message), la zone d'agent (un sous-processus ad hoc). Un élément hors du sous-ensemble est refusé à l'import,
    avec sa raison.
  - Personne ne voit de BPMN dans l'interface : la vue montre des étapes en mots (R166).
  - La table des emprunts :

    | Emprunt | Ce qu'il apporte à une entreprise | Ce qu'il coûte | Comment TaskForce le prend | Quand |
    | --- | --- | --- | --- | --- |
    | La sémantique d'exécution (jetons, passerelles exclusive et parallèle, minuteries, messages) | Un processus qui fait ce que son dessin dit, et se vérifie | Un moteur (R167) | Par la notation, un sous-ensemble ; le moteur refait ou intégré | J2, pour le processus d'E20 |
    | La compensation | Défaire proprement une suite d'étapes | Élevé | Par la notation | J5 |
    | Définir, exécuter, exploiter séparés | Changer une définition sans casser une instance en cours | Faible, s'il est fait dès le départ | Par le modèle de données (la définition, l'instance, son journal) et le modèle d'interface | J2 |
    | La version d'un processus | Savoir quelle définition et quelle règle ont produit chaque résultat | Faible | En le refaisant : chaque publication est une version immuable, avec son auteur et son empreinte, comme les règles (V125) | J2 |
    | Operate : instances, incidents, attente | Voir ce qui attend et ce qui casse, là où c'est | Moyen | Par le modèle d'interface, refait dans la vue (R166) | J2 |
    | Operate : modification et migration d'une instance | Réparer sans repartir de zéro | Moyen à élevé | En le refaisant, chaque geste jugé par les règles et entré au dossier | J5 |
    | Tasklist : les tâches humaines | La personne sait ce qu'on attend d'elle | Faible : « Waiting for you » existe | En le refaisant : les tâches humaines entrent dans « Waiting for you », une carte avec ses valeurs plutôt qu'un formulaire libre | J2 |
    | La zone ad hoc des agents | L'agent choisit, mais dans une zone bornée, et la structure reste lisible | Moyen | Par la notation, chaque choix de l'agent jugé par les règles | J2 |
    | Optimize : l'analyse | Où le processus perd du temps | Élevé | Plus tard, à partir du dossier | J7 |
    | DMN : les tables de décision | Des décisions métier lisibles | Moyen | Non : les règles en mots en tiennent lieu ; un import si un client en a | Non |
    | Les connecteurs | Brancher les systèmes | Déjà payé | Non : le catalogue MCP et la connexion par personne en tiennent lieu | Non |
    | bpmn-js | Dessiner du BPMN dans le navigateur | Un filigrane, ni retiré ni masqué | Non : l'export suffit pour ouvrir un processus ailleurs | Non |
    | Un processus appelable comme un outil | D'autres agents lancent un processus | Faible | Par le MCP de TaskForce (ADR-024) | J5 |

- **L'attaque de la contradictrice** : treize lignes, c'est un second produit. Tout ce que le processus d'E20 n'exige pas sort de J2.
- **Premier tour** : 20 oui, 2 non (Musk : le sous-ensemble est encore trop grand ; Shotwell), 2 abstentions (Jobs et Saarinen,
  tant que la vue n'est pas vue). 83,3 %.
- **Amendement** : J2 ne prend que ce qu'exige le processus « intégrer un module » ; le reste suit le jalon de la table, ou jamais.
  La table reste la référence.
- **Second tour** : 23 oui, 1 abstention (Jobs). 95,8 %.
- **Preuve en dix jours** : le processus « intégrer un module » écrit dans le sous-ensemble, exporté en BPMN 2.0, ouvert sans erreur
  dans un modeleur BPMN (le Desktop Modeler de Camunda est sous MIT), puis réimporté à l'identique.
- **Signal d'arrêt** : le processus d'E20 ne s'écrit pas dans le sous-ensemble sans un élément de plus. Le choix de BPMN se revoit
  alors, avant d'en ajouter un.

### R166. La vue du workflow : le projet entier, piloté là où on le voit

- **Quoi** :
  - Une vue du projet, au rang du board : son onglet, sa route, ses volets, en pleine largeur ; plus jamais une fenêtre par-dessus.
  - Les trois niveaux en une seule surface : l'objectif en tête (le but, la date, les critères de réussite, R56) ; l'exécution au
    centre (les étapes, ce qui tourne, ce qui attend, l'incident là où il s'est produit) ; la gouvernance sur chaque nœud (la règle
    qui s'applique, qui décide, l'accord à donner, la preuve).
  - Sur chaque nœud : ce qui a été fait, ce qui attend, qui décide (Norman) ; les ressources et les liens (documents rangés, issue,
    branche, pull request) ; les choix à un clic (accorder, relancer, arrêter), chacun jugé par les règles et entré au dossier.
  - Des données vivantes seulement (R15). Avant les processus de TF-J2-2, les étapes sont les colonnes du projet et ses cycles.
  - R57 tient : la vue montre le travail sur son objet, le projet ; aucun mur de surveillance des agents.
  - Ce qui se construit d'abord, dans l'ordre de la carte du code : les dépendances lisibles par projet, un flux du projet pour les
    missions et leurs accords, puis le fil d'événements.
- **L'attaque de la contradictrice** : une vue construite avant le moteur montrera ce que le moteur ne tient pas encore.
  Réponse de Saarinen et de Norman : la vue ne montre que ce qui est vivant, et les colonnes du projet suffisent avant TF-J2-2.
- **Vote** : 23 oui, 1 abstention (Shotwell). 95,8 %.
- **Preuve en dix jours** : la maquette relue par la Présidence ; puis une première version sur les données vivantes d'un projet :
  les colonnes en couloirs, les issues et leurs dépendances, les missions et leurs accords sur les nœuds, un accord décidé depuis
  un nœud et retrouvé au dossier ; une personne qui ne fait pas de logiciel dit en une minute ce qui attend et qui décide.
- **Signal d'arrêt** : un nœud qui montre une donnée fictive, ou un geste depuis la vue qui ne passe pas par les règles.

### R167. Le moteur durable d'ADR-023 : mesurer avant de copier Temporal (second tour)

- **Quoi** :
  - ADR-023 prévoit déjà, en J2, la comparaison avec « une bibliothèque d'exécution durable existante sur PostgreSQL ». Le Conseil
    nomme la candidate : Operaton, moteur BPMN sous Apache 2.0, en Java, embarquable, sur PostgreSQL, issu de Camunda 7, qui publie
    encore.
  - Les critères, écrits avant : la reprise après une coupure du runner, du backend et une mise en veille de la machine ; aucune
    étape faite deux fois ; l'empreinte sur l'app desktop ; la licence compatible avec l'AGPL ; le coût du branchement aux règles
    et au dossier.
  - Zeebe est écarté par sa licence ; Temporal reste possible pour un grand serveur (ADR-023, point 7).
- **L'attaque de la contradictrice** : un moteur embarqué se maintient ; un fork sans éditeur n'a personne à appeler un dimanche.
- **Premier tour** : 21 oui, 1 non (Shotwell), 2 abstentions (Rus : l'empreinte n'a pas de seuil ; Jobs, hors de son champ).
  87,5 %.
- **Amendements** :
  - le seuil d'empreinte sur l'app desktop, écrit avant l'essai (Rus) ;
  - l'activité du projet comme critère : des versions dans les six derniers mois et plusieurs contributeurs (Shotwell) ;
  - la sortie : le modèle de processus ne dépend pas du moteur, et l'export BPMN permet d'en changer (R165).
- **Second tour** : 23 oui, 1 non (Shotwell, maintenu : mesurer coûte un lot que J2 n'a pas). 95,8 %.
- **Preuve en dix jours** : l'essai de coupure joué sur les deux prototypes, les chiffres écrits ; la Présidence tranche.
- **Signal d'arrêt** : le moteur retenu perd une étape, ou en fait une deux fois, pendant un essai de coupure.

### R168. Au-dessus de Camunda : seulement ce qui est prouvé

- **Quoi** : une avance ne se dit en public qu'après sa preuve. La table des huit pistes :

  | Piste | Chez Camunda (dossier) | Chez TaskForce | Avant de l'affirmer |
  | --- | --- | --- | --- |
  | Un travail qui part de l'objectif | ProcessOS, en accès anticipé, propose ; une personne approuve | Rien | Ce n'est pas une avance ; au mieux à égalité (R169) |
  | Des agents qui font le travail | Des agents dans le moteur, outils en activités BPMN | Des missions de code sous les règles ; Copilot hors du runner | La boucle d'agent sur n'importe quel modèle (TF-J2-3), dans un processus |
  | Des règles écrites en mots, au-dessus d'un socle | DMN, autorisations, frontières du processus ; aucun socle sur les actions décrit | En production (TF-J2-4) | L'essai de la Présidence ; la couche du processus |
  | Une preuve qu'un tiers vérifie sans TaskForce | Un journal d'audit sans intégrité décrite | Chaînée et scellée ; pas signée | Le dossier signé, vérifié par un programme indépendant (critère 7) |
  | Le local et le modèle au choix | SaaS ou Kubernetes ; le local hors production | L'app desktop, Ollama pour Cortex | Les missions sur un modèle local (TF-J2-3) |
  | L'AGPL | Production sous licence payante | AGPL v3 | Rien : c'est un fait, à dire avec R106 |
  | Une connexion par personne | Non établi dans le dossier | En production (V126) | L'essai de bout en bout sur de vrais comptes |
  | Une interface sans BPMN à penser | `[DÉDUIT]` Des outils centrés sur BPMN | Rien | R166 |

- **L'attaque de la contradictrice** : une table d'avances est déjà du marketing ; et Dapr signe déjà ses historiques, en
  préversion. Une avance se compte en mois.
- **Vote** : 23 oui, 1 abstention (Nadella : la signature deviendra courante, la différence doit être ailleurs que dans la preuve
  seule). 95,8 %.
- **Preuve en dix jours** : la table dans les notes du produit, chaque ligne avec sa preuve ; les deux premières preuves faites :
  l'essai de la Présidence sur les règles (TF-J2-4), et un dossier vérifié par un programme indépendant (critère 7).
- **Signal d'arrêt** : une avance affirmée en public sans sa preuve.

### R169. L'objectif propose, la personne arrête, le moteur exécute (second tour)

- **Quoi** :
  - « Décrire l'objectif » produit un brouillon de processus, en mots : les étapes, qui fait, qui décide, les règles qui
    s'appliquent. Jamais un processus qui tourne seul.
  - Le brouillon dit ce qu'il ne sait pas, et devient un processus quand une personne nommée l'accepte ; il entre versionné, avec
    son auteur et son empreinte, comme une règle.
  - Avant d'être montré, le brouillon est vérifié par du code : chaque étape a une personne qui en répond (Harari) ; chaque étape
    d'agent a sa zone et ses règles (Bengio, LeCun).
  - À l'exécution, l'agent ne choisit que dans les zones ad hoc du processus, sous les règles. Une étape nouvelle fait une nouvelle
    version ; une instance en cours ne change qu'avec une raison écrite et approuvée (Hamilton).
- **L'attaque de la contradictrice** : un brouillon accepté d'un clic devient un processus que personne n'a pensé.
- **Premier tour** : 20 oui, 3 non (Saarinen, Musk, Harris), 1 abstention (Jobs). 83,3 %.
- **Amendements** :
  - le brouillon s'accepte étape par étape, chacune avec la personne qui en répond ; aucun « tout accepter » ;
  - le brouillon pose ses questions, et la personne y répond avant d'accepter ;
  - partir d'une liste vide, écrite en mots, reste toujours possible (Musk).
- **Second tour** : 22 oui, 1 non (Saarinen, maintenu : un brouillon généré n'est pas une conception), 1 abstention (Jobs).
  91,7 %.
- **Preuve en dix jours** : sur l'objectif d'E20, « intégrer un module », le brouillon proposé, puis corrigé et accepté étape par
  étape par la Présidence ; on compte les étapes changées et les questions posées.
- **Signal d'arrêt** : une étape acceptée que la personne ne sait pas expliquer le lendemain, ou plus de la moitié des étapes
  réécrites : le brouillon ne sert pas.

### R170. E20 et le pitch : un processus, montré de bout en bout

- **Quoi** :
  - Le processus « intégrer un module » (critère 6 de J2) est le premier processus : écrit dans le sous-ensemble (R165), exécuté
    par le moteur retenu (R167), vu et piloté dans la vue du workflow (R166), avec son dossier signé (TF-J2-7). Ses tâches humaines
    portent les points de pause de TF-J2-10 (Gawande).
  - C'est la démo du pitch (TF-J2-1) : la rigueur prise à Camunda (l'instance, l'incident, la reprise, la version), et ce que
    TaskForce y ajoute (la règle en mots qui arrête la bonne étape, la preuve vérifiée sans TaskForce, le modèle local). Aucune
    diapositive contre Camunda (R163).
  - L'ordre, à la demande de la contradictrice : le dossier signé et la vue sur les données vivantes d'abord ; puis le
    sous-ensemble et le moteur ; puis le processus joué, puis le pitch. Un emprunt qui menace la date d'E20 sort de J2 ; le
    critère 6 reste entier, la reprise après un redémarrage comprise.
- **L'attaque de la contradictrice** : quatre lots sur le chemin d'E20, pour une personne, en cinq semaines au plus.
- **Vote** : 23 oui, 1 abstention (Bezos : le communiqué d'E20 d'abord). 95,8 %.
- **Preuve en dix jours** : la définition du processus d'E20 écrite (les étapes, qui fait, qui décide, les règles), puis jouée une
  fois de bout en bout avec une coupure provoquée.
- **Signal d'arrêt** : E20 qui glisse au-delà de la seconde quinzaine de décembre à cause d'un emprunt à Camunda ; l'emprunt sort
  de J2.

### Les votes en une table

| R | Recommandation | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R163 | Le cadre et la phrase | 23 | Nadella | | 95,8 % (20 au premier tour) |
| R164 | Le concurrent n°1 : la cible d'abord | 22 | Shotwell | Bezos | 91,7 % |
| R165 | Les emprunts, un par un | 23 | | Jobs | 95,8 % (20 au premier tour) |
| R166 | La vue du workflow | 23 | | Shotwell | 95,8 % |
| R167 | Le moteur : mesurer avant de copier | 23 | Shotwell | | 95,8 % (21 au premier tour) |
| R168 | Au-dessus : seulement ce qui est prouvé | 23 | | Nadella | 95,8 % |
| R169 | L'objectif propose, la personne arrête | 22 | Saarinen | Jobs | 91,7 % (20 au premier tour) |
| R170 | E20 et le pitch | 23 | | Bezos | 95,8 % |

### Questions à la Présidence

1. **La cible, en une ligne** (R164) : la taille, qui configure (avec ou sans développeur), la première nature de travail. Les
   documents disent « n'importe quelle entreprise » ; le catalogue, « 10 à 500 personnes ».
2. **Le « Claude » de « Claude x Camunda »** : le modèle, ou Claude Code, l'agent qui fait les missions ? La réponse change ce que
   l'on compare.
3. **La pièce collée** : l'assistant qui l'a écrite avait-il reçu les documents de TaskForce ? Sa description de TaskForce,
   « piloté par des objectifs », est une vision, pas l'état réel.
4. **Le moteur** (R167) : accepter l'essai d'Operaton face au moteur maison, sachant qu'il ajoute une dépendance à tenir ?
5. **Se brancher à Camunda** (Q18) : instruire, ou non, TaskForce comme couche de règles et de preuve appelée par MCP depuis un
   processus Camunda, comme la question posée pour n8n (Q14) ?
6. **La maquette de la vue** (R166) : la voir avant de trancher R166, ou trancher d'abord ?

## Décision de la Présidence

Tranchée le 13/11/2026 au soir, en conversation, en un seul message. Sur l'ensemble : « Ce qu'il faut trancher avec ma
recommandation. Donc R163 à 170, donc je retiens, hein, prends en compte tout ce que je viens de te dire pour le process, et puis
peut-être que tu peux valider ça avec le conseil, mais moi je suis plutôt convaincu de ce que je dis. » Et, à la fin du message :
« On repasse ça au conseil pour valider, mais moi je suis à peu près sûr de ce que je dis, donc go. »

- **R163, retenue et amendée : se repositionner.** « Écoute, le R163, oui, bah, je crois qu'on l'avait déjà fait, mais écoute, on
  peut essayer de se repositionner peut-être. » Le repositionnement vient de sa réponse à la deuxième question, plus bas :
  l'expérience de Claude Code, où l'on pilote, plus des applications embarquées.
- **R164, retenue : la cible, « à peu près ».** « R164, bah, c'est la même chose. » Sur la ligne de la cible : « Bon bah la cible en
  une ligne, tu l'as aussi, à peu près, hein. » Cette ligne, que l'agent lui avait proposée en conversation et qu'elle tient « à peu
  près » : « des entreprises de 10 à 500 personnes, sans développeur dédié pour configurer, dont le premier travail est la
  livraison logicielle et les documents ». Puis des marchés plus complexes :
  - « Parce que voilà, eux aussi, c'est partir de l'objectif, mais du coup, on peut peut-être faire la même chose, mais nous partir
    sur vraiment des marchés un petit peu plus complexes. » ;
  - « Très intéressant s'ils n'ont pas de IQ, OQ, PQ, parce que ça va rester, et surtout j'ai déjà un petit peu d'expérience
    là-dessus, donc on pourra limite presque tester en fait. »

  Sur Camunda comme concurrent : « Et puis après, bah voilà, hein, si on est concurrent par rapport à Camunda, c'est pas non plus
  dégueu. Ils ont 700 clients, mais il y a certainement des millions d'entreprises encore qui n'ont pas ce genre de choses et qui
  demandent ce genre de choses. » La question du marché, qui ouvre le message, va à la séance n°26.
- **R165, retenue et élargie.** « R165, effectivement, donc voilà, un sous-ensemble de BPMN pour nos processus, donc il faut déjà
  pouvoir réussir à qualifier nos processus. » Les élargissements, dans ses mots :
  - **pas seulement l'échange** : « Après, voilà, import-export seulement, bah, effectivement on peut rajouter un import-export,
    mais pas seulement, du coup, hein, je pense qu'on peut en proposer un par défaut. » ;
  - **des workflows par défaut** : « par exemple un workflow par défaut qu'on peut créer qui nous paraît très bien pour n'importe
    quel développeur, n'importe quelle personne qui souhaiterait créer quelque chose ou simplement voilà éditer un document,
    etc. » ; « On peut en faire un par type d'action » ;
  - **nos agents les créent selon des règles, des conventions et des exemples** : « Est-ce que nos agents peuvent créer des BPMN en
    fonction des règles, des conventions? Est-ce que voilà, il y a différentes règles pour pouvoir créer des BPMN? Est-ce qu'il y a
    des exemples? Est-ce qu'on peut entraîner un agent exprès là-dessus, etc. » La question de l'entraînement va à la séance n°25 ;
  - **l'IA juge ce qui est de trop** : « je pense que ce serait top avec vraiment l'IA qui dit ok, bon bah ça c'est overkill, on le
    fait pas, donc on va passer uniquement là-dedans dans le workflow. Ou alors voilà, ça c'est un truc un peu spécifique, donc on
    va utiliser l'ensemble du workflow » ;
  - **des workflows créés et paramétrés par les utilisateurs, l'exemple du LIMS** : « des workflows du coup plus spécifiques que
    même les utilisateurs pourraient eux-mêmes créer, paramétrer. Par exemple, je dis n'importe quoi, je développe une
    application, un LIMS, et ben là, il me faudrait vraiment un workflow dédié pour ça, avec peut-être justement moi qui vais
    construire la partie IQ, OQ, PQ qui manque, la partie vraiment aller chercher les bons documents, GAMP, 21 CFR partie 11,
    etc. » ; « Donc je vais venir rajouter ça au workflow proposé par exemple par l'IA. Par notre modèle. » ;
  - **affichés et édités dans TaskForce, par les ingénieurs et par les PM** : « Jamais affiché à l'écran, ça je sais pas, je pense
    que ça devrait s'intégrer à nous les workflows qu'on va pouvoir afficher et éditer par les ingénieurs, les utilisateurs, etc.
    Et puis par les PM aussi, hein, qui peuvent très bien faire des agents de gestion de projet exprès, s'ils ont des règles à
    afficher. » ;
  - **les types d'étapes** : « 5 types d'étapes, ok, ça je te laisse faire, il y en a peut-être plus, je ne sais pas, mais en vrai
    je pense pas. Ça me paraît ok. » ;
  - **pas orienté full code** : « Attention, on n'est pas orienté full code, hein. Ça c'est peut-être une erreur, mais voilà, faut
    bien définir ça. » ;
  - **définir, exécuter, exploiter, la version, et ce qui attend** : « Donc séparation, définir, exécuter, exploiter, et la version
    de chaque processus, effectivement. Et puis la gestion, effectivement aussi, des incidents, des waiting lists, des approvals,
    et ce genre de choses. Des manques aussi, hein, s'il manque des documents que l'IA est en attente ou autre. »

  L'amendement voté par le Conseil (J2 ne prend que ce qu'exige le processus « intégrer un module ») n'est pas touché ; la séance
  n°25 dit ce qui entre dans J2.
- **R166, retenue et amendée : s'inspirer de Camunda, sans ses symboles.** « Alors, bah là, je pense qu'il faudrait s'inspirer
  quand même de Camunda. Peut-être le simplifier au niveau UX, mais enfin le simplifier. Je suis pas en train de faire des schémas
  d'ELEC, hein, eux ils ont des symboles assez particuliers, enfin vachement mathématiques, hein, ou informatiques avec les
  conditions, donc nous on va pas faire ça, on va quand même simplifier ça. Mais je pense que c'est quand même important d'avoir
  ça, et puis comme je te dis, si on peut piloter les workflows, ça peut vraiment être très cool. » Le public :
  - « Moi, mon but, c'est aussi qu'un CEO puisse absolument comprendre ce qui se passe là-dedans et puisse en faire quelque chose.
    Qu'un PM puisse aussi utiliser cet outil absolument sans problème » ;
  - pour la partie technique, « parce qu'il faut qu'on soit très précis » ;
  - garder la simplicité d'aujourd'hui et y ajouter volontairement : « garder ce qu'on a actuellement, qui est quand même
    relativement simple, entre guillemets, qui nécessiterait peut-être d'être simplifié au niveau de l'UI/UX pour les PM, ou pour
    des gens en tout cas de ce niveau d'hiérarchie-là, qui sont un peu moins hands-on, et puis le complexifier volontairement avec
    ce que Camunda, par exemple, propose ».

  La maquette ne précède pas la décision (sixième question, plus bas).
- **R167, retenue et amendée : pas de fork d'Operaton.** « Voilà, ensuite R167 pour le moteur durable comparé Operaton, un moteur
  fait maison, sur les mêmes essais de coupure. Effectivement, on peut essayer ça. Ok, alors après faire un fork, je suis
  peut-être pas fan, mais on peut s'en inspirer en tout cas, hein. Donc tu peux aller voir le code sans problème, et t'en inspirer.
  Mais faire un fork direct, ça je suis pas fan. Parce que ça fait vraiment copier-coller pour le coup. » Et sur l'essai : « Et puis
  l'essai d'Opératon. Alors, oui, mais je préfère que tu copies le code plutôt que tu fasses, enfin, que tu copies, que tu
  t'inspires du code, que tu ailles voir vraiment les fichiers, comment ça fonctionne, que tu reproduises la même chose chez nous,
  adapté évidemment à chez nous, plutôt que tu fasses un fork directement. Donc c'est peut-être plus de boulot, mais je préfère
  largement. » ADR-023 est amendé dans ce sens.
- **R168, retenue.** « R168, ne dire au-dessus de Camunda que ce qui est prouvé. Oui, effectivement. »
- **R169, retenue, Jobs sur l'UX.** « R169, l'objectif repose un brouillon de processus. Une personne la règle, le moteur exécute.
  Bon, ça tu vois, faudrait peut-être mettre Jobs sur la partie UX, encore une fois. »
- **R170, retenue**, avec les autres : « Donc R163 à 170, donc je retiens ».

**Les réponses aux six questions du Conseil :**

1. **La cible** : voir R164.
2. **Le « Claude » de « Claude x Camunda »** : l'expérience, pas le modèle.
   - « Alors, le Claude de Claude X Camunda, je pensais plutôt à l'expérience, plutôt que le modèle. Voilà, c'est-à-dire que c'est
     vraiment expérience Claude Code, c'est-à-dire qu'on pilote vraiment, on a vraiment l'impression de piloter quelque chose, et à
     côté, voilà, on a des fenêtres spécifiques qui permettent de nous montrer par exemple le board, par exemple les workflows, et
     de pouvoir, dans le board évidemment, piloter un board comme si on était sur Linear, piloter des workflows comme si on était
     sur Camunda. »
   - « c'est vraiment un espèce de Claude vide, avec des agents que nous on possède, hein, donc sans Opus par exemple, tout ça, on
     peut brancher Claude dessus, mais c'est vraiment expérience Claude, plus des applications embarquées en fait, si tu veux, c'est
     vraiment ça. On fait vraiment de l'applicatif embarqué là, si tu veux. »
3. **La pièce** : « Et l'assistant qui a écrit ma pièce, non, il n'avait pas les documents parce que c'était sur ChatGPT, voilà,
   très rapidement. »
4. **Le moteur** : voir R167 : l'essai, oui ; le fork, non.
5. **Se brancher à Camunda** (Q18) : oui, plus tard.
   - « Donc se brancher à Camunda, effectivement, plus tard, pour essayer de récupérer un petit peu ce qu'ils font de bien aussi, et
     ce que nous, bah, on va pas refaire non plus. » ; « Donc se brancher à Camuda, ça tu le feras plus tard. »
   - Le but : « pourquoi pas s'intégrer après à Camunda pour vraiment faire la séparation entre les deux et vraiment montrer ce que
     nous, on apporte en plus à Camunda et ce qui représente effectivement une partie supérieure à Camunda qui ne le ferait pas, par
     exemple. »
6. **La maquette** : pas avant de trancher. « La maquette avant de trancher, non, tu peux faire tout d'un coup. Enfin, discute avec
   Jobs et tout, essaye de faire une UX sympa. Essaye d'aller t'inspirer peut-être voilà, d'écrans qui existent déjà, de reprendre la
   DA aussi évidemment, de reprendre aussi ce que fait Claude au niveau de ses différents embarquements d'applications entre
   guillemets. Hein. Mais voilà, je pense qu'on n'a pas besoin de maquette directement. »

**La méthode** : le chantier suit le message entier (« prends en compte tout ce que je viens de te dire pour le process »), et le
Conseil le revoit avant la construction (« On repasse ça au conseil pour valider ») : c'est la séance n°25, tenue le même soir.

## Notes du secrétariat

- **Le dossier** : sur Camunda, seulement ses propres pages, lues le 13/11/2026 ; sur ses voisins, leurs pages officielles,
  relevées par un agent de recherche du secrétariat, dont deux faits revérifiés à la source. Le dossier complet du secrétariat,
  avec un lien et une date par fait, accompagne ce PV. Les résumés des moteurs de recherche n'ont servi qu'à trouver les pages.
- **Corrections du brief de séance** :
  - GitHub Copilot ne passe pas par le runner local : c'est l'agent cloud de GitHub, lancé par l'API des tâches d'agent de GitHub,
    qui revient en pull request ; `[DÉDUIT]` les règles de TaskForce ne jugent pas chacune de ses actions ;
  - « 104 outils branchés par MCP » : 104 préréglages, dont 102 serveurs MCP et deux API (Google Drive, Microsoft 365) ; cinq sont
    fermés ; aucun n'a passé l'essai de bout en bout sur de vrais comptes ;
  - le dossier signé et vérifiable hors de TaskForce n'existe pas, mais un dossier chaîné et scellé existe, exporté et vérifié par
    le runner.
- **Corrections des documents** :
  - la ligne TF-J2-12 de la roadmap dit encore « reste sa fusion » pour la PR #531, que la note ▶ du 13/11 donne en production
    avec la 1.16.0 ;
  - le Journal n'a pas d'entrée pour la séance n°23 du 12/11.
- **La pièce de la Présidence** : sa description de Camunda est en retard sur les faits (des agents dans ses processus depuis
  10/2025, ProcessOS depuis 05/2026) ; sa description de TaskForce est une vision. Sa mise en garde finale est confirmée.
- **Hors fiche, hors champ** :
  - Bezos : « le communiqué d'abord » est la méthode d'Amazon, pas une position de sa fiche ;
  - Duflo, Gawande, Li et Doudna parlent d'agents logiciels au-delà de positions publiques minces sur ce sujet (limites de leurs
    fiches) : leurs interventions transposent leur méthode ;
  - Jobs, hors de son champ sur le moteur, s'abstient au premier tour de R167.
- **Anachronismes** : Jobs et Hamilton ne connaissent Claude, Camunda et MCP que par le dossier.
- **Conflits d'intérêts** :
  - Nadella dirige Microsoft, voisin direct (Copilot Studio, Power Automate, Agent 365), dont GitHub Copilot est le second agent de
    TaskForce ; c'est Microsoft qu'il a désigné comme le concurrent qu'il voit d'abord ;
  - Saarinen dirige Linear, concurrent de TaskForce sur la gestion de projet avec agents ; Zhuo rejoint Meta ;
  - le secrétariat et l'agent de recherche sont des modèles d'Anthropic ; le cadre de la saisine nomme Claude ; Claude Code est le
    premier agent de TaskForce ; Camunda et Copilot Studio proposent Claude parmi leurs modèles.
- **Sources manquantes** : les effectifs de Camunda ; la date de sortie de la 8.9 ; le placement de Camunda dans l'édition 2026
  du Magic Quadrant BOAT (la page de Gartner refuse la lecture) ; le modèle des secrets des connecteurs de Camunda ; le niveau de
  maturité des fonctions agentiques de la 8.10 ; chez les voisins, l'hébergement et les prix de ServiceNow et d'Appian, et les
  annonces d'Ignite 2026, qui se tient après la séance.
- **Après la décision** (13/11/2026 au soir) :
  - **la pièce** : écrite sur ChatGPT, sans les documents de TaskForce, d'après la Présidence ; cela explique qu'elle décrive une
    vision plutôt que l'état réel ;
  - **IQ, OQ et PQ** : la Présidence dit en avoir l'expérience, et les place avec un LIMS, GAMP et 21 CFR Part 11 ; le sens noté
    `[DÉDUIT]` à Q13 le 30/10 (la qualification d'un équipement ou d'un système dans les industries réglementées) est confirmé ;
  - **« pas de fork » et la licence** : Operaton est sous Apache 2.0 ([dépôt](https://github.com/operaton/operaton), lu le 13/11/2026) ;
    l'ASF tient les deux licences pour incompatibles dans un seul sens : du code sous Apache 2.0 peut entrer dans un projet sous
    GPLv3, pas l'inverse ([ASF](https://www.apache.org/licenses/GPL-compatibility.html), lu le 13/11/2026). `[DÉDUIT]` Reprendre un
    fichier d'Operaton dans TaskForce, sous AGPL v3, reste possible s'il garde sa mention de droit d'auteur, la licence et le fichier
    NOTICE (Apache 2.0, §4) ; la Présidence préfère reproduire le mécanisme, adapté ;
  - **les cinq types d'étapes** : la Présidence laisse la main au secrétariat et au Conseil, et dit que cinq lui paraissent
    suffire (« en vrai je pense pas » qu'il y en ait plus) ;
  - **la ligne de la cible** n'est pas des mots de la Présidence : c'est celle que l'agent lui avait proposée, et qu'elle tient « à
    peu près » ;
  - **le conflit d'intérêts** du secrétariat s'étend : l'expérience que la Présidence retient porte le nom d'un produit d'Anthropic,
    Claude Code ; le choix de cette référence est le sien, et les agents de TaskForce restent sur n'importe quel modèle (R92).
- **L'avis du secrétariat**, après la clôture : le mien, pas celui du Conseil.
  - `[DÉDUIT]` Camunda ne fait pas exactement ce que TaskForce veut faire. Il orchestre des processus, très bien, pour les grandes
    organisations, et y met des agents depuis un an. TaskForce délègue du travail à des agents sous des règles, avec une preuve,
    et n'a pas encore de processus. Le recouvrement est réel dans l'intention, pas dans le produit.
  - `[DÉDUIT]` Les emprunts les plus utiles sont les moins chers s'ils se font dès le départ : séparer la définition, l'instance et
    sa version ; l'incident comme objet ; ce qu'attend chaque instance. Les plus chers (Optimize, DMN, les connecteurs, BPMN entier)
    ne servent pas E20.
  - `[DÉDUIT]` Le plus grand risque est de faire de J2 une course pour rattraper Camunda et de manquer E20 ; le second, de dire
    « au-dessus » avant la preuve.
  - **Mon ordre** : la ligne de la cible et E14 ; la maquette de la vue, avec la Présidence ; la mesure de R167 avant d'écrire un
    moteur ; puis le critère 7, parce que la preuve vérifiée par un tiers est la seule avance qu'aucun voisin ne revendique.

## Suites

- Le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal.
- Deux questions ouvertes : Q17 (le concurrent n°1 et la cible), Q18 (se brancher à Camunda).
- Après la décision de la Présidence, rangé le 13/11/2026 au soir :
  - au registre de la charte (§12) et au Journal : « la Présidence tranche la séance n°24 » ;
  - à `Questions-ouvertes.md` : Q17 en cours (la cible, tenue « à peu près ») ; Q18 tranchée (se brancher à Camunda, plus tard) ;
  - à `experiences/Experiences.md`, les preuves en dix jours retenues : E14 élargie (la phrase, et les noms des concurrents cités) ;
    E21, l'essai de coupure, Operaton en témoin (R167 amendée) ; E22, le brouillon d'E20 (R169) ; E23, le processus d'E20 dans le
    sous-ensemble, aller et retour (R165) ; E24, la vue lue en une minute à ses trois lectures (R166 amendée) ;
  - ADR-023 amendé (R167 : les mécanismes de Temporal et d'Operaton refaits chez nous, sans fork) ; ADR-027 ouvert en brouillon,
    le modèle des processus (R165, R169) ;
  - le chantier repassé au Conseil : la [séance n°25](./2026-11-13-le-workflow-pilotable.md), le workflow pilotable ; le marché,
    à la séance n°26 ;
  - à la roadmap, en mode développement : TF-J2-2, TF-J2-6, TF-J2-1 et TF-J2-11 précisés après la séance n°25 ;
  - la page de comparaison (R163) et la table des avances (R168) dans les notes du produit ;
  - la maquette de la vue du workflow (R166) : retirée par la Présidence (sixième question).
- Rien ne migre vers `v1/` sans tâche ni ADR (quarantaine, [`CLAUDE.md`](../../CLAUDE.md) §2).

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
