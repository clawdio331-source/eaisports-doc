# Skills System

### Reusable game templates that supercharge the AI build process.

---

## What Are Skills?

Skills are structured templates (YAML frontmatter + Markdown instructions) that seed the AI agent with domain-specific knowledge for building certain types of games. Instead of describing every detail from scratch, a skill gives the agent a blueprint.

```bash
# Build a trivia game using the trivia skill
eaisports build --skill trivia my-quiz
```

---

## Skill Format

Each skill is a directory containing a `SKILL.md` file:

```
~/.eaisports/skills/trivia/
└── SKILL.md
```

The `SKILL.md` file has YAML frontmatter followed by Markdown instructions:

```yaml
---
name: trivia
title: Trivia Game
description: Quiz games with categories, scoring, and timers
tags: [quiz, trivia, scoring]
author: eaisports
version: 1.0.0
---

# Trivia Game Template

Build a trivia quiz game with the following features:
- Multiple choice questions with 4 options
- Category selection
- Score tracking with streak bonuses
- Timer per question
...
```

---

## Built-In Skills

| Skill | Description |
| --- | --- |
| `trivia` | Quiz games with categories, scoring, and timers |
| `interactive-fiction` | Text-based narrative games with branching storylines |
| `puzzle-logic` | Logic puzzles, pattern matching, brain teasers |
| `game-ui` | Reusable UI components (menus, HUDs, leaderboards) |
| `mobile` | Mobile-optimized game templates with touch controls |
| `flash-game-feel` | Arcade-style games with classic flash game aesthetics |

---

## Skill Lifecycle

### 1. Use
Apply a skill when building a new game:
```bash
eaisports build --skill trivia my-quiz
```

### 2. Create
Create a new skill template from scratch:
```bash
eaisports skills init my-custom-skill
```

### 3. Publish
Share your skill with the community via the skills registry:
```bash
# Skills are published through the API
POST /api/skills/publish
```

### 4. Discover
Browse and search available skills:
```bash
eaisports skills list
eaisports skills search "puzzle"
eaisports skills info trivia
```

---

## Skills Registry

Published skills are stored in the EAISports API and accessible to all users. The web platform includes a skills browser at [eaisports.ai/skills](https://eaisports.ai/skills) where users can explore available templates.

The API caches the skills list for 5 minutes to reduce database load.

---

{% hint style="info" %}
For the full list of built-in skills and their specifications, see [Skills Reference](../reference/skills-reference.md).
{% endhint %}
