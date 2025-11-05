# Auftrag 3: Farben, Schriften & Fortgeschrittene Selektoren

## Ziel
Du lernst verschiedene Farbformate kennen, stylst Schriften professionell und nutzt fortgeschrittene Selektoren wie Pseudo-Klassen, Pseudo-Elemente und Kombinatoren für präzises Styling.

## Beschreibung

Farben und Schriften machen dein Design einzigartig. Kombiniert mit fortgeschrittenen Selektoren kannst du gezielt einzelne Elemente ansprechen, ohne überall Klassen zu vergeben. In diesem Auftrag perfektionierst du das visuelle Design deines Portfolios!

---

### Teil 1: Farben in CSS – Verschiedene Formate (20 Min)

**CSS unterstützt verschiedene Farbformate:**

```css
/* ==================
   FARBFORMATE
   ================== */

/* 1. Farbnamen (140 vordefinierte Namen) */
.color-name {
    color: blue;
    background-color: lightgray;
}

/* 2. Hex-Codes (am häufigsten) */
.color-hex {
    color: #376B8C;          /* Vollständig */
    background-color: #F8F;  /* Kurzform für #FF88FF */
}

/* 3. RGB (Red, Green, Blue) */
.color-rgb {
    color: rgb(55, 107, 140);  /* Werte: 0-255 */
}

/* 4. RGBA (mit Alpha/Transparenz) */
.color-rgba {
    background-color: rgba(55, 107, 140, 0.5);  /* 50% transparent */
    color: rgba(0, 0, 0, 0.8);                   /* 80% deckend */
}

/* 5. HSL (Hue, Saturation, Lightness) */
.color-hsl {
    color: hsl(200, 44%, 38%);  /* Farbton, Sättigung, Helligkeit */
}

/* 6. HSLA (mit Alpha) */
.color-hsla {
    background-color: hsla(200, 44%, 38%, 0.3);  /* 30% transparent */
}
```

**Erstelle eine Farbpalette für dein Portfolio:**

```css
/* ==================
   FARBPALETTE MIT CSS-VARIABLEN
   ================== */

:root {
    /* Primärfarben */
    --color-primary: #376B8C;
    --color-primary-light: #4E9BCC;
    --color-primary-dark: #1F3B4E;
    
    /* Sekundärfarben */
    --color-secondary: #29786A;
    --color-secondary-light: #45BA98;
    
    /* Akzentfarben */
    --color-accent: #CD7A15;
    --color-accent-light: #FEAF51;
    
    /* Neutrale Farben */
    --color-gray-100: #F8F8F8;
    --color-gray-300: #D0D0D0;
    --color-gray-600: #666;
    --color-gray-900: #333;
    
    --color-white: #FFFFFF;
    --color-black: #000000;
    
    /* Hintergrundfarben */
    --bg-light: #FFFFFF;
    --bg-section: #F8F8F8;
    --bg-overlay: rgba(0, 0, 0, 0.5);
}

/* Variablen nutzen */
body {
    color: var(--color-gray-900);
    background-color: var(--bg-light);
}

header {
    background-color: var(--color-primary);
    color: var(--color-white);
}

.highlight {
    background-color: var(--color-accent-light);
    border-left: 4px solid var(--color-accent);
}
```

**Teste verschiedene Transparenzen:**

```css
/* ==================
   TRANSPARENZ-DEMO
   ================== */

/* Halbtransparenter Overlay für Bilder */
.image-overlay {
    position: relative;
}

.image-overlay::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(55, 107, 140, 0.7);  /* 70% transparent */
}

/* Halbtransparente Info-Box */
.info-box {
    background-color: rgba(248, 248, 248, 0.9);  /* 90% deckend */
    padding: 20px;
    border-radius: 8px;
}
```

---

### Teil 2: Schrift-Eigenschaften professionell stylen (20 Min)

**Grundlegende Schrift-Eigenschaften:**

