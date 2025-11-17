# Auftrag 4 (Optional): API-Dashboard mit Favoriten und History

## Ziel

Du baust ein vollständiges API-Dashboard, das mehrere APIs kombiniert, Favoriten speichert und eine Suchhistorie führt. Dieser Auftrag zeigt fortgeschrittene Techniken wie LocalStorage-Persistenz, komplexes State Management und moderne UI-Patterns.

**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzungen:** Aufträge 1-3 abgeschlossen

## Beschreibung

In diesem anspruchsvollen Auftrag kombinierst du alle gelernten Konzepte zu einer echten Web-App. Du erstellst ein Dashboard mit mehreren API-Integrationen, die Benutzer als Favoriten speichern können. Alle Daten werden in LocalStorage persistiert und beim Reload der Seite wiederhergestellt.

**Features:**
- Mehrere APIs in einem Dashboard (Wetter, Zitate, GitHub, NASA APOD)
- Favoriten-System mit LocalStorage
- Suchhistorie mit Zeitstempel
- Export/Import-Funktion für Daten
- Dark/Light Mode Toggle
- Erweiterte Fehlerbehandlung mit Retry-Mechanismus

---

### Teil 1: Dashboard-Struktur (25 Min)

Erstelle eine neue Datei `dashboard.html`:

```html
<!DOCTYPE html>
<html lang="de" data-theme="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API Dashboard</title>
    <link rel="stylesheet" href="dashboard-styles.css">
</head>
<body>
    <div class="dashboard-container">
        <!-- Header -->
        <header class="dashboard-header">
            <h1>API Dashboard</h1>
            <div class="header-controls">
                <button id="theme-toggle" class="btn-icon" title="Theme wechseln">
                    🌙
                </button>
                <button id="export-data" class="btn-secondary" title="Daten exportieren">
                    📥 Export
                </button>
                <button id="import-data" class="btn-secondary" title="Daten importieren">
                    📤 Import
                </button>
            </div>
        </header>
        
        <!-- Sidebar: Navigation & History -->
        <aside class="sidebar">
            <h2>Navigation</h2>
            <nav class="nav-menu">
                <button class="nav-item active" data-section="weather">
                    🌤️ Wetter
                </button>
                <button class="nav-item" data-section="quotes">
                    💬 Zitate
                </button>
                <button class="nav-item" data-section="github">
                    🐙 GitHub
                </button>
                <button class="nav-item" data-section="nasa">
                    🚀 NASA APOD
                </button>
            </nav>
            
            <div class="history-section">
                <h3>Verlauf</h3>
                <div id="history-list" class="history-list">
                    <!-- History wird hier eingefügt -->
                </div>
                <button id="clear-history" class="btn-danger btn-small">
                    Verlauf löschen
                </button>
            </div>
            
            <div class="favorites-section">
                <h3>Favoriten</h3>
                <div id="favorites-list" class="favorites-list">
                    <!-- Favoriten werden hier eingefügt -->
                </div>
            </div>
        </aside>
        
        <!-- Main Content -->
        <main class="main-content">
            <!-- Wetter-Sektion -->
            <section id="section-weather" class="content-section active">
                <h2>Wetter-Informationen</h2>
                <div class="search-bar">
                    <input 
                        type="text" 
                        id="weather-input" 
                        placeholder="Stadt eingeben..."
                        class="form-input"
                    >
                    <button id="weather-search" class="btn-primary">Suchen</button>
                    <button id="weather-favorite" class="btn-favorite" disabled>
                        ⭐ Favorit
                    </button>
                </div>
                <div id="weather-result" class="result-container"></div>
            </section>
            
            <!-- Zitate-Sektion -->
            <section id="section-quotes" class="content-section">
                <h2>Inspirierende Zitate</h2>
                <div class="action-bar">
                    <button id="quotes-random" class="btn-primary">
                        Zufälliges Zitat
                    </button>
                    <button id="quotes-favorite" class="btn-favorite" disabled>
                        ⭐ Favorit
                    </button>
                </div>
                <div id="quotes-result" class="result-container"></div>
            </section>
            
            <!-- GitHub-Sektion -->
            <section id="section-github" class="content-section">
                <h2>GitHub-User</h2>
                <div class="search-bar">
                    <input 
                        type="text" 
                        id="github-input" 
                        placeholder="GitHub-Username..."
                        class="form-input"
                    >
                    <button id="github-search" class="btn-primary">Suchen</button>
                    <button id="github-favorite" class="btn-favorite" disabled>
                        ⭐ Favorit
                    </button>
                </div>
                <div id="github-result" class="result-container"></div>
            </section>
            
            <!-- NASA-Sektion -->
            <section id="section-nasa" class="content-section">
                <h2>NASA Astronomy Picture of the Day</h2>
                <div class="action-bar">
                    <button id="nasa-today" class="btn-primary">
                        Bild des Tages
                    </button>
                    <button id="nasa-favorite" class="btn-favorite" disabled>
                        ⭐ Favorit
                    </button>
                </div>
                <div id="nasa-result" class="result-container"></div>
            </section>
        </main>
    </div>
    
    <!-- Import-Modal -->
    <div id="import-modal" class="modal versteckt">
        <div class="modal-content">
            <h3>Daten importieren</h3>
            <p>Füge deinen Export-Code hier ein:</p>
            <textarea id="import-textarea" rows="10" class="form-input"></textarea>
            <div class="modal-buttons">
                <button id="import-confirm" class="btn-primary">Importieren</button>
                <button id="import-cancel" class="btn-secondary">Abbrechen</button>
            </div>
        </div>
    </div>
    
    <script src="dashboard.js"></script>
</body>
</html>
```

