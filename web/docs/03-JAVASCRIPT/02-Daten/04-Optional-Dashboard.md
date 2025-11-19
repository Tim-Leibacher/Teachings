# Optional: Interaktives Portfolio-Dashboard

## Ziel

Du kombinierst alle erlernten Konzepte (Variablen, Datentypen, if-else, Schleifen) in einem fortgeschrittenen Projekt: Ein interaktives Portfolio-Dashboard mit Projektverwaltung, Zielerreichung, Statistiken und dynamischen Filtern. Dieser Auftrag ist anspruchsvoller und zeigt dir, wie professionelle Entwickler komplexe Funktionen aufbauen.

## Beschreibung

In diesem Vertiefungsauftrag erstellst du ein Dashboard für dein Portfolio, das verschiedene Metriken verfolgt: abgeschlossene Projekte, Lernfortschritt, Zeitinvestment und Ziele. Du nutzt komplexe Datenstrukturen (Arrays von Objekten), verschachtelte Schleifen, mehrfache Bedingungen und berechnest automatisch Statistiken.

**Wichtig:** Dieser Auftrag ist deutlich anspruchsvoller als die vorherigen! Er kombiniert alle bisherigen Konzepte und erfordert selbstständiges Problemlösen. Nimm dir Zeit und arbeite schrittweise.

---

### Teil 1: Projekt-Datenstruktur aufbauen (25 Min)

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

// TODO 1.1: Erstelle ein Array mit mindestens 6 Projekten
// Jedes Projekt ist ein Objekt mit folgenden Properties:
// - id (Zahl)
// - titel (String)
// - kategorie (String: "Webentwicklung", "Lernen", "Projekt")
// - technologien (Array von Strings)
// - status (String: "Abgeschlossen", "In Arbeit", "Geplant")
// - fortschritt (Zahl 0-100)
// - startDatum (String im Format "YYYY-MM-DD")
// - geplantesEnde (String im Format "YYYY-MM-DD")
// - zeitInvestiert (Zahl: Stunden)
// - schwierigkeit (String: "Einfach", "Mittel", "Schwer")
// - prioritaet (String: "Niedrig", "Mittel", "Hoch")

// Hier ist EIN Beispiel-Projekt:
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
        zeitInvestiert: 45,
        schwierigkeit: "Mittel",
        prioritaet: "Hoch"
    },
    // TODO: Füge hier mindestens 5 weitere Projekte hinzu
    // Variiere Status, Fortschritt, Schwierigkeit
    // Mindestens 2x "Abgeschlossen", 3x "In Arbeit", 1x "Geplant"
    
];

console.log(`Gesamtanzahl Projekte: ${projekte.length}\n`);
```

**Lernziele:**
- Komplexe Datenstrukturen selbst erstellen
- Arrays in Objekten nutzen
- Realistische Daten planen

**Wichtig:** Nimm dir Zeit für sinnvolle Projektdaten! Sie sind die Basis für alle Berechnungen.

---

### Teil 2: Dashboard-Statistiken berechnen (30 Min)

```javascript
// === HAUPT-STATISTIKEN ===

console.log("=== STATISTIKEN ===\n");

// TODO 2.1: Initialisiere Zähler für verschiedene Status
let anzahlAbgeschlossen = 0;
let anzahlInArbeit = 0;
let anzahlGeplant = 0;

// TODO 2.2: Initialisiere Akkumulatoren für Summen
let gesamtZeit = 0;
let gesamtFortschritt = 0;


// TODO 2.3: Durchlaufe alle Projekte und zähle Status
// Für jedes Projekt:
// - Prüfe status und erhöhe entsprechenden Zähler
// - Addiere zeitInvestiert zu gesamtZeit
// - Addiere fortschritt zu gesamtFortschritt

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // Deine Lösung hier:
    
}


// TODO 2.4: Berechne Durchschnittswerte
const durchschnittFortschritt = // Math.round(gesamtFortschritt / projekte.length)


// TODO 2.5: Gib formatierte Statistiken aus
console.log("STATUS-VERTEILUNG:");
console.log(`  Abgeschlossen: ${anzahlAbgeschlossen}`);
// Weitere Ausgaben...

console.log("\nZEITINVESTMENT:");
// Deine Ausgaben hier...

console.log("\nFORTSCHRITT:");
// Deine Ausgaben hier...

