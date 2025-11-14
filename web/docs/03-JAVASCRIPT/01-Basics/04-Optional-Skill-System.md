# Auftrag 4 (Optional): Interaktives Skill-Rating-System

## Ziel

Du erstellst ein fortgeschrittenes, interaktives System, das deine Skills dynamisch visualisiert. Dieser Auftrag kombiniert DOM-Manipulation, CSS-Animationen und LocalStorage zu einem professionellen Feature.

**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzungen:** Aufträge 1-3 abgeschlossen

## Beschreibung

Viele Portfolio-Seiten zeigen Skills mit statischen Balken. Du erstellst ein **dynamisches System**, bei dem:
- Skills animiert eingeblendet werden
- Nutzer Skills bewerten können (1-5 Sterne)
- Bewertungen im LocalStorage gespeichert werden
- Skills sortiert und gefiltert werden können
- Fortschritt visuell dargestellt wird

Dieses Feature zeigt fortgeschrittene JavaScript-Kenntnisse und ist ein echter Hingucker im Portfolio.

---

## Teil 1: HTML-Struktur für Skill-System (15 Min)

Erstelle eine neue Sektion in `index.html`:

```html
<section id="skills-interaktiv">
    <h2>Meine Skills – Interaktiv</h2>
    <p>Bewerte meine Skills oder füge neue hinzu. Alle Änderungen werden lokal gespeichert.</p>
    
    <!-- Filter & Sortierung -->
    <div class="skill-controls">
        <div class="filter-gruppe">
            <label for="skill-filter">Filtern nach:</label>
            <select id="skill-filter">
                <option value="alle">Alle Skills</option>
                <option value="frontend">Frontend</option>
                <option value="backend">Backend</option>
                <option value="tools">Tools & Workflows</option>
            </select>
        </div>
        
        <div class="sort-gruppe">
            <label for="skill-sort">Sortieren nach:</label>
            <select id="skill-sort">
                <option value="name">Name (A-Z)</option>
                <option value="level">Level (aufsteigend)</option>
                <option value="level-desc">Level (absteigend)</option>
            </select>
        </div>
        
        <button id="reset-skills" class="btn-secondary">Skills zurücksetzen</button>
    </div>
    
    <!-- Skill-Container -->
    <div id="skill-container" class="skill-grid">
        <!-- Skills werden hier dynamisch eingefügt -->
    </div>
    
    <!-- Statistik -->
    <div class="skill-stats">
        <h3>Statistik</h3>
        <p>Gesamt Skills: <span id="total-skills">0</span></p>
        <p>Durchschnittslevel: <span id="avg-level">0</span> / 5</p>
        <p>Beste Kategorie: <span id="best-category">-</span></p>
    </div>
</section>
```

---

## Teil 2: CSS für Skill-System (10 Min)

Füge in `styles.css` hinzu:

