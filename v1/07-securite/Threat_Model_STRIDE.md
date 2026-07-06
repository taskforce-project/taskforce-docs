---
id: threat-model-stride
title: Threat Model STRIDE — TaskForce V1
doc_type: securite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [threat-model, stride, securite, menaces, owasp, risques, memoire, rncp, soutenance]
---

# 🎯 Threat Model STRIDE — TaskForce V1

> Analyse structurée des menaces selon la méthode **STRIDE** (Microsoft), appliquée aux flux
> critiques de TaskForce. Pour chaque menace : le **vecteur**, la **mitigation réellement
> implémentée** (avec preuve code) et le **risque résiduel**.
>
> **STRIDE** = **S**poofing (usurpation) · **T**ampering (altération) · **R**epudiation (déni) ·
> **I**nformation Disclosure (divulgation) · **D**enial of Service (déni de service) ·
> **E**levation of Privilege (élévation de privilège).

---

## 1. Périmètre et actifs à protéger

| Actif | Sensibilité | Localisation |
|---|---|---|
| Credentials utilisateurs | 🔴 Secrète | Keycloak (hash) |
| Tokens JWT / refresh (émis par Keycloak) | 🔴 Secrète | Client (access) + cookie HttpOnly (refresh) ; sessions gérées par Keycloak |
| Données personnelles (PII) | 🟠 Sensible | PostgreSQL (`users`, `enterprise_inquiries`) |
| Données métier (issues, pages, chat) | 🟠 Confidentielle | PostgreSQL (multi-tenant) |
| Secrets d'intégration (Stripe, Groq…) | 🔴 Secrète | Variables d'environnement |
| Fichiers uploadés | 🟠 Confidentielle | MinIO |
| Facturation / abonnements | 🟠 Sensible | PostgreSQL + Stripe |

## 2. Diagramme de flux de données (DFD) — vue macro

```
                         ┌─────────────┐
                         │  Utilisateur│
                         └──────┬──────┘
                       HTTPS/TLS │ WSS
                    ┌────────────▼─────────────┐
                    │   Frontend Next.js 16    │  ← CSP, en-têtes
                    └────────────┬─────────────┘
                       Bearer JWT │  (frontière de confiance)
      ┌──────────────────────────▼──────────────────────────┐
      │  Backend Spring Boot 4                               │
      │  ① RateLimitFilter  ② SecurityFilterChain (JWT)      │
      │  ③ WorkspaceAccessInterceptor  ④ AuthorizationService│
      └───┬───────────┬───────────┬───────────┬──────────────┘
          │           │           │           │
   ┌──────▼───┐ ┌─────▼────┐ ┌────▼────┐ ┌────▼─────┐
   │PostgreSQL│ │ Keycloak │ │  MinIO  │ │ Externes │
   │multi-tnt │ │ identité │ │ fichiers│ │Stripe/Groq│
   └──────────┘ └──────────┘ └─────────┘ └──────────┘
```

Les **4 gardes** ①②③④ constituent la défense en profondeur côté backend.

---

## 3. Analyse STRIDE par catégorie

### 3.1 🎭 Spoofing — Usurpation d'identité

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| S1 | Forger un JWT valide | Fabriquer un token sans la clé privée | Signature **RS256** (clé privée détenue par Keycloak) vérifiée via JWK + issuer par `NimbusJwtDecoder` | `SecurityConfig.jwtDecoder()`, `AuthServiceTest` | 🟢 Faible |
| S2 | Rejouer un token volé | Vol de token (XSS, MITM) | TLS + expiration courte + **révocation de session Keycloak** (`users().logout()`) | `SecurityConfig`, `KeycloakAuthService` | 🟢 Faible (révocation IdP possible) |
| S3 | Brute-force de credentials | Essais massifs sur `/login` | Rate limiting 10 req/min/IP + Keycloak | `RateLimitFilter` (AUTH_STRICT) | 🟢 Faible |
| S4 | Usurper une connexion WebSocket | Se connecter sans identité | Auth JWT au CONNECT STOMP | `StompAuthInterceptor`, `StompAuthInterceptorTest` | 🟢 Faible |
| S5 | Faux compte à l'inscription | Email d'autrui | Vérification OTP (TTL 15 min) | `OtpService`, `V6` | 🟢 Faible |

> **✅ S2 traité (05/07/2026)** : migration effectuée vers **Keycloak RS256 asymétrique + révocation
> OIDC** (`users().logout()`). Le risque résiduel de rejeu passe de moyen à faible. → [[Journal_Decisions_ADR|ADR-011]], TF-SEC-009.

