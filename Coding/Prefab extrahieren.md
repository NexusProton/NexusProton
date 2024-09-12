# Prefab extrahieren

Um ein einzelnes Prefab aus einem Asset-Paket wie dem "Ultimate Spaceship Generator" zu extrahieren und es zu kopieren, ohne das gesamte Asset-Paket mitzuschleppen, kannst du die folgenden Schritte durchführen. Damit werden die Daten des Prefabs (Modelle, Materialien, Texturen usw.) extrahiert und separat gespeichert.

### Vorgehensweise zur Extraktion eines einzelnen Prefabs:

1. **Prefab im Projektfenster finden:**
   - Öffne dein Unity-Projekt und navigiere im Projektfenster zum Asset-Ordner des Ultimate Spaceship Generator.
   - Suche das Prefab, das du extrahieren möchtest.

2. **Prefab in die Szene ziehen:**
   - Ziehe das Prefab in deine Szene, sodass es dort sichtbar ist und du es weiter bearbeiten kannst.

3. **Abhängigkeiten überprüfen:**
   - Wähle das Prefab in der Szene aus und gehe im Inspector-Fenster auf den Prefab-Root.
   - Klicke mit der rechten Maustaste auf das Prefab und wähle `Select Dependencies`. Dies zeigt alle Abhängigkeiten (Modelle, Materialien, Texturen), die das Prefab benötigt.

4. **Abhängige Dateien extrahieren:**
   - Kopiere die angezeigten Abhängigkeiten und das Prefab in einen separaten Ordner in deinem Projekt (z. B. "ExtractedPrefabs").
   - Um dies zu tun, kannst du im Projektfenster einen neuen Ordner erstellen, dann die ausgewählten Dateien in diesen Ordner ziehen.

5. **Prefab neu erstellen:**
   - Lösche das Prefab aus der Szene und ziehe die kopierte Version aus deinem neuen Ordner in die Szene, um sicherzustellen, dass es korrekt funktioniert und keine fehlenden Abhängigkeiten hat.

6. **Duplizierung und Neu-Speicherung:**
   - Wähle das Prefab im neuen Ordner und mache eine Kopie davon (`Ctrl + D`), um es zu duplizieren und sicherzustellen, dass keine Links zu den ursprünglichen Dateien bestehen.
   - Ziehe die Kopie in die Szene und wähle dann im Inspector „`Apply to Prefab`“ oder „`Override`“, um die Änderungen zu speichern.

7. **Projekt bereinigen:**
   - Teste das extrahierte Prefab, um sicherzustellen, dass es unabhängig von den ursprünglichen Asset-Paketen funktioniert. Anschließend kannst du das ursprüngliche Asset-Paket aus deinem Projekt entfernen, wenn du möchtest.

### Wichtige Hinweise:
- **Abhängigkeiten sorgfältig prüfen:** Achte darauf, dass alle Materialien, Texturen und Skripte, die das Prefab benötigt, ebenfalls kopiert wurden.
- **Rechte respektieren:** Beachte, dass du das extrahierte Prefab nur in Projekten verwenden solltest, die mit den Lizenzbedingungen des ursprünglichen Assets übereinstimmen.

Solltest du dabei auf Schwierigkeiten stoßen oder mehr Details benötigen, lass es mich wissen!
