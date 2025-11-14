# Optional: Interaktives Portfolio-Dashboard

## Ziel

Du kombinierst alle erlernten Konzepte (Variablen, Datentypen, if-else, Schleifen) in einem fortgeschrittenen Projekt: Ein interaktives Portfolio-Dashboard mit Projektverwaltung, Zielerreichung, Statistiken und dynamischen Filtern. Dieser Auftrag ist anspruchsvoller und zeigt dir, wie professionelle Entwickler komplexe Funktionen aufbauen.

## Beschreibung

In diesem Vertiefungsauftrag erstellst du ein Dashboard für dein Portfolio, das verschiedene Metriken verfolgt: abgeschlossene Projekte, Lernfortschritt, Zeitinvestment und Ziele. Du nutzt komplexe Datenstrukturen (Arrays von Objekten), verschachtelte Schleifen, mehrfache Bedingungen und berechnest automatisch Statistiken. Das Ergebnis ist eine realistische Komponente, die du später in dein Portfolio einbauen kannst.

---

### Teil 1: Projekt-Datenstruktur aufbauen (20 Min)

Erstelle eine neue Datei **`dashboard.js`** und binde sie ein:

```html
<script src="dashboard.js"></script>
```

**In `dashboard.js`:**

```javascript
// =====================================================
// PORTFOLIO-DASHBOARD
// =====================================================

console.log("=== PORTFOLIO-DASHBOARD ===\n");

// Projekt-Datenbank
const projekte = [
    {
        id: 1,
        titel: "Portfolio-Website",
        kategorie: "Webentwicklung",
        technologien: ["HTML", "CSS", "JavaScript"],
        status: "In Arbeit",
        fortschritt: 75,
        startDatum: "2025-09-01",
        geplantesEnde: "2025-12-31",
        zeitInvestiert: 45,  // Stunden
        schwierigkeit: "Mittel",
        prioritaet: "Hoch"
    },
    {
        id: 2,
        titel: "HTML-Grundlagen Kurs",
        kategorie: "Lernen",
        technologien: ["HTML"],
        status: "Abgeschlossen",
        fortschritt: 100,
        startDatum: "2025-08-01",
        geplantesEnde: "2025-08-31",
        zeitInvestiert: 30,
        schwierigkeit: "Einfach",
        prioritaet: "Mittel"
    },
    {
        id: 3,
        titel: "To-Do App",
        kategorie: "Projekt",
        technologien: ["HTML", "CSS", "JavaScript"],
        status: "Geplant",
        fortschritt: 0,
        startDatum: "2026-01-15",
        geplantesEnde: "2026-03-31",
        zeitInvestiert: 0,
        schwierigkeit: "Mittel",
        prioritaet: "Niedrig"
    },
    {
        id: 4,
        titel: "CSS Grid & Flexbox",
        kategorie: "Lernen",
        technologien: ["CSS"],
        status: "In Arbeit",
        fortschritt: 60,
        startDatum: "2025-10-01",
        geplantesEnde: "2025-11-30",
        zeitInvestiert: 20,
        schwierigkeit: "Mittel",
        prioritaet: "Hoch"
    },
    {
        id: 5,
        titel: "JavaScript Calculator",
        kategorie: "Projekt",
        technologien: ["HTML", "CSS", "JavaScript"],
        status: "In Arbeit",
        fortschritt: 40,
        startDatum: "2025-11-01",
        geplantesEnde: "2025-12-15",
        zeitInvestiert: 15,
        schwierigkeit: "Schwer",
        prioritaet: "Mittel"
    },
    {
        id: 6,
        titel: "Git Basics",
        kategorie: "Lernen",
        technologien: ["Git"],
        status: "Abgeschlossen",
        fortschritt: 100,
        startDatum: "2025-09-15",
        geplantesEnde: "2025-10-15",
        zeitInvestiert: 25,
        schwierigkeit: "Mittel",
        prioritaet: "Hoch"
    }
];

console.log(`Gesamtanzahl Projekte: ${projekte.length}\n`);
```

**Neue Konzepte:**
- Komplexe Datenstrukturen: Array von Objekten mit vielen Properties
- Realistische Projekt-Eigenschaften wie Status, Fortschritt, Zeitinvestment
- Basis für alle weiteren Berechnungen

---

### Teil 2: Dashboard-Statistiken berechnen (25 Min)

