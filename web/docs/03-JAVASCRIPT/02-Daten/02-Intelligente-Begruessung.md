# Auftrag 2: Intelligente Begrüssung mit if-else

## Ziel

Du lernst, mit if-else Verzweigungen und logischen Operatoren zu arbeiten, um Bedingungen zu prüfen und darauf zu reagieren. Deine Portfolio-Seite zeigt eine kontextabhängige Begrüssung basierend auf Tageszeit, Wochentag und Benutzerinteraktionen.

## Beschreibung

Kontrollstrukturen sind das Gehirn deines Codes – sie treffen Entscheidungen basierend auf Bedingungen. Mit if-else kann dein Portfolio intelligent auf verschiedene Situationen reagieren: Ist es Morgen oder Abend? Ist heute Wochenende? Ist der Besucher zum ersten Mal hier?

---

### Teil 1: Tageszeit-abhängige Begrüssung (20 Min)

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

// TODO 1.1: Hole die aktuelle Zeit
// Nutze: new Date(), .getHours() und .getMinutes()
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date

const jetzt = // Deine Lösung
const stunde = // Deine Lösung
const minute = // Deine Lösung


// TODO 1.2: Gib die aktuelle Uhrzeit formatiert aus
// Format: "Aktuelle Uhrzeit: 14:05 Uhr"
// Tipp: Nutze ternären Operator für führende Null bei Minuten unter 10
// Beispiel: minute < 10 ? '0' + minute : minute

