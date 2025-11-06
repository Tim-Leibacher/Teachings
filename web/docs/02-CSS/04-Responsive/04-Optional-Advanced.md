# Auftrag 4 (Optional): Advanced Responsive Techniques – Mobile Navigation & Performance

## Ziel
Du lernst fortgeschrittene Responsive-Techniken kennen, die in professionellen Websites zum Einsatz kommen: Ein mobiles Burger-Menü mit JavaScript, Container Queries, responsive Typografie und Performance-Optimierungen.

## Beschreibung

Dein Portfolio ist jetzt vollständig responsive. In diesem optionalen Vertiefungsauftrag lernst du fortgeschrittene Techniken, die echte Websites nutzen. Dieser Auftrag ist anspruchsvoller und setzt voraus, dass du die vorherigen Aufträge gemeistert hast.

---

### Teil 1: Mobiles Burger-Menü mit JavaScript (30 Min)

Auf Smartphones ist Platz wertvoll. Ein Burger-Menü versteckt die Navigation hinter einem Icon und zeigt sie erst bei Klick an.

**Schritt 1: HTML erweitern**

```html
<nav class="main-nav">
    <div class="nav-container">
        <div class="logo">
            <a href="#home">DN</a> <!-- Deine Initialen -->
        </div>
        
        <!-- Burger Button (nur auf Mobile sichtbar) -->
        <button class="nav-toggle" aria-label="Navigation öffnen" aria-expanded="false">
            <span class="hamburger"></span>
        </button>
        
        <!-- Navigation Menu -->
        <ul class="nav-menu">
            <li><a href="#home">Home</a></li>
            <li><a href="#ueber-mich">Über mich</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#projekte">Projekte</a></li>
            <li><a href="#kontakt">Kontakt</a></li>
        </ul>
    </div>
</nav>
```

**Schritt 2: CSS für das Burger-Menü**

```css
/* ==========================================
   NAVIGATION MIT BURGER-MENÜ
   ========================================== */

.main-nav {
    background-color: #2C5F7D;
    position: sticky;
    top: 0;
    z-index: 1000;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.nav-container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 15px;
}

/* Logo */
.logo a {
    color: white;
    font-size: 24px;
    font-weight: 700;
    text-decoration: none;
    padding: 15px 0;
    display: block;
}

/* Burger Button (nur auf Mobile) */
.nav-toggle {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 40px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    z-index: 1001;
}

.hamburger {
    position: relative;
    width: 25px;
    height: 2px;
    background-color: white;
    transition: all 0.3s ease;
}

.hamburger::before,
.hamburger::after {
    content: '';
    position: absolute;
    width: 25px;
    height: 2px;
    background-color: white;
    transition: all 0.3s ease;
}

.hamburger::before {
    top: -8px;
}

.hamburger::after {
    top: 8px;
}

/* Burger Animation: X wenn geöffnet */
.nav-toggle.active .hamburger {
    background-color: transparent;
}

.nav-toggle.active .hamburger::before {
    top: 0;
    transform: rotate(45deg);
}

.nav-toggle.active .hamburger::after {
    top: 0;
    transform: rotate(-45deg);
}

/* Navigation Menu - Mobile */
.nav-menu {
    position: fixed;
    top: 60px;
    left: -100%; /* Versteckt links ausserhalb des Bildschirms */
    width: 100%;
    height: calc(100vh - 60px);
    background-color: #2C5F7D;
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    transition: left 0.3s ease;
    overflow-y: auto;
}

.nav-menu.active {
    left: 0; /* Einsliden von links */
}

.nav-menu li {
    width: 100%;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.nav-menu a {
    display: block;
    padding: 20px 30px;
    color: white;
    text-decoration: none;
    font-size: 18px;
    transition: background-color 0.3s ease;
}

.nav-menu a:hover {
    background-color: rgba(255, 255, 255, 0.1);
}

/* Tablet: Burger-Menü ausblenden, normale Navigation anzeigen */
@media (min-width: 768px) {
    .nav-toggle {
        display: none; /* Burger verstecken */
    }
    
    .nav-menu {
        position: static;
        height: auto;
        flex-direction: row;
        justify-content: flex-end;
        gap: 0;
        background: none;
        left: 0;
    }
    
    .nav-menu li {
        width: auto;
        border-bottom: none;
    }
    
    .nav-menu a {
        padding: 20px 25px;
        font-size: 16px;
    }
}

/* Desktop: Noch mehr Abstand */
@media (min-width: 1024px) {
    .nav-menu a {
        padding: 22px 30px;
    }
}
```

