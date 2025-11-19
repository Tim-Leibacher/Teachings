# Storyboard: DOM-Manipulation

**Thema:** JavaScript DOM-Manipulation – HTML dynamisch steuern  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Gesamtdauer:** ca. 12-15 Minuten  
**Lernziele:** 
- DOM verstehen als Schnittstelle zwischen HTML und JavaScript
- Elemente mit `getElementById()` und `querySelector()` auswählen
- Inhalte mit `.textContent` und `.innerHTML` ändern
- CSS-Styles dynamisch anpassen
- Timing-Funktionen für Updates nutzen

---

## Szene 1: Intro & Motivation (30 Sek)

**Sprechertext:**
"Willkommen zurück! Heute machen wir deine Website interaktiv. Bisher war HTML statisch – der Inhalt ändert sich nie. Mit DOM-Manipulation kann JavaScript jedes Element auf deiner Seite finden und ändern, ohne die Seite neu zu laden. Das ist die Grundlage für alles: von einfachen Textänderungen bis zu komplexen Web-Apps. Lass uns direkt loslegen!"

**Bildschirm:**
- Zwei Browser-Fenster nebeneinander zeigen
- Links: Statische HTML-Seite (kein JavaScript)
- Rechts: Gleiche Seite mit dynamischen Elementen (Uhrzeit tickt, Text ändert sich)
- Cursor zeigt auf die dynamischen Elemente

**Dauer:** 30 Sekunden

---

## Szene 2: Was ist das DOM? (40 Sek)

**Sprechertext:**
"DOM steht für Document Object Model. Das ist eine Baumstruktur, die dein HTML repräsentiert. Jedes HTML-Element wird zum JavaScript-Objekt. Der Browser erstellt diese Struktur automatisch beim Laden der Seite. JavaScript kann dann über das `document`-Objekt auf diese Baumstruktur zugreifen. Schau dir an, wie aus HTML ein Baum wird."

**Bildschirm:**
- HTML-Code auf der linken Seite:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mein Portfolio</title>
  </head>
  <body>
    <h1 id="titel">Willkommen</h1>
    <p class="intro">Text hier</p>
  </body>
</html>
```
- Animation: HTML verwandelt sich in Baumstruktur
- Zeige document → html → head/body → h1/p
- Hervorheben: IDs und Klassen als Zugriffspunkte

**Dauer:** 40 Sekunden

---

## Szene 3: HTML-Struktur vorbereiten (35 Sek)

**Sprechertext:**
"Zuerst bereiten wir unser HTML vor. Ich füge eine neue Sektion mit Demo-Elementen ein. Wichtig: Jedes Element bekommt eine eindeutige ID. Über diese ID kann JavaScript später genau dieses Element finden. Die ID ist wie eine Adresse für JavaScript."

**Bildschirm:**
- VS Code zeigt `index.html`
- Live-Eingabe des Codes:
```html
<section id="interaktiv">
    <h2>Interaktive Demo</h2>
    
    <div class="demo-box">
        <h3>Dynamischer Text</h3>
        <p id="demo-text">Dieser Text wird geändert...</p>
    </div>
    
    <div class="demo-box">
        <h3>Aktuelle Uhrzeit</h3>
        <p>Es ist: <span id="aktuelle-zeit">--:--:--</span></p>
    </div>
</section>
```
- Hervorheben: `id="demo-text"` und `id="aktuelle-zeit"`

**Dauer:** 35 Sekunden

---

## Szene 4: Methode 1 – getElementById() (45 Sek)

**Sprechertext:**
"Die erste Methode: `getElementById()`. Sie findet ein Element mit einer bestimmten ID. Ich erstelle eine neue Datei `dom.js`. Mit `document.getElementById` greife ich auf das Element zu. Die Methode gibt ein JavaScript-Objekt zurück, das das HTML-Element repräsentiert. Mit `.textContent` ändere ich dann den Textinhalt. Wichtig: Nur der Text wird geändert, kein HTML."

**Bildschirm:**
- VS Code: Neue Datei `dom.js` erstellen
- Code live eintippen:
```javascript
// DOM-Element auswählen
let demoText = document.getElementById("demo-text");
console.log("Element gefunden:", demoText);

