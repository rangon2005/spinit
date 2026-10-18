# Spinit — Multiplayer Couples Chat & Mini-Games

## Project files
- `index.html` — frontend UI, mini-games and client logic
- `spinit-config.js` — Quick Match WebSocket endpoint configuration
- `chat-backgrounds/` — bundled chat wallpapers
- `server/` — Node WebSocket matchmaking/relay service
- `UPGRADE_NOTES.txt` — changes in this build
- `MULTIPLAYER_AUDIT.md` — focused checks and deployment-test limitations

## Games
- **Truth or Dare** — End and Play Again flow.
- **Tic Tac Toe** — starter rules for game start/rematch.
- **Snake Arena** — keyboard/pointer input consolidation, single responsive mobile D-pad, responsive canvas, food growth/food sync fix, correct `snakeDelta` relay, new-round state reset and winner/loser result sounds.
- **Rock Paper Scissors** — win/lose result sounds and share-result overlay.
- **Guess the Color** — a locked secret is hidden from non-owners/guessers in relayed snapshots.
- **Basketball Duel** — 3D-style court, backboard, rim/net and rotating ball arc; only a validated upward swipe released in the hoop scores.
- **broFight** — two-player cartoon fighter with five custom SVG human-like hero sprites, selectable/locked heroes, compact in-arena controls, three-round matches, unique boost powers, and a 1.5-second block window.
- **Game end/restart** — common End handling clears stale game snapshots and timers, including Ludo; a new launch creates a fresh match state.

## broFight abilities
| Hero | Ability | Damage |
|---|---|---:|
| Topuski | Groundquake Belly Slam | 27 |
| Arduino | Electric Clap | 21 |
| Rab | Hulk Power Punch | 39 |
| Ra.1 | Fire Hammer Throw & Return | 32 |
| Wa.fu | Sword Throw & Return | 26 |

## Deploy
Deploy the frontend root (`index.html`, `spinit-config.js`, `chat-backgrounds/`) and matching `server/` together. Run the Node server with `npm install` and `npm start` on Node.js 20+. Adjust `spinit-config.js` if the production endpoint differs.

## Validation
JavaScript syntax checks and focused unit/regression checks pass in this build. A complete headless browser smoke test did not finish in this environment, and physical-device/production-WebSocket checks were not run. See `MULTIPLAYER_AUDIT.md` for the checklist and limits.
