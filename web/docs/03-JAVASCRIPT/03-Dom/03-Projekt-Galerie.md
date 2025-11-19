# Auftrag 3: Dynamische Projekt-Galerie mit Filter

## Ziel

Du erstellst eine dynamische Projekt-Galerie, die per JavaScript gefiltert und sortiert werden kann. Das ist die Grundlage für viele moderne Web-Interfaces wie Online-Shops oder Portfolio-Seiten.

## Beschreibung

Statische HTML-Listen sind begrenzt. Mit JavaScript kannst du Inhalte dynamisch filtern, sortieren und durchsuchen – ohne die Seite neu zu laden. In diesem Auftrag erstellst du eine Projekt-Galerie mit mehreren Projekten. Der Benutzer kann nach Technologie filtern, Projekte sortieren und suchen.

Das ist ein typisches Praxisbeispiel für DOM-Manipulation in professionellen Web-Apps.

---

## Teil 1: HTML-Struktur für Projekt-Galerie (10 Min)

Erstelle eine neue Sektion für deine Projekte:

```html
<section id="projekt-galerie">
    <h2>Meine Projekte</h2>
    
    <!-- Filter & Such-Funktionen -->
    <div class="filter-leiste">
        <div class="filter-gruppe">
            <label for="tech-filter">Filtern nach Technologie:</label>
            <select id="tech-filter">
                <option value="alle">Alle Technologien</option>
                <option value="html">HTML</option>
                <option value="css">CSS</option>
                <option value="javascript">JavaScript</option>
                <option value="react">React</option>
            </select>
        </div>
        
        <div class="filter-gruppe">
            <label for="status-filter">Filtern nach Status:</label>
            <select id="status-filter">
                <option value="alle">Alle Status</option>
                <option value="abgeschlossen">Abgeschlossen</option>
                <option value="in-arbeit">In Arbeit</option>
                <option value="geplant">Geplant</option>
            </select>
        </div>
        
        <div class="filter-gruppe">
            <label for="sortierung">Sortieren:</label>
            <select id="sortierung">
                <option value="datum-neu">Neueste zuerst</option>
                <option value="datum-alt">Älteste zuerst</option>
                <option value="name-az">Name A-Z</option>
                <option value="name-za">Name Z-A</option>
            </select>
        </div>
        
        <div class="filter-gruppe">
            <label for="projekt-suche">Suchen:</label>
            <input type="text" id="projekt-suche" placeholder="Projekt suchen...">
        </div>
    </div>
    
    <!-- Statistik-Anzeige -->
    <div id="projekt-statistik">
        <p>Zeige <strong id="anzahl-sichtbar">0</strong> von <strong id="anzahl-gesamt">0</strong> Projekten</p>
    </div>
    
    <!-- Projekt-Container (wird per JavaScript gefüllt) -->
    <div id="projekt-container" class="projekt-grid">
        <!-- Projekte werden hier dynamisch eingefügt -->
    </div>
    
    <p id="keine-projekte" class="meldung versteckt">
        Keine Projekte gefunden mit den aktuellen Filtern.
    </p>
</section>
```

---

## Teil 2: CSS für Projekt-Galerie (15 Min)

**Deine Aufgabe:**
Erstelle CSS für die Projekt-Galerie mit folgenden Komponenten:

1. **Filter-Leiste** (`.filter-leiste`)
    - Grid-Layout mit responsive Spalten
    - Heller Hintergrund, Padding, abgerundete Ecken

2. **Filter-Gruppen** (`.filter-gruppe`)
    - Flexbox-Layout (vertikal)
    - Label und Input/Select sauber gestapelt

3. **Projekt-Grid** (`.projekt-grid`)
    - CSS Grid mit automatischen Spalten (min. 300px)
    - Responsive Gap zwischen Karten

4. **Projekt-Karte** (`.projekt-karte`)
    - Weisser Hintergrund, Border, Shadow
    - Hover-Effekt: Border-Farbe ändern, hochschweben
    - Transition-Animationen

5. **Status-Badges** (`.projekt-status`)
    - Verschiedene Farben je nach Status-Klasse
    - `.status-abgeschlossen` → grün
    - `.status-in-arbeit` → gelb/orange
    - `.status-geplant` → blau

6. **Tech-Badges** (`.tech-badge`)
    - Kleine Pills mit hellblauem Hintergrund

