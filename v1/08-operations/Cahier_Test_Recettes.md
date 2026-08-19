---
id: cahier-test-recettes
title: Cahier de recettes — TaskForce V1
doc_type: recettes
statut: valide
version: 2.0
date: "23/07/2026"
auteur: Pierre MICHEL
tags: [recettes, tests, scenarios, acceptance, cdc, qualite, memoire, rncp, soutenance]
---

# Cahier de recettes — TaskForce V1

> **Version 2.0, recadrée sur le cahier des charges.** La v1.0 organisait ses scénarios par cas
> d'usage de l'application, ce qui plaçait la facturation, la messagerie et le wiki au même rang que
> l'assignation automatique. Aucun de ces trois sujets ne figure au cahier des charges : ce sont des
> ajouts faits en cours de projet.
>
> Un cahier de recettes répond à la question du client : **l'application fait-elle ce qui a été
> demandé ?** Il est donc structuré sur les **six attentes fonctionnelles du §4 du CDC**, puis sur
> ses exigences techniques (§5) et ses critères de qualité (§7).
>
> Les fonctionnalités ajoutées n'apparaissent dans le corps du document que lorsqu'elles
> **prolongent une attente du CDC**, et elles sont alors signalées comme telles. Le périmètre étendu
> est récapitulé en annexe, pour mémoire, sans être présenté comme de la recette contractuelle.

## Comment lire ce document

Chaque attente est éprouvée par des **cas nominaux** et des **cas d'échec**. Un cahier qui ne décrit
que le chemin heureux ne prouve rien : c'est le comportement en cas d'erreur qui sépare une
application livrable d'une démonstration.

**Statut** : ✅ automatisé · 🟡 partiellement automatisé · ⬜ manuel uniquement.
La colonne « Test » ne cite que des classes ou fichiers **vérifiés présents dans le dépôt** au
23/07/2026.

## Correspondance des acteurs

Le CDC définit trois acteurs, TaskForce en implémente trois, mais le découpage diffère. Autant le
dire.

| Acteur du CDC | Rôle TaskForce | Écart |
|---|---|---|
| **Le Collaborateur** — reçoit les tâches assignées | `MEMBER` | Correspondance directe |
| **Le Manager** — suit la progression, ajuste les priorités, reçoit les alertes | `ADMIN` | Correspondance directe |
| **Le Responsable de Projet** — allocation initiale, définit les compétences requises et les priorités | `ADMIN`, ou `OWNER` pour la gestion du workspace | **Les deux rôles superviseurs du CDC ont été fusionnés.** Leurs permissions auraient été identiques : deux rôles indistinguables auraient ajouté de la complexité sans usage. Le `OWNER` porte en plus la gestion du workspace, qui n'est pas une demande du CDC |

---

# Attentes fonctionnelles du CDC (§4)

## F1 — Assignation automatique des tâches

> *« Basé sur les compétences, les disponibilités et la charge de travail actuelle des
> collaborateurs. »*

**Implémentation** : `SmartAssignService`. **Préconditions** : un workspace avec au moins deux
membres disposant d'un profil de compétences, et une issue non assignée.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F1-01 | Assignation nominale sur une issue décrite | Un candidat est proposé, avec son score et le détail des signaux ayant conduit à la décision | `SmartAssignServiceTest` | ✅ |
| F1-02 | Le candidat le plus compétent est surchargé | Le signal de charge le fait reculer au profit d'un candidat moins spécialisé mais disponible. C'est l'objectif même du CDC : éviter les surcharges | `SmartAssignServiceTest` | ✅ |
| F1-03 | Deux candidats de compétence équivalente | Départage sur la charge, puis sur l'historique. La décision reste déterministe | `SmartAssignServiceTest` | ✅ |
| F1-04 | **Échec** : aucun membre ne possède la compétence requise | Aucune assignation arbitraire. L'issue reste non assignée et le motif est exposé | `SmartAssignServiceTest` | ✅ |
| F1-05 | **Échec** : le modèle de langage est injoignable | Repli déterministe côté Java, l'assignation reste possible. **Aucune interruption de service** | `SmartAssignServiceTest` | ✅ |
| F1-06 | **Échec** : issue sans description exploitable | Le signal sémantique est neutralisé, les autres signaux continuent de s'appliquer | `SmartAssignServiceTest` | ✅ |
| F1-07 | **Échec** : demande sur un workspace dont l'appelant n'est pas membre | `403`, aucune donnée du workspace n'est divulguée | `AuthorizationServiceTest` | ✅ |

## F2 — Gestion des compétences

> *« Chaque collaborateur aura un profil avec ses compétences et son expérience dans différents
> domaines. »*

