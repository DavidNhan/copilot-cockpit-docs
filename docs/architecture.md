# Architektur

## Zweck

Dieses Dokument beschreibt die technische Architektur von Copilot Cockpit auf Produktebene: Komponenten, Datenfluesse, Integrationen und Betriebsgrenzen.

## 1. Architektur-Kern

Copilot Cockpit ist eine statische, datengetriebene Multi-Page-Webanwendung.

Architekturprinzip:

- Inhalt in JSON-Katalogen
- Rendering im Browser per Vanilla JavaScript
- Darstellung per HTML/CSS und eingebundenen Browser-Bibliotheken
- Navigation und Deep-Linking ueber URL-Hashes

Es gibt kein API-Backend als Pflichtkomponente fuer den Regelbetrieb der Site.

## 2. Komponentenmodell

### 2.1 Laufzeitkomponenten

| Komponente | Rolle | Notizen |
| --- | --- | --- |
| Multi-Page Frontend | Perspektivenspezifische Seiten (Terminal, Security, Runway, Tower usw.) | Jede Seite hat klaren Fachfokus |
| Cockpit Engine | Zentrale Interaktionslogik auf der Hauptseite | Rendering von Zonen, Instrumenten, Detailansicht |
| Globale Suche | Seitenuebergreifender Suchindex | Aggregiert Instrumente, Modelle, Controls, Changelog |
| Datenkataloge | Fachliche Quelle fuer nahezu alle Inhalte | JSON unter data/ |
| Visualisierung | Mermaid-Diagramme und Code-Highlighting | Vor allem fuer Topologie und Security-Kontext |

### 2.2 Betriebskomponenten

| Komponente | Rolle |
| --- | --- |
| Statisches Hosting (Vercel) | Auslieferung von HTML/CSS/JS/JSON |
| Playwright Test-Layer | Browserbasierte Regression und Integritaet |
| Enrichment Tooling | Pflege von Modellinformationen ausserhalb der Laufzeit |

## 3. Daten- und Kontrollfluss

### 3.1 Initialisierung

1. Nutzer oeffnet eine Perspektivenseite.
2. Seite laedt einen oder mehrere JSON-Kataloge.
3. JS rendert Karten, Tabellen, Detailansichten, Diagramme.
4. Hash und lokale Browserdaten steuern Fokuszustand.

### 3.2 Cross-Perspective Navigation

Copilot Cockpit verbindet Perspektiven gezielt:

- Cockpit -> Security fuer Threat/Control-Vertiefung
- Cockpit -> Tower fuer Governance-Vertiefung
- Cockpit -> Runway fuer Modell- und Engine-Kontext
- Flight Log/Wiring -> Cockpit fuer Ruecksprung auf Instrumente

Diese Bruecken sind ein zentrales Architekturmerkmal und Teil der Regressionstests.

## 4. Zustandsmanagement

Zustand bleibt bewusst im Browser (ohne serverseitige Session):

- Theme-Persistenz
- letzte Scanner-/Filterpositionen auf einzelnen Seiten
- Fortschritt in Onboarding-Checklisten

Das reduziert Komplexitaet und passt zum statischen Liefermodell.

## 5. Sicherheits- und Governance-Sicht

Die Architektur trennt Fachperspektiven statt Logik in eine einzige monolithische Seite zu druecken:

- Security-Perspektive: Threat Models, Countermeasures, Framework-Mapping
- Tower-Perspektive: Controls, Compliance, Data Residency, Souveraenitaet

Durch diese Trennung bleibt die UX fokussiert und die Pflege der Kataloge beherrschbar.

## 6. Qualitaetsattribute

| Attribut | Auspraegung |
| --- | --- |
| Wartbarkeit | Hoch durch datengetriebenes Modell und klare Seitensemantik |
| Erweiterbarkeit | Neue Inhalte primar als Datenaenderung moeglich |
| Nachvollziehbarkeit | Perspektiven und Querverweise sind explizit modelliert |
| Testbarkeit | E2E + Integritaetstests auf UI- und Datenebene |
| Betriebsaufwand | Niedrig durch statisches Hosting |

## 7. Bekannte Trade-offs

- Vorteil: Kein Build-Stack, schnelle Iteration, geringer Runtime-Overhead
- Nachteil: Weniger technische Leitplanken als bei typisierten Framework-Stacks
- Risiko: Datenqualitaet wird zum primaeren Stabilitaetsfaktor

## 8. Architektur-Governance (Empfehlung)

Fuer nachhaltige Pflege:

1. Architekturentscheidungen als ADR erfassen
2. Bei neuen Perspektiven immer Datenvertrag + Testfall anlegen
3. Cross-Links als verpflichtenden Abnahmepunkt behandeln
4. Quellen und Verifikationsstatus pro Datenkatalog dokumentieren
