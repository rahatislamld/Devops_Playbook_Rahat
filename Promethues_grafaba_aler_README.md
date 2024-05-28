# Docker Services Setup for Monitoring

This repository contains a Docker Compose setup for monitoring services using Prometheus, Grafana, Node Exporter, and a custom Dotnet Application.

## Docker Compose Setup

```yaml
version: "3"

services:
  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    networks:
      - monitoring

  dotnetapp:
    image: rahat17/promth:latest
    ports:
      - "80:80"
    networks:
      - monitoring

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    volumes:
      - grafana-data:/var/lib/grafana
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    networks:
      - monitoring

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
    networks:
      - monitoring
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.sysfs=/host/sys'
      - '--path.rootfs=/rootfs'

networks:
  monitoring:

volumes:
  grafana-data:


# Docker Services Setup for Monitoring

This repository contains a Docker Compose setup for monitoring services using Prometheus, Grafana, Node Exporter, and a custom Dotnet Application.

## Prometheus Configuration

```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s

scrape_configs:
  - job_name: "dotnet_application"
    honor_timestamps: true
    metrics_path: "/metrics"
    scheme: "http"
    static_configs:
      - targets: ["172.17.0.1:80"]

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
