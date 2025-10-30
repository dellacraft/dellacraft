# ⚙️ asdf Setup (v0.18+)

asdf is a **version manager** for multiple runtime environments such as Node.js, Python, Go, AWS CLI, and more.  
It ensures consistent development environments across machines and projects.

---

## 🧭 Overview

* Manages runtime versions per **user** (`~/.tool-versions`) or **project** (`.tool-versions`).
* Prevents version drift between developers or CI environments.
* Integrates easily with tools like **direnv** for auto-switching.

---

## 🚀 Installation & Basic Usage

```bash
# Install asdf via Homebrew
brew install asdf

# Load asdf in your shell (~/.zshrc)
. "$(brew --prefix asdf)/libexec/asdf.sh"

# Add plugins (first time only)
asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git
asdf plugin add python https://github.com/danhper/asdf-python.git
asdf plugin add awscli https://github.com/MetricMike/asdf-awscli.git
```
---

## 🐍 Python / 🪣 AWS CLI / 🟢 Node.js Setup

```bash
# Check available versions
asdf list all python | tail -5
asdf list all nodejs | tail -5
asdf list all awscli | tail -5

# Install desired versions
asdf install python 3.13.0
asdf install nodejs 22.8.0
asdf install awscli 2.17.34

# Set global (user-wide) defaults
asdf set -u python 3.13.0
asdf set -u nodejs 22.8.0
asdf set -u awscli 2.17.34

# Or, for a specific project
asdf set python 3.13.0
asdf set nodejs 22.8.0
asdf set awscli 2.17.34
```

✅ -u = user (global) ／ without -u = local (project)

---

## 📄 Example .tool-versions

```text
python  3.13.0
nodejs  22.8.0
awscli  2.17.34
```

> Commit this file to version control to guarantee reproducible environments.

---

## ⚙️ direnv Integration (optional)

```bash
brew install direnv
# In your shell config
eval "$(direnv hook zsh)"
```

Then in your project:

```bash
echo 'use asdf' > .envrc
direnv allow
```

Now asdf automatically activates the correct versions when entering the directory.

---

## 🔄 Updating Versions

```bash
# Find latest version
asdf latest python
# Install & set it
asdf install python 3.14.0
asdf set -u python 3.14.0
asdf reshim python

# Remove old version if desired
asdf uninstall python 3.13.0
```

> 🧩 reshim regenerates shims (the lightweight wrappers under ~/.asdf/shims/)
> after installing or removing tools so your PATH points to the right executables.

---

## 🧱 Version Management Reference

| Command                           | Description                               |
| --------------------------------- | ----------------------------------------- |
| `asdf list <tool>`                | Show installed versions                   |
| `asdf list all <tool>`            | Show all available versions               |
| `asdf current`                    | Show active versions and their source     |
| `asdf where <tool>`               | Show install path for a version           |
| `asdf uninstall <tool> <version>` | Remove an installed version               |
| `asdf plugin update --all`        | Update all plugin definitions             |
| `asdf reshim [tool]`              | Rebuild shims after installing / removing |

---

## 🪞 How Shims Work

```bash
~/.asdf/
├── installs/
│   └── python/3.13.0/bin/python3   # actual binary
└── shims/
    ├── python
    ├── aws
    └── node
```

When you type aws or python, the shim:
Reads .tool-versions (local → global fallback).
Activates the proper version.
Executes the binary under ~/.asdf/installs/....
If a command isn’t found, run:

```bash
asdf reshim
```

and confirm:

```bash
which aws
# => ~/.asdf/shims/aws
```

---

## 🧩 Best Practices

- Include .tool-versions in every repo.
- Use asdf set -u for global defaults, asdf set for project-specific ones.
- Run asdf plugin update --all regularly.
- After pip install or adding new executables, run asdf reshim.
- Keep ~/.asdf/shims in your PATH.

---

## 🔗 Related Sections

* [brew — CLI tool management](../brew/README.md)
* [pnpm — Node package management](../pnpm/README.md)
