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
## Installer Git, Python og MariaDB
   Nå skal vi laste ned alle de nødvendige applikasjonene for at koden skal fungere.
   Kjør disse kommandoene:
   ```
   sudo apt install python3-pip
   sudo apt install git
   sudo apt install mariadb-server
   sudo apt mysql_secure_installation
   ```
## Sett opp database-bruker i MariaDB
   Nå skal vi sette opp en database med MariaDB med den nødvendige dataen til å ha et fungerende program.
   Kjør disse kommandoene:
   1. Logg inn på MariaDB. 
   ```
   sudo mariadb -u root
   ```
   2. Lag en ny bruker på MariaDB. Skift "username" og "password" med brukernavn og passord du vil ha. I denne brukerveiledningen heter brukeren username og passordet er password.
   ```
   CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
   ```
   3. Gi den nye brukeren rettigheter.
   ```
   GRANT ALL PRIVILEGES ON . TO 'username'@'localhost' IDENTIFIED BY 'password';
   ```
   4. Ferdiggjør rettighetene.
   ```
   FLUSH PRIVILEGES;
   ```
## Koble til Raspberry Pi fra ekstern Windows maskin
   1. Åpne Command Prompt eller CMD ved å søke det opp i søkefeltet i Windows eller ved å trykke Windows+R og skrive inn "cmd" og trykke Enter.
   2. Inne i CMD, skriv følgende kommando. Skift ut "username" med brukernavnet til Raspberry Pien din og "ip" med ip adressen som du fikk tidligere.
      ```
      ssh brukernavn@ip
      ```
   Etter du skriven inn kommandoen må du skrive inn passordet til Raspberry Pien som du lagde tidligere
   Nå kommer en Linux terminal til å komme opp på Windows maskinen. Dette er da terminalen på Raspberry Pien din og man kan kjøre kommandoer på Raspberry Pien fra Windows maskinen.
## Kopier (clone) koden til Telefonkatalogen fra GitHub.
   1. For å laste ned koden trenger vi først en mappe koden skal være i. Vi lager denne mappen med "mkdir" kommandoen, som står for "make directory"
      ```
      mkdir telefonkatalog
      ```
   2. Neste steg er å gå inn på den mappen med "cd" kommandoen, som står for "current directory"
      ```
      cd telefonkatalog/
      ```
   3. Etter du er inn på mappen kjører vi kommandoen "git clone" for å klone kode fra Git/GitHub.
      ```
      git clone https://github.com/LektorRichvoldsen/telefonkatalog_og_database
      ```
      Vi sjekker om det funket med "ls" kommandoen som viser oss hva som er i mappen.
      ```
      ls
      ```
      Hvis alt gikk riktig, burde du få dette tilbake:
      ```
      telefonkatalog_og_database
      ```
   4. Det neste vi gjør er å gi inn på telefonkatalog_og_database mappen med "cd" kommandoen
      ```
      cd telefonkatalog_og_database/
      ```
      Etter det går vi videre inn i "sql" mappen.
      ```
      cd sql/
      ```
      Når det er gjort kjører vi "ls" kommandoen igjen for å sa hva som er inne i mappen.
      ```
      ls
      ```
      Du burde få dette tilbake:
      ```
      1_lag_database.sql 2_lag_tabell.sql 3_lag_testdata.sql 4_select_data.sql readme_sql.md
      ```   
      Dette er alle filene i mappen. Vi trenger koden i alle .sql filene for å lage de nødvendige databasene og tabellene for at programmet skal funke.
   ## Lag database og tabeller i MariaDB
      1. Start med å logge inn på MariaDB med brukeren vi lagde tidligere. Skriv brukernavnet hvor det står "username" og skriv inn passordet når programmet ber om det.
      ```
      sudo mariadb -u username -p
      ```
      2. Kopier koden fra de 3 første .sql filene og lim de inn i terminalen. Gjør det med riktig rekkefølge, fra 1 til 3. Vi starter med "1_lag_database.sql".
      ```
      CREATE DATABASE telefonkatalog;
      ```
      Etter det tar vi "2_lag_tabell.sql".
      ```
      USE telefonkatalog;
      CREATE TABLE person (
       id int NOT NULL AUTO_INCREMENT,
       fornavn VARCHAR(255) NOT NULL,
       etternavn VARCHAR(255) NOT NULL,
       telefonnummer CHAR(8),
       PRIMARY KEY (id)
      );
      ```
      Til sist tar vi "3_lag_testdata.sql"
      ```
      INSERT INTO person (fornavn, etternavn, telefonnummer)
      VALUES ('Erik', 'Perik', '12345678');
      INSERT INTO person (fornavn, etternavn, telefonnummer)
      VALUES ('Lise', 'Pise', '22334455');
      INSERT INTO person (fornavn, etternavn, telefonnummer)
      VALUES ('Testus', 'Jensen', '11114444');
      INSERT INTO person (fornavn, etternavn, telefonnummer)
      VALUES ('Knut', 'Donald', '31415926');
      ```
      For å teste om databasen funker kan vi kopiere kommandoene fra "4_select_data.sql".
      ```
      SELECT * FROM person;

      SELECT fornavn, telefonnummer FROM person;
      
      SELECT * FROM person WHERE fornavn = "Erik";
      
      SELECT telefonnummer FROM person WHERE fornavn = "Lise" AND etternavn = "Pise";
      ```
## Koble Python filen til databasen.
      Etter at vi har settet opp og testet databasen er det tid for å koble databasen til Python filen.
      
      
      
   
   
