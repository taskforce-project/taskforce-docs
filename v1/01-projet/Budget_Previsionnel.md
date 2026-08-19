---
id: budget-previsionnel
title: Budget prévisionnel & réel — TaskForce V1
doc_type: budget
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [budget, cout, charge, tjm, previsionnel, reel, memoire, rncp]
---

# 💶 Budget prévisionnel & réel — TaskForce V1

> Estimation de la valeur économique du projet et des coûts d'infrastructure.
> **Note** : projet académique sans financement externe. Les coûts réels sont les coûts
> d'infrastructure + services tiers (tiers gratuits utilisés en développement).

---

## 1. Estimation de la charge (valeur économique)

| Phase | Durée estimée | Profil | TJM référence | Coût équivalent |
|---|---|---|---|---|
| Cadrage & Conception | 7 semaines × 4 h/j ≈ 8 j | Architecte / Chef de projet | 600 €/j | ~4 800 € |
| Développement M1–M3 | 12 semaines × 6 h/j ≈ 36 j | Développeur Full Stack | 550 €/j | ~19 800 € |
| Tests & Validation | 4 semaines × 5 h/j ≈ 12 j | Dev/QA | 500 €/j | ~6 000 € |
| Déploiement & DevOps | 4 semaines × 3 h/j ≈ 7 j | DevOps | 550 €/j | ~3 850 € |
| Documentation | 2 semaines × 7 h/j ≈ 8 j | Tech Writer / Dev | 450 €/j | ~3 600 € |
| **TOTAL charge** | **~71 jours-homme** | | | **~38 050 €** |

> TJM moyen senior Full Stack France 2025 : 500–650 €/j. Valeur indicative à des fins
> pédagogiques (évaluation de la portée du projet).

---

## 2. Coûts d'infrastructure (réels — environnement dev/test)

| Service | Plan utilisé | Coût mensuel | Coût total (9 mois) |
|---|---|---|---|
| **PostgreSQL** | Docker local (gratuit) | 0 € | 0 € |
| **Keycloak** | Docker local (gratuit) | 0 € | 0 € |
| **RabbitMQ** | Docker local (gratuit) | 0 € | 0 € |
| **MinIO** | Docker local (gratuit) | 0 € | 0 € |
| **SigNoz** | Self-hosted Docker (gratuit) | 0 € | 0 € |
| **Groq API** | Tier gratuit (rate-limited) | 0 € | 0 € |
| **Mailtrap** | Tier gratuit (dev) | 0 € | 0 € |
| **Stripe** | Mode test (gratuit) | 0 € | 0 € |
| **GitHub** | Plan Free (public/étudiant) | 0 € | 0 € |
| **VM école (Guacamole)** | Fournies par Metz Numeric School | 0 € | 0 € |
| **TOTAL infra réel (dev)** | | **0 €** | **0 €** |

---

## 3. Coûts d'infrastructure (projection prod — post-soutenance)

| Service | Plan prod estimé | Coût mensuel estimé |
|---|---|---|
| VPS / hébergement cloud | 2–4 vCPU, 8 Go RAM | ~30–60 €/mois |
| Nom de domaine | .io ou .fr | ~15 €/an |
| Certificat TLS | Let's Encrypt (gratuit) | 0 € |
| Stripe | 2,9 % + 0,30 € / transaction | Variable (% du CA) |
| Groq API prod | Pay-per-token (faible usage initial) | ~5–20 €/mois |
| **Estimation prod Y1** | | **~500–900 €/an** |

---

## 4. Synthèse

| Catégorie | Valeur |
|---|---|
| **Valeur économique du travail** | ~38 000 € (équivalent prestation) |
| **Coût infra réel (dev)** | 0 € (tiers gratuits + Docker local) |
| **Coût infra production estimé** | ~500–900 €/an |
| **Budget académique** | 0 € (projet solo pédagogique) |

> ⚠️ La valeur économique est une estimation pédagogique montrant l'ampleur du travail réalisé,
> pas une facturation réelle. Source pricing → [[Business_Model_Pricing]].

> 🔗 Voir aussi : [[Plan_Projet]] · [[Gantt_Planning]] · [[Business_Model_Pricing]] ·
> [[Note_Cadrage]] §6 (contraintes budget).
