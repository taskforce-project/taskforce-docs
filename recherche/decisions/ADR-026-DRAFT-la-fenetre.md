---
id: adr-026-la-fenetre
title: "ADR-026 (à promouvoir) : la fenêtre, la conversation dans le shell et la page de la route dans un volet"
doc_type: adr
statut: active
version: 1.0
date: "07/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, frontend, fenetre, conversation, volets, cortex, conseil]
related:
  - "../conseil/seances/2026-11-05-atelier-fenetre.md"
  - "../conseil/seances/2026-10-30-atelier-ecrans-base.md"
  - "../../v1/02-produit/Frontend.md"
  - "../../v1/13-roadmap/Roadmap_Backlog.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-026 (à promouvoir) : la fenêtre, la conversation dans le shell et la page de la route dans un volet

> **Décidé à la séance n°18 du Conseil (05/11/2026, R119 à R126), validé d'avance par la Présidence.** Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 026 dès que
> l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 05/11/2026. Lot 1 construit le 07/11/2026 (TF-J1-9, branche `feat/window-lot1`, PR #493) ; les lots 2 et 3
suivent sous la même décision.

## Contexte

- `[ÉTABLI]` Avant la fenêtre, `AppShell` (`frontend/components/layout/app-shell.tsx`) posait une barre de navigation à
  gauche, une barre du haut (fil d'Ariane, recherche, cloche, thème, bouton d'AI Workflows), une page par route dans
  un `<main>` animé à chaque changement d'adresse, les panneaux d'AI Workflows qui glissaient par-dessus, et la barre
  unique en bas (R76), d'où la conversation avec Cortex se dépliait au-dessus de l'écran, sur un dégradé (décision du
  02/11/2026).
- `[ÉTABLI]` La Présidence, le 05/11/2026, après son test de la 1.10.0 : « full chat avec un endroit ou justement on
  peut voir les interfaces [...] Comme si on avait finalement integre un board dans CLaude Desktop [...] Et evidemment
  pouvoir tout de mm call le chat quand on est sur les board ». Le test montrait aussi la barre hors d'atteinte quand
  une fiche d'issue était ouverte.
- `[ÉTABLI]` La séance n°18 (atelier de la fenêtre) adopte la fenêtre de Claude Code avec l'identité de TaskForce
  (R119), les écrans en volets (R120), le travail et ses conversations à gauche (R121), ce qui entoure la conversation
  à droite (R122), et ce qui quitte l'écran (R124). Elle construit en trois lots.
- `[ÉTABLI]` Le même build sert la webapp et l'app desktop (Electron) ; Next.js (App Router) rend la page de la route
  comme `children` du layout.

## Décision

1. **Une fenêtre** : `[barre de gauche] [conversation] [volet] [zone de droite]`, sous une ligne de 44 px qui remplace
   la barre du haut ; la même dans la webapp et dans l'app desktop, où cette ligne déplace la fenêtre.
2. **La conversation vit dans le shell.** `AppShell` la rend, la même d'une route à l'autre ; son état reste dans
   `useCortexStore`. Elle tient sa colonne (720 px de texte au plus, centrée, le compositeur en bas) ; quand le volet
   prend toute la largeur, et sous `lg`, elle se replie dans le compositeur, en bas du volet, et sa réponse se déplie
   au-dessus (le motif du 02/11/2026, gardé).
3. **Le volet est la page de la route.** `AppShell` rend `children` dans l'emplacement du volet ; la route dit quel
   volet est ouvert (`paneOf`, `lib/window/pane.ts`) ; l'accueil de l'espace (`/{slug}`) n'a pas de volet, seule la
   conversation s'y montre. Fermer le volet mène à cet accueil ; la pleine largeur se retient pour la personne. Il n'y a
   plus d'animation entre les pages. L'emplacement reste générique : les lots suivants y ouvrent l'issue, la vue du
   travail d'une mission, « Progress ».
4. **Les deux bords lisent ce que l'app tient déjà.** La barre de gauche et la zone de droite lisent les stores
   existants (projets, conversations, missions, notifications, intégrations, état de l'IA), tenus à jour depuis le
   shell. Une seule donnée s'ajoute : le projet où une conversation commence (`ai_conversation.project_id`, V118),
   pour la ranger sous lui.
5. **Ce qui quitte l'écran part avec son code** : la barre du haut, la cloche, le sélecteur de thème, les panneaux
   d'AI Workflows et leur store, les sous-menus de la barre de gauche.

## Alternatives considérées

- **Garder les pages, avec la conversation en surimpression (l'état d'avant).** La conversation et l'écran se
  disputaient la même place : dépliée, elle cachait le bas de l'écran ; une fiche par-dessus la page la mettait hors
  d'atteinte. La Présidence demandait l'inverse : la conversation au centre, l'écran à côté. Écartée, sauf en pleine
  largeur et sous `lg`, où ce motif reste celui de la conversation repliée.
- **Une route dédiée à la conversation (`/{slug}/chat`).** Deux endroits pour la même chose : on quitte le tableau pour
  parler à Cortex, et Cortex ne voit plus ce qu'on regardait. C'est le contraire de « pouvoir call le chat quand on est
  sur les board ». Écartée.
- **Des volets tenus dans un store, sans la route.** La séance n°18 veut que chaque état de la fenêtre ait son adresse,
  et que le bouton retour marche (R120). Écartée : la route reste la source, les adresses s'étendent au lot 2.

## Conséquences

- Chaque page s'affiche dans un volet de largeur variable (480 px au moins à côté de la conversation) ; une page qui
  supposait toute la largeur l'obtient d'un clic. Sous 1 600 px, ouvrir un volet replie la zone de droite ; rouverte à
  la main, elle prend sur le volet.
- L'en-tête du volet et celui de la page se répètent tant que les pages ne deviennent pas des volets (lot 2).
- L'app desktop dessine 52 px en haut (la marge de 8 px et la ligne de 44 px) ; les boutons de Windows s'y posent.
- Les gestes faits sur leurs cartes (une issue préparée puis créée, une action accordée) sont gardés par
  `useCortexStore` pour « Changes », et « Undo » y a un seul état pour un même geste. L'archivage ou la suppression
  depuis la carte de suppression n'y entrent pas encore : la carte garde son résultat pour elle.
- Les tests suivent la fenêtre : la logique dans `lib/window`, le store de la fenêtre, les composants de la fenêtre ;
  les tests des composants retirés partent avec eux.

## Ce qui reste ouvert (lots 2 et 3)

- La poignée du volet et sa largeur retenue ; l'issue en volet par-dessus le tableau, avec un retour, à la place de la
  fiche ; la vue du travail d'une mission ; la conversation et le volet dans l'adresse.
- L'arrivée (ce qui attend, trois suggestions), le volet « Progress », la ligne grise sous chaque réponse, le retrait du
  tour guidé.

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Séance n°18](../conseil/seances/2026-11-05-atelier-fenetre.md)

**Dernière mise à jour :** 07/11/2026 · **v1.0** · Projet Taskforce
