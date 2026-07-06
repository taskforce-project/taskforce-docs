---
id: plan-securisation-ssdlc
title: Plan de sécurisation & S-SDLC — TaskForce V1
doc_type: securite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [securite, ssdlc, plan-securisation, devsecops, sast, dast, sca, owasp, memoire, rncp, soutenance]
---

# 🔒 Plan de sécurisation & S-SDLC — TaskForce V1

> Décrit **comment** la sécurité est intégrée à chaque étape du cycle de vie du logiciel
> (Secure Software Development Life Cycle) et le **plan de sécurisation en 5 étapes**
> appliqué à TaskForce. Tout est ancré dans l'outillage et le code réels.
>
> **Cadre** : ISO/IEC 27034 (sécurité applicative), OWASP SAMM, OWASP ASVS L1.

---

## 1. Le S-SDLC de TaskForce

La sécurité n'est pas une phase finale mais un fil rouge sur tout le cycle. Chaque étape porte
des contrôles concrets, outillés et **vérifiables**.

```
 ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐
 │  1.CONCE- │──▶│ 2.CONCEP- │──▶│ 3.DÉVELOP-│──▶│  4.TESTS  │──▶│ 5.DÉPLOI- │──▶│ 6.EXPLOI- │
 │   PTION   │   │   TION    │   │   PEMENT  │   │   SÉCU    │   │   EMENT   │   │  TATION   │
 └───────────┘   └───────────┘   └───────────┘   └───────────┘   └───────────┘   └───────────┘
  Exigences      Threat model    Règles d'or +   SAST/SCA/DAST   Secrets/TLS +   Audit + logs
  sécu (STB)     STRIDE + ADR    code sécurisé   + tests auto    en-têtes prod   + monitoring
```

### 1.1 Étape 1 — Conception des exigences

- Exigences de sécurité formalisées et **mesurables** dans le [[STB]] §4 (SEC-01 à SEC-10).
- Traduction des besoins RGPD (portabilité, oubli) en exigences techniques (CONF-01/02).
- **Preuve** : `01-projet/STB.md`, [[Matrice_Tracabilite_Tests]].

### 1.2 Étape 2 — Conception sécurisée

- **Threat modeling STRIDE** sur les flux critiques (auth, paiement, multi-tenant) — [[Threat_Model_STRIDE]].
- Décisions d'architecture de sécurité tracées en ADR (Keycloak, no-mock, isolation).
- Modèle RBAC 3 niveaux conçu avant le code (`WorkspaceRole`).
- **Preuve** : [[Journal_Decisions_ADR]], [[Diagramme_Cas_Usage_UML]] (cas gardés par le code).

### 1.3 Étape 3 — Développement sécurisé

Règles d'or appliquées à chaque commit (cf. `CLAUDE.md`) :

| Règle | Effet sécurité |
|---|---|
| Validation `@Valid` (back) / Zod (front) | Anti-injection, anti-données malformées |
| Secrets par variables d'env, jamais en dur | Anti-fuite de secrets |
| JPA paramétré (pas de SQL concaténé) | Anti-injection SQL |
| Autorisation au niveau service | Anti-élévation de privilège / IDOR |
| Enveloppe `ApiResponse<T>` + `GlobalExceptionHandler` | Pas de fuite de stack trace |

- **Preuve** : `SecurityConfig`, `AuthorizationService`, `EncryptedStringConverter`, `RateLimitFilter`.

### 1.4 Étape 4 — Tests de sécurité

- Tests unitaires/composant ciblés sécurité (priorité P0) — [[Politique_Tests]] §4.
- Analyse statique et dynamique automatisée — `scripts/security-scan.ps1`.
- **Preuve** : `SecurityHeadersWebMvcTest`, `AuthServiceTest`, `RateLimitFilterTest`,
  `EncryptedStringConverterTest`, `AuthorizationServiceTest`.

### 1.5 Étape 5 — Déploiement sécurisé

- Secrets injectés à l'exécution (jamais dans l'image).
- TLS/HTTPS via Nginx reverse-proxy.
- En-têtes durcis actifs (CSP, HSTS, X-Frame, nosniff…).
- Durcissement CSP frontend par nonce sur le build de production.
- **Preuve** : `docker-compose.prod.yml`, `SecurityConfig.applySecurityHeaders()`, `next.config.ts`.

### 1.6 Étape 6 — Exploitation & supervision

- Audit immuable (`AuditLog`) + journalisation OTEL→SigNoz.
- Métriques Prometheus (latence, erreurs) + alertes.
- Triage continu des vulnérabilités (PC-xxx → TF-xxx).
- **Preuve** : `observability/alerts/`, `09-audits/Problemes_Connus.md`.

---

## 2. Plan de sécurisation en 5 étapes

Démarche méthodique appliquée pour sécuriser l'application, du diagnostic à la vérification.

### Étape 1 — Cartographier la surface d'attaque

| Surface | Points d'entrée |
|---|---|
| API REST | 33 contrôleurs / ~130 endpoints (dont `/api/auth/**` public) |
| WebSocket | `/ws/**`, `/ws-sockjs/**` (STOMP, auth par `StompAuthInterceptor`) |
| Webhooks entrants | Stripe (`/api/stripe/**`), GitHub/Slack callbacks OAuth |
| Intégrations sortantes | Keycloak, Stripe, Groq, GitHub, Slack, MinIO, SMTP |
| Stockage | PostgreSQL (multi-tenant), MinIO (fichiers) |

