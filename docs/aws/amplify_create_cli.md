# ⚡ Create a Next.js App and Add Amplify Gen2 (with pnpm)

A concise, practical guide for setting up a Next.js app, adding AWS Amplify Gen2,
and running a local development environment using pnpm.

---

## 🎯 Purpose

This note explains how to:
- Scaffold a Next.js project using pnpm
- Add Amplify Gen2 backend to your app
- Launch a sandbox environment on AWS
- Run the application locally while connected to the sandbox backend
All from the terminal.

---

## 🧰 1. Create a Next.js Project (with pnpm)

Move to your development directory:

```bash

cd ~/dev

```

Generate a new Next.js app:

```bash

pnpm create next-app my-app

```

Follow the interactive prompts
(TypeScript, App Router, ESLint, Tailwind, etc. — choose what you prefer).
Move into the project:

```bash

cd my-app

```

---

## 🧱 2. Add Amplify Gen2 to the Project

Initialize Amplify Gen2 inside your Next.js project:

```bash

pnpm create amplify@latest

```

This command generates:
- An amplify/ directory
- amplify/backend.ts
- Necessary dependencies such as @aws-amplify/backend-cli in package.json

---

## 📦 3. Install Dependencies

Just to make sure the environment is consistent:

```bash

pnpm install

```

---

## 🚀 4. Launch Amplify Sandbox (Temporary Cloud Backend)

Start a sandbox backend environment:

```bash

pnpm ampx sandbox

```

What this does:
- Provisions backend resources temporarily on AWS
- Generates amplify_outputs.json
- Enables your frontend to connect to your backend (e.g., API, Auth, Storage)
> On first run, you may be asked to choose an AWS profile or credentials.

Leave the sandbox running while developing.

---

## 🎨 5. Run Next.js Locally

In another terminal tab:

```bash

pnpm dev

```

Then open:

```bash

http://localhost:3000

```

Your local Next.js app will now communicate with the backend created via sandbox.

---

## 🧭 Summary

With these commands:
1. pnpm create next-app my-app
2. pnpm create amplify@latest
3. pnpm ampx sandbox
4. pnpm dev
You get a fully functional Next.js + Amplify Gen2 development environment
— all without deploying production infrastructure.

Perfect for:
- Rapid prototyping
- Testing API/Auth/Storage changes
- Creating modern full-stack apps entirely from local development