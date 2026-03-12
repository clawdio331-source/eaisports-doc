# Deployment

### One command to go live.

---

## Push Your Game

```bash
eaisports push my-first-game
```

This does several things automatically:

1. **Bundles** your game's `dist/` directory into a tarball
2. **Uploads** the bundle to the EAISports API
3. **Generates** an AI-created icon for your game
4. **Publishes** the game at `eaisports.ai/play/my-first-game`

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
- **Tracked** — every visitor contributes to your creator stats

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
| **Total Visitors** | Lifetime play count across all games |
| **Points Balance** | Points earned from visitor milestones |
| **Per-Game Breakdown** | Visitors and points for each game |

You can also view your stats on the web dashboard at [eaisports.ai/dashboard](https://eaisports.ai/dashboard) after connecting your wallet.

---

## Updating a Game

To update an existing game, just push again:

```bash
eaisports build --resume my-first-game
# make changes...
eaisports push my-first-game
```

The new bundle replaces the previous version. Your visitor stats and points are preserved.

---

{% hint style="success" %}
**Congratulations!** Your game is live. Share the link, watch your visitor count grow, and earn points for every milestone.
{% endhint %}
