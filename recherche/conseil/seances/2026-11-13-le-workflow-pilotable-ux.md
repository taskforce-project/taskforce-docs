---
id: conseil-seance-25-ux-workflow
title: "Spécification d'UX : le workflow pilotable (séance n°25, tranchée par Jobs)"
doc_type: design
statut: proposed
date: "13/11/2026"
auteur: Pierre MICHEL
tags: [recherche, conseil, design, ux, workflow, applications-embarquees]
related:
  - "./2026-11-13-le-workflow-pilotable.md"
  - "./2026-11-13-le-workflow-pilotable-plan-des-lots.md"
  - "../../decisions/ADR-026-DRAFT-la-fenetre.md"
  - "../../decisions/ADR-027-DRAFT-modele-des-processus.md"
  - "../../../v1/14-design/Design_System.md"
---

# Spécification d'UX : le workflow pilotable

> Jointe au PV de la [séance n°25](./2026-11-13-le-workflow-pilotable.md). Tranchée par Jobs, par délégation de la Présidence
> (« faudrait peut-être mettre Jobs sur la partie UX »), avec Norman, Zhuo et Saarinen ; Jobs est un personnage simulé, et la
> Présidence garde le dernier mot. Sans maquette : ce texte suffit pour construire. Il sert trois lots : W1 (la vue sur les données
> vivantes), W4 (le mode d'édition et le brouillon), W5 (le pilotage d'un processus). Les textes de l'interface sont en anglais
> (§11) et vont dans `frontend/lib/constants_en.ts`.

## 1. Les principes

Les cinq premiers comptent le plus.

1. **Une carte, trois lectures.** Le dirigeant, le chef de projet et l'ingénieur lisent la même carte du projet, plus ou moins
   dense ; jamais trois écrans, jamais un tableau de bord à part (R57).
2. **Ce qui t'attend d'abord.** « Needs you » est un état à part : il a sa marque, son compte dans l'en-tête, la tête de chaque
   colonne. Une attente sur une minuterie ou sur une autre personne reste calme.
3. **On décide là où l'on voit, et la règle se voit sur la décision** : qui peut signer, combien de signatures restent, quand cela
   expire, ce qui suivra. Jamais un « Approve » nu.
4. **Des mots, pas des symboles.** Aucune notation de BPMN : pas de losange, pas de cercle d'événement, pas de jeton. Une étape dit
   ce qu'elle fait, qui en répond et ce qui attend, en une phrase.
5. **Piloter, c'est pouvoir défaire.** Chaque geste passe par les règles, entre au dossier, et se défait quand il le peut ; un geste
   qui ne se défait pas le dit avant. Changer la définition se fait dans un mode à part, jamais par accident.
6. **Seul le présent bouge, et rien ne saute.** Une seule animation continue : l'anneau d'une étape au travail. Une donnée qui
   arrive ne déplace pas ce qu'on regarde.
7. **Des données vivantes seulement.** Un nœud est une issue, une mission, un accord, une étape ou un document réels ; aucune donnée
   fictive, pas même dans un état vide.
8. **La conversation pilote, l'application montre.** Chaque geste existe dans l'application et en mots ; Cortex propose d'ouvrir,
   il ne déplace jamais l'écran seul.

La grammaire de R133 et la direction artistique tiennent partout : une phrase d'abord, le détail à un clic, le brut à deux ; Geist,
les gris chauds, un seul bleu (`--primary`), des angles droits, des séparateurs d'un pixel, jamais une carte dans une carte, des
icônes `lucide-react` de 16 px d'un seul trait, des mouvements de 150 à 200 ms sans rebond, aucun quand le système en demande moins.

## 2. Où vit l'application

- **La route** : `/{slug}/projects/{id}/workflow` (`app/(protected)/[workspace]/projects/[id]/workflow/page.tsx`), rendue dans le
  volet comme le board (ADR-026), en `h-full min-h-0`.
- **L'onglet** : « Workflow », dans `PROJECT_TABS`, juste après « Board », icône `Workflow` de `lucide-react`.
- **L'adresse** (la route reste la source, ADR-026) :
  - `?node=` : le nœud choisi, `issue-{id}`, `run-{id}`, `approval-{id}`, puis `step-{id}` avec les processus ; choisir un nœud
    remplace l'adresse, ouvrir un objet en pousse une nouvelle ;
  - `?view=summary|plan|detail` : la densité ; sans paramètre, celle que la personne a choisie en dernier, sinon Plan ;
  - `?filter=needs-you|blocked|missing|failed` : un filtre à la fois ;
  - `?edit=1` : le mode d'édition (W4) ;
  - `?issue=` garde son sens : l'issue s'ouvre par-dessus la vue, dans le même volet, et la vue reste montée dessous.
- **Les entrées**, les mêmes que le board (`usePaneNavigation`) : le bouton « Workflow » de la ligne du titre, à côté de « Board » ;
  Ctrl+K (« Open the workflow of {project} ») ; les liens des réponses de Cortex, qui portent `?node=` ; la carte des missions de la
  zone de droite, qui mène ici au lieu du dialogue d'aujourd'hui ; dans « Waiting for you », « Open on its workflow » à côté de
  « Open on its board » pour ce qui appartient à un processus (W5).
- **En pleine largeur**, la conversation se replie dans le compositeur, en bas, comme ailleurs (ADR-026).
- **Ce qui part** : `workflow-canvas.tsx`, `workflow-canvas-dialog.tsx` et leur bouton ; `@xyflow/react` si plus rien ne l'importe.
  La vue n'est pas un canevas libre : des colonnes, du CSS, et un calque SVG pour les dépendances.

## 3. La mise en page de l'application

