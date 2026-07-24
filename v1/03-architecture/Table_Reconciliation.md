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
> `db/migration/V*.sql` (72 migrations), `src/test/**/*Test.java` (72 fichiers de tests).
> **Aucune ligne inventée** : chaque migration et chaque test cités **existent** dans le dépôt.

---

## Matrice principale

| Cas d'usage | Entité(s) principale(s) | Migration(s) Flyway | Test(s) représentatif(s) |
|---|---|---|---|
| **Inscription + OTP** | `User`, `OtpVerification` | `V1`, `V2`, `V3`, `V4` | `AuthServiceTest`, `OtpServiceTest`, `AuthControllerWebMvcTest` |
| **Connexion (Keycloak OIDC RS256)** | `User` | `V1`, `V2`, `V3` | `AuthServiceTest`, `KeycloakAuthServiceTest`, `JwtIdentityResolverTest` |
| ~~**Nettoyage tokens**~~ | — | — | *Retiré (ADR-011) : tokens gérés par Keycloak ; `TokenCleanupScheduler` + table `refresh_tokens` custom abandonnés.* |
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
| **Chat temps réel** | `Channel`, `ChannelMember`, `ChatMessage` | `V28` | `StompAuthInterceptorTest` (sécurité du transport) — ⚠️ **aucun test de service ni de contrôleur** : `ChatServiceIntegrationTest` et `ChatWebSocketControllerTest` étaient cités mais **n'existent pas** (vérifié le 23/07/2026) |
| **Discussions** | `Discussion` | `V27` | ⚠️ **aucun test** : `DiscussionServiceIntegrationTest` était cité mais **n'existe pas** (vérifié le 23/07/2026) |
| **Notifications** | `Notification` | `V24` | `NotificationServiceTest` |
| **Intégration GitHub** | `Integration`, `IssueGitHubLink` | `V30` | `GitHubIntegrationServiceIntegrationTest`, `GitHubIntegrationContractTest` |
| **Intégration Slack** | `Integration`, `SlackChannel` | `V30` | `SlackIntegrationServiceIntegrationTest`, `SlackIntegrationContractTest` |
| **Webhooks** | `Webhook` | `V30` | `WebhookServiceIntegrationTest` |
| **GED / pièces jointes** | `Attachment` | `V29` | `AttachmentServiceIntegrationTest`, `AttachmentControllerWebMvcTest` |
| **Leads entreprise (sales)** | `enterprise_inquiries` | `V8`, `V9`, `V11` | `SalesServiceIntegrationTest`, `SalesControllerWebMvcTest` |
| **Assistant IA** | `ai_runs`, `ai_documents`, `ai_insight_snapshots` | `V32`, `V35` | `AssistantControllerWebMvcTest`, `AiConversationServiceTest`, `AiUsageServiceTest`, `BrainIngestionServiceTest` — `AssistantServiceTest` et `GroqServiceTest` étaient cités et **n'existent pas**, ce dernier n'ayant plus d'objet depuis le retrait de Groq |
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

- **72 migrations** Flyway (`V1` à `V72`), dont des migrations de **seed dev/QA** (`V17`, `V18`, `V31`,
  `V40`) — schéma **et** données de démo (jamais de mock frontend, cf. politique projet).
- **72 fichiers de tests** : `*WebMvcTest` (slices contrôleurs), `*IntegrationTest` (vrai Postgres voisin, pas Testcontainers),
  `*ServiceTest` (unitaires Mockito), `*ContractTest` (intégrations externes).
- **Écarts / manques éventuels** entre UC et couverture → tracés dans [[Problemes_Connus]] /
  [[Roadmap_Backlog]], **jamais comblés par une ligne fictive** ici.

> 🔗 Voir aussi : [[Diagramme_Cas_Usage_UML]] · [[Diagramme_Classes_UML]] · [[Dictionnaire_Donnees]] ·
> `08-operations/Tests.md` (stratégie de tests) · [[Roadmap_Documentation]].

---

## Contrôle d'intégrité des preuves

**Vérifié le 23/07/2026.** Les **53 classes de test citées** dans ce document ont été confrontées une
à une aux fichiers réellement présents dans le dépôt. **Cinq n'existaient pas.**

Une table de traçabilité dont les preuves sont introuvables est pire qu'une absence de table : elle
donne une assurance fausse, et un jury qui vérifie une seule ligne au hasard perd confiance dans
toutes les autres. Les cinq références ont été traitées selon leur cause :

| Référence citée | Cause | Traitement |
|---|---|---|
| `GroqServiceTest` | La classe testée a été supprimée avec Groq | Retirée |
| `AssistantServiceTest` | N'a jamais existé sous ce nom | Remplacée par les tests IA réels |
| `ChatServiceIntegrationTest` | N'existe pas | **Trou de couverture déclaré** |
| `ChatWebSocketControllerTest` | N'existe pas | **Trou de couverture déclaré** |
| `DiscussionServiceIntegrationTest` | N'existe pas | **Trou de couverture déclaré** |

Les trois derniers ne sont pas des erreurs de nommage : **le chat et les discussions n'ont aucun
test de service ni de contrôleur**. Seule la sécurité du transport temps réel est couverte
(`StompAuthInterceptorTest`). Ces domaines sont hors du périmètre du cahier des charges, ce qui
explique la priorité qui leur a été donnée, mais le fait doit être énoncé plutôt que masqué.

Ce contrôle est reproductible : extraire les identifiants entre accents graves se terminant par
`Test`, puis vérifier l'existence du fichier correspondant sous `src/test` et `frontend`.
