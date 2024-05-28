# Cassandra Installation Guide

This guide outlines the steps to install Cassandra on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH

## Installation Steps (Native)

1. **Download Apache Cassandra GPG Key:**
    ```bash
    curl -o /etc/apt/keyrings/apache-cassandra.asc https://downloads.apache.org/cassandra/KEYS
    ```

2. **Add Cassandra Repository:**
    ```bash
    echo "deb [signed-by=/etc/apt/keyrings/apache-cassandra.asc] https://debian.cassandra.apache.org 41x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
    ```

3. **Update Package Lists:**
    ```bash
    sudo apt-get update
    ```

4. **Install Cassandra:**
    ```bash
    sudo apt-get install cassandra
    ```

5. **Start Cassandra Service:**
    ```bash
    sudo systemctl start cassandra
    ```

6. **Enable Cassandra to Start on Boot:**
    ```bash
    sudo systemctl enable cassandra
    ```

7. **Check Cassandra Service Status:**
    ```bash
    sudo systemctl status cassandra
    ```

## Installation Steps (Docker Compose)

1. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3'

    services:
      cassandra:
        image: cassandra:latest
        container_name: cassandra-container
        ports:
           - '9042:9042'
        environment:
           - CASSANDRA_USER=admin
           - CASSANDRA_PASSWORD=admin
        volumes:
           - ./cassandra:/var/lib/cassandra
    ```

2. **Start Cassandra with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Check Cassandra Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After following the installation steps, you can verify that Cassandra is installed and running by checking its service status (for native installation) or container status (for Docker Compose).

## Additional Notes

- Cassandra is now running either natively or in Docker containers, depending on the method chosen.
- For native installation, Cassandra will be running as a systemd service.
- For Docker Compose, Cassandra is configured with default credentials and a volume for data persistence.
- Docker Compose provides a convenient way to manage Cassandra in a containerized environment.

