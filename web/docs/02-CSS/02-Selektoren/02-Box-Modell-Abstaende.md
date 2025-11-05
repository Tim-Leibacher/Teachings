# Auftrag 2: Box-Modell und Abstände – Layouts verstehen

## Ziel
Du verstehst das CSS-Box-Modell mit Content, Padding, Border und Margin. Du lernst, wie Abstände das Layout beeinflussen und kannst gezielt Raum um Elemente schaffen.

## Beschreibung

Jedes HTML-Element ist eine rechteckige Box. Das Box-Modell beschreibt, wie diese Box aufgebaut ist: Inhaltsbereich, Innenabstand (Padding), Rahmen (Border) und Aussenabstand (Margin). Dieses Wissen ist fundamental für jedes CSS-Layout!

---

### Teil 1: Das Box-Modell verstehen (15 Min)

**Die vier Bereiche einer Box:**

```
┌─────────────── MARGIN (Aussenabstand) ───────────────┐
│ ┌─────────────── BORDER (Rahmen) ─────────────────┐ │
│ │ ┌─────────────── PADDING (Innenabstand) ──────┐ │ │
│ │ │ ┌────────────────────────────────────────┐ │ │ │
│ │ │ │         CONTENT (Inhalt)               │ │ │ │
│ │ │ │                                        │ │ │ │
│ │ │ └────────────────────────────────────────┘ │ │ │
│ │ └──────────────────────────────────────────────┘ │ │
│ └────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────┘
```

**Erstelle eine Demo-Box in deiner `index.html`:**

```html
<section id="box-modell-demo">
    <h2>Box-Modell Demo</h2>
    
    <div class="demo-box">
        Dieser Text ist der CONTENT. Drumherum ist Padding, dann Border, dann Margin.
    </div>
</section>
```

**Style die Demo-Box in `styles.css`:**

```css
/* ==================
   BOX-MODELL DEMO
   ================== */

.demo-box {
    /* Content-Grösse */
    width: 300px;
    
    /* Padding: Abstand zwischen Content und Border */
    padding: 20px;
    
    /* Border: Rahmen um die Box */
    border: 5px solid #376B8C;
    
    /* Margin: Abstand zu anderen Elementen */
    margin: 40px auto;
    
    /* Weitere Styles für Sichtbarkeit */
    background-color: #E8F4F8;
    color: #1F3B4E;
    font-weight: bold;
}
```

**Öffne die DevTools (F12) → Elements → Wähle die .demo-box:**
- Du siehst das Box-Modell visuell dargestellt
- Content: 300px × Höhe
- Padding: 20px auf allen Seiten
- Border: 5px auf allen Seiten
- Margin: 40px oben/unten, automatisch links/rechts (zentriert)

**Gesamtbreite der Box:**
- Content: 300px
- Padding links: 20px
- Padding rechts: 20px
- Border links: 5px
- Border rechts: 5px
- **Total: 350px**

---

### Teil 2: Padding – Innenabstand (15 Min)

**Padding schafft Luft zwischen Inhalt und Rahmen.**

**Verschiedene Padding-Notationen:**

```css
/* Alle vier Seiten gleich */
.box-1 {
    padding: 20px;
}

/* Vertikal | Horizontal */
.box-2 {
    padding: 20px 40px;  /* Oben/Unten: 20px, Links/Rechts: 40px */
}

/* Oben | Horizontal | Unten */
.box-3 {
    padding: 10px 20px 30px;  /* Oben: 10px, Links/Rechts: 20px, Unten: 30px */
}

/* Oben | Rechts | Unten | Links (im Uhrzeigersinn) */
.box-4 {
    padding: 10px 20px 30px 40px;
}

/* Einzeln setzen */
.box-5 {
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 30px;
    padding-left: 40px;
}
```

**Wende Padding auf deine Projekt-Karten an:**

```css
/* ==================
   CARD MIT PADDING
   ================== */

.card {
    background-color: #F8F8F8;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    
    /* Gleichmässiger Innenabstand */
    padding: 30px;
    
    margin-bottom: 30px;
}

/* Card-Header: Weniger Padding unten */
.card-header {
    padding: 0 0 20px 0;
    border-bottom: 2px solid #D0D0D0;
    margin-bottom: 20px;
}

/* Card-Footer: Mehr Padding oben */
.card-footer {
    padding: 20px 0 0 0;
    border-top: 1px solid #E0E0E0;
    margin-top: 20px;
}
```

