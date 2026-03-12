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

### 3. Test It

```bash
eaisports build --skill my-skill test-game
```

### 4. Publish (Optional)

Share your skill with the community through the skills registry API:

```
POST /api/skills/publish
X-Wallet-Address: <your-wallet>
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

# View details of a specific skill
eaisports skills info trivia
```

Browse published skills on the web at [eaisports.ai/skills](https://eaisports.ai/skills).
