# 🔀 Day 29 – Git Pull Request Workflow (Protecting Master Branch)

## 📌 Scenario
The Nautilus DevOps team wanted to prevent developers from pushing code directly to the `master` branch, since it represents the final reviewed version.

A developer named **Max** pushed his changes to a feature branch (`story/fox-and-grapes`) on the Gitea server.  
The task was to raise a **Pull Request**, review it, and merge it safely into `master`.

---

## 🎯 Objectives
- Access Gitea using Max credentials
- Verify feature branch (`story/fox-and-grapes`)
- Create Pull Request to `master`
- Merge approved changes
- Ensure master branch contains final content

---

## 🛠️ Tasks Performed

### ✅ 1. SSH into Storage Server
```bash
ssh max@storage-server
```
✅ 2. Verify Repository
cd ~/the-fox-and-grapes
git branch
Confirmed branch:

story/fox-and-grapes
✅ 3. Open Gitea UI
Click Gitea UI from top bar

Login using:

Username: max

Password: Max_pass123

✅ 4. Create Pull Request
Steps in Gitea:

Open repository

Select Pull Requests

Click New Pull Request

Source: story/fox-and-grapes

Target: master

Create PR

✅ 5. Merge Pull Request
After review:

Click Merge Pull Request

Confirm merge

✅ Verification
git checkout master
git pull
✔️ Confirmed:

Story successfully merged into master

Direct pushes to master avoided

Feature branch preserved

🧠 Key Learnings
Pull Requests enforce code review before merging

Master branch should always stay protected

Feature branches allow safe development

PR workflow prevents accidental production issues

Gitea provides clean Git collaboration process

🎤 Interview Questions
Q1. Why block direct pushes to master?
To prevent unreviewed code from reaching production.

Q2. What is a Pull Request?
A request to merge changes from one branch into another after review.

Q3. Benefits of PR workflow?
Code review

Team collaboration

Safer deployments

Clear change history

Q4. Difference between merge vs pull request?
Merge:

Local Git operation

Pull Request:

Review-based merge via Git platform

✅ Task Completed Successfully

