---
id: conseil-seance-25-plan-des-lots
title: "Le plan des lots du workflow pilotable (séance n°25)"
doc_type: plan
statut: proposed
date: "13/11/2026"
auteur: Pierre MICHEL
tags: [recherche, conseil, workflow, lots, j2, plan]
related:
  - "./2026-11-13-le-workflow-pilotable.md"
  - "../../decisions/ADR-023-DRAFT-execution-durable-postgresql.md"
  - "../../decisions/ADR-027-DRAFT-modele-des-processus.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Le plan des lots du workflow pilotable

> Joint au PV de la [séance n°25](./2026-11-13-le-workflow-pilotable.md) (R178, en attente de la Présidence). Dix lots, W0 à W9 :
> W0 à W5 dans J2, réduits à ce qu'exige le processus « intégrer un module » d'E20 ; W6 à W9 après J2. Les durées sont des
> `[HYPOTHÈSE]`.

## Les règles de tous les lots

- **Les critères de fin sont écrits ici, avant le lot.** Un lot est fini quand tous ses critères tiennent, vérifiés.
- **Les relectures** : R159 (un relecteur qui n'a pas écrit le code, avant la fusion) pour un lot qui touche aux connexions, aux
  droits, aux accords, aux règles ou aux données d'une entreprise ; R161 (les écrans à 1440 et 375 px, en clair et en sombre, un
  contrôle d'accessibilité, mesurés à la grammaire de R133) pour un lot qui touche un écran. Puis l'essai de la Présidence sur
  l'app desktop, à la main (R162 amendée).
- **Les vérifications du dépôt** : backend, `mvn verify` ou `.\scripts\it.ps1 -Test ALL` ; frontend, `npx tsc --noEmit`,
  `npm run lint`, `npx vitest run --coverage` (la couverture vaut par fichier : un nouveau fichier a ses tests).
- **Des données vivantes seulement** : aucune donnée fictive, à l'écran comme dans les états vides (R15).
- **Chaque geste passe par les règles et entre au dossier.**
- **Un lot de code à la fois**, sauf W1 et W2, qui ne se touchent pas.
- **La définition de « fini » comprend les notes** : `v1/02-produit/Backend.md`, `Frontend.md`, `v1/05-api/API.md` dans
  `taskforce-docs`, et une trace dans `.ai/roadmap.md`.

## Les lots en un regard

| Lot | But | Dépend de | Relectures | Quand |
| --- | --- | --- | --- | --- |
| W0 | Les données vivantes du projet | Rien | R159 | J2, lancé |
| W1 | L'application Workflow, sur les données vivantes, sans moteur | W0 | R159, R161 | J2 |
| W2 | Le modèle des processus et son vérificateur | Rien | R159 | J2, en même temps que W1 |
| W3 | Le moteur durable v1 et ses coupures | W2 ; le dossier signé (TF-J2-7) avant | R159 | J2 |
| W4 | Le brouillon de l'IA et le premier workflow par défaut | W1, W2 | R159, R161 | J2 |
| W5 | Piloter le processus : incidents, attentes, manques | W1, W3 ; W4 pour le brouillon | R159, R161 | J2, puis E20 |
| W6 | Éditer et créer ses workflows ; le LIMS ; Documents | W4, W5 | R159, R161 | Après J2 (J3) |
| W7 | Exploiter : modifier, migrer, compenser, relancer depuis une étape | W3, W5 | R159, R161 | Après J2 (J5) |
| W8 | S'ouvrir : Camunda, MCP Apps, un processus appelable | W2, W5 | R159 | Après J2 (J5) |
| W9 | Améliorer : l'analyse sur la même carte | W5, le dossier | R161 | Après J2 (J7) |

## Dans J2, avant E20

### W0 : les données vivantes du projet (lancé)

- **But** : donner à la vue les données qui lui manquent (les manques 1 et 2 de la carte du code du 13/11).
- **Contenu** :
  - les dépendances de toutes les issues d'un projet, en une lecture ; un événement à chaque relation ajoutée ou retirée ;
  - les missions du projet et leurs accords en attente, en une lecture paginée par projet ;
  - le sujet temps réel `/topic/projects.{id}.delivery` ;
  - la couche de données du front : routes, services, stores, un abonnement ; aucun écran.
- **Dépend de** : rien. Branche `feat/workflow-live-data`.
- **Fini quand** :
  1. une lecture rend toutes les relations entre les issues d'un projet, de chaque sorte qui existe, vérifiées dans le service comme
     la liste des issues (l'appartenance au projet, puis le rôle) ; un non-membre ne reçoit rien ;
  2. ajouter ou retirer une relation publie un événement sur `/topic/projects.{id}` et entre à l'activité de l'issue ;
  3. une lecture rend les missions du projet, paginée par projet et non par le plafond de 200 de l'espace ; pour chacune, son
     état, son étape, ses liens (branche, pull request, suite) et ses accords en attente, avec les champs d'aujourd'hui ;
     `canDecide` se calcule pour l'appelant exactement comme `RuleApprovers` le décide ;
  4. `/topic/projects.{id}.delivery` publie les changements d'état et d'étape d'une mission, et chaque accord demandé ou décidé ;
     seuls les membres du projet s'y abonnent (`StompAuthInterceptor`) ; le sujet `.analysis` s'abonne depuis le front ;
  5. les routes dans `frontend/lib/config/api-routes.ts`, les services dans `frontend/lib/api/`, les stores (les relations du
     projet dans le store des issues, ses missions et leurs accords dans celui des livraisons), et un hook par
     `frontend/lib/hooks/use-stomp.ts` ; chaque nouveau fichier a ses tests ;
  6. `fern/openapi/openapi.json` régénéré ; `Backend.md` et `API.md` à jour.
- **Relectures** : R159.
- **Quand** : J2.

### W1 : l'application Workflow, sur les données vivantes, sans moteur

- **But** : la vue du projet au rang du board, pilotée sur ses nœuds, avant tout processus ([spécification d'UX](./2026-11-13-le-workflow-pilotable-ux.md)).
- **Contenu** :
  - la route `projects/[id]/workflow`, l'onglet « Workflow » après « Board », `workflowPath` à côté de `boardPath`, `"workflow"`
    dans les hôtes de projet de l'adresse, les mêmes entrées que le board (le bouton de la ligne du titre, Ctrl+K, les liens des
    réponses) ; la carte des missions mène à la route ;
  - l'objectif du projet : trois champs (le but en une phrase, la date visée, de un à cinq critères de réussite), leur migration
    Flyway, leurs routes, vérifiés comme le reste du projet, et le dialogue « Add an objective » (560 px) ;
  - les colonnes du projet comme étapes ; les issues comme nœuds, avec leur mission, leurs accords et le nombre de leurs
    documents ; les dépendances à la sélection ;
  - les états, leur tri, les trois densités, l'inspecteur, les gestes qui existent déjà (ouvrir, décider, demander à Cortex,
    arrêter, relancer, confier, déplacer), le temps réel par W0, tels que la spécification les décrit ;
  - dans la conversation, la carte compacte d'un nœud et « Open in Workflow » ;
  - le canevas d'aujourd'hui retiré avec son dialogue (`workflow-canvas.tsx`, `workflow-canvas-dialog.tsx`), et `@xyflow/react`
    si plus rien ne l'importe ;
  - les textes dans `frontend/lib/constants_en.ts`.
- **Dépend de** : W0.
- **Fini quand** :
  1. l'onglet « Workflow » ouvre le volet à `/{slug}/projects/{id}/workflow` ; le nœud choisi est dans l'adresse (`?node=`) ;
     retour et avant marchent ; un lien de réponse ouvre la vue sur son nœud ;
  2. chaque nœud est une issue, une mission ou un accord réels : un test compare les nœuds rendus aux données de l'API ;
  3. un accord décidé depuis un nœud entre au dossier, et quitte « Waiting for you » sur un autre client en moins de deux secondes ;
  4. une dépendance ajoutée sur le board se voit à la sélection du nœud, sans recharger ;
  5. les dix états suivent la table de la spécification, chacun avec sa marque et son mot, dans l'ordre de tri qu'elle donne ; une
     mission relancée ne passe pas au vert avant d'avoir réussi ;
  6. Summary, Plan et Detail se choisissent par le sélecteur et par 1, 2, 3, et le choix se retient pour la personne ; à 375 px,
     la liste par étape, et l'inspecteur en feuille ;
  7. sans objectif, l'en-tête le dit et propose de l'écrire ; avec, il montre le but, la date et les critères ;
  8. aucun mot interne au premier regard, aucun symbole de BPMN, aucune couleur sans son mot ;
  9. les vérifications du frontend et du backend vertes ; la revue des écrans sans défaut haut ouvert ; la relecture R159 sur la
     décision d'un accord depuis un nœud et sur les droits de l'objectif ; l'essai de la Présidence sur l'app desktop ;
  10. puis E24, dans les dix jours.
- **Relectures** : R161, R159.
- **Quand** : J2. `[HYPOTHÈSE]` une semaine.

### W2 : le modèle des processus et son vérificateur

- **But** : les processus comme données versionnées, dans le sous-ensemble de BPMN 2.0 ([ADR-027](../../decisions/ADR-027-DRAFT-modele-des-processus.md)).
- **Contenu** :
  - la définition et ses versions immuables (l'auteur, l'empreinte, calculée sur notre modèle), leurs tables et leurs routes de
    lecture ;
  - la liste écrite du sous-ensemble de J2, figée sur le processus d'E20 ; l'extension `tf:`, documentée ;
  - le vérificateur en Java, pur, avec ses cas ; l'import et l'export en XML de BPMN 2.0 ;
  - le schéma de sortie d'un brouillon, pour les modèles ;
  - le processus « intégrer un module » écrit, premier workflow par défaut de la livraison logicielle, ses étapes verrouillées
    comprises (les points de pause de TF-J2-10) ;
  - l'onglet « Definition » de l'inspecteur le lit ; aucun éditeur.
- **Dépend de** : rien ; en même temps que W1.
- **Fini quand** :
  1. E23 tenue : le processus d'E20 dans le sous-ensemble, exporté, ouvert sans erreur dans le Desktop Modeler de Camunda,
     réimporté à l'identique (la même empreinte, l'extension `tf:` gardée) ;
  2. le vérificateur refuse, avec sa raison en mots, chaque élément hors du sous-ensemble et chaque faute qu'ADR-027 nomme (une
     étape sans personne, une étape d'agent sans zone, une étape verrouillée absente, une décision sans condition jugée par du code,
     une étape qui ne mène à aucune fin) : un cas par refus ;
  3. une publication crée une version immuable ; changer une version publiée échoue, en base comme dans le service ;
  4. l'accès vérifié dans le service, l'appartenance au projet d'abord ; la migration au prochain numéro libre, vérifiée contre
     `origin/dev` juste avant le commit ;
  5. la liste du sous-ensemble et l'extension `tf:` documentées dans `Backend.md` et `API.md`.
