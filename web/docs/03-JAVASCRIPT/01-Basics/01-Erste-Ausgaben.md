# Auftrag 1: Erste JavaScript-Ausgaben

## Ziel

Du bindest JavaScript in dein Portfolio ein und erstellst erste Ausgaben mit `console.log()` in der Browser-Konsole.

## Beschreibung

JavaScript ist die Programmiersprache, die deine Website interaktiv macht. In diesem Auftrag lernst du, wie du JavaScript einbindest und die Browser-Konsole nutzt – dein wichtigstes Werkzeug beim Entwickeln.

---

### Teil 1: JavaScript im HTML einbinden (10 Min)

Öffne deine `index.html` und füge **vor dem schliessenden `</body>`-Tag** einen `<script>`-Bereich hinzu:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dein Name - Portfolio</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Dein bisheriger HTML-Inhalt -->
    <header>
        <h1>Mein Portfolio</h1>
        <nav>
            <!-- Navigation -->
        </nav>
    </header>
    
    <main>
        <!-- Deine Sektionen -->
    </main>
    
    <footer>
        <p>&copy; 2025 Dein Name</p>
    </footer>
    
    <!-- JavaScript hier einfügen -->
    <script>
        console.log("JavaScript ist aktiv!");
    </script>
</body>
</html>
```

**Wichtig:**
- Das `<script>`-Tag steht **VOR** dem schliessenden `</body>`-Tag
- So ist sichergestellt, dass die HTML-Seite bereits geladen ist
- Inline-JavaScript schreibst du direkt zwischen `<script>` und `</script>`

---

### Teil 2: Browser-Konsole öffnen (5 Min)

Die Browser-Konsole ist dein wichtigstes Werkzeug:

**Konsole öffnen:**
- **Windows/Linux:** Drücke `F12` oder `Strg + Shift + I`
- **Mac:** Drücke `Cmd + Option + I`
- **Oder:** Rechtsklick auf die Seite → "Untersuchen" → Tab "Console"

**Du solltest sehen:**
```
JavaScript ist aktiv!
```

Die Konsole zeigt dir:
- Alle `console.log()`-Ausgaben
- Fehlermeldungen (rot)
- Warnungen (gelb)
- Informationen (blau)

---

### Teil 3: Verschiedene Ausgaben testen (15 Min)

Erweitere deinen `<script>`-Bereich mit verschiedenen Ausgaben:

```html
<script>
    // === EINFACHE TEXTE ===
    console.log("Willkommen in meinem Portfolio!");
    console.log("Mein Name ist Sarah Müller");
    
    // === ZAHLEN ===
    console.log(2025);
    console.log(42);
    
    // === BERECHNUNGEN ===
    console.log("10 + 5 =", 10 + 5);
    console.log("20 * 3 =", 20 * 3);
    console.log("100 / 4 =", 100 / 4);
    
    // === MEHRERE WERTE GLEICHZEITIG ===
    console.log("Geburtsjahr:", 2006);
    console.log("Alter:", 2025 - 2006, "Jahre");
    
    // === INFORMATIONEN ÜBER DEINE SEITE ===
    console.log("Titel der Seite:", document.title);
    console.log("URL:", window.location.href);
    
    // === TRENNLINIEN FÜR ÜBERSICHT ===
    console.log("=".repeat(50));
    console.log("Portfolio von Sarah Müller");
    console.log("=".repeat(50));
</script>
```

**Erklärungen:**
- `//` sind Kommentare – sie werden nicht ausgeführt
- `console.log()` kann Text (in Anführungszeichen) oder Zahlen (ohne Anführungszeichen) ausgeben
- Mehrere Werte trennst du mit Kommas
- `document.title` gibt den Titel deiner Seite aus
- `window.location.href` gibt die URL aus

---

### Teil 4: Persönliche Ausgaben erstellen (10 Min)

Erstelle jetzt Ausgaben über dich selbst:

```html
<script>
    console.log("=== ÜBER MICH ===");
    
    // Persönliche Infos
    console.log("Name: Sarah Müller");
    console.log("Alter:", 2025 - 2006, "Jahre");
    console.log("Beruf: Informatikerin EFZ Applikationsentwicklung");
    console.log("Lehrjahr: 1. Lehrjahr");
    
    console.log("\n=== MEINE SKILLS ===");
    console.log("- HTML");
    console.log("- CSS");
    console.log("- JavaScript (lerne ich gerade!)");
    
    console.log("\n=== AKTUELLE ZIELE ===");
    console.log("1. JavaScript Grundlagen verstehen");
    console.log("2. Interaktive Portfolio-Seite erstellen");
    console.log("3. Erste kleine Web-App programmieren");
    
    console.log("\n=== KONTAKT ===");
    console.log("GitHub: github.com/sarah-mueller");
    console.log("LinkedIn: linkedin.com/in/sarah-mueller");
</script>
```