**Teste:** Ändere das Padding auf verschiedene Werte und schaue, wie sich der Raum um den Inhalt verändert!

---

### Teil 3: Margin – Aussenabstand (20 Min)

**Margin schafft Abstand zwischen Elementen.**

**Verschiedene Margin-Notationen:**

```css
/* Alle vier Seiten gleich */
.spacing-1 {
    margin: 20px;
}

/* Vertikal | Horizontal */
.spacing-2 {
    margin: 40px 0;  /* Oben/Unten: 40px, Links/Rechts: 0 */
}

/* Zentrieren mit auto */
.spacing-3 {
    margin: 0 auto;  /* Zentriert horizontal, wenn width gesetzt ist */
}

/* Einzeln setzen */
.spacing-4 {
    margin-top: 60px;
    margin-bottom: 40px;
    margin-left: 0;
    margin-right: 0;
}
```

**Margin Collapsing – Wichtig zu verstehen!**

```css
/* ==================
   MARGIN COLLAPSING DEMO
   ================== */

.element-1 {
    margin-bottom: 30px;
}

.element-2 {
    margin-top: 20px;
}

/* Die beiden Margins werden NICHT addiert (30 + 20 = 50px)!
   Stattdessen "kollabieren" sie zum grösseren Wert: 30px
   Das nennt man "Margin Collapsing" */
```

**Praktische Anwendung: Abstände zwischen Sektionen:**

```css
/* ==================
   SECTION SPACING
   ================== */

section {
    margin-bottom: 80px;  /* Grosser Abstand zwischen Sektionen */
}

/* Erste Section: Kein Margin oben */
section:first-of-type {
    margin-top: 0;
}

/* Letzte Section: Kein Margin unten */
section:last-of-type {
    margin-bottom: 0;
}

/* Überschriften: Abstand oben und unten */
h2 {
    margin-top: 60px;
    margin-bottom: 30px;
}

h3 {
    margin-top: 40px;
    margin-bottom: 20px;
}

/* Absätze: Kleiner Abstand unten */
p {
    margin-bottom: 15px;
}

/* Letzter Absatz in einem Container: Kein Margin unten */
p:last-child {
    margin-bottom: 0;
}
```

---

### Teil 4: Border – Rahmen gestalten (15 Min)

**Border-Eigenschaften:**

```css
/* ==================
   BORDER-STYLES
   ================== */

/* Kurzform: Dicke | Stil | Farbe */
.border-1 {
    border: 2px solid #376B8C;
}

/* Verschiedene Border-Styles */
.border-solid {
    border: 3px solid #376B8C;
}

.border-dashed {
    border: 3px dashed #29786A;
}

.border-dotted {
    border: 3px dotted #CD7A15;
}

.border-double {
    border: 5px double #376B8C;
}

/* Nur eine Seite */
.border-bottom-only {
    border-bottom: 3px solid #45BA98;
}

.border-left-only {
    border-left: 4px solid #CD7A15;
}

/* Unterschiedliche Borders pro Seite */
.border-mixed {
    border-top: 2px solid #376B8C;
    border-right: 1px dashed #29786A;
    border-bottom: 3px double #CD7A15;
    border-left: 4px solid #45BA98;
}

/* Border-Radius für abgerundete Ecken */
.rounded {
    border: 2px solid #376B8C;
    border-radius: 8px;
}

.rounded-pill {
    border: 2px solid #376B8C;
    border-radius: 50px;  /* Sehr rund */
}

.rounded-circle {
    width: 100px;
    height: 100px;
    border: 2px solid #376B8C;
    border-radius: 50%;  /* Perfekter Kreis */
}
```

**Wende Borders auf dein Portfolio an:**

```css
/* ==================
   PORTFOLIO BORDERS
   ================== */

/* Überschriften: Unterstrich */
h2 {
    border-bottom: 3px solid #45BA98;
    padding-bottom: 10px;
}

/* Highlight-Box: Linker Rand */
.highlight {
    background-color: #FFF8DC;
    padding: 20px;
    border-left: 4px solid #CD7A15;
}

/* Buttons: Border + Hover-Effekt */
.btn-outline {
    background-color: transparent;
    color: #376B8C;
    border: 2px solid #376B8C;
    padding: 10px 20px;
    border-radius: 4px;
    transition: all 0.3s;
}

.btn-outline:hover {
    background-color: #376B8C;
    color: white;
}

/* Profilbild: Runder Border */
.profile-image {
    width: 150px;
    height: 150px;
    border: 4px solid #376B8C;
    border-radius: 50%;
    object-fit: cover;
}
```

