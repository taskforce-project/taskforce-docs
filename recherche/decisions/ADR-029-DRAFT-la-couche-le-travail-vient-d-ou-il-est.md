---
id: adr-029-la-couche-le-travail-vient-d-ou-il-est
title: "ADR-029 (brouillon) : la couche, le travail vient d'où il est et l'issue reste l'ancre du dossier"
doc_type: adr
statut: proposed
version: 0.2
date: "22/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, integrations, issue, dossier, mcp, plugin, board, conseil]
related:
  - "../conseil/seances/2026-11-17-le-recentrage.md"
  - "../conseil/seances/2026-11-17-preciser-avant-de-trancher.md"
  - "../conseil/seances/2026-11-17-finir-la-v1.md"
  - "./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md"
  - "./ADR-031-DRAFT-une-source-de-travail-sans-copie.md"
  - "./ADR-022-DRAFT-infrastructure-pas-les-regles.md"
  - "./ADR-024-DRAFT-mcp-taskforce-surface-unique.md"
  - "./ADR-028-DRAFT-execution-isolee-par-defaut.md"
  - "../experiences/Experiences.md"
  - "../Questions-ouvertes.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-029 (brouillon) : la couche, le travail vient d'où il est et l'issue reste l'ancre du dossier

> **Brouillon, `DRAFT`, sans autorité avant sa promotion** ([Gabarits](../Gabarits.md) §6). Il naît de R199 (séance n°28),
> précisée par la séance n°29 (« R199, amendée ») et complétée par R208 et R209 (séance n°30). Ces recommandations sont
> **retenues le 22/11/2026 par délégation de la Présidence au Conseil, selon l'avis de sa majorité** : « Alright ecoute prends
> les meilleurs decision avec le conseille pour cette v1 et c'est partie ». Ce sont les recommandations qui sont retenues. Le
> texte ci-dessous reste une proposition du secrétariat, à relire par la Présidence, qu'E32 et E35 doivent éprouver. Il entre
> dans [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 029 après sa
> ratification.

## Statut

Proposé le 17/11/2026 ; amendé le 17/11/2026 par les séances n°29 et n°30 ; état de la décision inscrit le 22/11/2026. `DRAFT`,
pas promu. Le texte d'origine et ses amendements sont séparés : là où un amendement dit autre chose que le texte d'origine,
c'est l'amendement qu'on lit. En v1, rien ne se construit de ce projet au-delà de la ligne Claude Code, par le serveur MCP et
le plugin qui existent ; la première vraie source externe vient après le premier client test.

## Contexte

Contexte du texte d'origine (17/11/2026, séance n°28).

- `[ÉTABLI]` La Présidence, à sa recette de la 1.17.0 (étape s19, 17/11/2026) : « Au debut je voulais que les gens puissent
  abandonner linear, abandonner Asana et tout », « vaudrait mieux pouvoir s'integrer comme je le fais avec les integrations
  en fait tout simplement. Mais du coup le board sert a rien techniquement. »
- `[ÉTABLI]` Une mission ne part que d'une issue de TaskForce : `delivery_runs.issue_id` est `NOT NULL` vers `issues`, avec
  suppression en cascade (V86). Le dossier, les accords, la checklist, les liens et la portée de l'agent délégué pendent à
  cette issue (dossier de la [séance n°28](../conseil/seances/2026-11-17-le-recentrage.md), pièce 3).
- `[ÉTABLI]` Aucune synchronisation d'issues n'existe avec Linear, Jira, GitHub ou Asana : des outils à la demande pour
  Cortex, et un import ponctuel de 100 issues au plus, marquées `imported_from` (V126), sans identifiant externe ni retour.
- `[ÉTABLI]` Le serveur MCP de TaskForce expose 17 outils sur les issues, les projets, les missions et le Brain OS ; aucun
  n'expose le dossier, les règles ni l'état d'un accord. Le plugin Claude Code compte une commande et aucun hook : les
  actions locales d'une session ouverte par lui ne sont ni jugées ni gardées.
- `[ÉTABLI]` Les missions de Claude Code n'ont aucun connecteur externe : le runner ne leur donne que le serveur MCP de
  TaskForce.
- `[ÉTABLI]` Les outils de conformité qui se vendent se branchent sur les outils en place (dossier de la séance n°28,
  point 7) ; la révision du 28/07/2026 de MCP déprécie l'inscription automatique des clients, sur laquelle reposent 78 des
  104 préréglages.
- `[ÉTABLI]` La contradictrice de la séance, Vestager : une couche dépend de ceux sur qui elle se pose. Hamilton : une ancre
  hors de notre contrôle n'a pas de contrat.

Contexte ajouté par les séances n°29 et n°30 (17/11/2026).

- `[ÉTABLI]` Jobs, à la [séance n°29](../conseil/seances/2026-11-17-preciser-avant-de-trancher.md), sur son non à R199 : on
  perd la maîtrise de ce qui n'est pas ses écrans ; c'est un prix, et il n'était pas borné.
- `[ÉTABLI]` La plateforme de code dominante interdit déjà à l'agent d'approuver ou de fusionner sa propre pull request
  (dossier de la séance n°29, S37) : les quatre yeux sur le résultat existent chez l'hôte. Ce que l'hôte n'a pas, dans les
  pages lues : la décision prise pendant la mission, sur une action exacte, selon une règle de l'entreprise, gardée avec le
  reste.
- `[ÉTABLI]` La Présidence, dans la saisine de la [séance n°30](../conseil/seances/2026-11-17-finir-la-v1.md) : « c'est quoi es
  ecrans en question, comment on prend en compte qu'un utilisateur peut tres bien avoir l'ecran demander ailleurs et le reste
  chez nous » ; « Les integrations oui mais comment ? On allimente notre vue avec ? Ca foncitonne pas ca, trop lourd, trop de
  requete » ; « faire ce que fais Linear, pas tout copier, juste ce que nous on a besoin ».
- `[ÉTABLI]` Les trois écrans existent déjà dans l'app (séance n°30, pièce 1) : « Créer », « Accorder », « Relire », et
  l'export du dossier avec son vérificateur hors ligne. Le brief que l'agent reçoit n'entre pas encore au dossier (TF-J2-7).

## Décision

### Texte d'origine (17/11/2026, séance n°28, R199)

Gardé tel qu'il était proposé. Les points 3, 4, 6 et 8 sont précisés par les amendements qui suivent.

1. **TaskForce est une couche.** L'entreprise garde son outil de suivi. TaskForce ne cherche plus à le remplacer.
2. **L'issue de TaskForce reste l'ancre du dossier.** Le modèle des missions ne change pas : une mission pend toujours à une
   issue interne.
3. **Une issue peut porter la référence d'un élément de travail externe** : sa source, son identifiant chez elle, son
   adresse. Le résultat d'une mission (l'état, le lien de la pull request, le lien du dossier) y est renvoyé, par une
   écriture qui demande un accord comme toute écriture externe.
