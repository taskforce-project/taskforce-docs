---
id: produit-couverture-chat
title: Couverture du chat
doc_type: register
statut: active
version: 1.0
date: "02/11/2026"
auteur: Pierre MICHEL
review_cycle: per-milestone
tags: [produit, chat, cortex, mcp, couverture, j1]
related:
  - "./README.md"
  - "./Backend.md"
  - "./Frontend.md"
  - "../05-api/API.md"
  - "../13-roadmap/Roadmap_Backlog.md"
  - "../../recherche/decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Couverture du chat

**Version :** 1.0 · **Date :** 02/11/2026 · **Auteur :** Pierre MICHEL

[![Type: Registre](https://img.shields.io/badge/Type-Registre-orange?style=for-the-badge)]() [![Jalon: J1](https://img.shields.io/badge/Jalon-J1-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit](./README.md) · [Fiche Backend](./Backend.md) · [Fiche Frontend](./Frontend.md) · [API](../05-api/API.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [ADR-024](../../recherche/decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md)

**Tags :** `#produit` `#chat` `#cortex` `#mcp` `#couverture`

<p class="lead">
L'inventaire des gestes de l'app, surface par surface, et la part que le chat sait faire (TF-J1-6, critère de sortie
n°6 de J1). La Présidence, le 02/11/2026 : l'UX passe par le chat, et le MCP TaskForce est la seule surface d'outils,
la même pour Cortex et pour un agent extérieur (ADR-024).
</p>

## Table des matières
1. [Le chiffre](#1-le-chiffre)
2. [Ce qui compte comme un geste](#2-ce-qui-compte-comme-un-geste)
3. [Les gestes, par surface](#3-les-gestes-par-surface)
4. [Ce que le chat fait, et comment](#4-ce-que-le-chat-fait-et-comment)
5. [Hors de l'inventaire](#5-hors-de-linventaire)
6. [Tenir l'inventaire à jour](#6-tenir-linventaire-à-jour)

---

## 1. Le chiffre

| Date | Outils de Cortex | Gestes que le chat fait | Gestes de l'app | Part |
| --- | :--: | :--: | :--: | :--: |
| 02/11/2026, avant TF-J1-5 | 8 | 9 | 155 | 6 % |
| 02/11/2026, avec TF-J1-5 (`taskforce-fullstack` #480) | 13 | 31 | 155 | 20 % |

- Les 8 outils d'avant (`core/service/agent/tools/*` et les outils des services connectés) couvraient 9 gestes :
  `list_issues` en couvre deux (les issues d'un projet ou d'une colonne, et les miennes).
- TF-J1-5 ajoute 5 gestes du MCP TaskForce (`update_issue`, `add_comment`, `delegate_issue`, `get_mission`,
  `delete_issue`) et les cartes de la mission dans la conversation : 22 gestes de plus.
- Le chiffre se lit avec les surfaces : le chat couvre les issues et les missions, presque rien des réglages. ADR-024
  le prévoit : les gestes des réglages de l'espace (membres, intégrations, règles) viennent avec leurs surfaces, en J2
  et J3.

## 2. Ce qui compte comme un geste

- **Un geste** est ce qu'une personne fait dans l'app et qui change quelque chose (créer, changer, déplacer, supprimer,
  accorder, appliquer), ou une lecture qui porte une décision (où en est une mission, chercher une note).
- Un geste peut toucher plusieurs routes (changer le cycle d'une issue : la retirer d'un cycle, l'ajouter à un autre),
  et une route peut porter plusieurs gestes (`PATCH /issues/{id}` porte le titre, la colonne, l'assigné...). L'inventaire
  compte les gestes, pas les routes.
- **Le chat sait le faire** (✅) quand la personne l'obtient depuis la conversation, de sa phrase au résultat : un outil
  que Cortex appelle, jugé par les règles de l'espace et gardé au dossier de la réponse, ou une carte de la
  conversation dont la personne clique le bouton. ❌ : il faut passer par l'écran. « MCP » : un agent extérieur le fait
  par le serveur MCP de l'instance, Cortex pas encore.

## 3. Les gestes, par surface

Sources : les routes des contrôleurs (`backend/tf-api/src/main/java/com/taskforce/tf_api/**/*Controller.java`, 272 routes
dont 174 qui écrivent, le 02/11/2026) et les actions des stores du front (`frontend/lib/store/*.ts`), sur les écrans de
`frontend/app/(protected)/[workspace]/`.

### 3.1 Lire (6 sur 8)

| Geste | Route | Chat |
| --- | --- | :--: |
| Lister les projets | `GET /projects` | ✅ `list_projects` |
| Lister les issues d'un projet ou d'une colonne | `GET /projects/{id}/issues` | ✅ `list_issues` (filtre par colonne, lue comme sur le tableau) |
| Mes issues | `GET /my-issues` | ✅ `list_issues` (`mine`, ou sans filtre) |
| Lire une issue en entier (description, checklist, fil) | `GET /projects/{id}/issues/{issueId}` et ses sous-routes | ❌ (MCP : `get_issue`) |
| Où en est une mission | `GET /delivery/issues/{issueId}/run`, `GET /delivery/runs/{runId}/activity` | ✅ `get_mission`, cartes de la mission |
| Les indicateurs de l'espace | `GET /analytics/kpis` | ❌ (MCP : `workspace_kpis`) |
| Chercher dans les notes | `POST /brain/search` | ✅ `search_brain` |
| Trouver une intégration | `GET /integrations/catalog` | ✅ `find_integration` |

### 3.2 Issues : tableau, liste, fiche (13 sur 36)

| Geste | Route | Chat |
| --- | --- | :--: |
| Créer une issue | `POST /projects/{id}/issues` | ✅ `create_issue` : carte préparée, la personne la crée |
| Changer le titre | `PATCH /projects/{id}/issues/{issueId}` | ✅ `update_issue`, Undo |
| Changer la description | `PATCH` (idem) | ✅ `update_issue`, Undo |
| Changer la priorité | `PATCH` (idem) | ✅ `update_issue`, Undo |
| Déplacer dans une autre colonne | `PATCH` (`statusId`) | ✅ `update_issue` (`status` par son nom), Undo |
| Assigner, retirer l'assigné | `PATCH` (`assigneeId`, `unassign`) | ✅ `update_issue` (« moi », un nom, « none »), Undo |
| Ajouter ou retirer des labels | `PATCH` (`labelIds`) | ✅ `update_issue` (`addLabels`, `removeLabels`), Undo |
| Estimer en points | `PATCH` (`storyPoints`) | ✅ `update_issue`, Undo |
| Poser ou retirer l'échéance | `PATCH` (`dueDate`, `clearDueDate`) | ✅ `update_issue`, Undo |
| Mettre dans un cycle, l'en sortir | `POST`, `DELETE /projects/{id}/cycles/{cycleId}/issues` | ✅ `update_issue` (`cycle`), Undo |
| Changer la date de début | `PATCH` (`startDate`) | ❌ |
| Changer le type | `PATCH` (`typeId`) | ❌ |
| Changer le parent | `PATCH` (`parentId`) | ❌ |
| Ranger dans la colonne (glisser) | `PATCH` (`position`) | ❌ |
| Archiver | `PATCH .../archive` | ✅ carte de suppression (« Archive », puis Undo) |
| Désarchiver | `PATCH .../unarchive` | ❌ (seul l'Undo de la carte, juste après) |
| Épingler | `PATCH .../pin` | ❌ |
| Supprimer | `DELETE /projects/{id}/issues/{issueId}` | ✅ `delete_issue` : demandé, la carte dit ce qui part, « Delete » |
| Commenter | `POST .../comments` | ✅ `add_comment`, Undo |
| Modifier un commentaire | `PATCH .../comments/{commentId}` | ❌ |
| Supprimer un commentaire | `DELETE .../comments/{commentId}` | ❌ (seul l'Undo du commentaire de Cortex) |
| Ajouter une ligne de checklist | `POST .../checklist` | ❌ (à la création seulement, sur la carte) |
| Cocher une ligne | `PATCH .../checklist/{itemId}` | ❌ (MCP : `check_checklist_item`) |
| Supprimer une ligne | `DELETE .../checklist/{itemId}` | ❌ |
| Lier deux issues | `POST .../relations` | ❌ |
| Délier | `DELETE .../relations/{relationId}` | ❌ |
| Noter du temps passé | `POST .../worklogs` | ❌ |
| Retirer un temps noté | `DELETE .../worklogs/{worklogId}` | ❌ |
| Joindre un fichier | `POST .../attachments` | ❌ |
| Retirer une pièce jointe | `DELETE .../attachments/{attachmentId}` | ❌ |
| Générer une spécification | `POST .../ai/spec` | ❌ |
| Approuver la spécification | `POST .../ai/spec/approve` | ❌ |
| Smart Assign : une recommandation | `POST .../smart-assign` | ❌ (MCP : `smart_assign`) |
| Smart Assign en masse | `POST /issues/smart-assign/preview`, `/bulk` | ❌ |
| Accepter une assignation | `POST /api/me/assignments/{issueId}/accept` | ❌ |
| Refuser une assignation | `POST /api/me/assignments/{issueId}/decline` | ❌ |

### 3.3 Missions : confier une issue à un agent (9 sur 9)

| Geste | Route | Chat |
| --- | --- | :--: |
| Confier à Claude Code | `POST /delivery/issues/{issueId}/delegate` | ✅ `delegate_issue` : demandé, « Approve and run » |
| Refuser une demande de l'agent | `POST /delivery/runs/{runId}/approvals/{approvalId}` | ✅ carte de la demande, « Refuse » |
| Accorder (une fois, ou pour la mission) | `POST` (idem, `forMission`) | ✅ carte de la demande, « Allow » ou « Allow for this mission » |
| Appliquer le résultat | `POST /delivery/runs/{runId}/apply` | ✅ carte de résultat, « Apply » |
| Appliquer malgré des tests en échec, avec une raison | `POST .../apply` (`reason`) | ✅ carte de résultat, « Apply anyway » |
| Écarter le résultat | `POST .../discard` | ✅ carte de résultat, « Discard » |
| Relancer avec une remarque | `POST .../retry` | ✅ carte de résultat, « Try again » |
| Terminer sans changement | `POST .../done` | ✅ carte de résultat, « Mark as done » |
| Télécharger le dossier | `GET .../evidence?format=json\|md` | ✅ cartes de la mission |

### 3.4 Colonnes d'un projet (0 sur 4)

Créer, modifier, supprimer, réordonner les colonnes (`POST`, `PATCH`, `DELETE /projects/{id}/issues/statuses`,
`POST .../statuses/reorder`) : ❌.

### 3.5 Projets (1 sur 17)

| Geste | Route | Chat |
| --- | --- | :--: |
| Créer un projet | `POST /projects` | ✅ `create_project`, Undo |
| Modifier un projet (nom, description, statut, dates, responsable, visibilité) | `PATCH /projects/{id}` | ❌ |
| Archiver, supprimer | `POST .../archive`, `DELETE /projects/{id}` | ❌ ❌ |
| Ajouter, retirer un membre | `POST`, `DELETE .../members` | ❌ ❌ |
| Créer, modifier, supprimer un label | `POST`, `PUT`, `DELETE .../labels` | ❌ ❌ ❌ |
| Rattacher, détacher une équipe | `POST`, `DELETE .../teams` | ❌ ❌ |
| Mettre en favori | `POST`, `DELETE .../favorite` | ❌ |
| Lier, délier un dépôt de code | `PUT`, `DELETE .../repo` | ❌ ❌ |
| Poser la commande de test | `PUT .../repo/test-command` | ❌ |
| Importer, exporter un projet | `POST /projects/import`, `GET .../export` | ❌ ❌ |

### 3.6 Cycles (0 sur 3)

Créer, modifier (dates, démarrage, clôture), supprimer un cycle (`/projects/{id}/cycles`) : ❌.

### 3.7 Brain OS (1 sur 5)

| Geste | Route | Chat |
| --- | --- | :--: |
| Écrire une note | `POST /brain/nodes` | ✅ `create_note`, Undo |
| Modifier, déplacer, supprimer une note | `PATCH /brain/nodes/{id}`, `PATCH .../move`, `DELETE` | ❌ ❌ ❌ |
| Déposer un fichier | `POST /brain/files` | ❌ |

### 3.8 Intelligence, analyses et tableau de bord (0 sur 15)

Lancer une analyse, répondre à sa question, l'écarter (`/analysis`) ; accepter, épingler, écarter, modifier une priorité
(`/priorities/{id}`) ; générer, enregistrer, supprimer un graphique, explorer une répartition (`/analytics/chart`,
`/analytics/charts`, `/analytics/breakdown`) ; ajouter, modifier, supprimer, réordonner une carte du tableau de bord
(`/dashboard-cards`) : ❌.

### 3.9 Membres et équipes (0 sur 15)

Inviter, révoquer une invitation, accepter une invitation, changer un rôle, retirer un membre ; déclarer, retirer une
absence ; modifier les compétences, les faire suggérer ; créer, modifier, supprimer une équipe, y ajouter, en retirer un
membre ; répartir à nouveau le travail (`/redistribute/apply`) : ❌.

### 3.10 Intégrations (1 sur 20)

| Geste | Route | Chat |
| --- | --- | :--: |
| Lancer l'action d'un outil connecté | `POST /mcp/actions/execute` | ✅ outils des services connectés, une écriture accordée sur sa carte par un propriétaire ou un administrateur |
| GitHub : connecter, déconnecter, synchroniser, lier une PR ou un commit à une issue, retirer le lien | `/integrations/github/**` | ❌ (5) |
| Slack : connecter, ajouter, retirer un canal, déconnecter, synchroniser | `/integrations/slack/**` | ❌ (5) |
| Plane : connecter, déconnecter, synchroniser | `/integrations/plane/**` | ❌ (3) |
| Connecter un serveur MCP (catalogue ou personnalisé) | `/integrations/mcp/**` | ❌ |
| Webhooks : créer, modifier, supprimer, régénérer le secret, envoyer un test | `/webhooks/**` | ❌ (5) |

### 3.11 Espace (0 sur 5)

Créer, modifier, supprimer, importer un espace ; fournir un runner (Réglages, Agents, `POST /api/delivery/runners`) : ❌.

### 3.12 Boîte de réception (0 sur 5)

Marquer une notification lue, toutes lues, en prendre acte, toutes ; régler ses préférences : ❌.

### 3.13 Compte (0 sur 13)

Modifier son profil, son avatar ; poser, retirer la double authentification ; enregistrer, supprimer une passkey ; créer,
révoquer un jeton personnel ; autoriser, révoquer une session de l'app desktop ; supprimer, restaurer son compte ; finir
l'accueil : ❌. Ces gestes touchent la personne elle-même et restent à l'écran.

## 4. Ce que le chat fait, et comment

- **Une seule surface d'outils** (ADR-024) : un geste est un outil du MCP TaskForce (`TaskforceMcpTools`) qui porte
  l'action que la table de règles juge (`McpTool.action`). Cortex s'en sert dans le backend, au nom de la personne
  (`forCortex`, `CortexMcpTool`) ; Claude Code et les autres agents, par le serveur MCP de l'instance, dans le périmètre
  de leur session. Le runner nomme la même action (`taskforce-runner/src/harness/facts.ts`).
- **Les mêmes règles** : chaque appel de Cortex est jugé par `CortexGate` sur cette action, et gardé au dossier de la
  réponse.
- **Ce qui se défait se fait d'emblée, avec Undo (R77)** : un changement d'issue garde ses anciennes valeurs, un
  commentaire son id ; Undo les remet tant que personne n'a rien changé depuis, et nomme son geste (`ref`).
- **Ce qui ne se défait pas se demande** : confier une issue (une mission part sur la machine de la personne),
  supprimer une issue (la règle `delete-issue`). La carte de la suppression propose d'abord d'archiver.
- **Une décision est un clic sur le bouton d'une carte (R1)** : répondre à une demande d'une mission, trancher son
  résultat, accorder une action. Aucun outil ne décide à la place de la personne, et un « oui » écrit n'accorde rien.
- **Des noms, pas des ids** : la personne et Cortex nomment l'issue par sa clé (« TF-12 », « HR-1372-2 »), la colonne,
  la personne (« moi ») et le cycle par leurs noms ; une issue nommée par sa colonne ou son titre se trouve par
  `list_issues`.

## 5. Hors de l'inventaire

- **La plomberie** : connexion, inscription, mots de passe, OAuth, passkeys et connexion de l'app desktop
  (`/api/auth/**`), routes du runner (`/api/delivery/runner/**`, `/api/auth/runner/token`), journaux du client
  (`/api/logs/client`), le serveur MCP lui-même (`/mcp`).
- **Le chat lui-même** : poser une question, ses conversations, accorder ou défaire une action de Cortex, faire d'une
  réponse un cas de la banque d'évaluations.

## 6. Tenir l'inventaire à jour

1. **À chaque geste ajouté au chat** : l'outil MCP avec son action dans `TaskforceMcpTools` (et dans `CORTEX` si Cortex
   s'en sert), sa ligne dans `facts.ts` pour le runner, puis la ligne de ce tableau passe à ✅ avec l'outil ou la carte,
   et le chiffre du §1 se recompte.
2. **À chaque nouvelle route** : la liste des routes se relit (`rg -n "@(Get|Post|Put|Patch|Delete)Mapping"
   backend/tf-api/src/main/java --glob "*Controller.java"`, 272 le 02/11/2026) ; une route qui écrit est un geste
   nouveau, ou la part d'un geste déjà là. Les actions des stores du front (`frontend/lib/store/*.ts`) disent comment
   l'écran le fait.
3. **À chaque jalon** : le chiffre entre dans les critères de sortie du jalon ([feuille de route](../13-roadmap/Roadmap_Backlog.md)),
   comme pour J1 (critère n°6).
4. Un geste ne passe à ✅ que fait de bout en bout depuis la conversation, sous les règles et au dossier ; vérifié par un
   test, et sur la pile de dev avec un modèle local quand il dépend du modèle.

---

**Points d'entrée :** [🚧 État Produit](./README.md) · [📋 Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [ADR-024](../../recherche/decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md)

**Dernière mise à jour :** 02/11/2026 · **v1.0** · Projet Taskforce
