# 🧰 Create a GitHub Repository from CLI

A lightweight place to keep quick notes and tips I often forget.  
This one’s about creating a new **GitHub repository** directly from the terminal.

---

## 💻 Overview

Instead of going to GitHub’s web UI, you can create and configure a new repository  
entirely from the command line using **GitHub CLI (`gh`)** or **GitHub API (`curl`)**.

---

## ⚙️ Method 1: Using GitHub CLI (Recommended)

GitHub provides an official command-line tool called **`gh`**.

### 🪄 Install it

```bash
brew install gh
```

### 🔑 Log in to GitHub

```bash
gh auth login
```

> Follow the prompts:
> Choose GitHub.com
> Choose HTTPS or SSH
> Authenticate via browser or token

