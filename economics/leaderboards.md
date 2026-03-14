# Leaderboards

### Daily competition, weekly momentum, all-time bragging rights.

---

## Overview

Every published game on EAISports can have its own leaderboard. Players compete on **daily**, **weekly**, and **all-time** boards, with rankings based on submitted game scores.

Leaderboards are game-specific. A strong score in one game does not affect your rank in any other game.

---

## How Scores Are Submitted

Games submit scores through the EAISports SDK message bridge. When a run ends, the game posts a score message to the parent window and the platform forwards it to the API.

```js
window.parent.postMessage({ type: "eaisports:score", score: 4820 }, "*");
```

This keeps score submission inside the platform shell rather than exposing direct API credentials to game code.

---

## Ranking Rules

EAISports stores **one score entry per player per day** for each game. If a player submits multiple scores on the same day, the platform keeps the **highest** score through an upsert.

Public leaderboard views show the **top 10 players**, ranked by score from highest to lowest.

| Period | Behavior |
| --- | --- |
| Daily | Resets automatically every day |
| Weekly | Resets automatically every week |
| All-time | Never resets |

{% hint style="info" %}
Daily and weekly leaderboards reset automatically. All-time boards keep the highest historical results for each game.
{% endhint %}

---

## Payout Pool

Leaderboard rewards are funded from a dynamic points pool:

```text
max(500, visitors * 10)
```

That pool is distributed to top-performing players for the leaderboard period. Higher traffic games create larger pools, but every leaderboard has a minimum payout floor of **500 points**.

---

## Privacy

Leaderboards are public, but wallet addresses are not shown in full. The platform truncates wallets in the display layer so players can verify identity without exposing the entire address.

Example:

```text
9xQe...vW5x
```

---

## Where to Check

Players can view leaderboard standings directly from each game's public leaderboard endpoint and from the web experience where leaderboards are surfaced alongside the game.

{% hint style="success" %}
Games with strong replay loops benefit the most from leaderboards. A reason to replay today, this week, and over the long term increases retention.
{% endhint %}
