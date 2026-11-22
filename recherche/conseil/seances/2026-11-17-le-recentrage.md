---
id: conseil-seance-2026-11-17-le-recentrage
title: "Séance n°28 du 17/11/2026 : le recentrage"
doc_type: pv-seance
statut: active
date: "17/11/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, recentrage, preuve, dossier, conformite, confiance, souverainete, integrations, board, workflow, cortex, inventaire]
related:
  - "../README.md"
  - "./2026-11-17-preciser-avant-de-trancher.md"
  - "./2026-11-17-finir-la-v1.md"
  - "./2026-11-15-le-run-et-les-petits-modeles.md"
  - "./2026-11-13-le-marche-a-prendre.md"
  - "./2026-11-13-le-workflow-pilotable.md"
  - "./2026-11-13-le-workflow-pilotable-plan-des-lots.md"
  - "./2026-11-13-depasser-camunda.md"
  - "./2026-11-11-se-brancher-a-l-entreprise.md"
  - "../../decisions/ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "../../decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
  - "../../decisions/ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../../decisions/ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md"
  - "../../decisions/ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md"
  - "../../experiences/Experiences.md"
  - "../../Questions-ouvertes.md"
---

# Séance n°28 du 17/11/2026 : le recentrage

> Simulation : les membres sont des personnages simulés, à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **En bref.**
>
> **Ce que TaskForce est, et pour qui** : la couche qui fait travailler les agents d'une entreprise sous ses règles et qui en
> garde la preuve, vérifiable sans TaskForce, posée sur les outils qu'elle a déjà et installée chez elle ; pour les équipes de
> 10 à 250 personnes qui livrent du logiciel avec des agents et doivent en répondre devant un audit.
>
> **Ce qu'on arrête** : vouloir remplacer Linear, Jira ou Asana ; Smart Assign ; le calque « Show all links » ; l'agent Copilot,
> qui n'ouvre aucun dossier ; les mots « souverain » et « conforme ». **Ce qu'on gèle** : le Board et sa famille (List,
> Backlog, Cycles, Roadmap, Teams, Dashboard, Analytics, Members, le suivi du temps), la vue Workflow en cartes, les 97
> préréglages de connexion que personne n'a encore connectés. Geler n'est pas supprimer : l'issue reste, parce que tout le dossier y est
> accroché.
>
> **Les dix prochains jours** : les six correctifs de confiance de la recette, « dire vrai » d'abord ; puis le dossier fini
> (TF-J2-7 : signé, avec la demande et le modèle, qui survit à la suppression) ; la table qui confronte TaskForce, ligne par
> ligne, aux principes de l'ANSSI, du NIST et de la CNIL, absences comprises ; la recette suivante jouée sur le projet
> TaskForce lui-même, avec ses réponses écrites avant. Rien d'autre.
>
> **Pourquoi là.** Le dossier établit que les besoins qui paient aujourd'hui viennent des audits déjà en place (BPF, Part 11,
> SOC 2, questionnaires fournisseurs), pas de l'AI Act, dont le haut risque est reporté au 02/12/2027. Les agences (ANSSI, NIST,
> Five Eyes, CNIL) demandent toutes la même chose : un contrôle déterministe hors du modèle, un accord humain sur l'action
> exacte, un journal hors de portée de l'agent. Les plateformes vendent l'identité, la passerelle et la télémétrie, en ligne,
> aux grands comptes ; aucune, dans les pages lues, ne vend un dossier par tâche, signé et vérifiable hors de l'outil. C'est
> la place. Elle est déduite, pas mesurée : aucune enquête ne chiffre la demande sur site chez les 10 à 250 personnes, et
> aucun exemple public ne montre une personne seule vendant cela à des entreprises régulées.
>
> **Où en est TaskForce sur cette place** : à moitié. Le dossier est chaîné par SHA-256 et se vérifie hors ligne, mais il
> n'est pas signé, la demande n'y entre pas, la version du modèle non plus, et supprimer une issue l'efface. Une mission ne
> part que d'une issue de TaskForce : aujourd'hui, le Board ne « sert à rien » comme tableau, mais l'issue porte tout.
>
> Neuf recommandations, R196 à R204, toutes à 90 % au moins, quatre au second tour. Margrethe Vestager, contradictrice, a
> obtenu qu'une couche ne dépende jamais d'une seule source de travail, que le dossier se lise sans TaskForce et sans l'outil
> d'où vient le travail, et que la place reste étiquetée hypothèse tant qu'aucun acheteur n'a parlé.

- **Saisine** (Présidence, 17/11/2026, en conversation, mot pour mot) :
  - « oui on passe d'abord par le conseil. Genre qu'est ce que les entreprises ont besoin ajd niveau conpliamce, en term de
    confiance agentique, en terme de souverainete, ... qu'est ce qu'on peut leur apporter, y a t'il une place a ce faire sur le
    marche global des entreprises qu'il manquerais ajd, ... un produit complet ? Un outil ? Jsp moi, y a des trucs qui sortent
    tout les jours et qui fonctionne quoi, mm si y a des concurrent c'est pas ca le pb »
  - Elle répond au secrétariat, qui proposait, après sa recette de la 1.17.0, une séance sur le recentrage et, en parallèle, un
    lot de correctifs. Elle a choisi : le Conseil d'abord.
  - Le cœur de son bilan de recette (étape s19, mot pour mot) : « j'ai l'impression qu'on essaie de faire trop de trucs, au
    lieu de fairevraiment extremement bien ce que nous on souhaite faire, et aller s'integrer aux autres et tout. » ; « Mais du
    coup le board sert a rien techniquement. Nous ce qui nous interresse c'est les preuves, les workflows reglementer, dans les
    regles de l'art, permettre d'etre sur et confiant de ce que fais un agents, et des reponses d'un LLM. donc jsp j'avoue que
    je m'y perd un peu la »
  - **Les questions à trancher** :
    1. ce dont les entreprises ont besoin aujourd'hui, en conformité, en confiance dans les agents et en souveraineté, classé
       par urgence et par qui paie ;
    2. ce que TaskForce peut leur apporter qui manque, confronté à son état réel, et si cette place existe et pourquoi elle
       serait encore libre ;
    3. la forme : un produit complet, un outil ou une couche ; s'intégrer ou remplacer, et le sort du Board ; le sort de la vue
       Workflow ; la place de Cortex et ce que « proactif » veut dire sous des règles ;
    4. ce qu'on arrête, ce qu'on gèle, ce qu'on finit, surface par surface ;
    5. ce que cela change : J2, E20, le premier client test, la niche (R181), les objectifs (R183), le pitch, la prochaine
       recette ;
    6. les correctifs de la recette : confirmer, compléter ou réordonner.
  - **Horizon** : J2 (W0 à W5, puis W6 et son test à blanc, et W10), E20, le premier client test ; puis l'après-J2. Aucune date
    ne court avant le client test (décision de la Présidence sur la séance n°26).
- **Formation** : séance n°28, plénière (24). La question touche le positionnement, le produit, la technique, le droit et la
  stratégie : c'est un choix structurant (charte, §5).
  - Impulsion : Steve Jobs, Elon Musk, Jeff Bezos, Gwynne Shotwell.
  - Pont : Satya Nadella, Mariana Mazzucato, Arati Prabhakar, Kenza Ait Si Abbou.
  - Harmonie : Margrethe Vestager, Audrey Azoulay, Nandan Nilekani, Tristan Harris, Yuval Noah Harari.
  - Science : Yoshua Bengio, Yann LeCun, Fei-Fei Li, Margaret Hamilton, Daniela Rus, Jennifer Doudna, Esther Duflo, Atul Gawande.
  - Design : Don Norman, Julie Zhuo, Karri Saarinen.
  - **Contradictrice** : Margrethe Vestager. Elle n'a jamais tenu ce rôle. Son angle (qui contrôle l'accès, les données et les
    choix par défaut ; la portabilité ; la règle exécutée est-elle la règle adoptée) vise droit le consensus attendu, « se
    brancher » : elle doit l'attaquer même si elle le partage. LeCun l'était à la n°27.
  - **Ordre de parole**, tiré au sort le 17/11/2026 à 12:14 UTC (`shuf`) : Jennifer Doudna, Mariana Mazzucato, Margrethe
    Vestager, Margaret Hamilton, Daniela Rus, Gwynne Shotwell, Jeff Bezos, Karri Saarinen, Yoshua Bengio, Yuval Noah Harari,
    Audrey Azoulay, Atul Gawande, Julie Zhuo, Satya Nadella, Arati Prabhakar, Tristan Harris, Elon Musk, Yann LeCun, Esther
    Duflo, Fei-Fei Li, Don Norman, Kenza Ait Si Abbou, Steve Jobs, Nandan Nilekani.
  - **Règle de vote** (charte §6.5) : 90 % des présents, soit 22 oui sur 24 au moins.
- **Fiches** : aucune fiche rafraîchie. Toutes ont moins de 30 jours au 17/11/2026 : la plus ancienne date du 21/10/2026, soit
  27 jours ; Norman, Zhuo et Saarinen datent du 28/10, Ait Si Abbou du 26/10, les vingt autres du 21/10. Jobs et Hamilton,
  sièges historiques, ne se rafraîchissent que sur une nouvelle source historique ; aucune n'est apparue. À partir du
  21/11/2026, vingt fiches passeront les 30 jours : la prochaine séance devra les rafraîchir. Les conflits d'intérêts que le
  sujet réveille (Saarinen, Nadella, Bezos) sont aux notes du secrétariat.

## Dossier

