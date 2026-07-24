---
id: soutenance-plan-minute
title: Plan minuté de la soutenance (étape 1)
doc_type: soutenance
statut: a-valider
version: 2.0
date: "21/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, rncp, oral, plan, timing, bc02, bc03, grille]
---

# Plan minuté de la soutenance

> Étape 1 de la méthode définie dans `.ai/soutenance-brief.md`. **À valider avant toute rédaction
> du texte oral.** Cadre officiel : 20 minutes de présentation démonstration comprise, puis 15
> minutes de questions. Ordre imposé : bloc BC02 (front) puis bloc BC03 (back).
>
> **v2.0** : plan reconstruit sur la grille d'évaluation réelle du jury
> (`taskforce-docs/memoire/Grille_évaluation_vierge_DFS_25-26.xlsx`) et sur trois audits de code
> menés le 21/07/2026. La v1.0 couvrait les 14 compétences mais laissait 19 critères de notation
> sans aucune diapositive.

## 1. Le principe directeur

Le jury ne coche pas des compétences, il coche **des critères, un par un**, sur la grille Excel de
l'école. Il y a **26 critères sur BC02** et **22 sur BC03**. Chaque diapositive est donc conçue pour
faire cocher trois à cinq lignes de cette grille, et le vocabulaire du critère doit être prononcé à
voix haute.

**24 diapositives principales** plus **3 diapositives tampon**. Dix-neuf diapositives parlées,
4 minutes de démonstration en deux temps, 19 minutes 20 au total.

## 2. Le plan, diapositive par diapositive

Fonds du gabarit : T1 titre, T2 T3 T4 sombres, T5 T6 clairs, T7 séparateur, T8 pleine page orange.

### Ouverture (2 min 25)

| # | Fond | Message unique | Durée | Critères visés |
|---|---|---|---|---|
| 1 | T1 | Qui je suis, mon parcours, TaskForce en une phrase | 0:45 | Note pédagogique p. 5 |
| 2 | T2 | Le problème, la demande du client, les objectifs | 0:45 | Note pédagogique p. 5 |
| 3 | T2 | L'architecture d'ensemble et le parcours d'une requête | 0:55 | Cadre des deux blocs |

La diapositive 3 **ne justifie aucune technologie**. Elle pose la carte. Chaque bloc justifie ensuite
sa propre pile au moment où il la prouve, ce qui supprime la redondance de la v1.0 et sert deux
critères distincts, C15-1 pour le front et C22-1 pour le back.

Parcours à annoncer en diapositive 1, tiré du CV : Head of Engineering chez Plania, unité de
TechGuys, sur un SaaS à 12 000 dollars de revenu mensuel récurrent, après un poste de lead
technique sur des comptes entreprise, un LIMS pharmaceutique conforme 21 CFR Part 11 chez
Nancyclotep, et un stage au LORIA. Statut étudiant-entrepreneur.

### Partie 1, front-end, bloc BC02 (8 min 00)

| # | Fond | Message unique | Durée | Critères visés |
|---|---|---|---|---|
| 4 | T7 | Séparateur, Partie 1 Front-end | 0:10 | |
| 5 | T6 | La technologie front, pourquoi elle, et comment le code est organisé | 0:50 | C15-1, C15-2, C16-1, C16-5 |
| 6 | T5 | De la conception aux écrans livrés, et les cas d'usage couverts | 0:45 | C13-1, C13-3, C15-3 |
| 7 | T5 | La charte du client, traduite en design system | 0:40 | C14 |
| 8 | T6 | Sécurité, écoconception et chaîne de build du front | 0:55 | C16-2, C16-3, C16-4, C19-3 |
| 9 | T7 | **Démonstration côté utilisateur** | 1:55 | C13-1, C13-2, C15-3, C15-4 |
| 10 | T6 | Consommer l'API de façon sécurisée | 0:45 | C17-1, C17-2, C17-3, C17-4 |
| 11 | T5 | L'accessibilité, et jusqu'où elle est vérifiée | 0:45 | C13-2, C15-4 |
| 12 | T5 | Le référencement et la mesure d'audience | 0:45 | C20-1, C20-2, C20-3, C20-4 |
| 13 | T6 | Tester et industrialiser le front | 1:00 | C18-1 à C18-4, C19-1, C19-2 |

