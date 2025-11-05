# Auftrag 2: Box-Sizing & Display-Eigenschaften – Kontrolle über Grössen und Layout

## Ziel
Du verstehst den Unterschied zwischen `box-sizing: content-box` und `border-box` und kannst die Display-Eigenschaften `block`, `inline` und `inline-block` gezielt einsetzen. Du lernst, wie diese Eigenschaften dein Layout beeinflussen.

## Beschreibung

Standardmässig addiert der Browser Padding und Border zur Width hinzu. Das macht Berechnungen kompliziert! Mit `box-sizing: border-box` bleiben Padding und Border innerhalb der definierten Breite. Ausserdem lernst du, wie `display` bestimmt, ob Elemente nebeneinander oder untereinander angeordnet werden.

---

### Teil 1: Das Problem mit Standard Box-Sizing (15 Min)

**Standardmässig gilt `box-sizing: content-box`:**

**Erstelle ein Test-Beispiel in deinem HTML:**

```html
<section id="box-sizing-demo">
    <h2>Box-Sizing Vergleich</h2>
    
    <div class="box content-box">
        <strong>content-box (default)</strong><br>
        Width: 300px<br>
        Padding: 20px<br>
        Border: 5px
    </div>
    
    <div class="box border-box">
        <strong>border-box</strong><br>
        Width: 300px<br>
        Padding: 20px<br>
        Border: 5px
    </div>
</section>
```

**Füge in `styles.css` hinzu:**

```css
/* ==================
   BOX-SIZING DEMO
   ================== */
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    margin: 20px 0;
    background-color: #E8F4F8;
}

.content-box {
    box-sizing: content-box; /* Default */
    /* Tatsächliche Breite: 300px + 40px Padding + 10px Border = 350px */
}

.border-box {
    box-sizing: border-box;
    /* Tatsächliche Breite: 300px (Padding und Border sind inbegriffen) */
}
```

**Teste im Browser mit DevTools:**
1. Öffne DevTools (F12)
2. Inspiziere beide Boxen
3. Schau dir das Box-Modell an – siehst du den Grössenunterschied?

---

### Teil 2: Box-Sizing global setzen (10 Min)

**Die Lösung: Setze `border-box` für ALLE Elemente!**

**Füge ganz am Anfang deiner `styles.css` hinzu:**

```css
/* ==================
   GLOBAL BOX-SIZING
   ================== */
*, *::before, *::after {
    box-sizing: border-box;
}
```

**Warum?**
- `*` = Alle Elemente
- `*::before` und `*::after` = Pseudo-Elemente (lernst du später)
- Jetzt bleibt `width: 300px` auch wirklich 300px, egal wie viel Padding/Border du hinzufügst!

**Teste den Unterschied:**

**Vorher (content-box):**
```css
.card {
    width: 300px;
    padding: 20px;
    border: 2px solid gray;
}
/* Tatsächliche Breite: 344px */
```

**Nachher (border-box):**
```css
.card {
    width: 300px;
    padding: 20px;
    border: 2px solid gray;
}
/* Tatsächliche Breite: 300px */
```

---

### Teil 3: Display Block vs. Inline (15 Min)

**Block-Elemente:**
- Nehmen die volle Breite ein
- Beginnen auf einer neuen Zeile
- Können Width und Height haben
- Beispiele: `<div>`, `<p>`, `<h1>`, `<section>`

**Inline-Elemente:**
- Nehmen nur so viel Platz wie nötig
- Bleiben im Textfluss
- Width und Height funktionieren NICHT
- Beispiele: `<span>`, `<a>`, `<strong>`, `<em>`

**Erstelle ein Demo-Beispiel:**

```html
<section id="display-demo">
    <h2>Display-Eigenschaften</h2>
    
    <h3>Block-Elemente (stapeln sich vertikal)</h3>
    <div class="block-box">Block 1</div>
    <div class="block-box">Block 2</div>
    <div class="block-box">Block 3</div>
    
    <h3>Inline-Elemente (bleiben im Textfluss)</h3>
    <p>
        Dies ist ein Text mit 
        <span class="inline-box">Inline 1</span> und 
        <span class="inline-box">Inline 2</span> dazwischen.
    </p>
</section>
```