```css
/* ==================
   SCHRIFT-STYLES
   ================== */

/* Font-Family: Schriftart wählen */
body {
    font-family: 'Arial', 'Helvetica', sans-serif;
    /* Fallback-Fonts: Wenn Arial nicht verfügbar ist, wird Helvetica verwendet */
}

/* Font-Size: Schriftgrösse */
body {
    font-size: 16px;      /* Absolut in Pixeln */
    font-size: 1rem;      /* Relativ zur Root-Schriftgrösse */
    font-size: 1.2em;     /* Relativ zum Parent-Element */
}

/* Font-Weight: Schriftdicke */
h1 {
    font-weight: 700;     /* Numerisch: 100-900 */
    font-weight: bold;    /* Keyword: normal, bold */
}

/* Font-Style: Normal, kursiv, etc. */
em {
    font-style: italic;
}

/* Line-Height: Zeilenabstand */
p {
    line-height: 1.6;     /* 1.6× Schriftgrösse */
    line-height: 24px;    /* Fixe Höhe */
}

/* Letter-Spacing: Buchstabenabstand */
h1 {
    letter-spacing: 2px;  /* Positiv = mehr Abstand */
}

.tight-text {
    letter-spacing: -0.5px;  /* Negativ = enger */
}

/* Text-Transform: Gross-/Kleinschreibung */
.uppercase {
    text-transform: uppercase;  /* ALLES GROSS */
}

.capitalize {
    text-transform: capitalize;  /* Erster Buchstabe Gross */
}

.lowercase {
    text-transform: lowercase;  /* alles klein */
}

/* Text-Align: Ausrichtung */
h1 {
    text-align: center;
}

p {
    text-align: justify;  /* Blocksatz */
}

/* Text-Decoration: Unter-/Überstreichungen */
a {
    text-decoration: none;  /* Keine Unterstreichung */
}

.underline {
    text-decoration: underline;
}

.strikethrough {
    text-decoration: line-through;
}
```

**Wende Schrift-Styles auf dein Portfolio an:**

```css
/* ==================
   PORTFOLIO TYPOGRAFIE
   ================== */

/* Basis-Schriftart für gesamte Seite */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: var(--color-gray-900);
}

/* Überschriften */
h1, h2, h3, h4, h5, h6 {
    font-family: 'Arial', 'Helvetica', sans-serif;
    line-height: 1.2;
    font-weight: 700;
}

h1 {
    font-size: 48px;
    letter-spacing: 1px;
    text-transform: uppercase;
}

h2 {
    font-size: 32px;
    letter-spacing: 0.5px;
}

h3 {
    font-size: 24px;
}

/* Navigation */
nav a {
    font-size: 16px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
}

/* Lead-Paragraph (Intro-Text) */
.lead {
    font-size: 20px;
    font-weight: 400;
    line-height: 1.8;
    color: var(--color-gray-600);
}

/* Zitate */
blockquote {
    font-size: 18px;
    font-style: italic;
    line-height: 1.8;
    color: var(--color-gray-600);
}

/* Code-Text */
code {
    font-family: 'Courier New', Courier, monospace;
    font-size: 14px;
    background-color: var(--color-gray-100);
    padding: 2px 6px;
    border-radius: 3px;
}
```

---

### Teil 3: Pseudo-Klassen – Zustände stylen (20 Min)

**Pseudo-Klassen sprechen Elemente in bestimmten Zuständen an:**

```css
/* ==================
   PSEUDO-KLASSEN
   ================== */

/* :hover – Wenn Maus darüber schwebt */
a:hover {
    color: var(--color-primary-light);
    text-decoration: underline;
}

.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
}

/* :focus – Wenn Element fokussiert ist (z.B. Eingabefeld) */
input:focus {
    border-color: var(--color-primary);
    outline: 2px solid var(--color-primary-light);
}

/* :active – Während Klick/Touch */
button:active {
    transform: scale(0.98);
}

/* :visited – Besuchte Links */
a:visited {
    color: var(--color-secondary);
}

/* :first-child – Erstes Kind-Element */
section:first-child {
    margin-top: 0;
}

p:first-child {
    font-size: 18px;
    font-weight: 500;
}

/* :last-child – Letztes Kind-Element */
section:last-child {
    margin-bottom: 0;
}

/* :nth-child() – n-tes Kind */
li:nth-child(odd) {
    background-color: var(--color-gray-100);  /* Ungerade Elemente */
}

li:nth-child(even) {
    background-color: var(--color-white);  /* Gerade Elemente */
}

li:nth-child(3) {
    font-weight: bold;  /* Genau das 3. Element */
}

/* :nth-of-type() – n-tes Element eines Typs */
p:nth-of-type(2) {
    font-style: italic;  /* Zweiter Absatz */
}

/* :not() – Negation */
a:not(.btn) {
    text-decoration: underline;  /* Alle Links AUSSER .btn */
}

li:not(:last-child) {
    border-bottom: 1px solid var(--color-gray-300);  /* Alle ausser letztes */
}
```

**Wende Pseudo-Klassen auf dein Portfolio an:**

