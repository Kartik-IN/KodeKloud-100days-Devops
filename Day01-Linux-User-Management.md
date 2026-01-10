# 🚀 Day 01 – Linux User Management (Non-Interactive User)

> **Goal:** Securely create a service user with a non-interactive shell on a Linux server — just like real production systems handle backup agents, monitoring tools, and automation users.

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
- [x] Document mistakes and learnings  

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
```

---

## 🧠 What I Learned

### 🔒 Non-Interactive Shells

A non-interactive shell prevents users from logging into the system.

**Used for:**
- Backup agents  
- Monitoring services  
- Automation bots  
- System daemons  

**Common shells:**
```
/sbin/nologin
/bin/false
```

---

### 📁 Linux User Storage

User details are stored in:

```
/etc/passwd
```

**Format:**
```
username : password : UID : GID : comment : home : shell
```

The last field defines the login shell.

---

### 🛡️ Privilege Control

Only administrative users can modify:

```
/etc/passwd
/etc/shadow
/etc/group
```

Requires elevated access:

```bash
sudo
```

---

### 🌐 Server Awareness

In multi-server environments, each server maintains its own users and configuration.

Always verify the connected server:

```bash
hostname
```

---

## ❌ Mistakes I Made

| Mistake | Lesson |
|----------|----------|
| Created user on wrong server | Always verify hostname |
| Permission denied error | Forgot to use sudo |
| Tried logging into non-interactive user | Expected behavior |
| Confusion about home directory access | Service users don't need shells |

---

## ✅ How I Fixed It

✔ Verified correct server  
✔ Used sudo properly  
✔ Recreated user correctly  
✔ Verified shell configuration  
✔ Tested login restriction  

---

## 🔍 Validation Proof

```bash
getent passwd backupuser
```

**Expected Output:**
```
backupuser:x:1002:1002::/home/backupuser:/sbin/nologin
```

```bash
su - backupuser
```

**Expected Result:**
```
This account is currently not available.
```

---

## 🧪 Security Insight

> Service accounts should NEVER allow interactive login.  
> This reduces attack surface and prevents misuse.

---

## 🏁 Key Takeaways

✅ Always validate your environment  
✅ Permission errors guide debugging  
✅ Security-first user design  
✅ Verification > Assumptions  
✅ Learn from mistakes  

---

