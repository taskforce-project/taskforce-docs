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
.\tf.ps1 setup
```

**Linux/Mac :**
```bash
make init-dev
```

### 4️⃣ Démarrer les services

**Windows :**
```powershell
.\tf.ps1 up
```

**Linux/Mac :**
```bash
make dev-up
```

### 5️⃣ Accéder aux services

Une fois les services démarrés (⏱️ ~2 minutes) :

| Service | URL | Identifiants |
|---------|-----|--------------|
| **API Backend** | http://localhost:8080/api | - |
| **Swagger UI** | http://localhost:8080/api/swagger-ui.html | - |
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

### Windows (PowerShell) — launcher unique `tf.ps1`

> Menu interactif : `.\tf.ps1` · liste des clés : `.\tf.ps1 help` · scripts détaillés dans `scripts/`.

```powershell
# Démarrer
.\tf.ps1 up

# Arrêter
.\tf.ps1 down

# Voir les logs
.\tf.ps1 logs

# Rebuild
.\tf.ps1 rebuild

# Nettoyer tout
.\tf.ps1 clean

# Aide
.\tf.ps1 help
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
.\tf.ps1 clean
.\tf.ps1 rebuild
.\tf.ps1 up
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

Ouvrir http://localhost:8080/api/swagger-ui.html

### Via curl

```bash
# Health check
curl http://localhost:8080/api/actuator/health

# Exemple d'endpoint (à adapter selon votre API)
curl http://localhost:8080/api/v1/users
```

---

## 📚 Documentation Complète

- 🧰 [Boîte à outils infra & sécurité](../Outils_Infra_Securite.md)
- 🐳 [Utilisation GHCR / images Docker](../docker/GHCR_USAGE.md)
- 🏗️ [Architecture technique](../../03-architecture/Architecture.md)
- 🔀 [Git Workflow](../../04-engineering/git-workflow/README.md)
- 📖 [Brain OS — Hub](../../../Brain_OS.md)

---

## ❓ Problèmes Courants

### Docker Desktop ne démarre pas

1. Redémarrer Windows/Mac
2. Vérifier que WSL2 est installé (Windows)
3. Vérifier les ressources système

### Port déjà utilisé

```bash
# Voir quel processus utilise le port 8080
# Windows
netstat -ano | findstr :8080

# Linux/Mac
lsof -i :8080
```

### PostgreSQL ne démarre pas

```bash
# Supprimer le volume et recréer
docker volume rm taskforce-postgres-data-dev
.\tf.ps1 up
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
