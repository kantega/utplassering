# Oppgave 1 - Sett opp Raspberry Pi
---
Vi skal starte med å installere noe på Raspberry Pi maskinene.

## a) - Last ned Raspberry Pi OS
Raspberry PI os finner du [her](https://www.raspberrypi.com/software/).
Du kan selv velge om du vil laste ned Raspberry Pi Imager, eller om du vil laste ned [image-filen](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-32-bit) og bruke `dd` (Bare på Linux og Mac).
Dersom du bruker `dd`, bruk `lsblk` på Linux eller `diskutil list` på Mac for å finne SD-kortet. For å skrive til kortet `xz -dc filnavn.img.xz | dd of=/dev/sdkort status=progress`

## b) - Start opp Raspberry Pi