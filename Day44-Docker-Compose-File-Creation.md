# 🐳 Day 44 – Create Docker Compose File

## 📌 Scenario

The Nautilus DevOps team wanted to simplify container deployment using **Docker Compose**.  
Instead of running multiple Docker commands manually, they needed a **docker-compose.yml** file to define and run services in a structured way.

The task was to create a Docker Compose configuration and deploy containers using it.

---

## 🎯 Objectives

- Create a `docker-compose.yml` file
- Define service configuration
- Deploy container using Docker Compose
- Verify container status

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Project Directory

```bash
cd /opt/docker
```
✅ 2. Create Docker Compose File
Bash
Copy code
vi docker-compose.yml
✅ 3. Configure Compose File
Example configuration:
YAML
Copy code
version: '3'

services:
  web:
    image: nginx:latest
    container_name: nginx_compose
    ports:
      - "8080:80"
Explanation:
version → Compose file version
services → Defines containers
image → Docker image used
container_name → Custom container name
ports → Host-to-container port mapping
✅ 4. Start Containers Using Compose
Bash
Copy code
docker compose up -d
This command:
Creates container
Starts service
Runs container in detached mode
✅ 5. Verify Running Containers
Bash
Copy code
docker ps
Expected container:
Copy code

nginx_compose
✅ Verification
Test service:
Bash
Copy code
curl http://localhost:8080
Expected output:
Copy code

Welcome to nginx!
🧠 Key Learnings
Docker Compose manages multi-container applications
docker-compose.yml defines services declaratively
Compose simplifies container orchestration
Containers can be deployed using a single command
Useful for development and testing environments
🎤 Interview Questions
Q1. What is Docker Compose?
A tool used to define and run multi-container Docker applications using YAML configuration.
Q2. What command starts services defined in compose file?
Bash
Copy code
docker compose up
Q3. How do you stop containers created by Compose?
Bash
Copy code
docker compose down
Q4. Why use Docker Compose?
Simplifies multi-container setups
Improves reproducibility
Easier service management
Q5. Where is Docker Compose configuration stored?
Inside docker-compose.yml.
✅ Day 44 Task Completed Successfully
