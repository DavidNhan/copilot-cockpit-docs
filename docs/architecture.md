# Architekturueberblick

Diese Beschreibung bezieht sich auf das Quell-Repo `C:\Users\danh\copilot-cockpit`.

## 1. Systembild

Copilot Cockpit ist eine statische Multi-Page-Anwendung ohne Build-Step. Die HTML-Dateien im Repo-Root sind direkt deploybare Seiten. Die Logik ist vollstaendig clientseitig:

1. HTML liefert Struktur und Platzhalter.
2. JavaScript laedt JSON-Dateien aus `data\`.
3. Der Browser rendert daraus Karten, Tabellen, Mermaid-Diagramme, Detail-Panels und Filter.
4. Zustand wird ueber `window.location.hash` und `localStorage` gehalten.

Die Kernaussage der Architektur: **Inhalt liegt in JSON, Darstellung in HTML/CSS, Seitenlogik in leichtgewichtigen Seitenskripten.**

## 2. Hauptbausteine

| Baustein | Dateien | Verantwortung |
| --- | --- | --- |
| Statische Seiten | `index.html`, `terminal.html`, `security.html`, `jet-bridge.html`, `ramp.html`, `runway.html`, `tower.html`, `flight-log.html`, `preflight.html`, `wiring.html` | Eigene Seite pro Perspektive oder Utility-Funktion |
| Cockpit-Engine | `app.js` | Laedt Instrumente, Threat- und Governance-Indizes, rendert Grid und Detail-Blade auf `index.html` |
| Globale Suche | `search.js` | Baut einen Suchindex aus Instrumenten, Governance-Controls, Modellen und Changelog-Eintraegen |
| Gemeinsames Styling | `styles.css` | HUD-Layout, Farbtoken pro Zone, Dark/Light Theme, Komponentenstile |
| Inhaltsdaten | `data\*.json` | Fachinhalt fuer alle Seiten, inklusive Querverweise |
| Testschicht | `playwright.config.js`, `tests\*.spec.js` | Browserbasierte Regressionstests und Datenintegritaet |
| Medienpfad | `media\recordings`, `.github\workflows\record-demos.yml` | GIF-Demos fuer Instrumente und deren Aktualisierung |
| Offline-Pflege fuer Modellsicht | `tools\enrich\README.md`, `tools\enrich\sources.yml` | Separater Anreicherungspfad fuer `data\copilot-models.json` |

## 3. Seitenmodell

### 3.1 `index.html` ist die einzige wirklich zentrale Laufzeitseite

`index.html` laedt `app.js` und `search.js` sowie Prism und Mermaid. `app.js` bootet nach `DOMContentLoaded`, laedt parallel mehrere JSON-Quellen und rendert anschliessend:

- Cockpit-Zonen
- Instrumentkarten
- Legende
- Detail-Blade mit Tabs
- Deep-Links und Ruecknavigation

Relevant sind hier vor allem `app.js:41-113` fuer den Start, `app.js:120-244` fuer Grid/Zone-Rendering und `app.js:261-363` fuer die Detail-Blade.

### 3.2 Alle anderen Seiten sind eigenstaendige Inseln

Die restlichen HTML-Dateien enthalten jeweils ein Inline-Skript mit derselben Grundform:

1. Theme initialisieren
2. Eine oder mehrere JSON-Dateien laden
3. DOM fuellen
4. Optional Hash-Deep-Linking, Mermaid-Rendering oder `localStorage` aktivieren

Beispiele:

- `terminal.html:131-149` laedt `data/terminal-guide.json`
- `jet-bridge.html:150-169` laedt `data/jet-bridge-guide.json`
- `security.html:251-253` laedt drei Sicherheitskataloge
- `runway.html:290-312` laedt `data/copilot-models.json`
- `tower.html:193-227` laedt Governance-, Modell- und Souveraenitaetsdaten
- `wiring.html:147-171` laedt Verbindungsgraph und Instrumentkatalog

## 4. Datenfluss

### 4.1 Laufzeitdaten

Der fachliche Kern liegt in `data\`. Fast jede Seite ist datengetrieben:

- `index.html` / `app.js` liest `copilot-instruments.json` als Primarquelle und optional `security-threats.json`, `governance-controls.json`, `copilot-models.json`
- `search.js` baut aus vier JSON-Dateien einen seitenuebergreifenden Suchindex
- `security.html` verbindet Instrumente, Threat-Katalog und Framework-Registry
- `tower.html` verbindet Governance-Controls, Modellkatalog und Souveraenitaetsdaten
- `wiring.html` verbindet Verbindungsgraph und Instrumentkatalog

Damit ist die Anwendung logisch eher ein **statischer Katalog-Renderer** als eine klassische Web-App mit Services oder APIs.

### 4.2 Cross-Page-Navigation

Die Seiten sind bewusst miteinander verdrahtet:

| Ursprung | Ziel | Mechanik |
| --- | --- | --- |
| Cockpit-Detail-Blade | `security.html#scan=<id>` | X-Ray-Callout aus `app.js:410-420` |
| Cockpit-Detail-Blade | `tower.html#control=<id>` | Governance-Callout aus `app.js:423-433` |
| Cockpit-Detail-Blade | `runway.html` oder `runway.html#model-...` | Modell-Callout bzw. Engine-Links |
| Flight Log | `index.html#instrument-...` | Instrument-Links pro Changelog-Eintrag |
| Wiring | `index.html#instrument-...` | Mermaid-Node-Klick oeffnet Cockpit-Instrument |
| Search Palette | Cockpit / Tower / Runway / Flight Log | Direkte Ziel-URLs aus `search.js:28-85` |

