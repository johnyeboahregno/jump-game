# Jump Game

A single-page, Super-Mario-style pixel-art platformer built with plain HTML5 Canvas — one HTML file, no build step.

## Controls
| Action | Keyboard | Touch |
| --- | --- | --- |
| Move | ← / → arrow keys | ◀ ▶ buttons |
| Jump | `J` | `J` button |
| Double-height jump | press `J` twice | tap `J` twice |
| Punch | `P` | `P` button |
| Warp down a coloured pipe | `↓` (standing on it) | ▼ button |
| Come back home | `X` | `X` button (appears while away) |
| Pause | `Esc` | ⏸ button (top-left) |
| Music on/off | `M` | ♫ button (top-left) |
| Sound effects on/off | `S` | speaker button (top-left) |

Hop on/off crates, bonk `?` blocks for coins, smash bricks, stomp the purple Blorbs, and reach the flag.

## Warp pipes, ghosts & fighting
Every other player who's online gets their **own warp pipe** in your level — each in a different colour, with their
name above it. Stand on a coloured pipe and press **↓** to sink into it and pop out of a pipe on **that player's**
screen (wearing your pipe colour). Nothing happens unless you press ↓. Your device becomes the controller and shows a
**ghost** of your hero mirroring what it's doing over there. Your score, coins and lives travel with you.
Press **`X`** any time to come back home — you rise out of the pipe you left from (running out of lives also sends you home).

While you're on someone's screen you can **punch each other with `P`**. Each clean hit (not while the target is still
flashing from the last one) fills a red pip; **3 clean punches = K.O.** and the loser drops a life.

- The title screen shows how many players are online. Press `N` there to change your name.
- Want a private group instead of the global lobby? Everyone adds the same `?room=<anything>`,
  e.g. `https://jump-game-tan.vercel.app/?room=family`.
- The level has 6 pipes, so up to 6 other players can have a warp pipe at once; plain green pipes lead nowhere.
- How it works: players find each other through the free public MQTT relay `broker.emqx.io` (WebSockets). Once a hero
  warps, the two devices open a direct WebRTC data channel (STUN only) for low-latency inputs and poses; if a direct
  connection isn't possible, everything falls back to the relay. Only game data (name, score, button presses,
  positions) is ever sent.

## Tech notes
- Fixed 120 Hz physics step with render interpolation — smooth on 60/120/144 Hz screens.
- All pixel art is generated once at startup into offscreen canvases; the level's tiles are cached in a single layer and only changed tiles are redrawn.
- Low-res (240px tall) canvas scaled up with `image-rendering: pixelated`.
- Tiny WebAudio synth for sound effects plus an original chiptune soundtrack, scheduled ahead on the audio clock for steady timing (speeds up when time runs low).

## Run locally
Open `index.html` in a browser.
