# 🍺 Homebrew Setup

Homebrew is the **package manager for macOS**, used to install both CLI tools and GUI applications consistently.

---

## 🧭 Overview

* Manage developer tools and system utilities under macOS.
* Keep CLI and GUI apps version-controlled via a `Brewfile`.
* Simplify environment replication on new machines.

---

## ⚙️ Common Commands

```bash
brew list --versions    # List installed packages with versions
brew list --cask        # List installed GUI (cask) apps
brew info <name>        # Show details: version, dependencies, install path
brew cleanup -n         # Preview what can be cleaned up
brew upgrade awscli     # Upgrade a specific package
```

---

## 📦 Exporting & Restoring Environment

```bash
# Export current environment to Brewfile
brew bundle dump --file=./Brewfile --force

# Restore environment from Brewfile
brew bundle --file=./Brewfile
```

* The `Brewfile` acts like a lockfile for Homebrew packages.
* Recommended to commit it into your repository for reproducibility.

---

## 🧱 Recommended Policy

| Category  | Example                           | Notes                                    |
| --------- | --------------------------------- | ---------------------------------------- |
| CLI tools | `awscli`, `git`, `asdf`, `direnv` | Keep them versioned and managed via Brew |
| GUI apps  | `visual-studio-code`, `aws-vault` | Installed as casks                       |

---

## 📄 Example `Brewfile`

```rb
# CLI Tools
brew "asdf"
brew "awscli"
brew "git"

# Optional
brew "direnv"

# GUI Apps (Casks)
cask "visual-studio-code"
# cask "aws-vault"
```

---

## 💡 Tips

* Prefer installing **AWS CLI v2** via Homebrew to avoid pip conflicts.
* Use `brew upgrade` regularly to keep tools up to date.
* On Apple Silicon Macs, Homebrew defaults to `/opt/homebrew`. Run `brew --prefix` to confirm the path.

---

## 🔗 Related Sections

* [asdf — Runtime version management](../asdf/README.md)
* [pnpm — Node package management](../pnpm/README.md)

