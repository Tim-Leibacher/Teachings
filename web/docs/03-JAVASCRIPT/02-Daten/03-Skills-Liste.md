# Auftrag 3: Skills-Liste mit Schleifen

## Ziel

Du lernst, mit for- und while-Schleifen zu arbeiten, um wiederholende Aufgaben zu automatisieren. Deine Portfolio-Seite zeigt eine interaktive Skills-Liste, die automatisch generiert wird, und nutzt Schleifen für Berechnungen und Animationen.

## Beschreibung

Schleifen sind das Werkzeug, um Code zu wiederholen, ohne ihn hundertmal zu schreiben. Mit for-Schleifen automatisierst du Listen, Berechnungen und Animationen. While-Schleifen laufen, solange eine Bedingung wahr ist. In diesem Auftrag erstellst du eine dynamische Skills-Liste für dein Portfolio mit Fortschrittsbalken, Statistiken und automatisierten Ausgaben.

---

### Teil 1: Skills-Array und einfache for-Schleife (20 Min)

Erstelle eine neue Datei **`skills.js`** und binde sie ein:

```html
<script src="script.js"></script>
<script src="personal-data.js"></script>
<script src="greeting.js"></script>
<script src="skills.js"></script>
```

**In `skills.js`:**

```javascript
// =====================================================
// SKILLS-VERWALTUNG
// =====================================================

console.log("=== MEINE SKILLS ===\n");

// TODO 1.1: Erstelle ein Array mit mindestens 7 Skills
// Beispiele: "HTML", "CSS", "JavaScript", "Git", "VS Code", "Debugging", "Problemlösung"
// Dokumentation Arrays: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array

const skills = // Deine Lösung hier: [...]


// TODO 1.2: Gib die Anzahl der Skills aus
// Nutze die .length Eigenschaft von Arrays
// Dokumentation: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/length

console.log(// Deine Lösung: `Ich habe ${...} Skills:`);


// TODO 1.3: Erstelle eine for-Schleife, die alle Skills nummeriert ausgibt
// Format: "1. HTML", "2. CSS", etc.
// Standard-Muster: for (let i = 0; i < array.length; i++)
// Dokumentation for-Schleife: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/for

// Deine for-Schleife hier:


console.log("\n");


// TODO 1.4: Erstelle eine zweite for-Schleife mit Emojis
// Erstelle eine Variable skillEmoji = "⭐"
// Gib jeden Skill mit dem Emoji aus: "⭐ HTML"

const skillEmoji = // Deine Lösung

// Deine for-Schleife hier:

```

**Lernziele:**
- Arrays selbst erstellen und verstehen
- `.length` Eigenschaft nutzen
- For-Schleife selbst schreiben (wichtigstes Muster!)
- Array-Zugriff mit Index `array[i]` verstehen

**Wichtige Konzepte zum Recherchieren:**
- Warum startet `i` bei 0 und nicht bei 1?
- Was ist ein Array-Index?
- Wie greife ich auf ein Element zu?

---

### Teil 2: Skills mit Fortschritt (25 Min)

Erweitere die Skills mit Fortschrittsinformationen:

```javascript
// === SKILLS MIT FORTSCHRITT ===

console.log("\n=== SKILLS MIT FORTSCHRITT ===\n");

// TODO 2.1: Erstelle ein Array von Objekten mit Skills und Fortschritt
// Jedes Objekt hat: { name: "HTML", level: 85 }
// Level ist eine Zahl zwischen 0-100 (Prozent)
// Dokumentation Objekte: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object

const skillsDetailed = [
    { name: "HTML", level: 85 },
    // Füge hier mindestens 6 weitere Skills hinzu
    // Deine Lösung hier:
    
];


// TODO 2.2: Durchlaufe alle Skills mit einer for-Schleife
// Für jeden Skill: Extrahiere name und level in Variablen

for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    const name = // Deine Lösung: skill.name
    const level = // Deine Lösung: skill.level
    
    
    // TODO 2.3: Erstelle einen Fortschrittsbalken mit verschachtelter Schleife
    // Balken hat 10 Zeichen: █ für gefüllt, ░ für leer
    // Beispiel: Bei 85% → 8.5 ≈ 9 gefüllte Zeichen
    // Nutze Math.round(level / 10) für Anzahl gefüllte Zeichen
    // Dokumentation Math.round: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Math/round
    
    let balken = "";
    const balkenLaenge = // Deine Lösung: Math.round(...)
    
    
    // TODO 2.4: Verschachtelte for-Schleife für Balken-Zeichen
    // Durchlaufe 0 bis 9 (10 Zeichen total)
    // Wenn Index < balkenLaenge: Füge █ hinzu
    // Sonst: Füge ░ hinzu
    
    for (let j = 0; j < 10; j++) {
        if (/* Deine Bedingung */) {
            balken += // Deine Lösung
        } else {
            balken += // Deine Lösung
        }
    }
    
    
    // TODO 2.5: Gib formatierte Ausgabe aus
    // Nutze .padEnd(15) um Namen auf 15 Zeichen aufzufüllen
    // Format: "HTML            ████████░░ 85%"
    // Dokumentation padEnd: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd
    
    console.log(// Deine Lösung);
}
```

