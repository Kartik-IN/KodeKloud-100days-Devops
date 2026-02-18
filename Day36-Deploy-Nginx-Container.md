# 🐳 Day 36 – Deploy Nginx Container on Application Server

## 📌 Scenario

The Nautilus DevOps team started containerization testing on App Server 1.  
As part of this process, they needed to deploy an Nginx web server using Docker to validate container functionality.

---

## 🎯 Objectives

- Ensure Docker service is running
- Pull Nginx image
- Run Nginx container
- Verify container deployment
- Confirm web server accessibility

---

## 🛠️ Tasks Performed

### ✅ 1. Verify Docker Service

```bash
sudo systemctl status docker
✅ 2. Pull Nginx Image
docker pull nginx
✅ 3. Run Nginx Container
docker run -d --name nginx-container -p 80:80 nginx
Explanation:

-d → Detached mode

--name → Container name

-p 80:80 → Host port mapped to container port

nginx → Image name

✅ Verification
Check Running Containers
docker ps
Test Web Server
curl http://localhost
Expected output:

Welcome to nginx!
🧠 Key Learnings
Docker containers expose services using port mapping

docker ps helps verify running containers

Containers can be deployed in seconds compared to traditional setups

Port binding is mandatory to access container services externally

Containerization simplifies application deployment drastically

🎤 Interview Questions
Q1. What does docker run -d do?
Runs container in background (detached mode).

Q2. Why use -p 80:80?
Maps host port 80 to container port 80.

Q3. How do you check running containers?
Using:

docker ps
Q4. How do you stop a container?
docker stop <container-name>
Q5. Difference between image and container?
Image → Blueprint/template

Container → Running instance of image

✅ Day 36 Completed Successfully
