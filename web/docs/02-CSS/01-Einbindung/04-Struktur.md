# Auftrag 4 (Optional): CSS-Organisation & Best Practices – Professionelle Strukturierung

## Ziel
Du lernst fortgeschrittene Techniken zur Organisation von CSS-Code, verstehst Best Practices und kannst dein Stylesheet wie ein Profi strukturieren. Dieser Auftrag bereitet dich auf grössere Projekte vor.

## Beschreibung

Du kennst jetzt die drei Arten der CSS-Einbindung. In diesem optionalen Auftrag lernst du, wie Profis ihre CSS-Dateien organisieren, um auch bei grossen Projekten den Überblick zu behalten.

---

### Teil 1: CSS-Reset & Normalisierung (15 Min)

Browser haben unterschiedliche Standard-Styles. Ein CSS-Reset sorgt für Konsistenz.

**Erstelle `reset.css` im Projektordner:**

```css
/* ==================
   CSS RESET
   Basiert auf: Meyer Reset & Normalize.css
   ================== */

/* Box-Sizing für alle Elemente */
*, *::before, *::after {
    box-sizing: border-box;
}

/* Margins & Paddings zurücksetzen */
* {
    margin: 0;
    padding: 0;
}

/* HTML & Body */
html {
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

body {
    line-height: 1.6;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 
                 'Helvetica Neue', Arial, sans-serif;
    min-height: 100vh;
}

/* Listen */
ul, ol {
    list-style: none;
}

/* Links */
a {
    text-decoration: none;
    color: inherit;
}

/* Bilder & Medien */
img, picture, video, canvas, svg {
    display: block;
    max-width: 100%;
    height: auto;
}

/* Buttons & Inputs */
button, input, textarea, select {
    font: inherit;
    color: inherit;
}

/* Tabellen */
table {
    border-collapse: collapse;
    border-spacing: 0;
}

/* Formulare */
input, button, textarea, select {
    background: none;
    border: none;
    outline: none;
}
```

**Binde `reset.css` VOR `styles.css` ein:**

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dein Name - Portfolio</title>
    
    <!-- CSS-Reset zuerst -->
    <link rel="stylesheet" href="reset.css">
    
    <!-- Dann deine eigenen Styles -->
    <link rel="stylesheet" href="styles.css">
</head>
```

**Warum wichtig?**
- Konsistentes Verhalten in allen Browsern
- Vorhersagbare Abstände und Grössen
- Professionelle Basis für eigene Styles

---

### Teil 2: CSS-Variablen (Custom Properties) (20 Min)

Statt Farben überall zu wiederholen, definierst du sie zentral.

**Füge am Anfang von `styles.css` hinzu:**

```css
/* ==================
   CSS VARIABLEN
   ================== */
:root {
    /* Farben */
    --color-primary: #376B8C;
    --color-primary-light: #4E9BCC;
    --color-primary-dark: #1F3B4E;
    
    --color-secondary: #29786A;
    --color-secondary-light: #45BA98;
    
    --color-accent: #CD7A15;
    --color-accent-light: #FEAF51;
    
    --color-gray-100: #F8F8F8;
    --color-gray-300: #D0D0D0;
    --color-gray-600: #666;
    --color-gray-900: #333;
    
    --color-white: #FFFFFF;
    --color-black: #000000;
    
    /* Typografie */
    --font-family: Arial, sans-serif;
    --font-size-base: 16px;
    --font-size-sm: 14px;
    --font-size-lg: 18px;
    --font-size-xl: 24px;
    --font-size-2xl: 32px;
    --font-size-3xl: 48px;
    
    --line-height: 1.6;
    --line-height-heading: 1.2;
    
    /* Abstände */
    --spacing-xs: 8px;
    --spacing-sm: 12px;
    --spacing-md: 20px;
    --spacing-lg: 40px;
    --spacing-xl: 60px;
    
    /* Border Radius */
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 12px;
    
    /* Shadows */
    --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
    --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.15);
    
    /* Transitions */
    --transition-fast: 0.15s ease;
    --transition-base: 0.3s ease;
    --transition-slow: 0.5s ease;
}
```

**Nutze die Variablen in deinem CSS:**

```css
/* Vorher */
h1 {
    color: #376B8C;
    font-size: 48px;
}

