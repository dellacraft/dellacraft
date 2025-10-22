# 🔐 SSH Config Tips for macOS

A lightweight place to keep quick notes and tips I often forget.
This one’s about managing multiple SSH keys and GitHub accounts efficiently on macOS using the system Keychain.

---

## 🧭 Overview

When you have multiple GitHub accounts or SSH keys,
you can tell SSH which key to use for each host by editing ~/.ssh/config.
macOS automatically manages your SSH keys through Keychain,
so you don’t have to re-enter your passphrase after every reboot.

---

## ⚙️ Example Configuration

```sshconfig
# ~/.ssh/config

# Use the macOS keychain
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa

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

### 💡 Tips  
- Host * applies to all SSH connections. AddKeysToAgent yes and UseKeychain yes are essential for macOS Keychain integration.
- Host is just a nickname — you can name it anything like github-work or github-personal.
- File permissions matter:

```bash
chmod 600 ~/.ssh/id_rsa_*
chmod 644 ~/.ssh/*.pub
```

---

## 🍎 Add Keys to macOS Keychain

Run the following once to permanently store your passphrase in the Keychain:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_rsa_personal
ssh-add --apple-use-keychain ~/.ssh/id_rsa_work
```

> 💬 On macOS Ventura and later, -K is deprecated.
> Use --apple-use-keychain instead.

Check which keys are currently loaded:

```bash
ssh-add -l
```

---

## 🧩 How to Use a Custom Host in Git

After adding the custom host (e.g., github-work),
update your repository’s remote URL:

```bash
git remote set-url origin git@github-work:yourname/repo.git
```

Then test your connection:

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

---

## 🪄 Troubleshooting

| Symptom                              | Possible Fix                                                            |
| ------------------------------------ | ----------------------------------------------------------------------- |
| `Permission denied (publickey)`      | Check file permissions (`chmod 600`), or ensure the right key is in use |
| GitHub connects to the wrong account | Verify `Host` name and remote URL (`git remote -v`)                     |
| SSH config ignored                   | Ensure file is named exactly `config` (no extension)                    |
| Keychain not used                    | Add UseKeychain yes under Host * section                                |
| `ssh -T git@github-work` fails       | Try `ssh -vT git@github-work` for verbose output                        |

---

## ✅ Quick Recap

- Define multiple keys in ~/.ssh/config
- Enable macOS Keychain support (UseKeychain yes)
- Add keys with ssh-add --apple-use-keychain
- Use custom Host aliases per GitHub account

> 💬 This note is meant for quick recall —  
> no overthinking, just enough to fix the “Wait, how did I do that again?” moments.