console.log("");


// === TECHNOLOGIE-ANALYSE ===

console.log("=== TECHNOLOGIE-ANALYSE ===\n");

// TODO 2.6: Zähle, wie oft jede Technologie vorkommt
// Nutze ein Objekt als "Dictionary": { "HTML": 3, "CSS": 2, ... }
// Dokumentation Objekte: https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Working_with_Objects

let technologieCount = {};

// TODO 2.7: Durchlaufe alle Projekte
for (let i = 0; i < projekte.length; i++) {
    const technologien = projekte[i].technologien;
    
    // TODO 2.8: Durchlaufe alle Technologien des Projekts (verschachtelte Schleife!)
    for (let j = 0; j < technologien.length; j++) {
        const tech = technologien[j];
        
        // TODO 2.9: Zähle Technologie
        // Wenn tech schon in technologieCount existiert: Erhöhe um 1
        // Sonst: Setze auf 1
        // Tipp: if (technologieCount[tech]) { ... } else { ... }
        
        // Deine Lösung hier:
        
    }
}


// TODO 2.10: Gib Technologie-Statistik aus
// Nutze Object.keys(technologieCount) um alle Technologien zu holen
// Dokumentation Object.keys: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object/keys

console.log("TECHNOLOGIE-NUTZUNG:");

const techKeys = // Object.keys(...)

for (let i = 0; i < techKeys.length; i++) {
    const tech = techKeys[i];
    const anzahl = technologieCount[tech];
    const prozent = Math.round((anzahl / projekte.length) * 100);
    
    // TODO 2.11: Erstelle visuellen Balken
    let balken = "";
    for (let j = 0; j < anzahl; j++) {
        balken += "█";
    }
    
    console.log(`  ${tech.padEnd(12)} ${balken} ${anzahl}x (${prozent}%)`);
}

console.log("");
```

**Lernziele:**
- Mehrere Zähler parallel führen
- Verschachtelte Schleifen für komplexe Daten
- Objekte als "Dictionary" nutzen
- Object.keys() verstehen

**Debugging-Tipp:** Nutze `console.log()` nach jeder Berechnung, um Zwischenergebnisse zu prüfen!

---

### Teil 3: Projekt-Filter und Suche (25 Min)

```javascript
// === PROJEKT-FILTER ===

console.log("=== PROJEKT-FILTER ===\n");

// TODO 3.1: Filter 1 - Aktive Projekte mit hoher Priorität
console.log("AKTIVE PROJEKTE MIT HOHER PRIORITÄT:");

let gefiltert = 0;

// TODO 3.2: Durchlaufe alle Projekte
// Zeige nur Projekte mit status "In Arbeit" UND prioritaet "Hoch"

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    if (/* Deine Bedingung: status === "In Arbeit" && prioritaet === "Hoch" */) {
        console.log(`  ${projekt.id}. ${projekt.titel} (${projekt.fortschritt}%)`);
        gefiltert++;
    }
}

console.log(`  → ${gefiltert} Projekte gefunden\n`);


// TODO 3.3: Filter 2 - Projekte mit Verzögerung
console.log("PROJEKTE MIT VERZÖGERUNG (<50%):");

gefiltert = 0;

// TODO 3.4: Zeige Projekte mit status "In Arbeit" UND fortschritt < 50

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    if (/* Deine Bedingung */) {
        const differenz = // 50 - projekt.fortschritt
        console.log(`  ⚠️  ${projekt.titel}: ${projekt.fortschritt}% (${differenz}% hinter Plan)`);
        gefiltert++;
    }
}

// TODO 3.5: Wenn keine gefunden, positive Nachricht
if (gefiltert === 0) {
    console.log("  ✓ Alle Projekte im Plan!");
}

console.log("");


// TODO 3.6: Filter 3 - Nach Technologie suchen
const gesuchte_Technologie = "JavaScript";  // Ändere nach Bedarf

console.log(`PROJEKTE MIT ${gesuchte_Technologie.toUpperCase()}:`);

gefiltert = 0;

// TODO 3.7: Durchlaufe alle Projekte
for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // TODO 3.8: Prüfe, ob Technologie im technologien-Array enthalten ist
    // Nutze projekt.technologien.includes(gesuchte_Technologie)
    // Dokumentation includes: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/includes
    
    if (/* Deine Bedingung */) {
        console.log(`  - ${projekt.titel} (${projekt.status})`);
        gefiltert++;
    }
}

