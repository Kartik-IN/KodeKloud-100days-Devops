# 🔐 Day 05 – Install and Permanently Disable SELinux

## 📌 Challenge Description

As part of a security audit, the infrastructure team enabled SELinux testing on App Server 3.  
For controlled configuration changes, SELinux needed to be installed and permanently disabled temporarily until proper policies are configured.

---

## 🎯 Objective

- Install required SELinux packages.
- Permanently disable SELinux using configuration.
- Avoid immediate reboot as maintenance is scheduled.
- Ensure final SELinux status after reboot will be disabled.

---

## 🧠 Key Concepts Learned

### ✅ What is SELinux?

SELinux (Security-Enhanced Linux) provides Mandatory Access Control (MAC) to restrict processes and improve system security.

---

### ✅ SELinux Modes

| Mode | Description |
|------|-------------|
| Enforcing | Policies are actively enforced |
| Permissive | Violations are logged only |
| Disabled | SELinux is fully disabled |

---

### ✅ Temporary vs Permanent Configuration

Temporary changes affect only the current runtime session.  
Permanent changes require modifying the SELinux configuration file.

---

### ✅ SELinux Configuration File

SELinux configuration is managed in:
/etc/selinux/config


The `SELINUX` parameter controls the operating mode.

---

### ✅ Package Management

SELinux packages were installed using the system package manager to ensure required components are available.

---

## ❌ Mistakes and Learning

- Initially confused between runtime and persistent configuration.
- Reinforced importance of editing configuration files for permanent changes.

---

## ✅ How the Issue Was Solved

- Connected to App Server 3.
- Installed SELinux related packages.
- Opened SELinux configuration file using admin privileges.
- Updated SELINUX value to disabled.
- Saved configuration without reboot.
- Verified configuration file settings.

---

## 🔍 Verification Summary

Verification confirmed:

- SELinux packages are installed.
- Configuration file reflects disabled mode.
- No reboot required immediately.

---

## 💡 Key Takeaways

- Always use configuration files for permanent system changes.
- Understand security tradeoffs when disabling protections.
- Plan maintenance windows for reboots.
- Validate system configuration before production changes.

---

## 🎤 Interview Preparation Notes

### Q1: What is SELinux?
A Linux security module enforcing mandatory access control.

---

### Q2: Difference between enforcing and permissive?
Enforcing blocks violations, permissive only logs.

---

### Q3: How do you permanently disable SELinux?
By modifying SELinux configuration file.

---

### Q4: Why avoid immediate reboot during changes?
To avoid service disruption during peak hours.

---

---

## 📅 Progress Log

Day 05 : SELinux Installation and Permanent Disable  ✅ Completed

---

