# Skybox in Unity

Eine Skybox in Unity ist ein großartiges Mittel, um den Hintergrund deiner Szene mit einem Himmelsbild, einer Weltraumlandschaft oder einer anderen Umgebung zu füllen. Hier ist eine Schritt-für-Schritt-Anleitung, wie du eine Skybox hinzufügst:

### Schritt-für-Schritt-Anleitung: Skybox in Unity hinzufügen

1. **Importiere eine Skybox:**
   - Du kannst eine Skybox aus dem Unity Asset Store importieren oder eigene Skybox-Texturen verwenden.
   - Um eine Skybox aus dem Asset Store zu importieren:
     - Öffne den Unity Asset Store (`Window -> Asset Store` oder im Browser).
     - Suche nach „Skybox“ und lade eine passende Skybox herunter.
   - Alternativ kannst du eigene Texturen importieren und daraus eine Skybox erstellen.

2. **Erstelle ein Material für die Skybox:**
   - Erstelle ein neues Material:
     - Rechtsklick im Projektfenster → `Create -> Material`.
   - Benenne das Material sinnvoll, z.B. `SkyboxMaterial`.

3. **Skybox-Shader einstellen:**
   - Wähle das neu erstellte Material aus.
   - Ändere den Shader-Typ auf `Skybox`:
     - Im Inspector → Klicke auf das Dropdown-Menü neben „Shader“ → Wähle `Skybox` → Wähle den gewünschten Typ, z.B. `6 Sided`, `Cubemap`, `Procedural`, etc.

4. **Texturen zuweisen:**
   - Füge die entsprechenden Texturen den verschiedenen Seiten zu (wenn du `6 Sided` ausgewählt hast, fügst du Texturen für `Front`, `Back`, `Left`, `Right`, `Up`, `Down` hinzu).
   - Für `Cubemap` oder `Procedural` kannst du eine einzelne Cubemap oder prozedurale Parameter verwenden.

5. **Skybox als Umgebung festlegen:**
   - Öffne das Lighting-Fenster:
     - `Window -> Rendering -> Lighting Settings`.
   - In den `Environment`-Einstellungen findest du die Option „Skybox Material“.
   - Ziehe dein erstelltes Skybox-Material in das Feld „Skybox Material“.

6. **Anpassen und Feineinstellungen:**
   - Du kannst die Intensität und Rotation der Skybox im selben Fenster anpassen, um den gewünschten Effekt zu erzielen.

### Fertig! 

Jetzt wird deine Szene von der Skybox umgeben und verleiht der Umgebung eine immersive Atmosphäre. Wenn du eine andere Skybox ausprobieren möchtest, kannst du einfach das Material im Lighting-Fenster austauschen.
