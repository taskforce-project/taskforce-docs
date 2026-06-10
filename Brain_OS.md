---
type: hub
statut: actif
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [brain-os, hub, moc, architecture]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# 🧠 Brain OS — Taskforce

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Hub Brain OS](https://img.shields.io/badge/Type-Brain%20OS-purple?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Source vérifiée: code](https://img.shields.io/badge/Source-code%20v%C3%A9rifi%C3%A9-brightgreen?style=for-the-badge)]()

**Tags :** `#brain-os` `#hub` `#architecture` `#moc`

<p class="lead">
Le <strong>Brain OS</strong> est la mémoire de référence du projet Taskforce : une cartographie
vivante du système, conçue pour être lue d'un seul tenant par un humain comme par un agent IA, afin
de localiser le code et raisonner sur l'impact d'un changement sans re-scanner tout le dépôt.
Ce fichier est le <strong>point d'entrée unique</strong> (Map of Content) vers tous les documents techniques.
</p>

> **Principe fondateur** — Ces documents décrivent **la réalité du code**, pas l'intention. Toute
> divergence entre ce qui est documenté ailleurs et ce que fait le code est signalée et tracée.

## Table des matières

1. [Les 5 documents du noyau](#1-les-5-documents-du-noyau)
2. [Tableau de bord santé](#2-tableau-de-bord-santé)
3. [Comment utiliser ce Brain OS](#3-comment-utiliser-ce-brain-os)
4. [Le dépôt de code](#4-le-dépôt-de-code)
5. [Maintenance](#5-maintenance)

---

## 1. Les 5 documents du noyau

<div class="highlight-box">

| Document | Rôle | Répond à la question |
| -------- | ---- | -------------------- |
| [🏛️ Architecture](./v1/03-architecture/Architecture.md) | Vue globale, topologie, frontend/backend/infra, modèle de données | « Comment le système est-il câblé ? » |
| [🔌 Contrats API](./v1/05-api/API.md) | Mapping service front ↔ controller back, endpoints, incohérences | « Quel appel front touche quel endpoint ? » |
| [🧩 Modules](./v1/03-architecture/Modules.md) | Domaines fonctionnels, dépendances, stores, migrations | « Qui possède cette fonctionnalité ? » |
| [⚠️ Dette technique](./v1/09-audits/Dette_Technique.md) | Bugs, code mort, endpoints manquants, routes cassées, mocks | « Qu'est-ce qui est cassé ou bancal ? » |
| [🔥 Problèmes connus](./v1/09-audits/Problemes_Connus.md) | Triage priorisé : priorité · impact · effort · confiance | « Par quoi commencer ? » |

</div>

**Schémas (PFR) :** [flux complet](./assets/brain-os-flow.html) · [architecture technique](./assets/architecture-technique.html) · [boîte à outils infra/sécurité](./assets/infra-toolchain.html) · [système Brain OS](./assets/brain-os-systeme.html). 🧰 [Catalogue outils](./v1/06-infra/Outils_Infra_Securite.md).

**Pilotage & standard :**
[🤖 Contrat d'Agent (à lire en 1er par une IA)](./AGENTS.md) ·
[⚙️ SOP Développement](./frameworks/SOP_Developpement.md) (procédure de travail) ·
[🚧 État Produit & couverture fonctionnelle](./v1/02-produit/README.md) (fiches par répertoire, réf. croisée FE↔BE) ·
[📋 Backlog / Roadmap technique](./v1/13-roadmap/Roadmap_Backlog.md) ·
[📐 Conventions du vault](./v1/04-engineering/Conventions_Documentation.md) · templates dans [`_templates/`](./templates/Template_Doc_Technique.md).

> **Priorité actuelle = PRODUIT** (atteindre le niveau des outils de référence : Plane, Linear, GitHub…), mémoire RNCP ensuite. Suivi : [`produit/`](./v1/02-produit/README.md).

Documentation projet/métier complémentaire : [Dossier Projet](./v1/01-projet/Dossier_Projet.md) ·
[CdCF](./v1/01-projet/01_CdCF.md) · [CdCT](./v1/01-projet/02_CdCT.md). Doc développeur :
[Architecture (dev)](./v1/04-engineering/ARCHITECTURE.md) · [Git Workflow](./v1/04-engineering/git-workflow/README.md).

### 🎓 Mémoire RNCP (dossier de validation)

Le projet fil rouge alimente le mémoire du titre *Développeur Full Stack*. Sa structure colle au
référentiel (blocs → compétences C1–C32) et la **matrice de couverture** sert de checklist « 100 % ».

- [Hub du mémoire + matrice des 32 compétences](./v1/16-memoire-rncp/README.md)
- [Bloc 1 — Conception & modélisation](./v1/16-memoire-rncp/Bloc1_Conception_Modelisation.md) (C1–C12)
- [Bloc 2 — Front-end](./v1/16-memoire-rncp/Bloc2_Frontend.md) (C13–C20)
- [Bloc 3 — Back-end](./v1/16-memoire-rncp/Bloc3_Backend.md) (C21–C26)
- [Bloc 4 — Déploiement & production](./v1/16-memoire-rncp/Bloc4_Deploiement_Production.md) (C27–C32)

### 👥 Documentation utilisateur

- [Manuel Utilisateur](./v1/15-utilisateur/Manuel_Utilisateur.md) · [Guide d'installation](./v1/15-utilisateur/Guid_Installation.md) · [FAQ](./v1/15-utilisateur/FAQ.md) · [Release Notes](./v1/15-utilisateur/Release_Notes.md)

## 2. Tableau de bord santé

État de chaque domaine fonctionnel **vérifié dans le code au 08/06/2026** (branche `feat/dashboard`).

| Domaine | État | Note |
| ------- | :--: | ---- |
| Auth, Utilisateurs, Workspaces, Projets, Issues, Analytics, Notifications, Labels, Sales, Avatars | ✅ | Opérationnel bout-en-bout |
| Cycles, Teams, Pages (wiki), Discussions, Chat | ❌ | 404 — préfixe `/api` manquant côté backend ([PC-001](./v1/09-audits/Problemes_Connus.md)) |
| Messages, Intégrations (GitHub/Slack/Webhooks), Pièces jointes, Roadmap | ❌ | Constantes de routes front absentes ([PC-002](./v1/09-audits/Problemes_Connus.md)) |
| Profil (page), Refresh token, Webhooks Stripe | ⚠️ | Bugs runtime / handlers stubés |
| Assistant IA (streaming), AI Insights (cache) | ⚠️ | Fonctionnel mais dégradé |
| Service IA Python (`ai-service`) | 💤 | Vestigial — remplacé par Groq-direct en Java |

Détail complet et scoring : [Problèmes connus](./v1/09-audits/Problemes_Connus.md).

## 3. Comment utiliser ce Brain OS

<p class="lead">
Ce vault sert deux publics : les humains (équipe, doc utilisateur à venir) et les agents IA.
</p>

**Pour un humain** — Ouvrir le dépôt comme **vault Obsidian** (la config `.obsidian/` est fournie).
La vue Graphe colore les notes par dossier ; le volet Tags et les Propriétés sont alimentés par le
front-matter YAML de chaque document. Partir de ce hub puis suivre les liens.

**Pour un agent IA** — Lire d'abord les 5 documents du noyau **avant** d'explorer le code : ils
contiennent les chemins de fichiers exacts et les pièges connus. Le dépôt de code embarque aussi une
version compacte anglophone dans `taskforce-fullstack/.ai/` pour Copilot/Claude.

**Pour créer un nouveau document** — Dupliquer [`_templates/Template_Doc_Technique.md`](./templates/Template_Doc_Technique.md),
remplir le front-matter, conserver l'en-tête à badges et le footer, ajouter le lien dans ce hub.

## 4. Le dépôt de code

Le code vit dans le dépôt **frère** [`taskforce-fullstack`](../taskforce-fullstack) (monorepo).
Les chemins cités dans les documents techniques sont **relatifs à la racine de ce monorepo**
(ex. `backend/tf-api/src/main/java/...`, `frontend/lib/api/...`).

| Brique | Stack | Emplacement |
| ------ | ----- | ----------- |
| Backend API | Spring Boot 4.0 · Java 21 | `backend/tf-api/` |
| Frontend | Next.js 16 · React 19 · TS 5 | `frontend/` |
| Landing | Astro 5 | `landing-page/` |
| Service IA | FastAPI · Python 3.12 (vestigial) | `ai-service/` |
| Infra | Docker Compose · PostgreSQL 18 · Keycloak · MinIO · RabbitMQ | racine + `nginx/`, `keycloak/` |

## 5. Maintenance

<blockquote class="important">
<strong>Règle de fraîcheur :</strong> ces documents sont des photographies datées. Avant d'affirmer
un fait (numéro de ligne, comportement), re-vérifier dans le code courant. Mettre à jour la date du
footer et le champ <code>date</code> du front-matter à chaque révision.
</blockquote>

Cadence suggérée : revue à chaque merge sur `dev`, et re-vérification ciblée des [Problèmes connus](./v1/09-audits/Problemes_Connus.md)
après chaque correctif.

---

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