4. **Le dossier garde une copie de la demande telle qu'elle était au départ**, quelle que soit sa source. La preuve ne dépend
   jamais de l'outil d'origine : si la source change ou disparaît, le dossier se lit encore.
5. **Chaque source a un contrat écrit** : ce qui est lu, ce qui est écrit en retour, ce qui se passe quand la source change,
   refuse ou disparaît.
6. **Jamais une seule source.** Deux sources prouvées de bout en bout avant de dire « on s'intègre » ; l'issue interne reste
   la troisième, que personne ne peut fermer.
7. **La couche se joint par le protocole.** Le serveur MCP de TaskForce expose, en lecture, le dossier d'une mission et l'état
   d'un accord ([ADR-024](./ADR-024-DRAFT-mcp-taskforce-surface-unique.md) : chaque geste s'ajoute une fois, dans le MCP
   TaskForce). Le plugin Claude Code reçoit un hook qui juge et garde les actions d'une session, comme le runner le fait pour
   une mission.
8. **Le Board et sa famille gèlent** (R202) : visibles, sans travail nouveau, jusqu'au retour du client test.

## Amendements

### Amendement du 17/11/2026 : qui possède quel moment (séance n°29, « R199, amendée »)

R199 tient. Son prix, perdre la maîtrise de ce qui n'est pas ses écrans, se borne ainsi.

