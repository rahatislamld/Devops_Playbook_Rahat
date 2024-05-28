# PostgreSQL Installation Guide

This guide outlines the steps to install PostgreSQL and PostgreSQL contrib package on Ubuntu, as well as using Docker Compose to deploy PostgreSQL in a containerized environment.

## Prerequisites
- Ubuntu server
- Access to the server via SSH
- Docker and Docker Compose installed on the server

## Installation Steps (Native)

1. **Update Package Lists:**
    ```bash
    sudo apt update
    ```

2. **Install PostgreSQL and PostgreSQL Contrib Package:**
    ```bash
    sudo apt install postgresql postgresql-contrib
    ```

3. **Check PostgreSQL Service Status:**
    ```bash
    sudo service postgresql status
    ```

## Installation Steps (Docker Compose)

1. **Install Docker:**
    ```bash
    # Install Docker
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    sudo usermod -aG docker $USER
    ```

2. **Install Docker Compose:**
    ```bash
    # Install Docker Compose
    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```

3. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3.8'

    services:
      postgres:
        image: postgres:latest
        container_name: postgres_db
        restart: unless-stopped
        environment:
          POSTGRES_USER: <username>
          POSTGRES_PASSWORD: <password>
          POSTGRES_DB: <database_name>
        ports:
          - "5432:5432"
        volumes:
          - pgdata:/var/lib/postgresql/data

    volumes:
      pgdata:
    ```

4. **Start PostgreSQL with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

5. **Check PostgreSQL Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After running the installation commands, you can verify that PostgreSQL is installed and running by checking its service status or Docker container status.

## Additional Notes

- When using Docker Compose, make sure to replace `<username>`, `<password>`, and `<database_name>` in the docker-compose.yml file with your desired values.
- Docker Compose provides a convenient way to manage PostgreSQL in a containerized environment, with options for configuring volumes, ports, and environment variables.


