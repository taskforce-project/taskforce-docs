---
id: conseil-seance-2026-10-29-atelier-design-carte
title: "Séance n°9 du 29/10/2026 : l'atelier design n°2, l'écran d'arrivée et la carte des workflows"
doc_type: pv-seance
statut: active
date: "29/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, ux, workflows, cortex, harnais]
related:
  - "../README.md"
  - "./2026-10-28-atelier-design.md"
  - "./2026-10-29-recette-132.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°9 du 29/10/2026 : l'atelier design n°2, l'écran d'arrivée et la carte des workflows

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

La Présidence demande à l'équipe UI/UX de Jobs de dessiner l'app :
- ce qu'on voit en arrivant, et le layout ;
- les workflows principaux ;
- pour chacun, ce que fait la personne et ce qui se passe en même temps sans qu'elle le voie.

Elle veut une carte complète, et un écran d'arrivée innovant, qui ne soit pas un tableau de bord de suivi.

L'atelier part d'un fait : aujourd'hui, l'app s'ouvre sur un tableau de bord de cartes de suivi. Il propose une autre
arrivée, sur une seule phrase (« Quel résultat voulez-vous ? »). Ce qui attend la main de la personne y forme une pile
qui se vide. Ses résultats y sont placés dans le temps, autour d'une ligne « maintenant ». Et l'objet ouvert est à droite,
avec Cortex.

Le travail invisible des agents s'y voit en une ligne sur son objet, jamais dans un écran de monitoring. L'atelier
dessine sept workflows en diagrammes de séquence, sur la [carte](https://claude.ai/artifact/CzYEJ2xV4kHQpPzWCd8y4x) :
arriver, décrire un résultat, confier, répondre à une demande, juger, demander à Cortex, et quand ça casse.

Il formule cinq recommandations, R55 à R59, en attente de la décision de la Présidence.

Désaccord conservé : Saarinen, contradicteur, tient que la ligne du temps se périmera comme tous les diagrammes de Gantt.
Pour lui, la liste triée est la vérité, et le temps doit rester une vue.

- **Saisine** (Présidence, 29/10/2026) : « niveau interface ils voient tout ça comment la team Jobs UI/UX ? Genre
  dessinez-moi les workflows principaux, on arrive sur l'app qu'est-ce qu'on voit, c'est quoi le layout, faut que ce
  soit innovant, pas un simple dashboard de monitoring ». Puis : « que fait l'utilisateur, qu'est-ce qu'il se passe en
  même temps qu'il ne voit pas ». Et enfin : « un schéma vraiment poussé, très complet même si c'est complexe, je veux
  tout cartographier ».
- **Formation** : restreinte (5), l'équipe que la Présidence nomme : Steve Jobs (mène l'UX), Don Norman, Karri Saarinen
  et Julie Zhuo (pôle Design), et Tristan Harris (Harmonie), comme au premier atelier.
  - Ordre de parole tiré au sort : Don Norman, Karri Saarinen, Steve Jobs, Tristan Harris, Julie Zhuo.
  - Contradicteur désigné : Karri Saarinen. Le contradicteur change à chaque séance, et Hamilton l'était à la n°8.
- **Fiches** : toutes à jour (moins de 30 jours). Jobs, siège historique, ne se rafraîchit que sur une nouvelle source
  historique.

## Dossier

1. `[ÉTABLI]` **L'arrivée aujourd'hui.**
   - `/{espace}` redirige vers `/dashboard` (`app/(protected)/[workspace]/page.tsx`). C'est un tableau de bord :
     - un bandeau (« Connect your tools ») ;
     - des colonnes rapides ;
     - une grille de cartes choisies : indicateurs, burndown, débit, charge, santé des opérations, usage de l'IA,
       graphique de l'IA, « needs attention » (`components/dashboard/cards`).
   - Le menu nomme jusqu'à seize entrées (`lib/constants_en.ts`) : Dashboard, My Queue, Signals, Operations, Issues,
     Sprints, Roadmap, Teams, Members, Skills, Intelligence, Agents, Messages, Discussions, Settings, Help.