```
+--------------------------------------------------------------------------------------------------------------+
| Ligne du titre (44 px) : Projet    [Board] [Workflow] [List] ...        Live . [Summary|Plan|Detail] [Filter] [...] |
+--------------------------------------------------------------------------------------------------------------+
| En-tête de l'objectif (56 px)                                                                                  |
|  Le but, en une ligne                                                    Needs you 2   Blocked 1   Missing 1   |
|  Target 19 Dec . 14 of 31 done . 3 success criteria                                                            |
|  ============================.----------------------------- (2 px : la part faite ; un trait pour aujourd'hui)   |
+------------------+------------------+------------------+------------------+--------------------------------------+
| To do        7   | In progress  4   | In review    2   | Done        18   | Inspecteur (360 px, de 320 à 560)    |
| [porte]          | [nœud]           | [nœud]           | [nœud]           |  Titre . état                        |
| [nœud]           | [nœud]           |                  | Show 15 done     |  Details | Activity | Evidence | Def. |
| [nœud]           | ...              |                  |                  |  ...                                 |
+------------------+------------------+------------------+------------------+--------------------------------------+
```

- **La ligne du titre** (celle du volet, 44 px) : le nom du projet, ses onglets, puis à droite l'indicateur du temps réel, le
  sélecteur de densité (un contrôle segmenté de 28 px), « Filter », et « ... » (« Legend », « Export BPMN » avec les processus,
  « Edit process » avec W4).
- **L'en-tête de l'objectif** (56 px, fond `--paper-soft`, trait bas `--border`) :
  - à gauche, le but en une ligne (16 px, graisse 550, coupé d'une ellipse, entier au survol) ; dessous, en 12 px
    `--muted-foreground` : la date visée, ce qui est fait sur le total, le nombre de critères (un clic les montre) ;
  - à droite, des compteurs qui sont des filtres : « Needs you » (encre `--primary`, un point plein), « Blocked » et « Missing »
    (encre jaune), « Failed » (`--destructive`) ; un compteur à zéro disparaît ;
  - en bas, une ligne de 2 px : la part faite en `--primary`, sur le fond `--muted`, et un trait d'un pixel pour aujourd'hui entre
    le début et la date visée. L'avance ou le retard se lit à la forme, jamais à un pourcentage (R56).
  - sans objectif : « This project has no objective yet. » et le lien « Add an objective », qui ouvre un dialogue de 560 px, d'une
    colonne : le but en une phrase, la date visée, de un à cinq critères ; rien n'est inventé.
- **Les colonnes** : une par étape, de gauche à droite (W1 : les colonnes du projet, dans l'ordre du board ; avec un processus :
  ses étapes). Largeur 264 px en Plan (une carte de 240 px et 12 px de marge de chaque côté), 160 px en Summary, 304 px en Detail ;
  séparées par un trait d'un pixel `--border`, sans cadre. Un en-tête collant de 36 px : le nom (14 px, graisse 550), le nombre
  (Geist Mono 12 px, `--subtle`), et un cadenas de 16 px quand une porte ouvre l'étape. Les cartes s'empilent à 8 px d'écart ;
  défilement horizontal pour les colonnes, vertical dans chaque colonne.
- **Le tri dans une colonne** : Needs you, Failed, Missing, Blocked, Working, Waiting, Not started, Done ; Skipped et Stopped avec
  Done. Au-delà de cinq cartes faites, « Show {count} done ». Les sous-issues se rangent sous leur parent, en retrait de 12 px, avec
  un trait vertical d'un pixel ; repliées au-delà de trois.
- **L'inspecteur** : ancré à droite, 360 px par défaut, de 320 à 560 px par une poignée, la largeur retenue pour la personne ; il
  s'ouvre quand on choisit un nœud et se ferme par Échap. Sous 900 px de largeur de volet, il passe en feuille par-dessus les
  colonnes, avec un retour.
- **Rien d'autre** dans W1 : pas de minicarte, pas de zoom, pas de bande de temps (W9).

## 4. Le nœud

### 4.1 L'anatomie, en densité Plan

```
+-------------------------------------------+
|| (o) Approve the integration plan   OPS-35 |   ligne 1 : la marque d'état, le titre, la clé
||     [A] Alex  .  Claude Code             |   ligne 2 : qui en répond, et qui le fait
||     Waiting for your approval: the plan  |   ligne 3 : la phrase de ce qui se passe ou attend
||     before the agent starts.             |
||     [cadenas] 1 rule . 0 of 2 signed  [Decide] |   pied : la gouvernance, et un seul bouton
+-------------------------------------------+
```

- **La boîte** : 240 px de large, 72 px de haut au moins ; marge interne de 10 px en haut et en bas, 12 px sur les côtés ; trait
  d'un pixel `--border`, fond `--card`, angles droits, sans ombre. Survol : fond `--muted`. Choisi : un contour intérieur de 2 px
  `--ring`, le même au focus clavier.
- **La barre de gauche** (3 px) seulement pour ce qui demande l'attention : `--primary` pour Needs you, `--destructive` pour Failed,
  `--shape-yellow` pour Missing. Rien pour les autres.
- **Ligne 1** (20 px) : la marque d'état (16 px, §4.4), le titre (14 px, graisse 450, une ligne, ellipse), et à droite la clé de
  l'issue en Geist Mono 12 px `--subtle`. La clé est un mot de la personne (OPS-35), pas un identifiant interne ; aucun numéro de
  mission, d'accord ni empreinte n'apparaît.
- **Ligne 2** (16 px, 12 px, `--muted-foreground`) : qui en répond (un avatar de 16 px et le prénom) ; puis, s'il y a un agent, son
  logo de 16 px et son nom, suivis du modèle pour Cortex (« Cortex . qwen3:8b »).
- **Ligne 3** (12 px, deux lignes au plus) : la phrase de l'état (§11.4), en `--foreground` pour Needs you, Failed et Missing, en
  `--muted-foreground` sinon.
- **Le pied** (16 px, 12 px), seulement s'il a quelque chose à dire : un cadenas de 12 px et « {count} rules » (la phrase de la règle
  au survol) ; « {signed} of {needed} signed » ; « Proof: {count} events » ; en Detail, `+12 −1` en chasse fixe. À droite, au plus un
  bouton de 28 px, seulement quand le nœud attend la personne qui regarde : « Decide », « Review », « Provide », ou « See why » pour
  un échec.
- **Les clics** : un clic choisit le nœud et ouvre l'inspecteur ; le titre est un lien qui ouvre l'objet (l'issue par `?issue=`, la
  mission dans sa vue `/{slug}/missions/{runId}`) ; Entrée fait de même ; un double clic aussi.

### 4.2 La densité Summary (le dirigeant)

