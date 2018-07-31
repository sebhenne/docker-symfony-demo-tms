# docker-symfony-demo-tms
Docker Umgebung zum Lernen von symfony. Es wurde entworfen für die IT Scouts an der TMS in Oldesloe.

Dieses Repository vereint die bestehenden Repositories https://github.com/maxpou/docker-symfony und https://github.com/symfony/demo

## Installationsvoraussetzungen
Lediglich [Docker](https://www.docker.com/community-edition) ist als Laufzeitumgebung erforderlich.

## Installation
Nach dem Download müssen die Docker Umgebungen erstellt werden. Dazu im Verzeichnis `docker-symfony` die folgenden Befehle ausführen:
```bash
$ docker-compose up -d
```
new build Progress trigger

```
$ docker-compose build
```

Anschließend muss die symfony Konfiguration angepasst werden. Dazu muss die Umgebungskonfiguration ersstellt und angepasst werden:
```bash
$ cp symfony-demo/.env.dist symfony-demo/.env
```

Anschließend muss in dieser Datei die Datenbankverbindung `DATABASE_URL` wie folgt gesetzt werden:
```php
DATABASE_URL=mysql://root:root@db/symfony-demo
```
Anschließend kann im Verzeichnis `docker-symfony` die symfony Anwendung gebaut werden. Dabei die folgenden Befehle im Verzeichnis`docker-symfony`ausführen:
```bash
$ docker-compose exec php bash
$ composer install
$ bin/console doctrine:database:create
$ bin/console doctrine:schema:update --force
$ bin/console doctrine:fixtures:load --no-interaction
```
Dann sollte die [http://localhost](Symfony Anwendung) laufen.

## Starten und Stoppen
Stoppen kann man die Docker Container wie folgt:
```bash
$ docker-compose down
```
Wieder starten dann mit:
```bash
$ docker-compose up -d
```

