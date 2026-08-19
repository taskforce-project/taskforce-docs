---
id: wireframes-annotes
title: Wireframes annotés — TaskForce V1
doc_type: wireframes
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [wireframes, ui, ux, routes, design, conception, memoire, rncp, soutenance]
---

# 🖼️ Wireframes annotés — TaskForce V1

> **Nota bene — source de vérité** : aucun fichier de maquette statique n'a été archivé dans
> `assets/maquettes/`. Les wireframes ci-dessous sont **dérivés du code frontend réel**
> (`frontend/app/**/page.tsx`, 48 routes) et représentent l'interface telle qu'elle est
> implémentée.
>
> Chaque écran est annoté avec : **route URL**, **composants clés**, **UC correspondant(s)**,
> **endpoint(s) backend appelé(s)**.
>
> **Source de référence** : `frontend/app/` (Next.js App Router) · `frontend/components/` ·
> `frontend/lib/api/*-service.ts`

---

## 1. Flux d'authentification

### 1.1 Inscription — étape 1 (informations)

**Route** : `/auth/register`  
**UC** : UC-01 — Inscription + OTP  
**Composants** : `RegisterForm`, champs `firstName`, `lastName`, `email`, `password`

```
┌─────────────────────────────────────────────────────────┐
│  TaskForce                                              │
├─────────────────────────────────────────────────────────┤
│                                                         │
│         Créer votre compte                              │
│                                                         │
│  Prénom          [________________]                     │
│  Nom             [________________]                     │
│  Email           [________________]                     │
│  Mot de passe    [________________]                     │
│                                                         │
│  [  Continuer →  ]                                      │
│                                                         │
│  Déjà un compte ? → /auth/login                        │
└─────────────────────────────────────────────────────────┘
```

**Endpoint** : `POST /api/auth/register` → `{ userId, email }` (pas encore de JWT)

### 1.2 Inscription — étape 2 (choix du plan)

**Route** : `/auth/register/plan`  
**UC** : UC-11 — Abonnement Stripe (sélection initiale)  
**Composants** : `PlanSelectionCard` (FREE / PRO / Enterprise)

```
┌─────────────────────────────────────────────────────────┐
│  Choisissez votre plan                        Étape 2/3 │
├──────────────┬──────────────┬──────────────────────────┤
│   FREE       │  PRO         │  Enterprise               │
│   0 €        │  13 €/user   │  Sur devis                │
│              │  /mois       │  18–25 €/user             │
│  3 projets   │  Illimité    │  Illimité + SSO           │
│  5 membres   │  Illimité    │  Illimité + SLA           │
│              │  IA incluse  │  IA + support dédié       │
│  [Choisir]   │  [Choisir]   │  [Contacter]              │
└──────────────┴──────────────┴──────────────────────────┘
```

**Endpoint** : sélection stockée en session — utilisée à l'étape 3 pour créer la subscription Stripe.

### 1.3 Inscription — étape 3 (vérification OTP)

**Route** : `/auth/register/verification`  
**UC** : UC-01 — OTP à l'inscription (PAS au login)  
**Composants** : `OtpInput` (6 chiffres), `ResendButton`

```
┌─────────────────────────────────────────────────────────┐
│  Vérification email                           Étape 3/3 │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Code envoyé à : alice@exemple.com                      │
│                                                         │
│         [ 3 ][ 7 ][ 2 ][ 9 ][ 4 ][ 1 ]                 │
│                                                         │
│  Valide 15 minutes · Renvoyer le code                   │
│                                                         │
│  [  Vérifier →  ]                                       │
└─────────────────────────────────────────────────────────┘
```

**Endpoint** : `POST /api/auth/verify-otp` → si valide : `POST /api/auth/complete-registration`
→ création du compte Keycloak + JWT + redirection `/[workspace]/dashboard`.

### 1.4 Login

**Route** : `/auth/login`  
**UC** : UC-02 — Login Keycloak (délégué)

```
┌─────────────────────────────────────────────────────────┐
│  Connexion à TaskForce                                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Email           [________________]                     │
│  Mot de passe    [________________]                     │
│                                                         │
│  [  Se connecter  ]                                     │
│                                                         │
│  Mot de passe oublié → /auth/forgot-password           │
│  Pas de compte → /auth/register                        │
└─────────────────────────────────────────────────────────┘
```

**Endpoint** : `POST /api/auth/login` → Keycloak OIDC → JWT → redirection workspace.

---

## 2. Shell principal de l'application

**Route pattern** : `/(protected)/[workspace]/**`  
**Accès** : JWT valide + `WorkspaceMember` actif

