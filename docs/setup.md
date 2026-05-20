# Setup, Betrieb und Release

## Zweck

Dieses Dokument beschreibt den Betriebsweg fuer Copilot Cockpit: lokale Ausfuehrung, Testausfuehrung, Deployment und sichere Aenderungsdurchfuehrung.

## 1. Voraussetzungen

- Node.js + npm fuer Test- und Tooling-Befehle
- Python 3 fuer den lokalen statischen Server im Testpfad
- Chromium (Playwright Browser) fuer E2E-Verifikation

Hinweis:

- Direkter Aufruf per file:// ist ungeeignet, da Inhalte per fetch geladen werden.

## 2. Lokaler Schnellstart

```bash
npm install
npx playwright install chromium
```

Laufoptionen:

1. Statischer Schnelllauf

```bash
npx serve .
```

2. Testgetriebener Lauf (inkl. lokalem Webserver)

```bash
npm test
```

## 3. Betriebsmodell

Copilot Cockpit wird als statische Site betrieben.

Wichtige Eigenschaften:

- Kein klassischer Build-Step erforderlich
- HTML/CSS/JS/JSON werden direkt ausgeliefert
- Caching wird ueber Hosting-Konfiguration gesteuert

## 4. Deployment-Grundsaetze

1. Vor Deployment immer Tests ausfuehren
2. Datenaenderungen als risikoreich behandeln (Integritaet + Perspektiven pruefen)
3. Rollout erst nach dokumentierter Review-Freigabe
4. Bei kritischen Inhalten Quelle und Verifikationsstatus mitliefern

## 5. Change-Workflow (Best Practice)

1. Issue oder Change Request definieren
2. Betroffene Perspektiven und Datenkataloge bestimmen
3. Implementierung in kleinen, nachvollziehbaren Schritten
4. Lokale Testausfuehrung inkl. Integritaetschecks
5. Reviewer-Check auf fachliche Korrektheit und Cross-Linking
6. Merge und Release

## 6. Betriebskritische Checks vor Merge

- Seite bootet ohne Scriptfehler
- Navigation zwischen Perspektiven funktioniert
- Deep-Links oeffnen korrekte Details
- Suchpalette liefert erwartete Treffer
- Theme/UIs in zentralen Seiten stabil

## 7. Notfall- und Rueckfallstrategie

Empfehlungen:

1. Letzten stabilen Release-Stand markieren
2. Datenhotfixes getrennt von grossen UI-Refactorings halten
3. Bei regressiven Navigationseffekten sofort Rollback ermoeglichen
4. Incident kurz dokumentieren und Testluecke nachziehen