**Lernziele:**
- Array von Objekten erstellen
- Verschachtelte Schleifen verstehen und anwenden
- String-Manipulation mit +=
- Math.round() für Berechnungen nutzen

**Erwartete Konsolen-Ausgabe:**
```
HTML            ████████░░ 85%
CSS             ███████░░░ 75%
JavaScript      ██████░░░░ 60%
...
```

---

### Teil 3: Statistiken berechnen (25 Min)

Berechne Durchschnitt und beste/schlechteste Skills:

```javascript
// === SKILL-STATISTIKEN ===

console.log("\n=== STATISTIKEN ===\n");

// TODO 3.1: Berechne die Summe aller Level
// Initialisiere summe mit 0
// Durchlaufe alle Skills und addiere level zur Summe
// Tipp: summe += skillsDetailed[i].level

let summe = // Deine Lösung: 0

// Deine for-Schleife hier:


// TODO 3.2: Berechne den Durchschnitt
// Formel: summe / anzahl
// Runde mit Math.round()

const durchschnitt = // Deine Lösung


// TODO 3.3: Gib Statistiken aus
console.log(`Gesamte Skills: ${skillsDetailed.length}`);
console.log(// Durchschnittliches Level ausgeben);


// TODO 3.4: Finde den besten Skill
// Starte mit erstem Skill: let besterSkill = skillsDetailed[0]
// Durchlaufe ab Index 1 alle weiteren Skills
// Wenn ein Skill höheres Level hat: Setze ihn als besterSkill
// Dokumentation Vergleiche: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Greater_than

let besterSkill = // Deine Lösung

// Deine for-Schleife (ab i = 1):
for (let i = 1; i < skillsDetailed.length; i++) {
    if (/* Deine Bedingung: level größer als besterSkill.level? */) {
        // Deine Lösung
    }
}

console.log(`\nStärkster Skill: ${besterSkill.name} (${besterSkill.level}%)`);


// TODO 3.5: Finde den schwächsten Skill
// Gleiche Logik wie bester Skill, aber mit < Operator

let schwachsterSkill = // Deine Lösung

// Deine for-Schleife hier:


console.log(`Entwicklungspotential: ${schwachsterSkill.name} (${schwachsterSkill.level}%)`);


// TODO 3.6: Kategorisiere Skills nach Level
// Erstelle 3 leere Arrays
// Expert-Level: level >= 80
// Fortgeschritten: level >= 60 (aber < 80)
// Grundlagen: level < 60
// Dokumentation .push(): https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/push

let expertSkills = [];
let fortgeschritteneSkills = [];
let grundSkills = [];

// TODO 3.7: Durchlaufe alle Skills und füge sie in richtige Kategorie ein
for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    if (/* Level >= 80 */) {
        // Füge skill.name zu expertSkills hinzu
    } else if (/* Level >= 60 */) {
        // Füge skill.name zu fortgeschritteneSkills hinzu
    } else {
        // Füge skill.name zu grundSkills hinzu
    }
}


// TODO 3.8: Gib Kategorien aus
// Nutze .join(", ") um Array zu String zu verbinden
// Dokumentation join: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/join

console.log(`\nExpert-Level (≥80%): ${expertSkills.join(", ")}`);
console.log(// Fortgeschritten);
console.log(// Grundlagen);
```

**Lernziele:**
- Summen mit Schleifen berechnen
- Minimum/Maximum in Arrays finden
- Arrays dynamisch mit `.push()` füllen
- `.join()` für String-Konvertierung nutzen

---

### Teil 4: Lernziele mit while-Schleife (20 Min)

