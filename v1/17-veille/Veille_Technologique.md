---
id: veille-technologique
title: Veille technologique — TaskForce V1
doc_type: veille
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [veille, technologie, groq, spring-boot, nextjs, pgvector, signoz, e10, c12, rncp, soutenance]
---

# 🔭 Veille technologique — TaskForce V1

> Méthodologie de veille pratiquée durant le développement de TaskForce (Oct 2025 → Jul 2026)
> et entrées tracées ayant influencé des décisions d'architecture ou de développement réelles.
> Toutes les entrées sont démontrables : elles correspondent à un ADR, une migration, ou un
> composant présent dans le code.
>
> **Référentiel** : C12/E10 RNCP DFS — critère « veille technologique »

---

## 1. Méthodologie de veille

### 1.1 Objectifs

La veille technologique sur TaskForce couvre trois axes :
1. **Stabilité du stack** : suivre les évolutions des technologies utilisées (breaking changes, nouvelles versions)
2. **Opportunités d'amélioration** : identifier des patterns ou outils pouvant améliorer la qualité, la performance ou la sécurité
3. **Tendances IA/LLM** : surveiller l'évolution rapide des APIs de LLM (Groq, Anthropic, OpenAI) et des outils vectoriels

### 1.2 Sources surveillées

| Catégorie | Source | Fréquence | Format |
|---|---|---|---|
| **Releases officielles** | GitHub releases (Spring Boot, Next.js, Keycloak, pgvector, RabbitMQ) | Hebdomadaire | RSS / GitHub Watch |
| **Documentation officielle** | spring.io/blog, nextjs.org/blog, docs.keycloak.org | À chaque release majeure | Direct |
| **Communautés** | GitHub Discussions, Reddit r/SpringBoot, r/reactjs, r/selfhosted | Mensuelle | Navigation manuelle |
| **Sécurité** | CNIL, OWASP Top 10, CVE (NVD), GitHub Dependabot | Hebdomadaire | Newsletter / RSS |
| **IA/LLM** | blog.groq.com, Hugging Face Blog, Anthropic News | Hebdomadaire | Newsletter |
| **Observabilité** | signoz.io/blog, opentelemetry.io/blog | Mensuelle | Direct |

### 1.3 Processus de traitement

```
Découverte → Évaluation (pertinence + effort) → Expérimentation (branche feature)
    → Décision ADR (si structurante) → Implémentation → Documentation
```

**Critères d'évaluation** :
- La technologie apporte-t-elle une valeur démontrée pour TaskForce ?
- La migration est-elle réalisable en contexte solo (charge, risque de régression) ?
- La technologie est-elle stable / production-ready ?

### 1.4 Outillage de veille

- **GitHub Watch + Notifications** : releases, issues de sécurité (Dependabot alerts)
- **GitHub Dependabot** : activé sur `backend/` et `frontend/` — alertes CVE automatiques
- **npm audit / OWASP Dependency-Check** : intégré dans `security-scan.ps1`
- **OWASP ZAP** : scan DAST (`security-scan.ps1 -Dast`)

---

## 2. Entrées de veille — impact démontrés

### VT-001 — Spring Boot 4 + Java 21 Virtual Threads (Project Loom)

| Champ | Valeur |
|---|---|
| **Date de découverte** | Octobre 2025 |
| **Source** | spring.io/blog + release notes Spring Boot 4.0 RC |
| **Sujet** | Spring Boot 4.0 arrive avec support natif de Java 21 et des Virtual Threads (Project Loom) |
| **Impact sur TaskForce** | ADR-001 : choix de Spring Boot 4.0-SNAPSHOT + Java 21 LTS comme stack backend |

**Contexte de veille** : en octobre 2025, Spring Boot 4 est en Release Candidate. L'annonce de la prise en charge officielle de Java 21 LTS et des Virtual Threads (Project Loom) est un signal fort : cette version apporte une scalabilité I/O-bound native (un Virtual Thread par requête HTTP, sans pool de threads) sans réécrire le code existant.

**Points de vigilance surveillés** :
- Spring Boot 4 introduit des breaking changes par rapport à SB3 (Jakarta EE 10, package renaming `javax` → `jakarta`) — conséquence directe sur toutes les annotations JPA
- `spring-security` : refonte partielle de l'autoconfiguration OAuth2 Resource Server
- Keycloak Adapter SB4 : le `keycloak-spring-boot-adapter` officiel n'est plus maintenu pour SB4 → adopter la configuration Resource Server native Spring Security (ADR-003)

**Décision documentée** : [[Journal_Decisions_ADR]] ADR-001

**Preuve dans le code** :
```xml
<!-- backend/tf-api/pom.xml -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>4.0.0-SNAPSHOT</version>
</parent>
<java.version>21</java.version>
```

---

### VT-002 — Groq API : inférence LLM ultra-rapide (GroqCloud)

