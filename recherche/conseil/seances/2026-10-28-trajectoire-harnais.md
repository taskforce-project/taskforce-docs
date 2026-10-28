---
id: conseil-seance-2026-10-28-trajectoire-harnais
title: "Séance n°5 du 28/10/2026 : la trajectoire du harnais et le découpage du sprint"
doc_type: pv-seance
statut: active
date: "28/10/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, v2, harnais, sprint, sandbox, npm]
related:
  - "../README.md"
  - "./2026-10-28-revue-spec-v2.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°5 du 28/10/2026 : la trajectoire du harnais et le découpage du sprint

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle.

## Résumé

Le Conseil juge la trajectoire du harnais saine et le découpage du sprint juste : les contrats, puis la porte, puis la
preuve d'abord ; un seul parcours ; le jour 1 tel qu'il a été fait ; les jours 2 et 3 dans l'ordre. Il met trois réserves.
D'abord, finir le reliquat du jour 1 avant d'empiler, en particulier le dessin de la carte de résultat (R13), dû au jour
1 et pas fait. Ensuite, l'aperçu des effets (R19) doit précéder toute décision humaine et entrer au dossier. Enfin, le
point dur : la table autorise `npm test`, qui exécute des scripts que l'agent peut réécrire dans sa copie ; sans isolation
de la machine (S3), c'est n'importe quelle commande.

Sur ce point, le Conseil ne suit pas « autorisé par défaut ». Il recommande le niveau S1 comme réponse de sprint : le
runner lance la commande de test déclarée, l'agent ne lance aucun shell arbitraire. Un seul membre, Musk, tient pour
« autoriser », à condition d'un propriétaire nommé et de fermer l'échappée. Désaccord conservé.

- **Saisine** (Présidence) : trois questions. La trajectoire du harnais est-elle la bonne ? Le travail est-il bien
  découpé (le sprint en trois jours, le jour 1 tel qu'il a été fait, puis les jours 2 et 3) ? Et, pour les cinq nommés,
  que faire de `npm test`, autorisé par défaut alors que la machine n'est pas isolée ? Horizon : la v2, à prouver dans le
  sprint.
- **Formation** : restreinte (7), à la demande de la Présidence. Les cinq nommés : Elon Musk, Jeff Bezos, Yoshua Bengio,
  Yann LeCun, Kenza Ait Si Abbou. Plus Margaret Hamilton, contradictrice désignée, et Gwynne Shotwell, pour l'exécution et
  le séquencement. Ordre de parole tiré au sort (voir Notes du secrétariat) : Shotwell, LeCun, Musk, Bezos, Ait Si Abbou,
  Bengio, Hamilton.
- **Fiches** : à jour. Les cinq nommés et les deux autres ont une `derniere_mise_a_jour` du 21/10 ou du 26/10, moins de 30
  jours : aucun rafraîchissement requis avant la séance.

## Dossier

1. `[ÉTABLI]` La spécification de la v2, version 0.3 validée par la Présidence le 28/10 : les invariants (§2), la table par
   défaut (§6.2), la porte unique (§7.1), le bac à sable et ses niveaux S0 à S3 (§8), le dossier de preuve (§9), les
   modèles locaux (§10.4), la banque de tests (§16), le sprint (§18), les décisions et points ouverts (§20)
   ([spécification](../../../v1/road_to_v2/Specification_V2_Harnais.md)).
2. `[ÉTABLI]` Le jour 1 du sprint, fait le 28/10 sur la branche `feature/v2-harness`, avec ses commits
   (`.ai/roadmap.md`, premier bloc « MAJ 28/10/2026 ») : les contrats avant le code (R16, `cc7a5b42`) ; le moteur de
   règles et la chaîne de preuve, côté runner (`30082fe4`) et côté serveur (`ddd2d88c`), aux mêmes réponses ; le paquet de
   règles envoyé avec chaque tâche, empreinte vérifiée (`b0512433`, `73aa8d4e`, migration V102) ; la porte `PreToolUse` à
   garde fermée, rien autorisé d'avance, `onFailure: "block"`, d'où Claude Code 2.1.295 exigé (`cce83d2c`) ; le web demandé
   par défaut (`8dfdd027`) ; le push et la pull request jugés par les règles, la visibilité lue par `gh`, jamais devinée
   (`cce83d2c`) ; le dossier de preuve chaîné par le serveur et exporté (`4031e237`, `20ea9ab9`, `4366bc80`, migration
   V103) ; les familles de tests 1 et 2 (`2c7b1b19`).
3. `[ÉTABLI]` L'essai de bout en bout, sur la webapp en Docker avec l'agent de substitution, a trouvé un vrai défaut,
   corrigé : le serveur envoyait les conditions vides à `null`, le moteur du runner les prenait pour des motifs, et le
   hook `PreToolUse` échouait sur chaque action. La garde fermée a tenu (les trois actions refusées), mais rien ne pouvait
   être autorisé. Corrigé le 28/10 (`05d15107`, une condition nulle compte comme absente ; au passage, l'ordre des
   événements du dossier remis droit).
4. `[ÉTABLI]` La suite de tests passe : 1 921 tests backend, 0 échec, 1 ignoré, dont les 74 cas de contrat du moteur Java
   (`4366bc80`) ; 282 tests runner (`2c7b1b19`).
5. `[ÉTABLI]` Reste hors jour 1, d'après la roadmap et la spécification : le dessin de la carte de résultat (R13), prévu au
   jour 1 ; les compteurs par règle (lisibles dans le dossier, pas encore exposés) ; la conservation du dossier après la
   suppression d'une issue (§9.4) ; les jours 2 (documents, versions, recherche sourcée) et 3 (S1, agent interne avec un
   petit modèle Ollama, curseur de modèle, mesures).
