# Doyouok — Cron Job & Workflow Monitoring

[![Website](https://img.shields.io/badge/Website-doyouok.com-blue?style=flat-square)](https://doyouok.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

**Doyouok** is a lightweight, zero-install monitoring service for **cron jobs, scripts, database backups, background tasks, and automation workflows**.

It detects when scheduled jobs silently fail, stop running, or miss their expected check-in — and alerts you when something goes wrong.

> **If your job doesn't say "I'm OK", Doyouok lets you know.**

---

## 🚀 How It Works

Doyouok uses a simple HTTP heartbeat mechanism.

```text
Your Job / Script
       │
       │  HTTP Ping
       ▼
┌─────────────────┐
│     Doyouok     │
│  Monitor Check  │
└────────┬────────┘
         │
         │ No check-in
         ▼
      🔔 Alert
```

### 1. Create a Check

Create a monitor at [**doyouok.com**](https://doyouok.com) and get a unique Ping URL.

### 2. Ping When Your Job Succeeds

Send an HTTP request when your job or workflow completes successfully.

### 3. Get Alerted When It Stops

If Doyouok doesn't receive a check-in within the expected interval, you'll receive an alert.

---

## 🛠 Quickstart

### Cron / Shell Script

Add a `curl` request after your job completes successfully:

```bash
0 * * * * /path/to/backup.sh && curl -fsS https://ping.doyouok.com/ping/YOUR-API-KEY
```

The `&&` ensures Doyouok is notified **only when the job succeeds**.

---

### Python

```python
import requests

# Perform your automation / backup task
print("Executing job...")

# Notify Doyouok after successful completion
response = requests.get(
    "https://ping.doyouok.com/ping/YOUR-API-KEY",
    timeout=10
)

response.raise_for_status()

print("Doyouok check-in successful.")
```

---

### n8n / Make / Zapier / Power Automate

Use the native Doyouok integration instead of a generic HTTP request. It creates the check automatically, reports success or failure with a message, and alerts you when a run is missed:

| Platform | Integration | Setup guide |
|---|---|---|
| **n8n** | Verified community node: search "Doyouok" in the nodes panel | [doyouok.com/n8n-help](https://doyouok.com/n8n-help) |
| **Make** | Approved Doyouok app | [doyouok.com/make-help](https://doyouok.com/make-help) |
| **Zapier** | Doyouok app (invite link in the guide) | [doyouok.com/zapier-help](https://doyouok.com/zapier-help) |
| **Power Automate** | Certified Doyouok connector | [doyouok.com/power-automate-help](https://doyouok.com/power-automate-help) |

All integrations: [doyouok.com/integrations](https://doyouok.com/integrations)

On any other platform that can make HTTP requests, call your Ping URL at the end of the workflow:

```text
https://ping.doyouok.com/ping/YOUR-API-KEY
```

---

## 🤖 API and AI agents

- **API reference:** [doyouok.com/docs/api](https://doyouok.com/docs/api)
- **OpenAPI spec:** [doyouok.com/openapi.json](https://doyouok.com/openapi.json)
- **LLM summary:** [doyouok.com/llms.txt](https://doyouok.com/llms.txt)
- **Remote MCP server:** `https://doyouok.com/mcp` (Streamable HTTP, API token in the `Authorization` header; tools `register_check`, `list_checks`, `get_setup_guide`). Listed in the official MCP Registry as `com.doyouok/doyouok`.

---

## 💡 What Can You Monitor?

Doyouok can monitor almost anything that runs on a schedule:

- ⏰ Cron jobs
- 💾 Database backups
- 📦 Data import/export jobs
- 🔄 Background workers
- 🐍 Python scripts
- 🐚 Shell scripts
- ⚙️ Scheduled automation
- 🔗 n8n workflows
- 🤖 Zapier / Make automations
- 🖥️ Server maintenance tasks
- 📊 ETL and data pipelines
- 🔧 Scheduled maintenance scripts

If something runs on a schedule and you need to know when it stops running, Doyouok can monitor it.

---

## ✨ Why Doyouok?

### Zero Installation

No agent, daemon, package, or monitoring software is required.

### Simple HTTP Ping

If your job can make an HTTP request, it can use Doyouok.

### Detect Silent Failures

A cron job can stop running, hang, or fail without anyone noticing.

Doyouok watches for the expected heartbeat and alerts you when it is missing.

### Works Anywhere

Your job can run on:

- Linux
- Windows
- Docker
- VPS
- Cloud servers
- NAS
- Raspberry Pi
- CI/CD environments

No special infrastructure is required.

---

## 💰 Pricing

| Plan | Price | Checks |
|---|---:|---:|
| **Free** | **$0 / month** | 5 |
| **Starter** | **$3 / month** | 35 |
All plans include the core HTTP monitoring functionality.

For the latest pricing and features:

👉 **[View Doyouok Pricing](https://doyouok.com)**

---

## 🔐 No Agent. No Infrastructure Changes.

Doyouok doesn't require anything to be installed on the server running your jobs.

Your existing workflow stays the same:

```text
Existing Job
     │
     ├── Do the work
     │
     └── HTTP Ping → Doyouok
                         │
                         ├── ✓ Check-in received
                         │
                         └── ✕ Check-in missing
                                  │
                                  ▼
                                Alert
```

---

## 📚 Documentation

For setup instructions and integration examples, visit the:

👉 **[Doyouok Documentation](https://doyouok.com/home/docs)**

---

## 🌐 Doyouok

**Website:** [https://doyouok.com](https://doyouok.com)

**Documentation:** [https://doyouok.com/home/docs](https://doyouok.com/home/docs)

Create your first monitor for free:

👉 **[Get started with Doyouok](https://doyouok.com)**

---

## 📄 About This Repository

This public repository contains documentation and client integration examples for **Doyouok**.

The Doyouok monitoring service itself is not open source.

---

## 📄 License

The examples and documentation in this repository are released under the **MIT License**.