```css
/* ====================================
   INTERAKTIVES SKILL-SYSTEM
   ==================================== */

.skill-controls {
    display: flex;
    gap: 1rem;
    margin-bottom: 2rem;
    flex-wrap: wrap;
    align-items: center;
}

.skill-controls select,
.skill-controls button {
    padding: 0.5rem 1rem;
    border: 2px solid #376B8C;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
}

.skill-controls select {
    background: white;
}

.btn-secondary {
    background: #E07A42;
    color: white;
    border: none;
    transition: background 0.3s;
}

.btn-secondary:hover {
    background: #c96835;
}

.skill-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.skill-card {
    background: white;
    border: 2px solid #376B8C;
    border-radius: 10px;
    padding: 1.5rem;
    transition: transform 0.3s, box-shadow 0.3s;
    opacity: 0;
    animation: fadeInUp 0.5s forwards;
}

.skill-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(55, 107, 140, 0.3);
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.skill-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
}

.skill-name {
    font-size: 1.2rem;
    font-weight: bold;
    color: #376B8C;
}

.skill-category {
    font-size: 0.8rem;
    color: #666;
    background: #f0f0f0;
    padding: 0.25rem 0.5rem;
    border-radius: 5px;
}

.skill-level-bar {
    width: 100%;
    height: 20px;
    background: #e0e0e0;
    border-radius: 10px;
    overflow: hidden;
    margin: 1rem 0;
    position: relative;
}

.skill-level-fill {
    height: 100%;
    background: linear-gradient(90deg, #376B8C, #29786A);
    transition: width 1s ease-out;
    border-radius: 10px;
}

.skill-level-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-weight: bold;
    font-size: 0.9rem;
    text-shadow: 0 1px 2px rgba(0,0,0,0.3);
}

.skill-rating {
    display: flex;
    gap: 0.5rem;
    align-items: center;
}

.star {
    font-size: 1.5rem;
    cursor: pointer;
    color: #ddd;
    transition: color 0.2s, transform 0.2s;
}

.star.active {
    color: #FFD700;
}

.star:hover {
    transform: scale(1.2);
}

.skill-stats {
    background: linear-gradient(135deg, #376B8C, #29786A);
    color: white;
    padding: 2rem;
    border-radius: 10px;
    text-align: center;
}

.skill-stats h3 {
    margin-bottom: 1rem;
}

.skill-stats p {
    font-size: 1.1rem;
    margin: 0.5rem 0;
}

.skill-stats span {
    font-weight: bold;
    font-size: 1.3rem;
}
```

---

## Teil 3: JavaScript – Skill-Datenstruktur (15 Min)

Erstelle eine neue Datei **`skills-interaktiv.js`**:

