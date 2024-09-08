# Idee für eine Web- und Spiel-Erfahrung!

Hier ist eine Struktur, die deinem gewünschten Ablauf entspricht:

### Aufbau:

1. **Index-Seite (`index.html`)**: Diese Seite dient als kurze Einführungsseite, die nach einigen Sekunden automatisch zur Übersicht-Seite (`uebersicht.html`) wechselt.
   
2. **Übersicht-Seite (`uebersicht.html`)**: Diese Seite zeigt die Schaltflächen, die zu den Unity-Spielen führen. Die Schaltflächen erscheinen langsam.

3. **Unity-Spiel-Seiten (`spiel1.html`, `spiel2.html`, usw.)**: Jede dieser Seiten lädt das jeweilige Unity-Spiel. Nach Beenden des Spiels gelangt man durch einen Button zurück zur `index.html`.

Hier ist der Code für den gesamten Aufbau:

### 1. `index.html`

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Willkommen</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
        }
        h1 {
            font-size: 3rem;
        }
    </style>
</head>
<body>
    <h1>Willkommen!</h1>

    <script>
        // Nach 3 Sekunden zur Übersicht wechseln
        setTimeout(() => {
            window.location.href = 'uebersicht.html';
        }, 3000); // 3000 ms = 3 Sekunden
    </script>
</body>
</html>
```

### 2. `uebersicht.html`

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Übersicht</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }

        button {
            padding: 10px 20px;
            margin: 10px;
            font-size: 16px;
            cursor: pointer;
            opacity: 0; /* Start mit Unsichtbarkeit */
            transition: opacity 1s; /* Weiche Einblendung */
        }

        .visible {
            opacity: 1; /* Sichtbarkeit */
        }
    </style>
</head>
<body>

    <h1>Übersicht</h1>
    <p>Wähle ein Spiel aus:</p>

    <!-- Buttons für die Spiele -->
    <button class="fade-in" onclick="window.location.href='spiel1.html'">Spiel 1</button>
    <button class="fade-in" onclick="window.location.href='spiel2.html'">Spiel 2</button>
    <button class="fade-in" onclick="window.location.href='spiel3.html'">Spiel 3</button>

    <script>
        // Warte eine Sekunde, bevor die Knöpfe erscheinen
        window.onload = function() {
            setTimeout(() => {
                document.querySelectorAll('.fade-in').forEach(button => {
                    button.classList.add('visible');
                });
            }, 1000); // 1000 ms = 1 Sekunde
        }
    </script>

</body>
</html>
```

### 3. Beispiel für eine Spiel-Seite (`spiel1.html`)

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spiel 1</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <!-- Hier wird das Unity-Spiel eingebettet -->
    <iframe src="unitygame/index.html" width="800" height="600"></iframe>

    <!-- Knopf zurück zur Index-Seite -->
    <button onclick="window.location.href='index.html'">Zurück zur Startseite</button>

</body>
</html>
```

### Erklärung:
- **`index.html`**: Zeigt eine kurze Begrüßung und leitet nach 3 Sekunden automatisch zur Übersicht weiter.
- **`uebersicht.html`**: Enthält die Knöpfe zu den Spielen, die langsam nach einer Sekunde sichtbar werden.
- **`spiel1.html` (und weitere `spielX.html` Seiten)**: Lädt ein Unity-Spiel in einem `<iframe>` und bietet einen Knopf, um nach dem Spielen zurück zur Startseite zu gelangen.

Jeder der Unity-Spiele kann durch den entsprechenden Link aufgerufen werden und sorgt so für eine einfache Navigation zwischen den Spielen und der Hauptseite. Passt das so für dich, oder sollen wir noch etwas anpassen?