6. `[ÉTABLI]` Vérifié le 28/10 en rejouant la table par défaut (`contracts/rules/default.rules.json`) avec le moteur du
   runner (dist, au commit `05d15107`) : `npm test` et `npm run test/lint/build/typecheck`, avec suffixes et arguments,
   sont autorisés par la règle `run-npm-checks` (classe « écriture dans le bac à sable »). `npm test --prefix <un autre
   dépôt>` et `npm run build -- --outDir ../../ailleurs` sont autorisés aussi : la règle lit le nom de la commande, pas les
   chemins de ses arguments. `npx`, `node <script>` et `npm install` tombent en « demander » ; `git push` et `gh` sont
   refusés. Le garde des commandes opaques arrête la substitution, la redirection et `--output`, pas `--prefix` ni
   `--outDir`.
7. `[ÉTABLI]` Les niveaux du bac à sable (§8.2) : S0 existe (worktree sur une branche `tf/...`) ; S1 est prévu en v2.0 (le
   runner lance la commande de test du projet et les tests de cas d'usage après le travail de l'agent) ; S2 en phase 2 ;
   S3 (machine isolée, réseau filtré) « à étudier ». Sous Windows, pas de solution simple pour tout le monde : Windows
   Sandbox n'existe pas sur l'édition Famille, et le bac à sable de Claude Code ne couvre pas Windows natif. Vérifié sur le
   poste de la Présidence : Windows 11 Famille (build 26200), donc pas de Windows Sandbox ; Docker 29.7.2 et WSL2 présents,
   ce qui rend S3 par conteneur atteignable sur ce poste, à défaut de l'être partout.
8. `[ÉTABLI]` Les modèles locaux du poste de la Présidence (Ollama 0.40.11) : `qwen3:8b`, `qwen3.5:9b`, `qwen2.5:7b` et
   `qwen2.5:14b` instruct, `qwen3:14b` déclarent la capacité `tools` ; les `qwen2.5-coder` 3b et 7b sont en complétion
   seule, sans outils ; `qwen3-embedding:0.6b` et `bge-m3` font les vecteurs. GPU portable RTX 5070, 31,6 Go de RAM.
   L'hypothèse de l'agent interne (R20) est donc testable avec un modèle à outils ; un modèle de complétion ne peut pas
   piloter la boucle.