- **Relectures** : R159.
- **Quand** : J2. `[HYPOTHÈSE]` quatre jours.

### W3 : le moteur durable v1, et ses coupures

- **But** : le processus d'E20 survit aux coupures ([ADR-023](../../decisions/ADR-023-DRAFT-execution-durable-postgresql.md), amendé).
- **Contenu** :
  - le journal par instance ; les états d'attente comme points de sauvegarde ; la table des travaux, ses verrous et son verrou
    optimiste ; trois tentatives au plus, puis l'incident ; les clés d'idempotence des effets ; les minuteries, les messages, les
    accords en signaux ; chaque geste par les règles et au dossier ;
  - le banc des coupures, avec Operaton en témoin, à version figée, dans les tests seulement ;
  - les seuils, confirmés par la Présidence avant l'essai.
- **Dépend de** : W2 ; le dossier signé (TF-J2-7) passe avant, dans l'ordre de R170.
- **Fini quand** :
  1. E21 tenue : trois coupures, trois types d'étapes, dix passages chacun ; aucune étape perdue ; aucun effet en double, vérifié
     par les clés au dossier ; l'instance repart seule dans les 30 secondes ; au repos, au plus 50 Mo de mémoire et 1 % d'un cœur
     de plus sur l'app desktop ;
  2. une étape d'agent qui échoue trois fois crée un incident (l'étape, la cause, l'heure) ; l'instance s'arrête sur elle ; une
     personne la relance, la passe ou l'arrête, et le geste entre au dossier ;
  3. un accord attendu survit au redémarrage du backend, et se décide après ;
  4. le critère 6 de J2 : le processus d'E20 repris après un redémarrage ;
  5. Operaton n'entre dans aucune dépendance de l'application : un contrôle de la construction le vérifie ;
  6. les tests unitaires de la logique, les tests d'intégration sur PostgreSQL, le banc.
