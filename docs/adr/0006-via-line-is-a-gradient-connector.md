# Via-line is a hand-drawn gradient connector, promoted to the design system

The via-line — the brand's signature connecting motif — existed three incompatible ways: a flat gradient bar named `.atr-via-line` in the **Design system**; a gradient SVG connector in **atruvia-teach**; and a **coral** hand-drawn SVG in the onboarding (a decorative Hub swoosh `.hub-hero__via` plus labeled Lesson connectors `.via-line`). We make the hand-drawn, self-drawing SVG **connector** the one canonical via-line: painted with the VIA gradient (`--atr-via-gradient`; coral retired), always linking exactly **two labeled terms**, using **one shared path shape** reused on the Hub and every Lesson with only the labels swapped. That shape is the flowing **swoosh** (the former Hub `.hub-hero__via` geometry), chosen over a connector-with-loop alternative after a side-by-side prototype; each instance anchors a word at each end. It is defined once in the upstream Design system as `.atr-via-line`, flows to the `atruvia-design-system` skill copy via the existing sync, and is **consumed, not reinterpreted**, by atruvia-teach and the onboarding — which realigns with [ADR-0002](./0002-two-design-systems-one-brand.md) and the CONTEXT rule that the onboarding "never reinterprets" the Design system (the coral local version *was* such a reinterpretation).

## Considered Options

- **Keep coral** (distinctive, celebrated in earlier work) — rejected: coral is reserved for danger/accent, a coral *connector* discards the VIA "Wir verbinden" meaning, and a coral line cannot be promoted upstream as a brand default.
- **Name the connector `.atr-via-connector`, leave the flat bar as `.atr-via-line`** — rejected: the team already *says* "via-line" meaning the connector, so the code should match; the flat bar is genuinely a divider rule.
- **Per-page custom path shapes** (shared treatment only) — rejected: reintroduces the exact Hub-vs-Lesson visual inconsistency this change exists to remove.

## Consequences

- Breaking rename inside the Design system: `.atr-via-line` → `.atr-via-rule` (one usage in `ui_kits/website/sections.jsx`, plus its `guidelines/brand-via-line.html` card). `.atr-via-text` is unaffected.
- The onboarding deletes `.hub-hero__via` and its local `.via-line`; the Hub hero line stops being a decorative swoosh and becomes a real connector (`Technology ↔ Adoption`).
- The canonical path + gradient + draw-animation ship from the Design system; each page only authors its two labels.
