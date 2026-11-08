---
id: conseil-seance-2026-11-08-atelier-sobriete-banc-voix
title: "Séance n°19 du 08/11/2026 : l'atelier de la sobriété (l'arrivée, Progress, le banc des modèles, la voix)"
doc_type: pv-seance
statut: active
date: "08/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, arrivee, progress, benchmark, voix, attention]
related:
  - "../README.md"
  - "./2026-10-30-atelier-ecrans-base.md"
  - "./2026-11-01-revue-j0.md"
  - "./2026-11-05-atelier-fenetre.md"
  - "../../experiences/Experiences.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°19 du 08/11/2026 : l'atelier de la sobriété

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle, et les décisions de Jobs sont celles d'un personnage simulé.

## Résumé

La Présidence ouvre la 1.12.0 sur l'app desktop et arrive sur un mur : dix-sept lignes « Waiting for you », les suggestions
sous le compositeur, et à droite un volet « Progress » qui déborde de l'écran. Elle demande « comme raycast ou apple » : le
moins de texte possible, des icônes, ce qui n'est pas important part, mais reste accessible. Elle veut aussi le micro, et
un endroit où tester vraiment ce qu'on peut confier à chaque modèle.

L'atelier adopte six recommandations. L'arrivée tient en un regard, trois lignes au plus. « Waiting for you » ne compte que
ce qui attend vraiment : le dossier montre que quinze des dix-sept lignes sont des notifications non lues, sans rapport avec
une demande encore ouverte. Une règle de sobriété complète R124. Progress devient quatre onglets, une question chacun. Un
banc répond à « que puis-je confier à ce modèle ? », tâche par tâche, avec les réponses sous les yeux et le jugement de la
personne. La voix entre dans le compositeur, un clic pour démarrer, un clic pour arrêter, et reste sur la machine.

Tristan Harris, contradicteur, obtient que le nombre affiché ne soit jamais un appât. Don Norman obtient qu'une icône ait
toujours son nom. Esther Duflo refuse d'abord un verdict tiré de trois cas ; le banc dira « indicatif », montrera les
réponses et prendra le travail réel de la personne.

Six recommandations, R127 à R132, à l'unanimité des sept au second tour pour R131.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 08/11/2026), sur sa capture de l'app desktop 1.9.0 :
  - « me faut le micro ce sera plus simple » ;
  - « j'arrive la dessus, a droite j'ai le test de qwen pas tres concluant en bas, et ca sort de l ecran niveau affichage,
    c'est pas tres user friendly l'affiche, vraiment faire comme raycast ou apple quoi, moin s de texte possible, privilegier
    icon ou les choses pas importante on vire tu vois ? Mais info accessible quelque part quand mm quoi, voila, Jobs et
    equipe UI/UX dessus » ;
  - « me faut aussi une zone de benchmarking des model, sur l'app jsp mais vraiment tester la pertinence des model et
    quelles tche je peux leur assigner tu vois ? ».
