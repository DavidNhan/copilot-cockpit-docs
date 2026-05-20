# Testing und Verifikation

## Zweck

Dieses Dokument beschreibt die Qualitaetssicherungsstrategie fuer Copilot Cockpit mit Fokus auf Regression, Datenintegritaet und fachliche Navigationsketten.

## 1. Testpyramide fuer dieses Produkt

Copilot Cockpit ist datengetrieben und statisch ausgeliefert. Daher ist die praktische Prioritaet:

1. E2E-Verhalten im Browser
2. Datenvertrags- und Integritaetspruefungen
3. Gezielt manuelle visuelle Checks bei Layout-/Diagrammrisiken

## 2. Automatisierter Teststack

- Framework: Playwright
- Browser: Chromium
- Scope: Perspektivenseiten + Integritaetspruefungen
- Umfang laut Projektbeschreibung: 222 Tests in 11 Spec-Dateien

## 3. Testdomaenen

| Domaene | Fokus |
| --- | --- |
| Seiten-Boot | Start ohne Laufzeitfehler |
| Rendering | Sichtbare und korrekte Kernobjekte |
| Interaktion | Filter, Details, Tabs, Suchfluesse |
| Navigation | Deep-Links und Perspektivenuebergaenge |
| Persistenz | Browserstate wie Theme/Checklist |
| Datenintegritaet | IDs, Referenzen, Pflichtfelder, Typen |

## 4. Release-Gates (empfohlen)

Ein Release sollte nur passieren, wenn:

1. Alle relevanten automatisierten Suites gruen sind
2. Betroffene Cross-Perspective-Pfade erfolgreich getestet sind
3. Integritaetstests fuer geaenderte Kataloge ohne Fehler durchlaufen
4. Keine offenen Major-Defects in Security/Governance/Navigation bestehen

## 5. Risikoorientierte Testauswahl

| Aenderungstyp | Mindesttestumfang |
| --- | --- |
| Neue Instrumente/Modelle | Cockpit/Runway/Tower plus Integritaet |
| Security-Kataloge | Security plus Integritaet |
| Governance/Residency | Tower plus Integritaet |
| Wiring/Graph-Logik | Wiring plus Integritaet |
| Navigation/Suche | Cockpit, Flight Log, Cross-Link-Stichprobe |

## 6. Manuelle Verifikation (ergaenzend)

Automatisierte Tests sind notwendig, aber nicht hinreichend. Ergaenzende Checks:

1. Mermaid-Diagramme korrekt gerendert
2. Kritische Seiten in mindestens zwei typischen Viewport-Groessen geprueft
3. Fachliche Terminologie ueber Perspektiven konsistent
4. Changelog-Links verweisen auf erwartbare Ziele

## 7. Qualitaetsmetriken fuer Testgesundheit

- Pass-Rate je Pipeline-Lauf
- Anzahl regressiver Defects pro Release
- Mean time to fix fuer kritische Defects
- Anteil geaenderter Kataloge mit Integritaetspruefung

## 8. Testluecken aktiv schliessen

Wenn Fehler ausserhalb bestehender Tests auftreten, sollte unmittelbar folgen:

1. Reproduktion dokumentieren
2. Fehlenden Test ergaenzen
3. Fix implementieren
4. Regression bestaetigen