/* Nachher */
h1 {
    color: var(--color-primary);
    font-size: var(--font-size-3xl);
}

/* Vorher */
header {
    background-color: #376B8C;
    padding: 60px 20px;
}

/* Nachher */
header {
    background-color: var(--color-primary);
    padding: var(--spacing-xl) var(--spacing-md);
}
```

**Vorteile:**
- Farbe ändern? Nur an einer Stelle!
- Konsistente Abstände und Grössen
- Einfaches Umschalten zwischen Themes möglich

---

### Teil 3: BEM-Naming-Convention (20 Min)

BEM (Block Element Modifier) ist eine Namenskonvention für CSS-Klassen.

**Struktur:**
- **Block:** Hauptkomponente (z.B. `card`)
- **Element:** Teil des Blocks (z.B. `card__title`)
- **Modifier:** Variation (z.B. `card--featured`)

**Beispiel: Projekt-Karte mit BEM:**

**HTML:**
```html
<article class="card card--featured">
    <img src="projekt.jpg" alt="Projekt" class="card__image">
    <div class="card__content">
        <h3 class="card__title">Portfolio-Website</h3>
        <p class="card__description">Meine erste eigene Website...</p>
        <a href="#" class="card__link">Mehr erfahren →</a>
    </div>
</article>
```

**CSS:**
```css
/* Block */
.card {
    background-color: var(--color-gray-100);
    border: 1px solid var(--color-gray-300);
    border-radius: var(--radius-md);
    padding: var(--spacing-md);
    margin-bottom: var(--spacing-lg);
}

/* Element */
.card__image {
    width: 100%;
    border-radius: var(--radius-sm);
    margin-bottom: var(--spacing-sm);
}

.card__content {
    padding: var(--spacing-sm);
}

.card__title {
    color: var(--color-primary);
    font-size: var(--font-size-xl);
    margin-bottom: var(--spacing-xs);
}

.card__description {
    color: var(--color-gray-600);
    margin-bottom: var(--spacing-md);
}

.card__link {
    color: var(--color-primary);
    font-weight: bold;
    transition: color var(--transition-base);
}

.card__link:hover {
    color: var(--color-primary-light);
}

/* Modifier */
.card--featured {
    border: 2px solid var(--color-accent);
    background-color: var(--color-white);
    box-shadow: var(--shadow-lg);
}
```

**Vorteile:**
- Klare Hierarchie
- Keine Namenskonflikte
- Wiederverwendbare Komponenten

---

### Teil 4: Modulare CSS-Struktur (15 Min)

Für grosse Projekte: Mehrere CSS-Dateien!

**Projektstruktur:**
```
mein-portfolio/
├── index.html
├── about.html
└── css/
    ├── reset.css
    ├── variables.css
    ├── base.css
    ├── components/
    │   ├── header.css
    │   ├── nav.css
    │   ├── card.css
    │   └── footer.css
    └── main.css (importiert alle)
```

**main.css:**
```css
/* ==================
   MAIN STYLESHEET
   Importiert alle Module
   ================== */

/* Reset & Variablen */
@import url('reset.css');
@import url('variables.css');
@import url('base.css');

/* Komponenten */
@import url('components/header.css');
@import url('components/nav.css');
@import url('components/card.css');
@import url('components/footer.css');
```

**Im HTML nur eine Datei einbinden:**
```html
<link rel="stylesheet" href="css/main.css">
```

---

### Teil 5: CSS-Kommentare & Dokumentation (10 Min)

**Gute Kommentare helfen dir und anderen:**

```css
/* ==================
   KOMPONENTE: CARD
   
   Verwendung:
   <article class="card">
     <h3 class="card__title">Titel</h3>
     <p class="card__description">Text</p>
   </article>
   
   Modifier:
   - card--featured: Hervorgehobene Karte
   - card--compact: Kleinere Version
   ================== */

