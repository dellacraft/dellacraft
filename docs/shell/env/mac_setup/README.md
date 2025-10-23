# 🐚 macOS Environment Setup

> Directory: `shell/env/mac_setup/`

This section documents a **reproducible macOS development setup** focused on Homebrew, asdf, and pnpm — ideal for Node.js, TypeScript, and AWS CDK projects.

---

## 🎯 Goal

* Create a **consistent, reproducible** setup for macOS development.
* Target environment: **Node.js + TypeScript + AWS CDK**.
* Manage both CLI and GUI tools through Homebrew.
* Keep configurations portable across multiple machines or team members.

---

## 📁 Structure

```
shell/env/mac_setup/
├── README.md                 # Overview (this file)
├── brew/                     # CLI & GUI package management
│   ├── README.md
│   └── Brewfile.sample
├── asdf/                     # Runtime version management
│   ├── README.md
│   └── .tool-versions.sample
├── pnpm/                     # Node package management (Corepack-based)
│   ├── README.md
│   └── package.json.sample
└── scripts/                  # Setup automation scripts
    ├── dump-brew.sh
    └── setup-node.sh
```

---

## 🚀 Quick Start

```bash
# 1. Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. Restore CLI tools from Brewfile
cd brew
brew bundle --file=./Brewfile.sample

# 3. Set up asdf + Node.js
asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git
asdf install nodejs 22.8.0
asdf global nodejs 22.8.0

# 4. Enable Corepack & fix pnpm version
corepack enable
corepack use pnpm@9.12.0
```

---

## 🧱 Philosophy

| Layer       | Tool                | Purpose                                         |
| ----------- | ------------------- | ----------------------------------------------- |
| CLI tools   | Homebrew            | Manage utilities like awscli, git, asdf, direnv |
| Runtimes    | asdf                | Version-control Node.js, Python, etc.           |
| JS packages | pnpm (via Corepack) | Faster, reproducible alternative to npm         |

---

## 🧰 Notes

* asdf locks Node versions via `.tool-versions` for reproducibility.
* Corepack pins pnpm version in `packageManager` field of `package.json`.
* `brew bundle dump` exports all installed tools to a Brewfile.
* `scripts/` directory contains automation templates for rebuilding your environment with one command.

---

## 🔗 Related Categories

* [🐚 Shell — bash/zsh, ssh config, shortcuts](../..)
* [☁️ AWS — CDK, Lambda, CloudFormation](../../../aws)

---

Next section → [`brew/README.md`](./brew/README.md): How to manage CLI tools with Homebrew.