console.log(`  → ${gefiltert} Projekte gefunden\n`);
```

**Lernziele:**
- Komplexe Filter-Bedingungen mit && und ||
- .includes() für Array-Suche nutzen
- Verschiedene Filter kombinieren

---

### Teil 4: Zeitmanagement und Prognosen (30 Min)

```javascript
// === ZEITMANAGEMENT ===

console.log("=== ZEITMANAGEMENT ===\n");

// TODO 4.1: Finde Projekte, die im aktuellen Monat enden
// Aktueller Monat: November 2025 (2025-11)
const aktuellerMonat = "2025-11";

console.log(`PROJEKTE MIT DEADLINE IM ${aktuellerMonat}:`);

let anzahlDeadlines = 0;

// TODO 4.2: Durchlaufe alle Projekte
for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // TODO 4.3: Prüfe, ob geplantesEnde mit aktuellerMonat beginnt
    // Nutze projekt.geplantesEnde.startsWith(aktuellerMonat)
    // Dokumentation startsWith: https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith
    
    if (/* Deine Bedingung */) {
        // TODO 4.4: Berechne verbleibenden Fortschritt
        const verbleibend = // 100 - projekt.fortschritt
        
        // TODO 4.5: Schätze benötigte Stunden
        // Annahme: Gleiche Stunden-pro-Prozent wie bisher
        // stundenProProzent = zeitInvestiert / fortschritt
        // benoetigteStunden = verbleibend * stundenProProzent
        
        let benoetigteStunden = 0;
        if (projekt.fortschritt > 0) {
            const stundenProProzent = projekt.zeitInvestiert / projekt.fortschritt;
            benoetigteStunden = Math.round(verbleibend * stundenProProzent);
        }
        
        console.log(`  ⏰ ${projekt.titel}: ${projekt.fortschritt}% → 100% (ca. ${benoetigteStunden}h)`);
        anzahlDeadlines++;
    }
}

if (anzahlDeadlines === 0) {
    console.log("  ✓ Keine Deadlines in diesem Monat");
}

console.log("");


// TODO 4.6: Berechne Gesamtprognose für alle "In Arbeit" Projekte
console.log("PROGNOSE FÜR ALLE LAUFENDEN PROJEKTE:");

let gesamtBenoetigteStunden = 0;

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // TODO 4.7: Nur für Projekte "In Arbeit"
    if (/* status === "In Arbeit" */) {
        const verbleibend = // Deine Berechnung
        
        if (projekt.fortschritt > 0) {
            const stundenProProzent = projekt.zeitInvestiert / projekt.fortschritt;
            const benoetigteStunden = Math.round(verbleibend * stundenProProzent);
            gesamtBenoetigteStunden += benoetigteStunden;
        }
    }
}

console.log(`Geschätzte Gesamtzeit bis Fertigstellung: ${gesamtBenoetigteStunden}h`);
console.log(`Bei 10h/Woche: ca. ${Math.round(gesamtBenoetigteStunden / 10)} Wochen\n`);
```

**Lernziele:**
- String-Methoden wie .startsWith() nutzen
- Berechnungen mit Division und Multiplikation
- Prognosen basierend auf historischen Daten

---

### Teil 5: Zielerreichungs-Tracker (25 Min)

```javascript
// === ZIELERREICHUNG ===

console.log("=== ZIELERREICHUNG ===\n");

// TODO 5.1: Definiere Monatsziel
const aktuellesZiel = {
    monat: "November 2025",
    zielProjekte: 2,     // 2 Projekte abschließen
    zielStunden: 40      // 40 Stunden investieren
};

console.log(`MONATSZIEL: ${aktuellesZiel.monat}`);
console.log(`Ziel: ${aktuellesZiel.zielProjekte} Projekte, ${aktuellesZiel.zielStunden}h\n`);


// TODO 5.2: Zähle abgeschlossene Projekte im November
let novemberProjekte = 0;
let novemberStunden = 0;

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // TODO 5.3: Prüfe, ob Projekt im November abgeschlossen wurde
    // (status === "Abgeschlossen" UND geplantesEnde enthält "2025-11")
    
    if (/* Deine Bedingung */) {
        novemberProjekte++;
        novemberStunden += projekt.zeitInvestiert;
    }
}


