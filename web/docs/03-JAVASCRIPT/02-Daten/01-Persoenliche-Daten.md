# Auftrag 1: Persönliche Daten mit Variablen

## Ziel

Du lernst, mit Variablen zu arbeiten, verschiedene Datentypen zu unterscheiden und Template Literals für formatierte Ausgaben zu nutzen. Deine persönlichen Portfolio-Daten werden strukturiert gespeichert und ausgegeben.

## Beschreibung

Variablen sind wie beschriftete Schubladen – sie speichern Werte, auf die du später zugreifen kannst. In diesem Auftrag erstellst du ein persönliches Datenprofil für dein Portfolio mit let und const, nutzt verschiedene Datentypen und gibst alles formatiert in der Konsole aus.

---

### Teil 1: Grundlegende persönliche Daten (10 Min)

Erstelle eine neue Datei **`personal-data.js`** in deinem Projektordner und binde sie in deine `index.html` ein:

```html
<script src="script.js"></script>
<script src="personal-data.js"></script>
```

**In `personal-data.js`:**

```javascript
// =====================================================
// PERSÖNLICHE DATEN
// =====================================================

console.log("=== MEIN PROFIL ===\n");

// Name und Identität
const vorname = "Sarah";
const nachname = "Müller";
const geburtsjahr = 2006;

// Kontaktdaten
let email = "sarah.mueller@example.com";
let telefon = "+41 79 123 45 67";

// Berufsinformationen
const beruf = "Informatikerin EFZ Applikationsentwicklung";
let lehrjahr = 1;
const lehrbetrieb = "ACME Technologies AG";

// Ausgabe mit Template Literals
console.log(`Name: ${vorname} ${nachname}`);
console.log(`Geburtsjahr: ${geburtsjahr}`);
console.log(`E-Mail: ${email}`);
console.log(`Telefon: ${telefon}`);
console.log(`Beruf: ${beruf}`);
console.log(`Lehrjahr: ${lehrjahr}`);
console.log(`Lehrbetrieb: ${lehrbetrieb}`);
```

**Wichtig:**
- `const` für Werte, die sich nicht ändern (Name, Geburtsjahr)
- `let` für Werte, die sich ändern können (Lehrjahr, Telefonnummer)
- Template Literals mit Backticks `` ` `` für formatierte Ausgaben
- `${}` fügt Variablen in Strings ein

---

### Teil 2: Berechnungen mit Variablen (10 Min)

Erweitere `personal-data.js` mit Berechnungen:

```javascript
// === BERECHNUNGEN ===

console.log("\n=== BERECHNUNGEN ===\n");

// Alter berechnen
const aktuellesJahr = new Date().getFullYear();
const alter = aktuellesJahr - geburtsjahr;

console.log(`Aktuelles Jahr: ${aktuellesJahr}`);
console.log(`Mein Alter: ${alter} Jahre`);

// Lehrjahre
const lehrzeit = 4;  // 4 Jahre Ausbildung
const verbleibendeJahre = lehrzeit - lehrjahr;

console.log(`Lehrzeit: ${lehrzeit} Jahre`);
console.log(`Verbleibende Lehrjahre: ${verbleibendeJahre}`);

// Lehrabschluss berechnen
const startJahr = 2025;  // Beispiel
const abschlussJahr = startJahr + lehrzeit;

console.log(`Lehrstart: ${startJahr}`);
console.log(`Lehrabschluss: ${abschlussJahr}`);

// Prozentuale Fortschritt
const fortschritt = (lehrjahr / lehrzeit) * 100;

console.log(`Fortschritt: ${fortschritt}%`);
```

**Neue Konzepte:**
- Mathematische Operationen mit Variablen
- `new Date().getFullYear()` gibt aktuelles Jahr zurück
- Prozentrechnung mit JavaScript

---

### Teil 3: Verschiedene Datentypen (15 Min)

Ergänze verschiedene Datentypen und prüfe sie mit `typeof`:

```javascript
// === DATENTYPEN ===

console.log("\n=== DATENTYPEN ===\n");

// String (Text)
let stadt = "Bern";
let postleitzahl = "3000";  // Als String, nicht Number!

// Number (Zahlen)
let anzahlProjekte = 5;
let durchschnittsNote = 5.2;
let temperatur = -3;

// Boolean (Wahrheitswerte)
let istVolljährig = alter >= 18;
let hatFührerschein = false;
let sprichtEnglisch = true;

