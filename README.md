# Sprite-Stack Jet

A pixel-art jet flying over stacked islands, from the wavetops up to space. It's built with **plain Canvas 2D**: no WebGL, no 3D engine, no polygons.

## Run it
Open `index.html` in a browser. There's nothing to install or build.

## Controls
| Input | Action |
|---|---|
| Pointer / A, D | Steer |
| Click / R | Barrel roll |
| Hold click / Space | Thrust and climb |
| C | Switch between chase and cockpit views |

## How it works
1. **Sprite stacking.** The jet and the islands are piles of 2D pixel layers. Each layer is drawn turned by the same angle and shifted up a pixel, so the pile reads as a 3D voxel model.
2. **Fake perspective.** Anything at height `h` is scaled by `s = F / (F + altitude − h)`. The ground shrinks as you climb, while the jet always stays at `s = 1`.
3. **Mode 7 floor.** In the cockpit view, each screen row below the horizon maps to a ground distance `d = camHeight × focal / (row − horizon)`, and the world texture is sampled along that row.
4. **Fake roll.** Each layer is narrowed by `cos(roll)` and pushed sideways by `sin(roll) × (layer − centre)`.

Everything is drawn at 384×216 and scaled up with `image-rendering: pixelated`.
