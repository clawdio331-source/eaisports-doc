# Skills Reference

### Built-in game templates and how to create your own.

---

## Built-In Skills

### `trivia`

**Quiz games with categories, scoring, and timers.**

Best for: Knowledge quizzes, pub trivia, educational games

Features provided:
- Multiple choice questions with 4 options
- Category selection screen
- Per-question timer
- Score tracking with streak bonuses
- Results summary with share button

```bash
eaisports build --skill trivia my-quiz
```

---

### `interactive-fiction`

**Text-based narrative games with branching storylines.**

Best for: Choose-your-own-adventure, visual novels, story games

Features provided:
- Branching narrative structure
- Choice buttons with consequences
- Inventory/state tracking
- Multiple endings
- Save/load progress

```bash
eaisports build --skill interactive-fiction my-story
```

---

### `puzzle-logic`

**Logic puzzles, pattern matching, and brain teasers.**

Best for: Sudoku-style games, matching games, spatial puzzles

Features provided:
- Grid-based puzzle layouts
- Difficulty progression
- Hint system
- Timer and move counter
- Completion celebration

```bash
eaisports build --skill puzzle-logic my-puzzle
```

---

### `game-ui`

**Reusable UI components for any game type.**

Best for: Adding polished UI to custom games

Components provided:
- Main menu screen
- Settings panel
- HUD (score, lives, timer)
- Leaderboard display
- Game over / victory screens

```bash
eaisports build --skill game-ui my-game
```

---

### `mobile`

**Mobile-optimized game templates with touch controls.**

Best for: Games targeting phone and tablet players

Features provided:
- Touch-friendly controls and interactions
- Responsive layouts for various screen sizes
- Mobile performance optimizations
- Gesture support (swipe, tap, hold)

```bash
eaisports build --skill mobile my-mobile-game
```

---

### `flash-game-feel`

**Arcade-style games with classic flash game aesthetics.**

Best for: Retro arcade games, platformers, classic browser games

Features provided:
- Arcade-style game loop and timing
- Retro visual aesthetics
- High score tracking
- Quick restart mechanics
- Classic game feel (screen shake, hit feedback)

```bash
eaisports build --skill flash-game-feel my-arcade-game
```

---

## Creating Custom Skills

### 1. Initialize

```bash
eaisports skills init my-skill
```

Creates `~/.eaisports/skills/my-skill/SKILL.md` with a template.

### 2. Edit the SKILL.md

```yaml
---
name: my-skill
title: My Custom Skill
description: A brief description of what this skill builds
tags: [tag1, tag2]
author: your-name
version: 1.0.0
---

# My Custom Skill

Detailed instructions for the AI agent about how to build
this type of game. Include:

- Required features and mechanics
- UI layout guidelines
- Code patterns and architecture
- Example content structure
```

Skills can also include:
- `templates/` — JSX component templates
- `references/` — Example code, schemas, assets

### 3. Test It

```bash
eaisports build --skill my-skill test-game
```

### 4. Publish (Optional)

Share your skill with the community:

```bash
eaisports skills publish ~/.eaisports/skills/my-skill
```

### 5. Audit (Optional)

Run a security scan on a skill before installing:

```bash
eaisports skills audit my-skill
```

---

## Skill Format Specification

### Frontmatter Fields

| Field | Required | Description |
| --- | --- | --- |
| `name` | Yes | Unique skill identifier (kebab-case) |
| `title` | Yes | Display name |
| `description` | Yes | One-line description |
| `tags` | No | Array of searchable tags |
| `author` | No | Creator name or wallet |
| `version` | No | Semver version string |

### Body

The Markdown body contains instructions that are injected into the AI agent's context when building with the skill. Write it as if you're instructing a developer:

- Be specific about required features
- Include code patterns if you want consistency
- Describe the expected user experience
- List any dependencies or libraries to use

---

## Discovering Skills

```bash
# List all installed skills
eaisports skills list

# Search for skills by keyword
eaisports skills search "quiz"

# Browse all available skills
eaisports skills browse

# View details of a specific skill
eaisports skills info trivia

# Install from registry
eaisports skills install <skill-id>
```

Browse published skills on the web at [eaisports.ai/skills](https://eaisports.ai/skills).