**Tipp:** `\n` erstellt eine Leerzeile für bessere Lesbarkeit.

---

### Teil 5: Fehler erkennen und beheben (5 Min)

Teste absichtlich einen Fehler, um zu verstehen, wie die Konsole funktioniert:

```html
<script>
    console.log("Das funktioniert");
    console.log(Ups, hier fehlen Anführungszeichen);  // ❌ Fehler!
    console.log("Das wird nicht mehr ausgeführt");
</script>
```

**In der Konsole siehst du jetzt:**
```
Das funktioniert
Uncaught ReferenceError: Ups is not defined
```

**Wichtig:**
- Rote Meldungen sind Fehler – der Code stoppt hier!
- Alles nach einem Fehler wird nicht mehr ausgeführt
- Korrigiere den Fehler, speichere und aktualisiere die Seite (F5)

**Korrigierte Version:**
```html
<script>
    console.log("Das funktioniert");
    console.log("Ups, jetzt mit Anführungszeichen");  // ✅ Funktioniert!
    console.log("Das wird jetzt auch ausgeführt");
</script>
```

---

## Erfolgskriterien

- [ ] `<script>`-Tag ist vor dem schliessenden `</body>`-Tag eingefügt
- [ ] Browser-Konsole kann geöffnet werden (F12)
- [ ] Mindestens 10 verschiedene `console.log()`-Ausgaben funktionieren
- [ ] Persönliche Informationen werden in der Konsole ausgegeben
- [ ] Berechnungen (z.B. Alter) werden korrekt angezeigt
- [ ] Du verstehst, wie Fehlermeldungen aussehen und kannst sie beheben
- [ ] Kommentare (`//`) werden genutzt, um Code zu strukturieren

---

## Tipps

- **Konsole während der Entwicklung offen lassen:** So siehst du sofort, ob etwas nicht funktioniert
- **F5 zum Aktualisieren:** Nach Änderungen im Code immer die Seite neu laden
- **Strg + Shift + K (Firefox) oder Strg + Shift + J (Chrome):** Direkter Sprung zur Konsole
- **console.clear():** Löscht alle bisherigen Ausgaben – praktisch zum Aufräumen
- **Tipp für Profis:** Mit `console.table()` kannst du Arrays und Objekte übersichtlich darstellen (kommt später!)

---

## Reflexionsfragen

1. **Warum steht das `<script>`-Tag vor `</body>` und nicht im `<head>`?**  
   *Tipp: Was passiert, wenn JavaScript versucht, auf ein HTML-Element zuzugreifen, das noch nicht geladen ist?*

2. **Was ist der Unterschied zwischen diesen beiden Ausgaben?**
   ```javascript
   console.log(2025);      // Ohne Anführungszeichen
   console.log("2025");    // Mit Anführungszeichen
   ```

3. **Öffne die Konsole auf verschiedenen Websites (z.B. YouTube, Wikipedia). Was siehst du dort?**  
   *Tipp: Professionelle Websites nutzen die Konsole für Debugging und manchmal sogar für Easter Eggs!*

4. **Was passiert, wenn du einen Fehler in Zeile 5 hast, aber Zeile 10 noch wichtigen Code enthält?**  
   *Experimentiere: Erstelle absichtlich einen Fehler und schau, welche Ausgaben noch erscheinen.*

5. **Warum ist `console.log()` beim Programmieren so wichtig?**  
   *Denk an Situationen, wo dein Code nicht das tut, was du erwartest.*

---

## Weiterführende Links

**Grundlagen:**
- [MDN: console.log()](https://developer.mozilla.org/de/docs/Web/API/Console/log)
- [MDN: Das `<script>`-Element](https://developer.mozilla.org/de/docs/Web/HTML/Element/script)
- [W3Schools: JavaScript Output](https://www.w3schools.com/js/js_output.asp)

**Browser DevTools:**
- [Chrome DevTools: Console](https://developer.chrome.com/docs/devtools/console/)
- [Firefox DevTools: Web Console](https://firefox-source-docs.mozilla.org/devtools-user/web_console/)

**Interaktive Übungen:**
- [JavaScript.info: Konsole](https://javascript.info/devtools)
- [freeCodeCamp: JavaScript Basics](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

**Videos:**
- [The Net Ninja: JavaScript Console](https://www.youtube.com/watch?v=Qqx_wzMmFeA)
- [Web Dev Simplified: Console Methods](https://www.youtube.com/watch?v=L8CDt1J3DAw)

---

**⏱️ Geschätzte Zeit:** 45 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lagerst du JavaScript in eine externe Datei aus – der professionelle Weg!
