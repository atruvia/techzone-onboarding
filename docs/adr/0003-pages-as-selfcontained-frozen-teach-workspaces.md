# Each Page is a literally self-contained, frozen-but-resumable atruvia-teach workspace

> **Status: partially superseded by [ADR-0004](0004-one-shared-self-hosted-assets-folder.md) (2026-06-28).** Decision **(1) literal self-containment via duplication is reversed** — the four per-Page asset copies collapse into one shared root `/assets/`, and a Page folder no longer works standalone if extracted. Decision **(2) frozen-but-resumable is retained** unchanged: each Page keeps its full teach scaffolding. The text below is kept as the historical record of why duplication was originally chosen.

Each `pages/<name>/` is produced by one `/atruvia-teach` session and committed as static files. Two non-obvious choices fall out of this:

1. **Literal self-containment via duplication.** Every Page bundles its *own* copy of the design system (CSS + Atruvia fonts) under `pages/<name>/assets/`. There is no shared root `/assets/`.
2. **Frozen for serving, but kept resumable.** atruvia-teach is normally an interactive, multi-session tool with a live agent as teacher. We freeze its output into static HTML for GitHub Pages, yet keep the full workspace scaffolding (`MISSION.md`, `RESOURCES.md`, `learning-records/`, `NOTES.md`) committed alongside the served HTML.

## Context

The idea explicitly called each Page "a self-contained result". Developers have the Claude CLI pre-installed, so a committed teach workspace is genuinely re-openable, not dead weight.

## Considered options

- **Shared root `/assets/`** — DRY, smaller repo, one place to retheme; but Pages are no longer standalone if extracted.
- **Duplicated per Page** (chosen) — ~4× duplication of CSS/fonts and brand changes applied in every Page; in exchange each folder works standalone and a brand drift in one Page can't silently change the others.

## Consequences

- Repo carries multiple font/CSS copies; a brand update is a per-Page edit.
- The committed `.md` scaffolding is **not** linked from the site (harmless on Pages) and exists so a developer can re-open the folder in their Claude CLI and continue the teach session live.
- The served deliverable per Page is `index.html` (topic landing) + `lessons/` (~2–3) + `reference/` (~1) + `assets/`.
