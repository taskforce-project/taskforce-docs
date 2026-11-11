---
id: produit-guide-branchement
title: Guide de branchement de la première vague
doc_type: runbook
statut: active
version: 1.0
date: "11/11/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [produit, connecteurs, mcp, oauth, entreprise, j2, guide]
related:
  - "./Registre_des_outils.md"
  - "./README.md"
  - "../13-roadmap/Roadmap_Backlog.md"
  - "../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md"
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Guide de branchement

**Version :** 1.0 · **Date :** 11/11/2026 · **Auteur :** Pierre MICHEL

Ce que la Présidence fait, outil par outil, pour brancher la première vague de J2 sur ses propres comptes (R153, R154,
TF-J2-12). Sa consigne du 11/11/2026 : « pas de pb si la personne doit gerer un truc de son cote sur les app microsoft ou
autre, c'est normal, mais faut que le flux soit clair, coherent et accessible ».

- **Les faits des éditeurs** : toutes les pages citées ont été lues le 11/11/2026, sauf la mention « lu le 10/11 » (le
  dossier de la [séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)). `[HYPOTHÈSE]` :
  écrit sur aucune page lue ; `[TIERS]` : lu sur une page qui n'est pas celle de l'éditeur ; `[DÉDUIT]` : tiré du code et
  d'une page, sans essai.
- **Les faits de TaskForce** viennent du code de `origin/dev` (78c168b2, 11/11/2026). La PR de K (`feat/connect-any-tool`)
  change la connexion : ce qu'elle doit fixer porte « à confirmer par la PR de K ».
- **Rien de secret ici** : un identifiant client, un secret ou un jeton se tape chez l'éditeur et dans TaskForce, jamais
  dans une note, un ticket ou un dépôt.
- L'adoption, le chemin et la vague de chaque outil sont au [Registre des outils](./Registre_des_outils.md).

## En bref

