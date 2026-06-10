# 🏷️ Gestion des Versions - Taskforce

Documentation complète sur le système de versioning automatique.

---

## 📚 Table des matières

- [Vue d'ensemble](#vue-densemble)
- [Semantic Versioning](#semantic-versioning)
- [Release Candidates](#release-candidates)
- [Règles d'incrémentation](#règles-dincrémentation)
- [Exemples](#exemples)
- [FAQ](#faq)

---

## 🌟 Vue d'ensemble

Le projet Taskforce utilise un système de **versioning sémantique automatisé** :

- ✅ **Automatique** : Les tags sont créés lors du merge de PR
- ✅ **Sémantique** : Suit la spec [SemVer 2.0.0](https://semver.org/)
- ✅ **Release Candidates** : Versions RC sur `dev`, stables sur `main`
- ✅ **Validation** : Vérification automatique des labels

---

## 📦 Semantic Versioning (SemVer)

Format : **`vMAJOR.MINOR.PATCH[-rcX]`**

### Composants

```
v1.2.3-rc4
│ │ │  │ │
│ │ │  │ └─ Release Candidate Number
│ │ │  └─── Release Candidate Flag
│ │ └────── PATCH - Corrections de bugs
│ └──────── MINOR - Nouvelles fonctionnalités
└────────── MAJOR - Breaking changes
```

### Quand incrémenter ?

| Composant | Quand incrémenter | Exemple |
|-----------|-------------------|---------|
| **MAJOR** | Breaking changes incompatibles avec la version précédente | Changement d'API publique, suppression de features |
| **MINOR** | Nouvelles fonctionnalités rétro-compatibles | Nouvelle page, nouveau endpoint, nouvelle feature |
| **PATCH** | Corrections de bugs rétro-compatibles | Fix d'un bug, amélioration de performance, refactoring |

### Exemples de Versions

| Version | Type | Description |
|---------|------|-------------|
| `v1.0.0` | Stable | Première version majeure en production |
| `v1.0.0-rc1` | RC | Premier candidat pour v1.0.0 |
| `v1.0.1` | Stable | Correction de bugs |
| `v1.1.0` | Stable | Ajout de nouvelles features |
| `v2.0.0` | Stable | Breaking changes majeurs |

---

## 🧪 Release Candidates (RC)

### Qu'est-ce qu'un Release Candidate ?

Un **Release Candidate** est une **préversion** destinée aux tests avant la mise en production.

### Caractéristiques

- ✅ **Branche** : Uniquement sur `dev`
- ✅ **Format** : `vX.Y.Z-rcN` (N = numéro du candidat)
- ✅ **Usage** : Tests, validation, déploiement en staging
- ✅ **Stabilité** : Peut contenir des bugs

### Cycle de Vie

```
feature/xxx → PR → dev (v1.0.0-rc1) → tests → fix → dev (v1.0.0-rc2) → ...
                                                                          ↓
                                               ... → dev (v1.0.0-rc5) → PR → main (v1.0.0)
```

### Numérotation RC

Le numéro RC repart à **1** lors d'un changement de version :

```
v1.0.0-rc1 → v1.0.0-rc2 → v1.0.0-rc3
                                    ↓
                          (release:minor ajouté)
                                    ↓
                          v1.1.0-rc1 ← Reset à rc1
```

---

## 📋 Règles d'Incrémentation

### Sur la branche `dev` (Release Candidates)

| Label PR | Action | Exemple |
|----------|--------|---------|
| `release:major` | MAJOR+1, MINOR=0, PATCH=0, RC=1 | `v1.5.3-rc2` → `v2.0.0-rc1` |
| `release:minor` | MINOR+1, PATCH=0, RC=1 | `v1.5.3-rc2` → `v1.6.0-rc1` |
| `release:patch` | PATCH+1, RC=1 | `v1.5.3-rc2` → `v1.5.4-rc1` |
| Aucun label* | RC+1 (même version) | `v1.5.3-rc2` → `v1.5.3-rc3` |

*Note : Un label `release:*` est obligatoire. Si vous voulez juste incrémenter RC, utilisez le même label que la version actuelle.*

### Sur la branche `main` (Versions Stables)

| Label PR | Action | Exemple |
|----------|--------|---------|
| `release:major` | MAJOR+1, MINOR=0, PATCH=0 | `v1.5.3` → `v2.0.0` |
| `release:minor` | MINOR+1, PATCH=0 | `v1.5.3` → `v1.6.0` |
| `release:patch` | PATCH+1 | `v1.5.3` → `v1.5.4` |

**Note** : Sur `main`, les versions n'ont jamais de suffixe `-rc`.

---

## 💡 Exemples Détaillés

### Exemple 1 : Feature Development sur dev

**Contexte** :
- Version actuelle : `v1.0.0-rc1`
- Branche : `feature/user-profile` → PR vers `dev`
- Label : `release:minor`

**Calcul** :
```javascript
major = 1, minor = 0, patch = 0, rc = 1
labels.includes('release:minor') → true

// Action
minor += 1;  // minor = 1
patch = 0;
rc = 1;

nextVersion = `v${1}.${1}.${0}-rc${1}` = "v1.1.0-rc1"
```

**Résultat** : `v1.0.0-rc1` → `v1.1.0-rc1`

---

### Exemple 2 : Bug Fix sur dev

**Contexte** :
- Version actuelle : `v1.1.0-rc1`
- Branche : `fix/login-bug` → PR vers `dev`
- Label : `release:patch`

**Calcul** :
```javascript
major = 1, minor = 1, patch = 0, rc = 1
labels.includes('release:patch') → true

// Action
patch += 1;  // patch = 1
rc = 1;

nextVersion = `v${1}.${1}.${1}-rc${1}` = "v1.1.1-rc1"
```

**Résultat** : `v1.1.0-rc1` → `v1.1.1-rc1`

---

### Exemple 3 : Petite Modification (Incrément RC)

**Contexte** :
- Version actuelle : `v1.1.1-rc1`
- Branche : `chore/update-deps` → PR vers `dev`
- Label : `release:patch`

**Calcul** :
```javascript
major = 1, minor = 1, patch = 1, rc = 1
labels.includes('release:patch') → true

// Action
patch += 1;  // patch = 2
rc = 1;

nextVersion = `v${1}.${1}.${2}-rc${1}` = "v1.1.2-rc1"
```

**Résultat** : `v1.1.1-rc1` → `v1.1.2-rc1`

**Alternative** : Si vous voulez juste `v1.1.1-rc2`, créez une PR sans changement de version majeure/mineure/patch et le système incrémentera automatiquement RC.

---

### Exemple 4 : Release Stable (dev → main)

**Contexte** :
- Version actuelle sur `dev` : `v1.1.0-rc5`
- Version actuelle sur `main` : `v1.0.0`
- Branche : `release/1.1.0` (merge de dev) → PR vers `main`
- Label : `release:minor`

**Calcul** :
```javascript
major = 1, minor = 0, patch = 0  // Depuis main
labels.includes('release:minor') → true

// Action
minor += 1;  // minor = 1
patch = 0;

nextVersion = `v${1}.${1}.${0}` = "v1.1.0"  // Pas de -rc
```

**Résultat** : `v1.0.0` → `v1.1.0`

---

### Exemple 5 : Breaking Change

**Contexte** :
- Version actuelle : `v1.5.3-rc2`
- Branche : `feature/api-v2` → PR vers `dev`
- Label : `release:major`

**Calcul** :
```javascript
major = 1, minor = 5, patch = 3, rc = 2
labels.includes('release:major') → true

// Action
major += 1;  // major = 2
minor = 0;
patch = 0;
rc = 1;

nextVersion = `v${2}.${0}.${0}-rc${1}` = "v2.0.0-rc1"
```

**Résultat** : `v1.5.3-rc2` → `v2.0.0-rc1`

---

### Exemple 6 : Hotfix en Production

**Contexte** :
- Version actuelle sur `main` : `v1.0.0`
- Branche : `hotfix/critical-bug` → PR vers `main`
- Label : `release:patch`

**Calcul** :
```javascript
major = 1, minor = 0, patch = 0
labels.includes('release:patch') → true

// Action
patch += 1;  // patch = 1

nextVersion = `v${1}.${0}.${1}` = "v1.0.1"
```

**Résultat** : `v1.0.0` → `v1.0.1`

**⚠️ Important** : Après le merge sur `main`, reporter le fix sur `dev` !

---

## 🔄 Workflow Complet

### Développement Normal

```
1. feature/xxx → PR (release:minor) → dev
   v1.0.0-rc1 → v1.1.0-rc1

2. fix/yyy → PR (release:patch) → dev
   v1.1.0-rc1 → v1.1.1-rc1

3. Tests, corrections...
   fix/zzz → PR (release:patch) → dev
   v1.1.1-rc1 → v1.1.2-rc1

4. Prêt pour prod
   release/1.1.2 (merge dev) → PR (release:minor) → main
   v1.0.0 → v1.1.2
```

### Hotfix Urgent

```
1. hotfix/xxx → PR (release:patch) → main
   v1.1.2 → v1.1.3

2. Reporter sur dev
   git cherry-pick <sha> → dev
   v1.1.2-rc3 → v1.1.3-rc1 (ou manually sync)
```

---

## ❓ FAQ

### Puis-je créer un tag manuellement ?

❌ **Non recommandé**. Les tags sont gérés automatiquement par GitHub Actions. Créer un tag manuel peut casser le système.

### Comment sauter une version (v1.0.0 → v3.0.0) ?

❌ **Impossible**. Le système n'autorise que des incréments de +1 pour éviter les erreurs.

### Que se passe-t-il si j'oublie le label `release:*` ?

La PR sera **bloquée** automatiquement. Il suffit d'ajouter le label pour débloquer.

### Puis-je avoir plusieurs labels `release:*` ?

❌ **Non**. Un seul label `release:*` est autorisé par PR.

### Comment gérer plusieurs modifications mineures ?

Utilisez le même label de version (ex: `release:patch`) pour chaque PR. Le RC sera incrémenté automatiquement :
- `v1.0.0-rc1` → `v1.0.0-rc2` → `v1.0.0-rc3`

### Comment voir toutes les versions ?

```bash
# Lister tous les tags
git tag -l

# Tags RC uniquement
git tag -l "v*-rc*"

# Tags stables uniquement
git tag -l "v*" | grep -v "rc"

# Trier par date
git tag -l --sort=-creatordate
```

### Comment revenir à une version précédente ?

```bash
# Checkout un tag spécifique
git checkout v1.0.0

# Créer une branche depuis un tag
git checkout -b fix/rollback v1.0.0
```

### Les RC sont-ils déployés en production ?

❌ **Non**. Les RC sont pour les environnements de **staging/test** uniquement.  
✅ Seules les versions **stables** (sans `-rc`) sont déployées en production.

---

## 🎯 Best Practices

### 1. Utilisez des labels appropriés

```bash
# Feature importante
release:minor

# Correction de bug
release:patch

# Breaking change
release:major
```

### 2. Testez en RC avant la prod

```
dev (RC) → Tests → Validation → main (Stable)
```

### 3. Documentez les breaking changes

Pour un `release:major`, documentez clairement :
- Quels sont les breaking changes
- Comment migrer depuis la version précédente
- Quelles fonctionnalités sont supprimées/modifiées

### 4. Gardez un CHANGELOG

Mettez à jour un fichier `CHANGELOG.md` avec chaque release :

```markdown
## [1.1.0] - 2026-01-27

### Added
- User profile page
- Avatar upload

### Fixed
- Login timeout after 30 seconds

### Breaking Changes
- None
```

---

## 📚 Ressources

- [Semantic Versioning Spec](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Actions](./github-actions.md)
- [Pull Requests](./pull-requests.md)

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
