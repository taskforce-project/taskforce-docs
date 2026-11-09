---
id: conseil-seance-2026-11-09-atelier-recette-113
title: "Séance n°20 du 09/11/2026 : l'atelier de la recette 1.13 (la barre, la conversation, la mission, les volets, le banc)"
doc_type: pv-seance
statut: active
date: "09/11/2026"
auteur: Pierre MICHEL
formation: restreinte
tags: [recherche, conseil, seance, design, composeur, mission, workflow, diff, recette]
related:
  - "../README.md"
  - "./2026-11-05-atelier-fenetre.md"
  - "./2026-11-08-atelier-sobriete-banc-voix.md"
  - "../../experiences/Experiences.md"
  - "../../../v1/13-roadmap/Roadmap_Backlog.md"
---

# Séance n°20 du 09/11/2026 : l'atelier de la recette 1.13

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle, et les décisions de Jobs sont celles d'un personnage simulé.

## Résumé

La Présidence a joué la recette 1.13 sur l'app desktop 1.10.0 : 42 étapes, 28 OK, 11 KO, 2 sautées, et un bilan d'une ligne :
« bon les gros pb c'est tjr dans l'UI/UX de toute facon, apres cote infra et tout ca parait plutot good ». Elle donne la
direction : Claude Desktop et Dust, avec l'expérience du Mac et de Raycast, et demande une passe sans tout retester.

L'atelier adopte douze recommandations. Une grammaire commune : on prend la structure de ces références, jamais leur identité.
La barre de saisie devient celle qu'on connaît : elle s'agrandit, un « + » pour joindre, le modèle et le projet visibles sous la
boîte, un bouton pour arrêter, une file pour les messages suivants. Une conversation dit où elle travaille, et demande quand elle
ne sait pas. Une seule voix parle. Une réponse replie son travail en une ligne. La mission cesse d'être un journal de commandes :
cinq étapes en phrases, les changements fichier par fichier avec leurs lignes ajoutées et retirées, un retour en arrière, et un
agent qui rend des comptes comme un junior à un senior.

Atul Gawande, contradicteur, refuse un agent qui demande à chaque pas : on ne garde que deux points de pause, au plan quand il
engage beaucoup, et à la remise. Kenza Ait Si Abbou obtient que `@` et `/` restent des raccourcis jamais demandés. Le dossier
établit que deux KO n'étaient pas de l'interface : un plafond de 4 000 caractères refusait les longs messages avant le budget de
contexte, et les « unexpected error » du banc étaient des délais dépassés.

Douze recommandations, R133 à R144, à l'unanimité des sept, R140 au second tour.

## Saisine, formation, règle de vote

- **Saisine** (Présidence, 09/11/2026), dans la fiche de recette et en conversation :
  - « bon les gros pb c'est tjr dans l'UI/UX de toute facon, apres cote infra et tout ca parait plutot good, j'essaie de te faire
    confiance de toute facon on verra ca sur des sujets et projet complet en testant » ;
  - sur la vue d'une mission : « y a trop d'info faudrait pas cacher tout ca genre c'est le but que l utilisateur comprenne ce qu'il
    se passe et qu'il puisse avoir les preuves et tout mais la c'est trop tech, mm moi je comprends rien quand je regarde en 2 coups
    doeil, montrer un workflow par exemple » ; « voir le workflow principale manipulable a chaque etape, voir les diff dans les
    fichier editer le nombre de ligne ajouter, enlever, pouvoir revert corriger bref vraiment un truc de ouf booster, l'ingenieur
    bosse avec l'IA, pas l'inverse » ; « COmme un junior d'un metier qui demande a un senior en permanence quoi. On pourrait limite
    le voir etider en direct quoi si possible » ;
  - sur la barre : « le + je m'atend plus a un menu style claude » ; « stop avec les commandes @ / ou autre, les utilisateurs doivent
    les retenir et c'est pas des dev » ;
  - sur le projet : « on pourrait faire comme CLaude, savoir dans quel dossier on travail sur le PC et/ou dans quel projet le chat
    doit travailler tu vois ? » ;
  - la direction : « tu peux t'inspirer de Claude Desktop et Dust par exemple comme c'est ma DA globalement, avec experience
    Mac/Raycast/Apple evidemment » ; « je suis pas oblige de tout retester tu sais si tu corrige je fais globalement confiance, on
    reglera les details pendant l utilisation sur un test final avant grosse release majeur et aller agro des clients potentiels
    avec ca ».
