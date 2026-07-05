---
id: politique-confidentialite-cgu
title: Politique de confidentialité & CGU — TaskForce
doc_type: rgpd
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [rgpd, confidentialite, cgu, cgv, mentions-legales, cookies, landing, memoire, rncp, soutenance]
---

# 🔒 Politique de confidentialité & CGU — TaskForce

> Ce document catalogue les documents légaux **réellement implémentés** dans la landing page
> de TaskForce (Astro + React). Chaque section pointe vers les composants et fichiers réels.
> Les pages sont accessibles via la landing (`/privacy-policy`, `/terms`).
>
> **Règle** : rien n'est inventé — si une obligation légale n'est pas couverte côté code,
> c'est documenté comme gap avec référence au backlog.

---

## 1. Pages légales existantes

| Page | Route | Fichier Astro | Composant React |
|---|---|---|---|
| Politique de confidentialité | `/privacy-policy` | `landing-page/src/pages/privacy-policy.astro` | `PrivacyPolicyPageNew.tsx` |
| Conditions d'utilisation (CGU) | `/terms` | `landing-page/src/pages/terms.astro` | `TermsPageNew.tsx` |
| Accessibilité | `/accessibility` | `landing-page/src/pages/accessibility.astro` | — |

**Format** : pages React dynamiques (i18n EN/FR via `LanguageContext`),
contenu dans `landing-page/src/config/constants_en.ts` et `constants_fr.ts`.

---

## 2. Politique de confidentialité — contenu réel

Source : `constants_en.ts` clé `privacy` (dernière mise à jour déclarée : **January 7, 2026**).

### 2.1 Engagements affichés

La page affiche 3 engagements visibles :
1. **We Don't Sell Your Data** — pas de vente à des tiers
2. **Bank-Level Encryption** — AES-256 en transit et au repos
3. **You're In Control** — accès, export et suppression des données à tout moment

### 2.2 Sections documentées

| Section | Identifiant | Contenu |
|---|---|---|
| Introduction | `introduction` | Objet de la politique, accord implicite par utilisation |
| Données collectées | `information-we-collect` | Compte (email, pseudo, avatar) · Usage (activité, IP, analytics) · Cookies (4 types) |
| Utilisation des données | `how-we-use` | 6 finalités : service, amélioration, communication, sécurité, conformité légale, marketing |
| Sécurité | `data-security` | TLS · AES-256 · RBAC · Audits · Infra · Sauvegardes |
| Conservation | `data-retention` | Comptes actifs : durée + 90j · Facturation : 7 ans · Tickets support : 3 ans · Analytics : 26 mois |
| Droits RGPD | `your-rights` | 6 droits (accès, rectification, effacement, portabilité, opposition, limitation) + délai 30j |
| Conformité RGPD | `gdpr-compliance` | 4 bases légales (consentement, contrat, obligation légale, intérêt légitime) |
| Conformité CCPA | `ccpa-compliance` | Droits résidents Californie |
| Partage des données | `data-sharing` | Prestataires · Cession · Légal · Consentement |
| Transferts internationaux | `international-transfers` | SCCs, Privacy Shield, décisions d'adéquation |
| Protection des mineurs | `children-privacy` | Interdit -13 ans |
| Politique cookies | `cookies-policy` | 4 types : strictement nécessaires / fonctionnels / analytics / marketing |
| Changements | `changes` | Notification email + notice + date |
| Contact | `contact` | privacy@taskforce.app · dpo@taskforce.app |

### 2.3 Cohérence code ↔ politique

| Affirmation dans la politique | Vérifié dans le code | Note |
|---|---|---|
| "AES-256 encryption at rest" | ✅ | `EncryptedStringConverter` (AES-256-GCM) — PII libres uniquement |
| "TLS encrypted in transit" | ✅ | Nginx TLS + headers HSTS |
| "Access, correct, delete your data" | ✅ | `GET/DELETE /api/gdpr/*`, `PUT /api/users/me` |
| "30-day response SLA" | ✅ | `GdprController` + endpoint synchrone |
| "We don't sell your data" | ✅ | Aucun partage commercial dans le code |
| "Billing records: 7 years" | 🟡 | Durée applicable en France — durée physique en DB non encore enforced |
| "Regular security audits quarterly" | ⚠️ | Déclaratif — pas encore formalisé comme processus récurrent (TF-SEC-010) |
| "AWS, Stripe, Google Analytics" | ⚠️ | **Divergence** : l'app utilise Render / MinIO / pas de GA actif — à corriger dans `constants_en.ts` |

> **Action identifiée** : corriger les références aux sous-traitants dans `constants_en.ts`
> (remplacer "AWS, Stripe, Google Analytics" par "Render, Stripe, MinIO") → TF-RGPD-005.

