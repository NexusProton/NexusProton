# Debugging Tipps Unity

Beim Debugging in Unity gibt es viele interessante und nützliche Funktionen, die oft übersehen werden und die das Arbeiten erheblich erleichtern können. Hier sind einige spannende Techniken und Tools:

### 1. **Conditional Breakpoints (Bedingte Haltepunkte)**
   - Statt den Debugger an jedem Durchlauf zu stoppen, kannst du **bedingte Breakpoints** setzen, die nur dann ausgelöst werden, wenn eine bestimmte Bedingung erfüllt ist (z. B. `x == 5`).
   - Rechtsklick auf einen Breakpoint > „Bedingung…“ und eine Bedingung wie `myVariable == 5` hinzufügen.

### 2. **Immediate Window und Watch-Fenster**
   - Über das **Immediate Window** (`Ctrl + Alt + I`) kannst du Variablen abfragen oder sogar Code ausführen, um Änderungen live zu testen. Du kannst beispielsweise `myVariable = 10` eingeben, um die Variable im laufenden Programm zu ändern.
   - Im **Watch-Fenster** kannst du Variablen über mehrere Frames hinweg beobachten und ihren Zustand verfolgen.

### 3. **Log-Punkte statt Breakpoints**
   - Du kannst **Log-Punkte** verwenden, um Werte ohne komplettes Anhalten des Programms zu überprüfen. In Visual Studio kannst du durch Rechtsklick auf einen Breakpoint `Action > Print a Message` auswählen, um automatisch Debug-Informationen zu schreiben, ohne das Programm zu stoppen.
   - Unity selbst hat zudem den `Debug.Log()`-Befehl, den du zum Protokollieren in der Konsole verwenden kannst.

### 4. **Step Through und Step Into**
   - Mit `Step Over (F10)` kannst du eine Zeile Code ausführen, ohne in Funktionen zu gehen. Mit `Step Into (F11)` kannst du in eine Funktion gehen, um deren inneren Ablauf zu verfolgen. `Step Out (Shift + F11)` lässt dich aus der Funktion zurück in den aufrufenden Code springen.
   - Sehr nützlich, wenn du wissen möchtest, wie eine Funktion im Detail funktioniert, ohne deinen Debugging-Prozess zu unterbrechen.

### 5. **Hot Reload (Edit and Continue)**
   - Unity und Visual Studio unterstützen **Edit and Continue**, das es dir ermöglicht, den Code während des Debuggens zu ändern und direkt weiterlaufen zu lassen, ohne das Spiel neu zu starten. Besonders hilfreich bei kleinen Anpassungen, die du sofort testen möchtest.

### 6. **Debug.DrawLine und Debug.DrawRay**
   - In Unity kannst du mit **`Debug.DrawLine`** oder **`Debug.DrawRay`** visuelle Debugging-Informationen in der Szene darstellen. Dies ist besonders nützlich, um Pfade, Richtungen oder Trigger-Bereiche anzuzeigen.
   ```csharp
   Debug.DrawLine(startPosition, endPosition, Color.red, 2f);
   Debug.DrawRay(transform.position, transform.forward * 10, Color.green);
   ```

### 7. **Unity Profiler**
   - Der Unity **Profiler** bietet detaillierte Einblicke in die Leistung deines Spiels, wie CPU-, GPU-, Speicher- und Netzwerk-Auslastung. Damit kannst du Engpässe aufspüren und herausfinden, wo der größte Performance-Verlust entsteht.
   - Besonders nützlich, wenn das Spiel langsam läuft und du die Ursache finden musst.

### 8. **Deep Profiling**
   - Der **Deep Profiling Mode** in Unity geht noch tiefer und zeigt Informationen zu jeder Funktion an, die ausgeführt wird. Dies ist extrem leistungsintensiv, kann aber helfen, Performance-Probleme auf Funktionsebene zu identifizieren.
   - Deep Profiling ist in den Editor-Einstellungen des Profilers aktivierbar.

### 9. **Frame Debugger**
   - Der **Frame Debugger** (unter Window > Analysis > Frame Debugger) erlaubt dir, jeden Frame deines Spiels Schritt für Schritt durchzugehen und zu sehen, wie Unity das Bild rendert. Du kannst überprüfen, wann und warum bestimmte Objekte gezeichnet werden und wie Shading, Texturen und Post-Processing angewendet werden.
   - Ideal für grafische Probleme oder Performance-Bugs im Rendering.

### 10. **Custom Debugging Scripts**
   - Du kannst eigene Debugging-Tools schreiben. Beispielsweise könnte ein kleines Tool in deinem Spiel Debug-Informationen anzeigen oder es dir ermöglichen, Einstellungen während der Laufzeit anzupassen (z. B. `DebugConsole`, um Variablen oder Flags direkt zu ändern).

### 11. **Logging von Call Stacks**
   - Wenn du wissen möchtest, wie du in eine bestimmte Funktion gekommen bist, kannst du `Debug.LogError()` verwenden, um auch den Call Stack zu protokollieren. Dadurch siehst du den Pfad der Funktionsaufrufe, der zu einem bestimmten Punkt geführt hat:
   ```csharp
   Debug.LogError("Fehler hier aufgetreten", this);
   ```

### 12. **Physics Debugger**
   - Unity hat auch einen **Physics Debugger**, den du unter „Window > Analysis > Physics Debugger“ findest. Er zeigt dir die Collider und Rigidbody-Komponenten in der Szene, sodass du überprüfen kannst, ob Physik-Komponenten korrekt platziert sind und wie sie miteinander interagieren.

Mit diesen Tools und Tricks hast du mehr Kontrolle und Einblicke in deinen Code, sodass das Debuggen wesentlich leichter wird. Wenn du zu einem bestimmten Tool mehr wissen willst, kann ich gern ins Detail gehen!
