# Auftrag 1: Persönliche Daten mit Variablen

## Ziel

Du lernst, mit Variablen zu arbeiten, verschiedene Datentypen zu unterscheiden und Template Literals für formatierte Ausgaben zu nutzen. Deine persönlichen Portfolio-Daten werden strukturiert gespeichert und ausgegeben.

## Beschreibung

Variablen sind wie beschriftete Schubladen – sie speichern Werte, auf die du später zugreifen kannst. In diesem Auftrag erstellst du ein persönliches Datenprofil für dein Portfolio mit let und const, nutzt verschiedene Datentypen und gibst alles formatiert in der Konsole aus.

---

### Teil 1: Grundlegende persönliche Daten (15 Min)

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

// TODO 1.1: Erstelle Variablen für deinen Vornamen, Nachnamen und Geburtsjahr
// Nutze 'const' für Werte, die sich nicht ändern
// Beispiel: const vorname = "...";

// Deine Lösung hier:


// TODO 1.2: Erstelle Variablen für deine E-Mail und Telefonnummer
// Nutze 'let' für Werte, die sich ändern können

// Deine Lösung hier:


// TODO 1.3: Erstelle Variablen für deinen Beruf, Lehrjahr und Lehrbetrieb
// Überlege: Welche sollten const sein, welche let?

// Deine Lösung hier:


// TODO 1.4: Gib alle Variablen mit Template Literals aus
// Syntax: console.log(`Text ${variable} mehr Text`);
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals

// Deine Lösung hier:

```

**Selbstständige Aufgabe:**
- Recherchiere auf MDN, wie Template Literals funktionieren
- Überlege bei jeder Variable: const oder let?
- Teste deine Ausgaben in der Browser-Konsole (F12)

**Hilfreiche Links:**
- [MDN: let](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/let)
- [MDN: const](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/const)
- [MDN: Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)

---

### Teil 2: Berechnungen mit Variablen (15 Min)

Erweitere `personal-data.js` mit Berechnungen:

```javascript
// === BERECHNUNGEN ===

console.log("\n=== BERECHNUNGEN ===\n");

// TODO 2.1: Hole das aktuelle Jahr
// Tipp: Nutze new Date().getFullYear()
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear

const aktuellesJahr = // Deine Lösung hier


// TODO 2.2: Berechne dein Alter aus Geburtsjahr und aktuellem Jahr
// Formel: alter = aktuellesJahr - geburtsjahr

const alter = // Deine Lösung hier


// TODO 2.3: Gib aktuelles Jahr und Alter aus
console.log(`Aktuelles Jahr: ${aktuellesJahr}`);
// Deine console.log Ausgabe für Alter hier:


// TODO 2.4: Erstelle eine Variable 'lehrzeit' mit Wert 4 (Jahre)
// Berechne die verbleibenden Lehrjahre: lehrzeit - lehrjahr

// Deine Lösung hier:


// TODO 2.5: Berechne dein Lehrabschluss-Jahr
// Wenn du z.B. 2025 gestartet hast und 4 Jahre Lehrzeit hast:
// abschlussJahr = startJahr + lehrzeit

// Deine Lösung hier:


// TODO 2.6: Berechne deinen prozentualen Fortschritt
// Formel: (lehrjahr / lehrzeit) * 100
// Dokumentation Mathematische Operatoren: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators

// Deine Lösung hier:


// Gib alle berechneten Werte aus
```

**Lernziel:** Du sollst selbst herausfinden, wie man Berechnungen durchführt und Variablen kombiniert.

---

### Teil 3: Verschiedene Datentypen (20 Min)

Ergänze verschiedene Datentypen und prüfe sie mit `typeof`:

```javascript
// === DATENTYPEN ===

console.log("\n=== DATENTYPEN ===\n");

// TODO 3.1: Erstelle String-Variablen für Stadt und Postleitzahl
// Wichtig: Postleitzahl als String (wegen führenden Nullen!)

// Deine Lösung hier:


// TODO 3.2: Erstelle Number-Variablen
// - anzahlProjekte (Ganzzahl)
// - durchschnittsNote (Dezimalzahl)
// - temperatur (kann auch negativ sein)

