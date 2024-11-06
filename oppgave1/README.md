# Oppgave 1 - Sett opp Raspberry Pi
---
Vi skal starte med å installere noe på Raspberry Pi maskinene.

## a) - Last ned Raspberry Pi OS
Raspberry PI os finner du [her](https://www.raspberrypi.com/software/).
Du kan selv velge om du vil laste ned Raspberry Pi Imager, eller om du vil laste ned [image-filen](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-32-bit) og bruke `dd` (Bare på Linux og Mac).
Dersom du bruker `dd`, bruk `lsblk` på Linux eller `diskutil list` på Mac for å finne SD-kortet. For å skrive til kortet `xz -dc filnavn.img.xz | dd of=/dev/sdkort status=progress`
Sett in SD-kort, start maskinen og :crossed_fingers:

## b) - Konfigurer Raspberry Pi

- Oppdater systemet ved å kjøre følgende kommandoer:

```bash
sudo apt update
sudo apt upgrade -y
```

- Sett en statisk IP-adresse for Raspberry Pi. Åpne konfigurasjonsfilen:

```bash
sudo nano /etc/dhcpcd.conf
```

- Legg til følgende linjer nederst i filen (erstatt X med ønskede verdier):

```conf
interface eth0
static ip_address=X.X.X.X/24
static routers=X.X.X.X
static domain_name_servers=X.X.X.X
```

Endre hostname for Raspberry Pi. Kjør følgende kommando:

```bash
sudo raspi-config
```

- Velg "System Options" > "Hostname" og angi ønsket navn.

- Restart Raspberry Pi for å aktivere endringene:

```bash
sudo reboot
```

- Etter omstart, verifiser de nye innstillingene:
  - Sjekk IP-adressen: `ip addr show`
  - Sjekk hostname: `hostname`

---
