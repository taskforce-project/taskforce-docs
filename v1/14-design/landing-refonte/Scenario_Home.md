# Scénario de la home — le plan-séquence

[statut:: en cours] · [maj:: 2026-07-24] · [portee:: landing-page/src/components/site]
Parent : [[Plan_Refonte_Site]] · Règles de contenu : [[Spec_Master]] · Références visuelles : [[Design_Corpus_Guide]]

---

## 0. Le diagnostic qui a déclenché cette réécriture

La home comptait **neuf illustrations animées**. Chacune était correcte prise isolément. Ensemble, elles échouaient, pour quatre raisons mesurables :

| Défaut | Fait constaté | Conséquence |
| --- | --- | --- |
| **Neuf univers séparés** | Aucune illustration ne partageait un nom, un chiffre ou un artefact avec une autre. Une phrase dans `ContextDecay`, un « Run #145 » dans `RunTimeline`, quatre candidats dans `AssignRanking`, 128 sources dans `ContextRetrieval`. | On ne suit rien. La page se lit comme un catalogue de fonctionnalités animées, pas comme une démonstration. |
| **Tout boucle** | Les neuf composants tournaient en boucle infinie. | Une boucle n'atterrit jamais : on l'attrape au milieu, on ignore où l'histoire commence, et l'état final (celui qui porte le message) passe comme les autres. |
| **Aucun point focal** | Sur un écran de 900 px de haut, jusqu'à trois cartes s'animaient simultanément. | Le regard n'est plus guidé. La charge cognitive est subie. |
| **Des schémas, pas des écrans** | Toutes utilisaient le même châssis : carte blanche bordée, lignes icône plus texte, barre de fenêtre macOS à trois pastilles. | Personne ne croit que le produit existe. Une barre macOS est le signe le plus sûr qu'on regarde un dessin. |

Le tempo était en plus uniforme : 1500 ms par étape partout. Or un moment « Aha » se fabrique avec un **silence avant**, pas avec une étape de plus.

---

## 1. Le principe : la home est un seul run, filmé en plan-séquence

Même workspace, mêmes personnes, mêmes chiffres, du hero jusqu'au dashboard final. **Chaque section est un angle de caméra différent sur le même run.** À la fin, la demande arrivée du support en haut de page se retrouve comme un point identifiable sur la courbe de lead time.

C'est la grammaire des vidéos de lancement Linear et Raycast : une seule prise. La continuité n'est pas un effet de style, c'est **le mécanisme de crédibilité** : quand le même identifiant de run réapparaît quatre écrans plus bas, le visiteur cesse de lire une brochure et commence à regarder un logiciel.

### Le décor partagé

Source unique : `landing-page/src/lib/story.ts`. **Aucune scène ne code en dur un nom, un horaire ou un chiffre.**

| Élément | Valeur |
| --- | --- |
| Workspace | Northwind |
| Projet | Customer Portal |
| Run | #147, « Let customers export their invoices » |
| Origine | Message de Sam Okonkwo (Support), lundi 09:14 |
| Casting | Maya Ferrand (Produit), Léo Bianchi (Backend), Inès Roussel (Frontend), et **You** |
| Chiffres | lead time 1,8 j contre 6,5 j de médiane, 1 renvoi, 4 issues |

Deux choix délibérés :

1. **La demande vient du support, pas d'un ticket technique.** « Permettre aux clients d'exporter leurs factures » se comprend sans être développeur. C'est ce qui permet de vendre au-delà de l'ingénierie (décision D10) sans inventer des écrans pour des métiers qu'on n'a jamais livrés, ce que la règle d'honnêteté interdit.
2. **Le visiteur est le seul avatar coloré de l'écran.** Les autres sont en gris. « You » porte le bleu de marque. Le protagoniste, c'est la personne qui regarde.

### Le fil rouge, en une phrase

> Sam signale un besoin le lundi matin. Un agent le transforme en spec. **Vous la refusez.** Votre commentaire devient un critère d'acceptation. Le run repart, se découpe en issues, part vers les bonnes personnes, et livre en 1,8 jour.

Tout le reste de la page est la mise en scène de cette phrase.

---

## 2. Les règles de motion

Ce sont des contraintes de production, pas des intentions.

### R1. Une scène est une partition, pas une boucle

Primitive unique : `useScene(beats)` dans `landing-page/src/lib/useScene.ts`. Une scène reçoit une liste de durées, démarre quand elle entre à l'écran, se joue **une fois**, et **se fige sur son état final**.

