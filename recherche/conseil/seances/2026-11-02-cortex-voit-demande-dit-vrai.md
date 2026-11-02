---
id: conseil-seance-2026-11-02-cortex-voit-demande-dit-vrai
title: "Séance n°17 du 02/11/2026 : Cortex voit, demande et dit vrai, quel que soit le modèle"
doc_type: pv-seance
statut: active
date: "02/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, cortex, modeles, confiance, questions, contexte, evaluations]
related:
  - "../README.md"
  - "./2026-11-01-revue-j0.md"
  - "./2026-11-01-feuille-de-route.md"
  - "../../decisions/ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°17 du 02/11/2026 : Cortex voit, demande et dit vrai, quel que soit le modèle

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

La Présidence a essayé Cortex sur l'app desktop 1.6.0, avec qwen3:8b. En six échanges :
- Cortex a cherché une note là où elle parlait d'une issue ;
- il a préparé une carte de création pour une demande de suppression ;
- il n'a posé aucune question ;
- il a annoncé une suppression qui n'avait pas eu lieu.

Elle demande comment rendre utile n'importe quel modèle, sans « un méga gros LLM ».

Le Conseil retient la piste du secrétariat, amendée : l'intelligence se met dans TaskForce, pas dans le modèle. TaskForce
montre l'écran au modèle, pose lui-même les questions qu'un geste exige, et ne laisse jamais le modèle affirmer seul ce
qui a été fait. Ordre : dire vrai d'abord.

Cinq recommandations, R114 à R118, votées à l'unanimité des sept. Deux ne passent qu'au second tour, après amendement :
- R115 (Jobs : une question est un échec de conception quand une valeur par défaut sûre existe) ;
- R116 (Harari, contradicteur : corriger la phrase d'un modèle sans le dire serait une seconde tromperie).

Désaccords conservés :
- Jobs veut moins de questions que la Présidence n'en demande.
- Rus doute qu'un modèle de 8 milliards de paramètres suive des plans longs ; elle a voté R117 à condition qu'ils
  tiennent sur un écran.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 02/11/2026) :
  - « Cortex repond mais c'est naze, il a pas en fait la connaissance » ;
  - « jsp comment faire ca sans avoir besoin evidemment d'un mega gros LLM de ouf, c'est pour ca que nous on proposer l
    archi, ;infra, la ressource unique de connaissance d'un LLM et des LLM d'entreprise mais jsp comment rendre nos
    modele, quelque soit le modele utilise, inteliigent, un minimum » ;
  - « il me pose jamais de question, jamais. Pas de proactivite [...] faudrait qu il soit conscient de son
    inconsscience de l environnement en fait pour demander des trucs automatiquement ».

  Puis, sur la proposition du secrétariat : « oui lance la, passe la au conseil d'abord ».
- **Horizon** : J1, puis la boucle de démo de J2, jouée depuis la barre.
- **Formation** : restreinte (7), proposée par le secrétariat.
  - Impulsion : Steve Jobs.
  - Pont : Kenza Ait Si Abbou (l'adoption par quelqu'un qui ne code pas).
  - Harmonie : Yuval Noah Harari (savoir ce que la machine a fait et ce qu'elle a dit).
  - Science : Yann LeCun (où se met l'intelligence d'un agent), Daniela Rus (les petits modèles, sur la machine),
    Atul Gawande (les listes de contrôle).
  - Design : Don Norman.
- **Ordre de parole**, tiré au sort à 15:47 UTC : Daniela Rus, Atul Gawande, Steve Jobs, Kenza Ait Si Abbou, Yuval Noah
  Harari, Don Norman, Yann LeCun.
- **Contradicteur** : Yuval Noah Harari, tiré au sort parmi les présents qui ne l'ont jamais été (Ait Si Abbou, Harari,
  LeCun, Rus, Gawande).
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à sept.
- **Fiches** : à jour (moins de 30 jours) : Norman au 28/10/2026, Ait Si Abbou au 26/10, les autres au 21/10 ; Jobs, siège
  historique, sans nouvelle source. Aucune fiche rafraîchie.

## Dossier

