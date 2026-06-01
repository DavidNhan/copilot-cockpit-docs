# Projektdokumentation zu Workbench

Diese Dokumentation beschreibt die Workbench fuer technische Dokumentation auf Basis von Repositories und Zielumgebungen. Als Referenzobjekt wird das Quell-Repo `C:\Users\danh\copilot-cockpit` genutzt.

Alle Pfade in dieser Doku beziehen sich auf die Wurzel des Quell-Repos.

## Kurzprofil

| Bereich | Stand |
| --- | --- |
| Anwendungstyp | Workbench fuer standardisierte Repo- und Umgebungsdokumentation |
| Zentrale Einstiegspunkte | `index.html`, `terminal.html`, `security.html`, `jet-bridge.html`, `ramp.html`, `runway.html`, `tower.html`, `flight-log.html`, `preflight.html`, `wiring.html` |
| Gemeinsame Laufzeitdateien | `app.js`, `search.js`, `styles.css` |
| Inhaltliche Datenbasis | JSON-Dateien unter `data\` |
| Deployment | Vercel Static Hosting ueber `vercel.json` |
| Test-Setup | Playwright, 11 Spec-Dateien, 222 Tests |
| Zusatz-Tooling | `tools\enrich\` fuer Modellkatalog-Anreicherung, GitHub Action fuer Demo-Aufnahmen |

## Dokumentationssatz

- `docs/architecture.md` - Systembild, Laufzeitarchitektur, Querverbindungen
- `docs/setup.md` - Lokales Starten, Voraussetzungen, Deployment-Hinweise
- `docs/data-sources.md` - JSON-Kataloge, Verbraucher und Pflegepfade
- `docs/testing.md` - Testaufbau, Spec-Dateien und Testfokus
- `docs/site-map.md` - Zweck jeder HTML-Seite inklusive Daten- und Testbezug
- `docs/workbench.md` - Verpflichtender Workbench-Prozess fuer jede neue Dokumentation
- `docs/ultraplan.md` - Ralph-Iterationsplan mit 90%-Qualitaetsziel und Mermaid-Visualisierung
- `docs/output/copilot-cockpit-repo-dokumentation.md` - Ergebnisdokumentation fuer copilot-cockpit.com und das Basis-Repository

## Verbindliche Arbeitsregel

Bei jeder neuen Anfrage zur Erstellung von Dokumentation muessen immer beide Artefakte verwendet werden:

1. `docs/workbench.md`
2. `docs/ultraplan.md`

Eine Auslieferung gilt erst als abgeschlossen, wenn der Ralph-Zyklus ein Ergebnis von mindestens 90% in der Scorecard erreicht.

## Format- und Freigabestandard

Die Workbench erzeugt Dokumentation im festen Format nach Best Practices und den beiden Referenzvorlagen:

1. `SoftwareRequirements.doc`
2. `System_Requirements_Template.docx`

Der resultierende Standard kombiniert klassische SRS-Kapitel mit Anforderungen an Umgebung, Betrieb, Akzeptanz und Revisionsfuehrung.
Technische Dokumentation muss dabei immer Mermaid als visuelle Darstellung einsetzen und mindestens ein Kontext- sowie ein Ablauf-/Datenflussdiagramm enthalten.

## Relevante Quellstrukturen

| Pfad | Zweck |
| --- | --- |
| `*.html` im Repo-Root | Jede Seite ist ein eigener statischer Einstiegspunkt |
| `app.js` | Render-Engine fuer das Cockpit auf `index.html` |
| `search.js` | Globale Suchpalette fuer Instrumente, Controls, Modelle und Changelog |
| `styles.css` | Gemeinsames HUD-Design, Dark/Light Theme, Komponentenstile |
| `data\*.json` | Inhaltlicher Katalog fuer Seiten und Querverweise |
| `tests\*.spec.js` | End-to-End- und Integritaetstests mit Playwright |
| `media\recordings` | GIF-Demos fuer Media-Tabs im Cockpit |
| `tools\enrich\` | Separater Python-Pfad zur Pflege von `data\copilot-models.json` |
| `.github\workflows\record-demos.yml` | Automatisierte Aktualisierung der Demo-Aufnahmen |

## Einordnung

Das Repo ist kein Framework-Projekt und kein API-Backend. Es ist eine rein clientseitige Dokumentations- und Referenzanwendung: HTML + CSS + Vanilla JavaScript laden JSON-Dateien per `fetch()`, rendern daraus Oberflaechen und verbinden die Perspektiven ueber Hash-Deep-Links, lokale Browserzustandsdaten und gemeinsame Navigationsmuster.
