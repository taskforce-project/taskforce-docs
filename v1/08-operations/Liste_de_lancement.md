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
| Sans la runtime Visual C++ | Cette étape cache la runtime à Windows et dit ce qui marche encore (constat 1 ci-dessous). Son résultat n'arrête pas la liste : il concerne une autre machine que le runner. |
| Désinstallation | Code 0 ; le dossier du programme, son entrée dans la liste des programmes et ses raccourcis ont disparu. Les données de la personne restent, c'est voulu. |

L'artefact `launch-checklist-evidence` du run garde les captures d'écran, les journaux de l'app et de PostgreSQL, les
listes des dossiers et les nombres de lignes, 30 jours.

## 2. Comment la lancer

Dans GitHub, onglet Actions, « Desktop - Launch checklist », « Run workflow » : deux champs, `from` et `to`, vides pour
les deux dernières versions publiées. Ou en ligne de commande :

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

## 4. Résultat du 08/11/2026

Run : https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42509458147, de 1.8.0 à 1.9.0, vert en 3 min 47 s. Toutes les étapes de la liste passent. Les captures de
la fenêtre de connexion, avant et après la mise à jour, sont dans l'artefact. Le déclenchement à la main, avec ses deux
champs, a été essayé aussi, de 1.7.0 à 1.8.0 : vert (https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42509970856).

**Constat 1, un défaut réel : PostgreSQL a besoin de la runtime Visual C++, et TaskForce ne l'apporte pas.** Le runner a
cette runtime, donc la liste passe. L'étape qui la cache (`vcruntime140*.dll`, `msvcp140*.dll` et voisines retirées de
`System32`) montre ce qui se passerait sans elle : l'app atteint sa fenêtre de connexion et Java démarre (il a ses
propres copies), mais les six outils de PostgreSQL (`initdb`, `pg_ctl`, `postgres`, `pg_dump`, `pg_restore`, `psql`) ne
se chargent pas, code `0xC0000135` : une DLL manque. `initdb.exe` importe `VCRUNTIME140.dll`, que ni
`resources\postgres\bin` ni l'installeur n'apportent. Windows ne la garantit pas : sur un Windows 11 à jour, ses composants
n'en gardent qu'une copie privée hors de `System32` (`HealthAttestationClient`, `Microsoft-Edge-WebView`). Sur un PC qui
n'a jamais reçu le « Visual C++ Redistributable », l'app s'arrêterait donc juste après la connexion, à la création de
sa base, avec « TaskForce could not start ». Combien de PC sont dans ce cas, on ne le sait pas. Ce n'est pas corrigé
ici : la décision et le correctif appartiennent à une release. L'étape passera d'elle-même au vert le jour où une
version apportera la runtime, et il faudra alors retirer son `continue-on-error`.

**Constat 2, un défaut mineur : le backend ne refuse pas de démarrer sans compte.** Un essai fait en construisant la
liste (https://github.com/taskforce-project/taskforce-fullstack/actions/runs/42507933514, retiré ensuite) a lancé le backend installé avec tout ce que la coque lui donne, sauf le compte.
Il aurait dû refuser (`DesktopConfig.validate`) ; il a démarré, car les variables absentes restent le texte
`${TF_DESKTOP_ACCOUNT_SUBJECT}`, qui n'est pas vide. Il a appliqué ses 116 migrations avec Flyway sur le PostgreSQL
embarqué et créé un utilisateur à ce nom. Sans effet pour une personne (la coque passe toujours le compte, le jeton de
lancement reste exigé), mais la vérification ne fait pas ce qu'elle dit. La liste ne s'en sert pas : ce serait un faux
compte accepté par le code livré.
