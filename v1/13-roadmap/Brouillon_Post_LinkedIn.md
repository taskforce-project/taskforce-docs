---
id: brouillon-post-linkedin
title: Brouillon du post LinkedIn (sortie de TaskForce 1.0)
doc_type: brouillon
statut: draft
version: 0.1
date: "19/10/2026"
auteur: Pierre MICHEL
tags: [open-source, release, communication]
related:
  - "./Plan_Release_Open_Source.md"
  - "../03-architecture/Specification_App_Desktop.md"
---

# Brouillon du post LinkedIn (sortie de TaskForce 1.0)

**Date :** 19/10/2026 · **Pour :** le jour des résultats du diplôme (OSS-J.5), publié par le CEO.

Les passages entre crochets sont à compléter : ce sont des faits que seul l'auteur connaît (résultat, remerciements,
ce qu'il retient). Le paragraphe sur l'app desktop est optionnel : à garder seulement si elle est annoncée ce jour-là.
Aucun tiret long, aucune flèche, aucun emoji : le texte doit sonner écrit à la main.

## Version française

Mon projet de fin d'études est en ligne, et il est open source.

TaskForce est un outil de gestion de projet où les personnes et les agents de code travaillent sur les mêmes tickets.
Je l'ai construit pendant mon année de [titre du diplôme, RNCP niveau 6] à la Metz Numeric School. [Résultat.]

Après la soutenance, j'ai regardé le projet honnêtement. Comme produit à vendre, il arrivait sur un marché saturé, où
changer d'outil coûte cher, sans moyen de se faire connaître. Plutôt que de le laisser dormir, je l'ai terminé et je le
publie, sur le modèle de Plane : sous licence AGPL-3.0, à installer chez soi, seul ou en équipe.

Ce qu'il fait :
- On délègue un ticket à Claude Code, qui travaille sur votre ordinateur : on suit chaque action depuis le ticket, on
  autorise ou on refuse ce qui doit l'être, et la pull request arrive à la fin. GitHub Copilot est aussi proposé.
- Le Brain OS garde la connaissance de l'équipe : des pages Markdown liées entre elles, alimentées par GitHub, Slack et
  Plane.
- Cortex, l'assistant, répond à partir de ces pages et des projets, avec l'IA de votre choix : Ollama sur votre machine
  par défaut, ou une API compatible OpenAI.
- GitHub, Slack, Plane, n'importe quel serveur MCP et des webhooks signés pour le reste.

[Ce que je retiens de ce projet, en deux ou trois phrases.]

[Optionnel] La suite : une app desktop. On télécharge, on se connecte avec un compte TaskForce gratuit, et les projets
restent sur sa machine.

Le code : https://github.com/taskforce-project/taskforce-fullstack
La documentation : https://docs.taskforce-project.fr

[Remerciements.]

#opensource #gestiondeprojet #IA

## English version

My final-year project is live, and it is open source.

TaskForce is a project management tool where people and coding agents work on the same issues. I built it during my
[degree, RNCP level 6] at Metz Numeric School. [Result.]

After the defense, I took an honest look at it. As a product to sell, it entered a crowded market where switching
tools is costly, with no way to reach people. Rather than let it sit, I finished it and I am releasing it the way
Plane did: under the AGPL-3.0 license, to run yourself, alone or with a team.

What it does:
- Delegate an issue to Claude Code, which works on your own computer: follow each action from the issue, allow or deny
  what needs it, and get the pull request at the end. GitHub Copilot is available too.
- The Brain OS keeps the team's knowledge: linked Markdown pages, fed by GitHub, Slack and Plane.
- Cortex, the assistant, answers from those pages and the projects, with the AI you choose: Ollama on your machine by
  default, or any OpenAI-compatible API.
- GitHub, Slack, Plane, any MCP server, and signed webhooks for the rest.

[What I take away from this project, in two or three sentences.]

[Optional] Next: a desktop app. Download it, sign in with a free TaskForce account, and your projects stay on your
machine.

Code: https://github.com/taskforce-project/taskforce-fullstack
Docs: https://docs.taskforce-project.fr

[Thanks.]

#opensource #projectmanagement #AI

## Sources des affirmations

| Affirmation | Source |
| --- | --- |
| Constat après la soutenance (marché saturé, coût du changement, pas de canal) | [Plan de release](./Plan_Release_Open_Source.md) §1 |
| Modèle de Plane, AGPL-3.0, auto-hébergeable | Plan de release §2, ADR-014 et ADR-015 |
| Claude Code sur l'ordinateur de la personne, validations, pull request ; Copilot | ADR-018, `taskforce-runner/README.md` |
| Brain OS et ingestion GitHub, Slack, Plane ; Cortex ; Ollama ou API compatible OpenAI | README du dépôt, ADR-017, ADR-019 |
| Intégrations et webhooks signés | ADR-020, doc Fern (Webhooks) |
| App desktop avec compte TaskForce gratuit, projets sur la machine | [Spécification de l'app desktop](../03-architecture/Specification_App_Desktop.md) §10 |
