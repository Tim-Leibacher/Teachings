# Auftrag 2: Externe JavaScript-Datei erstellen

## Ziel

Du lagerst JavaScript in eine externe Datei aus und bindest sie professionell in dein Portfolio ein. Das macht den Code übersichtlicher und wiederverwendbar.

## Beschreibung

Inline-JavaScript (direkt im HTML) ist praktisch für kleine Tests, aber unprofessionell für echte Projekte. Professionelle Entwickler lagern JavaScript in separate `.js`-Dateien aus – genau wie CSS in `.css`-Dateien.

**Vorteile externer JavaScript-Dateien:**
- Code ist übersichtlicher und besser wartbar
- Wiederverwendbar auf mehreren HTML-Seiten
- Browser können die Datei cachen (= schnellere Ladezeiten)
- Klare Trennung: HTML = Struktur, CSS = Design, JavaScript = Logik

---

### Teil 1: JavaScript-Datei erstellen (10 Min)

Erstelle eine neue Datei **`script.js`** im gleichen Ordner wie deine `index.html`:

**Projektstruktur:**
```
mein-portfolio/
├── index.html
├── styles.css
└── script.js         ← Neue Datei!
```

**Inhalt von `script.js`:**

```javascript
// =====================================================
// PORTFOLIO JAVASCRIPT
// =====================================================
// Autor: Dein Name
// Datum: November 2025
// Beschreibung: JavaScript für meine Portfolio-Seite
// =====================================================

console.log("🚀 JavaScript erfolgreich geladen!");
console.log("Datei: script.js");

// === INFORMATIONEN ÜBER DIE SEITE ===
console.log("\n=== SEITEN-INFORMATIONEN ===");
console.log("Titel:", document.title);
console.log("URL:", window.location.href);
console.log("Sprache:", document.documentElement.lang);

// === PERSÖNLICHE BEGRÜSSUNG ===
console.log("\n=== WILLKOMMEN ===");
let vorname = "Sarah";
let nachname = "Müller";
let beruf = "Informatikerin EFZ Applikationsentwicklung";

console.log(`Hallo, ich bin ${vorname} ${nachname}`);
console.log(`Beruf: ${beruf}`);
console.log(`Lehrjahr: 1`);

// === AKTUELLES DATUM UND ZEIT ===
console.log("\n=== AKTUELLES DATUM ===");
let jetzt = new Date();
console.log("Datum:", jetzt.toLocaleDateString("de-CH"));
console.log("Uhrzeit:", jetzt.toLocaleTimeString("de-CH"));

// === BESUCHER-ZÄHLER (Simulation) ===
console.log("\n=== BESUCHER-INFO ===");
let besucherNummer = Math.floor(Math.random() * 1000) + 1;
console.log(`Du bist Besucher #${besucherNummer} heute`);

// === BROWSER-INFORMATIONEN ===
console.log("\n=== DEIN BROWSER ===");
console.log("Browser:", navigator.userAgent);
console.log("Bildschirmbreite:", window.innerWidth, "px");
console.log("Bildschirmhöhe:", window.innerHeight, "px");

// === ABSCHLUSS ===
console.log("\n" + "=".repeat(50));
console.log("Portfolio by", vorname, nachname);
console.log("Viel Erfolg beim Entdecken!");
console.log("=".repeat(50));
```

**Neue Elemente erklärt:**
- `let` erstellt Variablen – Platzhalter für Werte
- Template Strings mit Backticks: `` `Text ${variable}` ``
- `new Date()` gibt das aktuelle Datum/Uhrzeit zurück
- `Math.random()` erzeugt Zufallszahlen
- `navigator.userAgent` zeigt Browser-Informationen

---

### Teil 2: JavaScript-Datei im HTML einbinden (5 Min)

Öffne deine `index.html` und **ersetze** das bisherige `<script>`-Tag:

**Vorher (Inline-JavaScript):**
```html
<body>
    <!-- Dein HTML-Inhalt -->
    
    <script>
        console.log("JavaScript ist aktiv!");
    </script>
</body>
</html>
```

**Nachher (Externe Datei):**
```html
<body>
    <!-- Dein HTML-Inhalt -->
    
    <!-- Externe JavaScript-Datei einbinden -->
    <script src="script.js"></script>
