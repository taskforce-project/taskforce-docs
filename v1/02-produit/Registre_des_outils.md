---
id: produit-registre-outils
title: Registre des outils d'entreprise
doc_type: register
statut: active
version: 1.2
date: "12/11/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [produit, connecteurs, mcp, oauth, entreprise, j2]
related:
  - "./README.md"
  - "./Guide_de_branchement.md"
  - "./Backend.md"
  - "../13-roadmap/Roadmap_Backlog.md"
  - "../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md"
  - "../../recherche/decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Registre des outils d'entreprise

**Version :** 1.2 · **Date :** 12/11/2026 · **Auteur :** Pierre MICHEL

La liste des applications qu'une entreprise utilise le plus, et pour chacune la façon dont TaskForce peut s'y brancher. La
Présidence l'a demandée le 10/11/2026 : « je devrais pouvoir faire un listing exhaustif de l'ensemble des applications
Enterprise Grade qui sont les plus utilisées [...] on peut commencer par ça », pour « se plug partout, si possible ».

- **Le registre et le catalogue de l'app.** Depuis le 12/11/2026, l'app montre chaque outil du fichier des préréglages,
  essayé ou non (décision de la Présidence) ; `tried` y garde seulement la preuve d'un essai de bout en bout. Le registre
  dit tout ce qu'on sait de chaque outil, au catalogue ou non.
- **Les faits** ont été lus le 10/11/2026 sur les pages des éditeurs, des études et des normes ; un lien par ligne, celui
  de la contrainte qui compte. Une case suivie de `[HYPOTHÈSE]` n'est pas écrite sur une page lue.
- **Les seize outils de la première vague** ont été relus le 11/11/2026, avec leurs métadonnées OAuth publiques. Ce que la
  Présidence fait pour brancher chacun, et le détail des liens, est au [Guide de branchement](./Guide_de_branchement.md).
