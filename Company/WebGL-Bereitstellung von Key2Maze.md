**Max**: Um **Key2Maze** als WebGL-Spiel auf unsere Website zu bringen, müssen wir die folgenden Schritte unternehmen:

### Schritte zur WebGL-Bereitstellung von Key2Maze:

#### 1. **Projekt-Setup und Vorbereitung**
- **Unity-Projekt öffnen**: Öffne das Unity-Projekt von Key2Maze.
- **Backup erstellen**: Erstelle ein Backup des aktuellen Projekts, bevor wir Änderungen vornehmen.
- **Unity-Version prüfen**: Stelle sicher, dass wir eine Unity-Version verwenden, die WebGL-Builds unterstützt (Unity 5.3 und höher).

#### 2. **Build-Einstellungen konfigurieren**
- **Build-Einstellungen öffnen**: Gehe zu `File -> Build Settings`.
- **Plattform auswählen**: Wähle "WebGL" als Plattform aus und klicke auf "Switch Platform".
- **Build-Optionen**: Stelle sicher, dass alle notwendigen Szenen im Build enthalten sind, indem du die Häkchen neben den Szenen setzt, die eingebunden werden sollen.

#### 3. **WebGL-Spezifische Einstellungen**
- **Player-Einstellungen**: Klicke auf "Player Settings" und passe die WebGL-spezifischen Einstellungen an, z.B. Auflösung, Kompressionsformat und Speichergröße.
- **Quality-Einstellungen**: Setze die Qualitätseinstellungen für WebGL auf eine mittlere bis hohe Qualität, um eine gute Performance zu gewährleisten.
- **WebGL Template**: Wähle oder erstelle ein WebGL-Template, um das Erscheinungsbild der WebGL-Seite anzupassen.

#### 4. **Build-Prozess**
- **Build ausführen**: Klicke auf "Build" und wähle einen Zielordner für den WebGL-Build aus.
- **Build überprüfen**: Stelle sicher, dass der Build fehlerfrei durchläuft und die erforderlichen Dateien (HTML, JSON, JS) generiert werden.

#### 5. **Deployment auf der Website**
- **FTP-Zugang**: Stelle sicher, dass du FTP-Zugang zu unserer Website hast.
- **Dateien hochladen**: Lade die WebGL-Build-Dateien in ein neues Verzeichnis auf dem Webserver hoch.
- **Testen**: Überprüfe, ob das Spiel auf verschiedenen Browsern und Geräten funktioniert.

### Beispiel für Unity WebGL Deployment

#### Projekt-Setup und Vorbereitung
```csharp
using UnityEngine;

public class Key2Maze : MonoBehaviour
{
    void Start()
    {
        // Initialisierungen
    }

    void Update()
    {
        // Spiel-Logik
    }
}
```

#### Build-Einstellungen konfigurieren
- Öffne die Build-Einstellungen und wähle WebGL als Zielplattform:
```csharp
// Build-Einstellungen
void SetupBuild()
{
    // WebGL auswählen und Plattform wechseln
    BuildTarget target = BuildTarget.WebGL;
    EditorUserBuildSettings.SwitchActiveBuildTarget(BuildPipeline.GetBuildTargetGroup(target), target);
}
```

#### Deployment auf der Website
- Lade die Build-Dateien per FTP hoch:
```bash
# Beispiel für das Hochladen per FTP (Linux/MacOS Terminal)
ftp ftp://username:password@yourwebsite.com
put -r /path/to/WebGLBuild /path/to/website/directory
```

**Kai**: Um sicherzustellen, dass alles reibungslos funktioniert, sollten wir auch:

1. **Kommunikation und Dokumentation**
   - **Team-Meeting**: Ein kurzes Meeting abhalten, um sicherzustellen, dass alle wissen, was zu tun ist.
   - **Dokumentation**: Eine Schritt-für-Schritt-Dokumentation erstellen, falls wir den Prozess wiederholen müssen.

2. **Fehlerbehebung**
   - **Debugging**: Während des Build-Prozesses auf mögliche Fehler achten und diese sofort beheben.
   - **Tests**: Umfangreiche Tests durchführen, um sicherzustellen, dass das Spiel auf verschiedenen Browsern und Geräten funktioniert.

3. **Alternative Speicherlösungen**
   - **Cloud-Backup**: Zukünftige Projekte und wichtige Dateien in der Cloud sichern, um den Verlust von Daten zu vermeiden.
   - **Externe Festplatten**: Regelmäßige Backups auf externen Festplatten erstellen und diese sicher lagern.

Sobald wir den aktuellen Prototypen fertig haben und auf der Website bereitstellen können, sollten wir dies auch in unseren Marketing- und PR-Aktivitäten hervorheben. Das wird uns helfen, mehr Aufmerksamkeit auf unsere Projekte zu lenken und potenzielle Kunden und Partner zu beeindrucken.
