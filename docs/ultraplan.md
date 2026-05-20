# Ultraplan fuer die technische Dokumentation

## Ziel

Eine belastbare, produktzentrierte technische Dokumentation fuer Copilot Cockpit erstellen und in ralph-artigen Iterationen auf mindestens 90% Qualitaet bringen.

## Qualitaetsrubrik

Bewertungsskala je Kriterium: 0 bis 5

- 0: nicht vorhanden
- 1: rudimentaer
- 2: teilweise ausreichend
- 3: gut
- 4: sehr gut
- 5: best-practice-konform und nachweisbar

Gewichtung:

| Kriterium | Gewicht |
| --- | ---: |
| Vollstaendigkeit | 25% |
| Korrektheit | 25% |
| Nachvollziehbarkeit | 20% |
| Wartbarkeit | 15% |
| Testbarkeit/Verifizierbarkeit | 15% |

Formel:

`Gesamtscore = Summe((Punkte/5) * Gewicht)`

Harte Exit-Kriterien:

1. Gesamtscore >= 90%
2. Kein Kriterium unter 4/5
3. Vollstaendigkeit und Korrektheit jeweils mindestens 4.5/5

## Ralph-Zyklus

Jede Iteration folgt streng:

1. Plan
2. Draft
3. Review
4. Fix
5. Verify

Regeln:

1. Nach jeder Iteration Scorecard aktualisieren
2. Bei Score < 90% zwingend weitere Iteration
3. Pro Iteration Defizite priorisieren und gezielt beheben

## Phasenplan

### Phase 0: Scope und Governance

Deliverables:

- Dokumentationszielbild
- Kapitelverantwortung
- Bewertungsrubrik

Exit:

- Scope freigegeben
- Rubrik operationalisiert

### Phase 1: Produkt- und Architektur-Inventar

Deliverables:

- Capability- und Perspektivenmodell
- Komponenten- und Datenflussuebersicht
- Liste von Annahmen und Risiken

Exit:

- Kernfakten dokumentiert
- Informationsluecken markiert

### Phase 2: Struktur und Kapitelgerueste

Deliverables:

- README + docs Struktur
- Kapitel mit einheitlicher Struktur

Exit:

- Navigierbare Doku mit konsistenten Abschnittstypen

### Phase 3: Draft-Inhalt nach Best Practices

Deliverables:

- Architektur, Daten, Setup, Site Map, Testing
- Quellenhinweise und Betriebsregeln

Exit:

- Vollstaendiger Erstentwurf

### Phase 4: Ralph-Iterationen bis >=90%

Deliverables pro Runde:

- Reviewbefunde
- Fixpaket
- Verifikationsnachweis
- Aktualisierte Scorecard

Exit:

- Alle harten Exit-Kriterien erreicht

### Phase 5: Release und Pflege

Deliverables:

- Freigegebene Doku
- Pflegeprozess mit Review-Kadenz

Exit:

- Wartungsprozess aktiv

## Risiken und Gegenmassnahmen

| Risiko | Gegenmassnahme |
| --- | --- |
| Inkonsistente Begriffe | Zentrales Glossar und Terminologie-Regeln |
| Veraltete Inhalte | Review-Kadenz und Last-Reviewed-Pflicht |
| Fehlende Nachweise | Quellenpflicht fuer kritische Aussagen |
| Defekte Querverweise | Cross-Link Tests als Gate |

## Validierungsschritte

1. Fachreview der Kapitel
2. Architekturreview auf Konsistenz
3. Security-/Governance-Review fuer kritische Aussagen
4. Rubrikbasierte Endbewertung
5. Stichprobe Aussage -> Quelle -> Verantwortliche