- Les colonnes font 160 px. En tête de chacune, une ligne de compte : « 3 working . 1 needs you . 9 done ».
- Seules les exceptions gardent une carte, réduite à une ligne de 32 px (la marque, le titre, qui doit agir) : Needs you, Failed,
  Missing, Blocked, et ce qui a passé sa date. Le reste n'est qu'un compte.
- L'en-tête de l'objectif ne change pas : c'est la première lecture.

### 4.3 La densité Detail (l'ingénieur)

- Les colonnes font 304 px, les cartes 280 px.
- Une ligne de plus, en Geist Mono 12 px `--subtle`, entre la phrase et le pied : pour une mission, l'agent et son modèle, la
  branche, les tests (« tests 12/12 »), `+12 −1` ; pour un accord, la règle et sa version, l'échéance ; pour une étape (W2 à W5), son
  type, le délai et les tentatives.
- L'inspecteur s'ouvre sur l'onglet « Definition ».

### 4.4 Les états

Chaque état a sa marque et son mot : jamais la couleur seule. Les noms d'icônes sont ceux de `lucide-react` (ou leur équivalent dans
la version du projet).

| État | Marque | Couleur | Mot | Bouge | Tri |
| --- | --- | --- | --- | --- | --- |
| Needs you | `CircleDot` | `--primary`, barre `--primary` | Needs you | Non | 1 |
| Failed | `CircleAlert` | `--destructive`, barre `--destructive` | Failed ; Stuck pour un incident | Non | 2 |
| Missing | `FileQuestion` | encre jaune, barre `--shape-yellow` | Missing | Non | 3 |
| Blocked | `CircleSlash` | encre jaune | Blocked | Non | 4 |
| Working | `LoaderCircle`, qui tourne (un tour en 1,2 s ; fixe si le système demande moins de mouvement) | `--primary` | Working | Oui, seul | 5 |
| Waiting | `Clock` | `--muted-foreground` | Waiting for {who or what} | Non | 6 |
| Not started | `Circle` | `--subtle` | Not started | Non | 7 |
| Done | `CircleCheck` | encre verte | Done | Non | 8 |
| Skipped | `CircleDashed` | `--subtle` | Skipped ; Left out dans un brouillon | Non | 9 |
| Stopped | `CircleStop` | `--subtle` | Stopped | Non | 9 |

La légende (« ... », puis « Legend », ou la touche `?`) montre ces dix lignes, telles quelles.

### 4.5 D'où vient l'état (W1, puis W5)

Une logique pure, dans `frontend/lib/workflow/`, testée cas par cas. Le premier état qui s'applique l'emporte, dans l'ordre du tri :

1. **Needs you** : un accord en attente que la personne qui regarde peut décider (`canDecide`) ; une mission prête pour sa revue
   (« Ready for your review ») ; avec W5, une tâche humaine qui lui revient, ou un manque qu'on lui a demandé.
2. **Failed** : la dernière mission a échoué et n'a pas été relancée ; avec W5, un incident ouvert (« Stuck »).
3. **Missing** (W5) : un document ou une réponse attendus d'une autre personne.
4. **Blocked** : une relation « blocked by » vers une issue qui n'est pas finie (les relations de W0).
5. **Working** : une mission en cours ; avec W5, une étape d'agent en cours.
6. **Waiting** : un accord qu'une autre personne doit donner ; une mission en file (« Waiting for your runner to pick it up ») ;
   avec W5, une minuterie.
7. **Not started** : une issue dans une colonne de départ, sans mission.
8. **Done**, **Skipped**, **Stopped** : selon la colonne, la mission ou l'étape.

Une mission relancée reste Working, puis passe à Done seulement quand l'étape a réussi : jamais de faux vert.

### 4.6 Les portes

- W1 : un accord appartient à la mission d'une issue ; il vit sur le nœud de l'issue (l'état Needs you ou Waiting, le pied, le
  bouton). Pas de nœud flottant.
- Avec un processus (W4, W5) : un accord qui ouvre une étape est une porte, une carte en tête de la colonne, avec l'icône `Hand` et la
  phrase « Approval to enter {stage} » ; même anatomie, même décision.

### 4.7 Les types d'étapes à l'écran (W4, W5)

Aucun symbole de BPMN ; le type se lit dans les mots de la carte.

| Type | À l'écran |
| --- | --- |
| L'étape d'agent | La carte, avec l'agent et son modèle en ligne 2 ; dans l'inspecteur, le déroulé de la mission (Understand, Plan, Do, Check, Hand over) |
| La tâche humaine | La carte, avec la personne en ligne 2 et la question en ligne 3 ; au pied, son genre : « Approval », « Review », « Input », « Checklist {done} of {total} » |
| La décision | Une carte basse (48 px) : l'icône `Split` et « Decision: {question} » ; dessous, deux lignes en mots : « If yes: {step} », « Otherwise: {step} » ; les flèches seulement à la sélection |
| L'attente | La carte, avec `Clock` : « Wait for {what} » et qui doit le fournir, ou « Wait {duration} » |
| La zone d'agent | Un cadre en pointillés d'un pixel autour de ses étapes, titré « Agent zone: works freely here, under {count} rules » |
| En parallèle | Une étiquette « In parallel » au-dessus des cartes concernées, et un crochet de 2 px à gauche ; la jonction est implicite |

### 4.8 Les dépendances

- Dessinées seulement pour le nœud choisi : en amont ce qui le bloque, en aval ce qu'il bloque, sur un calque SVG au-dessus des
  colonnes ; des courbes de 2 px en `--primary`, une pointe de 6 px ; au survol d'une arête, « Blocks » ou « Blocked by ».
- Les autres nœuds s'estompent à 40 % d'opacité, en 150 ms.
- Au plus 50 arêtes dessinées ; au-delà, l'inspecteur dit « and {count} more ».

## 5. L'inspecteur

En-tête : le titre, la marque et le mot de l'état, « Ask about this step » (bouton fantôme), la croix. Quatre onglets :