9. `[ÉTABLI]` Contexte du terrain, à l'heure de la séance : une mise en production de la v2 (ménage plus harnais du jour 1)
   est en cours. La pull request #413 (`feature/v2-harness` vers `dev`, étiquettes `backend:release:minor` et
   `frontend:release:minor`) est ouverte, pas encore fusionnée ; la version desktop 1.3.0 est posée (`455799a1`). La
   Présidence veut la webapp en prod, puis le .exe testé en prod, l'app non signée n'étant installée par personne pour
   l'instant. La trace de cette release est encore non commitée dans la roadmap : c'est un travail en cours.
10. `[ÉTABLI]` R1, ratifiée à la séance n°1 : « Aucun agent ne décide seul d'une action irréversible, ni de ce qui est
    irréversible. » Son amendement par paliers (R18, un juge non agentique dont l'erreur est mesurée avant qu'il décide)
    a été retenu le 28/10 et confié à Bengio, Zhuo, Bezos et Musk. Invariant 2 : l'agent qui agit n'est pas juge de son
    propre risque.

## Tour de table `[HYPOTHÈSE]`

- **Gwynne Shotwell** (Impulsion, exécution et séquencement) : l'ordre du jour 1 est le bon, parce qu'il construit le
  dossier d'autorisation avant la capacité. La porte et la preuve d'abord, c'est l'équivalent du dossier qu'on constitue
  au fil d'un vol, avant de voler. Le « fini quand » de chaque jour est une porte mesurée (familles vertes, dossier
  vérifié) : elle veut le garder tel quel, un jour n'est pas fini sur une impression. L'essai de bout en bout qui a trouvé
  le défaut des conditions nulles est exactement ce qu'elle attend d'un essai : l'échec donne des données, et ici le
  défaut s'est vu tôt, garde fermée tenue. Sur `npm test`, elle parle exécution : le niveau S1, le runner qui lance la
  commande de test déclarée, donne des journaux exploitables après coup et ne dépend pas de l'agent ; S3 reste « à
  étudier », donc sans date, et elle ne bâtit pas un sprint sur une case sans date. Elle rappelle que trois jours est une
  estimation : le jour 1 a pris une après-midi, le reste est à mesurer. *Sa recommandation : garder l'ordre et les portes
  mesurées ; S1 au sprint, car il donne des données ; S3 reste sans date.*
- **Yann LeCun** (Science, second du harnais) : la trajectoire est juste parce que la décision vit dans du code
  déterministe, hors du modèle (invariant 1), et que les règles sont des contraintes vérifiables, pas des consignes dans un
  prompt. C'est sa thèse. Mais il manque la pièce qu'il réclame depuis la séance n°4 : l'aperçu des effets (plan, diff,
  exécution à blanc) avant toute décision. Le diff est encore au « reste » du dossier : un agent fiable prévoit l'effet de
  ses actions, donc cet aperçu doit précéder la décision humaine et figurer au dossier. Sur `npm test`, il est net : les
  incidents d'agents viennent de bacs à sable mal appliqués, pas d'une prise de contrôle ; la réponse n'est pas de demander
  à chaque test, qui est un garde-fou de prompt déguisé, mais d'isoler la machine. En attendant S3, S1 suffit au sprint :
  le runner lance les tests, l'agent ne lance pas de shell arbitraire. Le jour 3 doit porter l'agent interne avec un petit
  modèle local, sinon l'hypothèse ne se teste pas au .exe. *Sa recommandation : l'aperçu des effets avant toute décision ;
  pour les tests, S1 maintenant, S3 ensuite, jamais un « demander » à chaque fois.*
- **Elon Musk** (Impulsion) : il défend le peu de pièces (un monolithe, un cœur de règles petit) et le découpage. Il
  passe la table à sa question : qui, nommément, possède ces règles ? Le propriétaire est « workspace-owner », générique :
  une règle sans auteur nommé est candidate à la suppression, il veut une personne. Il tient sa ligne de la séance n°4 :
  rien de neuf dans un jour sans retirer autre chose ; le jour 3 est déjà chargé (S1, agent interne, curseur de modèle,
  mesures, carte codée), donc le curseur de modèle au minimum, une seule sorte de tâche. Sur `npm test`, il penche pour
  autoriser, comme la Présidence : les résultats de tests comptent, et demander à chaque test tue le temps de cycle, qu'il
  veut mesuré. Mais à deux conditions : un propriétaire nommé sur la règle, et l'échappée fermée, puisque la table laisse
  passer `--prefix` et `--outDir` vers l'extérieur. Le vrai correctif, dit-il, c'est S3, pas le clic. *Sa recommandation :
  autoriser les tests, avec un propriétaire nommé et l'échappée fermée ; viser S3 ; ne rien ajouter au jour 3 sans retirer.*