---

### Teil 2: Dashboard CSS (20 Min)

Erstelle `dashboard-styles.css`:

```css
/* === VARIABLES === */
:root {
    --bg-primary: #1a1a2e;
    --bg-secondary: #16213e;
    --bg-tertiary: #0f3460;
    --text-primary: #eaeaea;
    --text-secondary: #a0a0a0;
    --accent: #00d4ff;
    --accent-hover: #00b8e6;
    --success: #2ea44f;
    --danger: #dc3545;
    --warning: #ffc107;
}

[data-theme="light"] {
    --bg-primary: #f5f5f5;
    --bg-secondary: #ffffff;
    --bg-tertiary: #e0e0e0;
    --text-primary: #1a1a1a;
    --text-secondary: #666666;
    --accent: #0066cc;
    --accent-hover: #0052a3;
}

/* === RESET & BASE === */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: var(--bg-primary);
    color: var(--text-primary);
    transition: background 0.3s, color 0.3s;
}

/* === LAYOUT === */
.dashboard-container {
    display: grid;
    grid-template-areas:
        "header header"
        "sidebar main";
    grid-template-columns: 280px 1fr;
    grid-template-rows: 70px 1fr;
    min-height: 100vh;
}

.dashboard-header {
    grid-area: header;
    background: var(--bg-secondary);
    padding: 0 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 2px solid var(--bg-tertiary);
}

.dashboard-header h1 {
    font-size: 1.8em;
    color: var(--accent);
}

.header-controls {
    display: flex;
    gap: 10px;
}

.sidebar {
    grid-area: sidebar;
    background: var(--bg-secondary);
    padding: 20px;
    border-right: 2px solid var(--bg-tertiary);
    overflow-y: auto;
}

.main-content {
    grid-area: main;
    padding: 30px;
    overflow-y: auto;
}

/* === NAVIGATION === */
.nav-menu {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 30px;
}

.nav-item {
    background: var(--bg-tertiary);
    color: var(--text-primary);
    border: none;
    padding: 12px 15px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1em;
    text-align: left;
    transition: all 0.3s;
}

.nav-item:hover {
    background: var(--accent);
    color: white;
}

.nav-item.active {
    background: var(--accent);
    color: white;
    font-weight: 600;
}

/* === BUTTONS === */
.btn-primary, .btn-secondary, .btn-danger, .btn-favorite, .btn-icon {
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1em;
    font-weight: 600;
    transition: all 0.3s;
}

.btn-primary {
    background: var(--accent);
    color: white;
}

.btn-primary:hover {
    background: var(--accent-hover);
}

.btn-secondary {
    background: var(--bg-tertiary);
    color: var(--text-primary);
}

.btn-secondary:hover {
    background: var(--text-secondary);
}

.btn-danger {
    background: var(--danger);
    color: white;
}

.btn-danger:hover {
    background: #c82333;
}

.btn-favorite {
    background: transparent;
    border: 2px solid var(--warning);
    color: var(--warning);
}

.btn-favorite:hover:not(:disabled) {
    background: var(--warning);
    color: white;
}

.btn-favorite:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

.btn-favorite.active {
    background: var(--warning);
    color: white;
}

.btn-icon {
    background: transparent;
    font-size: 1.5em;
    padding: 8px 12px;
}

.btn-small {
    font-size: 0.85em;
    padding: 8px 15px;
}

/* === CONTENT SECTIONS === */
.content-section {
    display: none;
}

.content-section.active {
    display: block;
}

.content-section h2 {
    margin-bottom: 20px;
    color: var(--accent);
}

/* === SEARCH & ACTION BARS === */
.search-bar, .action-bar {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.search-bar input {
    flex: 1;
}

.form-input {
    background: var(--bg-tertiary);
    border: 2px solid transparent;
    color: var(--text-primary);
    padding: 12px;
    border-radius: 6px;
    font-size: 1em;
    transition: border 0.3s;
}

.form-input:focus {
    outline: none;
    border-color: var(--accent);
}

/* === RESULT CONTAINERS === */
.result-container {
    background: var(--bg-secondary);
    padding: 20px;
    border-radius: 12px;
    border: 2px solid var(--bg-tertiary);
    min-height: 200px;
}

/* === HISTORY & FAVORITES === */
.history-section, .favorites-section {
    margin-top: 30px;
}

.history-section h3, .favorites-section h3 {
    font-size: 1.2em;
    margin-bottom: 15px;
    color: var(--text-secondary);
}

.history-list, .favorites-list {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 15px;
    max-height: 300px;
    overflow-y: auto;
}

.history-item, .favorite-item {
    background: var(--bg-tertiary);
    padding: 10px;
    border-radius: 6px;
    font-size: 0.9em;
    cursor: pointer;
    transition: background 0.2s;
}

.history-item:hover, .favorite-item:hover {
    background: var(--accent);
    color: white;
}

.history-item .timestamp {
    font-size: 0.8em;
    opacity: 0.7;
    display: block;
    margin-top: 5px;
}

/* === MODAL === */
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal-content {
    background: var(--bg-secondary);
    padding: 30px;
    border-radius: 12px;
    max-width: 600px;
    width: 90%;
}

.modal-content h3 {
    margin-bottom: 15px;
}

.modal-content textarea {
    width: 100%;
    margin: 15px 0;
}

.modal-buttons {
    display: flex;
    gap: 10px;
    justify-content: flex-end;
}

/* === UTILITIES === */
.versteckt {
    display: none !important;
}

/* === RESPONSIVE === */
@media (max-width: 768px) {
    .dashboard-container {
        grid-template-areas:
            "header"
            "main"
            "sidebar";
        grid-template-columns: 1fr;
        grid-template-rows: 70px 1fr auto;
    }
    
    .sidebar {
        border-right: none;
        border-top: 2px solid var(--bg-tertiary);
    }
}
```

