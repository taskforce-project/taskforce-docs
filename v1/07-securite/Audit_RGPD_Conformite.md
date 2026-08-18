---
id: audit-rgpd-conformite
title: Audit RGPD — Analyse de conformité (E9)
doc_type: rgpd
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [rgpd, audit, conformite, gdpr, e9, memoire, rncp, soutenance]
---

# ⚖️ Audit RGPD — Analyse de conformité (E9)

> Analyse de la conformité RGPD de TaskForce dans un cadre d'utilisation professionnel (B2B SaaS).
> Chaque point de conformité est ancré dans du code réel (services Java, migrations, composants
> landing). Les gaps sont tracés au [[Roadmap_Backlog]].
>
> **Cadre d'analyse** : RGPD (Règlement UE 2016/679) · Recommandations CNIL 2023
> **Périmètre** : TaskForce V1 — contexte pédagogique RNCP / proto-produit SaaS

---

## 1. Inventaire des traitements (synthèse)

> Détail complet → [[Registre_Traitements_RGPD]] (7 traitements documentés)

| # | Traitement | Base légale | Statut |
|---|---|---|---|
| T1 | Comptes utilisateurs | Art. 6.1.b | ✅ Conforme |
| T2 | Facturation / Stripe | Art. 6.1.b + 6.1.c | ✅ Conforme |
| T3 | Données métier (issues, pages, chat) | Art. 6.1.b | ✅ Conforme |
| T4 | Profils de compétences + embeddings | Art. 6.1.f | ✅ Conforme (facultatif) |
| T5 | Journal d'audit | Art. 6.1.c + 6.1.f | ✅ Conforme |
| T6 | Leads Enterprise | Art. 6.1.f | ✅ Conforme (chiffré) |
| T7 | Tokens OAuth intégrations | Art. 6.1.a | 🟡 Partiel (pas de révocation auto à l'effacement) |

---

## 2. Droits des personnes — état d'implémentation

### 2.1 Droits implémentés (Art. 15–21)

| Droit | Article | Mécanisme | Statut | Preuve code |
|---|---|---|---|---|
| **Accès** | Art. 15 | `GET /api/gdpr/export` → JSON | ✅ Implémenté | `GdprController`, `GdprService.exportMyData` |
| **Portabilité** | Art. 20 | Export JSON structuré | ✅ Implémenté | `GdprService.exportMyData` |
| **Rectification** | Art. 16 | `PUT /api/users/me` | ✅ Implémenté | `UserService` |
| **Effacement** | Art. 17 | `DELETE /api/gdpr/delete-account` | ✅ Implémenté | `GdprService.deleteMyAccount` |
| **Opposition** | Art. 21 | Profil compétences facultatif | ✅ Partiel | `MemberSkillProfileService` |
| **Limitation** | Art. 18 | Non implémenté — compte supprimé | ⬜ Gap | TF-RGPD-001 |

### 2.2 Processus d'effacement — analyse détaillée

Le `GdprService.deleteMyAccount()` exécute les étapes suivantes (code réel) :

```
1. email          → deleted-{id}@anonymized.invalid
2. display_name   → null
3. avatar_url     → null
4. stripe_customer_id  → null
5. stripe_subscription_id → null
6. plan_status    → CANCELED
7. is_active      → false
8. refresh_tokens → révoqués (jwtService.revokeAllUserTokens)
9. audit_log      → GDPR_DELETE enregistré
```

**Ce qui survit à l'effacement** (légitimement) :
- `audit_logs` : `actor_user_id` → `null` (ON DELETE SET NULL) — les actions passées restent traçables
- `subscription_history` : obligation légale comptable (10 ans)
- Contenu créé dans les workspaces : ownership transféré ou orphan (à définir)

**✅ Corrigé (05/07/2026)** : la suppression du compte Keycloak est désormais automatisée — `GdprService.deleteMyAccount` appelle `KeycloakService.deleteUser` **après commit** (tolérant à l'échec, journalisé pour rejeu). L'identité est effacée côté IdP et les sessions invalidées. TF-RGPD-007 clos. *(Auparavant : accès coupé via `isActive=false` mais identité conservée dans l'IdP.)*

---

## 3. Minimisation et limitation des données

### 3.1 Principe de minimisation (Art. 5.1.c) — vérifié

| Donnée | Nécessaire ? | Justification |
|---|---|---|
| `email` | Oui | Authentification + notifications |
| `display_name` | Oui | Collaboration |
| `avatar_url` | Oui | UX identification |
| `keycloak_id` | Oui | Lien IdP |
| `ip_address` (audit) | Oui | Sécurité / imputabilité |
| `embedding` (vector 384d) | Oui | Smart Assign — calcul local, non exposé |
| `stripe_customer_id` | Oui | Facturation |
| Cookies analytics/marketing | Non encore | ⚠️ Non implémentés côté app — politique landing à activer |

### 3.2 Chiffrement des données sensibles

Le chiffrement AES-256-GCM est appliqué sur les colonnes à risque (code `EncryptedStringConverter`) :

| Colonne | Table | Chiffré | Preuve |
|---|---|---|---|
| `message` | `enterprise_inquiries` | ✅ | `@Convert(converter = EncryptedStringConverter)` |
| `notes` | `enterprise_inquiries` | ✅ | idem |
| `access_token` | `integrations` | ❌ Pas chiffré | Gap TF-SEC-008 (en clair dans la DB) |

---

## 4. Mesures techniques et organisationnelles (Art. 25 et 32)

### 4.1 Privacy by Design (Art. 25)

| Mesure | Statut | Preuve |
|---|---|---|
| Isolation multi-tenant par `workspace_id` | ✅ | `WorkspaceAccessInterceptor` |
| RBAC (OWNER/ADMIN/MEMBER) | ✅ | `AuthorizationService`, `WorkspaceRole` |
| Principe de moindre privilège | ✅ | `requireManager`, `assertIsOwner` |
| Anonymisation à la suppression | ✅ | `GdprService.deleteMyAccount` |
| Données minimales par défaut | ✅ | Profil compétences optionnel |

### 4.2 Sécurité (Art. 32)

| Mesure | Statut | Preuve |
|---|---|---|
| Chiffrement TLS en transit | ✅ | Nginx + TLS dans `docker-compose.prod.yml` |
| JWT RS256 (Keycloak) + révocation de session | ✅ | `SecurityConfig`, `KeycloakService.logoutUser` |
| Rate limiting | ✅ | `RateLimitFilter` (Bucket4j) 10–200 req/min |
| 6 headers sécurité OWASP | ✅ | `applySecurityHeaders()` — CSP, HSTS, etc. |
| Audit log immuable | ✅ | Table `audit_logs` — pas d'UPDATE/DELETE via API |
| OTP à l'inscription | ✅ | `OtpVerificationService` — 15 min TTL, 3 essais |
| Protection log-forging | ✅ | `ClientLogController.sanitize()` |
| Chiffrement AES-256-GCM (PII libres) | ✅ | `EncryptedStringConverter` |

---

## 5. Sous-traitants et transferts hors UE (Art. 28 et 46)

> Détail complet → [[Registre_Traitements_RGPD]] §Sous-traitants

| Sous-traitant | Pays | Risque RGPD | Mitigation |
|---|---|---|---|
| Stripe | USA | Moyen (données paiement) | DPA Stripe (SCCs) |
| Groq *(optionnel)* | USA | Faible — **uniquement si le provider Groq est activé** (`GROQ_API_KEY`) ; contexte tâche, pas PII directes ; **aucun par défaut (IA locale Ollama)** | Si activé : DPA + CCT/DPF → TF-RGPD-008 |
| GitHub | USA | Faible (OAuth token workspace) | DPA GitHub (SCCs) |
| Slack | USA | Faible (OAuth token) | DPA Slack (SCCs) |
| Keycloak (auto-hébergé) | EU | Nul | Auto-hébergé |
| MinIO (auto-hébergé) | EU | Nul | Auto-hébergé |

---

## 6. Information et transparence (Art. 13/14)

| Obligation | Statut | Preuve |
|---|---|---|
| Politique de confidentialité | ✅ Page dédiée | `landing-page/src/pages/legal/privacy.astro` |
| CGU/CGV | ✅ Page dédiée | `landing-page/src/pages/legal/terms.astro` |
| Mentions légales | ⬜ Pas de page dédiée | Gap — mentions légales à ajouter dans la landing (nom, adresse, SIRET) |
| Politique cookies | ✅ Notice d'information présente | `cookie-banner.tsx` (05/07) — cookies strictement nécessaires uniquement, donc consentement non requis CNIL ; pas de traceurs → TF-RGPD-001 clos |
| Accès à l'export et à la suppression | ✅ | `GdprController` (`/api/gdpr/export`, `/api/gdpr/delete-account`) |

---

## 7. Registre et documentation (Art. 30)

| Obligation | Statut |
|---|---|
| Registre des traitements | ✅ [[Registre_Traitements_RGPD]] (ce dossier, Art. 30) |
| Traçabilité des accès aux données | ✅ `audit_logs` (GDPR_EXPORT, GDPR_DELETE) |
| Notification violations (Art. 33) | ⬜ Procédure à définir → TF-RGPD-005 |

---

## 8. Bilan de conformité et plan d'action

### 8.1 Conformité actuelle

| Axe | Conforme | Partiel | Gap |
|---|---|---|---|
| Droits des personnes | 5/6 | — | Art. 18 (limitation) |
| Minimisation | ✅ | — | — |
| Sécurité technique | ✅ | — | `integrations.access_token` non chiffré |
| Sous-traitants | 4/6 | Groq DPA (si provider activé) | — |
| Transparence | 2/4 | Cookies | Mentions légales, bannière |
| Documentation Art. 30 | ✅ | — | — |

**Taux de conformité estimé : ~75 %** pour un proto-produit pédagogique.

### 8.2 Items backlog RGPD

| ID | Priorité | Description |
|---|---|---|
| TF-RGPD-001 | P2 | Bannière cookies interactive (CNIL) |
| TF-RGPD-004 | P3 | Double opt-in sur les traitements collectant des données personnelles |
| TF-RGPD-005 | P2 | Mentions légales dédiées (LEN Art. 6) + corriger sous-traitants `constants_en.ts` |
| TF-RGPD-007 | P2 | Suppression automatique compte Keycloak à l'effacement |
| TF-RGPD-008 | P2 | DPA formel + CCT/DPF avec Groq, Inc. — **applicable seulement si le provider Groq est activé** (`GROQ_API_KEY`) ; sans objet tant que l'IA tourne en local (Ollama, défaut) |
| TF-RGPD-009 | P2 | Procédure notification violations (Art. 33) — 72h CNIL |

---

## 9. Évaluation RNCP — compétences démontrées

| Compétence | Preuve dans TaskForce |
|---|---|
| Identifier les obligations légales d'un traitement | 7 traitements analysés, base légale RGPD identifiée pour chacun |
| Implémenter les droits des personnes | `GdprService` : export + anonymisation + audit |
| Appliquer Privacy by Design | Isolation `workspace_id`, RBAC, chiffrement PII, OTP |
| Documenter (Art. 30) | [[Registre_Traitements_RGPD]] complet |
| Identifier et tracer les gaps | 6 items TF-RGPD-001→006 backlog |

---

> 🔗 [[Registre_Traitements_RGPD]] — [[PSSI]] §4 — [[Auth_Autorisation]] —
> [[Threat_Model_STRIDE]] (I3/I5 — PII non chiffrées) — [[Roadmap_Backlog]] (TF-RGPD-001→006)
