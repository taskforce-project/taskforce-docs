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
- [x] **Gabarit de page unifié** `PageContainer`/`PageHeader` (max-width unifiée, en-tête cohérent) appliqué dashboard/projects/analytics/members/teams/my-work/inbox [id:: FE-CORE-020] [statut:: wip] [parite:: ok] [ref:: frontend/components/layout/page-shell.tsx] (QA2-12/PROD-8.1, 23/06/2026 ; reste settings + page projet) 
- [x] **Tokens cohérence Cloudflare** : roundedness ÷2 (`--radius` 0.375rem) + variant bouton `dangerGhost` (actions destructives rouges) + breadcrumb hover animé [id:: FE-UI-020] [statut:: done] [parite:: ok] [ref:: frontend/app/globals.css + components/ui/button.tsx + breadcrumb.tsx] (QA2-1/2/3, 23/06/2026)
- [x] **Avatars** : `WorkspaceAvatar` (dégradé déterministe seedé, rounded-full) + `UserAvatar` rounded-full partout (sidebar/profil) [id:: FE-UI-021] [statut:: done] [parite:: ok] [ref:: frontend/components/ui/workspace-avatar.tsx] (QA2-7/8, 23/06/2026)
- [x] **Cloche notifications** : badge non-lus + popover preview (6 dernières) + « tout marquer lu »/« voir toutes » [id:: FE-NOTIF-010] [statut:: done] [parite:: ok] [ref:: frontend/components/layout/topbar/notification-bell.tsx] (QA2-11, 23/06/2026)
- [x] **Profil dropdown** : badge Pro/Free + CTA upgrade si Free + fix double-séparateur [id:: FE-UI-022] [statut:: done] [parite:: ok] [ref:: frontend/components/layout/sidebar/nav-user.tsx] (QA2-6, 23/06/2026)
- [x] **Fix 500 inbox** (guard `signal.issueUrl` null) + **logo TaskForce** sur pages erreur/404 + sidebar icônes Members/Teams différenciées + My Queue onglet « All » [id:: FE-UI-023] [statut:: done] [parite:: ok] (QA2-4/5/9/10, 23/06/2026)
- [x] **Alignement bordures** : `SidebarHeader` en `h-14` (= topbar) → séparateur workspace aligné sur la bordure du breadcrumb [id:: FE-UI-024] [statut:: done] [parite:: ok] (QA2-27, 23/06/2026)
- [x] **Dashboard insight cards** : **style `SectionCard` conservé** (en-tête lien + corps) avec corps enrichis — `MetricSplit`/`Metric` + sous-ligne d'insight (`SegmentBar` ajouté à `section-card.tsx`) sur agrégats **réels** + **graphe ligne recharts** « Tâches/semaine » (résolues vs ouvertes) sur la carte Throughput via `getAnalyticsThroughput` [id:: FE-UI-025] [statut:: done] [parite:: ok] [ref:: frontend/components/ui/section-card.tsx] (QA2-13/PROD-8.3, 23/06/2026)
- [~] **Page projet `[id]`** : vue List corrigée (bouton filtre n'est plus étiré pleine largeur — toolbar aligné sur le board) + bouton Auto-assign mis en avant (rempli quand issues non assignées) [id:: FE-UI-026] [statut:: wip] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/[id]] (QA2-14, 23/06/2026 ; reste : kanban paramétrable, DragOverlay, refonte layout)
- [~] **Issue-sheet** : overflow horizontal corrigé (onglets scrollables) + responsive (corps empilé en mobile, sidebar métadonnées `w-full` → `sm:w-56 border-l`) [id:: FE-ISS-030] [statut:: wip] [parite:: ok] [ref:: frontend/components/sheets/issue-sheet.tsx] (QA2-15, 23/06/2026 ; reste : lier Page↔issue, clic membre → détail)
- [x] **Liste projets** : multi-affichage **list/cards**, **pin** (favori, épinglés en tête), **tri** (santé/récent/nom/progression/ouvertes), archive en **icône directe** (hors « … »), **skeletons** [id:: FE-PRJ-020] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/page.tsx] (QA2-22, 23/06/2026 ; reste templates = back)
- [x] **Board DnD fluide** : `DragOverlay` (clone `IssueCardPreview` suit le curseur, carte source estompée) [id:: FE-ISS-031] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/[id]/page.tsx] (QA2-14, 23/06/2026 ; reste kanban paramétrable « à discuter »)
- [x] **UI transverse — danger** : toutes les actions destructives user-facing en rouge (issue-sheet comment/attachment/relation/checklist/worklog, removes, delete/archive projet, delete team, `DeleteConfirmDialog`) [id:: FE-UI-027] [statut:: done] [parite:: ok] (QA2-R1/QA2-2, 23/06/2026)
- [x] **UI transverse — skeletons** : projects (list+cards), members (workspace+projet), List/Backlog/Cycles, board kanban ; reste analytics charts (P3) [id:: FE-UI-028] [statut:: done] [parite:: ok] (QA2-R5, 23/06/2026)
- [~] **Page projet — header & carte** : 2ᵉ breadcrumb retiré (header app suffit) + air onglets/toolbar ; **carte projet** : sparkline d'activité bleu (throughput réel par projet) à la place de la barre, **% déplacé** en pied [id:: FE-PRJ-021] [statut:: wip] [parite:: ok] (QA2-14/QA2-32, 23/06/2026)
- [x] **Layout intérieur opération** : one-screen (`h-full` + scroll interne), **scroll par colonne** kanban, **filtres en ligne** (`InlineIssueFilters`), **marges alignées dashboard** (`mx-auto max-w-screen-2xl`, fin du full-bleed) → New Issue/Auto-assign alignés [id:: FE-PRJ-022] [statut:: wip] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/[id]] (QA2-30, 23/06/2026 ; reste composant tabs dédié + vérif visuelle) ⚠️ rebuild non requis (front). **+ filtres en ligne aussi sur List/Backlog ; vue List : filtres + en-tête sticky, scroll interne ; bug `<button>` imbriqué (FilterRow) corrigé.**
- [x] **Issue-sheet façon GitHub** : sheet élargi (max-w-4xl) + onglets `flex-wrap` + colonne droite repensée (`MetaRow` label-au-dessus/valeur-en-dessous, sidebar `sm:w-72`) → plus d'infos coupées [id:: FE-ISS-032] [statut:: done] [parite:: ok] [ref:: frontend/components/sheets/issue-sheet.tsx] (QA2-31, 23/06/2026)
- [x] **Modal Upgrade dédié** : `UpgradeDialog` (3 plans, recommandé) monté global (`AppShell`) via `useUpgradeStore` ; CTA Pro = checkout Stripe direct ; tous les CTA recâblés (profil/switcher/members/analytics) [id:: FE-SUB-010] [statut:: done] [parite:: extra] [ref:: frontend/components/subscription/upgrade-dialog.tsx] (QA2-19, 23/06/2026)
- [x] **My Queue en onglets** : All / Issues / Sprints / Pages (compteurs, onglet initial selon la route) [id:: FE-MYW-010] [statut:: done] [parite:: ok] [ref:: frontend/components/my-work/my-work-view.tsx] (QA2-23, 23/06/2026)
- [~] **Help — vraie doc** : page `/help` dé-mockée (16 articles réels en accordéon, recherche, filtres catégories, contact mailto) [id:: FE-HELP-010] [statut:: wip] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/help/page.tsx] (QA2-25, 23/06/2026 ; reste étoffer le contenu + prompt assistant)
- [x] **Onglet projet Teams** (remplace Members) — **gestion complète** : créer équipe, voir/ajouter/retirer membres (recherche users), associer/dissocier, supprimer ; membres workspace via Settings projet + sidebar. **Case à cocher « done »** sur List/Backlog (icône statut → COMPLETED) [id:: FE-PRJ-023] [statut:: done] [parite:: ok] [ref:: frontend/components/projects/project-teams-section.tsx] (QA3-7/QA3-9, 23/06/2026)
- [x] **Chat IA — composants ElevenLabs** : `matrix` (dot-matrix animé, empty-state) + `shimmering-text` (« réfléchit… », recréé — registry bloqué) [id:: FE-IA-003] [statut:: done] [parite:: extra] [ref:: frontend/components/assistant/assistant-fab.tsx] (QA3-10, 23/06/2026)
- [~] **Settings workspace** : section Membres retirée (page dédiée) + section **Status** (ping API réel) ; reste notifs SMS/mail + logs/audit + Keycloak (back) [id:: FE-SET-011] [statut:: wip] [parite:: ok] (QA3-8, 23/06/2026)
- [~] **Settings — Billing** : bouton Upgrade (placeholder mort) → ouvre le modal Upgrade ; Enterprise → contact sales ; copies de plan alignées sur les vraies limites [id:: FE-SET-010] [statut:: wip] [parite:: ok] (QA2-18, 23/06/2026 ; reste backend : logs/audit/export, status, notifs SMS/mail)

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
- [x] **Members — bug limite plan** : footer codé en dur « /5 » → plan-aware (limite réelle via endpoint usage / `plan-limits` ; ENTERPRISE illimité, PRO 50 ; CTA upgrade seulement si limite atteinte) ; icône rouge sur « Remove » [id:: FE-WS-012] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/members/page.tsx] (QA2-20, 23/06/2026)
- [x] **Members — vue projets** : chips « dans quel projet » + filtre par projet (front-only, dérivé de `project.members`) [id:: FE-WS-013] [statut:: done] [parite:: ok] (QA2-20, 23/06/2026)
- [x] **Settings — Status & audit** : section Status (ping API + services) + **journal d'audit** (`GET /audit`) + **export CSV** (front-only) [id:: FE-SET-012] [statut:: done] [parite:: ok] (QA3-8, 23/06/2026)
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
- [x] **Discussions fonctionnelles** : list/create/pin/lock/delete/filtres/search câblés (`discussion-store` + `discussion-service`, `DiscussionController` porte bien `/api`) + **pilotage d'état** (Mark as answered / Close / Reopen via `updateDiscussion`) → rôle Q&R/annonces [id:: FE-DISC-001] [statut:: done] [parite:: extra] [ref:: frontend/app/(protected)/[workspace]/discussions/page.tsx] (PROD-6.7, 24/06/2026) ; **reste** vue thread + réponses (besoin back `DiscussionReply`) + déverrouillage sidebar
- [ ] Réparer Pages/wiki (route `/api`) [id:: FE-PAGE-001] [statut:: broken] [parite:: ok] [prio:: P0] [besoin-backend:: BE-PAGE-001] (PC-001)
- [ ] Réparer Teams + compléter `team-store` [id:: FE-TEAM-001] [statut:: broken] [parite:: extra] [prio:: P1] [besoin-backend:: BE-TEAM-001] (PC-001/006)
- [x] Teams : emoji/couleur à la création + Manage/Settings consolidé (« Gérer l'équipe ») [id:: FE-TEAM-010] [statut:: done] [parite:: ok] (PROD-3.6, 20/06/2026) ; reste assoc team↔opération (PROD-3.6b)
- [x] **Teams par projet (QA2-21)** : page Teams globale **supprimée** du menu + route `/teams` → redirige Members ; gestion déplacée dans l'opération (`ProjectTeamsSection`) avec **création inline** d'équipe [id:: FE-TEAM-020] [statut:: done] [parite:: ok] [ref:: frontend/components/projects/project-teams-section.tsx] (23/06/2026)

## 8. Notifications / Analytics / IA

**Fait :**
- [x] Inbox/notifications (mentions, assignations, alertes) [id:: FE-NOTIF-001] [statut:: done] [parite:: ok]
- [x] Dashboard analytics (KPIs, burndown, throughput, capacité) [id:: FE-ANA-001] [statut:: done] [parite:: ok]
- [x] AI Insights + Assistant (FAB/command palette) [id:: FE-IA-001] [statut:: wip] [parite:: extra]
- [x] **Board temps réel** : hook `useProjectRealtime` (STOMP `/topic/projects.{id}`) patche le store en direct [id:: FE-RT-001] [statut:: done] [parite:: extra] [ref:: frontend/lib/hooks/use-project-realtime.ts] (PROD-1.6, 20/06/2026)
- [x] **Export CSV** des issues (filtrées) depuis la toolbar du board [id:: FE-EXPORT-001] [statut:: done] [parite:: ok] [ref:: frontend/lib/utils/export-issues-csv.ts] (PROD-1.7, 20/06/2026)
- [x] **Sparkline activité projet** : carte projet branchée sur `GET …/projects/{id}/activity?days=14` (`getProjectActivity`) → vrai « issues créées/jour » sur 14 j, série continue, non gaté Pro [id:: FE-PROJ-030] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/page.tsx] (QA2-32, 24/06/2026)
- [x] **Infinite-scroll backlog** : rendu incrémental par pages de 25 (`IntersectionObserver`, sentinel + spinner), reset au changement de filtre ; endpoint paginé back `…/issues/paged` prêt pour pagination serveur à grande échelle [id:: FE-ISSUE-033] [statut:: done] [parite:: ok] [ref:: frontend/app/(protected)/[workspace]/projects/[id]/backlog/page.tsx] (QA2-33, 24/06/2026)
- [x] **PageShell partout** : `PageContainer`+`PageHeader` appliqués à toutes les pages contenu, **dont Settings** (fin du `max-w-5xl` ad-hoc) → layout/marges cohérents [id:: FE-LAYOUT-001] [statut:: done] [parite:: ok] [ref:: components/layout/page-shell.tsx · app/(protected)/[workspace]/settings/page.tsx] (PROD-8.1/QA2-18/QA2-R3, 24/06/2026)
- [x] **Ligne Signals répartie** : `SignalRow` en ligne unique aérée (icône · type `w-32` · titre+extrait flexible · méta projet/issue/heure poussée à droite `ml-auto`) au lieu de l'empilement collé à gauche [id:: FE-INBOX-010] [statut:: done] [parite:: ok] [ref:: frontend/components/inbox/inbox-view.tsx] (QA3-12, 24/06/2026)
- [x] **Notifications temps réel** (US-023) : hook `use-notifications-realtime` (abo STOMP `/topic/notifications.{userId}` → `pushSignal`) monté dans la cloche + polling 60 s de secours ; back pousse via `SimpMessagingTemplate` [id:: FE-NOTIF-010] [statut:: done] [parite:: ok] [ref:: frontend/lib/hooks/use-notifications-realtime.ts · components/layout/topbar/notification-bell.tsx] (US-023, 24/06/2026)
- [x] **Heatmap charge équipe** (US-022) : `WorkloadHeatmap` (membres×jours, intensité, légende) dans Analytics, gated Pro, branché `GET /analytics/workload` [id:: FE-ANA-022] [statut:: done] [parite:: gap→ok] [ref:: frontend/components/analytics/workload-heatmap.tsx] (US-022, 24/06/2026)
- [x] **Disponibilité / congés** (US-006) : `MemberAvailabilityCard` (liste + ajout type/dates/note + suppression) sur la page membre ; `availability-service`/`availability-store` ; back `member_leaves` (V49) [id:: FE-MEMBER-006] [statut:: done] [parite:: ok] [ref:: frontend/components/members/member-availability-card.tsx] (US-006, 24/06/2026)
- [x] **Pages exposées** : `/roadmap`, `/issues`, `/cycles` (existaient sans lien) ajoutées à la sidebar (groupe Work) + command-palette ; `/teams` palette → `/members` [id:: FE-NAV-010] [statut:: done] [parite:: ok] [ref:: components/layout/sidebar/app-sidebar.tsx · components/command-palette.tsx] (INFRA-1, 25/06/2026)
- [x] **Build prod réparé** : `next.config.ts` n'importe plus `webpack` (utilise l'instance injectée) + script `build`=`next build --webpack` → `next build` vert sous Next 16 (sinon conflit Turbopack/minification) [id:: FE-BUILD-001] [statut:: done] [parite:: ok] [ref:: frontend/next.config.ts · package.json] (INFRA-2, 25/06/2026)

**À faire :**
- [x] **Assistant câblé au backend** : `assistant-service` + route `ASSISTANT_ROUTES.CHAT` → `POST /api/workspaces/{slug}/assistant` ; adapter mock remplacé (corrige erreur de type), gestion erreurs, suggestions autoSend ; réponses réelles dès backend+Groq up [id:: FE-IA-002] [statut:: done] [parite:: extra] [ref:: frontend/components/assistant/assistant-fab.tsx] (QA2-16, 23/06/2026)
- [x] **Assistant analytics-aware** (socle) : back `AssistantService` injecte un **bloc métriques réelles** (total/ouvertes, créées 7j, vélocité 7j/30j, ouvertes par projet, charge par membre) dans le system prompt Groq → réponses chiffrées exactes ; empty-state du FAB pointe vers des questions analytics [id:: FE-IA-003] [statut:: done] [parite:: extra] [ref:: backend …/core/service/AssistantService.java · frontend/components/assistant/assistant-fab.tsx] (QA2-17 socle, 24/06/2026) ; **reste** graphe dans le chat (réponse structurée → recharts)
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

**Dernière mise à jour :** 24/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
