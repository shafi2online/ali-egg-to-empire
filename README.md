# Ali — Egg to Empire

A mobile-first 2D farming game. Start with one hen, collect and sell eggs, grow a flock, expand the coop, buy land and build Ali’s first home.

This is the first playable proof of concept. It is single-player; the city, kingdom and multiplayer systems discussed for future chapters are not implemented.

![First playable chapter, after building Ali’s first home](docs/preview.jpg)

## Play locally

Serve `dist/` with a static HTTP server. Python example:

```sh
python -m http.server 8080 --directory dist
```

Open `http://localhost:8080`. Opening `index.html` directly as a `file://` URL will not load JavaScript modules correctly.

No dependency installation or production build is required. Phaser 3.90.0 is bundled locally, so runtime code does not depend on a CDN.

## Controls

- Tap the coop or **Collect eggs** to move ready eggs into your basket.
- Tap the market or **Sell at market** to exchange the basket for fictional coins.
- Buy hens in **Farm shop**. Four hens unlock the coop expansion.
- Expand the coop, then use **Build & expand** to buy land and build a home.
- Follow the current goal for a guided path. Some milestones award bonus coins.
- Feeding is optional: a 30-second production boost, with no hunger or starvation mechanics.
- Sound is off initially and can be enabled. Reset requires confirmation.

## Saves

Progress is stored in this browser’s local storage under `ali-egg-to-empire-save-v1`. Sound preferences use `ali-sound`. There is no account, cloud sync, real-money balance or server.

Production while away is limited to four hours and the coop’s egg capacity. Clearing browser data removes the farm. The UI warns when local storage is unavailable. Browser saves can be edited by players; this client-only prototype is not suitable for competitive multiplayer economics.

## Source map

| File | Purpose |
| --- | --- |
| `dist/index.html` | Accessible interface, dialogs and page structure |
| `dist/styles.css` | Responsive presentation |
| `dist/app.js` | UI bindings, sound feedback and saves across visibility changes |
| `dist/game-state.js` | Game economy, progression, validation and persistence |
| `dist/world.js` | Phaser scene, original procedural world art and animations |
| `dist/assets/ali-concept.png` | Approved Ali character concept |
| `dist/assets/ali-sprite.png` | Ali character sprite derived from the approved concept |
| `dist/assets/phaser.min.js` | Locally bundled Phaser 3.90.0 |
| `tests/game-state.test.mjs` | Deterministic economy and persistence tests |

## Tests

Use Node.js 18 or newer:

```sh
npm test
```

Tests cover resource conservation, purchase prerequisites, time accounting, production boosts, milestone rewards, valid/corrupt saves and reset. The main economy simulation reaches the first home in roughly five minutes of active play; actual timing depends on player choices.

## Hosting

Deploy the contents of `dist/` to a static host. All application paths are relative, including the Phaser character asset, so the game can also be hosted under a subdirectory. The `.openai/hosting.json` manifest identifies the current Sites deployment and must not be reused as a new Site identity.

For competitive multiplayer later, move ownership, currency, production and battle results to an authoritative server before trusting any client state. ASP.NET can serve that role without changing the browser renderer.

## Credits

Ali artwork was generated for this project using the approved character reference. The world graphics and interface were created for this proof of concept. Phaser is third-party software under its MIT license; see `dist/assets/PHASER-LICENSE.md`.
