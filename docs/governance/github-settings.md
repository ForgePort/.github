<!-- SPDX-FileCopyrightText: 2026 Alexander Plate -->
<!-- SPDX-License-Identifier: BUSL-1.1 -->

# Benötigte GitHub-Einstellungen

Die folgenden Einstellungen sind Empfehlungen und nicht automatisch aktiv.

## Organisation und Pull Requests

- Basisberechtigung `read`; Sichtbarkeitsänderungen und Repositoryerstellung
  auf Owner beschränken.
- Standard-Workflowberechtigung `contents: read`; Actions dürfen keine Pull
  Requests erstellen oder freigeben.
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

Für Tags `v*`: Erstellung auf Release-Maintainer beschränken; Änderung und
Löschung blockieren. Nur `vMAJOR.MINOR.PATCH`, beginnend mit `v0.0.1`. Die
Environment `release` benötigt Required Reviewers und verbietet Self-Review.
Der dedizierte Ed25519-Private-Key liegt ausschließlich als Environment-Secret
`FORGEPORT_RELEASE_SSH_PRIVATE_KEY` in `release`, nie als allgemeines
Repository-Secret. Ein manuell ausgelöster, auf einen unveränderlichen zentralen
Workflow-SHA gepinnter Caller darf mit `contents: write` nur den aktuellen
reviewten Default-Branch-HEAD als neuen annotierten Tag signieren. PR- und
CI-Jobs erhalten dieses Secret nicht.

## Supply Chain und Release

- GHCR-Schreibzugriff nur im Releasejob; OIDC nur für Signatur und Provenance.
- Release-Tags sind annotiert und mit dem dedizierten SSH-/Ed25519-Schlüssel
  signiert. Die Gates prüfen sowohl `git verify-tag` gegen
  `forgeport-release` in der zentralen `release-trust/allowed_signers` des
  exakt gepinnten `.github`-Commits als auch GitHubs gültige Signaturevidence.
  Die Trust-Datei wird erst zusammen mit dem real geprüften Public Key
  veröffentlicht; Dummy-Schlüssel und Placeholder sind verboten.
- OCI-Verweise mit unveränderlichem Digest dokumentieren.
- SBOM, Third-Party-/Lizenzinventar, Notices und SHA-256-Prüfsummen beilegen.
- Jedes Releasepaket enthält eine mit der Quelle bytegleiche `LICENSE` und
  eine `VERSION`, die exakt dem Tag ohne `v` entspricht.
- Die BSL-Lizenz enthält die unveränderte deterministische Change-Date-Regel;
  keine Releaseautomation schreibt Veröffentlichungsdaten in `LICENSE`.
- Der `Licensed Work`-Parameter ist ein stabiler Komponentenname ohne Version,
  Datum oder Releasezustand. Aufrufer übergeben diesen Namen explizit an die
  wiederverwendbaren Release-Workflows.
- Öffentliche Git-Historie, unveränderlicher Tag und der
  GitHub-Release-Publikationszeitpunkt sind die Datumsevidenz. Provenance bindet
  den getaggten Commit, Artefakte und den Hash der ausgelieferten Lizenz.
- Sigstore/Cosign-Signaturen und registrygebundene SLSA-Provenance als portable
  Basis nutzen. GitHub Artifact Attestations nur zusätzlich aktivieren, wenn
  sie für Repositorysichtbarkeit und Tarif verfügbar sind.
- Rulesets und Maintainerprozess müssen die Kette erzwingen:
  reviewte Source-Änderung, Merge, geschützter unveränderlicher Tag und erst
  danach Package/GHCR/GitHub Release oder Public-Sichtbarkeitswechsel.
- Für vorgebaute OCI-Eingaben akzeptiert `reusable-oci.yml` nur einen exakt
  benannten Artifact-Upload desselben Tag-Workflowlaufs. Zielpfad und jede
  enthaltene Datei werden explizit angegeben; `trusted-artifact-sha256` ist der
  SHA-256-Wert des lexikografisch sortierten Manifests aus Datei-SHA-256, zwei
  Leerzeichen und relativem POSIX-Pfad. Fremde Runs, abweichende Commits,
  Traversal, Symlinks und unerwartete Dateien scheitern.

## Public Readiness

`forgeport-api`, `forgeport-ui`, `forgeport-squid`, `forgeport-dex` und
`forgeport-helm` sind öffentliche Kandidaten erst nach Prüfung der gesamten
Historie, Secrets, Drittanbieterquellen, Lizenzen/Notices, großen Dateien,
Kunden-/Personendaten und Workflows. `forgeport-int` und
`forgeport-license-issuer` bleiben privat. Repository-Root-BSL darf Squid
(GPL-2.0-or-later), Dex-/Proto-abgeleitete Inhalte (anwendbares Apache-2.0) oder
anderes Upstreammaterial nicht fälschlich erfassen. Dies ist keine rechtliche
Freigabe.

Beim einmaligen Bootstrap eines leeren öffentlichen Repositories muss ein
anderer Maintainer den vollständigen Kandidaten und exakten Tree prüfen, bevor
der Owner den direkten initialen `main`-Push freigibt. Ein vorab veröffentlichter
Review-Branch ist keine private Prüffläche. `LICENSE` bleibt auch beim Bootstrap
unverändert; der erfolgreiche öffentliche Git-Push ist Teil der Evidenz.