// Text ändern
demoText.textContent = "JavaScript hat diesen Text geändert!";
```
- Browser-Konsole zeigt: Element-Objekt
- Browser-Seite zeigt: Text hat sich geändert
- Cursor zeigt den geänderten Text

**Dauer:** 45 Sekunden

---

## Szene 5: Methode 2 – querySelector() (40 Sek)

**Sprechertext:**
"Die zweite Methode ist flexibler: `querySelector()`. Sie funktioniert mit CSS-Selektoren – genau wie in CSS. Für IDs nutzt du das Hashtag-Symbol. Du kannst aber auch Klassen mit Punkt oder Element-Namen verwenden. Diese Methode ist moderner und wird häufiger genutzt, weil sie vielseitiger ist."

**Bildschirm:**
- VS Code: Weiteren Code hinzufügen:
```javascript
// Mit querySelector (CSS-Syntax)
let element = document.querySelector("#demo-text");

// Funktioniert auch mit Klassen
let boxen = document.querySelectorAll(".demo-box");

// Oder mit Element-Namen
let alleAbsaetze = document.querySelectorAll("p");
```
- Vergleichstabelle einblenden:
  | Methode | Syntax | Findet |
  |---------|--------|--------|
  | getElementById() | "demo-text" | 1 Element |
  | querySelector() | "#demo-text" | 1 Element |
  | querySelectorAll() | ".demo-box" | Alle Elemente |

**Dauer:** 40 Sekunden

---

## Szene 6: textContent vs innerHTML (50 Sek)

**Sprechertext:**
"Es gibt zwei Wege, Inhalte zu ändern: `textContent` und `innerHTML`. Mit `textContent` änderst du nur den reinen Text – HTML-Tags werden nicht interpretiert. Mit `innerHTML` kannst du auch HTML-Code einfügen. Das ist mächtiger, aber gefährlich: Wenn Benutzereingaben verwendet werden, kann es zu Sicherheitslücken kommen – sogenanntes Cross-Site Scripting. Nutze `innerHTML` nur, wenn du die Quelle des Inhalts kontrollierst."

**Bildschirm:**
- VS Code: Beide Methoden zeigen:
```javascript
// NUR Text (sicher)
element.textContent = "Willkommen, <strong>Max</strong>!";
// Ergebnis: "Willkommen, <strong>Max</strong>!" (wörtlich)

// Mit HTML (mächtig, aber Risiko)
element.innerHTML = "Willkommen, <strong>Max</strong>!";
// Ergebnis: "Willkommen, Max!" (fett formatiert)
```
- Browser zeigt Unterschied nebeneinander
- Warnhinweis einblenden: "ACHTUNG: innerHTML mit Benutzereingaben = XSS-Risiko!"

**Dauer:** 50 Sekunden

---

## Szene 7: Praktisches Beispiel – Uhrzeit (1:10 Min)

**Sprechertext:**
"Jetzt ein praktisches Beispiel: Eine Live-Uhrzeit. Ich erstelle eine Funktion, die die aktuelle Zeit holt. Mit `new Date()` bekomme ich das aktuelle Datum und die Uhrzeit. Dann hole ich Stunden, Minuten und Sekunden. Wichtig: Ich füge führende Nullen hinzu, damit es immer zweistellig ist. Mit `setInterval` sage ich JavaScript: Führe diese Funktion jede Sekunde aus. So tickt unsere Uhr automatisch."

**Bildschirm:**
- VS Code: Code live schreiben:
```javascript
function zeigeUhrzeit() {
    let jetzt = new Date();
    let stunden = jetzt.getHours();
    let minuten = jetzt.getMinutes();
    let sekunden = jetzt.getSeconds();
    
    // Führende Nullen hinzufügen
    stunden = stunden < 10 ? "0" + stunden : stunden;
    minuten = minuten < 10 ? "0" + minuten : minuten;
    sekunden = sekunden < 10 ? "0" + sekunden : sekunden;
    
    let zeitString = `${stunden}:${minuten}:${sekunden}`;
    
    let zeitElement = document.getElementById("aktuelle-zeit");
    zeitElement.textContent = zeitString;
}

// Sofort ausführen
zeigeUhrzeit();