```
┌────────────────────────────────────────────────────────────────┐
│ ┌──────┐  TaskForce          [🔔 notifs]  [👤 profil]  [?]    │
│ │ Logo │  workspace: acme-corp                                  │
├─┴──────┴───────────────────┬───────────────────────────────────┤
│                            │                                   │
│  Navigation gauche         │   Zone de contenu principale      │
│  ─────────────────         │   (change selon la route)         │
│  🏠 Dashboard              │                                   │
│  📋 Issues                 │                                   │
│  📁 Projets                │                                   │
│  🔄 Cycles                 │                                   │
│  🗺️  Roadmap               │                                   │
│  💬 Messages               │                                   │
│  📝 Discussions            │                                   │
│  🧠 Brain OS               │                                   │
│  📊 Analytics              │                                   │
│  👥 Membres                │                                   │
│  ─────────────────         │                                   │
│  ⚙️  Paramètres             │                                   │
│  📥 Inbox                  │                                   │
│  🤖 Agents                 │                                   │
│  ❓ Aide                   │                                   │
│                            │                                   │
└────────────────────────────┴───────────────────────────────────┘
```

**Store Zustand** : `workspaceStore`, `notificationStore`  
**Endpoint** : `GET /api/workspaces/{slug}` (chargement workspace + rôle utilisateur)

---

## 3. Gestion des projets

### 3.1 Liste des projets

**Route** : `/[workspace]/projects`  
**UC** : UC-05 — Gestion projets (ADMIN+)

