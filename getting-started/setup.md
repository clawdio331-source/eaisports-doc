# Setup

### Get started in under 2 minutes.

---

## Prerequisites

- **Python 3.11+** — [python.org/downloads](https://www.python.org/downloads/)
- **Node.js 18+** — Required for local game preview ([nodejs.org](https://nodejs.org))
- **Any AI subscription** — ChatGPT Plus/Pro, OpenRouter, or [any supported provider](../reference/ai-providers.md)
- **Solana Wallet** — For creator identity and rewards (e.g., [Phantom](https://phantom.app))

---

## Install

```bash
pip install eaisports
```

Verify the installation:

```bash
eaisports version
```

---

## Configure

Run the interactive setup wizard:

```bash
eaisports init
```

The wizard walks you through:

| Step | What Happens |
| --- | --- |
| **AI Provider** | Choose your provider — ChatGPT (OpenAI Codex), OpenRouter, Nous, or others. If you have ChatGPT Plus/Pro, select OpenAI Codex. |
| **API Key** | Enter your API key (stored locally in `~/.eaisports/.env`, never sent to our servers) |
| **Wallet Address** | Your Solana public key for creator identity |
| **AI Model** | Pick a model from your provider's catalog (e.g., `gpt-5.4`, `claude-opus-4.6`) |

{% hint style="success" %}
**ChatGPT users:** Select "OpenAI Codex" as your provider during init. Your existing ChatGPT Plus or Pro subscription gives you API access — no separate API key purchase needed.
{% endhint %}

---

## Configuration Files

After setup, your config lives at:

```
~/.eaisports/
├── config.yaml     # Provider, model, wallet, preferences
├── .env            # API keys (never committed)
├── games/          # Built games stored here
├── skills/         # Installed skill templates
├── sessions/       # Build session history
└── memories/       # Agent memory across sessions
```

To view your current configuration:

```bash
eaisports config
```

---

## Verify Setup

Run the doctor command to check everything is configured correctly:

```bash
eaisports doctor
```

This checks:
- Python and Node.js versions
- AI provider API key validity
- Wallet address format
- Required dependencies

---

{% hint style="success" %}
**Ready to build?** Head to [Build Your First Game](your-first-game.md) to create your first game.
{% endhint %}
