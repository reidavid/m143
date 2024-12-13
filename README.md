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

##