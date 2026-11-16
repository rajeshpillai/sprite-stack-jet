# Sprite-Stack Jet

A pixel-art jet flying over stacked islands, from the wavetops up to space. It's built with **plain Canvas 2D**: no WebGL, no 3D engine, no polygons.

## Run it
Open `index.html` in a browser. There's nothing to install or build.

## Controls
| Input | Action |
|---|---|
| Pointer | Overhead: the jet turns toward the pointer. Cockpit: left/right turns, up/down climbs and dives |
| A, D / W, S | Turn / climb and dive |
| Click / R | Barrel roll |
| Hold click / Shift | Fire the thrusters |
| Space / C | Switch between overhead and cockpit views |

## How it works
1. **Sprite stacking.** The jet, terrain, trees and clouds are piles of 2D pixel layers, each drawn one pixel higher than the last. The overhead camera never rotates, so terraces, trees and clouds are *baked* into bitmaps once. Only the jet, which turns and rolls, is stacked live every frame.
2. **Fake perspective.** Anything at height `h` is scaled by `s = F / (F + altitude − h)`. The ground shrinks as you climb, while the jet always stays at `s = 1`.
3. **Mode 7 floor.** In the cockpit view, each screen row below the horizon maps to a ground distance `d = camHeight × focal / (row − horizon)`, and the world texture is sampled along that row.
4. **Fake roll.** Each layer is narrowed by `cos(roll)` and pushed sideways by `sin(roll) × (layer − centre)`.

The cockpit, HUD and instruments are plain rects and arcs, with a 3×5 pixel font. Everything is drawn at 320 px tall and scaled up with `image-rendering: pixelated`.
