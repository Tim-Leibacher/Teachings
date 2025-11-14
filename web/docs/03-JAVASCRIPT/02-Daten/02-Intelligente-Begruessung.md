# Auftrag 2: Intelligente Begrüssung mit if-else

## Ziel

Du lernst, mit if-else Verzweigungen und logischen Operatoren zu arbeiten, um Bedingungen zu prüfen und darauf zu reagieren. Deine Portfolio-Seite zeigt eine kontextabhängige Begrüssung basierend auf Tageszeit, Wochentag und Benutzerinteraktionen.

## Beschreibung

Kontrollstrukturen sind das Gehirn deines Codes – sie treffen Entscheidungen basierend auf Bedingungen. Mit if-else kann dein Portfolio intelligent auf verschiedene Situationen reagieren: Ist es Morgen oder Abend? Ist heute Wochenende? Ist der Besucher zum ersten Mal hier? Das macht Websites persönlich und interaktiv.

---

### Teil 1: Tageszeit-abhängige Begrüssung (15 Min)

Erstelle eine neue Datei **`greeting.js`** und binde sie ein:

```html
<script src="script.js"></script>
<script src="personal-data.js"></script>
<script src="greeting.js"></script>
```

**In `greeting.js`:**

```javascript
// =====================================================
// INTELLIGENTE BEGRÜSSUNG
// =====================================================

console.log("=== BEGRÜSSUNG ===\n");

// Aktuelle Zeit holen
const jetzt = new Date();
const stunde = jetzt.getHours();
const minute = jetzt.getMinutes();

console.log(`Aktuelle Uhrzeit: ${stunde}:${minute < 10 ? '0' + minute : minute} Uhr`);

// Tageszeit-abhängige Begrüssung
let begruessung = "";
let emoji = "";
let hinweis = "";

if (stunde >= 5 && stunde < 12) {
    begruessung = "Guten Morgen";
    emoji = "☀️";
    hinweis = "Zeit für Kaffee und Code!";
} else if (stunde >= 12 && stunde < 14) {
    begruessung = "Guten Tag";
    emoji = "🌤️";
    hinweis = "Mittagszeit – vergiss die Pause nicht!";
} else if (stunde >= 14 && stunde < 18) {
    begruessung = "Guten Nachmittag";
    emoji = "☁️";
    hinweis = "Produktivste Zeit des Tages!";
} else if (stunde >= 18 && stunde < 22) {
    begruessung = "Guten Abend";
    emoji = "🌆";
    hinweis = "Zeit zum Entspannen oder noch ein bisschen coden?";
} else {
    begruessung = "Gute Nacht";
    emoji = "🌙";
    hinweis = "Spät unterwegs? Vergiss nicht zu schlafen!";
}

console.log(`${emoji} ${begruessung}!`);
console.log(`Hinweis: ${hinweis}`);
```

**Neue Konzepte:**
- `new Date()` erstellt Datumsobjekt mit aktueller Zeit
- `.getHours()` gibt Stunde zurück (0-23)
- `.getMinutes()` gibt Minute zurück (0-59)
- `&&` (AND) verbindet zwei Bedingungen – beide müssen wahr sein
- Mehrere `else if` für verschiedene Zeitbereiche
- Ternärer Operator `? :` für führende Null bei Minuten

---

### Teil 2: Wochentag-abhängige Nachrichten (15 Min)

Erweitere `greeting.js` mit Wochentags-Logik:

