# Oppgave 4 - Docker Compose

## a) Deploy websiden med Docker Compose

Til nå har du startet containeren din med `docker run`, men nå skal vi start containeren med `compose`.

```
sudo su
cd ~
mkdir myapp
cd myapp
```

Inne i mappen myapp, opprett en fil med navn `docker-compose.yml` med følgende innhold:

```
services:
  app:
    image: <container-image>
    container_name: app
    ports:
      - 80:80
      - 443:443
    restart: unless-stopped
```
hvor du butter ut `<container-image>` med image-navnet som ble opprettet i Github og som du startet opp i forrige oppgave

Stop containeren som du startet i forrige oppgave, og start den på nytt med compose

```
docker ps
# merk deg navnet på den kjørende containeren

docker stop <navn>

docker compose up -d

docker ps
# merk deg navnet her, satt fra container_name i docker-compose.yml
```

For å se loggene fra den kjørende containeren

```
docker compose logs -f
```

Besøk nettsiden din på nytt, se at det produserer logglinjer

