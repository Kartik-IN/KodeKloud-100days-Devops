# ⚔️ Day 33 – Resolve Git Merge Conflicts & Fix Push Issues

## 📌 Scenario

Sarah and Max were working on a Git repository:

/home/max/story-blog


Max attempted to push new changes but encountered issues.

Requirements:

- Fix push errors
- Ensure `story-index.txt` contains titles for all 4 stories
- Correct typo:  
  "The Lion and the Moose" → should be "The Lion and the Mouse"
- Push changes successfully to origin

---

## 🎯 Objectives

- Identify why push failed
- Resolve merge conflicts (if any)
- Fix file content issues
- Commit and push clean changes

---

## 🛠️ Tasks Performed

### ✅ 1. SSH into Storage Server

```bash
ssh max@storage-server
✅ 2. Navigate to Repository
cd /home/max/story-blog
✅ 3. Check Git Status
git status
Observed:

Push rejected (remote ahead)

Merge conflict present

✅ 4. Pull Latest Changes
git pull origin master
Conflict markers appeared:

<<<<<<< HEAD
=======
>>>>>>> branch-name
✅ 5. Resolve Conflict Manually
Edited story-index.txt:

Added titles for all 4 stories

Fixed typo:

The Lion and the Mouse
Removed conflict markers.

✅ 6. Add & Commit Changes
git add story-index.txt
git commit -m "fix: resolve merge conflict and correct story title"
✅ 7. Push to Remote
git push origin master
✔️ Push successful

✅ Verification
git log --oneline
```
✔️ Clean commit history
✔️ No conflict markers
✔️ Correct file content
✔️ Remote updated successfully

🧠 Key Learnings
Push failures usually mean remote branch is ahead

Always pull before pushing

Conflict markers must be removed manually

Carefully review file content during conflict resolution

Git workflow discipline prevents production issues

🎤 Interview Questions
Q1. Why does git push get rejected?
Because remote branch has new commits that local branch doesn't.

Q2. How do you resolve merge conflicts?
Pull changes

Edit conflicting files

Remove conflict markers

Add & commit

Push again

Q3. What do conflict markers look like?
<<<<<<< HEAD
=======
>>>>>>> branch-name
Q4. Best practice to avoid conflicts?
Pull frequently

Work on feature branches

Keep commits small

✅ Day 33 Completed Successfully
