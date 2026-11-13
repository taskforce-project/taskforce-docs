---
id: produit-guide-branchement
title: Guide de branchement de la première vague
doc_type: runbook
statut: active
version: 1.3
date: "12/11/2026"
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

**Version :** 1.3 · **Date :** 12/11/2026 · **Auteur :** Pierre MICHEL

> **Avant l'essai, une release.** Les deux lots de J2 en cours, la connexion aux outils (PR
> [#523](https://github.com/taskforce-project/taskforce-fullstack/pull/523)) et les règles par couches (PR
> [#522](https://github.com/taskforce-project/taskforce-fullstack/pull/522)), doivent être en production, avec une nouvelle
> version de l'app desktop : l'API hébergée publie le document de métadonnées client de l'app desktop, et la coque de la
> nouvelle version reçoit le retour du navigateur sur `127.0.0.1`.

Ce que la Présidence fait, outil par outil, pour brancher la première vague de J2 sur ses propres comptes (R153, R154,
TF-J2-12). Sa consigne du 11/11/2026 : « pas de pb si la personne doit gerer un truc de son cote sur les app microsoft ou
autre, c'est normal, mais faut que le flux soit clair, coherent et accessible ».

- **Les faits des éditeurs** : les pages citées ont été lues le 11/11/2026, celles d'Excalidraw+ le 12/11/2026, sauf la
  mention « lu le 10/11 » (le dossier de la [séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)).
  `[HYPOTHÈSE]` : écrit sur aucune page lue ; `[TIERS]` : lu sur une page qui n'est pas celle de l'éditeur ; `[DÉDUIT]` :
  tiré du code et d'une page, sans essai.
- **Les faits de TaskForce** viennent du code de la PR #523, fusionnée dans `dev` le 12/11/2026 (`7182e856`) : le fichier
  des préréglages `backend/tf-api/src/main/resources/connectors/presets.json`, l'écran
  `frontend/components/integrations/connect-panel.tsx`, les textes de `frontend/lib/constants_en.ts`. Ce que K n'a pas pu
  essayer sans les comptes de la Présidence porte « non vérifié ».
- **Rien de secret ici** : un identifiant client, un secret ou un jeton se tape chez l'éditeur et dans TaskForce, jamais
  dans une note, un ticket ou un dépôt.
- L'adoption, le chemin et la vague de chaque outil sont au [Registre des outils](./Registre_des_outils.md).

## En bref

| Outil | Ce que fait la Présidence | Dans TaskForce |
| --- | --- | --- |
| Notion | Un clic | Préréglage prêt, à essayer |
| Linear | Un clic | Essayé, le seul préréglage qui porte `tried` |
| Stripe | Un clic ; ouvrir l'accès MCP de l'équipe s'il est fermé | Préréglage prêt, à essayer |
| GitLab | Un clic ; cocher l'accès MCP du groupe s'il a été fermé | Préréglage prêt, à essayer |
| Confluence, Jira | Deux connexions, un clic chacune ; sur l'app web, ajouter d'abord le domaine de TaskForce chez Atlassian | Préréglages prêts, à essayer |
| Excalidraw | Un clic, sans compte | Préréglage prêt ; TaskForce n'affiche pas les dessins |
| Excalidraw+ | Créer une clé MCP personnelle et la coller | Préréglage prêt, à essayer |
| GitHub | Rien pour l'intégration native ; pour ses outils MCP, coller un jeton fin ou enregistrer une application OAuth | Native inchangée ; préréglage MCP prêt, à essayer |
| Asana | Créer une « MCP app » chez Asana, une fois, puis saisir son identifiant et son secret | Préréglage prêt, à essayer |
| Slack | Créer une application interne avec MCP, une fois, puis saisir son identifiant et son secret | Préréglage prêt, à essayer ; le Slack natif reste à l'app web |
| Zoho | Créer son serveur MCP chez Zoho, une fois, puis coller son adresse | Préréglage prêt, à essayer |
| Docker Hub | L'exception de la Présidence : lancer la passerelle de Docker et copier son jeton, sur l'app desktop | Le chemin d'un serveur local est prêt |
| Figma | Rien pour le serveur distant ; sur l'app desktop, le serveur de l'app Figma (plan payant) | « Not available yet » : liste d'attente de Figma |
| Teams | Rien de plus que l'application Entra de OneDrive | Lire les canaux et les conversations, poster après l'accord (TF-J2-14), à essayer |
| OneDrive, SharePoint | Enregistrer une fois notre application dans Entra ; chez une entreprise dont la politique le veut, l'accord de son administrateur | Connexion « Microsoft 365 », lecture en direct, rangement (TF-J2-14), à essayer |
| Google Drive | Enregistrer une fois notre application chez Google (un client, la clé du sélecteur) | Connexion, sélecteur de Google, lecture en direct, rangement (TF-J2-14), à essayer |

## Ce qui vaut pour tous

### Tous les outils se montrent

Le catalogue montre chaque outil, essayé ou non, sans rien à régler (décision de la Présidence, 12/11/2026 :
« t'imagines, ça veut dire que l'utilisateur devra faire ça? »). Après l'essai réussi d'un outil, sa date et sa preuve
entrent dans son champ `tried`, dans le fichier des préréglages : ce champ garde la preuve, il ne cache rien.

### Le geste

1. Settings > Integrations (groupe « Workspace ») > la tuile de l'outil.
2. « Connect ». Une phrase dit ce que la connexion donne : « Cortex reads … with your own account and rights. It asks you
   before any change. » Deux cases : « Also let Cortex propose changes », quand l'éditeur sépare la lecture de l'écriture
   (la lecture seule par défaut, et chaque changement reste à approuver) ; « Share with the workspace », pour un propriétaire
   ou un administrateur, et pour une source partagée seulement.
3. Le navigateur s'ouvre chez l'éditeur ; la Présidence s'y connecte et accepte. Sur l'app desktop, TaskForce affiche
   « Finish in your browser » et attend, puis le navigateur dit « You're connected » et l'app revient devant ; sur l'app web,
   le navigateur revient dans TaskForce. L'outil dit alors « Connected as … ».

Derrière ce geste, `POST /api/workspaces/{slug}/mcp/servers/{key}/connect` prend le premier chemin possible
(`McpClientRegistrar`) : l'application de l'entreprise saisie dans Settings ; sinon la nôtre, lue dans
`TF_MCP_<CLÉ>_CLIENT_ID` et `TF_MCP_<CLÉ>_CLIENT_SECRET` ; sinon notre document de métadonnées client (CIMD), si le serveur
l'accepte ; sinon l'inscription dynamique ; sinon l'étape de l'administrateur, ou la clé guidée. TaskForce refuse un serveur
de connexion qui n'annonce pas PKCE S256 (`McpOAuthDiscovery`, comme le veut la norme MCP). Aucun jeton de l'app desktop ne
passe par notre serveur.

Un serveur sans préréglage se branche par « Connect an MCP server », « MCP server URL », puis « Connect with OAuth » ou « Use
a token instead » ; tous ses outils sont des écritures qui demandent (R158).

### Les adresses de retour à déclarer

Seuls les éditeurs sans auto-inscription les demandent : ici Asana, Slack et une application OAuth de GitHub ; depuis le
12/11/2026, nos applications chez HubSpot, Dropbox, Xero, Docusign et Canva, et les applications d'entreprise de Box, Wrike,
Zoom et PagerDuty (« Les outils du répertoire de Claude », plus bas).

- **App web** : `https://api.taskforce-project.fr/api/mcp/oauth/callback` (`McpOAuthSettings`) ; la route répond sur ce
  domaine depuis le 11/11/2026.
- **Serveur auto-hébergé** : `<APP_API_URL>/api/mcp/oauth/callback`.
- **App desktop** : `http://127.0.0.1:47816/mcp/callback`. La coque prend le premier port libre de 47816 à 47819, le même
  d'un lancement à l'autre (`desktop/src/mcp-callback.ts`) : chez un éditeur qui veut chaque adresse listée, déclarer les
  quatre, de `http://127.0.0.1:47816/mcp/callback` à `http://127.0.0.1:47819/mcp/callback`. Une application OAuth de GitHub
  admet tout port de bouclage : `http://127.0.0.1/mcp/callback` lui suffit. La connexion au compte TaskForce garde ses ports,
  de 47812 à 47815.
- L'écran « Your company's app » rappelle l'adresse de l'instance, sous « Redirect address to register ».
- **Nos documents de métadonnées client**, servis par l'API hébergée :
  `https://api.taskforce-project.fr/api/mcp/oauth/client.json` (le serveur) et
  `https://api.taskforce-project.fr/api/mcp/oauth/desktop-client.json` (l'app desktop, avec ses quatre adresses). Tant
  qu'ils ne répondent pas, le backend passe à l'inscription dynamique.

### Où va un identifiant client

- **Notre application** (chemin B) : `TF_MCP_<CLÉ>_CLIENT_ID` et `TF_MCP_<CLÉ>_CLIENT_SECRET`, la clé du préréglage en
  majuscules et tout autre signe changé en `_`, soit `TF_MCP_ASANA_CLIENT_ID` ou `TF_MCP_GITHUB_MCP_CLIENT_ID`
  (`McpClientRegistrar`). Sur le serveur, les fichiers compose ne transmettent que les paires déclarées : Asana, GitHub MCP, et depuis le 12/11/2026
  HubSpot, Dropbox, Xero (l'identifiant seul), Docusign et Canva ; sur l'app
  desktop, ce sont des variables de l'utilisateur Windows, que la coque passe au backend local. Jamais dans le dépôt.
- **L'application de l'entreprise** (chemin C) : un propriétaire ou un administrateur la saisit dans Settings >
  Integrations > l'outil, écran « Your company's app » : « Client ID », « Client secret », « Save and connect ». Le secret est rangé
  chiffré, pour l'espace (`connector_app`). Pour un outil dont l'entreprise tient le serveur (Glean, Zoho),
  le serveur auquel ce propriétaire ou cet administrateur se connecte d'abord par elle est retenu : chacun se
  connecte ensuite par la même application, à ce serveur seulement.
- **Une clé, ou l'adresse d'un serveur** : « Connect with a key instead », ou « Your server's address » pour Zoho ; masquée,
  rangée chiffrée, jamais réaffichée.

### Ce qu'elle verra

- **Branché** : « Connected as … », ou « Connected with your account » quand l'éditeur ne nomme pas le compte, avec « Yours »
  ou « Shared with the workspace » ; « What Cortex can do here » range les outils en « Reads » et « Asks you first ». Un
  serveur ajouté à la main dit « Connected, N tool(s) available ».
- **L'étape de l'administrateur** : « Your admin needs to act first », le message à lui envoyer, « Copy the message »,
  « Open the admin page », « Try again » ; l'outil reste « Waiting for your admin ». Un propriétaire ou un administrateur
  voit à la place « Your company's app ».
- **Un outil qui change** : la liste des outils est figée à la connexion ; « 1 tool changed since you connected. It stays
  off until you approve it. », puis « Approve the changes ».
- **Un jeton que l'éditeur refuse** : « Needs reconnecting », puis « Reconnect ».
- **Déconnecter** révoque chez l'éditeur quand il le permet : « Disconnected. Your access was revoked at … » ; sinon
  « Disconnected here. … doesn't let TaskForce revoke the access: remove TaskForce in your … settings. »
- Un outil que le préréglage ne classe pas est une écriture : Cortex demande avant de s'en servir (R158).

## Bureautique et stockage

### Google Drive

**Une étape de la Présidence, une fois : notre application chez Google ; puis un clic pour chaque personne.** Google
n'offre ni auto-inscription ni document de métadonnées client, et son serveur MCP de Drive est en Developer Preview, réservé
aux membres du programme ([Google](https://developers.google.com/workspace/guides/configure-mcp-servers)) : TaskForce parle
l'API Drive lui-même, derrière la même connexion que tout autre outil (TF-J2-14, PR [#528](https://github.com/taskforce-project/taskforce-fullstack/pull/528)). La seule portée
demandée est `drive.file` : TaskForce n'atteint que les fichiers que la personne choisit dans le sélecteur de Google, et
ceux qu'il range lui-même. Elle n'est pas sensible, donc ni vérification restreinte ni évaluation de sécurité ; `drive` et
`drive.readonly` le seraient ([Google](https://developers.google.com/workspace/drive/api/guides/api-specific-auth)).

Ce que fait la Présidence, sur console.cloud.google.com :

1. Un projet (« TaskForce »), puis APIs & Services > Library : activer **Google Drive API** et **Google Picker API**.
2. Google Auth Platform (l'écran de consentement) : Branding, le nom « TaskForce » et l'e-mail d'assistance ; Audience,
   **External** ; tant que l'application est en « Testing », ajouter ses comptes dans **Test users** (100 au plus, et une
   autorisation y expire après sept jours, [Google](https://support.google.com/cloud/answer/15549945)) ; Data access, les
   portées `openid`, `email` et `.../auth/drive.file`.
3. Clients > Create client > **Web application** (le serveur) : Authorized redirect URIs
   `https://api.taskforce-project.fr/api/mcp/oauth/callback` (une installation auto-hébergée : `<APP_API_URL>/api/mcp/oauth/callback`).
   Garder l'identifiant et le secret.
4. Clients > Create client > **Desktop app** (l'app desktop) : aucune adresse à saisir, Google admet le retour sur
   `http://127.0.0.1` à tout port pour ce type de client ([Google](https://developers.google.com/identity/protocols/oauth2/native-app)).
   Garder l'identifiant et le secret, que Google ne tient pas pour secret pour une app de bureau.
5. APIs & Services > Credentials > Create credentials > **API key**, pour le sélecteur : Application restrictions
   « Websites », l'adresse de l'app web (`FRONTEND_URL` de `.env.prod`) et, pour l'app desktop, `http://127.0.0.1` ;
   API restrictions, **Google Picker API** seule.
6. Le numéro du projet (IAM & Admin > Settings > Project number) : c'est `TF_GOOGLE_APP_ID`, que le sélecteur exige avec
   `drive.file` ([Google](https://developers.google.com/workspace/drive/picker/guides/overview)).
7. **Sur le serveur** : dans `.env.prod`, `TF_GOOGLE_CLIENT_ID` et `TF_GOOGLE_CLIENT_SECRET` (le client « Web
   application »), `TF_GOOGLE_API_KEY` et `TF_GOOGLE_APP_ID` ; `docker-compose.prod.yml` les passe au backend, qu'on recrée pour qu'il les lise. **Sur l'app desktop** :
   les mêmes noms en variables de l'utilisateur Windows, avec l'identifiant et le secret du client « Desktop app » ; la coque
   les passe au backend local (`desktop/src/backend.ts`). Jamais dans le dépôt.
8. **Dans TaskForce** : Settings > Integrations > Google Drive > « Connect » ; chez Google, choisir son compte et accepter ;
   retour, « Connected as … ». Puis, dans la même fiche, « Choose files » : le sélecteur de Google s'ouvre, les fichiers
   choisis sont ceux que Cortex lira. Enfin Settings > Storage > « Change » > Google Drive > « Choose a folder ».

Ce qu'elle verra : Cortex lit un fichier en direct (`google-drive__read_file`) et le cite avec sa version, son responsable
et sa date ; ranger un document demande son accord, puis le fichier arrive dans le dossier, et Settings > Storage dit où il
vit, avec son lien et sa version. Déconnecter révoque chez Google (`https://oauth2.googleapis.com/revoke`).

Non vérifié : le sélecteur dans la fenêtre de l'app desktop ; la clé du navigateur restreinte à `http://127.0.0.1` (le port
du proxy de la coque change à chaque lancement) ; l'avertissement « Google hasn't verified this app » tant que l'application
n'a pas passé la vérification de sa marque ; un retour avec un chemin (`/mcp/callback`) pour un client « Desktop app ».

### OneDrive et SharePoint (Microsoft 365)

**Une étape de la Présidence, une fois : notre application dans Entra ; puis, chez une entreprise dont la politique le
veut, l'accord de son administrateur.** Une seule connexion « Microsoft 365 » par personne sert OneDrive, SharePoint et
Teams, par Microsoft Graph, avec des droits délégués et PKCE S256 (TF-J2-14). Pas Work IQ, qui se paie en crédits Copilot
(voir Teams). Entra accepte S256 sans l'annoncer dans ses métadonnées, et nomme son émetteur `{tenantid}` pour `common` :
TaskForce l'admet pour les seuls émetteurs d'Entra, sur `login.microsoftonline.com`, quand la métadonnée se tait ; pour tout
autre serveur, la vérification reste entière (`McpOAuthDiscovery`, `EntraDiscoveryTest`).

Ce que fait la Présidence, sur entra.microsoft.com :

1. Identity > Applications > App registrations > New registration : le nom « TaskForce » ; Supported account types,
   **Accounts in any organizational directory and personal Microsoft accounts** (multilocataire) ; Redirect URI, plateforme
   **Web**, `https://api.taskforce-project.fr/api/mcp/oauth/callback`.
2. Pour l'app desktop : Manifest, dans `replyUrlsWithType`, les quatre adresses `http://127.0.0.1:47816/mcp/callback` à
   `http://127.0.0.1:47819/mcp/callback`, de type `InstalledClient` ; une adresse `127.0.0.1` ne s'ajoute que par le
   manifeste ([Microsoft](https://learn.microsoft.com/en-us/entra/identity-platform/reply-url)). Authentication : laisser
   « Allow public client flows » éteint.
3. Certificates & secrets > New client secret : la valeur, montrée une seule fois, pour le serveur seulement.
4. API permissions > Add a permission > Microsoft Graph > **Delegated permissions** : `openid`, `profile`, `email`,
   `offline_access`, `User.Read`, `Files.Read.All`, `Sites.Read.All`, `Team.ReadBasic.All`, `Channel.ReadBasic.All`,
   `ChannelMessage.Read.All`, `Chat.Read` ; et pour l'écriture `Files.ReadWrite.All`, `ChannelMessage.Send`,
   `ChatMessage.Send`. Dans son propre locataire : « Grant admin consent for … ».
5. Plus tard, pour les autres entreprises : Branding & properties > Publisher verification, par le Microsoft AI Cloud
   Partner Program ; sans elle, une entreprise dont le consentement par palier de risque est actif bloque l'accord des
   personnes ([Microsoft](https://learn.microsoft.com/en-us/entra/identity-platform/publisher-verification-overview)).
6. **Sur le serveur** : dans `.env.prod`, `TF_MICROSOFT_CLIENT_ID`, `TF_MICROSOFT_CLIENT_SECRET` et
   `TF_MICROSOFT_TENANT=common` (une installation avec une application d'un seul locataire met l'identifiant de son
   locataire). **Sur l'app desktop** : `TF_MICROSOFT_CLIENT_ID` (et `TF_MICROSOFT_TENANT`) en variables de l'utilisateur
   Windows, jamais le secret : pour Entra, l'app desktop est un client public, et la coque ne le passe pas.
7. **Dans TaskForce** : Settings > Integrations > Microsoft 365 > « Connect », en cochant « Also let Cortex propose
   changes » pour ranger dans OneDrive et poster dans Teams ; chez Microsoft, accepter ; retour. Puis Settings > Storage >
   « Change » > OneDrive or SharePoint > « Choose a folder » : son OneDrive, puis les bibliothèques des sites qu'elle suit.

Chez une entreprise dont la politique réserve `Files.Read.All`, `Sites.Read.All` ou `Chat.Read` à l'administrateur (c'est
la politique par défaut de Microsoft, [Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies)),
Microsoft répond AADSTS65001, 90094, 90095 ou 900941 `[DÉDUIT]`, et TaskForce affiche l'étape de l'administrateur : « Your admin
needs to act first », le message à lui envoyer, et la page de l'administrateur,
`https://login.microsoftonline.com/organizations/adminconsent?client_id=<l'identifiant de notre application>`
([Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/grant-admin-consent)) ; une fois l'accord
donné, « Try again ». Déconnecter ne révoque pas chez Microsoft, qui n'offre pas de révocation d'un jeton : TaskForce le dit
et indique où retirer l'accès.

Non vérifié : un compte Microsoft personnel devant les permissions de SharePoint et de Teams ; la page de l'administrateur
avec l'autorité `organizations` ; le retour sur `127.0.0.1` ajouté par le manifeste ; la version d'un fichier de OneDrive
personnel.

## Savoir et documentation

### Notion

**Un clic.** Notion accepte l'auto-inscription (RFC 7591) ou un document de métadonnées (CIMD), avec PKCE obligatoire, et
n'écrit aucune revue ([Notion](https://developers.notion.com/guides/mcp/build-mcp-client)) ; ses métadonnées disent
« Notion MCP (Beta) ». TaskForce lui présente d'abord son document de métadonnées, sinon l'inscription dynamique.

1. TaskForce : Notion > « Connect ».
2. Chez Notion : accepter.
3. Retour : « Connected as … ».

- **Si l'espace Notion est en Enterprise** et n'admet que des clients approuvés : son propriétaire approuve TaskForce dans
  Settings > Notion MCP > Manage workspace clients ([Notion](https://www.notion.com/help/notion-mcp)) ; TaskForce garde ce
  texte, replié, sous « If Notion refuses the connection: ».
- La connexion tient 180 jours au plus, ou 30 jours sans usage ; ensuite, « Needs reconnecting »
  ([Notion](https://developers.notion.com/guides/mcp/build-mcp-client)).
- Non vérifié : le retour sur `127.0.0.1` (Notion demande HTTPS en production) et la disponibilité générale du serveur.

### Confluence

**Un clic sur l'app desktop ; une étape d'abord sur l'app web.** Un seul serveur Atlassian sert Confluence, Jira, Jira
Service Management et Bitbucket : `https://mcp.atlassian.com/v2/mcp`, « Generally Available »
([Atlassian](https://github.com/atlassian/atlassian-mcp-server)) ; il accepte l'auto-inscription et PKCE
([métadonnées](https://mcp.atlassian.com/.well-known/oauth-authorization-server)). Dans TaskForce, Confluence et Jira sont
deux préréglages, chacun avec ses portées : deux connexions, chacune avec sa connexion chez Atlassian.

L'organisation n'admet que les adresses de retour de sa liste : par défaut `127.0.0.1` et `localhost`, et des domaines
d'éditeurs connus, pas celui de TaskForce
([Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-rovo-mcp-server-domains/)) ;
sinon le consentement répond « Your organization admin must authorize access from this redirect URL »
([Atlassian](https://support.atlassian.com/rovo/kb/fix-oauth-consent-block-for-atlassian-rovo-mcp-server-in-atlassian-cloud/)).

1. **Sur l'app web seulement, une fois** : admin.atlassian.com, son organisation > Connectors > Atlassian MCP server >
   « Add domain » ([Atlassian](https://support.atlassian.com/security-and-access-policies/docs/control-atlassian-rovo-mcp-server-settings/) ;
   ailleurs écrit Rovo > Rovo MCP server > Domain settings) : `https://api.taskforce-project.fr/**` (un protocole, puis `/**`
   pour tout chemin : [Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-mcp-server-domains/)).
   Sur l'app desktop, rien : `127.0.0.1` est admis par défaut.
2. TaskForce : Confluence > « Connect ».
3. Chez Atlassian : accepter l'accès au site.
4. Retour : « Connected as … ».

- Si le domaine manque, TaskForce affiche « Your admin needs to act first », avec le message pour l'administrateur.
- Les appels au Teamwork Graph (`searchAtlassian`, `getTeamworkGraphContext`) consomment des crédits Rovo
  ([Atlassian](https://support.atlassian.com/rovo/docs/getting-started-with-the-atlassian-remote-mcp-server/)).
- Non vérifié : si l'entrée `127.0.0.1` par défaut vaut pour tout port.

## Tickets et projets

### Jira

**Comme Confluence**, avec sa propre connexion : Jira > « Connect », la même étape sur l'app web. Supprimer et administrer
(`delete_jira`, `manage_jira`) restent coupés tant qu'un administrateur ne les ouvre pas ; Jira Service Management ne passe
que par un jeton d'API ([Atlassian](https://github.com/atlassian/atlassian-mcp-server)).

- Jira et Confluence servent sans demander les outils que la page d'Atlassian range en lecture, Teamwork Graph et la
  recherche de code compris ([Atlassian](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/supported-tools/),
  relue le 12/11/2026) ; `executeRead`, qui lance n'importe quel outil différé, demande : la page ne le limite pas à la
  lecture. Relue le 13/11/2026 : une lecture sur la description de chaque outil ; `exportConfluenceContent` (un export
  et son lien) et `getJiraWorkflowEditorLink` demandent.
- Non vérifié : un premier accord d'un administrateur du site, rapporté seulement par la communauté.

### Linear

**Un clic, déjà essayé**, le seul préréglage qui porte `tried` (03/09/2026) ; comme chaque préréglage, il se montre. Auto-inscription et
CIMD, PKCE ([métadonnées](https://mcp.linear.app/.well-known/oauth-authorization-server)). Sans « Also let Cortex propose
changes », TaskForce se branche sur l'adresse en lecture seule, `https://mcp.linear.app/mcp/readonly`
([Linear](https://linear.app/docs/mcp)).

1. TaskForce : Linear > « Connect ».
2. Chez Linear : accepter.
3. Retour : « Connected as … ».

- Si l'espace Linear approuve les applications tierces, un administrateur approuve TaskForce : Settings > Administration >
  Security > Third-party application approvals (texte du préréglage).
- Linear ne publie pas la liste de ses outils, mais écrit que l'adresse en lecture seule « only ever exposes read tools »
  ([Linear](https://linear.app/docs/mcp), relue le 13/11/2026) : sans l'écriture, chaque outil sert sans demander. Avec
  l'écriture, sur l'adresse entière, seuls ceux que son [journal des changements](https://linear.app/changelog) dit en
  lecture servent sans demander (`list_issues`, `list_issue_labels`, `list_comments`, `list_cycles`, `list_projects`,
  `get_project`, `list_teams`, `get_team`, `list_users`, `get_user`, `list_customer_needs`) ; les autres demandent.
- Non vérifié : le retour sur tout port de bouclage.

### Asana

**Une étape de son côté, une fois.** Le serveur V2, `https://mcp.asana.com/v2/mcp`, refuse l'auto-inscription : il faut une
« MCP app », avec un identifiant et un secret ; toute portée autre que `default` est refusée
([Asana](https://developers.asana.com/docs/integrating-with-asanas-mcp-server), page du 08/10/2026). Son serveur
d'autorisation n'admet qu'un client avec secret (métadonnées de `app.asana.com`).

1. `https://app.asana.com/0/my-apps` > « Create new app » : un nom, le type « MCP app », « Create app ».
2. L'adresse de retour (« Redirect URL ») : celle de l'app web et celle de l'app desktop (47816, et 47817 à 47819 en
   secours).
3. « Manage distribution » : « Any workspace », comme le dit le préréglage.
4. L'identifiant client et le secret : Settings > Integrations > Asana > « Connect » > « Your company's app » > « Client
   ID », « Client secret » > « Save and connect ». Ou, pour notre application, `TF_MCP_ASANA_CLIENT_ID` et
   `TF_MCP_ASANA_CLIENT_SECRET` : dans l'environnement de production pour le serveur, en variables de l'utilisateur Windows
   pour l'app desktop.
5. Chez Asana : accepter ; retour.

- En Enterprise, un administrateur d'Asana autorise aussi l'application (texte du préréglage).
- Asana publie ses outils ([MCP Tools Reference](https://developers.asana.com/docs/mcp-tools-reference), relue le
  12/11/2026) : les 25 qu'Asana dit en lecture servent sans demander ; les écritures et les trois outils interactifs
  demandent.
- Non vérifié : si PKCE dispense du secret.

## Messagerie, mail et réunions

### Slack

**Une étape de son côté, une fois.** Le serveur MCP de Slack, `https://mcp.slack.com/mcp`, n'accepte que les applications
publiées dans son annuaire ou internes à l'entreprise ; OAuth avec identifiant et secret, PKCE pour les clients de bureau,
pas d'auto-inscription ; les administrateurs de l'espace approuvent et gèrent les clients MCP
([Slack](https://docs.slack.dev/ai/slack-mcp-server/)). Publier dans l'annuaire demande une revue de dix semaines au plus (lu
le 10/11, [Slack](https://docs.slack.dev/slack-marketplace/slack-marketplace-review-guide)) : pour l'essai, l'application de
l'entreprise, interne à son espace.

1. `https://api.slack.com/apps` > « Create New App » : un nom, son espace.
2. Allumer MCP : dans le manifeste de l'application, `is_mcp_enabled: true` sous `settings`
   ([Slack](https://slack.dev/slack-developer-changelog-recap-april-june-2026/)).
3. OAuth & Permissions : les deux adresses de retour, et les portées de l'utilisateur en lecture du préréglage :
   `search:read.public`, `search:read.private`, `search:read.mpim`, `search:read.im`, `search:read.files`,
   `search:read.users`, `channels:history`, `groups:history`, `mpim:history`, `im:history`, `channels:read`, `groups:read`,
   `im:read`, `mpim:read`, `users:read`, `files:read`, `canvases:read`, `lists:read`, `reactions:read`, `emoji:read`.
4. Installer l'application dans son espace, sans activer la distribution publique `[HYPOTHÈSE]`.
5. Basic Information > App Credentials : l'identifiant client et le secret dans Settings > Integrations > Slack >
   « Connect » > « Your company's app » > « Save and connect ».
6. Chez Slack : accepter ; retour.

- Slack ne publie pas le nom de ses outils : chacun demande avant de servir, jusqu'à ce que l'essai les classe.
- Non vérifié : si Slack accepte un retour sur `127.0.0.1` (sa documentation montre `localhost`).
- **Le Slack natif** (les notifications des tickets, l'historique des canaux) ne change pas et reste à l'app web : « Connect »,
  l'application Slack de TaskForce s'installe, retour. Le serveur lit `SLACK_CLIENT_ID` et `SLACK_CLIENT_SECRET` ;
  l'application déclare `https://api.taskforce-project.fr/api/integrations/slack/callback` et les portées du robot
  `chat:write`, `chat:write.public`, `channels:read`, `channels:history`, `users:read`, `incoming-webhook`
  (`SlackIntegrationService`) ; configurée en production `[HYPOTHÈSE]`. Sur l'app desktop : « Web app only ».
- Les conditions de Slack interdisent l'entraînement d'un modèle et les copies durables des données d'autres organisations
  (lu le 10/11, [Slack](https://slack.com/terms-of-service/api)) : TaskForce lit en direct (R155).

### Microsoft Teams

**Sur la même connexion « Microsoft 365 » que OneDrive** (TF-J2-14) : rien de plus à enregistrer que l'application Entra
décrite plus haut, avec ses permissions de Teams. Pas Work IQ, le serveur MCP de Microsoft 365, qui se paie à l'usage en
crédits Copilot et qu'un administrateur global doit activer avec un plan de facturation
([Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/enable-work-iq)) : TaskForce
parle Microsoft Graph lui-même.

- **Lire** : Cortex liste les équipes et les canaux de la personne (`microsoft-365__list_teams`), ses conversations
  (`list_chats`), et lit un canal ou une conversation en direct (`read_channel`, `read_chat`), les vingt derniers messages,
  cités avec leur auteur et leur date, comme un contenu du dehors (R158). Les droits sont les siens : ce qu'elle ne lit pas
  dans Teams, Cortex ne le lit pas.
- **Écrire** : poster dans un canal ou une conversation (`post_channel_message`, `post_chat_message`) est une sortie : le
  moteur demande toujours une personne, et la carte dit où le message part.
- **Permissions** : `Team.ReadBasic.All`, `Channel.ReadBasic.All`, `ChannelMessage.Read.All`, `Chat.Read` pour lire ;
  `ChannelMessage.Send` et `ChatMessage.Send` pour poster, demandées quand la personne coche « Also let Cortex propose
  changes ». La politique par défaut de Microsoft réserve `Chat.Read` à l'administrateur
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies)) : chez une
  entreprise qui la garde, l'étape de l'administrateur de OneDrive vaut pour Teams.

Avec un compte Microsoft personnel, Teams ne sert pas : Graph ne donne ses canaux et conversations qu'aux comptes
professionnels `[DÉDUIT]`.

## Code

### GitHub

**L'intégration native ne change pas.** Settings > Integrations > GitHub : sur l'app desktop, GitHub CLI (un code à usage
unique dans le navigateur, comme `gh auth login`), « Connected with GitHub CLI on this computer, as … » ; sur l'app web,
« Connect », GitHub demande `repo` et `read:org`, puis « GitHub is connected for this workspace. ». Le serveur lit
`GITHUB_CLIENT_ID` et `GITHUB_CLIENT_SECRET`, et l'application OAuth déclare
`https://api.taskforce-project.fr/api/integrations/github/callback` (`GitHubIntegrationService`) ; configurée en production
`[HYPOTHÈSE]`.

**Ses outils MCP** passent par un préréglage à part, la seconde tuile GitHub : le serveur `https://api.githubcopilot.com/mcp/`,
en lecture seule par défaut sur `https://api.githubcopilot.com/mcp/readonly`. Chaque hôte y configure sa propre application,
ou un jeton personnel ([GitHub](https://github.com/github/github-mcp-server)). Deux façons :

1. **Une clé, le plus simple** : un jeton fin (fine-grained) dans GitHub, Settings > Developer settings, en lecture sur les
   dépôts que TaskForce peut lire (`https://github.com/settings/personal-access-tokens/new`) ; puis dans TaskForce : la tuile
   MCP de GitHub > « Connect » > « Connect with a key instead » > coller > « Connect ».
2. **Une application OAuth** : GitHub, Settings > Developer settings > OAuth apps, avec l'adresse de retour de l'app web ;
   son identifiant et son secret dans `TF_MCP_GITHUB_MCP_CLIENT_ID` et `TF_MCP_GITHUB_MCP_CLIENT_SECRET` sur le serveur, ou
   dans « Your company's app ». Pour l'app desktop, une seconde application OAuth avec `http://127.0.0.1/mcp/callback`,
   saisie dans « Your company's app » (PR #523).
3. Dans les deux cas, si son organisation restreint les applications OAuth, ce que font par défaut les organisations
   récentes ([GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/about-oauth-app-access-restrictions)),
   en propriétaire : Organizations > l'organisation > Settings > Third-party Access > OAuth app policy > « Review » à côté de
   l'application > « Grant access » ([GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/approving-oauth-apps-for-your-organization)).
   Pour GitHub CLI, l'approbation de l'organisation est `[HYPOTHÈSE]`.

- Non vérifié : la règle de port de bouclage des GitHub Apps (les applications OAuth admettent tout port).

### GitLab

**Un clic** ; une case à cocher si l'accès a été fermé. Le serveur, `https://gitlab.com/api/v4/mcp` (ou
`https://<instance>/api/v4/mcp`), est « Generally available » depuis la 19.5, sur les plans Free, Premium et Ultimate ; à la
première connexion, l'auto-inscription crée une application OAuth sur l'instance, avec la portée `mcp`, la seule que
TaskForce demande ([GitLab](https://docs.gitlab.com/user/gitlab_duo/model_context_protocol/mcp_server/)). L'inscription
dynamique déclare chaque fois l'adresse exacte : rien à déclarer à la main.

1. TaskForce : GitLab > « Connect ».
2. Chez GitLab : autoriser ; retour.
3. Si GitLab répond « MCP server not enabled for any of your groups »
   ([GitLab](https://docs.gitlab.com/user/model_context_protocol/mcp_server_troubleshooting/)) : en propriétaire d'un groupe
   de premier niveau, Settings > General > Permissions and group features > MCP client access > « Allow connection to
   GitLab » > « Save changes ». L'accès est ouvert par défaut depuis la 19.5 pour les nouveaux groupes et depuis la 19.6 pour
   les autres, sauf si un propriétaire l'a fermé ([GitLab](https://docs.gitlab.com/user/group/access_and_permissions/)).

- En auto-hébergé : l'administrateur de l'instance ouvre MCP ; s'il a coupé l'auto-inscription, une application OAuth
  pré-enregistrée (portée `mcp`, non confidentielle, l'adresse de retour exacte), saisie dans « Your company's app ».
- Non vérifié : si l'inscription dynamique donne un client public ou confidentiel.

### Docker Hub

**L'exception de la Présidence** : « on garde docker hub en exception, je copierai le jeton »
([séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)). Sur l'app desktop seulement, par
un jeton copié.

Docker Hub n'a pas de serveur distant. Le serveur officiel, `docker/hub-mcp`, tourne sur le poste : en stdio par défaut, ou
en HTTP sur `127.0.0.1` avec un jeton porteur ; il lit Docker Hub avec un jeton d'accès personnel ; ni OAuth ni adresse
distante ([GitHub](https://github.com/docker/hub-mcp)). Docker Desktop l'installe par son MCP Toolkit
([Docker](https://docs.docker.com/ai/mcp-catalog-and-toolkit/hub-mcp/)), et sa passerelle le sert à plusieurs clients en
HTTP ([GitHub](https://github.com/docker/mcp-gateway)). TaskForce n'admet une adresse locale que sur l'app desktop, et
seulement avec l'accord de la personne (`McpClient.isLocal`).

1. Docker Desktop > MCP Toolkit > Catalog : ajouter « Docker Hub », avec son identifiant et son jeton d'accès personnel
   Docker Hub, réglés dans Docker Desktop.
2. Un terminal : `docker mcp gateway run --transport streaming`, avec `--port 8811` s'il demande un port ; copier le jeton que
   la passerelle donne à ses clients (`MCP_GATEWAY_AUTH_TOKEN` le fixe, sinon elle en tire un nouveau à chaque lancement
   `[TIERS]`, [DEV](https://dev.to/udondan/running-docker-mcp-gateway-on-linux-without-docker-desktop-4da2)).
3. TaskForce (app desktop) : Settings > Integrations > « Connect an MCP server » : le nom « Docker Hub », l'adresse
   `http://localhost:8811/mcp`, « Use a token instead », le jeton ; cocher « I started this server myself » ; « Connect ».
4. Elle verra « Connected, N tool(s) available ».

- Chaque outil demande avant de servir : un serveur ajouté à la main n'a pas de préréglage qui les classe.
- Non vérifié : le port, le chemin et les options de jeton de la passerelle.

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
4. Connect : copier l'adresse du serveur. Elle vaut une clé, puisque « Regenerate API Key » en donne une nouvelle (même
   page).
5. TaskForce : Zoho > « Connect » > « Your server's address » : coller l'adresse, masquée, rangée chiffrée, jamais
   réaffichée, puis « Connect » ; se connecter chez Zoho s'il le demande.

- Chaque outil demande avant de servir : chaque entreprise choisit les siens, et l'essai les classera.
- Non vérifié : un serveur hors du centre de données indien de Zoho, où se trouve la console du guide.

### Stripe

**Un clic.** Le serveur, `https://mcp.stripe.com`, suit l'OAuth de la norme MCP du 28/07/2026
([Stripe](https://docs.stripe.com/mcp)) : auto-inscription, client public, PKCE, révocation, portée `mcp`
([métadonnées](https://access.stripe.com/.well-known/oauth-authorization-server/mcp)).

1. TaskForce : Stripe > « Connect ».
2. Chez Stripe : choisir le ou les comptes, un environnement de test d'abord, et les droits de chacun ; accepter
   ([Stripe](https://docs.stripe.com/mcp)).
3. Retour : « Connected as … ».

- Si Stripe refuse : un administrateur ouvre l'accès MCP de l'équipe, Dashboard > Settings > MCP and CLI access, à part pour
  le mode réel et pour le test (même page). Si le refus demande l'administrateur, TaskForce offre aussi « Connect with a key
  instead » : une clé Agent restreinte, en lecture seule.
- Déconnecter révoque aussi chez Stripe, qui annonce la révocation `[DÉDUIT]` ; à la main : les paramètres de l'utilisateur >
  OAuth sessions > « Revoke access » (même page).
- R158 : le préréglage classe en écriture `stripe_api_write` (toute méthode POST, PATCH, PUT ou DELETE), `send_money`,
  `transfer_money`, `convert_currency`, `setup_recipient`, `atlas_company_formation` et `send_stripe_feedback` ; certains
  gestes demandent en plus une confirmation dans le Dashboard (même page).
- À partir de décembre 2026, Stripe MCP refuse les clés secrètes complètes et les clés restreintes sans l'étiquette
  « Agent » (même page) : OAuth évite la question.
- Non vérifié : une liste des adresses de retour admises, que cite une page de place de marché de Stripe et non
  docs.stripe.com ; un choix de lecture seule sur l'écran de consentement.

## Design et collaboration

### Figma

**Hors de la vague pour le serveur distant ; un contournement sur l'app desktop.** TaskForce montre « Not available yet »,
avec la raison (le champ `blocked` du préréglage).

- Le serveur distant, `https://mcp.figma.com/mcp`, n'admet que les clients de son catalogue ; un nouveau client attend sur
  une liste, par un formulaire ([Figma](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation)).
  Inscrire TaskForce sur cette liste est un geste de la Présidence. R153 : un outil bloqué par son éditeur sort de la vague,
  la raison au registre.
- Le serveur de l'app Figma, `http://127.0.0.1:3845/mcp`, ne demande pas de connexion ; il exige un siège Dev ou Full sur un
  plan Professional, Education, Organization, Government ou Enterprise, et n'écrit pas dans le canevas
  ([Figma](https://developers.figma.com/docs/figma-mcp-server/local-server-installation)).

Sur l'app desktop, avec un plan payant :
1. L'app Figma (bureau) : ouvrir un fichier de design, passer en Dev Mode sans rien sélectionner, puis, dans le volet de
   droite, section MCP server, « Enable desktop MCP server » (même page).
2. TaskForce (app desktop) : Settings > Integrations > « Connect an MCP server » > `http://127.0.0.1:3845/mcp`, sans jeton ;
   cocher « I started this server myself » ; « Connect ».
3. Elle verra « Connected, N tool(s) available », tant que l'app Figma tourne `[HYPOTHÈSE]`. Ses outils demandent tous : un
   serveur ajouté à la main n'a pas de préréglage.

### Excalidraw

**Un clic, sans compte** : la tuile dit « No sign-in ». Le serveur officiel (organisation Excalidraw, licence MIT),
`https://mcp.excalidraw.com`, « Works with any client that supports MCP Apps »
([GitHub](https://github.com/excalidraw/excalidraw-mcp)). Sondé le 11/11/2026 sans compte (`initialize`, `tools/list`) :
`https://mcp.excalidraw.com/mcp` répond sans jeton, n'annonce pas d'OAuth, et offre cinq outils.

1. TaskForce : Excalidraw > « Connect ».
2. Elle verra « Connected with your account ». Rien à faire chez Excalidraw.

- R158 : le préréglage classe en écriture `export_to_excalidraw` (il envoie le dessin sur excalidraw.com et rend un lien de
  partage), `save_checkpoint` et `create_view` (il garde chaque dessin sur le serveur, `src/server.ts` relu le
  13/11/2026) ; `read_checkpoint` n'est pas classé ; seul `read_me` lit sans demander.
- Limite : le client MCP de TaskForce ne lit que du texte, ni ressources ni MCP Apps ; il appelle les outils sans afficher le
  dessin `[DÉDUIT]`.
- Non vérifié : ce que `create_view` rend à un client sans MCP Apps.

### Excalidraw+

**Une clé, une fois.** Le serveur d'Excalidraw+, `https://api.excalidraw.com/api/v1/mcp`, prend une clé en jeton porteur et
demande un espace Excalidraw+ ([Excalidraw+](https://plus.excalidraw.com/docs/mcp/getting-started)). Une clé personnelle
agit comme son propriétaire et atteint sa collection privée ; un administrateur de l'espace doit d'abord autoriser les clés
personnelles dans les réglages de l'espace ([Excalidraw+](https://plus.excalidraw.com/docs/mcp/mcp-api-key-types)).

1. Excalidraw+ : en administrateur de l'espace, autoriser les clés MCP personnelles, dans les réglages de l'espace.
2. Créer une clé MCP personnelle.
3. TaskForce : Excalidraw+ > « Connect » > coller la clé > « Connect ».

- R158 : le préréglage classe ses outils ; créer, modifier, supprimer ou partager une scène sont des écritures.
- Non vérifié : le plan requis, une clé en lecture seule.

## Les outils du répertoire de Claude (12/11/2026)

La Présidence, le 12/11/2026 : « regarde un peu ce que propose par exemple Claude en extension non communautaire [...] Et
puis on fait la même ». Le catalogue reprend les connecteurs d'entreprise du répertoire de Claude : 71 outils de plus, 102
préréglages en 13 catégories (PR [#527](https://github.com/taskforce-project/taskforce-fullstack/pull/527)). Leurs faits,
lus le 12/11/2026 sur les pages des éditeurs et dans leurs métadonnées OAuth publiques, sont au
[Registre des outils](./Registre_des_outils.md), avec une source par ligne ; les outils laissés de côté y sont, chacun avec sa
raison. Ici, ce que la Présidence fait une fois comme éditeur de TaskForce, puis ce que chaque personne fait.

### Ce que la Présidence enregistre une fois, comme éditeur

Les adresses de retour à déclarer sont celles d'en haut : l'app web,
`https://api.taskforce-project.fr/api/mcp/oauth/callback`, et les quatre de l'app desktop, de
`http://127.0.0.1:47816/mcp/callback` à `http://127.0.0.1:47819/mcp/callback`. Les variables vont dans le `.env` du serveur de
production, jamais dans un dépôt. Tant qu'une variable est vide, l'outil passe par l'application de l'entreprise : son
administrateur la crée et la saisit dans Settings.

| Éditeur | La console | Les variables | L'app desktop sans livrer de secret |
| --- | --- | --- | --- |
| HubSpot | Un compte développeur HubSpot, Development, MCP Auth Apps : une application avec les deux jeux d'adresses ; une application non listée s'installe dans 25 comptes au plus (10/11/2026) | `TF_MCP_HUBSPOT_CLIENT_ID`, `TF_MCP_HUBSPOT_CLIENT_SECRET` | Non : HubSpot remet un secret et ne décrit pas de client sans secret `[HYPOTHÈSE]` |
| Dropbox | App Console, Create app, accès « scoped » ; les permissions de lecture des fichiers et des partages (et d'écriture si l'on veut proposer des changements) ; les adresses exactes ; l'approbation de production dans les deux semaines après 50 personnes | `TF_MCP_DROPBOX_CLIENT_ID` (la clé de l'application), `TF_MCP_DROPBOX_CLIENT_SECRET` | Oui en principe : Dropbox admet PKCE pour un client public ; mais TaskForce lit l'identifiant dans l'environnement de la personne, pas dans l'app |
| Xero | Le portail développeur de Xero, New app, type PKCE (sans secret) ; le plan développeur Core ou plus pour de vraies organisations (Starter : l'organisation de démonstration) | `TF_MCP_XERO_CLIENT_ID` seulement | Oui, sans secret |
| Docusign | Apps and Keys, une clé d'intégration (PKCE ou secret), puis le formulaire MCP de Docusign pour la production et la revue Go-Live, de 24 à 48 h | `TF_MCP_DOCUSIGN_CLIENT_ID` (et `_CLIENT_SECRET` si la clé en a un) | Oui avec une clé PKCE `[HYPOTHÈSE]` pour MCP |
| Canva | Developer Portal, une intégration, « Canva MCP » sous « Outside Canva », l'adresse web ; le secret ne se montre qu'une fois | `TF_MCP_CANVA_CLIENT_ID`, `TF_MCP_CANVA_CLIENT_SECRET` | Non : un client sans secret passe par la liste d'attente de Canva |

Les demandes à faire une fois, sans application à créer :

- **Square** : entrer dans la liste des clients MCP de Square (forum des développeurs de Square, catégorie MCP). D'ici là,
  Square dit « Not available yet ».
- **Workable** : faire admettre les adresses de retour de TaskForce par le support de Workable. D'ici là, « Not available yet ».
- **Pipedrive** : faire admettre l'adresse de retour web (communauté des développeurs de Pipedrive) ; l'app desktop passe
  déjà `[TIERS]`.
- **Intercom** : faire admettre l'adresse de retour web par le support d'Intercom, une demande pour les serveurs américain et
  européen ; l'app desktop passe déjà (retour local sur tout port, lu le 10/11).
- **Facultatif** : une General app de TaskForce chez Zoom, soumise à la revue de Zoom, rendrait Zoom accessible en un clic à
  chaque compte ; aujourd'hui, l'administrateur de chaque entreprise crée la sienne. Une application de TaskForce chez
  PagerDuty, si PagerDuty la laisse servir d'autres comptes `[HYPOTHÈSE]`.

### Ce que fait chaque personne

| Chemin | Outils | Ce que fait la personne | Ce que fait l'administrateur de l'outil, une fois |
| --- | --- | --- | --- |
| Un clic | Trello, Productboard, Plane, Guru, Fireflies, Fathom, Granola, Otter.ai, tl;dv, Calendly, Netlify, Railway, CircleCI, Postman, MongoDB Atlas, PlanetScale, Jam, Datadog, New Relic, Honeycomb, incident.io, Rootly, Better Stack, Amplitude, Mixpanel, PostHog, Hex, ChartMogul, Supermetrics, Pipedrive, Close, Apollo.io, Clay, ZoomInfo, Gong, Klaviyo, Ramp, Brex, Mercury, Qonto, Expensify, FreshBooks, Airwallex, Deel, Gusto, Remote, Greenhouse, Miro, Lucid, Framer, Contentful, Vanta, Drata, Make, PandaDoc | « Connect », le navigateur, « Connected as … » ; « Also let Cortex propose changes » quand l'éditeur sépare la lecture de l'écriture | Rien d'ordinaire ; une note « If … refuses the connection: » dit sinon quoi faire : ouvrir MCP (Productboard, MongoDB Atlas, Mixpanel, Lucid, Miro en Enterprise), admettre l'adresse de retour (Datadog), installer l'application MCP dans chaque espace (Contentful), créer l'intégration (Gong) ou la configuration OAuth (Drata), choisir les portées (Greenhouse), activer Honeycomb Intelligence, accepter le contrat Developer API (Brex) |
| Notre application | HubSpot, Dropbox, Xero, Docusign (et Canva, Asana, GitHub MCP) | Un clic, une fois la Présidence passée chez l'éditeur | Rien ; sans nos variables, l'application de l'entreprise |
| L'application de l'entreprise | Box, Wrike, Zoom, PagerDuty | Un clic, après l'administrateur ; « Waiting for your admin » avant | La créer chez l'éditeur et la saisir une fois dans Settings, écran « Your company's app » |
| Une clé | Smartsheet, Render, Brevo (et les clés de secours de Fireflies, Postman, Jam, Rootly, Supermetrics, Deel, Cloudflare, Wrike, PagerDuty) | Créer la clé chez l'éditeur et la coller ; elle est rangée chiffrée | Rien ; la clé de Brevo a tous les droits du compte, celle de Render tous ses espaces |
| L'adresse du serveur de l'entreprise | Glean, Metabase (et Zoho) | Coller l'adresse, puis se connecter | Ouvrir MCP (Metabase : Admin, AI, MCP) |
| Fermé, avec la raison | Square, Workable (les listes ci-dessus) ; Snowflake, Databricks, Salesforce (une application et une adresse d'entreprise ensemble, que TaskForce ne prend pas encore) ; Figma (liste d'attente) | Rien : la carte dit « Not available yet », la fiche dit pourquoi | Rien aujourd'hui |

Une adresse européenne (Datadog, New Relic, Honeycomb, PagerDuty, Amplitude, Mixpanel, Vanta, Contentful, PandaDoc, Postman,
Smartsheet) se branche par « Connect an MCP server » et son adresse : le préréglage porte l'adresse américaine. Les noms des
outils de presque tous ces serveurs ne sont pas publiés : chacun demande avant d'agir tant qu'il n'est pas classé (R158),
sauf ceux que l'éditeur dit en lecture seule (tl;dv, Gong, Expensify, la requête de lecture de PlanetScale).

## Ce qui reste à vérifier à l'essai

1. **Une vraie connexion chez chaque éditeur** : la PR #523 a tout prouvé contre un faux éditeur, pas sur un compte réel ;
   seul Linear a été essayé, en septembre. Chaque outil s'essaie sur les comptes de la Présidence, après la release ; son
   `tried` (date, preuve) et son essai d'attaque (R158) viennent à la fin de J2, avec ces essais.
2. **Slack** : s'il accepte un retour sur `127.0.0.1`.
3. **Stripe** : la liste des adresses de retour admises, citée sur une page de place de marché ; un choix de lecture seule à
   la connexion.
4. **Docker** : le port, le chemin et les options de jeton de la passerelle.
5. **Slack, Zoho et Linear** : le nom de leurs outils, que ces éditeurs ne publient pas (Linear en nomme quelques-uns dans
   son journal des changements) ; les autres demandent jusqu'à ce que l'éditeur les documente. Asana publie les siens.
6. **Les ports de bouclage** : la règle de Notion, d'Atlassian (l'entrée `127.0.0.1` par défaut) et des GitHub Apps.
7. **Excalidraw** : ce que rend `create_view` à un client sans MCP Apps.
8. **Le reste** : la disponibilité générale de Notion, un premier accord d'un administrateur de site chez Atlassian, le
   client que donne l'inscription dynamique de GitLab, le plan et une clé en lecture seule chez Excalidraw+, si PKCE dispense
   Asana du secret.

Ce que les pages des éditeurs ne disent pas est au
[Registre des outils](./Registre_des_outils.md#ce-qui-na-pas-pu-être-vérifié).

---

**Points d'entrée :** [Registre des outils](./Registre_des_outils.md) · [Produit](./README.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [Séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)
