---
id: regles-dossier-projet
title: Règles de rédaction — Dossier de validation (dossier projet RNCP DFS)
doc_type: reference
statut: active
version: 1.0
date: "19/08/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, dossier, regles, redaction, jury, integrite]
---

# Règles de rédaction du dossier de validation

> Fichier de gouvernance. À relire au début de chaque session d'écriture ou de relecture du dossier.
> Il ne contient pas le dossier : il dit comment l'écrire. Toute règle ici prime sur une habitude de
> rédaction. Voisins utiles : [[Page_de_Garde]] (page imposée), [[README]] (matrice des compétences,
> source de vérité), [[Roadmap_Documentation]] (chantiers ouverts).

## 0. Le document en une phrase

Le **dossier de validation** (aussi appelé « dossier projet ») du titre **Développeur Full Stack**
(RNCP38606, Metz Numeric School 2025-2026), adossé au projet fil rouge **TaskForce**, remis en
**papier signé** au jury de deux professionnels externes, **lu à l'écrit puis rejoué en soutenance**.
La présentation de synthèse (les diapositives) accompagne ce texte : c'est le texte qui commande, pas
l'inverse.

## 1. Contraintes de forme imposées par le certificateur

Source : note pédagogique DFS V1 2025, page 3, citée dans [[Page_de_Garde]]. La note originale n'est
pas dans le dépôt : ces règles sont **exactes mais de seconde main**. Pour verrouiller la typographie
précise (police, marges, interligne, nombre d'exemplaires), **récupérer le PDF original auprès de
l'école** avant le rendu final.

**Structure imposée, dans l'ordre :**

1. Page de garde imposée (ne pas la recréer : `assets/Page_de_Garde_Imposee.pdf`)
2. Page de sommaire
3. Avant-propos ou préface
4. Remerciements
5. Résumé du projet
6. Liste des abréviations
7. Glossaire
8. Liste des figures et des tableaux
9. Introduction
10. **Contenu : 30 à 50 pages, 10 000 à 15 000 mots**
11. **Conclusion : une page maximum, 400 à 450 mots**
12. Annexes : livrables techniques, captures d'écran, extraits de code, bibliographie

**Conséquence directe sur l'ambition.** Le contenu est plafonné à 50 pages / 15 000 mots. « Plus
dense et plus profond que les dossiers de référence » ne veut donc pas dire plus long : cela veut dire
un raisonnement plus serré, des arbitrages plus argumentés, et une **annexe riche** (extraits de code
commentés, schémas, captures) qui, elle, n'est pas comptée dans le plafond. On coupe pour tenir, on
ne dilue pas pour remplir.

## 2. Périmètre de compétences couvert

- Le dossier écrit et sa grille couvrent **C1 à C26** : **Bloc 1** (conception, C1-C12), **Bloc 2**
  (front-end, C13-C20), **Bloc 3** (back-end, C21-C26).
- Le **Bloc 4** (C27-C32, déploiement) n'est **pas noté sur la grille écrite** : il est évalué en
  mise en situation surveillée. Ses livrables E21-E29 font néanmoins partie du dossier. On le traite
  donc **de façon proportionnée** (un chapitre honnête, pas un chapitre survendu), jamais mis en avant
  au-delà de ce que la fiche de compétences justifie.
- **C11 (RGPD)** est un cas particulier : le référentiel le rattache à un **cas professionnel externe**
  (un site marchand tiers fourni par l'école), pas à TaskForce. Décision retenue : présenter le RGPD
  **de TaskForce** comme preuve de **capacité** (il est solide), et signaler franchement que le
  livrable E9 sur le cas externe dépend d'un sujet non encore transmis par l'école. Ne jamais cocher
  les 4 sous-critères de C11 « sur TaskForce » comme s'ils valaient pour le cas externe.
- Exigence de fond du référentiel, verbatim : le dossier doit comporter des **« éléments de réflexion
  personnelle »** (solutions originales aux problèmes rencontrés, capacité d'analyse et de mise en
  perspective, préconisations). Ce n'est pas un ornement : c'est un critère. D'où le registre du §4 et
  le chapitre de distance critique.

## 3. Principe structurant de la table des matières

- Le certificateur **recommande de coller la table des matières aux blocs et activités** de la
  certification. On suit ce conseil : le contenu est organisé par blocs (Bloc 1 conception, Bloc 2
  front, Bloc 3 back), avec un cadrage projet en tête.
- En complément, un **tableau d'équivalence exhaustif compétence vers section** ouvre ou clôt le
  dossier. Il reprend la [[README|matrice de couverture]] et rend le pointage du jury immédiat.
- **Chaque section nomme les critères qu'elle sert et emploie leur vocabulaire.** Le jury note
  **critère par critère** sur la grille Excel : les mots de la grille (« analyse statique »,
  « couverture d'au moins 50 % », « conforme à au moins 70 % des critères SEO », « double opt-in »,
  « compatible Chrome, Firefox et Safari », etc.) doivent apparaître dans le texte, au bon endroit.
- Chaque compétence est rattachée à son ou ses livrables **E1-E29** (voir [[README]] §2), cités
  explicitement.

## 4. Registre et style

- **Première personne** (« j'ai conçu », « j'ai choisi », « je démontre »). La certification évalue
  les compétences du candidat : le jury doit voir ce que Pierre a fait et décidé.
- **Raisonnement argumenté**, pas un catalogue. On problématise, on pose l'arbitrage (option retenue
  contre alternatives), on tranche, et **chaque section ouvre la suivante** par une transition. La
  logique est explicite. On distingue les **faits** (mesurés, dans le code), les **interprétations**
  et les **préconisations**.
- **Profondeur technique supérieure aux dossiers de référence** : extraits de code commentés, schémas
  réels dérivés du dépôt, chiffres datés. La technique est nommée **au service d'un argument**, jamais
  déposée brute.
- **Pas de listes sèches** là où un raisonnement est attendu (le template maison le dit déjà). Les
  puces servent une énumération courte, pas à esquiver une démonstration.
- **Brain OS et l'IA au-delà du smart-assign** : une demi-page maximum, cadrée usage métier
  (comprendre une organisation pour affecter finement les tâches). Aucune techno exotique, rien qui
  déborde du référentiel.
- Français correct, phrases construites, ton clair et professionnel. Pas de style télégraphique.

## 5. Intégrité : rien d'inventé, démontrable uniquement

Règle d'or : **toute affirmation doit être prouvable** par le code, un test, une mesure datée ou un
document du dépôt. Un gap ne se cache pas : il devient une **perspective assumée**.

### 5.1 Les chiffres

- **Une seule valeur par métrique**, datée, avec son périmètre. Trois jeux de couvertures ont déjà
  coexisté et se contredisaient d'une page à l'autre. La valeur de référence actuelle (à
  **re-mesurer avant le rendu**, puis figer) :

  | Indicateur | Valeur de référence | Date | Réserve à porter |
  |---|---|---|---|
  | Couverture front | 89,55 % de lignes (périmètre logique : `lib`, `hooks`, `components/auth`) ; ~92 % au run du 16/08 | 23/07 puis 16/08 | **exclut les 48 routes et les composants de présentation** (couverts par Playwright). À annoncer soi-même |
  | Suite front | 805 tests / 63 fichiers, 0 échec ; ~781 tests au 16/08 | 23/07 puis 16/08 | — |
  | Couverture back | 73,71 % de lignes (JaCoCo) ; ~75-78 % au 16/08 | 22/07 puis 16/08 | — |
  | Suite back | 792 tests, 0 échec ; ~670 tests au 16/08 | 23/07 puis 16/08 | — |

- Seuils de la grille à citer explicitement : **C18 et C25** couverture **≥ 50 %** (largement tenu),
  **C20 SEO ≥ 70 %** (mesuré 92 % accueil, 100 % sur les 4 autres pages).

### 5.2 Liste « à ne pas affirmer » (sur-déclarations connues)

Ces formulations sont fausses en l'état du code. Ne pas les écrire, ou les écrire à l'envers (honnête) :

- **pgvector dans le smart-assign** : non. Le score sémantique vient d'une réponse **JSON du LLM
  (Groq)** avec pré-filtre Java et repli. pgvector ne sert que dans le Brain OS.
- **Testcontainers** : non. Les tests back tournent sur un **vrai PostgreSQL** conteneur voisin, sans
  simulacre.
- **Flux OAuth Authorization Code** : non, c'est un **password grant** côté Keycloak.
- **Jetons en cookie HttpOnly** : non, ils sont en **localStorage** côté front.
- **OTP présenté comme MFA** : non, l'OTP n'est pas un second facteur d'authentification.
- **Rôles de projet présentés comme contrôle d'accès** : le RBAC réel est **OWNER / ADMIN / MEMBER**.
- **Scans de sécurité « en CI »** : Trivy, Semgrep et ZAP sont lancés **manuellement**
  (`security-scan.ps1`), hors CI. De même le **gate JaCoCo (0,70) lié à `verify`** reste hors CI
  (nuance C26 à porter).
- **Application déployée en production** : non. Rien n'est déployé (C28 non acquis ; C29/C30 prêts mais
  jamais exécutés en prod). `nginx.conf.example` et `docker-compose.prod.yml` sont **prêts, non
  déployés**.
