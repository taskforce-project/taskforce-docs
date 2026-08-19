---
id: pipeline-cicd
title: Pipeline CI/CD — TaskForce V1
doc_type: devops
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [cicd, github-actions, pipeline, devops, docker, ghcr, release, memoire, rncp, soutenance]
---

# 🚀 Pipeline CI/CD — TaskForce V1

> Description du pipeline d'intégration et de livraison continues, tel qu'il est configuré
> dans `.github/workflows/`. Tout est dérivé des fichiers YAML réels — aucun élément inventé.
>
> **Registre d'images** : GitHub Container Registry (`ghcr.io`) — images poussées à chaque release.
> **Versioning** : indépendant par service (`backend-v*`, `frontend-v*`, `landing-v*`).

---

## 1. Vue d'ensemble — workflows actifs

| Workflow | Fichier | Déclencheur | Rôle |
|---|---|---|---|
| Backend Tests | `backend-tests.yml` | push/PR sur `main`, `dev`, `feature/**`, `fix/**` | Tests JUnit + JaCoCo + Codecov |
| Frontend Tests | `frontend-tests.yml` | push/PR sur `main`, `dev`, `feature/**`, `fix/**` | Vitest + TypeCheck + Build |
| E2E Tests | `e2e-tests.yml` | push/PR | Stack complète + Playwright |
| Release | `release.yml` | push sur `main`, `dev` | Versioning + build images Docker + GitHub Release |
| Landing Tests | `landing-tests.yml` | push/PR | Tests landing page (Astro) |
| Sync README Badges | `sync-readme-badges.yml` | push | Mise à jour badges README |
| Version Management | `version-management.yml` | push | Gestion des tags de version |

---

## 2. Backend Tests (`backend-tests.yml`)

```
push / PR ──▶ setup JDK 21 (Temurin) + cache Maven
           ──▶ ./mvnw clean test jacoco:report
           ──▶ résumé couverture → GITHUB_STEP_SUMMARY
           ──▶ upload Codecov (CODECOV_TOKEN, continue-on-error)
           ──▶ artifacts : jacoco-coverage-report (30 j) + test-results (7 j)
```

**Caractéristiques** :
- `runs-on: ubuntu-latest`, timeout 15 min
- Matrix `java-version: [21]`
- Path filters : `backend/tf-api/**` — ne se déclenche pas sur les commits frontend-only
- `MAVEN_OPTS: -Xmx2048m`
- Le job fail si des tests échouent (`exit 1` final)

---

## 3. Frontend Tests (`frontend-tests.yml`)

3 jobs parallèles (après le premier) :

```
push / PR ──▶ job "test"
              ├── npm ci
              ├── ESLint (continue-on-error)
              ├── Stratégie : PR/dev/main → "full", sinon "changed"
              ├── Vitest (tests ciblés ou complets selon stratégie)
              ├── Coverage → Codecov + artifact (7 j)
              └── Commentaire PR avec tableau de couverture
           ──▶ job "type-check" (parallèle)
              └── tsc --noEmit
           ──▶ job "build" (après test + type-check)
              └── npm run build (NEXT_PUBLIC_API_URL=http://localhost:8080/api)
```

**Seuils commentés sur PR** : Lines 70 %, Functions 70 %, Branches 60 %, Statements 70 %.

---

## 4. E2E Tests (`e2e-tests.yml`)

Stack complète levée sur le runner CI :

```
push / PR ──▶ docker compose -f docker-compose.dev.yml up --build
              (postgres, keycloak, backend, frontend, minio, rabbitmq)
           ──▶ attendre backend healthy (curl /actuator/health, 60 × 5 s)
           ──▶ seed démo (docker exec psql < dev_seed.sql)
           ──▶ attendre frontend (curl :3000, 60 × 5 s)
           ──▶ npm ci + npx playwright install --with-deps chromium
           ──▶ npm run e2e
           ──▶ artifact playwright-report (7 j, même si annulé)
           ──▶ logs docker si échec
```

**Timeout** : 30 min. Déclencheur : push sur `main`, `dev`, `feature/**`, `fix/**`, `test/**` + paths `frontend/**`, `backend/**`, `docker-compose.dev.yml`.

---

## 5. Release (`release.yml`)

Pipeline de release par service, déclenché sur push vers `dev` (RC) et `main` (stable) :

```
push (main/dev) ──▶ job "detect-and-version"
                     ├── Récupère labels de la PR associée au commit
                     ├── Détecte le service modifié (backend/frontend/landing)
                     │   via labels OU git diff HEAD~1
                     ├── Calcule la nouvelle version (SemVer indépendant par service)
                     │   dev → RC : backend-v1.2.0-rc1
                     │   main → stable : backend-v1.2.0
                     └── Crée les tags git (backend-v*, frontend-v*, landing-v*)
                ──▶ jobs "build-backend/frontend/landing" (parallèles, si service modifié)
                     ├── docker/setup-buildx
                     ├── Login GHCR (GITHUB_TOKEN)
                     └── docker/build-push → ghcr.io/{repo}/{service}:{version} + :latest
                         avec cache GHA (cache-from/to: type=gha,mode=max)
                ──▶ job "create-release"
                     └── GitHub Release (prerelease si -rc, draft: false)
```

**Conventions de labels PR** : `backend:release:major|minor|patch`, `frontend:release:major|minor|patch`, `landing:release:major|minor|patch`. Sans label → incrément RC (dev) ou patch (main).

**Images produites** :
```
ghcr.io/{owner}/taskforce/backend:{version}   # ex. backend-v1.3.0
ghcr.io/{owner}/taskforce/backend:latest
ghcr.io/{owner}/taskforce/frontend:{version}
ghcr.io/{owner}/taskforce/frontend:latest
ghcr.io/{owner}/taskforce/landing:{version}
ghcr.io/{owner}/taskforce/landing:latest
```

---

## 6. Schéma du flux complet

```
  Branch feature/* ──▶ backend-tests ──▶ frontend-tests ──▶ e2e-tests
                        (JUnit/JaCoCo)   (Vitest/TSC/Build) (Playwright)

  PR → dev
  ├── tous les tests verts requis avant merge
  └── commentaire coverage Vitest sur PR

  Merge → dev ──▶ release.yml ──▶ RC tags + images GHCR (:*-rc)

  PR → main
  ├── tous les tests verts requis
  └── E2E (stack complète)

  Merge → main ──▶ release.yml ──▶ tags stables + images GHCR (:version + :latest)
```

---

## 7. Gaps et cibles (pipeline)

| Gap | ID backlog | Description |
|---|---|---|
| SAST/SCA non bloquants en CI | TF-SEC-002/003 | Semgrep + Trivy intégrés à `security-scan.ps1` mais pas encore dans un workflow CI dédié |
| DAST non automatisé en CI | TF-SEC-010 | ZAP baseline lancé manuellement avant release |
| Gate de couverture non bloquant | TF-TEST-007 | JaCoCo gate dans `pom.xml` (60 %), Vitest thresholds dans `vitest.config.ts` — pas encore bloquants dans le workflow CI |
| Tests de charge | TF-TEST-009 | k6/Gatling non intégrés |
| CD vers environnement cible | TF-INFRA-004 | Pipeline CI → images GHCR ; le déploiement cible dépend du choix d'hébergement (voir [[Strategie_Hebergement]]) |

---

> 🔗 [[Strategie_Hebergement]] — [[Politique_Tests]] — [[Sécurité]] — [[STB]] §5 (QUAL) —
> [[Roadmap_Backlog]] (TF-INFRA-004, TF-SEC-002/003/010)
