# Storyboard: JavaScript Variablen, Datentypen & Kontrollstrukturen

**Video-Titel:** JavaScript Grundlagen – Variablen, Datentypen & Kontrollstrukturen  
**Gesamtdauer:** ca. 12-14 Minuten  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Voraussetzungen:** JavaScript Einbindung & Basics abgeschlossen

---

## Intro (30 Sek.)

### Sprechertext
"Willkommen zurück! Nachdem du JavaScript einbinden kannst, lernst du jetzt die wichtigsten Programmierbausteine kennen: Variablen speichern Werte, Datentypen definieren, was für Werte das sind, und Kontrollstrukturen lassen deinen Code Entscheidungen treffen. Am Ende dieses Videos kannst du deine Portfolio-Seite personalisieren und sie reagiert auf verschiedene Bedingungen. Los geht's!"

### Bildschirmdarstellung
Animierter Title-Screen mit BAND Design (Gradient blau-türkis):
```
JavaScript Grundlagen
─────────────────────
Variablen & Datentypen
Kontrollstrukturen
```

### Hinweise
- BAND Farbschema: #0066CC (blau) → #00C9A7 (türkis)
- Font: Aptos
- Musik: Subtiler Tech-Beat (fade in/out)

---

## Szene 1: Was sind Variablen? (1:30 Min)

### Sprechertext
"Variablen sind Container für Werte – wie beschriftete Schubladen. Du gibst ihnen einen Namen und legst einen Wert hinein. In JavaScript deklarierst du Variablen mit let oder const. let für Werte, die sich ändern können, const für konstante Werte. Schauen wir uns das an."

### Bildschirmdarstellung

**VS Code – neue Datei `variables.js`:**

```javascript
// =====================================================
// VARIABLEN & DATENTYPEN
// =====================================================

console.log("=== VARIABLEN DEMO ===");

// let = veränderbare Variable
let vorname = "Sarah";
console.log("Vorname:", vorname);

vorname = "Max";  // Wert ändern ist erlaubt
console.log("Neuer Vorname:", vorname);

// const = konstante Variable (unveränderbar)
const geburtsjahr = 2006;
console.log("Geburtsjahr:", geburtsjahr);

// geburtsjahr = 2007;  // ❌ Fehler! const kann nicht geändert werden
```

**In der Browser-Konsole zeigen:**
```
=== VARIABLEN DEMO ===
Vorname: Sarah
Neuer Vorname: Max
Geburtsjahr: 2006
```

### Hinweise
- Split-Screen: VS Code links (70%), Browser-Konsole rechts (30%)
- Markiere `let` und `const` farbig
- Zeige versuchte Änderung von `const` mit Fehlermeldung in roter Box
- Text-Overlay: "let = veränderbar | const = konstant"

---

## Szene 2: Datentypen in JavaScript (2 Min)

### Sprechertext
"JavaScript kennt verschiedene Datentypen: String für Text, Number für Zahlen, Boolean für Wahrheitswerte true oder false. JavaScript erkennt den Typ automatisch – du musst ihn nicht explizit angeben wie in anderen Sprachen. Mit typeof kannst du den Datentyp prüfen."

### Bildschirmdarstellung

```javascript
// === DATENTYPEN ===

// 1. STRING (Text) – mit " " oder ' ' oder ` `
let name = "Tim Leibacher";
let beruf = 'Informatiker EFZ';
let nachricht = `Willkommen auf meinem Portfolio!`;

console.log("Name:", name, "– Typ:", typeof name);

// 2. NUMBER (Zahlen)
let alter = 19;
let pi = 3.14159;
let temperatur = -5;

console.log("Alter:", alter, "– Typ:", typeof alter);

// 3. BOOLEAN (Wahrheitswerte)
let istVolljährig = true;
let istRegen = false;

console.log("Volljährig:", istVolljährig, "– Typ:", typeof istVolljährig);

// 4. UNDEFINED (noch kein Wert zugewiesen)
let unbekannt;
console.log("Unbekannt:", unbekannt, "– Typ:", typeof unbekannt);

// 5. NULL (bewusst leerer Wert)
let leer = null;
console.log("Leer:", leer, "– Typ:", typeof leer);
```

**Konsolen-Ausgabe:**
```
Name: Tim Leibacher – Typ: string
Alter: 19 – Typ: number
Volljährig: true – Typ: boolean
Unbekannt: undefined – Typ: undefined
Leer: null – Typ: object
```