1. **Demander appartient à TaskForce.** La mission part d'un brief que TaskForce montre et que la personne accepte, quelle que
   soit la source. Ce brief accepté est la copie de la demande au dossier (précise le point 4).
2. **Décider pendant la mission appartient à TaskForce.** La carte d'accord ne s'affiche jamais dans l'outil d'un hôte. Elle
   arrive à la personne par une notification et un lien, sans qu'elle cherche.
3. **L'état se lit chez l'hôte** : où en est l'agent, ce qui attend, un lien. Une personne ne quitte pas son outil pour le
   savoir. L'hôte reçoit un état et un lien, rien d'autre (précise le point 3).
4. **Juger le résultat n'a qu'un lieu par sorte de mission**, et l'écran de remise le dit. Quand une pull request existe,
   c'est elle : TaskForce n'y refait pas la revue, il y joint le lien du dossier et garde au dossier la décision de revue.
   Sans pull request, c'est la remise de TaskForce.
5. **Une source menée au bout d'abord**, puis la seconde. « On s'intègre » ne se dit pas avant deux, et l'issue interne reste
   la troisième, que personne ne peut fermer (remplace le point 6 : non plus deux sources de front, une puis l'autre).
6. **Chaque source a son contrat écrit**, qui dit aussi où vit chacun des trois moments (complète le point 5).
7. **Le dossier garde la copie de la demande et la décision de revue** : dépendre d'un hôte coûte la porte, jamais la preuve.

Signal d'arrêt de la séance : une carte d'accord affichée chez un hôte ; ou E32 qui trouve deux lieux pour juger la même
mission.

### Amendement du 17/11/2026 : les trois écrans, et ce que TaskForce possède (séance n°30, R208)

1. **Trois écrans, ceux qui existent, pas un de plus.** « Créer » porte la demande. « Accorder » porte la décision pendant la
   mission. « Relire » porte la décision de fin. Prouver n'est pas un écran de travail : c'est la page du dossier, qu'on ouvre
   depuis « Relire » et qu'on exporte.
2. **Le brief** : quelle que soit la source, la mission part d'une seule carte, celle de « Créer ». Elle dit en langage clair
   ce que l'agent va faire, sur quel dépôt, avec quel modèle, sous quelles règles, et d'où vient la demande. Une personne
   l'accepte. Le brief accepté entre au dossier (TF-J2-7).
3. **On demande où l'on veut ; la demande vient à TaskForce, il ne va pas la chercher.** Elle lui arrive par son serveur MCP
   et son plugin : un agent, ou une personne par lui, crée l'issue et la délègue. En v1, une seule porte hors de TaskForce :
   Claude Code, ou tout agent qui parle MCP, par le serveur et le plugin qui existent. Les autres lignes (un éditeur de code,
   un outil de suivi, GitHub, Slack) sont écrites au PV et marquées « pas construit ».
4. **Accepter d'un lien et d'un geste** : la personne qui demande ailleurs reçoit un lien qui ouvre la carte.
5. **Chaque écran dit d'où vient la demande et où le résultat se juge.**
6. **Une carte d'accord sans réponse expire et vaut refus.** La carte et sa notification le disent, avec le délai.
7. **Ce que TaskForce possède en propre, toujours** : le brief accepté, les règles, la carte d'accord, le dossier. Ce qu'il
   peut laisser à d'autres : la liste du travail, la discussion, la revue du code.

Signal d'arrêt de la séance : un quatrième écran de travail ; une carte d'accord affichée chez un hôte ; une demande venue
d'ailleurs qui part sans qu'une personne ait accepté le brief.

### Amendement du 17/11/2026 : le contrat d'une source, et le minimum gardé (séance n°30, R209)

1. **Le contrat d'une source tient en quatre temps** : un instantané au départ ; rien pendant la mission ; deux événements
   reçus, pas plus (la pull request fusionnée ou fermée, la décision de revue) ; un état et un lien écrits en retour. Aucune
   vue alimentée, aucune copie tenue à jour. Son détail est le projet
   [ADR-031](./ADR-031-DRAFT-une-source-de-travail-sans-copie.md), qui complète celui-ci (précise les points 3, 4 et 5).
2. **L'état écrit chez un hôte est une écriture externe.** Il attend une carte tant qu'une personne ne l'a pas déclaré
   réversible, outil par outil : c'est le projet [ADR-030](./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md) (précise le
   point 3 : « une écriture qui demande un accord » reste le défaut, et ADR-030 dit comment il peut changer).
