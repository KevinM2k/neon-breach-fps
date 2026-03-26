# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

No build step required. Open `index.html` directly in any modern browser:

```bash
open index.html
# or serve locally:
python3 -m http.server 8080
```

## Architecture

The entire game is a single self-contained file: `index.html` (~785 lines). No external dependencies, frameworks, or asset files.

**Tech stack:** Vanilla JS (ES6), HTML5 Canvas 2D, Web Audio API, Pointer Lock API.

### Key Systems (by line range)

- **Map/constants** (~1–90): 10×10 grid map (1=wall, 0=open), game constants
- **Audio** (~114–187): Procedural synthesis via Web Audio — no audio files; `playGunshot()`, `playHeartbeat()`, `playMedkit()`
- **Player state** (~200–301): Position (x,y,z), view angle/pitch, velocity, jump, aim/scope state
- **Enemy AI** (~349–398): Spawn system, line-of-sight detection, reaction timer, pathfinding, firing accuracy
- **Raycasting renderer** (~435–774): DDA algorithm, 800 rays/frame, sprite rendering (enemies, medkits), scope overlay, visual effects
- **Game loop** (~776–782): `requestAnimationFrame` driving `update()` + `draw()`

### Raycasting Renderer

Uses DDA (Digital Differential Analyzer) raycasting — same technique as Wolfenstein 3D. Wall height is computed from perpendicular ray distance. Sprites (enemies, medkits) are sorted by distance and drawn after walls. Distance fog is applied via brightness scaling.

### Enemy AI

Enemies have 3 HP. Up to 10 active at once, with spawn rate accelerating with kill count. They detect the player via line-of-sight raycasting, wait 3–5 seconds before shooting, and advance toward the player when visible. Shot accuracy degrades with distance.

### Combat

Cone-based hit detection with spread: 8px zoomed, 60px hip-fire. Only the nearest enemy in the cone is hit per shot. Player health: 100 HP; enemy shots deal 1–12 damage based on distance. Three medkits restore full health. Press R to respawn after death.

### Canvas Layout

Fixed 1600×800 canvas. FOV: 60° default, 9° when scoped (right-click to aim). Player z-axis enables jumping.
