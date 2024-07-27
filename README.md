# GitHub Repository Anleitung

## Einrichtung eines GitHub-Repositories

Hier sind die Schritte, um ein GitHub-Repository für unsere Dokumentation einzurichten:

### 1. Erstellen eines GitHub-Kontos
Falls du noch keinen GitHub-Account hast, erstelle einen unter [GitHub Sign Up](https://github.com/join).

### 2. Erstellen eines neuen Repositorys
- Gehe auf die GitHub-Website und logge dich in deinen Account ein.
- Klicke oben rechts auf das Plus-Symbol (+) und wähle "New repository".
- Gib dem Repository einen Namen, z.B. `Nexus-Pioneers-Documentation`.
- Wähle, ob das Repository öffentlich oder privat sein soll. Ein privates Repository ist nur für Teammitglieder sichtbar.
- Optional: Füge eine README-Datei hinzu, um die Grundstruktur zu erstellen.
- Klicke auf "Create repository".

### 3. Klonen des Repositorys auf deinem lokalen Rechner
- Öffne ein Terminal (oder die Git-Bash, wenn du Windows verwendest).
- Navigiere zu dem Verzeichnis, in dem du das Repository klonen möchtest.
- Führe den folgenden Befehl aus (ersetze `<your-username>` und `<repository-name>` durch die entsprechenden Werte):
  ```sh
  git clone https://github.com/<your-username>/<repository-name>.git

Wechsle in das neu erstellte Verzeichnis.
cd <repository-name>

### 4. Hinzufügen und Bearbeiten von Dateien
Erstelle oder bearbeite die Dateien im Repository-Ordner.
Füge die Änderungen zum Git-Index hinzu:
sh
Code kopieren
git add .

Committe die Änderungen mit einer entsprechenden Nachricht:
sh
Code kopieren

git commit -m "Initial commit with project documentation"

### 5. Hochladen der Änderungen zu GitHub
Pushe die Änderungen zu GitHub:
sh
Code kopieren

git push origin main

Falls der Hauptbranch in deinem Repository nicht main sondern master heißt, ersetze main durch master.

### 6. Zusammenarbeit mit dem Team
Teile das Repository mit deinen Teammitgliedern, indem du sie als Collaborators hinzufügst:

Gehe auf die Seite deines Repositorys auf GitHub.
Klicke auf "Settings" und dann auf "Manage access".
Klicke auf "Invite a collaborator" und gib die GitHub-Benutzernamen deiner Teammitglieder ein.
Zusammenfassung:

Erstelle ein GitHub-Konto und ein neues Repository.
Klone das Repository auf deinen lokalen Rechner.
Füge Dateien hinzu und committe Änderungen.
Pushe die Änderungen zu GitHub.
Teile das Repository mit deinem Team.

