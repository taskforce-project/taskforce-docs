---
id: registre-traitements-rgpd
title: Registre des traitements de données personnelles — Art. 30 RGPD
doc_type: rgpd
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [rgpd, registre, traitements, donnees-personnelles, art30, conformite, memoire, rncp, soutenance]
---

# 📋 Registre des traitements de données personnelles — Article 30 RGPD

> Registre des activités de traitement, conformément à l'**Art. 30 du RGPD**.
> Toutes les données listées sont dérivées des migrations Flyway (V1–V56) et du code réel
> (`GdprService`, `UserRepository`, migrations DB). Rien n'est inventé.
>
> **Responsable du traitement** : Pierre MICHEL — pierre.michel.work@gmail.com  
> **Contexte** : projet pédagogique RNCP Metz Numeric School 2025-2026 (SaaS de gestion de projet)  
> **Base légale générale** : Exécution d'un contrat (Art. 6.1.b) · Intérêt légitime (Art. 6.1.f) · Obligation légale (Art. 6.1.c)

---

## Traitement n°1 — Gestion des comptes utilisateurs

| Champ | Valeur |
|---|---|
| **Finalité** | Création et gestion du compte, authentification, identification dans l'application |
| **Base légale** | Exécution du contrat (Art. 6.1.b) |
| **Catégories de personnes** | Utilisateurs inscrits (OWNER, ADMIN, MEMBER) |
| **Données collectées** | `email` · `display_name` · `avatar_url` · `keycloak_id` · `is_active` · `created_at` · `plan_type` |
| **Source** | Saisie directe à l'inscription + OTP (V6 `otp_verification`) |
| **Durée de conservation** | Durée de vie du compte · Anonymisation à la demande (`GdprService.deleteMyAccount`) |
| **Destinataires** | Keycloak (identité) · Backend Spring Boot (sessions) |
| **Transferts hors UE** | Keycloak auto-hébergé (pas de transfert) |
| **Mesures de sécurité** | Hash bcrypt Keycloak · JWT **RS256 (OIDC Keycloak)** · Rate limiting · OTP |
| **Preuve** | `V1__init_schema.sql` · `V2__auth_and_subscriptions.sql` · `GdprService` |

---

## Traitement n°2 — Facturation et abonnements

| Champ | Valeur |
|---|---|
| **Finalité** | Gestion des plans (FREE/PRO/Enterprise), facturation, historique des paiements |
| **Base légale** | Exécution du contrat (Art. 6.1.b) · Obligation légale comptable (Art. 6.1.c) |
| **Catégories de personnes** | Utilisateurs payants (PRO, Enterprise) |
| **Données collectées** | `stripe_customer_id` · `stripe_subscription_id` · `plan_type` · `plan_status` · historique (`amount_paid`, `currency`, `period_start/end`, `stripe_invoice_id`) |
| **Source** | Stripe webhooks (5 événements : checkout, invoice, subscription, cancel, trial) |
| **Durée de conservation** | Durée légale de conservation des pièces comptables (10 ans en France) |
| **Destinataires** | Stripe (processeur de paiement, UE/US, Privacy Shield / SCCs) |
| **Transferts hors UE** | Stripe Inc. (USA) — DPA Stripe couvre les transferts UE→US |
| **Mesures de sécurité** | Signature HMAC webhooks · Idempotence `stripe_event_id UNIQUE` · Pas de données de carte stockées localement |
| **Preuve** | `V2__auth_and_subscriptions.sql` · `V8, V36` · `StripeWebhookService` |

---

## Traitement n°3 — Données de travail collaboratif (contenu métier)

| Champ | Valeur |
|---|---|
| **Finalité** | Permettre la collaboration (gestion de projets, issues, pages, discussions, chat) |
| **Base légale** | Exécution du contrat (Art. 6.1.b) |
| **Catégories de personnes** | Membres des workspaces |
| **Données collectées** | Contenu des issues (titre, description, commentaires) · pages wiki · messages de discussion · messages de chat · pièces jointes (MinIO) · worklogs (temps saisi) |
| **Source** | Création directe par les utilisateurs |
| **Durée de conservation** | Durée de vie du workspace · Suppression en cascade à la fermeture du workspace (ON DELETE CASCADE) |
| **Destinataires** | Membres du même workspace (isolation multi-tenant garantie par `WorkspaceAccessInterceptor`) |
| **Transferts hors UE** | Aucun (données sur la VM/Render EU Frankfurt) |
| **Mesures de sécurité** | Isolation `workspace_id` · RBAC · TLS · Pas d'accès inter-workspace |
| **Preuve** | `V15__projects.sql` · `V16__issues.sql` · `V25__pages.sql` · `V27__discussions.sql` · `V28__chat.sql` · `V29__attachments.sql` · `V47__issue_worklogs.sql` |

