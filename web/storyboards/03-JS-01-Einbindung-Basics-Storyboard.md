# Storyboard: JavaScript – Einbindung & Basics

**Modul:** JavaScript  
**Thema:** Einbindung & Basics  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Geschätzte Videolänge:** 8-10 Minuten  
**Autor:** Tim Leibacher

---

## Video-Übersicht

**Lernziele:**
- Unterschied zwischen HTML, CSS und JavaScript verstehen
- `<script>`-Tag im `<head>` und vor `</body>` einbinden können
- Browser-Konsole öffnen und nutzen
- Erste Ausgaben mit `console.log()` erstellen
- Externe JavaScript-Dateien einbinden

**Benötigte Ressourcen:**
- VS Code mit index.html geöffnet
- Browser (Chrome oder Firefox) mit DevTools
- Beispiel-HTML-Datei (siehe unten)
- Beispiel externe JS-Datei

---

## Szene 1: Intro & Kontext (40 Sek.)

### Sprechertext
"Willkommen zum JavaScript-Modul! Bisher haben wir HTML für die Struktur und CSS für das Design verwendet. Jetzt kommt JavaScript ins Spiel – die Programmiersprache, die deine Website lebendig macht. Stell dir vor: HTML ist das Skelett eines Hauses, CSS die Farbe und Dekoration, und JavaScript ist die Elektrik, die Licht, Heizung und alle interaktiven Elemente steuert. In diesem Video lernst du, wie du JavaScript in deine Website einbindest und erste Schritte mit der Browser-Konsole machst."

### Bildschirmdarstellung
- Zeige drei Browser-Tabs nebeneinander:
  1. Tab mit reinem HTML (Portfolio ohne Styles)
  2. Tab mit HTML + CSS (gestyltes Portfolio)
  3. Tab mit HTML + CSS + JS (Portfolio mit interaktivem Element, z.B. Button der bei Klick Text ändert)
- Text-Overlay: **"HTML = Struktur | CSS = Design | JavaScript = Interaktivität"**

### Hinweise zur Animation
- Fade-In für jeden Tab nacheinander (1 Sek. Abstand)
- Highlight-Effekt auf dem interaktiven Element im 3. Tab

---

## Szene 2: Das `<script>`-Tag – Basics (1 Min.)

### Sprechertext
"JavaScript bindest du mit dem `<script>`-Tag ein. Es gibt zwei Hauptorte: Im `<head>` oder vor dem schliessenden `</body>`-Tag. Schauen wir uns beide Varianten an. Zuerst schreiben wir JavaScript direkt im `<script>`-Tag – das nennt man 'Inline JavaScript'. Später lagern wir es in eine externe Datei aus, was professioneller ist."

### Bildschirmdarstellung
VS Code mit folgender HTML-Datei:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Einbindung</title>
    
    <!-- JavaScript im HEAD -->
    <script>
        console.log("JavaScript im HEAD geladen!");
    </script>
</head>
<body>
    <h1>Mein erstes JavaScript</h1>
    <p>Öffne die Konsole (F12), um die Ausgaben zu sehen.</p>
    
    <!-- JavaScript vor </body> -->
    <script>
        console.log("JavaScript vor </body> geladen!");
    </script>
</body>
</html>
```

### Hinweise
- Zeige Code in VS Code mit Syntax-Highlighting
- Markiere `<script>`-Tags farbig (z.B. gelber Rahmen)
- Text-Overlay: **"Inline JavaScript = Code direkt im HTML"**

---

## Szene 3: Browser-Konsole öffnen (30 Sek.)

### Sprechertext
"Die Browser-Konsole ist dein wichtigstes Werkzeug beim JavaScript-Entwickeln. Öffne sie mit F12 oder Rechtsklick > 'Untersuchen'. Hier siehst du alle JavaScript-Ausgaben, Fehler und Warnungen. Die Konsole ist wie ein Logbuch deiner Website."

### Bildschirmdarstellung
- Öffne im Browser (Chrome) die DevTools mit F12
- Navigiere zum Tab "Console"
- Zeige die beiden Ausgaben:
  ```
  JavaScript im HEAD geladen!
  JavaScript vor </body> geladen!
  ```

### Hinweise
- Screen Recording: Zeige den Tastendruck F12 als Overlay
- Cursor-Highlight beim Klicken auf "Console"-Tab
- Zoom auf die Konsolen-Ausgaben

---

## Szene 4: `console.log()` – Dein Debug-Werkzeug (1 Min.)

### Sprechertext
"`console.log()` ist deine wichtigste Funktion beim Programmieren. Du kannst damit Texte, Zahlen oder Variablen ausgeben, um zu prüfen, ob dein Code funktioniert. Das ist wie ein 'Echo' – du schickst etwas an die Konsole und siehst sofort das Ergebnis. Schauen wir uns verschiedene Ausgaben an."

### Bildschirmdarstellung
VS Code – füge mehr `console.log()`-Beispiele hinzu:

```html
<script>
    // Einfacher Text
    console.log("Hallo JavaScript!");
    
    // Zahlen
    console.log(42);
    console.log(2024);
    
    // Berechnungen
    console.log(10 + 5);
    console.log(20 * 3);
    
    // Mehrere Werte
    console.log("Mein Name:", "Sarah Müller");
    console.log("Alter:", 18, "Jahre");