**CSS:**

```css
/* ==================
   DISPLAY DEMO
   ================== */
.block-box {
    display: block;
    width: 200px;
    padding: 15px;
    margin: 10px 0;
    background-color: lightblue;
    border: 2px solid navy;
}

.inline-box {
    display: inline;
    padding: 5px 10px;
    background-color: lightcoral;
    border: 2px solid darkred;
    /* Width und Height haben KEINE Wirkung bei inline! */
}
```

**Experimentiere:**
- Füge `width: 300px` zu `.inline-box` hinzu → Was passiert? (Nichts!)
- Ändere `.block-box` auf `display: inline` → Jetzt stehen sie nebeneinander!

---

### Teil 4: Inline-Block – Das Beste aus beiden Welten (10 Min)

**`display: inline-block` kombiniert beide Eigenschaften:**
- Bleibt im Textfluss (wie inline)
- Kann Width und Height haben (wie block)
- Perfekt für Buttons, Cards nebeneinander, Navigation

**Erstelle eine Navigation mit Inline-Block:**

```css
/* ==================
   NAVIGATION MIT INLINE-BLOCK
   ================== */
nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
    text-align: center;
}

nav ul li {
    display: inline-block; /* Nebeneinander UND mit Width! */
    margin: 0 10px;
}

nav a {
    display: inline-block; /* Macht Links zu "Boxen" */
    padding: 10px 20px;
    background-color: var(--color-primary);
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: background-color 0.3s;
}

nav a:hover {
    background-color: var(--color-primary-light);
}
```

**Erstelle eine Card-Gallery mit Inline-Block:**

```css
/* ==================
   CARD GALLERY
   ================== */
.card-gallery {
    text-align: center; /* Zentriert die Karten */
}

.card-gallery article {
    display: inline-block;
    width: 280px; /* Fixe Breite */
    margin: 15px;
    padding: 20px;
    background-color: white;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    vertical-align: top; /* Richtet Karten oben aus */
    text-align: left; /* Text in Karten linksbündig */
}
```

**Füge in deinem HTML hinzu:**

```html
<section class="card-gallery">
    <h2>Meine Projekte</h2>
    
    <article>
        <h3>Projekt 1</h3>
        <p>Beschreibung...</p>
    </article>
    
    <article>
        <h3>Projekt 2</h3>
        <p>Längere Beschreibung mit mehr Text...</p>
    </article>
    
    <article>
        <h3>Projekt 3</h3>
        <p>Beschreibung...</p>
    </article>
</section>
```

---

### Teil 5: Display None – Elemente verstecken (5 Min)

**`display: none` entfernt Elemente komplett aus dem Layout:**

```css
/* ==================
   UTILITY CLASSES
   ================== */
.hidden {
    display: none; /* Element ist unsichtbar und nimmt keinen Platz ein */
}

.mobile-only {
    display: none; /* Versteckt auf Desktop */
}

/* Später mit Media Queries: */
@media (max-width: 768px) {
    .mobile-only {
        display: block; /* Zeigt auf Mobile */
    }
    
    .desktop-only {
        display: none; /* Versteckt auf Mobile */
    }
}
```

**Unterschied `display: none` vs. `visibility: hidden`:**

```css
.display-none {
    display: none; 
    /* Komplett entfernt, nimmt keinen Platz ein */
}

.visibility-hidden {
    visibility: hidden;
    /* Unsichtbar, aber Platz bleibt erhalten */
}
```

---

### Teil 6: Praktische Anwendung im Portfolio (10 Min)

**Wende das Gelernte auf dein Portfolio an:**

