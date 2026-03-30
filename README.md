# TruEdge Intelligence Agent

Autonomous Indian wealth advisory intelligence system for **TruEdge Financial Services** (ARN-344270).

---

## Quick Start

### 1. Install
```bash
npm install
```

### 2. Add your API key
```bash
cp .env.example .env
```
Open `.env` and set:
```
VITE_ANTHROPIC_API_KEY=sk-ant-api03-your-key-here
```
Get your key: https://console.anthropic.com → API Keys  
⚠️ Web Search requires a **paid Anthropic plan**.

### 3. Run
```bash
npm run dev
```

This starts **two processes** together:
- `server.cjs` — local proxy on port 3001 (forwards requests to Anthropic, handles CORS)
- `vite` — React app on http://localhost:5173

> **Why the proxy?** Browsers block direct calls to api.anthropic.com from localhost (CORS policy). The proxy runs server-side and attaches your API key securely — it never touches the browser.

---

## How it works

```
Browser (localhost:5173)
    │
    │  POST /api/anthropic  (no key needed in browser)
    ▼
Proxy (localhost:3001)  ← reads key from .env
    │
    │  POST https://api.anthropic.com/v1/messages  + x-api-key header
    ▼
Anthropic API  (web_search tool fetches SEBI, AMFI, media)
    │
    ▼
JSON intelligence brief → saved to localStorage
```

---

## Features

| Feature | Details |
|---|---|
| 🌐 Live Web Search | Searches SEBI, AMFI, ET Wealth, Mint, Value Research in real time |
| 🧠 5-Layer Intelligence | Snapshot · Detailed Intel · Advisory Edge · Portfolio Signals · Insurance |
| 🗃️ Persistent Memory | Briefs saved to localStorage — survives restarts, stores 30 briefs |
| ⏰ Auto-Scheduler | Daily or Weekly auto-run while the app is open |

---

## Troubleshooting

| Error | Fix |
|---|---|
| `● Proxy DOWN` in header | Run `npm run dev` (not just `vite`) |
| `Invalid API key` | Check `.env` has correct `VITE_ANTHROPIC_API_KEY` |
| `403 / permission` | Your Anthropic plan doesn't include web search — upgrade at console.anthropic.com |
| `Failed to fetch` | Proxy not running. Stop all, re-run `npm run dev` |

---

## Disclaimer

AMFI Registered Mutual Funds Distributor · ARN No - 344270  
Investment in securities is subject to market risks. For internal advisor use only.
