# Copilot Cockpit - Technische Dokumentation

Diese Doku beschreibt die Plattform Copilot Cockpit (https://copilot-cockpit.com/) und das oeffentliche Referenz-Repository (https://github.com/TheTrustedAdvisor/copilot-cockpit) nach Best Practices.

Ziel ist eine produkt- und architekturzentrierte Dokumentation mit klarer Nachvollziehbarkeit, statt einer lokalpfad-gebundenen Dateibeschreibung.

## Zielbild

Copilot Cockpit ist eine interaktive Referenz fuer GitHub Copilot, die Features in einer Luftfahrt-Cockpit-Metapher organisiert.

Wesentliche Eigenschaften:

- Statische Multi-Page-Webanwendung ohne klassischen Build-Step
- Datengetriebenes Rendering aus JSON-Katalogen
- Perspektivenmodell von Onboarding bis Governance und Security
- Browserbasierte End-to-End-Qualitaetssicherung mit Playwright

## Dokumentationsstruktur

- `docs/index.md`: Einstieg und Lesereihenfolge
- `docs/01-product-overview.md`: Produktzweck, Scope, Zielgruppen, Perspektiven
- `docs/02-architecture-context.md`: Systemkontext und Betriebsgrenzen
- `docs/03-component-architecture.md`: Komponenten, Verantwortung, Abhaengigkeiten
- `docs/04-data-flows.md`: Datenfluesse, Zustandsmodell, Integritaetsanforderungen
- `docs/05-integrations-and-apis.md`: Integrationen, externe Bibliotheken, Schnittstellen
- `docs/06-security-and-compliance.md`: Security-Modell und Governance-Aspekte
- `docs/07-deployment-and-operations.md`: Deployment-, Change- und Betriebsprozess
- `docs/08-observability-and-sre.md`: Monitoring, SLO/SLI, Incident-Muster
- `docs/09-testing-and-quality.md`: Teststrategie und Quality Gates
- `docs/10-risk-assumptions-and-decisions.md`: Risiken, Annahmen, ADR-Index
- `docs/11-runbooks-and-troubleshooting.md`: Runbooks fuer Stoerungen und Recovery
- `docs/12-glossary.md`: Einheitliche Begriffe und Abkuerzungen
- `docs/ultraplan.md`: Umsetzungs- und Qualitaetsplan (ralph-Zyklen, Exit-Kriterien)
- `docs/changelog.md`: Doku-Aenderungsprotokoll
- `docs/quality/*`: Rubrik, Scorecard, Iterationslog, Traceability
- `docs/adr/*`: Architecture Decision Records
- `docs/templates/*`: Vorlagen fuer Kapitel, Reviews, Verifikation

## Scope und Nicht-Scope

In Scope:

- Produktarchitektur und Seitenmodell
- Datenquellen und Verifikationsstatus
- Test- und Betriebskonzepte
- Nachvollziehbare Wartungs- und Review-Regeln

Nicht in Scope:

- Interne, nicht oeffentliche Roadmap
- Proprietaere Betriebskennzahlen ohne oeffentliche Quelle

## Quellenbasis

- Produktseite: https://copilot-cockpit.com/
- Repository und README: https://github.com/TheTrustedAdvisor/copilot-cockpit

## Qualitaetsanspruch

Die Doku wird nach einer gewichteten Rubrik bewertet (Vollstaendigkeit, Korrektheit, Nachvollziehbarkeit, Wartbarkeit, Testbarkeit) und iterativ verbessert, bis >=90% Gesamtqualitaet erreicht sind.

## Empfohlene Lesereihenfolge

1. `docs/index.md`
2. `docs/01-product-overview.md`
3. `docs/02-architecture-context.md`
4. `docs/03-component-architecture.md`
5. `docs/04-data-flows.md`
6. `docs/06-security-and-compliance.md`
7. `docs/07-deployment-and-operations.md`
8. `docs/09-testing-and-quality.md`