Trois diapositives sont nouvelles par rapport à la v1.0 : la 8, la 11 et la 12. La v1.0 faisait porter
l'accessibilité, la performance et les quatre critères de C20 à une seule diapositive de 50 secondes.

### Partie 2, back-end, bloc BC03 (7 min 35)

| # | Fond | Message unique | Durée | Critères visés |
|---|---|---|---|---|
| 14 | T7 | Séparateur, Partie 2 Back-end | 0:10 | |
| 15 | T2 | L'architecture back, le choix Java Spring, et où vivent les rôles | 0:55 | C22-1, C22-3, C22-4, C22-8 |
| 16 | T3 | La persistance et la sécurité en profondeur | 0:55 | C21 (six items) |
| 17 | T3 | Le modèle de données qui rend le smart-assign possible | 0:45 | C21, C22-2 |
| 18 | T7 | **Démonstration du smart-assign** | 2:00 | C22-2 |
| 19 | T4 | L'API sécurisée, lue au filtre de l'OWASP | 0:55 | C24-1, C24-2, C24-3 |
| 20 | T4 | De l'IA locale à la monétisation | 0:55 | C22-5, C23-1, C23-2, C23-3 |
| 21 | T6 | Tester et industrialiser le back | 1:00 | C25-1, C25-2, C26-1, C26-2, C26-3 |

La diapositive 20 suit exactement l'enchaînement voulu : le modèle tourne en local donc il ne coûte
rien, ce coût marginal nul rend le modèle économique tenable, voici la tarification par siège et sa
cible, et voici comment les plans débloquent les fonctionnalités.

### Conclusion (1 min 20)

| # | Fond | Message unique | Durée | Critères visés |
|---|---|---|---|---|
| 22 | T3 | Bilan, ce que j'assume et ce que j'ai corrigé | 0:45 | Esprit critique |
| 23 | T8 | Les améliorations possibles | 0:20 | Note pédagogique p. 6 |
| 24 | T1 | Merci, questions | 0:15 | |

**Total : 19 minutes 35.** Marge de 25 secondes. Front 8:00 contre back 7:50.

> **▶ 24/07/2026 — la diapositive 19 passe de 0:55 à 1:10.** Le script y affirmait « les données
> sensibles sont chiffrées au repos », formulation qui appelle un « lesquelles ? » auquel elle ne
> survit pas : quatre colonnes le sont, l'adresse de courriel non. Le périmètre est désormais précisé
> à l'oral, dans la même logique d'anticipation que les deux catégories OWASP non couvertes annoncées
> juste après. **La marge tombe à 25 secondes** : c'est le point à surveiller au chronomètre. Si elle
> ne tient pas, la variable d'ajustement est la diapositive 23 (améliorations possibles), dont le
> contenu figure déjà au dossier.

### Les trois diapositives tampon

Le professeur limite à trois les diapositives hors grille. Retenues, dans cet ordre de probabilité :

1. Le détail des pondérations du smart-assign (0,45 sémantique, 0,22 charge, 0,15 historique, 0,10 disponibilité, 0,08 labels, bonus de montée en compétence plafonné à 15).
2. Le tableau OWASP complet, avec les deux catégories non couvertes.
3. Le RGPD et l'observabilité.

> **▶ 24/07/2026 — une réponse à préparer, sans diapositive.** Si le jury demande « comment savez-vous
> que votre intégration de paiement fonctionne ? », la réponse est meilleure que « les tests passent ».
>
> *« Je l'ai crue fonctionnelle jusqu'au 24 juillet. Les tests étaient verts, la signature vérifiée,
> l'idempotence en place. En l'exerçant avec de vrais événements Stripe pour la première fois, j'ai
> trouvé deux défauts bloquants. Le premier : la version d'API de mon compte avait dépassé celle de ma
> bibliothèque, la désérialisation échouait, et mon serveur répondait 200 sans rien faire — Stripe
> considérait chaque événement comme livré et ne rejouait jamais. Le second, que le premier masquait :
> trois colonnes sont des types énumérés PostgreSQL, et deux entités ne les déclaraient pas comme
> telles, donc aucun abonnement n'avait jamais pu être créé par le code. Les lignes en base venaient du
> jeu de données de développement. Les deux sont corrigés et la chaîne est vérifiée de bout en bout,
> idempotence comprise. »*
>
> **Pourquoi cette réponse vaut mieux qu'un succès annoncé** : elle démontre exactement ce que la note
> pédagogique appelle l'esprit critique (page 6), et elle porte une leçon transférable — *un test vert
> prouve que le code fait ce qu'on lui demande, jamais qu'on lui demande la bonne chose*. Le même angle
> mort avait été trouvé le matin même sur le chiffrement au repos.
>
> Cette réponse **ne coûte rien au chronomètre** tant qu'elle n'est pas posée. Si le candidat préfère
> l'intégrer au fil principal, la place naturelle est la diapositive 22 — mais il faudra alors retirer
> l'un des trois arbitrages, la marge n'étant que de 25 secondes.

