---
id: conseil-seance-2026-11-05-atelier-fenetre
title: "Séance n°18 du 05/11/2026 : l'atelier de la fenêtre (la conversation au centre, les écrans en volets)"
doc_type: pv-seance
statut: active
date: "05/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, fenetre, conversation, volets, cortex, progression, installateur]
related:
  - "../README.md"
  - "./2026-10-28-atelier-design.md"
  - "./2026-10-30-atelier-ecrans-base.md"
  - "./2026-11-01-feuille-de-route.md"
  - "./2026-11-02-cortex-voit-demande-dit-vrai.md"
  - "../../decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
  - "../../../v1/14-design/Revue_UX_2026-11-01.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°18 du 05/11/2026 : l'atelier de la fenêtre

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle, et les décisions de Jobs sont celles d'un personnage simulé.

## Résumé

La Présidence veut une app « same as Claude Code » : la conversation au centre, les écrans qu'on regarde à côté, et la
conversation à portée sur chaque écran. Pas de maquette : Jobs tranche tout, la Présidence valide d'avance.

L'atelier adopte une fenêtre en trois zones. À gauche, le travail et ses conversations, rangés par projet. Au centre, la
conversation avec Cortex, le compositeur en bas. À droite, ce qui entoure la conversation : l'environnement, le contexte,
les connecteurs, les résultats, les modifications, les missions. Le tableau, l'issue, la vue du travail et les autres
écrans s'ouvrent en volet à côté de la conversation, entiers, avec tous leurs gestes. En pleine largeur, la conversation
se replie dans le compositeur. On prend la structure de Claude Code, jamais l'identité d'Anthropic.

Kenza Ait Si Abbou, contradictrice, obtient deux conditions : la conversation n'est jamais le seul chemin, et chaque
réponse dit quel modèle l'a écrite et ce qu'il a lu. Norman obtient que ce qui quitte l'écran reste à deux clics, et que
l'annulation ne parte jamais. Un volet « Progress » répond au tableau d'entraînement de la Présidence : ce que l'agent
sait, et comment il progresse, mesuré ici. L'installateur prend l'allure de la page de connexion.

Huit recommandations, R119 à R126, à l'unanimité des cinq, validées d'avance par la Présidence.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 05/11/2026), après son test de la 1.10.0 sur l'app desktop 1.7.0 :
  - « le chat c'est ok mais je me demande si on pourrait vraiment pas faire un truc similaire a Claude, genre full chat
    avec un endroit ou justement on peut voir les interfaces tu vois ? Comme si on avait finalement integre un board dans
    CLaude Desktop tu vois ? Gros changement mais je pense que ce serait mieux nan ? Et evidemment pouvoir tout de mm call
    le chat quand on est sur les board et pas avoir a reswitch » ;
  - « pour l instant y a rien dans la table, pas d ebenchmark de base dispo dans la description des models ? Et apres
    update sur un board plus complexe cote entrainement, ce que l'agent sait et tout quoi bref pour voir comment il
    devient de mieux en mieux dans le domaine » ;
  - puis, sur la proposition du secrétariat (des maquettes, puis un atelier) : « lance pas de maquette c'est vraiment
    same as Claude Code quoi genre le screen mdrr, t'as tout ce qu'il faut la pour que notre Steve Jobs et l'equipe UI/UX
    pousse l'interface au maximum, Appel vibe donc pas de superflux, il prend toute les decision possible, je valide tout
    directement ». « Appel vibe » se lit « Apple vibe ».
- **Horizon** : J1, avant sa revue ; la boucle de démo de J2 se jouera dans cette fenêtre.
- **Formation** : restreinte (5), l'équipe de Jobs, comme aux ateliers du 28/10 (n°6) et du 30/10 (n°13).
  - Impulsion : Steve Jobs, qui tranche par délégation.
  - Pont : Kenza Ait Si Abbou (l'adoption par quelqu'un qui ne code pas).
  - Design : Karri Saarinen, Don Norman, Julie Zhuo.
