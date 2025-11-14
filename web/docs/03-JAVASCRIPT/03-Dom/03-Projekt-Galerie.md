# Auftrag 3: Dynamische Projekt-Galerie mit Filter

## Ziel

Du erstellst eine dynamische Projekt-Galerie, die per JavaScript gefiltert und sortiert werden kann. Das ist die Grundlage für viele moderne Web-Interfaces wie Online-Shops oder Portfolio-Seiten.

## Beschreibung

Statische HTML-Listen sind begrenzt. Mit JavaScript kannst du Inhalte dynamisch filtern, sortieren und durchsuchen – ohne die Seite neu zu laden. In diesem Auftrag erstellst du eine Projekt-Galerie mit mehreren Projekten. Der Benutzer kann nach Technologie filtern, Projekte sortieren und suchen.

Das ist ein typisches Praxisbeispiel für DOM-Manipulation in professionellen Web-Apps.

---

### Teil 1: HTML-Struktur für Projekt-Galerie (15 Min)

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

### Teil 2: CSS für Projekt-Galerie (10 Min)

Füge in `styles.css` hinzu:

```css
/* === PROJEKT-GALERIE === */
#projekt-galerie {
    padding: 40px 0;
}

/* Filter-Leiste */
.filter-leiste {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    margin-bottom: 30px;
}

.filter-gruppe {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.filter-gruppe label {
    font-weight: 600;
    color: #495057;
    font-size: 0.9em;
}

.filter-gruppe select,
.filter-gruppe input {
    padding: 10px;
    border: 2px solid #dee2e6;
    border-radius: 4px;
    font-size: 1em;
    transition: border-color 0.2s ease;
}

.filter-gruppe select:focus,
.filter-gruppe input:focus {
    outline: none;
    border-color: #0066cc;
}

/* Statistik */
#projekt-statistik {
    background: #e7f5ff;
    padding: 15px;
    border-radius: 6px;
    border-left: 4px solid #0066cc;
    margin-bottom: 30px;
}

#projekt-statistik p {
    margin: 0;
    color: #495057;
}

#projekt-statistik strong {
    color: #0066cc;
    font-size: 1.1em;
}

/* Projekt-Grid */
.projekt-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 25px;
    margin-bottom: 30px;
}

/* Projekt-Karte */
.projekt-karte {
    background: white;
    border: 2px solid #e9ecef;
    border-radius: 8px;
    padding: 20px;
    transition: all 0.3s ease;
    opacity: 1;
    transform: scale(1);
}

.projekt-karte:hover {
    border-color: #0066cc;
    box-shadow: 0 8px 16px rgba(0, 102, 204, 0.15);
    transform: translateY(-5px);
}

.projekt-karte h3 {
    color: #0066cc;
    margin-bottom: 10px;
    font-size: 1.3em;
}

.projekt-status {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.85em;
    font-weight: 600;
    margin-bottom: 15px;
}

.status-abgeschlossen {
    background: #d4edda;
    color: #155724;
}

.status-in-arbeit {
    background: #fff3cd;
    color: #856404;
}

.status-geplant {
    background: #d1ecf1;
    color: #0c5460;
}

.projekt-beschreibung {
    color: #6c757d;
    margin-bottom: 15px;
    font-size: 0.95em;
    line-height: 1.6;
}

.projekt-technologien {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
}

.tech-badge {
    background: #e7f5ff;
    color: #0066cc;
    padding: 4px 10px;
    border-radius: 4px;
    font-size: 0.85em;
    font-weight: 500;
}

.projekt-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #868e96;
    font-size: 0.9em;
    padding-top: 15px;
    border-top: 1px solid #e9ecef;
}

/* Animation beim Filtern */
.projekt-karte.ausgeblendet {
    opacity: 0;
    transform: scale(0.8);
    display: none;
}

.versteckt {
    display: none;
}

.meldung {
    text-align: center;
    padding: 40px;
    color: #6c757d;
    font-size: 1.1em;
}
```

---

### Teil 3: JavaScript-Datenstruktur (10 Min)

Erstelle `projekte.js` mit deinen Projekt-Daten:

```javascript
// =====================================================
// PROJEKT-GALERIE
// =====================================================

console.log("📁 Projekt-Galerie geladen");

// === PROJEKT-DATEN ===
// Hier definierst du alle deine Projekte

const projekte = [
    {
        id: 1,
        name: "Portfolio-Website",
        beschreibung: "Meine persönliche Portfolio-Seite mit HTML, CSS und JavaScript. Zeigt meine Fähigkeiten und Projekte.",
        technologien: ["html", "css", "javascript"],
        status: "in-arbeit",
        startdatum: "2025-01-01",
        dauer: "4 Wochen"
    },
    {
        id: 2,
        name: "HTML Grundlagen",
        beschreibung: "Erste Schritte in HTML: Struktur, Semantik, Formulare und mehr.",
        technologien: ["html"],
        status: "abgeschlossen",
        startdatum: "2024-09-01",
        dauer: "2 Wochen"
    },
    {
        id: 3,
        name: "CSS Layouts",
        beschreibung: "Responsive Layouts mit Flexbox und Grid. Inklusive Mobile-First-Ansatz.",
        technologien: ["css"],
        status: "abgeschlossen",
        startdatum: "2024-10-01",
        dauer: "3 Wochen"
    },
    {
        id: 4,
        name: "JavaScript DOM-Manipulation",
        beschreibung: "Interaktive Elemente mit JavaScript: Klicks, Events, dynamische Inhalte.",
        technologien: ["javascript"],
        status: "in-arbeit",
        startdatum: "2025-01-15",
        dauer: "3 Wochen"
    },
    {
        id: 5,
        name: "To-Do App",
        beschreibung: "Eine vollständige To-Do-Liste mit LocalStorage, Filter und Kategorien.",
        technologien: ["html", "css", "javascript"],
        status: "geplant",
        startdatum: "2025-02-01",
        dauer: "5 Wochen"
    },
    {
        id: 6,
        name: "Wetter-App",
        beschreibung: "Wetter-Daten von einer API abrufen und anzeigen.Inklusive Standort-Erkennung.",
        technologien: ["javascript"],
        status: "geplant",
        startdatum: "2025-03-01",
        dauer: "3 Wochen"
    },
    {
        id: 7,
        name: "React-Einführung",
        beschreibung: "Erste Schritte mit React: Komponenten, Props, State und Hooks.",
        technologien: ["react", "javascript"],
        status: "geplant",
        startdatum: "2025-04-01",
        dauer: "6 Wochen"
    }
];

console.log(`✅ ${projekte.length} Projekte geladen`);

// === PROJEKTE ANZEIGEN ===

function zeigeProjekte(projekteListe) {
    let container = document.getElementById("projekt-container");
    
    // Container leeren
    container.innerHTML = "";
    
    // Statistik aktualisieren
    document.getElementById("anzahl-sichtbar").textContent = projekteListe.length;
    document.getElementById("anzahl-gesamt").textContent = projekte.length;
    
    // Meldung anzeigen, wenn keine Projekte
    let meldung = document.getElementById("keine-projekte");
    if (projekteListe.length === 0) {
        meldung.classList.remove("versteckt");
    } else {
        meldung.classList.add("versteckt");
    }
    
    // Jedes Projekt als Karte erstellen
    projekteListe.forEach(function(projekt, index) {
        // Karte erstellen
        let karte = document.createElement("div");
        karte.className = "projekt-karte";
        
        // Status-Klasse
        let statusKlasse = "status-" + projekt.status;
        
        // Status-Text anpassen
        let statusText = projekt.status;
        if (statusText === "in-arbeit") statusText = "In Arbeit";
        if (statusText === "abgeschlossen") statusText = "Abgeschlossen";
        if (statusText === "geplant") statusText = "Geplant";
        
        // Technologie-Badges erstellen
        let techBadges = "";
        projekt.technologien.forEach(function(tech) {
            techBadges += `<span class="tech-badge">${tech.toUpperCase()}</span>`;
        });
        
        // Karten-Inhalt
        karte.innerHTML = `
            <h3>${projekt.name}</h3>
            <span class="projekt-status ${statusKlasse}">${statusText}</span>
            <p class="projekt-beschreibung">${projekt.beschreibung}</p>
            <div class="projekt-technologien">
                ${techBadges}
            </div>
            <div class="projekt-meta">
                <span>📅 Start: ${formatiereDatum(projekt.startdatum)}</span>
                <span>⏱️ ${projekt.dauer}</span>
            </div>
        `;
        
        // Animation mit Verzögerung
        karte.style.opacity = "0";
        karte.style.transform = "scale(0.8)";
        
        container.appendChild(karte);
        
        // Fade-In-Animation
        setTimeout(function() {
            karte.style.transition = "all 0.3s ease";
            karte.style.opacity = "1";
            karte.style.transform = "scale(1)";
        }, index * 50); // 50ms Verzögerung pro Karte
    });
    
    console.log(`📊 ${projekteListe.length} Projekte angezeigt`);
}

// Hilfsfunktion: Datum formatieren
function formatiereDatum(datumsString) {
    let datum = new Date(datumsString);
    let monate = ["Jan", "Feb", "Mär", "Apr", "Mai", "Jun", 
                  "Jul", "Aug", "Sep", "Okt", "Nov", "Dez"];
    return `${datum.getDate()}. ${monate[datum.getMonth()]} ${datum.getFullYear()}`;
}

// === INITIAL ALLE PROJEKTE ANZEIGEN ===
zeigeProjekte(projekte);
```

