# Docker Services Setup for Monitoring

This repository contains a Docker Compose setup for monitoring services using Prometheus, Grafana, Node Exporter, and a custom Dotnet Application.

## Services

### Prometheus

Prometheus is an open-source monitoring and alerting toolkit. It scrapes metrics from configured targets at specified intervals, evaluates rule expressions, displays the results, and can trigger alerts if some condition is observed to be true.

- **Image:** prom/prometheus:latest
- **Volumes:** ./prometheus.yml:/etc/prometheus/prometheus.yml
- **Ports:** 9090:9090
- **Networks:** monitoring

### Dotnet Application

A custom Dotnet application containerized for deployment.

- **Image:** rahat17/promth:latest
- **Ports:** 80:80
- **Networks:** monitoring

### Grafana

Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics no matter where they are stored.

- **Image:** grafana/grafana:latest
- **Ports:** 3000:3000
- **Volumes:** grafana-data:/var/lib/grafana
- **Environment:** GF_SECURITY_ADMIN_PASSWORD=admin
- **Networks:** monitoring

### Node Exporter

Node Exporter is a Prometheus exporter for hardware and OS metrics exposed by *nix kernels, written in Go with pluggable metric collectors.

- **Image:** prom/node-exporter:latest
- **Container Name:** node-exporter
- **Ports:** 9100:9100
- **Networks:** monitoring
- **Restart:** unless-stopped
- **Volumes:**
  - /proc:/host/proc:ro
  - /sys:/host/sys:ro
  - /:/rootfs:ro
- **Command:**

## Networks

- **Name:** monitoring

## Volumes

- **Name:** grafana-data