---

### Teil 5: Box-Sizing – Die Lösung für einfachere Berechnungen (10 Min)

**Das Problem mit dem Standard-Box-Modell:**

```css
/* Ohne box-sizing: border-box */
.box-problem {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    
    /* Tatsächliche Breite: 300 + 40 + 10 = 350px */
}
```

**Die Lösung: box-sizing: border-box**

```css
/* ==================
   BOX-SIZING FIX
   ================== */

/* Für ALLE Elemente setzen (Best Practice) */
*, *::before, *::after {
    box-sizing: border-box;
}

/* Jetzt ist die Rechnung einfacher */
.box-fixed {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    
    /* Tatsächliche Breite: 300px (Padding und Border INKLUSIVE) */
}
```

**Füge das am Anfang deiner `styles.css` hinzu:**

```css
/* ==================
   RESET & BOX-SIZING
   ================== */

/* Box-Sizing für alle Elemente */
*, *::before, *::after {
    box-sizing: border-box;
}

/* Optional: Margins & Paddings zurücksetzen */
* {
    margin: 0;
    padding: 0;
}

body {
    margin: 0;
    padding: 0;
}
```

---

## Erfolgskriterien

- [ ] Du verstehst die vier Bereiche des Box-Modells (Content, Padding, Border, Margin)
- [ ] Eine Demo-Box mit sichtbarem Padding, Border und Margin existiert
- [ ] Mindestens 5 Elemente nutzen gezieltes Padding
- [ ] Mindestens 5 Elemente nutzen gezieltes Margin
- [ ] Verschiedene Border-Styles sind auf mindestens 3 Elementen angewendet
- [ ] `box-sizing: border-box` ist für alle Elemente gesetzt
- [ ] Du hast das Box-Modell in den DevTools inspiziert
- [ ] Die Abstände auf deiner Seite wirken harmonisch und professionell

## Tipps

- **DevTools sind dein Freund:** F12 → Elements → Wähle ein Element → Rechts siehst du das Box-Modell visuell
- **Shorthand-Notation:** `padding: 10px 20px` spart Schreibarbeit
- **Margin: 0 auto:** Zentriert Elemente horizontal (wenn `width` gesetzt ist)
- **Border-Radius:** Macht Ecken weich – 4-8px wirkt modern
- **Profitipp:** Nutze `outline` statt `border` zum Debuggen – es beeinflusst das Layout nicht
- **Margin Collapsing:** Nur vertikal, nicht horizontal!

## Reflexionsfragen

1. Was ist der Unterschied zwischen Padding und Margin? Wann nutzt du was?
2. Teste: Setze `margin: 100px` auf ein Element. Was passiert mit den umliegenden Elementen?
3. Experimentiere: Ändere `box-sizing` auf `content-box`. Wie verändert sich die Breite?
4. Öffne DevTools (F12) → Hovere über ein Element in der Elements-Liste. Siehst du das Box-Modell farbig markiert?
5. Was passiert, wenn zwei Elemente beide `margin-bottom: 30px` haben? Ist der Abstand 60px?
6. Erstelle eine Box mit `width: 200px`, `padding: 20px` und `border: 5px solid black`. Wie breit ist sie insgesamt?

## Weiterführende Links

**Box-Modell:**
- [MDN: The Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
- [MDN: box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)
- [CSS Tricks: Box-Sizing](https://css-tricks.com/box-sizing/)

**Padding & Margin:**
- [MDN: Padding](https://developer.mozilla.org/en-US/docs/Web/CSS/padding)
- [MDN: Margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin)
- [CSS Tricks: Margin Collapsing](https://css-tricks.com/what-you-should-know-about-collapsing-margins/)

**Border:**
- [MDN: Border](https://developer.mozilla.org/en-US/docs/Web/CSS/border)
- [MDN: border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius)
- [CSS Tricks: Border](https://css-tricks.com/almanac/properties/b/border/)

**Tools:**
- [Box Model Playground](https://codepen.io/carolineartz/full/ogVXZj)
- [Border-Radius Generator](https://border-radius.com/)

---

**Geschätzte Zeit:** 45-50 Minuten  
**Nächster Schritt:** In Auftrag 3 lernst du Farben, Schriften und fortgeschrittene Selektoren!
