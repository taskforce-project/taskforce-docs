---
id: cr-2026-s30-cloture-v1
title: Compte rendu d'activite, semaine 30, cycle Cloture V1
doc_type: compte-rendu
statut: valide
version: 1.0
date: "23/07/2026"
auteur: Pierre MICHEL
tags: [compte-rendu, e6, agile, cloture-v1, memoire, rncp]
---

# Compte rendu d'activite, semaine 30

> Exemple rempli de la [[Trame_Compte_Rendu_Activite]] (livrable E6). Toutes les valeurs de ce
> document ont ete mesurees, aucune n'est estimee. Les references de commit sont verifiables dans
> l'historique du depot.

## En-tete

| Champ | Valeur |
| --- | --- |
| Periode couverte | du 20/07/2026 au 23/07/2026 |
| Cycle | Cloture V1, cycle 2 sur 3 |
| Jalon vise | J5, gel fonctionnel et mise en preuve |
| Phase du plan projet | Qualite, securite et conformite, avant assemblage du dossier |
| Redacteur | Pierre MICHEL |
| Date de redaction | 23/07/2026 |

## 1. Contexte du cycle

Le gel fonctionnel etant acte depuis le 20/06, ce cycle ne produit plus de fonctionnalite. Il a un
seul objet : rendre **demontrable** ce qui etait jusqu'ici seulement affirme. La roadmap de cloture
listait onze lots restants, dont plusieurs decrits comme non commences. Le cycle a commence par
verifier cette liste plutot que par l'executer, ce qui s'est revele determinant : quatre lots sur
six etaient deja faits, et le probleme reel n'etait pas le code mais l'ecart entre le code et ce que
la documentation en disait.

## 2. Objectifs fixes a la priorisation

| # | Objectif | Quadrant Eisenhower | Critere de reussite | Reference |
| --- | --- | --- | --- | --- |
| 1 | Analyse statique propre sur tout le depot | Important et urgent | 0 erreur ESLint et 0 erreur TypeScript | lot C4 |
| 2 | Suite de tests verte et couverture remesuree | Important et urgent | seuls seuils chiffres de la grille, 50 % minimum | lots C3, C18, C25 |
| 3 | Aucune vulnerabilite critique | Important et urgent | 0 CRITICAL sur les images | lot C5 |
| 4 | Trancher l'accessibilite | Important non urgent | verdict fonde sur une mesure, pas sur un avis | lot C10 |
| 5 | Mesurer le referencement de la landing | Important non urgent | 70 % minimum exiges par la grille | lot C9 |
| 6 | Conformite RGPD de bout en bout | Important et urgent | droits des personnes et conservation effectifs | lot C7 |
| 7 | Verifier l'integration de paiement | Important non urgent | webhooks fonctionnels | lot C13 |
| 8 | Reconcilier le corpus documentaire | Important et urgent | un chiffre, une source datee | Phase A |

## 3. Activites realisees

| Objectif | Activite | Reference verifiable | Etat |
| --- | --- | --- | --- |
| 1 | Passage du linter sur l'ensemble du depot, et non plus sur les seuls fichiers touches | lot C4 | Terminee |
| 1 | Correction de deux defauts reels trouves au passage : recadrage de pagination fait dans un effet, et largeur de squelette tiree au sort au rendu | `use-pagination`, `SidebarMenuSkeleton` | Terminee |
| 2 | Reparation de 41 tests front en echec, tous decrivant un contrat perime | lot C3 | Terminee |
| 2 | Ecriture de 20 tests parametres sur l'export CSV, seul module sous son seuil | `8f5b575b`, `f69dd6bd` | Terminee |
| 2 | Creation de `ConnectorCatalogTest`, 27 cas parametres | lot C3 back | Terminee |
| 3 | Montee de version du parent Spring Boot, de Tomcat, de Netty et des BOM Jackson | `7495b5ab`, `446977c6` | Terminee |
| 3 | Suppression de npm de l'image d'execution du front, inutile en mode autonome et surface de vulnerabilite | `Dockerfile` front | Terminee |
| 4 | Correction du seuil du test d'accessibilite, qui n'echouait que sur les violations critiques | `71627514` | Terminee |
| 4 | Correction des violations revelees : contrastes, libelles de selecteur, poignee de deplacement clavier | `9102c9bb`, `68718afd`, `853eed20`, `129e10be` | Terminee |
| 5 | Reparation du job Lighthouse, qui n'avait jamais rien mesure | `be86511c` | Terminee |
| 6 | Ecriture de `RetentionScheduler` et de ses tests, appliquant les durees de conservation declarees | `b4b42145`, `062ebafa`, `9bb7f11b` | Terminee |
| 6 | Correction du registre des traitements : un sous-traitant hors UE y figurait alors qu'il est retire du code depuis le 16/07 | `2bfce6bb` | Terminee |
| 7 | Verification du flux de paiement dans le code | lot C13 | Terminee |
| 8 | Reconciliation des chiffres et correction de quatre sur-declarations | Phase A | Terminee |
| 8 | Mise a jour de la grille d'evaluation, inchangee depuis le 18/06 | grille XLSX | Terminee, une correction restant a appliquer, cf. section 6 |
| hors objectif | Suppression du code mort `RefreshToken` et de sa table | `98beafe8`, `b2c084d1`, `faac7376` | Terminee |
| hors objectif | Installation d'un garde mecanique de tracabilite documentaire | `08fcf135` | Terminee |