- **Details** :
  - ce que c'est (une issue, une mission, un accord, une étape et son type), en une phrase ;
  - « Answers for it » : la personne ; « Done by » : l'agent et son modèle ;
  - « Waiting for » : ce qui attend, et qui ; « Next » : l'étape ou la colonne qui suit ;
  - « Blocked by » et « Blocks » : des listes de lignes de 36 px, chacune un lien ;
  - « Documents » : ceux qu'on attend et ceux qui sont là (W5) ;
  - **la décision**, quand le nœud attend la personne (§6.1).
- **Activity** : pour une mission, le déroulé en cinq étapes de la vue d'une mission (le même composant, en compact), avec « Show
  commands » ; pour une issue, son activité ; pour une étape (W5), les événements de l'instance, en phrases.
- **Evidence** : la règle appliquée (sa phrase et sa version) ; les accords et leurs signatures (qui, quand, avec quelle
  signification) ; les fichiers changés, `+12 −1` par fichier, chacun ouvrant son diff dans la vue de la mission ; la pull request ;
  les tests ; « Proof: {count} events, sealed » et le téléchargement du dossier.
- **Definition** (Detail ouvre ici) : le type de l'étape et ses réglages, en lignes typées (l'agent, le modèle, les outils permis, le
  délai, les tentatives, la règle d'une décision, verrouillée ou non et par qui, la personne qui en répond) ; la version (« {process}
  . version {n} . by {author} . {date} ») ; « Export BPMN » au niveau du processus ; « Show raw » ouvre le brut, en chasse fixe, à
  deux clics.

## 6. Les gestes

### 6.1 Décider

« Decide » ouvre la décision dans l'inspecteur :

- « Approve {what}? », en 16 px ;
- « Rule: {sentence} » ;
- les signatures : « {count} different people approve: {signed} so far. » ; et, s'il le faut, « The person who delegated this task
  can't approve it. » ;
- l'échéance et ce qui suit : « Expires {time}. Then: No answer in time: refused. » ;
- la signification de la signature : « Signing as {name}. Meaning: Approval. » (W1 : toujours Approval ; avec W5, celle de la tâche :
  Approval, Review, Responsibility ou Authorship) ;
- « Why? (optional) », un champ d'une ligne ;
- « Approve » (bouton principal) et « Refuse » (bouton à liseré), en bas à droite ; « This can't be undone. » quand l'accord engage.

La décision passe par `POST /delivery/runs/{runId}/approvals/{approvalId}`, déjà jugée par les règles et entrée au dossier. Pour qui
ne peut pas décider : « Waiting for {who}. You can't decide this one. », sans bouton.

### 6.2 La table des gestes

| Geste | Où | Quand | Ce qui se passe | Défaire |
| --- | --- | --- | --- | --- |
| Choisir | Clic, `j` et `k`, les flèches | Toujours | L'inspecteur s'ouvre ; l'adresse prend `?node=` | Échap |
| Ouvrir | Le titre, Entrée, double clic | Toujours | L'issue par-dessus la vue, ou la vue de la mission | Retour |
| Décider | « Decide », `d` | Needs you, un accord | §6.1 | Non, et c'est dit |
| Demander à Cortex | « Ask about this step », `.` | Toujours | Le nœud se joint au compositeur ; Cortex voit la sélection | Retirer la pièce jointe |
| Arrêter | Le menu du nœud | Une mission au travail | Un dialogue de 420 px : « Stop this mission? The work done so far stays on its branch. » | Non |
| Relancer | « Try again » (W5 : « Try again from {step} ») | Failed, après avoir lu la cause | La route qui existe ; le nœud passe à Working, jamais au vert d'avance | Non |
| Confier | « Hand to an agent » | Not started, une issue | Le parcours de délégation qui existe, sous les règles | Arrêter la mission |
| Déplacer | « Move to... », `m` | Une issue | La route du board ; « Moved to {column}. Undo » pendant 5 s | « Undo » |
| Passer l'étape (W5) | Le menu du nœud | Une étape non verrouillée, par une personne | Un dialogue de 420 px : « Skip {step}? » et « Why skip it? », la raison exigée | « Undo » tant que l'étape suivante n'a pas commencé |
| Fournir (W5) | « Provide » | Missing, demandé à la personne | Un fichier ou un document rangé ; le message réveille l'instance | Non |
| Demander à quelqu'un d'autre (W5) | Le menu du nœud | Missing | Choisir un membre ; la demande passe à lui | Rendre la demande |
| Ajouter une étape (W4) | « + » entre deux cartes | En mode d'édition seulement | §8 | Retirer avant de publier |

Chaque geste passe par les règles et entre au dossier ; les mêmes gestes existent en mots, par Cortex, en cartes décidées par leurs
boutons. Pas de glisser-déposer dans W1 : on pilote sans risquer de déplacer par mégarde.

### 6.3 Le clavier

`j` et `k` : le nœud suivant ou précédent, colonne par colonne ; `←` et `→` : la colonne voisine ; `f` : le prochain nœud qui demande
l'attention (Needs you, puis Failed, puis Missing) ; Entrée : ouvrir ; `d` : décider ; `.` : demander à Cortex ; `m` : déplacer ; `1`,
`2`, `3` : Summary, Plan, Detail ; `?` : la légende ; Échap : fermer l'inspecteur, puis la sélection. Ces touches entrent au pied de
Ctrl+K ; aucune n'est annoncée ailleurs (R134).

## 7. Les trois lectures

| Lecture | La question de sa première minute (E24) | Où est la réponse |
| --- | --- | --- |
| Le dirigeant (CEO) | « Le projet tiendra-t-il sa date, qu'est-ce qui bloque, et qui doit décider ? » | L'en-tête (le but, la date, la ligne de la part faite et le trait d'aujourd'hui, les compteurs), et Summary : seules les exceptions, chacune avec qui doit agir |
| Le chef de projet (PM) | « Que pouvez-vous débloquer maintenant, et pour qui ? » | Plan : Needs you en tête de chaque colonne, `f`, le filtre « Needs you », la phrase de chaque carte, les gestes sur le nœud |
| L'ingénieur | « Qu'a fait exactement cette étape, sous quelle règle, et comment la relancer ? » | Detail et l'inspecteur : Activity (le déroulé, « Show commands »), Evidence (la règle et sa version, les signatures, les fichiers, la preuve), Definition (les réglages, la version), « Try again » |

