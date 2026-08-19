---
id: systeme-paiement-stripe
title: Système de paiement Stripe — TaskForce V1
doc_type: technique
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [stripe, paiement, webhook, subscription, billing, memoire, rncp, soutenance]
---

# 💳 Système de paiement Stripe — TaskForce V1

> Documentation de l'intégration Stripe : plans tarifaires, Checkout, webhooks,
> portail de facturation et cycle de vie des abonnements.
>
> **Fichiers de référence** :
> - `core/api/StripeController.java`
> - `core/api/StripeWebhookController.java`
> - `core/api/BillingController.java`
> - `core/service/StripeWebhookService.java`
> - `core/service/AuthService.java` (completeRegistrationAfterPayment)
> - Migrations : `V8__subscriptions.sql` · `V9__subscription_history.sql`

---

## 1. Plans tarifaires

| Plan | Prix | Limites | Cible |
|---|---|---|---|
| **FREE** | 0 € | 3 projets · 5 membres · pas d'IA | Équipes solo / test |
| **PRO** | 13 €/user/mois | Illimité · IA incluse · toutes intégrations | PME / startups |
| **ENTERPRISE** | 18–25 €/user/mois | Illimité + SSO + SLA + support dédié | Grandes entreprises |

**Source** : `PlanType` enum · `Business_Model_Pricing.md` · landing page `landing-page/`.

---

## 2. Architecture de l'intégration

```
Utilisateur                Backend                    Stripe
──────────                 ───────                    ──────
  Inscription étape 2
  Choix du plan ─────────▶ POST /api/auth/select-plan
                            (stocké en session/DB)

  Stripe Checkout
  (plan PRO/Enterprise) ──▶ AuthService
                              .completeRegistrationAfterPayment()
                              ──▶ Stripe.Session.retrieve(sessionId)
                              ──▶ Subscription créée en DB

  POST /api/webhooks/stripe ◀─────────────────────── Stripe (événements)
  (signature vérifiée)       StripeWebhookController
                              .handleStripeWebhook()
                              ──▶ StripeWebhookService.handle*()

  POST /api/billing/portal ──▶ BillingController ──▶ Stripe.BillingPortal
                                                    ──▶ URL session portail
  ← redirect portail Stripe
```

---

## 3. Flux d'inscription avec paiement

```
1. GET /api/stripe/verify-session?session_id={id}
   └─▶ Stripe.Session.retrieve(id)
   └─▶ AuthService.completeRegistrationAfterPayment(sessionId)
       ├─▶ Crée l'utilisateur en DB (User.save())
       ├─▶ Crée le compte Keycloak
       ├─▶ Crée la Subscription { planType: PRO, status: ACTIVE,
       │       stripeCustomerId, stripeSubscriptionId }
       └─▶ compte activé → redirect app /auth/login (tokens émis par Keycloak au login, ADR-011)
```

**Idempotence** : `stripe_event_id` (UNIQUE) sur `subscription_history` — un événement
traité deux fois ne double pas l'effet.

---

## 4. Webhook Stripe — signature et traitement

### 4.1 Vérification de signature

```java
// StripeWebhookController.java
Event event = Webhook.constructEvent(payload, sigHeader, webhookSecret);
```

Stripe signe chaque payload avec un secret HMAC (`STRIPE_WEBHOOK_SECRET`). Si la signature
est invalide → `400 Bad Request` (rejet immédiat). Si valide → dispatch par type d'événement.

### 4.2 Événements gérés

| Événement Stripe | Traitement |
|---|---|
| `checkout.session.completed` | Finalise inscription + `PlanStatus → ACTIVE` |
| `customer.subscription.updated` | Met à jour `Subscription.planStatus` + `planType` |
| `customer.subscription.deleted` | Passe le workspace en `FREE`, `PlanStatus → CANCELLED` |
| `invoice.payment_succeeded` | Enregistre le paiement dans `subscription_history` |
| `invoice.payment_failed` | Notifie l'OWNER + `PlanStatus → PAST_DUE` |

### 4.3 Stratégie d'erreur

