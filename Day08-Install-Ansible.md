# Day08-Install-Ansible
# 🤖 Ansible Installation on Jump Host (pip3)

## 📌 Task
Install **Ansible version 4.7.0** on the Jump Host using **pip3 only** and ensure that the Ansible binary is available globally for all users.

---

## 🎯 Objective
- Install Ansible using pip3.
- Pin the version to 4.7.0.
- Make sure Ansible is accessible system-wide.
- Verify installation from multiple users.

---

## 🛠️ Commands Used
```bash
# Install Ansible globally using pip3
sudo pip3 install ansible==4.7.0

# Verify Ansible version
ansible --version

# Verify global availability (from another user)
su - banner
ansible --version
```

🧠 Key Learnings

- pip3 can be used to install specific package versions.
- Using sudo installs packages system-wide (global access). 
- Avoid using --user when tools must be available to all users.
- Version pinning ensures consistency across environments.

⚠️ Mistakes / Fixes

- Initially checked user-base installation path (~/.local) which would limit access to one user.
- Corrected by installing Ansible globally using sudo.

✅ Verification

- Ansible --version shows version 4.7.0.
- Ansible command works for other users as well.
