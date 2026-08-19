---
id: pssi
title: PSSI — Politique de Sécurité du Système d'Information
doc_type: securite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [pssi, securite, gouvernance, ssi, owasp, rgpd, politique, memoire, rncp, soutenance]
---

# 🛡️ PSSI — Politique de Sécurité du Système d'Information

> Politique formelle décrivant les **objectifs de sécurité**, les **règles** et les **responsabilités**
> qui encadrent TaskForce. Chaque règle est **ancrée dans une mesure réellement implémentée**
> (code, config, migration) ou explicitement marquée comme **cible** (renvoyée au plan de sécurisation).
>
> **Portée** : application SaaS TaskForce V1 (backend Spring Boot 4, frontend Next.js 16, PostgreSQL 18,
> Keycloak, Stripe, MinIO, RabbitMQ) — environnements dev et cible de production.
>
> **Cadre de référence** : OWASP Top 10 2021, OWASP ASVS L1, RGPD, ISO/IEC 27034 (sécurité applicative).

---

## 1. Objectifs de sécurité (DICP)

La politique poursuit les quatre critères classiques de sécurité de l'information :

| Critère | Objectif TaskForce | Mesure principale |
|---|---|---|
| **D**isponibilité | Service accessible aux utilisateurs légitimes | Rate limiting, repli WebSocket in-memory, PCA/PRA (backup quotidien) |
| **I**ntégrité | Données non altérées de façon non autorisée | RBAC au niveau service, isolation multi-tenant, JPA paramétré, audit log |
| **C**onfidentialité | Données accessibles aux seules personnes autorisées | JWT + Keycloak, chiffrement au repos (AES-256-GCM), TLS, en-têtes durcis |
| **P**reuve / traçabilité | Actions sensibles imputables | `AuditLog` (login, rôles, suppression, RGPD, redistribution), journalisation OTEL→SigNoz |

---

## 2. Principes directeurs

1. **Défense en profondeur** — aucune mesure unique n'est un point de défaillance : plusieurs
   couches (réseau/TLS, filtre rate-limit, chaînes Spring Security, garde RBAC transverse,
   autorisation service, chiffrement colonne).
2. **Moindre privilège** — un utilisateur n'obtient que les droits de son rôle
   (`OWNER ⊃ ADMIN ⊃ MEMBER`), vérifié à chaque action sensible.
3. **Sécurité par conception (Security by Design)** — les contrôles sont intégrés au code
   (intercepteurs, converters, filtres) et non ajoutés a posteriori.
4. **Secure by default** — configuration durcie par défaut : CSP `default-src 'none'`,
   sessions STATELESS, secrets par variables d'environnement.
5. **Ne jamais faire confiance à l'entrée** — validation `@Valid` (back) / Zod (front),
   sanitisation des logs, signatures de webhooks vérifiées.
6. **Traçabilité des actions sensibles** — journalisation + audit immuable.

---

## 3. Gestion des identités et des accès (IAM)

### 3.1 Authentification

| Règle | Implémentation | Preuve |
|---|---|---|
| Tout accès aux ressources métier exige un JWT valide | 3e `SecurityFilterChain` `@Order(2)` → `anyRequest().authenticated()` | `SecurityConfig.java` |
| Les JWT sont signés (intégrité du token) | **RS256 émis par Keycloak**, validés via son JWK Set + issuer par `NimbusJwtDecoder` | `SecurityConfig.jwtDecoder()` |
| Vérification d'identité à l'inscription | OTP à usage unique, TTL 15 min | `OtpService`, migration `V6` |
| Protection anti-brute-force | Rate limiting par IP (10 req/min sur login) | `RateLimitFilter` (Bucket4j) |
| Protection anti-robots à l'inscription (anti-spoofing / anti-abus de volume) | Double barrière : **Cloudflare Turnstile** (juge le visiteur, `siteverify` côté serveur) + **défi signé maison sans tiers** (jeton HMAC : délai humain minimal + péremption) ; repli conservateur si Cloudflare est injoignable, le défi signé restant actif | `TurnstileService`, `HumanChallengeService` (tests `TurnstileServiceTest`, `HumanChallengeServiceTest`) |
| Référentiel d'identités centralisé | Keycloak (Admin REST API) | `KeycloakService` |

