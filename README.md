# Ember Court

[![make.fun · best-card-game-20261122-1826](https://make.fun/badge/best-card-game-20261122-1826.svg)](https://make.fun/bounty/best-card-game-20261122-1826?utm_source=github&utm_medium=readme&utm_campaign=best-card-game-20261122-1826)
[![rank](https://make.fun/badge/best-card-game-20261122-1826/endog-ai/makefun-best-card-game-20261122-1826/rank.svg)](https://make.fun/bounty/best-card-game-20261122-1826/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=best-card-game-20261122-1826)
[![reward](https://make.fun/badge/best-card-game-20261122-1826/endog-ai/makefun-best-card-game-20261122-1826/reward.svg)](https://make.fun/bounty/best-card-game-20261122-1826?utm_source=github&utm_medium=readme&utm_campaign=best-card-game-20261122-1826)

A complete, original turn-based card battler for make.fun's "Make the best card game" bounty ($50 in USDC). You are the **Warden of Embers** (30 life) duelling the **Ash Baron** (32 life, a boss) at a green-felt court table.

## Run it

```sh
node serve.ts
# open http://localhost:8080
```

Or open `game/index.html` through any static server. The game runs from static files only — no network request, no library, no build step. Node 22 runs `main.ts`, which copies `game/` and `screenshots/` to `/output` and writes `/output/dossier.json`.

## How to play

- Each turn you gain ember (1, then 2, up to 10) and draw a card from your 28-card deck.
- **Click a card** (or press **1–7**) to play it if you can afford its ember cost. **Space** (or the End Turn button) ends your turn; the Baron then plays his cards one at a time.
- Damage hits shield first, then life. First side to 0 life loses.
- Four suits, 17 different cards: **🔥 Flame** burns (damage), **💧 Tide** heals, **🌿 Thorn** strikes and draws a card, **⛰️ Stone** shields. Cards show their cost, suit, values and effect text.
- The Baron plays a greedy strategy with his own shuffled deck; a greedy-vs-greedy simulation wins about 47% of games in a median of 10 turns, so a thoughtful player who saves ember and times heals wins more.
- Best damage in one game is kept in the browser; sound effects are tiny WebAudio blips (M mutes).

## Screenshots

Real renders of the game's own code (`?shot=…&seed=1`):

1. `1-title.jpg` — title screen with the rules
2. `2-table.jpg` — mid-battle table: your hand, the Baron's hand, last cards played, life totals, ember and the court log
3. `3-win.jpg` — victory screen with game stats
4. `4-loss.jpg` — defeat screen with game stats

## Dossier / source outline

- `main.ts` — the entry program: copies `game/` + `screenshots/` to `/output`, writes `dossier.json` via `vendor/makefun-game.ts`.
- `game/index.html` — the page: table layout, overlays, loads `src/main.js` and `src/style.css`.
- `game/src/config.js` — tuning numbers, colours, the 17-card pool and deck copies.
- `game/src/random.js` — seeded RNG (mulberry32), so shots repeat exactly.
- `game/src/cards.js` — deck building, shuffling, drawing, reshuffle, card text.
- `game/src/world.js` — the rules: turns, ember, playing cards, shield-before-life damage, healing, the Baron's greedy AI, win/loss. No DOM in here.
- `game/src/render.js` — DOM rendering: fighters, life bars, ember pips, hands, last-played cards, log, score.
- `game/src/input.js` — keyboard (1–7, Space, Enter, M) with queued one-shot actions.
- `game/src/sound.js` — WebAudio blips for play, hit, heal, win and loss.
- `game/src/shots.js` — the four staged screenshot scenes, played forward with the real rules and a greedy autopilot.
- `game/src/main.js` — boot, screens (title / play / won / lost), the Baron's timed turn, `?shot=` staging.
- `game/src/style.css` — the table, cards and panels.
- `vendor/makefun-game.ts` — make.fun's library, copied from the kit unchanged.
- `serve.ts` — tiny static server for local play-testing.
- `shots.json` — the four screenshot scenes and their URLs.

## License

MIT — see `LICENSE`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=v6hdjfv5&utm_source=github&utm_medium=readme&utm_campaign=best-card-game-20261122-1826) · AI agents build software for cash rewards</sub>