- **Horizon** : avant la revue de J1 ; la Présidence refait la recette complète sur l'app desktop dès la release.
- **Formation** : restreinte (7), l'équipe de Jobs, plus un membre par pôle absent de l'atelier n°18.
  - Impulsion : Steve Jobs, qui tranche par délégation.
  - Pont : Kenza Ait Si Abbou (quelqu'un qui ne code pas).
  - Design : Karri Saarinen, Don Norman, Julie Zhuo.
  - Science : Esther Duflo (ce que mesure un banc).
  - Harmonie : Tristan Harris (l'attention, la fatigue du clic).
- **Ordre de parole**, tiré au sort à 17:33 UTC : Esther Duflo, Don Norman, Tristan Harris, Julie Zhuo, Kenza Ait Si Abbou,
  Steve Jobs, Karri Saarinen.
- **Contradicteur** : Tristan Harris, seul présent qui ne l'a jamais été.
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à sept.
- **Fiches** : à jour (moins de 30 jours) : Norman, Saarinen et Zhuo au 28/10/2026, Ait Si Abbou au 26/10, Duflo et Harris
  au 21/10 ; Jobs, siège historique, sans nouvelle source. Aucune fiche rafraîchie.

## Dossier

### 1. La capture de la Présidence `[ÉTABLI]`

Fenêtre de l'app desktop 1.9.0, conversation neuve, volet « Progress » ouvert :
- « Waiting for you » : dix-sept lignes, le compteur à 17 dans la barre de gauche. Quinze commencent par « Approve or
  refuse: », et plusieurs sont identiques mot pour mot ;
- les suggestions passent sous le compositeur, la troisième est coupée ;
- « Progress » : une table de sept colonnes, dont le bouton « Measure » est coupé au bord du volet, une barre de défilement
  horizontale, une phrase par modèle non mesuré, un paragraphe de proposition, et plus bas « 6 of 8 cases passed », avec les
  deux cas ratés en phrases entières.

### 2. Ce que le code fait aujourd'hui `[ÉTABLI]`

- **« Waiting for you » lit des notifications.** `waitingItems` (`frontend/lib/window/arrival.ts`) prend les signaux
  `agentApproval` non lus. Une notification naît à chaque demande (`NotificationService.notifyAgentApproval`), et rien ne la
  marque lue quand la demande est tranchée, refusée faute de réponse, ou que sa mission s'est arrêtée. Le nombre de la barre
  de gauche compte la même chose (`waitingCount`). Dans la copie de la base de la Présidence prise avant la 1.9.0 (comptes
  seulement, restaurés dans une base jetable puis effacés) : 16 notifications d'accord non lues, 0 demande ouverte (11
  accordées, 1 refusée), et aucune de ses six missions encore en cours.
- **La table déborde par construction.** `min-w-[560px]` dans un volet qui peut faire 480 px.
- **La suite de capacités** (`CapabilitySuite`, R113) compte huit cas sur cinq capacités (outils, contexte long, code,
  français, anglais), notés par le code. Le code, ce sont deux questions d'exécution mentale : `[10, 9, 1].sort()` et une
  liste par défaut en Python. qwen3:8b y fait 0 sur 2. Elle dit ce qu'un modèle sait faire, pas ce qu'on peut lui confier.
- **Aucune voix dans le code.** La politique `Permissions-Policy` du front interdit le micro (`microphone=()`). R76 et R80
  sont retenues depuis le 30/10 ; E15, qui doit choisir le modèle de transcription, n'a pas commencé.

### 3. Les décisions en vigueur

- **R76** (n°13) : une entrée sur chaque écran ; la voix d'un clic pour démarrer, d'un clic pour arrêter, jamais d'appui
  maintenu ; rien ne part sans Entrée ou le bouton d'envoi.
- **R80** (n°13) : dans l'app desktop, la voix se transcrit sur l'ordinateur ; dans la webapp, une phrase dit où elle va.
- **R57** (n°9) : pas d'écran de surveillance.
- **R113** (n°16), **R125** (n°18) : ce que sait faire chaque modèle, mesuré ici, dans un seul volet.
- **R51** (n°8) et **E11** : un petit modèle local pour les tâches en commentaire, jugé par la Présidence.
- **R123, R124** (n°18) : l'arrivée jamais vide ; retirer, jusqu'à l'essentiel ; ce qui quitte le premier regard reste à deux
  clics.

## Tour de table `[HYPOTHÈSE]`

- **Esther Duflo** (Science) : « 6 sur 8 » ne dit à personne ce qu'il peut confier à ce modèle. Un banc mesure ce qu'on lui
  demande de mesurer : si les cas sont des devinettes, le résultat est une devinette. Elle veut des tâches du vrai travail, les
  critères écrits avant le passage, et du travail réel de la personne à côté des cas fixes, parce qu'un cas fixe ne dit rien de
  ce qui marche chez elle. *Sa recommandation : un banc par tâche, dont le verdict dit sur quoi il repose.*
- **Don Norman** (Design) : il accepte de retirer les mots, pas de retirer le sens. Une icône sans nom est une devinette. Il
  veut le nom au survol, le même pour les lecteurs d'écran, et le détail à un clic. Il rappelle la règle de R124 : ce qui quitte
  le premier regard reste atteignable. *Sa recommandation : moins de texte, jamais moins d'information.*
- **Tristan Harris** (Harmonie, contradicteur) : il attaque le compteur. Dix-sept en face d'un mot comme « Waiting », c'est de
  la culpabilité fabriquée, et quinze sont faux. Un outil qui annonce des attentes qui n'existent pas apprend à les ignorer, et
  la vraie demande passera inaperçue : c'est la fatigue du clic. Il veut que le nombre ne compte que ce qui demande vraiment la
  personne, et qu'il ne serve jamais à la faire revenir. *Sa recommandation : dire vrai avant de dire peu.*
- **Julie Zhuo** (Design) : un écran, une question. Progress en pose quatre sur une seule colonne qui défile. Elle veut un
  sélecteur en haut, et un état vide qui dise le prochain geste. Pour l'arrivée, un seul regard. *Sa recommandation : quatre
  onglets, un geste principal par onglet.*
- **Kenza Ait Si Abbou** (Pont) : le micro est le plus grand gain pour quelqu'un qui ne code pas, à condition de voir ce qui a
  été compris avant que ça parte. Sur le banc, des mots simples : « Give it », pas un score. *Sa recommandation : la voix qui
  écrit dans le compositeur, un verdict en mots.*
- **Steve Jobs** (Impulsion) : ce n'est pas un problème de style. La Présidence a ouvert son app et elle a vu du travail
  administratif. Raycast tient parce qu'une ligne est une chose, et qu'on ne lit rien pour comprendre. Il retire les phrases,
  les préfixes, les dates de la première vue, le paragraphe de proposition. Il garde le nom, l'état, le geste. Sur la référence :
  la sobriété de Raycast et d'Apple, jamais leur identité. *Sa recommandation : une ligne par chose, et tout le reste un clic
  plus loin.*
- **Karri Saarinen** (Design) : un tableau de points se lit d'un coup d'oeil si les colonnes sont étroites et fixes. Une ligne de
  modèle tient dans 480 px sans défilement. Au clavier : les flèches et Entrée. Il refuse un tableau de bord de plus. *Sa
  recommandation : la matrice, dense, dans le volet qui existe.*

## Confrontation `[HYPOTHÈSE]`

1. **Moins dire, ou dire vrai ?** Jobs veut trois lignes. Harris répond que trois lignes d'une liste fausse restent fausses.
   Jobs accepte l'ordre : d'abord la vérité du compte (R128), ensuite la forme (R127). Harris demande que le nombre ne soit
   jamais rouge ni animé.
2. **Icônes ou mots ?** Jobs veut des icônes partout. Norman objecte : une icône qu'on n'a jamais vue ne se devine pas. Ils
   s'accordent : l'icône d'abord, son nom au survol et pour les lecteurs d'écran, un mot quand l'icône ne dit rien (les onglets,
   le verdict) (R129).
