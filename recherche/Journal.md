---
id: recherche-journal
title: Cahier de labo — R&D Brain OS
doc_type: register
statut: active
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, journal, cahier-de-labo, brain-os]
related:
  - "./README.md"
  - "./CLAUDE.md"
---

# 📓 Cahier de labo — R&D Brain OS

> **Le cahier de bord daté du laboratoire.** Une **entrée par session** de recherche, **la plus récente
> en haut**. À ouvrir en début de session (« où on en était »), à remplir en fin ([`CLAUDE.md`](./CLAUDE.md) §10).
>
> **Format d'entrée** (gabarit dans [`Gabarits.md`](./Gabarits.md)) : `Fait` · `Trouvé` · `Décidé` ·
> `Prochain coup`. On **date**, on **ne réécrit pas** le passé (une erreur reste, on la corrige dans une
> entrée suivante — c'est un cahier, pas un wiki).

---

## 2026-11-13 : séance n°24, dépasser Camunda

**Fait** : la Présidence demande si Camunda fait exactement ce que TaskForce veut faire, à quel point nous en sommes proches, comment lui prendre ce qu'il fait de mieux et passer au-dessus, et s'il est notre concurrent n°1 ; elle apporte une analyse écrite par un assistant d'IA. Le secrétariat a constitué le dossier sur les seules pages publiques de Camunda et de ses voisins, puis réuni le Conseil en plénière, Gwynne Shotwell contradictrice ([PV](./conseil/seances/2026-11-13-depasser-camunda.md)).

**Trouvé** :
- `[ÉTABLI]` Camunda 8.10 (13/10/2026) exécute des processus BPMN et y met des agents IA depuis la 8.8 : le modèle choisit ses outils dans un sous-processus ad hoc ; MCP dans les deux sens ; ProcessOS, en accès anticipé, part d'un résultat décrit en mots, et une personne approuve avant la production.
- `[ÉTABLI]` Près de 200 M$ de revenu récurrent, plus de 700 organisations, d'abord la banque, l'assurance et le secteur public ; aucun prix public ; la production auto-hébergée sous licence payante depuis la 8.6 ; Camunda 7 Community sans version depuis le 14/10/2025 ; Operaton, son fork sous Apache 2.0, publie encore.
- `[ÉTABLI]` Rien sur ses pages sur la pharmacie validée (BPF, IQ, OQ, PQ) ; Forrester le juge le mieux adapté aux grandes entreprises, IDC peu fait pour une offre toute prête par secteur.
- `[ÉTABLI]` Aucun voisin ne revendique une preuve vérifiée hors de l'outil par un tiers, ni des règles en mots au-dessus d'un socle ; seul Dapr signe ses historiques, en préversion.
- `[DÉDUIT]` En produit livré, TaskForce n'a aucune des briques de processus de Camunda ; il n'est devant que sur des pièces étroites (les règles sur chaque action, le dossier chaîné, le local, l'AGPL). Sur la cible écrite, Microsoft et n8n sont plus proches que Camunda, et la cible elle-même reste floue dans les documents.

**Décidé** : R163 à R170 recommandées, toutes à 90 % au moins (R163, R165, R167 et R169 au second tour) ; elles attendent la Présidence. Aucune fiche rafraîchie : toutes ont moins de 30 jours. Deux questions ouvertes, Q17 et Q18.

**Prochain coup** : la décision de la Présidence ; la ligne de la cible et E14 ; la maquette de la vue du workflow ; l'essai de coupure comparé de R167, en mode développement.

## 2026-11-12 : séance n°23, la revue complète de J2 (entrée ajoutée le 13/11)

**Fait** : à la demande de la Présidence, une revue complète de J2 à mi-chemin, par trois agents neufs (sécurité et logique, qualité, écrans), puis le Conseil en restreinte, Musk contradicteur ([PV](./conseil/seances/2026-11-12-revue-de-j2.md)).

**Trouvé** :
- `[ÉTABLI]` Dans des lots tous verts en CI : 13 défauts de sécurité et de logique et 4 manques, 1 défaut de qualité haut et 7 moyens, 8 défauts d'écrans hauts et 18 moyens.
- `[DÉDUIT]` Les essais d'un auteur confirment son intention, pas les cas qu'il n'a pas imaginés.

**Décidé** : R159 à R162, retenues par la Présidence le 12/11 ; R162 amendée : les essais de bout en bout se font à la main par la Présidence, puis en production sur l'app desktop, sans la CI. Les correctifs de R160 sont passés par #530, #531 et #532, chacun après sa relecture indépendante, et sont en prod avec la 1.16.0 le 13/11.

**Prochain coup** : la recette 1.16 de la Présidence sur l'app desktop, puis un lot de nettoyage des défauts moyens et faibles laissés par les revues.

## 2026-11-11 : la Présidence tranche la séance n°22

**Fait** : la Présidence retient R152 à R158 ([PV](./conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)).

**Décidé** : les critères de sortie de J2 sont chiffrés ; le registre est rangé par catégories ; la première vague devient les outils où la Présidence peut se connecter (GitHub, GitLab, OneDrive, Notion, Confluence, Jira, Slack, Teams, Linear, Docker Hub, Excalidraw, Figma, Stripe, Zoho, Asana) ; une étape côté entreprise est acceptable si le flux est clair, cohérent et accessible.

**Prochain coup** : la construction de J2, en lots : se brancher (la couche de connexion et la première vague), les règles par couches, et le guide de branchement de chaque outil.

## 2026-11-11 : séance n°22, se brancher à l'entreprise

**Fait** : la Présidence lance J2 et demande de se brancher à n'importe quel outil de l'entreprise, en un clic, en commençant par la liste exhaustive des outils les plus utilisés. Le secrétariat a dressé le [Registre des outils](../v1/02-produit/Registre_des_outils.md) (46 outils) et réuni le Conseil ([PV](./conseil/seances/2026-11-11-se-brancher-a-l-entreprise.md)).

**Trouvé** :
- `[ÉTABLI]` La connexion en un clic existe déjà pour MCP côté serveur, mais une connexion vaut pour tout l'espace, les agents de code n'atteignent aucun outil, et le stockage se choisit une fois par installation.
- `[ÉTABLI]` Sept éditeurs laissent toute application s'inscrire seule ; Google exige six semaines et un audit annuel pour lire tout un Drive, Microsoft 365 l'accord de l'administrateur.
- `[ÉTABLI]` Aucune plateforme de connecteurs ouverte et neutre ; l'injection par un contenu lu n'est résolue nulle part.
- `[DÉDUIT]` Sans connexion par personne, TaskForce lit avec les droits de qui a branché : ni la confiance ni l'audit ne tiennent.

**Décidé** : R152 à R158 recommandées ; elles attendent la Présidence.

**Prochain coup** : sa décision, puis la construction de J2 en lots, la connexion en un clic et la première vague d'abord.

## 2026-11-10 : la Présidence tranche la séance n°21

**Fait** : la Présidence a relu le PV de la séance n°21 et tranché R145 à R151 ([PV](./conseil/seances/2026-11-10-premier-client-e20.md)).

**Trouvé** :
- `[ÉTABLI]` Les règles sont déjà des données : un paquet versionné par espace (`harness_rule_sets`, V102), 38 règles par défaut, et chaque mission note la version et l'empreinte des règles reçues. Manquent l'éditeur, les couches et un socle que l'entreprise ne peut pas relâcher.
- `[ÉTABLI]` L'app desktop se connecte par le serveur de la webapp (`desktop/src/account.ts`) : l'échéance du 31/12/2026 la concerne aussi.
- `[ÉTABLI]` Le Mac App Store impose le bac à sable et interdit de télécharger des ressources qui ajoutent une fonction (Apple, règle 2.4.5, lue le 10/11).

**Décidé** : R145, R147, R148 et R151 retenues ; R146 amendée (une démo en vidéo avant l'entretien) ; R147 élargie (se brancher à l'outillage de l'entreprise, Google Drive d'abord, le stockage à son choix, ses propres règles par couches) ; R149 reportée après J2 et les vidéos, GCP envisagé ; R150 modifiée (pas de version non signée pour le premier client, l'adhésion d'Apple quand il montre une vraie intention).

**Prochain coup** : les critères de sortie de J2 et le déroulé de la démo, puis un atelier du Conseil sur la façon de se brancher à l'entreprise et sur les règles par couches.

## 2026-11-10 : séance n°21, la première version pour une entreprise, et E20

**Fait** : la release 1.14.0 et l'app desktop 1.11.0 sont en production ; la liste de lancement de 1.10.0 à 1.11.0 est verte sur un Windows neuf. La Présidence redéfinit E20 et demande au Conseil où en est la feuille de route ([PV](./conseil/seances/2026-11-10-premier-client-e20.md)).

**Trouvé** :
- `[ÉTABLI]` J1, prévu pour deux à trois semaines à partir du 02/11, est en production le 10/11 ; J2 n'a pas commencé.
- `[ÉTABLI]` Sans VPS au 31/12/2026, une nouvelle installation de l'app desktop ne pourra plus se connecter (Q13).
- `[ÉTABLI]` Un `.exe` ne s'exécute pas sur macOS ; une app Mac non notariée s'ouvre une première fois par « Ouvrir quand même », et ne se met pas à jour seule (Apple et Electron, lus le 10/11).
- `[DÉDUIT]` La valeur à prouver est ce que TaskForce sait de l'entreprise et ce qu'il empêche : seul un contre-essai la mesure.

**Décidé** : par la Présidence, la runtime Visual C++ dans l'installeur, le logo de Claude sans demande à Anthropic (Q12), le site mis à jour en dernier, les correctifs graves de Dependabot à la prochaine release ; R145 à R151 attendent sa décision.

**Prochain coup** : sa décision sur R145 à R151, l'entretien avec le premier client possible, puis J2 dans l'ordre d'E20.

## 2026-11-09 : séance n°20, l'atelier de la recette 1.13

**Fait** : la Présidence a joué la recette 1.13 sur l'app desktop 1.10.0 (42 étapes : 28 OK, 11 KO, 2 sautées) et donné la direction : Claude Desktop et Dust, avec l'expérience du Mac et de Raycast. Jobs et l'équipe UI/UX tranchent ([PV](./conseil/seances/2026-11-09-atelier-recette-113.md)).

**Trouvé** :
- `[ÉTABLI]` « Sorry, I couldn't answer » cachait un refus de validation : `AssistantController` plafonne un message à 4 000 caractères, avant le budget de contexte de la 1.13.
- `[ÉTABLI]` Les « unexpected error » du banc sont des délais dépassés vers Ollama, remontés en erreur 500.
- `[ÉTABLI]` E15, à la dictée réelle : 168 à 222 ms pour 2,6 à 4,3 s de parole ; la Présidence : « le module est vraiment fort ».
- `[DÉDUIT]` Une erreur muette fait douter de tout le reste : ces deux causes ont coûté plus que leur correction.

**Décidé** : R133 à R144 ; E20 s'ouvre ; rien n'est envoyé aux utilisateurs pour l'instant.

**Prochain coup** : la construction (TF-J1-14 à TF-J1-20), puis le test final de la Présidence sur un vrai projet (E20), avant la release majeure.

## 2026-11-08 : séance n°19, l'atelier de la sobriété

**Fait** : la Présidence a ouvert la 1.12.0 sur l'app desktop 1.9.0 et a demandé « comme raycast ou apple », le micro et un banc des modèles ; Jobs et l'équipe UI/UX tranchent ([PV](./conseil/seances/2026-11-08-atelier-sobriete-banc-voix.md)).

**Trouvé** :
- `[ÉTABLI]` « Waiting for you » lit les notifications non lues : 16 pour 0 demande ouverte dans la copie de la base de la Présidence prise avant la 1.9.0 (comptes seulement).
- `[ÉTABLI]` Cette copie se restaure sans un message d'erreur, en une seconde, dans une base jetable effacée ensuite : 79 tables, migration V118, 1 540 lignes, pgvector lu. La restauration n'existe pas dans l'app : elle s'est faite à la main, avec le `pg_restore` livré.
- `[ÉTABLI]` La suite de capacités (huit cas) dit ce qu'un modèle sait faire, pas ce qu'on peut lui confier ; son code tient en deux questions d'exécution mentale.
- `[DÉDUIT]` Un nombre faux abîme tout ce qui l'entoure : on apprend à ignorer le compteur, puis la vraie demande.

**Décidé** : R127 à R132 ; E15 commence, E19 s'ouvre. Une correction : le secrétariat avait écrit que le micro attendait une décision ; R76 et R80 sont retenues depuis le 30/10.

**Prochain coup** : la construction (TF-J1-10 à TF-J1-12), la release, la recette complète de la Présidence, puis la revue de J1.

## 2026-11-05 : séance n°18, l'atelier de la fenêtre

**Fait** : la Présidence a essayé la 1.10.0 sur l'app desktop 1.7.0, puis a demandé une app « same as Claude Code », sans maquette, Jobs tranchant tout et elle validant d'avance ([PV](./conseil/seances/2026-11-05-atelier-fenetre.md)).

**Trouvé** :
- `[ÉTABLI]` À « prend OPS-35 et propose moi un resume dans les commentaire stp », Cortex n'a appelé que `add_comment`, sans lire l'issue, et a écrit le résumé d'une itération qu'il n'avait pas lue ; la réponse ne disait pas quel modèle l'avait écrite (incident de confiance, E17).
- `[ÉTABLI]` La fiche d'issue recouvre la barre ; la conversation n'a pas de place à elle ; ses conversations ne sont pas dans la barre de gauche.
- `[DÉDUIT]` Quand la conversation devient l'écran principal, ce qu'elle a lu doit se voir sous chaque réponse, sinon une invention passe pour un résumé.

**Décidé** : R119 à R126, à l'unanimité des cinq : la fenêtre en trois zones (le travail et ses conversations, la conversation, ce qui l'entoure) ; les écrans en volets, entiers ; la conversation jamais vide, jamais seule, avec le modèle et ce qu'il a lu sous chaque réponse ; retirer sans cacher, l'annulation toujours là ; un volet « Progress » ; l'installateur à l'allure de la page de connexion. La structure de Claude Code, l'identité de TaskForce.

**Prochain coup** : TF-J1-9, en trois lots, après la fusion des deux corrections en cours ; E18 mesure la fenêtre avant et après.

---

## 2026-11-02 : séance n°17, Cortex voit, demande et dit vrai

**Fait** : la Présidence a essayé Cortex sur l'app desktop 1.6.0 (qwen3:8b), puis a soumis au Conseil la piste du secrétariat avant de la lancer ([PV](./conseil/seances/2026-11-02-cortex-voit-demande-dit-vrai.md)).

**Trouvé** :
- `[ÉTABLI]` En six échanges, Cortex a confondu une issue et une note, préparé une création pour une suppression, posé zéro question, et annoncé une suppression qui n'a pas eu lieu (incident de confiance, E17).
- `[DÉDUIT]` Demander, situer et dire vrai dépendent aujourd'hui de la bonne volonté du modèle.

**Décidé** : R114 à R118, à l'unanimité des sept (R115 et R116 au second tour) : TaskForce montre l'écran au modèle, pose lui-même les questions qu'un geste exige, dit ce qui a été fait à la place du modèle, écrit des plans pour les demandes courantes, et mesure chaque modèle sur les échecs de la Présidence. Dire vrai d'abord.

**Prochain coup** : TF-J1-8, R116 et R118 tout de suite, R114, R115 et R117 après les gestes du chat (TF-J1-5).

## 2026-11-02 : J0 clos sur le rejeu de la Présidence

**Fait** : la release 1.8.0 et l'app desktop 1.5.0 (la porte, l'issue qui dit vrai, la conversation depuis la barre) ; le rejeu de la mission par la Présidence.

