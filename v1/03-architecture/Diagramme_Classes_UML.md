---
id: diagramme-classes-uml
title: Diagramme de classes UML
doc_type: reference
statut: active
version: 2.0
date: "24/07/2026"
auteur: Pierre MICHEL
tags: [architecture, uml, classes, jpa, e8]
---

# Diagramme de classes UML

> **Livrable E8** (dossier de conception, compétence C8).
>
> **Ce document est GÉNÉRÉ**, il ne se modifie pas à la main. Source de vérité : les classes
> annotées `@Entity` du code réel. Aucune classe ni association n'est inventée.
>
> Régénération : `node scripts/generate-class-diagram.mjs` (voir §5).

## 1. Méthode et périmètre

- **48 entités JPA**, **13 héritant** de `AuditableEntity`, **84 associations** entre entités.
- **21 références par identifiant nu** (voir §4), qui ne sont pas des associations JPA.
- Extraction par analyse des annotations, commentaires et chaînes retirés au préalable.
- Les entités vivent majoritairement dans `core/model`, mais **pas exclusivement** : les modules
  métier portent les leurs. Restreindre l'extraction à `core/model` en oublierait.

> **Piège de comptage à connaître.** `@EntityListeners` contient la chaîne `@Entity` : un
> décompte par recherche textuelle simple inclut donc `AuditableEntity`, qui est un
> `@MappedSuperclass` et non une entité. Le compte exact est **48**, pas 49.

## 2. Vue par domaine

Le stéréotype `<<table>>` sous chaque classe donne sa table de rattachement, ce qui permet de
recouper ce diagramme avec le [modèle de données](./Modele_Donnees_MCD_MLD.md), généré depuis la
base par un script frère et partageant le même classement par domaine.

### 4.1 IAM et Workspace

Le socle multi-tenant. Toute donnée métier est rattachée à un workspace, et l'appartenance à un workspace conditionne l'accès.

**6 entités** : `Team`, `TeamMember`, `User`, `Workspace`, `WorkspaceInvitation`, `WorkspaceMember`.

```mermaid
classDiagram
  class Team {
    <<teams>>
  }
  class TeamMember {
    <<team_members>>
  }
  class User {
    <<users>>
    +Long companyId
  }
  class Workspace {
    <<workspaces>>
  }
  class WorkspaceInvitation {
    <<workspace_invitations>>
  }
  AuditableEntity <|-- WorkspaceInvitation
  class WorkspaceMember {
    <<workspace_members>>
  }
  Team "*" --> "1" Workspace : workspace
  Team "*" --> "1" User : createdBy
  TeamMember "*" --> "1" Team : team
  TeamMember "*" --> "1" User : user
  Workspace "*" --> "1" User : owner
  Workspace "1" --> "*" WorkspaceMember : members
  WorkspaceInvitation "*" --> "1" Workspace : workspace
  WorkspaceInvitation "*" --> "1" User : invitedBy
  WorkspaceMember "*" --> "1" Workspace : workspace
  WorkspaceMember "*" --> "1" User : user
  WorkspaceMember "*" --> "1" User : invitedBy
```

### 4.2 Projets et Issues (coeur métier)

Le domaine que le cahier des charges décrit : les tâches, leur affectation, la charge et les compétences qui la conditionnent.

**18 entités** : `Attachment`, `Cycle`, `CycleIssue`, `Issue`, `IssueActivity`, `IssueChecklistItem`, `IssueComment`, `IssueRelation`, `IssueSequenceCounter`, `IssueStatus`, `IssueType`, `IssueWorklog`, `MemberLeave`, `Project`, `ProjectFavorite`, `ProjectLabel`, `ProjectMember`, `ProjectTeam`.