- **Horizon** : une passe maintenant, un test final de la Présidence sur un vrai projet avant la release majeure.
- **Formation** : restreinte (7), l'équipe de Jobs, plus un membre par pôle.
  - Impulsion : Steve Jobs, qui tranche par délégation (la Présidence : « faut demande a Jobs et l'equipe dedie »).
  - Pont : Kenza Ait Si Abbou (quelqu'un qui ne code pas).
  - Design : Karri Saarinen, Don Norman, Julie Zhuo.
  - Science : Atul Gawande (les listes de vérification, les points de pause).
  - Harmonie : Nandan Nilekani (des outils pour des gens qui ne sont pas du métier).
- **Ordre de parole**, tiré au sort à 11:27 UTC : Nandan Nilekani, Steve Jobs, Karri Saarinen, Don Norman, Atul Gawande, Kenza Ait Si
  Abbou, Julie Zhuo.
- **Contradicteur** : Atul Gawande.
- **Règle de vote** (charte §6.5) : 90 % des présents, donc l'unanimité à sept.
- **Fiches** : à jour (moins de 30 jours) : Norman, Saarinen et Zhuo au 28/10/2026, Ait Si Abbou au 26/10, Gawande et Nilekani au
  21/10 ; Jobs, siège historique, sans nouvelle source. Aucune fiche rafraîchie.

## Dossier

### 1. La recette `[ÉTABLI]`

| Sujet | Étapes | Ce que la Présidence a vu |
| --- | --- | --- |
| La barre | 4, 12, 35, 37 | Pas de retour à la ligne ; un « + » qui ne joint qu'issue et projet ; impossible d'arrêter une demande ; le modèle ne se change pas facilement et rien ne dit lequel répond |
| Le projet | 14, 15 | Une issue préparée dans le projet de l'écran sans que personne l'ait dit ; après « tu t'es trompé de projet », la même carte, avec une description inventée ; un dépôt qu'on ne peut pas créer |
| La voix | 14 | « jsp pk il parle au nom de Taskforce, c'est Cortex ou un autre nom » |
| La réponse | 9, 16, 36 | « Je sais tjr pas c'est quoi les sources » ; le formulaire du cas de test : « Oula » ; `/compact` : « feedback pas clair », « la ca supp tout le context ??? » |
| La mission | 8, 10, 20 | Vingt-quatre lignes de commandes, des `sha256`, des noms d'outils |
| Les volets | 5, 18, 21 | Un tableau à colonnes `Type`, `Signal`, `Op`, un mot `Ack` ; « interface de search naze » |
| Le banc | 23, 27, 29 | Il plaît (« J'aime les notations »), mais « An unexpected error occurred », deux modèles obligatoires, « models c'est quoi ? », « history je vois que dalle » |
| L'attente | 2, 30 | Le redémarrage ferme l'app sans écran ; « pk je dois dl un truc c'est chelou ? » |
| Les noms | 7, 40 | Le logo de Claude, « ca fait 15 fois que je demande » ; « Agent Trial ? C'est quoi ca ? » |

### 2. Ce que les journaux et le code disent `[ÉTABLI]`

- **Étapes 35 et 38.** Le journal du backend dit, à 00:59:11 : `Validation error: {message=[size must be between 0 and 4000]}`.
  `AssistantController` refuse tout message de plus de 4 000 caractères. Le budget de contexte de la 1.13 n'a donc jamais vu le texte
  de la Présidence, et le front a répondu « Sorry, I couldn't answer ».
- **Étape 23.** Quatre appels au modèle finissent en `HttpTimeoutException` entre 00:26 et 00:44 et remontent en `Unexpected error`.
  Un modèle de 14 milliards de paramètres (9,3 Go) ne tient pas dans une carte de 8 Go.
- **Étape 2.** Entre la fermeture de l'app (23:06:32 UTC) et la copie de la base par la nouvelle version (23:09:04 UTC) : 2 min 32 s,
  avec pour seul signe deux notifications Windows (`desktop/src/updater.ts`).
- **Étape 4.** Le champ du compositeur est un `<input>` : une seule ligne, par construction.
- **Étape 14.** `ProjectGestures.java` dit lui-même « TaskForce can't create a repository here ».
- **Étape 41**, vérifiée à la demande de la Présidence : trois sauvegardes, dont celle d'avant la 1.10.0.
- **E15**, par sa dictée réelle : 222 ms pour 4,3 s de parole, 202 ms pour 3,8 s, 168 ms pour 2,6 s ; 2,7 s pour 44 s de parole.

### 3. Les références `[ÉTABLI]`

- **Claude Code Desktop** ([documentation](https://code.claude.com/docs/en/desktop)) : un bouton « + » pour les fichiers, les compétences, les connecteurs et
  les plugins ; sous la boîte, une rangée : environnement, dossier du projet, mode de permission, modèle, anneau d'usage ; le bouton
  d'arrêt ; un message tapé pendant le travail attend l'étape suivante ; un compte `+12 -1` qui ouvre le diff ; un commentaire sur une
  ligne du diff, auquel l'agent répond par un nouveau diff ; trois modes de lecture, dont un où les outils sont repliés.
- **Dust** ([documentation](https://docs.dust.tt/docs/user-documentation/agents/skills/skills-overview)) : la ligne « Completed in N sec » ouvre le panneau de détail ; le trombone joint
  des documents ; l'indicateur de contexte vit dans la barre.
- Les captures de Mobbin demandent un abonnement : le dossier s'appuie sur ces documentations.

### 4. Les décisions en vigueur

R15 (on ne montre que ce qui marche) ; R116 (TaskForce signe la correction d'une phrase fausse) ; R123 et R124 (la conversation, le
premier regard) ; R126 (la mise à jour sans fenêtre Windows) ; R129 (une ligne par chose, le nom au survol) ; R130 (Progress) ;
R53 (le logo : en attente).

## Tour de table `[HYPOTHÈSE]`

- **Nandan Nilekani** (Harmonie) : le mot « Sources » n'a de sens que pour qui a déjà construit un moteur de recherche. Un outil pour des
  gens qui ne sont pas du métier se juge à ce qu'ils n'ont pas à apprendre. *Sa recommandation : aucun mot interne à l'écran, jamais.*
- **Steve Jobs** (Impulsion) : la Présidence a lu vingt-quatre lignes et n'a rien compris, elle qui a construit le produit. Ce n'est pas
  un défaut de présentation, c'est l'absence d'histoire. Une mission raconte quelque chose : elle a compris, elle a prévu, elle a fait,
  elle a vérifié, elle rend. *Sa recommandation : cinq étapes, des phrases, et les preuves derrière.*
- **Karri Saarinen** (Design) : la barre est l'objet le plus touché de l'app. Il n'y a rien à inventer : les gens savent déjà s'en servir
  ailleurs. Il faut que les contrôles existent là où la main les cherche. *Sa recommandation : la structure qu'on connaît, à la
  densité de la maison.*
- **Don Norman** (Design) : une erreur sans cause apprend seulement à ne plus essayer. « Sorry, I couldn't answer » cachait un refus de
  taille, « unexpected error » un délai. *Sa recommandation : chaque échec dit ce qui s'est passé et quoi faire.*
- **Atul Gawande** (Science, contradicteur) : un chirurgien ne s'arrête pas à chaque geste, il s'arrête aux moments où une erreur coûte
  cher. Un junior qui demande en permanence épuise son senior. *Sa recommandation : peu de points de pause, placés là où ils
  changent quelque chose.*
- **Kenza Ait Si Abbou** (Pont) : ce qu'il faut retenir exclut ceux qui ne l'ont pas appris. `@` et `/` peuvent exister, mais personne ne
  doit en avoir besoin. *Sa recommandation : tout se fait au clic et à la parole, les raccourcis en plus.*
- **Julie Zhuo** (Design) : une conversation qui agit sur un projet sans le montrer trompe même quand elle a raison. *Sa recommandation :
  l'endroit où l'on travaille est toujours visible et toujours modifiable.*

## Confrontation `[HYPOTHÈSE]`

1. **Tout cacher ou tout montrer ?** La Présidence demande les deux : comprendre en deux coups d'œil et avoir les preuves. Jobs replie
   tout ; Nilekani rappelle qu'on doit pouvoir vérifier sans demander. Accord : une phrase d'abord, le détail à un clic, les commandes à
   deux, et rien de supprimé.
2. **Le junior qui demande sans cesse.** Jobs lit « en permanence » au pied de la lettre : l'agent dit où il en est à chaque pas. Gawande
   répond qu'une demande qui n'attend pas de réponse est du bruit, et qu'une demande qui bloque à chaque pas tue l'autonomie (premier
   tour de R140 : 5 pour, 2 contre). Amendement : l'agent raconte en continu sans rien demander ; il n'attend qu'à deux moments.
3. **`@` et `/` : les retirer ?** Saarinen tient à ces raccourcis pour qui va vite. Ait Si Abbou accepte, s'ils ne sont jamais annoncés.
4. **Le projet, deviné ou demandé ?** Zhuo veut qu'on ne devine jamais. Saarinen répond qu'une question à chaque issue est insupportable.
   Accord : le projet de la conversation se voit dans la rangée et sert par défaut ; sans projet, Cortex demande.
5. **Une voix ou deux ?** Norman rappelle R116 : TaskForce signe quand il corrige le modèle. La Présidence ne comprend pas qui parle. Accord :
   tout est dit par Cortex, sauf la correction d'une phrase fausse, qui reste signée.

## Recommandations `[HYPOTHÈSE]`

### R133. La grammaire : la structure de Claude Desktop et de Dust, le calme du Mac, jamais leur identité

- **Quoi** : une règle pour tout écran :
  - aucun mot interne à l'écran (nom d'outil, code d'erreur, identifiant, empreinte) ;
  - une phrase d'abord, le détail à un clic, le brut à deux, rien de supprimé ;
  - un dialogue a une colonne, ses libellés au-dessus des champs, une action principale, jamais de tableau ; trois largeurs ;
  - ce qui attend se montre là où l'on regarde, sans déplacer ni faire défiler la page ;
  - un échec dit ce qui s'est passé et quoi faire ;
  - la police, les couleurs et le logo restent ceux de TaskForce.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : aucun nom d'outil ni `sha256` au premier regard sur les écrans de la recette.
- **Signal d'arrêt** : une preuve que la Présidence ne retrouve plus.

### R134. La barre de saisie

- **Quoi** : le texte passe à la ligne, jusqu'à 17 lignes, puis défile ; le « + » ouvre un menu (fichiers, issue, projet, connecteurs), et les
  fichiers se glissent aussi dans la boîte ; le modèle se choisit sous la boîte et dit celui qui répond ; le bouton d'envoi devient un bouton
  d'arrêt pendant le travail ; un message envoyé pendant le travail attend son tour, visible et retirable ; `@` et `/` restent, sans jamais être
  annoncés.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : changer de modèle en un clic, arrêter une réponse en un clic, écrire vingt lignes sans perdre le début.
- **Signal d'arrêt** : un message mis en file et envoyé sans que la personne le voie partir.

### R135. Une conversation dit où elle travaille

- **Quoi** : le projet de la conversation se voit dans la rangée sous la boîte et se change d'un clic, « No project » compris. Il sert par défaut.
  Sans projet, et quand un geste en demande un, Cortex demande lequel, par une carte. L'écran ouvert renseigne Cortex, il ne décide plus.
  « Tu t'es trompé de projet » ouvre le choix du projet. La création d'un projet propose de créer son dépôt quand GitHub le permet.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : le cas de l'étape 15 rejoué : une question, pas une carte dans un projet supposé.
- **Signal d'arrêt** : la question revient alors que le projet est visible.

### R136. Une seule voix

- **Quoi** : tout ce qui se dit dans la conversation est dit par Cortex, questions comprises. TaskForce ne signe que la correction d'une phrase fausse
  (R116) et ce qui parle du modèle (« Answered by… »).
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : aucune carte de question signée TaskForce.
- **Signal d'arrêt** : une correction de TaskForce prise pour une phrase de Cortex.

### R137. La réponse replie son travail

- **Quoi** : pendant le travail, une ligne dit ce qui se passe ; à la fin, « Worked for 8 s » et un chevron, à la manière de Dust. Dépliée, elle dit en
  phrases ce qui a été lu et fait. Le mot « Sources » disparaît : la ligne grise dit « read 5 notes », et un clic les nomme. Sous la réponse, au survol :
  copier, bien, pas bien. « Pas bien » demande une phrase : ce qu'il aurait fallu. Le formulaire du cas de test passe sous « Advanced ».
  Un long texte collé se replie dans sa bulle.
  `/compact` dit qu'il travaille, ne fait pas défiler, laisse le fil lisible, montre le résumé d'un clic et remet la jauge à sa nouvelle valeur.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : une réponse sans outil ne montre que son texte et sa ligne grise.
- **Signal d'arrêt** : la Présidence cherche ce que Cortex a lu sans le trouver.

### R138. La mission est un déroulé

- **Quoi** : cinq étapes, toujours les mêmes : Understand, Plan, Do, Check, Hand over. Chacune porte une phrase et son état, et se déplie en phrases du
  métier (« Read the issue », « Searched your notes for… »). Un interrupteur montre les commandes. La preuve se replie en une ligne : le nombre d'événements,
  scellés, et le téléchargement. La même chose se voit dans la conversation en plus petit ; la conversation ne remplace pas le déroulé.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : la mission de l'étape 8 se lit en dix secondes par quelqu'un qui ne code pas.
- **Signal d'arrêt** : une étape vide ou fausse pendant le travail.

### R139. Les changements sous les yeux

- **Quoi** : les fichiers touchés, chacun avec ses lignes ajoutées et retirées, pendant le travail et après, sans attendre une pull request ; un clic ouvre son
  diff ; un fichier se remet comme avant ; un commentaire sur une ligne repart à l'agent. Ce qui n'est pas prêt ne s'affiche pas (R15).
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : une mission réelle : la liste bouge pendant qu'elle travaille, un fichier est remis, un commentaire produit un nouveau diff.
- **Signal d'arrêt** : un compte de lignes faux, ou un retour en arrière qui touche autre chose.

### R140. L'agent rend des comptes (second tour)

- **Quoi** : l'agent raconte en continu, sans rien demander ; il n'attend qu'à deux points de pause : son plan, quand il engage beaucoup, et la remise. La remise est
  écrite à la première personne, en trois parties : ce que j'ai fait, ce que tu devrais vérifier, ce dont je ne suis pas sûr. Une correction tapée pendant le
  travail lui parvient à l'étape suivante, si l'agent le permet.
- **Premier tour** (« à chaque étape, l'agent demande ») : 5 pour, 2 contre (Gawande, Zhuo). **Second tour**, amendé : les sept.
- **Preuve en dix jours** : la Présidence dit avoir su quoi vérifier sans lire le journal.
- **Signal d'arrêt** : on approuve sans lire.

### R141. Les listes et les volets

- **Quoi** : « Waiting for you » et les alertes sont des listes, une phrase par ligne, regroupées (ce qui attend, ce qui s'est passé, les alertes), plus de tableau ni
  de colonne `Op`, plus de `Ack`. Le rail de droite dit pour chaque carte ce qu'elle apporte, sans jargon. Ctrl+K devient une vraie palette : grande, en sections,
  au clavier, qui cherche aussi dans les notes.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : aucun tableau dans un volet de moins de 720 px.
- **Signal d'arrêt** : une action qui ne se retrouve plus.

### R142. Le banc dit ce qu'il mesure

- **Quoi** : les modèles passent l'un après l'autre ; un délai dépassé est un verdict (« Too slow here »), jamais une erreur, et le passage continue ; chaque modèle a sa
  description (famille, taille, ce que veulent dire `base` et `instruct`, s'il tient dans la carte graphique) ; un modèle incapable de discuter le dit au lieu d'échouer ;
  « Models » et « Benchmark » deviennent un seul onglet ; l'essai à l'aveugle accepte un seul modèle ; « History » vide dit quoi faire. Les agents connectés (Claude Code,
  Copilot) viendront après.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : tout passer d'un coup sur les sept modèles sans une erreur.
- **Signal d'arrêt** : un verdict « Too slow » pris pour un mauvais modèle.

### R143. Ce qui fait attendre se voit

- **Quoi** : du clic sur `Restart now` à la réouverture, une fenêtre de TaskForce dit ce qui se passe, à la place des notifications Windows. Le modèle de voix se prépare seul,
  en arrière-plan, sans étape à valider. Un message trop long pour le modèle obtient la réponse prévue par la 1.13 : le plafond de 4 000 caractères disparaît.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : une mise à jour réelle sans un instant sans TaskForce à l'écran.
- **Signal d'arrêt** : un téléchargement qui gêne le travail.

### R144. Les noms

- **Quoi** : « Trial » disparaît : l'agent s'appelle Cortex, suivi de son modèle. Claude Code montre le logo de Claude, à la demande de la Présidence.
- **Pour** : les sept. **Contre** : aucun.
- **Preuve en dix jours** : personne ne demande « c'est quoi ? » devant la liste des agents.
- **Signal d'arrêt** : une demande d'Anthropic sur l'usage de son logo.

## Le dessin, tranché par Jobs `[HYPOTHÈSE]`

| Élément | Mesure ou règle |
| --- | --- |
| Barre | Boîte arrondie, texte de 14 px, de 1 à 17 lignes ; dans la boîte, en bas : « + » à gauche, micro et envoi à droite |
| Rangée sous la boîte | 24 px de haut, texte de 12 px, sans bordure : projet, modèle ; à droite, l'anneau de contexte |
| Menu « + » | 260 px, lignes de 32 px : Add files, Issue, Project, puis Connectors |
| Arrêt | Le bouton d'envoi devient un carré ; Échap arrête |
| File | Une ligne au-dessus de la boîte par message en attente, cinq au plus, une croix |
| Ligne de travail | « Working… » et l'étape, puis « Worked for 8 s » et un chevron |
| Sous une réponse | Au survol, 24 px : copier, bien, pas bien |
| Déroulé d'une mission | Cinq lignes de 40 px : un rond vide, un anneau qui tourne, une coche ; le nom de l'étape, sa phrase |
| Changements | Le fichier, `+12 −1` en chiffres à chasse fixe, le retour en arrière au survol |
| Dialogues | 420, 560 ou 720 px ; une colonne ; libellés au-dessus ; l'action principale en bas à droite |
| Listes | 36 px par ligne : icône, phrase, clé, moment ; les actions au survol |
| Ctrl+K | 640 px, champ de 48 px, sections, un pied avec les raccourcis |
| Mise à jour | Une fenêtre de TaskForce, son logo, une phrase, une barre d'avancement |

## Décision de la Présidence

La Présidence a remis la suite à l'équipe (« je pense que t'as tout ce qu'il faut », « faut demande a Jobs et l'equipe dedie ») et ne refera pas tout (« si tu corrige je fais
globalement confiance »). R133 à R144 se construisent telles que Jobs les a tranchées. Elle garde le dernier mot : elle peut en écarter ou en changer une en la voyant, au test
final avant la release majeure.

Deux points tranchés par elle à la même occasion :

- **La politique de confidentialité** a changé avec le micro, et elle promet un e-mail aux titulaires de compte : « On envoie rien aux user deja sur l'app pour le moment ». Rien
  n'est envoyé ; à reprendre avant la release majeure.
- **Le logo de Claude** : « met le a jour stp c'est gonflant ca fait 15 fois que je demande ». R53 restait en attente ; la Présidence choisit le logo.

## Notes du secrétariat

- **La délégation à Jobs** est, comme aux n°18 et n°19, un choix de la Présidence pour cette séance ; elle ne change pas la charte (§2, point 4).
- **Les références** viennent de la Présidence. On prend la structure, pas l'identité.
- **La licence des DLL Visual C++** de l'installeur : la Présidence répond « jsp oui je suppose ». Ce n'est pas une confirmation ; à vérifier avant la release majeure.
- **Le logo de Claude** : les conditions d'Anthropic demandent une autorisation écrite (lues le 29/10/2026) ; à demander avant d'aller chercher des clients.
- **Conflits d'intérêts** : Saarinen dirige Linear ; Zhuo a rejoint Meta avec le rachat de Sundial ; le secrétariat est tenu par un modèle d'Anthropic, dont un produit sert ici de
  référence : la Présidence l'a choisi, le secrétariat n'a rien proposé d'autre.
- **Siège historique** : Jobs, mort en 2011, ne connaît ces outils que par le dossier.

## Suites

- Le PV au registre (§12) et au Journal.
- À `v1/13-roadmap/Roadmap_Backlog.md` : TF-J1-14 (la barre), TF-J1-15 (la conversation), TF-J1-16 (le déroulé de la mission), TF-J1-17 (les changements et la remise), TF-J1-18 (les listes,
  les volets, la palette), TF-J1-19 (le banc), TF-J1-20 (la mise à jour, la voix, les noms).
- À `experiences/Experiences.md` : E20, un vrai projet dans un domaine que la Présidence ne connaît pas.
- Après la passe : les agents connectés au banc ; une banque de comportements avec l'accord des personnes (« genre pouvoir analyser aussi les resultats des utilisateur quoi […] et avoir
  l'accord des user aussi ») ; puis J2.

## Avis du secrétariat

Mon avis, après la clôture, et non celui du Conseil.

- R139 et R140 portent la promesse et sont les plus risquées : la présentation ne suffit pas, il faut que le retour en arrière et le commentaire marchent vraiment.
- Les deux causes du dossier (le plafond et les délais) ont coûté plus que leur correction : une erreur muette fait douter de tout le reste.
- Une passe aussi large, sans recette complète derrière, fait porter le risque sur le test final : il faudra qu'il arrive tôt.

---

**Points d'entrée :** [Charte](../README.md) · [📓 Journal](../../Journal.md) · [🧰 Gabarits](../../Gabarits.md)