**Implémentation** : `MemberSkillProfileService`, table `member_skill_profiles`.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F2-01 | Création d'un profil de compétences | Compétences, séniorité et capacité hebdomadaire enregistrées et relues à l'identique | `MemberSkillProfileServiceIntegrationTest` | ✅ |
| F2-02 | Mise à jour d'une compétence | Prise en compte par l'assignation suivante, sans redémarrage | `MemberSkillProfileServiceIntegrationTest` | ✅ |
| F2-03 | Consultation de son profil par un collaborateur | Lecture autorisée, données complètes | `skill-service.test.ts`, `skill-store.test.ts` | ✅ |
| F2-04 | **Échec** : capacité hebdomadaire aberrante | `400`, validation refusée avant persistance | `MemberSkillProfileServiceIntegrationTest` | ✅ |
| F2-05 | **Échec** : modification du profil d'autrui par un collaborateur | `403` | `MemberSkillProfileServiceIntegrationTest` | ✅ |
| F2-06 | **Échec** : profil absent au moment de l'assignation | Le membre est écarté des candidats sans faire échouer l'assignation | `SmartAssignServiceTest` | ✅ |
| F2-07 | *Extension rattachée à F2* : mode montée en compétence, favorisant un candidat en apprentissage | Bonus plafonné, jamais dominant sur la compétence réelle | `SmartAssignServiceTest` | ✅ |

## F3 — Suivi de la charge de travail

> *« Tableau de bord permettant de suivre en temps réel la répartition des tâches et la charge de
> travail des collaborateurs. »*

**Implémentation** : `AnalyticsService`, `DashboardCardService`, temps réel via STOMP.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F3-01 | Affichage de la charge par collaborateur | La charge affichée correspond aux issues ouvertes réellement assignées | `AnalyticsServiceIntegrationTest` | ✅ |
| F3-02 | Mise à jour après assignation | Le tableau reflète le changement sans rechargement manuel | `use-notifications-realtime.test.ts` | ✅ |
| F3-03 | Composition du tableau de bord | Cartes choisies et ordre persistés par utilisateur | `DashboardCardServiceTest`, `dashboard-cards-store.test.ts` | ✅ |
| F3-04 | **Échec** : workspace sans aucune issue | État vide explicite, ni erreur ni division par zéro | `AnalyticsServiceIntegrationTest` | ✅ |
| F3-05 | **Échec** : accès au tableau de bord d'un workspace tiers | `403`, aucune fuite de volumétrie | `AnalyticsServiceIntegrationTest` | ✅ |
| F3-06 | **Échec** : connexion temps réel sans jeton valide | La connexion est **refusée**, pas dégradée en silence | `StompAuthInterceptor` (tests dédiés) | ✅ |

## F4 — Ajustements dynamiques

> *« Redistribution automatique des tâches en fonction des disponibilités et des éventuels retards
> ou surcharges. »*

**Implémentation** : `RedistributionService`. C'est le cœur du CDC, ce qui distingue TaskForce d'un
gestionnaire de tâches ordinaire.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F4-01 | Redistribution après détection d'une surcharge | Réattribution vers des membres disponibles, chaque décision étant tracée | `RedistributionServiceTest` | ✅ |
| F4-02 | Parcours complet depuis l'interface | L'utilisateur déclenche, visualise les propositions, confirme | `redistribution.spec.ts` (bout en bout) | ✅ |
| F4-03 | Historisation des décisions | Chaque réattribution est conservée avec son motif : la décision reste auditable | `RedistributionServiceTest` | ✅ |
| F4-04 | **Échec** : aucun membre disponible pour absorber la charge | Aucune réattribution forcée. La surcharge est **signalée** plutôt que déplacée sur un membre déjà saturé | `RedistributionServiceTest` | ✅ |
| F4-05 | **Échec** : déclenchement par un collaborateur sans droit | `403` | `RedistributionControllerWebMvcTest` | ✅ |
| F4-06 | **Échec** : issue déjà réassignée entre-temps | Pas d'écrasement silencieux, l'état courant fait foi | `RedistributionServiceTest` | ✅ |

## F5 — Notifications et alertes

> *« Alertes en cas de surcharge de travail ou de retard dans l'accomplissement des tâches. »*