---

### Teil 4: Filter-Funktionen (20 Min)

Erweitere `projekte.js` mit Filter-Funktionen:

```javascript
// === FILTER-FUNKTIONEN ===

let aktuelleFilter = {
    technologie: "alle",
    status: "alle",
    suchbegriff: "",
    sortierung: "datum-neu"
};

// Technologie-Filter
document.getElementById("tech-filter").addEventListener("change", function() {
    aktuelleFilter.technologie = this.value;
    console.log("🔍 Filtern nach Technologie:", this.value);
    wendeFilterAn();
});

// Status-Filter
document.getElementById("status-filter").addEventListener("change", function() {
    aktuelleFilter.status = this.value;
    console.log("🔍 Filtern nach Status:", this.value);
    wendeFilterAn();
});

// Suche
document.getElementById("projekt-suche").addEventListener("input", function() {
    aktuelleFilter.suchbegriff = this.value.toLowerCase();
    console.log("🔍 Suche:", this.value);
    wendeFilterAn();
});

// Sortierung
document.getElementById("sortierung").addEventListener("change", function() {
    aktuelleFilter.sortierung = this.value;
    console.log("↕️ Sortiere:", this.value);
    wendeFilterAn();
});

// === FILTER ANWENDEN ===

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

// === SORTIER-FUNKTION ===

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

console.log("✅ Filter-Funktionen initialisiert");
```

---

### Teil 5: Erweiterte Statistiken (Optional, 10 Min)

Füge eine Statistik-Übersicht hinzu:

```javascript
// === STATISTIKEN BERECHNEN ===

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

// Statistik-Übersicht anzeigen
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

// Beim Laden aufrufen
zeigeStatistikUebersicht();
```

---

## Erfolgskriterien

- [ ] Projekt-Galerie-Sektion in HTML eingefügt
- [ ] CSS für Karten, Filter und Animationen vorhanden
- [ ] `projekte.js` mit mindestens 5 Projekten erstellt
- [ ] Projekte werden als Karten angezeigt
- [ ] Technologie-Filter funktioniert
- [ ] Status-Filter funktioniert
- [ ] Suchfunktion funktioniert (Name & Beschreibung)
- [ ] Sortierung funktioniert (Datum & Name)
- [ ] Statistik zeigt korrekte Anzahl
- [ ] Animation beim Einblenden der Karten
- [ ] "Keine Projekte"-Meldung bei leerem Ergebnis

---

## Tipps

- **Array.filter():** Filtert Elemente nach Bedingung
- **Array.sort():** Sortiert Elemente (mit Vergleichsfunktion)
- **includes():** Prüft, ob Element in Array vorhanden
- **Spread-Operator [...]:** Erstellt Kopie eines Arrays
- **Template Literals:** Für dynamisches HTML (`${variable}`)

**Performance-Tipp:**
Bei sehr vielen Projekten (100+) solltest du Debouncing für die Suche einsetzen, damit nicht bei jedem Tastendruck gefiltert wird.

---

## Reflexionsfragen

1. **Warum erstellen wir eine Kopie mit `[...projekte]` bevor wir filtern?**  
   *Was würde passieren, wenn wir direkt `projekte.filter()` nutzen?*

2. **Wie funktioniert die `sort()`-Funktion mit einer Vergleichsfunktion?**  
   *Was bedeuten die Rückgabewerte -1, 0 und 1?*

3. **Könntest du einen weiteren Filter hinzufügen, z.B. nach Dauer?**  
   *Welche Schritte wären nötig? (HTML, Event-Listener, Filter-Logik)*

4. **Die Projekte sind hardcoded im JavaScript. Wie könnte man sie aus einer Datei oder API laden?**  
   *Recherchiere: fetch() und JSON-Dateien.*

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
- [Virtual Scrolling](https://web.dev/virtualize-long-lists-react-window/) (für sehr viele Elemente)

**Best Practices:**
- [Google: Rendering Performance](https://web.dev/rendering-performance/)
- [JavaScript Design Patterns](https://www.patterns.dev/posts/classic-design-patterns/)

---

**⏱️ Geschätzte Zeit:** 65 Minuten  
**📦 Nächster Schritt:** Auftrag 6 (Optional) – Theme-Switcher mit Animation
