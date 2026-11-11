---
id: produit-registre-outils
title: Registre des outils d'entreprise
doc_type: register
statut: active
version: 1.1
date: "11/11/2026"
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

**Version :** 1.1 · **Date :** 11/11/2026 · **Auteur :** Pierre MICHEL

La liste des applications qu'une entreprise utilise le plus, et pour chacune la façon dont TaskForce peut s'y brancher. La
Présidence l'a demandée le 10/11/2026 : « je devrais pouvoir faire un listing exhaustif de l'ensemble des applications
Enterprise Grade qui sont les plus utilisées [...] on peut commencer par ça », pour « se plug partout, si possible ».

- **Ce registre n'est pas le catalogue de l'app.** L'app ne montre un outil qu'une fois essayé de bout en bout (R15, R99,
  [séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md), R153). Le registre, lui, dit tout ce
  qu'on sait de chaque outil, essayé ou non.
- **Les faits** ont été lus le 10/11/2026 sur les pages des éditeurs, des études et des normes ; un lien par ligne, celui
  de la contrainte qui compte. Une case suivie de `[HYPOTHÈSE]` n'est pas écrite sur une page lue.
- **Les seize outils de la première vague** ont été relus le 11/11/2026, avec leurs métadonnées OAuth publiques. Ce que la
  Présidence fait pour brancher chacun, et le détail des liens, est au [Guide de branchement](./Guide_de_branchement.md).
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
| Google Drive (Docs, Sheets, Slides) | Okta n°2 (Workspace) | B | Pas d'auto-inscription : un projet Google Cloud, un client OAuth et son secret ; le serveur MCP de Drive est en Developer Preview, réservé aux membres du programme. La portée `drive.file` (les fichiers que la personne choisit ou que l'app crée) n'est pas sensible ; `drive.readonly` est restreinte : environ six semaines de vérification, un audit CASA par an, 100 personnes au plus en attendant. Construit au lot suivant (fichiers), par l'API Drive | 1 (lot suivant) | [Google](https://developers.google.com/workspace/drive/api/guides/api-specific-auth) |
| SharePoint, OneDrive | Okta n°1 (Microsoft 365) | C | Pas d'auto-inscription chez Entra. La politique par défaut retire `Files.Read.All` et `Sites.Read.All` du consentement des personnes, pas `Files.Read` (ses propres fichiers) : l'administrateur approuve le reste ; la vérification d'éditeur évite un blocage chez les autres entreprises. Work IQ (MCP) ne sert que les comptes professionnels, en crédits Copilot. Construit au lot suivant (fichiers), par Microsoft Graph | 1 (lot suivant) | [Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies) |
| Box | Okta Japon n°5 | B ou C | Notre application Box, ou l'intégration prédéfinie que l'administrateur active | 2 | [Box](https://developer.box.com/guides/box-mcp/remote/) |
| Dropbox | Cledara n°46 | B | L'approbation de production dans les deux semaines après 50 personnes, sinon les connexions gèlent | 2 | [Dropbox](https://docs.dropboxapi.com/dropbox-api/docs/developer-resources/developer-guide) |
| Egnyte | non classé | D | Une clé limitée à un domaine de test jusqu'à l'approbation d'Egnyte | plus tard | [Egnyte](https://developers.egnyte.com/integration/cfs/api-docs/getting-started) |
| Nextcloud (auto-hébergé) | non classé | C | L'administrateur installe l'agent de contexte ; un mot de passe d'application, pas d'OAuth | plus tard | [Nextcloud](https://docs.nextcloud.com/server/latest/admin_manual/ai/app_context_agent.html) |
| Amazon S3 (stockage du serveur) | Okta n°3 (AWS) | C | Des droits IAM et la politique d'accès du serveur MCP d'AWS | stockage | [AWS](https://docs.aws.amazon.com/agent-toolkit/latest/userguide/getting-started-aws-mcp-server.html) |

## Savoir et documentation

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Notion | Okta Japon n°9 | A | Auto-inscription (DCR ou CIMD) et PKCE, aucune revue écrite ; le serveur se dit en bêta dans ses métadonnées ; l'espace Enterprise peut n'accepter que des clients approuvés ; la connexion tient 180 jours au plus | 1 | [Notion](https://developers.notion.com/guides/mcp/build-mcp-client) |
| Confluence | Torii n°3 (Atlassian) | A | Un seul serveur Atlassian, GA, pour Confluence et Jira ; l'organisation n'admet que les retours de sa liste : `127.0.0.1` et `localhost` par défaut, le domaine de l'app web s'ajoute par l'administrateur | 1 | [Atlassian](https://support.atlassian.com/security-and-access-policies/docs/available-atlassian-rovo-mcp-server-domains/) |

## Tickets et projets

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Jira (et Jira Service Management) | Torii n°19 | A | Le serveur de Confluence ; supprimer et administrer restent coupés tant que l'administrateur ne les ouvre pas ; Jira Service Management par jeton d'API seulement | 1 | [Atlassian](https://github.com/atlassian/atlassian-mcp-server) |
| Linear | essayé dans TaskForce | A | Aucune revue ; DCR et CIMD ; une adresse en lecture seule | 1 (fait) | [Linear](https://linear.app/docs/mcp) |
| Asana | non classé | B ou C | Pas d'auto-inscription : une « MCP app » créée dans la console d'Asana, avec identifiant et secret, diffusée à des espaces choisis ou à tous ; toute portée autre que `default` est refusée | 1 (une étape) | [Asana](https://developers.asana.com/docs/integrating-with-asanas-mcp-server) |
| monday.com | non classé | A puis C | L'auto-inscription existe, mais chaque nouveau client attend l'administrateur du compte | 2 | [monday.com](https://developer.monday.com/api-reference/docs/mcp-dynamic-client-registration) |
| ClickUp | non classé | A `[HYPOTHÈSE]` | L'auto-inscription est annoncée, mais l'éditeur parle d'une liste de clients vérifiés | 2 | [ClickUp](https://clickup.com/blog/how-to-use-clickup-mcp-server/) |
| Smartsheet | non classé | B | Un secret et des retours HTTPS seulement | plus tard | [Smartsheet](https://developers.smartsheet.com/api/smartsheet/guides/advanced-topics/oauth) |
| Trello | non classé | Aucun | Pas de serveur MCP officiel ; une API OAuth avec PKCE annoncée le 15/09/2026 | plus tard | [Atlassian](https://community.developer.atlassian.com/t/oauth-2-0-3lo-is-now-available-for-trello/102691) |

## Messagerie, mail et réunions

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Slack | Okta n°6 | B ou C | Le serveur MCP n'accepte que les applications publiées (revue jusqu'à dix semaines) ou internes à l'entreprise, avec identifiant et secret, sans auto-inscription, MCP allumé application par application ; les conditions interdisent l'entraînement d'un modèle et les copies durables des données d'autres organisations | 1 (l'application interne) | [Slack](https://docs.slack.dev/ai/slack-mcp-server/) |
| Microsoft Teams | Torii n°12 | C | Work IQ (MCP) : comptes professionnels seulement ; un administrateur global l'active avec une facturation à l'usage en crédits Copilot, et ses permissions demandent l'administrateur. Par Graph, `Chat.Read` hors du consentement par défaut. Construit au lot suivant | 1 (lot suivant, payant) | [Microsoft](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/enable-work-iq) |
| Outlook | Torii n°18 | C | `Mail.Read` et `Calendars.Read` hors du consentement par défaut | 2 | [Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies) |
| Google Calendar | Okta n°2 (Workspace) | B | Des portées sans doute sensibles `[HYPOTHÈSE]` | 2 | [Google](https://developers.google.com/workspace/guides/configure-mcp-servers) |
| Gmail | Okta n°2 (Workspace) | B | `gmail.readonly` est restreinte : vérification et audit | plus tard | [Google](https://developers.google.com/workspace/gmail/api/auth/scopes) |
| Zoom | Okta n°5 | B | Inscription manuelle seulement ; une revue pour les autres comptes | plus tard | [Zoom](https://developers.zoom.us/docs/mcp/servers/connect-to-zoom-mcp-servers/) |

## Code

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| GitHub | Okta n°8 | B | Déjà intégré (application OAuth ; GitHub CLI dans l'app desktop) ; les organisations récentes restreignent les applications OAuth : le propriétaire approuve ; le serveur MCP distant demande une application par hôte, ou un jeton | 1 (existant) | [GitHub](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/about-oauth-app-access-restrictions) |
| GitLab | Ramp n°5 (nouvelles dépenses) | A | GA depuis la 19.5, sur tous les plans ; l'auto-inscription crée une application sur l'instance ; l'accès MCP est ouvert par défaut aux groupes de premier niveau, sauf si un propriétaire l'a fermé ; en auto-hébergé, l'administrateur de l'instance l'ouvre | 1 | [GitLab](https://docs.gitlab.com/user/group/access_and_permissions/) |
| Bitbucket Cloud | non classé | A | L'espace doit être relié à une organisation Atlassian | 2 | [Atlassian](https://github.com/atlassian/atlassian-mcp-server) |
| Azure DevOps | non classé | C | Une application Entra avec le consentement de l'administrateur | plus tard | [Microsoft](https://learn.microsoft.com/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops) |
| Docker Hub | non classé | Aucun | Ajouté par la Présidence le 11/11/2026. Pas de serveur distant : le serveur officiel tourne sur le poste (stdio, ou HTTP local protégé par un jeton) et lit Docker Hub avec un jeton d'accès personnel, sans OAuth ; branchable sur l'app desktop seulement, par une adresse locale et un jeton copié | 1, app desktop par un jeton (hors du clic) | [Docker](https://github.com/docker/hub-mcp) |

## Ventes et relation client

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Salesforce | Okta n°4 | C | L'administrateur crée l'application et active chaque serveur ; la création d'applications connectées est coupée par défaut depuis Spring '26 | 2 | [Salesforce](https://www.salesforce.com/blog/?p=136995) |
| HubSpot | Cledara n°19 | B puis C | Un administrateur du compte connecte d'abord ; une application non listée s'installe 25 fois au plus | 2 | [HubSpot](https://developers.hubspot.com/changelog/new-marketplace-distribution-app-install-limits) |
| Pipedrive | non classé | D | Un serveur MCP depuis le 30/06/2026 ; l'inscription n'est pas décrite | plus tard | [Pipedrive](https://www.pipedrive.com/en/newsroom/pipedrive-launches-native-mcp-server-bringing-crm-workflows-directly-into-ai-assistants) |
| Zoho CRM | non classé | C | Chaque entreprise crée son propre serveur MCP dans la console de Zoho, avec les outils choisis ; son URL vaut une clé (« Regenerate API Key ») ; ensuite OAuth 2.1, chaque personne avec son compte par défaut | 1 (une étape) | [Zoho](https://www.zoho.com/mail/help/mcp/mcp-server-configuration.html) |
| Dynamics 365 | non classé | C | L'administrateur active MCP et chaque client | plus tard | [Microsoft](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-disable) |
| Stripe | non classé | A | Ajouté par la Présidence le 11/11/2026 (« Stripe aussi important »). Auto-inscription (DCR), PKCE, révocation, portée `mcp` ; la personne choisit à la connexion ses comptes, réels ou de test, et leurs droits ; un administrateur peut couper MCP pour l'équipe ; déjà parmi les préréglages MCP de TaskForce | 1 | [Stripe](https://docs.stripe.com/mcp) |

## Support et services informatiques

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Intercom | Cledara n°36 | A | Auto-inscription, retours locaux sur tout port | 2 | [Intercom](https://developers.intercom.com/docs/guides/mcp) |
| Zendesk | Cledara n°37 | Aucun | MCP annoncé le 19/05/2026, en accès anticipé ; l'API accepte PKCE, mais une application pour plusieurs clients demande un client global créé par Zendesk | 2 | [Zendesk](https://developer.zendesk.com/documentation/marketplace/building-a-marketplace-app/set-up-a-global-oauth-client/) |
| ServiceNow | Vertice n°8 | C | L'administrateur inscrit chaque client ; Now Assist requis | plus tard | [ServiceNow](https://www.servicenow.com/docs/r/platform-security/authentication/cimd-inbound-integration-workflow.html) |
| Freshworks (Freshdesk, Freshservice) | non classé | D | Freshdesk : une clé d'API ; Freshservice : une clé ou OAuth | plus tard | [Freshdesk](https://support.freshdesk.com/support/solutions/articles/50000012670) |

## Ressources humaines, finance et ERP

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| SAP | Vertice n°4 | Aucun | Pas de serveur hébergé par SAP ; le client le construit sur sa propre plateforme | plus tard | [SAP](https://developers.sap.com/tutorials/integration-suite-mcp-server/) |
| Workday | Vertice n°6 | C | Outils MCP en accès anticipé ; l'agent est inscrit par le client et passe par la passerelle de Workday | plus tard | [Workday](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/workday-agent-gateway-for-partner-agents.html) |
| Oracle NetSuite | Vertice n°9 (PME) | C puis D | L'administrateur active les fonctions et installe l'application ; ensuite « tout client », avec PKCE | plus tard | [Oracle](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_4160616848.html) |
| QuickBooks Online | Zylo n°4 | Aucun | Un serveur local seulement ; un retour HTTPS public exigé en production | plus tard | [Intuit](https://github.com/intuit/quickbooks-online-mcp-server) |
| Xero | Cledara n°10 | D | PKCE sans secret ; un plafond de connexions selon le plan ; les conditions interdisent d'entraîner une IA sur les données | plus tard | [Xero](https://developer.xero.com/pricing) |
| Odoo | non classé | Aucun | Une API par clé, réservée aux plans « Custom » | plus tard | [Odoo](https://www.odoo.com/pricing-plan) |

## Design et collaboration

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Figma | Okta n°11 | B | Seuls les clients du catalogue de Figma ; les nouveaux passent par une liste d'attente. Le serveur de l'app Figma (`127.0.0.1:3845`), sans connexion, demande un siège Dev ou Full sur un plan payant et n'écrit pas | hors de la vague 1 (liste d'attente, R153) ; le serveur local sur l'app desktop | [Figma](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation) |
| Canva | Zylo n°3 | B | Une application créée chez Canva ; les clients sans secret sur liste d'attente | plus tard | [Canva](https://www.canva.dev/blog/developers/canva-mcp-ga/) |
| Miro | Cledara n°28 | A | MCP parfois coupé en Enterprise jusqu'à l'administrateur | 2 | [Miro](https://developers.miro.com/docs/miro-mcp-server-frequently-asked-questions) |
| Excalidraw | non classé | A | Ajouté par la Présidence le 11/11/2026. Serveur officiel public, sans compte ni OAuth ; ses dessins ne s'affichent que dans un client qui gère les MCP Apps ; un outil publie le dessin sur excalidraw.com | 1 (branchable, dessins non affichés) | [Excalidraw](https://github.com/excalidraw/excalidraw-mcp) |

## Autres

| Outil | Adoption | Chemin | Ce qu'il faut | Vague | Source |
| --- | --- | :--: | --- | :--: | --- |
| Airtable | Cledara n°49 | A | Une liste blanche de clients possible en Enterprise | 2 | [Airtable](https://support.airtable.com/docs/using-the-airtable-mcp-server) |
| DocuSign | Torii n°20 | B | Les clients personnalisés passent par une liste blanche ; une revue de mise en production de 24 à 48 h | plus tard | [DocuSign](https://www.docusign.com/blog/developers/docusign-mcp-server-general-availability) |

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

---

**Points d'entrée :** [Produit](./README.md) · [Guide de branchement](./Guide_de_branchement.md) · [Feuille de route](../13-roadmap/Roadmap_Backlog.md) · [Séance n°22](../../recherche/conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)
