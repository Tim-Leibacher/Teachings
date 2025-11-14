# Auftrag 4 (Optional): Theme-Switcher mit Animationen

## Ziel

Du erstellst einen professionellen Theme-Switcher (Hell/Dunkel-Modus) mit flüssigen Animationen und Persistenz. Dieses Feature findet sich in fast allen modernen Websites und Apps.

## Beschreibung

Ein Theme-Switcher erlaubt Benutzern, zwischen verschiedenen Farbschemas zu wechseln. Das ist nicht nur modern, sondern auch wichtig für Barrierefreiheit und Benutzerkomfort. In diesem optionalen Auftrag lernst du, wie du:

- CSS-Custom Properties (CSS-Variablen) mit JavaScript änderst
- Themes nahtlos mit Animationen wechselst
- Benutzer-Präferenzen im LocalStorage speicherst
- System-Präferenzen des Betriebssystems erkennst
- Mehrere Themes (nicht nur Hell/Dunkel) implementierst

Dieser Auftrag ist fortgeschritten und kombiniert mehrere Konzepte. Er geht über die Video-Inhalte hinaus und ist perfekt für Lernende, die mehr wollen.

---

## Vorkenntnisse

Dieser Auftrag baut auf den vorherigen Aufträgen auf. Du solltest verstehen:
- DOM-Manipulation (querySelector, classList)
- LocalStorage (setItem, getItem)
- Event-Listener (addEventListener)
- CSS-Grundlagen (Klassen, Selektoren)

---

### Teil 1: CSS-Custom Properties einrichten (15 Min)

Custom Properties (CSS-Variablen) sind der Schlüssel für flexible Themes. Erstelle oder erweitere deine styles.css:

```css
/* =====================================================
   THEME SYSTEM - CSS CUSTOM PROPERTIES
   ===================================================== */

:root {
    /* === HELL-THEME (Standard) === */
    --bg-primary: #ffffff;
    --bg-secondary: #f8f9fa;
    --bg-tertiary: #e9ecef;
    
    --text-primary: #212529;
    --text-secondary: #6c757d;
    --text-tertiary: #adb5bd;
    
    --accent-primary: #0066cc;
    --accent-secondary: #00b8d4;
    --accent-tertiary: #ff6b35;
    
    --border-color: #dee2e6;
    --shadow-color: rgba(0, 0, 0, 0.1);
    
    /* Spezifische Elemente */
    --header-bg: linear-gradient(135deg, #0066cc 0%, #00b8d4 50%, #ff6b35 100%);
    --card-bg: #ffffff;
    --code-bg: #f8f9fa;
    
    /* Transitions */
    --transition-speed: 0.3s;
}

/* === DUNKEL-THEME === */
[data-theme="dark"] {
    --bg-primary: #1a1a1a;
    --bg-secondary: #2c2c2c;
    --bg-tertiary: #3a3a3a;
    
    --text-primary: #f5f5f5;
    --text-secondary: #b0b0b0;
    --text-tertiary: #808080;
    
    --accent-primary: #4da6ff;
    --accent-secondary: #33d4ff;
    --accent-tertiary: #ff8c5a;
    
    --border-color: #4a4a4a;
    --shadow-color: rgba(0, 0, 0, 0.5);
    
    --header-bg: linear-gradient(135deg, #003d7a 0%, #006b8f 50%, #cc3d1a 100%);
    --card-bg: #2c2c2c;
    --code-bg: #1e1e1e;
}

/* === GLOBALE STYLES MIT VARIABLEN === */
body {
    background-color: var(--bg-primary);
    color: var(--text-primary);
    transition: background-color var(--transition-speed) ease,
                color var(--transition-speed) ease;
}

section {
    background-color: var(--card-bg);
    border: 1px solid var(--border-color);
    box-shadow: 0 2px 4px var(--shadow-color);
    transition: all var(--transition-speed) ease;
}

h1, h2, h3 {
    color: var(--accent-primary);
    transition: color var(--transition-speed) ease;
}

a {
    color: var(--accent-primary);
    transition: color var(--transition-speed) ease;
}

a:hover {
    color: var(--accent-secondary);
}

code, pre {
    background: var(--code-bg);
    color: var(--text-primary);
    border: 1px solid var(--border-color);
}
```