```mermaid
classDiagram
  class Attachment {
    <<attachments>>
  }
  class Cycle {
    <<cycles>>
  }
  class CycleIssue {
    <<cycle_issues>>
  }
  class Issue {
    <<issues>>
  }
  class IssueActivity {
    <<issue_activity>>
  }
  class IssueChecklistItem {
    <<issue_checklist_items>>
    +Long issueId
  }
  class IssueComment {
    <<issue_comments>>
  }
  class IssueRelation {
    <<issue_relations>>
  }
  class IssueSequenceCounter {
    <<issue_sequence_counters>>
    +Long projectId
  }
  class IssueStatus {
    <<issue_statuses>>
  }
  class IssueType {
    <<issue_types>>
  }
  class IssueWorklog {
    <<issue_worklogs>>
    +Long issueId
  }
  class MemberLeave {
    <<member_leaves>>
    +Long workspaceId
    +Long userId
  }
  AuditableEntity <|-- MemberLeave
  class Project {
    <<projects>>
  }
  class ProjectFavorite {
    <<project_favorites>>
    +Long userId
    +Long projectId
  }
  class ProjectLabel {
    <<project_labels>>
  }
  class ProjectMember {
    <<project_members>>
  }
  class ProjectTeam {
    <<project_teams>>
  }
  Attachment "*" --> "1" Issue : issue
  Attachment "*" --> "1" User : uploadedBy
  Cycle "*" --> "1" Project : project
  Cycle "*" --> "1" User : createdBy
  CycleIssue "*" --> "1" Cycle : cycle
  CycleIssue "*" --> "1" Issue : issue
  CycleIssue "*" --> "1" User : addedBy
  Issue "*" --> "1" Project : project
  Issue "*" --> "1" IssueStatus : status
  Issue "*" --> "1" IssueType : type
  Issue "*" --> "1" User : assignee
  Issue "*" --> "1" User : reporter
  Issue "*" --> "1" Issue : parent
  Issue "1" --> "*" Issue : children
  Issue "*" --> "*" ProjectLabel : labels
  Issue "1" --> "*" IssueComment : comments
  Issue "1" --> "*" IssueActivity : activities
  IssueActivity "*" --> "1" Issue : issue
  IssueActivity "*" --> "1" User : actor
  IssueComment "*" --> "1" Issue : issue
  IssueComment "*" --> "1" User : author
  IssueRelation "*" --> "1" Issue : source
  IssueRelation "*" --> "1" Issue : target
  IssueRelation "*" --> "1" User : createdBy
  IssueSequenceCounter "1" --> "1" Project : project
  IssueStatus "*" --> "1" Project : project
  IssueType "*" --> "1" Project : project
  IssueWorklog "*" --> "1" User : user
  Project "*" --> "1" Workspace : workspace
  Project "*" --> "1" User : createdBy
  Project "1" --> "*" ProjectMember : members
  Project "1" --> "*" ProjectLabel : labels
  ProjectLabel "*" --> "1" Project : project
  ProjectMember "*" --> "1" Project : project
  ProjectMember "*" --> "1" User : user
  ProjectMember "*" --> "1" User : addedBy
  ProjectTeam "*" --> "1" Project : project
  ProjectTeam "*" --> "1" Team : team
```

### 4.3 IA, affectation intelligente et graphe de connaissances

Le moteur d'affectation et sa mémoire. `knowledge_nodes` porte les vecteurs d'embedding utilisés par la recherche sémantique.

**10 entités** : `AiConversation`, `AiMessage`, `AiTokenUsage`, `AnalysisJob`, `BrainWorkspace`, `DecisionBriefEntity`, `DecisionPriority`, `KnowledgeEdge`, `KnowledgeNode`, `SavedChart`.

