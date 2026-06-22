---
id: produit-frontend
title: État Produit — Frontend
doc_type: register
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, frontend]
related:
  - "./README.md"
  - "./Backend.md"
  - "../05-api/API.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# État Produit — Frontend (`frontend/`)

**Version :** 1.0 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: frontend](https://img.shields.io/badge/R%C3%A9pertoire-frontend-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [Fiche Backend](./Backend.md) · [Contrats API](../05-api/API.md) · [🧠 Brain OS](../../Brain_OS.md)

**Tags :** `#produit` `#suivi` `#frontend`

<p class="lead">
Stack : Next.js 16 (App Router) · React 19 · TS 5 strict · Tailwind 4 · shadcn/Radix · Zustand · Axios ·
TipTap · STOMP. Légende : ✅ <code>done</code> · 🔄 <code>wip</code> · ⬜ <code>todo</code> · ❌ <code>broken</code>.
Les items <code>[besoin-backend:: BE-xxx]</code> renvoient à une tâche de la <a href="./Backend.md">fiche Backend</a>.
</p>

## Table des matières
1. [Plateforme & socle](#1-plateforme--socle)
2. [Auth & compte](#2-auth--compte)
3. [Workspaces / Projets / Membres](#3-workspaces--projets--membres)
4. [Work items (issues)](#4-work-items-issues)
5. [Cycles / Roadmap](#5-cycles--roadmap)
6. [Modules / Views / Layouts](#6-modules--views--layouts-gaps-plane)
7. [Collaboration (chat, discussions, pages)](#7-collaboration-chat-discussions-pages)
8. [Notifications / Analytics / IA](#8-notifications--analytics--ia)
9. [Intégrations / Pièces jointes](#9-intégrations--pièces-jointes)
10. [Qualité (tests, a11y, perf, sécurité)](#10-qualité-tests-a11y-perf-sécurité)

---

## 1. Plateforme & socle

**Fait :**
- [x] App Router + groupes de routes (protected/auth/payment) [id:: FE-CORE-001] [statut:: done] [parite:: ok] [ref:: frontend/app]
- [x] Client Axios (bearer JWT, refresh-on-401, mapping erreurs) [id:: FE-CORE-002] [statut:: done] [parite:: ok] [ref:: frontend/lib/api/client.ts]
- [x] Stores Zustand par domaine [id:: FE-CORE-003] [statut:: done] [parite:: ok] [ref:: frontend/lib/store]
- [~] **Socle de panneaux** (gauche/droite, empilables, redimensionnables, façon Claude/Cloudflare) — `panel-store` + `PanelDock` + 1er conso Assistant (bouton « Ask AI ») [id:: FE-CORE-006] [statut:: wip] [parite:: extra] [ref:: frontend/lib/store/panel-store.ts + components/layout/panel-dock.tsx] (PROD-8.9 v1, 20/06/2026 — reste : migrer issue-sheet, persistance largeur, mobile)
- [x] i18n FR/EN (constants) [id:: FE-CORE-004] [statut:: wip] [parite:: ok] [ref:: frontend/lib/constants_*]
- [x] Verrou menu « coming soon » — entrées non livrées non cliquables (Agents, Discussions) [id:: FE-CORE-005] [statut:: done] [parite:: extra] [ref:: frontend/components/layout/sidebar/app-sidebar.tsx] (PROD-1.1, 20/06/2026)
- [x] Déclarer les 4 groupes de routes (MESSAGE/INTEGRATION/ATTACHMENT/ROADMAP) [id:: FE-CORE-010] [statut:: done] [parite:: ok] [ref:: frontend/lib/config/api-routes.ts] — vérifié présent 20/06/2026 (ex-PC-002)

**À faire :**
- [ ] Corriger import `profile-service` (`./client`) [id:: FE-CORE-011] [statut:: broken] [prio:: P0] [ref:: frontend/lib/api/profile-service.ts] (PC-003)
- [ ] Aligner la séquence refresh token [id:: FE-CORE-012] [statut:: todo] [prio:: P1] [besoin-backend:: BE-AUTH-001] [ref:: frontend/lib/api/client.ts] (PC-004)
- [ ] Compléter i18n sur toutes les vues [id:: FE-CORE-013] [statut:: todo] [prio:: P2]

## 2. Auth & compte

**Fait :**
- [x] Inscription 3 étapes + OTP, login, forgot-password [id:: FE-AUTH-001] [statut:: done] [parite:: ok] [ref:: frontend/app/auth]
- [x] Choix de plan + retour paiement Stripe [id:: FE-AUTH-002] [statut:: done] [parite:: extra] [ref:: frontend/app/payment]

**À faire :**
- [x] Gestion d'abonnement self-service (Stripe Customer Portal — bouton « Gérer la facturation ») [id:: FE-AUTH-010] [statut:: done] [parite:: extra] [ref:: lib/api/stripe-service.ts openBillingPortal] (PROD-4.5, 20/06/2026)

## 3. Workspaces / Projets / Membres

**Fait :**
- [x] CRUD workspaces, membres, rôles, settings [id:: FE-WS-001] [statut:: done] [parite:: ok] [ref:: frontend/lib/store/workspace-store.ts]
- [x] CRUD projets, membres, labels, statuts custom, archivage [id:: FE-PRJ-001] [statut:: done] [parite:: ok] [ref:: frontend/lib/store/project-store.ts]
- [x] Profil de compétences membre (saisie skills + expertise, alimente Smart Assign — trou CDC #1) [id:: FE-SKILL-001] [statut:: done] [parite:: extra] [prio:: P1] [besoin-backend:: BE-SKILL-001] [ref:: frontend/components/members/member-skills-card.tsx] (PROD-1.2, 20/06/2026)

**À faire :**
- [ ] **Recherche & invitation façon GitHub** : ~5 propositions (avatar+username+email), multi-sélection, rôle ; invite projet → confirmation ajout workspace + option team (existante/nouvelle) [id:: FE-WS-011] [statut:: todo] [parite:: gap] [prio:: P2] [besoin-backend:: BE-WS-011] (PROD-3.4)
- [ ] Templates de projet [id:: FE-PRJ-010] [statut:: todo] [parite:: gap] [prio:: P3] [besoin-backend:: BE-PRJ-010]
- [ ] Rôle GUEST / accès externes [id:: FE-WS-010] [statut:: todo] [parite:: gap] [prio:: P3] [besoin-backend:: BE-WS-010]

## 4. Work items (issues)

**Fait :**
- [x] CRUD issues, statuts (Kanban), types, priorités, labels [id:: FE-ISS-001] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/[id]/issues]
- [x] Commentaires, activité, relations (onglet Relations : ajout/suppression liens) [id:: FE-ISS-002] [statut:: done] [parite:: ok] (relations UI : PROD-2.2, 20/06/2026)
- [x] Smart Assign (panel IA) — **mis en avant** (CTA + auto-ouvert) **+ « wow » v1** : pourquoi (raison Groq + skills qui matchent) + breakdown de score [id:: FE-ISS-003] [statut:: done] [parite:: extra] [ref:: frontend/components/smart-assign] (PROD-1.4/8.10, 20/06/2026)
- [x] Smart Assign **à la création** d'issue (bouton « Suggest assignee » + best match/alternatives dans le modal) [id:: FE-ISS-004] [statut:: done] [parite:: extra] [prio:: P1] [besoin-backend:: BE-SA-001] [ref:: frontend/components/dialogs/create-issue-dialog.tsx] (PROD-1.3, 20/06/2026)
- [x] **Multi-assign** : dialog « Auto-assign (N) » (toolbar board) → recommande + assigne en lot les issues non assignées [id:: FE-ISS-005] [statut:: done] [parite:: extra] [prio:: P1] [besoin-backend:: BE-SA-001] [ref:: frontend/components/dialogs/bulk-assign-dialog.tsx] (PROD-1.9, 20/06/2026)

**À faire :**
- [x] Hiérarchie sous-issues (onglet Sub-tasks : liste enfants + quick-add) [id:: FE-ISS-010] [statut:: done] [parite:: ok] [ref:: components/sheets/issue-sheet.tsx] (PROD-2.1, 20/06/2026)
- [x] Onglets issue-sheet : Relations (PROD-2.2) + Checklist avec % (PROD-2.3) [id:: FE-ISS-020] [statut:: done] [parite:: ok] [ref:: components/sheets/issue-sheet.tsx] (20/06/2026)
- [x] Supprimer une issue (en-tête issue-sheet + confirmation) [id:: FE-ISS-021] [statut:: done] [parite:: ok] (PROD-2.4, 20/06/2026)
- [x] Cycles clarifiés (explication + indice cycle vide) [id:: FE-CYC-010] [statut:: done] [parite:: ok] (PROD-2.5, 20/06/2026)
- [x] Filtres avancés câblés sur List + Backlog (en plus du board) [id:: FE-VIEW-010] [statut:: done] [parite:: ok] (PROD-2.6, 20/06/2026)
- [x] Bascule d'onglets projet instantanée : `fetchIssues` cache-first par projet (`loadedProjectId`) [id:: FE-VIEW-011] [statut:: done] [parite:: ok] [ref:: lib/store/issue-store.ts] (PROD-2.7, 20/06/2026)
- [x] Nettoyage UI dashboard/sidebar : retrait bandeau « operational » + badge « critical », scrollbar discrète, « New project » → modal (`?new=1`) [id:: FE-UI-010] [statut:: done] [parite:: ok] (PROD-8.2/8.6/8.7, 20/06/2026)
- [x] Danger zones en rouge (variante `danger` sur SectionCard, façon GitHub) [id:: FE-UI-012] [statut:: done] [parite:: ok] (20/06/2026)
- [x] Agents marqués « AI · » (page agents + dashboard) ; modals create-issue/project repassés en `modal` (overlay+focus-trap) ; `EditProjectDialog` (édition infos globales) [id:: FE-UI-011] [statut:: done] [parite:: ok] (PROD-8.4/8.5/2.10, 20/06/2026)
- [ ] Estimates (points) sur l'issue + agrégat [id:: FE-ISS-011] [statut:: todo] [parite:: gap] [prio:: P1] [besoin-backend:: BE-ISS-011]
- [ ] Time tracking / worklogs [id:: FE-ISS-012] [statut:: todo] [parite:: gap] [prio:: P3] [besoin-backend:: BE-ISS-012]
- [ ] Bulk actions (multi-sélection) [id:: FE-ISS-013] [statut:: todo] [parite:: gap] [prio:: P2]
- [ ] Brancher « Create issue » de la command palette [id:: FE-ISS-014] [statut:: todo] [prio:: P3] [ref:: frontend/components/command-palette.tsx] (PC-013)

## 5. Cycles / Roadmap

**À faire / cassé :**
- [ ] Réparer l'accès Cycles (route `/api`) [id:: FE-CYC-001] [statut:: broken] [parite:: ok] [prio:: P0] [besoin-backend:: BE-CYC-001] (PC-001)
- [ ] Burndown/vélocité par cycle dans l'UI [id:: FE-CYC-002] [statut:: todo] [parite:: ok] [prio:: P2] [besoin-backend:: BE-CYC-002]
- [ ] Réparer Roadmap (constante `ROADMAP_ROUTES`) [id:: FE-ROAD-001] [statut:: broken] [prio:: P0] (PC-002)
- [ ] Vue Gantt/Timeline complète [id:: FE-ROAD-002] [statut:: todo] [parite:: partial] [prio:: P2] [besoin-backend:: BE-ROAD-002]

## 6. Modules / Views / Layouts (GAPS Plane)

**À faire (gaps majeurs de parité) :**
- [ ] **Modules** : regroupement de features (UI CRUD + rattachement d'issues) [id:: FE-MOD-001] [statut:: todo] [parite:: gap] [prio:: P1] [besoin-backend:: BE-MOD-001]
- [ ] **Views** : filtres/tri/affichage sauvegardés et partagés [id:: FE-VIEW-001] [statut:: todo] [parite:: gap] [prio:: P1] [besoin-backend:: BE-VIEW-001]
- [ ] Layout **Calendrier** [id:: FE-VIEW-002] [statut:: todo] [parite:: gap] [prio:: P2]
- [ ] Layout **Tableur (spreadsheet)** éditable [id:: FE-VIEW-003] [statut:: todo] [parite:: gap] [prio:: P2]
- [ ] **Intake** : boîte de réception/triage de demandes [id:: FE-INTK-001] [statut:: todo] [parite:: gap] [prio:: P2] [besoin-backend:: BE-INTK-001]

## 7. Collaboration (chat, discussions, pages)

**À faire / cassé :**
- [ ] Réparer Chat (route `/api` + `MESSAGE_ROUTES`) puis retirer le mock [id:: FE-CHAT-001] [statut:: broken] [parite:: extra] [prio:: P0] [besoin-backend:: BE-CHAT-001] (PC-001/002/011)
- [ ] Réparer Discussions (route `/api`) [id:: FE-DISC-001] [statut:: broken] [parite:: extra] [prio:: P0] [besoin-backend:: BE-DISC-001] (PC-001)
- [ ] Réparer Pages/wiki (route `/api`) [id:: FE-PAGE-001] [statut:: broken] [parite:: ok] [prio:: P0] [besoin-backend:: BE-PAGE-001] (PC-001)
- [ ] Réparer Teams + compléter `team-store` [id:: FE-TEAM-001] [statut:: broken] [parite:: extra] [prio:: P1] [besoin-backend:: BE-TEAM-001] (PC-001/006)
- [x] Teams : emoji/couleur à la création + Manage/Settings consolidé (« Gérer l'équipe ») [id:: FE-TEAM-010] [statut:: done] [parite:: ok] (PROD-3.6, 20/06/2026) ; reste assoc team↔opération (PROD-3.6b)

## 8. Notifications / Analytics / IA

**Fait :**
- [x] Inbox/notifications (mentions, assignations, alertes) [id:: FE-NOTIF-001] [statut:: done] [parite:: ok]
- [x] Dashboard analytics (KPIs, burndown, throughput, capacité) [id:: FE-ANA-001] [statut:: done] [parite:: ok]
- [x] AI Insights + Assistant (FAB/command palette) [id:: FE-IA-001] [statut:: wip] [parite:: extra]
- [x] **Board temps réel** : hook `useProjectRealtime` (STOMP `/topic/projects.{id}`) patche le store en direct [id:: FE-RT-001] [statut:: done] [parite:: extra] [ref:: frontend/lib/hooks/use-project-realtime.ts] (PROD-1.6, 20/06/2026)
- [x] **Export CSV** des issues (filtrées) depuis la toolbar du board [id:: FE-EXPORT-001] [statut:: done] [parite:: ok] [ref:: frontend/lib/utils/export-issues-csv.ts] (PROD-1.7, 20/06/2026)

**À faire :**
- [ ] Streaming réel de l'assistant (SSE) côté UI [id:: FE-IA-010] [statut:: todo] [parite:: extra] [prio:: P2] [besoin-backend:: BE-IA-001] (PC-009)

## 9. Intégrations / Pièces jointes

**À faire :**
- [ ] Brancher Intégrations (GitHub/Slack/Webhooks) — `INTEGRATION_ROUTES` [id:: FE-INT-001] [statut:: broken] [parite:: ok] [prio:: P0] (PC-002)
- [ ] Brancher Pièces jointes — `ATTACHMENT_ROUTES` [id:: FE-ATT-001] [statut:: broken] [parite:: ok] [prio:: P0] (PC-002)
- [ ] URL absolue pour les connect OAuth (`*_CONNECT`) [id:: FE-INT-002] [statut:: todo] [prio:: P1] [ref:: frontend/lib/config/api-routes.ts] (voir P0-fix-plan §002)

## 10. Qualité (tests, a11y, perf, sécurité)

**À faire :**
- [ ] Couverture tests ≥ 50 % (Vitest+RTL+MSW) + rapport [id:: FE-QA-001] [statut:: todo] [prio:: P1] (TF-TEST-001)
- [ ] E2E Playwright parcours clés [id:: FE-QA-002] [statut:: todo] [parite:: extra] [prio:: P2]
- [ ] Audit accessibilité WCAG 2.1 AA (axe, clavier, ARIA) [id:: FE-QA-003] [statut:: todo] [prio:: P1]
- [ ] En-têtes sécurité + CSP, `npm audit` 0 vuln [id:: FE-QA-004] [statut:: todo] [prio:: P1] [besoin-backend:: BE-SEC-001]
- [ ] Budget perf Lighthouse ≥ 90 (bundle, images, lazy) [id:: FE-QA-005] [statut:: todo] [prio:: P2]
- [ ] Pre-commit hooks (husky + lint-staged) [id:: FE-QA-006] [statut:: todo] [prio:: P2]

---

> **Note Brain OS** — Les `[besoin-backend:: BE-xxx]` ci-dessus doivent exister dans [Backend.md](./Backend.md).
> Items cassés = P0 du [Backlog](../13-roadmap/Roadmap_Backlog.md) / [`.ai/P0-fix-plan.md`](../../../taskforce-fullstack/.ai/P0-fix-plan.md).

**Dernière mise à jour :** 20/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
