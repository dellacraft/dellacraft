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