</body>
</html>
```

**Wichtig:**
- Das `src`-Attribut zeigt auf die JavaScript-Datei
- Kein Code zwischen `<script>` und `</script>` – die Datei wird extern geladen
- Das `<script>`-Tag bleibt **vor dem schliessenden `</body>`-Tag**

---

### Teil 3: Mehrere JavaScript-Dateien einbinden (10 Min)

Für grössere Projekte lohnt es sich, JavaScript in mehrere Dateien aufzuteilen:

**Erstelle eine zweite Datei: `analytics.js`**

```javascript
// =====================================================
// ANALYTICS & TRACKING
// =====================================================
// Simuliert Analyse-Funktionen (später mit echten Tools)

console.log("\n=== ANALYTICS GELADEN ===");

// Seitenaufrufe zählen (vereinfacht)
let seitenaufrufe = localStorage.getItem("pageviews") || 0;
seitenaufrufe++;
localStorage.setItem("pageviews", seitenaufrufe);
console.log("Seitenaufrufe (gesamt):", seitenaufrufe);

// Zeit auf der Seite messen
let startzeit = new Date();
console.log("Session gestartet:", startzeit.toLocaleTimeString("de-CH"));

// Beim Verlassen der Seite (vereinfacht)
window.addEventListener("beforeunload", function() {
    let endzeit = new Date();
    let verweildauer = Math.floor((endzeit - startzeit) / 1000);
    console.log("Verweildauer:", verweildauer, "Sekunden");
});

console.log("Analytics aktiv ✓");
```

**Binde beide Dateien in `index.html` ein:**

```html
<body>
    <!-- Dein HTML-Inhalt -->
    
    <!-- JavaScript-Dateien in der richtigen Reihenfolge -->
    <script src="script.js"></script>
    <script src="analytics.js"></script>
</body>
</html>
```

**Wichtig bei mehreren Dateien:**
- Die **Reihenfolge** ist wichtig – Dateien werden von oben nach unten geladen
- Wenn `analytics.js` auf Variablen aus `script.js` zugreifen soll, muss `script.js` zuerst geladen werden

---

### Teil 4: Projekt-Informationen dynamisch anzeigen (15 Min)

Erstelle eine dritte Datei: **`projects.js`**

```javascript
// =====================================================
// PROJEKT-DATEN
// =====================================================

console.log("\n=== MEINE PROJEKTE ===");

// Projekt-Objekte (vereinfacht)
let projekt1 = {
    titel: "Portfolio-Website",
    technologien: ["HTML", "CSS", "JavaScript"],
    status: "In Arbeit",
    startdatum: "Oktober 2025"
};

let projekt2 = {
    titel: "HTML Grundlagen",
    technologien: ["HTML"],
    status: "Abgeschlossen",
    startdatum: "September 2025"
};

let projekt3 = {
    titel: "To-Do App",
    technologien: ["HTML", "CSS", "JavaScript"],
    status: "Geplant",
    startdatum: "Dezember 2025"
};

// Projekt-Ausgabe
function zeigeProjekt(projekt) {
    console.log("\n---");
    console.log("Projekt:", projekt.titel);
    console.log("Technologien:", projekt.technologien.join(", "));
    console.log("Status:", projekt.status);
    console.log("Start:", projekt.startdatum);
}

// Alle Projekte anzeigen
zeigeProjekt(projekt1);
zeigeProjekt(projekt2);
zeigeProjekt(projekt3);

