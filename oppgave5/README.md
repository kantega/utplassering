# Oppgave 5 - Lets Encrypt

## a)

Les litt om Let's Encrypt og hvordan det fungerer: [Let's Encrypt - How it works](https://letsencrypt.org/how-it-works/)

## b) Lag et sertifikat med Certbot

I denne oppgaven skal du bruke `certbot` for å lage et SSL-sertifikat basert på HTTP-ACME challenge. Oppgaven tar utgangspunkt i at du kjører Nginx-imaget fra oppgave 3/4.

Det er dette tilfellet absolutt enklest å installere `certbot` inne i container imaget, som et proof of concept.

Ende `Dockerfile` i repoet ditt og legg til følgende i bunn av filen

```
RUN apt-get update -y \
 && apt-get install -y python3-certbot python3-certbot-nginx
```

Push koden og la Github bygge et nytt image

På Raspberry'n, utvid `docker-compose.yml` med `volumes` slik at den ser slik ut. Samtidig, bytt ut `image` med det nye imaget ditt, hvor `certbot` er installert.

```
services:
  app:
    image: <container-image>
    container_name: app
    ports:
      - 80:80
      - 443:443
    restart: unless-stopped
    volumes:
      - ./ssl:/ssl
```

Restart appen slik at nytt image blir startet og volumet blir etablert
```
docker compose down
docker compose up -d
```

Hopp inn i containeren og kjør `certbot`-commandoen for å lage SSL-sertifikatet
```
docker exec -it app bash
certbot.... TODO
```