---

## Traitement n°4 — Profils de compétences membres (Smart Assign)

| Champ | Valeur |
|---|---|
| **Finalité** | Automatisation de l'assignation des tâches (Smart Assign) — analyse des compétences déclarées et de la disponibilité |
| **Base légale** | Intérêt légitime (Art. 6.1.f) — optimisation de la gestion de projet |
| **Catégories de personnes** | Membres des workspaces avec profil renseigné |
| **Données collectées** | `skills_json` (compétences déclarées) · `seniority` · `capacity_hours_per_week` · `profile_text` · `growth_enabled` · `growth_target_skills` · `embedding` (vecteur pgvector 384d — représentation mathématique) |
| **Source** | Saisie directe + calcul automatique (`SmartAssignService`, `MemberSkillProfileService`) |
| **Durée de conservation** | Durée de vie du workspace ou du membership |
| **Destinataires** | Backend (calcul Smart Assign) · Groq API (LLM — données contextualisées, pas de PII directes) |
| **Transferts hors UE** | Groq Inc. (USA) — contexte de la tâche uniquement, pas de PII directes |
| **Mesures de sécurité** | Accès restreint aux membres du workspace · `embedding` non exposé en API |
| **Preuve** | `V33__member_skill_profiles.sql` · `V44__member_skill_capacity_seniority.sql` · `V46__member_growth_objectives.sql` |

---

## Traitement n°5 — Journal d'audit (traçabilité sécurité/RGPD)

| Champ | Valeur |
|---|---|
| **Finalité** | Traçabilité des actions sensibles (sécurité, conformité RGPD, imputabilité) |
| **Base légale** | Obligation légale / Intérêt légitime (Art. 6.1.c / 6.1.f) |
| **Catégories de personnes** | Tous les utilisateurs ayant effectué des actions auditées |
| **Données collectées** | `actor_user_id` · `action` · `entity_type/id` · `details` · `ip_address` · `created_at` |
| **Actions tracées** | login · changement de rôle · suppression · export RGPD (`GDPR_EXPORT`) · effacement (`GDPR_DELETE`) · redistribution |
| **Source** | Hooks applicatifs (`AuditService.record()`) |
| **Durée de conservation** | `ON DELETE SET NULL` (le log survit à l'anonymisation de l'utilisateur) — durée de conservation à définir en prod |
| **Destinataires** | Responsable du traitement (via `GET /api/audit`) · SigNoz (logs) |
| **Transferts hors UE** | Aucun |
| **Mesures de sécurité** | Table immuable (pas d'UPDATE/DELETE via l'API) · Accès restreint OWNER |
| **Preuve** | `V48__audit_log.sql` · `AuditService.java` |

---

## Traitement n°6 — Demandes de contact Enterprise (leads sales)

| Champ | Valeur |
|---|---|
| **Finalité** | Traitement des demandes de contact pour le plan Enterprise (prospection commerciale) |
| **Base légale** | Intérêt légitime (Art. 6.1.f) — suivi commercial |
| **Catégories de personnes** | Prospects ayant rempli le formulaire Enterprise |
| **Données collectées** | `full_name` · `email` · `team_size` · `message` (chiffré AES-256-GCM) · `status` · `notes` (chiffrées) · `contacted_at` · `converted_at` |
| **Source** | Formulaire de contact Enterprise (`/api/sales/inquiry`) |
| **Durée de conservation** | Durée de vie de la relation commerciale + délai légal |
| **Destinataires** | Équipe commerciale (accès `assigned_to`) |
| **Transferts hors UE** | Aucun |
| **Mesures de sécurité** | Chiffrement AES-256-GCM colonnes `message` + `notes` (`EncryptedStringConverter`) |
| **Preuve** | `V9__create_enterprise_inquiries_table.sql` · `V11__add_audit_columns_to_enterprise_inquiries.sql` · `EncryptedStringConverter` |

