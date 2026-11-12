---
id: conseil-seance-2026-11-11-se-brancher-a-l-entreprise
title: "Séance n°22 du 11/11/2026 : le lancement de J2, se brancher à l'entreprise (ses outils, son stockage, ses règles) et les critères de sortie"
doc_type: pv-seance
statut: active
date: "11/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, j2, connecteurs, mcp, oauth, stockage, regles, securite]
related:
  - "../README.md"
  - "./2026-11-10-premier-client-e20.md"
  - "./2026-11-01-feuille-de-route.md"
  - "../../../v1/02-produit/Registre_des_outils.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
  - "../../decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
---

# Séance n°22 du 11/11/2026 : le lancement de J2, se brancher à l'entreprise

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

La Présidence lance J2 et précise sa demande : TaskForce se branche à n'importe quel outil de l'entreprise, pas seulement à
Google Drive, en un clic ; l'entreprise choisit où TaskForce range ce qu'il écrit ; elle écrit ses propres règles au-dessus
des nôtres. Elle demande d'abord la liste exhaustive des outils d'entreprise les plus utilisés : le secrétariat l'a dressée
pour la séance, 46 outils, dans le [Registre des outils](../../../v1/02-produit/Registre_des_outils.md).

Le dossier tient en deux constats.
- **Côté produit**, la moitié du chemin existe : le client MCP et la connexion en un clic avec inscription automatique.
  Mais une connexion vaut pour tout l'espace, avec les droits de qui l'a faite ; les agents de code n'atteignent aucun outil ;
  le stockage se choisit une fois par installation ; personne ne peut écrire de règle.
- **Côté éditeurs**, le clic dépend de l'inscription : sept éditeurs laissent toute application s'inscrire seule (Notion,
  Atlassian, Linear, GitLab, Miro, Airtable, Intercom). Google demande une vérification de six semaines et un audit annuel
  pour lire tout un Drive, sauf pour les fichiers que la personne choisit. Microsoft 365 demande l'accord de l'administrateur.
  L'injection par un contenu lu n'est résolue nulle part.

Le Conseil adopte sept recommandations :
- les critères de sortie de J2, chiffrés avant de construire (Arati Prabhakar) ;
- le registre exhaustif et public, et une première vague de huit outils essayés de bout en bout ;
- un clic pour la personne, quatre chemins derrière, une connexion par personne, et aucun jeton relayé par notre serveur ;
- lire sans tout copier ;
- ranger où l'entreprise le choisit ;
- les règles de l'entreprise par couches, au-dessus d'un socle qu'aucune ne relâche ;
- la sécurité des connecteurs.

Yoshua Bengio, contradicteur, a obtenu qu'aucun outil ne devienne visible avant son essai d'attaque. R153 et R154 ont
passé au second tour. La Présidence les retient toutes le jour même : le flux peut demander une étape à l'entreprise,
pourvu qu'il soit clair ; la première vague s'élargit aux outils où elle peut se connecter.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 10/11/2026, en conversation) :
  - « Ok, go, on peut attaquer J2. Après, quand je te dis Google Drive, retiens bien que ça peut être n'importe quel outil que
    l'entreprise utilise. Donc, je devrais pouvoir faire un listing exhaustif de l'ensemble des applications Enterprise Grade qui
    sont les plus utilisées, par exemple. Hein, on peut commencer par ça. Et pouvoir les intégrer directement dans Task Force pour
    une connexion rapide et simple. Je dis par là donc certainement un clic pour connecter, ça ouvre l'application, on se
    connecte, retourner dans Task Force et bim, c'est connecté. » ;
  - « Mais voilà, l'idée c'est vraiment de pouvoir se plug partout, si possible. Donc voilà, faut pas se fixer juste sur, sur
    Google Drive ou juste l'environnement Google, quoi. C'est pas scalable ça comme, comme pensée, quoi. » ;
  - « Mais avant, je préfère valider que le concept de l'application fonctionne, que c'est utile et que ça peut servir à une
    entreprise de manière vraiment exhaustive et pas juste comme ça pour faire beau, quoi. » ;
  - et, le même jour, sa décision sur la [séance n°21](./2026-11-10-premier-client-e20.md) : le stockage au choix de
    l'entreprise, ses propres règles « toujours encadré par quelque chose que nous, on contrôle ».
