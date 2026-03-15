# EAISports

**Your ChatGPT subscription is a money machine.**

> You already pay for ChatGPT. EAISports turns that subscription into a game development studio. Describe a game, watch AI build it, deploy it in one command, and earn `$EAISPORTS` tokens as players discover and play your games.

---

## How It Works

1. **Install** — `pip install eaisports`
2. **Connect** — Link your ChatGPT account (or any AI provider) and Solana wallet
3. **Build** — Describe your game idea. The AI agent builds it through conversation.
4. **Push** — One command deploys your game live at eaisports.ai
5. **Earn** — Get tokens for every player milestone, climb leaderboards, grow your network

---

## Quick Start

```bash
pip install eaisports
eaisports init        # Connect your AI + wallet
eaisports build       # Describe your game, AI builds it
eaisports preview     # Test locally
eaisports push        # Deploy live — start earning
```

---

## Quick Navigation

| Section | What You'll Learn |
| --- | --- |
| [What is EAISports?](why-eaisports/what-is-eaisports.md) | Platform overview and the viral loop |
| [Setup](getting-started/setup.md) | Install and configure in 2 minutes |
| [Build Your First Game](getting-started/your-first-game.md) | From idea to live game in 5 minutes |
| [Start Earning](getting-started/start-earning.md) | How the money flows |
| [AI Providers](reference/ai-providers.md) | ChatGPT, OpenRouter, and 5 more options |
| [Creator Rewards](creators/creator-rewards.md) | Milestones, tokens, and the creator flywheel |
| [API Reference](reference/api-reference.md) | Full REST API documentation |
| [CLI Reference](reference/cli-reference.md) | All CLI commands and options |

---

## Use the AI You Already Pay For

| Provider | Best For |
|----------|----------|
| **ChatGPT (OpenAI Codex)** | Already have ChatGPT Plus or Pro? You're ready to go. |
| **OpenRouter** | Access 100+ models (Claude, GPT, Gemini, etc.) through one API key |
| **Nous Research** | Custom open-source models via the Nous portal |
| **Z.AI / GLM** | GLM-family models |
| **Kimi / Moonshot** | Moonshot AI models |
| **MiniMax** | Global and China regions |
| **Custom Endpoint** | Any OpenAI-compatible API you already have access to |

---

## Tech Stack

| Layer | Stack |
|-------|-------|
| **CLI** | Python 3.11+, multi-provider AI agent (ChatGPT, OpenRouter, +5 more), tool-calling loop |
| **API** | Fastify 5, TypeScript, Supabase (PostgreSQL), cloud storage |
| **Web** | Next.js 15, React 19, Tailwind CSS, xp.css, Solana Wallet Adapter |
| **Auth** | Solana wallet (public key as identity) |

---

## Links

- **Website**: [eaisports.ai](https://eaisports.ai)
- **Documentation**: [docs.eaisports.ai](https://docs.eaisports.ai)
- **PyPI**: [pypi.org/project/eaisports](https://pypi.org/project/eaisports/)