**Argument à opposer si le nombre de diapositives hors grille est contesté** : la Note pédagogique
impose elle-même, page 5 et 6, la présentation du candidat, le parcours professionnel, le contexte,
le bilan et les améliorations possibles. Les diapositives 1, 2, 22 et 23 ne sont pas des diapositives
tampon, ce sont des diapositives exigées.

## 3. Le cahier des charges et le choix de la pile technique

Position corrigée par rapport à la v1.0. Le CDC, page 2 et 3, sous le titre « 5. Exigences
Techniques », écrit ceci :

- Back-end : PHP (Symfony) ou Node.js
- Front-end : React ou Vue.js
- Base de données : MySQL ou PostgreSQL

**Deux lignes sur trois sont respectées** : Next.js est un framework React, et la base est
PostgreSQL. Le seul point de divergence est le back-end.

Ce point ne se présente pas comme un écart mais comme **un choix technique justifié**. Le critère
C22-1 demande littéralement « un choix de technologies et frameworks back-end **adaptés** », pas un
choix conforme au cahier des charges. La grille récompense la pertinence, pas l'obéissance.

**Point tranché le 23/07/2026.** Le cadre est confirmé : **le choix technique est libre, à condition
de pouvoir l'argumenter.** Ce n'est donc pas un écart à défendre mais une décision à justifier, ce
qui est un exercice différent et plus favorable.

Une réserve subsiste néanmoins sur la **formulation** : le cahier des charges n'écrit nulle part que
ces technologies seraient données à titre indicatif. Ne pas bâtir l'argumentaire sur cette
affirmation, qui reste orale. Bâtir sur la pertinence technique.

L'argumentaire écrit se trouve désormais dans [[Journal_Decisions_ADR]], ADR-001, section
« Alternatives écartées, face au cahier des charges ». Elle manquait jusqu'au 23/07 : l'ADR
comparait Java à Quarkus et Micronaut, jamais à **Symfony ni à Node.js**, c'est-à-dire aux deux
options que le jury demandera d'écarter. Trois arguments à retenir : le cœur du produit est un
moteur d'affectation où le typage fort et les threads virtuels de Java 21 servent réellement ; le
front étant déjà en TypeScript, prendre Node aurait donné un projet mono-langage qui n'aurait rien
démontré de plus pour un titre « Full Stack » ; la contrainte dominante était la sécurité et la
traçabilité, où l'outillage Spring est intégré et éprouvé.

## 4. Chiffres vérifiés, à utiliser tels quels

> **Actualisé le 23/07/2026.** Les valeurs de couverture et de volumétrie de tests du 21/07 ont elles
> aussi vieilli : la semaine du 21 au 23 a vu 41 tests front réparés, une cinquantaine ajoutés, et
> deux classes de tests back créées. Les lignes concernées portent désormais la mesure du 23/07 ;
> l'ancienne valeur est conservée en regard, puisque c'est l'écart qui doit être connu avant l'oral.

| Indicateur | Valeur réelle | Ce qui circulait |
|---|---|---|
| Tests front | **805 unitaires** (63 fichiers), 0 échec, le 23/07 | 746, puis 706, puis 709 |
| Couverture front | **89,55 % de lignes sur le périmètre logique**, le 23/07 | « 92 % », puis 92,33 % |
| Tests back | **792 cas exécutés**, 0 échec, le 23/07 | 658, puis 670, puis 692, puis 759 |
| Couverture back | **73,71 % de lignes**, le 22/07 | 78 %, 86,1 % dans une fiche, puis 71,3 % |
| Composants front | **176 fichiers**, dont **76** primitives | 165 dont 74, puis 189 dont 77 |
| Tokens CSS | **165 déclarations** | non chiffré |
| Migrations Flyway | **72** | 68, puis 71 |
| Entités JPA | **48** | 49 (le comptage naïf inclut `AuditableEntity`, qui est un `@MappedSuperclass`) |
| Contrôleurs | **36**, pour **219** points d entree | 35, « 200+ » |

