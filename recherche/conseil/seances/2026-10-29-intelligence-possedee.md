---
id: conseil-seance-2026-10-29-intelligence-possedee
title: "Séance n°10 du 29/10/2026 : posséder son intelligence, la direction de TaskForce"
doc_type: pv-seance
statut: active
date: "29/10/2026"
auteur: Pierre MICHEL
formation: plénière
tags: [recherche, conseil, seance, vision, harnais, modeles, conformite, business]
related:
  - "../README.md"
  - "./2026-10-27-vision.md"
  - "./2026-10-29-atelier-design-carte.md"
  - "../../../v1/road_to_v2/Specification_V2_Harnais.md"
---

# Séance n°10 du 29/10/2026 : posséder son intelligence, la direction de TaskForce

> Simulation : les membres sont des personnages simulés à partir de leurs positions publiques sourcées. Aucune phrase des
> interventions n'est une citation de la personne réelle ; seules les citations du dossier en sont, avec leur lien.

## Résumé

La Présidence propose une direction : les entreprises posséderont des modèles spécialisés, entraînés sur leurs données,
sous leurs propres règles, et elles les contrôleront. TaskForce en serait le harnais, d'abord pour la conformité :
réunir des outils de conformité dispersés et réduire le travail des spécialistes. Elle demande si cela colle à ce que
fait TaskForce, ce que cela coûterait, et jusqu'où l'on peut aller à coût nul.

Le Conseil valide la direction, avec une condition centrale. Il faut posséder **la boucle** avant **les poids**. La boucle,
ce sont les règles, les dossiers, les évaluations tirées des workflows, le registre des modèles et l'export des données.
Elle seule fait d'un changement de modèle une décision de l'entreprise. Les poids deviennent une option que la boucle rend
sûre. Rien n'est entraîné dans TaskForce cette année : le labo n'a ni données ni GPU (C1, C4).

Le prototype à coût nul passe par la machine du client : dans l'app desktop, son modèle tourne chez lui. La conformité est
le premier terrain, par le premier cas d'usage et un partenaire de conception, avant tout connecteur.

Il formule six recommandations, R60 à R65, toutes retenues par la Présidence le 29/10/2026.

Désaccords conservés :
- **Jeff Bezos**, contradicteur : la plupart des entreprises loueront, comme elles louent leur calcul. Il faut donc
  construire aussi pour elles, et faire de la possession une option, pas la promesse.
- **Karri Saarinen** : « unifier la conformité » est l'inverse d'un parti pris.
- **Esther Duflo** : la valeur d'un modèle spécialisé reste une hypothèse tant qu'un essai ne l'a pas mesurée.

- **Saisine** (Présidence, 29/10/2026) : « je propose au conseil, que les models puissent appartenir aux compagnies pour
  les entrainer sur leur donnez, avec leur propre regle et ainsi de suite et ils pourront les controllers. Specialized
  models. » La Présidence apporte un texte en anglais, ci-dessous résumé.
  - Constat : presque toute entreprise loue aujourd'hui son intelligence à un laboratoire de pointe. Les modèles ouverts
    sont désormais compétitifs sur des tests qui comptent.
  - Pronostic : beaucoup voudront posséder les modèles dont elles dépendent, les améliorer sur leurs données, les faire
    tourner où elles veulent, décider quand ils changent. C'est surtout vrai dans les secteurs régulés.
  - Le chaînon manquant : quelqu'un doit faire des workflows des évaluations, de l'expertise des données d'entraînement,
    des échecs de production des améliorations, et reporter tout cela à chaque nouveau modèle de base.
  - La Présidence : « ca colle a ce qu on fait ou pas du tout ? Soit honnete stp ». Puis : « je dis pas qu'on va aller
    toucher au modèle et tous les trucs-là, mais si on peut à la limite avoir un support pour ça et le faire après, là ce
    serait vraiment insane ». Elle précise le positionnement : « AI-Native Compliance Infrastructure », réunir des outils
    de conformité dispersés et réduire le travail des spécialistes, « d'ou le gros harness ».
  - Elle demande enfin d'évaluer le business, les coûts possibles, ce qu'il faut, et « a quelle niveau on peut faire un
    proto avec 0 cout », avec quelque chose en production que les gens peuvent utiliser pour un coût nul ou très faible.
- **Formation** : plénière, 24 membres (« Remobilisation du conseil ») : c'est un choix de positionnement (charte, §5).
  - Ordre de parole tiré au sort le 29/10/2026 à 18:28 UTC.
  - Contradicteur désigné : Jeff Bezos. Saarinen l'était à la n°9.
