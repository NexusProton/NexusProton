# Bulk-Convert .mp3 to .mp4

Tools und Programme, mit denen du mehrere MP3-Dateien gleichzeitig in MP4-Videodateien umwandeln kannst. Hier sind einige Optionen, die dir helfen können, die Konvertierung im "Bulk" durchzuführen:

### 1. **Desktop-Software für Batch-Konvertierung**

#### **VLC Media Player**
- VLC ist ein beliebter Media Player, der auch eine Batch-Konvertierungsfunktion bietet.
- **Anleitung:**
  1. Öffne VLC und gehe zu **Medien > Konvertieren/Speichern**.
  2. Füge die MP3-Dateien hinzu, die du konvertieren möchtest.
  3. Wähle unten die Option **Konvertieren** und stelle das Ausgabemodell auf MP4 ein.
  4. Füge ein statisches Bild als Hintergrund hinzu, wenn du es möchtest.

#### **FFmpeg (für Fortgeschrittene)**
- **FFmpeg** ist ein leistungsfähiges Kommandozeilen-Tool zur Medienbearbeitung. Es bietet die Möglichkeit, mehrere MP3-Dateien zu MP4-Videos zu konvertieren, indem man ein Skript verwendet.
- **Anleitung (Batch-Skript):**
  - Installiere **FFmpeg**.
  - Öffne die Eingabeaufforderung und verwende folgenden Befehl:
    ```bash
    for %i in (*.mp3) do ffmpeg -loop 1 -i image.jpg -i "%i" -c:v libx264 -c:a aac -strict experimental -b:a 192k -shortest "%~ni.mp4"
    ```
    - Ersetze `image.jpg` durch das Bild, das du als Hintergrund verwenden möchtest.

#### **Freemake Video Converter**
- **Freemake Video Converter** bietet ebenfalls die Möglichkeit, MP3-Dateien in MP4-Videos zu konvertieren. Es unterstützt das Hinzufügen von Hintergrundbildern und die Konvertierung mehrerer Dateien gleichzeitig.
- **Hinweis**: Die kostenlose Version hat ein Wasserzeichen. Um dies zu entfernen, musst du die Vollversion kaufen.

### 2. **Online-Bulk-Konvertierungstools**
Es gibt auch Online-Tools, die mehrere MP3-Dateien gleichzeitig umwandeln können. Beachte, dass die kostenlose Version meist eine Begrenzung der Dateigröße hat.

#### **Online-Convert.com**
- Dieses Tool ermöglicht es dir, mehrere Dateien hochzuladen und diese gleichzeitig in MP4 zu konvertieren.
- Du kannst auch ein statisches Bild hinzufügen, das im Video angezeigt wird.
- **Hinweis**: Die kostenlose Version hat eine Dateigrößenbegrenzung.

#### **Convertio**
- **Convertio** bietet eine einfache Möglichkeit, mehrere MP3-Dateien in MP4-Dateien umzuwandeln.
- Es ist einfach zu bedienen, kann jedoch ebenfalls durch eine maximale Dateigröße eingeschränkt sein.

### 3. **Spezielle Batch-Konvertierungssoftware**
- Es gibt spezielle Tools, die für die Batch-Konvertierung großer Mengen an Dateien entwickelt wurden.

#### **Xilisoft Video Converter**
- **Xilisoft** bietet die Möglichkeit, mehrere MP3-Dateien mit einem statischen Bild in MP4 umzuwandeln. Es ist benutzerfreundlich und bietet viele Anpassungsoptionen.
  
#### **Any Video Converter**
- **Any Video Converter** ist eine Software, die es dir ermöglicht, mehrere Dateien in verschiedenen Formaten in einem Schritt zu konvertieren. Es ist einfach zu bedienen und ermöglicht das Hinzufügen von Standbildern für die MP3-Dateien.

### Empfehlung
- Wenn du eine einfache und schnelle Lösung ohne Installation suchst, empfehle ich **Online-Convert.com** oder **Convertio**.
- Für erweiterte Kontrolle und eine kostenlose Lösung auf deinem Desktop ist **FFmpeg** sehr leistungsstark, wenn auch etwas technischer.
- Wenn du regelmäßig viele Dateien konvertieren möchtest, wäre ein Desktop-Programm wie **Any Video Converter** oder **Freemake Video Converter** eine gute Wahl.

Für alle diese Optionen solltest du das Bild hinzufügen, das du als Hintergrund für die MP3s verwenden möchtest, damit sie wie ein richtiges Video auf YouTube angezeigt werden.