- **Ordre de parole**, tiré au sort à 11:37 UTC : Steve Jobs, Kenza Ait Si Abbou, Karri Saarinen, Don Norman, Julie Zhuo.
- **Contradictrice** : Kenza Ait Si Abbou, seule présente qui ne l'a jamais été.
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à cinq.
- **Fiches** : à jour (moins de 30 jours) : Norman, Saarinen et Zhuo au 28/10/2026, Ait Si Abbou au 26/10 ; Jobs, siège
  historique, sans nouvelle source. Aucune fiche rafraîchie.

## Dossier

### 1. La capture de la Présidence `[ÉTABLI]`

La capture du 05/11/2026 montre la fenêtre de l'app desktop de Claude Code, en trois zones. Le PV n'en décrit que la
structure : les noms de sessions qu'elle montre sont privés.

| Zone | Ce qu'elle contient |
| --- | --- |
| À gauche | « Créer », « Rechercher », les artéfacts, les tâches planifiées, la personnalisation, « Plus » ; puis les sessions rangées par projet, chacune avec sa branche ou sa pull request ; la personne et les réglages en bas |
| Au centre | La conversation ; en bas, le compositeur : « + » pour joindre, le texte, l'envoi, le micro ; dessous, le modèle et l'indicateur de contexte |
| À droite | Six lignes repliables, chacune avec son nombre : l'environnement (cet ordinateur, le dossier, le dépôt, la branche), le contexte (95 %), les connecteurs (3 à reconnecter), les résultats (8), les modifications (3 pull requests), les tâches en arrière-plan (leur durée, un bouton d'arrêt ; 40 terminées) |
| En haut à droite | Des boutons qui ouvrent des volets à côté de la conversation : le terminal, le navigateur, les fichiers |

### 2. Ce que TaskForce montre aujourd'hui `[ÉTABLI]`

Lu dans le code de `dev` le 05/11/2026 (`frontend/components/layout/`).

| Zone | Aujourd'hui |
| --- | --- |
| À gauche | Une barre de navigation : Dashboard, Inbox (trois sous-pages), My work (trois), Projects, Analytics, Members ; Settings et Help en bas. Les conversations de Cortex n'y sont pas : elles se retrouvent depuis la conversation elle-même |
| En haut | Une barre : le fil d'Ariane, la recherche (Ctrl+K), la cloche des notifications, le thème, le bouton d'AI Workflows |
| Au centre | Une page par écran, qui change avec l'adresse |
| En bas | La barre unique (R76) ; la conversation se déplie au-dessus, sur un dégradé, jamais sur le côté (décision du 02/11) |
| Sur les côtés | Les panneaux d'AI Workflows, qui glissent par-dessus la page |
| Par-dessus | La fiche d'issue, qui recouvre la barre (constat 5 de la revue UX ; correction en cours) |

Sur l'app desktop, le contenu est déjà une carte arrondie dans le cadre de la barre de gauche, « façon Claude Desktop »
(commentaire du code).

### 3. Ce que le test de la 1.10.0 a montré sur l'interface `[ÉTABLI]`

- La barre hors d'atteinte quand une issue est ouverte : « j ai pas acces au chat quand je suis en train de spectate une
  issue ».
- L'installateur : « ca c'est naze comme interface jsp si on peut faire comme la page de login par exemple, mm l
  installateur hein, la c est une fenetre system windows c'est naze ».
- L'indicateur de contexte, « 45k / 33k (100%) » en rouge, qui ne dit rien d'utile : « le context jsp c'est bizarre ca
  fait rien ».
- La table des capacités, vide tant qu'on n'a pas cliqué « Measure ».
- La carte de suppression qui nomme TESTTA-1, dans Done, quand la demande visait l'issue de « In review by AI », TESTTA-2,
  de même titre.
- La création d'un projet qui reposait les mêmes questions.
- À « prend OPS-35 et propose moi un resume dans les commentaire stp », Cortex n'a appelé que `add_comment`, sans lire
  l'issue, et a écrit le résumé d'une itération qu'il n'avait pas lue, en Markdown brut. Le pied de la réponse dit
  « deep » et le nombre de tokens, pas le modèle : « Jsp avec quel model il a fait ca par contre, dans le tableau c'est le
  qwen3:8b ».

