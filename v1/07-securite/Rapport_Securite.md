---
id: rapport-securite
title: Rapport de sécurité consolidé — TaskForce V1
doc_type: securite
statut: valide
version: 1.0
date: "16/08/2026"
auteur: Pierre MICHEL
tags: [securite, rapport, pssi, stride, owasp, audit, memoire, rncp, soutenance]
---

# 🛡️ Rapport de sécurité consolidé — TaskForce V1

> Document de **synthèse unique** de la posture de sécurité de TaskForce : contrôles réellement
> implémentés (avec preuves code + tests), modèle de menaces, risques résiduels, et outillage de
> scan. Il consolide des documents détaillés existants ([[PSSI]], [[Threat_Model_STRIDE]],
> [[Plan_Securisation_SSDLC]], [[Auth_Autorisation]], [[Chiffrement_Au_Repos]]) pour offrir une vue
> d'ensemble datée — le « rapport de sécurité » attendu au dossier.
>
> **Périmètre** : backend Spring Boot (`backend/tf-api`), frontend Next.js, landing Astro, IA (ai-service),
> infra Docker/CI. **Cadre** : OWASP Top 10, RGPD Art. 32, PSSI interne.

---

## 1. Synthèse (executive summary)

La sécurité **applicative** de TaskForce est **solide et testée** : authentification déléguée à un IdP
standard (Keycloak/OIDC, **RS256**), autorisation au niveau service (RBAC + garde anti-IDOR), **chiffrement
au repos** des PII sensibles, **en-têtes de sécurité** stricts, **limitation de débit**, validation
d'entrée serveur systématique, et durcissement des dépendances. Les **failles inter-tenant (IDOR)**
identifiées ont été corrigées et couvertes par des tests.

**Durcissement prod + portes CI traités (17/08/2026)** : les 3 P0 de configuration de prod (profil `dev` en
prod, CORS codé en dur, seeds à mots de passe en clair) sont **corrigés** (PC-024/026/027, §6) et les CVE HIGH
corrigeables montées ; les portes CI qualité/sécurité rendues **bloquantes** (gate JaCoCo via `mvn verify`,
scans Trivy/Semgrep en CI). **Tous les P0 de config + déploiement prod (profil, CORS, seeds, pgvector) sont
corrigés** ; il ne reste que des points documentaires (STRIDE/PSSI à actualiser) et l'hygiène de secrets
(rotation `.env.dev`, côté exploitant) — sans effet sur la démo locale.

---

## 2. Contrôles par domaine (preuves)

### 2.1 Authentification & sessions
- **OIDC Keycloak, tokens RS256** validés par JWKS + **contrôle de l'`issuer`** ; sessions **STATELESS**.
  L'ancien HS512 auto-émis a été supprimé (dette PC-019 / TF-SEC-009 close).
  → `shared/security/SecurityConfig.java`, [[Auth_Autorisation]].
- **Anti-bot** à l'inscription : défi signé maison + **Cloudflare Turnstile** (jugement du visiteur).
  → `shared/security/TurnstileService`, `HumanChallengeService` (tests `TurnstileServiceTest` 9,
  `HumanChallengeServiceTest` 10). *(Contrôle réel — à intégrer à la [[PSSI]] / au [[Threat_Model_STRIDE]].)*

### 2.2 Autorisation (RBAC + multi-tenant)
- Vérifications **au niveau service** : `AuthorizationService` (`requireMember/requireRole/requireManager`)
  + `ProjectVisibilityGuard` (`assertCanView/assertCanWrite`) + `WorkspaceAccessInterceptor`.
- Rôles : `WorkspaceRole {OWNER, ADMIN, MEMBER}`, `ProjectRole {LEAD, MEMBER, VIEWER}`.
- **IDOR inter-tenant corrigés + testés** (PC-021 Pages, PC-034 pièces jointes) → accès croisé = **403**.

