# Redis Installation Guide

This guide outlines the steps to install and configure Redis on Ubuntu.

## Prerequisites
- Ubuntu server
- Access to the server via SSH

## Installation Steps

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

## Verifying Installation

1. **Check Redis Status:**
    ```bash
    sudo systemctl status redis-server
    ```

2. **Test Redis Connection:**
    ```bash
    redis-cli ping
    ```

    If Redis is running, you should see the response "PONG".

## Additional Configuration

- By default, Redis is configured to listen on localhost (127.0.0.1) on port 6379. 
- You can configure Redis by editing the configuration file located at `/etc/redis/redis.conf`.
- For security, you may want to configure Redis to require authentication. This can be done by setting a password in the configuration file and restarting the Redis service.

## Usage

- Once Redis is installed and running, you can use it as a caching or messaging system for your applications.