Wichtig: Ersetze alle hardcodierten Farben in deinem CSS durch CSS-Variablen!

---

### Teil 2: HTML für Theme-Switcher (10 Min)

F�ge eine Theme-Switcher-Komponente in dein HTML ein (z.B. im Header):

```html
<div id="theme-switcher">
    <button id="theme-toggle" class="theme-button" aria-label="Theme wechseln">
        <span class="theme-icon">🌙</span>
        <span class="theme-text">Dunkel</span>
    </button>
</div>
```

---

### Teil 3: CSS für Theme-Switcher (10 Min)

Styles für die Theme-Switcher-Komponente:

```css
/* === THEME SWITCHER === */
#theme-switcher {
    position: fixed;
    top: 20px;
    right: 20px;
    z-index: 1000;
}

.theme-button {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 20px;
    background: var(--card-bg);
    border: 2px solid var(--border-color);
    border-radius: 25px;
    cursor: pointer;
    font-size: 1em;
    font-weight: 600;
    color: var(--text-primary);
    box-shadow: 0 4px 8px var(--shadow-color);
    transition: all 0.3s ease;
}

.theme-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 12px var(--shadow-color);
    border-color: var(--accent-primary);
}

.theme-icon {
    font-size: 1.3em;
    transition: transform 0.3s ease;
}

.theme-button:hover .theme-icon {
    transform: rotate(15deg) scale(1.1);
}
```

---

### Teil 4: JavaScript für Theme-Switcher (25 Min)

Erstelle theme-switcher.js:

```javascript
// =====================================================
// THEME SWITCHER
// =====================================================

console.log("🎨 Theme-Switcher geladen");

// === AKTUELLES THEME ===
let aktuellesTheme = "light";

// === SYSTEM-PRÄFERENZ ERKENNEN ===
function getSystemTheme() {
    // Browser-API: prefers-color-scheme
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
        return "dark";
    }
    return "light";
}

// === THEME ANWENDEN ===
function setzeTheme(themeName) {
    console.log("🎨 Setze Theme:", themeName);
    
    // Theme am <html>-Element setzen
    document.documentElement.setAttribute("data-theme", themeName);
    
    // Aktuelles Theme speichern
    aktuellesTheme = themeName;
    
    // Button-Text und Icon aktualisieren
    aktualisiereButton(themeName);
    
    // Theme in LocalStorage speichern
    localStorage.setItem("gewaehltes-theme", themeName);
    
    console.log("✅ Theme aktiviert:", themeName);
}

// === BUTTON AKTUALISIEREN ===
function aktualisiereButton(themeName) {
    let button = document.getElementById("theme-toggle");
    let icon = button.querySelector(".theme-icon");
    let text = button.querySelector(".theme-text");
    
    // Icon und Text je nach Theme
    if (themeName === "dark") {
        icon.textContent = "☀️";
        text.textContent = "Hell";
    } else {
        icon.textContent = "🌙";
        text.textContent = "Dunkel";
    }
}

// === GESPEICHERTES THEME LADEN ===
function ladeGespeichertesTheme() {
    let gespeichert = localStorage.getItem("gewaehltes-theme");
    
    if (gespeichert) {
        console.log("📂 Lade gespeichertes Theme:", gespeichert);
        setzeTheme(gespeichert);
    } else {
        // Kein gespeichertes Theme → System-Präferenz nutzen
        let systemTheme = getSystemTheme();
        console.log("ℹ️ Nutze System-Präferenz:", systemTheme);
        setzeTheme(systemTheme);
    }
}

// === TOGGLE-BUTTON (Hell ↔ Dunkel) ===
document.getElementById("theme-toggle").addEventListener("click", function() {
    // Toggle zwischen hell und dunkel
    let neuesTheme = aktuellesTheme === "dark" ? "light" : "dark";
    setzeTheme(neuesTheme);
});

// === SYSTEM-THEME ÄNDERUNGEN BEOBACHTEN ===
if (window.matchMedia) {
    window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', function(e) {
        // Nur reagieren, wenn kein Theme gespeichert ist
        let gewaehltes = localStorage.getItem("gewaehltes-theme");
        if (!gewaehltes) {
            let neuesSystemTheme = e.matches ? "dark" : "light";
            console.log("⚙️ System-Theme geändert:", neuesSystemTheme);
            setzeTheme(neuesSystemTheme);
        }
    });
}

// === BEIM LADEN DER SEITE ===
ladeGespeichertesTheme();

console.log("✅ Theme-Switcher initialisiert");
```