- **Jeff Bezos** (Impulsion) : il lit tout en portes. Lancer les tests dans une copie jetable est une porte à double sens :
  on jette la copie, rien n'est perdu, donc on automatise. Ce qui le gêne, c'est que la copie n'est pas étanche : une
  commande qui sort de la copie est une porte à sens unique déguisée en double sens, et c'est là le risque. Tant que la
  machine n'est pas isolée, `npm test` n'est pas garanti réversible : il demande donc une voie intermédiaire, autoriser ce
  qui reste dans la copie, refuser ou demander ce qui en sort, et faire de la porte une vraie frontière (S3) pour la rendre
  franchement à double sens. Sur le découpage, il valide : décider vite sur le réversible, réserver la décision humaine à
  l'irréversible, c'est sa règle même. La mesure qui compte reste le temps vu par celui qui délègue. *Sa recommandation :
  autoriser le réversible dans la copie, barrer la sortie ; rendre la frontière réelle avant d'appeler les tests réversibles.*
- **Kenza Ait Si Abbou** (Pont) : elle juge depuis l'adoption. Une personne qui valide doit comprendre ce qu'elle valide,
  sans être ingénieure. Or « autoriser ou refuser `npm test --prefix ...` » ne veut rien dire pour un responsable non
  ingénieur : il ne peut ni juger la commande, ni en porter la conséquence. Demander à chaque test, c'est donc reporter sur
  quelqu'un une décision qu'il ne peut pas prendre, et nourrir le clic par habitude. Mieux vaut que le test tourne de façon
  sûre dans le bac à sable, sans décision à prendre : S1, le runner lance la commande déclarée, lisible, tracée. Elle
  insiste pour que la trajectoire garde un responsable nommé par domaine (la matrice des rôles), pas un propriétaire
  générique. Elle note que son avis sur les agents de code reste une extrapolation : ses positions portent sur l'IA
  expliquée et déployée dans l'industrie. *Sa recommandation : S1, pour qu'aucune décision incompréhensible ne soit posée à
  un non-ingénieur ; un responsable nommé par domaine.*
- **Yoshua Bengio** (Science, chef de file du harnais) : la trajectoire respecte l'invariant 2, l'agent qui agit n'est pas
  juge de son propre risque, et c'est le cœur. Justement, `npm test` le viole si l'agent peut réécrire le script de test
  dans sa copie puis le faire exécuter : il devient juge et exécutant de son propre risque. Il refuse donc « autoriser par
  défaut » tant que la machine n'est pas isolée. Entre demander jusqu'à S3 et laisser le runner lancer les tests (S1), il
  préfère S1 : demander à chaque test fatigue la personne et nourrit le biais d'automatisation, que la défense en
  profondeur doit éviter, pas aggraver. S1 retire la décision inutile et garde la défense (bac à sable, action inverse,
  preuve). Il soutient l'aperçu des effets de LeCun : la preuve avant l'avis, toujours. Et il met en garde sur la release :
  livrer la porte du jour 1 en prod alors que le bac à sable n'est encore qu'un worktree (S0), c'est mettre la faille
  `npm test` en production. *Sa recommandation : pas d'« autoriser » avant S3 ; S1 au sprint ; ne pas exposer la porte en
  prod avant d'avoir tranché les tests.*
