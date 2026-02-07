# 🤖 n8n Multi-Agent Workflow System (Supervisor Orchestrator)

This repository contains the **Supervisor Orchestrator** workflow for handling user requests, coordinating internal agents, and handing off a PR to a downstream workflow.

## ✅ What this repo does
- Chats naturally with the user (no formal recaps)
- Asks 1–2 short clarification questions only if needed
- Waits for explicit approval keyword: **ابدأ**
- Runs two internal agents in sequence:
  1. **Prompt Engineer Agent**
  2. **Programmer Agent**
- Sends the final contract to the downstream workflow **github_pr_agent**

> **Note:** Deployment is **not** triggered here. Deployment will be handled later by Repo 3 after the PR is merged.

---

## 📦 How to import the Supervisor workflow
1. Open n8n → **Workflows** → **Import from File**
2. Import the JSON file:
   - `workflows/Supervisor_agent_fully_sanitized.json`
3. Set your credentials (see below).

---

## 🔐 Required credentials (placeholders)
You must configure these credentials in n8n:
- **LLM Provider** (OpenAI/Codex via API)
  - Credential name can be anything, but the workflow expects an LLM Chat node to be connected.
- **Telegram Trigger + Telegram Send Message**
  - Bot token for receiving and sending messages

---

## 🧭 Project registry
Project configuration lives in **`project-registry.json`**.

To add future shops, edit:
```
project-registry.json
```

Current entry (shop3) includes:
- `repo_owner` and `repo_name` placeholders
- `base_branch: main`
- `server_path: /var/www/shop3`
- `pm2_process: shop3-api`
- `frontend_folder: frontend`

---

## ✅ PR merge + deployment flow
- The Supervisor Orchestrator only creates a PR via **github_pr_agent**.
- The user manually merges the PR.
- **Deployment is triggered separately in Repo 3** (not in this repo).

---

## 📁 Folder Structure
- `/workflows`: n8n JSON exports
- `/docs`: technical docs
- `/assets`: optional diagrams
