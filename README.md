# STARWAKE

**STARWAKE** is a 3D arcade runner about riding the wake of a live data stream. Pilot through green glyph columns, harvest data shards, repair your ship, manage boost, and dodge red wireframe sentinel nodes that actively hunt your line.

> **Playable now:** [Launch STARWAKE](https://supportaiforall-cmd.github.io/solid-engine/STARWAKE%20Space.html)

## What changed

The latest release gives the STARWAKE landing experience a more cinematic cockpit direction while keeping the game controls and interactive systems intact. The visual refresh includes:

- A stronger hero composition with clearer Play and How to Fly actions
- A green-grid cockpit aesthetic with layered gradients, scan textures, and system readouts
- More deliberate spacing and hierarchy across the controls, co-pilot, systems, and studio sections
- Deeper card surfaces, responsive borders, hover states, and status treatments
- Improved mobile layouts for touch controls, ship systems, and the co-pilot ticker
- Visible keyboard focus states and reduced-motion support for a more accessible experience

## The run

The ship accelerates continuously. Thread data shards through the ship's nose to build score, restore integrity, and recharge boost. Sentinel impacts damage the ship, while the Matrix AI co-pilot calls out the state of the run and helps route recovery opportunities.

### Controls

| Action | Inputs |
| --- | --- |
| Steer | WASD, arrow keys, mouse, or touch |
| Boost | Space, Shift, or the on-screen boost control |
| Pause | In-game pause control |
| Sound | In-game sound control |

### Ship systems

- **Hull:** structural integrity and the primary failure state
- **Shield:** absorbs incoming sentinel pressure
- **Core:** keeps the ship's systems online
- **Boost:** trades reserve energy for speed and risk

## Matrix AI co-pilot

The co-pilot is presented as a live crew member rather than a static menu. It:

1. Narrates shards, streaks, near misses, and impacts as they happen
2. Warns about integrity loss early enough to react
3. Adapts shard and sentinel pressure to the way you fly
4. Generates a run debrief from the actual game stats

## Technology

- Three.js
- Web Audio API for synthesized engine and gameplay sound
- Self-contained HTML with embedded assets
- Responsive CSS and touch-friendly controls

## Repository

The playable page is contained in [`STARWAKE Space.html`](./STARWAKE%20Space.html). It can be opened directly in a browser or served as a static page.

Production URL: <https://supportaiforall-cmd.github.io/solid-engine/STARWAKE%20Space.html>

---

*Ilya and Casper Productions, with the assistance of Matrix AI for All*