```mermaid
classDiagram
  class AiConversation {
    <<ai_conversation>>
    +Long workspaceId
    +Long userId
    +Long summaryUptoId
  }
  AuditableEntity <|-- AiConversation
  class AiMessage {
    <<ai_message>>
    +Long conversationId
  }
  class AiTokenUsage {
    <<ai_token_usage>>
    +Long accountId
  }
  AuditableEntity <|-- AiTokenUsage
  class AnalysisJob {
    <<analysis_job>>
  }
  AuditableEntity <|-- AnalysisJob
  class BrainWorkspace {
    <<brain_workspaces>>
  }
  AuditableEntity <|-- BrainWorkspace
  class DecisionBriefEntity {
    <<decision_brief>>
  }
  AuditableEntity <|-- DecisionBriefEntity
  class DecisionPriority {
    <<decision_priority>>
  }
  AuditableEntity <|-- DecisionPriority
  class KnowledgeEdge {
    <<knowledge_edges>>
  }
  class KnowledgeNode {
    <<knowledge_nodes>>
    +Long refId
    +Long parentNodeId
  }
  AuditableEntity <|-- KnowledgeNode
  class SavedChart {
    <<saved_chart>>
  }
  AuditableEntity <|-- SavedChart
  AnalysisJob "*" --> "1" Workspace : workspace
  AnalysisJob "*" --> "1" Project : project
  AnalysisJob "*" --> "1" User : user
  AnalysisJob "1" --> "1" DecisionBriefEntity : brief
  BrainWorkspace "1" --> "1" Workspace : workspace
  DecisionBriefEntity "*" --> "1" Workspace : workspace
  DecisionBriefEntity "*" --> "1" Project : project
  DecisionBriefEntity "1" --> "*" DecisionPriority : priorities
  DecisionPriority "*" --> "1" DecisionBriefEntity : brief
  DecisionPriority "*" --> "1" Issue : issue
  KnowledgeEdge "*" --> "1" Workspace : workspace
  KnowledgeEdge "*" --> "1" KnowledgeNode : fromNode
  KnowledgeEdge "*" --> "1" KnowledgeNode : toNode
  KnowledgeNode "*" --> "1" Workspace : workspace
  KnowledgeNode "*" --> "1" BrainWorkspace : brain
  SavedChart "*" --> "1" Workspace : workspace
  SavedChart "*" --> "1" User : createdByUser
```

### 4.4 Authentification et sécurité

L'identité est déléguée à Keycloak. Ne subsistent ici que les données propres à l'application : codes à usage unique, jetons anti-CSRF, journal d'audit.

**3 entités** : `AuditLog`, `OAuthState`, `OtpVerification`.

```mermaid
classDiagram
  class AuditLog {
    <<audit_logs>>
    +Long workspaceId
    +Long actorUserId
  }
  class OAuthState {
    <<oauth_states>>
  }
  class OtpVerification {
    <<otp_verification>>
    +Long userId
  }
  OAuthState "*" --> "1" Workspace : workspace
  OAuthState "*" --> "1" User : user
```

### 4.5 Facturation

Abonnements et historique. Aucune donnée de carte n'est stockée : la facturation est déléguée au prestataire de paiement.

**2 entités** : `Subscription`, `SubscriptionHistory`.

```mermaid
classDiagram
  class Subscription {
    <<subscriptions>>
    +Long userId
  }
  class SubscriptionHistory {
    <<subscription_history>>
    +Long userId
  }
```

### 4.6 Intégrations et communications

Connecteurs externes et notifications. Les identifiants de connecteurs sont chiffrés en base (AES-256-GCM).

**6 entités** : `ConnectorConnection`, `Integration`, `IssueGitHubLink`, `Notification`, `SlackChannel`, `Webhook`.

```mermaid
classDiagram
  class ConnectorConnection {
    <<connector_connection>>
  }
  AuditableEntity <|-- ConnectorConnection
  class Integration {
    <<integrations>>
  }
  class IssueGitHubLink {
    <<issue_github_links>>
  }
  class Notification {
    <<notifications>>
  }
  class SlackChannel {
    <<slack_channels>>
  }
  class Webhook {
    <<webhooks>>
  }
  ConnectorConnection "*" --> "1" Workspace : workspace
  ConnectorConnection "*" --> "1" User : connectedBy
  Integration "*" --> "1" Workspace : workspace
  Integration "*" --> "1" User : installedBy
  IssueGitHubLink "*" --> "1" Issue : issue
  IssueGitHubLink "*" --> "1" User : linkedBy
  Notification "*" --> "1" User : recipient
  Notification "*" --> "1" Workspace : workspace
  Notification "*" --> "1" User : actor
  SlackChannel "*" --> "1" Workspace : workspace
  Webhook "*" --> "1" Workspace : workspace
  Webhook "*" --> "1" User : createdBy
```

### 4.7 Documentation, tableaux de bord et prospects

Pages de documentation collaborative, composition du tableau de bord par utilisateur, et demandes commerciales.

