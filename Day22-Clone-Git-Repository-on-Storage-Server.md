# 📦 Day 22 – Git Repository Cloning on Storage Server

## 📌 Scenario
The DevOps team at **xFusionCorp Industries** had previously created a Git repository that was unused.  
Now, the **Nautilus application development team** required a copy of this repository on the **Storage Server** in **Stratos Datacenter**.

The task was to clone the repository **safely and correctly**, following strict operational rules.

---

## 🎯 Objectives
- Clone an existing Git repository from a local source
- Use the correct system user for the task
- Avoid modifying permissions or existing directories
- Maintain production-grade discipline

---

## 🛠️ Task Details
- **Source Repository:** `/opt/official.git`
- **Destination Directory:** `/usr/src/kodekloudrepos`
- **User to perform task:** `natasha`
- ❌ Do NOT modify permissions
- ❌ Do NOT use sudo
- ❌ Do NOT alter existing directories

---

## 🧩 Solution Approach

### ✅ 1. Switch to Correct User
```bash
su - natasha

✅ 2. Navigate to Target Directory
cd /usr/src/kodekloudrepos

✅ 3. Clone the Repository
git clone /opt/official.git


Repository cloned without altering permissions or directory structure.

✅ 4. Verify Repository
ls -l


✔️ Repository files present
✔️ Ownership correct
✔️ No permission changes made

⚠️ Common Mistakes to Avoid

Using sudo git clone

Cloning as root

Changing directory permissions unnecessarily

Deleting existing directories before cloning

These actions would cause task failure in real production environments.

🧠 Key Learnings

Git operations are part of infrastructure management

User context is critical in production systems

Minimal change is a core DevOps principle

Correct execution matters more than just “getting it to work”

🎤 Interview Questions
Q1. Why is cloning as the correct user important?

It ensures proper ownership and prevents permission-related issues in production systems.

Q2. Why should permissions not be changed unnecessarily?

Unplanned permission changes can introduce security risks and break dependent services.

Q3. What does this task simulate in real-world DevOps?

Safe repository deployment with zero configuration drift.

✅ Task Completed Successfully 🎉
