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

- Legg til følgende linjer  i filen (Se på tavla for adresser):

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

- Start SSH-server ved å opprette en tom fil med navn ssh på boot partisjonen:

```bash
sudo touch /boot/firmware/ssh
```

- Endre hostname for Raspberry Pi (Se på tavla for hostnavn). Kjør følgende kommando:

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

## c) - Installer Docker
[Docker](https://en.wikipedia.org/wiki/Docker_(software)) er en programvare for å kjøre [konteinere](https://en.wikipedia.org/wiki/Containerization_(computing)) på Linux. Konteinere er en måte å isolere applikasjoner som kjører på en server.
Du finner også denne [installasjonsguiden](https://docs.docker.com/engine/install/raspberry-pi-os/) på Dockers dokumentasjon.

- Avinstallere programvare som kan være installert fra før.

```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

- Legg til Dockers installasjonskilde

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/raspbian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/raspbian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

- Installer siste versjon av Docker

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

- Test installasjonen

```bash
sudo docker run --rm -p 80:80 nginx:alpine-slim
```

- Åpne en nettleser, eller bruk `curl` på http://dittdomene for å teste om det fungerer. Tast `ctrl-c` for å avslutte konteineren.

---
