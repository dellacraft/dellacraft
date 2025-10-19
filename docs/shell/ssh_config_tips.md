# 🔐 SSH Config Tips

A lightweight place to keep quick notes and tips I often forget.  
This one’s about managing multiple SSH keys and GitHub accounts efficiently.

---

## 🧭 Overview

When you have more than one GitHub account or deploy key,  
you can tell SSH which key to use for each host by editing `~/.ssh/config`.

This prevents "Permission denied" or "wrong account" errors when pushing or pulling.

---

## ⚙️ Example Configuration

```sshconfig

# ~/.ssh/config

# Default GitHub (personal)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_personal

# Work GitHub (custom alias)
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_work

```

💡 Tips  
- Host can be any name — it’s like a nickname for that connection.
- You can have multiple entries, one per identity.
- File permissions matter:

```bash

chmod 600 ~/.ssh/id_rsa_*
chmod 644 ~/.ssh/*.pub

```

---

## 🧩 How to Use a Custom Host in Git

After adding the custom host (github-work),
update your repository’s remote URL:

```bash

git remote set-url origin git@github-work:yourname/repo.git

```

Then test it:

```bash

ssh -T git@github-work

```

Expected output:

```bash

Hi yourname! You've successfully authenticated, but GitHub does not provide shell access.

```

---

## 🧠 Notes

| What                   | Command / Path               | Description                              |
| ---------------------- | ---------------------------- | ---------------------------------------- |
| SSH config file        | `~/.ssh/config`              | Defines which key is used for which host |
| List active identities | `ssh-add -l`                 | Shows keys loaded into the SSH agent     |
| Add a key to agent     | `ssh-add ~/.ssh/id_rsa_work` | Temporary for this session               |
| Remove all keys        | `ssh-add -D`                 | Clears agent cache                       |
