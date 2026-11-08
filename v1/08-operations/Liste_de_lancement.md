---
id: liste-de-lancement
title: Liste de lancement de l'app desktop
doc_type: operations
statut: valide
version: 1.0
date: "08/11/2026"
auteur: Pierre MICHEL
tags: [desktop, lancement, installation, mise-a-jour, sauvegarde, restauration, ci, r105, j1]
---

# Liste de lancement de l'app desktop

> Chaque jalon se valide par une liste de lancement (R105, [[Roadmap_Backlog]] §0) : installation propre, mise à jour,
> sauvegarde et restauration. Le CEO a un seul ordinateur, où l'app est déjà installée : une installation propre ne se
> prouve qu'ailleurs. Le workflow « Desktop - Launch checklist » (`.github/workflows/desktop-launch-checklist.yml`) la
> prouve sur un runner Windows neuf, avec seulement ce qui est publié : les installeurs des GitHub Releases, aucun
> compte, aucun secret.

## 1. Ce que la liste prouve

Chaque étape finit par une ligne dans le résumé du job. Une étape qui échoue fait échouer le job et dit laquelle.

| Étape | Ce qui est prouvé |
|---|---|
| Versions et installeurs | Par défaut, les deux dernières versions desktop publiées. Chaque installeur vient de sa release et correspond au SHA-512 de son `latest.yml`, celui que vérifie l'outil de mise à jour. |
| Installation propre | Sur une machine sans aucune trace de TaskForce, la version précédente s'installe en silence (`/S`, code 0). Le programme, son Java, son backend, son PostgreSQL, son interface, son runner et ses raccourcis sont à leur place. L'exécutable, le `package.json` de l'app et la liste des programmes disent la même version. |
| Premier démarrage | L'app démarre et l'écrit dans son journal (`TaskForce X starting`), ouvre la fenêtre « Sign in to TaskForce », dont la page se charge depuis les fichiers de l'app avec son bouton utilisable, puis se ferme avec le code 0, sans rapport de plantage. |
| Base embarquée | Le PostgreSQL installé crée un cluster avec les options de l'app, dans le dossier de données comme celui d'une personne, et démarre seul. Les migrations du backend installé s'appliquent, pgvector se charge, 2 000 lignes avec vecteurs sont écrites et retrouvées par leur index. |
| Mise à jour | La version suivante s'installe par-dessus avec les arguments que l'app donne à l'installeur (`--updated /S --force-run`). Les fichiers disent la nouvelle version, l'app se rouvre seule et atteint la même fenêtre. Un fichier témoin et le dossier de la base arrivent identiques à l'octet, le journal garde les lignes du premier lancement. |
| Base après la mise à jour | Le PostgreSQL de la nouvelle version ouvre la base de l'ancienne et y trouve les mêmes lignes. Une copie faite comme celle de l'app avant une migration (`pg_dump -Fc`), restaurée dans une seconde base, a le même nombre de lignes dans toutes les tables et les mêmes vecteurs, retrouvés par leur index reconstruit. Aucune migration déjà livrée n'a changé (Flyway refuserait la base), et les nouvelles s'appliquent. |
| Sans compte | Le Java installé tourne, le serveur de l'interface répond et sert ses propres fichiers. |
| Sans la runtime Visual C++ | Cette étape cache la runtime à Windows, comme sur un PC qui ne l'a jamais reçue. L'app doit atteindre sa fenêtre, Java démarrer, les six outils de PostgreSQL se charger, `initdb` créer un cluster et PostgreSQL démarrer. Bloquante à partir de la version 1.10.0, qui apporte cette runtime. Pour les versions publiées avant, elle dit ce qu'elle trouve sans arrêter la liste. |
| Le correctif sur les fichiers publiés | Pour une version d'avant 1.10.0 seulement : le code de la construction (`desktop/scripts/postgres-runtime.mjs`) s'applique à une copie des fichiers publiés, puis, la runtime cachée, les six outils se chargent, `initdb` crée un cluster et PostgreSQL démarre avec pgvector et uuid-ossp. Bloquante. |
| Désinstallation | Code 0 ; le dossier du programme, son entrée dans la liste des programmes et ses raccourcis ont disparu. Les données de la personne restent, c'est voulu. |

L'artefact `launch-checklist-evidence` du run garde les captures d'écran, les journaux de l'app et de PostgreSQL, les
listes des dossiers et les nombres de lignes, 30 jours.

## 2. Comment la lancer

