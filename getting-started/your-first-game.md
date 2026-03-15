# Build Your First Game

### Create a playable browser game in minutes using AI.

---

## Quick Start

```bash
eaisports build my-first-game
```

This launches an interactive AI build session. The agent will:

1. Scaffold a React + Vite project in `~/.eaisports/games/my-first-game/`
2. Ask you what kind of game you want to build
3. Write code iteratively through conversation

---

## The Build Loop

Once the session starts, you're in a conversational loop with the AI agent:

```
You:    "Build a simple snake game with arrow key controls"
Agent:  [creates files, writes game logic]
You:    "/preview"
Agent:  [launches local dev server]
You:    "Make the snake faster and add a score counter"
Agent:  [updates code]
You:    "/done"
Agent:  [finalizes build]
```

### Commands During Build

| Command | What It Does |
| --- | --- |
| `/preview` | Launch local Vite dev server to test your game |
| `/done` | End the build session and finalize |
| Any text | Give feedback, request changes, describe features |

---

## Using Skills

Skills are reusable game templates that give the AI a head start. Instead of describing everything from scratch, use a skill:

```bash
eaisports build --skill trivia my-quiz-game
```

Available built-in skills:

| Skill | Game Type |
| --- | --- |
| `trivia` | Quiz games with categories, scoring, and timers |
| `interactive-fiction` | Text-based narrative games with branching storylines |
| `puzzle-logic` | Logic puzzles, pattern matching, brain teasers |
| `game-ui` | Reusable UI components (menus, HUDs, leaderboards) |
| `mobile` | Mobile-optimized game templates with touch controls |
| `flash-game-feel` | Arcade-style games with classic flash game aesthetics |

List all available skills:

```bash
eaisports skills list
```

---

## Preview Locally

Test your game in the browser before deploying:

```bash
eaisports preview my-first-game
```

This starts a Vite dev server at `http://localhost:5173` with hot module replacement.

---

## Resume a Previous Session

Need to come back to a game later? Resume where you left off:

```bash
eaisports build --resume my-first-game
```

Or browse all your past sessions:

```bash
eaisports sessions browse
```

---

{% hint style="info" %}
**Tip:** Be specific with your feedback. Instead of "make it better", try "add particle effects when the player scores" or "change the background to a gradient from blue to purple".
{% endhint %}

{% hint style="success" %}
**Game ready?** Head to [Deploying](../creators/deploying.md) to push it live and start earning.
{% endhint %}
