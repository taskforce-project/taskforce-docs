---
id: dossier-validation
title: Dossier de validation — TaskForce (RNCP38606, DFS)
doc_type: memoire
statut: squelette
version: 0.2
date: "19/08/2026"
auteur: Pierre MICHEL
tags: [memoire, rncp, dossier-validation, dfs, taskforce]
---

<!--
  GOUVERNANCE : ce document obéit à [[_REGLES_Dossier_Projet]]. Le relire avant chaque session.
  STATUT : squelette. Les blocs `<!-- ... -->` sont des consignes de rédaction ; ils N'APPARAISSENT
  PAS dans le PDF exporté. Convention figures : [FIGURE N : ... | source : ...].
  RÉCIT (Duarte) : les 4 PARTIES sont les mouvements du récit (problème, choix, construction, recul).
  Chaque section ouvre sur la tension traitée et ferme sur ce que le choix a changé.
  SOMMAIRE : 3 niveaux numérotés max (chapitre.section.sous-section), regroupés sous parties (bannières).
  Sous-sections seulement là où une section se scinde vraiment (ex. 3.5, 5.5, 6.5).
-->

# Dossier de validation — TaskForce

Certification **Développeur Full Stack**, RNCP38606, niveau 6. Metz Numeric School, 2025-2026.
Projet fil rouge : **TaskForce**, outil de répartition dynamique des tâches.

---

## Pages liminaires (structure imposée)

<!-- Ordre imposé, ne pas réordonner. Enrichissements pro validés : abstract EN + keywords. -->

- **Page de garde** imposée : insérer `assets/Page_de_Garde_Imposee.pdf`. Champs : candidat
  (Pierre MICHEL), tuteur (à confirmer), date de soutenance (28 ou 29 septembre 2026), signatures
  manuscrites sur le papier.
- **Sommaire** (généré, 3 niveaux numérotés maximum, sous bannières de parties).
- **Avant-propos / préface**. <!-- Cadre personnel court : d'où vient le projet, l'intention. -->
- **Remerciements**. <!-- École, équipe pédagogique, tuteur, jury. Sobre. -->
- **Résumé du projet** (FR). <!-- 200-250 mots, porte déjà l'arc transformation. -->
- **Abstract** (EN) + **Mots-clés / Keywords**.
- **Liste des abréviations**. <!-- À PRODUIRE : API, RBAC, OIDC, JWT, CI, RGPD, MCD/MLD, SSR, CSP... -->
- **Glossaire**. <!-- À PRODUIRE : aucun n'existe dans le corpus. -->
- **Liste des figures et des tableaux**. <!-- Générée en fin de rédaction. -->

---

## Sommaire

<!-- Version de travail, à régénérer. Parties = bannières de récit, non numérotées. -->

**Introduction**

**Partie I — Comprendre le problème et cadrer le projet**
- 1. Contexte, demande et cadrage
  - 1.1 Le problème métier et la reformulation de la demande
  - 1.2 Préconisations et parti pris technique
  - 1.3 Caractéristiques du projet : public, sécurité, SEO, délais, budget
  - 1.4 Périmètre livré, acteurs et rôles
  - 1.5 Enjeu économique, valeur et modèle d'affaires
- 2. Conduite de projet
  - 2.1 Méthode agile et rituels
  - 2.2 Environnement de développement collaboratif
  - 2.3 Planification, budget prévisionnel et risques
  - 2.4 Documentation vivante et suivi de projet (Brain OS)
  - 2.5 Veille technologique et influence sur les décisions

**Partie II — Concevoir : des choix aux modèles**
- 3. Choix technologiques et arbitrages
  - 3.1 Démarche de choix et contraintes
  - 3.2 Étude comparative back-end et choix retenu
  - 3.3 Étude comparative front-end et choix retenu
  - 3.4 Base de données et choix retenu
  - 3.5 L'écart au cahier des charges : un choix assumé
    - 3.5.1 Ce que le cahier des charges demande
    - 3.5.2 Ce que j'ai choisi et pourquoi
    - 3.5.3 Conformité réelle et écart maîtrisé