> ✅ **PC-019 / TF-SEC-009 résolus (05/07/2026, [[Journal_Decisions_ADR|ADR-011]])** : les tokens sont
> désormais émis et signés par **Keycloak (RS256/OIDC)** ; le backend agit en Resource Server (plus de
> `JwtService` ni de secret symétrique). Bénéfices acquis : révocation de session (`users().logout()`),
> refresh OIDC natif, rotation de clés (JWK).

### 3.2 Autorisation (RBAC)

| Niveau | Contrôle | Preuve |
|---|---|---|
| Périmètre workspace | Garde transverse : appartenance obligatoire sous `/api/workspaces/{slug}/...` | `WorkspaceAccessInterceptor` |
| Rôle workspace | `getMemberOrThrow` / `requireManager` / `assertIsOwner` | `AuthorizationService` |
| Rôle projet | `ProjectMember` (MANAGER / MEMBER) | `AuthorizationService` |
| Fermeture des IDOR | Vérification `workspace_id` centralisée (fail-open sur incertitude, 403 sur non-membre) | `WorkspaceAccessInterceptor`, `AuthorizationServiceTest` |

### 3.3 Gestion des secrets

- **Aucun secret en dur** dans le code source (règle d'or #8) — tous via variables d'environnement.
- `.env` **non versionné** (contrainte CT-05).
- Secrets couverts : `KEYCLOAK_CLIENT_SECRET`, `KEYCLOAK_ADMIN_PASSWORD`, `STRIPE_SECRET_KEY`,
  `STRIPE_WEBHOOK_SECRET`, `POSTGRES_PASSWORD`, clé de chiffrement (`EncryptionKeyHolder`).
  *(Plus de `JWT_SECRET` depuis [[Journal_Decisions_ADR|ADR-011]] : la validation repose sur la clé publique JWK de Keycloak.)*

---

## 4. Protection des données

### 4.1 Chiffrement

| État | Mesure | Preuve |
|---|---|---|
| En transit | TLS/HTTPS via Nginx (production) | `docker-compose.prod.yml` |
| Au repos (colonne) | AES-256-GCM sur PII libre non requêtée (`EnterpriseInquiry.message/notes`) | `EncryptedStringConverter` |
| Au repos (cible) | Chiffrement disque/volume (infra, transparent) au déploiement | plan de sécurisation |

**Choix assumé** : email/nom/skills **ne sont pas** chiffrés en colonne car ce sont des clés de
recherche (GCM non déterministe casserait les `findByEmail`). Mitigation : RBAC + TLS + anonymisation
à l'effacement (droit à l'oubli RGPD).

### 4.2 Classification des données

| Classe | Exemples | Protection |
|---|---|---|
| **Sensible (PII)** | email, nom, prénom, messages | RBAC, TLS, anonymisation à l'effacement |
| **Confidentielle métier** | issues, pages, discussions | Isolation multi-tenant + RBAC |
| **Secrète** | mots de passe, secrets API, clés | Keycloak (hash), variables d'env, jamais en base en clair |
| **Publique** | landing, pages marketing | Aucune restriction |

### 4.3 Conformité RGPD

- **Portabilité (Art. 20)** : export JSON des données personnelles — `GdprService.exportMyData`.
- **Droit à l'oubli (Art. 17)** : anonymisation — `GdprService.anonymize`.
- **Traçabilité** : registre des traitements (Art. 30) — *à produire (Phase 8)*.

---

## 5. Sécurité applicative (couverture OWASP)

Synthèse — le détail par risque et les tests associés sont dans [[Sécurité]] et le [[Threat_Model_STRIDE]].