Périmètre de couverture front, à préciser systématiquement : `vitest.config.ts` n'inclut que `lib`,
`hooks` et `components/auth`. Les 47 routes et environ 180 fichiers de composants sont hors mesure,
par décision assumée et commentée dans le fichier, au motif qu'ils sont couverts par Playwright.

## 5. Le scénario de démonstration

Le seed `backend/tf-api/seed/dev_seed.sql` est exploitable tel quel : workspace `taskforce-demo`,
9 membres, 8 profils de compétences différenciés, environ 267 issues dont une ouverte sur quatre
non assignée, 12 décisions d'affectation historisées.

**Démonstration front, 1 min 55.** Connexion, tableau de bord du workspace, navigation vers un
projet, vue Kanban avec glisser-déposer, ouverture d'une issue, bascule de thème, passage en
affichage mobile. Le parcours doit faire prononcer les mots des critères : cas d'usage couverts,
navigation clavier, responsive.

**Démonstration back, 2 min 00.** Deux exécutions du smart-assign, choisies pour prouver que la
logique varie avec les données :

1. **API-4, « Rate limiting sur l'authentification »**, non assignée, priorité haute, 5 points,
   labels côté API. Marcus Webb (java, spring, sql, api, 40 h par semaine, senior, bon historique)
   doit sortir devant Lina Park (design, ui, ux, figma, 32 h).
2. **WEB-4, « Dark mode incomplet »**, labels css et ui, 3 points, sur le projet WEB qui a le mode
   montée en compétence actif. Diego Santos, junior en apprentissage de TypeScript et React, doit
   remonter avec le facteur de tâche formatrice.

Dans les deux cas, ouvrir le détail des sous-scores : score sémantique, charge, historique,
disponibilité, correspondance de labels. C'est ce qui prouve que la recommandation est auditable et
non une boîte noire.

Plan de repli : capture vidéo des deux exécutions, réalisée et testée avant le 25/09.

## 6. Visuels à produire

| Diapositive | Visuel | État |
|---|---|---|
| 3 | Diagramme C4, vue conteneurs | À exporter |
| 6 | Wireframe et écran livré, côte à côte | **À produire**, voir §7 |
| 7 | Planche du design system | À capturer |
| 8 | Taille du CSS et du bundle après build | **À mesurer**, voir §7 |
| 11 | Rapport d'accessibilité | À produire |
| 12 | Rapport SEO et tableau de bord d'audience | **À produire**, voir §7 |
| 17 | Modèle de données ciblé, 7 entités | À dessiner |
| 19 | Tableau OWASP, 10 lignes | À composer |
| 21 | Couverture et chaîne d'intégration continue | À capturer |

## 7. À faire côté produit avant la soutenance

Liste destinée au chat projet. Classée par rapport entre l'effort et le nombre de critères gagnés.

**Bloquant, sinon une diapositive entière n'a aucune preuve**

1. **Lancer un build de production du front.** `frontend/.next/` est vide et `landing-page/dist/`
   n'existe pas. Aucun fichier CSS de production n'existe sur le disque, donc la diapositive 8 ne
   peut rien montrer. Un build donne la taille réelle du CSS et du bundle, ce qui est exactement ce
   que demande C19-3, « la chaîne de build permet effectivement d'améliorer les performances ».
2. **Produire les wireframes de TaskForce.** Les 14 images de `taskforce-docs/assets/maquettes/`
   sont brandées **« TaskFlow AI »**, avec une navigation et une palette qui ne correspondent pas à
   l'application. C13-3 exige la conformité aux maquettes validées : en l'état, un juré qui ouvre le
   dossier voit une contradiction. Soit on produit les wireframes de TaskForce, soit on retire ces
   images du dossier.
3. **Relancer la couverture front.** Le rapport date du 04/07, le code a bougé les 20 et 21/07.
4. **Corriger les identifiants de prix Stripe.** `STRIPE_PRICE_ID_BASIC` et
   `STRIPE_PRICE_ID_BUSINESS` ont la **même valeur** dans les deux `.env.dev`, et
   `STRIPE_ENTERPRISE_PRICE_ID` n'est pas défini. Conséquence démontrable : un abonnement Business
   est reclassé Basic au premier événement `customer.subscription.updated`, et un paiement
   Enterprise échouerait. C'est C23-1, « l'intégration du système de paiement est fonctionnelle ».

