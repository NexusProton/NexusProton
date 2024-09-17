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

### Es scheint, dass wir ein paar grundlegende Überlegungen und Optimierungen vornehmen sollten, um die Ordnung im Projekt zu verbessern:

1. **Terrain-Kollisionsverhalten**:
   - Der Terrain Collider ist in Unity grundsätzlich undurchdringbar, solange die Objekte darauf Kollisionen erkennen können. Der Layer "Obstacle" sollte klar definiert werden und nicht einfach auf "Default" gesetzt bleiben. Überlege, den Layer speziell für Hindernisse oder das Terrain zuzuweisen, falls du später mit verschiedenen Layern arbeiten möchtest.
   - Für die Wälle, die durch Anhebung des Terrains entstehen, sollte der Terrain Collider bereits greifen. Du musst also keine zusätzlichen Kollisionsobjekte für diese Wälle einfügen, solange sie hoch genug sind.

2. **Schiff-Kollisionen**:
   - Schiffe mit einem **Mesh Collider** sind oft rechenintensiv und komplizierter, insbesondere wenn du eine Kollisionserkennung gegen das Terrain und andere Schiffe benötigst.
   - Es wäre möglicherweise besser, **Rigidbody-Komponenten** hinzuzufügen, um physikbasierte Bewegung und Kollisionen zu handhaben. Zusammen mit einem **Box- oder Sphere-Collider** könnte das effizienter sein. 
   - Wenn die Schiffe keine tatsächliche Physikinteraktion haben müssen (z. B. mit Schwerkraft), kannst du den Rigidbody auf **kinematisch** setzen, um physikalische Berechnungen zu vereinfachen.

3. **Tagging und Layer-System**:
   - Für die zukünftige Verwaltung solltest du dir überlegen, verschiedene Tags oder Layers für unterschiedliche Bereiche des Terrains (Wände, Pfade) zu verwenden. Zum Beispiel könnte das Terrain selbst auf einem speziellen Layer sein, während Wände und andere Hindernisse explizit markiert oder mit Tags versehen werden.
   - Die Schiffe könnten entweder den **"Obstacle" Layer** verwenden (wenn sie Hindernisse darstellen sollen) oder einen eigenen Layer bekommen, um sie einfacher von anderen Objekten zu unterscheiden.

4. **Raycast für Kollisionserkennung**:
   - Da die Wälle durch Anhebung des Terrains entstehen, könntest du prüfen, ob das aktuelle Raycasting gegen den richtigen Layer läuft. Der **Layer "Obstacle"** sollte auf das Terrain oder die Wälle angewendet werden, um sicherzustellen, dass die Schiffe die Wände erkennen.
   - Falls das Terrain als Obstacle dient, stelle sicher, dass der **Terrain Collider** in deinem Raycast mit dem passenden Layer verknüpft ist, um die Bewegung der Schiffe korrekt zu steuern.

5. **Verfeinerung der Bewegungslogik**:
   - Für die Schiffe könnte eine **intelligente Bewegungslogik** notwendig sein, die nicht nur zufällig eine Richtung wählt, sondern auch abhängig von der Umgebung sinnvoll handelt. Eventuell könnten Wegpunkte oder eine Art A* (A-Star) Pfadfindungsalgorithmus für das Navigieren durch das Labyrinth sinnvoll sein, wenn du präzise Steuerungen möchtest.

Lass mich wissen, welche Punkte du priorisieren möchtest, oder ob du weitere Ideen hast!
