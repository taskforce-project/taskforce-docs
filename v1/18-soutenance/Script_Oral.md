---
id: soutenance-script-oral
title: Script oral de la soutenance
doc_type: soutenance
statut: a-relire
version: 1.1
date: "21/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, rncp, oral, script, bc02, bc03]
---

# Script oral

> Étape 2 de la méthode. Structure validée le 21/07/2026, voir [[Plan_Minute]].
> Texte écrit pour être **dit**, pas lu. Les mots en gras sont ceux qui font cocher une ligne de la
> grille du jury : les prononcer distinctement.
> Calibré à 145 mots par minute, démonstrations comprises. Les indications entre crochets sont des
> consignes de jeu, elles ne se disent pas.

---

## Ouverture

### Diapositive 1, titre. 0:45

Bonjour. Je m'appelle Pierre Michel, je termine le Bachelor Développeur Full Stack à Metz Numeric
School.

En parallèle, je suis Head of Engineering chez Plania, une unité de TechGuys, où je pilote un
logiciel en ligne qui réalise 12 000 dollars de revenu mensuel récurrent. Avant cela, j'ai été lead
technique sur des comptes entreprise, et j'ai développé le cœur d'un logiciel de laboratoire
pharmaceutique soumis à la norme 21 CFR Part 11. J'ai commencé au LORIA, un laboratoire du CNRS. Je
suis aussi étudiant-entrepreneur.

Le projet que je vous présente s'appelle TaskForce. C'est un outil de gestion de projet, et il part
d'une question que les autres ne traitent pas.

[Marquer un temps.]

### Diapositive 2, le problème et les objectifs. 0:45

Cette question, la voici. Quand un chef de projet confie une tâche, il croise de tête trois choses :
qui sait faire, qui est disponible, et qui n'est pas déjà surchargé. Jira ou Linear enregistrent très
bien que la tâche a été confiée. Aucun ne l'aide à décider **à qui**.

Le résultat est connu : les mêmes personnes sont sollicitées, les surcharges se voient trop tard, et
les juniors ne progressent pas.

Le cahier des charges demandait donc une répartition dynamique des tâches selon les **compétences,
la charge de travail et les disponibilités**, avec suivi en temps réel et alertes de surcharge.
C'est ce que fait TaskForce, et son principe tient en une phrase : **l'outil propose, le manager
valide**.

### Diapositive 3, l'architecture d'ensemble. 0:55

Avant d'entrer dans les deux parties, voici la carte.

TaskForce a deux étages séparés par un contrat d'interface. Devant, une application Next.js.
Derrière, une interface REST en Spring Boot. Entre les deux, du JSON et un jeton signé.

L'identité est sortie de l'application : Keycloak authentifie, et mon back-end ne stocke aucun mot
de passe. Les données vivent dans PostgreSQL, avec pgvector pour la recherche sémantique. Un service
Python sert de passerelle vers un modèle de langage exécuté en local. Le tout tourne en conteneurs.

Suivons une requête. L'utilisateur clique. Le front appelle une route centralisée qui attache le
jeton. Le back vérifie la signature, vérifie que l'utilisateur appartient à cet espace de travail,
puis exécute.

Je justifie maintenant cette architecture des deux côtés, en commençant par le front.

---

## Partie 1, front-end, bloc BC02

### Diapositive 4, séparateur. 0:10

Première partie, le front-end. La technologie, la conception, la charte, la sécurité, la
démonstration, l'accessibilité, le référencement et les tests.

### Diapositive 5, la technologie front. 0:50

Le front est une application Next.js 16 avec l'App Router, React 19, et **TypeScript en mode
strict**. Pourquoi ce choix plutôt que du React seul.

Trois raisons. Le rendu hybride : les pages sont rendues côté serveur, les interactions restent côté
client, donc un premier affichage rapide sans perdre l'interactivité. TypeScript strict ensuite : le
contrat de l'API est typé de bout en bout, une erreur de champ se voit à la compilation, pas en
production. Enfin la sortie autonome, qui me donne une image Docker minimale.

Le code est organisé par domaine, sur 47 routes.

Sur la validité du code, deux outils tournent : une **analyse statique** avec ESLint, et une
vérification de types qui **bloque l'intégration continue**. L'application est **compatible Chrome,
Firefox et Safari**, comme le demandait le cahier des charges.

