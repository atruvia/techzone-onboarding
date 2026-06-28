# Hub and Lessons share one chrome; the Hub adopts the atruvia-teach reading system

The Hub (`hub.css`) and Pages (`page.css` + the teach-derived `lessons.css`) had divergent chrome — different headers (`.hub-nav`: sticky, 30px logo, "TechZone" tag vs `.page-top`: static, 24px logo, Back-link) and different hero type (a 60px fixed title + 18px lead vs the teach `.lesson__title` clamp + 22px lead). We unify them so the Hub and quiz pages feel like one page.

- **One shared header shell**, sticky on both, 24px logo, rendered unobtrusively (thin bottom border, slight translucent/blur). The left is a site-wide identity cluster `Atruvia · TechZone`; the right is a slot holding the **Back-link** on a Page and **nothing** on the Hub — the Hub can't carry a Back-link, it *is* the overview the Back-link returns to.
- **The Hub's hero adopts the atruvia-teach lesson-header type roles wholesale** (eyebrow, `.lesson__title` clamp 48→60, 22px lead) instead of its own `.hub-hero__title` / `.hub-hero__lead`. The Hub keeps its hero *layout* (centered, cards below); only the type comes from the shared roles.

The shared header lives in the onboarding's own shared `/assets/` (per [ADR-0004](./0004-one-shared-self-hosted-assets-folder.md)); atruvia-teach ships no page header, so nothing is pushed into the skill — "based on atruvia-teach" means the Hub adopts teach's type/reading system and the shared via-line, not that teach grows site chrome.

## Considered Options

- **Literally identical headers** — rejected: the Hub has no Back-link, so this would either strand a self-pointing link on the Hub or strip the Back-link contract from Pages.
- **Static headers on both** — rejected: sticky keeps the Back-link (the "one site" contract) always one click away and matches the design-system's own sticky header; the slim bar never touches the reading column.
- **Keep the Hub title a notch larger for hero emphasis** — rejected: contradicts "the same"; the clamp already lands at 60px on desktop, so the Hub keeps its presence anyway.

## Consequences

- `.hub-nav`, `.hub-hero__title`, and `.hub-hero__lead` are retired; the Hub uses the shared header + teach type roles. Logo standardized to 24px across all pages.
- The Hub's hero via-line stops being a decorative coral swoosh and becomes the canonical gradient via-line connector (`Technology ↔ Adoption`) — see [ADR-0006](./0006-via-line-is-a-gradient-connector.md).
