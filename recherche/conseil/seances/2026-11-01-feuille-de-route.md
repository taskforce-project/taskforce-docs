---
id: conseil-seance-2026-11-01-feuille-de-route
title: "Séance n°15 du 01/11/2026 : TaskForce complet, problème par problème, et la feuille de route jusqu'au bout"
doc_type: pv-seance
statut: active
date: "01/11/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, vision, feuille-de-route, souverainete, architecture]
related:
  - "../README.md"
  - "./2026-10-31-souverainete-operationnelle.md"
  - "./2026-10-27-vision.md"
  - "./2026-10-29-intelligence-possedee.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°15 du 01/11/2026 : TaskForce complet, problème par problème, et la feuille de route jusqu'au bout

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.
>
> **Décidé le 01/11/2026** : la Présidence a confirmé la lecture de ses décisions sur la séance n°14 et tranché R90 à
> R106 ; R90 à l'essai, R91 modifiée, R92, R102 et R103 précisées. La décision, et ce qu'elle change à la feuille de
> route, sont plus bas : ils priment sur les sections qui précèdent.

## Résumé

La Présidence a répondu à la séance n°14. Elle est d'accord avec le Conseil, et elle fixe le cap :
- un TaskForce complet pour la démo, de niveau entreprise, utilisable par n'importe quel métier ;
- devant sur chaque ligne de la carte ;
- la confiance comme indicateur premier ;
- un seul moteur, en Java ;
- la webapp considérée comme morte ;
- aucun modèle imposé.

Elle exige au moins 90 % de oui sur chaque solution et demande si le Conseil a compris ce qu'elle veut faire.

Le Conseil répond en cinq points.

1. **Oui, il a compris** (24 sur 24). TaskForce est l'infrastructure qui permet à n'importe quelle entreprise de faire
   travailler ses agents IA, sur les modèles qu'elle choisit, sous ses propres règles et sur ses propres données. Elle voit
   leur travail comme on voit Claude Code coder, prouve ce qu'ils ont fait et s'améliore à chaque échec. Les gens du métier
   construisent l'outil ; TaskForce fournit les briques, le moteur et la preuve.
2. **Dix-sept solutions** (R90 à R106), une par problème soulevé, chacune votée par au moins 22 membres sur 24 (le seuil de
   90 %). Quatre n'ont passé le seuil qu'au second tour, après amendements : R94, R102, R103, R105.
3. **Une feuille de route en dix jalons** (J0 à J9) :
   - une démo complète mais mince dès J2, vers le début de janvier 2027 ;
   - la démo complète, sur trois métiers de natures différentes, à J8 ;
   - chaque jalon se valide de la même façon : la boucle de démo rejouée, les tests, des yeux extérieurs, l'indice de
     confiance, une séance du Conseil, puis le go de la Présidence.
4. **Deux urgences.**
   - La faille de la recherche et « Apply » qui ignore les tests (J0).
   - Une dépendance cachée : l'app desktop se connecte par la webapp. Si la webapp meurt, aucune nouvelle installation ne
     démarre. J1 supprime cette dépendance.
5. **Une mise en garde, en tête du dossier** : « un n8n IA » existe déjà sous ce nom. n8n se présente comme une plateforme
   pour construire et déployer des agents IA et des flux de travail. La différence de TaskForce n'est donc pas « des agents
   dans des flux ». Elle tient en quatre points :
   - la règle du métier sur chaque action de chaque agent, hors du modèle ;
   - la preuve vérifiable sans TaskForce ;
   - le métier qui construit sans code ;
   - le local, sous AGPL.

Désaccords conservés :
- **Julie Zhuo**, contradictrice : un produit pour tous les métiers est le plus difficile à rendre bon. Elle vote non sur R94,
  R103 et R105.
- **Karri Saarinen** : non sur R103, abstention sur R94 et R99.
- **Elon Musk** : non sur R101, abstention sur R97.
- **Jeff Bezos** : abstention sur R98 et R101.
- **Steve Jobs** : abstention sur R95 et R98.
- **Satya Nadella** : abstention sur R91.
- **Gwynne Shotwell** : abstention sur R102.

Décision de la Présidence (01/11/2026) : tout retenu, sauf R90, à l'essai, et R91, modifiée : la webapp reste en ligne,
on n'y teste rien pour l'instant. Le détail est plus bas.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 01/11/2026), dans ses mots :
  - « Sur ce que je viens de dire je suis d'accord avec l'ensemble du conseil sur tout les points » ;
  - « faut qu'on soit devant absolument partout, on vise l excellence, le client focus » ;
  - « qu'ils proposent des solutions pour chaque pb rencontre et dans le sens de tout le monde, me faut au moins 90% de
    oui sur chaque solutions trouve a un pb, et je veux une solution forte, solide, complete » ;
  - « Avaient vous compris et a tu compris ce qu'on souahite faire avec Taskfroce finalement ? » ;
  - « etablissez une roadmap clair, precise, pour qu'on aille jusuq'au bout en iterant et en validant chaque etape de
    cette roadmap ».
- **Horizon** : jusqu'à la démo complète et la mise sur le marché ; la direction à trois ans reste R60.
- **Formation** : plénière, 24 membres. C'est un choix structurant (charte, §5).
  - Ordre de parole tiré au sort le 01/11/2026 à 10:31 UTC (`shuf`).
  - Contradictrice désignée : Julie Zhuo, jamais désignée jusqu'ici. Le consensus qui se formera est « un produit complet,
    pour tous les métiers » ; sa fiche porte la question qu'il esquive : quel problème, de qui, et comment saura-t-on
    qu'il est résolu ? Nadella l'était à la n°14.
