# STARWAKE Design & Layout Reference

Working notes for anyone editing the STARWAKE landing page (`STARWAKE Space.html`). The page is a single self-contained HTML file: embedded fonts, embedded key art, one `<style>` block, one `<script>` block, no build step and no external requests.

This document describes the visual system as it stands after the November 2026 refresh, and calls out the places where the code will surprise you if you edit it blind.

---

## 1. Structure of the file

The document is ordered the way the browser reads it:

| Region | What lives there |
| --- | --- |
| `<head>` | Meta, title, two base64 `@font-face` payloads (Orbitron, Share Tech Mono) |
| `<style>` first half | Original layout: tokens, hero, sections, panels, footer |
| `<style>` second half | The `/* ===== VISUAL REFRESH ===== */` block: re-declares `:root`, restyles components, adds responsive and motion rules |
| `<body>` | Hero, then four numbered sections, a play band, the shelf, and the footer |
| `<script>` | Self-invoking function: ticker cycle, steering tester, systems lab simulation |

### The override block matters

The refresh was added as a second stylesheet layer appended before `</style>`, not by rewriting the original rules. Because both layers are in the same block, the later declarations win on equal specificity.

Consequences when editing:

- Changing a token in the **first** `:root` usually has no visible effect, because the second `:root` redeclares it. Edit the tokens in the refresh block.
- Prose-level rules such as `.wrap` or `section.block` may be declared twice. Search for the property, not the selector, before assuming you found the live rule.
- New rules can be appended at the end of the refresh block and will take effect without fighting specificity.

---

## 2. Design tokens

Effective values, as declared in the refresh block:

### Colour

| Token | Value | Role |
| --- | --- | --- |
| `--bg` | `#030706` | Page base, near-black with a green cast |
| `--bg2` | `#07110d` | Alternating section wash |
| `--panel` | `rgba(9, 24, 17, 0.78)` | Card surface |
| `--panel2` | `rgba(12, 34, 23, 0.8)` | Raised surface, key caps |
| `--line` | `rgba(102, 255, 150, 0.34)` | Structural borders, active outlines |
| `--line-dim` | `rgba(102, 255, 150, 0.15)` | Default card borders, dividers |
| `--green` | `#39f27a` | Primary signal colour |
| `--green-hi` | `#b5ffd0` | Interactive text, links, highlights |
| `--ink` | `#eef8f1` | Primary text |
| `--ink-dim` | `#a9bbb0` | Body copy |
| `--ink-faint` | `#657a6e` | Labels, metadata, captions |
| `--amber` | `#ffd166` | Boost, core systems, co-pilot numerals |
| `--red` | `#ff5365` | Damage, sentinel, destructive action |

Semantic rule of thumb: green is the ship and the stream, amber is energy and instrumentation, red is threat. Do not introduce a fourth accent hue; emphasis inside copy is done with weight and `--green-hi` (or `--amber` for warnings).

### Type

| Token | Stack | Use |
| --- | --- | --- |
| `--font-d` | Orbitron, Segoe UI, sans-serif | Wordmark, section headings, buttons, system names |
| `--font-m` | Share Tech Mono, ui-monospace, Menlo, monospace | Labels, readouts, key caps, ticker, stats |
| `--font-b` | Segoe UI, system-ui, sans-serif | Body copy |

Both display faces are embedded as base64 in `@font-face`. Orbitron is declared as the variable range `500 900`, so weights between those endpoints are available without extra payload. Keep body copy on `--font-b`: Orbitron below 15px loses legibility, and the monospace face is for short strings only.

### Scale

- Wordmark: `clamp(50px, 11vw, 132px)`, weight 900
- Section headings: `clamp(30px, 4.8vw, 52px)`
- Play band heading: `clamp(32px, 6vw, 68px)`
- Section intro paragraph: 16.5px, line-height 1.65, capped at 62ch
- Body and card copy: 14.5 to 15px, line-height 1.6
- Eyebrow labels: 11 to 12px monospace, letter-spacing 0.22 to 0.34em, uppercase

