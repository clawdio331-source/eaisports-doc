# Building Games

### The AI build loop — from idea to playable game.

---

## Starting a Build

```bash
eaisports build my-game
```

This creates a new game project at `~/.eaisports/games/my-game/` and starts an interactive AI session. The agent scaffolds a React + Vite project and waits for your direction.

You can also start with a description:

```bash
eaisports build -d "a space invaders clone with retro pixel art" my-space-game
```

---

## The Conversational Loop

Building a game is a conversation. You describe what you want, the agent builds it, and you iterate:

1. **Describe** — Tell the agent what kind of game you want
2. **Watch** — The agent writes code, creates files, runs commands
3. **Preview** — Type `/preview` to see it in your browser
4. **Refine** — Give feedback ("make the enemies faster", "add a power-up system")
5. **Finalize** — Type `/done` when you're happy

The agent uses a full tool suite: file operations, terminal commands, browser preview, and persistent memory across sessions.

---

## Using Skills

Skills are game templates that give the agent a head start:

```bash
eaisports build --skill trivia my-quiz
eaisports build --skill puzzle-logic my-puzzle
eaisports build --skill mobile my-mobile-game
```

Skills provide:
- Pre-defined game mechanics and structure
- UI patterns and components
- Best practices for the game type
- Example content and configuration

Browse available skills:

```bash
eaisports skills list                # Installed skills
eaisports skills search "arcade"     # Search registry
eaisports skills browse              # Browse all available
```

---

## Session Management

Every build session is saved automatically. Come back anytime:

```bash
eaisports build --resume my-game     # Resume specific game
eaisports -c                         # Continue last session
eaisports sessions browse            # Pick from all sessions
eaisports sessions list              # See recent sessions
```

Sessions include full conversation history, so the agent remembers everything you've discussed.

---

## Tips for Better Games

- **Be specific** — "Add a particle explosion when enemies die" beats "make it look cooler"
- **Use skills** — They save time and produce more polished results
- **Preview often** — Catch issues early with `/preview`
- **Think about replayability** — Games with high scores, randomized content, and short sessions perform best on leaderboards
- **Test on mobile** — Many players visit eaisports.ai from phones

---

## Execution Backends

The CLI supports multiple environments for running build commands:

| Backend | Use Case |
| --- | --- |
| **Local** | Default — runs on your machine |
| **Docker** | Containerized builds |
| **Modal** | Cloud compute for heavy builds |
| **SSH** | Remote machine execution |
| **Daytona** | Dev container environments |
| **Singularity** | HPC container environments |

Configure via `~/.eaisports/config.yaml` under the `terminal` section.