```javascript
// === WOCHENTAG ===

console.log("\n=== WOCHENTAG ===\n");

const tag = jetzt.getDay();  // 0 = Sonntag, 1 = Montag, ..., 6 = Samstag
let wochentagName = "";
let wochentagTyp = "";
let motivation = "";

// Wochentag bestimmen
if (tag === 0) {
    wochentagName = "Sonntag";
    wochentagTyp = "Wochenende";
    motivation = "Erholung ist wichtig!";
} else if (tag === 1) {
    wochentagName = "Montag";
    wochentagTyp = "Wochentag";
    motivation = "Frisch in die neue Woche!";
} else if (tag === 2) {
    wochentagName = "Dienstag";
    wochentagTyp = "Wochentag";
    motivation = "Der Dienstag ist oft der produktivste Tag!";
} else if (tag === 3) {
    wochentagName = "Mittwoch";
    wochentagTyp = "Wochentag";
    motivation = "Halbzeit der Woche!";
} else if (tag === 4) {
    wochentagName = "Donnerstag";
    wochentagTyp = "Wochentag";
    motivation = "Fast geschafft!";
} else if (tag === 5) {
    wochentagName = "Freitag";
    wochentagTyp = "Wochentag";
    motivation = "TGIF – Thank God It's Friday!";
} else if (tag === 6) {
    wochentagName = "Samstag";
    wochentagTyp = "Wochenende";
    motivation = "Wochenende geniessen!";
}

console.log(`Heute ist ${wochentagName} (${wochentagTyp})`);
console.log(`Motivation: ${motivation}`);

// Prüfen, ob Wochenende
let istWochenende = (tag === 0 || tag === 6);

if (istWochenende) {
    console.log("✓ Es ist Wochenende!");
} else {
    console.log("→ Es ist ein Arbeitstag");
}
```

**Neue Konzepte:**
- `.getDay()` gibt Wochentag zurück (0-6)
- `===` für strikte Gleichheitsprüfung (Wert und Typ)
- `||` (OR) bedeutet "oder" – mindestens eine Bedingung muss wahr sein
- Klammern `()` gruppieren Bedingungen

---

### Teil 3: Verschachtelte Bedingungen (15 Min)

Erstelle komplexere Logik mit verschachtelten if-else:

```javascript
// === ARBEITSZEIT-ANALYSE ===

console.log("\n=== ARBEITSZEIT-ANALYSE ===\n");

// Ist es ein Arbeitstag UND Arbeitszeit?
if (!istWochenende) {
    console.log("Arbeitstag erkannt");
    
    if (stunde >= 8 && stunde < 17) {
        console.log("→ Reguläre Arbeitszeit (08:00 - 17:00)");
        
        if (stunde >= 12 && stunde < 13) {
            console.log("   → Mittagspause empfohlen");
        } else {
            console.log("   → Volle Konzentration!");
        }
    } else if (stunde >= 17 && stunde < 20) {
        console.log("→ Feierabend – Zeit für Hobbies!");
    } else {
        console.log("→ Ausserhalb der Arbeitszeit");
    }
} else {
    console.log("Wochenende – Erholung oder Hobby-Projekte?");
    
    if (stunde >= 9 && stunde < 22) {
        console.log("→ Guter Zeitpunkt für persönliche Projekte!");
    } else {
        console.log("→ Ruhezeit – morgen ist auch noch ein Tag!");
    }
}
```

**Neue Konzepte:**
- `!` (NOT) kehrt Boolean um: `!true` wird zu `false`
- Verschachtelte if-else für komplexe Entscheidungen
- Einrückungen zeigen Struktur – extrem wichtig für Lesbarkeit!

---

### Teil 4: Logische Operatoren kombinieren (10 Min)

```javascript
// === KOMPLEXE BEDINGUNGEN ===

console.log("\n=== STATUS-CHECK ===\n");

// Verschiedene Variablen
const istAngemeldet = true;
const istAdmin = false;
const hatBerechtigung = true;
const istBetaUser = false;

// AND-Verknüpfung (alle müssen wahr sein)
if (istAngemeldet && hatBerechtigung) {
    console.log("✓ Zugriff erlaubt");
} else {
    console.log("✗ Zugriff verweigert");
}

// OR-Verknüpfung (mindestens eine muss wahr sein)
if (istAdmin || istBetaUser) {
    console.log("✓ Erweiterte Features verfügbar");
} else {
    console.log("→ Standard-Features");
}

// Kombination von AND und OR mit Klammern
if (istAngemeldet && (istAdmin || hatBerechtigung)) {
    console.log("✓ Premium-Bereich zugänglich");
} else {
    console.log("✗ Nur öffentlicher Bereich");
}

// NOT-Operator
if (!istAdmin) {
    console.log("→ Kein Admin – eingeschränkte Berechtigungen");
}

// Mehrere Bedingungen
if (istAngemeldet && hatBerechtigung && !istAdmin) {
    console.log("→ Normaler Benutzer mit Berechtigungen");
}
```

