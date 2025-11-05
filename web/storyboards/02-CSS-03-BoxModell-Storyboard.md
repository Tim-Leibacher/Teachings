# Storyboard: CSS Box-Modell & Layout

## Video-Übersicht
- **Gesamtdauer:** ca. 7-8 Minuten
- **Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ
- **Lernziele:** Box-Modell verstehen, Abstände kontrollieren, Block vs. Inline-Elemente unterscheiden

---

## Szene 1: Einführung – Jedes Element ist eine Box

**Sprechertext:** „In CSS wird jedes HTML-Element als rechteckige Box dargestellt. Egal ob Text, Bild oder Container – alles ist eine Box. Das Verständnis dieses Box-Modells ist fundamental für jedes Layout."

**Bildschirmdarstellung:** 
- Zeige eine einfache Webseite
- Aktiviere in DevTools (F12) die Box-Modell-Visualisierung
- Alle Elemente werden als farbige Rechtecke angezeigt

**Dauer:** 30 Sekunden

---

## Szene 2: Die vier Bereiche des Box-Modells

**Sprechertext:** „Jede Box besteht aus vier Bereichen: Content (der Inhalt selbst), Padding (Innenabstand), Border (Rahmen) und Margin (Aussenabstand). Diese Bereiche bestimmen die Gesamtgrösse und Position des Elements."

**Bildschirmdarstellung:** 
Grafik/Animation zeigt:
```
┌─────────── MARGIN (transparent) ───────────┐
│ ┌─────────── BORDER ───────────┐           │
│ │ ┌─────────── PADDING ───────┐ │           │
│ │ │ ┌─────── CONTENT ───────┐ │ │           │
│ │ │ │   Text oder Bild      │ │ │           │
│ │ │ └───────────────────────┘ │ │           │
│ │ └───────────────────────────┘ │           │
│ └─────────────────────────────────┘           │
└───────────────────────────────────────────────┘
```

**Dauer:** 40 Sekunden

---

## Szene 3: Content – Der Inhalt

**Sprechertext:** „Der Content-Bereich enthält den tatsächlichen Inhalt – Text, Bilder oder andere Elemente. Mit width und height bestimmst du die Grösse dieses Bereichs."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
.box {
    width: 300px;
    height: 200px;
    background-color: lightblue;
}
```
Browser-Vorschau: Blaue Box mit Text

**Dauer:** 30 Sekunden

---

## Szene 4: Padding – Innenabstand

**Sprechertext:** „Padding ist der Innenabstand zwischen Content und Border. Er vergrössert die Box und übernimmt die Hintergrundfarbe. Du kannst Padding für alle vier Seiten einzeln oder gemeinsam setzen."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
.box {
    width: 300px;
    padding: 20px;
    background-color: lightblue;
}
```
Zeige im Browser: Box wird grösser, Text rückt nach innen
DevTools: Padding-Bereich grün hervorgehoben

**Dauer:** 40 Sekunden

---

## Szene 5: Border – Rahmen

**Sprechertext:** „Der Border ist der Rahmen um die Box. Er hat eine Farbe, Dicke und Stil. Der Border liegt zwischen Padding und Margin und vergrössert ebenfalls die Box."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid navy;
    background-color: lightblue;
}
```
Browser-Vorschau: Dunkler Rahmen um die Box
DevTools: Border-Bereich gelb hervorgehoben

**Dauer:** 35 Sekunden

---

## Szene 6: Margin – Aussenabstand

**Sprechertext:** „Margin ist der Aussenabstand zwischen Elementen. Er schafft Platz um die Box herum, ist aber transparent und übernimmt keine Hintergrundfarbe. Margins können sich zwischen Elementen überlappen – das nennt man Margin Collapsing."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid navy;
    margin: 30px;
    background-color: lightblue;
}
```
Browser-Vorschau: Abstand zwischen Boxen
DevTools: Margin-Bereich orange hervorgehoben

**Dauer:** 40 Sekunden

---

## Szene 7: Kurzschreibweisen für Abstände

**Sprechertext:** „Statt jede Seite einzeln zu definieren, kannst du Kurzschreibweisen nutzen. Ein Wert setzt alle Seiten, zwei Werte setzen oben-unten und links-rechts, vier Werte gehen im Uhrzeigersinn: oben, rechts, unten, links."

**Bildschirmdarstellung:** 
Code-Editor zeigt verschiedene Varianten:
```css
/* Alle Seiten gleich */
padding: 20px;

/* Oben-Unten: 20px, Links-Rechts: 40px */
padding: 20px 40px;

/* Oben: 10px, Rechts: 20px, Unten: 30px, Links: 40px */
padding: 10px 20px 30px 40px;

/* Einzelne Seiten */
padding-top: 10px;
padding-right: 20px;
```

