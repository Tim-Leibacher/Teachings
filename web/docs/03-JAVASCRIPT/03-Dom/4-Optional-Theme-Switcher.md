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

## Teil 1: CSS-Custom Properties einrichten (20 Min)

### Aufgabe 1.1: CSS-Variablen für Hell-Theme

**Deine Aufgabe:**
Erstelle oder erweitere deine `styles.css` mit CSS Custom Properties (CSS-Variablen) für ein Hell-Theme:

Definiere im `:root` mindestens:
- Hintergrund-Farben (primär, sekundär, tertiär)
- Text-Farben (primär, sekundär, tertiär)
- Akzent-Farben (primär, sekundär)
- Border- und Shadow-Farben
- Transition-Geschwindigkeit

**Wo nachschlagen:**
- [MDN: CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN: :root](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)
- [CSS-Tricks: A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)

**Hinweise:**
- Nutze `--variable-name` für Custom Properties
- Definiere sie in `:root` für globale Verfügbarkeit
- Wähle konsistente Farbschemata

<details>
<summary>💡 Beispiel-Struktur anzeigen</summary>

```css
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
    
    --border-color: #dee2e6;
    --shadow-color: rgba(0, 0, 0, 0.1);
    
    --transition-speed: 0.3s;
}
```
</details>

### Aufgabe 1.2: CSS-Variablen für Dunkel-Theme

**Deine Aufgabe:**
Erstelle ein zweites Theme-Set mit dem Attribut-Selektor `[data-theme="dark"]`. Definiere die gleichen Variablen mit anderen Werten für ein dunkles Farbschema.

**Hinweise:**
- Dunkle Hintergründe, helle Texte
- Reduziere Kontrast für Akzent-Farben
- Stärkere Schatten

<details>
<summary>💡 Beispiel anzeigen</summary>

```css
[data-theme="dark"] {
    --bg-primary: #1a1a1a;
    --bg-secondary: #2c2c2c;
    --bg-tertiary: #3a3a3a;
    
    --text-primary: #f5f5f5;
    --text-secondary: #b0b0b0;
    --text-tertiary: #808080;
    
    --accent-primary: #4da6ff;
    --accent-secondary: #33d4ff;
    
    --border-color: #4a4a4a;
    --shadow-color: rgba(0, 0, 0, 0.5);
}
```
</details>

### Aufgabe 1.3: Variablen in existierendem CSS nutzen

**Deine Aufgabe:**
Ersetze alle hardcodierten Farben in deinem CSS durch `var(--variable-name)`.

Mindestens für:
- `body` (background-color, color)
- `section` (background, border, box-shadow)
- Überschriften (color)
- Links (color)
- Buttons (background, color)

