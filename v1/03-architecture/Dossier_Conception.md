---
id: dossier-conception
title: Dossier de conception — TaskForce V1
doc_type: dossier-conception
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [conception, architecture, uml, mcd, e8, dossier, memoire, rncp, soutenance]
---

# 🧩 Dossier de conception — TaskForce V1

> **Livrable E8** (référentiel DFS — Développeur Full Stack, Metz Numeric School 2025–2026).
>
> Ce dossier est le document de synthèse de la phase de conception. Il **assemble et met en perspective**
> l'ensemble des artefacts produits (UML, MCD/MLD, C4, dictionnaire de données) en les
> reliant aux **exigences du CdCF/STB** et aux **choix d'architecture (ADR)**. Chaque section
> pointe vers le document source pour le détail.
>
> Règle : aucun artefact n'est inventé ici — tout est dérivé du code, des migrations Flyway (V1–V56)
> et des entités JPA réelles.

---

## Table des matières

1. [Contexte & problématique](#1-contexte--problématique)
2. [Étude des besoins — synthèse](#2-étude-des-besoins--synthèse)
3. [Conception fonctionnelle](#3-conception-fonctionnelle)
4. [Conception des données](#4-conception-des-données)
5. [Conception de l'architecture technique](#5-conception-de-larchitecture-technique)
6. [Conception de la sécurité](#6-conception-de-la-sécurité)
7. [Conception de l'observabilité](#7-conception-de-lobservabilité)
8. [Décisions structurantes (synthèse ADR)](#8-décisions-structurantes-synthèse-adr)
9. [Traçabilité exigences → conception](#9-traçabilité-exigences--conception)
10. [Bilan de la phase de conception](#10-bilan-de-la-phase-de-conception)

---

## 1. Contexte & problématique

TaskForce est un **SaaS de gestion de projet multi-tenant** (famille Linear/Jira), développé
en tant que projet fil rouge pour la certification RNCP "Développeur Full Stack" à Metz Numeric
School (2025–2026). Il est développé par un seul développeur endossant tous les rôles (PO, PM,
architecte, dev, QA, DevOps, tech writer).

**Problème central** : les équipes de développement manquent d'un outil centralisé qui combine
gestion des issues, cycles (sprints), chat d'équipe, pages wiki, analytics, assistance IA
contextuelle et facturation — sans dépendre de N outils disparates.

**Réponse produit** : un SaaS unifié organisé autour de la notion de **workspace** (1 entreprise
= 1 workspace), avec des projets, issues, cycles, chat, Brain OS (knowledge graph) et
une facturation Stripe (FREE / PRO 13 €/user/mois / Enterprise).

> 🔗 [[Note_Cadrage]] — [[PRD_Vision_Produit]] — [[CdCF_v2]] — [[Business_Model_Pricing]]

---

## 2. Étude des besoins — synthèse

### 2.1 Acteurs et périmètre fonctionnel

Trois acteurs hiérarchiques (chacun hérite des droits des niveaux inférieurs) :

```
MEMBER ⊂ ADMIN ⊂ OWNER
```

| Acteur | Responsabilités principales |
|---|---|
| **MEMBER** | Participer aux projets assignés, créer/modifier des issues, utiliser le chat |
| **ADMIN** | Gérer les membres, créer des projets, configurer les intégrations |
| **OWNER** | Gérer le billing Stripe, supprimer le workspace, tous les droits ADMIN |

Deux acteurs systèmes : **Stripe** (webhooks paiement) et **Ordonnanceur** (redistribution
automatique des issues).

> 🔗 Détail UC + gardes de code → [[Diagramme_Cas_Usage_UML]]

### 2.2 Cas d'usage principaux (V1)

| UC | Acteurs | Guard code | Statut |
|---|---|---|---|
| UC-01 Inscription + OTP | Anonyme | — | ✅ |
| UC-02 Login Keycloak | MEMBER+ | Keycloak OIDC | ✅ |
| UC-03 Gestion workspace (CRUD) | OWNER | `assertIsOwner` | ✅ |
| UC-04 Gestion membres + invitations | ADMIN+ | `requireManager` | ✅ |
| UC-05 Gestion projets | ADMIN+ | `requireManager` | ✅ |
| UC-06 Issues — CRUD + assignation | MEMBER+ | `ProjectMember` check | ✅ |
| UC-07 Smart-assign (suggestion LLM) | MEMBER+ | `ProjectMember` check | ✅ |
| UC-08 Cycles (sprints) | ADMIN+ | `requireManager` | ✅ |
| UC-09 Chat (canaux + messages) | MEMBER+ | `ChannelMember` check | ✅ |
| UC-10 Pages wiki | MEMBER+ | `ProjectMember` check | ✅ |
| UC-11 Abonnement Stripe | OWNER | Webhook Stripe | ✅ |
| UC-12 Export RGPD | MEMBER (ses données) / ADMIN (workspace) | `assertIsOwner` pour bulk | ✅ |

### 2.3 Exigences techniques clés (STB)

| Famille | Exemple d'exigence | Source |
|---|---|---|
| PERF | API p95 < 200 ms ; smart-assign < 3 s | Prometheus histogram |
| SEC | OWASP Top 10 couvert ; JWT RS256 (Keycloak OIDC) ; HTTPS prod | `SecurityConfig.java` |
| QUAL | JaCoCo ≥ 60 % ; Vitest ≥ 90 % ; TS strict | `pom.xml` + `vitest.config.ts` |
| DISP | RTO < 2 h ; PRA documenté | `PS_PCA_PRA.md` |
| INT | Stripe + GitHub + Slack OAuth opérationnels | `docker-compose.dev.yml` |

> 🔗 Exigences complètes (9 familles, ~45 IDs) → [[STB]]

---

## 3. Conception fonctionnelle

### 3.1 Diagramme de cas d'usage

Représente les 12 UC V1, les 3 acteurs hiérarchiques et les 2 acteurs systèmes.
Chaque cas est **gardé par du code réel** (`AuthorizationService`, `assertIsOwner`,
`requireManager`, vérifications `WorkspaceMember` / `ProjectMember`).

> 🔗 [[Diagramme_Cas_Usage_UML]] — 3 acteurs + diagramme Mermaid + table des gardes

### 3.2 Diagrammes de séquence (6 parcours clés)

| Séquence | Particularité documentée |
|---|---|
| **Inscription + OTP** | OTP à l'inscription, PAS au login (Keycloak gère le login) |
| **Login Keycloak** | Délégation OIDC complète — aucun token généré par le backend |
| **Smart-assign** | Scoring SQL (charge, compétences, disponibilité) puis modèle **auto-hébergé** en sortie JSON forcée, top-3 |
| **Redistribution auto** | Preview (dry-run) → validation ADMIN → apply ; ordonnanceur `@Scheduled` |
| **Stripe checkout + webhooks** | `checkout.session.completed` → `customer.subscription.updated` |
| **Export RGPD** | Agrégation multi-tables → JSON → download sécurisé |

> 🔗 [[Diagrammes_Sequence_UML]] — 6 diagrammes Mermaid `sequenceDiagram`

### 3.3 Machines à états (5 entités)

| Entité | Nature | Transitions libres ? |
|---|---|---|
| `Issue` (statut catégorie) | Board kanban | ✅ Oui — aucune contrainte dans le code |
| `WorkspaceInvitation` | FSM réelle | ❌ Non — `PENDING → ACCEPTED/DECLINED/EXPIRED/REVOKED` |
| `Cycle` | Phases sprint | ❌ Non — `DRAFT → ACTIVE → COMPLETED` |
| `PlanStatus` | Miroir Stripe | ❌ Non — piloté par les webhooks Stripe |
| Redistribution | Workflow preview→apply | ❌ Non — `PREVIEW → CONFIRMED → APPLIED` |

> 🔗 [[Diagramme_Etats_UML]] — 5 diagrammes Mermaid `stateDiagram-v2`

---

## 4. Conception des données

### 4.1 Modèle Entité-Association (MCD)

7 domaines métier, modélisés en Mermaid `erDiagram` depuis le schéma réel
(`information_schema`) :

| Domaine | Entités principales | Tables |
|---|---|---|
| **Identité & Accès** | User, Workspace, WorkspaceMember, WorkspaceInvitation | 4 |
| **Projets & Issues** | Project, Issue, IssueComment, IssueActivity, IssueRelation, ProjectLabel | 9 |
| **Cycles & Planning** | Cycle, CycleIssue, Page | 3 |
| **Équipes & Canaux** | Team, TeamMember, Channel, ChannelMember, ChatMessage | 5 |
| **Compétences & Charge** | MemberSkillProfile, WorkLog | 2 |
| **Auth & Facturation** | RefreshToken, OtpVerification, Subscription, SubscriptionHistory, AuditLog | 5 |
| **Brain OS** | BrainWorkspace, KnowledgeNode, KnowledgeLink | 3 |
| Transverse | Notification, Attachment, Integration, IssueGitHubLink, Discussion, DiscussionPost | 6 |

**Total : 55 tables / 483 colonnes / 104 clés étrangères**

> 🔗 [[Modele_Donnees_MCD_MLD]] — MCD par domaine + MLD + règles de gestion

### 4.2 Modèle Logique (MLD) et contraintes

- **Héritage** : 4 entités étendent `AuditableEntity` (`BrainWorkspace`, `KnowledgeNode`,
  `MemberLeave`, `WorkspaceInvitation`) — colonnes `created_at`, `updated_at`, `created_by`.
- **Contraintes FK** : `ON DELETE CASCADE` pour les données de vie du workspace
  (ex: `workspace_members`) ; `ON DELETE SET NULL` pour les références optionnelles
  (ex: `issue.assignee_id`) ; FK omise volontairement pour Auth/Facturation (cf. §4.3).
- **Index** : `ivfflat` sur `knowledge_nodes.embedding vector(1536)` pour la recherche k-NN
  (pgvector, migration V51).
- **Unique constraints** : slug workspace (`V3`), email user, `workspace_id` de `brain_workspaces`.

### 4.3 Modèle hybride FK — choix de conception

Les entités d'audit/auth/facturation (`AuditLog`, `RefreshToken`, `OtpVerification`,
`Subscription`, `SubscriptionHistory`) **ne déclarent pas de `@ManyToOne User`** mais stockent
un `Long userId`. Raison documentée dans le Javadoc de `AuditLog.java` :

> *"le journal doit survivre à la suppression de l'utilisateur"*

Ce choix est une **décision de conception explicite** (ADR-008) — pas un oubli.

> 🔗 [[Dictionnaire_Donnees]] — 55 tables × types/nullable/défauts/clés complets

### 4.4 Flyway — évolution du schéma

72 migrations V1 → V56 tracent l'évolution complète du schéma :

```
V1  — users + workspaces (init)
V3  — slug workspace (unique)
V4  — workspace_members (OWNER/ADMIN/MEMBER)
V10 — rollback optionnel (documenté)
V33 — member_skill_profiles
V44 — worklogs (charge de travail)
V47 — smart-assign metadata
V51 — Brain OS foundation (pgvector extension + brain_workspaces + knowledge_nodes)
V56 — dernière migration (schéma stable)
```

Aucune migration ne peut être modifiée après application (`ddl-auto=validate`).

---

## 5. Conception de l'architecture technique

### 5.1 Vue C4 — trois niveaux

**Niveau 1 — Contexte** : TaskForce (système) ↔ Utilisateur / Stripe / GitHub / Slack. Le modèle de langage est **auto-hébergé**, donc interne au système et non acteur externe

**Niveau 2 — Conteneurs** :

| Conteneur | Tech | Port (dev) |
|---|---|---|
| Frontend App | Next.js 16.1, React 19, TS 5, Tailwind 4 | 3000 |
| Backend API | Spring Boot 4, Java 21, Maven | 8080 |
| Landing | Astro 5.x | 4321 |
| PostgreSQL + pgvector | PostgreSQL 18 | 5432 |
| Keycloak | Custom (build dev) / 26 prod | 8180 |
| RabbitMQ | 4 + STOMP | 5672/61613 |
| MinIO | S3-compatible | 9000 |
| ai-service | FastAPI stub — **vestigial** (DT-010) | 8000 |

**Niveau 3 — Composants backend** :

```
shared ← core ← modules
  ↑          ↑         ↑
Config   Auth/WS    chat/ged/sales
Security  Business
Audit     Services
```

> 🔗 [[Architecture_C4]] — 3 niveaux Mermaid détaillés

### 5.2 Architecture frontend (Next.js App Router)

Organisation en groupes de routes :

| Groupe | Chemin | Accès |
|---|---|---|
| Authentification | `auth/login`, `auth/register/*` | Public |
| App protégée | `(protected)/[workspace]/**` | JWT valide + WorkspaceMember |
| Paiement | `payment/success`, `payment/cancel` | Public (retour Stripe) |
| Invitation | `invitations/[token]` | Public |
| Légal | `privacy-policy`, `legal-notices` | Public |

**Flux nominal d'une action** :

```
Page → Store Zustand → Service API → client Axios → /api/** → ApiResponse<T>
                ↑                                                      ↓
        use-stomp.ts ←──────── RabbitMQ/STOMP ←── @Scheduled / WebSocket
```

### 5.3 Règle de dépendance backend

```
shared ← core ← modules
```

- `shared` : configurations, DTOs globaux, `AuditableEntity`, `GlobalExceptionHandler`
- `core` : 18 contrôleurs, ~25 services, ~35 entités JPA, 19 enums
- `modules` : `chat/`, `ged/`, `sales/` — chacun isolé (ne dépend pas des autres modules)

**Violation = erreur de compilation** (Spring context fail si cycle de dépendance).

### 5.4 Temps réel — architecture STOMP

```
Browser ──SockJS/STOMP──▶ Backend :8080/ws-sockjs
                                    ↓
                            RabbitMQ :61613 (STOMP relay)
                            Topics : /topic/workspace.{id}.*
                                      /queue/user.{userId}
                            Fallback : SimpleBroker (in-memory)
```

---

## 6. Conception de la sécurité

### 6.1 Authentification — délégation Keycloak

```
Inscription (3 étapes) :
  1. POST /api/auth/register (données + plan)
  2. POST /api/auth/verify-otp (code 6 chiffres, TTL 15 min)
  3. POST /api/auth/complete-registration → création compte Keycloak + JWT

Login :
  → Keycloak OIDC (Resource Owner Password Grant)
  → tokens RS256 émis par Keycloak, validés par Spring OAuth2 Resource Server (JWK + issuer)
```

### 6.2 Autorisation — RBAC au niveau service

Trois niveaux de vérification dans les services :
1. **JWT valide** → `SecurityConfig` (filtre Spring Security)
2. **WorkspaceMember actif** → `AuthorizationService.getMemberOrThrow()`
3. **Rôle suffisant** → `requireManager()` (ADMIN+) ou `assertIsOwner()` (OWNER)

`ProjectMember` check additionnel pour les ressources de projet.

### 6.3 Posture OWASP Top 10

| Risque OWASP | Contre-mesure implémentée |
|---|---|
| A01 Broken Access Control | RBAC service-level + tests `WorkspaceMemberGuardTest` |
| A02 Crypto Failures | JWT RS256 (Keycloak) ; TLS prod (Nginx) ; secrets env vars ; AES-256-GCM PII |
| A03 Injection | JPA paramétré + `@Valid` Bean Validation |
| A07 Auth Failures | Keycloak gère bruteforce + refresh rotation |
| A09 Logging failures | `AuditLog` + SigNoz traces |

> 🔗 [[Sécurité.md]] — posture complète + résultats pentest ZAP/SAST Semgrep/SCA Trivy

---

## 7. Conception de l'observabilité

**Stack retenue** : OpenTelemetry Collector → SigNoz (traces + métriques + logs) +
Prometheus en complément (9 règles d'alerte).

```
Backend (OTLP gRPC :4317) ─▶ OTel Collector ─▶ SigNoz (visualisation)
                                              └─▶ Prometheus :8889 (alertes)
```

**9 règles Prometheus** couvrent : latence API, JVM heap, erreurs HTTP 5xx, disponibilité
services, saturation DB.

> 🔗 ADR-010 — `observability/otel-collector-config.yaml` — `observability/alerts/`

---

## 8. Décisions structurantes (synthèse ADR)

Les 10 décisions d'architecture qui ont le plus impacté la conception :

| ADR | Décision | Impact conception |
|---|---|---|
| ADR-001 | Spring Boot 4 + Maven + Java 21 | Tout le backend, 72 migrations Flyway |
| ADR-002 | Multi-tenant logique + OWNER/ADMIN/MEMBER | `workspace_id` sur 40+ tables ; `AuthorizationService` |
| ADR-003 / ADR-011 | Keycloak IdP ; tokens **OIDC RS256** émis par Keycloak (ex-JWT HS512, migré) | Inscription 3 étapes ; `SecurityConfig` OAuth2 RS |
| ADR-004 | ⚠️ **Périmé (23/07)**. Groq retiré le 16/07 (`TF-AI-GROQ-CLEANUP`), `GroqService` n'existe plus. Chemin réel : `LlmClient` puis `AiGatewayClient` puis `ai-service` puis Ollama Qwen3 local |
| ADR-005 | pgvector natif | `V51` + `KnowledgeNode.embedding vector(1536)` |
| ADR-006 | RabbitMQ + STOMP | Architecture temps réel WebSocket + relay |
| ADR-007 | No-mock. ⚠️ **Testcontainers n'est PAS utilisé** : incompatibilité du client docker-java avec le mandataire de Docker Desktop. Un PostgreSQL voisin est démarré par `scripts/it.ps1`, avec les vraies migrations Flyway |
| ADR-008 | Hybride FK `Long id` | AuditLog / Facturation survivent à la suppression |
| ADR-009 | Brain OS 1:1 workspace | `BrainWorkspace @OneToOne unique` ; knowledge graph isolé |
| ADR-010 | OTEL → SigNoz | Observabilité 3-piliers sans Grafana/Prometheus seul |

> 🔗 [[Journal_Decisions_ADR]] — contexte, alternatives, conséquences de chaque décision

---

## 9. Traçabilité exigences → conception

Extrait de la table de réconciliation complète :

| Exigence (CdCF / STB) | Artefact de conception | Implémentation |
|---|---|---|
| UC-01 Inscription OTP | Séquence 1 + `OtpVerification` (MLD) | `AuthService.verifyOtpAndCompleteRegistration` |
| UC-07 Smart-assign | Séquence 3 + `MemberSkillProfile`/`WorkLog` (MLD) | `SmartAssignService` puis `LlmClient` puis `ai-service` |
| SEC-01 Auth OIDC | C4 Keycloak + `SecurityConfig` | `JwtDecoderConfig`, `KeycloakConfig` |
| PERF-01 p95 < 200 ms | STB + Prometheus histogram | `otel-collector-config.yaml` |
| CAP-03 pgvector | ADR-005 + V51 | `knowledge_nodes.embedding vector(1536)` |
| INT-01 Stripe webhooks | Séquence 5 + `Subscription` (MLD) | `StripeWebhookController` |
| RGPD export | Séquence 6 + domaine Auth (MLD) | `GdprService.exportUserData` |

> 🔗 Table complète (~30 UC × 72 migrations × 72 tests) → [[Table_Reconciliation]]

---

## 10. Bilan de la phase de conception

### Ce qui a été conçu et livré

| Artefact | Statut | Preuve |
|---|---|---|
| MCD / MLD (7 domaines) | ✅ | `Modele_Donnees_MCD_MLD.md` — 55 tables/104 clés étrangères |
| Diagramme de classes UML (5 domaines) | ✅ | `Diagramme_Classes_UML.md` — 48 entités JPA |
| Diagramme de cas d'usage | ✅ | `Diagramme_Cas_Usage_UML.md` — 12 UC + 5 acteurs |
| Diagrammes de séquence (6) | ✅ | `Diagrammes_Sequence_UML.md` |
| Machines à états (5) | ✅ | `Diagramme_Etats_UML.md` |
| Architecture C4 (3 niveaux) | ✅ | `Architecture_C4.md` |
| Dictionnaire de données | ✅ | `Dictionnaire_Donnees.md` — 483 colonnes |
| Journal de décisions (10 ADR) | ✅ | `Journal_Decisions_ADR.md` |
| Table de réconciliation | ✅ | `Table_Reconciliation.md` |

### Écarts de conception (gaps → roadmap produit)

| Gap | Impact | Statut |
|---|---|---|
| ai-service Python | ⚠️ **Constat inversé le 23/07** : c'est la passerelle IA **active** (`AiGatewayClient` vers `ai-service` vers Ollama), pas un vestige. La dette DT-010 est à refermer, pas à traiter |
| Wireframes statiques | Aucun fichier `assets/maquettes/` — UI = code source | ⬜ Roadmap : captures annotées |
| Contraintes de transition issues | Board libre (pas de workflow imposé) — feature roadmap | ⬜ Roadmap V2 |
| Workspace sans champ statut | `Workspace` n'a pas de `status` — suppression = seule sortie | ⬜ Roadmap : soft-delete |

> **Ces gaps ne sont pas des oublis** : ils reflètent les choix de périmètre V1 ou des dettes
> techniques documentées. Voir [[Registre_Risques]] R03 (scope creep) et [[Problemes_Connus]].

---

> 🔗 Navigation : [[CdCF_v2]] · [[CdCT_v2]] · [[STB]] · [[Journal_Decisions_ADR]] ·
> [[Table_Reconciliation]] · [[Modele_Donnees_MCD_MLD]] · [[Diagramme_Classes_UML]] ·
> [[Diagrammes_Sequence_UML]] · [[Diagramme_Etats_UML]] · [[Architecture_C4]] ·
> [[Dictionnaire_Donnees]] · [[Diagramme_Cas_Usage_UML]]
