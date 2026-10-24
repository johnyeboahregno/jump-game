# Jump Game

A single-page, Super-Mario-style platformer with an N64-style ("64-bit") 2.5D low-poly look — one HTML file, no build step.
Rendered with three.js (WebGL); falls back to the original pixel-art Canvas renderer if WebGL isn't available.

## Controls
| Action | Keyboard | Touch |
| --- | --- | --- |
| Move | ← / → arrow keys | ◀ ▶ buttons |
| Jump | `J` | `J` button |
| Double-height jump | press `J` twice | tap `J` twice |
| Punch | `P` | `P` button |
| Pause | `Esc` | ⏸ button (top-left) |
| Music on/off | `M` | ♫ button (top-left) |
| Sound effects on/off | `S` | speaker button (top-left) |

Hop on/off crates, bonk `?` blocks for coins, smash bricks, stomp the purple Blorbs, and reach the flag.

## Network portals, ghosts & fighting
Walk into a purple **PORTAL** and your hero jumps onto the screen of another player who is online — anyone playing
the game, anywhere. Your device becomes the controller and shows a **ghost** of your hero mirroring what it's doing
on their screen. Your score, coins and lives travel with you. Jump into a portal over there (or run out of lives)
to come home.

While you're on someone's screen you can **punch each other with `P`**. Each clean hit (not while the target is still
flashing from the last one) fills a red pip; **3 clean punches = K.O.** and the loser drops a life.

- The title screen shows how many players are online. Press `N` there to change your name.
- Want a private group instead of the global lobby? Everyone adds the same `?room=<anything>`,
  e.g. `https://jump-game-tan.vercel.app/?room=family`.
- How it works: players find each other through the free public MQTT relay `broker.emqx.io` (WebSockets). Once a hero
  ports, the two devices open a direct WebRTC data channel (STUN only) for low-latency inputs and poses; if a direct
  connection isn't possible, everything falls back to the relay. Only game data (name, score, button presses,
  positions) is ever sent.

## Tech notes
- Fixed 120 Hz physics step with render interpolation — smooth on 60/120/144 Hz screens.
- 3D: instanced meshes for all tiles (one draw call per block type), soft shadows, fog, low-poly flat-shaded scenery;
  64×64 textures generated from the pixel tiles at startup.
- All pixel art is generated once at startup into offscreen canvases; the level's tiles are cached in a single layer and only changed tiles are redrawn.
- Low-res (240px tall) canvas scaled up with `image-rendering: pixelated`.
- Tiny WebAudio synth for sound effects plus an original chiptune soundtrack, scheduled ahead on the audio clock for steady timing (speeds up when time runs low).

## Run locally
Open `index.html` in a browser.
