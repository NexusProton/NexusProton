Die Multiplayer-Variante von Minesweeper mit Unity und **C#** umsetzen. Hier ist eine Schritt-für-Schritt-Anleitung, wie du **Photon PUN 2** verwendest, um den Multiplayer-Aspekt mit C# in Unity zu implementieren:

### Schritte zur Implementierung von *Minesweeper Multiplayer* mit Photon und Visual Studio:

#### 1. **Unity-Projekt vorbereiten**:
   - **Photon PUN 2 installieren**: 
     - Gehe zu **Window > Asset Store** und suche nach "Photon PUN 2". Installiere das Plugin in deinem Projekt.
     - Erstelle ein Photon-Konto unter [Photon Engine](https://www.photonengine.com/) und hole dir einen **App-ID-Schlüssel**. Füge diesen unter **PhotonServerSettings** in Unity hinzu.
   
#### 2. **Lobby-System**:
   - Füge in Unity eine einfache **Lobby** hinzu, in der die Spieler ein Spiel erstellen oder einem Spiel beitreten können.
   - Implementiere ein grundlegendes System, um Räume (Rooms) zu erstellen, denen andere Spieler beitreten können.

```csharp
using Photon.Pun;
using Photon.Realtime;
using UnityEngine;
using UnityEngine.UI;

public class LobbyManager : MonoBehaviourPunCallbacks
{
    public InputField roomNameInput;
    public Text statusText;

    void Start()
    {
        PhotonNetwork.ConnectUsingSettings();  // Verbindung zum Photon-Server herstellen
    }

    public void CreateRoom()
    {
        PhotonNetwork.CreateRoom(roomNameInput.text, new RoomOptions { MaxPlayers = 2 });
    }

    public void JoinRoom()
    {
        PhotonNetwork.JoinRoom(roomNameInput.text);
    }

    public override void OnConnectedToMaster()
    {
        statusText.text = "Verbunden mit Photon!";
    }

    public override void OnJoinedRoom()
    {
        statusText.text = "Raum beigetreten!";
        PhotonNetwork.LoadLevel("MinesweeperMultiplayerScene");  // Lade die Szene
    }
}
```

#### 3. **Spielfeld erstellen (Grid)**:
   - Verwende das `Tile`-Prefab aus deinem Minesweeper-Spiel und synchronisiere es zwischen den Spielern mithilfe von **PhotonView**.
   - Jedes `Tile`-Objekt sollte mit einem **PhotonView**-Komponenten versehen sein, um das Synchronisieren von Spielaktionen (wie das Aufdecken von Feldern) zu ermöglichen.

```csharp
using Photon.Pun;
using UnityEngine;

public class MultiplayerTile : MonoBehaviourPun
{
    public bool isMine = false;
    public int adjacentMines = 0;
    public bool revealed = false;

    private SpriteRenderer spriteRenderer;

    public Sprite hiddenSprite;
    public Sprite revealedSprite;
    public Sprite mineSprite;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
        spriteRenderer.sprite = hiddenSprite;
    }

    [PunRPC]
    public void RevealTile()
    {
        if (revealed)
            return;

        revealed = true;

        if (isMine)
        {
            spriteRenderer.sprite = mineSprite;
            // Sende an alle Spieler, dass das Spiel vorbei ist
            photonView.RPC("GameOver", RpcTarget.All);
        }
        else
        {
            spriteRenderer.sprite = revealedSprite;
        }
    }

    void OnMouseOver()
    {
        if (Input.GetMouseButtonDown(0) && PhotonNetwork.IsMasterClient)  // Linksklick nur vom Host
        {
            photonView.RPC("RevealTile", RpcTarget.All);
        }
    }
}
```

#### 4. **Netzwerk-Synchronisierung (Spieleraktionen)**:
   - **PhotonView**: Stelle sicher, dass jede Spielaktion (wie das Aufdecken eines Feldes) zwischen den Clients synchronisiert wird. Dies wird mit RPC (Remote Procedure Calls) erreicht.

#### 5. **Spielzustand synchronisieren (Game Over)**:
   - Wenn ein Spieler eine Mine aufdeckt, wird das Spiel für alle Spieler beendet. Dazu kannst du ein `GameOver`-Event an alle Clients senden, um den Spielzustand zu synchronisieren.

```csharp
[PunRPC]
void GameOver()
{
    Debug.Log("Game Over! Alle Spieler sind informiert.");
    // Hier kannst du die Spielende-Logik und den Reset implementieren
}
```

#### 6. **Ressourcen-Management**:
   - Verwende die nummerierten Sprites (wie das von dir hochgeladene Bild), um die Anzahl der benachbarten Minen anzuzeigen, sobald ein Feld aufgedeckt wird.

#### 7. **Multiplayer-Features erweitern**:
   - **Koop-Modus**: Arbeite daran, wie Spieler zusammen Minen markieren und das Spielfeld aufdecken können.
   - **Wettkampfmodus**: Implementiere einen Timer, der zeigt, wer schneller mehr Felder aufdeckt.
   - **Runden-System**: Baue ein einfaches Punktesystem ein, das Runden und Siege für jedes Team/Spieler verfolgt.

#### 8. **Testen und Debugging**:
   - Teste das Spiel im Unity-Editor, indem du das **Unity-Multiplayer-Playmode**-Tool nutzt, um das Spiel lokal mit mehreren Clients zu simulieren.
   - Stelle sicher, dass das Spiel korrekt zwischen mehreren Spielern synchronisiert wird und teste die wichtigsten Spielereignisse (wie das Aufdecken einer Mine).

### Was du als Nächstes machen kannst:
- **Visual Studio**: Mit **Visual Studio** kannst du den gesamten C#-Code direkt für Unity schreiben. Richte die **Photon PUN 2**-Abhängigkeiten in Unity ein und beginne mit der Implementierung.
- **Optimierungen**: Du kannst dein Projekt jederzeit optimieren, indem du die Spielerinteraktionen und das UI weiterentwickelst. Teste mit verschiedenen Netzwerkszenarien (zum Beispiel, wenn ein Spieler das Spiel verlässt).

### Ressourcen:
- [Photon PUN 2 Dokumentation](https://doc.photonengine.com/en-us/pun/current/getting-started/pun-intro) für Details zum Multiplayer in Unity.

Wenn du Unterstützung bei der Implementierung oder Fragen hast, stehe ich gerne zur Verfügung!
