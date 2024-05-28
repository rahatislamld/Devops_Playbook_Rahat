# MongoDB Installation Guide

This guide outlines the steps to install MongoDB on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH

## Installation Steps (Native)

1. **Install Required Packages:**
    ```bash
    sudo apt-get install gnupg curl
    ```

2. **Add MongoDB Repository Key:**
    ```bash
    curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
       sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
       --dearmor
    ```

3. **Update Package Lists:**
    ```bash
    sudo apt-get update
    ```

4. **Install MongoDB:**
    ```bash
    sudo apt-get install -y mongodb-org
    ```

5. **Start MongoDB Service:**
    ```bash
    sudo systemctl start mongod
    ```

6. **Enable MongoDB to Start on Boot:**
    ```bash
    sudo systemctl enable mongod
    ```

7. **Check MongoDB Service Status:**
    ```bash
    sudo systemctl status mongod
    ```

## Installation Steps (Docker Compose)

1. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3'

    services:
      mongodb:
        image: mongo:latest
        container_name: mongodb-container
        ports:
           - '27017:27017'
    ```

2. **Start MongoDB with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Check MongoDB Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After running the installation commands, you can verify that MongoDB is installed and running by checking its service status or Docker container status.

## Additional Notes

- MongoDB will be accessible on port 27017 by default.
- You can configure MongoDB by editing the configuration file located at `/etc/mongod.conf`.
- MongoDB is now ready to be used as a database for your applications.


