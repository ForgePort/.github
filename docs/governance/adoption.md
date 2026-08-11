<!-- SPDX-FileCopyrightText: 2026 Alexander Plate -->
<!-- SPDX-License-Identifier: BUSL-1.1 -->

# Empfohlene Einführung

1. Repositoryeigene Build-, Test- und Lintlogik stabilisieren.
   Dabei eine getrackte, public-safe `AGENTS.md` aus der Organisationsvorlage
   aufnehmen; keine internen Koordinationsdetails übertragen.
2. BSL-Geltungsbereich, SPDX, Third-Party-/Lizenzinventar und Notices prüfen.
3. Vollständige History-, Secret- und Vulnerability-Scans auswerten.
4. Quality-, Dependency- und Security-Workflows zunächst beobachtend einführen.
5. Checks nach erfolgreicher Erprobung im Ruleset verpflichtend machen.
6. Prepare-Release und Release mit geschützten Environments testen.
7. Rulesets erzwingen lassen: manueller Dispatch, reviewpflichtiger Prepare-PR,
   Merge, geschützter Tag, Veröffentlichung und gegebenenfalls Public-Wechsel.
8. Erst dann je öffentlichem Kandidaten Prüfbericht und Owner-Freigabe einholen.

Beim leeren, bereits öffentlichen `.github`-Repository gilt für den ersten
Commit die dokumentierte lokale Bootstrap-Ausnahme. Weder ein Review-Branch
noch ein unreleased Platzhalter darf vorab gepusht werden.

| Repository | Einführungsschwerpunkt |
|---|---|
| `forgeport-api` | Maven, OpenAPI, Security, OCI, Release |
| `forgeport-ui` | npm, Accessibility, Asset-Budgets, OCI, Release |
| `forgeport-squid` | Go, Squid, Container, GPL-/Source-Abgrenzung |
| `forgeport-dex` | Go-Controller, Dex-/Proto-Apache-2.0-Notices |
| `forgeport-helm` | Helm lint/template/schema, Digest-Policy, Chart-Release |
| `forgeport-int` | Privat; keine internen Inhalte öffentlich übernehmen |
| `forgeport-license-issuer` | Privat; nur synthetisches CI-Testmaterial |

Aufrufer pinnen wiederverwendbare Workflows auf einen Commit-SHA. Die konkrete
BSL-Version und Datumsparameter werden pro veröffentlichtem Versionsstand
reviewt; keine Root-Lizenz relizenziert Drittmaterial.
