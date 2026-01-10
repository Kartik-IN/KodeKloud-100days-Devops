# 🚀 Day 01 – Linux User Management (Non-Interactive User)

> **Goal:** Securely create a service user with a non-interactive shell on a Linux server — exactly how real production systems handle backup agents, monitoring tools, and automation users.

---

## 🧩 Problem Statement

A backup agent requires a **service account** that:
- ❌ Must NOT allow interactive login  
- ✅ Must exist only for system operations  
- ✅ Must be created on the correct server node  

This simulates a real-world DevOps security scenario.

---

## 🎯 Objective Checklist

- [x] Create a user account  
- [x] Assign a non-interactive shell  
- [x] Perform task on correct server  
- [x] Validate behavior and permissions  
- [x] Document mistakes + learnings  

---

## 🛠️ Commands Used

```bash
# Check current server
hostname

# Create non-interactive user
sudo useradd -s /sbin/nologin backupuser

# Verify user entry
cat /etc/passwd | grep backupuser

# Try switching user (should fail)
su - backupuser

# Verify shell assignment
getent passwd backupuser
