# TechZone — BMAD-Onboarding

Eine statisch ausgelieferte Website, die Entwickler\*innen bei Atruvia den Einstieg in **BMAD** (die [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD), ein KI-gestütztes agiles Entwicklungs-Framework) erleichtert. Die Seite leitet dich zu dem BMAD-Workflow, der zu deiner Situation passt — und lässt dich jedes Thema mit dem KI-Tutor vertiefen.

## Status

**Gebaut und live.** Hub und vier Unterseiten sind erstellt, geprüft und über **GitHub Pages** unter <https://atruvia.github.io/techzone-onboarding/> veröffentlicht. Daneben enthält das Repository das Domänenmodell, die Architekturentscheidungen und den Bauplan, auf deren Grundlage die Seiten entstanden sind.

## Idee

Der Einstieg orientiert sich an der Frage »Wo stehst du gerade?«. Die Startseite (der **Hub**) führt über ein 2×2-Raster aus vier anklickbaren Karten zu vier in sich geschlossenen Unterseiten:

| Karte | Situation | Slug |
|---|---|---|
| »Erkunden & Recherche« | Du hast eine vage Idee — Brainstorming und Recherche | `innovate` |
| »Kleine Aufgabe« | Eine kleine, konkrete Änderung im kurzen Dev-Zyklus | `small-task` |
| »Kleines Projekt« | Ein vollständiges Projekt: Planung, Umsetzung, Retro | `small-project` |
| »Lernen mit dem KI-Tutor« | Ein einzelnes Thema tief lernen mit `/atruvia-teach` | `learning` |

Jede Unterseite unter `pages/<slug>/` ist ein in sich geschlossenes Ergebnis, erstellt mit dem Skill `/atruvia-teach`. Hub und Unterseiten teilen sich **dieselbe Gestaltung** — eine gemeinsame, mitlaufende Kopfzeile (`Atruvia · TechZone`), dieselbe Typografie und die **VIA-Linie** als Marken-Konnektor — aufgebaut auf dem `/atruvia-teach`-Lesesystem und dem offiziellen Atruvia Design System (`/atruvia-design-system`).

## Struktur

```
techzone-onboarding/
├── index.html          # Hub (Startseite, Root-Index)
├── .nojekyll
├── assets/             # EINE gemeinsame Quelle: Design-System-Spiegel + CSS/JS (Hub + Unterseiten)
│   └── design-system/  #   selbst gehosteter Spiegel des Atruvia Design Systems
├── pages/
│   ├── innovate/       # je eine in sich geschlossene Unterseite
│   ├── small-task/
│   ├── small-project/
│   └── learning/
├── CONTEXT.md          # Glossar / Ubiquitous Language
└── docs/
    ├── BUILD-PLAN.md   # Dateibaum, Inhalts-Kontrakt, Bau-Reihenfolge
    └── adr/            # Architekturentscheidungen
```

## Design & Technik

- **Offizielles Atruvia Design System, selbst gehostet.** Eine kuratierte Kopie liegt unter `assets/design-system/` — VIAType-Schriften, Design-Tokens, Wortmarke und Icon-Sprite. **Keine externen Laufzeit-Aufrufe** (keine Google Fonts, kein Icon-CDN). Siehe [ADR-0004](./docs/adr/0004-one-shared-self-hosted-assets-folder.md) und [ADR-0005](./docs/adr/0005-zero-external-runtime-dependencies.md).
- **Einheitliche Chrome.** Hub und Unterseiten teilen eine mitlaufende Kopfzeile (`Atruvia · TechZone`; »Zurück zur Übersicht« auf Unterseiten, keiner auf dem Hub) und dieselbe Typografie. Siehe [ADR-0007](./docs/adr/0007-hub-and-lessons-share-one-chrome.md).
- **Die VIA-Linie** ist der handgezeichnete Marken-Konnektor mit Verlauf (navy → blau → aqua), der zwei Begriffe verbindet — eine kanonische Form aus dem Design System (`.atr-via-line`). Siehe [ADR-0006](./docs/adr/0006-via-line-is-a-gradient-connector.md).

## Hosting

Die Seite wird über **GitHub Pages** als Projekt-Site unter `https://atruvia.github.io/techzone-onboarding/` ausgeliefert (Deploy from branch → `main` / root). Alle Links und Asset-Pfade sind **relativ**, damit sie unter dem Projekt-Unterpfad funktionieren.

## Lokale Vorschau

```sh
python3 -m http.server
# danach http://localhost:8000 öffnen
```

## Sprache

Alle nutzerseitigen Inhalte sind **ausschließlich auf Deutsch** (plural »Wir«, informelles »du«, Gender-Stern). Ausnahme sind feststehende englische Begriffe der BMAD-METHOD (z. B. `PM`, `Architect`, `Scrum Master`, PRD) sowie Code.

## Dokumentation

- [CONTEXT.md](./CONTEXT.md) — Glossar und gemeinsame Sprache des Projekts
- [docs/BUILD-PLAN.md](./docs/BUILD-PLAN.md) — Bauplan mit Dateibaum, Inhalts-Kontrakt und Reihenfolge
- [docs/adr/](./docs/adr/) — Architekturentscheidungen (ADRs)

## Lizenz

Proprietär · © 2026 Atruvia AG. **Kein Open Source** — Nutzung ausschließlich durch autorisierte Atruvia-Nutzer*innen für Atruvia-Zwecke. Siehe [LICENSE](./LICENSE).
