# CBB Live: shot volume and 3P scoreboard

A live NCAA D-I men's scoreboard. For every game it shows status, TV channel, score, the best available live spread
and over/under across US sportsbooks (with the book for each), and each team's
3-point shooting (3PM-3PA, 3PM and 3PA differences, 3P%, 3P% gap), shot volume (**FGA + FTA/2**) with the margin,
and points in the paint with the margin.

Color: only three columns are shaded, on a green scale: a lower 3P% margin, a higher shot-volume margin and a higher paint-point margin are greener.

**Flag:** a team is flagged when it is trailing in a live game and is green in all three shaded columns: its 3P% is
lower than its opponent's, its shot-volume margin is positive, and its paint-point margin is positive. Flags only
appear on live games.

Page: https://tannerstruth.github.io/cbb-live-3p-sv/

## Data
Scores, clock, TV and box stats come from ESPN's free public scoreboard (`groups=50` covers all of D-I).
It refreshes every 20 seconds while the tab is visible. Points in the paint are not on the scoreboard, so the page
also loads each live game's ESPN summary on every refresh (finals load once). Smaller games without ESPN
play-by-play may show no paint points. No API key is needed.

Filters: All / Live / Upcoming / Final, Flagged only, Ranked teams only, and a date picker for other days.

## Team fouls and bonus
On live games, **Fouls / This half** counts each team's fouls in the current half from ESPN's play-by-play (overtime
carries the 2nd-half count). **Bonus** is shown on the team that shoots: "Bonus" (1-and-1) once the opponent has 7
fouls in the half, "Double bonus" (two shots) at 10, otherwise "No". Games without ESPN play-by-play show "–". Every
foul ESPN logs counts, including technicals, so a rare administrative technical could make the count one high.

## Live odds (The Odds API)
Lines come from The Odds API (`basketball_ncaab`, `regions=us`, `markets=spreads,totals`, no moneyline). For each
team's spread the page shows the most points available (then the best price), plus the lowest Over and highest Under,
and names the book for each one. Until the Worker below is connected, ESPN's pregame line is shown instead.

**Credits:** one call is 2 credits and covers every game. Odds are only requested while a game on today's slate is
live and the tab is visible, every 2.5 minutes (`ODDS_MIN` near the top of `index.html`). That is about 48 credits per
live hour, or roughly 580 for a 12-hour Saturday. The Worker also makes at most one real call per 60 seconds, however
many tabs are open. Tiles show credits remaining/used (from the `x-requests-*` headers) and what this page spent today
and this session.

### One-time setup: Cloudflare Worker (about 5 minutes, free)
The Odds API key must not be in this public page, so a small Cloudflare Worker holds it.

1. Sign in at https://dash.cloudflare.com (the free plan is enough).
2. **Workers & Pages** → **Create** → **Create Worker** (Hello World). Name it e.g. `cbb-odds` and click **Deploy**.
3. **Edit code**: delete everything, paste in [`worker/odds-proxy.js`](worker/odds-proxy.js), click **Deploy**.
4. Worker → **Settings** → **Variables and Secrets** → **Add**: type **Secret**, name `ODDS_API_KEY`, value = your key. Deploy.
5. Copy the Worker URL (e.g. `https://cbb-odds.<your-subdomain>.workers.dev`) and set `WORKER_URL` near the top of
   `index.html` to it (or send it to Claude to do it).

The Worker only answers browser requests from `https://tannerstruth.github.io`. That doesn't stop someone with the URL
from calling it with a script, but the 60-second cache limits the cost, and you can rotate the key or delete the Worker anytime.
