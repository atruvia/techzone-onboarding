# Hub and Pages use two different Atruvia design systems — one brand, two registers

> **Status: superseded by [ADR-0004](0004-one-shared-self-hosted-assets-folder.md) (2026-06-28).** The "two design systems" framing is obsolete: the site now adopts a single vendored design system, and the Hub and Pages are two *register layers* on top of it. The conclusion that survives — keep the lobby/classroom distinction (two **registers**), guaranteed by shared tokens + the back-link — is restated in ADR-0004. The text below is kept as the historical record.

The Hub is built with `/atruvia-design-system` (marketing/website components: `TopNav`, `Hero`, `Footer`, cards). The Pages are built with `/atruvia-teach`'s `lessons.css` (Tufte-style teaching components: callouts, primary-source boxes, quizzes). We deliberately keep both rather than forcing one.

## Context

The two skills produce different component vocabularies but share the same brand anchor (navy `#000064`, the Atruvia webfont, the VIA line). Forcing everything into one kit would fight each skill's intended output and lose the strength of each.

## Why this is acceptable

The Hub is a *lobby* (route me somewhere) and the Pages are *classrooms* (teach me) — different jobs justify different registers. Coherence is guaranteed by two contracts rather than by pixel-identical components:

1. Shared brand tokens (navy, Atruvia font, VIA line) across both.
2. Every Page header carries the Atruvia logo and a »Zurück zur Übersicht« back-link to the Hub.

## Consequences

- A retheme touches two systems, not one.
- Reviewers should not "unify" the two kits — the split is deliberate.
