# Git Hook Setup for Nautilus Application Repository

## Repository Details
- **Main repository path:** `/opt/ecommerce.git`
- **Cloned repository path:** `/usr/src/kodekloudrepos`
- **Server:** Storage server in Stratos DC
- **User:** `natasha`

---

## Task Summary
The Nautilus application development team required a Git hook to automate release tagging whenever changes are pushed to the `master` branch.

### Steps Completed
1. **Merged feature branch into master branch.**
2. **Created a `post-update` hook** in `/opt/ecommerce.git/hooks/`:
   - Hook automatically generates a release tag with the format:
     ```
     release-YYYY-MM-DD
     ```
     where `YYYY-MM-DD` is the current date.
   - Example: On 20th June 2023, the tag created is:
     ```
     release-2023-06-20
     ```
3. **Tested the hook**:
   - Verified that pushing changes to `master` triggers the hook.
   - Confirmed that a release tag for today’s date was successfully created.
4. **Pushed changes** to the repository.

---

## Verification
- After pushing to `master`, the following command shows the new release tag:
  ```bash
  git tag --list
- Expected output includes:
release-2026-02-16


- (example for today’s date)
Notes
- Repository and directory permissions were not altered.
- All tasks were performed using the natasha user.
- This setup ensures automated release tagging for every push to master.


