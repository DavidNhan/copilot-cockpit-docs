# Datenquellen und Datenvertraege

## Zweck

Dieses Dokument beschreibt die fachlichen Datenquellen von Copilot Cockpit, ihre Verbraucher und die Regeln zur Datenqualitaet.

## 1. Datenstrategie

Copilot Cockpit folgt einem data-first Ansatz:

- Fachinhalt liegt in JSON-Katalogen
- Seitenlogik rendert Daten statt Inhalte hart zu codieren
- Integritaetsregeln werden per Tests abgesichert

Damit sind Datenaenderungen oft wichtiger als JavaScript-Aenderungen.

## 2. Kataloguebersicht

| Katalog | Hauptzweck | Primaere Verbraucher |
| --- | --- | --- |
| `copilot-instruments.json` | Instrumente, Zonen, Plaene, Querverweise | Cockpit, Ramp, Wiring, Suche |
| `copilot-models.json` | Modellkatalog fuer Runway/Engine/Planung | Runway, Tower, Cockpit, Suche |
| `governance-controls.json` | Admin-/Governance-Controls | Tower, Cockpit, Suche |
| `sovereign-cloud.json` | Residency- und Souveraenitaetsoptionen | Tower |
| `security-threats.json` | Threat Models und Schutzmassnahmen | Security, Cockpit |
| `security-frameworks.json` | Mapping zu OWASP/ATLAS/CWE | Security |
| `terminal-guide.json` | Einstieg und Lernpfad | Terminal |
| `jet-bridge-guide.json` | Prompting-, Kontext- und Agent-Patterns | Jet Bridge |
| `preflight-checklist.json` | Readiness-Checkliste | Pre-Flight |
| `known-changelog-entries.json` | Historie und Feature-Entwicklung | Flight Log, Suche |
| `wiring-diagram.json` | Verbindungen zwischen Instrumenten | Wiring |

## 3. Datenvertraege (Best Practice)

Jeder Katalog sollte mindestens diese Vertragselemente besitzen:

1. Eindeutige IDs
2. Pflichtfelder je Entitaet
3. Version/Stand oder Last-Verified-Metadaten
4. Referenzielle Integritaet fuer Cross-Links
5. Verifikationsstatus fuer unsichere Quellen

Empfehlung:

- Kritische Kataloge mit `verificationRequired` markieren
- Bei neuen Feldern immer Abwaertskompatibilitaet pruefen

## 4. Konsum-Matrix (Seite -> Daten)

| Perspektive/Seite | Gelesene Daten |
| --- | --- |
| Cockpit | Instrumente plus kontextuell Security/Governance/Modelle |
| Security | Instrumente, Threats, Framework-Mappings |
| Runway | Modelle |
| Tower | Controls, Modelle, Souveraenitaet |
| Ramp | Instrumente (gefiltert auf Ramp-Kontext) |
| Terminal | Terminal Guide |
| Jet Bridge | Jet Bridge Guide |
| Pre-Flight | Checklist |
| Flight Log | Changelog |
| Wiring | Wiring Graph + Instrumente |
| Global Search | Instrumente, Controls, Modelle, Changelog |

## 5. Datenqualitaetsrisiken

Haeufige Risiken in datengetriebenen Referenzsites:

1. Verwaiste Referenzen (IDs nicht mehr vorhanden)
2. Uneinheitliche Terminologie ueber Kataloge
3. Fehlende Verifikationsupdates bei externen Quellen
4. Inkonsistente Taxonomien bei Status/Plans/Types

## 6. Kontrollpunkte fuer Aenderungen

Bei jeder Datenaenderung:

1. Integritaetstest laufen lassen
2. Betroffene Perspektiven visuell pruefen
3. Cross-Link-Navigation testen
4. Falls relevant Changelog-Eintrag aktualisieren
5. Verifikationsstatus und Quellenhinweis mitpflegen

## 7. Pflegeprozess (empfohlen)

1. Change an Katalog vornehmen
2. Schema- und Integritaetspruefung
3. Perspektivenspezifische Regression
4. Reviewer-Freigabe mit Source-Check
5. Dokumentation des Aenderungsgrunds
