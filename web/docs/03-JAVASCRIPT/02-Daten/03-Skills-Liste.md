# Auftrag 3: Skills-Liste mit Schleifen

## Ziel

Du lernst, mit for- und while-Schleifen zu arbeiten, um wiederholende Aufgaben zu automatisieren. Deine Portfolio-Seite zeigt eine interaktive Skills-Liste, die automatisch generiert wird, und nutzt Schleifen für Berechnungen und Animationen.

## Beschreibung

Schleifen sind das Werkzeug, um Code zu wiederholen, ohne ihn hundertmal zu schreiben. Mit for-Schleifen automatisierst du Listen, Berechnungen und Animationen. While-Schleifen laufen, solange eine Bedingung wahr ist. In diesem Auftrag erstellst du eine dynamische Skills-Liste für dein Portfolio mit Fortschrittsbalken, Statistiken und automatisierten Ausgaben.

---

### Teil 1: Skills-Array und einfache for-Schleife (15 Min)

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

// Skills als Array
const skills = [
    "HTML",
    "CSS",
    "JavaScript",
    "Git",
    "VS Code",
    "Debugging",
    "Problemlösung"
];

// Anzahl Skills
console.log(`Ich habe ${skills.length} Skills:`);

// Skills mit for-Schleife ausgeben
for (let i = 0; i < skills.length; i++) {
    console.log(`${i + 1}. ${skills[i]}`);
}

console.log("\n");

// Alternative: Jeder Skill mit Emoji
const skillEmoji = "⭐";

for (let i = 0; i < skills.length; i++) {
    console.log(`${skillEmoji} ${skills[i]}`);
}
```

**Neue Konzepte:**
- Arrays speichern mehrere Werte: `[wert1, wert2, wert3]`
- `.length` gibt Anzahl Elemente zurück
- `for (let i = 0; i < array.length; i++)` ist das Standard-Muster für Arrays
- `i` ist der Index (0, 1, 2, 3, ...)
- `array[i]` greift auf Element an Position i zu

---

### Teil 2: Skills mit Fortschritt (20 Min)

Erweitere die Skills mit Fortschrittsinformationen:

```javascript
// === SKILLS MIT FORTSCHRITT ===

console.log("\n=== SKILLS MIT FORTSCHRITT ===\n");

// Skills mit Fortschritt in Prozent
const skillsDetailed = [
    { name: "HTML", level: 85 },
    { name: "CSS", level: 75 },
    { name: "JavaScript", level: 60 },
    { name: "Git", level: 50 },
    { name: "VS Code", level: 70 },
    { name: "Debugging", level: 55 },
    { name: "Problemlösung", level: 65 }
];

// Ausgabe mit Level
for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    const name = skill.name;
    const level = skill.level;
    
    // Fortschrittsbalken erstellen
    let balken = "";
    const balkenLaenge = Math.round(level / 10);  // 100% = 10 Zeichen
    
    for (let j = 0; j < 10; j++) {
        if (j < balkenLaenge) {
            balken += "█";
        } else {
            balken += "░";
        }
    }
    
    console.log(`${name.padEnd(15)} ${balken} ${level}%`);
}
```

**Neue Konzepte:**
- Objekte in Arrays: `[{ key: value }, { key: value }]`
- Verschachtelte Schleifen: Eine Schleife in einer anderen
- `Math.round()` rundet auf ganze Zahl
- `.padEnd(n)` füllt String auf n Zeichen auf
- Block-Zeichen `█` und `░` für visuelle Balken

**Konsolen-Ausgabe:**
```
HTML            ████████░░ 85%
CSS             ███████░░░ 75%
JavaScript      ██████░░░░ 60%
Git             █████░░░░░ 50%
VS Code         ███████░░░ 70%
Debugging       █████░░░░░ 55%
Problemlösung   ██████░░░░ 65%
```

---

### Teil 3: Statistiken berechnen (15 Min)

Berechne Durchschnitt und beste/schlechteste Skills:

```javascript
// === SKILL-STATISTIKEN ===

