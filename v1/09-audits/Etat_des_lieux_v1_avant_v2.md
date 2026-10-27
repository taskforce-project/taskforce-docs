---
type: documentation-technique
statut: active
version: 1.0
date: "27/10/2026"
auteur: Pierre MICHEL
tags: [audit, etat-des-lieux, harnais, v2, desktop, delegation, brain-os, connecteurs]
related:
  - "./Problemes_Connus.md"
  - "../../recherche/conseil/seances/2026-10-27-vision.md"
---

# État des lieux de la v1, avant la v2

**Version :** 1.0 · **Date :** 27/10/2026 · **Auteur(s) :** Pierre MICHEL

> **Pourquoi** : la séance n°2 du Conseil d'Avenir a retenu le harnais comme cap
> ([PV](../../recherche/conseil/seances/2026-10-27-vision.md)) et demandé, avant la spécification de la v2, de savoir ce
> qui marche vraiment, sans rien inventer, et ce qu'il faut retirer.
>
> **Méthode** : lecture du code de `dev` (instantané du 27/10/2026, commit `9c1041e5`) en trois audits, chaque
> affirmation vérifiée dans le code ou dans le journal daté des vérifications (`.ai/roadmap.md`) ; quatre constats clés
> revérifiés à la main. Rien n'a été exécuté pendant l'audit : « vérifié » veut dire vérifié à une date passée, consignée
> dans le journal.

## En une page

| Constat | Détail |
| --- | --- |
| **Vérifié de bout en bout** | Claude Code délégué depuis l'app desktop jusqu'à la pull request, issue en « In review by AI » ; une validation acceptée dans l'app (19/10). Le hook de validation : accepter, refuser, silence = refus (18/10, ligne de commande). Le serveur MCP de TaskForce (12 outils, 18/10). La recherche sémantique du Brain OS (18/10, sur la stack web). Le paquet du Store qui démarre (25/10). |
| **Existe, jamais vérifié dans l'app desktop** | La recherche du Brain OS, Cortex, les connecteurs MCP, Plane, le refus et l'expiration d'une validation depuis l'app, le mode sans dépôt avec le vrai Claude Code, le transfert d'un espace. GitHub Copilot n'a jamais été essayé. |
| **Manque pour la v2** | Les règles écrites comme des données ; le classement réversible ou irréversible ; un bac à sable au-delà de la branche ; un dossier de preuve exportable ; l'exécution à blanc ; un relecteur distinct de l'agent ; les outils de l'entreprise pour l'agent délégué ; l'import de documents ; les versions des notes ; la recherche au-delà des 4 000 premiers caractères d'une note. |
| **Cassé dans l'app desktop** | La connexion MCP en un clic ; GitHub et Slack en natif (tuiles visibles, impossibles à connecter) ; l'alerte de surcharge, qui renvoie vers des pages cachées. |
| **Le ménage** | 43 pages, dont 29 joignables dans l'app desktop, soit une vingtaine d'écrans. Une partie sert une équipe ou le web, pas une personne seule sur son ordinateur : liste au §3. |

## Le premier cas d'usage, étape par étape

Un ingénieur dont le standard de communication évolue veut l'analyse d'impact de la nouvelle version sur son projet.

| Étape | Aujourd'hui | État |
| --- | --- | --- |
| 1. Importer l'ancien et le nouveau standard (des centaines de pages) | Aucun import de document ; aucune lecture de PDF ou de Word ; une pièce jointe est stockée telle quelle | **Absent** |
| 2. Les chercher, version par version | Seuls les 4 000 premiers caractères d'une note sont indexés ; une note n'a pas d'historique de versions | **Absent** |
| 3. L'agent les lit pendant une délégation | `brain_search` renvoie des notes entières à Claude Code ; mais les documents n'y sont pas | Partiel |
| 4. Il produit une analyse sourcée | Rien n'exige ni ne vérifie qu'une affirmation cite sa source | **Absent** |
| 5. L'humain valide | Les validations sur l'issue et la pull request existent | **Existe** |
| 6. La preuve se relit et s'exporte | Chronologie et validations stockées, sans export ; elles disparaissent avec l'issue | Partiel |

**Conclusion** : la chaîne de délégation existe pour le code. La moitié « contexte » (documents, versions, sources) et la
moitié « preuve » (règles, dossier exportable) sont à construire pour la v2.

## 1. Délégation aux agents et validations

### Comment ça marche aujourd'hui

1. La personne choisit « Delegate to an agent » dans le menu Assignee d'une issue
   (`frontend/components/smart-assign/assignee-menu.tsx`) ; un run « en file » est créé
   (`backend/.../service/delivery/DeliveryService.java`).
