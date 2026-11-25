# CBB Live: shot volume and 3P scoreboard

A live NCAA D-I men's scoreboard. For every game it shows status, TV channel, score, and each team's
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
