# 🚀 Quickstart - Taskforce

Guide de démarrage rapide pour développer sur le projet Taskforce.

---

## ⚡ Démarrage en 5 minutes

### 1️⃣ Prérequis

Vérifiez que vous avez :
- ✅ **Docker Desktop** installé et démarré
- ✅ **Git** installé
- ✅ **PowerShell 5.1+** (Windows) ou **Bash** (Linux/Mac)
- ✅ **GitHub CLI** (`gh`) recommandé

### 2️⃣ Cloner le projet

```bash
git clone <votre-repo-url>
cd taskforce-fullstack
```

### 3️⃣ Initialiser l'environnement

**Windows :**
```powershell
.\init-dev.ps1
```

**Linux/Mac :**
```bash
make init-dev
```

### 4️⃣ Démarrer les services

**Windows :**
```powershell
.\docker.ps1 dev-up
```

**Linux/Mac :**
```bash
make dev-up
```

### 5️⃣ Accéder aux services

Une fois les services démarrés (⏱️ ~2 minutes) :

| Service | URL | Identifiants |
|---------|-----|--------------|
| **API Backend** | http://localhost:8081/api | - |
| **Swagger UI** | http://localhost:8081/api/swagger-ui.html | - |
| **Keycloak Admin** | http://localhost:8180 | admin / admin |
| **PostgreSQL** | localhost:5432 | postgres / postgres |
| **pgAdmin** | http://localhost:5050 | admin@taskforce.dev / admin |

---

## 📁 Structure du Projet

```
taskforce-fullstack/
├── backend/
│   └── tf-api/              # API REST Spring Boot
├── frontend/                # Application Next.js
├── landing-page/            # Site vitrine Astro
├── keycloak/                # Configuration Keycloak
├── nginx/                   # Reverse proxy
└── .github/                 # CI/CD workflows
```

---

## 🛠️ Commandes Essentielles

### Windows (PowerShell)

```powershell
# Démarrer
.\docker.ps1 dev-up

# Arrêter
.\docker.ps1 dev-down

# Voir les logs
.\docker.ps1 dev-logs

# Rebuild
.\docker.ps1 dev-build

# Nettoyer tout
.\docker.ps1 dev-clean

# Aide
.\docker.ps1 help
```

### Linux/Mac (Make)

```bash
# Démarrer
make dev-up

# Arrêter
make dev-down

# Voir les logs
make dev-logs

# Rebuild
make dev-build

# Nettoyer tout
make dev-clean

# Aide
make help
```

---

## 🔄 Workflow de Développement

### 1. Créer une branche

```bash
# Feature
git checkout dev
git pull origin dev
git checkout -b feature/ma-feature

# Bugfix
git checkout dev
git pull origin dev
git checkout -b fix/mon-bug
```

### 2. Développer

```bash
# Éditer le code...
git add .
git commit -m "feat: description de ma feature"
git push origin feature/ma-feature
```

### 3. Créer une Pull Request

1. Ouvrir une PR sur GitHub vers `dev`
2. **OBLIGATOIRE** : Ajouter un label `release:*`
   - `release:major` - Breaking changes
   - `release:minor` - Nouvelle feature
   - `release:patch` - Bug fix
3. Remplir le template
4. Attendre la review

---

## 🐛 Debugging

### Voir les logs d'un service

```bash
# Tous les services
docker compose -f docker-compose.dev.yml logs -f

# Un service spécifique
docker logs taskforce-backend-dev -f
docker logs taskforce-postgres-dev -f
docker logs taskforce-keycloak-dev -f
```

### Accéder à un conteneur

```bash
# Backend
docker exec -it taskforce-backend-dev sh

# PostgreSQL
docker exec -it taskforce-postgres-dev psql -U postgres -d taskforce_dev

# Keycloak
docker exec -it taskforce-keycloak-dev sh
```

### Rebuild complet

Si quelque chose ne fonctionne pas :

```powershell
# Windows
.\docker.ps1 dev-clean
.\docker.ps1 dev-build
.\docker.ps1 dev-up
```

```bash
# Linux/Mac
make dev-clean
make dev-build
make dev-up
```

---

## 🧪 Tester l'API

### Via Swagger UI

Ouvrir http://localhost:8081/api/swagger-ui.html

### Via curl

```bash
# Health check
curl http://localhost:8081/api/actuator/health

# Exemple d'endpoint (à adapter selon votre API)
curl http://localhost:8081/api/v1/users
```

---

## 📚 Documentation Complète

- 🔧 [Configuration Environnement](../../../developpeur/quickstart/environment-setup.md)
- 🐳 [Docker Setup Détaillé](../../../developpeur/quickstart/docker-setup.md)
- 🏗️ [Infrastructure Overview](../../../developpeur/infrastructure/overview.md)
- 🔀 [Git Workflow](../../04-engineering/git-workflow/README.md)
- 📖 [Documentation Technique](../../../technique/README.md)

---

## ❓ Problèmes Courants

### Docker Desktop ne démarre pas

1. Redémarrer Windows/Mac
2. Vérifier que WSL2 est installé (Windows)
3. Vérifier les ressources système

### Port déjà utilisé

```bash
# Voir quel processus utilise le port 8081
# Windows
netstat -ano | findstr :8081

# Linux/Mac
lsof -i :8081
```

### PostgreSQL ne démarre pas

```bash
# Supprimer le volume et recréer
docker volume rm taskforce-postgres-data-dev
.\docker.ps1 dev-up
```

---

## 🆘 Besoin d'aide ?

- 📖 [FAQ Complète](../../15-utilisateur/FAQ.md)
- 🐛 [Créer une issue](https://github.com/votre-org/taskforce/issues)
- 💬 Contacter l'équipe

---

**Prochaines étapes** :
1. ✅ Lancer l'environnement local
2. ✅ Tester l'API via Swagger
3. ✅ Créer votre première branche
4. ✅ Faire votre première PR

Bon développement ! 🎉