- **Règle de vote** (Présidence, 01/11/2026) : au moins 90 % de oui par solution, soit 22 voix sur 24.
  - Une solution sous le seuil est retravaillée puis revotée ; le PV garde le premier tour quand il a échoué.
  - Le secrétariat note la tension avec la charte (§7.5, « l'unanimité est suspecte »). Pour la tenir, la contradictrice
    attaque chaque solution avant le vote, et un oui ne compte qu'avec l'amendement qui a répondu à l'objection de son
    auteur.
- **Fiches** : toutes à jour (du 21/10 au 28/10/2026, moins de 30 jours). Jobs et Hamilton, sièges historiques, ne se
  rafraîchissent que sur une nouvelle source historique.

## Ce que la Présidence a dit de la séance n°14

La Présidence dit son accord avec tout le Conseil, et donne en même temps des orientations qui modifient plusieurs
recommandations. La lecture ci-dessous est celle du secrétariat ; elle attend sa confirmation (charte, §2.4 : la raison
est la sienne, pas celle du secrétariat).

| R | Recommandation de la n°14 | Ce que la Présidence a dit | Lecture proposée |
| --- | --- | --- | --- |
| R81 | Le texte ne devient pas la feuille de route | « sur le tableau faut qu'on soit devant absolument partout » | Retenue, modifiée : le texte n'est pas la feuille de route, mais ses 21 lignes deviennent la barre à dépasser (la carte cible). « Aucune autre couche » tombe. |
| R82 | Dire vrai avant de dire plus | accord ; la webapp « morte » | Retenue. Tant que la webapp tourne, ses pages disent vrai ; puis elle ferme proprement (R91). |
| R83 | Mesurer avant de construire | « c'est la confiance » ; « me faut une demo pour aller chercher le client » | Retenue, modifiée : la mesure ne bloque plus la construction, elle juge chaque jalon (R104, R105). |
| R84 | Un geste, une personne | « c est une produit grade entreprise » ; « faire une tache quelconque » ; « un n8n IA » | Remplacée par R103 et R105 : la boucle complète, générale, montrée sur trois métiers. |
| R85 | La pharmacie n'est pas le premier terrain | « te fixe pas sur la pharma, nous on creer l'infra, pas les regles en elles mm » | Retenue, élargie : aucun secteur d'abord (R103). |
| R86 | Les règles appartiennent au client | « c'est a eux de construire l'outil » | Retenue, élargie (R94, R98). |
| R87 | Une preuve d'auditeur, « Apply » qui respecte les tests | accord | Retenue ; « Apply » corrigé avant la release de R78 (J0). |
| R88 | La fiabilité avant une couche de plus | la webapp « morte » | Retenue sans la webapp : ni secours pour Groq ni VPS pour l'instant ; la file durable et les événements sur disque vont en J2 et J5. |
| R89 | Publier le contrat, et l'essai de l'effet | accord | Retenue (R98, R100). |

Les quatre questions de la n°14 :
1. La conversation avec ChatGPT avait-elle reçu la pile de TaskForce ? **Sans réponse**, et sans enjeu pour la suite.
2. Les chiffres d'usage de la production : **sans objet**, la webapp n'étant plus testée.
3. Attendre la correction d'« Apply » avant la release de R78 : **oui**, par R87 retenue.
4. Les dix équipes extérieures de R84 : **remplacées** par les personnes extérieures de chaque jalon (R105).

### Ses orientations, et la solution qui répond à chacune

| Ce que la Présidence a dit | Solution | Jalon |
| --- | --- | --- |
| « pas de duoplication stp » entre Java et TypeScript | R90 | J1 |
| « devant absolument partout » sur le tableau | La carte cible, R105 | J0 à J9 |
| La webapp « morte », plus de test dessus | R91 | J0, J1 |
| « Claude et modele Ollama point barre », « Aucune dependance a des modeles » | R92 | J1, J2, J5 |
| Les données : savoir où elles vont, choisir son hébergement, « chiffrement obligatoire » | R93 | J2, J6 |
| La souveraineté du métier : « c'est a eux de construire l'outil » | R94, R98 | J2, J3 |
| Les agents : « plus robuste, plus scalable, plus visualisable » | R97, R95 | J2, J5 |
| La souveraineté opérationnelle | R93, R97, R100 | J5, J6 |
| Couche 1 : « une interface pour chaque partie, puis un chat pour qu'il nous assiste partout » | R95 | J2 à J8 |
| Couche 2 : « que l'agent hesite surtout pas a demander si des choses semble manquer » | R96 | J2, J4 |
| Couche 3 | R97 | J2, J5 |
| Couche 4A : vérifier la duplication | R90, R98 | J1, J3 |
| Couche 4B : « faut trouver une solution » | R92 | J1, J5 |
| Couche 5 : un outil bien fait, puis « n'importe quel outils » sans plus de code | R99 | J4, J5 |
| Couche 6 | R100 | J2, J6, J7 |
| Mécanismes A et B | R96, R98, R101 | J4, J7 |
| Mécanismes C et D | R101 | J7 |
| Le parcours d'arrivée « comme un jeu », « Hyper ludique et attirant » | R102 | J3, J8 |
| La grille de variables | R94 (le profil de l'espace) | J3 |
| « c est tout industrie ou entreprise », des trucs généraux d'abord | R103 | J2, J3, J8 |
| Les trois phases | R105 | J0 à J9 |
| La pile, et « on pourrait copier Temporal » | R97 | J2, J5 |
| « c'est la confiance » comme indicateur premier | R104 | J2, puis chaque jalon |
| « Pour l instant c est gratuit mais ca va pas le rester » | R106 | J8, J9 |
| « un truc qui fonctionne complet avec une boucle complete » | R105 | J2 (mince), J8 (complète) |

## Le Conseil a-t-il compris ?

### La reformulation soumise aux membres

`[HYPOTHÈSE]` TaskForce est l'infrastructure qui permet à n'importe quelle entreprise, dans n'importe quel métier, de faire
travailler des agents IA sous ses propres règles et sur ses propres données, chez elle. Ces agents sont les siens, sur
les modèles qu'elle choisit.
- Chaque action d'un agent passe par les règles de l'entreprise.
- On voit le travail se faire comme on voit Claude Code coder.
- Chaque résultat laisse une preuve qu'un tiers vérifie sans TaskForce.
- Chaque échec et chaque question améliorent le système, avec l'accord d'une personne.

Ce sont les gens du métier qui construisent leur outil. TaskForce fournit les briques, le moteur et la preuve, jamais les
règles du métier. La promesse reste R5' : « Vous décrivez le résultat ; TaskForce le fait faire par l'agent de votre
choix, avec vos outils et vos règles, et vous montre qu'il est bon. »

La Présidence parle d'« un n8n IA ». Le Conseil retient l'image, avec sa limite (dossier, point 8) : n8n met des agents
dans des flux ; TaskForce met les flux et les agents sous les règles du métier, avec la preuve.

### Ce que TaskForce n'est pas

- Un modèle d'IA.
- Un cabinet qui écrit les règles d'un métier.
- Un tableau de surveillance des agents (R57 tient).
- Le client d'un seul fournisseur de modèles.
- D'abord un service en ligne : d'abord la machine ou le serveur de l'entreprise.

### La boucle complète, sur un métier que personne ici ne connaît

`[HYPOTHÈSE]` Une entreprise de maintenance d'ascenseurs, quarante personnes, deux agences. Personne au Conseil ne connaît
ce métier, et c'est le but.

1. **Configurer.** La gérante joue le parcours d'arrivée (R102). Elle renomme « projet » en « contrat » et crée le type
   « intervention » (adresse, appareil, urgence, technicien). Elle écrit trois lignes rouges :
   - une intervention de sécurité ne se clôt qu'avec la signature d'un technicien habilité ;
   - un devis au-delà de 5 000 € demande sa signature, et celui qui l'a préparé ne peut pas la donner ;
   - les données des clients ne vont qu'aux modèles installés sur leurs machines.
2. **Brancher.** Elle dépose les notices des constructeurs et l'historique des interventions. Chaque source a un responsable
   et une date de validité (R96).
3. **Dessiner.** Le processus « panne signalée » : un agent qualifie la panne, un agent prépare l'ordre d'intervention et la
   liste des pièces, un vérificateur contrôle les consignes de sécurité, le chef d'équipe accorde, un agent écrit au client
   (R94, R97).
4. **Faire travailler.** Les agents tournent sur Ollama pour tout ce qui touche aux clients, et sur un modèle plus fort
   pour le reste ; chaque action passe par les règles (R92, R93).
5. **Voir.** Le chef d'équipe suit le travail comme on suit Claude Code : les étapes, les documents produits, ce qui a été
   vérifié (R95).
6. **Décider.** Il accorde la liste de pièces ; la gérante signe le devis (R98).
7. **Prouver.** Le dossier de l'intervention, signé, se vérifie sans TaskForce, par un client ou un contrôleur (R93).
8. **Améliorer.** TaskForce remarque deux choses (R101) :
   - l'agent a demandé trois fois la notice du même appareil : la source manque ;
   - le chef d'équipe accorde toujours les listes de pièces sous 500 €.

   Il propose de déposer la notice et d'autoriser ces listes sous 500 €. La gérante accepte ; les évaluations sont
   rejouées ; le dossier garde sa décision.

La même infrastructure sert une équipe logicielle (une issue jusqu'à la pull request) et une juriste (un brief jusqu'au
document cité et revu), sans une ligne de code propre à l'un ou à l'autre.

### Le vote

**Compris : 24 sur 24.** Trois réserves, qui ne portent pas sur la compréhension :
- Zhuo et Saarinen : compris ne veut pas dire d'accord sur « pour tous les métiers » (confrontation, débat 1) ;
- Bezos : « complet » devait être défini ; la boucle en huit temps le définit.

## La Présidence prend-elle le problème à l'envers ?

La Présidence le demande elle-même : « je prends peut etre le pb a l envers mais je suis pas sur finalement ».

- **Non, à une condition** : 20 membres.
  - Pour un produit dont la valeur est la confiance, la confiance vient d'une architecture qu'on peut montrer. Un acheteur
    ne croit pas une diapositive : il croit une boucle qui tourne devant lui. Construire d'abord est donc légitime.
  - La condition : des yeux extérieurs à chaque jalon dès J2, et la démo montrée avant d'être complète (R105).
- **En partie** : Zhuo, Duflo, Saarinen et Bezos.
  - La douleur que la Présidence connaît, elle l'a vécue elle-même : c'est une personne, pas un marché.
  - Le risque n'est pas de construire, c'est de construire sept mois sans que personne d'autre ne s'en serve.
  - La condition de la majorité répond à leur objection, si elle est tenue.

## Dossier

Constitué le 01/11/2026 par le secrétariat, à partir du code (`taskforce-fullstack`, `dev` au commit `6ab62b1d`, la
correction de la recherche n'y est pas encore), du PV n°14 et de pages lues ce jour.

1. `[ÉTABLI]` **La duplication que la Présidence a vue est réelle, et elle porte sur trois logiques.**
   - **La décision des règles.**
     - En Java : `RulesEngine`, `Glob` et `RulesDigest`, dans `backend/tf-api/.../core/harness/rules/`, environ 200
       lignes. Elles servent Cortex.
     - En TypeScript : `rules.ts` et `glob.ts`, dans `taskforce-runner/src/harness/`, environ 185 lignes. Elles servent les
       missions : chaque action de Claude Code est jugée dans le runner (`approvals.ts`), sans passer par le serveur.
   - **La chaîne de preuve.**
     - En Java, elle est écrite par `CanonicalJson` et `EvidenceChain`.
     - En TypeScript, elle est recalculée et vérifiée par `evidence.ts` et `verify.ts`.
   - **Le protocole d'IA.**
     - En Python, l'`ai-service` de la webapp, environ 550 lignes.
     - En TypeScript, la coque de l'app desktop le sert à nouveau (`desktop/src/ai.ts`, 377 lignes). Son commentaire dit
       son comportement « aligné sur `ai-service/app/services/provider.py` », c'est-à-dire recopié à la main.
   - **Pourquoi il en est ainsi.** C'était un choix de la spécification v2 (R16 : les contrats avant le code) :
     - le serveur Java publie les règles, le runner TypeScript les applique (`contracts/README.md`) ;
     - le runner tourne à côté de Claude Code, et jugeait chaque action sans aller-retour vers un serveur qui pouvait être
       loin (la webapp) ;
     - les 51 cas partagés (`contracts/rules/cases.json`) garantissent la même décision des deux côtés.
   - **Ce qui a changé.** Dans l'app desktop, le backend Java tourne sur la même machine que le runner
     (`desktop/README.md`). L'aller-retour ne coûte plus qu'un appel local.
2. `[ÉTABLI]` **L'app desktop dépend de la webapp pour démarrer.**
   - Elle se connecte par la page `/auth/desktop` de la webapp (`desktop/src/account.ts`), puis fonctionne hors ligne
     (`desktop/README.md`).
   - La webapp et le serveur de comptes tournent sur des machines de l'école, dont la date d'arrêt n'est pas au dossier.
   - Le VPS n'est pas acheté (décision du 30/10/2026 : « dès que possible »).
   - Le compte obligatoire a été décidé le 19/10/2026 ; l'ADR-021 promettait l'inverse (n°14, point 8).
   - `[DÉDUIT]` Webapp morte veut dire : aucune nouvelle installation ne démarre.
3. `[ÉTABLI]` **Les modèles aujourd'hui.**
   - App desktop : Ollama sur la machine, ou une API compatible OpenAI, au choix (Réglages > AI), relayés par la coque.
   - Webapp : Groq.
   - Missions : Claude Code ou Copilot seulement ; un modèle local ne peut pas mener une mission (R51 non construit).
   - Ni registre, ni routage, ni secours, ni budget.
4. `[ÉTABLI]` **Le chiffrement aujourd'hui.**
   - Au repos, seuls les secrets sont chiffrés : intégrations, connecteurs, webhooks, états OAuth
     (`EncryptedStringConverter`, quatre entités).
   - Le contenu est en clair dans PostgreSQL : issues, notes, dossiers.
   - Les sauvegardes de la production sont en clair, sur la même machine.
   - L'app desktop garde ses secrets dans le trousseau du système.
5. `[ÉTABLI]` **Ce qu'un métier peut configurer aujourd'hui : presque rien.**
   - Les objets sont fixes : projets, issues, cycles.
   - Les 35 règles ne se modifient pas ; la table par espace (V102) n'est jamais écrite.
   - Aucun processus ne se dessine : « AI Workflows » montre un plan d'analyse fixe.
   - Aucun vocabulaire ne se change, et l'interface n'existe qu'en anglais.
6. `[ÉTABLI]` **Le contexte aujourd'hui.**
   - Le moteur du Brain OS tourne, sans écran depuis le 28/10/2026.
   - Aucun document n'est lu ; les notes n'ont ni version ni responsable.
   - L'ingestion automatique n'est câblée que pour Plane ; un nouveau lecteur coûte trois à cinq jours de code.
   - La recherche ne respecte pas encore tous les droits des projets privés ; le détail reste hors du PV, les dépôts étant
     publics.
7. `[ÉTABLI]` **L'exécution aujourd'hui.**
   - Cortex fait cinq tours au plus.
   - Les missions passent par une file en base, sans moteur durable ni reprise.
   - Les événements du runner vivent en mémoire.
   - « Apply » reste actif quand les tests ont échoué.
   - Un accord sans réponse devient un refus silencieux au bout de dix minutes.
8. `[ÉTABLI]` **« Un n8n IA » existe déjà sous ce nom.**
   - Le dépôt de n8n le présente comme une « Fair-code platform to build and deploy AI agents and workflows »
     ([GitHub](https://github.com/n8n-io/n8n), lu le 01/11/2026). Il annonce aussi :
     - des modèles de plusieurs fournisseurs, interchangeables ;
     - des accords humains et des journaux d'audit ;
     - l'auto-hébergement et plus de 1 500 intégrations.
   - Sa licence (Sustainable Use License) n'est pas une licence libre au sens de l'OSI.
   - `[DÉDUIT]` La page ne revendique ni un moteur de règles du métier appliqué à chaque action d'agent, ni une preuve
     vérifiable hors de l'outil ; à vérifier dans sa documentation complète.
9. `[ÉTABLI]` **Deux faits pour les débats.**
   - Temporal : son moteur d'exécution durable est sous licence MIT, gratuit à auto-héberger, avec un SDK Java natif
     ([Temporal](https://temporal.io/llm-info)).
   - Amazon compte « gagner la confiance » parmi ses principes de direction publiés
     ([Amazon](https://www.aboutamazon.com/working-at-amazon/our-leadership-principles)).
10. `[ÉTABLI]` **Les moyens et le terrain.**
    - Un fondateur seul, un budget proche de zéro, pas de VPS.
    - Neuf utilisateurs réels au 08/09/2026, aucun revenu, aucun partenaire.
    - Aucune des expériences E7 à E15 menée.
    - Les contraintes C1 à C4 du labo ([`CLAUDE.md`](../../CLAUDE.md) §3).

## Tour de table `[HYPOTHÈSE]`

Dans l'ordre tiré au sort. Chaque membre dit s'il a compris, ce qui casserait, et ce qu'il apporte aux solutions. Les
interventions sont paraphrasées : aucune phrase n'est de la personne réelle.

### 1. Margrethe Vestager (Harmonie)

- **Compris** : oui. Une infrastructure où l'entreprise garde la main sur ses données, ses règles et ses fournisseurs.
- **Ce qui casse** : la souveraineté dite avant d'être vraie.
  - Aujourd'hui, seuls les secrets sont chiffrés, et les sauvegardes restent en clair sur la même machine.
  - La webapp « morte » tourne encore, avec une politique de confidentialité qui ne nomme pas Groq. Une webapp morte qu'on
    n'éteint pas reste un traitement de données.
- **Apporte** :
  - la carte des flux comme preuve, chaque sortie de donnée étant soumise à une règle ;
  - le chiffrement du contenu ;
  - un kit de conformité tiré de la configuration réelle (R93) ;
  - fermer la webapp proprement : prévenir, exporter, éteindre (R91).

### 2. Jeff Bezos (Impulsion)

- **Compris** : oui. Il prend acte : l'indicateur premier est la confiance. Ce n'est pas loin de lui, Amazon compte « gagner
  la confiance » parmi ses principes (dossier, point 9).
- **Ce qui casse** : une confiance déclarée. Elle se lit dans ce que font les gens : ils accordent plus d'autonomie à l'agent,
  ils reviennent, ils paient. Le temps gagné reste une composante, plus le titre.
- **Apporte** :
  - un indice de confiance fait de comportements mesurables (R104) ;
  - le communiqué et la foire aux questions de la démo, écrits avant de la construire (méthode d'Amazon, hors fiche) ;
  - un modèle de revenus instruit avant la tournée de démos (R106).
- **Condition** : une démo montrable tôt, pas seulement à la fin.

### 3. Karri Saarinen (Design, conflit d'intérêts : Linear)

- **Compris** : oui. Il maintient sa réserve de la n°14 : un outil pour tous les métiers devient vite une interface que
  personne n'aime.
- **Ce qui casse** : sept surfaces dessinées chacune à sa façon ; un générique qui se voit à l'écran.
- **Apporte** :
  - une seule grammaire d'interface pour toutes les surfaces ;
  - des réglages par défaut tranchés, portés par les packs ;
  - une vue du travail aussi lisible qu'une issue bien tenue (R95).
- **Vote** : non sur R103 ; abstention sur R94 et R99.

### 4. Steve Jobs (Impulsion, siège historique)

- **Compris** : oui. Complet ne veut pas dire tout. Complet veut dire une boucle entière, sans couture, de la première minute
  à la preuve.
- **Ce qui casse** : une démo qui montre des écrans au lieu de montrer un résultat.
- **Apporte** :
  - la démo est le produit : son déroulé s'écrit d'abord, et chaque jalon le rejoue en entier (R105) ;
  - le parcours-jeu est la première minute : il doit donner envie et construire du vrai (R102) ;
  - une seule promesse, R5'.
- **Vote** : abstention sur R95 (sept surfaces, ce sont sept produits ; il votera en les voyant) et sur R98 (R9').

### 5. Yuval Noah Harari (Harmonie)

- **Compris** : oui. Il entend « garder le controle de mes agents » et « voir les ameliorations, les reocmmendations ».
- **Ce qui casse** : la confiance déplacée vers le système sans personne qui en réponde. Un système qui recommande ses
  propres changements se juge lui-même.
- **Apporte** :
  - un responsable nommé pour chaque processus, chaque règle et chaque mission ;
  - aucune recommandation appliquée sans l'accord d'une personne, que le dossier nomme (R94, R101).

### 6. Nandan Nilekani (Harmonie)

- **Compris** : oui, et c'est une infrastructure au sens où il l'entend : des briques, des formats ouverts, des règles
  communes, et chacun construit dessus.
- **Ce qui casse** : supprimer le second moteur sans publier la spécification. Un format que personne d'autre ne peut
  implémenter n'est pas une infrastructure.
- **Apporte** :
  - un seul moteur, mais la spécification, les cas de conformité et le format des packs publiés, pour que d'autres puissent
    écrire leur propre vérificateur (R90, R98) ;
  - MCP dans les deux sens (R99).

### 7. Jennifer Doudna (Science)

- **Compris** : oui. Sa réserve de la n°14 tombe : aucun secteur n'est exclu, et ce sont les gens du métier qui écrivent
  leurs règles.
- **Ce qui casse** : une autonomie qui s'accorde sans preuve, et aucun canal pour signaler un incident.
- **Apporte** :
  - des paliers d'autonomie qui s'ouvrent sur preuve et se referment sur incident, jamais sur l'irréversible (R1, R97) ;
  - un canal de signalement ouvert à tous (R100).

### 8. Daniela Rus (Science)

- **Compris** : oui. Le local est l'architecture, pas une option.
- **Ce qui casse** : l'app desktop qui ne démarre pas sans la webapp ; des missions qui ne tournent pas sur un modèle local.
- **Apporte** :
  - un desktop qui s'installe et vit sans réseau ni compte (R91) ;
  - des missions sur un modèle local (R92) ;
  - la latence et la consommation mesurées sur un poste ordinaire ;
  - un vrai bac à sable (R97).

### 9. Fei-Fei Li (Science)

- **Compris** : oui. Une IA au service des gens du métier, pas à leur place.
- **Ce qui casse** : des évaluations faites par le vendeur, sur ses propres cas.
- **Apporte** :
  - une banque d'évaluations par pack et par agent (R100) ;
  - un registre des incidents nourri par les dossiers ;
  - une évaluation par un tiers à J8 (R101, R105).

### 10. Arati Prabhakar (Pont)

- **Compris** : oui. Elle le lit comme un programme à jalons.
- **Ce qui casse** : un « devant » sans protocole d'essai.
- **Apporte** :
  - pour chaque ligne de la carte, un essai et un seuil ;
  - pour chaque jalon, un « go / no-go » écrit avant (R105) ;
  - l'essai contradictoire d'après le Top 10 agentique de l'OWASP, en continu, son taux d'arrêt publié (R100).

### 11. Elon Musk (Impulsion)

- **Compris** : oui. La suppression du doublon est la bonne première étape : supprimer avant d'ajouter.
- **Ce qui casse** : six couches construites comme six produits par une seule personne. La seule voie est de remplacer des
  fonctions par des briques, et de supprimer ce qu'elles remplacent.
- **Apporte** :
  - la liste de suppression de J1 : le moteur et la chaîne en TypeScript, l'ai-service Python, le relais d'IA de la coque,
    les préréglages de connecteurs jamais essayés retirés du catalogue visible, le plan figé d'« AI Workflows » (R90) ;
  - une version de la boucle de démo construite chaque jour (R105).
- **Vote** : non sur R101 (l'affinage avant le premier client, c'est du stock) ; abstention sur R97.

### 12. Yann LeCun (Science)

- **Compris** : oui. Pas de modèle maison, des modèles ouverts, une couche de contrôle : le bon côté.
- **Ce qui casse** : un planificateur posé sur un LLM, qu'on croirait fiable.
- **Apporte** :
  - l'aperçu des effets avant d'agir : le diff, les commandes, l'exécution à blanc ;
  - la vérification par contraintes (les règles, les tests) plutôt que par un second LLM seul ;
  - un vrai bac à sable (R97).

### 13. Gwynne Shotwell (Impulsion)

- **Compris** : oui. « Grade entreprise » veut dire qu'on l'installe, le met à jour, le sauvegarde, le restaure et le
  dépanne sans le fondateur.
- **Ce qui casse** : une démo qui marche sur le poste de la Présidence et nulle part ailleurs.
- **Apporte** : une liste de lancement à chaque jalon (installation propre, mise à jour, sauvegarde et restauration, dossier
  d'exploitation), et la démo traitée comme un lancement (R105).
- **Vote** : abstention sur R102 (un acheteur industriel demande d'abord un plan d'installation, pas un jeu).

### 14. Mariana Mazzucato (Pont)

- **Compris** : oui. Elle pose la question de la valeur : qui la garde ?
- **Ce qui casse** : une plateforme qui remplace un seigneur par un autre.
- **Apporte** :
  - les packs, les données, les évaluations et les modèles affinés appartiennent à l'entreprise et partent avec elle
    (R93, R94) ;
  - le cœur reste sous AGPL, quel que soit le modèle de revenus (R106).

### 15. Esther Duflo (Science)

- **Compris** : oui. Elle accepte que la mesure ne bloque plus la construction, à une condition.
- **Ce qui casse** : des jalons jugés par celui qui les construit, avec des critères écrits après coup.
- **Apporte** :
  - des critères de sortie écrits avant chaque jalon ;
  - une mesure de départ à J2 ;
  - des personnes extérieures à chaque jalon ;
  - les échecs écrits au Journal (R104, R105).

### 16. Audrey Azoulay (Harmonie)

- **Compris** : oui. Un outil pour toute organisation, y compris petite.
- **Ce qui casse** : une interface en anglais seulement ; des règles lisibles seulement en JSON.
- **Apporte** : l'interface en français et en anglais ; la charte des règles d'un espace, lisible par un auditeur et tirée des
  règles réelles (R95, R98).

### 17. Kenza Ait Si Abbou (Pont)

- **Compris** : oui. Sa réserve de la n°14 tombe aussi.
- **Ce qui casse** : les mots d'ingénieur. Une technicienne de maintenance ne délègue pas une « issue ».
- **Apporte** :
  - le vocabulaire de l'espace et des types d'objets propres au métier (R94) ;
  - des sources avec un responsable et une date de validité (R96) ;
  - le parcours-jeu dans la langue du métier (R102).

### 18. Atul Gawande (Science)

- **Compris** : oui.
- **Ce qui casse** : une vérification qui ne dit pas ce qu'elle vérifie.
- **Apporte** :
  - des listes de contrôle aux points de pause : le vérificateur coche, la personne voit ce qui a été vérifié (R97) ;
  - le temps et les erreurs mesurés avant et après sur chaque tâche de démo, comme composantes de la confiance (R104).

### 19. Don Norman (Design)

- **Compris** : oui. Une interface par partie et un assistant partout : il le préfère à la seule barre.
- **Ce qui casse** :
  - l'assistant qui remplace les écrans : on ne découvre plus ce qui est possible ;
  - l'accord donné sans lire ;
  - le refus par délai qui ne se dit pas.
- **Apporte** :
  - chaque surface montre ses possibilités ;
  - l'assistant agit par les mêmes gestes, sous les mêmes règles ;
  - tout passage outre est explicite et motivé ;
  - le jeu enseigne comment le système fonctionne (R95, R102).

### 20. Julie Zhuo (Design, contradictrice, conflit d'intérêts : Meta, par Sundial)

Contradictrice, elle attaque le consensus qui s'est formé : « complet, pour tous les métiers, devant partout ».

- **Compris** : oui, et c'est le problème : la phrase décrit une solution, pas une personne. Quel problème, de qui, et
  comment saura-t-on qu'il est résolu ?
- **Ce qui casse** :
  - un produit pour tous les métiers est le plus difficile à rendre bon ;
  - sept mois de construction avant la première personne extérieure ;
  - « devant partout » comme slogan.
- **Ce qu'elle obtient** :
  - trois personnes-types pour la démo, chacune avec son test de première minute et de première semaine ;
  - des yeux extérieurs dès J2 ;
  - « devant » défini ligne par ligne, avec sa preuve (R103, R105).
- **Vote** : non sur R94, R103 et R105, maintenu.

### 21. Yoshua Bengio (Science)

- **Compris** : oui. Un plan de contrôle, pas un agent de plus.
- **Ce qui casse** : un vérificateur qui partage les objectifs de l'agent ; un modèle affiné qui perd ses garde-fous.
- **Apporte** :
  - un vérificateur d'un autre fournisseur, non agentique, qui estime le risque avant l'accord (R97) ;
  - une famille d'évaluations de sûreté obligatoire avant d'enregistrer un modèle affiné (R101).

### 22. Satya Nadella (Pont)

- **Compris** : oui. Il maintient son désaccord de la n°14 : la porte et la preuve sont devenues un standard du marché, et
  n8n dit déjà « agents » et « confiance » (dossier, point 8).
- **Ce qui casse** : se battre contre les plateformes au lieu de s'y brancher.
- **Apporte** :
  - un point de décision ouvert : tout moteur d'agents extérieur (n8n compris) peut demander la décision aux règles de
    l'entreprise et écrire au dossier, par MCP ou par HTTP (R99) ;
  - OpenTelemetry exportable vers les outils déjà en place (R100).

  La différence est la combinaison du local, de la preuve et des packs du métier.
- **Vote** : abstention sur R91 (pour une entreprise, le serveur hébergé n'est pas facultatif ; « plus tard » demande une
  date).

### 23. Tristan Harris (Harmonie)

- **Compris** : oui.
- **Ce qui casse** :
  - un jeu d'accueil qui emprunte les ressorts de l'attention : séries à tenir, récompenses, peur de manquer ;
  - un indicateur qui récompense l'automatisation plutôt que la confiance.
- **Apporte** :
  - un jeu sans piège : la progression et le retour immédiat, aucune récompense d'engagement (R102) ;
  - un indice de confiance qui mesure aussi l'accord donné sans lire (R104).

### 24. Margaret Hamilton (Science, siège historique)

- **Compris** : oui.
- **Ce qui casse** : un moteur de processus qui perd une mission quand la machine s'endort.
- **Apporte** :
  - l'exécution durable : journal, rejeu, reprise ;
  - les priorités et ce que le système lâche d'abord quand il sature, écrits avant ;
  - les événements du runner sur disque ;
  - moins de pièces mobiles, donc un seul moteur (R90, R97).

## Confrontation `[HYPOTHÈSE]`

### 1. Pour tous les métiers, ou bon pour quelqu'un ?

- **Zhuo, contradictrice, et Saarinen** : les produits qui gagnent sont faits pour quelqu'un. « Pour tous les métiers » est
  la phrase des produits que personne n'aime.
- **Nilekani, Nadella et Musk** : une infrastructure gagne par ses briques. La généralité est dans le moteur, la
  particularité dans les packs. Un outil fait pour un métier ne s'étend pas ; une brique bien faite sert tous les métiers.
- **Jobs** : la démo doit rester une seule expérience. Complet, c'est la boucle, pas le catalogue.
- **Où l'on arrive** : un moteur et des briques génériques ; trois personnes-types précises pour la démo ; les métiers
  apportent leurs packs (R103). Zhuo et Saarinen maintiennent leur non.

### 2. « Devant partout » : un mot, ou une barre ?

- **Zhuo, Duflo et Bezos** : un mot sans mesure. Devant qui, sur quoi, vu par qui ?
- **Prabhakar, Vestager et Shotwell** : une barre par ligne, avec son essai, et vue par quelqu'un d'extérieur.
- **Nadella** : devant le texte, partout, c'est faisable. Devant le marché, partout, c'est faux : les plateformes ont la
  distribution et des centaines d'intégrations.
- **Où l'on arrive** :
  - « devant » est défini ligne par ligne face au texte, comme dans le tableau de la Présidence, avec sa preuve (la carte
    cible) ;
  - face au marché, la carte dit honnêtement où TaskForce vise à mener et où elle vise la parité.

  Tous les membres acceptent cette définition, Zhuo comprise ; elle entre dans R105.

### 3. « Un n8n IA » : n8n l'est déjà ?

- **Nadella et Saarinen** : n8n se présente déjà comme une plateforme d'agents et de flux, avec des accords humains, des
  journaux et l'auto-hébergement (dossier, point 8).
- **Nilekani, Bengio et Vestager** : ce que n8n ne revendique pas est justement la pièce de TaskForce : la règle du métier
  sur chaque action, hors du modèle, fermée en cas de panne, et la preuve vérifiable par un tiers.
- **Mazzucato** : la licence aussi compte. L'AGPL laisse au client ce que la licence de n8n réserve à son éditeur.
- **Où l'on arrive** : « n8n IA » est une image de travail, pas une promesse. TaskForce se branche à n8n plutôt que de le
  combattre : n8n peut demander la décision et écrire au dossier (R99). La phrase de la promesse se teste (E14, à J8).

### 4. Le contexte d'abord, ou la boucle mince d'abord ?

- **Nadella, Ait Si Abbou et Li** : la couche 2 est la grande guerre, comme le dit la Présidence. Sans contexte juste, les
  agents inventent ; une démo sans documents ne convainc personne.
- **Jobs, Musk, Shotwell et Hamilton** : une boucle complète et mince d'abord, sur une fondation durable, puis on
  l'épaissit. Une couche finie sans boucle autour ne se montre pas.
- **Où l'on arrive** : J2 construit la boucle mince avec un contexte mince mais réel (des documents versionnés et cités) ;
  J4 livre le contexte complet.

### 5. La webapp : geler, fermer, ou la garder pour les comptes ?

- **Musk** : la supprimer.
- **Bezos et Nadella** : les entreprises louent ; la version hébergée reviendra.
- **Rus, LeCun et Vestager** : l'app desktop doit tenir seule, et une webapp morte qui tourne traite encore des données.
- **Où l'on arrive** (R91) :
  - J1 rend l'app desktop autonome ;
  - puis la webapp ferme proprement, sur décision de la Présidence ;
  - le serveur revient plus tard, avec le même moteur.

  Nadella s'abstient.

### 6. Un jeu, dans un produit d'entreprise ?

- **Harris, Shotwell, Gawande et Vestager** : un jeu manipule, ou fait peu sérieux devant un acheteur.
- **Jobs, Ait Si Abbou, Norman et Zhuo** : la première minute décide de tout, et un jeu bien fait enseigne.
- **Où l'on arrive** (R102) : un jeu qui construit du vrai, sans aucun piège d'attention, avec un mode sobre. Shotwell
  s'abstient.

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R90 (R89 est la dernière). Chacune dit :
- le problème et la solution ;
- un exemple, ce que la solution change, et ce qui reste à faire ;
- le vote et, s'il y en a, les amendements ;
- le jalon, la preuve en dix jours et le signal d'arrêt.

### R90. Un seul moteur, en Java

- **Le problème** : trois logiques existent en double (dossier, point 1) : la décision des règles, la chaîne de preuve, le
  protocole d'IA.
- **La solution** :
  1. **La décision n'existe qu'en Java.**
     - Le runner devient un adaptateur. Il traduit l'action de l'agent en faits, et ce code-là est propre à chaque agent,
       ce n'est pas un doublon.
     - Il demande la décision au moteur Java de la machine (`127.0.0.1`, avec le secret de lancement).
     - Sans réponse, l'action est refusée : le système reste fermé en cas de panne.
  2. **La chaîne de preuve n'est écrite qu'en Java**, au moment même de la décision.
     - La vérification d'un export se fait par un petit outil Java livré avec l'app.
     - La spécification et les cas restent publiés, pour qui veut écrire son propre vérificateur (Nilekani).
  3. **La passerelle de modèles passe en Java**, dans le backend (R92).
     - L'ai-service Python et le relais d'IA de la coque disparaissent.
     - La clé d'API reste dans le trousseau du système. Le backend la reçoit au lancement, en mémoire, jamais en base.
  4. **Une règle d'architecture (ADR) et un contrôle de la CI** : la décision, la chaîne et la passerelle n'existent qu'en
     Java. Le contrôle échoue si un second moteur réapparaît.
  5. **Ce qui reste en TypeScript est de l'interface** : la coque Electron, le frontend, l'adaptateur du runner.
- **Exemple** : Claude Code veut lancer `git push`.
  - Aujourd'hui, le runner décide seul, en TypeScript.
  - Demain, il envoie les faits (l'action `git.push`, la branche, la visibilité du dépôt) au backend Java de la machine.
    Celui-ci décide, écrit l'événement dans la chaîne et répond en quelques millisecondes.
- **Ce que ça change** :
  - une règle ne se modifie qu'à un endroit ;
  - l'éditeur de règles (R94, R98) n'a qu'un moteur à servir ;
  - la preuve est écrite là où la décision est prise.
- **Ce qui reste** : quand la version hébergée reviendra, chaque action devra joindre un serveur distant ; la latence se
  mesurera alors (Hamilton).
- **Amendements** :
  - Nilekani : la spécification et les cas publiés ;
  - Hamilton : le refus sans réponse, et la latence mesurée ;
  - Musk : la liste de suppression.
- **Vote** : 24 oui. La contradictrice l'a attaquée : deux à trois semaines qui ne montrent rien à un client. Le vote est
  resté unanime parce que tout le reste se construit dessus.
- **Jalon** : J1.
- **Preuve en dix jours** : une mission déléguée de bout en bout, chaque action décidée par le moteur Java, et les 51 cas
  verts en Java.
- **Signal d'arrêt** : une décision qui diffère entre Cortex et une mission sur les mêmes faits, ou une latence qui gêne
  l'agent.

### R91. L'app desktop tient seule ; la webapp se gèle, puis ferme proprement

- **Le problème** :
  - La Présidence considère la webapp comme morte : elle coûte un hébergement.
  - Mais l'app desktop se connecte par elle ; sans webapp, aucune nouvelle installation ne démarre (dossier, point 2).
  - La webapp tourne encore, avec des utilisateurs et des pages qui ne disent pas vrai (n°14, point 8).
- **La solution** :
  1. **Tout de suite (J0)** : la webapp est gelée.
     - Plus de développement ni de test qui lui soit propre.
     - Ses pages disent vrai tant qu'elle tourne : Groq nommé, hébergement réel.
  2. **J1** : l'app desktop crée une identité locale à l'installation.
     - Le compte en ligne devient facultatif ; il servira plus tard à la synchronisation et à la version hébergée.
     - Les installations déjà connectées continuent sans rien perdre.
  3. **Fin de J1, sur décision de la Présidence** : la webapp ferme proprement.
     - Les comptes sont prévenus.
     - Chacun exporte son espace (le fichier d'espace existe déjà) et l'importe dans l'app desktop.
     - Puis on éteint.
  4. **Le banc d'essai de référence devient la machine de la Présidence** : Claude Code et Ollama (R92).
  5. **La version serveur revient quand le budget le permet** : le même moteur, en profil serveur (R93).
- **Exemple** : une personne télécharge l'app un dimanche, sans réseau. Elle crée son espace, branche Ollama, délègue une
  tâche. Aucun serveur de TaskForce n'est touché.
- **Ce que ça change** :
  - la souveraineté devient vraie dès le premier lancement ;
  - plus aucun coût d'hébergement ;
  - plus aucune donnée traitée sur les machines de l'école.
- **Ce qui reste** : compter les téléchargements (GitHub le fait déjà) et écrire aux utilisateurs (une inscription
  facultative). Cette solution revient sur la décision du 19/10/2026 : la Présidence tranche.
- **Amendements** :
  - Bezos : le serveur reviendra pour qui loue ;
  - Vestager : fermer veut dire prévenir, exporter, éteindre ;
  - Rus : le fonctionnement sans réseau se mesure.
- **Vote** : 23 oui, 1 abstention (Nadella : pour une entreprise, le serveur hébergé n'est pas facultatif, et « plus tard »
  demande une date).
- **Jalon** : J0 pour le gel, J1 pour l'autonomie, fin de J1 pour la fermeture si la Présidence la décide.
- **Preuve en dix jours** : une installation neuve, réseau coupé, utilisable de bout en bout.
- **Signal d'arrêt** : une fonction de l'app qui exige un serveur de TaskForce.

### R92. Aucun modèle imposé

- **Le problème** : un seul fournisseur par instance, sans registre, routage, secours ni budget ; les missions ne passent que
  par Claude Code ou Copilot (dossier, point 3).
- **La solution** :
  1. **Une passerelle de modèles en Java** (R90) : Ollama, toute API compatible OpenAI (vLLM, LM Studio, Mistral, Groq et
     d'autres), l'API d'Anthropic. Elle sert la conversation, les outils et les vecteurs.
  2. **Un registre des modèles par espace.** Pour chaque modèle, il dit :
     - où il tourne : machine, pays, fournisseur ;
     - ce qu'il sait faire et ce qu'il coûte ;
     - quelles classes de données il a le droit de voir.
  3. **Un routage par tâche et par classe de donnée**, avec une chaîne de secours et un budget. Une donnée confidentielle ne
     va qu'à un modèle local, par une règle du moteur (R93).
  4. **Des moteurs d'agents interchangeables** :
     - Claude Code, comme aujourd'hui ;
     - la boucle d'agent de TaskForce, qui fait travailler n'importe quel modèle de la passerelle avec les outils MCP (R51
       devient possible) ;
     - d'autres agents ensuite, par le contrat d'adaptateur (`contracts/agent/adapter.md`).
  5. **Un changement de modèle demande une raison, un accord et les évaluations rejouées** (R61, Hamilton).
  6. **Copilot reste branché**, mais l'interface dit qu'il ne passe ni par les règles ni par le dossier, tant que ce n'est
     pas le cas (Harari, n°14).
- **Exemple** : la Présidence délègue la même tâche deux fois : à Claude Code, puis à un modèle Ollama par la boucle de
  TaskForce. Les deux missions passent par les mêmes règles ; le registre montre où chaque appel est allé.
- **Ce que ça change** : l'entreprise choisit ses modèles et n'est fixée à aucun fournisseur.
- **Ce qui reste** : sur un petit modèle local, la boucle d'agent de TaskForce fera moins bien que Claude Code. Cela se
  mesure (E11), et l'interface le dit.
- **Vote** : 24 oui.
- **Jalon** :
  - J1 : la passerelle Java ;
  - J2 : le registre v1 et la boucle d'agent ;
  - J5 : le routage, le secours, le budget, le changement sous évaluation.
- **Preuve en dix jours** : la même tâche menée par Claude Code puis par un modèle Ollama, sous les mêmes règles.
- **Signal d'arrêt** : un appel de modèle absent du registre.

### R93. On sait où va chaque donnée

- **Le problème** (dossier, point 4) :
  - seuls les secrets sont chiffrés au repos, et les sauvegardes sont en clair ;
  - aucune carte des sorties de données ;
  - pas d'export complet (R64) ;
  - un dossier ni signé ni conservé.
- **La solution** :
  1. **La carte des flux.** Chaque sortie (modèle, connecteur, webhook, mise à jour) est journalisée avec sa destination,
     son but, sa classe de donnée, son volume et son pays. Elle se voit en direct.
  2. **Des règles de sortie dans le moteur** : pour chaque classe de donnée, les destinations permises. Rien ne sort sans
     passer par elles.
  3. **Le chiffrement obligatoire** :
     - le contenu au repos, par enveloppe, avec une clé par espace (trousseau du système, ou KMS côté serveur) ;
     - les sauvegardes, chiffrées et gardées hors de la machine ;
     - TLS partout côté serveur.
  4. **La preuve d'auditeur** (R87) : le dossier est signé par la clé de l'espace, horodaté, conservé pour une durée choisie,
     et survit à la suppression de son objet.
  5. **L'export complet** (R64) : l'espace, ses règles, ses packs, ses dossiers, ses évaluations, ses connaissances et son
     registre des modèles, dans un seul fichier, importable dans un nouvel espace.
  6. **Les profils d'hébergement** : l'app desktop ; un serveur auto-hébergé (Docker Compose, puis Kubernetes) ; plus tard,
     la version hébergée.
  7. **Un kit de conformité tiré de la configuration réelle**. C'est de la documentation, pas une certification :
     - le registre des traitements ;
     - la liste des sous-traitants, tirée de la carte des flux ;
     - la journalisation demandée par l'AI Act ;
     - la correspondance avec l'ISO 42001.
  8. **Des données d'entraînement possédées** : les résultats acceptés deviennent des jeux de données, avec leur provenance et
     leur classe (R101).
- **Exemple** : une entreprise classe ses contrats « confidentiels ». Un agent veut envoyer un extrait à un modèle hébergé :
  la règle de sortie refuse et propose le modèle local. La carte des flux montre la tentative.
- **Ce que ça change** : « souverain » devient un fait qu'on montre, plus un mot.
- **Ce qui reste** : le chiffrement applicatif coûte en performance et complique la recherche ; c'est à mesurer.
- **Amendements** :
  - Vestager : le kit tiré du système ;
  - Mazzucato : l'export complet comme preuve ;
  - Nadella : OpenTelemetry exportable.
- **Vote** : 24 oui.
- **Jalon** : J2 pour le dossier signé v1, J6 pour le reste.
- **Preuve en dix jours** : une capture réseau d'une démo, comparée à la carte des flux : aucune sortie n'y manque.
- **Signal d'arrêt** : une sortie de donnée que la carte ne montre pas.

### R94. Le métier construit son outil

- **Le problème** : un métier ne peut presque rien configurer aujourd'hui (dossier, point 5).
- **La solution** : un métamodèle, c'est-à-dire huit briques que le métier assemble sans code.
  1. **Le profil de l'espace** : la grille de variables du texte (confidentialité, criticité, stabilité des connaissances,
     autonomie, coût, hébergement, conservation, et les autres).
     - Il règle les valeurs par défaut : sévérité des règles, routage des modèles, durée de conservation.
     - Il se voit dans chaque décision.
  2. **Le vocabulaire** : le métier renomme les objets (« issue » devient « intervention », « dossier », « écart »), dans
     l'interface et dans les consignes des agents.
  3. **Les types d'objets** : les noms du métier, avec leurs champs et leurs états.
  4. **Les règles** : un éditeur en mots, sans JSON à l'écran, avec un responsable, une raison et une date de revue (R86),
     et des cas d'essai (R98).
  5. **Les processus** : un canevas modifiable (R97).
  6. **Les agents** : un rôle, des consignes, des outils permis, un modèle, un palier d'autonomie.
  7. **Les évaluations** : ce qu'est un bon résultat dans ce métier (R101).
  8. **Les packs** : le tout s'exporte en un fichier versionné, au format ouvert, et s'importe dans un nouvel espace. Un
     pack contient la configuration, jamais les données.

  Chaque brique a un responsable nommé (Harari). Personne ne part d'une page blanche : le parcours-jeu (R102) et les packs
  de démonstration (R103) donnent un point de départ.
- **Exemple** : l'entreprise d'ascenseurs crée le type « intervention », renomme « projet » en « contrat », écrit sa règle de
  signature, puis exporte le tout pour sa seconde agence.
- **Ce que ça change** : TaskForce n'écrit plus les règles d'un métier ; le métier les écrit.
- **Ce qui reste** : un outil qui sait tout configurer est le plus difficile à rendre simple (Zhuo, Jobs).
- **Premier tour** : 19 oui, 5 non (Jobs, Saarinen, Zhuo, Musk, Norman). Un constructeur d'outils pour tous les métiers
  devient une usine à écrans.
- **Amendements** :
  - jamais de page blanche : des packs, le jeu, et l'assistant qui construit avec la personne ;
  - des gestes, pas des formulaires techniques (Norman) ;
  - huit briques, pas une de plus, chacune remplaçant un cas particulier qui existe déjà (Musk) ;
  - des réglages par défaut tranchés (Saarinen).
- **Vote final** : 22 oui, 1 non (Zhuo), 1 abstention (Saarinen, qui votera sur l'écran).
- **Jalon** : J2 pour les règles, les processus et les agents en v1 ; J3 pour le profil, le vocabulaire, les types, les
  packs et les règles complètes.
- **Preuve en dix jours** : une personne d'un métier que l'équipe ne connaît pas configure seule un type, trois règles et un
  processus de trois étapes.
- **Signal d'arrêt** : un métier qui a besoin de code pour exprimer une règle ou un processus courant.

### R95. Une surface par partie, l'assistant partout

- **Le problème** :
  - R76 (n°13) a fait d'une barre unique l'entrée de chaque écran ;
  - les règles, les processus, les modèles et les connaissances n'ont pas de surface ;
  - R57 refuse un écran de surveillance.

  La Présidence demande « une interface pour chaque partie, puis un chat pour qu'il nous assiste partout ».
- **La solution** :
  1. **Sept surfaces, une par brique, avec la même grammaire** : Travail, Processus, Règles, Connaissances, Agents et
     modèles, Preuves, Améliorations. Plus les Réglages de l'espace.
  2. **L'assistant (Cortex) sur chaque surface**, par la barre de R76, où l'on écrit ou parle.
     - Il agit par les mêmes gestes que la personne, sous les mêmes règles.
     - Ses actions entrent au dossier.
     - Il ne remplace aucun écran : R76 précisée, comme Saarinen le demandait à la n°13.
  3. **La vue du travail**, comme quand on regarde Claude Code coder. On y voit en direct :
     - les étapes et les appels d'outils ;
     - les fichiers et documents produits, et leurs diffs ;
     - les accords ;
     - la preuve qui se construit.
  4. **R57 tient** : aucun écran ne surveille les agents. Le travail se voit sur son objet, les améliorations dans leur boîte.
  5. **Les objectifs** (R56) : chaque processus porte un but, une date et des critères de réussite.
  6. **Le français et l'anglais** (Azoulay).
- **Exemple** : la Présidence ouvre Règles et voit la règle qui a demandé un accord dix fois cette semaine. Elle dit à la
  barre « passe-la en autorisée sous 500 € ». L'assistant prépare la modification ; elle l'accepte ; le dossier la garde.
- **Ce que ça change** : chaque partie a son lieu, et l'assistant aide partout sans cacher ce qui est possible.
- **Ce qui reste** : tenir sept surfaces au niveau d'exigence que demande Saarinen.
- **Vote** : 23 oui, 1 abstention (Jobs).
- **Jalon** : J2 pour Travail, Processus et Règles en v1 ; J3 à J7 pour les autres ; J8 pour l'ensemble poli.
- **Preuve en dix jours** : la maquette des sept surfaces avec la même grammaire, et une action de l'assistant visible
  ensuite au dossier.
- **Signal d'arrêt** : une action de l'assistant qu'aucune surface ne montre.

### R96. Un contexte juste, et l'agent qui demande

- **Le problème** : aucun document n'est lu, les notes n'ont ni version ni responsable, les droits de la recherche sont à
  corriger, l'ingestion n'est câblée que pour Plane (dossier, point 6).
- **La solution** :
  1. **Lire les documents** : PDF, Word, Excel, PowerPoint, HTML, Markdown, e-mails, avec leur structure (titres, tableaux).
     La lecture se fait en Java (Apache Tika, PDFBox, POI), sur la machine.
  2. **Une fiche pour chaque source** : sa version, son responsable, sa date de validité, sa classe de donnée et sa
     provenance. Deux versions d'une source se comparent.
  3. **Les droits appliqués dans la requête**, avant le classement, et prouvés par un essai contradictoire.
  4. **Une recherche hybride** : texte intégral, vecteurs, voisins dans le graphe, puis un reclassement local. Les citations
     renvoient au passage près, avec sa version.
  5. **L'agent qui demande.**
     - Chaque agent a un outil « demander ».
     - Un détecteur de manque repère trois cas : peu de sources, des sources contradictoires, une source périmée.
     - La question va au responsable de la source ; sa réponse devient une connaissance versionnée, à son nom.
     - La mission attend ou continue, selon la règle.
  6. **La surface Connaissances** : les sources, leur fraîcheur, leurs responsables, les manques, les questions ouvertes,
     les contradictions. Pas un arbre de pages.
  7. **Des évaluations de recherche par pack** : des questions de référence, et la précision mesurée avant et après.
- **Exemple** : l'agent prépare une intervention sur un appareil dont la notice manque. Au lieu d'inventer, il demande au
  responsable des notices de la déposer. La notice sert ensuite à toutes les interventions.
- **Ce que ça change** : l'agent cite au lieu d'inventer, et chaque question enrichit la base.
- **Ce qui reste** : les documents scannés et les tableaux complexes, à mesurer sur les packs.
- **Amendements** :
  - Ait Si Abbou : un responsable et une date de validité pour chaque source ;
  - Vestager : les droits prouvés ;
  - Li : les évaluations.
- **Vote** : 24 oui.
- **Jalon** :
  - J0 : les droits ;
  - J2 : les documents v1, avec versions et citations ;
  - J4 : le reste.
- **Preuve en dix jours** : sur un manque semé exprès, l'agent demande au lieu d'inventer, et la réponse sert à la mission
  suivante.
- **Signal d'arrêt** : un agent qui cite une source que la personne n'avait pas le droit de lire.

### R97. Des agents robustes, vérifiés, visibles

- **Le problème** : pas de moteur durable ni de reprise, pas de vérificateur indépendant (R4, R15), des événements du runner
  en mémoire, un bac à sable qui n'isole rien (dossier, point 7 ; n°14).
- **La solution** :
  1. **Un moteur d'exécution durable, sur le modèle de Temporal, en Java sur PostgreSQL.**
     - Chaque processus a un journal d'événements et se rejoue après une panne.
     - Les étapes ont des délais et des reprises ; les minuteries et les accords humains sont des signaux.
     - Les missions perdues sont reprises par le serveur (§13.2).
     - On copie le modèle, pas le serveur : l'app desktop reste légère. Temporal lui-même reste possible pour un grand
       serveur.
  2. **Les priorités, et ce que le système lâche d'abord quand il sature**, écrits avant (Hamilton).
  3. **Les événements du runner écrits sur disque d'abord**, puis renvoyés après une coupure.
  4. **Un vérificateur indépendant** (Bengio, Gawande) :
     - une étape tenue par un autre modèle, d'un autre fournisseur, non agentique ;
     - il suit une liste de contrôle ;
     - il estime le risque avant l'accord humain.
  5. **L'aperçu des effets avant d'agir** : le diff, les commandes, l'exécution à blanc (LeCun).
  6. **Un vrai bac à sable** : l'agent travaille dans un environnement isolé (conteneur ou machine légère), avec une règle
     pour le réseau.
  7. **Des paliers d'autonomie** : conseiller, adjoint, délégué.
     - Ils s'ouvrent sur preuve et se referment sur incident (Doudna, Zhuo).
     - Ils ne s'ouvrent jamais sur l'irréversible (R1).
  8. **Plusieurs agents en parallèle**, avec des quotas ; tout se voit dans la vue du travail (R95).
- **Exemple** : la machine s'endort au milieu d'un processus de six étapes. Au réveil, il reprend à l'étape quatre. Le
  dossier dit la coupure, et rien n'est fait deux fois.
- **Ce que ça change** : un processus ne se perd plus, et rien d'important ne passe sans un second regard.
- **Ce qui reste** : un moteur durable fait maison est un projet en soi (Musk). Il se construit mince en J2 et se complète en
  J5.
- **Vote** : 23 oui, 1 abstention (Musk : un moteur maison doit d'abord prouver qu'il vaut mieux que Temporal ; à mesurer en
  J2).
- **Jalon** : J2 pour le moteur v1 (journal et reprise), J5 pour le reste.
- **Preuve en dix jours** : on coupe le runner, puis le backend, au milieu d'une mission. Elle reprend ou s'arrête
  proprement, et le dossier le dit.
- **Signal d'arrêt** : une mission perdue découverte par une personne.

### R98. Des règles complètes, lisibles, publiées

- **Le problème** (n°14, point 5) :
  - le moteur ignore la classe d'une règle ;
  - onze actions sur trente ne sont produites par aucun code ;
  - les actions inverses ne s'exécutent pas ;
  - il n'y a ni seuil, ni double signature, ni séparation des rôles ;
  - les règles ne se lisent qu'en JSON.
- **La solution** :
  1. **Un contrat qui dit vrai** : le moteur applique la classe, les onze actions sans code sont retirées, et une action
     inverse s'exécute vraiment ou sort du contrat.
  2. **Des obligations** :
     - un seuil sur un champ (« au-delà de 5 000 € ») ;
     - une double signature ;
     - la séparation des rôles : celui qui prépare ne signe pas.
  3. **Des cas d'essai pour chaque règle**, rejoués à chaque modification. Une règle qui ne passe pas ses cas ne s'enregistre
     pas.
  4. **La charte des règles d'un espace**, en français et en anglais, tirée des règles réelles et lisible par un auditeur
     (Azoulay).
  5. **La spécification publiée** (règles, dossier, packs) comme la documentation de ce que fait le moteur, numérotée v0,
     avec ses cas (R89, Nilekani). Pas comme un standard (R9').
- **Exemple** : « tout devis au-delà de 5 000 € demande la signature du gérant, et celui qui l'a préparé ne peut pas la
  donner ».
- **Ce que ça change** : les règles d'une vraie entreprise s'expriment, se testent et se lisent.
- **Ce qui reste** : garder l'éditeur simple malgré les obligations (Jobs, Norman).
- **Vote** : 22 oui, 2 abstentions (Bezos et Jobs : publier avant d'avoir des clients va contre R9').
- **Jalon** :
  - J2 : l'éditeur v1, la classe appliquée, les actions mortes retirées ;
  - J3 : les obligations et la charte ;
  - J9 : la publication.
- **Preuve en dix jours** : une règle à seuil et à double signature, écrite dans l'éditeur, arrête la mission suivante au bon
  moment, et le dossier le montre.
- **Signal d'arrêt** : une règle enregistrée sans cas d'essai.

### R99. Un connecteur générique : un outil bien fait, puis tous les outils sans code

- **Le problème** :
  - GitHub est intégré en profondeur ;
  - MCP est générique : 25 préréglages, un seul essayé ;
  - l'ingestion n'est câblée que pour Plane, et chaque lecteur coûte trois à cinq jours de code.
- **La solution** :
  1. **Pour agir : MCP partout.** Le serveur MCP d'un outil se branche par un préréglage, sans code, et ses outils passent par
     les règles.
  2. **Pour lire : un manifeste déclaratif** remplace le code propre à chaque outil. Il décrit :
     - l'authentification et les points d'accès ;
     - la correspondance avec les types d'objets du métier ;
     - les droits de la source.

     Le lecteur de Plane est réécrit en manifeste ; puis un second outil s'ajoute sans une ligne de code.
  3. **Des essais de contrat**, générés depuis le manifeste pour chaque outil (Shotwell, Hamilton).
  4. **Les droits du système source sont conservés** (Nilekani). Les préréglages jamais essayés quittent le catalogue
     visible jusqu'à leur essai (Musk).
  5. **Un point de décision ouvert** : tout moteur d'agents extérieur peut demander la décision aux règles de l'espace et
     écrire au dossier, par MCP ou par HTTP. n8n, Copilot ou un agent maison restent ainsi sous les règles du métier
     (Nadella).
  6. **Le catalogue s'élargit plus tard**, par manifestes, à la demande des clients.
- **Exemple** : une entreprise veut lire les tickets de son outil de support. Elle importe un manifeste d'une vingtaine de
  lignes ; les tickets entrent dans les connaissances avec leurs droits, et aucun code n'est livré.
- **Ce que ça change** : un nouvel outil coûte un fichier, et plus quelques jours de code.
- **Ce qui reste** : un outil sans API propre ne se branche pas ainsi.
- **Vote** : 23 oui, 1 abstention (Saarinen : chaque outil mérite son geste dans l'interface).
- **Jalon** :
  - J4 : le manifeste d'ingestion ;
  - J5 : les actions et le point de décision ouvert ;
  - ensuite, à la demande.
- **Preuve en dix jours** : le second outil branché par son seul manifeste.
- **Signal d'arrêt** : un outil qui exige du code propre pour un besoin courant.

### R100. Tout se voit, tout se mesure, tout se signale

- **Le problème** (n°14, point 7) :
  - OpenTelemetry n'est pas activé en production ;
  - le journal d'audit ne compte que sept actions d'administration ;
  - la banque d'évaluations est manuelle et réservée à Cortex ;
  - l'effet des règles n'a jamais été essayé, et rien ne permet de signaler un incident.
- **La solution** :
  1. **OpenTelemetry actif par défaut**, vers un collecteur local, et exportable vers les outils de l'entreprise.
  2. **Le journal des actions d'IA** : chaque décision, chaque appel de modèle, chaque accord, avec son dossier.
  3. **La banque d'évaluations pour chaque processus, agent et pack**, avec une famille de sûreté.
  4. **L'essai contradictoire** d'après le Top 10 agentique de l'OWASP, rejoué par la CI, avec son taux d'arrêt publié (R89,
     Prabhakar).
  5. **Un registre des incidents** nourri par les dossiers, et un canal de signalement ouvert à tous, client ou non (Doudna,
     Li).
- **Vote** : 24 oui.
- **Jalon** :
  - J2 : le journal des actions d'IA ;
  - J6 : OpenTelemetry ;
  - J7 : la banque généralisée et l'essai contradictoire.
- **Preuve en dix jours** : le premier rapport d'essai contradictoire, avec son taux d'arrêt.
- **Signal d'arrêt** : une action d'agent absente du journal et des dossiers.

### R101. L'amélioration continue, toujours acceptée par une personne

- **Le problème** : la banque d'évaluations n'a pas de cas proposés, aucune recommandation n'est tirée des missions, et il
  n'existe ni affinage ni export de données d'entraînement (E12 proposée).
- **La solution** :
  1. **Des recommandations tirées des dossiers** :
     - un échec devient un cas d'évaluation ;
     - une règle qui demande souvent un accord sur du réversible devient une proposition de règle (E7 mesurée) ;
     - une question de l'agent qui revient devient une tâche de connaissance ;
     - une étape lente ou souvent ratée devient une proposition de processus.
  2. **Chaque recommandation reste une proposition** (Harari). Elle a un responsable, une personne l'accepte ou la refuse,
     elle est versionnée, et les évaluations la jugent avant et après.
  3. **Les données possédées** (mécanisme C) : les résultats acceptés deviennent des jeux de données, avec leur provenance,
     leur classe et le consentement.
  4. **L'affinage chez le client** (mécanismes C et D).
     - TaskForce prépare les données, lance l'affinage sur la machine ou chez le fournisseur que l'entreprise choisit, puis
       évalue.
     - Un modèle affiné n'entre au registre qu'avec un gain mesuré et la famille de sûreté passée, et il se retire d'un
       geste (Bengio).
  5. **Les paliers d'autonomie bougent sur ces preuves** (R97), jamais sur l'irréversible (R1).
- **Exemple** : la règle « envoyer la liste des pièces » a demandé quarante accords, tous donnés. TaskForce propose de
  l'autoriser sous 500 €. Le gérant accepte, les évaluations sont rejouées, et le dossier garde sa décision.
- **Vote** : 22 oui, 1 non, 1 abstention.
  - Non : Musk, pour qui l'affinage avant le premier client est du stock.
  - Abstention : Bezos, même réserve, sans s'y opposer.
- **Jalon** : J2 (un échec devient un cas), J7 (le reste).
- **Preuve en dix jours** : un échec semé devient un cas, une correction est acceptée, et la mission suivante passe.
- **Signal d'arrêt** : une recommandation appliquée sans qu'une personne l'ait acceptée.

### R102. Le parcours d'arrivée est un jeu qui construit du vrai

- **Le problème** :
  - aucun parcours d'arrivée n'existe ; celui du texte, en huit étapes, est fait par des consultants (n°14, ligne 16) ;
  - le premier lancement de l'app desktop ouvre un espace vide, ce qui avait surpris la Présidence le 20/10/2026.
- **La solution** :
  1. **Un parcours mené par un agent, en niveaux**. Chaque niveau produit une vraie configuration :
     1. Qui êtes-vous ? (le profil de l'espace) ;
     2. Vos mots (le vocabulaire et les types) ;
     3. Vos lignes rouges (les règles) ;
     4. Vos sources (les connaissances) ;
     5. Votre premier agent (son rôle, son modèle) ;
     6. Votre premier processus ;
     7. La première mission, le niveau final ;
     8. La preuve (lire son dossier) ;
     9. Améliorer (accepter une recommandation).
  2. **Le ressort du jeu** :
     - une progression visible et un retour immédiat ;
     - des exemples tirés du métier de la personne ;
     - un bac à sable avec des données d'essai ;
     - le droit de sauter un niveau ou de reprendre plus tard.
  3. **Aucun piège d'attention** : ni série à tenir, ni récompense d'engagement, ni compte à rebours (Harris). Un mode sobre
     pour qui le préfère.
  4. **Il enseigne comment le système fonctionne** : la personne finit en sachant ce qu'est une règle, un accord et un
     dossier (Norman). C'est aussi une liste de contrôle (Gawande).
  5. **Il est essayé avant d'être construit** : une maquette en J3, jouée par des personnes extérieures, puis la construction
     en J8.
- **Exemple** : une gérante d'agence installe l'app. Quarante minutes plus tard, sans aide, elle a son vocabulaire, cinq
  règles et un processus de demande d'intervention. Elle lit le dossier de sa première mission.
- **Premier tour** : 20 oui, 4 non (Harris, Shotwell, Gawande, Vestager). Un jeu, dans un produit d'entreprise, manipule ou
  fait peu sérieux.
- **Amendements** :
  - aucun piège d'attention ;
  - chaque niveau construit du vrai ;
  - un mode sobre ;
  - le parcours sert aussi de liste de contrôle.
- **Vote final** : 23 oui, 1 abstention (Shotwell : un acheteur industriel demande d'abord un plan d'installation).
- **Jalon** : J3 pour la maquette essayée, J8 pour la construction.
- **Preuve en dix jours** : la maquette jouée par trois personnes extérieures ; on note où chacune s'arrête.
- **Signal d'arrêt** : une personne qui finit le parcours sans savoir ce qu'est une règle.

### R103. L'infrastructure, pas les règles : aucun secteur d'abord, trois métiers pour la démo

- **Le problème** : la Présidence dit « nous on creer l'infra, pas les regles en elles mm » et « c est tout industrie ou
  entreprise ». Or R85 et les niches A et B de la séance n°2 visaient des secteurs.
- **La solution** :
  1. **TaskForce ne choisit aucun secteur et n'écrit les règles d'aucun métier.** Les secteurs régulés ne sont pas exclus :
     leurs gens écrivent leurs packs.
  2. **La généralité se prouve par trois packs de démonstration**, de natures différentes, faits par configuration
     seulement :
     - **Livraison logicielle** : de l'issue à la pull request, tests compris ;
     - **Rédaction et revue de document** : du brief au document cité, revu, puis approuvé ;
     - **Traitement de demandes** : une demande entre, puis elle est qualifiée, préparée, vérifiée, accordée et répondue.
  3. **Trois personnes-types, une par pack**, chacune avec son test de première minute et de première semaine (Zhuo) :
     - une responsable de livraison logicielle ;
     - une professionnelle de l'écrit (juriste, rédactrice, chargée de qualité) ;
     - un responsable d'opérations.
  4. **Les besoins propres à un secteur viennent des clients**, et deviennent des packs.
  5. **Zéro ligne de code propre à un pack**, vérifié par un contrôle de la CI.
- **Ce que ça change** : remplace les niches A et B de la séance n°2. C'est un changement de positionnement, donc un ADR.
- **Premier tour** : 18 oui, 6 non (Zhuo, Saarinen, Jobs, Bezos, Duflo, Musk). « Pour tous », c'est « pour personne ».
- **Amendements** :
  - trois personnes-types précises pour la démo ;
  - des yeux extérieurs dès J2 ;
  - zéro code par pack.
- **Vote final** : 22 oui, 2 non (Zhuo et Saarinen, maintenus).
- **Jalon** : J2 (deux packs), J3 (le troisième), J8 (les trois, montés par le jeu).
- **Preuve en dix jours** : le deuxième pack tourne sans une ligne de code de plus que le premier.
- **Signal d'arrêt** : un pack qui exige du code propre.

### R104. La confiance est l'indicateur premier, et elle se mesure

- **Le problème** : la Présidence dit « c'est pas le temps ici le KPI principale, c'est la confiance ». À la n°14, Bezos
  parlait d'heures gagnées et de clients.
- **La solution** : l'indice de confiance, un ensemble de signaux mesurés à chaque jalon, chacun avec son seuil (détail plus
  bas) :
  - la couverture des règles et la preuve vérifiable ;
  - l'effet des règles (leur taux d'arrêt) ;
  - les résultats acceptés sans correction ;
  - les accords réellement lus, l'autonomie accordée, les flux visibles ;
  - le retour des personnes extérieures ;
  - le temps et les erreurs, avant et après, comme composantes et jamais seuls (Gawande).
- **Conditions** :
  - des critères écrits avant (Duflo), avec une mesure de départ à J2 ;
  - aucun signal d'engagement (Harris) ;
  - un tiers à J8 (Li).
- **Vote** : 24 oui. Bezos y retrouve un principe qu'il connaît, et garde le comportement comme juge.
- **Jalon** : la mesure de départ à J2, puis chaque jalon.
- **Preuve en dix jours** : la mesure de départ, sur la boucle actuelle (Créer, Accorder, Relire).
- **Signal d'arrêt** : un signal qui se dégrade deux jalons de suite.

### R105. La feuille de route en dix jalons, chacun validé

- **La solution** : les dix jalons ci-dessous, et le même rituel de validation à chacun.
  - « Devant » est défini ligne par ligne, avec sa preuve (la carte cible).
  - La démo est montrable dès J2.
  - Une version de la boucle se construit chaque jour (Musk).
  - Chaque jalon a un « go / no-go » écrit avant (Prabhakar), une liste de lancement (Shotwell) et des personnes
    extérieures dès J2 (Zhuo, Bezos, Duflo).
- **Premier tour** : 20 oui, 4 non (Zhuo, Musk, Bezos, Duflo) : sept mois de construction avant le premier utilisateur.
- **Amendements** :
  - une démo complète mais mince dès J2 ;
  - des personnes extérieures à chaque jalon à partir de J2 ;
  - une version de la boucle chaque jour.
- **Vote final** : 23 oui, 1 non (Zhuo : le plan reste écrit avant la première personne).
- **Preuve en dix jours** : J0 fini, et le déroulé de la démo écrit (Bezos, Jobs).
- **Signal d'arrêt** : un jalon qui dépasse de moitié sa taille sans décision de la Présidence.

### R106. Gratuit aujourd'hui, payant demain : le modèle se décide avant la tournée

- **Le problème** : la Présidence dit « Pour l instant c est gratuit mais ca va pas le rester ». Stripe a été retiré le
  18/10/2026, et il n'y a aucun revenu.
- **La solution** :
  1. **Rien de payant ne se construit avant J9.**
  2. **Trois options instruites avant J8** :
     - **une double licence** : l'AGPL, et une licence commerciale pour qui ne veut pas de ses obligations ;
     - **l'open core** : le cœur sous AGPL, et des fonctions d'entreprise payantes (SSO, serveur à plusieurs espaces,
       conservation légale, horodatage, support) ;
     - **l'installation et le support payants**.

     La version hébergée viendra quand le budget le permettra.
  3. **Le cœur reste sous AGPL**, quel que soit le choix (Mazzucato).
  4. **La disposition à payer se teste pendant les démos de J8** (Bezos). La Présidence tranche à J9.
  5. **Une vérification juridique** : la double licence suppose de détenir les droits sur tout le code, contributions
     comprises.
- **Vote** : 24 oui.
- **Jalon** : J8 pour l'instruction et le test, J9 pour la décision.
- **Preuve en dix jours** : les trois options écrites sur une page, avec ce que chacune exige.
- **Signal d'arrêt** : une fonction payante construite avant la décision.

### Les votes en une table

| R | Solution | Oui | Non | Abstention | Part de oui |
| --- | --- | --- | --- | --- | --- |
| R90 | Un seul moteur, en Java | 24 | | | 100 % |
| R91 | Le desktop seul ; la webapp gelée puis fermée | 23 | | Nadella | 95,8 % |
| R92 | Aucun modèle imposé | 24 | | | 100 % |
| R93 | On sait où va chaque donnée | 24 | | | 100 % |
| R94 | Le métier construit son outil | 22 | Zhuo | Saarinen | 91,7 % (19 au premier tour) |
| R95 | Une surface par partie, l'assistant partout | 23 | | Jobs | 95,8 % |
| R96 | Un contexte juste, l'agent qui demande | 24 | | | 100 % |
| R97 | Des agents robustes, vérifiés, visibles | 23 | | Musk | 95,8 % |
| R98 | Des règles complètes, lisibles, publiées | 22 | | Bezos, Jobs | 91,7 % |
| R99 | Un connecteur générique | 23 | | Saarinen | 95,8 % |
| R100 | Tout se voit, se mesure, se signale | 24 | | | 100 % |
| R101 | L'amélioration continue, acceptée par une personne | 22 | Musk | Bezos | 91,7 % |
| R102 | Le parcours-jeu | 23 | | Shotwell | 95,8 % (20 au premier tour) |
| R103 | L'infrastructure, pas les règles ; trois métiers | 22 | Zhuo, Saarinen | | 91,7 % (18 au premier tour) |
| R104 | La confiance, mesurée | 24 | | | 100 % |
| R105 | Dix jalons validés | 23 | Zhuo | | 95,8 % (20 au premier tour) |
| R106 | Le modèle de revenus avant la tournée | 24 | | | 100 % |

## La feuille de route : dix jalons, chacun validé

### Les principes

1. **Une boucle complète tôt, puis on l'épaissit.** La démo est montrable à J2, et complète à J8.
2. **Une brique remplace des fonctions.** Chaque jalon supprime ce que ses briques remplacent (Musk).
3. **Rien n'est « devant » sans sa preuve**, vue par quelqu'un d'extérieur.
4. **Le banc d'essai de référence** est la machine de la Présidence : l'app desktop, Claude Code et Ollama. Plus aucun test
   sur la webapp (R91).
5. **Le code ne connaît aucun métier** : zéro ligne propre à un pack (R103).
6. **Un seul moteur, en Java** (R90).

### Le rituel de validation, à la fin de chaque jalon

1. **Avant** : les critères de sortie et leurs seuils sont écrits (Duflo, Prabhakar).
2. **Pendant** : une version de la boucle se construit chaque jour (Musk).
3. **À la fin** :
   1. la boucle de démo rejouée de bout en bout sur le banc de référence (Jobs) ;
   2. les tests verts : unitaires, d'intégration, cas de conformité, essai contradictoire (Hamilton, Prabhakar) ;
   3. la liste de lancement : installation propre, mise à jour, sauvegarde et restauration (Shotwell) ;
   4. à partir de J2, au moins trois personnes extérieures, d'au moins deux métiers (Zhuo, Bezos) ;
   5. l'indice de confiance mesuré (R104) ;
   6. une séance restreinte du Conseil, qui juge le jalon : continuer, corriger ou arrêter ;
   7. le go de la Présidence, puis la release sur son « go release ».

### Les dix jalons en une table

Les tailles sont des `[HYPOTHÈSE]`, recalées sur la vitesse réelle à la fin de J1. Calendrier indicatif pour une seule
personne aidée d'agents :
- la démo mince vers le début de janvier 2027 ;
- la démo complète vers la fin de mai 2027 ;
- la mise sur le marché en juin 2027.

| Jalon | Ce qu'il donne | Taille | Lignes de la carte qui passent devant |
| --- | --- | --- | --- |
| **J0** Dire vrai, fermer les failles | La recherche respecte les droits ; « Apply » respecte les tests ; les pages disent vrai ; la webapp gelée ; R78 publiée | 1 semaine | 2 et 10, en partie |
| **J1** Un seul moteur, un desktop qui tient seul | Décision, preuve et passerelle en Java ; plus de Python ni de doublon TypeScript ; l'identité locale | 2 à 3 semaines | 1, 3 en partie, 10 |
| **J2** La boucle complète, mince | Processus modifiable, agents, règles éditables, documents cités, vue du travail, dossier signé, un échec devient un cas ; deux packs | 4 à 5 semaines | 5, 9 en partie, 14 |
| **J3** Le métier construit son outil | Profil, vocabulaire, types, règles complètes, packs, français et anglais, maquette du jeu ; le troisième pack | 3 semaines | 4, 17, 18 |
| **J4** Le contexte | Tous les documents, droits prouvés, recherche hybride, citations, l'agent qui demande, surface Connaissances, manifeste d'ingestion | 4 semaines | 8, 12 pour la lecture |
| **J5** Des agents robustes | Moteur durable complet, vérificateur, aperçu des effets, bac à sable, paliers, registre et routage des modèles, point de décision ouvert | 4 semaines | 3, 5, 9, 11, 12 pour l'action |
| **J6** Données souveraines, preuve d'auditeur | Carte des flux, règles de sortie, chiffrement, dossier horodaté et conservé, export complet, profil serveur, kit de conformité, OpenTelemetry | 3 semaines | 2, 6, 13 en partie |
| **J7** L'amélioration continue | Recommandations, banque généralisée, essai contradictoire, données possédées, affinage chez le client, objectifs | 3 semaines | 13, 14, 15 |
| **J8** Le jeu et la démo complète | Le parcours-jeu ; les trois packs montés par le jeu ; cinq personnes extérieures ; une évaluation par un tiers | 3 semaines | 7, 16, 19 |
| **J9** La mise sur le marché | Le modèle de revenus, la distribution, la spécification et l'essai publiés, le serveur selon le budget | 2 semaines, puis en continu | 20, 21 |

### J0. Dire vrai, fermer les failles (une semaine)

- **Pourquoi d'abord** : une entreprise dont le produit est la confiance ne garde ni une faille ouverte ni une page qui ment
  (R82, R87).
- **Contenu** :
  1. La recherche du Brain OS respecte les droits des projets privés, avec un essai qui le prouve. La tâche est déjà
     proposée.
  2. « Apply » se désactive quand les tests ont échoué. Passer outre demande un geste explicite et une raison écrite au
     dossier (R87).
  3. Un accord refusé faute de réponse le dit à la personne (Norman, n°14).
  4. Les pages et documents faux de la n°14 (point 8) sont corrigés, dont la confidentialité et l'hébergement de la webapp
     tant qu'elle tourne (R82).
  5. La webapp est gelée (R91).
  6. R78 est publiée (Créer, Accorder, Relire), sur « go release ».
- **Sortie** :
  - un commit par écart fermé ;
  - l'essai des droits de recherche vert ;
  - R78 publiée, avec « Apply » bloqué sur un échec de tests ;
  - la boucle actuelle rejouée de bout en bout sur l'app desktop.
- **Ce que la Présidence voit** : une mission dont les tests échouent ne s'applique pas sans qu'elle le décide et l'écrive.

### J1. Un seul moteur, un desktop qui tient seul (deux à trois semaines)

- **Contenu** :
  1. La décision en Java seulement (R90). Le runner envoie les faits ; le backend de la machine décide, écrit la chaîne et
     répond. Sans réponse, aucune action.
  2. La vérification d'un export par un outil Java livré avec l'app ; la spécification et les cas publiés.
  3. La passerelle de modèles en Java : Ollama, API compatible OpenAI, Anthropic. L'ai-service Python et le relais de la
     coque sont supprimés (R90, R92).
  4. L'identité locale : l'app s'installe et vit sans compte ni réseau, et les installations connectées gardent tout (R91).
  5. La règle d'architecture (ADR) et son contrôle dans la CI.
  6. Les suppressions demandées par Musk : les préréglages jamais essayés quittent le catalogue visible, et le plan figé
     d'« AI Workflows » disparaît.
- **Sortie** :
  - une mission déléguée de bout en bout, chaque action décidée en Java, la latence de décision mesurée ;
  - les 51 cas verts en Java, et aucun moteur hors de Java (contrôle de la CI) ;
  - Cortex sur Ollama par la passerelle Java ;
  - une installation neuve, réseau coupé, utilisable ;
  - la liste de lancement.
- **La décision attendue de la Présidence à la fin** : fermer la webapp, avec préavis, export puis extinction ?
- **Ce que la Présidence voit** : l'app installée sur une machine neuve, sans réseau, qui délègue une tâche à Claude Code
  sous les règles.

### J2. La boucle complète, mince (quatre à cinq semaines)

- **Le principe** : toute la boucle existe de bout en bout, en version mince, sur deux natures de travail, sans code propre
  à l'une ou à l'autre. La démo devient montrable.
- **Contenu** :
  1. Le déroulé de la démo écrit d'abord, avec son communiqué et sa foire aux questions (Bezos, Jobs).
  2. **Processus v1** : un canevas modifiable (React Flow est déjà dans la pile).
     - Cinq types d'étapes : agent, décision humaine, outil MCP, condition, vérification.
     - Le processus est versionné, et exécuté par le moteur durable v1 (journal et reprise, R97).
  3. **Agents v1** : un rôle, des consignes, des outils, un modèle, un palier. Deux moteurs : Claude Code, et la boucle
     d'agent de TaskForce sur n'importe quel modèle (R92, qui rend R51 possible).
  4. **Règles v1 éditables** : l'éditeur en mots, la table V102 écrite, la classe appliquée, les actions mortes retirées,
     des cas d'essai par règle (R94, R98).
  5. **Contexte v1** : des documents (PDF, Word, Markdown) importés avec leur version, leur responsable et leur date de
     validité, et cités au passage près (R96).
  6. **La vue du travail v1**, et les surfaces Travail, Processus et Règles, avec l'assistant (R95).
  7. **Dossier v1** : il survit à la suppression, il est signé par la clé de l'espace, exporté et vérifié par l'outil Java.
     Le journal des actions d'IA s'ouvre (R93, R100).
  8. **Amélioration v1** : un échec devient un cas en un geste (R101).
  9. **Deux packs** : Livraison logicielle, et Rédaction et revue de document (R103).
- **Sortie** :
  - la démo jouée de bout en bout sur les deux packs, avec Claude Code puis avec Ollama ;
  - zéro ligne de code propre à un pack (contrôle de la CI) ;
  - trois personnes extérieures, de deux métiers, dont une non développeuse qui construit seule un processus de trois
    étapes ;
  - la mesure de départ de l'indice de confiance.
- **Ce que la Présidence voit** : un brief entre, et un document cité en sort. Un second modèle le relit, elle l'accorde, et
  un dossier vérifiable le garde. La même chose se fait pour une issue de code.

### J3. Le métier construit son outil (trois semaines)

- **Contenu** :
  1. Le profil de l'espace, c'est-à-dire la grille de variables : il règle les valeurs par défaut et se voit dans chaque
     décision (R94).
  2. Le vocabulaire et les types d'objets du métier.
  3. Les règles complètes : seuils, double signature, séparation des rôles, actions inverses réelles, charte lisible en
     français et en anglais (R98).
  4. Les packs : l'export et l'import d'une configuration complète, au format ouvert.
  5. L'interface en français et en anglais.
  6. La maquette du parcours-jeu, jouée par trois personnes extérieures (R102).
  7. Le troisième pack : Traitement de demandes (R103).
- **Sortie** :
  - une personne d'un métier que l'équipe ne connaît pas configure seule son vocabulaire, deux types, cinq règles et un
    processus, en moins d'une heure ;
  - un pack exporté puis importé reproduit l'espace ;
  - le troisième pack tourne sans code.
- **Ce que la Présidence voit** : quelqu'un du métier monte devant elle un exemple comme celui des ascenseurs.

### J4. Le contexte, la grande guerre (quatre semaines)

- **Contenu** :
  1. Tous les formats courants, avec leur structure, et les versions comparées (R96).
  2. Les droits appliqués dans la requête, et prouvés par un essai contradictoire.
  3. La recherche hybride (texte intégral, vecteurs, graphe, reclassement local) et les citations au passage près.
  4. L'agent qui demande : l'outil « demander », le détecteur de manque, la question au responsable, la réponse versionnée.
  5. La surface Connaissances : les sources, leur fraîcheur, leurs responsables, les manques, les contradictions.
  6. Le manifeste d'ingestion : Plane réécrit en manifeste, puis un second outil sans code (R99).
  7. Les évaluations de recherche, pack par pack.
- **Sortie** :
  - la précision de recherche mesurée sur les trois packs, en hausse depuis J2 ;
  - sur un manque semé, l'agent demande, et la réponse sert ensuite ;
  - l'essai des droits vert ;
  - le second outil branché par son seul manifeste.

### J5. Des agents robustes, vérifiés, visibles (quatre semaines)

- **Contenu** :
  1. Le moteur durable complet (R97) :
     - les délais, les reprises, les minuteries, les signaux et les baux ;
     - la reprise des missions perdues ;
     - les priorités et le délestage, écrits avant.
  2. Les événements du runner sur disque, renvoyés après une coupure.
  3. Le vérificateur indépendant, avec sa liste de contrôle et son estimation du risque.
  4. L'aperçu des effets, et le bac à sable isolé.
  5. Les paliers d'autonomie sur preuve, jamais sur l'irréversible (R1).
  6. Le registre des modèles complet : le routage par tâche et par classe, le secours, le budget, le changement sous
     évaluation (R92).
  7. Le point de décision ouvert aux moteurs d'agents extérieurs (R99).
  8. Plusieurs agents en parallèle, avec des quotas, et la vue du travail complète.
- **Sortie** :
  - des coupures provoquées (runner, backend, mise en veille) : reprise ou arrêt propre, et le dossier le dit ;
  - une erreur semée, arrêtée par le vérificateur ;
  - un agent promu puis rétrogradé sur preuve ;
  - le même processus sur Claude Code, sur Ollama et sur une API compatible OpenAI.

### J6. Données souveraines, preuve d'auditeur (trois semaines)

- **Contenu** :
  1. La carte des flux, et les règles de sortie par classe de donnée (R93).
  2. Le chiffrement du contenu au repos et des sauvegardes, gardées hors de la machine ; TLS côté serveur.
  3. Le dossier horodaté et conservé pour une durée choisie ; les dossiers de Cortex exportés.
  4. L'export complet (R64).
  5. Le profil serveur auto-hébergé (Docker Compose), documenté.
  6. Le kit de conformité tiré de la configuration.
  7. OpenTelemetry actif et exportable (R100).
- **Sortie** :
  - une capture réseau de la démo, identique à la carte des flux ;
  - une restauration chiffrée sur une autre machine ;
  - un dossier vérifié hors ligne par une personne extérieure, idéalement de l'audit ou de la conformité, qui dit ce qui lui
    manque.

### J7. L'amélioration continue (trois semaines)

- **Contenu** :
  1. Les recommandations tirées des dossiers : les échecs, les accords répétés, les questions, les étapes lentes. Une personne
     les accepte, et les évaluations les jugent avant et après (R101).
  2. La banque d'évaluations pour chaque processus, agent et pack, avec la famille de sûreté.
  3. L'essai contradictoire (Top 10 agentique de l'OWASP) dans la CI, avec son taux d'arrêt publié (R100).
  4. Les données possédées, et l'affinage chez le client, sous évaluation et sous la famille de sûreté.
  5. Les objectifs de chaque processus (R56).
- **Sortie** :
  - un échec récurrent semé devient un cas ; une correction est acceptée, et la mission suivante passe ;
  - un modèle refusé parce que ses évaluations reculent ;
  - un rapport d'amélioration lisible par le métier.

### J8. Le parcours-jeu et la démo complète (trois semaines)

- **Contenu** :
  1. Le parcours-jeu construit (R102).
  2. Les trois packs montés par le jeu, chacun par une personne-type (R103).
  3. Cinq personnes de cinq métiers, dont trois non développeuses, sans aide, et une évaluation par un tiers (Li).
  4. E14 : la promesse redite en une phrase.
  5. Les trois options de revenus testées pendant les démos (R106).
- **Sortie** :
  - quatre personnes sur cinq arrivent seules à leur première mission sous règles, en moins d'une heure ;
  - l'indice de confiance au-dessus des seuils fixés à J2 ;
  - la promesse redite par trois personnes sur cinq.

### J9. La mise sur le marché (deux semaines, puis en continu)

- **Contenu** :
  1. Le modèle de revenus, tranché par la Présidence (R106).
  2. La distribution : l'installateur et la version du Microsoft Store, les mises à jour, un dossier d'exploitation et de
     support, un paquet de sécurité (SBOM, politique de vulnérabilités).
  3. La publication de la spécification (règles, dossier, packs) et du rapport d'essai contradictoire (R98, R100).
  4. Le retour du serveur hébergé quand le budget le permet, avec le même moteur.
- **Sortie** : un premier pilote engagé, payant ou par une lettre d'intention signée.

### Les trois phases du texte, dans cette feuille de route

| Phase du texte | Jalons | Ce qui est devant |
| --- | --- | --- |
| 1. Un noyau sur un cas étroit | J0 à J2 | Le noyau sert deux natures de travail, pas une ; il est local, et sa preuve se vérifie sans TaskForce |
| 2. La personnalisation contrôlée | J3 à J7 | Faite par le métier, sans code et sans consultant, et jugée par les évaluations |
| 3. L'entreprise pilotée par des agents | J8, J9, puis la suite | Des paliers sur preuve, jamais sur l'irréversible, et une personne qui répond de chaque processus |

## La carte cible : devant sur chacune des 21 lignes

« Devant » se dit face au texte, comme dans le tableau de la Présidence : faire mieux ou plus concret que lui. La dernière
colonne dit, honnêtement, la position visée face au marché (débat 2).

| # | Ligne | Aujourd'hui (n°14) | « Devant » veut dire | La preuve | Jalon | Face au marché |
| - | --- | --- | --- | --- | --- | --- |
| 1 | La thèse | Pile | La seule couche de contrôle qui tourne entière chez le client, avec n'importe quel modèle, et dont la preuve se vérifie sans TaskForce | Installation neuve hors réseau ; dossier vérifié hors TaskForce | J1, J6 | Mener |
| 2 | Souveraineté des données | En route | Chaque sortie visible et soumise à une règle ; contenu et sauvegardes chiffrés ; hébergement au choix ; export complet | Capture réseau identique à la carte ; restauration ailleurs | J1, J6 | Mener |
| 3 | Souveraineté des modèles | En route | N'importe quel modèle, routé par classe de donnée, changé sous évaluation | Un même processus sur trois fournisseurs | J1, J2, J5 | Mener sur le routage par classe de donnée |
| 4 | Souveraineté du métier | Derrière | Le métier écrit ses types, règles, processus, agents et évaluations sans code, et les emporte en pack | Une personne d'un métier inconnu configure seule ; un pack réimporté | J2, J3 | Mener |
| 5 | Souveraineté des agents | Devant, sans éditeur | Chaque action sous règles, vue en direct ; des paliers sur preuve ; un vérificateur indépendant | Essai contradictoire ; paliers qui bougent sur preuve | J2, J5 | Parité, mener en local |
| 6 | Souveraineté opérationnelle | En route | Dossier signé, conservé, rejouable ; retour arrière réel ; changement de fournisseur | Un processus rejoué ; une action inverse exécutée | J5, J6 | Mener sur la preuve vérifiable |
| 7 | Couche 1, le cockpit | Ailleurs, et derrière sur les objectifs | Une surface par brique, une grammaire, l'assistant partout, la vue du travail, les objectifs ; aucun écran de surveillance | Cinq personnes extérieures trouvent seules | J2 à J8 | Parité |
| 8 | Couche 2, le contexte | Derrière | Des documents versionnés et à responsable, des droits prouvés, des citations au passage, l'agent qui demande | Précision mesurée par pack ; manque semé | J2, J4 | Mener sur les droits et la demande |
| 9 | Couche 3, le runtime | En route, mince | Exécution durable, reprise, vérificateur, aperçu des effets, bac à sable | Coupures provoquées | J2, J5 | Parité, mener en local |
| 10 | Couche 4A, les politiques | Devant sur le moteur, derrière sur la gouvernance | Un seul moteur, éditable par le métier, avec obligations, cas d'essai par règle, charte lisible, spécification publiée | Une règle à seuil et à double signature | J1, J2, J3, J9 | Mener |
| 11 | Couche 4B, la passerelle | Derrière | Registre, routage par tâche et par classe, secours, budget, changement sous évaluation | Un appel refusé vers un modèle non permis | J1, J5 | Parité, mener sur la classe de donnée |
| 12 | Couche 5, les intégrations | Derrière, par choix | MCP pour agir, un manifeste pour lire, zéro code par outil, des droits conservés, un point de décision ouvert | Un second outil par son seul manifeste | J4, J5 | Derrière sur le nombre d'outils (assumé), mener sur le coût d'un ajout |
| 13 | Couche 6, audit et évaluation | Devant sur la preuve, derrière sur l'observabilité | OpenTelemetry, journal des actions d'IA, banque généralisée, essai contradictoire publié, incidents | Le rapport d'essai publié | J2, J6, J7 | Mener sur le taux d'arrêt publié |
| 14 | Mécanismes A et B | Pile sur l'ordre | Contexte et règles mesurés, et améliorés par le métier | Précision et effet mesurés avant et après | J4, J7 | Mener |
| 15 | Mécanismes C et D | Pile sur la décision | Données possédées, affinage chez le client, entrée au registre sous évaluation et sûreté, retrait d'un geste | Un modèle affiné refusé, puis accepté sur preuve | J7 | Mener à faible coût |
| 16 | Le parcours d'arrivée | Ailleurs | Un jeu mené par un agent, qui construit le vrai espace en moins d'une heure, sans consultant | Cinq personnes extérieures | J3, J8 | Mener |
| 17 | La grille de variables | En route | Le profil de l'espace, explicite, modifiable, qui règle les valeurs par défaut et se voit dans chaque décision | Un changement de profil change une décision | J3 | Mener |
| 18 | L'exemple (la pharmacie) | Ailleurs | Trois métiers de natures différentes, montés par configuration ; un pack de la pharmacie serait écrit par ses gens | Trois packs, zéro code | J2, J3, J8 | Sans objet : aucun secteur choisi |
| 19 | Les trois phases | En route | Les phases 1 et 2 du texte deviennent du produit, plus du service | Les jalons validés | J0 à J9 | Mener |
| 20 | La pile technique | Pile | La même pile, un seul moteur, l'exécution durable sur le modèle de Temporal ; « pile », voulu par la Présidence | Aucun second moteur (contrôle de la CI) ; coupures provoquées | J1, J5 | Parité |
| 21 | L'opportunité | En route, ailleurs dans les faits | Une offre générale, un modèle de revenus, des besoins clients qui deviennent des packs | Un premier pilote engagé | J9 | À prouver |

## L'indice de confiance

Un ensemble de signaux, pas un chiffre unique : un indice composé se triche (Duflo, Li). Les seuils sont des
`[HYPOTHÈSE]`, fixés pour de bon à J2 avec la mesure de départ.

| Signal | Ce qu'il mesure | Seuil visé | Dès |
| --- | --- | --- | --- |
| Couverture des règles | La part des actions d'agents jugées par une règle | 100 % | J1 |
| Preuve vérifiable | La part des dossiers qui se vérifient hors TaskForce | 100 % | J2 |
| Effet des règles | Le taux d'arrêt de l'essai contradictoire | Publié, en hausse à chaque jalon | J7 |
| Justesse | La part des résultats acceptés sans correction | En hausse depuis la mesure de départ | J2 |
| Accords lus | La part des accords donnés après lecture du détail ; la part des demandes qui portent sur du réversible (E7) | Le réversible demandé en baisse | J2 |
| Autonomie accordée | La part des actions qu'une personne fait passer à un palier supérieur | En hausse | J5 |
| Flux visibles | La part des sorties de données présentes dans la carte des flux | 100 % | J6 |
| Retour extérieur | La part des personnes extérieures qui laisseraient l'agent agir chez elles | 3 sur 5 au moins à J8 | J2 |
| Temps et erreurs | Avant et après, sur les tâches de démo | Mesurés, jamais seuls | J2 |

## Décision de la Présidence

Le 01/11/2026, dans ses mots.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| Lecture des décisions de la n°14 | Confirmée | « Daccord partout apres » |
| R90. Un seul moteur, en Java | **À l'essai** : le double moteur reste, protégé par les 51 cas partagés ; on cherche une source unique sans aller-retour vers Java (E16), puis la Présidence tranche | « Ok alors on peut garder du coup ca me va comme reponse en soit » ; « R90 du coup faut voir, si on a pas une solution parce qu c'est vrai que c est lourd d'appeler Java a chaque fois » |
| R91. L'app desktop seule, la webapp gelée | **Modifiée** : la webapp reste en ligne, reçoit chaque release et sert la connexion de l'app desktop ; on n'y teste rien pour l'instant ; l'app desktop est le banc d'essai. Ni identité locale, ni fermeture | « nan on ferme pas la webapp, juste ne concidere pas faire de test dessus, ce sera plus tard (parce que pas de serveur, pas d'API Claude ou autre, pas de connexion possible avec des agent ou autre a moins de payer bref) » ; « on pousse tout sur la webapp on se connecte dessus et tout mais pour l instant fait comme si y avait personne dessus donc on test sur l'app desktop » |
| R92. Aucun modèle imposé | **Retenue, élargie** : toute entreprise ou personne branche son LLM ou ses modèles, quels qu'ils soient ; TaskForce ne gère pas les modèles, sauf l'entraînement si c'est possible | « oui mais c est plus que ca, n'importe quelle entreprise ou personnes devrait pouvoir se connecter a son LLM/ses differents model. Peut importe ce que c'est je m'en fiche, nous on gere pas les modeles (sauf partie entrainement si on peut) » |
| R93 à R98, R100, R101 | Retenues | « Daccord partout apres » |
| R99. Un connecteur générique | Retenue ; le branchement à n8n (point 5) reporté (Q14) | « On va pas se brancher a n8n je pense, enfin jsp a voir » |
| R102. Le parcours d'arrivée | **Retenue, précisée** : ce n'est pas un jeu, il se vit comme un jeu : ludique, jamais pénible à remplir | « c'est pas un jeu, ca doit faire comme un jeu, donc ludique, pas chiant a remplir mais oui » |
| R103. L'infrastructure, pas les règles | **Retenue, modifiée** : une infrastructure générale, montrée sur trois natures de travail ; pas un produit pour tous les métiers pour le moment | « Je suis d'accord avec Zhuo, mais je n'ai pas la pretention de faire un produit pour tout les metiers pour le moment » |
| R104 et R105 | Retenues | « faut une boucle qui tourne devant le clienet qu'il voit l interet directement » |
| R106 | Retenue | « Daccord partout apres » ; « Pour l instant c est gratuit mais ca va pas le rester » |
| La règle des 90 % | Inscrite à la charte (§6) | « me faut au moins 90% de oui sur chaque solutions trouve a un pb » |
| Lancer la feuille de route | Oui | « Tu peux y aller a fond, mets a jour la doc et vas y fonce » |

### Ce que la décision change à la feuille de route

- **J0** ne change pas, sauf un point : la webapp n'est pas gelée, elle reçoit chaque release ; on n'y teste rien. La
  correction de la recherche existe déjà : une session dédiée l'a faite le 31/10/2026 (`taskforce-fullstack` #459), avec
  sa voisine sur l'analyse d'un projet privé (#460).
- **J1** devient « Aucun modèle imposé, et l'essai du moteur unique » (deux semaines) :
  1. **E16** : mesurer ce que coûte une décision demandée au backend Java de la machine, face au moteur du runner, et
     essayer une source unique (le moteur Java compilé en JavaScript pour le runner). La Présidence tranche R90 sur la
     mesure.
  2. **La passerelle de modèles ouverte** (R92 élargie) : n'importe quel LLM ou modèle, en un seul endroit du backend.
     Un appel de modèle dure des secondes : l'aller-retour qui gêne R90 ne la concerne pas. L'ai-service Python et le
     relais de la coque cessent de servir.
  3. **Les suppressions demandées par Musk** : les préréglages jamais essayés quittent le catalogue visible, le plan figé
     d'« AI Workflows » disparaît.
  4. Ni identité locale, ni fermeture de la webapp (R91 modifiée).
- **J2 à J9** ne changent pas, avec deux précisions :
  - le parcours d'arrivée se vit comme un jeu, ce n'en est pas un (R102) ;
  - la démo montre trois natures de travail, sans prétendre servir tous les métiers (R103).

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 01/11/2026 à 10:31 UTC (`shuf`). Contradictrice désignée : Julie Zhuo.
- **La règle des 90 %** est une règle de la Présidence pour cette séance.
  - Pour l'appliquer, le secrétariat a fait voter chaque solution, puis retravailler celles qui échouaient : R94, R102, R103
    et R105 ont passé le seuil au second tour.
  - Sept solutions sont unanimes : R90, R92, R93, R96, R100, R104 et R106. La contradictrice les a toutes attaquées avant le
    vote (charte, §7.5). L'unanimité porte sur l'hygiène du code et sur des faits de souveraineté, pas sur la direction.
  - Si la Présidence veut garder la règle, elle s'inscrit au §6 de la charte (la convergence).
- **Hors fiche** : Bezos, sur le communiqué et la foire aux questions de la démo. C'est la méthode d'Amazon, pas une position
  de sa fiche ; même réserve qu'à la n°14.
- **Conflits d'intérêts** : Saarinen (Linear), Zhuo (Meta, par Sundial), Nadella (Microsoft).
- **Le dossier** :
  - les faits sur TaskForce viennent du code, lu le 01/11/2026, avec leurs chemins ;
  - les faits sur n8n, Temporal et Amazon viennent de leurs propres pages, lues ce jour ;
  - la page de n8n est une présentation commerciale : ses capacités sont à vérifier dans sa documentation avant toute
    comparaison publique.
- **La faille de la recherche** est décrite sans détail, les dépôts étant publics. Elle n'est pas encore corrigée sur `dev`.
  Les PV n°14 et n°15 ne se commitent qu'après sa correction.
- **Une erreur du dossier de la n°14** : il présentait le double moteur (Java et TypeScript) comme une force, deux mises en
  œuvre prouvées par les mêmes cas, sans en dire le coût. La Présidence l'a vu avant le Conseil.
- **Questions à la Présidence** :
  1. Confirmes-tu la lecture de tes décisions sur la n°14 (la table plus haut) ?
  2. R91 : l'app desktop sans compte obligatoire ? Cela revient sur ta décision du 19/10/2026.
  3. Quand les machines de l'école s'arrêtent-elles ? La date commande l'urgence de J1.
  4. À la fin de J1, fermer la webapp, avec préavis et export ?
  5. La règle des 90 % : pour cette séance seulement, ou dans la charte ?
  6. Lancer J0 ? La release de R78, après la correction d'« Apply », attendra ton « go release ».
- **Réponses de la Présidence (01/11/2026)** :
  - la lecture de la n°14 est confirmée ;
  - pas d'app desktop sans compte : elle continue de se connecter par la webapp (R91 modifiée) ;
  - la date d'arrêt des machines de l'école reste sans réponse (Q13) ;
  - la webapp ne ferme pas ;
  - la règle des 90 % entre à la charte ;
  - J0 est lancé ; la release de R78 attend toujours son « go release ».
- **Le risque reste écrit** : si les machines de l'école s'arrêtent avant le VPS, une nouvelle installation de l'app
  desktop ne peut plus se connecter (Q13).

## Suites

Rangées le 01/11/2026 :

- les PV n°14 et n°15 dans `seances/`, une ligne chacun au registre de la charte (§12), leur récit au Journal ; la règle
  des 90 % au §6 de la charte ;
- à `experiences/Experiences.md` : E16 (le moteur unique sans aller-retour) et E17 (l'indice de confiance, mesure de
  départ à J2) ; E7, E13 et E14 placées dans les jalons ;
- à `Questions-ouvertes.md` : Q13 complétée (la webapp reste, la date d'arrêt des machines de l'école manque), Q14
  (se brancher à n8n ?) et Q15 (le modèle de revenus) ;
- deux brouillons d'ADR, ratifiés, à promouvoir dans `v1/12-decisions/` :
  - ADR-022 : l'infrastructure, pas les règles (le métamodèle et les packs ; R94, R103), qui remplace les niches A et B ;
  - ADR-023 : l'exécution durable sur PostgreSQL, sur le modèle de Temporal (R97) ;
- R90 n'a pas d'ADR tant qu'E16 n'a pas tranché ;
- les jalons J0 à J9 dans `v1/13-roadmap/Roadmap_Backlog.md` (§0) et dans `.ai/roadmap.md` de `taskforce-fullstack`, en
  tâches ;
- les corrections de documents de R82 qui sont dans ce dépôt (l'architecture, le modèle de prix) ; celles du site et de
  la webapp vont en J0, côté code ; l'ADR-010 et l'ADR-021 attendent que l'index des ADR soit libre (des modifications
  d'une autre session y sont en cours).

## Avis du secrétariat

Après la clôture, l'avis du secrétariat. C'est le mien, pas celui du Conseil.

- **Oui, j'ai compris.** Tu ne veux pas un outil de délégation de code avec des règles autour. Tu veux l'infrastructure sur
  laquelle n'importe quelle entreprise fait travailler ses agents, sous ses règles, chez elle, en voyant tout et en pouvant
  tout prouver. Le code n'est qu'un métier parmi d'autres.
- `[DÉDUIT]` **Ce qui me paraît le plus juste** dans ta direction tient en deux phrases :
  - « l'infra, pas les règles » ;
  - « un outil bien fait, puis n'importe quel outil sans plus de code ».

  C'est la seule façon, pour une personne seule, d'être large. La largeur vient de briques génériques, pas de fonctions
  ajoutées une à une.
- `[DÉDUIT]` **Ce qui me paraît le plus risqué** :
  - sept mois avant la démo complète, sans revenu. J2 réduit ce risque, à condition de montrer la démo mince dès qu'elle
    tourne ;
  - « devant partout » face au marché n'est pas tenable sur le nombre d'intégrations ni sur la distribution. Face au texte, ça
    l'est, sur les 21 lignes ;
  - n8n occupe déjà l'image du « n8n IA ». La différence doit se dire en une phrase qui ne parle que de règles et de preuve.
- **Mon ordre pour lundi** :
  1. J0 : la faille, puis « Apply », puis les pages ;
  2. J1, en commençant par l'identité locale de l'app desktop. C'est la dépendance qui peut tout bloquer, si les machines de
     l'école s'arrêtent avant.
