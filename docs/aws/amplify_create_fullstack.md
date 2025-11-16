# 🧰 Full-Stack Setup: GitHub + Next.js + Amplify Gen2 + CI/CD

A concise, practical guide for building a full-stack app using:
- Next.js (pnpm)
- AWS Amplify Gen2 (Backend-as-Code)
- GitHub CLI
- GitHub Actions (CI/CD)
This document walks through creating the project locally, connecting it to GitHub, provisioning an Amplify app in AWS, and deploying via CI/CD.

---

## 🎯 Overview

You will learn how to:
1. Create a GitHub repository from the CLI
2. Scaffold a Next.js app with pnpm
3. Add an Amplify Gen2 backend
4. Run a sandbox backend for development
5. Create an Amplify App (deployment target) in AWS
6. Configure GitHub Secrets
7. Deploy the backend using GitHub Actions
Everything is done from the terminal except the one-time Amplify App creation.

---

## 🧩 1. Create a GitHub Repository from the CLI

Install GitHub CLI:

```bash

brew install gh
gh --version

```

Authenticate:

```bash

gh auth login

```

Follow the prompts:
- GitHub.com
- SSH for Git operations
- “Login with a web browser”
- Enter the one-time code
- Complete authentication

### 📌 Note

- Browser login → GitHub API
- SSH key → Git operations (git push, git pull)

### Create a new repo (fresh project)

```bash

gh repo create

```

Choose:
- Repository name
- public/private
- Local directory / README / gitignore / license (optional)

### Create a repo from an existing directory

```bash

cd my-app
gh repo create --source=. --remote=origin --push --private

```

This will:
- Create the repo on GitHub
- Link it as origin
- Push your local commits

---

## ⚡ 2. Create a Next.js Project (pnpm)

Move to your dev folder:

```bash

cd ~/dev

```

Generate the project:

```bash

pnpm create next-app my-app
cd my-app

```

Choose your preferred options (TypeScript recommended).

---

## 🧱 3. Add Amplify Gen2 to the Project

Inside your Next.js project:

```bash

pnpm create amplify@latest

```

This generates:
- amplify/
- amplify/backend.ts
- Amplify backend CLI dependencies in package.json

Install dependencies:

```bash

pnpm install

```

---

## 🧪 4. Start a Sandbox Backend

Run a temporary backend on AWS for development:

```bash

pnpm ampx sandbox

```

This will:
- Deploy a temporary backend stack
- Generate amplify_outputs.json
- Allow your Next.js app to talk to Amplify

You can specify a profile:

```bash

AWS_PROFILE=my-profile pnpm ampx sandbox

```

---

## 🖥️ 5. Run Next.js Locally

In another terminal:

```bash

pnpm dev

```

Open:

```bash

http://localhost:3000

```

Your app now interacts with the sandbox backend.

---

## 🏗️ 6. Create an Amplify App for Deployment (AWS Console)

Before enabling CI/CD, you must create a deployment target Amplify App in AWS.

Steps:
1. Open AWS Management Console
2. Go to AWS Amplify
3. Click Create App
4. Choose Backend only (Amplify Gen2)
5. Enter a name (e.g., my-app)
6. Finish app creation

This creates a persistent Amplify App where CI/CD can deploy your backend.
You only do this once per environment (e.g., dev, main).

---

## 🆔 7. Get the Amplify App ID

After creating the Amplify App, copy its App ID, such as:

```bash

d123abc4efgh5

```

Alternatively via CLI:

```bash

aws amplify list-apps --query "apps[].{name:name,appId:appId}"

```

---

## 🔐 8. Add GitHub Secrets for CI/CD

Go to:

GitHub → Repository → Settings → Secrets and variables → Actions

Add:

| Name                    | Value                           |
| ----------------------- | ------------------------------- |
| `AWS_ACCESS_KEY_ID`     | IAM user access key             |
| `AWS_SECRET_ACCESS_KEY` | IAM secret key                  |
| `AWS_REGION`            | e.g. `ap-northeast-1`           |
| `AMPLIFY_APP_ID`        | The app ID from Amplify console |

### IAM Permissions

For learning or personal work:
- PowerUserAccess is sufficient.

PowerUserAccess is sufficient.

---

## 🚀 9. Add the CI/CD Workflow (Amplify Gen2 Backend Deploy)

Create the file:

```bash

.github/workflows/amplify-backend-deploy.yml

```

Add:

```yaml

name: Deploy Amplify Gen2 backend

on:
  push:
    branches:
      - main

jobs:
  deploy-backend:
    runs-on: ubuntu-latest

    env:
      AWS_REGION: ${{ secrets.AWS_REGION }}
      AMPLIFY_APP_ID: ${{ secrets.AMPLIFY_APP_ID }}
      BRANCH_NAME: main
      CI: true

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '24'
          cache: 'pnpm'

      - name: Enable corepack
        run: corepack enable

      - name: Install dependencies
        run: pnpm install --frozen-lockfile

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}

      - name: Deploy Amplify backend (Gen2)
        run: |
          pnpm dlx @aws-amplify/backend-cli \
            ampx pipeline-deploy \
              --branch "$BRANCH_NAME" \
              --app-id "$AMPLIFY_APP_ID" \
              --debug

```

---

## 🎉 Done!

You now have a complete workflow:
- Local development with pnpm dev + pnpm ampx sandbox
- GitHub repo created and managed via CLI
- AWS Amplify Gen2 backend added
- Amplify App created as a deployment target
- GitHub Actions pipeline automatically deploying your backend

This setup is ideal for:
- Modern full-stack apps
- Multi-environment workflows
- Continuous delivery with minimal AWS manual work
- Scalable backend-as-code architecture

---
