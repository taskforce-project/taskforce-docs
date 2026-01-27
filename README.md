# 📚 Taskforce - Documentation

Documentation complète du projet Taskforce ERP.

---

## 📖 Table des matières

### 🎯 [Gestion de Projet](./projet/)
- [Dossier Projet](./projet/Dossier_Projet.md) - Vue d'ensemble et objectifs
- [Cahier des Charges Fonctionnel](./projet/02_CdCF.md) - Spécifications fonctionnelles
- [Cahier des Charges Technique](./projet/03_CdCT.md) - Spécifications techniques
- [Étude Business](./projet/Etude_business.md) - Analyse de marché

### 🛠️ [Documentation Technique](./technique/)
- **Architecture & Infrastructure**
  - [Architecture](./technique/Architecture.md) - Architecture globale du système
  - [API Documentation](./technique/API.md) - Spécifications des API
  - [Sécurité](./technique/Sécurité.md) - Stratégie de sécurité
  - [PS/PCA/PRA](./technique/PS_PCA_PRA.md) - Plans de continuité

- **Développement & Qualité**
  - [Tests](./technique/Tests.md) - Stratégie de tests
  - [Cahier de Tests & Recettes](./technique/Cahier_Test_Recettes.md)
  - [DevOps](./technique/DevOps.md) - Pipeline CI/CD

### 👥 [Documentation Utilisateur](./utilisateur/)
- [Manuel Utilisateur](./utilisateur/Manuel_Utilisateur.md)
- [Guide d'Installation](./utilisateur/Guid_Installation.md)
- [FAQ](./utilisateur/FAQ.md)
- [Release Notes](./utilisateur/Release_Notes.md)

### 🚀 [Documentation Développeur](./developpeur/)
- **Démarrage**
  - [Quickstart Guide](./developpeur/quickstart/README.md)
  - [Configuration Environnement](./developpeur/quickstart/environment-setup.md)
  - [Docker Setup](./developpeur/quickstart/docker-setup.md)

- **Infrastructure**
  - [Infrastructure Overview](./developpeur/infrastructure/overview.md)
  - [Services Docker](./developpeur/infrastructure/docker-services.md)

- **Git & CI/CD**
  - [Workflow Git](./developpeur/git-workflow/README.md)
  - [GitHub Actions](./developpeur/git-workflow/github-actions.md)
  - [Gestion des Versions](./developpeur/git-workflow/versioning.md)
  - [Pull Requests](./developpeur/git-workflow/pull-requests.md)
  - [Setup Initial](./developpeur/git-workflow/setup.md)

- **Docker & Images**
  - [Utilisation GHCR](./developpeur/docker/GHCR_USAGE.md) - Pull et test des images Docker

---

## 🎯 Guides Rapides

### Pour les développeurs
```bash
# Cloner le projet
git clone <votre-repo>
cd taskforce-fullstack

# Lancer l'environnement de dev
.\init-dev.ps1
.\docker.ps1 dev-up
```

👉 [Guide complet de démarrage](./developpeur/quickstart/README.md)

### Pour créer une PR
1. Créer une branche depuis `dev`
2. Ajouter un label `release:*` (major/minor/patch)
3. Remplir le template de PR

👉 [Guide des Pull Requests](./developpeur/git-workflow/pull-requests.md)

---

## 📊 Vue d'ensemble du projet

**Taskforce** est un ERP modulaire moderne construit avec :
- **Backend**: Spring Boot 3.4.1 (Java 21)
- **Frontend**: Next.js 15
- **Auth**: Keycloak 23
- **Database**: PostgreSQL 16
- **Infrastructure**: Docker, GitHub Actions

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│           Taskforce Fullstack                   │
│                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │PostgreSQL│  │ Keycloak │  │ Backend  │     │
│  │  :5432   │◄─┤  :8180   │◄─┤  :8081   │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│                                                 │
│  ┌──────────┐  ┌──────────┐                   │
│  │ Frontend │  │ Landing  │                   │
│  │  :3000   │  │  :4321   │                   │
│  └──────────┘  └──────────┘                   │
└─────────────────────────────────────────────────┘
```

👉 [Architecture détaillée](./technique/Architecture.md)

---

## 📝 Contribution

### Workflow Git

1. **Branches**:
   - `main` - Production stable
   - `dev` - Développement (RC versions)
   - `feature/*` - Nouvelles fonctionnalités
   - `fix/*` - Corrections de bugs
   - `hotfix/*` - Corrections urgentes

2. **Versioning**: Semantic Versioning automatique
   - `v1.0.0` - Version stable
   - `v1.0.0-rc1` - Release Candidate

3. **Labels obligatoires** sur PR:
   - `release:major` - Breaking changes
   - `release:minor` - Nouvelles features
   - `release:patch` - Bug fixes

👉 [Documentation complète Git Workflow](./developpeur/git-workflow/README.md)

---

## 🔗 Liens Utiles

- **Code Source**: [taskforce-fullstack](../taskforce-fullstack/)
- **API Swagger**: http://localhost:8081/api/swagger-ui.html
- **Keycloak Admin**: http://localhost:8180
- **pgAdmin**: http://localhost:5050

---

## 📞 Support

Pour toute question :
- 📖 Consultez la [FAQ](./utilisateur/FAQ.md)
- 🐛 Créez une [issue](https://github.com/votre-org/taskforce/issues)
- 📧 Contactez l'équipe

---

**Dernière mise à jour**: Janvier 2026  
**Version**: 1.0.0
