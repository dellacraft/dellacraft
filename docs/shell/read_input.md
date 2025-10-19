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

### 💡 Tips

- -p adds a prompt message before reading input.
- The input is stored in the variable name after read.
- "$@" allows passing command-line args if needed later.

---

### 🔐 Silent Input (Passwords)

You can hide input characters — useful for passwords or tokens.

```bash
read -sp "Enter your password: " password
echo
echo "Password length: ${#password}"
```

💡 -s stands for “silent mode” — no characters are echoed on screen.

---

### 🧮 Multiple Variables

You can read multiple values at once:

```bash
read -p "Enter first and last name: " first last
echo "Welcome, ${first} ${last}!"
```

> If the user types John Doe,  
> → $first="John" and $last="Doe".

---

## 🧩 Common Options

| Option | Meaning                     | Example                      |
| ------ | --------------------------- | ---------------------------- |
| `-p`   | Show a prompt               | `read -p "Name: " name`      |
| `-s`   | Silent (no echo)            | `read -sp "Password: " pass` |
| `-r`   | Don’t interpret backslashes | `read -r line`               |
| `-a`   | Read into an array          | `read -a arr`                |

---

## 🧠 Notes

| Command    | Description                                              |
| ---------- | -------------------------------------------------------- |
| `read var` | Reads one line and stores it in `var`                    |
| `${#var}`  | Returns the length of a variable                         |
| `read -r`  | Recommended when reading raw input (no escaping)         |
| `IFS`      | Defines input field separator; `$IFS` controls splitting |

---

## 🚀 Example Run

```bash
./read_input.sh
```

Output:
```yaml
Enter your name: dellacraft
Hello, dellacraft!
```

---
