# 📦 pnpm Setup

pnpm is a **fast, disk-efficient alternative to npm** for managing JavaScript and TypeScript project dependencies. Combined with Corepack, it ensures reproducible builds and consistent dependency versions across machines.

---

## 🧭 Overview

* Manages Node.js project dependencies (like npm or yarn).
* Uses a **global content-addressable store** to save disk space.
* Ensures reproducible installs via `pnpm-lock.yaml`.
* Plays well with monorepos and workspaces.

---

## 🚀 Installation & Setup

Enable Corepack (bundled with Node.js ≥16.10):

```bash
corepack enable
corepack use pnpm@9.12.0
```

This will pin the pnpm version in your project’s `packageManager` field automatically.

Verify installation:

```bash
pnpm -v
```

---

## 📄 Example `package.json`

```json
{
  "name": "example-project",
  "private": true,
  "packageManager": "pnpm@9.12.0",
  "scripts": {
    "build": "tsc -p tsconfig.json",
    "deploy": "pnpm cdk deploy"
  },
  "devDependencies": {
    "typescript": "5.6.3",
    "aws-cdk": "2.158.0",
    "aws-cdk-lib": "2.158.0",
    "constructs": "10.3.0"
  }
}
```

---

## ⚙️ Common Commands

| Purpose              | Command               |
| -------------------- | --------------------- |
| Install dependencies | `pnpm install`        |
| Add a new package    | `pnpm add <pkg>`      |
| Remove a package     | `pnpm remove <pkg>`   |
| Run a script         | `pnpm run <script>`   |
| Update dependencies  | `pnpm update`         |
| Execute binaries     | `pnpm exec <command>` |

Example:

```bash
pnpm add aws-cdk-lib constructs
pnpm run build
pnpm exec cdk deploy
```

---

## 🧱 Workspaces (Monorepo Support)

If your repository contains multiple packages, use `pnpm-workspace.yaml` to manage them together.

```yaml
packages:
  - "infra"      # AWS CDK project
  - "packages/*" # Shared libraries
```

Then run commands at the root:

```bash
pnpm install       # Installs all workspace dependencies
pnpm -r run build  # Runs build script across all packages
```

---

## 🧩 Corepack Integration

Corepack ensures the same pnpm version across environments:

```bash
corepack use pnpm@9.12.0
```

This adds the following line to your `package.json` automatically:

```json
"packageManager": "pnpm@9.12.0"
```

Commit this field to version control so all collaborators use the same pnpm release.

---

## ⚡ Advantages over npm

| Feature             | npm                   | pnpm                        |
| ------------------- | --------------------- | --------------------------- |
| Speed               | 🐢 slower             | ⚡ faster (shared store)     |
| Disk usage          | High                  | Very low (deduplicated)     |
| Reproducibility     | Moderate              | Excellent (strict lockfile) |
| Monorepo support    | Limited               | Built-in, first-class       |
| Installation method | Nested `node_modules` | Symlinked, flat layout      |

---

## 🧰 Troubleshooting: `pnpm not found`

If you see `zsh: command not found: pnpm`, it usually means pnpm is not linked to your PATH yet. Try these steps in order:

1️⃣ **Make sure Node.js is active (via asdf)**

```bash
node -v
```

If this fails, install and activate Node:

```bash
asdf install nodejs 22.8.0
asdf local nodejs 22.8.0
```

2️⃣ **Enable Corepack**

```bash
corepack enable
corepack prepare pnpm@9.12.0 --activate
```

3️⃣ **Regenerate asdf shims**

```bash
asdf reshim nodejs
```

4️⃣ **Reload your shell**

```bash
exec $SHELL -l
```

5️⃣ **Check PATH**

```bash
echo $PATH | tr ':' '\n' | grep asdf/shims
```

If missing, add this to your `~/.zshrc`:

```bash
. "$(brew --prefix asdf)/libexec/asdf.sh"
```

6️⃣ **Verify installation**

```bash
which pnpm
pnpm -v
```

It should now point to `~/.asdf/shims/pnpm`.

> 💡 Run `asdf reshim nodejs` anytime you enable Corepack or install new global tools to update shims.

---

## 🔁 Migrating from npm

If your project previously used **npm**, here’s how things map when switching to **pnpm**:

### 1) Local project dependencies

* Remove npm artifacts and reinstall with pnpm:

  ```bash
  rm -rf node_modules package-lock.json
  pnpm install
  ```
* pnpm creates a **symlinked `node_modules`** and uses a shared content-addressable store for faster, leaner installs.
* A `pnpm-lock.yaml` will be generated (commit this instead of `package-lock.json`).

### 2) Global packages

* npm’s global packages are **not reused** by pnpm (they live in different locations).
* Reinstall only what you need:

  ```bash
  pnpm add -g typescript eslint aws-cdk
  ```
* Check global lists:

  * npm: `npm list -g --depth 0`
  * pnpm: `pnpm list -g --depth 0`

### 3) Corepack integration

Enable Corepack to standardize the pnpm version across machines:

```bash
corepack enable
corepack use pnpm@9.12.0
```

This pins pnpm via the `packageManager` field in `package.json` and avoids accidental npm usage.

### 4) Team-safe migration checklist

1. Verify `pnpm install` works locally
2. Remove `package-lock.json`
3. Commit `pnpm-lock.yaml` and `"packageManager"` field
4. Document pnpm usage in your README

### Quick reference

| Topic         | npm                     | pnpm                     |
| ------------- | ----------------------- | ------------------------ |
| Lockfile      | `package-lock.json`     | `pnpm-lock.yaml`         |
| Local install | `npm install`           | `pnpm install`           |
| Global list   | `npm list -g --depth 0` | `pnpm list -g --depth 0` |
| Store         | `~/.npm`                | `~/.pnpm-store`          |

---

## 🧰 Tips

* Use `pnpm store prune` to clean up unused packages.
* `pnpm dlx <pkg>` is the pnpm equivalent of `npx <pkg>`.
* Add `pnpm-lock.yaml` to version control to ensure consistent installs.

---

## ✅ Best Practices

* Always enable Corepack and pin pnpm version.
* Commit both `packageManager` and `pnpm-lock.yaml`.
* Use workspace setup (`pnpm-workspace.yaml`) for multi-package projects.
* Avoid mixing npm and pnpm installs within the same repo.

---

## 🔗 Related Sections

* [asdf — Runtime version management](../asdf/README.md)
* [brew — CLI tool management](../brew/README.md)