- **Relectures** : R159.
- **Quand** : J2. `[HYPOTHÈSE]` une semaine et demie.

### W4 : le brouillon de l'IA et le premier workflow par défaut

- **But** : « décrire l'objectif » donne un brouillon en mots, vérifié par du code, accepté étape par étape (R169, R175).
- **Contenu** :
  - les conventions (moins de dix lignes) et les exemples ; le brouillon par Cortex, sur n'importe quel modèle, en sortie
    structurée ; le vérificateur, deux essais au plus, puis la personne ;
  - ce qui est de trop, jugé au brouillon : chaque étape écartée avec sa raison et « Keep it » ; une étape verrouillée jamais
    écartée ; rien d'écarté dans un workflow marqué régulé ; les questions du brouillon ;
  - le mode « Edit » de l'application : le bandeau, accepter, changer ou retirer chaque étape, ajouter une étape, les questions,
    « Publish version {n} » ; aucun « tout accepter » ; partir d'une liste vide ;
  - la carte du brouillon dans la conversation, « Review in Workflow » ;
  - les cas du brouillon dans la banque d'évaluations (E25), lus dans Progress.
- **Dépend de** : W1, W2.
- **Fini quand** :
  1. E22 faite : le brouillon d'E20, accepté étape par étape par la Présidence ; les étapes changées et les questions comptées ;
  2. E25 tenue : sur dix objectifs, dont des objectifs de la Présidence et des cas pièges, aucune étape verrouillée écartée, et huit
     brouillons au moins qui passent le vérificateur en deux essais au plus, modèle par modèle ; un modèle qui écarte une étape
     verrouillée n'est plus proposé pour le brouillon ;
  3. publier exige que chaque étape soit acceptée et ait une personne qui en répond, que les questions aient leur réponse et que
     le vérificateur passe ; aucun bouton « tout accepter » n'existe ;
  4. le nombre d'étapes écartées entre au dossier de la version publiée ;
  5. partir d'une liste vide marche ;
  6. la revue des écrans ; la relecture R159 sur les étapes verrouillées et le vérificateur ; l'essai de la Présidence.