2. `[ÉTABLI]` **Ce qui est retenu.**
   - J1 : dans Cortex, on demande et l'agent rend compte, mais on n'y décide pas.
   - J2 : les flows sont classés par la promesse, et le board marche.
   - J3 : une seule carte de résultat, sur l'issue.
   - J4 : la délégation se voit.
   - J5 : le mode dégradé dit la vraie cause.
   - J6 : un nom par chose.
   - J7 : Cortex ne retient pas.
   - R45 : on délègue dès la création.
   - R46 : un accord pour ce qui sort.
   - R47 : Cortex prépare l'issue entière en brouillon.
   - R48 : la colonne et l'échéance d'après le but et le temps. La Présidence : « c'est lui qui décide », « on n'oublie
     pas l'outcome ».
   - R50 : la revue dans TaskForce.
   - R54 : la refonte commence par créer, relire, accorder.
3. `[ÉTABLI]` **Ce qui tourne sans se voir** (le code du 29/10/2026).
   - **App desktop** : un backend Java et sa base Postgres en local, une passerelle IA (`desktop/src/ai.ts`) vers
     Ollama, et le runner, qui lance Claude Code avec git et gh.
   - **Web** : Next.js, le même backend Java, le service IA en Python (FastAPI) vers le fournisseur, Postgres avec
     pgvector, Redis (débit, cache) et Keycloak.
   - **Temps réel** : par STOMP (`use-stomp.ts`).
   - **Le noyau du harnais** : le contrat (`contracts/`), le moteur de règles (TypeScript dans le runner, Java au
     serveur) et la chaîne de preuve.
   - **La boucle du runner** : réclamer une mission, contrôler son poste chaque minute, juger chaque action par les
     règles, attendre un accord dix minutes au plus, lancer les tests du projet (S1), pousser puis ouvrir la pull request
     selon les règles.
   - **La boucle de Cortex** : cinq tours d'outils au plus, les outils internes et douze outils externes au plus, la
     garde de débit, le contrôle d'honnêteté. Ses écritures ne passent pas encore par le noyau (séance n°8).
4. `[ÉTABLI]` **Le temps dans les données.**
   - Une issue porte une échéance, une date de début et des points.
   - Un cycle porte ses dates et son état.
   - Une colonne porte sa catégorie (Backlog, à faire, en cours, terminée, annulée).
   - Un projet n'a ni but ni date de fin : sa description en tient lieu (`list_projects`, R48).
5. `[ÉTABLI]` **Le cadre de la Présidence** : innovant, pas un tableau de bord de suivi ; le résultat d'abord ; Cortex
   décide du placement dans le temps et demande s'il doute.

## Tour de table `[HYPOTHÈSE]`

- **Don Norman** (Design) : la personne doit toujours savoir ce que fait le système, sans le surveiller.
  - Un tableau de bord de cartes demande d'interpréter des courbes pour savoir quoi faire : c'est un écart d'évaluation
    à la charge de la personne.
  - L'arrivée doit répondre à deux questions sans effort : qu'est-ce qui attend ma main, et où en sont mes résultats.
  - Le temps est une bonne correspondance, si elle est naturelle : la gauche pour le passé, la droite pour l'avenir, une
    ligne « maintenant ».
  - Chaque mission invisible laisse un signe sur son objet en moins d'une seconde. Ce qui se défait se défait d'un geste.
- **Karri Saarinen** (Design, contradicteur, conflit déclaré : Linear) : il attaque le consensus qui se forme, « une
  ligne du temps en page d'accueil ».
  1. Les diagrammes de Gantt se périment : personne ne tient les dates, et l'écran ment en silence.
  2. La vérité d'un outil de travail, c'est une liste triée, rapide, au clavier. Le temps doit rester une vue qu'on
     choisit.
  3. Si la ligne du temps reste, alors pas une date posée à la main : Cortex place, replace et montre son incertitude, en
     plage, pas en point.
  4. La pile « maintenant » est une bonne idée si elle reste petite, et chaque élément se traite sans quitter l'écran.
