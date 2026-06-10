# 🏷️ Référence des Labels - Taskforce

Liste complète et détaillée de tous les labels GitHub utilisés dans le projet.

---

## 📚 Table des matières

- [Labels Release (OBLIGATOIRES)](#labels-release-obligatoires)
- [Labels Type](#labels-type)
- [Labels Composants](#labels-composants)
- [Labels Priorité](#labels-priorité)
- [Labels Status](#labels-status)
- [Labels Epics](#labels-epics)
- [Import Automatique](#import-automatique)

---

## 📦 Labels Release (OBLIGATOIRES)

Ces labels sont **OBLIGATOIRES** sur chaque Pull Request. Un seul label de cette catégorie doit être présent.

### `release:major`
- **Couleur** : 🔴 `#d73a4a`
- **Description** : Breaking changes - Incrémente MAJOR (v1.0.0 → v2.0.0)
- **Usage** : Changements incompatibles avec la version précédente
- **Exemples** :
  - Modification de l'API publique
  - Suppression de fonctionnalités
  - Changement de structure de base de données incompatible
  - Migration vers une nouvelle architecture

### `release:minor`
- **Couleur** : 🟢 `#0e8a16`
- **Description** : New features - Incrémente MINOR (v1.0.0 → v1.1.0)
- **Usage** : Nouvelles fonctionnalités rétro-compatibles
- **Exemples** :
  - Nouvelle page ou composant
  - Nouveau endpoint API
  - Nouvelle feature majeure
  - Ajout de fonctionnalités

### `release:patch`
- **Couleur** : 🟡 `#fbca04`
- **Description** : Bug fixes - Incrémente PATCH (v1.0.0 → v1.0.1)
- **Usage** : Corrections de bugs rétro-compatibles
- **Exemples** :
  - Correction de bugs
  - Amélioration de performance
  - Refactoring interne
  - Hotfix

---

## 🎯 Labels Type

Labels optionnels pour catégoriser le type de changement.

### `type:feature`
- **Couleur** : `#a2eeef`
- **Description** : Nouvelle fonctionnalité
- **Usage** : PR ajoutant une nouvelle feature
- **Combine avec** : Généralement `release:minor`

### `type:bugfix`
- **Couleur** : `#d73a4a`
- **Description** : Correction de bug
- **Usage** : PR corrigeant un bug
- **Combine avec** : Généralement `release:patch`

### `type:hotfix`
- **Couleur** : `#b60205`
- **Description** : Hotfix urgent en production
- **Usage** : PR pour correction urgente (vers `main`)
- **Combine avec** : `release:patch` + `priority:critical`

### `type:refactor`
- **Couleur** : `#fbca04`
- **Description** : Refactoring de code
- **Usage** : PR de refactoring interne
- **Combine avec** : Généralement `release:patch`

### `type:test`
- **Couleur** : `#1d76db`
- **Description** : Ajout ou modification de tests
- **Usage** : PR ajoutant/modifiant des tests
- **Combine avec** : `release:patch`

### `type:ci/cd`
- **Couleur** : `#ededed`
- **Description** : CI/CD et DevOps
- **Usage** : PR modifiant les workflows, Docker, etc.
- **Combine avec** : `release:patch`

### Labels Existants à Conserver

- **`bug`** - `#d73a4a` - Something isn't working
- **`enhancement`** - `#a2eeef` - New feature or request
- **`documentation`** - `#0075ca` - Improvements or additions to documentation

---

## 🧩 Labels Composants

Labels pour identifier quelle partie du projet est affectée.

### `backend`
- **Couleur** : `#5319e7`
- **Description** : Backend / API
- **Usage** : Changements dans l'API Spring Boot

### `frontend`
- **Couleur** : `#0052cc`
- **Description** : Frontend / UI
- **Usage** : Changements dans le frontend Next.js

### `database`
- **Couleur** : `#c5def5`
- **Description** : Database related
- **Usage** : Changements de schéma, migrations Flyway

### `infra`
- **Couleur** : `#ededed`
- **Description** : Infrastructure & DevOps
- **Usage** : Docker, Nginx, Keycloak, CI/CD

### `security`
- **Couleur** : `#b60205`
- **Description** : Sécurité
- **Usage** : Corrections de sécurité, vulnérabilités

### `performance`
- **Couleur** : `#fbca04`
- **Description** : Performance optimization
- **Usage** : Optimisations de performance

---

## ⚡ Labels Priorité

Labels pour indiquer l'urgence de la PR.

### `priority:critical`
- **Couleur** : `#b60205`
- **Description** : Critique - À traiter immédiatement
- **Usage** : Bugs critiques, failles de sécurité, production down
- **SLA** : Traitement immédiat

### `priority:high`
- **Couleur** : `#d93f0b`
- **Description** : Haute - À traiter rapidement
- **Usage** : Bugs importants, features urgentes
- **SLA** : 24-48h

### `priority:medium`
- **Couleur** : `#fbca04`
- **Description** : Moyenne - À traiter normalement
- **Usage** : Features normales, bugs mineurs
- **SLA** : 1 semaine

### `priority:low`
- **Couleur** : `#0e8a16`
- **Description** : Basse - Quand possible
- **Usage** : Nice to have, refactoring non-urgent
- **SLA** : Quand disponible

---

## 📊 Labels Status

Labels pour indiquer l'état de la PR.

### `status:ready-for-review`
- **Couleur** : `#0e8a16`
- **Description** : Prêt pour review
- **Usage** : PR prête à être reviewée
- **Action** : Assigner des reviewers

### `status:in-progress`
- **Couleur** : `#fbca04`
- **Description** : En cours de développement
- **Usage** : PR en draft ou en cours de développement
- **Action** : Ne pas merger

### `status:blocked`
- **Couleur** : `#d73a4a`
- **Description** : Bloqué - Nécessite intervention
- **Usage** : PR bloquée par un problème externe
- **Action** : Résoudre le blocage

### `status:needs-info`
- **Couleur** : `#d876e3`
- **Description** : Informations manquantes
- **Usage** : PR nécessitant des clarifications
- **Action** : Auteur doit fournir des infos

### `status:on-hold`
- **Couleur** : `#ededed`
- **Description** : En attente
- **Usage** : PR mise en pause temporairement
- **Action** : Attendre décision

---

## 📁 Labels Epics

Labels pour regrouper les PR par epic/feature majeure.

### `epic:admin`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Admin
- **Usage** : Fonctionnalités d'administration

### `epic:auth`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Authentication
- **Usage** : Authentification, autorisation

### `epic:dashboard`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Dashboard
- **Usage** : Tableaux de bord

### `epic:notifications`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Notifications
- **Usage** : Système de notifications

### `epic:projects`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Projects
- **Usage** : Gestion de projets

### `epic:tasks`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Tasks
- **Usage** : Gestion de tâches

### `epic:teams`
- **Couleur** : `#3e4b9e`
- **Description** : Epic Teams
- **Usage** : Gestion d'équipes

---

## 📥 Import Automatique

### Fichier de Configuration

Le fichier [`.github/labels.yml`](../../../../taskforce-fullstack/.github/labels.yml) contient tous les labels.

### Méthode 1 : GitHub CLI (Recommandé)

```bash
# Naviguer vers le projet
cd taskforce-fullstack

# Importer tous les labels
gh label create -f .github/labels.yml
```

### Méthode 2 : Import Manuel

Voir le [Guide de Setup](./setup.md#étape-3--importer-les-labels) pour la liste complète des commandes.

### Vérifier les Labels

```bash
# Lister tous les labels
gh label list

# Lister par catégorie
gh label list | grep "release:"
gh label list | grep "type:"
gh label list | grep "priority:"
```

---

## 🎯 Exemples d'Usage

### Feature Importante

```bash
gh pr create \
  --base dev \
  --title "feat: user profile page" \
  --label "release:minor" \
  --label "type:feature" \
  --label "frontend" \
  --label "epic:admin" \
  --label "priority:high"
```

### Bug Fix Simple

```bash
gh pr create \
  --base dev \
  --title "fix: login timeout" \
  --label "release:patch" \
  --label "type:bugfix" \
  --label "backend" \
  --label "priority:medium"
```

### Hotfix Critique

```bash
gh pr create \
  --base main \
  --title "fix: critical security vulnerability" \
  --label "release:patch" \
  --label "type:hotfix" \
  --label "security" \
  --label "priority:critical"
```

### Refactoring

```bash
gh pr create \
  --base dev \
  --title "refactor: extract user service" \
  --label "release:patch" \
  --label "type:refactor" \
  --label "backend" \
  --label "priority:low"
```

---

## ✅ Best Practices

### 1. Labels Obligatoires

**Toujours** ajouter :
- ✅ Un label `release:*` (obligatoire)
- ✅ Un label `type:*` (recommandé)
- ✅ Un ou plusieurs labels de composants

### 2. Combinaisons Recommandées

| Type de PR | Labels suggérés |
|------------|----------------|
| **Nouvelle feature** | `release:minor` + `type:feature` + composant + epic |
| **Bug fix** | `release:patch` + `type:bugfix` + composant + priorité |
| **Hotfix** | `release:patch` + `type:hotfix` + `priority:critical` + composant |
| **Refactoring** | `release:patch` + `type:refactor` + composant |
| **Tests** | `release:patch` + `type:test` + composant |
| **CI/CD** | `release:patch` + `type:ci/cd` + `infra` |

### 3. Cohérence

Soyez cohérent dans l'utilisation des labels pour faciliter le filtrage et les statistiques.

---

## 📚 Ressources

- [Setup Initial](./setup.md)
- [Git Workflow](./README.md)
- [Pull Requests](./pull-requests.md)
- [GitHub Labels Documentation](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels)

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