```javascript
// === HAUPT-STATISTIKEN ===

console.log("=== STATISTIKEN ===\n");

// Zähler initialisieren
let anzahlAbgeschlossen = 0;
let anzahlInArbeit = 0;
let anzahlGeplant = 0;

let gesamtZeit = 0;
let gesamtFortschritt = 0;

// Projekte durchgehen
for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // Status zählen
    if (projekt.status === "Abgeschlossen") {
        anzahlAbgeschlossen++;
    } else if (projekt.status === "In Arbeit") {
        anzahlInArbeit++;
    } else if (projekt.status === "Geplant") {
        anzahlGeplant++;
    }
    
    // Zeit und Fortschritt summieren
    gesamtZeit += projekt.zeitInvestiert;
    gesamtFortschritt += projekt.fortschritt;
}

// Durchschnitte berechnen
const durchschnittFortschritt = Math.round(gesamtFortschritt / projekte.length);

console.log("STATUS-VERTEILUNG:");
console.log(`  Abgeschlossen: ${anzahlAbgeschlossen}`);
console.log(`  In Arbeit:     ${anzahlInArbeit}`);
console.log(`  Geplant:       ${anzahlGeplant}`);
console.log("");

console.log("ZEITINVESTMENT:");
console.log(`  Gesamt:        ${gesamtZeit} Stunden`);
console.log(`  Pro Projekt:   ${Math.round(gesamtZeit / projekte.length)} Stunden`);
console.log("");

console.log("FORTSCHRITT:");
console.log(`  Durchschnitt:  ${durchschnittFortschritt}%`);
console.log("");

// === TECHNOLOGIE-ANALYSE ===

console.log("=== TECHNOLOGIE-ANALYSE ===\n");

// Technologien zählen
let technologieCount = {};

for (let i = 0; i < projekte.length; i++) {
    const technologien = projekte[i].technologien;
    
    for (let j = 0; j < technologien.length; j++) {
        const tech = technologien[j];
        
        if (technologieCount[tech]) {
            technologieCount[tech]++;
        } else {
            technologieCount[tech] = 1;
        }
    }
}

// Technologien sortiert ausgeben
console.log("TECHNOLOGIE-NUTZUNG:");

const techKeys = Object.keys(technologieCount);

for (let i = 0; i < techKeys.length; i++) {
    const tech = techKeys[i];
    const anzahl = technologieCount[tech];
    const prozent = Math.round((anzahl / projekte.length) * 100);
    
    let balken = "";
    for (let j = 0; j < anzahl; j++) {
        balken += "█";
    }
    
    console.log(`  ${tech.padEnd(12)} ${balken} ${anzahl}x (${prozent}%)`);
}

console.log("");
```

**Neue Konzepte:**
- Mehrere Zähler gleichzeitig führen
- Verschachtelte Schleifen für Arrays in Objekten
- Objekt als "Dictionary" für Zählung: `{ key: count }`
- `Object.keys()` gibt alle Schlüssel eines Objekts zurück

---

### Teil 3: Projekt-Filter und Suche (20 Min)

```javascript
// === PROJEKT-FILTER ===

console.log("=== PROJEKT-FILTER ===\n");

// Filter: Nur aktive Projekte mit hoher Priorität
console.log("AKTIVE PROJEKTE MIT HOHER PRIORITÄT:");

let gefiltert = 0;

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    if (projekt.status === "In Arbeit" && projekt.prioritaet === "Hoch") {
        console.log(`  ${projekt.id}. ${projekt.titel} (${projekt.fortschritt}%)`);
        gefiltert++;
    }
}

console.log(`  → ${gefiltert} Projekte gefunden\n`);

// Filter: Projekte mit Fortschritt unter 50%
console.log("PROJEKTE MIT VERZÖGERUNG (<50%):");

gefiltert = 0;

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    if (projekt.status === "In Arbeit" && projekt.fortschritt < 50) {
        const differenz = 50 - projekt.fortschritt;
        console.log(`  ⚠️  ${projekt.titel}: ${projekt.fortschritt}% (${differenz}% hinter Plan)`);
        gefiltert++;
    }
}

if (gefiltert === 0) {
    console.log("  ✓ Alle Projekte im Plan!");
}

console.log("");

// Filter: Nach Technologie
const gesuchte_Technologie = "JavaScript";

console.log(`PROJEKTE MIT ${gesuchte_Technologie.toUpperCase()}:`);

gefiltert = 0;

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    let hatTechnologie = false;
    
    for (let j = 0; j < projekt.technologien.length; j++) {
        if (projekt.technologien[j] === gesuchte_Technologie) {
            hatTechnologie = true;
            break;  // Schleife abbrechen, wenn gefunden
        }
    }
    
    if (hatTechnologie) {
        console.log(`  ${projekt.titel} (${projekt.status})`);
        gefiltert++;
    }
}

console.log(`  → ${gefiltert} Projekte gefunden\n`);
```

