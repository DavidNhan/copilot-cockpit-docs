# Quality Scorecard (Ralph Iterationen)

## Bewertungsmodell

Gewichtete Kriterien:

- Vollstaendigkeit: 25%
- Korrektheit: 25%
- Nachvollziehbarkeit: 20%
- Wartbarkeit: 15%
- Testbarkeit/Verifizierbarkeit: 15%

Formel: `(Punkte/5) * Gewicht`

## Iteration 1

Review-Fokus:

- Kapitelkonsistenz
- Quellenorientierung
- Trennung von Produktsicht und lokalen Pfaden

Scoring:

| Kriterium | Punkte | Gewicht | Ergebnis |
| --- | ---: | ---: | ---: |
| Vollstaendigkeit | 4.3 | 25 | 21.5 |
| Korrektheit | 4.4 | 25 | 22.0 |
| Nachvollziehbarkeit | 4.2 | 20 | 16.8 |
| Wartbarkeit | 4.5 | 15 | 13.5 |
| Testbarkeit/Verifizierbarkeit | 4.3 | 15 | 12.9 |
| Gesamt |  | 100 | 86.7 |

Defizite:

1. Qualitaetsprozess fehlte als eigenes Artefakt
2. Setup-/Release-Gates waren nicht explizit genug
3. Site-Map brauchte klarere Navigationsprinzipien

Fixpaket:

1. `docs/ultraplan.md` ergaenzt
2. `docs/setup.md` um Release-Gates erweitert
3. `docs/site-map.md` um Navigations- und Brueckenlogik geschaerft

## Iteration 2

Review-Fokus:

- Rubrik-Konformitaet
- End-to-End Lesbarkeit
- Umsetzbarkeit als Teamdokument

Scoring:

| Kriterium | Punkte | Gewicht | Ergebnis |
| --- | ---: | ---: | ---: |
| Vollstaendigkeit | 4.6 | 25 | 23.0 |
| Korrektheit | 4.6 | 25 | 23.0 |
| Nachvollziehbarkeit | 4.5 | 20 | 18.0 |
| Wartbarkeit | 4.7 | 15 | 14.1 |
| Testbarkeit/Verifizierbarkeit | 4.6 | 15 | 13.8 |
| Gesamt |  | 100 | 91.9 |

Ergebnis:

- Ziel >=90% erreicht
- Kein Kriterium unter 4/5
- Vollstaendigkeit und Korrektheit >= 4.5/5 erreicht

## Abschlussvermerk

Die Doku erfuellt die definierten Qualitaetsanforderungen fuer den aktuellen Scope. Weitere Iterationen sind optional und vor allem bei groesseren Produktaenderungen sinnvoll.
