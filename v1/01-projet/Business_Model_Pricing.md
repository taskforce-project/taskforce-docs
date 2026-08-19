---
id: business-model-pricing
title: Business Model & Pricing — TaskForce
doc_type: business
statut: valide
version: 2.0
date: "12/07/2026"
auteur: Pierre MICHEL
tags: [business, pricing, monetisation, saas, stripe, freemium, per-seat, tam-sam-som, memoire, rncp]
---

# 💰 Business Model & Pricing — TaskForce

> Synthèse du modèle économique. Reflète la grille **4 forfaits par siège** réellement implémentée
> (migration `V68`, cf. `PlanType` / `WorkspaceService` / `StripeService`). Source marché complète →
> analyse **TAM/SAM/SOM** (§3) et [[Etude_business]].

> **v2.0 (12/07/2026)** — refonte : passage de 3 niveaux (FREE/PRO/Enterprise) à **4 niveaux
> per-seat façon Linear** (FREE/BASIC/BUSINESS/ENTERPRISE), ajout du plafond « projets privés façon
> GitHub », intégration de l'analyse de marché chiffrée et de la facturation Stripe **par siège**.

---

## 1. Modèle SaaS freemium — 4 niveaux (par membre / mois)

| Plan | Prix | Cible | Limites clés | Fonctionnalités clés |
|---|---|---|---|---|
| **FREE** | 0 € (permanent) | TPE / équipes en évaluation | 2 workspaces · 250 issues · **projets privés ≤ 5 collab.** | Board/List/Cycles · **Smart Assign (IA)** |
| **BASIC** | **10 €/membre/mois** | Petites équipes qui démarrent | 5 workspaces · issues & collab. privés illimités | + Uploads illimités · rôles admin |
| **BUSINESS** | **16 €/membre/mois** | Équipes qui livrent | Workspaces illimités | + Analytics avancées · **Insights & Assistant IA** · intégrations · invités & projets privés · historique illimité |
| **ENTERPRISE** | Sur devis | Grandes organisations | Illimité | + SSO/SAML/SCIM · audit & conformité RGPD · on-premise · support dédié |

> **Membres illimités sur tous les plans** (tarification par siège, façon Linear). Le seul plafond de
> type « membre » = le **nombre de collaborateurs d'un projet _privé_ en FREE (5, façon GitHub)** ;
> un projet public a des collaborateurs illimités. Anciens comptes **PRO → BUSINESS** (migration `V68`).

> **Implémenté (V1)** : FREE / BASIC / BUSINESS en **self-service** via Stripe Checkout **par siège**
> (quantité = nb de membres) + webhooks. ENTERPRISE = contact commercial (`mailto:sales@`).

### Logique de la grille

- **Per-seat façon Linear** : membres illimités partout → on laisse toute l'équipe s'onboarder
  gratuitement (« aha moment » du Smart Assign dès FREE), puis le mur d'usage/features déclenche
  l'upgrade — et le per-seat facture alors **tous** les sièges déjà présents.
- **Mur « membre » façon GitHub** : les projets _privés_ sont plafonnés à 5 collaborateurs en FREE
  (rendre public **ou** passer payant pour lever la limite) — un frein tangible et confidentiel.
- **IA incluse, pas en add-on** : là où la concurrence facture l'IA en supplément (Asana « Everything AI »
  **+28 $**, ClickUp Brain **+9 $**, Monday en crédits), TaskForce l'inclut au prix du forfait. C'est l'angle.
- **Prix alignés Linear** : 10 € / 16 € par membre ≈ Linear Basic/Business (8 $ / 14 $ annuels).

---

## 2. Unité économique (unit economics) — indicatif

| Métrique | Hypothèse Y1 | Repère marché (sourcé §3) |
|---|---|---|
| **CAC** (acquisition, self-serve PLG) | ~180 € | — |
| **ARPU / siège** | ~13 €/mois (mix BASIC 10 € / BUSINESS 16 €) | catalogue PM PME 85–300 $/siège/an |
| **Conversion freemium → payant** | 6 % cible | médiane ~8 % ; « bon » 3–5 %, PQL/triggers ×3 |
| **Churn mensuel** | 4,0 % Y1 → 2,5 % Y4–5 | SMB SaaS 3–7 %/mois |
| **Durée de vie moyenne** | ~25 mois (1/churn) | — |
| **LTV / siège** | ~325 € → **LTV:CAC > 3×** au niveau **compte** (≈ 8–11 sièges) | cible ≥ 3× |

> ⚠️ 43 % des pertes clients SMB surviennent dans les **90 premiers jours** → la qualité d'onboarding
> est le levier n°1 de rétention (source : benchmarks §3).

---

## 3. Marché (TAM / SAM / SOM) & go-to-market

Synthèse de l'**analyse de marché sourcée** (Grand View, Mordor, Precedence, Capterra 2025, Gartner,
PMI, Eurostat, INSEE). *Les cabinets divergent (périmètres différents) → fourchettes affichées.*

