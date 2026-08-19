---
id: observabilite
title: Observabilité — Métriques, Traces, Logs & Alertes
doc_type: infra
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [observabilite, otel, signoz, prometheus, alertes, traces, logs, memoire, rncp, soutenance]
---

# 📊 Observabilité — Métriques, Traces, Logs & Alertes

> Pile d'observabilité de TaskForce : OpenTelemetry → SigNoz (ClickHouse).
> Dérivé des fichiers `observability/otel-collector-config.yaml` et
> `observability/alerts/prometheus-rules.yml`. Rien n'est inventé.

---

## 1. Architecture d'observabilité

```
┌──────────────────────────────────────────────────────────────────┐
│  Services instrumentés                                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │  Backend    │  │  Frontend   │  │  Conteneurs Docker       │  │
│  │Spring Boot  │  │  (logs API  │  │  (filelog                │  │
│  │OTLP/gRPC    │  │  client)    │  │  /var/lib/docker/…)      │  │
│  └──────┬──────┘  └──────┬──────┘  └───────────┬──────────────┘  │
│         └────────────────┴─────────────────────┘                  │
│                              OTLP gRPC :4317 / HTTP :4318          │
└──────────────────────────────────────────────────────────────────┘
                              │
         ┌────────────────────▼─────────────────────┐
         │   OTel Collector (otel-collector-config)  │
         │  receivers : otlp, filelog, prometheus    │
         │  processors : batch, resourcedetection,   │
         │               signozspanmetrics/delta      │
         └────────────────────┬─────────────────────┘
                              │
         ┌────────────────────▼─────────────────────┐
         │   SigNoz — ClickHouse                     │
         │  signoz_traces · signoz_metrics            │
         │  signoz_logs   · signoz_meter              │
         │  signoz_metadata                           │
         └───────────────────────────────────────────┘
                     │           │           │
                 Traces UI   Métriques   Logs UI
```

---

## 2. OTel Collector — pipelines configurés

Fichier : `observability/otel-collector-config.yaml`

| Pipeline | Receivers | Processors | Exporters |
|---|---|---|---|
| `traces` | `otlp` | `signozspanmetrics/delta`, `batch` | `clickhousetraces`, `metadataexporter`, `signozmeter` |
| `metrics` | `otlp` | `batch` | `signozclickhousemetrics`, `metadataexporter`, `signozmeter` |
| `metrics/prometheus` | `prometheus` | `batch` | `signozclickhousemetrics`, `metadataexporter`, `signozmeter` |
| `logs` | `otlp`, `filelog` | `batch` | `clickhouselogsexporter`, `metadataexporter`, `signozmeter` |
| `metrics/meter` | `signozmeter` | `batch/meter` | `signozclickhousemeter` |

### Collecte Prometheus depuis le backend

```yaml
# otel-collector : scrape /actuator/prometheus
prometheus:
  config:
    global:
      scrape_interval: 60s
    scrape_configs:
      - job_name: otel-collector
        static_configs:
          - targets: [localhost:8888]
```

Le backend Spring Boot expose ses métriques Micrometer sur `/actuator/prometheus`
(job `taskforce-backend` dans les règles d'alerte).

### Histogramme de latence (spans)

Buckets configurés pour le p95 :
`100µs · 1ms · 2ms · 6ms · 10ms · 50ms · 100ms · 250ms · 500ms · 1s · 1.4s · 2s · 5s · 10s · 20s · 40s · 60s`

---

## 3. Journalisation — logs applicatifs

| Type | Source | Pipeline |
|---|---|---|
| **Logs applicatifs** | Slf4j → Spring Boot stdout | `filelog` receiver (fichiers JSON Docker) |
| **Traces HTTP** | Spring Boot Micrometer + OTLP | `traces` pipeline |
| **Erreurs client** | `ClientLogController` → Slf4j | Même pipeline que les logs applicatifs |
| **Audit métier** | `AuditLog` (entité DB) | Accessible via `GET /api/audit` |

Les logs de conteneurs sont collectés depuis `/var/lib/docker/containers/*/*-json.log`
via le `filelog` receiver (poll 200ms, parse format Docker JSON).

---

## 4. Alertes Prometheus — `alerts/prometheus-rules.yml`

4 groupes d'alertes définis, portables Prometheus / SigNoz :

### 4.1 Disponibilité backend

| Alerte | Expression | For | Sévérité |
|---|---|---|---|
| `BackendDown` | `up{job="taskforce-backend"} == 0` | 2 min | critical |
| `HealthDown` | Taux 5xx sur `/actuator/health` > 0 | 3 min | critical |

### 4.2 Erreurs et latence

| Alerte | Expression | For | Sévérité |
|---|---|---|---|
| `HighServerErrorRate` | Taux 5xx > 5 % (excl. `/actuator`) | 5 min | warning |
| `HighLatencyP95` | `histogram_quantile(0.95, …) > 1s` | 5 min | warning |

### 4.3 Saturation

| Alerte | Expression | For | Sévérité |
|---|---|---|---|
| `HighJvmHeap` | Heap JVM > 90 % | 5 min | warning |
| `DbConnectionPoolSaturated` | `hikaricp_connections_pending > 0` | 3 min | warning |
| `HighCpuUsage` | `system_cpu_usage > 0.9` | 5 min | warning |

### 4.4 Sécurité

| Alerte | Expression | For | Sévérité |
|---|---|---|---|
| `RateLimitSpike` | Taux de 429 > 1/5 min | 2 min | warning |
| `AuthFailureSpike` | Taux de 401 sur `/login` > 1/5 min | 3 min | warning |

Les deux alertes de sécurité complètent `RateLimitFilter` (surveillance passive)
en ajoutant une supervision active des tentatives de brute-force.

---

## 5. Métriques exposées (Spring Boot Micrometer)

Le backend expose automatiquement via `spring-boot-starter-actuator` :

| Métrique clé | Description |
|---|---|
| `http_server_requests_seconds_{count,sum,bucket}` | Latence et débit par route |
| `jvm_memory_used_bytes{area="heap"}` | Utilisation heap JVM |
| `jvm_memory_max_bytes{area="heap"}` | Capacité max heap |
| `hikaricp_connections_pending` | File d'attente pool DB |
| `system_cpu_usage` | CPU système |
| `up{job="taskforce-backend"}` | Disponibilité (scrape Prometheus) |

---

## 6. Gaps et cibles

| Gap | ID backlog | Description |
|---|---|---|
| Dashboards SigNoz non documentés | TF-INFRA-005 | L'infra OTEL est en place mais les dashboards SigNoz ne sont pas encore formalisés/exportés |
| Alerting en production | TF-INFRA-005 | Les règles `prometheus-rules.yml` sont définies mais nécessitent un Prometheus+Alertmanager ou SigNoz Alerts en prod |
| Rétention logs (immuabilité) | TF-INFRA-005 | Politique de rétention SigNoz/ClickHouse à définir pour la production |

---

> 🔗 [[Strategie_Hebergement]] — [[Pipeline_CICD]] — [[PSSI]] §6 (journalisation) —
> [[Threat_Model_STRIDE]] (alertes sécu) — [[STB]] §1 (PERF-01) — [[Roadmap_Backlog]] (TF-INFRA-005)
