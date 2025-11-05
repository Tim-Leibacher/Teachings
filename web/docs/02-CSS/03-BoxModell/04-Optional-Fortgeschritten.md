# Auftrag 4 (Optional): Fortgeschrittene Layout-Techniken – Position, Float & Advanced Box-Modell

## Ziel
Du lernst fortgeschrittene Layout-Techniken kennen: `position` (static, relative, absolute, fixed, sticky), Float für Text-Umfluss und komplexe Stacking-Contexts. Dieses Wissen ist essentiell für Overlays, Fixed Headers und kreative Layouts.

## Beschreibung

Dieser optionale Auftrag vertieft dein Box-Modell-Wissen mit Techniken, die für komplexe Layouts unverzichtbar sind. Du lernst, wie man Elemente aus dem normalen Dokumentfluss herausnimmt und präzise positioniert.

---

## Teil 1: Position Static & Relative (15 Min)

**Position: Static (Default)**

Jedes Element hat standardmässig `position: static`. Es folgt dem normalen Dokumentfluss.

```css
.element {
    position: static; /* Default, muss nicht explizit gesetzt werden */
    /* top, right, bottom, left haben KEINE Wirkung */
}
```

**Position: Relative**

Das Element bleibt im Dokumentfluss, kann aber relativ zu seiner ursprünglichen Position verschoben werden.

**Erstelle ein Demo:**

```html
<section id="position-demo">
    <h2>Position: Relative</h2>
    
    <div class="box static">Static Box</div>
    <div class="box relative">Relative Box (verschoben)</div>
    <div class="box static">Static Box</div>
</section>
```

```css
/* ==================
   POSITION DEMO
   ================== */
.box {
    display: inline-block;
    width: 150px;
    padding: 20px;
    margin: 10px;
    background-color: lightblue;
    border: 2px solid navy;
}

.static {
    position: static; /* Default */
}

.relative {
    position: relative;
    top: 20px; /* 20px nach unten verschoben */
    left: 30px; /* 30px nach rechts verschoben */
    background-color: lightcoral;
    
    /* Der ursprüngliche Platz bleibt erhalten! */
}
```

**Wichtig:**
- Der ursprüngliche Platz im Dokumentfluss bleibt erhalten (Lücke)
- Andere Elemente werden NICHT verschoben
- Nützlich für kleine Anpassungen oder als Basis für `absolute`-Kinder

**Praktische Anwendung – Badge positionieren:**

```html
<div class="notification-icon">
    🔔
    <span class="badge">3</span>
</div>
```

```css
.notification-icon {
    position: relative; /* Basis für absolutes Kind */
    display: inline-block;
    font-size: 48px;
    padding: 10px;
}

.badge {
    position: absolute;
    top: 0;
    right: 0;
    background-color: red;
    color: white;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: bold;
}
```

---

## Teil 2: Position Absolute (20 Min)

**Position: Absolute**

Das Element wird aus dem Dokumentfluss entfernt und relativ zum nächsten nicht-static Eltern-Element positioniert.

**Wichtige Regel:** Das Eltern-Element braucht `position: relative` (oder absolute/fixed/sticky)!

```html
<div class="parent">
    Eltern-Element (relative)
    <div class="child">Kind-Element (absolute)</div>
</div>
```

```css
.parent {
    position: relative; /* WICHTIG! */
    width: 400px;
    height: 300px;
    background-color: #E8F4F8;
    border: 2px solid navy;
    margin: 20px;
}

.child {
    position: absolute;
    top: 20px; /* 20px vom oberen Rand des Eltern-Elements */
    right: 20px; /* 20px vom rechten Rand */
    padding: 15px;
    background-color: lightcoral;
    border: 2px solid darkred;
}
```

**Zentrieren mit Absolute:**

```css
.centered {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%); /* Verschiebt um eigene Grösse */
    padding: 20px;
    background-color: white;
    border: 2px solid black;
}
```

**Praktische Anwendung – Overlay/Modal:**

```html
<div class="modal-overlay">
    <div class="modal">
        <button class="close-btn">×</button>
        <h2>Modal-Titel</h2>
        <p>Dies ist ein zentriertes Modal.</p>
    </div>
</div>
```