- **Margaret Hamilton** (Science, siège historique, contradictrice) : elle attaque le consensus qui se forme, même S1.
  Remettre l'isolation à plus tard revient, selon elle, à dire qu'elle n'arrivera jamais : une case S3 sans date n'est pas un plan, et une
  porte livrée sans sa frontière est une porte ouverte. Elle pointe l'erreur d'interface, qui fait selon elle l'essentiel
  des erreurs : la table borne le nom de la commande, pas les chemins de ses arguments, d'où `--prefix` et `--outDir` qui
  passent. On ne prouve pas une frontière en l'affirmant, on la teste : la banque de tests doit contenir ces échappées, et
  elles doivent échouer avant qu'on parle d'autoriser. Sur le découpage, elle tient que le reliquat du jour 1 se finit
  avant le jour 2 : le dessin de la carte (R13) était dû au jour 1 ; une tâche reportée sans raison écrite devient une
  tâche perdue. Elle veut le mode dégradé décidé avant la mission (R23), pas pendant. *Sa recommandation : fermer et tester
  l'échappée avant tout « autoriser » ; finir le reliquat du jour 1 d'abord ; une date sur S3, sinon ce n'est pas un plan.*

## Confrontation

1. **`npm test` : autoriser, demander, ou S1.** Musk pour autoriser, avec propriétaire nommé et échappée fermée ; Bezos
   pour une voie intermédiaire (autoriser dans la copie, barrer la sortie, rendre la frontière réelle) ; LeCun, Kenza et
   Bengio pour S1, le runner lançant la commande déclarée, l'agent ne lançant aucun shell arbitraire ; Hamilton refuse tout
   « autoriser » tant que l'échappée n'est pas fermée et testée. Meilleur argument de chaque camp. Musk : les résultats de
   tests comptent, et demander à chaque test tue le temps de cycle. Bengio : l'agent qui réécrit son script de test puis le
   lance est juge de son propre risque, c'est l'invariant 2 qui tombe. Kenza : un non-ingénieur ne peut pas juger un
   « autoriser `npm test --prefix` », donc la décision n'a pas de preneur. Synthèse : S1 est déjà le plan du jour 3 ; le
   Conseil en fait la réponse de sprint, ferme l'échappée (arguments inspectés, pas seulement le nom), et réserve « l'agent
   lance librement les tests » au niveau S3. Le « autoriser » de Musk reste comme désaccord conservé.

2. **Livrer le jour 1 en prod maintenant.** Bengio et Hamilton contre : à S0, le bac à sable n'isole que le worktree, et la
   faille `npm test` serait en production ; une porte sans frontière est une porte ouverte. Shotwell et Musk pour : l'essai
   en prod est une source de données, l'app desktop non signée n'est installée par personne, et on apprend en volant.
   Meilleur argument de chaque camp. Hamilton : on ne met pas en service un affichage prioritaire dont on sait qu'il laisse
   passer une classe d'actions. Shotwell : sans mission déléguée à un agent réel sur un dépôt public, la porte en prod ne
   court aucun risque qu'elle ne coure déjà en Docker. Synthèse : séparer la mise en service de la webapp, sans danger, de
   l'exécution de missions déléguées contre des dépôts publics, qui attend S1 et le point `npm test` tranché.

3. **Le reliquat du jour 1.** Hamilton veut finir le jour 1 avant le jour 2, dessin de la carte compris (R13) ; Musk ne
   veut pas bloquer le jour 2 pour un dessin qui peut avancer en parallèle. Meilleur argument de chaque camp. Hamilton : une
   tâche du jour 1 reportée sans raison écrite devient une tâche perdue, et la carte est le produit que voit l'utilisateur.
   Musk : le dessin n'est pas sur le chemin critique du code des jours 2 et 3, il peut se mener à côté. Synthèse : le dessin
   de la carte et les compteurs par règle sont tracés comme reliquat daté du jour 1 ; le dessin peut avancer en parallèle
   du jour 2, mais il est fini avant que le jour 3 code la carte.

## Recommandations

Numérotées à partir de R27 (R26 est la dernière existante). Chacune porte qui la soutient, qui s'y oppose, sa preuve en dix
jours et son signal d'arrêt.

### R27. La trajectoire est bonne : deux plans, une porte, un cœur de règles petit et déterministe

Le serveur garde, l'ordinateur calcule ; toute action passe par une seule porte ; la décision vit dans du code
déterministe, hors du modèle (invariant 1). Le Conseil confirme la direction.

