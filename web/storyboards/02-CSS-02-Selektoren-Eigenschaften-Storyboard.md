# Storyboard: CSS – Selektoren und Eigenschaften

## Video-Übersicht
- **Gesamtdauer:** ca. 8-9 Minuten
- **Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ
- **Lernziele:** CSS-Selektoren verstehen und Eigenschaften gezielt anwenden

---

## Szene 1: Einführung – Was sind Selektoren?

**Sprechertext:** „CSS-Selektoren sind wie Adressen: Sie sagen dem Browser, welche HTML-Elemente du stylen möchtest. Es gibt verschiedene Arten von Selektoren – vom einfachen Element-Selektor bis zu komplexen Kombinationen."

**Bildschirmdarstellung:** 
- Zeige Portfolio-Seite mit verschiedenen Elementen
- Markiere nacheinander: Alle `<h2>`, dann alle `.card`, dann `#header`
- Zeige, wie unterschiedliche Selektoren verschiedene Elemente ansprechen

**Dauer:** 30 Sekunden

---

## Szene 2: Element-Selektoren – Die Grundlage

**Sprechertext:** „Element-Selektoren sprechen alle Elemente eines Typs an. Wenn du `h1` stylst, werden alle Überschriften der ersten Ebene formatiert. Das ist praktisch für konsistentes Design, aber manchmal zu unspezifisch."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
h1 {
    color: #376B8C;
    font-size: 48px;
}

p {
    color: #666;
    line-height: 1.6;
}
```
Browser-Vorschau: Alle `<h1>` und `<p>` werden gestylt

**Dauer:** 35 Sekunden

---

## Szene 3: Klassen-Selektoren – Wiederverwendbar

**Sprechertext:** „Klassen-Selektoren beginnen mit einem Punkt und können mehrfach verwendet werden. Du vergibst im HTML eine class und stylst sie in CSS. Das macht dein Design flexibel und wiederverwendbar."

**Bildschirmdarstellung:** 
HTML zeigt:
```html
<article class="card">...</article>
<article class="card">...</article>
```

CSS zeigt:
```css
.card {
    background-color: #F8F8F8;
    padding: 20px;
    border-radius: 8px;
}
```
Browser-Vorschau: Beide Cards haben denselben Stil

**Dauer:** 40 Sekunden

---

## Szene 4: ID-Selektoren – Einmalig

**Sprechertext:** „ID-Selektoren beginnen mit einer Raute und sollten nur einmal pro Seite verwendet werden. Sie sind sehr spezifisch und überschreiben andere Styles. Nutze IDs sparsam – meistens sind Klassen die bessere Wahl."

**Bildschirmdarstellung:** 
HTML zeigt:
```html
<header id="main-header">...</header>
```

CSS zeigt:
```css
#main-header {
    background-color: #376B8C;
    height: 80px;
}
```
Browser-Vorschau: Nur dieser eine Header wird gestylt

**Dauer:** 35 Sekunden

---

## Szene 5: Verschachtelte Selektoren – Gezielt ansprechen

**Sprechertext:** „Mit Leerzeichen kombinierst du Selektoren. `header h1` bedeutet: Style alle h1, die innerhalb eines headers stehen. So kannst du sehr gezielt formatieren, ohne überall Klassen zu vergeben."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
header h1 {
    color: white;
}

main h1 {
    color: #376B8C;
}
```
Browser-Vorschau: h1 im Header ist weiss, h1 im Main ist blau

**Dauer:** 35 Sekunden

---

## Szene 6: Multiple Selektoren – Effizient stylen

**Sprechertext:** „Wenn mehrere Elemente denselben Stil brauchen, trennst du sie mit Komma. Das spart Schreibarbeit und macht dein CSS übersichtlicher."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
h1, h2, h3 {
    font-family: Arial, sans-serif;
    color: #376B8C;
}
```
Browser-Vorschau: Alle drei Überschriftenebenen haben denselben Font und Farbe

**Dauer:** 30 Sekunden

---

## Szene 7: Das Box-Modell – Abstände verstehen

**Sprechertext:** „Jedes HTML-Element ist eine Box mit Inhalt, Padding, Border und Margin. Padding ist Abstand nach innen, Margin nach aussen. Das Box-Modell ist zentral für CSS-Layouts."

**Bildschirmdarstellung:** 
- Zeige Box-Modell-Diagramm mit farblich markierten Bereichen
- Code-Editor zeigt:
```css
.card {
    padding: 20px;      /* Innen */
    margin: 10px;       /* Aussen */
    border: 2px solid #376B8C;
}
```
- DevTools: Zeige Box-Modell-Inspektor

**Dauer:** 45 Sekunden

---

## Szene 8: Farben – Verschiedene Formate

**Sprechertext:** „CSS unterstützt verschiedene Farbformate: Hex-Codes, RGB, HSL und Farbnamen. Hex ist am verbreitetsten, RGBA ermöglicht Transparenz. Wähle, was für dich am intuitivsten ist."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
h1 {
    color: #376B8C;              /* Hex */
    color: rgb(55, 107, 140);    /* RGB */
    color: rgba(55, 107, 140, 0.8); /* RGBA mit Transparenz */
    color: hsl(200, 44%, 38%);   /* HSL */
}
```
Browser-Vorschau: Zeige visuell identische Farben

**Dauer:** 40 Sekunden

---

## Szene 9: Schrift-Eigenschaften – Typografie gestalten