// Array (Listen)
let hobbies = ["Programmieren", "Gaming", "Lesen"];
let lieblingszahlen = [7, 13, 42];

// Ausgabe mit Typprüfung
console.log(`Stadt: ${stadt} (Typ: ${typeof stadt})`);
console.log(`Postleitzahl: ${postleitzahl} (Typ: ${typeof postleitzahl})`);
console.log(`Projekte: ${anzahlProjekte} (Typ: ${typeof anzahlProjekte})`);
console.log(`Note: ${durchschnittsNote} (Typ: ${typeof durchschnittsNote})`);
console.log(`Volljährig: ${istVolljährig} (Typ: ${typeof istVolljährig})`);
console.log(`Hobbies: ${hobbies} (Typ: ${typeof hobbies})`);

// Hinweis: Arrays werden als "object" angezeigt
console.log(`Ist Array?: ${Array.isArray(hobbies)}`);
```

**Erklärungen:**
- **String:** Text in Anführungszeichen `"..."` oder `'...'`
- **Number:** Zahlen ohne Anführungszeichen (auch Dezimalzahlen)
- **Boolean:** `true` oder `false` (ohne Anführungszeichen!)
- **Array:** Liste von Werten `[wert1, wert2, wert3]`
- `typeof` zeigt den Datentyp an

---

### Teil 4: Strukturierte Ausgabe (10 Min)

Erstelle eine übersichtliche, formatierte Ausgabe:

```javascript
// === STRUKTURIERTE AUSGABE ===

console.log("\n" + "=".repeat(50));
console.log("PORTFOLIO – PERSÖNLICHE DATEN");
console.log("=".repeat(50) + "\n");

console.log("📋 PERSÖNLICHE INFORMATIONEN");
console.log("─".repeat(50));
console.log(`   Name:            ${vorname} ${nachname}`);
console.log(`   Geburtsjahr:     ${geburtsjahr} (${alter} Jahre alt)`);
console.log(`   Wohnort:         ${stadt}, Schweiz`);
console.log("");

console.log("💼 BERUFLICHES");
console.log("─".repeat(50));
console.log(`   Beruf:           ${beruf}`);
console.log(`   Lehrjahr:        ${lehrjahr}/${lehrzeit}`);
console.log(`   Lehrbetrieb:     ${lehrbetrieb}`);
console.log(`   Fortschritt:     ${fortschritt}%`);
console.log(`   Abschluss:       ${abschlussJahr}`);
console.log("");

console.log("📞 KONTAKT");
console.log("─".repeat(50));
console.log(`   E-Mail:          ${email}`);
console.log(`   Telefon:         ${telefon}`);
console.log("");

console.log("🎯 HOBBIES");
console.log("─".repeat(50));
for (let i = 0; i < hobbies.length; i++) {
    console.log(`   ${i + 1}. ${hobbies[i]}`);
}
console.log("");

console.log("✓ STATUS");
console.log("─".repeat(50));
console.log(`   Volljährig:      ${istVolljährig ? "Ja" : "Nein"}`);
console.log(`   Führerschein:    ${hatFührerschein ? "Ja" : "Nein"}`);
console.log(`   Englisch:        ${sprichtEnglisch ? "Ja" : "Nein"}`);
console.log("");

console.log("=".repeat(50));
```

**Neue Elemente:**
- `.repeat(n)` wiederholt einen String n-mal
- `\n` erzeugt Zeilenumbruch
- Ternärer Operator: `bedingung ? wennWahr : wennFalsch`
- For-Schleife für Array-Ausgabe

---

### Teil 5: Daten im HTML anzeigen (5 Min)

Füge in deiner `index.html` ein neues `<div>` ein:

```html
<section id="profil">
    <h2>Mein Profil</h2>
    <div id="profil-daten">
        <!-- Wird von JavaScript gefüllt -->
    </div>
</section>
```

Ergänze am Ende von `personal-data.js`:

```javascript
// === IM HTML ANZEIGEN ===

