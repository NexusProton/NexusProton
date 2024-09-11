Hier ist die Dokumentation für die beiden Klassen `TerrainFollower` und `FollowCamera`, mit den entsprechenden Code-Kommentaren integriert, um die Funktionsweise und Anpassungen zu verdeutlichen:

---

### **Klasse: TerrainFollower**

Die `TerrainFollower`-Klasse steuert ein Schiff, das über einem Terrain schwebt und sich entlang des Terrains bewegt. Die Klasse passt die Höhe des Schiffs an die Terrainhöhe an und sorgt dafür, dass das Schiff Hindernisse sanft erklimmt, wenn es auf einen Anstieg zufährt.

```csharp
using UnityEngine;

public class TerrainFollower : MonoBehaviour
{
    public Terrain terrain;             // Referenz auf das Terrain
    public float hoverHeight = 1f;      // Höhe über dem Terrain
    public float moveSpeed = 10f;       // Geschwindigkeit des Schiffs
    public float rotationSpeed = 100f;  // Drehgeschwindigkeit
    public float lookAheadDistance = 2f; // Distanz, um vor dem Schiff die Terrainhöhe zu prüfen
    public float heightAdjustSpeed = 2f; // Geschwindigkeit, mit der das Schiff auf eine neue Höhe lerpt

    private float targetHeight;         // Zielhöhe des Schiffs

    void Update()
    {
        // Spielerbewegung mit den Pfeiltasten oder WASD
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        // Bewegung des Schiffs basierend auf der Eingabe
        Vector3 moveDirection = new Vector3(horizontal, 0, vertical).normalized;
        transform.Translate(moveDirection * moveSpeed * Time.deltaTime, Space.World);

        // Berechne die neue Höhe des Schiffs basierend auf dem Terrain vor ihm
        AdjustHeightToTerrain(moveDirection);

        // Rotation des Schiffs basierend auf der Eingabe
        if (moveDirection != Vector3.zero)
        {
            // Drehung des Schiffs in Bewegungsrichtung
            Quaternion toRotation = Quaternion.LookRotation(moveDirection, Vector3.up);
            transform.rotation = Quaternion.RotateTowards(transform.rotation, toRotation, rotationSpeed * Time.deltaTime);
        }
    }

    // Passt die Höhe des Schiffs an die Terrainhöhe an und sorgt für ein sanftes Steigen und Sinken
    void AdjustHeightToTerrain(Vector3 moveDirection)
    {
        // Erhalte die aktuelle Position des Schiffs
        Vector3 currentPosition = transform.position;

        // Erzeuge einen Punkt vor dem Schiff, um die kommende Terrainhöhe zu prüfen
        Vector3 lookAheadPosition = currentPosition + moveDirection * lookAheadDistance;

        // Bestimme die Höhe des Terrains an der Position des Schiffs und am Look-Ahead-Punkt
        float currentTerrainHeight = terrain.SampleHeight(currentPosition) + hoverHeight;
        float lookAheadTerrainHeight = terrain.SampleHeight(lookAheadPosition) + hoverHeight;

        // Wenn das Terrain vor dem Schiff höher ist, setze das Ziel auf diese Höhe
        targetHeight = Mathf.Max(currentTerrainHeight, lookAheadTerrainHeight);

        // Lerne sanft zur Zielhöhe
        transform.position = new Vector3(currentPosition.x, Mathf.Lerp(currentPosition.y, targetHeight, heightAdjustSpeed * Time.deltaTime), currentPosition.z);
    }
}
```

---

### **Klasse: FollowCamera**

Die `FollowCamera`-Klasse steuert eine Kamera, die einem Zielobjekt (z. B. einem Schiff) folgt. Sie sorgt dafür, dass die Kamera sich hinter dem Ziel positioniert, sanft die Bewegung verfolgt und auf das Ziel ausgerichtet bleibt.

```csharp
using UnityEngine;

public class FollowCamera : MonoBehaviour
{
    public Transform target;          // Das Schiff oder das Ziel, dem die Kamera folgen soll
    public Vector3 offset = new Vector3(0, 5, -10);  // Abstand zur Zielposition (etwas höher und zurückversetzt)
    public float followSpeed = 5f;    // Wie schnell die Kamera dem Schiff folgt
    public float rotationSpeed = 2f;  // Wie schnell die Kamera die Rotation anpasst

    void LateUpdate()
    {
        // Zielposition der Kamera berechnen: Offset relativ zur Ausrichtung des Schiffs
        Vector3 targetPosition = target.position + target.TransformDirection(offset);

        // Kamera sanft zu der Zielposition bewegen
        transform.position = Vector3.Lerp(transform.position, targetPosition, followSpeed * Time.deltaTime);

        // Berechne die Blickrichtung auf das Ziel
        Quaternion targetRotation = Quaternion.LookRotation(target.position - transform.position, Vector3.up);

        // Kamera sanft in die Richtung des Ziels rotieren lassen
        transform.rotation = Quaternion.Slerp(transform.rotation, targetRotation, rotationSpeed * Time.deltaTime);
    }
}
```

---

