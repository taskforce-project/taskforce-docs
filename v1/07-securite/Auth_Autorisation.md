---
id: auth-autorisation
title: Authentification & autorisation — TaskForce V1
doc_type: securite
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [auth, jwt, keycloak, rbac, securite, hs512, spring-security, memoire, rncp, soutenance]
---

# 🔐 Authentification & autorisation — TaskForce V1

> Documentation du mécanisme d'authentification (JWT HS512 + Keycloak Admin API)
> et du contrôle d'accès (RBAC à 3 niveaux). Tout est dérivé du code réel.
>
> **Fichiers de référence** :
> - `shared/security/SecurityConfig.java`
> - `shared/security/JwtDecoderConfig.java`
> - `core/service/JwtService.java`
> - `core/service/KeycloakService.java`
> - `core/service/AuthService.java`
> - `core/service/AuthorizationService.java`

---

## 1. Vue d'ensemble

```
┌─────────────────────────────────────────────────────────────────┐
│                     Flux d'authentification                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Inscription (3 étapes)                                         │
│  ─────────────────────                                          │
│  1. POST /api/auth/register ──▶ OtpVerification (DB)           │
│                               ──▶ KeycloakService.createUser() │
│  2. POST /api/auth/verify-otp ──▶ OTP valide ?                  │
│  3. Keycloak user activé ──▶ JwtService.generateTokens()        │
│                           ──▶ accessToken (HS512) + refresh    │
│                                                                 │
│  Login                                                          │
│  ──────                                                         │
│  POST /api/auth/login ──▶ AuthService.login()                  │
│    ──▶ vérif email/password (Keycloak admin API)               │
│    ──▶ JwtService.generateTokens()                              │
│    ──▶ { accessToken, refreshToken, user }                     │
│                                                                 │
│  Requête protégée                                               │
│  ─────────────────                                              │
│  Authorization: Bearer <accessToken>                           │
│    ──▶ SecurityConfig (NimbusJwtDecoder HS512)                 │
│    ──▶ JWT valide ? ──▶ service ──▶ AuthorizationService       │
└─────────────────────────────────────────────────────────────────┘
```

> ⚠️ **Amélioration prévue (PC-019 / TF-SEC-009)** : faire émettre les JWT par Keycloak
> (Authorization Code / ROPC → RS256, JWK endpoint) plutôt que par `JwtService` maison.
> Bénéfices : révocation session réelle, refresh natif OIDC, rotation automatique des clés,
> suppression de la table `refresh_tokens` et du secret HS512 partagé.
> **Ce document sera mis à jour après le fix** — voir [[Roadmap_Backlog]] TF-SEC-009.

---

## 2. Architecture JWT

### 2.1 Génération du token

Le backend génère ses propres JWT via `JwtService` (`io.jsonwebtoken.Jwts`).
**Keycloak n'émet pas les tokens** — il est utilisé comme référentiel d'identité (Admin REST API).

```java
// JwtService.generateAccessToken() — core/service/JwtService.java
Map<String, Object> claims = new HashMap<>();
claims.put("userId",      user.getId());
claims.put("keycloakId",  user.getKeycloakId());
claims.put("email",       user.getEmail());
claims.put("firstName",   keycloakUser.getFirstName());
claims.put("lastName",    keycloakUser.getLastName());
claims.put("planType",    user.getPlanType().toString());

return Jwts.builder()
    .setClaims(claims)
    // ...
    .signWith(key, SignatureAlgorithm.HS512)
    .build();
```

**Claims du token** :

| Claim | Type | Description |
|---|---|---|
| `sub` | String | Identifiant Spring Security |
| `userId` | Long | ID interne en base (`users.id`) |
| `keycloakId` | String | UUID Keycloak de l'utilisateur |
| `email` | String | Email vérifié |
| `firstName` | String | Prénom (depuis Keycloak) |
| `lastName` | String | Nom (depuis Keycloak) |
| `planType` | String | `FREE` / `PRO` / `ENTERPRISE` |
| `iat` | Long | Émission (Unix timestamp) |
| `exp` | Long | Expiration |

### 2.2 Validation du token

```java
// SecurityConfig.java — shared/security/SecurityConfig.java
@Bean
public JwtDecoder jwtDecoder() {
    byte[] keyBytes = jwtSecret.getBytes(StandardCharsets.UTF_8);
    SecretKeySpec keySpec = new SecretKeySpec(keyBytes, "HmacSHA512");
    return NimbusJwtDecoder.withSecretKey(keySpec)
            .macAlgorithm(MacAlgorithm.HS512)
            .build();
}
```