L'état final est le message. Une boucle le noie ; un arrêt le grave.

### R2. Un temps long est un silence, et le silence est là où on regarde

Le tempo n'est jamais régulier. La partition du hero est `900, 1900, 600, 700`. Le 1900 n'est pas une étape lente : c'est la respiration qui rend la bascule suivante lisible.

### R3. Un seul point focal à la fois

Deux animations importantes ne démarrent jamais ensemble. À l'intérieur d'une scène, quand un moment doit porter, **le reste du panneau descend à 40 % d'opacité**. Ce n'est pas un effet, c'est de la mise au point.

### R4. Une animation ne change jamais la hauteur de son conteneur

Règle déjà en vigueur, désormais outillée. Deux techniques admises :

- **Réserver** : le texte complet est rendu en `invisible` derrière le texte tapé, ce qui fige la hauteur malgré le retour à la ligne.
- **Superposer** : la barre d'approbation est en position absolue et le corps réserve sa hauteur par un `padding-bottom`. Elle remonte **par-dessus** le contenu ; la fenêtre ne bouge pas d'un pixel.

Interdit : `grid-rows-[0fr]` vers `grid-rows-[1fr]`, qui est précisément ce qui faisait varier `RunTimeline` de 150 px.

### R5. Une scène atterrit, mais le produit continue de respirer

Contradiction apparente avec « jamais un écran figé ». Résolution : après l'atterrissage, **exactement deux éléments** restent vivants, et ce sont les mêmes sur toutes les scènes :

- le **chronomètre du run**, qui avance d'une seconde par seconde ;
- la **présence**, une pastille verte qui bat toutes les 2,4 s à côté des avatars.

C'est suffisant pour dire « ce logiciel tourne » et trop discret pour reprendre l'attention.

### R6. Frapper plutôt qu'apparaître

Un fondu dit « voici du contenu ». Une frappe caractère par caractère dit « **quelque chose est en train de l'écrire** ». C'est la seule différence, et c'est exactement le sens voulu.

### R7. `prefers-reduced-motion` saute à l'état final

Pas de dégradé, pas de version allégée : l'état final, directement. La personne reçoit le message, pas le mouvement (WCAG 2.3.3).

---

## 3. Les scènes

### Scène 1 — Hero : « le logiciel travaille déjà, et il vous attend »

**État :** livrée (`home/Hero.tsx`).

**1. Message principal (3 à 5 s).** Ce produit exécute du travail réel, et il s'arrête tout seul devant un humain.

**2. Problème illustré.** Un hero de produit IA est presque toujours soit une capture figée, soit du décor animé (dégradés, cartes qui flottent). Dans les deux cas on ne peut pas savoir si quelque chose fonctionne. On ne montre donc pas le produit : on montre **le travail en train de se faire**.

**3. Démonstration visuelle.** Une fenêtre TaskForce, avec barre latérale, fil d'Ariane `Northwind / Customer Portal / Run #147`, présence et chronomètre. À gauche les sept checkpoints, à droite l'artefact en cours d'écriture, précédé du message de Sam qui a déclenché le run.

**4. Progression.**

| t | Ce qui se passe |
| --- | --- |
| 0,0 s | La fenêtre monte. Un run est ouvert, l'étape 2 tourne. |
| 0,9 s | Le troisième critère d'acceptation s'écrit, caractère par caractère, curseur visible. |
| 2,8 s | L'étape bascule. **Pas en vert : en ambre**, « ready ». La jauge passe de 1/7 à 2/7. |
| 3,4 s | La barre d'approbation remonte du bas de la fenêtre, avec son ombre portée. |
| 4,1 s | Le bouton `Approve` reçoit **un seul** anneau d'attention. Puis plus rien. |

**5. Moment « Aha ».** La bascule en ambre à 2,8 s. On attend le vert. Le produit refuse d'avancer, et cela se voit **avant d'avoir lu une ligne de texte**.

**6. Pourquoi mieux qu'une animation classique.** Trois raisons. La scène anime le travail et non le décor. Elle atterrit sur la thèse du produit au lieu de boucler dans le vide. Et elle plante le fil narratif (le message de Sam) que les cinq sections suivantes vont dérouler.

**Décision associée : suppression des onglets de persona.** Ils coupaient l'attention en quatre dès la première seconde et signalaient « composant » plutôt que « produit ». Ni Linear, ni Raycast, ni Stripe n'ont d'onglets dans leur hero. Une scène, un point focal.

---