**Trouvé** :
- `[ÉTABLI]` La porte demande ce que la table demande : la lecture de nodejs.org et la recherche web ont ouvert leur demande (journal du runner, mission 7).
- `[ÉTABLI]` Deux demandes restent du bruit (`echo`, `git branch --show-current`) ; « assignée à moi » n'est pas compris ; « Apply » s'éteint sans dire pourquoi quand la mission n'a rien changé.

**Décidé** : J0 clos (R109). La Présidence fait passer l'expérience par le chat : le MCP TaskForce devient la seule surface d'outils, pour Cortex comme pour tout agent (ADR-024 en brouillon) ; les premiers gestes du chat et sa couverture entrent en J1.

**Prochain coup** : J1 : les écarts du rejeu, le chat en bulle, les premiers gestes du chat (TF-J1-5), E16, la passerelle Java après le contrôle de VM1.

## 2026-11-01 : séance n°16 du Conseil, la revue de J0 sur l'app desktop

**Fait** : la Présidence a rejoué la boucle de J0 sur l'app desktop 1.4.0 (produit 1.7.0), sur un projet privé neuf.
Séance restreinte de sept membres sur ce rejeu (Bengio contradicteur, tiré au sort ;
[PV](./conseil/seances/2026-11-01-revue-j0.md)).