// Deine Lösung hier:


// TODO 3.3: Erstelle Boolean-Variablen
// - istVolljährig: Prüfe ob alter >= 18
// - hatFührerschein: true oder false
// - sprichtEnglisch: true oder false
// Dokumentation Boolean: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Boolean

// Deine Lösung hier:


// TODO 3.4: Erstelle Arrays (Listen)
// - hobbies: Array mit mindestens 3 Hobbies als Strings
// - lieblingszahlen: Array mit mindestens 3 Zahlen
// Syntax: let arrayName = [wert1, wert2, wert3];
// Dokumentation Arrays: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array

// Deine Lösung hier:


// TODO 3.5: Gib alle Variablen MIT ihrem Typ aus
// Nutze typeof: console.log(`Variable: ${variable} (Typ: ${typeof variable})`);
// Für Arrays zusätzlich: Array.isArray(variable)

// Deine Lösung hier:

```

**Recherche-Aufgaben:**
1. Warum sollte Postleitzahl ein String sein? (Tipp: Was passiert mit 0800 als Number?)
2. Wie erstellt man ein Array? Schau auf MDN nach!
3. Warum zeigt `typeof` für Arrays "object"? Wie prüft man richtig auf Arrays?

---

### Teil 4: Strukturierte Ausgabe (15 Min)

Erstelle eine übersichtliche, formatierte Ausgabe:

```javascript
// === STRUKTURIERTE AUSGABE ===

// TODO 4.1: Erstelle eine Trennlinie mit 50 Gleichheitszeichen
// Tipp: Nutze "=".repeat(50)
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/String/repeat

console.log("\n" + /* Deine Lösung */);
console.log("PORTFOLIO – PERSÖNLICHE DATEN");
console.log(/* Trennlinie wiederholen */);

// TODO 4.2: Gib deine persönlichen Informationen formatiert aus
// Nutze Einrückungen mit Leerzeichen für bessere Lesbarkeit
console.log("\n📋 PERSÖNLICHE INFORMATIONEN");
console.log("─".repeat(50));
// Deine console.log Ausgaben hier (Name, Geburtsjahr, Alter, Wohnort):


// TODO 4.3: Gib berufliche Informationen aus
console.log("\n💼 BERUFLICHES");
console.log("─".repeat(50));
// Deine console.log Ausgaben hier (Beruf, Lehrjahr, Lehrbetrieb, Fortschritt, Abschluss):


// TODO 4.4: Gib Kontaktdaten aus
console.log("\n📞 KONTAKT");
console.log("─".repeat(50));
// Deine console.log Ausgaben hier:


// TODO 4.5: Gib Hobbies als nummerierte Liste aus
// Nutze eine for-Schleife: for (let i = 0; i < hobbies.length; i++)
// Dokumentation for-Schleife: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/for
console.log("\n🎯 HOBBIES");
console.log("─".repeat(50));
// Deine for-Schleife hier:


// TODO 4.6: Gib Status-Informationen aus mit Ternärem Operator
// Syntax: bedingung ? "Ja" : "Nein"
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Conditional_Operator
console.log("\n✓ STATUS");
console.log("─".repeat(50));
console.log(`   Volljährig:      ${istVolljährig ? "Ja" : "Nein"}`);
// Weitere Status-Ausgaben hier:


console.log("\n" + "=".repeat(50));
```

**Lernziele:**
- Selbst eine for-Schleife schreiben (mit MDN-Hilfe)
- Ternären Operator verstehen und anwenden
- String-Methoden wie `.repeat()` nutzen

---

### Teil 5: Daten im HTML anzeigen (10 Min)

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

// TODO 5.1: Erstelle HTML-Content mit Template Literals
// Nutze innerHTML um den Content ins div#profil-daten einzufügen
// Dokumentation innerHTML: https://developer.mozilla.org/de/docs/Web/API/Element/innerHTML
// Dokumentation Array.join(): https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/join

// TODO 5.2: Hole das Element mit getElementById
const profilContainer = // Deine Lösung hier


// TODO 5.3: Erstelle HTML-Content als String
// Inkludiere: Name, Alter, Beruf, Lehrjahr, Wohnort, Hobbies, E-Mail
// Tipp: Hobbies mit hobbies.join(", ") als kommagetrennten String ausgeben
// Tipp: E-Mail als Link mit <a href="mailto:${email}">${email}</a>

profilContainer.innerHTML = `
    <div class="profil-card">
        <!-- Dein HTML-Code hier -->
    </div>
