<!-- SPDX-FileCopyrightText: 2026 Alexander Plate -->
<!-- SPDX-License-Identifier: BUSL-1.1 -->

# AGENTS.md — ForgePort organization repository

Dieses öffentliche Repository enthält ausschließlich organisationsweite Community-,
Governance- und wiederverwendbare CI-Dateien für ForgePort.

## Verbindliche Grenzen

- Keine Geheimnisse, Zugangsdaten, privaten Schlüssel, Kundeninformationen,
  produktiven Lizenzen, internen Systeme, privaten Repositoryinhalte oder
  kundenspezifischen Angaben aufnehmen.
- `forgeport-int` und `forgeport-license-issuer` sind privat. Inhalte daraus
  dürfen nicht hierher kopiert werden. Der License-Issuer darf in CI niemals
  Produktivschlüssel oder reale Kundenlizenzen erzeugen.
- Keine Sichtbarkeit anderer Repositories ändern. API, UI, Squid, Dex und Helm
  dürfen erst nach dokumentierter History-, Secret-, Third-Party- und
  Lizenzprüfung öffentlich werden.
- Keine Rechts-, Zertifizierungs-, SLA-, Sicherheits- oder Konformitätsaussage
  erfinden. Geplante Kontrollen nicht als implementiert darstellen.
- Repositoryspezifische Buildlogik bleibt im jeweiligen Produkt-Repository.
  Wiederverwendbare Workflows orchestrieren nur klar definierte Inputs und
  Artefakte.
- Externe GitHub Actions müssen auf vollständige Commit-SHAs gepinnt sein.
  GitHub-Token erhalten jeweils nur die minimal benötigten Berechtigungen.
- Unvertrauenswürdiger PR-Code erhält niemals Secrets oder Schreibrechte.
  Kein `pull_request_target` zum Ausführen von PR-Code verwenden.
- Keine automatischen Merges. Releases benötigen geschützte Tags und die
  manuell freizugebende GitHub-Environment `release`.
- Release-Tags sind annotierte SSH-signierte Tags eines dedizierten
  Ed25519-Schlüssels. Der Private Key darf ausschließlich im geschützten
  Environment-Secret `FORGEPORT_RELEASE_SSH_PRIVATE_KEY` liegen; PRs und normale
  CI erhalten ihn nie. Zentrale Gates prüfen den Principal
  `forgeport-release` gegen commitgebundene öffentliche Trust-Evidenz.
- Renovate nicht einführen. Dependabot verwenden; Major-Updates separat halten.
- ForgePort-eigene Inhalte stehen unter BSL 1.1 mit Apache-2.0 als Change
  License. Drittanbieter-/Upstreammaterial bleibt unter seiner eigenen Lizenz
  und muss durch SPDX, Pfade und Notices eindeutig abgegrenzt werden.
- Die BSL-Lizenz enthält wörtlich die deterministische Change-Date-Regel
  `Four years from the date this version of the Licensed Work is first publicly
  available.` Releaseautomation verändert `LICENSE` niemals. Öffentliche
  Git-Historie, unveränderlicher Tag, GitHub-Release-Zeitpunkt und Provenance
  bilden die Veröffentlichungsevidenz; ausgelieferte Lizenzkopien sind
  bytegleich zur Lizenz des getaggten Quellstands.
- `Licensed Work` enthält ausschließlich den stabilen Produkt- oder
  Komponentennamen. Version, Datum und Releasezustand werden nur durch
  `VERSION`, Tag, Commit und Veröffentlichungsevidenz beschrieben.
- Historische Releases bleiben in der Git-Historie unverändert. Das ist keine
  Vorlage für neue Versionen; die wiederverwendbaren Release-Gates verlangen
  die deterministische Regel und einen konfigurierten stabilen Namen.
- Kommunikation erfolgt über Issues, Pull Requests und versionierte fachliche
  Dateien, nicht über eine gemeinsam gepflegte Statusdatei.

## Arbeitsweise

- Dokumentationssprache ist Deutsch; technische Bezeichner dürfen Englisch sein.
- Bestehende Historie und fremde Änderungen bewahren.
- Vor Lösch- oder Verschiebeaktionen exakte Ziele nennen und Freigabe einholen.
- Änderungen lokal linten und validieren. Nicht committen oder pushen, sofern
  dies nicht ausdrücklich beauftragt wurde.