Chacun de ces points a une correction en cours, sur deux branches (`fix/replay-1100`, `fix/desktop-sheet-bar-updates`) :
pour OPS-35, TaskForce lit l'issue avant tout résumé, le nom du modèle s'affiche sous chaque réponse, et les commentaires
sont rendus. Cette séance dessine ce qui reste : la fenêtre.

### 4. Les décisions en vigueur

- **R76** (n°13) : une seule entrée, sur chaque écran ; la voix d'un clic ; rien ne part sans envoi.
- **Le débat de la n°13**, « Tout par la barre, ou un établi ? » : Saarinen gardait sa réserve, la barre ne doit pas
  remplacer un écran.
- **R57** (atelier du 29/10) : l'invisible se voit en une ligne, sur son objet ; aucun écran ne surveille les agents.
- **R95** (n°15) : une surface par partie, l'assistant partout ; il ne remplace aucun écran ; la vue du travail, « comme
  quand on regarde Claude Code coder ». Jobs s'était abstenu : sept surfaces, ce sont sept produits.
- **ADR-024** (brouillon, 02/11) : la conversation pilote tout, par le MCP de TaskForce, le même pour l'agent interne et
  pour les agents externes.
- **R113** (n°16) : ce qu'un modèle sait faire se mesure ici, jamais d'après les chiffres de son éditeur.
- **R114 et R116** (n°17) : Cortex voit l'écran ; TaskForce dit ce qui a été fait.
- **La revue UX du 01/11** (R112) : vingt constats ; ceux qui attendent touchent la fiche d'issue (10, 17), les en-têtes
  (18), les mots (19) et l'arrivée (20).

## Tour de table `[HYPOTHÈSE]`

- **Steve Jobs** (Impulsion) : la Présidence a vu le produit qu'elle veut, il est sur son écran tous les jours. On ne
  dessine pas la maquette de ce qui existe : on le fait. Trois zones, une conversation, le travail à côté. « Apple » n'est
  pas un style, c'est ce qu'on retire : chaque élément à l'écran doit gagner sa place. Il retire la barre du haut, la
  cloche, le tableau de bord comme accueil, les sous-menus, le tour guidé, les panneaux qui glissent. On prend la
  structure, pas la peau : la police, les couleurs et la marque restent celles de TaskForce. *Sa recommandation : la
  fenêtre de Claude Code, avec la grammaire de TaskForce, d'un seul tenant.*
- **Kenza Ait Si Abbou** (Pont, contradictrice) : elle attaque l'idée que le chat simplifie. Pour quelqu'un qui ne code
  pas, une conversation vide est l'écran le plus difficile : il faut savoir quoi demander. La fenêtre de Claude Code est
  faite pour des développeurs qui connaissent leurs outils. Et OPS-35 montre le risque : quand la conversation est l'écran
  principal, chaque invention est au premier rang, et la personne qui valide ne distingue pas un résumé d'une invention.
  Elle demande : rien qui ne passe que par la conversation ; sous chaque réponse, le modèle et ce qu'il a lu ; une
  conversation qui s'ouvre sur ce qui attend la personne ; des mots simples. *Sa recommandation : la conversation au
  centre, jamais seule, et qui montre ce qu'elle a lu.*
- **Karri Saarinen** (Design) : à la n°13, il voulait un établi, pas un chat. Cette fenêtre en est un : chez Claude Code,
  la conversation est à côté du terminal, du navigateur et des fichiers ; les volets sont l'établi. Ses conditions : le
  tableau dans un volet est le vrai tableau, pas un aperçu ; le volet peut prendre toute la fenêtre ; l'adresse d'une
  issue ouvre l'issue ; un volet s'ouvre aussi vite qu'un écran d'aujourd'hui. À gauche, le travail d'abord : les projets,
  et sous chacun ses conversations et ses missions, pas une liste de discussions sans objet. *Sa recommandation : des
  volets qui sont les vrais écrans, à la vitesse d'un outil.*
