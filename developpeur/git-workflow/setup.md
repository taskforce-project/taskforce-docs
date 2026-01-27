# 🚀 Setup Initial - GitHub Project Management

Guide d'installation et de configuration initiale des GitHub Actions et du workflow de versioning.

---

## 📋 Prérequis

Avant de commencer :
- ✅ Accès administrateur au repository GitHub
- ✅ [GitHub CLI](https://cli.github.com/) installé
- ✅ Git configuré localement

---

## 🔧 Installation Étape par Étape

### Étape 1 : Installer GitHub CLI

**Windows** :
```powershell
winget install GitHub.cli
```

**macOS** :
```bash
brew install gh
```

**Linux** :
```bash
# Debian/Ubuntu
sudo apt install gh

# Fedora/RHEL
sudo dnf install gh
```

### Étape 2 : Se connecter à GitHub

```bash
gh auth login
```

Suivre les instructions :
1. Sélectionner "GitHub.com"
2. Sélectionner "HTTPS"
3. Authentifier via le navigateur

---

## 🏷️ Étape 3 : Importer les Labels

### Option A : Import Automatique (Recommandé)

```bash
# Naviguer vers le projet
cd c:\taskforce-project\taskforce-fullstack

# Importer tous les labels depuis le fichier YAML
gh label create -f .github/labels.yml
```

### Option B : Import Manuel

Si l'import automatique échoue, créer les labels un par un :

```bash
# Labels RELEASE (OBLIGATOIRES)
gh label create "release:major" --color "d73a4a" --description "⬆️ Breaking changes - Incrémente MAJOR (v1.0.0 -> v2.0.0)"
gh label create "release:minor" --color "0e8a16" --description "✨ New features - Incrémente MINOR (v1.0.0 -> v1.1.0)"
gh label create "release:patch" --color "fbca04" --description "🐛 Bug fixes - Incrémente PATCH (v1.0.0 -> v1.0.1)"

# Labels TYPE
gh label create "type:feature" --color "a2eeef" --description "✨ Nouvelle fonctionnalité"
gh label create "type:bugfix" --color "d73a4a" --description "🐛 Correction de bug"
gh label create "type:hotfix" --color "b60205" --description "🚨 Hotfix urgent en production"
gh label create "type:refactor" --color "fbca04" --description "♻️ Refactoring de code"
gh label create "type:test" --color "1d76db" --description "🧪 Ajout ou modification de tests"
gh label create "type:ci/cd" --color "ededed" --description "⚙️ CI/CD et DevOps"

# Labels COMPONENTS
gh label create "backend" --color "5319e7" --description "🔧 Backend / API"
gh label create "frontend" --color "0052cc" --description "🎨 Frontend / UI"
gh label create "database" --color "c5def5" --description "🗄️ Database related"
gh label create "infra" --color "ededed" --description "🏗️ Infrastructure & DevOps"
gh label create "security" --color "b60205" --description "🔒 Sécurité"
gh label create "performance" --color "fbca04" --description "⚡ Performance optimization"

# Labels PRIORITY
gh label create "priority:critical" --color "b60205" --description "🔴 Critique - À traiter immédiatement"
gh label create "priority:high" --color "d93f0b" --description "🟠 Haute - À traiter rapidement"
gh label create "priority:medium" --color "fbca04" --description "🟡 Moyenne - À traiter normalement"
gh label create "priority:low" --color "0e8a16" --description "🟢 Basse - Quand possible"

# Labels STATUS
gh label create "status:ready-for-review" --color "0e8a16" --description "✅ Prêt pour review"
gh label create "status:in-progress" --color "fbca04" --description "🚧 En cours de développement"
gh label create "status:blocked" --color "d73a4a" --description "🚫 Bloqué - Nécessite intervention"
gh label create "status:needs-info" --color "d876e3" --description "❓ Informations manquantes"
gh label create "status:on-hold" --color "ededed" --description "⏸️ En attente"
```

### Vérifier les labels

```bash
gh label list
```

---

## 🏷️ Étape 4 : Créer le Premier Tag

```bash
# Se placer sur la branche dev
git checkout dev
git pull origin dev

# Créer le tag initial
git tag v0.1.0-rc0
git push origin v0.1.0-rc0

# Vérifier
git tag -l
```

**Note** : Ce tag initial sert de point de départ pour le versioning automatique.

---

## ⚙️ Étape 5 : Configurer les Permissions GitHub Actions

### Via l'interface GitHub

1. Aller sur **Settings** du repository
2. **Actions** → **General**
3. **Workflow permissions** :
   - ✅ Sélectionner **"Read and write permissions"**
   - ✅ Cocher **"Allow GitHub Actions to create and approve pull requests"**
4. Cliquer **Save**

### Via GitHub CLI

```bash
# Activer les permissions (nécessite droits admin)
gh api repos/{owner}/{repo}/actions/permissions \
  -X PUT \
  -f default_workflow_permissions=write \
  -F can_approve_pull_request_reviews=true
```

---

## ✅ Étape 6 : Vérifier les Workflows

Les workflows sont déjà présents dans `.github/workflows/` :
- ✅ `version-management.yml`
- ✅ `release.yml`

GitHub Actions les détecte automatiquement. Pour vérifier :

```bash
# Lister les workflows
gh workflow list

# Voir l'historique
gh run list
```

---

## 🧪 Étape 7 : Tester le Workflow

### 1. Créer une branche de test

```bash
git checkout dev
git pull origin dev
git checkout -b feature/test-workflow
```

### 2. Faire un changement

```bash
echo "# Test Workflow" >> TEST_WORKFLOW.md
git add TEST_WORKFLOW.md
git commit -m "feat: test GitHub Actions workflow"
git push origin feature/test-workflow
```

### 3. Créer une Pull Request

**Via GitHub CLI** :
```bash
gh pr create \
  --base dev \
  --title "feat: test GitHub Actions workflow" \
  --body "Test du workflow de versioning automatique" \
  --label "release:minor"
```

**Via l'interface GitHub** :
1. Aller sur le repository
2. Créer une PR vers `dev`
3. Ajouter le label `release:minor`

### 4. Vérifier le commentaire automatique

Le bot devrait commenter avec :
```markdown
## 🏷️ Version Bump Preview

**Current version:** `v0.1.0-rc0`
**Next version:** `v0.1.0-rc1`
**Target branch:** `dev`

This version will be tagged automatically when the PR is merged.
```

### 5. Merger la PR

```bash
gh pr merge --squash
```

### 6. Vérifier la création du tag

```bash
git checkout dev
git pull origin dev
git tag -l

# Devrait afficher v0.1.0-rc0 et v0.1.0-rc1
```

### 7. Vérifier les images Docker

1. Aller sur **Packages** du repository
2. Vérifier la présence de :
   - `backend:v0.1.0-rc1`
   - `frontend:v0.1.0-rc1`
   - `landing:v0.1.0-rc1`

---

## ✅ Checklist Finale

Vérifier que tout est bien configuré :

- [ ] GitHub CLI installé et authentifié
- [ ] Labels créés sur GitHub (voir avec `gh label list`)
- [ ] Tag initial `v0.1.0-rc0` créé
- [ ] Permissions GitHub Actions configurées
- [ ] Workflows visibles dans **Actions**
- [ ] PR de test créée et mergée
- [ ] Tag `v0.1.0-rc1` créé automatiquement
- [ ] Images Docker publiées sur GitHub Packages
- [ ] Documentation lue

---

## 🎯 Prochaines Étapes

Maintenant que tout est configuré :

1. ✅ **Lire la documentation** :
   - [Git Workflow](./README.md)
   - [GitHub Actions](./github-actions.md)
   - [Pull Requests](./pull-requests.md)

2. ✅ **Créer votre première vraie PR** :
   - Partir de `dev`
   - Ajouter un label `release:*`
   - Merger et voir la magie opérer ✨

3. ✅ **Consulter les releases** :
   - Aller sur **Releases** du repository
   - Voir les versions publiées

---

## 🐛 Problèmes Courants

### ❌ "gh: command not found"

**Solution** : Réinstaller GitHub CLI et redémarrer le terminal

### ❌ "Authentication required"

**Solution** :
```bash
gh auth logout
gh auth login
```

### ❌ Labels déjà existants

**Solution** :
```bash
# Supprimer un label existant
gh label delete "release:major" --yes

# Recréer
gh label create "release:major" --color "d73a4a" --description "..."
```

### ❌ Workflow ne se déclenche pas

**Solutions** :
1. Vérifier **Settings → Actions → General → Actions permissions**
2. Activer "Allow all actions and reusable workflows"
3. Vérifier les permissions "Read and write"

### ❌ "Permission denied" lors du push du tag

**Solution** : Vérifier les permissions dans **Settings → Actions → General → Workflow permissions**

---

## 📞 Support

Besoin d'aide ?
- 📖 [Documentation GitHub Actions](https://docs.github.com/en/actions)
- 🐛 [Créer une issue](https://github.com/votre-org/taskforce/issues)
- 💬 Contacter l'équipe DevOps

---

## 🎉 C'est Fait !

Votre workflow est maintenant opérationnel. Chaque PR mergée créera automatiquement :
- ✅ Un tag Git
- ✅ Des images Docker
- ✅ Une GitHub Release

Bon développement ! 🚀

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