---

## Traitement n°7 — Tokens OAuth / intégrations (GitHub, Slack)

| Champ | Valeur |
|---|---|
| **Finalité** | Permettre les intégrations avec GitHub (liens PR/commits) et Slack (notifications) |
| **Base légale** | Exécution du contrat / Consentement (Art. 6.1.b / 6.1.a) |
| **Catégories de personnes** | Membres ADMIN/OWNER ayant activé une intégration |
| **Données collectées** | `access_token` (OAuth) · `meta` (login GitHub, team_id Slack) · `installed_by` |
| **Source** | Flux OAuth (GitHub/Slack callbacks) |
| **Durée de conservation** | Durée de vie de l'intégration (révocable) |
| **Destinataires** | GitHub API · Slack API (services tiers) |
| **Transferts hors UE** | GitHub Inc. (USA) · Slack Technologies (USA) — DPA respectifs |
| **Mesures de sécurité** | Token stocké en DB (chiffrement volume cible en prod) · Pas d'exposition API |
| **Preuve** | `V30__integrations.sql` · `GitHubIntegrationService` · `SlackIntegrationService` |

---

## Droits des personnes exercés via l'application

| Droit RGPD | Article | Implémentation | Preuve |
|---|---|---|---|
| **Portabilité** | Art. 20 | `GET /api/gdpr/export` → JSON (profil, memberships, skillProfiles, worklogs) | `GdprService.exportMyData` |
| **Effacement / oubli** | Art. 17 | `DELETE /api/gdpr/delete-account` → anonymisation + révocation tokens | `GdprService.deleteMyAccount` |
| **Accès** | Art. 15 | Export JSON = accès complet aux données | `GdprService.exportMyData` |
| **Rectification** | Art. 16 | Modification profil via `PUT /api/users/me` | `UserService` |
| **Opposition Smart Assign** | Art. 21 | Profil de compétences facultatif | `MemberSkillProfileService` |

**Données anonymisées à l'effacement** (code réel `GdprService.deleteMyAccount`) :
- `email` → `deleted-{id}@anonymized.invalid`
- `display_name` → `null`
- `avatar_url` → `null`
- `stripe_customer_id` → `null`
- `stripe_subscription_id` → `null`
- `plan_status` → `CANCELED`
- `is_active` → `false`
- Refresh tokens → révoqués (`jwtService.revokeAllUserTokens`)

> ⚠️ **Gap connu** : la suppression du compte Keycloak associé n'est pas encore automatisée
> (commentaire dans `GdprService.deleteMyAccount` — côté IdP, l'accès est déjà coupé via
> `isActive=false` + tokens révoqués). → [[Roadmap_Backlog]] TF-RGPD-003.

---

## Traitement n°8 — Assistance par modèle de langage (Cortex, spécifications, décisions)

| Champ | Valeur |
|---|---|
| **Finalité** | Génération de spécifications d'issue, briefs de décision, réponses de l'assistant, classement des candidats au smart-assign |
| **Base légale** | Exécution du contrat (Art. 6.1.b) — fonctionnalité du service souscrit |
| **Catégories de personnes** | Membres d'un workspace dont le contenu de travail est soumis au modèle |
| **Données transmises** | Titre et description d'issue, libellés, noms d'affichage des candidats, métriques de charge. **Pas de mot de passe, ni jeton, ni donnée de paiement** |
| **Source** | Contenu saisi par les utilisateurs dans l'application |
| **Durée de conservation** | **Aucune conservation par le modèle** : l'inférence est sans état, rien n'est réutilisé pour un entraînement |
| **Destinataires** | **Aucun tiers.** Le modèle (Qwen3 via Ollama) est **auto-hébergé** ; l'application ne parle qu'à `ai-service`, qui parle au modèle local |
| **Transferts hors UE** | **Aucun** |
| **Mesures de sécurité** | Passerelle interne unique (`AiGatewayClient` → `ai-service`), jamais d'appel direct depuis les services métier · quotas par compte (`AiMeter`) · dégradation en repli déterministe si le modèle est injoignable |
| **Preuve** | `LlmConfig` · `AiGatewayClient` · `ai-service/app/services/ollama_gateway.py` · `SmartAssignService` (repli `java-fallback`) |

