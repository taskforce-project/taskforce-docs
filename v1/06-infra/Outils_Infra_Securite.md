---
id: outils-infra-securite
title: Boîte à outils — Infra, Qualité & Sécurité
doc_type: reference
statut: active
version: 1.0
date: "09/06/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [v1, infra, securite, outils, devsecops, gratuit]
related:
  - "../../Brain_OS.md"
  - "./quickstart/README.md"
  - "../13-roadmap/Roadmap_Backlog.md"
---
<!-- Logo établissement : assets/images/logo_metz_numeric_school.svg | Logo projet : assets/images/logo_taskforce.png -->

# 🧰 Boîte à outils — Infra, Qualité & Sécurité

**Version :** 1.0 · **Date :** 09/06/2026 · **Auteur :** Pierre MICHEL

[![Type: Référence](https://img.shields.io/badge/Type-R%C3%A9f%C3%A9rence-blue?style=for-the-badge)]() [![Focus: Gratuit / OSS](https://img.shields.io/badge/Focus-Gratuit%20%2F%20OSS-brightgreen?style=for-the-badge)]() [![Statut: Actif](https://img.shields.io/badge/Statut-Actif-brightgreen?style=for-the-badge)]()

## Liens rapides
- [🧠 Brain OS](../../Brain_OS.md) · [Architecture §5](../03-architecture/Architecture.md) · [Backlog](../13-roadmap/Roadmap_Backlog.md) · [Schéma visuel](../../assets/infra-toolchain.html)

**Tags :** `#infra` `#securite` `#devsecops` `#outils` `#gratuit`

<p class="lead">
Catalogue exhaustif des outils mobilisables pour mener TaskForce au niveau « ultra pro », en privilégiant
le <strong>gratuit / open-source</strong>. Légende : ✅ déjà utilisé · 🆓 gratuit ou OSS auto-hébergeable ·
◐ free tier (freemium, gratuit jusqu'à un quota). Colonne RNCP = compétence(s) servie(s).
</p>

## 1. Build, conteneurs & orchestration
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Docker, Docker Compose | ✅ | conteneurisation dev/prod | C5/C30 |
| Maven, Node/npm | ✅ | build back / front | C19/C26 |
| Podman | 🆓 | alternative Docker rootless | C30 |
| Kubernetes (k3s, kind) + Helm | 🆓 | orchestration (si scale) | C29/C30 |

## 2. CI/CD & gestion des dépendances
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| GitHub Actions + GHCR | ✅ | pipelines + registre d'images | C19/C26/C31 |
| `act` | 🆓 | exécuter les workflows en local | C26 |
| Dependabot / Renovate | 🆓 | maj automatique des dépendances | C16/C22 |
| release-please / semantic-release | 🆓 | versioning + changelog auto | C26/C27 |

## 3. Tests
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Vitest + React Testing Library + MSW | ✅ | tests unitaires/intégration front | C18 |
| Playwright | 🆓 | E2E navigateur | C18 |
| JUnit 5 + Mockito + AssertJ | ✅ | tests back | C25 |
| Testcontainers | 🆓 | tests d'intégration (PostgreSQL, Keycloak) | C25 |
| REST Assured | 🆓 | tests d'API | C24/C25 |
| k6 / Locust / Gatling | 🆓 | tests de charge/performance | C25/C26 |
| JaCoCo · Vitest coverage · Codecov | ✅/🆓/◐ | couverture ≥ 50 % + rapport | C18/C25 |

## 4. Qualité de code & SAST
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| ESLint + Prettier (ou Biome) | ✅ | lint/format front | C16/C19 |
| Spotless / Checkstyle / PMD | 🆓 | lint/format back | C22/C26 |
| SonarQube Community (self-host) / SonarCloud (public) | 🆓/◐ | qualité + dette + couverture | C19/C26 |
| Semgrep | ✅ | SAST (règles `p/secrets`, OWASP) | C16/C22 |
| CodeQL | 🆓 | SAST avancé (gratuit repos publics) | C24 |

## 5. Sécurité — dépendances (SCA)
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| OWASP Dependency-Check | 🆓 | CVE des dépendances (Java/JS) | C22/C26 |
| Trivy | ✅ | vulnérabilités (deps, images, IaC, secrets) | C26/C30 |
| Grype + Syft (SBOM) | 🆓 | scan vulnérabilités + inventaire SBOM | C26 |
| OSV-Scanner (Google) | 🆓 | CVE multi-écosystèmes | C22 |
| npm audit | ✅ | CVE front | C16 |
| Snyk | ◐ | SCA + remédiation (free tier) | C22 |

## 6. Sécurité — secrets & DAST
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Gitleaks / TruffleHog | 🆓 | détection de secrets (repo + CI + pre-commit) | C21/C24 |
| OWASP ZAP | 🆓 | DAST (scan dynamique de l'app) | C24/C32 |
| Nuclei / Nikto | 🆓 | scan de vulnérabilités web | C32 |
| Burp Suite Community | 🆓 | pentest manuel | C24 |
| Nmap | 🆓 | reconnaissance réseau/ports | C30/C32 |

## 7. Sécurité — conteneurs, IaC & runtime
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Hadolint / Dockle | 🆓 | lint + bonnes pratiques Dockerfile/image | C26/C30 |
| Checkov / tfsec | 🆓 | scan IaC (Terraform, Compose, K8s) | C30 |
| kube-bench / kube-score | 🆓 | durcissement Kubernetes (si utilisé) | C30 |
| Falco | 🆓 | détection d'intrusion runtime | C32 |

## 8. Secrets management (runtime)
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| HashiCorp Vault (OSS) / Infisical (OSS) | 🆓 | coffre de secrets centralisé | C21/C30 |
| SOPS + age | 🆓 | secrets chiffrés versionnés (Git) | C21 |
| GitHub Actions secrets / Doppler | ✅/◐ | secrets CI | C26 |

## 9. Observabilité & supervision
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| SigNoz + OpenTelemetry | ✅ | traces, métriques, logs (OSS) | C32 |
| Prometheus + Grafana + Loki + Tempo | 🆓 | métriques/logs/traces (stack OSS) | C32 |
| Spring Boot Actuator | ✅ | health, metrics, prometheus | C32 |
| Uptime Kuma | 🆓 | monitoring d'uptime (self-host) | C32 |
| Sentry (self-host GlitchTip) | 🆓/◐ | suivi d'erreurs applicatives | C32 |

## 10. Hébergement (gratuit / free tier)
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Oracle Cloud **Always Free** (VM ARM) | 🆓 | héberger toute la stack Docker (gratuit à vie) | C29/C30 |
| Fly.io / Render / Railway | ◐ | PaaS conteneurs (free tier) | C29 |
| Coolify / Dokku (self-host PaaS) | 🆓 | PaaS open-source sur ta VM | C29/C31 |
| Vercel (front) / Netlify · Cloudflare Pages (landing) | ◐ | hébergement front/SSG gratuit | C29 |
| Neon / Supabase (PostgreSQL) | ◐ | Postgres managé free tier | C29 |

## 11. Proxy, TLS, backup & provisioning
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Nginx | ✅ | reverse proxy (prod) | C30 |
| Traefik / Caddy (TLS auto) | 🆓 | proxy + Let's Encrypt automatique | C28/C30 |
| Let's Encrypt / Certbot · Cloudflare Tunnel | 🆓 | certificats TLS + accès sécurisé gratuit | C28 |
| restic / pgBackRest / `pg_dump` · `mc mirror` (MinIO) | 🆓 | sauvegarde/restauration | C9/C32 |
| OpenTofu / Terraform / Ansible | 🆓 | Infrastructure as Code | C30 |

## 12. Socle applicatif & conformité
| Outil | Statut | Rôle | RNCP |
| ----- | :----: | ---- | ---- |
| Keycloak | ✅ | identité OAuth2/OIDC (OSS) | C21/C24 |
| PostgreSQL + pgvector · Redis/Valkey · RabbitMQ · MinIO | ✅/🆓 | données, cache, messaging, stockage | C9/C21 |
| springdoc-openapi · Redoc | ✅/🆓 | documentation d'API | C24/C27 |
| Klaro / CookieConsent (OSS) | 🆓 | bandeau de consentement RGPD | C11 |
| pre-commit · husky + lint-staged · commitlint | 🆓 | garde-fous avant commit | C19/C26 |

---

> **Note Brain OS** — Tâches associées dans le [Backlog](../13-roadmap/Roadmap_Backlog.md) (sections Tests,
> Sécurité, Infra/DevOps). Vue visuelle : [`assets/infra-toolchain.html`](../../assets/infra-toolchain.html).
> Priorité : commencer par ce qui est **gratuit + déjà à moitié en place** (Trivy/Semgrep en CI, Testcontainers,
> Caddy/Let's Encrypt, Oracle Always Free pour l'hébergement).

**Dernière mise à jour :** 09/06/2026 · **Projet :** Taskforce — Metz Numeric School 2025-2026