Personne ne choisit sa lecture par un profil : la densité se change d'un geste, et se retient pour la personne.

## 8. Le mode d'édition (W4, puis W6)

- **On y entre** par « Edit process » (le menu « ... ») ou par « Review in Workflow » sur la carte d'un brouillon. L'adresse prend
  `?edit=1`.
- **Un bandeau** de 40 px sous l'en-tête, fond teinté bleu, encre bleue : « Editing {process}: draft of version {n}. Nothing running
  changes. » ; à droite : « Review changes » (bouton à liseré), « Publish version {n} » (bouton principal, inactif tant que rien ne
  le permet), « Leave ».
- **Les questions** du brouillon, sous le bandeau : « {count} questions before you can publish », chacune avec son champ typé (un
  choix, une date, une personne).
- **Chaque étape proposée** porte, au survol et au focus, trois gestes : « Accept », « Change » (le titre, qui répond, qui décide,
  dans la carte ; les réglages dans l'inspecteur), « Remove ». Une étape verrouillée montre un cadenas et, à « Remove », « Required by
  {source}. It can't be removed. »
- **Une étape écartée par l'IA** reste à sa place, en carte fantôme en pointillés : « Left out: {step}. {reason} » et « Keep it ».
  Dans un workflow marqué régulé, il n'y en a aucune.
- **Ajouter une étape** : un « + » de 16 px entre deux cartes, au survol ; un menu de cinq lignes : « Agent step », « Human task »,
  « Decision », « Wait », « Agent zone » ; la carte naît en édition, et demande qui en répond.
- **Publier** exige : chaque étape acceptée, chacune avec une personne qui en répond, les questions répondues, le vérificateur
  passé. Sinon, la phrase de ce qui manque (« {count} steps still to accept. », « Every step needs a person who answers for it. »),
  et « Show me » mène à la carte. Un workflow régulé demande une seconde personne : « A regulated workflow needs a second person to
  publish. »
- **« Review changes »** : un dialogue de 720 px, la liste en mots depuis la version publiée (« Added: … », « Removed: … », « Changed:
  … », « Left out: … »), et « Show BPMN » pour l'ingénieur.
- **Après la publication** : « Version {n} published. Running work keeps version {previous}. »
- **Jamais** de « tout accepter ». « Start from an empty list » reste possible.

## 9. La conversation et les applications embarquées

- **Une réponse** qui nomme une issue, une mission, une étape ou un accord en fait un lien vers son application, nœud choisi.
- **La carte d'un nœud dans la conversation** : le même composant que la carte de la vue, en compact (deux lignes : la marque, le
  titre et le mot de l'état ; la phrase), avec le bouton de son geste (« Decide », « Try again », « Provide ») et « Open in Workflow »
  (bouton fantôme). Elle lit les mêmes stores : elle change quand la vue change.
- **La carte d'un geste préparé** par Cortex garde sa forme : « Cortex proposes to {what}. Nothing changes until you approve it. »,
  puis « Approve » et « Refuse » ; une fois décidé, le nœud de la vue s'allume une seconde (fond `--accent`, qui s'éteint en 600 ms).
- **La carte d'un brouillon** (W4) : « Draft from your objective », « {steps} steps, {leftOut} left out, {questions} questions », et
  « Review in Workflow ».
- **Cortex voit** l'application ouverte et le nœud choisi (R114) ; « Ask about this step » joint le nœud au compositeur.
- **Cortex n'ouvre ni ne déplace jamais l'écran** : il propose « Open in Workflow », la personne clique.

## 10. Le vivant, l'échelle, l'étroit, l'accessibilité

- **Le temps réel** : `/topic/projects.{id}`, `/topic/projects.{id}.delivery` (W0) et `.analysis`, par `use-stomp.ts`. Dans la ligne
  du titre, un point et un mot : « Live » (point vert), « Reconnecting… » (point jaune), « Offline. Showing {time}. » (point gris) ; au
  retour, tout se relit.
- **Rien ne saute** : une carte nouvelle apparaît en fin de sa place de tri, en 150 ms de fondu ; une carte qui change d'état ne
  change de place que dans sa colonne ; une carte qui change de colonne glisse en 200 ms, sans rebond ; une donnée qui arrive ne
  déplace ni la sélection, ni le défilement.
- **L'échelle** : au-delà de 50 cartes dans une colonne, « Show {count} more » ; seules les cartes visibles se rendent ; les arêtes
  seulement pour la sélection, 50 au plus ; aucune position n'est enregistrée.
- **L'étroit** (sous 768 px, la webapp) : les colonnes deviennent une liste de sections, une par étape, les cartes en pleine
  largeur ; l'inspecteur, une feuille plein écran avec un retour ; l'en-tête sur deux lignes ; Plan seulement, Summary par le filtre
  « Needs you ».
- **L'accessibilité** : chaque carte est un élément focalisable, nommé par son titre et décrit par sa phrase ; un tabindex mobile
  par colonne, les flèches pour se déplacer ; l'inspecteur est une région complémentaire ; un changement vers Needs you s'annonce
  poliment (`aria-live="polite"`), et rien d'autre ; les contrastes des jetons, AA en clair et en sombre ; l'état n'est jamais dit
  par la couleur seule.
- **Les états de la vue** : le chargement, des colonnes en squelette, sans roue qui tourne ; l'erreur, « Couldn't load the
  workflow. {cause} » et « Try again » ; un projet sans travail, « This project has no work yet. » et « Create an issue » ; un filtre
  vide, « Nothing needs you here. ».

## 11. Les textes de l'interface (anglais)

