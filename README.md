# Backup- und Restore-Systeme implementieren

## Auftraggeber

- Rohr Philipp

## Projektende/-abgabe

- (geplant) 24.01.2025

## Beschreibung

Ein Backup-Konzept eines Betriebs entwickeln und dieses umsetzen.

## Hindernisse

- Benutzerdaten sind immer die wichtigsten Daten, ansonsten soll man zwischen Nutz- und Nichtnutzdaten entscheiden.
- Man sollte Daten auf der Cloud und lokal ein Backup zu haben, damit man im Falle eines Datenverlustes, Bankrupts bei
  der Cloud die Daten immer noch wiederherstellen kann.

# User Story

Als Verantwortlicher der Daten des Betriebs "Fashion Store" möchte ich ein Backup-Konzept erstellen, um im Falle eines
Datenverlustes die Daten wiederherstellen zu können.

# Projekt Ablauf

## Webseite

Für die Webseite habe ich mich entschieden Django zu benutzen. Der Grund dafür ist, dass Django sehr umfangreich ist,
und ich es vorhin noch nie benutzt habe. Beispielsweise ist die integrierte Datenbankfunktion sehr hilfreich, da ich
dann keinen Datenbankserver erstellen muss.

Ich habe damit angefangen, das Django Projekt zu erstellen mithilfe von Pycharm. Dies hat es mir ermöglicht, die
Webseite lokal bei mir zu entwickeln mit einem virtuellen Python environment. Für das Projekt habe ich auch ein
Repository erstellt, damit ich dieses, sobald ich die Entwicklungsphase beendet habe, diese auf den Webserver klonen
kann und in die Produktion einsteigen kann.

In die Django-Seite wollte ich eine API integrieren, damit man die zugänglichen Daten abrufen kann wie beispielsweise
die Produkte des Kleiderladens. Mit dem Rest-Framework für Django habe ich dies einfach umsetzen können.

Die Datenbank wollte ich nicht auf dem Web-Server betreiben, sondern es sollte auf einem separaten DB-Server ablaufen.

In der Webseite selbst sollte man Accounts haben, also sich einloggen, ausloggen und registrieren können. Diese
Funktion war bereits in Django programmiert worden, also musste ich diese nur mit der Template Sprache in die
HTML-Seiten einfügen. Zu einer gewöhnlichen Seite, die Kleider verkauft, gehören auch viele DB-Modelle / Objekte.

## Dockerserver

Um die Infrastruktur simpel zu behalten, arbeite ich mit zwei Dockerservern / Ein Server, der Docker und Portainer installiert hat und
worauf Container für die Datenbank und für die Webseite erstellt werden. Der Andere Dockerserver dient zu Backupzwecken. Auf dem Backup Dockerserver werde ich Der Vorteil dieses Vorgehens ist, dass ich dann nur bei einem Server einen Backup durchführen
muss und dass ich auch dynamisch nach Lust und Laune auch zusätzliche Container erstellen, falls ich beispielsweise
einen Mailserver brauche.

## Datenbankserver

Für den Datenbankserver benutze ich MariaDB. Da Django SQLite benutzt, muss ich dessen Daten mit `py manage.py dumpdata`
exportieren, und diese dann in mariadb einfügen und migrieren. In der Theorie ist das sehr einfach.

Den Datenbankserver habe ich in einem Docker Container erstellt. Diese hat eine statische IP-Adresse, damit der
Web-Server mit der Datenbank kommunizieren kann, auch wenn der Container neu gestartet wird.

Zum Testen habe ich einen phpmyadmin container erstellt, um Daten von Django einfach zu importieren.

## Webserver

Mithilfe von apache2 konnte ich einen einfachen Webserver erstellen. Das docker-compose file habe ich so geschrieben,
dass der 80er Port / der HTTP Port geöffnet ist. 

## Backupserver

Für den Backupserver habe ich einen separaten Dockerserver auf einem Ubuntu Betriebssystem aufgesetzt.
