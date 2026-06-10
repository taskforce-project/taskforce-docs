---
id: produit-ia
title: État Produit — IA
doc_type: register
statut: active
version: 0.1
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, ia, groq]
related:
  - "./README.md"
  - "./Backend.md"
---
<!-- Logo établissement : assets/images/logo_metz_numeric_school.svg | Logo projet : assets/images/logo_taskforce.png -->

# État Produit — IA (`ai-service/` + Groq)

**Version :** 0.1 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: IA](https://img.shields.io/badge/R%C3%A9pertoire-IA-blue?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [Fiche Backend](./Backend.md) · [🧠 Brain OS](../../Brain_OS.md)

**Tags :** `#produit` `#ia` `#groq`

> Prod : Groq direct depuis le backend Java (`GroqService`). `ai-service` Python = **vestigial**.
> Légende : ✅ `done` · 🔄 `wip` · ⬜ `todo`. Atout différenciant (➕ au-delà du standard).

## Existant
- [x] Smart Assign (pré-filtre Java + scoring Groq, repli) [id:: IA-SA-001] [statut:: done] [parite:: extra] [ref:: core/service/SmartAssignService.java]
- [x] Assistant IA (chat contextualisé) [id:: IA-AS-001] [statut:: wip] [parite:: extra]
- [x] AI Insights (analytics) [id:: IA-IN-001] [statut:: wip] [parite:: extra]

## À faire
- [ ] Vrai streaming SSE de l'assistant [id:: IA-AS-002] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-001] (PC-009)
- [ ] Cache Insights (`ai_runs`/`insight_snapshots`) + garde quota/timeout Groq [id:: IA-IN-002] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-002] (PC-007)
- [ ] Feature flags IA [id:: IA-CFG-001] [statut:: todo] [prio:: P2] [besoin-backend:: BE-IA-003] (PC-014)
- [ ] Décision `ai-service` Python : supprimer ou documenter legacy [id:: IA-LEG-001] [statut:: todo] [prio:: P3] [besoin-backend:: BE-IA-004] (PC-012)

---
**Dernière mise à jour :** 09/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
