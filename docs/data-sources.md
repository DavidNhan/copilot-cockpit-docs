# Workbench Datenquellen

Das Quell-Repo ist stark datengetrieben. Fast alle Inhalte werden aus JSON-Dateien unter `data\` gerendert. Diese Seite beschreibt sowohl die Laufzeitdaten als auch den Pflegepfad fuer den Modellkatalog.

## 1. Laufzeitkataloge unter `data\`

| Datei | Hauptverbraucher | Inhaltlicher Zweck | Wichtige Hinweise |
| --- | --- | --- | --- |
| `data\copilot-instruments.json` | `app.js`, `ramp.html`, `wiring.html`, `search.js` | Zentralkatalog fuer Zonen, Plaene und Instrumente | Enthalten sind Beschreibungen, Status, Planverfuegbarkeit, Capabilities, Diagramme, Codebeispiele, Medien und Querverweise |
| `data\copilot-models.json` | `runway.html`, `tower.html`, `app.js`, `search.js` | Modellkatalog fuer Runway, Tower und Engine-Zone im Cockpit | `verificationRequired: true`; laut Datei ist eine manuelle Verifikation noch noetig |
| `data\governance-controls.json` | `tower.html`, `app.js`, `search.js` | Governance- und Admin-Controls inkl. Compliance-Bezug | In `tower.spec.js` wird erwartet, dass 20 Controls gerendert werden |
| `data\sovereign-cloud.json` | `tower.html` | Deployment-Optionen, EU-Compliance, Provider-Strategien, Restrisiken | Grundlage fuer Mermaid-Diagramm, Optionskarten und Matrix auf der Tower-Seite |
| `data\security-threats.json` | `security.html`, `app.js` | Threat-Katalog pro Instrument bzw. Control | Enthalten sind Threat Models, Demos, Countermeasures, Blast Radius und CWE/Framework-Mappings |
| `data\security-frameworks.json` | `security.html` | Registry fuer OWASP LLM, MITRE ATLAS und CWE-Linkmuster | `verificationRequired: true`; URL- und Titelpflege ist laut Datei noch manuell abzusichern |
| `data\terminal-guide.json` | `terminal.html` | Einstieg fuer Plaene, IDE-Setup, erste Uebungen, naechste Perspektiven | Die Tests erwarten 5 Plan-Karten, 6 IDE-Karten und 3 Uebungen |
| `data\jet-bridge-guide.json` | `jet-bridge.html` | Prompting-, Kontext-, Edit- und Agent-Patterns | Die Seite rendert daraus 6 Techniken, 3 Teilnehmer, 3 Variablen, 3 Workflows und 5 Agent-Patterns |
| `data\preflight-checklist.json` | `preflight.html` | Onboarding-Checkliste ueber mehrere Perspektiven | Enthalten sind 6 Kategorien, deren Fortschritt in `localStorage` gespeichert wird |
| `data\known-changelog-entries.json` | `flight-log.html`, `search.js` | Changelog und Historisierung von Feature-Aenderungen | Beinhaltet `entryTypes` und `entries`; Eintraege verlinken zurueck auf Instrumente |
| `data\wiring-diagram.json` | `wiring.html` | Verbindungsgraph zwischen Instrumenten | Definiert Verbindungstypen und einzelne Kanten fuer den Mermaid-Graph |

## 2. Wer laedt was?

Die Fetch-Pfade sind direkt in den Seitenskripten ablesbar:

| Verbraucher | Gelesene Daten |
| --- | --- |
| `app.js` | `copilot-instruments.json`, optional `security-threats.json`, `governance-controls.json`, `copilot-models.json` |
| `search.js` | `copilot-instruments.json`, `governance-controls.json`, `copilot-models.json`, `known-changelog-entries.json` |
| `terminal.html` | `terminal-guide.json` |
| `jet-bridge.html` | `jet-bridge-guide.json` |
| `security.html` | `copilot-instruments.json`, `security-threats.json`, `security-frameworks.json` |
| `ramp.html` | `copilot-instruments.json` |
| `runway.html` | `copilot-models.json` |
| `tower.html` | `governance-controls.json`, `copilot-models.json`, `sovereign-cloud.json` |
| `flight-log.html` | `known-changelog-entries.json` |
| `preflight.html` | `preflight-checklist.json` |
| `wiring.html` | `wiring-diagram.json`, `copilot-instruments.json` |

## 3. Inhaltliche Rollen der wichtigsten Kataloge

### `copilot-instruments.json`

Diese Datei ist der fachliche Mittelpunkt des Projekts. Sie definiert:

- die 8 Cockpit-Zonen
- die Plan-Tiers
- die Instrumente selbst
- Medien, Codebeispiele, Mermaid-Diagramme und externe Links

Ohne diese Datei funktionieren Cockpit, Ramp und Wiring nicht sinnvoll.

### `copilot-models.json`

Diese Datei speist mehr als nur die Runway-Seite:

- Runway nutzt den vollen Katalog fuer Departure Board, Topologie, Engine-Abschnitt und Detail-Blade
- Tower nutzt ihn fuer Flight Plans
- `app.js` extrahiert daraus eine reduzierte Modellansicht fuer die EICAS/Engine-Zone im Cockpit
- `search.js` macht Modelle global suchbar

Wichtig ist der Pflegehinweis im Dateikopf: Der Katalog ist bewusst als nur teilweise verifiziert markiert.

### `governance-controls.json` und `security-threats.json`

Diese beiden Dateien verbinden das Cockpit mit vertieften Perspektiven:

- `app.js` baut aus `security-threats.json` einen Scanner-Index und zeigt nur fuer abgedeckte Instrumente einen X-Ray-Callout
- `app.js` baut aus `governance-controls.json` einen Governance-Index und zeigt nur fuer passende Instrumente einen Tower-Callout

Dadurch entstehen echte fachliche Querverweise statt lose Navigation.

## 4. Pflegepfad fuer den Modellkatalog

Neben den Laufzeitdaten existiert ein separater Pflegepfad unter `tools\enrich\`.

### Wichtige Dateien

| Datei | Zweck |
| --- | --- |
| `tools\enrich\README.md` | Beschreibt die Enrichment-Pipeline und deren Sicherheitsprinzipien |
| `tools\enrich\sources.yml` | Registry der Upstream-Quellen inklusive URL, Adaptername, Feldumfang und Phase |

### Architekturelle Bedeutung

- Der Pfad ist **nicht** Teil der Browser-Laufzeit.
- Er ist fuer die manuelle oder halbautomatische Pflege von `data\copilot-models.json` vorgesehen.
- Laut README soll die Pipeline Rohdaten sammeln und normalisieren, aber nicht selbsttaetig `data\` veraendern.

## 5. Datenqualitaet und Verifikation

Mehrere Dateien tragen ihren Verifikationsstatus selbst mit:

| Datei | Signal | Bedeutung |
| --- | --- | --- |
| `data\copilot-models.json` | `verificationRequired: true` | Modellmetadaten sind teilweise angereichert, aber nicht vollstaendig menschlich verifiziert |
| `data\security-frameworks.json` | `verificationRequired: true` | Framework-Links und Zusammenfassungen muessen laut Dateikommentar manuell geprueft werden |
| `data\governance-controls.json` | `verificationRequired: false` | Tower zeigt daher keinen Warnbanner mehr |

Fuer inhaltliche Aenderungen an Datenkatalogen sollte immer mitgeprueft werden, welche Seiten und Tests diese Datei konsumieren.