**3 entités** : `DashboardCard`, `EnterpriseInquiry`, `Page`.

```mermaid
classDiagram
  class DashboardCard {
    <<dashboard_cards>>
  }
  AuditableEntity <|-- DashboardCard
  class EnterpriseInquiry {
    <<enterprise_inquiries>>
    +Long userId
  }
  AuditableEntity <|-- EnterpriseInquiry
  class Page {
    <<pages>>
  }
  DashboardCard "*" --> "1" Workspace : workspace
  DashboardCard "*" --> "1" User : user
  Page "*" --> "1" Project : project
  Page "*" --> "1" User : createdBy
```

## 3. Héritage

`AuditableEntity` est un **`@MappedSuperclass`**, pas une entité : elle n'a pas de table propre,
ses colonnes sont recopiées dans chaque table fille. C'est ce qui explique qu'on retrouve
`created_at` et `updated_at` répétés au dictionnaire de données plutôt que dans une table commune.

**13 entités sur 48** en héritent :

- `AiConversation` (`ai_conversation`)
- `AiTokenUsage` (`ai_token_usage`)
- `AnalysisJob` (`analysis_job`)
- `BrainWorkspace` (`brain_workspaces`)
- `ConnectorConnection` (`connector_connection`)
- `DashboardCard` (`dashboard_cards`)
- `DecisionBriefEntity` (`decision_brief`)
- `DecisionPriority` (`decision_priority`)
- `EnterpriseInquiry` (`enterprise_inquiries`)
- `KnowledgeNode` (`knowledge_nodes`)
- `MemberLeave` (`member_leaves`)
- `SavedChart` (`saved_chart`)
- `WorkspaceInvitation` (`workspace_invitations`)

Les 35 autres portent leur horodatage elles-mêmes, ou n'en ont pas besoin
(tables de liaison, compteurs de séquence, jetons éphémères).

## 4. Le modèle hybride de références

Certaines clés étrangères sont portées par une **association JPA** (`@ManyToOne` vers l'entité
cible), d'autres par un **identifiant nu** (`Long xxxId`). Ce n'est pas une incohérence mais un
arbitrage : l'association donne la navigation et le chargement paresseux, l'identifiant nu évite
un couplage de cycle de vie là où il serait nuisible.

Le cas emblématique est le journal d'audit : conserver un identifiant nu permet à la trace de
**survivre à l'anonymisation** du compte qu'elle référence, ce qu'une association avec cascade
aurait empêché. Une contrainte `ON DELETE SET NULL` complète le dispositif côté base.

**21 références de ce type** sont recensées :

| Entité | Références par identifiant |
|---|---|
| `AiConversation` | `workspaceId`, `userId`, `summaryUptoId` |
| `AiMessage` | `conversationId` |
| `AiTokenUsage` | `accountId` |
| `AuditLog` | `workspaceId`, `actorUserId` |
| `EnterpriseInquiry` | `userId` |
| `IssueChecklistItem` | `issueId` |
| `IssueSequenceCounter` | `projectId` |
| `IssueWorklog` | `issueId` |
| `KnowledgeNode` | `refId`, `parentNodeId` |
| `MemberLeave` | `workspaceId`, `userId` |
| `OtpVerification` | `userId` |
| `ProjectFavorite` | `userId`, `projectId` |
| `Subscription` | `userId` |
| `SubscriptionHistory` | `userId` |
| `User` | `companyId` |

## 5. Régénération

```bash
node scripts/generate-class-diagram.mjs
```

Le script **échoue volontairement** si une entité n'a pas de `@Table` explicite, ou si sa table
n'est classée dans aucun domaine de `scripts/lib/domaines.mjs`. Ce classement est partagé avec le
générateur du modèle de données : deux classifications séparées auraient divergé, ce qui est
exactement le défaut que ces scripts corrigent.

Variante non destructive, utilisable en intégration continue :

```bash
node scripts/generate-class-diagram.mjs --check
```

> Voir aussi : [[Modele_Donnees_MCD_MLD]] · [[Dictionnaire_Donnees]] · [[Architecture_C4]].
