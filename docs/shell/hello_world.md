# 🐚 Hello World (Bash)

A lightweight place to keep quick notes and tips I often forget.  
This one’s about creating your first **Bash script** on macOS — from zero to execution.

---

## 💻 Overview

Bash scripts let you automate simple tasks on macOS and Linux.  
Here’s the simplest possible example: printing `"Hello, world!"`.

---

## ⚙️ Script

```bash
#!/usr/bin/env bash
# Description: Print a simple greeting.
# Usage: ./hello.sh [name]

set -euo pipefail
IFS=$'\n\t'

main() {
  local name="${1:-World}"
  echo "Hello, $name!"
}

main "$@"
```

### 💡 Tips

- The #!/usr/bin/env bash line ensures your script runs with Bash even if it’s not in /bin/.
- set -euo pipefail makes your script safer (exit on error, undefined vars, and broken pipes).
- $@ passes any command-line arguments to the main function.
- local limits variables to the function’s scope.

---

## 🚀 How to Run

1. Create the file

```bash
touch hello.sh
```

2. Open in VS Code

```bash
code hello.sh
```

3. Paste the script above
4. Make it executable

```bash
chmod +x hello.sh
```

5. Run it

```bash
./hello.sh

./hello.sh dellacraft
```

### 🧾 Output:

```bash
Hello, World!

Hello, dellacraft!
```

---

## 🧠 Notes

| Command             | Description                           |
| ------------------- | ------------------------------------- |
| `chmod +x hello.sh` | Give the file execute permission      |
| `./hello.sh`        | Run the script in the current folder  |
| `bash hello.sh`     | Run without execute permission        |
| `"$@"`              | Forward all arguments to the function |

---

## 🪄 Troubleshooting

| Problem                       | Solution                                           |
| ----------------------------- | -------------------------------------------------- |
| `Permission denied`           | Run `chmod +x hello.sh` first                      |
| `command not found`           | Make sure you’re using `./hello.sh` (include `./`) |
| `zsh: bad interpreter`        | Try changing the shebang to `#!/usr/bin/env bash`  |
| VS Code doesn’t find the file | Check that you’re in the same directory            |

---

## ✅ Quick Recap

- Create a .sh file with a proper shebang
- Add set -euo pipefail for safety
- Make it executable with chmod +x
- Run it via ./script.sh

> 💬 The smallest script you’ll ever write — but the first step to automation.