.card {
    /* Layout */
    display: flex;
    flex-direction: column;
    
    /* Spacing */
    padding: var(--spacing-md);
    margin-bottom: var(--spacing-lg);
    
    /* Visuals */
    background-color: var(--color-gray-100);
    border: 1px solid var(--color-gray-300);
    border-radius: var(--radius-md);
    
    /* Interaktion */
    transition: transform var(--transition-base);
}

/* Hover-Effekt: Leicht anheben */
.card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
}
```

---

## Erfolgskriterien

- [ ] Ein CSS-Reset (`reset.css`) ist eingebunden
- [ ] CSS-Variablen sind definiert und werden genutzt
- [ ] Mindestens 3 Komponenten nutzen BEM-Naming
- [ ] CSS ist modular strukturiert (mehrere Dateien)
- [ ] Aussagekräftige Kommentare dokumentieren komplexe Bereiche
- [ ] Alle Farben, Abstände und Schriftgrössen nutzen Variablen
- [ ] Die Seite funktioniert weiterhin einwandfrei

## Tipps

- **CSS-Variablen:** In DevTools kannst du Variablen-Werte live ändern!
- **@import:** Kann Performance-Probleme verursachen – für Production lieber zusammenführen
- **BEM:** Nutze ein Plugin in VS Code für Autovervollständigung (z.B. "BEM Helper")
- **CSS-Linter:** Installiere "Stylelint" in VS Code für automatische Code-Qualitätsprüfung
- **Profitipp:** Nutze Sass/SCSS für noch bessere Organisation (lernst du später!)

## Reflexionsfragen

1. Was ist der Vorteil von CSS-Variablen gegenüber fest definierten Werten?
2. Vergleiche: Element-Selektoren (`h1`) vs. Klassen-Selektoren (`.card__title`). Was ist flexibler?
3. Experimentiere: Ändere `--color-primary` auf Rot. Wie viele Elemente ändern sich?
4. Was ist der Unterschied zwischen `card__title` (Element) und `card--featured` (Modifier)?
5. Warum ist modulares CSS besser für Teams? Überlege dir Vorteile.

## Weiterführende Links

- [MDN: CSS Custom Properties (Variablen)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [BEM Methodology](http://getbem.com/)
- [CSS Guidelines by Harry Roberts](https://cssguidelin.es/)
- [SMACSS (Scalable CSS Architecture)](http://smacss.com/)
- [ITCSS (Inverted Triangle CSS)](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)
- [Stylelint](https://stylelint.io/) – CSS-Linter
- [Sass Documentation](https://sass-lang.com/) – CSS-Präprozessor (Vorschau)

## Bonus-Challenges

**Challenge 1: Dark Mode mit CSS-Variablen**
- Erstelle ein zweites Farbschema für Dark Mode
- Nutze `prefers-color-scheme` Media Query
- Alle Farben sollen automatisch umschalten

**Challenge 2: Component Library**
- Erstelle eine HTML-Seite mit allen Komponenten (Button, Card, Header, etc.)
- Dokumentiere jede Komponente mit Code-Beispielen
- Nutze das als Referenz für zukünftige Projekte

**Challenge 3: Performance-Optimierung**
- Kombiniere alle CSS-Dateien in eine einzige für Production
- Minifiziere das CSS (entferne Kommentare, Whitespace)
- Vergleiche die Dateigrösse vorher/nachher

**Challenge 4: CSS-Styleguide**
- Erstelle ein Dokument mit deinen Namenskonventionen
- Definiere Regeln für Kommentare, Einrückung, Reihenfolge
- Teile es mit deinem Team oder nutze es als Referenz

---

**⏱️ Geschätzte Zeit:** 60-75 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächster Schritt:** Glückwunsch! Du beherrschst CSS-Einbindung und Organisation. Weiter mit CSS-Selektoren & Eigenschaften!

---

**Hinweis:** Diese Techniken sind optional für Anfänger, aber essentiell für professionelle Projekte. Du wirst sie im Laufe deiner Ausbildung immer mehr nutzen!
