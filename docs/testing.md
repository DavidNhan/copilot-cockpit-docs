# Teststrategie und Testabdeckung

Das Quell-Repo nutzt Playwright als einzigen automatisierten Teststack. Die Tests pruefen sowohl Browserverhalten als auch Datenintegritaet der JSON-Kataloge.

## 1. Technische Basis

Relevante Dateien:

- `package.json` - Script `npm test`
- `playwright.config.js` - Testkonfiguration
- `tests\*.spec.js` - 11 Spec-Dateien

Die Konfiguration in `playwright.config.js` setzt:

| Einstellung | Wert |
| --- | --- |
| `testDir` | `./tests` |
| `reporter` | `list` |
| Browser | Chromium |
| `baseURL` | `http://localhost:3000` |
| lokaler Webserver | `python3 -m http.server 3000 --bind 127.0.0.1` |
| CI-Verhalten | `retries: 2`, `workers: 1` |

## 2. Start der Tests

```bash
cd C:\Users\danh\copilot-cockpit
npm test
```

Optional kann eine einzelne Suite gezielt gestartet werden:

```bash
npx playwright test tests\tower.spec.js
```

## 3. Umfang

Die Testbasis umfasst **222 Tests** in **11 Spec-Dateien**.

| Spec-Datei | Anzahl Tests | Schwerpunkt |
| --- | ---: | --- |
| `tests\cockpit.spec.js` | 29 | Haupt-Cockpit, Blade, Tabs, Filter, Suche, Themes, Deep Links |
| `tests\security.spec.js` | 37 | X-Ray Scanner, Posture Score, Deep Links, Theme, Cockpit-Bruecke |
| `tests\runway.spec.js` | 31 | Modellkatalog, Filter, Blade, Topologie, Engine, Runway-Bruecke |
| `tests\tower.spec.js` | 25 | Governance-Controls, Souveraenitaet, Flight Plans, Print, Deep Links |
| `tests\terminal.spec.js` | 17 | Plan-Auswahl, IDE-Setup, Uebungen, Perspektivnavigation |
| `tests\jet-bridge.spec.js` | 17 | Prompt Craft, Kontext, Edit Mode, Agent Patterns |
| `tests\flight-log.spec.js` | 15 | Timeline, Filter, Instrument-Links, Theme, Navigation |
| `tests\ramp.spec.js` | 15 | Ramp-Karten, Detail-Blade, Deep Links, Metaphernschluessel |
| `tests\wiring.spec.js` | 14 | Mermaid-Graph, Filter, Legende, Zonen, Statistiken |
| `tests\preflight.spec.js` | 13 | Checkliste, Fortschritt, `localStorage`, Reset |
| `tests\integrity.spec.js` | 9 | Katalog- und Querverweis-Integritaet |

## 4. Was wird konkret getestet?

### 4.1 Oberflaechen- und Seitentests

Fast jede Perspektivenseite hat eine eigene Suite fuer:

- fehlerfreies Booten ohne JS-Fehler
- sichtbare Haupt-Landmarks
- aktive Navigationsmarkierung
- korrekte Anzahl und Struktur der gerenderten Karten, Reihen oder Controls

### 4.2 Interaktionstests

Die interaktiven Kernmuster werden direkt auf UI-Ebene abgesichert:

- Cockpit-Detail-Blade, Tabs und Suchfilter
- Runway-Model-Blade und Filterchips
- Ramp-Detail-Blade inkl. Hash-Deep-Link
- Security-Scanner und Posture-Checkboxen
- Pre-Flight-Fortschritt und Reset
- Theme-Persistenz ueber `localStorage`

### 4.3 Cross-Page-Bruecken

Ein wichtiges Architekturmerkmal des Projekts sind Tests fuer Querverbindungen:

- Cockpit -> Security
- Cockpit -> Tower
- Cockpit -> Runway
- Flight Log -> Cockpit
- Wiring -> Cockpit

Damit wird nicht nur isolierte Seitendarstellung, sondern auch die Verdrahtung des Gesamtsystems regressionssicher gemacht.

### 4.4 Integritaet der Datenkataloge

`tests\integrity.spec.js` ist die wichtigste nicht-visuelle Suite. Sie prueft unter anderem:

- Instrument-Referenzen in Changelog-Eintraegen
- Endpunkte in `wiring-diagram.json`
- `relatedInstruments`-Referenzen
- doppelte Instrument- und Modell-IDs
- Pflichtfelder in Instrumenten
- gueltige Zonen
- definierte Changelog- und Connection-Typen

Diese Suite ist fuer dieses Repo besonders wichtig, weil die Anwendung stark datengetrieben ist.

## 5. Testcharakter des Projekts

Die Tests sind keine Unit-Tests fuer lose Funktionen, sondern vor allem:

1. **Smoke Tests** fuer das Booten der Seiten
2. **Akzeptanztests** fuer Interaktionen und Seitensemantik
3. **Datenvertragstests** fuer JSON-Kataloge und ihre Querverweise

Fuer ein statisches, kataloggetriebenes Projekt ist das passend: Die groessten Risiken liegen hier in kaputten Links, ungueltigen IDs, unvollstaendigen Datenobjekten und ausfallenden Seitenskripten.

## 6. Was bei Aenderungen mitgetestet werden sollte

| Aenderung | Relevante Tests |
| --- | --- |
| Cockpit-Instrumente oder Detail-Blade | `cockpit.spec.js`, oft auch `security.spec.js`, `tower.spec.js`, `runway.spec.js`, `integrity.spec.js` |
| Sicherheitsdaten | `security.spec.js`, `integrity.spec.js` |
| Governance- oder Souveraenitaetsdaten | `tower.spec.js`, `integrity.spec.js` |
| Modellkatalog | `runway.spec.js`, `tower.spec.js`, `integrity.spec.js` |
| Wiring-Graph | `wiring.spec.js`, `integrity.spec.js` |
| Changelog-Eintraege | `flight-log.spec.js`, `integrity.spec.js`, indirekt `search.js` |
| Onboarding-/Tutorial-Daten | `terminal.spec.js`, `jet-bridge.spec.js`, `preflight.spec.js` |

## 7. Bewertung

Fuer eine statische Referenzsite ist die Testabdeckung auffallend systematisch. Das Repo testet nicht nur Rendering, sondern auch Datenvertraege, Deep Links, lokale Persistenz und fachliche Bruecken zwischen den Perspektiven. Genau diese Kombination schuetzt das Projekt vor den wahrscheinlichsten Fehlern.