Binde die Datei ein:

```html
<script src="dom.js"></script>
<script src="profil.js"></script>
<script src="projekte.js"></script>
<script src="theme-switcher.js"></script>
```

---

### Teil 5: Erweiterte Animationen (Optional, 15 Min)

F�ge flüssige Übergänge hinzu:

```javascript
// === THEME-WECHSEL MIT ANIMATION ===

function setzeThemeMitAnimation(themeName) {
    // Fade-Out Animation
    document.body.style.opacity = "0.8";
    document.body.style.transition = "opacity 0.3s ease";
    
    setTimeout(function() {
        // Theme wechseln
        setzeTheme(themeName);
        
        // Fade-In Animation
        document.body.style.opacity = "1";
    }, 150);
}

// Toggle-Button Event ersetzen mit Animation
document.getElementById("theme-toggle").addEventListener("click", function() {
    let neuesTheme = aktuellesTheme === "dark" ? "light" : "dark";
    setzeThemeMitAnimation(neuesTheme);
});
```

---

### Teil 6: Erweiterte Features (Optional, 20 Min)

Mehrere Themes und erweiterte Optionen:

```javascript
// === VERFÜGBARE THEMES ===
const themes = {
    light: { icon: "☀️", text: "Hell" },
    dark: { icon: "🌙", text: "Dunkel" },
    sepia: { icon: "📜", text: "Sepia" }
};

// Sepia-Theme in CSS definieren:
/*
[data-theme="sepia"] {
    --bg-primary: #f4ecd8;
    --text-primary: #5b4636;
    --accent-primary: #8b4513;
}
*/

// === THEME-AUSWAHL MENU ===
function erstelleThemeMenu() {
    let switcher = document.getElementById("theme-switcher");
    let menu = document.createElement("div");
    menu.className = "theme-menu versteckt";
    
    for (let theme in themes) {
        let button = document.createElement("button");
        button.textContent = themes[theme].icon + " " + themes[theme].text;
        button.setAttribute("data-theme", theme);
        button.className = "theme-option";
        
        button.addEventListener("click", function() {
            setzeTheme(theme);
            menu.classList.add("versteckt");
        });
        
        menu.appendChild(button);
    }
    
    switcher.appendChild(menu);
    
    // Menu bei Klick auf Button öffnen
    document.getElementById("theme-toggle").addEventListener("click", function(e) {
        e.stopPropagation();
        menu.classList.toggle("versteckt");
    });
    
    // Menu schliessen bei Klick ausserhalb
    document.addEventListener("click", function() {
        menu.classList.add("versteckt");
    });
}

// Beim Laden aufrufen
erstelleThemeMenu();
```

CSS für Theme-Menu:

```css
.theme-menu {
    position: absolute;
    top: 60px;
    right: 0;
    background: var(--card-bg);
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: 10px;
    min-width: 150px;
    box-shadow: 0 8px 16px var(--shadow-color);
}

.theme-menu.versteckt {
    display: none;
}

.theme-option {
    display: block;
    width: 100%;
    padding: 10px;
    background: transparent;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1em;
    color: var(--text-primary);
    transition: background 0.2s ease;
    text-align: left;
}

.theme-option:hover {
    background: var(--bg-secondary);
}
```