Dans GitHub, onglet Actions, « Desktop - Launch checklist », « Run workflow » : deux champs, `from` et `to`, vides pour
les deux dernières versions publiées, et `runner` pour une autre image (`windows-2022`, celle qui construit l'app). Ou en
ligne de commande :

```
gh workflow run desktop-launch-checklist.yml -f from=1.8.0 -f to=1.9.0
```

Un run dure moins de 5 minutes (limite : 20). Le script installe et désinstalle TaskForce dans les dossiers de
l'utilisateur : il refuse de tourner ailleurs que sur un runner hébergé par GitHub, on ne le lance jamais sur un poste.

## 3. Ce qu'elle ne peut pas prouver

- **Tout ce qui suit la connexion.** Sans compte, la fenêtre de connexion est le bout du chemin. Restent hors de portée : la pile démarrée par l'app, Flyway lancé par le backend, l'interface avec des données, la mise à jour lancée par l'app elle-même (téléchargement depuis `desktop-latest`, « Restart now »). Le backend n'est pas démarré. La restauration d'une vraie sauvegarde se prouve à part, sur le poste du CEO.
- **Un vrai PC.** Le runner est un Windows Server 2025, en administrateur, sans carte graphique, sans SmartScreen ni antivirus grand public : la réaction d'un Windows à un installeur non signé ne s'y voit pas.
- **Un PC sans outils.** Le runner a Java, Node et PostgreSQL. La liste retire leurs variables et lance tout par chemin absolu, mais une bibliothèque du système qui manquerait à un vrai PC ne se voit que si on la cache exprès, comme la runtime Visual C++.
- **De vraies données.** Les tables de l'app sont vides sans compte : la copie et sa restauration portent sur le vrai schéma et sur les lignes de la table d'essai.
- **Le Store et Linux.** La version Microsoft Store et les paquets Linux ne sont pas couverts.
- **Le paquet d'une version pas encore publiée.** La liste ne prend que ce qui est publié : elle ne prouve l'installeur qui apporte la runtime (1.10.0) qu'une fois celui-ci publié, par un run de 1.9.0 à 1.10.0 : fait le 08/11 (section 4).

## 4. Résultat du 08/11/2026

Run : https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42513560113, de 1.8.0 à 1.9.0, vert en 3 min 40 s, sur `windows-latest`. Même résultat sur `windows-2022`,
l'image qui construit l'app : https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42513905622. Toutes les étapes de la liste passent. Les captures de la fenêtre de
connexion, avant et après la mise à jour, sont dans l'artefact. Le déclenchement à la main avec ses champs a été essayé
aussi, de 1.7.0 à 1.8.0 : vert (https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42509970856).

**De 1.9.0 à 1.10.0, une fois publiée** : vert en 3 min 42 s, sur `windows-latest`
(https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42531976429). L'installeur publié porte la
runtime Visual C++ : l'étape bloquante passe, la runtime cachée à Windows, jusqu'à la fenêtre de connexion, Java, les
six outils de PostgreSQL et `initdb`.

**Constat 1, corrigé à partir de la 1.10.0 : le PostgreSQL embarqué a besoin de la runtime Visual C++.** Jusqu'à la
1.9.0, ni `resources\postgres\bin` ni l'installeur ne l'apportent. Le runner l'a, donc la liste passe. L'étape qui la
cache montre ce qui se passerait sans elle : l'app atteint sa fenêtre de connexion et Java démarre, mais les six outils
de PostgreSQL (`initdb`, `pg_ctl`, `postgres`, `pg_dump`, `pg_restore`, `psql`) ne se chargent pas, code
`0xC0000135` : une DLL manque. Windows ne la garantit pas : sur un Windows 11 à jour, ses composants n'en gardent qu'une
copie privée hors de `System32` (`HealthAttestationClient`, `Microsoft-Edge-WebView`). Sur un PC qui n'a jamais reçu le
« Visual C++ Redistributable », l'app s'arrêterait juste après la connexion, à la création de sa base, avec « TaskForce
could not start ». Combien de PC sont dans ce cas, on ne le sait pas.

Le correctif (`desktop/scripts/postgres-runtime.mjs`, appelé par `prepare-resources.mjs`) lit les tables d'import de
tout ce que contiennent `postgres/bin` et `postgres/lib`, et de ce qu'il copie : il faut `vcruntime140.dll`,
`vcruntime140_1.dll` et `msvcp140.dll`. Ces trois DLL sont copiées à côté de `postgres.exe`, depuis le dossier de
redistribution de Visual Studio de la machine de construction. Le Java embarqué porte ces trois noms, mais en
14.40.33810, plus anciens que les outils 14.44 des binaires de PostgreSQL : Microsoft demande une runtime au moins aussi
récente que les outils de compilation du plus récent des binaires. Une DLL absente ou trop ancienne arrête la
construction en la nommant. La version du Store prend les mêmes ressources (`extraResources` d'`electron-builder.yml`,
construites une seule fois pour les deux paquets) : elle est couverte du même coup.

Ce droit de copier existe : la liste des fichiers distribuables de Visual Studio 2022 permet de copier et de distribuer
avec son programme, sans les modifier, les fichiers du dossier `VC\redist`, pour un utilisateur de Visual Studio sous
licence. Microsoft déconseille le déploiement local parce qu'il ne met pas ces DLL à jour lui-même, et recommande alors
de les mettre à jour soi-même : chaque construction reprend celles du Visual Studio de sa machine.

Prouvé avant la release : sur une copie des fichiers publiés de 1.9.0, le code de la construction copie ces DLL, puis,
la runtime cachée, les six outils se chargent, `initdb` crée un cluster, et PostgreSQL démarre et charge pgvector et
uuid-ossp. Sur `windows-2022`, les DLL viennent de Visual Studio 2022, en 14.44.35211. Prouvé après la publication de
1.10.0 : l'installeur publié porte ces DLL et passe l'étape bloquante (section 4). Le paquet du
Store, lui, ne passe pas par cette liste.

**Constat 2, corrigé à partir de la 1.10.0 : le backend ne refusait pas de démarrer sans compte.** Un essai fait en
construisant la liste (https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42507933514, retiré ensuite) a lancé le backend installé avec tout ce que la coque lui donne,
sauf le compte. `DesktopConfig.validate` aurait dû le refuser ; il a démarré, car une variable absente restait le texte
`${TF_DESKTOP_ACCOUNT_SUBJECT}`, qui n'est pas vide. Il a appliqué ses 116 migrations avec Flyway sur le PostgreSQL
embarqué et créé un utilisateur à ce nom. Sans effet pour une personne (la coque passe toujours le compte, le jeton de
lancement reste exigé), mais la vérification ne faisait pas ce qu'elle dit. Le dossier de données avait le même trou.
`application-desktop.yml` donne maintenant à ces réglages le défaut vide des réglages facultatifs : une variable absente
compte comme vide, et le démarrage est refusé. La liste ne démarre toujours pas le backend : ce serait un faux compte
accepté par le code livré.
