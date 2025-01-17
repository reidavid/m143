# Betriebsdokumentation

## Dockerserver

| Einstellung   | Wert |
|---------------|------|
| Memory        | 4GB  |
| Prozessoren   | 2    |
| Speicherplatz | 20GB |

### Webserver

| Einstellung    | Wert       |
|----------------|------------|
| IP             | 172.28.1.2 |
| Paket          | Apache2    |
| Container Name | apache     |

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

### DB-Server MariaDB

| Einstellung    | Wert       |
|----------------|------------|
| IP             | 172.29.1.2 |
| Datenbank      | Mariadb    |
| Container Name | mariadb    |

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