**Trouvé** :
- `[ÉTABLI]` La boucle passe de bout en bout : Cortex prépare l'issue, la Présidence la crée, Claude Code la prend, la carte
  de résultat arrive, « Apply » fusionne et termine l'issue. Une commande de test qui échoue éteint « Apply ».
- `[ÉTABLI]` La porte du runner ne posait pas toujours la question que la table demande : elle confiait « demander » aux
  permissions de Claude Code. Corrigée le jour même (R107, R108), publiée avec la release suivante.
- `[ÉTABLI]` Les retours de la Présidence portent sur ce que l'outil montre : la carte de Cortex incomplète et un mot
  faux (« Subtasks » pour une checklist), une activité qui ne dit pas qui a agi, une réponse qui s'ouvre loin de la
  question, un agent qui ne met pas l'issue à jour.

**Décidé** : R107 à R113, votées à 7 sur 7. R109 (J0 se clôt sur le rejeu de la mission 6, J1 part tout de suite) et R113
(ce que sait faire chaque modèle, mesuré chez la personne ; R51 essayée en J1) retenues par la Présidence ; les cinq
autres mises en œuvre sur sa demande de « corriger tout ça ».

**Prochain coup** : la release des correctifs de J0 sur « go release », le rejeu de la mission 6, puis J1 (E16, la
passerelle Java, les suppressions, la table des capacités).

## 2026-11-01 : séances n°14 et n°15 du Conseil, la feuille de route jusqu'à la démo complète

**Fait** : deux plénières de 24 membres.
- La n°14 (31/10/2026, Nadella contradicteur, [PV](./conseil/seances/2026-10-31-souverainete-operationnelle.md)) a jugé
  un texte de ChatGPT sur la « souveraineté opérationnelle de l'IA ». Elle a dressé une carte de 21 lignes (pile, devant,
  en route, derrière, ailleurs) et formulé R81 à R89.
- La n°15 (01/11/2026, Zhuo contradictrice, [PV](./conseil/seances/2026-11-01-feuille-de-route.md)) a répondu au cap
  de la Présidence. Elle a d'abord dit avoir compris ce que la Présidence veut faire de TaskForce. Elle a ensuite voté
  une solution par problème, R90 à R106, chacune à 90 % de oui au moins, et tracé une feuille de route en dix jalons,
  J0 à J9.

**Trouvé**
- `[ÉTABLI]` Trois logiques existent en double :
  - la décision des règles, en Java pour Cortex et en TypeScript dans le runner ;
  - la chaîne de preuve, en Java et en TypeScript ;
  - le protocole d'IA, dans l'ai-service en Python et dans la coque de l'app desktop en TypeScript.

  Le premier double est un choix de la spécification v2 : le runner juge chaque action sans aller-retour vers le serveur.
- `[ÉTABLI]` L'app desktop se connecte par la webapp (`/auth/desktop`), qui tourne sur les machines de l'école.
- `[ÉTABLI]` Au repos, seuls les secrets sont chiffrés ; le contenu et les sauvegardes sont en clair.
- `[ÉTABLI]` n8n se présente déjà comme une plateforme d'agents IA et de flux, avec des accords humains et l'auto-hébergement.
  « Un n8n IA » n'est donc pas une place libre : la différence est la règle du métier sur chaque action, la preuve
  vérifiable sans TaskForce, le métier qui construit sans code, le local sous AGPL.
