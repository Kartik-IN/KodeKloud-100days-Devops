# 🐳 Day 41 – Create Custom Docker Image with Apache (Port 6000)

## 📌 Scenario

The Nautilus application development team required a custom Docker image for testing purposes.

DevOps team was asked to:

- Create a Dockerfile at `/opt/docker/Dockerfile` on App Server 3
- Use `ubuntu:24.04` as base image
- Install Apache2
- Configure Apache to run on port **6000**
- Avoid modifying other Apache configurations (like document root)

---

## 🎯 Objectives

- Create Dockerfile with proper base image
- Install apache2
- Modify Apache to listen on port 6000 only
- Build custom image successfully
- Validate configuration

---

## 🛠️ Tasks Performed

### ✅ 1. Create Docker Directory

```bash
sudo mkdir -p /opt/docker
cd /opt/docker
```
✅ 2. Create Dockerfile
sudo vi Dockerfile
✅ 3. Dockerfile Configuration
FROM ubuntu:24.04

RUN apt update && \
    apt install -y apache2 && \
    sed -i 's/Listen 80/Listen 6000/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost *:6000>/' /etc/apache2/sites-available/000-default.conf

EXPOSE 6000

CMD ["apachectl", "-D", "FOREGROUND"]
🔍 Explanation

FROM ubuntu:24.04 → Base image

apt install apache2 → Install Apache

sed commands → Update only port configuration

EXPOSE 6000 → Document container port

apachectl -D FOREGROUND → Keep Apache running in container

✅ 4. Build Docker Image
docker build -t custom-apache:6000 .
✅ 5. Verify Image
docker images

Confirmed image:

custom-apache   6000
🧠 Key Learnings

Dockerfile ensures reproducible builds

Apache must run in foreground inside containers

Port change requires modifying both:

ports.conf

VirtualHost file

EXPOSE does not publish port automatically

Docker images should be built declaratively (not via commit)

🎤 Interview Questions
Q1. Why use apachectl -D FOREGROUND?

Containers require a foreground process to stay running.

Q2. What does EXPOSE do?

Documents container port but does not publish it.

Q3. Why not use service apache2 start in Dockerfile?

Because containers don’t use systemd and background services cause container exit.

Q4. Why modify both ports.conf and VirtualHost?

Apache binds based on both configurations.

Q5. Difference between docker commit and Dockerfile?

Dockerfile → Reproducible build

docker commit → Snapshot of container

✅ Day 41 Task Completed Successfully
