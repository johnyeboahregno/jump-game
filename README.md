# Jump Game

A single-page, Super-Mario-style platformer built with plain HTML5 Canvas — no build step, no dependencies.

## Controls
| Action | Keyboard | Touch |
| --- | --- | --- |
| Move | ← / → arrow keys | ◀ ▶ buttons |
| Jump | `J` | `J` button |
| Double-height jump | press `J` twice | tap `J` twice |
| Pause | `P` / `Esc` | — |
| Mute | `M` | — |

Hop on/off crates, bonk `?` blocks for coins, smash bricks, stomp the purple Blorbs, and reach the flag.

## Tech notes
- Fixed 120 Hz physics step with render interpolation — smooth on 60/120/144 Hz screens.
- All pixel art is generated once at startup into offscreen canvases; the level's tiles are cached in a single layer and only changed tiles are redrawn.
- Low-res (240px tall) canvas scaled up with `image-rendering: pixelated`.
- Tiny WebAudio synth for sound effects.

## Run locally
Open `index.html` in a browser.