**Dauer:** 45 Sekunden

---

## Szene 8: Box-Sizing – Die Grössenberechnung

**Sprechertext:** „Standardmässig addiert der Browser Padding und Border zur Width hinzu. Mit box-sizing: border-box bleiben Padding und Border innerhalb der definierten Breite – das erleichtert die Berechnung enorm."

**Bildschirmdarstellung:** 
Split-Screen Vergleich:

**Links (default):**
```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
}
/* Tatsächliche Breite: 350px */
```

**Rechts (border-box):**
```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
/* Tatsächliche Breite: 300px */
```

DevTools zeigt die Grössenunterschiede

**Dauer:** 45 Sekunden

---

## Szene 9: Display – Block vs. Inline vs. Inline-Block

**Sprechertext:** „Die Display-Eigenschaft bestimmt, wie Elemente dargestellt werden. Block-Elemente nehmen die volle Breite ein und erzwingen einen Zeilenumbruch. Inline-Elemente bleiben im Textfluss. Inline-Block kombiniert beides."

**Bildschirmdarstellung:** 
Drei Beispiele nebeneinander:

**Block:**
```css
div {
    display: block;
    background: lightblue;
}
```
Zeige: Elemente stapeln sich vertikal

**Inline:**
```css
span {
    display: inline;
    background: lightcoral;
}
```
Zeige: Elemente nebeneinander im Text

**Inline-Block:**
```css
div {
    display: inline-block;
    width: 150px;
    background: lightgreen;
}
```
Zeige: Boxen nebeneinander mit Width

**Dauer:** 50 Sekunden

---

## Szene 10: Margin Collapsing

**Sprechertext:** „Bei vertikalen Margins zwischen Block-Elementen überlappen sich die Abstände – der grössere Wert gewinnt. Das nennt man Margin Collapsing. Dieser Effekt tritt nur bei vertikalen Margins auf, nicht bei horizontalen."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
.box1 {
    margin-bottom: 30px;
}

.box2 {
    margin-top: 20px;
}
/* Abstand zwischen box1 und box2: 30px (nicht 50px!) */
```

Animation: Zwei Margins bewegen sich aufeinander zu und überlappen
DevTools: Visualisierung des Margin Collapsing

**Dauer:** 35 Sekunden

---

## Szene 11: DevTools – Box-Modell inspizieren

**Sprechertext:** „Die Browser DevTools sind dein bester Freund beim Debuggen. Im Elements-Tab siehst du das Box-Modell jedes Elements visuell. Orange ist Margin, grün ist Padding, gelb ist Border, blau ist Content. So findest du schnell Layout-Probleme."

**Bildschirmdarstellung:** 
- Öffne DevTools (F12)
- Klicke auf ein Element
- Zeige die Box-Modell-Visualisierung rechts unten
- Ändere Werte live und zeige sofortige Auswirkungen
- Hover über Elemente im HTML → Box-Modell wird auf der Seite hervorgehoben

**Dauer:** 40 Sekunden

---

## Szene 12: Praktisches Beispiel – Card Component

**Sprechertext:** „Zusammengefasst: Eine typische Card nutzt das Box-Modell perfekt. Padding für Innenabstand, Border für den Rahmen, Margin für Abstand zu anderen Cards. Mit box-sizing: border-box bleibt die Width berechenbar."

**Bildschirmdarstellung:** 
Code-Editor zeigt komplettes Beispiel:
```css
.card {
    /* Box-Sizing */
    box-sizing: border-box;
    
    /* Content */
    width: 300px;
    
    /* Padding */
    padding: 20px;
    
    /* Border */
    border: 2px solid #ccc;
    border-radius: 8px;
    
    /* Margin */
    margin: 20px;
    
    /* Visuals */
    background-color: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

Browser-Vorschau: Mehrere Cards nebeneinander
DevTools: Zeige alle vier Bereiche hervorgehoben

**Dauer:** 45 Sekunden

---

## Benötigte Ressourcen für Video-Produktion

### Code-Beispiele
1. **box-model-demo.html** – Einfache Box mit allen Bereichen
2. **display-comparison.html** – Block vs. Inline vs. Inline-Block
3. **margin-collapsing.html** – Demonstration von Margin Collapsing
4. **card-component.html** – Praktisches Beispiel

### Grafiken / Animationen
- Box-Modell-Diagramm (Content, Padding, Border, Margin)
- Animation: Box-Modell aufbauen (Layer für Layer)
- Vergleich: `box-sizing: content-box` vs `border-box`
- Margin Collapsing Animation

### DevTools-Demonstrationen
- Box-Modell-Visualisierung in Browser DevTools
- Live-Editing von Padding, Margin, Border
- Hover-Effekt über Elemente im HTML

---

## CSS-Beispieldateien für Video

### box-model-demo.html
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Box-Modell Demo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
            background-color: #f5f5f5;
        }
        
        .box {
            width: 300px;
            padding: 30px;
            border: 10px solid #333;
            margin: 40px;
            background-color: #4E9BCC;
            color: white;
            font-size: 18px;
        }
        
        .box-comparison {
            display: flex;
            gap: 40px;
        }
        
        .content-box {
            width: 300px;
            padding: 20px;
            border: 5px solid red;
            background-color: lightcoral;
        }
        
        .border-box {
            width: 300px;
            padding: 20px;
            border: 5px solid green;
            background-color: lightgreen;
            box-sizing: border-box;
        }
    </style>
