---
id: faq
title: FAQ — TaskForce V1
doc_type: utilisateur
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [utilisateur, faq, support, rncp, soutenance]
---

# ❓ FAQ — TaskForce V1

> Réponses aux questions les plus fréquentes, dérivées des fonctionnalités réelles de la V1
> et des vecteurs d'erreur identifiés lors des tests (`Problemes_Connus.md`).

---

## 1. Compte & connexion

**Je n'ai pas reçu mon code de vérification (OTP).**

1. Vérifier le dossier **Spam** — les emails OTP peuvent y atterrir.
2. Le code est valable **15 minutes** — après expiration, relancer le processus d'inscription pour recevoir un nouveau code.
3. S'assurer que l'adresse email est correctement saisie (pas de faute de frappe).
4. Si le problème persiste, contacter support@taskforce.app.

---

**J'ai oublié mon mot de passe.**

Depuis la page de connexion → **Mot de passe oublié** :
1. Saisir l'adresse email du compte
2. Recevoir un code OTP par email (15 min)
3. Saisir le code → choisir un nouveau mot de passe

---

**Mon compte est bloqué après plusieurs tentatives de connexion.**

Le système limite les tentatives d'authentification à **10 requêtes par minute** par adresse IP (protection anti-brute force). Après blocage, attendre 1 minute et réessayer. En cas de blocage persistant, contacter le support.

---

**Puis-je utiliser la même adresse email dans plusieurs workspaces ?**

Oui. Un compte utilisateur (une adresse email) peut être membre de plusieurs workspaces distincts avec des rôles différents dans chacun.

---

## 2. Tâches & assignation

**Comment fonctionne le Smart Assign (assignation automatique) ?**

Le Smart Assign analyse 3 dimensions pour chaque membre :
1. **Compétences** : les compétences requises pour la tâche (dans le titre/description) vs. les compétences déclarées du membre
2. **Charge** : nombre d'issues actives × priorité vs. la capacité horaire déclarée
3. **Disponibilité** : présence en cycle actif

Il produit un classement commenté en langage naturel. Pour bénéficier de suggestions pertinentes, chaque membre doit renseigner son **profil de compétences** dans les paramètres du workspace.

---

**Le Smart Assign ne m'affiche pas comme candidat.**

Si vous n'apparaissez pas dans les suggestions, vérifier :
- Que votre profil de compétences est renseigné (menu Membres → votre fiche → Comp��tences)
- Que votre capacité horaire (`capacity_hours_per_week`) est > 0
- Que vous êtes bien membre actif du projet concerné

---

**Puis-je ignorer la suggestion du Smart Assign et assigner manuellement ?**

Oui. Le Smart Assign est une **suggestion**, pas une contrainte. La liste déroulante d'assignation reste toujours accessible. Si vous refusez la suggestion, votre feedback est enregistré et améliore les prochaines suggestions.

---

**Comment suis-je alerté si je suis surchargé ?**

Les alertes de surcharge remontent dans l'**Inbox** (icône cloche dans le menu). Une notification est générée lorsqu'une issue supplémentaire est assignée alors que votre charge calculée dépasse votre capacité déclarée.

---

**Comment enregistrer le temps passé sur une issue ?**

Sur la fiche d'une issue, bouton **Enregistrer du temps** (icône chrono) :
- Durée en minutes
- Description de ce qui a été fait

Ces worklogs sont inclus dans l'export RGPD et alimentent les analytiques de capacité.

---

## 3. Collaboration

**Comment créer un canal de discussion ?**

Dans la navigation gauche → section **Chat** → **+ Nouveau canal** :
- Nom du canal (ex. `#general`, `#backend`)
- Description optionnelle

Les canaux sont liés à un projet. Tous les membres du projet y ont accès.

---

**Les messages du chat sont-ils persistés ?**

Oui. Tous les messages sont stockés en base de données et consultables à tout moment via l'historique du canal. La persistance survit aux reconnexions et rechargements de page.

---

**Quelle est la différence entre Chat et Discussions ?**

| | Chat | Discussions |
|---|---|---|
| **Mode** | Temps réel (STOMP/WebSocket) | Asynchrone |
| **Format** | Messages courts | Fils de conversation structurés |
| **Usage** | Coordination immédiate | Décisions, annonces, questions techniques |
| **Persistance** | Oui | Oui |

---

**Comment mentionner quelqu'un ?**

