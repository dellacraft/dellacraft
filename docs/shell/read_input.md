# 🧠 Read User Input (Bash)

A lightweight place to keep quick notes and tips I often forget.  
This one’s about reading user input from the terminal and storing it in a variable.

---

## 💻 Overview

The `read` command allows Bash scripts to take **interactive input** from the user —  
for example, asking for a name, password, or confirmation before continuing.

---

## ⚙️ Basic Example

```bash
#!/usr/bin/env bash
# Description: Simple example of reading user input.
# Usage: ./read_input.sh

set -euo pipefail
IFS=$'\n\t'

main() {
  read -p "Enter your name: " name
  echo "Hello, $name!"
}

main "$@"
```

