<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# CdCF – Cahier des Charges Fonctionnel

**Version :** 1.1  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: CdCF](https://img.shields.io/badge/Type-CdCF-green?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Business & Analyse de marché](./Etude_business.md)
- [Stratégie Marketing & Commerciale](./Strategie_Marketing.md)
- [Repository GitHub](https://github.com/...)

**Tags :** `#cdcf` `#fonctionnel` `#use-cases` `#specifications` `#erp` `#saas`

<div class="section-intro">

## Sommaire

1. [Introduction et contexte](#1-introduction-et-contexte)
2. [Expression du besoin](#2-expression-du-besoin)
3. [Analyse fonctionnelle](#3-analyse-fonctionnelle)
4. [Acteurs et permissions](#4-acteurs-et-permissions)
5. [Cas d'usage fonctionnels](#5-cas-dusage-fonctionnels)
6. [Scénarios utilisateurs](#6-scénarios-utilisateurs)
7. [Modélisation UML](#7-modélisation-uml)
8. [Exigences non fonctionnelles](#8-exigences-non-fonctionnelles)
9. [Contraintes et limites](#9-contraintes-et-limites)
10. [Wireframes et maquettes](#10-wireframes-et-maquettes)

</div>

<div class="section-main">

## 1. Introduction et contexte

### Objet du document

Ce Cahier des Charges Fonctionnel (CdCF) définit l'ensemble des besoins fonctionnels de la plateforme Taskforce, un ERP modulaire SaaS destiné à optimiser la gestion de projets et l'assignation automatique des tâches. Le document s'adresse aux parties prenantes projet (MOA, MOE, développeurs) et constitue la référence fonctionnelle pour le développement et la validation de l'application.

### Périmètre fonctionnel

Le périmètre couvre le Core applicatif comportant l'authentification multi-tenant, la gestion des organisations et utilisateurs, ainsi que le système de gestion des abonnements. Le module métier principal intègre la gestion complète de projets et tâches, le système de compétences, l'algorithme d'assignation automatique, le suivi de charge de travail et le système d'alertes. Les modules optionnels futurs (LIMS, Qualité, GED) sont anticipés dans l'architecture mais ne font pas partie du MVP. Les aspects techniques détaillés (technologies, architecture, infrastructure) sont traités dans le [CdCT](./03_CdCT.md).

### Références documentaires

Ce document s'inscrit dans l'écosystème documentaire projet comprenant le [Dossier Projet](./Dossier_Projet.md) pour la vision globale et le pilotage, le [CdCT](./03_CdCT.md) pour les spécifications techniques détaillées, et l'[Étude Business](./Etude_business.md) pour le modèle économique et l'analyse de marché. Les normes de référence incluent RGPD pour la protection des données, WCAG 2.1 niveau AA pour l'accessibilité, et OWASP Top 10 pour la sécurité.

### Glossaire métier

**Core applicatif** : Socle technique réutilisable fournissant l'infrastructure de base (authentification, multi-tenant, sécurité, API générique).

**Module métier** : Ensemble cohérent de fonctionnalités répondant à un besoin métier spécifique (ex: module Gestion de Projet).

**Module optionnel** : Extension activable dynamiquement par organisation pour ajouter des fonctionnalités spécialisées (ex: LIMS, Qualité).

**Assignation automatique** : Algorithme qui attribue intelligemment les tâches aux collaborateurs selon leurs compétences, disponibilités et charge de travail.

**Multi-tenant** : Architecture permettant d'isoler complètement les données de chaque organisation cliente sur une infrastructure technique partagée.

**Plan tarifaire** : Niveau d'abonnement définissant les fonctionnalités accessibles et les limitations (Gratuit, Pro, Enterprise).

</div>

<div class="section-needs">

## 2. Expression du besoin

### Contexte métier et problématique

Les entreprises modernes font face à une complexité croissante dans la coordination des équipes et l'allocation des ressources. La répartition manuelle des tâches génère des déséquilibres de charge, des pertes de productivité et une démotivation des collaborateurs. Les managers manquent de visibilité globale sur les compétences disponibles et la charge réelle des équipes, conduisant à des décisions d'affectation sous-optimales. Les collaborateurs subissent des situations de surcharge sans possibilité d'anticipation ni de réajustement.

### Objectifs fonctionnels

L'application vise à transformer la gestion quotidienne des tâches en automatisant l'assignation selon des critères objectifs (compétences, charge, priorités), en offrant une visibilité temps réel sur la charge de travail individuelle et collective, en détectant proactivement les situations de surcharge avec alertes et possibilité de réajustement, en optimisant l'utilisation des ressources humaines par une répartition équitable, et en fournissant une interface collaborative pour le suivi d'avancement partagé.

### Bénéfices attendus

Pour les managers, l'application apporte un gain de temps significatif dans l'affectation des tâches, une aide à la décision basée sur des données objectives, une meilleure visibilité sur les capacités réelles des équipes, et une réduction des conflits liés à la répartition. Les collaborateurs bénéficient d'une répartition plus équitable de la charge, d'une transparence sur les critères d'assignation, d'une meilleure visibilité sur leurs tâches et priorités, et d'une réduction des situations de surcharge non anticipées. L'organisation gagne en productivité globale par une meilleure allocation des ressources, en satisfaction des équipes via une charge mieux répartie, et en agilité par une capacité de réajustement rapide.

### Parties prenantes

Les parties prenantes sont détaillées dans le [Dossier Projet - Section 11](./Dossier_Projet.md) incluant la MOA (porteur de projet), la MOE (équipe technique), les utilisateurs finaux (managers, collaborateurs, administrateurs), les partenaires techniques (Keycloak, Stripe, GitHub), et les parties prenantes académiques (jury, tuteur).

### Positionnement produit

La plateforme se positionne comme un ERP modulaire SaaS combinant un Core robuste avec des modules métier extensibles. L'approche diffère des outils de gestion de projet classiques (Jira, Asana) par l'assignation automatique intelligente et l'architecture modulaire permettant l'ajout de modules conformes à des normes sectorielles (21 CFR Part 11 pour pharma, LIMS pour laboratoires). Le modèle SaaS multi-tenant avec plans tarifaires différenciés (Gratuit, Pro, Enterprise) assure l'accessibilité aux TPE/PME tout en permettant une montée en gamme pour les grandes entreprises.

</div>

<div class="section-functional">

## 3. Analyse fonctionnelle

### Architecture fonctionnelle générale

L'architecture fonctionnelle se structure en trois niveaux. Le **Core applicatif** fournit les services transverses incluant l'authentification et gestion des identités via Keycloak (SSO, RBAC), l'infrastructure multi-tenant avec isolation complète des données par organisation, la gestion des utilisateurs et permissions avec profils configurables, le système de gestion d'abonnements intégré à Stripe (plans, facturation, webhooks), et l'API REST générique servant de fondation aux modules métier.

Le **Module Gestion de Projet** constitue le cœur métier avec la gestion complète de projets (création, planification, statuts, jalons), la gestion de tâches (CRUD, affectation, priorisation, dépendances), le système de compétences (référentiel, niveaux de maîtrise, profils utilisateurs), l'algorithme d'assignation automatique prenant en compte compétences requises, charge actuelle, disponibilités et priorités, le suivi de charge de travail (calcul automatique, visualisations, historiques), le système d'alertes (détection surcharge, notifications configurables, propositions de réajustement), et le reporting avec tableaux de bord personnalisables.

Les **Modules optionnels** anticipés comprennent le module LIMS pour la gestion de laboratoires réglementés, le module Qualité pour les processus ISO et audits, et le module GED pour la gestion documentaire avancée. Ces modules s'intègrent via une interface standardisée permettant activation/désactivation dynamique par organisation et isolation stricte des données métier.

### Fonctions principales

#### Gestion des projets

La gestion de projets permet de créer et configurer des projets avec informations descriptives (nom, description, dates, budget), de définir les jalons et livrables avec dates cibles, d'assigner des équipes et responsables, de suivre l'avancement global avec calcul automatique basé sur les tâches, et de clôturer ou archiver les projets terminés. Les projets peuvent être organisés par organisation cliente dans le contexte multi-tenant.

#### Gestion des tâches

La gestion des tâches offre la création avec informations détaillées (titre, description, priorité, estimation), la définition des compétences requises via sélection dans le référentiel, l'affectation manuelle ou automatique selon disponibilité et compétences, le suivi des statuts (Brouillon, En attente, En cours, Terminée, Archivée), la gestion des dépendances entre tâches, et la modification ou suppression avec traçabilité.

#### Gestion des compétences

Le système de compétences maintient un référentiel de compétences organisé par domaines et catégories, définit des niveaux de maîtrise (Débutant, Intermédiaire, Confirmé, Expert), associe les compétences aux profils utilisateurs avec niveaux appropriés, permet la recherche de collaborateurs par compétence, et fait évoluer les profils dans le temps avec historique.

#### Assignation automatique des tâches

L'assignation automatique constitue la fonctionnalité innovante centrale de Taskforce. L'algorithme analyse multiples critères pour proposer le collaborateur le plus pertinent pour chaque tâche, optimisant à la fois la qualité du travail et l'équilibre de charge de l'équipe.

**Critères d'évaluation**

L'algorithme évalue chaque collaborateur candidat selon plusieurs dimensions :

**Adéquation des compétences (40% du score)** : Le système compare les compétences requises par la tâche avec celles détenues par le collaborateur en prenant en compte le niveau de maîtrise. Pour une tâche nécessitant "Java niveau Confirmé", un collaborateur Expert Java obtiendra un score de 100%, un Confirmé 90%, un Intermédiaire 60%, et un Débutant 30%. Si plusieurs compétences sont requises, le score global est la moyenne pondérée des scores individuels. Un collaborateur sans la compétence requise est éliminé d'office sauf si le manager a activé l'option "formation" permettant d'assigner des tâches légèrement au-dessus du niveau pour faire progresser les juniors.

**Charge de travail actuelle (30% du score)** : Le système calcule la charge en cours du collaborateur basée sur l'estimation totale des tâches assignées non terminées. Un collaborateur à 40% de sa capacité maximale obtiendra un meilleur score qu'un collaborateur à 80%. La formule appliquée est : `score_charge = 100 - (charge_actuelle / capacité_max * 100)`. Par exemple, si un collaborateur a 24h de tâches en cours sur une capacité de 40h/semaine, son score de charge sera de 40%. Les collaborateurs déjà en surcharge (>90%) sont automatiquement exclus sauf si toute l'équipe est en surcharge (le manager reçoit alors une alerte systématique).

**Disponibilité et absences (15% du score)** : Le calendrier des absences planifiées (congés, formations, arrêts maladie déclarés) est vérifié. Si un collaborateur est absent pendant la période prévue de réalisation de la tâche (calculée à partir de la date de début souhaitée et de l'estimation), son score de disponibilité diminue proportionnellement. Une absence couvrant 50% de la période réduit le score de moitié. Les collaborateurs totalement absents sur toute la période sont exclus.

**Historique de performance (10% du score)** : Le système mémorise les performances passées du collaborateur sur des tâches similaires (même domaine de compétence, même niveau de complexité). Le taux de respect des délais, la qualité perçue (via feedback informel du manager), et le nombre de tâches similaires réussies influencent ce score. Un collaborateur ayant réalisé avec succès 8 tâches Java sur 10 dans les délais obtiendra un meilleur score historique qu'un collaborateur n'ayant réalisé que 2 tâches ou ayant un taux de retard élevé.

**Préférences et affinités (5% du score)** : Les managers peuvent définir des préférences d'affectation (certains binômes fonctionnent mieux ensemble, certains collaborateurs préfèrent certains types de tâches). Ces préférences sont optionnelles et ajustent légèrement le score final. Un collaborateur "préféré" pour un type de tâche gagne un bonus de 5 à 10 points.

**Calcul du score global**

Le score final de pertinence pour chaque candidat est calculé selon la formule pondérée :

```
Score_final = (Score_compétences × 0.40)
            + (Score_charge × 0.30)
            + (Score_disponibilité × 0.15)
            + (Score_historique × 0.10)
            + (Score_préférences × 0.05)
```

Les candidats sont ensuite classés du score le plus élevé au plus faible. Le système propose par défaut les 3 meilleurs candidats au manager avec leur score détaillé et la répartition par critère pour transparence de la décision.

**Paramètres configurables**

Les administrateurs et managers peuvent ajuster plusieurs paramètres organisationnels :

- **Pondérations des critères** : Modifier les poids de chaque critère (ex: privilégier la charge équilibrée sur l'expertise pour favoriser le développement des juniors)
- **Seuil de surcharge** : Définir à quel pourcentage de capacité un collaborateur est considéré en surcharge (par défaut 90%)
- **Mode d'assignation** : Automatique complet (le système assigne au meilleur candidat sans validation), Semi-automatique (proposition à valider par défaut), ou Manuel (désactivation de l'algorithme)
- **Activation du mode formation** : Permettre ou non les assignations "stretch" à des collaborateurs légèrement sous-qualifiés pour les faire progresser
- **Prise en compte géographique** : Si équipes distribuées, intégrer la proximité géographique ou le fuseau horaire comme critère additionnel

**Cas particuliers et règles métier**

L'algorithme gère plusieurs situations spécifiques :

- **Aucun candidat éligible** : Si aucun collaborateur ne possède les compétences requises, le système le signale au manager avec suggestion de modifier les critères, reporter la tâche, ou recruter/former
- **Égalité de scores** : En cas d'égalité stricte entre candidats, le système privilégie le collaborateur ayant le moins de tâches assignées en absolu, puis celui ayant le plus d'ancienneté dans l'équipe
- **Urgence de la tâche** : Les tâches marquées "CRITIQUE" reçoivent un traitement prioritaire avec augmentation automatique du poids du critère "disponibilité immédiate"
- **Dépendances entre tâches** : Si une tâche B dépend d'une tâche A en cours, le système privilégie d'assigner B au même collaborateur que A pour cohérence (bonus de 10 points si activation de l'option "continuité")
- **Rééquilibrage périodique** : Un job automatique hebdomadaire analyse la répartition globale de charge et suggère des réaffectations si déséquilibres importants détectés

**Validation et apprentissage**

Après assignation, le système trace les décisions prises et collecte des métriques de performance réelle (délai respecté, qualité, feedback). Ces données alimentent le score historique pour affiner progressivement les recommandations futures. Les managers peuvent également signaler des assignations particulièrement réussies ou problématiques pour ajuster les pondérations automatiquement via machine learning (feature plannifiée post-MVP).

La validation finale reste toujours entre les mains du manager qui peut accepter la proposition, choisir un autre candidat dans la liste, ou assigner manuellement n'importe quel membre de l'équipe. L'algorithme est un assistant intelligent, pas un décideur autonome.

#### Suivi de la charge de travail

Le suivi de charge calcule automatiquement la charge individuelle basée sur les estimations de tâches assignées, agrège la charge au niveau équipe et organisation, visualise la répartition via graphiques et indicateurs, compare la charge aux capacités disponibles, et historise l'évolution pour analyses tendancielles. Les seuils de surcharge sont configurables par organisation.

#### Alertes et notifications

Le système d'alertes détecte automatiquement les situations de surcharge (individuelle ou collective), notifie les managers et collaborateurs concernés via email et notifications in-app, propose des actions de réajustement (réaffectation, report, escalade), permet la configuration des seuils et canaux de notification, et assure la traçabilité des alertes et actions prises.

### Fonctions secondaires

#### Tableau de bord et reporting

Les tableaux de bord proposent des vues personnalisables par rôle (manager, collaborateur, administrateur), des indicateurs clés (taux d'avancement, charge moyenne, surcharges), des graphiques d'évolution (charge dans le temps, vélocité équipe), des rapports exportables (PDF, Excel), et un historique pour analyses comparatives.

#### Gestion des équipes et organisations

La gestion permet de créer et structurer des organisations (clients multi-tenant), de définir des équipes au sein de chaque organisation, d'assigner des utilisateurs aux équipes, de configurer les paramètres organisationnels (seuils, préférences), et d'isoler strictement les données entre organisations.

#### Gestion des utilisateurs et rôles

La gestion utilisateurs offre la création de comptes avec informations de profil, l'attribution de rôles (Collaborateur, Manager, Administrateur) avec permissions associées, la gestion des droits d'accès granulaires basés sur RBAC, la désactivation ou suppression de comptes avec respect du RGPD, et l'export des données personnelles (portabilité RGPD).

#### Gestion des abonnements et plans

La gestion d'abonnements intègre trois plans tarifaires (Gratuit limité à 5 utilisateurs et 3 projets, Pro illimité avec 2 modules optionnels, Enterprise sur devis avec tous modules), le processus de souscription et paiement via Stripe, l'application automatique des limitations par plan, le passage d'un plan à un autre avec proratisation, et la gestion de la facturation avec historique.

> **Note** : Les détails complets des plans tarifaires (grille de prix, comparatif détaillé des fonctionnalités par plan, stratégie de pricing, positionnement concurrentiel) sont traités dans le document [**Stratégie Marketing & Commerciale**](./Strategie_Marketing.md) dédié. Le présent CdCF se concentre sur les aspects fonctionnels de la gestion des abonnements.

#### Import / Export de données

Les fonctions d'import/export permettent l'import de données depuis fichiers CSV/Excel (utilisateurs, projets, tâches), l'export des données au format CSV/Excel/PDF, l'import/export respectant les structures de données et validations, et la gestion des erreurs avec rapports détaillés.

### Fonctions de support

#### Authentification et autorisation

Le système d'authentification via Keycloak offre un SSO (Single Sign-On) pour une expérience unifiée, l'authentification OAuth2/OIDC, la gestion des sessions sécurisées, l'authentification forte optionnelle (2FA), les autorisations basées sur RBAC avec vérification à chaque requête, et la traçabilité des connexions et actions sensibles.

#### Gestion des préférences utilisateur

Les préférences incluent la langue d'interface (français, anglais), le fuseau horaire et format de date, les notifications (canaux, fréquence), le thème de l'interface (clair, sombre), et la personnalisation des tableaux de bord.

#### Aide contextuelle et documentation

L'aide propose une documentation en ligne accessible depuis l'application, des tooltips et guides contextuels, des tutoriels vidéo pour les fonctionnalités clés, une base de connaissances (FAQ), et un support par email selon le plan.

#### Accessibilité

L'accessibilité respecte WCAG 2.1 niveau AA avec navigation complète au clavier, support des lecteurs d'écran (attributs ARIA), contrastes de couleurs conformes, tailles de texte ajustables, et tests automatisés via axe-core. Le RGAA complète ces exigences pour le contexte français.

</div>

<div class="section-actors">

## 4. Acteurs et permissions

### Typologie des utilisateurs

**Collaborateur / Membre d'équipe** : Utilisateur standard qui consulte ses tâches assignées, met à jour le statut de ses tâches, consulte sa charge de travail personnelle, et gère son profil de compétences. Il dispose d'une visibilité limitée à ses propres tâches et à sa charge.

**Manager / Chef de projet** : Responsable d'équipe ou de projet qui crée et gère des projets, crée et affecte des tâches (manuellement ou via assignation automatique), consulte la charge de travail de son équipe, configure les alertes de surcharge, génère des rapports d'avancement, et gère les compétences des membres de son équipe. Il a une visibilité étendue sur les projets et équipes sous sa responsabilité.

**Administrateur système** : Responsable de la configuration et de l'administration de l'organisation qui gère les utilisateurs et leurs rôles, configure les équipes et organisations, gère les abonnements et modules optionnels, configure les paramètres globaux (seuils, préférences), accède aux logs et audits système, et assure le support de premier niveau. Il dispose d'une visibilité complète sur l'organisation dont il a la charge.

**Invité / Utilisateur externe** : Utilisateur occasionnel avec accès limité (consultation uniquement) sur des projets ou tâches spécifiques, sans possibilité de modification. Ce rôle permet d'ouvrir l'accès à des parties prenantes externes (clients, prestataires) de façon contrôlée.

### Matrice acteurs / fonctionnalités

La matrice complète des permissions par rôle est disponible dans la [documentation technique du projet](./03_CdCT.md). En synthèse, les **Collaborateurs** disposent de droits de lecture sur leurs propres ressources et de mise à jour limitée, les **Managers** bénéficient de droits étendus de création et modification sur les projets et équipes sous leur responsabilité, les **Administrateurs** ont accès complet à toutes les fonctionnalités d'administration, et les **Invités** sont limités à la consultation selon les permissions spécifiques accordées.

### Contrôle d'accès

Le contrôle d'accès s'appuie sur un modèle RBAC (Role-Based Access Control) géré par Keycloak avec vérification des permissions à chaque requête API, isolation multi-tenant garantissant que chaque organisation accède uniquement à ses données, traçabilité complète des accès et modifications via audit logs, et gestion fine des permissions au niveau ressource (projet, tâche, équipe). Les détails d'implémentation technique sont décrits dans le [CdCT - Section Sécurité](./03_CdCT.md).

</div>

<div class="section-usecases">

## 5. Cas d'usage fonctionnels

### UC01 : Créer un projet

**Acteur** : Manager  
**Préconditions** : Utilisateur authentifié avec rôle Manager, plan tarifaire autorisant la création de projets  
**Description** : Le manager accède à l'interface de création de projet, saisit les informations (nom, description, dates, budget), sélectionne l'équipe assignée, définit les jalons si nécessaire, valide la création. Le système enregistre le projet et notifie l'équipe.  
**Postconditions** : Projet créé et accessible aux membres de l'équipe

### UC02 : Créer une tâche

**Acteur** : Manager  
**Préconditions** : Projet existant, utilisateur authentifié avec droits appropriés  
**Description** : Le manager accède au projet, crée une nouvelle tâche avec titre, description, priorité et estimation, définit les compétences requises, et sauvegarde. La tâche est créée avec statut "En attente" et prête pour affectation.  
**Postconditions** : Tâche créée et visible dans le projet

### UC03 : Affecter manuellement une tâche

**Acteur** : Manager  
**Préconditions** : Tâche en attente d'affectation  
**Description** : Le manager sélectionne une tâche, choisit manuellement un collaborateur dans la liste des membres d'équipe, confirme l'affectation. Le système vérifie la disponibilité, met à jour la charge du collaborateur et notifie l'intéressé.  
**Postconditions** : Tâche affectée et collaborateur notifié

### UC04 : Déclencher l'assignation automatique

**Acteur** : Manager  
**Préconditions** : Tâche avec compétences requises définies  
**Description** : Le manager déclenche l'assignation automatique pour une ou plusieurs tâches. L'algorithme analyse les compétences requises, la charge actuelle des collaborateurs éligibles, leurs disponibilités, et propose une liste de candidats classés par pertinence. Le manager valide ou choisit manuellement parmi les propositions.  
**Postconditions** : Tâche(s) affectée(s) de façon optimale

### UC05 : Consulter la charge de travail

**Acteur** : Manager, Collaborateur  
**Préconditions** : Utilisateur authentifié  
**Description** : L'utilisateur accède à son tableau de bord charge de travail. Le système affiche la charge actuelle (individuelle pour le collaborateur, équipe complète pour le manager) avec visualisations graphiques, indicateurs de surcharge éventuelle, et détail par projet/tâche.  
**Postconditions** : Visibilité sur la répartition de la charge

### UC06 : Gérer les compétences d'un collaborateur

**Acteur** : Manager, Administrateur, et Collaborateur (auto-évaluation)
**Préconditions** : Utilisateur cible existant  
**Description** : Le manager accède au profil du collaborateur, consulte les compétences actuelles, ajoute de nouvelles compétences avec niveau de maîtrise, modifie les niveaux existants, ou retire des compétences obsolètes. Les modifications sont enregistrées avec historique.  
**Postconditions** : Profil de compétences mis à jour

### UC07 : Configurer les alertes de surcharge

**Acteur** : Manager, Administrateur  
**Préconditions** : Utilisateur avec droits de configuration  
**Description** : L'utilisateur accède aux paramètres d'alertes, définit les seuils de surcharge (en heures ou jours de travail), configure les canaux de notification (email, in-app), active ou désactive certaines alertes, et sauvegarde la configuration.  
**Postconditions** : Alertes configurées selon préférences

### UC08 : Générer un rapport d'avancement

**Acteur** : Manager  
**Préconditions** : Projet(s) avec tâches en cours  
**Description** : Le manager sélectionne le périmètre du rapport (projet, équipe, période), choisit les indicateurs à inclure (taux d'avancement, charge, vélocité), sélectionne le format (PDF, Excel), et génère le rapport. Le système compile les données et produit le document exportable.  
**Postconditions** : Rapport généré et téléchargeable

### UC09 : S'abonner à un plan

**Acteur** : Administrateur (nouveau client)  
**Préconditions** : Organisation créée (inscription initiale)  
**Description** : L'administrateur consulte les plans disponibles (Gratuit, Pro, Enterprise), sélectionne un plan, saisit les informations de paiement si plan payant (flux Stripe), confirme la souscription. Le système active le plan, applique les limitations/fonctionnalités associées, et envoie la confirmation avec facture.  
**Postconditions** : Abonnement actif avec fonctionnalités correspondantes

### UC10 : Gérer les modules optionnels

**Acteur** : Administrateur  
**Préconditions** : Plan tarifaire autorisant les modules optionnels (Pro ou Enterprise)  
**Description** : L'administrateur accède à la gestion des modules, consulte les modules disponibles (LIMS, Qualité, GED), active ou désactive un module pour son organisation. Le système met à jour la configuration et rend les fonctionnalités du module accessibles (ou les retire) immédiatement.  
**Postconditions** : Module activé/désactivé selon demande

### Autres cas d'usage

Les cas d'usage secondaires incluent la gestion des absences et disponibilités, l'export de données pour conformité RGPD, la gestion des dépendances entre tâches, la configuration des préférences utilisateur, et la consultation de l'aide contextuelle. Ces cas suivent des patterns similaires aux cas principaux décrits ci-dessus.

</div>

<div class="section-scenarios">

## 6. Scénarios utilisateurs

### Scénario 1 : Manager créant un projet et affectant des tâches

Marie, chef de projet marketing, se connecte à l'application Taskforce. Elle crée un nouveau projet "Lancement Produit X" avec une date de livraison fixée à fin mars. Elle définit trois jalons intermédiaires (Conception, Production, Lancement) et assigne son équipe de 5 collaborateurs. Marie crée ensuite une série de tâches : "Élaborer stratégie de lancement" (compétence Marketing Stratégique requise), "Créer visuels publicitaires" (compétence Design Graphique), et "Rédiger communiqués de presse" (compétence Rédaction). Pour chaque tâche, elle déclenche l'assignation automatique. Le système propose Jean pour la stratégie (expert en Marketing Stratégique, charge actuelle 60%), Sophie pour les visuels (confirmée en Design, charge 45%), et Luc pour les communiqués (expert Rédaction, charge 70%). Marie valide les propositions. Les trois collaborateurs reçoivent instantanément une notification avec détail de leur nouvelle tâche.

### Scénario 2 : Collaborateur consultant ses tâches et sa charge

Jean, collaborateur marketing, ouvre son tableau de bord Taskforce chaque matin. Il voit immédiatement ses 8 tâches en cours réparties sur 3 projets différents. La vue "Charge de travail" lui indique qu'il est actuellement à 75% de capacité avec 30 heures de travail estimées sur les 2 prochaines semaines. Il filtre par priorité et décide de commencer par la tâche "Élaborer stratégie de lancement" qui vient d'être assignée. Il clique sur la tâche, consulte les détails et la description fournie par Marie, met le statut à "En cours", et commence son travail. En fin de journée, il met à jour l'avancement à 30% complété.

### Scénario 3 : Détection et résolution d'une surcharge

Le mercredi matin, le système Taskforce détecte que Sophie, designer graphique, vient d'atteindre 95% de sa capacité suite à l'ajout d'une tâche urgente sur un autre projet. Une alerte est automatiquement envoyée à Marie, sa manager, avec le détail de la surcharge et une proposition de réajustement : réaffecter la tâche "Créer visuels publicitaires" à Thomas, designer junior ayant les compétences requises et actuellement à 50% de charge. Marie consulte l'alerte, vérifie le profil de Thomas (niveau Intermédiaire en Design Graphique, suffisant pour cette tâche), et accepte la réaffectation. Le système transfère la tâche, notifie Sophie du retrait et Thomas de la nouvelle assignation, recalcule les charges, et ferme l'alerte. L'équilibre de charge est restauré sans intervention manuelle complexe.

### Scénario 4 : Activation d'un module optionnel

LabTech, laboratoire pharmaceutique client de Taskforce, utilise actuellement le plan Enterprise pour gérer ses projets de R&D. Après 3 mois d'utilisation, l'administrateur système du laboratoire, Dr. Martin, souhaite activer le module LIMS pour gérer également les échantillons et analyses en conformité avec les normes réglementaires. Il se connecte en tant qu'administrateur, accède à la section "Modules" du menu de configuration, consulte la description du module LIMS (gestion d'échantillons, traçabilité complète, audit trails, conformité 21 CFR Part 11), et clique sur "Activer". Le système vérifie l'éligibilité (plan Enterprise valide), active le module instantanément, et affiche un message de confirmation. Un nouveau menu "LIMS" apparaît dans la navigation principale, donnant accès aux fonctionnalités spécialisées de gestion de laboratoire. Les équipes peuvent immédiatement commencer à enregistrer des échantillons et analyses tout en continuant à utiliser les fonctionnalités de gestion de projet standards.

### Scénario 5 : Passage d'un plan gratuit à un plan payant

StartupTech, jeune entreprise de 4 personnes, utilise Taskforce avec le plan Gratuit depuis 2 mois. L'équipe grandit et atteint 6 collaborateurs, dépassant la limite de 5 utilisateurs du plan gratuit. Sarah, la CEO, reçoit une notification l'informant de la limite atteinte et proposant de passer au plan Pro. Elle consulte les fonctionnalités supplémentaires du plan Pro (utilisateurs illimités, projets illimités, 2 modules optionnels, support prioritaire) et décide de souscrire. Sarah clique sur "Passer au plan Pro", est redirigée vers le formulaire de paiement Stripe, saisit les informations de carte bancaire de l'entreprise, et valide. Le système Stripe traite le paiement (29€/mois/utilisateur soit 174€/mois pour 6 utilisateurs), renvoie la confirmation via webhook, et Taskforce active immédiatement le plan Pro. Sarah peut ajouter les 6ème et 7ème collaborateurs sans limitation, créer des projets supplémentaires, et reçoit une facture par email. Le passage s'est effectué sans interruption de service et l'équipe peut continuer à travailler normalement avec les nouvelles capacités débloquées.

Je me permets ici de rappeler que le système devra aussi prendre en charge l'amélioration continue des employées (assigné une tâches plus dur à quelqu'un qui a un niveau de compétence plus bas pour le faire progresser) et la possibilité de faire du "shadowing" (un collaborateur junior peut suivre les tâches d'un collaborateur senior pour apprendre). Ces scénarios d'évolution des compétences et de mentorat sont essentiels pour la croissance professionnelle des employés et devraient être intégrés dans les fonctionnalités futures du système.

</div>

<div class="section-uml">

## 7. Modélisation UML

### Diagrammes de cas d'utilisation

Le diagramme de cas d'utilisation global identifie les acteurs principaux (Collaborateur, Manager, Administrateur, Système, Services Externes) et leurs interactions avec les fonctionnalités de la plateforme. Les cas d'utilisation sont organisés par domaine fonctionnel (Gestion Projets, Gestion Tâches, Gestion Compétences, Assignation, Reporting, Administration).

**[Diagramme à intégrer : Use Case Diagram global]**

### Diagrammes d'activité

Les diagrammes d'activité détaillent les processus métier clés, notamment le workflow d'assignation automatique de tâches (analyse des compétences → calcul de charge → vérification disponibilités → classement candidats → proposition → validation), le processus de détection et résolution de surcharge (monitoring charge → détection seuil → génération alerte → proposition réaffectation → validation → mise à jour), et le workflow de souscription à un plan (sélection plan → saisie paiement → appel Stripe → webhook confirmation → activation plan → application limitations).

**[Diagrammes à intégrer : Activity Diagrams pour processus clés]**

### Diagrammes de séquence

Les diagrammes de séquence illustrent les interactions entre composants pour des scénarios fonctionnels spécifiques, notamment l'authentification utilisateur via Keycloak (User → Frontend → Backend → Keycloak → Backend → Frontend → User), la création de tâche avec assignation automatique (Manager → Frontend → Backend → Assignation Service → Backend → Frontend → Manager), et le workflow de paiement Stripe (User → Frontend → Backend → Stripe → Webhook → Backend).

**[Diagrammes à intégrer : Sequence Diagrams pour scénarios clés]**

### Diagrammes de classes

Le diagramme de classes métier modélise les entités principales et leurs relations : Organisation (1) --- (N) Équipe (1) --- (N) Utilisateur (1) --- (N) Tâche, Projet (1) --- (N) Tâche, Tâche (N) --- (N) Compétence, Utilisateur (N) --- (N) Compétence (avec niveau de maîtrise), Abonnement (1) --- (1) Organisation, Module (N) --- (N) Organisation. Chaque classe comprend ses attributs et méthodes principales.

**[Diagramme à intégrer : Class Diagram métier]**

### Diagrammes d'états-transitions

Les diagrammes d'états modélisent l'évolution des entités clés. Une **Tâche** suit le cycle : Brouillon → En attente → En cours → Terminée → Archivée (avec possibilité de Suspendue). Un **Projet** évolue : Planification → Actif → En cours → Suspendu (optionnel) → Clôturé → Archivé. Un **Abonnement** passe par : Essai → Actif → Suspendu (impayé) → Résilié, avec possibilités de transitions entre plans (Gratuit ↔ Pro ↔ Enterprise).

**[Diagrammes à intégrer : State Diagrams pour entités principales]**

</div>

<div class="section-requirements">

## 8. Exigences non fonctionnelles

### Performance

L'application doit garantir des temps de réponse inférieurs à 2 secondes pour les opérations courantes (consultation de tâches, mise à jour de statut), inférieurs à 5 secondes pour les opérations complexes (génération de rapports, assignation automatique de multiples tâches), et supporter une charge de 100 utilisateurs simultanés en phase MVP avec scalabilité prévue à 1000+ utilisateurs.

La mesure de performance s'effectue selon plusieurs indicateurs. Le **temps de chargement initial** de la page d'accueil ne doit pas excéder 3 secondes sur connexion haut débit (4G/Fibre) et 5 secondes sur connexion mobile 3G. Les **opérations CRUD** (Create, Read, Update, Delete) sur les tâches et projets doivent s'exécuter en moins de 500ms au 95e percentile. L'**assignation automatique** pour un ensemble de 20 tâches avec analyse de 50 collaborateurs doit se terminer en moins de 3 secondes. La **génération de rapports** complexes agrégant jusqu'à 6 mois de données doit compléter en moins de 8 secondes.

La scalabilité anticipée repose sur une architecture stateless pour le backend permettant l'ajout de serveurs applicatifs horizontalement, un cache distribué pour réduire les accès base de données répétitifs, et une optimisation continue via monitoring des requêtes lentes (slow query log PostgreSQL > 1s).

### Disponibilité

Le système vise une disponibilité de 99% en phase MVP (soit moins de 7h de downtime par mois) et 99.9% en production stable (moins de 45 minutes de downtime par mois). Les maintenances planifiées sont effectuées en dehors des heures ouvrées avec préavis de 48h minimum.

### Sécurité

La sécurité s'appuie sur l'authentification forte via Keycloak avec support 2FA optionnel, le chiffrement des données en transit (TLS 1.3) et au repos (chiffrement base de données), la conformité OWASP Top 10 validée par tests automatisés, l'audit logging complet des actions sensibles, et la conformité RGPD avec mécanismes de consentement, droit à l'oubli et portabilité.

#### Protection contre les vulnérabilités OWASP Top 10

L'OWASP (Open Web Application Security Project) Top 10 identifie les risques de sécurité les plus critiques pour les applications web. Taskforce implémente des protections spécifiques contre chacune de ces menaces :

**1. Broken Access Control** : Le contrôle d'accès défaillant permettrait à un utilisateur d'accéder à des ressources non autorisées. Protection via vérification systématique des permissions à chaque requête API, isolation multi-tenant stricte (un utilisateur ne voit jamais les données d'une autre organisation), et tests automatisés de conformité des permissions.

**2. Cryptographic Failures** : Les échecs cryptographiques exposent les données sensibles. Protection via chiffrement TLS 1.3 pour toutes les communications, chiffrement at-rest de la base de données PostgreSQL, hashing sécurisé des mots de passe (bcrypt géré par Keycloak), et stockage des secrets hors du code (variables d'environnement).

**3. Injection** : Les attaques par injection (SQL, NoSQL, commandes OS) exploitent des entrées non validées. Protection via requêtes paramétrées exclusivement (JPA/JPQL), validation stricte de toutes les entrées utilisateur côté backend (Bean Validation), échappement automatique des sorties, et interdiction totale de SQL brut ou concaténation de requêtes.

**4. Insecure Design** : La conception non sécurisée introduit des failles architecturales. Protection via modélisation des menaces dès la conception, principe du moindre privilège (droits minimaux nécessaires), defense in depth (multiples couches de sécurité), et revue de code sécurité sur toutes les Pull Requests sensibles.

**5. Security Misconfiguration** : Les erreurs de configuration exposent des surfaces d'attaque. Protection via configuration durcie par défaut, désactivation des endpoints sensibles en production (Swagger UI, Spring Actuator non authentifié), secrets externalisés hors du code, et scans automatisés de configuration (OWASP ZAP dans CI/CD).

**6. Vulnerable and Outdated Components** : Les composants vulnérables introduisent des failles connues. Protection via Dependabot GitHub scannant automatiquement les CVE, mises à jour régulières des dépendances Maven et npm, monitoring des bulletins de sécurité des technologies utilisées (Spring Boot, Next.js, Keycloak), et remplacement proactif des bibliothèques abandonnées.

**7. Identification and Authentication Failures** : Les failles d'authentification permettent l'usurpation d'identité. Protection via délégation complète à Keycloak (solution éprouvée enterprise-grade), tokens JWT avec expiration courte (15 minutes), refresh tokens sécurisés, support 2FA optionnel (TOTP), et rate limiting sur les tentatives de connexion.

**8. Software and Data Integrity Failures** : Les échecs d'intégrité compromettent le code ou les données. Protection via signatures des artefacts Docker, vérification des checksums des dépendances, pipelines CI/CD sécurisés (secrets GitHub Actions), et webhooks Stripe signés cryptographiquement.

**9. Security Logging and Monitoring Failures** : L'absence de logs empêche la détection d'incidents. Protection via audit logging structuré de toutes les actions sensibles (connexion, modification permissions, suppression ressources), monitoring temps réel via Prometheus/Grafana, alertes automatiques sur comportements anormaux, et rétention des logs conforme RGPD (1 an minimum).

**10. Server-Side Request Forgery (SSRF)** : Les attaques SSRF exploitent le serveur pour accéder à des ressources internes. Protection via validation stricte des URLs externes, whitelist des domaines autorisés (Stripe, services cloud uniquement), interdiction d'accès aux IPs privées depuis le backend, et timeout courts sur les requêtes sortantes.

Les détails techniques d'implémentation sont décrits dans le [CdCT - Section Sécurité](./03_CdCT.md).

### Accessibilité

L'accessibilité respecte WCAG 2.1 niveau AA (Web Content Accessibility Guidelines) garantissant l'utilisabilité pour les personnes en situation de handicap. Le niveau AA représente le standard légal dans de nombreux pays et couvre les besoins de la majorité des utilisateurs.

#### Critères WCAG 2.1 niveau AA implémentés

**Perceptibilité** : Toute information est présentée de manière compréhensible par tous les sens. Les images importantes disposent d'alternatives textuelles descriptives (attribut alt), les vidéos incluent sous-titres et transcriptions, les contrastes de couleurs respectent le ratio minimum 4.5:1 pour le texte normal et 3:1 pour le texte large (18pt+), et aucune information n'est transmise uniquement par la couleur (icônes + texte combinés).

**Opérabilité** : L'interface est navigable et utilisable de multiples manières. La navigation complète au clavier est garantie avec ordre de tabulation logique (tabindex), focus visible permanent, absence de piège clavier, et raccourcis clavier documentés pour les actions fréquentes. Les formulaires incluent labels explicites associés aux champs, messages d'erreur clairs et suggestions de correction, et délais de saisie ajustables ou désactivables.

**Compréhensibilité** : Le contenu est lisible et prévisible. La langue de la page est déclarée (attribut lang), les termes techniques sont expliqués au premier usage, les formulaires incluent des hints contextuels, les messages d'erreur sont explicites ("Le champ email est invalide" plutôt que "Erreur champ 2"), et la navigation reste cohérente sur toutes les pages. Les changements de contexte surviennent uniquement sur action explicite de l'utilisateur (pas de redirections automatiques inattendues).

**Robustesse** : Le contenu est compatible avec les technologies d'assistance actuelles et futures. Le HTML sémantique est utilisé systématiquement (nav, main, article, aside), les attributs ARIA complètent quand nécessaire (role, aria-label, aria-live pour notifications dynamiques), et le code valide W3C garantit le rendu correct par les assistive technologies (NVDA, JAWS, VoiceOver, TalkBack).

#### RGAA et conformité française

Le RGAA (Référentiel Général d'Amélioration de l'Accessibilité) adapte WCAG au contexte réglementaire français. Une déclaration d'accessibilité publique documente le niveau de conformité actuel, les non-conformités identifiées, le calendrier de mise en conformité, et les moyens de contact pour signaler des problèmes. Des audits réguliers (automatisés via axe-core dans CI/CD et manuels semestriels) valident la conformité continue.

Les tests automatisés détectent environ 30% des problèmes d'accessibilité. Les 70% restants nécessitent tests manuels incluant navigation complète au clavier, test avec lecteur d'écran (NVDA sur Windows, VoiceOver sur macOS/iOS), vérification avec utilisateurs en situation de handicap, et validation par expert accessibilité externe pour certification.

### Compatibilité

L'application supporte les navigateurs modernes (Chrome, Firefox, Safari, Edge, versions N et N-1), fonctionne sur desktop, tablette et mobile (responsive design), et assure une compatibilité avec les lecteurs d'écran (NVDA, JAWS, VoiceOver).

### Maintenabilité

Le code respecte les standards de qualité avec couverture de tests supérieure à 70%, documentation technique à jour (code commenté, README, architecture), dette technique inférieure à 5% (mesurée via SonarQube), et architecture modulaire facilitant les évolutions sans régression.

### Conformité réglementaire

#### RGPD (Règlement Général sur la Protection des Données)

Le RGPD encadre le traitement des données personnelles des citoyens européens avec sanctions sévères en cas de non-conformité (jusqu'à 4% du chiffre d'affaires ou 20M€). Taskforce implémente les principes fondamentaux suivants :

**Licéité et transparence** : Les utilisateurs sont informés clairement des données collectées (email, nom, prénom, organisation, compétences, activité dans l'application), des finalités du traitement (fourniture du service ERP, assignation automatique, facturation via Stripe), et de la base légale (consentement + exécution du contrat). La politique de confidentialité accessible depuis toutes les pages détaille ces éléments en langage clair.

**Minimisation des données** : Seules les données strictement nécessaires au service sont collectées. Pas de collecte de données sensibles (origine ethnique, opinions politiques, santé, etc.) sauf cas spécifique modules futurs avec consentement explicite séparé. Les champs optionnels sont clairement marqués.

**Limitation de la conservation** : Les données des comptes actifs sont conservées pendant toute la durée du contrat. Suite à résiliation ou suppression de compte, les données sont anonymisées après 30 jours (délai légal) sauf obligations légales de conservation (factures conservées 10 ans pour obligations comptables, purgées des données personnelles non essentielles).

**Droits des personnes** : Les utilisateurs exercent leurs droits via l'interface applicative ou demande email. **Droit d'accès** : consultation de toutes leurs données personnelles stockées. **Droit de rectification** : modification de leurs informations de profil à tout moment. **Droit à l'effacement (droit à l'oubli)** : suppression complète du compte et anonymisation des données associées sous 30 jours. **Droit à la portabilité** : export de leurs données au format JSON ou CSV structuré. **Droit d'opposition** : désactivation du compte et cessation des traitements non contractuels (newsletters).

**Sécurité** : Le chiffrement TLS 1.3 protège les données en transit, le chiffrement at-rest sécurise la base de données, les accès sont tracés dans les audit logs, et les backups sont chiffrés. Les employés accédant aux données en production sont formés RGPD et liés par clauses de confidentialité.

**Sous-traitants** : Les sous-traitants (Stripe pour paiements, hébergeur cloud pour infrastructure) sont sélectionnés pour leur conformité RGPD avec Data Processing Agreements (DPA) signés garantissant le même niveau de protection. Les transferts hors UE respectent les mécanismes légaux (clauses contractuelles types).

**Notification de violation** : En cas de fuite de données, la CNIL est notifiée sous 72h si risque pour les droits et libertés, et les utilisateurs concernés sont informés directement si risque élevé.

#### Autres conformités

WCAG 2.1/RGAA pour l'accessibilité (détaillé ci-dessus), OWASP Top 10 pour la sécurité (détaillé ci-dessus), et anticipation de 21 CFR Part 11 (FDA Electronic Records) et GAMP 5 (Good Automated Manufacturing Practice) pour modules pharmaceutiques futurs nécessitant audit trail complet, signatures électroniques, et validation système étendue. Les mécanismes de conformité sont détaillés dans le [Dossier Projet - Section 18](./Dossier_Projet.md) et le [CdCT](./03_CdCT.md).

</div>

<div class="section-constraints">

## 9. Contraintes et limites

### Contraintes projet

Le projet est porté par un seul membre assumant tous les rôles (MOA/MOE), imposant une priorisation stricte des fonctionnalités et une gestion rigoureuse du temps. Le calendrier académique impose des jalons fixes avec livraison finale en juin 2026. Le budget est limité aux coûts d'infrastructure cloud (150-250€/mois estimés) sans possibilité d'investissement en licences payantes ou services premium.

### Contraintes techniques

L'architecture doit supporter le multi-tenant dès le MVP, complexifiant le modèle de données et l'isolation. Les modules optionnels doivent être anticipés architecturalement sans être développés au MVP, nécessitant une conception d'interfaces extensibles. La conformité RGPD et accessibilité est obligatoire dès la v1, imposant des développements spécifiques et des tests dédiés.

### Limites fonctionnelles MVP

Le MVP se concentre sur le Core et le Module Gestion de Projet uniquement. Les modules optionnels (LIMS, Qualité, GED) ne sont pas développés mais l'architecture les anticipe. Certaines fonctionnalités avancées sont reportées en post-MVP : gestion avancée des dépendances entre tâches, planning type Gantt interactif, intégrations tierces (Slack, Teams, calendriers), et application mobile native.

### Limitations par plan tarifaire

Le **plan Gratuit** est limité à 5 utilisateurs maximum, 3 projets actifs simultanés, Core uniquement sans modules optionnels, et support communautaire par email. Le **plan Pro** offre utilisateurs et projets illimités, accès à 2 modules optionnels au choix, et support prioritaire par email et chat. Le **plan Enterprise** débloque tous modules disponibles, développements sur mesure, support dédié avec SLA, et configuration personnalisée.

### Évolutions futures

Les évolutions post-MVP envisagées comprennent le développement des modules optionnels (LIMS, Qualité, GED), les intégrations avec outils tiers populaires, l'application mobile native (iOS/Android), le planning Gantt interactif, la gestion avancée des ressources (congés, absences, contrats), et l'intelligence artificielle pour optimiser l'assignation automatique.

</div>

<div class="section-wireframes">

## 10. Wireframes et maquettes

### Approche de conception

La conception UX/UI suit une démarche itérative centrée utilisateur avec prototypage rapide, tests utilisateurs, et ajustements basés sur les retours. Le design system repose sur shadcn-ui combiné à Tailwind CSS4, garantissant cohérence visuelle et maintenabilité. L'accessibilité est intégrée dès la conception avec respect WCAG 2.1 niveau AA.

### Parcours utilisateurs clés

Les parcours principaux identifiés incluent l'inscription avec souscription à un plan (onboarding complet), la création de projet et ajout de tâches (workflow manager), la consultation de charge de travail (dashboard collaborateur), l'assignation automatique de tâches (processus intelligent), et l'activation de modules optionnels (configuration admin).

### Wireframes basse fidélité

Les wireframes définissent l'arborescence de navigation (Dashboard → Projets → Tâches → Compétences → Reporting → Administration), la structure des pages principales (layouts, zones de contenu), les parcours utilisateurs avec points d'entrée et transitions, et les interactions principales (création, édition, assignation).

**[Wireframes à intégrer : Écrans principaux basse fidélité]**

### Maquettes haute fidélité

Les maquettes finalisent le design visuel avec charte graphique appliquée, composants UI finaux (boutons, formulaires, tableaux, graphiques), responsive design pour desktop/tablette/mobile, et états interactifs (hover, focus, disabled, error).

**[Maquettes à intégrer : Écrans finalisés haute fidélité]**

### Prototypes interactifs

Les prototypes permettent de tester les parcours utilisateurs en condition quasi-réelle avec navigation entre écrans, interactions simulées, et collecte de feedback. Les outils utilisés incluent Figma pour la conception collaborative et les prototypes cliquables.

**[Lien prototype Figma à intégrer]**

### Tests utilisateurs

Les tests utilisateurs sont réalisés auprès d'un panel représentatif (managers, collaborateurs) avec scénarios guidés, observation des interactions, recueil de feedback qualitatif, et ajustements itératifs. Les résultats des tests guident les optimisations UX avant développement.

</div>

<div class="section-conclusion">

## Conclusion

Ce Cahier des Charges Fonctionnel définit l'ensemble des besoins fonctionnels de la plateforme Taskforce, ERP modulaire SaaS innovant combinant gestion de projets classique et assignation automatique intelligente de tâches. L'approche modulaire (Core + Modules métier + Extensions optionnelles) garantit l'évolutivité du système tout en maintenant une complexité maîtrisée pour le MVP.

Les spécifications fonctionnelles détaillées dans ce document constituent la référence pour le développement et la validation de l'application. Les aspects techniques (architecture, technologies, infrastructure) sont traités dans le [CdCT](./03_CdCT.md) qui complète ce document. Le modèle économique et l'analyse de marché sont présentés dans l'[Étude Business](./Etude_business.md).

La réalisation suivra une approche agile avec validation progressive des fonctionnalités et ajustements basés sur les retours utilisateurs, dans le respect du planning projet détaillé dans le [Dossier Projet](./Dossier_Projet.md).

</div>

**Dernière mise à jour :** 27/02/2026  
**Version :** 1.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