Dans un message (chat ou commentaire d'issue), taper `@` suivi du nom du membre. L'utilisateur mentionné reçoit une notification dans son Inbox.

---

## 4. Facturation & plans

**Quelles différences entre FREE, PRO et ENTERPRISE ?**

| Fonctionnalité | FREE | PRO | ENTERPRISE |
|---|:---:|:---:|:---:|
| Workspaces, projets, issues | ✅ | ✅ | ✅ |
| Pages wiki | ✅ | ✅ | ✅ |
| Chat temps réel | ✅ | ✅ | ✅ |
| Smart Assign (IA) | Limité | ✅ | ✅ |
| Analytiques avancées | ❌ | ✅ | ✅ |
| Intégrations (GitHub, Slack) | ❌ | ✅ | ✅ |
| Support dédié | ❌ | ❌ | ✅ |
| SLA et configuration sur mesure | ❌ | ❌ | ✅ |

---

**Comment passer à un plan payant ?**

Depuis `/profile/billing` (ou menu utilisateur → Facturation) → **Mettre à niveau** → choisir le plan → paiement Stripe sécurisé. Le plan est activé immédiatement.

---

**Puis-je annuler mon abonnement ?**

Oui, depuis le portail de facturation (`/profile/billing` → **Gérer mon abonnement**). L'annulation prend effet à la fin de la période de facturation en cours — l'accès PRO/Enterprise est conservé jusqu'à cette date.

---

**Mes données de carte bancaire sont-elles stockées par TaskForce ?**

Non. TaskForce délègue entièrement la gestion des paiements à **Stripe**. Aucune donnée de carte n'est stockée dans la base de données de TaskForce.

---

## 5. Données & sécurité

**Mes données sont-elles sécurisées ?**

Oui. Plusieurs couches de protection sont en place :
- **Chiffrement en transit** : TLS sur toutes les connexions
- **Chiffrement en base** : AES-256-GCM sur les données sensibles libres (messages de contact Enterprise)
- **Authentification** : JWT HS512 + tokens refresh HttpOnly
- **Isolation** : chaque workspace est strictement isolé — aucun accès inter-workspace n'est possible
- **Rate limiting** : protection anti-brute force sur toutes les API d'authentification

---

**Comment exporter mes données (droit d'accès RGPD) ?**

Depuis `/profile/settings` → **Exporter mes données** (ou `GET /api/gdpr/export`).

Le téléchargement est un fichier JSON contenant : profil, memberships, profil de compétences, worklogs.

---

**Comment supprimer mon compte (droit à l'oubli RGPD) ?**

Depuis `/profile/settings` → **Supprimer mon compte** (ou `DELETE /api/gdpr/delete-account`).

> ⚠️ Irréversible. Email anonymisé, données de profil effacées, session révoquée immédiatement. Les données comptables (factures) sont conservées selon les obligations légales.

---

**Qui a accès à mes données dans mon workspace ?**

Seuls les **membres de votre workspace** peuvent accéder aux données de ce workspace. L'équipe TaskForce n'accède à vos données que pour des raisons de support technique, avec journalisation dans les logs d'audit.

---

**Où sont hébergées mes données ?**

En développement : sur l'infrastructure locale. Pour la production, selon l'option d'hébergement choisie :
- **Option A** (VM école) : serveur physique à Metz (EU)
- **Option B** (Render.com) : région **Frankfurt (EU)** — couverture RGPD

---

## 6. Problèmes techniques fréquents

**La page ne se charge pas après connexion.**

Vérifier que les cookies tiers ne sont pas bloqués par votre navigateur — le refresh token est stocké dans un cookie HttpOnly. Si le blocage est activé, ajouter `taskforce.app` à la liste d'exceptions.

---

**Le chat ne reçoit pas les messages en temps réel.**

La connexion temps réel utilise **WebSocket/SockJS**. Si la connexion échoue (réseau d'entreprise, proxy), le frontend bascule automatiquement sur SockJS (fallback). Vérifier que le port 443 n'est pas filtré.

---

**J'ai une erreur "403 Forbidden" en accédant à une ressource.**

Cette erreur signifie que votre rôle dans le workspace ne vous autorise pas à effectuer cette action. Vérifier votre rôle (MEMBER/ADMIN/OWNER) dans les paramètres du workspace avec un ADMIN/OWNER.

---

> 🔗 [[Manuel_Utilisateur]] — [[Guid_Installation]] — [[Release_Notes]] —
> [[Audit_RGPD_Conformite]] (droits données) — [[Problemes_Connus]] (bugs connus)
