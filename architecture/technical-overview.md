# Technical Overview

### Three repositories, one platform.

---

## System Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   CLI (Python)  │────▶│   API (Fastify)   │◀────│  Web (Next.js)  │
│                 │     │                    │     │                 │
│ - AI agent      │     │ - Game deploy      │     │ - XP desktop    │
│ - Game scaffold │     │ - Creator profiles │     │ - Game browser  │
│ - Local preview │     │ - Analytics        │     │ - Game player   │
│ - Push/deploy   │     │ - Skills registry  │     │ - Dashboard     │
└─────────────────┘     └──────────────────┘     └─────────────────┘
                              │
                        ┌─────┴──────┐
                        │  Supabase  │
                        │ (Postgres) │
                        │ + Storage  │
                        └────────────┘
```

---

## CLI — `eaisports`

| Attribute | Detail |
| --- | --- |
| **Language** | Python 3.11+ |
| **AI Backend** | OpenRouter API (OpenAI-compatible, Claude Opus 4.6 default) |
| **Agent Runtime** | Tool-calling loop with file ops, terminal, browser, memory tools |
| **Session Storage** | SQLite + FTS5 per game session |
| **Package** | [pypi.org/project/eaisports](https://pypi.org/project/eaisports/) |

The CLI is built on a fork of Hermes Agent (Nous Research) with game-building enhancements. It uses an OpenAI-compatible tool-calling agent that iterates through a build loop: the model proposes tool calls, the CLI executes them, and the results feed back into the conversation.

Key modules:
- `run_agent.py` — AIAgent class managing the tool-calling loop
- `eaisports_state.py` — SQLite session management with full-text search
- `tools/` — Tool suite (file operations, terminal, memory, skills, browser)
- `agent/` — Prompt building, context compression, model interface

---

## API — `eaisports-api`

| Attribute | Detail |
| --- | --- |
| **Framework** | Fastify 5 (TypeScript) |
| **Database** | Supabase (PostgreSQL) |
| **Storage** | Supabase Storage (game bundles, icons) |
| **Auth** | Wallet address header (`X-Wallet-Address`) |
| **Hosting** | Railway |

Route groups:
- `/api/games` — Game CRUD, deploy, icon generation
- `/api/creators` — Creator stats and profiles
- `/api/analytics` — Visit tracking
- `/api/skills` — Skills registry
- `/` — Health check

Middleware: CORS, rate limiting (100 req/min global), multipart upload (5MB limit), request logging, centralized error handling.

---

## Web — `eaisports-web`

| Attribute | Detail |
| --- | --- |
| **Framework** | Next.js 15 (React 19, TypeScript) |
| **Styling** | Tailwind CSS 4, xp.css (Windows XP theme) |
| **Wallet** | Solana Wallet Adapter (`@solana/wallet-adapter-react`) |
| **Windows** | react-rnd for draggable XP-style windows |
| **Hosting** | Vercel |

Key pages:
- `/` — XP desktop with game icons, taskbar, start menu
- `/browse` — Arcade game browser with filters
- `/play/[slug]` — Game player (sandboxed iframe)
- `/dashboard` — Creator stats dashboard
- `/skills` — Skills browser

---

## Data Model

| Table | Purpose |
| --- | --- |
| `games` | Game metadata (slug, title, description, genre, status, icon_url) |
| `bundles` | Game bundle records (hash, storage path, version) |
| `creators` | Creator profiles (wallet, display_name, avatar_id, token_balance) |
| `visits` | Per-game visitor tracking |
| `skills` | Published skill registry |

---

{% hint style="info" %}
For API endpoint details, see [API Reference](../appendix/api-reference.md). For CLI commands, see [CLI Reference](../appendix/cli-reference.md).
{% endhint %}
