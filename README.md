# ⚽ Last Squad Standing — World Cup 2026 Sweepstake

A live, phone-friendly leaderboard for a 16-player friends-and-family World Cup 2026
sweepstake. Each player owns **3 countries**; you stay **in** while one of them is
still in the world cup, and you're **out** when all three are gone. Everyone is ranked on **Survival Points**
from champion 🏆 down to the wooden spoon 🥄.

It updates itself — a scheduled robot re-checks the scores every 15 minutes and
redeploys the site. No logins, no app to install: just open the link.

## How points work

| Event | Points |
|---|---|
| Win (any match) | +3 |
| Draw (any match) | +1 |
| Reach Round of 32 | +5 |
| Reach Round of 16 | +8 |
| Reach Quarter-final | +13 |
| Reach Semi-final | +21 |
| Reach Final | +34 |
| Win the World Cup 🏆 | +55 |

Reach bonuses are cumulative (you bank each as your team advances). Ties share a rank.
All values live in [`public/config.mjs`](public/config.mjs).

## Run it locally

```bash
node scripts/fetch.mjs   # pull the latest scores into public/data.json
npm run serve            # open http://localhost:4321
```

## How it works

- **Data**: ESPN's free, key-less soccer API (`fifa.world` scoreboard), swept across the
  whole tournament window by [`scripts/fetch.mjs`](scripts/fetch.mjs) → `public/data.json`.
- **Scoring**: [`public/scoring.mjs`](public/scoring.mjs) — pure functions, run in the
  browser so the maths is transparent and recalculates live.
- **Auto-update + hosting**: [GitHub Actions](.github/workflows/update.yml) re-fetches and
  redeploys to GitHub Pages every 15 minutes.

See [SPEC.md](SPEC.md) for the full design.

## The draw

16 players, 3 teams each — defined in [`public/config.mjs`](public/config.mjs).
