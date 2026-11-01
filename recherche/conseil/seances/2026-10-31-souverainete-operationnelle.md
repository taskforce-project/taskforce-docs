---
id: conseil-seance-2026-10-31-souverainete-operationnelle
title: "Séance n°14 du 31/10/2026 : TaskForce face au texte de la « souveraineté opérationnelle de l'IA »"
doc_type: pv-seance
statut: active
date: "31/10/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, vision, positionnement, souverainete, etat-des-lieux]
related:
  - "../README.md"
  - "./2026-10-27-vision.md"
  - "./2026-10-29-intelligence-possedee.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°14 du 31/10/2026 : TaskForce face au texte de la « souveraineté opérationnelle de l'IA »

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **Décidé le 01/11/2026** : la Présidence a dit son accord avec tout le Conseil, avec des orientations qui modifient
> plusieurs recommandations. La décision est plus bas ; la [séance n°15](./2026-11-01-feuille-de-route.md) en tire les
> suites.

## Résumé

La Présidence demande où en est TaskForce face à un texte de ChatGPT qui décrit une « plateforme de souveraineté
opérationnelle de l'IA », et si ce texte n'est pas ce qu'un dirigeant veut entendre.

Le Conseil répond en trois points.

1. **Le texte est compétent, et presque entièrement générique.**
   - C'est l'architecture que vendent en 2026 Microsoft, AWS, Google, OpenAI, ServiceNow et IBM.
   - Il ressemble à TaskForce (sa pile, ses mots, sa direction du 29/10), d'où l'impression d'une validation.
   - Il ne dit presque rien de ce qui décide : un client, un prix, la validation en GxP, la concurrence, une équipe
     d'une personne. Ses meilleures phrases sont ses mises en garde.
2. **TaskForce face au texte** :
   - **pile** sur la thèse et sur l'ordre (le contexte et les règles avant l'affinage), tranchés avant ce texte ;
   - **devant** sur un morceau étroit : la porte de règles prouvée en Java et en TypeScript, le dossier chaîné
     vérifiable par d'autres, le local ;
   - **derrière** sur presque tout le reste :
     - les documents, les processus, les objectifs ;
     - les systèmes d'entreprise, les règles réglables par le client ;
     - la passerelle de modèles, l'observabilité ;
     - et tout le commerce ;
   - **ailleurs** dans les faits : un établi gratuit qui délègue des issues de code à Claude Code, avec neuf utilisateurs
     réels, aucun client, aucun partenaire, aucune expérience menée.
3. **Ce qu'il recommande** (R81 à R89) :
   - ne pas faire de ce texte la feuille de route ;
   - dire vrai avant de dire plus ;
   - mesurer avant de construire ;
   - un geste, une personne ;
   - la pharmacie plus tard, par un partenaire ;
   - les règles au client ;
   - une preuve digne d'un auditeur, et « Apply » qui respecte les tests ;
   - la fiabilité avant une couche de plus ;
   - publier le contrat et l'essai de l'effet.

Désaccords conservés :
- **Satya Nadella**, contradicteur : la porte et la preuve sont devenues un produit standard ; l'avance se compte en
  mois ; la différence est ailleurs.
- **Nandan Nilekani** : publier le contrat de règles maintenant, contre R9'.
- **Kenza Ait Si Abbou, Jennifer Doudna et Mariana Mazzucato** : ne pas repousser la cible régulée.
- **Elon Musk** : supprimer d'abord, à commencer par la webapp et les connecteurs jamais essayés.

Décision de la Présidence (01/11/2026) : accord avec tout le Conseil, avec ses orientations (plus bas).

- **Saisine** (Présidence, 31/10/2026) : la Présidence apporte un texte produit par ChatGPT, qui décrit une « plateforme de
  souveraineté opérationnelle de l'IA ». Elle demande au Conseil :
  - « a quel point on est proche de ca, si on est devant ca, derriere ca, si on fait autre chose, si on fait pile ca ou
    on va vers ca » ;
  - « un topo complet de taskforce actuellement » ;
  - si ce texte n'est pas « vraiment limite ce qu'un CEO d'entreprise voudrait entendre » ;
  - « l'avis du conseil complet sur tout les points », « l'avis de tout le monde, detaille, bien explique », avant de
    consigner quoi que ce soit ; des documents seront sans doute à modifier ensuite.
- **Horizon** : l'état d'aujourd'hui, et la direction à trois ans.
- **Formation** : plénière, 24 membres. C'est une question de positionnement (charte, §5). La Présidence demande des
  interventions détaillées : chaque membre parle plus longuement que les cinq à huit lignes d'usage.
  - Ordre de parole tiré au sort le 31/10/2026 à 20:19 UTC (`shuf`).
  - Contradicteur désigné : Satya Nadella. Microsoft vend déjà une couche de gouvernance des agents ; il est le mieux
    placé pour attaquer le consensus qui se formera. Norman l'était à la n°13.
- **Fiches** : toutes à jour (moins de 30 jours ; les plus anciennes datent du 21/10/2026). Jobs et Hamilton, sièges
  historiques, ne se rafraîchissent que sur une nouvelle source historique.

## Le texte apporté, en résumé

Le texte (environ 5 000 mots, en français) propose, dans l'ordre :

1. **La thèse** : ne pas développer un LLM, mais l'infrastructure qui permet à une entreprise de faire de ses données, de
   ses règles et de ses processus un système d'IA qu'elle contrôle : « une couche de contrôle entre les modèles, les
   données, les processus métier et les systèmes de l'entreprise ».
2. **Cinq souverainetés** : des données, des modèles, du métier (règles et procédures versionnées), des agents (outils,
   actions, validations, arrêts), opérationnelle (auditer, reproduire, revenir en arrière, changer de fournisseur).
3. **Six couches** : un cockpit de pilotage (des objectifs, pas des prompts) ; un moteur de contexte de l'entreprise
   (documents, données opérationnelles, processus, règles et responsabilités, historique, reliés en graphe) ; un runtime
   d'agents (planificateur, exécutant, vérificateur) ; un moteur de politiques séparé d'une passerelle de modèles ; les
   intégrations (ERP, CRM, LIMS, GED, qualité) ; l'audit et l'évaluation, transversaux.
4. **Quatre façons d'adapter l'IA** : contexte et RAG (priorité 1), moteur de règles (priorité 1), affinage (priorité 2),
   petits modèles spécialisés et distillation (priorité 3) ; l'affinage seulement quand les évaluations montrent un gain.
5. **Un parcours d'arrivée en huit étapes** : connecter les sources, comprendre et normaliser, formaliser processus et
   règles, définir les compétences des agents, construire les évaluations, tester les modèles, déployer par paliers
   (lecture, préparation, exécution limitée), améliorer à partir des résultats.
6. **Une grille de variables** (confidentialité, criticité, stabilité des connaissances, complexité des processus,
   qualité des données, autonomie, calcul, portabilité, coût, responsabilité, observabilité).
7. **Un exemple** : les déviations qualité dans une usine pharmaceutique, avec le LLM qui propose et l'humain qui
   arbitre ; aucune libération de lot par le modèle.
8. **Trois phases** : un noyau sur un cas étroit, la personnalisation contrôlée, puis l'entreprise pilotée par des agents.
9. **Une pile technique** : Java et Spring Boot, React et Next.js, PostgreSQL et pgvector, stockage compatible S3,
   Temporal, OIDC et RBAC, OpenTelemetry, vLLM ou Ollama, Docker Compose puis Kubernetes.
10. **L'opportunité** : « un système d'exploitation des opérations métier par l'IA », d'abord en secteur régulé ; la
    promesse « automatiser vos processus avec l'IA sans perdre le contrôle de vos données, de vos règles ni de vos
    décisions » ; et une question finale : une infrastructure installée par des équipes techniques, ou une plateforme
    métier qui cartographie l'entreprise.

## Dossier

Constitué le 31/10/2026 par cinq relevés du secrétariat : quatre sur le code (`taskforce-fullstack`, `dev` au commit
`6ab62b1d`, comparé à `main`, la production) et les notes de conception, un sur le marché et la réglementation, à partir
de pages lues le jour même. La Présidence demandant un état complet, le dossier compte douze points au lieu de cinq à
dix.

