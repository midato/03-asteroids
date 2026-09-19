# AGENTS.md

Asteroids clone: single-file HTML5 Canvas game. No dependencies, no bundler, no test/build/lint tooling.

## Run / verify
- Open `index.html` directly in a browser, or `npx serve .` then visit `http://localhost:3000`.
- There is no automated verification. The only check is manual: load the page, watch for JS console errors, play briefly (any game state change: shooting, level completion, death, restart).

## Structure
- `game.js` — all game logic and rendering, loaded via `<script src="game.js">`. Do not split into modules; keep single-file.
- `index.html` — canvas element and inline CSS. Canvas attrs `width="800" height="600"` must stay in sync with the hardcoded `W`/`H` constants at the top of `game.js`. No bundler.

## Conventions
- Repo is in Spanish: README, HUD strings, and code comments are Spanish (e.g. `NIVEL`, `PUNTAJE`, `llama del propulsor`). Match this in new UI strings and comments.
- Entity classes (`Bullet`, `Asteroid`, `Ship`, `Particle`) own their `update(dt)` / `draw()` / `dead` flag; the global `update`/`draw` cycle filter dead objects each frame.
- Timestep: dt is clamped to 0.05s in the rAF loop.
- Object pools are plain arrays reassigned after filtering (e.g. `asteroids = asteroids.filter(...)`); keep this style.