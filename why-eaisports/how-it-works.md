# How It Works

### From idea to live game in minutes.

---

## The Creator Flow

```
eaisports init  →  eaisports build  →  eaisports preview  →  eaisports push
   (setup)          (AI builds)         (test locally)        (deploy live)
```

### 1. Setup
Install the CLI and run `eaisports init`. The wizard walks you through connecting your AI provider (ChatGPT, OpenRouter, or any supported provider), your Solana wallet, and your preferred AI model.

### 2. Build
Run `eaisports build my-game` to launch an interactive AI build session. The agent scaffolds a React + Vite project and builds your game through a conversational loop:

- Describe what you want
- The agent writes code using tool calls (file writes, terminal commands)
- Type `/preview` to test in your browser
- Give feedback to refine
- Type `/done` when you're satisfied

### 3. Preview
`eaisports preview my-game` launches a local Vite dev server on port 5173 so you can test your game before deploying.

### 4. Push
`eaisports push my-game` bundles your game's dist/ directory into a tarball, uploads it to the EAISports API, and generates an AI-created icon. Your game is instantly live at `eaisports.ai/play/my-game`.

### 5. Earn
As players discover and play your game, you earn:
- **10 `$EAISPORTS` per unique daily visitor** to your games
- **Milestone bonuses** at 100, 500, 1,000, and 5,000 visitors
- **Referral income** when players you invited play any game

---

## The Player Flow

```
Visit eaisports.ai  →  Browse games  →  Click to play  →  Earn points & compete
```

1. Players land on a Windows XP-themed desktop
2. Games appear as desktop icons and in the arcade browser
3. Click any game to play — it loads instantly in a sandboxed iframe
4. No account required to play, but connecting a Solana wallet enables earning
5. Top scorers share a daily prize pool on every game's leaderboard

---

## Data Flow

```
CLI (Python)  ──POST /api/games/deploy──▶  API (Fastify)  ──▶  Supabase + Cloud Storage
                                                │
Web (Next.js)  ◀──GET /api/games──────────────┘
     │
     └──▶  Player visits  ──POST /api/analytics/visit──▶  API  ──▶  Creator stats
```

- **CLI → API**: Game bundles uploaded via multipart POST with JWT auth
- **API → Storage**: Bundles stored in cloud, metadata in Supabase
- **Web → API**: Game listings, creator stats, profiles fetched via REST
- **Web → API**: Player visits recorded for creator reward tracking