| Niveau | Estimation | Base |
|---|---|---|
| **TAM** | ≈ **8 Md$** (2025) → ~20 Md$ (2030), CAGR ~15,7 % | PM software mondial (fourchette sources 7,6–10,3 Md$) |
| ↳ cœur IA-PM | ≈ **3 Md$** (2024) → ~14 Md$ (2034), **+17 %/an** | sous-marché « IA dans le PM » (le plus dynamique) |
| **SAM** | ≈ **2,6 Md$** | PME 10–249, Europe (PM Europe 6,5 Md$ × ~40 % PME) |
| ↳ beachhead France | ≈ **0,4 Md$** | ~182 k firmes 10–249 (INSEE : 175 k PME + 7,4 k ETI) |
| **SOM** | ≈ **3–5 M€ ARR** à 3 ans | ~2 500 comptes × ~11 sièges × ~140 €/siège/an (≈ 1 % du beachhead FR) |

**Signal de timing** : l'ajout de fonctionnalités IA est le **1ᵉʳ déclencheur d'achat** d'un logiciel PM
pour **55 %** des acheteurs (Capterra 2025), alors que **12 %** seulement des organisations ont une
adoption IA substantielle (PMI) — fenêtre ouverte. Gartner : **80 %** des tâches de PM automatisées d'ici 2030.

| Segment (GTM) | Taille FR | Stratégie d'entrée | Cycle vente |
|---|---|---|---|
| **PME 10–249** (prioritaire) | ~182 000 | Freemium self-service (PLG) + SEO/LinkedIn | 1–3 mois |
| **Moyennes 250–1K** | ~15 000 | POC structurés, sécurité/conformité | 6–12 mois |
| **Grandes +1K** | ~2 500 | RFP, contrats pluriannuels (Enterprise) | 12–24 mois |

---

## 4. Différenciation concurrentielle

| Concurrent | Prix d'entrée / siège | IA | Faiblesse exploitée par TaskForce |
|---|---|---|---|
| Linear | 8–16 $ | **native** | Centré dev/produit ; pas de gestion surcharge/bien-être |
| Jira | ~7,5 $ | add-on (Rovo) | Complexité ; IA en tiers supérieur |
| Monday.com | 9 $ | crédits payants | Pas d'assignation auto explicable |
| Asana | 10,99 $ | **+28 $/user** | Assignation limitée ; IA chère |
| ClickUp | 7 $ | **+9 $/user** | Surcharge cognitive ; IA en add-on |
| Notion | 8–10 $ | +8–10 $/user | PM léger ; IA en add-on |

**Avantage TaskForce** : **IA d'assignation explicable multi-critères incluse** (pas d'add-on),
**projets privés façon GitHub**, RGPD by design, **Brain OS** (mémoire de connaissance native).

---

## 5. Implémentation Stripe (livrée en V1) — facturation par siège

| Élément | Détail | Preuve code |
|---|---|---|
| **Checkout per-seat** | Session `SUBSCRIPTION`, **quantité = nb de membres distincts** du compte | `BillingController.createCheckout` → `POST /api/billing/checkout` |
| **Prix par forfait** | price-ids BASIC / BUSINESS (par siège) ; ENTERPRISE = devis | `StripeService.getPriceIdForPlan` · `application-dev.yml` |
| **Webhooks** | checkout / subscription / invoice → maj plan & historique | `StripeWebhookService` |
| **Idempotence** | `stripe_event_id UNIQUE` (pas de double traitement) | Migration V36 |
| **Portail client** | Self-service changement de plan, gestion paiement | `BillingController.createPortalSession` |
| **État abonnement** | `PlanStatus` : ACTIVE / PAST_DUE / CANCELED… | Enum `PlanStatus`, `User.planStatus` |

> Reste à câbler (documenté `docs/STRIPE_SETUP.md`) : **prix annuels réels** (le toggle « annuel » est
> visuel) et **proration des sièges** quand l'effectif change.

---

## 6. Projection financière (indicative — fil rouge académique)

| Année | ARR visé | Comptes payants (≈ sièges) | Statut fondateur |
|---|---|---|---|
| An 1 | ~0,4 M€ | ~400 (× 8) | 0 € (réinvestissement) |
| An 2 | ~1,6 M€ | ~1 200 (× 10) | 400 €/mois |
| An 3 | ~3,9 M€ | ~2 500 (× 11) | 1 200 €/mois |

Cohérent avec le **SOM ~3–5 M€ ARR à 3 ans** (§3). Une exécution PLG plus agressive pousse le haut
de fourchette vers ~9 M€.

> ⚠️ **Note** : projections à titre **indicatif** (étude de marché pédagogique). Le projet est un fil
> rouge académique — aucun revenu réel à la date de soutenance. SAM/SOM = estimations construites
> (hypothèses explicites), à affiner avec une étude terrain (entretiens PME cible).

> 🔗 Voir aussi : [[PRD_Vision_Produit]] · [[Note_Cadrage]] · [[Etude_business]] ·
> [[Strategie_Marketing]] · `docs/PLANS_MATRIX.md` (matrice permissions/accès) · `docs/STRIPE_SETUP.md`.