---

### Teil 3: Dashboard JavaScript (45 Min)

Erstelle `dashboard.js` mit State Management:

```javascript
// =====================================================
// API DASHBOARD
// =====================================================
// Vollständiges Dashboard mit mehreren APIs, Favoriten und History

console.log("Dashboard geladen!");

// === STATE MANAGEMENT ===

const STATE = {
    currentSection: "weather",
    theme: "dark",
    history: [],
    favorites: [],
    currentData: {
        weather: null,
        quotes: null,
        github: null,
        nasa: null
    }
};

// === INITIALIZATION ===

document.addEventListener("DOMContentLoaded", function() {
    console.log("DOM geladen, initialisiere Dashboard...");
    
    // State aus LocalStorage laden
    ladeStateAusLocalStorage();
    
    // Event Listeners registrieren
    registriereEventListeners();
    
    // Theme anwenden
    wendeThemeAn();
    
    // History und Favoriten anzeigen
    aktualisiereHistoryUI();
    aktualisiereFavoritenUI();
    
    console.log("Dashboard initialisiert ✅");
});

// === STATE PERSISTENZ ===

function speichereStateInLocalStorage() {
    try {
        localStorage.setItem("dashboard_state", JSON.stringify(STATE));
        console.log("State gespeichert");
    } catch (fehler) {
        console.error("Fehler beim Speichern:", fehler);
    }
}

function ladeStateAusLocalStorage() {
    try {
        let gespeicherterState = localStorage.getItem("dashboard_state");
        
        if (gespeicherterState) {
            let geladenerState = JSON.parse(gespeicherterState);
            Object.assign(STATE, geladenerState);
            console.log("State geladen:", STATE);
        }
    } catch (fehler) {
        console.error("Fehler beim Laden:", fehler);
    }
}

// === EVENT LISTENERS ===

function registriereEventListeners() {
    // Navigation
    document.querySelectorAll(".nav-item").forEach(function(button) {
        button.addEventListener("click", function() {
            wechsleSektion(this.dataset.section);
        });
    });
    
    // Theme Toggle
    document.getElementById("theme-toggle").addEventListener("click", toggleTheme);
    
    // Export/Import
    document.getElementById("export-data").addEventListener("click", exportiereDaten);
    document.getElementById("import-data").addEventListener("click", zeigImportModal);
    document.getElementById("import-confirm").addEventListener("click", importiereDaten);
    document.getElementById("import-cancel").addEventListener("click", versteckeImportModal);
    
    // History löschen
    document.getElementById("clear-history").addEventListener("click", loescheHistory);
    
    // API-spezifische Listeners
    registriereWetterListeners();
    registriereZitateListeners();
    registriereGitHubListeners();
    registriereNASAListeners();
}

// === NAVIGATION ===

function wechsleSektion(sektion) {
    STATE.currentSection = sektion;
    
    // Navigation-Buttons aktualisieren
    document.querySelectorAll(".nav-item").forEach(function(button) {
        button.classList.remove("active");
    });
    document.querySelector(`[data-section="${sektion}"]`).classList.add("active");
    
    // Content-Sektionen aktualisieren
    document.querySelectorAll(".content-section").forEach(function(section) {
        section.classList.remove("active");
    });
    document.getElementById(`section-${sektion}`).classList.add("active");
    
    console.log(`Sektion gewechselt: ${sektion}`);
}

// === THEME MANAGEMENT ===

function toggleTheme() {
    STATE.theme = STATE.theme === "dark" ? "light" : "dark";
    wendeThemeAn();
    speichereStateInLocalStorage();
}

function wendeThemeAn() {
    document.documentElement.setAttribute("data-theme", STATE.theme);
    let icon = STATE.theme === "dark" ? "🌙" : "☀️";
    document.getElementById("theme-toggle").textContent = icon;
}

// === HISTORY MANAGEMENT ===

function fuegeHistoryHinzu(typ, beschreibung) {
    let eintrag = {
        typ: typ,
        beschreibung: beschreibung,
        timestamp: new Date().toISOString()
    };
    
    STATE.history.unshift(eintrag); // Am Anfang einfügen
    
    // Maximal 50 Einträge
    if (STATE.history.length > 50) {
        STATE.history = STATE.history.slice(0, 50);
    }
    
    speichereStateInLocalStorage();
    aktualisiereHistoryUI();
}

function aktualisiereHistoryUI() {
    let container = document.getElementById("history-list");
    
    if (STATE.history.length === 0) {
        container.innerHTML = "<p style='opacity: 0.6; font-size: 0.9em;'>Noch keine Suchen</p>";
        return;
    }
    
    container.innerHTML = STATE.history.map(function(eintrag) {
        let datum = new Date(eintrag.timestamp);
        let zeitString = datum.toLocaleString("de-CH", {
            day: "2-digit",
            month: "2-digit",
            hour: "2-digit",
            minute: "2-digit"
        });
        
        return `
            <div class="history-item">
                <strong>${eintrag.typ}:</strong> ${eintrag.beschreibung}
                <span class="timestamp">${zeitString}</span>
            </div>
        `;
    }).join("");
}

function loescheHistory() {
    if (confirm("Wirklich den gesamten Verlauf löschen?")) {
        STATE.history = [];
        speichereStateInLocalStorage();
        aktualisiereHistoryUI();
        console.log("History gelöscht");
    }
}

// === FAVORITEN MANAGEMENT ===

function fuegeFavoritHinzu(typ, daten) {
    let favorit = {
        typ: typ,
        daten: daten,
        timestamp: new Date().toISOString()
    };
    
    STATE.favorites.push(favorit);
    speichereStateInLocalStorage();
    aktualisiereFavoritenUI();
    
    console.log("Favorit hinzugefügt:", favorit);
}

function entferneFavorit(index) {
    STATE.favorites.splice(index, 1);
    speichereStateInLocalStorage();
    aktualisiereFavoritenUI();
}

function aktualisiereFavoritenUI() {
    let container = document.getElementById("favorites-list");
    
    if (STATE.favorites.length === 0) {
        container.innerHTML = "<p style='opacity: 0.6; font-size: 0.9em;'>Noch keine Favoriten</p>";
        return;
    }
    
    container.innerHTML = STATE.favorites.map(function(favorit, index) {
        let beschreibung = "";
        
        if (favorit.typ === "weather") {
            beschreibung = favorit.daten.city;
        } else if (favorit.typ === "quote") {
            beschreibung = favorit.daten.content.substring(0, 50) + "...";
        } else if (favorit.typ === "github") {
            beschreibung = favorit.daten.login;
        } else if (favorit.typ === "nasa") {
            beschreibung = favorit.daten.title;
        }
        
        return `
            <div class="favorite-item" onclick="entferneFavorit(${index})">
                <strong>${favorit.typ}:</strong> ${beschreibung}
                <span style="float: right;">❌</span>
            </div>
        `;
    }).join("");
}

// === EXPORT/IMPORT ===

function exportiereDaten() {
    let exportData = {
        version: "1.0",
        exportDate: new Date().toISOString(),
        state: STATE
    };
    
    let jsonString = JSON.stringify(exportData, null, 2);
    
    // Download als Datei
    let blob = new Blob([jsonString], { type: "application/json" });
    let url = URL.createObjectURL(blob);
    let a = document.createElement("a");
    a.href = url;
    a.download = `dashboard-export-${Date.now()}.json`;
    a.click();
    
    console.log("Daten exportiert");
}

function zeigImportModal() {
    document.getElementById("import-modal").classList.remove("versteckt");
}

function versteckeImportModal() {
    document.getElementById("import-modal").classList.add("versteckt");
}

function importiereDaten() {
    try {
        let textarea = document.getElementById("import-textarea");
        let importData = JSON.parse(textarea.value);
        
        if (importData.version && importData.state) {
            Object.assign(STATE, importData.state);
            speichereStateInLocalStorage();
            
            // UI aktualisieren
            wendeThemeAn();
            aktualisiereHistoryUI();
            aktualisiereFavoritenUI();
            
            versteckeImportModal();
            alert("Daten erfolgreich importiert!");
            
            console.log("Daten importiert:", STATE);
        } else {
            throw new Error("Ungültiges Format");
        }
    } catch (fehler) {
        alert("Fehler beim Importieren: " + fehler.message);
        console.error("Import-Fehler:", fehler);
    }
}

// === API-FUNKTIONEN (Beispiele) ===

// WETTER
function registriereWetterListeners() {
    document.getElementById("weather-search").addEventListener("click", sucheWetter);
    document.getElementById("weather-favorite").addEventListener("click", function() {
        if (STATE.currentData.weather) {
            fuegeFavoritHinzu("weather", STATE.currentData.weather);
        }
    });
}

async function sucheWetter() {
    let stadt = document.getElementById("weather-input").value.trim();
    if (!stadt) return;
    
    fuegeHistoryHinzu("Wetter", stadt);
    
    // Hier würde der API-Call folgen
    console.log("Suche Wetter für:", stadt);
    
    // Favorit-Button aktivieren
    document.getElementById("weather-favorite").disabled = false;
}

// ZITATE (analog zu anderen APIs)
function registriereZitateListeners() {
    document.getElementById("quotes-random").addEventListener("click", ladeZufaelligesZitat);
}

async function ladeZufaelligesZitat() {
    fuegeHistoryHinzu("Zitat", "Zufälliges Zitat geladen");
    console.log("Lade Zitat...");
}

// GITHUB
function registriereGitHubListeners() {
    document.getElementById("github-search").addEventListener("click", sucheGitHubUser);
}

async function sucheGitHubUser() {
    let username = document.getElementById("github-input").value.trim();
    if (!username) return;
    
    fuegeHistoryHinzu("GitHub", username);
    console.log("Suche GitHub-User:", username);
}

// NASA
function registriereNASAListeners() {
    document.getElementById("nasa-today").addEventListener("click", ladeNASABild);
}

async function ladeNASABild() {
    fuegeHistoryHinzu("NASA APOD", "Bild des Tages");
    console.log("Lade NASA-Bild...");
}

console.log("Event Listeners registriert ✅");
```

