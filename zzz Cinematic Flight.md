## Cinematic Kamera im MAZE

### 1. Konzept
Die Idee besteht darin, eine Cinematic Kamera zu erstellen, die sich dynamisch durch die verschiedenen Etagen eines Labyrinths (MAZE) bewegt. Diese Kamera soll zufällige Punkte anfliegen und dabei sanfte Übergänge (Lerping) zwischen den Positionen zeigen. Dadurch erhalten die Spieler eine eindrucksvolle Ansicht des Labyrinths und seiner Struktur.

### 2. Funktionen der Cinematic Kamera
- **Zufällige Wegpunkte:**
  - Die Kamera wählt zufällig Wegpunkte im MAZE aus, zu denen sie fliegt. Diese Punkte können strategisch platziert sein, um interessante Bereiche des Labyrinths zu zeigen.
- **Etagenwechsel:**
  - Die Kamera kann zwischen verschiedenen Etagen wechseln, um die vertikale Dimension des Labyrinths zu betonen.
- **Sanfte Übergänge (Lerping):**
  - Die Bewegung der Kamera erfolgt durch Lerping, was bedeutet, dass die Übergänge zwischen den Punkten sanft und flüssig sind.

### 3. Technische Umsetzung
- **Wegpunkt-Generator:**
  - Ein Skript, das zufällige Wegpunkte innerhalb des MAZE generiert. Diese Wegpunkte sollten sicherstellen, dass interessante Bereiche des Labyrinths hervorgehoben werden.
  
- **Kamerabewegung:**
  - Die Kamera bewegt sich durch Lerping von einem Wegpunkt zum nächsten. Lerping sorgt für weiche Übergänge und vermeidet ruckartige Bewegungen.

- **Etagenverwaltung:**
  - Ein System, das die Etagen des MAZE kennt und die Kamera entsprechend navigiert. Dies könnte durch eine Hierarchie von Etagen oder durch Tags/Markierungen an bestimmten Punkten geschehen.

### 4. Implementierungsschritte
- **Schritt 1: Wegpunkt-Generator**
  - Entwickle einen Algorithmus, der zufällige Punkte im MAZE auswählt.
  - Stelle sicher, dass die Punkte gleichmäßig über das MAZE verteilt sind und interessante Bereiche abdecken.

- **Schritt 2: Kamerabewegung**
  - Implementiere die Bewegung der Kamera durch Lerping. Nutze dabei mathematische Funktionen, um weiche Übergänge zu gewährleisten.
  
- **Schritt 3: Etagenwechsel**
  - Füge ein System hinzu, das die Kamera von einer Etage zur anderen bewegt. Dies könnte durch das Setzen von Wegpunkten in verschiedenen Etagen erreicht werden.

- **Schritt 4: Testen und Verfeinern**
  - Teste die Cinematic Kamera in verschiedenen Szenarien, um sicherzustellen, dass die Bewegung flüssig und die Ansichten beeindruckend sind.
  - Passe die Parameter des Lerping und der Wegpunkt-Generierung an, um die besten Ergebnisse zu erzielen.

### 5. Beispielcode (Pseudocode)
```python
class CinematicCamera:
    def __init__(self, maze):
        self.maze = maze
        self.current_position = self.get_random_point()
        self.target_position = self.get_random_point()
        self.lerp_speed = 0.1

    def get_random_point(self):
        # Generiere einen zufälligen Punkt im MAZE
        return self.maze.get_random_point()

    def update(self):
        # Bewege die Kamera durch Lerping zur Zielposition
        self.current_position = self.lerp(self.current_position, self.target_position, self.lerp_speed)
        if self.is_at_target():
            self.target_position = self.get_random_point()

    def lerp(self, start, end, speed):
        # Berechne die nächste Position durch Lerping
        return start + (end - start) * speed

    def is_at_target(self):
        # Überprüfe, ob die Kamera die Zielposition erreicht hat
        return distance(self.current_position, self.target_position) < threshold
