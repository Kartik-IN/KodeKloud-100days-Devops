# 🐳 Day 35 – Install Docker & Docker Compose

## 📌 Scenario

The Nautilus DevOps team decided to start containerizing applications after discussions with the application development team.  
As a first step, Docker and Docker Compose needed to be installed and initialized on **App Server 1** to enable container-based testing.

---

## 🎯 Objectives

- Install Docker Engine (docker-ce)
- Install Docker Compose
- Start and enable Docker service
- Verify Docker installation

---

## 🛠️ Tasks Performed

### ✅ 1. Install Docker Engine & Docker Compose

```bash
sudo yum install -y docker-ce docker-compose
✅ 2. Start Docker Service
sudo systemctl start docker
✅ 3. Enable Docker at Boot
sudo systemctl enable docker
✅ Verification
Check Docker Service Status
sudo systemctl status docker
Expected result:

Active: active (running)
Verify Docker Version
docker --version
Verify Docker Compose
docker-compose --version
🧠 Key Learnings
Docker daemon must be running before using any Docker commands

systemctl enable docker ensures Docker starts after reboot

Docker Compose simplifies multi-container application management

Containerization is the foundation for modern DevOps workflows

🎤 Interview Questions
Q1. What is Docker?
Docker is a containerization platform that packages applications and their dependencies into lightweight containers.

Q2. Why is Docker Compose used?
Docker Compose is used to define and manage multi-container applications using a single YAML file.

Q3. What happens if Docker service is not running?
Docker commands will fail because the Docker daemon is unavailable.

Q4. Difference between Docker and Docker Compose?
Docker → Manages individual containers

Docker Compose → Manages multi-container applications

✅ Day 36 Completed Successfully
