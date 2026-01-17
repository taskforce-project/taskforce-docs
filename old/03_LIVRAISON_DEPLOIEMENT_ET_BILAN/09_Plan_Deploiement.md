# Plan de déploiement

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire

- [1. Introduction](#1-introduction)
- [2. Objectifs du déploiement](#2-objectifs-du-déploiement)
- [3. Environnement de déploiement](#3-environnement-de-déploiement)
- [4. Pré-requis](#4-pré-requis)
- [5. Étapes de déploiement](#5-étapes-de-déploiement)
- [6. Gestion des risques](#6-gestion-des-risques)
- [7. Plan de communication](#7-plan-de-communication)
- [8. Suivi post-déploiement](#8-suivi-post-déploiement)
- [9. Annexes](#9-annexes)

---

## 1. Introduction

### 1.1 Objectif du Document
Ce document décrit le processus complet de déploiement de l'application **TaskForce** en environnement de production. Il couvre la préparation, l'exécution, la validation et le suivi post-déploiement.

### 1.2 Portée
Le déploiement concerne :
- Backend (Spring Boot API)
- Frontend (Next.js Application)
- Base de données PostgreSQL
- Infrastructure (Serveur, Docker, Nginx)

---

## 2. Objectifs du déploiement

### 2.1 Objectifs Principaux
1. **Mise en production du MVP** : Livraison de la version 1.0 fonctionnelle
2. **Disponibilité** : Application accessible 24/7
3. **Sécurité** : Déploiement sécurisé (HTTPS, secrets protégés)
4. **Performance** : Temps de réponse optimaux (< 200ms API)
5. **Fiabilité** : Zero downtime lors des mises à jour futures

### 2.2 Indicateurs de Succès
- ✅ Application accessible sur l'URL de production
- ✅ Tous les tests E2E passent en production
- ✅ Aucune erreur critique dans les logs (24h post-déploiement)
- ✅ Performance conforme aux SLA (< 200ms p95)

---

## 3. Environnement de déploiement

### 3.1 Architecture Cible

```
┌─────────────────────────────────────────────────────┐
│                    INTERNET                          │
└───────────────────┬─────────────────────────────────┘
                    │
┌───────────────────┴─────────────────────────────────┐
│              SERVEUR (On-premise)                    │
│                                                      │
│  ┌──────────────────────────────────────────────┐  │
│  │          Nginx (Reverse Proxy + SSL)         │  │
│  │         Port 80 → 443 (HTTPS)                │  │
│  └──────────────────┬───────────────────────────┘  │
│                     │                                │
│  ┌──────────────────┴───────────────────────────┐  │
│  │              Docker Compose                   │  │
│  │                                               │  │
│  │  ┌──────────────┐  ┌─────────────────────┐  │  │
│  │  │  Frontend    │  │  Backend (API)       │  │  │
│  │  │  (Next.js)   │  │  (Spring Boot)       │  │  │
│  │  │  Port 3000   │  │  Port 8080           │  │  │
│  │  └──────────────┘  └──────────┬───────────┘  │  │
│  │                               │               │  │
│  │  ┌────────────────────────────┴───────────┐  │  │
│  │  │     PostgreSQL Database               │  │  │
│  │  │     Port 5432 (interne)                │  │  │
│  │  └────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────┘  │
│                                                      │
│  ┌──────────────────────────────────────────────┐  │
│  │          File Storage (Local)                 │  │
│  │          /var/taskforce/uploads               │  │
│  └──────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────┘
```

### 3.2 Configuration Serveur

**Serveur On-Premise**
- **OS** : Ubuntu Server 22.04 LTS (ou Debian 12)
- **CPU** : 4 vCores minimum (8 recommandé)
- **RAM** : 8 GB minimum (16 GB recommandé)
- **Stockage** : 100 GB SSD
- **Réseau** : IP publique fixe

**Nom de Domaine** : taskforce.local (ou custom domain)

### 3.3 Environnements

| Environnement | URL | Usage |
|:--------------|:----|:------|
| **Development** | localhost:3000 | Développement local |
| **Staging** | staging.taskforce.local | Tests pré-production (optionnel) |
| **Production** | taskforce.local | Production publique |

---

## 4. Pré-requis

### 4.1 Infrastructure

**Logiciels à installer sur le serveur** :
- Docker Engine 24.x+
- Docker Compose 2.x+
- Nginx 1.24+
- Certbot (Let's Encrypt pour SSL)
- Git

**Installation Rapide** :
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Docker
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER

# Install Docker Compose
sudo apt install docker-compose-plugin -y

# Install Nginx
sudo apt install nginx -y

# Install Certbot
sudo apt install certbot python3-certbot-nginx -y

# Install Git
sudo apt install git -y
```

### 4.2 Configuration DNS

**Enregistrements DNS à créer** :
```
A Record :
taskforce.local → [IP_PUBLIQUE_SERVEUR]

(Optionnel si staging)
staging.taskforce.local → [IP_PUBLIQUE_SERVEUR]
```

### 4.3 Secrets et Variables d'Environnement

**Fichier `.env.production` (Backend)** :
```env
# Database
DATABASE_URL=jdbc:postgresql://postgres:5432/taskforce_prod
DATABASE_USERNAME=taskforce_user
DATABASE_PASSWORD=<STRONG_PASSWORD>

# JWT
JWT_SECRET=<RANDOM_256_BIT_KEY>
JWT_EXPIRATION=86400000

# Server
SERVER_PORT=8080
SPRING_PROFILES_ACTIVE=prod

# File Storage
UPLOAD_DIR=/app/uploads

# CORS
ALLOWED_ORIGINS=https://taskforce.local
```

**Fichier `.env.production` (Frontend)** :
```env
NEXT_PUBLIC_API_URL=https://taskforce.local/api
NEXT_PUBLIC_WS_URL=wss://taskforce.local/ws
```

**⚠️ Sécurité** : Ne jamais commit ces fichiers ! Utiliser `.gitignore`.

---

## 5. Étapes de déploiement

### 5.1 Phase de Préparation (Sprint 23)

#### Étape 1 : Préparation du Serveur

```bash
# Se connecter au serveur
ssh user@<IP_SERVEUR>

# Créer répertoire de l'application
sudo mkdir -p /var/taskforce
sudo chown $USER:$USER /var/taskforce
cd /var/taskforce

# Créer répertoires de données
mkdir -p data/postgres uploads logs
```

#### Étape 2 : Configuration Nginx

```bash
sudo nano /etc/nginx/sites-available/taskforce
```

**Contenu** :
```nginx
server {
    listen 80;
    server_name taskforce.local;
    
    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name taskforce.local;
    
    # SSL Configuration (Certbot will fill this)
    ssl_certificate /etc/letsencrypt/live/taskforce.local/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/taskforce.local/privkey.pem;
    
    # Frontend (Next.js)
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    
    # Backend API
    location /api {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    
    # WebSocket
    location /ws {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
    }
}
```

**Activation** :
```bash
sudo ln -s /etc/nginx/sites-available/taskforce /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### Étape 3 : Obtenir Certificat SSL

```bash
sudo certbot --nginx -d taskforce.local
```

### 5.2 Phase de Build (Sprint 24)

#### Étape 4 : Cloner le Repository

```bash
cd /var/taskforce
git clone https://github.com/taskforce-project/taskforce-fullstack.git
cd taskforce-fullstack
git checkout main
```

#### Étape 5 : Configuration Docker Compose

**Fichier `docker-compose.prod.yml`** :
```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16-alpine
    container_name: taskforce-postgres-prod
    environment:
      POSTGRES_DB: taskforce_prod
      POSTGRES_USER: taskforce_user
      POSTGRES_PASSWORD: ${DATABASE_PASSWORD}
    volumes:
      - /var/taskforce/data/postgres:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    restart: unless-stopped
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U taskforce_user"]
      interval: 10s
      timeout: 5s
      retries: 5

  backend:
    build:
      context: ./backend/tf-api
      dockerfile: Dockerfile
    container_name: taskforce-backend-prod
    environment:
      - SPRING_PROFILES_ACTIVE=prod
      - DATABASE_URL=jdbc:postgresql://postgres:5432/taskforce_prod
      - DATABASE_USERNAME=taskforce_user
      - DATABASE_PASSWORD=${DATABASE_PASSWORD}
      - JWT_SECRET=${JWT_SECRET}
    volumes:
      - /var/taskforce/uploads:/app/uploads
      - /var/taskforce/logs:/app/logs
    ports:
      - "8080:8080"
    depends_on:
      postgres:
        condition: service_healthy
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/actuator/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
      args:
        - NEXT_PUBLIC_API_URL=https://taskforce.local/api
        - NEXT_PUBLIC_WS_URL=wss://taskforce.local/ws
    container_name: taskforce-frontend-prod
    ports:
      - "3000:3000"
    depends_on:
      - backend
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000"]
      interval: 30s
      timeout: 10s
      retries: 3
```

#### Étape 6 : Créer les Variables d'Environnement

```bash
cd /var/taskforce/taskforce-fullstack
nano .env.prod
```

**Contenu** :
```env
DATABASE_PASSWORD=<GÉNÉRER_PASSWORD_FORT>
JWT_SECRET=<GÉNÉRER_SECRET_256BIT>
```

### 5.3 Phase de Déploiement (Sprint 24)

#### Étape 7 : Build et Lancement

```bash
# Build des images
docker-compose -f docker-compose.prod.yml build

# Lancement des conteneurs
docker-compose -f docker-compose.prod.yml up -d

# Vérifier les logs
docker-compose -f docker-compose.prod.yml logs -f
```

#### Étape 8 : Initialisation de la Base de Données

```bash
# Les migrations Flyway s'exécutent automatiquement au démarrage
# Vérifier dans les logs backend :
docker-compose -f docker-compose.prod.yml logs backend | grep Flyway
```

#### Étape 9 : Création du Compte Administrateur

```bash
# Se connecter au conteneur backend
docker exec -it taskforce-backend-prod bash

# Utiliser un script SQL ou endpoint dédié
# (À prévoir dans le code : /api/admin/init avec token secret)
```

### 5.4 Phase de Validation (Sprint 24)

#### Étape 10 : Tests de Validation

**Tests Manuels** :
1. ✅ Accéder à https://taskforce.local
2. ✅ Créer un compte
3. ✅ Se connecter
4. ✅ Créer un projet
5. ✅ Créer une tâche
6. ✅ Uploader un fichier
7. ✅ Ajouter un commentaire
8. ✅ Vérifier les notifications

**Tests Automatisés** :
```bash
# Exécuter les tests E2E en pointant vers la prod
npm run test:e2e:prod
```

#### Étape 11 : Smoke Tests

```bash
# Test de santé API
curl https://taskforce.local/api/actuator/health

# Réponse attendue : {"status":"UP"}
```

---

## 6. Gestion des risques

### 6.1 Risques Identifiés et Mitigations

| Risque | Probabilité | Impact | Mitigation |
|:-------|:------------|:-------|:-----------|
| **Panne serveur pendant déploiement** | Faible | Critique | Snapshot VM avant déploiement |
| **Migration DB échoue** | Moyen | Majeur | Backup complet DB avant migration |
| **Certificat SSL invalide** | Faible | Majeur | Tester Certbot en staging d'abord |
| **Performance dégradée** | Moyen | Moyen | Tests de charge préalables (Sprint 20) |
| **Config incorrecte (secrets)** | Moyen | Critique | Double vérification + checklist |

### 6.2 Plan de Rollback

**En cas d'échec critique** :

```bash
# 1. Arrêter les conteneurs
docker-compose -f docker-compose.prod.yml down

# 2. Restaurer la version précédente (si update)
git checkout tags/v0.9.0
docker-compose -f docker-compose.prod.yml up -d

# 3. Restaurer la base de données
docker exec -i taskforce-postgres-prod psql -U taskforce_user taskforce_prod < backup_pre_deploy.sql
```

**Durée estimée du rollback** : < 10 minutes

---

## 7. Plan de communication

### 7.1 Communication Pré-Déploiement

**Audience** : AMOA (Cédric Brasseur), MNS

**Message** :
```
Objet : Déploiement TaskForce MVP - 25 Mai 2026

Bonjour,

Le déploiement de la version 1.0 de TaskForce est prévu le 25 mai à 14h00.

Durée estimée : 2 heures
Fenêtre de maintenance : 14h00-16h00

L'application sera accessible à l'URL : https://taskforce.local

Merci de votre compréhension.

Pierre MICHEL
```

### 7.2 Communication Post-Déploiement

**Annonce de mise en production** :
```
Objet : ✅ TaskForce MVP déployé avec succès

Bonjour,

Le déploiement de TaskForce v1.0 est terminé avec succès.

✅ Application accessible : https://taskforce.local
✅ Tous les tests de validation OK
✅ Performance conforme aux attentes

Vous pouvez dès maintenant créer votre compte et explorer l'application.

Support : pierre.michel@taskforce.local

Cordialement,
Pierre MICHEL
```

---

## 8. Suivi post-déploiement

### 8.1 Monitoring (48h post-déploiement)

**Actions quotidiennes** :
1. ✅ Vérifier les logs d'erreurs
   ```bash
   docker-compose -f docker-compose.prod.yml logs --tail=100 backend
   ```

2. ✅ Vérifier la disponibilité
   ```bash
   curl -I https://taskforce.local
   ```

3. ✅ Surveiller l'usage disque
   ```bash
   df -h
   ```

4. ✅ Monitorer la charge CPU/RAM
   ```bash
   docker stats
   ```

### 8.2 Indicateurs à Suivre

| Métrique | Seuil Alerte | Action si Dépassé |
|:---------|:-------------|:-------------------|
| CPU > 80% | 5 min continu | Investiguer + optimiser |
| RAM > 90% | - | Augmenter ressources |
| Disk > 85% | - | Nettoyer logs/uploads |
| Erreurs 5xx > 5/min | - | Check logs + rollback si critique |
| Temps réponse > 500ms | - | Investiguer perf |

### 8.3 Plan de Support

**Heures de support** : Lun-Ven 9h-18h (pendant 2 semaines post-MVP)

**Canal** : Email pierre.michel@taskforce.local

**Engagement** :
- Réponse sous 4h (bugs bloquants)
- Réponse sous 24h (bugs mineurs)
- Hotfix sous 8h (critiques)

---

## 9. Annexes

### 9.1 Checklist de Déploiement

**Pré-Déploiement** :
- [ ] Backup base de données effectué
- [ ] Snapshot serveur créé
- [ ] Variables d'environnement configurées
- [ ] Certificat SSL valide
- [ ] Tests E2E passent en staging

**Déploiement** :
- [ ] Code cloné/pull (branch main)
- [ ] Images Docker buildées
- [ ] Conteneurs lancés sans erreur
- [ ] Migrations DB OK
- [ ] Compte admin créé

**Post-Déploiement** :
- [ ] Smoke tests OK
- [ ] Tests manuels validation OK
- [ ] Logs sans erreur critique
- [ ] Performance conforme (< 200ms)
- [ ] Communication envoyée

### 9.2 Commandes Utiles

```bash
# Logs en temps réel
docker-compose -f docker-compose.prod.yml logs -f

# Redémarrer un service
docker-compose -f docker-compose.prod.yml restart backend

# Voir les ressources
docker stats

# Nettoyer les images inutilisées
docker system prune -a

# Backup DB
docker exec taskforce-postgres-prod pg_dump -U taskforce_user taskforce_prod > backup_$(date +%Y%m%d).sql

# Restore DB
docker exec -i taskforce-postgres-prod psql -U taskforce_user taskforce_prod < backup.sql
```

### 9.3 Procédure de Mise à Jour Future

```bash
# 1. Backup
docker exec taskforce-postgres-prod pg_dump -U taskforce_user taskforce_prod > backup_pre_update.sql

# 2. Pull nouvelle version
cd /var/taskforce/taskforce-fullstack
git pull origin main

# 3. Rebuild
docker-compose -f docker-compose.prod.yml build

# 4. Redéploiement avec zero downtime (optionnel : blue-green)
docker-compose -f docker-compose.prod.yml up -d --no-deps --build backend frontend

# 5. Vérifier
docker-compose -f docker-compose.prod.yml ps
docker-compose -f docker-compose.prod.yml logs -f
```

---

**Dernière mise à jour** : Décembre 2025  
**Responsable Déploiement** : Pierre MICHEL
