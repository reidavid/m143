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
Funktion war bereits in Django programmiert worden, also musste ich diese nur mit der Templatesprache in die
HTML-Seiten einfügen. Zu einer gewöhnlichen Seite, die Kleider verkauft, gehören auch viele DB-Modelle / Objekte.

## Dockerserver

| Einstellung   | Wert |
|---------------|------|
| Memory        | 4GB  |
| Prozessoren   | 2    |
| Speicherplatz | 20GB |

### docker-compose

```yaml
version: '3.8'

services:
  apache:
    image: httpd:latest  # Using the latest official Apache image
    container_name: apache  # Container will be named "apache"
    ports:
      - "80:80"  # Exposing port 80 from the container to the host machine
    volumes:
      - ./html:/usr/local/apache2/htdocs  # Optional: Mount a directory from host to container (your custom HTML files)
    networks:
      apache_net:
        ipv4_address: 172.28.1.2
    restart: always  # Always restart the container unless stopped manually

networks:
  apache_net:
    driver: bridge
    ipam:
      config:
        - subnet: 172.28.1.0/24
```

### Details

Um die Infrastruktur simpel zu behalten, arbeite ich mit zwei Dockerservern / Ein Server, der Docker und Portainer  
installiert hat und worauf Container für die Datenbank und für die Webseite erstellt werden. Der Andere Dockerserver
dient zu Backupzwecken.
Der Vorteil dieses Vorgehens ist, dass ich dann nur bei einem Server ein Backup durchführen muss und dass ich nach Lust
und Laune auch zusätzliche Container erstellen kann, falls ich beispielsweise einen Mailserver brauche.
Auf dem Backup Dockerserver erstelle ich eine Datenbank für das Backup der Produktiv-Datenbank und alle Django Apps.

![img.png](srvdir.png)

## Datenbankserver

| Einstellung    | Wert       |
|----------------|------------|
| IP             | 172.29.1.2 |
| Datenbank      | Mariadb    |
| Container Name | mariadb    |

### docker-compose

```yaml
version: "3.9"

services:
  mariadb:
    image: mariadb:latest
    container_name: mariadb
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root_password  # Set the root password
      MYSQL_DATABASE: clothingstore_db          # Initial database to create
      MYSQL_USER: db_user            # Username for the database
      MYSQL_PASSWORD: db_password    # Password for the user
    ports:
      - "3306:3306"  # Expose the MariaDB port to the host
    volumes:
      - mariadb_data:/var/lib/mysql       # Persist database data
    networks:
      mariadb_net:
        ipv4_address: 172.29.1.2

volumes:
  mariadb_data:

networks:
  mariadb_net:
    driver: bridge
    ipam:
      config:
        - subnet: 172.29.1.0/24
```

### Details

Für den Datenbankserver benutze ich MariaDB. Da Django SQLite benutzt, muss ich dessen Daten mit `py manage.py dumpdata`
exportieren, und diese dann in mariadb einfügen und migrieren. In der Theorie ist das sehr einfach.

Den Datenbankserver habe ich in einem Docker Container erstellt. Diese hat eine statische IP-Adresse, damit der
Web-Server mit der Datenbank kommunizieren kann, auch wenn der Container neu gestartet wird.

Zum Testen habe ich einen phpmyadmin container erstellt, um Daten von Django einfach zu importieren.

## Webserver

| Einstellung    | Wert       |
|----------------|------------|
| IP             | 172.28.1.2 |
| Paket          | Apache2    |
| Container Name | apache     |

Mithilfe von apache2 konnte ich einen einfachen Webserver erstellen. Das docker-compose file habe ich so geschrieben,
dass der 80er Port / der HTTP Port geöffnet ist. Somit kann man für Test Zwecke über die IP-Adresse auf den Server
zugreifen, solange man sich im Netzwerk befindet.

## Backupserver

Für den Backupserver habe ich einen separaten Dockerserver auf einem Debian Betriebssystem aufgesetzt.

## TrueNAS Backup

Um noch einen Speicherort zu haben, wo Daten gesichert sind, habe ich mich für einen TrueNAS Backup entschieden. Auf
diesem sollte dann alle wichtigen Kundendaten, Produkte und der Sourcecode der Webseite und der Datenbank gespeichert
werden.

## Gitlab Container Registry Backup

# Auswertung

Meiner Meinung nach habe ich dieses Projekt gut abgeschlossen und bin sehr zufrieden mit meinem Endresultat.

## Backup

## Funktionalität

# Reflexion

Rückblickend bin ich sehr zufrieden mit diesem Projekt. Im Laufe des Vorgangs gab es einige Rückschläge, die mich dazu
führten den Plan umzudenken, ein paar Schritte zurückzukehren und diese zu wiederholen oder sogar Ideen vollständig zu
streichen, weil diese entweder nicht im Zeitraum des Projekts passten oder diese Ideen zu kompliziert waren umzusetzen.
Im Folge eines Rückschlags versuchte ich immer motiviert zu sein und am Ball zu bleiben, damit ich mein Projekt
möglichst effizient und zeitgerecht fortsetzen konnte. Da ich jedoch Frameworks und Systeme gewählt haben, die gut
miteinander fungieren, konnte ich mich recht gut durch das Projekt navigieren.

Letztendlich war mein Ziel jedoch, nicht nur die mir bereits bekannten Methoden und Software anzuwenden, sondern auch
neues zu lernen. Beispielsweise habe ich konstant und ohne Pause an der Webseite mit Django im Betrieb gearbeitet (damit
ich meinen Fokus in der Schule hauptsächlich dem Backup richten kann). Bei der Kreierung einer Webseite mithilfe Django
habe ich massiv viel gelernt über die Model struktur, URL Routing, Views, Forms und vieles mehr, da Django ein
umfangreiches Framework ist.

Persönlich bin ich sehr stolz auf meine errungenen Erkenntnisse währenddessen und hoffe in der Zukunft mehr über Backups
und Datensicherheiten im Detail zu lernen. 
