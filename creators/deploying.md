# Deploying

### One command to go live.

---

## Push Your Game

```bash
eaisports push my-first-game
```

This does several things automatically:

1. **Builds** your game with `npm run build`
2. **Bundles** the `dist/` directory into a tar.gz archive
3. **Computes** a SHA-256 hash for deduplication (skip upload if nothing changed)
4. **Uploads** the bundle to the EAISports API with idempotency protection
5. **Generates** an AI-created Windows XP-style icon for your game
6. **Publishes** the game at `eaisports.ai/play/my-first-game`

---

## What Gets Deployed

The push command sends your built game files (HTML, JS, CSS, assets) to cloud storage. The API creates or updates the game record in the database with metadata like title, description, and genre.

{% hint style="warning" %}
**Make sure your game builds first.** Run `eaisports preview` to verify your game works locally before pushing. The push command bundles the `dist/` output — if there's no build, there's nothing to push.
{% endhint %}

---

## After Deployment

Your game is immediately:

- **Playable** at `eaisports.ai/play/your-slug`
- **Discoverable** in the arcade browser and as a desktop icon
- **Shareable** with a direct URL and auto-generated Open Graph image
- **Tracked** — every visitor contributes to your creator stats and milestones

---

## Check Your Stats

See how your games are performing:

```bash
eaisports stats
```

This shows:

| Metric | Description |
| --- | --- |
| **Total Games** | Number of games you've published |
| **Total Visitors** | Lifetime unique visitor count across all games |
| **Token Balance** | `$EAISPORTS` tokens earned from milestones |
| **Per-Game Breakdown** | Visitors and tokens for each game |

You can also view your stats on the web dashboard at [eaisports.ai/dashboard](https://eaisports.ai/dashboard) after connecting your wallet.

---

## Updating a Game

To update an existing game, just build and push again:

```bash
eaisports build --resume my-first-game
# make changes...
eaisports push my-first-game
```

The new bundle replaces the previous version. Your visitor stats and milestones are preserved. If the bundle hash matches the existing version, the upload is skipped.

---

## Deleting a Game

Games can be deleted if they haven't been played in the last 48 hours:

```bash
# Via API — DELETE /api/games/:slug
```

Games with recent player activity cannot be deleted to protect leaderboard integrity.

---

{% hint style="success" %}
**Congratulations!** Your game is live. Share the link, watch your visitor count grow, and earn tokens for every milestone.
{% endhint %}
