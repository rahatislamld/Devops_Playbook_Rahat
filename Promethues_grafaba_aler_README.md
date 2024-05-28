# Project Name

This project aims to integrate Prometheus, Grafana, and Node Exporter to monitor metrics of a .NET application.

## Installation

1. Install the `prometheus-net` package to your .NET project:

   ```bash
   dotnet add package prometheus-net
   ```

2. Add the necessary function to your project for exposing metrics.

3. Write the required Docker Compose files for running Prometheus, Grafana, and Node Exporter.

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
      - "--path.procfs=/host/proc"
      - "--path.sysfs=/host/sys"
      - "--path.rootfs=/rootfs"

networks:
  monitoring:

volumes:
  grafana-data:
```

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

  - job_name: "node-exporter"
    static_configs:
      - targets: ["node-exporter:9100"]
```

## Docker Compose Setup for Node Exporter

```yaml
version: "3.8"

services:
  node_exporter:
    image: prom/node-exporter:latest
    container_name: node_exporter
    ports:
      - "9100:9100"
    networks:
      - monitoring
    restart: unless-stopped

networks:
  monitoring:
    driver: bridge
```

## Accessing Prometheus

- Access Prometheus using: [http://localhost:9090](http://localhost:9090)
- Navigate to `Status` -> `Targets` to view targets and their health.

## Accessing Grafana

- Access Grafana using: [http://localhost:3000](http://localhost:3000)
- Add Prometheus as a new data source in Grafana.
- Create a new dashboard and specify the Prometheus URL to connect Grafana with Prometheus.
- Visualize metrics and create dashboards to monitor your application's performance.

## Additional Notes

- Ensure that all services are up and running before accessing Prometheus and Grafana.
- Customize Grafana dashboards and alerts as per your monitoring requirements.

## Troubleshooting

- If encountering issues, refer to the documentation of Prometheus, Grafana, and Node Exporter for troubleshooting steps.

This repository contains a Docker Compose setup for monitoring services using Prometheus, Grafana, Node Exporter, and a custom Dotnet Application.

```

```
