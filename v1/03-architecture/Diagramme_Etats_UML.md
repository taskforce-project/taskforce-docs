---
id: diagramme-etats-uml
title: Diagrammes d'états / d'activité (UML) — cycles de vie
doc_type: conception
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [uml, etats, state-machine, activite, cycle-de-vie, issue, invitation, abonnement, conception, memoire, rncp]
---

# 🔄 Diagrammes d'états / d'activité (UML) — cycles de vie

> **But** : formaliser les **cycles de vie** des objets à états de TaskForce. **Seules les machines à
> états réellement présentes** (enums Java `@Enumerated`) sont modélisées.
>
> ⚠️ **Deux faits vérifiés qui cadrent ce document** :
> 1. **Les transitions d'issue ne sont PAS contraintes** par le code (`IssueService` ne valide aucune
>    transition) → mouvement **libre** sur le board. Les *catégories* de statut portent la **sémantique**
>    (quel statut compte comme « terminé »), **pas** une FSM stricte. On ne dessine donc **aucune
>    transition interdite** (ce serait inventé).
> 2. **`Workspace` n'a pas de champ statut** → pas de machine à états de workspace ; son cycle se résume
>    à *créé → (actif) → supprimé* (hard-delete `deleteWorkspace`, OWNER only).
>
> **Sources** : `core/enums/*.java` (`IssueStatusCategory`, `InvitationStatus`, `CycleStatus`,
> `PlanStatus`), `core/service/*`.

---

## 1. Cycle de vie d'une **issue** (sémantique de catégorie)

Chaque `IssueStatus` (défini **par projet**, personnalisable) porte une **catégorie**
(`IssueStatusCategory`) parmi 5 valeurs. C'est la catégorie — pas le nom du statut — qui donne le sens.

```mermaid
stateDiagram-v2
    direction LR
    [*] --> BACKLOG
    BACKLOG --> UNSTARTED
    UNSTARTED --> STARTED
    STARTED --> COMPLETED
    COMPLETED --> [*]
    BACKLOG --> CANCELLED
    UNSTARTED --> CANCELLED
    STARTED --> CANCELLED
    CANCELLED --> [*]

    note right of STARTED
      Transitions LIBRES : le board autorise
      tout statut → tout statut. Les flèches
      ci-dessus = flux NOMINAL, pas une
      contrainte (aucune validation en code).
    end note
```

> **Preuve** : enum `IssueStatusCategory { BACKLOG, UNSTARTED, STARTED, COMPLETED, CANCELLED }` ;
> `IssueStatus.category` (`@Enumerated(STRING)`). Absence de garde de transition dans `IssueService`.
> `COMPLETED`/`CANCELLED` = catégories terminales **sémantiquement** (ex. exclues de la charge active
> du smart-assign), pas verrouillées techniquement.

---

## 2. Cycle de vie d'une **invitation** (FSM réelle)

Contrairement à l'issue, l'invitation **a** une machine à états dirigée (`InvitationStatus`).

```mermaid
stateDiagram-v2
    direction LR
    [*] --> PENDING : invitation créée (manager)
    PENDING --> ACCEPTED : login/accept du destinataire
    PENDING --> REVOKED : annulée par un manager
    PENDING --> EXPIRED : délai dépassé
    ACCEPTED --> [*]
    REVOKED --> [*]
    EXPIRED --> [*]
```

> **Preuve** : enum `InvitationStatus { PENDING, ACCEPTED, REVOKED, EXPIRED }` ;
> `WorkspaceInvitationService` (création manager, `acceptPendingInvitations` au login).

---

## 3. Cycle de vie d'un **cycle** (sprint)

```mermaid
stateDiagram-v2
    direction LR
    [*] --> DRAFT
    DRAFT --> ACTIVE : démarrage
    ACTIVE --> COMPLETED : clôture
    COMPLETED --> [*]
```

> **Preuve** : enum `CycleStatus { DRAFT, ACTIVE, COMPLETED }` (`core/enums/CycleStatus.java`).

---

## 4. Cycle de vie d'un **abonnement** (piloté par Stripe)

L'état d'abonnement (`PlanStatus`) est la **projection des événements Stripe** (webhooks) — voir
[[Diagrammes_Sequence_UML]] §5. TaskForce ne décide pas seul de ces transitions : elles reflètent Stripe.

```mermaid
stateDiagram-v2
    direction LR
    [*] --> TRIALING : période d'essai
    [*] --> INCOMPLETE : paiement initial en attente
    TRIALING --> ACTIVE : paiement réussi
    INCOMPLETE --> ACTIVE : paiement réussi
    INCOMPLETE --> INCOMPLETE_EXPIRED : abandon
    ACTIVE --> PAST_DUE : échec de paiement
    PAST_DUE --> ACTIVE : régularisation
    PAST_DUE --> UNPAID : échecs répétés
    ACTIVE --> CANCELED : résiliation
    UNPAID --> CANCELED
    CANCELED --> [*]
    INCOMPLETE_EXPIRED --> [*]
```

> **Preuve** : enum `PlanStatus { ACTIVE, CANCELED, PAST_DUE, TRIALING, INCOMPLETE, INCOMPLETE_EXPIRED,
> UNPAID }` (miroir des statuts Stripe) ; `StripeWebhookService.handleSubscription*`.
> ⚠️ Les flèches reflètent la **sémantique Stripe** ; TaskForce **applique** ces états, il n'impose pas
> ses propres règles de transition dessus.

---

## 5. Diagramme d'activité — **redistribution automatique** (⭐)

Vue « processus » du parcours manager (complète la séquence [[Diagrammes_Sequence_UML]] §4).

```mermaid
flowchart TD
    A([Gestionnaire demande un aperçu]) --> B{requireManager ?}
    B -- non --> B1[["403 Forbidden"]]
    B -- oui --> C[Pour chaque issue :<br/>rankForRedistribution]
    C --> D[pickTarget<br/>exclut la source, respecte la capacité]
    D --> E[/Plan proposé :<br/>moves + charges projetées/]
    E --> F{Le manager valide ?}
    F -- non --> G([Abandon, aucune écriture])
    F -- oui --> H[apply : updateIssue par move]
    H --> I[Audit REDISTRIBUTION_APPLY]
    I --> J([applied / skipped])
```

> **Preuve** : `RedistributionService.preview` (lecture seule, aucun effet) puis `apply` (écriture +
> audit). Conforme au CDC : **proposition auto → validation manager**.

---

## 6. Traçabilité

| Machine à états | Enum (preuve) | Contrainte de transition |
|---|---|---|
| Issue (catégorie) | `IssueStatusCategory` | **Aucune** (board libre) |
| Invitation | `InvitationStatus` | FSM dirigée (`WorkspaceInvitationService`) |
| Cycle | `CycleStatus` | linéaire |
| Abonnement | `PlanStatus` | dictée par Stripe (webhooks) |
| Workspace | — *(pas de champ statut)* | créé → supprimé (hard-delete OWNER) |

> 🔗 Voir aussi : [[Diagrammes_Sequence_UML]] · [[Diagramme_Classes_UML]] · [[Modele_Donnees_MCD_MLD]] ·
> [[Roadmap_Documentation|plan de production doc]].
