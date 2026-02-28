# 🐳 Day 38 – Pull Docker Image from Registry

## 📌 Scenario

The Nautilus DevOps team needed to pull a required Docker image from the Docker registry onto an application server for further deployment testing.

The task was to:

- Pull the specified image
- Ensure it downloads successfully
- Verify the image locally

---

## 🎯 Objectives

- Pull Docker image from Docker Hub / registry
- Verify successful download
- Confirm image availability locally

---

## 🛠️ Tasks Performed

### ✅ 1. Verify Docker Service is Running

```bash
sudo systemctl status docker
```
If not running:

sudo systemctl start docker
✅ 2. Pull Required Docker Image
docker pull <image-name>

Example:

docker pull nginx

Docker output shows layers being downloaded and extracted.

✅ 3. Verify Image Download
docker images

Output confirms:

Image name

Tag

Image ID

Size

✔️ Image successfully available locally.

🚨 Issue Faced

Common issues that can occur:

Docker service not running

Incorrect image name

Network / DNS issues

Permission denied (not in docker group)

🛠️ Fix Applied

Ensured docker service was active

Verified correct image name

Used proper user privileges if required

🧠 Key Learnings

docker pull fetches images from remote registry

Docker images are downloaded layer by layer

Always verify using docker images

Docker must be running before pulling images

Correct image naming is critical

🎤 Interview Questions
Q1. What does docker pull do?

Downloads a Docker image from a registry to the local system.

Q2. Where are Docker images stored locally?

Under Docker’s storage directory (usually /var/lib/docker).

Q3. How to pull a specific version of an image?
docker pull nginx:1.25
Q4. Difference between docker pull and docker run?

docker pull → Only downloads image

docker run → Pulls (if needed) + creates container

Q5. How to list downloaded images?
docker images

✅ Day 38 Task Completed Successfully
