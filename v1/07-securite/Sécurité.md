---
id: securite
title: Sécurité — Posture, OWASP & pentest
doc_type: reference
statut: active
version: 1.0
date: "28/08/2026"
auteur: Pierre MICHEL
tags: [securite, owasp, pentest, zap, trivy, semgrep, rgpd, defense-en-profondeur]
---

# Sécurité — Posture, OWASP & pentest

> Défense en profondeur : authentification forte, autorisation centralisée, chiffrement,
> en-têtes durcis, journalisation, et outillage SAST/SCA/DAST automatisé.

## 1. Couverture OWASP Top 10

| Risque | Mesure | Testé |
| --- | --- | --- |
| **A01 Broken Access Control** | RBAC centralisé (`AuthorizationService`) + `WorkspaceAccessInterceptor` + **visibilité projet `ProjectVisibilityGuard`** (privé → 404) + **temps réel par canal `RealtimeAuthorizationService`** (H2) + **scoping liens GitHub** (H1) ; autz au niveau service | `AuthorizationServiceTest`, IDOR sur Issue/Redistribution/Workspace |
| **A02 Cryptographic Failures** | Chiffrement PII libre au repos (`EncryptedStringConverter`, AES-256-GCM) ; TLS en transit | `EncryptedStringConverterTest` |
| **A03 Injection** | JPA paramétré (pas de SQL concaténé) ; validation `@Valid`/Zod | slices `@WebMvcTest` (`@Valid`→400) |
| **A05 Security Misconfiguration** | En-têtes durcis : CSP, HSTS, X-Frame DENY, nosniff, Referrer-Policy, Permissions-Policy (`SecurityConfig`) | **`SecurityHeadersWebMvcTest`** |
| **A07 Identification & Auth Failures** | Keycloak **OIDC RS256** (tokens émis par l'IdP), **2FA TOTP** (`TwoFactorService`), refresh token en **cookie HttpOnly**, OTP, **rate-limiting** brute-force (`RateLimitFilter`), refresh/logout natifs OIDC | `AuthServiceTest`, `RateLimitFilterTest`, `OtpServiceTest`, `TwoFactorServiceTest` |
| **A09 Logging & Monitoring** | Journal d'audit (`AuditLog`) : login, rôles, suppression, RGPD, redistribution | hooks + `GET /audit` |
| **A10 SSRF** | Validation des URL de webhook **sortantes** (`SsrfGuard`) : http(s) public only, IP interne (boucle/privé/link-local/CGNAT/ULA) rejetée à la config **et** à l'envoi | `SsrfGuardTest`, `WebhookServiceIntegrationTest` |

## 2. Chiffrement au repos (état V1)
- **Colonne (AES-256-GCM)** : PII libre non requêtée (`EnterpriseInquiry.message/notes`).
- **Non chiffré en colonne** : email/nom/skills/worklogs (clés de recherche — GCM non déterministe casserait les lookups) → mitigé par RBAC + TLS + anonymisation à l'effacement.
- **Cible** : chiffrement **disque/volume** (infra, transparent) au déploiement → couvre tout.

## 3. Outillage automatisé — `scripts/security-scan.ps1`

| Type | Outil | Portée |
| --- | --- | --- |
| **SAST** (code) | Semgrep (`--config auto` + `p/secrets`) | secrets, patterns dangereux |
| **SAST** (flux/taint) | **CodeQL** (`security-extended`) | suivi de flux de données, code scanning GitHub |
| **SCA** (dépendances) | Trivy filesystem | CVE des libs (npm/maven) |
| **Images** | Trivy image | vulnérabilités des conteneurs |
| **DAST** (app en marche) | **OWASP ZAP baseline** (`-Dast`) | vulns web dynamiques (headers, CSP, cookies…) |

```powershell
.\scripts\security-scan.ps1            # SAST + SCA + images
.\scripts\security-scan.ps1 -Dast      # DAST ZAP (app levée requise)
```

> **En CI** (depuis le 17-28/08) : `security-scan.yml` (Semgrep + Trivy, push/PR, gate CRITICAL/ERROR),
> `codeql.yml` (CodeQL `security-extended`, push/PR + hebdo), `zap-dast.yml` (ZAP baseline planifié/manuel,
> gate HIGH). Le script local reste l'outil d'exécution à la demande.

## 4. Pentest — résultats (04/07/2026, ZAP baseline)

| Cible | Alertes | HIGH | MEDIUM |
| --- | --- | --- | --- |
| **Backend** (`:8080`) | 1 | **0** | **0** |
| **Frontend** (`:3000`) | 15 | **0** | 4 |

- **Aucune vulnérabilité HIGH/critique.** Backend **clean** (en-têtes durcis validés).
- **4 MEDIUM (frontend)** = **CSP permissive** : `script-src 'unsafe-eval' 'unsafe-inline'`, `style-src 'unsafe-inline'`, wildcard.
  **Tradeoff connu & assumé** (cf. `next.config.ts`) : `unsafe-eval` requis par le HMR **dev** Next.js, `unsafe-inline` par Tailwind/hydration.
  **Durcissement** : CSP **par nonce** sur le **build de production** (middleware Next) → retire `unsafe-*`. → phase déploiement.
- Reste : LOW×6 / INFO×5 (informationnel).

## 5. RGPD
Voir [PS/PCA/PRA](../11-pca-pra/PS_PCA_PRA.md) (sauvegarde) et le chantier C11 : audit, chiffrement, droits export/effacement validés (`GdprService`).