console.log("\n=== STATISTIKEN ===\n");

// Durchschnitt berechnen
let summe = 0;

for (let i = 0; i < skillsDetailed.length; i++) {
    summe += skillsDetailed[i].level;
}

const durchschnitt = Math.round(summe / skillsDetailed.length);

console.log(`Gesamte Skills: ${skillsDetailed.length}`);
console.log(`Durchschnittliches Level: ${durchschnitt}%`);

// Bester Skill finden
let besterSkill = skillsDetailed[0];

for (let i = 1; i < skillsDetailed.length; i++) {
    if (skillsDetailed[i].level > besterSkill.level) {
        besterSkill = skillsDetailed[i];
    }
}

console.log(`\nStärkster Skill: ${besterSkill.name} (${besterSkill.level}%)`);

// Schwächster Skill finden
let schwachsterSkill = skillsDetailed[0];

for (let i = 1; i < skillsDetailed.length; i++) {
    if (skillsDetailed[i].level < schwachsterSkill.level) {
        schwachsterSkill = skillsDetailed[i];
    }
}

console.log(`Entwicklungspotential: ${schwachsterSkill.name} (${schwachsterSkill.level}%)`);

// Skills nach Level kategorisieren
let expertSkills = [];
let fortgeschritteneSkills = [];
let grundSkills = [];

for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    if (skill.level >= 80) {
        expertSkills.push(skill.name);
    } else if (skill.level >= 60) {
        fortgeschritteneSkills.push(skill.name);
    } else {
        grundSkills.push(skill.name);
    }
}

console.log(`\nExpert-Level (≥80%): ${expertSkills.join(", ")}`);
console.log(`Fortgeschritten (≥60%): ${fortgeschritteneSkills.join(", ")}`);
console.log(`Grundlagen (< 60%): ${grundSkills.join(", ")}`);
```

**Neue Konzepte:**
- Summe mit Schleife berechnen: `summe += wert`
- Minimum/Maximum suchen mit Vergleichen in Schleife
- Neue Arrays mit `.push()` füllen
- `.join(", ")` verbindet Array-Elemente mit Komma

---

### Teil 4: Lernziele mit while-Schleife (15 Min)

```javascript
// === LERNZIELE ===

console.log("\n=== LERNZIELE ===\n");

// Ziel: Alle Skills auf mindestens 70% bringen
console.log("Ziel: Alle Skills auf mindestens 70%\n");

let anzahlUnter70 = 0;
let stundenGeschaetzt = 0;

for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    if (skill.level < 70) {
        const differenz = 70 - skill.level;
        const stundenProProzent = 2;  // 2 Stunden pro 1%
        const stundenBenoetigt = differenz * stundenProProzent;
        
        console.log(`${skill.name}: ${skill.level}% → 70% (${differenz}% fehlen, ca. ${stundenBenoetigt}h Übung)`);
        
        anzahlUnter70++;
        stundenGeschaetzt += stundenBenoetigt;
    }
}

console.log(`\nGesamt: ${anzahlUnter70} Skills unter 70%`);
console.log(`Geschätzte Übungszeit: ${stundenGeschaetzt} Stunden`);

// Simuliere Lernfortschritt mit while-Schleife
console.log("\n=== LERNFORTSCHRITT SIMULATION ===\n");

let aktuellerFortschritt = 60;  // JavaScript startet bei 60%
let zielFortschritt = 70;
let wochen = 0;
const fortschrittProWoche = 2;  // 2% pro Woche

while (aktuellerFortschritt < zielFortschritt) {
    wochen++;
    aktuellerFortschritt += fortschrittProWoche;
    console.log(`Woche ${wochen}: JavaScript-Level: ${aktuellerFortschritt}%`);
}