// TODO 5.4: Prüfe Projekt-Ziel
const projektErreicht = // novemberProjekte >= aktuellesZiel.zielProjekte
const projektFehlt = // aktuellesZiel.zielProjekte - novemberProjekte

if (projektErreicht) {
    console.log(`  ✅ Projekte: ${novemberProjekte}/${aktuellesZiel.zielProjekte} – Ziel erreicht!`);
} else {
    console.log(`  ⏳ Projekte: ${novemberProjekte}/${aktuellesZiel.zielProjekte} – Noch ${projektFehlt} benötigt`);
}


// TODO 5.5: Prüfe Stunden-Ziel
const stundenErreicht = // Deine Bedingung
const stundenFehlen = // Deine Berechnung

if (stundenErreicht) {
    console.log(`  ✅ Stunden: ${novemberStunden}/${aktuellesZiel.zielStunden}h – Ziel erreicht!`);
} else {
    const prozent = Math.round((novemberStunden / aktuellesZiel.zielStunden) * 100);
    console.log(`  ⏳ Stunden: ${novemberStunden}/${aktuellesZiel.zielStunden}h (${prozent}%) – Noch ${stundenFehlen}h`);
}

console.log("");


// TODO 5.6: Erstelle dynamische Motivations-Nachricht
let motivation = "";

// TODO 5.7: Verschiedene Fälle mit if-else-if
if (projektErreicht && stundenErreicht) {
    motivation = "🎉 Fantastisch! Beide Ziele erreicht!";
} else if (projektErreicht || stundenErreicht) {
    motivation = "👍 Gut im Plan! Ein Ziel erreicht, weitermachen!";
} else {
    // TODO 5.8: Berechne Gesamt-Prozent beider Ziele
    const gesamtProzent = Math.round(
        ((novemberProjekte / aktuellesZiel.zielProjekte) + 
         (novemberStunden / aktuellesZiel.zielStunden)) / 2 * 100
    );
    
    // TODO 5.9: Verschiedene Motivationen je nach Prozent
    if (gesamtProzent >= 75) {
        motivation = // Deine Nachricht
    } else if (gesamtProzent >= 50) {
        motivation = // Deine Nachricht
    } else {
        motivation = // Deine Nachricht
    }
}

console.log(motivation);
console.log("");
```

**Lernziele:**
- Komplexe verschachtelte Bedingungen
- Mehrere Metriken kombinieren
- Dynamische Nachrichten basierend auf Daten

---

### Teil 6: Dashboard im HTML anzeigen (35 Min)

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

// TODO 6.1: Erstelle Statistik-Karten
// 6 Karten: Gesamt, Abgeschlossen, In Arbeit, Zeitinvestment, Ø Fortschritt, Jahresziel
// Jede Karte hat class="stat-card" und zeigt eine Zahl + Beschreibung

const statsHTML = `
    <div class="stat-card">
        <h3>${projekte.length}</h3>
        <p>Gesamt Projekte</p>
    </div>
    <!-- TODO: Füge 5 weitere Karten hinzu -->
`;

// TODO 6.2: Füge ins DOM ein
// document.getElementById("dashboard-stats").innerHTML = statsHTML


// TODO 6.3: Erstelle Projekt-Karten für alle "In Arbeit" Projekte
let projekteHTML = "";

for (let i = 0; i < projekte.length; i++) {
    const projekt = projekte[i];
    
    // TODO 6.4: Nur Projekte "In Arbeit" anzeigen
    if (projekt.status !== "In Arbeit") {
        continue;  // Überspringt diesen Durchlauf
    }
    
    
    // TODO 6.5: Bestimme CSS-Klasse basierend auf Fortschritt
    let statusClass = "";
    if (projekt.fortschritt >= 75) {
        statusClass = "status-gut";
    } else if (/* fortschritt >= 50 */) {
        statusClass = "status-mittel";
    } else {
        statusClass = "status-niedrig";
    }
    
    
    // TODO 6.6: Erstelle HTML für Projekt-Karte
    // Inkludiere:
    // - Titel und Priorität
    // - Kategorie und Schwierigkeit
    // - Technologien (mit .map() oder Schleife)
    // - Fortschrittsbalken mit style="width: X%"
    // - Statistiken (Fortschritt, Zeit)
    
    projekteHTML += `
        <div class="projekt-card ${statusClass}">
            <!-- Dein HTML-Code hier -->
        </div>
    `;
}

// TODO 6.7: Füge ins DOM ein
// document.getElementById("projekt-liste").innerHTML = projekteHTML


// TODO 6.8: Erstelle Zielerreichungs-Box
// Zeige:
// - Monatsziel-Titel
// - Fortschrittsbalken für Projekte
// - Fortschrittsbalken für Stunden
// - Motivations-Nachricht

const zieleHTML = `
    <div class="ziele-box">
        <h3>Monatsziel ${aktuellesZiel.monat}</h3>
        <!-- Dein HTML-Code hier -->
        <p class="motivation">${motivation}</p>
    </div>
