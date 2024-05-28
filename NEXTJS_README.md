# MyWebAppNext Deployment Guide

This guide outlines the steps to deploy your Next.js web application using both traditional deployment and Docker.

## Prerequisites
- Ubuntu server
- Access to the server via SSH
- Node.js and npm installed on the server
- SCP utility installed on your local machine
- Docker installed on the server

## Deployment Steps (General Way)

1. **Update Ubuntu Packages:**
    ```bash
    sudo apt update
    ```

2. **Install Node.js and npm:**
    ```bash
    sudo apt install nodejs npm
    ```

3. **Install pnpm:**
    ```bash
    sudo npm install -g pnpm
    ```

4. **Install project dependencies:**
    ```bash
    pnpm i
    ```

5. **Run the application in development mode:**
    ```bash
    npm run dev
    ```

6. **Transfer Application Files to Server Using SCP:**
    ```bash
    scp -i /home/rahat/Downloads/test-key.pem -r /home/rahat/Desktop/Nextbuild/* ubuntu@13.214.218.152:/home/ubuntu/nextmanualdeploy
    ```

7. **Connect to the Server and Navigate to Deployment Directory:**
    ```bash
    ssh -i /home/rahat/Downloads/test-key.pem ubuntu@13.214.218.152
    cd /home/ubuntu/nextmanualdeploy
    ```

8. **Install project dependencies on the server:**
    ```bash
    npm i
    ```

9. **Navigate to the application directory on the server:**
    ```bash
    cd /home/ubuntu/nextmanualdeploy
    ```

10. **Start the application on the server:**
    ```bash
    npm start
    ```

## Deployment Steps (Docker)

1. **Update Ubuntu Packages:**
    ```bash
    sudo apt-get update
    ```

2. **Build Docker Image:**
    ```bash
    docker build -t nextjs .
    ```

3. **Tag Docker Image:**
    ```bash
    docker tag nextjs rahat17/nextjs:latest
    ```

4. **Push Docker Image to Docker Hub:**
    ```bash
    docker login -u rahat17
    docker push rahat17/nextjs:latest
    ```

5. **View Docker Images:**
    ```bash
    docker images
    ```

6. **Run Docker Container:**
    ```bash
    docker run -d -p 3002:3000 rahat17/nextjs:latest
    ```

7. **View Running Containers:**
    ```bash
    docker ps
    ```

## Additional Notes

- Ensure that necessary ports are open on your server to allow incoming traffic to your web application.
- Make sure to handle any environment-specific configurations such as database connections, API endpoints, etc., before deploying to production.