---

## 3. Conditions générales d'utilisation (CGU)

Source : `constants_en.ts` clé `terms` (dernière mise à jour déclarée : **January 7, 2026**).

### 3.1 Sections documentées

| Section | Identifiant | Contenu |
|---|---|---|
| Acceptation des CGU | `agreement` | Accord par utilisation · Modifications notifiées |
| Licence d'utilisation | `license` | Usage personnel/commercial · Interdictions (ingénierie inverse, copie, interférence) |
| Comptes utilisateurs | `accounts` | Données exactes · Responsabilité des accès · Mot de passe · 13 ans minimum |
| Politique d'utilisation acceptable | `acceptable-use` | 8 interdictions (violations lois, IP, code malveillant, harcèlement, spam, DoS, accès non autorisé, collecte PII sans consentement) |
| Propriété intellectuelle | `intellectual-property` | Droits réservés TaskForce · Marques protégées |
| Contenu utilisateur | `user-content` | Droits conservés par l'utilisateur · Licence non-exclusive opérationnelle accordée |
| Résiliation | `termination` | Résiliation pour violation · Effets post-résiliation |
| Limitation de responsabilité | `liability` | Exclusion dommages indirects · Plafond 12 mois de paiement ou 100 $ |
| Avertissement | `disclaimer` | Service "as is", sans garantie d'uptime ni d'exactitude |
| Modifications du service | `changes` | Droit de modifier ou retirer le service sans préavis |
| Droit applicable | `governing-law` | Loi du pays d'établissement de TaskForce (non précisé dans la version V1) |
| Contact | `contact` | legal@taskforce.app |

### 3.2 Points à préciser pour V1 production

| Clause | Statut | Note |
|---|---|---|
| Loi applicable | ⚠️ | "Jurisdiction where Taskforce is established" non précisé — à compléter (France) |
| SIRET / identification légale | ⬜ | Absent — obligatoire pour un service commercial |
| Hébergeur | ⬜ | Non mentionné — obligatoire (mentions légales) |

---

## 4. Mentions légales — état

| Élément obligatoire (LEN Art. 6) | Statut | Localisation |
|---|---|---|
| Nom de l'éditeur | ⬜ | Absent — à ajouter |
| Adresse | ⬜ | Absent — à ajouter |
| Email de contact | ✅ | privacy@taskforce.app / legal@taskforce.app dans les pages légales |
| Numéro SIRET | ⬜ | N/A (contexte pédagogique) |
| Nom de l'hébergeur | ⬜ | Absent — à ajouter (Render ou VM école) |
| Responsable de publication | ⬜ | Absent — à ajouter |

> Pour la soutenance (contexte pédagogique) : les mentions légales minimales suffisent.
> Pour une mise en production commerciale : page `/legal` dédiée obligatoire. → TF-RGPD-006.

---

## 5. Politique cookies — état

La politique cookies est **décrite** dans la Privacy Policy (section `cookies-policy`),
mais aucune bannière de consentement interactive n'est implémentée.

| Type de cookie | Décrit | Bannière | État |
|---|---|---|---|
| Strictly Necessary | ✅ | N/A (pas de consentement requis) | Conforme |
| Functional | ✅ | ⬜ | Gap — consentement à recueillir |
| Analytics | ✅ | ⬜ | Gap — consentement à recueillir (CNIL) |
| Marketing | ✅ | ⬜ | Gap — consentement explicite requis |

> La recommandation CNIL impose une bannière de consentement active pour les cookies
> non-essentiels. → TF-RGPD-001.

**Cookies réellement déposés par l'app** (observable depuis les DevTools) :
- `JSESSIONID` équivalent → JWT `access_token` (stocké `localStorage`, pas cookie)
- `refresh_token` → cookie `HttpOnly; Secure; SameSite=Strict` (d'après `JwtService`)
- `taskforce-language` → `localStorage` (préférence langue landing)

> Les tokens JWT sont des cookies HttpOnly, la donnée la plus sensible n'est pas accessible
> par JavaScript — conforme aux recommandations CNIL.

---

## 6. Gap summary Phase 8 — légal

| ID | Priorité | Description |
|---|---|---|
| TF-RGPD-001 | P2 | Bannière cookies interactive (CNIL) |
| TF-RGPD-005 | P2 | Mentions légales dédiées + corriger sous-traitants dans `constants_en.ts` |

---

> 🔗 [[Registre_Traitements_RGPD]] — [[Audit_RGPD_Conformite]] — [[PSSI]] §4 —
> [[Roadmap_Backlog]] (TF-RGPD-002/006)