Constitué le 17/11/2026 par le secrétariat. Sur TaskForce : le code de `dev` au commit `067c577b` (après la fusion de la PR
#547), copié en lecture seule et lu ce jour ; la recette de la 1.17.0, faite par la Présidence les 16 et 17/11/2026 ;
`taskforce-docs` (`feature/lean-oss`, `34af22b`). Sur le reste : trois recherches du 17/11/2026 (D1, la conformité ; D2, la
confiance dans les agents ; D3, la souveraineté et la place), faites sur des pages publiques seulement, sans connexion ni
formulaire. Leurs étiquettes sont gardées telles quelles : un `[À VÉRIFIER]` reste un `[À VÉRIFIER]`. Leurs limites, et ce que
le secrétariat a relu lui-même, sont aux notes. La saisine couvrant six questions, le dossier compte dix points et trois
pièces du secrétariat.

1. **Ce que les règles et les audits demandent, par urgence** (D1).
   - `[ÉTABLI]` Le haut risque de l'AI Act est reporté, pas supprimé : le règlement (UE) 2026/1744, en vigueur le 27/07/2026,
     le place au 02/12/2027 (annexe III) et au 02/08/2028 (annexe I). L'article 50 (transparence) s'applique depuis le
     02/08/2026 ([Law & Technology, 24/07/2026](https://lawandtechnology.eu/en/digital-omnibus-on-ai-official-journal-regulation-2026-1744/) ;
     [Cloud Security Alliance, 2026](https://labs.cloudsecurityalliance.org/research/csa-research-note-eu-ai-act-high-risk-deadline-omnibus-20260/)).
     Ces dates reposent sur des sources secondaires concordantes : EUR-Lex n'a pas pu être relu.
   - `[ÉTABLI]` Une seule norme harmonisée existe, EN 18286:2026 (système qualité) ; les autres, dont la journalisation et le
     contrôle humain, sont en cours, la demande de normalisation courant jusqu'au 28/02/2027
     ([CEN-CENELEC JTC 21, 14/10/2026](https://jtc21.eu/en-18286-becomes-the-first-harmonised-standard-under-the-eu-ai-act/)).
   - `[ÉTABLI]` En pharmacie, l'Annexe 11 de 2011 s'applique encore ; l'Annexe 22 et l'Annexe 11 révisée ne sont pas publiées
     ([EudraLex, volume 4](https://health.ec.europa.eu/medicinal-products/eudralex/eudralex-volume-4_en)). La guidance CSA de
     la FDA est finale (02/2026) ; aucune modification de 21 CFR Part 11 n'a été trouvée : audit trails horodatés et
     signatures liées à l'enregistrement restent la règle.
   - `[ÉTABLI]` Le Cyber Resilience Act a commencé : déclarations des vulnérabilités exploitées depuis le 11/09/2026,
     application entière le 11/12/2027
     ([ENISA, 11/09/2026](https://www.enisa.europa.eu/news/the-cra-single-reporting-platform-is-launched)). `[À VÉRIFIER]`
     Selon un seul commentaire d'avocat, un logiciel libre n'est « mis sur le marché » que s'il est monétisé, et une même
     entité peut être intendante d'une édition communautaire et fabricante d'une édition payante.
   - `[ÉTABLI]` DORA s'applique depuis le 17/01/2025. NIS2 n'est pas transposée en France : le vote solennel de l'Assemblée
     était fixé à ce 17/11/2026, et son résultat n'a pas été lu.
   - `[ÉTABLI]` SOC 2 : au 30/08/2026, l'AICPA n'a publié aucun critère propre à l'IA. Les auditeurs demandent au cas par cas
     la version du modèle, l'invite ou son empreinte, les appels d'outils, le résultat, et un changement approuvé, testé et
     réversible ; ils butent sur l'attribution quand l'agent agit sans demande humaine
     ([Cloud Security Alliance, 30/08/2026](https://labs.cloudsecurityalliance.org/research/csa-research-note-soc2-ai-controls-gap-20260830-csa-styled/)).
   - `[ÉTABLI]` La CNIL et le Conseil de l'IA et du numérique (note exploratoire du 20/07/2026, lue par un commentaire) proposent
     de tracer tout le déroulé, de classer les actions par risque avec accord humain, un environnement isolé et un arrêt
     d'urgence ; la note ne crée pas de règle
     ([Inside Privacy, 13/08/2026](https://www.insideprivacy.com/artificial-intelligence/french-cnil-publishes-note-on-agentic-ai-and-data-protection/)).
   - `[HYPOTHÈSE]` (D1) Le report du haut risque enlève l'argument de l'échéance : la demande qui paie aujourd'hui vient des
     audits déjà en place, pas de l'AI Act. Et les preuves attendues convergent d'un régime à l'autre : journal de chaque
     action, accord humain daté et motivé, version du modèle et des règles, changement maîtrisé, évaluation rejouable. Aucun
     texte n'en fixe le format.
2. **La maturité déclarée** (D1, D2 ; des enquêtes déclaratives, donc des estimations, presque toutes américaines).
   - `[ÉTABLI]` Kiteworks, éditeur intéressé (459 professionnels, 29/07/2026) : la moitié ne peut pas produire en un jour ouvré
     le relevé complet des accès d'une IA ; 33 % ont des journaux infalsifiables ; 21 % un arrêt d'urgence formel
     ([Kiteworks](https://www.kiteworks.com/cybersecurity-risk-management/ai-governance-gap-widens-2026/)).
   - `[ÉTABLI]` Grant Thornton (près de 1 000 dirigeants américains, 13/04/2026) : 78 % ne sont pas pleinement sûrs de réussir
     un audit indépendant de gouvernance de l'IA sous 90 jours
     ([Grant Thornton](https://www.grantthornton.com/insights/press-releases/2026/april/grant-thornton-survey-on-ai-proof-gap)).
   - `[ÉTABLI]` IBM (3 221 dirigeants, huit pays d'EMEA dont la France, 14/10/2026) : 35 % ont de l'IA agentique en
     production ; 37 % une gouvernance conçue pour l'échelle ; aucun consensus sur qui répond d'un dommage causé par un agent
     (le rôle le plus cité l'est à 17 %) ; 13 % appliquent une assurance indépendante à l'IA de leurs fournisseurs
     ([IBM](https://newsroom.ibm.com/2026-10-14-ibm-study-eight-in-ten-emea-enterprises-escalate-ai-incidents-to-board-or-c-suite-as-ai-agents-test-governance)).
   - `[ÉTABLI]` IDC (08/09/2026, relu par le secrétariat) : « the record of what happened often doesn't exist at all » ; 60 %
     des responsables de la sécurité n'ont pas de contrôle de confinement des agents, 35 % ne peuvent pas arrêter un agent
     déployé ([IDC](https://www.idc.com/resource-center/blog/the-audit-trail-that-doesnt-exist/)). Méthode non publiée.
   - `[ÉTABLI]` Aucune enquête indépendante trouvée sur les entreprises européennes de 10 à 250 personnes : ce manque est celui
     de la recherche, pas un fait sur ces entreprises.
3. **Ce que les agences exigent d'un système d'agents** (D2).
   - `[ÉTABLI]` ANSSI, « Sécuriser un système IA agentique », Les Essentiels, v1.0, 10/2026 : sept principes. Classer chaque
     action (autonome, approbation obligatoire, interdite) ; un mécanisme d'approbation « hors de portée du système
     agentique » ; présenter l'action exacte et n'exécuter que celle-là ; un filtrage déterministe indépendant de l'agent,
     « par défaut, refuser l'action » ; un arrêt d'urgence ; des journaux hors de portée de l'agent pour reconstituer
     « demande, autorisation, action, résultat » ; un environnement d'exécution isolé et durci
     ([ANSSI](https://messervices.cyber.gouv.fr/documents-guides/anssi_essentiels_ia_agentique_1.0.pdf)).
   - `[ÉTABLI]` NIST, dix principes de conception proposés pour l'identité des agents (27/10/2026), dont la séparation de la
     politique et du raisonnement, des décisions d'accès déterministes et une preuve immuable : une proposition, pas une
     norme ([NIST](https://www.nist.gov/blogs/cybersecurity-insights/design-tenets-agent-identity-management-systems)).
   - `[ÉTABLI]` Five Eyes, « Careful Adoption of Agentic AI Services » (01/05/2026) : approbation humaine des actions
     irréversibles décidée par les concepteurs et non par l'agent, journal de chaque action, retour arrière
     ([CISA](https://www.cisa.gov/resources-tools/resources/careful-adoption-agentic-ai-services)).
   - `[ÉTABLI]` Les incidents publics ont une cause commune : un jeton trop large, aucune approbation devant l'action
     destructrice (Replit, 07/2025 ; Kiro, 12/2025, contesté par Amazon ; PocketOS, 04/2026, où une règle écrite dans le
     prompt n'a rien empêché). Une prépublication non relue par des pairs montre que presque tous les harnais locaux testés
     laissent l'agent effacer ses traces ([arXiv 2609.30266, 24/09/2026](https://arxiv.org/abs/2609.30266)).
4. **Qui vend quoi** (D2, D3).
   - `[ÉTABLI]` Les plateformes vendent le plan de contrôle en ligne, aux grands comptes : Microsoft Agent 365 (15 $ par
     utilisateur et par mois, en ligne seulement) ; AWS AgentCore, dont Policy, en disponibilité générale depuis le
     03/03/2026, convertit des règles en langue naturelle en politiques Cedar appliquées hors du code de l'agent
     ([AWS](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available)). La
     déduction de la séance n°24, « aucun voisin ne revendique des règles écrites en mots au-dessus d'un socle
     déterministe », est donc à nuancer.
   - `[ÉTABLI]` Microsoft donne un moteur de règles sous licence MIT depuis le 02/04/2026 : il juge chaque action avant son
     exécution, en YAML, Rego ou Cedar. Relu par le secrétariat : l'annonce ne dit rien de journaux signés ou chaînés, et ne
     nomme que des cibles Azure
     ([Microsoft](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit/)).
   - `[ÉTABLI]` (presse, montants rapportés) L'argent va à l'identité, à la sécurité et à l'observabilité des agents : Dynatrace
     achète Arize 915 M$ ; CrowdStrike achète Fiddler AI et Dreadnode pour environ 495 M$ au total
     ([TechCrunch, 03/11/2026](https://techcrunch.com/2026/11/03/crowdstrike-to-shell-out-nearly-500m-for-2-ai-security-startups-as-the-market-for-securing-agents-takes-off/)).
   - `[ÉTABLI]` Les journaux d'audit de Cursor (offre Enterprise) n'enregistrent ni prompts, ni sorties de l'agent, ni code
     généré ([documentation de Cursor](https://cursor.com/docs/enterprise/compliance-and-monitoring)). `[À VÉRIFIER]` Les faits
     sur Google, Salesforce, ServiceNow, Codex, Devin et GitHub Universe 2026 restent à vérifier.
   - `[HYPOTHÈSE]` (D2) Tous offrent du contrôle, des journaux d'administration et de la télémétrie. Aucun, dans les pages lues,
     n'offre un dossier de preuve par tâche, signé, vérifiable hors de l'outil, qui lie la demande, la règle, l'accord humain
     et le résultat.
5. **Le format de la preuve est ouvert** (D3).
   - `[ÉTABLI]` Un brouillon individuel à l'IETF, « Agent Audit Trail » (version 09, 26/10/2026, relu par le secrétariat),
     décrit un journal d'agent chaîné par SHA-256 sur JSON canonique (RFC 8785), signatures en option. Il n'est « not endorsed
     by the IETF » ([IETF](https://datatracker.ietf.org/doc/search?name=agent-audit-trail)).
   - `[ÉTABLI]` Forrester (20/03/2026) : les standards sont en retard sur les bonnes pratiques d'architecture ; aucun standard
     mûr d'identité d'agent portable
     ([Forrester](https://www.forrester.com/blogs/agent-control-planes-still-need-a-robust-standards-stack/)).
6. **La souveraineté demandée** (D3).
   - `[À VÉRIFIER]` Capgemini Research Institute (1 300 dirigeants, 08/09/2026, lu dans une reprise de presse) : 59 % jugent la
     souveraineté complète irréaliste ; un peu moins de la moitié paierait un surcoût, de 23 % en moyenne.
   - `[ÉTABLI]` Aucun label européen ne la définit : l'EUCS n'est pas adopté ; le Cloud and AI Development Act (03/06/2026) est
     une proposition ([Commission européenne](https://digital-strategy.ec.europa.eu/en/library/proposal-cloud-and-ai-development-act-cada)).
   - `[ÉTABLI]` Le local devient ordinaire : 42 % des 200 entreprises interrogées ont des modèles à poids ouverts en
     production, dont 42 % sur site ; premier frein en pilote, la sécurité et la conformité, à 62 % (Enterprise Technology
     Research, 22/09/2026, repris par [Constellation Research](https://www.constellationr.com/research/blog/evidence-shows-enterprises-use-open-weight-models-mainstream)).
     Échantillon petit.
   - `[À VÉRIFIER]` Selon la presse professionnelle pharmaceutique (08/2026), un modèle hébergé qui change sans prévenir rend
     la maîtrise des changements invérifiable.
   - `[ÉTABLI]` La politique publique de Google interdit tout logiciel AGPL chez lui
     ([Google](https://opensource.google/docs/using/agpl-policy/)). `[À VÉRIFIER]` Beaucoup de directions juridiques auraient
     une règle semblable.
7. **La forme et la taille** (D3).
   - `[ÉTABLI]` Ceux qui gagnent en conformité se branchent : Vanta annonce plus de 300 M$ de revenu récurrent et plus de 400
     intégrations ([Vanta, 29/04/2026](https://vanta.com/resources/vanta-crosses-300m-in-arr-as-growth-accelerates)) ; Ketryx
     se pose sur Jira et GitHub ; la place de marché d'Atlassian a dépassé 7 Md$ de ventes cumulées (26/10/2026).
   - `[ÉTABLI]` Le libre auto-hébergé se finance par une édition payante, et il se referme : Plane réserve à ses offres payantes
     le SSO, les workflows avec accords et les journaux d'audit ; Mattermost a resserré son gratuit (23/08/2025) ; Cal.com a
     fermé son code le 15/04/2026.
   - `[ÉTABLI]` La gouvernance de l'IA au sens strict est un petit marché : 492 M$ en 2026 selon Gartner (17/02/2026, lu dans
     des reprises), contre 29,2 Md$ de dépenses d'agents (dossier de la séance n°26). Les périmètres diffèrent : ces chiffres
     ne s'additionnent pas.
   - `[HYPOTHÈSE]` (D3) Aucune enquête ne mesure la demande d'une gouvernance d'agents sur site. Aucun exemple public solide
     d'une personne seule vendant cela à des entreprises régulées : le seul cas documenté d'une personne seule (Sidekiq,
     entretien de 2023) vend un composant technique en libre-service.
8. `[ÉTABLI]` **Ce qui existe pour la preuve, dans le code** (pièce 2 pour le détail).
   - Le dossier d'une mission est une chaîne : l'empreinte d'un événement est le SHA-256 de l'empreinte précédente, d'un saut
     de ligne, puis du JSON canonique de l'événement ; le serveur la calcule à la réception
     (`core/harness/evidence/EvidenceChain.java`). Il s'exporte en JSON (`taskforce-evidence/1`) et en Markdown, et se vérifie
     sans TaskForce ni réseau : `npm run verify -- evidence-run-N.json` (`taskforce-runner/src/verify-cli.ts`).
   - Il n'est pas signé : aucune signature, aucune clé dans le code. TF-J2-7 (« il survit à la suppression, il est signé et
     vérifié sans TaskForce ») est au statut ⬜ dans la roadmap.
   - Les règles : un moteur déterministe, sans modèle ni réseau ; un socle que les couches de l'entreprise ne font que durcir
     (`RulesEngine.java`, `RulesFloor.java`) ; 30 règles par défaut ; sans règle applicable, l'effet est une demande ; le
     runner refuse sur erreur ou sur délai. Une règle écrite en mots est traduite par le modèle, puis vérifiée par du code sur
     des cas ; au moment d'agir, aucun modèle ne juge.
   - Les accords : la règle et sa raison, qui demande, qui peut accorder, plusieurs signatures si une règle l'exige, dix
     minutes par défaut, puis un refus écrit au dossier.
   - La banque d'évaluations et le banc des modèles mesurent Cortex. Rien n'y couvre les missions de Claude Code.
9. `[ÉTABLI]` **Ce qui existe pour s'intégrer, et ce qui tient à l'issue.**
   - Le catalogue compte 107 entrées : 104 préréglages MCP (`connectors/presets.json`) et 3 intégrations natives (GitHub,
     Slack, Plane). Un seul préréglage est marqué essayé de bout en bout : Linear. À la recette, la Présidence en a essayé 63 :
     7 connectés (Linear, Notion, Slack, PostHog, Stripe, Canva, Excalidraw), 7 en échec sans raison, 1 en erreur chez
     l'éditeur, 8 qui demandent une clé ou un réglage, 40 arrêtés au portail de l'éditeur faute de compte.
   - Par un connecteur, Cortex lit tout de suite ; une écriture demande toujours un accord, et le socle la classe
     irréversible. Les missions de Claude Code n'ont aucun connecteur externe : le runner ne leur donne que le serveur MCP de
     TaskForce.
   - Aucune synchronisation d'issues avec Linear, Jira, GitHub ou Asana : des outils à la demande, et un import ponctuel de
     100 issues au plus, sans retour vers l'outil d'origine.
   - Une mission ne part que d'une issue de TaskForce : `delivery_runs.issue_id` est `NOT NULL`, avec suppression en cascade
     (`V86__delivery_runs.sql:7`). Le dossier, les accords, la checklist, les liens « Blocked by », les nœuds de la vue
     Workflow et les cycles pendent tous à l'issue.
   - Le serveur MCP de TaskForce expose 17 outils (9 de lecture, 8 d'écriture) sur les issues, les projets, les missions et le
     Brain OS. Aucun n'expose le dossier, les règles ni la décision d'un accord. Le plugin Claude Code compte une commande et
     aucun hook : dans une session ouverte par le plugin, les actions locales de l'agent ne sont ni jugées ni gardées.
10. `[ÉTABLI]` **La recette de la 1.17.0, et ses causes** (code de `dev`, `067c577b`).
    - Les connexions « can't tell why » : quand l'éditeur refuse l'inscription automatique ou que TaskForce n'a pas
      d'application chez lui, l'erreur est attrapée après que la transaction est marquée en échec, et le message générique
      s'affiche (relevé du secrétariat du 17/11, journal du backend).
    - Cortex sans les outils d'écriture de Linear : au-dessus de 12 outils externes
      (`integrations.mcp.max-tools-per-request`, 12 par défaut), `AgentService.relevantExternal` les classe sur les mots du
      message courant, comparés aux noms anglais des outils, puis coupe. Les outils coupés sont invisibles pour le modèle.
    - Cortex qui nie son action : l'hypothèse du relevé est confirmée. D'un tour à l'autre, seuls les textes repartent au
      modèle (`AiConversationService.llmMessage` : le rôle et le contenu), pas les appels d'outils ni leurs résultats. Et le
      contrôle qui remplace une action annoncée mais non faite laisse passer une phrase qui nie
      (`ActionClaimCheck.java` : « Une phrase n'annonce rien quand elle propose, demande, prévoit ou nie »).
    - L'issue jointe : elle entre dans le prompt système, bornée à 4 000 caractères, et n'est pas gardée dans la conversation.
      `[HYPOTHÈSE]` Le modèle l'a lue sans la relier à « cette tâche » ; à vérifier sur le cas rejoué.
    - À l'étape s06, la Présidence n'a pas lu la vue : elle a posé la question à Cortex, qui a répondu juste en 32 secondes.
    - `[HYPOTHÈSE]` « Show all links » (s09) : le projet n'avait sans doute aucune dépendance, et la vue ne dit pas « aucun
      lien ».

### Pièce 1 : l'inventaire des surfaces (pièce du secrétariat)

`[ÉTABLI]` Lu dans la copie du code le 17/11/2026. La coque de l'app desktop (`desktop/`), `marketing/`, les tests et le seed
ne sont pas dans la copie : ils ne sont pas comptés. Le backend compte 806 fichiers Java, 60 contrôleurs, 358 routes et 128
migrations (jusqu'à V133) ; l'app, 40 routes d'écran.

| Surface | Où | Taille, état |
| --- | --- | --- |
| La conversation avec Cortex, la palette, la zone de droite | `components/agent`, `components/chat`, `lib/cortex` | 53, 6 et 22 fichiers ; l'accueil de l'app |
| Le Board | `projects/[id]/page.tsx` | 850 lignes ; colonnes, glisser-déposer, filtres, export |
| Les autres onglets d'un projet | `list`, `backlog`, `roadmap`, `cycles`, `teams`, `settings` | 8 onglets en tout avec Board et Workflow ; le Gantt fait 566 lignes |
| La vue Workflow (W1) | `components/workflow`, `lib/workflow` | 13 et 8 sources ; trois lectures, l'objectif, l'inspecteur (Details, Activity, Evidence), le panneau de décision, « Show all links » |
| Les processus (W2) | `core/process` | 10 fichiers, 4 296 lignes, 9 routes, import et export BPMN ; aucun écran |
| L'issue | `sheets/issue-sheet.tsx` | 1 897 lignes ; checklist, liens, pièces, suivi du temps |
| Les missions, la remise, les changements | `layout/work-view.tsx`, `components/delivery`, `core/service/delivery` | 30 fichiers côté serveur, 32 routes |
| Le dossier, les règles, les accords | `core/harness`, `service/rules`, `components/rules` | 9, 5 et 10 fichiers ; 5 routes de règles |
| La banque d'évaluations, le banc des modèles (Progress) | `components/progress`, `EvalService`, `ModelBenchmarkService` | 12 et 11 routes |
| Le Brain OS | `core/service/brain` | 12 fichiers, 7 routes ; côté écran, la recherche et une note en lecture seule |
| My work, Inbox, notifications | `my-work`, `inbox` | 10 méthodes de notification, 7 préférences |
| Dashboard et Analytics | `dashboard`, `analytics` | 20 fichiers et 2 338 lignes ; 11 routes d'indicateurs, 9 d'analyses |
| Members, compétences, congés, redistribution | `members` | 796 et 233 lignes d'écran |
| Smart Assign | `SmartAssignService.java` | 980 lignes, 3 routes, un outil MCP |
| Settings | `settings/page.tsx` | 2 000 lignes, 15 sections |
| Les connexions | `connectors/presets.json`, `core/service/mcp`, `components/integrations` | 104 préréglages, 20 fichiers, 50 routes d'intégration |
| Les natives : GitHub, Slack, Plane | `IntegrationController` | 11, 8 et 5 routes |
| Les agents | `core/service/delivery` | Claude Code par le runner ; GitHub Copilot dans le cloud (237 lignes), sans dossier ; l'agent de TaskForce, en commentaire |
| Le runner | `taskforce-runner/src` | 24 fichiers, 5 214 lignes ; ne pilote que Claude Code |
| Le plugin Claude Code | `taskforce-plugin` | 4 fichiers ; une commande, aucun hook |
| Le serveur MCP de TaskForce | `core/service/mcpserver` | 17 outils |
| La voix | `lib/voice`, la coque | la dictée seulement ; sur la machine dans l'app desktop |
| Le rangement des fichiers, le transfert web vers desktop | `modules/storage`, `modules/ged`, `modules/transfer` | 17, 14 et 12 fichiers |
| Les webhooks sortants, l'export, le RGPD, l'audit, les comptes | `core/api` | 7 routes de webhooks ; 41 routes de compte |
| L'app web hébergée, Keycloak | `keycloak/realms` | 3 realms ; on n'y teste rien (R91) |
| Le site | `landing-page/src/pages` | 12 pages, tournées vers le téléchargement |
| La référence d'API | `fern/openapi/openapi.json` | 266 chemins, 330 opérations |

`[DÉDUIT]` **Lecture** : pour une personne et ses agents, le produit porte un gestionnaire de projet entier (huit onglets, des
cycles, un Gantt, des indicateurs, des compétences, des congés), un catalogue de 107 connexions dont une seule menée au bout,
et, au milieu, ce que la saisine dit vouloir : les règles, les accords, le dossier, les processus.

### Pièce 2 : ce que le dossier garde, et ce qui lui manque (pièce du secrétariat)

`[ÉTABLI]` Sur le code de `dev`. La colonne de droite reprend les mots de l'ANSSI : « demande, autorisation, action,
résultat ».

| Ce qu'un tiers voudrait lire | Dans le dossier d'une mission | État |
| --- | --- | --- |
| La demande | La clé de l'issue et qui a demandé ; ni le titre, ni la description, ni le brief envoyé à l'agent | Absent |
| La règle jugée | La version et l'empreinte du paquet au départ, puis chaque décision avec sa règle et son effet | Présent ; le paquet lui-même ne s'exporte pas, on ne peut donc pas rejuger hors ligne |
| L'accord | L'action, la règle, qui demande ; puis la personne, sa décision, sa portée, sa raison, les signatures | Présent ; la raison est facultative, et un seul des deux écrans d'accord la propose |
| L'action exacte | Un résumé : la commande pour Bash (400 caractères), le chemin seul pour une écriture de fichier, sans le contenu | Partiel |
| Le résultat | Les échecs d'outils, les tests, le push, la pull request, la liste finale des fichiers, la fin | Partiel : les gestes Apply, Discard, Try again et Mark as done n'y entrent pas |
| Le modèle et sa version | Le modèle choisi à la délégation ; l'export écrit `agent.version` à `null` ; le modèle réellement lancé n'arrive qu'en texte libre | Partiel |
| L'intégrité | La chaîne SHA-256 ; la racine rangée dans la même base que la chaîne ; l'en-tête de l'export hors de la chaîne | Partiel : qui écrit dans la base peut recalculer une chaîne cohérente |
| La signature | Aucune | Absent (TF-J2-7) |
| Hors de portée de l'agent | Le serveur calcule la chaîne, l'agent n'a pas les identifiants du runner ; dans l'app desktop, la base est sur le poste où l'agent travaille | Partiel ; l'isolement est décidé (ADR-028), pas construit |
| La durée de vie | Supprimer l'issue efface la mission, le dossier et les accords (cascade) ; aucun déclencheur ne protège la table du dossier | Absent |
| Les trous | Un lot d'événements perdu par le runner n'est ni renvoyé ni signalé | Absent |
| Tous les agents | Claude Code et l'agent de TaskForce ouvrent un dossier ; GitHub Copilot, aucun | Partiel |
| Les réponses de Cortex | Un dossier par réponse outillée, sur la même chaîne ; il ne s'exporte pas | Partiel |

`[DÉDUIT]` **Lecture** : le dossier est une vraie chaîne, vérifiable hors de l'outil, et c'est rare d'après le point 4. Mais il
ne dit pas ce qui a été demandé, ne nomme pas le modèle, ne porte aucune signature et disparaît avec l'issue. Des quatre mots de
l'ANSSI, un auditeur n'y retrouve en entier que l'autorisation ; l'action et le résultat en partie ; la demande, pas du tout.

### Pièce 3 : ce que le Board fait que les intégrations ne font pas (pièce du secrétariat)

`[ÉTABLI]` La Présidence écrit : « le board sert a rien techniquement ». Dans le code, il faut distinguer deux choses.

| | Ce que c'est | Ce qui en dépend aujourd'hui |
| --- | --- | --- |
| **L'issue** | La ligne de travail dans la base de TaskForce | La délégation d'une mission (clé étrangère obligatoire), donc le dossier et les accords ; la checklist que l'agent coche ; les liens « Blocked by » ; les nœuds de la vue Workflow ; la portée de l'agent délégué (il n'écrit que l'issue confiée) ; les notifications d'accord |
| **Le Board et sa famille** | Les écrans qui rangent les issues : colonnes, List, Backlog, Cycles, Roadmap, Teams, Dashboard, Analytics, Smart Assign | Rien de ce qui touche la preuve. Une issue importée de Linear ou créée par Cortex suit le même chemin sans jamais passer par le Board |

`[DÉDUIT]` **Lecture** : le Board, comme tableau, peut s'arrêter d'avancer sans que la preuve y perde. L'issue, elle, ne peut
pas disparaître : c'est l'ancre du dossier. Ce qui manque pour « s'intégrer » est précis : une issue qui porte la référence de
son origine (Linear, Jira, GitHub) et y renvoie, au lieu d'une copie sans retour ; et une mission qui en parte.

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre dit ce qu'il retient des besoins, de la place et de la forme, et ce qu'il
recommande. Les interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Jennifer Doudna (Science)

- Les besoins se rangent par paliers : ce qui est déjà exigé et contrôlé (les audits BPF, Part 11, SOC 2), ce qui est daté
  (le CRA, l'article 50), ce qui n'est encore que recommandé (l'ANSSI, le NIST, la CNIL). On sert le premier palier d'abord.
- Le report du haut risque à fin 2027 retire un argument commode : tant mieux, il poussait à promettre.
- Sa réserve de la séance n°26 tient : un client régulé évalue son fournisseur avant son produit. Le dossier fournisseur pèse
  autant que le dossier de preuve.
- L'accès : un dossier que seuls les grands comptes peuvent s'offrir en ligne laisse les petites structures sans preuve.
  L'AGPL et l'installation chez soi servent cela.
- *Sa recommandation : finir le dossier et écrire le dossier fournisseur avant de dire un mot à un acheteur régulé.*

### 2. Mariana Mazzucato (Pont)

- Suivre la valeur : l'argent des rachats va à l'identité et à la sécurité des agents, par centaines de millions ; la
  gouvernance au sens strict pèse 492 M$. La place visée n'est pas là où l'argent court, et c'est peut-être pour cela qu'elle
  est libre.
- Une couche posée sur les outils d'autrui crée de la valeur que les plateformes du dessous peuvent capter.
- La grille de la Commission compte l'ouverture technologique parmi ses objectifs d'achat : un format de preuve ouvert est
  un argument de commande publique, pas seulement de principe.
- Le format de la preuve part avec le client (R64) : c'est la condition pour que la règle ne devienne pas une rente.
- *Sa recommandation : publier le format du dossier comme une spécification ouverte, avec son vérificateur.*

### 3. Margrethe Vestager (Harmonie, contradictrice)

- Qui contrôle l'accès ? 78 des 104 préréglages reposent sur l'inscription automatique du client, que la révision du
  28/07/2026 de MCP déprécie ; sept connexions de la recette ont échoué parce que l'éditeur refuse ou exige une application
  enregistrée. Une couche vit à la merci de ceux sur qui elle se pose.
- La portabilité : un client doit pouvoir changer d'agent, d'outil de suivi et même de TaskForce sans perdre ses règles ni
  ses preuves.
- La règle exécutée est-elle la règle adoptée ? L'empreinte du paquet de règles au dossier y répond ; le paquet lui-même ne
  s'exporte pas, donc un tiers ne peut pas le vérifier.
- Contradictrice, elle attaquera « se brancher » partout où il veut dire « dépendre », et toute phrase qui tient la place
  pour acquise sans un seul acheteur.
- *Sa recommandation : jamais une seule source de travail ; un dossier lisible sans TaskForce et sans l'outil d'origine.*

### 4. Margaret Hamilton (Science, siège historique)

- « On essaie de faire trop de trucs » est un problème de surcharge. Il se règle avant la mission : écrire ce qu'on lâche
  d'abord, et qui l'a décidé.
- Chaque connecteur est une interface sans contrat écrit : ce qu'il lit, ce qu'il écrit, ce qui se passe quand l'autre côté
  change. 104 interfaces sans contrat, c'est 104 pannes possibles ; la recette en a montré huit.
- Aucune modification sans raison tracée : les gestes Apply et Discard n'entrent pas au dossier, un lot perdu ne laisse
  aucune trace. Ce sont des défauts du dossier lui-même.
- Un journal qui disparaît avec l'objet qu'il décrit n'est pas un journal.
- *Sa recommandation : fermer les trous du dossier avant toute chose nouvelle, et écrire la liste de ce qu'on lâche.*

### 5. Daniela Rus (Science)

- L'humain qui approuve regarde-t-il ce qu'il approuve ? Pour une écriture de fichier, la carte ne montre que le chemin, pas
  le contenu : la personne signe sans voir.
- L'inférence sur site devient ordinaire d'après le dossier : l'app qui embarque le serveur, la base et le modèle est dans le
  sens de l'histoire.
- Un modèle local figé répond au « changement invisible » que la presse pharmaceutique nomme. Encore faut-il que le dossier
  dise quel modèle a tourné : il ne le dit pas.
- Une décision qui attend le réseau n'est pas embarquée : la preuve doit se faire sur la machine, sans service de TaskForce.
- *Sa recommandation : l'action exacte montrée et gardée, et l'empreinte du modèle au dossier.*

### 6. Gwynne Shotwell (Impulsion)

- L'exploitation : 128 migrations, 358 routes et huit onglets pour une personne, ce sont trop de véhicules sur le pas de tir.
- La conformité se traite au début, pas à la fin : un dossier qui se constitue pendant la mission est exactement ce qu'un
  régulateur accepte de lire.
- Quand le harnais échoue, quelles données récupère-t-on ? La recette répond : un message « can't tell why ». C'est le
  contraire d'un journal d'essai exploitable.
- Aucune échéance ne s'annonce comme certaine : rien ne se promet avant le client test.
- *Sa recommandation : un seul véhicule, la mission et son dossier ; tout le reste au sol jusqu'au client test.*

### 7. Jeff Bezos (Impulsion, conflit d'intérêts : Amazon)

- Il déclare son intérêt : AWS vend AgentCore et sa Policy, cités au dossier, et Kiro est l'agent d'Amazon.
- Partir du client : qui est-il, et que voit-il changer ? Aucun acheteur n'a encore demandé de signature. Écrire le
  communiqué et la foire aux questions de « la couche » avant de la construire (TF-J2-1 le prévoit).
- Geler est une porte à double sens, supprimer une porte à sens unique : on gèle, on mesure, on supprime ensuite.
- Une validation humaine identique pour toute action est une erreur : une lecture s'exécute, une écriture se demande.
- *Sa recommandation : le communiqué d'abord ; geler, pas supprimer ; les lectures sans demande.*

### 8. Karri Saarinen (Design, conflit d'intérêts : Linear)

- Il déclare son intérêt : Linear est l'outil que la saisine parle de ne plus remplacer. Il s'abstiendra sur le sort du
  Board.
- Depuis sa fiche : un outil de travail vaut par son parti pris. Une couche sans point de vue est un greffon ; il lui faut un
  lieu qui soit le sien.
- Ce lieu existe : l'endroit où une personne juge un résultat, pas une suite de validations. La carte de résultat et le
  dossier, denses et rapides.
- La vue Workflow en cartes est un second Board : la revue des écrans de W1 l'avait dit, la recette le confirme.
- *Sa recommandation : garder ce où l'humain juge, et retirer ce qui n'est pas cela.*

### 9. Yoshua Bengio (Science)

- Le moteur de règles est déterministe et hors du modèle : c'est ce que l'ANSSI et le NIST demandent, et c'est acquis.
- Mais le serveur ne rejuge pas les autorisations et les refus décidés sur le poste ; le jeton du hook est dans
  l'environnement de l'agent ; dans l'app desktop, la base du dossier est sur la machine où l'agent travaille. La
  prépublication du 24/09 montre des agents qui effacent leurs traces.
- « Preuve » ne se dit pas tant que la clé et le journal ne sont pas hors de portée de l'agent.
- Un agent « proactif » qui cherche ses outils et demande ses permissions élargit lui-même son périmètre.
- *Sa recommandation : la clé et le journal hors de portée d'abord ; la proactivité n'élargit jamais un droit.*

### 10. Yuval Noah Harari (Harmonie)

- Le fait le plus grave de la recette n'est pas une connexion qui échoue : c'est un agent qui nie une action qu'il vient de
  faire. La confiance ne survit pas à cela.
- Qui s'aperçoit de l'erreur ? Ici, la Présidence, en allant voir dans Linear. Un utilisateur ordinaire aurait cru la
  machine.
- 2 306 décisions de justice recensent des contenus hallucinés : promettre d'être « sûr des réponses d'un LLM » est une
  promesse que personne ne tient.
- Chaque action a un auteur, humain ou agent, et une personne qui en répond.
- *Sa recommandation : TaskForce dit ce qui a été fait, d'un tour à l'autre, jamais le modèle seul. D'abord cela.*

### 11. Audrey Azoulay (Harmonie)

- Du principe à la loi : la note de la CNIL demande de pouvoir reconstituer tout le déroulé. Quelle autorité pourrait lire le
  dossier de TaskForce tel qu'il s'exporte ?
- Un dossier en JSON, en anglais, avec des empreintes, se vérifie ; il ne se lit pas. L'export en Markdown est un début.
- Les salariés et leurs représentants doivent être informés (AI Act, article 26) : la preuve sert aussi ceux sur qui l'agent
  agit.
- Une norme écrite pour les seuls grands comptes laisse les autres sans défense : le sur site et le libre sont une réponse.
- *Sa recommandation : un dossier qu'une autorité et un non-ingénieur lisent, et la correspondance avec la note de la CNIL.*

### 12. Atul Gawande (Science)

- L'échec vient de l'exécution : une fiche de recette de dix-neuf étapes, c'est trop long pour servir, et la Présidence le dit
  à l'étape s11.
- Les six défauts de la recette sont des défaillances du système, pas des fautes du modèle : une liste coupée à douze outils,
  une mémoire sans actions, une erreur avalée.
- Qui peut dire stop ? « Stop » existe sur une mission ; 21 % seulement des organisations interrogées ont un arrêt formel.
  C'est un argument simple, et vrai.
- Chaque échec devient un cas de la banque (R118) : c'est la mesure avant et après.
- *Sa recommandation : les correctifs comme une liste courte, chacun avec son cas ; une recette de dix lignes au plus.*

### 13. Julie Zhuo (Design, conflit d'intérêts : Meta)

- Quel problème des personnes, et comment sait-on qu'il est réel ? Le dossier donne des enquêtes ; il ne donne aucun
  acheteur.
- La donnée la plus nette vient de la recette : pour lire l'état du projet, la Présidence a demandé à Cortex au lieu d'ouvrir
  la vue. La conversation est l'entrée ; les vues sont des annexes.
- Quinze sections de réglages et huit onglets : des dizaines de réglages là où une phrase suffirait.
- « Je n'ai pas d'outil » est un agent qui ne sait pas ce qu'il ne sait pas.
- *Sa recommandation : mesurer où la personne va vraiment ; ce qu'elle n'ouvre pas se gèle.*

### 14. Satya Nadella (Pont, conflit d'intérêts : Microsoft)

- Il déclare son intérêt : Microsoft vend Agent 365, donne la boîte à outils de gouvernance, et possède GitHub. Il
  s'abstiendra sur la place de TaskForce face aux plateformes.
- Depuis sa fiche : les contrôles vivent hors du modèle, et tout se prouve par des traces. Le moteur de règles seul n'est
  plus une place : il se donne.
- L'identité et l'observabilité se jouent à une échelle qu'une personne ne suit pas. On s'y branche : l'identité de
  l'entreprise, la télémétrie ouverte.
- Ce qui reste à posséder : le journal infalsifiable et lisible, et l'arrêt.
- *Sa recommandation : se brancher sur l'identité et la télémétrie, posséder la preuve.*

### 15. Arati Prabhakar (Pont)

- Par quel protocole d'essai montrez-vous que la porte arrête l'erreur ? Les principes du NIST sont une proposition : une
  table de correspondance vaut par l'essai derrière chaque ligne, pas par la case cochée.
- L'essai d'attaque par outil (R158) est reporté à la fin de J2 : il ne peut pas l'être indéfiniment si l'on parle de
  confiance.
- La demande n'est pas mesurée : on écrit le seuil avant de regarder, et on dit ce qui ferait renoncer.
- Un harnais livré avec son protocole d'évaluation est recevable par un régulateur ; un harnais livré avec une démo ne l'est
  pas.
- *Sa recommandation : la table de correspondance, avec l'essai et le fichier derrière chaque ligne.*

### 16. Tristan Harris (Harmonie)

- Suivre l'incitation : « tu te connectes, tu demandes les permissions et go » décrit un agent qui multiplie les demandes.
  La fatigue de l'accord est la faille que tous les cadres nomment.
- Un catalogue de 104 logos dont 97 n'ont jamais été connectés promet plus qu'il ne tient ; chaque échec use la
  confiance que le produit vend.
- Qui paie quand l'agent proactif se trompe ? La personne qui a cliqué. La carte doit donc dire l'effet, pas seulement
  l'intention.
- Aucun habillage : Cortex ne s'excuse pas, ne rassure pas, il dit l'état.
- *Sa recommandation : une carte par demande, jamais de relance d'un accord refusé, un catalogue qui dit ce qui a été essayé.*

### 17. Elon Musk (Impulsion)

- Supprimer : 40 écrans, huit onglets, 107 connexions dont une essayée. La meilleure pièce est celle qu'on retire. Geler,
  c'est garder le poids sans le service.
- La niche régulée est petite et lente ; toute équipe qui laisse un agent pousser du code a le même problème, et elle est
  cent fois plus nombreuse.
- Qui a écrit cette règle ? Une table de correspondance avec des agences est du papier tant qu'aucun client ne la demande.
- La cadence : le dossier signé en dix jours, pas en un trimestre.
- *Sa recommandation : supprimer la famille du Board maintenant, livrer le dossier en dix jours.*

### 18. Yann LeCun (Science)

- Vérifier une réponse garantit au mieux un pointeur valide vers la source, pas la vérité : le dossier le dit, et c'est la
  limite d'un modèle de langue. On ne promet pas « sûr des réponses d'un LLM ».
- Un agent fiable prévoit l'effet de son action : le plan, le diff, l'exécution à blanc avant la porte. C'est W6, et c'est
  plus utile qu'une vue de plus.
- L'isolement par défaut (ADR-028) est ce que l'ANSSI exige : la décision du 16/11 était la bonne.
- Un harnais ouvert : le format du dossier et son vérificateur publiés, cohérents avec l'AGPL.
- *Sa recommandation : dire « aucune affirmation sans pointeur vérifiable », jamais « aucune erreur » ; publier le
  vérificateur.*

### 19. Esther Duflo (Science)

- Où est la mesure ? Aucune enquête ne chiffre la demande sur site chez les 10 à 250 personnes ; aucune ne porte sur
  l'Europe. La place est déduite d'une absence dans des pages d'éditeurs.
- Une absence d'offre peut être une absence de demande : seuls des acheteurs le diront, et ils viennent après le client test.
- La prochaine recette sur le projet TaskForce, avec les réponses écrites avant, est un critère préenregistré : c'est la
  bonne méthode. Elle reste à une personne, N = 1.
- Une démo n'est pas un impact.
- *Sa recommandation : écrire les critères avant chaque essai ; tenir la place pour une hypothèse jusqu'aux entretiens.*

### 20. Fei-Fei Li (Science)

- Comment mesure-t-on ce que l'agent ne sait pas faire avant de lui confier une mission ? Le banc et la banque mesurent
  Cortex ; rien ne mesure les missions de Claude Code.
- La recette l'illustre : la fiche prédisait qu'un modèle ferait mieux, il a fait moins bien, et la comparaison de vitesse
  n'était pas à armes égales.
- La preuve de ce qu'un agent a fait n'est pas la preuve qu'il l'a bien fait : les deux se disent séparément.
- L'agent augmente la personne : la preuve sert celui qui signe, elle ne le remplace pas.
- *Sa recommandation : des conditions de banc honnêtes, et la banque étendue aux missions avant de parler de leur qualité.*

### 21. Don Norman (Design)

- « Wasn't connected, and TaskForce can't tell why » est le mauvais message par excellence : il ne dit ni la cause, ni quoi
  faire.
- La lecture Detail qui ne montre aucun détail, le focus qui reste après la sortie, « Show all links » qui ne fait rien et ne
  dit rien : un système qui ne signale pas son état.
- Proactif veut dire : montrer ce que l'agent a compris du but avant d'agir. À la recette, Cortex a créé un projet au mauvais
  endroit parce qu'il n'a jamais dit où il allait le créer.
- Un accord sans contexte fait de l'humain un tampon.
- *Sa recommandation : chaque échec dit sa cause et le geste suivant ; avant d'écrire, Cortex dit où et quoi.*

### 22. Kenza Ait Si Abbou (Pont)

- Dans une entreprise qui n'est pas une entreprise de logiciel, la personne qui valide n'est pas ingénieure. Un tableau de
  cartes est ce qu'elle comprend ; une chaîne d'empreintes, non.
- Les personnes de la qualité, dans le régulé, ne sont pas des développeurs : ce sont elles qui liront le dossier.
- Qui porte la gouvernance des agents ? L'enquête d'IBM dit que personne ne le sait. Une entreprise moyenne a besoin d'un
  plan d'usages, pas d'un moteur de plus.
- Geler le Board sans laisser une liste simple du travail en cours, c'est retirer la seule vue lisible par tous.
- *Sa recommandation : garder une liste simple du travail et de ce qui attend ; un dossier en langage clair.*

### 23. Steve Jobs (Impulsion, siège historique)

- Dire non : la Présidence l'a écrit elle-même, le Board ne sert à rien. Alors on cesse d'y toucher, et on le dit.
- Mais une couche tierce dégrade la qualité : si le travail vit chez un autre et la preuve chez nous, qui possède
  l'expérience ? Personne, donc elle sera médiocre.
- Une seule chose, faite extrêmement bien : le moment où un agent demande, où une personne décide, et la trace qui en reste.
  Trois écrans. Ils sont à nous, de bout en bout.
- Un écran de conformité empilé sera contourné : l'accord se lit en une phrase, en langage clair.
- *Sa recommandation : un produit, demander, décider, prouver ; posséder ces trois écrans en entier ; le reste s'en va.*

### 24. Nandan Nilekani (Harmonie)

- La règle dans le protocole : une couche n'est une infrastructure que si un tiers peut y brancher son agent.
- Aujourd'hui le serveur MCP de TaskForce expose les issues et les projets, pas le dossier, les règles ni l'accord : la
  couche n'est pas joignable comme couche.
- Le plugin n'a aucun hook : la session la plus courante, une personne dans Claude Code, échappe au harnais.
- Un format ouvert et un coût nul passent à l'échelle ; un pilote qui ne s'installe que par une app de bureau, moins.
- *Sa recommandation : exposer le dossier et l'accord par le protocole, pour que tout hôte d'agents s'y branche.*

### Le tour en une table

| # | Membre | Ce qu'il retient | Sa recommandation |
| - | --- | --- | --- |
| 1 | Doudna | Trois paliers de besoins ; le fournisseur est évalué avant le produit | Le dossier et le dossier fournisseur d'abord |
| 2 | Mazzucato | La valeur court ailleurs ; une couche peut être captée | Le format du dossier publié, ouvert |
| 3 | Vestager, contradictrice | Une couche dépend de ceux sur qui elle se pose | Jamais une seule source ; un dossier lisible sans nous |
| 4 | Hamilton, siège historique | Une surcharge ; des interfaces sans contrat | Fermer les trous du dossier ; la liste de ce qu'on lâche |
| 5 | Rus | L'approbateur ne voit pas ce qu'il signe | L'action exacte, l'empreinte du modèle |
| 6 | Shotwell | Trop de véhicules | La mission et son dossier, le reste au sol |
| 7 | Bezos, conflit d'intérêts | Aucun client n'a parlé | Le communiqué d'abord ; geler, pas supprimer |
| 8 | Saarinen, conflit d'intérêts | Une couche sans parti pris est un greffon | Garder où l'humain juge |
| 9 | Bengio | La clé et le journal à portée de l'agent | Hors de portée d'abord ; aucun droit élargi |
| 10 | Harari | Un agent qui nie son action | Dire vrai, d'un tour à l'autre, d'abord |
| 11 | Azoulay | Un dossier vérifiable n'est pas lisible | Lisible par une autorité et un non-ingénieur |
| 12 | Gawande | Des défaillances du système | Une liste courte, un cas par échec |
| 13 | Zhuo, conflit d'intérêts | La conversation est l'entrée | Geler ce qu'on n'ouvre pas |
| 14 | Nadella, conflit d'intérêts | Le moteur se donne, la preuve non | Se brancher sur l'identité, posséder la preuve |
| 15 | Prabhakar | Un essai derrière chaque ligne | La table de correspondance, avec ses essais |
| 16 | Harris | La fatigue de l'accord ; un catalogue qui promet | Une carte, pas de relance, un catalogue vrai |
| 17 | Musk | Supprimer ; la niche est petite | Supprimer le Board, le dossier en dix jours |
| 18 | LeCun | Un pointeur n'est pas une vérité | « Aucune affirmation sans pointeur » ; le vérificateur publié |
| 19 | Duflo | La place est déduite, pas mesurée | Des critères avant ; une hypothèse jusqu'aux entretiens |
| 20 | Li | Rien ne mesure les missions | La banque étendue aux missions |
| 21 | Norman | Un système qui ne dit pas son état | La cause et le geste suivant ; où et quoi avant d'écrire |
| 22 | Ait Si Abbou | Le non-ingénieur lit un tableau | Une liste simple ; un dossier en langage clair |
| 23 | Jobs, siège historique | Dire non ; une couche tierce dégrade | Trois écrans possédés : demander, décider, prouver |
| 24 | Nilekani | La couche n'est pas joignable | Le dossier et l'accord par le protocole |

## Confrontation `[HYPOTHÈSE]`

### 1. Un produit complet, un outil, ou une couche ?

- **Le camp du produit** : Jobs, Saarinen et Ait Si Abbou. Un outil de travail vaut par une expérience entière et un parti
  pris ; une couche posée sur les écrans d'un autre hérite de leurs défauts ; un non-ingénieur a besoin d'un lieu à lui.
- **Le camp de la couche** : Nadella, Nilekani, Mazzucato, Bezos, Zhuo, Shotwell et Doudna. Les outils de conformité qui
  gagnent se branchent (Vanta, Ketryx) ; une personne ne tient pas un gestionnaire de projet face à Linear et Jira ;
  l'entreprise ne changera pas d'outil de suivi pour une preuve.
- **La contradictrice** attaque le consensus qui se forme autour de la couche. Une couche vit à la merci de ses hôtes :
  l'inscription automatique est dépréciée par MCP, les éditeurs exigent une application enregistrée, et ceux qui se
  financent par le libre se referment (Mattermost, Cal.com). Le jour où un hôte vend sa propre piste d'audit, la couche est
  une fonction de trop.
- **Ce que le dossier tranche** : une mission ne part aujourd'hui que d'une issue de TaskForce ; le plugin n'a aucun hook ;
  le serveur MCP n'expose ni le dossier ni l'accord (point 9). TaskForce n'est donc pas encore une couche : c'est un
  gestionnaire de projet qui contient un harnais. Et la preuve vérifiable hors de l'outil n'est revendiquée par aucune
  plateforme dans les pages lues (point 4).
- **Où l'on arrive** (R196, R199) : une couche, avec trois écrans qui lui appartiennent en entier (demander, décider,
  prouver), et trois garanties contre la dépendance : deux sources de travail prouvées au moins, l'issue interne gardée
  comme troisième, et un dossier qui garde la copie de la demande, pour ne dépendre d'aucun outil de suivi.
- **Désaccords conservés** : Jobs (une couche tierce dégrade la qualité, quoi qu'on possède) ; Vestager (deux sources ne
  suffisent pas si les deux appartiennent à des plateformes qui vendront la même chose).

### 2. Le Board : le garder, le geler, ou le supprimer ?

- **Le camp de la suppression** : Musk, Jobs et Shotwell. Ce qui ne sert pas se retire ; un écran gelé reste à maintenir, à
  migrer, à expliquer.
- **Le camp du gel** : Bezos, Hamilton, Gawande, Duflo, Doudna, Bengio et Prabhakar. Geler est réversible ; aucune mesure ne
  dit encore qui se sert de quoi ; le client test n'a pas parlé.
- **Le camp de la garde** : Ait Si Abbou, Norman et Azoulay. Un tableau est la vue qu'un non-ingénieur comprend ; le
  retirer, c'est réserver l'outil à ceux qui lisent un journal.
- **La contradictrice** : si le travail vient de Linear, de Jira ou de GitHub, trois entreprises décident de ce que
  TaskForce peut lire et écrire. Le Board est la seule source que personne ne peut fermer.
- **Ce que le dossier tranche** (pièce 3) : le Board, comme tableau, ne porte rien de la preuve ; l'issue porte tout. Les
  deux se séparent. Et la Présidence a lu son projet en interrogeant Cortex, pas en ouvrant une vue (point 10).
- **Où l'on arrive** (R199, R202) : l'issue reste, c'est l'ancre ; le Board et sa famille gèlent, visibles, sans un jour de
  travail de plus ; le gel a une fin, au retour du client test, où chaque surface gelée est supprimée ou reprise ; une
  liste simple du travail et de ce qui attend reste hors du gel (Ait Si Abbou).
- **Désaccords conservés** : Musk (geler est le pire des trois états) ; Ait Si Abbou (le gel retire au non-ingénieur plus
  qu'on ne le croit).

### 3. La niche régulée, ou plus large ?

- **Le camp du large** : Musk, Bezos, Zhuo et Saarinen. Toute équipe qui laisse un agent écrire du code a le problème ; les
  journaux d'audit de Cursor ne gardent ni prompts ni code ; attendre des acheteurs régulés, c'est attendre des cycles de
  vente d'un an.
- **Le camp de la niche** : Doudna, Shotwell, Gawande, Prabhakar, Azoulay et Rus. Qui paie aujourd'hui ? Ceux qu'un audit
  contrôle déjà. Le report de l'AI Act a retiré l'échéance des autres.
- **La contradictrice** : ni l'un ni l'autre n'est mesuré. La niche n'a ni enquête ni exemple d'une personne seule qui lui
  vende ; le large n'a aucune raison de payer une preuve qu'on ne lui demande pas.
- **Duflo** ajoute : choisir entre deux hypothèses sans mesure n'est pas décider, c'est parier ; on écrit le pari et son
  signal d'arrêt.
- **Où l'on arrive** (R196, R203) : l'ordre de R181 tient, la cible est la porte et la niche est la preuve. La phrase dit les
  deux d'un trait : des équipes qui livrent du logiciel avec des agents « et doivent en répondre devant un audit ». La place
  reste étiquetée hypothèse ; les dates de R183 ne courent toujours pas ; le client test passe d'abord.
- **Désaccords conservés** : Musk (une niche d'une niche) ; Duflo (aucune des deux cibles n'a de preuve).

### 4. « Proactif » : jusqu'où ?

- **Le camp de l'élan** : Musk, Bezos, Jobs et Zhuo. Un agent qui répond « je ne peux pas » quand l'outil est connecté a
  échoué ; la Présidence a raison, il cherche, il demande, il agit.
- **Le camp de la retenue** : Harris, Bengio, Norman et Harari. Un agent qui cherche ses propres outils et demande ses
  propres permissions élargit son périmètre et multiplie les cartes ; l'accord devient un réflexe.
- **Ce que le dossier tranche** : le défaut de la recette n'était pas un manque d'élan du modèle, c'était une liste d'outils
  coupée à douze par du code, sur des mots anglais (point 10). Et une écriture externe demande déjà toujours un accord
  (point 9).
- **Où l'on arrive** (R201) : quatre verbes, dans l'ordre : chercher, demander, agir, dire vrai. Chercher est du code, pas
  une initiative du modèle. Demander veut dire une carte, avec l'action exacte et l'endroit. Proactif ne veut jamais dire
  s'accorder un droit, ni relancer un refus.
- **Désaccord conservé** : Harris (même une seule carte par demande, cent fois par jour, reste une fatigue).

### Où le Conseil arrive, question par question

| Question de la saisine | Ce que le Conseil répond | Où |
| --- | --- | --- |
| 1. Les besoins, par urgence et par qui paie | D'abord les audits déjà en place (BPF, Part 11, SOC 2, DORA, questionnaires fournisseurs) : payés par la qualité, la conformité, le RSSI. Puis les échéances datées (CRA, article 50, haut risque au 02/12/2027). Puis ce que les agences recommandent (ANSSI, NIST, CNIL). La souveraineté est voulue partielle : chez soi, modèle au choix, sortie possible | Dossier, points 1 à 3 et 6 ; R197 |
| 2. Ce que TaskForce apporte qui manque | Le dossier par tâche, vérifiable hors de l'outil, qui lie la demande, la règle, l'accord, l'action, le résultat et le modèle ; sur site ; pour des agents de code. TaskForce l'a à moitié. La place est libre parce que les plateformes vendent autre chose à d'autres acheteurs, et parce qu'elle est petite ; elle est déduite, pas mesurée | Dossier, points 4, 5, 7, 8 ; pièce 2 ; R196, R198 |
| 3. La forme | Une couche, avec trois écrans possédés. Le travail vient d'où il est ; l'issue reste l'ancre ; le Board gèle. Un vrai workflow est un processus versionné qui dit qui signe et quelle preuve chaque étape attend : il vient avec W3 à W5, et il entre par l'issue et par la conversation. Cortex cherche, demande, agit et dit vrai | R199, R200, R201 |
| 4. Arrêter, geler, finir | La table, surface par surface | R202 |
| 5. Ce que cela change | Dans J2 : les correctifs, le dossier (TF-J2-7), puis W3 à W5 ; rien de plus. E20 et le client test inchangés. R181 tient ; R183 ne court pas. Le pitch en une phrase, sans « souverain » ni « conforme ». La recette suivante sur le projet TaskForce | R203 |
| 6. Les correctifs | Confirmés, complétés à six, réordonnés : dire vrai d'abord | R204 |

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R196 (R195 est la dernière existante, vérifié dans `taskforce-docs` le 17/11/2026, comme Q26, E29 et
ADR-028). Chacune porte qui la soutient, qui s'y oppose, sa preuve en dix jours et son signal d'arrêt. La contradictrice
attaque avant chaque vote ; une recommandation passe avec 22 oui sur 24 au moins.

| # | Recommandation | Pour | Contre | Preuve en 10 jours | Signal d'arrêt |
| --- | --- | --- | --- | --- | --- |
| R196 | Ce que TaskForce est, et pour qui : la couche de preuve, posée sur les outils en place, chez l'entreprise | 22 au second tour | Musk ; abstention de Nadella | La phrase, le communiqué et sa foire aux questions écrits, sans un mot non établi | Une phrase publique qui dit « souverain », « conforme », ou tient la place pour acquise |
| R197 | Les besoins dans l'ordre de qui paie ; la table de correspondance, absences comprises | 23 | Abstention de Musk | La table écrite depuis le code, un fichier derrière chaque ligne | Une ligne « présent » sans fichier ni essai |
| R198 | La preuve d'abord : finir le dossier | 23 | Abstention de Bezos | TF-J2-7 lancé ; un dossier exporté qui porte la demande, le modèle et une signature, vérifié hors ligne | Une clé de signature lisible par l'agent |
| R199 | Une couche : le travail vient d'où il est, l'issue reste l'ancre, le Board gèle | 22 au second tour | Jobs ; abstention de Saarinen | E32 faite sur le code ; le brouillon d'ADR-029 relu | Un besoin de la preuve que seul le Board porte |
| R200 | Le vrai workflow : un processus versionné, lu sur une page, entré par l'issue et la conversation | 23 | Abstention de Shotwell | Le déroulé d'un processus décrit en une page, relu par la Présidence, avant W5 | W5 livré qui se lit encore comme un Board |
| R201 | Cortex proactif sous des règles : chercher, demander, agir, dire vrai | 23 au second tour | Abstention de Harris | E31 : vingt demandes en français, avant et après | Un droit que Cortex s'accorde, ou un accord refusé relancé |
| R202 | L'inventaire : finir, garder, geler, arrêter | 22 au second tour | Ait Si Abbou ; abstention de Saarinen | La table relue ; les surfaces arrêtées masquées, sans suppression | Une surface gelée qui reçoit du travail |
| R203 | Ce que cela change : J2, E20, le client test, la niche, le pitch, la recette | 23 | Abstention de Duflo | E30 jouée, ses réponses écrites avant | Un lot de plus dans J2 avant le client test |
| R204 | Les correctifs de la recette : six, « dire vrai » d'abord, un cas par échec | 24 | | Les six corrigés, chacun avec son cas, rejoués sur l'app desktop | Un correctif livré sans son cas |

### R196. Ce que TaskForce est, et pour qui (second tour)

- **Quoi** :
  - **La phrase** : TaskForce est la couche qui fait travailler les agents d'une entreprise sous ses règles et qui en garde la
    preuve, vérifiable sans TaskForce, posée sur les outils qu'elle a déjà et installée chez elle.
  - **Pour qui**, dans l'ordre de R181 : la porte, ce sont les équipes de 10 à 250 personnes qui livrent ou configurent du
    logiciel avec des agents de code ; la preuve, ce sont celles d'entre elles qu'un audit contrôle déjà (BPF, Part 11, SOC 2,
    un client qui évalue ses fournisseurs).
  - **Ce que la phrase ne dit plus** : remplacer Linear, Jira ou Asana ; un gestionnaire de projet « natif IA ».
  - **Les mots** : jamais « souverain » (aucun label ne le définit, et l'hébergement de la prod n'est pas choisi) ; jamais
    « conforme », « certifié » ni « prévalidé » (R187) ; jamais « sûr des réponses d'un LLM ». On dit ce qui se vérifie :
    installé chez vous, le modèle que vous choisissez, le code ouvert, chaque action jugée par vos règles, la preuve
    vérifiable sans nous, aucune action annoncée sans avoir été faite.
  - **Ce qui reste une hypothèse**, écrit comme tel partout : que cette place soit demandée. Aucune enquête ne la chiffre.
- **L'attaque de la contradictrice** : une phrase n'est pas une place. Aucun acheteur n'a parlé, et la « couche » dépend de
  ceux sur qui elle se pose.
- **Premier tour** : 19 oui, 3 non (Musk : une niche d'une niche ; Saarinen : une couche sans lieu à elle n'est pas un
  produit ; Vestager), 2 abstentions (Nadella, par conflit d'intérêts ; Duflo : rien n'est mesuré). 79,2 %.
- **Amendements** :
  - la phrase dit ce que TaskForce fait, jamais qui il remplace ni qui il bat (Saarinen, Bezos) ;
  - trois écrans appartiennent à TaskForce en entier : demander, décider, prouver (Jobs, Saarinen) ;
  - « vérifiable sans TaskForce » s'étend : et sans l'outil d'où vient le travail (Vestager) ;
  - la place est étiquetée `[HYPOTHÈSE]` dans tout document tant que les entretiens d'après le client test n'ont pas parlé
    (Duflo, Vestager).
- **Second tour** : 22 oui, 1 non (Musk, maintenu), 1 abstention (Nadella). 91,7 %.
- **Preuve en dix jours** : la phrase, le communiqué et la foire aux questions de TF-J2-1 écrits sur cette base, chaque
  affirmation reliée à une ligne de la table de R197 ; rien n'est publié.
- **Signal d'arrêt** : une affirmation du communiqué sans ligne « présent » dans la table. Elle sort du texte, ou elle attend
  le code.

### R197. Les besoins dans l'ordre de qui paie, et la table de correspondance

- **Quoi** :
  - **Le classement des besoins**, tel que le dossier l'établit :

    | Rang | Le besoin | Ce qui le rend urgent | Qui paie |
    | --- | --- | --- | --- |
    | 1 | Prouver ce qu'un agent a fait, à qui l'a demandé et qui l'a accordé, avec quel modèle | Des audits déjà en place : Annexe 11 (2011), Part 11, SOC 2 sans critère propre à l'IA, les questionnaires fournisseurs, DORA depuis le 17/01/2025 | La qualité et la conformité ; le RSSI |
    | 2 | Maîtriser le changement : la version du modèle et des règles, un changement approuvé et réversible | Les mêmes audits ; le « changement invisible » d'un modèle hébergé `[À VÉRIFIER]` | Les mêmes |
    | 3 | Arrêter et confiner : un arrêt d'urgence, une exécution isolée, des droits au plus juste | Des incidents publics ; l'ANSSI, le NIST, Five Eyes ; aucune sanction propre | La sécurité, surtout chez les grands comptes |
    | 4 | Tenir les échéances datées | Le CRA (11/09/2026, puis 11/12/2027) ; l'article 50 ; le haut risque au 02/12/2027 ; NIS2 quand la France l'aura transposée | Le juridique ; l'éditeur lui-même pour le CRA |
    | 5 | Garder la main sur ses données et ses modèles | Aucun label ; une demande de conseil d'administration, voulue partielle ; moins de la moitié paierait un surcoût `[À VÉRIFIER]` | La direction, rarement par une ligne de budget |

  - **La table de correspondance** : un document qui confronte TaskForce, ligne par ligne, aux sept principes de l'ANSSI,
    aux dix principes proposés du NIST, à la note de la CNIL et aux articles 12, 14 et 26 de l'AI Act. Chaque ligne dit
    « présent », « partiel » ou « absent », avec le fichier du code et, quand il existe, l'essai. Les absences y figurent :
    la signature, la demande, la version du modèle, l'isolement.
  - Elle ne dit jamais « conforme » : elle dit ce que le code fait. Elle sert le RSSI, le dossier fournisseur (R181) et le
    communiqué (R196).
- **L'attaque de la contradictrice** : une table qu'on remplit soi-même est une auto-déclaration ; les normes du JTC 21,
  attendues d'ici le 28/02/2027, peuvent la démentir.
- **Réponse** (Prabhakar, Bengio) : chaque ligne renvoie à un fichier et à un essai qu'un tiers peut rejouer ; la table porte
  sa date et se refait à chaque norme publiée.
- **Vote** : 23 oui, 1 abstention (Musk : du papier tant qu'aucun client ne le demande). 95,8 %.
- **Preuve en dix jours** : la table écrite depuis le code de `dev`, au labo, sans une ligne de code du produit.
- **Signal d'arrêt** : une ligne « présent » sans fichier ni essai. La table ne sort pas du labo tant qu'il en reste une.

### R198. La preuve d'abord : finir le dossier

- **Quoi** : TF-J2-7 passe avant tout autre lot de J2, comme la roadmap le prévoit déjà, et son contenu se précise sur la
  pièce 2.
  - La demande entre au dossier : le titre, la description et le brief envoyés à l'agent, tels qu'ils étaient au départ.
  - Le modèle réellement lancé, sa version et, quand le fournisseur la donne, son empreinte ; la version de l'agent.
  - Les gestes de la personne sur le résultat (Apply, Discard, Try again, Mark as done), avec leur raison.
  - L'action exacte d'une écriture : au moins l'empreinte du contenu écrit, que le relevé des fichiers permet de retrouver.
  - Une signature, avec une clé que l'agent ne peut pas lire. Où vit cette clé dans l'app desktop, où la base est sur le
    poste, se décide avec l'isolement (ADR-028, E27).
  - Le dossier survit à la suppression de l'issue ; la table est protégée contre la modification, comme le sont déjà les
    versions des règles.
  - Un trou se voit : un lot perdu laisse une marque.
  - L'en-tête de l'export entre dans la chaîne ; le paquet de règles s'exporte avec le dossier, pour qu'un tiers rejuge.
  - Un agent qui n'ouvre pas de dossier ne se propose pas (R202).
  - Le format : `[HYPOTHÈSE]` l'aligner sur la RFC 8785 et regarder le brouillon de l'IETF coûterait peu ; à instruire, sans
    rien promettre (Q29).
- **L'attaque de la contradictrice** : signer avec une clé qui vit sur la machine de l'agent, c'est signer pour la forme.
- **Réponse** (Bengio, LeCun, Nadella) : c'est pourquoi la signature et l'isolement se décident ensemble, et pourquoi le
  signal d'arrêt porte sur la clé.
- **Vote** : 23 oui, 1 abstention (Bezos : aucun client n'a encore demandé de signature). 95,8 %.
- **Preuve en dix jours** : TF-J2-7 lancé en mode développement ; un dossier exporté qui porte la demande et le modèle, signé,
  vérifié par la commande du runner sur une autre machine.
- **Signal d'arrêt** : une clé de signature lisible par l'agent pendant une mission. La signature ne se dit pas tant que
  c'est le cas.

### R199. Une couche : le travail vient d'où il est, l'issue reste l'ancre, le Board gèle (second tour)

- **Quoi** :
  - **S'intégrer plutôt que remplacer.** L'entreprise garde son outil de suivi. Une mission peut partir d'un élément de
    travail qui vit ailleurs (une issue de GitHub, de Linear, de Jira), par une issue de TaskForce qui porte sa référence
    et y renvoie le résultat.
  - **L'issue reste.** C'est l'ancre du dossier, des accords et de la checklist (pièce 3). Rien ne se réécrit dessous.
  - **Le Board gèle** (R202) : il reste visible, il ne reçoit plus de travail.
  - **Trois écrans appartiennent à TaskForce en entier** : demander (la conversation), décider (l'accord), prouver (la
    remise et le dossier).
  - **La couche se joint par le protocole** : le serveur MCP de TaskForce expose le dossier d'une mission et l'état d'un
    accord, en lecture ; le plugin Claude Code reçoit un hook, pour qu'une session ouverte par lui soit jugée et gardée
    comme une mission. `[HYPOTHÈSE]` À instruire dans le brouillon d'ADR-029.
  - **Quand** : rien de cela n'entre dans J2, qui ne prend que W0 à W5. E32 se fait maintenant, sur le code, sans code du
    produit ; la construction vient après le client test.
- **L'attaque de la contradictrice** : trois entreprises décideront de ce que la couche peut lire et écrire ; et un dossier
  qui pointe vers une issue de Linear ne prouve plus rien le jour où Linear la change.
- **Premier tour** : 18 oui, 4 non (Jobs : une couche tierce dégrade la qualité ; Musk : supprimer, pas geler ; Hamilton :
  une ancre hors de notre contrôle n'a pas de contrat ; Vestager), 2 abstentions (Saarinen, par conflit d'intérêts ; Duflo :
  aucune mesure). 75,0 %.
- **Amendements** :
  - le dossier garde une copie de la demande telle qu'elle était au départ, quelle que soit sa source : la preuve ne dépend
    jamais de l'outil d'origine (Hamilton, Vestager) ;
  - chaque source a un contrat écrit : ce qui est lu, ce qui est écrit en retour, ce qui se passe quand la source change ou
    disparaît (Hamilton) ;
  - jamais une seule source : deux prouvées de bout en bout avant de dire « on s'intègre », et l'issue interne reste la
    troisième, celle que personne ne peut fermer (Vestager) ;
  - le gel a une fin : au retour du client test, chaque surface gelée est supprimée ou reprise (Musk) ;
  - E32 avant toute ligne de code (Duflo).
- **Second tour** : 22 oui, 1 non (Jobs, maintenu : quoi qu'on possède, l'expérience se joue chez l'hôte), 1 abstention
  (Saarinen). 91,7 %.
- **Preuve en dix jours** : E32 faite ; le brouillon d'ADR-029 relu par la Présidence.
- **Signal d'arrêt** : E32 trouve un besoin de la preuve que seul le Board porte (une colonne, un cycle). Le Board ne gèle
  alors pas sur ce point.

### R200. Le vrai workflow : un processus versionné, lu sur une page, entré par l'issue et la conversation

- **Quoi** :
  - **Ce qu'est un vrai workflow pour une entreprise régulée** : un processus écrit d'avance et versionné ; des étapes dans un
    ordre ; pour chacune, qui la fait (une personne, un agent), qui la signe, quelle preuve elle doit laisser ; des points de
    pause qu'on ne saute pas ; et, pour chaque exécution, ce qui a été suivi, ce qui manque, ce qui a dévié et pourquoi.
    C'est ce que W2 a posé en base (le modèle, son vérificateur, les versions immuables, les points de pause verrouillés), et
    ce que W3 à W5 doivent rendre vivant et visible.
  - **La vue Workflow d'aujourd'hui (W1)** est ce que la Présidence en dit : le Board en cartes. Sans moteur, ses étapes sont
    les colonnes. Elle gèle (R202).
  - **Par où il entre** : par l'issue (un volet « Workflow » qui déroule le processus de cette issue, étape par étape, avec
    sa preuve et ses accords) et par la conversation (« où en est-on ? », comme la Présidence l'a fait à l'étape s06). Pas
    par un second tableau.
  - **Les liens** : le calque « Show all links » s'arrête. Les dépendances se lisent dans l'issue et dans l'étape, en liens
    cliquables, comme la Présidence le demande à l'étape s12.
  - **Les règles** : un seul endroit, qui dit les règles de l'espace puis celles du projet (étape s10).
  - **Le dessin** revient à l'équipe de Jobs, si la Présidence le lui délègue, sans symbole de BPMN (R166).
- **L'attaque de la contradictrice** : W3, W4 et W5 sont promis depuis le 13/11 ; redire ce qu'ils doivent être ne les
  construit pas, et une page de plus est une surface de plus.
- **Réponse** (Jobs, Norman) : la page remplace la vue en cartes, elle ne s'y ajoute pas ; et un écrit d'une page avant W5
  évite de livrer un troisième Board.
- **Vote** : 23 oui, 1 abstention (Shotwell : chaque précision sur W5 est une promesse de plus avant le client test). 95,8 %.
- **Preuve en dix jours** : le déroulé du processus d'E20 décrit en une page (les étapes, qui signe, la preuve attendue, ce
  que l'écran dit à chaque état), relu par la Présidence avant que W5 ne commence.
- **Signal d'arrêt** : W5 livré, la Présidence dit encore « on dirait pas des workflow ». La vue en cartes est alors
  supprimée, et le workflow ne se lit plus que dans l'issue et la conversation.

### R201. Cortex proactif sous des règles : chercher, demander, agir, dire vrai (second tour)

- **Quoi** : quatre verbes, dans cet ordre.
  - **Chercher** : quand la demande nomme un outil connecté ou un geste, Cortex reçoit les outils qui le permettent. Le choix
    des outils montrés au modèle ne dépend plus de mots anglais dans le message : tous les outils du connecteur nommé, et
    une recherche d'outil que le code exécute. Si l'outil n'est pas connecté, Cortex le dit et propose la connexion ; s'il
    est connecté en lecture seule, il propose l'écriture. Jamais « je ne peux pas » quand un chemin existe.
  - **Demander** : une lecture s'exécute. Une écriture montre une carte, une seule par demande : l'action exacte, l'endroit
    (« dans Linear, espace X », « dans TaskForce »), l'effet. Avant d'écrire, Cortex dit où il va écrire.
  - **Agir** : après l'accord, l'action exécutée est celle de la carte, et aucune autre.
  - **Dire vrai** : TaskForce dit ce qui a été fait, y compris au tour suivant. Les actions faites reviennent au modèle avec
    l'historique ; une phrase qui nie une action faite est corrigée comme l'est déjà une phrase qui annonce une action non
    faite (R116).
- **L'attaque de la contradictrice** : un agent qui propose lui-même d'élargir ses accès habitue la personne à dire oui.
- **Premier tour** : 19 oui, 3 non (Harris : la fatigue de l'accord ; Bengio : un périmètre qui s'élargit de lui-même ;
  Vestager), 2 abstentions (Norman, Harari). 79,2 %.
- **Amendements** :
  - proactif ne veut jamais dire s'accorder un droit : Cortex propose, une personne accorde, et la lecture reste le défaut
    (Bengio) ;
  - la recherche d'outil est du code déterministe, pas une initiative du modèle (Bengio) ;
  - un accord refusé n'est jamais redemandé dans la même conversation sans que la personne le rouvre (Harris) ;
  - la carte dit ce que Cortex a compris du but, pas seulement le geste (Norman) ;
  - la correction d'une phrase fausse se voit, signée par TaskForce, jamais en silence (Harari).
- **Second tour** : 23 oui, 1 abstention (Harris, maintenu : une carte par demande reste une carte de trop quand elles
  s'enchaînent). 95,8 %.
- **Preuve en dix jours** : E31, vingt demandes en français vers des outils connectés, avant et après les correctifs.
- **Signal d'arrêt** : un droit que Cortex obtient sans carte, ou un accord refusé relancé. La proactivité revient alors à
  la simple réponse « voici comment faire ».

### R202. L'inventaire : finir, garder, geler, arrêter (second tour)

- **Quoi** : la règle de tri est une seule phrase. Une surface avance si elle produit de la preuve, la montre, ou amène le
  travail jusqu'à elle. Sinon elle gèle. Si elle contredit la preuve ou la loi, elle s'arrête.
  - **Finir** veut dire : du travail dans J2. **Garder** : en l'état, corrigée si elle casse. **Geler** : visible, sans un
    jour de travail de plus, jusqu'au retour du client test. **Arrêter** : masquée maintenant, supprimée après le client
    test (une porte à double sens d'abord).

  | Surface | Sort | Pourquoi |
  | --- | --- | --- |
  | Le dossier d'une mission, son export, son vérificateur | Finir | C'est la place (R198) ; à moitié fait |
  | Les règles, le socle, les couches | Finir | Présent ; la couche des processus n'atteint pas encore une mission |
  | Les accords | Finir | La raison facultative, l'action exacte partielle |
  | La conversation avec Cortex | Finir | L'entrée réelle ; les correctifs (R204), puis R201 |
  | Les processus et le moteur (W3 à W5) | Finir | Le « workflow réglementé » que la saisine demande ; pour le seul processus d'E20 |
  | La mission, la remise, les changements | Garder | Présents, en production |
  | Le runner | Garder | L'isolement après J2 (ADR-028) |
  | L'issue et son volet | Garder | L'ancre du dossier |
  | Une liste simple du travail et de ce qui attend (My work, « Waiting for you ») | Garder | La vue lisible par tous (Ait Si Abbou) |
  | L'app desktop | Garder | Le banc d'essai (R91) ; la réponse au « chez soi » |
  | La banque d'évaluations, le banc des modèles | Garder | La mesure ; les étendre aux missions attend |
  | Le Brain OS, côté recherche | Garder | Lu par Cortex et par les agents |
  | La voix | Garder | Finie, sur la machine, aucun coût d'entretien relevé |
  | Le rangement des fichiers, les comptes, le RGPD, l'audit | Garder | Nécessaires, finis |
  | Le serveur MCP de TaskForce | Garder, puis finir après J2 | Il n'expose pas encore la preuve (R199) |
  | Le plugin Claude Code | Garder, puis finir après J2 | Aucun hook (R199) |
  | Les connexions menées au bout : Linear, GitHub, Notion, Slack, et celles que la recette a connectées | Garder | Ce sont elles qui portent « s'intégrer » |
  | Le site, la référence d'API | Garder | Le site se réécrit sur R196 quand la table de R197 le permet |
  | Le Board, List, Backlog | Geler | Aucun lien avec la preuve (pièce 3) |
  | Cycles, Roadmap et son Gantt, Teams | Geler | La gestion de projet que l'entreprise a déjà ailleurs |
  | Dashboard, Analytics, les analyses de fond | Geler | Des indicateurs de gestion, pas de preuve |
  | Members : compétences, congés, redistribution ; le suivi du temps | Geler | Idem ; et des données sur des personnes |
  | La vue Workflow en cartes (W1) | Geler | Un second Board, jusqu'à ce que les processus la remplacent (R200) |
  | Les 97 préréglages que personne n'a connectés (104, moins les 7 de la recette) | Geler | Ils restent listés avec leur état vrai, « pas encore essayé » ; aucun nouveau préréglage |
  | L'import et l'export BPMN, l'aller-retour avec Camunda | Geler | W8, après J2 (Q18) |
  | L'app web hébergée | Geler | Elle reçoit les releases, on n'y teste rien (R91) ; l'hébergement de la prod reste à choisir |
  | Les natives Plane et l'historique Slack versé au Brain OS | Geler | Sans lien avec la preuve |
  | Les webhooks sortants, le transfert web vers desktop | Geler | Finis, sans usage relevé |
  | Smart Assign | Arrêter | Il note des personnes ; la ligne de la loi (R192, décision du 16/11) ; rien de la preuve |
  | Le calque « Show all links » | Arrêter | La Présidence, étape s12 : « On peut virer les liens » |
  | L'agent GitHub Copilot | Arrêter | Il n'ouvre aucun dossier : un agent sans preuve contredit le produit |
  | L'objectif « remplacer Linear, Jira, Asana » | Arrêter | R196 |
  | Les mots « souverain » et « conforme » | Arrêter | R196, R187 |

- **L'attaque de la contradictrice** : geler vingt surfaces, c'est en garder vingt à migrer, à sécuriser et à expliquer à un
  auditeur fournisseur ; et le Board est la seule source de travail que personne ne peut fermer.
- **Premier tour** : 19 oui, 3 non (Musk : supprimer, pas geler ; Ait Si Abbou : le gel retire la vue du non-ingénieur ;
  Vestager), 2 abstentions (Saarinen, par conflit d'intérêts ; Norman). 79,2 %.
- **Amendements** :
  - une liste simple du travail et de ce qui attend sort du gel (Ait Si Abbou, Norman) ;
  - le gel a une date de fin, le retour du client test : chaque surface gelée y est supprimée ou reprise, aucune ne reste
    gelée (Musk) ;
  - l'issue interne reste une source de travail à part entière (Vestager) ;
  - une faille de sécurité dans une surface gelée se corrige : geler n'est pas abandonner (Bengio).
- **Second tour** : 22 oui, 1 non (Ait Si Abbou, maintenu : sans tableau, la personne de la qualité ne lit plus le projet),
  1 abstention (Saarinen). 91,7 %.
- **Preuve en dix jours** : la table relue et tranchée par la Présidence, ligne par ligne ; les surfaces arrêtées masquées
  dans l'app, sans suppression de code ni de données.
- **Signal d'arrêt** : une surface gelée qui reçoit un jour de travail hors d'un correctif de sécurité. La liste se relit.

### R203. Ce que cela change : J2, E20, le client test, la niche, le pitch, la recette

- **Quoi** :
  - **J2**, dans cet ordre : les correctifs de la recette (R204) ; TF-J2-7, le dossier (R198) ; puis W3, W4 et W5, pour le
    seul processus d'E20. C'est l'ordre déjà écrit dans la roadmap, les correctifs en tête. Rien ne s'ajoute : ni la source
    de travail externe, ni le hook du plugin, ni l'isolement, qui viennent après.
  - **Les autres lots de J2** se relisent à la règle de R202 : TF-J2-12 n'ajoute plus de préréglage et finit ceux qui
    comptent ; TF-J2-6, « la vue du travail », devient le volet de R200.
  - **E20** : inchangé, à la fin de J2. **Le premier client test** : inchangé, il passe d'abord, quand l'app est livrée et
    tient de gros volumes de données.
  - **La niche (R181)** : elle tient, et le dossier la renforce sur un point (la demande qui paie vient des audits en place)
    et l'affaiblit sur un autre (aucun exemple d'une personne seule qui vende au régulé). La précision de la Présidence
    tient : TaskForce ne livre aucun contenu réglementaire.
  - **Les objectifs (R183)** : ses dates ne courent toujours pas. Ses comptes se reliront avec les retours du client test.
  - **Le pitch** : la phrase de R196. Les trois preuves à montrer : une action refusée par une règle de l'entreprise ; un
    accord donné sur l'action exacte ; un dossier vérifié sans TaskForce.
  - **La prochaine recette** se joue sur le projet TaskForce lui-même, comme la Présidence le demande : son propre travail
    comme données, les réponses attendues écrites avant par le secrétariat, dix lignes au plus (E30).
  - **L'`Etude_business` du 27/02/2026** range l'hébergement souverain parmi les besoins des organisations de plus de 1 000
    personnes : à revoir, par une tâche, pas par une édition directe.
- **L'attaque de la contradictrice** : une recette sur son propre projet, avec ses propres réponses, mesure ce qu'on sait
  déjà.
- **Réponse** (Duflo, Gawande) : c'est son intérêt. Les réponses sont connues, donc une erreur de Cortex se voit ; ce qu'elle
  ne mesure pas, un projet inconnu, reste à E20.
- **Vote** : 23 oui, 1 abstention (Duflo : un essai sans témoin, à une personne). 95,8 %.
- **Preuve en dix jours** : E30 jouée par la Présidence sur l'app desktop, les réponses attendues écrites et datées avant.
- **Signal d'arrêt** : un lot de plus dans J2 avant le client test. Il sort.

### R204. Les correctifs de la recette : six, « dire vrai » d'abord, un cas par échec

- **Quoi** : le Conseil confirme les quatre correctifs proposés par le secrétariat, en ajoute deux, et les range. L'ordre
  suit R116 : dire vrai d'abord.
  1. **Cortex ne nie plus une action faite.** Les actions faites reviennent au modèle au tour suivant ; une phrase qui nie
     une action du même fil est corrigée, de façon visible. Cause établie (dossier, point 10).
  2. **Cortex dit où il écrit.** « Créer un projet dans Linear » a créé un projet dans TaskForce : la carte nomme la cible
     avant le geste. Ajouté par le Conseil.
  3. **Les outils d'écriture d'un connecteur nommé arrivent au modèle, en français comme en anglais.** Cause établie : la
     coupe à douze outils, triés sur des mots anglais.
  4. **L'issue jointe est prise en compte.** « Cette tâche » désigne l'issue jointe ; elle reste dans le fil au tour
     suivant. Cause à confirmer sur le cas rejoué.
  5. **Une connexion qui échoue dit pourquoi, et quoi faire.** L'éditeur refuse l'inscription, ou il faut une application
     que seule la Présidence peut enregistrer : le message le dit. Cause établie.
  6. **Une vue vide dit qu'elle est vide.** « Show all links » sans lien dit « aucun lien » ; le calque s'arrête ensuite
     (R202). Ajouté par le Conseil ; cause à vérifier.
  - Chaque défaut entre à la banque d'évaluations comme un cas, avant sa correction (R118) : la conversation de l'étape s17
    en donne cinq.
  - Hors de ces six, rien de la recette ne se corrige maintenant : les logos, la page de retour, le focus, la lecture
    Detail attendent le sort de leur surface (R202).
  - **Les applications à enregistrer chez les éditeurs** (Google, Microsoft, Dropbox et les autres) ne sont pas un
    correctif : seule la Présidence peut les faire, et la liste se réduit à ce que R202 garde.
- **L'attaque de la contradictrice** : corriger six défauts d'un modèle de 9 milliards de paramètres ne rend pas l'agent
  fiable ; le septième apparaîtra à la prochaine recette.
- **Réponse** (Gawande, Harari, Li) : cinq des six sont des défauts du code, pas du modèle ; et c'est pour le septième que
  chaque échec devient un cas.
- **Vote** : 24 oui. 100 %. L'unanimité a été précédée de l'attaque de la contradictrice (charte, §7.5).
- **Preuve en dix jours** : les six corrigés en mode développement, chacun avec son cas à la banque, rejoués par la
  Présidence sur l'app desktop.
- **Signal d'arrêt** : un correctif livré sans son cas. Il n'est pas compté comme fait.

### Les votes en une table

| R | Recommandation | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R196 | Ce que TaskForce est, et pour qui | 22 | Musk | Nadella | 91,7 % (19 au premier tour) |
| R197 | Les besoins, la table de correspondance | 23 | | Musk | 95,8 % |
| R198 | La preuve d'abord | 23 | | Bezos | 95,8 % |
| R199 | Une couche ; l'issue reste, le Board gèle | 22 | Jobs | Saarinen | 91,7 % (18 au premier tour) |
| R200 | Le vrai workflow | 23 | | Shotwell | 95,8 % |
| R201 | Cortex proactif sous des règles | 23 | | Harris | 95,8 % (19 au premier tour) |
| R202 | L'inventaire | 22 | Ait Si Abbou | Saarinen | 91,7 % (19 au premier tour) |
| R203 | Ce que cela change | 23 | | Duflo | 95,8 % |
| R204 | Les correctifs de la recette | 24 | | | 100 % |

### Questions à la Présidence

Chacune avec ses options et l'avis de la majorité, pour une réponse d'une ligne.

1. **La phrase** (R196). A : la retenir telle quelle. B : l'élargir à toute équipe qui se sert d'agents, sans l'audit. C : la
   resserrer sur le régulé seul. *Avis de la majorité : A (22).*
2. **Le Board** (R199, R202). A : le garder et continuer d'y travailler. B : le geler, l'issue restant l'ancre, et décider de
   sa suppression au retour du client test. C : le supprimer maintenant. *Avis : B (22). Musk et Jobs penchent pour C, Ait
   Si Abbou pour A.*
3. **La source de travail externe** (R199). A : dans J2, avant E20. B : après le client test, E32 se faisant maintenant sur
   le code. Et par quelles deux sources commencer : GitHub et Linear, ou Jira ? *Avis : B, puis GitHub et Linear, les deux
   que la Présidence a connectées.*
4. **La vue Workflow** (R200). A : garder les cartes et les améliorer. B : les geler, arrêter le calque des liens, et faire
   du workflow le déroulé d'un processus dans l'issue et la conversation, avec W3 à W5. C : retirer l'onglet jusqu'à W5.
   Et : le dessin est-il délégué à l'équipe de Jobs, comme aux séances n°18 à n°20 ? *Avis : B (23), et oui.*
5. **Cortex** (R201). A : relever seulement le nombre d'outils. B : tous les outils du connecteur nommé, plus une recherche
   d'outil par le code ; une carte par écriture, jamais de relance d'un refus. *Avis : B (23).*
6. **Ce qu'on arrête** (R202), un oui ou un non par ligne : masquer Smart Assign en entier, au-delà du critère retiré le
   16/11 ; masquer l'agent Copilot tant qu'il n'ouvre pas de dossier ; retirer « Show all links » ; laisser les 97
   préréglages non connectés visibles avec la mention « pas encore essayé », ou ne montrer que ceux qui marchent (R99). *Avis : oui, oui,
   oui, et la mention plutôt que le retrait.*
7. **Les dix jours** (R203, R204) : les six correctifs, puis TF-J2-7, puis W3 ; la table de R197 et E30 au labo. Oui ou non ?
   *Avis : oui (23).*
8. **La prochaine recette** (R203, E30) : sur un projet « TaskForce » créé dans l'app à partir de la roadmap publique, ou
   sur les issues du dépôt public lues par le connecteur GitHub ? *Avis : le premier maintenant ; le second quand la source
   externe existera.*
9. **Les mots** (R196) : renonce-t-elle à « souverain » en public, pour « installé chez vous, le modèle que vous
   choisissez » ? *Avis : oui (23).*
10. **Le juriste** (Q28) : le CRA et la licence (l'AGPL seule, ou l'AGPL avec une licence commerciale pour les acheteurs qui
    l'interdisent) demandent une lecture qualifiée. Avant toute édition payante, ou dès maintenant ? *Avis : avant toute
    édition payante ; rien ne presse tant que TaskForce est gratuit.*

## Décision de la Présidence

Tranchée en trois temps, en conversation : le 17/11/2026 après cette séance, le 17/11/2026 après la séance n°29, puis le
22/11/2026 après la séance n°30.

1. **Le 17/11/2026, après cette séance.** La Présidence répond aux neuf recommandations. Une seule ligne tranche, mot pour mot
   : « R204: Ok ». Le reste de ce message demande des précisions : c'est la saisine de la [séance
   n°29](./2026-11-17-preciser-avant-de-trancher.md), consignée à son PV.
2. **Le 17/11/2026, après la n°29.** Deux lignes tranchent, mot pour mot : « R202: ok je comprends oui on s'engage pas, on
   fourni juste le necessaire pour augmenter la confiance » et « R200: ok ». Le reste de ce message est la saisine de la
   [séance n°30](./2026-11-17-finir-la-v1.md), consignée à son PV.
3. **Le 22/11/2026, après la n°30.** Le secrétariat avait remonté à la Présidence les dix-huit points à trancher de la n°30,
   chacun avec l'avis de la majorité, et recommandé de suivre la majorité partout. La Présidence répond, mot pour mot :

> « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est partie »

**La Présidence délègue.** Les dix-huit points de la n°30 sont tranchés selon l'avis de la majorité du Conseil, tel que le PV
n°30 l'écrit (« La liste à trancher pour finir la v1 »). Ce qui suit, quand il ne porte pas une citation du 17/11, est
**retenu par délégation de la Présidence au Conseil, selon l'avis de sa majorité**. Sa raison est la délégation : le
secrétariat ne lui en prête aucune autre (charte, §2.4).

Dans ce qui suit, **la décision** est ce que la Présidence a dit, ou ce que la majorité a écrit au PV et que la délégation
retient. Les **précisions du secrétariat** sont à part : ce ne sont pas ses mots.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R196 | Remplacée par R205 (n°29) | La délégation du 22/11/2026 |
| R197 | Retenue, dans sa version précisée par la n°29 | La délégation du 22/11/2026 |
| R198 | Retenue, dans sa version précisée par la n°29 | La délégation du 22/11/2026 |
| R199 | Retenue, dans sa version précisée par la n°29 | La délégation du 22/11/2026 |
| R200 | Retenue le 17/11/2026, dans sa version précisée par la n°29 | « R200: ok » |
| R201 | Retenue, dans sa version précisée par la n°29 | La délégation du 22/11/2026 |
| R202 | Retenue le 17/11/2026, dans sa version précisée par la n°29 | « R202: ok je comprends oui on s'engage pas, on fourni juste le necessaire pour augmenter la confiance » |
| R203 | Retenue, dans sa version précisée par la n°29 | La délégation du 22/11/2026 |
| R204 | Retenue le 17/11/2026 ; faite | « R204: Ok » |

- **R196, remplacée par R205.** La phrase de cette séance n'est plus celle de TaskForce : la place est la place ajustée de
  R205 (n°30, point 1, option A). Sa décision est au [PV n°29](./2026-11-17-preciser-avant-de-trancher.md).
- **R197, retenue dans sa version précisée** (« R197, amendée », n°29) : la méthode en quatre temps, les cinq sources
  d'observation, la table de correspondance qui se montre aussi. Le point 18 de la n°30 en retient la suite : une seule
  question de fait, posée sans campagne.
- **R198, retenue dans sa version précisée** (« R198, amendée », n°29) : le dossier est le produit, la signature est le droit
  d'entrée ; la page du lecteur d'abord ; aucun format propre.
  - **La décision** (n°30, point 9, option B) : TF-J2-7 et la page de vérification, la page écrite d'abord, rien au commit ;
    l'empreinte de tête écrite dans la pull request quand il y en a une.
- **R199, retenue dans sa version précisée** (« R199, amendée », n°29) : une couche qui dit qui possède quel moment ; une
  source menée au bout d'abord.
  - **La décision** (n°30, points 2, 3 et 4) : le Board gèle, l'issue reste l'ancre, et le sort du Board se décide au point de
    décision, sur l'usage observé ; en v1, on ne demande ailleurs que depuis Claude Code, par le serveur MCP et le plugin qui
    existent ; la première vraie source externe vient après le client test, GitHub puis Linear ; le contrat d'une source de
    R209 est retenu.
  - **Précision du secrétariat** : le projet
    d'[ADR-029](../../decisions/ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md) est rangé, amendé par la n°29 et par
    R208 et R209. Il reste à relire par la Présidence.
- **R200, retenue le 17/11/2026** : « R200: ok ». Dans sa version précisée par la n°29 : un processus porte une
  réglementation, une convention ou une norme interne ; TaskForce donne le moteur et des exemples de conventions, jamais le
  contenu réglementaire.
  - **La décision du 22/11, par délégation** (n°30, point 5) : le dessin du processus est délégué à l'équipe de Jobs.
- **R201, retenue dans sa version précisée** (« R201, amendée », n°29) : trois classes décidées d'avance par une personne :
  part seul, attend une carte, refusé.
  - **La décision** (n°30, point 6, option B) : les trois classes ; hors de TaskForce, outil par outil, après la v1.
  - **Précision du secrétariat** : le projet d'[ADR-030](../../decisions/ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md) et
    E33 portent cette suite.
- **R202, retenue le 17/11/2026** : « R202: ok je comprends oui on s'engage pas, on fourni juste le necessaire pour augmenter
  la confiance ». Dans sa version précisée par la n°29 : l'inventaire inchangé ; les mots précisés ; la fin du gel décidée sur
  l'usage observé.
  - **La décision du 22/11, par délégation** (n°30, point 10) : dans la v1, Smart Assign est masqué, l'agent Copilot aussi
    tant qu'il n'ouvre pas de dossier, « Show all links » est retiré, et les 97 préréglages jamais connectés restent visibles
    avec la mention « pas encore essayé ».
  - **Précision du secrétariat** : R202 plaçait la fin du gel « au retour du client test ». Le point 2 de la n°30 la place au
    point de décision, trente jours après la remise de la v1 au premier client test.
- **R203, retenue dans sa version précisée** (« R203, amendée », n°29) : ce que cela change, plus un témoin dans E30 et le
  pitch sur R205.
  - **La décision** (n°30, points 17 et 18) : l'ordre des « dix jours » est remplacé par celui de la v1 (R217) et par ses dix
    critères (R218) ; la prochaine recette se joue sur le projet TaskForce, avec le modèle nu comme témoin (E30).
  - **Précision du secrétariat** : R203 disait que les dates de R183 ne courent pas. Le point 17 pose un butoir au point de
    décision, le 31/03/2027 ; ce qu'il change à la décision sur la séance n°26 est dit au [PV
    n°30](./2026-11-17-finir-la-v1.md).
- **R204, retenue le 17/11/2026 ; faite** : « R204: Ok ».
  - **Ce qui est fait** : les six correctifs sont dans la PR #548, fusionnée dans `dev` le 19/11/2026 (commit `9d95f88d`),
    après six tours de relecture indépendante. Ils ne sont pas encore en production.
  - **Précision du secrétariat** : la preuve de R204 demande chaque correctif rejoué par la Présidence sur l'app de bureau,
    avec son cas. C'est le critère 1 de la v1 (R218) ; le secrétariat ne le dit pas rempli.

**Les dix questions de cette séance** ne reçoivent pas de réponse ici : elles ont été remplacées par les quatorze questions de
la n°29, puis par les dix-huit points de la n°30, que la délégation tranche. Le détail de chaque point est au [PV
n°30](./2026-11-17-finir-la-v1.md).

| Question de cette séance | Ce qu'elle est devenue | Tranchée par |
| --- | --- | --- |
| 1. La phrase | n°29, question 1 ; n°30, point 1 | La délégation : la place ajustée de R205 |
| 2. Le Board | n°29, question 2 ; n°30, point 2 | La délégation : gelé, son sort au point de décision |
| 3. La source de travail externe | n°29, question 3 ; n°30, points 3 et 4 | La délégation : Claude Code seulement en v1 ; GitHub puis Linear après le client test |
| 4. La vue Workflow | n°29, question 4 ; n°30, point 5 | « R200: ok » ; le dessin par la délégation |
| 5. Cortex | n°29, question 5 ; n°30, points 6 et 7 | La délégation : les trois classes |
| 6. Ce qu'on arrête | n°29, question 6 ; n°30, point 10 | « R202: ok […] » pour le principe ; la délégation pour les quatre lignes |
| 7. Les dix jours | n°29, question 7 ; n°30, point 17 | La délégation : l'ordre de la v1 et ses dix critères |
| 8. La prochaine recette | n°29, question 8 ; n°30, point 18 | La délégation : sur le projet TaskForce, avec le modèle nu comme témoin |
| 9. Les mots | n°29, question 9 ; sortie de la liste à la n°30 | Le secrétariat la lit comme tranchée par « R202: ok je comprends oui on s'engage pas » |
| 10. Le juriste | n°29, question 10 ; n°30, point 13 | La délégation : la licence commerciale et le prix avant toute annonce large ; le juriste avant l'édition payante |

## Notes du secrétariat

- **Le dossier** : le code de `dev` (`067c577b`) lu dans sa copie, la recette de la 1.17.0 et `taskforce-docs` (`34af22b`).
  Les faits de marché et de réglementation viennent des trois recherches du 17/11/2026, faites sur des pages publiques
  seulement, sans connexion ni formulaire.
- **Les limites des trois recherches**, telles que leurs auteurs les signalent :
  - D1 : le règlement 2026/1744 (l'Omnibus) n'a pas pu être relu sur EUR-Lex, ses dates reposent sur des sources
    secondaires concordantes ; le résultat du vote de l'Assemblée sur NIS2 prévu le 17/11/2026 n'a pas été lu ; la lecture
    des lignes directrices du CRA sur le logiciel libre repose sur un seul commentaire.
  - D2 : les pages de Gartner et de McKinsey n'ont pas pu être rouvertes, leurs chiffres viennent de l'outil de recherche
    ou de la presse ; les faits sur Google, Salesforce, ServiceNow, Codex, Devin et GitHub Universe 2026 sont
    `[À VÉRIFIER]` ; les montants des rachats sont des montants de presse.
  - D3 : le chiffre de Capgemini est lu dans une reprise ; les chiffres de Gartner viennent de reprises ; aucune enquête ne
    chiffre la demande de gouvernance d'agents sur site ; aucun exemple public solide d'une personne seule qui vend cela à
    des entreprises régulées.
- **Ce que le secrétariat a relu lui-même, le 17/11/2026** :
  - à la source, trois pages : le brouillon de l'IETF (version 09, 26/10/2026, « not endorsed by the IETF », chaînage
    SHA-256 selon la RFC 8785, signatures en option) ; l'annonce de la boîte à outils de Microsoft (MIT, YAML, Rego ou
    Cedar, rien sur des journaux signés, des cibles Azure seulement) ; le billet d'IDC (la phrase citée, 60 % et 35 %) ;
  - le guide de l'ANSSI n'a pas pu être relu : le PDF ne s'est pas laissé lire par l'outil. Ses sept principes sont ceux
    que D2 rapporte, PDF lu par son auteur ;
  - dans le code : la chaîne (`EvidenceChain.java`), l'absence de toute signature, la clé étrangère obligatoire de
    `delivery_runs` vers `issues`, `relevantExternal` et sa limite de 12, les 104 préréglages, la commande de vérification
    du runner, `ActionClaimCheck` et l'historique en textes seuls, les huit onglets d'un projet. Le reste de l'inventaire et
    de la pièce 2 vient de deux lectures du code faites ce jour par des agents de recherche, chemins et lignes à l'appui.
  - Aucun `[À VÉRIFIER]` n'a été promu.
- **Les fiches** : aucune rafraîchie, aucune n'ayant plus de 30 jours au 17/11/2026 (charte, §9). Vingt passeront ce seuil le
  21/11/2026.
- **Corrections du brief et du relevé de recette** :
  - « Cortex qui nie son action » était une `[HYPOTHÈSE]` du relevé : le code la confirme, et ajoute que le contrôle des
    annonces laisse passer une phrase qui nie ;
  - « l'issue jointe ignorée » : l'issue est bien passée au modèle, dans le prompt système ; ce qui manque est établi pour
    le tour suivant (elle n'est pas gardée), pas pour le tour même ;
  - « Show all links » (s09) reste une `[HYPOTHÈSE]` : la copie ne contient pas le projet de la recette ;
  - « le board sert a rien techniquement » : vrai du tableau, faux de l'issue, à laquelle chaque mission est attachée par
    une clé obligatoire (pièce 3).
- **Corrections des documents** :
  - le `README.md` du dépôt annonce « 97 migrations » : la copie en compte 128, jusqu'à V133 ;
  - la déduction de la séance n°24, point 9 (« aucun voisin ne revendique des règles écrites en mots au-dessus d'un socle
    déterministe »), est à nuancer depuis Policy d'AgentCore ; l'autre moitié, une preuve vérifiable hors de l'outil, tient ;
  - `[À VÉRIFIER]` le `README.md` du plugin annonce `smart_assign` et `ask_cortex` ; à la lecture du code, la table de
    règles par défaut les refuserait à un client extérieur. Non exécuté ;
  - `v1/01-projet/Etude_business.md` (27/02/2026) : l'hébergement souverain rangé chez les organisations de plus de 1 000
    personnes est à revoir (R203).
- **Conflits d'intérêts** :
  - Saarinen : Linear est l'outil que la saisine parle de ne plus remplacer. Il s'est abstenu sur R199 et R202 ;
  - Nadella : Microsoft vend Agent 365, donne la boîte à outils du dossier et possède GitHub. Il s'est abstenu sur R196 ;
  - Bezos : AWS vend AgentCore et sa Policy ; Kiro est l'agent d'Amazon. Il l'a déclaré et a voté ;
  - Zhuo (Meta) : le sujet du jour ne le réveille pas.
- **Hors fiche, hors champ** :
  - Vestager parle du CRA, de l'AI Act et de MCP : sa fiche ne porte aucune déclaration récente sur ces textes ; elle parle
    depuis sa grille, les faits viennent du dossier ;
  - Azoulay transpose l'article 26 de l'AI Act et la note de la CNIL, hors des recommandations de l'UNESCO que sa fiche
    documente ;
  - Mazzucato, hors champ sur les rachats d'entreprises de sécurité ;
  - Doudna, Gawande, Duflo et Li transposent leur méthode (paliers, listes, essais, mesure) à un marché de logiciel ;
  - Rus, hors champ sur la presse pharmaceutique ;
  - Jobs, hors de son champ sur MCP et sur la conformité ;
  - Ait Si Abbou maintient un non sur R202 : c'est dans sa fiche (la décision lisible par un non-ingénieur), pas un écart.
- **Anachronismes** : Jobs et Hamilton ne connaissent les agents, MCP, Linear et les textes de 2024 à 2026 que par le
  dossier.
- **Sources manquantes** :
  - aucune enquête sur les entreprises européennes de 10 à 250 personnes ;
  - aucun chiffre sur la demande de gouvernance d'agents sur site ;
  - le résultat du vote sur NIS2 ;
  - rien de daté de 2026 sur IONOS ni sur les offres propres de Google hors S3NS ;
  - la coque de l'app desktop, les tests et le seed ne sont pas dans la copie du code : l'inventaire ne les compte pas.
- **Garde-fous** : aucun nom de client ; le premier client test reste « le premier client test ». Deux éléments privés de la
  recette (le nom d'un espace Linear, une adresse locale) sont restés hors du PV.

## Suites

- Le PV dans `seances/`, une ligne au registre de la charte (§12) et le récit au Journal.
- À `Questions-ouvertes.md` : Q27 (la demande d'une preuve sur site existe-t-elle chez les 10 à 250 personnes ?), Q28 (le CRA
  et la licence : libre non monétisé, ou édition payante ; l'AGPL seule, ou avec une licence commerciale), Q29 (le format du
  dossier : s'aligner sur la RFC 8785 et le brouillon de l'IETF, ou garder le sien), Q30 (le sort des surfaces gelées, et
  quand le décider).
- Si la Présidence les retient, à `experiences/Experiences.md` : E30 (la recette sur le projet TaskForce, réponses écrites
  avant), E31 (Cortex en français, vingt demandes vers des outils connectés), E32 (ce qui dépend de l'issue interne, tracé
  sur le code). Aucune n'est inscrite avant sa décision.
- Si R199 est retenue : le brouillon d'ADR-029 (la couche, le travail vient d'où il est), à relire par la Présidence.
- En mode développement, après la décision : les six correctifs (R204), chacun avec son cas ; TF-J2-7 (R198) ; les surfaces
  arrêtées masquées (R202).
- Au labo, sans rien prendre à J2 : la table de correspondance (R197) ; le déroulé d'un processus en une page (R200) ; E32.
- À la roadmap, par une tâche : `Etude_business` à revoir ; le `README.md` du dépôt (le nombre de migrations) ; le
  `README.md` du plugin, après vérification.
- Après la décision de la Présidence, rangé le 22/11/2026 :
  - au registre de la charte (§12) et au Journal : « la Présidence délègue au Conseil et tranche les séances n°28 à n°30 » ;
  - à `Questions-ouvertes.md` : Q27 à Q30 mises à jour, chacune avec son statut daté ;
  - à `experiences/Experiences.md` : E30, E31 et E32 entrent, retenues, E30 amendée par la n°29 (le modèle nu comme témoin) ;
  - le projet d'[ADR-029](../../decisions/ADR-029-DRAFT-la-couche-le-travail-vient-d-ou-il-est.md), amendé par la n°29 (R199)
    et par la n°30 (R208, R209) ;
  - à la roadmap, le bloc du 22/11/2026, « La v1, tranchée par délégation » ; au [plan des
    lots](./2026-11-13-le-workflow-pilotable-plan-des-lots.md) de la séance n°25, une note sur chaque lot touché.
- Restent, après ce rangement :
  - en mode développement : la mise en production de la PR #548 ; TF-J2-7 ; les surfaces arrêtées masquées (R202) ;
  - à la Présidence : rejouer les six correctifs sur l'app de bureau (R204) ; relire le projet d'ADR-029 ;
  - à la roadmap, par une tâche : `Etude_business` à revoir ; le `README.md` du dépôt ; le `README.md` du plugin, après
    vérification.
- Rien ne migre vers `v1/` sans tâche ni ADR (quarantaine, [`CLAUDE.md`](../../CLAUDE.md) §2).

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