### Hinweise
- Farbcodierung: Strings grün, Numbers blau, Booleans orange
- Zeige `typeof` Operator in Aktion
- Text-Overlay mit Icon-Grafiken für jeden Datentyp
- Hinweis einblenden: "typeof null = object ist ein bekannter JS-Bug!"

---

## Szene 3: Template Literals (1 Min)

### Sprechertext
"Template Literals mit Backticks sind super praktisch: Du kannst Variablen direkt in Strings einfügen mit Dollar-Klammer-Syntax. Das ist viel lesbarer als klassische String-Konkatenation mit Pluszeichen."

### Bildschirmdarstellung

```javascript
// === TEMPLATE LITERALS ===

let vorname = "Sarah";
let nachname = "Müller";
let alter = 19;

// Alte Methode (mit +)
console.log("Hallo, ich bin " + vorname + " " + nachname + " und bin " + alter + " Jahre alt.");

// Neue Methode (Template Literal)
console.log(`Hallo, ich bin ${vorname} ${nachname} und bin ${alter} Jahre alt.`);

// Mehrzeilige Strings
let nachricht = `
Willkommen auf meinem Portfolio!
Mein Name ist ${vorname} ${nachname}.
Ich bin ${alter} Jahre alt.
`;

console.log(nachricht);
```

### Hinweise
- Vergleich: Alte vs. neue Syntax nebeneinander
- Backticks ` ` hervorheben
- `${}` Platzhalter animiert pulsieren lassen
- Text-Overlay: "Template Literals = Lesbar & Praktisch"

---

## Szene 4: Operatoren (1:30 Min)

### Sprechertext
"Operatoren führen Berechnungen oder Vergleiche durch. Rechenoperatoren kennst du: Plus, Minus, Mal, Geteilt. Vergleichsoperatoren prüfen Bedingungen: Ist etwas gleich, grösser oder kleiner? Wichtig: Drei Gleichheitszeichen für strikten Vergleich ohne automatische Typ-Umwandlung."

### Bildschirmdarstellung

```javascript
// === RECHENOPERATOREN ===

let a = 10;
let b = 3;

console.log("Addition:", a + b);        // 13
console.log("Subtraktion:", a - b);     // 7
console.log("Multiplikation:", a * b);  // 30
console.log("Division:", a / b);        // 3.333...
console.log("Rest (Modulo):", a % b);   // 1
console.log("Potenz:", a ** b);         // 1000

// === VERGLEICHSOPERATOREN ===

let x = 5;
let y = "5";

console.log("x == y:", x == y);    // true (Wert-Vergleich)
console.log("x === y:", x === y);  // false (Typ + Wert-Vergleich)
console.log("x != y:", x != y);    // false
console.log("x !== y:", x !== y);  // true

console.log("10 > 5:", 10 > 5);    // true
console.log("10 < 5:", 10 < 5);    // false
console.log("10 >= 10:", 10 >= 10); // true
```

### Hinweise
- Tabelle einblenden mit Operatoren-Übersicht
- `==` vs `===` farblich unterscheiden (rot vs. grün)
- Warnung einblenden: "Nutze immer ===, nicht =="
- Animation: Berechnungen Schritt für Schritt zeigen

---

## Szene 5: If-Else Verzweigungen (2 Min)

### Sprechertext
"Mit if-else trifft dein Code Entscheidungen. Wenn eine Bedingung wahr ist, wird der Code im if-Block ausgeführt, sonst der im else-Block. Mit else if kannst du mehrere Bedingungen nacheinander prüfen. So wird deine Website intelligent."

### Bildschirmdarstellung

```javascript
// === IF-ELSE VERZWEIGUNGEN ===

let alter = 19;

if (alter >= 18) {
    console.log("✓ Du bist volljährig");
} else {
    console.log("✗ Du bist minderjährig");
}

// === MEHRFACHE BEDINGUNGEN (else if) ===

let note = 5.2;

if (note >= 5.5) {
    console.log("Sehr gut!");
} else if (note >= 5.0) {
    console.log("Gut");
} else if (note >= 4.5) {
    console.log("Genügend");
} else if (note >= 4.0) {
    console.log("Ungenügend");
} else {
    console.log("Sehr schwach");
}

// === VERSCHACHTELTE BEDINGUNGEN ===

let istAngemeldet = true;
let istAdmin = false;

if (istAngemeldet) {
    console.log("Benutzer ist angemeldet");
    
    if (istAdmin) {
        console.log("→ Admin-Bereich verfügbar");
    } else {
        console.log("→ Standard-Bereich verfügbar");
    }
} else {
    console.log("Bitte anmelden");
}
```