</script>
```

Zeige dann im Browser die Konsole mit allen Ausgaben.

### Hinweise
- Split-Screen: VS Code links, Browser-Konsole rechts
- Highlight jede `console.log()`-Zeile und zeige parallel die Ausgabe

---

## Szene 5: Unterschied `<head>` vs. vor `</body>` (1 Min. 20 Sek.)

### Sprechertext
"Jetzt zur wichtigen Frage: Wo soll das `<script>`-Tag hin? Im `<head>` wird JavaScript geladen, BEVOR die Seite sichtbar ist. Das kann zu Problemen führen, wenn dein Code auf HTML-Elemente zugreifen will, die noch nicht existieren. Vor dem schliessenden `</body>`-Tag wird JavaScript geladen, NACHDEM die ganze Seite geladen ist – das ist meistens die bessere Wahl."

### Bildschirmdarstellung

**Beispiel 1: JavaScript im `<head>` – Problem**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Problem: Script im HEAD</title>
    
    <script>
        // Versuch, auf h1 zuzugreifen
        let titel = document.querySelector("h1");
        console.log(titel); // null – Element existiert noch nicht!
    </script>
</head>
<body>
    <h1>Dieser Titel existiert erst nach dem HEAD</h1>
</body>
</html>
```

Zeige in der Konsole: `null` (weil `<h1>` noch nicht existiert).

**Beispiel 2: JavaScript vor `</body>` – Lösung**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Lösung: Script vor </body></title>
</head>
<body>
    <h1>Dieser Titel existiert jetzt</h1>
    
    <script>
        // Jetzt funktioniert es!
        let titel = document.querySelector("h1");
        console.log(titel); // <h1>Dieser Titel existiert jetzt</h1>
    </script>
</body>
</html>
```

Zeige in der Konsole: Das gesamte `<h1>`-Element wird ausgegeben.

### Hinweise
- Split-Screen: Code links, Konsole rechts
- Markiere die Position der `<script>`-Tags mit Pfeilen
- Text-Overlay beim ersten Beispiel: **"⚠️ Problem: Element existiert noch nicht"**
- Text-Overlay beim zweiten Beispiel: **"✅ Lösung: Seite ist geladen"**

---

## Szene 6: Externe JavaScript-Datei einbinden (1 Min. 30 Sek.)

### Sprechertext
"Professionelle Websites lagern JavaScript in externe Dateien aus – genau wie bei CSS. Das macht den Code übersichtlicher und wiederverwendbar. Erstellen wir eine externe JavaScript-Datei und binden sie ein."

### Bildschirmdarstellung

**Schritt 1: JavaScript-Datei erstellen**

VS Code – Erstelle neue Datei: `script.js`

```javascript
// script.js

console.log("Externe JavaScript-Datei geladen!");

// Informationen über die Seite
console.log("Titel der Seite:", document.title);
console.log("URL der Seite:", window.location.href);

// Einfache Begrüssung
let begruessung = "Willkommen auf meiner Portfolio-Seite!";
console.log(begruessung);
```

**Schritt 2: Datei im HTML einbinden**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Externe JavaScript-Datei</title>
</head>
<body>
    <h1>Portfolio mit externem JavaScript</h1>
    
    <!-- Externe JavaScript-Datei einbinden -->
    <script src="script.js"></script>
</body>
</html>
```

