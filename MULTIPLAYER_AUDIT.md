# Spinit Multiplayer Audit — 14 October 2026

## Fixes applied
1. Replaced the final installer lookup `window.SpinitApp?.prototype` with `window.app?.constructor?.prototype`. This was a real runtime issue: the app class is not guaranteed to be exposed as a `window` property, so the final basketball/broFight/reliability patch could silently return before installing.
2. Match relay rewrites a client action's `playerId` using the server-known participant associated with its WebSocket.
3. Ludo actions also derive the player ID from the paired WebSocket. A forged `msg.playerId` is ignored.
4. Unexpected Quick Match socket loss uses the recovery/requeue path.

## Automated checks run
- All 8 inline JavaScript blocks: `node --check` pass.
- `server/server.js`: `node --check` pass.
- Local two-page Chromium simulation using a mocked matchmaking WebSocket relay:
  - Both browsers matched and received the same two-player state.
  - broFight state appeared on both browsers; character selection and both-player Ready synced.
  - Client action with a forged host `playerId` moved only the authenticated client's fighter; host fighter remained unchanged.
  - Synthetic voice-message packet/state appeared in both clients.
  - Basketball tap and miss did not score; a valid upward swipe did score and synced to the opponent.
  - Simulated unexpected socket close sent both browsers back to matchmaking and they paired again.
  - Browser `pageerror` collection: empty.

## What was not verified here
- The actual Node WebSocket server was not launched for end-to-end tests in this environment because the `ws` dependency could not be installed during this run.
- The configured production Render WebSocket endpoint was not tested from real client devices.
- Microphone permission/physical audio recording, real mobile touch latency, and real-device animation performance were not exercised.

For deployment, deploy this frontend and the matching `server/` directory together. Then open the site in two separate devices/browser profiles, pair them, exchange a voice message, play broFight and Basketball Duel, and test Next/reconnect.