### Diapositive 6, de la conception aux écrans. 0:45

Sur la conception, je vais être précis, parce que c'est un point où je peux être pris en défaut.

J'ai travaillé à partir de **wireframes annotés** qui décrivent chaque écran, sa structure et ses
états. En revanche, une partie de cette documentation a été consolidée **pendant** le développement,
pas entièrement avant. Je préfère vous le dire plutôt que de laisser croire à un cycle en cascade
que je n'ai pas suivi.

Ce que je démontre, en revanche, c'est la couverture : **les douze cas d'utilisation du dossier de
conception sont tous implémentés**, de l'authentification par code jusqu'à la facturation.

Voici le wireframe, et à côté, l'écran livré.

### Diapositive 7, la charte du client. 0:40

Le cahier des charges décrit une charte en trois exigences : un **design épuré et moderne**, un
**design responsive**, et une expérience fluide avec **réduction des clics superflus**.

Je les ai traduites en système de design. Épuré, cela veut dire une palette tenue : **165 variables
CSS** définissent toutes les couleurs, rayons, espacements et ombres, en thème clair et sombre.
Aucune couleur ne se décide dans un composant.

Réduction des clics, cela se joue dans les composants : **189 composants**, dont **77 primitives**
construites sur Radix, qui donnent des raccourcis clavier et des dialogues cohérents partout. Le
responsive, je vous le montre dans un instant.

### Diapositive 8, sécurité, écoconception et chaîne de build. 0:55

Un front n'est pas seulement une interface, c'est une surface d'attaque.

Quatre mesures. La communication est chiffrée par **TLS**. Les **en-têtes HTTP de sécurité** sont
posés dans la configuration Next : **politique de sécurité du contenu**, HSTS, interdiction
d'affichage en iframe, interdiction du reniflage de type. Le **CORS** est restreint aux origines
déclarées. Et les **dépendances sont verrouillées et auditées**.

Sur l'**écoconception** et la performance, c'est le rôle de la chaîne de build. Tailwind 4 ne génère
que les classes réellement utilisées dans mon code, et la compilation de production minifie le CSS
et le JavaScript. Voici la taille du CSS réellement livré.

