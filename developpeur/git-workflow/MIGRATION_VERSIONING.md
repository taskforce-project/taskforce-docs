# 🔄 Migration vers le Versioning par Service

## 📅 Date de Migration
**28 Janvier 2025**

---

## 🎯 Objectif

Passer d'un **versioning monolithique unique** à un **versioning indépendant par service** :

| Avant | Après |
|-------|-------|
| `v1.2.3-rc1` | `backend-v1.2.3-rc1`<br>`frontend-v2.0.1-rc1`<br>`landing-v1.0.0-rc1` |
| Un seul tag pour tout le projet | Un tag par service modifié |
| Build de tous les services à chaque merge | Build uniquement des services modifiés |

---

## ✅ Changements Effectués

### 1. GitHub Actions Workflows

#### `release.yml` - Nouveau workflow complet
- ✅ Détection automatique des services modifiés (via labels + fichiers)
- ✅ Calcul de version indépendant par service
- ✅ Création de tags séparés : `backend-v*`, `frontend-v*`, `landing-v*`
- ✅ Build conditionnel (seulement les services modifiés)
- ✅ Publication Docker avec tags spécifiques par service
- ✅ Création de GitHub Releases séparées

#### `version-management.yml` - Validation mise à jour
- ✅ Validation des labels par service (`backend:release:*`, `frontend:release:*`, `landing:release:*`)
- ✅ Vérification qu'un service n'a pas plusieurs labels de release
- ✅ Calcul et aperçu des versions pour chaque service modifié
- ✅ Commentaire automatique sur la PR avec les versions prévues

### 2. Labels GitHub

**Supprimés** :
- ❌ `release:major`
- ❌ `release:minor`
- ❌ `release:patch`

**Ajoutés** :
```yaml
# Backend
- backend:release:major
- backend:release:minor
- backend:release:patch

# Frontend
- frontend:release:major
- frontend:release:minor
- frontend:release:patch

# Landing
- landing:release:major
- landing:release:minor
- landing:release:patch
```

### 3. Documentation

**Nouveaux fichiers** :
- ✅ `versioning-par-service.md` - Guide complet du nouveau système
- ✅ `pull-requests-service.md` - Création de PR avec labels par service

**Mis à jour** :
- ✅ `README.md` - Liens vers la nouvelle documentation
- ✅ `labels-reference.md` - Référence des nouveaux labels

---

## 🚀 Migration des Tags Existants

### État actuel (avant migration)
```bash
v0.1.0-rc0  # Tag monolithique actuel
```

### État après migration
```bash
# Tags initiaux pour chaque service
backend-v0.1.0-rc0
frontend-v0.1.0-rc0
landing-v0.1.0-rc0

# L'ancien tag v0.1.0-rc0 reste pour historique mais n'est plus utilisé
```

### Commandes de migration

```bash
# 1. Récupérer le dernier commit tagué
git checkout dev
git pull origin dev

# 2. Créer les tags initiaux pour chaque service
git tag -a backend-v0.1.0-rc0 -m "Initial Backend Version"
git tag -a frontend-v0.1.0-rc0 -m "Initial Frontend Version"
git tag -a landing-v0.1.0-rc0 -m "Initial Landing Version"

# 3. Pousser les nouveaux tags
git push origin backend-v0.1.0-rc0
git push origin frontend-v0.1.0-rc0
git push origin landing-v0.1.0-rc0
```

---

## 📋 Guide de Transition

### Pour les Développeurs

#### Avant (ancien système)
```bash
gh pr create \
  --base dev \
  --label "release:minor"
```

#### Après (nouveau système)
```bash
# Si modification du backend uniquement
gh pr create \
  --base dev \
  --label "backend:release:minor"

# Si modification de plusieurs services
gh pr create \
  --base dev \
  --label "backend:release:minor,frontend:release:patch"
```

### Workflow PR

1. **Identifier les services modifiés**
   ```bash
   git status
   # Fichiers dans backend/ → backend:release:*
   # Fichiers dans frontend/ → frontend:release:*
   # Fichiers dans landing-page/ → landing:release:*
   ```

2. **Choisir le type de version** (major/minor/patch)
   - **major** : Breaking changes
   - **minor** : Nouvelles features (compatibles)
   - **patch** : Bugfixes

3. **Créer la PR avec les bons labels**
   ```bash
   gh pr create --base dev \
     --label "backend:release:minor" \
     --label "type:feature"
   ```

