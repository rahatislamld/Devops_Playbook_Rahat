# Kafka Installation Guide

This guide outlines the steps to install Kafka on Ubuntu, including both native installation and using Docker Compose.

## Prerequisites
- Ubuntu server
- Access to the server via SSH
- Default JDK installed on the server

## Installation Steps (Native)

1. **Update Package Lists:**
    ```bash
    sudo apt update 
    ```

2. **Install Default JDK:**
    ```bash
    sudo apt install default-jdk
    ```

3. **Download Kafka from Official Website:**
   - Download Kafka from the [official website](https://kafka.apache.org/downloads) (e.g., kafka_2.13-3.7.0.tgz)
   - Save the downloaded .tgz file to a directory on your Ubuntu server, e.g., `/home/rahat/Downloads`.

4. **Unzip Kafka:**
    ```bash
    tar -xzf /home/rahat/Downloads/kafka_2.13-3.7.0.tgz -C /opt
    ```

5. **Check Zookeeper Status:**
    ```bash
    sudo systemctl status zookeeper
    ```

6. **Create Kafka systemd Service File:**
    ```bash
    sudo nano /etc/systemd/system/kafka.service
    ```
    Paste the following content into the file:
    ```ini
    [Unit]
    Description=Apache Kafka Server
    Documentation=http://kafka.apache.org/documentation.html
    Requires=zookeeper.service

    [Service]
    Type=simple
    Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64"
    ExecStart=/opt/kafka_2.13-3.7.0/bin/kafka-server-start.sh /opt/kafka_2.13-3.7.0/config/server.properties
    ExecStop=/opt/kafka_2.13-3.7.0/bin/kafka-server-stop.sh

    [Install]
    WantedBy=multi-user.target
    ```

7. **Reload systemd Configuration:**
    ```bash
    sudo systemctl daemon-reload
    ```

8. **Start Zookeeper Service:**
    ```bash
    sudo systemctl start zookeeper
    ```

9. **Start Kafka Service:**
    ```bash
    sudo systemctl start kafka
    ```

10. **Check Kafka Service Status:**
    ```bash
    sudo systemctl status kafka
    ```

## Installation Steps (Docker Compose)

1. **Create a Docker Compose file (docker-compose.yml):**
    ```yaml
    version: '3'

    services:
      zookeeper:
        image: confluentinc/cp-zookeeper:latest
        container_name: zookeeper-container

      kafka:
        image: confluentinc/cp-kafka:latest
        container_name: kafka-container
        depends_on:
           - zookeeper
        ports:
           - '9092:9092'
           - '29092:29092'
        environment:
           KAFKA_BROKER_ID: 1
           KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
           KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://localhost:29092
           KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
           KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
           KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    ```

2. **Start Kafka with Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Check Kafka Container Status:**
    ```bash
    docker ps
    ```

## Verifying Installation

- After following the installation steps, you can verify that Kafka is installed and running by checking its service status (for native installation) or container status (for Docker Compose).

## Additional Notes

- Kafka is now running either natively or in Docker containers, depending on the method chosen.
- For native installation, ensure to replace `/home/rahat/Downloads/kafka_2.13-3.7.0.tgz` with the actual download path of Kafka.
- Docker Compose provides a convenient way to manage Kafka in a containerized environment.

