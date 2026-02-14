# 🔄 Day 32 – Git Rebase Feature Branch with Master

## 📌 Scenario

The Nautilus development team was working on a repository:

/usr/src/kodekloudrepos/media


The repository already had two branches:

- master
- feature

Some new commits were pushed to **master**, while development was still ongoing on **feature**.

The requirement:

- Rebase `feature` branch with `master`
- Do NOT create a merge commit
- Preserve feature branch work
- Push updated feature branch to origin

---

## 🎯 Objectives

- Switch to feature branch
- Rebase feature on top of master
- Resolve conflicts if any
- Push rebased branch

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/media
✅ 2. Checkout Feature Branch
git checkout feature
✅ 3. Pull Latest Master
git fetch origin
✅ 4. Rebase Feature with Master
git rebase origin/master
✅ 5. Resolve Conflicts (if any)
git status
# fix files manually
git add .
git rebase --continue
✅ 6. Push Rebased Feature Branch
Since history changed:

git push origin feature --force
✅ Verification
git log --oneline --graph
```
✔️ Feature commits now sit on top of master
✔️ No merge commit created
✔️ Changes pushed successfully

🧠 Key Learnings
git rebase keeps history linear

Rebasing avoids unnecessary merge commits

Always fetch latest master before rebasing

After rebase, force push is required

Rebase rewrites commit history

🎤 Interview Questions
Q1. Difference between merge and rebase?
Merge creates a merge commit

Rebase rewrites history and keeps it linear

Q2. When should you avoid rebase?
On shared/public branches used by multiple developers.

Q3. Why is --force needed after rebase?
Because commit hashes change.

Q4. Advantage of rebase?
Cleaner commit history.

✅ Task Completed Successfully
