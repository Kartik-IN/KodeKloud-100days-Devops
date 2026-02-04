# 🌿 Day 24 – Create Git Branch on Storage Server

## 📌 Scenario

Nautilus developers are actively working on a project repository located at:

/usr/src/kodekloudrepos/games


They decided to implement new features and wanted these changes maintained in a **separate Git branch**.  
The DevOps team was asked to create a new branch on the **Storage Server** without modifying any code.

---

## 🎯 Objectives

- Access the existing Git repository on Storage Server
- Create a new branch from the `master` branch
- Ensure no code changes are made
- Verify branch creation

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/games
```
✅ 2. Verify Current Branch
git branch
Confirmed existing branch:

master
✅ 3. Create New Branch
Created a new branch named:

xfusioncorp_games
git checkout -b xfusioncorp_games
✅ 4. Verify Branch Creation
git branch
Output confirmed:

* xfusioncorp_games
  master
✅ Verification
New branch successfully created

No source code modified

Repository remains intact

🧠 Key Learnings
Git branching allows feature isolation without impacting production code

git checkout -b creates and switches branches in one step

Always verify branches after creation

DevOps workflows often require repository operations without touching application code

Proper branching improves collaboration between developers and operations

🎤 Interview Questions
Q1. Why do we create separate branches?
To isolate development changes and avoid impacting the main production code.

Q2. What does git checkout -b do?
Creates a new branch and switches to it immediately.

Q3. How do you list all branches?
git branch
Q4. Why should DevOps avoid modifying application code?
DevOps focuses on infrastructure and automation while developers handle application logic.

Q5. What is the purpose of the master branch?
It represents the stable production-ready codebase.

✅ Day 24 Completed Successfully

