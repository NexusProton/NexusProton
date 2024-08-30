# Unterschiedliche Bilder auf jeder Würfelseite (Unity)

Um sicherzustellen, dass jeder Würfel (Tile) in Unity unterschiedliche Bilder auf seinen sechs Seiten hat, müssen die Materialien auf eine spezielle Weise angewendet werden. Das Problem entsteht, weil der Unity-Würfel standardmäßig nur einen Materialslot hat, der alle sechs Seiten gleich texturiert. Hier sind die Schritte, um jeden Würfel mit sechs unterschiedlichen Bildern zu versehen:

### Schritt-für-Schritt-Anleitung: Unterschiedliche Bilder auf jeder Würfelseite

1. **Custom Cube Model mit UV Mapping (empfohlen)**: Erstelle ein benutzerdefiniertes Würfelmodell in einem 3D-Modellierungsprogramm (z.B. Blender), das jede Seite separat UV-gemappt hat. Dies ermöglicht es, verschiedene Texturen auf jede Seite des Würfels zu legen. Wenn du Blender oder ein anderes 3D-Programm nicht verwenden möchtest, gehe zum nächsten Schritt.

2. **Verwendung von Unity's Standard-Würfel mit Material-Workaround:**

### Methode ohne 3D-Modellierungsprogramm

1. **Würfel erstellen:**
   - Erstelle in Unity einen Standardwürfel (`GameObject -> 3D Object -> Cube`).

2. **Materialien für jede Seite erstellen:**
   - Erstelle sechs Materialien (Rechtsklick im Assets-Ordner -> `Create -> Material`), z.B. `MaterialTop`, `MaterialBottom`, `MaterialFront`, `MaterialBack`, `MaterialLeft`, `MaterialRight`.
   - Füge jedem Material die jeweilige Textur/Bild hinzu, das auf die jeweilige Würfelseite soll, indem du die Textur auf das Albedo-Feld des Materials ziehst.

3. **Custom Shader für Würfel erstellen:**
   - Damit jede Seite unterschiedliche Bilder anzeigen kann, erstellen wir einen Shader, der dies ermöglicht:

   **Erstelle einen neuen Shader:**
   - Rechtsklick im Assets-Ordner -> `Create -> Shader -> Shader Graph -> URP Lit Shader Graph` (wenn URP verwendet wird) oder `Standard Surface Shader`.
   - Benenne den Shader z.B. `CubeSideShader`.

4. **Shader-Setup für Würfelseiten:**
   
   Verwende den folgenden Shader-Code, wenn du keinen Shader Graph benutzen möchtest und Standard Shader bevorzugst:

   ```csharp
   Shader "Custom/CubeSideShader"
   {
       Properties
       {
           _TopTex ("Top Texture", 2D) = "white" {}
           _BottomTex ("Bottom Texture", 2D) = "white" {}
           _FrontTex ("Front Texture", 2D) = "white" {}
           _BackTex ("Back Texture", 2D) = "white" {}
           _LeftTex ("Left Texture", 2D) = "white" {}
           _RightTex ("Right Texture", 2D) = "white" {}
       }
       SubShader
       {
           Tags { "RenderType"="Opaque" }
           LOD 200

           Pass
           {
               CGPROGRAM
               #pragma vertex vert
               #pragma fragment frag

               struct appdata
               {
                   float4 vertex : POSITION;
                   float3 normal : NORMAL;
               };

               struct v2f
               {
                   float4 pos : SV_POSITION;
                   float3 normal : TEXCOORD0;
               };

               sampler2D _TopTex;
               sampler2D _BottomTex;
               sampler2D _FrontTex;
               sampler2D _BackTex;
               sampler2D _LeftTex;
               sampler2D _RightTex;

               fixed4 frag(v2f i) : SV_Target
               {
                   // Placeholder logic for mapping based on normal, adjust as needed
                   fixed4 col = fixed4(1,1,1,1);

                   if (i.normal.y > 0.5) col = tex2D(_TopTex, i.normal.xy); // Top
                   else if (i.normal.y < -0.5) col = tex2D(_BottomTex, i.normal.xy); // Bottom
                   else if (i.normal.z > 0.5) col = tex2D(_FrontTex, i.normal.xy); // Front
                   else if (i.normal.z < -0.5) col = tex2D(_BackTex, i.normal.xy); // Back
                   else if (i.normal.x > 0.5) col = tex2D(_RightTex, i.normal.xy); // Right
                   else if (i.normal.x < -0.5) col = tex2D(_LeftTex, i.normal.xy); // Left

                   return col;
               }
               ENDCG
           }
       }
   }
   ```

5. **Wende den Shader auf den Würfel an:**
   - Erstelle ein Material und setze dessen Shader auf „Custom/CubeSideShader“.
   - Weise diesem Material die sechs verschiedenen Texturen zu.

6. **Material dem Würfel zuweisen:**
   - Weise das erstellte Material deinem Würfel zu.

### 3. **Kamera und Steuerung**:
   
- Stelle sicher, dass deine Kamera korrekt positioniert ist und der Spieler senkrecht auf das Spielfeld schaut, z.B., Kamera-Position `(5, 15, 5)` und Rotation `(90, 0, 0)`.

Mit diesen Schritten wird jeder Würfel auf jeder Seite unterschiedliche Bilder anzeigen, und der Shader steuert, welche Textur auf welcher Seite angezeigt wird.
