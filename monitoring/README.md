# **Infrastructure Monitoring Stack**

## Overview

This repository provides a complete monitoring and alerting stack built with **Prometheus**, **Loki**, **Grafana**, and **Alertmanager**. It includes metric collection, log aggregation, visualization dashboards, and alert routing. The setup is designed to monitor system health, container performance, application metrics, and external endpoints, providing deep observability across infrastructure and services.

## Components

* **Prometheus**
  Central monitoring engine that collects metrics from various exporters and evaluates alert rules.

* **Alertmanager**
  Handles alert notifications from Prometheus and routes them to email and Microsoft Teams.

* **Grafana**
  Visualization layer for metrics and logs with customizable dashboards.

* **Loki**
  Log aggregation system that integrates with Grafana for real-time log analysis.

* **Grafana Alloy**
  Collects and forwards logs from local services and system components to Loki.

* **Prometheus-MSTeams**
  Webhook relay to send alerts from Alertmanager to Microsoft Teams channels.

### Exporters Integrated

* **node\_exporter** – Hardware and operating system metrics
* **cAdvisor** – Container-level CPU, memory, network, and storage metrics
* **Blackbox Exporter** – Probes external HTTP(S), TCP, ICMP endpoints for availability and latency
* **Speedtest Exporter** – Measures download, upload, and ping metrics from speed tests
* **Traefik Exporter** – Collects reverse proxy metrics and HTTP routing stats
* **NGINX Exporter** – Gathers NGINX request/connection statistics
* **RabbitMQ Exporter** – Tracks queues, messages, and throughput for RabbitMQ
* **JVM Exporter** – Java Virtual Machine metrics (heap usage, GC time, threads, etc.)
* **MySQL (Percona) Exporter** – Monitors MySQL/MariaDB performance and queries
* **PostgreSQL Exporter** – Collects PostgreSQL-specific metrics
* **Elasticsearch Exporter** – Retrieves health, performance, and index stats from Elasticsearch


## Architecture

* **Prometheus** scrapes metrics from all integrated exporters.

* **Grafana Alloy** collects logs and sends them to **Loki**.

* **Alertmanager** routes Prometheus alerts to:

  * Email
  * Microsoft Teams (via Prometheus-MSTeams)

* **Grafana** connects to:

  * **Prometheus** for metrics
  * **Loki** for logs

* Metrics and logs are collected locally, without reliance on external scraping targets.

* Network access to Prometheus is secured; the web UI is not exposed publicly.

* Grafana is accessible over HTTPS via a reverse proxy.

## Alerts

The following alerts are pre-configured:

* **High CPU Usage** – Triggers when CPU usage exceeds 85% for more than 2 minutes
* **High Memory Usage** – Alerts if memory usage exceeds 85%
* **High Load Average** – Based on CPU core count thresholds
* **Disk Space Low** – Alerts when disk space drops below 10% available
* **Node Down** – When a monitored instance becomes unreachable
* **High System Temperature** – Alerts if system temperature exceeds 85°C
* **Blackbox Probe Failure** – Triggers if an endpoint fails to respond within 2 minutes
* **HTTP Response Errors** – Unexpected HTTP status codes for monitored services
* **Container Lifecycle** – Alerts on container stops, removals, or frequent restarts


## Author

**Hassaan Bin Tariq**