```css
/* ==================
   GLOBAL SETTINGS
   ================== */
*, *::before, *::after {
    box-sizing: border-box; /* IMMER als erstes! */
}

body {
    margin: 0;
    padding: 0;
}

/* ==================
   NAVIGATION
   ================== */
nav ul li {
    display: inline-block;
    margin: 0 15px;
}

nav a {
    display: inline-block;
    padding: 10px 20px;
    /* Width funktioniert jetzt! */
}

/* ==================
   SKILL BADGES
   ================== */
.skill-badge {
    display: inline-block;
    padding: 8px 16px;
    margin: 5px;
    background-color: var(--color-primary);
    color: white;
    border-radius: 20px;
    font-size: 14px;
}

/* ==================
   PROJECT CARDS
   ================== */
.projects-grid article {
    display: inline-block;
    width: 300px;
    margin: 15px;
    padding: 20px;
    vertical-align: top;
    /* Dank box-sizing: border-box bleibt width auch mit padding bei 300px! */
}

/* ==================
   FOOTER LINKS
   ================== */
footer a {
    display: inline-block;
    margin: 0 10px;
    padding: 5px;
}
```

---

## Erfolgskriterien

- [ ] `box-sizing: border-box` ist global für alle Elemente gesetzt
- [ ] Du verstehst den Unterschied zwischen `content-box` und `border-box`
- [ ] Mindestens 3 Elemente nutzen `display: inline-block`
- [ ] Die Navigation nutzt `inline-block` für horizontale Anordnung
- [ ] Projekt-Karten oder Skill-Badges sind mit `inline-block` nebeneinander
- [ ] Du hast `display: block` und `display: inline` experimentell getestet
- [ ] Ein Element nutzt `display: none` (z.B. für mobile/desktop)
- [ ] Die Seite funktioniert ohne Layout-Brüche

## Tipps

- **`box-sizing: border-box` ist ein Muss!** Setze es global am Anfang deines CSS
- **Inline-Block:** Vorsicht mit Whitespace im HTML – Leerzeichen zwischen Elementen werden als Abstand angezeigt
- **Profitipp:** `vertical-align: top` bei inline-block verhindert unerwünschtes Verhalten bei unterschiedlichen Höhen
- `display: flex` und `display: grid` sind modernere Alternativen (lernst du später!)
- **DevTools-Trick:** Klicke auf ein Element → Ändere `display` live und sieh dir die Auswirkungen an
- Bei `inline-block`: Nutze `text-align: center` auf dem Eltern-Element zum Zentrieren

## Selbsttest

Überprüfe dein Verständnis:

- **Box-Sizing verstehen:** Ich kann erklären, warum `border-box` die Grössenberechnung vereinfacht und kann die tatsächliche Breite bei `content-box` berechnen
- **Display-Eigenschaften unterscheiden:** Ich weiss, dass `display: inline` keine Width und Height akzeptiert, während `display: inline-block` beides ermöglicht
- **Global Box-Sizing setzen:** Ich verstehe, warum `*, *::before, *::after { box-sizing: border-box; }` am Anfang des CSS stehen sollte
- **Whitespace-Problem bei Inline-Block:** Ich weiss, dass Leerzeichen im HTML zwischen `inline-block`-Elementen als Abstand dargestellt werden und kann das Problem lösen

## Weiterführende Links

- [MDN: box-sizing](https://developer.mozilla.org/de/docs/Web/CSS/box-sizing)
- [MDN: display](https://developer.mozilla.org/de/docs/Web/CSS/display)
- [CSS Tricks: Box-Sizing](https://css-tricks.com/box-sizing/)
- [CSS Tricks: Inline vs. Inline-Block](https://css-tricks.com/whats-the-difference-between-inline-and-inline-block/)
- [W3Schools: Display Property](https://www.w3schools.com/css/css_display_visibility.asp)
- [Can I Use: box-sizing](https://caniuse.com/css3-boxsizing)

---

**⏱️ Geschätzte Zeit:** 30-35 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 lernst du fortgeschrittene Layout-Techniken mit Position und Float!