**Konsolen-Ausgabe:**
```
✓ Du bist volljährig
Gut
Benutzer ist angemeldet
→ Standard-Bereich verfügbar
```

### Hinweise
- Flowchart-Animation: Bedingung → wahr/falsch → Ausführung
- Code-Blöcke farbig hervorheben (grün = ausgeführt, grau = übersprungen)
- Text-Overlay: "if = Entscheidung | else = Alternative"

---

## Szene 6: Logische Operatoren (1:30 Min)

### Sprechertext
"Logische Operatoren verbinden mehrere Bedingungen. AND mit zwei Ampersands bedeutet: Beide Bedingungen müssen wahr sein. OR mit zwei senkrechten Strichen: Mindestens eine Bedingung muss wahr sein. NOT mit Ausrufezeichen kehrt den Wahrheitswert um."

### Bildschirmdarstellung

```javascript
// === LOGISCHE OPERATOREN ===

let alter = 19;
let hatFührerschein = true;
let istMüde = false;

// && (AND) – Beide Bedingungen müssen wahr sein
if (alter >= 18 && hatFührerschein) {
    console.log("✓ Du darfst Auto fahren");
}

// || (OR) – Mindestens eine Bedingung muss wahr sein
let istWochenende = false;
let istFeiertag = true;

if (istWochenende || istFeiertag) {
    console.log("✓ Frei heute!");
}

// ! (NOT) – Kehrt Wahrheitswert um
if (!istMüde) {
    console.log("✓ Bereit für Coding!");
}

// === KOMPLEXE BEDINGUNGEN ===

let stunde = 14;
let istSchultag = true;

if ((stunde >= 8 && stunde < 17) && istSchultag) {
    console.log("Unterricht läuft");
} else {
    console.log("Freizeit!");
}
```

**Wahrheitstabellen einblenden:**
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

### Hinweise
- Wahrheitstabelle als Pop-up einblenden
- Logik-Gatter-Animation (UND/ODER/NICHT)
- Klammern farbig markieren bei komplexen Bedingungen

---

## Szene 7: For-Schleifen (2 Min)

### Sprechertext
"Schleifen wiederholen Code automatisch. Die for-Schleife ist perfekt, wenn du genau weisst, wie oft etwas wiederholt werden soll. Sie hat drei Teile: Initialisierung, Bedingung, Inkrement. Der Code im Schleifenkörper läuft so lange, bis die Bedingung falsch wird."

### Bildschirmdarstellung

```javascript
// === FOR-SCHLEIFE ===

console.log("=== ZAHLEN VON 1 BIS 10 ===");

for (let i = 1; i <= 10; i++) {
    console.log(i);
}

// === EIGENEN NAMEN AUSGEBEN ===

console.log("\n=== MEIN NAME 5 MAL ===");

let name = "Tim";

for (let i = 1; i <= 5; i++) {
    console.log(`${i}. ${name}`);
}

// === SUMME BERECHNEN ===

console.log("\n=== SUMME VON 1 BIS 100 ===");

let summe = 0;

for (let i = 1; i <= 100; i++) {
    summe = summe + i;  // oder: summe += i;
}

console.log("Summe:", summe);  // 5050

// === GERADE ZAHLEN ===

console.log("\n=== GERADE ZAHLEN BIS 20 ===");

for (let i = 0; i <= 20; i += 2) {
    console.log(i);
}

// === COUNTDOWN ===

console.log("\n=== COUNTDOWN ===");

for (let i = 10; i >= 1; i--) {
    console.log(i);
}
console.log("Start! 🚀");
```

### Hinweise
- Animation: Schleife durchlaufen mit Zähler-Visualisierung
- `i` Variable farbig highlighten
- Zeige Ausgabe Live in Konsole (scrollt mit)
- Text-Overlay: "Initialisierung | Bedingung | Inkrement"
- Flowchart der Schleife einblenden

---

## Szene 8: While-Schleifen (1:30 Min)

### Sprechertext
"Die while-Schleife läuft, solange eine Bedingung wahr ist. Sie ist flexibler als for, weil du vorher nicht wissen musst, wie oft sie läuft. Perfekt für Situationen wie: Wiederhole, bis der Benutzer die richtige Eingabe macht."

### Bildschirmdarstellung

