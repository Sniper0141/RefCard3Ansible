# The RefCard 3 with Ansible

Das hier ist ein Schul-Projekt. 

Diese Dokumentation führt Sie durch den Prozess der Inbetriebnahme des Projekts "RefCard3Ansible" auf Ihrem eigenen Computer mithilfe von Ansible. Bitte folgen Sie den untenstehenden Schritten.

## Voraussetzungen
 
Stellen Sie sicher, dass die folgenden Softwarekomponenten auf Ihrem Computer installiert sind:
 
- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Maven](https://maven.apache.org/)
- [Java](https://www.java.com/)
 
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

## Ansible in WSL installieren

1. Öffne WSL
2. Mit `sudo apt update` WSL updaten
3. Mit `sudo apt install ansible` ansible lokal installieren

## Ansible playbook

1. Mit ChatGPT generieren
2. `ansible-playbook playbook.yml` in WSL eingeben