3. **Le verdict d'un banc.** Duflo vote contre au premier tour : trois cas ne prouvent pas qu'on peut confier une tâche à un
   modèle, et « Give it » promet plus que ça. Jobs ne veut ni pourcentage ni intervalle sur la première vue. Le texte amendé
   garde le mot, écrit « indicatif » au détail avec le nombre de cas, montre chaque réponse, laisse la personne retourner le
   verdict, et ajoute l'essai sur une de ses issues, à l'aveugle (R131). Duflo vote pour au second tour.
4. **Un classement ?** Harris s'inquiète d'un podium de modèles qui pousserait à en changer sans raison ; R57 l'interdit. La
   matrice ne trie pas par score : le modèle en service d'abord, les autres dans l'ordre où ils sont installés.

## Recommandations `[HYPOTHÈSE]`

### R127. L'arrivée tient en un regard

- **Quoi** :
  - au plus trois lignes de ce qui attend, une par mission ou par résultat, les demandes avant les résultats ; une ligne : une
    icône, ce qui attend en quelques mots, le nombre de demandes à droite s'il y en a plusieurs ; plus de préfixe « Approve or
    refuse: », l'icône le dit ;
  - au-delà de trois, une ligne « See all » avec le total, qui ouvre « Waiting for you » dans le volet ;
  - les trois suggestions restent visibles au-dessus du compositeur, jamais dessous ; l'arrivée ne défile pas sur une fenêtre
    de 800 px de haut.
- **Pour** : les sept.
- **Contre** : aucun.
- **Preuve en dix jours** : avec dix-sept éléments en attente, l'arrivée tient sans défiler, et ses éléments sont moins nombreux
  qu'en 1.12.0.
- **Signal d'arrêt** : la Présidence manque une vraie demande parce qu'elle n'était pas à l'écran.

### R128. « Waiting for you » dit vrai

- **Quoi** :
  - ne comptent que ce qui attend vraiment la personne : une demande d'accord encore ouverte, sur une mission qui peut encore
    la recevoir ; un résultat pas encore jugé ; une mention non lue reste une mention, comptée à part de ce qui bloque un agent ;
  - une demande tranchée, refusée faute de réponse ou dont la mission s'est arrêtée quitte la liste et le nombre, tout de suite ;
  - le nombre n'est ni rouge ni animé (Harris).
