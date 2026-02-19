# 🐳 Day 37 – Copy Files from Docker Host to Container

## 📌 Scenario

The Nautilus DevOps team needed to securely transfer an encrypted file from the Docker host to a running container on **App Server 1**.

A container named `ubuntu_latest` was already running on the same server.

Task was to copy:

/tmp/nautilus.txt.gpg


from host → container `/home/` directory **without modifying the file**.

---

## 🎯 Objectives

- Identify running container
- Copy encrypted file from host to container
- Ensure file integrity
- Verify successful transfer

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to File Location

```bash
cd /tmp
✅ 2. Copy File into Container
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/nautilus.txt.gpg
Explanation:

docker cp → Copy files between host & container

/tmp/nautilus.txt.gpg → Source file on host

ubuntu_latest:/home/ → Destination inside container
```

✅ Verification
Docker confirmed:

Successfully copied 2.05kB to ubuntu_latest:/home/nautilus.txt.gpg
✔️ File transferred successfully.

🚨 Issue Faced
Initially tried:

cp nautilus.txt.gpg ubuntu_latest:/home/
Resulted in error:

No such file or directory
🛠️ Fix Applied
Realized that regular cp does NOT work with Docker containers.

Correct approach:

docker cp
🧠 Key Learnings
Normal cp cannot copy into containers

docker cp is required for host ↔ container transfers

Container paths must exist

Docker provides secure file transfer without modifying data

Always verify container name before copying

🎤 Interview Questions
Q1. Difference between cp and docker cp?
cp → host filesystem
docker cp → host ↔ container filesystem

Q2. How do you copy files into containers?
docker cp <source> <container>:<destination>
Q3. How to list running containers?
docker ps
Q4. Does docker cp change file content?
No — it preserves file integrity.

Q5. When is docker cp useful?
For debugging, backups, configuration injection, and secure file transfers.

✅ Day 37 Task Completed Successfully