**Neue Konzepte:**
- Mehrfache Filter-Bedingungen mit `&&`
- `break;` bricht Schleife vorzeitig ab
- Suche in verschachtelten Arrays
- Flag-Variable `hatTechnologie` für Tracking

---

### Teil 4: Zeitmanagement & Prognose (20 Min)

```javascript
// === ZEITMANAGEMENT ===

console.log("=== ZEITMANAGEMENT ===\n");

// Verbleibende Zeit bis zum Ziel berechnen
const zielStunden = 200;  // Jahresziel: 200 Stunden
const verbleibendeStunden = zielStunden - gesamtZeit;
const fortschrittZiel = Math.round((gesamtZeit / zielStunden) * 100);

console.log("JAHRESZIEL:");
console.log(`  Ziel:          ${zielStunden} Stunden`);
console.log(`  Erreicht:      ${gesamtZeit} Stunden (${fortschrittZiel}%)`);
console.log(`  Verbleibend:   ${verbleibendeStunden} Stunden`);
console.log("");

// Prognose: Wann ist das Ziel erreicht?
const stundenProWoche = 8;  // Durchschnittlich 8h pro Woche
const wochenBisZiel = Math.ceil(verbleibendeStunden / stundenProWoche);

console.log("PROGNOSE:");
console.log(`  Wochenstunden:   ${stundenProWoche}h`);
console.log(`  Wochen bis Ziel: ${wochenBisZiel}`);
console.log("");

// Welche Projekte brauchen am meisten Zeit?
console.log("ZEITINTENSIVSTE PROJEKTE:");

// Projekte nach Zeit sortieren (Bubble Sort vereinfacht)
let projekteKopie = [];

for (let i = 0; i < projekte.length; i++) {
    projekteKopie.push(projekte[i]);
}

// Sortieren (einfache Methode)
for (let i = 0; i < projekteKopie.length; i++) {
    for (let j = i + 1; j < projekteKopie.length; j++) {
        if (projekteKopie[j].zeitInvestiert > projekteKopie[i].zeitInvestiert) {
            const temp = projekteKopie[i];
            projekteKopie[i] = projekteKopie[j];
            projekteKopie[j] = temp;
        }
    }
}

// Top 3 ausgeben
for (let i = 0; i < 3 && i < projekteKopie.length; i++) {
    const projekt = projekteKopie[i];
    const prozent = Math.round((projekt.zeitInvestiert / gesamtZeit) * 100);
    console.log(`  ${i + 1}. ${projekt.titel}: ${projekt.zeitInvestiert}h (${prozent}%)`);
}

console.log("");
```

**Neue Konzepte:**
- Zukunftsprognosen mit Berechnungen
- `Math.ceil()` rundet auf (im Gegensatz zu `Math.floor()`)
- Array kopieren für Sortierung
- Bubble Sort Algorithmus (einfachste Sortierung)
- Temp-Variable für Tausch

---

### Teil 5: Zielerreichungs-Tracker (15 Min)

