# Prometheus & Grafana HA Monitoring Lab

Projekt demonstracyjny monitoringu infrastruktury i aplikacji z wykorzystaniem Prometheus, Grafana oraz Alertmanager.

## Cel projektu

Celem projektu było przygotowanie środowiska monitoringu typu production-ready, które obejmuje:

- Prometheus w trybie High Availability
- Grafana dashboards
- Alertmanager
- Nginx jako load balancer
- Node Exporter
- cAdvisor
- custom application exporter
- alert rules
- monitoring kontenerów
- podstawowe business metrics

## Wykorzystane technologie

- Prometheus
- Grafana
- Alertmanager
- Nginx
- Docker
- Docker Compose
- Node Exporter
- cAdvisor
- Python Flask
- PromQL

## Zakres projektu

Środowisko składa się z następujących komponentów:

- `prometheus-1`
- `prometheus-2`
- `nginx-lb`
- `grafana`
- `alertmanager`
- `node-exporter`
- `cadvisor`
- `custom-app`

## Architektura

- dwie instancje Prometheus pracują równolegle
- Nginx pełni rolę load balancera dla Prometheus
- Grafana korzysta z Prometheus jako datasource
- Alertmanager obsługuje alerty
- Node Exporter zbiera metryki hosta
- cAdvisor zbiera metryki kontenerów
- custom Python app udostępnia własne metryki aplikacyjne

## Struktura projektu

```bash
lesson40-prometheus-grafana-ha/
│
├── docker-compose.yml
├── README.md
│
├── prometheus/
│   └── config/
│       ├── prometheus.yml
│       └── alert_rules.yml
│
├── grafana/
│   └── provisioning/
│       ├── datasources/
│       │   └── prometheus.yml
│       └── dashboards/
│           ├── dashboard.yml
│           ├── infrastructure-overview.json
│           └── business-metrics.json
│
├── alertmanager/
│   └── config/
│       └── alertmanager.yml
│
├── nginx/
│   └── nginx.conf
│
└── app/
    ├── app.py
    └── Dockerfile
```

## Komendy wdrożeniowe

Uruchomienie środowiska:

```bash
docker compose up -d
```

Sprawdzenie kontenerów:

```bash
docker compose ps
```

Sprawdzenie logów:

```bash
docker compose logs -f
```

Zatrzymanie środowiska:

```bash
docker compose down
```

## Dostęp do usług

Prometheus przez load balancer:

```bash
http://localhost:9090
```

Grafana:

```bash
http://localhost:3000
```

Alertmanager:

```bash
http://localhost:9093
```

Custom application:

```bash
http://localhost:5000
```

## Dane logowania do Grafany

```bash
admin / admin123!
```

## Konfiguracja Prometheus

Prometheus zbiera metryki z:

- Prometheus HA instances
- Node Exporter
- cAdvisor
- custom Python application

Przykładowe joby:

- `prometheus-ha`
- `node-exporter`
- `cadvisor`
- `custom-app`

## Alert rules

Przygotowane alerty:

- `HighCPUUsage`
- `DiskSpaceLow`
- `ContainerHighCPU`
- `ContainerHighMemory`

## Grafana dashboards

Przygotowane dashboardy:

- `Infrastructure Overview`
- `Business Metrics`

Dashboardy pokazują między innymi:

- status usług
- CPU usage
- metryki aplikacji
- business metrics
- podstawowe dane kontenerów

## Custom application exporter

Aplikacja Python Flask udostępnia endpoint:

```bash
/metrics
```

Prometheus pobiera z niego metryki aplikacyjne.

## Testowanie

Sprawdzenie custom app:

```bash
curl http://localhost:5000/
```

Sprawdzenie metryk aplikacji:

```bash
curl http://localhost:5000/metrics
```

Sprawdzenie targets w Prometheus:

```bash
curl http://localhost:9090/api/v1/targets
```

## Rezultat projektu

Projekt demonstruje:

- wdrożenie Prometheus HA
- konfigurację load balancingu
- podstawową konfigurację Alertmanager
- provisioning Grafana datasource
- provisioning Grafana dashboards
- monitoring infrastruktury
- monitoring kontenerów
- custom application metrics
- podstawowe alert rules
- praktyczne użycie PromQL w monitoringu DevOps/SRE