- **Don Norman** (Design) : « Apple vibe » est le risque qu'il nomme, une interface épurée qui cache les fonctions ou
  supprime l'annulation. Dans une conversation, comment découvre-t-on ce qu'on peut demander ? Il veut des signes : des
  suggestions, la liste de `/` dès le premier caractère. La carte de suppression qui nommait TESTTA-1 est une méprise que
  l'écran a permise : la carte doit montrer où est l'issue, et l'issue s'ouvrir à côté. Chaque geste de la conversation
  laisse une trace qu'on peut défaire. *Sa recommandation : ce qui quitte l'écran reste à deux clics, et chaque geste se
  défait depuis la fenêtre.*
- **Julie Zhuo** (Design) : comment saura-t-on que c'est mieux ? Trois mesures, avant et après : la boucle de démo jouée
  sans changer d'écran ; les clics entre l'ouverture de l'app et la première action utile ; les éléments de l'écran
  d'arrivée. La boîte de saisie vide la fait bondir : l'arrivée dit ce qui attend. Sur l'entraînement, elle rejoint la
  Présidence : on fait confiance à ce qu'on voit progresser, un volet qui montre ce que l'agent sait, ce qu'il a raté et
  ce qui a été corrigé, mesuré et daté. *Sa recommandation : une arrivée jamais vide, un volet de progression, une mesure
  avant et après.*

## Confrontation `[HYPOTHÈSE]`

1. **La conversation au centre, ou l'établi ?** Saarinen et Jobs s'accordent vite : la conversation et les volets
   partagent la fenêtre, aucun ne cache l'autre. Kenza Ait Si Abbou attaque ce consensus : la fenêtre d'un outil de
   développeur, offerte à tous. Jobs répond que dire ce qu'on veut avec ses mots est le chemin le plus court pour
   quelqu'un qui ne code pas, à condition que la conversation ne soit jamais vide ni le seul chemin. Elle accepte avec ces
   deux conditions écrites (R120, R123).
2. **Retirer sans cacher.** Jobs veut retirer la barre du haut, la cloche, les sous-menus et le tableau de bord comme
   accueil. Norman l'arrête sur deux points : ce qui quitte le premier regard reste dans le produit, à deux clics ou par
   la recherche ; l'annulation ne quitte jamais l'écran. Jobs accepte : c'est la ligne « Changes », à droite, avec
   « Undo » (R122, R124).
3. **Une page et un volet ?** Zhuo craint deux endroits pour la même chose. Jobs tranche : il n'y a plus de pages,
   seulement des volets, et chaque état de la fenêtre a son adresse. Saarinen obtient la pleine largeur ; la conversation
   se replie alors dans le compositeur, et la réponse se déplie au-dessus, comme décidé le 02/11 (R120).
4. **Le tableau d'entraînement.** Jobs s'était abstenu sur les sept surfaces de R95. Il accepte un seul volet,
   « Progress », pas une surface par brique. Kenza Ait Si Abbou veut qu'il se lise sans être ingénieure ; Norman, qu'il ne
   devienne pas un écran de surveillance (R57) : il montre ce que l'agent sait et ce qui s'améliore, jamais son activité
   (R125). Sur « pas de benchmark de base », le tour garde R113 : rien d'un éditeur ne s'affiche comme une mesure ; ce que
   dit la fiche du modèle (taille, fenêtre, outils) s'affiche comme tel, en attendant la mesure.
5. **Le modèle sous chaque réponse.** Jobs le voulait au survol, pour ne rien ajouter. Norman et Kenza Ait Si Abbou le
   veulent visible : la Présidence a demandé quel modèle avait écrit le résumé d'OPS-35. Jobs cède : une ligne grise,
   sous chaque réponse et dans chaque commentaire de Cortex (R123).
6. **My work au premier niveau ?** Saarinen le voudrait à gauche, en haut ; Jobs le range sous « More », puisque
   « Waiting for you » dit déjà ce qui attend la personne. Saarinen vote avec une réserve, écrite comme signal d'arrêt
   (R121).

## Recommandations `[HYPOTHÈSE]`

### R119. La fenêtre de Claude Code, la grammaire de TaskForce

