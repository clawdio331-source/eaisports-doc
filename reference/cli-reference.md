# CLI Reference

### All commands, flags, and options for the `eaisports` CLI.

---

## Commands

### `eaisports init`

Interactive setup wizard. Configures your AI provider, API key, wallet address, and AI model.

```bash
eaisports init
```

Supported providers: ChatGPT (OpenAI Codex), OpenRouter, Nous Research, Z.AI, Kimi, MiniMax, custom endpoint. See [AI Providers](ai-providers.md) for details.

---

### `eaisports build [slug]`

Launch an AI-powered game build session.

```bash
eaisports build my-game
eaisports build --skill trivia my-quiz
eaisports build --resume my-game
eaisports build -d "a space invaders clone" my-game
```

| Flag | Description |
| --- | --- |
| `--skill <name>` | Use a skill template to seed the build |
| `--resume` | Resume a previous build session |
| `-d <description>` | Start with a game description |

**In-session commands:**
| Command | Description |
| --- | --- |
| `/preview` | Launch local dev server to test |
| `/done` | End the build session |
| Any text | Give feedback or request changes |

---

### `eaisports preview [slug]`

Launch a local Vite dev server for testing.

```bash
eaisports preview my-game
```

Opens at `http://localhost:5173` with hot module replacement.

---

### `eaisports push [slug]`

Deploy a built game to eaisports.ai.

```bash
eaisports push my-game
```

Builds dist/, bundles into tar.gz, computes SHA-256 hash, uploads with idempotency key, generates icon, and publishes live.

---

### `eaisports stats`

View your creator dashboard.

```bash
eaisports stats
```

Shows total games, total visitors, token balance, and per-game breakdown.

---

### `eaisports skills`

Manage game skill templates.

```bash
eaisports skills list              # List installed skills
eaisports skills info <name>       # Show skill details
eaisports skills init <name>       # Create a new skill template
eaisports skills search <query>    # Search available skills
eaisports skills browse            # Browse all available skills
eaisports skills install <id>      # Install from registry
eaisports skills publish <path>    # Publish to registry
eaisports skills audit             # Security scan a skill
```

---

### `eaisports sessions`

Manage build sessions.

```bash
eaisports sessions list            # List recent sessions
eaisports sessions browse          # Interactive session picker
eaisports sessions rename <id> <title>  # Rename a session
eaisports sessions export <file>   # Export session as JSONL
eaisports -c                       # Continue last session
eaisports --resume SESSION_ID      # Resume by ID
```

---

### `eaisports config`

View current configuration.

```bash
eaisports config
```

---

### `eaisports doctor`

Check that everything is configured correctly.

```bash
eaisports doctor
```

Verifies Python/Node versions, AI provider API key, wallet address, and dependencies.

---

### `eaisports insights`

View token usage analytics for the last 30 days.

```bash
eaisports insights
```

---

### `eaisports cron`

Manage scheduled tasks.

```bash
eaisports cron
```

---

### `eaisports status`

Check component health.

```bash
eaisports status
```

---

### `eaisports update`

Check for and install new CLI versions.

```bash
eaisports update
```

---

### `eaisports version`

Show the installed version.

```bash
eaisports version
```

---

## Configuration

### Files

| Path | Purpose |
| --- | --- |
| `~/.eaisports/config.yaml` | Provider, model, wallet, preferences |
| `~/.eaisports/.env` | API keys (never committed) |
| `~/.eaisports/games/` | Built game projects |
| `~/.eaisports/skills/` | Installed skill templates |
| `~/.eaisports/sessions/` | Build session database |
| `~/.eaisports/memories/` | Persistent agent memory |
| `~/.eaisports/logs/` | Agent logs |

### Environment Variables

| Variable | Required | Description |
| --- | --- | --- |
| `OPENROUTER_API_KEY` | If using OpenRouter | API key for OpenRouter |
| `EAISPORTS_API_URL` | No | Override the API base URL (default: `https://api.eaisports.ai`) |

{% hint style="info" %}
API keys for other providers are configured during `eaisports init` and stored in `~/.eaisports/.env`. The specific environment variable depends on your chosen provider.
{% endhint %}

### Default AI Model

Depends on your provider. Common defaults:
- **ChatGPT (Codex):** `gpt-5.4`
- **OpenRouter:** `anthropic/claude-opus-4.6`

Can be changed during `eaisports init` or by editing `~/.eaisports/config.yaml`.

---

## Installation

```bash
pip install eaisports
```

Requires Python 3.11+ and Node.js 18+.