- `[ÉTABLI]` La faille des droits dans la recherche du Brain OS est corrigée par une session dédiée, dans deux pull
  requests ouvertes (`taskforce-fullstack` #459 et #460).

**Décidé** (Présidence, 01/11/2026) :
- la lecture de ses décisions sur la n°14 est confirmée ;
- R90 (un seul moteur, en Java) est à l'essai : le double moteur reste, protégé par ses cas partagés, tant qu'une source
  unique sans aller-retour vers Java n'est pas trouvée (E16) ;
- R91 est modifiée : la webapp reste en ligne et reçoit chaque release, mais on n'y teste rien ; l'app desktop, avec
  Claude Code et Ollama, est le banc d'essai ;
- R92 est élargie : chacun branche ses modèles, quels qu'ils soient, et TaskForce ne gère pas les modèles, sauf
  l'entraînement si c'est possible ;
- R102 est précisée : l'arrivée se vit comme un jeu, ce n'en est pas un ;
- R103 est modifiée : une infrastructure générale, montrée sur trois natures de travail, pas un produit pour tous les
  métiers pour le moment ;
- tout le reste est retenu, et la règle des 90 % entre à la charte (§6).

**Prochain coup** : J0. Fusionner #459 et #460, puis « Apply » qui respecte les tests, le refus par délai qui se dit,
et les pages qui disent vrai. La release de R78 attend le « go release » de la Présidence. Ensuite J1 : E16 et la
passerelle de modèles ouverte.

---

## 2026-10-30 (bis) : l'atelier des écrans de base, séance n°13 du Conseil

**Fait** : la Présidence a lancé l'atelier en même temps que la release 1.6.7 (la banque de tests en production).
Restreinte (7), l'équipe de Jobs, Norman contradicteur ([PV](./conseil/seances/2026-10-30-atelier-ecrans-base.md)), avec
des maquettes de sept écrans. La règle `project.create` passe en `allow` (`taskforce-fullstack` #442).

**Trouvé**
- `[ÉTABLI]` Il n'existe aujourd'hui qu'une barre, dans le panneau de Cortex, et aucune voix dans le code.
- `[ÉTABLI]` Les mots de la cible, d'après la Présidence : audit, traçabilité, IQ, OQ, PQ, réglementation, référentiel.
- `[ÉTABLI]` Le texte de la séance n°10 vient d'un post Instagram d'une personne de Y Combinator.

**Décidé** (Présidence) : R76 modifiée (la voix démarre et s'arrête d'un clic, rien ne part sans que la personne envoie),
R77 à R79 retenues ; R80 à préciser, après la réponse du secrétariat sur l'entraînement.

**Décidé ensuite** (Présidence, même jour) : R80 retenue (la voix sur la machine dans l'app desktop, par le navigateur
dans la webapp) ; « Undo » tant que rien n'a bougé ; la note créée comme un projet, avec « Undo » ; les libellés de la
maquette gardés. La barre (R76) et « Undo » (R77) sont construits (`taskforce-fullstack` #444 et #446).

**Prochain coup** : la release de la barre et de « Undo » ; les trois écrans (R78) ; E15 ; un message à Y Combinator.

---

## 2026-10-30 : les réserves du premier lot, séance n°12 du Conseil

**Fait** : la Présidence a retenu R66 à R71 en faisant siennes quatre réserves, chacune à résoudre. Restreinte (7), Jobs
contradicteur ([PV](./conseil/seances/2026-10-29-reserves-premier-lot.md)). Le premier lot est fusionné dans `dev`
(`taskforce-fullstack` #437) ; la 1.6.6 et le desktop 1.3.6 sont en production.

**Trouvé**
- `[ÉTABLI]` Un cas ne garde ni l'identifiant des notes servies ni la version des règles : rien ne dit qu'il a vieilli.
- `[ÉTABLI]` Le serveur MCP de l'espace expose douze outils, aucun de la banque ; l'API en a huit routes.
- `[DÉDUIT]` Les réserves portent sur l'ordre autant que sur le fond : ajouter des surfaces avant les écrans de base
  disperse le produit.

**Décidé** (Présidence, 30/10/2026) : R72 à R75 retenues ; le désaccord de Jobs suivi : aucune surface nouvelle avant
les écrans de base. Et des explications plus explicites.

**Prochain coup** : l'atelier des écrans de l'équipe de Jobs, avec la banque dans les workflows 8 et 9 ; puis le lot 2
de la banque (l'adaptation des cas, « Add as proposed »).

---

## 2026-10-29 (quater) : le premier lot de la boucle, séance n°11 du Conseil

**Fait** : la Présidence a demandé d'enchaîner sur R61 en consultant le Conseil. Restreinte (7), Duflo contradictrice
([PV](./conseil/seances/2026-10-29-boucle-premier-lot.md)). Le premier lot a été construit sur une branche et vérifié en
développement (`taskforce-fullstack` #437) : le modèle au dossier de chaque réponse, le rejeu à blanc d'un cas figé, la
banque notée par du code, son écran.

**Trouvé**
- `[ÉTABLI]` La capture de V81 a été retirée le 18/10/2026 (`5700e4b1`) : rien ne pouvait l'activer, elle est restée
  vide. La note du flywheel la disait faite ; elle est corrigée.
- `[ÉTABLI]` En développement, un cas tiré d'une vraie réponse passe sur deux modèles locaux (`qwen3:8b`,
  `qwen2.5:7b-instruct`), sans écriture ni dossier pendant les rejeux.
- `[ÉTABLI]` Depuis le noyau, une écriture accordée peut échouer après le clic : un petit modèle a inventé un type de
  note. Corrigé à part (`taskforce-fullstack` #438).

**Décidé** (Présidence) : R66 à R71 retenues ; les réserves de Shotwell (R66, R68, R71) et de Duflo (R67) faites siennes,
chacune à résoudre.

**Prochain coup** : les solutions aux quatre réserves, au Conseil ; puis le registre des modèles par tâche (R61).

---

## 2026-10-29 (ter) : la carte des workflows et la direction, séances n°9 et n°10 du Conseil

**Fait** : l'équipe de Jobs a dessiné l'écran d'arrivée et les sept workflows principaux en diagrammes de séquence
(séance n°9, [PV](./conseil/seances/2026-10-29-atelier-design-carte.md),
[carte](https://claude.ai/artifact/CzYEJ2xV4kHQpPzWCd8y4x)). Le noyau pour Cortex est construit et vérifié en
développement. Puis la Présidence a saisi le Conseil entier : les entreprises posséderont des modèles spécialisés, sous
leurs règles, et TaskForce en serait le harnais, d'abord pour la conformité. Elle demandait aussi le business, les coûts
et un prototype à coût nul. Plénière (24), Bezos contradicteur, sur un dossier sourcé
([PV](./conseil/seances/2026-10-29-intelligence-possedee.md)).

**Trouvé**
- `[ÉTABLI]` TaskForce a le socle de la thèse : règles, dossiers chaînés, accords, choix du modèle, modèle local dans
  l'app desktop. Pas la boucle : ni évaluations par espace, ni registre des modèles, ni export des données, ni
  entraînement.
- `[ÉTABLI]` C1 et C4 excluent tout entraînement dans le labo, et toute preuve de la valeur d'un modèle spécialisé sur
  nos données.
- `[ÉTABLI]` Les meilleurs modèles ouverts ont environ quatre mois de retard en moyenne (Epoch AI). Sur une tâche étroite,
  un petit modèle affiné peut battre un modèle de pointe (prépublications de 2026).
- `[ÉTABLI]` L'entraînement et l'hébergement de modèles spécialisés sont occupés par des fournisseurs financés ; la
  conformité « agentique » lève des fonds ; l'Omnibus reporte le haut risque au 02/12/2027.
- `[DÉDUIT]` Servir chacun à coût nul et posséder son intelligence sont la même architecture : le local.

**Décidé** (Présidence) : R55 à R59 et R60 à R65 retenues, « on suit le conseil sur tout, go ».

**Prochain coup** : la direction dans la spécification et la roadmap ; la boucle (R61 : évaluations, registre des
modèles, export des données) ; E12 (l'affinage sur le corpus public) ; un partenaire de conception (R63, E13) ; les mots
(R65, E14) ; l'atelier des écrans reprend sur la carte, avec deux workflows de plus.

---

## 2026-10-29 (bis) : la recette de la 1.3.2, séance n°8 du Conseil

**Fait** : la Présidence a rejoué la recette sur l'app desktop 1.3.2 et la webapp 1.6.2, avec la même fiche. Le
secrétariat a relu chaque note et vérifié les causes dans le code, les journaux et les réglages de la prod. Il a relu le
code des réparations en Java, Python et TypeScript. Puis il a réuni le Conseil en formation élargie (10), Hamilton
contradictrice ([PV](./conseil/seances/2026-10-29-recette-132.md)).

**Trouvé**
- `[ÉTABLI]` 19 étapes OK, 3 KO, aucune bloquée (7 à la recette précédente) : une mission va jusqu'à la pull request.
- `[ÉTABLI]` Cortex a créé l'issue dans un autre projet que celui nommé. `create_issue` ne connaît le projet que par son
  numéro, que le modèle n'a pas cherché. L'outil répond « Issue created in TaskForce », que le modèle a pris pour le nom
  du projet.
- `[ÉTABLI]` Une recherche web demande un accord à chaque requête : la règle la classe irréversible, puisque la requête
  sort de la machine. Sur une mission de modification, trois accords sur quatre portaient sur du réversible (E7).
- `[ÉTABLI]` La pull request affiche « nothing pushed » au-dessus d'une branche poussée : le runner recopie le résumé de
  l'agent. Et le prompt demande à l'agent des tests qu'une règle lui interdit.
- `[ÉTABLI]` Le « rate limiting » de la recette est le frein de la bêta : une requête IA par minute et par compte.
- `[ÉTABLI]` La relecture a trouvé dix défauts dans les réparations, dont un introduit par le secrétariat (la mise en
  place de la double vérification la coupait sans code). Ils sont corrigés et livrés en 1.6.3.

**Décidé** (Présidence) : R46 à R54 retenues, R31 avec elles, « on suit le conseil sur tout, go release ».

**Prochain coup** : les réparations courtes (R48, R49, R52), puis R46, puis la refonte des trois écrans avec Jobs (R54) ;
E11 pour la délégation à un modèle local.

---

## 2026-10-29 : la recette de la 1.3.1, séance n°7 du Conseil

**Fait** : la Présidence a passé la recette de l'app desktop 1.3.1 et de la webapp 1.5.1 (24 étapes, le parcours J9).
Le secrétariat a relu chaque note, cherché les causes dans le code, les journaux et la prod, puis réuni le Conseil en
formation élargie (10) ([PV](./conseil/seances/2026-10-29-recette-131.md)).

**Trouvé**
- `[ÉTABLI]` 11 étapes OK, dont 8 avec des remarques ; 4 KO ; 7 bloquées ; une passée.
- `[ÉTABLI]` Depuis le 05/09/2026, le serveur envoie au modèle des définitions d'outils invalides. Le paramètre `title`
  de `create_issue` devient du texte. Ollama et Groq les refusent (400), et la passerelle retire tous les outils sans le
  dire. Dans l'app desktop, le modèle invente « Issue created » ; sur le web, Groq refuse aussi la requête sans outils,
  car le modèle appelle un outil que le prompt nomme. Les deux erreurs sont rejouées et citées au PV.
- `[ÉTABLI]` Claude Code n'était plus connecté sur le poste de la Présidence. L'app le savait mais proposait l'agent, et
  le runner ne contrôle que la version : quatre missions ont échoué au démarrage. Le contrôle du poste par le
  secrétariat ne regardait, lui aussi, que la version.
- `[ÉTABLI]` La directive `/no_think` est ignorée par Ollama 0.40.11 : couper le raisonnement par le réglage natif fait
  passer un appel d'outil de 2,9 s à 0,5 s.
- `[ÉTABLI]` La double vérification se désactive sans code. Un refus de règle s'affiche « Agent failed », avec des mots
  internes.

**Décidé** (Présidence) : R34 à R45 retenues, « on suit le conseil sur tout », et les réparations lancées.

**Prochain coup** : le premier panier (les outils de Cortex, la délégation sans
connexion) dans une seule branche, une version web et desktop, et la recette rejouée.

---

## 2026-10-28 (bis) : le jour 1 du sprint en prod, séances n°5 et n°6 du Conseil

**Fait** : le ménage et le jour 1 du harnais construits, vérifiés de bout en bout et mis en prod (TaskForce 1.5.0,
app desktop 1.3.0) ; deux séances tenues en parallèle, à la demande de la Présidence. La séance n°5 a revu la
trajectoire, le découpage et `npm test` ([PV](./conseil/seances/2026-10-28-trajectoire-harnais.md)). La séance n°6 est
l'atelier design mené par Jobs : Cortex, les flows, la carte de résultat, le parcours de test
([PV](./conseil/seances/2026-10-28-atelier-design.md)).

**Trouvé**
- `[ÉTABLI]` La porte laissait passer `npm test --prefix ../ailleurs` et `--outDir=../../x` : la règle ne lisait que
  le nom de la commande. Trouvé par la séance n°5, corrigé sur la branche v2.
- `[ÉTABLI]` Le serveur envoie les conditions vides des règles à `null`. Le moteur du runner les prenait pour des
  motifs ; trouvé par l'essai de bout en bout, corrigé. La garde fermée a tenu pendant le défaut.
- `[ÉTABLI]` L'atelier a relevé dans le code huit défauts visibles. Exemples : « Brain OS » encore dans Cortex ; Claude
  Code 2.1.293 affiché prêt ; les demandes du runner affichées « Claude Code asks ». Liste au PV.
- `[HYPOTHÈSE]` Quatre des cinq membres consultés refusent `npm test` autorisé par défaut tant que la machine n'est pas
  isolée ; ils préfèrent que le runner lance seul les tests après l'agent (S1). Musk le défend autorisé, sous
  conditions.

**Décidé** (Présidence) : R32 retenue, les tests lancés par le runner après l'agent (S1), aucune règle qui autorise l'agent à lancer un shell arbitraire ; R33 retenue, pas de mission déléguée en prod sur un dépôt public avant S1 ; les décisions de Jobs J1 à J9 gardées telles quelles. R27 à R31 en attente.

**Prochain coup** : l'essai de la Présidence sur l'app desktop 1.3.0 et la webapp 1.5.0, selon le parcours de Jobs ;
en parallèle, les défauts relevés par l'atelier, puis le reliquat du jour 1.

---

## 2026-10-28 : spécification de la v2 en 0.2, pôle Design, séance n°4 du Conseil

**Fait** : la spécification passe en 0.2 avec les décisions de la Présidence
([spécification](../v1/road_to_v2/Specification_V2_Harnais.md)) et un schéma en image
([schéma](../assets/diagrammes/architecture-v2-harnais.svg)) ; trois recherches sourcées (Java et Spring, outils
d'agents et OAuth, fiches) ; le pôle Design rejoint le Conseil (Don Norman, Julie Zhuo, Karri Saarinen) ; séance n°4
en formation élargie, revue de la spécification ([PV](./conseil/seances/2026-10-28-revue-spec-v2.md)).

**Trouvé**
- `[ÉTABLI]` Un hook HTTP injoignable laisse passer l'action de Claude Code, sauf avec `onFailure: "block"`, qui
  demande la 2.1.295 ; la version minimale du runner (2.1.293) ne suffit pas.
- `[ÉTABLI]` Seul Claude Code tient la décision « demander » sans interface ; Codex, Cursor et Gemini CLI s'arrêtent à
  autoriser ou refuser.
- `[ÉTABLI]` Ollama fait tourner Claude Code sur un modèle local, mais Anthropic ne prend pas en charge Claude Code sur
  d'autres modèles : la boucle interne de TaskForce reste le chemin des petits modèles.
- `[DÉDUIT]` Le monolithe modulaire est imposé par l'app desktop : le même backend doit tenir sur un ordinateur.

**Décidé** (Présidence, avant la séance) : la webapp d'abord, en local, puis le .exe ; trois produits ; le front du
Brain OS supprimé ; R10 à R15 retenues ; l'approche A ; le fil de l'équipe plutôt qu'une messagerie. Après la séance :
R16 à R26 retenues, R23 après un second tour (Jobs, Bengio, Bezos) ; une hiérarchie d'agents et de modèles choisie par
tâche (R20 élargie) ; des produits aux fonctions différentes ; le harnais pourra servir dans d'autres outils, Linear
compris. Spécification en 0.3, validée.

**Prochain coup** : le ménage d'une demi-journée, puis le sprint, en mode développement : la webapp dans Docker, puis
une version de l'app desktop pour l'essai de la Présidence avec ses modèles Ollama.

---

## 2026-10-27 (ter) : état des lieux de la v1, séance n°3 du Conseil, spécification de la v2

**Fait** : état des lieux d'un jour de la v1, tiré du code et du journal daté
([état des lieux](../v1/09-audits/Etat_des_lieux_v1_avant_v2.md), PC-059 à PC-062) ; ménage tranché par la Présidence ;
spécification de la v2, version 0.1 ([spécification](../v1/road_to_v2/Specification_V2_Harnais.md)) ; séance n°3 en
formation restreinte, Jobs et Musk, sur le ménage et la spécification ([PV](./conseil/seances/2026-10-27-menage-spec-v2.md)).

**Trouvé**
- `[ÉTABLI]` La délégation de code marche de bout en bout dans l'app desktop (19/10) ; ce qui fera le harnais manque :
  documents et versions, règles en données, preuve exportable.
- `[ÉTABLI]` Pour le premier cas d'usage, deux étapes sur six sont absentes à la base : importer un document, le chercher
  par version.
- `[DÉDUIT]` L'architecture de la v1 a déjà la bonne forme : un serveur qui garde, un runner qui exécute ; la v2 la
  généralise au lieu de la remplacer.

**Décidé** (Présidence) : le .exe d'abord, le Store et la webapp ensuite ; l'équipe gardée, comme contexte ; Mentions
gardé ; Assignments à retravailler ; GitHub et Slack à faire marcher ; Public et Private gardés ; Status retiré de la
vue ; Pages supprimées au profit du Brain OS ; Copilot gardé, à essayer ; code mort supprimé ; dans le doute, masquer
plutôt que supprimer. Priorité de la v2 : le harnais et l'architecture, scalables et robustes.

**Prochain coup** : la Présidence relit la spécification et tranche son §20 (dont R10 à R15) ; puis le sprint de trois
jours avec la banque de tests, en mode développement.

---

## 2026-10-27 (bis) : séance n°2 du Conseil, la vision de la Présidence

**Fait** : plénière des 21 membres sur la vision de Pierre (le harnais comme principe fondamental de tout outil avec
IA), tour de table, confrontation, second tour à sa demande, dernier mot du Conseil
([PV](./conseil/seances/2026-10-27-vision.md)). Question ouverte Q11 (harnais embarqué). La règle zéro garde « prouve ».

**Trouvé**
- `[DÉDUIT]` Le Conseil converge : miser sur l'entreprise, jamais sur les défauts des modèles ; vendre un résultat, le
  harnais invisible pour l'utilisateur et lisible pour l'auditeur ; un plan de contrôle neutre et local plutôt qu'une
  interface générique.
- `[ÉTABLI]` L'écart principal avec la vision : pendant une délégation, l'agent ne voit que le serveur MCP de
  TaskForce, pas encore les outils externes de l'entreprise (`taskforce-runner/src/agent.ts`).

**Décidé** (Présidence) : vision validée à dix ans ; R5' (la promesse), R6, R7' (tout tracé, seul l'irréversible
attend), R8, R9' retenues ; I1 (assurable) et I2 (embarqué) gardées ; niches A puis B ; premier cas d'usage : un
standard de communication de vingt-cinq ans qui évolue ; le bac à sable plutôt que la branche ; « libre mais
encadré » ; les outils de Microsoft se branchent sur TaskForce, pas l'inverse. Séance close.

**Prochain coup** : résumé pour la Présidence, état des lieux d'un jour de la v1, spécification de la v2 relue par la
Présidence, puis sprint de trois jours avec la banque de tests (passage en mode développement).

---

## 2026-10-27 : séance n°1 du Conseil, la première règle non négociable

**Fait** : première séance du Conseil d'Avenir, en formation restreinte (7 membres, contradicteur : Elon Musk), sur
la saisine « quelle est la première règle non négociable de TaskForce ? »
([PV](./conseil/seances/2026-10-26-premiere-regle.md)). Expériences E7 à E10 déclarées
([`Experiences.md`](./experiences/Experiences.md)), question Q10 ouverte. Kenza Ait Si Abbou entre au pôle Pont, à la
demande de Pierre (fiche sourcée) : le Conseil compte 21 membres, dont 11 femmes. Margaret Hamilton, morte le
30/09/2026, passe en siège historique. La fiche de Satya Nadella le rangeait par erreur dans Impulsion : corrigée (Pont).

**Trouvé**
- `[ÉTABLI]` Le dossier tient sur des sources primaires : le rapport d'Anthropic du 16/10/2026 (environ 80 % des
  sessions interactives à attendre un humain, chez ses employés), le billet d'OpenAI sur le harness engineering, le
  rapport de la NASA sur les règles de mission d'Apollo, la checklist de l'OMS.
- `[DÉDUIT]` Les sept membres convergent sur un point : la règle doit vivre hors de l'agent, écrite avant la mission.
  Ils divergent sur la vitesse (Musk, Bezos) et sur ce qu'on mesure (Harris).

**Décidé** (Présidence, 27/10/2026) : R1 « Aucun agent ne décide seul d'une action irréversible, ni de ce qui est
irréversible » retenue (une branche de travail rend réversible ce qui reste local) ; R2 retenue, à mieux expliquer ;
R3 retenue, avec le temps de cycle en plus ; R4 retenue (un relecteur dédié, avec une liste et une partie libre). Règle
zéro ratifiée : « On vise dix ans, on prouve en dix jours. »

**Prochain coup** : séance n°2 sur la vision de la Présidence, pas encore présentée au Conseil. E7 à E10 demandent un
passage en mode développement, après arbitrage de priorité.

---

## 2026-10-21 : création du Conseil d'Avenir

**Fait** : le Conseil d'Avenir est créé à la demande de Pierre, pour faire émerger les versions futures de TaskForce.
Charte et règlement [`conseil/README.md`](./conseil/README.md) (présidence, secrétariat, composition, formations,
déroulé d'une séance, règles du débat et d'honnêteté, mise à jour des fiches, traçabilité, règle zéro, registre) ;
20 fiches sourcées dans [`conseil/membres/`](./conseil/membres/) ; gabarits §7 (fiche membre) et §8 (procès-verbal)
dans [`Gabarits.md`](./Gabarits.md) ; protocole [`CLAUDE.md`](./CLAUDE.md) v1.2 (§7 : le Conseil siège à chaque
session) ; carte du labo v2.1. Poussé le 25/10, après le correctif de la version Store de l'app desktop.

**Trouvé**
- `[ÉTABLI]` La proposition de départ, venue de ChatGPT, réunissait surtout des dirigeants de la tech, sans
  scientifique. Pierre a demandé des femmes, des conseillères scientifiques et Yoshua Bengio. Composition retenue :
  20 membres, 10 femmes et 10 hommes, en quatre pôles (Impulsion, Pont, Harmonie, Science).
- `[ÉTABLI]` Chaque position `[ÉTABLI]` d'une fiche porte sa source ; 151 liens sur 158 répondent, les 7 autres sont
  des refus de robot ou des murs payants, aucun lien mort. Sept fiches gardent des points « à vérifier », dont la
  fonction actuelle d'Arati Prabhakar.
- `[DÉDUIT]` Le risque du dispositif est la fausse citation et l'aval implicite : d'où la règle « rien ne sort du labo
  sous le nom d'un membre » (charte §8).

**Décidé** : Pierre préside sans prendre part aux débats ; le Conseil siège à chaque session du labo ; l'agent tient
le secrétariat. En attente de ratification : la règle zéro « On vise dix ans, on prouve en dix jours ».

**Prochain coup** : première séance, avec le retour de ChatGPT que Pierre apporte. Saisine candidate : « quelle est
la première règle non négociable de TaskForce ? ». Aucun passage en mode dev.

---

## 2026-07-31 (quinquies) — A6 (Φ) + A7 (causalité) : clôture de la frontière

**Fait** — A6 et A7 traités **ensemble** → fiche commune [`theorie/A6-A7-frontiere.md`](./theorie/A6-A7-frontiere.md).
Entrées A6 et A7 de [`Axiomes.md`](./theorie/Axiomes.md) réduites. **Frontière A4–A8 entièrement poussée.**

**Trouvé**
- `[DÉDUIT]` A6 et A7 = **le même geste** : décorer le graphe d'une grandeur **absente des données**
  (potentiel / cause). Les deux **s'échouent sur C2**.
- `[DÉDUIT]` **A6 (Φ) hors modèle** : la valeur d'option vient de la **volatilité $\sigma$**, or ni prix ni
  $\sigma$ ici ; tout proxy = métrique de graphe qui ne mesure pas l'optionalité, ou **runway relabellisé**.
  Doublement bloqué (présuppose A4 + A5). **Sauvetage** : `irr(v)=\deg^-_{DEPENDS\_ON}(v)` (irréversibilité), calculable, ≠ Φ.
- `[DÉDUIT]` **A7 = l'ombre statique de A4** : `CAUSED_BY` est $P(G'|G,do(a))$ au grain de l'arête → même
  non-identifiabilité, **tombent ensemble**. `[ÉTABLI]` `count=0` (personne ne l'écrit). **Sauvetage** :
  couche **précédence barreau 1** = générateur d'hypothèses, `SUSPECTED_CAUSE` + confiance + provenance.
- `[DÉDUIT]` **Point de méthode** : A6/A7 **n'ont pas d'expérience** — leur verdict est « hors modèle »,
  fabriquer un test pour les faire paraître actifs serait malhonnête. **Un axiome a le droit à un « non ».**

**Décidé** — Frontière close. **Le rocher commun = C2** : A4, A6, A7, A5b s'y échouent, et tous ont le
**même repli** : structure observée + mémoire (**F2**), jamais futur/cause **inférés (F3)**.

**Méta (frontière complète A4–A8)** — Le système d'axiomes, poussé à fond, **redit ce que les revues
disaient** : le moat n'est pas la prédiction, c'est la **mémoire instrumentée**. Ce qui reste
constructible : **table d'épisodes/écarts**, **taux de base (E3)**, **front rétrospectif (E6, A8)**,
+ deux fragments structurels (`irr(v)`, précédence). Tout le reste est bloqué par C2.

**Prochain coup** — **Synthèse** : « ce à quoi le système d'axiomes s'est réduit » — candidate à
**promotion** (ADR, ou note dans `v1/road_to_v2/`). Point dev en attente inchangé (worklogs peuplés ?).

---

## 2026-07-31 (quater) — A8 (trajectoires / Pareto) poussée à fond · frontière solo

**Fait** — A8 → fiche dédiée [`theorie/A8-trajectoires.md`](./theorie/A8-trajectoires.md). Entrée A8 de
[`Axiomes.md`](./theorie/Axiomes.md) réduite. Nouvelle expérience **E6** (informativité du front de Pareto passé).

**Trouvé**
- `[DÉDUIT]` **Sur le passé, on compare des résultats réalisés, pas des futurs alternatifs** (générer des
  futurs = A4 bloqué ; contrefactuel = C2). → A8 groundé est **descriptif (F2)**, pas prescriptif. Ground
  la **math** de Pareto, pas l'**usage** (choisir un futur).
- `[ÉTABLI]` **Malédiction dimensionnelle** : à $m \gtrsim \log_2 n$ (ici $n{\approx}20$, seuil ~4,3) le
  **front ≈ tout** → le rêve **6 axes** est **inutile**. Inversion : seuls **2–3 objectifs sont
  mesurables**, ce qui garde $m$ petit et **sauve** A8 (mais tue l'ambition « riche arbitrage »).
- `[ÉTABLI]` Une **somme pondérée linéaire** ne touche que le **bord convexe** → prouvablement incomplète.
- `[HYPOTHÈSE]` **La forme utile n'est pas le front pur mais l'ε-contrainte** (« maximiser X s.c. runway
  > 6 mois ») : **contraintes, pas poids**, atteint le non convexe, et **produit une décision** (le front pur botte en touche).
- `[HYPOTHÈSE]` **Le noyau durable de A8 = refuser de scalariser l'incommensurable** — la partie la plus
  solide de tout le système, survit même quand le calcul est bloqué. Étoile polaire : **jamais de score global unique.**
- `[DÉDUIT]` Fragilité à $n{=}20$ + seed synthétique → **bootstrapper le front**.

**Décidé** — A8 reformulé : principe (durable) + calcul **rétrospectif** (2–3 axes, E6) + ε-contrainte
comme forme pratique. Le prescriptif reste bloqué (A4 + C2).

**Méta (3 axiomes de frontière poussés : A5, A4, A8)** — ils **convergent** : tout ce qui est groundable
est **F2/mémoire** (table d'épisodes, front rétrospectif) ; tout le **prescriptif** (simuler des futurs)
est bloqué par **A4 + C2**. Les deux seules briques buildables qui reviennent partout : **(a) la table
d'épisodes/écarts, (b) « quelque chose bat-il le taux de base ? » (E3).** A8 ajoute le **seul livrable
montrable sans rien débloquer** : le front rétrospectif (E6).

**Prochain coup** — frontière solo restante : **A6 (Φ)** et **A7 (causalité)** — les deux probablement
« hors modèle / bloqués », mais à documenter proprement pour fermer la frontière. Point dev inchangé (worklogs peuplés ?).

---

## 2026-07-31 (ter) — A4 (dynamique f) poussée à fond · frontière solo

**Fait** — A4 → fiche dédiée [`theorie/A4-dynamique.md`](./theorie/A4-dynamique.md). Entrée A4 de
[`Axiomes.md`](./theorie/Axiomes.md) réduite. Nouvelle expérience **E5** (stabilité du LLM-comme-$f$).

**Trouvé**
- `[ÉTABLI]` La forme **$M \cdot S_t$ est morte** : le graphe grandit (dimension variable), une matrice
  n'ajoute pas de nœud. $f$ = **graph rewriting**, pas algèbre linéaire.
- `[HYPOTHÈSE]` **Scinder $f = f_{\text{drift}}$** (= A3, gratuit, groundable) **+ $f_{\text{action}}$** (le problème).
- `[DÉDUIT]` **$f_{\text{action}}$ non identifiable** : l'action n'est pas aléatoire (confondue par le
  *motif* de la décision) + contrefactuel jamais observé (C2). **Plus profond que « pas assez de
  données »** — c'est **A7** (causalité) qui revient.
- `[HYPOTHÈSE]` **Le $f$ honnête n'est pas une formule** mais une **récupération non paramétrique**
  d'épisodes $(G,a,G')$. → **A4 dépend de la table des écarts de A5** : A5 ne *juge* pas $f$, **elle le
  nourrit**. Dépendance plus forte qu'on croyait.
- `[ÉTABLI]` **Un opérateur local existe déjà et est idempotent** (ingestion Phase 4bis, verrou V69).
  A4 = **généraliser**, pas inventer un monolithe.
- `[HYPOTHÈSE]` **Markov douteux** → $f(G_t,a)$ partiel (A2). **Horizon $\leq 2$–$3$** (erreur composée, pas de fonction de valeur).
- `[HYPOTHÈSE]` **Un LLM n'est pas une fonction** ($\operatorname{Var}_\omega$) → **E5**.

**Décidé** — A4 **reformulé** : drift + action, récupération non paramétrique, **bloqué derrière A5**. La
séquence réelle est **A5 (émettre l'incertitude + table d'épisodes) → A4 (récupération dessus)**.

**Prochain coup** — frontière solo suivante : **A8** (Pareto, grounding **gratuit** sur trajectoires
passées) ou **A7** (causalité, déjà à moitié traité en A4 §3) ou **A6** (Φ). Point dev inchangé (worklogs peuplés ?).

---

## 2026-07-31 (bis) — A5 (calibration) poussée à fond · frontière solo

**Fait** — Première frontière poussée en solo : **A5 → fiche dédiée** [`theorie/A5-calibration.md`](./theorie/A5-calibration.md)
(pattern « un axiome poussé = une fiche »). Entrée A5 de [`Axiomes.md`](./theorie/Axiomes.md) réduite à un
résumé. E1 raffiné en 3 régimes ([`experiences/Experiences.md`](./experiences/Experiences.md)). `issue_worklogs`
(V47) lu.

**Trouvé**
- `[ÉTABLI]` **Le système n'émet aujourd'hui aucune croyance calibrable** : story points = **point** (pas
  de distribution), « déjà-vu 41 % » = **cosinus déguisé en proba** (l'erreur même que A5 dénonce). Donc
  A5 est **bloqué en amont** : avant de calibrer, il faut que le **produit émette une incertitude**.
- `[DÉDUIT]` **« Calibré » est trivial** (prédire le taux de base y arrive) → viser **calibré ET tranchant**
  (décomposition de Murphy : fiabilité *et* résolution). Un test de calibration seul validerait un prédicteur nul.
- `[DÉDUIT]` **A5 se scinde** : **A5a** (scoreable, groundable) / **A5b** (contrefactuel, **infalsifiable
  par C2** → jamais de proba, un scénario). Groundable où c'est le moins précieux, impossible où ça compte le plus.
- `[DÉDUIT]` Au grain cycle, ~4 points/bin → **IC de Wilson ≈ [0,30 ; 0,95]** : calibration **indécidable** (C3).
- `[ÉTABLI]` Le « réel » d'un story point = **effort** = `SUM(issue_worklogs.minutes)` (V47) ; **si** peuplé,
  sinon proxy **latence** (biaisé). Le prédicteur calibré **existe déjà** : le **taux de base** (`GROUP BY`).

**Décidé** — A5 acté comme **scindé A5a/A5b** dans la spec. La vraie question de A5 n'est pas « calibrer le
LLM » mais « **quelque chose bat-il le taux de base ?** » (E3).

**Prochain coup**
- Frontière solo suivante : **A4** (dynamique `f`) — ou **A8** (Pareto sur trajectoires *passées*, faisable sans A4).
- Point dev en attente : vérifier si `issue_worklogs` est peuplé (décide si E1 mesure l'effort ou la latence).

---

## 2026-07-31 — Écosystème, grounding E2, système d'axiomes, structuration du labo

**Fait**
- Revue critique du **dump « écosystème en couches »** + 4 croquis → [`revues/Ecosysteme.md`](./revues/Ecosysteme.md).
- **E2 mis au cordeau** contre le **schéma réel** (V16/V23/V38 lus) : requête SQL exécutable, pièges
  documentés (pas de `completed_at` sur `cycles`, lien via `cycle_issues`, `story_points` nullable).
  → [`experiences/Experiences.md`](./experiences/Experiences.md#e2--la-dérivée-dot-x-apporte-t-elle-de-linformation-).
- **Système d'axiomes v0.1** créé → [`theorie/Axiomes.md`](./theorie/Axiomes.md) : noyau A1–A3 (grounded),
  frontière A4–A8 (chacun avec son test), carte de dépendances.
- **Brouillon ADR-012** (exposition du Brain OS, réponse à Q6) → [`decisions/`](./decisions/ADR-012-DRAFT-brain-os-exposition.md).
- Deux questions ajoutées : **Q8** (construire vers l'intérieur/extérieur), **Q9** (quel flywheel : F1/F2/F3).
- **Restructuration du dossier en laboratoire** : stations `theorie/ experiences/ revues/ references/
  decisions/`, paillasse racine (README/CLAUDE/Journal/Gabarits/Questions), ce cahier de bord.

**Trouvé**
- `[DÉDUIT]` **A5 (calibration) est le goulot** : sans savoir scorer une prédiction, ni A4 (dynamique),
  ni les probabilités, ni A8 (trajectoires) ne se groundent. Le grand système se réduit, aujourd'hui,
  à **une question à un jour** : sait-on scorer nos propres prédictions ? → **E1**.
- `[ÉTABLI]` Trois choses s'appellent « flywheel » et une seule est faible : **F1** (style, speccé),
  **F2** (mémoire organisationnelle = **le moat**, déjà à moitié bâti), **F3** (modèle du monde, étranglé
  par C1/C3). Le pitch « more usage → better models » vend **F3**, le plus faible. → vendre **F2**.
- `[ÉTABLI]` Le simulateur `MCTS/Monte-Carlo` du schéma est infaisable (C1 : rien à apprendre ; C2 :
  monde non rejouable). Ne survit qu'un **modèle System Dynamics à la main, assumé outil de pensée**.
- `[ÉTABLI]` Schéma : `cycles` n'a **pas** de `completed_at` (clôture non datée) ; seed = ~8 issues en
  cycle sur 267 → E2 sur ~4 cycles = **plomberie**, pas validation statistique (C3).

**Décidé** *(en attente de ratification humaine)*
- Reco **ADR-012 = option B** : la **connaissance** est un produit exposé (UI Brain OS déjà livrée), le
  **raisonnement** (croyances, trajectoires, écarts) reste **interne**. → à ratifier pour promotion en `v1/12-decisions/`.
- « Complet » abandonné au profit de « **reproductible** » pour le système d'axiomes (un axiome = un test SQL).

**Prochain coup**
- **E1** (grounder A5 : story points prédits vs réel, score de Brier) — **nécessite un passage en mode
  dev** + arbitrage priorité vs clôture V1.
- Option parallèle en R&D pur : **pousser la frontière A4–A8** dans le gabarit (solo, ou workflow ~7–8 agents).
- ⏳ **Ratifier ou non l'ADR-012.**

> **Intendance** — un auto-committer (probable `obsidian-git`) balaie les fichiers du labo en commits
> non déclenchés par l'agent. Sans danger, mais la section se construit en commits « fantômes ».

---

## 2026-07-17 — Amorçage du laboratoire

**Fait** — Création de la section R&D : protocole [`CLAUDE.md`](./CLAUDE.md) (contrat épistémique,
contraintes C1–C4, comité, cinq altitudes), formalisme [`theorie/Modele-mathematique.md`](./theorie/Modele-mathematique.md),
revue [`revues/World-Model.md`](./revues/World-Model.md), registres [`Questions-ouvertes.md`](./Questions-ouvertes.md)
et [`experiences/Experiences.md`](./experiences/Experiences.md), bibliothèque [`references/Bibliotheque.md`](./references/Bibliotheque.md).

**Trouvé** — Le trou central de `World Model.md` : **personne ne calcule `f`**. Sous C1–C4, `f` est soit
écrite à la main (simulation de nos croyances), soit produite par un LLM (texte chiffré) — jamais apprise.
La meilleure idée récupérable : **`ẋ`, la dérivée** (calculable en SQL).

**Décidé** — La direction retenue reste celle du 07/07 (mémoire/retrieval, sans gradient) ; `World Model.md`
est une note de recherche **sans autorité** tant qu'aucun ADR ne tranche.

**Prochain coup** — Préciser E2, esquisser l'ADR de Q6. *(fait le 31/07)*

---

**Points d'entrée :** [🔬 Labo](./README.md) · [📋 Protocole](./CLAUDE.md) · [🧰 Gabarits](./Gabarits.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
