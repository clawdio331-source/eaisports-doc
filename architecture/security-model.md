# Security Model

### Wallet-based identity with signed challenges and sandboxed games.

---

## Authentication

EAISports uses **Solana wallets** as the core identity layer. Protected API operations now use signed wallet challenges to issue short-lived session tokens instead of relying only on raw wallet headers.

| Layer | Mechanism | Scope |
| --- | --- | --- |
| **API Auth** | `Authorization: Bearer <token>` | Protected write operations, player actions, referrals |
| **Wallet Sign-In** | `/api/auth/challenge` + `/api/auth/verify` | Issues JWTs valid for 7 days |
| **Legacy Support** | `X-Wallet-Address` header (deprecated) | Older integrations only |
| **Web Auth** | Solana Wallet Adapter + wallet signature | Dashboard access, protected user actions |
| **CLI Auth** | Wallet address in config | Push, stats, and older creator workflows |

---

## Key Security Decisions

### No API Keys in the CLI

The CLI is distributed publicly via PyPI. Storing platform API keys (Replicate, Supabase) in the CLI would expose them to every user. Instead, all privileged operations (icon generation, storage uploads, score submission) happen server-side through the API.

Creators only provide their **own** AI provider credentials (ChatGPT, OpenRouter, etc.) for AI model access during the build phase.

### Signed Challenge Flow

Protected wallet actions use a challenge-response flow:

1. The client requests a challenge from `/api/auth/challenge`
2. The wallet signs the challenge locally
3. The signed challenge is verified at `/api/auth/verify`
4. The API returns a JWT valid for **7 days**

This proves wallet ownership without introducing passwords, API secrets, or long-lived credentials in client code.

### Game Sandboxing

Games run inside sandboxed iframes with:

```text
allow-scripts allow-same-origin allow-pointer-lock allow-popups allow-downloads
```

Score reporting happens through a `postMessage` bridge rather than direct API access from game code.

### Rate Limiting

| Scope | Limit |
| --- | --- |
| Global | 100 requests per minute per IP |
| Auth endpoints | 10 requests per minute per IP |
| Analytics (visits) | 60 requests per minute per IP |
| Player play | 30 requests per minute per IP |
| Player score | 60 requests per minute per IP |
| Icon generation | 5 requests per hour per wallet |
| Icon backfill | 1 request per minute |

### CORS

The API restricts cross-origin requests to whitelisted origins only (`eaisports.ai` in production). All standard HTTP methods (GET, POST, PUT, DELETE, PATCH) are allowed for whitelisted origins.

---

## Trust Boundaries

```text
Trusted:      API server, Supabase, storage layer
Semi-trusted: CLI (runs on creator's machine), authenticated web shell
Untrusted:    Game code (sandboxed iframe), anonymous browser clients
```

- The API is the single source of truth for game state, player points, referrals, creator stats, and profiles
- Game code cannot call privileged platform APIs directly; score submission is mediated by the platform shell
- Wallet ownership is cryptographically verified for Bearer-token auth flows
- Legacy header-based auth remains only for backward compatibility during the migration window

---

{% hint style="info" %}
For the full API surface, see [API Reference](../reference/api-reference.md).
{% endhint %}
