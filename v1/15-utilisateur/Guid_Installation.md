---
type: documentation-utilisateur
statut: draft
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [utilisateur, installation, déploiement, docker]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Guide d'Installation — TaskForce

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Utilisateur](https://img.shields.io/badge/Type-Documentation%20Utilisateur-green?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS](../../Brain_OS.md)
- [Manuel Utilisateur](./Manuel_Utilisateur.md)
- [Quickstart développeur](../06-infra/quickstart/README.md)
- [Architecture & infra](../03-architecture/Architecture.md)

**Tags :** `#utilisateur` `#installation` `#docker` `#déploiement`

<p class="lead">
Ce guide décrit l'installation de TaskForce, de l'environnement de développement local jusqu'au
déploiement de production. L'application est entièrement conteneurisée (Docker Compose).
</p>

## Table des matières

1. [Prérequis](#1-prérequis)
2. [Installation en développement](#2-installation-en-développement)
3. [Variables d'environnement](#3-variables-denvironnement)
4. [Déploiement de production](#4-déploiement-de-production)
5. [Vérification & dépannage](#5-vérification--dépannage)

---

## 1. Prérequis

| Outil | Version | Usage |
| ----- | ------- | ----- |
| Docker + Docker Compose | V2 | Orchestration de tous les services |
| Git | ≥ 2.40 | Récupération du code |
| Node.js | 20 LTS | (optionnel) front hors Docker |
| Java | 21 LTS | (optionnel) back hors Docker |

> _À rédiger :_ <!-- ressources matérielles minimales, ports requis -->

## 2. Installation en développement

```bash
git clone https://github.com/taskforce-project/taskforce-fullstack.git
cd taskforce-fullstack
cp .env.example .env.dev   # puis renseigner les variables
.\docker.ps1 dev-up        # ou: docker compose -f docker-compose.dev.yml up
```

Services exposés (dev) :

| Service | URL |
| ------- | --- |
| Frontend | http://localhost:3000 |
| Backend API | http://localhost:8080/api |
| Keycloak | http://localhost:8180 |
| pgAdmin | http://localhost:5050 |
| MinIO console | http://localhost:9001 |
| RabbitMQ | http://localhost:15672 |

> _À rédiger :_ <!-- comptes de test (Keycloak), seed data, premier login -->

## 3. Variables d'environnement

Renseigner `.env.dev` (dev) / `.env.prod` (prod) à partir de `.env.example`. **Ne jamais committer de
secrets réels.** Catégories principales :

| Catégorie | Variables (exemples) | Rôle |
| --------- | -------------------- | ---- |
| Base de données | `POSTGRES_*`, `DB_HOST/PORT/NAME/USER/PASSWORD` | PostgreSQL 18 + pgvector |
| Backend | `SERVER_PORT`, `SPRING_PROFILES_ACTIVE`, `CORS_ALLOWED_ORIGINS`, `JWT_SECRET` | API Spring Boot |
| Keycloak | `KEYCLOAK_URL/REALM/CLIENT_ID/CLIENT_SECRET`, `KEYCLOAK_ADMIN_USERNAME/PASSWORD` | Identité OAuth2/OIDC |
| Frontend | `NEXT_PUBLIC_API_URL`, `NEXT_PUBLIC_API_URL_SSR`, `FRONTEND_PORT` | Client Next.js |
| Stripe | `STRIPE_SECRET_KEY`, `STRIPE_PUBLIC_KEY`, `STRIPE_WEBHOOK_SECRET`, `STRIPE_PRICE_ID_*` | Paiement / abonnements |
| Groq (IA) | `GROQ_API_KEY`, `GROQ_SMART_ASSIGN_MODEL`, `GROQ_ASSISTANT_MODEL` | LLM (smart-assign, assistant) |
| MinIO | `MINIO_ENDPOINT`, `MINIO_ROOT_USER/PASSWORD`, `MINIO_BUCKET` | Stockage objets (avatars, PJ) |
| RabbitMQ | `RABBITMQ_HOST/PORT`, `RABBITMQ_USER/PASSWORD`, `RABBITMQ_STOMP_PORT` | Temps réel (STOMP) |
| Email | `MAIL_HOST/PORT`, `MAIL_USERNAME/PASSWORD`, `MAIL_FROM` | OTP & notifications (Mailtrap en dev) |
| Observabilité | `OTEL_*` | Traces OpenTelemetry → SigNoz (optionnel) |

> ⚠️ Dans Docker, les services se joignent par **nom de service** (`http://backend:8080`), pas `localhost`.

## 4. Déploiement de production

L'environnement de production utilise `docker-compose.prod.yml` (PostgreSQL, Keycloak, backend, frontend,
**Nginx** reverse proxy + SSL). Images publiées sur **GHCR** ([GHCR_USAGE](../06-infra/docker/GHCR_USAGE.md)).

> _À rédiger :_ <!-- nom de domaine, certificats TLS, secrets prod, sauvegarde (cf. PS/PCA/PRA), supervision SigNoz -->

## 5. Vérification & dépannage

> _À rédiger :_ <!-- healthchecks (/actuator/health), logs docker, problèmes fréquents -->

---

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
