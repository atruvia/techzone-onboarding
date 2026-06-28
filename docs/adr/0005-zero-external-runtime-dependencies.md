# Zero external runtime dependencies — self-host fonts and the Atruvia icon sprite

The site makes **no external runtime calls**. Two dependencies that previously hit the network are removed: the Google-Fonts `@import` (Manrope + JetBrains Mono) in the old `colors_and_type.css`, and the Lucide CDN `<script>` on the Hub. Fonts are now the self-hosted VIAType woff2 files (`ATRUVIA` / `ATRUVIA Mono`) shipped by the vendored design system. Icons are now the self-hosted official Atruvia sprite (`assets/design-system/brand/atruvia-icons.svg`), referenced via `<svg><use href="…#icon-…">` with color set through `currentColor`.

## Context

"Self-hosted" was an explicit goal of this migration. The Google-Fonts import dies for free once the reconstructed `colors_and_type.css` is retired in favour of the vendored, self-hosting `fonts.css`. The Lucide CDN is the only remaining live call, and the updated design system ships an official, themeable icon sprite (no baked-in fills; uniform `200×200` viewBox), so we switch to it.

## Considered options (icons)

- **Inline the Lucide SVGs** — zero JS, zero network, keeps Lucide's exact metaphors (`compass`, `wrench`, `graduation-cap`). Rejected: not the official brand iconography.
- **Self-host `lucide.js`** — ships a JS runtime to render a handful of static icons. Rejected as wasteful.
- **Atruvia sprite via `<use>`** (chosen) — official, on-brand, zero JS. The trade-off is metaphor fidelity: the corporate set has no `compass`/`wrench`/`graduation-cap`, so the four Cards map to `icon-idea` (Erkunden), `icon-edit` (Kleine Aufgabe), `icon-routes` (Kleines Projekt) and `icon-robot` (KI-Tutor) — arguably stronger matches — with `icon-arrow-right` for the card affordance and `icon-return` for the back-link.

## Consequences

- The icon **style** shifts from Lucide's hairline stroke to Atruvia's house style — a deliberate on-brand change, not a regression.
- The four scenario glyphs are now corporate-set substitutions; a reviewer who expects the old metaphors should read this ADR before "fixing" them.
- A standing verification gate: a grep for `https://` in served files must return **only** content citations (BMAD/GitHub), never a font/script/stylesheet fetch.
