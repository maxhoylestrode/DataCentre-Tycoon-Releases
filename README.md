# Datacentre Tycoon

Build and run your own datacentre. Start with an empty room and a bit of cash, then lay out racks, power, cooling and networking, sign customers, hire staff and keep everything from catching fire.

**Play it in the browser:** [tycoon.apexstudio.dev](https://tycoon.apexstudio.dev)
**Desktop app:** Windows, macOS and Linux installers are published from the [releases repository](https://github.com/maxhoylestrode/datacentre-tycoon-releases).

![The All racks panel over the live datacentre floor](overhaul-screenshots/curated/phase5/1920x1080-30-panel-racks.jpg)

---

## What it is

Datacentre Tycoon mixes three kinds of game:

- **Management sim.** Grid placement, staff, incidents and a floor you have to plan around. Think RollerCoaster Tycoon, but for server halls.
- **Business and logistics.** Buy hardware, take contracts, manage power and bandwidth supply, and deal with a market that moves under you and rivals who want your customers.
- **Real IT concepts.** Racks, PDUs, aisles, cooling, uptime, SLAs, certifications and custom silicon. You learn some of how a datacentre actually works without needing to know it first.

Racks earn money. Everything else exists to keep them running, cool, powered and online.

## Features

- **Racks and power.** Place racks, add power units and PDUs, and watch the power bar. Racks draw more than you have and you'll have brownouts.
- **Heat and cooling.** Racks throw off heat. Use aisles, chillers and cooling units to stop things running hot. A heat map overlay shows where the trouble is.
- **Customers and contracts.** Clients sign contracts with uptime and bandwidth requirements. Meet them and you get paid. Miss them and you pay for it.
- **Internet.** Your uplink has a ceiling. Upgrade it, or hit it with a streaming surge and watch the network bar fill.
- **Staff.** Hire engineers to build and repair. They walk the floor, so a rack behind a locked-off corridor is a rack nobody can reach.
- **Incidents.** Failures happen: power trips, cooling faults, cyber attacks, ransomware. Good planning softens them. Bad planning bankrupts you.
- **Custom silicon.** Design your own chips in a 3D die editor, pick a cooler (air, liquid or immersion), tape out and roll them into your racks.
- **Trade-ups and upgrades.** Move racks up to bigger classes, swap in better parts, and bulk-upgrade a whole fleet with a preview of what it costs.
- **Research.** A tech tree that unlocks new hardware, packaging and building options.
- **Rooms and decor.** Floors, walls, lighting and decor sets that count towards prestige.
- **Compliance and certifications.** ISO 27001, SOC 2, green energy and Uptime Tier III and IV. Many contracts ask for them.
- **Rivals.** Competitors fight you for market share, measured by capacity and quality.
- **Achievements, goals and levels.** Goals give XP and cash, XP unlocks new things, and levels take you from a server closet to a global network.
- **Scenarios.** Separate games with their own twists (a server closet with no room to expand, desert heat, Nordic hydro, a hyperscale deadline). Each one has three star objectives.
- **Sandbox mode and an interactive tutorial** for learning the ropes.
- **Saves.** Multiple save slots with autosave, and a notification log. On desktop, saves are real files you can back up.
- **Works on a phone.** The UI has a phone layout and the bottom bar scrolls sideways for more tools.

## Progression at a glance

| Tier | Unlocks at level | Focus |
|---|---|---|
| Server closet | 1 | Power and heat basics |
| Small hosting company | 6 | Customers and contracts |
| Regional datacentre | 13 | Reliability and people |
| Enterprise | 21 | Scale and competition |
| Hyperscale | 31 | Optimisation and prestige |
| Global network | 41 | Running datacentres across the world |

## Controls

| Key | Action |
|---|---|
| **E** | Select (the default tool, click to inspect without building) |
| **R** / **P** / **C** | Racks, Power, Cooling build tools |
| **Esc** | Back out a step, clear the selection, or open the menu |
| **G** | Open the in-game guide |
| **Drag** | Pan the camera |
| **Q** | Rotate the selection |
| **Scroll / pinch** | Zoom |

The in-game guide (press **G**) has the full rundown of every system, and it's the best place to learn the details.

On a phone: drag with one finger to look around, pinch to zoom, and swipe the bottom bar sideways for more buttons.

## Running it locally

You need [Node.js](https://nodejs.org) 22 or newer.

```bash
git clone https://github.com/maxhoylestrode/DataCentre-Tycoon.git
cd DataCentre-Tycoon
npm install
npm run dev
```

Then open the address Vite prints in the terminal.

### Other scripts

| Command | What it does |
|---|---|
| `npm run dev` | Dev server with hot reload |
| `npm run build` | Type-check and build the web game into `dist/` |
| `npm run preview` | Serve the production build locally |
| `npm test` | Run the test suite with Vitest |
| `npm run test:watch` | Run the tests in watch mode |
| `npm run desktop` | Build and launch the Electron desktop app |
| `npm run dist:desktop` | Build installers with electron-builder |

## Project layout

```
src/
  sim/        Pure TypeScript simulation. No Three.js or DOM imports.
    content/  Data only: tiers, unlocks, goals, achievements, scenarios, parts.
  render/     Three.js rendering. Reads game state, never changes it.
  input/      Mouse, keyboard and touch. Turns input into sim commands.
  ui/         HUD, panels, dialogs and the guide. Plain DOM, no UI framework.
  io/         Save storage and update checks.
  main.ts     Wires everything together.
electron/     Desktop app shell (main process, preload, save files, window state).
tests/        Vitest tests, mostly for the simulation.
docs/         Notes for contributors, including ADDING_CONTENT.md.
```

The split is deliberate. The simulation is headless and tested on its own, and the renderer and UI only send commands to it. Balance numbers live in `src/config.ts`.

Want to add content? Tiers, unlocks, goals and achievements are plain data in `src/sim/content/`. [docs/ADDING_CONTENT.md](docs/ADDING_CONTENT.md) explains how, and `npm test` checks every entry.

## Art, audio and assets

There are no image, model or audio files to license. Everything is built in code:

- 3D models are Three.js primitives (boxes, cylinders, planes).
- Textures like the raised floor and the die-shot circuits are drawn on canvases at runtime.
- Sound is generated with WebAudio.
- Icons are inline SVG.
- Fonts are Inter and Rajdhani, both under the SIL Open Font License 1.1.

[ASSETS.md](ASSETS.md) lists every asset and where it came from. Hardware part names such as CPUs and GPUs are trademarks of their owners, and the game says so.

## Releases

The web version deploys from `main` to GitHub Pages. Desktop builds are made by GitHub Actions and published to a separate public repository, which is where the app checks for updates. The steps are in [RELEASING.md](RELEASING.md).

## Credits

Made by Apex Studio.

Built with [Vite](https://vitejs.dev), [TypeScript](https://www.typescriptlang.org), [Three.js](https://threejs.org) and [Electron](https://www.electronjs.org).