**Wo nachschlagen:**
- [MDN: var()](https://developer.mozilla.org/en-US/docs/Web/CSS/var)

**Hinweise:**
- Füge `transition` für smooth theme-changes hinzu

<details>
<summary>💡 Beispiel anzeigen</summary>

```css
body {
    background-color: var(--bg-primary);
    color: var(--text-primary);
    transition: background-color var(--transition-speed) ease,
                color var(--transition-speed) ease;
}

section {
    background-color: var(--bg-secondary);
    border: 1px solid var(--border-color);
    box-shadow: 0 2px 4px var(--shadow-color);
}

h1, h2, h3 {
    color: var(--accent-primary);
}

a {
    color: var(--accent-primary);
    transition: color var(--transition-speed) ease;
}
```
</details>

---

## Teil 2: HTML für Theme-Switcher (5 Min)

Füge eine Theme-Switcher-Komponente in dein HTML ein (z.B. im Header):

```html
<div id="theme-switcher">
    <button id="theme-toggle" class="theme-button" aria-label="Theme wechseln">
        <span class="theme-icon">🌙</span>
        <span class="theme-text">Dunkel</span>
    </button>
</div>
```

---

## Teil 3: CSS für Theme-Switcher (10 Min)

**Deine Aufgabe:**
Erstelle Styles für den Theme-Switcher-Button:
- Fixed Position (oben rechts)
- Flexbox-Layout für Icon und Text
- Hover- und Active-States
- Smooth transitions

**Wo nachschlagen:**
- [MDN: position: fixed](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [MDN: z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
- [CSS-Tricks: Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

**Hinweise:**
- Button sollte über anderen Elementen sein (`z-index: 1000`)
- Nutze CSS-Variablen für Farben
- Hover-Effekt: leicht hochschweben

<details>
<summary>💡 Beispiel anzeigen</summary>

```css
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
    background: var(--bg-secondary);
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
</details>

---

## Teil 4: JavaScript für Theme-Switcher (30 Min)

Erstelle `theme-switcher.js`.

### Aufgabe 4.1: Theme-Variablen und System-Präferenz

**Deine Aufgabe:**
1. Erstelle eine Variable `aktuellesTheme`
2. Implementiere die Funktion `getSystemTheme()`, die die Browser-Präferenz erkennt

**Wo nachschlagen:**
- [MDN: Window.matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia)
- [MDN: prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)
- [Web.dev: prefers-color-scheme](https://web.dev/prefers-color-scheme/)

**Hinweise:**
- `window.matchMedia('(prefers-color-scheme: dark)')` prüft System-Theme
- `.matches` gibt `true/false` zurück

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
console.log("🎨 Theme-Switcher geladen");

let aktuellesTheme = "light";

function getSystemTheme() {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
        return "dark";
    }
    return "light";
}
```
</details>

### Aufgabe 4.2: Theme setzen

**Deine Aufgabe:**
Erstelle die Funktion `setzeTheme(themeName)`, die:
1. Das `data-theme` Attribut am `<html>`-Element setzt
2. Die Variable `aktuellesTheme` aktualisiert
3. Den Button (Icon und Text) aktualisiert
4. Das Theme in LocalStorage speichert

**Wo nachschlagen:**
- [MDN: Element.setAttribute](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)
- [MDN: document.documentElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/documentElement)
- [MDN: localStorage.setItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/setItem)

**Hinweise:**
- `document.documentElement` ist das `<html>`-Element
- Button-Update: Icon ☀️ für Hell, 🌙 für Dunkel
- Speichere mit Key `"gewaehltes-theme"`

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function setzeTheme(themeName) {
    console.log("🎨 Setze Theme:", themeName);
    
    // Theme am <html>-Element setzen
    document.documentElement.setAttribute("data-theme", themeName);
    
    // Aktuelles Theme speichern
    aktuellesTheme = themeName;
    
    // Button-Text und Icon aktualisieren
    let button = document.getElementById("theme-toggle");
    let icon = button.querySelector(".theme-icon");
    let text = button.querySelector(".theme-text");
    
    if (themeName === "dark") {
        icon.textContent = "☀️";
        text.textContent = "Hell";
    } else {
        icon.textContent = "🌙";
        text.textContent = "Dunkel";
    }
    
    // Theme in LocalStorage speichern
    localStorage.setItem("gewaehltes-theme", themeName);
    
    console.log("✅ Theme aktiviert:", themeName);
}
```
</details>

### Aufgabe 4.3: Gespeichertes Theme laden

**Deine Aufgabe:**
Erstelle die Funktion `ladeGespeichertesTheme()`, die:
1. Prüft ob ein Theme in LocalStorage gespeichert ist
2. Wenn ja: lädt dieses Theme
3. Wenn nein: nutzt System-Präferenz

**Wo nachschlagen:**
- [MDN: localStorage.getItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/getItem)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function ladeGespeichertesTheme() {
    let gespeichert = localStorage.getItem("gewaehltes-theme");
    
    if (gespeichert) {
        console.log("📂 Lade gespeichertes Theme:", gespeichert);
        setzeTheme(gespeichert);
    } else {
        let systemTheme = getSystemTheme();
        console.log("ℹ️ Nutze System-Präferenz:", systemTheme);
        setzeTheme(systemTheme);
    }
}
```
</details>

### Aufgabe 4.4: Toggle-Button

**Deine Aufgabe:**
Füge einen Event-Listener zum Button hinzu, der zwischen Hell und Dunkel wechselt.

**Hinweise:**
- Toggle-Logik: `aktuellesTheme === "dark" ? "light" : "dark"`

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
document.getElementById("theme-toggle").addEventListener("click", function() {
    let neuesTheme = aktuellesTheme === "dark" ? "light" : "dark";
    setzeTheme(neuesTheme);
});
```
</details>

### Aufgabe 4.5: System-Theme Änderungen beobachten

**Deine Aufgabe:**
Füge einen Listener hinzu, der auf Änderungen der System-Präferenz reagiert (nur wenn kein Theme gespeichert ist).

**Wo nachschlagen:**
- [MDN: MediaQueryList.addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList/addEventListener)
- [MDN: change event (MediaQueryList)](https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList/change_event)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
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
```
</details>

### Aufgabe 4.6: Initialisierung

**Deine Aufgabe:**
Rufe beim Laden der Seite `ladeGespeichertesTheme()` auf.

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
ladeGespeichertesTheme();
console.log("✅ Theme-Switcher initialisiert");
```
</details>

**Binde die Datei ein:**

```html
<script src="dom.js"></script>
<script src="profil.js"></script>
<script src="projekte.js"></script>
<script src="theme-switcher.js"></script>
```

---

## Teil 5: Erweiterte Animationen (Optional, 15 Min)

### Aufgabe 5.1: Fade-Animation beim Wechsel

**Deine Aufgabe:**
Erweitere die `setzeTheme()` Funktion mit einer Fade-Animation:
1. Fade-Out (opacity: 0.8)
2. Theme wechseln (nach 150ms)
3. Fade-In (opacity: 1)

**Wo nachschlagen:**
- [MDN: HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
- [MDN: setTimeout](https://developer.mozilla.org/de/docs/Web/API/setTimeout)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
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

// Toggle-Button Event ersetzen
document.getElementById("theme-toggle").addEventListener("click", function() {
    let neuesTheme = aktuellesTheme === "dark" ? "light" : "dark";
    setzeThemeMitAnimation(neuesTheme);
});
```
</details>

---

## Teil 6: Mehrere Themes (Optional, 25 Min)

### Aufgabe 6.1: Drittes Theme hinzufügen

**Deine Aufgabe:**
1. Füge ein "Sepia"-Theme in CSS hinzu (`[data-theme="sepia"]`)
2. Erstelle ein Objekt mit allen verfügbaren Themes
3. Erweitere die Button-Logik für Rotation durch alle Themes

**Wo nachschlagen:**
- [MDN: Array.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [Modulo Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder)

**CSS-Beispiel für Sepia:**
```css
[data-theme="sepia"] {
    --bg-primary: #f4ecd8;
    --bg-secondary: #e8ddc7;
    --text-primary: #5b4636;
    --accent-primary: #8b4513;
    /* ... */
}
```

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
const themes = ["light", "dark", "sepia"];
const themeIcons = {
    light: "🌙",
    dark: "📜",
    sepia: "☀️"
};
const themeTexte = {
    light: "Dunkel",
    dark: "Sepia",
    sepia: "Hell"
};

document.getElementById("theme-toggle").addEventListener("click", function() {
    let index = themes.indexOf(aktuellesTheme);
    let naechsterIndex = (index + 1) % themes.length;
    let neuesTheme = themes[naechsterIndex];
    
    setzeTheme(neuesTheme);
    
    // Button aktualisieren
    let icon = this.querySelector(".theme-icon");
    let text = this.querySelector(".theme-text");
    icon.textContent = themeIcons[neuesTheme];
    text.textContent = themeTexte[neuesTheme];
});
```
</details>

### Aufgabe 6.2: Theme-Auswahl-Menu (Advanced)

**Deine Aufgabe:**
Erstelle ein Dropdown-Menu mit allen verfügbaren Themes.

**Hinweise:**
- Erstelle das Menu dynamisch per JavaScript
- Zeige/Verstecke es beim Klick auf den Button
- Schliesse es bei Klick ausserhalb

**Wo nachschlagen:**
- [MDN: Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
- [MDN: Event.stopPropagation](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function erstelleThemeMenu() {
    let switcher = document.getElementById("theme-switcher");
    let menu = document.createElement("div");
    menu.className = "theme-menu versteckt";
    
    themes.forEach(function(theme) {
        let button = document.createElement("button");
        button.textContent = themeIcons[theme] + " " + theme.charAt(0).toUpperCase() + theme.slice(1);
        button.className = "theme-option";
        
        button.addEventListener("click", function() {
            setzeTheme(theme);
            menu.classList.add("versteckt");
        });
        
        menu.appendChild(button);
    });
    
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

erstelleThemeMenu();
```

CSS für Menu:
```css
.theme-menu {
    position: absolute;
    top: 60px;
    right: 0;
    background: var(--bg-secondary);
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
    cursor: pointer;
    color: var(--text-primary);
    transition: background 0.2s ease;
}

.theme-option:hover {
    background: var(--bg-tertiary);
}
```
</details>

---

## Erfolgskriterien

- [ ] CSS Custom Properties für mindestens 2 Themes definiert
- [ ] Alle Farben in CSS nutzen CSS-Variablen
- [ ] Theme-Switcher-Button im HTML eingefügt
- [ ] `theme-switcher.js` erstellt und eingebunden
- [ ] Theme-Wechsel funktioniert (hell/dunkel)
- [ ] Gewähltes Theme wird in LocalStorage gespeichert
- [ ] Gespeichertes Theme wird beim Laden geladen
- [ ] System-Präferenz (prefers-color-scheme) wird erkannt
- [ ] Button zeigt aktuelles Theme an
- [ ] Smooth transitions beim Wechsel

Bonus-Kriterien:
- [ ] Mehr als 2 Themes verfügbar
- [ ] Theme-Auswahl-Menu funktioniert
- [ ] Fade-Animation beim Wechsel

---

## Tipps & Troubleshooting

### Häufige Fehler:
- **Theme wechselt nicht?** → Prüfe ob `data-theme` am `<html>`-Element gesetzt wird
- **Farben ändern sich nicht?** → Prüfe ob alle Styles `var(--variable)` nutzen
- **System-Theme wird nicht erkannt?** → Prüfe Browser-Support für `matchMedia`
- **Button zeigt falsches Theme?** → Prüfe Button-Update-Logik

### Browser-Support:
- CSS Custom Properties: Alle modernen Browser
- `prefers-color-scheme`: IE11 nicht unterstützt
- `matchMedia`: Alle modernen Browser

### Performance:
- CSS-Variablen sind sehr performant
- Transitions sollten nicht zu langsam sein (<0.5s)
- Vermeide zu viele gleichzeitige Transitions

### Wichtige Konzepte:
- **CSS Custom Properties:** Wiederverwendbare CSS-Werte
- **Data-Attribute:** `data-theme` steuert Theme
- **prefers-color-scheme:** Browser-API für System-Theme
- **LocalStorage:** Speichert Benutzer-Präferenz

---

## Reflexionsfragen

1. **Warum setzen wir `data-theme` am `<html>`-Element und nicht am `<body>`?**  
   *Tipp: Was ist mit `:root` in CSS?*

2. **CSS Custom Properties vs. Klassen – was ist besser für Themes?**  
   *Vergleiche: `.dark-theme` vs. `[data-theme="dark"]`. Was sind Vor- und Nachteile?*

3. **Die `prefers-color-scheme` API erkennt System-Präferenzen. Welche anderen Präferenzen gibt es?**  
   *Recherchiere: `prefers-reduced-motion`, `prefers-contrast`*

4. **Wie könnte man Themes für einzelne Komponenten statt der ganzen Seite anwenden?**  
   *Tipp: CSS Custom Properties können auf jedem Element gesetzt werden.*

5. **Bonus-Challenge: Wie würdest du mehrere Themes (>3) übersichtlich anbieten?**  
   *Denk an UX: Dropdown, Grid, Tabs?*

---

## Weiterführende Links

**CSS Custom Properties:**
- [MDN: Using CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS-Tricks: A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)
- [Web.dev: CSS Custom Properties](https://web.dev/css-variables/)

**System-Präferenzen:**
- [MDN: prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)
- [Web.dev: prefers-color-scheme Guide](https://web.dev/prefers-color-scheme/)
- [MDN: prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)

**Barrierefreiheit:**
- [WCAG: Color Contrast](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WebAIM: Color Contrast Checker](https://webaim.org/resources/contrastchecker/)

**Best Practices:**
- [Web.dev: Building a Theme Switch](https://web.dev/building-a-theme-switch-component/)
- [CSS-Tricks: Dark Mode](https://css-tricks.com/a-complete-guide-to-dark-mode-on-the-web/)

---

## Warum ist dieser Auftrag optional?

Dieser Auftrag geht deutlich über die Grundlagen hinaus:
- Fortgeschrittene CSS-Konzepte: Custom Properties, Data-Attribut-Selektoren
- Browser-APIs: `matchMedia`, `prefers-color-scheme`
- Komplexere Logik: State-Management, Event-Handling, Persistenz
- Best Practices: Barrierefreiheit, Performance, UX

Er ist perfekt für Lernende, die:
- Die Grundaufträge sicher beherrschen
- Mehr Herausforderung suchen
- Moderne Web-Development-Patterns lernen wollen
- Ihr Portfolio professioneller gestalten möchten

---

**⏱️ Geschätzte Zeit:** 90-110 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächstes Kapitel:** Event Handling – Interaktionen mit Benutzern