### **Zusammenarbeit der Klassen:**
- **`TerrainFollower`** sorgt dafür, dass das Schiff sanft über dem Terrain fährt und auf Anstiege reagiert.
- **`FollowCamera`** folgt dem Schiff und positioniert sich entsprechend der Blickrichtung des Schiffs, um eine dynamische Perspektive zu ermöglichen.

Diese Kommentare im Code erläutern die Funktionsweise der Variablen und Methoden und erleichtern die Anpassung für verschiedene Anwendungsfälle.
Hier ist die Dokumentation für die beiden Klassen `TerrainFollower` und `FollowCamera`. Diese Dokumentation erklärt die Funktionalität jeder Klasse, ihre Variablen und Methoden sowie deren Anwendung.

---

### **Klasse: TerrainFollower**

Die `TerrainFollower`-Klasse steuert ein Schiff, das über einem Terrain schwebt und sich entlang des Terrains bewegt. Die Klasse passt die Höhe des Schiffs an die Terrainhöhe an und sorgt dafür, dass das Schiff Hindernisse sanft erklimmt, wenn es auf einen Anstieg zufährt.

#### **Variablen:**
- `public Terrain terrain`: Referenz auf das Terrain-Objekt in der Szene, das die Höheninformationen für das Schiff bereitstellt.
- `public float hoverHeight = 1f`: Höhe, die das Schiff über dem Terrain schweben soll.
- `public float moveSpeed = 10f`: Geschwindigkeit, mit der sich das Schiff bewegt.
- `public float rotationSpeed = 100f`: Geschwindigkeit, mit der sich das Schiff dreht.
- `public float lookAheadDistance = 2f`: Distanz, in der vor dem Schiff die Terrainhöhe geprüft wird, um mögliche Steigungen oder Hindernisse frühzeitig zu erkennen.
- `public float heightAdjustSpeed = 2f`: Geschwindigkeit, mit der das Schiff auf die neue Zielhöhe lerpt, um sanft auf und ab zu steigen.
- `private float targetHeight`: Interne Variable, die die Zielhöhe des Schiffs speichert, basierend auf der aktuellen und der kommenden Terrainhöhe.

#### **Methoden:**
- `void Update()`: Hauptmethode, die pro Frame aufgerufen wird. Sie steuert die Bewegung des Schiffs basierend auf Benutzereingaben und passt die Höhe des Schiffs an.
  - **Bewegung und Rotation**: Die Eingaben von Pfeiltasten oder WASD steuern das Schiff relativ zur aktuellen Ausrichtung.
  - **Höhenanpassung**: Die Höhe des Schiffs wird kontinuierlich angepasst, um sanft über dem Terrain zu bleiben.
  
- `void AdjustHeightToTerrain(Vector3 moveDirection)`: Methode, die die Höhe des Schiffs an die Terrainhöhe anpasst. Sie prüft die Terrainhöhe vor dem Schiff (Look-Ahead) und passt die Zielhöhe entsprechend an, sodass das Schiff sanft hoch- und runterfährt.

---

### **Klasse: FollowCamera**

Die `FollowCamera`-Klasse steuert eine Kamera, die einem Zielobjekt (z. B. einem Schiff) folgt. Sie sorgt dafür, dass die Kamera sich hinter dem Ziel positioniert, sanft die Bewegung verfolgt und auf das Ziel ausgerichtet bleibt.

#### **Variablen:**
- `public Transform target`: Referenz auf das Zielobjekt, dem die Kamera folgen soll.
- `public Vector3 offset = new Vector3(0, 5, -10)`: Definiert die relative Position der Kamera zum Ziel, z. B. etwas höher und hinter dem Ziel.
- `public float followSpeed = 5f`: Geschwindigkeit, mit der die Kamera der Zielposition folgt.
- `public float rotationSpeed = 2f`: Geschwindigkeit, mit der die Kamera ihre Ausrichtung anpasst, um das Ziel im Blick zu behalten.

#### **Methoden:**
- `void LateUpdate()`: Wird pro Frame nach allen anderen Update-Methoden aufgerufen, um sicherzustellen, dass die Kamera zuletzt angepasst wird.
  - **Zielposition berechnen**: Die Zielposition der Kamera wird anhand der Position des Ziels und des Offsets bestimmt.
  - **Sanfte Bewegung**: Die Kamera bewegt sich sanft zur berechneten Zielposition.
  - **Zielrotation berechnen**: Die Kamera richtet sich auf das Ziel aus, damit es immer im Blick bleibt.

---

### **Zusammenarbeit der Klassen:**
- **`TerrainFollower`** steuert das Schiff und sorgt dafür, dass es sich entsprechend der Benutzereingaben bewegt und über dem Terrain bleibt.
- **`FollowCamera`** folgt dem Schiff und sorgt dafür, dass der Spieler die Bewegung des Schiffs im Blick hat, während die Kamera sich hinter dem Schiff positioniert.

Diese Dokumentation sollte helfen, die Funktionsweise der beiden Klassen besser zu verstehen und deren Anpassung für verschiedene Anwendungsfälle zu erleichtern.
