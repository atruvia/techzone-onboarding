# Build Plan — TechZone BMAD Onboarding

Implementation plan derived from the grilling session. Decisions live in [CONTEXT.md](../CONTEXT.md) (glossary) and [docs/adr/](./adr/) (rationale). This file is the *how*.

---

# Phase 2 — design-system adoption + shared `/assets/` (2026-06-28)

Migration derived from a second grilling session. Adopts the updated upstream [Design system](../CONTEXT.md) and collapses the per-Page asset copies into **one** shared root `/assets/`. Decisions: [ADR-0004](./adr/0004-one-shared-self-hosted-assets-folder.md) (shared/vendored assets, supersedes the duplication half of ADR-0003 and the framing of ADR-0002) and [ADR-0005](./adr/0005-zero-external-runtime-dependencies.md) (self-host fonts + icons). **This phase supersedes the asset layout in Phase 1 below; everything else in Phase 1 stays accurate.**

## Target file tree (post-migration)

```
techzone-onboarding/
├── index.html                       # Hub — lobby register, new tokens, sprite icons (no Lucide CDN)
├── .nojekyll · README.md · CONTEXT.md
├── assets/                          # ── ONE shared folder: Hub + all four Pages ──
│   ├── design-system/               # VENDORED mirror (read-only) of atruvia/design-system
│   │   ├── VENDOR.md                #   upstream commit + what was copied/trimmed
│   │   ├── styles.css               #   trimmed manifest: fonts + tokens + base (NO component-styles)
│   │   ├── fonts.css · fonts/VIAType-*.woff2   (7 cuts)
│   │   ├── tokens/{colors,typography,spacing,radius,shadows,motion,base}.css
│   │   └── brand/{atruvia-wordmark.svg, atruvia-icons.svg, favicon.ico}
│   ├── hub.css                      # OUR layer — Hub, on new tokens
│   ├── lessons.css                  # OUR layer — teach register, new tokens + reading carve-out
│   ├── page.css                     # OUR layer — page chrome
│   ├── quiz.js                      # OUR layer
│   └── lesson-template.html         # OUR layer — single resumable authoring template (new tokens)
├── docs/adr/0001…0005.md · docs/BUILD-PLAN.md
└── pages/<slug>/                    # innovate · small-task · small-project · learning
    ├── index.html                   # links ../../assets/… ; back-link uses sprite icon-return
    ├── lessons/0001…-*.html          # links ../../../assets/…
    ├── reference/*.html              # links ../../../assets/…
    ├── MISSION.md · RESOURCES.md · NOTES.md · learning-records/   # teach workspace — KEPT
    └── (local assets/ DELETED — incl. old DESIGN-SYSTEM.md)
```

## Build order (vertical slice — same shape as Phase 1)

1. **Vendor** the curated mirror into `assets/design-system/` (+ `VENDOR.md`); trim `styles.css` to drop the `component-styles.css` import.
2. **Hub slice** — rewrite `hub.css` onto the new tokens; swap logo→`atruvia-wordmark.svg`, favicon→`favicon.ico`, icons→sprite (`<use>`); delete the Lucide `<script>`. Prove the Hub renders (Display-800 titles, gradient VIA line, themed sprite glyphs).
3. **Page slice** — rewrite `lessons.css` + `page.css` onto the new tokens **with the reading carve-out** (720px measure, generous air, underlined body links); re-home the retired classes (`.atr-hero`, `.atr-eyebrow`, `.atr-lead`, `.on-navy`, …) into our layer; author the single new-token `lesson-template.html`. Prove `pages/innovate/` end-to-end (landing + lessons + reference + back-link + quiz).
4. **Replicate** — re-point every `<link>`/`<img>`/`<use>` href in the other three Pages to the shared `/assets/` at correct depth; delete each Page's local `assets/` (incl. `DESIGN-SYSTEM.md`). Mechanical — the CSS is now shared and was byte-identical.
5. **Global verify** against the four gates below.

## Definition of done (Phase 2 verification gates)

- [ ] **No dead tokens** — grep finds zero old token names (`--atr-navy`, `--fs-*`, `--space-*`, `--r-*`, `--font-display`, `--atr-coral`, …) in any served CSS/HTML.
- [ ] **Zero external loads** — grep for `https://` in served files returns **only** content citations (BMAD/GitHub); no font/script/stylesheet fetch (kills the Lucide CDN + Google-Fonts import).
- [ ] **Paths resolve under the subpath** — every asset href is relative and correct at each depth (`assets/…` root, `../../assets/…` Page index, `../../../assets/…` lessons/reference); no root-absolute `/assets/`.
- [ ] **Renders self-hosted** — under `python3 -m http.server`: VIAType fonts load, sprite icons theme via `currentColor`, Hub↔Page back-links work both ways, no 404s.

---

# Phase 1 — original build (status met)

The sections below are the original build plan. They remain accurate **except** for the asset layout (per-Page duplication), which Phase 2 above supersedes.

## Target file tree

