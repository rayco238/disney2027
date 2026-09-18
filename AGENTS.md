# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project

Single-page static web app: a canvas animated countdown to a Disneyland Paris trip
(2027-11-14), targeting the Hotel Disney Newport Bay Club and Sleeping Beauty's Castle.
There is **no build step** — the entire app lives in `index.html`.

## Commands

- **Serve / test**: nothing to build. Run any static server, e.g. `python3 -m http.server 8080`, and open the page. `index.html` works directly from the filesystem (service worker and fonts are progressive enhancements).
- **No lint/typecheck/test framework** is configured. Keep the app dependency-free.

## Conventions

- **Single file**: put all markup, CSS, and JS inside `index.html`. Do not split into modules or add npm packages. No external libraries or CDNs — the only network call is the Open-Meteo weather API.
- **Language**: UI strings and comments are in **Spanish** (matching the audience). Code order/logic in English is fine, but keep user-facing strings Spanish.
- **JS style**: ES5-style `var`-based code, IIFE wrapper, `"use strict"`. No arrow functions in hot paths; keep the current style when editing.
- **Canvas**: design-space is 1600×900 (`DESIGN_W`/`DESIGN_H` ≈ 1600/900); resize applies `sceneScale`/`sceneOX`/`sceneOY`. Use proportional coordinates (`0.x*cw`, `0.x*ch`) rather than pixel constants.
- **Color palette**: use the `DAY_SKY_*`, `WALL`, `ROOF`, `GOLD`/`GOLD_GLOW`, `NIT_SKY_*` constants already declared; avoid hardcoded hexes unless intentional. Accent gold is `#ffd98a`.

## Key locations

- `applyMode()` — the environment simulation modes (auto/day/night/dusk/rain/snow/storm/wind).
- `drawScene()` — orchestrates the two scenes; `drawHotel()`/`drawCastleScene()` draw them.
- `codeInfo()` — maps Open-Meteo weather codes to scene states.
- `fetchWeather()` — Open-Meteo call; refresh interval set at the bottom of the script.
- `TARGET`, `LAT`, `LON` — trip date and location constants at the top of the `<script>`.
- `sw.js` — service worker (cache name `disney-2027-v1`); bump the `CACHE` constant when the shell assets change.

## Deploy

Repo: `git@github.com:rayco238/disney2027.git`, branch `main`, served as static content.