```css
/* ==================
   PORTFOLIO PSEUDO-KLASSEN
   ================== */

/* Links: Hover & Visited */
a {
    color: var(--color-primary);
    transition: color 0.3s;
}

a:hover {
    color: var(--color-primary-light);
}

a:visited {
    color: var(--color-secondary);
}

/* Navigation: Aktiver Link */
nav a:hover {
    background-color: rgba(255, 255, 255, 0.2);
}

/* Buttons: Interaktive States */
.btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.btn:active {
    transform: translateY(0);
}

/* Cards: Hover-Effekt */
.card:hover {
    transform: scale(1.02);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

/* Listen: Zebra-Streifen */
.skill-list li:nth-child(odd) {
    background-color: var(--color-gray-100);
}

.skill-list li:nth-child(even) {
    background-color: var(--color-white);
}

/* Erster Absatz: Grösser */
section p:first-of-type {
    font-size: 18px;
    line-height: 1.8;
}

/* Letzter Absatz: Kein Margin unten */
section p:last-child {
    margin-bottom: 0;
}
```

---

### Teil 4: Pseudo-Elemente – Inhalte einfügen (15 Min)

**Pseudo-Elemente erstellen virtuelle Elemente:**

```css
/* ==================
   PSEUDO-ELEMENTE
   ================== */

/* ::before – Vor dem Inhalt */
h2::before {
    content: "→ ";
    color: var(--color-accent);
    font-weight: bold;
}

/* ::after – Nach dem Inhalt */
.external-link::after {
    content: " ↗";
    font-size: 14px;
    color: var(--color-gray-600);
}

/* ::first-letter – Erster Buchstabe */
.intro::first-letter {
    font-size: 48px;
    font-weight: bold;
    color: var(--color-primary);
    float: left;
    line-height: 1;
    margin-right: 8px;
}

/* ::first-line – Erste Zeile */
.lead::first-line {
    font-weight: 600;
    color: var(--color-primary);
}

/* ::selection – Markierter Text */
::selection {
    background-color: var(--color-primary);
    color: var(--color-white);
}

/* Dekorative Elemente mit ::before/::after */
.quote::before {
    content: """;
    font-size: 60px;
    color: var(--color-gray-300);
    position: absolute;
    top: -10px;
    left: -10px;
}

.section-divider::after {
    content: "";
    display: block;
    width: 50px;
    height: 3px;
    background-color: var(--color-primary);
    margin: 20px auto;
}
```

**Wende Pseudo-Elemente auf dein Portfolio an:**

```css
/* ==================
   PORTFOLIO PSEUDO-ELEMENTE
   ================== */

/* Überschriften: Dekorativer Unterstrich */
h2::after {
    content: "";
    display: block;
    width: 60px;
    height: 4px;
    background-color: var(--color-accent);
    margin-top: 15px;
}

/* Externe Links: Icon danach */
a[href^="http"]::after {
    content: " ↗";
    font-size: 12px;
    color: var(--color-gray-600);
}

/* Zitate: Grosse Anführungszeichen */
blockquote::before {
    content: """;
    font-size: 80px;
    color: var(--color-gray-300);
    position: absolute;
    top: -20px;
    left: -10px;
}

/* Skills: Checkmarks */
.skill-list li::before {
    content: "✓ ";
    color: var(--color-secondary);
    font-weight: bold;
}

/* Lead-Paragraph: Erster Buchstabe gross */
.intro::first-letter {
    font-size: 56px;
    font-weight: bold;
    color: var(--color-primary);
    float: left;
    line-height: 1;
    margin-right: 10px;
    margin-top: 5px;
}

/* Text-Selektion: Eigene Farbe */
::selection {
    background-color: var(--color-primary);
    color: white;
}
```

---

### Teil 5: Kombinatoren – Beziehungen ausnutzen (10 Min)

**Kombinatoren verbinden Selektoren:**

```css
/* ==================
   KOMBINATOREN
   ================== */

/* Nachfahren-Selektor (Leerzeichen) – Alle Nachfahren */
header a {
    color: white;  /* Alle Links innerhalb des Headers */
}

/* Kind-Selektor (>) – Nur direkte Kinder */
nav > ul {
    list-style: none;  /* Nur <ul>, das direktes Kind von <nav> ist */
}

/* Nachbar-Selektor (+) – Direkt folgendes Geschwister */
h2 + p {
    font-size: 18px;  /* Nur <p>, das direkt nach <h2> kommt */
}

/* Allgemeiner Geschwister-Selektor (~) – Alle folgenden Geschwister */
h2 ~ p {
    color: var(--color-gray-600);  /* Alle <p> nach einem <h2> */
}
```

**Wende Kombinatoren auf dein Portfolio an:**