### Scène 2 — Le problème : « la même demande, recopiée quatre fois »

**État :** à faire. Remplace `ContextDecay`.

**1. Message principal.** Rien n'est perdu volontairement. C'est la recopie qui perd, et cela finit par coûter.

**2. Problème illustré.** Une décision, sa raison et le travail qu'elle produit atterrissent dans trois outils différents. Le jour où quelqu'un a besoin de la raison, c'est la seule chose qui n'a jamais été écrite.

**3. Démonstration visuelle.** Le message de Sam, littéralement le même qu'au hero, traverse quatre surfaces : Slack, la spec Notion, l'issue Linear, la description de PR. À chaque saut, des mots disparaissent. Pas d'abstraction, pas de barre de rétention : **on voit le texte se raccourcir**.

**4. Progression.** Un saut toutes les 1,2 s, avec les mots perdus qui s'effacent (et non qui glissent : ils ne vont nulle part). Après le quatrième saut, **1,5 s de silence total**. Puis, dans ce silence, un ticket de bug apparaît, daté de trois semaines plus tard, citant exactement la clause tombée en route.

**5. Moment « Aha ».** Le ticket de bug. La perte de contexte cesse d'être un concept et devient une facture.

**6. Pourquoi mieux.** L'ancienne version affichait des pourcentages de rétention (100, 55, 20, 0). Un pourcentage est une affirmation, pas une preuve. Un ticket de bug qui cite la phrase manquante est un souvenir : le visiteur reconnaît sa propre semaine. Et c'est la même phrase que l'agent, lui, ne perdra pas dans la scène 3.

---

### Scène 3 — Le run : la scène centrale

**État :** à faire. **Fusionne et remplace `RunTimeline`, `ApprovalLoop`, `AgentHandoff` et `ContextRetrieval`.** Quatre composants, une scène.

C'est l'animation la plus longue de la page (environ 14 s) et la seule qui mérite ce budget.

**1. Message principal.** Votre phrase devient une ligne de la spec. Le run ne vous contourne pas, il vous intègre.

**2. Problème illustré.** « Human in the loop » est devenu un slogan sans démonstration. Presque personne ne montre ce qui se passe **quand l'humain dit non**.

**3. Démonstration visuelle.** La même fenêtre qu'au hero, mais en grand. Trois actes dans un seul plan.

**4. Progression.**

- **Acte A, la matière (0 à 4 s).** L'agent lit trois sources du workspace, dont un ADR, sur les 128 du projet. Les sources retenues portent leur score ; les autres s'éteignent. Puis la spec s'écrit, avec ses citations.
- **Acte B, le silence (4 à 7,5 s).** Le run s'arrête. **Tout le panneau descend à 40 % sauf la barre d'approbation.** `Request changes` s'active. Un commentaire s'écrit, mot pour mot : « Invoices before 2024 live in the old billing system. »
- **Acte C, la conséquence (7,5 à 14 s).** L'étape se rejoue. **Un quatrième critère apparaît, en vert, rédigé à partir de votre commentaire.** Approuvé. Le run repart, et le passage de rôle CPO vers CTO puis COO se lit comme un changement de couloir dans la gouttière de gauche, sans jamais devenir une animation à part entière.

**5. Moment « Aha ».** Le critère 4. Votre phrase, reformulée en critère d'acceptation, en vert, quatre secondes après que vous l'avez écrite. C'est le produit entier en une image.

**6. Pourquoi mieux.** Une timeline qui se remplit de gauche à droite montre **un processus** : c'est décoratif, tout le monde en a une. Ici on montre **une conséquence de l'humain**, ce qui est le seul argument que les concurrents ne peuvent pas recopier en un trimestre. Le silence de l'acte B est le seul moment calme de la page : c'est précisément ce qui fait atterrir l'acte C. Et une scène qui répond à quatre questions vaut mieux que quatre cartes qui en répondent chacune à une.

---

### Scène 4 — Smart Assign : une micro-interaction, pas une animation

**État :** à faire. Remplace `AssignRanking`.

**1. Message principal.** L'issue part vers la bonne personne, et on peut demander pourquoi.

**2. Problème illustré.** L'affectation se décide en réunion de triage, sur la base de qui a parlé en dernier.

**3. Démonstration visuelle.** Fin du run : quatre issues sortent du découpage et **rejoignent chacune un avatar**, en 2 s, dans la fenêtre. Puis la scène s'arrête. Le visiteur peut alors **cliquer une issue** et voir les cinq signaux qui ont produit ce choix.

