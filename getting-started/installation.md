# Installation

### Get the CLI installed and configured in under 5 minutes.

---

## Prerequisites

- **Python 3.11+** — [python.org/downloads](https://www.python.org/downloads/)
- **Node.js 18+** — Required for local game preview ([nodejs.org](https://nodejs.org))
- **OpenRouter API Key** — For AI model access ([openrouter.ai](https://openrouter.ai))
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

This will prompt you for:

| Setting | Description |
| --- | --- |
| **OpenRouter API Key** | Your API key for AI model access (stored in `~/.eaisports/.env`) |
| **Wallet Address** | Your Solana public key for creator identity |
| **AI Model** | Default: `anthropic/claude-opus-4.6` (can be changed later) |

---

## Configuration Files

After setup, your config lives at:

```
~/.eaisports/
├── config.yaml     # Model, wallet, preferences
├── .env            # API keys (never committed)
├── games/          # Built games stored here
└── skills/         # Installed skill templates
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
- OpenRouter API key validity
- Wallet address format
- Required dependencies

---

{% hint style="success" %}
**Ready to build?** Head to [Build Your First Game](first-game.md) to create your first game.
{% endhint %}