```javascript
// === ZIELERREICHUNG ===

console.log("=== ZIELERREICHUNG ===\n");

// Monatsziele definieren
const monatsZiele = [
    { monat: "November", zielProjekte: 2, zielStunden: 40 },
    { monat: "Dezember", zielProjekte: 1, zielStunden: 35 }
];

// Aktueller Fortschritt (November)
const novemberProjekte = anzahlAbgeschlossen;  // Vereinfacht
const novemberStunden = gesamtZeit;

const aktuellesZiel = monatsZiele[0];

console.log(`MONATSZIEL ${aktuellesZiel.monat.toUpperCase()}:`);
console.log("");

// Projekt-Ziel prüfen
const projektErreicht = novemberProjekte >= aktuellesZiel.zielProjekte;
const projektFehlt = aktuellesZiel.zielProjekte - novemberProjekte;

if (projektErreicht) {
    console.log(`  ✅ Projekte: ${novemberProjekte}/${aktuellesZiel.zielProjekte} – Ziel erreicht!`);
} else {
    console.log(`  ⏳ Projekte: ${novemberProjekte}/${aktuellesZiel.zielProjekte} – Noch ${projektFehlt} benötigt`);
}

// Stunden-Ziel prüfen
const stundenErreicht = novemberStunden >= aktuellesZiel.zielStunden;
const stundenFehlen = aktuellesZiel.zielStunden - novemberStunden;

if (stundenErreicht) {
    console.log(`  ✅ Stunden: ${novemberStunden}/${aktuellesZiel.zielStunden}h – Ziel erreicht!`);
} else {
    const prozent = Math.round((novemberStunden / aktuellesZiel.zielStunden) * 100);
    console.log(`  ⏳ Stunden: ${novemberStunden}/${aktuellesZiel.zielStunden}h (${prozent}%) – Noch ${stundenFehlen}h`);
}

console.log("");

// Motivations-Nachricht basierend auf Fortschritt
let motivation = "";

if (projektErreicht && stundenErreicht) {
    motivation = "🎉 Fantastisch! Beide Ziele erreicht!";
} else if (projektErreicht || stundenErreicht) {
    motivation = "👍 Gut im Plan! Ein Ziel erreicht, weitermachen!";
} else {
    const gesamtProzent = Math.round(((novemberProjekte / aktuellesZiel.zielProjekte) + (novemberStunden / aktuellesZiel.zielStunden)) / 2 * 100);
    
    if (gesamtProzent >= 75) {
        motivation = "💪 Fast geschafft! Noch ein kleiner Push!";
    } else if (gesamtProzent >= 50) {
        motivation = "⚡ Halbzeit! Weiter so!";
    } else {
        motivation = "🚀 Zeit, Gas zu geben! Du schaffst das!";
    }
}

console.log(motivation);
console.log("");
```

**Neue Konzepte:**
- Komplexe Bedingungslogik für verschiedene Szenarien
- Mehrere Bedingungen mit `&&` und `||` kombinieren
- Dynamische Nachrichten basierend auf Metriken
- Prozentuale Berechnungen für Fortschritt

---

### Teil 6: Dashboard im HTML anzeigen (30 Min)

Füge in `index.html` ein:

```html
<section id="dashboard">
    <h2>Portfolio Dashboard</h2>
    <div id="dashboard-stats" class="dashboard-grid">
        <!-- Statistiken -->
    </div>
    <div id="dashboard-projekte">
        <h3>Aktuelle Projekte</h3>
        <div id="projekt-liste">
            <!-- Projekt-Karten -->
        </div>
    </div>
    <div id="dashboard-ziele">
        <!-- Zielerreichung -->
    </div>
</section>
```

Am Ende von `dashboard.js`:

```javascript
// === DASHBOARD IM HTML ===

console.log("=== HTML-AUSGABE ===\n");

// Statistik-Karten
const statsHTML = `
    <div class="stat-card">
        <h3>${projekte.length}</h3>
        <p>Gesamt Projekte</p>
    </div>
    <div class="stat-card">
        <h3>${anzahlAbgeschlossen}</h3>
        <p>Abgeschlossen</p>
    </div>
    <div class="stat-card">
        <h3>${anzahlInArbeit}</h3>
        <p>In Arbeit</p>
    </div>
    <div class="stat-card">
        <h3>${gesamtZeit}h</h3>
        <p>Zeitinvestment</p>
    </div>
    <div class="stat-card">
        <h3>${durchschnittFortschritt}%</h3>
        <p>Ø Fortschritt</p>
    </div>
    <div class="stat-card">
        <h3>${fortschrittZiel}%</h3>
        <p>Jahresziel</p>
    </div>
