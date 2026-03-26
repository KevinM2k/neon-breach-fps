# GEMINI.md - Neon Breach FPS

This file provides architectural context and development guidelines for the Neon Breach FPS project.

## Project Overview
Neon Breach FPS is a self-contained, browser-based first-person shooter built with vanilla JavaScript and HTML5 Canvas. It uses a custom raycasting renderer (DDA algorithm) similar to Wolfenstein 3D to create a 3D effect on a 2D canvas.

- **Main Technologies**: Vanilla JS (ES6+), HTML5 Canvas 2D, Web Audio API, Pointer Lock API.
- **Architecture**: Single-file application (`index.html`). No external dependencies, build steps, or asset files.
- **Key Features**: Procedural map generation, escalating enemy waves, multiple weapons (Pistol, MG, Sniper), and procedural sound synthesis.

## Building and Running
No build process is required.

- **To Play**: Open `index.html` directly in a modern web browser.
- **To Serve Locally**: 
  ```bash
  python3 -m http.server 8080
  ```
  Then navigate to `http://localhost:8080`.

## Development Conventions

### Single-File Structure
The entire game logic, styling, and markup are contained within `index.html`.
- **CSS**: Located in the `<style>` block in `<head>`.
- **Game Logic**: Located in the `<script>` block.
- **Assets**: All visual and audio assets are generated programmatically. No external images or sounds should be added.

### Code Organization (Within index.html)
The code follows a roughly sequential order:
1.  **State & Constants**: Game settings, player state, and map variables.
2.  **Map Generation**: `applyNewMap()` handles procedural 10x10 grid generation and BFS connectivity validation.
3.  **Audio System**: Procedural synthesis using the Web Audio API.
4.  **Input Handling**: Pointer Lock API for mouse look, event listeners for keyboard/mouse.
5.  **Enemy AI**: Line-of-sight detection and basic state machine for Grunt, Veteran, and Elite tiers.
6.  **Raycasting Renderer**: Core DDA loop, distance fog, sprite depth sorting, and UI overlays.
7.  **Game Loop**: `update()` and `draw()` functions driven by `requestAnimationFrame`.

### Renderer Details
- **Canvas Size**: Fixed at 1600x800.
- **Raycasting**: 800 rays per frame (one per two horizontal pixels for performance).
- **Sprites**: Enemies and pickups are rendered as billboards, sorted by distance to the player to ensure correct occlusion.

### Contribution Guidelines
- **No Dependencies**: Do not introduce external libraries or frameworks.
- **Performance**: Maintain 60 FPS. Optimize raycasting and sprite sorting loops if adding features.
- **Proceduralism**: New features (textures, sounds, maps) should be generated via code rather than static files.