// Jede Sekunde wiederholen
setInterval(zeigeUhrzeit, 1000);
```
- Browser zeigt: Uhrzeit tickt jede Sekunde
- Hervorheben: `setInterval(funktion, millisekunden)`

**Dauer:** 1:10 Minuten

---

## Szene 8: Styles dynamisch ändern (1:00 Min)

**Sprechertext:**
"JavaScript kann auch CSS-Styles direkt ändern. Mit `.style.eigenschaft` greifst du auf CSS-Eigenschaften zu. Ich zeige dir ein Beispiel: Je nach Tageszeit ändert sich der Hintergrund. Tagsüber hell, nachts dunkel – ein automatischer Dark Mode. Dafür hole ich die aktuelle Stunde. Wenn es zwischen 6 und 18 Uhr ist, setze ich helle Farben, sonst dunkle. Beachte: CSS-Eigenschaften mit Minus werden zu camelCase – `background-color` wird zu `backgroundColor`."

**Bildschirm:**
- VS Code: Code eintippen:
```javascript
function anpasseFarben() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    
    let body = document.body;
    
    if (stunde >= 6 && stunde < 18) {
        // Tagsüber: hell
        body.style.backgroundColor = "#f5f5f5";
        body.style.color = "#1a1a1a";
    } else {
        // Nachts: dunkel
        body.style.backgroundColor = "#1a1a1a";
        body.style.color = "#f5f5f5";
    }
}

anpasseFarben();
```
- Browser zeigt: Seite wechselt zwischen hell und dunkel
- DevTools: Elements-Tab zeigt `style="..."`-Attribut
- Tabelle einblenden: CSS-Name → JavaScript-Name

**Dauer:** 1:00 Minute

---

## Szene 9: Mehrere Elemente mit querySelectorAll() (45 Sek)

**Sprechertext:**
"Was, wenn du mehrere Elemente gleichzeitig ändern willst? Dafür gibt es `querySelectorAll()`. Diese Methode gibt eine Liste von Elementen zurück – wie ein Array. Mit `.forEach()` gehst du durch alle Elemente und führst eine Funktion aus. Ich zeige dir ein Beispiel: Alle Demo-Boxen bekommen einen Fade-In-Effekt mit zeitlicher Verzögerung."

**Bildschirm:**
- VS Code: Code zeigen:
```javascript
let demoBoxen = document.querySelectorAll(".demo-box");

demoBoxen.forEach(function(box, index) {
    setTimeout(function() {
        box.style.opacity = "0";
        box.style.transition = "opacity 0.5s";
        box.style.opacity = "1";
    }, index * 200);  // 200ms pro Box verzögert
});
```
- Browser zeigt: Boxen faden nacheinander ein
- Hervorheben: `.forEach()` Schleife und `setTimeout()`

**Dauer:** 45 Sekunden

---

## Szene 10: JavaScript einbinden & testen (40 Sek)

**Sprechertext:**
"Jetzt müssen wir die JavaScript-Datei noch einbinden. Im HTML füge ich ein `<script>`-Tag vor dem schließenden `</body>`-Tag ein. Wichtig: Das Script-Tag muss am Ende stehen, damit das HTML bereits geladen ist. Sonst findet JavaScript die Elemente nicht. Ich lade die Seite neu und öffne die Konsole. Keine Fehler – perfekt! Die Uhrzeit tickt, der Text ist geändert, alles funktioniert."

**Bildschirm:**
- VS Code: HTML zeigen:
```html
    <!-- Vor </body> einfügen -->
    <script src="dom.js"></script>
</body>
</html>
```
- Browser: Seite neu laden (F5)
- DevTools: Konsole öffnen (F12)
- Zeigen: Keine Fehler, grüne Haken
- Seite zeigt: Uhrzeit tickt, Text geändert, Farben angepasst

**Dauer:** 40 Sekunden

---

## Szene 11: DevTools – DOM inspizieren (50 Sek)

**Sprechertext:**
"Die Browser-DevTools sind dein bester Freund. Im Elements-Tab siehst du die Live-DOM-Struktur. Wenn JavaScript Elemente ändert, siehst du das hier sofort. Rechts im Styles-Panel siehst du CSS-Eigenschaften – auch die, die JavaScript gesetzt hat. Du kannst hier sogar live experimentieren: Ändere Werte direkt in den DevTools und sieh die Auswirkungen sofort. Super praktisch zum Testen!"

**Bildschirm:**
- DevTools: Elements-Tab geöffnet
- DOM-Baum zeigen
- Element `<p id="demo-text">` anklicken
- Rechts: Styles-Panel zeigt CSS
- Live ändern: `.style.color = "red"` in Konsole eingeben
- Element wird rot
- Cursor zeigt auf geänderte Properties

**Dauer:** 50 Sekunden

---

## Szene 12: Häufige Fehler vermeiden (55 Sek)

**Sprechertext:**
"Drei häufige Fehler und wie du sie vermeidest. Erstens: Script-Tag im `<head>` statt vor `</body>`. Das führt zu 'Element nicht gefunden'-Fehlern, weil das HTML noch nicht geladen ist. Zweitens: Tippfehler bei IDs. JavaScript findet das Element nicht und gibt `null` zurück – dann gibt es einen Fehler. Prüfe IDs in HTML und JavaScript genau. Drittens: Vergessen, die JS-Datei einzubinden. Kein JavaScript läuft, keine Fehlermeldung – die Seite bleibt einfach statisch. Prüfe immer die Konsole auf Fehler!"

**Bildschirm:**
- Fehler 1 zeigen:
```html
<!-- FALSCH -->
<head>
    <script src="dom.js"></script>  ❌
