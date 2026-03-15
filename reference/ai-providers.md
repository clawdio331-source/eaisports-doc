# AI Providers

### Use the AI you already pay for.

---

## Overview

EAISports works with **7 AI providers**. You don't need to buy a new API key — if you already have a ChatGPT subscription or any other AI service, you can connect it and start building games immediately.

During `eaisports init`, the wizard asks you to select your provider and enter your credentials. Everything is stored locally in `~/.eaisports/.env` and never sent to EAISports servers.

---

## ChatGPT (OpenAI Codex)

**Already have ChatGPT Plus or Pro? This is the fastest way to start.**

Your existing ChatGPT subscription includes API access through OpenAI Codex. Select "OpenAI Codex" during `eaisports init` and connect your account.

| Detail | Value |
| --- | --- |
| **Provider ID** | `codex` |
| **Auth** | OpenAI account (ChatGPT Plus/Pro subscription) |
| **Recommended Models** | `gpt-5.4`, `gpt-4.1` |
| **Best For** | Anyone already paying for ChatGPT who wants to start building immediately |

```bash
eaisports init
# Select: OpenAI Codex
# Follow the authentication flow
```

---

## OpenRouter

**Access 100+ models through a single API key.**

OpenRouter is an AI aggregator that gives you access to models from OpenAI, Anthropic, Google, Meta, and many others through one unified API.

| Detail | Value |
| --- | --- |
| **Provider ID** | `openrouter` |
| **Auth** | API key from [openrouter.ai](https://openrouter.ai) |
| **Env Variable** | `OPENROUTER_API_KEY` |
| **Recommended Models** | `anthropic/claude-opus-4.6`, `openai/gpt-5.4`, `google/gemini-2.5-pro`, `qwen/qwen3-235b-a22b` |
| **Best For** | Power users who want to switch between models |

```bash
eaisports init
# Select: OpenRouter
# Enter your API key
```

---

## Nous Research

**Custom open-source models via the Nous portal.**

| Detail | Value |
| --- | --- |
| **Provider ID** | `nous` |
| **Auth** | Nous Research portal credentials |
| **Best For** | Open-source model enthusiasts |

---

## Z.AI / GLM

**GLM-family models from Zhipu AI.**

| Detail | Value |
| --- | --- |
| **Provider ID** | `zai` |
| **Auth** | Z.AI API key |
| **Best For** | GLM model users |

---

## Kimi / Moonshot

**Moonshot AI models.**

| Detail | Value |
| --- | --- |
| **Provider ID** | `kimi` |
| **Auth** | Moonshot API key |
| **Best For** | Kimi/Moonshot users |

---

## MiniMax

**Global and China region support.**

| Detail | Value |
| --- | --- |
| **Provider ID** | `minimax` |
| **Auth** | MiniMax API key |
| **Best For** | Users in China or wanting MiniMax models |

---

## Custom Endpoint

**Bring any OpenAI-compatible API.**

If you have access to any service that exposes an OpenAI-compatible chat completions endpoint, you can use it with EAISports.

| Detail | Value |
| --- | --- |
| **Provider ID** | `custom` |
| **Auth** | Your API key + base URL |
| **Best For** | Self-hosted models, corporate APIs, or niche providers |

```bash
eaisports init
# Select: Custom Endpoint
# Enter your base URL and API key
```

---

## Switching Providers

You can change your provider at any time:

```bash
eaisports init   # Re-run the wizard
```

Or edit `~/.eaisports/config.yaml` directly to change the `model` and provider settings.

---

## Model Selection

Each provider has a curated list of recommended models shown during `eaisports init`. You can also specify any model your provider supports:

```yaml
# In ~/.eaisports/config.yaml
model: anthropic/claude-opus-4.6    # OpenRouter format
model: gpt-5.4                      # OpenAI Codex format
```

The model can also be switched at runtime during build sessions.
