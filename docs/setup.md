# Setup und Betrieb

Diese Anleitung beschreibt das Quell-Repo `C:\Users\danh\copilot-cockpit`.

## 1. Voraussetzungen

Da die Website statisch ist, sind die Voraussetzungen ueberschaubar:

- Node.js und npm fuer Abhaengigkeiten und Playwright
- Python 3 fuer den in `playwright.config.js` definierten lokalen Webserver
- Ein statischer HTTP-Server, falls die Seiten ohne Playwright lokal angesehen werden sollen

Wichtig: Die HTML-Seiten koennen nicht sinnvoll per `file://` geoeffnet werden, weil sie JSON-Dateien per `fetch('data/...')` laden.

## 2. Installation

```bash
cd C:\Users\danh\copilot-cockpit
npm install
npx playwright install chromium
```

`package.json` definiert bewusst nur eine minimale Node-Seite: Die einzige Dev-Dependency ist `@playwright/test`.

## 3. Lokales Starten

### Option A: Beliebiger statischer Server

Das README des Quell-Repos nennt diesen einfachen Weg:

```bash
npx serve .
```

Danach kann die Site lokal ueber den ausgegebenen Port geoeffnet werden.

### Option B: Start ueber den Testpfad

`playwright.config.js` startet fuer Tests automatisch einen Webserver:

```bash
npm test
```

Intern nutzt die Konfiguration:

- `baseURL: http://localhost:3000`
- `webServer.command: python3 -m http.server 3000 --bind 127.0.0.1`

Damit ist Python 3 eine praktische Laufzeitvoraussetzung fuer den Testbetrieb.

## 4. Seitenstruktur im Betrieb

Die Anwendung besteht aus direkt auslieferbaren Root-Dateien:

- `index.html` fuer das Haupt-Cockpit
- weitere HTML-Dateien fuer jede Perspektive und Utility-Seite
- `styles.css` als gemeinsames Stylesheet
- `app.js` und `search.js` als gemeinsame JavaScript-Dateien
- `data\*.json` als Inhaltskataloge

Es gibt keinen Build-Output, kein `dist\` und keinen Bundler.

## 5. Deployment

`vercel.json` zeigt, dass das Repo als reine statische Site deployt wird:

- `buildCommand` ist leer
- `outputDirectory` ist `.` (Repo-Wurzel)
- Cache-Header sind separat fuer `media`, `.css`, `.js` und `data` gesetzt

Praktisch bedeutet das:

1. HTML-Dateien werden direkt aus dem Repo ausgerollt.
2. JavaScript und JSON erhalten kurze Revalidierungsfenster.
3. Medien unter `media\` werden langfristig gecacht.

## 6. Typische Aenderungspfade

| Aenderungsart | Relevante Dateien |
| --- | --- |
| Neue Perspektivenseite | neue `*.html`, ggf. neue JSON-Datei unter `data\`, passende Spec-Datei unter `tests\` |
| Neue oder geaenderte Instrumente | `data\copilot-instruments.json`, evtl. `app.js`, `wiring-diagram.json`, `known-changelog-entries.json`, Tests |
| Modellkatalog aktualisieren | `data\copilot-models.json`, optional `tools\enrich\` |
| Governance-Inhalte | `data\governance-controls.json`, `data\sovereign-cloud.json`, `tower.html`, Tests |
| Sicherheitsinhalte | `data\security-threats.json`, `data\security-frameworks.json`, `security.html`, Tests |

## 7. Hinweise fuer lokale Entwicklung

- Theme-Zustand wird per `localStorage` gespeichert und ueber Seiten hinweg wiederverwendet.
- Mehrere Seiten nutzen Mermaid; Probleme zeigen sich oft erst im Browser und sollten per Playwright mitgetestet werden.
- Das Repo hat eigene Medienaufnahmen fuer Instrumente. Wenn sich Media-Tabs oder Pfade aendern, muessen `media\recordings` und der Demo-Workflow mitgedacht werden.
- `tools\enrich\` ist ein separater Python-Pfad und nicht noetig, um die Website lokal zu starten.