### 4.3 Hash-Deep-Links

Die Anwendung nutzt Hashes konsequent fuer teilseiteninterne Navigation:

| Seite | Format | Zweck |
| --- | --- | --- |
| Cockpit | `#instrument-<id>` | Direktes Oeffnen eines Instruments |
| Security | `#scan=<id>` | Vorselektierter Threat/Control-Scan |
| Ramp | `#instrument-<id>` | Direktes Oeffnen der Detail-Blade |
| Runway | `#model-<id>` | Direktes Oeffnen eines Modells |
| Tower | `#control=<id>` / `#sovereign=<id>` | Fokus auf Governance-Control oder Deployment-Option |

## 5. Zustand im Browser

Ein leichter Persistenzlayer steckt komplett im Browser:

| Key | Dateien | Zweck |
| --- | --- | --- |
| `cockpit-theme` | praktisch alle HTML-Seiten plus `app.js` | Dark/Light Theme seitenuebergreifend |
| `cockpit-last-scan` | `security.html` | zuletzt geoeffneter X-Ray-Scan |
| `cockpit-security-posture` | `security.html` | Checkbox-Status des Security Posture Score |
| `copilot-preflight` | `preflight.html` | Fortschritt der Onboarding-Checkliste |

Das ist bewusst minimalistisch: kein Framework-State, kein Store, kein Backend.

## 6. Darstellung und Libraries

### Gemeinsame Designschicht

`styles.css` definiert globale Design-Tokens fuer Farben, Zonen und Statusanzeigen (`styles.css:10-34`). Das Light Theme ist kein separates Stylesheet, sondern eine Override-Schicht unter `body.light-theme` (`styles.css:36-140`).

### Externe Browser-Libraries

| Bibliothek | Verwendung |
| --- | --- |
| Mermaid | Sicherheitsdiagramme, Runway-Topologie, Souveraenitaetsdiagramm, Wiring-Graph |
| Prism.js | Syntaxhighlighting in Code-Beispielen der Cockpit-Detailansicht |

Die Libraries werden per CDN eingebunden; es gibt kein Package-Bundling fuer Browsercode.

## 7. Medien- und Demo-Pfad

Instrumente koennen in `copilot-instruments.json` `terminalRecordings` und `videos` hinterlegen. `app.js:609-658` rendert diese Daten im Media-Tab.

Die GIF-Demos liegen unter `media\recordings`. Die Workflow-Datei `.github\workflows\record-demos.yml` aktualisiert Aufnahmen aus `media\scripts\**` automatisiert und commitet geaenderte GIFs zurueck ins Repo.

## 8. Nicht-Laufzeit-Komponente: `tools\enrich\`

`tools\enrich\` gehoert architektonisch nicht zur ausgelieferten Website, sondern zur Datenpflege des Modellkatalogs:

- `tools\enrich\README.md` beschreibt eine human-gesteuerte Enrichment-Pipeline
- `tools\enrich\sources.yml` listet Upstream-Quellen und Adapter
- Ziel ist die Pflege von `data\copilot-models.json`

Wichtig: Laut Tooling-Doku soll dieser Pfad **nicht direkt in `data\` schreiben**, sondern nur Rohdaten ernten und fuer manuell gepruefte Merges vorbereiten.