- **Relectures** : R159, R161.
- **Quand** : J2, pour le seul workflow d'E20 ; les autres natures de travail après. `[HYPOTHÈSE]` une semaine. C'est le premier
  lot qu'on lâche après la densité Summary.

### W5 : piloter le processus

- **But** : les incidents, les attentes, les manques et les gestes sur un processus qui tourne, dans l'application et en mots.
- **Contenu** :
  - l'incident sur son nœud : la cause, quoi faire, « Try again » sans faux vert, « Skip this step » avec une raison si l'étape
    n'est pas verrouillée, « Stop » ;
  - les attentes distinguées : ce qui attend la personne qui regarde, une minuterie, une autre personne ;
  - le manque : un document attendu, une attente sur un message et une demande à une personne nommée (R96) ; « Provide », « Ask
    someone else » ;
  - la tâche humaine : l'accord avec la signification de la signature, la saisie typée, la liste de contrôle de moins de dix lignes,
    chaque ligne cochée au dossier ;
  - l'ordre des étapes imposé par le moteur (R179) ;
  - les mêmes gestes en mots, par Cortex ; « Waiting for you » liste les tâches humaines du processus, avec « Open on its
    workflow ».
- **Dépend de** : W1, W3 ; W4 pour le brouillon.
- **Fini quand** :
  1. le processus d'E20 joué de bout en bout sur l'app desktop, avec une coupure provoquée, un incident résolu depuis son nœud et un
     document manquant fourni depuis son nœud, le tout au dossier ;
  2. une étape faite hors de l'ordre est refusée par le moteur ;
  3. chaque tâche humaine montre la signification de sa signature, et la signature entre au dossier avec le nom, la date et l'heure ;
  4. la mesure avant et après des erreurs bêtes (Gawande) : deux erreurs semées sur trois missions (le critère 8 de J2), comptées
     avec le processus et sans lui ;
  5. la revue des écrans ; la relecture R159 ; l'essai de la Présidence.
- **Relectures** : R159, R161.
- **Quand** : J2. `[HYPOTHÈSE]` une semaine. Puis la démo (TF-J2-1) et E20 (TF-J2-11).

## Après J2

### W6 : éditer et créer ses workflows

