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
6. Release-Gate, OCI- und Release-Workflows mit der geschützten Environment
   `release` testen.
7. Rulesets erzwingen lassen: reviewter Versionsstand, Merge, geschützter Tag,
   Veröffentlichung und gegebenenfalls Public-Wechsel.
8. Erst dann je öffentlichem Kandidaten Prüfbericht und Owner-Freigabe einholen.

Beim leeren, bereits öffentlichen `.github`-Repository galt für den ersten
Commit die dokumentierte lokale Bootstrap-Ausnahme. Ein Review-Branch wäre
bereits eine Veröffentlichung gewesen.

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
BSL-Version wird pro veröffentlichtem Versionsstand reviewt. `LICENSE` enthält
die deterministische Vierjahresregel und wird im Releasebuild nicht verändert;
`Licensed Work` ist der stabile Komponentenname ohne Versions- oder
Datumszusatz. Keine Root-Lizenz relizenziert Drittmaterial.