```java
// StripeWebhookController.java — commentaire Javadoc
// Erreur de traitement (souvent transitoire : DB indisponible…) → 500 pour que Stripe
// RÉ-ESSAIE (backoff ~3j). Le traitement est idempotent (alreadyProcessed via
// stripe_event_id unique), donc un retry ne double jamais l'effet.
// Renvoyer 200 ici perdrait l'événement sur un échec transitoire (FIX-005).
return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Webhook processing error");
```

Stripe réessaie automatiquement les webhooks sur les codes 5xx (backoff exponentiel, jusqu'à 3 jours).

---

## 5. Cycle de vie des abonnements (`PlanStatus`)

```
            ┌──────────┐
            │ PENDING  │  (sélection plan, avant paiement)
            └────┬─────┘
                 │ checkout.session.completed
                 ▼
            ┌──────────┐
            │  ACTIVE  │◀────────────────────────────┐
            └────┬─────┘                             │
                 │ invoice.payment_failed             │ invoice.payment_succeeded
                 ▼                                   │  (renouvellement OK)
            ┌──────────┐                             │
            │ PAST_DUE │─────────────────────────────┘
            └────┬─────┘
                 │ customer.subscription.deleted
                 ▼
           ┌───────────┐
           │ CANCELLED │
           └───────────┘
                 │
                 ▼
             (downgrade FREE)
```

**Source** : `PlanStatus` enum · `StripeWebhookService.handleSubscriptionUpdated()` ·
[[Diagramme_Etats_UML]] §4.

---

## 6. Portail de facturation (self-service)

```java
// BillingController.java
@PostMapping("/portal")
public ResponseEntity<ApiResponse<Map<String, String>>> createPortalSession(...) {
    // Stripe.BillingPortal.Session.create()
    // Retourne { url: "https://billing.stripe.com/session/..." }
}
```

L'OWNER peut depuis le portail Stripe :
- Changer de plan (upgrade / downgrade)
- Mettre à jour le moyen de paiement
- Télécharger les factures
- Annuler l'abonnement

---

## 7. Modèle de données Stripe (DB)

### Table `subscriptions` (V8)

| Colonne | Type | Description |
|---|---|---|
| `id` | BIGSERIAL | Clé primaire |
| `user_id` | BIGINT | FK → `users.id` (Long, pas @ManyToOne — ADR-008) |
| `workspace_id` | BIGINT | FK → `workspaces.id` |
| `plan_type` | VARCHAR | `FREE` / `PRO` / `ENTERPRISE` |
| `plan_status` | VARCHAR | `PENDING` / `ACTIVE` / `PAST_DUE` / `CANCELLED` |
| `stripe_customer_id` | VARCHAR | Identifiant client Stripe (`cus_…`) |
| `stripe_subscription_id` | VARCHAR | Identifiant abonnement Stripe (`sub_…`) |
| `current_period_start` | TIMESTAMP | Début de la période courante |
| `current_period_end` | TIMESTAMP | Fin de la période courante |

### Table `subscription_history` (V9)

Trace chaque changement de statut. Colonne `stripe_event_id` UNIQUE — garantit l'idempotence
des webhooks.

---

## 8. Variables d'environnement requises

| Variable | Usage |
|---|---|
| `STRIPE_SECRET_KEY` | API Stripe (sk_live_… / sk_test_…) |
| `STRIPE_WEBHOOK_SECRET` | Vérification signature webhook (whsec_…) |
| `STRIPE_PRO_PRICE_ID` | ID du prix PRO dans le catalogue Stripe (price_…) |
| `STRIPE_ENTERPRISE_PRICE_ID` | ID du prix Enterprise |

**Aucune clé n'est committée** — toutes dans `.env.prod` (non versionné) ou secrets CI/CD.

---

## 9. Checklist test paiement (mode test Stripe)

```
stripe listen --forward-to localhost:8080/api/webhooks/stripe
stripe trigger checkout.session.completed
stripe trigger customer.subscription.updated
stripe trigger invoice.payment_failed
```

Cartes de test : `4242 4242 4242 4242` (succès) · `4000 0000 0000 0341` (paiement refusé).

> 🔗 Voir aussi : [[Business_Model_Pricing]] §3 — [[Auth_Autorisation]] §3 (inscription)
> [[Diagrammes_Sequence_UML]] §5 (séquence Stripe) — [[ADR-001]] (tech stack) —
> [[Spec_API_OpenAPI]] §17
