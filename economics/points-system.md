# Points System

### Play games, earn points, climb the ranks.

---

## How Points Work

EAISports tracks **visitor milestones** for every published game. When players visit and play your games, you earn points based on engagement thresholds.

Points are tracked per creator wallet and visible on both the CLI (`eaisports stats`) and the web dashboard.

---

## Earning Points

| Action | Points | Who Earns |
| --- | --- | --- |
| Publishing a game | Awarded on first deploy | Creator |
| Visitor milestones | Up to 50,000 pts per game | Creator |
| Playing games | Tracked for future rewards | Player (planned) |

### Visitor Milestones

Creators earn points as their games reach visitor count thresholds. The more people play your game, the more you earn.

{% hint style="success" %}
**Points are cumulative.** Publishing multiple popular games compounds your total balance.
{% endhint %}

---

## Checking Your Balance

### CLI

```bash
eaisports stats
```

Returns your total games, total visitors, and points balance.

### Web Dashboard

Visit [eaisports.ai/dashboard](https://eaisports.ai/dashboard) and connect your Solana wallet to see:

- Points balance
- Per-game visitor counts
- Per-game points earned
- Total lifetime visitors

---

## Wallet Connection

Points are tied to your **Solana wallet address**. The same wallet you configure in the CLI is used to track your web profile.

- **Not required to play** — anyone can play games without a wallet
- **Required to earn** — connecting a wallet enables points tracking and profile features
- **Non-signed users see a prompt** — game end screens remind disconnected players about the rewards they're missing

---

## Current Status

| Feature | Status |
| --- | --- |
| Points tracking per creator | Live |
| Visitor milestone rewards | Live |
| Creator dashboard (CLI + Web) | Live |
| Player rewards | Planned |
| Token economy | Planned |

{% hint style="info" %}
The points system is the foundation for a future token economy. See [Creator Rewards](creator-rewards.md) for details on reward tiers and [Vision](../roadmap/vision.md) for long-term economic plans.
{% endhint %}
