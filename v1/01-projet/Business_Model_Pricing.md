---
id: business-model-pricing
title: Business Model & Pricing — TaskForce
doc_type: business
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [business, pricing, monetisation, saas, stripe, freemium, memoire, rncp]
---

# 💰 Business Model & Pricing — TaskForce

> Synthèse du modèle économique. Source complète → [[Etude_business]] (v2.0, 27/02/2026)
> et [[Strategie_Marketing]]. Ce document extrait les éléments clés en format Obsidian.

---

## 1. Modèle SaaS freemium — 3 niveaux

| Plan | Prix | Cible | Fonctionnalités clés |
|---|---|---|---|
| **FREE** | 0 € (permanent) | Équipes ≤ 5 membres · PME en évaluation | Workspace, projets, issues, smart-assign de base |
| **PRO** | **13 €/user/mois** (annuel) · 15 € (mensuel) | PME 5–250 membres | Tout FREE + membres illimités, redistribution auto, intégrations, analytics, Brain OS |
| **Enterprise** | 18–25 €/user/mois (sur devis, min. 50 users) | Grandes organisations | Tout PRO + hébergement dédié, SLA, modules sectoriels, SSO |

> **Plans V1 implémentés** : FREE et PRO via Stripe Checkout + webhooks. Enterprise = backlog commercial.

### Logique de la grille

- **Freemium** : exposer le smart-assign (innovation core) dès le plan gratuit → « aha moment » immédiat.
  Benchmark conversion freemium→Pro : 12 % M6, 18 % M12, 22 % M24 (source : OpenView SaaS).
- **PRO à 13 €** : entre ClickUp (7 €) et Monday (12 €)/Asana (10,99 €), justifié par l'IA d'assignation.
- **Modules sectoriels** (backlog post-V1) : 3–9 €/user/mois additionnels (LIMS, Qualité ISO, GED).

---

## 2. Unité économique (unit economics)

| Métrique | Valeur estimée Y1 |
|---|---|
| **CAC** (Coût d'acquisition client) | 180 € |
| **LTV Pro** (Lifetime Value) | 936 € (13 €/mois × 12 mois / churn 4 %/mois) |
| **LTV:CAC** | 5,2× (cible ≥ 3×) |
| **Payback** | ~20 mois Y1 → ~11 mois Y5 |
| **Churn mensuel Pro** | 4,0 % Y1 → 2,5 % Y4–5 (optimisation CS + produit) |
| **ARPU cible PME** | 13 €/user/mois |

---

## 3. Segmentation clients & go-to-market

| Segment | Taille FR | Stratégie d'entrée | Cycle vente |
|---|---|---|---|
| **PME 50–250** (prioritaire) | 120 000 entreprises | Freemium self-service + SEO/LinkedIn Ads | 3–6 mois |
| **Moyennes 250–1K** | 15 000 | POC structurés, certifications sécurité | 9–15 mois |
| **Grandes +1K** | 2 500 | RFP, contrats pluriannuels (150–500 K€ ARR) | 12–24 mois |

Marché mondial PM Software : 9,85 Mds$ (2023) → 17,69 Mds$ (2028), CAGR 10,67 %.

---

## 4. Différenciation concurrentielle

| Concurrent | Prix | Faiblesse exploitée par TaskForce |
|---|---|---|
| Monday.com | 9–19 €/user | Pas d'assignation auto intelligente |
| Jira | 8–15 €/user | Complexité, pas de gestion surcharge/bien-être |
| ClickUp | 0–7 €/user | Surcharge cognitive, multi-tenant fragile |
| Asana | 10,99–24,99 €/user | Assignation limitée (automations préconfig) |

**Avantage TaskForce** : IA d'assignation explicable multi-critères, RGPD by design, Brain OS.

---

## 5. Implémentation Stripe (livrée en V1)

| Élément | Détail | Preuve code |
|---|---|---|
| **Checkout** | Souscription plan PRO à l'inscription | `StripeController.verifySession` |
| **Webhooks** | 5 événements traités (checkout, subscription, invoice) | `StripeWebhookController` |
| **Idempotence** | `stripe_event_id UNIQUE` (pas de double traitement) | Migration V36 |
| **Portail client** | Self-service changement de plan, gestion paiement | `BillingController.createPortalSession` |
| **État abonnement** | `PlanStatus` : ACTIVE / PAST_DUE / CANCELED… | Enum `PlanStatus`, `User.planStatus` |

---

## 6. Projection financière (indicative — source Etude_business.md)

| Année | ARR visé | Utilisateurs Pro | Statut fondateur |
|---|---|---|---|
| 2026 | Amorçage | < 50 | 0 € (réinvestissement) |
| 2027 | Break-even M18 | ~200 | 400 €/mois |
| 2028 | Consolidation | ~800 | 1 200 €/mois |
| 2029 | Scaling | ~2 500 | 2 000 €/mois |

> ⚠️ **Note** : projections financières à titre indicatif (étude de marché pédagogique). Le projet
> est un fil rouge académique — aucun revenu réel à la date de soutenance.

> 🔗 Voir aussi : [[PRD_Vision_Produit]] · [[Note_Cadrage]] · [[Etude_business]] ·
> [[Strategie_Marketing]] · [[CdCF_v2]] §4.7.
