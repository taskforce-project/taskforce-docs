---
id: diagrammes-sequence-uml
title: Diagrammes de séquence (UML) — parcours clés
doc_type: conception
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [uml, sequence, parcours, auth, otp, stripe, redistribution, rgpd, conception, memoire, rncp]
---

# 🔀 Diagrammes de séquence (UML) — parcours clés

> **But** : décrire les **enchaînements d'appels réels** des parcours critiques, du contrôleur aux
> services et systèmes externes. Chaque flèche correspond à un appel **présent dans le code**
> (`AuthService`, `SmartAssignService`, `RedistributionService`, `GdprService`, `Stripe*`).
> Aucune étape n'est inventée ; les points non implémentés sont notés, pas dessinés.
>
> **Sources** : `core/api/*Controller.java`, `core/service/*Service.java` (backend `tf-api`).

---

## 1. Inscription + OTP + paiement (onboarding)

> ⚠️ **Fait vérifié** : l'**OTP est utilisé à l'INSCRIPTION** (pas au login). L'utilisateur est créé
> dans **Keycloak** dès `register`, l'e-mail est vérifié par OTP, puis (plan payant) via **Stripe
> Checkout**. Preuve : `AuthService.register` / `verifyOtpAndCompleteRegistration` /
> `completeRegistrationAfterPayment`.

```mermaid
sequenceDiagram
    autonumber
    actor U as Utilisateur
    participant AC as AuthController
    participant AS as AuthService
    participant KC as Keycloak
    participant OTP as OtpService
    participant MAIL as EmailService
    participant WS as WorkspaceService
    participant JWT as JwtService

    U->>AC: POST /auth/register (email, pwd, plan)
    AC->>AS: register(request)
    AS->>KC: createUser(email, pwd)
    AS->>OTP: generateOtp(email)
    AS->>MAIL: envoi code OTP
    AS-->>U: 200 (OTP envoyé)

    U->>AC: POST /auth/verify-otp (email, code)
    AC->>AS: verifyOtpAndCompleteRegistration
    AS->>OTP: verifyOtpAndGetDetails(email, code)
    OTP-->>AS: OtpVerification (ou null → 400)
    AS->>KC: verifyEmail(keycloakId)
    AS->>AS: userRepository.save(user)
    AS->>WS: createWorkspace(user)
    AS->>MAIL: sendWelcomeEmail
    AS->>JWT: generateTokens(user)
    AS-->>U: 200 (accessToken + refreshToken)

    note over U,AS: Plan PAYANT → redirection Stripe Checkout,<br/>puis GET /stripe/verify-session →<br/>completeRegistrationAfterPayment
```

---

## 2. Connexion (login)

> ⚠️ Le login **délègue l'authentification à Keycloak** (`keycloakAuthService.authenticate`), pas à un
> hash local. Auto-provisionnement du `User` en DB si absent de Keycloak. Journalisé (`USER_LOGIN`).

```mermaid
sequenceDiagram
    autonumber
    actor U as Utilisateur
    participant AC as AuthController
    participant AS as AuthService
    participant KC as Keycloak
    participant INV as WorkspaceInvitationService
    participant JWT as JwtService
    participant AUD as AuditService

    U->>AC: POST /auth/login (email, pwd)
    AC->>AS: login(request)
    AS->>KC: authenticate(email, pwd)
    alt échec
        KC-->>AS: exception
        AS-->>U: 401 (identifiants incorrects)
    else succès
        KC-->>AS: OK
        AS->>KC: getUserByEmail → emailVerified ?
        AS->>AS: findByKeycloakId (crée si absent)
        AS->>INV: acceptPendingInvitations(user)
        AS->>JWT: generateTokens(user)
        AS->>AUD: record(USER_LOGIN)
        AS-->>U: 200 (tokens)
    end
```

---

## 3. Affectation intelligente (smart-assign) — ⭐ cœur CDC

> Scoring d'un candidat = **compétences** (`member_skill_profiles`, SQL brut) × **charge réelle
> cross-projets** (`IssueWorklog`) × **disponibilité** (`MemberLeave`), affiné par un **LLM Groq**
> (`groq.scores()` / `groq.reasons()`). Preuve : `SmartAssignService.recommend` / `rankForRedistribution`.

```mermaid
sequenceDiagram
    autonumber
    actor M as Membre
    participant IC as IssueController
    participant SA as SmartAssignService
    participant DB as (member_skill_profiles / worklog / leave)
    participant GROQ as Groq LLM

    M->>IC: GET /issues/{id}/smart-assign
    IC->>SA: recommend(workspace, project, issue)
    SA->>DB: fetchProfileSkills (skills_json)
    SA->>DB: charge cross-projets (IssueWorklog)
    SA->>DB: disponibilité (MemberLeave)
    SA->>GROQ: scores(candidats, contexte issue)
    GROQ-->>SA: scores + justifications
    SA->>SA: rankCandidates (métriques + LLM)
    SA-->>M: SmartAssignResponse (candidats classés + raisons)
```

