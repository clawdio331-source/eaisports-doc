# API Reference

### Complete REST API surface for the EAISports platform.

**Base URL:** `https://api.eaisports.ai`

---

## Authentication

Write operations require a wallet address header:

```
X-Wallet-Address: <solana-public-key>
```

Read operations are public (no auth required).

---

## Games

| Method | Endpoint | Auth | Description |
| --- | --- | --- | --- |
| `GET` | `/api/games` | No | List all games. Optional `?status=live` filter. |
| `GET` | `/api/games/:slug` | No | Get game metadata by slug. |
| `POST` | `/api/games/deploy` | Yes | Deploy a game bundle. Multipart form data. |
| `POST` | `/api/games/:slug/generate-icon` | Yes | Generate AI icon for a game. |

### Deploy Request

```
POST /api/games/deploy
Content-Type: multipart/form-data
X-Wallet-Address: <wallet>

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
| Analytics | 60 requests/minute per IP |

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
| `403` | Wallet address mismatch |
| `404` | Resource not found |
| `429` | Rate limit exceeded |
| `500` | Internal server error |

---

{% hint style="info" %}
For authentication details, see [Security Model](../architecture/security-model.md).
{% endhint %}