</head>
```
- Konsole: "Cannot read property 'textContent' of null"

- Fehler 2 zeigen:
```javascript
// HTML: id="demo-text"
let element = document.getElementById("demo-txt");  // ❌ Tippfehler!
console.log(element);  // null
```

- Fehler 3 zeigen:
```html
<!-- Script-Tag vergessen -->
<body>
    <!-- ... -->
    <!-- Kein <script src="dom.js"></script> -->
</body>
```
- Konsole: Leer, kein Output

**Dauer:** 55 Sekunden

---

## Szene 13: Zusammenfassung & Ausblick (40 Sek)

**Sprechertext:**
"Fassen wir zusammen: Das DOM ist die Brücke zwischen HTML und JavaScript. Mit `getElementById()` und `querySelector()` greifst du auf Elemente zu. Mit `.textContent` und `.innerHTML` änderst du Inhalte. Mit `.style` änderst du Styles. Und mit `setInterval()` machst du Updates automatisch. Das sind die Grundlagen! Im nächsten Video schauen wir uns Event Handling an – wie Klicks, Tastatureingaben und andere Benutzeraktionen. Dann wird's richtig interaktiv! Viel Erfolg bei den Aufträgen!"

**Bildschirm:**
- Mind-Map einblenden mit Hauptkonzepten:
  - DOM = Document Object Model
  - Zugriff: getElementById(), querySelector()
  - Ändern: textContent, innerHTML, style
  - Timing: setInterval(), setTimeout()
- Vorschau nächstes Video: "Event Handling – Klicks & Interaktion"
- Outro-Animation mit Logo

**Dauer:** 40 Sekunden

---

## Gesamtdauer

Ca. 12-15 Minuten (je nach Tempo)

---

## Benötigte Materialien für Video

### 1. Demo-HTML-Datei
**Datei:** `demo.html` (vollständiges Beispiel für Video)

### 2. Demo-JavaScript-Datei
**Datei:** `dom.js` (vollständiges Beispiel)

### 3. CSS für Demo-Boxen
**Datei:** `demo-styles.css`

### 4. Animationen & Grafiken
- DOM-Baum-Animation (HTML → Baumstruktur)
- Vergleichstabelle getElementById vs querySelector
- Mind-Map für Zusammenfassung
- Warnhinweis-Grafik für innerHTML-Sicherheit

### 5. Screenshots
- Browser mit tickender Uhrzeit
- DevTools Elements-Tab
- Konsole mit Fehlermeldungen
- Vorher/Nachher bei Textänderung

---

## Technische Hinweise

**Software:**
- VS Code als Editor
- Google Chrome für DevTools
- Screen Recording mit 1920x1080
- Code-Syntax-Highlighting aktiviert

**BAND Design System:**
- Hintergrund: Gradient (blau → türkis → orange)
- Schriftart: Aptos
- Farben:
  - Primär: #0066cc (blau)
  - Sekundär: #00b8d4 (türkis)
  - Akzent: #ff6b35 (orange)

**Tipps für Recording:**
- Code langsam eintippen (nicht copy-paste)
- Cursor-Bewegungen bewusst einsetzen
- Pausen nach jedem Konzept für Verarbeitung
- Browser und Editor nebeneinander bei Vergleichen
- Konsole immer geöffnet halten