## 4. Controle de la Definition of Done

- [x] Code implemente et compilant
- [x] Tests unitaires et d'integration ecrits et passants
- [ ] Chaine d'integration continue verte
- [x] Aucune regression sur les tests existants
- [x] Code fusionne
- [x] Documentation du Brain OS mise a jour

La troisieme case n'est pas cochee et ce n'est pas un oubli. Les suites sont vertes en local, mais
la chaine d'integration continue n'execute ni analyse statique de qualite back, ni porte de
couverture bloquante, ni scan de securite. Ecart declare en section 6.

## 5. Indicateurs mesures

| Indicateur | Valeur | Mesure le | Perimetre ou reserve |
| --- | --- | --- | --- |
| Analyse statique front | 0 erreur, 21 avertissements documentes | 21/07 | Depot entier. Etat initial : 185 erreurs et 586 avertissements sur 65 fichiers |
| Types | 0 erreur | 21/07 | `tsc --noEmit` |
| Suite front | 805 tests sur 63 fichiers, 0 echec | 23/07 | Etat initial : 41 en echec |
| Couverture front | 89,55 % de lignes | 23/07 | Perimetre logique uniquement. Les 48 routes et les composants de presentation sont couverts par Playwright, pas par cette mesure |
| Suite back | 792 tests, 0 echec | 23/07 | |
| Couverture back | 73,71 % de lignes | 22/07 | Non remesuree apres l'ajout de `RetentionSchedulerTest` |
| Images, vulnerabilites critiques | 0 sur les deux images | 22/07 | Etat initial : 13 sur le back, 1 sur le front |
| Images, vulnerabilites hautes | 12, dont 11 issues des images de base Alpine | 22/07 | Correctif amont, hors de notre portee |
| Dependances front en production | 0 critique, 0 haute | 22/07 | Arbre de production seul |
| Pentest applicatif | 0 alerte de risque sur l'API | 22/07 | A rejouer apres les modifications d'en-tetes, cf. section 6 |
| Accessibilite | 0 violation sur 3 pages, tous impacts confondus | 22/07 | Etat initial reel : 10 violations invisibles, 4 sur la connexion et 6 sur le tableau de bord |
| Referencement de la landing | 92 % sur l'accueil, 100 % sur les 4 autres pages | 22/07 | Seuil exige : 70 % |
| Grille d'evaluation | 78 verts, 9 jaunes, 3 rouges | 23/07 | Avant la correction de C11 decrite en section 6 |

## 6. Ecarts par rapport aux objectifs

| Objectif concerne | Ecart constate | Cause | Traitement retenu |
| --- | --- | --- | --- |
| 3 | Le scan du code source n'a pas pu etre execute | Il ne termine pas sous Docker pour Windows, meme apres exclusion des repertoires volumineux | Reporte en integration continue. **Non mesure, donc non declare comme acquis** |
| 3 | Le pentest n'a pas ete rejoue apres les modifications de politique de securite du contenu | Manque de temps sur le cycle | Report au cycle suivant |
| 7 | Le flux de paiement n'a jamais ete exerce avec de vrais evenements | Necessite les cles de test, que je place moi-meme dans l'environnement | Configuration desormais complete, execution a faire |
| 8 | Quatre criteres de C11 ont ete passes au vert a tort | Ils ont ete evalues sur l'implementation RGPD de TaskForce, alors que le referentiel les rattache au cas professionnel externe E9 | Repasses au rouge. Correction ecrite mais **non encore appliquee, le fichier etant ouvert dans le tableur** |
| 2 | Trois tests d'authentification ont expire une fois sous instrumentation de couverture | Cause non etablie : le nettoyage entre tests est pourtant configure et le delai est deja a 15 secondes | **Aucun correctif applique.** Un correctif que je ne peux pas verifier n'en est pas un. Risque documente |
| Definition of Done | La chaine d'integration continue n'execute ni analyse qualite back, ni porte de couverture, ni scan de securite | Les outils existent et sont utilises, mais par script manuel | Cablage a faire, tracé au lot C26 |