### 3.2 🔧 Tampering — Altération de données

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| T1 | Modifier le contenu d'un JWT | Altérer claims (rôle, email) | Signature **RS256** vérifiée via JWK Keycloak → token altéré rejeté | `SecurityConfig.jwtDecoder()` (signature invalide → 401) | 🟢 Faible |
| T2 | Injection SQL | Payload dans un champ | JPA paramétré (aucune concaténation) | Repos JPA, slices `@WebMvcTest` | 🟢 Faible |
| T3 | Falsifier un webhook Stripe | POST forgé sur `/api/stripe/**` | Vérification signature HMAC `Webhook.constructEvent` | `PaymentAndDataControllersWebMvcTest` (sig invalide → 400) | 🟢 Faible |
| T4 | Rejouer un webhook Stripe | Doublon d'événement | Idempotence `stripe_event_id UNIQUE` | `StripeWebhookServiceTest`, `V36` | 🟢 Faible |
| T5 | Injection de fausses lignes de log | `\n`/`\r` dans un message client | Sanitisation avant journalisation | `ClientLogController.sanitize()` | 🟢 Faible |
| T6 | Altérer les données d'un autre tenant | Requête cross-workspace | Isolation `workspace_id` centralisée | `WorkspaceAccessInterceptor` | 🟢 Faible |

### 3.3 📝 Repudiation — Déni d'action

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| R1 | Nier une action sensible (suppression, changement de rôle) | Absence de trace | `AuditLog` immuable (login, rôles, suppression, RGPD, redistribution) | `AuditLog.java`, `GET /audit` | 🟢 Faible |
| R2 | Nier une erreur client | Pas de corrélation | Journalisation `ClientLogController` avec identité (si JWT) → SigNoz | `ClientLogController` | 🟢 Faible |
| R3 | Perte de traçabilité (logs altérés) | Accès aux logs | Centralisation OTEL→SigNoz (hors application) | `otel-collector-config.yaml` | 🟠 Moyen (rétention/immuabilité SigNoz à durcir en prod) |

### 3.4 🔍 Information Disclosure — Divulgation

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| I1 | IDOR — lire une ressource d'un autre workspace | ID devinable | Garde d'appartenance transverse (403 non-membre) | `WorkspaceAccessInterceptor`, `AuthorizationServiceTest` | 🟢 Faible |
| I2 | Fuite de stack trace / détails internes | Erreur non gérée | `GlobalExceptionHandler` + enveloppe `ApiResponse<T>` | Convention CT-07 | 🟢 Faible |
| I3 | Vol de PII en base | Accès disque / dump | Chiffrement AES-256-GCM (PII libre) + cible chiffrement volume | `EncryptedStringConverter` | 🟠 Moyen (email/nom non chiffrés en colonne — clés de recherche) |
| I4 | Interception réseau (MITM) | Trafic clair | TLS/HTTPS (Nginx prod) + HSTS preload | `SecurityConfig` (HSTS 1 an) | 🟢 Faible |
| I5 | Fuite de secrets | Secret en dur / commit | Variables d'env, `.env` non versionné, scan Semgrep `p/secrets` | `security-scan.ps1`, CT-05 | 🟢 Faible |
| I6 | Énumération de comptes | Réponses login distinctes | `401` uniforme (pas de leak « email inconnu ») | `AuthServiceTest` | 🟢 Faible |
| I7 | Clickjacking / embedding | iframe malveillante | `X-Frame-Options: DENY` + CSP `frame-ancestors 'none'` | `SecurityHeadersWebMvcTest` | 🟢 Faible |

### 3.5 🚫 Denial of Service — Déni de service

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| D1 | Flood d'authentification | Requêtes massives sur `/login` | Rate limiting AUTH_STRICT (10/min/IP) | `RateLimitFilter` | 🟢 Faible |
| D2 | Épuisement quota LLM (Groq) | Spam smart-assign | Rate limiting AI (20/min/IP) + mode dégradé scoring local | `RateLimitFilter`, `SmartAssignService` | 🟢 Faible |
| D3 | Flood API générique | Requêtes massives | Rate limiting DEFAULT (200/min/IP) | `RateLimitFilter` | 🟠 Moyen (in-memory, mono-instance — pas distribué) |
| D4 | Indisponibilité broker (RabbitMQ) | Panne broker | Repli automatique `SimpleBroker` in-memory | `WebSocketConfig` (DISP-04) | 🟢 Faible |
| D5 | DoS applicatif (payload volumineux) | Gros body/stack | Bornage taille (`@Size` 8000 sur stack log) | `ClientLogRequest` | 🟠 Moyen (bornage non systématique partout) |

