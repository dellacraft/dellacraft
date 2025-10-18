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

💡 Tips
Host can be any name — it’s like a nickname for that connection.
You can have multiple entries, one per identity.
File permissions matter:
