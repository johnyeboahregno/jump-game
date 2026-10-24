# Jump Game

A single-page, Super-Mario-style pixel-art platformer built with plain HTML5 Canvas — one HTML file, no build step.

## Controls
| Action | Keyboard | Touch |
| --- | --- | --- |
| Move | ← / → arrow keys | ◀ ▶ buttons |
| Jump | `J` | `J` button |
| Double-height jump | press `J` twice | tap `J` twice |
| Punch | `P` | `P` button |
| Join a player (down their coloured pipe) | `↓` (standing on it) | ▼ button |
| Leave the joined game | `X` | `X` button (appears while joined) |
| Pause | `Esc` | ⏸ button (top-left) |
| Music on/off | `M` | ♫ button (top-left) |
| Sound effects on/off | `S` | speaker button (top-left) |

Hop on/off crates, bonk `?` blocks for coins, smash bricks, stomp the purple Blorbs, and reach the flag.

## Warp pipes, joining & fighting
Every other player who's online gets their **own warp pipe** in your level — each in a different colour, with their
name above it. Stand on a coloured pipe and press **↓** to **join** that player: you pop out next to them, but you
**keep playing your own game on your own screen**. From then on you see them in your level and they see you in theirs
(in your pipe colour, with your name above you). Nothing happens unless you press ↓.
Press **`X`** to leave — either player can.

While you're joined you can **punch each other with `P`**. Each clean hit (not while the target is still
flashing from the last one) fills a red pip; **3 clean punches = K.O.** and the loser drops a life.

- The title screen shows how many players are online. Press `N` there to change your name.
- Want a private group instead of the global lobby? Everyone adds the same `?room=<anything>`,
  e.g. `https://jump-game-tan.vercel.app/?room=family`.
- The level has 6 pipes, so up to 6 other players can have a warp pipe at once; plain green pipes lead nowhere.
- How it works: players find each other through the free public MQTT relay `broker.emqx.io` (WebSockets). Once two players
  join, the two devices open a direct WebRTC data channel (STUN only) to stream each hero's position with low latency; if a direct
  connection isn't possible, everything falls back to the relay. Only game data (name, position, punches) is ever sent.

## Tech notes
- Fixed 120 Hz physics step with render interpolation — smooth on 60/120/144 Hz screens.
- All pixel art is generated once at startup into offscreen canvases; the level's tiles are cached in a single layer and only changed tiles are redrawn.
- Low-res (240px tall) canvas scaled up with `image-rendering: pixelated`.
- Tiny WebAudio synth for sound effects plus an original chiptune soundtrack, scheduled ahead on the audio clock for steady timing (speeds up when time runs low).

## Run locally
Open `index.html` in a browser.
