# 🚀 GitHub Actions - Taskforce

Documentation complète des workflows GitHub Actions pour l'automatisation du versioning et du déploiement.

---

## 📚 Table des matières

- [Vue d'ensemble](#vue-densemble)
- [Workflow 1: Version Management](#workflow-1-version-management)
- [Workflow 2: Release & Docker Publish](#workflow-2-release--docker-publish)
- [Configuration Requise](#configuration-requise)
- [Debugging](#debugging)

---

## 🌟 Vue d'ensemble

Le projet utilise **2 workflows GitHub Actions** :

| Workflow | Déclencheur | Rôle |
|----------|-------------|------|
| **Version Management** | Ouverture/update de PR | Valide les labels et calcule la version |
| **Release & Docker Publish** | Push sur `dev`/`main` | Crée le tag et publie les images Docker |

---

## 📋 Workflow 1: Version Management

### Fichier

`.github/workflows/version-management.yml`

### Déclencheurs

```yaml
on:
  pull_request:
    types: [opened, synchronize, labeled, unlabeled]
    branches:
      - dev
      - main
```

**Déclenché quand** :
- Une PR est ouverte vers `dev` ou `main`
- Une PR est mise à jour (nouveau commit)
- Un label est ajouté/retiré

### Jobs

#### 1. `validate-version-label`

**Objectif** : Vérifier la présence et l'unicité du label `release:*`

**Étapes** :
```javascript
// Récupérer les labels de la PR
const labels = context.payload.pull_request.labels.map(l => l.name);
const releaseLabels = labels.filter(l => l.startsWith('release:'));

// Vérifier qu'il y a exactement 1 label release
if (releaseLabels.length === 0) {
  core.setFailed('❌ Missing release label!');
}
if (releaseLabels.length > 1) {
  core.setFailed('❌ Multiple release labels found!');
}
```

**Résultat** :
- ✅ Succès si exactement 1 label `release:*`
- ❌ Échec sinon (bloque la PR)

---

#### 2. `calculate-next-version`

**Objectif** : Calculer la prochaine version et commenter sur la PR

**Étapes** :

1. **Récupérer le dernier tag**
   ```bash
   if [[ "${{ github.base_ref }}" == "dev" ]]; then
     LATEST=$(git tag -l "v*-rc*" --sort=-v:refname | head -n1)
   else
     LATEST=$(git tag -l "v*" --sort=-v:refname | grep -v "rc" | head -n1)
   fi
   ```

2. **Parser la version**
   ```bash
   # Regex: v1.2.3-rc4
   [_, major, minor, patch, __, rc] = latestTag.match(/v(\d+)\.(\d+)\.(\d+)(-rc(\d+))?/);
   ```

3. **Calculer la nouvelle version**

   **Pour `dev`** :
   ```javascript
   if (labels.includes('release:major')) {
     major += 1; minor = 0; patch = 0; rc = 1;
     nextVersion = `v${major}.${minor}.${patch}-rc${rc}`;
   } else if (labels.includes('release:minor')) {
     minor += 1; patch = 0; rc = 1;
     nextVersion = `v${major}.${minor}.${patch}-rc${rc}`;
   } else if (labels.includes('release:patch')) {
     patch += 1; rc = 1;
     nextVersion = `v${major}.${minor}.${patch}-rc${rc}`;
   } else {
     rc += 1; // Incrémente juste le RC
     nextVersion = `v${major}.${minor}.${patch}-rc${rc}`;
   }
   ```

   **Pour `main`** :
   ```javascript
   if (labels.includes('release:major')) {
     major += 1; minor = 0; patch = 0;
   } else if (labels.includes('release:minor')) {
     minor += 1; patch = 0;
   } else {
     patch += 1;
   }
   nextVersion = `v${major}.${minor}.${patch}`; // Pas de -rc
   ```

4. **Commenter sur la PR**
   ```markdown
   ## 🏷️ Version Bump Preview
   
   **Current version:** `v1.0.0-rc1`
   **Next version:** `v1.1.0-rc1`
   **Target branch:** `dev`
   
   This version will be tagged automatically when the PR is merged.
   ```

---

## 🚀 Workflow 2: Release & Docker Publish

### Fichier

`.github/workflows/release.yml`

### Déclencheurs

```yaml
on:
  push:
    branches:
      - dev
      - main
```

**Déclenché quand** :
- Un commit est pushé sur `dev` (après merge d'une PR)
- Un commit est pushé sur `main` (après merge d'une PR)

### Permissions

```yaml
permissions:
  contents: write    # Pour créer des tags et releases
  packages: write    # Pour publier sur GitHub Container Registry
```

### Job: `create-tag-and-publish`

#### Étape 1 : Checkout

```yaml
- name: Checkout
  uses: actions/checkout@v4
  with:
    fetch-depth: 0  # Récupère tout l'historique Git
```

---

#### Étape 2 : Récupérer les labels de la PR

```javascript
// Trouver la PR associée au commit
const commit = context.payload.head_commit.id;
const prs = await github.rest.repos.listPullRequestsAssociatedWithCommit({
  owner: context.repo.owner,
  repo: context.repo.repo,
  commit_sha: commit
});

const pr = prs.data[0];
const labels = pr.labels.map(l => l.name);

core.setOutput('labels', labels.join(','));
```

**Important** : Cette étape récupère les labels de la PR qui vient d'être mergée.

---

#### Étape 3 : Calculer la version

Même logique que le workflow `version-management.yml`, mais cette fois on crée vraiment le tag.

```bash
BRANCH="${{ github.ref_name }}"

if [[ "$BRANCH" == "dev" ]]; then
  LATEST=$(git tag -l "v*-rc*" --sort=-v:refname | head -n1)
  # ... calcul version RC ...
  NEW_VERSION="v${MAJOR}.${MINOR}.${PATCH}-rc${RC}"
else
  LATEST=$(git tag -l "v*" --sort=-v:refname | grep -v "rc" | head -n1)
  # ... calcul version stable ...
  NEW_VERSION="v${MAJOR}.${MINOR}.${PATCH}"
fi

echo "version=$NEW_VERSION" >> $GITHUB_OUTPUT
```

---

#### Étape 4 : Créer le tag Git

```yaml
- name: Create Git Tag
  run: |
    git config user.name "github-actions[bot]"
    git config user.email "github-actions[bot]@users.noreply.github.com"
    git tag -a "${{ steps.version.outputs.version }}" -m "Release ${{ steps.version.outputs.version }}"
    git push origin "${{ steps.version.outputs.version }}"
```

**Résultat** : Tag créé et poussé sur GitHub

---

#### Étape 5 : Build et Push des Images Docker

**Backend** :
```yaml
- name: Build and push Backend
  uses: docker/build-push-action@v5
  with:
    context: ./backend/tf-api
    file: ./backend/tf-api/Dockerfile
    push: true
    tags: |
      ghcr.io/${{ github.repository }}/backend:${{ steps.version.outputs.version }}
      ghcr.io/${{ github.repository }}/backend:latest
      ghcr.io/${{ github.repository }}/backend:sha-${{ github.sha }}
    cache-from: type=gha
    cache-to: type=gha,mode=max
```

**Frontend** :
```yaml
- name: Build and push Frontend
  uses: docker/build-push-action@v5
  with:
    context: ./frontend
    file: ./frontend/Dockerfile
    push: true
    tags: |
      ghcr.io/${{ github.repository }}/frontend:${{ steps.version.outputs.version }}
      ghcr.io/${{ github.repository }}/frontend:latest
      ghcr.io/${{ github.repository }}/frontend:sha-${{ github.sha }}
```

**Landing** :
```yaml
- name: Build and push Landing
  uses: docker/build-push-action@v5
  with:
    context: ./landing-page
    file: ./landing-page/Dockerfile
    push: true
    tags: |
      ghcr.io/${{ github.repository }}/landing:${{ steps.version.outputs.version }}
      ghcr.io/${{ github.repository }}/landing:latest
      ghcr.io/${{ github.repository }}/landing:sha-${{ github.sha }}
```

**Résultat** : 3 images publiées avec 3 tags chacune

---

#### Étape 6 : Créer une GitHub Release

```javascript
const version = '${{ steps.version.outputs.version }}';
const isPrerelease = version.includes('-rc');

await github.rest.repos.createRelease({
  owner: context.repo.owner,
  repo: context.repo.repo,
  tag_name: version,
  name: version,
  body: `## ${version}

Released from \`${branch}\` branch.

**Docker Images:**
- \`ghcr.io/${{ github.repository }}/backend:${version}\`
- \`ghcr.io/${{ github.repository }}/frontend:${version}\`
- \`ghcr.io/${{ github.repository }}/landing:${version}\``,
  draft: false,
  prerelease: isPrerelease  // true si -rc, sinon false
});
```

**Résultat** : Release créée sur GitHub avec les liens vers les images Docker

---

## ⚙️ Configuration Requise

### 1. Permissions GitHub Actions

**Settings → Actions → General → Workflow permissions**

- ✅ **Read and write permissions**
- ✅ **Allow GitHub Actions to create and approve pull requests**

### 2. GitHub Container Registry

Les images sont automatiquement publiées sur `ghcr.io` (GitHub Container Registry).

**Accès** :
- Public : `docker pull ghcr.io/OWNER/REPO/backend:latest`
- Privé : `docker login ghcr.io` avec un PAT

### 3. Labels

Les labels doivent être créés sur le repo. Voir [setup.md](./setup.md) pour l'import automatique.

---

## 🐛 Debugging

### Voir les logs d'un workflow

1. Aller sur **Actions** dans GitHub
2. Sélectionner le workflow
3. Cliquer sur le job
4. Voir les logs détaillés

### Tester localement

Vous pouvez tester les scripts bash localement :

```bash
# Simuler le calcul de version
BRANCH="dev"
LABELS="release:minor"
LATEST=$(git tag -l "v*-rc*" --sort=-v:refname | head -n1)

if [[ $LATEST =~ v([0-9]+)\.([0-9]+)\.([0-9]+)(-rc([0-9]+))? ]]; then
  MAJOR="${BASH_REMATCH[1]}"
  MINOR="${BASH_REMATCH[2]}"
  PATCH="${BASH_REMATCH[3]}"
  RC="${BASH_REMATCH[5]:-0}"
  
  echo "Current: v$MAJOR.$MINOR.$PATCH-rc$RC"
  
  # Calculer next version...
fi
```

### Problèmes courants

#### ❌ Workflow ne se déclenche pas

**Causes** :
- Permissions GitHub Actions désactivées
- Branche protégée sans règles appropriées

**Solution** :
- Vérifier **Settings → Actions → General**
- Vérifier **Settings → Branches → Branch protection rules**

---

#### ❌ "No PR found for this commit"

**Cause** : Le commit n'est pas associé à une PR (push direct)

**Solution** : Toujours merger via une PR, ne jamais push directement sur `dev`/`main`

---

#### ❌ Docker build fail

**Causes** :
- Dockerfile invalide
- Contexte de build incorrect
- Secrets manquants

**Solution** :
- Tester le build localement : `docker build -f backend/tf-api/Dockerfile backend/tf-api`
- Vérifier les secrets dans **Settings → Secrets**

---

#### ❌ "Permission denied" lors du push du tag

**Cause** : Permissions insuffisantes

**Solution** :
- Vérifier **Settings → Actions → General → Workflow permissions**
- Activer "Read and write permissions"

---

## 📊 Monitoring

### Voir les versions publiées

```bash
# Lister tous les tags
git tag -l

# Voir les images Docker
# GitHub Packages : https://github.com/OWNER/REPO/pkgs/container/PACKAGE
```

### Statistiques

- **Actions** → **Workflows** → Voir l'historique
- **Insights** → **Dependency graph** → **Dependabot**

---

## 🔐 Sécurité

### Secrets utilisés

| Secret | Usage | Valeur |
|--------|-------|--------|
| `GITHUB_TOKEN` | Authentification GitHub | Automatique |

**Note** : `GITHUB_TOKEN` est automatiquement fourni par GitHub Actions.

### Best Practices

- ✅ Ne jamais hardcoder de secrets dans les workflows
- ✅ Utiliser `${{ secrets.NAME }}` pour les secrets
- ✅ Limiter les permissions au strict nécessaire
- ✅ Activer Dependabot pour les updates de sécurité

---

## 📚 Ressources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Docker Build Push Action](https://github.com/docker/build-push-action)
- [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

---

**Dernière mise à jour** : Janvier 2026  
**Version** : 1.0.0
