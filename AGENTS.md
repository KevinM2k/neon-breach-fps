# Repository Guidelines

## Project Structure & Module Organization
This repository is intentionally minimal. [`index.html`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/index.html) contains the full game: HTML shell, CSS, and all JavaScript systems. [`README.md`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/README.md) is the player-facing overview; [`CLAUDE.md`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/CLAUDE.md) and [`GEMINI.md`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/GEMINI.md) document architecture for coding agents. There is no `src/`, `tests/`, or asset pipeline. New visuals and sounds should stay procedural unless the project structure changes intentionally.

## Build, Test, and Development Commands
There is no build step or dependency install.

```bash
open index.html
python3 -m http.server 8080
```

Use `open index.html` for quick local playtesting. Use `python3 -m http.server 8080` when browser security or pointer-lock behavior is more reliable over `http://localhost:8080`. If you add tooling later, keep commands lightweight and document them in [`README.md`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/README.md).

## Coding Style & Naming Conventions
Match the existing style in [`index.html`](/Users/kevin/code/github/kevinm2k/neon-breach-fps/index.html): 4-space indentation, semicolons, and descriptive camelCase names such as `applyNewMap`, `spawnEnemy`, and `playGunshot`. Use `const` by default and `let` only for mutable state. Keep related systems grouped in file order: constants/state, map generation, audio, input, AI, rendering, loop. Avoid adding frameworks, bundlers, or external assets without explicit justification.

## Testing Guidelines
Automated tests are not set up in this repository. Validate changes manually in a modern browser and check the main gameplay paths: menu flow, pointer lock, movement, combat, pickups, pause, death/respawn, and `localStorage`-backed high score and sound settings. For regressions, include the exact scenario you tested in your PR description.

## Commit & Pull Request Guidelines
Recent history uses short, imperative commit subjects such as `Add items/pickups, fix enemies...` and `Progress`. Prefer clearer one-line summaries like `Tune elite spawn timing` or `Fix pause button state`. Keep each commit focused. PRs should describe gameplay impact, list manual test coverage, link any related issue, and include screenshots or a short recording for visible UI or rendering changes.

## Contributor Constraints
Preserve the no-dependency, single-file approach unless the change explicitly restructures the project. Favor procedural generation over checked-in media, and keep rendering and update loops performant enough for smooth browser play.