**Wahrheitstabellen:**

```
AND (&&):
true  && true  = true
true  && false = false
false && false = false

OR (||):
true  || true  = true
true  || false = true
false || false = false

NOT (!):
!true  = false
!false = true
```

---

### Teil 5: Besucher-Tracking mit LocalStorage (15 Min)

```javascript
// === BESUCHER-TRACKING ===

console.log("\n=== BESUCHER-INFO ===\n");

// Besucher-Zähler
let besuchsZahl = localStorage.getItem("besuchsZahl");

if (besuchsZahl === null) {
    // Erster Besuch
    besuchsZahl = 1;
    localStorage.setItem("besuchsZahl", besuchsZahl);
    console.log("🎉 Willkommen zum ersten Mal!");
} else {
    // Wiederkehrender Besucher
    besuchsZahl = parseInt(besuchsZahl) + 1;
    localStorage.setItem("besuchsZahl", besuchsZahl);
    console.log(`👋 Willkommen zurück! Besuch Nr. ${besuchsZahl}`);
}

// Unterschiedliche Nachrichten je nach Besuchsanzahl
let besucherStatus = "";

if (besuchsZahl === 1) {
    besucherStatus = "Neu hier? Schau dich um!";
} else if (besuchsZahl >= 2 && besuchsZahl <= 5) {
    besucherStatus = "Schön, dass du wieder da bist!";
} else if (besuchsZahl > 5 && besuchsZahl <= 10) {
    besucherStatus = "Du bist jetzt Stammgast!";
} else if (besuchsZahl > 10) {
    besucherStatus = "Wow, du liebst diese Seite! 🏆";
}

console.log(`Status: ${besucherStatus}`);

// Letzter Besuch speichern
const jetziger_Zeitstempel = new Date().toLocaleString("de-CH");
localStorage.setItem("letzterBesuch", jetziger_Zeitstempel);

const letzterBesuch = localStorage.getItem("letzterBesuch");
if (letzterBesuch) {
    console.log(`Letzter Besuch: ${letzterBesuch}`);
}
```

**Neue Konzepte:**
- `localStorage.getItem()` liest gespeicherte Daten
- `localStorage.setItem()` speichert Daten dauerhaft
- `=== null` prüft, ob noch keine Daten gespeichert sind
- `parseInt()` wandelt String in Zahl um
- `toLocaleString()` formatiert Datum/Zeit nach Region

---

### Teil 6: Personalisierte Ausgabe im HTML (10 Min)

Füge in `index.html` ein:

```html
<section id="willkommen">
    <div id="begruessung-box">
        <!-- Wird von JavaScript gefüllt -->
    </div>
</section>
```

Am Ende von `greeting.js`:

```javascript
// === IM HTML ANZEIGEN ===

let htmlAusgabe = `
    <div class="greeting-card">
        <h2>${emoji} ${begruessung}!</h2>
        <p><strong>Heute ist ${wochentagName}</strong> – ${hinweis}</p>
        <p>${besucherStatus}</p>
        <p><small>Du bist zum ${besuchsZahl}. Mal hier. Letzter Besuch: ${letzterBesuch || "Gerade eben"}</small></p>
    </div>
