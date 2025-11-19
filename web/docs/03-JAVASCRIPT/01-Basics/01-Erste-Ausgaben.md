# Auftrag 1: Erste JavaScript-Ausgaben

## Ziel

Du bindest JavaScript in dein Portfolio ein und erstellst erste Ausgaben mit `console.log()` in der Browser-Konsole.

## Beschreibung

JavaScript ist die Programmiersprache, die deine Website interaktiv macht. In diesem Auftrag lernst du, wie du JavaScript einbindest und die Browser-Konsole nutzt – dein wichtigstes Werkzeug beim Entwickeln.

---

### Teil 1: JavaScript im HTML einbinden (10 Min)

**Aufgabe:**
Öffne deine `index.html` und füge **vor dem schliessenden `</body>`-Tag** einen `<script>`-Bereich hinzu.

**Grundstruktur (als Orientierung):**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <!-- Dein Head-Bereich -->
</head>
<body>
    <!-- Dein bisheriger HTML-Inhalt -->
    
    <!-- Hier kommt dein JavaScript -->
    
</body>
</html>
```

**Deine Aufgaben:**
1. Füge ein `<script>`-Tag vor dem schliessenden `</body>`-Tag ein
2. Schreibe **innerhalb** des Script-Tags eine Ausgabe mit `console.log()`, die den Text "JavaScript ist aktiv!" ausgibt

**Nachschlagen:**
- [MDN: Das `<script>`-Element](https://developer.mozilla.org/de/docs/Web/HTML/Element/script) - Wie bindet man JavaScript ein?
- [MDN: console.log()](https://developer.mozilla.org/de/docs/Web/API/Console/log) - Wie funktioniert die Konsolenausgabe?

**Wichtig:**
- Das `<script>`-Tag steht **VOR** dem schliessenden `</body>`-Tag
- So ist sichergestellt, dass die HTML-Seite bereits geladen ist

---

### Teil 2: Browser-Konsole öffnen (5 Min)

Die Browser-Konsole ist dein wichtigstes Werkzeug:

**Konsole Öffnen:**
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

### Teil 3: Verschiedene Ausgaben testen (20 Min)

**Aufgabe:**
Erweitere deinen `<script>`-Bereich. Erstelle folgende Ausgaben:

**3.1 Texte ausgeben**
- Gib deinen Namen aus
- Gib deinen Beruf aus ("Informatikerin EFZ Applikationsentwicklung")
- Gib dein Lehrjahr aus

**3.2 Zahlen und Berechnungen**
- Gib das aktuelle Jahr (2025) aus
- Berechne dein Alter: `2025 - deinGeburtsjahr`
- Berechne: `10 + 5`
- Berechne: `20 * 3`

**3.3 Mehrere Werte kombinieren**
- Gib "Geburtsjahr:" und dein Geburtsjahr in **einer** Zeile aus
- Gib "Alter:" und dein berechnetes Alter in **einer** Zeile aus

**Tipp:** Du kannst mehrere Werte mit Kommas trennen:
```javascript
console.log("Text", variable, "mehr Text");
```

**3.4 Seiteninfos ausgeben**
- Gib den Titel deiner Seite aus (Hinweis: `document.title`)
- Gib die URL deiner Seite aus (Hinweis: `window.location.href`)

**3.5 Trennlinien für Übersicht**
- Erstelle eine Trennlinie aus 50 Gleichheitszeichen
- Tipp: Recherchiere die `.repeat()` Methode

**Nachschlagen:**
- [MDN: Expressions and operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators) - Mathematische Operationen
- [MDN: String.prototype.repeat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat) - Zeichen wiederholen
- [W3Schools: JavaScript Output](https://www.w3schools.com/js/js_output.asp) - Verschiedene Ausgabearten

**Hinweise:**
- `//` sind Kommentare – sie werden nicht ausgeführt (nutze sie zur Strukturierung!)
- Text muss in Anführungszeichen ("Text" oder 'Text')
- Zahlen stehen ohne Anführungszeichen
- `\n` erstellt eine Leerzeile

---

### Teil 4: Persönliche Ausgaben strukturieren (15 Min)

**Aufgabe:**
Erstelle eine strukturierte Ausgabe über dich selbst mit folgenden Abschnitten:

**Struktur:**
```
=== ÜBER MICH ===
Name: [Dein Name]
Alter: [Dein Alter] Jahre
Beruf: [Dein Beruf]
Lehrjahr: [Dein Lehrjahr]

=== MEINE SKILLS ===
[Liste deine Skills auf]

=== AKTUELLE ZIELE ===
[Liste deine Ziele auf]

=== KONTAKT ===
[Deine Kontaktinfos]
```

