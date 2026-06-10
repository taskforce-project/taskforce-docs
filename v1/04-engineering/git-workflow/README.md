# 🔀 Git Workflow - Taskforce

Guide complet du workflow Git et de la gestion des versions.

---

## 📚 Table des matières

- [Vue d'ensemble](#vue-densemble)
- [Branches](#branches)
- [Versioning Sémantique](#versioning-sémantique)
- [Pull Requests](#pull-requests)
- [Labels](#labels)
- [Exemples Pratiques](#exemples-pratiques)

---

## 🌟 Vue d'ensemble

Le projet Taskforce utilise un workflow Git professionnel avec :
- ✅ **Versioning sémantique automatique** (SemVer)
- ✅ **Release Candidates** sur la branche `dev`
- ✅ **Releases stables** sur la branche `main`
- ✅ **Publication automatique** d'images Docker
- ✅ **Validation automatique** des labels de version

---

## 🌿 Branches

### Branches principales

| Branche | Rôle | Versions | Protection |
|---------|------|----------|------------|
| **`main`** | Production | `v1.0.0` (stable) | ✅ PR requise |
| **`dev`** | Développement | `v1.0.0-rc1` (RC) | ✅ PR requise |

### Branches de travail

| Type | Nomenclature | Usage | Depuis |
|------|--------------|-------|--------|
| **Feature** | `feature/nom-feature` | Nouvelles fonctionnalités | `dev` |
| **Fix** | `fix/nom-bug` | Corrections de bugs | `dev` |
| **Hotfix** | `hotfix/nom-fix` | Corrections urgentes | `main` |

---

## 🏷️ Versioning Sémantique

Format : **`vMAJOR.MINOR.PATCH[-rcX]`**

### Composants

- **MAJOR** : Breaking changes incompatibles
- **MINOR** : Nouvelles fonctionnalités rétro-compatibles
- **PATCH** : Corrections de bugs rétro-compatibles
- **RC** : Release Candidate (préversion pour tests)

### Exemples

| Version | Type | Description |
|---------|------|-------------|
| `v1.0.0` | Stable | Version production |
| `v1.0.0-rc1` | RC | Premier candidat de v1.0.0 |
| `v1.0.0-rc2` | RC | Deuxième candidat de v1.0.0 |
| `v1.1.0` | Stable | Nouvelle feature en production |
| `v2.0.0` | Stable | Breaking change |

---

## 📋 Règles d'Incrémentation

### Sur la branche `dev` (Release Candidates)

| Label PR | Changement | Exemple |
|----------|-----------|---------|
| `release:major` | Breaking changes | `v1.0.0-rc1` → `v2.0.0-rc1` |
| `release:minor` | Nouvelles features | `v1.0.0-rc1` → `v1.1.0-rc1` |
| `release:patch` | Bug fixes | `v1.0.0-rc1` → `v1.0.1-rc1` |
| Aucun | Incrémente RC | `v1.0.0-rc1` → `v1.0.0-rc2` |

**Note** : Sur `dev`, le numéro RC repart toujours à 1 lors d'un changement de version.

### Sur la branche `main` (Versions Stables)

| Label PR | Changement | Exemple |
|----------|-----------|---------|
| `release:major` | Breaking changes | `v1.0.0` → `v2.0.0` |
| `release:minor` | Nouvelles features | `v1.0.0` → `v1.1.0` |
| `release:patch` | Bug fixes | `v1.0.0` → `v1.0.1` |

**Note** : Sur `main`, les versions sont toujours stables (pas de `-rc`).

---

## 🎯 Pull Requests

### Processus

1. **Créer une branche** depuis `dev` (ou `main` pour hotfix)
2. **Développer** et commiter
3. **Pousser** la branche
4. **Créer une PR** vers `dev` (ou `main`)
5. **Ajouter un label `release:*`** (OBLIGATOIRE)
6. **Remplir le template** de PR
7. **Attendre la validation** automatique
8. **Review** par l'équipe
9. **Merge** automatique → Tag + Docker images

### Template de PR

Chaque PR doit inclure :
- ✅ Description des changements
- ✅ Type de changement coché
- ✅ **Label `release:*`** (obligatoire)
- ✅ Checklist de validation
- ✅ Issues liées

### Validation Automatique

Le workflow `version-management.yml` vérifie :
- ✅ Présence d'un label `release:*`
- ✅ Un seul label de release
- ✅ Calcule la prochaine version
- ✅ Poste un commentaire sur la PR

❌ **La PR est bloquée si** :
- Aucun label `release:*`
- Plusieurs labels `release:*`

---

## 🏷️ Labels

### 📦 Release (OBLIGATOIRE)

| Label | Couleur | Description | Usage |
|-------|---------|-------------|-------|
| `release:major` | 🔴 | Breaking changes | v1.0.0 → v2.0.0 |
| `release:minor` | 🟢 | Nouvelles features | v1.0.0 → v1.1.0 |
| `release:patch` | 🟡 | Bug fixes | v1.0.0 → v1.0.1 |

### 🎯 Type (Optionnel)

| Label | Description |
|-------|-------------|
| `type:feature` | Nouvelle fonctionnalité |
| `type:bugfix` | Correction de bug |
| `type:hotfix` | Correction urgente |
| `type:refactor` | Refactoring |
| `type:test` | Tests |
| `type:ci/cd` | CI/CD |

### 🧩 Composants (Optionnel)

| Label | Description |
|-------|-------------|
| `backend` | Backend / API |
| `frontend` | Frontend / UI |
| `database` | Base de données |
| `infra` | Infrastructure |
| `security` | Sécurité |
| `performance` | Performance |

### ⚡ Priorité (Optionnel)

| Label | Description |
|-------|-------------|
| `priority:critical` | 🔴 À traiter immédiatement |
| `priority:high` | 🟠 À traiter rapidement |
| `priority:medium` | 🟡 Priorité normale |
| `priority:low` | 🟢 Quand possible |

### 📊 Status (Optionnel)

| Label | Description |
|-------|-------------|
| `status:ready-for-review` | ✅ Prêt pour review |
| `status:in-progress` | 🚧 En cours |
| `status:blocked` | 🚫 Bloqué |
| `status:needs-info` | ❓ Info manquante |

👉 [Liste complète des labels](./labels-reference.md)

---

## 🚀 CI/CD Automatique

### Workflow 1 : Version Management

**Fichier** : `.github/workflows/version-management.yml`

**Déclenché sur** : Ouverture/mise à jour de PR

**Actions** :
1. Vérifie la présence d'un label `release:*`
2. Calcule la prochaine version
3. Poste un commentaire sur la PR avec la version

### Workflow 2 : Release & Docker Publish

**Fichier** : `.github/workflows/release.yml`

**Déclenché sur** : Push sur `dev` ou `main` (après merge)

**Actions** :
1. Récupère les labels de la PR mergée
2. Calcule la nouvelle version
3. Crée un tag Git
4. Build et push des images Docker :
   - `ghcr.io/OWNER/REPO/backend:vX.Y.Z`
   - `ghcr.io/OWNER/REPO/frontend:vX.Y.Z`
   - `ghcr.io/OWNER/REPO/landing:vX.Y.Z`
5. Crée une GitHub Release

### Images Docker Publiées

Chaque service reçoit 3 tags :
- `vX.Y.Z[-rcX]` - Version spécifique
- `latest` - Dernière version
- `sha-XXXXXXX` - Commit SHA

---

## 💡 Exemples Pratiques

### Exemple 1 : Nouvelle Feature sur `dev`

```bash
# 1. Créer la branche
git checkout dev
git pull origin dev
git checkout -b feature/user-profile

# 2. Développer
# ... éditer le code ...
git add .
git commit -m "feat: add user profile page with avatar upload"
git push origin feature/user-profile
```

**Sur GitHub** :
1. Créer une PR vers `dev`
2. Ajouter le label `release:minor`
3. Remplir le template
4. Le bot commente : "Next version: `v1.1.0-rc1`"
5. Review + Merge
6. ✅ Tag `v1.1.0-rc1` créé automatiquement
7. ✅ Images Docker publiées

---

### Exemple 2 : Bug Fix sur `dev`

```bash
# 1. Créer la branche
git checkout dev
git pull origin dev
git checkout -b fix/login-timeout

# 2. Corriger
# ... éditer le code ...
git add .
git commit -m "fix: resolve login timeout after 30 seconds"
git push origin fix/login-timeout
```

**Sur GitHub** :
1. Créer une PR vers `dev`
2. Ajouter le label `release:patch`
3. Merge
4. ✅ Tag `v1.0.1-rc1` créé

---

### Exemple 3 : Hotfix Urgent sur `main`

```bash
# 1. Créer depuis main
git checkout main
git pull origin main
git checkout -b hotfix/critical-security-fix

# 2. Corriger
# ... éditer le code ...
git add .
git commit -m "fix: patch critical security vulnerability CVE-XXXX"
git push origin hotfix/critical-security-fix
```

**Sur GitHub** :
1. Créer une PR vers `main`
2. Ajouter le label `release:patch`
3. Ajouter le label `priority:critical`
4. Merge
5. ✅ Tag `v1.0.1` créé (sans -rc)
6. ✅ Images Docker en production
7. **Important** : Reporter le fix sur `dev` !

```bash
# Reporter sur dev
git checkout dev
git pull origin dev
git cherry-pick <commit-sha>
git push origin dev
```

---

### Exemple 4 : Release Candidate → Stable

```bash
# Après plusieurs RC testés (v1.1.0-rc1, rc2, rc3...)
# Créer une PR de dev → main

git checkout main
git pull origin main
git checkout -b release/v1.1.0
git merge dev
git push origin release/v1.1.0
```

**Sur GitHub** :
1. Créer une PR `dev` → `main`
2. Ajouter le label `release:minor`
3. Merge
4. ✅ Tag `v1.1.0` créé (version stable)

---

## ❓ FAQ

### Que faire si j'oublie le label `release:*` ?

La PR sera automatiquement bloquée. Il suffit d'ajouter le label approprié et la validation se relancera.

### Puis-je sauter une version (v1.0.0 → v3.0.0) ?

Non. Le système n'autorise qu'un incrément de +1 en MAJOR pour éviter les erreurs.

### Comment gérer plusieurs petites modifications ?

Utilisez des commits successifs sans label de version. Le RC sera incrémenté automatiquement :
- `v1.0.0-rc1` → `v1.0.0-rc2` → `v1.0.0-rc3`

### Dois-je créer les tags manuellement ?

Non. Les tags sont créés automatiquement par GitHub Actions après le merge.

### Comment voir toutes les versions ?

```bash
# Lister tous les tags
git tag -l

# Tags RC uniquement
git tag -l "v*-rc*"

# Tags stables uniquement
git tag -l "v*" | grep -v "rc"
```

---

## 📚 Documentation Complémentaire

- 📋 [Guide des Pull Requests](./pull-requests.md)
- 🏷️ [Référence des Labels](./labels-reference.md)
- 🚀 [GitHub Actions Détaillé](./github-actions.md)
- 🔧 [Setup Initial](./setup.md)

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
