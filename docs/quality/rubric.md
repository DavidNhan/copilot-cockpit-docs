# Rubrik fuer Workbench-Qualitaet

## Skala

- 0: nicht vorhanden
- 1: rudimentaer
- 2: teilweise ausreichend
- 3: gut
- 4: sehr gut
- 5: best-practice-konform mit Evidenz

## Gewichtung und Gates

| Kriterium | Gewicht | Gate |
| --- | ---: | ---: |
| Vollstaendigkeit | 25 | >= 4.5 |
| Korrektheit | 25 | >= 4.5 |
| Nachvollziehbarkeit | 20 | >= 4.0 |
| Wartbarkeit | 15 | >= 4.0 |
| Verifizierbarkeit | 15 | >= 4.0 |

Formel:

`Gesamtscore (%) = Summe((Punkte / 5) * Gewicht)`

## Bewertungsanker

| Kriterium | Erwartung fuer 5/5 | Erwartete Evidenz |
| --- | --- | --- |
| Vollstaendigkeit | Alle Pflichtkapitel aus Workbench vorhanden, inklusive `Not Applicable`-Begruendungen | Kapitelabdeckung, Release-Paket, Header, Mermaid |
| Korrektheit | Aussagen sind mit Repo-, Config-, Test- oder Betriebsquellen belegbar | Dateipfade, Konfigurationen, Testbezug, Vorlagen-Mapping |
| Nachvollziehbarkeit | Leser kann vom Zweck ueber Architektur bis zur Verifikation logisch folgen | klare Querverweise, Datenfluesse, Traceability |
| Wartbarkeit | Struktur ist wiederverwendbar, stabil und fuer Folgedokumente adaptierbar | konsistente Kapitelreihenfolge, wiederverwendbare Tabellen, klare Terminologie |
| Verifizierbarkeit | Anforderungen und Aussagen koennen geprueft oder getestet werden | Akzeptanzkriterien, Teststrategie, Evidenz- und Quellenstand |

## Template-Fit

Eine hohe Bewertung setzt voraus, dass die Struktur sowohl die klassische SRS-Form aus `SoftwareRequirements.doc`
als auch die sectionspezifischen Betriebs- und Akzeptanzaspekte aus `System_Requirements_Template.docx` sichtbar abbildet.

## Exit

1. Gesamtscore >= 90
2. Alle Gates erreicht
3. Mermaid-Diagramme und Querverweise valide
