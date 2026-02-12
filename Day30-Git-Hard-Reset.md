# 🔄 Day 30 – Git Hard Reset (Cleaning Commit History)

## 📌 Scenario
The Nautilus development team was working on a test repository located at:

/usr/src/kodekloudrepos/cluster


Some unnecessary commits were pushed during testing.  
Now the team wants to **clean the repository history** and reset `HEAD` so that only two commits remain:

- `initial commit`
- `add data.txt file`

After cleanup, changes must be pushed back to origin.

---

## 🎯 Objectives
- Navigate to cluster repository
- Identify commit history
- Reset branch to required commit
- Ensure only two commits exist
- Push cleaned history to remote

---

## 🛠️ Tasks Performed

### ✅ 1. Move into Repository

```bash
cd /usr/src/kodekloudrepos/cluster
```
✅ 2. Check Commit History
git log --oneline
Located commit:

add data.txt file
✅ 3. Hard Reset to Required Commit
git reset --hard <commit-hash>
(This commit corresponds to add data.txt file)

✅ 4. Verify History
git log --oneline
✔️ Only visible commits:

initial commit

add data.txt file

✅ 5. Push Changes to Remote
git push origin master --force
(Force push required after hard reset)

✅ Verification
git log --oneline
Confirmed:

Repository contains only required commits

HEAD correctly points to add data.txt file

🧠 Key Learnings
git reset --hard rewrites commit history

Force push is required after history changes

Hard reset permanently removes commits

Always confirm commit hash before resetting

Use carefully in production repositories

🎤 Interview Questions
Q1. What does git reset --hard do?
Moves HEAD and deletes working tree + staging changes.

Q2. Why is --force needed while pushing?
Because history was rewritten locally.

Q3. Difference between soft, mixed, hard reset?
Soft → keeps changes staged

Mixed → keeps changes unstaged

Hard → deletes everything

Q4. When should hard reset be avoided?
On shared branches unless absolutely required.

✅ Task Completed Successfully