**Schritt 3: JavaScript für das Burger-Menü**

Erstelle eine Datei `navigation.js` im gleichen Ordner wie deine `index.html`:

```javascript
// navigation.js - Burger-Menü Funktionalität

// Warte, bis das HTML vollständig geladen ist
document.addEventListener('DOMContentLoaded', function() {
    
    // Elemente auswählen
    const navToggle = document.querySelector('.nav-toggle');
    const navMenu = document.querySelector('.nav-menu');
    const navLinks = document.querySelectorAll('.nav-menu a');
    
    // Burger-Button: Navigation öffnen/schliessen
    navToggle.addEventListener('click', function() {
        // Toggle-Klasse für Button-Animation
        navToggle.classList.toggle('active');
        
        // Toggle-Klasse für Menu-Anzeige
        navMenu.classList.toggle('active');
        
        // Aria-Attribut für Accessibility aktualisieren
        const isExpanded = navToggle.getAttribute('aria-expanded') === 'true';
        navToggle.setAttribute('aria-expanded', !isExpanded);
    });
    
    // Alle Navigation-Links: Menü schliessen beim Klick
    navLinks.forEach(link => {
        link.addEventListener('click', function() {
            // Nur auf Mobile schliessen (wenn Burger sichtbar)
            if (window.innerWidth < 768) {
                navToggle.classList.remove('active');
                navMenu.classList.remove('active');
                navToggle.setAttribute('aria-expanded', 'false');
            }
        });
    });
    
    // Bei Fenster-Resize: Menu schliessen, wenn zu Desktop gewechselt wird
    window.addEventListener('resize', function() {
        if (window.innerWidth >= 768) {
            navToggle.classList.remove('active');
            navMenu.classList.remove('active');
            navToggle.setAttribute('aria-expanded', 'false');
        }
    });
});
```

**Schritt 4: JavaScript einbinden**

Füge am Ende deines `<body>` (vor `</body>`) hinzu:

```html
    <script src="navigation.js"></script>
</body>
</html>
```

**Teste das Burger-Menü:**
1. Öffne deine Seite im Responsive-Modus (F12, Handy-Symbol)
2. Wähle iPhone 14 Pro
3. Klicke auf das Burger-Icon → Navigation sollte von links einslideen
4. Klicke erneut → Navigation sollte verschwinden
5. Wechsle zu Tablet-Grösse (768px+) → Burger verschwindet, normale Navigation erscheint

---

### Teil 2: Responsive Typography mit Fluid Types (20 Min)

Statt feste Schriftgrössen für jeden Breakpoint zu definieren, können Schriftgrössen flüssig mitwachsen.

**CSS-Technik: Clamp-Funktion**

```css
/* Fluid Typography - Schriftgrössen wachsen mit Bildschirmbreite */

body {
    /* Mobile: 16px, Desktop: 18px, dazwischen flüssiger Übergang */
    font-size: clamp(16px, 1vw + 14px, 18px);
    line-height: 1.6;
}

h1 {
    /* Mobile: 28px, Desktop: 56px */
    font-size: clamp(28px, 5vw, 56px);
    line-height: 1.2;
    margin-bottom: clamp(15px, 2vw, 30px);
}

h2 {
    /* Mobile: 24px, Desktop: 40px */
    font-size: clamp(24px, 4vw, 40px);
    line-height: 1.3;
    margin-bottom: clamp(15px, 2vw, 25px);
}

h3 {
    /* Mobile: 20px, Desktop: 28px */
    font-size: clamp(20px, 3vw, 28px);
    line-height: 1.4;
}

p {
    margin-bottom: clamp(15px, 2vw, 20px);
}

/* Abstände: Auch flüssig */
section {
    padding: clamp(40px, 5vw, 80px) clamp(15px, 3vw, 40px);
}
```

**Was macht `clamp()`?**
- `clamp(MIN, PREFERRED, MAX)`
- MIN: Kleinster Wert (Mobile)
- PREFERRED: Bevorzugter Wert (berechnet sich mit Viewport-Einheiten)
- MAX: Grösster Wert (Desktop)