> **Point d'attention D3** : `RateLimitFilter` stocke les buckets en `ConcurrentHashMap`
> (mémoire locale). En déploiement multi-instances, il faudra un backend distribué
> (Redis/Bucket4j distributed) pour un rate limiting cohérent. → gap TF-SEC-011.

### 3.6 ⬆️ Elevation of Privilege — Élévation de privilège

| # | Menace | Vecteur | Mitigation implémentée | Preuve | Résiduel |
|---|---|---|---|---|:---:|
| E1 | Agir au-delà de son rôle (MEMBER → ADMIN) | Appel d'endpoint protégé | `requireManager` / `assertIsOwner` au niveau service | `AuthorizationService`, `AuthorizationServiceTest` | 🟢 Faible |
| E2 | Auto-promotion de rôle | Modifier son propre rôle | Contrôle serveur : seuls ADMIN/OWNER changent les rôles ; OWNER non rétrogradable par ADMIN | `AuthorizationServiceTest` (UC04-06) | 🟢 Faible |
| E3 | Accès manager masqué contourné | Confiance au flag front | Autorisation revérifiée côté serveur (le front ne décide pas) | `AuthorizationService` | 🟢 Faible |
| E4 | Accès à un workspace non membre | Slug d'un autre tenant | `WorkspaceAccessInterceptor` (403) | `WorkspaceAccessInterceptor` | 🟢 Faible |
| E5 | Escalade via endpoint public oublié | Endpoint sensible dans `PUBLIC_MATCHERS` | Liste `PUBLIC_MATCHERS` restreinte + revue | `SecurityConfig.PUBLIC_MATCHERS` | 🟠 Moyen (à auditer à chaque ajout d'endpoint) |

---

## 4. Synthèse des risques résiduels

| Risque résiduel | Catégorie | Niveau | Action / backlog |
|---|---|:---:|---|
| Secret HS512 symétrique, pas de révocation immédiate | Spoofing S2 | 🟠 Moyen | Migration Keycloak RS256/OIDC — **TF-SEC-009** |
| Rate limiting non distribué (mono-instance) | DoS D3 | 🟠 Moyen | Backend distribué (Redis) — **TF-SEC-011** |
| Email/nom non chiffrés en colonne | Info Disclosure I3 | 🟠 Moyen | Chiffrement volume prod (transparent) — infra |
| Immuabilité/rétention des logs SigNoz | Repudiation R3 | 🟠 Moyen | Durcir rétention prod — **TF-INFRA-005** |
| `PUBLIC_MATCHERS` à auditer à chaque ajout | Elevation E5 | 🟠 Moyen | Checklist revue de code sécu |
| Scans SAST/DAST non bloquants en CI | Transverse | 🟠 Moyen | SAST/SCA **TF-SEC-002/003** + DAST **TF-SEC-010** |
| Bornage de payload non systématique | DoS D5 | 🟢 Faible | Étendre `@Size`/limites body |

**Bilan** : aucune menace au niveau 🔴 Élevé non mitigée. Les gardes ①②③④ couvrent les menaces
majeures (spoofing, tampering, IDOR, élévation). Les risques résiduels sont **Moyens** et tracés
au backlog — cohérent avec le résultat du pentest ZAP (0 HIGH/critique, cf. [[Sécurité]] §4).

---

## 5. Couverture STRIDE ↔ OWASP ↔ tests

| STRIDE | OWASP 2021 | Test principal |
|---|---|---|
| Spoofing | A07 Auth Failures | `AuthServiceTest`, `JwtIdentityResolverTest`, `RateLimitFilterTest` |
| Tampering | A03 Injection, A08 Data Integrity | `StripeWebhookServiceTest`, slices `@WebMvcTest` |
| Repudiation | A09 Logging Failures | `AuditLog` + revue |
| Info Disclosure | A01, A02 | `AuthorizationServiceTest`, `EncryptedStringConverterTest`, `SecurityHeadersWebMvcTest` |
| Denial of Service | A05 (config) | `RateLimitFilterTest` |
| Elevation of Privilege | A01 Broken Access Control | `AuthorizationServiceTest` |

---

> 🔗 [[PSSI]] (politique) — [[Plan_Securisation_SSDLC]] (mise en œuvre) — [[Sécurité]] (posture + pentest) —
> [[Auth_Autorisation]] (mécanismes) — [[Matrice_Tracabilite_Tests]] (couverture SEC) —
> [[Roadmap_Backlog]] (TF-SEC-009/010/011, TF-INFRA-005)