---

## Erfolgskriterien

- [ ] CSS Custom Properties für mindestens 2 Themes definiert
- [ ] Theme-Switcher-Button im HTML eingefügt
- [ ] theme-switcher.js erstellt und eingebunden
- [ ] Theme-Wechsel funktioniert (hell/dunkel)
- [ ] Theme-Wechsel ist animiert
- [ ] Gewähltes Theme wird in LocalStorage gespeichert
- [ ] Gespeichertes Theme wird beim Laden geladen
- [ ] System-Präferenz (prefers-color-scheme) wird erkannt
- [ ] Alle wichtigen Farben in CSS nutzen CSS-Variablen
- [ ] Button zeigt aktuelles Theme an

Bonus-Kriterien:
- [ ] Mehr als 2 Themes verfügbar
- [ ] Theme-Auswahl-Menu funktioniert
- [ ] Fade-Animation beim Wechsel
- [ ] Statistiken in Konsole

---

## Tipps

- CSS Custom Properties: var(--variable-name) greift auf Werte zu
- Data-Attribut: data-theme="dark" am <html> steuert alle Themes
- prefers-color-scheme: Browser-API für System-Theme
- matchMedia(): Hört auf Änderungen der System-Präferenz
- Transitions: Sanfte Übergänge mit transition: all 0.3s ease

Häufige Fehler:
- Vergessen, Farben in CSS-Variablen umzuwandeln
- data-theme am falschen Element (nicht <body>, sondern <html>)
- LocalStorage-Key falsch schreiben
- Transitions zu langsam (>0.5s)

---

## Reflexionsfragen

1. Warum setzen wir data-theme am <html>-Element und nicht am <body>?  
   Tipp: Was ist mit :root in CSS?

2. CSS Custom Properties vs. Klassen – was ist besser für Themes?  
   Vergleiche: .dark-theme vs. [data-theme="dark"]. Was sind Vor- und Nachteile?

3. Die prefers-color-scheme API erkennt System-Präferenzen. Welche anderen Präferenzen gibt es?  
   Recherchiere: prefers-reduced-motion, prefers-contrast

4. Wie könnte man Themes für einzelne Komponenten statt der ganzen Seite anwenden?  
   Tipp: CSS Custom Properties können auf jedem Element gesetzt werden.

5. Bonus-Challenge: Wie würdest du mehrere Themes (>3) übersichtlich anbieten?  
   Denk an UX: Dropdown, Grid, Tabs?

---

## Weiterführende Links

CSS Custom Properties:
- MDN: Using CSS Custom Properties
- CSS-Tricks: A Complete Guide to Custom Properties

System-Präferenzen:
- MDN: prefers-color-scheme
- Web.dev: prefers-color-scheme

Barrierefreiheit:
- WCAG: Color Contrast
- WebAIM: Color Contrast Checker

---

## Warum ist dieser Auftrag optional?

Dieser Auftrag geht deutlich über die Grundlagen hinaus:
- Fortgeschrittene CSS-Konzepte: Custom Properties, Data-Attribut-Selektoren
- Browser-APIs: matchMedia, prefers-color-scheme
- Komplexere Logik: State-Management, Event-Handling, Persistenz
- Best Practices: Barrierefreiheit, Performance, UX

Er ist perfekt für Lernende, die:
- Die Grundaufträge sicher beherrschen
- Mehr Herausforderung suchen
- Moderne Web-Development-Patterns lernen wollen
- Ihr Portfolio professioneller gestalten möchten

---

Geschätzte Zeit: 60-75 Minuten  
Schwierigkeitsgrad: Fortgeschritten  
Nächstes Kapitel: Event Handling – Interaktionen mit Benutzern
