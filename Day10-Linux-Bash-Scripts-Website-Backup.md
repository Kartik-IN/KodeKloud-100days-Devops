# 🐧 Day 10 – Linux Bash Scripts | Website Backup Automation

## 📌 Scenario
The production support team at xFusionCorp Industries required an automated solution to back up a static website hosted on App Server 1.

A Bash script was created to:
- Compress the website directory into a zip archive.
- Store the backup locally.
- Transfer the backup securely to a remote backup server.
- Execute without manual password input.

---

## 🎯 Objective
- Write a Bash script for automated website backup.
- Compress website files into a zip archive.
- Store the archive in `/backup`.
- Transfer the archive to Nautilus Backup Server.
- Enable passwordless file transfer using SSH keys.
- Avoid using sudo inside the script.
- Allow normal user execution.

---

## 📂 Script Location
/scripts/ecommerce_backup.sh

---

## 📝 Script Content
```bash
#!/bin/bash

BACKUP_FILE="/backup/xfusioncorp_ecommerce.zip"
SOURCE_DIR="/var/www/html/ecommerce"
REMOTE_USER="clint"
REMOTE_HOST="172.16.238.16"
REMOTE_PATH="/backup/"

# Create zip archive
zip -r $BACKUP_FILE $SOURCE_DIR

# Copy archive to backup server
scp $BACKUP_FILE ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_PATH}

echo "Backup completed successfully."
```
🛠️ Setup Steps
1️⃣ Install zip package (manual)
sudo dnf install zip unzip

2️⃣ Generate SSH Key
ssh-keygen

3️⃣ Copy Public Key to Backup Server
ssh-copy-id clint@172.16.238.16

4️⃣ Make Script Executable
chmod +x /scripts/ecommerce_backup.sh

▶️ Execution
/scripts/ecommerce_backup.sh

✅ Verification
Local Verification
ls /backup/


Confirmed zip file exists locally.

Remote Verification
ssh clint@172.16.238.16
ls /backup/


Confirmed zip file exists on Nautilus Backup Server.

🧠 Key Learnings

Bash scripting enables repeatable automation.

SSH key authentication allows passwordless execution.

Variables improve script maintainability and readability.

Avoid using sudo inside automation scripts.

Always verify backups locally and remotely.

🎤 Interview Questions
Q1. Why automate backups instead of manual?

Automation improves reliability, consistency, and reduces human errors.

Q2. Why is passwordless SSH important for automation?

Automation cannot depend on manual input.

Q3. What is the purpose of a shebang (#!/bin/bash)?

It tells the system which interpreter should execute the script.

Q4. Difference between zip and tar?

zip → compression + archive

tar → archive (compression optional)