console.log("\n---");
console.log("Gesamt:", 3, "Projekte");
```

**Neue Konzepte:**
- **Objekte:** Strukturierte Daten mit Eigenschaften (`titel`, `technologien`, etc.)
- **Arrays:** Listen von Werten (z.B. `["HTML", "CSS", "JavaScript"]`)
- **Funktionen:** Wiederverwendbare Code-Blöcke (`zeigeProjekt()`)
- `.join(", ")` verbindet Array-Elemente mit Kommas

**Binde die Datei ein:**

```html
<script src="script.js"></script>
<script src="analytics.js"></script>
<script src="projects.js"></script>
```

---

### Teil 5: Fehler beheben – Häufige Probleme (10 Min)

**Problem 1: Datei nicht gefunden**

Fehlermeldung in der Konsole:
```
GET http://localhost/script.js net::ERR_FILE_NOT_FOUND
```

**Lösung:**
- Prüfe den Dateinamen (Gross-/Kleinschreibung beachten!)
- Prüfe den Pfad (ist die Datei im richtigen Ordner?)
- Richtig: `<script src="script.js"></script>`
- Falsch: `<script src="scrip.js"></script>` (Tippfehler!)

---

**Problem 2: JavaScript funktioniert nicht**

**Lösung:**
- Öffne die Konsole (F12) und schaue nach Fehlermeldungen (rot)
- Häufige Fehler:
  - Vergessene Anführungszeichen: `console.log(Test)` → `console.log("Test")`
  - Vergessene Klammern: `console.log("Test"` → `console.log("Test")`
  - Tippfehler in Variablennamen: `vorNme` → `vorname`

---

**Problem 3: Falsche Reihenfolge der Dateien**

Wenn `analytics.js` auf Variablen aus `script.js` zugreift, muss `script.js` **zuerst** geladen werden:

```html
<!-- ✅ Richtig -->
<script src="script.js"></script>
<script src="analytics.js"></script>

<!-- ❌ Falsch – Fehler in der Konsole -->
<script src="analytics.js"></script>
<script src="script.js"></script>
```

---

## Erfolgskriterien

- [ ] Datei `script.js` ist erstellt und im Projektordner
- [ ] JavaScript-Datei ist korrekt in `index.html` eingebunden (`src`-Attribut)
- [ ] Browser-Konsole zeigt alle Ausgaben aus der externen Datei
- [ ] Persönliche Informationen (Vorname, Nachname, Beruf) werden ausgegeben
- [ ] Aktuelles Datum und Uhrzeit werden angezeigt
- [ ] (Optional) Mehrere JavaScript-Dateien sind eingebunden und funktionieren
- [ ] (Optional) Projekt-Informationen werden strukturiert ausgegeben
- [ ] Keine Fehlermeldungen in der Konsole (rot)

---

## Tipps

- **Dateinamen konsistent:** Immer Kleinschreibung, keine Leerzeichen, z.B. `script.js`, `analytics.js`
- **Kommentare nutzen:** Erkläre, was dein Code macht (für dich selbst in 6 Monaten!)
- **Code formatieren:** VS Code: `Shift + Alt + F` (Windows) oder `Shift + Option + F` (Mac)
- **Live Server Extension:** Nutze die VS Code Extension "Live Server" für automatisches Neuladen
- **DevTools offen lassen:** Fehler werden sofort angezeigt
- **Tipp für Profis:** Nutze `defer` im Script-Tag: `<script src="script.js" defer></script>` – lädt asynchron

---

## Reflexionsfragen

1. **Was sind die Vorteile einer externen JavaScript-Datei im Vergleich zu Inline-JavaScript?**  
   *Denk an Wartbarkeit, Wiederverwendbarkeit und Ladezeiten.*

2. **Warum ist die Reihenfolge der Script-Tags wichtig?**  
   *Experimentiere: Tausche die Reihenfolge von `script.js` und `analytics.js`. Was passiert?*

3. **Was ist der Unterschied zwischen diesen beiden Varianten?**
   ```html
   <script src="script.js"></script>
   <script src="script.js" defer></script>
   ```
   *Tipp: Recherchiere das `defer`-Attribut!*

4. **Öffne die DevTools → Network Tab. Siehst du, wie `script.js` geladen wird?**  
   *Wie gross ist die Datei? Wie lange hat das Laden gedauert?*

5. **Was passiert, wenn du in `script.js` eine Variable definierst und in `analytics.js` darauf zugreifst?**  
   *Teste es: Definiere `let testVariable = "Hallo"` in `script.js` und gebe sie in `analytics.js` aus.*

---

## Weiterführende Links

**Grundlagen:**
- [MDN: Das `<script>`-Element](https://developer.mozilla.org/de/docs/Web/HTML/Element/script)
- [MDN: JavaScript Module](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Modules)
- [W3Schools: JavaScript Where To](https://www.w3schools.com/js/js_whereto.asp)

**Best Practices:**
- [Google: Optimize JavaScript](https://web.dev/fast/#optimize-your-javascript)
- [JavaScript.info: Scripts: async, defer](https://javascript.info/script-async-defer)

**Dateien organisieren:**
- [MDN: Structuring JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions#splitting_your_code_into_functions)
- [freeCodeCamp: Organize JavaScript](https://www.freecodecamp.org/news/how-to-organize-your-javascript-code/)

**Debugging:**
- [Chrome DevTools: JavaScript Debugging](https://developer.chrome.com/docs/devtools/javascript/)
- [Firefox: JavaScript Debugger](https://firefox-source-docs.mozilla.org/devtools-user/debugger/)

---

**⏱️ Geschätzte Zeit:** 50 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 machst du deine Seite interaktiv – mit DOM-Manipulation!