---

## 3. Layout

- Content container: `.wrap`, `min(1160px, calc(100% - 48px))`, centred.
- Sections: `section.block` with `clamp(76px, 9vw, 128px)` vertical padding and a hairline bottom border. Each section opens with a 42px green accent rule drawn as a `::before` at the container's left edge.
- Alternating wash: `.block.alt` applies a vertical gradient between `--bg2` and transparent, used by the co-pilot section.
- Grids: `auto-fit, minmax(230px, 1fr)` for controls, three fixed columns for ship systems, `1.05fr 0.95fr` for the co-pilot split.

### Breakpoints

| Query | Behaviour |
| --- | --- |
| `max-width: 760px` | Container narrows to 100% - 32px, hero art shifts to `64%` object position, tester and lab collapse to one column, co-pilot and systems grids stack, ticker stops being sticky, section accent rules inset to 16px |
| `prefers-reduced-motion: reduce` | Smooth scrolling off, all animation and transition durations cut to 0.01ms |

There is no tablet-specific breakpoint. Between 761px and roughly 1000px the existing grids reflow on their own via `auto-fit`; check any new component at ~820px, where the co-pilot split is tightest.

---

## 4. Page anatomy

1. **Hero** (`.hero`). Full-bleed key art at 62% opacity with saturation and contrast pushed down, a horizontal shade gradient for text legibility, and a scanline overlay at 30% with screen blending. The `.hero::after` bottom fade seats the hero into the page. Text sits in `.hero-main`, pushed down with `clamp(120px, 20vh, 220px)` top padding so the wordmark lands below the subject's eyeline.
2. **01 · Controls** (`#fly`). Four `.ctl` cards, then `.tester`: copy beside a 300px steering pad.
3. **02 · Matrix AI** (`#copilot`, `.block.alt`). Numbered `.cp-item` list beside a sticky `.ticker-panel`.
4. **03 · Ship Systems** (`#systems`). Three `.sys` cards with bars, then the `.lab` panel, then `.facts-row`.
5. **Play band**. Full-width CTA stripe with its own radial glow and a decorative `STARWAKE // OPEN CHANNEL` caption set in `::before`.
6. **04 · Studio Shelf** (`#shelf`). Three `.slot` cards, one marked `.now`.
7. **Footer**. Production credit and metadata.

Section numbering in the eyebrow text (`01 ·`, `02 ·` and so on) is hard-coded, not generated. If a section is added or reordered, update the labels by hand.

---

## 5. Components

### Cards (`.ctl`, `.sys`, `.slot`, `.lab`, `.tester`)

Surface is a 145° gradient from translucent panel to near-black, one hairline border in `--line-dim`, an inset top highlight, and a soft drop shadow. `.ctl` and `.sys` add a 44px green hairline in the top-right corner as a `::after`. Hover raises the card 2px and promotes the border to `--line`.

Hover elevation is decorative only. Never gate information behind hover, because the layout must stay usable on touch.

### Key caps (`.key`)

Monospace, 3px bottom border to read as physical keys, `.on` state flips to a filled green (or amber for boost) with a glow. The `data-k` attribute is the contract with the script: `w`, `a`, `s`, `d`, `arrowup`, `arrowleft`, `arrowdown`, `arrowright`, `" "` (space), `shift`. `.steer-key` and `.boost-key` classes are what the script toggles.

### Ticker (`.ticker-panel`)

Header with a pulsing dot, stacked `.tick-line` blocks, and a footer caption. Inactive lines sit at 28% opacity; `.active` brings one to full. Sticky at `top: 32px` on desktop, static below 760px.

### Integrity bars (`.bar` > `i`)

Track is a 11px bordered trough; the fill animates width over 420ms. Fill colour comes from the system's own rule, with `.low` switching to the red gradient. Widths are driven by the script through inline styles.

