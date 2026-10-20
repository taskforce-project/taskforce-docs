---
id: release-notes
title: Release Notes / CHANGELOG — TaskForce
doc_type: utilisateur
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [utilisateur, release-notes, changelog, versions, e29, rncp, soutenance]
---

# 📦 Release Notes / CHANGELOG — TaskForce

> Journal des livraisons de TaskForce, conformément au critère **E29** du référentiel RNCP DFS.
>
> **Convention** : versions `MAJOR.MINOR.PATCH` (SemVer). Versioning indépendant par service
> (`backend-vX.Y.Z`, `frontend-vX.Y.Z`, `landing-vX.Y.Z`) géré automatiquement par le
> workflow `version-management.yml` via labels de PR.
>
> **Note landing page** : la page `/changelog` de la landing présente des versions
> "v2.0.0–v2.4.0" à titre de **projection produit** (roadmap marketing). Ce document
> couvre la **livraison réelle V1.0** pour la soutenance RNCP (Metz Numeric School 2025-2026).

---

## produit v1.3.0 (20/10/2026) : tout le travail entre la webapp et l'app desktop

- **Espaces entiers, Brain OS compris, dans les deux sens** : un fichier d'espace (.zip) porte l'espace, son Brain OS (pages, liens, fichiers) et tous les projets que la personne voit. Dans l'app, Operations > From the web app > Copy everything copie chaque espace de la webapp ; Réglages > General > Copy to the web app renvoie un espace entier. La webapp a la même carte (télécharger le fichier, l'importer). Chaque import crée un nouvel espace, sans rien fusionner.
- **Messages clairs** quand un envoi vers la webapp est trop gros ou que la réponse tarde.
- **Site** : la page de migration promet tout le travail ; l'installation sous Windows explique Smart App Control, qui bloque une app non signée.
- **TaskForce Desktop 1.2.0**.

## produit v1.2.0 (20/10/2026) : projets entre la webapp et l'app desktop

- **Projets dans les deux sens** : fichier de projet (menu Export, New project > From a file) et copie directe par l'app, avec tickets, historique, pages et pièces jointes.
- **App desktop** : photo du compte reprise, copie de la base avant chaque mise à jour, notifications du système, Copilot avec le compte GitHub de la personne, pull request liée à son ticket et ticket terminé à la fusion.
- **API** : un paramètre de requête absent ou mal typé répond 400 (plus 500).
- **Site** : une fenêtre accompagne chaque téléchargement (avertissements de Windows, rapport VirusTotal, quarantaine) ; macOS annoncé pour plus tard. **TaskForce Desktop 1.1.0**.

## produit v1.1.5 (20/10/2026) : guide d'installation sur le site

- Section « Install » de la page de téléchargement (Windows, Linux), SHA-256 et rapport VirusTotal sous chaque fichier.

## produit v1.1.4 (20/10/2026) : page « merci » à la désinstallation

- Le désinstalleur Windows ouvre la page `/goodbye` du site. **TaskForce Desktop 1.0.3**.

## produit v1.1.3 (20/10/2026) : corrections d'API et de sécurité

- Un corps de requête absent ou illisible répond 400 (plus 500) ; les 88 alertes CodeQL ouvertes sont corrigées ou justifiées.

## produit v1.1.2 (20/10/2026) : récupération du compte dans l'app desktop

- L'app reprend les réglages du compte en ligne (rôle, onboarding, compétences, notifications) ; page « Code signing policy » sur le site. **TaskForce Desktop 1.0.2**.

## produit v1.1.1 (20/10/2026) : fenêtre façon Claude Desktop

- Fenêtre sans barre de titre du système, haut dessiné par l'interface ; peinture de l'accueil du site sur les pages de connexion. **TaskForce Desktop 1.0.1**.

## produit v1.1.0 (19/10/2026) : TaskForce Desktop, passkeys, connexion sans page Keycloak