- **Horizon** : J2, la première version qu'une entreprise peut utiliser.
- **Formation** : restreinte (7), au moins un membre par pôle.
  - Impulsion : Elon Musk (les premiers principes, supprimer ce qui ne sert pas).
  - Pont : Satya Nadella (les agents en entreprise, l'identité, les contrôles hors du modèle) ; Arati Prabhakar (les
    programmes à haut risque et leurs critères de passage).
  - Harmonie : Nandan Nilekani (les protocoles ouverts, le consentement).
  - Science : Yoshua Bengio (la sûreté des agents) ; Margaret Hamilton (la fiabilité, les modes de panne).
  - Design : Karri Saarinen (l'interface d'un outil de travail).
- **Ordre de parole**, tiré au sort le 11/11/2026 à 09:49 UTC : Nandan Nilekani, Elon Musk, Karri Saarinen, Satya Nadella,
  Margaret Hamilton, Arati Prabhakar, Yoshua Bengio.
- **Contradicteur** : Yoshua Bengio.
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à sept.
- **Fiches** : à jour (moins de 30 jours) : Saarinen au 28/10/2026 ; Musk, Nadella, Prabhakar, Nilekani et Bengio au 21/10 ;
  Hamilton, siège historique, sans nouvelle source. Aucune fiche rafraîchie.

## Dossier

### 1. Ce que TaskForce sait faire aujourd'hui `[ÉTABLI]`

Lu dans le code de `dev` le 10/11/2026.

- **Trois sortes de connecteurs** : GitHub, Slack et Plane, écrits à la main ; 25 serveurs MCP préréglés, dont un seul essayé
  (Linear) ; tout autre serveur MCP, ajouté par son adresse. Le catalogue montre Plane, GitHub, Slack et Linear.
- **La connexion en un clic existe pour MCP**, côté serveur : découverte de l'autorisation, inscription automatique (DCR,
  obligatoire chez nous), PKCE, rafraîchissement du jeton. Il n'y a ni application pré-enregistrée chez un éditeur, ni
  inscription par document de métadonnées (CIMD), et l'app desktop n'a pas ses adresses de retour pour ce chemin.
- **Une connexion vaut pour tout l'espace**, faite par un propriétaire ou un administrateur, et tous les membres passent par
  elle : chacun lit dans l'outil avec les droits de qui l'a branché `[DÉDUIT]`.
- **Lire** : Cortex interroge les outils en direct ; rien n'est indexé, sauf les synchronisations manuelles de GitHub, Slack et
  Plane. **Les agents de code n'atteignent aucun connecteur.**
- **Les règles** : le format prévoit un paquet par espace (V102), mais rien ne permet de l'écrire, et il n'y a pas de couche
  par projet. Lecture ou écriture : la classe d'un outil externe vient de ce que l'outil déclare de lui-même. Deux gestes
  d'administration ne passent pas par le moteur de règles.
- **Le stockage** des fichiers se choisit une fois par installation (un stockage S3 sur le serveur, le disque sur l'app
  desktop), jamais par espace.
- **Déconnecter** efface le jeton chez nous, sans le révoquer chez l'éditeur.

### 2. Les outils des entreprises `[ÉTABLI]`

Lu le 10/11/2026 ; le détail, outil par outil, avec un lien par ligne, est au
[Registre des outils](../../../v1/02-produit/Registre_des_outils.md).

