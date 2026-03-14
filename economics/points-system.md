# Points System

### Play games, earn daily points, unlock creator milestones.

---

## How Points Work

EAISports rewards both sides of the ecosystem:

- **Players** earn points for playing games and growing the network through referrals
- **Creators** earn milestone rewards as their games reach unique visitor thresholds

Points are tied to wallet addresses and visible in the web dashboard. Creator stats are also available through the CLI with `eaisports stats`.

---

## Player Earning

Players earn **10 points per game play per day**. The first rewarded play for a given game on a given day counts. Additional plays on the same game that day do not grant another base play reward.

| Action | Reward | Who Earns |
| --- | --- | --- |
| Playing a game | 10 points | Player |
| Direct referral bonus (L1) | 20% of invitee play points | Referrer |
| Second-level referral bonus (L2) | 10% of L2 invitee play points | Upstream referrer |
| Referral invitee boost | Permanent 20% boost on all play point earnings | Invitee |

{% hint style="success" %}
Referral bonuses stack on top of normal play rewards. A referred player keeps their 20% boost permanently.
{% endhint %}

---

## Creator Milestone Rewards

Creators earn milestone rewards as their games reach unique visitor thresholds.

| Unique Visitors | Reward |
| --- | --- |
| 100 | 500 `$EAISPORTS` |
| 500 | 3,000 `$EAISPORTS` |
| 1,000 | 8,000 `$EAISPORTS` |
| 5,000 | 50,000 `$EAISPORTS` |

These are **milestone rewards**. Each threshold is earned **once** when reached and is not repeated.

---

## Checking Your Balance

### CLI

```bash
eaisports stats
```

Returns creator totals including games, visitors, and rewards earned.

### Web Dashboard

Visit [eaisports.ai/dashboard](https://eaisports.ai/dashboard) and connect your Solana wallet to see:

- Total points
- Per-game visitor counts
- Creator milestone progress
- Referral stats and bonus totals

---

## Wallet Connection

Points are tied to your **Solana wallet address**. The same wallet you configure in the CLI is used to track your web profile.

- **Not required to play** — anyone can play games without a wallet
- **Required to earn** — connecting a wallet enables player rewards, referrals, and creator tracking
- **One wallet, one identity** — points, boosts, and creator milestones are all tracked at the wallet level

---

## Current Status

| Feature | Status |
| --- | --- |
| Player play rewards | Live |
| Referral bonuses | Live |
| Creator milestone rewards | Live |
| Creator dashboard (CLI + Web) | Live |
| Leaderboard system | Live |

{% hint style="info" %}
See [Referral System](referral-system.md) for bonus rules, [Leaderboards](leaderboards.md) for score-based competition, and [Creator Rewards](creator-rewards.md) for the broader creator growth model.
{% endhint %}