2. Le runner, lancé par l'app avec un secret tiré à chaque lancement, réclame le run toutes les 5 s
   (`taskforce-runner/src/index.ts`, `backend/.../LocalRunnerService.java`).
3. Il prépare un worktree git sur une branche `tf/...` (ou un dossier jetable sans dépôt) et lance Claude Code sans
   interface : permissions en mode manuel, outils autorisés d'avance, outils refusés, seul le serveur MCP de TaskForce,
   60 tours et 45 minutes au plus (`taskforce-runner/src/agent.ts`).
4. Toute action hors du socle devient une demande de validation, affichée sur l'issue avec « Allow » et « Deny ». Seule
   la personne qui a délégué peut répondre ; 10 minutes sans réponse valent un refus
   (`frontend/components/sheets/run-activity.tsx`, `backend/.../DeliveryActivityService.java`).
5. À la fin : commit, push, pull request (jamais de fusion automatique), résultat posté, issue en « In review by AI »,
   ou en « Blocked » en cas d'échec (`taskforce-runner/src/git.ts`, `backend/.../DeliveryRunner.java`). Une pull request
   fusionnée termine l'issue.

**Autorisé d'avance** : lire, chercher et écrire des fichiers ; les commandes git locales (status, diff, log, add,
commit) ; 10 outils MCP de TaskForce (lire les issues et les projets, `brain_search`, créer ou modifier une issue du
projet, commenter). **Refusé** : `git push` et `gh` lancés par l'agent, le runner poussant lui-même. **Côté serveur**,
l'agent n'écrit que dans les issues du projet du run et ne supprime jamais rien (`DeliverySessionScope.java`).

### Ce qui est tracé

- **Stocké** : le run (statut, modèle, résumé, lien du résultat, erreur, dates) ; la chronologie (500 événements au plus,
  textes coupés à 600 caractères, appels d'outils résumés) ; chaque validation (outil, résumé, statut, qui a décidé,
  heure de la demande et de la décision).
- **Pas stocké** : la transcription complète, les sorties d'outils réussies, le diff, les résultats de tests, le coût,
  les commits.
- **Aucun export**, rien dans le journal d'audit ; supprimer l'issue efface ses runs.
- Ce que l'agent écrit par MCP est attribué à la personne qui a délégué : rien ne marque l'écriture comme celle de
  l'agent.

### GitHub Copilot