**Implémentation** : `OverloadAlertScheduler` (quotidien, 08h30), `DueDateAlertScheduler`
(quotidien, 08h00), `NotificationService`.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F5-01 | Alerte de surcharge émise vers les managers | Seuls `OWNER` et `ADMIN` sont notifiés, pas le collaborateur concerné | `OverloadAlertSchedulerTest` | ✅ |
| F5-02 | Absence de doublon | Une alerte non acquittée n'est pas réémise le lendemain | `NotificationServiceTest` | ✅ |
| F5-03 | Réception en temps réel | La notification apparaît sans rechargement | `use-notifications-realtime.test.ts`, `notification-store.test.ts` | ✅ |
| F5-04 | **Échec** : aucun membre en surcharge | Aucune alerte émise, le job se termine normalement | `OverloadAlertSchedulerTest` | ✅ |
| F5-05 | **Échec** : workspace sans manager | Le job n'échoue pas et n'émet pas d'alerte orpheline | `OverloadAlertSchedulerTest` | ✅ |
| F5-06 | Alerte d'échéance approchant ou dépassée | Les issues ouvertes et assignées dont l'échéance approche déclenchent une notification | **aucun test dédié** | ⬜ |

> **Écart déclaré, relevé le 23/07/2026.** `DueDateAlertScheduler` n'a **aucune classe de test**,
> alors que l'alerte de retard est une attente du CDC au même titre que l'alerte de surcharge, elle
> testée. F5-06 n'est donc vérifiable que manuellement. Le déclenchement est configurable par la
> propriété `taskforce.alerts.due-date-cron`, ce qui permet de le rejouer en démonstration sans
> attendre 08h00.

## F6 — Rapports et analyses

> *« Génération de rapports sur la répartition des tâches, les performances des collaborateurs, et
> les délais de réalisation. »*

**Implémentation** : `AnalyticsController`, `AnalyticsService`, export CSV.

| ID | Scénario | Critère d'acceptation | Test | Statut |
|---|---|---|---|:--:|
| F6-01 | Rapport de répartition des tâches | Volumes par membre et par statut conformes aux données réelles | `AnalyticsServiceIntegrationTest` | ✅ |
| F6-02 | Indicateurs de délai | Les issues en retard sont comptées sur la base de l'échéance et du statut | `AnalyticsServiceIntegrationTest` | ✅ |
| F6-03 | *Extension rattachée à F6* : export CSV de la liste d'issues | Conforme RFC 4180 : échappement des virgules, guillemets et retours à la ligne ; BOM UTF-8 pour la lecture par un tableur | `export-issues-csv.test.ts` (20 cas) | ✅ |
| F6-04 | **Échec** : période sans aucune donnée | Rapport vide et lisible, pas d'erreur | `AnalyticsServiceIntegrationTest` | ✅ |
| F6-05 | **Échec** : consultation par un non-membre | `403` | `AnalyticsServiceIntegrationTest` | ✅ |

---

# Exigences techniques du CDC (§5)

| ID | Exigence | Critère d'acceptation | Vérification | Statut |
|---|---|---|---|:--:|
| T-01 | **API REST** permettant l'intégration avec d'autres outils | 36 contrôleurs, 219 points d'entrée, documentés en OpenAPI et consultables via Swagger | `Spec_API_OpenAPI.md`, tests de tranche web | ✅ |
| T-02 | **Respect du RGPD** | Registre de 9 traitements, droits d'accès et d'effacement exposés, durées de conservation appliquées automatiquement | `Registre_Traitements_RGPD.md`, `GdprService`, `RetentionSchedulerTest` | ✅ |
| T-03 | **Compatibilité multi-navigateurs** (Chrome, Firefox, Safari) | Aucune interface propriétaire ; cible de construction standard | vérification manuelle | 🟡 |
| T-04 | **Design responsive** (desktop, tablette, mobile) | Points de rupture appliqués sur toutes les vues | vérification manuelle | 🟡 |

> **Deux exigences en jaune, et c'est volontaire.** T-03 et T-04 ne sont couvertes par aucun test
> automatisé : il n'existe ni campagne multi-navigateurs ni test de rendu par taille d'écran,
> Playwright ne s'exécutant que sur Chromium. Les déclarer vertes serait une sur-déclaration qu'une
> seule question du jury mettrait en défaut.

# Critères de qualité du CDC (§7)

| ID | Critère | Critère d'acceptation | Vérification | Statut |
|---|---|---|---|:--:|
| Q-01 | **Chiffrement des données personnelles** | AES-256-GCM appliqué aux secrets stockés | `EncryptedStringConverterTest` (9 cas) | 🟡 |
| Q-02 | **Performance** sur un volume important | Index et pagination systématiques sur les listes | revue de code, **aucun test de charge** | 🟡 |
| Q-03 | **Évolutivité**, code modulaire | Architecture en couches `shared ← core ← modules`, dépendances unidirectionnelles | `Architecture_C4.md`, analyse statique | ✅ |
| Q-04 | **Fiabilité** de l'assignation et de la redistribution à volume variable | Décisions déterministes, repli sans modèle de langage, historisation | `SmartAssignServiceTest`, `RedistributionServiceTest` | ✅ |

