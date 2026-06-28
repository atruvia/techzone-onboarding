# Vendored Atruvia design system

This folder is a **curated, read-only mirror** of the upstream Atruvia design
system. Do not hand-edit it — change it only by re-vendoring (below).

- **Upstream:** `github.com/atruvia/design-system`
- **Vendored from commit:** `e387596` (2026-06-28, "docs: align README intro with German repo description")
- **Vendored on:** 2026-06-28

## What was copied

| Upstream path | Here |
|---|---|
| `fonts/fonts.css` | `fonts.css` |
| `assets/fonts/VIAType-*.woff2` (7 cuts) | `fonts/VIAType-*.woff2` |
| `tokens/{colors,typography,spacing,radius,shadows,motion,base}.css` | `tokens/` |
| `assets/logos/atruvia-wordmark.svg` | `brand/atruvia-wordmark.svg` |
| `assets/icons/atruvia-icons.svg` | `brand/atruvia-icons.svg` |
| `assets/logos/favicon.ico` | `brand/favicon.ico` |
| `styles.css` (manifest) | `styles.css` (adapted — see below) |

## Adaptations applied (the only deviations from upstream)

1. **`fonts.css` paths flattened:** `url("../assets/fonts/…")` → `url("fonts/…")`,
   because the woff2 files live in `./fonts/` here, not `../assets/fonts/`.
2. **`styles.css` trimmed:** imports `./fonts.css` (not `./fonts/fonts.css`) and
   **drops** the `components/component-styles.css` import — this site uses none of
   the upstream React component styling; it hand-authors `hub.css` / `lessons.css`
   / `page.css` on top of the tokens.

## Deliberately NOT vendored

`_ds_bundle.js` (React), `components/`, `guidelines/`, `ui_kits/`, `templates/`,
`uploads/`, photography, `finanzgruppe*.svg` — unused by this static onboarding site.

## Re-sync

To adopt a newer upstream: re-copy the table above, re-apply the two adaptations,
update the commit hash + date here, then re-run the BUILD-PLAN Phase-2 verification
gates (a new token could rename something the site's layer references).
