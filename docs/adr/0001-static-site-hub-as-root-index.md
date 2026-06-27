# Static site on GitHub Pages with the Hub as the repo-root index

The site is plain static HTML served by GitHub Pages in "Deploy from a branch" mode (`main` / root `/`), with a root `.nojekyll` so Jekyll never reprocesses the folders. The Hub lives directly at the repository-root `index.html`; there is **no `home/` subfolder**, and the four Pages sit under `pages/<slug>/` alongside it.

## Context

The original idea described a `home/` subfolder *and* called the home page "the index". On a GitHub Pages **project** site (`atruvia.github.io/techzone-onboarding/`) the site root needs an `index.html` directly at the served root, and assets are reached under a `/techzone-onboarding/` subpath.

## Considered options

- **Hub at `home/index.html` + a root redirect** — honours the "home subfolder" wording but adds an indirection file and a redirect flash.
- **Serve from `/docs`** — keeps the repo root clean but forces everything deployable under `/docs`.
- **Hub IS the root `index.html`** (chosen) — zero redirects, works on Pages out of the box.

## Consequences

- **All links and asset references must be relative** (`pages/innovate/`, `../../index.html`) — never root-absolute (`/pages/...`), which would 404 under the project subpath. Relative paths also survive a future custom domain.
- No build step; pushing to `main` publishes.