- **TaskForce Desktop (préversion, Windows et Linux)** : l'app se télécharge sur le site. Elle demande un compte TaskForce gratuit, créé ou utilisé sur les pages habituelles de la webapp (aucune page Keycloak), puis garde projets, Brain OS, IA (Ollama ou une API compatible OpenAI) et Claude Code sur l'ordinateur, hors ligne compris. Installeurs non signés : Windows avertit au premier lancement, la page de téléchargement explique quoi faire.
- **Passkeys** : on en ajoute une dans Réglages > Sécurité (Windows Hello, Touch ID, un téléphone, une clé de sécurité), puis on se connecte sans mot de passe depuis la page de connexion, ou en la choisissant dans le champ e-mail. Une passkey vaut aussi la double authentification.
- **Ordinateurs connectés** : Réglages > Sécurité liste les ordinateurs connectés à l'app desktop et permet de les déconnecter.
- **Sécurité** : l'API n'accepte plus que les jetons obtenus par TaskForce (une connexion par les pages de Keycloak contournait la double authentification) ; les connexions par passkey et par l'app desktop sont limitées en débit comme la connexion par mot de passe.

## produit v0.42.0 (16/10/2026) : release de sécurité, licence AGPL-3.0

- **Connexion GitHub ou Google** : quand la double authentification est activée, l'application demande maintenant le code à six chiffres après le retour du fournisseur. Auparavant, ce mode de connexion la contournait.
- **Invitations** : la recherche ne propose plus que les personnes avec qui l'on partage déjà un espace de travail. Pour inviter quelqu'un d'autre, on saisit son adresse complète.
- **Serveurs MCP** : une adresse qui vise le réseau interne du serveur est refusée ; les actions qui modifient des données dans un outil externe sont réservées aux propriétaires et administrateurs.
- **Licence** : TaskForce est désormais un logiciel libre sous licence AGPL-3.0 ; le pied de page du site l'indique.
- **Sécurité technique** : métriques du serveur déplacées sur un port interne, Next.js 16.3.6, logos d'Anthropic retirés du site.

## produit v0.41.0 (28/09/2026) : runner local en libre-service

- **Runner local** : chacun configure le sien dans Réglages > Agents. Un bouton crée son identité, puis l'application affiche une seule fois le fichier `.env` et les commandes pour lancer le runner. Régénérer le secret demande une confirmation, puisque cela coupe un runner déjà lancé.
- **Délégation non prise en charge** : le message d'échec indique maintenant où configurer son runner.
- **Site** : la section Local runner, le changelog, la roadmap et la FAQ décrivent la configuration en libre-service au lieu de l'accès anticipé.
- **Plugin Claude Code** (hors application) : une commande `/taskforce` pour travailler ses tâches TaskForce depuis son propre Claude Code, en tant que soi.

## produit v0.40.1 (25/09/2026) : délégation au runner local fiabilisée, logo Anthropic retiré

- **Runner local** : une tâche confiée à Claude Code que personne ne prend en charge passe en échec au bout de 15 minutes, avec un message qui dit quoi faire, au lieu de rester « en attente » sans fin.
- **Production** : le réglage qui active le runner local est désormais durable (il ne saute plus à la mise à jour suivante).
- **Marque** : le logo d'Anthropic n'est plus affiché, ni sur le site ni dans l'application ; Claude et Anthropic sont nommés en texte.

## landing-v1.3.0 · produit v0.40.0 (25/09/2026) : runner local présenté, Enterprise sur un écran

