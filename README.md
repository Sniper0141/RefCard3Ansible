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

## Hosts
1. Zuerst muss man ein .txt file erstellen für die Hosts
2. Die zwei IP Adressen von den VM's muss man kopieren und in diesem Textfile richtig einsetzten
3. Dann muss man noch den User festlegen dies sieht dann in etwa so aus.
4. `[web] web1 ansible_host=192.168.66.27 ansible_user=kyle`
5. `[db] db1 ansible_host=192.168.66.28 ansible_user=kyle`

## Kontrollieren ob die Hosts verbunden sind
1. Auf wireguard gehen und den Tunnel zum MAAS aktivieren.
2. Ins WSL Terminal gehen und `ansible -m ping all` eingeben
3. Es sollte in etwa so aussehen: `db1 | SUCCESS => {
       "changed": false,
    "ping": "pong"
}
web1 | SUCCESS => {
      "changed": false,
    "ping": "pong"`
4. Im WSL Terminal kann man auch `ansible-inventory --graph` eingeben und dann sieht man alle Hosts.
   
## Ansible in WSL installieren
1. Öffne WSL
2. Mit `sudo apt update` WSL updaten
3. Mit `sudo apt install ansible` ansible lokal installieren

## Ansible playbook
Als erstes muss man ein .yml File erstellen, das wird das Playbook File.
Da man zwei Hosts hat muss man dies unterteilen. 
1. Host deklarieren `- name: Webserver
  hosts: web
  gather_facts: false
  become: true`
2. `tasks:` Hier beginnen die einzelnen Aufgaben, die auf dem Webserver ausgeführt werden.
3. `git:` Klont das Git-Repository des Projekts auf den Zielhost.
4. Java und Maven installieren
5. `apt:` Installiert Java und Maven mit dem Paketmanager APT.
6. `command:` "mvn package": Führt den Maven-Build-Prozess im Verzeichnis "RefCard3Ansible" aus.
7. `lineinfile:` Fügt eine Zeile in die Datei .bashrc ein, um Umgebungsvariablen zu setzen.
8. `shell:` ". ~/.bashrc": Lädt die Bash-Umgebung neu, um die neuen Umgebungsvariablen zu aktivieren.

Wir haben es nicht hinbekommen die Applikation zum Laufen zu bringen.
Um das Playbook auszufühen muss man im WSL Terminal `ansible-playbook playbook.yml` eingeben wenn man nur Kontrollieren will und das Playbook nicht ausführen will muss man `ansible-playbook playbook.yml --check` eingeben.

## Datanbank



