---
id: table-reconciliation
title: Table de réconciliation — UC ↔ entité ↔ migration ↔ test
doc_type: reference
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [tracabilite, matrice, reconciliation, uc, entite, migration, test, memoire, rncp]
---

# 🔗 Table de réconciliation — UC ↔ entité ↔ migration ↔ test

> **But** : matrice de **traçabilité** reliant chaque fonctionnalité (cas d'usage) à sa (ses) **entité(s)**,
> à la **migration Flyway** qui crée le schéma, et au **test** qui la couvre. Preuve de cohérence de bout
> en bout : *besoin → conception → réalisation → vérification*.
>
> **Sources vérifiées** : [[Diagramme_Cas_Usage_UML]] (UC), [[Diagramme_Classes_UML]] (entités),
> `db/migration/V*.sql` (56 migrations), `src/test/**/*Test.java` (72 fichiers de tests).
> **Aucune ligne inventée** : chaque migration et chaque test cités **existent** dans le dépôt.

---

## Matrice principale

| Cas d'usage | Entité(s) principale(s) | Migration(s) Flyway | Test(s) représentatif(s) |
|---|---|---|---|
| **Inscription + OTP** | `User`, `OtpVerification` | `V1`, `V2`, `V3`, `V4` | `AuthServiceTest`, `OtpServiceTest`, `AuthControllerWebMvcTest` |
| **Connexion (Keycloak/JWT)** | `User`, `RefreshToken` | `V1`, `V2`, `V3` | `AuthServiceTest`, `KeycloakAuthServiceTest`, `JwtServiceTest`, `JwtIdentityResolverTest` |
| **Nettoyage tokens** | `RefreshToken` | `V2` | `TokenCleanupSchedulerTest` |
| **Gérer workspace & membres** | `Workspace`, `WorkspaceMember` | `V13`, `V14` | `WorkspaceServiceIntegrationTest` |
| **Inviter des membres** | `WorkspaceInvitation` | `V42` | `WorkspaceInvitationServiceIntegrationTest` |
| **Gérer projets** | `Project`, `ProjectMember`, `ProjectLabel` | `V15`, `V19`–`V21`, `V37`, `V41`, `V43`, `V45` | `ProjectServiceIntegrationTest`, `ProjectControllerWebMvcTest` |
| **Gérer équipes** | `Team`, `TeamMember`, `ProjectTeam` | `V26`, `V43` | `TeamServiceIntegrationTest` |
| **Gérer issues** | `Issue`, `IssueStatus`, `IssueType`, `IssueComment`, `IssueChecklistItem` | `V16`, `V21`, `V22`, `V38`, `V39`, `V50` | `IssueServiceIntegrationTest`, `IssueRepositoryIntegrationTest`, `IssueControllerWebMvcTest` |
| **Relations d'issues** | `IssueRelation` | `V22` | `IssueServiceIntegrationTest` |
| **Logger du temps** | `IssueWorklog` | `V47` | `IssueServiceIntegrationTest` |
| **Cycles (sprints)** | `Cycle`, `CycleIssue` | `V23` | `CycleServiceIntegrationTest` |
| **Pages (wiki)** | `Page` | `V25` | `PageServiceIntegrationTest` |
| **⭐ Smart-assign** | `MemberSkillProfile`, `IssueWorklog`, `MemberLeave` | `V33`, `V34`, `V44`, `V46`, `V47`, `V49` | `SmartAssignServiceTest` |
| **⭐ Redistribution auto** | `Issue` (+ smart-assign) | `V16`, `V47` | `RedistributionServiceTest`, `RedistributionControllerWebMvcTest` |
| **Alerte de surcharge** | `MemberLeave`, `IssueWorklog` | `V47`, `V49` | `OverloadAlertSchedulerTest` |
| **Profils de compétences** | `member_skill_profiles` *(SQL brut)* | `V33`, `V44`, `V46` | `MemberSkillProfileServiceIntegrationTest` |
| **Congés** | `MemberLeave` | `V49` | `MemberLeaveServiceIntegrationTest` |
| **Paiement / abonnement** | `Subscription`, `SubscriptionHistory`, `User` | `V2`, `V3`, `V36` | `StripeServiceTest`, `StripeWebhookServiceTest` |
| **Chat temps réel** | `Channel`, `ChannelMember`, `ChatMessage` | `V28` | `ChatServiceIntegrationTest`, `ChatWebSocketControllerTest`, `StompAuthInterceptorTest` |
| **Discussions** | `Discussion` | `V27` | `DiscussionServiceIntegrationTest` |
| **Notifications** | `Notification` | `V24` | `NotificationServiceTest` |
| **Intégration GitHub** | `Integration`, `IssueGitHubLink` | `V30` | `GitHubIntegrationServiceIntegrationTest`, `GitHubIntegrationContractTest` |
| **Intégration Slack** | `Integration`, `SlackChannel` | `V30` | `SlackIntegrationServiceIntegrationTest`, `SlackIntegrationContractTest` |
| **Webhooks** | `Webhook` | `V30` | `WebhookServiceIntegrationTest` |
| **GED / pièces jointes** | `Attachment` | `V29` | `AttachmentServiceIntegrationTest`, `AttachmentControllerWebMvcTest` |
| **Leads entreprise (sales)** | `enterprise_inquiries` | `V8`, `V9`, `V11` | `SalesServiceIntegrationTest`, `SalesControllerWebMvcTest` |
| **Assistant IA** | `ai_runs`, `ai_documents`, `ai_insight_snapshots` | `V32`, `V35` | `AssistantServiceTest`, `AssistantControllerWebMvcTest`, `GroqServiceTest` |
| **Brain OS (knowledge graph)** | `BrainWorkspace`, `KnowledgeNode`, `KnowledgeEdge` | `V51`–`V56` | `CreateNoteToolTest`, `SearchBrainToolTest`, `AgentServiceTest`, `EmbeddingClientTest` |
| **Analytics** | *(issues / worklog agrégés)* | — *(lecture)* | `AnalyticsServiceIntegrationTest` |
| **Journal d'audit** | `AuditLog` | `V48` | *(couvert via services : `RedistributionServiceTest`, etc.)* |
| **Export RGPD** | `User` + agrégats | — *(lecture)* | `GdprServiceIntegrationTest` |
| **Utilisateurs / profil** | `User` | `V12` | `UserServiceIntegrationTest` |

---

## Cas transverses (sécurité & qualité)

| Aspect | Mécanisme | Test(s) |
|---|---|---|
| **Autorisation RBAC** | `AuthorizationService` (`requireMember`/`requireManager`) | `AuthorizationServiceTest` |
| **En-têtes de sécurité (OWASP A05)** | filtres / config sécurité | `SecurityHeadersWebMvcTest` |
| **Rate limiting** | `RateLimitFilter` | `RateLimitFilterTest` |
| **Chiffrement au repos** | `EncryptedStringConverter` (JPA converter) | `EncryptedStringConverterTest` |
| **Gestion d'erreurs normalisée** | `GlobalExceptionHandler` (`ApiResponse<T>`) | `GlobalExceptionHandlerTest` |
| **Logs client (front)** | `ClientLogController` | `ClientLogControllerWebMvcTest` |

---

## Notes de traçabilité

- **56 migrations** Flyway (`V1`→`V56`), dont des migrations de **seed dev/QA** (`V17`, `V18`, `V31`,
  `V40`) — schéma **et** données de démo (jamais de mock frontend, cf. politique projet).
- **72 fichiers de tests** : `*WebMvcTest` (slices contrôleurs), `*IntegrationTest` (Testcontainers),
  `*ServiceTest` (unitaires Mockito), `*ContractTest` (intégrations externes).
- **Écarts / manques éventuels** entre UC et couverture → tracés dans [[Problemes_Connus]] /
  [[Roadmap_Backlog]], **jamais comblés par une ligne fictive** ici.

> 🔗 Voir aussi : [[Diagramme_Cas_Usage_UML]] · [[Diagramme_Classes_UML]] · [[Dictionnaire_Donnees]] ·
> `08-operations/Tests.md` (stratégie de tests) · [[Roadmap_Documentation]].
