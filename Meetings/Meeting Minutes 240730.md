### Zusammenfassung der täglichen Stand-up-Besprechung

**Datum:** 25.07.2024

#### Anwesende
- Boss
- Max
- Julia
- Tobi
- Operator (abwesend)

#### Besprochene Punkte
1. **Neue Spielidee von Julia**
   - Idee: Der Spieler soll von Punkt A nach Punkt B gelangen, wobei beide Punkte auf beliebigen Stockwerken sein können.
   - Zusätzliche Idee: Implementierung einer Steuerung ähnlich wie bei Pac-Man, wo der Held in vier Richtungen gelenkt wird und selbstständig weiterläuft, bis er gegen eine Wand stößt.

2. **Kombination der Ideen**
   - Julia und Max haben über die Integration der beiden Ideen diskutiert.
   - Vorschlag: Ersetzen einiger Wände durch Items, die der Spieler einsammeln muss.

3. **Anpassungen am PlayerController**
   - Max hat den `PlayerController` angepasst, damit der Spieler auf dem höchsten Stockwerk spawnt, sich bewegen kann und die Kamera dem Spieler folgt.

4. **Nächste Schritte und Aufgabenverteilung**
   - Julia wird die visuelle Darstellung der neuen Ideen weiterentwickeln.
   - Max wird den `PlayerController` weiter verfeinern und die neue Mechanik implementieren.
   - Tobi wird die Dokumentation aktualisieren und Vorschläge für die besten Tools zur Erstellung von Diagrammen machen.
   - Operator ist heute abwesend, daher wird das Team eigenständig weiterarbeiten.

#### Anleitungen und Vorschläge
- **Draw.io Anleitung von Tobi**
  - Eine ausführliche Anleitung zur Nutzung von Draw.io für Diagramme wurde erstellt und in die Dokumentation aufgenommen.

- **Max' Vorschlag zur Code-Strukturierung**
  - Diskussion über die Modularität des Codes und die Erstellung einzelner Klassen für verschiedene Komponenten des Spiels.
  - Vorschlag zur Code-Strukturierung wurde detailliert besprochen und dokumentiert.

### Anleitung zur Nutzung von Draw.io

#### Einleitung
Draw.io ist ein benutzerfreundliches Tool zur Erstellung von Diagrammen. Es eignet sich hervorragend für die Visualisierung von Projektstrukturen, Workflows und anderen Diagrammtypen.

#### Schritte zur Nutzung von Draw.io

1. **Zugriff auf Draw.io**
   - Öffnen Sie Ihren Webbrowser und gehen Sie zu [Draw.io](https://www.draw.io/).

2. **Erstellen eines neuen Diagramms**
   - Klicken Sie auf "Create New Diagram".
   - Wählen Sie eine Vorlage oder beginnen Sie mit einem leeren Diagramm.
   - Geben Sie dem Diagramm einen Namen und wählen Sie den Speicherort aus (lokal oder in der Cloud).

3. **Diagrammelemente hinzufügen**
   - Verwenden Sie die linke Seitenleiste, um verschiedene Formen und Symbole auszuwählen.
   - Ziehen Sie die gewünschten Elemente in das Arbeitsbereich.

4. **Verbindungen erstellen**
   - Verwenden Sie die Verbindungstools, um Linien zwischen den Elementen zu ziehen.
   - Passen Sie die Linien an, um die Beziehungen zwischen den Elementen darzustellen.

5. **Elemente anpassen**
   - Klicken Sie auf ein Element, um seine Eigenschaften anzupassen (Farbe, Text, Größe, etc.).
   - Verwenden Sie die rechte Seitenleiste, um detailliertere Anpassungen vorzunehmen.

6. **Speichern und Exportieren**
   - Speichern Sie Ihr Diagramm regelmäßig, um sicherzustellen, dass keine Daten verloren gehen.
   - Exportieren Sie das Diagramm in verschiedenen Formaten (PNG, PDF, SVG, etc.) für die Verwendung in Präsentationen oder Dokumentationen.

#### Tipps
- Nutzen Sie die Vorlagenbibliothek, um schnell professionelle Diagramme zu erstellen.
- Verwenden Sie Ebenen, um komplexe Diagramme übersichtlich zu halten.
- Teilen Sie Ihr Diagramm mit Teammitgliedern, um gemeinsam daran zu arbeiten.

### Beispielcode

#### PlayerController.cs
```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    private CharacterController characterController;
    public int highestFloor = 10; // Beispielwert, anpassen an die tatsächliche Anzahl der Stockwerke

    private void Start()
    {
        characterController = GetComponent<CharacterController>();
        SpawnOnHighestFloor();
    }

    private void SpawnOnHighestFloor()
    {
        // Anpassen der Y-Koordinate, um auf dem höchsten Stockwerk zu spawnen
        Vector3 spawnPosition = new Vector3(0, highestFloor * 3.0f, 0); // Annahme: Stockwerkshöhe = 3 Einheiten
        transform.position = spawnPosition;
    }

    private void Update()
    {
        float moveHorizontal = Input.GetAxis("Horizontal");
        float moveVertical = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
        characterController.Move(movement * moveSpeed * Time.deltaTime);
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Item"))
        {
            // Handle item collection
            Destroy(other.gameObject);
            UIManager.Instance.UpdateScore(1); // Beispiel zur Punkteaktualisierung
        }
    }
}