- **L'état chez nous** se lit dans la colonne de la vague (12/11/2026, PR [#523](https://github.com/taskforce-project/taskforce-fullstack/pull/523)) : « préréglage prêt, à essayer » veut dire que l'outil est dans le fichier des préréglages de TaskForce (`connectors/presets.json` : sa catégorie, son serveur, son chemin, les portées utiles, l'étape de l'administrateur, la classe de ses outils) et se connecte par le geste « Connect » ; il se montre dans l'app, et son essai de bout en bout se note `tried` dans le même fichier.
- **Le répertoire des connecteurs de Claude, relu le 12/11/2026** (PR [#527](https://github.com/taskforce-project/taskforce-fullstack/pull/527)) : la Présidence a demandé de reprendre
  ses connecteurs d'entreprise, ceux qu'Anthropic a revus (« regarde un peu ce que propose par exemple Claude en extension
  non communautaire [...] Et puis on fait la même »). Les outils qu'une entreprise de 10 à 500 personnes utilise sont entrés
  au catalogue, 71 de plus, 102 préréglages en tout. Leurs faits ont été lus le 12/11/2026 sur les pages des éditeurs et
  dans leurs métadonnées OAuth publiques (`/.well-known/oauth-protected-resource`, puis celles du serveur d'autorisation),
  sans connexion ni installation. « catalogue » dans la colonne de la vague : préréglage prêt, à essayer ; « fermé » :
  l'outil se montre avec la raison, sans le geste. Les outils laissés de côté, et pourquoi, sont en fin de registre.
- **Revue** : chaque trimestre, et à chaque outil essayé.

## Les chemins de connexion

Pour la personne, le geste est toujours le même : un clic, le navigateur s'ouvre, elle se connecte, elle revient dans
TaskForce, c'est branché. Derrière, quatre chemins, selon ce que l'éditeur permet :

| Chemin | Ce que c'est | Pour la personne | Pour nous |
| --- | --- | --- | --- |
| **A, l'auto-inscription** | Le serveur MCP officiel de l'éditeur laisse toute application s'inscrire seule (CIMD ou DCR, norme MCP du 28/07/2026) | Un clic | Rien à enregistrer chez l'éditeur |
| **B, notre application** | TaskForce s'enregistre chez l'éditeur, et passe sa revue quand il y en a une | Un clic | Un enregistrement par éditeur, parfois une revue de plusieurs semaines |
| **C, l'administrateur d'abord** | L'éditeur exige que l'administrateur de l'entreprise approuve ou crée l'application, une fois | Un clic, après l'administrateur | Un assistant qui guide l'administrateur |
| **D, à vérifier** | L'éditeur dit « tout client », sans dire comment s'inscrire | À essayer | Un essai avant de classer |
| **Aucun** | Pas de serveur MCP officiel ouvert à une application tierce | Une API, quand elle existe | Un lecteur déclaratif (R99) |

Un chemin suivi de « liste » : l'éditeur n'admet que les clients, ou les adresses de retour, de sa liste ; la Présidence le
lui demande une fois ([Guide de branchement](./Guide_de_branchement.md)). « Adresse de l'entreprise » : la personne colle
l'adresse du serveur que son entreprise tient chez l'éditeur, puis se connecte.

La vague, retenue par la Présidence le 11/11/2026 (R153) : **1** = J2, avec les outils où la Présidence peut se connecter,
**2** = la vague suivante, **plus tard** = à la demande d'un client.

## Le classement d'adoption

- **Okta, Businesses at Work 2026** (clients d'Okta, données du 01/11/2024 au 31/10/2025) : n°1 Microsoft 365, n°2 Google
  Workspace, n°3 AWS, n°4 Salesforce, n°5 Zoom, n°6 Slack, n°8 GitHub, n°11 Figma ; au Japon, n°5 Box, n°9 Notion ; 98
  applications par entreprise en moyenne, 83 en France
  ([Okta](https://www.okta.com/ja-jp/newsroom/press-releases/okta-businesses-at-work2026/)).
- **D'autres classements** recoupent le même noyau, avec Atlassian : Torii, octobre 2026
  ([Torii](https://www.toriihq.com/research/reports/adoption-index-october-2026.md)) ; Cledara, 2026
  ([Cledara](https://cledara.com/blog/50-most-popular-saas-tools-2026)) ; Zylo ([Zylo](https://zylo.com/blog/top-expensed-saas-applications)) ;
  Vertice, par dépense ([Vertice](https://www.vertice.one/insights/most-popular-saas-vendors-by-spend)) ; Ramp, janvier 2026
  ([Ramp](https://ramp.com/data/top-saas-vendors-on-ramp-january-2026)).

## Bureautique et stockage

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Google Drive (Docs, Sheets, Slides) | Okta n°2 (Workspace) | B | Pas d'auto-inscription : un projet Google Cloud, un client OAuth et son secret ; le serveur MCP de Drive est en Developer Preview, réservé aux membres du programme. La portée `drive.file` (les fichiers que la personne choisit ou que l'app crée) n'est pas sensible ; `drive.readonly` est restreinte : environ six semaines de vérification, un audit CASA par an, 100 personnes au plus en attendant. Construit le 12/11/2026 par l'API Drive, derrière la même connexion (PR [#528](https://github.com/taskforce-project/taskforce-fullstack/pull/528)) : notre client `TF_GOOGLE_*`, `drive.file` et le sélecteur de Google, la lecture citée, le rangement dans le dossier choisi | 1 (construit, à essayer) | [Google](https://developers.google.com/workspace/drive/api/guides/api-specific-auth) |
| SharePoint, OneDrive | Okta n°1 (Microsoft 365) | C | Pas d'auto-inscription chez Entra. La politique par défaut retire `Files.Read.All` et `Sites.Read.All` du consentement des personnes, pas `Files.Read` (ses propres fichiers) : l'administrateur approuve le reste ; la vérification d'éditeur évite un blocage chez les autres entreprises. Work IQ (MCP) ne sert que les comptes professionnels, en crédits Copilot. Construit le 12/11/2026 par Microsoft Graph (PR [#528](https://github.com/taskforce-project/taskforce-fullstack/pull/528)) : une connexion « Microsoft 365 » par personne, droits délégués, PKCE S256 admis pour les seuls émetteurs d'Entra, l'étape de l'administrateur sur AADSTS65001, 90094, 90095 ou 900941, la lecture citée, le rangement | 1 (construit, à essayer) | [Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies) |
| Box | Okta Japon n°5 | C | L'administrateur active l'intégration « Box MCP server » (Admin Console, Integrations), l'allume, choisit ses portées et l'adresse de retour, puis saisit son identifiant et son secret dans TaskForce ; Box Doc Gen demande Enterprise Advanced ; pas d'inscription dynamique dans les métadonnées | catalogue (préréglage prêt, à essayer) | [Box](https://developer.box.com/guides/box-mcp/remote/) |
| Dropbox | Cledara n°46 | B | L'inscription dynamique ne sert que les clients de confiance de Dropbox (Claude, ChatGPT, Cursor) : notre application Dropbox, ou celle de l'entreprise ; l'approbation de production dans les deux semaines après 50 personnes (10/11/2026) | catalogue (une étape de la Présidence ; préréglage prêt) | [Dropbox](https://help.dropbox.com/integrations/connect-dropbox-mcp-server) |
| Egnyte | non classé | D | Une clé limitée à un domaine de test jusqu'à l'approbation d'Egnyte | plus tard | [Egnyte](https://developers.egnyte.com/integration/cfs/api-docs/getting-started) |
| Nextcloud (auto-hébergé) | non classé | C | L'administrateur installe l'agent de contexte ; un mot de passe d'application, pas d'OAuth | plus tard | [Nextcloud](https://docs.nextcloud.com/server/latest/admin_manual/ai/app_context_agent.html) |
| Amazon S3 (stockage du serveur) | Okta n°3 (AWS) | C | Des droits IAM et la politique d'accès du serveur MCP d'AWS | stockage | [AWS](https://docs.aws.amazon.com/agent-toolkit/latest/userguide/getting-started-aws-mcp-server.html) |

## Savoir et documentation

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Notion | Okta Japon n°9 | A | Auto-inscription (DCR ou CIMD) et PKCE, aucune revue écrite ; le serveur se dit en bêta dans ses métadonnées ; l'espace Enterprise peut n'accepter que des clients approuvés ; la connexion tient 180 jours au plus | 1 (préréglage prêt, à essayer) | [Notion](https://developers.notion.com/guides/mcp/build-mcp-client) |
| Confluence | Torii n°3 (Atlassian) | A | Un seul serveur Atlassian, GA, pour Confluence et Jira ; l'organisation n'admet que les retours de sa liste : `127.0.0.1` et `localhost` par défaut, le domaine de l'app web s'ajoute par l'administrateur | 1 (préréglage prêt, à essayer) | [Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-rovo-mcp-server-domains/) |
| Guru | répertoire de Claude | A `[HYPOTHÈSE]` | Guru pré-approuve OAuth pour quelques applications, les autres peut-être sur demande ; un jeton d'API avec l'e-mail sinon | catalogue (préréglage prêt, à essayer) | [Guru](https://help.getguru.com/docs/connecting-gurus-mcp-server) |
| Glean | répertoire de Claude | A, adresse de l'entreprise | L'adresse du serveur vient du MCP Configurator de Glean ; OAuth avec inscription dynamique, sinon un client statique créé par l'administrateur ; MCP ouvert par défaut aux espaces éligibles | catalogue (préréglage prêt, à essayer) | [Glean](https://developers.glean.com/guides/mcp) |

## Tickets et projets

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Jira (et Jira Service Management) | Torii n°19 | A | Le serveur de Confluence ; supprimer et administrer restent coupés tant que l'administrateur ne les ouvre pas ; Jira Service Management par jeton d'API seulement | 1 (préréglage prêt, à essayer) | [Atlassian](https://github.com/atlassian/atlassian-mcp-server) |
| Linear | essayé dans TaskForce | A | Aucune revue ; DCR et CIMD ; une adresse en lecture seule | 1 (fait) | [Linear](https://linear.app/docs/mcp) |
| Asana | non classé | B ou C | Pas d'auto-inscription : une « MCP app » créée dans la console d'Asana, avec identifiant et secret, diffusée à des espaces choisis ou à tous ; toute portée autre que `default` est refusée | 1 (une étape ; préréglage prêt, à essayer) | [Asana](https://developers.asana.com/docs/integrating-with-asanas-mcp-server) |
| monday.com | non classé | A puis C | L'auto-inscription existe, mais chaque nouveau client attend l'administrateur du compte | 2 | [monday.com](https://developer.monday.com/api-reference/docs/mcp-dynamic-client-registration) |
| ClickUp | non classé | A `[HYPOTHÈSE]` | L'auto-inscription est annoncée, mais l'éditeur parle d'une liste de clients vérifiés | 2 | [ClickUp](https://clickup.com/blog/how-to-use-clickup-mcp-server/) |
| Smartsheet | non classé | D | Un jeton d'API (Bearer) ; Business, Enterprise ou Advanced Work Management ; des adresses à part pour l'UE et l'Australie ; l'OAuth de Smartsheet demande un secret et des retours HTTPS, sans inscription dynamique | catalogue (clé guidée ; préréglage prêt) | [Smartsheet](https://developers.smartsheet.com/ai-mcp/smartsheet/install-the-smartsheet-mcp-server) |
| Trello | non classé | A | Un serveur officiel, `mcp.trello.com/v1`, derrière l'OAuth d'Atlassian (CIMD et DCR) ; l'administrateur de l'organisation Atlassian règle les domaines admis et le niveau d'accès, comme pour Jira ; tous les plans `[TIERS]` | catalogue (préréglage prêt, à essayer) | [Atlassian](https://github.com/atlassian/trello-mcp-server) |
| Wrike | répertoire de Claude | C | Pas d'auto-inscription : l'administrateur crée une application OAuth, une fois, que les personnes réutilisent ; un jeton permanent pour les essais ; l'ancien point SSE s'arrête le 28/02/2027 | catalogue (préréglage prêt, à essayer) | [Wrike](https://developers.wrike.com/docs/wrike-mcp-server-overview) |
| Productboard | répertoire de Claude | A | Un administrateur ouvre MCP pour l'espace et choisit qui s'en sert (Settings, Integrations, MCP server) | catalogue (préréglage prêt, à essayer) | [Productboard](https://productboard.com/integrations/mcp-server) |
| Plane (serveur MCP) | intégré à TaskForce | A | Hors du répertoire de Claude, nommé par la Présidence : le serveur hébergé de Plane, OAuth avec inscription dynamique, Plane Cloud seulement ; l'intégration native par clé reste | catalogue (préréglage prêt, à essayer) | [Plane](https://docs.plane.so/ai/mcp-server) |

## Messagerie, mail et réunions

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Slack | Okta n°6 | B ou C | Le serveur MCP n'accepte que les applications publiées (revue jusqu'à dix semaines) ou internes à l'entreprise, avec identifiant et secret, sans auto-inscription, MCP allumé application par application ; les conditions interdisent l'entraînement d'un modèle et les copies durables des données d'autres organisations | 1 (l'application interne ; préréglage prêt, à essayer) | [Slack](https://docs.slack.dev/ai/slack-mcp-server/) |
| Microsoft Teams | Torii n°12 | C | Work IQ (MCP) : comptes professionnels seulement ; un administrateur global l'active avec une facturation à l'usage en crédits Copilot, et ses permissions demandent l'administrateur. Par Graph, `Chat.Read` hors du consentement par défaut. Construit le 12/11/2026 par Graph, sans Work IQ, sur la connexion « Microsoft 365 » (PR [#528](https://github.com/taskforce-project/taskforce-fullstack/pull/528)) : lire les canaux et les conversations de la personne, poster après l'accord d'une personne | 1 (construit, à essayer) | [Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/enable-work-iq) |
| Outlook | Torii n°18 | C | `Mail.Read` et `Calendars.Read` hors du consentement par défaut | 2 | [Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies) |
| Google Calendar | Okta n°2 (Workspace) | B | Des portées sans doute sensibles `[HYPOTHÈSE]` | 2 | [Google](https://developers.google.com/workspace/guides/configure-mcp-servers) |
| Gmail | Okta n°2 (Workspace) | B | `gmail.readonly` est restreinte : vérification et audit | plus tard | [Google](https://developers.google.com/workspace/gmail/api/auth/scopes) |
| Zoom | Okta n°5 | C | Inscription manuelle seulement : l'administrateur crée une General app (Develop, Build app) avec l'adresse de retour et les portées, puis la saisit dans TaskForce ; une application de TaskForce pour tous les comptes demanderait la revue de Zoom | catalogue (préréglage prêt, à essayer) | [Zoom](https://developers.zoom.us/docs/mcp/servers/connect-to-zoom-mcp-servers/) |
| Fireflies | répertoire de Claude | A | OAuth (CIMD et DCR) ou une clé d'API ; un compte actif | catalogue (préréglage prêt, à essayer) | [Fireflies](https://docs.fireflies.ai/getting-started/mcp-configuration) |
| Fathom | répertoire de Claude | A | OAuth (DCR), portée `mcp` ; le plan et un réglage de l'administrateur `[HYPOTHÈSE]` (seules les métadonnées ont été lues) | catalogue (préréglage prêt, à essayer) | [Fathom](https://api.fathom.ai/.well-known/oauth-authorization-server) |
| Granola | répertoire de Claude | A | Tout client OAuth ; en Enterprise, l'administrateur choisit les notes que MCP atteint ; « Make changes over MCP » se coupe pour lire seulement ; dossiers et transcriptions sur les plans payants | catalogue (préréglage prêt, à essayer) | [Granola](https://docs.granola.ai/help-center/sharing/integrations/mcp) |
| Otter.ai | répertoire de Claude | A | OAuth, portées de lecture seule ; le plan : Enterprise selon le centre d'aide, tous les plans selon le blog | catalogue (préréglage prêt, à essayer) | [Otter](https://help.otter.ai/hc/en-us/articles/35287607569687-Otter-MCP-Server) |
| tl;dv | répertoire de Claude | A | OAuth ; le serveur ne fait que lire (cinq outils, classés en lecture) ; Pro ou plus | catalogue (préréglage prêt, à essayer) | [tl;dv](https://tldv.io/blog/how-to-connect-meeting-notes-to-claude-with-mcp/) |
| Calendly | répertoire de Claude | A | Le client doit savoir l'inscription dynamique ; un identifiant de console ne marche pas ; lecture et écriture séparées | catalogue (préréglage prêt, à essayer) | [Calendly](https://developer.calendly.com/calendly-mcp-server) |

## Code et déploiement

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| GitHub | Okta n°8 | B | Déjà intégré (application OAuth ; GitHub CLI dans l'app desktop) ; les organisations récentes restreignent les applications OAuth : le propriétaire approuve ; le serveur MCP distant demande une application par hôte, ou un jeton | 1 (existant ; son serveur MCP en préréglage prêt, à essayer) | [GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/about-oauth-app-access-restrictions) |
| GitLab | Ramp n°5 (nouvelles dépenses) | A | GA depuis la 19.5, sur tous les plans ; l'auto-inscription crée une application sur l'instance ; l'accès MCP est ouvert par défaut aux groupes de premier niveau, sauf si un propriétaire l'a fermé ; en auto-hébergé, l'administrateur de l'instance l'ouvre | 1 (préréglage prêt, à essayer) | [GitLab](https://docs.gitlab.com/user/group/access_and_permissions/) |
| Bitbucket Cloud | non classé | A | L'espace doit être relié à une organisation Atlassian | 2 | [Atlassian](https://github.com/atlassian/atlassian-mcp-server) |
| Azure DevOps | non classé | C | Une application Entra avec le consentement de l'administrateur | plus tard | [Microsoft](https://learn.microsoft.com/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops) |
| Docker Hub | non classé | Aucun | Ajouté par la Présidence le 11/11/2026. Pas de serveur distant : le serveur officiel tourne sur le poste (stdio, ou HTTP local protégé par un jeton) et lit Docker Hub avec un jeton d'accès personnel, sans OAuth ; branchable sur l'app desktop seulement, par une adresse locale et un jeton copié | 1, en exception : un jeton copié sur l'app desktop (Présidence, 11/11/2026) ; le chemin d'un serveur local, accordé par la personne, est prêt | [Docker](https://github.com/docker/hub-mcp) |
| Vercel | répertoire de Claude | A (CIMD) | L'inscription dynamique est réservée aux clients que Vercel a revus ; un document de métadonnées client (CIMD) passe | catalogue (préréglage prêt, à essayer) | [Vercel](https://vercel.com/docs/agent-resources/vercel-mcp) |
| Cloudflare | répertoire de Claude | A | Le serveur de toute l'API (search, execute) ; la personne choisit les permissions à la connexion, ou colle un jeton d'API limité | catalogue (préréglage prêt, à essayer) | [Cloudflare](https://developers.cloudflare.com/agents/model-context-protocol/cloudflare/servers-for-cloudflare/) |
| Supabase | répertoire de Claude | A | Inscription dynamique ; `read_only=true` fait passer les requêtes par un rôle en lecture seule (l'adresse de lecture de TaskForce) ; `project_ref` borne à un projet | catalogue (préréglage prêt, à essayer) | [Supabase](https://supabase.com/docs/guides/ai-tools/mcp) |
| Neon | répertoire de Claude | A | L'adresse passe de l'ancien `/sse` à `/mcp` ; `?readonly=true` ou la portée de lecture | catalogue (préréglage prêt, à essayer) | [Neon](https://neon.com/docs/ai/neon-mcp-server) |
| Netlify | répertoire de Claude | A | OAuth (DCR) ; un jeton personnel pour le serveur local | catalogue (préréglage prêt, à essayer) | [Netlify](https://docs.netlify.com/build/build-with-ai/netlify-mcp-server/) |
| Render | répertoire de Claude | D | Une clé d'API (Bearer), qui ouvre tous les espaces du compte ; l'OAuth sert les extensions de Render seulement | catalogue (clé guidée ; préréglage prêt) | [Render](https://render.com/docs/mcp-server) |
| Railway | répertoire de Claude | A | OAuth ; la personne choisit ses espaces et projets ; annoncé en essai public le 17/04/2026 | catalogue (préréglage prêt, à essayer) | [Railway](https://docs.railway.com/ai/mcp-server) |
| CircleCI | répertoire de Claude | A | OAuth2 par défaut, un jeton personnel sinon | catalogue (préréglage prêt, à essayer) | [CircleCI](https://circleci.com/docs/guides/toolkit/connecting-to-the-circleci-mcp-server/) |
| Postman | répertoire de Claude | A | OAuth aux États-Unis ; l'UE par clé seulement (`mcp.eu.postman.com`) | catalogue (préréglage prêt, à essayer) | [Postman](https://learning.postman.com/docs/reference/postman-api/postman-mcp-server/postman-mcp-remote-server) |
| MongoDB Atlas | répertoire de Claude | A (CIMD) | L'accès des clients IA est fermé par défaut : un propriétaire de l'organisation l'ouvre, en lecture seule ou complet | catalogue (préréglage prêt, à essayer) | [MongoDB](https://www.mongodb.com/docs/mcp-server/remote-mcp/access-models/) |
| PlanetScale | répertoire de Claude | A | La personne choisit aucun accès, lecture seule ou complet ; un administrateur peut plafonner les requêtes | catalogue (préréglage prêt, à essayer) | [PlanetScale](https://planetscale.com/docs/mcp-server) |
| Jam | répertoire de Claude | A | OAuth ; portées `mcp:read` et `mcp:write` ; un jeton personnel par espace sinon | catalogue (préréglage prêt, à essayer) | [Jam](https://jam.dev/docs/debug-a-jam/mcp) |

## Supervision

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Sentry | répertoire de Claude | A | OAuth seulement ; l'adresse peut se borner à une organisation ou un projet ; aucune lecture seule documentée | catalogue (préréglage prêt, à essayer) | [Sentry](https://mcp.sentry.dev/) |
| Grafana Cloud | répertoire de Claude | A | Lire seulement : l'accès « Read », sans « Query » ni « Write » ; l'administrateur plafonne l'accès des clients enregistrés à la main ; écrire demande le rôle Assistant Admin | catalogue (préréglage prêt, à essayer) | [Grafana](https://grafana.com/docs/grafana-cloud/ai-tools/mcp-servers/cloud-mcp/) |
| Datadog | répertoire de Claude | A | Une adresse par site (`mcp.<site>/v1/mcp`, `mcp.datadoghq.eu/v1/mcp` en UE) ; l'administrateur admet l'adresse de retour (Organization Settings, MCP OAuth Redirect URLs) | catalogue (préréglage prêt, à essayer) | [Datadog](https://docs.datadoghq.com/mcp_server/setup/) |
| New Relic | répertoire de Claude | A | OAuth ; l'administrateur ouvre MCP dans le gestionnaire des fonctions (le serveur l'est par défaut) ; une adresse UE à part | catalogue (préréglage prêt, à essayer) | [New Relic](https://docs.newrelic.com/docs/agentic-ai/mcp/setup/) |
| Honeycomb | répertoire de Claude | A | Avec Honeycomb Intelligence, que l'équipe active ; lecture seule au choix à la connexion ; une adresse UE à part | catalogue (préréglage prêt, à essayer) | [Honeycomb](https://docs.honeycomb.io/integrations/mcp/configuration-guide) |
| PagerDuty | répertoire de Claude | C | Pas d'auto-inscription : une application PagerDuty (Scoped OAuth) créée par l'administrateur, ou un jeton d'API ; une adresse UE à part | catalogue (préréglage prêt, à essayer) | [PagerDuty](https://support.pagerduty.com/main/docs/pagerduty-mcp-server-integration-guide) |
| incident.io | répertoire de Claude | A | OAuth, PKCE sans secret ; la personne choisit lecture seule ou lecture et écriture ; reconnexion tous les 28 jours | catalogue (préréglage prêt, à essayer) | [incident.io](https://docs.incident.io/ai/remote-mcp) |
| Rootly | répertoire de Claude | A | OAuth depuis le 28/05/2026, un jeton d'API sinon ; l'ancien point SSE s'arrête après le 20/11/2026 | catalogue (préréglage prêt, à essayer) | [Rootly](https://docs.rootly.com/integrations/mcp-server) |
| Better Stack | répertoire de Claude | A | OAuth ou jeton d'API ; la lecture seule passe par une liste d'outils | catalogue (préréglage prêt, à essayer) | [Better Stack](https://betterstack.com/docs/ai-sre/mcp-server-comparison/) |

## Données et analyse

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Amplitude | répertoire de Claude | A | OAuth 2.0 seulement ; un serveur UE à part | catalogue (préréglage prêt, à essayer) | [Amplitude](https://amplitude.com/docs/amplitude-ai/amplitude-mcp) |
| Mixpanel | répertoire de Claude | A | OAuth, PKCE ; MCP ouvert d'office pour les comptes gratuits et Growth créés après le 01/08/2026, sinon l'administrateur l'ouvre (Settings, Org, AI Settings) ; adresses UE et Inde | catalogue (préréglage prêt, à essayer) | [Mixpanel](https://docs.mixpanel.com/docs/mcp) |
| PostHog | répertoire de Claude | A | OAuth ; `?readonly=true` retire les outils d'écriture (l'adresse de lecture de TaskForce) ; la région suit le compte | catalogue (préréglage prêt, à essayer) | [PostHog](https://posthog.com/docs/model-context-protocol/faq) |
| Hex | répertoire de Claude | A | OAuth par personne ; le rôle Explorer lit, modifier demande Editor | catalogue (préréglage prêt, à essayer) | [Hex](https://learn.hex.tech/docs/api-integrations/mcp-server) |
| Metabase | répertoire de Claude | A, adresse de l'entreprise | Une adresse par Metabase (`/api/metabase-mcp`) ; un serveur OAuth intégré ; l'administrateur ouvre MCP (Admin, AI, MCP) | catalogue (préréglage prêt, à essayer) | [Metabase](https://www.metabase.com/docs/latest/ai/mcp) |
| ChartMogul | répertoire de Claude | A | OAuth en lecture seule ; ouvert par défaut, l'administrateur peut le fermer | catalogue (préréglage prêt, à essayer) | [ChartMogul](https://help.chartmogul.com/article/348-chartmogul-mcp-server) |
| Supermetrics | répertoire de Claude | A | OAuth par personne ; dans les plans avec Data API ; une clé `api_*` sinon | catalogue (préréglage prêt, à essayer) | [Supermetrics](https://supermetrics.com/products/supermetrics-mcp) |
| Snowflake | répertoire de Claude | C, adresse de l'entreprise | Pas d'inscription dynamique : l'administrateur crée une intégration de sécurité OAuth, et le serveur porte l'adresse de son compte ; TaskForce ne prend pas encore les deux | catalogue, fermé | [Snowflake](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents-mcp) |
| Databricks | répertoire de Claude | C, adresse de l'entreprise | Pas d'inscription dynamique : une connexion d'application créée dans la console du compte, et l'adresse de l'espace ; TaskForce ne prend pas encore les deux | catalogue, fermé | [Databricks](https://docs.databricks.com/aws/en/generative-ai/mcp/connect-external-services) |

## Ventes, marketing et relation client

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Salesforce | Okta n°4 | C, adresse de l'entreprise | L'administrateur active chaque serveur et crée une External Client App (portées `mcp_api` et `refresh_token`, PKCE, jetons JWT) ; la création d'applications connectées est coupée par défaut depuis Spring '26 ; TaskForce ne prend pas encore l'application et l'adresse ensemble | catalogue, fermé | [Salesforce](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/create-external-client-app.html) |
| HubSpot | Cledara n°19 | B | Pas d'auto-inscription : une « MCP Auth App » (Development, MCP Auth Apps), identifiant et secret, PKCE obligatoire, adresse `mcp.hubspot.com` ; une application non listée s'installe 25 fois au plus (10/11/2026) | catalogue (une étape de la Présidence ; préréglage prêt) | [HubSpot](https://developers.hubspot.com/docs/apps/developer-platform/build-apps/integrate-with-the-remote-hubspot-mcp-server) |
| Pipedrive | non classé | A, liste | Un serveur ouvert à tout client, sur tous les plans ; l'inscription dynamique refuse une adresse de retour web tant que Pipedrive ne l'a pas admise (une adresse locale passe) | catalogue (une demande de la Présidence pour l'app web) | [Pipedrive](https://www.pipedrive.com/en/features/mcp-server) |
| Attio | répertoire de Claude | A | OAuth par personne | catalogue (préréglage prêt, à essayer) | [Attio](https://docs.attio.com/mcp/overview) |
| Close | répertoire de Claude | A | Trois portées : `mcp.read`, `mcp.write_safe`, `mcp.write_destructive` ; TaskForce ne demande pas la dernière | catalogue (préréglage prêt, à essayer) | [Close](https://help.close.com/docs/mcp-server) |
| Apollo.io | répertoire de Claude | A | OAuth, tous les plans ; l'enrichissement dépense des crédits ; la clé d'API agit comme le plus ancien administrateur, TaskForce ne la propose pas | catalogue (préréglage prêt, à essayer) | [Apollo](https://docs.apollo.io/docs/apollo-mcp) |
| Clay | répertoire de Claude | A | DCR et PKCE ; le rôle Viewer ne se connecte pas ; les crédits de l'espace | catalogue (préréglage prêt, à essayer) | [Clay](https://university.clay.com/docs/connect-to-clay-mcp) |
| ZoomInfo | répertoire de Claude | A | OAuth par personne ; le plan diffère selon les pages de l'éditeur (crédits de données, abonnement SalesOS ou Copilot) | catalogue (préréglage prêt, à essayer) | [ZoomInfo](https://pipeline.zoominfo.com/operations/zoominfo-mcp-server) |
| Gong | répertoire de Claude | A | Un administrateur technique crée une intégration MCP, à inscription automatique ou manuelle ; elle ne fait que lire (outils classés en lecture) ; un siège payant | catalogue (préréglage prêt, à essayer) | [Gong](https://help.gong.io/docs/enable-supported-ai-tools-for-gong) |
| Brevo | répertoire de Claude | D | Le serveur générique prend une clé d'API avec l'option MCP, qui a tous les droits du compte ; la connexion par navigateur sert les connecteurs de Brevo pour Claude et ChatGPT | catalogue (clé guidée ; préréglage prêt) | [Brevo](https://developers.brevo.com/docs/mcp-protocol) |
| Klaviyo | répertoire de Claude | A | OAuth (DCR) ; rôle Owner, Admin ou Manager ; `read-only=true` retire les écritures (l'adresse de lecture de TaskForce) | catalogue (préréglage prêt, à essayer) | [Klaviyo](https://developers.klaviyo.com/en/docs/connect_to_the_klaviyo_mcp_server) |
| Zoho CRM | non classé | C | Chaque entreprise crée son propre serveur MCP dans la console de Zoho, avec les outils choisis ; son URL vaut une clé (« Regenerate API Key ») ; ensuite OAuth 2.1, chaque personne avec son compte par défaut | 1 (une étape ; préréglage prêt, à essayer) | [Zoho](https://www.zoho.com/mail/help/mcp/mcp-server-configuration.html) |
| Dynamics 365 | non classé | C | L'administrateur active MCP et chaque client | plus tard | [Microsoft](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-disable) |
| Stripe | non classé | A | Ajouté par la Présidence le 11/11/2026 (« Stripe aussi important »). Auto-inscription (DCR), PKCE, révocation, portée `mcp` ; la personne choisit à la connexion ses comptes, réels ou de test, et leurs droits ; un administrateur peut couper MCP pour l'équipe ; déjà parmi les préréglages MCP de TaskForce | 1 (préréglage prêt, à essayer) | [Stripe](https://docs.stripe.com/mcp) |

## Support et services informatiques

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Intercom | Cledara n°36 | A, liste | Auto-inscription ; les retours locaux sur tout port, les autres sur demande à Intercom ; une adresse UE à part, pas d'Australie | catalogue (une demande de la Présidence pour l'app web) | [Intercom](https://developers.intercom.com/docs/guides/mcp) |
| Zendesk | Cledara n°37 | Aucun | Absent du répertoire de Claude le 12/11/2026 ; MCP annoncé le 19/05/2026, en accès anticipé ; l'API accepte PKCE, mais une application pour plusieurs clients demande un client global créé par Zendesk | 2 | [Zendesk](https://developer.zendesk.com/documentation/marketplace/building-a-marketplace-app/set-up-a-global-oauth-client/) |
| ServiceNow | Vertice n°8 | C | L'administrateur inscrit chaque client ; Now Assist requis | plus tard | [ServiceNow](https://www.servicenow.com/docs/r/platform-security/authentication/cimd-inbound-integration-workflow.html) |
| Freshworks (Freshdesk, Freshservice) | non classé | D | Freshdesk : une clé d'API ; Freshservice : une clé ou OAuth | plus tard | [Freshdesk](https://support.freshdesk.com/support/solutions/articles/50000012670) |

## Ressources humaines, finance et ERP

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| SAP | Vertice n°4 | Aucun | Pas de serveur hébergé par SAP ; le client le construit sur sa propre plateforme | plus tard | [SAP](https://developers.sap.com/tutorials/integration-suite-mcp-server/) |
| Workday | Vertice n°6 | C | Outils MCP en accès anticipé ; l'agent est inscrit par le client et passe par la passerelle de Workday | plus tard | [Workday](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/workday-agent-gateway-for-partner-agents.html) |
| Oracle NetSuite | Vertice n°9 (PME) | C puis D | L'administrateur active les fonctions et installe l'application ; ensuite « tout client », avec PKCE | plus tard | [Oracle](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_4160616848.html) |
| QuickBooks Online | Zylo n°4 | Aucun | Le serveur hébergé du répertoire de Claude répond 403, sans métadonnées OAuth publiques : réservé aux assistants partenaires d'Intuit `[HYPOTHÈSE]` ; un serveur local, avec un retour HTTPS public en production | laissé de côté | [Intuit](https://github.com/intuit/quickbooks-online-mcp-server) |
| Xero | Cledara n°10 | B | Le serveur documenté est `api.xero.com/mcp/v1` (le répertoire de Claude donne `mcp.xero.com`) ; une application PKCE sans secret, dans le portail de Xero ; les vraies organisations demandent le plan développeur Core ou plus ; les conditions interdisent d'entraîner une IA | catalogue (une étape de la Présidence ; préréglage prêt) | [Xero](https://developer.xero.com/documentation/guides/remote-mcp/overview/) |
| Odoo | non classé | Aucun | Une API par clé, réservée aux plans « Custom » | plus tard | [Odoo](https://www.odoo.com/pricing-plan) |
| PayPal | répertoire de Claude | A | OAuth par navigateur, ou les identifiants de l'application du compte ; un serveur de bac à sable à part | catalogue (préréglage prêt, à essayer) | [PayPal](https://developer.paypal.com/ai-tools/mcp-server/) |
| Square | répertoire de Claude | A, liste | Square n'admet que les clients de sa liste ; en bêta, la production seulement ; l'adresse passe de l'ancien `/sse` à `/mcp` | catalogue, fermé tant que TaskForce n'est pas sur la liste | [Square](https://developer.squareup.com/docs/mcp) |
| Ramp | répertoire de Claude | A | L'adresse documentée est `mcp.ramp.com/mcp` ; la personne choisit lecture seule ou accès complet ; l'administrateur limite qui se connecte | catalogue (préréglage prêt, à essayer) | [Ramp](https://support.ramp.com/ramp-mcp) |
| Brex | répertoire de Claude | A | Un administrateur accepte le contrat Developer API et ouvre la bêta ; chaque employé se connecte avec ses droits | catalogue (préréglage prêt, à essayer) | [Brex](https://developer.brex.com/docs/mcp) |
| Mercury | répertoire de Claude | A | Lire demande la portée `read`, chaque écriture la sienne ; paiements et virements s'approuvent dans Mercury, et TaskForce ne demande pas ces portées | catalogue (préréglage prêt, à essayer) | [Mercury](https://docs.mercury.com/docs/connecting-mercury-mcp) |
| Qonto | répertoire de Claude | A | Propriétaires, administrateurs et comptables d'office ; managers et employés après l'ouverture par un administrateur ; tous les plans | catalogue (préréglage prêt, à essayer) | [Qonto](https://docs.qonto.com/mcp/overview) |
| Expensify | répertoire de Claude | A | OAuth 2.1, PKCE ; tout membre ; lecture seule (portée `mcp:tools`, outils classés en lecture) | catalogue (préréglage prêt, à essayer) | [Expensify](https://help.expensify.com/articles/new-expensify/connections/connect-ai-assistants/Use-the-Expensify-MCP-Server-With-AI-Assistants) |
| FreshBooks | répertoire de Claude | A | La lecture d'abord (`mcp:all:read`) ; les écritures annoncées « bientôt » | catalogue (préréglage prêt, à essayer) | [FreshBooks](https://support.freshbooks.com/hc/en-us/articles/47907329443597) |
| Airwallex | répertoire de Claude | A | Seuls Owner, Admin et Finance Admin autorisent ; les portées se choisissent à l'autorisation | catalogue (préréglage prêt, à essayer) | [Airwallex](https://www.airwallex.com/docs/developer-tools/ai/agentos) |
| Deel | répertoire de Claude | A | OAuth2 avec DCR, ou un jeton personnel ; un compte avec l'accès API | catalogue (préréglage prêt, à essayer) | [Deel](https://developer.deel.com/mcp/introduction) |
| Gusto | répertoire de Claude | A | L'adresse générique est `mcp.api.gusto.com` ; seuls les administrateurs principaux ou complets se connectent | catalogue (préréglage prêt, à essayer) | [Gusto](https://gusto.com/product/integrations/gusto-mcp) |
| Remote | répertoire de Claude | A | PKCE, inscription dynamique, sans secret ; l'accès suit le rôle | catalogue (préréglage prêt, à essayer) | [Remote](https://developer.remote.com/docs/introduction-to-remote-mcp) |
| Greenhouse | répertoire de Claude | A | Le Site Admin choisit les portées (Dev Center, MCP Access), en lecture par défaut ; bêta ouverte, selon l'abonnement | catalogue (préréglage prêt, à essayer) | [Greenhouse](https://support.greenhouse.io/hc/en-us/articles/52096319906971-Set-up-Greenhouse-MCP-with-supported-AI-tools) |
| Workable | répertoire de Claude | A, liste | L'OAuth n'admet que les adresses de retour de sa liste : une demande au support ; tous les plans | catalogue, fermé tant que les adresses ne sont pas admises | [Workable](https://help.workable.com/hc/en-us/articles/39415735712407-Using-the-Workable-MCP-server-to-connect-to-AI-assistant) |

## Design et collaboration

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Figma | Okta n°11 | B | Seuls les clients du catalogue de Figma ; les nouveaux passent par une liste d'attente. Le serveur de l'app Figma (`127.0.0.1:3845`), sans connexion, demande un siège Dev ou Full sur un plan payant et n'écrit pas | hors de la vague 1 (liste d'attente, R153) ; le serveur local sur l'app desktop | [Figma](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation) |
| Canva | Zylo n°3 | B | Une application du Developer Portal (Canva MCP sous Outside Canva), identifiant et secret ; les clients sans secret passent par une liste d'attente ; deux adresses selon les pages | catalogue (une étape de la Présidence ; préréglage prêt) | [Canva](https://www.canva.dev/docs/mcp/troubleshooting/) |
| Miro | Cledara n°28 | A | DCR pour tout client ; en Enterprise, MCP parfois coupé jusqu'à l'administrateur | catalogue (préréglage prêt, à essayer) | [Miro](https://developers.miro.com/docs/miro-mcp-server-frequently-asked-questions) |
| Lucid | répertoire de Claude | A | OAuth ; un serveur en lecture seule (`/mcp/readonly`, l'adresse de lecture de TaskForce) ; en Team et Enterprise, l'administrateur ouvre MCP ; tous les comptes sauf FedRAMP | catalogue (préréglage prêt, à essayer) | [Lucid](https://help.lucid.co/hc/en-us/articles/42578801807508-Integrate-Lucid-with-AI-tools-using-the-Lucid-MCP-server) |
| Framer | répertoire de Claude | A | OAuth ; gratuit pendant l'aperçu | catalogue (préréglage prêt, à essayer) | [Framer](https://www.framer.com/help/articles/getting-started-with-framer-mcp/) |
| Webflow | répertoire de Claude | A | L'adresse passe de l'ancien `/sse` à `/mcp` ; inscription dynamique | catalogue (préréglage prêt, à essayer) | [Webflow](https://mcp.webflow.com/.well-known/oauth-authorization-server) |
| Wix | non classé | A | L'adresse passe de l'ancien `/sse` à `/mcp` ; inscription dynamique ; la page de Wix n'a pas été lue | catalogue (préréglage prêt, à essayer) | [Wix](https://mcp.wix.com/.well-known/oauth-authorization-server) |
| Contentful | répertoire de Claude | A | L'application MCP de Contentful s'installe dans chaque espace et environnement, avec des groupes d'outils en lecture seule ou lecture et écriture ; gratuit ; une adresse UE à part | catalogue (préréglage prêt, à essayer) | [Contentful](https://www.contentful.com/developers/docs/tools/mcp-server/) |
| Excalidraw | non classé | A | Ajouté par la Présidence le 11/11/2026. Serveur officiel public, sans compte ni OAuth ; ses dessins ne s'affichent que dans un client qui gère les MCP Apps ; un outil publie le dessin sur excalidraw.com | 1 (branchable, dessins non affichés ; préréglages Excalidraw et Excalidraw+ prêts, à essayer) | [Excalidraw](https://github.com/excalidraw/excalidraw-mcp) |

## Sécurité et conformité

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Vanta | répertoire de Claude | A | OAuth comme la personne ; tout utilisateur ; bêta publique depuis avril 2026 ; adresses UE et Australie à part | catalogue (préréglage prêt, à essayer) | [Vanta](https://developer.vanta.com/docs/vanta-mcp) |
| Drata | répertoire de Claude | A | L'administrateur crée une configuration OAuth MCP et ses portées (Settings, MCP Configuration) ; la personne a le recoupement de ces portées et de son rôle | catalogue (préréglage prêt, à essayer) | [Drata](https://help.drata.com/en/articles/13379899-mcp-setup) |

## Autres

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Airtable | Cledara n°49 | A | DCR ou un jeton personnel ; en Enterprise, une liste de clients par identifiant | catalogue (préréglage prêt, à essayer) | [Airtable](https://support.airtable.com/docs/using-the-airtable-mcp-server) |
| DocuSign | Torii n°20 | B | Une clé d'intégration (PKCE ou secret), à faire admettre par le formulaire MCP de Docusign pour la production ; une revue de mise en production de 24 à 48 h ; le Partner Program discuté `[HYPOTHÈSE]` | catalogue (une étape de la Présidence ; préréglage prêt) | [Docusign](https://developers.docusign.com/platform/mcp-server) |
| Zapier | répertoire de Claude | A | L'adresse `mcp.zapier.com/api/v1/connect` pour tout client ; OAuth, ou un jeton de connexion | catalogue (préréglage prêt, à essayer) | [Zapier](https://docs.zapier.com/mcp/get-started/connect) |
| Make | répertoire de Claude | A | OAuth borné à une organisation ; changer les scénarios demande un plan payant | catalogue (préréglage prêt, à essayer) | [Make](https://developers.make.com/mcp-server) |
| PandaDoc | répertoire de Claude | A | OAuth ; tous les plans, Free compris, pour un temps ; une adresse UE à part | catalogue (préréglage prêt, à essayer) | [PandaDoc](https://developers.pandadoc.com/docs/getting-started-with-mcp) |

## Laissés de côté le 12/11/2026

Vus dans le répertoire des connecteurs de Claude le 12/11/2026, et pas repris, chacun pour une raison :

- **Google et Microsoft** (Gmail, Google Calendar, BigQuery, Outlook, Teams, OneDrive, SharePoint) : le lot des fichiers, en
  cours (F) ; ils passent par les mêmes applications que Google Drive et Microsoft 365.
- **Mailchimp** : son connecteur est fait pour Claude et ChatGPT ; le serveur ouvert ne couvre que l'e-mail transactionnel de
  Mandrill.
- **QuickBooks** : le serveur hébergé répond 403 sans métadonnées OAuth publiques (ligne ci-dessus).
- **Adobe** : son connecteur créatif sert des assistants nommés ; l'accès des agents tiers à Creative Cloud est une bêta
  privée annoncée pour début 2027.
- **Shopify** : le serveur du répertoire (`setup.shopify.com`) n'a pas de page publique pour d'autres clients ; les serveurs
  documentés de Shopify servent les acheteurs et les développeurs d'applications.
- **Salesloft, Signeasy** : un ancien point SSE seulement, que le client de TaskForce ne parle pas.
- **Une adresse par compte ou par région, sans page lue ce jour** : Sprinto, Coralogix, Elastic Cloud, Pendo, ActiveCampaign,
  dbt, Freshservice, BambooHR, Chargebee. À reprendre à la demande d'un client.
- **Faits pour de grandes entreprises** : Adobe Workfront, ThoughtSpot, Sisense, Infor, MuleSoft, CloudBees, Workday (Sana),
  Darwinbox, Datarails, Contentsquare.
- **Couverts par un autre préréglage** : Zoho Projects, Zoho CRM, Zoho Desk, Zoho Books, Bigin et Vani (le serveur Zoho de
  l'entreprise) ; Loom et Bitbucket (le serveur d'Atlassian).
- **Outils de niche ou d'un seul métier** : Hive, Todoist, Astravue, Chaser (tâches) ; Grain, Circleback, Scriptivox
  (réunions) ; Omni, Coefficient, CorralData, Blaze SQL, Millentic, CData, Polar Analytics, Prophecy (données) ; Bronto, Reco,
  Pi Security, Have I Been Pwned (supervision et sécurité) ; Supersei, Salesflare, Nutshell, Affinity, Wealthbox, Reply.io,
  ClickFunnels, GrowSurf (ventes) ; Breezing, NumbersGame, stub, BillingMart, Pine Labs, freee, Rillet, Aleph, Meridian pour
  Xero (finance) ; Breezy HR, Windmill (RH) ; Juro, Ironclad, LinkSquares, Bloomberg Law, InfoTrack, NetDocuments,
  PaperOffice (juridique) ; Frontify, Subframe, Moda, Wonder, Orshot, Picsart, Tella, Brightcove, Bitmovin, BioRender, WeWeb
  (création) ; Bitrise, Control Plane, Stytch, QuickNode, Manufact (développement) ; RingCentral (téléphonie).
- **Données du dehors plutôt qu'outils de l'entreprise** : Similarweb, FactSet, Morningstar, D&B, Ramp Data, Coinversa.
- **Grand public ou personnels** : athletedata, Tineo, CarGurus, LegalZoom, Readwise, Configure Memory, Superhuman,
  Squarespace, WeTransfer.
- **Infrastructure pour agents** : Inkbox, AgentMail, Bird, Speko, OneSignal, Attentive, Pushwoosh, beehiiv, Migma, Resend,
  Chatbase, ElevenLabs, Duvo, CodeWords, Perspective AI, Spacefast.

## Ce qui vaut pour tous

- **La norme MCP du 28/07/2026** préfère l'inscription par document de métadonnées (CIMD) et rend l'inscription dynamique
  (DCR) dépréciée ; PKCE est obligatoire ; un client garde ses identifiants par émetteur
  ([MCP](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization/client-registration)).
- **Sur l'app desktop** : le navigateur du système, un retour sur `127.0.0.1`, PKCE S256, jamais de fenêtre intégrée
  ([RFC 8252](https://www.rfc-editor.org/rfc/rfc8252.html)). C'est déjà le chemin de la connexion à TaskForce.
- **Les conditions d'utilisation** peuvent interdire de copier ou d'entraîner : Slack interdit les copies durables et
  l'entraînement ([Slack](https://slack.com/terms-of-service/api)), Xero l'entraînement
  ([Xero](https://developer.xero.com/xero-developer-platform-terms-conditions)). Lire sans copier est le défaut (R155).
- **Aucune plateforme de connecteurs ouverte et neutre** n'a été trouvée : Nango est sous Elastic License 2.0 et son
  auto-hébergement gratuit ne couvre que l'authentification et le relais
  ([Nango](https://nango.dev/docs/guides/platform/self-hosting/self-hosting.md)) ; les autres sont commerciales ou réservent
  l'auto-hébergement à leur offre Enterprise.

## Ce qui n'a pas pu être vérifié

Le statut exact de plusieurs serveurs (Zendesk, Workday, ServiceNow, Pipedrive, QuickBooks hébergé) ; PKCE ou le retour
local chez Box, Notion (API), Atlassian (API), Bitbucket, ClickUp, Smartsheet, Miro (API), Pipedrive, Zoho, Intercom (API),
Egnyte et Dropbox ; les pages de Salesforce sur son serveur hébergé (accès refusé) ; la compatibilité de chaque licence avec
l'AGPL.

Pour la première vague, relue le 11/11/2026 :
- **Zoho** : si ses serveurs acceptent l'auto-inscription, et l'adresse de la console pour un compte européen ;
- **Slack** : le menu des réglages qui allume MCP (la propriété du manifeste est écrite par Slack, le menu seulement par des
  tiers), et si une application interne demande autre chose ;
- **Atlassian** : si la première connexion demande un administrateur du site, et le plan requis ;
- **GitLab** : si GitLab.com refuse une personne sans groupe, et si le passage de la 19.6 vaut déjà sur GitLab.com ;
- **Docker Hub** : le chemin HTTP et le jeton de la passerelle MCP de Docker, lus sur des pages tierces seulement ;
- **Excalidraw** : ce que `create_view` rend en texte à un client sans MCP Apps ;
- **Asana** : si une application de bureau peut se passer du secret ;
- **Microsoft** : si Work IQ demande une licence Microsoft 365 Copilot en plus des crédits ;
- **GitHub** : si l'application GitHub CLI demande l'approbation d'une organisation qui restreint ;
- **Stripe** : l'état par défaut de l'accès MCP d'une équipe ;
- **Figma** : si son auto-inscription, annoncée dans ses métadonnées, refuse un client hors du catalogue.

Pour les outils du répertoire de Claude, relus le 12/11/2026 :
- **les noms des outils** de presque tous : aucun éditeur ne les publie en entier ; chaque outil demande avant d'agir tant
  qu'il n'est pas classé, sauf les serveurs que l'éditeur dit en lecture seule (tl;dv, Gong, Expensify) ;
- **qu'une inscription dynamique annoncée admette un client inconnu** (Guru, Vercel, Pipedrive, ClickUp), et le retour local
  de l'app desktop chez HubSpot, Dropbox, Xero et Docusign ;
- **les plans** que Fathom, Netlify, CircleCI, Attio, Productboard, ZoomInfo et Otter.ai exigent (les pages se contredisent
  ou se taisent) ;
- **les adresses régionales** (UE de Datadog, New Relic, Honeycomb, PagerDuty, Amplitude, Mixpanel, Vanta, Contentful,
  PandaDoc, Postman, Smartsheet) : le préréglage porte l'adresse américaine, l'autre se branche par son adresse ;
- **Salesforce** : la page des clients MCP a refusé la lecture (403), l'adresse de ses serveurs vient d'un résumé de recherche ;
- **Fathom et Wix** : seules leurs métadonnées OAuth ont été lues.

---

**Points d'entrée :** [Produit](./README.md) · [Guide de branchement](./Guide_de_branchement.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [Séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)
