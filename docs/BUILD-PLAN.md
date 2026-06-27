# Build Plan — TechZone BMAD Onboarding

Implementation plan derived from the grilling session. Decisions live in [CONTEXT.md](../CONTEXT.md) (glossary) and [docs/adr/](./adr/) (rationale). This file is the *how*.

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

- [ ] `https://atruvia.github.io/techzone-onboarding/` shows the Hub with a working 2×2 grid.
- [ ] Each Card opens its Page; each Page has a working »Zurück zur Übersicht« back-link.
- [ ] All four Pages: German content, ~2–3 lessons + 1 reference, every claim cites a BMAD source.
- [ ] No root-absolute paths anywhere; site works under the `/techzone-onboarding/` subpath.
- [ ] No installation instructions (environment is pre-provisioned); no emoji; brand voice consistent.
```