```css
/* ==================
   MODAL OVERLAY
   ================== */
.modal-overlay {
    position: fixed; /* Bleibt beim Scrollen sichtbar */
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000; /* Über allem anderen */
}

.modal {
    position: relative;
    width: 90%;
    max-width: 600px;
    padding: 40px;
    background-color: white;
    border-radius: 12px;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.close-btn {
    position: absolute;
    top: 15px;
    right: 15px;
    width: 40px;
    height: 40px;
    background-color: transparent;
    border: none;
    font-size: 32px;
    cursor: pointer;
    color: #666;
    transition: color 0.3s;
}

.close-btn:hover {
    color: black;
}
```

---

## Teil 3: Position Fixed & Sticky (20 Min)

**Position: Fixed**

Das Element wird aus dem Dokumentfluss entfernt und relativ zum Viewport (Browser-Fenster) positioniert. Es bleibt beim Scrollen an derselben Stelle.

**Fixed Header:**

```html
<header class="fixed-header">
    <h1>Mein Portfolio</h1>
    <nav>
        <a href="#about">Über mich</a>
        <a href="#projects">Projekte</a>
        <a href="#contact">Kontakt</a>
    </nav>
</header>

<!-- Platzhalter, damit Inhalt nicht unter Header verschwindet -->
<div class="header-spacer"></div>

<main>
    <!-- Dein Inhalt -->
</main>
```

```css
/* ==================
   FIXED HEADER
   ================== */
.fixed-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: var(--color-primary);
    color: white;
    padding: 20px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    z-index: 1000; /* Über allem anderen */
}

.header-spacer {
    height: 80px; /* Höhe des Headers */
    /* Verhindert, dass Inhalt unter Header verschwindet */
}
```

**Fixed "Back to Top" Button:**

```html
<button class="back-to-top" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">
    ↑
</button>
```

```css
.back-to-top {
    position: fixed;
    bottom: 30px;
    right: 30px;
    width: 50px;
    height: 50px;
    background-color: var(--color-primary);
    color: white;
    border: none;
    border-radius: 50%;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: background-color 0.3s, transform 0.3s;
    z-index: 999;
}

.back-to-top:hover {
    background-color: var(--color-primary-light);
    transform: translateY(-4px);
}
```

**Position: Sticky**

Das Element verhält sich wie `relative`, bis es beim Scrollen einen definierten Punkt erreicht – dann wird es `fixed`.

```html
<section>
    <h2 class="sticky-header">Projekte</h2>
    <article>Projekt 1...</article>
    <article>Projekt 2...</article>
    <article>Projekt 3...</article>
    <!-- Mehr Inhalt zum Scrollen -->
</section>
```

```css
.sticky-header {
    position: sticky;
    top: 0; /* Bleibt beim Scrollen oben kleben */
    background-color: white;
    padding: 15px 0;
    border-bottom: 2px solid var(--color-primary);
    z-index: 10;
}
```

---

## Teil 4: Float – Text-Umfluss (15 Min)

**Float war früher für Layouts verwendet, heute hauptsächlich für Text-Umfluss.**

**Bild mit Text-Umfluss:**

```html
<article>
    <img src="images/profil.jpg" alt="Profilbild" class="float-left">
    <h3>Über mich</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
    Der Text fliesst um das Bild herum...</p>
    <p>Weitere Absätze umfliessen ebenfalls das Bild.</p>
</article>
```

```css
/* ==================
   FLOAT BEISPIELE
   ================== */
.float-left {
    float: left;
    margin: 0 20px 20px 0; /* Abstand rechts und unten */
    width: 200px;
    border-radius: 8px;
}

.float-right {
    float: right;
    margin: 0 0 20px 20px; /* Abstand links und unten */
    width: 200px;
    border-radius: 8px;
}
```

**Clearfix – Float-Probleme lösen:**

Wenn ein Container nur gefloatete Kinder hat, verliert er seine Höhe!

**Problem:**
```html
<div class="container">
    <img src="bild.jpg" class="float-left">
    <p>Text...</p>
</div>
<!-- Container hat Höhe 0! -->
```

**Lösung 1: Clearfix (klassisch):**
```css
.clearfix::after {
    content: "";
    display: table;
    clear: both;
}
```