Même menu, mais par l'API des tâches de Copilot (en préversion publique d'après le code) : il travaille dans le cloud de
GitHub, sans Brain OS, sans chronologie, sans validations, et GitHub choisit le modèle. **Jamais essayé** (pas
d'abonnement).

### Écarts avec le harnais

| Élément | État | Ce qui existe |
| --- | --- | --- |
| Règles écrites comme des données (fichier, par projet, dans l'app) | Partiel | Listes codées en dur ; un `runner.config.json` local, sans interface |
| Classement réversible ou irréversible des actions | **Absent** | Trois cases : autorisé, à valider, refusé ; le push et la pull request partent sans validation |
| Bac à sable au-delà de la branche | Partiel | Worktree, dossier jetable, environnement nettoyé ; aucune isolation du système ni du réseau |
| Dossier de preuve par run | Partiel | Chronologie et validations ; ni export, ni diff, ni tests, ni empreintes |
| Exécution à blanc, aperçu des effets | **Absent** | |
| Relecteur distinct de l'agent | Partiel | Relecture humaine de la pull request ; aucun relecteur automatique ; la même personne délègue et valide |
| Outils externes de l'entreprise pour l'agent | **Absent** | L'agent ne voit que le serveur MCP de TaskForce ; les connecteurs ne servent qu'à Cortex |

**Petits défauts relevés** : les deux délais de validation (runner et serveur) sont réglés séparément ; les délais de
réclamation et de battement de cœur ne se vérifient que lorsque l'interface lit le run ; la version minimale de Claude
Code (2.1.293) n'est contrôlée que par `--check`, que l'app ne lance pas : elle lit la version installée sans la
comparer.

## 2. Le contexte de l'IA (Brain OS) et les connecteurs

### Le Brain OS aujourd'hui

- **Les notes** : éditeur Markdown, arbre de pages, `#tags` et `[[liens]]` qui tissent le graphe tout seuls, pièces
  jointes de 10 Mo stockées telles quelles.
- **Ce qui l'alimente** : la clôture d'un cycle, une issue terminée dans un cycle actif, la création d'un projet,
  l'activité de l'espace ; à la main, la synchronisation d'un dépôt GitHub, d'un canal Slack ou d'un projet Plane.
  Aucune synchronisation planifiée. Jamais ingérés : les commentaires, les issues hors cycle, les Pages des projets, les
  données des outils branchés en MCP.
- **La recherche** : sémantique d'abord (vecteurs de 1 024 dimensions, `bge-m3`), le texte intégral seulement si la
  sémantique ne trouve rien. Pas de mélange des deux, pas de reclassement, pas d'index plein texte. Seuls les 4 000
  premiers caractères d'une note comptent pour la sémantique (`BrainEmbeddingIndexer.java`).
- **Dans l'app desktop**, les vecteurs viennent du modèle choisi par la personne (Ollama par défaut, à installer à part) ;
  sans modèle de 1 024 dimensions, la recherche reste en texte intégral.
- **Accès** : chaque membre de l'espace voit toutes les notes.
- **Deux systèmes de documents** : les Pages des projets (éditeur riche) et le Brain OS. Ni Cortex ni Claude Code ne
  lisent les Pages.

### Les connecteurs aujourd'hui

- **Catalogue** : Plane, GitHub et Slack en natif ; 25 serveurs MCP préréglés (Linear, Jira, Asana, ClickUp, monday,
  Airtable, Sentry, GitLab, Grafana, Vercel, Cloudflare, Supabase, Neon, Stripe, PayPal, Square, HubSpot, Intercom,
  Attio, Notion, Figma, Canva, Webflow, Wix, Zapier) ; tout serveur MCP ajouté à la main.
- **Connecter n'est pas ingérer** : connecter un serveur MCP enregistre son adresse et son jeton. Ses outils servent en
  direct à Cortex, à la console et à l'import d'issues, jamais au Brain OS.
- **Dans l'app desktop** :
  - GitHub et Slack en natif ne peuvent pas se connecter : ce profil n'a pas d'identifiants OAuth
    (`application-desktop.yml`). GitHub passe par le `gh` de la personne, pour Copilot, l'état des pull requests et le
    lien d'un dépôt ;
  - la connexion MCP en un clic renvoie vers `localhost:8080`, alors que le backend de l'app écoute sur un port tiré au
    hasard (`McpOAuthService.java`) ;
  - la connexion MCP par jeton est permise, mais n'a jamais été essayée.
- **Pas de connecteur générique** pour une API documentée (OpenAPI), pas de transport MCP local (stdio).

### Cortex, l'assistant de TaskForce

Fournisseurs : Ollama (par défaut), toute API compatible OpenAI, ou aucun. Il lit les 5 notes que la recherche place en
tête, et le modèle reçoit au plus 12 outils externes par demande. Les lectures partent seules ; une écriture dans un outil externe attend
« Approve and run » d'un propriétaire ou d'un admin ; ses écritures internes (issue, projet, note) partent sans
validation.

### Écarts avec la vision

| Besoin | État | Pourquoi |
| --- | --- | --- |
| L'agent délégué voit les documents de l'entreprise | Partiel | `brain_search` renvoie des notes entières ; ni pièces jointes, ni Pages |
| L'agent délégué utilise les outils de l'entreprise | **Absent** | Seul le serveur MCP de TaskForce lui est donné |
| Importer un gros document et le chercher par version | **Absent** | Ni import, ni lecture de PDF ou Word, 4 000 caractères indexés, pas de versions |
| Importer un dossier ou un coffre Obsidian | **Absent** | Le seul import est le fichier d'espace de TaskForce |
| Se connecter à tout | Partiel | Tout serveur MCP par adresse et jeton ; pas d'OpenAPI ; OAuth cassé dans l'app desktop |
| Tracer chaque appel à un outil externe | Partiel | Les appels de Cortex passent par TaskForce ; rien n'est gardé comme preuve |

## 3. Inventaire et ménage

**Chiffres** : 43 pages, 29 joignables dans l'app desktop, soit une vingtaine d'écrans distincts ; 11 sections de
réglages sur 12 ; 20 entrées fixes dans la palette (Ctrl+K).

### Le cœur, pour le harnais

- **Projets et issues** : liste des projets, tableau, liste, backlog, panneau d'issue, réglages du projet, création d'un
  projet avec son dépôt, fichiers de projet et d'espace.
- **Délégation** : choisir un agent dans le menu Assignee, suivre le run sur l'issue, accepter ou refuser ses demandes,
  le panneau des délégations, Réglages > Agents, les notifications des agents.
- **Brain OS** : la page, les pages dans Ctrl+K, le champ Activité de l'espace, `brain_search`.
- **Cortex** : le panneau Ask AI, « Approve and run », Réglages > AI.

### Utile, mais secondaire

Inbox (All et Alerts) et My Work ; les cycles et la feuille de route du projet ; les Pages des projets ; la page
Intelligence et les cartes du tableau de bord ; serveurs MCP, Plane et webhooks ; l'assignation automatique (pour
proposer un agent) ; étiquettes et exports ; la visite guidée, l'onboarding desktop, plusieurs espaces ; la copie vers
et depuis la webapp, comme chemin de migration.

### Proposition de ménage pour l'app desktop (à trancher)

| Groupe | Quoi | Pourquoi |
| --- | --- | --- |
| Équipe | Membres et profils, équipes et membres des projets, invitations, rééquilibrage de charge, « Shared with you » | Une personne par app, sans synchronisation |
| Assignation d'équipe | Compétences et disponibilités du profil, question de séniorité de l'onboarding, mode « Skill growth », carte et graphiques de charge d'équipe | Servent à choisir entre coéquipiers |
| Inbox et notifications | Onglets Mentions et Assignments, colonne E-mail des notifications | Toujours vides quand on travaille seul ; pas de serveur de courrier |
| Intégrations | Tuiles GitHub (OAuth) et Slack, cartes de canaux, logos qui les annoncent | Impossibles à connecter dans l'app desktop |
| Visibilité | Public et Private sur les projets | N'a de sens qu'avec des collaborateurs |
| Panneaux | Status (santé du serveur, journal d'admin) ; usage de Cortex à fondre dans Réglages > AI | Parlent d'un serveur et d'un quota d'instance |
| Textes | Confidentialité et mentions légales, vocabulaire d'équipe de la visite et des agents, « Manage cookies » | Écrits pour la webapp hébergée |
| Copilot | Le proposer seulement une fois essayé | Jamais testé |
| Restes | `/[ws]/profile`, `/projects/[id]/members`, commentaires « Labs », libellés inutilisés, alias `TeamSwitcher`, pouces de Cortex sans effet, suggestions de Cortex écrites pour le dépôt de TaskForce, infobulle « Workflows IA » en français | Morts ou en double |
| Doublons à trancher | Deux listes de commandes (Ctrl+K et la recherche du tableau de bord) ; cycles à trois endroits, feuille de route à deux ; Pages des projets ou Brain OS | Un seul chemin par geste |

**Petits défauts** : « All my queues » ouvre l'onglet Issues ; l'entrée « Account » du menu ouvre le Profil ; un même
objet porte plusieurs noms (Inbox, Signals ; Projects, Operations ; Cycles, Sprints ; Analytics, Intelligence) ; les
demandes de validation n'ont pas d'onglet à elles dans l'Inbox.

## 4. Ce qui est cassé, à corriger quoi qu'il arrive

| Problème | Dans | Fiche |
| --- | --- | --- |
| La connexion MCP en un clic renvoie vers une mauvaise adresse | App desktop | PC-059 |
| GitHub et Slack en natif affichés mais impossibles à connecter | App desktop | PC-060 |
| L'alerte de surcharge tourne et renvoie vers des pages cachées | App desktop | PC-061 |
| Petits défauts d'interface (« All my queues », « Account », pouces de Cortex) | App desktop et webapp | PC-062 |

## 5. Ce que cet état des lieux ne dit pas

- Rien n'a été relancé : le Brain OS, Cortex et les connecteurs n'ont jamais été vérifiés dans l'app desktop, et cet audit
  ne l'a pas fait non plus.
- Les réglages de construction (`next.config.ts`, CI, variables) n'étaient pas dans l'instantané.
- Le code du service d'IA de la webapp (Python) n'était pas dans l'instantané.

## 6. Ce que la v2 doit fermer, pour le premier cas d'usage

1. **Importer des documents** (PDF, Word, Markdown, un dossier ou un coffre Obsidian) dans le Brain OS, découpés pour
   être cherchés en entier, avec leur **version**.
2. **Une recherche qui mêle** le sens et le texte exact, et qui renvoie la source précise (document, version, passage).
3. **Les règles en données**, avec le classement réversible ou irréversible (R1) et un propriétaire par règle (R2).
4. **Le bac à sable** (le workflow rejoué avec ses tests), puis la décision humaine pour ce qui en sort.
5. **Les outils de l'entreprise pour l'agent délégué**, à travers TaskForce, chaque appel tracé (R7').
6. **Le dossier de preuve** par mission, lisible et exportable (R9'), et la **carte de résultat** pour l'utilisateur.
7. Les quatre problèmes du §4.

---

**Dernière mise à jour :** 27/10/2026 · **v1.0**