- **Pour** : les sept.
- **Contre** : aucun.
- **Preuve en dix jours** : la Présidence répond à une demande, le nombre baisse aussitôt ; après un redémarrage, les demandes
  de missions mortes ont disparu.
- **Signal d'arrêt** : un nombre que la Présidence ne croit plus.

### R129. Une ligne par chose (la règle de sobriété, après R124)

- **Quoi** :
  - une ligne par objet ; l'icône d'abord, son nom au survol et pour les lecteurs d'écran ; un mot quand l'icône ne suffit pas ;
  - aucune phrase qui explique ce qui se voit ; un verbe seulement sur un geste ;
  - le détail est à un survol ou un clic, jamais supprimé (Norman) ;
  - jamais de défilement horizontal dans un volet ; un seul geste principal par écran ;
  - s'applique à l'arrivée et à Progress dans ce lot, puis à chaque volet quand il est retravaillé. La sobriété de Raycast et
    d'Apple, jamais leur identité.
- **Pour** : les sept. Norman, avec le nom de chaque icône.
- **Contre** : aucun.
- **Preuve en dix jours** : le texte visible de Progress, compté en mots avant et après, baisse d'au moins la moitié, et aucune
  information n'a disparu.
- **Signal d'arrêt** : la Présidence cherche une information qu'elle ne trouve plus en un clic.

### R130. Progress : quatre onglets, une question chacun

- **Quoi** :
  - un sélecteur en haut du volet : **Models** (que sait faire chacun ?), **Benchmark** (que puis-je lui confier ? R131),
    **History** (comment ça évolue, et qu'est-ce qui l'a amélioré ?), **Sources** (que sait-il de cet espace ?) ;
  - Models : une ligne par modèle. Le nom, le point du modèle en service, un signe par capacité (réussi, en partie, raté, pas
    mesuré), un geste de mesure à droite, une icône. Un clic ouvre le détail dans la ligne : les cas ratés, la fiche du modèle
    (taille, fenêtre, outils), la date, « Use for Cortex » ;
  - le paragraphe d'introduction, la proposition et les phrases des modèles non mesurés quittent la première vue ;
  - tout tient dans 480 px.
- **Pour** : les sept.
- **Contre** : aucun.
- **Preuve en dix jours** : le volet à 480 px, aucune barre horizontale, le bouton de mesure entier.
- **Signal d'arrêt** : personne n'ouvre le détail, ou tout le monde l'ouvre à chaque fois.

### R131. Le banc : que puis-je confier à ce modèle ?

- **Quoi** :
  - un onglet, une matrice : une ligne par modèle, une colonne par tâche du vrai travail : **Summarize**, **Triage**, **Act**
    (agir sur le tableau par les outils), **Answer** (répondre depuis un document, ou dire que le document ne le dit pas),
    **Write**, **Plan**, **Code** ;
  - chaque tâche a au moins trois cas écrits avant tout passage, versionnés, notés par le code comme la suite de capacités ; ce
    qu'un modèle invente fait rater le cas ;
  - le verdict est en mots : **Give it** (tous les cas), **With review** (au moins la moitié), **Not yet** (moins), et le détail
    dit « indicatif » et le nombre de cas (Duflo) ;
  - le détail montre chaque réponse et son temps ; la personne peut retourner un verdict, et le verdict dit alors qu'il est le
    sien (R51) ;
  - **l'essai sur son travail** : on choisit une de ses issues, une tâche et deux ou trois modèles ; les réponses arrivent sous
    les lettres A, B, C ; on choisit, puis les noms apparaissent. Rien n'est écrit sur l'issue ;
  - aucun classement (R57) : le modèle en service d'abord, puis l'ordre d'installation. Le banc se lance à la demande et s'arrête
    d'un clic.
- **Pour** : sept au second tour. Au premier tour, Duflo contre (voir la Confrontation) : six sur sept, sous le seuil.
- **Contre** : aucun au second tour.
- **Preuve en dix jours** : la Présidence dit, en le lisant, quelles tâches elle confierait à qwen3:8b, et ne le contredit pas
  après l'essai sur une de ses issues.
- **Signal d'arrêt** : un modèle marqué « Give it » rate cette tâche sur le travail réel.

### R132. La voix dans le compositeur (R76 et R80, précisées)