## 7. Obstacles et risques

| Obstacle ou risque | Effet sur le projet | Reference registre | Action |
| --- | --- | --- | --- |
| La machine virtuelle de l'ecole est derriere une traduction d'adresses, sans entree possible | Si elle est retenue, l'application n'aura pas d'adresse publique et la competence C28 restera non demontrable | Choix d'hebergement, cf. [[Strategie_Hebergement]] | Demande envoyee, decision en attente |
| Le sujet du cas professionnel E9 n'a pas ete fourni | Quatre criteres de C11 en dependent, et la matiere ne nous appartient pas | Nouveau | A reclamer immediatement |
| Le choix de Java et Spring diverge du cahier des charges, qui impose PHP avec Symfony ou Node.js | Question probable en soutenance | Nouveau | Argumentaire prepare, validation par un formateur toujours non obtenue |

## 8. Bilan

**Ce qui a fonctionne et doit etre reconduit : mesurer avant d'executer.** Le cycle a commence par
verifier l'inventaire des taches restantes au lieu de l'appliquer. Sur six lots examines, **quatre
etaient deja faits** et documentes comme manquants. Le temps passe a verifier a ete tres largement
recupere. Le meme reflexe a evite deux fausses conclusions : l'accessibilite semblait acquise alors
que dix violations passaient sous le seuil du test, et le referencement semblait defaillant alors
que c'est l'outil de mesure qui ne mesurait rien.

**Ce qui a mal fonctionne : la documentation derivait plus vite que le code.** Les chiffres de
couverture circulaient sous trois valeurs differentes, et quatre affirmations decrivaient au present
des elements inexistants, dont des certificats et une zone de noms de domaine. Une sur-declaration
est plus couteuse qu'un manque annonce : un manque se defend, une preuve reclamee et absente ne se
defend pas.

**Changement de pratique effectivement mis en place**, et non simple intention. Deux regles
textuelles imposaient deja la mise a jour documentaire et elles ont derive quand meme, parce
qu'elles se declenchent en fin de tache, au moment ou l'attention est la plus faible. Elles ont donc
ete remplacees par un **garde mecanique** qui refuse la cloture d'une session laissant du code
modifie sans trace ecrite. Regle complementaire adoptee : tout indicateur porte desormais sa date et
son perimetre, faute de quoi il se perime en quelques jours.

## 9. Decisions engageantes

| Decision | Motif | Consequence | ADR |
| --- | --- | --- | --- |
| Abaisser le seuil de couverture back de 84 % a 70 % et verifier qu'il se declenche reellement | Le seuil de 84 % etait inerte, car lie a une phase que la construction n'atteignait pas. Un seuil qu'on ne franchit jamais ne prouve rien | Porte desormais reellement bloquante en verification locale | a formaliser |
| Ne pas fixer dans le code la duree de conservation du journal d'audit | Cette duree releve du responsable de traitement, pas du developpeur. La trancher inventerait une politique et contredirait une mesure de securite deja annoncee au registre | Point ouvert, a decider avant exploitation reelle | a formaliser |
| Ne pas chiffrer l'adresse de courriel ni l'identifiant d'authentification | Le chiffrement authentifie n'est pas deterministe et casserait les recherches | Ne jamais ecrire que toutes les donnees personnelles sont chiffrees. Formulation exacte imposee au dossier | a formaliser |
| Conserver Testcontainers hors du projet | Incompatibilite du client Docker embarque avec le mandataire de Docker Desktop lorsque les tests s'executent en conteneur | Ne jamais annoncer Testcontainers a l'oral : la bibliotheque n'est pas dans le fichier de construction | existante |

## 10. Objectifs du cycle suivant

1. Reclamer le sujet du cas professionnel **E9**, dont dependent quatre criteres. Priorite haute : la matiere ne nous appartient pas.
2. Appliquer la correction des quatre criteres de C11 dans la grille.
3. Produire la **presentation de synthese**, annexe obligatoire du dossier.
4. Rejouer le pentest apres les modifications d'en-tetes.
5. Exercer le flux de paiement avec de vrais evenements.
6. Assembler le **dossier unique**, le jury attendant un document et non les quatre-vingt-dix-sept fichiers actuels.
7. Purger les caracteres de mise en forme automatique sur l'ensemble du dossier, en dernier.

---

> Trame source : [[Trame_Compte_Rendu_Activite]] · Methode : [[Note_Methode_Agile]] ·
> Suivi : [[Registre_Risques]] · [[Gantt_Planning]].