4. **Vérifier le commentaire du bot**
   ```markdown
   ## 📦 Version Preview
   - **Backend**: `backend-v1.3.0-rc1`
   ```

5. **Merger** → Les tags et images Docker sont créés automatiquement

---

## 🧪 Tests et Validation

### Test 1 : PR Backend uniquement
```bash
# Créer une PR test
gh pr create --base dev \
  --title "test: Validate backend versioning" \
  --label "backend:release:patch"

# Vérifier :
✅ Le workflow version-management valide les labels
✅ Le bot poste un commentaire avec backend-vX.Y.Z-rcN
✅ Après merge : tag backend-vX.Y.Z-rcN créé
✅ Image Docker ghcr.io/org/backend:backend-vX.Y.Z-rcN publiée
```

### Test 2 : PR Multi-services
```bash
gh pr create --base dev \
  --title "test: Validate multi-service versioning" \
  --label "backend:release:minor,frontend:release:patch"

# Vérifier :
✅ 2 versions calculées séparément
✅ 2 tags créés
✅ 2 images Docker publiées
✅ Landing non buildé (car non modifié)
```

---

## ⚠️ Points d'Attention

### ⚠️  Anciens tags conservés
Les anciens tags `v*` restent dans l'historique Git mais **ne doivent plus être utilisés** :
```bash
# ❌ Ne plus créer
git tag v1.2.3

# ✅ Utiliser maintenant
git tag backend-v1.2.3
```

### ⚠️  PR en cours
Les **PR ouvertes avant la migration** doivent être mises à jour :
```bash
# Retirer ancien label
gh pr edit <PR_NUMBER> --remove-label "release:minor"

# Ajouter nouveau(x) label(s)
gh pr edit <PR_NUMBER> --add-label "backend:release:minor"
```

### ⚠️  Branches de feature en cours
Les branches créées avant la migration fonctionneront normalement, mais **devront utiliser les nouveaux labels** lors de la création de PR.

---

## 📊 Impact sur le CI/CD

### Avant
```yaml
Merge PR → Build ALL services → Tag unique v1.2.3-rc1
```

### Après
```yaml
Merge PR → Detect changes → Build ONLY modified services
         → Create service-specific tags
         → Publish service-specific Docker images
```

### Bénéfices
- ✅ **Temps de build réduit** (build seulement ce qui a changé)
- ✅ **Versioning précis** (chaque service a sa propre version)
- ✅ **Rollback granulaire** (rollback backend sans toucher frontend)
- ✅ **Images Docker plus claires** (ghcr.io/org/backend:backend-v1.2.3)

---

## 🔍 Vérification Post-Migration

### Checklist
- [x] Workflows `release.yml` et `version-management.yml` mis à jour
- [x] Labels GitHub créés (9 nouveaux labels `service:release:*`)
- [x] Documentation créée (`versioning-par-service.md`, `pull-requests-service.md`)
- [ ] Tags initiaux créés (`backend-v0.1.0-rc0`, etc.)
- [ ] Labels importés sur GitHub (`gh label import`)
- [ ] Test PR backend seul
- [ ] Test PR multi-services
- [ ] Communication équipe effectuée

### Commandes de Vérification

```bash
# 1. Vérifier les workflows
ls -l .github/workflows/
# Doit contenir : release.yml, version-management.yml

# 2. Vérifier les labels
cat .github/labels.yml | grep "release"
# Doit contenir : backend:release:*, frontend:release:*, landing:release:*

# 3. Vérifier les tags Git
git tag -l "*-v*"
# Doit contenir : backend-v*, frontend-v*, landing-v*

# 4. Tester le workflow (dry-run)
gh pr create --base dev --draft \
  --title "test: Migration validation" \
  --label "backend:release:patch"
```

---

## 📚 Références

- [Versioning par Service](./versioning-par-service.md)
- [Pull Requests avec Services](./pull-requests-service.md)
- [GitHub Actions](./github-actions.md)
- [Labels Reference](./labels-reference.md)

---

## 💡 Support

En cas de problème avec la migration :
1. Consulter la [documentation complète](./versioning-par-service.md)
2. Vérifier les [exemples de scénarios](./pull-requests-service.md#exemples-de-scénarios)
3. Contacter l'équipe DevOps

---

**Migration effectuée par** : GitHub Copilot  
**Date** : 28 Janvier 2025  
**Status** : ✅ Workflows et documentation complétés - Tags initiaux à créer
