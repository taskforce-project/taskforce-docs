# Plan de Sécurité - PCA / PRA

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_light.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Introduction](#1-introduction)
- [2. Politique de Sécurité (PSSI)](#2-politique-de-sécurité-pssi)
- [3. Analyse des Risques](#3-analyse-des-risques)
- [4. Mesures de Prévention](#4-mesures-de-prévention)
- [5. Plan de Continuité d'Activité (PCA)](#5-plan-de-continuité-dactivité-pca)
- [6. Plan de Reprise d'Activité (PRA)](#6-plan-de-reprise-dactivité-pra)
- [7. Gestion des Incidents](#7-gestion-des-incidents)

---

## 1. Introduction
Ce document définit la stratégie de sécurité de l'application **TaskForce**, ainsi que les procédures garantissant la continuité et la reprise des services en cas d'incident majeur. Il vise à assurer la disponibilité, l'intégrité, la confidentialité et la traçabilité (DICP) des données.

---

## 2. Politique de Sécurité (PSSI)

### 2.1 Objectifs de Sécurité (DICP)
*   **Disponibilité** : Le service doit être accessible 99.9% du temps sur les heures ouvrées.
*   **Intégrité** : Les données (tâches, compétences) ne doivent pas être altérées par des tiers non autorisés ou des erreurs système.
*   **Confidentialité** : Les données personnelles (performances, charge de travail) sont strictement réservées aux managers concernés et à l'administrateur.
*   **Preuve/Traçabilité** : Toutes les actions critiques (assignation, suppression, modification de droits) sont loguées.

### 2.2 Classification des Données
*   **Publique** : Aucune.
*   **Interne** : Structure des projets, listes de tâches génériques.
*   **Confidentielle** : Données personnelles des collaborateurs, évaluations de compétences, stratégie d'entreprise.
*   **Critique** : Mots de passe (hashés), clés API, certificats SSL.

---

## 3. Analyse des Risques

| Menace | Impact | Probabilité | Niveau de Risque | Conséquences |
| :--- | :--- | :--- | :--- | :--- |
| **Intrusion / Vol de données** | Critique | Faible | Élevé | Fuite de données RH, perte de confiance, sanctions RGPD. |
| **Attaque DDoS** | Majeur | Moyen | Moyen | Indisponibilité du service, perte de productivité. |
| **Panne Serveur / BDD** | Majeur | Moyen | Moyen | Arrêt de production, perte de données récente. |
| **Erreur Humaine (Suppression)** | Moyen | Élevé | Moyen | Perte de données projet. |
| **Bug Critique (IA)** | Moyen | Moyen | Moyen | Mauvaises assignations, surcharge des équipes. |

---

## 4. Mesures de Prévention

### 4.1 Sécurité Physique et Logique
*   Hébergement sur cloud sécurisé (AWS/Azure/OVH) certifié ISO 27001.
*   Pare-feu (Firewall) et WAF (Web Application Firewall) en amont.
*   Mise à jour régulière des OS et des dépendances (Patch Management).

### 4.2 Sécurité Applicative
*   Revue de code systématique (Code Review) axée sécurité.
*   Scan de vulnérabilités automatisé (SAST/DAST) dans la CI/CD.
*   Principe de moindre privilège pour les accès BDD et API.

### 4.3 Sauvegardes (Backup)
*   **Fréquence** :
    *   Base de données : Complète quotidienne (J-1 à J-7), Incrémentale toutes les heures.
    *   Fichiers de configuration : À chaque modification (Git).
*   **Stockage** : Sur un site distant (Géoredondance) et chiffré.
*   **Test** : Test de restauration mensuel obligatoire.

---

## 5. Plan de Continuité d'Activité (PCA)
*Objectif : Maintenir le service fonctionnel en mode dégradé lors d'un incident.*

### 5.1 Architecture Haute Disponibilité (Cible)
*   Redondance des serveurs d'application (Load Balancing).
*   Base de données en mode Maître/Esclave (Replication).

### 5.2 Mode Dégradé
En cas de panne du **Service IA** :
1.  L'application bascule automatiquement en mode "Manuel".
2.  Les managers reçoivent une notification.
3.  L'assignation des tâches reste possible manuellement.
4.  Les fonctionnalités de reporting et de CRUD restent actives.

---

## 6. Plan de Reprise d'Activité (PRA)
*Objectif : Remettre le service en route après un arrêt total.*

### 6.1 Indicateurs Cibles
*   **RTO (Recovery Time Objective)** : Temps maximal d'interruption toléré = **4 heures**.
*   **RPO (Recovery Point Objective)** : Perte de données maximale tolérée = **1 heure** (dernière sauvegarde incrémentale).

### 6.2 Procédure de Reprise (Scénario : Crash Total BDD)
1.  **Diagnostic** : Confirmation de la perte de la base de données principale.
2.  **Communication** : Notification aux utilisateurs (Email/Slack) de l'indisponibilité.
3.  **Basculement** : Activation de la base de données de secours (Replica) OU Restauration du dernier dump valide sur une nouvelle instance.
4.  **Vérification** : Contrôle de l'intégrité des données par l'équipe technique.
5.  **Relance** : Redémarrage des services Back-end connectés à la nouvelle BDD.
6.  **Retour à la normale** : Notification de fin d'incident.

---

## 7. Gestion des Incidents

### 7.1 Processus d'Escalade
1.  **Niveau 1 (Support)** : Qualification de l'incident.
2.  **Niveau 2 (Dev/Ops)** : Analyse technique et résolution.
3.  **Niveau 3 (Expert/CTO)** : Gestion de crise majeure.

### 7.2 Post-Mortem
Après tout incident critique, une réunion "Post-Mortem" est organisée pour :
*   Analyser les causes racines (Root Cause Analysis).
*   Évaluer l'efficacité de la réponse.
*   Mettre à jour le PCA/PRA et les procédures pour éviter la récidive.