```css
/* ==================
   PORTFOLIO KOMBINATOREN
   ================== */

/* Alle Links im Header: Weiss */
header a {
    color: white;
}

/* Aber nicht Links in der Navigation */
header nav a {
    color: rgba(255, 255, 255, 0.9);
}

/* Absätze direkt nach h2: Grösser */
h2 + p {
    font-size: 18px;
    line-height: 1.8;
    margin-top: 20px;
}

/* Alle Absätze nach h2 (nicht nur der erste) */
h2 ~ p {
    color: var(--color-gray-700);
}

/* Nur direkte Listen-Kinder der Navigation */
nav > ul {
    display: flex;
    gap: 20px;
}

/* Cards innerhalb der Projekt-Sektion */
#projekte .card {
    border-left: 4px solid var(--color-accent);
}

/* Bilder innerhalb von Cards */
.card img {
    border-radius: 4px;
    margin-bottom: 15px;
}
```

---

## Erfolgskriterien

- [ ] Mindestens 3 verschiedene Farbformate sind verwendet (Hex, RGB, RGBA)
- [ ] CSS-Variablen für Farben sind definiert und genutzt
- [ ] Schrift-Eigenschaften (font-family, font-size, font-weight, line-height) sind auf mindestens 5 Elementen angewendet
- [ ] Mindestens 5 Pseudo-Klassen sind implementiert (:hover, :first-child, :nth-child, etc.)
- [ ] Mindestens 3 Pseudo-Elemente sind genutzt (::before, ::after, ::first-letter)
- [ ] Mindestens 3 Kombinatoren sind eingesetzt (Nachfahren, Kind, Nachbar)
- [ ] Die Seite hat ein konsistentes, professionelles Farbschema
- [ ] Hover-Effekte machen die Seite interaktiv

## Tipps

- **Farbpaletten-Tools:** Nutze [Coolors.co](https://coolors.co) oder [Adobe Color](https://color.adobe.com) für harmonische Farbkombinationen
- **Transparenz:** RGBA/HSLA ist perfekt für Overlays und halbtransparente Hintergründe
- **Schrift-Paarungen:** Kombiniere eine Serif- mit einer Sans-Serif-Schrift (z.B. Georgia + Arial)
- **Pseudo-Klassen-Reihenfolge:** :link → :visited → :hover → :active (LVHA)
- **DevTools:** Aktiviere `:hover` manuell in den DevTools, um Hover-States zu inspizieren
- **Profitipp:** Nutze `::selection` für eigene Farben bei markiertem Text

## Reflexionsfragen

1. Was ist der Unterschied zwischen `rgb(255, 0, 0)` und `rgba(255, 0, 0, 0.5)`?
2. Experimentiere: Ändere `:nth-child(odd)` auf `:nth-child(3n)`. Was passiert?
3. Was ist der Unterschied zwischen `section p` und `section > p`?
4. Teste: Füge einem Link `::before { content: "→ "; }` hinzu. Wo erscheint der Pfeil?
5. Warum sollte man CSS-Variablen nutzen statt Farben direkt zu schreiben?
6. Öffne DevTools → Elements → Wähle ein Element mit :hover-Effekt → Aktiviere :hov → Teste verschiedene States

## Weiterführende Links

**Farben:**
- [MDN: Color](https://developer.mozilla.org/en-US/docs/Web/CSS/color)
- [MDN: CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [Coolors.co](https://coolors.co) – Farbpaletten-Generator
- [Adobe Color](https://color.adobe.com) – Farbharmonien erstellen

**Schriften:**
- [MDN: font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family)
- [Google Fonts](https://fonts.google.com) – Kostenlose Webfonts
- [CSS Tricks: Typography](https://css-tricks.com/snippets/css/css-typography-cheat-sheet/)

**Pseudo-Klassen & -Elemente:**
- [MDN: Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- [MDN: Pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
- [CSS Tricks: A Complete Guide to Pseudo-Elements](https://css-tricks.com/pseudo-element-roundup/)

**Selektoren & Kombinatoren:**
- [MDN: CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Tricks: Child and Sibling Selectors](https://css-tricks.com/child-and-sibling-selectors/)
- [CSS Diner](https://flukeout.github.io/) – Interaktives Spiel zum Lernen von Selektoren

**Tools:**
- [CSS Stats](https://cssstats.com/) – Analysiere dein CSS
- [Contrast Checker](https://webaim.org/resources/contrastchecker/) – Prüfe Farbkontraste für Accessibility

---

**Geschätzte Zeit:** 55-60 Minuten  
**Nächster Schritt:** Glückwunsch! Du beherrschst CSS-Selektoren und -Eigenschaften. Weiter mit CSS-Layouts (Flexbox & Grid)!