**Vorteile:**
- Keine Media Queries für Schriftgrössen nötig
- Flüssige Übergänge zwischen Breakpoints
- Weniger CSS-Code
- Automatische Anpassung an jede Bildschirmgrösse

---

### Teil 3: Container Queries – Die Zukunft von Responsive Design (25 Min)

Container Queries erlauben es, Styles basierend auf der Grösse des Eltern-Containers anzupassen, nicht der gesamten Seite.

**Szenario:** Du hast eine Komponente, die in unterschiedlichen Bereichen deiner Seite erscheint. Sie soll sich an die Grösse ihres Containers anpassen, nicht an die Bildschirmgrösse.

**HTML:**

```html
<section class="sidebar">
    <div class="card-container">
        <article class="card">
            <img src="images/news1.jpg" alt="News 1">
            <h3>News-Artikel 1</h3>
            <p>Kurzer Teaser-Text...</p>
            <a href="#">Weiterlesen</a>
        </article>
    </div>
</section>

<section class="main-content">
    <div class="card-container">
        <article class="card">
            <img src="images/news2.jpg" alt="News 2">
            <h3>News-Artikel 2</h3>
            <p>Kurzer Teaser-Text...</p>
            <a href="#">Weiterlesen</a>
        </article>
    </div>
</section>
```

**CSS mit Container Queries:**

```css
/* Container Query Setup */
.card-container {
    container-type: inline-size;
    container-name: card;
}

/* Standard Card Layout (schmaler Container) */
.card {
    background-color: #F8F8F8;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.card h3 {
    padding: 15px 15px 10px;
    margin: 0;
    font-size: 18px;
}

.card p {
    padding: 0 15px;
    color: #666;
    font-size: 14px;
}

.card a {
    display: block;
    padding: 15px;
    color: #376B8C;
    text-decoration: none;
    font-weight: 600;
}

/* Wenn der Container mindestens 400px breit ist */
@container card (min-width: 400px) {
    .card {
        display: grid;
        grid-template-columns: 150px 1fr;
        grid-template-rows: auto 1fr auto;
    }
    
    .card img {
        grid-column: 1;
        grid-row: 1 / -1;
        height: 100%;
    }
    
    .card h3 {
        grid-column: 2;
        grid-row: 1;
    }
    
    .card p {
        grid-column: 2;
        grid-row: 2;
    }
    
    .card a {
        grid-column: 2;
        grid-row: 3;
    }
}
```

**Vorteil von Container Queries:**
- Die Card passt sich an ihren Container an, nicht an die Bildschirmbreite
- Dieselbe Card kann in einer schmalen Sidebar vertikal sein, aber in der Hauptspalte horizontal
- Viel flexibler als Media Queries!