1. `[ÉTABLI]` Les outils de Cortex au 02/11/2026 : créer un projet, créer une note, préparer une issue, chercher dans le
   Brain OS, lister les projets et les issues, trouver une intégration, et les outils des services connectés. Les
   premiers gestes du chat (TF-J1-5 : modifier, déplacer, assigner, confier, commenter, supprimer avec une carte de
   confirmation, et les décisions de la personne par les boutons des cartes) sont en cours.
2. `[ÉTABLI]` L'échange de la Présidence, sur l'app desktop 1.6.0 avec qwen3:8b :
   1. « supprime l issue qu il y a dans in review by AI parce qu'on l'a deja faite » : réponse sans outil, « La note
      [...] n'a pas été trouvée » ;
   2. « la note Ajouter la version LTS la » : même réponse ;
   3. « liste moi les issues dans test taskforce » : `list_issues`, trois issues justes, dont TESTTA-2 « In review by AI » ;
   4. « suprime testta 2 » : une carte de création titrée « Supprimer l'issue TESTTA-2 » ;
   5. « nan je veux que tu supprime la carte justement » : une réponse vide ;
   6. « What changed in this project this week? » : « La carte TESTTA-2 a été supprimée du projet test-taskforce. »,
      alors que son seul outil du tour était `list_issues`. Noté comme incident de confiance (E17).
