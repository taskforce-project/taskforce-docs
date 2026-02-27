# Plan de Sauvegarde, Continuité et Reprise d'Activité (PS/PCA/PRA)

**Version :** 1.0  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Technique](https://img.shields.io/badge/Type-Documentation%20Technique-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Priorité: Critique](https://img.shields.io/badge/Priorité-Critique-red?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](../projet/Dossier_Projet.md)
- [CdCF - Cahier des Charges Fonctionnel](../projet/01_CdCF.md)
- [CdCT - Cahier des Charges Technique](../projet/02_CdCT.md)
- [Architecture Technique](./Architecture.md)
- [Sécurité](./Sécurité.md)
- [DevOps](./DevOps.md)

**Tags :** `#sauvegarde` `#backup` `#pca` `#pra` `#continuité-activité` `#disaster-recovery` `#résilience` `#haute-disponibilité`

## Table des matières

1. [Vue d'ensemble et objectifs](#1-vue-densemble-et-objectifs)
2. [Plan de Sauvegarde (PS)](#2-plan-de-sauvegarde-ps)
3. [Plan de Continuité d'Activité (PCA)](#3-plan-de-continuité-dactivité-pca)
4. [Plan de Reprise d'Activité (PRA)](#4-plan-de-reprise-dactivité-pra)
5. [Organisation et gouvernance](#5-organisation-et-gouvernance)
6. [Amélioration continue](#6-amélioration-continue)

## 1. Vue d'ensemble et objectifs

### 1.1 Contexte et enjeux

La plateforme Taskforce est construite comme un service SaaS multi-tenant destiné à gérer les projets et tâches de multiples organisations clientes. Dans ce contexte, la disponibilité continue et la protection des données ne sont pas optionnelles : elles conditionnent directement la confiance des clients et la viabilité commerciale du service. Ce document établit la stratégie globale pour garantir cette résilience à travers trois piliers complémentaires : la sauvegarde des données, la continuité de service en cas d'incident mineur, et la capacité de reprise complète après un sinistre majeur.

### 1.2 Objectifs stratégiques et indicateurs clés

La stratégie de résilience repose sur deux objectifs mesurables fondamentaux : le Recovery Time Objective (RTO) qui fixe le délai maximal acceptable pour restaurer un service après incident, et le Recovery Point Objective (RPO) qui définit la perte de données maximale tolérable. Pour Taskforce, le RTO cible est fixé à 4 heures maximum, ce qui signifie qu'en cas de panne complète, le service doit être restauré dans ce délai. Le RPO est quant à lui établi à 15 minutes, limitant la perte potentielle de données à ce court intervalle.

Ces objectifs ambitieux se traduisent concrètement par un engagement de disponibilité annuelle de 99,9%, soit environ 8 heures d'interruption maximale par an. Pour atteindre ces cibles, l'infrastructure est conçue avec plusieurs niveaux de redondance et des mécanismes automatiques de basculement qui permettent de maintenir le service même en cas de défaillance partielle.

| Indicateur | Objectif | Seuil critique |
|------------|----------|----------------|
| **RTO** (temps de restauration) | < 4 heures | 8 heures max |
| **RPO** (perte de données) | < 15 minutes | 1 heure max |
| **Disponibilité annuelle** | 99,9% (8h downtime/an) | 99,5% minimum |
| **Taux de réussite backups** | 99,95% | 99% minimum |

---

## 2. Plan de Sauvegarde (PS)

### 2.1 Stratégie globale

La stratégie de sauvegarde suit le principe éprouvé de la règle 3-2-1 : maintenir trois copies des données (l'originale en production plus deux sauvegardes), sur deux types de supports différents (disque et cloud), avec au moins une copie stockée hors site dans une région géographique distincte. Cette approche garantit qu'une défaillance unique, qu'elle soit matérielle ou géographique, ne peut jamais entraîner de perte de données.

Le modèle de sauvegarde adopté privilégie la continuité plutôt que les snapshots isolés. PostgreSQL utilise un système de Write-Ahead Logging (WAL) qui capture chaque modification de la base de données en temps quasi-réel, permettant de restaurer l'état exact de la base à n'importe quel moment avec une précision de quelques secondes. Cette approche incrémentale continue est complétée par des snapshots complets réguliers qui servent de points de référence pour accélérer les restaurations.

### 2.2 Données sauvegardées et fréquence

Les données critiques de la plateforme incluent la base PostgreSQL complète avec son schéma, les fichiers uploadés par les utilisateurs (avatars, documents, exports), les configurations système (variables d'environnement, secrets Kubernetes), et les logs applicatifs nécessaires à l'audit. Chaque catégorie suit une politique de sauvegarde adaptée à sa criticité et son volume.

La base de données bénéficie d'une protection maximale avec un archivage WAL continu (toutes les 5 minutes ou dès que 16 MB de données sont modifiées) et des snapshots complets toutes les 6 heures. Les fichiers utilisateurs sont directement stockés sur S3 avec le versioning activé, créant automatiquement une nouvelle version à chaque modification. Les configurations sont sauvegardées à chaque changement, et les logs sont agrégés en continu avec une rétention de 90 jours pour respecter les besoins d'audit sécurité.

| Type de données | Méthode | Fréquence | Rétention |
|-----------------|---------|-----------|-----------|
| Base PostgreSQL | WAL continu + Snapshot | Continue + 6h | WAL 7j, Snapshot 30j |
| Fichiers utilisateurs | S3 versioning | Temps réel | 90 jours versions |
| Configurations | Backup incrémental | À chaque modification | 365 jours |
| Logs applicatifs | Agrégation continue | Temps réel | 90 jours |

### 2.3 Infrastructure et réplication

L'architecture de sauvegarde s'articule autour de deux régions cloud géographiquement séparées (Paris et Milan). La région primaire héberge la base de données en production ainsi que les archives WAL locales. Chaque modification est immédiatement archivée localement puis répliquée de manière asynchrone vers un bucket S3 dans la région primaire. Ce bucket S3 est lui-même configuré avec une réplication cross-region automatique vers la région secondaire, créant ainsi trois copies géographiquement distribuées des données.

Pour les fichiers utilisateurs stockés directement sur S3, la réplication cross-region est également active avec un délai typique inférieur à 15 minutes. Les anciennes versions de fichiers suivent une politique de cycle de vie automatique : après 30 jours, elles migrent vers le tier de stockage Infrequent Access moins coûteux, puis après 90 jours vers Glacier pour archivage long terme à coût minimal.

### 2.4 Tests et validation

La fiabilité des sauvegardes ne peut être garantie sans tests réguliers de restauration. Un programme structuré vérifie hebdomadairement la capacité à restaurer un fichier individuel, mensuellement la restauration complète d'une base de données en environnement de test, et trimestriellement la procédure de restauration totale incluant tous les services. Ces tests ne sont pas de simples formalités : chaque restauration est chronométrée pour mesurer les RTO/RPO effectifs, et les écarts par rapport aux objectifs déclenchent immédiatement des actions correctives.

Le test mensuel de base de données suit un protocole rigoureux : provisionnement d'une instance PostgreSQL isolée, restauration du dernier snapshot complet, application des archives WAL jusqu'à un point précis dans le temps, vérification de l'intégrité des données via checksums, connexion de l'application de test pour valider les requêtes fonctionnelles, et mesure du temps total de restauration. Les résultats sont systématiquement documentés dans un ticket de suivi avec identification des axes d'amélioration éventuels.

### 2.5 Monitoring et alerting

La surveillance automatique des sauvegardes couvre plusieurs dimensions critiques. Chaque échec de backup déclenche une alerte immédiate sur le canal Slack #ops, avec escalade automatique si le problème n'est pas résolu dans les 15 minutes. La durée des opérations de backup est également surveillée : un dépassement de 4 heures indique un problème de performance nécessitant investigation. Des variations soudaines de taille (plus de 50% d'écart) alertent sur une possible corruption ou anomalie fonctionnelle.

L'espace disque disponible pour les archives WAL fait l'objet d'une surveillance particulière car son épuisement bloquerait toute nouvelle transaction. Un seuil d'alerte est fixé à 80% d'utilisation pour permettre une intervention préventive. Enfin, l'âge du dernier backup réussi est vérifié en continu : un délai supérieur à 25 heures sans backup valide déclenche une alerte critique avec notification du CTO.

---

## 3. Plan de Continuité d'Activité (PCA)

### 3.1 Philosophie et objectifs

Le Plan de Continuité d'Activité intervient lors d'incidents de gravité intermédiaire qui dégradent les performances ou la disponibilité du service sans pour autant le rendre totalement inutilisable. L'objectif n'est pas de maintenir une qualité de service parfaite pendant ces périodes, ce qui serait irréaliste, mais de préserver les fonctionnalités essentielles permettant aux utilisateurs de continuer leur travail avec des limitations acceptables. Cette approche pragmatique reconnaît qu'un mode dégradé contrôlé vaut mieux qu'une indisponibilité complète.

Le PCA définit plusieurs niveaux de fonctionnement selon la sévérité de l'incident. En mode dégradé léger, toutes les fonctionnalités restent accessibles mais avec une latence accrue et une capacité réduite à environ 50% de la charge normale. En mode dégradé sévère, seules les fonctionnalités critiques sont maintenues (authentification, consultation de projets et tâches) tandis que les fonctions secondaires (notifications, exports, chatbot IA) sont temporairement désactivées. Le temps de basculement vers un mode dégradé ne doit pas excéder 30 minutes depuis la détection de l'incident.

### 3.2 Classification des services par criticité

Tous les services de la plateforme ne se valent pas en termes d'importance business. L'authentification via Keycloak et la consultation des données projets/tâches sont classées comme critiques : leur indisponibilité rend le service complètement inutilisable. Ces fonctions bénéficient de mécanismes de fallback sophistiqués comme un cache local d'authentification permettant une autonomie de 1 heure et un mode lecture seule de l'API avec extension du cache.

Les services importants comme la création/modification de tâches et les notifications ne sont pas strictement indispensables sur de courtes périodes. En cas d'incident, ces opérations peuvent être mises en file d'attente asynchrone avec un traitement différé, ou même temporairement désactivées si le mode dégradé doit se prolonger. Les services standards (chatbot IA, génération de rapports) et non-critiques (landing page) peuvent être arrêtés sans impact significatif sur l'activité principale des utilisateurs.

| Criticité | Services | Mode dégradé | Arrêt acceptable |
|-----------|----------|--------------|------------------|
| **Critique** | Authentification, Consultation projets/tâches | Cache local 1h, Read-only | Non |
| **Important** | Écriture API, Notifications | Queue différée | Temporaire (< 4h) |
| **Standard** | Chatbot IA, Exports/rapports | Désactivation | Oui |
| **Facultatif** | Landing page | Message maintenance | Oui |

### 3.3 Architecture redondante et basculement

La résilience du PCA repose sur une infrastructure géographiquement distribuée avec redondance à plusieurs niveaux. Le load balancer (AWS ALB ou Azure Traffic Manager) surveille la santé de chaque instance d'application via des health checks réguliers. Si une instance répond avec des erreurs ou présente une latence excessive, elle est automatiquement retirée du pool de routage et le trafic est redistribué sur les instances saines. Ce mécanisme de basculement automatique intervient typiquement en moins d'une minute sans intervention humaine.

La base de données PostgreSQL maintient en permanence un réplica en streaming dans une région secondaire, synchronisé avec quelques secondes de décalage en conditions normales. Ce réplica fonctionne en lecture seule, permettant d'absorber une partie des requêtes de consultation et de réduire la charge sur la base primaire. En cas d'indisponibilité de la région primaire, le réplica peut être promu en maître avec une fenêtre d'intervention de 15 à 30 minutes incluant validation de l'état des données et reconfiguration des applications.

### 3.4 Communication de crise

La gestion d'un incident ne se limite pas aux aspects techniques : la communication transparente avec les utilisateurs est cruciale pour maintenir la confiance. Dès qu'un incident est détecté et confirmé (moins de 5 minutes après déclenchement), une notification est publiée sur la status page publique avec le statut "Investigating". Cette première communication reconnaît le problème et informe les utilisateurs que l'équipe technique est mobilisée.

Si l'incident nécessite l'activation d'un mode dégradé, une mise à jour détaille précisément les fonctionnalités affectées et celles qui restent disponibles, avec une estimation de durée de résolution. Les clients Enterprise bénéficient d'une communication directe par email dans les 15 minutes. Enfin, lorsque le service est restauré, un message de résolution indique la durée totale d'incident, l'impact constaté, et l'engagement de publier un post-mortem détaillé dans les 48 heures suivantes. Cette transparence post-incident transforme chaque problème en opportunité d'amélioration documentée.

---

## 4. Plan de Reprise d'Activité (PRA)

### 4.1 Déclenchement et scénarios

Le Plan de Reprise d'Activité représente le niveau ultime de réponse face à un sinistre majeur rendant l'infrastructure primaire totalement inutilisable pour une durée indéterminée. Son activation n'est pas une décision technique de routine mais une décision stratégique prise conjointement par le CTO et la Direction Générale, car elle implique des coûts significatifs et une fenêtre d'indisponibilité incompressible de plusieurs heures.

Les scénarios déclenchant le PRA incluent la destruction physique d'un datacenter (catastrophe naturelle, incendie majeur), une cyberattaque de type ransomware ayant chiffré les systèmes primaires et nécessitant une reconstruction complète, une corruption massive des données sans possibilité de réparation, ou l'indisponibilité prolongée d'une région cloud entière chez le fournisseur. Le critère décisionnel principal est simple : si l'indisponibilité prévisible dépasse 2 heures sans perspective de résolution rapide, ou si la sécurité des données est compromise de manière irréversible, le PRA est activé.

### 4.2 Site de secours et synchronisation

Le site de secours est une infrastructure miroir maintenue en permanence dans une région géographiquement distincte (Milan pour le secondaire, Paris pour le primaire), distantes de plus de 500 kilomètres pour limiter les risques de sinistre commun. Cette infrastructure secondaire n'est pas une simple sauvegarde froide mais un environnement actif recevant en continu les réplications de données et maintenant des images applicatives pré-déployées, prêtes à être activées.

La base de données secondaire fonctionne comme un réplica en streaming synchronisé en quasi-temps réel avec la base primaire. Le décalage typique (lag) est inférieur à 30 secondes en conditions normales, pouvant atteindre 5 minutes lors de pics de charge. Les fichiers utilisateurs sur S3 bénéficient de la réplication cross-region automatique avec un délai maximal de 15 minutes. Cette synchronisation continue garantit que le site de secours dispose toujours de données récentes, minimisant la perte potentielle lors d'un basculement d'urgence.

### 4.3 Procédure de reprise en quatre phases

La mise en œuvre du PRA suit un protocole structuré en quatre phases distinctes avec des objectifs temporels clairs. La phase 1 (0 à 30 minutes) concerne l'activation et la mobilisation : déclaration formelle du PRA, convocation de la cellule de crise en war room, évaluation de la situation et des causes, publication de la communication préalable informant tous les clients de l'incident majeur en cours. Cette phase établit le cadre organisationnel et communicationnel nécessaire à la suite des opérations.

La phase 2 (30 minutes à 1h30) prépare l'environnement de secours : vérification de la santé de l'infrastructure secondaire, promotion du réplica PostgreSQL en mode lecture/écriture, validation de l'intégrité des données restaurées par comparaison avec les dernières métriques connues, reconfiguration des services applicatifs avec les nouvelles coordonnées de connexion, et activation du cluster Keycloak secondaire avec restauration de sa base de données dédiée.

La phase 3 (1h30 à 3h) bascule le trafic vers le site de secours : modification des enregistrements DNS pour pointer vers les nouvelles adresses IP (avec TTL court de 2 minutes pour propagation rapide), exécution d'une suite de tests fonctionnels critiques couvrant l'authentification et les opérations CRUD essentielles, validation des performances avec objectif de temps de réponse inférieur à 500ms en percentile 95, et activation complète du monitoring sur l'environnement de reprise.

La phase 4 (3h à 4h) ouvre progressivement le service : retrait de la page de maintenance, activation de rate limiting prudent à 50% de capacité pour limiter les risques, surveillance intensive par toute l'équipe technique, communication de restauration sur tous les canaux, et montée en charge graduelle vers 100% de capacité sur 4 à 8 heures selon la stabilité observée.

### 4.4 Retour à la normale

Le retour vers l'infrastructure primaire après résolution du sinistre initial n'est pas moins critique que l'activation du PRA. Il nécessite un minimum de 24 heures de stabilité complète sur le site de secours et la résolution confirmée de la cause racine de l'incident. La reconstruction du site primaire peut prendre de 2 à 5 jours selon l'ampleur des dégâts, incluant reprovisionnement de l'infrastructure, restauration des configurations depuis les backups, et synchronisation complète des données depuis le site de reprise.

Le basculement retour s'effectue lors d'une fenêtre de maintenance planifiée et communiquée 24 heures à l'avance aux clients. Durant cette fenêtre de moins d'une heure, le site de secours passe en mode lecture seule, une synchronisation finale des données vers le site primaire est effectuée, la base primaire est promue en mode écriture, la réplication est inversée (primaire vers secondaire), et le DNS est basculé progressivement. L'équipe reste mobilisée en surveillance intensive pendant 48 heures suivant le retour pour détecter toute anomalie éventuelle.

### 4.5 Post-mortem obligatoire

Chaque activation du PRA fait obligatoirement l'objet d'un rapport post-mortem détaillé publié dans les 48 heures suivant le retour à la normale. Ce document constitue un actif stratégique d'apprentissage organisationnel analysant la cause racine de l'incident, les facteurs contributifs, le déroulement chronologique précis des événements, l'efficacité de la réponse apportée avec identification des points forts et des difficultés rencontrées, et surtout la liste exhaustive des mesures correctives à court et long terme.

Le post-mortem est partagé en version complète avec l'équipe technique et la direction, en version résumée avec les clients Enterprise (focus sur l'impact et les garanties de non-récurrence), et en version communication publique sur le blog et la status page (transparence sur l'incident et engagement d'amélioration). Cette approche de transparence radicale transforme chaque crise en opportunité de renforcer la confiance des clients par la demonstration d'une culture d'amélioration continue.

---

## 5. Organisation et gouvernance

### 5.1 Rôles et responsabilités

La gestion de la continuité d'activité repose sur une organisation clairement définie avec des rôles et responsabilités sans ambiguïté. Le CTO assume la responsabilité globale de la stratégie PCA/PRA, des décisions budgétaires associées, et des décisions d'activation lors d'incidents majeurs. Le Lead DevOps coordonne les aspects opérationnels au quotidien : maintenance des procédures, organisation et supervision des tests réguliers, formation de l'équipe.

Le Database Administrator (DBA) porte la responsabilité technique des sauvegardes et restaurations de bases de données, de la supervision de la réplication, et de l'optimisation des performances. Le RSSI (Responsable Sécurité des Systèmes d'Information) veille aux aspects sécurité et conformité réglementaire. Le VP Customer Success gère la communication externe vers les clients pendant les incidents. Chaque rôle dispose d'un backup désigné pour garantir une couverture 24/7, l'astreinte technique tournant sur une base hebdomadaire entre les membres de l'équipe DevOps.

### 5.2 Comité de pilotage et astreintes

Un comité de pilotage trimestriel réunit CTO, Lead DevOps, DBA, RSSI, VP Customer Success et CFO pour examiner les incidents du trimestre écoulé, analyser les résultats des tests PRA, réviser les indicateurs RTO/RPO effectifs, ajuster les budgets et investissements nécessaires, intégrer les évolutions réglementaires, et mettre à jour les procédures. Ce forum stratégique assure que la résilience reste une priorité alignée avec les objectifs business.

L'organisation des astreintes garantit une capacité de réaction 24/7 avec une rotation hebdomadaire incluant un DevOps on-call primaire, un DevOps backup pour escalade, et un DBA disponible via PagerDuty. Les outils d'astreinte incluent alerting automatique avec escalade, canal Slack dédié #ops-oncall pour coordination, runbook documenté dans Confluence avec toutes les procédures standard, et accès VPN sécurisé à l'infrastructure de production. Une compensation financière (prime d'astreinte) et en temps de récupération est prévue pour reconnaître cette disponibilité étendue.

---

## 6. Amélioration continue

### 6.1 Programme de tests structuré

La fiabilité des plans de continuité ne peut être présumée : elle doit être prouvée régulièrement par des tests réels. Un programme structuré définit plusieurs niveaux de tests avec fréquences adaptées. Les tests hebdomadaires de restauration d'un fichier individuel, réalisés par le DevOps d'astreinte en 15 minutes, valident les procédures de base. Les tests mensuels de restauration complète de base de données, impliquant DBA et DevOps sur 2 heures, mesurent les RTO/RPO effectifs et identifient les points d'optimisation.

Les tests trimestriels simulent un basculement complet vers la région secondaire avec mobilisation de toute l'équipe technique sur 4 heures, validant l'infrastructure redondante et la coordination d'équipe. Les simulations semestrielles de PRA complet engagent toute l'entreprise (technique, communication, direction) sur 8 heures dans un exercice réaliste incluant les aspects communication clients. Enfin, un exercice annuel de type "tabletop" réunit direction et équipe technique pour un jeu de rôle d'incident majeur, testant la prise de décision stratégique sans exécution technique.

### 6.2 Indicateurs et culture d'amélioration

Le suivi d'indicateurs clés permet de mesurer objectivement la maturité de la résilience. Le MTBF (Mean Time Between Failures, temps moyen entre pannes) cible plus de 30 jours, le MTTR (Mean Time To Repair, temps moyen de résolution) vise moins d'une heure, et les RTO/RPO effectifs mesurés lors des tests sont comparés aux objectifs. La disponibilité mensuelle cible 99,9% et le taux de réussite des backups 99,95%. Ces métriques sont suivies sur des dashboards Grafana avec alertes automatiques en cas de dégradation.

Chaque incident, quel que soit sa gravité, fait l'objet d'une revue post-incident obligatoire dans les 48 heures avec analyse cause racine (méthode 5 Why), évaluation de l'efficacité de la réponse, identification d'actions correctives, et mise à jour de la documentation. Cette culture de l'apprentissage par l'échec transforme chaque problème en opportunité d'amélioration. Un plan d'évolution pluriannuel structure les investissements : automatisation complète des tests de backup en Q2 2026, implémentation de chaos engineering régulier en Q3, certification ISO 22301 en Q4, et déploiement d'un troisième site de reprise en Asie à long terme.

---

**Dernière mise à jour** : 27 février 2026  
**Validé par** : CTO + Direction Générale  
**Prochaine revue** : Mai 2026 (trimestriel)

**Niveau de classification** : 🔴 **CONFIDENTIEL - Usage interne uniquement**
