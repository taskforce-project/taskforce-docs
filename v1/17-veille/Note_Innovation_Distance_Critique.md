---
id: note-innovation-distance-critique
title: Note d'innovation & distance critique — TaskForce V1
doc_type: innovation
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [innovation, distance-critique, eco-responsabilite, inclusion, accessibilite, ia, rncp, soutenance]
---

# 💡 Note d'innovation & distance critique — TaskForce V1

> Analyse des **apports innovants** de TaskForce, de la **distance critique** vis-à-vis
> des choix techniques, et de la prise en compte des enjeux transverses
> (éco-responsabilité, inclusion, accessibilité).
>
> **Règle** : rien n'est inventé. Chaque affirmation est ancrée dans du code, une migration,
> ou une décision documentée. Les limites sont nommées sans euphémisme.
>
> **Référentiel** : CERT-C1/C2 RNCP DFS — expertise, innovation, distance critique

---

## 1. Innovations démontrables dans TaskForce

### 1.1 Smart Assign — Assignation dynamique par IA (différenciateur principal)

**Ce qui est habituel dans les PM tools** : assignation manuelle, ou "recommandation" basée sur un simple round-robin / disponibilité de calendrier.

**L'approche TaskForce** : un moteur d'assignation multi-dimensionnel qui calcule un score composite à partir de 5 signaux :

| Signal | Poids | Source |
|---|---|---|
| Similarité sémantique (embedding ↔ profil membre) | 0.45 | pgvector cosine similarity |
| Charge de travail en cours (cross-projets) | 0.22 | `findByWorkspaceSlugAndAssigneeId` |
| Historique d'assignation (taux de résolution) | 0.15 | `assignment_events` |
| Disponibilité en cycle | 0.10 | `CycleService` |
| Correspondance labels | 0.08 | `IssueLabel` |

Le tout est enrichi par un appel LLM (Groq `llama-3.1-8b-instant`) qui génère une **explication en langage naturel** pour chaque suggestion — pas un score opaque.

**Fonctionnalité inédite** : le mode **montée en compétence** (`growth_mode`). Quand activé sur un projet, l'algorithme favorise modérément (bonus borné `+12/+15`) un membre junior dont les compétences cibles (`growth_target_skills`) sont adjacentes à la tâche — à condition que la tâche ne soit pas urgente et que la disponibilité soit ≥ 60 %. Cela permet de faire grandir l'équipe sans sacrifier la vélocité sur les tâches critiques.

**Preuve** : `SmartAssignService.java` (calcul des scores), `V46__member_growth_objectives.sql` (migration growth_enabled + growth_target_skills), `assignment_events` (feedback).

---

### 1.2 Brain OS — Mémoire de workspace native

**Concept** : chaque workspace TaskForce a un **graphe de connaissance intégré** (`knowledge_nodes`, `knowledge_links`). Ce n'est pas un wiki classique : les nœuds (ADR, SOP, FINDING, RUNBOOK…) peuvent pointer vers des issues ou projets réels, et l'IA peut interroger et **écrire dans ce graphe** (write-back).

**Différence avec Confluence/Notion** : la connaissance est liée au workspace par design (pas un espace séparé), et les agents IA ont accès au contexte complet de l'entreprise (décisions + historique + code + métriques) en une seule source de vérité.

**Preuve** : `V50__knowledge_graph_nodes.sql`, `V51__knowledge_graph_links.sql`, `V52__knowledge_graph_tags.sql`, `V53__knowledge_node_versions.sql` — graphe versionné avec support wikilinks et tags.

**Statut V1** : socle complet (graphe + éditeur + recherche sémantique). La génération IA est env-gated (active avec `GROQ_API_KEY`), dégradation gracieuse sans clé.

---

### 1.3 Observabilité orientée sécurité

**Approche originale** : les 9 règles d'alerte Prometheus incluent deux alertes **sécurité-first** — `RateLimitSpike` (montée des 429) et `AuthFailureSpike` (montée des 401 sur `/login`) — pas seulement des alertes d'infrastructure. L'observabilité surveille activement les tentatives de brute-force.

**Preuve** : `observability/alerts/prometheus-rules.yml` — deux groups séparés (infra + sécurité).

---

## 2. Distance critique — ce qui ne va pas (ou pas encore)

La distance critique consiste à nommer honnêtement les limites, sans les minimiser. Elle démontre la maturité d'analyse plutôt qu'un triomphalisme de livraison.

### 2.1 JWT HS512 symétrique — dette architecturale connue (PC-019)

**Problème** : TaskForce génère ses propres JWT HS512 via `JwtService` (io.jsonwebtoken) plutôt que de déléguer les tokens à Keycloak (OIDC natif). Le token est signé avec une clé symétrique (`JWT_SECRET`) — si cette clé fuit, tous les tokens existants sont compromis.

