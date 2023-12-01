# The RefCard 3 with Ansible

Dies ist ein Schul-Projekt.

## Wie man Visual Studio in WSL öffnet

1. WSL im command line öffnen
2. Directory öffnen
3. "code ." eingeben

## Finde deinen public-key raus

1. WSL Ubuntu öffnen
1. Folgendes eingeben: `cat /home/"user"/.ssh/id_rsa.pub`

## Cloud-config schreiben

1. Neuen default user erstellen
2. bei `ssh_authorized_keys` den public-key einfügen

##  Erstellen Sie 2 MaaS Instanzen mit Ihrem Schlüsselpaar. Wählen Sie "druettimann" als Lehrer
1. Im Browser https://maas.bbw-it.ch/index.php eingeben und sich einloggen.
2. Im Header **MAAS** auswählen
3. Im Feld **Organisation** beim Dropdown **Teacher**: **druettimann** auswählen.
4. Im Feld **Software** beim Input feld Initial Script: **Cloud config** rein Kopieren aus dem Dokument **cloud-config.yml**
5. Dann erstellen.
6. Dies Zwei mal machen da man 1 Instanz für die Webapp braucht und eine Instanz für die DB
