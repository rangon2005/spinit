# Spinit — Multiplayer Couples Chat & Mini-Games

## Included project files
- `index.html` — frontend and multiplayer game logic
- `spinit-config.js` — Quick Match WebSocket endpoint configuration
- `chat-backgrounds/` — bundled chat wallpaper images
- `server/` — Node WebSocket matchmaking/relay service
- `MULTIPLAYER_AUDIT.md` — locally run test results and remaining deployment checks

## Games
- Truth or Dare — shared End option and restart flow
- Tic Tac Toe
- Snake Arena — food scoring and collision handling
- Rock Paper Scissors
- Guess the Color
- Basketball Duel — swipe/drag upward and release in the hoop; taps and misses do not score
- **broFight** — two-player street-fighting game with Topuski, Arduino, Rab, Ra.1 and Wa.fu; both players must Ready; host-validated HP/damage, distinct boost effects, block/punch/kick/movement/jump/crouch controls, and three rounds

## Fixes in this build
- Fixed the final upgrade installer guard: the patch now attaches to the actual `window.app` constructor. Previously the `window.SpinitApp` check could silently skip the final basketball/broFight/reliability patch.
- Hardened Quick Match relay sender identity; clients cannot supply another participant's `playerId` for relayed actions.
- Ludo actions now use the participant identity derived from the authenticated WebSocket instead of trusting `msg.playerId`.
- Quick Match requeue/recovery after unexpected socket close; allows a fresh pair instead of leaving the match screen stuck.
- Basketball score requires a valid upward swipe ending in the hoop; host validates and synchronizes the point.
- Darker chat background overlay and larger message, sender, composer and voice-player text.
- Truth or Dare End/restart flow shared with the room.
- Next button double-trigger/click-overlay safeguards.
- Voice recording MIME compatibility, pointer/touch press-release-cancel handling, inline playback and read-error handling.
- Snake food/score tick snapshot fix.

## Deployment
### Frontend
Deploy the project root containing `index.html`, `spinit-config.js`, and `chat-backgrounds/`.

### Quick Match server
Deploy `server/` as a Node Web Service using Node.js 20 or later. Run `npm install`, then `npm start`. Set `FRONTEND_ORIGIN` to the frontend origin if needed. Keep TURN credentials server-side. Update `spinit-config.js` if your server URL differs from the configured Render endpoint.

## Verification
See `MULTIPLAYER_AUDIT.md`. This build passed JavaScript syntax checks and a two-browser local simulation for Quick Match state pairing, broFight selection/Ready/movement sync, sender-identity enforcement, voice-message state delivery, basketball shot validation/scoring sync, and unexpected-close recovery.

**Limitations:** the browser relay was simulated locally, not run against the configured production Render service. Real microphone hardware/permissions and two physical phones were not exercised. Deploy the matching `server/` code together with this frontend, then perform a two-device smoke test.
