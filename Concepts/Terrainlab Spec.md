# Terrainlab Spezifikation

Kein Problem! Ich fasse zusammen, was deine drei Klassen tun und welche Funktionen du implementiert hast:

### 1. **MazeTerrainGenerator**:
   - **Verantwortung**: Erzeugt das Terrain mit einem Maze (Labyrinth) und platziert verschiedene Elemente (z. B. Start- und Zielpunkte, Schiffe).
   - **Wichtige Eigenschaften**:
     - Parameter für die Größe des Terrains und des Labyrinths, die Höhe der "Mauern" (Hügel), und Prefabs für Start-, Ziel- und Schiffsobjekte.
     - Der Algorithmus zur **DFS-basierten Labyrinth-Generierung** (Depth-First-Search), der das Labyrinth in einer 2D-Array-Repräsentation erzeugt.
     - **Wichtige Funktionen**:
       - `GenerateMazeDFS`: Generiert das Labyrinth, wobei "1" einen Weg und "0" eine Wand (Hügel) darstellt.
       - `ApplyMazeToTerrain`: Überträgt die Labyrinthstruktur auf das Terrain, indem Höhenwerte (für Mauern) gesetzt werden.
       - **Schiffplatzierung**: Zufällige Platzierung von Schiffen an validen Positionen im Labyrinth (Wegbereiche, keine Wände).
       - `PlaceStartAndGoal`: Platziert die Start- und Zielpunkte im Labyrinth.
       - `SetupFlyingCamera`: Setzt die Flugkamera für die Spielersteuerung auf.

### 2. **FlyingCameraController**:
   - **Verantwortung**: Ermöglicht dem Spieler die Kontrolle der Kamera über Maus- und Tastatureingaben.
   - **Wichtige Eigenschaften**:
     - **Bewegung**: Spieler bewegt die Kamera mit den Tasten (`Horizontal`, `Vertical`, `Q`, `E`).
     - **Rotation**: Kamera dreht sich basierend auf Mausbewegungen (`Mouse X`, `Mouse Y`).
   
### 3. **MazeGhostShip**:
   - **Verantwortung**: Steuert die Bewegung der Geisterschiffe durch das Labyrinth.
   - **Wichtige Eigenschaften**:
     - **Bewegungsgeschwindigkeit** und **Rotationsgeschwindigkeit** für die Schiffe.
     - Raycasting-Mechanismus zur Hinderniserkennung. Bei einer Kollision mit einer Wand wählt das Schiff eine neue zufällige Richtung.
     - Ein **cursorPrefab** zeigt die Position eines Hindernisses an, falls aktiviert.
     - **Wichtige Funktionen**:
       - `ChooseRandomDirection`: Wählt eine zufällige Bewegungsrichtung aus (oben, unten, links, rechts).
       - `MoveShip`: Überprüft per Raycast, ob sich ein Hindernis in Bewegungsrichtung befindet. Falls kein Hindernis erkannt wird, bewegt sich das Schiff in diese Richtung. Andernfalls wird eine neue Richtung gewählt.
       - `AlignToMovement`: Richtet das Schiff sanft an der Bewegungsrichtung aus.

---

### Zusammenfassung der Gesamtstruktur:
- **MazeTerrainGenerator**: Erstellt das Labyrinth, modifiziert das Terrain entsprechend und platziert Schiffe.
- **FlyingCameraController**: Ermöglicht freie Kamerabewegung für den Spieler über das Terrain.
- **MazeGhostShip**: Verwaltet die autonome Bewegung der Schiffe durch das Labyrinth mit Hinderniserkennung und Richtungswechsel.

---

### Auffällige Punkte:
1. **Platzierung der Schiffe**: Du hast eine gute Methode entwickelt, die sicherstellt, dass die Schiffe nur auf gültigen Pfaden (keine Wände) platziert werden. Die Überprüfung der Terrains-Höhe sorgt auch dafür, dass sie auf der richtigen Höhe erscheinen.
   
2. **Raycasting der Schiffe**: Es gibt eine angepasste Version des Raycastings, die sicherstellt, dass der Raycast leicht in Bewegungsrichtung versetzt startet (`Vector3 raycastStart`). Das ist eine sinnvolle Verbesserung, um potenzielle Kollisionen besser zu erkennen.

3. **Fliegende Kamera**: Mit den aktuellen Bewegungseingaben (Maus und Tastatur) kannst du die Kamera frei bewegen und drehen, was für die Erkundung des Labyrinths nützlich ist.

Gibt es spezifische Teile des Codes, zu denen du Fragen hast oder die du optimieren möchtest?