> **Q-01, formulation à ne pas surestimer.** Le chiffrement porte sur les **secrets** : identifiants
> de connecteurs, configuration d'intégration, deux champs des demandes Enterprise. Le CDC demande
> le chiffrement des « données personnelles des employés (compétences, charge de travail) » : **ces
> données ne sont pas chiffrées**. Elles sont protégées par le contrôle d'accès et le chiffrement
> disque de l'hôte. L'adresse de courriel et l'identifiant d'authentification ne le sont pas non
> plus, le chiffrement authentifié n'étant pas déterministe et casserait les recherches. Choix
> défendable, à condition d'être annoncé.
>
> **Q-02** : aucun test de charge n'a été mené. L'affirmation de performance repose sur des choix de
> conception vérifiables par lecture, pas sur une mesure. À ne pas présenter comme démontré.

---

# Synthèse de couverture

| Périmètre | Scénarios | Automatisés | Manuels |
|---|:--:|:--:|:--:|
| F1 Assignation automatique | 7 | 7 | 0 |
| F2 Gestion des compétences | 7 | 7 | 0 |
| F3 Suivi de la charge | 6 | 6 | 0 |
| F4 Ajustements dynamiques | 6 | 6 | 0 |
| F5 Notifications et alertes | 6 | 5 | 1 |
| F6 Rapports et analyses | 5 | 5 | 0 |
| Exigences techniques (§5) | 4 | 2 | 2 |
| Critères de qualité (§7) | 4 | 3 | 1 |
| **Total périmètre CDC** | **45** | **41** | **4** |

**Les six attentes fonctionnelles sont couvertes**, chacune avec ses cas nominaux **et** ses cas
d'échec. Sur 45 scénarios, 41 sont adossés à un test automatisé vérifié présent dans le dépôt.

# Écarts connus, à énoncer avant qu'on les trouve

1. **`DueDateAlertScheduler` n'a aucun test**, quand son homologue de surcharge en a un. C'est le seul manque de couverture sur une attente fonctionnelle du CDC.
2. **Aucune campagne multi-navigateurs** : Playwright ne s'exécute que sur Chromium.
3. **Aucun test de charge** : la performance annoncée est un choix de conception, pas une mesure.
4. **Le chiffrement ne couvre ni les compétences ni la charge de travail**, que le CDC cite pourtant nommément.

---

# Annexe — Périmètre étendu, hors cahier des charges

Ces fonctionnalités ont été ajoutées en cours de projet. Elles ne relèvent pas de la recette
contractuelle et ne sont pas comptées dans la synthèse ci-dessus, mais elles sont testées et leur
volume témoigne de l'ampleur du travail réalisé.

| Domaine | Scénarios | Couverture | Rattachement éventuel au CDC |
|---|:--:|---|---|
| Inscription avec vérification par code à usage unique | 7 | ✅ automatisée | Prérequis d'accès, non demandé explicitement |
| Connexion, jetons, révocation | 6 | ✅ automatisée | idem |
| Gestion de workspace | 5 | ✅ automatisée | Support du multi-équipes, non demandé |
| Membres et invitations | 7 | ✅ automatisée | Peuple les acteurs du CDC |
| Projets | 6 | ✅ automatisée | Regroupe les tâches du CDC |
| Issues, statuts, relations | 9 | ✅ automatisée | **Support direct des tâches du CDC** |
| Cycles | 6 | 🟡 5 sur 6 | Extension du suivi de charge |
| Messagerie | 5 | 🟡 4 sur 5 | Hors CDC |
| Pages de documentation | 4 | ✅ automatisée | Hors CDC |
| Abonnement et facturation | 8 | ✅ automatisée | Hors CDC, sert la monétisation du titre |
| Export et effacement RGPD | 4 | ✅ automatisée | **Rattaché à T-02** |
| Sécurité transverse | 6 | ✅ automatisée | **Rattaché à Q-01 et T-02** |

Sur la sécurité transverse, une correction du 23/07/2026 mérite d'être signalée : le test
d'accessibilité s'intitulait « WCAG 2.1 AA » mais n'échouait que sur les violations de niveau
`critical`, alors que les manquements AA remontent en `serious`. Dix violations passaient
inaperçues. Le seuil inclut désormais `serious`, elles ont été corrigées, et l'assertion à zéro
violation est devenue vraie.

---

> Voir aussi : [[Politique_Tests]] · [[Matrice_Tracabilite_Tests]] · [[Registre_Traitements_RGPD]] ·
> [[Problemes_Connus]] · [[Manuel_Utilisateur]] pour le périmètre étendu.
