---
id: recherche-index
title: Laboratoire R&D — Brain OS
doc_type: moc
statut: active
version: 2.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, moc, brain-os, world-model, laboratoire]
related:
  - "./CLAUDE.md"
  - "./Journal.md"
  - "../Brain_OS.md"
  - "../v1/road_to_v2/Moteur_IA_World_Model_OODA.md"
---

# 🔬 Laboratoire R&D — Brain OS

**Version :** 2.0 · **Date :** 31/07/2026 · **Auteur :** Pierre MICHEL

[![Type: Laboratoire R&D](https://img.shields.io/badge/Type-Laboratoire%20R%26D-purple?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Nature: Spéculatif](https://img.shields.io/badge/Nature-Sp%C3%A9culatif-orange?style=for-the-badge)]()

<p class="lead">
Le laboratoire de <strong>réflexion théorique</strong> du Brain OS : world models, formalisme des
états, trajectoires, incertitude, moteur de décision. C'est la <strong>seule zone du vault</strong> où
l'on écrit ce qui <strong>n'est pas encore démontré</strong> — sous discipline stricte.
</p>

> ## ⚠️ Zone spéculative — la charte du labo
>
> Le reste du vault applique « ne rien inventer, uniquement le démontrable »
> ([Conventions](../v1/04-engineering/Conventions_Documentation.md)). **Ici, l'exception est accordée**
> contre trois obligations : **(1)** étiqueter chaque affirmation `[ÉTABLI]` · `[DÉDUIT]` ·
> `[HYPOTHÈSE]` ; **(2)** rien ne sort par copier-coller (vers `v1/` : démontré, ou en tâche, ou en
> ADR) ; **(3)** zéro référence inventée. **Ce dossier n'est pas un livrable de soutenance.**

## Comment travailler ici — le déroulé d'une session

1. Dire « **mode recherche** ». L'agent lit le protocole [`CLAUDE.md`](./CLAUDE.md) et l'applique.
2. Ouvrir le cahier de bord [`Journal.md`](./Journal.md) : où on en était, quel était le prochain coup.
3. Travailler à la bonne **station** (ci-dessous), au format des [`Gabarits.md`](./Gabarits.md).
4. En fin de session : **remplir le Journal** (fait · trouvé · décidé · prochain coup) — sinon la
   session est perdue ([`CLAUDE.md`](./CLAUDE.md) §10).

## La paillasse (racine) — les 5 références toujours ouvertes

| Fichier | Rôle |
| --- | --- |
| [🔬 `README.md`](./README.md) | **Cette carte** : où va quoi, tableau de bord |
| [📋 `CLAUDE.md`](./CLAUDE.md) | **Le protocole** du mode recherche (rôle, méthode, comité, garde-fous) |
| [📓 `Journal.md`](./Journal.md) | **Le cahier de labo** : entrées datées, la mémoire chronologique |
| [🧰 `Gabarits.md`](./Gabarits.md) | Les **formes standard** : fiche axiome / expérience / revue / entrée journal |
| [❓ `Questions-ouvertes.md`](./Questions-ouvertes.md) | Le **tableau** des questions non tranchées (Q1…Q9) |

## Les stations (sous-dossiers) — le travail qui grandit

| Station | Contient | Entrée | Grandit avec |
| --- | --- | --- | --- |
| [📏 `theorie/`](./theorie/) | La **spécification** formelle | [`Axiomes.md`](./theorie/Axiomes.md) (la spec) · [`Modele-mathematique.md`](./theorie/Modele-mathematique.md) (brouillon) | un axiome par fiche, dérivations |
| [🧪 `experiences/`](./experiences/) | Les **tests falsifiables** | [`Experiences.md`](./experiences/Experiences.md) (registre E1–E4) | une fiche de résultat par run |
| [📖 `revues/`](./revues/) | La **critique** des idées entrantes | [`World-Model.md`](./revues/World-Model.md) · [`Ecosysteme.md`](./revues/Ecosysteme.md) | une revue par dump/brainstorm |
| [📚 `references/`](./references/) | La **bibliothèque** | [`Bibliotheque.md`](./references/Bibliotheque.md) | une note de lecture par papier |
| [⚖️ `decisions/`](./decisions/) | Les **ADR en gestation** (avant promotion en `v1/`) | [`ADR-012-DRAFT`](./decisions/ADR-012-DRAFT-brain-os-exposition.md) | un brouillon par décision |

> **Où va quoi, en un mot** : un **axiome** → `theorie/` · un **test** → `experiences/` · un **dump à
> critiquer** → `revues/` · un **papier** → `references/` · une **décision** → `decisions/` · une
> **question** → `Questions-ouvertes.md` · le **récit de la session** → `Journal.md`.

## Tableau de bord

**Le système d'axiomes** ([`theorie/Axiomes.md`](./theorie/Axiomes.md)) — deux couches :

| | Axiomes | État |
| --- | --- | --- |
| **Noyau** (grounded) | A1 état=graphe · A2 Ŝ≠S · A3 rythme `ẋ` | ✅ (A3 : mesuré ✅, validé 🟡) |
| **Frontière** (hypothèses) | A4 dynamique `f` · A5 calibration · A6 potentiel Φ · A7 causalité · A8 trajectoires | ❌/🟡, chacun avec son test |

**Le prochain coup** : `[DÉDUIT]` **A5 (calibration) commande tout** — sans savoir scorer une prédiction,
rien de la frontière ne se ground. → **[E1](./experiences/Experiences.md#e1--nos-prédictions-sont-elles-calibrées-)** (nécessite un passage en mode dev).

**Les 4 contraintes du terrain** ([`CLAUDE.md`](./CLAUDE.md) §3), à opposer avant toute idée :

| # | Contrainte | Conséquence |
| - | --- | --- |
| **C1** | **N ≈ 1** — un seul workspace | Aucun modèle appris (JEPA, MuZero, Dreamer) |
| **C2** | **Monde non rejouable** | Le contrefactuel n'est jamais observable |
| **C3** | **Horloge lente** — 1 cycle = 2 semaines | ~20 points de données par an |
| **C4** | **Réseau contraint, budget ≈ 0** | Ni entraînement, ni fine-tune, ni modèle hosted massif |

## Rattachement au reste du vault

| Document | Lien | Nature |
| --- | --- | --- |
| [`World Model.md`](../World%20Model.md) | Le **brainstorm source** (07→17/07/2026), à la racine du vault | Transcript brut — critiqué dans [`revues/World-Model.md`](./revues/World-Model.md) |
| [`IDEA.md`](../IDEA.md) | Vision « AI Delivery OS » | Produit |
| [Moteur_IA_World_Model_OODA](../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) | **Architecture décidée** (07/07) : world model mémoire/retrieval, sans gradient | ⚠️ Un simulateur mathématique la **contredit** → ADR requis |
| [Data_Flywheel_et_Apprentissage](../v1/road_to_v2/Data_Flywheel_et_Apprentissage.md) | Le flywheel de préférence (F1) | Déjà speccé |
| [`.ai/brain-os-roadmap.md`](../../taskforce-fullstack/.ai/brain-os-roadmap.md) | L'état **réel** du code Brain OS | Source de vérité technique |

---

**Points d'entrée :** [📋 Protocole](./CLAUDE.md) · [📓 Journal](./Journal.md) · [🧠 Brain OS](../Brain_OS.md) · [🤖 AGENTS — mode dev](../AGENTS.md) · [🚀 road_to_v2](../v1/road_to_v2/README.md)

**Dernière mise à jour :** 31/07/2026 · **v2.0** · Projet Taskforce — Metz Numeric School 2025-2026