```javascript
// =====================================================
// INTERAKTIVES SKILL-SYSTEM
// =====================================================

console.log("Skill-System geladen!");

// === SKILL-DATEN ===
const skillDaten = [
    { id: 1, name: "HTML", kategorie: "frontend", level: 4, beschreibung: "Semantisches Markup" },
    { id: 2, name: "CSS", kategorie: "frontend", level: 4, beschreibung: "Responsive Design, Flexbox, Grid" },
    { id: 3, name: "JavaScript", kategorie: "frontend", level: 3, beschreibung: "DOM, Events, ES6+" },
    { id: 4, name: "Git", kategorie: "tools", level: 3, beschreibung: "Versionskontrolle, Branching" },
    { id: 5, name: "VS Code", kategorie: "tools", level: 4, beschreibung: "Produktive Entwicklungsumgebung" },
    { id: 6, name: "Node.js", kategorie: "backend", level: 2, beschreibung: "Grundlagen, NPM" },
    { id: 7, name: "Express", kategorie: "backend", level: 2, beschreibung: "Einfache APIs erstellen" },
    { id: 8, name: "Responsive Design", kategorie: "frontend", level: 4, beschreibung: "Mobile-First, Media Queries" },
    { id: 9, name: "Chrome DevTools", kategorie: "tools", level: 3, beschreibung: "Debugging, Performance" },
    { id: 10, name: "Markdown", kategorie: "tools", level: 4, beschreibung: "Dokumentation" }
];

// === LOKALE BEWERTUNGEN LADEN ===
function ladeBewertungen() {
    let gespeichert = localStorage.getItem("skillBewertungen");
    if (gespeichert) {
        return JSON.parse(gespeichert);
    }
    return {};
}

// === BEWERTUNGEN SPEICHERN ===
function speichereBewertungen(bewertungen) {
    localStorage.setItem("skillBewertungen", JSON.stringify(bewertungen));
}

// Bewertungen beim Start laden
let skillBewertungen = ladeBewertungen();

// === SKILLS ANZEIGEN ===
function zeigeSkills(filterKategorie = "alle", sortierung = "name") {
    let container = document.getElementById("skill-container");
    container.innerHTML = ""; // Leeren
    
    // Filtern
    let gefiltert = skillDaten.filter(skill => {
        if (filterKategorie === "alle") return true;
        return skill.kategorie === filterKategorie;
    });
    
    // Sortieren
    gefiltert.sort((a, b) => {
        if (sortierung === "name") {
            return a.name.localeCompare(b.name);
        } else if (sortierung === "level") {
            return a.level - b.level;
        } else if (sortierung === "level-desc") {
            return b.level - a.level;
        }
    });
    
    // Skills erstellen
    gefiltert.forEach((skill, index) => {
        let card = erstelleSkillCard(skill, index);
        container.appendChild(card);
    });
    
    // Statistik aktualisieren
    aktualisiereStatistik();
}

// === SKILL-CARD ERSTELLEN ===
function erstelleSkillCard(skill, index) {
    let card = document.createElement("div");
    card.className = "skill-card";
    card.style.animationDelay = `${index * 0.1}s`;
    
    // Bewertung aus LocalStorage holen (falls vorhanden)
    let bewertung = skillBewertungen[skill.id] || skill.level;
    
    card.innerHTML = `
        <div class="skill-header">
            <span class="skill-name">${skill.name}</span>
            <span class="skill-category">${kategorieUebersetzen(skill.kategorie)}</span>
        </div>
        
        <p class="skill-beschreibung">${skill.beschreibung}</p>
        
        <div class="skill-level-bar">
            <div class="skill-level-fill" style="width: ${bewertung * 20}%"></div>
            <span class="skill-level-text">${bewertung} / 5</span>
        </div>
        
        <div class="skill-rating">
            <span>Bewerten:</span>
            ${erstelleSterne(skill.id, bewertung)}
        </div>
    `;
    
    return card;
}

// === STERNE ERSTELLEN ===
function erstelleSterne(skillId, aktuelleBewertung) {
    let sterneHTML = "";
    for (let i = 1; i <= 5; i++) {
        let active = i <= aktuelleBewertung ? "active" : "";
        sterneHTML += `<span class="star ${active}" data-skill="${skillId}" data-rating="${i}">★</span>`;
    }
    return sterneHTML;
}

// === KATEGORIE ÜBERSETZEN ===
function kategorieUebersetzen(kategorie) {
    const uebersetzungen = {
        "frontend": "Frontend",
        "backend": "Backend",
        "tools": "Tools & Workflows"
    };
    return uebersetzungen[kategorie] || kategorie;
}

// === EVENT LISTENERS ===
document.addEventListener("DOMContentLoaded", function() {
    // Initiales Anzeigen
    zeigeSkills();
    
    // Filter
    document.getElementById("skill-filter").addEventListener("change", function(e) {
        let sortierung = document.getElementById("skill-sort").value;
        zeigeSkills(e.target.value, sortierung);
    });
    
    // Sortierung
    document.getElementById("skill-sort").addEventListener("change", function(e) {
        let filter = document.getElementById("skill-filter").value;
        zeigeSkills(filter, e.target.value);
    });
    
    // Reset-Button
    document.getElementById("reset-skills").addEventListener("click", function() {
        if (confirm("Alle Bewertungen zurücksetzen?")) {
            localStorage.removeItem("skillBewertungen");
            skillBewertungen = {};
            zeigeSkills();
            console.log("Skills zurückgesetzt!");
        }
    });
    
    // Sterne-Bewertung (Event Delegation)
    document.getElementById("skill-container").addEventListener("click", function(e) {
        if (e.target.classList.contains("star")) {
            let skillId = parseInt(e.target.dataset.skill);
            let rating = parseInt(e.target.dataset.rating);
            
            // Bewertung speichern
            skillBewertungen[skillId] = rating;
            speichereBewertungen(skillBewertungen);
            
            // Skills neu anzeigen
            let filter = document.getElementById("skill-filter").value;
            let sortierung = document.getElementById("skill-sort").value;
            zeigeSkills(filter, sortierung);
            
            console.log(`Skill ${skillId} bewertet mit ${rating} Sternen`);
        }
    });
});

// === STATISTIK ===
function aktualisiereStatistik() {
    // Gesamtanzahl
    let total = skillDaten.length;
    document.getElementById("total-skills").textContent = total;
    
    // Durchschnittslevel
    let summe = skillDaten.reduce((acc, skill) => {
        let bewertung = skillBewertungen[skill.id] || skill.level;
        return acc + bewertung;
    }, 0);
    let durchschnitt = (summe / total).toFixed(1);
    document.getElementById("avg-level").textContent = durchschnitt;
    
    // Beste Kategorie
    let kategorien = {
        frontend: [],
        backend: [],
        tools: []
    };
    
    skillDaten.forEach(skill => {
        let bewertung = skillBewertungen[skill.id] || skill.level;
        kategorien[skill.kategorie].push(bewertung);
    });
    
    let beste = "";
    let hoechsterDurchschnitt = 0;
    
    for (let kat in kategorien) {
        if (kategorien[kat].length > 0) {
            let katDurchschnitt = kategorien[kat].reduce((a, b) => a + b) / kategorien[kat].length;
            if (katDurchschnitt > hoechsterDurchschnitt) {
                hoechsterDurchschnitt = katDurchschnitt;
                beste = kategorieUebersetzen(kat);
            }
        }
    }
    
    document.getElementById("best-category").textContent = beste;
}
```

