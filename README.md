# TechZone — BMAD-Onboarding

Eine statisch ausgelieferte Website, die Entwickler\*innen bei Atruvia den Einstieg in **BMAD** (die [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD), ein KI-gestütztes agiles Entwicklungs-Framework) erleichtert. Die Seite leitet dich zu dem BMAD-Workflow, der zu deiner Situation passt — und lässt dich jedes Thema mit dem KI-Tutor vertiefen.

## Status

**Design und Plan abgeschlossen, Umsetzung folgt.** Dieses Repository enthält aktuell das Domänenmodell, die Architekturentscheidungen und den Bauplan. Die eigentlichen Seiten (Hub und vier Unterseiten) werden auf dieser Grundlage erstellt.

## Idee

Der Einstieg orientiert sich an der Frage »Wo stehst du gerade?«. Die Startseite (der **Hub**) führt über ein 2×2-Raster aus vier anklickbaren Karten zu vier in sich geschlossenen Unterseiten:

| Karte | Situation | Slug |
|---|---|---|
| »Erkunden & Recherche« | Du hast eine vage Idee — Brainstorming und Recherche | `innovate` |
| »Kleine Aufgabe« | Eine kleine, konkrete Änderung im kurzen Dev-Zyklus | `small-task` |
| »Kleines Projekt« | Ein vollständiges Projekt: Planung, Umsetzung, Retro | `small-project` |
| »Lernen mit dem KI-Tutor« | Ein einzelnes Thema tief lernen mit `/atruvia-teach` | `learning` |

Jede Unterseite unter `pages/<slug>/` ist ein in sich geschlossenes Ergebnis, erstellt mit dem Skill `/atruvia-teach`. Der Hub wird mit dem `/atruvia-design-system` gestaltet.

## Struktur (Zielzustand)

```
techzone-onboarding/
├── index.html          # Hub (Startseite, Root-Index)
├── .nojekyll
├── assets/             # eigene Assets des Hubs
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

[MIT](./LICENSE) © 2026 Atruvia AG