**Schritt 3: Im Browser testen**

Zeige im Browser die Konsole mit allen Ausgaben aus `script.js`.

### Hinweise
- Split-Screen: VS Code (2 Dateien) links, Browser rechts
- Zeige Dateistruktur im VS Code Explorer:
  ```
  projekt/
  ├── index.html
  └── script.js
  ```
- Text-Overlay: **"Externe Datei = Sauberer Code + Wiederverwendbar"**

---

## Szene 7: Häufige Fehler und Debugging (1 Min.)

### Sprechertext
"Schauen wir uns häufige Fehler an und wie du sie in der Konsole erkennst. Fehler in JavaScript stoppen oft den gesamten Code – deshalb ist die Konsole so wichtig. Ein roter Text bedeutet: Hier ist etwas schiefgelaufen."

### Bildschirmdarstellung

**Fehler 1: Vergessene Anführungszeichen**

```javascript
console.log(Hallo JavaScript);  // ❌ Fehler!
```

Zeige in der Konsole:
```
Uncaught ReferenceError: Hallo is not defined
```

**Fehler 2: Falsche Dateinamen**

```html
<script src="scrip.js"></script>  <!-- ❌ Tippfehler! -->
```

Zeige in der Konsole:
```
GET http://localhost/scrip.js net::ERR_FILE_NOT_FOUND
```

**Fehler 3: Vergessene schliessende Klammer**

```javascript
console.log("Test"  // ❌ Klammer fehlt
```

Zeige in der Konsole:
```
Uncaught SyntaxError: missing ) after argument list
```

### Hinweise
- Zeige jeden Fehler mit Code + Konsolen-Ausgabe
- Markiere das Problem im Code mit rotem Pfeil
- Text-Overlay: **"Rote Meldung = Fehler gefunden!"**

---

## Szene 8: Zusammenfassung & Praxis-Tipps (1 Min.)

### Sprechertext
"Fassen wir zusammen: Du hast gelernt, JavaScript mit dem `<script>`-Tag einzubinden – entweder inline im HTML oder als externe Datei. Du weisst jetzt, dass JavaScript vor dem schliessenden `</body>`-Tag die beste Position ist, und du kannst mit `console.log()` Ausgaben erstellen. Die Browser-Konsole ist dein wichtigstes Werkzeug – nutze sie immer, wenn etwas nicht funktioniert. Im nächsten Video schauen wir uns Variablen und Datentypen an. Viel Erfolg bei den Aufträgen!"

### Bildschirmdarstellung
Checkliste mit Animationen (erscheint Punkt für Punkt):

```
✅ <script>-Tag nutzen
✅ Browser-Konsole öffnen (F12)
✅ console.log() für Ausgaben
✅ Externe .js-Datei einbinden
✅ Script vor </body> platzieren
✅ Fehler in der Konsole lesen
```

### Hinweise
- Zeige finale Projekt-Struktur:
  ```
  mein-portfolio/
  ├── index.html
  ├── styles.css
  └── script.js
  ```
- Fade-Out mit BAND Design (Gradient-Hintergrund)

---

## Zusatzmaterialien für Video-Produktion

### Beispiel-Dateien zum Mitschneiden

**index.html (Vollständiges Beispiel)**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Einbindung Demo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Mein Portfolio</h1>
        <p>Lerne JavaScript Schritt für Schritt</p>
    </header>
    
    <main>
        <section id="demo">
            <h2>JavaScript ist aktiv!</h2>
            <p>Öffne die Konsole (F12), um die Ausgaben zu sehen.</p>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2025 Dein Name</p>
    </footer>
    
    <!-- Externes JavaScript -->
    <script src="script.js"></script>
</body>
</html>
```

**script.js (Vollständiges Beispiel)**
```javascript
// ==================
// JavaScript Demo für Video
// ==================

console.log("🚀 JavaScript erfolgreich geladen!");

// Informationen über die Seite
console.log("Titel:", document.title);
console.log("URL:", window.location.href);

// Einfache Berechnungen
console.log("10 + 5 =", 10 + 5);
console.log("20 * 3 =", 20 * 3);

// Persönliche Begrüssung
let vorname = "Sarah";
let nachname = "Müller";
console.log("Willkommen,", vorname, nachname);