console.log(`\n✓ Ziel erreicht nach ${wochen} Wochen!`);
```

**Neue Konzepte:**
- while-Schleife: `while (bedingung) { ... }`
- Läuft, solange Bedingung wahr ist
- Wichtig: Variable muss sich ändern, sonst Endlosschleife!
- Praktisch für Simulationen und unbekannte Anzahl Durchläufe

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

// Skills-Liste mit Fortschrittsbalken
let skillsHTML = '<div class="skills-container">';

for (let i = 0; i < skillsDetailed.length; i++) {
    const skill = skillsDetailed[i];
    
    // CSS-Klasse basierend auf Level
    let levelClass = "";
    if (skill.level >= 80) {
        levelClass = "expert";
    } else if (skill.level >= 60) {
        levelClass = "advanced";
    } else {
        levelClass = "basic";
    }
    
    skillsHTML += `
        <div class="skill-item ${levelClass}">
            <div class="skill-name">${skill.name}</div>
            <div class="skill-bar-container">
                <div class="skill-bar" style="width: ${skill.level}%"></div>
            </div>
            <div class="skill-percent">${skill.level}%</div>
        </div>
    `;
}

skillsHTML += '</div>';

document.getElementById("skills-liste").innerHTML = skillsHTML;

// Statistiken anzeigen
const statsHTML = `
    <div class="stats-box">
        <h3>Statistiken</h3>
        <p><strong>Anzahl Skills:</strong> ${skillsDetailed.length}</p>
        <p><strong>Durchschnitt:</strong> ${durchschnitt}%</p>
        <p><strong>Stärkster Skill:</strong> ${besterSkill.name} (${besterSkill.level}%)</p>
        <p><strong>Entwicklungspotential:</strong> ${schwachsterSkill.name} (${schwachsterSkill.level}%)</p>
    </div>
`;

document.getElementById("skills-stats").innerHTML = statsHTML;

console.log("✓ Skills im HTML angezeigt");
```

**Optional: CSS für schöne Darstellung** (in `styles.css`):

```css
.skills-container {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.skill-item {
    display: grid;
    grid-template-columns: 150px 1fr 50px;
    gap: 1rem;
    align-items: center;
}

.skill-bar-container {
    background-color: #e0e0e0;
    border-radius: 5px;
    height: 20px;
    overflow: hidden;
}

.skill-bar {
    height: 100%;
    background: linear-gradient(90deg, #0066CC, #00C9A7);
    border-radius: 5px;
    transition: width 0.5s ease;
}

.skill-item.expert .skill-bar {
    background: linear-gradient(90deg, #00C9A7, #00FF88);
}

.skill-item.advanced .skill-bar {
    background: linear-gradient(90deg, #0066CC, #00C9A7);
}

.skill-item.basic .skill-bar {
    background: linear-gradient(90deg, #FF6B35, #FFA500);
}

.stats-box {
    margin-top: 2rem;
    padding: 1rem;
    background-color: #f5f5f5;
    border-radius: 8px;
}
```

---

### Teil 6: Animierte Skill-Erhöhung (Optional, 10 Min)

Füge eine Animation hinzu, die Skills langsam hochzählt:

```javascript
// === ANIMIERTE SKILL-ANZEIGE ===

function animiereSkills() {
    const skillBars = document.querySelectorAll(".skill-bar");
    
    skillBars.forEach((bar, index) => {
        // Starte bei 0%
        bar.style.width = "0%";
        
        // Ziel-Breite aus data-Attribut oder berechnen
        const zielBreite = skillsDetailed[index].level;
        
        // Animiere mit setInterval
        let aktuelleBreite = 0;
        const schritte = 50;  // Anzahl Schritte
        const schrittGroesse = zielBreite / schritte;
        const interval = 20;  // Millisekunden pro Schritt
        
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

// Animation nach 500ms starten (damit HTML geladen ist)
setTimeout(animiereSkills, 500);
```

