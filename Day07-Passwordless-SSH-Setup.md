# 🔐 Day 07 – Passwordless SSH Setup from Jump Host

## 🎯 Objective
- Configure password-less SSH access from jump host user `thor`.
- Enable access to all app servers using their respective sudo users.
- Verify SSH login without password prompt.

---

## 🛠️ Commands Used
```bash
# Switch to thor user on jump host
su - thor

# Generate SSH key pair (if not already present)
ssh-keygen

# Copy public key to app server sudo user
ssh-copy-id user@app-server

# Test passwordless SSH login
ssh user@app-server

# Verify .ssh permissions if required
ls -ld ~/.ssh
ls -l ~/.ssh/authorized_keys
```
🧠 Key Learnings

- SSH key authentication allows secure passwordless login.
- Private key stays on source machine, public key goes to remote server.
- Public key must exist in ~/.ssh/authorized_keys.
- Proper permissions are required for SSH to work correctly.
- Passwordless SSH is essential for automation and CI/CD pipelines.

⚠️ Mistakes / Fixes

- Did not know how to copy public key initially → Learned to use key-copy command.
- Verified permissions when authentication failed.

✅ Verification

- SSH login from jump host to app servers works without password prompt.
- Successful access using sudo users on each server.
