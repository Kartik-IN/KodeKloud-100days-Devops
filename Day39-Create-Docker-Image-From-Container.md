# 🐳 Day 39 – Create Docker Image from Running Container

## 📌 Scenario

One of the Nautilus developers was testing new changes inside a running container and wanted to preserve those changes.

The DevOps team was asked to:

- Create a new Docker image from the running container
- Tag it as `beta:xfusion`
- Perform this task on Application Server 1
- Ensure the image is created successfully

Container name: `ubuntu_latest`

---

## 🎯 Objectives

- Identify running container
- Create a new image from container state
- Tag the image properly
- Verify image creation

---

## 🛠️ Tasks Performed

### ✅ 1. Verify Running Container

```bash
docker ps
```
Confirmed container:

ubuntu_latest
✅ 2. Create Image from Container
docker commit ubuntu_latest beta:xfusion

This command creates a new image from the current state of the container.

✅ 3. Verify Image Creation
docker images

Confirmed image:

beta   xfusion

✔️ Image successfully created.

🚨 Common Mistakes

Using wrong container ID/name

Forgetting image tag format

Trying to commit stopped container

Not verifying with docker images

🧠 Key Learnings

docker commit creates an image from a container’s current state

Images preserve filesystem + changes made inside container

Tag format: repository:tag

Always verify using docker images

This method is useful for quick backups but not recommended for production CI/CD workflows (Dockerfile is better practice)

🎤 Interview Questions
Q1. What does docker commit do?

Creates a new Docker image from a container’s current state.

Q2. Why is docker commit not preferred in production?

Because it does not provide version-controlled, reproducible builds like a Dockerfile.

Q3. How do you tag an image properly?
repository:tag

Example:

beta:xfusion
Q4. How to verify image creation?
docker images
Q5. What is the difference between Dockerfile build and docker commit?

Dockerfile → Declarative, reproducible

docker commit → Snapshot of container state

✅ Day 39 Task Completed Successfully