**4. Progression.** Deux secondes automatiques, puis rien. Le reste est à la main du visiteur.

**5. Moment « Aha ».** Le panneau « pourquoi » : ce n'est pas un score opaque, ce sont cinq signaux nommés, et un bouton pour réaffecter.

**6. Pourquoi mieux.** L'ancienne version faisait courir quatre barres de score en boucle, ce qui est une course de chevaux, pas une démonstration. Une chose qu'on peut **toucher** est retenue bien plus longtemps qu'une chose qu'on regarde, et c'est la signature des pages Linear. Cela réduit aussi d'une animation automatique le budget d'attention de la page.

---

### Scène 5 — La conséquence : le run atterrit dans le dashboard

**État :** à faire. Réécrit `DeliveryInsights` autour du run #147.

**1. Message principal.** Ça se voit dans les chiffres, et on peut pointer lequel.

**2. Problème illustré.** Tout le monde promet un gain de vélocité. Personne ne montre d'où vient le point.

**3. Démonstration visuelle.** Une courbe de lead time. Elle est déjà tracée quand la scène démarre. **Un dernier point arrive**, se pose à 1,8 jour, et porte une étiquette : `Run #147`.

**4. Progression.** La courbe est calme, statique. Le point arrive seul, avec un léger dépassement puis stabilisation. L'étiquette se pose 400 ms après lui. Rien d'autre ne bouge.

**5. Moment « Aha ».** L'étiquette. Le visiteur vient de passer trois écrans avec ce run ; il reconnaît le point.

**6. Pourquoi mieux.** Une courbe qui descend est de la décoration ; tout le monde sait qu'on l'a dessinée dans le sens qui arrange. Une courbe où **on reconnaît un point précis dont on a vu toute l'histoire** est une preuve. C'est aussi ce qui referme le plan-séquence : la boucle ouverte par le message de Sam se ferme ici.

---

### Zones interactives, sans animation automatique

Deux blocs restent, volontairement dépourvus d'autoplay. Après cinq scènes, la variété de forme fait autant pour la lecture que la variété de contenu.

- **Modèles et souveraineté.** Un interrupteur que le visiteur bascule : local ou hébergé. Deux lignes du run changent de destination et la mention « Leaves your network » passe de non à oui. Aucune mention de prix (contrainte utilisateur explicite). Remplace `ModelRouting` et son autoplay.
- **Catalogue d'intégrations.** Recherche, dix filtres, 58 outils, compteur, état vide. Déjà livré et conservé tel quel.

Restent statiques et denses : maturité du produit, conformité, direction, CTA.

---

## 4. L'audit : ce qui disparaît

| Composant | Sort | Motif |
| --- | --- | --- |
| `RunTimeline` | Fusionné dans la scène 3 | Montrait le processus, pas la conséquence |
| `ApprovalLoop` | Fusionné dans la scène 3 | L'approbation n'est pas un sujet séparé, c'est le cœur du run |
| `AgentHandoff` | Fusionné dans la scène 3 (gouttière) | Le passage de rôle est un détail du run, pas une section |
| `ContextRetrieval` | Fusionné dans la scène 3 (acte A) | La récupération sert la spec, elle ne vit pas seule |
| `AssignRanking` | Devient une micro-interaction | Une course de barres n'est pas une démonstration |
| `ModelRouting` | Devient un interrupteur | Un argument de souveraineté se teste, il ne se regarde pas |
| `ContextDecay` | Réécrit (scène 2) | Bon principe, conséquence manquante |
| `DeliveryInsights` | Réécrit (scène 5) | Bon principe, aucun lien avec le reste de la page |
| `CapabilityPairs` | **Supprimé** | C'est le schéma d'un argument. L'argument survit très bien en texte, et c'est le premier composant qu'un designer senior couperait. |
| `IntegrationCatalogue` | Conservé | Zone utilisable, déjà au niveau |

**Compte final : 9 animations automatiques deviennent 5 scènes et 2 zones interactives.**

---

## 5. Le test de sortie

Avant de retenir une scène, trois questions. Une réponse négative annule la scène.

1. Est-ce qu'un designer produit senior chez Linear la garderait ?
2. Est-ce qu'elle montre une **conséquence**, ou seulement un mécanisme ?
3. Est-ce que je comprends le bénéfice **sans lire le texte** de la section ?

Et une vérification mécanique, à chaque scène livrée : hauteur du conteneur mesurée à chaque battement sur un cycle complet, amplitude attendue **0 px**.