`;
```

**Selbstständige Aufgaben:**
- Recherchiere, wie `getElementById` funktioniert
- Lerne, wie man Arrays mit `.join()` zu einem String verbindet
- Verstehe, wie `innerHTML` HTML-Code einfügt

---

## Erfolgskriterien

- [ ] Alle TODO-Aufgaben sind selbstständig gelöst
- [ ] Mindestens 8 verschiedene Variablen sind deklariert
- [ ] `const` wird für unveränderliche Werte genutzt, `let` für veränderliche
- [ ] Mindestens 3 verschiedene Datentypen werden verwendet
- [ ] Template Literals mit `${}` werden für formatierte Ausgaben genutzt
- [ ] Alter wird korrekt aus Geburtsjahr berechnet
- [ ] Prozentuale Fortschrittsberechnung funktioniert
- [ ] `typeof` wird genutzt, um Datentypen zu prüfen
- [ ] For-Schleife für Hobbies funktioniert
- [ ] Ternärer Operator wird für Status verwendet
- [ ] Daten werden im HTML angezeigt
- [ ] Keine Fehler in der Konsole

---

## Tipps für selbstständiges Arbeiten

- **MDN ist dein Freund:** Bei jeder Frage zuerst auf MDN nachschlagen
- **Konsole nutzen:** Teste einzelne Code-Zeilen direkt in der Browser-Konsole
- **Kleine Schritte:** Teste nach jedem TODO, ob es funktioniert
- **Fehler lesen:** Fehlermeldungen in der Konsole genau lesen – sie sagen dir meist, was falsch ist
- **Kommentare:** Schreibe Kommentare zu deinem Code, um dein Verständnis zu festigen

---

## Reflexionsfragen

1. **Was passiert, wenn du versuchst, eine `const` Variable zu ändern?**  
   *Teste es: Erstelle `const name = "Max"` und versuche dann `name = "Tim"`. Was zeigt die Konsole?*

2. **Warum sollte Postleitzahl als String und nicht als Number gespeichert werden?**  
   *Teste: Was passiert mit `let plz = 0800;`? Welcher Wert wird gespeichert?*

3. **Was ist der Unterschied zwischen diesen Ausgaben?**
   ```javascript
   console.log("Alter: " + alter);           // String-Konkatenation
   console.log(`Alter: ${alter}`);           // Template Literal
   ```
   *Welche Methode ist lesbarer bei vielen Variablen?*

4. **Experimentiere: Was gibt `typeof null` zurück?**  
   *Ist das korrekt? Recherchiere, warum JavaScript hier ein bekanntes "Bug" hat.*

5. **Erstelle eine Variable `let zahl = "42"`. Was ist ihr Typ?**  
   *Wie kannst du sie in eine echte Number umwandeln? Recherchiere `parseInt()` und `Number()`*

---

## Weiterführende Links

**Pflichtlektüre für TODO-Aufgaben:**
- [MDN: Variablen](https://developer.mozilla.org/de/docs/Learn/JavaScript/First_steps/Variables)
- [MDN: Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)
- [MDN: typeof](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/typeof)
- [MDN: for-Schleife](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/for)
- [MDN: Ternärer Operator](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

**Vertiefung:**
- [JavaScript.info: Datentypen](https://javascript.info/types)
- [JavaScript.info: Variables](https://javascript.info/variables)
- [W3Schools: JS Data Types](https://www.w3schools.com/js/js_datatypes.asp)

**Best Practices:**
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

---

**Geschätzte Zeit:** 75 Minuten  
**Nächster Schritt:** In Auftrag 2 nutzt du if-else Verzweigungen, um auf Bedingungen zu reagieren!