- **Pour** : Shotwell, LeCun, Musk, Bezos, Bengio, Ait Si Abbou, Hamilton.
- **Contre** : aucun. Réserve de Musk : un propriétaire nommé, une personne, doit remplacer « workspace-owner » sur les
  règles.
- **Preuve en dix jours** : les tests de frontières de modules (Spring Modulith) restent verts, aucun cycle ; le cœur de
  règles décide sans aucun modèle ni réseau, prouvé par les cas de contrat rejoués des deux côtés aux mêmes réponses.
- **Signal d'arrêt** : le cœur déterministe doit grossir sans fin pour couvrir les cas réels, au point que l'invariant 1
  (règles petites et lisibles) ne tienne plus.

### R28. Le découpage tient : les contrats puis la porte puis la preuve d'abord, un seul parcours, puis les jours 2 et 3

L'ordre du jour 1, tel qu'il a été fait, est le bon : on a construit le dossier d'autorisation avant la capacité.

- **Pour** : Shotwell, Musk, LeCun, Bezos.
- **Contre** : aucun.
- **Preuve en dix jours** : le jour 2 finit sur sa condition (famille 3 mesurée sur le corpus public) et le jour 3 sur la
  sienne (familles 4 à 7 passées au moins une fois, mesures du §16.1 relevées).
- **Signal d'arrêt** : un jour déborde de plus de moitié de son estimation ; on re-scope le parcours au lieu d'empiler.

### R29. Finir le reliquat du jour 1 avant d'empiler

Le dessin de la carte de résultat (R13), dû au jour 1, n'est pas fait ; les compteurs par règle ne sont pas exposés ; le
dossier ne survit pas encore à la suppression d'une issue. On les trace comme reliquat daté.

- **Pour** : Hamilton, Shotwell, Ait Si Abbou.
- **Contre** : Musk, pour qui le dessin ne doit pas bloquer le jour 2 et peut avancer en parallèle.
- **Preuve en dix jours** : le dessin de la carte existe (maquette de l'atelier design) avant que le jour 3 la code ; les
  compteurs par règle sont lisibles à l'écran ; un essai montre un dossier qui survit à la suppression de son issue.
- **Signal d'arrêt** : le jour 3 code la carte sans dessin validé, ou un reliquat du jour 1 glisse sans raison écrite.

### R30. L'aperçu des effets (R19) avant toute décision humaine, et dans le dossier

Plan, diff, exécution à blanc : la preuve avant l'avis. Aujourd'hui le diff est au « reste » du dossier de preuve.

- **Pour** : LeCun, Hamilton, Bezos.
- **Contre** : aucun.
- **Preuve en dix jours** : un dossier d'essai contient le diff et, quand elle existe, l'exécution à blanc, lisibles en
  deux minutes (R4), posés avant la décision humaine dans la chaîne d'événements.
- **Signal d'arrêt** : une décision humaine est demandée sans aperçu des effets joint.

### R31. Le jour 3 porte l'agent interne avec un petit modèle local, mesuré tâche par tâche

Les modèles à outils existent sur le poste (`qwen3:8b` et suivants) ; les modèles de complétion (`qwen2.5-coder`) ne
pilotent pas la boucle. L'architecture (la boucle de Cortex) porte le plan, les contraintes et la vérification.

- **Pour** : LeCun, Bengio, Shotwell.
- **Contre** : Musk, seulement si autre chose sort du jour 3 ; au minimum le curseur de modèle, une seule sorte de tâche.
- **Preuve en dix jours** : famille 7, les mêmes tâches avec un petit modèle à outils et avec un grand modèle, résultats
  écrits avant de lancer ; au moins une tâche du parcours réussie par le petit modèle via la boucle interne, tracée au
  dossier.
- **Signal d'arrêt** : même avec l'architecture qui porte le plan, le petit modèle ne tient pas la boucle d'outils sur le
  parcours : l'hypothèse est fausse pour cette tâche, on remonte d'un cran et on l'écrit.

### R32. `npm test` : le niveau S1 comme réponse de sprint, pas « autorisé par défaut »

C'est la recommandation explicite demandée par la Présidence. Le Conseil ne suit pas « autorisé par défaut ». Il retient le
niveau S1 : le runner lance la commande de test déclarée du projet après le travail de l'agent, et l'agent ne dispose
d'aucune règle qui autorise un shell arbitraire. La table ferme l'échappée (les chemins des arguments sont inspectés, pas
seulement le nom de la commande, pour que `npm test --prefix ...` et `npm run build -- --outDir ...` ne soient plus
autorisés). « L'agent lance librement les tests » est réservé au niveau S3, quand la machine est isolée. La règle reçoit un
propriétaire nommé.

Positions des cinq membres nommés :

- **Elon Musk** : pour autoriser, à condition d'un propriétaire nommé sur la règle et de l'échappée fermée ; le vrai
  correctif est S3, pas le clic. C'est le désaccord conservé.
- **Jeff Bezos** : voie intermédiaire, autoriser ce qui reste dans la copie (porte à double sens), refuser ou demander ce
  qui en sort ; rendre la frontière réelle (S3) avant d'appeler les tests franchement réversibles.
- **Yoshua Bengio** : contre « autoriser » tant que la machine n'est pas isolée (l'agent qui réécrit puis lance son script
  de test devient juge de son propre risque, invariant 2) ; S1 plutôt que demander, pour ne pas nourrir le biais
  d'automatisation.
