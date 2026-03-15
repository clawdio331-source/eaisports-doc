# Referral System

### Invite players, grow the network, earn bonus points.

---

## Overview

EAISports uses a **2-level referral system** to grow the player base and reward the wallets bringing new players into the ecosystem.

When a player joins through a referral code, the platform tracks the direct referrer (L1) and the upstream referrer (L2). Bonus points are applied automatically as the invitee earns play rewards.

---

## Getting a Referral Code

Referral codes are managed through the web dashboard:

1. Connect your Solana wallet
2. Open the dashboard at [eaisports.ai/dashboard](https://eaisports.ai/dashboard)
3. Your code is auto-generated when eligible

Referral codes are:

- **5-character hex strings** (e.g., `A1B2C`)
- **One per wallet**
- **Available after you've been referred yourself or you are a creator**

{% hint style="info" %}
You do not need to manually request a code. If your wallet is eligible, the dashboard creates it automatically.
{% endhint %}

---

## Applying a Code

Referral codes can only be applied once per wallet. This keeps the referral graph stable and prevents reward abuse.

The platform enforces three core rules:

- **One-time only** — once a wallet has a referrer, it cannot be changed
- **No self-referrals** — you cannot apply your own code
- **No circular referrals** — referral chains cannot loop back to a previous wallet

---

## Bonus Structure

| Participant | Bonus |
| --- | --- |
| **Invitee** | Permanent **20% boost** on all play point earnings |
| **L1 referrer (direct)** | **20%** of the invitee's play points as bonus |
| **L2 referrer (upstream)** | **10%** of the L2 invitee's play points as bonus |

Referral bonuses apply to **player play rewards** only. They do not affect leaderboard rank logic or creator milestone rewards.

### How It Compounds

Say you refer 10 active players who each earn 100 points/day:
- You earn **200 bonus points/day** (20% × 100 × 10)
- If those 10 players each refer 5 more players earning 50 points/day, you earn an additional **250 points/day** (10% × 50 × 50)
- Total passive income: **450 points/day** from your referral network

---

## Checking Your Stats

The dashboard shows referral performance in real time:

- Your referral code
- Total referrals (L1 + L2)
- L1 referral count
- L2 referral count
- Total bonus points earned from referrals

---

{% hint style="success" %}
Strong referral trees compound over time. An active invitee earns more than a one-time signup because their future play rewards continue to generate bonuses for you.
{% endhint %}
