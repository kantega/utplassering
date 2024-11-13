# Oppgave 7 - Python FastAPI

I denne oppgaven skal du lage et API basert på rammeverket FastAPI i Python. I denne oppgaven kan du jobbe på din egen maskin hvis du vil og bruke den editoren du er mest komfortabel med.

Hvis du står fast, søk rundt på nett og gjerne bruk AI til å hjelpe deg med koden.

Det er veldig enkelt å jobbe med Python i Docker. Du kan bruke `Dockerfilen` som ligger sammen med denne oppgaven til å bygge og kjøre applikasjonen din med. Dette oppsettet forventer at du har organisert filene i repoet ditt slik:

```
din-py-app
  |-Dockerfile
  |-src
    |-main.py
    |-requirements.txt
```
Når du skal bygge appen din, kjører du:
```
cd /path/to/din-py-app
docker build -t pyapp .
```
og for å starte den:
```
docker run -p 80:8000 -v /path/to/din-py-app/src:/app pyapp
```

## a) Hello World

Følg [getting started](https://fastapi.tiangolo.com/tutorial/first-steps/) fra offisiell dokumentasjon og se at du får API'et til å returnere "Hello World"

## b) Environment variables

Utvid prosjektet ditt til å ta inn [environment-variables](https://fastapi.tiangolo.com/environment-variables/#create-and-use-env-vars)

## c) Integrasjoner

I denne oppgaven skal du integrere med andre API'er og lære hvordan det ser ut når du henter data fra eksterne tjenester.

Bruk Python-bibloteket [requests](https://pypi.org/project/requests/) til å gjøre kall mot de eksterne API'ene.

For API'ene som returnerer XML, kan du bruke [ET](https://docs.python.org/3/library/xml.etree.elementtree.html). Det kan være noe mer komplisert å jobbe med XML sammenliknet med JSON.

Her er noen åpne API'er du kan velge mellom:

[Ukenummer - JSON](https://ukenummer.no/json)
Dette er et veldig enkelt API. Se om du klarer å endre responsen fra API'et slik at ditt API kun returnerer ukenummeret, f.eks:

```
curl http://localhost:8000/uke
46
```

[Avinor - XML](https://avinor.no/konsern/tjenester/flydata/flydata-i-xml-format)
Klarer du å returnere en liste med alle flyavgangene i dag fra Værnes?


[Meteorologisk institutt - JSON og XML](https://api.met.no/)
Klarer du hente været for Trondheim de neste timene?