```javascript
// === WHILE-SCHLEIFE ===

console.log("=== ZAHLEN MIT WHILE ===");

let zahl = 1;

while (zahl <= 5) {
    console.log(zahl);
    zahl++;  // Wichtig! Sonst Endlosschleife
}

// === PRAKTISCHES BEISPIEL: MÜNZWURF ===

console.log("\n=== MÜNZWURF BIS KOPF ===");

let wurf = 0;
let ergebnis = "";

while (ergebnis !== "Kopf") {
    wurf++;
    ergebnis = Math.random() < 0.5 ? "Kopf" : "Zahl";
    console.log(`Wurf ${wurf}: ${ergebnis}`);
}

console.log(`✓ Kopf nach ${wurf} Würfen!`);

// === DO-WHILE (läuft mindestens 1x) ===

console.log("\n=== DO-WHILE DEMO ===");

let x = 10;

do {
    console.log("Läuft mindestens 1x:", x);
    x++;
} while (x < 5);  // Bedingung ist false, aber läuft trotzdem 1x
```

### Hinweise
- Zeige Endlosschleifen-Warnung (Animation: unendliches Symbol)
- While vs. For Vergleich einblenden
- Math.random() Münzwurf animiert darstellen
- Text-Overlay: "while = Bedingung prüfen → ausführen"

---

## Szene 9: Praxis-Beispiel – Interaktive Begrüssung (2 Min)

### Sprechertext
"Kombinieren wir jetzt alles! Wir erstellen eine intelligente Begrüssung für dein Portfolio: Sie passt sich der Tageszeit an, zeigt dein Alter berechnet aus deinem Geburtsjahr und zählt, wie oft die Seite besucht wurde. Das ist echte Programmlogik in Aktion!"

### Bildschirmdarstellung

**Neue Datei: `portfolio-logic.js`**

```javascript
// =====================================================
// PORTFOLIO-LOGIK MIT VARIABLEN & KONTROLLSTRUKTUREN
// =====================================================

console.log("=== PORTFOLIO GELADEN ===");

// === PERSÖNLICHE DATEN ===

const vorname = "Tim";
const nachname = "Leibacher";
const geburtsjahr = 2006;

// Alter berechnen
const aktuellesJahr = new Date().getFullYear();
const alter = aktuellesJahr - geburtsjahr;

console.log(`Name: ${vorname} ${nachname}`);
console.log(`Alter: ${alter} Jahre`);

// === TAGESZEIT-ABHÄNGIGe BEGRÜSSUNG ===

const jetzt = new Date();
const stunde = jetzt.getHours();

let begruessung = "";
let emoji = "";

if (stunde >= 5 && stunde < 12) {
    begruessung = "Guten Morgen";
    emoji = "☀️";
} else if (stunde >= 12 && stunde < 18) {
    begruessung = "Guten Tag";
    emoji = "🌤️";
} else if (stunde >= 18 && stunde < 22) {
    begruessung = "Guten Abend";
    emoji = "🌆";
} else {
    begruessung = "Gute Nacht";
    emoji = "🌙";
}

console.log(`\n${emoji} ${begruessung}!`);

// === BESUCHER-ZÄHLER ===

let besuche = localStorage.getItem("besuchsZahl") || 0;
besuche = parseInt(besuche) + 1;
localStorage.setItem("besuchsZahl", besuche);

console.log(`Du bist heute zum ${besuche}. Mal hier!`);

// === SKILLS AUSGEBEN (mit Schleife) ===

console.log("\n=== MEINE SKILLS ===");

const skills = ["HTML", "CSS", "JavaScript", "Git"];

for (let i = 0; i < skills.length; i++) {
    console.log(`${i + 1}. ${skills[i]}`);
}

// === IM HTML ANZEIGEN ===

document.getElementById("portfolio-begruessung").innerHTML = `
    ${emoji} ${begruessung}, ${vorname}!<br>
    <small>Du bist ${alter} Jahre alt und besuchst diese Seite zum ${besuche}. Mal.</small>
`;
```

**HTML-Anpassung zeigen:**

```html
<div id="portfolio-begruessung">
    <!-- Wird von JavaScript gefüllt -->
</div>
```

**Live-Resultat im Browser:**
```
🌤️ Guten Tag, Tim!
Du bist 19 Jahre alt und besuchst diese Seite zum 3. Mal.
```

### Hinweise
- Split-Screen: Code + Live-Resultat
- Schritt-für-Schritt-Durchlauf mit Markierungen
- Variablenwerte einblenden während Ausführung
- Text-Overlay: "Variablen + Bedingungen + Schleifen = Intelligente Website"

