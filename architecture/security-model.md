# Security Model

### Wallet-based identity with zero shared secrets.

---

## Authentication

EAISports uses **Solana wallet addresses** as the primary identity mechanism. No passwords, no accounts, no email signups.

| Layer | Mechanism | Scope |
| --- | --- | --- |
| **API Auth** | `X-Wallet-Address` header | Deploy, profile updates, icon generation |
| **Web Auth** | Solana Wallet Adapter modal | Profile selection, dashboard access |
| **CLI Auth** | Wallet address in config | Game push, stats retrieval |

---

## Key Security Decisions

### No API Keys in the CLI

The CLI is distributed publicly via PyPI. Storing platform API keys (Replicate, Supabase) in the CLI would expose them to every user. Instead, all privileged operations (icon generation, storage uploads) happen server-side through the API.

Creators only provide their **own** OpenRouter API key for AI model access during the build phase.

### Game Sandboxing

Games run inside sandboxed iframes using `srcdoc` injection. This prevents:

- Access to the parent page's DOM or cookies
- Navigation away from the game
- Cross-origin data exfiltration

### Rate Limiting

| Scope | Limit |
| --- | --- |
| Global | 100 requests per minute per IP |
| Analytics (visits) | 60 requests per minute per IP |

### CORS

The API restricts cross-origin requests to whitelisted origins only (`eaisports.ai` in production). All standard HTTP methods (GET, POST, PUT, DELETE, PATCH) are allowed for whitelisted origins.

---

## Trust Boundaries

```
Trusted:     API server, Supabase, cloud storage
Semi-trusted: CLI (runs on creator's machine with their own API key)
Untrusted:   Game code (sandboxed iframe), browser client
```

- The API is the single source of truth for game state, creator stats, and profiles
- Game code cannot access platform APIs directly — analytics are tracked by the web shell
- Wallet addresses are verified on write operations but not cryptographically signed (current limitation)

---

{% hint style="info" %}
For the full API surface, see [API Reference](../appendix/api-reference.md).
{% endhint %}