Dans `frontend/lib/constants_en.ts`, sous `workflow` (et `detail.workflow` pour l'onglet). Les textes qui existent déjà se
reprennent tels quels : « Approve », « Refuse », « Try again », « Stop », « Waiting for you », « Ready for your review », « Waiting
for your runner to pick it up », « No answer in time: refused ». Aucun tiret cadratin : des deux-points et des virgules.

### 11.1 Naviguer

| Clé | Texte |
| --- | --- |
| `detail.workflow` | Workflow |
| `workflow.paletteOpen` | Open the workflow of {project} |
| `workflow.openInWorkflow` | Open in Workflow |
| `workflow.openOnWorkflow` | Open on its workflow |
| `workflow.density.label` | How much to show |
| `workflow.density.summary` | Summary |
| `workflow.density.plan` | Plan |
| `workflow.density.detail` | Detail |
| `workflow.filter.label` | Filter |
| `workflow.filter.clear` | Show everything |
| `workflow.legend` | Legend |
| `workflow.follow` | Follow |
| `workflow.nextAttention` | Next that needs attention |
| `workflow.live.on` | Live |
| `workflow.live.reconnecting` | Reconnecting… |
| `workflow.live.offline` | Offline. Showing {time}. |

### 11.2 L'objectif

| Clé | Texte |
| --- | --- |
| `workflow.objective.none` | This project has no objective yet. |
| `workflow.objective.add` | Add an objective |
| `workflow.objective.target` | Target {date} |
| `workflow.objective.noTarget` | No target date |
| `workflow.objective.done` | {done} of {total} done |
| `workflow.objective.criteriaOne` | 1 success criterion |
| `workflow.objective.criteriaMany` | {count} success criteria |
| `workflow.objective.dialogTitle` | What is this project for? |
| `workflow.objective.goalLabel` | Objective, in one sentence |
| `workflow.objective.dateLabel` | Target date |
| `workflow.objective.criteriaLabel` | How you'll know it's done |
| `workflow.objective.criteriaHelp` | One to five criteria. Each one should be something you can check. |
| `workflow.objective.save` | Save the objective |
| `workflow.count.needsYou` | Needs you {count} |
| `workflow.count.blocked` | Blocked {count} |
| `workflow.count.missing` | Missing {count} |
| `workflow.count.failed` | Failed {count} |

### 11.3 Les états

| Clé | Texte |
| --- | --- |
| `workflow.state.needsYou` | Needs you |
| `workflow.state.failed` | Failed |
| `workflow.state.stuck` | Stuck |
| `workflow.state.missing` | Missing |
| `workflow.state.blocked` | Blocked |
| `workflow.state.working` | Working |
| `workflow.state.waiting` | Waiting |
| `workflow.state.notStarted` | Not started |
| `workflow.state.done` | Done |
| `workflow.state.skipped` | Skipped |
| `workflow.state.leftOut` | Left out |
| `workflow.state.stopped` | Stopped |

### 11.4 Les phrases des nœuds

| Clé | Texte |
| --- | --- |
| `workflow.now.approval` | Waiting for your approval: {what}. |
| `workflow.now.waitingFor` | Waiting for {who}. |
| `workflow.now.blockedBy` | Blocked by {key}: {title}. |
| `workflow.now.blockedByMany` | Blocked by {count} issues. |
| `workflow.now.failed` | {step} failed: {cause}. |
| `workflow.now.stuck` | Stopped after {attempts} tries: {cause}. |
| `workflow.now.missing` | Missing: {document}. Asked {who} {time}. |
| `workflow.now.missingYou` | Missing: {document}. You were asked {time}. |
| `workflow.now.retried` | Tried again {time}. Waiting for the result. |
| `workflow.now.skipped` | Skipped by {who}: {reason} |
| `workflow.now.done` | Done {time}. |
| `workflow.now.due` | Due {time}. |
| `workflow.action.decide` | Decide |
| `workflow.action.review` | Review |
| `workflow.action.provide` | Provide |
| `workflow.action.seeWhy` | See why |
| `workflow.gov.rulesOne` | 1 rule |
| `workflow.gov.rulesMany` | {count} rules |
| `workflow.gov.signed` | {signed} of {needed} signed |
| `workflow.gov.proof` | Proof: {count} events |
| `workflow.gov.lockedBy` | Required by {source}. It can't be skipped. |
| `workflow.incident.whatToDo` | What to do: {action} |
| `workflow.incident.resolved` | Resolved by {who}: {how}. |

### 11.5 Les types d'étapes

| Clé | Texte |
| --- | --- |
| `workflow.type.agent` | Agent step |
| `workflow.type.human` | Human task |
| `workflow.type.decision` | Decision |
| `workflow.type.wait` | Wait |
| `workflow.type.zone` | Agent zone |
| `workflow.type.approval` | Approval |
| `workflow.type.input` | Input |
| `workflow.type.checklist` | Checklist {done} of {total} |
| `workflow.type.decisionQuestion` | Decision: {question} |
| `workflow.type.ifYes` | If yes: {step} |
| `workflow.type.otherwise` | Otherwise: {step} |
| `workflow.type.waitFor` | Wait for {what} |
| `workflow.type.waitDuration` | Wait {duration} |
| `workflow.type.zoneTitle` | Agent zone: works freely here, under {count} rules |
| `workflow.type.parallel` | In parallel |
| `workflow.type.gate` | Approval to enter {stage} |

### 11.6 L'inspecteur et la décision

| Clé | Texte |
| --- | --- |
| `workflow.inspector.details` | Details |
| `workflow.inspector.activity` | Activity |
| `workflow.inspector.evidence` | Evidence |
| `workflow.inspector.definition` | Definition |
| `workflow.inspector.answersFor` | Answers for it |
| `workflow.inspector.doneBy` | Done by |
| `workflow.inspector.waitsFor` | Waiting for |
| `workflow.inspector.next` | Next |
| `workflow.inspector.blockedBy` | Blocked by |
| `workflow.inspector.blocks` | Blocks |
| `workflow.inspector.documents` | Documents |
| `workflow.inspector.ask` | Ask about this step |
| `workflow.inspector.showRaw` | Show raw |
| `workflow.inspector.exportBpmn` | Export BPMN |
| `workflow.inspector.moreEdges` | and {count} more |
| `workflow.inspector.proofSealed` | Proof: {count} events, sealed |
| `workflow.decide.title` | Approve {what}? |
| `workflow.decide.rule` | Rule: {sentence} |
| `workflow.decide.expires` | Expires {time}. Then: {then} |
| `workflow.decide.signingAs` | Signing as {name}. Meaning: {meaning}. |
| `workflow.decide.meaning.approval` | Approval |
| `workflow.decide.meaning.review` | Review |
| `workflow.decide.meaning.responsibility` | Responsibility |
| `workflow.decide.meaning.authorship` | Authorship |
| `workflow.decide.why` | Why? (optional) |
| `workflow.decide.final` | This can't be undone. |
| `workflow.decide.notYours` | Waiting for {who}. You can't decide this one. |

### 11.7 Les gestes

| Clé | Texte |
| --- | --- |
| `workflow.gesture.open` | Open |
| `workflow.gesture.stopTitle` | Stop this mission? |
| `workflow.gesture.stopBody` | The work done so far stays on its branch. |
| `workflow.gesture.retryFrom` | Try again from {step} |
| `workflow.gesture.handToAgent` | Hand to an agent |
| `workflow.gesture.moveTo` | Move to… |
| `workflow.gesture.moved` | Moved to {column}. |
| `workflow.gesture.undo` | Undo |
| `workflow.gesture.skip` | Skip this step |
| `workflow.gesture.skipTitle` | Skip {step}? |
| `workflow.gesture.skipWhy` | Why skip it? |
| `workflow.gesture.skipConfirm` | Skip the step |
| `workflow.gesture.askSomeoneElse` | Ask someone else |

### 11.8 L'édition et le brouillon

| Clé | Texte |
| --- | --- |
| `workflow.edit.enter` | Edit process |
| `workflow.edit.banner` | Editing {process}: draft of version {n}. Nothing running changes. |
| `workflow.edit.reviewChanges` | Review changes |
| `workflow.edit.publish` | Publish version {n} |
| `workflow.edit.leave` | Leave |
| `workflow.edit.accept` | Accept |
| `workflow.edit.change` | Change |
| `workflow.edit.remove` | Remove |
| `workflow.edit.addStep` | Add a step |
| `workflow.edit.leftOut` | Left out: {step}. {reason} |
| `workflow.edit.keepIt` | Keep it |
| `workflow.edit.questionsOne` | 1 question before you can publish |
| `workflow.edit.questionsMany` | {count} questions before you can publish |
| `workflow.edit.toAccept` | {count} steps still to accept. |
| `workflow.edit.ownerMissing` | Every step needs a person who answers for it. |
| `workflow.edit.showMe` | Show me |
| `workflow.edit.lockedRemove` | Required by {source}. It can't be removed. |
| `workflow.edit.regulatedSecond` | A regulated workflow needs a second person to publish. |
| `workflow.edit.published` | Version {n} published. Running work keeps version {previous}. |
| `workflow.edit.startEmpty` | Start from an empty list |
| `workflow.edit.showBpmn` | Show BPMN |
| `workflow.draft.title` | Draft from your objective |
| `workflow.draft.summary` | {steps} steps, {leftOut} left out, {questions} questions |
| `workflow.draft.review` | Review in Workflow |

### 11.9 Les états de la vue

| Clé | Texte |
| --- | --- |
| `workflow.empty.noWork` | This project has no work yet. |
| `workflow.empty.createIssue` | Create an issue |
| `workflow.empty.nothingNeedsYou` | Nothing needs you here. |
| `workflow.showDone` | Show {count} done |
| `workflow.showMore` | Show {count} more |
| `workflow.error.load` | Couldn't load the workflow. {cause} |

## 12. Ce qu'il ne faut pas faire

- Un symbole de BPMN : losange, cercle d'événement, jeton, couloir de rôle.
- Une fenêtre par-dessus l'application, ou un dialogue pour la vue entière : la vue a son adresse.
- Voir sans pouvoir agir : chaque état qui attend quelqu'un a son geste sur le nœud.
- La pelote : toutes les arêtes à la fois.
- Une couleur sans son mot, ou une couleur qui change de sens d'une densité à l'autre.
- Une mise en page qui saute quand une donnée arrive.
- Une attente cachée, un faux vert après une relance.
- Un « Approve » nu, sans la règle, les signatures, l'échéance et ce qui suit.
- Les journaux comme seul détail : la phrase d'abord, les commandes à deux clics.
- Une vivacité à deviner : le temps réel se dit dans la ligne du titre.
- Un mot interne au premier regard : un nom d'outil, un code d'erreur, un identifiant de mission ou d'accord, une empreinte.
- Une carte dans une carte ; un tableau dans un volet de moins de 720 px (R141) ; plus d'une couleur d'accent.
- Un glisser-déposer qui change un état par mégarde ; un écran qui bouge sans que la personne l'ait demandé.
- Un « tout accepter » ; une étape verrouillée qu'on peut retirer ; un écart de l'IA dans un workflow régulé.
- Une donnée fictive, même pour remplir un état vide.

## 13. Les motifs repris de la recherche du 13/11, avec leurs sources

| # | Motif | Ce que TaskForce en prend | Où | Sources |
| --- | --- | --- | --- | --- |
| 1 | Une carte, des modes séparés | Une seule carte ; Run par défaut, Edit à part ; trois densités | §3, §8 | [Camunda, mode test](https://docs.camunda.io/docs/components/modeler/web-modeler/play-your-process/) ; [Tasklist](https://docs.camunda.io/docs/components/tasklist/userguide/using-tasklist/) ; [Optimize](https://docs.camunda.io/docs/components/optimize/userguide/process-analysis/report-analysis/compare-target-values/) ; [ServiceNow](https://www.servicenow.com/docs/r/yokohama/build-workflows/workflow-studio/process-automation-designer-lanes-activities.html) |
| 2 | L'état sur le nœud, peu d'états, seul le présent bouge | Dix états, une marque et un mot ; seul Working tourne ; une légende | §4.4 | [Operate, attentes](https://docs.camunda.io/docs/components/operate/userguide/view-wait-states/) ; [agents de Camunda](https://docs.camunda.io/docs/components/agentic-orchestration/monitor-ai-agents/) ; [ServiceNow](https://www.servicenow.com/docs/r/xanadu/customer-service-management/csm-playbook-layout.html) ; [Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-view-execution-details.html) ; [Unreal](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-debugging-example-in-unreal-engine) |
| 3 | « En attente d'une personne » à part, en tête | Needs you : son état, son compte, la tête des colonnes | §3, §4.5 | [Buildkite](https://buildkite.com/docs/pipelines/build-page) ; [Airflow](https://airflow.apache.org/docs/apache-airflow/stable/tutorial/hitl.html) ; [Zapier](https://help.zapier.com/hc/en-us/articles/38838306755981-Special-step-run-statuses-in-Human-in-the-Loop-actions) ; [Linear](https://linear.app/developers/agent-interaction) |
| 4 | L'étape déclare sa question, l'interface rend un contrôle typé | Les questions du brouillon et les tâches humaines en champs typés | §8 ; W5 | [Airflow](https://airflow.apache.org/docs/apache-airflow/stable/tutorial/hitl.html) ; [Prefect](https://www.prefect.io/docs/v3/advanced/interactive) ; [Argo](https://argo-workflows.readthedocs.io/en/latest/intermediate-inputs/) ; [LangChain](https://docs.langchain.com/oss/python/langchain/human-in-the-loop) |
| 5 | La règle se voit sur la décision | La règle, les signatures, l'échéance et ce qui suit, la signification de la signature | §6.1 | [Harness](https://developer.harness.io/docs/platform/approvals/adding-harness-approval-stages/) ; [GitHub](https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/review-deployments) ; [Airflow](https://airflow.apache.org/docs/apache-airflow/stable/tutorial/hitl.html) |
| 6 | Les opérations risquées dans un mode préparé | Le mode d'édition : un bandeau, les changements, la revue, la publication | §8 | [Operate, modification](https://docs.camunda.io/docs/components/operate/userguide/process-instance-modification/) ; [UiPath Maestro](https://docs.uipath.com/maestro/automation-cloud/latest/user-guide/process-overview-homepage) |
| 7 | De l'incident à la réparation sans quitter la carte | La cause et quoi faire sur le nœud ; « See why », « Try again » ; aucun faux vert | §4.5, §6.2 | [Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-view-execution-details.html) ; [Operate, incidents](https://docs.camunda.io/docs/components/operate/userguide/resolve-incidents-update-variables/) ; [ComfyUI](https://docs.comfy.org/interface/right-side-panel) ; [Make](https://help.make.com/manage-incomplete-executions) |
| 8 | Relancer depuis une étape, garder l'original | « Try again from {step} » ; le reste en W7 | §6.2 ; W7 | [Inngest](https://www.inngest.com/docs/platform/manage/rerun-function-runs) ; [LangGraph Studio](https://docs.langchain.com/langgraph-platform/use-studio) ; [n8n](https://docs.n8n.io/workflows/executions/debug/) |
| 9 | Suivre, aller à l'échec, éclairer le chemin | `j`, `k`, `f` ; les dépendances de la sélection seulement | §4.8, §6.3 | [Buildkite](https://buildkite.com/resources/blog/visualize-your-ci-cd-pipeline-on-a-canvas/) ; [Temporal](https://temporal.io/blog/lets-visualize-a-workflow) ; [ServiceNow](https://www.servicenow.com/docs/r/xanadu/customer-service-management/csm-playbook-layout.html) |
| 10 | Plusieurs vues, une sélection | La sélection dans l'adresse, la même dans les trois densités et dans la conversation | §2, §9 | [Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-view-execution-details.html) ; [Kestra](https://kestra.io/docs/ui/executions) ; [Buildkite](https://buildkite.com/docs/pipelines/build-page) |
| 11 | Un inspecteur ancré, pas une bulle | L'inspecteur à droite, quatre onglets | §5 | [Operate](https://docs.camunda.io/docs/components/operate/userguide/basic-operate-navigation/) ; [Inngest](https://www.inngest.com/docs/platform/monitor/traces) ; [Buildkite](https://buildkite.com/docs/pipelines/build-page) |
| 12 | La preuve accrochée au nœud | L'onglet Evidence ; le pied de la carte | §4.1, §5 | [Buildkite](https://buildkite.com/docs/pipelines/build-page) ; [Linear](https://linear.app/developers/agent-interaction) ; [GitHub](https://github.blog/ai-and-ml/github-copilot/how-to-orchestrate-agents-using-mission-control/) ; [Vercel](https://vercel.com/docs/deployment-checks) |
| 13 | La trace de l'agent dans son nœud | Le déroulé de la mission dans Activity, l'agent et son modèle sur la carte | §4.1, §5 | [agents de Camunda](https://docs.camunda.io/docs/components/agentic-orchestration/monitor-ai-agents/) ; [Linear](https://linear.app/developers/agent-interaction) |
| 14 | Lisible à des milliers de nœuds | Des colonnes, des sous-issues repliées, « Show {count} more », les arêtes à la sélection, la liste en étroit | §3, §10 | [Dagster](https://dagster.io/blog/scaling-dag-visualization) ; [Buildkite](https://buildkite.com/docs/pipelines/build-page) |
| 15 | La même carte pour améliorer, une ligne de santé | La ligne de la part faite dans l'en-tête ; la santé et les durées en W9 | §3 ; W9 | [Optimize](https://docs.camunda.io/docs/components/optimize/userguide/process-analysis/report-analysis/compare-target-values/) ; [Linear](https://linear.app/docs/initiative-and-project-updates) |

Le cadre vient des trois archétypes empilés de la même recherche : le tableau d'étapes vivant (ServiceNow, UiPath, Pega, Linear,
Airflow) pour les colonnes, les arêtes du graphe du travail (Dagster, Buildkite) à la sélection, les portes du plan de processus
(Camunda, Step Functions) en tête d'étape. Et de Claude : la conversation au centre et les volets à côté (Claude Code Desktop), les
applications vivantes dans la conversation (les connecteurs interactifs, MCP Apps), dont TaskForce prend la structure, jamais
l'identité (R119, R133).

## 14. Quand W1 est fini

Les critères du [plan des lots](./2026-11-13-le-workflow-pilotable-plan-des-lots.md), W1, rappelés : l'onglet et l'adresse ; des nœuds réels, comparés aux données de
l'API ; un accord décidé depuis un nœud, au dossier, parti de « Waiting for you » en moins de deux secondes ailleurs ; une dépendance
du board visible à la sélection ; les dix états et leur tri ; les trois densités et l'étroit ; l'objectif dit ou proposé ; aucun mot
interne, aucun symbole, aucune couleur sans mot ; la revue des écrans (R161), la relecture (R159), l'essai de la Présidence ; puis
E24.