**Critères gagnés pour un effort très faible**

5. **Rendre ESLint bloquant** dans `frontend-tests.yml` : l'étape est en `continue-on-error: true`,
   donc une erreur d'analyse statique ne casse rien. C16-1 porte précisément sur ce point.
6. **Ajouter un `dependabot.yml`.** Il n'en existe aucun, alors que la documentation en revendique
   un. C19-2 et C26-2 demandent tous deux « une gestion des dépendances est mise en œuvre ».
7. **Ajouter `npm audit` au workflow du front.** Il n'existe que sur la landing. C16-3 demande des
   composants tiers « à jour et sans vulnérabilité connue ».
8. **Ajouter le reporter `json-summary` à Vitest.** Le commentaire de couverture sur les pull
   requests lit `coverage-summary.json`, qui n'est jamais produit. La preuve d'industrialisation est
   donc invisible.
9. **Faire échouer le test axe sur `serious`, pas seulement sur `critical`.** Les défauts de
   contraste sont classés `serious` par axe : aujourd'hui ils ne font pas échouer le test, donc
   l'accessibilité des contrastes n'est pas réellement vérifiée. Le dernier passage local de ce test,
   sur la page des membres, était d'ailleurs en échec.
10. **Vérifier la variable de dépôt `E2E_ENABLED`.** Le workflow de bout en bout est gardé par
    `if: vars.E2E_ENABLED == 'true'` : s'il n'est pas activé, il ne s'exécute jamais et un job ignoré
    remonte tout de même en succès.

**Ce qui manque pour C20, aujourd'hui à zéro**

11. **Un outil de mesure d'audience.** C20-2 et C20-3 exigent un outil de mesure d'audience et de
    performance marketing, et son intégration fonctionnelle. Il n'y en a aucun. Recommandation :
    Plausible ou Matomo auto-hébergé, cohérent avec le discours RGPD et sans bandeau de cookies.
12. **Un `sitemap.xml`.** Le `robots.txt` de la landing en déclare un qui n'existe pas, donc il
    pointe vers une erreur 404.
13. **Les données structurées JSON-LD**, absentes des deux projets.
14. **La clé `site:` dans `astro.config.mjs`**, sans laquelle la balise canonique de la landing est
    relative, donc non conforme.
15. **Les métadonnées de l'application Next**, limitées à un titre et une description : ni Open
    Graph, ni robots, ni manifeste, ni canonique.

**Ce qui rendrait la partie accessibilité et performance réellement professionnelle**

16. **Mesure terrain des Core Web Vitals** avec la bibliothèque `web-vitals`, expédiée vers
    OpenTelemetry et SigNoz, qui sont déjà en place. La mesure en conditions réelles vaut mieux
    qu'un audit de laboratoire, et c'est un argument que peu de candidats tiennent.
17. **Budgets de ressources** dans la configuration Lighthouse, et audit rendu bloquant. Aujourd'hui
    Lighthouse ne tourne que sur la landing, uniquement sur les pull requests, et en
    `continue-on-error: true`, donc sans aucun pouvoir de blocage.
18. **Un passage au lecteur d'écran NVDA**, filmé, sur un parcours complet. C'est la preuve
    d'accessibilité la plus convaincante devant un professionnel.

**À trancher, car cela conditionne ce qui peut être affirmé**

19. ~~**Le seuil JaCoCo de 84 % ne s'exécute jamais.**~~ **Tranché et corrigé le 22/07/2026.**
    L'exécution `jacoco-check` n'ayant pas de phase déclarée, elle tombait en `verify` alors que la
    CI lance `mvn clean test` : la porte était donc inerte, et son seuil de 84 % décoratif. Il a été
    **abaissé à 70 %**, valeur inférieure à la couverture réelle (73,71 %), et son déclenchement
    effectif a été vérifié par un `mvn verify`. C'est l'option honnête, et elle se raconte bien :
    un seuil qu'on ne franchit pas ne prouve rien, un seuil vrai et bloquant prouve quelque chose.
    Reste à câbler `verify` dans le workflow pour que la porte s'exerce aussi en CI.
20. **L'image Docker du back est construite avec `SKIP_TESTS=true`**, et le job de publication ne
    dépend d'aucun job de test. C26-3 parle d'une chaîne de build qui améliore « les performances
    **et la sécurité** ».

