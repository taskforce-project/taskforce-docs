---
id: recherche-index
title: R&D — Recherche
doc_type: moc
statut: active
version: 1.0
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, moc, brain-os, world-model]
related:
  - "./CLAUDE.md"
  - "../Brain_OS.md"
  - "../v1/road_to_v2/Moteur_IA_World_Model_OODA.md"
---

# 🔬 R&D — Recherche

**Version :** 1.0 · **Date :** 17/07/2026 · **Auteur :** Pierre MICHEL

[![Type: Recherche](https://img.shields.io/badge/Type-R%26D-purple?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Nature: Spéculatif](https://img.shields.io/badge/Nature-Sp%C3%A9culatif-orange?style=for-the-badge)]()

**Tags :** `#recherche` `#brain-os` `#world-model`

<p class="lead">
Espace de <strong>réflexion théorique</strong> sur le moteur de décision du Brain OS : world models,
formalisme des états, trajectoires, incertitude. C'est la seule zone du vault où l'on a le droit
d'écrire ce qui <strong>n'est pas encore démontré</strong> — sous conditions strictes.
</p>

> ## ⚠️ Zone spéculative — lire avant d'écrire ici
>
> Le reste du vault applique la règle d'or **« ne rien inventer, uniquement le démontrable »**
> ([Conventions](../v1/04-engineering/Conventions_Documentation.md)). **Ici, l'exception est
> accordée** — en échange de trois obligations :
>
> 1. **Étiqueter chaque affirmation** : `[ÉTABLI]` · `[DÉDUIT]` · `[HYPOTHÈSE]`. Sans marqueur, une
>    phrase est lue comme établie — c'est ainsi qu'une doc se met à mentir.
> 2. **Rien ne sort d'ici par copier-coller.** Vers `v1/` : uniquement **démontré** (code + mesure),
>    ou en **tâche** ([Backlog](../v1/13-roadmap/Roadmap_Backlog.md)), ou en **ADR**
>    ([Décisions](../v1/12-decisions/Journal_Decisions_ADR.md)).
> 3. **Zéro référence inventée.** Certain, ou marqué « à vérifier ».
>
> **Ce dossier n'est pas un livrable de soutenance.** La priorité au 17/07/2026 reste la clôture V1.

## Comment s'en servir

Dire « **mode recherche** ». L'agent lit [`CLAUDE.md`](./CLAUDE.md) et applique le contrat : posture
de chercheur, contre-exemples systématiques, falsification obligatoire, comité de 5 experts, cinq
altitudes d'analyse.

## Les fichiers

| Fichier | Rôle | Question à laquelle il répond |
| --- | --- | --- |
| [🤖 `CLAUDE.md`](./CLAUDE.md) | **Contrat d'agent** du mode recherche : rôle, méthode, garde-fous | « Comment on réfléchit ici ? » |
| [📐 `Mathematical_Model.md`](./Mathematical_Model.md) | Le formalisme candidat : objets, opérateurs, trajectoires | « Quels objets manipule le moteur ? » |
| [📖 `World_Model_Notes.md`](./World_Model_Notes.md) | Notes de lecture critiques sur le corpus source | « Qu'est-ce qui tient, qu'est-ce qui casse ? » |
| [❓ `Open_Questions.md`](./Open_Questions.md) | Registre des questions non tranchées | « Sur quoi on bloque ? » |
| [🧪 `Experiments.md`](./Experiments.md) | Registre des hypothèses **falsifiables** + protocole | « Comment on saurait qu'on a tort ? » |
| [📚 `References.md`](./References.md) | Bibliothèque mentale — cadres réels, vérifiés | « Qui a déjà résolu ça ? » |

> **Pas de `Vision.md`** — volontaire. La vision produit vit déjà dans [`IDEA.md`](../IDEA.md) et
> [`v1/road_to_v2/`](../v1/road_to_v2/README.md). La dupliquer ici créerait une **deuxième source de
> vérité**, exactement ce que les règles du vault interdisent.

## Rattachement au reste du vault

| Document | Lien | Nature |
| --- | --- | --- |
| [`World Model.md`](../World%20Model.md) | Le **brainstorm source** (07→17/07/2026) | Transcript brut, non structuré — critiqué dans [`World_Model_Notes.md`](./World_Model_Notes.md) |
| [`IDEA.md`](../IDEA.md) | Vision « AI Delivery OS » | Produit |
| [Moteur_IA_World_Model_OODA](../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) | **Architecture déjà décidée** (07/07) : world model mémoire/retrieval, sans gradient, couplé OODA | ⚠️ Toute proposition de simulateur mathématique la **contredit** → ADR requis |
| [`.ai/brain-os-roadmap.md`](../../taskforce-fullstack/.ai/brain-os-roadmap.md) | L'état **réel** du code Brain OS | Source de vérité technique |

## État du terrain — les 4 contraintes qui tranchent

Détaillées dans [`CLAUDE.md`](./CLAUDE.md) §3. À opposer à toute idée **avant** de la formaliser :

| # | Contrainte | Conséquence |
| - | --- | --- |
| **C1** | **N ≈ 1** — un seul workspace d'historique | Aucun modèle appris (JEPA, MuZero, Dreamer) n'est applicable |
| **C2** | **Monde non rejouable** | Le contrefactuel n'est jamais observable |
| **C3** | **Horloge lente** — 1 cycle = 2 semaines | ~20 points de données par an, au mieux |
| **C4** | **Réseau contraint, budget ≈ 0** | Ni entraînement, ni fine-tune, ni modèle hosted massif |

---

**Points d'entrée :** [🧠 Brain OS](../Brain_OS.md) · [🤖 AGENTS — mode dev](../AGENTS.md) · [🚀 road_to_v2](../v1/road_to_v2/README.md) · [📐 Conventions](../v1/04-engineering/Conventions_Documentation.md)

**Dernière mise à jour :** 17/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
