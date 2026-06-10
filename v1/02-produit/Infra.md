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
- [x] CI GitHub Actions (tests, release, versioning) → GHCR [id:: INF-CI-001] [statut:: done] [parite:: ok] [ref:: .github/workflows]
- [x] Observabilité SigNoz (profil tools) [id:: INF-OBS-001] [statut:: wip] [parite:: ok]

## À faire
- [ ] Hébergement cloud + diagramme de déploiement + coûts [id:: INF-HOST-001] [statut:: todo] [parite:: gap] [prio:: P1] (TF-INFRA-001 · C29)
- [ ] Domaine + DNS + certificats TLS [id:: INF-DNS-001] [statut:: todo] [prio:: P1] (TF-INFRA-002 · C28)
- [ ] Prod durcie (secrets manager, bastion, isolation) [id:: INF-HARD-001] [statut:: todo] [prio:: P1] (TF-INFRA-003 · C30)
- [ ] Pipeline CD qualif → prod [id:: INF-CD-001] [statut:: todo] [prio:: P1] (TF-INFRA-004 · C31)
- [ ] Dashboards SigNoz + sondes + alertes [id:: INF-OBS-002] [statut:: todo] [prio:: P2] (TF-INFRA-005 · C32)
- [ ] Sauvegarde/restauration testée [id:: INF-BAK-001] [statut:: todo] [prio:: P1] (TF-INFRA-006)
- [ ] Corriger healthcheck actuator [id:: INF-FIX-001] [statut:: todo] [prio:: P3] (PC-015)
- [ ] Durcissement images Docker (non-root, distroless, SBOM, scan bloquant) [id:: INF-IMG-001] [statut:: todo] [parite:: extra] [prio:: P2] (TF-INFRA-008)

---
**Dernière mise à jour :** 09/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
