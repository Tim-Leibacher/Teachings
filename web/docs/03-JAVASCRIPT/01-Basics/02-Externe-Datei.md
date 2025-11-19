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

### Teil 1: JavaScript-Datei erstellen (15 Min)

**Aufgabe:**
Erstelle eine neue Datei **`script.js`** im gleichen Ordner wie deine `index.html`.

**Projektstruktur (Ziel):**
```
mein-portfolio/
├── index.html
├── styles.css
└── script.js         ← Neue Datei!
```

**Deine Aufgaben:**

**1.1 Grundstruktur**
- Erstelle einen Datei-Header mit Kommentaren:
    - Titel: "PORTFOLIO JAVASCRIPT"
    - Dein Name als Autor
    - Aktuelles Datum
    - Kurze Beschreibung

**1.2 Erste Ausgaben**
- Gib "JavaScript erfolgreich geladen!" aus
- Gib "Datei: script.js" aus

**1.3 Seiten-Informationen**
Recherchiere und gib aus:
- Den Titel der Seite (Hinweis: `document.title`)
- Die URL der Seite (Hinweis: `window.location.href`)
- Die Sprache der Seite (Hinweis: `document.documentElement.lang`)

**1.4 Variablen nutzen**
Erstelle Variablen für:
- Deinen Vornamen (mit `let vorname = "..."`)
- Deinen Nachnamen (mit `let nachname = "..."`)
- Deinen Beruf
- Dein Lehrjahr

Gib diese Informationen formatiert aus.

**Tipp:** Nutze Template Strings für schönere Ausgaben:
```javascript
let name = "Max";
console.log(`Hallo, ich bin ${name}`);
```

**1.5 Aktuelles Datum**
Recherchiere `Date`-Objekt und gib aus:
- Das aktuelle Datum (formatiert für die Schweiz: "de-CH")
- Die aktuelle Uhrzeit (formatiert für die Schweiz: "de-CH")

**Nachschlagen:**
- [MDN: let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) - Variablen deklarieren
- [MDN: Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) - String-Formatierung
- [MDN: Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) - Datum und Uhrzeit
- [MDN: toLocaleDateString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString) - Datum formatieren

---

### Teil 2: JavaScript-Datei im HTML einbinden (10 Min)

**Aufgabe:**
Öffne deine `index.html` und binde die externe JavaScript-Datei ein.

**Vorgehen:**
1. Entferne das bisherige `<script>`-Tag mit Inline-Code (falls vorhanden)
2. Füge ein neues `<script>`-Tag **vor dem schliessenden `</body>`-Tag** ein
3. Nutze das `src`-Attribut, um auf `script.js` zu verweisen

**Struktur (als Hilfe):**
```html
<body>
    <!-- Dein HTML-Inhalt -->
    
    <!-- Hier externe JavaScript-Datei einbinden -->
    
</body>
</html>
```

**Wichtig:**
- Das `src`-Attribut zeigt auf die JavaScript-Datei
- Zwischen `<script>` und `</script>` steht **kein Code** mehr
- Das Tag bleibt vor dem schliessenden `</body>`-Tag

**Test:**
- Speichere beide Dateien
- Öffne `index.html` im Browser
- Öffne die Konsole (F12)
- Siehst du alle Ausgaben aus `script.js`?

