---
id: adr-012-brain-os-exposition
title: "ADR-012 (BROUILLON) — Brain OS : moteur interne, produit-connaissance exposé"
doc_type: adr
statut: proposed
version: 0.1
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, brain-os, exposition, moteur, recherche, draft]
related:
  - "./Open_Questions.md"
  - "./Ecosystem_Notes.md"
  - "../v1/road_to_v2/Moteur_IA_World_Model_OODA.md"
  - "../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-012 (BROUILLON) — Brain OS : moteur interne, produit-connaissance exposé

> ⚠️ **BROUILLON de recherche, en quarantaine.** Ce n'est **pas** encore une décision. Il répond à
> [Q6](../Questions-ouvertes.md#q6--le-brain-os-est-invisible--que-montre-t-on-alors-). Une fois **ratifié
> par Pierre**, il est **promu** dans [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md)
> sous le n° **ADR-012** (l'index s'arrête à 010 mais **ADR-011 existe déjà** dans le corps → 012 est
> le prochain libre). Tant qu'il vit ici, il n'a **aucune autorité**.

## Statut
`proposed` (brouillon) — en attente de décision humaine.

## Contexte

`[ÉTABLI]` **Trois sources se contredisent** sur ce que l'utilisateur doit voir du Brain OS :

1. **[Moteur_IA_World_Model_OODA](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §7 (07/07/2026)** a
   **décidé** : *« le Brain OS est le moteur ; l'utilisateur voit la route, jamais le moteur. »* Rien
   d'exposé : ni embeddings, ni délibérations d'agents, ni écarts de prédiction.
2. **Le code livré (Phases 3 / 4ter)** expose au contraire une **UI Brain OS riche** : explorateur
   2-panneaux, graphe force-directed avec régions par projet, éditeur, recherche sémantique. `[ÉTABLI]`
3. **La vision `World Model.md` + le dump écosystème** vont plus loin encore : ils veulent **montrer**
   `Decision Engine → Compare trajectories → Decision Support`, des scénarios chiffrés avec probabilités.

`[DÉDUIT]` Trois réponses incompatibles à « qu'expose-t-on ? » coexistent dans le vault. C'est
exactement le cas que les [Conventions](../../v1/04-engineering/Conventions_Documentation.md) §6 imposent
de trancher par un ADR. Sans décision, on ne sait pas quoi démontrer en soutenance ni quoi construire.

## Décision (proposée)

**Séparer le _produit-connaissance_ (exposé) du _moteur de raisonnement_ (interne).**

- **Exposé** — la **connaissance** comme objet produit : le graphe de notes (ADR, SOP, rétros, specs),
  l'explorateur, l'éditeur, la recherche sémantique, les régions par projet. C'est **F2** (la mémoire
  organisationnelle, [`Ecosystem_Notes.md`](../revues/Ecosysteme.md) §3), et c'est **déjà livré**.
- **Interne, jamais exposé brut** — le **moteur** : embeddings, croyances $B_t$ et leurs confidences,
  trajectoires simulées, écarts prédit/réel, délibérations multi-agents, scores de routing.
- **L'explicabilité passe par des objets produit dérivés**, pas par le moteur : au point
  human-in-the-loop, l'utilisateur voit une **décision + résumé + risques + sources**, pas l'arbre de
  simulation qui l'a produite. Ces objets ont leur propre cycle de vie (spec, doc, checklist).

> Formule : **la connaissance est un produit ; le raisonnement est un moteur.** road_to_v2 §7 avait
> raison sur le *moteur*, mais confondait « moteur » et « connaissance » — l'UI livrée expose la
> **seconde**, ce qui est légitime, sans exposer le **premier**.

## Alternatives considérées

| Option | Avantages | Inconvénients |
| --- | --- | --- |
| **A — Moteur ET connaissance invisibles** (road_to_v2 §7 littéral) | Moat maximal ; cohérent avec « voir la route, pas le moteur » | **Contredit le code livré** (UI Brain OS Phases 3/4ter) ; jette un travail réel et démontrable en soutenance |
| **B — Connaissance exposée, moteur interne** *(retenue)* | Réconcilie l'UI livrée avec le principe §7 ; protège le moat (F3/croyances cachés) ; démontrable | Renonce au « wow » de montrer des futurs simulés |
| **C — Tout exposé, y compris scénarios/probabilités** (vision écosystème) | Effet « waouh » en démo | Montre un **raisonnement à moitié cuit** ; les probabilités ne sont **pas calibrées** (E1) ; risque de fuite inter-workspace ; vend **F3** (le flywheel le plus faible) |

## Conséquences

**Positives**
- Récit cohérent et **déjà démontrable** (l'UI existe) pour la soutenance.
- Moat protégé : la partie non défendable (simulateur/croyances, cf. C1–C2) reste cachée — donc son
  **inexistence actuelle n'est pas un trou visible**.
- Aligne l'exposition sur **F2** (le vrai moat) et non **F3** (la prédiction fragile).

**Négatives / risques**
- Le « comparateur de trajectoires » du dump écosystème est **hors produit** tant que le moteur n'est
  pas calibré (E1). `[DÉDUIT]` Ce n'est pas une perte réelle : montrer des futurs non calibrés serait
  activement trompeur (cf. [`World_Model_Notes.md`](../revues/World-Model.md) §4).
- Frontière à tenir dans le code : un endpoint qui renverrait une confidence brute ou une trajectoire
  viole l'ADR. → garde-fou de revue.

## Plan de déploiement

1. **Décision humaine requise** (Pierre) : valider l'option B, ou trancher autrement.
2. Si B : **promouvoir** ce fichier en ADR-012 dans le journal, mettre à jour son index (qui oublie
   déjà 011), et marquer Q6 `tranchée`.
3. Ligne de revue : aucun endpoint n'expose `B_t`, trajectoires, écarts, scores de routing.

## Liens
- [❓ Q6](../Questions-ouvertes.md#q6--le-brain-os-est-invisible--que-montre-t-on-alors-) · [📖 Ecosystem_Notes §5](../revues/Ecosysteme.md)
- [🧠 Brain OS](../../Brain_OS.md) · [Journal ADR](../../v1/12-decisions/Journal_Decisions_ADR.md) · [Moteur_IA_World_Model_OODA §7](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md)

---

**Brouillon v0.1** · 31/07/2026 · Projet Taskforce — Metz Numeric School 2025-2026
