# One shared `/assets/`, vendored from the Atruvia design system

The Atruvia design system (`github.com/atruvia/design-system`) was updated, and we adopt it as the onboarding's single look. Instead of the four per-Page copies + the Hub's own copy (ADR-0003), there is now **one** root `/assets/` shared by the Hub and every Page. Inside it, `assets/design-system/` is a **curated, read-only vendored mirror** of the upstream system (VIAType fonts, design tokens, a trimmed `styles.css` manifest, official wordmark + icon sprite), and `hub.css` / `lessons.css` / `page.css` / `quiz.js` are the site's own thin layers composed from the new tokens. Pages link up via relative paths (`../../assets/…`, `../../../assets/…`).

## Context

This reverses the duplication half of [ADR-0003](0003-pages-as-selfcontained-frozen-teach-workspaces.md) and obsoletes the "two design systems" framing of [ADR-0002](0002-two-design-systems-one-brand.md). What carries over from those: the **two-register distinction survives** — Hub as *lobby* (TopNav, hero, card grid), Pages as *classroom* (720px reading measure, callouts, quizzes) — but now as two layers on **one** system, not two systems. Coherence is still guaranteed by shared tokens + the »Zurück zur Übersicht« back-link.

## Considered options

- **Per-Page duplication** (the old ADR-0003 choice) — every folder standalone, but ~5× duplicated fonts/CSS and a brand update is a per-Page edit; the system would drift from upstream.
- **Git submodule of the design system** — stays linked to upstream, but GitHub Pages "Deploy from branch" + `.nojekyll` doesn't reliably init submodules (and won't at all for a private/internal repo), and it would drag in the whole system (React bundle, photography, guidelines) for a no-build static site.
- **One shared `/assets/`, curated copy** (chosen) — true adoption of the new tokens with a single source of truth in-repo; re-syncing on the next upstream update is a wholesale folder replace recorded in `assets/design-system/VENDOR.md`.

## Consequences

- A Page folder **no longer works standalone if extracted** — its `../../assets/…` links break outside the repo. This property was deliberately given up.
- **Resumability is unaffected:** each Page keeps its `MISSION.md` / `RESOURCES.md` / `NOTES.md` / `learning-records/`. A resumed `/atruvia-teach` session must link up to the shared `/assets/` (and use the single `/assets/lesson-template.html`) rather than re-bundling a local copy.
- Adopting the new tokens is bounded to rewriting three CSS files, because the lesson HTML is class-based, not token-based — only `<link>` hrefs change in the HTML.
- A brand update is now **one** edit (re-vendor the mirror), not four.
