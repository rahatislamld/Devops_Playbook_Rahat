# Elasticsearch Installation Guide

This guide outlines the steps to install Elasticsearch on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH

## Installation Steps (Native)

1. **Add Elasticsearch GPG Key:**
    ```bash
    curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
    ```

2. **Add Elasticsearch Repository:**
    ```bash
    sudo add-apt-repository "deb https://artifacts.elastic.co/packages/7.x/apt stable main"
    ```

3. **Update Package Lists:**
    ```bash
    sudo apt-get update
    ```

4. **Install Elasticsearch:**
    ```bash
    sudo apt-get install elasticsearch
    ```

5. **Start Elasticsearch Service:**
    ```bash
    sudo systemctl start elasticsearch
    ```

6. **Enable Elasticsearch to Start on Boot:**
    ```bash
    sudo systemctl enable elasticsearch
    ```

## Installation Steps (Docker Compose)

1. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3'

    services:
      elasticsearch:
        image: docker.elastic.co/elasticsearch/elasticsearch:7.15.2
        container_name: elasticsearch
        environment:
           - discovery.type=single-node
           - xpack.security.enabled=false
        ports:
           - '9200:9200'
           - '9300:9300'
        volumes:
           - esdata:/usr/share/elasticsearch/data

    volumes:
      esdata:
    ```

2. **Start Elasticsearch with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Check Elasticsearch Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After following the installation steps, you can verify that Elasticsearch is installed and running by checking its service status (for native installation) or container status (for Docker Compose).

## Additional Notes

- Elasticsearch is now running either natively or in Docker containers, depending on the method chosen.
- For native installation, Elasticsearch will be running as a systemd service.
- For Docker Compose, Elasticsearch is configured to run in a single-node mode with disabled security features.
- Docker Compose provides a convenient way to manage Elasticsearch in a containerized environment.

