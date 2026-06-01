# Workbench Seitenlandkarte

Diese Uebersicht beschreibt jede HTML-Seite des Quell-Repos `C:\Users\danh\copilot-cockpit`, ihren fachlichen Zweck, ihre Datenquellen und die zugehoerige Testabdeckung.

## Gesamtstruktur

Die Site folgt einer Flughafenreise:

1. `terminal.html` - Einstieg
2. `jet-bridge.html` - Arbeitsweise mit Copilot
3. `ramp.html` - autonome und externe Tool-Ebene
4. `index.html` - Haupt-Cockpit
5. `runway.html` - Modell- und Routing-Sicht
6. `tower.html` - Governance- und Admin-Sicht

Dazu kommen vier Utility- bzw. Vertiefungsseiten:

- `security.html`
- `flight-log.html`
- `preflight.html`
- `wiring.html`

## Seitentabelle

| Datei | Rolle | Hauptdaten | Wichtige Interaktionen | Testdatei |
| --- | --- | --- | --- | --- |
| `index.html` | Zentrale Cockpit-Uebersicht mit allen Instrumenten in 8 Zonen | `copilot-instruments.json`, optional Threats, Governance-Controls und Modelle | Filter, Inline-Suche, Detail-Blade, Tabs, Cross-Links zu Security/Tower/Runway, globale Suche ueber `search.js` | `tests\cockpit.spec.js` |
| `terminal.html` | Onboarding-Einstieg: Plaene, IDE-Setup, erste Uebungen, naechste Ziele | `terminal-guide.json` | reine Katalogdarstellung mit Perspektivnavigation | `tests\terminal.spec.js` |
| `jet-bridge.html` | Arbeitsmethodik: Prompt Craft, Kontextsteuerung, Edit Mode, Agent Patterns | `jet-bridge-guide.json` | tutorialartige Karten und Beispielprompts | `tests\jet-bridge.spec.js` |
| `ramp.html` | Perspektive fuer Agenten, MCP und externe Tool-Ausfuehrung | `copilot-instruments.json` (gefiltert auf `perspectives.includes('ramp')`) | Kartenraster, Detail-Blade, Deep Link `#instrument-...` | `tests\ramp.spec.js` |
| `runway.html` | Voller Modellkatalog und Routing-Sicht | `copilot-models.json` | Filter nach Plan/Provider/Status, Modell-Blade, Deep Link `#model-...`, Mermaid-Topologie | `tests\runway.spec.js` |
| `tower.html` | Governance, Compliance, Datenresidenz, Flight Plans | `governance-controls.json`, `copilot-models.json`, `sovereign-cloud.json` | Highlight per `#control=...` und `#sovereign=...`, Print-Ansicht, Mermaid-Diagramm | `tests\tower.spec.js` |
| `security.html` | Sicherheits- und Bedrohungssicht mit X-Ray Scanner | `copilot-instruments.json`, `security-threats.json`, `security-frameworks.json` | Scan-Wechsel, Threat-Details, Posture Score, `#scan=...`, Print | `tests\security.spec.js` |
| `flight-log.html` | Changelog-/Timeline-Sicht | `known-changelog-entries.json` | Filter nach Entry-Typ und Zone, Links zurueck ins Cockpit | `tests\flight-log.spec.js` |
| `preflight.html` | Interaktive Onboarding-Checkliste | `preflight-checklist.json` | Checkboxen, Fortschrittsanzeige, `localStorage`, Reset | `tests\preflight.spec.js` |
| `wiring.html` | Verbindungskarte zwischen Instrumenten | `wiring-diagram.json`, `copilot-instruments.json` | Filterbare Mermaid-Grafik, Legende, Zonen- und Statistikansicht | `tests\wiring.spec.js` |

## Detailbeschreibung pro Seite

## `index.html`

Die Hauptseite ist kein statischer Textcontainer, sondern die eigentliche Produktkarte des Projekts. `app.js` laedt den Instrumentkatalog und erzeugt daraus:

- Zonenkacheln
- Instrumentkarten
- Status-LEDs
- eine rechte Detail-Blade mit Overview-, Diagram-, Code-, Media- und Resources-Tabs

