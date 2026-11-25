# CBB Live: shot volume and 3P scoreboard

A live NCAA D-I men's scoreboard. For every game it shows status, TV channel, score, and each team's
3-point shooting (3PM-3PA, 3PM and 3PA differences, 3P%, 3P% gap), shot volume (**FGA + FTA/2**) with the margin,
and points in the paint with the margin.

Color: only three columns are shaded, on a green scale: a lower 3P% margin, a higher shot-volume margin and a higher paint-point margin are greener.

**Flag:** a team is flagged when it is trailing in a live game even though it has a shot-volume edge of
at least 5 and a 3P% deficit of at least 10 points (both teams have at least 5 3PA). The thresholds are in **Settings**.

Page: https://tannerstruth.github.io/cbb-live-3p-sv/

## Data
Scores, clock, TV and box stats come from ESPN's free public scoreboard (`groups=50` covers all of D-I).
It refreshes every 20 seconds while the tab is visible, and you can change that in Settings. Points in the paint
are not on the scoreboard, so the page also loads each live game's ESPN summary on every refresh (finals load once).
Smaller games without ESPN play-by-play may show no paint points. No API key is needed.

Filters: All / Live / Upcoming / Final, Flagged only, Ranked teams only, and a date picker for other days.