- **But** : les ingénieurs et les PM éditent et créent leurs workflows dans TaskForce ; l'exemple du LIMS ; l'application Documents.
- **Contenu** : le mode « Edit » complet (ajouter, retirer, réordonner, grouper des étapes en blocs, écrire une condition en mots,
  nommer qui répond et qui décide, verrouiller, demander des documents) ; les workflows de l'espace, dérivés d'un défaut ; les
  workflows marqués régulés (deux personnes pour publier, aucun écart de l'IA) ; la signature qui redemande l'identité, si Q20 est
  tranchée ; les deux autres workflows par défaut (la rédaction et la revue d'un document ; le traitement de demandes) ; les agents
  de gestion de projet, avec leurs règles (R94) ; l'application Documents (ce que le projet range, attend et a fait accorder).
- **Dépend de** : W4, W5.
- **Fini quand** : une personne qui ne fait pas de logiciel dérive « rédaction et revue d'un document », ajoute une étape, une
  personne qui décide et une règle en mots, et publie, en quinze minutes au plus ; la Présidence construit son workflow de LIMS (IQ,
  OQ, PQ, les documents de GAMP, une revue au titre de 21 CFR Part 11) sans une ligne de code ; publier un workflow régulé demande
  deux personnes ; les relectures.
- **Relectures** : R159, R161.
- **Quand** : après J2 (J3).

### W7 : exploiter, complet

- **But** : réparer sans repartir de zéro.
- **Contenu** : la modification d'une instance dans un mode préparé (un bandeau, les changements en attente, l'annulation, une revue,
  puis appliquer), avec une raison écrite et un accord ; la migration d'une instance vers une autre version, tout ou rien ; la
  compensation ; relancer depuis une étape en gardant l'original ; les baux et la reprise des exécutions perdues par le serveur ; les
  priorités et le délestage ; les événements du runner sur disque.
- **Dépend de** : W3, W5.
- **Fini quand** : chaque opération entre au dossier avec sa raison et son accord ; une migration passe en entier ou pas du tout ;
  les essais de coupure restent verts ; les relectures.
- **Relectures** : R159, R161.
- **Quand** : après J2 (J5).

### W8 : s'ouvrir

- **But** : se brancher à d'autres outils sans s'enfermer (Q18, Q19).
- **Contenu** : l'import d'un processus de Camunda dans le sous-ensemble ; TaskForce appelée par MCP depuis un processus Camunda ;
  un processus appelable comme un outil (ADR-024) ; le point de décision ouvert à tout moteur d'agents (R99) ; les applications de
  TaskForce comme applications MCP, si Q19 est tranchée.
- **Dépend de** : W2, W5.
- **Fini quand** : un processus Camunda du sous-ensemble importé et joué ; un essai d'attaque sur chaque surface nouvelle (R158) ; la
  relecture.
- **Relectures** : R159.
- **Quand** : après J2 (J5).

### W9 : améliorer

- **But** : où le processus perd du temps, sur la même carte.
- **Contenu** : les durées et les cibles par étape, tirées du dossier ; une bande de temps sous les colonnes ; la ligne de santé du
  projet (On track, At risk, Off track), écrite par la personne qui en répond, Cortex pouvant en préparer le texte.
- **Dépend de** : W5, le dossier.
- **Fini quand** : une étape lente vue sur la carte se retrouve au dossier ; aucune mesure d'agent ni classement (R57) ; la revue des
  écrans.
- **Relectures** : R161.
- **Quand** : après J2 (J7).

## Ce qu'on lâche d'abord, et ce qu'on ne lâche jamais

Si E20 glisse au-delà de la seconde quinzaine de décembre à cause d'un lot du workflow, on lâche, dans cet ordre :

1. la densité Summary : le dirigeant lit l'en-tête de l'objectif ;
2. le brouillon de l'IA (W4) : le processus d'E20 s'écrit à la main dans le sous-ensemble, et la Présidence l'accepte étape par
   étape ;
3. le témoin Operaton : les coupures se jouent sur notre moteur seul.

On ne lâche jamais : le moteur et ses coupures (le critère 6 de J2), les règles sur chaque geste, les données vivantes.

## Où se placent les autres lots de J2

- **TF-J2-7, le dossier signé** : avant W3, comme R170 le demande (le dossier signé et la vue sur les données vivantes d'abord).
- **TF-J2-10, les points de pause** : ce sont les étapes verrouillées du workflow d'E20 (W2), et ses tâches humaines (W4, W5).
- **TF-J2-9, la fiche d'environnement** : chaque étape d'agent la lit ; elle se construit hors de ce plan.
- **TF-J2-3, les agents sur n'importe quel modèle** : l'étape d'agent les appelle ; hors de ce plan.
- **TF-J2-1, la démo, et TF-J2-11, E20** : après W5.

`[HYPOTHÈSE]` L'ordre de grandeur : W0 fini et W1 avec W2 la semaine du 16/11 ; TF-J2-7 puis W3 jusqu'au début de décembre ; W4 et
W5 ensuite ; le processus d'E20 joué, la démo, puis E20 en seconde quinzaine de décembre. La date d'E20 se réécrit ici après W1.
