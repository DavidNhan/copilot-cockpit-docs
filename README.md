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

- `docs/index.md`: Einstieg mit Aufteilung in User Docs und Technical Docs

User Docs:

- `docs/user-docs/index.md`
- `docs/user-docs/getting-started.md`
- `docs/user-docs/navigation-and-workflows.md`
- `docs/user-docs/faq.md`

Technical Docs:

- `docs/technical-docs/index.md`
- `docs/technical-docs/architecture-at-a-glance.md`
- `docs/01-product-overview.md`
- `docs/02-architecture-context.md`
- `docs/03-component-architecture.md`
- `docs/04-data-flows.md`
- `docs/05-integrations-and-apis.md`
- `docs/06-security-and-compliance.md`
- `docs/07-deployment-and-operations.md`
- `docs/08-observability-and-sre.md`
- `docs/09-testing-and-quality.md`
- `docs/10-risk-assumptions-and-decisions.md`
- `docs/11-runbooks-and-troubleshooting.md`
- `docs/12-glossary.md`

Governance und Qualitaet:

- `docs/ultraplan.md`
- `docs/changelog.md`
- `docs/quality/*`
- `docs/adr/*`
- `docs/templates/*`

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