---

## Szene 10: Häufige Fehler & Debugging (1:30 Min)

### Sprechertext
"Beim Programmieren machst du Fehler – das ist normal! Die häufigsten: Falsche Variablentypen, fehlende geschweifte Klammern, Endlosschleifen. Die Konsole zeigt dir genau, wo der Fehler ist. Nutze console.log() um Variablenwerte zu prüfen – das ist Debugging Nummer eins."

### Bildschirmdarstellung

**Fehler 1: let vs. const verwechselt**

```javascript
const name = "Sarah";
name = "Tim";  // ❌ TypeError: Assignment to constant variable
```

**Konsole zeigt:**
```
Uncaught TypeError: Assignment to constant variable.
    at script.js:2
```

**Fehler 2: Vergessene geschweifte Klammer**

```javascript
if (alter >= 18) {
    console.log("Volljährig");
// ❌ Fehler: Schliessende Klammer fehlt!
```

**Fehler 3: Endlosschleife**

```javascript
let i = 0;
while (i < 10) {
    console.log(i);
    // ❌ Fehler: i++ fehlt → Endlosschleife!
}
```

**Debugging-Tipp:**

```javascript
// Variablenwerte während der Ausführung prüfen
let summe = 0;
for (let i = 1; i <= 5; i++) {
    summe += i;
    console.log(`i = ${i}, summe = ${summe}`);  // Debug-Ausgabe
}
```

### Hinweise
- Zeige jeden Fehler mit roter Fehlermeldung
- Korrekte Version daneben zeigen (Vorher/Nachher)
- Endlosschleifen-Animation mit "STOP" Button
- Text-Overlay: "console.log() = dein bester Freund beim Debuggen"

---

## Szene 11: Zusammenfassung & Ausblick (1 Min)

### Sprechertext
"Fassen wir zusammen: Mit let und const speicherst du Werte. Datentypen wie String, Number und Boolean strukturieren deine Daten. If-else lässt deinen Code Entscheidungen treffen, Schleifen automatisieren Wiederholungen. Logische Operatoren verbinden Bedingungen. Das sind die Bausteine jeder Programmlogik! In den Aufträgen baust du jetzt eine intelligente Portfolio-Seite mit personalisierten Inhalten. Im nächsten Video geht's um Event Handling – dann wird deine Seite richtig interaktiv!"

### Bildschirmdarstellung

Animierte Checkliste:

```
✓ Variablen (let, const)
✓ Datentypen (String, Number, Boolean)
✓ Template Literals (`${}`)
✓ Operatoren (===, &&, ||)
✓ if-else Verzweigungen
✓ for & while Schleifen
✓ Debugging mit console.log()
```

**Projekt-Vorschau zeigen:**
```
mein-portfolio/
├── index.html
├── styles.css
├── script.js
├── variables.js
└── portfolio-logic.js
```

### Hinweise
- BAND Design Gradient-Hintergrund
- Punkte nacheinander einblenden mit Animation
- Outro-Musik fade in
- Call-to-Action einblenden: "Jetzt Aufträge lösen!"

---

## Zusatzmaterialien für Video-Produktion

### Demo-Dateien zum Mitschneiden

**variables.js (Vollständig)**
```javascript
// =====================================================
// VARIABLEN & DATENTYPEN
// =====================================================

console.log("=== VARIABLEN DEMO ===");

// let = veränderbare Variable
let vorname = "Sarah";
console.log("Vorname:", vorname);

vorname = "Max";
console.log("Neuer Vorname:", vorname);

// const = konstante Variable
const geburtsjahr = 2006;
console.log("Geburtsjahr:", geburtsjahr);

// === DATENTYPEN ===

let name = "Tim Leibacher";
let alter = 19;
let istVolljährig = true;
let unbekannt;
let leer = null;

console.log("Name:", name, "– Typ:", typeof name);
console.log("Alter:", alter, "– Typ:", typeof alter);
console.log("Volljährig:", istVolljährig, "– Typ:", typeof istVolljährig);
console.log("Unbekannt:", unbekannt, "– Typ:", typeof unbekannt);
console.log("Leer:", leer, "– Typ:", typeof leer);

// === TEMPLATE LITERALS ===

console.log(`Hallo, ich bin ${name} und bin ${alter} Jahre alt.`);

// === OPERATOREN ===

let a = 10;
let b = 3;

console.log("Addition:", a + b);
console.log("Subtraktion:", a - b);
console.log("Multiplikation:", a * b);
console.log("Division:", a / b);
console.log("Rest:", a % b);

let x = 5;
let y = "5";

console.log("x == y:", x == y);
console.log("x === y:", x === y);

// === IF-ELSE ===

let note = 5.2;

if (note >= 5.5) {
    console.log("Sehr gut!");
} else if (note >= 5.0) {
    console.log("Gut");
} else if (note >= 4.5) {
    console.log("Genügend");
} else {
    console.log("Ungenügend");
}

// === LOGISCHE OPERATOREN ===

let hatFührerschein = true;
let ist18 = true;

if (ist18 && hatFührerschein) {
    console.log("Darf Auto fahren");
}

// === FOR-SCHLEIFE ===

console.log("\n=== ZAHLEN 1-10 ===");

for (let i = 1; i <= 10; i++) {
    console.log(i);
}

// === WHILE-SCHLEIFE ===

console.log("\n=== COUNTDOWN ===");

let countdown = 5;

while (countdown > 0) {
    console.log(countdown);
    countdown--;
}
console.log("Start!");
```