```
techzone-onboarding/
├── index.html                  # Hub (Root index) — built with /atruvia-design-system
├── .nojekyll                   # stop Jekyll reprocessing folders
├── README.md                   # German: what this is, preview & deploy
├── CONTEXT.md                  # glossary (done)
├── assets/                     # Hub's OWN website-kit assets (not shared with Pages)
│   ├── atruvia-logo.svg
│   ├── via-line.svg
│   ├── colors_and_type.css
│   ├── hub.css                 # hub styles, built only from tokens
│   └── fonts/…
├── docs/
│   ├── adr/0001…0003.md
│   └── BUILD-PLAN.md           # this file
└── pages/
    ├── innovate/               # ── one Page (repeated 4×) ──
    │   ├── index.html          # topic landing (DE) + logo + »Zurück zur Übersicht«
    │   ├── MISSION.md          # teach scaffolding (not linked from site)
    │   ├── RESOURCES.md
    │   ├── NOTES.md
    │   ├── learning-records/
    │   ├── lessons/0001…0003-*.html
    │   ├── reference/*.html
    │   └── assets/design-system/   # OWN copy: lessons.css, fonts, quiz.js, via-line
    ├── small-task/             # same shape
    ├── small-project/          # same shape
    └── learning/               # same shape
```

## Per-Page content contract

Every Page: `index.html` topic landing (German; what the scenario is, when to use it, links to its lessons + reference; logo + back-link) → ~2–3 short Lessons (one tangible win each, cite BMAD docs) → ~1 Reference (cheat sheet/glossary) → own `assets/` copy. Audience has BMAD + Claude CLI + Node + Python pre-installed, so **teach usage, never installation**.

| Page (`slug`) — Card | MISSION (DE) | Lessons (~2–3) | Reference | Primary source |
|---|---|---|---|---|
| `innovate` — »Erkunden & Recherche« | Vage Idee strukturiert erkunden | 1) Wann nutze ich den Analyst/Brainstorm-Modus? 2) Brainstorming mit dem Analyst-Agenten 3) Von Idee zum Project Brief | Cheat-Sheet: Analyst-Befehle & Brainstorming-Techniken | BMAD docs — brainstorming/analysis |
| `small-task` — »Kleine Aufgabe« | Eine kleine konkrete Änderung im kurzen Dev-Zyklus umsetzen | 1) Was ist eine »kleine Aufgabe«? (Scope) 2) Der kurze Dev-Zyklus mit dem Dev-Agenten 3) QA/Review im Kleinen | Cheat-Sheet: Dev-Zyklus-Befehle | BMAD docs — dev cycle |
| `small-project` — »Kleines Projekt« | Vollständiges kleines Projekt: Planung, Umsetzung, Retro | 1) Der volle BMAD-Lebenszyklus im Überblick 2) Planung: PM + Architect (PRD + Architektur) 3) Umsetzung & Retro: SM → Dev → QA → Retro | Cheat-Sheet: Rollen & Artefakte | BMAD docs — full user guide |
| `learning` — »Lernen mit dem KI-Tutor« | Ein einzelnes Thema tief lernen mit `/atruvia-teach` | 1) Was ist der KI-Tutor, wann nutze ich ihn? 2) Eine Lernsession starten: `/atruvia-teach <Thema>` 3) Wie der Tutor arbeitet (Mission, Lektionen, Lernaufzeichnungen) | Cheat-Sheet: `/atruvia-teach` Befehle & Workspace-Dateien | atruvia-teach SKILL.md (self-demonstrating) |

## Hub contract

`/atruvia-design-system` website kit: TopNav (Atruvia logo) → Hero (H1 »Willkommen beim BMAD-Onboarding«, one-line subhead, VIA line) → 2×2 grid of 4 Cards (Lucide icon + German title + one-line description; whole card links to `pages/<slug>/`) → Footer. Brand tokens only; relative links; no emoji.

## Build order

1. **Scaffold** the tree: folders, `.nojekyll`, `README.md`; copy the website-kit assets into root `assets/`.
2. **Hub** — build `index.html` with `/atruvia-design-system`; cards link to `pages/<slug>/` (stubbed at first).
3. **Vertical slice** — build `pages/innovate/` end-to-end with `/atruvia-teach`, grounded in fetched BMAD docs. This proves the per-Page template (landing + back-link + lessons + reference + own assets copy).
4. **Replicate** the proven template to `small-task`, `small-project`, `learning` — each its own `/atruvia-teach` session, German, citing BMAD docs.
5. **Wire & verify navigation** both directions; confirm every link/asset path is relative.
6. **Local preview** with `python3 -m http.server`; fix any path/casing issues.
7. **Deploy** — `git init`, commit, create `atruvia/techzone-onboarding`, push `main`; enable Pages (Deploy from branch → `main` / root). Verify the live URL.

## Definition of done

**Status: met — 2026-06-27, live at <https://atruvia.github.io/techzone-onboarding/> (commit `8d2097f`).**

- [x] `https://atruvia.github.io/techzone-onboarding/` shows the Hub with a working 2×2 grid.
- [x] Each Card opens its Page; each Page has a working »Zurück zur Übersicht« back-link.
- [x] All four Pages: German content, ~2–3 lessons + 1 reference, every claim cites a BMAD source.
- [x] No root-absolute paths anywhere; site works under the `/techzone-onboarding/` subpath.
- [x] No installation instructions (environment is pre-provisioned); no emoji; brand voice consistent.
```