**Browser-Support:** Container Queries sind relativ neu. Prüfe auf [Can I Use](https://caniuse.com/css-container-queries) den aktuellen Support.

---

### Teil 4: Performance-Optimierung – Critical CSS (20 Min)

Critical CSS bedeutet, dass wichtiges CSS inline im `<head>` steht, damit die Seite schneller lädt.

**Strategie:**
1. Above-the-fold CSS (alles, was ohne Scrollen sichtbar ist) → Inline im Head
2. Rest des CSS → Externe Datei, die asynchron geladen wird

**Beispiel:**

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio - Dein Name</title>
    
    <!-- Critical CSS inline für schnelleres First Paint -->
    <style>
        /* Minimal-CSS für Hero & Header */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: system-ui, sans-serif; }
        .hero {
            background: linear-gradient(135deg, #376B8C, #29786A);
            color: white;
            padding: 100px 20px;
            text-align: center;
        }
        .hero h1 { font-size: 36px; margin-bottom: 15px; }
    </style>
    
    <!-- Restliches CSS asynchron laden -->
    <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link rel="stylesheet" href="styles.css"></noscript>
</head>
```

**Tools zur Generierung von Critical CSS:**
- [Critical](https://github.com/addyosmani/critical) (Node.js Tool)
- [Critical CSS Generator](https://jonassebastianohlsson.com/criticalpathcssgenerator/)

---

### Teil 5: Bildoptimierung mit WebP & AVIF (25 Min)

Moderne Bildformate wie WebP und AVIF sind 25-50% kleiner als JPEG/PNG bei gleicher Qualität.

**HTML mit moderneren Bildformaten:**

```html
<picture>
    <!-- Moderne Browser: AVIF (beste Kompression) -->
    <source type="image/avif" srcset="images/projekt1.avif">
    
    <!-- Moderne Browser: WebP (gute Kompression) -->
    <source type="image/webp" srcset="images/projekt1.webp">
    
    <!-- Fallback: JPEG (alle Browser) -->
    <img src="images/projekt1.jpg" alt="Portfolio-Website" loading="lazy">
</picture>
```

**Responsive Images mit verschiedenen Grössen:**

```html
<picture>
    <!-- Desktop: Grosse Bilder -->
    <source media="(min-width: 1024px)" 
            type="image/webp"
            srcset="images/hero-desktop.webp">
    
    <!-- Tablet: Mittlere Bilder -->
    <source media="(min-width: 768px)" 
            type="image/webp"
            srcset="images/hero-tablet.webp">
    
    <!-- Mobile: Kleine Bilder -->
    <source type="image/webp"
            srcset="images/hero-mobile.webp">
    
    <!-- Fallback -->
    <img src="images/hero-mobile.jpg" 
         alt="Hero Background" 
         loading="lazy">
</picture>
```

**Tools zur Bildkonvertierung:**
- [Squoosh](https://squoosh.app/) – Online, kostenlos
- [ImageMagick](https://imagemagick.org/) – Kommandozeile
- [Sharp](https://sharp.pixelplumbing.com/) – Node.js Library

**Performance-Tipps:**
- WebP: 25-35% kleiner als JPEG
- AVIF: 50% kleiner als JPEG (neuer Standard)
- Lazy Loading für alle Bilder unterhalb des Folds
- `decoding="async"` für nicht-kritische Bilder

---

### Teil 6: Accessibility-Verbesserungen (20 Min)

Responsive Design muss auch barrierefrei sein.

**Skip-Link für Tastatur-Navigation:**

```html
<body>
    <a href="#main-content" class="skip-link">Zum Hauptinhalt springen</a>
    
    <nav>
        <!-- Navigation -->
    </nav>
    
    <main id="main-content">
        <!-- Content -->
    </main>
</body>
```

```css
/* Skip-Link: Normalerweise versteckt, bei Fokus sichtbar */
.skip-link {
    position: absolute;
    top: -100px;
    left: 0;
    background: #376B8C;
    color: white;
    padding: 10px 20px;
    text-decoration: none;
    z-index: 9999;
}

.skip-link:focus {
    top: 0;
}
```

**Focus-Styles für Tastatur-Navigation:**

```css
/* Sichtbare Focus-Styles */
a:focus,
button:focus,
input:focus,
textarea:focus {
    outline: 3px solid #FEAF51;
    outline-offset: 2px;
}

/* Nur bei Tastatur-Fokus, nicht bei Maus-Klick */
a:focus:not(:focus-visible) {
    outline: none;
}

a:focus-visible {
    outline: 3px solid #FEAF51;
    outline-offset: 2px;
}
```

**Aria-Labels für Screen Reader:**

```html
<nav aria-label="Hauptnavigation">
    <ul>
        <li><a href="#home">Home</a></li>
        <!-- ... -->
    </ul>
</nav>

<button class="nav-toggle" 
        aria-label="Navigation öffnen" 
        aria-expanded="false">
    <span class="hamburger"></span>
</button>
```

---

## Erfolgskriterien

- [ ] Burger-Menü funktioniert auf Mobile und verschwindet auf Tablet/Desktop
- [ ] JavaScript öffnet/schliesst die Navigation
- [ ] Fluid Typography mit `clamp()` implementiert
- [ ] Container Queries (optional, wenn Browser unterstützt)
- [ ] Critical CSS inline für Hero-Bereich
- [ ] WebP-Bilder mit JPEG-Fallback
- [ ] Lazy Loading für alle Bilder aktiviert
- [ ] Skip-Link für Tastatur-Navigation vorhanden
- [ ] Focus-Styles für alle interaktiven Elemente
- [ ] Aria-Labels für wichtige UI-Elemente

---

## Tipps

**Browser-Support testen:** Nicht alle Features funktionieren in allen Browsern. Nutze [Can I Use](https://caniuse.com/) um zu prüfen, welche Browser ein Feature unterstützen.

**Progressive Enhancement:** Implementiere Features so, dass die Seite auch ohne JavaScript funktioniert. Das Burger-Menü sollte auf No-JS-Geräten immer offen sein.

**Performance messen:** Nutze [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) in Chrome DevTools, um die Performance deiner Seite zu messen.

**JavaScript-Performance:** Für das Burger-Menü nutzt du Event-Listener. Entferne diese, wenn sie nicht mehr gebraucht werden, um Memory Leaks zu vermeiden.

**AVIF vs. WebP:** AVIF ist neuer und hat bessere Kompression, aber weniger Browser-Support. Nutze beides mit Fallback.

---

## Häufige Fehler

**JavaScript nicht geladen:** Wenn das Burger-Menü nicht funktioniert, prüfe die Browser-Konsole (F12 → Console) auf Fehler.

**CSS-Spezifität Probleme:** Wenn neue Styles nicht greifen, könnte ein anderer Selektor spezifischer sein. Nutze DevTools zum Debuggen.

**Container Queries ohne Fallback:** Alte Browser verstehen Container Queries nicht. Nutze Feature Queries: `@supports (container-type: inline-size) { ... }`.

**Zu grosses Critical CSS:** Critical CSS sollte max. 10-15 KB sein. Mehr verlangsamt die Seite wieder.

**Accessibility vergessen:** Nicht jeder nutzt eine Maus! Teste deine Seite mit Tab-Taste zur Navigation.

---

## Reflexionsfragen

1. **Burger-Menü:** Warum versteckst du die Navigation auf Mobile hinter einem Burger-Menü? Welche Vor- und Nachteile hat das für die User Experience?

2. **Fluid Typography:** `font-size: clamp(16px, 1vw + 14px, 18px)` – Erkläre, wie diese Formel funktioniert und bei welcher Viewport-Breite welche Schriftgrösse genutzt wird.

3. **Container Queries vs. Media Queries:** Was ist der Hauptunterschied zwischen Container Queries und Media Queries? Wann würdest du welches nutzen?

4. **Critical CSS:** Warum lädt die Seite schneller, wenn wichtiges CSS inline im Head steht statt in einer externen Datei?

5. **WebP vs. JPEG:** Ein JPEG-Bild ist 500 KB gross. Als WebP ist es nur 175 KB gross (65% Ersparnis). Wie viel Ladezeit sparst du bei einer 4G-Verbindung mit 10 Mbps Download-Speed?

---

## Weiterführende Links

**Burger-Menü:**
- [A11Y: Accessible Burger Menu](https://www.a11yproject.com/posts/accessible-hamburger-menu/)
- [CSS-Tricks: Hamburger Menu](https://css-tricks.com/hamburger-menu-alternatives/)

**Fluid Typography:**
- [Fluid Typography Calculator](https://fluid-typography.com/)
- [Modern Fluid Typography](https://css-tricks.com/simplified-fluid-typography/)
- [Utopia - Fluid Responsive Design](https://utopia.fyi/)

**Container Queries:**
- [MDN: CSS Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries)
- [Container Queries: A Quick Start Guide](https://www.smashingmagazine.com/2021/05/complete-guide-css-container-queries/)

**Performance:**
- [Web.dev: Fast Load Times](https://web.dev/fast/)
- [Critical CSS Generator](https://jonassebastianohlsson.com/criticalpathcssgenerator/)
- [Lighthouse Documentation](https://developer.chrome.com/docs/lighthouse/)

**Modern Image Formats:**
- [Squoosh - Image Compressor](https://squoosh.app/)
- [WebP vs AVIF Comparison](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/)
- [Can I Use: AVIF](https://caniuse.com/avif)

**Accessibility:**
- [WebAIM: Keyboard Accessibility](https://webaim.org/techniques/keyboard/)
- [The A11Y Project](https://www.a11yproject.com/)
- [WAVE - Web Accessibility Evaluation Tool](https://wave.webaim.org/)

---

⏱️ **Geschätzte Zeit:** 140 Minuten