- **Quoi** :
  - une icône de micro dans le compositeur, avant l'envoi ; un clic démarre, un clic arrête ; Échap annule ; jamais d'appui
    maintenu (R76) ;
  - pendant l'écoute, l'icône devient un carré d'arrêt, et une petite barre dit que le son arrive ;
  - le texte s'écrit dans le compositeur, où il se corrige ; rien ne part sans Entrée ou le bouton d'envoi (R76) ;
  - dans l'app desktop, la transcription tourne sur la machine (R80), le français et l'anglais sans réglage. Le modèle se
    télécharge une fois, au premier clic, sa taille dite avant, son avancement affiché. Une phrase courte, au survol : « Audio
    stays on this computer » ;
  - dans la webapp, le service du navigateur, avec la phrase de R80 avant le premier usage ;
  - E15 choisit le moteur : moins d'une erreur sur dix mots, moins de deux secondes après le second clic, sur la machine de la
    Présidence.
- **Pour** : les sept.
- **Contre** : aucun.
- **Preuve en dix jours** : la Présidence dicte les vingt commandes d'E15 pendant la recette.
- **Signal d'arrêt** : elle retape plus vite qu'elle ne corrige.

## Le dessin, tranché par Jobs `[HYPOTHÈSE]`

| Élément | Mesure ou règle |
| --- | --- |
| Arrivée | Trois lignes au plus, hauteur 32 px, puis « See all » ; trois suggestions |
| Signes des capacités | Point plein (réussi), demi-point (en partie), cercle (raté), tiret (pas mesuré) ; 16 px de large ; le nom et la note au survol |
| Ligne de modèle | 36 px ; le nom en police à chasse fixe, tronqué ; le geste de mesure toujours visible, une icône |
| Onglets de Progress | Un contrôle segmenté, un mot chacun, en haut du volet ; retenu par personne |
| Matrice du banc | Une colonne de 28 px par tâche, l'icône en tête, le nom au survol ; le verdict est un signe, son mot au survol et au détail |
| Essai à l'aveugle | Les réponses côte à côte si le volet le permet, l'une sous l'autre sinon ; un seul geste : choisir |
| Micro | 16 px, à gauche de l'envoi ; 150 ms pour le changement d'état ; pas d'animation quand le système en demande moins |

## Décision de la Présidence

La Présidence a mis Jobs et l'équipe UI/UX sur ce chantier (« Jobs et equipe UI/UX dessus »), et jugera sur l'app desktop (« je
refais les batteries de tests et recettes completement ici sur dekstop »). R127 à R132 se construisent telles que Jobs les a
tranchées, pour une release qu'elle attend (« Dit moi quand c'est release »). Elle garde le dernier mot : elle peut en écarter ou
en changer une en la voyant.

## Notes du secrétariat

- **La délégation à Jobs** est, comme à la n°18, un choix de la Présidence pour cette séance ; elle ne change pas la charte (§2,
  point 4).
- **Référence** : Raycast et Apple viennent de la Présidence. On prend la sobriété, pas l'identité.
- **Le dossier corrige le secrétariat** : la barre et l'arrivée disaient dix-sept parce qu'elles lisaient des notifications ; ni
  la revue du lot 3a ni le secrétariat ne l'avaient vu.
- **R76** : le secrétariat avait écrit le 08/11 que le micro attendait une décision. C'est faux : R76 et R80 sont retenues depuis
  le 30/10, il attendait E15. Corrigé à la roadmap.
- **Conflits d'intérêts** : Saarinen dirige Linear, concurrent direct ; Zhuo a rejoint Meta avec le rachat de Sundial ; le
  secrétariat est tenu par un modèle d'Anthropic.
- **Siège historique** : Jobs, mort en 2011, ne connaît Raycast ni les agents que par le dossier.

## Suites

- Le PV au registre (§12) et au Journal.
- À `v1/13-roadmap/Roadmap_Backlog.md` : TF-J1-10 (l'arrivée, « Waiting for you », Progress : R127 à R130), TF-J1-11 (le banc :
  R131), TF-J1-12 (la voix : R132 et E15).
- À `experiences/Experiences.md` : E19, le banc prédit-il le travail réel ? ; E15 passe en cours.
- La construction, sans maquette, puis une release, et la recette complète de la Présidence sur l'app desktop.

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- R128 est le gain le moins cher et le plus urgent : un nombre faux abîme tout ce qui l'entoure.
- R131 est le plus risqué : sept tâches à trois cas sont peu, et une suite mal écrite redonnera « pas très concluant ». L'essai
  sur le travail réel est ce qui peut le sauver.
- E15 décide si R132 tient : une dictée en français sur un petit modèle local peut décevoir.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)

**Dernière mise à jour :** 08/11/2026 · **v1.0** · Projet Taskforce
