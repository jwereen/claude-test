# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository

Single-file browser game project hosted at https://github.com/jwereen/claude-test.

## Development

Open `pacman.html` directly in a browser — no build step, no dependencies, no server required.

## Architecture

`pacman.html` is a self-contained Pac-Man game in one HTML file:

- **Map** — `BASE_MAP` (21×21 grid): `0`=dot, `1`=wall, `2`=empty, `3`=power pellet, `4`=ghost house door. `initMap()` resets it each level.
- **Game loop** — `requestAnimationFrame`-driven; `update()` and `draw()` called every frame. Movement is gated by frame counters (`PAC_SPEED_DIV`, `GHOST_SPEED_DIV`) rather than delta time.
- **Pac-Man** — position in grid coordinates (floats). Queues the next direction in `nextDx/nextDy`; commits it only when the next cell is passable.
- **Ghosts** — 4 ghosts with individual `exitDelay` timers before leaving the ghost house. Frightened state uses random movement; normal state uses a 60% chance to move toward Pac-Man, otherwise random among valid non-reversing directions.
- **Collision** — checked after ghost movement each frame; frightened ghosts are eaten and respawned at their start positions.

## Git

All file changes are auto-committed via a PostToolUse hook (`Write|Edit` → `git add -A && git commit`). Push manually when ready:

```
git push
```
