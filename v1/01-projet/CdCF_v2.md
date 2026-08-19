---
id: cdcf-v2
title: CdCF v2 — Cahier des Charges Fonctionnel (périmètre livré)
doc_type: cdcf
statut: valide
version: 2.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [cdcf, fonctionnel, use-cases, specifications, saas, memoire, rncp, livrables]
---

# 📋 CdCF v2 — Cahier des Charges Fonctionnel

> **Version 2.0 — périmètre réellement livré (juillet 2026)**
>
> Ce document **remplace et corrige** le [[01_CdCF|CdCF v1.1 (27/02/2026)]] pour les parties qui
> divergent de l'implémentation finale. **Principe** : ne décrire que les fonctionnalités
> **réellement livrées et démontrables** dans le code. Les fonctionnalités planifiées mais non livrées
> sont indiquées « ⬜ non livré — backlog » et ne sont pas spécifiées comme si elles existaient.
>
> Pour les diagrammes UML associés → [[Diagramme_Cas_Usage_UML]] · [[Diagrammes_Sequence_UML]] ·
> [[Diagramme_Classes_UML]]. Pour la description technique → [[CdCT_v2|CdCT v2]].

---

## Sommaire

1. [Contexte & objet](#1-contexte--objet)
2. [Évolutions v1 → v2 (delta)](#2-évolutions-v1--v2-delta)
3. [Acteurs et modèle de rôles](#3-acteurs-et-modèle-de-rôles)
4. [Périmètre fonctionnel livré](#4-périmètre-fonctionnel-livré)
5. [Cas d'usage V2 (mis à jour)](#5-cas-dusage-v2-mis-à-jour)
6. [Scénarios utilisateurs](#6-scénarios-utilisateurs)
7. [Exigences non fonctionnelles](#7-exigences-non-fonctionnelles)
8. [Hors périmètre V1 (backlog)](#8-hors-périmètre-v1-backlog)

---

## 1. Contexte & objet

**TaskForce** est un SaaS de gestion de projet multi-tenant différencié par un moteur de
**répartition intelligente des tâches** assisté par IA. Le gestionnaire reçoit une proposition
automatique (scoring compétences × charge × disponibilités, affiné par LLM Groq) et **valide ou
ajuste** — il reste décisionnaire à tout moment.

Ce CdCF couvre le **produit tel que livré à la date de soutenance RNCP (juillet 2026)**, projet
fil rouge de certification Développeur Full Stack — Metz Numeric School 2025-2026.

---

## 2. Évolutions v1 → v2 (delta)

| Sujet | CdCF v1.1 (02/2026) | CdCF v2 (livré réel) |
|---|---|---|
| **Modèle de rôles** | Manager / Collaborateur / Administrateur / Invité | **OWNER / ADMIN / MEMBER** (3 rôles hiérarchiques, pas d'Invité) |
| **Modules optionnels** | LIMS / Qualité / GED activables | ⬜ **Non livrés** — anticipés dans l'architecture, backlog post-V1 |
| **Smart-assign** | Algorithme d'assignation décrit conceptuellement | ✅ Livré : scoring multi-critères + LLM Groq + `IssueWorklog` charge réelle |
| **Redistribution auto** | Non prévu dans v1 | ✅ Livré : preview plan → validation manager → apply (journalisé) |
| **Chat temps réel** | Non prévu | ⛔️ Retiré (11/07/2026) : hors CdC, on n'out-Slack pas Slack → intégration Slack/Teams visée à la place. (Avait été livré — canaux STOMP — puis supprimé, migration V64.) |
| **Pages wiki** | Non prévu | ✅ Livré : pages Markdown par projet |
| **Cycles (sprints)** | Non prévu explicitement | ✅ Livré : DRAFT → ACTIVE → COMPLETED, avec CycleIssue |
| **Brain OS** | Non prévu | ✅ Livré : knowledge graph pgvector, assistant IA Groq |
| **Intégrations** | Mentionnées comme futures | ✅ Livrés : GitHub (liens issues), Slack (channels), webhooks entrants |
| **Export RGPD** | Mentionné en UC secondaire | ✅ Livré : export portabilité JSON + anonymisation (droit à l'oubli) |
| **Alertes surcharge** | UC07 décrit conceptuellement | ✅ Livré : `OverloadAlertScheduler` + règles Prometheus |
| **Rapport PDF/Excel** | UC08 prévu | ⬜ **Non livré** — analytics JSON disponibles, export fichier absent |
| **Invité / utilisateur externe** | Prévu | ⬜ **Non livré** — modèle de rôles simplifié à 3 niveaux |
| **UML** | Section 7 décrite textuellement | ✅ Livré en Phase 0 : 5 docs Mermaid dérivés du code réel |

---

## 3. Acteurs et modèle de rôles

### 3.1 Rôles implémentés (`WorkspaceRole`)

| Rôle | Nom code | Profil métier | Héritage |
|---|---|---|---|
| **Collaborateur** | `MEMBER` | Membre d'équipe, exécute les issues | — |
| **Gestionnaire** | `ADMIN` | Manager d'équipe / chef de projet | hérite de MEMBER |
| **Propriétaire** | `OWNER` | Titulaire du workspace, gère l'abonnement | hérite de ADMIN |

> **Modèle hiérarchique** : chaque rôle hérite des droits du précédent.
> `requireManager` dans le code = `OWNER ∪ ADMIN` (preuve : `AuthorizationService.requireManager`).
> `assertIsOwner` = OWNER seul (2 actions : `updateMemberRole`, `deleteWorkspace`).
> Voir détail complet → [[Diagramme_Cas_Usage_UML]] §3.

### 3.2 Acteurs externes

| Acteur | Nature | Rôle |
|---|---|---|
| **Stripe** | Système tiers (webhooks) | Notifie les événements de facturation (signature HMAC) |
| **Ordonnanceur** | Service interne planifié | Détecte et notifie les surcharges (`OverloadAlertScheduler`) |

---

## 4. Périmètre fonctionnel livré

### 4.1 Domaine — Identité & Workspace

- Inscription par e-mail (3 étapes : données → plan → vérification OTP)
- Connexion par login/mot de passe (délégation Keycloak), session JWT (access + refresh)
- Réinitialisation de mot de passe par OTP
- Multi-tenant : **workspace** comme unité d'isolation des données
- Gestion des membres (invitations, rôles, congés/absences)
- Équipes (`Team`) regroupant des membres, assignables à des projets

### 4.2 Domaine — Projets & Issues

- CRUD complet de projets (icône, couleur, statut actif/paused/archived)
- **Statuts** et **types** d'issues configurables **par projet**
- Issues : titre, description, priorité, estimation, assignée, reporter, parent, étiquettes, checklist
- **Relations entre issues** (blocks, is-blocked-by, relates-to, duplicates)
- **Time tracking** : worklogs (temps logué par collaborateur, base de la charge réelle)
- **Cycles (sprints)** : DRAFT → ACTIVE → COMPLETED ; issues affectables à un cycle
- **Pages wiki** par projet (contenu Markdown)
- **Liens GitHub** sur les issues (branches, PRs)
- Roadmap, analytics (avancement, vélocité, charge)

### 4.3 Domaine — ⭐ Répartition intelligente (cœur CDC)

- **Smart-assign** : pour une issue donnée, classe les membres candidats par score
  (compétences `member_skill_profiles` × charge réelle cross-projets `IssueWorklog` ×
  disponibilité `MemberLeave`, affiné par LLM Groq). **Profil de croissance** : peut favoriser un
  membre moins expérimenté pour le faire progresser (`growth_enabled`).
- **Redistribution automatique** : le gestionnaire déclenche un *preview* (plan complet sans effet),
  valide les mouvements souhaités, puis *apply* (réaffectation réelle + audit). Aucune écriture
  sans validation manager.
- **Alertes de surcharge** : détection automatique planifiée, notification aux OWNER/ADMIN.

### 4.4 Domaine — Collaboratif

- **Chat temps réel** : canaux (`Channel`) + messages STOMP/SockJS via RabbitMQ (repli `SimpleBroker`)
- **Discussions** : threads attachés à un workspace
- **Notifications** in-app (destinataire + acteur)

### 4.5 Domaine — IA / Brain OS

- **Knowledge graph natif** : 1 workspace = 1 `BrainWorkspace`, nœuds `KnowledgeNode` avec
  embeddings `vector(384)` (pgvector), arêtes `KnowledgeEdge`
- **Assistant conversationnel** : LLM Groq (`llama-3.3-70b-versatile`), contexte ancré dans le Brain
- **Outils IA** : `CreateNoteTool`, `SearchBrainTool`, `AgentService`

### 4.6 Domaine — Intégrations

- **GitHub** : OAuth, lien issues TaskForce ↔ PRs/branches GitHub
- **Slack** : OAuth, channels SlackChannel
- **Webhooks entrants** : configuration et déclenchement d'événements vers URL externe

### 4.7 Domaine — Facturation

- Plans **FREE** et **PRO** (via Stripe Checkout, portail client)
- Webhooks Stripe : `checkout.session.completed`, `subscription.updated/deleted`,
  `invoice.payment_succeeded/failed` (idempotents via `stripe_event_id`)
- Historique des abonnements (`SubscriptionHistory`)

### 4.8 Domaine — Conformité RGPD

- **Export portabilité** (Art. 20) : profil + memberships + compétences + worklogs → JSON
- **Anonymisation** (droit à l'oubli / Art. 17) : suppression données identifiantes, conservation
  traces anonymes

### 4.9 Domaine — Sécurité & Observabilité

- RBAC multi-tenant (toutes requêtes vérifiées), headers sécurité (OWASP A05)
- Rate limiting, chiffrement au repos (`EncryptedStringConverter`)
- Journal d'audit applicatif (`AuditLog`) pour les actions sensibles
- Logs client frontend → `POST /api/logs/client` (Slf4j, protection log-forging)
- OpenTelemetry → SigNoz, Prometheus (9 alertes), Grafana

---

## 5. Cas d'usage V2 (mis à jour)

> Les UC ci-dessous correspondent aux cas définis dans [[Diagramme_Cas_Usage_UML]].
> Le découpage acteur est MEMBER / ADMIN+OWNER (gestionnaire) / OWNER seul.

### UC01 — S'authentifier

**Acteur** : tout utilisateur non encore connecté  
**Flux nominal** : saisie email + mot de passe → authentification Keycloak → JWT généré → session ouverte  
**Flux alternatif (inscription)** : email + pwd → OTP envoyé → vérification OTP → workspace créé → tokens → (plan payant : Stripe Checkout)  
**Preuve** : `AuthController`, `AuthService.login` / `verifyOtpAndCompleteRegistration`

### UC02 — Gérer ses tâches (MyWork)

**Acteur** : MEMBER  
**Description** : consultation du tableau de bord personnel (issues assignées, worklogs, cycles en cours, charge personnelle)  
**Preuve** : `MyWorkController`

### UC03 — Créer / traiter une issue

**Acteur** : MEMBER  
**Description** : créer une issue dans un projet, modifier son statut, sous-type, priorité, ajouter checklist, loguer du temps, commenter, créer une relation avec une autre issue  
**Preuve** : `IssueController`, `IssueService`, `IssueWorklog`

### UC04 — ⭐ Déclencher le smart-assign

**Acteur** : MEMBER (recommandation pour une issue), ADMIN/OWNER (redistribution)  
**Description** : demander une recommandation d'assignation pour une issue → liste de candidats classés avec score et justification LLM  
**Preuve** : `SmartAssignService.recommend`, `GET /issues/{id}/smart-assign`

### UC05 — ⭐ Redistribuer automatiquement (preview → apply)

**Acteur** : ADMIN/OWNER (`requireManager`)  
**Description** :
1. Demander un *preview* : plan de redistribution proposé (mouvements + charges projetées), **aucune écriture**
2. Valider tout ou partie → *apply* : réaffectations effectives + audit `REDISTRIBUTION_APPLY`  

**Preuve** : `RedistributionController`, `RedistributionService`

### UC06 — Gérer les compétences

**Acteur** : MEMBER (son propre profil) / ADMIN+OWNER (profil d'un autre)  
**Description** : modifier `member_skill_profiles` (compétences, séniorité, capacité hebdomadaire, objectifs de croissance)  
**Preuve** : `MemberSkillController`, `MemberSkillProfileService` (garde `isManager`)

### UC07 — Gérer les congés / disponibilités

**Acteur** : MEMBER (demande) / ADMIN+OWNER (approbation)  
**Description** : déposer une demande d'absence ; manager l'approuve ou la refuse (impacte la disponibilité dans le smart-assign)  
**Preuve** : `MemberLeaveController`, `MemberLeaveService`

### UC08 — Chat & discussions

**Acteur** : MEMBER  
**Description** : envoyer des messages dans un canal, créer/lire des discussions, recevoir les messages temps réel (STOMP/SockJS)  
**Preuve** : `ChannelController`, `ChatWebSocketController`, `DiscussionService`

### UC09 — Interroger l'assistant IA / Brain OS

**Acteur** : MEMBER (lecture) / ADMIN+OWNER (écriture Brain)  
**Description** : poser des questions à l'assistant (contexte ancré au graph), créer/modifier des nœuds de connaissance  
**Preuve** : `AssistantController`, `KnowledgeController`, `BrainAccessGuard`

### UC10 — Gérer l'abonnement (facturation)

**Acteur** : OWNER  
**Description** : accéder au portail Stripe (changement de plan, gestion de paiement), consulter l'état d'abonnement  
**Preuve** : `BillingController`, `StripeController`

### UC11 — Exporter ses données (RGPD)

**Acteur** : MEMBER (ses propres données)  
**Description** : télécharger l'export JSON de toutes ses données personnelles (Art. 20 RGPD)  
**Preuve** : `GdprController`, `GdprService.exportMyData`

### UC12 — Administrer le workspace

**Acteur** : OWNER (updateMemberRole, deleteWorkspace) / ADMIN+OWNER (invitations, audit)  
**Description** : gérer les membres (rôles, invitations), consulter le journal d'audit, configurer les intégrations, supprimer le workspace (OWNER seul)  
**Preuve** : `WorkspaceController`, `WorkspaceService`, `InvitationController`

---

## 6. Scénarios utilisateurs

### Scénario A — Onboarding d'un gestionnaire (parcours complet)

Alice s'inscrit sur TaskForce, choisit le plan Pro, vérifie son e-mail via OTP. Un workspace est
créé automatiquement à son nom. Elle invite 3 collaborateurs (Bob, Carole, David) — ils reçoivent
un lien d'invitation, acceptent à leur prochaine connexion. Alice complète les profils de compétences
de son équipe. Elle crée un projet « Refonte UI », y définit ses statuts/types personnalisés, ouvre
un premier cycle (sprint), et crée 10 issues. Pour chaque issue, elle déclenche le smart-assign :
TaskForce propose Bob (Back, charge 40 %) pour l'API, Carole (Design, charge 30 %) pour les wireframes.
Alice valide les propositions. Bob et Carole reçoivent leurs notifications in-app.

### Scénario B — Redistribution suite à une surcharge

Bob tombe malade (congé déclaré). L'`OverloadAlertScheduler` détecte que 4 issues lui sont encore
assignées dans le sprint en cours et envoie une alerte à Alice. Alice ouvre la vue Redistribution,
clique « Voir le plan » : TaskForce propose de transférer 2 issues à David (compétences compatibles,
charge 55 %) et 2 à une prestataire externe (Emma, capacité partielle). Alice valide le plan.
Les issues sont réaffectées, David et Emma notifiés, l'action journalisée dans l'audit.

### Scénario C — Collaborateur en croissance

David est junior React. Alice active `growth_enabled` dans son profil de compétences avec comme
cible `TypeScript avancé`. Lors du prochain smart-assign d'une issue TypeScript, TaskForce place
David en 2ème position (score légèrement inférieur à Bob) et ajoute dans la justification LLM
« candidat en parcours de croissance ciblant TypeScript avancé ». Alice peut choisir de l'affecter
pour le faire monter en compétence.

---

## 7. Exigences non fonctionnelles

| Catégorie | Exigence | Preuve / mesure |
|---|---|---|
| **Performance** | Réponse API < 200 ms (p95) sur endpoints courants | Prometheus `http_server_requests_seconds` (percentile-histogram) |
| **Disponibilité** | Cible 99 % (hors fenêtres de maintenance) | PCA/PRA documenté (`11-pca-pra/PS_PCA_PRA.md`) |
| **Sécurité** | OWASP Top 10 adressé, 0 vulnérabilité critique | `SecurityHeadersWebMvcTest`, ZAP baseline, Semgrep, Trivy |
| **Conformité RGPD** | Export portabilité + anonymisation opérationnels | `GdprServiceIntegrationTest` |
| **Accessibilité** | WCAG 2.1 AA (axe-core < 10 violations) | `a11y.spec.ts` Playwright, `Accessibilite.md` |
| **Couverture tests** | ≥ 60 % (JaCoCo backend) · ≥ 70 % (Vitest frontend) | Rapports JaCoCo / Vitest v8 |
| **Multi-tenant** | Isolation stricte par `workspace_id` sur toutes les entités | `WorkspaceAccessInterceptor`, RBAC checks |

---

## 8. Hors périmètre V1 (backlog)

Ces fonctionnalités étaient envisagées dans le CdCF v1 ou en cours d'idéation, mais **ne sont pas
livrées** dans la version soumise à la soutenance. Elles figurent dans [[Roadmap_Backlog]].

| Fonctionnalité | Statut | Référence |
|---|---|---|
| Modules optionnels LIMS / Qualité / GED | ⬜ backlog | [[Roadmap_Backlog]] |
| Rôle « Invité » (accès lecture externe) | ⬜ backlog | [[Roadmap_Backlog]] |
| Export rapport PDF/Excel (UC08 v1) | ⬜ backlog | [[Roadmap_Backlog]] |
| SSO SAML / Active Directory | ⬜ backlog | [[Roadmap_Backlog]] |
| CI/CD complet déployé en prod | ⬜ déploiement VM école en cours | [[Roadmap_Documentation]] |
| Landing page (refonte complète) | ⬜ hors scope V1 | [[Roadmap_Documentation]] |

> 🔗 Voir aussi : [[Note_Cadrage]] · [[CdCT_v2]] · [[Diagramme_Cas_Usage_UML]] ·
> [[Diagrammes_Sequence_UML]] · [[Catalogue_Documentation]].