**Vorgehen:**
1. Überlege dir, welche Informationen du ausgeben möchtest
2. Strukturiere mit Überschriften (z.B. "=== ÜBER MICH ===")
3. Nutze `\n` für Abstände zwischen Abschnitten
4. Teste deine Ausgaben in der Konsole

---

### Teil 5: Fehler erkennen und beheben (10 Min)

**Aufgabe:**
Erstelle absichtlich folgende Fehler und beobachte die Konsolenmeldungen:

**Fehler 1: Fehlende Anführungszeichen**
```javascript
console.log(Das ist ein Fehler);
```
- Was zeigt die Konsole?
- Korrigiere den Fehler
- Speichere und aktualisiere (F5)

**Fehler 2: Fehlende Klammer**
```javascript
console.log("Test";
```
- Was zeigt die Konsole?
- Korrigiere den Fehler

**Fehler 3: Falsche Variable**
```javascript
console.log(nichtExistierendeVariable);
```
- Was zeigt die Konsole?
- Was ist der Unterschied zu den anderen Fehlern?

**Beobachtung:**
- Wo stoppt die Ausführung?
- Werden Zeilen nach dem Fehler noch ausgeführt?
- Wie sehen Fehlermeldungen aus?

**Nachschlagen:**
- [MDN: JavaScript Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors) - Fehlertypen verstehen
- [Chrome DevTools: Console](https://developer.chrome.com/docs/devtools/console/) - Konsole effektiv nutzen

---

## Erfolgskriterien

- [ ] `<script>`-Tag ist vor dem schliessenden `</body>`-Tag eingefügt
- [ ] Browser-Konsole kann geöffnet werden (F12)
- [ ] Mindestens 10 verschiedene `console.log()`-Ausgaben funktionieren
- [ ] Persönliche Informationen werden in der Konsole ausgegeben
- [ ] Berechnungen (z.B. Alter) werden korrekt angezeigt
- [ ] Du verstehst, wie Fehlermeldungen aussehen und kannst sie beheben
- [ ] Kommentare (`//`) werden genutzt, um Code zu strukturieren
- [ ] Ausgaben sind sinnvoll strukturiert (mit Überschriften, Abständen)

---

## Zusatzaufgaben (Optional)

**Für Schnelle:**

**A) Erweiterte Berechnungen**
- Berechne, wie viele Tage du bereits in der Lehre bist (ca.-Wert)
- Berechne, wie viele Tage noch bis zum Lehrabschluss (ca.-Wert)

**B) Browser-Informationen**
Recherchiere und gib aus:
- Die Bildschirmbreite (Hinweis: `window.innerWidth`)
- Die Bildschirmhöhe (Hinweis: `window.innerHeight`)
- Den Browser-Namen (Hinweis: `navigator.userAgent`)

**C) Kreative Ausgaben**
- Erstelle ein ASCII-Art Banner mit deinem Namen
- Nutze verschiedene Zeichen (=, -, *, #) für Rahmen

**Nachschlagen:**
- [MDN: Window](https://developer.mozilla.org/en-US/docs/Web/API/Window) - Fenster-Eigenschaften
- [MDN: Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) - Browser-Informationen

---

## Tipps

- **Konsole während der Entwicklung offen lassen:** So siehst du sofort, ob etwas nicht funktioniert
- **F5 zum Aktualisieren:** Nach Änderungen im Code immer die Seite neu laden
- **Strg + Shift + K (Firefox) oder Strg + Shift + J (Chrome):** Direkter Sprung zur Konsole
- **console.clear():** Löscht alle bisherigen Ausgaben – praktisch zum Aufräumen
- **Fehler von unten nach oben lesen:** Oft ist der erste Fehler in der Liste der wichtigste

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

---

## Lernziele-Check

Nach diesem Auftrag kannst du:
- [ ] JavaScript in HTML einbinden
- [ ] Die Browser-Konsole öffnen und nutzen
- [ ] Verschiedene Datentypen ausgeben (Text, Zahlen)
- [ ] Einfache Berechnungen durchführen
- [ ] Fehler in der Konsole erkennen und interpretieren
- [ ] Code mit Kommentaren strukturieren
- [ ] Auf einfache Dokumentation zugreifen und sie anwenden

---

**⏱️ Geschätzte Zeit:** 60 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lagerst du JavaScript in eine externe Datei aus – der professionelle Weg!