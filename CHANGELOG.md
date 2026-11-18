# Changelog

Notable changes to the STARWAKE project, newest first. Each entry names the commit it landed in so the history can be traced back in git.

---

## 2026-11-18

### Documentation

- Expanded the README design summary into a dated **Recent design changes** section with a link to the design commit and notes grouped by area: hero, atmosphere, sections, cards, instrumentation, mobile, and accessibility. (`861c158`)
- Added this changelog, covering the project's commits to date rather than only the design refresh.
- Added `DESIGN.md`, a design and layout reference covering tokens, type scale, layout, components, script behaviour, accessibility, and the deploy loop. (`0e411fa`)
- Added QR codes for the live page as `assets/starwake-qr-light.png`, `assets/starwake-qr-dark.png`, and `assets/starwake-qr-print.svg`. All three were decoded back to the exact page URL before committing. (`c1408d5`)

### Fixed

- Small label text (`--ink-faint`) sat at 3.7:1 on card surfaces, failing WCAG AA. Raised from `#657a6e` to `#7b9484`, which measures 5.26:1 on cards and 6.18:1 on the page background. (`de5e0c0`)
- Added a meta description plus `og:type`, `og:title`, and `og:description`, which the page previously lacked entirely. (`de5e0c0`)

---

## 2026-11-10

### Added

- `STARWAKE Space.html` enters the repository as a single self-contained page: embedded fonts, embedded key art, one stylesheet block, one script block, no build step and no external requests. The file arrives already carrying the November visual refresh. (`b6319ae`, 1,032 lines added)

### Changed

- Landing page redesigned around a cinematic cockpit direction while leaving the game, its controls, and every interactive system untouched. The refresh was applied as a second CSS layer appended inside the same stylesheet block, which is why editing the original `:root` no longer changes anything.

### Documentation

- README grew from a one-line stub into full project documentation: overview, live URL, design changes, the gameplay loop, a controls table, ship systems, Matrix AI co-pilot behaviour, technology notes, and repository layout. (`a24061a`, +62/-1)

### Deployment

- GitHub Pages enabled for the `main` branch at the repository root, with HTTPS enforced. Production URL published at <https://supportaiforall-cmd.github.io/solid-engine/STARWAKE%20Space.html>.

---

## 2026-11-07

### Added

- Initial commit. Repository created with a placeholder `README.md`. (`e47208e`)

---

## State of the project

| Area | Where it stands |
| --- | --- |
| Playable page | Live on GitHub Pages, verified byte-for-byte against the committed file |
| Design | November refresh shipped: hero rework, cockpit atmosphere, card depth, responsive and reduced-motion handling |
| Documentation | README covers product and design; this changelog covers history |
| Game itself | Separate build; this repository hosts the landing page only |