---

## 4. Redistribution automatique (proposer → valider) — ⭐ cœur CDC

> **Manager only** (`requireManager`). `preview` calcule un **plan** sans rien modifier ; `apply`
> exécute les déplacements validés via `IssueService.updateIssue` (réutilise activité, temps réel,
> notifications) puis **journalise** (`REDISTRIBUTION_APPLY`). Preuve : `RedistributionService`.

```mermaid
sequenceDiagram
    autonumber
    actor G as Gestionnaire
    participant RC as RedistributionController
    participant RS as RedistributionService
    participant AUTH as AuthorizationService
    participant SA as SmartAssignService
    participant IS as IssueService
    participant AUD as AuditService

    G->>RC: GET /redistribution/preview (targetUser?)
    RC->>RS: preview(slug, userId, targetUserId)
    RS->>AUTH: requireManager (403 sinon)
    loop pour chaque issue à déplacer
        RS->>SA: rankForRedistribution(issue)
        SA-->>RS: candidats classés
        RS->>RS: pickTarget (exclut la source, respecte capacité)
    end
    RS-->>G: RedistributionPlanResponse (moves + charges projetées)

    G->>RC: POST /redistribution/apply (moves validés)
    RC->>RS: apply(slug, userId, request)
    RS->>AUTH: requireManager
    loop pour chaque move validé
        RS->>IS: updateIssue(assignee)
    end
    RS->>AUD: record(REDISTRIBUTION_APPLY, count)
    RS-->>G: ApplyRedistributionResponse (applied / skipped)
```

---

## 5. Paiement Stripe (abonnement)

> Deux chemins : **Checkout** (souscription → `verify-session` → finalisation) et **Webhooks**
> entrants (source de vérité de l'état d'abonnement), authentifiés par **signature**
> (`Webhook.constructEvent`). Idempotents via `stripe_event_id` unique. Preuve :
> `StripeController` / `StripeWebhookController` / `StripeWebhookService`.

```mermaid
sequenceDiagram
    autonumber
    actor U as Utilisateur
    participant STC as StripeController
    participant AS as AuthService
    participant STRIPE as Stripe
    participant SWC as StripeWebhookController
    participant SWS as StripeWebhookService

    U->>STRIPE: Stripe Checkout (paiement)
    U->>STC: GET /stripe/verify-session?session_id=...
    STC->>AS: completeRegistrationAfterPayment(sessionId)
    AS-->>U: 200 (inscription finalisée)

    STRIPE->>SWC: POST /webhooks/stripe (event + signature)
    SWC->>SWC: Webhook.constructEvent (vérif signature)
    alt signature invalide
        SWC-->>STRIPE: 400
    else valide
        alt type d'événement
            SWC->>SWS: handleCheckoutSessionCompleted
            SWC->>SWS: handleSubscriptionUpdated / Deleted
            SWC->>SWS: handleInvoicePaymentSucceeded / Failed
        end
        SWC-->>STRIPE: 200 (idempotent)
    end
```

---

## 6. Export RGPD (portabilité — Art. 20)

> `@Transactional` **en écriture** (et non `readOnly`) car l'export **écrit un log d'audit** — un
> `readOnly` provoquait une `SQLSTATE 25006` (corrigé, cf. [[Problemes_Connus]] PC / QF-5). Agrège
> profil + memberships + compétences (SQL brut) + worklogs. Preuve : `GdprService.exportMyData`.

```mermaid
sequenceDiagram
    autonumber
    actor U as Utilisateur
    participant GC as GdprController
    participant GS as GdprService
    participant DB as PostgreSQL

    U->>GC: GET /gdpr/export
    GC->>GS: exportMyData(userId)
    GS->>DB: user (profil)
    GS->>DB: workspaceMemberRepository.findByUserId (memberships)
    GS->>DB: member_skill_profiles (SQL brut)
    GS->>DB: IssueWorklog.findByUser (temps loggé)
    GS-->>U: JSON complet (portabilité)
```

---

## 7. Traçabilité

| Diagramme | Preuve principale |
|---|---|
| Inscription + OTP | `AuthService.register` / `verifyOtpAndCompleteRegistration` |
| Login Keycloak | `AuthService.login` (`keycloakAuthService.authenticate`) |
| Smart-assign | `SmartAssignService.recommend` / `rankForRedistribution` (Groq + SQL) |
| Redistribution | `RedistributionService.preview` / `apply` (`requireManager`, audit) |
| Stripe | `StripeController.verifySession` + `StripeWebhookController` (5 événements) |
| Export RGPD | `GdprService.exportMyData` (`@Transactional`) |

> 🔗 Voir aussi : [[Diagramme_Cas_Usage_UML]] · [[Diagramme_Classes_UML]] · [[Sécurité]] ·
> [[Roadmap_Documentation|plan de production doc]].