// Prüfe, ob bestimmte Elemente existieren
let ueberschrift = document.querySelector("h1");
console.log("Haupt-Überschrift gefunden:", ueberschrift);
```

**styles.css (Basis-Styling für Video)**
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Aptos', 'Segoe UI', sans-serif;
    line-height: 1.6;
    color: #1a1a1a;
    background: linear-gradient(135deg, #376B8C 0%, #29786A 100%);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

header {
    background: rgba(255, 255, 255, 0.95);
    padding: 2rem;
    text-align: center;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

header h1 {
    color: #376B8C;
    font-size: 2.5rem;
}

main {
    flex: 1;
    max-width: 800px;
    margin: 3rem auto;
    padding: 2rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
}

section {
    margin-bottom: 2rem;
}

h2 {
    color: #376B8C;
    margin-bottom: 1rem;
}

footer {
    background: rgba(26, 26, 26, 0.9);
    color: white;
    text-align: center;
    padding: 1rem;
}
```

---

## Technische Hinweise für Videoaufnahme

### Software & Settings
- **Screen Recording:** OBS Studio oder Camtasia
- **Auflösung:** 1920x1080 (Full HD)
- **Framerate:** 30fps
- **Audio:** Klares Mikrofon, Rauschunterdrückung aktiv
- **Cursor:** Highlight-Effekt aktivieren

### VS Code Settings für Video
- **Theme:** Dark+ (default dark) oder Light+ (default light)
- **Font Size:** 16-18px (gut lesbar im Video)
- **Minimap:** Deaktivieren für mehr Platz
- **Zoom:** 120-130% für Lesbarkeit

### Browser DevTools Settings
- **Zoom:** Console auf 110% für Lesbarkeit
- **Theme:** Wie VS Code (einheitliches Bild)
- **Preserve Log:** Aktiviert, damit Ausgaben nicht verschwinden

### Farbschema (BAND Design)
- **Primärfarbe (Blau):** #376B8C
- **Sekundärfarbe (Türkis):** #29786A
- **Akzentfarbe (Orange):** #E07A42
- **Textfarbe:** #1a1a1a
- **Hintergrund:** Weiss #FFFFFF

---

## Timing-Übersicht (Total: ca. 9 Min.)

| Szene | Inhalt | Dauer |
|-------|--------|-------|
| 1 | Intro & Kontext | 40 Sek. |
| 2 | `<script>`-Tag Basics | 1 Min. |
| 3 | Browser-Konsole | 30 Sek. |
| 4 | `console.log()` | 1 Min. |
| 5 | `<head>` vs. vor `</body>` | 1 Min. 20 Sek. |
| 6 | Externe JS-Datei | 1 Min. 30 Sek. |
| 7 | Häufige Fehler | 1 Min. |
| 8 | Zusammenfassung | 1 Min. |
| **Total** | | **~8-9 Min.** |

---

## Checkliste für Video-Produktion

**Vor der Aufnahme:**
- [ ] Alle Beispiel-Dateien erstellt und getestet
- [ ] VS Code Font Size auf 16-18px erhöht
- [ ] Browser DevTools Theme angepasst
- [ ] Desktop aufgeräumt (keine privaten Tabs/Dateien sichtbar)
- [ ] Mikrofon-Test durchgeführt
- [ ] OBS/Camtasia Einstellungen geprüft

**Während der Aufnahme:**
- [ ] Langsam und deutlich sprechen
- [ ] Pausen zwischen Szenen einhalten
- [ ] Cursor-Bewegungen bewusst und langsam
- [ ] Nach jedem Code-Beispiel kurz warten (5 Sek.)
- [ ] Bei Fehlern: Stopp, Korrektur, Neustart der Szene

**Nach der Aufnahme:**
- [ ] Video auf Tippfehler im Code prüfen
- [ ] Audio-Pegel normalisieren
- [ ] Text-Overlays hinzufügen (siehe Hinweise)
- [ ] Übergänge zwischen Szenen (Fade, 0.5 Sek.)
- [ ] Intro & Outro mit BAND Design
- [ ] Export in 1080p
- [ ] Upload auf YouTube mit Kapitelmarken (Timestamps)

---

**Viel Erfolg bei der Video-Produktion!**
