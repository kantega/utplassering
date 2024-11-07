# Oppgave 1 - Sett opp Raspberry Pi
---
Vi skal starte med å installere noe på Raspberry Pi maskinene.

## a) - Last ned Raspberry Pi OS
Raspberry PI os finner du [her](https://www.raspberrypi.com/software/).
Du kan selv velge om du vil laste ned Raspberry Pi Imager, eller om du vil laste ned [image-filen](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-32-bit) og bruke `dd` (Bare på Linux og Mac).
Dersom du bruker `dd`, bruk `lsblk` på Linux eller `diskutil list` på Mac for å finne SD-kortet. For å skrive til kortet `xz -dc filnavn.img.xz | sudo dd of=/dev/sdkort status=progress` (vær sikker på at du skriver til riktig device under /dev!!!).
Sett in SD-kort, start maskinen og :crossed_fingers:

## b) - Konfigurer Raspberry Pi

- Sett en statisk IP-adresse for Raspberry Pi. Lag konfigurasjonsfilen:

```bash
sudo nano /etc/network/interfaces.d/eth0
```

- Legg til følgende linjer nederst i filen (erstatt X med ønskede verdier):

```conf
allow-hotplug eth0
iface eth0 inet static
address XXX.XXX.XXX.XXX
netmask 255.255.255.0
gateway XXX.XXX.XXX.XXX
```

- Legg til DNS-server for navneoppslag:

```bash
sudo nano /etc/resolv.conf
```

- Legg til følgende linje nederst i filen

```conf
nameserver 1.1.1.1
```


- Endre hostname for Raspberry Pi. Kjør følgende kommando:

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

- Oppdater systemet ved å kjøre følgende kommandoer:

```bash
sudo apt update
sudo apt upgrade -y
```

## c) - Installer Docker og Git


---