**Neue Konzepte:**
- `setInterval()` wiederholt Funktion in Intervallen
- `clearInterval()` stoppt die Wiederholung
- `setTimeout()` führt Funktion nach Verzögerung aus
- `.forEach()` durchläuft alle Elemente einer NodeList

---

## Erfolgskriterien

- [ ] `skills.js` ist erstellt und eingebunden
- [ ] Mindestens 5 Skills sind als Array definiert
- [ ] Skills werden mit for-Schleife in der Konsole ausgegeben
- [ ] Skills mit Level-Angabe (0-100%) als Objekt-Array
- [ ] Fortschrittsbalken werden mit verschachtelter Schleife erstellt
- [ ] Durchschnitt, bester und schwächster Skill werden berechnet
- [ ] While-Schleife simuliert Lernfortschritt
- [ ] Skills werden im HTML mit Fortschrittsbalken angezeigt
- [ ] Statistiken werden im HTML ausgegeben
- [ ] Keine Fehler in der Konsole

---

## Tipps

- **Schleifen-Zähler:** Nutze immer `let i = 0` in for-Schleifen, nicht `var`
- **Array-Index:** Arrays starten bei 0, nicht bei 1! `array[0]` ist das erste Element
- **Endlosschleifen vermeiden:** Bei while-Schleifen IMMER prüfen, ob die Variable sich ändert
- **console.log() in Schleifen:** Zum Debuggen innerhalb der Schleife ausgeben, was passiert
- **Performance:** Viele Elemente im DOM? Erst kompletten HTML-String bauen, dann einmal `innerHTML` setzen
- **CSS-Klassen dynamisch:** Nutze Bedingungen, um verschiedene CSS-Klassen zuzuweisen

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen for- und while-Schleife?**  
   *Wann würdest du welche nutzen? Gib je 2 Beispiele.*

2. **Was passiert, wenn du `i <= array.length` statt `i < array.length` schreibst?**  
   *Teste es und erkläre den Fehler. Tipp: `undefined`*

3. **Erstelle eine for-Schleife, die nur gerade Zahlen von 0 bis 20 ausgibt.**  
   *Tipp: Nutze `i += 2` oder `if (i % 2 === 0)`*

4. **Warum ist diese while-Schleife gefährlich?**
   ```javascript
   let x = 10;
   while (x > 5) {
       console.log(x);
       // Fehler: x wird nie verändert!
   }
   ```
   *Wie kannst du sie stoppen, ohne den Browser zu schliessen?*

5. **Experimentiere: Erstelle eine verschachtelte Schleife für ein Multiplikationstabelle (1x1 bis 10x10).**  
   *Wie viele Durchläufe macht die äussere, wie viele die innere Schleife?*

---

## Weiterführende Links

**Schleifen:**
- [MDN: for-Schleife](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/for)
- [MDN: while-Schleife](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/while)
- [JavaScript.info: Loops](https://javascript.info/while-for)

**Arrays:**
- [MDN: Array](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JavaScript.info: Arrays](https://javascript.info/array)
- [W3Schools: JS Arrays](https://www.w3schools.com/js/js_arrays.asp)

**Array-Methoden:**
- [MDN: forEach](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN: map](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [MDN: filter](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

**Performance:**
- [JavaScript Loop Performance](https://stackoverflow.com/questions/5349425/whats-the-fastest-way-to-loop-through-an-array-in-javascript)
- [Best Practices for Loops](https://www.sitepoint.com/premium/books/javascript-best-practice/read/2/k01nwte1)

**Interaktive Übungen:**
- [freeCodeCamp: Loops](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- [JavaScript.info: Tasks](https://javascript.info/while-for#tasks)

---

**Geschätzte Zeit:** 95 Minuten  
**Nächster Schritt:** Im optionalen Vertiefungsauftrag erstellst du ein interaktives Quiz mit allen erlernten Konzepten!
