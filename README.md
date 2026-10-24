# Jump Game

A single-page, Super-Mario-style platformer built with plain HTML5 Canvas — no build step, no dependencies.

## Controls
| Action | Keyboard | Touch |
| --- | --- | --- |
| Move | ← / → arrow keys | ◀ ▶ buttons |
| Jump | `J` | `J` button |
| Double-height jump | press `J` twice | tap `J` twice |
| Pause | `P` / `Esc` | — |
| Mute music & sound | `M` | — |

Hop on/off crates, bonk `?` blocks for coins, smash bricks, stomp the purple Blorbs, and reach the flag.

## Network portals
Walk into a purple **PORTAL** and your hero jumps onto the screen of another player on the same network
(same Wi-Fi / same public IP). Your device becomes the controller: keep using your arrow keys/`J` (or touch
buttons) and your hero — pink cap, with your name above it — plays on their screen. Your score, coins and lives
travel with you. Jump into a portal over there (or run out of lives) to come home.

- Players on the same network find each other automatically; the title screen shows how many are online.
- Devices on different networks (e.g. a phone on cellular) can join the same group with `?room=<anything>`,
  e.g. `https://jump-game-tan.vercel.app/?room=family`.
- Press `N` on the title screen to change your player name.
- How it works: each device looks up its public IPv4 (via api.ipify.org), hashes it into a room id, and exchanges
  small JSON messages through the free public MQTT relay `broker.emqx.io` (WebSockets). The raw IP is never sent.
  The relay is public, so only game data (name, score, button presses) is ever sent.

## Tech notes
- Fixed 120 Hz physics step with render interpolation — smooth on 60/120/144 Hz screens.
- All pixel art is generated once at startup into offscreen canvases; the level's tiles are cached in a single layer and only changed tiles are redrawn.
- Low-res (240px tall) canvas scaled up with `image-rendering: pixelated`.
- Tiny WebAudio synth for sound effects plus an original chiptune soundtrack, scheduled ahead on the audio clock for steady timing (speeds up when time runs low).

## Run locally
Open `index.html` in a browser.
