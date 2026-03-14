# API Reference

### Complete REST API surface for the EAISports platform.

**Base URL:** `https://api.eaisports.ai`

---

## Authentication

Write operations use a Bearer token header:

```
Authorization: Bearer <token>
```

Tokens are obtained through the wallet challenge flow:

1. `POST /api/auth/challenge`
2. Sign the returned challenge with your wallet
3. `POST /api/auth/verify`

JWTs are valid for **7 days**.

Legacy integrations may still use:

```
X-Wallet-Address: <solana-public-key>
```

{% hint style="warning" %}
`X-Wallet-Address` is deprecated and will be removed in a future release. Use the Bearer token flow for all new integrations.
{% endhint %}

Read operations are public unless noted otherwise.

---

## Auth

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `POST` | `/api/auth/challenge` | No | Request a sign-in challenge. Rate limited: 10/min per IP. |
| `POST` | `/api/auth/verify` | No | Verify a wallet signature and return a JWT. Rate limited: 10/min per IP. |

### Challenge Request

```json
{
  "wallet_address": "9xQeWvG816bUx9EPf5dC7t1k2L4m6n8pQ2rS3tU4vW5x"
}
```

### Challenge Response

```json
{
  "challenge": "Sign this message to authenticate with EAISports.",
  "expires_at": "2026-03-14T12:00:00.000Z"
}
```

### Verify Request

```json
{
  "wallet_address": "9xQeWvG816bUx9EPf5dC7t1k2L4m6n8pQ2rS3tU4vW5x",
  "signature": "base58-signature",
  "challenge": "Sign this message to authenticate with EAISports."
}
```

### Verify Response

```json
{
  "token": "eyJhbGciOi..."
}
```

---

## Games

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/games` | No | List all games. Optional `?status=live` filter. |
| `GET` | `/api/games/:slug` | No | Get game metadata by slug. |
| `POST` | `/api/games/deploy` | Yes | Deploy a game bundle. Multipart form data. |
| `POST` | `/api/games/:slug/generate-icon` | Yes | Generate AI icon for a game. |
| `DELETE` | `/api/games/:slug` | Yes | Delete or unpublish a game. Returns `409` if the game was played in the last 48 hours. |
| `POST` | `/api/games/backfill-icons` | Yes | Batch generate icons for games without them. Rate limited: 1/min. |

### Deploy Request

```
POST /api/games/deploy
Content-Type: multipart/form-data
Authorization: Bearer <token>

Fields:
  bundle:          <file> (tar.gz, max 5MB)
  slug:            string
  wallet_address:  string
  description:     string (optional)
  genre:           string (optional)
```

### Deploy Response

```json
{
  "url": "https://eaisports.ai/play/my-game",
  "tokens_earned": 100,
  "game_id": "uuid"
}
```

---

## Player

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `POST` | `/api/player/play` | Yes | Record a play session. Rate limited: 30/min per IP. |
| `POST` | `/api/player/score` | Yes | Submit a game score. Rate limited: 60/min per IP. |
| `GET` | `/api/player/:wallet/stats` | No | Get player statistics. |

### Play Request

```json
{
  "wallet_address": "9xQeWvG816bUx9EPf5dC7t1k2L4m6n8pQ2rS3tU4vW5x",
  "game_id": "uuid"
}
```

### Play Response

```json
{
  "points_earned": 12,
  "already_played_today": false
}
```

### Score Request

```json
{
  "wallet_address": "9xQeWvG816bUx9EPf5dC7t1k2L4m6n8pQ2rS3tU4vW5x",
  "game_id": "uuid",
  "score": 4820
}
```

### Score Response

```json
{
  "is_new_high": true,
  "rank": 3
}
```

### Player Stats Response

```json
{
  "total_points": 120,
  "games_played": 8,
  "recent_plays": []
}
```

---

## Leaderboards

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/games/:slug/leaderboard` | No | Get a game leaderboard. Optional `?period=daily|weekly|alltime` query. Default: `daily`. |

### Leaderboard Response

```json
[
  {
    "rank": 1,
    "wallet": "9xQe...vW5x",
    "score": 4820,
    "played_on": "2026-03-14"
  }
]
```

---

## Creator Stats & Profiles

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/creators/:wallet/stats` | No | Get creator dashboard stats. |
| `GET` | `/api/creators/:wallet/profile` | No | Get creator profile. |
| `PUT` | `/api/creators/:wallet/profile` | Yes | Update creator profile. |

### Stats Response

```json
{
  "total_games": 3,
  "total_visitors": 231,
  "token_balance": 2000,
  "games": [
    {
      "slug": "my-quiz",
      "visitors": 142,
      "tokens_earned": 1200,
      "status": "live"
    }
  ]
}
```

### Update Profile Request

```json
{
  "display_name": "PlayerOne",
  "avatar_id": "astronaut"
}
```

Valid `avatar_id` values: `guest`, `astronaut`, `chess`, `dog`, `duck`, `guitar`, `horse`, `snowflake`, `soccer`, `fish`, `butterfly`

---

## Referrals

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/referral/:wallet/code` | Yes | Get or create a referral code for a wallet. Ownership is validated. |
| `POST` | `/api/referral/apply` | Yes | Apply a referral code to a wallet. |
| `GET` | `/api/referral/:wallet/stats` | No | Get referral statistics. |

### Apply Referral Request

```json
{
  "wallet_address": "9xQeWvG816bUx9EPf5dC7t1k2L4m6n8pQ2rS3tU4vW5x",
  "code": "AB12CD34"
}
```

### Apply Referral Response

```json
{
  "success": true,
  "referrer_wallet": "7fLm...2Qp9"
}
```

### Referral Stats Response

```json
{
  "total_referrals": 14,
  "l1_count": 10,
  "l2_count": 4,
  "total_bonus_earned": 380
}
```

---

## Analytics

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `POST` | `/api/analytics/visit` | No | Record a game visit. Rate limited: 60/min per IP. |

### Visit Request

```json
{
  "game_id": "uuid",
  "visitor_hash": "string"
}
```

---

## Skills

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/skills` | No | List all published skills. Cached 5 min. |
| `POST` | `/api/skills/publish` | Yes | Publish a skill to the registry. |

---

## Health

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/` | No | Health check. Returns `{ status: "ok" }`. |

---

## Rate Limits

| Scope | Limit |
| --- | --- |
| Global | 100 requests/minute per IP |
| Auth endpoints | 10 requests/minute per IP |
| Analytics visit | 60 requests/minute per IP |
| Player play | 30 requests/minute per IP |
| Player score | 60 requests/minute per IP |
| Icon generation | 5 requests/hour per wallet |
| Icon backfill | 1 request/minute |

---

## Error Responses

All errors follow a consistent format:

```json
{
  "error": "Error message",
  "statusCode": 400
}
```

| Status | Meaning |
| --- | --- |
| `400` | Invalid request body or parameters |
| `401` | Missing or invalid authentication |
| `403` | Wallet address mismatch or ownership validation failed |
| `404` | Resource not found |
| `409` | Conflict with current resource state |
| `429` | Rate limit exceeded |
| `500` | Internal server error |

---

{% hint style="info" %}
For authentication details, see [Security Model](../architecture/security-model.md).
{% endhint %}