- **Runner local (Beta, accès anticipé)** : la page Orchestration explique ce qui tourne aujourd'hui. On assigne une issue à Claude Code, un runner sur la machine de l'utilisateur la prend, travaille dans une branche isolée et ouvre une pull request qu'une personne relit. Ce que l'agent peut toucher est détaillé ; TaskForce ne voit jamais les identifiants Claude.
- **Home** : le bloc Entreprise tient sur un écran (texte et garanties à côté de la vue d'audit), et la vue d'audit reste lisible sur téléphone.
- **Ponctuation** : les derniers tirets de liaison des textes d'introduction sont remplacés par la vraie ponctuation.

## landing-v1.2.0 · produit v0.39.0 (25/09/2026) : site repositionné et poli

- **Positionnement** (24/09, produit v0.38.1) : le hero présente TaskForce comme la couche gouvernée au-dessus des agents de code (Claude Code, Cursor, Copilot).
- **Hero** : mise en page scindée avec une table de runs animée par rôle (Engineering, Product, Operations, Client services), marquée « Illustrative ».
- **Home plus courte** : de 14,3 à 11,0 écrans (sections fusionnées, doublons retirés, détail des 7 checkpoints repliable).
- **Lecture** : titres de section révélés au défilement (désactivé si l'utilisateur réduit les animations, contraste AA conservé) ; titres de cartes sur une échelle unique.
- **Mobile** : la frise « The run » passe en vertical sur téléphone.
- **Référencement** : metas de 155 caractères au plus, meta dédiée par fiche connecteur, `/docs` retiré du sitemap.

---

## v1.0.0 — 05/07/2026 — Livraison soutenance RNCP

> Version complète livrée pour la soutenance **Développeur Full Stack RNCP niveau 6**.
> Développée d'octobre 2025 à juillet 2026 (9 mois, ~1 développeur ETP).

---

### ✨ Authentification & sécurité

- **Inscription en 3 étapes** avec vérification OTP email (TTL 15 min, 3 essais) — UC-01
- **Connexion sécurisée** via Keycloak — tokens **OIDC RS256 émis par l'IdP** (Resource Server côté API) — UC-02
- Refresh tokens HttpOnly Secure SameSite=Strict avec rotation
- **Rate limiting Bucket4j** : 10 req/min (auth), 200 req/min (default), 20 req/min (IA)
- 6 **headers de sécurité OWASP** : CSP `default-src 'none'`, HSTS 31536000s, X-Frame DENY, nosniff, Referrer-Policy, Permissions-Policy
- Protection **log-forging** (`ClientLogController.sanitize`)
- Chiffrement **AES-256-GCM** sur PII sensibles (messages Enterprise, notes)

---

### 🏢 Workspaces & membres

- Création de workspace avec slug unique — UC-03
- RBAC 3 niveaux : **OWNER / ADMIN / MEMBER** avec `AuthorizationService` + `WorkspaceAccessInterceptor`
- Système d'**invitations par email** avec lien de 72h — UC-04
- Gestion des rôles inline (ADMIN → MEMBER, MEMBER → ADMIN)
- **Profils de compétences** membres : skills JSON, séniorité, capacité h/sem., objectifs de croissance

---

### 📋 Projets, issues & kanban

- Gestion de **projets** avec membres, identifiant, description — UC-05
- **Issues** : titre, description, type (7), priorité (5), statut, assigné, labels, cycle, module, dates — UC-06
- Statuts d'issue **personnalisables** par projet (catégories BACKLOG/UNSTARTED/STARTED/COMPLETED/CANCELLED)
- Vue **Kanban** drag-and-drop, vue **Liste** avec filtres multi-critères, vue **Backlog**
- Commentaires, activité, sous-issues, relations (`blocks`/`blocked-by`/`duplicate-of`)
- **Pièces jointes** (upload MinIO avec contrôle de scope workspace/project/issue)
- **Worklogs** (temps passé par issue) — alimentent les analytiques Smart Assign

---

### 🤖 Smart Assign — Assignation intelligente par IA

- **Moteur d'assignation** basé sur 3 axes : compétences × charge × disponibilité — UC-07
- Inférence LLM via **Groq API** (Java natif `GroqService`, pas de microservice Python)
- Stockage vectoriel **pgvector** (PostgreSQL 18) : embeddings profils membres (vector 384d) + documents RAG
- Explication en langage naturel pour chaque suggestion
- **Feedback** utilisateur (acceptation/rejet) → amélioration continue (`assignment_events`)
- Analytiques IA : `ai_runs`, `ai_insight_snapshots` (coût, latence, source décision)

---

### 🔄 Cycles (sprints)

- Création de **cycles** avec dates début/fin — UC-08
- Ajout/retrait d'issues dans un cycle
- Vue de progression : issues planifiées vs. terminées, barre de complétion, jours restants

---

### 📄 Pages wiki

- Création et organisation de **pages** hiérarchiques (parent/enfant) — UC-10
- Éditeur riche (ProseMirror) avec formatage Markdown, blocs de code, tableaux
- Navigation arborescente dans la sidebar

---

### 💬 Chat & discussions

- **Chat temps réel** par canaux liés aux projets (STOMP/SockJS + RabbitMQ 4) — UC-09
- Messages persistés avec historique complet
- Mentions `@utilisateur` avec notification inbox
- Authentification STOMP (`StompAuthInterceptor`) + vérification appartenance au canal
- Fallback SockJS automatique si WebSocket bloqué
- **Discussions** asynchrones (forum) avec sous-catégories

---

### 💳 Plans & facturation Stripe

- 3 plans : **FREE / PRO / ENTERPRISE** — UC-11
- Flux **Stripe Checkout** (création session, redirection, confirmation)
- 5 webhooks Stripe traités : `checkout.session.completed`, `invoice.*`, `customer.subscription.*`
- Machine à états `PlanStatus` : `ACTIVE → PAST_DUE → CANCELED`
- Idempotence des webhooks (`stripe_event_id UNIQUE`)
- Portail de facturation Stripe (modification paiement, annulation, téléchargement factures)
- Formulaire de contact **Enterprise** (leads sales) avec chiffrement AES-256-GCM

---

### ⚖️ RGPD & droits des personnes

- Export de données JSON (Art. 20 RGPD) : `GET /api/gdpr/export` — UC-12
- Suppression et anonymisation de compte (Art. 17) : `DELETE /api/gdpr/delete-account`
- Journalisation audit RGPD (`GDPR_EXPORT`, `GDPR_DELETE`)
- Politique de confidentialité + CGU dédiées sur la landing page

---

### 🔌 Intégrations

- **GitHub** : OAuth2, liens issues ↔ PR/commits
- **Slack** : OAuth2, notifications de canal
- **Webhooks** : configurable par workspace avec signature HMAC
- Configuration DNS pour les callbacks OAuth

---

### 🚀 CI/CD & infrastructure

- **7 workflows GitHub Actions** : `backend-tests.yml`, `frontend-tests.yml`, `e2e-tests.yml`, `release.yml`, `landing-tests.yml`, `sync-badges.yml`, `version-management.yml`
- Versioning SemVer **indépendant** par service (`backend-v*`, `frontend-v*`, `landing-v*`)
- Images Docker publiées sur **GHCR** à chaque release
- Stack **Docker Compose** complète : postgres, backend, frontend, keycloak, minio, rabbitmq, otel-collector, signoz
- **Option A** (VM école) : `docker-compose.prod.yml` + nginx TLS
- **Option B** (Render.com Frankfurt) : `render.yaml` — ~46 $/mois

---

### 📊 Observabilité

- **OTel → SigNoz → ClickHouse** : 5 pipelines (traces, métriques, métriques/prometheus, logs, meter)
- 9 règles d'alerte Prometheus : disponibilité, erreurs/latence p95, saturation JVM/pool DB/CPU, sécurité (rate-limit spike, auth failure spike)
- Logs conteneurs via `filelog` receiver (Docker JSON)
- Métriques Micrometer exposées sur `/actuator/prometheus`

---

### 🧪 Tests

- **Backend** : 72 fichiers de test / 670 tests / **78 % couverture JaCoCo** (gate 60 %)
  - Testcontainers (PostgreSQL + Keycloak) — pas de mocks
  - Tests paramétrés `@ParameterizedTest`
- **Frontend** : 55 fichiers / 746 tests / **92 % couverture Vitest** (gate 70 % lines)
- **E2E** : 3 specs Playwright (auth, routes, accessibilité WCAG 2.1 AA via axe-core)

---

### ♿ Accessibilité

- Audit **axe-core** en CI (spec Playwright `a11y.spec.ts`) — WCAG 2.1 AA
- `aria-label` sur tous les boutons iconiques
- Gestion du focus visible, navigation clavier

---

### 🌐 Landing page (Astro)

- Pages marketing complètes : accueil, pricing, enterprise, security, accessibility, about, blog (placeholder), changelog, contact
- Pages légales : Politique de confidentialité (`/privacy-policy`), CGU (`/terms`)
- i18n EN/FR (`LanguageContext`, `constants_en.ts`, `constants_fr.ts`)
- Formulaire de contact Enterprise (`POST /api/sales/inquiry`)

---

## Roadmap V1.x — Items en backlog prioritaire

> Pour le détail complet : [[Roadmap_Backlog]]

| ID | Description | Priorité |
|---|---|---|
| TF-SEC-009 | Migration JWT HS512 → Keycloak OIDC natif | P2 |
| TF-RGPD-001 | Bannière de consentement cookies (CNIL) | P2 |
| TF-SEC-010 | DAST ZAP en CI (bloquant sur HIGH) | P2 |
| TF-SEC-011 | Rate limiting distribué (Redis) pour multi-instances | P2 |
| TF-TEST-009 | Tests de charge k6/Gatling (validation seuils STB) | P2 |
| TF-INFRA-009 | Runbooks / Dossier d'exploitation | P2 |

---

> 🔗 [[Manuel_Utilisateur]] — [[Pipeline_CICD]] — [[Roadmap_Backlog]] — [[STB]] (exigences)
