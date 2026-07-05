---
id: strategie-hebergement
title: Stratégie d'hébergement — TaskForce V1
doc_type: infra
statut: decision-pendante
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [hebergement, infra, deploiement, render, vm-ecole, production, memoire, rncp, soutenance]
---

# 🖥️ Stratégie d'hébergement — TaskForce V1

> Document de décision sur l'hébergement de production. Deux options réalistes identifiées.
> **Statut : en attente de décision** — stand-by côté VM école (07/2026).
>
> **Ce document décrit les options et les prépare ; il ne prétend pas qu'un déploiement de
> production est actif.** L'infrastructure de développement est complète et fonctionnelle
> (`docker-compose.yml`, `docker-compose.dev.yml`).
>
> **Règle** : le serveur de l'école est une option pédagogique uniquement — une mise en
> production commerciale irait vers une option cloud dédiée.

---

## 1. Contexte

| Paramètre | Valeur |
|---|---|
| Stack | Spring Boot 4, Next.js 16, PostgreSQL 18, Keycloak, MinIO, RabbitMQ |
| Images Docker | Disponibles sur GHCR (`ghcr.io/{owner}/taskforce/*`) via `release.yml` |
| IaC existante | `docker-compose.prod.yml` (VM auto-hébergée) · `render.yaml` (Render.com) |
| Statut déploiement | Dev local complet · Production : décision d'hébergement pendante |

---

## 2. Option A — VM École (Guacamole)

**Principe** : serveur physique mis à disposition par Metz Numeric School,
accessible via interface Guacamole (client web). Stack déployée en self-hosted avec
`docker-compose.prod.yml`.

### Architecture cible sur la VM

```
         Internet
             │ HTTPS (443)
         ┌───▼───┐
         │ Nginx │  reverse-proxy TLS, headers sécurité
         └───┬───┘
     ┌───────┼───────┐
     ▼       ▼       ▼
  Backend  Frontend  Keycloak
  (:8080) (:3000)   (:8180)
     └───────┴──────┐
                    ▼
               PostgreSQL
               (:5432, interne)
               MinIO (:9000)
               RabbitMQ (:5672)
```

### docker-compose.prod.yml — services définis

| Service | Image / Build | Port interne | Notes |
|---|---|---|---|
| `postgres` | `postgres:16-alpine` | 5432 | Volume `postgres_prod_data`, pas exposé |
| `keycloak` | `quay.io/keycloak/keycloak:23.0` | 8080 | `--import-realm --optimized`, `KC_PROXY: edge` |
| `backend` | Build `./backend/tf-api/Dockerfile` | 8080 | `JAVA_OPTS: -Xmx1024m`, JVM G1GC, healthcheck actuator |
| `nginx` | `nginx:alpine` | 80, 443 | Reverse proxy TLS + `nginx.conf` + certificats |

**Variables d'env** : toutes via `--env-file backend/tf-api/.env.prod` (jamais dans le compose).

### Prérequis techniques VM

- Docker + Docker Compose installés
- Ports 80/443 ouverts (Nginx)
- DNS pointé vers l'IP de la VM (domaine à provisionner)
- Certificats TLS (Let's Encrypt via Certbot, ou fournis par l'école)
- Accès SSH ou Guacamole pour déploiement initial et maintenance

### Commande de déploiement

```bash
docker compose -f docker-compose.prod.yml --env-file backend/tf-api/.env.prod up -d
```

### Avantages / Inconvénients

