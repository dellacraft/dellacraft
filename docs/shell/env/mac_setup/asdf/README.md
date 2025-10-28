
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

## 🧩 Best Practices

* Always include `.tool-versions` in your repo.
* Prefer **local version locking (`asdf local`)** for project-specific environments.
* Use `asdf install` on new machines to automatically install required versions.
* Run `asdf plugin update --all` periodically.

---

## 🔗 Related Sections

* [brew — CLI tool management](../brew/README.md)
* [pnpm — Node package management](../pnpm/README.md)
