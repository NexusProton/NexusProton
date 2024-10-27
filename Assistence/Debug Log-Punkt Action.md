# Debug Log-Punkt Action
Neben der Aktion **"Print a Message"** gibt es noch einige weitere interessante Aktionen, die du für Breakpoints in Visual Studio konfigurieren kannst. Diese erweiterten Optionen helfen dir dabei, das Debugging anzupassen, ohne das Programm ständig anzuhalten. Hier sind einige nützliche Aktionen:

### 1. **Continue Execution (Fortsetzen der Ausführung)**
   - Diese Option erlaubt es dir, **automatisch weiterzumachen**, nachdem ein Breakpoint erreicht wurde, ohne dass das Programm angehalten wird.
   - Dies ist nützlich, wenn du nur eine Meldung protokollieren möchtest, ohne dass der Debugger das Programm unterbricht. So kannst du kontinuierlich Informationen protokollieren, ohne das Programmfluss zu stören.

### 2. **Log Call Stack (Protokollierung des Aufrufstapels)**
   - Du kannst den **aktuellen Call Stack** (Aufrufkette der Funktionen) in der Konsole oder im Protokoll ausgeben lassen, wenn der Breakpoint erreicht wird.
   - Dies ist besonders hilfreich, wenn du nachverfolgen möchtest, wie das Programm zu diesem Punkt gelangt ist, ohne manuell den Call Stack zu prüfen.

### 3. **Evaluate and Log (Ausdruck auswerten und protokollieren)**
   - Diese Option ermöglicht es dir, **bestimmte Ausdrücke oder Variablen** zu evaluieren und den resultierenden Wert zu protokollieren.
   - Du kannst zum Beispiel `myVariable + 10` oder `someObject.property` auswerten und das Ergebnis direkt im Protokoll anzeigen lassen. Damit kannst du den Wert eines bestimmten Ausdrucks überprüfen, ohne zusätzliche `Debug.Log()`-Befehle in deinen Code einzubauen.

### 4. **Conditional Breakpoints (Bedingte Breakpoints)**
   - Mit bedingten Breakpoints kannst du festlegen, dass der Breakpoint **nur dann ausgelöst** wird, wenn eine bestimmte Bedingung erfüllt ist (z. B. `count > 100`).
   - Diese Bedingung lässt sich auch zusammen mit den anderen Aktionen wie "Print a Message" kombinieren, um spezifische Debugging-Meldungen nur in bestimmten Fällen zu protokollieren.

### 5. **Hit Count (Trefferanzahl festlegen)**
   - Mit der "Hit Count"-Option kannst du festlegen, dass der Breakpoint **nur nach einer bestimmten Anzahl von Treffern** ausgelöst wird.
   - Zum Beispiel kann der Breakpoint so eingestellt werden, dass er erst beim zehnten Mal angehalten wird. Dies ist besonders nützlich, wenn eine Schleife oder ein Abschnitt im Code häufig durchlaufen wird und du nur ein bestimmtes Mal anhalten willst.

### 6. **Object ID setzen (nur in .NET)**
   - Visual Studio erlaubt es dir, einem Objekt eine eindeutige **Objekt-ID** zuzuweisen, wenn der Breakpoint ausgelöst wird.
   - Dies ist nützlich, um den Zustand eines bestimmten Objekts während des Debuggens zu verfolgen, insbesondere in Situationen, in denen du mit mehreren Instanzen arbeitest und die Werte einzelner Objekte überwachen möchtest.

### 7. **Remove Breakpoint after Hit (Breakpoint nach Treffer entfernen)**
   - Du kannst einstellen, dass der Breakpoint **automatisch entfernt wird**, nachdem er einmal ausgelöst wurde.
   - Das ist besonders praktisch, wenn du nur einmalig an einer bestimmten Stelle anhalten und dann weitermachen möchtest, ohne den Breakpoint manuell zu löschen.

### 8. **Tracepoint (Rückverfolgbare Meldungen)**
   - Tracepoints sind eine spezielle Art von Breakpoints, die dazu dienen, **automatisierte Debug-Nachrichten** ohne das Anhalten des Codes zu erzeugen.
   - Sie können z. B. kontinuierlich Variablenwerte protokollieren, ähnlich wie „Print a Message“, und geben dir damit eine detaillierte Nachverfolgung, ohne den Debugger zu unterbrechen.

Diese Aktionen und erweiterten Einstellungen können dir viel Zeit sparen und dir helfen, den Ablauf deines Programms besser zu verstehen, ohne die Ausführung ständig anzuhalten.