1. `[ÉTABLI]` **Ce que TaskForce est aujourd'hui, en production** (webapp 1.6.8, app desktop 1.3.8).
   - Un outil de gestion de projet : espaces, projets publics ou privés, issues, cycles, équipes, compétences.
   - Un assistant, Cortex, derrière une barre unique sur chaque écran (R76). Il a sept outils internes et jusqu'à douze
     outils MCP de l'espace, et fait cinq tours au plus. Chaque appel est jugé par le moteur de règles et tracé avant
     d'agir. Ce qu'il crée se défait d'un geste tant que rien n'a bougé
     (`backend/tf-api/.../core/service/agent/AgentService.java`, `CortexGate.java`, `CortexUndo.java`).
   - La délégation d'une issue de code à Claude Code, sur l'ordinateur de la personne, par le runner local.
     - L'agent travaille dans une copie de travail git, sur une branche.
     - Les règles sont rejugées à chaque action, et les accords se demandent à la personne.
     - Les tests du projet sont lancés par le runner, et la pull request est ouverte par le runner.
     - Un dossier de preuve chaîné (SHA-256) s'exporte en JSON et en Markdown, et se vérifie sans TaskForce
       (`taskforce-runner/src/`, `.../delivery/MissionEvidenceService.java`).
   - Copilot est un second fournisseur, sans les règles ni le dossier de TaskForce, jamais essayé (spécification §10.2).
     Le fournisseur « Claude API » a été retiré le 18/10/2026.
   - En dev, pas encore publiés : les trois écrans de R78, « Créer », « Accorder » et « Relire » (#456 à #458).
   - Le site promet « Delegate to AI agents. Keep the final say. » (`landing-page/src/pages/index.astro`). Le produit est
     gratuit, sous AGPL ; Stripe et les offres payantes ont été retirés le 18/10/2026 (`.ai/roadmap.md`).
2. `[ÉTABLI]` **Les moyens.**
   - Un fondateur seul (`v1/01-projet/Note_Cadrage.md`).
   - 9 utilisateurs réels au 08/09/2026 (`.ai/roadmap.md`). Le chiffre du jour n'a pas été lu : l'accès aux métriques
     de la production demande une validation de la Présidence.
   - Un e-mail de lancement prévu pour environ huit personnes (`marketing/emails/2026-10-desktop-launch/README.md`).
   - Aucun partenaire de conception (Q13 : « plus tard »), aucun revenu, aucune certification.
   - La webapp et le serveur de comptes, dont l'app desktop a besoin à sa première connexion, tournent sur des machines
     de l'école qui s'arrêtent. Le VPS d'OVH n'est pas encore pris (Q13).
   - Les sauvegardes restent sur la même machine, non chiffrées, sans les fichiers joints (`ops/backup/README.md`).
3. `[ÉTABLI]` **La direction déjà tranchée par la Présidence.**
   - R5' (séance n°2) : « Vous décrivez le résultat ; TaskForce le fait faire par l'agent de votre choix, avec vos outils
     et vos règles, et vous montre qu'il est bon. » Niche A d'abord (les équipes logicielles qui utilisent déjà des
     agents), niche B ensuite, en vitrine (embarqué, défense, aérospatial).
   - R1 (séance n°1) : aucun agent ne décide seul d'une action irréversible, ni de ce qui est irréversible.
   - R60 à R65 (séance n°10, 29/10/2026) :
     - posséder son intelligence (règles, dossiers, évaluations, puis modèles) ;
     - la boucle avant les poids ;
     - le coût nul par la machine du client ;
     - la conformité par un partenaire ;
     - ce qui est possédé part avec le client ;
     - les mots avant la page.
   - R56 (séance n°9) : un objectif, une date cible, des critères de réussite. R57 : aucun écran ne surveille les agents ;
     la spécification refuse « un tableau de bord de suivi » (§15).
4. `[ÉTABLI]` **Les expériences du labo : aucune n'a été menée.**
   - E7 à E15 sont toutes « proposées » (`recherche/experiences/Experiences.md`). E13 (un spécialiste gagne-t-il du temps
     sur un vrai dossier ?) et E14 (la promesse se redit-elle en une phrase ?) demandent des personnes extérieures.
   - La seule observation réelle : à la recette de la 1.3.2, trois accords sur quatre portaient sur du réversible
     ([PV n°8](./2026-10-29-recette-132.md)).
   - En six jours, le Conseil a formulé quatre-vingts recommandations.
5. `[ÉTABLI]` **La pièce forte : le moteur de règles.**
   - Un contrat de 35 règles : 17 permises, 13 demandées, 5 refusées. Les classes : 5 lecture, 5 écriture dans le bac à
     sable, 8 sortie réversible, 17 irréversible (`contracts/rules/default.rules.json`).
   - Le même moteur en Java et en TypeScript, prouvé par les mêmes cas (51 décisions, 18 motifs, l'empreinte), rejoués
     par la CI des deux côtés (`contracts/rules/cases.json`).
   - Fermé en cas de panne (`onFailure: block`) ; versionné par empreinte, que le runner vérifie avant toute mission.
   - **Ses limites** :
     - Aucun écran ni aucune API ne permet à un client de modifier ses règles ; la table par espace (V102) n'est jamais
       écrite. Chaque espace reçoit la même table (`.../core/harness/rules/HarnessRulesService.java`).
     - Le moteur ignore la classe d'une règle. Onze des trente actions du contrat ne sont produites par aucun code. Les
       actions inverses ne s'exécutent pas : « Undo » supprime.
     - Aucun seuil, aucune double signature, aucune séparation des rôles.
6. `[ÉTABLI]` **Le contexte de l'entreprise est le grand manque.**
   - Le Brain OS tourne en production (graphe, vecteurs de 1 024 dimensions, index HNSW), mais n'a plus d'écran depuis
     le 28/10/2026. On le rencontre par les sources de Cortex et l'outil MCP `brain_search`.
   - Aucun document n'est lu, versionné ou découpé : ni PDF ni Word. Le « jour 2 » du sprint (les documents et leurs
     versions, spécification §5) n'a pas été construit.
   - Une note n'a ni version, ni propriétaire, ni date de validité ; elle se réécrit en place.
   - Aucune donnée opérationnelle d'entreprise (produit, lot, fournisseur, équipement), aucun processus modélisable. Le
     canevas « AI Workflows » montre un plan d'analyse fixe, en lecture seule.
   - La recherche ne respecte pas encore tous les droits des projets privés. Une correction est proposée ; le détail
     reste hors du PV, les dépôts étant publics.
   - Conséquence : le premier cas d'usage ne peut pas tourner, puisqu'il commence par importer deux versions d'un
     standard (spécification §17).
7. `[ÉTABLI]` **Modèles, évaluation, observabilité.**
   - Une seule API compatible OpenAI par instance (`ai-service/app/config.py`).
     - En production web : Groq, offre gratuite, avec un frein d'une requête par minute et par compte, sans fournisseur
       de secours.
     - Dans l'app desktop : Ollama, sur la machine.
   - Ni registre des modèles par tâche, ni routage par espace, ni budget (les quotas par offre ont été retirés).
   - Ni affinage ni export de données d'entraînement ; E12 est proposée.
   - Les missions déléguées ne peuvent pas utiliser un modèle local (R51 n'est pas construit) : posséder son modèle ne
     vaut aujourd'hui que pour Cortex.
   - La banque d'évaluations (1.6.7) est manuelle et réservée à Cortex : cas figés, rejeu à blanc, notation par du code.
     Elle n'a ni cas proposés, ni évaluation de sûreté.
   - Le dossier de mission n'est pas signé et disparaît avec son issue. Aucune durée de conservation ne s'applique aux
     dossiers.
   - OpenTelemetry n'est pas activé en production. Le journal d'audit compte sept actions d'administration, aucune
     action d'IA.
8. `[ÉTABLI]` **Ce qui est écrit et n'est pas vrai.**
   - L'architecture dit qu'aucun contenu de travail ne quitte l'infrastructure (`v1/03-architecture/Architecture.md`). En
     production, les questions à Cortex partent chez Groq, et la politique de confidentialité de la webapp ne le nomme
     pas.
   - Les pages légales du site disent le serveur de comptes hébergé par OVH en France. Il tourne sur les machines de
     l'école.
   - La règle par défaut `search-knowledge` dit que la recherche filtre par sensibilité et par droits. Ce n'est pas le
     cas.
   - La spécification dit que le dossier survit à l'issue (§9.4) : il est supprimé avec elle.
   - L'ADR-010 (OpenTelemetry vers SigNoz) n'est pas appliqué. L'ADR-021 promettait l'app desktop sans compte : elle en
     demande un.
   - Le modèle de prix marqué « valide » décrit des offres payantes ; le produit est gratuit.
   - Le site annonce la fermeture de la webapp, la spécification la garde.
9. `[ÉTABLI]` **Le marché a rejoint le texte, et il est occupé.**
   - Les grandes plateformes vendent maintenant des plans de contrôle d'agents :
     - Microsoft Agent 365, disponible le 01/05/2026, avec registre d'agents, identités et protection des données
       ([Microsoft](https://learn.microsoft.com/en-us/microsoft-agent-365/overview)) ;
     - AWS AgentCore Policy, en règles Cedar, disponible en 03/2026, puis un harnais géré en 06/2026
       ([AWS](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/release-notes.html)) ;
     - Google Gemini Enterprise Agent Platform, le 22/04/2026
       ([Google](https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform)) ;
     - OpenAI Frontier, le 05/02/2026
       ([TechCrunch](https://techcrunch.com/2026/02/05/openai-launches-a-way-for-enterprises-to-build-and-manage-ai-agents/)) ;
     - ServiceNow AI Control Tower, étendu le 05/05/2026
       ([ServiceNow](https://newsroom.servicenow.com/press-releases/details/2026/ServiceNow-expands-AI-Control-Tower-to-discover-observe-govern-secure-and-measure-AI-deployed-across-any-system-in-the-enterprise/default.aspx)) ;
     - IBM, un plan de contrôle agentique le 02/07/2026
       ([IBM](https://www.ibm.com/new/announcements/introducing-the-agentic-control-plane)).
   - Les éditeurs qualité de la pharma ont déjà des agents relus par l'humain, dans des systèmes déjà validés :
     - Veeva, un agent de déviation dans Vault QMS ([Veeva](https://quality.veevavault.help/en/lr/1006459)) ;
     - MasterControl, l'Event Summarizer, sur une plateforme certifiée ISO 42001
       ([MasterControl](https://www.mastercontrol.com/news/mastercontrol-ai-event-summarizer/)) ;
     - Kivo, un accès MCP en lecture seule ; ses agents proposent, les humains exécutent
       ([BioSpace](https://www.biospace.com/press-releases/kivo-launches-headless-gxptm-to-power-compliant-agentic-ai-in-drug-development)) ;
     - Compliance Group, qui présente CLAiRE comme un harnais agentique pour les industries régulées, le 13/08/2026
       ([Business Wire](https://markets.financialcontent.com/wral/article/bizwire-2026-8-13-compliance-group-launches-ai-agents-for-life-sciences-to-accelerate-quality-reviews-strengthen-audit-readiness-and-reduce-validation-time)).
   - En Europe :
     - Mistral lève 3 Md€ en 09/2026 ([TechCrunch](https://techcrunch.com/2026/09/08/mistral-raises-e3b-as-sovereign-ai-becomes-big-business/))
       et publie fin 10/2026 les poids de Large 4 ([Mistral](https://mistral.ai/news/mistral-large-4-oss/)) ;
     - Dust lève 40 M$ en 05/2026 ([Tech Funding News](https://techfundingnews.com/dust-40m-series-b-collaborai-ai-enterprise-workspaces-sequoia/)) ;
     - LightOn, éditeur souverain coté, fait 1,07 M€ de chiffre d'affaires au premier semestre 2026
       ([EQS](https://www.eqs-news.com/news/fr-regulatory/lighton-results-for-the-six-month-period-ended-30-june-2026-and-new-strategic-roadmap-to-accelerate-sales-and-change-scale/8492ea76-0aba-4896-a827-b3226396d83e_en)).
   - Temporal, le moteur d'exécution durable que cite le texte, lève 300 M$ en 02/2026 puis 550 M$ en 09/2026
     ([Temporal](https://temporal.io/news/temporal-raises-550m-at-a-12-55b-valuation)) ; Mistral Workflows repose sur lui.
10. `[ÉTABLI]` **La pharma, terrain de l'exemple du texte.**
    - **L'annexe 22 des BPF** (IA) reste un projet, comme l'annexe 11 révisée ; les textes finaux sont visés au T4 2026
      ([EMA](https://www.ema.europa.eu/en/documents/other/3-year-work-plan-inspectors-working-group_en.pdf)).
      - Dans la version mise en consultation (07/2025), l'IA générative et les LLM « should not be used in critical GMP
        applications » ([Commission](https://health.ec.europa.eu/document/download/5f38a92d-bb8e-4264-8898-ea076e926db6_en)).
      - L'atelier de l'EMA (rapport du 02/10/2026) discute de les admettre sous une stratégie de contrôle documentée.
        Parmi les cas présentés figurait un agent d'aide à la gestion des déviations
        ([EMA](https://www.ema.europa.eu/en/documents/report/report-multistakeholder-workshop-expert-contributions-artificial-intelligence-guidance-development-annex-22_en.pdf)).
    - **La FDA** a adressé le 02/04/2026 une lettre d'avertissement à une entreprise qui avait fait rédiger par des
      agents ses spécifications et ses dossiers de production, sans revue de l'unité qualité. Chaque sortie doit être
      revue et validée par une personne habilitée ; l'IA n'est pas interdite
      ([FDA](https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/warning-letters/purolea-cosmetics-lab-722591-04022026)).
    - **21 CFR Part 11** demande des audit trails sécurisés, horodatés et conservés aussi longtemps que les
      enregistrements, et des signatures électroniques liées à l'enregistrement
      ([eCFR](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-A/part-11)).
    - **Le guide GAMP de l'ISPE sur l'IA** (07/2025, 290 pages) encadre le cycle de vie des systèmes à IA en GxP
      ([ISPE](https://ispe.org/publications/guidance-documents/gamp-guide-artificial-intelligence)).
    - **L'AI Act** :
      - l'Omnibus (règlement 2026/1744) repousse le haut risque au 02/12/2027 (annexe III) et au 02/08/2028 (annexe I)
        ([Commission](https://ec.europa.eu/commission/presscorner/api/files/document/print/en/ip_26_1714/IP_26_1714_EN.pdf)) ;
      - la première norme harmonisée, EN 18286 (système qualité), paraît au JO le 14/10/2026
        ([EUR-Lex](https://eur-lex.europa.eu/eli/dec_impl/2026/2274/oj)) ;
      - l'annexe I ne cite pas la législation du médicament (lecture du secrétariat, à confirmer par un juriste).
11. `[ÉTABLI]` **Les contraintes du terrain** ([`CLAUDE.md`](../../CLAUDE.md) §3) : un seul espace d'historique réel
    (C1), un monde qu'on ne rejoue pas (C2), une horloge lente (C3), un budget proche de zéro sans GPU (C4).
12. **Le texte lui-même.**
    - `[ÉTABLI]` La Présidence l'a fait écrire par ChatGPT. Il cite l'OWASP, le règlement européen et le NIST. Ses
      images viennent de pages d'éditeurs, dont « Kivo for Quality ».
    - `[ÉTABLI]` Sa pile technique reprend celle de TaskForce élément par élément (Java et Spring Boot, Next.js,
      PostgreSQL et pgvector, stockage S3, Ollama, OIDC, Docker Compose), sauf Temporal et Kubernetes.
    - `[DÉDUIT]` Soit la conversation lui avait donné cette pile, soit c'est la pile par défaut de 2026 : la question est
      posée à la Présidence.

## La carte du secrétariat : TaskForce face au texte, élément par élément

Les faits du dossier, rangés selon la question de la Présidence. Cinq positions :
- **Pile** : TaskForce fait ou a décidé la même chose.
- **Devant** : TaskForce fait mieux ou plus concret que le texte.
- **En route** : la direction est prise, le chemin n'est pas fait.
- **Derrière** : le texte attend ce que TaskForce n'a pas.
- **Ailleurs** : TaskForce fait autre chose, par choix ou par fait.

| # | Ce que propose le texte | Où en est TaskForce | Position |
| - | --- | --- | --- |
| 1 | La thèse : pas de LLM, une couche de contrôle entre modèles, données, processus et systèmes | R60 et R5', tranchés les 27 et 29/10/2026 | **Pile** |
| 2 | Souveraineté des données | App desktop et auto-hébergement en production. La webapp passe par Groq, sur des machines qui s'arrêtent. L'export complet (R64) n'existe pas | **En route** |
| 3 | Souveraineté des modèles | Sur le desktop, le modèle se choisit (Ollama). La webapp a un seul fournisseur, sans secours. Les missions ne passent que par Claude Code ou Copilot | **En route** |
| 4 | Souveraineté du métier : règles et procédures versionnées par l'entreprise | Une table de 35 règles que le client ne peut pas modifier, aucune procédure, des notes sans version | **Derrière** |
| 5 | Souveraineté des agents : outils, actions, validations, arrêts | Règles par action, porte unique, accords, fermeture en panne, session bornée à son projet | **Devant**, sans éditeur |
| 6 | Souveraineté opérationnelle : auditer, reproduire, revenir, changer de fournisseur | Dossier chaîné exportable, Undo, adaptateurs d'agents. Le dossier n'est pas signé, disparaît avec l'issue et n'a pas de durée de conservation | **En route** |
| 7 | Couche 1 : un cockpit d'objectifs, de plans et de décisions en attente | Barre unique. Aucun objectif (R56 retenue, pas construite), aucun plan, pas de boîte des décisions. Le tableau de suivi est refusé (§15, R57) | **Ailleurs** par choix, **Derrière** sur les objectifs |
| 8 | Couche 2 : le moteur de contexte de l'entreprise | Graphe et RAG en production, sans écran. Aucun document lu ni versionné, aucune donnée opérationnelle, aucun processus, des droits de recherche à corriger | **Derrière** |
| 9 | Couche 3 : planifier, exécuter, vérifier, reprendre | Cortex (cinq tours) et missions en file. Ni planificateur, ni moteur durable, ni reprise, ni vérificateur indépendant (R4 et R15 retenues). Les tests du runner ne bloquent rien | **En route**, mince |
| 10 | Couche 4A : le moteur de politiques | Le contrat partagé Java et TypeScript, prouvé par la CI, fermé en panne, versionné. Aucune édition, ni seuil, ni double signature | **Devant** sur le moteur, **Derrière** sur la gouvernance des règles |
| 11 | Couche 4B : la passerelle de modèles | Une API compatible OpenAI et un frein de débit. Ni routage par tâche, ni registre, ni secours, ni budget | **Derrière** |
| 12 | Couche 5 : les intégrations (ERP, CRM, LIMS, GED, qualité) | GitHub en profondeur, MCP générique (25 préréglages, Linear essayé), Slack partiel, webhooks sortants. Aucun système d'entreprise | **Derrière**, par choix (R63 : le partenaire avant le connecteur) |
| 13 | Couche 6 : audit et évaluation, transversaux | Dossier de mission vérifiable sans TaskForce. Banque d'évaluations manuelle, réservée à Cortex. Ni OpenTelemetry en production, ni journal des actions d'IA | **Devant** sur la preuve de mission, **Derrière** sur l'observabilité et la conservation |
| 14 | Mécanismes A et B : le contexte et les règles, d'abord | En production, sans citations précises ni règles réglables | **Pile** sur l'ordre |
| 15 | Mécanismes C et D : l'affinage et la distillation, ensuite et sur preuve | Rien de construit ; E12 proposée ; R61 et R62 disent la même chose | **Pile** sur la décision |
| 16 | Le parcours d'arrivée en huit étapes | Aucun : c'est un travail de service, chez chaque client | **Ailleurs** |
| 17 | La grille de variables | Réversibilité et autonomie par les classes. La sensibilité est annoncée, pas faite. Aucun coût par tâche | **En route** |
| 18 | L'exemple : les déviations qualité en pharmacie | Niche B : l'embarqué, la défense, l'aérospatial. Premier cas d'usage : un standard de communication chez un éditeur de logiciels embarqués | **Ailleurs** |
| 19 | Les trois phases | Phase 1 en partie : règles, runtime, accords et preuve oui ; documents, provenance et citations précises non | **En route** (phase 1) |
| 20 | La pile technique | Identique, sauf Temporal (une file en base) et Kubernetes | **Pile** |
| 21 | L'opportunité : un système d'exploitation des opérations métier, en secteur régulé d'abord | R60 la vise. Le site vend la délégation aux agents de code ; rien n'est vendu | **En route** vers elle, **Ailleurs** dans les faits |

`[DÉDUIT]` **Lecture de la carte** :
- **Pile** sur la thèse, sur l'ordre des façons d'adapter l'IA et sur la pile technique, tranchées par la Présidence avant
  ce texte.
- **Devant** sur un morceau étroit : la porte de règles prouvée des deux côtés, le dossier chaîné vérifiable sans
  TaskForce, le local.
- **Derrière** sur presque tout le reste : le contexte documentaire, les processus, les objectifs, les systèmes
  d'entreprise, les règles réglables par le client, la passerelle, l'observabilité, la conservation, et tout le
  commerce.
- **Ailleurs** en pratique : un établi gratuit qui délègue des issues de code à Claude Code, avec neuf utilisateurs
  réels.

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre répond à trois questions : que vaut le texte, où en est TaskForce, que faire.
Les interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Gwynne Shotwell (Impulsion)

- **Le texte** : juste sur un point que les ingénieurs oublient, la conformité se construit dès le départ. Muet sur
  l'exploitation. Il ne dit jamais combien d'autorisations, de validations et de mois il faut avant qu'un laboratoire
  laisse un logiciel toucher un dossier qualité. Pas un mot de la qualification (IQ, OQ, PQ, les mots que la Présidence
  a elle-même donnés), ni de la validation d'un système informatisé. Il décrit une architecture, pas un produit qu'on
  peut lancer en pharmacie.
- **TaskForce** : devant sur la pièce qu'un inspecteur demandera en premier, la trace. Mais Part 11 demande plus :
  - une conservation aussi longue que l'enregistrement, alors que le dossier disparaît avec l'issue ;
  - des signatures liées, qui n'existent pas.

  Et aucune donnée d'essai : neuf utilisateurs, aucun dossier réel, aucune expérience menée.
- **À faire** : traiter le premier client comme un lancement. Dresser dès maintenant la liste des autorisations qu'il
  exigera (sa qualité, sa sécurité, ses achats) et préparer ce dossier avec le produit. Faire tourner le produit sur de
  vrais dossiers, même ratés : un échec mesuré vaut plus qu'une couche de plus.
- **Verdict** : en route sur la preuve, au point mort sur l'exploitation.

### 2. Tristan Harris (Harmonie)

- **Le texte** : suivre l'incitation de celui qui l'a écrit. Un assistant conversationnel est réglé pour être utile et
  agréable à qui l'interroge. Il rend à la Présidence son vocabulaire, sa pile et son ambition, en plus grand : la
  mécanique des fils d'actualité, appliquée à la stratégie. Le texte n'est pas faux ; il est sans friction. Rien n'y
  coûte, rien n'y est tranché contre son lecteur.
- **TaskForce** : du bon côté de la pente qu'il défend, un agent étroit et contrôlable dont chaque action laisse une
  trace. Le « système d'exploitation des opérations » du texte remonte la pente vers l'agent général. Deux incitations
  l'inquiètent :
  - les pages et les documents de TaskForce disent ce que le code ne fait pas (dossier, point 8), et une entreprise dont
    le produit est la preuve ne peut pas laisser sa propre documentation mentir ;
  - trois accords sur quatre portaient sur du réversible, et un harnais qui demande trop apprend à l'humain à cliquer
    sans lire.
- **À faire** : avant tout discours sur la souveraineté, corriger chaque phrase publique que le code ne tient pas, et
  nommer Groq là où il reçoit des données. La charge de la preuve est au constructeur.
- **Verdict** : bonne pente, mauvaise incitation. Le texte flatte, et les pages promettent plus que le code.

### 3. Jeff Bezos (Impulsion)

- **Le texte** : il part de la technologie et remonte vers le client, le contraire de ce qu'il faut. Six couches, cinq
  souverainetés, huit étapes, et pas un client nommé, pas un prix, pas une heure gagnée. C'est un plan d'architecture
  pour une entreprise qui aurait déjà mille clients : une réponse à une autre question.
- **TaskForce** : la seule question est de savoir qui l'utilise et pourquoi il revient. Neuf utilisateurs réels, un
  e-mail de lancement à huit personnes, aucun revenu, aucun partenaire. En six jours, trois écrans, une banque
  d'évaluations, des règles et un dossier, que personne d'extérieur n'a demandés.
  - Il maintient l'objection de la séance n°10 : la plupart des entreprises loueront leur intelligence comme elles
    louent leur calcul. La souveraineté est une option vendue à certains, pas une promesse faite à tous.
  - LightOn, souverain et coté, fait un million d'euros de chiffre d'affaires en un semestre.
- **À faire** :
  - Décider vite : ce sont des portes à double sens.
  - Garder la direction, mais arrêter de construire des surfaces jusqu'à ce que dix équipes extérieures aient délégué des
    missions et dit ce qui leur manque.
  - Écrire le communiqué du premier client avant la prochaine ligne de code (hors fiche).
- **Verdict** : ni devant ni derrière ; pas encore dans la course, faute de client.

### 4. Mariana Mazzucato (Pont)

- **Le texte** : le mot « souveraineté » y est vidé de sa direction. Souverain pour quoi faire, au service de quelle
  mission ? Il parle de contrôle, jamais de qui capte la valeur créée par les agents ni de ce que l'organisation apprend.
  Il remplace un seigneur (le laboratoire de modèles) par un autre (la plateforme de contrôle). C'est le féodalisme
  numérique, décalé d'une couche : les six couches décrites sont celles que les grandes plateformes vendent déjà
  (dossier, point 9), et l'on n'en sort pas plus facilement.
- **TaskForce** : mieux placée que le texte sur la direction, grâce à l'AGPL et à R64 (ce qui est possédé part avec le
  client). Mais R64 n'est pas construit : on copie aujourd'hui projets, issues et notes, pas les règles, les dossiers ni
  les évaluations. Et la webapp envoie les questions à un fournisseur gratuit, ce qui est la rente, en plus cher demain.
- **À faire** :
  - Faire de l'export complet la preuve de la souveraineté, avant tout mot sur le site.
  - Chercher une porte publique, la commande publique ou une infrastructure numérique européenne gouvernée en bien
    commun, où une preuve ouverte vaut plus qu'une fonction de plus.
- **Verdict** : en route, dans la bonne direction ; la souveraineté n'est pas encore un fait.

### 5. Don Norman (Design)

- **Le texte** : il traite l'humain comme un « validateur » au bout d'une chaîne. C'est la zone dangereuse qu'il décrit
  depuis longtemps :
  - une automatisation intermédiaire, assez forte pour agir, incapable de dire ce qu'elle va faire ;
  - qui rend la main sans contexte au pire moment.

  Le mot « cockpit » est révélateur : dans un cockpit, l'automatisation mal conçue est une grande source de méprises. Le
  texte n'en dit rien.
- **TaskForce** : devant le texte sur ce point, et c'est rare. Ce sont des décisions de conception, pas des fonctions :
  - le refus du tableau de suivi (§15, R57) ;
  - la demande dite en mots (R78, en dev) ;
  - « Undo » tant que rien n'a bougé ;
  - une carte de résultat qui sépare les contrôles des mots de l'agent.

  Deux défauts, sérieux :
  - « Apply » reste actif quand les tests ont échoué, ce qui invite au raté ;
  - une demande sans réponse devient un refus silencieux au bout de dix minutes, ce qui prive la personne du retour.
- **À faire** : ne pas adopter le cockpit du texte. Garder l'établi, et corriger ces deux défauts avant la release de
  R78 : un échec de tests doit se voir et se franchir explicitement, un refus par délai doit se dire.
- **Verdict** : devant sur la conception de la décision humaine, si « Apply » est corrigé avant la release.

### 6. Yann LeCun (Science)

- **Le texte** : juste sur ce qu'il défend lui-même, ne pas construire un LLM de plus et rester au-dessus des modèles
  ouverts. Faux quand il croit qu'un « planificateur » posé sur un LLM planifiera : sans modèle du monde, un LLM ne
  planifie pas de façon fiable. Le trio planificateur, exécutant, vérificateur est un schéma, pas un système. Ce qui le
  rendrait fiable, la vérification par contraintes et l'exécution à blanc, le texte ne le décrit pas.
- **TaskForce** : sur le bon chemin, et plus honnête que le texte. Elle ne prétend pas planifier : elle délègue une
  issue bornée, sur une copie, avec des règles vérifiables et des tests qui tournent. Deux limites :
  - le bac à sable n'en est pas un, puisque c'est une copie git sur la machine, sans isolation du système ni du réseau ;
  - « fini » est le code de sortie de l'agent, ce qui n'est pas une prévision de l'effet.
- **À faire** : avant un planificateur, l'aperçu des effets (le diff, les commandes, l'exécution à blanc), puis un vrai
  bac à sable. Garder le harnais ouvert : avec l'AGPL et des modèles ouverts comme Large 4 de Mistral, TaskForce est du
  bon côté de la plateforme.
- **Verdict** : pile sur la thèse, derrière sur l'isolation et l'aperçu des effets.

### 7. Margrethe Vestager (Harmonie)

- **Le texte** : il fait de la souveraineté un argument commercial, ce qu'elle combat : l'enfermement vendu comme une
  commodité. Il cite le règlement européen sans en dire l'état :
  - le haut risque est repoussé à 2027 et 2028 ;
  - la première norme harmonisée vient de paraître ;
  - le médicament n'est pas cité à l'annexe I.

  Vendre à un laboratoire la peur d'une échéance européenne serait faux : en pharmacie, le levier, ce sont les BPF et la
  FDA, pas l'AI Act.
- **TaskForce** : derrière sur la souveraineté qu'elle affiche. Une autorité lirait d'abord trois faits :
  - la politique de confidentialité ne nomme pas Groq ;
  - les pages légales décrivent un hébergement qui n'existe pas ;
  - la recherche ne respecte pas encore tous les droits des projets privés.

  En revanche, un dossier chaîné et vérifiable par d'autres est exactement une technologie de vérification, celle que
  l'Europe dit vouloir. C'est le meilleur argument de TaskForce, à condition qu'il soit vrai partout.
- **À faire** : mettre ses propres pages en conformité dans les dix jours (sous-traitants, hébergement, transferts hors
  de l'Union), puis rendre la portabilité réelle entre fournisseurs d'agents (R64). La règle adoptée doit être celle qui
  s'exécute, et la preuve doit le montrer.
- **Verdict** : devant sur la preuve vérifiable, derrière sur sa propre conformité ; réparer la maison avant de vendre la
  souveraineté.

### 8. Audrey Azoulay (Harmonie)

- **Le texte** : écrit pour une grande entreprise, avec des couches que seule une direction informatique comprend. La
  souveraineté y est celle de l'entreprise face au fournisseur. Ce n'est jamais celle d'une autorité qui doit contrôler,
  ni celle d'une petite structure sans équipe d'IA.
- **TaskForce** : sur le bon principe, avec deux atouts :
  - un dossier pensé pour être lu par un auditeur (§9.6) ;
  - le local à coût nul (R62), qui sert une PME ou un pays sans de grands moyens.

  Mais l'interface n'existe qu'en anglais, aucune autorité réelle n'a lu un dossier exporté, et les choix encodés dans
  les 35 règles ne se lisent que dans un fichier JSON.
- **À faire** : faire lire un dossier exporté par une personne d'une autorité ou d'un organisme de contrôle, et noter ce
  qu'elle n'a pas compris. Publier la table des règles en clair, en français et en anglais, comme une charte.
- **Verdict** : en route ; le principe est bon, sa lisibilité par une autorité reste à prouver.

### 9. Elon Musk (Impulsion)

- **Le texte** : quarante pour cent sont à supprimer. Six couches, cinq souverainetés, huit étapes, onze variables :
  c'est un organigramme, pas un produit. Chaque exigence doit avoir un nom derrière elle ; ici, aucune n'en a. Le texte
  automatise avant de simplifier.
- **TaskForce** : l'erreur inverse du texte, mais une erreur quand même, trop de surfaces pour un fondateur seul :
  - la gestion de projet ;
  - un Brain OS sans écran ;
  - vingt-cinq connecteurs, dont un seul essayé ;
  - une webapp et une app desktop ;
  - une banque d'évaluations, et la voix à venir.

  Onze des trente actions de la table de règles ne sont produites par aucun code : des règles pour des choses qui
  n'existent pas. Ce qui marche de bout en bout tient en une phrase : une issue de code déléguée à Claude Code, sous des
  règles, avec une preuve.
- **À faire** : supprimer avant d'ajouter (les règles qui ne bloquent jamais rien, les connecteurs jamais essayés, la
  webapp si l'app desktop porte la promesse). Puis itérer sur la seule boucle qui marche, avec dix utilisateurs et une
  version par jour. Ne pas bâtir un produit sur la peur d'un règlement (hors champ, et assumé).
- **Verdict** : ailleurs, et tant mieux ; ne pas devenir ce texte, supprimer jusqu'à ce qu'il reste une boucle qui
  gagne.

### 10. Yoshua Bengio (Science)

- **Le texte** : il nomme un « vérificateur », mais le place dans la même chaîne que l'agent : un vérificateur qui
  partage les objectifs de ce qu'il vérifie. Il ne dit rien de la sûreté d'un modèle affiné, alors qu'un affinage peut
  défaire ses garde-fous (dossier de la séance n°10). Et il propose une « exécution autonome sur des périmètres
  autorisés » sans dire qui estime le risque de chaque action.
- **TaskForce** : devant le texte sur la défense en profondeur :
  - des règles hors du modèle ;
  - la fermeture en cas de panne ;
  - un humain sur l'irréversible (R1).

  Mais le vérificateur indépendant que le Conseil a retenu (R4, R15) n'existe pas. « Fini » veut dire que l'agent a rendu
  la main, et des tests en échec ne bloquent ni la pull request ni « Apply ». La banque d'évaluations ne contient aucune
  évaluation de sûreté.
- **À faire** : un juge non agentique, même simple, entre l'agent et l'exécution, par exemple un relecteur d'un autre
  fournisseur sur la pull request, qui chiffre le risque avant l'accord humain. Et une famille « sûreté » dans la banque
  avant tout modèle affiné (E12).
- **Verdict** : devant sur l'architecture de contrôle, derrière sur la vérification indépendante déjà décidée.

### 11. Karri Saarinen (Design, conflit d'intérêts : Linear)

- **Le texte** : l'opposé d'un parti pris. Tout pour tout le monde, six couches, une plateforme qui « cartographie
  l'entreprise ». Les produits qui gagnent sont conçus pour quelqu'un en particulier ; ce texte n'a personne dedans. Son
  cockpit est un tableau de bord de plus, avec le chat comme interface par défaut.
- **TaskForce** : ailleurs, et au bon endroit si elle l'assume. Elle a trouvé une grammaire de la délégation :
  - l'humain reste assigné et l'agent est délégué ;
  - l'activité de l'agent est visible ;
  - ses actions sont tracées et réversibles ;
  - la carte de résultat dit qui tranche.

  C'est un établi pour une équipe logicielle qui délègue à des agents. Mais il se dilue : un outil de gestion de projet
  complet face à Linear (il le dit avec son conflit d'intérêts), un Brain OS sans écran, une voix à venir.
- **À faire** : choisir une personne, l'ingénieur qui délègue une issue à un agent et doit en répondre. Tout le reste
  sert ce geste ou disparaît. Pas de cockpit.
- **Verdict** : ailleurs. TaskForce fait un établi de délégation, pas une plateforme d'entreprise ; qu'elle le fasse
  excellent.

### 12. Steve Jobs (Impulsion, siège historique)

- **Le texte** : un texte d'ingénieur, qui part de la technologie. Personne ne se réveille le matin en voulant « une
  plateforme de souveraineté opérationnelle de l'IA » ; on achète des heures en moins sur un dossier, un résultat qu'on
  peut montrer. La question finale (infrastructure ou plateforme métier ?) révèle que le texte ne sait pas pour qui il
  est écrit.
- **TaskForce** : la direction est juste depuis la séance n°10, à la condition qu'il avait posée : que
  l'infrastructure ne devienne pas le produit. Or :
  - le site vend la délégation aux agents de code ;
  - la direction vend la possession de l'intelligence ;
  - ce texte vend la souveraineté.

  Trois produits en trois phrases. Les trois écrans de R78 sont ce qui a été fait de mieux cette semaine, parce qu'ils
  partent du geste de la personne.
- **À faire** : dire non à ce texte comme feuille de route. Garder une seule promesse, R5' (dossier, point 3). Finir les
  écrans de base avant toute couche ; rien sur le site qui ne marche pas (R12).
- **Verdict** : à côté. Ce texte ferait perdre le seul produit que TaskForce a commencé à bien faire.

### 13. Nandan Nilekani (Harmonie)

- **Le texte** : le plus juste sur l'architecture. La conformité doit être dans l'architecture, pas dans un manuel ; les
  connecteurs doivent préserver les droits et la vérité des systèmes sources. Mais il pense en entreprise unique : une
  plateforme, un client, un graphe. L'échelle vient des réseaux ouverts, où chacun branche son agent sous des règles
  communes.
- **TaskForce** : en route, avec une pièce rare : un contrat de règles neutre, le même en Java et en TypeScript, prouvé
  par des cas partagés. C'est le début d'un protocole, pas seulement d'un produit, et MCP dans les deux sens (un serveur
  par espace, un client pour les outils) va dans ce sens. Mais un contrat que personne d'autre n'implémente n'est pas un
  protocole, et une règle que le client ne peut pas écrire n'est pas son architecture.
- **À faire** : publier le contrat de règles et le format du dossier comme une spécification ouverte, avec leurs cas,
  pour qu'un autre harnais ou un outil qualité puisse les vérifier. Le terrain des formats ouverts se prend maintenant :
  Microsoft a publié sa spécification de contrôle des agents en 06/2026 (fiche de Satya Nadella). Il entend R9' (pas de
  standard avant les clients) : il ne parle pas de standard, mais de publication.
- **Verdict** : en route, avec une pièce d'infrastructure publique possible, le contrat de règles, s'il s'ouvre.

### 14. Yuval Noah Harari (Harmonie)

- **Le texte** : « l'IA comprend le fonctionnement de l'organisation », « l'entreprise pilotée par des agents » : ces mots
  déplacent la confiance des personnes vers le système, sans dire qui répond quand il se trompe. Le texte parle de
  « responsables » mais jamais d'une personne qui signe. La responsabilité y est une colonne de tableau.
- **TaskForce** : devant le texte. Chaque action est attribuée (la personne, Claude Code, Copilot), seule la personne qui
  a délégué tranche, et aucun agent ne décide seul de l'irréversible (R1). Deux failles :
  - Copilot travaille sans les règles ni le dossier de TaskForce, et rien ne le dit à la personne ;
  - au bout de dix minutes, le délai décide à sa place sans qu'elle le sache.
- **À faire** : écrire sur chaque mission le nom de la personne qui en répond. Ne jamais montrer un agent comme soumis
  aux règles s'il ne l'est pas. Faire de la contestation d'un résultat un geste visible, comme « Undo ».
- **Verdict** : devant sur l'attribution, à condition de ne jamais laisser croire à un contrôle qui n'existe pas.

### 15. Margaret Hamilton (Science, siège historique)

- **Le texte** : il confond la description d'un système et la garantie qu'il marche. « Reprise sur erreur », « retour
  arrière », « conditions d'arrêt » restent des promesses tant qu'on n'a pas dit, avant la mission, ce que le système
  lâche d'abord quand il sature, et qui l'a décidé.
- **TaskForce** : en route, sur des fondations saines (la fermeture en cas de panne, des transitions d'état gardées, un
  contrat écrit entre le serveur et le runner). Mais des trous qu'elle n'accepterait pas en vol :
  - une mission perdue n'est déclarée que quand quelqu'un ouvre l'issue ;
  - le résultat du runner n'est pas renvoyé s'il échoue ;
  - les événements du runner vivent en mémoire et se perdent, alors que le contrat dit « sur disque d'abord » ;
  - le dossier disparaît avec l'issue ;
  - un changement de modèle n'a aucune porte : ni registre, ni raison écrite (R61).
- **À faire** : avant toute couche nouvelle, la file durable avec baux et une tâche du serveur qui reprend les missions
  perdues (§13.2), les événements sur disque, le dossier conservé hors de l'issue. Puis le registre des modèles : aucun
  changement sans raison, accord et évaluations rejouées.
- **Verdict** : en route, mais pas encore digne d'un système dont dépend une décision qualité.

### 16. Fei-Fei Li (Science)

- **Le texte** : il parle d'évaluation partout et ne mesure rien. Ses indicateurs (« taux d'exécution sans
  correction », « couverture des preuves ») sont bons, mais sans un chiffre, sans une méthode, sans tiers. En secteur
  régulé, une évaluation faite par le vendeur sur ses propres cas ne vaut pas grand-chose.
- **TaskForce** : en route, honnêtement. La banque d'évaluations existe : des cas figés, un rejeu à blanc, une notation
  par du code, ce qui est rigoureux. Mais elle est manuelle, limitée à Cortex, sans cas de sûreté ni tiers. Rien ne
  mesure ce que l'agent ne sait pas faire avant qu'on lui confie une mission.
- **À faire** : un registre des incidents et des échecs, nourri par les dossiers ; R61 l'a décidé, une tâche échouée
  devient un cas. Puis une évaluation par un tiers sur le premier cas d'usage, même modeste.
- **Verdict** : en route sur la mesure, pas encore vérifiable par un tiers.

### 17. Daniela Rus (Science)

- **Le texte** : il a raison de séparer l'endroit où tourne le modèle de ce qu'il a le droit de faire. Il a tort de
  traiter l'inférence locale comme un détail de la pile (« vLLM ou Ollama ») : pour un système critique, l'embarqué est
  un choix d'architecture, parce qu'une décision ne doit pas dépendre du réseau.
- **TaskForce** : devant le texte sur un point concret. L'app desktop fait tourner sur la machine la base, le backend, le
  runner et le modèle. Elle ne transmet que la connexion du compte, les mises à jour, et ce que la personne choisit.
  C'est l'architecture des systèmes critiques. Deux limites :
  - l'app dépend d'un serveur de comptes sur des machines qui s'arrêtent ;
  - les missions déléguées ne peuvent pas utiliser un modèle local (R51), si bien que posséder son modèle ne vaut que
    pour Cortex.
- **À faire** : que l'app desktop fonctionne sans réseau une fois installée, et qu'une mission puisse tourner sur un
  petit modèle local mesuré (E11). Mesurer la latence et la consommation sur un poste ordinaire.
- **Verdict** : devant sur le local, à condition qu'il tienne sans réseau et qu'il serve aussi les missions.

### 18. Atul Gawande (Science)

- **Le texte** : l'exemple de la déviation est le seul passage concret, et il est bien construit : le modèle propose,
  l'humain arbitre, rien d'irréversible n'est laissé à la machine. Mais il saute ce qui décide de tout : combien de
  temps un responsable qualité passe aujourd'hui sur une déviation, et combien demain. Sans mesure avant et après, c'est
  une intention.
- **TaskForce** : en route sur les points de pause. Accorder, relire et appliquer ressemblent à une checklist en trois
  moments. La lettre de la FDA du 02/04/2026 montre que ce point de pause est la bonne réponse. Encore faut-il le
  prouver sur un vrai dossier : aucune mesure avant et après n'a été faite (E13), et le premier cas d'usage ne peut pas
  tourner, faute d'import de documents.
- **À faire** : un vrai dossier, une vraie personne, un chronomètre. L'écart entre deux versions d'un standard est assez
  proche d'une revue qualité pour servir de preuve, si l'import de documents existe.
- **Verdict** : en route sur la conception des pauses ; rien n'est encore mesuré.

### 19. Esther Duflo (Science)

- **Le texte** : une théorie du changement sans un seul test. Il affirme que la plateforme réduira le travail
  documentaire ; c'est peut-être vrai, mais rien ne le montre. La plupart des interventions bien conçues ne marchent pas
  comme prévu. Sa « boucle d'amélioration » n'a pas de groupe témoin.
- **TaskForce** : exactement là où la séance n°10 l'avait laissée. Neuf expériences déclarées, aucune menée, et
  quatre-vingts recommandations en six jours sans l'épreuve d'un utilisateur extérieur. La seule observation réelle
  (trois accords sur quatre sur du réversible) met en cause un réglage de R1 et n'a pas été suivie.
- **À faire** : geler les surfaces nouvelles et mener trois expériences avant la fin de novembre :
  - E14 : cinq entretiens sur la promesse ;
  - E13 : un dossier réel, chronométré ;
  - E7 : la part des accords sur du réversible, dans des missions réelles.

  Écrire les critères avant, publier les échecs.
- **Verdict** : on ne sait pas où est TaskForce, puisque rien n'a été mesuré. C'est le premier problème, avant le
  texte.

### 20. Jennifer Doudna (Science)

- **Le texte** : il propose des paliers d'autonomie (lecture, préparation, exécution limitée), ce qu'elle défend. Mais il
  ne dit pas quelle preuve fait passer d'un palier au suivant, ni qui peut signaler un usage dangereux. Et il réserve
  tout cela aux grandes entreprises qui peuvent payer une intégration en huit étapes.
- **TaskForce** : devant sur la gouvernance graduée, dans le code. L'irréversible est fermé par défaut, le réversible
  passe, l'inconnu est traité comme irréversible : la structure qu'elle aurait voulue ailleurs. Et l'accès est ouvert,
  gratuit, sous AGPL, en local. Mais aucun palier ne s'ouvre sur preuve : rien ne mesure qu'un agent a mérité plus
  d'autonomie. Et il n'y a pas de canal de signalement.
- **À faire** : écrire la règle de passage d'un palier à l'autre (combien de missions sans incident, sur quelles
  actions). Ouvrir un canal simple pour signaler un incident d'agent, même à qui n'est pas client.
- **Verdict** : devant sur la structure graduée, en route sur la preuve qui fait changer de palier.

### 21. Arati Prabhakar (Pont)

- **Le texte** : il cite le NIST comme une caution, sans en tirer la seule chose utile, un protocole d'essai. Un
  garde-fou n'existe que si l'on montre qu'il arrête l'erreur qu'il prétend arrêter. Et il réduit l'ambition à
  « réduire de 30 % le délai des dossiers fournisseurs » : de l'automatisation de bureau, pas un objectif qui change
  quelque chose.
- **TaskForce** : en route, avec un atout : les cas de règles partagés sont déjà un protocole d'essai, rejoué par la CI à
  chaque changement. Mais ce protocole protège le moteur, pas l'effet. Rien ne montre qu'un agent réel a été arrêté au
  bon moment, ni combien d'erreurs passent.
- **À faire** : un essai contradictoire publié. Une série de missions conçues pour tenter des actions interdites, d'après
  le Top 10 de l'OWASP pour les applications agentiques (12/2025), et le taux d'arrêt mesuré. C'est ce qu'un régulateur
  recevrait comme preuve.
- **Verdict** : en route, avec la bonne culture de l'essai ; l'essai qui compte, celui de l'effet, reste à faire.

### 22. Julie Zhuo (Design, conflit d'intérêts : Meta, par Sundial)

- **Le texte** : il ne répond à aucune des trois questions qu'on pose à un produit : quel problème de quelles personnes,
  comment savoir qu'il est réel, comment savoir qu'il est résolu. C'est une solution qui cherche son problème, écrite
  pour plaire à qui a déjà la solution en tête. Sa question finale prouve qu'il n'a personne en face de lui.
- **TaskForce** : ailleurs, sur un problème réel connu de l'intérieur, déléguer du code à un agent sans perdre la main.
  Son échelle d'autonomie (lire, préparer, agir sous accord) ressemble à celle qu'elle propose (conseiller, adjoint,
  régent). Mais TaskForce ne sait pas si le problème est assez douloureux pour qu'on change d'outil : neuf
  utilisateurs, aucun entretien écrit, aucune critique de la première minute.
- **À faire** : faire découvrir l'app desktop, sans aide, à cinq ingénieurs qui délèguent déjà à Claude Code, et noter
  leur première minute puis leur première semaine. Écrire le pronostic à un an avant de lire les résultats.
- **Verdict** : ailleurs, sur un vrai problème dont on ne sait pas encore s'il fait assez mal.

### 23. Satya Nadella (Pont, contradicteur)

Contradicteur, il attaque le consensus qui s'est formé : le texte flatte, TaskForce est « devant » sur la porte et la
preuve, il suffit de se concentrer et de mesurer.

- **Le texte** : le Conseil le traite trop vite de flatteur. Il a raison sur un point que le Conseil balaie : la valeur
  est dans la combinaison du contexte de l'entreprise, de l'exécution et des politiques (couches 2, 3 et 4). C'est là
  que les plateformes horizontales sont faibles pour une petite organisation régulée, pas sur la porte.
- **TaskForce** : le « devant » du Conseil est un mot dangereux. Les règles hors du modèle, la porte unique et la preuve
  chaînée, c'est sa propre doctrine, et c'est devenu en 2026 un produit standard : Agent 365, AgentCore Policy et son
  harnais géré, Google, OpenAI, ServiceNow, IBM (dossier, point 9).
  - Microsoft a publié en 06/2026 sa spécification de contrôle des agents.
  - En pharmacie, un éditeur se présente déjà comme « harnais agentique », et Veeva, MasterControl et Kivo ont des agents
    relus par l'humain dans des systèmes déjà validés.
  - L'avance de TaskForce sur la porte se compte en mois, et sans distribution.
- **À faire** : ne pas se battre sur le plan de contrôle horizontal ; s'y brancher. Il remet en cause la phrase de la
  séance n°2 (« Microsoft se branche sur nous, pas l'inverse »). Le défendable de TaskForce serait ailleurs :
  - la preuve lisible par un auditeur, pour une petite organisation régulée qui n'achètera jamais Agent 365 ;
  - en local, en open source ;
  - interopérable avec les plans de contrôle des grands (MCP, formats ouverts).

  Il parle aussi en fournisseur de plateformes (limite de sa fiche).
- **Verdict** : ni devant ni derrière, sur un terrain que les plateformes viennent d'occuper. La différence doit être
  ailleurs que dans la porte.

### 24. Kenza Ait Si Abbou (Pont)

- **Le texte** : écrit par un ingénieur pour un ingénieur. Une responsable qualité dans une PME industrielle ne
  reconnaîtra rien de son travail dans « Enterprise Context Engine », « Policy Engine » ou « Model Gateway ». La promesse
  que l'IA « comprend le fonctionnement de l'organisation » fait peur ou fait rêver ; elle ne fait pas adopter.
- **TaskForce** : en route sur les mots. La séance n°10 a mis les mots avant la page (R65), et les écrans de R78 parlent
  en gestes simples (créer, accorder, relire). Mais :
  - E14 n'a pas eu lieu : personne de la cible n'a redit la promesse en une phrase ;
  - les données ont un problème de qualité, puisque les notes n'ont ni responsable, ni version, ni date de validité.

  Posséder son intelligence, c'est d'abord posséder la qualité de ses données ; TaskForce ne le peut pas encore.
- **À faire** : mener E14 cette semaine, avec deux publics, un ingénieur logiciel (niche A) et une personne de la qualité
  dans l'industrie (niche B). Si la seconde ne comprend pas, la niche B attend. Donner à chaque note un responsable et
  une date de validité avant de parler de contexte d'entreprise.
- **Verdict** : en route sur la clarté des gestes ; les mots pour la cible régulée n'ont jamais été essayés.

### Le tour en une table

| # | Membre | Le texte | Où en est TaskForce |
| - | --- | --- | --- |
| 1 | Shotwell | Muet sur l'exploitation | En route sur la preuve, au point mort sur l'exploitation |
| 2 | Harris | Flatteur par construction | Bonne pente ; les pages promettent plus que le code |
| 3 | Bezos | Répond à une autre question | Pas encore dans la course : aucun client |
| 4 | Mazzucato | Un seigneur pour un autre | En route ; la souveraineté n'est pas un fait |
| 5 | Norman | L'humain réduit à un validateur | Devant sur la décision humaine, si « Apply » est corrigé |
| 6 | LeCun | Juste sur les modèles ouverts, faux sur le planificateur | Pile sur la thèse, derrière sur l'isolation |
| 7 | Vestager | La souveraineté en argument commercial | Devant sur la preuve, derrière sur sa propre conformité |
| 8 | Azoulay | Pour les grandes entreprises | En route ; lisibilité par une autorité à prouver |
| 9 | Musk | Un organigramme | Ailleurs, et tant mieux |
| 10 | Bengio | Un vérificateur qui n'est pas indépendant | Devant sur le contrôle, derrière sur la vérification |
| 11 | Saarinen | Aucun parti pris | Ailleurs : un établi de délégation |
| 12 | Jobs | Part de la technologie | À côté ; ne pas en faire la feuille de route |
| 13 | Nilekani | Juste, mais pensé pour une seule entreprise | En route ; ouvrir le contrat de règles |
| 14 | Harari | La responsabilité en colonne de tableau | Devant sur l'attribution |
| 15 | Hamilton | Des promesses de fiabilité | En route, pas encore digne d'une décision qualité |
| 16 | Li | Ne mesure rien | En route sur la mesure, sans tiers |
| 17 | Rus | Le local traité en détail | Devant sur le local |
| 18 | Gawande | Un bon exemple, sans mesure | En route ; rien n'est mesuré |
| 19 | Duflo | Une théorie sans test | On ne sait pas : rien n'est mesuré |
| 20 | Doudna | Des paliers sans preuve de passage | Devant sur la structure graduée |
| 21 | Prabhakar | Le NIST en caution | En route ; l'essai de l'effet reste à faire |
| 22 | Zhuo | Une solution qui cherche son problème | Ailleurs, sur un vrai problème |
| 23 | Nadella, contradicteur | Juste sur la valeur du contexte | Sur un terrain que les plateformes occupent |
| 24 | Ait Si Abbou | Écrit pour des ingénieurs | En route sur les gestes, pas sur les mots |

## Confrontation `[HYPOTHÈSE]`

### Devant, ailleurs, ou sur un terrain occupé ?

- **Le camp « devant »** : Norman, Vestager, Bengio, Harari, Rus et Doudna. La porte, la preuve vérifiable par d'autres,
  le local et les paliers sont concrets, et rares dans un outil de cette taille.
- **Nadella, contradicteur** : la porte est devenue un produit standard en 2026. L'avance se compte en mois.
- **Norman lui répond** : les plateformes vendent un registre et des politiques à un service informatique ; TaskForce
  conçoit la décision de la personne qui délègue. La différence n'est pas d'avoir une porte, c'est la façon dont un
  humain y décide.
- **Saarinen**, avec son conflit d'intérêts : une grammaire d'interface se copie en un trimestre. Linear a publié les
  règles d'interaction de ses agents.
- **Jobs** : une différence n'est jamais une fonction ; c'est le produit entier, pour une personne.
- **Bezos et Duflo** : la question est prématurée. Sans client ni mesure, « devant » ne veut rien dire.
- **Où l'on arrive** : le Conseil s'accorde sur les faits, une pièce réelle, rare à cette taille mais pas unique. Il ne
  s'accorde pas sur leur valeur. Le désaccord est conservé, et seul l'usage le tranchera (R83, R84) :
  - une avance, pour Norman, Vestager et Bengio ;
  - un produit courant, pour Nadella et Saarinen.

### Six couches, ou un seul geste ?

- **Le camp du geste** : Musk, Jobs, Saarinen, Zhuo et Bezos. Un geste, une personne : l'ingénieur qui délègue et répond
  du résultat. Le reste se supprime.
- **Le camp des couches** : Nadella, Nilekani et Prabhakar. Sans le contexte de l'entreprise (couche 2) et sans règles
  que le client règle lui-même (couche 4A), le geste reste un outil de développeur. Le texte a raison sur la
  combinaison.
- **Hamilton et Bengio** : ni l'un ni l'autre d'abord, la fiabilité. Un geste qui ment une fois perd le client.
- **Où l'on arrive** : le geste d'abord, c'est-à-dire la boucle de délégation. Il ne se complète que de deux choses :
  - dans la couche 2, ce qu'exige le premier cas d'usage (l'import des documents, leurs versions, leurs citations) ;
  - dans la couche 4A, des règles que le client règle.

  Aucune autre couche. Musk maintient qu'il faut d'abord supprimer : la webapp, les connecteurs jamais essayés.

### La pharmacie, maintenant ?

- **Pas maintenant** : Shotwell, Gawande, Hamilton et Vestager. Leurs raisons :
  - l'annexe 22 est en projet, et sa version de consultation exclut les LLM des usages critiques ;
  - les textes finaux sont attendus fin 2026 ;
  - la FDA sanctionne déjà les agents sans revue de l'unité qualité ;
  - un système à IA en GxP se valide selon le guide GAMP ;
  - les éditeurs en place ont déjà leurs agents, dans des systèmes validés ;
  - un fondateur seul, sans certification, n'y entre pas.
- **Ne pas abandonner la cible régulée** : Ait Si Abbou, Doudna et Mazzucato. Les petites structures n'ont pas les moyens
  des grands éditeurs ; le local et l'ouvert sont un argument d'accès.
- **Nadella** : la porte s'entrouvre, puisque l'EMA a examiné un agent de gestion des déviations. Qui aura un format de
  preuve accepté quand elle s'ouvrira gagnera, mais avec un partenaire en place (Kivo ouvre un accès MCP), pas seul.
- **Où l'on arrive** : la pharmacie n'est pas le premier terrain.
  - La niche B reste celle de la séance n°2 : l'embarqué, la défense, l'aérospatial. Ce sont des industries régulées où
    le logiciel est le produit, proches de la niche A.
  - La pharmacie se surveille (annexe 22, guides de la FDA) et ne s'approche que par un partenaire.
  - Désaccord conservé : Ait Si Abbou et Doudna.

### La souveraineté : une promesse ou un fait ?

- **Un fait à construire avant de le dire** : Vestager, Mazzucato, Harris et Harari. Groq, les pages légales, la
  recherche et l'export disent qu'elle n'est pas encore un fait.
- **Une option, pas un titre** : Bezos et Musk. La plupart des clients loueront. LightOn montre que la souveraineté seule
  se vend mal.
- **Le local, seule souveraineté réelle aujourd'hui** : Rus, LeCun et Doudna. L'app desktop doit tenir sans réseau.
- **Où l'on arrive** : pas de « souveraineté » en titre, la vérité d'abord, le local comme preuve. Bezos maintient qu'il
  faut construire aussi pour le client qui loue.

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R81 (R80 est la dernière existante). Chacune porte qui la soutient, qui s'y oppose, sa preuve en
dix jours et son signal d'arrêt.

### R81. Ce texte ne devient pas la feuille de route

- La direction reste R60, et la promesse R5'.
- Du texte, on ne retient que trois manques, déjà prévus :
  - les documents versionnés et cités (spécification §5) ;
  - les règles réglables par le client (§6.6) ;
  - les objectifs (R56).
- Aucune autre couche. Le texte sert de liste des questions qu'un acheteur régulé posera, pas de plan.
- **Pour** : Jobs, Saarinen, Musk, Zhuo, Bezos, Duflo, Norman, Ait Si Abbou, Harris, Gawande.
- **Contre** :
  - Nadella, contradicteur : la valeur est dans la combinaison des couches 2, 3 et 4, qu'il ne faut pas réduire à trois
    manques.
  - Nilekani : la combinaison passe par un contrat ouvert (R89).
- **Preuve en dix jours** : la feuille de route du 10/11/2026 ne contient aucune tâche qui ne serve ni le premier cas
  d'usage ni la boucle de délégation.
- **Signal d'arrêt** : une surface livrée sans qu'un utilisateur l'ait demandée.

### R82. Dire vrai avant de dire plus

- Dans les dix jours, corriger chaque phrase publique ou de conception que le code ne tient pas (dossier, point 8) :
  - la politique de confidentialité, qui doit nommer Groq ;
  - les pages légales, sur l'hébergement ;
  - l'architecture, qui dit qu'aucun contenu ne sort ;
  - la règle de recherche, qui annonce des droits ;
  - la spécification, sur la survie du dossier ;
  - le modèle de prix, l'ADR-010 et l'ADR-021.
- Corriger la recherche qui ne respecte pas encore tous les droits des projets privés (tâche proposée).
- **Pour** : Harris, Vestager, Mazzucato, Harari, Azoulay, Ait Si Abbou, Hamilton, Bengio, Li, Jobs.
- **Contre** : aucun. Réserve de Musk : supprimer une page fausse plutôt que la réécrire.
- **Preuve en dix jours** : chaque écart du dossier fermé, chacun avec son commit.
- **Signal d'arrêt** : une affirmation publique que le code ne tient pas.

### R83. Mesurer avant de construire

- Trois expériences avant le 30/11/2026, critères écrits avant, échecs publiés :
  - E14 : cinq entretiens, deux publics ;
  - E13 : un dossier réel, chronométré, sur le premier cas d'usage ;
  - E7 : la part des accords sur du réversible, dans des missions réelles.
- Aucune surface nouvelle tant qu'E14 n'est pas faite.
- **Pour** : Duflo, Bezos, Zhuo, Gawande, Li, Ait Si Abbou, Shotwell, Prabhakar.
- **Contre** : Musk, en réserve : itérer avec dix utilisateurs vaut mieux qu'un protocole.
- **Preuve en dix jours** : E14 faite, ses résultats écrits.
- **Signal d'arrêt** : au 30/11, aucun résultat. Le Conseil cesse alors de recommander des fonctions.

### R84. Un geste, une personne

- La personne : l'ingénieur qui délègue une issue à un agent et en répond. C'est la niche A, rendue concrète.
- Le produit se concentre sur la boucle « Créer, Accorder, Relire » (R78) jusqu'à ce que dix équipes extérieures s'en
  servent. Leur usage tranche entre la webapp et l'app desktop.
- La niche B ne passe que par le premier cas d'usage. Il exige l'import des documents (§5), seul travail permis dans la
  couche 2.
- **Pour** : Saarinen, Jobs, Zhuo, Musk, Bezos, LeCun.
- **Contre** :
  - Nadella, contradicteur : GitHub et Linear intégreront cet établi.
  - Ait Si Abbou : ne pas perdre la cible qui n'écrit pas de code.
  - Mazzucato : la mission se perd.
- **Preuve en dix jours** : dix équipes extérieures invitées, et le nombre de celles qui délèguent une deuxième mission.
- **Signal d'arrêt** : au bout de trente jours, moins de trois équipes extérieures ont délégué une deuxième mission.

### R85. La pharmacie n'est pas le premier terrain

- La niche B reste celle de la séance n°2.
- La pharmacie se surveille, avec une veille datée au Journal :
  - le texte final de l'annexe 22 ;
  - les guides de la FDA sur l'IA en fabrication.
- On ne l'approche que par un partenaire, jamais seul.
- **Pour** : Shotwell, Gawande, Hamilton, Vestager, Nadella, Duflo, Jobs.
- **Contre** : Ait Si Abbou, Doudna et Mazzucato. Les petites structures régulées ont le plus besoin d'une preuve
  abordable.
- **Preuve en dix jours** : une conversation avec une personne de la qualité pharmaceutique, dans le cadre d'E14, pour
  mettre à l'épreuve l'hypothèse « pas maintenant ».
- **Signal d'arrêt** (qui ferait revenir sur R85) : un partenaire de la pharmacie demande le dossier tel qu'il est.

### R86. Les règles appartiennent au client

- Un éditeur de règles par espace, avec propriétaire, raison et date de revue. La table V102 existe déjà, elle n'est
  jamais écrite.
- Le moteur applique la classe de la règle.
- Les onze actions sans code sont retirées ou marquées.
- Les actions inverses s'exécutent, ou disparaissent du contrat.
- **Pour** : Vestager, Nilekani, Musk (pour l'élagage), Hamilton, Mazzucato, Doudna.
- **Contre** :
  - Jobs, en réserve : un éditeur de règles est une surface d'ingénieur, et la personne ne doit voir que des gestes
    (R22).
  - Norman, en réserve : pas un fichier JSON à l'écran.
- **Preuve en dix jours** : un espace change une règle par l'interface, la mission suivante en tient compte, et le
  dossier le montre.
- **Signal d'arrêt** : aucune règle modifiée par un utilisateur dans les trente jours.

### R87. Une preuve digne d'un auditeur, et « Apply » qui respecte les tests

- **Avant la release de R78** : un échec de tests désactive « Apply ». La personne ne peut passer outre que par un geste
  explicite, avec une raison écrite au dossier.
- **Ensuite** :
  - le dossier survit à l'issue et a une durée de conservation ;
  - il est horodaté et signé ;
  - les dossiers de Cortex s'exportent ;
  - les sauvegardes quittent la machine et sont chiffrées ;
  - les missions sont observées en production.
- **Pour** : Hamilton, Shotwell, Vestager, Bengio, Li, Gawande, Norman, Azoulay, Prabhakar.
- **Contre** : Musk et Bezos, en réserve : seulement ce qu'un premier client exige.
- **Preuve en dix jours** :
  - la release de R78 avec « Apply » bloqué sur un échec de tests ;
  - un dossier exporté, lu par une personne extérieure qui dit ce qui lui manque.
- **Signal d'arrêt** : un dossier qu'un auditeur ne sait pas lire.

### R88. La fiabilité avant une couche de plus

- La file durable avec baux, et la reprise des missions perdues par le serveur (§13.2).
- Les événements du runner sur disque, et son résultat renvoyé s'il échoue.
- Un secours pour le modèle de la webapp, ou le local, et le registre des modèles (R61).
- La webapp et le serveur de comptes hors des machines de l'école (Q13).
- **Pour** : Hamilton, Rus, Bengio, Shotwell, Nadella.
- **Contre** :
  - Musk : supprimer la webapp plutôt que la fiabiliser.
  - Bezos : fiabiliser d'abord ce que les clients utilisent.
- **Preuve en dix jours** :
  - une mission dont on coupe le runner en plein travail est reprise ou arrêtée proprement, et le dossier le dit ;
  - la webapp tourne sur le VPS.
- **Signal d'arrêt** : une mission perdue découverte par un utilisateur.

### R89. Publier le contrat, et l'essai de l'effet

- Le contrat de règles, le format du dossier et leurs cas partagés, publiés comme une spécification ouverte.
- Un essai contradictoire, publié : des missions qui tentent des actions interdites, d'après le Top 10 agentique de
  l'OWASP, avec le taux d'arrêt mesuré.
- **Pour** : Nilekani, Prabhakar, LeCun, Doudna, Vestager, Azoulay.
- **Contre** :
  - R9' (séance n°2, pas de standard avant les clients), défendue par Bezos et Jobs en réserve.
  - Nadella : les grands publient déjà les leurs ; publier ne crée pas d'adoption.
- **Preuve en dix jours** : le rapport d'essai publié, avec son taux d'arrêt.
- **Signal d'arrêt** : personne ne lit ni ne reprend la spécification en soixante jours.

## Décision de la Présidence

Le 01/11/2026, dans ses mots : « Sur ce que je viens de dire je suis d'accord avec l'ensemble du conseil sur tout les
points » ; « Je suis d'accord avec tout les membres du conseil ». Ses orientations du même message modifient plusieurs
recommandations. Le secrétariat en a proposé la lecture ci-dessous à la séance n°15 ; la Présidence l'a confirmée
(« Daccord partout apres »).

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R81 | Retenue, modifiée : le texte n'est pas la feuille de route, mais ses 21 lignes deviennent la barre à dépasser ; « aucune autre couche » tombe | « sur le tableau faut qu'on soit devant absolument partout, on vise l excellence, le client focus » |
| R82 | Retenue | Accord avec tout le Conseil |
| R83 | Retenue, modifiée : la mesure ne bloque plus la construction, elle juge chaque jalon (R104, R105) | « c'est pas le temps ici le KPI principale, c'est la confiance » ; « me faut une demo pour aller chercher le client » |
| R84 | Remplacée par R103 et R105 | « c est une produit grade entreprise, on peut pas ce permettre de faire une petite demo qui fonctionne avec un use case des plus simple » |
| R85 | Retenue, élargie : aucun secteur d'abord (R103) | « te fixe pas sur la pharma, nous on creer l'infra, pas les regles en elles mm » |
| R86 | Retenue, élargie (R94, R98) | « c'est a eux de construire l'outil » |
| R87 | Retenue ; « Apply » corrigé avant la release de R78 | Accord avec tout le Conseil |
| R88 | Retenue, sans secours pour Groq ni VPS pour l'instant | « pas de serveur, pas d'API Claude ou autre [...] a moins de payer » (séance n°15) |
| R89 | Retenue (R98, R100) | Accord avec tout le Conseil |

Les quatre questions du secrétariat : la première reste sans réponse ; la deuxième est sans objet (on ne teste plus sur
la webapp) ; la troisième est tranchée par R87 ; la quatrième est remplacée par les personnes extérieures de chaque
jalon (R105).

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 31/10/2026 à 20:19 UTC (`shuf`). Contradicteur désigné : Satya Nadella.
- **Formation** : plénière. Les interventions sont plus longues que l'usage de la charte (§5), à la demande de la
  Présidence.
- **Le dossier** :
  - Faits sur TaskForce : cinq relevés du secrétariat le 31/10/2026 (code et notes de conception), avec leurs chemins.
  - Faits de marché et de réglementation : pages lues ce jour par la recherche du secrétariat, liens joints. Certains
    viennent de sources secondaires (presse spécialisée, communiqués). À revérifier un par un avant toute citation hors
    du labo.
- **Hors fiche, hors champ** :
  - Bezos : « le communiqué du premier client d'abord » est la méthode d'Amazon, pas une position de sa fiche.
  - Musk : il parle hors champ de la réglementation pharmaceutique, et l'assume.
- **Le contradicteur** : Nadella attaque une doctrine qu'il partage (séparer l'intelligence de l'autorité), et remet en
  cause une phrase de la séance n°2. Il parle aussi en fournisseur de plateformes, limite inscrite à sa fiche. Nilekani
  cite un fait de cette fiche.
- **Conflits d'intérêts** : Saarinen (Linear), Zhuo (Meta, par Sundial), Nadella (Microsoft).
- **La faille de la recherche** est décrite sans détail, les dépôts étant publics. Une tâche de correction est proposée.
  Ce PV ne se commite qu'après la correction.
- **Les chiffres d'usage** sont ceux du 08/09/2026. Ceux du jour demandent l'accès à la production.
- **Correction (01/11/2026)** : la spécification ne dit pas faux sur la conservation. Son §9.4 décrit la cible, puis
  ajoute « Pas encore » : le dossier part avec son run. Le point 8 du dossier l'a lu trop vite.
- **D'autres écarts entre documents et code**, relevés par le dossier :
  - l'ADR-005 décrit un index ivfflat de 1 536 dimensions, le code un index HNSW de 1 024 ;
  - l'ADR-017 dit l'ingestion de GitHub, Slack et Plane automatique, elle est manuelle ;
  - le catalogue des connecteurs annonce 47 outils, le code en a 28 ;
  - la note Backend liste encore les quotas par offre, retirés par l'ADR-016 ;
  - les notes Backend et Frontend marquent « fait » du travail encore en dev ;
  - le tableau des expériences s'arrête à E11 ;
  - la note `.ai/brain-os-roadmap.md` a été supprimée le 19/10/2026, mais le protocole du labo la cite encore comme
    source (§3, §8).
- **Questions à la Présidence** :
  1. La conversation avec ChatGPT lui avait-elle donné la pile et le vocabulaire de TaskForce ?
  2. Les chiffres d'usage du jour : valider l'accès à la production, ou les donner.
  3. La release de R78 : attendre la correction d'« Apply » (R87) ?
  4. Les dix équipes extérieures de R84 : lesquelles, et par quel canal ?

## Suites

Rangées le 01/11/2026 avec celles de la [séance n°15](./2026-11-01-feuille-de-route.md), qui les reprend :

- le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal ;
- les dates d'E7, E13 et E14 dans `experiences/Experiences.md` ;
- une question ouverte : la porte de la pharmacie (veille de l'annexe 22 et de la FDA) ;
- les tâches de R82, R86, R87 et R88 à la roadmap, et les corrections de documents du dossier (point 8) ;
- un brouillon d'ADR si R81 ou R85 sont retenues, parce qu'elles engagent le positionnement.

## Avis du secrétariat

Après la clôture, l'avis du secrétariat. C'est le mien, pas celui du Conseil.

- `[DÉDUIT]` **Le texte n'est pas mauvais ; il est générique.** C'est l'architecture que vendent les grandes plateformes
  en 2026, décrite avec la pile et les mots de TaskForce. Il plaît parce qu'il ressemble à son lecteur. Il est utile
  comme liste des questions qu'un acheteur régulé posera ; pas comme feuille de route.
- `[ÉTABLI]` **Le fait le plus important de la séance n'est pas dans le texte** : neuf utilisateurs réels, aucune
  expérience menée, quatre-vingts recommandations en six jours. Le labo produit plus vite que le marché ne valide.
- `[DÉDUIT]` **En une phrase** : TaskForce va vers ce texte, elle est devant sur une pièce, derrière sur presque tout le
  reste, et elle fait aujourd'hui autre chose. Le texte décrit l'entreprise que TaskForce pourrait devenir dans trois
  ans, si la pièce qu'elle a déjà trouve des utilisateurs.
- **Mon ordre** :
  1. R82 cette semaine, avec la correction de la recherche ;
  2. le blocage d'« Apply » sur un échec de tests, avant la release de R78 ;
  3. E14 tout de suite ;
  4. puis R84.
- `[ÉTABLI]` **Une erreur à moi** : « Apply » actif malgré un échec de tests vient de la carte de résultat que j'ai
  construite le 30/10/2026. Je ne l'avais pas relevé.