3. **Ce que TaskForce garde de la gestion du travail : onze choses**, chacune avec sa raison. Une ligne sans raison sort.

   | # | Gardé | Pourquoi le dossier en a besoin |
   | - | --- | --- |
   | 1 | L'issue : un titre, une description | C'est l'ancre de la mission et du dossier |
   | 2 | Sa liste à cocher | Elle devient la liste dure (R211) |
   | 3 | Ses commentaires et son activité, en un fil | Les demandes de changement et les décisions s'y lisent |
   | 4 | Ses pièces jointes | Ce que l'agent a reçu |
   | 5 | L'assigné et le délégué | La personne qui répond, et l'agent qui agit |
   | 6 | Un état simple | À faire, en cours, attend quelqu'un, en revue, fait, bloqué |
   | 7 | La référence d'origine | D'où vient la demande, quand elle vient d'ailleurs |
   | 8 | Le projet : un dépôt, une commande de tests, des règles | Ce que la mission a le droit de toucher |
   | 9 | La liste du travail d'un projet, par état, en langage clair | Hors du gel depuis la n°29 |
   | 10 | « Waiting for you » | Ce qui attend une personne |
   | 11 | La mission, sa remise et son dossier | Le produit |

4. **Tout le reste demeure gelé**, tel qu'il est, sans suppression : le Board et sa famille, les cycles, les points, le suivi
   du temps, les tableaux de bord. Le sort du Board se décide au point de décision, sur l'usage observé (précise le point 8 :
   non plus « au retour du client test » sans autre critère).

La « référence d'un élément de travail externe » du point 3 d'origine et la « référence d'origine » de la ligne 7 sont la même
chose : ce projet et ADR-031 disent désormais « la référence d'origine ».

## État de la décision au 22/11/2026

**La décision.** Après la séance n°30, la Présidence, à qui le secrétariat avait remonté les dix-huit points à trancher avec
l'avis de la majorité, répond : « Alright ecoute prends les meilleurs decision avec le conseille pour cette v1 et c'est
partie ». La Présidence délègue : les points sont tranchés selon l'avis de la majorité du Conseil, tel que le
[PV n°30](../conseil/seances/2026-11-17-finir-la-v1.md) l'écrit (« La liste à trancher pour finir la v1 »). Pour ce projet :

- R199, dans sa version précisée par la n°29, R208 et R209 sont retenues par délégation de la Présidence au Conseil, selon
  l'avis de sa majorité ;
- point 2, le Board : gelé, l'issue reste l'ancre, son sort se décide au point de décision, sur l'usage observé ;
- point 3, demander ailleurs en v1 : Claude Code seulement, par le serveur MCP et le plugin qui existent ; la première vraie
  source externe après le premier client test, GitHub puis Linear ;