console.log(// Deine Lösung);


// TODO 1.3: Erstelle Variablen für Begrüssung, Emoji und Hinweis
let begruessung = "";
let emoji = "";
let hinweis = "";


// TODO 1.4: Implementiere if-else Struktur für verschiedene Tageszeiten
// Dokumentation if-else: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/if...else
// Dokumentation Vergleichsoperatoren: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators

// Zeitbereiche:
// 05:00 - 11:59: "Guten Morgen" mit ☀️
// 12:00 - 13:59: "Guten Tag" mit 🌤️
// 14:00 - 17:59: "Guten Nachmittag" mit ☁️
// 18:00 - 21:59: "Guten Abend" mit 🌆
// 22:00 - 04:59: "Gute Nacht" mit 🌙

// Tipp: Nutze && (AND) Operator für Zeitbereiche
// Beispiel: if (stunde >= 5 && stunde < 12) { ... }

if (/* Bedingung für Morgen */) {
    begruessung = // Deine Lösung
    emoji = // Deine Lösung
    hinweis = // Deine Lösung (z.B. "Zeit für Kaffee und Code!")
} else if (/* Bedingung für Mittag */) {
    // Deine Lösung
} else if (/* Bedingung für Nachmittag */) {
    // Deine Lösung
} else if (/* Bedingung für Abend */) {
    // Deine Lösung
} else {
    // Deine Lösung für Nacht
}


// TODO 1.5: Gib Begrüssung und Hinweis aus
console.log(// Deine Lösung);
console.log(// Deine Lösung);
```

**Lernziele:**
- Date-Objekt selbst nutzen und Stunden/Minuten extrahieren
- if-else-if Kette selbst aufbauen
- Logische Operatoren (&&) verstehen und anwenden

---

### Teil 2: Wochentag-abhängige Nachrichten (20 Min)

Erweitere `greeting.js` mit Wochentags-Logik:

```javascript
// === WOCHENTAG ===

console.log("\n=== WOCHENTAG ===\n");

// TODO 2.1: Hole den Wochentag
// .getDay() gibt 0-6 zurück (0 = Sonntag, 1 = Montag, ..., 6 = Samstag)
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay

const tag = // Deine Lösung


// TODO 2.2: Erstelle Variablen für Wochentagsdaten
let wochentagName = "";
let wochentagTyp = "";  // "Wochentag" oder "Wochenende"
let motivation = "";


// TODO 2.3: Implementiere if-else für alle Wochentage (0-6)
// Für jeden Tag: wochentagName setzen, wochentagTyp, passende Motivation
// Recherchiere: Wie vergleicht man auf Gleichheit? (===)

if (tag === 0) {
    // Sonntag
    wochentagName = // Deine Lösung
    wochentagTyp = // "Wochenende"
    motivation = // Deine Lösung
} else if (/* Montag */) {
    // Deine Lösung
} // Füge alle weiteren Tage hinzu (Dienstag bis Samstag)


// TODO 2.4: Gib Wochentag und Motivation aus
console.log(// Deine Lösung);
console.log(// Deine Lösung);


// TODO 2.5: Prüfe, ob Wochenende ist
// Nutze || (OR) Operator: Samstag (6) ODER Sonntag (0)
// Dokumentation logische Operatoren: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Logical_Operators

let istWochenende = // Deine Lösung mit tag === 0 || tag === 6


// TODO 2.6: Gib entsprechende Nachricht aus
if (istWochenende) {
    console.log(// "✓ Es ist Wochenende!");
} else {
    console.log(// "→ Es ist ein Arbeitstag");
}
```

**Recherche-Aufgaben:**
1. Warum startet `.getDay()` bei 0 statt bei 1?
2. Was ist der Unterschied zwischen `==` und `===`?
3. Wie funktioniert der `||` (OR) Operator?

---

### Teil 3: Verschachtelte Bedingungen (20 Min)

Erstelle komplexere Logik mit verschachtelten if-else:

```javascript
// === ARBEITSZEIT-ANALYSE ===

console.log("\n=== ARBEITSZEIT-ANALYSE ===\n");

// TODO 3.1: Implementiere verschachtelte if-else Struktur
// Äussere Bedingung: Ist es ein Arbeitstag? (!istWochenende)
// Innere Bedingungen: Verschiedene Tageszeiten

// Dokumentation ! (NOT) Operator: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Logical_NOT

if (!istWochenende) {
    console.log("Arbeitstag erkannt");
    
    // TODO 3.2: Prüfe auf reguläre Arbeitszeit (08:00 - 17:00)
    if (/* Deine Bedingung */) {
        console.log("→ Reguläre Arbeitszeit (08:00 - 17:00)");
        
        // TODO 3.3: Verschachtelte Bedingung für Mittagspause (12:00 - 13:00)
        if (/* Deine Bedingung */) {
            console.log("   → Mittagspause empfohlen");
        } else {
            console.log("   → Volle Konzentration!");
        }
        
    } else if (/* Feierabend: 17:00 - 20:00 */) {
        // Deine Lösung
    } else {
        // Deine Lösung: Ausserhalb Arbeitszeit
    }
    
} else {
    // TODO 3.4: Wochenend-Logik
    console.log("Wochenende – Erholung oder Hobby-Projekte?");
    
    if (/* Guter Zeitpunkt 09:00 - 22:00 */) {
        // Deine Lösung
    } else {
        // Deine Lösung: Ruhezeit
    }
}
```

**Lernziele:**
- Verschachtelte if-else selbst strukturieren
- NOT-Operator (!) verstehen
- Einrückungen für Lesbarkeit nutzen

---

### Teil 4: Logische Operatoren kombinieren (15 Min)

```javascript
// === KOMPLEXE BEDINGUNGEN ===

console.log("\n=== STATUS-CHECK ===\n");

// TODO 4.1: Erstelle Boolean-Variablen für verschiedene Status
const istAngemeldet = true;
const istAdmin = false;
const hatBerechtigung = true;
const istBetaUser = false;


// TODO 4.2: AND-Verknüpfung (&&)
// Prüfe: istAngemeldet UND hatBerechtigung
// Beide müssen wahr sein für Zugriff

if (/* Deine Bedingung */) {
    console.log("✓ Zugriff erlaubt");
} else {
    console.log("✗ Zugriff verweigert");
}


// TODO 4.3: OR-Verknüpfung (||)
// Prüfe: istAdmin ODER istBetaUser
// Mindestens eine muss wahr sein

if (/* Deine Bedingung */) {
    console.log("✓ Erweiterte Features verfügbar");
} else {
    console.log("→ Standard-Features");
}


// TODO 4.4: Kombination mit Klammern
// Prüfe: istAngemeldet UND (istAdmin ODER hatBerechtigung)
// Klammern steuern die Auswertungsreihenfolge!

if (/* Deine Bedingung */) {
    console.log("✓ Premium-Bereich zugänglich");
} else {
    console.log("✗ Nur öffentlicher Bereich");
}


// TODO 4.5: NOT-Operator (!)
// Kehrt Boolean um: !true wird false, !false wird true

if (/* Prüfe: NICHT Admin */) {
    console.log("→ Kein Admin – eingeschränkte Berechtigungen");
}


// TODO 4.6: Mehrere Bedingungen kombinieren
// istAngemeldet UND hatBerechtigung UND NICHT istAdmin

if (/* Deine Bedingung */) {
    console.log("→ Normaler Benutzer mit Berechtigungen");
}
```

**Wahrheitstabellen zum Nachschlagen:**

```
AND (&&) - Beide müssen wahr sein:
true  && true  = true
true  && false = false
false && false = false

OR (||) - Mindestens eine muss wahr sein:
true  || true  = true
true  || false = true
false || false = false

NOT (!) - Kehrt um:
!true  = false
!false = true
```

---

### Teil 5: Besucher-Tracking mit LocalStorage (25 Min)

```javascript
// === BESUCHER-TRACKING ===

console.log("\n=== BESUCHER-INFO ===\n");

// TODO 5.1: Lade Besuchszahl aus LocalStorage
// Dokumentation: https://developer.mozilla.org/de/docs/Web/API/Window/localStorage
// Methode: localStorage.getItem("schlüssel")

let besuchsZahl = // Deine Lösung: localStorage.getItem(...)


// TODO 5.2: Prüfe, ob es der erste Besuch ist
// Wenn getItem() noch nichts gespeichert hat, gibt es null zurück
// Dokumentation null: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/null

if (besuchsZahl === null) {
    // TODO 5.3: Erster Besuch
    besuchsZahl = // Setze auf 1
    // Speichere mit localStorage.setItem("schlüssel", wert)
    // Deine Lösung:
    
    console.log("🎉 Willkommen zum ersten Mal!");
} else {
    // TODO 5.4: Wiederkehrender Besucher
    // Wandle String in Zahl um (parseInt) und erhöhe um 1
    // Dokumentation parseInt: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/parseInt
    
    besuchsZahl = // Deine Lösung
    // Speichere den neuen Wert
    // Deine Lösung:
    
    console.log(`👋 Willkommen zurück! Besuch Nr. ${besuchsZahl}`);
}


// TODO 5.5: Erstelle unterschiedliche Nachrichten je nach Besuchsanzahl
let besucherStatus = "";

// Nutze if-else-if für verschiedene Bereiche:
// - Genau 1: "Neu hier? Schau dich um!"
// - 2-5: "Schön, dass du wieder da bist!"
// - 6-10: "Du bist jetzt Stammgast!"
// - Über 10: "Wow, du liebst diese Seite! 🏆"

if (/* Deine Bedingung */) {
    besucherStatus = // Deine Lösung
} else if (/* Deine Bedingung */) {
    besucherStatus = // Deine Lösung
} // Weitere Bedingungen...


console.log(`Status: ${besucherStatus}`);


// TODO 5.6: Speichere aktuellen Zeitstempel
// Nutze new Date().toLocaleString("de-CH")
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString

const jetzigerZeitstempel = // Deine Lösung
// Speichere mit localStorage.setItem("letzterBesuch", ...)
// Deine Lösung:


// TODO 5.7: Lade und zeige letzten Besuch an
const letzterBesuch = // Lade aus localStorage
if (letzterBesuch) {
    console.log(`Letzter Besuch: ${letzterBesuch}`);
}
```

**Wichtige Konzepte zum Recherchieren:**
- Was ist LocalStorage und wie funktioniert es?
- Warum brauchen wir `parseInt()`?
- Was bedeutet `=== null`?

---

### Teil 6: Personalisierte Ausgabe im HTML (15 Min)

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

// TODO 6.1: Erstelle HTML-String mit allen Informationen
// Nutze Template Literals für mehrzeiligen String
// Inkludiere: emoji, begruessung, wochentagName, hinweis, besucherStatus, besuchsZahl, letzterBesuch

let htmlAusgabe = `
    <div class="greeting-card">
        <!-- Dein HTML-Code hier -->
        <!-- Beispiel: <h2>${emoji} ${begruessung}!</h2> -->
    </div>
`;


// TODO 6.2: Füge bedingte Zusatz-Infos hinzu
// Verwende += um weiteren HTML-Code anzuhängen

// Bedingung 1: Wenn Wochenende UND zwischen 10:00-20:00
if (/* Deine Bedingung */) {
    htmlAusgabe += `
        <div class="tip-box">
            💡 <strong>Tipp:</strong> Perfekte Zeit für persönliche Projekte!
        </div>
    `;
}

// Bedingung 2: Wenn Arbeitstag UND zwischen 08:00-17:00
else if (/* Deine Bedingung */) {
    htmlAusgabe += `
        <div class="tip-box">
            💼 <strong>Hinweis:</strong> Arbeitszeit – fokussiere dich!
        </div>
    `;
}


// TODO 6.3: Füge HTML in die Seite ein
// Nutze getElementById und innerHTML
// Dokumentation: https://developer.mozilla.org/de/docs/Web/API/Document/getElementById

// Deine Lösung:


console.log("\n✓ Begrüssung im HTML angezeigt");
```

**Selbstständige Aufgaben:**
- Gestalte das HTML mit eigenen Ideen
- Teste verschiedene Tageszeiten (ändere Systemzeit)
- Experimentiere mit weiteren bedingten Ausgaben

---

## Erfolgskriterien

- [ ] Alle TODO-Aufgaben sind selbstständig gelöst
- [ ] Tageszeit-abhängige Begrüssung funktioniert für alle 5 Zeitbereiche
- [ ] Wochentag wird korrekt erkannt (alle 7 Tage implementiert)
- [ ] Wochenende vs. Arbeitstag wird unterschieden
- [ ] Logische Operatoren (`&&`, `||`, `!`) werden korrekt eingesetzt
- [ ] Verschachtelte if-else Strukturen funktionieren
- [ ] Besucher-Zähler mit localStorage funktioniert
- [ ] Unterschiedliche Nachrichten je nach Besuchsanzahl
- [ ] Personalisierte Ausgabe wird im HTML angezeigt
- [ ] Code ist gut eingerückt und lesbar
- [ ] Keine Fehler in der Konsole

---

## Tipps für selbstständiges Arbeiten

- **Teste schrittweise:** Nach jedem TODO testen, ob es funktioniert
- **Konsole ist dein Freund:** Nutze `console.log()` zum Debuggen
- **MDN durchlesen:** Die verlinkten MDN-Artikel enthalten alle nötigen Infos
- **Experimentiere:** Ändere Werte, schau was passiert
- **LocalStorage testen:** `localStorage.clear()` in der Konsole löscht alle Daten
- **Systemzeit ändern:** Teste verschiedene Tageszeiten durch Ändern der Systemuhr

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `==` und `===`?**  
   *Teste: `5 == "5"` vs. `5 === "5"`. Was kommt raus und warum?*

2. **Warum nutzen wir Klammern bei `(tag === 0 || tag === 6)`?**  
   *Was würde ohne Klammern bei `!istWochenende && tag === 0 || tag === 6` passieren?*

3. **Experimentiere: Ändere die Systemzeit deines Computers.**  
   *Wie reagiert die Begrüssung? Funktioniert alles korrekt?*

4. **Was passiert, wenn du `localStorage.clear()` in der Konsole ausführst?**  
   *Teste es und lade die Seite neu. Was siehst du?*

5. **Erstelle eine Bedingung, die nur an Freitagen zwischen 15:00 und 17:00 Uhr wahr ist.**  
   *Schreibe die komplette if-Bedingung auf.*

---

## Weiterführende Links

**Pflichtlektüre für TODO-Aufgaben:**
- [MDN: if...else](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/if...else)
- [MDN: Vergleichsoperatoren](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)
- [MDN: Logische Operatoren](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
- [MDN: Date](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [MDN: LocalStorage](https://developer.mozilla.org/de/docs/Web/API/Window/localStorage)

**Vertiefung:**
- [JavaScript.info: Bedingungen](https://javascript.info/ifelse)
- [JavaScript.info: Logische Operatoren](https://javascript.info/logical-operators)
- [JavaScript.info: LocalStorage](https://javascript.info/localstorage)

**Best Practices:**
- [Clean Code JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
- [Airbnb Style Guide: Comparison Operators](https://github.com/airbnb/javascript#comparison-operators--equality)

---

**Geschätzte Zeit:** 115 Minuten  
**Nächster Schritt:** In Auftrag 3 automatisierst du Wiederholungen mit Schleifen!