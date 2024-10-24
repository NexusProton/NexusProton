# Debugger in Unity mit Visual Studio
Um den Debugger in Unity mit Visual Studio einzurichten und zu verwenden, folge diesen Schritten:

### Schritt 1: Visual Studio Tools für Unity installieren
Normalerweise wird Visual Studio mit den "Visual Studio Tools for Unity" geliefert, die du brauchst, um den Debugger korrekt zu verwenden. Stelle sicher, dass du diese Tools installiert hast.

### Schritt 2: Unity mit Visual Studio verknüpfen
1. **Unity-Einstellungen**: Öffne Unity und gehe zu `Edit` > `Preferences` > `External Tools`.
2. **Externer Editor**: Wähle unter "External Script Editor" `Visual Studio` aus. Das stellt sicher, dass Unity Visual Studio verwendet, wenn du auf Skripte doppelklickst.

### Schritt 3: Haltepunkte setzen
1. Öffne dein C#-Skript in Visual Studio.
2. Klicke links neben die Zeile, an der du die Ausführung anhalten möchtest, um einen **Haltepunkt** zu setzen (roter Punkt).

### Schritt 4: Debugging starten
1. **Zurück zu Unity**: Kehre zu Unity zurück und klicke auf `Play`, um das Spiel zu starten.
2. **Zurück zu Visual Studio**: Wechsel zu Visual Studio und klicke auf `Debug` > `Attach to Unity`. Alternativ kannst du auf das kleine grüne Dreieck mit einer Datenverbindung klicken (im Debug-Menü), um Visual Studio mit Unity zu verbinden.
3. Sobald Visual Studio verbunden ist, wird das Spiel an den von dir gesetzten Haltepunkten anhalten, sodass du die aktuellen Variablen und Zustände inspizieren kannst.

- wenn du zurück zu Unity gewechselt hast, mußt du idR das Spiel neu starten!

### Schritt 5: Debugging durchführen
- **Schrittweise ausführen** (`F10`): Führe den Code Zeile für Zeile aus.
- **In Funktionen hineinspringen** (`F11`): Springe in Methodenaufrufe hinein, um zu sehen, was innerhalb einer Funktion passiert.
- **Ausführung fortsetzen** (`F5`): Setze die Ausführung fort, bis der nächste Haltepunkt erreicht wird.

Mit diesen Schritten kannst du den Debugger verwenden, um Fehler in deinem Code zu finden, Variablen zu überwachen und den Ablauf deines Spiels im Detail zu verstehen.
