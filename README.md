# Spinit — Multiplayer Couples Chat & Mini-Games

## Included project files
- `index.html` — frontend UI and client-side multiplayer/game logic
- `spinit-config.js` — Quick Match WebSocket endpoint configuration
- `chat-backgrounds/` — bundled chat wallpaper images
- `server/` — Node WebSocket matchmaking/relay service
- `UPGRADE_NOTES.txt` — changes in this build
- `MULTIPLAYER_AUDIT.md` — focused checks and deployment-test limitations

## Games
- Truth or Dare — shared End and Play Again flow
- Tic Tac Toe — the person who starts a game moves first; the player who clicks Play Again gets the first move in the replay
- Snake Arena — food/score fix, responsive mobile canvas and on-screen touch directions
- Rock Paper Scissors
- Guess the Color — a locked color is hidden from non-owners/guessers in relayed state snapshots
- Basketball Duel — layered 3D-style court, backboard, rim/net and rotating ball arc; only a validated upward swipe released in the hoop scores
- **broFight** — two-player cartoon street fighter with Topuski, Arduino, Rab, Ra.1 and Wa.fu; kung-fu-like punch/kick/jump/block animations, three rounds, shared Ready flow, character selection locks once picked, equal boost damage/power for each character, distinct visual effects and mobile/keyboard controls

## Other updates
- Darker chat wallpaper veil and larger chat, sender, composer and voice-player text
- Truth or Dare End/Play Again state shared across the room
- Next button double-trigger/click-overlay safeguards
- Voice recording MIME compatibility, pointer/touch press-release-cancel handling, inline playback and read-error handling
- Result overlay at game end with Share Result Card and Save Image actions
- Quick Match reconnect/requeue improvements and host-authoritative game actions
- Sender identity enforcement in the relay server; client-supplied player IDs are not trusted for forwarded actions

## Deploy
### Frontend
Deploy the project root containing `index.html`, `spinit-config.js`, and `chat-backgrounds/`.

### Quick Match server
Deploy `server/` as a Node Web Service using Node.js 20 or later. Run `npm install`, then `npm start`. Set `FRONTEND_ORIGIN` to the frontend origin if needed. Keep TURN credentials server-side. Update `spinit-config.js` if your server URL differs from the configured endpoint.

## Verification notes
The latest feature build passed syntax checks for all 9 inline JavaScript blocks and `server/server.js`; focused regression tests passed for basket-shot validation, Tic Tac Toe starter selection, color-secret sanitization, equal broFight power, mobile Snake layout, and result-card integration. CSS blocks were parsed with no syntax errors. The existing multiplayer base was previously tested with a two-browser mocked relay, but a full browser run against the production WebSocket endpoint and physical-device/mobile touch/microphone tests have **not** been completed for this latest visual/privacy patch. Deploy the frontend and matching `server/` together, then test from two separate browsers/devices.
