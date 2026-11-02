---
id: adr-024-mcp-taskforce-surface-unique
title: "ADR-024 (à promouvoir) : le MCP TaskForce, une seule surface d'outils pour Cortex et pour tout agent"
doc_type: adr
statut: active
version: 1.0
date: "02/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, mcp, cortex, agents, chat, regles, modeles]
related:
  - "../conseil/seances/2026-11-01-feuille-de-route.md"
  - "../conseil/seances/2026-11-01-revue-j0.md"
  - "../../v1/13-roadmap/Roadmap_Backlog.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-024 (à promouvoir) : le MCP TaskForce, une seule surface d'outils pour Cortex et pour tout agent

> **Décidé par la Présidence le 02/11/2026.** Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 024 dès que
> l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 02/11/2026. Les premiers gestes se construisent en J1 (TF-J1-5), la couverture se mesure à chaque jalon
(TF-J1-6).

## Contexte

- `[ÉTABLI]` Deux surfaces d'outils existent, chacune avec sa liste :
  - Cortex, l'agent de l'app, a ses propres outils (8 au 02/11/2026 : créer un projet, une note, préparer une issue,
    chercher dans le Brain OS, lister les projets et les issues, trouver une intégration, et les outils des services
    connectés) ;
  - le serveur MCP de l'instance sert les agents extérieurs (Claude Code par le runner, le plugin `/taskforce`) avec une
    autre liste, qui sait déjà modifier une issue, la commenter et cocher sa checklist.
- `[ÉTABLI]` Les deux passent par la même table de règles : en Java pour Cortex, dans le runner pour Claude Code
  (R90, à l'essai), avec les mêmes cas partagés.
- `[ÉTABLI]` La passerelle de modèles en Java (TF-J1-2) donne à Cortex n'importe quel modèle : Ollama, une API compatible
  OpenAI, l'API d'Anthropic.
- `[ÉTABLI]` R95 (séance n°15) : l'assistant agit sur chaque surface « par les mêmes gestes que la personne, sous les
  mêmes règles », et ses actions entrent au dossier.
- `[ÉTABLI]` La Présidence, le 02/11/2026 : « l'UX je suis convaincu que ca doit passer par le chat en fait globalement,
  donc donner a nos agent ollama claude ou n'importe quel agent au final, le MCP taskforce finalement qui serait
  nativement utilisable, avec regles et tout le bazare, mais de toute facon le MCP taskforce sera le mm pour l agent
  interne que lea gent externe en fait c 'est ca qui est cool, on est pas dependant des models ».

## Décision

1. **Une seule surface d'outils : le MCP TaskForce.** Cortex s'en sert dans le backend, au nom de la personne, avec le
   modèle qu'elle a choisi ; les agents extérieurs s'en servent par le serveur MCP, dans le périmètre de leur session.
2. **Un geste s'ajoute une fois** : un outil MCP et la classe d'action que la table de règles juge. Il sert aussitôt à
   Cortex comme à Claude Code ou à tout autre agent.
3. **Les mêmes règles partout** : chaque appel est jugé par la table, quel que soit l'agent ou le modèle. Ce qui
   s'annule se fait, avec « Undo » ; ce qui ne s'annule pas se demande ; tout entre au dossier.
4. **La présentation reste propre à chaque client** : dans la conversation, Cortex montre des cartes (l'issue préparée,
   « Undo », la demande d'accord) ; un agent extérieur reçoit le résultat en texte.
5. **Un accord se donne par un bouton**, sur la carte de la demande, y compris dans la conversation. Jamais par un « oui »
   écrit que le modèle interpréterait : un texte piégé pourrait le faire croire (R1).

## Conséquences

- Les outils propres à Cortex passent sur la surface MCP, en gardant leurs comportements : la carte de l'issue préparée,
  la question quand le projet ou la personne est ambigu, « Undo ».
- La couverture du chat se mesure : l'inventaire des gestes de l'app, et la part que le chat sait faire (TF-J1-6).
- Un petit modèle ne reçoit pas tous les outils : la table des capacités de la passerelle (R113) choisit ceux qu'il peut
  tenir, comme la réduction des outils sur un refus 400 ou 413 le fait déjà.
- Le texte d'un outil (description, schéma) devient un contrat public, lu par n'importe quel modèle : il se relit comme
  une API.

## Ce qui reste ouvert

- Le chemin de Cortex vers les outils : un appel dans le processus du backend, ou le même serveur MCP en local. À
  trancher sur la mesure de E16 (l'aller-retour) et sur la simplicité.
- Les gestes qui touchent les réglages de l'espace (membres, intégrations, règles) : ils viennent avec leurs surfaces (J2,
  J3), sous la même décision.

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Feuille de route](../../v1/13-roadmap/Roadmap_Backlog.md)

**Dernière mise à jour :** 02/11/2026 · **v1.0** · Projet Taskforce