- **Lighthouse de l'application** : les mesures Lighthouse portent sur le **site vitrine (landing)**,
  pas sur l'application authentifiée. Le dire.
- **Maquettes** : les PNG de `assets/maquettes/` sont brandés « TaskFlow AI » (autre produit). **Ne
  pas les insérer telles quelles.** Utiliser les [[Wireframes_Annotes|wireframes annotés]] (48 routes)
  ou des captures réelles de TaskForce.
- **C11 sur le cas externe** : les 4 sous-critères RGPD ne sont pas démontrés sur un site marchand
  tiers (cas non fourni). Ne pas les présenter comme acquis pour E9.

### 5.3 Les distances critiques sont un atout, pas un aveu

Les limites se disent en premier, calmement, avec le correctif ou la perspective : périmètre de la
couverture front, gate et scans hors CI, absence de déploiement réel, cas RGPD externe en attente,
OWASP à vérifier (le corpus indiquait une couverture partielle). Les dire soi-même, avant le jury.

## 6. Purge des caractères de signature IA

Le rendu au jury ne doit contenir **aucun** des caractères suivants (le juré est réputé réticent à
l'IA). Spécimens interdits, montrés ici entre accents graves uniquement pour être identifiés :

- tiret cadratin `—` et tiret demi-cadratin `–` : remplacer par deux-points, parenthèses, virgule, ou
  « et »
- flèches `→` `⇒` : écrire « vers », « puis », « donne »
- point médian `·` : remplacer par virgule ou puce réelle
- points de suspension en un seul glyphe `…` : écrire trois points ou reformuler
- émojis : aucun

Cette règle vaut pour le dossier **et** pour les diapositives.

## 7. Figures, schémas, captures

- Là où Pierre insérera une capture ou un schéma, laisser un repère explicite :
  `[FIGURE N : description courte | source : chemin ou "capture à prendre"]`. Idem `[TABLEAU N : ...]`.
- Numéroter figures et tableaux en continu (la section 8 imposée en exige la liste).
- Sources visuelles déjà disponibles : `assets/diagrammes/` (WBS, PBS, SMART, RACI, matrice des
  risques, organigramme), les diagrammes Mermaid de `03-architecture/` (C4, cas d'usage, classes,
  séquences, états), le [[Modele_Donnees_MCD_MLD|MCD/MLD]].

## 8. Sources autorisées (matière première)

Le dossier est une **synthèse réduite et hiérarchisée**, pas une agrégation. On puise dans les
documents ci-dessous, on coupe, on reformule ; **on ne copie pas** les brouillons tels quels.

- **Vérité compétences** : [[README]] (matrice C1-C32, maj 16/08) et la grille remplie
  (`memoire/Grille_evaluation_TaskForce_REMPLIE_DFS_25-26.xlsx`).
- **Brouillons à condenser** : [[Bloc1_Conception_Modelisation]], [[Bloc2_Frontend]],
  [[Bloc3_Backend]], [[Bloc4_Deploiement_Production]] (matière, pas dossier final).
- **Cadrage / besoin** : `01-projet/` (Dossier_Projet, CdCF_v2, CdCT_v2, STB, Note_Cadrage,
  Gantt, PERT, Budget_Previsionnel, Registre_Risques, Note_Methode_Agile).
- **Conception / archi** : `03-architecture/` (Dossier_Conception, Architecture_C4, UML *,
  Modele_Donnees_MCD_MLD, Dictionnaire_Donnees, Table_Reconciliation), `12-decisions/Journal_Decisions_ADR`.
- **Front** : `14-design/` (Design_System, Wireframes_Annotes, Accessibilite), `02-produit/Frontend`.
- **Back** : `05-api/Spec_API_OpenAPI`, `07-securite/Auth_Autorisation`, `04-engineering/Systeme_Paiement_Stripe`,
  `02-produit/Backend`, `02-produit/IA` (smart-assign).
- **Tests / indus** : `08-operations/` (Cahier_Test_Recettes, Politique_Tests, Matrice_Tracabilite_Tests,
  Rapport_Tests, Pipeline_CICD), `06-infra/Observabilite`.
- **Sécurité / RGPD** : `07-securite/` (Rapport_Securite, PSSI, Threat_Model_STRIDE, Chiffrement_Au_Repos,
  Registre_Traitements_RGPD, Audit_RGPD_Conformite, DPIA, Procedure_Violation_Donnees, Politique_Confidentialite_CGU).
- **Veille / innovation** : `17-veille/` (Veille_Technologique, Note_Innovation_Distance_Critique).

Doublons connus à arbitrer (ne garder qu'une version de référence) : CdCF v1 contre v2, CdCT v1 contre
v2, `Architecture.md` contre `Architecture_C4.md`, `Tests.md` contre `Politique_Tests.md`, `Sécurité.md`
contre `Rapport_Securite.md`. Retenir la version qui reflète le **livré**.

## 9. Production et format

- Rédaction en **Markdown Obsidian** dans `taskforce-docs`, puis export **PDF** bien mis en forme.
- Respect strict de la structure imposée (§1). Suivi du **compteur de mots** (cible 10 000 à 15 000
  sur le contenu, conclusion 400 à 450).
- Un glossaire et une liste d'abréviations sont **à produire** (aucun n'existe dans le corpus).

## 10. Checklist avant rendu

- [ ] Contenu entre 30 et 50 pages, 10 000 à 15 000 mots ; conclusion ≤ 1 page (400-450 mots)
- [ ] Les 12 éléments de structure imposée présents et dans l'ordre
- [ ] Page de garde imposée + champs (candidat, tuteur, date de soutenance)
- [ ] Tableau d'équivalence compétences C1-C26 vers sections
- [ ] Chaque critère de la grille couvert, son vocabulaire présent au bon endroit
- [ ] Chiffres re-mesurés, une seule valeur par métrique, datés, réserves portées
- [ ] Liste « à ne pas affirmer » (§5.2) respectée d'un bout à l'autre
- [ ] Zéro caractère de signature IA, zéro émoji (§6)
- [ ] Figures et tableaux numérotés et listés ; aucune maquette « TaskFlow AI »
- [ ] Glossaire et liste d'abréviations produits
- [ ] Présentation de synthèse (diapositives) annexée en PDF
- [ ] Exemplaires papier signés candidat et tuteur