## 8. Ce qu'il ne faut pas affirmer devant le jury

Établi par audit du code le 21/07/2026. Chaque ligne est une affirmation que le code contredit.

| Ne pas dire | Dire à la place |
|---|---|
| « Le smart-assign utilise pgvector et des embeddings » | Le score sémantique est demandé à un modèle de langage qui répond en JSON. La colonne `member_skill_profiles.embedding` existe mais n'est jamais lue. pgvector est utilisé, mais pour la recherche du Brain OS. |
| « Le service Python calcule le score » | Le service Python est une passerelle vers le modèle local et un calculateur d'embeddings. Ses points d'entrée smart-assign existent mais ne sont appelés par personne. |
| « Nos tests d'intégration utilisent Testcontainers » | Un vrai PostgreSQL avec pgvector, lancé en conteneur voisin, avec les vraies migrations Flyway et `ddl-auto=validate`. Testcontainers a été écarté pour incompatibilité avec le proxy Docker Desktop, et c'est documenté dans la classe socle. |
| « Nous couvrons les dix catégories de l'OWASP » | Huit sur dix. La falsification de requête côté serveur n'a aucune parade sur les webhooks sortants, et il n'y a aucune analyse de dépendances automatisée. Les deux sont assumés. |
| « Le flux OIDC est Authorization Code » | C'est un flux par mot de passe direct, choisi pour garder un formulaire de connexion sans redirection. Ce grant est déprécié par OAuth 2.1, c'est un arbitrage assumé. |
| « Les jetons sont stockés de façon sécurisée » | Jeton d'accès et de rafraîchissement en `localStorage`, sans cookie `HttpOnly`. Arbitrage assumé, corrigé dans la feuille de route. |
| « Toutes les données personnelles sont chiffrées » | Le chiffrement AES-256-GCM porte sur quatre colonnes sensibles : jetons d'intégration, configuration de connecteur, et deux champs de demande entreprise. |
| « L'OTP est un second facteur » | C'est un code à six chiffres envoyé par courriel, à l'inscription et à la réinitialisation de mot de passe. Il n'intervient pas à la connexion. |
| « Les rôles projet contrôlent les accès » | Les rôles projet servent de liste d'appartenance pour les projets privés. Le contrôle d'accès réel s'appuie sur les rôles de workspace. |
| « Les scans de sécurité tournent en intégration continue » | Trivy, Semgrep et OWASP ZAP sont lancés par un script manuel. Aucun des sept workflows n'est un workflow de sécurité. |
| « L'application est auditée par Lighthouse » | Lighthouse ne tourne que sur la landing, sur les pull requests, et sans pouvoir bloquer. |
| « Backend couvert à 78 % » | **73,71 % de lignes**, mesuré le 22/07. Le chiffre de 78 % n'a jamais été retrouvé depuis. |
| « Nos tests d'intégration utilisent Testcontainers » (2) | À ne dire nulle part : la bibliothèque n'est pas dans le `pom.xml`. Voir la ligne dédiée plus haut. |
| « Les certificats TLS sont émis par Let's Encrypt » | **Rien n'est déployé** : aucun domaine, aucune zone DNS, aucun certificat. La configuration nginx est prête et validée, elle n'est pas en service. Le dossier l'affirmait au présent, corrigé le 23/07. |
| « L'audit RGPD couvre le livrable E9 » | L'audit existant porte sur **TaskForce**. E9 demande un **cas professionnel externe**, qui n'est pas commencé. |
| « La suite front est verte » | Elle l'est : **805 tests, 0 échec, et la mesure de couverture sort en code 0**, seuils par chemin compris. Ce n'était pas le cas le matin du 23/07, `lib/utils` étant sous son seuil faute de test sur l'export CSV ; corrigé le jour même. |

Deux points ne sont **pas** des défauts et ne doivent pas être présentés comme tels, car ce sont des
décisions produit assumées : l'absence de plafond de membres par plan, qui relève d'une tarification
par siège, et l'IA disponible dès le plan gratuit, métrée par jetons plutôt que verrouillée par plan.

## 9. Suite

Une fois ce plan validé : rédaction du texte oral complet, puis liste de questions probables, puis
report dans le PowerPoint.

> Voir aussi : [[Plan_Soutenance]] pour l'historique du deck v3, et
> [[README|Matrice des 32 compétences]], dont les chiffres sont périmés au regard du §4.
