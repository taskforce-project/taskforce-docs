---
id: plan-deploiement-2vm
title: Plan de déploiement — 2 VM (Cloudflare Zero Trust)
doc_type: operations
statut: plan
version: 0.1
date: "18/08/2026"
auteur: Pierre MICHEL
tags: [deploiement, infra, cloudflare, tunnel, access, observabilite, loki, prometheus, vm, groq, c27, c28, c29, c30]
---

# 🚀 Plan de déploiement — 2 VM (Zero Trust)

> **Plan À EXÉCUTER** (rien n'est encore déployé). Cible : **2 VM** (2 vCPU / **4 Go RAM** / ~20 Go
> disque), **derrière le NAT école** → aucune entrée directe possible. LLM déporté sur **Groq** (zéro
> compute local) → l'AI-service n'a plus besoin d'un Ollama hébergé. **On commence par le backend (VM1).**

## 1. Répartition des services

| VM | Services | RAM estimée |
|---|---|---|
| **VM1 — backend / données** | postgres (pgvector) · keycloak · **backend** (prod) · ai-service (**Groq**) · minio · redis · agent logs (Alloy) · cloudflared | **~3,2 Go — tendu** |
| **VM2 — front / observabilité** | frontend · landing · nginx (reverse proxy) · umami · **Prometheus + Grafana + Loki** · cloudflared | ~1,8 Go — marge |

> Les gros postes (backend 1,5 Go + Keycloak + Postgres) → tous sur VM1. VM2 garde la marge pour toute
> l'observabilité. **Keycloak = risque RAM #1** (JVM gourmande) → capper son heap (`JAVA_OPTS_KC`) au besoin.

## 2. Observabilité + logs — SANS duplication

**Tout le lourd (Grafana + Prometheus + Loki) vit UNIQUEMENT sur VM2 ; VM1 ne porte qu'un agent plume.**
- **Métriques** (*pull*) : Prometheus (VM2) *scrape* `GET backend:8080/actuator/prometheus` (VM1) via le
  réseau privé. Déjà exposé côté backend (micrometer + `management.endpoints…prometheus`).
- **Logs** (*push*) : le backend écrit `/var/log/taskforce-api/application.log` (application-prod.yml). Un
  agent léger **Grafana Alloy** (ou Promtail, ~50–80 Mo) sur VM1 *tail* ce fichier et *pousse* vers
  **Loki** (VM2).
- **Grafana** (VM2) affiche métriques + logs au même endroit. **Zéro stack de monitoring sur VM1**, juste
  l'agent → pas de duplication.
- ⚠️ **Pas SigNoz** (ClickHouse ≈ 4 Go seul) — trop lourd. **PLG** (Prometheus/Loki/Grafana) est le bon choix ici.

## 3. Réseau inter-VM
Connexions privées à assurer : frontend→backend, Prometheus→backend, Alloy→Loki, umami→postgres.
→ **Tailscale** (mesh WireGuard, marche derrière NAT, gratuit) : chaque VM obtient une IP `100.x`, on
s'adresse par nom Tailscale. Les URLs cross-VM du compose pointent sur ces adresses (le nom de service
Docker n'est plus partagé entre 2 hôtes).

## 4. Ingress + auth — Cloudflare Zero Trust (« profil comme safex »)
NAT école = aucune entrée → **Cloudflare Tunnel** (`cloudflared`, connexion **sortante** vers l'edge CF,
zéro port ouvert). Hostnames publics routés :
- `app.<domaine>` → frontend (VM2) · `api.<domaine>` → backend (VM1 via Tailscale) · `auth.<domaine>` → keycloak (VM1).
- **Cloudflare Access** devant → politique d'identité (Google / OTP email) : seuls les emails autorisés
  entrent. C'est le « profil safex ».
- ⚠️ Keycloak : son **issuer** doit être l'URL publique (`auth.<domaine>`) — déjà prévu par
  `KEYCLOAK_PUBLIC_URL` / `KC_HOSTNAME` dans le compose prod.

## 5. Changements compose à faire (AVANT exécution)
1. **Découper** `docker-compose.prod.yml` → `docker-compose.vm1.yml` + `docker-compose.vm2.yml`.
2. **AI-service en Groq** : rebrancher `GROQ_API_KEY` (+ `GROQ_MODEL…`) sur l'ai-service (aujourd'hui il
   attend un Ollama externe — commentaire du 24/07 périmé). Zéro LLM local sur les 4 Go.
3. **Ajouter** Prometheus + Grafana + Loki (VM2) + Alloy (VM1) avec leurs configs.
4. **URLs cross-VM** → adresses Tailscale (frontend SSR→backend, Prometheus→backend, Alloy→Loki, umami→postgres).
5. **cloudflared** (tunnel + hostnames) — a priori sur VM2, routant vers le front local + backend/keycloak via Tailscale.

## 6. Profils / env — déjà OK (rien à réactiver)
- **Java** : `SPRING_PROFILES_ACTIVE: prod` posé dans le compose + défaut `prod` fail-safe du Dockerfile (**PC-024**).
- **Postgres prod** : `pgvector/pgvector:pg18` (**PC-025**).

## 7. Ordre d'exécution
1. **VM1 backend d'abord** : Tailscale → postgres + keycloak + backend + ai-service(Groq) + minio + redis
   → healthchecks verts → `GET /api/actuator/health` OK.
2. **VM2** : front + nginx + observabilité (Prometheus scrape VM1, Loki + Alloy) + cloudflared + Access.
3. **Bout-en-bout** : `app.<domaine>` derrière Access → login → l'app parle à `api.<domaine>`.

---
**Réf.** : [[DevOps]] · [[Pipeline_CICD]] · `docker-compose.prod.yml` · [[Problemes_Connus]] (PC-024/025).
