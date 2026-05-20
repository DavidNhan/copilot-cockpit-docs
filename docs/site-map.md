# Site Map und Informationsarchitektur

## Zweck

Dieses Dokument beschreibt die inhaltliche Informationsarchitektur von Copilot Cockpit und die Beziehungen zwischen den Perspektiven.

## 1. Journey-Modell

Die Seite folgt einer Flughafen-Metapher mit Lern- und Betriebsreise:

1. Terminal (Einstieg)
2. Jet Bridge (Arbeitsweise)
3. Ramp (Agenten und Tooling)
4. Cockpit (zentrale Feature-Landkarte)
5. Runway (Modelle)
6. Tower (Governance)
7. Security (Risiken und Gegenmassnahmen)

Utility-Ebenen:

- Flight Log (Historie)
- Pre-Flight (Readiness)
- Wiring (Verbindungsgraph)

## 2. Seitenverantwortung je Perspektive

| Perspektive | Primafrage | Haupteinheit |
| --- | --- | --- |
| Terminal | Wie starte ich? | Onboarding und Setup |
| Jet Bridge | Wie arbeite ich effektiv? | Prompting/Kontext/Edit-Patterns |
| Ramp | Wie orchestriere ich Agenten und Integrationen? | Operatives Tooling |
| Cockpit | Welche Features gibt es und wie haengen sie zusammen? | Instrumentraster + Detailansicht |
| Runway | Welches Modell passt zu welchem Zweck? | Modellkatalog + Topologie |
| Tower | Welche Controls regeln Betrieb und Compliance? | Governance-Controls |
| Security | Welche Risiken bestehen und wie mitigieren wir sie? | Threat/Countermeasure-Mapping |
| Flight Log | Was hat sich geaendert? | Changelog/Timeline |
| Pre-Flight | Sind wir rollout-bereit? | Checkliste |
| Wiring | Wie sind Features technisch/fachlich verdrahtet? | Verbindungsdiagramm |

## 3. Navigationsprinzipien

1. Perspektivenspezifische Tiefe statt ueberfrachteter Einzelseite
2. Deep-Linking fuer direkte Einstiege in relevante Details
3. Cross-Links fuer fachliche Uebergaenge zwischen Security/Governance/Modelle
4. Global Search als Abkuerzung ueber mehrere Kataloge

## 4. Kritische Bruecken

| Quelle | Ziel | Fachlicher Zweck |
| --- | --- | --- |
| Cockpit | Security | Risikovertiefung pro Feature |
| Cockpit | Tower | Steuerungs- und Compliance-Kontext |
| Cockpit | Runway | Modellbezug eines Features |
| Flight Log | Cockpit | Ruecksprung auf geaenderte Instrumente |
| Wiring | Cockpit | Graph -> Detailkontext |

## 5. UX-Risiken und Gegenmassnahmen

Risiken:

1. Informationssilos pro Perspektive
2. Inkonsistente Terminologie zwischen Seiten
3. Defekte Deep-Links

Gegenmassnahmen:

1. Einheitliches Glossar und zentrale Taxonomien
2. Verbindliche Cross-Link-Tests
3. Changelog-Pflicht bei Perspektivenerweiterungen
