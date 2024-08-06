Um das Spiel "Garden Keeper A.I." als Referenz auf deine Website zu bringen, gibt es einige Schritte, die du befolgen kannst:

### 1. Vorbereitung
Stelle sicher, dass du alle notwendigen Dateien des Spiels "Garden Keeper A.I." zur Verfügung hast. Dies könnten HTML-, CSS-, JavaScript-Dateien oder ein Unity-WebGL-Build sein.

### 2. Spiel hochladen
Lade das Spiel auf deinen Webserver hoch. Falls es sich um einen Unity-WebGL-Build handelt, solltest du die gesamten Build-Dateien in einen separaten Ordner hochladen, z.B. `garden_keeper_ai`.

### 3. Integration des Spiels auf der Website
Erstelle eine neue Seite oder einen neuen Bereich auf deiner bestehenden Website, um das Spiel zu präsentieren.

#### Beispiel für eine HTML-Seite:
Falls es sich um ein Unity-WebGL-Spiel handelt, kannst du es wie folgt einbetten:

**index.html**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Garden Keeper A.I.</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Garden Keeper A.I.</h1>
        <p>Sammle Punkte, pass auf die KI-Wächter auf!</p>
    </header>
    <main>
        <div class="unity-container">
            <div id="unity-canvas"></div>
        </div>
    </main>
    <footer>
        <p>Ein Spiel von Sahin A.I. Tech</p>
    </footer>
    <script src="Build/UnityLoader.js"></script>
    <script>
        var buildUrl = "Build";
        var loaderUrl = buildUrl + "/{{BuildFileName}}.json";
        var config = {
            dataUrl: buildUrl + "/{{BuildFileName}}.data",
            frameworkUrl: buildUrl + "/{{BuildFileName}}.framework.js",
            codeUrl: buildUrl + "/{{BuildFileName}}.wasm",
            streamingAssetsUrl: "StreamingAssets",
            companyName: "Sahin A.I. Tech",
            productName: "Garden Keeper A.I.",
            productVersion: "1.0",
        };

        var container = document.querySelector("#unity-canvas");
        var canvas = document.createElement("canvas");
        container.appendChild(canvas);

        UnityLoader.instantiate("unity-canvas", loaderUrl, config);
    </script>
</body>
</html>
```

#### Beispiel für eine CSS-Datei:
**style.css**
```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    text-align: center;
}

header {
    background-color: #333;
    color: #fff;
    padding: 20px;
}

main {
    padding: 20px;
}

.unity-container {
    width: 960px;
    height: 600px;
    margin: 0 auto;
    background: #000;
}

footer {
    background-color: #333;
    color: #fff;
    padding: 10px;
    position: fixed;
    bottom: 0;
    width: 100%;
}
```

### 4. Navigation hinzufügen
Füge auf deiner Startseite einen Link hinzu, der zu dieser neuen Seite führt.

**Beispiel für die Startseite:**
```html
<a href="garden_keeper_ai.html">Garden Keeper A.I.</a>
```

### 5. Testen
Stelle sicher, dass das Spiel korrekt auf der neuen Seite geladen wird und getestet werden kann.

### 6. Beschreibung und Details hinzufügen
Auf der Seite, auf der das Spiel eingebettet ist, füge eine kurze Beschreibung des Spiels und dessen Funktionen hinzu.

### Beispielbeschreibung:
```html
<header>
    <h1>Garden Keeper A.I.</h1>
    <p>Sammle Punkte, pass auf die KI-Wächter auf! Steuere deinen Charakter durch den Garten, sammle alle Gegenstände ein und weiche den KI-Wächtern aus. Ein spannendes Spiel von Sahin A.I. Tech.</p>
</header>
```

### Zusammenfassung
Durch das Einbetten eines Spiels wie "Garden Keeper A.I." auf deiner Website kannst du ein interaktives und spannendes Element hinzufügen, das die Besucher länger auf deiner Seite hält und dein Portfolio als Game-Developer unterstreicht.