- **Fiches** : toutes à jour (moins de 30 jours). Jobs et Hamilton, sièges historiques, ne se rafraîchissent que sur
  une nouvelle source historique.

## Dossier

1. `[ÉTABLI]` **Ce que TaskForce a déjà.**
   - Un contrat neutre (`contracts/` : règles, preuve, cas partagés) et un moteur de règles déterministe, le même en
     Java et en TypeScript, prouvé par les mêmes cas.
   - Un dossier chaîné par mission (V103), et des accords humains.
   - Des modèles au choix : la passerelle IA parle à Ollama ou à toute API compatible OpenAI. L'app desktop fait tourner
     le modèle sur l'ordinateur de la personne (Ollama).
   - Le noyau pour Cortex juge aussi les outils de l'agent interne et garde son dossier (V107). Il est construit sur une
     branche, pas encore en production.
   - En production, l'IA de la webapp passe par l'offre gratuite de Groq, avec un frein d'une requête par minute et par
     compte.
2. `[ÉTABLI]` **Ce que TaskForce n'a pas.**
   - Ni entraînement, ni affinage (fine-tuning), ni export des dossiers en données d'entraînement.
   - Ni registre des modèles par tâche, ni banque d'évaluations par espace.
   - Ni connecteur d'outil de conformité, ni partenaire de conception, ni certification.
   - La spécification les annonce en partie : le harnais apprend (§14), la banque de tests et sa famille « modèles »
     (§16).
3. `[ÉTABLI]` **Les contraintes du labo** ([`CLAUDE.md`](../../CLAUDE.md) §3).
   - C1 : un seul espace d'historique réel.
   - C4 : pas de GPU, budget proche de zéro.
   - Elles excluent « tout entraînement, tout fine-tune » chez nous, et toute preuve de la valeur d'un modèle spécialisé
     sur nos propres données.
