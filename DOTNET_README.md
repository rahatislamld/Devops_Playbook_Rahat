# MyWebApp Deployment Guide

This guide outlines the steps to deploy your .NET web application using the dotnet SDK and SCP.

## Prerequisites

- Ubuntu server
- Access to the server via SSH
- dotnet SDK 8.0 installed on the server
- SCP utility installed on your local machine

## Deployment Steps

1. **Update Ubuntu Packages:**

   ```bash
   sudo apt-get update
   ```

2. **Install .NET SDK 8.0:**

   ```bash
   sudo apt-get install -y dotnet-sdk-8.0
   ```

3. **Create a new .NET Web Application:**

   ```bash
   dotnet new web -n MyWebApp
   ```

4. **Navigate to the Application Directory:**

   ```bash
   cd MyWebApp
   ```

5. **Build the Application:**

   ```bash
   dotnet build
   ```

6. **Run the Application:**

   ```bash
   dotnet run
   ```

7. **Transfer Application Files to Server Using SCP:**

   ```bash
   scp -i /home/rahat/Downloads/test-key.pem -r /home/rahat/Desktop/out/* ubuntu@13.214.218.152:/home/ubuntu/dotnettdeploy
   ```

8. **Connect to the Server and Navigate to Deployment Directory:**

   ```bash
   ssh -i /home/rahat/Downloads/test-key.pem ubuntu@13.214.218.152
   cd /home/ubuntu/dotnettdeploy
   ```

9. **Navigate to Application Directory:**

   ```bash
   cd out
   ```

10. **Run the Application on the Server:**
    ```bash
    dotnet MyWebApp.dll
## Deployment Steps (Docker)

1. **Update Ubuntu Packages:**
    ```bash
    sudo apt-get update
    ```

2. **Install Docker:**
    ```bash
    sudo apt install docker.io
    ```

3. **Grant Docker Permissions:**
    ```bash
    sudo chown $USER /var/run/docker.sock
    ```

4. **Build Docker Image:**
    ```bash
    docker build -t dotnet .
    ```

5. **Tag Docker Image:**
    ```bash
    docker tag dotnet rahat17/dotnet
    ```

6. **Push Docker Image to Docker Hub:**
    ```bash
    docker login -u rahat17
    docker push rahat17/dotnet    ```

## Additional Notes

- Ensure that necessary ports are open on your server to allow incoming traffic to your web application.
- Make sure to handle any environment-specific configurations such as database connections, API endpoints, etc., before deploying to production.

