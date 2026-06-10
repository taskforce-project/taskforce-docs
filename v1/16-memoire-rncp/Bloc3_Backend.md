---
type: memoire-rncp
bloc: 3
statut: en-cours
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, bloc3, backend, api, securite]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Bloc 3 — Développer la partie back-end

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Mémoire RNCP](https://img.shields.io/badge/Type-M%C3%A9moire%20RNCP-purple?style=for-the-badge)]() [![Bloc: 3](https://img.shields.io/badge/Bloc-3%20Back--end-blue?style=for-the-badge)]() [![Statut: En cours](https://img.shields.io/badge/Statut-En%20cours-orange?style=for-the-badge)]()

## Liens rapides

- [🎓 Mémoire — Hub](./README.md)
- [🧠 Brain OS](../../Brain_OS.md)
- [Architecture §4 (backend)](../03-architecture/Architecture.md) · [Contrats API](../05-api/API.md) · [Modules](../03-architecture/Modules.md)

**Tags :** `#memoire` `#bloc3` `#backend` `#api` `#securite`

<p class="lead">
Ce bloc couvre le développement back-end : couche de persistance, code serveur, paiement/monétisation,
API sécurisée, tests et industrialisation. Compétences C21 à C26, livrables E15 à E20.
<strong>Évalué aussi en soutenance (démo back-end).</strong>
</p>

> Stack TaskForce back : Spring Boot 4 · Java 21 · PostgreSQL 18 + pgvector · Keycloak (OAuth2/OIDC) ·
> Stripe · MinIO · RabbitMQ/STOMP · Groq. Détail : [Architecture §4](../03-architecture/Architecture.md).

## Table des matières

1. [Activité — Développement back-end](#activité--développement-back-end) (C21–C24)
2. [Activité — Tests back-end](#activité--tests-back-end) (C25, C26)

---

## Activité — Développement back-end

### C21 — Développer la couche de persistance
**Livrable :** E15.
**Critères d'évaluation :**
- [ ] « Sécurité en profondeur » : filtrage des données entrantes/sortantes, authentification forte, journalisation, monitoring, validation des configurations, contrôle d'accès.
- [ ] Bases de données et systèmes de cache performants et sécurisés.

**Preuve dans TaskForce :** JPA/Hibernate + Flyway (V1–V35), [Architecture §6](../03-architecture/Architecture.md), autorisation par `WorkspaceMember`/`ProjectMember`, `AuditableEntity`. Statut : ✅.

> _À rédiger :_ <!-- schéma persistance, indexation, contrôle d'accès, journalisation -->

### C22 — Langage back-end (qualité, sécurité, écoconception)
**Livrable :** E16 — développer intégralement le back-end + intégrer le front.
**Critères d'évaluation :**
- [ ] Couvre l'ensemble des cas d'utilisation du dossier de conception.
- [ ] Code valide et conforme aux référentiels du/des langage(s).
- [ ] Organisation du code conforme aux usages et bonnes pratiques.
- [ ] Bonnes pratiques d'écoconception intégrées.
- [ ] Composants tiers à jour, sans vulnérabilité connue ; prise en compte des performances.
- [ ] Compatible avec les plateformes/versions actuelles.

**Preuve dans TaskForce :** architecture en couches `shared/core/modules` ([Architecture §4](../03-architecture/Architecture.md)), [Modules](../03-architecture/Modules.md), `pom.xml`.

> _À rédiger :_ <!-- organisation du code, conventions, gestion des deps (Maven), perfs -->

### C23 — Implémenter un système de paiement + monétisation
**Livrable :** E17.
**Critères d'évaluation :**
- [ ] Intégration du système de paiement fonctionnelle.
- [ ] Respect des recommandations de sécurité (paiement).
- [ ] Système de monétisation adapté au contexte et pertinent vs cible marketing.

**Preuve dans TaskForce :** **Stripe** (`StripeController`, `StripeWebhookController`, `StripeService`), plans FREE/PRO/ENTERPRISE, checkout. ⚠️ Webhooks de cycle de vie stubés ([PC-005](../09-audits/Problemes_Connus.md)) — à finaliser. Modèle de monétisation : [Stratégie Vente](../01-projet/Strategie_Vente_LLM.md).

> _À rédiger :_ <!-- flux de paiement Stripe, sécurité (webhook signature), plans tarifaires -->

### C24 — Développer une API sécurisée
**Livrable :** E18.
**Critères d'évaluation :**
- [ ] Authentification et autorisation solides.
- [ ] Toutes les entrées utilisateur validées et filtrées.
- [ ] Toutes les données sensibles chiffrées.
- [ ] API documentée et publiée.

**Preuve dans TaskForce :** API REST (`/api/**`), `SecurityConfig` (JWT/Keycloak), `@Valid` sur DTOs, **OpenAPI/Swagger** (`OpenApiConfig`, `/swagger-ui.html`), [Contrats API](../05-api/API.md). ⚠️ Voir incohérences de routes ([PC-001/002](../09-audits/Problemes_Connus.md)).

> _À rédiger :_ <!-- doc OpenAPI, sécurité JWT, validation, chiffrement (TLS, secrets) -->

## Activité — Tests back-end

### C25 — Tester le back-end
**Livrable :** E19 — plan de tests complet et cohérent.
**Critères d'évaluation :**
- [ ] Plan de test cohérent avec les exigences des spécifications.
- [ ] **Couverture du code source ≥ 50 %.**

**Preuve dans TaskForce :** JUnit 5 + Mockito (`backend/tf-api/src/test`), JaCoCo. ⚠️ **Compléter la couverture à 50 %** ([PC-010](../09-audits/Problemes_Connus.md)).

> _À rédiger :_ <!-- plan de tests, rapport JaCoCo, tests d'intégration -->

### C26 — Industrialiser le back-end
**Livrable :** E20.
**Critères d'évaluation :**
- [ ] Outils de qualité cohérents avec les spécifications.
- [ ] Gestion des dépendances mise en œuvre.
- [ ] Chaîne de build améliorant performances **et sécurité** du back.

**Preuve dans TaskForce :** `.github/workflows/backend-tests.yml`, `release.yml`, `version-management.yml`, Maven, Docker (GHCR). Scanners `trivy`/`semgrep` (`docker-compose.tools.yml`). Statut : ✅.

> _À rédiger :_ <!-- pipeline CI back, build Maven/Docker, scans sécurité -->

---

> **Note Brain OS** — Détails back dans [Architecture §4](../03-architecture/Architecture.md) /
> [Contrats API](../05-api/API.md). Risques (Stripe, tests, routes) suivis dans
> [Problèmes connus](../09-audits/Problemes_Connus.md).

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