- **Steve Jobs** (Impulsion, mène l'UX, siège historique) : la Présidence a raison, une page d'accueil de courbes est un
  aveu, celui de ne pas savoir quoi faire pour la personne.
  - Une seule phrase en bas de l'écran, toujours là : « Quel résultat voulez-vous ? ». C'est le produit.
  - Au-dessus, deux choses seulement : ce qui vous attend, et vos résultats dans le temps.
  - Il dit non :
    - aux seize entrées du menu : il en garde cinq, Résultats, Agents, Connaissances, Équipe, Réglages ;
    - aux cartes d'indicateurs sur l'accueil ;
    - à un écran qui surveille les agents.
  - L'objet ouvert vient à droite, avec Cortex, comme on écrit à côté de son document.
- **Tristan Harris** (Harmonie) : ce que l'écran maximise décide de ce que la personne devient.
  - La pile « maintenant » est finie, et elle se vide : quand rien n'attend, l'écran le dit, « Rien ne vous attend. Trois
    agents travaillent. », et c'est tout.
  - Pas de pastille rouge qui compte, pas de fil infini, pas de relance.
  - Le temps rendu à la personne se mesure : les décisions prises à l'arrivée, pas le temps passé dans l'app.
- **Julie Zhuo** (Design, conflit déclaré : Meta) : partir du travail que la personne veut voir fait.
  - Le chemin est toujours le même : je veux un résultat, Cortex le découpe et le place, je confie, je réponds à ce qu'on
    me demande, je juge, j'applique.
  - L'arrivée montre ce chemin pour chaque résultat, en cours. Les sept workflows sont ses étapes.
  - Ce qui se passe sans qu'on le voie doit être dessiné aussi précisément que ce qu'on voit, sinon l'équipe produit
    construit des écrans qui mentent.

## Confrontation `[HYPOTHÈSE]`

1. **La ligne du temps à l'accueil, ou la liste.**
   - Saarinen : la liste est la vérité, le temps une vue.
   - Norman et Zhuo : le résultat et l'échéance sont la question de la personne ; la liste n'y répond pas d'un coup
     d'œil.
   - Jobs : la ligne du temps, si personne n'y pose de date à la main.
   - Issue : R56, la ligne du temps est calculée par Cortex (R48), avec des plages et non des points ; la liste reste à
     une touche. Saarinen maintient son objection.
2. **La pile « maintenant » : une boîte de réception de plus, ou la fin des boîtes.**
   - Harris : finie, vide quand rien n'attend.
   - Saarinen : chaque élément se traite sur place.
   - Jobs : elle remplace Signals et My Queue sur l'accueil, elle ne s'y ajoute pas.
   - Issue : R55.
3. **Une phrase en bas de l'écran, ou la palette de commandes.**
   - Saarinen : la palette au clavier est plus rapide.
   - Jobs : une phrase visible, et la palette pour qui la connaît.
   - Issue : les deux, la palette s'ouvrant sur la même phrase (D3).

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R55 (R54 est la dernière existante). Chacune porte qui la soutient, qui s'y oppose, sa preuve en
dix jours et son signal d'arrêt.

### R55. L'arrivée : une phrase, ce qui vous attend, vos résultats dans le temps

- **En bas, toujours** : la boîte « Quel résultat voulez-vous ? ». Cortex y prépare l'issue entière (R47).
- **Au centre, à gauche** : « Maintenant », une pile finie de ce qui attend la main de la personne. On y trouve les
  demandes d'accord, les résultats prêts à juger, les mentions et les échéances du jour. Chaque élément se traite sur
  place ; vide, l'écran le dit.
- **Au centre** : la ligne des résultats (R56).
- **À droite** : l'objet ouvert et Cortex, côte à côte (D2).
- **À gauche** : cinq entrées, Résultats, Agents, Connaissances, Équipe, Réglages. La recherche et la palette sont à une
  touche.
- Les cartes de suivi quittent l'accueil.

- **Pour** : Jobs, Norman, Zhuo, Harris.
- **Contre** : Saarinen, sur la ligne du temps à l'accueil (R56).
- **Preuve en dix jours** : la maquette cliquable de l'arrivée, jugée par la Présidence sur ses vrais projets. En moins
  de dix secondes, elle dit ce qui l'attend et où en sont ses résultats.
- **Signal d'arrêt** : la Présidence ouvre un autre écran pour savoir quoi faire.

### R56. Le résultat porte un but et une date ; Cortex le place dans le temps

- Un projet devient un résultat : un but en une phrase, une date visée, des critères de réussite. Le modèle de données
  ne les a pas encore (dossier, point 4).
- La ligne du temps se calcule : Cortex place et replace les issues d'après le but, les cycles, les échéances et les
  estimations (R48). Personne n'y pose de date à la main.
- L'avance ou le retard se voit par la forme (une plage qui dépasse la date visée), jamais par un chiffre.
- La liste et le board restent des vues du résultat, à une touche (J2).

- **Pour** : Jobs, Norman, Zhuo.
- **Contre** : Saarinen : le temps doit rester une vue ; des dates calculées sont fausses avec aplomb. Harris, en
  partie : pas de rouge qui alarme.
- **Preuve en dix jours** : les projets de la Présidence placés par Cortex. Elle corrige moins d'un placement sur cinq.
- **Signal d'arrêt** : la Présidence déplace les éléments à la main plus souvent qu'elle ne les lit.

### R57. L'invisible se voit en une ligne, sur son objet

- Chaque mission a un pouls sur l'issue qu'elle sert : l'étape en cours, mise à jour en continu, dans les mots de R22.
  On en compte quatre états : au travail, en attente de vous, en échec, terminé (J4).
- Le détail est dans le dossier, déplié à la demande. Aucun écran ne surveille les agents.
- Quand quelque chose casse, le bandeau du mode dégradé (J5) se pose sur l'objet concerné et dit la vraie cause.

- **Pour** : tous.
- **Preuve en dix jours** : une mission suivie du début à la fin sans quitter l'issue ni ouvrir AI Workflows.
- **Signal d'arrêt** : la Présidence cherche un écran de monitoring pour savoir où en est un agent.

### R58. La carte des sept workflows est la référence de la refonte

- La [carte](https://claude.ai/artifact/CzYEJ2xV4kHQpPzWCd8y4x) dessine sept workflows en diagrammes de séquence :
  - arriver ;
  - décrire un résultat ;
  - confier ;
  - répondre à une demande ;
  - juger et décider ;
  - demander à Cortex ;
  - quand ça casse.
- Chaque diagramme a sept acteurs : la personne, l'interface, Cortex, le noyau du harnais, le serveur TaskForce, le
  runner et l'agent, l'extérieur. Il distingue ce qui existe de ce qui est proposé.
- Chaque écran de la refonte se dessine depuis ces diagrammes et se teste contre eux. Un écran qui contredit un diagramme
  corrige l'un des deux, par écrit.

- **Pour** : tous.
- **Preuve en dix jours** : les écrans « créer », « relire » et « accorder » (R54) dessinés depuis la carte, et la
  recette suivante écrite depuis elle.
- **Signal d'arrêt** : un écran construit sans son workflow sur la carte.

### R59. Le noyau dessiné au centre, et Cortex dedans

- Sur la carte, toutes les actions passent par le noyau : les faits, les règles, la décision, le dossier, puis l'effet.
  Cela vaut pour celles des agents et pour celles de Cortex. Le chemin de Cortex est dessiné comme il sera, une fois
  branché (séance n°8).
- Le noyau ne se montre jamais à la personne sous ce nom (R22, J8). Elle en voit les effets : la demande d'accord, la
  carte de résultat, le dossier.

- **Pour** : Jobs, Norman, Zhuo, Harris.
- **Contre** : aucun. Réserve de Saarinen : un dessin n'est pas une architecture ; il faut le tenir à jour avec le code.
- **Preuve en dix jours** : le branchement de Cortex sur le noyau livré, et le diagramme « demander à Cortex » vrai au
  code.
- **Signal d'arrêt** : un écart entre le diagramme et le code, découvert en recette.

## Décision de la Présidence (29/10/2026)

Toutes les recommandations sont retenues telles que le Conseil les a formulées : « on suit le conseil sur tout, go »,
après la séance n°10. L'objection de Saarinen, contradicteur, reste au PV sans être retenue.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R55 à R59 | Retenues | « on suit le conseil sur tout » |

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 29/10 à 16:57 UTC (`shuf`). Contradicteur désigné : Karri Saarinen.
- **Formation** : cinq membres de trois pôles ; Pont et Science manquent, contre la règle d'un membre par pôle (§5). Le
  premier atelier l'avait noté de même : c'est l'équipe que la Présidence nomme pour l'interface.
- **La carte** est dessinée par le secrétariat depuis le tour de table et le code.
  - Ce qui existe est lu dans le code du 29/10/2026.
  - Ce qui est proposé est marqué « proposé » sur chaque diagramme.
  - Les noms d'écran et les libellés en anglais y sont des propositions, à relire pour le glossaire de R22.
- **Extrapolations** :
  - Les cinq entrées du menu et la phrase « Quel résultat voulez-vous ? » sont des propositions de Jobs simulé.
  - La position de Saarinen sur les diagrammes de Gantt est dans son champ (l'interface d'un outil de travail), sans
    citation.
- **Anachronismes** : Jobs (mort en 2011) ne connaît les agents de 2026 que par le dossier.

## Suites

- Ce PV ; une ligne au registre de la charte (§12) et le récit au [Journal](../../Journal.md), après la décision.
- Produit, après la décision : R56 demande une migration (le but, la date visée et les critères d'un projet). Les écrans
  de R54 se dessinent depuis la carte.