- point 4, le contrat d'une source : oui (un instantané, deux événements, un état en retour, aucune copie ; onze choses
  gardées de la gestion du travail) ;
- point 6, les accords pendant la mission : trois classes ; hors de TaskForce, outil par outil, après la v1 (ADR-030, E33).

**Précisions du secrétariat.**

- Ce qui se construit en v1 : la ligne Claude Code, avec ce qui existe, éprouvée d'abord par E35 ; le brief accepté au dossier,
  avec TF-J2-7. Rien d'autre de ce projet.
- Ce qui vient après la v1 : la première source externe (GitHub), menée au bout, puis la seconde (Linear) ; le dossier et
  l'état d'un accord exposés en lecture par le serveur MCP ; le hook du plugin, qui se décide avec l'isolement
  ([ADR-028](./ADR-028-DRAFT-execution-isolee-par-defaut.md)).
- Le projet lui-même n'est pas ratifié : les Suites des trois PV le donnent « à relire par la Présidence ». Rien ne va dans
  `v1/12-decisions/` avant cette relecture.
- Désaccords conservés au PV : Vestager (commencer par GitHub, c'est commencer par la dépendance la plus risquée) ; Jobs (les
  lignes non construites devraient sortir du PV public) ; Musk (huit choses gardées, pas onze).

## Alternatives considérées

Du texte d'origine.

- **Garder le produit complet** : un gestionnaire de projet entier, avec la preuve dedans. Écartée par la séance : une
  personne ne le tient pas face à Linear et Jira, et la Présidence dit elle-même qu'elle veut s'intégrer.
- **Supprimer l'issue interne**, et attacher la mission à l'élément externe directement. Écartée : la preuve dépendrait
  d'un outil qu'on ne contrôle pas, et tout le modèle des missions serait à réécrire.
- **Une synchronisation complète dans les deux sens** (un miroir de Linear ou de Jira). Écartée : c'est refaire l'outil de
  suivi par un autre chemin ; la référence et le retour du résultat suffisent à la preuve, `[HYPOTHÈSE]` qu'E32 éprouve. La
  saisine de la n°30 l'écarte aussi (« trop lourd, trop de requete »), et ADR-031 en fait une règle : aucune copie.
- **Ne rien exposer par MCP** et garder la couche dans l'app. Écartée : une couche que seul son propre écran atteint n'en est
  pas une (Nilekani).

Ajoutées par les amendements.

- **Afficher la carte d'accord chez l'hôte**, là où la personne travaille. Écartée par la n°29 : décider pendant la mission
  est ce que l'hôte n'a pas, et ce que TaskForce garde ; l'hôte reçoit un état et un lien.
- **Deux lieux pour juger le même résultat** (la pull request et la remise). Écartée par la n°29 : un seul lieu par sorte de
  mission.
- **Une source externe complète dès la v1.** Écartée par la n°30 (point 3, option C) : la v1 se finit sur ce qui existe.

## Conséquences

- La preuve ne perd rien : l'ancre reste où elle est.
- Un champ de plus sur l'issue, la référence d'origine, et un geste de retour vers la source, à écrire une fois par source.
- Le dossier grossit du brief accepté et de la décision de revue ; c'est déjà demandé par R198 (TF-J2-7).
- Le hook du plugin étend le harnais à la session la plus courante, une personne dans Claude Code ; il doit tenir la même
  garde fermée que le runner, et se décide avec l'isolement (ADR-028).