**Algorithme** : HMAC-SHA512 (clé symétrique, partagée entre le service de génération et le décodeur).  
**Config** : `${jwt.secret}` (variable d'environnement, jamais en dur).

### 2.3 Durée de vie et refresh

| Token | Durée | Stockage |
|---|---|---|
| Access token | Court (≤ 15 min recommandé) | Memory / localStorage front |
| Refresh token | Long (7–30 j) | `refresh_tokens` table (DB) |

Le client Axios (`client.ts`) gère la séquence `401 → POST /api/auth/refresh-token → retry`.

> ⚠️ **Dette PC-004** : le frontend appelle `/api/auth/refresh` (absent), le backend mappe
> `/api/auth/refresh-token`. La séquence de refresh ne peut pas aboutir en l'état.

---

## 3. Rôle de Keycloak

Keycloak est utilisé comme **référentiel d'identité** (pas comme émetteur de tokens) :

```java
// KeycloakService.java — Keycloak Admin REST API
public String createUser(String email, String password,
                          String firstName, String lastName) {
    // POST /admin/realms/{realm}/users (Keycloak Admin API)
    // → retourne keycloakId (UUID)
}

public void verifyEmail(String keycloakId) {
    // PUT /admin/realms/{realm}/users/{id}/execute-actions-email
}
```

| Responsabilité | Qui la prend |
|---|---|
| Création de compte | `KeycloakService.createUser()` (via Admin REST) |
| Vérification email | `KeycloakService.verifyEmail()` |
| Récupération utilisateur | `KeycloakService.getUserById()` |
| Validation credentials au login | Auth Service via Admin API |
| **Émission des JWT** | **`JwtService.generateTokens()`** (backend) |

---

## 4. Chaînes de sécurité Spring

`SecurityConfig` définit **trois** `SecurityFilterChain` ordonnées (`@Order`) :

### Chaîne 1 — Routes WebSocket (ordre le plus haut)

```java
// Gère /ws/** et /ws-sockjs/** — pas d'auth HTTP requise
// L'auth STOMP est gérée par StompAuthInterceptor
.authorizeHttpRequests(authz -> authz.anyRequest().permitAll())
.csrf(csrf -> csrf.disable())
```

### Chaîne 2 — Routes publiques

```java
// Gère PUBLIC_MATCHERS : /api/auth/**, /api/stripe/**, /api/sales/**, etc.
.authorizeHttpRequests(authz -> authz.anyRequest().permitAll())
.csrf(csrf -> csrf.disable())
```

### Chaîne 3 — Routes protégées (toutes les autres)

```java
.authorizeHttpRequests(authz -> authz.anyRequest().authenticated())
.oauth2ResourceServer(oauth2 -> oauth2.jwt(jwt -> jwt.decoder(jwtDecoder())))
.sessionManagement(session -> session
    .sessionCreationPolicy(SessionCreationPolicy.STATELESS))
.csrf(csrf -> csrf.disable())
```

### En-têtes de sécurité (toutes chaînes)

```java
// applySecurityHeaders()
HSTS           maxAge=31_536_000s, includeSubDomains, preload
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
CSP            default-src 'none'; frame-ancestors 'none'; form-action 'none'
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), ...
```

---

## 5. RBAC — Contrôle d'accès par rôle

### 5.1 Hiérarchie des rôles

```java
// WorkspaceRole.java
public enum WorkspaceRole {
    OWNER,   // Accès total + billing + suppression workspace
    ADMIN,   // Gestion membres, projets, paramètres
    MEMBER   // Participation aux projets assignés
}
```

Hiérarchie implicite : `OWNER ⊃ ADMIN ⊃ MEMBER` (chaque niveau hérite des droits inférieurs).

### 5.2 Implémentation — AuthorizationService

```java
// AuthorizationService.java — core/service/AuthorizationService.java

// Vérifie que l'utilisateur est membre actif du workspace
public WorkspaceMember getMemberOrThrow(Long workspaceId) {
    return repository.findByWorkspaceIdAndUserId(workspaceId, currentUserId())
        .orElseThrow(() -> new ForbiddenException("Accès workspace refusé"));
}

// Vérifie rôle ADMIN ou OWNER
public void requireManager(Long workspaceId) {
    WorkspaceMember member = getMemberOrThrow(workspaceId);
    if (member.getRole() == WorkspaceRole.MEMBER) {
        throw new ForbiddenException("Action réservée aux admins et owners");
    }
}

// Vérifie rôle OWNER uniquement
public void assertIsOwner(Long workspaceId) {
    WorkspaceMember member = getMemberOrThrow(workspaceId);
    if (member.getRole() != WorkspaceRole.OWNER) {
        throw new ForbiddenException("Action réservée au propriétaire");
    }
}
```

### 5.3 Matrice rôles × actions

| Action | MEMBER | ADMIN | OWNER |
|---|:---:|:---:|:---:|
| Lire les issues / projets / pages | ✅ | ✅ | ✅ |
| Créer / modifier des issues | ✅ | ✅ | ✅ |
| Créer un projet | ❌ | ✅ | ✅ |
| Gérer les membres (inviter, rôles) | ❌ | ✅ | ✅ |
| Configurer les intégrations | ❌ | ✅ | ✅ |
| Modifier les paramètres workspace | ❌ | ❌ | ✅ |
| Accéder au portail billing Stripe | ❌ | ❌ | ✅ |
| Supprimer le workspace | ❌ | ❌ | ✅ |
| Exporter ses données RGPD | ✅ | ✅ | ✅ |
| Export RGPD bulk workspace | ❌ | ❌ | ✅ |

### 5.4 Rôle projet (`ProjectRole`)

En plus du rôle workspace, chaque `ProjectMember` peut avoir un rôle de projet :
`MANAGER` (peut modifier paramètres projet) ou `MEMBER` (participation uniquement).

```
Workspace MEMBER + Project MANAGER = peut gérer les issues et cycles du projet
Workspace ADMIN = accès gestionnaire sur tous les projets du workspace
```

---

## 6. Flux OTP — inscription

L'OTP est utilisé **uniquement à l'inscription** (pas au login).

```
1. POST /api/auth/register
   └─▶ Génère OtpVerification { code: "123456", expiresAt: now+15min }
   └─▶ Envoie email via SMTP/Mailtrap

2. POST /api/auth/verify-otp { email, code }
   └─▶ Vérifie code + TTL (15 min)
   └─▶ Si invalide : BusinessException(OTP_INVALID)
   └─▶ Si expiré  : BusinessException(OTP_EXPIRED)

3. POST /api/auth/complete-registration (appelé après OTP valide)
   └─▶ KeycloakService.createUser() → keycloakId
   └─▶ User.save() (DB)
   └─▶ JwtService.generateTokens()
   └─▶ { accessToken, refreshToken, user }
```

**Preuve** : `core/service/AuthService.verifyOtpAndCompleteRegistration()` ·
migration `V6__otp_verifications.sql` (table `otp_verifications` : `code`, `expires_at`).

---

## 7. StompAuthInterceptor — WebSocket

Les connexions WebSocket STOMP sont authentifiées via `StompAuthInterceptor` :

```java
// shared/config/StompAuthInterceptor.java
@Override
public Message<?> preSend(Message<?> message, MessageChannel channel) {
    if (CONNECT.equals(accessor.getCommand())) {
        String token = extractToken(accessor); // header "Authorization"
        Claims claims = jwtService.parseClaimsFromToken(token);
        // Injecte le principal dans la session STOMP
        accessor.setUser(new JwtPrincipal(claims));
    }
    return message;
}
```

Un client STOMP sans JWT valide est rejeté à la connexion (avant de pouvoir s'abonner à des topics).

---

## 8. Gestion des secrets

| Secret | Stockage | Variable d'env |
|---|---|---|
| Clé JWT | Variable d'env | `JWT_SECRET` |
| Keycloak admin password | Variable d'env | `KEYCLOAK_ADMIN_PASSWORD` |
| Stripe secret key | Variable d'env | `STRIPE_SECRET_KEY` |
| Stripe webhook secret | Variable d'env | `STRIPE_WEBHOOK_SECRET` |
| DB password | Variable d'env | `POSTGRES_PASSWORD` |

**Règle** : aucun secret en dur dans le code (`application.yml` → `${VAR:default_dev_only}`).
Les valeurs par défaut dans `application-dev.yml` ne sont utilisées qu'en développement local.

> 🔗 Voir aussi : [[Sécurité.md]] — [[Spec_API_OpenAPI]] §1.2 — [[ADR-003]] (Keycloak)
> [[Diagrammes_Sequence_UML]] §1 (inscription OTP) §2 (login)
