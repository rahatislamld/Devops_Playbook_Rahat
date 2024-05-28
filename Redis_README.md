# Redis Installation Guide

This guide outlines the steps to install and configure Redis on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH

## Installation Steps (Native)

1. **Install Required Packages:**
    ```bash
    sudo apt install lsb-release curl gpg
    ```

2. **Add Redis Repository Key:**
    ```bash
    curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
    ```

3. **Add Redis Repository:**
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
    ```

4. **Update Package Lists:**
    ```bash
    sudo apt-get update
    ```

5. **Install Redis:**
    ```bash
    sudo apt-get install redis
    ```

6. **Start Redis Server:**
    ```bash
    sudo systemctl start redis-server
    ```

7. **Enable Redis to Start on Boot:**
    ```bash
    sudo systemctl enable redis-server
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
    version: '3'

    services:
      redis:
        image: redis:latest
        container_name: redis_server
        restart: always
        ports:
          - "6379:6379"
    ```

4. **Start Redis with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

5. **Check Redis Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After running the installation commands, you can verify that Redis is installed and running by checking its service status or Docker container status.

## Additional Configuration

- By default, Redis is configured to listen on localhost (127.0.0.1) on port 6379. 
- You can configure Redis by editing the configuration file located at `/etc/redis/redis.conf`.
- For security, you may want to configure Redis to require authentication. This can be done by setting a password in the configuration file and restarting the Redis service.

## Usage

- Once Redis is installed and running, you can use it as a caching or messaging system for your applications.


