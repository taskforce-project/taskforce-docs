---
type: memoire-rncp
bloc: 4
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc4, deploiement, devops, supervision]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 4 — Déployer et maintenir en production

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 4](https://img.shields.io/badge/Bloc-4%20D%C3%A9ploiement-blue?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture §5 (infra)](../03-architecture/Architecture.md) · [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) · [GHCR](../06-infra/docker/GHCR_USAGE.md)

**Tags :** `#memoire` `#bloc4` `#deploiement` `#devops` `#supervision`

<p class="lead">
Ce bloc couvre la documentation technique, le déploiement et le maintien en production : choix
d'hébergement, administration des services, déploiement automatisé (DevOps) et supervision. Compétences
C27 à C32, livrables E21 à E29. <strong>Également évalué via une mise en situation de maintenance</strong>
(bugs, failles, composants obsolètes).
</p>

> Infra TaskForce : Docker Compose (dev/prod/tools) · Nginx (prod) · Keycloak · MinIO · RabbitMQ ·
> PostgreSQL · SigNoz (observabilité) · GitHub Actions → GHCR. Détail : [Architecture §5](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Documentation & solutions de production](#activité--documentation--solutions-de-production) (C27, C28, C29)
2. [Activité — Administration & déploiement](#activité--administration--déploiement) (C30, C31)
3. [Activité — Supervision & maintenance](#activité--supervision--maintenance) (C32)

---

## Activité — Documentation & solutions de production

### C27 — Produire la documentation technique + base de connaissances
**Livrable :** E29 — génération de documentation + mise à jour du changelog.
**Critères d'évaluation :**
- [ ] Génération automatique de documentation à partir du code source.
- [ ] Documentation de l'API rédigée pour faciliter sa consommation par des tiers.
- [ ] Mises à jour portées dans le journal des évolutions (changelog).
- [ ] Liste des modifications structurée (ordre décroissant de commit, regroupement par version).

**Preuve dans TaskForce :** **Ce Brain OS** (`taskforce-docs/`), OpenAPI/Swagger auto-généré, versioning sémantique automatisé (`version-management.yml`, `sync-readme-badges.yml`), [Release Notes](../15-utilisateur/Release_Notes.md). Statut : 🟡 (formaliser le changelog).

> _À rédiger :_ <!-- doc API publiée, base de connaissances, changelog structuré -->

### C28 — Administration (domaine, DNS, certificats, sécurité)
**Livrable :** E23 — réservation nom de domaine, configuration DNS, installation/vérification des certificats.
**Critères d'évaluation :**
- [ ] Nom de domaine et déclarations administratives effectuées.
- [ ] Serveurs de noms configurés et fonctionnels (bonnes pratiques de sécurité).
- [ ] Certificats de sécurité installés, configurés pour les différents services.

**Preuve dans TaskForce :** `nginx/` (reverse proxy, SSL prod), `docker-compose.prod.yml`. Statut : ⬜ à documenter (domaine, DNS, Let's Encrypt/certificats).

> _À rédiger :_ <!-- nom de domaine, zone DNS, émission/renouvellement certificats TLS -->

### C29 — Sélectionner une plateforme d'hébergement
**Livrable :** E21 — choix d'une solution cloud argumentée + diagramme de déploiement.
**Critères d'évaluation :**
- [ ] Architecture technique d'hébergement adaptée à l'application.
- [ ] Principe d'élasticité pris en compte.
- [ ] Dimensionnement et coûts cohérents avec les besoins.
- [ ] Diagramme de déploiement formalisé ; choix du système de déploiement adapté ; déploiement sur l'environnement de qualification effectué.

**Preuve dans TaskForce :** conteneurisation Docker (portable cloud), images GHCR. Statut : ⬜ produire le comparatif (VPS/cloud/PaaS) + diagramme de déploiement + estimation coûts.

> _À rédiger :_ <!-- comparatif hébergeurs, diagramme de déploiement, élasticité, coûts -->

## Activité — Administration & déploiement

### C30 — Administrer des services d'hébergement (cloud / conteneurisé)
**Livrable :** E22 — mise en œuvre sécurisée de l'environnement de production + administration.
**Critères d'évaluation :**
- [ ] Services d'hébergement configurés et fonctionnels (gestionnaire de conteneurs).
- [ ] Environnement conteneurisé fonctionnel.
- [ ] Bonnes pratiques de sécurité (architecture, configuration, **hôte bastion**).

**Preuve dans TaskForce :** `docker-compose.prod.yml` (postgres, keycloak, backend, frontend, nginx), réseaux Docker isolés. Statut : 🟡 (formaliser bastion + durcissement prod).

> _À rédiger :_ <!-- topologie prod, durcissement, bastion, secrets -->

### C31 — Mettre en œuvre un déploiement automatisé (DevOps)
**Livrable :** E24 — système de déploiement automatisé.
**Critères d'évaluation :**
- [ ] Bonnes pratiques DevOps respectées (livraison en continu).
- [ ] Système de déploiement fonctionnel sur l'environnement de qualification, repris en production.
- [ ] Opérationnel et conforme aux recommandations DevOps.

**Preuve dans TaskForce :** `.github/workflows/` (`backend-tests`, `frontend-tests`, `landing-tests`, `release`, `version-management`), images **GHCR** ([GHCR_USAGE](../06-infra/docker/GHCR_USAGE.md)), [GitHub Actions](../04-engineering/git-workflow/github-actions.md). Statut : 🟡 (CI complète ; CD vers prod à formaliser).

> _À rédiger :_ <!-- pipeline CI/CD complet, stratégie de déploiement (qualif → prod) -->

## Activité — Supervision & maintenance

### C32 — Superviser (sondes, alertes, journalisation, détection)
**Livrable :** E25 journalisation/audit · E26 supervision + alertes · E27 détection bugs + correctifs · E28 détection failles + correctifs.
**Critères d'évaluation :**
- [ ] Journalisation des services implémentée ; outils d'audit fonctionnels (analyse efficace des erreurs).
- [ ] Outils de sauvegarde fonctionnels ; stratégie de tolérance de panne adaptée.
- [ ] Outils de supervision fonctionnels ; sondes et alertes efficaces.
- [ ] Bugs identifiés, mesures correctives efficaces.
- [ ] Failles de sécurité identifiées, mesures correctives efficaces.

**Preuve dans TaskForce :** **SigNoz** (OpenTelemetry, `docker-compose.tools.yml` profil observability), Spring Actuator (`/actuator/health,metrics,prometheus`), [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) (sauvegarde/restauration), scanners `trivy`/`semgrep`. Cf. aussi [Problèmes connus](../09-audits/Problemes_Connus.md) (détection de bugs/dette = preuve de la démarche). Statut : 🟡.

> _À rédiger :_ <!-- dashboards SigNoz, sondes/alertes, stratégie backup, exemples de bugs/failles détectés et corrigés -->

---

> **Note Brain OS** — La démarche de **détection de bugs/failles** (C27/C32) est déjà matérialisée par
> [Dette technique](../09-audits/Dette_Technique.md) et [Problèmes connus](../09-audits/Problemes_Connus.md) :
> les réutiliser comme preuves. Infra : [Architecture §5](../03-architecture/Architecture.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