Zusaetzlich laedt die Seite `search.js`, womit nur hier die globale Suchpalette fuer Instrumente, Modelle, Controls und Changelog-Eintraege verfuegbar ist.

## `terminal.html`

Die Seite beantwortet die Frage: **Wie steige ich ein?** Sie ist in vier Abschnitte gegliedert:

- Check-In Desk fuer Planwahl
- Boarding Pass fuer IDE-Setup
- First Flight fuer erste Uebungen
- Departure Board fuer naechste Perspektiven

Sie ist deutlich kuratierter als das Cockpit und wirkt eher wie eine gefuehrte Einfuehrung.

## `jet-bridge.html`

Diese Seite schliesst die Luecke zwischen erstem Einstieg und taeglicher Nutzung. Der Schwerpunkt liegt auf Arbeitsweise statt Produktkatalog:

- gute vs. schlechte Prompts
- Kontextteilnehmer wie `@workspace` oder `@terminal`
- Edit-Workflows
- Agent-Muster inklusive Risikoindikatoren

## `ramp.html`

Die Ramp-Seite extrahiert aus dem allgemeinen Instrumentkatalog nur die fuer autonome bzw. externe Toolnutzung relevanten Instrumente. Inhaltlich ist sie die operative Infrastruktur-Sicht fuer:

- Cloud Agent
- MCP
- Agent Self-Review
- Extensions
- Autopilot
- Agent-Konfiguration

## `runway.html`

Runway ist die Modell- und Routing-Sicht des Systems. Die Seite kombiniert drei Ebenen:

1. **Katalog** aller Modelle
2. **Topologie** zwischen IDE, GitHub API, Cloud-Modellen, Cloud Runtime und BYOK
3. **Bewertung** ueber NOTAMs, Flight-Plans und Detail-Blade

Das macht Runway zur technisch tiefsten Datenkatalog-Seite neben dem Cockpit.

## `tower.html`

Tower ist die administrative Gegenseite zu Runway. Statt Modellwahl geht es hier um Steuerung, Compliance und Betriebsgrenzen:

- Framework-Legende
- Governance-Control-Liste
- Souveraenitaets- und Residency-Sicht
- modellbezogene Flight Plans aus Governance-Perspektive

Die Seite ist ausserdem Ziel der Governance-Callouts aus dem Cockpit.

## `security.html`

Security ist keine allgemeine Uebersichtsseite, sondern eine drill-down-faehige Risikosicht. Der X-Ray Scanner verbindet:

- Control/Instrument-Auswahl
- Threat Model
- Angriffsszenario
- Before/After-Demo
- Countermeasures
- OWASP-, ATLAS- und CWE-Referenzen

Inhaltlich ist das die sicherheitstechnisch am staerksten strukturierte Seite.

## `flight-log.html`

Flight Log dient der Historisierung. Es macht Produktveraenderungen sichtbar und verknuepft sie mit betroffenen Instrumenten. Dadurch entsteht fuer das Repo ein nachvollziehbarer Fachkontext fuer neue oder geaenderte Inhalte.

## `preflight.html`

Pre-Flight ist eine utilityartige Checkliste fuer Einfuehrung und Rollout. Die Seite ist fachlich querliegend: Ihre Kategorien verweisen auf andere Perspektiven und machen den Onboarding-Fortschritt messbar.

## `wiring.html`

Wiring ist die graphische Sicht auf Abhaengigkeiten und Signale. Anders als das Cockpit zeigt die Seite nicht die fachliche Einordnung eines einzelnen Instruments, sondern die Beziehungen zwischen Instrumenten und Zonen.

## Querverbindungen zwischen den Seiten

| Von | Nach | Zweck |
| --- | --- | --- |
| Cockpit | Security | Sicherheitsvertiefung fuer abgedeckte Controls |
| Cockpit | Tower | Governance-Vertiefung fuer steuerbare Controls |
| Cockpit | Runway | Modellauswahl und Routing-Kontext |
| Flight Log | Cockpit | Ruecksprung auf betroffene Instrumente |
| Wiring | Cockpit | Klick auf Graph-Knoten oeffnet Instrument |
| Pre-Flight | verschiedene Perspektiven | Lern- und Rolloutpfad |
