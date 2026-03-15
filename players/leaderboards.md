# Leaderboards

### Daily competition, weekly momentum, all-time bragging rights.

---

## Overview

Every published game on EAISports has its own leaderboard. Players compete on **daily**, **weekly**, and **all-time** boards, with rankings based on submitted game scores.

Leaderboards are game-specific. A strong score in one game does not affect your rank in any other game.

---

## How Scores Work

Games submit scores through the EAISports SDK message bridge. When a run ends, the game posts a score to the platform:

```js
window.parent.postMessage({ type: "eaisports:score", score: 4820 }, "*");
```

The platform stores **one score entry per player per day** for each game. If you submit multiple scores on the same day, only your **highest** score is kept.

---

## Ranking

Public leaderboards show the **top 10 players**, ranked by score from highest to lowest.

| Period | Behavior |
| --- | --- |
| Daily | Resets every day at midnight UTC |
| Weekly | Resets every week |
| All-time | Never resets |

---

## Prize Pool

Leaderboard rewards are distributed daily from a dynamic points pool:

```
Pool = max(500, daily_unique_visitors × 10)
```

| Rank | Share |
| --- | --- |
| 1st place | 50% of the pool |
| 2nd place | 30% of the pool |
| 3rd place | 20% of the pool |

Higher traffic games create larger pools, but every leaderboard has a minimum payout floor of **500 points**. A game with 200 daily visitors has a **2,000-point pool**.

---

## Privacy

Wallet addresses are truncated in leaderboard displays so players can verify identity without exposing the full address:

```
9xQe...vW5x
```

---

## Where to Check

- **In-game:** Leaderboards appear alongside the game after each play
- **Web:** Visit any game page to see its current leaderboard
- **API:** `GET /api/games/:slug/leaderboard?period=daily|weekly|alltime`

---

{% hint style="success" %}
Games with strong replay loops benefit the most from leaderboards. A reason to replay today, this week, and over the long term drives retention and grows the prize pool.
{% endhint %}
