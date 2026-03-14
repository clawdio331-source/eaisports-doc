# Technical Overview

### Three repositories, one platform.

---

## System Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   CLI (Python)  │────▶│   API (Fastify)   │◀────│  Web (Next.js)  │
│                 │     │                    │     │                 │
│ - AI agent      │     │ - Game deploy      │     │ - XP desktop    │
│ - Game scaffold │     │ - Auth + players   │     │ - Game browser  │
│ - Local preview │     │ - Referrals        │     │ - Game player   │
│ - Push/deploy   │     │ - Leaderboards     │     │ - Dashboard     │
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
| **Auth** | Bearer JWT (`Authorization`) via wallet challenge flow; legacy `X-Wallet-Address` header still supported on older integrations |
| **Hosting** | Railway |

Route groups:
- `/api/auth` — Challenge and verify wallet sign-in
- `/api/games` — Game CRUD, deploy, icon generation, leaderboards
- `/api/player` — Play tracking, score submission, player stats
- `/api/creators` — Creator stats and profiles
- `/api/referral` — Referral codes, application, stats
- `/api/analytics` — Visit tracking
- `/api/skills` — Skills registry
- `/` — Health check

Middleware: CORS, rate limiting (100 req/min global plus route-specific limits), multipart upload (5MB limit), request logging, centralized error handling.

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

| Table | Key Fields | Purpose |
| --- | --- | --- |
| `creators` | `wallet_address` (unique), `codex_id`, `display_name`, `avatar_id` | Creator identity and profile metadata |
| `games` | `creator_id` (FK), `slug` (unique per creator), `title`, `description`, `genre`, `skills_used` (JSONB), `thumbnail_url`, `status` | Published game metadata and lifecycle state |
| `visits` | `game_id` (FK), `visitor_hash`, `visited_at` | Per-game visit tracking with a 24-hour dedup window per visitor |
| `token_ledger` | `creator_id` (FK), `wallet_address`, `amount`, `reason`, `threshold_met` | Creator reward ledger with threshold tracking to prevent double rewards |
| `game_bundles` | `game_id` (FK), `bundle_hash`, `size_bytes`, `format_version`, `storage_path` | Uploaded bundle records and storage metadata |
| `skills` | `name` (unique), `version`, `author`, `description`, `tags` (JSONB), `downloads`, `verified`, `origin`, `bundle_url` | Published skill registry and marketplace metadata |
| `player_points` | `wallet_address`, `game_id` (FK), `amount`, `reason`, `played_on` | Player point rewards with a unique constraint on wallet + game + date for `play_reward` |
| `game_scores` | `game_id` (FK), `wallet_address`, `score`, `played_on` | Per-game leaderboard scores with a unique constraint on game + wallet + date; upserts keep the highest score |
| `leaderboard_payouts` | `game_id` (FK), `payout_date`, `pool_amount`, `results` (JSONB) | Stored leaderboard payout results for each game and period |
| `referral_codes` | `wallet_address` (unique), `code` (unique, 8-char) | Referral code lookup table |
| `referrals` | `referrer_wallet`, `invitee_wallet` (unique) | Referral graph edges with a `CHECK` constraint preventing self-referral |

Row Level Security (RLS) is enabled on all tables. The service role has full access; the anon role is read-only on published games and published skills.

---

{% hint style="info" %}
For API endpoint details, see [API Reference](../appendix/api-reference.md). For CLI commands, see [CLI Reference](../appendix/cli-reference.md).
{% endhint %}
