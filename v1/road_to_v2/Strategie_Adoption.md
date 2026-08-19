---
id: strategie-adoption
title: Stratégie d'adoption — intégration-first (v2 / positionnement)
doc_type: note
statut: parked
version: 1.0
date: "07/07/2026"
auteur: Pierre MICHEL
tags: [strategie, adoption, positionnement, go-to-market, v2]
related:
  - "README.md"
  - "../../IDEA.md"
---

# Stratégie d'adoption — intégration-first (⏸ park pour v2 / positionnement)

> Insight go-to-market. **Pas un chantier PFR** — mais la note à garder pour le positionnement.

## Le vrai risque : le *switching cost*
Demander à une équipe de **quitter Linear/Asana/Notion/Jira** = bataille perdue d'avance (« tout marche déjà »), même si le produit est meilleur.

## La bonne approche : **s'intégrer, pas remplacer**
```
GitHub ┐
Linear ┼──► Brain OS (couche d'intelligence)
Notion ┤
Slack  ┘
```
L'équipe **garde ses outils**. Le Brain OS :
- lit tickets / Git / docs → construit le knowledge graph,
- propose specs / PRD / **prompts Claude Code**.
→ L'utilisateur **ne change presque rien**. (Comme Cursor : « garde VS Code, + IA ».)

Puis, progressivement, on ajoute **Brain Issues / Roadmap / Kanban** — les gens adoptent tes vues **parce qu'elles sont meilleures** (modèle Notion).

## Repositionnement le plus fort : **PM = une vue de la connaissance**
```
Knowledge (décisions, archi, contexte, roadmap, risques)
        ↓  projections
Kanban · Timeline · Sprint · Gantt · Graph
```
On ne remplace pas un gestionnaire de tickets : **les tickets deviennent une projection de la connaissance.** Subtil, mais ça change tout le positionnement.

## La question produit à répondre
> **Pourquoi installer Brain OS demain SANS quitter Linear ?**
Réponse forte = une **capacité qu'ils n'ont pas** (l'IA comprend leur projet mieux que n'importe quel outil). Le reste (Kanban/roadmap) suit.

## Lien avec l'existant (les seeds sont là)
Nos **intégrations GitHub/Slack + miroir** = déjà le *wedge d'intégration*. Le Brain OS = déjà la couche de connaissance. → cette stratégie n'est pas un pivot de plus, c'est la **suite naturelle**.
