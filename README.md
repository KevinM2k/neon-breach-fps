# Neon Breach FPS

A browser-based first-person shooter built with vanilla JavaScript and HTML5 Canvas. No dependencies, no build step — open `index.html` and play.

Procedurally generated maps, escalating enemy waves, and a suite of pickups to find each run.

---

## Running

```bash
open index.html
# or serve locally:
python3 -m http.server 8080
```

---

## Controls

| Input | Action |
|---|---|
| `W A S D` | Move |
| `Shift` | Sprint |
| `Space` | Jump |
| `Right Click` | Aim / zoom |
| `Left Click` | Shoot |
| `P` / `Esc` | Pause |
| `M` | Toggle sound |
| `R` | Respawn (when dead) |

> Headshots deal bonus damage — aim for the visor.

---

## Weapons

| Weapon | Ammo | Body dmg | Head dmg | Notes |
|---|---|---|---|---|
| **Pistol** | Unlimited | 1 | 3 | Default |
| **Machine Gun** | 80 per pickup (max 160) | 0.5 | 1 | Hold to fire, wider spread |
| **Sniper** | 12 per pickup (max 24) | 2 | Instant kill | Extreme zoom when aimed |

Picking up a weapon you already carry adds ammo. Running dry reverts to pistol.

---

## Pickups

3–4 items spawn per map alongside 3 medkits.

| Item | Effect |
|---|---|
| **Medkit** | Fully restores HP. Respawns over time (rarer at high kill counts). |
| **Machine Gun** | Equips machine gun with 80 rounds |
| **Sniper** | Equips sniper rifle with 12 rounds |
| **Armour** | 25 shots at 30% incoming damage (blue screen border while active) |
| **Force Field** | 8 shots of complete damage immunity (purple screen border while active) |

Armour and Force Field stack — shield takes priority.

---

## Enemies

Enemies spawn in waves. Higher tiers unlock as your kill count rises.

| Tier | Name | HP | Accuracy | Fire rate | Reaction | Unlocks at |
|---|---|---|---|---|---|---|
| 1 | **Grunt** | 3 | Low | Slow | 3–5 s | Start |
| 2 | **Veteran** | 6 | Medium | Medium | 2–4 s | 3 kills |
| 3 | **Elite** | 10 | High | Fast | <1 s | 8 kills |

Enemies detect you by line of sight, wait out a reaction timer, then advance and shoot. Up to 10 active at once; spawn rate accelerates with kills.

---

## Features

- **Mission briefing screen** — menu shows controls, all field items with icons, and all three enemy types with stats before you start
- **Procedural maps** — randomised 10×10 grid each run, BFS-validated for connectivity
- **Neon lights** — 2–3 per map, cast coloured glow onto facing walls with flicker
- **Persistent high score** — saved to `localStorage`, shown on the death screen
- **Sound toggle** — preference saved across sessions
- **Raycasting renderer** — DDA algorithm (Wolfenstein-style), 800 rays/frame, distance fog, sprite depth sorting