`;

document.getElementById("dashboard-stats").innerHTML = statsHTML;

// Projekt-Karten (nur aktive)
let projekteHTML = "";

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // Nur In Arbeit anzeigen
    if (projekt.status !== "In Arbeit") {
        continue;  // Überspringen
    }
    
    // Status-Klasse für CSS
    let statusClass = "";
    if (projekt.fortschritt >= 75) {
        statusClass = "status-gut";
    } else if (projekt.fortschritt >= 50) {
        statusClass = "status-mittel";
    } else {
        statusClass = "status-niedrig";
    }
    
    projekteHTML += `
        <div class="projekt-card ${statusClass}">
            <div class="projekt-header">
                <h4>${projekt.titel}</h4>
                <span class="prioritaet prioritaet-${projekt.prioritaet.toLowerCase()}">${projekt.prioritaet}</span>
            </div>
            <div class="projekt-meta">
                <span class="kategorie">${projekt.kategorie}</span>
                <span class="schwierigkeit">${projekt.schwierigkeit}</span>
            </div>
            <div class="technologien">
                ${projekt.technologien.map(tech => `<span class="tech-tag">${tech}</span>`).join('')}
            </div>
            <div class="fortschritt-container">
                <div class="fortschritt-bar" style="width: ${projekt.fortschritt}%"></div>
            </div>
            <div class="projekt-stats">
                <span>Fortschritt: ${projekt.fortschritt}%</span>
                <span>Zeit: ${projekt.zeitInvestiert}h</span>
            </div>
        </div>
    `;
}

document.getElementById("projekt-liste").innerHTML = projekteHTML;

// Zielerreichung
const zieleHTML = `
    <div class="ziele-box">
        <h3>Monatsziel ${aktuellesZiel.monat}</h3>
        <div class="ziel-item">
            <p>Projekte: ${novemberProjekte}/${aktuellesZiel.zielProjekte}</p>
            <div class="ziel-bar">
                <div class="ziel-fortschritt" style="width: ${(novemberProjekte / aktuellesZiel.zielProjekte) * 100}%"></div>
            </div>
        </div>
        <div class="ziel-item">
            <p>Stunden: ${novemberStunden}/${aktuellesZiel.zielStunden}h</p>
            <div class="ziel-bar">
                <div class="ziel-fortschritt" style="width: ${(novemberStunden / aktuellesZiel.zielStunden) * 100}%"></div>
            </div>
        </div>
        <p class="motivation">${motivation}</p>
    </div>
`;

document.getElementById("dashboard-ziele").innerHTML = zieleHTML;

console.log("✓ Dashboard im HTML angezeigt");
```

**CSS für Dashboard** (in `styles.css`):

```css
.dashboard-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
}

.stat-card {
    background: linear-gradient(135deg, #0066CC, #00C9A7);
    color: white;
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
}

.stat-card h3 {
    font-size: 2rem;
    margin: 0 0 0.5rem 0;
}

#projekt-liste {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1rem;
}

.projekt-card {
    background: #f5f5f5;
    padding: 1rem;
    border-radius: 8px;
    border-left: 4px solid #0066CC;
}

.projekt-card.status-gut { border-left-color: #00C9A7; }
.projekt-card.status-mittel { border-left-color: #FF6B35; }
.projekt-card.status-niedrig { border-left-color: #FF0000; }

.fortschritt-bar {
    height: 8px;
    background: linear-gradient(90deg, #0066CC, #00C9A7);
    border-radius: 4px;
}
```

---

## Erfolgskriterien

- [ ] `dashboard.js` ist erstellt mit mindestens 5 Projekten
- [ ] Haupt-Statistiken werden berechnet (Status, Zeit, Fortschritt)
- [ ] Technologie-Analyse mit Zählung und Visualisierung
- [ ] Mehrere Filter-Funktionen implementiert
- [ ] Zeitmanagement mit Prognosen funktioniert
- [ ] Zielerreichungs-Tracker mit Motivations-System
- [ ] Dashboard wird im HTML mit Karten angezeigt
- [ ] CSS-Styling für professionelles Aussehen
- [ ] Verschachtelte Schleifen und komplexe Bedingungen genutzt
- [ ] Keine Fehler in der Konsole

---

## Tipps

- **Datenstruktur planen:** Überlege dir VOR dem Coden, welche Daten du brauchst
- **Kleine Schritte:** Teste jede Funktion einzeln, bevor du sie kombinierst
- **console.log() intensiv nutzen:** Bei komplexen Berechnungen Zwischenergebnisse ausgeben
- **Copy-Paste vermeiden:** Wenn du Code 3x wiederholst → Schleife oder Funktion nutzen (kommt später)
- **CSS separat:** Erst Logik programmieren, dann Styling
- **Performance:** Bei vielen Projekten (>100) optimiere mit `break` in Schleifen

---

## Weiterführende Links

- [JavaScript Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Sorting Algorithms Explained](https://www.freecodecamp.org/news/sorting-algorithms-explained/)
- [Dashboard Design Best Practices](https://www.interaction-design.org/literature/article/dashboard-design-best-practices)
- [Advanced JavaScript Patterns](https://www.patterns.dev/)

---

**Geschätzte Zeit:** 130 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Gratulation!** Du beherrschst jetzt die Grundlagen von JavaScript-Programmierung!