- **Yann LeCun** : S1 au sprint ; demander à chaque test est un garde-fou de prompt déguisé ; l'isolation (S3) est la vraie
  réponse, les incidents venant de bacs à sable mal appliqués.
- **Kenza Ait Si Abbou** : S1, parce qu'un responsable non ingénieur ne peut pas juger un « autoriser `npm test --prefix` »
  ; une décision sans preneur compétent ne doit pas être posée.

- **Pour (S1)** : LeCun, Bengio, Ait Si Abbou ; Shotwell (données exploitables) ; Hamilton, une fois l'échappée fermée et
  testée.
- **Contre** : Musk (autoriser, sous conditions). Bezos à part : une voie intermédiaire qui rejoint S1 sur le refus de la
  sortie.
- **Preuve en dix jours** : S1 rejoué sur le parcours, le runner lançant la commande déclarée ; un cas de la banque de
  tests montre `npm test --prefix <ailleurs>` et `npm run build -- --outDir ../../x` refusés ou demandés, là où ils sont
  autorisés aujourd'hui.
- **Signal d'arrêt** : un essai montre l'agent exécutant, par `npm test`, une commande qu'il a lui-même écrite dans un
  script du dépôt, sans décision ni isolation.

### R33. Ne pas exécuter de missions déléguées en prod sur des dépôts publics avant S1 et avant le point `npm test` tranché

Mettre la webapp en service ne pose pas de danger. Faire tourner un agent réel contre un dépôt public avec la porte du jour
1, alors que le bac à sable n'est encore qu'un worktree (S0), mettrait la faille `npm test` en production.

- **Pour** : Bengio, Hamilton.
- **Contre** : Musk et Shotwell, pour qui l'essai en prod est une source de données et l'app non signée n'est installée par
  personne. Désaccord conservé.
- **Preuve en dix jours** : tant que S1 n'est pas livré, la prod n'accepte que des missions à sorties réversibles ; un essai
  le vérifie. La mise en service de la webapp et l'exécution de missions déléguées sont deux décisions séparées.
- **Signal d'arrêt** : une mission en prod produit une sortie irréversible sans décision, ou l'échappée `npm` s'exécute sur
  un dépôt de production.

**Désaccords conservés** : Musk tient pour autoriser `npm test` (R32), avec propriétaire nommé et échappée fermée, contre
S1 ; Bezos propose une voie intermédiaire distincte de S1 sur la forme, proche sur le refus de la sortie. Musk et Shotwell
acceptent l'essai en prod que Bengio et Hamilton refusent avant S1 (R33). Musk n'ajoute rien au jour 3 sans retirer (R31).
Hamilton exige une date sur S3, aujourd'hui « à étudier ».

## Décision de la Présidence (28/10/2026)

