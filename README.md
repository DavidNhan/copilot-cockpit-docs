# Projektdokumentation zu Copilot Cockpit

Diese Dokumentation beschreibt das Quell-Repo `C:\Users\danh\copilot-cockpit` auf Basis der tatsaechlichen Dateien, Seiten, Datenkataloge und Tests. Das Projekt selbst ist eine statische, datengetriebene Referenzsite zu GitHub Copilot mit durchgaengiger Luftfahrt-Metapher.

Alle Pfade in dieser Doku beziehen sich auf die Wurzel des Quell-Repos.

## Kurzprofil

| Bereich | Stand |
| --- | --- |
| Anwendungstyp | Statische Multi-Page-Webseite ohne Build-Step |
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