---

## Erfolgskriterien

Grundfunktionen:
- [ ] Dashboard-Layout funktioniert
- [ ] Navigation zwischen Sektionen
- [ ] Theme-Wechsel (Dark/Light Mode)
- [ ] History-System speichert Suchen
- [ ] Favoriten-System funktioniert
- [ ] Export/Import von Daten
- [ ] LocalStorage-Persistenz

Erweiterte Features:
- [ ] Alle 4 APIs integriert (Wetter, Zitate, GitHub, NASA)
- [ ] Favorit-Button aktiviert/deaktiviert sich korrekt
- [ ] History zeigt Timestamp
- [ ] Favoriten können entfernt werden
- [ ] Export als JSON-Datei
- [ ] Import validiert Daten
- [ ] Responsive Design funktioniert

---

## Tipps

- **State Management:** Zentraler State macht Code wartbar
- **LocalStorage:** Immer try-catch bei JSON.parse/stringify
- **Export/Import:** Blob API für File-Downloads
- **Theme System:** CSS Custom Properties für einfachen Wechsel
- **Array Methods:** unshift(), splice(), slice() für History/Favoriten

**Performance-Tipps:**
- Debounce bei Eingabefeldern
- Lazy Loading für API-Daten
- Cache für API-Responses

---

## Reflexionsfragen

1. **Warum ist zentrales State Management wichtig?**
2. **Was sind die Limits von LocalStorage?**
3. **Wie würdest du das Dashboard skalieren für 20+ APIs?**
4. **Was ist der Unterschied zwischen SessionStorage und LocalStorage?**
5. **Wie könnte man die App für Offline-Nutzung optimieren?**

---

**Geschätzte Zeit:** 90-120 Minuten  
**Challenge:** Füge 2 weitere APIs deiner Wahl hinzu!
