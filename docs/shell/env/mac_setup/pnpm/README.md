
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