> **Point notable pour la conformité.** Le choix d'un modèle auto-hébergé plutôt qu'une API tierce
> (OpenAI, Anthropic, Groq…) supprime tout transfert de contenu de travail hors de l'infrastructure.
> C'est l'argument le plus fort du registre : aucune donnée client ne quitte le périmètre maîtrisé
> pour alimenter un service d'IA externe.

---

## Synthèse des sous-traitants (Art. 28)

| Sous-traitant | Pays | Données transmises | Garantie |
|---|---|---|---|
| **Keycloak** (auto-hébergé) | EU (VM école / Render Frankfurt) | Credentials, keycloakId | Auto-hébergé — pas de tiers |
| **Stripe Inc.** | USA | stripe_customer_id, montants | DPA Stripe (SCCs) |
| ~~**Groq Inc.**~~ | ~~USA~~ | **Aucune — retiré le 16/07/2026** | Sans objet |
| **GitHub Inc.** | USA | OAuth token, meta workspace | DPA GitHub (SCCs) |
| **Slack Technologies** | USA | OAuth token, channel meta | DPA Slack (SCCs) |
| **MinIO** (auto-hébergé) | EU (VM école / Render Frankfurt) | Fichiers uploadés | Auto-hébergé |
| **Ollama / Qwen3** (auto-hébergé) | EU / poste de développement | Contenu d'issue soumis à l'inférence | Auto-hébergé — **aucun tiers, aucun transfert** |

> **Mise à jour du 22/07/2026.** Groq Inc. figurait dans ce tableau comme destinataire du « contexte
> de tâche ». C'était **inexact depuis le 16/07** : `GroqService`, `GroqConfig` et la branche
> `ai.provider=groq` ont été supprimés (`TF-AI-GROQ-CLEANUP`). Vérifié le 22/07 — il ne subsiste que
> des commentaires retraçant la décision, aucun appel. Un registre qui déclare un transfert hors UE
> inexistant est aussi fautif qu'un registre qui en omet un.

### Application des durées de conservation

**Mise à jour du 22/07/2026.** Les durées de conservation étaient jusqu'ici **déclarées mais jamais
appliquées** : les méthodes de purge existaient sans être cadencées, les seuls `@Scheduled` du
projet portant sur les alertes métier (échéances, surcharge). `RetentionScheduler` comble ce vide.

| Donnée | Échéance appliquée | Preuve |
|---|---|---|
| Codes OTP | Expirés depuis plus de 7 jours | `OtpService.cleanupExpiredOtps()` |
| States OAuth | Dès l'expiration (jeton anti-CSRF à usage unique) | `OAuthStateRepository.deleteByExpiresAtBefore` |
| Invitations sans suite | Expirées depuis plus de 30 jours (`taskforce.retention.invitation-grace-days`) | `WorkspaceInvitationRepository.deleteStaleInvitations` |

Le job tourne quotidiennement à 03:30 (`taskforce.retention.cron`), décalé des jobs d'alerte de
08:00 et 08:30. Chaque purge est isolée des autres : un incident sur une table ne gèle pas la
rétention entière. Preuve : `RetentionScheduler.java` + `RetentionSchedulerTest` (6 cas).

Ces trois traitements ont en commun de **porter leur propre date d'expiration**. Les purger une fois
expirés n'invente aucune politique de conservation : cela applique l'échéance que la donnée déclare
déjà. L'invitation est le cas le plus sensible des trois — elle porte l'adresse d'une personne qui
n'est jamais devenue utilisatrice.

#### Reste ouvert — durée de conservation du journal d'audit

Le traitement n°5 porte la mention « durée à définir en prod », et sa table est déclarée
**immuable**. Fixer cette durée relève du **responsable de traitement**, pas du développeur :
la trancher dans le code reviendrait à inventer une politique et à contredire une mesure de
sécurité annoncée au registre. Le journal d'audit est donc **volontairement hors du périmètre**
de `RetentionScheduler`, et la décision reste à prendre avant une exploitation réelle.

---

> 🔗 [[PSSI]] §4 (protection données) — [[Auth_Autorisation]] §7 (secrets) —
> [[Plan_Securisation_SSDLC]] (S-SDLC) — [[Problemes_Connus]] (PC-019) —
> [[Roadmap_Backlog]] (TF-RGPD-001→006)
