# Konzeptblatt

## Projekt Konzept / User Story

- Unternehmen ist ein KMU, welches Kleidung / Fashionprodukte verkauft
- Unternehmen hat folgende Server im Betrieb:
  - Webserver
  - FTP Server
  - evtl. Datenbankserver

| Server          | Serverbeschreibung                                             | Serverkomponente                |
|-----------------|----------------------------------------------------------------|---------------------------------|
| Webserver       | Firmenwebseite läuft hier mit der Beschreibung des Produkts    | - Django Framework<br/>- Apache |
| FTP Server      | Beinhaltet alle Administrative Dokumente des Unternehmens und  | FTP                             |
| Datenbankserver | Beinhaltet alle                                                | MariaDB                         |

User Story
Als TICTS der Schule Testhausen, mit rund 500 Schülern und Lehrern, möchte ich ein robustes und effizientes Backup-Konzept, das den Anforderungen der Schule entspricht und sicherstellt, dass bei einem Datenverlust oder Systemausfall alle wichtigen Daten, wie Schülerdaten, Unterrichtsmaterialien und Noten, schnell und vollständig wiederhergestellt werden können.
Das Backup-System soll folgende Anforderungen erfüllen:
1. Automatisierte Backups: Täglich sollen automatisierte Backups der kritischen Systeme durchgeführt werden, um den manuellen Aufwand zu minimieren und die Verfügbarkeit aktueller Daten zu gewährleisten.
2. Flexibilität: Das System muss sowohl lokale als auch cloudbasierte Backups unterstützen, um eine hohe Datensicherheit und Ausfallsicherheit zu garantieren.
3. Einfache Bedienung: Eine benutzerfreundliche Oberfläche für den IT-Administratoren zur Verwaltung und Überwachung der Backups soll verfügbar sein.
4. Kosteneffizienz: Die Lösung muss finanziell nachhaltig und ressourcenschonend sein.
5. Schnelle Wiederherstellung: Das Backup-System muss eine zügige Wiederherstellung ermöglichen, um Ausfallzeiten und Unterrichtsunterbrechungen zu minimieren.
6. Datensicherheit und Compliance: Um die Vertraulichkeit und Integrität der Daten zu gewährleisten, müssen gespeicherte Daten verschlüsselt und vor unberechtigtem Zugriff geschützt werden. Zudem soll das System den rechtlichen Datenschutzbestimmungen der Schweiz entsprechen.
Diese Anforderungen werden durch eine Kombination aus NAS-Systemen, Cloud-Backups und regelmäßiger Überwachung sichergestellt.