---

## Teil 4: Script einbinden und testen (5 Min)

Füge in `index.html` vor `</body>` hinzu:

```html
<script src="script.js"></script>
<script src="dom.js"></script>
<script src="skills-interaktiv.js"></script>
```

**Test-Checkliste:**
- [ ] Skills werden als Cards angezeigt
- [ ] Animationen beim Laden funktionieren
- [ ] Filter nach Kategorie funktioniert
- [ ] Sortierung funktioniert
- [ ] Sterne können angeklickt werden
- [ ] Bewertungen werden gespeichert (nach F5 noch vorhanden)
- [ ] Statistik zeigt korrekte Werte
- [ ] Reset-Button löscht Bewertungen

---

## Teil 5: Erweiterte Features (Optional, 20 Min)

### Feature 1: Neuen Skill hinzufügen

```javascript
// HTML hinzufügen:
// <button id="add-skill">Neuen Skill hinzufügen</button>

document.getElementById("add-skill").addEventListener("click", function() {
    let name = prompt("Skill-Name:");
    if (!name) return;
    
    let kategorie = prompt("Kategorie (frontend/backend/tools):");
    if (!["frontend", "backend", "tools"].includes(kategorie)) {
        alert("Ungültige Kategorie!");
        return;
    }
    
    let level = parseInt(prompt("Level (1-5):"));
    if (isNaN(level) || level < 1 || level > 5) {
        alert("Level muss zwischen 1 und 5 liegen!");
        return;
    }
    
    let beschreibung = prompt("Beschreibung:");
    
    let neuerSkill = {
        id: skillDaten.length + 1,
        name: name,
        kategorie: kategorie,
        level: level,
        beschreibung: beschreibung || "Keine Beschreibung"
    };
    
    skillDaten.push(neuerSkill);
    zeigeSkills();
    console.log("Neuer Skill hinzugefügt:", neuerSkill);
});
```

### Feature 2: Skill-Export (JSON-Download)

```javascript
function exportiereSkills() {
    let daten = {
        skills: skillDaten,
        bewertungen: skillBewertungen,
        exportDatum: new Date().toISOString()
    };
    
    let json = JSON.stringify(daten, null, 2);
    let blob = new Blob([json], { type: "application/json" });
    let url = URL.createObjectURL(blob);
    
    let link = document.createElement("a");
    link.href = url;
    link.download = "meine-skills.json";
    link.click();
    
    console.log("Skills exportiert!");
}

// Button hinzufügen:
// <button onclick="exportiereSkills()">Skills exportieren</button>
```

