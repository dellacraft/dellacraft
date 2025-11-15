# 🧰 Create a GitHub Repository from the CLI

A concise, practical guide for creating GitHub repos directly from the terminal.

---

## 🎯 Purpose

This note explains how to create and manage a GitHub repository entirely from the command line, without opening the GitHub website.
You’ll use:

- GitHub CLI (gh) → for GitHub API operations
- SSH keys → for Git operations (git push, git pull)

### ⚙️ 1. Install GitHub CLI

```bash

brew install gh

```

Verify:

```bash

gh --version

```

### 🔑 2. Authenticate GitHub CLI

Run:

```bash

gh auth login

```

Follow the prompts:
- Choose GitHub.com
- Select SSH for Git operations
- Select “Login with a web browser”（recommended）
- A one-time code appears → paste it into the browser
- Authentication completes

📌 Point
- Web/browser login is for GitHub API
- SSH keys are for Git

### 🆕 3. Create a New Repository (Fresh Project)

If starting a brand-new repo:

```bash

gh repo create

```

Choose:
- Repository name
- Visibility（public / private）
- Whether to create a local directory
- Whether to add README / .gitignore / license
This creates a GitHub remote for you automatically.

### 📁 4. Create a Repo from an Existing Directory

If you already have a project folder:

```bash

cd my-app
gh repo create --source=. --remote=origin --push　--private

```

This will:
- Create a GitHub repository
- Link it as origin
- Push all existing commits

### 📂 5. Initialize Git (if needed)

If the directory isn’t a Git repo yet:

```bash

git init
git add .
git commit -m "Initial commit"
git branch -M main

```

### 🔗 6. Add Remote Manually (Optional)

If gh repo create didn't add the remote:

```bash

git remote add origin git@github.com:<username>/<repo>.git

```

Check:

```bash

git remote -v

```

### 📤 7. Push to GitHub

```bash

git push -u origin main

```

If you configured SSH during gh auth login,
this push will automatically use your SSH key.

### 🧭 8. Useful Shortcuts

Open the repo in your browser:

```bash

gh repo view --web

```

Clone a repo via SSH:

```bash

gh repo clone <username>/<repo>

```

List your repos:

```bash

gh repo list

```

### 🎉 Done!

You now have a fully functional GitHub repository created and pushed
entirely from the terminal.

This workflow is ideal for:
- Quick experiments
- Small utilities
- Personal templates
- Automating project scaffolding