### 2.3 Protection des données (Art. 32)
- **Chiffrement au repos AES-256-GCM** sur 4 colonnes PII (converter JPA) ; **clé hors base** (variable
  d'env), **refus de démarrage prod sans clé** (`EncryptionKeyHolder`). → [[Chiffrement_Au_Repos]].
- **En transit** : TLS (terminaison nginx en prod).
- **RGPD** : export/portabilité, **anonymisation** à l'effacement + suppression de l'identité Keycloak.
  → [[Audit_RGPD_Conformite]], [[Procedure_Violation_Donnees]], [[DPIA_Analyse_Prealable]].

### 2.4 Surface HTTP (en-têtes, CORS, CSP)
- **En-têtes** (testés `SecurityHeadersWebMvcTest`) : HSTS `max-age=31536000; includeSubDomains; preload`,
  `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, **CSP API** `default-src 'none';
  frame-ancestors 'none'; form-action 'none'`, Referrer-Policy, **Permissions-Policy** (camera/micro/geo/
  payment/usb désactivés).
- ⚠️ **CORS** : `CorsConfig` code en dur les origines et **n'exploite pas** `cors.allowed-origins` (PC-027) —
  à piloter par variable d'env avant prod.

### 2.5 Limitation de débit
- **Bucket4j** par profil IP : AUTH_STRICT 10/60 s, AUTH_REFRESH 20/60 s, AI 20/60 s, DEFAULT 200/60 s ;
  émet `Retry-After` + `X-RateLimit-Remaining` ; exclut les préflights `OPTIONS` (PC-033).
- **Mode distribué Redis** supporté (`ProxyManager`) → TF-SEC-011 **résolu dans le code** (le
  [[Threat_Model_STRIDE]] le liste encore « gap D3 » : **à actualiser**).
- Tests : `RateLimitFilterTest` (8).

### 2.6 Validation d'entrée
- **Serveur (autorité)** : **76 `@Valid`** sur 27 fichiers (contrôleurs + DTOs), retours `ApiResponse<T>`.
- **Client** : **Zod** câblé sur les formulaires d'auth (login/register, `lib/validation/auth-schemas.ts`)
  — ferme l'écart « Zod déclaré mais inutilisé » (16/08).

### 2.7 Dépendances & secrets
- **Durcissement** : overrides Trivy dans le `pom.xml` (tomcat, netty, thymeleaf, bouncycastle, postgresql,
  jackson…) ; overrides front (sharp/ws).
- **Secrets** : uniquement par variables d'environnement ; `.env.*` **gitignore et non suivis**. Les valeurs
  courantes sont **absentes de l'historique git** (vérifié par pickaxe). ⚠️ **Action** : **roter** la clé Groq
  (morte) et les 2 secrets OAuth GitHub présents en clair dans `.env.dev` local avant remise du dossier.

---

## 3. Modèle de menaces (STRIDE) — résumé
Analyse complète : [[Threat_Model_STRIDE]] (6 catégories × flux réels). Points saillants : Spoofing couvert
par OIDC + Turnstile ; Tampering par signatures (JWT, webhook Stripe) ; Info disclosure par RBAC + chiffrement ;
DoS par rate limiting ; Elevation par les gardes d'autorisation. **Risque résiduel** principal = configuration
de prod (§6).

## 4. Couverture de tests sécurité
`SecurityHeadersWebMvcTest` (5), `EncryptedStringConverterTest` (11), `RateLimitFilterTest` (8),
`JwtIdentityResolverTest` (3), `AuthorizationServiceTest`, `TurnstileServiceTest` (9),
`HumanChallengeServiceTest` (10), `StripeWebhookServiceTest` (signature invalide → 400),
`GdprServiceIntegrationTest`. **Cas d'échec** (401/403/400, IDOR, signature) bien couverts.
→ Détail : [[Cahier_Test_Recettes]], [[Matrice_Tracabilite_Tests]].

## 5. Outillage & résultats de scan (SAST / SCA / DAST)

`scripts/security-scan.ps1` orchestre **Trivy** (images + fs : CVE, secrets, misconfig), **Semgrep**
(`--config auto` + `p/secrets`), **OWASP ZAP** (baseline DAST). Sorties JSON/HTML/SARIF.

### Run du 16/08/2026 (artefacts persistés — `security-reports/2026-08-16_18-54-07/` + `…_18-49-21/`)

| Outil | Portée | Résultat | Lecture |
|---|---|---|---|
| **Trivy — images** (backend + frontend) | CVE dépendances + OS | **0 CRITICAL · 25 HIGH · 61 MEDIUM** | Les **25 HIGH ont TOUTES un correctif disponible** (Next.js, Netty, Spring-webmvc/data, micrometer, curl/OS) → **hygiène de mise à jour** des dépendances |
| **Trivy — secrets (fs)** + **Semgrep p/secrets** | Secrets en clair | **0 secret** | Corrobore l'absence de secret dans le code et l'historique git (pickaxe) |
| **Semgrep SAST** (410 règles, 2597 fichiers) | Java + TS + IaC | **695 WARNING · 0 ERROR** | **632/695 (91 %) = `plaintext-http-link` dans du HTML** (bonne pratique https, non exploitable) ; **47 = tags GitHub Actions mutables** (durcissement CI). **1 `spring-sqli` = FAUX POSITIF vérifié** (`AnalyticsQueryService:116` : fragments SQL issus d'**enums figés** + `projectIds` en **paramètres liés**) ; 1 `script-tag` dans un fichier de **test**. **Aucun finding ERROR/bloquant réel.** |
| **OWASP ZAP — DAST** (backend + frontend live) | Vulns runtime | **0 HIGH · 4 MEDIUM** | En-têtes/hardening ; MEDIUM à revoir en contexte prod |

**Bilan** : **0 CRITICAL, 0 secret, 0 SAST ERROR, 0 DAST HIGH.** Le bruit Semgrep (liens http en HTML, tags CI)
relève de la bonne pratique, pas de la vulnérabilité.

**Correctifs de dépendances appliqués (17/08/2026).** Les CVE **HIGH corrigeables** (correctifs disponibles) ont
été montées — patchs de même mineure, vérifiées par `it.ps1 -Verify` (**874 tests, gate vert**) et `next build` :
- **Back (`pom.xml`)** : `spring-framework` 7.0.7 → **7.0.8** (spring-webmvc, spring-expression), `netty` 4.2.15 →
  **4.2.16**, `micrometer` 1.16.5 → **1.16.6**, `spring-data-commons` 4.0.5 → **4.0.6**.
- **Front (`package.json`)** : `next` 16.2.6 → **16.2.11** (4 CVE HIGH).
- **OS des images de base** : `apk upgrade --no-cache` ajouté aux Dockerfiles (curl/libcurl/libexpat/p11-kit back,
  openssl front) — les CVE OS ne se corrigent pas par le code applicatif.
- **`keycloak-admin-client` 25.0.6 → 26.0.6 ✅** (bump MAJEUR, fait dans une passe testée) : ferme la CVE HIGH
  `keycloak-core`. L'API admin réellement utilisée (`KeycloakService` : `users().create/get/search/update/
  resetPassword/remove/logout`) est stable entre 25 et 26 → **874 tests verts, 0 conflit transitif**. Le serveur
  Keycloak (image) reste indépendant de cette lib.

> ⚠️ **Limites du run** : le scan Trivy **fs** local est **très lent** dans cet environnement Docker (le
> scanner de secrets lit chaque fichier — observé > plusieurs heures, même avec `--skip-dirs`), et son rapport
> misconfig du 16/08 est ressorti vide. **Résolution (17/08)** : plutôt qu'un artefact local ponctuel,
> `security-scan.yml` exécute désormais **Trivy fs (vuln + secret + misconfig) en CI** à chaque push/PR → la
> couverture misconfig est **assurée en continu**. Le **0 CRITICAL** reste établi par le scan d'**images**
> (16/08) + les overrides CVE forcés dans le `pom.xml`. Le compteur de synthèse du script pour Semgrep était
> faux (0) — le vrai chiffre (695) est lu depuis `semgrep.txt` / `.json`.

### Industrialisation
- **Corrigé (17/08)** : scans **intégrés à la CI** — workflow `security-scan.yml` (Trivy deps/secrets/misconfig +
  Semgrep SAST) sur push/PR (`main`, `dev`) + run **hebdo** planifié ; rapport complet en artefact et **gate
  bloquant sur le plus haut niveau** (Trivy CRITICAL corrigeable + Semgrep ERROR — 0 aujourd'hui). Le DAST (ZAP)
  reste manuel via `security-scan.ps1 -Dast` (exige la stack levée). Clôt TF-SEC-002/003.
- **Corrigé (16/08)** : les **artefacts sont désormais archivés** et horodatés dans `security-reports/` (avant : seul un plan ZAP).

## 6. Risques résiduels & plan de traitement

| # | Risque | Sévérité | Traitement |
|---|---|---|---|
| PC-024 | Prod démarre en profil `dev` (Dockerfile) | ✅ **fait 17/08** | `Dockerfile` défaut `prod` (fail-safe) ; `docker-compose.prod.yml` déjà aligné |
| PC-026 | Seeds à mots de passe en clair migrables en prod | ✅ **fait 17/08** | Seeds (`V17/18/31/40`) déplacés en `db/seed`, chargés en **dev seulement** (base + prod + `it` = `db/migration`) ; vérifié `it.ps1 -Verify` (chaîne sans seeds, V73, 0 erreur) |
| PC-027 | CORS en dur (config env ignorée) | ✅ **fait 17/08** | `CorsConfig` lit `cors.allowed-origins` (`@Value` CSV) |
| PC-028 | Portes CI (couverture/scans) non bloquantes | ~~P0~~ **fait 17/08** | `backend-tests.yml` → `mvn verify` (gate JaCoCo ≥ 70 % **bloquant**) ; `security-scan.yml` (Trivy + Semgrep, gate CRITICAL/ERROR) |
| TF-SEC-002/003 | SAST/SCA non automatisés | ~~P1~~ **fait 17/08** | `security-scan.yml` (Semgrep + Trivy en CI) |
| TF-SEC-010 | DAST non automatisé | ✅ **fait 17/08** | `zap-dast.yml` — ZAP baseline **planifié (hebdo) + manuel**, gate sur alerte HIGH ; gaté sur l'opt-in stack (`E2E_ENABLED` + secret env), comme les E2E |
| — | Secrets tiers en clair dans `.env.dev` local | P1 | Roter (Groq, OAuth GitHub) |

---

## 7. Conclusion
Posture **applicative mûre et vérifiée** (auth, autorisation, chiffrement, en-têtes, rate limiting, validation,
RGPD), avec des **tests de sécurité réels** (succès + échec). Les portes CI (couverture JaCoCo + SAST/SCA)
sont désormais **bloquantes** (17/08), les preuves de scan persistées, les **3 P0 de config prod corrigés**
(profil, CORS, seeds, **pgvector** — PC-024/025/026/027) et **toutes les CVE HIGH corrigeables montées** (y
compris le bump majeur Keycloak 26). Le travail restant est surtout **documentaire** (actualiser STRIDE
rate-limiting et PSSI Turnstile) et l'hygiène de secrets. Aucune de ces réserves
ne compromet la démo ; elles sont tracées et priorisées ci-dessus et au [[Problemes_Connus]].

---
**Références** : [[PSSI]] · [[Threat_Model_STRIDE]] · [[Plan_Securisation_SSDLC]] · [[Auth_Autorisation]] ·
[[Chiffrement_Au_Repos]] · [[Audit_RGPD_Conformite]] · [[Procedure_Violation_Donnees]] ·
[[DPIA_Analyse_Prealable]] · [[Problemes_Connus]] · OWASP Top 10 · RGPD Art. 32.
