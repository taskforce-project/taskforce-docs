<!--
Logo établissement (placeholder)
Logo projet (placeholder)
-->

# CdCF – Cahier des Charges Fonctionnel

**Version :** 1.0  
**Date :** 17/01/2026  
**Auteur(s) :** [Nom Prénom]

---

[![Type: CdCF](https://img.shields.io/badge/Type-CdCF-green?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

---

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Business & Analyse de marché](./04_Etude_Faisabilite.md)
- [Documentation GitHub](https://github.com/...) <!-- À compléter -->
- [Repository GitHub](https://github.com/...)

---

**Tags :** `#gestion-de-projet` `#documentation` `#webapp` `#architecture` `#erp` `#saas` `#cahier-des-charges-fonctionnel` `#analyse-fonctionnelle`

---

## Table des matières

1. [Introduction et contexte](#1-introduction-et-contexte)
   - 1.1 [Objet du document](#11-objet-du-document)
   - 1.2 [Périmètre fonctionnel](#12-périmètre-fonctionnel)
   - 1.3 [Références et documents associés](#13-références-et-documents-associés)
   - 1.4 [Glossaire et terminologie métier](#14-glossaire-et-terminologie-métier)

2. [Expression du besoin](#2-expression-du-besoin)
   - 2.1 [Contexte métier et problématique](#21-contexte-métier-et-problématique)
   - 2.2 [Objectifs fonctionnels du projet](#22-objectifs-fonctionnels-du-projet)
   - 2.3 [Bénéfices attendus](#23-bénéfices-attendus)
   - 2.4 [Parties prenantes et utilisateurs cibles](#24-parties-prenantes-et-utilisateurs-cibles)
   - 2.5 [Positionnement produit (ERP modulaire / SaaS)](#25-positionnement-produit-erp-modulaire--saas)

3. [Analyse fonctionnelle](#3-analyse-fonctionnelle)
   - 3.1 [Architecture fonctionnelle générale](#31-architecture-fonctionnelle-générale)
     - 3.1.1 [Core applicatif](#311-core-applicatif)
     - 3.1.2 [Modules optionnels et extensions](#312-modules-optionnels-et-extensions)
     - 3.1.3 [Interactions inter-modules](#313-interactions-inter-modules)
   - 3.2 [Fonctions principales](#32-fonctions-principales)
     - 3.2.1 [Gestion des projets](#321-gestion-des-projets)
     - 3.2.2 [Gestion des tâches et affectations](#322-gestion-des-tâches-et-affectations)
     - 3.2.3 [Gestion des compétences](#323-gestion-des-compétences)
     - 3.2.4 [Assignation automatique des tâches](#324-assignation-automatique-des-tâches)
     - 3.2.5 [Suivi de la charge de travail](#325-suivi-de-la-charge-de-travail)
     - 3.2.6 [Alertes et notifications](#326-alertes-et-notifications)
   - 3.3 [Fonctions secondaires](#33-fonctions-secondaires)
     - 3.3.1 [Tableau de bord et reporting](#331-tableau-de-bord-et-reporting)
     - 3.3.2 [Gestion des équipes et organisations](#332-gestion-des-équipes-et-organisations)
     - 3.3.3 [Gestion des utilisateurs et rôles](#333-gestion-des-utilisateurs-et-rôles)
     - 3.3.4 [Gestion des abonnements et plans](#334-gestion-des-abonnements-et-plans)
     - 3.3.5 [Import / Export de données](#335-import--export-de-données)
   - 3.4 [Fonctions de support](#34-fonctions-de-support)
     - 3.4.1 [Authentification et autorisation](#341-authentification-et-autorisation)
     - 3.4.2 [Gestion des préférences utilisateur](#342-gestion-des-préférences-utilisateur)
     - 3.4.3 [Aide contextuelle et documentation](#343-aide-contextuelle-et-documentation)
     - 3.4.4 [Accessibilité (WCAG / RGAA)](#344-accessibilité-wcag--rgaa)

4. [Description détaillée des acteurs](#4-description-détaillée-des-acteurs)
   - 4.1 [Typologie des utilisateurs](#41-typologie-des-utilisateurs)
     - 4.1.1 [Collaborateur / Membre d'équipe](#411-collaborateur--membre-déquipe)
     - 4.1.2 [Manager / Chef de projet](#412-manager--chef-de-projet)
     - 4.1.3 [Administrateur système](#413-administrateur-système)
     - 4.1.4 [Invité / Utilisateur externe](#414-invité--utilisateur-externe)
   - 4.2 [Matrice acteurs / fonctionnalités](#42-matrice-acteurs--fonctionnalités)
   - 4.3 [Profils de permissions et contrôle d'accès](#43-profils-de-permissions-et-contrôle-daccès)

5. [Cas d'usage (Use Cases)](#5-cas-dusage-use-cases)
   - 5.1 [UC01 : Créer un projet](#51-uc01--créer-un-projet)
   - 5.2 [UC02 : Créer une tâche](#52-uc02--créer-une-tâche)
   - 5.3 [UC03 : Affecter manuellement une tâche](#53-uc03--affecter-manuellement-une-tâche)
   - 5.4 [UC04 : Déclencher l'assignation automatique](#54-uc04--déclencher-lassignation-automatique)
   - 5.5 [UC05 : Consulter la charge de travail](#55-uc05--consulter-la-charge-de-travail)
   - 5.6 [UC06 : Gérer les compétences d'un collaborateur](#56-uc06--gérer-les-compétences-dun-collaborateur)
   - 5.7 [UC07 : Configurer les alertes de surcharge](#57-uc07--configurer-les-alertes-de-surcharge)
   - 5.8 [UC08 : Générer un rapport d'avancement](#58-uc08--générer-un-rapport-davancement)
   - 5.9 [UC09 : S'abonner à un plan (plan gratuit ou payant)](#59-uc09--sabonner-à-un-plan-plan-gratuit-ou-payant)
   - 5.10 [UC10 : Gérer les modules optionnels](#510-uc10--gérer-les-modules-optionnels)
   - 5.11 [Autres cas d'usage fonctionnels](#511-autres-cas-d-usage-fonctionnels)

6. [Scénarios utilisateurs](#6-scénarios-utilisateurs)
   - 6.1 [Scénario 1 : Manager créant un projet et affectant des tâches](#61-scénario-1--manager-créant-un-projet-et-affectant-des-tâches)
   - 6.2 [Scénario 2 : Collaborateur consultant ses tâches et sa charge](#62-scénario-2--collaborateur-consultant-ses-tâches-et-sa-charge)
   - 6.3 [Scénario 3 : Détection et résolution d'une surcharge](#63-scénario-3--détection-et-résolution-dune-surcharge)
   - 6.4 [Scénario 4 : Activation d'un module optionnel (ex : LIMS)](#64-scénario-4--activation-dun-module-optionnel-ex--lims)
   - 6.5 [Scénario 5 : Passage d'un plan gratuit à un plan payant](#65-scénario-5--passage-dun-plan-gratuit-à-un-plan-payant)

7. [Diagrammes UML fonctionnels](#7-diagrammes-uml-fonctionnels)
   - 7.1 [Diagramme de cas d'usage général](#71-diagramme-de-cas-dusage-général)
   - 7.2 [Diagrammes de cas d'usage détaillés par module](#72-diagrammes-de-cas-dusage-détaillés-par-module)
   - 7.3 [Diagrammes d'activité](#73-diagrammes-dactivité)
     - 7.3.1 [Processus d'assignation automatique](#731-processus-dassignation-automatique)
     - 7.3.2 [Processus de création de projet](#732-processus-de-création-de-projet)
     - 7.3.3 [Processus de gestion de surcharge](#733-processus-de-gestion-de-surcharge)
   - 7.4 [Diagrammes de séquence](#74-diagrammes-de-séquence)
     - 7.4.1 [Séquence : Assignation automatique](#741-séquence--assignation-automatique)
     - 7.4.2 [Séquence : Consultation de la charge](#742-séquence--consultation-de-la-charge)
     - 7.4.3 [Séquence : Souscription à un plan](#743-séquence--souscription-à-un-plan)
   - 7.5 [Diagrammes d'état-transition](#75-diagrammes-détat-transition)
     - 7.5.1 [États d'une tâche](#751-états-dune-tâche)
     - 7.5.2 [États d'un projet](#752-états-dun-projet)
     - 7.5.3 [États d'un abonnement](#753-états-dun-abonnement)

8. [Structuration du projet (PBS / WBS)](#8-structuration-du-projet-pbs--wbs)
   - 8.1 [Product Breakdown Structure (PBS)](#81-product-breakdown-structure-pbs)
     - 8.1.1 [Décomposition par modules fonctionnels](#811-décomposition-par-modules-fonctionnels)
     - 8.1.2 [Hiérarchie des fonctionnalités](#812-hiérarchie-des-fonctionnalités)
   - 8.2 [Work Breakdown Structure (WBS)](#82-work-breakdown-structure-wbs)
     - 8.2.1 [Décomposition par lots de travail](#821-décomposition-par-lots-de-travail)
     - 8.2.2 [Attribution des responsabilités (RACI)](#822-attribution-des-responsabilités-raci)
   - 8.3 [Matrice de traçabilité exigences / livrables](#83-matrice-de-traçabilité-exigences--livrables)

9. [Exigences fonctionnelles détaillées](#9-exigences-fonctionnelles-détaillées)
   - 9.1 [Exigences de gestion de projet](#91-exigences-de-gestion-de-projet)
     - 9.1.1 [Création et configuration de projets](#911-création-et-configuration-de-projets)
     - 9.1.2 [Gestion du cycle de vie des projets](#912-gestion-du-cycle-de-vie-des-projets)
     - 9.1.3 [Organisation hiérarchique (portefeuilles, programmes)](#913-organisation-hiérarchique-portefeuilles-programmes)
   - 9.2 [Exigences de gestion des tâches](#92-exigences-de-gestion-des-tâches)
     - 9.2.1 [CRUD des tâches](#921-crud-des-tâches)
     - 9.2.2 [Affectation et réaffectation](#922-affectation-et-réaffectation)
     - 9.2.3 [Dépendances entre tâches](#923-dépendances-entre-tâches)
     - 9.2.4 [Jalons et échéances](#924-jalons-et-échéances)
   - 9.3 [Exigences de gestion des compétences](#93-exigences-de-gestion-des-compétences)
     - 9.3.1 [Référentiel de compétences](#931-référentiel-de-compétences)
     - 9.3.2 [Attribution et niveau de maîtrise](#932-attribution-et-niveau-de-maîtrise)
     - 9.3.3 [Évolution et certification](#933-évolution-et-certification)
   - 9.4 [Exigences d'assignation automatique](#94-exigences-dassignation-automatique)
     - 9.4.1 [Algorithme d'assignation](#941-algorithme-dassignation)
     - 9.4.2 [Critères de sélection (compétences, charge, priorités)](#942-critères-de-sélection-compétences-charge-priorités)
     - 9.4.3 [Configuration et paramétrage](#943-configuration-et-paramétrage)
     - 9.4.4 [Gestion des contraintes (disponibilité, préférences)](#944-gestion-des-contraintes-disponibilité-préférences)
   - 9.5 [Exigences de suivi de charge](#95-exigences-de-suivi-de-charge)
     - 9.5.1 [Calcul de la charge individuelle](#951-calcul-de-la-charge-individuelle)
     - 9.5.2 [Visualisation temps réel](#952-visualisation-temps-réel)
     - 9.5.3 [Seuils d'alerte](#953-seuils-dalerte)
     - 9.5.4 [Historiques et tendances](#954-historiques-et-tendances)
   - 9.6 [Exigences de notification et alerte](#96-exigences-de-notification-et-alerte)
     - 9.6.1 [Déclencheurs d'alertes](#961-déclencheurs-dalertes)
     - 9.6.2 [Canaux de notification (in-app, email, webhook)](#962-canaux-de-notification-in-app-email-webhook)
     - 9.6.3 [Paramétrage utilisateur](#963-paramétrage-utilisateur)
   - 9.7 [Exigences de reporting et tableaux de bord](#97-exigences-de-reporting-et-tableaux-de-bord)
     - 9.7.1 [Indicateurs clés (KPI)](#971-indicateurs-clés-kpi)
     - 9.7.2 [Tableaux de bord personnalisables](#972-tableaux-de-bord-personnalisables)
     - 9.7.3 [Export de rapports](#973-export-de-rapports)
   - 9.8 [Exigences de gestion des abonnements](#98-exigences-de-gestion-des-abonnements)
     - 9.8.1 [Plans tarifaires (gratuit, payant)](#981-plans-tarifaires-gratuit-payant)
     - 9.8.2 [Gestion via Stripe](#982-gestion-via-stripe)
     - 9.8.3 [Limitation des fonctionnalités par plan](#983-limitation-des-fonctionnalités-par-plan)
     - 9.8.4 [Migration entre plans](#984-migration-entre-plans)
   - 9.9 [Exigences de modularité et extensibilité](#99-exigences-de-modularité-et-extensibilité)
     - 9.9.1 [Activation / désactivation de modules](#991-activation--désactivation-de-modules)
     - 9.9.2 [API pour extensions tierces](#992-api-pour-extensions-tierces)
     - 9.9.3 [Gestion des dépendances inter-modules](#993-gestion-des-dépendances-inter-modules)

10. [Exigences non fonctionnelles (référence)](#10-exigences-non-fonctionnelles-référence)
    - 10.1 [Renvoi vers le CdCT](#101-renvoi-vers-le-cdct)
    - 10.2 [Synthèse des contraintes impactant le fonctionnel](#102-synthèse-des-contraintes-impactant-le-fonctionnel)
      - 10.2.1 [Performance et temps de réponse](#1021-performance-et-temps-de-réponse)
      - 10.2.2 [Ergonomie et expérience utilisateur](#1022-ergonomie-et-expérience-utilisateur)
      - 10.2.3 [Conformité réglementaire (RGPD)](#1023-conformité-réglementaire-rgpd)
      - 10.2.4 [Accessibilité (WCAG / RGAA)](#1024-accessibilité-wcag--rgaa)

11. [Parcours utilisateurs et maquettes fonctionnelles](#11-parcours-utilisateurs-et-maquettes-fonctionnelles)
    - 11.1 [Wireframes basse fidélité](#111-wireframes-basse-fidélité)
    - 11.2 [Prototypes interactifs (référence)](#112-prototypes-interactifs-référence)
    - 11.3 [Arborescence de navigation](#113-arborescence-de-navigation)
    - 11.4 [Flux d'interactions principaux](#114-flux-dinteractions-principaux)

12. [Règles métier et logiques fonctionnelles](#12-règles-métier-et-logiques-fonctionnelles)
    - 12.1 [Règles d'assignation automatique](#121-règles-dassignation-automatique)
    - 12.2 [Règles de calcul de charge](#122-règles-de-calcul-de-charge)
    - 12.3 [Règles de priorisation des tâches](#123-règles-de-priorisation-des-tâches)
    - 12.4 [Règles de validation et de conformité](#124-règles-de-validation-et-de-conformité)
    - 12.5 [Règles de gestion des droits et permissions](#125-règles-de-gestion-des-droits-et-permissions)

13. [Critères de validation et d'acceptation](#13-critères-de-validation-et-dacceptation)
    - 13.1 [Critères d'acceptation par fonctionnalité](#131-critères-dacceptation-par-fonctionnalité)
    - 13.2 [Scénarios de tests fonctionnels](#132-scénarios-de-tests-fonctionnels)
    - 13.3 [Indicateurs de performance fonctionnelle](#133-indicateurs-de-performance-fonctionnelle)
    - 13.4 [Critères de recette utilisateur](#134-critères-de-recette-utilisateur)
    - 13.5 [Matrice de traçabilité exigences / tests](#135-matrice-de-traçabilité-exigences--tests)

14. [Gestion des évolutions et priorisation](#14-gestion-des-évolutions-et-priorisation)
    - 14.1 [Roadmap fonctionnelle](#141-roadmap-fonctionnelle)
    - 14.2 [Priorisation des fonctionnalités (MoSCoW)](#142-priorisation-des-fonctionnalités-moscow)
      - 14.2.1 [Must Have (indispensables)](#1421-must-have-indispensables)
      - 14.2.2 [Should Have (importantes)](#1422-should-have-importantes)
      - 14.2.3 [Could Have (souhaitables)](#1423-could-have-souhaitables)
      - 14.2.4 [Won't Have (hors périmètre)](#1424-wont-have-hors-périmètre)
    - 14.3 [Gestion des demandes d'évolution](#143-gestion-des-demandes-dévolution)
    - 14.4 [Processus de validation des changements](#144-processus-de-validation-des-changements)

15. [Contraintes et limitations fonctionnelles](#15-contraintes-et-limitations-fonctionnelles)
    - 15.1 [Limitations par plan tarifaire](#151-limitations-par-plan-tarifaire)
    - 15.2 [Contraintes de volumétrie](#152-contraintes-de-volumétrie)
    - 15.3 [Contraintes métier](#153-contraintes-métier)
    - 15.4 [Dépendances externes](#154-dépendances-externes)

16. [Annexes](#16-annexes)
    - 16.1 [Glossaire métier](#161-glossaire-métier)
    - 16.2 [Liste des acronymes](#162-liste-des-acronymes)
    - 16.3 [Références documentaires](#163-références-documentaires)
    - 16.4 [Historique des versions du document](#164-historique-des-versions-du-document)

---

**Note importante :** Ce document est le Cahier des Charges Fonctionnel (CdCF). Il décrit **ce que** le système doit faire du point de vue métier et utilisateur. Pour les aspects techniques (architecture, technologies, infrastructure, sécurité technique, etc.), se référer au [CdCT – Cahier des Charges Technique](./03_CdCT.md).
