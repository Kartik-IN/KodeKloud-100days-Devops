# ⚙️ Day 04 – Grant Execute Permission to a Script

## 📌 Challenge Description

A new automation script named `xfusioncorp.sh` was distributed to the servers for backup automation.  
However, the script did not have executable permissions on **App Server 1**.

The task was to grant executable permissions so that **all users** can execute the script.

---

## 🎯 Objective

- Locate the script in the `/tmp` directory.
- Grant execute permission to the script.
- Ensure all users (owner, group, others) can run it.
- Verify the permission change.

---

## 🧠 Key Concepts Learned

### ✅ Linux File Permissions

Linux permissions are divided into three types:

- **Read (r)** – View file contents  
- **Write (w)** – Modify the file  
- **Execute (x)** – Run the file as a program  

A script must have execute permission to run.

---

### ✅ Permission Categories

Every file has permissions for:

- **Owner**
- **Group**
- **Others**

To allow everyone to execute the script, execute permission must be enabled for all three categories.

---

### ✅ Permission Modification

Linux provides a command to modify file permissions.

Permissions can be updated using:
- Symbolic mode (adding or removing permissions)
- Numeric mode (setting permission values)

---

### ✅ Privilege Requirement

If the file is owned by another user or protected, administrative privileges are required to change permissions safely.

---

## ❌ Mistakes and Learning

- Initially forgot that permission changes may require elevated privileges.
- Reinforced the importance of verifying permissions after modification.

---

## ✅ How the Issue Was Solved

- Navigated to the `/tmp` directory on App Server 1.
- Verified the existing permissions of the script.
- Added execute permission to the script.
- Re-checked permissions to confirm changes.
- Successfully executed the script without permission errors.

---

## 🔍 Verification Summary

Verification confirmed:

- Execute permission is enabled.
- All users can run the script.
- No permission errors occur during execution.

---

## 💡 Key Takeaways

- Scripts must have execute permission to run.
- Always verify permissions before and after changes.
- Use minimal permissions required for security.
- Administrative access may be needed for system files.

---

## 🎤 Interview Preparation Notes

### Q1: What happens if a script does not have execute permission?
The script cannot be run and will return a permission denied error.

---

### Q2: What is the difference between read and execute permission?
Read allows viewing the file content, while execute allows running the file.

---

### Q3: Why should we avoid giving write permission to everyone?
It can cause accidental or malicious modification of files.

---

### Q4: What does execute permission mean for directories?
It allows entering and accessing the directory.

---

## 📅 Progress Log

Day 04 : Script Execution Permissions  ✅ Completed

---

