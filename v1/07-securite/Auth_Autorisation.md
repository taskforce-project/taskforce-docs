---
id: auth-autorisation
title: Authentification & autorisation — TaskForce V1
doc_type: securite
statut: valide
version: 1.1
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [auth, oidc, keycloak, rs256, jwt, rbac, securite, spring-security, memoire, rncp, soutenance]
---

# 🔐 Authentification & autorisation — TaskForce V1

> Documentation du mécanisme d'authentification (**tokens OIDC RS256 émis par Keycloak**)
> et du contrôle d'accès (RBAC à 3 niveaux). Tout est dérivé du code réel.
>
> **▶ v1.1 (05/07/2026)** — Ce document reflète la migration **[ADR-011]** : l'émission des JWT
> a été déléguée à Keycloak (RS256), le `JwtService` HS512 custom a été supprimé. Voir §2.
>
> **Fichiers de référence** :
> - `shared/security/SecurityConfig.java` (décodeur RS256 + chaînes de filtres)
> - `core/service/KeycloakAuthService.java` (flux OIDC : login ROPC / refresh / logout)
> - `core/service/KeycloakService.java` (Admin REST API : création, vérif email, suppression)
> - `core/service/AuthService.java` (orchestration)
> - `shared/security/JwtIdentityResolver.java` (résolution de l'utilisateur depuis le token)
> - `core/service/AuthorizationService.java` (RBAC)

---

## 1. Vue d'ensemble

```
┌─────────────────────────────────────────────────────────────────┐
│                     Flux d'authentification                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Inscription (3 étapes)                                          │
│  ─────────────────────                                           │
│  1. POST /api/auth/register  ──▶ KeycloakService.createUser()    │
│                              ──▶ OtpVerification (DB) + email OTP │
│  2. POST /api/auth/verify-otp ──▶ OTP valide ? ──▶ user activé   │
│  3. Compte prêt ──▶ PAS d'auto-login (Keycloak exige le mot de   │
│                     passe) ──▶ le front redirige vers /auth/login │
│                                                                  │
│  Login                                                           │
│  ──────                                                          │
│  POST /api/auth/login ──▶ AuthService.login()                    │
│    ──▶ KeycloakAuthService.authenticate()  (grant ROPC)          │
│    ──▶ Keycloak émet { access_token (RS256), refresh_token }     │
│    ──▶ { accessToken, refreshToken, user }                       │
│                                                                  │
│  Requête protégée                                                │
│  ─────────────────                                               │
│  Authorization: Bearer <access_token Keycloak>                   │
│    ──▶ SecurityConfig (NimbusJwtDecoder RS256, JWK Keycloak)     │
│    ──▶ signature + issuer valides ? ──▶ JwtIdentityResolver      │
│    ──▶ email ──▶ User (DB) ──▶ AuthorizationService (RBAC)        │
└─────────────────────────────────────────────────────────────────┘
```

> ✅ **PC-019 / TF-SEC-009 résolus** ([ADR-011], 05/07/2026) : les tokens sont désormais émis et
> signés par **Keycloak (RS256, clé asymétrique)**. Le backend n'émet plus aucun token et agit en
> pur **Resource Server**. Bénéfices : révocation de session native (`users().logout()`), refresh
> OIDC natif (rotation gérée par l'IdP), rotation automatique des clés (JWK), plus de secret
> symétrique partagé. La table `refresh_tokens` subsiste mais **n'est plus utilisée**.

---

## 2. Architecture des tokens (OIDC RS256)

### 2.1 Émission — par Keycloak (grant ROPC)

Le backend **ne signe plus aucun token**. Au login, il délègue à Keycloak via le
*Resource Owner Password Credentials Grant* (formulaire de connexion custom, pas de redirection) :

```java
// KeycloakAuthService.authenticate() — POST {realm}/protocol/openid-connect/token
params.add("grant_type", "password");
params.add("username", email);
params.add("password", password);
params.add("client_id", clientId);
params.add("client_secret", clientSecret);
// ← Keycloak renvoie { access_token (RS256), refresh_token, expires_in, ... }
```

`AuthService.login()` renvoie directement ces tokens Keycloak (enveloppés dans `AuthResponse`
avec le profil DB). **Preuve** : `AuthService.buildAuthResponse()`.

### 2.2 Validation — Resource Server RS256

```java
// SecurityConfig.jwtDecoder() — shared/security/SecurityConfig.java
String issuer   = keycloakUrl + "/realms/" + keycloakRealm;
String jwkSetUri = issuer + "/protocol/openid-connect/certs";

NimbusJwtDecoder decoder = NimbusJwtDecoder.withJwkSetUri(jwkSetUri).build();
decoder.setJwtValidator(JwtValidators.createDefaultWithIssuer(issuer)); // + exp, nbf
return decoder;
```

**Algorithme** : RS256 (signature asymétrique ; la clé privée ne quitte jamais Keycloak).
**Vérifications** : signature via le JWK Set public de Keycloak + `issuer` + expiration.
Aucun secret partagé côté backend.

### 2.3 Claims exploités & résolution d'identité

Le token Keycloak porte les claims OIDC standards. La correspondance vers l'utilisateur local se
fait par **email** (jamais par un claim `userId` custom), via `JwtIdentityResolver` :

| Claim (Keycloak) | Usage TaskForce |
|---|---|
| `sub` | UUID Keycloak (fallback identité) |
| `email` / `preferred_username` | Résolution `User` en base (`findByEmail`) |
| `given_name` / `family_name` | Affichage profil |
| `iss` | Validé (défense contre un token d'un autre realm) |
| `exp` / `iat` | Durée de vie (gérée par Keycloak) |

```java
// JwtIdentityResolver.resolveEmail(Jwt) — utilisé par les ~21 contrôleurs
return firstNonBlank(jwt.getClaimAsString("preferred_username"),
                     jwt.getClaimAsString("email"), jwt.getSubject());
```

> **Conséquence clé de la migration** : comme la résolution passe par `email` (présent dans le
> token Keycloak), **aucun contrôleur n'a eu besoin d'être modifié**.

### 2.4 Refresh & logout — natifs OIDC

| Opération | Mécanisme |
|---|---|
| Refresh | `KeycloakAuthService.refreshToken()` → `grant_type=refresh_token` (rotation gérée par l'IdP) |
| Logout | `KeycloakService.logoutUser()` → `users().logout()` (invalide **toutes** les sessions) |

Plus de table `refresh_tokens` custom, plus de rotation maison. Le client Axios (`client.ts`)
gère la séquence `401 → POST /api/auth/refresh-token → retry`.

---

## 3. Rôle de Keycloak

Keycloak est à la fois **référentiel d'identité** (Admin REST API) **et émetteur des tokens** (OIDC) :

```java
// KeycloakService.java — Admin REST API
createUser(email, password, firstName, lastName)  // POST /admin/.../users
verifyEmail(keycloakId)                            // marque email_verified
deleteUser(keycloakId)                             // effacement RGPD (TF-RGPD-007)
logoutUser(keycloakId)                             // révocation de session
```

| Responsabilité | Qui la prend |
|---|---|
| Création de compte | `KeycloakService.createUser()` (Admin REST) |
| Vérification email | `KeycloakService.verifyEmail()` |
| Validation credentials au login | `KeycloakAuthService.authenticate()` (ROPC) |
| **Émission & signature des tokens** | **Keycloak (RS256)** |
| Refresh / logout | `KeycloakAuthService.refreshToken()` / `KeycloakService.logoutUser()` |
| Effacement identité (RGPD) | `KeycloakService.deleteUser()` |

---

## 4. Chaînes de sécurité Spring

`SecurityConfig` définit les `SecurityFilterChain`, conditionnées par `keycloak.enabled` :
un mode **dev sans OAuth** (`permitAll`) et le mode **Keycloak** (défaut) avec chaînes publique + protégée.

### Chaîne publique (`@Order(1)`)

```java
// PUBLIC_MATCHERS : /api/auth/**, /api/stripe/**, /api/sales/**, /ws/**, /actuator/**, ...
.securityMatcher(PUBLIC_MATCHERS)
.authorizeHttpRequests(authz -> authz.anyRequest().permitAll())
.csrf(csrf -> csrf.disable());
```

### Chaîne protégée (`@Order(2)`, toutes les autres routes)

```java
.authorizeHttpRequests(authz -> authz.anyRequest().authenticated())
.oauth2ResourceServer(oauth2 -> oauth2.jwt(jwt -> jwt.decoder(jwtDecoder()))) // RS256 Keycloak
.sessionManagement(s -> s.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
.csrf(csrf -> csrf.disable());
```

### En-têtes de sécurité (toutes chaînes)

```
HSTS            maxAge=31_536_000s, includeSubDomains, preload
X-Frame-Options DENY
X-Content-Type-Options nosniff
CSP             default-src 'none'; frame-ancestors 'none'; form-action 'none'
Referrer-Policy strict-origin-when-cross-origin
Permissions-Policy camera=(), microphone=(), geolocation=(), payment=(), usb=(), ...
```

---

## 5. RBAC — Contrôle d'accès par rôle

### 5.1 Hiérarchie des rôles

```java
public enum WorkspaceRole { OWNER, ADMIN, MEMBER }  // OWNER ⊃ ADMIN ⊃ MEMBER
```

### 5.2 Implémentation — AuthorizationService

**Signatures réelles** (`core/service/AuthorizationService.java`) — chaque méthode prend
l'**identifiant de l'appelant en second paramètre** : le service ne lit jamais le contexte de sécurité
lui-même, il reçoit l'identité de l'appelant. C'est ce qui rend ces gardes testables unitairement.

```java
public WorkspaceMember requireMember(Long workspaceId, Long userId);                   // sinon 403
public WorkspaceMember requireRole(Long workspaceId, Long userId, WorkspaceRole... r); // sinon 403
public WorkspaceMember requireManager(Long workspaceId, Long userId);                  // = requireRole(OWNER, ADMIN)
public boolean         isMember(Long workspaceId, Long userId);                        // prédicat, ne jette pas
```

⚠️ **`assertIsOwner` n'appartient pas à ce service.** C'est une méthode **privée** de
`WorkspaceService`, appelée à exactement **deux** endroits (`WorkspaceService:362` et `:394`).
Recensement vérifié le 24/07/2026 : il n'existe aucun autre appel dans le dépôt.

### 5.3 Matrice rôles × actions

> **▶ Corrigée le 24/07/2026.** La version précédente comportait **quatre erreurs**, toutes dans le sens
> restrictif : elle annonçait des verrous qui n'existent pas. Une matrice d'habilitations trop sévère est
> aussi trompeuse qu'une matrice trop permissive — elle donne l'illusion d'un contrôle qui n'est pas là.

| Action | MEMBER | ADMIN | OWNER | Garde réelle |
|---|:---:|:---:|:---:|---|
| Lire issues / projets / **pages / cycles** | ⚠️ | ✅ | ✅ | `ProjectVisibilityGuard.assertCanView` — **pas le rôle workspace** (cf. §5.5) |
| Créer / modifier des issues | ⚠️ | ✅ | ✅ | `assertCanWrite` — **refusé au `VIEWER` du projet** (cf. §5.5) |
| **Créer un projet** | **✅** | ✅ | ✅ | `resolveWorkspaceAndAssertMember` — **simple appartenance** |
| Inviter des membres | ❌ | ✅ | ✅ | `requireManager` |
| **Changer le rôle d'un membre** | ❌ | **❌** | ✅ | `assertIsOwner` (`WorkspaceService:362`) |
| Configurer les intégrations | ❌ | ✅ | ✅ | `IntegrationController.requireManager` |
| **Modifier les paramètres workspace** | ❌ | **✅** | ✅ | `assertCanManage` = « **tout sauf MEMBER** » (`WorkspaceService:490`) |
| Consulter le journal d'audit | ❌ | ✅ | ✅ | `WorkspaceService:253` |
| Supprimer le workspace | ❌ | ❌ | ✅ | `assertIsOwner` (`WorkspaceService:394`) |
| Exporter ses données RGPD | ✅ | ✅ | ✅ | portée **self** |
| **Gérer son abonnement Stripe** | — | — | — | **hors axe workspace** (cf. §5.6) |

**Les quatre corrections, et ce qu'elles changent :**

1. **Créer un projet n'est pas réservé aux gestionnaires.** `ProjectService.createProject` n'exige que
   l'appartenance au workspace. C'est cohérent avec le modèle « dépôt » retenu (§5.5), mais il fallait
   le dire : la matrice affirmait l'inverse.
2. **Modifier les paramètres du workspace n'est pas réservé à l'OWNER.** `assertCanManage` rejette le
   rôle `MEMBER` et laisse donc passer `ADMIN`.
3. **« Gérer les membres » confondait deux droits distincts.** Inviter relève de `requireManager` ;
   **changer un rôle** est l'une des deux seules actions strictement OWNER. Un ADMIN ne peut pas se
   promouvoir, ce qui est précisément l'intérêt de la distinction.
4. **Le portail de facturation n'est pas gardé par un rôle** — voir §5.6, la raison est structurelle.

### 5.4 Rôle projet (`ProjectRole`)

> **▶ Corrigé le 24/07/2026.** La version précédente décrivait deux rôles, `MANAGER` et `MEMBER`.
> **`MANAGER` n'existe pas** dans l'enum, et le troisième rôle — `VIEWER` — était absent alors qu'il
> porte la seule restriction d'écriture du modèle.

```java
public enum ProjectRole { LEAD, MEMBER, VIEWER }   // core/enums/ProjectRole.java
```

| Rôle | Droits | Effet |
|---|---|---|
| `LEAD` | Contribue **et** administre le projet | Peut archiver le projet (`assertCanManageProject`) |
| `MEMBER` | Contribue | Lecture et écriture |
| `VIEWER` | **Lecture seule** | `canWrite` renvoie faux, **même sur un projet public** |

Un OWNER/ADMIN du workspace a un accès complet à tous les projets, y compris privés.

### 5.5 Second axe — visibilité du projet (`ProjectVisibilityGuard`)

**C'est cette garde, et non le rôle workspace, qui décide de l'accès aux issues.** Elle croise la
visibilité du projet (public/privé) avec le rôle projet, selon le modèle « dépôt » de GitHub et Linear.

```java
// core/service/ProjectVisibilityGuard.java — source unique du contrôle d'accès au contenu projet
canView(project, userId)   // public OU membre du projet OU OWNER/ADMIN du workspace
canWrite(project, userId)  // OWNER/ADMIN partout ; sinon membre non-VIEWER ; sinon projet public
```

Cette garde n'est pas réservée aux issues : elle est consommée par `ProjectService`, `IssueService`,
`PageService` et `CycleService`. **Tout ce qui appartient à un projet passe par elle** — c'est le point
qui rend le modèle cohérent, et c'est aussi pourquoi la matrice du §5.3 ne peut pas répondre « ✅ » à
« lire une page » sans préciser de quel projet il s'agit.

**Trois propriétés de sécurité à retenir :**

1. **Un projet privé invisible renvoie `404`, jamais `403`.** Répondre « interdit » confirmerait
   l'existence du projet et de son nom. `assertCanWrite` appelle d'ailleurs `assertCanView` **en
   premier** : on ne discute jamais des droits d'écriture sur un objet dont l'appelant n'a pas le droit
   de connaître l'existence.
2. **`VIEWER` reste en lecture seule même sur un projet public.** Un rôle explicite l'emporte sur
   l'ouverture du projet.
3. **Un non-membre peut contribuer à un projet public.** L'absence de rôle n'est pas un refus : dans ce
   modèle, l'ouverture est le défaut et la restriction un acte délibéré.

Les vues agrégées (analytique, workflows) ne sont **pas masquées** aux non-gestionnaires : elles sont
restreintes par `viewableProjectIds`. Deux collaborateurs ouvrent donc la même page et y lisent des
chiffres différents, chacun réduit à son propre périmètre.

### 5.6 Facturation — hors de l'axe des rôles

Le portail Stripe n'a **aucune garde de rôle**, et ce n'est pas un oubli : **l'abonnement est porté par
le compte utilisateur, pas par le workspace** (`BillingController` → `subscriptionRepository.findByUserId`,
`user.getPlanType()`). Un utilisateur authentifié ne peut donc atteindre que **son propre** abonnement,
ce qui rend la question du rôle sans objet.

La tarification reste **par siège** : la quantité facturée est le nombre de membres distincts sur les
workspaces du compte. C'est un abonnement par compte, dont le volume est dérivé de l'usage des
workspaces — pas un abonnement de workspace.

> ⚠️ **Conséquence à assumer devant un jury** : la question « qui peut résilier l'abonnement ? » a pour
> réponse « le titulaire du compte », et non « le propriétaire du workspace ». Les deux coïncident dans
> l'usage nominal, puisque c'est le créateur du workspace qui souscrit.

---

## 6. Flux OTP — inscription et réinitialisation

**L'OTP n'intervient jamais au login.** Il sert à deux flux, pas un seul — l'enum `OtpType` en déclare
trois, dont un inutilisé :

| `OtpType` | Utilisé ? | Où |
|---|:--:|---|
| `EMAIL_VERIFICATION` | ✅ | Inscription et renvoi de code (`AuthService:135`, `:384`) |
| `PASSWORD_RESET` | ✅ | Mot de passe oublié (`AuthService:419`, vérifié en `:438`) |
| `TWO_FACTOR_AUTH` | ❌ | **Déclaré mais jamais généré** — aucune double authentification n'est implémentée |

> **▶ Corrigé le 24/07/2026.** Ce paragraphe affirmait « uniquement à l'inscription ». La
> réinitialisation de mot de passe manquait. Le point importe pour l'analyse de risque : c'est un second
> chemin par lequel un code à usage unique circule par courriel.
>
> ⚠️ **`TWO_FACTOR_AUTH` ne doit pas être présenté comme une fonctionnalité.** La valeur existe dans
> l'enum, rien ne la produit. Annoncer une double authentification serait une surpromesse démentie par
> une recherche de trois secondes dans le code. Le cycle de vie complet du code OTP est décrit dans
> [[Diagramme_Etats_UML]] §7.

```
1. POST /api/auth/register
   └─▶ KeycloakService.createUser() → keycloakId
   └─▶ OtpVerification { code, expiresAt: now+15min } + email OTP

2. POST /api/auth/verify-otp { email, code }
   └─▶ Vérifie code + TTL (15 min, 5 essais) ; sinon exception
   └─▶ KeycloakService.verifyEmail() + User.save() (DB) + workspace initial

3. Compte prêt — PAS de tokens émis ici
   └─▶ Keycloak ne peut signer un token sans mot de passe (absent à ce stade)
   └─▶ le front redirige vers /auth/login (cf. [ADR-011])
```

**Preuve** : `AuthService.verifyOtpAndCompleteRegistration()` (retourne `authData = null`) ·
migration `V6__otp_verifications.sql`.

---

## 7. StompAuthInterceptor — WebSocket

Les connexions WebSocket STOMP sont authentifiées à la commande `CONNECT` via le **même
`JwtDecoder` RS256** (injecté) — elles bénéficient donc automatiquement de la migration OIDC :

```java
// shared/config/StompAuthInterceptor.java
private final JwtDecoder jwtDecoder;   // = décodeur RS256 Keycloak
// ...
Jwt jwt = jwtDecoder.decode(authorization.substring(7)); // valide signature + issuer
// principal injecté dans la session STOMP ; sinon connexion rejetée
```

Un client STOMP sans token Keycloak valide est rejeté avant de pouvoir s'abonner à un topic.

---

## 8. Gestion des secrets

| Secret | Stockage | Variable d'env |
|---|---|---|
| Keycloak client secret | Variable d'env | `KEYCLOAK_CLIENT_SECRET` |
| Keycloak admin password | Variable d'env | `KEYCLOAK_ADMIN_PASSWORD` |
| Stripe secret key | Variable d'env | `STRIPE_SECRET_KEY` |
| Stripe webhook secret | Variable d'env | `STRIPE_WEBHOOK_SECRET` |
| DB password | Variable d'env | `POSTGRES_PASSWORD` |

> **▶ Depuis [ADR-011]** : plus de `JWT_SECRET` (le backend ne signe plus rien ; la validation
> repose sur la clé **publique** JWK de Keycloak). Aucun secret en dur dans le code
> (`application.yml` → `${VAR:default_dev_only}` ; les défauts ne servent qu'en dev local).

---

## 9. Pré-requis de déploiement (post-migration)

- Le realm Keycloak doit **inclure le claim `email`** dans l'access token (scope `email`, actif par
  défaut) — sinon `JwtIdentityResolver` échoue.
- Le client Keycloak doit autoriser le **grant `password`** (Direct Access Grants activé).
- `application-prod.yml` : `spring.security.oauth2.resourceserver.jwt.issuer-uri` / `jwk-set-uri`
  pointant sur le realm de prod.

---

> 🔗 Voir aussi : [[Sécurité]] — [[Spec_API_OpenAPI]] §1.2 — [[Journal_Decisions_ADR]] (ADR-003, **ADR-011**)
> — [[Diagrammes_Sequence_UML]] §1 (inscription OTP) §2 (login) — [[Threat_Model_STRIDE]] — [[PSSI]]

**Dernière mise à jour :** 05/07/2026 · **Version :** 1.1 (migration OIDC RS256) · **Projet :** Taskforce
