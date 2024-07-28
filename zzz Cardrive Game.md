# Unity Browsergame: Fahrzeugsteuerung in einer Landschaft

## 1. Unity-Projekt Einrichten

### a. Unity herunterladen und installieren:
- Lade die neueste Version von Unity Hub herunter und installiere sie.
- Erstelle ein neues Projekt in Unity Hub mit dem 3D-Template.

### b. Projektstruktur vorbereiten:
- Erstelle in deinem Unity-Projekt die benötigten Ordner, z.B. `Assets/Scenes`, `Assets/Prefabs`, `Assets/Scripts`, und `Assets/Models`.

## 2. Landschaft Erstellen

### a. Terrain hinzufügen:
- Gehe zu `GameObject` > `3D Object` > `Terrain`, um eine neue Terrain-Oberfläche hinzuzufügen.
- Verwende die Terrain-Werkzeuge im Inspector, um das Terrain zu formen und Texturen hinzuzufügen.

### b. Terrain-Texturen und -Objekte hinzufügen:
- Füge verschiedene Texturen (z.B. Gras, Felsen) zu deinem Terrain hinzu.
- Importiere und platziere zusätzliche Objekte (wie Bäume oder Felsen), um die Landschaft interessanter zu gestalten.

## 3. Fahrzeug hinzufügen

### a. Fahrzeug-Modell importieren:
- Du kannst ein einfaches Auto-Modell aus dem Unity Asset Store importieren oder ein eigenes Modell verwenden.
- Ziehe das Fahrzeug-Modell in die Szene.

### b. Fahrzeug-Rigidbody hinzufügen:
- Wähle dein Fahrzeugmodell in der Hierarchie aus.
- Gehe zu `Component` > `Physics` > `Rigidbody`, um Physik-Komponenten für dein Fahrzeug hinzuzufügen.

### c. Fahrzeug-Kollisionskörper hinzufügen:
- Gehe zu `Component` > `Physics` > `Box Collider` (oder `Mesh Collider` je nach Modell), um dem Fahrzeug einen Kollisionskörper hinzuzufügen.

## 4. Fahrzeugsteuerung

### a. Fahrzeugssteuerungsskript erstellen:
- Erstelle ein neues C#-Skript in `Assets/Scripts` und nenne es z.B. `CarController`.

### b. Skriptcode für Fahrzeugsteuerung:
- Öffne das Skript und füge den Code für die Fahrzeugsteuerung hinzu.

### c. Skript zum Fahrzeug hinzufügen:
- Ziehe das `CarController`-Skript auf dein Fahrzeug-Modell im Unity-Editor.

## 5. Kamera konfigurieren

### a. Kamera hinzufügen und anpassen:
- Wähle die Kamera in der Hierarchie aus.
- Positioniere die Kamera hinter dem Fahrzeug, sodass der Spieler das Fahrzeug gut sehen kann.
- Du kannst eine einfache Verfolgungskamera erstellen oder Unitys `Cinemachine`-System verwenden, um eine bessere Kameraführung zu erzielen.

## 6. Testen und Anpassen

### a. Szene speichern:
- Speichere deine Szene unter einem geeigneten Namen, z.B. `MainScene`.

### b. Testen:
- Drücke den Play-Button im Unity-Editor, um das Spiel zu starten.
- Verwende die Pfeiltasten oder WASD-Tasten, um das Fahrzeug zu steuern und die Bewegung auf dem Terrain zu testen.

### c. Feinabstimmung:
- Falls nötig, passe die Werte für Geschwindigkeit und Drehgeschwindigkeit im `CarController`-Skript an.
- Verfeinere das Terrain und die Fahrzeugsteuerung, um das Spielgefühl zu verbessern.

## Weiterführende Schritte

1. **Erweiterungen:**
   - Füge zusätzliche Features wie Geschwindigkeitsanzeigen, Benutzeroberflächen oder mehr Fahrzeuganpassungen hinzu.

2. **Fehlerbehebung und Optimierung:**
   - Überprüfe das Verhalten des Fahrzeugs und die Interaktion mit der Umgebung.
   - Optimiere die Leistung für eine flüssigere Spielerfahrung.

3. **Veröffentlichung:**
   - Bereite dein Spiel für die Veröffentlichung vor, indem du es für WebGL oder andere Plattformen exportierst.

Wenn du Fragen zu spezifischen Aspekten oder weiteren Funktionen hast, lass es mich wissen!

```csharp
using UnityEngine;

public class CarController : MonoBehaviour
{
    public float speed = 10f;
    public float turnSpeed = 50f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        float move = Input.GetAxis("Vertical") * speed;
        float turn = Input.GetAxis("Horizontal") * turnSpeed;

        Vector3 moveVector = transform.forward * move * Time.deltaTime;
        rb.MovePosition(rb.position + moveVector);

        Quaternion turnRotation = Quaternion.Euler(0f, turn * Time.deltaTime, 0f);
        rb.MoveRotation(rb.rotation * turnRotation);
    }
}
