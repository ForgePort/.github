<!-- SPDX-FileCopyrightText: 2026 Alexander Plate -->
<!-- SPDX-License-Identifier: BUSL-1.1 -->

# Benötigte GitHub-Einstellungen

Die folgenden Einstellungen sind Empfehlungen und nicht automatisch aktiv.

## Organisation und Pull Requests

- Basisberechtigung `read`; Sichtbarkeitsänderungen und Repositoryerstellung
  auf Owner beschränken.
- Standard-Workflowberechtigung `contents: read`; Actions dürfen keine Pull
  Requests erstellen oder freigeben, ausgenommen der eigens autorisierte
  Prepare-Release-Workflow.
- Die Repositoryoption zum Erstellen von Pull Requests durch Actions muss für
  den Prepare-Workflow aktiviert werden. Nur dessen geschützter Job erhält
  `contents: write` und `pull-requests: write`; Reviews durch Actions bleiben
  unzulässig.
- Externe Fork-PR-Workflows benötigen Maintainer-Freigabe. Fork-Code erhält
  keine Secrets und keine Schreibrechte. Kein `pull_request_target` führt
  unvertrauenswürdigen Code aus.
- Nur GitHub-eigene und explizit freigegebene Actions zulassen und vollständige
  SHA-Pins erzwingen, soweit tariflich verfügbar.
- Dependabot, Dependency Graph, Security Updates, Private Vulnerability
  Reporting, Secret Scanning, Push Protection und Code Scanning passend zum
  Repository und Tarif aktivieren. Kein Auto-Merge.

## Rulesets

Für `main`: Pull Request, Code-Owner-Review, erneute Freigabe nach neuen
Commits, aufgelöste Diskussionen, aktuelle Branchbasis und erforderliche
Statuschecks verlangen; Force Push und Löschung blockieren. Für
sicherheits-/releasekritische Repositories zwei Freigaben empfehlen.

Für Tags `v*`: Erstellung, Änderung und Löschung auf Release-Maintainer
beschränken. Nur `vMAJOR.MINOR.PATCH`, beginnend mit `v0.0.1`. Die
Environment `release` benötigt Required Reviewers und verbietet Self-Review.
Die Environment `release-preparation` schützt den manuellen Prepare-Schritt.

## Supply Chain und Release

- GHCR-Schreibzugriff nur im Releasejob; OIDC nur für Signatur und Provenance.
- OCI-Verweise mit unveränderlichem Digest dokumentieren.
- SBOM, Third-Party-/Lizenzinventar, Notices und SHA-256-Prüfsummen beilegen.
- Jedes Releasepaket enthält eine mit der Quelle bytegleiche `LICENSE` und
  eine `VERSION`, die exakt dem Tag ohne `v` entspricht.
- Sigstore/Cosign-Signaturen und registrygebundene SLSA-Provenance als portable
  Basis nutzen. GitHub Artifact Attestations nur zusätzlich aktivieren, wenn
  sie für Repositorysichtbarkeit und Tarif verfügbar sind.
- Releases und Publish-Jobs scheitern bei den zentral festgelegten
  unreleased BSL-Datumsmarkern oder der festgelegten
  Unreleased-Kennzeichnung.
- Prepare Release erhält Version und geplantes Erstveröffentlichungsdatum,
  berechnet +4 Kalenderjahre und eröffnet einen reviewpflichtigen PR. Der
  eigentliche Releasebuild ändert `LICENSE` nie.
- Rulesets und Maintainerprozess müssen die Kette erzwingen:
  autorisierter manueller `workflow_dispatch`, Prepare-PR, unabhängiges Review,
  Merge, geschützter Tag und erst danach Package/GHCR/GitHub Release oder
  Public-Sichtbarkeitswechsel. Eine Datumsverschiebung verlangt PR-Aktualisierung
  und erneutes Review.

## Public Readiness

`forgeport-api`, `forgeport-ui`, `forgeport-squid`, `forgeport-dex` und
`forgeport-helm` sind öffentliche Kandidaten erst nach Prüfung der gesamten
Historie, Secrets, Drittanbieterquellen, Lizenzen/Notices, großen Dateien,
Kunden-/Personendaten und Workflows. `forgeport-int` und
`forgeport-license-issuer` bleiben privat. Repository-Root-BSL darf Squid
(GPL-2.0-or-later), Dex-/Proto-abgeleitete Inhalte (anwendbares Apache-2.0) oder
anderes Upstreammaterial nicht fälschlich erfassen. Dies ist keine rechtliche
Freigabe.

Das leere, bereits öffentliche Organisations-Repository benötigt beim ersten
inhaltlichen Push einen Bootstrap: Die BSL-Daten müssen unmittelbar vorher im
lokalen, geprüften Kandidaten manuell mit dem tatsächlichen Veröffentlichungstag
parametrisiert und separat freigegeben werden, weil der Prepare-Workflow vor dem
ersten Commit noch nicht auf dem Defaultbranch existiert.

Ein Review-Branch ist für diesen Bootstrap unzulässig, weil bereits dessen Push
die erste öffentliche Veröffentlichung wäre. Einmalig wird Prepare Release rein
lokal mit dem ausdrücklich geplanten tatsächlichen Pushdatum ausgeführt. Ein
anderer Maintainer prüft die vollständige staged Dateiliste sowie den exakten
Tree- und Commit-Hash. Erst nach separater Ownerfreigabe wird exakt dieser
Kandidat direkt als initialer `main`-Commit gepusht – ohne gleichzeitigen Tag,
GitHub Release, Package oder OCI-Publish. Danach sind Rulesets und Environments
sofort zu konfigurieren; alle Folgeänderungen laufen über Review-PRs. Verschiebt
sich der Push auf einen anderen Kalendertag oder schlägt er fehl, werden
First-Publication- und Change-Date erneut erzeugt und der vollständige Kandidat
erneut getestet und reviewt.