| + Avantages | - Inconvénients |
|---|---|
| Coût nul (fourni par l'école) | Contexte pédagogique uniquement |
| Contrôle total de l'infra | Disponibilité dépendante de l'école |
| Proximité du stack complet | Pas de scalabilité, pas de SLA |
| Adapté à la soutenance | Non viable en production commerciale |

### Statut

⏳ **Stand-by** — VM en attente de provisionnement. Document prêt, `docker-compose.prod.yml`
opérationnel. À activer quand l'accès Guacamole sera disponible.

---

## 3. Option B — Render.com

**Principe** : hébergement cloud managé déclaré via `render.yaml`. Services Docker déployés
directement depuis les images GHCR (ou rebuild Render).

### render.yaml — services déclarés

| Service | Type | Plan | Région | Notes |
|---|---|---|---|---|
| `taskforce-backend` | `web` (Docker) | `starter` | Frankfurt | healthcheck `/api/actuator/health`, env depuis DB Render |
| `taskforce-frontend` | `web` (Docker) | `starter` | Frankfurt | Next.js, `NEXT_PUBLIC_API_URL` pointant vers backend |
| `taskforce-landing` | `web` (static) | `starter` | Frankfurt | Build Astro, headers sécurité déclarés |
| `taskforce-keycloak` | `web` (Docker) | `standard` | Frankfurt | `KC_PROXY: edge`, RAM plus élevée requise |
| `taskforce-postgres` | `database` | `starter` | Frankfurt | PostgreSQL managé, IP whitelist interne uniquement |

**Avantage clé** : Render injecte les variables de connexion DB (`DB_HOST`, `DB_PORT`…) automatiquement via `fromDatabase`.

### Flux de déploiement Render

```
git push → main ──▶ GitHub Actions release.yml ──▶ images GHCR
                ──▶ Render webhook (ou pull auto) ──▶ redéploiement
```

> ⚠️ Le couplage CI→Render (webhook ou image pull) n'est pas encore configuré.
> Actuellement, le `render.yaml` prépare la configuration mais le déploiement
> continu n'est pas activé.

### Estimation coûts Render (plans `starter`)

| Service | Plan | Coût/mois |
|---|---|---|
| Backend | starter | ~7 $ |
| Frontend | starter | ~7 $ |
| Landing | starter (static) | Gratuit |
| Keycloak | standard (RAM) | ~25 $ |
| PostgreSQL | starter | ~7 $ |
| **Total estimé** | | **~46 $/mois** |

> Ce chiffre est indicatif et dépend de la consommation réelle.
> Pour une production sérieuse, Keycloak peut être hébergé séparément
> ou remplacé par un service OIDC managé.

### Avantages / Inconvénients

| + Avantages | - Inconvénients |
|---|---|
| Déploiement rapide, CI/CD natif | Coût mensuel (~46 $/mois minimum) |
| Scalabilité managée | Keycloak = plan `standard` (RAM) |
| SLA Render (99 % uptime) | Moins de contrôle sur l'infra |
| Adapté à la production commerciale | Pas de GPUs / workloads spéciaux |
| TLS automatique | —  |

### Statut

✅ **Configuration prête** — `render.yaml` complet, images disponibles sur GHCR.
Activation nécessite : connexion repo GitHub → Render, définition des variables
secrètes (`KEYCLOAK_ADMIN_PASSWORD`, `STRIPE_*`, etc.) dans le dashboard Render.

---

## 4. Comparaison et recommandation

| Critère | VM École (A) | Render.com (B) |
|---|:---:|:---:|
| Coût | Gratuit | ~46 $/mois |
| Disponibilité | Variable (école) | 99 % SLA |
| Scalabilité | Non | Oui |
| TLS / DNS | Manuel | Automatique |
| Contrôle infra | Total | Partiel |
| Contexte pédagogique | ✅ Idéal | Possible |
| Contexte production commerciale | ❌ | ✅ Idéal |
| Délai d'activation | Attente VM | Immédiat |

**Recommandation** :
- **Soutenance / démonstration** → Option A (VM école, coût nul, approprié)
- **Production commerciale / Go-to-market** → Option B (Render ou équivalent cloud, SLA garanti)
- Une migration A→B est fluide : les images GHCR et le `render.yaml` sont prêts.

---

## 5. Infrastructure de développement (état actuel)

L'infrastructure **de développement** est complète et fonctionnelle :

```bash
# Stack de développement complète
docker compose -f docker-compose.dev.yml up -d

# Services : postgres, backend, frontend, keycloak, minio, rabbitmq, otel-collector, signoz
```

C'est cette stack qui est levée dans le workflow `e2e-tests.yml` (CI) et dans la procédure de
développement local. Elle inclut SigNoz, MinIO, RabbitMQ — l'environnement complet.

---

## 6. Variables d'environnement requises (production)

| Variable | Service | Secret | Source |
|---|---|---|---|
| `DB_HOST/PORT/NAME/USER/PASSWORD` | Backend | Oui | Render DB ou `.env.prod` |
| `JWT_SECRET` | Backend | Oui | Généré (≥32 chars) |
| `KEYCLOAK_ADMIN_PASSWORD` | Keycloak | Oui | Défini manuellement |
| `KEYCLOAK_CLIENT_SECRET` | Backend | Oui | Défini dans Keycloak |
| `STRIPE_SECRET_KEY` | Backend | Oui | Dashboard Stripe |
| `STRIPE_WEBHOOK_SECRET` | Backend | Oui | Dashboard Stripe |
| `GROQ_API_KEY` | Backend | Oui | Console Groq |
| `ENCRYPTION_SECRET` | Backend | Oui | Généré (clé AES-256) |
| `ALLOWED_ORIGINS` | Backend | Non | URL frontend de prod |

> Toutes ces variables sont injectées à l'exécution — **jamais** dans le code ni dans les images.
> Voir [[PSSI]] §3.3 (gestion des secrets).

---

> 🔗 [[Pipeline_CICD]] — [[PSSI]] §3.3 (secrets) — [[Architecture_C4]] (conteneurs) —
> [[Roadmap_Backlog]] (TF-INFRA-001/003/004)