- **L'adoption** : n°1 Microsoft 365, n°2 Google Workspace, n°3 AWS, n°4 Salesforce, n°5 Zoom, n°6 Slack, n°8 GitHub, n°11
  Figma ; 98 applications par entreprise en moyenne, 83 en France
  ([Okta, 2026](https://www.okta.com/ja-jp/newsroom/press-releases/okta-businesses-at-work2026/)). Atlassian revient dans les
  autres classements.
- **Quatre chemins de connexion**, selon l'éditeur :
  - **A, l'auto-inscription** : Notion, Atlassian (Confluence, Jira, Bitbucket), Linear, GitLab, Miro, Airtable, Intercom ;
  - **B, une application enregistrée chez l'éditeur** : Google, GitHub, Slack, Zoom, Asana, HubSpot, Dropbox, Box, Figma,
    Canva, DocuSign ;
  - **C, l'administrateur d'abord** : Microsoft 365 et Dynamics, Salesforce, ServiceNow, Workday, SAP, Zoho ;
  - **aucun serveur ouvert** : Trello, Odoo, QuickBooks, et Zendesk tant que son serveur est en accès anticipé.
- **Google** : lire tout un Drive est une portée « restreinte », avec environ six semaines de vérification, un audit CASA par an
  et 100 personnes au plus en attendant ; la portée `drive.file`, limitée aux fichiers que la personne choisit, n'est pas
  sensible ([Google](https://developers.google.com/workspace/drive/api/guides/api-specific-auth),
  [FAQ](https://support.google.com/cloud/answer/13463817)).
- **Microsoft 365** : la politique par défaut retire du consentement des personnes la lecture de tous les fichiers, des
  sites, du mail, de l'agenda et des discussions ; l'administrateur approuve
  ([Microsoft](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-app-consent-policies)).
- **Slack** : son serveur MCP n'accepte que les applications publiées ou internes à l'entreprise
  ([Slack](https://docs.slack.dev/ai/slack-mcp-server/)), et ses conditions interdisent l'entraînement d'un modèle et les copies
  durables des données d'autres organisations ([conditions](https://slack.com/terms-of-service/api)).
- **La norme MCP du 28/07/2026** préfère CIMD et rend DCR dépréciée, gardée au moins douze mois ; PKCE obligatoire
  ([MCP](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization/client-registration)). Une extension
  laisse l'annuaire de l'entreprise autoriser les connexions (EMA) ; Keycloak la porte à titre expérimental depuis la 26.7.0
  ([MCP](https://modelcontextprotocol.io/extensions/auth/enterprise-managed-authorization)).
- **Aucune plateforme de connecteurs ouverte et neutre** : Nango est sous Elastic License 2.0, et son auto-hébergement gratuit
  ne couvre que l'authentification et le relais ([Nango](https://nango.dev/docs/guides/platform/self-hosting/self-hosting.md)) ;
  les autres sont commerciales, ou réservent l'auto-hébergement à leur offre Enterprise.
- **Une app desktop** se connecte par le navigateur du système, un retour sur `127.0.0.1` et PKCE, jamais par une fenêtre
  intégrée ([RFC 8252](https://www.rfc-editor.org/rfc/rfc8252.html)) : c'est déjà le chemin de la connexion à TaskForce.
- **L'injection n'est pas résolue** :
  - une issue publique a fait sortir des données privées dans une pull request publique par le serveur MCP de GitHub
    ([Invariant, 26/05/2025](https://invariantlabs.ai/blog/mcp-github-vulnerability)) ;
  - un ticket a fait écrire des jetons dans le ticket lui-même ([General Analysis, 08/07/2025](https://www.generalanalysis.com/blog/supabase-mcp-blog)) ;
  - des jetons OAuth volés ont vidé des instances Salesforce
    ([Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence/data-theft-salesforce-instances-via-salesloft-drift)) ;
  - Meta recommande qu'un agent ne réunisse jamais plus de deux de ces trois choses : un contenu non fiable, des données
    sensibles, une action qui change un état ou communique au-dehors ([Meta](https://ai.meta.com/blog/practical-ai-agent-security/)).

### 3. Les décisions en vigueur

R1 (aucun agent ne décide seul d'une action irréversible) ; R15 (on ne montre que ce qui marche) ; R93 (on sait où va chaque
donnée) ; R94 (le métier construit son outil) ; R96 (un contexte juste, l'agent qui demande) ; R98 (des règles complètes, avec
leurs cas) ; R99 (MCP pour agir, un manifeste pour lire, rien de visible avant essai) ; ADR-024 (une seule surface d'outils pour
tous les agents) ; R147, élargie par la Présidence le 10/11, et R148 ; la trifecta de la séance n°8.

## Tour de table `[HYPOTHÈSE]`

- **Nandan Nilekani** (Harmonie) : une connexion est un consentement : qui donne quoi, à qui, pour quoi, jusqu'à quand. Elle se
  donne, se voit, se retire, et laisse une trace. Les données restent où elles sont ; on y va avec la permission, on ne les
  déménage pas. Et un protocole ouvert vaut mieux qu'une plateforme : il survit à son éditeur. *Sa recommandation : chaque
  connexion est un consentement nominatif, limité, révocable et journalisé.*
- **Elon Musk** (Impulsion) : la moitié existe déjà, le client MCP et la connexion avec découverte. Écrire quarante-six
  intégrations à la main serait l'erreur : un seul chemin, générique, sur les normes, et on supprime ce qui n'a pas servi. Une
  première vague en jours, pas en mois. *Sa recommandation : étendre ce qu'on a, et aucune intégration écrite à la main de
  plus.*
- **Karri Saarinen** (Design) : le geste tient en quatre temps : « Connect », le navigateur, le retour, « Connected as … ».
  L'état se voit toujours : branché, à reconnecter, en attente de l'administrateur. L'étape de l'administrateur se dit en une
  phrase, avec un lien à lui envoyer. Et le catalogue se range par ce qu'on fait (documents, tickets, code, discussions), pas
  par le nom des éditeurs. *Sa recommandation : un geste, trois états, jamais un jeton à l'écran.*
- **Satya Nadella** (Pont) : Microsoft 365 et Google Workspace sont en tête de toutes les listes ; sans eux, il n'y a pas
  d'entreprise. Leur réalité, c'est un administrateur qui approuve une fois. Ensuite, chaque personne agit avec ses propres
  droits, la gouvernance vit hors du modèle, et le journal se lit sans l'agent. *Sa recommandation : l'administrateur une
  fois, puis un clic par personne, avec ses droits.*
- **Margaret Hamilton** (Science, siège historique) : un connecteur tombe en panne. Le jeton expire en pleine mission,
  l'éditeur change son API, une limite de débit coupe la lecture. Le système doit le savoir avant, le dire, et se replier sans
  rien casser. Chaque connecteur a ses essais, rejoués à chaque changement. *Sa recommandation : un état de santé par outil,
  une vérification avant chaque mission, des essais de contrat.*
- **Arati Prabhakar** (Pont) : J2 est un programme à haut risque. On écrit les seuils de passage avant de construire, on
  mesure, et on arrête ce qui ne les tient pas. Sans critère écrit, J2 durera jusqu'à la fatigue. *Sa recommandation : dix
  critères chiffrés, et pour chacun un oui ou un non.*
- **Yoshua Bengio** (Science, contradicteur) : se brancher partout, c'est ouvrir autant de portes d'entrée. Les fuites
  documentées sont passées par une issue, un ticket, un document : un contenu lu, que l'agent a pris pour une consigne. Un
  agent qui lit un ticket piégé, voit des données privées et peut écrire au-dehors réunit tout ce qu'il faut pour une fuite.
  *Sa recommandation : le moindre privilège, jamais les trois à la fois sans une personne, et un essai d'attaque avant chaque
  outil visible.*

## Confrontation `[HYPOTHÈSE]`

1. **Construire ou acheter ?** Nadella évoque une plateforme du marché pour couvrir plus d'outils plus vite. Nilekani et Bengio
   refusent un tiers dans le chemin des jetons et des données ; Musk rappelle que la moitié existe. Accord : notre couche, sur
   les normes ouvertes (MCP du 28/07/2026, RFC 8252), sans plateforme tierce dans le chemin des données ; Keycloak, déjà dans le
   produit, est étudié pour l'autorisation par l'annuaire de l'entreprise.
2. **Une connexion pour l'espace, ou pour chaque personne ?** Musk préfère une connexion par espace, plus simple. Nilekani et
   Nadella répondent qu'alors chacun lit avec les droits de qui a branché. Accord : une connexion par personne par défaut ; une
   connexion d'espace seulement pour une source partagée, visible comme telle.
3. **Un relais pour les éditeurs qui exigent un secret ?** Musk le veut pour couvrir plus d'outils. Bengio et Nilekani refusent
   qu'un jeton passe par notre serveur. Premier tour de R154 : 6 pour, 1 contre (Bengio). Amendement : aucun relais en J2 ; ces
   éditeurs passent par l'application de l'entreprise, ou attendent.
4. **Indexer ou lire en direct ?** Hamilton veut une copie, pour tenir quand l'outil tombe. Nilekani rappelle les conditions des
   éditeurs, Slack interdit les copies durables, et la souveraineté de l'entreprise. Accord : en direct par défaut ; indexé
   seulement avec l'accord de l'entreprise, si l'éditeur le permet ; la fiche de la source dit lequel.
5. **L'exhaustif contre la sécurité.** La Présidence veut tous les outils ; Bengio refuse un catalogue qui grandit plus vite
   que ses essais d'attaque. Premier tour de R153 : 6 pour, 1 contre (Bengio). Amendement : le registre est exhaustif et
   public ; l'app ne montre un outil qu'après ses essais de contrat et son essai d'attaque.

## Recommandations `[HYPOTHÈSE]`

### R152. Les critères de sortie de J2, écrits avant

- **Quoi** : J2 se termine quand chacun de ces critères est tenu, mesuré sur l'app desktop :
  1. **se brancher** : depuis un espace neuf, chaque outil de la première vague se connecte en un clic, sans copier ni jeton
     ni identifiant, en moins d'une minute ;
  2. **lire** : dix questions sur l'outil de base de l'essai, au moins huit réponses justes, citées au passage près, avec la
     version de la source ;
  3. **ranger** : un document écrit par TaskForce arrive dans le stockage choisi par l'espace, après accord, et le dossier dit
     où ;
  4. **l'environnement** : la fiche validée par une personne ; trois missions qui emploient ses commandes ;
  5. **les règles** : une règle écrite en mots par l'entreprise passe ses cas ; une règle qui tente de relâcher le socle est
     refusée ;
  6. **le processus** « intégrer un module » se déroule de bout en bout, chaque étape accordée par qui de droit, et reprend
     après un redémarrage ;
  7. **le dossier** signé se vérifie par un programme indépendant, hors de TaskForce ;
  8. **les erreurs bêtes** : sur trois missions, deux erreurs semées sont attrapées avant d'arriver ;
  9. **la sécurité** : un document piégé dans un outil branché ne fait sortir aucune donnée, et la tentative est au dossier ;
  10. **le rituel de R105** : tests verts, liste de lancement verte, trois personnes extérieures d'au moins deux métiers, et la
      mesure de départ de l'indice de confiance (E17).
  E20 se joue ensuite.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : les critères relus par la Présidence, chacun avec sa mesure.
- **Signal d'arrêt** : un critère qu'on ne sait pas mesurer ; il se réécrit avant de construire.

### R153. Le registre exhaustif, et une première vague essayée (second tour)

- **Quoi** :
  - le [Registre des outils](../../../v1/02-produit/Registre_des_outils.md) est la liste exhaustive : chaque outil avec son
    adoption, son chemin de connexion, ce qu'exige l'éditeur et son état chez nous. Il est public, revu chaque trimestre ;
  - l'app ne montre un outil qu'après ses essais de contrat (R99) et son essai d'attaque (R158) ; il a alors un état de santé
    visible ;
  - **la première vague de J2**, huit outils pour les documents, le savoir, les tickets et le code : Google Drive, SharePoint et
    OneDrive, Notion, Confluence, Jira, GitLab, avec GitHub et Linear déjà branchés ;
  - **la vague suivante** : la messagerie et l'agenda (Slack, Teams, Outlook, Google Calendar), le stockage (Box, Dropbox), la
    relation client (Salesforce, HubSpot), les projets (Asana, monday.com, ClickUp), le support (Intercom, Zendesk), Miro,
    Airtable, Bitbucket ; le reste à la demande d'un client.
- **Premier tour** (sans essai d'attaque avant d'être visible) : 6 pour, 1 contre (Bengio). **Second tour**, amendé : les sept.
- **Preuve en dix jours** : les huit outils branchés en un clic depuis un espace neuf, chacun en moins d'une minute.
- **Signal d'arrêt** : un outil de la première vague bloqué par son éditeur (revue, liste d'attente) ; il sort de la vague, la
  raison au registre.

### R154. Un clic pour la personne, quatre chemins derrière (second tour)

- **Quoi** :
  - pour la personne, toujours le même geste : un clic, le navigateur, la connexion, le retour, « Connected as … » ; trois états
    visibles : branché, à reconnecter, en attente de l'administrateur ;
  - derrière, TaskForce prend le chemin que l'éditeur permet : **A**, l'auto-inscription (CIMD, puis DCR) ; **B**, notre
    application enregistrée chez l'éditeur ; **C**, l'application de l'entreprise, que son administrateur crée ou approuve une
    fois, guidé par un assistant et un lien à lui envoyer ; **D**, en dernier recours, une clé d'API, guidée ;
  - pour Google Drive, la portée des fichiers que la personne choisit, sans vérification restreinte ;
  - **une connexion par personne**, avec ses propres droits dans l'outil ; une connexion d'espace seulement pour une source
    partagée, visible comme telle ;
  - sur l'app desktop : le retour sur `127.0.0.1` et PKCE, comme la connexion à TaskForce ; les jetons protégés par le système ;
  - déconnecter révoque chez l'éditeur ;
  - **aucun jeton relayé par notre serveur** en J2.
- **Premier tour** (avec un relais pour les éditeurs qui exigent un secret) : 6 pour, 1 contre (Bengio). **Second tour**, sans
  relais : les sept.
- **Preuve en dix jours** : Notion (A), Google Drive (B) et SharePoint (C) branchés en un clic sur l'app desktop.
- **Signal d'arrêt** : un chemin qui demande à la personne de copier un jeton ou un identifiant.

### R155. Lire sans tout copier

- **Quoi** : TaskForce lit en direct par défaut. Il n'indexe une source qu'avec l'accord de l'entreprise, et si les conditions
  de l'éditeur le permettent. Chaque source a sa fiche (R96) : version, responsable, date de validité, classe de donnée,
  provenance, lue en direct ou indexée. Les droits de la source suivent la personne. Les agents de code atteignent les outils
  par la surface MCP de TaskForce (ADR-024), sous les mêmes règles.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : une question sur une page Notion et un ticket Jira, la réponse citée avec sa version ; l'agent de
  code lit le même ticket par TaskForce.
- **Signal d'arrêt** : une réponse qui cite ce que la personne ne peut pas lire dans l'outil.

### R156. Ranger où l'entreprise le choisit

- **Quoi** : chaque espace, et chaque projet s'il le veut, choisit où TaskForce range ce qu'il écrit : sur la machine (un
  dossier choisi), dans le stockage de l'entreprise (Google Drive, OneDrive ou SharePoint, Box, Dropbox, Nextcloud), ou sur le
  serveur. Écrire chez l'entreprise est une sortie (R93) : TaskForce demande, et le dossier dit où vit chaque document.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : le même compte rendu rangé sur la machine, puis dans un Google Drive, puis sur OneDrive, chaque fois
  avec l'accord et la trace.
- **Signal d'arrêt** : un document écrit hors de la cible choisie.

### R157. Les règles de l'entreprise, par couches, au-dessus d'un socle

- **Quoi** :
  - **le socle**, écrit dans notre code, ne se relâche jamais : R1 ; aucun secret ne sort ; jamais les trois éléments de R158 à
    la fois sans une personne ; TaskForce classe lui-même chaque outil en lecture ou en écriture ; chaque geste, d'une personne
    ou d'un agent, passe par le moteur et entre au dossier ;
  - **au-dessus**, les couches de l'entreprise : l'organisation, le projet, le processus, la personne ou son rôle. Une couche
    ne peut que durcir celle du dessous : demander au lieu de permettre, refuser au lieu de demander, ajouter un accord, un
    seuil, une double signature ;
  - une règle s'écrit en mots (R94), se traduit dans le format des règles, passe ses cas (R98), puis entre versionnée et signée
    au dossier. Jamais de JSON à l'écran.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : « aucun changement dans le module comptable sans l'accord de la responsable », écrite en mots ; ses
  cas passent ; une règle qui tente de permettre une action irréversible sans personne est refusée.
- **Signal d'arrêt** : l'essai contradictoire trouve une règle d'entreprise qui relâche le socle.

### R158. La sécurité des connecteurs

- **Quoi** :
  - **le moindre privilège** : la lecture par défaut, les portées strictement utiles, l'écriture demandée outil par outil ;
  - **un contenu lu est une donnée**, jamais une consigne ;
  - **jamais les trois à la fois sans une personne** : un contenu non fiable, des données sensibles, une écriture ou une
    communication au-dehors ;
  - **la liste des outils est figée** à la connexion : une description qui change redemande l'accord ;
  - les jetons rangés par émetteur, renouvelés, révoqués à la déconnexion ; aucun chemin hors du moteur de règles.
- **Pour** : les sept ; Musk note le coût d'un essai d'attaque par outil. **Contre** : aucun.
- **Preuve en dix jours** : un document piégé dans un outil branché tente de faire sortir une donnée ; rien ne sort, et la
  tentative est au dossier.
- **Signal d'arrêt** : une seule donnée sortie pendant l'essai ; l'outil ne devient pas visible.

## Décision de la Présidence

Tranchée le 11/11/2026, en conversation : « Je retiens les 7 reco c'est ok ».

- **R152, retenue** : « Chiffre alors oui va falloir chiffrer les resultats attendue ».
- **R153, retenue et élargie** : le registre par catégories (« Et oui les separer en categorie c'est top ») ; la première
  vague s'étend aux outils où la Présidence peut se connecter, pour les essayer de bout en bout : « on peut essayer avec des
  outils sur lesquel je peux me connecter, donc Github, Gitlab, OneDrive, Notion, Conflu, Jira, Slack, Teams ?, Linear, Docker
  Hub ?, Excalidraw ?, Jira, ... Figma ?, Bref voila pas mal de truc, Stripe aussi important, Zoho ca devrait etre facile je
  pense, Asana, ... ».
- **R154, retenue et amendée** : le clic n'est pas une fin en soi, la clarté l'est : « pas de pb si la personne doit gerer un
  truc de son cote sur les app microsoft ou autre, c'est normal, mais faut que le flux soit clair, coherent et accessible
  c'est tout, et que avec taskforce on puisse communiquer avec le reste donc c'est ok si c'est pas forcement un clique ».
- **R155 à R158, retenues.**
- **Docker Hub, gardé en exception** au premier critère de R152 (sans copier de jeton), une fois le guide de branchement lu :
  « on garde docker hub en exception, je copierai le jeton ». Il se branche sur l'app desktop par la passerelle locale de Docker et un jeton copié.
- **Le 12/11/2026, après la PR #523** :
  - **chaque outil du catalogue se montre**, essayé ou non, sans variable à poser : « t'imagines, ça veut dire que
    l'utilisateur devra faire ça? Attends, là c'est hardcore là ». L'essai d'attaque par outil de R158 passe à la fin de J2,
    avec les essais de la Présidence ;
  - **le catalogue reprend les connecteurs d'entreprise de l'annuaire de Claude** : « regarde un peu ce que propose par
    exemple Claude en extension non communautaire [...] Et puis on fait la même » ;
  - **le lot des fichiers commence** (Google Drive, OneDrive, SharePoint, Teams), et les connexions s'essaient à la fin :
    « On pourra tout tester à la fin ».

## Notes du secrétariat

- **Le registre** a été dressé pour la séance à partir de pages lues le 10/11/2026 : 46 outils. Ce qui n'a pas pu être vérifié
  y est listé.
- **Les faits du produit** viennent du code de `dev` ; deux constats (la classe déclarée par l'outil, deux gestes
  d'administration hors du moteur) sont dits sans leur détail, et se corrigent dans J2 (R157, R158).
- **Conflits d'intérêts** : Nadella dirige Microsoft, dont Microsoft 365, Teams, Azure DevOps et GitHub figurent au registre ;
  Saarinen dirige Linear, déjà branché dans TaskForce ; le secrétariat est tenu par un modèle d'Anthropic.
- **Siège historique** : Hamilton ne connaît MCP et ces outils que par le dossier.

## Suites

- Le PV au registre (§12) et au Journal ; le [Registre des outils](../../../v1/02-produit/Registre_des_outils.md) entre dans
  les notes du produit.
- Après la décision de la Présidence : à la roadmap, la connexion en un clic et la première vague (R153, R154), la lecture sans
  copie (R155, avec TF-J2-5), le stockage au choix (R156), les règles par couches (R157, avec TF-J2-4), la sécurité des
  connecteurs (R158), et les critères de R152 en tête de J2.
- Puis la construction, en lots.

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- Le levier le plus fort est la connexion par personne : sans elle, TaskForce lit avec les droits de l'administrateur, et ni
  la confiance ni l'audit ne tiennent.
- Le plus gros risque est l'injection par un contenu branché : R158 est la recommandation qui coûtera le plus, et celle qu'il
  faut le moins sacrifier.
- Google Drive avec les seuls fichiers choisis répond à « se brancher » sans six semaines de vérification ; lire tout un Drive
  demandera, plus tard, la vérification de Google, ou l'application de l'entreprise elle-même.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