| Risque OWASP 2021 | Mesure | Preuve |
|---|---|---|
| A01 Broken Access Control | RBAC centralisé + interceptor anti-IDOR | `AuthorizationServiceTest` |
| A02 Cryptographic Failures | AES-256-GCM au repos + TLS | `EncryptedStringConverterTest` |
| A03 Injection | JPA paramétré + validation `@Valid`/Zod | slices `@WebMvcTest` |
| A05 Security Misconfiguration | En-têtes durcis (CSP/HSTS/X-Frame/nosniff/Referrer/Permissions) | `SecurityHeadersWebMvcTest` |
| A07 Auth Failures | OIDC Keycloak (RS256) + OTP + rate-limiting | `AuthServiceTest`, `RateLimitFilterTest` |
| A08 Data Integrity Failures | Signature HMAC webhooks Stripe + idempotence | `StripeWebhookServiceTest` |
| A09 Logging Failures | `AuditLog` + sanitisation log-forging | `ClientLogController` |

---

## 6. Journalisation et supervision

| Type | Mécanisme | Portée |
|---|---|---|
| **Audit métier/sécurité** | `AuditLog` (entité immuable) | login, changement de rôle, suppression, RGPD, redistribution |
| **Journalisation applicative** | Slf4j → OpenTelemetry → SigNoz | erreurs serveur + erreurs client (`ClientLogController`) |
| **Métriques** | Prometheus (`http_server_requests_seconds`) | latence, débit, taux d'erreur |
| **Anti log-forging** | Sanitisation `\n`/`\r` sur les entrées journalisées | `ClientLogController.sanitize()` |

---

## 7. Rôles et responsabilités

> Projet réalisé en solo (contexte pédagogique). Les rôles ci-dessous décrivent les
> **fonctions** assumées, transposables à une équipe.

| Fonction | Responsabilité SSI |
|---|---|
| **Responsable produit / RSSI** (Pierre MICHEL) | Définit la politique, arbitre les risques, valide les correctifs |
| **Développeur** | Applique les règles d'or, écrit les tests de sécurité, corrige les vulnérabilités |
| **Ops / DevOps** | Gère secrets, TLS, backups, scans DAST, monitoring |
| **Utilisateur (OWNER/ADMIN/MEMBER)** | Respecte le moindre privilège, protège ses accès |

---

## 8. Gestion des vulnérabilités

| Étape | Outil / procédure | Fréquence |
|---|---|---|
| SAST (code) | Semgrep (`--config auto` + `p/secrets`) | À chaque scan `security-scan.ps1` |
| SCA (dépendances) | Trivy filesystem | Idem |
| Scan images | Trivy image | Idem |
| DAST (app en marche) | OWASP ZAP baseline (`-Dast`) | Avant release |
| Triage | `09-audits/Problemes_Connus.md` (PC-xxx) → `13-roadmap/Roadmap_Backlog.md` (TF-xxx) | Continu |

**Résultat pentest 04/07/2026** : 0 vulnérabilité HIGH/critique ; backend clean ; 4 MEDIUM frontend
(CSP permissive en dev, tradeoff HMR assumé — durcissement par nonce en prod). Détail : [[Sécurité]] §4.

---

## 9. Application et révision

- **Non-régression sécurité** : les tests prioritaires (auth, RBAC, headers, chiffrement) doivent
  rester au vert — CI bloquante. Voir [[Politique_Tests]] §4.
- **Un bug de sécurité = un test** couvrant le scénario (règle de non-régression).
- **Révision** : la PSSI est revue à chaque évolution majeure de l'architecture de sécurité
  (ex. migration JWT Keycloak TF-SEC-009).

---

> 🔗 [[Sécurité]] (posture OWASP + pentest) — [[Auth_Autorisation]] (mécanismes détaillés) —
> [[Threat_Model_STRIDE]] (analyse de menaces) — [[Plan_Securisation_SSDLC]] (mise en œuvre) —
> [[STB]] §4 (exigences SEC) — [[Matrice_Tracabilite_Tests]] (couverture)