| Champ | Valeur |
|---|---|
| **Date de découverte** | Janvier 2026 |
| **Source** | blog.groq.com + HuggingFace Daily Papers |
| **Sujet** | Groq propose une API LLM avec des latences ×10 inférieures à OpenAI grâce à son LPU (Language Processing Unit) |
| **Impact sur TaskForce** | ADR-004 : remplacement du microservice Python par un appel direct Java → Groq |

**Contexte de veille** : la Phase 4 (Smart Assign) nécessitait un LLM pour générer des explications en langage naturel et scorer les candidats. Deux approches étaient évaluées :
1. Microservice Python (`ai-service`) avec FastAPI + Ollama/local model
2. API externe LLM (OpenAI / Anthropic / Groq)

La veille sur Groq a révélé un différenciateur majeur : les latences de génération (Llama 3.1 8B → **~150 tokens/s** sur Groq, vs ~30 tokens/s sur OpenAI) rendent l'UX Smart Assign interactive (réponse < 1s). Le tier gratuit de GroqCloud (14,400 requêtes/jour) couvre les besoins du prototype.

**Décision documentée** : [[Journal_Decisions_ADR]] ADR-004

**Preuve dans le code** :
```java
// GroqConfig.java
@Value("${groq.api-key}")
private String apiKey;

@Value("${groq.base-url:https://api.groq.com/openai/v1}")
private String baseUrl;
```
```yaml
# application-dev.yml
groq:
  api-key: ${GROQ_API_KEY}
  smart-assign-model: llama-3.1-8b-instant
  assistant-model: llama-3.1-70b-versatile
```

**Suivi post-implémentation** :
- Janvier 2026 : Groq annonce `llama-3.1-70b-versatile` → adopté pour l'assistant conversationnel (contexte plus riche nécessaire)
- Février 2026 : surveillance des limites de rate (429) — gestion de fallback Java (`fallbackAnswer`) ajoutée
- **Risque surveillé** : Groq est une API tierce — changement de prix ou depreciation de modèle possible. Fallback Java garanti (`fallbackAnswer` — jamais de 500).

---

### VT-003 — pgvector : recherche vectorielle native PostgreSQL

| Champ | Valeur |
|---|---|
| **Date de découverte** | Mars 2026 |
| **Source** | github.com/pgvector/pgvector releases + Hacker News |
| **Sujet** | pgvector 0.7.0 introduit l'index HNSW (Hierarchical Navigable Small World) — ×100 plus rapide que l'index IVFFlat précédent |
| **Impact sur TaskForce** | ADR-005 : adoption de pgvector avec index HNSW pour les embeddings de profils membres et documents RAG |

**Contexte de veille** : lors de la conception de la couche IA (Phase 4), le choix du stockage vectoriel était structurant. Trois options :
1. **Pinecone** (SaaS) — payant, transfert de données hors UE, incompatible RGPD strict
2. **Weaviate / Qdrant** — bases vectorielles dédiées, overhead opérationnel supplémentaire
3. **pgvector** (extension PostgreSQL) — intégration native dans la DB existante, pas de nouveau service

La veille sur la release pgvector 0.7.0 (mars 2026) a été déterminante : l'index HNSW change la donne pour la recherche de similarité en production (< 10ms p95 sur 100k vecteurs). L'adoption dans PostgreSQL 18 est officielle.

**Décision documentée** : [[Journal_Decisions_ADR]] ADR-005

**Preuve dans le code** :
```sql
-- V33__member_skill_profiles.sql
embedding vector(384),
-- Index HNSW cosine similarity
CREATE INDEX idx_member_skill_profiles_embedding
    ON member_skill_profiles USING hnsw (embedding vector_cosine_ops)
    WITH (m = 16, ef_construction = 64);
```
```sql
-- V32__ai_documents.sql
embedding vector(384),
CREATE INDEX idx_ai_documents_embedding
    ON ai_documents USING hnsw (embedding vector_cosine_ops)
    WITH (m = 16, ef_construction = 64);
```

**Modèle d'embedding** : `all-MiniLM-L6-v2` (384 dimensions) — équilibre qualité/performance, open-source, pas de dépendance à une API externe.

---

### VT-004 — SigNoz : alternative open-source à Datadog

| Champ | Valeur |
|---|---|
| **Date de découverte** | Février 2026 |
| **Source** | signoz.io/blog + CNCF Landscape |
| **Sujet** | SigNoz v0.45 supporte nativement OpenTelemetry avec ClickHouse comme storage — alternative open-source à Datadog/New Relic |
| **Impact sur TaskForce** | ADR-010 : adoption de SigNoz comme backend d'observabilité, couplé à OpenTelemetry Collector |