**Lösung 2: Overflow (einfach):**
```css
.container {
    overflow: auto; /* Oder hidden */
}
```

**Lösung 3: Display Flex (modern):**
```css
.container {
    display: flex;
    flex-wrap: wrap;
    /* Float wird ignoriert */
}
```

---

## Teil 5: Z-Index & Stacking Context (15 Min)

**Z-Index kontrolliert die Stapelreihenfolge von positionierten Elementen.**

**Wichtig:** Z-Index funktioniert nur bei Elementen mit `position` (außer `static`)!

```html
<div class="layer layer-1">Layer 1 (z-index: 1)</div>
<div class="layer layer-2">Layer 2 (z-index: 2)</div>
<div class="layer layer-3">Layer 3 (z-index: 3)</div>
```

```css
.layer {
    position: absolute;
    width: 200px;
    height: 200px;
    padding: 20px;
    border: 2px solid black;
}

.layer-1 {
    top: 50px;
    left: 50px;
    background-color: lightblue;
    z-index: 1;
}

.layer-2 {
    top: 100px;
    left: 100px;
    background-color: lightcoral;
    z-index: 2; /* Über Layer 1 */
}

.layer-3 {
    top: 150px;
    left: 150px;
    background-color: lightgreen;
    z-index: 3; /* Über Layer 1 und 2 */
}
```

**Typische Z-Index-Werte in professionellen Projekten:**

```css
:root {
    --z-index-dropdown: 100;
    --z-index-sticky: 200;
    --z-index-fixed: 300;
    --z-index-modal-backdrop: 400;
    --z-index-modal: 500;
    --z-index-popover: 600;
    --z-index-tooltip: 700;
}

.fixed-header {
    z-index: var(--z-index-fixed);
}

.modal-overlay {
    z-index: var(--z-index-modal-backdrop);
}

.modal {
    z-index: var(--z-index-modal);
}
```

**Stacking Context verstehen:**

Ein neuer Stacking Context wird erstellt durch:
- `position: relative/absolute/fixed/sticky` mit `z-index` (außer auto)
- `opacity` < 1
- `transform`, `filter`, `perspective`
- Flex/Grid Items mit `z-index`

**Wichtig:** Z-Index funktioniert nur innerhalb desselben Stacking Context!

```html
<div class="parent" style="z-index: 1;">
    <div class="child" style="z-index: 9999;">
        <!-- Bleibt unter Elementen mit z-index: 2 im globalen Context! -->
    </div>
</div>
<div style="z-index: 2;">
    Ich bin über dem Kind, trotz z-index: 9999!
</div>
```

---

## Teil 6: Komplexes Beispiel – Card mit Overlay (15 Min)

**Erstelle eine Projekt-Karte mit Hover-Overlay:**

```html
<article class="advanced-card">
    <img src="images/projekt.jpg" alt="Projekt">
    <div class="card-overlay">
        <h3>Portfolio-Website</h3>
        <p>HTML, CSS, JavaScript</p>
        <a href="#" class="btn-primary">Ansehen →</a>
    </div>
</article>
```

```css
/* ==================
   ADVANCED CARD
   ================== */
.advanced-card {
    position: relative; /* Basis für absolute Kinder */
    width: 350px;
    height: 400px;
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s;
}

.advanced-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
}

.advanced-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s;
}

.advanced-card:hover img {
    transform: scale(1.1); /* Zoom-Effekt */
}

/* ==================
   OVERLAY
   ================== */
.card-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 30px;
    background: linear-gradient(to top, rgba(0,0,0,0.9), transparent);
    color: white;
    transform: translateY(60%); /* Teilweise versteckt */
    transition: transform 0.3s;
}

.advanced-card:hover .card-overlay {
    transform: translateY(0); /* Vollständig sichtbar */
}

.card-overlay h3 {
    margin: 0 0 8px 0;
    font-size: 24px;
}

.card-overlay p {
    margin: 0 0 16px 0;
    color: #ddd;
}

.btn-primary {
    display: inline-block;
    padding: 10px 20px;
    background-color: var(--color-primary);
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: background-color 0.3s;
}

.btn-primary:hover {
    background-color: var(--color-primary-light);
}
```

---

## Erfolgskriterien