→ Détail des menaces par surface : [[Threat_Model_STRIDE]].

### Étape 2 — Durcir l'authentification et l'autorisation

| Mesure | Statut | Preuve |
|---|:---:|---|
| JWT signé + validé (RS256, Keycloak) | ✅ | `SecurityConfig` (décodeur JWK) |
| OTP à l'inscription | ✅ | `OtpService` |
| Rate limiting brute-force | ✅ | `RateLimitFilter` |
| RBAC centralisé 3 niveaux | ✅ | `AuthorizationService` |
| Garde anti-IDOR transverse | ✅ | `WorkspaceAccessInterceptor` |
| Émission JWT par Keycloak (RS256/OIDC) | ⬜ cible | TF-SEC-009 |

### Étape 3 — Protéger les données et les communications

| Mesure | Statut | Preuve |
|---|:---:|---|
| Chiffrement au repos (PII libre) AES-256-GCM | ✅ | `EncryptedStringConverter` |
| TLS/HTTPS en transit | ✅ (prod) | Nginx `docker-compose.prod.yml` |
| Isolation multi-tenant (`workspace_id`) | ✅ | `WorkspaceAccessInterceptor` |
| Anonymisation à l'effacement (RGPD) | ✅ | `GdprService.anonymize` |
| Chiffrement disque/volume | ⬜ cible | déploiement infra |

### Étape 4 — Durcir la configuration et bloquer les injections

| Mesure | Statut | Preuve |
|---|:---:|---|
| En-têtes de sécurité HTTP (6 en-têtes) | ✅ | `SecurityConfig.applySecurityHeaders()` |
| CSP API `default-src 'none'` | ✅ | `SecurityConfig.API_CSP` |
| Sessions STATELESS (pas de session serveur) | ✅ | `SessionCreationPolicy.STATELESS` |
| Validation entrées `@Valid`/Zod | ✅ | slices `@WebMvcTest` |
| Sanitisation anti log-forging | ✅ | `ClientLogController.sanitize()` |
| Signature HMAC webhooks Stripe | ✅ | `StripeWebhookController` |
| CSP frontend par nonce (prod) | ⬜ cible | `next.config.ts` |

### Étape 5 — Vérifier en continu (scan + tests + monitoring)

| Mesure | Statut | Preuve |
|---|:---:|---|
| SAST (Semgrep) | ✅ | `security-scan.ps1` |
| SCA (Trivy filesystem + image) | ✅ | `security-scan.ps1` |
| DAST (ZAP baseline) | ✅ | `security-scan.ps1 -Dast` |
| Tests sécurité automatisés | ✅ | suite JUnit prioritaire |
| Audit + monitoring | ✅ | `AuditLog`, SigNoz, Prometheus |
| Intégration scans en CI | ⬜ cible | TF-SEC-002/003 (SAST/SCA), TF-SEC-010 (DAST) |

---

## 3. Outillage DevSecOps — `scripts/security-scan.ps1`

| Type | Outil | Portée | Commande |
|---|---|---|---|
| SAST | Semgrep (`--config auto` + `p/secrets`) | secrets, patterns dangereux | `.\scripts\security-scan.ps1` |
| SCA | Trivy filesystem | CVE libs (npm/maven) | idem |
| Images | Trivy image | vulns conteneurs | idem |
| DAST | OWASP ZAP baseline | vulns web dynamiques | `.\scripts\security-scan.ps1 -Dast` |

---

## 4. Checklist « 10 commandements » du développeur sécurisé

Appliquée à chaque contribution TaskForce :

1. **Tu ne feras jamais confiance à l'entrée utilisateur** → `@Valid` / Zod systématique.
2. **Tu ne concaténeras point de SQL** → JPA paramétré uniquement.
3. **Tu vérifieras l'autorisation au niveau service** → `AuthorizationService`, jamais côté client seul.
4. **Tu n'exposeras aucun secret dans le code** → variables d'environnement, `.env` non versionné.
5. **Tu chiffreras les données sensibles** → au repos (GCM) + en transit (TLS).
6. **Tu durciras les en-têtes HTTP** → CSP, HSTS, X-Frame, nosniff par défaut.
7. **Tu limiteras le débit des endpoints sensibles** → `RateLimitFilter`.
8. **Tu ne divulgueras pas de stack trace** → `GlobalExceptionHandler` + `ApiResponse<T>`.
9. **Tu journaliseras les actions sensibles** → `AuditLog`, en neutralisant le log-forging.
10. **Tu testeras chaque correctif de sécurité** → un bug de sécu = un test de non-régression.

---

## 5. Revue de code sécurité

- **Règles d'or** vérifiées à chaque PR (cf. `CLAUDE.md` § « Ne JAMAIS faire »).
- **Points de contrôle** : pas de `any`, pas de mock, pas de secret en dur, pas de `context-path`,
  pas d'édition de migration appliquée.
- **Traçabilité** : tout correctif de sécurité référence un `PC-xxx` (problème) et un `TF-SEC-xxx`
  (backlog), avec test associé.

---

> 🔗 [[PSSI]] (politique) — [[Threat_Model_STRIDE]] (menaces) — [[Sécurité]] (posture + pentest) —
> [[Politique_Tests]] (tests sécu) — [[STB]] §4 (exigences) — [[Roadmap_Backlog]] (TF-SEC-009/010/011)