**Ce que l'on aurait dû faire** : laisser Keycloak émettre les tokens (flux OIDC standard avec RS256 asymétrique). Keycloak est déjà en place comme IdP — le glissement vers l'émission JWT custom s'est produit lors de l'implémentation de la logique OTP (besoin de contrôle sur le payload).

**Impact** : moyen en contexte mono-instance (clé protégée en env var), critique en production multi-instances. Documenté comme backlog TF-SEC-009.

**Honnêteté** : ce choix a émergé par pragmatisme de développement, pas par décision délibérée. C'est un contre-exemple ADR — une décision prise sans formalisation qui crée de la dette.

**✅ Résolu (05/07/2026)** : migration effective vers **Keycloak OIDC (RS256)** — `JwtService`/HS512 supprimés, décodeur JWK + validation issuer, refresh/logout natifs IdP. Formalisé a posteriori dans [[Journal_Decisions_ADR]] ADR-011. La dette est donc close ; le récit de sa correction (et le compromis UX assumé : plus d'auto-login post-inscription) illustre la démarche de remédiation.

---

### 2.2 Rate limiting en mémoire — limitation multi-instances

**Problème** : `RateLimitFilter` utilise `ConcurrentHashMap` pour stocker les buckets Bucket4j. En déploiement multi-instances (horizontal scaling), chaque instance a son propre état — un client peut donc contourner le rate limit en alternant entre instances.

**Solution connue** : Bucket4j distributed avec Redis comme store partagé. Documenté TF-SEC-011.

**Pourquoi c'est resté** : l'horizon V1 est mono-instance (VM école ou Render starter). La contrainte ne se matérialise qu'au scale-out. Décision consciente de différer.

**✅ Résolu (05/07/2026)** : `RateLimitFilter` accepte désormais un `ProxyManager` Bucket4j/Lettuce (Redis) partageant les buckets entre instances, avec **fallback local** si `ratelimit.distributed.enabled=false` (dev). Redis ajouté au `docker-compose.prod.yml` + `render.yaml`. TF-SEC-011 clos.

---

### 2.3 Tests de charge absents (STB non validés en latence)

**Problème** : les exigences de performance du STB (PERF-01 : `p95 < 500ms`, PERF-02 : 100 req/s) sont validées en **comportement** (les tests passent) mais pas en **latence réelle** (aucun test de charge k6/Gatling). La `HighLatencyP95` alerte Prometheus est configurée à 1s — ce seuil n'a jamais été challengé en charge.

**Conséquence** : on ne sait pas si le système tient ses SLOs sous charge. Documenté TF-TEST-009.

**Distance** : publier des SLOs sans les avoir mesurés sous charge est une pratique courante dans les startups early-stage — mais c'est une dette de qualité à combler avant mise en production.

---

### 2.4 Groq comme dépendance critique non contractualisée

**Problème** : Smart Assign et l'assistant IA dépendent de Groq Inc. (USA). Aucun DPA formel n'est en place (TF-RGPD-008). La dégradation gracieuse (fallback Java) existe, mais la valeur différenciante du produit dépend de la disponibilité de Groq.

**Distance** : se battre pour l'innovation IA tout en restant RGPD-compliant est une tension réelle — les LLMs performers sont aux USA. La solution à moyen terme est un modèle open-source auto-hébergé (ex. Mistral 7B sur GPU dédié), mais hors portée V1.

---

### 2.5 Suppression Keycloak non automatisée

**Problème** : quand un utilisateur supprime son compte (`GdprService.deleteMyAccount`), son entrée dans Keycloak n'est pas supprimée. L'accès est coupé (`isActive=false` + tokens révoqués), mais l'identité reste dans l'IdP. Documenté TF-RGPD-007.

**Pourquoi** : l'appel à l'API Admin Keycloak au moment de l'effacement aurait été un appel synchrone externe supprimable lors d'un rollback. Décision de sécurité au sens ACID — ne pas introduire une dépendance externe dans une transaction critique. La correction propre est une tâche asynchrone post-effacement.

**✅ Résolu (05/07/2026)** : exactement cette correction — `GdprService.deleteMyAccount` déclenche `KeycloakService.deleteUser` **après commit** de la transaction (`TransactionSynchronization.afterCommit`), tolérant à l'échec (journalisé pour rejeu). L'identité IdP est donc bien effacée sans risque ACID. TF-RGPD-007 clos.

---

## 3. Éco-responsabilité

### 3.1 Choix techniques orientés efficience

| Choix | Impact éco | Justification |
|---|---|---|
| Modèle d'embedding `all-MiniLM-L6-v2` (384d) au lieu d'OpenAI Ada (1536d) | ×4 moins de stockage vectoriel · ×4 moins de calcul cosine | Qualité suffisante intra-workspace — pas besoin d'un modèle général |
| pgvector (PostgreSQL) au lieu d'une base vectorielle dédiée | Un seul processus DB au lieu de deux | Moins de RAM/CPU en production |
| Groq LPU vs GPU standard | Efficience énergétique × 3-10 vs GPU Nvidia | LPU = architecture spécialisée pour l'inférence, non pour l'entraînement |
| SigNoz self-hosted vs Datadog | Aucune transmission de données vers des datacenters tiers | Données restent sur l'infra choisie |
| Alpine base images (`postgres:16-alpine`, `nginx:alpine`) | Images ×3 plus légères → moins de transferts réseau | Réduction du temps de pull CI/CD |

### 3.2 Limites actuelles

- **Pas de mesure de l'empreinte carbone** : aucun outil de mesure (Green Software Foundation API, Scaphandre) n'est intégré. C'est une limite connue pour un projet pédagogique mono-développeur.
- **Groq (USA)** : même si l'inférence est plus efficiente, les données traversent l'Atlantique — impact réseau non mesuré.
- **Docker Compose vs Kubernetes** : sans auto-scaling, les instances tournent à pleine capacité même à faible charge. L'auto-scaling (HPA Kubernetes) est une amélioration post-V1.

---

## 4. Inclusion & accessibilité

### 4.1 Accessibilité implémentée (WCAG 2.1 AA)

| Mesure | Preuve |
|---|---|
| Audit axe-core automatisé en CI (E2E Playwright `a11y.spec.ts`) | `tests/e2e/a11y.spec.ts` — violations WCAG 2.1 AA bloquantes |
| `aria-label` sur tous les boutons iconiques | Commits 05/07/2026 — ajout systématique |
| Navigation clavier | Shadcn/Radix UI — accessibilité clavier native |
| Focus visible | CSS `:focus-visible` dans `globals.css` |
| Thème sombre/clair | `ThemeProvider` — respect `prefers-color-scheme` |
| Contraste de couleurs | Design system avec ratios WCAG AA dans `globals.css` |
| Landing page `/accessibility` dédiée | `landing-page/src/pages/accessibility.astro` |

### 4.2 Limites d'inclusion

- **Langue unique** : l'application TaskForce (app) est en anglais uniquement (constants dans `constants_fr.ts` partiellement remplis). La landing a une bascule EN/FR fonctionnelle, mais pas l'app principale.
- **Accessibilité motrice** : vérifiée clavier/screen-reader sur les parcours principaux ; les vues Kanban drag-and-drop restent difficiles pour les utilisateurs sans souris (pas de fallback clavier pour le drag-and-drop des cartes).
- **Coût des plans** : le modèle freemium avec un plan FREE restrictif peut exclure des équipes à budget limité. C'est une tension business intentionnelle, pas une oubli.

### 4.3 Design inclusif dans Smart Assign

Le mode **montée en compétence** (`growth_mode`) est une fonctionnalité d'inclusion professionnelle : il donne intentionnellement des opportunités aux membres juniors sur des tâches non-critiques, plutôt de toujours assigner les experts. C'est un choix de conception délibéré pour lutter contre le "winner takes all" dans la répartition de tâches.

---

## 5. Synthèse

| Dimension | Forces | Limites identifiées |
|---|---|---|
| **Innovation technique** | Smart Assign multi-dimensionnel · Brain OS · pgvector HNSW · Groq natif Java | ~~JWT symétrique~~ ✅ · ~~Rate limiting mono-instance~~ ✅ (résolus 05/07) |
| **Qualité** | 78 % backend + 92 % frontend · Testcontainers · E2E Playwright | Tests de charge absents (TF-TEST-009) |
| **Sécurité** | OWASP A01-A09 · PSSI · STRIDE · AES-256-GCM · **auth OIDC RS256 (Keycloak)** | DAST CI absent (TF-SEC-010) |
| **RGPD** | Export + anonymisation + registre Art.30 + **effacement IdP Keycloak** | DPA Groq · double opt-in · mentions légales |
| **Éco-responsabilité** | Modèles légers · pgvector · Alpine images | Pas de mesure empreinte carbone |
| **Inclusion** | WCAG 2.1 AA + axe-core CI · Growth mode Smart Assign | App monolingue EN · Drag-and-drop sans fallback clavier |

---

> 🔗 [[Veille_Technologique]] — [[Journal_Decisions_ADR]] — [[PSSI]] — [[Audit_RGPD_Conformite]] —
> [[Roadmap_Backlog]] (TF-SEC-009/011, TF-RGPD-001/007/008, TF-TEST-009)
