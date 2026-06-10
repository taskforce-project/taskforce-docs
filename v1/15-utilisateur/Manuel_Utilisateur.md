---
type: documentation-utilisateur
statut: draft
version: 0.1
date: "08/06/2026"
auteur: Pierre MICHEL
tags: [utilisateur, manuel, guide]
---
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Manuel Utilisateur — TaskForce

**Version :** 0.1  
**Date :** 08/06/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Documentation Utilisateur](https://img.shields.io/badge/Type-Documentation%20Utilisateur-green?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Public: Utilisateurs finaux](https://img.shields.io/badge/Public-Utilisateurs-lightgrey?style=for-the-badge)]()

## Liens rapides

- [🧠 Brain OS](../../Brain_OS.md)
- [Guide d'installation](./Guid_Installation.md)
- [FAQ](./FAQ.md)
- [Release Notes](./Release_Notes.md)

**Tags :** `#utilisateur` `#manuel` `#guide`

<p class="lead">
TaskForce est un outil de gestion de projet et de <strong>répartition dynamique des tâches</strong> :
il assigne les tâches selon les compétences, la charge de travail et les disponibilités de chacun. Ce
manuel guide les trois profils d'utilisateurs — le Collaborateur, le Manager et le Responsable de projet —
dans l'usage quotidien de l'application.
</p>

> 🖼️ _Insérer des captures d'écran depuis_ `assets/maquettes/` _au fil des sections._

## Table des matières

1. [Premiers pas](#1-premiers-pas)
2. [Rôles & permissions](#2-rôles--permissions)
3. [Espaces de travail (workspaces)](#3-espaces-de-travail-workspaces)
4. [Projets](#4-projets)
5. [Tâches (issues)](#5-tâches-issues)
6. [Cycles & roadmap](#6-cycles--roadmap)
7. [Collaboration](#7-collaboration)
8. [Notifications & inbox](#8-notifications--inbox)
9. [Analytics & assistance IA](#9-analytics--assistance-ia)
10. [Compte, profil & facturation](#10-compte-profil--facturation)

---

## 1. Premiers pas

<p class="lead">Création de compte, vérification et première connexion.</p>

- **Inscription** (3 étapes) : informations → choix du plan → vérification par code OTP (email).
- **Connexion** : email + mot de passe.
- **Mot de passe oublié** : réinitialisation par code OTP.

> _À rédiger :_ <!-- captures du parcours auth, durée de validité de l'OTP, dépannage -->

## 2. Rôles & permissions

| Rôle (CDC) | Dans TaskForce | Peut faire |
| ---------- | -------------- | ---------- |
| Collaborateur | Membre | Reçoit/traite ses tâches selon compétences et charge |
| Manager | Admin de workspace | Suit la progression, ajuste priorités, reçoit les alertes de surcharge |
| Responsable de projet | Lead de projet | Définit compétences requises, priorités, allocation initiale |

> _À rédiger :_ <!-- tableau détaillé des permissions par rôle (WorkspaceRole, ProjectRole) -->

## 3. Espaces de travail (workspaces)

> _À rédiger :_ <!-- créer/rejoindre un workspace, inviter des membres, gérer les rôles, paramètres -->

## 4. Projets

> _À rédiger :_ <!-- créer un projet, membres, labels, statuts d'issue personnalisés, archivage -->

## 5. Tâches (issues)

<p class="lead">Cœur de l'application : créer, prioriser, assigner et suivre les tâches.</p>

- Création d'une tâche (titre, description, type, priorité, assigné, labels, échéances).
- Statuts (Backlog → To do → In progress → In review → Done) et tableau Kanban / liste / backlog.
- Commentaires, activité, relations entre tâches, pièces jointes.
- **Smart Assign (IA)** : suggestion d'assignation selon compétences, charge et disponibilités.

> _À rédiger :_ <!-- captures Kanban, fiche tâche, usage du Smart Assign -->

## 6. Cycles & roadmap

> _À rédiger :_ <!-- cycles/sprints (création, ajout de tâches, suivi), vue roadmap (dates) -->

## 7. Collaboration

> _À rédiger :_ <!-- messagerie/canaux (chat temps réel), discussions/forum, pages wiki, équipes -->

## 8. Notifications & inbox

> _À rédiger :_ <!-- inbox (mentions, assignations, alertes de surcharge), marquage lu/accusé -->

## 9. Analytics & assistance IA

> _À rédiger :_ <!-- tableau de bord (KPIs, burndown, throughput, capacité), AI Insights, assistant -->

## 10. Compte, profil & facturation

> _À rédiger :_ <!-- profil (stats, avatar), préférences (thème), plans FREE/PRO/ENTERPRISE, paiement -->

---

<blockquote class="important">
<strong>Note interne (à retirer en version publique) :</strong> certains modules sont en cours de
finalisation (cf. <a href="../09-audits/Problemes_Connus.md">Problèmes connus</a>). Documenter ici
uniquement les fonctionnalités effectivement opérationnelles au moment de la release.
</blockquote>

**Dernière mise à jour :** 08/06/2026  
**Version :** 0.1  
**Projet :** Taskforce — Metz Numeric School 2025-2026