---

### Grafiken für Video

**Operatoren-Übersicht (einblenden als Tabelle):**

| Operator | Bedeutung | Beispiel | Ergebnis |
|----------|-----------|----------|----------|
| + | Addition | 5 + 3 | 8 |
| - | Subtraktion | 5 - 3 | 2 |
| * | Multiplikation | 5 * 3 | 15 |
| / | Division | 15 / 3 | 5 |
| % | Rest (Modulo) | 10 % 3 | 1 |
| ** | Potenz | 2 ** 3 | 8 |
| === | Strikte Gleichheit | 5 === "5" | false |
| !== | Strikte Ungleichheit | 5 !== "5" | true |
| > | Grösser als | 5 > 3 | true |
| < | Kleiner als | 5 < 3 | false |
| >= | Grösser oder gleich | 5 >= 5 | true |
| <= | Kleiner oder gleich | 3 <= 5 | true |
| && | Logisches UND | true && false | false |
| \|\| | Logisches ODER | true \|\| false | true |
| ! | Logisches NICHT | !true | false |

---

### Animationen

**Schleifendurchlauf-Visualisierung:**
```
for (let i = 1; i <= 3; i++) {
    console.log(i);
}

Durchlauf 1: i = 1 → Bedingung true → Ausgabe: 1 → i++
Durchlauf 2: i = 2 → Bedingung true → Ausgabe: 2 → i++
Durchlauf 3: i = 3 → Bedingung true → Ausgabe: 3 → i++
Durchlauf 4: i = 4 → Bedingung false → Schleife endet
```

**Flowchart if-else:**
```
┌─────────────┐
│ if-Bedingung│
└──────┬──────┘
       │
   ┌───┴───┐
   │       │
  wahr   falsch
   │       │
   ▼       ▼
┌──────┐ ┌──────┐
│if    │ │else  │
│Block │ │Block │
└──────┘ └──────┘
```

---

## Technische Anforderungen

**Bildschirmauflösung:** 1920x1080  
**Framerate:** 30 FPS  
**Font:** Aptos (BAND Corporate Design)  
**Farbschema:** 
- Primär: #0066CC (Blau)
- Sekundär: #00C9A7 (Türkis)
- Akzent: #FF6B35 (Orange)
- Hintergrund: Gradient blau → türkis

**Code-Editor:** VS Code mit Theme "Dark+"  
**Browser:** Chrome oder Firefox mit DevTools  
**Musik:** Subtle Tech Beat (non-intrusive, ca. 90 BPM)

---

## Checkliste für Produktion

- [ ] Alle Code-Beispiele funktionieren fehlerfrei
- [ ] variables.js und portfolio-logic.js vorbereitet
- [ ] Browser-Konsole voreingestellt (F12)
- [ ] Animationen für Schleifen und Flowcharts bereit
- [ ] BAND Design Intro/Outro erstellt
- [ ] Tabellen und Grafiken als Overlays vorbereitet
- [ ] Mikrofon-Test durchgeführt
- [ ] Bildschirm-Aufnahme-Software konfiguriert
- [ ] Backup der Demo-Dateien erstellt

---

**Gesamtdauer:** ca. 12-14 Minuten  
**Schwierigkeitsgrad:** Anfänger  
**Nächstes Video:** Event Handling & DOM Interaktion
