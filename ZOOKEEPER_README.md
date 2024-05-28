# Zookeeper Installation Guide

This guide outlines the steps to install Zookeeper on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH
- Docker and Docker Compose installed on the server

## Installation Steps (Native)

1. **Download Apache Zookeeper:**
   - Visit the [Apache Zookeeper download page](https://zookeeper.apache.org/releases.html) and download the desired version of the Apache Zookeeper zip file.
   - Save the downloaded zip file to a directory on your Ubuntu server, e.g., `/home/rahat/Downloads`.

2. **Unzip Apache Zookeeper:**
    ```bash
    unzip /home/rahat/Downloads/apache-zookeeper-3.8.4-bin.zip -d /opt
    ```

3. **Create systemd Service File:**
    ```bash
    sudo nano /etc/systemd/system/zookeeper.service
    ```
    Paste the following content into the file:
    ```ini
    [Unit]
    Description=Apache Zookeeper server
    Documentation=http://zookeeper.apache.org
    Requires=network.target remote-fs.target
    After=network.target remote-fs.target

    [Service]
    Type=simple
    ExecStart=/opt/apache-zookeeper-3.8.4-bin/bin/zkServer.sh start
    ExecStop=/opt/apache-zookeeper-3.8.4-bin/bin/zkServer.sh stop
    Restart=on-abnormal

    [Install]
    WantedBy=multi-user.target
    ```

4. **Reload systemd Configuration:**
    ```bash
    sudo systemctl daemon-reload
    ```

5. **Start Zookeeper Service:**
    ```bash
    sudo systemctl start zookeeper
    ```

6. **Check Zookeeper Service Status:**
    ```bash
    sudo systemctl status zookeeper
    ```

7. **Stop Zookeeper Service:**
    ```bash
    sudo systemctl stop zookeeper
    ```

## Installation Steps (Docker Compose)

1. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3'

    services:
      zookeeper:
        image: confluentinc/cp-zookeeper:latest
        container_name: zookeeper-container
        environment:
           ZOOKEEPER_CLIENT_PORT: 2181
           ZOOKEEPER_TICK_TIME: 2000
        ports:
           - '2181:2181'
    ```

2. **Start Zookeeper with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Check Zookeeper Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After following the installation steps, you can verify that Zookeeper is installed and running by checking its service status (for native installation) or container status (for Docker Compose).

## Additional Notes

- For native installation, ensure to replace `/home/rahat/Downloads/apache-zookeeper-3.8.4-bin.zip` and `/opt/apache-zookeeper-3.8.4-bin` with the actual download path and installation directory of Apache Zookeeper.
- Zookeeper is now running either natively or in a Docker container, depending on the method chosen.
- Docker Compose provides a convenient way to manage Zookeeper in a containerized environment.