### Lab (`.lab`)

Two-column panel: readout copy with a four-stat row on the left, a vertical button stack on the right, and a full-width co-pilot message row underneath spanning `1 / -1`. Buttons use a filled surface with `--line-dim` border, brightening on hover; `:active` scales to 0.98.

### Buttons

- `.btn-play`: clipped-corner solid green with dark text, double shadow. The only high-emphasis action on the page; two instances, both pointing at the game.
- `.btn-ghost`: bordered translucent panel for the secondary hero action.
- `.lab-btn`: instrument-panel style for simulation controls; `.danger` variant for the sentinel hit.

---

## 6. Behaviour

All behaviour lives in one self-invoking function at the end of the document. It reads `prefers-reduced-motion` once at start-up.

| Feature | Elements | Notes |
| --- | --- | --- |
| Ticker cycle | `[data-tick]` | Adds `.active` progressively, resets after the last line, ticks every 2100ms. Under reduced motion every line is shown statically and no interval is created. |
| Steering tester | `#padZone`, `#padShip`, `#padReadout`, `#padHint` | Tracks held keys in a local map, moves the ship by 2.4% per frame clamped to 6-94% horizontally and 10-90% vertically, and lights the matching caps. Boost multiplies movement by 1.7. |
| Systems lab | `#btnShard`, `#btnHit`, `#btnReset`, `#barHull/Shield/Core`, `#valHull/Shield/Core`, `#labScore`, `#labShards`, `#labBoost`, `#labSpeed`, `#labMsg` | Mutates hull, shield, core, score, shard count, boost and speed, writes bar widths inline, and writes co-pilot lines into `#labMsg`. |

There is no state persistence: no `localStorage`, no URL state, and a reload resets everything. That is intentional, since the page is a showcase and the real game lives separately.

When adding behaviour, reuse the existing ID naming pattern (`bar*` / `val*` pairs) so the lab stays easy to extend.

---

## 7. Accessibility

- Focus: a global `:focus-visible` rule draws a 2px `--green-hi` outline with 4px offset. The steering pad also carries its own focus ring.
- Motion: the reduced-motion query neutralises transitions and animation durations, and the ticker script skips its interval entirely rather than shortening it.
- Contrast: body copy uses `--ink-dim` on near-black surfaces, comfortably above 4.5:1. Labels at 11px pair the monospace face with wide tracking rather than low opacity, so they stay readable. Avoid dropping opacity below 0.7 on text.
- Semantics: the steering pad is a focusable `role="application"` region with a visible instruction line; the ticker panel has an `aria-label` describing its content.
- Touch: primary controls are at least 44px tall. The hero, play band, and shelf CTAs are plain anchors, so they work without pointer precision.

---

## 8. Repository and deployment

| Item | Location |
| --- | --- |
| Page | `STARWAKE Space.html` at the repository root |
| Docs | `README.md`, this file |
| Hosting | GitHub Pages, `main` branch, root path, HTTPS enforced |
| Live URL | <https://supportaiforall-cmd.github.io/solid-engine/STARWAKE%20Space.html> |

Editing loop: change the HTML locally, open it directly in a browser (no server needed), verify at desktop and about 390px wide, then commit to `main`. Pages rebuilds on push. Confirm the deployed file matches the commit rather than trusting the build status alone, since a build can report success while still serving the previous artifact for a short window.

The URL-encoded space in the filename is deliberate and stable. Renaming the file breaks the published link and any QR code already printed for it.

---

## 9. Editing checklist

- Tokens changed in the refresh `:root`, not the original one
- New component verified at 1440px, 1000px, 820px, and 390px
- Text checked against its surface for contrast, no opacity-only emphasis
- Any new interactive element has a `:focus-visible` state
- Any new animation is skipped or neutralised under reduced motion
- Section eyebrow numbers still match the actual order
- CTAs still point at the game, and the production URL in this file is unchanged
