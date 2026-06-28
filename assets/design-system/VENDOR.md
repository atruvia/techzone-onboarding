# Vendored Atruvia design system

This folder is a **curated, read-only mirror** of the upstream Atruvia design
system. Do not hand-edit it — change it only by re-vendoring (below).

- **Upstream:** `github.com/atruvia/design-system`
- **Vendored from commit:** `bed17cc` (2026-06-28, "chore: remove broken HTML-as-woff2 fonts from uploads/"; the real typeface landed upstream in `5cf2208`)
- **Vendored on:** 2026-06-28

> **2026-06-28 — via-line promotion:** `tokens/base.css` was re-vendored to carry
> the canonical hand-drawn **`.atr-via-line`** connector and the renamed
> **`.atr-via-rule`** (the former flat-bar `.atr-via-line`). See ADR-0006 —
> re-vendored from design-system `5f8a909`; the full-mirror hash above bumps
> on the next complete re-sync.

## What was copied

| Upstream path | Here |
|---|---|
| `fonts/fonts.css` | `fonts.css` (path-flattened — see deviation 1) |
| `assets/fonts/VIAType-{Light,Regular,Medium,Bold}.woff2` | `fonts/VIAType-*.woff2` (4 real cuts) |
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

## Resolved — the former font substitution

Earlier mirrors carried a third deviation: upstream had shipped **broken** font
files (every `assets/fonts/VIAType-*.woff2` was actually an HTML page, magic
`<!D…`), so this mirror substituted real fonts — renamed `atruvia-*.woff2` —
recovered from a pre-migration commit. Upstream fixed this at the source in
`5cf2208`, so the fonts are now vendored **straight from upstream** with their
original `VIAType-*` filenames — no substitution, no rename. The four files are
byte-identical to upstream (verified `sha256` match). The brand ships **four
real weights** (300/400/500/700); weight 600 and 800 reuse the real Bold, and
there is no brand mono, so `--font-mono` falls back to a system mono stack.

**On re-sync, still verify** each woff2 is a real font: `head -c4` must be
`wOF2`, not `<!D`.

## Deliberately NOT vendored

`_ds_bundle.js` (React), `components/`, `guidelines/`, `ui_kits/`, `templates/`,
`uploads/`, photography, `finanzgruppe*.svg` — unused by this static onboarding site.

## Re-sync

To adopt a newer upstream: re-copy the table above, re-apply the two adaptations,
update the commit hash + date here, then re-run the BUILD-PLAN Phase-2 verification
gates (a new token could rename something the site's layer references).
