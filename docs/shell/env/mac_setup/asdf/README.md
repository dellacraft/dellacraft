# ⚙️ asdf Setup

asdf is a **version manager** for multiple runtime environments such as Node.js, Python, Go, and more. It ensures consistent development environments across machines and projects.

---

## 🧭 Overview

* Manages runtime versions per project (Node.js, Python, etc.).
* Prevents version drift between developers or CI environments.
* Integrates easily with tools like direnv for auto-switching.

---

## 🚀 Installation & Usage

```bash
# Install asdf via Homebrew
brew install asdf

# Add Node.js plugin (first time only)
asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git

# List available Node versions
asdf list all nodejs | grep '^22\.'

# Install and set Node 22.x
asdf install nodejs 22.8.0
asdf local nodejs 22.8.0     # Lock Node version for this project
```

---

## 📄 Example `.tool-versions`

This file defines the runtime versions used in your project and should be committed to version control.

```
nodejs 22.8.0
```

> You can add other runtimes like `python`, `golang`, or `java` to the same file.

---

## ⚙️ direnv Integration (Optional)

To automatically switch versions when entering a directory:

```bash
brew install direnv
# In your shell config (.zshrc or .bashrc):
eval "$(direnv hook zsh)"
```

Then, in your project:

```bash
echo 'use asdf' > .envrc
direnv allow
```

Now `asdf` automatically activates the correct Node version when you `cd` into the directory.

---

## 🧩 How Installation Works

* `.tool-versions` declares which versions should be used.
* `asdf install` reads `.tool-versions` and installs missing runtimes.
* Once installed, `asdf` automatically switches to the correct version whenever you run commands.

### Typical Flow

```bash
# 1. Clone the repo
cd my-project

# 2. Install required versions from .tool-versions
asdf install

# 3. Use the specified version automatically
node -v   # v22.8.0
```

> You only need to install each version once. After that, it is reused across projects.

---

## 🧱 Version Management

### 🔍 Check Installed Versions

```bash
asdf list nodejs
```

Example output:

```
  20.12.2
* 22.8.0
```

* `*` marks the currently active version.

### 📦 Check Currently Active Versions for All Tools

```bash
asdf current
```

Example:

```
nodejs   22.8.0   (set by /Users/you/projects/my-app/.tool-versions)
python   3.12.1   (set by /Users/you/.tool-versions)
```

### 🧰 Show All Installed Versions

```bash
asdf list
```

### 📁 Check Where Versions Are Installed

```bash
ls ~/.asdf/installs/nodejs/
# => 20.12.2  22.8.0
```

| Command                      | Purpose                                      |
| ---------------------------- | -------------------------------------------- |
| `asdf list <lang>`           | Show installed versions                      |
| `asdf current`               | Show active versions and source files        |
| `asdf list`                  | List all installed tools and versions        |
| `asdf list all <lang>`       | Show all available versions for installation |
| `ls ~/.asdf/installs/<lang>` | Check actual installation directories        |

---

## 🧩 Best Practices

* Always include `.tool-versions` in your repo.
* Prefer **local version locking (`asdf local`)** for project-specific environments.
* Use `asdf install` on new machines to automatically install required versions.
* Run `asdf plugin update --all` periodically.

---

## 🔗 Related Sections

* [brew — CLI tool management](../brew/README.md)
* [pnpm — Node package management](../pnpm/README.md)