**Nachschlagen:**
- [MDN: Das `<script>`-Element](https://developer.mozilla.org/de/docs/Web/HTML/Element/script) - src-Attribut
- [W3Schools: JavaScript Where To](https://www.w3schools.com/js/js_whereto.asp) - Externe Dateien

---

### Teil 3: Zusätzliche Funktionen implementieren (20 Min)

**Aufgabe:**
Erweitere deine `script.js` mit folgenden Funktionen:

**3.1 Zufalls-Besucher-Nummer**
- Erstelle eine Variable `besucherNummer`
- Generiere eine Zufallszahl zwischen 1 und 1000
- Gib aus: "Du bist Besucher #[Zahl] heute"

**Hinweis:** Recherchiere `Math.random()` und `Math.floor()`

**3.2 Browser-Informationen**
Recherchiere und gib aus:
- Den Browser (Hinweis: `navigator.userAgent` - nur die Ausgabe, nicht interpretieren)
- Die Bildschirmbreite in Pixeln
- Die Bildschirmhöhe in Pixeln

**3.3 Formatierte Abschluss-Nachricht**
Erstelle eine Abschluss-Box:
- Trennlinie aus 50 Gleichheitszeichen
- Text: "Portfolio by [Dein Name]"
- Text: "Viel Erfolg beim Entdecken!"
- Trennlinie aus 50 Gleichheitszeichen

**Nachschlagen:**
- [MDN: Math.random()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random) - Zufallszahlen
- [MDN: Math.floor()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) - Abrunden
- [MDN: Window](https://developer.mozilla.org/en-US/docs/Web/API/Window) - Fenster-Eigenschaften
- [MDN: Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) - Browser-Info

---

### Teil 4: Zweite JavaScript-Datei erstellen (15 Min)

**Aufgabe:**
Für grössere Projekte ist es sinnvoll, JavaScript in mehrere Dateien aufzuteilen.

**4.1 Neue Datei erstellen**
Erstelle eine Datei **`projects.js`** im gleichen Ordner.

**4.2 Projekt-Daten strukturieren**

Deine Aufgabe ist es, drei Projekte mit folgender Struktur anzulegen:

**Projekt-Eigenschaften:**
- `titel`: Name des Projekts
- `technologien`: Array mit verwendeten Technologien
- `status`: "In Arbeit", "Abgeschlossen" oder "Geplant"
- `startdatum`: Monat und Jahr

**Beispiel-Struktur (nicht kopieren - selbst umsetzen):**
```javascript
let projektX = {
    titel: "...",
    technologien: ["...", "..."],
    status: "...",
    startdatum: "..."
};
```

**4.3 Projekte ausgeben**
Erstelle eine Funktion `zeigeProjekt(projekt)`, die:
- Den Titel ausgibt
- Die Technologien ausgibt (als kommagetrennten Text)
- Den Status ausgibt
- Das Startdatum ausgibt
- Zwischen Projekten eine Trennlinie einfügt

**Tipp:** Arrays in Text umwandeln mit `.join(", ")`

**4.4 Alle Projekte anzeigen**
- Rufe die Funktion für alle drei Projekte auf
- Gib am Ende die Gesamtzahl der Projekte aus

**Nachschlagen:**
- [MDN: Objekte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects) - Daten strukturieren
- [MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) - Listen
- [MDN: Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions) - Funktionen erstellen
- [MDN: Array.prototype.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) - Arrays verbinden

**4.5 Datei einbinden**
Binde `projects.js` in deiner `index.html` ein (nach `script.js`).

---

### Teil 5: Fehler beheben – Häufige Probleme (10 Min)

**Aufgabe:**
Teste folgende Fehlerszenarien und behebe sie:

**Fehler 1: Falsche Datei-Referenz**
- Ändere absichtlich den Dateinamen im `src`-Attribut (z.B. `scrip.js` statt `script.js`)
- Was zeigt die Konsole?
- Korrigiere den Fehler

**Fehler 2: Falsche Reihenfolge**
- Verschiebe das `<script>`-Tag für `projects.js` **vor** `script.js`
- Versuche in `projects.js` auf eine Variable aus `script.js` zuzugreifen
- Was passiert?
- Erkläre, warum die Reihenfolge wichtig ist
- Korrigiere die Reihenfolge

**Fehler 3: Syntax-Fehler**
Erstelle absichtlich einen Fehler in `script.js`:
- Vergiss ein Semikolon
- Vergiss eine schliessende Klammer
- Schreibe einen falschen Variablennamen

Beobachte die Fehlermeldungen und korrigiere sie.

**Nachschlagen:**
- [Chrome DevTools: JavaScript Debugging](https://developer.chrome.com/docs/devtools/javascript/) - Fehler finden
- [MDN: JavaScript Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors) - Fehlertypen

---

## Erfolgskriterien

- [ ] Datei `script.js` ist erstellt und im Projektordner
- [ ] JavaScript-Datei ist korrekt in `index.html` eingebunden (`src`-Attribut)
- [ ] Browser-Konsole zeigt alle Ausgaben aus der externen Datei
- [ ] Persönliche Informationen (Vorname, Nachname, Beruf) werden mit Variablen ausgegeben
- [ ] Aktuelles Datum und Uhrzeit werden formatiert angezeigt
- [ ] Zufalls-Besucher-Nummer wird generiert
- [ ] Datei `projects.js` ist erstellt und eingebunden
- [ ] Mindestens drei Projekte sind als Objekte strukturiert
- [ ] Funktion zur Projekt-Anzeige funktioniert
- [ ] Keine Fehlermeldungen in der Konsole (rot)

---

## Zusatzaufgaben (Optional)

**Für Schnelle:**

**A) Analytics simulieren**
Erstelle eine Datei `analytics.js`, die:
- Die Anzahl der Seitenaufrufe zählt (mit `localStorage`)
- Die Session-Startzeit speichert
- Beim Verlassen der Seite die Verweildauer berechnet

**Hinweise:**
- `localStorage.getItem("key")` - Daten holen
- `localStorage.setItem("key", wert)` - Daten speichern
- Event: `window.addEventListener("beforeunload", function)`

**B) Erweiterte Projekt-Funktionen**
- Funktion `zaehleAbgeschlossene()` - zählt abgeschlossene Projekte
- Funktion `zaehleTechnologien()` - listet alle verwendeten Technologien auf (ohne Duplikate)
- Funktion `filtereNachStatus(status)` - zeigt nur Projekte mit bestimmtem Status

**Nachschlagen:**
- [MDN: Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) - localStorage
- [MDN: Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) - Duplikate entfernen

---

## Tipps

- **Dateinamen konsistent:** Immer Kleinschreibung, keine Leerzeichen
- **Kommentare nutzen:** Erkläre, was dein Code macht
- **Code formatieren:** VS Code: `Shift + Alt + F` (Windows) oder `Shift + Option + F` (Mac)
- **Live Server:** Nutze die VS Code Extension für automatisches Neuladen
- **DevTools Network Tab:** Sieh, wie Dateien geladen werden
- **Inkrementell testen:** Nach jeder kleinen Änderung speichern und testen

---

## Reflexionsfragen

1. **Was sind die Vorteile einer externen JavaScript-Datei im Vergleich zu Inline-JavaScript?**  
   *Denk an Wartbarkeit, Wiederverwendbarkeit und Ladezeiten.*

2. **Warum ist die Reihenfolge der Script-Tags wichtig?**  
   *Was passiert, wenn Datei B auf Code aus Datei A zugreift, aber A noch nicht geladen ist?*

3. **Was passiert, wenn du eine Variable in `script.js` mit `let` definierst und in `projects.js` darauf zugreifen willst?**  
   *Teste es und erkläre das Ergebnis.*

4. **Öffne die DevTools → Network Tab. Wie gross sind deine JavaScript-Dateien? Wie lange dauert das Laden?**  
   *Ab welcher Grösse wird das Laden spürbar langsamer?*

5. **Recherchiere: Was macht das `defer`-Attribut im Script-Tag?**  
   *Wann würdest du es einsetzen? Was ist der Unterschied zu `async`?*

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
- [freeCodeCamp: Organize JavaScript](https://www.freecodecamp.org/news/how-to-organize-your-javascript-code/)

**Debugging:**
- [Chrome DevTools: JavaScript Debugging](https://developer.chrome.com/docs/devtools/javascript/)

---

## Lernziele-Check

Nach diesem Auftrag kannst du:
- [ ] JavaScript in externe Dateien auslagern
- [ ] Externe JavaScript-Dateien korrekt einbinden
- [ ] Mit Variablen arbeiten
- [ ] Template Strings nutzen
- [ ] Einfache Objekte und Arrays erstellen
- [ ] Funktionen definieren und aufrufen
- [ ] Die Reihenfolge von Script-Tags verstehen
- [ ] Fehler in mehreren Dateien debuggen
- [ ] Dokumentation selbstständig nutzen

---

**⏱️ Geschätzte Zeit:** 70 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 machst du deine Seite interaktiv – mit DOM-Manipulation!