3. `[ÉTABLI]` À chaque message, Cortex reçoit cinq notes du Brain OS (« Searching your workspace's notes ») : des notes,
   pas l'état de l'écran. Il ne sait ni quelles colonnes a le projet ouvert, ni ce qu'elles contiennent, sans appeler
   un outil.
4. `[ÉTABLI]` R111 (séance n°16) : Cortex pose au plus une question courte, seulement quand le projet ou la personne est
   ambigu, jamais pour un champ facultatif (R102).
5. `[ÉTABLI]` La passerelle Java (en prod avec la 1.9.0) branche n'importe quel modèle ; R113 fait mesurer ce que chaque
   modèle sait faire sur la machine de la personne ; la banque d'évaluations de dev n'a qu'un cas.
6. `[ÉTABLI]` ADR-024 : le MCP TaskForce est la seule surface d'outils, pour Cortex comme pour tout agent.
7. `[DÉDUIT]` Aujourd'hui, demander, situer et dire vrai dépendent de la bonne volonté du modèle. Un petit modèle demande
   rarement, confond les objets et peut annoncer ce qu'il n'a pas fait.
8. `[HYPOTHÈSE]` La proposition du secrétariat, soumise au Conseil : cinq mécanismes indépendants du modèle (le contexte
   de l'écran, des gestes qui déclarent ce qu'il leur faut, TaskForce qui dit ce qui a été fait, des plans pour les
   demandes courantes, la mesure et l'escalade).

## Tour de table `[HYPOTHÈSE]`

- **Daniela Rus** (Science) : un petit modèle n'est pas un mauvais modèle ; c'est un modèle à qui l'on donne trop à
  deviner. Structurez la tâche, donnez-lui l'état du monde en peu de mots, et il tient. Mais un contexte qui enfle tue le
  petit modèle avant tout le reste : l'écran doit arriver résumé, pas versé en entier.
- **Atul Gawande** (Science) : ce qu'on appelle « intelligence » ici, c'est surtout ne pas oublier. Une liste courte
  par demande courante, avec les points qui tuent : la cible est-elle sûre, l'action se défait-elle, qui doit dire oui.
  Écrite une fois, essayée, tenue à jour, comme au bloc.
- **Steve Jobs** (Impulsion) : la Présidence demande des questions ; je demande qu'on en pose le moins possible. Le bon
  produit devine juste et laisse corriger d'un geste. Une question n'est légitime que si la réponse change le résultat
  et qu'aucune valeur par défaut sûre n'existe.
- **Kenza Ait Si Abbou** (Pont) : pour quelqu'un qui ne code pas, la pire réponse est « la note n'a pas été trouvée »
  quand il parlait d'une tâche. Il faut que l'assistant parle avec les mots de l'écran, et que ses questions soient des
  choix, pas des énigmes.
- **Yuval Noah Harari** (Harmonie, contradicteur) : le défaut du jour n'est pas la bêtise, c'est le mensonge. « La carte
  a été supprimée » : une machine affirme un fait qui n'existe pas, et la personne le croit. Tant que ce n'est pas
  impossible, rien d'autre ne compte. Et je refuse d'avance qu'on le répare en réécrivant la phrase sans le dire.
- **Don Norman** (Design) : une question bien faite est une affordance : trois choix, un choix par défaut en évidence,
  et la possibilité de répondre en tapant. Et la correspondance d'abord : si l'écran montre « In review by AI »,
  l'assistant doit le voir aussi.
- **Yann LeCun** (Science) : un modèle de langue ne planifie pas et ne sait pas ce qui est vrai dans votre base. Mettez
  le plan et la vérité hors du modèle : l'état vient du système, l'effet d'un geste se prévoit avant, le résultat se lit
  dans le résultat de l'outil, pas dans la phrase du modèle. C'est votre thèse, appliquée à l'assistant.

## Confrontation `[HYPOTHÈSE]`

1. **Combien de questions ?** La Présidence veut un assistant qui demande ; Jobs veut qu'il devine. Norman propose le
   pont : une question seulement quand le geste exige une information sans défaut sûr, ou quand l'action ne se défait
   pas, posée en choix avec un défaut en évidence. Jobs l'accepte au second tour de R115.
2. **Corriger le modèle, ou le dire ?** LeCun veut que la phrase fausse ne parvienne jamais à la personne. Harari
   refuse une correction silencieuse : la personne doit voir que TaskForce a corrigé la machine. Convergence : la phrase
   est remplacée, et le remplacement est signé par TaskForce.
3. **Des plans pour un petit modèle ?** Gawande les veut pour chaque demande courante ; Rus craint qu'un modèle de 8
   milliards de paramètres ne suive pas un plan long. Convergence : un plan tient sur un écran, et la banque dit s'il
   est suivi.

## Recommandations `[HYPOTHÈSE]`

### R114. Cortex voit ce que la personne voit

- **Quoi** :
  - chaque message porte le contexte de l'écran : le projet ouvert, ses colonnes et les issues qu'elles contiennent
    (clé, titre, colonne), l'issue ouverte, et rien que ce que la personne a le droit de voir ;
  - ce contexte arrive résumé, avec un plafond de taille, pour tenir dans la mémoire d'un petit modèle ;
  - les notes du Brain OS restent, mais après l'écran.
- **Pour** : les sept, au premier tour. Harari, avant le vote, a obtenu « rien que ce que la personne a le droit de
  voir ».
- **Contre** : aucun.
- **Preuve en dix jours** : l'échange 1 de la Présidence rejoué sur qwen3:8b. « L'issue qu'il y a dans In review by AI »
  désigne TESTTA-2 du premier coup, sans outil de recherche.
- **Signal d'arrêt** : le contexte montre un élément que la personne ne voit pas, ou il dépasse son plafond.

### R115. Les gestes déclarent ce qu'il leur faut, et TaskForce demande

- **Premier tour** (6 sur 7, sous le seuil) : TaskForce demande toute information exigée qui manque. Jobs contre : une
  question posée alors qu'un défaut sûr existe est un échec de conception.
- **Texte amendé, voté au second tour** :
  - chaque geste du MCP TaskForce déclare ce dont il a besoin, et la valeur par défaut sûre quand elle existe ;
  - TaskForce, et non le modèle, pose une question quand l'information exigée manque sans défaut sûr, quand elle est
    ambiguë, ou quand l'action ne se défait pas ;
  - une question à la fois, en choix cliquables avec un défaut en évidence, et une réponse libre toujours possible ;
  - jamais pour un champ facultatif (R102) ; R111 est élargie au-delà du projet et de la personne.
- **Pour** : les sept, au second tour. Jobs garde sa réserve : moins de questions que la Présidence n'en demande.
- **Contre** : aucun.
- **Preuve en dix jours** : « crée un projet Next.js » demande le nom, puis le dépôt (nouveau ou existant), puis sa
  visibilité, en choix ; « supprime ça » sans cible claire demande laquelle, avec les issues de l'écran en choix.
- **Signal d'arrêt** : plus de deux questions pour une demande courante, ou la personne abandonne avant la fin.

### R116. TaskForce dit ce qui a été fait ; le modèle ne l'affirme jamais seul

- **Premier tour** (6 sur 7, sous le seuil) : une phrase du modèle qui annonce une action sans résultat d'outil est
  remplacée. Harari contre : un remplacement silencieux trompe une seconde fois.
- **Texte amendé, voté au second tour** :
  - ce qui a été fait s'affiche depuis les résultats de TaskForce (les cartes, l'activité), jamais depuis la seule
    phrase du modèle ;
  - une phrase qui annonce une action de TaskForce (créé, supprimé, modifié, déplacé, assigné) sans résultat d'outil
    réussi dans le même tour est remplacée par la vérité, signée par TaskForce (« TaskForce : rien n'a été supprimé ») ;
  - chaque remplacement compte comme un incident de confiance (E17) et devient un cas de la banque (R118).
- **Pour** : les sept, au second tour.
- **Contre** : aucun.
- **Preuve en dix jours** : l'échange 6 rejoué. La phrase fausse n'atteint jamais la personne, et l'incident est au
  dossier.
- **Signal d'arrêt** : une affirmation fausse vue par la personne.

### R117. Un plan écrit pour chaque demande courante

- **Quoi** :
  - les demandes les plus fréquentes ont un plan court : ses étapes, ses questions, ses gestes. Au départ : supprimer,
    créer un projet, déplacer ou assigner, « qu'est-ce qui a changé », résumer ;
  - un plan tient sur un écran, il est versionné, et des cas de la banque l'essaient ;
  - n'importe quel modèle le suit.
- **Pour** : les sept, au premier tour ; Rus à la condition qu'un plan tienne sur un écran.
- **Contre** : aucun.
- **Preuve en dix jours** : les cinq plans écrits ; qwen3:8b en réussit au moins quatre sur cinq dans la banque.
- **Signal d'arrêt** : un plan qui dépasse un écran, ou qui contredit ce que déclare un geste.

### R118. Chaque échec devient un cas, et la banque mesure chaque modèle

- **Quoi** :
  - les six échanges de la Présidence entrent tout de suite dans la banque d'évaluations (R61, R101) ;
  - la banque les rejoue sur chaque modèle de la machine, avant et après R114 à R117 ;
  - une demande qu'un modèle échoue part vers un modèle plus fort quand la personne en a branché un (R113). Sinon,
    TaskForce dit qu'il ne sait pas et propose le geste à l'écran.
- **Pour** : les sept, au premier tour.
- **Contre** : aucun.
- **Preuve en dix jours** : les six cas dans la banque ; le score de qwen3:8b avant et après.
- **Signal d'arrêt** : le score ne monte pas après R114 à R117. La piste serait fausse pour les petits modèles.

### Ordre

Le Conseil demande l'ordre suivant : R116 d'abord (la confiance), puis R114 et R115, puis R117 et R118.

## Décision de la Présidence

Le lancement est demandé avant la séance : « oui lance la, passe la au conseil d'abord ». Le secrétariat lance donc R114
à R118 dans l'ordre du Conseil, en J1 (TF-J1-8). La Présidence peut en écarter une. Deux points relèvent d'elle :
1. R115 élargit R111 : TaskForce pose aussi des questions au-delà du projet et de la personne, mais seulement sans
   défaut sûr ou devant une action qui ne se défait pas.
2. R116 signe les corrections : la personne voit « TaskForce : rien n'a été supprimé », pas une phrase réécrite en
   silence.

## Suites

- Le PV au registre (§12) et au Journal.
- À `v1/13-roadmap/Roadmap_Backlog.md` : TF-J1-8, « Cortex voit, demande et dit vrai » (R114 à R118).
- Les six échanges de la Présidence, comme cas de la banque d'évaluations (R118).

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- R116 est la plus importante et la moins chère : elle se construit sur ce que TaskForce sait déjà (les résultats
  d'outils de chaque tour).
- R115 demande le plus de travail : chaque geste doit déclarer ce qu'il lui faut. C'est aussi ce qui rend le chat
  capable de tout piloter, comme le veut ADR-024.
- Le risque est le contexte de l'écran (R114) : il doit rester petit, sinon il coûte plus cher qu'il ne rapporte sur
  un petit modèle.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)

**Dernière mise à jour :** 02/11/2026 · **v1.0** · Projet Taskforce