[Montrer le chiffre. Dire « la chaîne de build produit ce résultat », jamais « j'ai optimisé ».]

### Diapositive 9, démonstration côté utilisateur. 1:55

[Basculer sur l'application. Jeu de données chargé, session déjà ouverte.]

Je passe sur l'application. Vous voyez un espace de travail réel, neuf membres, environ deux cent
cinquante tâches.

[Tableau de bord.]

Le tableau de bord. La charge de chaque membre est visible immédiatement, et les alertes de
surcharge remontent ici.

[Ouvrir un projet en vue Kanban, déplacer une tâche.]

Un projet en vue Kanban. Je déplace une tâche, l'état est enregistré immédiatement.

[Ouvrir une issue.]

J'ouvre une tâche : description en éditeur riche, libellés, estimation, commentaires et historique.

[Basculer le thème.]

Le thème sombre et le thème clair partagent les mêmes variables, donc aucun écran n'est oublié.

[Réduire la fenêtre au format mobile.]

Le même écran en format mobile. La navigation se replie, les colonnes s'empilent, aucune fonction
n'est perdue.

[Naviguer au clavier, touche Tab.]

Et je navigue uniquement au clavier : le focus est visible en permanence, chaque élément interactif
est atteignable.

[Revenir aux diapositives.]

### Diapositive 10, consommer l'API de façon sécurisée. 0:45

Le front ne parle jamais à la base. Il consomme une **interface REST en JSON**, format choisi parce
qu'il est lisible, universel, et qu'il permettra à d'autres outils de consommer mes données, ce que
le cahier des charges demandait.

Tous les appels passent par **un client HTTP unique**. Il attache le jeton d'accès à chaque requête,
et quand le jeton expire, il **le renouvelle automatiquement et rejoue la requête**, de façon
transparente.

L'**authentification est déléguée à Keycloak**, avec des jetons signés par clé asymétrique : mon
application ne peut pas forger un jeton, seulement vérifier une signature. Et l'API est **documentée
et publiée** en OpenAPI.

### Diapositive 11, l'accessibilité. 0:45

L'accessibilité vient de la base technique. Les composants Radix implémentent nativement les **rôles
ARIA**, le piégeage du focus dans les fenêtres modales et la **navigation clavier**.

Par-dessus, j'ai ajouté des libellés explicites sur les boutons à icône seule, un anneau de focus
visible et unique, et des **contrastes conformes au niveau AA du référentiel WCAG 2.1**.

Et c'est **vérifié automatiquement** : axe-core s'exécute dans mes tests de bout en bout, sur les
parcours d'authentification, de tableau de bord et de gestion des membres.

Une limite, que j'assume : mon test bloque sur les violations critiques et journalise les sérieuses.
Le durcir est ma prochaine étape.

### Diapositive 12, référencement et mesure d'audience. 0:45

Le référencement ne concerne pas l'application, qui est derrière une authentification, mais le site
public qui la vend. Il est construit avec Astro, en pages statiques : du HTML servi tel quel, la
meilleure base pour l'indexation.

Sur les **balises**, chaque page porte un titre unique, une description, une balise canonique et les
balises Open Graph.

Sur la **mesure d'audience**, j'ai choisi une solution respectueuse de la vie privée plutôt que
Google Analytics. Elle mesure les visites et les conversions **sans cookie de suivi**, donc sans
bandeau de consentement, ce qui est cohérent avec la conformité RGPD exigée par le cahier des
charges. Voici le tableau de bord et le rapport technique.

### Diapositive 13, tester et industrialiser le front. 1:00

Mon **plan de test** a trois niveaux.

Premier niveau, **805 tests unitaires** avec Vitest, sur la logique : services d'appel à l'API,
magasins d'état, crochets React et composants d'authentification. La **couverture y est de 89,55 %**,
pour un seuil demandé de 50 %. Je précise le périmètre : ces 88 % portent sur la logique, pas sur
chaque pixel.

Deuxième niveau, les pages et les composants d'interface sont couverts par des **tests de bout en
bout Playwright**, qui pilotent un vrai navigateur.

Troisième niveau, un **cahier de recette de 79 scénarios dérivés des spécifications**, dont 77
automatisés.

Sur l'industrialisation, tout s'exécute en **intégration continue** à chaque envoi de code : analyse
statique, vérification de types, tests, couverture, compilation. La **gestion des dépendances** est
automatisée, avec mises à jour proposées et audit de vulnérabilités.

---

## Partie 2, back-end, bloc BC03

### Diapositive 14, séparateur. 0:10

Deuxième partie, le back-end. L'architecture, la persistance, le modèle de données, le moteur
d'assignation, l'API, la monétisation et les tests.

### Diapositive 15, l'architecture back. 0:55

Le back-end est en **Java 21 et Spring Boot**.

Le cahier des charges suggérait PHP ou Node. J'ai retenu Java, et je l'assume comme un **choix
technique adapté**. Trois raisons. Le typage fort : sur 49 entités liées, une erreur de contrat est
détectée avant l'exécution. L'écosystème Spring, qui me donne sécurité, persistance, validation et
supervision dans un cadre éprouvé en entreprise. Et mon expérience professionnelle en environnement
réglementé, sur cette même pile.

L'**organisation du code** suit trois couches, avec une règle stricte : le partagé, le noyau, puis
les modules métier, jamais l'inverse.

Un point dont je suis satisfait : **Keycloak répond à « qui es-tu », ma base répond à « qu'as-tu le
droit de faire »**. Aucun rôle n'est lu dans le jeton. Je peux changer d'annuaire d'identité sans
toucher à mes autorisations.

### Diapositive 16, persistance et sécurité en profondeur. 0:55

La couche de persistance applique une **sécurité en profondeur**, à cinq niveaux.

Le **contrôle d'accès** : un intercepteur vérifie à chaque requête que l'utilisateur est membre de
l'espace de travail, puis chaque service revérifie le rôle. C'est ma parade contre l'accès à une
ressource d'autrui, centralisée en un seul endroit.

Le **filtrage des données entrantes** : environ 180 règles de validation avant d'atteindre la
logique métier. En sortie, aucune entité n'est renvoyée telle quelle.

L'**authentification forte** : jetons signés par clé asymétrique, validation de l'émetteur, sessions
sans état, protection contre la force brute.

La **journalisation** : une table d'audit trace les actions sensibles, et elle survit à l'effacement
du compte.

La **supervision** : les traces partent en OpenTelemetry vers SigNoz, avec des alertes dont deux
orientées sécurité. Et un **cache Redis** porte la limitation de débit, distribuée entre instances.

### Diapositive 17, le modèle de données du smart-assign. 0:45

Le modèle complet compte 49 entités et 68 migrations versionnées. Je ne vais pas le dérouler, je
vous montre les sept tables qui rendent la fonctionnalité principale possible.

Au centre, la tâche, avec son estimation et ses libellés. À gauche, le membre et son profil de
compétences : compétences déclarées, capacité en heures par semaine, séniorité. À droite,
l'historique des décisions d'affectation : chaque recommandation passée, acceptée ou refusée,
réussie ou non.

Ce sont ces trois signaux, compétences, charge calculée sur les tâches ouvertes, et historique, qui
alimentent le moteur. Et toutes les migrations sont rejouées à l'identique dans les tests.

### Diapositive 18, démonstration du smart-assign. 2:00

[Basculer sur l'application, projet API.]

Voici le cœur du produit. Je prends une tâche non assignée : « limitation de débit sur
l'authentification ». Priorité haute, cinq points, libellés côté back.

[Cliquer sur Smart Assign.]

Je demande une recommandation.

[Résultat.]

L'outil propose Marcus Webb, et surtout il explique pourquoi, en français. Je déplie le détail.

[Ouvrir les sous-scores.]

Vous voyez chaque facteur séparément : la correspondance sémantique entre la tâche et son profil, sa
charge mesurée sur tous ses projets, son historique de résolution, sa disponibilité selon la
capacité qu'il a déclarée, et les libellés qui correspondent à ses compétences. Ce n'est pas une
boîte noire, c'est une décision auditable.

[Prendre WEB-4 sur le projet WEB.]

Je change de cas : un correctif d'interface, sur un projet où j'ai activé le mode montée en
compétence.

[Smart Assign.]

Cette fois, l'outil remonte Diego, qui est junior, avec une mention de tâche formatrice. Le moteur a
vu que la tâche est légèrement au-dessus de son niveau habituel, qu'elle n'est pas urgente, et qu'il
a de la disponibilité. C'est l'arbitrage qu'un chef de projet fait rarement, faute de temps.

[Valider l'assignation.]

Je valide, et la décision est enregistrée pour affiner les suivantes.

[Revenir aux diapositives.]

### Diapositive 19, l'API sécurisée au filtre de l'OWASP. 0:55

L'API compte 35 contrôleurs et plus de 200 points d'entrée, documentés en OpenAPI.

Je l'ai relue au filtre du **Top 10 de l'OWASP**. Sur les dix catégories, huit ont une parade que je
peux vous montrer dans le code.

Le **contrôle d'accès** est traité par le point de contrôle unique. Les **injections** sont écartées
par des requêtes paramétrées, sans concaténation de SQL. Les **entrées sont toutes validées et
filtrées**. Et les **données sensibles sont chiffrées au repos**, en AES-256-GCM.

Deux catégories ne sont pas couvertes, et je préfère vous les donner que d'attendre la question. La
falsification de requête côté serveur : mes webhooks sortants appellent une adresse saisie par
l'utilisateur, sans liste blanche. Et l'analyse de dépendances, que je lance à la main avec Trivy,
Semgrep et OWASP ZAP. Les deux sont dans ma feuille de route.

### Diapositive 20, de l'IA locale à la monétisation. 0:55

Le moteur d'assignation appelle un modèle de langage, et ce modèle **tourne en local**, un Qwen
exécuté par Ollama.

Trois conséquences. Les données de mes clients ne sortent pas de l'infrastructure. Le coût par
requête est nul. Et c'est une démarche d'**écoconception** : un petit modèle pour les tâches
rapides, un plus grand seulement si nécessaire.

Ce coût marginal nul rend le modèle économique tenable. La **monétisation** passe par Stripe, en
paiement par siège, avec quatre offres : gratuite, 10 euros, 16 euros, et sur devis. La **cible**,
c'est l'équipe technique de 5 à 50 personnes, celle qui a déjà un outil de suivi mais aucune aide à
la décision.

Sur la **sécurité du paiement**, je ne vois jamais un numéro de carte : Stripe héberge le
formulaire. Les cinq notifications de Stripe sont **signées, vérifiées et traitées de façon
idempotente**.

Et l'IA est disponible dès l'offre gratuite, avec un quota mensuel. Je vends l'usage, pas l'accès.

### Diapositive 21, tester et industrialiser le back. 1:00

Le **plan de test** du back est **dérivé des spécifications**, en trois niveaux.

Les **tests unitaires** isolent la logique métier, en particulier le moteur d'assignation :
classement, exclusion des membres inactifs, calcul de charge, comportement de repli quand le modèle
ne répond pas.

Les **tests d'intégration** tournent sur un **vrai PostgreSQL avec pgvector**, avec les vraies
migrations rejouées et la validation stricte du schéma, exactement comme en production. Ce n'est pas
une base simulée.

Les tests de tranche web valident les contrôleurs avec la sécurité réelle : les refus sont testés,
pas supposés.

Au total, **792 cas de test s'exécutent sans échec**, pour une **couverture de 73,71 % des lignes**.
Le seuil demandé est de 50 %.

Tout cela tourne en **intégration continue** à chaque envoi de code. Les **dépendances** sont gérées
par Maven en versions verrouillées, et la chaîne produit une image Docker publiée et versionnée,
**prête pour le déploiement**.

---

## Conclusion

### Diapositive 22, bilan et distance critique. 0:45

Ce que je retire de ce projet, ce sont trois arbitrages.

Le premier, je l'ai corrigé. Au départ j'émettais moi-même mes jetons, avec une clé symétrique. Ma
veille m'a montré que je portais un risque inutile. J'ai tout basculé sur Keycloak, en signature
asymétrique, et cette décision vient d'une remise en cause.

Le deuxième, je l'assume : mes jetons sont stockés dans le navigateur, et non dans un cookie
inaccessible au JavaScript. C'est un compromis connu, il est dans ma feuille de route.

Le troisième, je le reconnais : il n'y a pas encore de production active. L'infrastructure est
prête, la décision d'hébergement n'est pas prise.

Et deux chantiers restent ouverts : passer l'analyse de sécurité en intégration continue, et écrire
la protection contre la falsification de requête.

### Diapositive 23, les améliorations possibles. 0:20

La suite est déjà amorcée. Le moteur qui recommande une personne peut recommander un découpage, une
estimation, une priorisation. L'objectif est que TaskForce assiste toute la chaîne, de l'idée à la
livraison, chaque étape restant validée par un humain.

### Diapositive 24, remerciements. 0:15

Merci de votre attention. Ce projet m'a fait progresser sur la sécurité déléguée, sur
l'intelligence artificielle exécutée en local, et sur la discipline des tests. Je suis à votre
disposition pour vos questions.

---

## Notes de jeu

**Rythme.** Le script est calibré à 145 mots par minute. Si vous êtes en avance à la diapositive 13,
c'est que vous avez accéléré : ralentissez sur le back, qui porte les chiffres.

**Les deux moments à ne pas précipiter.** La diapositive 18, quand vous dépliez les sous-scores, et
la diapositive 22, quand vous nommez vos limites. Ce sont les deux endroits où le jury décide s'il
vous croit.

**Les phrases exactes au mot près**, à ne jamais improviser : « 89,55 % de couverture sur la
logique », « 792 cas de test sans échec », « 73,71 % des lignes côté back », « huit catégories sur
dix », « le seuil demandé est de 50 % ».

> Chiffres actualisés le 23/07/2026. Ils avaient déjà changé trois fois depuis la première
> rédaction : les revérifier une dernière fois la veille de l'oral, et ne jamais citer de mémoire.

**Si la démonstration échoue.** Basculer sur la vidéo de secours en annonçant simplement : « je
passe sur l'enregistrement que j'ai préparé ». Ne pas déboguer devant le jury, cela coûte deux
minutes et la maîtrise du rythme.

> Voir aussi : [[Plan_Minute]] pour la structure et les correctifs produit, et [[Plan_Soutenance]]
> pour l'historique.