`;

// Zusätzliche Infos basierend auf Bedingungen
if (istWochenende && stunde >= 10 && stunde < 20) {
    htmlAusgabe += `
        <div class="tip-box">
            💡 <strong>Tipp:</strong> Perfekte Zeit für persönliche Projekte!
        </div>
    `;
} else if (!istWochenende && stunde >= 8 && stunde < 17) {
    htmlAusgabe += `
        <div class="tip-box">
            💼 <strong>Hinweis:</strong> Arbeitszeit – fokussiere dich!
        </div>
    `;
}

document.getElementById("begruessung-box").innerHTML = htmlAusgabe;

console.log("\n✓ Begrüssung im HTML angezeigt");
```

---

## Erfolgskriterien

- [ ] `greeting.js` ist erstellt und eingebunden
- [ ] Tageszeit-abhängige Begrüssung funktioniert (Morgen/Mittag/Abend/Nacht)
- [ ] Wochentag wird erkannt und angezeigt
- [ ] Wochenende vs. Arbeitstag wird unterschieden
- [ ] Logische Operatoren (`&&`, `||`, `!`) werden genutzt
- [ ] Verschachtelte if-else Strukturen sind implementiert
- [ ] Besucher-Zähler mit localStorage funktioniert
- [ ] Unterschiedliche Nachrichten je nach Besuchsanzahl
- [ ] Personalisierte Ausgabe wird im HTML angezeigt
- [ ] Keine Fehler in der Konsole

---

## Tipps

- **Strikt vergleichen:** Nutze immer `===` statt `==` für Vergleiche
- **Klammern bei komplexen Bedingungen:** `(a && b) || c` ist klarer als `a && b || c`
- **Einrückungen beachten:** Jede verschachtelte Ebene eine Stufe weiter einrücken
- **LocalStorage testen:** Mit `localStorage.clear()` in der Konsole alle Daten löschen und neu testen
- **Boolean-Variablen klar benennen:** `istWochenende`, `hatBerechtigung` sind lesbarer als `w`, `b`
- **Debugging:** Nutze `console.log()` vor und nach if-else, um zu sehen, welcher Block ausgeführt wird

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `==` und `===`?**  
   *Teste: `5 == "5"` vs. `5 === "5"`. Was kommt raus und warum?*

2. **Warum nutzen wir Klammern bei `(tag === 0 || tag === 6)`?**  
   *Was würde ohne Klammern bei `!istWochenende && tag === 0 || tag === 6` passieren?*

3. **Experimentiere: Ändere die Systemzeit deines Computers. Wie reagiert die Begrüssung?**  
   *Verstehst du, wie `new Date()` funktioniert?*

4. **Was passiert, wenn du `localStorage.clear()` in der Konsole ausführst?**  
   *Teste es und lade die Seite neu. Was siehst du?*

5. **Erstelle eine Bedingung, die nur an Freitagen zwischen 15:00 und 17:00 Uhr wahr ist.**  
   *Wie sieht die if-Bedingung aus? Tipp: Kombiniere `tag === 5 && ...`*

---

## Weiterführende Links

**If-Else & Kontrollstrukturen:**
- [MDN: if...else](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/if...else)
- [MDN: Vergleichsoperatoren](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)
- [JavaScript.info: Bedingungen](https://javascript.info/ifelse)

**Logische Operatoren:**
- [MDN: Logische Operatoren](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
- [W3Schools: JS Comparison](https://www.w3schools.com/js/js_comparisons.asp)

**LocalStorage:**
- [MDN: Web Storage API](https://developer.mozilla.org/de/docs/Web/API/Web_Storage_API)
- [JavaScript.info: LocalStorage](https://javascript.info/localstorage)

**Best Practices:**
- [Clean Code JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
- [JavaScript Naming Conventions](https://www.robinwieruch.de/javascript-naming-conventions/)

**Interaktive Übungen:**
- [freeCodeCamp: Basic JavaScript](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- [Codecademy: Conditionals](https://www.codecademy.com/learn/introduction-to-javascript)

---

**Geschätzte Zeit:** 80 Minuten  
**Nächster Schritt:** In Auftrag 3 automatisierst du Wiederholungen mit Schleifen!
