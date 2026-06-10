---
id: agents-contract
title: Contrat d'Agent — TaskForce Brain OS
doc_type: sop
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [agents, sop, brain-os, kernel]
related:
  - "./Brain_OS.md"
  - "./frameworks/SOP_Developpement.md"
  - "./v1/02-produit/README.md"
---

# 🤖 Contrat d'Agent — Brain OS TaskForce

> **À lire en PREMIER par tout agent (Copilot, Claude…) ouvrant ce vault.** C'est le « kernel » de
> l'OS : comment s'orienter, choisir la prochaine action, et entretenir le système tout seul.

## 0. Rituel de démarrage de session (OBLIGATOIRE)

Quand l'utilisateur dit « go », « on commence », « prochaine action ? » ou ouvre une session de travail,
**exécute ces 4 étapes puis rends compte** (ne code pas encore) :

1. Lire le tableau de bord santé de [`Brain_OS.md`](./Brain_OS.md).
2. Lire le bloc **« ▶ État & prochaine action »** de [`produit/README.md`](./v1/02-produit/README.md).
3. Calculer la **prochaine action** (règle §1) à partir des fiches [`produit/`](./v1/02-produit/README.md) (statuts `[statut::]` + `[prio::]`).
4. Répondre en **3 lignes max** : `État actuel` · `Prochaine action recommandée (ID + 1 phrase)` · `On y va ?`

## 1. Comment choisir la prochaine action

Ordre de priorité, du plus prioritaire au moins :
1. Items `[statut:: broken]` **P0** (réparations — débloquent des pans entiers). Réf : [`.ai/P0-fix-plan.md`](../taskforce-fullstack/.ai/P0-fix-plan.md).
2. Items `P0` puis `P1`, `P2`, `P3` non terminés.
3. Respecter les **dépendances** : un item front avec `[besoin-backend:: BE-xxx]` nécessite que `BE-xxx` soit fait d'abord (ou en parallèle).
4. **Produit avant mémoire** : viser le niveau des outils de référence ([matrice](./v1/02-produit/README.md#2-matrice-de-couverture-fonctionnelle)) avant la rédaction RNCP.
5. Signaler si une action requiert une **décision humaine** (ex. TF-FIX-004/005 : design sécurité/facturation) → ne pas exécuter seul.

## 2. Definition of Done (par tâche)

Une tâche n'est **finie** que si **tout** est vrai :
- [ ] Le code marche **bout-en-bout** (front → endpoint réel, pas de mock).
- [ ] Règles d'or respectées (cf. [SOP](./frameworks/SOP_Developpement.md) §2).
- [ ] Tests ajoutés/maj (viser couverture ≥ 50 %).
- [ ] **Fiche produit mise à jour** : item passé en `[statut:: done]` (ou `wip`).
- [ ] Brain OS mis à jour **si** l'archi/le contrat a changé ([Architecture](./v1/03-architecture/Architecture.md)/[API](./v1/05-api/API.md) + tableau de bord).
- [ ] Changelog mis à jour si visible utilisateur ([Release_Notes](./v1/15-utilisateur/Release_Notes.md)).
- [ ] **Bloc « ▶ Prochaine action » recalculé** dans [`produit/README.md`](./v1/02-produit/README.md).

## 3. Auto-entretien du vault

Après **chaque** tâche, l'agent **maintient le système lui-même** :
- bascule les statuts `[statut::]` des items concernés ;
- si le front crée un besoin backend → ajoute `[besoin-backend:: BE-xxx]` (front) + item miroir `[id:: BE-xxx] [demande-par:: frontend]` (back) ;
- recalcule et réécrit le bloc « ▶ Prochaine action » ;
- propose la tâche suivante à l'utilisateur.

Revue **hebdomadaire** : relire la [matrice de parité](./v1/02-produit/README.md#2-matrice-de-couverture-fonctionnelle) et la fraîcheur des notes (re-vérifier dans le code avant d'affirmer).

## 4. Garde-fous

- **Jamais** de commande / commit / push **sans accord explicite** de l'utilisateur.
- Documenter la **réalité du code**, pas l'intention.
- Réponses **courtes, en français**, propositions claires.
- Respecter les conventions ([Conventions](./v1/04-engineering/Conventions_Documentation.md)) et le [SOP](./frameworks/SOP_Developpement.md).

---

**Points d'entrée :** [🧠 Brain OS](./Brain_OS.md) · [🚧 État Produit](./v1/02-produit/README.md) · [⚙️ SOP](./frameworks/SOP_Developpement.md) · [📋 Backlog](./v1/13-roadmap/Roadmap_Backlog.md)

**Maj :** 09/06/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
