<!-- SPDX-FileCopyrightText: 2026 Alexander Plate -->
<!-- SPDX-License-Identifier: BUSL-1.1 -->

# Zu ForgePort beitragen

Danke für dein Interesse an ForgePort. Nutze für Fehler und Vorschläge zuerst
das passende Issue-Template im betroffenen Repository. Sicherheitslücken gehören
nicht in öffentliche Issues; siehe [SECURITY.md](SECURITY.md).

## Beiträge vorbereiten

1. Beschreibe Problem, Ziel und betroffene Komponente nachvollziehbar.
2. Halte Änderungen klein und repositoryspezifisch. Kopple unabhängige
   Microservices nicht über Datenbanken oder interne Implementierungsdetails.
3. Ergänze Tests, Dokumentation, Drittanbieter- und Lizenznachweise, soweit die
   Änderung sie berührt.
4. Verwende keine Geheimnisse, echten Kundendaten oder produktiven Lizenzen in
   Code, Tests, Issues oder Logs.
5. Akzeptiere den Verhaltenskodex und fülle die Pull-Request-Vorlage aus.

Jedes öffentliche ForgePort-Quellrepository enthält eine kleine, getrackte und
öffentlich unbedenkliche `AGENTS.md`. Verwende die
[Organisationsvorlage](docs/governance/public-repository-AGENTS.template.md)
und konkretisiere nur Zuständigkeit sowie echte Build-/Testbefehle. Interne
Issues, Task-IDs, Hosts, Kunden-, Credential- oder Geschäftsdetails gehören
nicht hinein. Die Datei darf aus einem ausgelieferten Helm-Paket ausgeschlossen
werden, bleibt aber Bestandteil des öffentlichen Quellrepositories.

## Pull Requests

- Pull Requests aus Forks werden erst nach Maintainer-Prüfung zur Ausführung
  kostenpflichtiger oder besonders ressourcenintensiver Workflows freigegeben.
- PR-Code läuft ausschließlich mit Lesezugriff und ohne Secrets. Workflows mit
  `pull_request_target` dürfen keinen unvertrauenswürdigen Checkout ausführen.
- Externe Actions werden auf vollständige Commit-SHAs gepinnt.
- Automatische Merges sind nicht vorgesehen. Mindestens die in den Rulesets
  festgelegten Reviews und Statusprüfungen müssen erfolgreich sein.
- Versionsnummern folgen Semantic Versioning; die erste Releaseversion ist
  `v0.0.1`.

Mit einem Beitrag bestätigst du, dass du ihn rechtmäßig unter der im jeweiligen
Repository angegebenen Lizenz bereitstellen darfst. Diese Aussage ersetzt keine
rechtliche Prüfung.