```
┌─────────────────────────────────────────────────────────┐
│  Projets                              [+ Nouveau projet] │
├─────────────────────────────────────────────────────────┤
│  🔍 Rechercher...                                       │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ 📁 Frontend App                    ADMIN ●●●○○  │   │
│  │    12 issues · 2 cycles · Actif                 │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ 📁 Backend API                     MEMBER ●●●●○ │   │
│  │    27 issues · 1 cycle · Actif                  │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

**Endpoints** : `GET /api/workspaces/{id}/projects` · `POST /api/projects` (ADMIN+)

### 3.2 Issues d'un projet (vue Board)

**Route** : `/[workspace]/projects/[id]/issues`  
**UC** : UC-06 — Issues CRUD + Smart-assign (UC-07)

```
┌─────────────────────────────────────────────────────────────────┐
│  Frontend App > Issues     [Filtres ▼]  [Grouper ▼]  [+ Issue] │
├──────────────────┬──────────────────┬──────────────────────────┤
│  🔴 TODO         │  🟡 IN PROGRESS  │  🟢 DONE                  │
│  ──────────      │  ─────────────   │  ──────────              │
│  #42 Login UI    │  #38 Auth API    │  #31 DB setup            │
│  Assigné: Alice  │  Assigné: Bob    │  Assigné: Alice          │
│  P1 · 3pts       │  P2 · 5pts       │  P1 · 2pts               │
│                  │                  │                           │
│  #45 Signup      │                  │                           │
│  Non assigné     │                  │                           │
│  P2 · [Smart ✨] │                  │                           │
└──────────────────┴──────────────────┴──────────────────────────┘
```

**Smart-assign** : bouton `[Smart ✨]` → `POST /api/issues/{id}/smart-assign` →
top-3 assignataires suggérés par Groq.  
**Note** : les colonnes sont libres (pas de workflow imposé — ADR-002 / Diagramme_Etats_UML §1).

### 3.3 Détail d'une issue

**Route** : `/[workspace]/projects/[id]/issues/[issueId]`  
**UC** : UC-06 + UC-07

```
┌──────────────────────────────────────────────────────────────────┐
│  ← Issues  |  #42 — Implémenter le formulaire de connexion       │
├─────────────────────────────────────────────────┬────────────────┤
│                                                 │  Détails       │
│  Description                                    │  ─────────     │
│  ────────────                                   │  Statut    [▼] │
│  Formulaire email/password, validation Zod,     │  Priorité  [▼] │
│  redirect après login...                        │  Assigné   [▼] │
│                                                 │  Labels    [+] │
│  Activité                                       │  Cycle     [▼] │
│  ──────────                                     │  Effort    [▼] │
│  Alice a créé l'issue · il y a 2 j              │                │
│  Bob a commenté · il y a 1 h                    │  Smart ✨      │
│                                                 │  [Suggérer]    │
│  [Écrire un commentaire...]        [Envoyer]    │                │
└─────────────────────────────────────────────────┴────────────────┘
```

**Endpoints** : `GET /api/issues/{id}` · `PATCH /api/issues/{id}` · `POST /api/issues/{id}/comments`

---

## 4. Cycles (sprints)

**Route** : `/[workspace]/projects/[id]/cycles`  
**UC** : UC-08 — Cycles

```
┌──────────────────────────────────────────────────────────────────┐
│  Cycles                                        [+ Nouveau cycle] │
├──────────────────────────────────────────────────────────────────┤
│  ● ACTIF                                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ Sprint 3 — "Auth & Profil"                               │   │
│  │ 01/06 → 14/06/2026   Progression : ████████░░  80 %     │   │
│  │ 12 issues · 8 terminées · 4 restantes                   │   │
│  │                                              [Voir →]   │   │
│  └──────────────────────────────────────────────────────────┘   │
│  ○ TERMINÉ                                                       │
│  Sprint 2 — "Projets & Issues"     23/05 → 30/05   100 % ✅     │
│  Sprint 1 — "Core & Auth"          10/05 → 22/05   100 % ✅     │
└──────────────────────────────────────────────────────────────────┘
```

**Endpoints** : `GET /api/projects/{id}/cycles` · `POST /api/cycles` (ADMIN+)  
**État** : `DRAFT → ACTIVE → COMPLETED` (FSM — [[Diagramme_Etats_UML]] §3)

---

## 5. Chat (Messages)

**Route** : `/[workspace]/messages`  
**UC** : UC-09 — Chat canaux + messages  
**Temps réel** : STOMP `/topic/workspace.{id}.channel.{channelId}`

```
┌──────────────────────────────────────────────────────────────────┐
│  Messages                                                        │
├────────────────┬─────────────────────────────────────────────────┤
│  # général     │  # général                    👥 12 membres     │
│  # backend     │  ────────────────────────────────────────────   │
│  # frontend    │  Alice  10:42                                   │
│  # design      │    Quelqu'un a vu l'erreur 401 sur /api/auth ?  │
│  ──────────    │                                                 │
│  [+ Canal]     │  Bob  10:44                                     │
│                │    Oui, c'est le context-path qui manque        │
│                │    → voir ARCHITECTURE.md                       │
│                │                                                 │
│                │  ─────────────────────────────────────────────  │
│                │  [Écrire un message...] [📎] [😊]    [Envoyer] │
└────────────────┴─────────────────────────────────────────────────┘
```

**Endpoints** : `GET /api/workspaces/{id}/channels` · `POST /api/channels/{id}/messages`  
**WebSocket** : `use-stomp.ts` → `chatStore` → re-render temps réel

---

## 6. Brain OS (Knowledge Graph)

**Route** : `/[workspace]/brain`  
**UC** : UC implicite — gestion de la base de connaissance du workspace  
**Note** : Phase 0 livrée (structure de données) — UI en cours

```
┌──────────────────────────────────────────────────────────────────┐
│  🧠 Brain OS — acme-corp                    [+ Nœud]  [Sync]    │
├────────────────────────────────────────────────────────────────  │
│                                                                  │
│  Recherche sémantique : [Qu'est-ce que le smart-assign ?    🔍] │
│                                                                  │
│  Nœuds récents                          Graphe de connaissances  │
│  ─────────────                                                   │
│  📄 Smart Assign — how it works         ●─────●                  │
│     Lié à : Architecture, GroqService   │     │                  │
│                                         ●─────●                  │
│  📄 Onboarding checklist                                         │
│     Lié à : Membres, Projets                                     │
│                                                                  │
│  📄 API conventions                                              │
│     Lié à : Backend, ARCHITECTURE.md                            │
└──────────────────────────────────────────────────────────────────┘
```

**Endpoints** : `GET /api/workspaces/{id}/brain` · `GET /api/brain/{id}/nodes`  
**DB** : `brain_workspaces` (V51) + `knowledge_nodes` (embedding `vector(1536)`) + `knowledge_links`

---

## 7. Paramètres et membres

### 7.1 Membres du workspace

**Route** : `/[workspace]/members`  
**UC** : UC-04 — Gestion membres + invitations (ADMIN+)

```
┌──────────────────────────────────────────────────────────────────┐
│  Membres                                   [Inviter un membre]   │
├──────────────────────────────────────────────────────────────────┤
│  🔍 Rechercher...                                                │
│                                                                  │
│  Nom             Email                  Rôle        Actions      │
│  ──────────────  ─────────────────────  ──────────  ─────────    │
│  Alice Martin    alice@acme.com         🔑 OWNER    —            │
│  Bob Dupont      bob@acme.com           🛡️ ADMIN    [▼] [✗]     │
│  Paula Chen      paula@acme.com         👤 MEMBER   [▼] [✗]     │
└──────────────────────────────────────────────────────────────────┘
```

**Endpoints** : `GET /api/workspaces/{id}/members` · `POST /api/workspaces/{id}/invitations` ·
`PATCH /api/workspace-members/{id}/role` (ADMIN+) · `DELETE /api/workspace-members/{id}` (ADMIN+)

### 7.2 Paramètres workspace

**Route** : `/[workspace]/settings`  
**UC** : UC-03 — Gestion workspace (OWNER)

```
┌──────────────────────────────────────────────────────────────────┐
│  Paramètres — acme-corp                                          │
├──────────────────────────────────────────────────────────────────┤
│  Général    |  Abonnement    |  Intégrations    |  Danger zone   │
├──────────────────────────────────────────────────────────────────┤
│  Nom du workspace     [acme-corp              ]                  │
│  Slug                 [acme-corp              ] (URL)            │
│  Fuseau horaire       [Europe/Paris    ▼      ]                  │
│                                                                  │
│                                        [Enregistrer]            │
└──────────────────────────────────────────────────────────────────┘
```

---

## 8. Flux de paiement Stripe

### 8.1 Retour succès

**Route** : `/payment/success`  
**UC** : UC-11 — Retour Stripe après checkout

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│           ✅  Abonnement activé !                       │
│                                                         │
│  Votre plan PRO est maintenant actif.                   │
│  Prochain renouvellement : 05/08/2026                   │
│                                                         │
│  [  Accéder à mon workspace →  ]                        │
└─────────────────────────────────────────────────────────┘
```

**Backend** : webhook `checkout.session.completed` → `StripeWebhookController` →
`SubscriptionService` → `PlanStatus.ACTIVE` (FSM Stripe — [[Diagramme_Etats_UML]] §4)

### 8.2 Invitation externe

**Route** : `/invitations/[token]`  
**UC** : UC-04 — Acceptation d'invitation (lien email)

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  Vous êtes invité(e) à rejoindre                        │
│  l'espace de travail acme-corp                          │
│                                                         │
│  Invité par : Alice Martin (ADMIN)                      │
│  Rôle proposé : MEMBER                                  │
│                                                         │
│  [  Accepter l'invitation  ]   [  Refuser  ]            │
└─────────────────────────────────────────────────────────┘
```

**Endpoint** : `POST /api/invitations/{token}/accept` →
`InvitationStatus.PENDING → ACCEPTED` ([[Diagramme_Etats_UML]] §2)

---

## 9. Récapitulatif des routes et UC

| Route | UC(s) | Rôle minimum |
|---|---|---|
| `/auth/register` | UC-01 | Public |
| `/auth/register/plan` | UC-11 (sélection) | Public |
| `/auth/register/verification` | UC-01 OTP | Public |
| `/auth/login` | UC-02 | Public |
| `/[w]/dashboard` | — | MEMBER |
| `/[w]/issues` | UC-06 | MEMBER |
| `/[w]/projects` | UC-05 | MEMBER (lecture) |
| `/[w]/projects/[id]/issues` | UC-06, UC-07 | MEMBER |
| `/[w]/projects/[id]/issues/[id]` | UC-06, UC-07 | MEMBER |
| `/[w]/projects/[id]/cycles` | UC-08 | MEMBER (lecture) |
| `/[w]/projects/[id]/backlog` | UC-06 | MEMBER |
| `/[w]/projects/[id]/pages/[id]` | UC-10 | MEMBER |
| `/[w]/projects/[id]/teams` | UC-04 | MEMBER (lecture) |
| `/[w]/messages` | UC-09 | MEMBER |
| `/[w]/brain` | Brain OS | MEMBER |
| `/[w]/analytics` | — | MEMBER |
| `/[w]/members` | UC-04 | ADMIN+ |
| `/[w]/settings` | UC-03 | OWNER |
| `/[w]/roadmap` | — | MEMBER |
| `/[w]/discussions` | — | MEMBER |
| `/[w]/cycles` | UC-08 | MEMBER |
| `/[w]/my-work/**` | UC-06 | MEMBER |
| `/[w]/inbox/**` | — | MEMBER |
| `/[w]/agents` | UC-07 | MEMBER |
| `/invitations/[token]` | UC-04 | Public |
| `/payment/success` | UC-11 | Public |
| `/payment/cancel` | UC-11 | Public |

> 🔗 Voir aussi : [[Diagramme_Cas_Usage_UML]] · [[Diagrammes_Sequence_UML]] ·
> [[CdCF_v2]] (UC détaillés) · [[Architecture_C4]] (structure frontend)
