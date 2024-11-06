
Det jeg lagde på Actions i fjor

# Oppgave X

Hent Github pages prosjektet ditt til Raspberry Pi.

*a)*  
Lag et nytt par med ssh-nøkler uten passord på Raspberry Pi. [Se her](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

*b)*  
Legg til ny public ssh-nøkkel til i Github som deploy key i ditt pages prosjekt. [Se her](https://dylancastillo.co/how-to-use-github-deploy-keys/#create-a-deploy-key-on-github)

*c)*  
Sjekk om du har installert git på Raspberry Pi. Hvis ikke:
```
apt install git
```

*d)*  
På Raspberry Pi, slett default side i Nginx
```
rm /var/www/html/*.html
```
(Sjekk først om den ligger der).
Hente side fra Github
```
git clone git@github.com:example/example.github.io.git .
```
Husk å stå i katalogen `/var/www/html`

---

Husk pause!!!

## Oppgave 2

Lag et SSL fra [Let's Encrypt](https://letsencrypt.org/). Legg til sertifikat til webserveren din, slik at du kan bruke HTTPS.

*a)*  
Installer [Certbot](https://certbot.eff.org/) og Nginx-plugin på Raspberry Pi.
```
apt install certbot python3-certbot-nginx
```

*b)*  
Lag et sertifikat ved hjelp av Certbot.
```
certbot --nginx -d eksempel.kantega.no
```

---

Husk pause!!!

## Oppgave 3

Automatiser publisering av endringer på siden med [Github Actions](https://github.com/features/actions)

*a)*  
Legg public key du lagde tidligere inn i `.ssh/authorized_keys` på Raspberry.

*b)*  
Vi vil at Github Actions skal kopiere koden vår til Raspberry når vi gjør en push. Vi skal bruke et ferdiglaget prosjekt sammen med Github Actions. Se litt på eksemplene [her](https://github.com/appleboy/ssh-action). Før må vi legge inn litt info i prosjektet om hvor prosjektet skal lastes opp. Gå til `Settings > Secrets and variables > Actions` i ditt Github-prosjekt og legg inn:

- HOST=DNS navn på Raspberry
- KEY=Privat nøkkel opprettet tidligere
- PORT=SSH port (22)
- USERNAME=Brukernavn (root)

*c)*  
I ditt prosjekt opprett filen `.github/workflows/github-actions.yml` med innholdet:

```yaml
name: remote ssh command
on: [push]
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
    - name: executing remote ssh commands using password
      uses: appleboy/ssh-action@v1.0.3
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USERNAME }}
        key: ${{ secrets.KEY }}
        port: ${{ secrets.PORT }}
        script: |
          cd /var/www/html
          git pull              
```

Merk den siste biten under `script:` i filen.

*d)*  
Gjør en endring i koden og push, sjekk om den virker under Actions i prosjektet.

---

Godt jobba!!!  
Har du husket is?
```

Note: I've removed the styling and icon references as they are not directly translatable to standard markdown. The structure and content of the document have been preserved.