document.getElementById("profil-daten").innerHTML = `
    <div class="profil-card">
        <h3>${vorname} ${nachname}</h3>
        <p><strong>Alter:</strong> ${alter} Jahre</p>
        <p><strong>Beruf:</strong> ${beruf}</p>
        <p><strong>Lehrjahr:</strong> ${lehrjahr}/${lehrzeit} (${fortschritt}% abgeschlossen)</p>
        <p><strong>Wohnort:</strong> ${stadt}, Schweiz</p>
        <p><strong>Hobbies:</strong> ${hobbies.join(", ")}</p>
        <p><strong>E-Mail:</strong> <a href="mailto:${email}">${email}</a></p>
    </div>
`;
```

**Tipp:** Ergänze später CSS für schöneres Styling der `.profil-card`!

---

## Erfolgskriterien

- [ ] `personal-data.js` ist erstellt und eingebunden
- [ ] Mindestens 8 verschiedene Variablen sind deklariert (Name, Alter, Beruf, etc.)
- [ ] `const` wird für unveränderliche Werte genutzt, `let` für veränderliche
- [ ] Mindestens 3 verschiedene Datentypen werden verwendet (String, Number, Boolean)
- [ ] Template Literals mit `${}` werden für formatierte Ausgaben genutzt
- [ ] Alter wird aus Geburtsjahr berechnet
- [ ] Prozentuale Fortschrittsberechnung funktioniert
- [ ] `typeof` wird genutzt, um Datentypen zu prüfen
- [ ] Strukturierte Konsolenausgabe mit Formatierung (Linien, Emojis)
- [ ] Daten werden im HTML angezeigt (mit `innerHTML`)

---

## Tipps

- **const vs. let:** Nutze `const` immer, wenn sich der Wert nicht ändern soll – das verhindert versehentliche Fehler
- **Namenskonventionen:** Variablennamen immer mit Kleinbuchstaben beginnen, bei mehreren Wörtern camelCase nutzen: `meineVariable`
- **Template Literals sind mächtiger:** Sie unterstützen auch mehrzeilige Strings und eingebettete Ausdrücke
- **typeof für Debugging:** Wenn etwas nicht funktioniert, prüfe mit `typeof`, ob die Variable den erwarteten Typ hat
- **Kommentare nutzen:** Schreibe Kommentare (`//`) zu deinem Code – du wirst es später schätzen!
- **Konsole immer offen:** Lass die Browser-Konsole während der Entwicklung geöffnet (F12)

---

## Reflexionsfragen

1. **Was passiert, wenn du versuchst, eine `const` Variable zu ändern?**  
   *Teste es: Erstelle `const name = "Max"` und versuche dann `name = "Tim"`. Was zeigt die Konsole?*

2. **Warum sollte Postleitzahl als String und nicht als Number gespeichert werden?**  
   *Tipp: Führende Nullen! Was passiert mit `0800` als Number?*

3. **Was ist der Unterschied zwischen diesen Ausgaben?**
   ```javascript
   console.log("Alter: " + alter);           // String-Konkatenation
   console.log(`Alter: ${alter}`);           // Template Literal
   ```
   *Welche Methode ist lesbarer bei vielen Variablen?*

4. **Experimentiere: Was gibt `typeof null` zurück?**  
   *Ist das korrekt? Recherchiere, warum JavaScript hier ein bekanntes "Bug" hat.*

5. **Erstelle eine Variable `let zahl = "42"`. Was ist ihr Typ?**  
   *Wie kannst du sie in eine echte Number umwandeln? Tipp: `parseInt()` oder `Number()`*

---

## Weiterführende Links

**JavaScript Grundlagen:**
- [MDN: let](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/let)
- [MDN: const](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/const)
- [MDN: Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)
- [MDN: typeof](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/typeof)

**Datentypen:**
- [JavaScript.info: Datentypen](https://javascript.info/types)
- [W3Schools: JS Data Types](https://www.w3schools.com/js/js_datatypes.asp)
- [MDN: JavaScript Datentypen](https://developer.mozilla.org/de/docs/Web/JavaScript/Data_structures)

**Best Practices:**
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

**Interaktive Übungen:**
- [freeCodeCamp: JavaScript Basics](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- [JavaScript.info: Variables](https://javascript.info/variables)

**Videos:**
- [The Net Ninja: Variables & Data Types](https://www.youtube.com/watch?v=Hrd3SfCCXZw)
- [Web Dev Simplified: Let vs Const](https://www.youtube.com/watch?v=9WIJQDvt4Us)

---

**Geschätzte Zeit:** 50 Minuten  
**Nächster Schritt:** In Auftrag 2 nutzt du if-else Verzweigungen, um auf Bedingungen zu reagieren!
