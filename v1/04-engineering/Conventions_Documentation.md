---
id: conventions-documentation
title: Conventions du Vault de Documentation
doc_type: reference
status: active
owner: pierre
created: "08/06/2026"
updated: "08/06/2026"
review_cycle: quarterly
tags: [technique, conventions, brain-os, obsidian]
related:
  - "../../Brain_OS.md"
  - "../../templates/Template_Doc_Technique.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Conventions du Vault — Brain OS

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Inspiré de: Plania Vault](https://img.shields.io/badge/Inspir%C3%A9-Plania%20Vault-purple?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Template technique](../../templates/Template_Doc_Technique.md)
- [Backlog / Roadmap technique](../13-roadmap/Roadmap_Backlog.md)

**Tags :** `#technique` `#conventions` `#brain-os` `#obsidian`

<p class="lead">
Ce document définit le standard du vault, inspiré du « documentation operating system » de Plania,
adapté au contexte TaskForce (dépôt lisible sur GitHub <em>et</em> dans Obsidian, et servant de mémoire
RNCP). L'objectif : un vault navigable par un humain comme par une IA, où chaque note est typée, datée,
reliée et traçable.
</p>

## Table des matières

1. [Front-matter standard](#1-front-matter-standard)
2. [Taxonomie `doc_type`](#2-taxonomie-doc_type)
3. [Taxonomie des tags](#3-taxonomie-des-tags)
4. [Identifiants normalisés](#4-identifiants-normalisés)
5. [Liens & navigation](#5-liens--navigation)
6. [Cycle de vie & contribution](#6-cycle-de-vie--contribution)
7. [Obsidian — config recommandée](#7-obsidian--config-recommandée)

---

## 1. Front-matter standard

Chaque note **doit** porter ce front-matter YAML (alimente Propriétés, volet Tags, recherche, et le RAG IA) :

```yaml
---
id: slug-unique-kebab-case
title: Titre lisible
doc_type: reference|moc|register|adr|runbook|sop|memoire-rncp|documentation-utilisateur|audit
statut: draft|active|archived
version: X.Y
date: "JJ/MM/AAAA"
auteur: Pierre MICHEL
review_cycle: monthly|quarterly|annual
tags: [domaine, sous-domaine]
related:
  - "../../technique/chemin/vers/note.md"
---
```

L'en-tête visuel (commentaire logos + badges shields + footer) du
[template](../../templates/Template_Doc_Technique.md) est **conservé** sous le front-matter pour le rendu
GitHub et le jury. Le front-matter sert Obsidian/IA ; les badges servent l'humain/jury.

## 2. Taxonomie `doc_type`

| `doc_type` | Usage | Exemple |
| ---------- | ----- | ------- |
| `moc` | Hub / carte de contenu | [Brain_OS](../../Brain_OS.md) |
| `reference` | Doc technique de référence | [Architecture](../03-architecture/Architecture.md), ce fichier |
| `register` | Registre vivant (suivi) | [Dette technique](../09-audits/Dette_Technique.md), [Backlog](../13-roadmap/Roadmap_Backlog.md) |
| `adr` | Décision d'architecture | `_templates/TPL_ADR.md` |
| `runbook` | Procédure opérationnelle | `_templates/TPL_Runbook.md` |
| `sop` | Procédure standard | — |
| `audit` / `finding` | Audit / constat | `_templates/TPL_Finding.md` |
| `memoire-rncp` | Pièce du dossier de validation | [Mémoire](../16-memoire-rncp/README.md) |
| `documentation-utilisateur` | Doc utilisateur finale | [Manuel](../15-utilisateur/Manuel_Utilisateur.md) |

## 3. Taxonomie des tags

Tags **hiérarchiques** (catégorie/sous-catégorie), jamais isolés sans contexte :
`technique`, `frontend`, `backend`, `infrastructure`, `securite`, `tests`, `rgpd`, `memoire`, `rncp`,
`bloc1`…`bloc4`, `utilisateur`. Préfixer par domaine pour filtrer dans le graphe Obsidian.

## 4. Identifiants normalisés

Pour la traçabilité (et pour pointer depuis le code / les commits) :

| Préfixe | Objet | Source |
| ------- | ----- | ------ |
| `DT-xxx` | Élément de dette technique | [Dette technique](../09-audits/Dette_Technique.md) |
| `PC-xxx` | Problème connu (triage) | [Problèmes connus](../09-audits/Problemes_Connus.md) |
| `TF-<AREA>-xxx` | Tâche du backlog (FE/BE/LP/INFRA/SEC/TEST/RGPD/DOC) | [Backlog](../13-roadmap/Roadmap_Backlog.md) |
| `Cxx` / `Exx` | Compétence / livrable RNCP | [Mémoire](../16-memoire-rncp/README.md) |
| `ADR-xxxx` | Décision d'architecture | dossier `adr/` (à créer) |

## 5. Liens & navigation

<blockquote class="important">
<strong>Choix assumé vs Plania :</strong> Plania utilise des <code>[[wikilinks]]</code>. Ici on garde
les <strong>liens markdown relatifs</strong> <code>[texte](../../technique/chemin.md)</code> car le dépôt est aussi lu
sur GitHub (où les wikilinks ne fonctionnent pas) et sert de livrable. Obsidian gère parfaitement les deux
(config <code>useMarkdownLinks: true</code>). Chaque note remonte vers son hub via un lien « Liens rapides ».
</blockquote>

## 6. Cycle de vie & contribution

- **Patch** (corrige/précise) : éditer en place, bump `date` + footer.
- **Minor** (ajoute une section/note) : idem + mettre à jour le hub et `related`.
- **Major** (restructure/contredit l'existant) : créer un `ADR-xxxx`, puis appliquer.
- **Archivage** : ne pas supprimer — déplacer vers `archive/` avec suffixe `-AAAA-MM`.
- **Commits** : `docs(scope): description` (cf. [copilot-instructions](../../../taskforce-fullstack/.github/copilot-instructions.md)).
- **Fraîcheur** : re-vérifier dans le code avant d'affirmer ; les notes sont datées.

## 7. Obsidian — config recommandée

Le dossier `.obsidian/` est fourni (graphe coloré par dossier, templates, liens markdown). Pour atteindre
le niveau « Plania », installer ces plugins communautaires (Obsidian → Paramètres → Plugins tiers) :

| Plugin | Usage |
| ------ | ----- |
| **Templater** | Templates dynamiques (`_templates/`) |
| **Dataview** | Tableaux de bord dynamiques (registres, backlog) |
| **Obsidian Git** | Auto-commit/push du vault |
| **Kanban** | Vue Kanban du [Backlog](../13-roadmap/Roadmap_Backlog.md) |
| **Excalidraw** | Diagrammes (archi, déploiement, MCD) |
| **Smart Connections** | Recherche sémantique / RAG IA |

> Une liste pré-remplie est fournie dans `.obsidian/community-plugins.json` (Obsidian proposera de les installer).

---

> **Note Brain OS** — Standard appliqué progressivement aux notes existantes (tâche `TF-DOC-002` du
> [Backlog](../13-roadmap/Roadmap_Backlog.md)).

**Dernière mise à jour :** 08/06/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
