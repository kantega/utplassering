# Oppgave 3 - Containerisering + Github Actions

## a) Containeriser din Github Pages

På roten av Github pages repoet ditt, opprett filen `Dockerfile` med følgende innhold

```
FROM nginx

COPY ./src /usr/share/nginx/html
```

Her antas det også at kildekoden din flyttes til en egen mappe med navn `src`, altså at filstrukturen din ender opp med å se slik ut:

```
Dockerfile
src
 |
 |- index.html
 |- style.css
 |- whatever.js
```

Dette fordi du vil _bare_ kopiere inn de filene som har noe med websiden din å gjøre i container imaget

Test å bygg container imaget ditt lokalt og test at det fungerer.

```
docker build -t myapp .
docker run -p 80:80 myapp
```

## b) Bygging av container image på Github

I forrige oppgave bygde du container imaget lokalt. I denne oppgaven skal du flytte byggingen til å skje automatisk i Github med Github Actions

I repoet ditt, opprett filen `.github/workflows/build.yaml`. Filen kan du kopiere ut fra repoet, `build.yaml`

Når du nå pusher dette til Github, vil du kunne se denne workflowen kjøre under Ditt repo -> Actions.

Når workflowen har kjørt ferdig og imaget er ferdig bygd vil du kunne finne igjen imaget ditt under Din profil -> Packages

## c) Deploy container image fra Github

Først, opprett en API / deploy key, Din profil -> Settings -> Developer Settings -> Personal Access Tokens -> Token (Classic) -> Generate New (Classic) -> Sett navn / Expiry / read:packages

Nøkkelen som blir produsert her er et passord du kan bruke for å logge inn med Docker i Github som registry, slik:

```
docker login ghcr.io $DITT_GITHUB_BRUKERNAVN
```
hvor du paster inn det genererte passordet på passord-promptet, hvor hvis alt gikk bra skal få en melding om success login.

Du kan nå pulle container imaget fra Github med:

```
docker pull ghcr.io/gtufte/<namespace>/<image>
```

Prøv å få dette container imaget deployet på din Raspberry

