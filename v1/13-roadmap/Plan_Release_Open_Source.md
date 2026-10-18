---
id: plan-release-open-source
title: Plan de release open source (TaskForce 1.0)
doc_type: plan
statut: active
version: 1.0
date: "14/10/2026"
auteur: Pierre MICHEL
review_cycle: weekly
tags: [roadmap, open-source, release, securite, ia, agents, auto-hebergement]
related:
  - "../12-decisions/Journal_Decisions_ADR.md"
  - "./Roadmap_Backlog.md"
  - "../02-produit/README.md"
---

# Plan de release open source (TaskForce 1.0)

**Version :** 1.0
**Date :** 14/10/2026
**Auteur(s) :** Pierre MICHEL

[![Type: Plan](https://img.shields.io/badge/Type-Plan-blue?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides

- [Journal des ADR](../12-decisions/Journal_Decisions_ADR.md) : ADR-014 à ADR-020
- [Backlog & roadmap](./Roadmap_Backlog.md) · [État produit](../02-produit/README.md)
- Code : branche `feature/lean-oss` de `taskforce-fullstack`, trace dans `.ai/roadmap.md`

**Tags :** `#open-source` `#release` `#securite` `#auto-hebergement`

## 1. Pourquoi ce plan

La soutenance est passée. Le constat du CEO : commercialement, la v1 ne résout presque aucun problème. Elle attaque la
gestion de projet, une catégorie saturée où changer d'outil coûte cher, sans canal de distribution. La recherche d'un
point d'entrée commercial (04/10) est mise en pause (ADR-014).

Le 14/10, le CEO décide de publier TaskForce comme un projet open source fini, sur le modèle de Plane : forkable,
utilisable seul ou en entreprise, hébergeable chez soi avec son propre modèle d'IA ou son propre agent de code. Le
post LinkedIn « projet de fin d'études » sortira le jour des résultats du diplôme, en même temps que la mise en
production. D'ici là, la production reste en v0.41.0, la version vue par le jury.

## 2. Décisions du 14/10/2026

| Sujet | Choix | ADR |
|---|---|---|
| Positionnement | Open source lean et auto-hébergeable ; pas de fissure : fini ou supprimé | ADR-014 |
| Licence | AGPL-3.0 (comme Plane), nom et logo hors licence | ADR-015 |
| Facturation | Retirée, avec toutes les limites de plan ; plafonds d'IA réglables par l'instance | ADR-016 |
| Brain OS | Garder le cœur (pages, éditeur, recherche, ingestion) ; couper graphe, galaxies, gabarits, Labs | ADR-017 |
| Agents de code | Claude Code (runner local, validations dans l'app) et vrai Copilot ; les autres retirés | ADR-018 |
| IA | Config générique compatible OpenAI, Ollama et petits modèles par défaut | ADR-019 |
| Intégrations | MCP générique + webhooks sortants signés ; GitHub, Slack, Plane natifs | ADR-020 |
| Calendrier | `dev` + test en Docker local ; release de sécurité (lots 0 et 1) avant les résultats ; le reste le jour des résultats, version 1.0.0 | ADR-014 |
| Distribution (16/10) | Plus de serveur après les résultats : 1.0 = téléchargement Docker ; ensuite essai d'un mode desktop | ADR-014 |
| Desktop (18/10) | App desktop locale sur le modèle de Claude Desktop, appelée à devenir la seule version ; une base de code, profils `desktop` et `server` ; rôle de la webapp tranché après la spec ; lot 7 gelé au minimum | ADR-021 |
| Direction artistique (18/10) | Celle du portfolio du CEO : Geist, bleu `#2f6bf6`, gris chauds, angles droits ; logo propre, pas de formes multicolores | [[Direction_Artistique_2026]] |

## 3. Constat de l'audit (14/10/2026)

Audit en lecture seule en cinq passes : backend, frontend et site, outillage des agents et auto-hébergement, mécanismes
de Claude Code (doc officielle), agents de code déclenchables par API.

- **Ce qui fonctionne de bout en bout** : comptes, workspaces, droits, invitations, équipes, projets, issues (statuts,
  commentaires, sous-issues, checklist, temps passé), cycles, labels, pages de projet, pièces jointes, notifications en
  direct, inbox, roadmap, My Work, dashboard, analytics, RGPD, onboarding, 2FA, Smart Assign, spec, briefs d'analyse.
- **Fissures** : appels d'IA dans des transactions de base ; Cortex outillé seulement si la demande contient des verbes
  français ; quatre fournisseurs d'agent sur cinq factices ou jamais testés ; 138 tuiles d'intégration dont 3 réelles ;
  webhooks jamais envoyés ; limites du plan gratuit codées en dur ; chaînes françaises dans l'interface anglaise.
- **Failles** : voir le lot 1.
- **Installation à neuf impossible** : chemin documenté en PowerShell seulement, `.env.dev` racine introuvable,
  Keycloak absent du compose de base, Ollama absent de tous les compose, images Docker privées.
- **Historique git** : scanné en entier (valeurs masquées) ; aucun secret de production ; identifiants de dev et mot de
  passe Mailtrap sandbox présents.

## 4. Lots

Chaque lot donne une PR vers `dev`, CI verte, commits atomiques au nom du CEO. Le CEO teste en Docker local à la fin
des lots visibles (2, 3, 5, 7).

### Lot 0 : licence, fichiers communautaires, ménage

- [x] Licence AGPL-3.0 et toutes ses références [id:: OSS-0.1] [statut:: done] [ref:: 47c921b8]
- [x] SECURITY.md, CODE_OF_CONDUCT.md, formulaires d'issues, modèle de PR avec les vrais labels [id:: OSS-0.2] [statut:: done] [ref:: a8886689]
- [x] Ménage : QUICKSTART et compose Keycloak (identifiants Mailtrap en clair), TODO.md, `.instructions/`, `.pyc`, sous-module orphelin, lockfile vide, cible k6 locale [id:: OSS-0.3] [statut:: done] [ref:: c4250b1f, 5bb89eb4, d6377462, 2fa314f9]
- [x] Dates en anglais (travail en cours du CEO) [id:: OSS-0.4] [statut:: done] [ref:: 001b0b55]

### Lot 1 : sécurité

- [x] La connexion GitHub ne contourne plus la 2FA (défi scellé + `POST /api/auth/oauth/2fa`) [id:: OSS-1.1] [statut:: done] [ref:: f4a7a049]
- [x] URL MCP collée vérifiée contre les adresses internes (SSRF), option `MCP_ALLOW_PRIVATE_NETWORK` [id:: OSS-1.2] [statut:: done] [ref:: cdd20266]
- [x] Actuator sur le port de gestion 8081 en prod, `/livez` et `/readyz` sur le port de l'API [id:: OSS-1.3] [statut:: done] [ref:: 2d9c4a93]
- [x] Plus de réglage qui désactive l'authentification (`keycloak.enabled=false`) [id:: OSS-1.4] [statut:: done] [ref:: 2d9c4a93]
- [x] Exécution d'outils MCP en écriture réservée aux propriétaires et administrateurs ; allow-list appliquée à l'exécution [id:: OSS-1.5] [statut:: done]
- [x] Profil par défaut sûr : l'image backend démarre déjà en `prod` ; compose racine refait au lot 7 [id:: OSS-1.6] [statut:: done]
- [x] Recherche de membres limitée aux personnes qui partagent un workspace (fin de la fuite d'e-mails) [id:: OSS-1.7] [statut:: done]
- [x] Runner : réglages du dépôt cloné ignorés (`--setting-sources user`, vérifié sur la CLI 2.1.293) [id:: OSS-1.8] [statut:: done] [ref:: 98ef93d5]
- [x] Clés PostHog en dur retirées, logos Anthropic retirés ; `ai-service` déjà non exposé [id:: OSS-1.9] [statut:: done] [ref:: 4905f653, cc791f54]

### Lot 2 : facturation et limites

- [x] Backend : plus aucune limite de plan (workspaces, issues, collaborateurs, intégrations, MCP, analytics, historique) [id:: OSS-2.1] [statut:: done] [ref:: d30a51b1]
- [x] Plafonds d'IA et limitation de débit réglables par variables, illimités par défaut (`AI_MONTHLY_TOKENS_PER_ACCOUNT`, `AI_RATE_*`, transmis au conteneur prod) [id:: OSS-2.2] [statut:: done] [ref:: 1d4ed5bf, 6600906f]
- [x] Stripe, facturation et module commercial retirés du backend ; inscription sans étape de forfait ; V90 rend son défaut `'FREE'` à `users.plan_type` (NOT NULL sans défaut depuis V6) [id:: OSS-2.3] [statut:: done] [ref:: 881cb666, 1b1940f4]
- [x] Front : `/billing`, `/payment`, upgrades, badges, cadenas, étape d'upsell du tour, « View plans » retirés ; paquets `@stripe/*` retirés [id:: OSS-2.4] [statut:: done] [ref:: 57a83a16, 0bee8e01]
- [x] Docs Stripe et matrice des plans retirées ; tables gardées (aucune migration destructive) ; page Fern « IA et consommation » [id:: OSS-2.5] [statut:: done] [ref:: 6600906f, f2165d44]
- [x] Suite backend complète verte (1304 tests), front 864 tests et seuils de couverture, validation en Docker local, PR [#341](https://github.com/taskforce-project/taskforce-fullstack/pull/341) vers `dev` [id:: OSS-2.6] [statut:: done]

### Lot 3 : coupes et anglais

- [x] Routes mortes (issues, teams et help du workspace, `projects/new`, liste des issues du projet), 35 fichiers inatteignables, 25 paquets jamais importés (dont `keycloak-js`, `@tanstack/react-query`, `@assistant-ui/react`) [id:: OSS-3.1] [statut:: done] [ref:: e19c354e]
- [x] Étiquette Labs retirée partout : bandeau « Experimental space », fiole de la sidebar, groupe Labs du Ctrl+K et du dashboard, étape de la visite [id:: OSS-3.2] [statut:: done] [ref:: 8327b697]
- [x] Fournisseurs d'agent retirés : stub, faux Copilot, Cursor, Claude API, avec les endpoints de clé `/delivery/anthropic` et `/delivery/cursor` ; Claude Code (runner local) reste seul ; V91 supprime les clés stockées et clôt en échec les runs bloqués [id:: OSS-3.3] [statut:: done] [ref:: 56ca4e0c]
- [x] Brain OS : graphe, galaxies, gabarits, préremplissage `demo` et reseed retirés, comme les endpoints sans appelant (`GET /brain/nodes`, `GET /brain/nodes/{id}`, `POST` et `DELETE /brain/edges`) ; V92 change les pages `TEMPLATE` en notes [id:: OSS-3.4] [statut:: done] [ref:: d68c71c1, 80b13ad8]
- [x] Tout en anglais : interface (locale française retirée, environ 80 chaînes traduites, nombres en `en-US`), erreurs backend, messages Slack, e-mails, notes initiales (environ 500 chaînes côté backend). Les prompts passent au lot 4 (OSS-4.5) [id:: OSS-3.5] [statut:: done] [ref:: a16b91ea, 4942114e, ddcd2b2f]
- [x] Code backend mort : endpoints jamais appelés, ancienne 2FA Keycloak, config JWT, capture `ai_generations` [id:: OSS-3.6] [statut:: done] [ref:: 212bdb12, 7348e8dd, 5700e4b1, 428c3a0e]
- [x] Raccourcis clavier affichés mais non câblés retirés ; page Help retirée, « Replay the product tour » passe dans Ctrl+K [id:: OSS-3.7] [statut:: done] [ref:: 37bc299c, e19c354e]
- [x] Dépendances vulnérables mises à jour : Next.js 16.3.8, axios 1.20, vitest 4 et vite 8 (seuils de couverture recalibrés), SDK MCP 1.32.1, Astro 7.4.0, BouncyCastle 1.85 ; deux erreurs ESLint corrigées [id:: OSS-3.8] [statut:: done] [ref:: 14489c4e, eefd7725, 39b84d19, c18def7b, c3b08198]
- [x] Feedback intégré remplacé par « Report an issue on GitHub » dans Ctrl+K ; endpoint, service et entité retirés, table `feedback` gardée [id:: OSS-3.9] [statut:: done] [ref:: 8327b697]
- [x] Dernières mentions de forfait retirées : carte de débit, toast MCP, carte d'usage de Cortex, conditions d'utilisation [id:: OSS-3.10] [statut:: done] [ref:: 0369ecc6]

### Lot 4 : IA locale d'abord

- [x] Appels au modèle sortis des transactions de base : spec d'issue (génération et approbation), résumé de conversation, Smart Assign (recommandation, aperçu, lot), recherche du Brain OS ; lecture en transaction courte, appel au modèle, puis écriture [id:: OSS-4.1] [statut:: done] [ref:: b61c204b, 752b9f8b]
- [x] Config générique compatible OpenAI pour le chat et les embeddings (`AI_BASE_URL`, `AI_API_KEY`, `AI_MODEL`, `AI_MODEL_FAST`, `AI_EMBED_*`, `AI_TIMEOUT`), alias `GROQ_*` et `OLLAMA_*` conservés, `AI_PROVIDER=none` pour couper [id:: OSS-4.2] [statut:: done] [ref:: 30e0cad4, c540acbf]
- [x] Ollama de la machine hôte par défaut, un seul modèle de chat (`qwen3:8b` pour les deux paliers, pas de rechargement) et `bge-m3` ; `/no_think` seulement pour Qwen3, sauf au palier `deep` ; bloc `<think>` retiré des réponses [id:: OSS-4.3] [statut:: done] [ref:: 30e0cad4]
- [x] Sans fournisseur : échec immédiat (`AiStatusService`, `GET /api/ai/status`), avis « AI is not configured » dans Cortex, recherche du Brain OS en plein texte ; vecteurs liés à leur modèle (V94) et recalculés en tâche de fond [id:: OSS-4.4] [statut:: done] [ref:: b61c204b, 752b9f8b, af513ade]
- [x] Cortex : plus de routage par mots-clés, le modèle choisit ses outils ; 12 outils MCP externes au plus ; écriture externe proposée puis lancée après validation (« Approve and run ») ; prompts, outils, étapes du workflow d'analyse et replis en anglais [id:: OSS-4.5] [statut:: done] [ref:: b61c204b, af513ade]
- [x] `ai-service` : réseau interne sans port publié, secret partagé `AI_SERVICE_TOKEN` obligatoire sur `/v1` (tout est refusé sans secret configuré), `/health` sans détail, `GET /v1/status`, 60 tests pytest et workflow CI ; scoring Python mort et repli « lexical » des embeddings supprimés [id:: OSS-4.6] [statut:: done] [ref:: 30e0cad4, c540acbf]
- [x] Suite backend complète verte (1284 tests), ai-service 60 tests, front 840 tests et seuils de couverture ; validation locale avec l'Ollama de la machine (vrai chat `qwen3:8b`, vrais embeddings `bge-m3`, 344 notes réindexées en tâche de fond, recherche réelle du Brain OS) ; PR [#344](https://github.com/taskforce-project/taskforce-fullstack/pull/344) vers `dev` [id:: OSS-4.7] [statut:: done] [ref:: 505d7df8]

### Lot 5 : Claude Code et Copilot

- [x] Jetons personnels durables et révocables (`tfp_`, empreinte SHA-256, expiration 30, 90, 365 jours ou aucune) dans Réglages > Agents ; utilisables seulement sur le serveur MCP (filtre fail-closed) ; V95 [id:: OSS-5.1] [statut:: done] [ref:: 1edf5345, 6ccec74f]
- [x] Serveur MCP servi par le backend en HTTP (`POST /api/workspaces/{slug}/mcp`, 12 outils, chaque outil rejugé par la portée de la session déléguée sur son équivalent REST) ; plugin en HTTP avec jeton personnel ; `taskforce-mcp` (Node) retiré [id:: OSS-5.2] [statut:: done] [ref:: 9e787f2d, 2a49a48b, 2592d8e9]
- [x] Runner : `stream-json` relayé par lots, chronologie de l'issue (500 événements au plus par run) ; MCP de l'instance en HTTP (plus de build local) ; V96 [id:: OSS-5.3] [statut:: done] [ref:: 1c93b20d, 5501346b, 6ccec74f]
- [x] Validations : `--permission-mode manual --permission-prompts none` + hook `PermissionRequest` HTTP vers un serveur local du runner ; Allow ou Deny sur l'issue, par la seule personne qui a délégué ; refus au bout de 10 minutes ; vérifié en réel sur Claude Code 2.1.293 [id:: OSS-5.4] [statut:: done] [ref:: 1c93b20d, 5501346b, 6ccec74f]
- [x] Notifications : validation demandée, run terminé, run en échec (y compris jamais réclamé), réglage « Coding agents » [id:: OSS-5.5] [statut:: done] [ref:: 9303fe24, 6ccec74f]
- [x] Vrai Copilot : tâche de l'agent cloud de GitHub (API des tâches d'agent, préversion publique) dans le dépôt du projet, avec le jeton GitHub du workspace ; état suivi, lien vers la PR ; **à tester par le CEO avec un abonnement Copilot** [id:: OSS-5.6] [statut:: done] [ref:: 48fd096b, 9de77e50]
- [x] Agents prêts seulement (runner créé pour Claude Code ; GitHub connecté et dépôt lié pour Copilot) dans Smart Assign, le menu Assignee et la délégation ; tests des contrôleurs du runner [id:: OSS-5.7] [statut:: done] [ref:: b33ef7cc, 20196ef3, 9de77e50]
- [ ] Distribution du runner en une commande (npm, compte et nom de paquet à choisir par le CEO) ; le serveur MCP n'a plus à être distribué, l'instance le sert. Côté code, il restera à lire `.env` et `runner.config.json` dans le dossier du runner quand il est installé par npm [id:: OSS-5.8] [statut:: todo]
- [x] Suites vertes (backend complet, runner 125, front avec seuils) ; essais réels : Claude Code branché en HTTP avec un jeton personnel, validations sur la CLI 2.1.293, run complet runner + faux agent (chronologie, validation autorisée, notifications) ; PR [#345](https://github.com/taskforce-project/taskforce-fullstack/pull/345) vers `dev` [id:: OSS-5.9] [statut:: done]

### Lot 6 : intégrations

- [ ] « Connecter un serveur MCP » + 25 préréglages officiels ; 104 tuiles retirées [id:: OSS-6.1] [statut:: todo]
- [ ] Webhooks sortants envoyés, signés HMAC, avec nouvelles tentatives [id:: OSS-6.2] [statut:: todo]
- [ ] GitHub : statut des PR rafraîchi, dépôt modifiable après création, « Disconnect » réparé [id:: OSS-6.3] [statut:: todo]
- [ ] Slack : messages en anglais, variables branchées en prod [id:: OSS-6.4] [statut:: todo]

### Lot 7 : auto-hébergement (gelé au minimum, ADR-021)

- [ ] Compose d'auto-hébergement multi-OS, Ollama en option, point d'entrée unique [id:: OSS-7.1] [statut:: todo]
- [ ] `.env.example` minimal et script de génération des secrets (bash et PowerShell) [id:: OSS-7.2] [statut:: todo]
- [ ] Inscription possible sans SMTP [id:: OSS-7.3] [statut:: todo]
- [ ] Keycloak 26 partout, realm configuré par variables (dont `frontendUrl`) [id:: OSS-7.4] [statut:: todo]
- [ ] SELF_HOSTING.md et CONTRIBUTING.md [id:: OSS-7.5] [statut:: todo]
- [ ] Test d'une installation à neuf (Linux) [id:: OSS-7.6] [statut:: todo]
- [ ] Déploiement de la prod du CEO compatible (VM1, VM2) [id:: OSS-7.7] [statut:: todo]

### Lot 8 : vitrine

- [ ] Landing ramenée à une dizaine de pages, promesses fausses retirées, positionnement open source, direction artistique (OSS-DA.4) [id:: OSS-8.1] [statut:: todo]
- [ ] README en anglais avec captures [id:: OSS-8.2] [statut:: todo]
- [ ] Docs Fern : auto-hébergement, API régénérée [id:: OSS-8.3] [statut:: todo]
- [ ] Purge de `.ai/` et `docs/` ; fichiers d'instructions des assistants regroupés [id:: OSS-8.4] [statut:: todo]
- [ ] Brouillon du post LinkedIn [id:: OSS-8.5] [statut:: todo]

### Release de sécurité (avant les résultats)

- [x] Suite backend complète verte (1366 tests), PR [#335](https://github.com/taskforce-project/taskforce-fullstack/pull/335) vers `dev`, CI 16/16 verte [id:: OSS-S.1] [statut:: done]
- [x] Validation en Docker local (navigateur intégré, compte de seed ; aller-retour GitHub couvert par les tests) [id:: OSS-S.2] [statut:: done]
- [x] `POSTHOG_KEY` posée sur VM2, relais de métriques VM1 repointé sur 8081 [id:: OSS-S.3] [statut:: done]
- [ ] `PUBLIC_POSTHOG_KEY` sur Vercel puis redéploiement du site (CEO) [id:: OSS-S.5] [statut:: todo]
- [x] Release [#336](https://github.com/taskforce-project/taskforce-fullstack/pull/336) sur `main` (v0.42.0, 16/10), déploiement vérifié : backend, app, site, Prometheus [id:: OSS-S.4] [statut:: done]

### Lot DA : direction artistique du portfolio

- [x] Relevé du portfolio, correspondance des jetons, point sur la ressemblance avec Dust [id:: OSS-DA.0] [statut:: done] [ref:: [[Direction_Artistique_2026]]]
- [x] Jetons clairs et sombres, polices Geist, rayon à 0 ; contraste élevé étendu aux nouveaux jetons [id:: OSS-DA.1] [statut:: done] [ref:: e4af23f1]
- [x] Composants de base (bouton à liseré, badges teinte et encre, voiles, avatar de workspace) ; écrans de connexion (panneau papier doux, intro en aplat bleu) [id:: OSS-DA.2] [statut:: done] [ref:: e4af23f1, 788daa0a]
- [x] Couleurs codées en dur ramenées aux jetons (563 classes après le lot 3, hex des composants) ; couleurs stockées converties par V93 [id:: OSS-DA.3] [statut:: done] [ref:: c50100a3, 9679cbfe]
- [ ] Site, doc Fern, README, captures : faits avec le lot 8 (mêmes fichiers, et les écrans changent encore aux lots 4 à 7) ; logo inchangé (monochrome) ; illustrations en attente de la licence [id:: OSS-DA.4] [statut:: todo]

### Desktop (ADR-021)

- [x] ADR-021 et spécification fonctionnelle et technique [[Specification_App_Desktop]] [id:: OSS-D.0] [statut:: done]
- [ ] Essai de deux à trois jours, critères chiffrés (§8 de la spec) [id:: OSS-D.1] [statut:: todo]
- [ ] Profil `desktop` du backend : API locale, utilisateur unique, stockage fichier, courtier en mémoire, caches locaux, sans SMTP, sans service Python [id:: OSS-D.2] [statut:: todo]
- [ ] Base embarquée, emplacement des données, sauvegarde avant migration, export et import [id:: OSS-D.3] [statut:: todo]
- [ ] Coque Electron : processus, écran d'attente, trousseau, notifications système [id:: OSS-D.4] [statut:: todo]
- [ ] Claude Code lancé par l'app (worktrees, MCP, autorisations, chronologie) [id:: OSS-D.5] [statut:: todo]
- [ ] Copilot et GitHub par device flow et interrogation [id:: OSS-D.6] [statut:: todo]
- [ ] Interface en profil `desktop` : écrans multi-utilisateurs retirés, onboarding local [id:: OSS-D.7] [statut:: todo]
- [ ] Paquets, signature, mises à jour, page de téléchargement [id:: OSS-D.8] [statut:: todo]

### Jour J : résultats du diplôme

- [ ] Release 1.0.0 sur `main` [id:: OSS-J.1] [statut:: todo]
- [ ] Variables d'environnement de prod mises à jour (VM1, VM2), dont les plafonds IA de l'instance publique (Groq) : sans eux elle devient illimitée. Anciennes valeurs : `AI_RATE_GLOBAL_TPM=8000`, `AI_RATE_ACCOUNT_TPM=6000`, `AI_RATE_ACCOUNT_RPM=1` ; `AI_MONTHLY_TOKENS_PER_ACCOUNT` si la clé est payante. **Nouveau depuis le lot 4 : `AI_SERVICE_TOKEN` obligatoire dans `.env.prod` de VM1** (secret partagé backend / ai-service, `openssl rand -hex 32`) : sans lui, le compose de prod refuse de démarrer [id:: OSS-J.2] [statut:: todo]
- [ ] Images GHCR publiques, signalement privé de vulnérabilités activé, description du dépôt (CEO) [id:: OSS-J.3] [statut:: todo]
- [ ] Branche `feature/lean-oss` de la doc fusionnée [id:: OSS-J.4] [statut:: todo]
- [ ] Post LinkedIn (CEO) [id:: OSS-J.5] [statut:: todo]

## 5. Actions du CEO hors code

- Régénérer le mot de passe Mailtrap (présent dans l'historique public).
- Révoquer la clé personnelle PostHog `phx_` (rappel de l'audit du 22/09).
- Tester Copilot avec son compte (lot 5).
- Créer ou fournir l'accès npm pour publier le runner et le serveur MCP (lot 5).
- Valider en Docker local à la fin des lots 2, 3, 5 et 7.
- Jour J : rendre publics les paquets GHCR, activer le signalement privé de vulnérabilités, mettre à jour la
  description et les topics du dépôt.

---

**Projet :** Taskforce, Metz Numeric School 2025-2026
