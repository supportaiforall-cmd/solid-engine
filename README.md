# STARWAKE

**STARWAKE** is a 3D arcade runner about riding the wake of a live data stream. Pilot through green glyph columns, harvest data shards, repair your ship, manage boost, and dodge red wireframe sentinel nodes that actively hunt your line.

> **Playable now:** [Launch STARWAKE](https://supportaiforall-cmd.github.io/solid-engine/STARWAKE%20Space.html)

## Recent design changes

**November 2026 · commit [`b6319ae`](https://github.com/supportaiforall-cmd/solid-engine/commit/b6319ae034007783f0309eb0c851ff303d05144f)** The landing page was reworked around a cinematic cockpit direction. The game itself, its controls, and every interactive system were left untouched.

- **Hero.** Larger wordmark, a bordered kicker badge, heavier shade and scan overlays on the key art, and clearer Play / How to Fly calls to action.
- **Atmosphere.** A fixed green grid overlay, layered radial gradients behind the page, and a bottom fade that seats the hero into the first section.
- **Sections.** Numbered index labels with a hairline accent rule, a tighter heading hierarchy, and more generous vertical rhythm between blocks.
- **Cards.** Deeper gradient surfaces with hairline top accents and a subtle lift on hover across controls, ship systems, and shelf slots.
- **Instrumentation.** The systems lab and tester panels sit on a darker plate with clearer button hover and pressed states.
- **Mobile.** Single-column tester and lab layouts, repositioned hero art for narrow screens, and a static co-pilot ticker instead of a sticky one.
- **Accessibility.** Visible `:focus-visible` rings on every interactive element and a `prefers-reduced-motion` fallback that disables transitions and smooth scrolling.

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