**Sprechertext:** „Mit font-family wählst du Schriftarten, mit font-size die Grösse, mit font-weight die Dicke. line-height bestimmt den Zeilenabstand. Gute Typografie macht Texte lesbarer und professioneller."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
body {
    font-family: Arial, sans-serif;
    font-size: 16px;
    line-height: 1.6;
}

h1 {
    font-size: 48px;
    font-weight: bold;
    letter-spacing: 1px;
}
```
Browser-Vorschau: Zeige Unterschiede in Schriftgrösse und -dicke

**Dauer:** 40 Sekunden

---

## Szene 10: Text-Ausrichtung und Dekoration

**Sprechertext:** „Text-align richtet Text aus, text-decoration fügt Unter- oder Überstreichungen hinzu. text-transform ändert Gross- und Kleinschreibung. Diese Eigenschaften verfeinern dein Design."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
h1 {
    text-align: center;
}

a {
    text-decoration: none;
}

.uppercase {
    text-transform: uppercase;
}
```
Browser-Vorschau: Zeige zentrierten Text, unterstrichene Links, Uppercase-Text

**Dauer:** 35 Sekunden

---

## Szene 11: Spezifität – Welcher Style gewinnt?

**Sprechertext:** „Wenn mehrere Regeln dasselbe Element ansprechen, entscheidet die Spezifität. IDs sind stärker als Klassen, Klassen stärker als Elemente. Inline-Styles überschreiben alles. Verstehe Spezifität, um Bugs zu vermeiden."

**Bildschirmdarstellung:** 
CSS zeigt:
```css
h1 { color: blue; }              /* Spezifität: 1 */
.title { color: green; }         /* Spezifität: 10 */
#main-title { color: red; }      /* Spezifität: 100 */
```
HTML zeigt:
```html
<h1 id="main-title" class="title">Welche Farbe?</h1>
```
Browser-Vorschau: h1 ist rot (ID gewinnt)

**Dauer:** 45 Sekunden

---

## Szene 12: DevTools – CSS live ändern

**Sprechertext:** „Die Browser-DevTools sind dein bester Freund. Öffne sie mit F12, wähle ein Element aus und ändere CSS-Eigenschaften live. Experimentiere, bis es passt, und kopiere dann den Code in deine Datei."

**Bildschirmdarstellung:** 
- Zeige Portfolio-Seite
- F12 drücken → Elements-Tab
- Element auswählen → Styles-Panel
- Farbe ändern → sofortige Änderung im Browser
- Hinweis: Änderungen sind temporär

**Dauer:** 40 Sekunden

---

## Szene 13: Best Practices – Sauberes CSS

**Sprechertext:** „Nutze Klassen statt IDs für Styles. Halte Selektoren einfach. Gruppiere verwandte Styles zusammen. Kommentiere komplexe Bereiche. Sauberes CSS ist wartbar und erweiterbar."

**Bildschirmdarstellung:** 
Vergleichstabelle:

| ✅ Gut | ❌ Schlecht |
|--------|-------------|
| `.card { ... }` | `#card-1 { ... }` |
| `header nav { ... }` | `body header nav ul li a { ... }` |
| Kommentare nutzen | Keine Struktur |

**Dauer:** 35 Sekunden

---

## Szene 14: Zusammenfassung & Ausblick

**Sprechertext:** „Zusammengefasst: Selektoren wählen Elemente aus, Eigenschaften definieren das Aussehen. Element-, Klassen- und ID-Selektoren haben unterschiedliche Stärken. Das Box-Modell regelt Abstände. Im nächsten Schritt lernst du fortgeschrittene Layouts mit Flexbox und Grid. Viel Erfolg!"

**Bildschirmdarstellung:** 
Zusammenfassung mit Icons:
- Element-Selektor: `h1 { }`
- Klassen-Selektor: `.card { }`
- ID-Selektor: `#header { }`
- Box-Modell: Content → Padding → Border → Margin

**Dauer:** 30 Sekunden

---

## Benötigte Ressourcen für Video-Produktion

### Code-Beispiele
1. **selectors-demo.html** – Portfolio mit verschiedenen Selektoren
2. **styles.css** – Stylesheet mit kommentierten Beispielen
3. **box-model-demo.html** – Demonstration des Box-Modells

### Grafiken / Animationen
- Box-Modell-Diagramm (Content, Padding, Border, Margin)
- Spezifitäts-Pyramide (Element < Klasse < ID < Inline)
- Farbformat-Vergleichstabelle

### Browser-Demonstrationen
- DevTools Elements-Tab mit Live-Editing
- Box-Modell-Inspektor in DevTools
- Computed Styles Panel

### Visuelles Design
- Split-Screen: Code links, Browser-Vorschau rechts
- Highlighting von Selektoren und Eigenschaften
- Farbige Markierungen für verschiedene Selektor-Typen

---

## Lernziele (nach Video)

Nach diesem Video können Lernende:
- Element-, Klassen- und ID-Selektoren unterscheiden und korrekt einsetzen
- Verschachtelte Selektoren schreiben und verstehen
- Das Box-Modell (margin, padding, border) erklären und anwenden
- Farben in verschiedenen Formaten (Hex, RGB, RGBA) definieren
- Schrift-Eigenschaften (font-family, font-size, font-weight) nutzen
- Die Spezifität von CSS-Regeln verstehen
- DevTools für CSS-Experimente verwenden

---

**Gesamtdauer:** ca. 8-9 Minuten  
**Schnitt-Hinweise:** Häufig zwischen Code-Editor und Browser wechseln. Bei Box-Modell und Spezifität visuelle Diagramme einblenden. DevTools-Demo langsam und deutlich zeigen.