</head>
<body>
    <h1>Box-Modell Demonstration</h1>
    
    <div class="box">
        Ich bin eine Box mit:
        <ul>
            <li>Width: 300px</li>
            <li>Padding: 30px</li>
            <li>Border: 10px</li>
            <li>Margin: 40px</li>
        </ul>
    </div>
    
    <h2>Box-Sizing Vergleich</h2>
    <div class="box-comparison">
        <div class="content-box">
            <strong>content-box (default)</strong><br>
            Breite: 300px + 40px Padding + 10px Border = 350px
        </div>
        
        <div class="border-box">
            <strong>border-box</strong><br>
            Breite: 300px (inklusive Padding und Border)
        </div>
    </div>
</body>
</html>
```

### display-comparison.html
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Display Eigenschaften</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
        }
        
        .block {
            display: block;
            width: 200px;
            padding: 20px;
            margin: 10px 0;
            background-color: lightblue;
        }
        
        .inline {
            display: inline;
            padding: 10px;
            background-color: lightcoral;
        }
        
        .inline-block {
            display: inline-block;
            width: 150px;
            padding: 20px;
            margin: 10px;
            background-color: lightgreen;
        }
    </style>
</head>
<body>
    <h1>Display: Block</h1>
    <div class="block">Block 1</div>
    <div class="block">Block 2</div>
    <div class="block">Block 3</div>
    
    <h1>Display: Inline</h1>
    <p>
        Text mit <span class="inline">inline Element 1</span> und 
        <span class="inline">inline Element 2</span> dazwischen.
    </p>
    
    <h1>Display: Inline-Block</h1>
    <div class="inline-block">Box 1</div>
    <div class="inline-block">Box 2</div>
    <div class="inline-block">Box 3</div>
</body>
</html>
```

### margin-collapsing.html
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Margin Collapsing</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
        }
        
        .box1 {
            padding: 20px;
            margin-bottom: 40px;
            background-color: lightblue;
        }
        
        .box2 {
            padding: 20px;
            margin-top: 30px;
            background-color: lightcoral;
        }
        
        .no-collapse {
            display: inline-block;
            width: 100%;
        }
    </style>
</head>
<body>
    <h1>Margin Collapsing Demonstration</h1>
    
    <h2>Mit Margin Collapsing (Abstand: 40px, nicht 70px)</h2>
    <div class="box1">Box 1: margin-bottom: 40px</div>
    <div class="box2">Box 2: margin-top: 30px</div>
    
    <h2>Ohne Margin Collapsing (mit inline-block)</h2>
    <div class="box1 no-collapse">Box 1: margin-bottom: 40px</div>
    <div class="box2 no-collapse">Box 2: margin-top: 30px</div>
</body>
</html>
```

---

## Lernziele (nach Video)

Nach diesem Video können Lernende:
- Die vier Bereiche des Box-Modells (Content, Padding, Border, Margin) benennen und erklären
- Padding und Margin mit Kurzschreibweisen setzen
- Den Unterschied zwischen `box-sizing: content-box` und `border-box` verstehen
- Block-, Inline- und Inline-Block-Elemente unterscheiden und anwenden
- Das Box-Modell in den Browser DevTools inspizieren
- Margin Collapsing erkennen und verstehen

---

**Gesamtdauer:** ca. 7-8 Minuten  
**Schnitt-Hinweise:** 
- DevTools-Ansicht prominent zeigen (Split-Screen mit Code)
- Box-Modell-Visualisierung farbig hervorheben
- Bei Box-Sizing-Vergleich beide Varianten direkt nebeneinander zeigen
- Für Margin Collapsing: Animation verwenden
