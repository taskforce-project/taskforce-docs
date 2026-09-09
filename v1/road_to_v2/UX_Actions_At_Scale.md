---
id: ux-actions-at-scale
title: UX des actions/outils a l'echelle - eviter le dropdown-hell (inspiration Linear)
doc_type: spec
statut: draft
version: 0.1
date: "09/09/2026"
auteur: Pierre MICHEL
tags: [road-to-v2, spec, ux, ui, linear, command-menu]
related:
  - "Agent_Delivery_Pipeline.md"
  - "Connecteurs_et_Catalogue.md"
  - "../02-produit/Frontend.md"
---

# UX des actions/outils a l'echelle

> **Le probleme.** Une issue va accumuler **beaucoup** d'actions et d'outils : déléguer a un agent, lier un repo, brancher un CRM/Slack/Stripe, lancer un workflow, générer une spec... Empiler ça en **dropdowns / boutons visibles** = une liste incalculable, illisible, naze. **Comment gérer sans casser la lisibilité ?** Réponse : on fait comme **Linear** - actions **découvrables a la demande**, pas **affichées en permanence**. On est **ouvert au refactor UI/UX** (D8 de [[Agent_Delivery_Pipeline]]) tant que le **métier ne bouge pas** (sinon on casse la démo Smart Assign).

## Comment Linear gere ça (patrons a reprendre)

| Patron | Principe | Chez nous |
|---|---|---|
| **Command menu (Cmd/Ctrl-K)** | UN point d'entrée **cherchable** vers **toute** action, filtré par le contexte courant. Les actions **vivent dans la palette**, pas dans la barre d'outils. | « Delegate to agent », « Link repo », « Connect tool », « Run workflow », « Generate spec » = entrées de palette, contextualisées a l'issue/au projet sélectionné. |
| **Slash `/` inline** | Dans un champ texte (description, commentaire), `/` insere une action/un bloc. | `/spec`, `/delegate`, `/link-repo` directement dans l'issue. |
| **Mini-picker cherchable** | Chaque propriété (assigné, projet, label, repo, agent) ouvre un **petit popover fuzzy-search**, jamais une liste plate géante. | Le meme composant pour : assigner une **personne**, assigner un **agent** (avec logo), **lier un repo**, **brancher un outil**. Cohérence totale. |
| **Rail de propriétés compact** | Panneau latéral avec les champs **groupés**, seulement les plus utiles visibles ; le reste au clic. | Rail issue : statut, assigné (humain **ou** agent), projet, repo lié, priorité. Le long tail (outils, connecteurs) reste dans la palette. |
| **Menu contextuel groupé** | Clic droit → actions **rangées par catégorie**. | Actions sur l'issue groupées : IA / Intégrations / Board. |
| **Clavier d'abord** | Raccourci mono-touche pour le fréquent ; recents/favoris remontent. | `A` assigner, `S` statut, `D` déléguer... recents en tete de palette. |
| **Progressive disclosure** | Visible = le plus pertinent ; le reste **cherchable**. | L'issue reste **lean** : jamais tous les outils affichés, toujours a portée de recherche. |

## Regle d'or

> **On n'ajoute jamais un dropdown de plus. On ajoute une entrée cherchable.** Quand un nouvel outil/agent arrive (et il y en aura beaucoup), il apparait dans la **palette** et dans les **mini-pickers**, sans alourdir l'écran. L'écran ne grandit pas avec le catalogue ; la **recherche** absorbe la croissance.

## Application au pipeline de délégation

- **Déléguer** = action de palette + le **picker d'assigné inclut les agents** (logos providers). Meme UX que « assigner une personne ».
- **Lier un repo** = action, au **niveau projet** (défaut) **et issue** (surcharge), via picker cherchable - pas un dropdown (cf. [[Agent_Delivery_Pipeline]] §3.3).
- **Brancher un outil** (CRM/Slack/Stripe) = le [[Connecteurs_et_Catalogue|catalogue de connecteurs]] surfacé dans un picker cherchable, jamais des boutons empilés.
- **Choisir le provider/modele** = picker cherchable (reco de notre IA en tete, overridable).

## Garde-fous

- **Métier intact** : on refactore la **surface** (composants de sélection, palette), pas la logique (Smart Assign sémantique, assignation, RBAC restent). D8.
- **Cohérence** : un **seul** composant mini-picker réutilisé partout (personnes, agents, repos, outils) - c'est ce qui rend l'UX « lean mais efficace » de Linear.
- **Accessibilité clavier** obligatoire (la palette est inutile sans).

## Statut

Guide de **conception a prototyper/valider** (patrons Linear connus, non encore implémentés chez nous). A confronter au design system existant ([[../02-produit/Frontend.md]]) avant build.
