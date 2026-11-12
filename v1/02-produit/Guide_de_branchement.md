---
id: produit-guide-branchement
title: Guide de branchement de la première vague
doc_type: runbook
statut: active
version: 1.1
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

**Version :** 1.1 · **Date :** 12/11/2026 · **Auteur :** Pierre MICHEL

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
| Linear | Un clic | Essayé, le seul préréglage montré d'office |
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
| Teams | Rien dans ce lot | Lot suivant, payant chez Microsoft |
| OneDrive | Rien dans ce lot | Lot suivant (fichiers) |
| Google Drive | Rien dans ce lot | Lot suivant (fichiers) |

## Ce qui vaut pour tous

### Montrer les outils pas encore essayés

Le catalogue ne montre d'office que les intégrations natives (GitHub, Slack, Plane) et les préréglages essayés de bout en
bout, aujourd'hui Linear seul (R15, R153 ; `ConnectorCatalog.isShown`). Pour l'essai, `TF_CATALOG_SHOW_UNTRIED=true` les
montre tous :

- **App desktop** : une variable d'environnement de l'utilisateur Windows, puis relancer l'app ; la coque la passe au backend
  local (`desktop/src/backend.ts`).
- **Serveur** : la variable dans l'environnement du fichier compose de production, qui la transmet au backend
  (`docker-compose.prod.yml`) ; tous les espaces de l'instance voient alors les préréglages pas encore essayés.

Après l'essai réussi d'un outil, sa date et sa preuve entrent dans son champ `tried`, dans le fichier des préréglages : il se
montre alors à tous, sans la variable.

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

Seuls les éditeurs sans auto-inscription les demandent : ici Asana, Slack et une application OAuth de GitHub.

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
  (`McpClientRegistrar`). Sur le serveur, le fichier compose de production ne transmet que ces deux paires ; sur l'app
  desktop, ce sont des variables de l'utilisateur Windows, que la coque passe au backend local. Jamais dans le dépôt.
- **L'application de l'entreprise** (chemin C) : un propriétaire ou un administrateur la saisit dans Settings >
  Integrations > l'outil, écran « Your company's app » : « Client ID », « Client secret », « Save and connect ». Le secret est rangé
  chiffré, pour l'espace (`connector_app`).
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

**Rien dans ce lot.** La PR #523 laisse Google Drive au lot suivant (« fichiers : lire et ranger »), par l'API Drive plutôt
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

**Rien dans ce lot.** Laissé au lot suivant (« fichiers »), par Microsoft Graph. Le code ajoute une raison : TaskForce
refuse un serveur de connexion qui n'annonce pas PKCE S256, et les métadonnées d'Entra ne l'annoncent pas
([Entra](https://login.microsoftonline.com/organizations/v2.0/.well-known/openid-configuration)).

- Microsoft Entra n'offre pas non plus d'auto-inscription : ses métadonnées n'ont pas de `registration_endpoint` (même
  page) ; il faut une application enregistrée dans Entra.
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

- Non vérifié : un premier accord d'un administrateur du site, rapporté seulement par la communauté.

### Linear

**Un clic, déjà essayé**, le seul préréglage que le catalogue montre d'office (`tried` du 03/09/2026). Auto-inscription et
CIMD, PKCE ([métadonnées](https://mcp.linear.app/.well-known/oauth-authorization-server)). Sans « Also let Cortex propose
changes », TaskForce se branche sur l'adresse en lecture seule, `https://mcp.linear.app/mcp/readonly`
([Linear](https://linear.app/docs/mcp)).

1. TaskForce : Linear > « Connect ».
2. Chez Linear : accepter.
3. Retour : « Connected as … ».

- Si l'espace Linear approuve les applications tierces, un administrateur approuve TaskForce : Settings > Administration >
  Security > Third-party application approvals (texte du préréglage).
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
- Asana ne publie pas le nom de ses outils : chacun demande avant de servir, jusqu'à ce que l'essai les classe.
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

**Bloqué dans ce lot** : la PR #523 le laisse au lot suivant, et le chemin de Microsoft coûte.

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
- Et TaskForce refuserait aujourd'hui le serveur de connexion d'Entra, qui n'annonce pas PKCE S256 (voir OneDrive).

Ce qu'elle fera, quand le lot suivant le construira `[HYPOTHÈSE]` :
1. Dans son locataire Microsoft 365 : enregistrer l'application comme pour OneDrive, avec la permission déléguée de Work IQ
   (`WorkIQ.Read`) ou de Graph (`Chat.Read`), puis « Grant admin consent ».
2. Pour Work IQ seulement : en administrateur global, activer Work IQ et lui relier un plan de facturation.
3. L'identifiant de l'application dans TaskForce, là où le lot suivant le dira.

Avec un compte Microsoft personnel, Work IQ ne sert pas : il ne connaît que les comptes professionnels `[DÉDUIT]`.

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
  partage) et `save_checkpoint` ; `read_me`, `create_view` et `read_checkpoint` lisent.
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

## Ce qui reste à vérifier à l'essai

1. **Une vraie connexion chez chaque éditeur** : la PR #523 a tout prouvé contre un faux éditeur, pas sur un compte réel ;
   seul Linear a été essayé, en septembre. Chaque outil s'essaie sur les comptes de la Présidence, après la release ; il ne
   se montre qu'avec son `tried` (date, preuve) et son essai d'attaque (R153, R158).
2. **Slack** : s'il accepte un retour sur `127.0.0.1`.
3. **Stripe** : la liste des adresses de retour admises, citée sur une page de place de marché ; un choix de lecture seule à
   la connexion.
4. **Docker** : le port, le chemin et les options de jeton de la passerelle.
5. **Asana, Slack et Zoho** : le nom de leurs outils, que les éditeurs ne publient pas ; tous demandent jusqu'à ce que l'essai
   les classe.
6. **Les ports de bouclage** : la règle de Notion, d'Atlassian (l'entrée `127.0.0.1` par défaut) et des GitHub Apps.
7. **Excalidraw** : ce que rend `create_view` à un client sans MCP Apps.
8. **Le reste** : la disponibilité générale de Notion, un premier accord d'un administrateur de site chez Atlassian, le
   client que donne l'inscription dynamique de GitLab, le plan et une clé en lecture seule chez Excalidraw+, si PKCE dispense
   Asana du secret.

Ce que les pages des éditeurs ne disent pas est au
[Registre des outils](./Registre_des_outils.md#ce-qui-na-pas-pu-être-vérifié).

---

**Points d'entrée :** [Registre des outils](./Registre_des_outils.md) · [Produit](./README.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [Séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)