- [ ] Du verstehst die 5 Position-Werte (static, relative, absolute, fixed, sticky)
- [ ] Ein Fixed Header oder Back-to-Top Button ist implementiert
- [ ] Mindestens ein Element nutzt `position: absolute` für präzise Platzierung
- [ ] Float wird für Text-Umfluss um ein Bild verwendet
- [ ] Z-Index wird korrekt für Overlays oder Modals eingesetzt
- [ ] Ein komplexes Card-Layout mit Hover-Overlay ist erstellt
- [ ] Keine Layout-Brüche oder überlappende Elemente (außer gewollt)
- [ ] Sticky-Header oder Sticky-Section funktioniert beim Scrollen

## Tipps

- **Position: Relative** ist meist die Basis für `absolute`-Kinder
- **Fixed Elements** brauchen meist einen Platzhalter, damit Inhalt nicht verdeckt wird
- **Z-Index:** Nutze konsistente Werte (100, 200, 300, etc.) statt zufällige (9999)
- Float ist veraltet für Layouts → Nutze Flexbox/Grid (lernst du später)
- **DevTools:** Aktiviere 3D-Ansicht (Chrome) → Sieh Stacking Contexts visuell
- **Profitipp:** `position: sticky` funktioniert nicht in allen Browsern perfekt – teste gut!

## Selbsttest

Überprüfe dein Verständnis:

- **Position-Werte unterscheiden:** Ich kann die fünf Position-Werte (static, relative, absolute, fixed, sticky) erklären und weiss, welche aus dem Dokumentfluss entfernt werden
- **Absolute Positionierung verstehen:** Ich weiss, dass ein `absolute`-Element relativ zum nächsten nicht-static Eltern-Element positioniert wird und dass das Eltern-Element `position: relative` braucht
- **Z-Index richtig einsetzen:** Ich verstehe, dass z-index nur bei positionierten Elementen funktioniert und kann Stacking Contexts erklären
- **Float und Clearfix:** Ich kann erklären, warum Float-Container ihre Höhe verlieren und kenne mindestens zwei Lösungen (Clearfix, Overflow, Flexbox)

## Weiterführende Links

- [MDN: position](https://developer.mozilla.org/de/docs/Web/CSS/position)
- [MDN: float](https://developer.mozilla.org/de/docs/Web/CSS/float)
- [MDN: z-index](https://developer.mozilla.org/de/docs/Web/CSS/z-index)
- [MDN: Stacking Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
- [CSS Tricks: position](https://css-tricks.com/almanac/properties/p/position/)
- [CSS Tricks: All About Floats](https://css-tricks.com/all-about-floats/)
- [Interactive Position Demo](https://cssreference.io/property/position/)

## Bonus-Challenges

**Challenge 1: Sticky Navigation**
- Erstelle eine Navigation, die erst nach dem Header sticky wird
- Nutze `position: sticky` mit `top: 0`
- Füge einen Schatten hinzu, wenn sie sticky ist (mit JavaScript)

**Challenge 2: Modal-System**
- Erstelle ein vollständiges Modal mit Overlay
- Zentriert mit `position: fixed` und Flexbox
- Schliess-Button mit `position: absolute`
- Nutze korrekten Z-Index für Overlay und Modal

**Challenge 3: Parallax-Effekt**
- Nutze `position: fixed` für ein Hintergrundbild
- Inhalt scrollt über das fixe Bild
- Experimentiere mit verschiedenen Scroll-Geschwindigkeiten

**Challenge 4: Float-basiertes Magazin-Layout**
- Erstelle ein klassisches Magazin-Layout
- Bilder floaten links und rechts
- Text umfliesst die Bilder
- Nutze Clearfix für korrekte Container-Höhe

---

**⏱️ Geschätzte Zeit:** 60-75 Minuten  
**🎓 Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächster Schritt:** Glückwunsch! Du beherrschst das Box-Modell und Layout-Techniken. Weiter mit Flexbox für moderne Layouts!

---

**💬 Hinweis:** Viele dieser Techniken (besonders Float und Position für Layouts) wurden durch Flexbox und Grid ersetzt. Sie sind aber essentiell für Overlays, Fixed Headers und spezielle Layout-Effekte!