- 4. Conception et modélisation
  - 4.1 Wireframes et parcours
  - 4.2 Du besoin au dossier de conception et cas d'usage
  - 4.3 Modélisation UML : classes, séquences, états
  - 4.4 Modèle de données MCD/MLD et persistance
  - 4.5 Architecture logicielle : C4, modules, multi-tenant

**Partie III — Construire le produit**
- 5. Développement du front-end
  - 5.1 Interface et charte graphique
  - 5.2 UX, parcours et accessibilité
  - 5.3 Qualité, sécurité et écoconception du code front
  - 5.4 Consommation sécurisée de l'API
  - 5.5 Tests du front-end
    - 5.5.1 Périmètre et méthode
    - 5.5.2 Résultats et couverture
    - 5.5.3 Réserve assumée sur le périmètre
  - 5.6 Industrialisation du front
  - 5.7 Performances et SEO
- 6. Développement du back-end
  - 6.1 Persistance et sécurité en profondeur
  - 6.2 Qualité, sécurité et écoconception du code back
  - 6.3 Paiement et monétisation
  - 6.4 API REST sécurisée
  - 6.5 Le moteur IA et le smart-assign
    - 6.5.1 Le problème d'affectation
    - 6.5.2 Le pré-filtre et le scoring
    - 6.5.3 Repli et garde-fous
  - 6.6 Tests du back-end
  - 6.7 Industrialisation du back

**Partie IV — Sécuriser, industrialiser et prendre du recul**
- 7. Sécurité et conformité RGPD
  - 7.1 Posture de sécurité
  - 7.2 RGPD de TaskForce
  - 7.3 Le cas RGPD externe
- 8. Industrialisation, déploiement et supervision
  - 8.1 Documentation technique et base de connaissances
  - 8.2 Intégration continue et déploiement automatisé
  - 8.3 Hébergement et production
  - 8.4 Supervision, journalisation, observabilité
- 9. Distance critique et perspectives
  - 9.1 Innovations
  - 9.2 Limites assumées et dette technique
  - 9.3 Préconisations et évolutions

**Conclusion**

**Annexes**

---

