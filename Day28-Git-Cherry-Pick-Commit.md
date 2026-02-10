# 🍒 Day 28 – Git Cherry-Pick Specific Commit

## 📌 Scenario
The Nautilus development team was working on the repository:

`/usr/src/kodekloudrepos/games`

Two branches existed:
- `master`
- `feature`

A developer was still working on the `feature` branch but requested that **one specific commit** (`Update info.txt`) be merged into `master` without merging the entire branch.

The DevOps team was asked to perform this operation safely and push the changes.

---

## 🎯 Objectives
- Identify the required commit from `feature`
- Apply only that commit to `master`
- Avoid merging unfinished work
- Push final changes to origin

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Repository
```bash
cd /usr/src/kodekloudrepos/games
```
✅ 2. Fetch Latest Branches
```
git fetch
```
✅ 3. View Feature Branch Commits
```
git log feature --oneline
```
Located commit with message:

Update info.txt
✅ 4. Switch to Master Branch
git checkout master
✅ 5. Cherry-Pick Required Commit
git cherry-pick <commit-hash>
(Used the hash of “Update info.txt” commit)

✅ 6. Push Changes
git push origin master
✅ Verification
git log --oneline
✔️ Confirmed:

Commit successfully added to master

No extra commits merged

Feature branch remains untouched

🧠 Key Learnings
git cherry-pick allows selective commit merging

Useful when feature branch is incomplete

Avoids merging unwanted changes

Always review commits before cherry-picking

Push only after verification

🎤 Interview Questions
Q1. What is git cherry-pick?
It applies a specific commit from one branch onto another.

Q2. When should cherry-pick be used?
When only one or few commits are required instead of full branch merge.

Q3. Difference between merge and cherry-pick?
Merge:

Combines full branch history

Cherry-pick:

Copies individual commits

Q4. Does cherry-pick preserve original commit hash?
No — it creates a new commit with a new hash.

✅ Task Completed Successfully
