# Vendored Atruvia design system

This folder is a **curated, read-only mirror** of the upstream Atruvia design
system. Do not hand-edit it — change it only by re-vendoring (below).

- **Upstream:** `github.com/atruvia/design-system`
- **Vendored from commit:** `e387596` (2026-06-28, "docs: align README intro with German repo description")
- **Vendored on:** 2026-06-28

## What was copied

| Upstream path | Here |
|---|---|
| `fonts/fonts.css` | `fonts.css` (rewritten — see deviation 3) |
| ~~`assets/fonts/VIAType-*.woff2`~~ (BROKEN upstream) | **not used** — see deviation 3 |
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
3. **Fonts substituted — upstream fonts are BROKEN.** Every upstream
   `assets/fonts/VIAType-*.woff2` (and the `uploads/` hashed copies) is actually
   an **HTML page**, not a font (magic bytes `<!D…`, ~58 KB, `lang="de-DE"`), so a
   browser silently falls back to a system sans. We instead ship the **real Atruvia
   corporate typeface** — `fonts/atruvia-{light,regular,medium,bold}.woff2` (real
   `wOF2`, 300/400/500/700) recovered from this project's pre-migration commit
   `142221e^` — and rewrote `fonts.css` to map family `"ATRUVIA"` to them
   (600/800 → real Bold; no `"ATRUVIA Mono"`, so `--font-mono` → ui-monospace).
   **On re-sync: do NOT re-copy the upstream woff2 until upstream ships real fonts;
   verify `head -c4` is `wOF2`, not `<!D`.**

## Deliberately NOT vendored

`_ds_bundle.js` (React), `components/`, `guidelines/`, `ui_kits/`, `templates/`,
`uploads/`, photography, `finanzgruppe*.svg` — unused by this static onboarding site.

## Re-sync

To adopt a newer upstream: re-copy the table above, re-apply the two adaptations,
update the commit hash + date here, then re-run the BUILD-PLAN Phase-2 verification
gates (a new token could rename something the site's layer references).