- **Quoi** :
  - trois zones : à gauche, le travail et ses conversations ; au centre, la conversation avec Cortex, le compositeur en
    bas ; à droite, ce qui entoure la conversation ;
  - les écrans s'ouvrent en volet, entre la conversation et la zone de droite (R120) ;
  - la même fenêtre sur l'app desktop et sur la webapp, testée sur l'app desktop d'abord (R91) ;
  - la structure vient de Claude Code ; l'identité reste celle de TaskForce, sa police, ses couleurs, sa marque. Rien de
    l'identité d'Anthropic, ni logo ni couleur.
- **Pour** : les cinq.
- **Contre** : aucun.
- **Preuve en dix jours** : la Présidence joue la boucle de démo de J2 dans la nouvelle fenêtre, sans changer d'écran.
- **Signal d'arrêt** : la Présidence cherche un écran qu'elle ne trouve plus.

### R120. Les écrans deviennent des volets, la conversation reste à portée

- **Quoi** :
  - le tableau d'un projet, l'issue, la vue du travail d'une mission (R95, point 3), My work, le tableau de bord, la
    feuille de route, les cycles, les membres et l'analytique s'ouvrent en volet ;
  - le volet est l'écran entier, avec tous ses gestes : rien ne passe que par la conversation (R95, point 2 ; la réserve
    de Saarinen à la n°13) ;
  - un volet s'ouvre depuis le nom d'un projet, à gauche ; depuis un lien dans une réponse ; depuis les boutons du haut ;
    depuis la recherche ;
  - il se redimensionne à la poignée, passe en pleine largeur, se ferme ; l'issue s'ouvre par-dessus le tableau, dans le
    même volet, avec un retour ;
  - en pleine largeur, la conversation se replie dans le compositeur, en bas au centre : on écrit, et la réponse se déplie
    au-dessus (le motif du 02/11) ; Échap la replie ;
  - chaque état de la fenêtre a son adresse : un lien vers une issue ouvre la fenêtre sur cette issue, et le bouton
    retour marche ;
  - la fiche d'issue par-dessus la page disparaît : le constat 5 de la revue est réglé par construction.
- **Pour** : les cinq. Saarinen : un volet s'ouvre aussi vite qu'un écran d'aujourd'hui.
- **Contre** : aucun.
- **Preuve en dix jours** : ouvrir OPS-35 depuis une réponse, changer sa priorité dans le volet, puis demander « résume-la »
  sans fermer le volet.
- **Signal d'arrêt** : la personne ferme la conversation pour travailler sur le tableau.

### R121. À gauche, le travail et ses conversations

- **Quoi** :
  - en haut : « New conversation » ; « Search » (Ctrl+K : conversations, issues, projets, personnes, gestes) ; « Waiting
    for you », avec son nombre : les demandes d'accord, les résultats à juger, les mentions. Il remplace l'Inbox et la
    cloche ;
  - puis chaque projet : son nom ouvre son tableau en volet ; dessous, ses conversations et ses missions en cours, chacune
    avec son état en un point (au travail, en attente de vous, en échec, terminé : les quatre états de R57) ;
  - puis les conversations hors projet ;
  - en bas, la personne : l'espace, les réglages, l'aide, la version, la déconnexion ;
  - sous « More » : My work, le tableau de bord, la feuille de route, les cycles, les membres, l'analytique. Retirés du
    premier regard, pas du produit.
- **Pour** : les cinq. Saarinen, avec une réserve : My work au premier niveau.
- **Contre** : aucun.
- **Preuve en dix jours** : la Présidence trouve chaque écran d'aujourd'hui en deux clics, ou par la recherche.
- **Signal d'arrêt** : la Présidence ouvre « More » pour My work plus d'une fois par jour ; My work remonte alors au
  premier niveau.

### R122. À droite, ce qui entoure la conversation

