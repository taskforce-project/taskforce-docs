---
id: produit-infra
title: État Produit — Infra
doc_type: register
statut: active
version: 0.1
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [produit, suivi, infra, devops]
related:
  - "./README.md"
---
<!-- Logo établissement : assets/images/logo_metz_numeric_school.svg | Logo projet : assets/images/logo_taskforce.png -->

# État Produit — Infra (`docker-*`, `nginx/`, CI)

**Version :** 0.1 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Suivi Produit](https://img.shields.io/badge/Type-Suivi%20Produit-orange?style=for-the-badge)]() [![Répertoire: infra](https://img.shields.io/badge/R%C3%A9pertoire-infra-blue?style=for-the-badge)]()

## Liens rapides
- [🚧 État Produit — Hub](./README.md) · [Architecture §5](../03-architecture/Architecture.md) · [🧠 Brain OS](../../Brain_OS.md)

**Tags :** `#produit` `#infra` `#devops`

> Légende : ✅ `done` · 🔄 `wip` · ⬜ `todo`. Bloc RNCP dominant : **4 (déploiement/production)**.

## Existant
- [x] Docker Compose dev/prod/tools [id:: INF-DOC-001] [statut:: done] [parite:: ok] [ref:: docker-compose.*.yml]
- [x] **`docker-compose.prod.yml` rendu démarrable (22/07/2026)** [id:: INF-PROD-001] [statut:: done] [parite:: ok] [ref:: docker-compose.prod.yml + .env.prod.example] — Le fichier ne déclarait que **5 services sur 9** (frontend, landing, ai-service et MinIO absents) : la pile ne pouvait pas démarrer. Quatre défauts bloquants corrigés : **(1)** `postgres:16-alpine` → `pgvector/pgvector:pg18`, l'image standard n'embarquant pas l'extension `vector` exigée par les migrations V32/V33/V52/V59 ; **(2)** `db/init` n'était pas monté, donc ni la base `keycloak_prod` ni `CREATE EXTENSION vector` n'étaient jouées → nouveau répertoire `db/init-prod/` ; **(3)** les quatre services manquants ajoutés, avec les variables backend qui allaient avec (MinIO, `AI_SERVICE_URL`, mail, Stripe, `ENCRYPTION_KEY`) ; **(4)** `KC_CACHE: ispn` + `CACHE_STACK: kubernetes` → `local`, la pile Infinispan `kubernetes` sondant un DNS de cluster inexistant sur un hôte Docker seul. Gabarit `.env.prod.example` créé (24 variables, aucun secret réel). ⚠️ Rappel `TF-INFRA-011` : `docker compose config` sort **0 avec des variables vides** — sa réussite ne prouve pas que le déploiement fonctionne.
- [x] **Origines publiques du frontend figées au build (22/07/2026)** [id:: INF-FE-001] [statut:: done] [parite:: ok] [ref:: frontend/Dockerfile] — Next.js **inline** les `NEXT_PUBLIC_*` pendant `next build` : les poser en `environment:` du compose n'a aucun effet sur le bundle envoyé au navigateur. Sans `ARG`, l'image de production aurait été construite avec les défauts `localhost:8080` / `localhost:9000` de `next.config.ts` — donc une application déployée appelant `localhost` depuis le poste des utilisateurs, et une CSP autorisant les mauvaises origines. Ajout de trois `ARG`/`ENV` dans l'étage `builder` + `build.args` côté compose. **Conséquence opérationnelle : changer une URL publique impose de reconstruire l'image frontend, pas seulement de la redémarrer.**
- [x] CI GitHub Actions (tests, release, versioning) → GHCR [id:: INF-CI-001] [statut:: done] [parite:: ok] [ref:: .github/workflows]
- [x] Observabilité SigNoz (profil tools) [id:: INF-OBS-001] [statut:: wip] [parite:: ok]

## Dimensionnement (mesuré le 22/07/2026)

> Base chiffrée pour `INF-HOST-001`. Colonne « dev » = `docker stats` sur la pile de développement au
> repos. Colonne « prod » = recommandation, dérivée du mesuré et du configuré.

| Service | Dev (mesuré) | Prod : vCPU / RAM | Disque | Origine du chiffre |
|---|---|---|---|---|
| backend | 694 Mio | 2 / 1,5 Gio | — | **Configuré** : `-Xmx1024m`, limite 1536M, Hikari 20 |
| keycloak | 975 Mio | 1 / 1,25 Gio | 1 Go | Mesuré (`--optimized` en prod) |
| postgres | 71 Mio (à vide) | 1–2 / 1–2 Gio | ≥ 20 Go | Mesuré à vide → à revoir selon volume |
| frontend | 3,13 Gio | 1 / 0,5 Gio | — | ⚠️ Le dev est un serveur Turbopack ; la prod tourne `node server.js` (`output: standalone`). **Estimé, non mesuré** |
| landing | 90 Mio | 0,25 / 0,25 Gio | — | Mesuré (Astro statique servi par `serve`) |
| ai-service | **45 Mio** | 0,25 / 0,25 Gio | — | Mesuré. Passe-plat `fastapi`/`uvicorn`/`pydantic`, **aucun modèle en process** |
| minio | 105 Mio | 0,5 / 0,5 Gio | selon pièces jointes | Mesuré |
| redis | — | 0,25 / 0,25 Gio | — | **Configuré** : `--maxmemory 128mb`, sans persistance |
| nginx | — | 0,25 / 0,25 Gio | — | Reverse proxy + TLS |

**Total hors LLM : ~5,75 Gio de RAM.** Les pics n'étant pas simultanés, une machine **4 vCPU / 8 Gio / 60 Go** couvre l'ensemble avec de la marge.

### Le LLM décide du reste

Modèles configurés, tailles réelles (`ollama list`) : `qwen3:14b` **9,3 Go**, `qwen3:8b` **5,2 Go**,
`bge-m3` **1,2 Go** — soit **15,7 Go sur disque**, à garder résidents en mémoire pour servir.

| | LLM déporté | LLM co-hébergé |
|---|---|---|
| Machine applicative | 4 vCPU / 8 Gio / 60 Go | 8 vCPU / **24 Gio** / 80 Go |
| GPU | inutile | **fortement recommandé** |

Le besoin de GPU n'est pas une supposition : `OLLAMA_TIMEOUT` vaut **300 s**, le commentaire de
`ai-service/app/config.py` indique « génération locale = lente », et le front porte un
`AI_TIMEOUT_MS` de **200 s**. Ces valeurs décrivent une inférence CPU, intenable en production.
`AI_OLLAMA_BASE_URL` étant une variable d'environnement, le LLM peut vivre sur une autre machine.

**RabbitMQ n'est pas requis en mono-instance** : le broker STOMP en mémoire est le défaut explicite
(`taskforce.realtime.relay.enabled=false`, cf. `WebSocketConfig` / `TF-RT-PROD`). Il ne devient
nécessaire que pour partager les topics entre plusieurs instances backend.

## À faire
- [ ] Hébergement cloud + diagramme de déploiement + coûts [id:: INF-HOST-001] [statut:: todo] [parite:: gap] [prio:: P1] (TF-INFRA-001 · C29) — dimensionnement chiffré ci-dessus
- [ ] Domaine + DNS + certificats TLS [id:: INF-DNS-001] [statut:: todo] [prio:: P1] (TF-INFRA-002 · C28)
- [ ] Prod durcie (secrets manager, bastion, isolation) [id:: INF-HARD-001] [statut:: todo] [prio:: P1] (TF-INFRA-003 · C30)
- [ ] Pipeline CD qualif → prod [id:: INF-CD-001] [statut:: todo] [prio:: P1] (TF-INFRA-004 · C31)
- [ ] Dashboards SigNoz + sondes + alertes [id:: INF-OBS-002] [statut:: todo] [prio:: P2] (TF-INFRA-005 · C32)
- [ ] Sauvegarde/restauration testée [id:: INF-BAK-001] [statut:: todo] [prio:: P1] (TF-INFRA-006)
- [ ] Corriger healthcheck actuator [id:: INF-FIX-001] [statut:: todo] [prio:: P3] (PC-015)
- [ ] Durcissement images Docker (non-root, distroless, SBOM, scan bloquant) [id:: INF-IMG-001] [statut:: todo] [parite:: extra] [prio:: P2] (TF-INFRA-008)

---
**Dernière mise à jour :** 22/07/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
