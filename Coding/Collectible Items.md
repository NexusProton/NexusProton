Um diese Funktionalität zu implementieren, müssen wir mehrere Dinge berücksichtigen: das Erkennen der Kollision zwischen dem Helden und der Kugel, das Hinzufügen von Punkten zum Punktestand des Helden, das Abspielen eines Sounds und das Entfernen der Kugel. Hier ist eine Schritt-für-Schritt-Anleitung, wie du das erreichen kannst:

1. **Erstellen eines Skripts für die Kugel:**
   - Dieses Skript kümmert sich um die Kollisionserkennung und die Interaktion mit dem Helden.
   
2. **Erstellen eines Punktesystems:**
   - Ein einfaches Punktesystem, das die Punkte des Helden verwaltet.

3. **Hinzufügen eines Audiosystems:**
   - Ein Audiosystem, das den Sound abspielt, wenn der Held die Kugel berührt.

### Schritt 1: Skript für die Kugel

Erstelle ein neues C#-Skript mit dem Namen `Collectible.cs` und füge es der Kugel hinzu:

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    public int points = 100;
    public AudioClip collectSound;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            // Füge Punkte hinzu
            GameManager.Instance.AddPoints(points);
            
            // Spiele den Sound ab
            AudioSource.PlayClipAtPoint(collectSound, transform.position);

            // Zerstöre die Kugel
            Destroy(gameObject);
        }
    }
}
```

### Schritt 2: Punktesystem

Erstelle ein weiteres Skript namens `GameManager.cs` und füge es einem leeren GameObject in deiner Szene hinzu (z.B. einem Objekt namens `GameManager`). Stelle sicher, dass dieses Objekt mit dem Tag `GameManager` versehen ist.

```csharp
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public static GameManager Instance;
    private int score = 0;

    private void Awake()
    {
        if (Instance == null)
        {
            Instance = this;
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }

    public void AddPoints(int points)
    {
        score += points;
        Debug.Log("Score: " + score);
    }

    public int GetScore()
    {
        return score;
    }
}
```

### Schritt 3: Audiomanager (optional, falls noch nicht vorhanden)

Falls du noch keinen Audiomanager hast, erstelle ein Skript namens `AudioManager.cs`:

```csharp
using UnityEngine;

public class AudioManager : MonoBehaviour
{
    public static AudioManager Instance;
    public AudioSource audioSource;

    private void Awake()
    {
        if (Instance == null)
        {
            Instance = this;
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }

    public void PlaySound(AudioClip clip)
    {
        audioSource.PlayOneShot(clip);
    }
}
```

### Schritt 4: Einstellungen in Unity

1. **Kugel Prefab:**
   - Füge dem Kugel-Prefab das `Collectible`-Skript hinzu.
   - Setze den Wert für `points` im `Collectible`-Skript auf 100.
   - Weisen Sie das `collectSound`-Audio-Clip zu.
   - Stelle sicher, dass die Kugel einen Collider (z.B. `SphereCollider`) hat und die Option "Is Trigger" aktiviert ist.

2. **Player:**
   - Füge deinem Helden (Player) das Tag `Player` hinzu.

3. **AudioManager:**
   - Erstelle ein leeres GameObject und füge das `AudioManager`-Skript hinzu.
   - Füge eine `AudioSource`-Komponente hinzu und weise sie dem `audioSource`-Feld im `AudioManager`-Skript zu.

4. **GameManager:**
   - Erstelle ein leeres GameObject und füge das `GameManager`-Skript hinzu.
   - Setze den Tag des GameObjects auf `GameManager`.

### Testen

Starte das Spiel und bewege den Helden zur Kugel. Wenn der Held die Kugel berührt, sollte die Kugel verschwinden, 100 Punkte hinzugefügt werden und der Sound abgespielt werden.

Mit diesen Schritten solltest du eine funktionierende Kugelsammelmechanik in deinem Spiel haben. Lass mich wissen, ob du weitere Anpassungen oder Ergänzungen benötigst!