- **Quoi** : six lignes, repliées par défaut, chacune avec son nombre.
  1. **Environment** : l'espace, le projet, le dépôt, et où tourne le modèle (cet ordinateur, ou TaskForce).
  2. **Context** : ce que Cortex voit (le volet ouvert, R114) et la place prise dans la fenêtre du modèle, en une phrase.
  3. **Connectors** : connectés, à reconnecter ; un clic mène aux réglages.
  4. **Results** : les résultats qui attendent le jugement de la personne ; chacun ouvre l'issue et sa carte de résultat,
     la seule (atelier n°6).
  5. **Changes** : ce que la conversation a changé dans TaskForce (créé, déplacé, assigné, commenté, archivé, supprimé),
     avec « Undo » tant que c'est possible, et les pull requests ouvertes par ses missions.
  6. **Missions** : celles qui tournent, leur durée et « Stop » ; puis le nombre de celles terminées.
- R57 tient : ce panneau ne montre que le travail de la personne, et chaque ligne mène à son objet ; aucune mesure
  d'agent, aucun classement. Les panneaux d'AI Workflows disparaissent : leur contenu va dans « Missions » et dans la vue
  du travail.
- Sous 1 600 px de large, ouvrir un volet replie ce panneau ; un clic le rouvre.
- **Pour** : les cinq.
- **Contre** : aucun.
- **Preuve en dix jours** : après « archive l'issue qu'il y a dans In review by AI », « Changes » montre la bonne issue, et
  « Undo » la rend.
- **Signal d'arrêt** : une action de Cortex qui n'apparaît pas dans « Changes ».

### R123. La conversation n'est jamais vide, et dit ce qu'elle a lu

- **Quoi** :
  - la fenêtre s'ouvre là où la personne l'a laissée : la dernière conversation et son volet ;
  - une nouvelle conversation s'ouvre sur ce qui attend la personne (les résultats à juger, les demandes d'accord), puis
    sur trois suggestions tirées de l'état réel de l'espace, jamais d'exemples inventés ;
  - le compositeur : « + » pour joindre une issue, un projet ou un fichier ; le texte ; le micro (R76) ; l'envoi. Dessous,
    le modèle et l'indicateur de contexte. `@` pour les issues, les personnes et les projets, `/` pour les gestes, la
    liste ouverte dès le premier caractère ;
  - sous chaque réponse, une ligne grise : le modèle qui a répondu et ce que TaskForce lui a donné à lire (« qwen3:8b ·
    read OPS-35 and 3 comments »). Les commentaires que Cortex écrit sur une issue portent aussi le nom du modèle ;
  - les mots de l'agent sont toujours rendus, jamais en Markdown brut, dans la conversation comme dans les commentaires
    (constat 14) ;
  - une carte qui agit sur une issue montre sa clé, son titre et sa colonne ; un clic ouvre l'issue dans le volet.
- **Pour** : les cinq. Kenza Ait Si Abbou obtient « ce qu'il a lu » ; Norman, la colonne sur la carte.
- **Contre** : aucun.
- **Preuve en dix jours** : « prend OPS-35 et propose moi un resume dans les commentaire » : la ligne grise dit quel modèle
  a répondu et ce qu'il a lu, et un résumé écrit sans lire l'issue se voit à la lecture.
- **Signal d'arrêt** : la personne demande encore avec quel modèle une réponse a été écrite.

### R124. Retirer, jusqu'à l'essentiel