`;

// TODO 6.9: Füge ins DOM ein
// document.getElementById("dashboard-ziele").innerHTML = zieleHTML


console.log("✓ Dashboard im HTML angezeigt");
```

**Optionales CSS** (in `styles.css`):

```css
/* TODO: Füge eigenes Styling hinzu oder nutze diese Vorlage */

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
```

---

## Erfolgskriterien

- [ ] Alle TODO-Aufgaben sind selbstständig gelöst
- [ ] Mindestens 6 Projekte mit vollständigen Daten erstellt
- [ ] Haupt-Statistiken werden korrekt berechnet
- [ ] Technologie-Analyse mit Zählung funktioniert
- [ ] Mindestens 3 verschiedene Filter implementiert
- [ ] Zeitmanagement mit Prognosen berechnet
- [ ] Zielerreichungs-Tracker mit Motivations-System
- [ ] Dashboard wird im HTML angezeigt
- [ ] Verschachtelte Schleifen und komplexe Bedingungen genutzt
- [ ] Code ist gut strukturiert und kommentiert
- [ ] Keine Fehler in der Konsole

---

## Tipps für selbstständiges Arbeiten

- **Datenstruktur ist fundamental:** Investiere Zeit in sinnvolle Projekt-Daten
- **Kleine Schritte:** Teste jede Funktion einzeln
- **console.log() überall:** Bei komplexen Berechnungen Zwischenergebnisse ausgeben
- **MDN ist dein Freund:** Bei jeder neuen Methode nachschlagen
- **Break-Points nutzen:** Im Browser DevTools kannst du Code anhalten
- **Erst Logik, dann Design:** Fokussiere auf funktionierende Berechnungen
- **Zeit einplanen:** Dieser Auftrag braucht 3-4 Stunden!

---

## Reflexionsfragen

1. **Welche Datenstruktur hast du gewählt und warum?**  
   *Array von Objekten vs. Objekt mit Arrays?*

2. **Wo hast du verschachtelte Schleifen genutzt?**  
   *Wie viele Durchläufe hatte die innere Schleife?*

3. **Welche Filter-Bedingung war am komplexesten?**  
   *Wie viele && oder || Operatoren hast du kombiniert?*

4. **Wie hast du Prognosen berechnet?**  
   *Welche Annahmen hast du getroffen?*

5. **Was würdest du anders machen, wenn du das Dashboard neu baust?**  
   *Welche Funktionen würdest du extrahieren?*

---

## Weiterführende Links

**Pflichtlektüre:**
- [MDN: Objekte](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Working_with_Objects)
- [MDN: Array Methods Übersicht](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: Object.keys()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

**Vertiefung:**
- [JavaScript.info: Objects](https://javascript.info/object)
- [JavaScript.info: Array Methods](https://javascript.info/array-methods)
- [Patterns.dev: JavaScript Patterns](https://www.patterns.dev/)

**Inspiration:**
- [Dashboard Design Best Practices](https://www.interaction-design.org/literature/article/dashboard-design-best-practices)
- [Data Visualization Guide](https://datavizcatalogue.com/)

---

**Geschätzte Zeit:** 170 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Gratulation!** Du beherrschst jetzt die Grundlagen von JavaScript-Programmierung!

## Nächste Schritte

Nach diesem Auftrag kannst du:
- Funktionen lernen (Code wiederverwenden)
- DOM-Manipulation vertiefen (Events, Interaktivität)
- Fetch API nutzen (externe Daten laden)
- Lokale Storage erweitern (Daten persistent speichern)
- Frameworks erkunden (React, Vue)