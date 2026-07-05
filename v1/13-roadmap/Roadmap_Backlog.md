---
id: roadmap-backlog
title: Backlog & Roadmap Technique (exhaustif)
doc_type: register
statut: active
version: 1.0
date: "08/06/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [technique, backlog, roadmap, todo, rncp, securite, tests]
related:
  - "../../Brain_OS.md"
  - "../09-audits/Problemes_Connus.md"
  - "../16-memoire-rncp/README.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Backlog & Roadmap Technique

**Version :** 1.0  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Registre](https://img.shields.io/badge/Type-Registre-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]() [![Couverture: RNCP + Pro](https://img.shields.io/badge/Couverture-RNCP%20%2B%20Ultra%20Pro-purple?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS — Hub](../../Brain_OS.md)
- [Problèmes connus](../09-audits/Problemes_Connus.md) · [Dette technique](../09-audits/Dette_Technique.md)
- [Mémoire — matrice des compétences](../16-memoire-rncp/README.md)

**Tags :** `#technique` `#backlog` `#roadmap` `#todo` `#rncp`

<p class="lead">
Liste <strong>exhaustive</strong> de tout ce qui reste à faire pour mener TaskForce au niveau « ultra
pro » : landing, frontend, backend, infrastructure, plus les chantiers transverses (tests, sécurité,
conventions, RGPD, documentation, SEO). Chaque tâche est mappée à une compétence RNCP (le référentiel est
le <strong>socle minimal</strong> ; les items marqués ★ vont au-delà). À piloter comme un tableau Kanban
(plugin Obsidian Kanban recommandé).
</p>

> **Légende** — Priorité : 🔴 P0 (bloquant) · 🟠 P1 · 🟡 P2 · 🟢 P3 (nice-to-have). Effort : S ≤½j ·
> M ½–2j · L 3–5j · XL >1 sem. Statut : ⬜ à faire · 🔄 en cours · ✅ fait. ★ = au-delà du référentiel.

## Table des matières

1. [P0 — Correctifs bloquants](#1-p0--correctifs-bloquants)
2. [Frontend](#2-frontend)
3. [Backend](#3-backend)
4. [Landing page](#4-landing-page)
5. [Infrastructure & DevOps](#5-infrastructure--devops)
6. [Tests & qualité](#6-tests--qualité)
7. [Sécurité](#7-sécurité)
8. [RGPD & légal](#8-rgpd--légal)
9. [Conventions & process](#9-conventions--process)
10. [Documentation](#10-documentation)
11. [Synthèse de couverture RNCP](#11-synthèse-de-couverture-rncp)

---

## 1. P0 — Correctifs bloquants

À traiter en premier : ils débloquent des pans entiers de l'app (cf. [Problèmes connus](../09-audits/Problemes_Connus.md)).

> **▶ MAJ 05/07/2026** — Vérifié sur la branche `test/v1-hardening` (le snapshot 08/06 était sur `feat/dashboard`) :
> **TF-FIX-001 à 005 sont ✅ résolus** dans le code actuel (préfixes `/api` présents partout, groupes de routes front déclarés,
> import `profile-service` correct, refresh/logout désormais **Keycloak natif** — cf. TF-SEC-009, webhooks Stripe câblés).

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-FIX-001 | ✅ **Résolu** — préfixe `/api` présent sur les 5 contrôleurs (Cycle, Team, Page, Discussion, Channel) | 🔴 P0 | M | C24 | PC-001 |
| TF-FIX-002 | ✅ **Résolu** — 4 groupes de routes front déclarés (MESSAGE/INTEGRATION/ATTACHMENT/ROADMAP) | 🔴 P0 | S | C17 | PC-002 |
| TF-FIX-003 | ✅ **Résolu** — `profile-service.ts` importe bien `./client` | 🔴 P0 | S | C16 | PC-003 |
| TF-FIX-004 | ✅ **Résolu (05/07)** — refresh/logout migrés sur Keycloak natif (rotation IdP, logout serveur) | 🟠 P1 | M | C24 | PC-004 |
| TF-FIX-005 | ✅ **Résolu** — 5 handlers webhook Stripe câblés (`StripeWebhookController` → `StripeWebhookService`) | 🟠 P1 | L | C23 | PC-005 |

## 2. Frontend

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-FE-001 | Compléter `team-store` (parité CRUD) | 🟡 P2 | M | C15 | PC-006 |
| TF-FE-002 | Brancher « Create issue » de la command palette | 🟢 P3 | S | C15 | PC-013 |
| TF-FE-003 | Retirer les données mock chat (`messages/data.ts`) une fois l'API câblée | 🟡 P2 | S | C15 | PC-011 |
| TF-FE-004 | Audit accessibilité (WCAG 2.1 AA) : navigation clavier, ARIA, contrastes, `axe` | 🟠 P1 | L | C13/C15 | ★ |
| TF-FE-005 | Compléter l'i18n FR/EN (`constants_fr/en`) sur toutes les vues | 🟡 P2 | M | C15 | — |
| TF-FE-006 | En-têtes de sécurité front + CSP (via Next/Nginx), `npm audit` 0 vuln | 🟠 P1 | M | C16 | DT-019 |
| TF-FE-007 | Budget de performance : Lighthouse ≥ 90, analyse de bundle, lazy-loading, images optimisées | 🟡 P2 | M | C16 | ★ |
| TF-FE-008 | États d'erreur/chargement homogènes (error boundaries, skeletons) | 🟢 P3 | M | C13 | — |
| TF-FE-009 | Validation Zod systématique sur tous les formulaires | 🟡 P2 | M | C16 | — |
| TF-FE-010 | ★ Storybook de la UI library (`components/ui`) | 🟢 P3 | L | C13 | ★ |
| TF-FE-011 | Écoconception front : éco-index, sobriété requêtes/poids | 🟢 P3 | M | C16 | — |

## 3. Backend

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-BE-001 | Vrai streaming SSE de l'assistant (tokens Groq) | 🟡 P2 | M | C22 | PC-009 |
| TF-BE-002 | Cache des AI Insights (`ai_runs`/`insight_snapshots`) + garde quota/timeout Groq | 🟡 P2 | M | C22 | PC-007 |
| TF-BE-003 | Feature flags IA (`enabled`/`smartAssign`/`assistant`/`insights`) | 🟡 P2 | M | C22 | PC-014 |
| TF-BE-004 | Notification email + alerte équipe pour les inquiries Sales | 🟡 P2 | S | C22 | PC-008 |
| TF-BE-005 | Compléter les annotations OpenAPI + publier la doc API (Swagger) | 🟠 P1 | M | C24 | DT — |
| TF-BE-006 | Rate limiting / throttling sur endpoints sensibles (auth, IA) | 🟠 P1 | M | C21/C24 | ★ |
| TF-BE-007 | Journalisation structurée (corrélation, niveaux) + masquage données sensibles | 🟠 P1 | M | C21/C32 | — |
| TF-BE-008 | Audit requêtes JPA : index, détection N+1, pagination généralisée | 🟡 P2 | M | C9/C21 | ★ |
| TF-BE-009 | ★ Couche de cache (Redis) pour sessions/Groq/analytics | 🟢 P3 | L | C21 | ★ |
| TF-BE-010 | Décision `ai-service` Python : supprimer ou documenter en legacy | 🟢 P3 | S | C22 | PC-012 |
| TF-BE-011 | Validation/filtrage exhaustif des entrées (DTO `@Valid`) + chiffrement données sensibles | 🟠 P1 | M | C24 | — |
| TF-BE-012 | Écoconception back : sobriété requêtes, tailles de payload | 🟢 P3 | S | C22 | — |

## 4. Landing page

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-LP-001 | SEO technique : `<title>`/meta, sitemap.xml, robots.txt, Open Graph, données structurées (JSON-LD) | 🟠 P1 | M | C20 | — |
| TF-LP-002 | Atteindre ≥ 70 % des critères SEO (audit Lighthouse SEO) | 🟠 P1 | M | C20 | — |
| TF-LP-003 | Outils de mesure d'audience (analytics respectueux RGPD) | 🟡 P2 | S | C20 | — |
| TF-LP-004 | Densité mots-clés + contenu (pricing, CTA, valeur) | 🟡 P2 | M | C20 | — |
| TF-LP-005 | Accessibilité + performance landing (Lighthouse a11y/perf ≥ 90) | 🟡 P2 | M | C20 | ★ |
| TF-LP-006 | i18n landing si cible bilingue | 🟢 P3 | M | C20 | — |

## 5. Infrastructure & DevOps

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-INFRA-001 | Choix d'hébergement cloud argumenté + **diagramme de déploiement** + estimation coûts/élasticité | 🟠 P1 | L | C29/E21 | — |
| TF-INFRA-002 | Nom de domaine + configuration DNS + certificats TLS (Let's Encrypt) | 🟠 P1 | M | C28/E23 | — |
| TF-INFRA-003 | Environnement de production durci (secrets manager, hôte **bastion**, isolation réseau) | 🟠 P1 | L | C30/E22 | — |
| TF-INFRA-004 | Pipeline CD : qualification → production (au-delà du CI actuel) | 🟠 P1 | L | C31/E24 | — |
| TF-INFRA-005 | Observabilité : dashboards SigNoz + sondes + alertes (état services & sécurité) | 🟡 P2 | M | C32/E26 | — |
| TF-INFRA-006 | Stratégie de sauvegarde/restauration validée (test de restore) | 🟠 P1 | M | C9/C32 | PS/PCA/PRA |
| TF-INFRA-007 | Corriger le chemin du healthcheck actuator (`/actuator/health`) | 🟢 P3 | S | C32 | PC-015 |
| TF-INFRA-008 | ★ Durcissement images Docker (non-root, distroless, SBOM, scan trivy bloquant en CI) | 🟡 P2 | M | C26 | ★ |
| TF-INFRA-009 | Runbooks ops (déploiement, incident, restore) — cf. `_templates/TPL_Runbook.md` | 🟡 P2 | M | C27/C32 | — |
| TF-INFRA-010 | ★ IaC (Terraform/Ansible) pour l'environnement cible | 🟢 P3 | XL | C30 | ★ |
| TF-INFRA-011 | **Corriger `docker-compose.prod.yml`** — des `` `n `` PowerShell **littéraux** (lignes ~65/114) cassent le YAML et attachent le volume d'import realm Keycloak au **mauvais service** (backend au lieu de keycloak). Découvert le 05/07. | 🟠 P1 | S | C30 | — |
| TF-BUILD-001 | **Build backend cassé par dérive d'image** — le tag mouvant `maven:3.9-eclipse-temurin-21` a tiré JDK 21.0.11 → NPE javac `SharedNameTable` avec Lombok au `testCompile`. **Contournement appliqué** (`-XDuseUnsharedTable=true` + fork dans le `pom`). À terme : **épingler** l'image Maven sur un digest sain. Découvert le 05/07. | 🟡 P2 | S | C26 | — |

## 6. Tests & qualité

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-TEST-001 | Couverture **front ≥ 50 %** (Vitest + RTL + MSW) + rapport publié | 🟠 P1 | L | C18 | PC-010 |
| TF-TEST-002 | Couverture **back ≥ 50 %** (JUnit/Mockito) + rapport JaCoCo — ✅ **02/07 : 86,1 % (668 tests), gate JaCoCo ≥ 0,84 bloquant** | ✅ done | L | C25 | PC-010 |
| TF-TEST-003 | Plan de tests documenté (front & back), cohérent avec les specs | 🟠 P1 | M | C18/C25 | — |
| TF-TEST-004 | Tests d'intégration back (**Postgres réel** pgvector + Flyway) — ✅ **02/07 socle `@DataJpaTest`** ; Keycloak/MinIO/Stripe → E2E | ✅ done | L | C25 | ★ |
| TF-TEST-005 | ★ E2E Playwright sur les parcours clés (auth, issue, smart-assign) | 🟡 P2 | L | C18 | DT-022 |
| TF-TEST-006 | ★ Tests de contrat API (front ↔ back) pour prévenir les régressions de routes | 🟡 P2 | M | C17/C24 | PC-001/002 |
| TF-TEST-007 | Tests de non-régression + gate de couverture en CI | 🟡 P2 | M | C19/C26 | — |
| TF-TEST-008 | Tests d'accessibilité (axe) et UX (utilisateurs en situation de handicap) | 🟢 P3 | M | C18 | — |
| TF-TEST-009 | **Tests de charge/performance** (k6/Gatling) sur endpoints critiques — vérifier les seuils PERF-01..05 du STB (actuellement validés en comportement, pas en latence) | 🟡 P2 | M | C25 | STB §1 |

## 7. Sécurité

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-SEC-001 | Revue OWASP Top 10 (injection, auth, accès, SSRF…) + checklist | 🟠 P1 | L | C21/C24 | ★ |
| TF-SEC-002 | Scan dépendances (front `npm audit`, back OWASP Dependency-Check) bloquant en CI | 🟠 P1 | M | C16/C22 | — |
| TF-SEC-003 | SAST en CI (`semgrep`) + remédiation des findings | 🟡 P2 | M | C19/C26 | — |
| TF-SEC-004 | Gestion des secrets (hors repo, vault/CI secrets, rotation) | 🟠 P1 | M | C21 | — |
| TF-SEC-005 | En-têtes HTTP de sécurité (HSTS, CSP, X-Frame-Options…) + SSL valide | 🟠 P1 | M | C16 | DT-019 |
| TF-SEC-006 | Contrôle d'accès : revue des `@PreAuthorize`/checks workspace/projet | 🟠 P1 | M | C21/C24 | — |
| TF-SEC-007 | ★ Modèle de menaces (threat model) + registre des risques — ✅ **05/07 : STRIDE documenté** (`07-securite/Threat_Model_STRIDE.md`, 6 catégories × flux réels + risques résiduels) | 🟢 P3 | M | C21 | ★ |
| TF-SEC-008 | Sécurité paiement : vérification signature webhook Stripe, PCI scope | 🟠 P1 | M | C23 | PC-005 |
| **TF-SEC-009** | ✅ **Résolu (05/07)** — émission des JWT migrée vers **Keycloak OIDC (RS256)** : `JwtService` custom supprimé, décodeur `NimbusJwtDecoder` sur JWK Keycloak + validation issuer, login/refresh/logout via `KeycloakAuthService` (ROPC + refresh natif + `users().logout()`). Auto-login post-inscription retiré (Keycloak exige le mot de passe) → redirection `/auth/login`. Table `refresh_tokens` conservée mais inutilisée. **Vérifié : 658 tests backend verts.** Doc auth à réviser : [[Auth_Autorisation]], [[Journal_Decisions_ADR]] (ADR-011). | 🟠 P1 | L | C21/C24 | PC-019 |
| TF-SEC-010 | **DAST ZAP baseline en CI** (bloquant sur alerte HIGH) — complète TF-SEC-002/003 (SAST/SCA déjà spécifiés en CI). Intègre `security-scan.ps1 -Dast` au pipeline avant release. | 🟡 P2 | M | C19/C21 | Threat_Model_STRIDE §4 |
| TF-SEC-011 | ✅ **Résolu (05/07)** — **rate limiting distribué** : `RateLimitFilter` accepte un `ProxyManager` Bucket4j/Lettuce (Redis) partagé entre instances ; fallback local si `ratelimit.distributed.enabled=false` (dev). Redis ajouté au compose prod + `render.yaml`. | 🟡 P2 | M | C30 | Threat_Model_STRIDE (D3) |

## 8. RGPD & légal

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-RGPD-001 | ✅ **Résolu (05/07)** — bannière `cookie-banner.tsx` présente + requalifiée en **notice d'information** (l'app n'utilise que des cookies strictement nécessaires → consentement non requis par la CNIL ; un faux « Refuser » sur des cookies d'auth serait trompeur). CTA d'acquittement « Got it », mention de l'absence de traceurs. | 🟡 P2 | M | C11/E9 | Politique_Confidentialite_CGU §5 |
| TF-RGPD-002 | ✅ **Politique de confidentialité** — **fait (05/07)** : `PrivacyPolicyPageNew.tsx` + `constants_en.ts` (privacy) | ✅ | — | C11/E9 | Politique_Confidentialite_CGU |
| TF-RGPD-003 | ✅ **Accès/export/suppression RGPD** — **fait** : `GdprService.exportMyData` + `deleteMyAccount` + `GdprController` (`/api/gdpr/*`) | ✅ | — | C11/E9 | Audit_RGPD_Conformite §2 |
| TF-RGPD-004 | Double opt-in sur les traitements collectant des données personnelles | 🟢 P3 | M | C11/E9 | — |
| TF-RGPD-005 | 🟡 **Partiel (05/07)** — sous-traitants **corrigés** dans `constants_en.ts`/`constants_fr.ts` (AWS/GA faux → Stripe + Groq, démontrables). Reste : page **Mentions légales** dédiée (LEN Art. 6). | 🟡 P2 | S | C11 | Politique_Confidentialite_CGU §4 |
| TF-RGPD-006 | ✅ **Registre des traitements + audit RGPD** — **fait (05/07)** : `Registre_Traitements_RGPD.md` (7 traitements Art. 30) + `Audit_RGPD_Conformite.md` (E9) | ✅ | — | C11/E9 | Registre_Traitements_RGPD |
| TF-RGPD-007 | ✅ **Résolu (05/07)** — `GdprService.deleteMyAccount` supprime l'identité Keycloak (appel `KeycloakService.deleteUser` **après commit**, tolérant à l'échec ; invalide aussi les sessions). Vérifié en intégration Postgres. | 🟡 P2 | S | C11 | Audit_RGPD_Conformite §2.2 |
| TF-RGPD-008 | **DPA formel Groq** — formaliser Data Processing Agreement avec Groq Inc. (USA) pour le contexte LLM Smart Assign | 🟡 P2 | S | C11 | Registre_Traitements_RGPD §T4 |
| TF-RGPD-009 | **Procédure notification violations** (Art. 33 RGPD) — délai 72h CNIL non documenté comme procédure opérationnelle | 🟡 P2 | S | C11 | Audit_RGPD_Conformite §7 |

## 9. Conventions & process

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-CONV-001 | Pre-commit hooks (husky + lint-staged) : ESLint/Prettier/format | 🟡 P2 | S | C19 | — |
| TF-CONV-002 | Linters/formatters back (Spotless/Checkstyle) en CI | 🟡 P2 | S | C26 | — |
| TF-CONV-003 | Checklist de code review + template de PR (déjà présent à valider) | 🟢 P3 | S | C5 | — |
| TF-CONV-004 | Conventions de code documentées (front & back) + ADR `ADR-0001` | 🟡 P2 | M | C5/C10 | — |
| TF-CONV-005 | ★ Conventional commits + changelog auto (release-please ou équivalent) | 🟢 P3 | M | C26 | — |

## 10. Documentation

| ID | Tâche | Prio | Effort | RNCP | Réf |
| -- | ----- | :--: | :----: | :--: | --- |
| TF-DOC-001 | Compléter le **mémoire** : rédiger chaque compétence des 4 blocs (preuves + captures) | 🟠 P1 | XL | C1–C32 | [Mémoire](../16-memoire-rncp/README.md) |
| TF-DOC-002 | Harmoniser le front-matter de toutes les notes sur le [standard](../04-engineering/Conventions_Documentation.md) | 🟡 P2 | M | C27 | — |
| TF-DOC-003 | Compléter la **doc utilisateur** (Manuel, Installation, FAQ, Release Notes) | 🟠 P1 | L | — | [Utilisateur](../15-utilisateur/Manuel_Utilisateur.md) |
| TF-DOC-004 | Dossier de conception : diagrammes de **cas d'usage**, **classes**, **MCD** (Excalidraw/PlantUML) | 🟠 P1 | L | C7/C8/E8 | — |
| TF-DOC-005 | Formaliser les **wireframes** (E7) à partir de `assets/maquettes/` | 🟡 P2 | M | C6/E7 | — |
| TF-DOC-006 | Méthodologie de **veille** technologique (E10) | 🟡 P2 | S | C12/E10 | — |
| TF-DOC-007 | Doc API publiée pour tiers + **changelog** structuré (E29) | 🟠 P1 | M | C27/C32 | [Release Notes](../15-utilisateur/Release_Notes.md) |
| TF-DOC-008 | ADRs des décisions clés (stack, multi-tenant, IA Groq, STOMP) | 🟡 P2 | M | C10 | — |
| TF-DOC-009 | Note de préconisations techniques (E3) + planification/budget (E2) | 🟡 P2 | M | C2/C3 | — |
| TF-DOC-010 | Note justifiant la méthode **agile** + trame de compte rendu (E5/E6) | 🟡 P2 | S | C4 | — |
| TF-DOC-011 | **Sweep doc auth HS512→OIDC** — mentions résiduelles de `JwtService`/HS512 dans PSSI, Threat_Model_STRIDE, Diagrammes_Sequence_UML (login), CdCT_v2, Dossier_Conception, Sécurité.md, Modules.md, Table_Reconciliation. `Auth_Autorisation.md` déjà fait (v1.1). Découvert 05/07. | 🟡 P2 | M | C27 | ADR-011 |

## 11. Synthèse de couverture RNCP

<p class="lead">
Le tableau ci-dessous relie chaque compétence à son chantier principal. La <a href="../16-memoire-rncp/README.md">matrice
du mémoire</a> reste la checklist « 100 % » faisant foi.
</p>

| Bloc | Compétences | Chantiers backlog dominants |
| ---- | ----------- | --------------------------- |
| 1 — Conception | C1–C12 | TF-DOC-004/005/006/009/010, TF-RGPD-* (C11) |
| 2 — Front-end | C13–C20 | TF-FE-*, TF-TEST-001, TF-LP-* (C20), TF-SEC-005 (C16) |
| 3 — Back-end | C21–C26 | TF-BE-*, TF-TEST-002, TF-SEC-*, TF-FIX-005 (C23) |
| 4 — Déploiement | C27–C32 | TF-INFRA-*, TF-DOC-007, TF-DOC-001 |

<blockquote class="important">
<strong>Ordre conseillé :</strong> P0 (TF-FIX-001→005) → couverture de tests (TF-TEST-001/002, exigence
≥50 % du référentiel) → sécurité & RGPD (P1) → déploiement/observabilité → finition pro (★). En parallèle,
rédiger le mémoire (TF-DOC-001) au fur et à mesure que chaque preuve est produite.
</blockquote>

---

> **Note Brain OS** — Registre vivant : mettre à jour le statut des tâches à chaque avancement. Relié à
> [Problèmes connus](../09-audits/Problemes_Connus.md) (PC-xxx) et à la [matrice du mémoire](../16-memoire-rncp/README.md).

**Dernière mise à jour :** 05/07/2026 (round de correctifs V1-hardening : TF-SEC-009/011, TF-RGPD-001/005/007, +TF-INFRA-011/TF-BUILD-001)  
**Version :** 1.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
