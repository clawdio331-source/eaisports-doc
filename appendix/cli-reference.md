# CLI Reference

### All commands, flags, and options for the `eaisports` CLI.

---

## Commands

### `eaisports init`

Interactive setup wizard. Configures API key, wallet address, and AI model.

```bash
eaisports init
```

---

### `eaisports build [slug]`

Launch an AI-powered game build session.

```bash
eaisports build my-game
eaisports build --skill trivia my-quiz
eaisports build --resume my-game
```

| Flag | Description |
| --- | --- |
| `--skill <name>` | Use a skill template to seed the build |
| `--resume` | Resume a previous build session |

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

Bundles `dist/`, uploads to the API, generates an icon, and publishes the game live.

---

### `eaisports stats`

View your creator dashboard.

```bash
eaisports stats
```

Shows total games, total visitors, points balance, and per-game breakdown.

---

### `eaisports skills`

Manage game skill templates.

```bash
eaisports skills list              # List installed skills
eaisports skills info <name>       # Show skill details
eaisports skills init <name>       # Create a new skill template
eaisports skills search <query>    # Search available skills
```

---

### `eaisports sessions browse`

Browse and resume past build sessions.

```bash
eaisports sessions browse
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

Verifies Python/Node versions, API key, wallet address, and dependencies.

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
| `~/.eaisports/config.yaml` | Model, wallet, preferences |
| `~/.eaisports/.env` | API keys (OPENROUTER_API_KEY) |
| `~/.eaisports/games/` | Built game projects |
| `~/.eaisports/skills/` | Installed skill templates |

### Environment Variables

| Variable | Required | Description |
| --- | --- | --- |
| `OPENROUTER_API_KEY` | Yes | API key for AI model access via OpenRouter |
| `EAISPORTS_API_URL` | No | Override the API base URL (default: `https://api.eaisports.ai`) |

### Default AI Model

`anthropic/claude-opus-4.6` via OpenRouter. Can be changed during `eaisports init` or by editing `~/.eaisports/config.yaml`.

---

## Installation

```bash
pip install eaisports
```

Requires Python 3.11+ and Node.js 18+.
