---
id: cahier-test-recettes
title: Cahier de recettes — TaskForce V1
doc_type: recettes
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [recettes, tests, scenarios, acceptance, uc, qualite, memoire, rncp, soutenance]
---

# 📋 Cahier de recettes — TaskForce V1

> Scénarios de recette par cas d'usage, avec **critères d'acceptation** mesurables.
> Chaque scénario est tracé vers son test automatique quand il existe.
>
> **Légende statut** : ✅ Automatisé · 🟡 Partiel · ⬜ Manuel uniquement.

---

## UC-01 — Inscription + vérification OTP

**Préconditions** : aucun compte existant avec cet email.

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC01-01 | Inscription nominale (FREE) | Compte créé, OTP reçu, JWT retourné, redirection workspace | `AuthServiceTest`, `AuthControllerWebMvcTest`, E2E `auth.spec.ts` | ✅ |
| UC01-02 | OTP incorrect | `400 OTP_INVALID`, aucun compte créé | `OtpServiceTest` | ✅ |
| UC01-03 | OTP expiré (> 15 min) | `400 OTP_EXPIRED`, renvoi possible | `OtpServiceTest` | ✅ |
| UC01-04 | Email déjà utilisé | `409 CONFLICT`, message explicite | `AuthServiceTest` | ✅ |
| UC01-05 | Inscription PRO → Stripe Checkout | Redirect vers Stripe, session créée | `StripeServiceTest` | ✅ |
| UC01-06 | Renvoi OTP (`/resend-otp`) | Nouveau code envoyé, ancien invalidé | `OtpServiceTest` | ✅ |
| UC01-07 | Données invalides (email malformé, password court) | `400` avec détail de validation | `AuthControllerWebMvcTest` (`@Valid`) | ✅ |

---

## UC-02 — Login

