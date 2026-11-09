---
id: roadmap-backlog
title: Backlog & Roadmap Technique (exhaustif)
doc_type: register
statut: active
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [technique, backlog, roadmap, todo, rncp, securite, tests]
related:
  - "../../Brain_OS.md"
  - "../09-audits/Problemes_Connus.md"
  - "../16-memoire-rncp/README.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Backlog & Roadmap Technique

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

> **▶ 01/11/2026 :** le chantier en cours est la feuille de route jusqu'à la démo complète, J0 à J9, décidée par la
> Présidence après les séances n°14 et n°15 du Conseil ([PV](../../recherche/conseil/seances/2026-11-01-feuille-de-route.md)).
> Elle est au [§0](#0-la-feuille-de-route-jusquà-la-démo-complète-j0-à-j9) ; chaque jalon se valide avant le suivant.
> Date butoir hors jalons : les machines de l'école s'arrêtent le 31/12/2026 (Présidence, 01/11) ; le VPS d'OVH doit
> porter avant cette date les comptes, la webapp, l'API et les sauvegardes, puisque l'app desktop se connecte par la
> webapp ([Q13](../../recherche/Questions-ouvertes.md)).
>
> **▶ 14/10/2026 :** le chantier en cours est la release open source de TaskForce 1.0, suivie item par item dans
> [[Plan_Release_Open_Source]] (ADR-014 à ADR-020). Ce backlog reste la référence historique de la v1.

[![Type: Registre](https://img.shields.io/badge/Type-Registre-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Couverture: RNCP + Pro](https://img.shields.io/badge/Couverture-RNCP%20%2B%20Ultra%20Pro-purple?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Problèmes connus](../09-audits/Problemes_Connus.md) · [Dette technique](../09-audits/Dette_Technique.md)
- [Mémoire — matrice des compétences](../16-memoire-rncp/README.md)

**Tags :** `#technique` `#backlog` `#roadmap` `#todo` `#rncp`

<p class="lead">
Liste <strong>exhaustive</strong> de tout ce qui reste à faire pour mener TaskForce au niveau « ultra
pro » : landing, frontend, backend, infrastructure, plus les chantiers transverses (tests, sécurité,
conventions, RGPD, documentation, SEO). Chaque tâche est mappée à une compétence RNCP (le référentiel est
le <strong>socle minimal</strong> ; les items marqués ★ vont au-delà). À piloter comme un tableau Kanban
(plugin Obsidian Kanban recommandé).
</p>

> **Légende** — Priorité : 🔴 P0 (bloquant) · 🟠 P1 · 🟡 P2 · 🟢 P3 (nice-to-have). Effort : S ≤½j ·
> M ½–2j · L 3–5j · XL >1 sem. Statut : ⬜ à faire · 🔄 en cours · ✅ fait. ★ = au-delà du référentiel.

## Table des matières

0. [La feuille de route jusqu'à la démo complète (J0 à J9)](#0-la-feuille-de-route-jusquà-la-démo-complète-j0-à-j9)
1. [P0 — Correctifs bloquants](#1-p0--correctifs-bloquants)
2. [Frontend](#2-frontend)
3. [Backend](#3-backend)
4. [Landing page](#4-landing-page)
5. [Infrastructure & DevOps](#5-infrastructure--devops)
6. [Tests & qualité](#6-tests--qualité)
7. [Sécurité](#7-sécurité)
8. [RGPD & légal](#8-rgpd--légal)
9. [Conventions & process](#9-conventions--process)
10. [Documentation](#10-documentation)
11. [Synthèse de couverture RNCP](#11-synthèse-de-couverture-rncp)

---

## 0. La feuille de route jusqu'à la démo complète (J0 à J9)

Décidée le 01/11/2026 ([séance n°15](../../recherche/conseil/seances/2026-11-01-feuille-de-route.md), R90 à R106). Le
cap :
- l'infrastructure sur laquelle une entreprise fait travailler ses agents, sous ses règles, sur ses données, avec les
  modèles qu'elle choisit, en voyant et en prouvant tout ;
- les gens du métier construisent l'outil (ADR-022) ;
- la confiance est l'indicateur premier (R104).

Le banc d'essai est l'app desktop, avec Claude Code et Ollama. La webapp reçoit chaque release, mais on n'y teste rien
pour l'instant (R91).

**Chaque jalon se valide de la même façon** (R105) :
1. les critères de sortie écrits avant ;
2. la boucle de démo rejouée de bout en bout ;
3. les tests verts ;
4. la [liste de lancement](../08-operations/Liste_de_lancement.md) (installation, mise à jour, sauvegarde et restauration) ;
5. trois personnes extérieures au moins, dès J2 ;
6. l'indice de confiance mesuré (E17) ;
7. une séance du Conseil, puis le go de la Présidence.

| ID | Tâche | Jalon | Statut | Réf |
| -- | ----- | :--: | :--: | --- |
| TF-J0-1 | La recherche du Brain OS respecte les droits des projets privés ; l'analyse d'un projet privé ne se lance ni ne se suit hors de ses membres (`taskforce-fullstack` #459, #460, fusionnées dans `dev` le 01/11) | J0 | ✅ | R82 |
| TF-J0-2 | « Apply » se désactive sur un échec de tests ; passer outre demande un geste explicite et une raison, gardée sur la mission et postée sur l'issue (#461, fusionnée dans `dev` le 01/11) | J0 | ✅ | R87 |
| TF-J0-3 | Un accord refusé faute de réponse le dit à la personne : déjà fait, la chronologie dit « No answer in time: refused » (#457) | J0 | ✅ | R87 |
| TF-J0-4 | Les pages qui disent vrai : la confidentialité de la webapp (Groq), les pages légales du site (l'hébergement réel), l'annonce de fermeture de la webapp ; l'architecture et le modèle de prix (faits le 01/11) ; le site et la webapp (#462, en prod avec la 1.7.0) ; reste l'ADR-010 et l'ADR-021 | J0 | 🔄 | R82 |
| TF-J0-5 | La release de R78 (Créer, Accorder, Relire) avec J0, sur « go release » : 1.7.0 en prod le 01/11 (#463), desktop 1.4.0 | J0 | ✅ | R78, R87 |
| TF-J0-6 | La porte : une demande de la table atteint toujours la personne, un accord vaut morceau par morceau, les lectures dans la copie ont leur règle ([séance n°16](../../recherche/conseil/seances/2026-11-01-revue-j0.md)) ; #467, en prod avec la 1.8.0 le 02/11 | J0 | ✅ | R107, R108 |
| TF-J0-7 | L'issue dit vrai et l'agent la tient à jour : la carte de Cortex complète, au plus une question, « Checklist » ; l'activité dit qui a fait quoi ; l'agent coche la checklist sous son nom, sur la seule issue confiée, et demande au-delà de 30 changements ; #471 et #472, en prod avec la 1.8.0 le 02/11 | J0 | ✅ | R110, R111 |
| TF-J0-8 | La revue UI/UX, et la réponse qui naît où l'on a écrit : la note [Revue_UX_2026-11-01](../14-design/Revue_UX_2026-11-01.md) et #469, en prod avec la 1.8.0 le 02/11 ; les constats en attente y sont listés | J0 | ✅ | R112 |
| TF-J1-1 | E16 : une source unique pour le moteur de règles (l'aller-retour mesuré, le moteur Java compilé en JavaScript) ; la Présidence tranche R90. E16 faite le 02/11 ; (b) adoptée le 02/11 (« on adopte R90 (b) », [ADR-025](../../recherche/decisions/ADR-025-DRAFT-un-seul-moteur-de-regles.md)) : le runner décide avec le moteur Java compilé en JavaScript, la copie TypeScript disparaît. #479 fusionnée dans `dev` le 02/11 (module `backend/rules-engine-js`, 84 cas verts, vérifié sous le Node d'Electron 44.8.0) ; en prod avec la 1.10.0 le 05/11 (#488) | J1 | ✅ | R90 |
| TF-J1-2 | En prod avec la 1.9.0 le 02/11 (#470) : le backend dit « AI gateway: OPENAI at api.groq.com », l'ai-service supprimé de VM1 ; reste un essai de l'API d'Anthropic avec une vraie clé, et une banque d'évaluations plus large que son cas unique. La passerelle de modèles ouverte : n'importe quel LLM ou modèle, en un seul endroit du backend ; l'ai-service Python et le relais de la coque cessent de servir. La passerelle Java joint Ollama, toute API compatible OpenAI et l'API d'Anthropic ; l'ai-service, son secret et le relais de la coque sont supprimés ; un serveur garde ses variables, l'app desktop change de fournisseur sans redémarrer (`taskforce-fullstack` #470, ouverte vers `dev`) | J1 | ✅ | R92 |
| TF-J1-3 | En prod avec la 1.8.0 le 02/11 (#468). Les préréglages de connecteurs jamais essayés quittent le catalogue visible ; le plan figé d'« AI Workflows » disparaît. Le catalogue ne montre à tous que Linear, le seul préréglage essayé de bout en bout ; un préréglage jamais essayé reste visible de l'espace qui l'a connecté. Le plan d'étapes des analyses est supprimé, du panneau à la base (V113) ; l'historique des délégations reste (`taskforce-fullstack` #468, ouverte vers `dev`) | J1 | ✅ | R99, R105 |
| TF-J1-4 | Ce que chaque modèle sait faire, mesuré par la banque d'évaluations sur la machine de la personne ; TaskForce propose le premier capable, la personne choisit ; R51 essayée sur la passerelle (cinq tâches en commentaire). Fait (`taskforce-fullstack` #485, en prod avec la 1.10.0 le 05/11 (#488)) : huit cas fixes de la banque par modèle (outils, contexte, code, français, anglais), la table et « Measure » dans Réglages > AI de la webapp et de l'app desktop, la proposition et « Use for Cortex » ; l'escalade de R118, proposée sous la réponse et envoyée d'un clic ; l'agent à l'essai de R51 pour les tâches sans dépôt. Mesuré le 04/11 sur le poste de la Présidence (Ollama, sept modèles) : outils 2/2 pour les cinq modèles d'instruction, contexte 1/2 pour tous (le contexte par défaut d'Ollama, 4 096 jetons), code 1/2 au mieux (qwen3:14b), français et anglais 1/1, les deux modèles de base sans outils ; R51 à 4 sur 5 avec qwen3:8b ([E11](../../recherche/experiences/Experiences.md)) ; en prod avec la 1.10.0 le 05/11 (#488), avec la fenêtre de contexte d'Ollama (#487) | J1 | ✅ | R113, R118, R51 |
| TF-J1-5 | Les premiers gestes du chat : modifier, déplacer et assigner une issue ; la confier à Claude Code ; répondre à une demande depuis la conversation, par le bouton de sa carte ; « Apply », « Discard », « Try again ». Chaque geste s'ajoute une fois, dans le MCP TaskForce, et sert à Cortex comme à tout agent, sous les mêmes règles ([ADR-024](../../recherche/decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md), Présidence, 02/11). Fait : `update_issue` (champs, colonne, assigné, labels, points, cycle, échéance), `add_comment`, `delegate_issue`, `get_mission` et, après le test de la Présidence, `delete_issue` (règle `delete-issue`, la carte propose d'archiver d'abord), jugés sur leur action ; Undo de ce qui se défait, demande de ce qui ne se défait pas ; les cartes de la mission dans la conversation, décidées par leurs boutons ; vérifié avec qwen3:8b sur la pile de dev (`taskforce-fullstack` #480, en prod avec la 1.10.0 le 05/11 (#488)) | J1 | ✅ | R95, R92, R99 |
| TF-J1-6 | La couverture du chat : l'inventaire de tous les gestes de l'app et la part que le chat sait faire (8 au 02/11), suivie à chaque jalon. [Couverture_du_chat](../02-produit/Couverture_du_chat.md) : 155 gestes par surface ; le chat en faisait 9 avec ses 8 outils, 31 avec #480 (20 %) (`taskforce-fullstack` #480, en prod avec la 1.10.0 le 05/11 (#488)) | J1 | ✅ | R95 |
| TF-J1-7 | Ce que le rejeu de la 1.8.0 a montré : « moi » est la personne qui demande ; une colonne nommée à peu près (« To Do ») est celle du projet, sinon sa colonne par défaut ; « Mark as done » quand la mission n'a rien changé ; le commentaire de l'agent s'affiche sur l'issue ouverte ; `echo` et les lectures de git sans demande ; GitHub, Slack et Plane au catalogue avec leur état (`taskforce-fullstack` #476, en prod avec la 1.9.0 le 02/11) | J1 | ✅ | R109 |
| TF-J1-8 | Cortex voit, demande et dit vrai, quel que soit le modèle : le contexte de l'écran à chaque message (R114) ; les gestes déclarent ce qu'il leur faut et TaskForce demande, en choix (R115) ; TaskForce dit ce qui a été fait, jamais le modèle seul (R116) ; un plan écrit par demande courante (R117) ; chaque échec devient un cas, mesuré sur chaque modèle, avec l'escalade (R118). Ordre : R116 d'abord ([séance n°17](../../recherche/conseil/seances/2026-11-02-cortex-voit-demande-dit-vrai.md)). Première partie, R116 et les six échanges de la Présidence en cas de la banque (R118) : `taskforce-fullstack` #483, fusionnée dans `dev` ; qwen3:8b à 3/6 cas avant comme après, l'annonce sans résultat d'outil de 5/6 à 6/6. Deuxième partie, R114 (l'écran avant les notes), R115 (les gestes déclarent ce qu'il leur faut, TaskForce demande en choix, créer un projet dans le MCP), R117 (cinq plans choisis par TaskForce, cinq cas) et la réponse vide signée par TaskForce : `taskforce-fullstack` #484, en prod avec la 1.10.0 le 05/11 (#488) | J1 | ✅ | R114 à R118 |
| TF-J1-9 | La fenêtre, « same as Claude Code » : à gauche le travail et ses conversations, rangés par projet ; au centre la conversation avec Cortex, le compositeur en bas ; à droite ce qui l'entoure (environnement, contexte, connecteurs, résultats, modifications, missions) ; les écrans en volets, entiers, la conversation repliée dans le compositeur en pleine largeur ; le modèle et ce qu'il a lu sous chaque réponse ; un volet « Progress » ; l'installateur à l'allure de la page de connexion ([séance n°18](../../recherche/conseil/seances/2026-11-05-atelier-fenetre.md)). Sans maquette, en trois lots : la fenêtre ; les volets et leurs adresses ; l'arrivée, « Progress » et ce qui quitte l'écran. Mesurée avant et après (E18). Lot 1 (R119 à R122, R124 ; les conversations rangées par projet, V118) : `taskforce-fullstack` #493, en prod avec la 1.11.0 et la desktop 1.8.0 le 07/11 (#494). Lot 2 (R120 : l'issue en volet, la poignée, la vue du travail, les adresses) : #496. Lot 3 en deux moitiés : la conversation (R123, R124 : l'arrivée à la place du tour guidé, « + », `@` et `/`, la ligne grise, le modèle sur les commentaires de Cortex, Ctrl+K qui trouve les issues ; V119, V120), #498 ; le volet « Progress » (R125), #497. Les lots 2 et 3 en prod avec la 1.12.0 et la desktop 1.9.0 le 08/11 (#499). Le micro est arrivé avec la 1.13.0 (TF-J1-12). Reste : la mesure E18 sur l'app desktop, à la recette de la Présidence | J1 | 🟡 | R119 à R126 |
| TF-J1-10 | L'arrivée tient en un regard ; « Waiting for you » ne compte que ce qui attend vraiment ; une ligne par chose ; Progress en onglets ([séance n°19](../../recherche/conseil/seances/2026-11-08-atelier-sobriete-banc-voix.md)), le quatrième (le banc) avec TF-J1-11. En prod avec la 1.13.0 et la desktop 1.10.0 le 08/11 (#503, #506) ; reste la recette de la Présidence sur l'app desktop | J1 | 🟡 | R127 à R130 |
| TF-J1-11 | Le banc des modèles : que puis-je confier à ce modèle ? Sept tâches du vrai travail (22 cas écrits avant tout passage), les réponses sous les yeux, le verdict de la personne, l'essai à l'aveugle sur ses issues (E19). Deuxième onglet de Progress, en prod avec la 1.13.0 et la desktop 1.10.0 le 08/11 (#502, #506) ; reste E19 avec la Présidence | J1 | 🟡 | R131 |
| TF-J1-12 | La voix dans le compositeur : un clic pour démarrer, un clic pour arrêter, rien ne part sans envoi, la transcription sur la machine (E15 : Parakeet par sherpa-onnx, 2 à 3 % d'erreur sur voix de synthèse). En prod avec la 1.13.0 et la desktop 1.10.0 le 08/11 (`taskforce-fullstack` #504, #506) ; reste la dictée de la Présidence à la recette | J1 | 🟡 | R76, R80, R132 |
| TF-J1-13 | Le contexte selon le modèle, comme Claude : la fenêtre de chaque modèle (celle que le fournisseur dit, sinon une estimation dite comme telle), un budget en jetons par requête, la compaction passé environ 80 % (`/compact` à la demande), la boucle d'outils tenue dans la fenêtre, rien de coupé sans le dire. En prod avec la 1.13.0 et la desktop 1.10.0 le 08/11 (#505, #506) ; reste l'essai à la recette et un fournisseur hébergé en vrai | J1 | 🟡 | Décision de la Présidence, 08/11 |
| TF-J1-14 | La barre de saisie, comme Claude : le retour à la ligne jusqu'à 17 lignes, le « + » (fichiers, issue, projet, connecteurs), le projet et le modèle sous la boîte, l'arrêt, la file d'attente ([séance n°20](../../recherche/conseil/seances/2026-11-09-atelier-recette-113.md)) | J1 | 🔄 | R133 à R135 |
| TF-J1-15 | La conversation : une seule voix, le travail replié, plus de mot « Sources », le cas de test en un geste, `/compact` lisible, le projet demandé quand il manque, le dépôt créé, les longs messages | J1 | 🔄 | R135 à R137, R143 |
| TF-J1-16 | La mission en déroulé : cinq étapes en phrases, les commandes et la preuve repliées, le résultat qui dit ce qui est rendu, un vrai « Stop ». PR #510 vers `dev` | J1 | 🔄 | R138 |
| TF-J1-17 | Les changements sous les yeux et la remise : lignes ajoutées et retirées en direct, diff sans pull request, retour en arrière par fichier, commentaire sur une ligne, remise à la première personne | J1 | 🔄 | R139, R140 |
| TF-J1-18 | Les listes, les volets et la palette : « Waiting for you » et les alertes en listes, le rail de droite, Ctrl+K | J1 | 🔄 | R133, R141 |
| TF-J1-19 | Le banc dit ce qu'il mesure : une file, un délai qui est un verdict, des descriptions, un seul onglet, l'essai à un modèle | J1 | 🔄 | R142 |
| TF-J1-20 | La mise à jour sans trou, la voix préparée seule, les noms (Cortex, le logo de Claude) | J1 | 🔄 | R143, R144 |
| TF-J2-1 | Le déroulé de la démo, son communiqué et sa foire aux questions, écrits d'abord | J2 | ⬜ | R105 |
| TF-J2-2 | Processus v1 : un canevas modifiable, cinq types d'étapes, exécuté par le moteur durable v1 | J2 | ⬜ | R97, ADR-023 |
| TF-J2-3 | Agents v1 ; la boucle d'agent de TaskForce sur n'importe quel modèle (missions sur un modèle local) | J2 | ⬜ | R92, R51 |
| TF-J2-4 | Règles v1 éditables : la table V102 écrite, la classe appliquée, les actions sans code retirées, des cas par règle | J2 | ⬜ | R94, R98 |
| TF-J2-5 | Contexte v1 : des documents importés avec version, responsable et date de validité, cités au passage près | J2 | ⬜ | R96 |
| TF-J2-6 | La vue du travail v1 ; les surfaces Travail, Processus et Règles, avec l'assistant | J2 | ⬜ | R95 |
| TF-J2-7 | Dossier v1 : il survit à la suppression, il est signé et vérifié ; le journal des actions d'IA ; un échec devient un cas | J2 | ⬜ | R93, R100, R101 |
| TF-J2-8 | Deux packs (livraison logicielle ; rédaction et revue de document), zéro code par pack ; mesure de départ de l'indice de confiance | J2 | ⬜ | R103, E17 |
| TF-J3 | Le profil de l'espace, le vocabulaire, les types d'objets, les règles complètes (seuils, double signature, séparation des rôles, charte), les packs, le français et l'anglais, la maquette du parcours d'arrivée, le troisième pack | J3 | ⬜ | R94, R98, R102 |
| TF-J4 | Le contexte : tous les formats, les droits prouvés, la recherche hybride, les citations, l'agent qui demande, la surface Connaissances, le manifeste d'ingestion | J4 | ⬜ | R96, R99 |
| TF-J5 | Des agents robustes : le moteur durable complet, le vérificateur indépendant, l'aperçu des effets, le bac à sable, les paliers d'autonomie, le registre et le routage des modèles | J5 | ⬜ | R92, R97 |
| TF-J6 | Les données souveraines : la carte des flux, les règles de sortie, le chiffrement du contenu et des sauvegardes, le dossier conservé, l'export complet, le profil serveur, le kit de conformité, OpenTelemetry | J6 | ⬜ | R93, R100 |
| TF-J7 | L'amélioration continue : les recommandations acceptées par une personne, la banque d'évaluations généralisée, l'essai contradictoire publié, les données possédées et l'affinage chez le client | J7 | ⬜ | R100, R101 |
| TF-J8 | Le parcours d'arrivée, qui se vit comme un jeu ; la démo complète sur trois natures de travail ; cinq personnes extérieures ; une évaluation par un tiers | J8 | ⬜ | R102, R103, E13, E14 |
| TF-J9 | La mise sur le marché : le modèle de revenus, la distribution, la spécification et l'essai publiés | J9 | ⬜ | R98, R106 |

**Critères de sortie de J0** (PV n°15) : un commit par écart fermé ; l'essai des droits de recherche vert ; R78 publiée avec « Apply » bloqué sur un échec de tests ; la boucle actuelle (Créer, Accorder, Relire) rejouée de bout en bout sur l'app desktop. Ajouté par la séance n°16 (R109, retenue le 01/11) : J0 se clôt sur le rejeu de la mission 6 par la Présidence, une fois la porte publiée ; la liste de fin de jalon reçoit la ligne « chaque demande de la table atteint la personne », prouvée par un essai automatique et par le rejeu.

**J0 clos le 02/11/2026** (R109) : la Présidence a rejoué la mission sur l'app desktop 1.5.0 (mission 7, TESTTA-2). La lecture de nodejs.org et la recherche web ont été demandées (journal du runner, 12:10 UTC), puis accordées pour la mission ; l'issue préparée par Cortex porte sa priorité, sa personne et « prepared by Cortex » ; pendant la mission, « Claude Code, for Pierre ». Les écarts relevés partent en J1 : « assignée à moi » non compris, la colonne « To Do », « Apply » éteint quand rien n'a changé, deux demandes inutiles (`echo`, `git branch`), le commentaire de l'agent à vérifier dans l'activité, les intégrations natives dans le catalogue, un chat plus visible.

**Critères de sortie de J1**, écrits le 01/11/2026, avant le jalon :
1. E16 mesurée : le délai d'une décision demandée au backend de la machine (médiane, 95e centile) face au moteur du runner, et le moteur Java compilé en JavaScript essayé sur les 51 cas ; la Présidence tranche R90.
2. Cortex répond par la passerelle Java avec Ollama, avec une API compatible OpenAI et avec l'API d'Anthropic ; l'ai-service Python et le relais de la coque ne servent plus ; la banque d'évaluations (R61) ne recule sur aucun cas.
3. Le catalogue ne montre que des connecteurs essayés ; le plan figé d'« AI Workflows » a disparu.
4. La liste de lancement : une installation propre, une mise à jour depuis la version publiée, une sauvegarde puis une restauration.
5. Ajouté par la séance n°16 (R113, retenue le 01/11) : la table de ce que sait faire chaque modèle de la machine de la Présidence, mesurée par la banque d'évaluations ; R51 essayée par la passerelle, cinq tâches en commentaire par qwen3:8b, trois réussies au moins (sinon R51 reste en J2). **04/11/2026** : la table mesurée pour les sept modèles du poste de la Présidence, et R51 à 4 tâches sur 5 (TF-J1-4, E11) ; reste sa relecture par la Présidence.
6. Ajouté par la Présidence le 02/11/2026 : les gestes de TF-J1-5 se font depuis la barre, sur n'importe quel modèle de la passerelle, sous les règles et au dossier ; l'inventaire de TF-J1-6 est publié avec la part couverte.

**Pour les critères de sortie de J2**, décidé par la Présidence le 02/11/2026 (à reprendre quand ils s'écrivent, avant J2) : la boucle de démo se joue entièrement depuis la barre, de la création jusqu'à « Apply » ; les accords se donnent par les boutons des cartes, dans la conversation.
5. Les tests verts ; la boucle rejouée sur l'app desktop, avec Claude Code et Ollama.

---

## 1. P0 — Correctifs bloquants

À traiter en premier : ils débloquent des pans entiers de l'app (cf. [Problèmes connus](../09-audits/Problemes_Connus.md)).

> **▶ MAJ 05/07/2026** — Vérifié sur la branche `test/v1-hardening` (le snapshot 08/06 était sur `feat/dashboard`) :
> **TF-FIX-001 à 005 sont ✅ résolus** dans le code actuel (préfixes `/api` présents partout, groupes de routes front déclarés,
> import `profile-service` correct, refresh/logout désormais **Keycloak natif** — cf. TF-SEC-009, webhooks Stripe câblés).

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-FIX-001 | ✅ **Résolu** — préfixe `/api` présent sur les 5 contrôleurs (Cycle, Team, Page, Discussion, Channel) | 🔴 P0 | M | C24 | PC-001 |
| TF-FIX-002 | ✅ **Résolu** — 4 groupes de routes front déclarés (MESSAGE/INTEGRATION/ATTACHMENT/ROADMAP) | 🔴 P0 | S | C17 | PC-002 |
| TF-FIX-003 | ✅ **Résolu** — `profile-service.ts` importe bien `./client` | 🔴 P0 | S | C16 | PC-003 |
| TF-FIX-004 | ✅ **Résolu (05/07)** — refresh/logout migrés sur Keycloak natif (rotation IdP, logout serveur) | 🟠 P1 | M | C24 | PC-004 |
| TF-FIX-005 | ✅ **Résolu** — 5 handlers webhook Stripe câblés (`StripeWebhookController` → `StripeWebhookService`) | 🟠 P1 | L | C23 | PC-005 |

## 2. Frontend

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-FE-001 | Compléter `team-store` (parité CRUD) | 🟡 P2 | M | C15 | PC-006 |
| TF-FE-002 | Brancher « Create issue » de la command palette | 🟢 P3 | S | C15 | PC-013 |
| TF-FE-003 | Retirer les données mock chat (`messages/data.ts`) une fois l'API câblée | 🟡 P2 | S | C15 | PC-011 |
| TF-FE-004 | Audit accessibilité (WCAG 2.1 AA) : navigation clavier, ARIA, contrastes, `axe` | 🟠 P1 | L | C13/C15 | ★ |
| TF-FE-005 | Compléter l'i18n FR/EN (`constants_fr/en`) sur toutes les vues | 🟡 P2 | M | C15 | — |
| TF-FE-006 | En-têtes de sécurité front + CSP (via Next/Nginx), `npm audit` 0 vuln | 🟠 P1 | M | C16 | DT-019 |
| TF-FE-007 | Budget de performance : Lighthouse ≥ 90, analyse de bundle, lazy-loading, images optimisées | 🟡 P2 | M | C16 | ★ |
| TF-FE-008 | États d'erreur/chargement homogènes (error boundaries, skeletons) | 🟢 P3 | M | C13 | — |
| TF-FE-009 | Validation Zod systématique sur tous les formulaires | 🟡 P2 | M | C16 | — |
| TF-FE-010 | ★ Storybook de la UI library (`components/ui`) | 🟢 P3 | L | C13 | ★ |
| TF-FE-011 | Écoconception front : éco-index, sobriété requêtes/poids | 🟢 P3 | M | C16 | — |

## 3. Backend

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-BE-001 | Vrai streaming SSE de l'assistant (tokens Groq) | 🟡 P2 | M | C22 | PC-009 |
| TF-BE-002 | Cache des AI Insights (`ai_runs`/`insight_snapshots`) + garde quota/timeout Groq | 🟡 P2 | M | C22 | PC-007 |
| TF-BE-003 | Feature flags IA (`enabled`/`smartAssign`/`assistant`/`insights`) | 🟡 P2 | M | C22 | PC-014 |
| TF-BE-004 | Notification email + alerte équipe pour les inquiries Sales | 🟡 P2 | S | C22 | PC-008 |
| TF-BE-005 | Compléter les annotations OpenAPI + publier la doc API (Swagger) | 🟠 P1 | M | C24 | DT — |
| TF-BE-006 | Rate limiting / throttling sur endpoints sensibles (auth, IA) | 🟠 P1 | M | C21/C24 | ★ |
| TF-BE-007 | Journalisation structurée (corrélation, niveaux) + masquage données sensibles | 🟠 P1 | M | C21/C32 | — |
| TF-BE-008 | Audit requêtes JPA : index, détection N+1, pagination généralisée | 🟡 P2 | M | C9/C21 | ★ |
| TF-BE-009 | ★ Couche de cache (Redis) pour sessions/Groq/analytics | 🟢 P3 | L | C21 | ★ |
| TF-BE-010 | Décision `ai-service` Python : supprimer ou documenter en legacy | 🟢 P3 | S | C22 | PC-012 |
| TF-BE-011 | Validation/filtrage exhaustif des entrées (DTO `@Valid`) + chiffrement données sensibles | 🟠 P1 | M | C24 | — |
| TF-BE-012 | Écoconception back : sobriété requêtes, tailles de payload | 🟢 P3 | S | C22 | — |
| TF-MCP-03 | Cortex agentique : réflexe d'intégration. Pilier 1 (va chercher l'info via l'outil connecté au lieu de dire « pas d'accès ») ✅ ; Pilier 2 routage défaut TaskForce + propose les deux (prérequis : outils internes `create_issue`/`list_issues`) ; Pilier 3 « connecte X » (injection du catalogue) | 🟡 P2 | L | C22 | — |
| TF-MCP-04 | Import de projet externe (Linear → issues natives TaskForce) dans le wizard nouveau projet, via les outils MCP de lecture (`list_projects`/`list_issues`) + mapping statuts/labels. Plus tard : sync continu 2 sens | 🟢 P3 | L | C22 | — |

## 4. Landing page

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-LP-001 | SEO technique : `<title>`/meta, sitemap.xml, robots.txt, Open Graph, données structurées (JSON-LD) | 🟠 P1 | M | C20 | — |
| TF-LP-002 | Atteindre ≥ 70 % des critères SEO (audit Lighthouse SEO) | 🟠 P1 | M | C20 | — |
| TF-LP-003 | Outils de mesure d'audience (analytics respectueux RGPD) | 🟡 P2 | S | C20 | — |
| TF-LP-004 | Densité mots-clés + contenu (pricing, CTA, valeur) | 🟡 P2 | M | C20 | — |
| TF-LP-005 | Accessibilité + performance landing (Lighthouse a11y/perf ≥ 90) | 🟡 P2 | M | C20 | ★ |
| TF-LP-006 | i18n landing si cible bilingue | 🟢 P3 | M | C20 | — |

## 5. Infrastructure & DevOps

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-INFRA-001 | Choix d'hébergement cloud argumenté + **diagramme de déploiement** + estimation coûts/élasticité | 🟠 P1 | L | C29/E21 | — |
| TF-INFRA-002 | Nom de domaine + configuration DNS + certificats TLS (Let's Encrypt) | 🟠 P1 | M | C28/E23 | — |
| TF-INFRA-003 | Environnement de production durci (secrets manager, hôte **bastion**, isolation réseau) | 🟠 P1 | L | C30/E22 | — |
| TF-INFRA-004 | Pipeline CD : qualification → production (au-delà du CI actuel) | 🟠 P1 | L | C31/E24 | — |
| TF-INFRA-005 | Observabilité : dashboards SigNoz + sondes + alertes (état services & sécurité) | 🟡 P2 | M | C32/E26 | — |
| TF-INFRA-006 | Stratégie de sauvegarde/restauration validée (test de restore) | 🟠 P1 | M | C9/C32 | PS/PCA/PRA |
| TF-INFRA-007 | Corriger le chemin du healthcheck actuator (`/actuator/health`) | 🟢 P3 | S | C32 | PC-015 |
| TF-INFRA-008 | ★ Durcissement images Docker (non-root, distroless, SBOM, scan trivy bloquant en CI) | 🟡 P2 | M | C26 | ★ |
| TF-INFRA-009 | Runbooks ops (déploiement, incident, restore) — cf. `_templates/TPL_Runbook.md` | 🟡 P2 | M | C27/C32 | — |
| TF-INFRA-010 | ★ IaC (Terraform/Ansible) pour l'environnement cible | 🟢 P3 | XL | C30 | ★ |
| TF-INFRA-011 | **Corriger `docker-compose.prod.yml`** — des `` `n `` PowerShell **littéraux** (lignes ~65/114) cassent le YAML et attachent le volume d'import realm Keycloak au **mauvais service** (backend au lieu de keycloak). Découvert le 05/07. | 🟠 P1 | S | C30 | — |
| TF-BUILD-001 | **Build backend cassé par dérive d'image** — le tag mouvant `maven:3.9-eclipse-temurin-21` a tiré JDK 21.0.11 → NPE javac `SharedNameTable` avec Lombok au `testCompile`. **Contournement appliqué** (`-XDuseUnsharedTable=true` + fork dans le `pom`). À terme : **épingler** l'image Maven sur un digest sain. Découvert le 05/07. | 🟡 P2 | S | C26 | — |

## 6. Tests & qualité

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-TEST-001 | Couverture **front ≥ 50 %** (Vitest + RTL + MSW) + rapport publié | 🟠 P1 | L | C18 | PC-010 |
| TF-TEST-002 | Couverture **back ≥ 50 %** (JUnit/Mockito) + rapport JaCoCo — ✅ **02/07 : 86,1 % (668 tests), gate JaCoCo ≥ 0,84 bloquant** | ✅ done | L | C25 | PC-010 |
| TF-TEST-003 | Plan de tests documenté (front & back), cohérent avec les specs | 🟠 P1 | M | C18/C25 | — |
| TF-TEST-004 | Tests d'intégration back (**Postgres réel** pgvector + Flyway) — ✅ **02/07 socle `@DataJpaTest`** ; Keycloak/MinIO/Stripe → E2E | ✅ done | L | C25 | ★ |
| TF-TEST-005 | ★ E2E Playwright sur les parcours clés (auth, issue, smart-assign) | 🟡 P2 | L | C18 | DT-022 |
| TF-TEST-006 | ★ Tests de contrat API (front ↔ back) pour prévenir les régressions de routes | 🟡 P2 | M | C17/C24 | PC-001/002 |
| TF-TEST-007 | Tests de non-régression + gate de couverture en CI | 🟡 P2 | M | C19/C26 | — |
| TF-TEST-008 | Tests d'accessibilité (axe) et UX (utilisateurs en situation de handicap) | 🟢 P3 | M | C18 | — |
| TF-TEST-009 | **Tests de charge/performance** (k6/Gatling) sur endpoints critiques — vérifier les seuils PERF-01..05 du STB (actuellement validés en comportement, pas en latence) | 🟡 P2 | M | C25 | STB §1 |

## 7. Sécurité

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-SEC-001 | Revue OWASP Top 10 (injection, auth, accès, SSRF…) + checklist | 🟠 P1 | L | C21/C24 | ★ |
| TF-SEC-002 | Scan dépendances (front `npm audit`, back OWASP Dependency-Check) bloquant en CI | 🟠 P1 | M | C16/C22 | — |
| TF-SEC-003 | SAST en CI (`semgrep`) + remédiation des findings | 🟡 P2 | M | C19/C26 | — |
| TF-SEC-004 | Gestion des secrets (hors repo, vault/CI secrets, rotation) | 🟠 P1 | M | C21 | — |
| TF-SEC-005 | En-têtes HTTP de sécurité (HSTS, CSP, X-Frame-Options…) + SSL valide | 🟠 P1 | M | C16 | DT-019 |
| TF-SEC-006 | Contrôle d'accès : revue des `@PreAuthorize`/checks workspace/projet | 🟠 P1 | M | C21/C24 | — |
| TF-SEC-007 | ★ Modèle de menaces (threat model) + registre des risques — ✅ **05/07 : STRIDE documenté** (`07-securite/Threat_Model_STRIDE.md`, 6 catégories × flux réels + risques résiduels) | 🟢 P3 | M | C21 | ★ |
| TF-SEC-008 | Sécurité paiement : vérification signature webhook Stripe, PCI scope | 🟠 P1 | M | C23 | PC-005 |
| **TF-SEC-009** | ✅ **Résolu (05/07)** — émission des JWT migrée vers **Keycloak OIDC (RS256)** : `JwtService` custom supprimé, décodeur `NimbusJwtDecoder` sur JWK Keycloak + validation issuer, login/refresh/logout via `KeycloakAuthService` (ROPC + refresh natif + `users().logout()`). Auto-login post-inscription retiré (Keycloak exige le mot de passe) → redirection `/auth/login`. Table `refresh_tokens` conservée mais inutilisée. **Vérifié : 658 tests backend verts.** Doc auth à réviser : [[Auth_Autorisation]], [[Journal_Decisions_ADR]] (ADR-011). | 🟠 P1 | L | C21/C24 | PC-019 |
| TF-SEC-010 | **DAST ZAP baseline en CI** (bloquant sur alerte HIGH) — complète TF-SEC-002/003 (SAST/SCA déjà spécifiés en CI). Intègre `security-scan.ps1 -Dast` au pipeline avant release. | 🟡 P2 | M | C19/C21 | Threat_Model_STRIDE §4 |
| TF-SEC-011 | ✅ **Résolu (05/07)** — **rate limiting distribué** : `RateLimitFilter` accepte un `ProxyManager` Bucket4j/Lettuce (Redis) partagé entre instances ; fallback local si `ratelimit.distributed.enabled=false` (dev). Redis ajouté au compose prod + `render.yaml`. | 🟡 P2 | M | C30 | Threat_Model_STRIDE (D3) |

## 8. RGPD & légal

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-RGPD-001 | ✅ **Résolu (05/07)** — bannière `cookie-banner.tsx` présente + requalifiée en **notice d'information** (l'app n'utilise que des cookies strictement nécessaires → consentement non requis par la CNIL ; un faux « Refuser » sur des cookies d'auth serait trompeur). CTA d'acquittement « Got it », mention de l'absence de traceurs. | 🟡 P2 | M | C11/E9 | Politique_Confidentialite_CGU §5 |
| TF-RGPD-002 | ✅ **Politique de confidentialité** — **fait (05/07)** : `PrivacyPolicyPageNew.tsx` + `constants_en.ts` (privacy) | ✅ | — | C11/E9 | Politique_Confidentialite_CGU |
| TF-RGPD-003 | ✅ **Accès/export/suppression RGPD** — **fait** : `GdprService.exportMyData` + `deleteMyAccount` + `GdprController` (`/api/gdpr/*`) | ✅ | — | C11/E9 | Audit_RGPD_Conformite §2 |
| TF-RGPD-004 | Double opt-in sur les traitements collectant des données personnelles | 🟢 P3 | M | C11/E9 | — |
| TF-RGPD-005 | 🟡 **Partiel (05/07)** — sous-traitants **corrigés** dans `constants_en.ts`/`constants_fr.ts` (AWS/GA faux → Stripe + Groq, démontrables). Reste : page **Mentions légales** dédiée (LEN Art. 6). | 🟡 P2 | S | C11 | Politique_Confidentialite_CGU §4 |
| TF-RGPD-006 | ✅ **Registre des traitements + audit RGPD** — **fait (05/07)** : `Registre_Traitements_RGPD.md` (7 traitements Art. 30) + `Audit_RGPD_Conformite.md` (E9) | ✅ | — | C11/E9 | Registre_Traitements_RGPD |
| TF-RGPD-007 | ✅ **Résolu (05/07)** — `GdprService.deleteMyAccount` supprime l'identité Keycloak (appel `KeycloakService.deleteUser` **après commit**, tolérant à l'échec ; invalide aussi les sessions). Vérifié en intégration Postgres. | 🟡 P2 | S | C11 | Audit_RGPD_Conformite §2.2 |
| TF-RGPD-008 | **DPA formel Groq** — formaliser Data Processing Agreement avec Groq Inc. (USA) pour le contexte LLM Smart Assign | 🟡 P2 | S | C11 | Registre_Traitements_RGPD §T4 |
| TF-RGPD-009 | **Procédure notification violations** (Art. 33 RGPD) — délai 72h CNIL non documenté comme procédure opérationnelle | 🟡 P2 | S | C11 | Audit_RGPD_Conformite §7 |

## 9. Conventions & process

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-CONV-001 | Pre-commit hooks (husky + lint-staged) : ESLint/Prettier/format | 🟡 P2 | S | C19 | — |
| TF-CONV-002 | Linters/formatters back (Spotless/Checkstyle) en CI | 🟡 P2 | S | C26 | — |
| TF-CONV-003 | Checklist de code review + template de PR (déjà présent à valider) | 🟢 P3 | S | C5 | — |
| TF-CONV-004 | Conventions de code documentées (front & back) + ADR `ADR-0001` | 🟡 P2 | M | C5/C10 | — |
| TF-CONV-005 | ★ Conventional commits + changelog auto (release-please ou équivalent) | 🟢 P3 | M | C26 | — |

## 10. Documentation

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-DOC-001 | Compléter le **mémoire** : rédiger chaque compétence des 4 blocs (preuves + captures) | 🟠 P1 | XL | C1–C32 | [Mémoire](../16-memoire-rncp/README.md) |
| TF-DOC-002 | Harmoniser le front-matter de toutes les notes sur le [standard](../04-engineering/Conventions_Documentation.md) | 🟡 P2 | M | C27 | — |
| TF-DOC-003 | Compléter la **doc utilisateur** (Manuel, Installation, FAQ, Release Notes) | 🟠 P1 | L | — | [Utilisateur](../15-utilisateur/Manuel_Utilisateur.md) |
| TF-DOC-004 | Dossier de conception : diagrammes de **cas d'usage**, **classes**, **MCD** (Excalidraw/PlantUML) | 🟠 P1 | L | C7/C8/E8 | — |
| TF-DOC-005 | Formaliser les **wireframes** (E7) à partir de `assets/maquettes/` | 🟡 P2 | M | C6/E7 | — |
| TF-DOC-006 | Méthodologie de **veille** technologique (E10) | 🟡 P2 | S | C12/E10 | — |
| TF-DOC-007 | Doc API publiée pour tiers + **changelog** structuré (E29) | 🟠 P1 | M | C27/C32 | [Release Notes](../15-utilisateur/Release_Notes.md) |
| TF-DOC-008 | ADRs des décisions clés (stack, multi-tenant, IA Groq, STOMP) | 🟡 P2 | M | C10 | — |
| TF-DOC-009 | Note de préconisations techniques (E3) + planification/budget (E2) | 🟡 P2 | M | C2/C3 | — |
| TF-DOC-010 | Note justifiant la méthode **agile** + trame de compte rendu (E5/E6) | 🟡 P2 | S | C4 | — |
| TF-DOC-011 | ✅ **Résolu (05/07)** — sweep doc auth HS512→OIDC : `Auth_Autorisation.md` (v1.1) + 17 fichiers alignés (PSSI, STRIDE, séquences UML, CdCT_v2, Dossier_Conception, Sécurité, Modules, Table_Reconciliation, STB, Registre/Audit RGPD, Politique_Tests, Matrice_Tracabilité, Cahier_Recettes, Plan_SSDLC, Stripe, FAQ, Release_Notes, Catalogue, Bloc1). Restent volontairement les mentions **historiques** (ADR-003/011, Note d'innovation, veille ANSSI). | 🟡 P2 | M | C27 | ADR-011 |

## 11. Synthèse de couverture RNCP

<p class="lead">
Le tableau ci-dessous relie chaque compétence à son chantier principal. La <a href="../16-memoire-rncp/README.md">matrice
du mémoire</a> reste la checklist « 100 % » faisant foi.
</p>

| Bloc | Compétences | Chantiers backlog dominants |
| ---- | ----------- | --------------------------- |
| 1 — Conception | C1–C12 | TF-DOC-004/005/006/009/010, TF-RGPD-* (C11) |
| 2 — Front-end | C13–C20 | TF-FE-*, TF-TEST-001, TF-LP-* (C20), TF-SEC-005 (C16) |
| 3 — Back-end | C21–C26 | TF-BE-*, TF-TEST-002, TF-SEC-*, TF-FIX-005 (C23) |
| 4 — Déploiement | C27–C32 | TF-INFRA-*, TF-DOC-007, TF-DOC-001 |

<blockquote class="important">
<strong>Ordre conseillé :</strong> P0 (TF-FIX-001→005) → couverture de tests (TF-TEST-001/002, exigence
≥50 % du référentiel) → sécurité & RGPD (P1) → déploiement/observabilité → finition pro (★). En parallèle,
rédiger le mémoire (TF-DOC-001) au fur et à mesure que chaque preuve est produite.
</blockquote>

---

> **Note Brain OS** — Registre vivant : mettre à jour le statut des tâches à chaque avancement. Relié à
> [Problèmes connus](../09-audits/Problemes_Connus.md) (PC-xxx) et à la [matrice du mémoire](../16-memoire-rncp/README.md).

**Dernière mise à jour :** 05/07/2026 (round de correctifs V1-hardening : TF-SEC-009/011, TF-RGPD-001/005/007, +TF-INFRA-011/TF-BUILD-001)  
**Version :** 1.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