- La dépendance aux éditeurs reste : une application à enregistrer chez chacun, que seule la Présidence peut faire.
- Une personne qui travaille ailleurs dépend d'une notification pour répondre à une carte d'accord, qui expire et vaut refus.
- Désaccords conservés : Jobs (une couche tierce dégrade la qualité, quoi qu'on possède ; à la n°29, il ne vote pas un écran
  qu'il n'a pas vu) ; Vestager (une seule source d'abord, c'est dépendre d'une seule).

## La preuve

- E32 ([Expériences](../experiences/Experiences.md)) : sur le code, la liste de ce que la preuve lit de l'issue, et de ce qui
  ne vient que du Board. Si un chemin de la preuve dépend d'un champ que seul le Board renseigne, ce projet se réécrit. La
  n°29 lui ajoute une lecture : une mission n'a-t-elle jamais deux lieux de jugement ?
- E35 : demander une mission depuis Claude Code, avec le serveur MCP et le plugin tels qu'ils sont, avant d'écrire une ligne.
- La liste des onze confrontée à l'inventaire de la n°28, pour vérifier qu'aucune surface gelée n'y revient (R209).

## Plan de déploiement

À jour au 22/11/2026. Il remplace celui du texte d'origine, qui renvoyait à R196, remplacée depuis par R205.

- **Maintenant, au labo, sans code du produit** : E32 et E35 ; le contrat écrit de la ligne Claude Code (ce qui est lu, écrit,
  gardé, et ce qui se passe quand cela casse).
- **En v1** : la ligne Claude Code par ce qui existe ; le brief accepté au dossier, avec TF-J2-7. Ce qui manque à cette ligne
  (une commande pour demander depuis le plugin, la référence d'origine, l'acceptation du brief venu d'ailleurs) ne s'écrit
  pas avant E35.
- **Après le premier client test** : la première source externe, GitHub, menée au bout selon son contrat (ADR-031) ; puis
  Linear.
- **Ensuite** : le dossier et l'état d'un accord par le serveur MCP ; le hook du plugin, avec l'isolement.
- **Avant toute annonce** : « on s'intègre » ne se dit pas avant deux sources prouvées de bout en bout.

## Questions à la Présidence

Le secrétariat ne répond pas à sa place.

1. **La relecture.** Ce projet dit-il ce que la Présidence veut de la couche ? Une ligne suffit pour le corriger ou le retirer.
2. **La promotion.** Le projet entre-t-il au journal des décisions après E32 et E35, ou seulement quand la première source
   externe est menée au bout ?
3. **Les applications à enregistrer chez les éditeurs** (GitHub, puis Linear) : seule la Présidence peut le faire. Le moment
   lui revient, après le premier client test.
4. **Le sort des surfaces gelées** (Q30) : il se décide au point de décision, sur l'usage observé. La décision lui revient.

## Liens

- [PV de la séance n°28](../conseil/seances/2026-11-17-le-recentrage.md), R199, R202 et la décision de la Présidence
- [PV de la séance n°29](../conseil/seances/2026-11-17-preciser-avant-de-trancher.md), « R199, amendée », « R201, amendée » et
  R206
- [PV de la séance n°30](../conseil/seances/2026-11-17-finir-la-v1.md), R208, R209, les pièces 1 à 3 et la liste à trancher
  (points 2, 3, 4 et 6)
- [ADR-030](./ADR-030-DRAFT-la-classe-d-une-ecriture-externe.md), la classe d'une écriture externe : l'état écrit chez un hôte
  en dépend
- [ADR-031](./ADR-031-DRAFT-une-source-de-travail-sans-copie.md), une source de travail sans copie : le contrat d'une source,
  en détail
- [ADR-022](./ADR-022-DRAFT-infrastructure-pas-les-regles.md), l'infrastructure, pas les règles
- [ADR-024](./ADR-024-DRAFT-mcp-taskforce-surface-unique.md), le MCP TaskForce, surface unique
- [ADR-028](./ADR-028-DRAFT-execution-isolee-par-defaut.md), l'exécution isolée par défaut
- [Expériences](../experiences/Experiences.md), E32 et E35
- [Questions ouvertes](../Questions-ouvertes.md), Q30 (le sort des surfaces gelées), Q31 (le témoin) et Q33 (la classe d'une
  écriture externe)

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 22/11/2026 · **v0.2** · Projet Taskforce