**Wo nachschlagen:**
- [MDN: CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout)
- [CSS-Tricks: A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [MDN: CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions)
- [MDN: transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

**Hinweise:**
- Nutze `grid-template-columns: repeat(auto-fill, minmax(300px, 1fr))` für responsive Grid
- Hover-Effekt mit `transform: translateY(-5px)`
- Transitions für smooth animations

<details>
<summary>💡 CSS-Grundstruktur anzeigen</summary>

```css
/* Filter-Leiste */
.filter-leiste {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    /* ... weitere Styles */
}

/* Projekt-Grid */
.projekt-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 25px;
}

/* Projekt-Karte mit Hover */
.projekt-karte {
    transition: all 0.3s ease;
}

.projekt-karte:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 102, 204, 0.15);
}
```
</details>

---

## Teil 3: JavaScript-Datenstruktur (15 Min)

Erstelle `projekte.js`.

### Aufgabe 3.1: Projekt-Daten definieren

**Deine Aufgabe:**
Erstelle ein Array `projekte` mit mindestens 6 Projekt-Objekten. Jedes Projekt sollte haben:
- `id` (Nummer)
- `name` (String)
- `beschreibung` (String)
- `technologien` (Array von Strings: "html", "css", "javascript", etc.)
- `status` (String: "abgeschlossen", "in-arbeit", oder "geplant")
- `startdatum` (String im Format "YYYY-MM-DD")
- `dauer` (String z.B. "2 Wochen")

**Wo nachschlagen:**
- [MDN: Array](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: Objects](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object)

**Tipp:** Nutze deine echten Lern-Projekte! Z.B.:
- HTML Grundlagen
- CSS Layouts
- JavaScript Basics
- Portfolio-Website
- Eigene Projekt-Ideen

<details>
<summary>💡 Beispiel-Struktur anzeigen</summary>

```javascript
console.log("📁 Projekt-Galerie geladen");

const projekte = [
    {
        id: 1,
        name: "Portfolio-Website",
        beschreibung: "Meine persönliche Portfolio-Seite mit HTML, CSS und JavaScript.",
        technologien: ["html", "css", "javascript"],
        status: "in-arbeit",
        startdatum: "2025-01-01",
        dauer: "4 Wochen"
    },
    {
        id: 2,
        name: "HTML Grundlagen",
        beschreibung: "Erste Schritte in HTML: Struktur, Semantik, Formulare.",
        technologien: ["html"],
        status: "abgeschlossen",
        startdatum: "2024-09-01",
        dauer: "2 Wochen"
    },
    // ... mindestens 4 weitere Projekte
];
```
</details>

### Aufgabe 3.2: Projekte anzeigen

**Deine Aufgabe:**
Erstelle eine Funktion `zeigeProjekte(projekteListe)`, die:
1. Den Container leert
2. Für jedes Projekt eine Karte erstellt mit:
    - Projekt-Name als `<h3>`
    - Status-Badge mit entsprechender Klasse
    - Beschreibung als `<p>`
    - Tech-Badges für jede Technologie
    - Meta-Informationen (Datum, Dauer)
3. Die Karten mit Animation einblendet
4. Statistik aktualisiert (Anzahl sichtbar / gesamt)

**Wo nachschlagen:**
- [MDN: createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
- [MDN: innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
- [MDN: appendChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
- [MDN: forEach](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN: Date](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date)

**Hinweise:**
- Erstelle für jedes Projekt ein `<div class="projekt-karte">`
- Nutze Template Literals für dynamisches HTML
- Füge Animationen mit `setTimeout()` hinzu
- Formatiere das Datum schön (z.B. "15. Jan 2025")

**Struktur einer Karte:**
```html
<div class="projekt-karte" data-status="..." data-technologien="...">
    <h3>Projekt-Name</h3>
    <span class="projekt-status status-...">Status</span>
    <p class="projekt-beschreibung">Beschreibung</p>
    <div class="projekt-technologien">
        <span class="tech-badge">HTML</span>
        ...
    </div>
    <div class="projekt-meta">
        <span>📅 Start: ...</span>
        <span>⏱️ Dauer</span>
    </div>
</div>
```

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function zeigeProjekte(projekteListe) {
    let container = document.getElementById("projekt-container");
    let keineProjekteMeldung = document.getElementById("keine-projekte");
    
    // Container leeren
    container.innerHTML = "";
    
    // Statistik aktualisieren
    document.getElementById("anzahl-sichtbar").textContent = projekteListe.length;
    document.getElementById("anzahl-gesamt").textContent = projekte.length;
    
    // Keine Projekte?
    if (projekteListe.length === 0) {
        keineProjekteMeldung.classList.remove("versteckt");
        return;
    } else {
        keineProjekteMeldung.classList.add("versteckt");
    }
    
    // Karten erstellen
    projekteListe.forEach(function(projekt, index) {
        let karte = document.createElement("div");
        karte.className = "projekt-karte";
        karte.setAttribute("data-status", projekt.status);
        karte.setAttribute("data-technologien", projekt.technologien.join(","));
        
        // Status-Klasse
        let statusKlasse = `status-${projekt.status}`;
        let statusText = projekt.status === "abgeschlossen" ? "✅ Abgeschlossen" :
                        projekt.status === "in-arbeit" ? "🚧 In Arbeit" :
                        "📅 Geplant";
        
        // Tech-Badges
        let techBadges = "";
        projekt.technologien.forEach(function(tech) {
            techBadges += `<span class="tech-badge">${tech.toUpperCase()}</span>`;
        });
        
        // Datum formatieren
        let datum = new Date(projekt.startdatum);
        let monate = ["Jan", "Feb", "Mär", "Apr", "Mai", "Jun", 
                      "Jul", "Aug", "Sep", "Okt", "Nov", "Dez"];
        let formatDatum = `${datum.getDate()}. ${monate[datum.getMonth()]} ${datum.getFullYear()}`;
        
        // Karten-Inhalt
        karte.innerHTML = `
            <h3>${projekt.name}</h3>
            <span class="projekt-status ${statusKlasse}">${statusText}</span>
            <p class="projekt-beschreibung">${projekt.beschreibung}</p>
            <div class="projekt-technologien">${techBadges}</div>
            <div class="projekt-meta">
                <span>📅 Start: ${formatDatum}</span>
                <span>⏱️ ${projekt.dauer}</span>
            </div>
        `;
        
        // Animation
        karte.style.opacity = "0";
        karte.style.transform = "scale(0.8)";
        container.appendChild(karte);
        
        setTimeout(function() {
            karte.style.transition = "all 0.3s ease";
            karte.style.opacity = "1";
            karte.style.transform = "scale(1)";
        }, index * 50);
    });
    
    console.log(`📊 ${projekteListe.length} Projekte angezeigt`);
}

// Initial alle Projekte anzeigen
zeigeProjekte(projekte);
```
</details>

---

## Teil 4: Filter-Funktionen (30 Min)

### Aufgabe 4.1: Filter-State verwalten

**Deine Aufgabe:**
Erstelle ein Objekt `aktuelleFilter` das den aktuellen Filter-Zustand speichert:
- `technologie`
- `status`
- `suchbegriff`
- `sortierung`

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
let aktuelleFilter = {
    technologie: "alle",
    status: "alle",
    suchbegriff: "",
    sortierung: "datum-neu"
};
```
</details>

### Aufgabe 4.2: Event-Listener für Filter

**Deine Aufgabe:**
Füge Event-Listener für alle Filter-Elemente hinzu:
1. Technologie-Filter (`#tech-filter`)
2. Status-Filter (`#status-filter`)
3. Such-Input (`#projekt-suche`)
4. Sortierung (`#sortierung`)

Jeder Listener sollte:
- Den `aktuelleFilter` aktualisieren
- Eine Funktion `wendeFilterAn()` aufrufen

**Wo nachschlagen:**
- [MDN: change event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event)
- [MDN: input event](https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event)
- [MDN: Event.target](https://developer.mozilla.org/en-US/docs/Web/API/Event/target)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
document.getElementById("tech-filter").addEventListener("change", function() {
    aktuelleFilter.technologie = this.value;
    console.log("🔍 Filtern nach Technologie:", this.value);
    wendeFilterAn();
});

document.getElementById("status-filter").addEventListener("change", function() {
    aktuelleFilter.status = this.value;
    console.log("🔍 Filtern nach Status:", this.value);
    wendeFilterAn();
});

document.getElementById("projekt-suche").addEventListener("input", function() {
    aktuelleFilter.suchbegriff = this.value.toLowerCase();
    console.log("🔍 Suche:", this.value);
    wendeFilterAn();
});

document.getElementById("sortierung").addEventListener("change", function() {
    aktuelleFilter.sortierung = this.value;
    console.log("↕️ Sortiere:", this.value);
    wendeFilterAn();
});
```
</details>

### Aufgabe 4.3: Filter anwenden

**Deine Aufgabe:**
Erstelle die Funktion `wendeFilterAn()`, die:
1. Eine Kopie des `projekte` Arrays erstellt
2. Nach Technologie filtert (wenn nicht "alle")
3. Nach Status filtert (wenn nicht "alle")
4. Nach Suchbegriff filtert (Name ODER Beschreibung)
5. Die gefilterten Projekte sortiert
6. Die gefilterten Projekte anzeigt

**Wo nachschlagen:**
- [MDN: Array.filter()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [MDN: Array.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
- [MDN: String.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)
- [MDN: String.toLowerCase()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
- [MDN: Spread Syntax](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

**Hinweise:**
- Nutze `[...projekte]` für eine Kopie (Spread-Operator)
- `Array.filter()` gibt ein neues Array zurück
- Verkette mehrere `.filter()` Aufrufe
- Nutze `.includes()` um zu prüfen ob ein Element im Array ist

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function wendeFilterAn() {
    // Kopie der Projekt-Liste
    let gefiltert = [...projekte];
    
    // 1. Nach Technologie filtern
    if (aktuelleFilter.technologie !== "alle") {
        gefiltert = gefiltert.filter(function(projekt) {
            return projekt.technologien.includes(aktuelleFilter.technologie);
        });
    }
    
    // 2. Nach Status filtern
    if (aktuelleFilter.status !== "alle") {
        gefiltert = gefiltert.filter(function(projekt) {
            return projekt.status === aktuelleFilter.status;
        });
    }
    
    // 3. Nach Suchbegriff filtern
    if (aktuelleFilter.suchbegriff !== "") {
        gefiltert = gefiltert.filter(function(projekt) {
            let name = projekt.name.toLowerCase();
            let beschreibung = projekt.beschreibung.toLowerCase();
            return name.includes(aktuelleFilter.suchbegriff) || 
                   beschreibung.includes(aktuelleFilter.suchbegriff);
        });
    }
    
    // 4. Sortieren
    gefiltert = sortiereProjekte(gefiltert, aktuelleFilter.sortierung);
    
    // Gefilterte Projekte anzeigen
    zeigeProjekte(gefiltert);
}
```
</details>

### Aufgabe 4.4: Sortier-Funktion

**Deine Aufgabe:**
Erstelle die Funktion `sortiereProjekte(liste, sortierung)`, die je nach Sortierung:
- `"datum-neu"` → Neueste zuerst (Datum absteigend)
- `"datum-alt"` → Älteste zuerst (Datum aufsteigend)
- `"name-az"` → Alphabetisch A-Z
- `"name-za"` → Alphabetisch Z-A

**Wo nachschlagen:**
- [MDN: Array.sort()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [MDN: String.localeCompare()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)
- [MDN: switch](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/switch)

**Hinweise:**
- `Array.sort()` braucht eine Vergleichsfunktion
- Für Datum: `new Date(a.startdatum) - new Date(b.startdatum)`
- Für Strings: `a.name.localeCompare(b.name)`
- Nutze `switch` für verschiedene Sortierungen

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function sortiereProjekte(liste, sortierung) {
    let sortiert = [...liste];
    
    switch(sortierung) {
        case "datum-neu":
            sortiert.sort(function(a, b) {
                return new Date(b.startdatum) - new Date(a.startdatum);
            });
            break;
            
        case "datum-alt":
            sortiert.sort(function(a, b) {
                return new Date(a.startdatum) - new Date(b.startdatum);
            });
            break;
            
        case "name-az":
            sortiert.sort(function(a, b) {
                return a.name.localeCompare(b.name);
            });
            break;
            
        case "name-za":
            sortiert.sort(function(a, b) {
                return b.name.localeCompare(a.name);
            });
            break;
    }
    
    return sortiert;
}
```
</details>

---

## Teil 5: Statistiken (Optional, 15 Min)

### Aufgabe 5.1: Statistik-Funktion

**Deine Aufgabe:**
Erstelle eine Funktion `berechneStatistiken()`, die zurückgibt:
- Gesamtzahl Projekte
- Anzahl abgeschlossene Projekte
- Anzahl Projekte in Arbeit
- Anzahl geplante Projekte
- Anzahl Projekte pro Technologie

**Wo nachschlagen:**
- [JavaScript.info: Objects](https://javascript.info/object)
- [MDN: for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

**Hinweise:**
- Nutze ein Objekt um Technologien zu zählen
- Iteriere über alle Projekte und zähle hoch

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function berechneStatistiken() {
    let stats = {
        gesamt: projekte.length,
        abgeschlossen: 0,
        inArbeit: 0,
        geplant: 0,
        technologien: {}
    };
    
    projekte.forEach(function(projekt) {
        // Status zählen
        if (projekt.status === "abgeschlossen") stats.abgeschlossen++;
        if (projekt.status === "in-arbeit") stats.inArbeit++;
        if (projekt.status === "geplant") stats.geplant++;
        
        // Technologien zählen
        projekt.technologien.forEach(function(tech) {
            if (!stats.technologien[tech]) {
                stats.technologien[tech] = 0;
            }
            stats.technologien[tech]++;
        });
    });
    
    return stats;
}

// Statistik-Übersicht in Konsole anzeigen
function zeigeStatistikUebersicht() {
    let stats = berechneStatistiken();
    
    console.log("\n=== PROJEKT-STATISTIKEN ===");
    console.log("Gesamt:", stats.gesamt);
    console.log("Abgeschlossen:", stats.abgeschlossen);
    console.log("In Arbeit:", stats.inArbeit);
    console.log("Geplant:", stats.geplant);
    console.log("\nTechnologien:");
    for (let tech in stats.technologien) {
        console.log(`  ${tech.toUpperCase()}: ${stats.technologien[tech]} Projekte`);
    }
}

zeigeStatistikUebersicht();
```
</details>

---

## Erfolgskriterien

- [ ] Projekt-Galerie-Sektion in HTML eingefügt
- [ ] CSS für Karten, Filter und Animationen vorhanden
- [ ] `projekte.js` mit mindestens 6 Projekten erstellt
- [ ] Projekte werden als Karten angezeigt
- [ ] Technologie-Filter funktioniert
- [ ] Status-Filter funktioniert
- [ ] Suchfunktion funktioniert (Name & Beschreibung)
- [ ] Sortierung funktioniert (Datum & Name)
- [ ] Statistik zeigt korrekte Anzahl
- [ ] Animation beim Einblenden der Karten
- [ ] "Keine Projekte"-Meldung bei leerem Ergebnis

---

## Tipps & Troubleshooting

### Häufige Fehler:
- **Filter funktioniert nicht?** → Prüfe ob Event-Listener korrekt sind
- **Sortierung ändert sich nicht?** → Prüfe ob `sortiereProjekte()` aufgerufen wird
- **Keine Projekte sichtbar?** → Prüfe die Konsole auf Fehler
- **Suche findet nichts?** → Prüfe ob `.toLowerCase()` verwendet wird

### Performance-Tipp:
Bei sehr vielen Projekten (100+) solltest du **Debouncing** für die Suche einsetzen, damit nicht bei jedem Tastendruck gefiltert wird.

**Wo nachschlagen:**
- [CSS-Tricks: Debouncing](https://css-tricks.com/debouncing-throttling-explained-examples/)
- [Lodash: debounce](https://lodash.com/docs/#debounce)

### Wichtige Konzepte:
- **Array.filter():** Erstellt neues Array mit gefilterten Elementen
- **Array.sort():** Sortiert Array (verändert Original!)
- **Spread-Operator [...]:** Erstellt Kopie eines Arrays
- **Template Literals:** Für dynamisches HTML

---

## Reflexionsfragen

1. **Warum erstellen wir eine Kopie mit `[...projekte]` bevor wir filtern?**  
   *Was würde passieren, wenn wir direkt `projekte.filter()` nutzen?*

2. **Wie funktioniert die `sort()`-Funktion mit einer Vergleichsfunktion?**  
   *Was bedeuten die Rückgabewerte -1, 0 und 1?*

3. **Könntest du einen weiteren Filter hinzufügen, z.B. nach Dauer?**  
   *Welche Schritte wären nötig? (HTML, Event-Listener, Filter-Logik)*

4. **Die Projekte sind hardcoded im JavaScript. Wie könnte man sie aus einer JSON-Datei laden?**  
   *Recherchiere: fetch() API.*

5. **Bonus: Wie könnte man neue Projekte per Formular hinzufügen?**  
   *Welche Funktionen bräuchtest du? Wo würdest du die Daten speichern?*

---

## Weiterführende Links

**Array-Methoden:**
- [MDN: Array.filter()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [MDN: Array.sort()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [JavaScript.info: Array Methods](https://javascript.info/array-methods)

**Fortgeschrittene Konzepte:**
- [Debouncing & Throttling](https://css-tricks.com/debouncing-throttling-explained-examples/)
- [MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) - Für externe Daten

**Best Practices:**
- [Google: Rendering Performance](https://web.dev/rendering-performance/)
- [MDN: Performance](https://developer.mozilla.org/en-US/docs/Learn/Performance)

---

**⏱️ Geschätzte Zeit:** 90 Minuten  
**📦 Nächster Schritt:** Auftrag 4 (Optional) – Theme-Switcher mit Animation