**Contexte de veille** : une pile d'observabilité était nécessaire pour la production (traces, métriques, logs, alertes). Datadog (~$15/host/mois) et New Relic sont hors budget pour un projet pédagogique. La veille sur SigNoz a révélé :
- Support natif OTLP (pas d'agent propriétaire)
- ClickHouse comme storage columnaire (requêtes analytiques rapides sur les logs)
- Mode self-hosted gratuit (image Docker)
- Dashboard pré-configurés pour Spring Boot et JVM

**Décision documentée** : [[Journal_Decisions_ADR]] ADR-010

**Preuve dans le code** : `observability/otel-collector-config.yaml` — 5 pipelines exportant vers SigNoz ClickHouse, 9 règles d'alerte Prometheus dans `observability/alerts/prometheus-rules.yml`.

---

### VT-005 — OWASP Top 10 2025 & recommandations CNIL cookies

| Champ | Valeur |
|---|---|
| **Date de découverte** | Continue (Nov 2025 → Jul 2026) |
| **Source** | owasp.org/Top10, cnil.fr/recommandations, ANSSI guides |
| **Sujet** | OWASP A01-A09 coverage + recommandation CNIL sur les cookies (bannière obligatoire pour cookies non-essentiels) |
| **Impact sur TaskForce** | PSSI (couverture OWASP A01-A09) + Plan_Securisation_SSDLC + Audit_RGPD_Conformite (gap bannière cookies TF-RGPD-001) |

**Points de veille appliqués** :

| Source | Recommandation | Application dans TaskForce |
|---|---|---|
| OWASP A01 — Broken Access Control | Anti-IDOR, isolation par workspace | `WorkspaceAccessInterceptor`, `AuthorizationService.getMemberOrThrow` |
| OWASP A02 — Cryptographic Failures | AES-256-GCM pour PII libres, TLS | `EncryptedStringConverter`, nginx TLS |
| OWASP A07 — Identification Failures | Rate limiting, OTP inscription | `RateLimitFilter` Bucket4j, `OtpVerificationService` |
| CNIL recommandation cookies | Bannière consentement active pour cookies non-essentiels | ⚠️ Gap identifié → TF-RGPD-001 |
| ANSSI — JWT | Algorithme HS512 (symétrique) déconseillé en production → migrer vers RS256 ou utiliser OIDC natif Keycloak | PC-019 → [[Roadmap_Backlog]] TF-SEC-009 |

**Preuve dans le code** : `SecurityConfig.applySecurityHeaders()` — 6 headers OWASP appliqués sur toutes les réponses (CSP `default-src 'none'`, HSTS 31536000s, X-Frame-Options DENY, nosniff, Referrer-Policy, Permissions-Policy).

---

### VT-006 — Next.js + React 19 : Server Actions et Compiler

| Champ | Valeur |
|---|---|
| **Date de découverte** | Novembre 2025 |
| **Source** | nextjs.org/blog + react.dev/blog |
| **Sujet** | React 19 GA (Dec 2024) : `use()`, Server Actions stables, React Compiler (optimisation automatique des re-renders) |
| **Impact sur TaskForce** | Choix Next.js 16.1 + React 19 comme stack frontend (ADR implicite — pas d'ADR dédié) |

**Contexte** : React 19 apporte `use()` pour les promesses, les Server Actions stables, et le React Compiler (ex-Forget) qui élimine automatiquement les `useMemo`/`useCallback` manuels. Next.js 16 intègre tout cela nativement avec le `app/` router.

**Impact observé sur TaskForce** :
- Architecture `app/` router avec layouts (`layout.tsx`) et loading UI (`loading.tsx`)
- Stores Zustand simplifiés (React Compiler optimise les re-renders sans annotation manuelle)
- `"use client"` / `"use server"` directement dans les composants

**Surveillance continue** : mise à jour Dependabot pour `next` et `react` — aucun breaking change critique en V1.

---

## 3. Tableau de synthèse

| ID | Technologie | Découverte | Impact | ADR |
|---|---|---|---|---|
| VT-001 | Spring Boot 4 + Java 21 Virtual Threads | Oct 2025 | Stack backend + Virtual Threads | ADR-001 |
| VT-002 | Groq API LLM (GroqCloud) | Jan 2026 | Smart Assign + Assistant IA | ADR-004 |
| VT-003 | pgvector HNSW (PostgreSQL 18) | Mar 2026 | Recherche vectorielle Smart Assign | ADR-005 |
| VT-004 | SigNoz open-source observability | Fév 2026 | Stack observabilité OTel→SigNoz | ADR-010 |
| VT-005 | OWASP Top 10 + CNIL cookies | Continu | PSSI, sécurité, gap TF-RGPD-001 | — |
| VT-006 | Next.js 16 + React 19 | Nov 2025 | Stack frontend | — |

---

> 🔗 [[Journal_Decisions_ADR]] — [[PSSI]] — [[Architecture_C4]] — [[Roadmap_Backlog]] —
> [[Note_Innovation_Distance_Critique]]
