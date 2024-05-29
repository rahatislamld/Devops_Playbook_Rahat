# Load Balancing with Nginx and Docker Compose

This repository contains a Docker Compose setup for load balancing multiple backend services using Nginx.

## Overview

Load balancing is a technique used to distribute incoming network traffic across multiple servers or services to improve reliability, performance, and scalability. Nginx is a powerful web server and reverse proxy that can be used for load balancing.

## Prerequisites

- Docker
- Docker Compose

## Docker Compose Setup

### Step 1: Define Docker Compose Configuration

Create a `docker-compose.yml` file with the following contents:

```yaml
version: "3.8"

services:
  app-dev:
    image: rahat17/loadbalancingnginx:dev
    ports:
      - "5000:80"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development

  app-stage:
    image: rahat17/loadbalancingnginx2:stage
    ports:
      - "5001:80"
    environment:
      - ASPNETCORE_ENVIRONMENT=Staging

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - app-dev
      - app-stage
```

### Step 2: Write The Nginx File

```
events {
    worker_connections 1024;
}

http {
    upstream app_cluster {
        server app-dev:80;
        server app-stage:80;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://app_cluster;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```

## Testing Load Balancing

To test the load balancing setup, follow these steps:

1. Open your browser.
2. Visit the configured URL (e.g., [http://localhost/env](http://localhost)).
3. Hit the URL multiple times by refreshing the page or opening it in multiple tabs/windows.
4. Observe that you receive different data or responses each time you hit the URL.
   - This indicates that Nginx is distributing the requests between the configured backend services (`app-dev` and `app-stage`).
