# 🐳 Day 43 – Deploy Nginx Container with Port Mapping

## 📌 Scenario

The Nautilus DevOps team planned to host an application using an **nginx-based container**.

A task was assigned to deploy an Nginx container on **Application Server 3** with the following requirements:

- Pull `nginx:alpine` image
- Create a container named `news`
- Map host port **3002** to container port **80**
- Keep the container running

---

## 🎯 Objectives

- Pull required nginx image
- Create and run container
- Configure port mapping
- Verify container status

---

## 🛠️ Tasks Performed

### ✅ 1. Pull Nginx Alpine Image

docker pull nginx:alpine
✅ 2. Verify Image Download
docker images

Expected output includes:

nginx   alpine
✅ 3. Run Nginx Container
docker run -d --name news -p 3002:80 nginx:alpine

Explanation:

-d → Run container in background

--name news → Assign container name

-p 3002:80 → Host port 3002 mapped to container port 80

nginx:alpine → Lightweight nginx image

✅ 4. Verify Container Status
docker ps

Expected result:

news   nginx:alpine   Up
✅ Verification

Test nginx service:

curl http://localhost:3002

Expected output:

Welcome to nginx!
🧠 Key Learnings

nginx:alpine is a lightweight nginx image

Port mapping allows external access to container services

Containers should run in detached mode in production

docker ps confirms running containers

Proper naming improves container management

🎤 Interview Questions
Q1. What does -p 3002:80 mean?

Host port 3002 is mapped to container port 80.

Q2. Why use nginx:alpine?

Because it is smaller, faster, and optimized for containers.

Q3. How do you check running containers?
docker ps
Q4. How to stop the container?
docker stop news
Q5. How to remove a container?
docker rm news

✅ Day 43 Task Completed Successfully
