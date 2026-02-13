# 📦 Day 31 – Git Stash Restore & Push Changes

## 📌 Scenario
The Nautilus development team was working on a repository located at:

/usr/src/kodekloudrepos/media


One of the developers had stashed some in-progress changes earlier.  
Now the team wants to:

- Restore stash entry `stash@{1}`
- Commit the restored changes
- Push them back to origin

---

## 🎯 Objectives

- Navigate to media repository
- List available stashes
- Apply specific stash (`stash@{1}`)
- Commit restored changes
- Push updates to remote

---

## 🛠️ Tasks Performed

### ✅ 1. Move to Repository

```bash
cd /usr/src/kodekloudrepos/media
✅ 2. List Stashes
git stash list
Confirmed stash exists:

stash@{1}
✅ 3. Apply Required Stash
git stash apply stash@{1}
(Restores files without deleting stash)

✅ 4. Verify Restored Files
git status
✅ 5. Stage Changes
git add .
✅ 6. Commit Changes
git commit -m "restore stashed changes"
✅ 7. Push to Origin
git push origin master
✅ Verification
git status
```
✔️ Working tree clean
✔️ Changes successfully pushed

🧠 Key Learnings
git stash temporarily stores uncommitted work

git stash list shows all saved stashes

git stash apply restores changes without deleting stash

git stash pop restores + removes stash

Always check git status before committing

🎤 Interview Questions
Q1. Difference between stash apply and stash pop?
apply → restores stash but keeps it

pop → restores and deletes stash

Q2. Why use git stash?
To temporarily save unfinished work without committing.

Q3. How do you restore a specific stash?
git stash apply stash@{n}
Q4. Can stash contain untracked files?
Yes, using:

git stash -u
✅ Task Completed Successfully