**Préconditions** : compte actif, email vérifié.

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC02-01 | Login nominal | `200` + `{ accessToken, refreshToken, user }` | `AuthServiceTest`, `AuthControllerWebMvcTest` | ✅ |
| UC02-02 | Mauvais mot de passe | `401 UNAUTHORIZED` | `KeycloakAuthServiceTest` | ✅ |
| UC02-03 | Email inconnu | `401 UNAUTHORIZED` (pas de leak d'info) | `AuthServiceTest` | ✅ |
| UC02-04 | Token invalide sur endpoint protégé | `401` → client retente le refresh | `CoreControllersWebMvcTest` | ✅ |
| UC02-05 | Token expiré | `401` + séquence refresh → retry | `AuthServiceTest`, `client.test.ts` | ✅ |
| UC02-06 | Logout → refresh token révoqué | Refresh ultérieur retourne `401` | `AuthServiceTest` | ✅ |

---

## UC-03 — Gestion workspace (OWNER)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC03-01 | Création workspace | `201` + workspace en DB avec slug unique | `WorkspaceServiceIntegrationTest` | ✅ |
| UC03-02 | Modification nom/slug | `200`, slug unique validé | `WorkspaceServiceIntegrationTest` | ✅ |
| UC03-03 | Suppression workspace (OWNER) | `200`, workspace + données supprimés | `WorkspaceServiceIntegrationTest` | ✅ |
| UC03-04 | Tentative suppression par ADMIN | `403 FORBIDDEN` | `CoreControllersWebMvcTest` | ✅ |
| UC03-05 | Slug dupliqué | `409 CONFLICT` | `WorkspaceServiceIntegrationTest` | ✅ |

---

## UC-04 — Gestion membres & invitations (ADMIN+)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC04-01 | Invitation nominale (email + rôle) | Email envoyé, invitation en `PENDING` | `WorkspaceInvitationServiceIntegrationTest` | ✅ |
| UC04-02 | Acceptation invitation (token valide) | Membre ajouté, invitation `ACCEPTED` | `WorkspaceInvitationServiceIntegrationTest` | ✅ |
| UC04-03 | Invitation expirée | `400` token expiré | `WorkspaceInvitationServiceIntegrationTest` | ✅ |
| UC04-04 | Révocation invitation | Invitation `REVOKED`, token invalide | `WorkspaceInvitationServiceIntegrationTest` | ✅ |
| UC04-05 | Changement de rôle MEMBER → ADMIN | `200`, rôle mis à jour | `WorkspaceServiceIntegrationTest` | ✅ |
| UC04-06 | Rétrogradation impossible (OWNER → MEMBER par ADMIN) | `403` | `AuthorizationServiceTest` | ✅ |
| UC04-07 | Invitation par MEMBER | `403 FORBIDDEN` | `CoreControllersWebMvcTest` | ✅ |

---

## UC-05 — Gestion projets (ADMIN+)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC05-01 | Création projet | `201`, projet en DB, créateur = MANAGER | `ProjectServiceIntegrationTest` | ✅ |
| UC05-02 | Modification projet | `200`, champs mis à jour | `ProjectServiceIntegrationTest` | ✅ |
| UC05-03 | Suppression projet + issues en cascade | `200`, issues supprimées (FK cascade) | `ProjectServiceIntegrationTest` | ✅ |
| UC05-04 | Ajout/retrait de membre de projet | `200`, `ProjectMember` créé/supprimé | `ProjectServiceIntegrationTest` | ✅ |
| UC05-05 | Création par MEMBER | `403` | `ProjectControllerWebMvcTest` | ✅ |
| UC05-06 | Accès projet hors workspace | `403` (workspace boundary) | `AuthorizationServiceTest` | ✅ |

---

## UC-06 — Issues — CRUD + statuts + relations

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC06-01 | Création issue | `201`, issue en DB, activité tracée | `IssueServiceIntegrationTest` | ✅ |
| UC06-02 | Modification (titre, statut, priorité, assigné) | `200`, `IssueActivity` créée | `IssueServiceIntegrationTest` | ✅ |
| UC06-03 | Suppression issue | `200`, commentaires cascadés | `IssueServiceIntegrationTest` | ✅ |
| UC06-04 | Changement statut libre (board) | Tout statut accessible depuis tout statut | `IssueServiceIntegrationTest` | ✅ |
| UC06-05 | Ajout commentaire | `201`, commentaire en DB | `IssueServiceIntegrationTest` | ✅ |
| UC06-06 | Archivage / désarchivage | `200`, flag `archived` mis à jour | `IssueRepositoryIntegrationTest` | ✅ |
| UC06-07 | Pagination infinie (backlog) | `GET /paged?page=0&size=25` retourne page | `IssueControllerWebMvcTest` | ✅ |
| UC06-08 | Relation "bloque" / "est bloqué par" | Relation créée dans les 2 sens | `IssueServiceIntegrationTest` | ✅ |
| UC06-09 | Accès issue hors projet | `403` | `AuthorizationServiceTest` | ✅ |

---

## UC-07 — Smart-assign (LLM Groq)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC07-01 | Smart-assign nominal | Top-3 assignataires avec score + justification | `SmartAssignServiceTest` | ✅ |
| UC07-02 | Mode dégradé (Groq indisponible) | Scoring local seul retourné, pas d'erreur 500 | `GroqServiceContractTest` | ✅ |
| UC07-03 | Clé Groq absente | `SmartAssignService` retourne scoring local | `GroqServiceTest` | ✅ |
| UC07-04 | Bulk smart-assign (multi-issues) | `POST /smart-assign/bulk` applique les suggestions | `SmartAssignServiceTest` | ✅ |
| UC07-05 | Preview redistribution globale | Dry-run sans persistance, résultat cohérent | `RedistributionServiceTest`, E2E `redistribution.spec.ts` | ✅ |
| UC07-06 | Apply redistribution après preview | Issues réassignées en DB | `RedistributionServiceTest` | ✅ |

---

## UC-08 — Cycles (sprints)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC08-01 | Création cycle | `201`, statut `DRAFT` | `CycleServiceIntegrationTest` | ✅ |
| UC08-02 | Activation cycle (`DRAFT → ACTIVE`) | `200`, `started_at` renseigné | `CycleServiceIntegrationTest` | ✅ |
| UC08-03 | Clôture cycle (`ACTIVE → COMPLETED`) | `200`, `ended_at` renseigné | `CycleServiceIntegrationTest` | ✅ |
| UC08-04 | Transition invalide (`COMPLETED → ACTIVE`) | `400` | `CycleServiceIntegrationTest` | ✅ |
| UC08-05 | Ajout / retrait issue dans un cycle | `200`, `CycleIssue` créé/supprimé | `CycleServiceIntegrationTest` | ✅ |
| UC08-06 | Création par MEMBER | `403` | — | 🟡 |

---

## UC-09 — Chat (canaux + messages)

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC09-01 | Envoi message REST | `201`, message en DB | `ChatServiceIntegrationTest` | ✅ |
| UC09-02 | Réception temps réel STOMP | Message reçu via `use-stomp` sans rechargement | E2E (manuel) | ⬜ |
| UC09-03 | Auth STOMP — token invalide | Connexion STOMP rejetée | `StompAuthInterceptorTest` | ✅ |
| UC09-04 | Création canal | `201`, canal en DB | `ChannelControllerWebMvcTest` | ✅ |
| UC09-05 | Modification / suppression message | `200` / `200` | `ChatServiceIntegrationTest` | ✅ |

---

## UC-10 — Pages wiki

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC10-01 | Création page | `201`, page en DB | `PageServiceIntegrationTest` | ✅ |
| UC10-02 | Modification contenu Markdown | `200`, contenu mis à jour | `PageServiceIntegrationTest` | ✅ |
| UC10-03 | Suppression page | `200`, page supprimée | `PageServiceIntegrationTest` | ✅ |
| UC10-04 | Accès hors projet | `403` | `MiscControllersWebMvcTest` | ✅ |

---

## UC-11 — Abonnement Stripe

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC11-01 | Checkout.session.completed | `PlanStatus → ACTIVE`, subscription en DB | `StripeWebhookServiceTest` | ✅ |
| UC11-02 | invoice.payment_succeeded | Historique enregistré | `StripeWebhookServiceTest` | ✅ |
| UC11-03 | invoice.payment_failed | `PlanStatus → PAST_DUE`, notification OWNER | `StripeWebhookServiceTest` | ✅ |
| UC11-04 | customer.subscription.deleted | `PlanStatus → CANCELLED`, workspace → FREE | `StripeWebhookServiceTest` | ✅ |
| UC11-05 | Signature Stripe invalide | `400`, événement rejeté | `PaymentAndDataControllersWebMvcTest` | ✅ |
| UC11-06 | Idempotence (événement dupliqué) | 2e traitement ignoré (stripe_event_id UNIQUE) | `StripeWebhookServiceTest` | ✅ |
| UC11-07 | Portail billing (OWNER) | URL session Stripe retournée | `StripeServiceTest` | ✅ |
| UC11-08 | Portail billing par ADMIN | `403` | `PaymentAndDataControllersWebMvcTest` | ✅ |

---

## UC-12 — Export RGPD

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| UC12-01 | Export données utilisateur | JSON avec toutes les données personnelles, téléchargeable | `GdprServiceIntegrationTest` | ✅ |
| UC12-02 | Export en lecture seule (`@Transactional(readOnly)`) | Aucun INSERT parasite (correction PC-017) | `GdprServiceIntegrationTest` | ✅ |
| UC12-03 | Suppression de compte (droit à l'oubli) | Données anonymisées, compte inaccessible | `GdprServiceIntegrationTest` | ✅ |
| UC12-04 | Export par autre utilisateur | `403` | `PaymentAndDataControllersWebMvcTest` | ✅ |

---

## Cas transverses — Sécurité

| ID | Scénario | Critère d'acceptation | Test automatique | Statut |
|---|---|---|---|:---:|
| SEC-01 | En-têtes OWASP sur toutes les routes | `HSTS`, `X-Frame-Options: DENY`, `CSP`, `nosniff`, `Referrer-Policy`, `Permissions-Policy` | `SecurityHeadersWebMvcTest` | ✅ |
| SEC-02 | IDOR — accès issue hors workspace | `403` même si ID devinable | `AuthorizationServiceTest` | ✅ |
| SEC-03 | Rate limiting auth (`/api/auth/login`) | `429` après N tentatives rapides | `RateLimitFilterTest` | ✅ |
| SEC-04 | Chiffrement donnée sensible (`EncryptedStringConverter`) | Valeur chiffrée en DB, décryptée à la lecture | `EncryptedStringConverterTest` | ✅ |
| SEC-05 | JWT tampered (signature invalide) | `401` | `SecurityConfig` (décodeur RS256 rejette la signature), `CoreControllersWebMvcTest` | ✅ |
| SEC-06 | Accessibilité WCAG 2.1 AA | Audit axe-core sans violation critique | E2E `a11y.spec.ts` | ✅ |

---

## Résumé de couverture par UC

| UC | Scénarios totaux | Automatisés | Manuel | Couverture |
|---|:---:|:---:|:---:|:---:|
| UC-01 Inscription OTP | 7 | 7 | 0 | ✅ 100 % |
| UC-02 Login | 6 | 6 | 0 | ✅ 100 % |
| UC-03 Workspace | 5 | 5 | 0 | ✅ 100 % |
| UC-04 Membres/invitations | 7 | 7 | 0 | ✅ 100 % |
| UC-05 Projets | 6 | 6 | 0 | ✅ 100 % |
| UC-06 Issues | 9 | 9 | 0 | ✅ 100 % |
| UC-07 Smart-assign | 6 | 6 | 0 | ✅ 100 % |
| UC-08 Cycles | 6 | 5 | 1 | 🟡 83 % |
| UC-09 Chat | 5 | 4 | 1 | 🟡 80 % |
| UC-10 Pages | 4 | 4 | 0 | ✅ 100 % |
| UC-11 Stripe | 8 | 8 | 0 | ✅ 100 % |
| UC-12 RGPD | 4 | 4 | 0 | ✅ 100 % |
| Sécurité transverse | 6 | 6 | 0 | ✅ 100 % |
| **TOTAL** | **79** | **77** | **2** | **✅ 97 %** |

> 🔗 [[Politique_Tests]] — [[Matrice_Tracabilite_Tests]] — [[Tests]] — [[STB]] — [[Table_Reconciliation]]