4. `[ÉTABLI]` **L'écart entre modèles ouverts et fermés.**
   - Epoch AI estime le retard des meilleurs modèles ouverts à environ quatre mois en moyenne, de janvier à mai 2026, et
     dit que l'estimation le sous-évalue peut-être, les modèles ouverts réussissant moins bien les tests privés
     ([Epoch AI](https://epoch.ai/data-insights/open-closed-eci-gap)).
   - Une analyse indépendante l'estime à huit à dix mois sur les tests privés
     ([LessWrong](https://www.lesswrong.com/posts/rJcCrXyEsJKmmDpWG/how-far-behind-are-open-models)).
5. `[ÉTABLI]` **Sur une tâche étroite, un petit modèle spécialisé peut battre un modèle de pointe.**
   - Un modèle juridique auto-hébergé obtient le meilleur F1 face à cinq systèmes commerciaux, sur l'extraction de
     clauses ([arXiv](https://arxiv.org/html/2605.05532v1), mai 2026).
   - Des modèles de moins d'un milliard de paramètres, affinés sur la tâche, battent GPT-5.4 et Claude Sonnet 4.6 sans
     exemples sur l'extraction de relations. Les auteurs attribuent le gain à l'adaptation à la tâche
     ([arXiv](https://arxiv.org/html/2606.22606v1), 2026).
   - Ce sont des prépublications, sur des tâches étroites aux jeux de test choisis. Sur un travail ouvert, les modèles de
     pointe gardent l'avantage.
6. `[ÉTABLI]` **La thèse est répandue, et le terrain est occupé.**
   - Le guide de Sequoia, « Own Your Intelligence » (Sonya Huang, 19/08/2026), place les évaluations d'abord, puis la
     méthode d'après-entraînement la plus légère qui améliore l'évaluation. Il recommande une petite équipe dédiée, et
     une boucle qui fait des trajectoires de production des évaluations et des correctifs
     ([Sequoia](https://sequoiacap.com/article/own-your-intelligence-a-how-to-guide)).
   - Des fournisseurs vendent déjà l'entraînement et l'hébergement de modèles spécialisés : Fireworks, Oumi, Baseten
     ([Fireworks](https://fireworks.ai/blog/specialized-intelligence-train-your-own-model),
     [The Deep View](https://www.thedeepview.com/articles/why-enterprise-ai-is-shifting-from-rent-to-own)).
   - Le texte apporté par la Présidence n'a pas été retrouvé mot pour mot ; sa source reste à préciser.
7. `[ÉTABLI]` **Les positions publiques de Satya Nadella, membre du Conseil.**
   - « we need to separate the supply of intelligence from the authority over it » : garder chez soi évaluations, traces
     et mémoire, et découpler l'orchestration de tout modèle unique (sa [fiche](../membres/satya-nadella.md)).
   - Son billet de juin 2026, connu par la presse : l'avantage durable viendrait des systèmes qui relient l'IA aux
     données, aux workflows et au savoir de l'entreprise, tout en permettant de changer le modèle dessous
     ([Pure AI](https://pureai.com/articles/2026/06/17/nadella-asks-will-the-future-of-ai-belong-to-frontier-models-or-frontier-ecosystems.aspx),
     [Business Today](https://www.businesstoday.in/tech-today/news/story/satya-nadella-ai-economy-microsoft-chief-says-ecosystems-matter-more-than-models-536791-2026-06-14)).
8. `[ÉTABLI]` **Affiner un modèle peut lui faire perdre ses garde-fous**, même sans intention de nuire : quelques dizaines
   d'exemples suffisent à dégrader l'alignement de sécurité d'un modèle
   ([Qi et al., arXiv 2310.03693](https://arxiv.org/abs/2310.03693), ICLR 2024).
9. `[ÉTABLI]` **La conformité « agentique » lève des fonds.**
   - Comp AI lève 34 M$ en série A en septembre 2026 ; ses chiffres de croissance sont déclarés par l'entreprise
     ([TechCrunch](https://techcrunch.com/2026/09/17/comp-ai-sets-eyes-on-a-continiously-agentic-future-for-security-and-complaince/)).
   - Complyance lève 20 M$ en février 2026, avec GV en tête de tour
     ([GlobeNewswire](https://www.globenewswire.com/news-release/2026/02/11/3236367/0/en/complyance-raises-20m-series-a-led-by-gv-google-ventures-to-modernize-enterprise-grc-with-agentic-ai.html)).
10. `[ÉTABLI]` **La loi recule ses échéances.**
    - L'Omnibus numérique sur l'IA, le règlement (UE) 2026/1744, est en vigueur depuis le 27/07/2026. Il reporte les
      obligations des systèmes à haut risque de l'annexe III au 02/12/2027, et celles de l'annexe I au 02/08/2028
      ([FPF](https://fpf.org/blog/the-ai-act-implementation-timeline-what-changes-under-the-ai-omnibus/)).
    - Les obligations des modèles à usage général gardent leur calendrier.
    - Les traces automatiques (article 12) et la supervision humaine (article 14) restent la cible de la preuve.
11. `[ÉTABLI]` **Le calcul gratuit existe, borné.**
    - Kaggle offrirait environ 30 heures de GPU par semaine, et Colab un quota gratuit variable. Ces chiffres viennent de
      comparatifs, à vérifier sur les pages officielles avant de planifier
      ([Clusy](https://www.clusy.io/compare/colab-vs-kaggle)). Selon les mêmes guides, cela suffit pour un affinage
      LoRA ou QLoRA d'un modèle d'environ 7 milliards de paramètres.
    - L'offre toujours gratuite d'Oracle est passée à 1 500 heures d'OCPU et 9 000 Go-heures par mois, soit 2 OCPU et
      12 Go en continu ([Oracle](https://docs.oracle.com/en-us/iaas/Content/FreeTier/resourceref.htm)).

## Tour de table `[HYPOTHÈSE]`

| # | Membre | L'essentiel | Notre direction ? |
| - | --- | --- | --- |
| 1 | Elon Musk (Impulsion) | Supprimer avant d'automatiser : une conformité inutile ne s'automatise pas, elle se supprime. Un prototype en trois jours sur un GPU gratuit vaut mieux qu'un plan | Oui pour posséder, non pour vendre de la paperasse |
| 2 | Esther Duflo (Science) | « Un modèle spécialisé améliore l'entreprise » est une hypothèse : mêmes tâches, modèle loué contre modèle spécialisé, évaluations écrites avant, résultats rapportés même en échec | On ne le sait pas encore ; un essai le dira |
| 3 | Satya Nadella (Pont) | Ce que l'entreprise doit posséder d'abord, c'est la boucle : évaluations, traces, mémoire, règles ; le modèle se change dessous. Le harnais est cet endroit | Oui, si la boucle passe avant les poids |
| 4 | Yann LeCun (Science) | L'IA devient une plateforme, et les plateformes s'ouvrent. À votre échelle, vous n'apprendrez pas de modèle (C1) : restez au-dessus des modèles ouverts, avec le contexte et la preuve de l'entreprise | Oui, au-dessus des modèles ouverts |
| 5 | Kenza Ait Si Abbou (Pont) | Posséder son intelligence, c'est d'abord posséder la qualité de ses données : qui les a écrites, avec quelle vision du monde. Le dirigeant entend « posséder », le spécialiste veut moins de travail | Oui, si les mots restent lisibles par un non-ingénieur |
| 6 | Steve Jobs (Impulsion, historique) | Personne n'achète une infrastructure de conformité : on achète des heures en moins sur un dossier. Dire non à l'entraînement cette année | Oui, si le produit reste un résultat ; non, si l'infrastructure devient le produit |
| 7 | Fei-Fei Li (Science) | Faire confiance, mais vérifier : évaluations par des tiers, signalement des incidents. En secteur régulé, un modèle spécialisé sans évaluation extérieure ne vaut rien | Oui, si l'on mesure avant de promettre |
| 8 | Tristan Harris (Harmonie) | Un modèle étroit est plus contrôlable qu'un agent général : c'est la bonne pente. Vérifier les incitations : ce que le client possède ne doit pas le rendre dépendant autrement | Oui, si l'étroit reste étroit |
| 9 | Jennifer Doudna (Science) | L'accès : si posséder un modèle reste réservé aux grands groupes, on reproduit l'inégalité. Le local et le gratuit sont l'argument | Oui, si une PME peut le faire |
| 10 | Yuval Noah Harari (Harmonie) | Posséder un modèle, c'est en répondre : qui signe, dans l'entreprise, quand le modèle spécialisé se trompe ? | Oui, si chaque modèle a un responsable nommé |
| 11 | Karri Saarinen (Design, conflit : Linear) | Un bon produit a un parti pris. « Réunir les outils de conformité » est l'inverse : choisir un métier, un flux, un geste | Pas encore : trop large |
| 12 | Jeff Bezos (Impulsion, contradicteur) | La plupart des entreprises loueront, comme elles louent leur calcul : posséder ce qui ne les distingue pas est une charge. Partir du client : quel spécialiste, quelle heure gagnée ? Hors fiche : l'argument s'appuie sur l'histoire d'AWS, pas sur une déclaration récente | Non, si posséder devient une fin ; oui, comme option du client |
| 13 | Atul Gawande (Science) | Le travail du spécialiste se réduit par une liste courte au bon moment, pas par un modèle plus savant. Mesurer avant et après, sur de vrais dossiers | Oui, si l'essentiel tient en une page |
| 14 | Nandan Nilekani (Harmonie) | Viser l'usage, pas le modèle. La conformité à grande échelle passe par l'architecture, et c'est ce que fait le harnais. L'inférence locale et bon marché fera la diffusion | Oui, si l'architecture porte la conformité |
| 15 | Gwynne Shotwell (Impulsion) | Un échec est une mine de données : le dossier chaîné en est déjà le registre. Chaque lancement demande des dizaines d'autorisations : la douleur du spécialiste est réelle | Oui, si chaque échec devient un cas d'essai |
| 16 | Julie Zhuo (Design) | Partir des tâches que le spécialiste déteste, raisonner en flux de travail ; un agent adjoint dont chaque action est revue ; la confiance se gagne par des évaluations | Oui, si l'on part des tâches détestées |
| 17 | Arati Prabhakar (Pont) | Chaque modèle livré avec son banc d'essai, rejoué à chaque nouvelle version de base | Oui, si chaque modèle a son banc d'essai |
| 18 | Margaret Hamilton (Science, historique) | Changer de modèle est une modification : aucune n'entre sans raison écrite, approbation et essais, et le système doit savoir revenir en arrière | Oui, si chaque changement de modèle passe par la porte |
| 19 | Don Norman (Design) | Le spécialiste doit savoir ce que fait le modèle et quand il sort de son domaine ; une automatisation à moitié faite le prive du retour | Oui, si la machine dit quand elle ne sait pas |
| 20 | Mariana Mazzucato (Pont) | Louer son intelligence, c'est payer une rente. Mais ne remplacez pas un seigneur par un autre : ce que le client possède doit pouvoir partir avec lui | Oui, sans rente fermée |
| 21 | Daniela Rus (Science) | Des modèles compacts et interprétables, sur la machine du client : c'est la voie des systèmes critiques. Mesurer la latence et la consommation | Oui, si le modèle tient sur la machine |
| 22 | Margrethe Vestager (Harmonie) | L'Europe veut du calcul et des technologies de vérification à elle ; des traces chaînées en sont une. Mais l'Omnibus repousse le haut risque à fin 2027 : ne pas vendre la peur d'une échéance | Oui, si la preuve se vérifie par d'autres |
| 23 | Yoshua Bengio (Science) | Un modèle affiné peut perdre ses garde-fous : le harnais compte davantage avec un modèle possédé. Évaluations de sûreté dans la banque, et jamais le modèle comme juge de lui-même | Oui, si la sûreté est une capacité mesurée |
| 24 | Audrey Azoulay (Harmonie) | Un modèle spécialisé encode des choix de l'entreprise : ils doivent être écrits, et lisibles par une autorité | Oui, si les choix encodés sont écrits |

## Confrontation `[HYPOTHÈSE]`

### Posséder les poids, ou posséder la boucle ?

- **Bezos**, contradicteur : on loue ce qui ne distingue pas. Un cabinet qui fait de la conformité ne veut pas gérer des
  GPU, des versions de modèles et des jeux de données. Il veut un dossier juste, vite.
- **Nadella** lui donne raison sur les poids, pas sur la boucle. Les évaluations, les traces, la mémoire et les règles
  sont propres à l'entreprise, que le modèle soit loué ou possédé. C'est la boucle qui rend le changement de modèle
  possible sans tout perdre.
- **LeCun et Rus** : sans les poids, la boucle dépend encore d'un loueur, qui peut changer son modèle ou son prix. Avec
  un modèle ouvert sur la machine, l'entreprise garde la main.
- **Mazzucato** : posséder la boucle sur un modèle loué, c'est continuer de payer la rente, même mieux informé.
- **Où l'on arrive** : la boucle d'abord, parce qu'elle fait d'un changement de modèle une décision mesurée, avec sa
  raison et son retour en arrière (Hamilton). Les poids viennent ensuite, comme option que la boucle rend sûre. L'app
  desktop offre déjà cette option à coût nul : un modèle ouvert sur la machine.
- **Bezos maintient** : il faut construire aussi pour le client qui louera toujours.

### La conformité, maintenant ?

- **Gawande, Shotwell, Vestager et Nilekani** : la douleur du spécialiste est réelle, et l'architecture peut porter la
  conformité. Le dossier chaîné est déjà une preuve.
- **Jobs et Saarinen** : « réunir des outils de conformité dispersés » ne dit ni pour qui ni quel geste. Il faut un
  métier et un dossier.
- **Duflo** : le gain de temps n'est pas mesuré.
- **Musk** : la moitié des contrôles se suppriment avant d'être automatisés.
- **Vestager ajoute** que l'Omnibus repousse les échéances du haut risque. La conformité se vend sur le temps gagné, pas
  sur la peur d'une date.
- **Où l'on arrive** : la conformité est le premier terrain, par le premier cas d'usage déjà retenu (la conformité d'un
  produit à un standard qui évolue). Elle passe par un partenaire de conception et par le temps du spécialiste mesuré
  avant et après. Aucun connecteur d'outil de conformité avant qu'un client le demande.

### Coût nul et crédibilité

- **Musk et Doudna** : tout de suite, gratuitement, en local. Un GPU gratuit suffit pour montrer la boucle.
- **Bengio, Hamilton et Li** : un modèle affiné sans évaluations de sûreté ni de qualité est un risque, en secteur régulé
  plus qu'ailleurs. Il ne doit jamais se vérifier lui-même.
- **Jobs** : rien sur le site avant que ça marche (R12).
- **Où l'on arrive** : une seule expérience déclarée, sur le corpus public de la banque de tests (§16.2), jamais sur des
  données de client. On compare le modèle de base, le modèle de base avec recherche, et le modèle affiné, sur les mêmes
  évaluations écrites avant, sûreté comprise. Les résultats sont rapportés, échec compris.

## Le business : ce que cela coûte, ce qu'il faut, jusqu'où à coût nul `[HYPOTHÈSE]`

Le Conseil raisonne par paliers. Chaque palier se finance seul et prouve une chose, une seule.

| Palier | Ce qu'on construit | Coût pour TaskForce | Ce que ça prouve | Ce que ça ne prouve pas |
| --- | --- | --- | --- | --- |
| 0 | L'existant : harnais, dossiers, règles, modèles locaux dans l'app desktop, webapp avec le frein de la bêta | L'infrastructure actuelle (coût réel à confirmer par la Présidence) | Que l'IA de l'entreprise peut tourner chez elle, sous ses règles | Qu'elle s'améliore |
| 1 | Les évaluations tirées des workflows : une tâche échouée, refusée ou regrettée devient un cas, avec son résultat attendu écrit. Plus le registre des modèles par tâche : lequel, qui l'a choisi, pourquoi, son score | 0 €, du code | Qu'un changement de modèle se décide sur preuve | La valeur d'un modèle spécialisé |
| 2 | L'export des dossiers en données d'entraînement, en formats ouverts, avec consentement et filtre de sensibilité | 0 €, du code | Que l'entreprise peut entraîner où elle veut, sans nous | Que l'entraînement aide |
| 3 | Une démonstration d'affinage : un petit modèle ouvert sur le corpus public, sur un GPU gratuit, puis dans Ollama | 0 € de calcul, dans les quotas gratuits | La boucle de bout en bout | La valeur sur des données réelles (C1) |
| 4 | Avec un partenaire de conception : la boucle sur ses données, sur sa machine | Son matériel ; notre temps | Le temps gagné du spécialiste, mesuré | Que d'autres paieront |
| 5 | Vendre en secteur régulé : sécurité, audits, certifications, support | Élevé, à chiffrer | Que le marché paie | |

- **Mettre en production pour un coût nul** :
  - Seule l'app desktop le permet à grande échelle, parce que le modèle tourne sur l'ordinateur de la personne. Elle se
    distribue gratuitement, par GitHub et le Microsoft Store.
  - La webapp reste une démonstration : au-delà de l'offre gratuite de Groq, chaque requête se paie.
  - Si l'hébergement actuel s'arrête, un petit serveur coûte de l'ordre de dix euros par mois (devis à refaire).
  - Posséder son intelligence et servir chacun à coût nul sont donc la même architecture : le local.
- **Ce qu'il faut** :
  - Le temps de la Présidence.
  - Un partenaire de conception dans le secteur régulé du premier cas d'usage.
  - Le savoir-faire des évaluations.
  - Rien d'autre pour les paliers 0 à 3.
- **Ce qu'il ne faut pas faire** : l'infrastructure d'entraînement et d'hébergement. Des fournisseurs financés l'occupent
  (dossier, point 6). TaskForce gagne au-dessus d'eux, là où la boucle se décide.

## Recommandations `[HYPOTHÈSE]`

Numérotées à partir de R60 (R59 est la dernière existante). Chacune porte qui la soutient, qui s'y oppose, sa preuve en
dix jours et son signal d'arrêt.

### R60. La direction : le harnais de l'intelligence possédée

- TaskForce aide une entreprise à posséder son intelligence : ses règles, ses dossiers, ses évaluations, et demain ses
  modèles. Cela vaut sur n'importe quel modèle, loué ou possédé, là où elle le choisit.
- Le harnais est l'endroit où le travail de l'entreprise devient son intelligence.
- La conformité est le premier terrain : réduire le travail du spécialiste.
- Cela prolonge la vision du 27/10 (« partout où une IA agit, un harnais réglé par ceux qui en répondent ») sans la
  remplacer.

- **Pour** : Nadella, Nilekani, Shotwell, Mazzucato, LeCun, Rus, Hamilton, Gawande, Vestager, Harris, Doudna, Zhuo,
  Prabhakar, Bengio, Li, Azoulay, Norman, Ait Si Abbou, Harari, Musk, avec leurs conditions.
- **Contre** :
  - Bezos, contradicteur : la possession doit rester une option du client.
  - Saarinen : trop large.
  - Jobs : non, si l'infrastructure devient le produit.
  - Réserve de Duflo : une hypothèse, tant qu'un essai ne l'a pas mesurée.
- **Preuve en dix jours** : celles de R61 et R62.
- **Signal d'arrêt** : dans trente jours, aucune équipe ne décide un changement de modèle par ses évaluations, et aucun
  partenaire ne veut de la boucle.

### R61. Posséder la boucle avant les poids

- **La banque d'évaluations de l'espace**, nourrie par les dossiers : une tâche échouée, refusée ou regrettée devient un
  cas, avec son résultat attendu écrit.
- **Le registre des modèles par tâche** : lequel tourne, quelle version, qui l'a choisi, pourquoi, son score. Changer de
  modèle est un changement de règle : raison écrite, accord, évaluations rejouées, retour en arrière possible (Hamilton).
- **L'export des dossiers en données d'entraînement**, en formats ouverts, avec consentement et filtre de sensibilité.
- Aucun entraînement dans TaskForce cette année (C1, C4).

- **Pour** : Nadella, Hamilton, Prabhakar, Li, Zhuo, Shotwell, Duflo ; Bezos, comme option du client.
- **Contre** : LeCun et Rus, en réserve : sans les poids, la boucle dépend encore d'un loueur. Le modèle local de l'app
  desktop y répond en partie. Mazzucato partage la réserve.
- **Preuve en dix jours** : dans un espace, une tâche (par exemple le résumé des commentaires) change de modèle après
  avoir rejoué ses évaluations. La décision est au dossier, et le retour en arrière est essayé.
- **Signal d'arrêt** : des évaluations que personne ne lit, ou un changement de modèle fait sans elles.

### R62. Le prototype à coût nul passe par la machine du client

- **Le local d'abord** : dans l'app desktop, le modèle de l'entreprise tourne chez elle. Le coût par personne est nul
  pour TaskForce. La webapp reste une démonstration, sous le frein de la bêta.
- **Une expérience déclarée** (labo, §9) : affiner un petit modèle ouvert sur le corpus public de la banque de tests,
  sur un GPU gratuit, puis le faire tourner dans Ollama. On le compare au modèle de base, avec et sans recherche, sur les
  mêmes évaluations écrites avant, sûreté comprise.

- **Pour** : Musk, Doudna, Rus, LeCun, Nilekani, Harris.
- **Contre** :
  - Bengio, Hamilton et Li, en réserve : aucun modèle affiné dans le produit avant ses évaluations de sûreté.
  - Jobs : rien sur le site avant que ça marche.
- **Preuve en dix jours** : l'expérience faite pour 0 €, résultats rapportés, échec compris.
- **Signal d'arrêt** : si le modèle affiné ne bat pas le modèle de base avec recherche sur les évaluations, on ne promet
  pas l'entraînement. La boucle reste les évaluations et le choix du modèle.

### R63. La conformité comme premier terrain, par un partenaire

- Le premier cas d'usage, la conformité d'un produit à un standard qui évolue, se présente comme un travail de
  conformité : réduire la charge du spécialiste.
- Le dossier est la pièce justificative : traces automatiques (article 12), supervision humaine (article 14).
- Un partenaire de conception dans un secteur régulé, avant tout connecteur d'outil de conformité.
- On vend le temps gagné par dossier, pas une « infrastructure ».
- L'Omnibus repousse le haut risque à décembre 2027 : on ne vend pas la peur d'une échéance.

- **Pour** : Gawande, Shotwell, Vestager, Nilekani, Zhuo, Azoulay ; Jobs, si le produit reste un résultat.
- **Contre** :
  - Musk : supprimer les contrôles avant de les automatiser.
  - Saarinen : un métier, pas « réunir ».
  - Duflo : mesurer d'abord.
- **Preuve en dix jours** : un spécialiste du partenaire fait une vraie revue dans TaskForce, et son temps est mesuré
  avant et après.
- **Signal d'arrêt** : pas de partenaire dans trente jours. On reste alors sur la niche A (les équipes logicielles avec
  agents), et la conformité attend.

### R64. Ce qui est possédé part avec le client

- Pas de nouveau loueur : les règles, les dossiers, les évaluations, les jeux de données et, plus tard, les modèles
  adaptés s'exportent en formats ouverts (R9').
- Un espace part avec tout, et le client peut faire tourner ses modèles sans TaskForce.

- **Pour** : Mazzucato, Vestager, Harris, LeCun, Doudna, Azoulay.
- **Contre** : aucun. Réserve de Bezos : la portabilité ne vend pas seule.
- **Preuve en dix jours** : un aller-retour d'export et d'import des règles, des dossiers et des évaluations d'un
  espace.
- **Signal d'arrêt** : une fonction qui ne marche que dans notre nuage.

### R65. Les mots avant la page

- Kenza Ait Si Abbou, cheffe de file du vocabulaire, éprouve deux formules auprès de cinq personnes de la cible (un
  spécialiste, un responsable) avant que le site change : « posséder son intelligence » et « infrastructure de
  conformité native IA ».
- Rien sur l'entraînement sur le site avant que ça marche (R12).
- Le harnais reste invisible à la personne (R22, J8).

- **Pour** : Ait Si Abbou, Jobs, Norman, Zhuo, Saarinen.
- **Contre** : Musk, en réserve : parler aux clients, pas des mots.
- **Preuve en dix jours** : cinq entretiens, où chacun redit la promesse en une phrase.
- **Signal d'arrêt** : moins de trois sur cinq la comprennent.

## Décision de la Présidence (29/10/2026)

Toutes les recommandations sont retenues telles que le Conseil les a formulées : « on suit le conseil sur tout, go ».
Les objections de Bezos, contradicteur, et de Saarinen, comme la réserve de Duflo, restent au PV sans être retenues.

| Recommandation | Décision | Raison de la Présidence |
| --- | --- | --- |
| R60 à R65 | Retenues | « on suit le conseil sur tout » |
| La source du texte apporté | Non précisée | Question encore posée à la Présidence (Q13) |
| Les questions du Conseil : hébergement, temps, partenaire | Non tranchées | Q13 |

## Notes du secrétariat

- **Ordre de parole** tiré au sort le 29/10/2026 à 18:28 UTC (`shuf`). Contradicteur désigné : Jeff Bezos.
- **Contraintes du terrain** : C1 et C4 opposées dès l'ouverture (dossier, point 3). Elles excluent tout entraînement
  dans le labo ; l'expérience de R62 se fait hors du labo, sur un GPU gratuit et un corpus public.
- **Hors fiche** : l'argument de Bezos sur la location s'appuie sur l'histoire d'AWS, pas sur une déclaration récente de
  sa fiche.
- **Prudence sur les sources** :
  - Le billet de juin 2026 de Nadella n'est connu que par la presse : l'original n'a pas été joint.
  - Les quotas de GPU gratuits viennent de comparatifs, à vérifier sur les pages de Kaggle et de Google.
  - Les chiffres de Comp AI sont déclarés par l'entreprise.
  - Les gains des petits modèles spécialisés viennent de prépublications, sur des tâches étroites.
- **Le texte de la Présidence** n'a pas été retrouvé mot pour mot. Des textes proches existent (dossier, point 6). Sa
  source est demandée : si c'est un appel d'investisseurs, y répondre devient une suite possible.
- **Questions à la Présidence** :
  - Le coût réel de l'hébergement actuel, et jusqu'à quand il tient.
  - Le temps qu'elle peut donner chaque semaine.
  - Le partenaire de conception possible, dans le secteur du premier cas d'usage.

## Avis du secrétariat

Après la clôture, l'avis du secrétariat, qui est le mien et pas celui du Conseil.

- `[DÉDUIT]` **Sur le fond, ça colle.** Le chaînon que le texte dit manquant est ce que le harnais est en train de devenir : faire
  des workflows des évaluations, et des échecs des améliorations, puis le reporter à chaque nouveau modèle.
  - TaskForce en a les fondations : les règles, le dossier chaîné, les accords, le choix du modèle, le modèle local dans
    l'app desktop.
  - La spécification annonçait la suite : le harnais apprend (§14), et la banque de tests compare déjà petits modèles et
    grands modèles (§16).
- `[ÉTABLI]` **À la lettre, pas encore.** Il n'existe ni entraînement, ni export de données, ni banque d'évaluations par espace, ni
  registre des modèles, ni connecteur de conformité, ni partenaire. Le labo ne peut pas prouver la valeur d'un modèle
  spécialisé sur nos données (C1, C4). Dire « c'est à peu près ce qu'on a fait » serait faux : on a le socle, pas la
  boucle.
- `[DÉDUIT]` **Où ne pas aller** : l'entraînement et l'hébergement de modèles. Le terrain est occupé par des fournisseurs financés,
  et il demande du capital.
- `[HYPOTHÈSE]` **Où TaskForce peut gagner** : la couche du dessus, là où la boucle se décide. Elle est locale d'abord, ouverte, avec
  un moteur de règles déterministe et une preuve chaînée. C'est ce que le guide de Sequoia appelle un harnais sur
  mesure, avec sa boucle.
- `[HYPOTHÈSE]` **La conformité** n'est crédible que par le premier cas d'usage et un partenaire. « Réunir les outils de conformité
  dispersés » est une promesse trop large pour une équipe d'une personne. « Réduire la charge du spécialiste sur un type
  de dossier » est tenable.
- `[DÉDUIT]` **Le coût** : 0 € pour les paliers 0 à 3. Le vrai coût est le temps de la Présidence, et la recherche d'un partenaire.

## Suites

Si la Présidence retient ces recommandations :
- **La spécification** reçoit la direction (§1) et une section sur la boucle : banque d'évaluations, registre des
  modèles, export des données.
- **La roadmap** reçoit un lot : les paliers 1 et 2, puis l'expérience de R62.
- **L'atelier des écrans** reprend, sur la carte des sept workflows (R58), avec deux workflows de plus : « une erreur
  devient un cas d'essai » et « changer de modèle ».
- **Le registre** des séances reçoit sa ligne, et le PV est commité.