<!--
  PLAN DES FIGURES ET TABLEAUX (document de travail, deviendra la "Liste des figures et tableaux").
  Le corpus fournit déjà l'essentiel ; le dossier doit être dense en schémas. Cible : au moins une
  figure ou un tableau par chapitre lourd. Réserve disponible et affectation :
    1.3 / 2.3  : Gantt (Gantt_Planning), PERT (Diagramme_PERT), matrice des risques + organigramme +
                 RACI + SMART (assets/diagrammes/*.drawio.png, RACI xlsx/pdf)
    3.2-3.4    : 3 TABLEAUX comparatifs (back / front / BDD) avec colonne "choix retenu"
    4.1        : wireframes TaskForce (Wireframes_Annotes ; NE PAS prendre les PNG TaskFlow AI)
    4.2        : diagramme de cas d'usage (Diagramme_Cas_Usage_UML)
    4.3        : diagramme de classes (38 entités) + séquence smart-assign (Diagramme_Classes/Sequence_UML)
    4.4        : MCD/MLD MERISE (Modele_Donnees_MCD_MLD) + extrait dictionnaire (Dictionnaire_Donnees)
    4.5        : C4 contexte/conteneurs/composants + carte des modules (Architecture_C4, Modules)
    5.1-5.2    : palette + tokens du design system, captures d'écran, résultat axe-core
    5.7        : scores Lighthouse SEO (accueil + 4 pages)
    6.4        : capture Swagger / OpenAPI ; 6.5 : schéma pré-filtre + scoring smart-assign ; 6.6 : JaCoCo
    7.1        : DFD STRIDE (Threat_Model_STRIDE) ; 7.2 : parcours droits RGPD
    8.2        : chaîne CI/CD (Pipeline_CICD) ; 8.3 : diagramme de déploiement ; 8.4 : SigNoz + alertes
  Convention : numérotation continue [FIGURE N] / [TABLEAU N], légende + source sous chaque visuel.
  Les diagrammes Mermaid seront exportés en image nette pour le PDF ; les captures seront prises par Pierre.
-->

## Introduction

<!-- L'arc de transformation complet (Duarte) : le problème (surcharge et répartition ad hoc des
tâches), pourquoi il compte (coût de coordination, dépendance aux personnes clés), ce qui existait
(tableurs, outils génériques), ce que j'ai construit (TaskForce et son moteur d'affectation), pourquoi
ces choix, ce que ça change. Question directrice + annonce des 4 parties. Registre argumenté.
Sources : 01-projet/Dossier_Projet, IDEA.md, Note_Innovation_Distance_Critique. -->

_À rédiger._

---

## Partie I — Comprendre le problème et cadrer le projet

<!-- Mouvement 1 : le problème et pourquoi il compte. Ouvre l'arc. -->

### 1. Contexte, demande et cadrage

#### 1.1 Le problème métier et la reformulation de la demande
<!-- Critères : C1 [E1]. Sources : Dossier_Projet, 01_CdCF, CDC école. Rédigé v0.3. -->

Le point de départ de TaskForce n'est pas une fonctionnalité, c'est une friction quotidienne. Dans une équipe qui livre, répartir les tâches à la main devient vite une source de déséquilibres de charge, de perte de productivité et de démotivation. Le constat est documenté : un responsable consacre jusqu'à 40 % de son temps à des tâches administratives de coordination (McKinsey, 2023), pendant que 44 % des salariés déclarent un stress chronique (Gallup, 2023). Les outils installés sur ce marché, Jira, Linear ou Asana, savent suivre l'état d'une tâche, mais ils n'assistent pas la décision d'affectation : à qui confier ce travail, compte tenu des compétences réelles, de la charge courante et des disponibilités de chacun.

C'est cette décision, et non le suivi, que le projet devait outiller. **J'ai analysé la demande** initiale du cahier des charges, un outil de répartition dynamique des tâches, puis **je l'ai reformulée** en un besoin précis : proposer au responsable une affectation argumentée qu'il valide ou ajuste, plutôt qu'une liste de tickets à trier à la main. Le responsable reste décisionnaire ; l'outil porte la charge cognitive de la proposition.

De cette reformulation découle le produit livré : TaskForce, un logiciel de gestion de projet multi-locataire dont le différenciateur est un moteur de répartition intelligente des tâches. Là où un gestionnaire de tickets classique attend qu'on lui indique qui fait quoi, TaskForce calcule une recommandation à partir des compétences, de la charge et des disponibilités, l'explique, et laisse le dernier mot à l'humain. Tout le dossier montre comment ce parti pris a orienté les choix qui suivent, de l'architecture jusqu'aux tests.

#### 1.2 Préconisations et parti pris technique
<!-- Critères : C2 [E1, E3]. Sources : Note_Innovation_Distance_Critique, Journal_Decisions_ADR. Rédigé v0.3. -->

Répondre à ce besoin supposait davantage que de coder un cahier des charges : il fallait **conseiller** sur la direction technique et en **assumer les préconisations**. J'ai porté trois partis pris.

Le premier est le cœur du produit : faire de l'affectation une aide à la décision assistée par l'IA, et non une règle figée. La recommandation combine un score déterministe (compétences, charge, disponibilité) et un affinage par un modèle de langage, tout en restant explicable et réversible. C'est ce qui sépare TaskForce d'un énième gestionnaire de tickets.

Le deuxième est architectural : un socle applicatif, le Core, qui porte l'authentification, le multi-locataire et la sécurité, et un module métier de gestion de projet posé dessus. Ce découpage n'est pas décoratif ; il prépare l'extension vers des modules spécialisés sans réécrire le socle, et il isole les préoccupations transverses.

Le troisième est le modèle de distribution : un SaaS multi-locataire, où plusieurs organisations cohabitent sur une même instance avec une isolation stricte de leurs données. C'est une exigence de sécurité autant qu'un choix économique.

Ces préconisations engageaient une pile technique, et c'est là que se situe l'écart le plus visible avec le cahier des charges. Je l'expose et je l'argumente au chapitre 3.

#### 1.3 Caractéristiques du projet : public, sécurité, SEO, délais, budget
<!-- Critères : C3 [E2]. Sources : Note_Cadrage, Gantt_Planning, Budget_Previsionnel, Registre_Risques. Rédigé v0.3. -->

Caractériser le projet, c'est fixer ses contraintes avant d'écrire la première ligne de code. Cinq dimensions ont cadré TaskForce.

Le **public cible** est la PME, typiquement de 50 à 250 collaborateurs, avec deux profils d'usage : le responsable qui affecte et arbitre, le collaborateur qui exécute et signale sa charge.

La **sécurité** et la conformité n'étaient pas négociables : le RGPD, l'accessibilité WCAG 2.1 AA et le référentiel OWASP encadraient le développement, une non-conformité valant blocage. J'y ai répondu par une analyse statique du code (Semgrep), une analyse des dépendances (Trivy), un test d'intrusion automatisé (ZAP) et un chiffrement des données sensibles au repos, sans vulnérabilité critique résiduelle. Le chapitre 7 y revient en détail.

Le **référencement naturel (SEO)** a dicté un choix concret : le site vitrine est bâti avec Astro, pour un rendu statique favorable au SEO, cohérent avec une acquisition en libre-service.

Les **délais** ont formé le cadre le plus rigide. Le développement s'est étalé sur environ neuf mois, de novembre 2025 à juin 2026, avec un gel des fonctionnalités en fin de parcours et une échéance de certification à l'automne 2026 qui ne se négociait pas. Six jalons ont rythmé la trajectoire, du Core livré en janvier 2026 au gel fonctionnel de juin 2026.

Le **budget**, enfin, distingue la valeur du travail de la dépense réelle. La charge représente environ 71 jours-homme, soit une valeur de travail de l'ordre de 38 000 €. L'infrastructure de développement, entièrement conteneurisée en local, n'a rien coûté ; la mise en production est projetée entre 500 et 900 € par an. Le projet a été mené seul, sans financement externe.

[FIGURE 1 : diagramme de Gantt et jalons J1 à J6 | source : Gantt_Planning]
[FIGURE 2 : matrice des risques (probabilité et impact) | source : Registre_Risques]

#### 1.4 Périmètre livré, acteurs et rôles
<!-- Sources : CdCF_v2 (12 UC, hors-périmètre), Diagramme_Cas_Usage_UML. RBAC réel OWNER/ADMIN/MEMBER. Rédigé v0.3. -->

Le périmètre livré se lit à travers ses acteurs et ses cas d'usage.

Le cahier des charges initial distinguait un collaborateur, un manager et un responsable de projet. Le modèle réellement livré les traduit en trois rôles hiérarchiques, portés par le contrôle d'accès de l'application : le **MEMBER** (le collaborateur, qui exécute ses tâches), l'**ADMIN** (le gestionnaire, qui pilote une équipe et hérite des droits du membre) et l'**OWNER** (le propriétaire de l'espace de travail, qui gère l'abonnement et hérite des droits de l'admin). Deux acteurs externes complètent le tableau : Stripe, pour la facturation, et un ordonnanceur interne qui déclenche les alertes de surcharge.

Sur ce socle de rôles, douze cas d'usage constituent la version 1.

| Cas d'usage | Intitulé |
|:---:|---|
| UC01 | S'authentifier |
| UC02 | Gérer ses tâches personnelles |
| UC03 | Créer et traiter une issue |
| UC04 | Déclencher la répartition intelligente (smart-assign) |
| UC05 | Redistribuer automatiquement la charge |
| UC06 | Gérer les compétences |
| UC07 | Gérer les congés et disponibilités |
| UC08 | Échanger (canaux et discussions) |
| UC09 | Interroger l'assistant IA |
| UC10 | Gérer l'abonnement |
| UC11 | Exporter ses données personnelles (RGPD) |
| UC12 | Administrer l'espace de travail |

Le hors-périmètre a été documenté et assumé plutôt que subi : les modules spécialisés (LIMS, Qualité, gestion documentaire), le rôle d'invité externe, l'export de rapports en PDF et Excel, l'authentification unique SAML et l'internationalisation relèvent du backlog, pas de la version 1. Ce tri est un acte de conception : livrer un périmètre cohérent et testé vaut mieux qu'un périmètre large et fragile.

[FIGURE 3 : diagramme des cas d'usage (trois acteurs, douze cas) | source : Diagramme_Cas_Usage_UML]

#### 1.5 Enjeu économique, valeur et modèle d'affaires
<!-- Appuie C3. Sources : Etude_business, Business_Model_Pricing. Rédigé v0.3. Chiffres business divergents (ARR/SOM/conversion) volontairement écartés ; une seule donnée marché citée et sourcée. -->

Si le problème est réel, encore faut-il que sa résolution ait de la valeur. C'est l'objet de ce cadrage économique, tenu volontairement sobre, car le dossier reste avant tout un dossier de développement.

La proposition de valeur tient en une phrase : TaskForce supprime la surcharge managériale liée à la répartition manuelle des tâches. Le système propose, détecte la surcharge, et le responsable valide. Le différenciateur est un moteur d'affectation explicable (compétences, charge, disponibilité, affiné par un modèle de langage), là où les outils installés gèrent l'état des tâches sans assister la décision.

Le marché porte cette valeur : le logiciel de gestion de projet est un secteur en croissance soutenue, estimé autour de 9,9 milliards de dollars en 2023 et attendu vers 17,7 milliards en 2028, soit une croissance annuelle proche de 11 % (MarketsandMarkets, Statista). Surtout, l'IA y est devenue le premier déclencheur d'achat pour une majorité d'acheteurs (Capterra, 2025). Le segment visé, la PME, reste peu servi sur ce terrain de l'aide à la décision.

Le modèle économique est un freemium par siège, dans l'esprit de Linear : un plan gratuit permanent pour l'adoption, puis des plans payants facturés au membre, l'assistance par IA étant incluse plutôt que vendue en supplément, à rebours de plusieurs concurrents. La version 1 livre cette mécanique de bout en bout : inscription en plan gratuit, passage à un plan payant en libre-service via Stripe Checkout, et gestion des événements de facturation par webhooks. La grille tarifaire complète est encore en consolidation ; le chapitre 6 décrit le paiement tel qu'il est réellement implémenté.

Ce cadrage, le problème, sa valeur et son modèle, fixe la barre que les choix techniques devaient tenir. C'est à ces choix qu'est consacré le chapitre suivant.

### 2. Conduite de projet

#### 2.1 Méthode agile et rituels
<!-- Critères : C4 [E5, E6]. Sources : Note_Methode_Agile, Trame_Compte_Rendu_Activite, CR_2026-S30. Cycles dans l'app = preuve vivante. -->
_À rédiger._

#### 2.2 Environnement de développement collaboratif
<!-- Critères : C5 [E4]. Sources : quickstart/README, GHCR_USAGE, docker-compose.dev, git-workflow/. -->
_À rédiger._

#### 2.3 Planification, budget prévisionnel et risques
<!-- Appuie C3. Sources : Gantt_Planning, Diagramme_PERT, Budget_Previsionnel (CAPEX/OPEX), Registre_Risques. [FIGURE : Gantt] [FIGURE : matrice des risques]. -->
_À rédiger._

#### 2.4 Documentation vivante et suivi de projet (Brain OS)
<!-- Appuie C5, C27, C4. DEMI-PAGE. Cadrer STRICTEMENT méthode/outillage : le corpus taskforce-docs
comme source unique de vérité, tenue à jour en temps réel avec le code (docs-as-code), qui a servi de
base de connaissances et de suivi de projet. NE PAS déborder vers la vision produit "AI Delivery OS".
C'est le "comment j'ai gardé la maîtrise" du récit. Preuve : le corpus lui-même. -->
_À rédiger._

#### 2.5 Veille technologique et influence sur les décisions
<!-- Critères : C12 [E10]. Sources : Veille_Technologique (VT-001 à 006 avec ADR + preuves). Relier chaque veille à une décision réelle. -->
_À rédiger._

---

## Partie II — Concevoir : des choix aux modèles

<!-- Mouvement 2 : ce qui existait, pourquoi ces choix, de l'idée au modèle. -->

### 3. Choix technologiques et arbitrages

#### 3.1 Démarche de choix et contraintes
<!-- Contexte : contraintes CDC, délais, compétences, cible. Sources : Journal_Decisions_ADR, CdCT_v2. -->
_À rédiger._

#### 3.2 Étude comparative back-end et choix retenu
<!-- [TABLEAU : back-end] Java/Spring vs Node vs Symfony. Argument : robustesse, typage, écosystème, moteur métier. Source : ADR-001. -->
_À rédiger._

#### 3.3 Étude comparative front-end et choix retenu
<!-- [TABLEAU : front-end] Next.js/React vs Vue. SSR, App Router, écosystème. -->
_À rédiger._

#### 3.4 Base de données et choix retenu
<!-- [TABLEAU : BDD] PostgreSQL (+ pgvector) vs MySQL. Intégrité, extensions, vecteurs pour le Brain OS. -->
_À rédiger._

#### 3.5 L'écart au cahier des charges : un choix assumé
<!-- Critères : C2 [E3]. THÈME CENTRAL. Ne PAS s'excuser, argumenter techniquement. Ne pas bâtir la défense sur le seul "c'était des exemples". -->

##### 3.5.1 Ce que le cahier des charges demande
<!-- Back PHP-Symfony ou Node ; front React ou Vue ; BDD MySQL ou PostgreSQL. -->
_À rédiger._

##### 3.5.2 Ce que j'ai choisi et pourquoi
<!-- Java/Spring pour le moteur métier et la robustesse ; Next.js ; PostgreSQL. -->
_À rédiger._

##### 3.5.3 Conformité réelle et écart maîtrisé
<!-- React et PostgreSQL sont conformes ; seul le back diverge, par choix argumenté. -->
_À rédiger._

### 4. Conception et modélisation

#### 4.1 Wireframes et parcours
<!-- Critères : C6 [E7]. Sources : Wireframes_Annotes (48 routes). NE PAS utiliser les PNG assets/maquettes (brandés TaskFlow AI). Wireframes TaskForce ou captures réelles. -->
_À rédiger._

#### 4.2 Du besoin au dossier de conception et cas d'usage
<!-- Critères : C7 [E8]. Sources : Dossier_Conception, STB, Diagramme_Cas_Usage_UML (3 acteurs RBAC). -->
_À rédiger._

#### 4.3 Modélisation UML : classes, séquences, états
<!-- Critères : C8 [E8]. Sources : Diagramme_Classes_UML (38 entités), Diagrammes_Sequence_UML (6 parcours), Diagramme_Etats_UML. [FIGURE : classes] [FIGURE : séquence smart-assign]. -->
_À rédiger._

#### 4.4 Modèle de données MCD/MLD et persistance
<!-- Critères : C8, C9 [E8]. Sources : Modele_Donnees_MCD_MLD (MERISE), Dictionnaire_Donnees (50 tables/94 FK), migrations Flyway. [FIGURE : MCD]. -->
_À rédiger._

#### 4.5 Architecture logicielle : C4, modules, multi-tenant
<!-- Critères : C10 [E8]. Sources : Architecture_C4, Modules (shared/core/modules), Journal_Decisions_ADR. [FIGURE : C4 conteneurs]. -->
_À rédiger._

---

## Partie III — Construire le produit

<!-- Mouvement 3 : ce que j'ai construit. Les deux blocs démontrés en soutenance. -->

### 5. Développement du front-end

#### 5.1 Interface et charte graphique
<!-- Critères : C13, C14 [E11]. Sources : Design_System (tokens light/dark, Inter/SF Pro, shadcn/Radix, Lucide), globals.css. -->
_À rédiger._

#### 5.2 UX, parcours et accessibilité
<!-- Critères : C15 [E11]. WCAG 2.1 AA : 0 violation axe-core sur 3 pages (22/07), test durci de "critical" à "serious". Sources : Accessibilite (à étoffer), Bloc2. -->
_À rédiger._

#### 5.3 Qualité, sécurité et écoconception du code front
<!-- Critères : C16 [E11]. ESLint, TypeScript strict, CSP/CORS/HSTS, validation Zod câblée (login+register). Renvoi sécu ch. 7. -->
_À rédiger._

#### 5.4 Consommation sécurisée de l'API
<!-- Critères : C17 [E12]. client.ts (Axios + JWT + refresh), STOMP authentifié. Jetons en localStorage (le dire), pas HttpOnly. -->
_À rédiger._

#### 5.5 Tests du front-end
<!-- Critères : C18 [E13] seuil ≥ 50 %. -->

##### 5.5.1 Périmètre et méthode
<!-- Vitest sur la logique (lib/hooks/components/auth), Playwright sur les routes/présentation. -->
_À rédiger._

##### 5.5.2 Résultats et couverture
<!-- ~92 % lignes (périmètre logique), ~781 tests. Re-mesurer avant rendu, une seule valeur datée. -->
_À rédiger._

##### 5.5.3 Réserve assumée sur le périmètre
<!-- Le chiffre EXCLUT 48 routes + composants de présentation (couverts par Playwright). Le dire soi-même. -->
_À rédiger._

#### 5.6 Industrialisation du front
<!-- Critères : C19 [E14]. frontend-tests.yml, e2e-tests.yml, Dependabot. -->
_À rédiger._

#### 5.7 Performances et SEO
<!-- Critères : C20 seuil ≥ 70 %. SEO 92 % accueil, 100 % sur 4 autres pages (Lighthouse). PRÉCISER : mesure sur le site vitrine, pas l'app. -->
_À rédiger._

### 6. Développement du back-end

#### 6.1 Persistance et sécurité en profondeur
<!-- Critères : C21 [E15]. WorkspaceAccessInterceptor, AuditableEntity, EncryptedStringConverter (AES-256-GCM). -->
_À rédiger._

#### 6.2 Qualité, sécurité et écoconception du code back
<!-- Critères : C22 [E16]. shared/core/modules, Virtual Threads Java 21. Scans Trivy/Semgrep manuels, hors CI (le dire). -->
_À rédiger._

#### 6.3 Paiement et monétisation
<!-- Critères : C23 [E17]. Stripe Checkout, 5 webhooks (signature, idempotence stripe_event_id UNIQUE), portail, anti-rétrogradation Business/Basic. Reste : test avec de vrais événements Stripe. -->
_À rédiger._

#### 6.4 API REST sécurisée
<!-- Critères : C24 [E18]. Keycloak OIDC RS256 (password grant, PAS Authorization Code), @Valid DTOs, OpenAPI/Swagger. Renvoi OWASP ch. 7. -->
_À rédiger._

#### 6.5 Le moteur IA et le smart-assign
<!-- Illustration du cas d'usage (demande explicite). Le "ce que ça change" du produit. Source : 02-produit/IA. -->

##### 6.5.1 Le problème d'affectation
<!-- Affecter la bonne tâche à la bonne personne : surcharge, compétences, historique. -->
_À rédiger._

##### 6.5.2 Le pré-filtre et le scoring
<!-- Pré-filtre Java (charge, disponibilité) puis score sémantique via JSON du LLM Groq (PAS pgvector). Pondérations. -->
_À rédiger._

##### 6.5.3 Repli et garde-fous
<!-- Repli déterministe si le LLM échoue, quotas tokens, supervision humaine. -->
_À rédiger._

#### 6.6 Tests du back-end
<!-- Critères : C25 [E19] seuil ≥ 50 %. 73,71 % JaCoCo (~75-78 % au 16/08), ~670-792 tests, vrai PostgreSQL voisin (PAS Testcontainers). Re-mesurer avant rendu. -->
_À rédiger._

#### 6.7 Industrialisation du back
<!-- Critères : C26 [E20]. backend-tests.yml (Postgres pgvector en CI), release.yml, images GHCR. NUANCE : gate JaCoCo 0,70 (verify) et scans sécu hors CI. -->
_À rédiger._

---

## Partie IV — Sécuriser, industrialiser et prendre du recul

<!-- Mouvement 4 : la confiance, la mise en état de marche, et ce que ça change. Referme l'arc. -->

### 7. Sécurité et conformité RGPD

#### 7.1 Posture de sécurité
<!-- Appuie C16, C21, C24. Sources : Rapport_Securite, PSSI, Threat_Model_STRIDE, Chiffrement_Au_Repos. OWASP : vérifier la couverture réelle (corpus : partielle) avant d'affirmer "complet". -->
_À rédiger._

#### 7.2 RGPD de TaskForce
<!-- Critères : C11 (capacité) [E9]. Sources : Registre_Traitements_RGPD (Art.30), DPIA, Procedure_Violation_Donnees, Audit_RGPD_Conformite, Politique_Confidentialite_CGU. Gaps réels : bannière cookies interactive, mentions légales LEN, double opt-in à vérifier. -->
_À rédiger._

#### 7.3 Le cas RGPD externe
<!-- Critères : C11 [E9]. Le référentiel exige l'audit d'un site marchand tiers FOURNI par l'école (non transmis). Capacité démontrée sur TaskForce, livrable externe en attente. Ne pas cocher les 4 sous-critères sur TaskForce. -->
_À rédiger._

### 8. Industrialisation, déploiement et supervision

#### 8.1 Documentation technique et base de connaissances
<!-- Critères : C27 [E29]. OpenAPI auto-généré, Release_Notes, versioning. Lien avec 2.4 (Brain OS). -->
_À rédiger._

#### 8.2 Intégration continue et déploiement automatisé
<!-- Critères : C31 [E24]. 7 workflows GitHub Actions, images GHCR versionnées. Source : Pipeline_CICD. -->
_À rédiger._

#### 8.3 Hébergement et production
<!-- Critères : C28, C29, C30 [E21-E23]. HONNÊTE : rien n'est déployé. docker-compose.prod (9 services) et nginx.conf.example prêts mais jamais exécutés en prod. IA déployable via Groq hébergé. Sources : Strategie_Hebergement, Diagramme_Deploiement, Plan_Deploiement_2VM. -->
_À rédiger._

#### 8.4 Supervision, journalisation, observabilité
<!-- Critères : C32 [E25-E28]. OTel vers SigNoz, 9 alertes Prometheus, AuditLog (7 events), backup.ps1 (PCA/PRA testé). Sources : Observabilite, PS_PCA_PRA. -->
_À rédiger._

### 9. Distance critique et perspectives

#### 9.1 Innovations
<!-- Smart-assign, observabilité sécurité, Brain OS (DEMI-PAGE, cadré métier). Source : Note_Innovation_Distance_Critique. -->
_À rédiger._

#### 9.2 Limites assumées et dette technique
<!-- Dire les limites en premier : périmètre couverture front, gate + scans hors CI, pas de prod, cas RGPD externe, OWASP à confirmer. Sources : Dette_Technique, Problemes_Connus. -->
_À rédiger._

#### 9.3 Préconisations et évolutions
<!-- Préconisations concrètes + cap v2 (une page). Source : road_to_v2 (sobre, hors périmètre référentiel). -->
_À rédiger._

---

## Conclusion

<!-- UNE PAGE MAX, 400 à 450 mots. Referme l'arc : la transformation obtenue, ce que le projet démontre,
ouverture mesurée. Pas de techno nouvelle ici. -->

_À rédiger._

---

## Annexes

<!-- Hors décompte des pages. Portent le volume. -->

- A. **(Filet de sécurité, optionnel)** Correspondance compétences C1-C26 vers sections. <!-- À garder si le jury peut lire la structure comme non strictement alignée sur les blocs ; sinon supprimable. -->
- B. Extraits de code commentés. <!-- multi-tenant, webhook Stripe idempotent, scoring smart-assign, validation @Valid, migration versionnée, header sécurité. -->
- C. Schémas : C4, MCD/MLD, séquences, déploiement.
- D. Captures d'écran de l'application.
- E. Bibliographie.
- F. Présentation de synthèse (diapositives) au format PDF.
