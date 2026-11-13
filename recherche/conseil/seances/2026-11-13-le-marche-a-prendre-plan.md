---
id: plan-marche-26
title: "Le plan d'accès au marché (séance n°26)"
doc_type: plan
statut: brouillon
date: "13/11/2026"
auteur: Pierre MICHEL
related:
  - "./2026-11-13-le-marche-a-prendre.md"
---

# Le plan d'accès au marché

> Issu de la [séance n°26](./2026-11-13-le-marche-a-prendre.md) du Conseil (13/11/2026), R180 à R187, en
> attente de la décision de la Présidence. Chaque chiffre porte sa source ; un chiffre sans source est une `[HYPOTHÈSE]` et ne
> fonde rien (charte, §7.2).

## 1. Le marché, compté

| | Sur la cible écrite | Sur la niche régulée |
| --- | --- | --- |
| **Marché total**, en valeur, monde | L'orchestration et l'automatisation des processus : près de 7 Md$ en 2025, plus de 21 Md$ en 2029 ([Gartner](https://www.gartner.com/en/documents/6530402), 28/05/2025). Les agents et assistants d'IA : 16,5 Md$ de dépenses en 2025, 29,2 Md$ en 2026 ([Gartner](https://www.gartner.com/en/newsroom/press-releases/2026-09-16-gartner-forecasts-worldwide-ai-spending-to-grow-49-point-5-percent-in-2026), 16/09/2026). En voisin, la gestion du travail : 7,9 à 11,9 Md$ en 2025 (Grand View, Fortune BI). Trois séries, jamais additionnées | Le LIMS : 1,48 à 3,26 Md$ (Fortune BI, 26/10/2026 ; MarketsandMarkets, 18/09/2026). Le QMS des sciences de la vie : 3,7 Md$ en 2025 ([Grand View](https://www.grandviewresearch.com/industry-analysis/life-sciences-quality-management-software-market-report), 07/2026) |
| **Marché atteignable**, en entreprises | UE : 47 477 entreprises du logiciel (J62, J58.2) de 10 à 249 personnes, plus 105 798 dans les documents (M69, M70.2, M71, M72). France : 5 703, plus 16 159 ([Eurostat](https://ec.europa.eu/eurostat/databrowser/view/sbs_sc_ovw/default/table?lang=en), 2024). Déjà sous IA en 2025 : 65,7 % des entreprises du logiciel de l'UE ([Eurostat](https://ec.europa.eu/eurostat/databrowser/view/isoc_eb_ain2/default/table?lang=en)) | France : de 720 à 2 200 entreprises des sciences de la vie de 10 personnes et plus `[DÉDUIT]` (Eurostat 2024 pour les fabricants ; [Snitem](https://www.snitem.fr/presse/dispositif-medical-une-filiere-industrielle-de-357-milliards-deuros-toujours-dynamique-mais-desormais-sous-pression/), 1 500 entreprises du dispositif ; [France Biotech et EY](https://www.ey.com/fr_fr/newsroom/2026/02/panorama-france-healthtech-2026), près de 2 800 healthtech). UE : de l'ordre de 9 000 fabricants ; [MedTech Europe](https://www.medtecheurope.org/about-the-industry/facts-figures) : 36 000 entreprises, 90 % de PME |
| **En valeur**, ordre de grandeur | 210 à 330 M$ par an dans l'UE, 24 à 38 M$ en France, au prix public de Linear (10 à 16 $ par personne et par mois). `[HYPOTHÈSE]` sur le prix : TaskForce est gratuit | Aucun coût public de la validation d'un système. Repères : la qualification pèse 5 à 10 % des coûts directs d'un grand projet ([ISPE](https://ispe.org/pharmaceutical-engineering/march-april-2026/digital-commissioning-qualification-and-validation), 03-04/2026) ; un QMS des sciences de la vie coûte dès 25 000 $ par an ([Qualio](https://www.qualio.com/pricing)) |
| **Part visée**, à douze mois | 25 entreprises actives : 0,05 % du marché atteignable de l'UE, 0,4 % de celui de la France `[HYPOTHÈSE]` | 5 entreprises actives et une validation acceptée : 0,2 à 0,7 % des entreprises françaises `[HYPOTHÈSE]` |
| **En euros** | Zéro : rien de payant avant J9 (R106) | Zéro, pour la même raison |

## 2. La cible

Des entreprises de 10 à 500 personnes, sans développeur dédié pour configurer, dont le premier travail est la livraison
logicielle et les documents (Présidence, 13/11/2026, « à peu près »). Deux critères ne se comptent pas, « sans développeur
dédié » et « valide sous GxP » : ils se testent en entretien (R180).

## 3. La niche

Les sciences de la vie sous GxP, par une seule porte : les entreprises de 10 à 250 personnes qui **livrent ou configurent du
logiciel** sous GxP (l'éditeur ou l'intégrateur de logiciel de laboratoire ou de dispositif médical, le cabinet de validation).
Jamais une décision BPF critique : le projet d'annexe 22 ferme ces usages aux modèles génératifs (R181). Pourquoi là :

- les généralistes s'arrêtent aux briques et laissent la validation au client (Microsoft, Appian, Pega, ServiceNow, UiPath,
  Atlassian) ; Camunda, n8n, Linear et monday.com n'en disent rien ;
- les spécialistes vendent aux grands ou cher : Kneat (9 des 10 premières, racheté par Thoma Bravo le 11/08/2026), ValGenesis
  (30 des 50 premières), Qualio (dès 25 000 $ par an) ; le voisin le plus proche est Ketryx, dans le logiciel des dispositifs ;
- TaskForce apporte le local, le modèle au choix, l'AGPL (GAMP 5 traite de l'open source), les règles jugées à chaque action,
  et l'expérience de la Présidence ; la preuve vérifiée hors de l'outil reste à construire (TF-J2-7) ;
- l'obligation de valider reste (Part 11, annexes 11 et 15), sa forme change (la CSA de la FDA, GAMP 5) : aider à prouver,
  jamais « conforme » (R187).

## 4. Les canaux, dans l'ordre de leur coût pour une personne seule

1. Le réseau GxP de la Présidence, pour les premiers entretiens ; quatre sur dix au moins hors de lui.
2. La démo, puis le post LinkedIn de la Présidence, récrit sur le positionnement du 13/11 ; mesuré par les téléchargements publics
   et les réponses par e-mail, sans formulaire ni traceur. LinkedIn compte 25 millions de membres en France
   ([LinkedIn](https://news.linkedin.com/fr-fr/-linkedin-compte-desormais-25-millions-de-membres-en-france), 2022).
3. Un partenaire de conception : un cabinet de validation ou un intégrateur de LIMS qui vend au forfait ; aucun revendeur avant J9.
4. ISPE France et le GAMP Francophone (environ 300 membres, depuis 2006), après un premier cas
   ([ISPE France](https://ispe.org/france-affiliate)).
5. L'open source comme preuve : le code, les essais, les versions signées, un dossier fournisseur public.
6. Pas maintenant : la publicité, les salons, les appels d'offres, les places de marché.

## 5. Les objectifs

| Horizon | Ce qui se prend | Se compte par |
| --- | --- | --- |
| **Premier mois**, du 14/11 au 13/12/2026 | Aucune part de marché : 10 entretiens (5 de la cible, 5 GxP, 4 hors du réseau) ; la démo GxP enregistrée parmi les vidéos de TF-J2-1 ; la page en ligne ; 2 partenaires de conception d'accord pour janvier ; R63 tranchée avant le 28/11 | Les notes d'entretien, la vidéo, la page, un accord d'une page |
| **Premier trimestre**, au 13/02/2027 | E20 joué ; 3 partenaires actifs sur un vrai projet, dont 1 GxP ; le post publié ; 25 entretiens au total ; un serveur en service avant le 31/12/2026 (Q13) | Une mission par semaine ; les téléchargements avant et après le post ; les comptes créés |
| **Première année**, au 13/11/2027 | 25 entreprises actives, dont 5 GxP ; une modification d'un système GxP validée chez un partenaire, sa preuve acceptée par son assurance qualité ; un partenaire qui s'en sert pour deux clients ; le modèle de revenus tranché en J9 (Q15) | Quatre semaines d'affilée avec une mission ; l'écrit de l'assurance qualité ; les démos de J8 |

Les objectifs GxP dépendent de TF-J2-7 (le dossier signé) et de TF-J2-2 (les processus) : sans eux à la fin du trimestre, le
pilote GxP ne porte que sur la documentation, et l'objectif de l'année glisse.

## 6. La première entreprise

Jamais un nom. 10 à 50 personnes ; elle livre ou configure du logiciel (son produit, un LIMS, un module) et doit prouver son
travail à un client ou à un inspecteur ; une personne de qualité ou de validation, aucun développeur dédié aux outils ; elle se
sert déjà d'un agent de code, ou le veut ; sous Windows ; une vraie modification à livrer dans les trois mois. Ce qu'on lui
montre, en dix minutes, sur des données vivantes : la demande de modification, le plan par le risque, l'agent sous les règles,
les essais et les preuves réunies en chemin, la matrice de traçabilité, les accords, le dossier, et ce que TaskForce ne fait pas.
Le premier client possible garde sa place dans E20 (R184).

## 7. Les preuves en dix jours

| Essai | Ce qu'on fait | Signal d'arrêt |
| --- | --- | --- |
| **Les entretiens** | Dix, sur une grille écrite avant : comment vous validez, ce que cela coûte en jours et en euros, avec quels outils ; « à quoi le compareriez-vous ? » ; ce qui vous ferait refuser un fournisseur ; un engagement sans argent (un vrai projet, deux heures par semaine) | Moins de trois GxP sur cinq décrivent une validation qui leur coûte ; ou moins de trois de la cible sur cinq essaieraient sur un vrai projet |
| **La démo d'un workflow GxP** | « Valider une modification » sur un vrai dépôt public (un LIMS public ou le logiciel public d'E20) : exigence, risque, modification sous les règles, essais, matrice, accords, dossier ; jugée par les cinq personnes GxP | Moins de trois sur cinq disent en deux minutes qui a accordé quoi, sur quelle preuve ; ou deux assurances qualité disent que la preuve ne passerait pas |
| **L'essai de page** | Une section du site, la promesse de la cible et celle de la niche, en mots de R187 ; le trafic du réseau puis du post | Moins de cinq réponses dans les dix jours qui suivent le post |

**Les conditions** : une personne et ses agents ; gratuit ; rien de ce plan ne prend la place d'E20 ; aucun nom de client dans
les documents publics.