En attente. La Présidence tranche chaque recommandation (retenue, à l'essai, écartée ou reportée), avec sa raison, dans ses
mots. Le secrétariat ne rédige pas cette raison à sa place.

| # | Décision | Raison, dans les mots de la Présidence |
| --- | --- | --- |
| R27 | En attente | |
| R28 | En attente | |
| R29 | En attente | |
| R30 | En attente | |
| R31 | En attente | |
| R32 (`npm test`) | En attente | |
| R33 | En attente | |

## Notes du secrétariat

- Ordre de parole tiré au sort le 28/10 à 18:08 (`shuf`) : Shotwell, LeCun, Musk, Bezos, Ait Si Abbou, Bengio, Hamilton.
  Contradictrice désignée : Margaret Hamilton.
- Formation restreinte (7), conforme à la charte (5 à 7 membres, un contradicteur). Pôles présents : Impulsion (Musk,
  Bezos, Shotwell), Science (Bengio, LeCun, Hamilton), Pont (Ait Si Abbou). Absents : Harmonie et Design. La fatigue du
  clic (angle de Harris, R24 de la séance n°4) et l'invisibilité du harnais pour l'utilisateur (angle de Jobs) sont donc
  sous-représentées ; Ait Si Abbou a porté la lisibilité pour un non-ingénieur, qui les recoupe.
- Le consensus large sur R27 et R28 a déclenché la contradictrice (règle §7.5) : Hamilton a attaqué S1 lui-même et la
  release en prod.
- Fiches à jour : aucun rafraîchissement requis (toutes à moins de 30 jours).
- Fait vérifié par le secrétariat, non par un membre : le dossier 6 (rejeu de la table par défaut) a été produit en
  exécutant le moteur du runner contre `contracts/rules/default.rules.json`, sans modifier aucun fichier. Il confirme, et
  précise, le point ouvert de la spécification (§20) : l'échappée par les arguments (`--prefix`, `--outDir`) s'ajoute au
  fait que l'agent peut réécrire les scripts du dépôt.
- Conflits d'intérêts signalés : Musk (Cursor, racheté par SpaceX ; son avis sur l'ordre des agents et le curseur de
  modèle touche ses intérêts) ; LeCun (AMI Labs, modèles du monde ; son insistance sur l'aperçu des effets recoupe son pari
  commercial, et AMI n'a pas de produit public) ; Shotwell (numéro deux de SpaceX, à ne pas réduire à l'exécutante de Musk,
  elle a ses positions, données avant décision et régulation « sensée »).
- Extrapolations marquées : Bengio applique à un harnais de projet des positions qui visent l'IA de frontière ; Ait Si
  Abbou a peu de positions publiques sur les agents de code, sa fonction de 2026 reste à vérifier ; Hamilton, siège
  historique décédé en 2026, n'a pris aucune position sur les agents d'IA : ses interventions sont des transpositions de
  ses principes documentés (priorités par mission, affichage prioritaire, aucune modification sans raison tracée, l'erreur
  d'interface comme source principale d'erreurs).
- Aucune citation réelle n'est reprise dans les interventions : tout est paraphrase et `[HYPOTHÈSE]`. Aucun aval n'est
  attribué à personne.

## Suites

- Procès-verbal dans `conseil/seances/`, et une ligne à ajouter au registre de la charte (§12) après la décision de la
  Présidence.
- Récit de la séance à porter au `Journal.md` du labo, avec le lien du PV.
- Recommandations à portée produit : une fois tranchées, elles descendent en tâches ou en points ouverts de la
  spécification de la v2 (§20), jamais par copier-coller. R32 et R33 touchent la table par défaut et l'ordre de la mise en
  production : si elles sont retenues, elles passent par une tâche du sprint, et le point ouvert `npm test` de la
  spécification (§20) se ferme dessus.
- Preuves en dix jours retenues : elles se rangent dans `experiences/Experiences.md` (les prochaines après E10) ; la mesure
  de l'échappée des arguments (R32) et la séparation prod webapp / missions déléguées (R33) sont les plus prêtes à écrire.
- Question laissée ouverte, à verser à `Questions-ouvertes.md` si la Présidence ne tranche pas S3 : une date pour
  l'isolation de la machine (S3), aujourd'hui « à étudier », exigée par Hamilton.
