# 📋 Pull Requests - Guide Complet

Guide pour créer et gérer les Pull Requests dans le projet Taskforce.

---

## 🎯 Avant de Créer une PR

### Checklist Pré-PR

- [ ] Ma branche est à jour avec `dev`
- [ ] Mon code compile sans erreurs
- [ ] J'ai testé localement
- [ ] J'ai écrit/mis à jour les tests si nécessaire
- [ ] J'ai mis à jour la documentation si nécessaire
- [ ] Mon code suit les conventions du projet

---

## 📝 Créer une Pull Request

### Méthode 1 : Via GitHub CLI (Recommandé)

```bash
# Depuis votre branche
gh pr create \
  --base dev \
  --title "feat: description courte" \
  --body "Description détaillée de vos changements" \
  --label "release:minor" \
  --label "type:feature"
```

**Options** :
- `--base dev` - Branche cible
- `--title` - Titre de la PR (utiliser les [conventions de commit](#conventions-de-commit))
- `--body` - Description (ou `-F file.md` pour un fichier)
- `--label` - Ajouter des labels (répéter pour plusieurs labels)
- `--draft` - Créer en mode brouillon

### Méthode 2 : Via l'Interface GitHub

1. Aller sur le repository GitHub
2. Cliquer **Pull Requests** → **New Pull Request**
3. Sélectionner :
   - **base:** `dev`
   - **compare:** votre branche
4. Cliquer **Create Pull Request**
5. Remplir le template
6. Ajouter les labels appropriés
7. Cliquer **Create Pull Request**

---

## 🏷️ Labels Obligatoires

### ⚠️ Label `release:*` (OBLIGATOIRE)

**Chaque PR DOIT avoir UN ET UN SEUL label de release** :

| Label | Usage | Exemple |
|-------|-------|---------|
| `release:major` | Breaking changes incompatibles | Changement d'API publique |
| `release:minor` | Nouvelles fonctionnalités | Nouvelle page, nouveau endpoint |
| `release:patch` | Corrections de bugs | Fix d'un bug, hotfix |

**❌ Sans label `release:*`** → PR bloquée  
**❌ Plusieurs labels `release:*`** → PR bloquée

### Labels Optionnels (mais recommandés)

#### Type
- `type:feature` - Nouvelle fonctionnalité
- `type:bugfix` - Correction de bug
- `type:refactor` - Refactoring
- `type:test` - Tests
- `type:ci/cd` - CI/CD

#### Composants
- `backend` - Backend / API
- `frontend` - Frontend / UI
- `database` - Base de données
- `infra` - Infrastructure

#### Priorité
- `priority:critical` - Urgent
- `priority:high` - Haute
- `priority:medium` - Moyenne
- `priority:low` - Basse

---

## 📋 Template de PR

Le template se remplit automatiquement. Voici les sections :

### 1. Description

```markdown
## 📋 Description

Ajout d'une page de profil utilisateur avec :
- Avatar uploadable
- Édition des informations personnelles
- Changement de mot de passe
```

### 2. Type de changement

```markdown
## 🏷️ Type de changement

- [x] ✨ New feature (`release:minor`)
- [ ] 🐛 Bug fix (`release:patch`)
- [ ] 💥 Breaking change (`release:major`)
```

### 3. Checklist

```markdown
## ✅ Checklist

- [x] Mon code suit les conventions du projet
- [x] J'ai ajouté les labels appropriés
- [x] J'ai testé localement mes changements
- [x] Les tests passent en local
```

### 4. Issues liées

```markdown
## 🔗 Issues liées

Closes #42
Relates to #35, #36
```

---

## 🤖 Validation Automatique

### Workflow "Version Management"

**Déclenché automatiquement** quand vous :
- Ouvrez une PR
- Pushez un nouveau commit
- Ajoutez/retirez un label

**Actions** :
1. ✅ Vérifie la présence d'un label `release:*`
2. 🔢 Calcule la prochaine version
3. 💬 Poste un commentaire :

```markdown
## 🏷️ Version Bump Preview

**Current version:** `v1.0.0-rc1`
**Next version:** `v1.1.0-rc1`
**Target branch:** `dev`

This version will be tagged automatically when the PR is merged.
```

---

## 🎯 Scénarios Courants

### Scénario 1 : Feature Simple

```bash
# 1. Créer la branche
git checkout dev
git pull origin dev
git checkout -b feature/user-profile

# 2. Développer
# ... code ...
git add .
git commit -m "feat: add user profile page"
git push origin feature/user-profile

# 3. Créer la PR
gh pr create \
  --base dev \
  --title "feat: add user profile page" \
  --label "release:minor" \
  --label "type:feature" \
  --label "frontend"
```

**Résultat** :
- ✅ Bot commente : "Next version: `v1.1.0-rc1`"
- ✅ Après merge : Tag `v1.1.0-rc1` créé

---

### Scénario 2 : Bug Fix

```bash
# 1. Créer la branche
git checkout dev
git pull origin dev
git checkout -b fix/login-timeout

# 2. Corriger
# ... code ...
git add .
git commit -m "fix: resolve login timeout after 30s"
git push origin fix/login-timeout

# 3. Créer la PR
gh pr create \
  --base dev \
  --title "fix: resolve login timeout" \
  --label "release:patch" \
  --label "type:bugfix" \
  --label "backend"
```

**Résultat** :
- ✅ Bot commente : "Next version: `v1.0.1-rc1`"
- ✅ Après merge : Tag `v1.0.1-rc1` créé

---

### Scénario 3 : Breaking Change

```bash
# 1. Créer la branche
git checkout dev
git pull origin dev
git checkout -b feature/api-v2

# 2. Développer
# ... changements majeurs d'API ...
git add .
git commit -m "feat!: migrate to API v2"
git push origin feature/api-v2

# 3. Créer la PR
gh pr create \
  --base dev \
  --title "feat!: migrate to API v2 (BREAKING)" \
  --label "release:major" \
  --label "type:feature" \
  --label "backend"
```

**Résultat** :
- ✅ Bot commente : "Next version: `v2.0.0-rc1`"
- ✅ Après merge : Tag `v2.0.0-rc1` créé

---

### Scénario 4 : Hotfix en Production

```bash
# 1. Créer depuis main
git checkout main
git pull origin main
git checkout -b hotfix/critical-security

# 2. Corriger
# ... fix urgent ...
git add .
git commit -m "fix: patch critical security vulnerability"
git push origin hotfix/critical-security

# 3. Créer la PR vers MAIN
gh pr create \
  --base main \
  --title "fix: patch critical security vulnerability" \
  --label "release:patch" \
  --label "type:hotfix" \
  --label "priority:critical" \
  --label "security"
```

**Résultat** :
- ✅ Bot commente : "Next version: `v1.0.1`" (pas de -rc)
- ✅ Après merge : Tag `v1.0.1` créé
- ⚠️ **N'oubliez pas** de reporter le fix sur `dev` !

```bash
# Reporter sur dev
git checkout dev
git pull origin dev
git cherry-pick <commit-sha>
git push origin dev
```

---

### Scénario 5 : Plusieurs Petites Modifications (Incréments RC)

Si vous voulez juste incrémenter le RC sans changer la version :

```bash
gh pr create \
  --base dev \
  --title "chore: update dependencies" \
  --label "release:patch"  # Ou minor/major selon le besoin
```

**Résultat** :
- `v1.0.0-rc1` → `v1.0.0-rc2` → `v1.0.0-rc3` etc.

---

## 👀 Review Process

### 1. Review Automatique (CI)

**GitHub Actions vérifie** :
- ✅ Label `release:*` présent et unique
- ✅ Version calculée correctement
- 🔄 (Futur) Tests, linting, build

### 2. Review Humaine

**Au moins 1 approbation requise** (configurable)

**Reviewers vérifient** :
- Code quality
- Tests
- Documentation
- Respect des conventions

### 3. Merge

**Options** :
- **Squash and merge** (recommandé) - Combine tous les commits en un
- **Rebase and merge** - Garde l'historique linéaire
- **Merge commit** - Garde tous les commits

```bash
# Merger via CLI
gh pr merge 42 --squash

# Avec confirmation
gh pr merge 42 --squash --delete-branch
```

---

## 🚀 Après le Merge

### Automatique

1. ✅ Tag Git créé (ex: `v1.1.0-rc1`)
2. ✅ Images Docker buildées et publiées :
   - `ghcr.io/OWNER/REPO/backend:v1.1.0-rc1`
   - `ghcr.io/OWNER/REPO/frontend:v1.1.0-rc1`
   - `ghcr.io/OWNER/REPO/landing:v1.1.0-rc1`
3. ✅ GitHub Release créée

### Manuel

```bash
# Mettre à jour votre branche locale
git checkout dev
git pull origin dev

# Vérifier le nouveau tag
git tag -l

# Voir les images Docker
# GitHub Packages : https://github.com/OWNER/REPO/pkgs/container/PACKAGE
```

---

## 🐛 Problèmes Courants

### ❌ "Missing release label"

**Cause** : Aucun label `release:*` ajouté

**Solution** :
```bash
# Via CLI
gh pr edit 42 --add-label "release:minor"

# Via interface : Ajouter le label manuellement
```

---

### ❌ "Multiple release labels found"

**Cause** : Plusieurs labels `release:*` sur la PR

**Solution** :
```bash
# Retirer le mauvais
gh pr edit 42 --remove-label "release:major"

# Garder le bon
# (ex: garder release:minor)
```

---

### ❌ Conflit de merge

**Solution** :
```bash
# Mettre à jour votre branche
git checkout feature/ma-feature
git fetch origin
git rebase origin/dev

# Résoudre les conflits
# ... résolution manuelle ...
git add .
git rebase --continue

# Force push (rebase change l'historique)
git push --force-with-lease
```

---

### ❌ Tests échouent

**Solution** :
```bash
# Corriger localement
# ... fix ...
git add .
git commit -m "fix: resolve test failures"
git push origin feature/ma-feature

# La PR se met à jour automatiquement
```

---

## 📚 Conventions de Commit

Utilisez les [Conventional Commits](https://www.conventionalcommits.org/) :

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types** :
- `feat:` - Nouvelle fonctionnalité
- `fix:` - Correction de bug
- `docs:` - Documentation
- `style:` - Formatage (pas de changement de code)
- `refactor:` - Refactoring
- `test:` - Tests
- `chore:` - Maintenance

**Exemples** :
```bash
feat(auth): add OAuth2 login
fix(api): resolve CORS issue on /users endpoint
docs(readme): update installation instructions
refactor(core): extract user service
test(auth): add integration tests for login
chore(deps): update Spring Boot to 3.4.1
```

---

## ✅ Best Practices

### 1. Gardez les PR petites

- ✅ **Bon** : 1 feature = 1 PR
- ❌ **Mauvais** : 5 features = 1 PR

### 2. Description claire

```markdown
## 📋 Description

**Avant** : Les utilisateurs ne pouvaient pas modifier leur profil
**Après** : Ajout d'une page de profil avec édition complète

**Changements** :
- Nouvelle route `/profile`
- Component ProfileForm
- API endpoint PATCH /users/:id
```

### 3. Tests

- Ajoutez des tests pour chaque nouvelle feature
- Assurez-vous que tous les tests passent

### 4. Documentation

- Mettez à jour le README si nécessaire
- Commentez le code complexe
- Documentez les nouvelles API

---

## 📞 Besoin d'Aide ?

- 📖 [Guide Git Workflow](./README.md)
- 🤖 [Documentation GitHub Actions](./github-actions.md)
- 🏷️ [Référence des Labels](./labels-reference.md)
- 🐛 [Créer une issue](https://github.com/votre-org/taskforce/issues)

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