- **Quoi** :
  - quittent l'écran : la barre du haut (chaque volet a sa ligne de titre, la conversation la sienne) ; la cloche
    (« Waiting for you ») ; le tableau de bord comme accueil (un volet) ; le tour guidé (les suggestions de l'arrivée) ;
    les panneaux qui glissent (R122) ; les sous-menus de la barre de gauche (des filtres dans leur volet) ; l'animation
    entre les pages, puisqu'il n'y a plus de pages ;
  - les règles : une police, trois tailles dans la conversation ; une couleur d'accent ; des séparateurs d'un pixel
    plutôt que des cadres ; jamais une carte dans une carte ; des icônes de 16 px, d'un seul trait ; des mouvements de 150
    à 200 ms, sans rebond, et aucun quand le système en demande moins ; clair et sombre selon le système ; les hauteurs de
    contrôle d'aujourd'hui, inchangées ;
  - la règle de Norman : ce qui quitte le premier regard reste à deux clics ou par la recherche, et l'annulation ne quitte
    jamais l'écran.
- **Pour** : les cinq.
- **Contre** : aucun.
- **Preuve en dix jours** : les éléments de l'écran d'arrivée, comptés avant et après ; la boucle de démo jouée sans aide.
- **Signal d'arrêt** : une fonction dont la Présidence se servait reste introuvable une minute.

### R125. Ce que l'agent sait, et comment il progresse

- **Quoi** : un volet, « Progress », ouvert depuis le nom du modèle dans le compositeur et depuis Settings > AI.
  1. **Ce que chaque modèle sait faire**, mesuré ici (R113). Le modèle de Cortex se mesure seul la première fois
     (correction en cours) ; pour un modèle pas encore mesuré, ce que dit sa fiche (taille, fenêtre, outils), affiché
     comme tel, jamais un score d'éditeur. La table quitte les réglages pour ce volet.
  2. **Comment il fait dans le temps** : les résultats de la banque d'évaluations, par modèle et par date (R61, R118), et
     leur courbe dès qu'il y a plusieurs passages.
  3. **Ce qui l'a amélioré** : chaque correction devenue un cas (« Add to test bank »), l'incident d'où elle vient (E17),
     et son résultat depuis.
  4. **Ce qu'il sait de cet espace** : les sources qu'il peut lire (projets, notes, documents), comptées et datées.
- Ce n'est pas un écran de surveillance (R57) : il montre ce que l'agent sait et ce qui s'améliore, jamais son activité.
- **Pour** : les cinq. Jobs : un volet, pas une surface par brique.
- **Contre** : aucun.
- **Preuve en dix jours** : après la mesure automatique, le volet montre la ligne de qwen3:8b, et les six cas de R118 avec
  leur résultat.
- **Signal d'arrêt** : la Présidence le lit comme un écran de surveillance, ou personne ne l'ouvre en dix jours de test.

### R126. Le premier contact : l'installateur et les mises à jour

- **Quoi** :
  - les mises à jour s'installent sans fenêtre Windows : l'app télécharge, puis s'installe en silence à « Restart now » ou
    à la fermeture, montre son propre écran d'avancement, à l'allure de la page de connexion, et se relance ; un échec le
    dit (correction en cours) ;
  - la première installation : une fenêtre à l'allure de la page de connexion, la marque, une ligne d'avancement, aucun
    « Next » ; l'app s'ouvre à la fin. La technique se choisit sur les options chiffrées de la correction en cours (un
    petit installateur aux couleurs de TaskForce, le paquet Microsoft Store déjà prévu, d'autres), par coût et par
    risque ; d'ici là, la fenêtre NSIS habillée aux couleurs de TaskForce. La signature reste hors champ.
- **Pour** : les cinq.
- **Contre** : aucun.
- **Preuve en dix jours** : une mise à jour installée sans qu'aucune fenêtre Windows ne s'ouvre.
- **Signal d'arrêt** : une mise à jour qui échoue sans le dire.

## Le dessin, tranché par Jobs `[HYPOTHÈSE]`

Ce que la construction doit savoir, au-delà des recommandations.

| Élément | Mesure ou règle |
| --- | --- |
| Barre de gauche | La largeur d'aujourd'hui (16rem) ; Ctrl+B la replie |
| Conversation | Le texte sur une colonne de 720 px au plus, centrée ; le compositeur à la même largeur, en bas |
| Volet | Par défaut, la moitié de la place qui reste ; 480 px au moins ; une poignée ; la pleine largeur ; la largeur retenue pour la personne |
| Zone de droite | 320 px ; repliée sous 1 600 px de large quand un volet est ouvert |
| Ligne du haut | 44 px, la zone qu'on saisit pour déplacer la fenêtre de l'app desktop. À gauche, le bouton de la barre, puis le titre de la conversation (renommer, archiver, supprimer). À droite, le tableau du projet, la vue du travail quand une mission tourne, le bouton de la zone de droite ; sur Windows, les boutons de la fenêtre après eux |
| Écran étroit (webapp) | Les deux barres deviennent des tiroirs ; un volet couvre la conversation, avec un retour ; le compositeur reste en bas |
| Raccourcis | Ctrl+K cherche ; Ctrl+B replie la barre de gauche ; Échap referme ce qui vient de s'ouvrir |
| Les noms | New conversation, Search, Waiting for you, More, Environment, Context, Connectors, Results, Changes, Missions, Progress. Ils entrent au glossaire de l'interface (R22) |
| Ce qui ne change pas | La page de connexion, l'arrivée d'un nouveau compte, les réglages en fenêtre, la carte de résultat |

## Décision de la Présidence

La Présidence a validé d'avance : « il prend toute les decision possible, je valide tout directement », et « lance pas de
maquette ». R119 à R126 sont donc retenues telles que Jobs les a tranchées, et se construisent sans maquette. La
Présidence garde le dernier mot : elle peut en écarter ou en changer une en la voyant dans l'app.

## Notes du secrétariat

- **Formation** : cinq membres de trois pôles ; Harmonie et Science manquent, contre la règle d'un membre par pôle (§5),
  comme à l'atelier n°6. Le dossier porte R57, R95, R113, R114 et R116, votées avec ces pôles : l'atelier dessine dans
  ces limites et n'en amende aucune.
- **La délégation à Jobs** est un choix de la Présidence pour cette séance. Elle ne change pas la charte, où la
  Présidence décide seule (§2, point 4) : les décisions de Jobs sont déléguées, sous son dernier mot, et ne sortent pas
  du labo sous son nom (§8, point 3).
- **Siège historique et anachronismes** : Jobs, mort en 2011, ne connaît Claude Code, Electron ni les agents que par le
  dossier ; ses positions sont des transpositions de ses principes documentés.
- **Écart à la fiche** : la fiche de Saarinen le fait bondir devant un chat greffé comme interface par défaut. Il accepte
  ici une conversation au centre parce que les volets sont les vrais écrans et qu'aucun geste ne passe que par elle. Le
  secrétariat relève la tension, pas d'écart.
- **Conflits d'intérêts** :
  - Saarinen dirige Linear, concurrent direct de TaskForce ;
  - Zhuo a rejoint Meta avec le rachat de Sundial (23/10/2026) ;
  - le secrétariat est tenu par un modèle d'Anthropic, l'éditeur de Claude Code, la référence de la séance. La référence
    vient de la Présidence (sa capture), pas du secrétariat, et la séance prend la structure en écartant l'identité
    (R119).
- **La capture** montre une session de la Présidence : le PV n'en décrit que la structure, sans les noms de sessions.

## Suites

- Le PV au registre (§12) et au Journal.
- À `v1/13-roadmap/Roadmap_Backlog.md` : TF-J1-9, la fenêtre (R119 à R126).
- À `experiences/Experiences.md` : E18, la fenêtre mesurée avant et après (Zhuo) ; l'incident d'OPS-35 à E17.
- La construction, sans maquette, après la fusion des deux corrections en cours, qui touchent la fiche d'issue, la barre
  et Cortex. Trois lots, chacun utilisable :
  1. la fenêtre : les trois zones, la barre de gauche, le compositeur, la zone de droite avec ce qui existe ;
  2. les volets : le tableau, l'issue, la vue du travail et les autres écrans ; la pleine largeur et le compositeur
     replié ; les adresses ;
  3. l'arrivée, le volet « Progress », ce qui quitte l'écran, la ligne grise sous chaque réponse.
- Puis une release sur « go release », et le test de la Présidence sur l'app desktop.
- Un brouillon d'ADR avec le lot 1, puisque la fenêtre engage l'architecture du front (les volets et leurs adresses).

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- Le lot 2 est le plus risqué : les adresses, et la fiche d'issue devenue volet, touchent tous les écrans.
- Le lot 1 est le moins cher : la barre de gauche et la zone de droite réutilisent ce qui existe (les conversations, les
  accords, les missions, les connecteurs).
- La ligne grise de R123 est le gain de confiance le moins cher : TaskForce sait déjà quels outils ont tourné et quel
  modèle a répondu.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)

**Dernière mise à jour :** 05/11/2026 · **v1.0** · Projet Taskforce
