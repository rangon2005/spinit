# Spinit — Multiplayer Couples Chat & Mini-Games

## Included project files
- `index.html` — frontend UI, game visuals and client-side game logic
- `spinit-config.js` — Quick Match WebSocket endpoint configuration
- `chat-backgrounds/` — bundled chat wallpaper images
- `server/` — Node WebSocket matchmaking/relay service
- `UPGRADE_NOTES.txt` — changes in this build
- `MULTIPLAYER_AUDIT.md` — focused checks and deployment-test limitations

## Games
- **Truth or Dare** — shared End and Play Again flow.
- **Tic Tac Toe** — the person who starts a game moves first; the Play Again requester gets the opening move of that replay.
- **Snake Arena** — Quick Match host `snakeDelta` packets are allowed through the WebSocket relay; one pointer/keyboard input path, one mobile D-pad, responsive canvas and a stale-packet snapshot request. Winner and loser hear different result sounds.
- **Rock Paper Scissors** — win/lose result sounds and share-result overlay.
- **Guess the Color** — a locked secret is hidden from non-owners/guessers in relayed state snapshots.
- **Basketball Duel** — 3D-style court, backboard, rim/net and rotating ball arc; only a validated upward swipe released in the hoop scores.
- **broFight** — two-player cartoon street fighter with Topuski, Arduino, Rab, Ra.1 and Wa.fu. Select-and-lock hero, both players Ready, three rounds, compact controls inside the arena, human-like character silhouettes, unique character boost moves and damage levels, and a 1.5-second block window that cancels incoming boost damage.

## broFight boost abilities
| Hero | Ability | Damage |
|---|---|---:|
| Topuski | Groundquake Belly Slam | 27 |
| Arduino | Electric Clap | 21 |
| Rab | Hulk Power Punch | 39 |
| Ra.1 | Fire Hammer Throw & Return | 32 |
| Wa.fu | Sword Throw & Return | 26 |

Boost damage is host-authoritative and resolves after the 1.5-second block window. If the defender's block action reaches the host before resolution, the boost deals zero damage. Move animations are kept active during the pending window.

## Other updates
- Darker chat-wallpaper overlay and larger chat/sender/composer/voice-player text.
- Next-button double-trigger/click-overlay safeguards.
- Voice recording MIME compatibility, pointer/touch press-release-cancel handling, inline playback and read-error handling.
- Game-end result overlay with Share Result Card, Save Image and a larger close button.
- Quick Match reconnect/requeue handling and host-authoritative game actions.
- Relay sender identity comes from the paired WebSocket, not a browser-supplied `playerId`.

## Deploy
### Frontend
Deploy the project root containing `index.html`, `spinit-config.js`, and `chat-backgrounds/`.

### Quick Match server
Deploy `server/` as a Node Web Service using Node.js 20 or later. Run `npm install`, then `npm start`. Set `FRONTEND_ORIGIN` to the frontend origin if needed. Keep TURN credentials server-side. Update `spinit-config.js` if your server URL differs from the configured endpoint.

## Verification
This build's inline JavaScript, server JavaScript, key Snake relay check and focused broFight boost/block-window regression tests pass. The tests are not a substitute for deployment verification: the production WebSocket endpoint and two physical devices with touch input/microphone were not exercised in this environment. Deploy the frontend and matching `server/` together, then run the two-device checklist in `MULTIPLAYER_AUDIT.md`.