### Feature 3: Dark Mode Toggle

```javascript
function toggleDarkMode() {
    document.body.classList.toggle("dark-mode");
    let isDark = document.body.classList.contains("dark-mode");
    localStorage.setItem("darkMode", isDark);
}

// Beim Laden prüfen
if (localStorage.getItem("darkMode") === "true") {
    document.body.classList.add("dark-mode");
}

// CSS hinzufügen:
/*
body.dark-mode {
    background: #1a1a1a;
    color: #f5f5f5;
}

body.dark-mode .skill-card {
    background: #2a2a2a;
    border-color: #4E9BCC;
    color: #f5f5f5;
}
*/
```

---

## Erfolgskriterien

**Basis-Features:**
- [ ] Skill-Cards werden dynamisch erstellt
- [ ] CSS-Animationen funktionieren (Fade-In)
- [ ] Filter nach Kategorie funktioniert
- [ ] Sortierung funktioniert
- [ ] Bewertungen können vergeben werden (Sterne anklicken)
- [ ] Bewertungen werden in LocalStorage gespeichert
- [ ] Nach Neuladen (F5) bleiben Bewertungen erhalten
- [ ] Statistik zeigt korrekte Werte

**Erweiterte Features (Optional):**
- [ ] Neue Skills können hinzugefügt werden
- [ ] Skills können exportiert werden (JSON-Download)
- [ ] Dark Mode funktioniert
- [ ] Responsives Design (Mobile-optimiert)

---

## Tipps

- **Event Delegation:** Statt jedem Stern einen Event Listener zu geben, nutze einen Listener auf dem Container
- **LocalStorage Limits:** Max. 5-10 MB – für Skills ist das mehr als genug
- **JSON.parse() Fehler:** Wrap in try-catch, falls gespeicherte Daten korrupt sind
- **Performance:** Bei 100+ Skills solltest du Virtual Scrolling erwägen
- **Accessibility:** Füge `aria-label` zu Sternen hinzu für Screenreader

---

## Reflexionsfragen

1. **Warum ist Event Delegation effizienter als individuelle Event Listener?**  
   *Teste: Erstelle 100 Skills. Wie viele Event Listener hast du mit Delegation vs. ohne?*

2. **Was passiert, wenn du `JSON.parse()` auf korrupte Daten anwendest?**  
   *Experimentiere: Ändere den LocalStorage-Wert manuell in den DevTools.*

3. **LocalStorage vs. Cookies vs. IndexedDB – was sind die Unterschiede?**  
   *Wann würdest du welche Technologie nutzen?*

4. **Wie würdest du das System erweitern, um Skills von einem Server zu laden (API)?**  
   *Tipp: `fetch()` kommt im nächsten Modul!*

5. **Performance-Optimierung: Was könntest du tun, wenn du 1000+ Skills hast?**  
   *Stichwörter: Lazy Loading, Pagination, Virtual Scrolling*

---

## Weiterführende Links

**Fortgeschrittene JavaScript-Konzepte:**
- [MDN: Event Delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation)
- [MDN: JSON methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JavaScript.info: Data types](https://javascript.info/data-types)

**LocalStorage & Performance:**
- [MDN: Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
- [Google: Web Storage Best Practices](https://web.dev/storage-for-the-web/)

**Animation & UX:**
- [CSS-Tricks: Animation Performance](https://css-tricks.com/animations-the-angular-way/)
- [MDN: Using CSS animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations/Using_CSS_animations)

**Accessibility:**
- [MDN: ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
- [WebAIM: Accessible JavaScript](https://webaim.org/techniques/javascript/)

---

**⏱️ Geschätzte Zeit:** 90-120 Minuten  
**🎯 Challenge:** Erweitere das System um Export/Import, Dark Mode und Custom Themes!  
**📦 Portfolio-Boost:** Dieses Feature zeigt fortgeschrittene JS-Kenntnisse und ist ein echter Hingucker!