| Outil | Ce que fait la Présidence | État le 11/11/2026 |
| --- | --- | --- |
| Notion | Un clic | Prêt chez Notion |
| Linear | Un clic | Déjà essayé dans TaskForce |
| Stripe | Un clic | Prêt chez Stripe, préréglage de TaskForce pas encore essayé |
| GitLab | Un clic ; cocher l'accès MCP du groupe s'il a été fermé | Prêt chez GitLab |
| Confluence, Jira | Un clic sur l'app desktop ; sur l'app web, ajouter d'abord le domaine de TaskForce chez Atlassian | Prêt chez Atlassian |
| Excalidraw | Un clic, sans compte | Branchable, mais TaskForce n'affiche pas les dessins |
| GitHub | Rien de neuf ; approuver l'application pour l'organisation si elle restreint | Déjà branché (GitHub CLI sur l'app desktop) |
| Asana | Créer une application MCP chez Asana, une fois | Attend la PR de K (un client enregistré) |
| Slack | Créer une application interne avec MCP chez Slack, une fois | Attend la PR de K ; le Slack natif reste à l'app web |
| Zoho | Créer son serveur MCP chez Zoho, une fois, et copier son URL | Branchable par l'URL `[HYPOTHÈSE]` |
| Docker Hub | Lancer un serveur local et copier un jeton, sur l'app desktop seulement | Pas de serveur distant |
| Figma | Rien : TaskForce attend sur la liste de Figma ; sur l'app desktop, le serveur de l'app Figma (plan payant) | Bloqué (liste d'attente) |
| Teams | Rien dans ce lot | Bloqué : lot suivant, payant chez Microsoft |
| OneDrive | Rien dans ce lot | Lot suivant (fichiers) |
| Google Drive | Rien dans ce lot | Lot suivant (fichiers) |

## Ce qui vaut pour tous

### Le geste, dans TaskForce

1. Settings > Integrations (groupe « Workspace »).
2. La tuile de l'outil, ou « Connect an MCP server » et l'adresse du serveur donnée plus bas : l'app ne montre un outil
   qu'après son essai de bout en bout (R15, R153), et l'essai de la Présidence en fait partie.
3. « Connect with OAuth » : le navigateur s'ouvre chez l'éditeur, la Présidence s'y connecte et accepte, puis revient dans
   TaskForce.

Aujourd'hui, cette connexion ne marche que sur l'app web, et chez un éditeur qui accepte l'auto-inscription ; sinon
TaskForce répond « This server doesn't support dynamic client registration (DCR): one-click connection is unavailable,
connect it with a token instead. » (`McpOAuthService`). La PR de K ajoute l'app desktop, nos clients enregistrés et
l'application de l'entreprise.

### Les adresses de retour à déclarer

Seuls les éditeurs sans auto-inscription demandent qu'on leur déclare une adresse de retour : ici Asana et Slack, au lot
suivant Microsoft et Google.

- **App web** : `https://api.taskforce-project.fr/api/mcp/oauth/callback`. C'est la route `GET /api/mcp/oauth/callback` de
  `McpOAuthCallbackController`, sur la base `integrations.mcp.oauth.redirect-base`, soit `APP_API_URL` (à défaut `APP_URL`)
  en production ; le 11/11/2026, elle répond sur ce domaine par un renvoi vers l'app. À confirmer par la PR de K pour un
  client enregistré.
- **Serveur auto-hébergé** : `<APP_API_URL>/api/mcp/oauth/callback`.
- **App desktop** : un retour sur `127.0.0.1` avec PKCE (R154, [RFC 8252](https://www.rfc-editor.org/rfc/rfc8252.html), lu
  le 10/11), comme la connexion à TaskForce, qui écoute `http://127.0.0.1:<port>/callback` sur les ports 47812 à 47815
  (`desktop/src/account.ts`). Le profil desktop ne règle aujourd'hui aucune adresse de retour pour MCP, et son backend change
  de port à chaque lancement (`desktop/src/backend.ts`) : l'adresse exacte, avec un port fixe pour les éditeurs qui comparent
  l'adresse entière, est à confirmer par la PR de K.
- **GitHub et Slack natifs, sur l'app web** : `https://api.taskforce-project.fr/api/integrations/github/callback` et
  `https://api.taskforce-project.fr/api/integrations/slack/callback` (`IntegrationController`).

### Où va un identifiant client

- **Notre application** (chemin B) : l'identifiant client, et le secret si l'éditeur l'exige, dans une variable
  d'environnement par outil sur le serveur, jamais dans le dépôt, comme `GITHUB_CLIENT_ID` et `GITHUB_CLIENT_SECRET`,
  `SLACK_CLIENT_ID` et `SLACK_CLIENT_SECRET` aujourd'hui (`application-prod.yml`). Les noms des nouvelles variables sont à
  confirmer par la PR de K.
- **L'application de l'entreprise** (chemin C) : son administrateur tape l'identifiant et le secret une fois dans Settings >
  Integrations, où ils sont rangés chiffrés. Les champs sont à confirmer par la PR de K.
- Sur l'app desktop, aucun jeton ne passe par notre serveur (R154).

### Ce qu'elle verra

- **Aujourd'hui** : « Connected, N tool(s) available », puis « Run an action ». Une lecture passe seule ; une écriture
  attend l'accord d'un propriétaire ou d'un administrateur de l'espace.
- **Avec la PR de K** : l'état de chaque outil, « Connected as … », « Needs reconnecting », « Waiting for your admin » ou
  « Not connected », et si la connexion est la sienne ou celle de l'espace. Libellés à confirmer par la PR de K.

## Bureautique et stockage

### Google Drive

**Rien dans ce lot.** La PR de K laisse Google Drive au lot suivant (« fichiers : lire et ranger »), par l'API Drive plutôt
que par MCP.

- Pas d'auto-inscription : un projet Google Cloud, un client OAuth « Web application » et son secret ; le serveur MCP de
  Drive, `https://drivemcp.googleapis.com/mcp/v1`, est en Developer Preview, réservé aux membres du programme
  ([Google](https://developers.google.com/workspace/guides/configure-mcp-servers)).
- La portée `drive.file` (les fichiers que la personne ouvre avec l'app ou qu'elle crée) n'est pas sensible ;
  `drive.readonly` et `drive` sont restreintes : une vérification, et une évaluation de sécurité si les données passent par
  un serveur ([Google](https://developers.google.com/workspace/drive/api/guides/api-specific-auth)). R154 retient
  `drive.file`.
- Une application « External » en test : 100 testeurs au plus, et chaque autorisation expire au bout de sept jours
  ([Google](https://support.google.com/cloud/answer/15549945)).

Ce qu'elle fera au lot suivant `[HYPOTHÈSE]`, à confirmer par ce lot :
1. console.cloud.google.com : un projet, l'API Google Drive activée.
2. L'écran de consentement : l'audience « External », elle-même parmi les testeurs, la portée `drive.file`.
3. Un client OAuth, avec l'adresse de retour que donnera le lot suivant ; l'identifiant et le secret dans TaskForce, là où ce
   lot le dira.

### OneDrive (et SharePoint)

**Rien dans ce lot.** Laissé au lot suivant (« fichiers »), par Microsoft Graph.

- Microsoft Entra n'offre pas d'auto-inscription : ses métadonnées n'ont pas de `registration_endpoint`
  ([Entra](https://login.microsoftonline.com/organizations/v2.0/.well-known/openid-configuration)) ; il faut une application
  enregistrée dans Entra.
- Sur un compte professionnel, la politique de consentement par défaut laisse la personne accepter `Files.Read` (ses
  fichiers), mais retire `Files.Read.All` et `Sites.Read.All` : l'administrateur
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies)).
- Une application multilocataire dont l'éditeur n'est pas vérifié est bloquée au consentement des autres entreprises quand
  leur consentement par palier de risque est actif ; la vérification passe par le Microsoft AI Cloud Partner Program
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity-platform/publisher-verification-overview)). L'application de
  l'entreprise, enregistrée dans son propre locataire, échappe à ce blocage `[HYPOTHÈSE]`.
- Une adresse de retour `http://localhost` ignore le port ; `http://127.0.0.1` ne s'ajoute que par le manifeste de
  l'application ; avec les comptes personnels, aucun paramètre dans l'adresse
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity-platform/reply-url)).
- Work IQ, le serveur MCP de Microsoft 365, couvre OneDrive et SharePoint, mais pour les comptes professionnels seulement et
  en crédits Copilot (voir Teams).

Ce qu'elle fera au lot suivant `[HYPOTHÈSE]` :
1. entra.microsoft.com > App registrations > New registration : son organisation seulement, ou « tous les annuaires et les
   comptes Microsoft personnels » pour un OneDrive personnel.
2. Authentication : les adresses de retour du lot suivant (« Web » pour le serveur, « Mobile and desktop applications » pour
   l'app desktop).
3. API permissions > Microsoft Graph > Delegated : `Files.Read`, `offline_access`, `User.Read`.
4. L'identifiant de l'application, et un secret pour le serveur, dans TaskForce, là où le lot suivant le dira.

## Savoir et documentation

### Notion

**Un clic.** Notion accepte l'auto-inscription (RFC 7591) ou un document de métadonnées (CIMD), avec PKCE obligatoire, et
n'écrit aucune revue ([Notion](https://developers.notion.com/guides/mcp/build-mcp-client)) ; ses métadonnées disent
« Notion MCP (Beta) ».

1. TaskForce : Notion, ou « Connect an MCP server » avec `https://mcp.notion.com/mcp` ; « Connect with OAuth ».
2. Chez Notion : accepter.
3. Retour dans TaskForce : branché.

- **Si l'espace Notion est en Enterprise** et n'admet que des clients approuvés : son propriétaire approuve TaskForce dans
  Settings > Notion MCP > Manage workspace clients ([Notion](https://www.notion.com/help/notion-mcp)).
- La connexion tient 180 jours au plus, ou 30 jours sans usage ; ensuite, reconnecter
  ([Notion](https://developers.notion.com/guides/mcp/build-mcp-client)).

### Confluence

**Un clic sur l'app desktop ; une étape d'abord sur l'app web.** Un seul serveur Atlassian sert Confluence, Jira, Jira
Service Management et Bitbucket : `https://mcp.atlassian.com/v2/mcp`, « Generally Available »
([Atlassian](https://github.com/atlassian/atlassian-mcp-server)) ; il accepte l'auto-inscription et PKCE
([métadonnées](https://mcp.atlassian.com/.well-known/oauth-authorization-server)). L'organisation n'admet que les adresses de
retour de sa liste : par défaut `127.0.0.1` et `localhost`, et des domaines d'éditeurs connus, pas celui de TaskForce
([Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-rovo-mcp-server-domains/)) ;
sinon le consentement répond « Your organization admin must authorize access from this redirect URL »
([Atlassian](https://support.atlassian.com/rovo/kb/fix-oauth-consent-block-for-atlassian-rovo-mcp-server-in-atlassian-cloud/)).

1. **Sur l'app web seulement, une fois** : admin.atlassian.com, son organisation > Connectors > Atlassian MCP server >
   « Add domain » ([Atlassian](https://support.atlassian.com/security-and-access-policies/docs/control-atlassian-rovo-mcp-server-settings/) ;
   ailleurs écrit Rovo > Rovo MCP server > Domain settings) : `https://api.taskforce-project.fr/**` (un protocole, puis `/**`
   pour tout chemin : [Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-mcp-server-domains/)).
2. TaskForce : Jira, ou « Connect an MCP server » avec `https://mcp.atlassian.com/v2/mcp` ; « Connect with OAuth ».
3. Chez Atlassian : accepter l'accès au site.
4. Retour dans TaskForce : la même connexion sert Confluence et Jira `[DÉDUIT]` ; une tuile Confluence est à confirmer par
   la PR de K.

- Si le domaine manque, l'éditeur refuse ; TaskForce dira « Waiting for your admin », à confirmer par la PR de K.
- Les appels au Teamwork Graph (`searchAtlassian`, `getTeamworkGraphContext`) consomment des crédits Rovo
  ([Atlassian](https://support.atlassian.com/rovo/docs/getting-started-with-the-atlassian-remote-mcp-server/)).

## Tickets et projets

### Jira

**Comme Confluence** : le même serveur, la même étape sur l'app web. Supprimer et administrer (`delete_jira`, `manage_jira`)
restent coupés tant qu'un administrateur ne les ouvre pas ; Jira Service Management ne passe que par un jeton d'API
([Atlassian](https://github.com/atlassian/atlassian-mcp-server)).

### Linear

**Un clic, déjà essayé** (TF-MCP-02, la liste `TRIED` de `ConnectorCatalog`). Auto-inscription et CIMD, PKCE
([métadonnées](https://mcp.linear.app/.well-known/oauth-authorization-server)) ; une adresse en lecture seule existe,
`https://mcp.linear.app/mcp/readonly` ([Linear](https://linear.app/docs/mcp)).

1. TaskForce : Linear > « Connect with OAuth ».
2. Chez Linear : accepter.
3. Retour : branché. Sur l'app desktop, ce clic attend la PR de K.

### Asana

**Une étape de son côté, une fois.** Le serveur V2, `https://mcp.asana.com/v2/mcp`, refuse l'auto-inscription : il faut une
« MCP app » avec un identifiant et un secret ; aucune portée à demander, toute autre que `default` est refusée
([Asana](https://developers.asana.com/docs/integrating-with-asanas-mcp-server), page du 08/10/2026). Son serveur
d'autorisation n'admet qu'un client avec secret (métadonnées de `app.asana.com`).

1. `https://app.asana.com/0/my-apps` > « Create new app » : un nom, le type « MCP app », « Create app ».
2. L'adresse de retour (« Redirect URL ») : sur l'app web, `https://api.taskforce-project.fr/api/mcp/oauth/callback` ; sur
   l'app desktop, celle de la PR de K.
3. « Manage distribution » : « Specific workspaces » et son espace pour l'application de l'entreprise, ou « Any workspace »
   pour l'application de TaskForce.
4. L'identifiant client et le secret dans TaskForce : Settings > Integrations > Asana (l'application de l'entreprise), ou
   les variables d'environnement d'Asana sur le serveur (notre application) ; à confirmer par la PR de K.
5. TaskForce : Asana > « Connect with OAuth » ; chez Asana, accepter ; retour.

- Sans la PR de K, TaskForce refuse : pas d'inscription automatique.

## Messagerie, mail et réunions

### Slack

**Une étape de son côté, une fois.** Le serveur MCP de Slack, `https://mcp.slack.com/mcp`, n'accepte que les applications
publiées dans son annuaire ou internes à l'entreprise ; OAuth avec identifiant et secret, PKCE pour les clients de bureau,
pas d'auto-inscription ; les administrateurs de l'espace approuvent et gèrent les clients MCP
([Slack](https://docs.slack.dev/ai/slack-mcp-server/)). Publier dans l'annuaire demande une revue de dix semaines au plus (lu
le 10/11, [Slack](https://docs.slack.dev/slack-marketplace/slack-marketplace-review-guide)) : pour l'essai, une application
interne à son espace.

1. `https://api.slack.com/apps` > « Create New App » : un nom, son espace.
2. Allumer MCP : dans le manifeste de l'application, `is_mcp_enabled: true` sous `settings`
   ([Slack](https://slack.dev/slack-developer-changelog-recap-april-june-2026/)).
3. OAuth & Permissions : l'adresse de retour (sur l'app web,
   `https://api.taskforce-project.fr/api/mcp/oauth/callback` ; sur l'app desktop, celle de la PR de K) et les portées de
   l'utilisateur pour lire : `search:read.public`, `search:read.private`, `search:read.im`, `search:read.mpim`,
   `search:read.files`, `files:read`, `channels:history`, `groups:history`, `im:history`, `mpim:history`, `channels:read`,
   `groups:read`, `im:read`, `mpim:read`, `users:read` ([Slack](https://docs.slack.dev/ai/slack-mcp-server/)). La liste
   exacte est à confirmer par la PR de K (R158 : la lecture par défaut).
4. Ne pas activer la distribution publique : l'application reste interne `[HYPOTHÈSE]`.
5. Basic Information > App Credentials : l'identifiant client et le secret dans TaskForce, Settings > Integrations > Slack
   (l'application de l'entreprise), à confirmer par la PR de K.
6. TaskForce : « Connect with OAuth » ; chez Slack, accepter ; retour.

- **Le Slack natif** (les notifications des tickets, l'historique des canaux) reste à l'app web : « Connect », l'application
  Slack de TaskForce s'installe, retour. Le serveur lit `SLACK_CLIENT_ID` et `SLACK_CLIENT_SECRET` ; l'application déclare
  l'adresse native ci-dessus et les portées du robot `chat:write`, `chat:write.public`, `channels:read`, `channels:history`,
  `users:read`, `incoming-webhook` (`SlackIntegrationService`) ; configuré en production `[HYPOTHÈSE]`. Sur l'app desktop :
  « Web app only ».
- Les conditions de Slack interdisent l'entraînement d'un modèle et les copies durables des données d'autres organisations
  (lu le 10/11, [Slack](https://slack.com/terms-of-service/api)) : TaskForce lit en direct (R155).

### Microsoft Teams

**Bloqué dans ce lot** : la PR de K le laisse au lot suivant, et le chemin de Microsoft coûte.

- Work IQ, le serveur MCP de Microsoft 365, `https://workiq.svc.cloud.microsoft/mcp`, lit et écrit le mail, l'agenda, les
  discussions Teams, OneDrive et SharePoint ([Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/mcp/overview)) ;
  ses métadonnées renvoient à `login.microsoftonline.com/organizations`, donc aux seuls comptes professionnels `[DÉDUIT]`.
- Ses trois permissions demandent le consentement de l'administrateur
  ([Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/permissions)) ; il se paie à
  l'usage, en crédits Copilot ([Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/api-overview)) ;
  un administrateur global l'active une fois, avec un plan de facturation à l'usage dans Copilot Studio relié à un
  abonnement Azure ([Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/enable-work-iq)).
- Par Microsoft Graph, `Chat.Read` est retiré du consentement par défaut : l'administrateur
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies)).

Ce qu'elle fera, quand le lot suivant le construira `[HYPOTHÈSE]` :
1. Dans son locataire Microsoft 365 : enregistrer l'application comme pour OneDrive, avec la permission déléguée de Work IQ
   (`WorkIQ.Read`) ou de Graph (`Chat.Read`), puis « Grant admin consent ».
2. Pour Work IQ seulement : en administrateur global, activer Work IQ et lui relier un plan de facturation.
3. L'identifiant de l'application dans TaskForce, là où le lot suivant le dira.

Avec un compte Microsoft personnel, Work IQ ne sert pas : il ne connaît que les comptes professionnels `[DÉDUIT]`.

## Code

### GitHub

**Déjà branché** : GitHub est une intégration native de TaskForce, pas un serveur MCP.

1. TaskForce : Settings > Integrations > GitHub. Sur l'app desktop, se connecter avec GitHub CLI (un code à usage unique
   dans le navigateur, comme `gh auth login`) ; la connexion reste dans le trousseau du système. Sur l'app web,
   « Connect » : GitHub demande `repo` et `read:org`.
2. Si son organisation restreint les applications OAuth, ce que font par défaut les organisations récentes
   ([GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/about-oauth-app-access-restrictions)),
   en propriétaire : Organizations > l'organisation > Settings > Third-party Access > OAuth app policy > « Review » à côté de
   l'application > « Grant access » ([GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/approving-oauth-apps-for-your-organization)).
   Sur l'app desktop, l'application à approuver est GitHub CLI `[HYPOTHÈSE]`.
3. Elle verra « Connected with GitHub CLI on this computer, as … » sur l'app desktop, « GitHub is connected for this
   workspace. » sur l'app web.

- Sur l'app web, le serveur lit `GITHUB_CLIENT_ID` et `GITHUB_CLIENT_SECRET`, et l'application OAuth déclare l'adresse
  native ci-dessus (`GitHubIntegrationService`) ; configurée en production `[HYPOTHÈSE]`.
- Le serveur MCP distant de GitHub, `https://api.githubcopilot.com/mcp/`, demande que chaque hôte configure sa propre
  application GitHub ou OAuth, ou un jeton personnel ([GitHub](https://github.com/github/github-mcp-server)) : inutile pour
  la vague, l'intégration native suffit.

### GitLab

**Un clic** ; une case à cocher si l'accès a été fermé. Le serveur, `https://gitlab.com/api/v4/mcp` (ou
`https://<instance>/api/v4/mcp`), est « Generally available » depuis la 19.5, sur les plans Free, Premium et Ultimate ; à la
première connexion, l'auto-inscription crée une application OAuth sur l'instance, avec la portée `mcp`
([GitLab](https://docs.gitlab.com/user/gitlab_duo/model_context_protocol/mcp_server/)).

1. TaskForce : « Connect an MCP server » avec `https://gitlab.com/api/v4/mcp` ; « Connect with OAuth ».
2. Chez GitLab : autoriser ; retour.
3. Si GitLab répond « MCP server not enabled for any of your groups »
   ([GitLab](https://docs.gitlab.com/user/model_context_protocol/mcp_server_troubleshooting/)) : en propriétaire d'un groupe
   de premier niveau, Settings > General > Permissions and group features > MCP client access > « Allow connection to
   GitLab » > « Save changes ». L'accès est ouvert par défaut depuis la 19.5 pour les nouveaux groupes et depuis la 19.6 pour
   les autres, sauf si un propriétaire l'a fermé ([GitLab](https://docs.gitlab.com/user/group/access_and_permissions/)).

- En auto-hébergé : l'administrateur de l'instance ouvre MCP ; s'il a coupé l'auto-inscription, une application OAuth
  pré-enregistrée (portée `mcp`, non confidentielle, adresse de retour exacte), dont l'identifiant va dans TaskForce, à
  confirmer par la PR de K.
- TaskForce ne demandera que `mcp` : il lit d'abord les portées du serveur MCP (`McpOAuthDiscovery`), et celui de GitLab
  n'annonce que celle-là (ses métadonnées).

### Docker Hub

**Pas de serveur distant.** Le serveur officiel, `docker/hub-mcp`, tourne sur le poste : en stdio par défaut, ou en HTTP sur
`127.0.0.1` avec un jeton porteur ; il lit Docker Hub avec un jeton d'accès personnel ; il n'a ni OAuth ni adresse distante
([GitHub](https://github.com/docker/hub-mcp)). Docker Desktop l'installe par son MCP Toolkit
([Docker](https://docs.docker.com/ai/mcp-catalog-and-toolkit/hub-mcp/)). TaskForce ne parle que le HTTP « Streamable », pas
le stdio (`McpClient`) ; sur l'app desktop, il admet une adresse locale pour une connexion par jeton
(`allow-private-network: true`), jamais par OAuth.

Sur l'app desktop seulement, si elle veut l'essayer (la clé guidée, dernier recours de R154) :
1. Docker Hub : un jeton d'accès personnel, en lecture seule si Docker Hub le propose `[HYPOTHÈSE]`.
2. Docker Desktop > MCP Toolkit > Catalog : « Docker Hub » > ajouter, avec son identifiant et ce jeton
   ([Docker](https://docs.docker.com/ai/mcp-catalog-and-toolkit/hub-mcp/)).
3. Un terminal : `docker mcp gateway run --transport streaming --port 8811`
   ([GitHub](https://github.com/docker/mcp-gateway)), avec un jeton de passerelle qu'elle choisit dans
   `MCP_GATEWAY_AUTH_TOKEN`, sinon la passerelle en tire un nouveau à chaque lancement `[TIERS]`
   ([DEV](https://dev.to/udondan/running-docker-mcp-gateway-on-linux-without-docker-desktop-4da2)).
4. TaskForce (app desktop) : « Connect an MCP server » > `http://127.0.0.1:8811/mcp` `[HYPOTHÈSE]` > « Use a token instead » >
   « Authorization: Bearer » > le jeton de la passerelle > « Connect ».

- Ce chemin fait copier un jeton : il ne tient pas le premier critère de J2 (« sans copier de jeton »). Proposition :
  Docker Hub reste hors du clic tant que Docker n'offre pas de serveur distant ; à trancher par la Présidence.

## Ventes et relation client

### Zoho (Zoho CRM et les autres applications)

**Une étape de son côté, une fois** : chaque entreprise crée son propre serveur MCP chez Zoho, avec les outils qu'elle
choisit.

1. La console Zoho MCP, `https://mcp.zoho.com` (pour un compte européen, `https://mcp.zoho.eu` `[HYPOTHÈSE]`) > « Create MCP
   Server » : un nom ([Zoho](https://help.zoho.com/portal/en/kb/mcp/implementation-guide/articles/zoho-mcp-implementation-guide)).
2. Tools > « Add Tools » : Zoho CRM, cocher les outils de lecture, « Add Now » (même page).
3. Garder « Authorization on Demand » : chaque personne s'y connecte avec son propre compte. « Authorization via
   Connection » ferait passer toute l'équipe par le compte d'un Super Admin
   ([Zoho](https://www.zoho.com/mail/help/mcp/mcp-server-configuration.html)), contraire à une connexion par personne
   (R154).
4. Connect : copier l'URL du serveur. Elle vaut une clé, puisque « Regenerate API Key » en donne une nouvelle (même page) :
   la traiter comme un mot de passe.
5. TaskForce : « Connect an MCP server » > cette URL > « Connect with OAuth » ; chez Zoho, « Allow » ; retour. Si TaskForce
   refuse faute d'auto-inscription : « Use a token instead », sans jeton, puis « Connect » `[HYPOTHÈSE]`.

- Copier une URL qui vaut une clé touche au signal d'arrêt de R154 ; c'est le modèle de Zoho.

### Stripe

**Un clic.** Le serveur, `https://mcp.stripe.com`, suit l'OAuth de la norme MCP du 28/07/2026
([Stripe](https://docs.stripe.com/mcp)) : auto-inscription, client public, PKCE, révocation, portée `mcp`
([métadonnées](https://access.stripe.com/.well-known/oauth-authorization-server/mcp)). Il est déjà parmi les préréglages
de TaskForce (`ConnectorCatalog`), pas encore essayé.

1. TaskForce : « Connect an MCP server » > `https://mcp.stripe.com` > « Connect with OAuth ».
2. Chez Stripe : choisir le ou les comptes, un environnement de test d'abord, et les droits de chacun ; accepter
   ([Stripe](https://docs.stripe.com/mcp)).
3. Retour : branché.

- Si Stripe refuse : un administrateur ouvre l'accès MCP de l'équipe, Dashboard > Settings > MCP and CLI access, à part pour
  le mode réel et pour le test (même page).
- Révoquer chez Stripe : les paramètres de l'utilisateur > OAuth sessions > « Revoke access » (même page). La révocation
  depuis TaskForce est à confirmer par la PR de K.
- R158 : `stripe_api_write` écrit par toute méthode POST, PATCH, PUT ou DELETE, et certains gestes (un remboursement, un
  envoi d'argent) demandent en plus une confirmation dans le Dashboard (même page) ; TaskForce le classe en écriture, à
  confirmer par la PR de K.
- À partir de décembre 2026, Stripe MCP refuse les clés secrètes complètes et les clés restreintes sans l'étiquette
  « Agent » (même page) : OAuth évite la question.

## Design et collaboration

### Figma

**Bloqué pour le serveur distant ; un contournement sur l'app desktop.**

- Le serveur distant, `https://mcp.figma.com/mcp`, n'admet que les clients de son catalogue ; un nouveau client attend sur
  une liste, par un formulaire ([Figma](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation)).
  Inscrire TaskForce sur cette liste est un geste de la Présidence.
- Le serveur de l'app Figma, `http://127.0.0.1:3845/mcp`, ne demande pas de connexion ; il exige un siège Dev ou Full sur
  un plan Professional, Education, Organization, Government ou Enterprise, et n'écrit pas dans le canevas
  ([Figma](https://developers.figma.com/docs/figma-mcp-server/local-server-installation)).

Sur l'app desktop, avec un plan payant :
1. L'app Figma (bureau) : ouvrir un fichier de design, passer en Dev Mode sans rien sélectionner, puis, dans le volet de
   droite, section MCP server, « Enable desktop MCP server » (même page).
2. TaskForce (app desktop) : « Connect an MCP server » > `http://127.0.0.1:3845/mcp` > « Use a token instead », sans jeton >
   « Connect ».
3. Elle verra « Connected, N tool(s) available », tant que l'app Figma tourne `[HYPOTHÈSE]`.

- R153 : un outil bloqué par son éditeur sort de la vague, la raison au registre.

### Excalidraw

**Un clic, sans compte.** Le serveur officiel (organisation Excalidraw, licence MIT), `https://mcp.excalidraw.com`, « Works
with any client that supports MCP Apps » ([GitHub](https://github.com/excalidraw/excalidraw-mcp)). Sondé le 11/11/2026
sans compte (`initialize`, `tools/list`) : `https://mcp.excalidraw.com/mcp` répond sans jeton, n'annonce pas d'OAuth, et
offre cinq outils, `read_me`, `create_view` (le dessin, dans une vue des MCP Apps), `export_to_excalidraw` (envoie le
dessin sur excalidraw.com et rend un lien de partage), `save_checkpoint` et `read_checkpoint`.

1. TaskForce : « Connect an MCP server » > `https://mcp.excalidraw.com/mcp` > « Use a token instead », sans jeton >
   « Connect ».
2. Elle verra « Connected, 5 tool(s) available ». Rien à faire chez Excalidraw.

- Limite : le client MCP de TaskForce ne lit que du texte, ni ressources ni MCP Apps (`McpClient`) ; il appelle les outils
  sans afficher le dessin `[DÉDUIT]`.
- R158 : `export_to_excalidraw` publie au-dehors, par un lien ; TaskForce doit le classer en écriture, quoi que déclare le
  serveur, à confirmer par la PR de K.

## Ce que la PR de K doit confirmer

1. L'adresse de retour d'un client enregistré (aujourd'hui `/api/mcp/oauth/callback`) et celle de l'app desktop, avec son
   port.
2. Les noms des variables d'environnement par outil, et les champs de l'application de l'entreprise dans Settings.
3. Les libellés des états, et l'endroit où se branche un outil pas encore essayé.
4. Les portées demandées : aujourd'hui toutes celles qu'annonce le serveur, `read` et `write` chez Linear par exemple.
5. La classe des outils qui écrivent ou publient, comme `stripe_api_write` et `export_to_excalidraw`.
6. Une tuile Confluence sur le serveur d'Atlassian.
7. Pour Microsoft, au lot suivant : les métadonnées d'Entra n'annoncent pas `code_challenge_methods_supported`
   ([Entra](https://login.microsoftonline.com/organizations/v2.0/.well-known/openid-configuration)), alors que la norme MCP
   veut qu'un client refuse un serveur qui ne l'annonce pas (lu le 10/11,
   [MCP](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization/security-considerations)).

Ce qui n'a pas pu être vérifié est au [Registre des outils](./Registre_des_outils.md#ce-qui-na-pas-pu-être-vérifié).

---

**Points d'entrée :** [Registre des outils](./Registre_des_outils.md) · [Produit](./README.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [Séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)
