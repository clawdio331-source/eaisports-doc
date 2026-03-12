# EAISports

**Build AI-powered games. Deploy in seconds. Earn rewards.**

> EAISports is a full-stack platform that lets anyone create browser-based games using AI, deploy them to the cloud with a single command, and earn points as players discover and play them.

---

## How It Works

1. **Build** — Use the CLI to spin up an AI agent that builds your game through conversation
2. **Preview** — Test locally with a built-in dev server
3. **Push** — One command deploys your game live at eaisports.ai
4. **Play** — Players discover your game on a retro Windows XP-themed desktop
5. **Earn** — Creators earn points for every visitor milestone

---

## Quick Navigation

| Section | What You'll Learn |
| --- | --- |
| [What is EAISports?](overview/what-is-eaisports.md) | Platform overview and key features |
| [Installation](getting-started/installation.md) | Get the CLI installed and configured |
| [Build Your First Game](getting-started/first-game.md) | Step-by-step game creation tutorial |
| [Technical Overview](architecture/technical-overview.md) | How the platform is built |
| [Points & Rewards](economics/points-system.md) | How creators earn |
| [API Reference](appendix/api-reference.md) | Full REST API documentation |
| [CLI Reference](appendix/cli-reference.md) | All CLI commands and options |

---

## Tech Stack

| Layer | Stack |
|-------|-------|
| **CLI** | Python 3.11+, OpenRouter (Claude Opus 4.6), tool-calling agent |
| **API** | Fastify 5, TypeScript, Supabase (PostgreSQL), cloud storage |
| **Web** | Next.js 15, React 19, Tailwind CSS, xp.css, Solana Wallet Adapter |
| **Auth** | Solana wallet (public key as identity) |

---

## Links

- **Website**: [eaisports.ai](https://eaisports.ai)
- **Documentation**: [docs.eaisports.ai](https://docs.eaisports.ai)
- **GitHub**: [github.com/clawdio331-source/eaisports](https://github.com/clawdio331-source/eaisports)
- **PyPI**: [pypi.org/project/eaisports](https://pypi.org/project/eaisports/)

{% hint style="info" %}
**Documentation Version:** v1.0 · March 2026
{% endhint %}
