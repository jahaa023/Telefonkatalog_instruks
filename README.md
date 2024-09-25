# Hvordan man setter opp telefonkatalog på Raspberry pi

# Sett opp Raspberry Pi
1. Skru på din Raspberry Pi
2. Følg instruksjonene på skjermen:
   ## Trykk "Next"
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/start.png?hash=b09c881a5736586851e18c5f05848de9" /><br>
   ## Velg land, område, tidssone og tastatur
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/locale.png?hash=fbd68b45d7d7dbdb8d4b8a007b884dcd" /><br>
   ## Lag en bruker. Velg et passord og brukernavn.
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/user.png?hash=a599f2e570ef4504b7686165b75ff87d" /><br>
   ## Koble til et nettverk
   For dette trenger du enten en ethernet kabel, eller en wireless WiFi adapter. <br>
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/network.png?hash=0689b7309b820bbe9d6481ede702ae90" /><br>
   ## Velg en default browser
   Dette er ikke særlig viktig, og begge funker fint <br>
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/browser.png?hash=81ebfe9b12c6bf8977067fd8570b5c3d" /><br>
   ## Raspberry Pi Connect
   Vi trenger ikke Raspberry Pi Connect for dette, så du kan skru den av.
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/connect.png?hash=778089c4dbf6d00753d303420a211a6f" /><br>
   ## Oppdatering av Software
   Dette er smart å skru på, sånn at vi kan være sikre på at vi har de nyeste oppdateringene, så trykk "Next" <br>
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/update.png?hash=246c11bd48b5c6f0e3332b39fc58e6a5" /><br>
   Denne skjermen vil poppe opp. Vi venter til den blir ferdig. <br>
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/download.png?hash=1b90dc708944ceeeabe6ac5fb3c65df4" /><br>
   ## Bli ferdig
   Når oppdateringene blir ferdig får du denne skjermen. Trykk restart for å fortsette.<br>
   <img src="https://www.raspberrypi.com/documentation/computers/images/initial-setup/restart.png?hash=a4722ccce3851961d3c05d4ac8245452" /><br>

# Last ned SSH
   ## Åpne terminalen og last ned oppdateringer.
   Når du kommer inn på Desktopen, åpne Terminalen ved å trykke Ctrl + Alt + T. Terminalen burde se sånn ut: <br>
   <img src="https://github.com/jahaa023/Telefonkatalog_instruks/blob/main/img/pi-command-prompt.png" /><br>
   I terminalen skriv dette:
   ```
   sudo apt update
   ```
   og dette:
   ```
   sudo apt upgrade
   ``` 
   Disse kommandoene sørger for at vi har alle de nyeste oppdateringene lastet den.
   ## Set opp brannmur for SSH
   Det er lurt å ha en firewall i systemet vårt, så vi laster ned og setter opp UFW.
   1. Last ned UFW (uncomplicated firewall) :
      ```
      sudo apt install ufw
      ```
   2. Skru på firewall:
      ```
      sudo ufw enable
      ```
   3. Tillat SSH gjennom brannmuren:
      ```
      sudo ufw allow ssh
      ```
   4. Til slutt, sjekk statusen av firewall:
      ```
      sudo ufw status
      ```
   ## Last ned og skru på SSH
   SSH er ett program som lar oss kjøre kommandoer på Raspberry Pien vår fra en annen maskin.
   1. Last ned SSH-server:
      ```
      sudo apt install openssh-server
      ```
   2. Skru på SSH når PCen starter i fremtiden:
      ```
      sudo systemctl enable ssh
      ```
   3. Skru på SSH:
      ```
      sudo systemctl start ssh
      ```
   4. Finn IPen din.
      ```
      ip a
      ```
      Resultatet av kommandoen burde se ut som noe likt dette. IPen som er i den røde boksen er den vi fokuserer på. Dette er ip-adressen vi bruker til å koble til Raspberry       Pien via ssh hvis du bruker trådløs nettverk. Hvis du bruker ethernet kabel, så er ip-adressen etter "eth0:": <br>
      <img src="https://github.com/jahaa023/Telefonkatalog_instruks/blob/main/img/ipa_terminal_red.png" /><br>
