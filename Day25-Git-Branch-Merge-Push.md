# 🔀 Day 25 – Git Branch Creation, Merge & Push Workflow

## 📌 Scenario

The Nautilus development team is working on a project repository located at:

/usr/src/kodekloudrepos/official


The original bare repository exists at:

/opt/official.git


DevOps was asked to:

- Create a new branch
- Copy a file into the repo
- Commit changes
- Merge back to master
- Push both branches to origin

---

## 🎯 Objectives

- Create a new branch `xfusion`
- Copy `/tmp/index.html` into repository
- Commit changes in new branch
- Merge branch into `master`
- Push both branches to origin

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/official
```
✅ 2. Verify Current Branch
git branch
Confirmed:

master
✅ 3. Create New Branch
git checkout -b xfusion
✅ 4. Copy File into Repository
cp /tmp/index.html .
✅ 5. Stage & Commit Changes
git add index.html
git commit -m "Added index.html file"
✅ 6. Merge Branch into Master
Switch back to master:

git checkout master
Merge:

git merge xfusion
✅ 7. Push Both Branches to Origin
git push origin master
git push origin xfusion
✅ Verification
git branch
Confirmed both branches exist.

git log --oneline
Verified commit applied.

Repository successfully synced with origin.

🧠 Key Learnings
Feature branches help isolate changes

Always commit before merging

Merge integrates feature work into main branch

Both branches must be pushed explicitly

DevOps workflows often include Git operations without touching application logic

🎤 Interview Questions
Q1. Why create a feature branch?
To isolate changes before merging into production.

Q2. Difference between git merge and git push?
Merge combines branches locally

Push sends changes to remote repository

Q3. Why push both branches?
To ensure origin reflects complete branch structure.

Q4. What does git checkout -b do?
Creates and switches to a new branch.

Q5. Why verify with git log?
To confirm commits were applied correctly.

✅ Day 25 Completed Successfully
