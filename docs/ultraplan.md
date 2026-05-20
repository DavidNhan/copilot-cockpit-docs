# Ultraplan fuer User Docs und Technical Docs

## Ziel

Eine belastbare Dokumentation fuer Copilot Cockpit erstellen, aufgeteilt in:

- User Docs (Nutzung, Navigation, Workflows)
- Technical Docs (Architektur, Betrieb, Qualitaet, Governance)

Beide Spuren werden in ralph-artigen Iterationen auf mindestens 90% Qualitaet gebracht.

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

Zusatzregel fuer Dual-Track-Doku:

1. User Docs und Technical Docs muessen jeweils klar abgegrenzt sein.
2. Jede Hauptfrage muss einem Track zuordenbar sein.
3. Die Navigation zwischen beiden Tracks muss explizit dokumentiert sein.

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

Ralph-Reviewfokus je Track:

1. User Docs: Verstaendlichkeit, Aufgabenorientierung, schnelle Orientierung
2. Technical Docs: technische Tiefe, Betriebsfaehigkeit, Nachweisbarkeit

## Phasenplan

### Phase 0: Scope und Governance

Deliverables:

- Dokumentationszielbild fuer beide Tracks
- Kapitelverantwortung
- Bewertungsrubrik

Exit:

- Scope freigegeben
- Rubrik operationalisiert

### Phase 1: Produkt- und Architektur-Inventar

Deliverables:

- Capability- und Perspektivenmodell (User-Sicht)
- Komponenten- und Datenflussuebersicht (Technical-Sicht)
- Liste von Annahmen und Risiken

Exit:

- Kernfakten dokumentiert
- Informationsluecken markiert

### Phase 2: Struktur und Kapitelgerueste

Deliverables:

- README + docs Struktur mit klarer Trennung von User Docs und Technical Docs
- Kapitel mit einheitlicher Struktur

Exit:

- Navigierbare Doku mit konsistenten Abschnittstypen

### Phase 3: Draft-Inhalt nach Best Practices

Deliverables:

- User Docs: Einstieg, Navigation, Workflows, FAQ
- Technical Docs: Architektur, Daten, Integrationen, Security, Operations, Quality
- Quellenhinweise und Betriebsregeln fuer beide Tracks

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
| Vermischung der Zielgruppen | Klare Trennung in User Docs und Technical Docs |

## Validierungsschritte

1. Fachreview der Kapitel
2. Architekturreview auf Konsistenz
3. Security-/Governance-Review fuer kritische Aussagen
4. Rubrikbasierte Endbewertung
5. Stichprobe Aussage -> Quelle -> Verantwortliche
6. Track-Check: Jede Seite ist eindeutig User Docs oder Technical Docs zugeordnet
