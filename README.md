# CBB Live: shot volume and 3P scoreboard

A live NCAA D-I men's scoreboard. For every game it shows status, TV channel, score, and each team's
3-point shooting (3PM-3PA, 3P%, 3P% gap) and shot volume (**FGA + FTA/2**) with the margin.

**Flag:** a team is flagged when it is trailing in a live game even though it has a shot-volume edge of
at least 5 and a 3P% deficit of at least 10 points (both teams have at least 5 3PA). The thresholds are in **Settings**.

Page: https://tannerstruth.github.io/cbb-live-3p-sv/

## Data
Scores, clock, TV and box stats come from ESPN's free public scoreboard (`groups=50` covers all of D-I).
It refreshes every 20 seconds while the tab is visible, and you can change that in Settings. If the scoreboard
is missing box stats for a game, the page falls back to that game's ESPN summary. No API key is needed.

Filters: All / Live / Upcoming / Final, Flagged only, Ranked teams only, and a date picker for other days.