```javascript
// === LERNZIELE ===

console.log("\n=== LERNZIELE ===\n");

console.log("Ziel: Alle Skills auf mindestens 70%\n");

// TODO 4.1: Zähle Skills unter 70% und berechne benötigte Stunden
let anzahlUnter70 = 0;
let stundenGeschaetzt = 0;

// TODO 4.2: Durchlaufe alle Skills
for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    // TODO 4.3: Prüfe ob level < 70
    if (/* Deine Bedingung */) {
        // TODO 4.4: Berechne Differenz zu 70
        const differenz = // Deine Lösung: 70 - skill.level
        
        // TODO 4.5: Berechne benötigte Stunden
        // Annahme: 2 Stunden pro 1% Fortschritt
        const stundenProProzent = 2;
        const stundenBenoetigt = // Deine Lösung
        
        console.log(`${skill.name}: ${skill.level}% → 70% (${differenz}% fehlen, ca. ${stundenBenoetigt}h Übung)`);
        
        // TODO 4.6: Erhöhe Zähler und Summe
        anzahlUnter70++;
        stundenGeschaetzt += // Deine Lösung
    }
}

console.log(`\nGesamt: ${anzahlUnter70} Skills unter 70%`);
console.log(`Geschätzte Übungszeit: ${stundenGeschaetzt} Stunden`);


// TODO 4.7: Simuliere Lernfortschritt mit while-Schleife
// Dokumentation while: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/while

console.log("\n=== LERNFORTSCHRITT SIMULATION ===\n");

// Wähle einen Skill der unter 70% ist (z.B. JavaScript bei 60%)
let aktuellerFortschritt = 60;  // Anpassen an deinen Skill
let zielFortschritt = 70;
let wochen = 0;
const fortschrittProWoche = 2;  // 2% pro Woche

// TODO 4.8: Erstelle while-Schleife
// Bedingung: Solange aktuellerFortschritt < zielFortschritt
// In der Schleife:
// - Erhöhe wochen um 1
// - Erhöhe aktuellerFortschritt um fortschrittProWoche
// - Gib Status aus

// Deine while-Schleife hier:


console.log(`\n✓ Ziel erreicht nach ${wochen} Wochen!`);
```

**Lernziele:**
- While-Schleife selbst schreiben
- Unterschied for vs while verstehen
- Berechnungen mit Akkumulatoren (summe +=)
- Wichtig: Variable MUSS sich ändern, sonst Endlosschleife!

**Reflexion:**
- Warum nutzen wir hier while statt for?
- Was passiert, wenn fortschrittProWoche = 0?

---

### Teil 5: Skills im HTML anzeigen (20 Min)

Füge in `index.html` ein:

```html
<section id="skills">
    <h2>Meine Skills</h2>
    <div id="skills-liste">
        <!-- Wird von JavaScript gefüllt -->
    </div>
    <div id="skills-stats">
        <!-- Statistiken -->
    </div>
</section>
```

Am Ende von `skills.js`:

```javascript
// === IM HTML ANZEIGEN ===

console.log("\n=== HTML-AUSGABE WIRD GENERIERT ===\n");

// TODO 5.1: Erstelle HTML-String für alle Skills
let skillsHTML = '<div class="skills-container">';

// TODO 5.2: Durchlaufe alle Skills und erstelle HTML
for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    // TODO 5.3: Bestimme CSS-Klasse basierend auf Level
    let levelClass = "";
    if (/* level >= 80 */) {
        levelClass = "expert";
    } else if (/* level >= 60 */) {
        levelClass = "advanced";
    } else {
        levelClass = "basic";
    }
    
    
    // TODO 5.4: Füge HTML für diesen Skill hinzu
    // Nutze Template Literals und +=
    // Inkludiere: skill-name, skill-bar (mit width: ${skill.level}%), skill-percent
    
    skillsHTML += `
        <div class="skill-item ${levelClass}">
            <!-- Dein HTML-Code hier -->
            <!-- Tipp: <div class="skill-bar" style="width: ${skill.level}%"></div> -->
        </div>
    `;
}

skillsHTML += '</div>';


// TODO 5.5: Füge HTML ins DOM ein
// Dokumentation getElementById: https://developer.mozilla.org/de/docs/Web/API/Document/getElementById

// Deine Lösung:



// TODO 5.6: Erstelle Statistiken-Box
// Zeige: Anzahl Skills, Durchschnitt, bester Skill, schwächster Skill

const statsHTML = `
    <div class="stats-box">
        <h3>Statistiken</h3>
        <!-- Dein HTML-Code hier -->
    </div>
`;

// Deine Lösung: Füge ins DOM ein


console.log("✓ Skills im HTML angezeigt");
```

**Selbstständige Aufgaben:**
- Erstelle eigenes HTML-Design
- Experimentiere mit verschiedenen Darstellungen
- Füge zusätzliche Informationen hinzu

---

### Teil 6: Animation (Optional, 15 Min)

Füge eine Animation hinzu, die Skills langsam hochzählt:

```javascript
// === ANIMIERTE SKILL-ANZEIGE ===

// TODO 6.1: Erstelle Funktion für Animation
// Dokumentation setInterval: https://developer.mozilla.org/de/docs/Web/API/setInterval
// Dokumentation setTimeout: https://developer.mozilla.org/de/docs/Web/API/setTimeout

function animiereSkills() {
    // TODO 6.2: Hole alle Skill-Balken
    // Nutze querySelectorAll(".skill-bar")
    // Dokumentation: https://developer.mozilla.org/de/docs/Web/API/Document/querySelectorAll
    
    const skillBars = // Deine Lösung
    
    
    // TODO 6.3: Durchlaufe alle Balken mit forEach
    // Dokumentation forEach: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach
    
    skillBars.forEach((bar, index) => {
        // Starte bei 0%
        bar.style.width = "0%";
        
        // TODO 6.4: Hole Ziel-Breite
        const zielBreite = // skillsDetailed[index].level
        
        // TODO 6.5: Erstelle Animation mit setInterval
        let aktuelleBreite = 0;
        const schritte = 50;
        const schrittGroesse = zielBreite / schritte;
        const interval = 20;  // Millisekunden
        
        const animation = setInterval(() => {
            aktuelleBreite += schrittGroesse;
            
            if (aktuelleBreite >= zielBreite) {
                bar.style.width = zielBreite + "%";
                clearInterval(animation);
            } else {
                bar.style.width = aktuelleBreite + "%";
            }
        }, interval);
    });
}

// TODO 6.6: Starte Animation nach 500ms
// Nutze setTimeout

// Deine Lösung:

```

**Lernziele:**
- Funktionen erstellen (kommt ausführlich später)
- setInterval und setTimeout verstehen
- DOM-Manipulation mit style

---

## Erfolgskriterien

- [ ] Alle TODO-Aufgaben sind selbstständig gelöst
- [ ] Mindestens 7 Skills sind als Array definiert
- [ ] Skills werden mit for-Schleife in der Konsole ausgegeben
- [ ] Skills mit Level-Angabe (0-100%) als Objekt-Array
- [ ] Fortschrittsbalken werden mit verschachtelter Schleife erstellt
- [ ] Durchschnitt, bester und schwächster Skill werden berechnet
- [ ] Skills werden nach Kategorien sortiert
- [ ] While-Schleife simuliert Lernfortschritt
- [ ] Skills werden im HTML mit Fortschrittsbalken angezeigt
- [ ] Statistiken werden im HTML ausgegeben
- [ ] Code ist gut strukturiert und kommentiert
- [ ] Keine Fehler in der Konsole

---

## Tipps für selbstständiges Arbeiten

- **Schleifen-Muster verstehen:** Das for-Schleifen-Muster `for (let i = 0; i < length; i++)` ist fundamental!
- **Array-Index:** Immer daran denken: Arrays starten bei 0, nicht bei 1
- **Endlosschleifen:** Bei while-Schleifen IMMER prüfen, ob sich die Variable ändert
- **Debugging:** Nutze `console.log(i)` in Schleifen, um zu sehen, was passiert
- **Performance:** Erst kompletten HTML-String bauen, dann einmal `innerHTML` setzen
- **Teste schrittweise:** Nach jedem TODO testen!

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen for- und while-Schleife?**  
   *Wann würdest du welche nutzen? Gib je 2 Beispiele.*

2. **Was passiert, wenn du `i <= array.length` statt `i < array.length` schreibst?**  
   *Teste es und erkläre den Fehler. Warum kommt `undefined`?*

3. **Erstelle eine for-Schleife, die nur gerade Zahlen von 0 bis 20 ausgibt.**  
   *Zwei Lösungswege: Nutze `i += 2` oder `if (i % 2 === 0)`*

4. **Warum ist diese while-Schleife gefährlich?**
   ```javascript
   let x = 10;
   while (x > 5) {
       console.log(x);
       // x wird nie verändert!
   }
   ```
   *Wie kannst du sie stoppen, ohne den Browser zu schließen?*

5. **Experimentiere: Erstelle eine verschachtelte Schleife für ein Multiplikationstabelle (1x1 bis 10x10).**  
   *Wie viele Durchläufe macht die äußere, wie viele die innere Schleife?*

---

## Weiterführende Links

**Pflichtlektüre für TODO-Aufgaben:**
- [MDN: for-Schleife](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/for)
- [MDN: while-Schleife](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/while)
- [MDN: Array](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: Array.push()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
- [MDN: Array.join()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

**Vertiefung:**
- [JavaScript.info: Loops](https://javascript.info/while-for)
- [JavaScript.info: Arrays](https://javascript.info/array)
- [JavaScript.info: Array Methods](https://javascript.info/array-methods)

**Array-Methoden:**
- [MDN: forEach](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN: map](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [MDN: filter](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

**Interaktive Übungen:**
- [freeCodeCamp: Loops](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- [JavaScript.info: Tasks](https://javascript.info/while-for#tasks)

---

**Geschätzte Zeit:** 120 Minuten  
**Nächster Schritt:** Im optionalen Vertiefungsauftrag erstellst du ein interaktives Dashboard mit allen erlernten Konzepten!