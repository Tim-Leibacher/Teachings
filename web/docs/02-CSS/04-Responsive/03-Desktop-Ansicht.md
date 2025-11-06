# Auftrag 3: Desktop-Ansicht – Vollständig responsive Website

## Ziel
Du erweiterst dein Portfolio für grosse Bildschirme und lernst, wie man komplexe mehrspaltige Layouts erstellt. Am Ende dieses Auftrags hast du eine vollständig responsive Website, die auf allen Geräten perfekt aussieht.

## Beschreibung

Dein Portfolio funktioniert jetzt auf Smartphones und Tablets. In diesem Auftrag optimierst du es für Desktop-Bildschirme (ab 1024px Breite). Du lernst, wie man den vorhandenen Platz optimal nutzt und eine professionelle Desktop-Website erstellt.

---

### Teil 1: Desktop Media Query hinzufügen (10 Min)

Desktop-Bildschirme haben viel Platz. Wir nutzen eine dritte Media Query, um Layouts mit 3 oder mehr Spalten zu erstellen.

**Füge am Ende deiner `styles.css` hinzu:**

```css
/* ==========================================
   DESKTOP-ANSICHT (1024px+)
   ========================================== */

@media (min-width: 1024px) {
    
    /* Container: Maximale Breite begrenzen */
    .container {
        max-width: 1200px;
        padding: 0 40px;
    }
    
    /* Header: Noch grösser */
    header {
        padding: 80px 40px;
    }
    
    header h1 {
        font-size: 48px;
        margin-bottom: 15px;
    }
    
    header p {
        font-size: 20px;
    }
    
    /* Navigation: Mehr Abstand zwischen Links */
    nav a {
        padding: 18px 30px;
        font-size: 17px;
    }
    
    /* Main Content: Grosszügige Abstände */
    main {
        padding: 60px 40px;
    }
    
    section {
        margin-bottom: 80px;
    }
    
    section h2 {
        font-size: 40px;
        margin-bottom: 30px;
    }
    
    section h3 {
        font-size: 28px;
    }
    
    /* Projekt-Karten: 3 Spalten */
    .projekte-grid {
        grid-template-columns: repeat(3, 1fr); /* 3 statt 2 Spalten */
        gap: 40px;
    }
    
    /* Skills-Liste: 3 Spalten */
    .skills-liste {
        grid-template-columns: repeat(3, 1fr);
        gap: 20px;
    }
    
    /* Footer: Grössere Schrift */
    footer {
        padding: 40px;
    }
    
    footer p {
        font-size: 16px;
    }
}
```

---

### Teil 2: Hero-Sektion mit grossem Hintergrund (20 Min)

Auf Desktop-Bildschirmen wirkt ein Hero-Bereich mit Hintergrundbild beeindruckend.

**Erstelle einen Hero-Bereich in deiner `index.html`:**

```html
<section class="hero">
    <div class="hero-content">
        <h1>Willkommen in meinem Portfolio</h1>
        <p class="hero-subtitle">
            Informatiker/in EFZ in Ausbildung – Leidenschaftlich für 
            Webentwicklung und moderne Technologien
        </p>
        <div class="hero-buttons">
            <a href="#projekte" class="btn btn-primary">Meine Projekte</a>
            <a href="#kontakt" class="btn btn-secondary">Kontakt</a>
        </div>
    </div>
</section>
```

**Basis-CSS (Mobile):**

```css
.hero {
    background: linear-gradient(135deg, #376B8C 0%, #29786A 100%);
    color: white;
    padding: 60px 20px;
    text-align: center;
}

.hero-content h1 {
    font-size: 32px;
    margin-bottom: 15px;
    font-weight: 700;
}

.hero-subtitle {
    font-size: 18px;
    margin-bottom: 30px;
    opacity: 0.95;
}

.hero-buttons {
    display: flex;
    flex-direction: column;
    gap: 15px;
    align-items: center;
}

.btn {
    display: inline-block;
    padding: 15px 30px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 600;
    transition: all 0.3s ease;
    width: 100%;
    max-width: 300px;
}

.btn-primary {
    background-color: #FEAF51;
    color: #1A1A1A;
}

.btn-primary:hover {
    background-color: #FFC470;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(254, 175, 81, 0.4);
}

.btn-secondary {
    background-color: transparent;
    color: white;
    border: 2px solid white;
}

.btn-secondary:hover {
    background-color: white;
    color: #376B8C;
    transform: translateY(-2px);
}
```

**Tablet-Optimierung:**

```css
@media (min-width: 768px) {
    .hero {
        padding: 100px 40px;
    }
    
    .hero-content h1 {
        font-size: 42px;
    }
    
    .hero-subtitle {
        font-size: 20px;
        max-width: 700px;
        margin-left: auto;
        margin-right: auto;
    }
    
    .hero-buttons {
        flex-direction: row;
        justify-content: center;
    }
    
    .btn {
        width: auto;
    }
}
```

**Desktop-Optimierung mit Hintergrundbild:**

```css
@media (min-width: 1024px) {
    .hero {
        background: 
            linear-gradient(135deg, rgba(55, 107, 140, 0.9), rgba(41, 120, 106, 0.9)),
            url('../images/hero-background.jpg') center/cover;
        padding: 150px 40px;
        position: relative;
    }
    
    .hero-content h1 {
        font-size: 56px;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    
    .hero-subtitle {
        font-size: 24px;
        max-width: 800px;
    }
}
```

---

### Teil 3: Zweispaltiges Layout für "Über mich" (20 Min)

Auf Desktop haben wir Platz für komplexere Layouts. Wir erstellen eine zweispaltige Sektion.

**Erweitere deine Über-mich-Sektion:**

```html
<section id="ueber-mich">
    <h2>Über mich</h2>
    
    <div class="ueber-mich-content">
        <div class="ueber-mich-links">
            <div class="profilbild">
                <img src="images/profil.jpg" alt="Dein Name - Profilbild">
            </div>
            
            <div class="facts-box">
                <h3>Quick Facts</h3>
                <ul class="facts-liste">
                    <li><strong>Ausbildung:</strong> Informatiker/in EFZ</li>
                    <li><strong>Lehrjahr:</strong> 1. Lehrjahr</li>
                    <li><strong>Ort:</strong> Zürich, Schweiz</li>
                    <li><strong>Interessen:</strong> Webdev, Gaming, Tech</li>
                </ul>
            </div>
        </div>
        
        <div class="ueber-mich-rechts">
            <p>
                Hallo! Ich bin <strong>Dein Name</strong> und befinde mich im 
                ersten Lehrjahr der Ausbildung zum/zur Informatiker/in EFZ mit 
                Fachrichtung Applikationsentwicklung.
            </p>
            <p>
                Meine Leidenschaft für Technologie begann bereits in der Schule...
            </p>
            
            <h3>Meine Ziele</h3>
            <ul>
                <li>Moderne Webtechnologien meistern (React, Node.js)</li>
                <li>Eigene Apps entwickeln und veröffentlichen</li>
                <li>Open-Source-Projekte unterstützen</li>
                <li>Kontinuierlich neue Skills aufbauen</li>
            </ul>
        </div>
    </div>
</section>
```

**CSS für Desktop:**

```css
/* Mobile & Tablet: Bereits vorhanden aus Auftrag 2 */

@media (min-width: 1024px) {
    .ueber-mich-content {
        display: grid;
        grid-template-columns: 350px 1fr;
        gap: 60px;
        align-items: start;
    }
    
    .ueber-mich-links {
        position: sticky;
        top: 100px; /* Bleibt beim Scrollen sichtbar */
    }
    
    .profilbild img {
        width: 100%;
        max-width: 350px;
        height: 350px;
        object-fit: cover;
        margin-bottom: 30px;
    }
    
    .facts-box {
        background-color: #F8F8F8;
        border-left: 4px solid #376B8C;
        padding: 20px;
        border-radius: 8px;
    }
    
    .facts-box h3 {
        margin-top: 0;
        color: #376B8C;
        font-size: 22px;
    }
    
    .facts-liste {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    
    .facts-liste li {
        padding: 8px 0;
        border-bottom: 1px solid #E0E0E0;
    }
    
    .facts-liste li:last-child {
        border-bottom: none;
    }
    
    .ueber-mich-rechts {
        font-size: 18px;
        line-height: 1.8;
    }
}
```

---

### Teil 4: Advanced Grid Layout für Projekte (25 Min)

Auf Desktop können wir ein komplexeres Grid-Layout erstellen, bei dem ein Projekt hervorgehoben wird.

**HTML-Struktur erweitern:**

```html
<section id="projekte">
    <h2>Meine Projekte</h2>
    
    <div class="projekte-grid">
        <!-- Featured Projekt (nimmt mehr Platz ein) -->
        <article class="projekt-karte featured">
            <img src="images/projekt1.jpg" alt="Portfolio-Website">
            <div class="projekt-content">
                <span class="projekt-badge">Aktuelles Projekt</span>
                <h3>Portfolio-Website</h3>
                <p class="projekt-tech">
                    <strong>Stack:</strong> HTML5, CSS3, Responsive Design
                </p>
                <p>
                    Meine erste professionelle Website mit vollständig responsivem 
                    Design, modernem Layout und sauberem Code. Entstanden während 
                    der Ausbildung mit Fokus auf Best Practices.
                </p>
                <div class="projekt-links">
                    <a href="#" class="projekt-link">Live Demo</a>
                    <a href="#" class="projekt-link">GitHub</a>
                </div>
            </div>
        </article>
        
        <!-- Normale Projekte -->
        <article class="projekt-karte">
            <img src="images/projekt2.jpg" alt="To-Do App">
            <div class="projekt-content">
                <h3>To-Do App</h3>
                <p class="projekt-tech">
                    <strong>Stack:</strong> HTML, CSS, JavaScript
                </p>
                <p>
                    Eine interaktive To-Do-Liste mit localStorage für persistente Daten.
                </p>
                <div class="projekt-links">
                    <a href="#" class="projekt-link">Details</a>
                </div>
            </div>
        </article>
        
        <article class="projekt-karte">
            <img src="images/projekt3.jpg" alt="Wetter-App">
            <div class="projekt-content">
                <h3>Wetter-App</h3>
                <p class="projekt-tech">
                    <strong>Stack:</strong> HTML, CSS, JavaScript, API
                </p>
                <p>
                    Wetterdaten von einer API abrufen und anzeigen.
                </p>
                <div class="projekt-links">
                    <a href="#" class="projekt-link">Details</a>
                </div>
            </div>
        </article>
        
        <article class="projekt-karte">
            <img src="images/projekt4.jpg" alt="Calculator">
            <div class="projekt-content">
                <h3>Taschenrechner</h3>
                <p class="projekt-tech">
                    <strong>Stack:</strong> HTML, CSS, JavaScript
                </p>
                <p>
                    Ein funktionaler Taschenrechner mit allen Grundrechenarten.
                </p>
                <div class="projekt-links">
                    <a href="#" class="projekt-link">Details</a>
                </div>
            </div>
        </article>
    </div>
</section>
```

**Advanced Grid CSS:**

```css
/* Desktop: Featured-Projekt hervorheben */
@media (min-width: 1024px) {
    .projekte-grid {
        grid-template-columns: repeat(3, 1fr);
        grid-auto-rows: minmax(350px, auto);
    }
    
    /* Featured Projekt: 2 Spalten breit, 2 Reihen hoch */
    .projekt-karte.featured {
        grid-column: span 2;
        grid-row: span 2;
        display: flex;
        flex-direction: column;
    }
    
    .projekt-karte.featured img {
        height: 400px;
        object-fit: cover;
    }
    
    .projekt-karte.featured .projekt-content {
        flex: 1;
        display: flex;
        flex-direction: column;
    }
    
    .projekt-badge {
        display: inline-block;
        background-color: #FEAF51;
        color: #1A1A1A;
        padding: 5px 12px;
        border-radius: 20px;
        font-size: 14px;
        font-weight: 600;
        margin-bottom: 10px;
    }
    
    .projekt-tech {
        color: #666;
        font-size: 14px;
        margin-bottom: 10px;
    }
    
    .projekt-links {
        margin-top: auto;
        display: flex;
        gap: 10px;
    }
    
    .projekt-link {
        display: inline-block;
        padding: 8px 16px;
        background-color: #376B8C;
        color: white;
        border-radius: 5px;
        text-decoration: none;
        font-size: 14px;
        transition: background-color 0.3s ease;
    }
    
    .projekt-link:hover {
        background-color: #29786A;
    }
}
```

**Visuelles Layout:**

```
Desktop (1024px+):
┌──────────────┬──────┬──────┐
│              │ P2   │ P3   │
│   Featured   ├──────┼──────┤
│   Projekt 1  │ P4   │ P5   │
│   (2x2)      │      │      │
└──────────────┴──────┴──────┘
```

---

### Teil 5: Performance-Optimierung für grosse Bildschirme (15 Min)

Auf Desktop können wir höher aufgelöste Bilder laden, aber wir müssen aufpassen, dass die Seite nicht zu langsam wird.

**Optimierte Bild-Einbindung:**

```html
<picture>
    <source media="(min-width: 1024px)" srcset="images/projekt1-large.jpg">
    <source media="(min-width: 768px)" srcset="images/projekt1-medium.jpg">
    <img src="images/projekt1-small.jpg" alt="Portfolio-Website">
</picture>
```

**Lazy Loading für Bilder:**

```html
<img src="images/projekt1.jpg" 
     alt="Portfolio-Website" 
     loading="lazy">
```

Das `loading="lazy"` Attribut sorgt dafür, dass Bilder erst geladen werden, wenn sie in den sichtbaren Bereich scrollen.

---

### Teil 6: Kompletter Test auf allen Geräten (20 Min)

Jetzt testest du deine Website auf allen drei Breakpoints.

**Test-Checklist:**

**Mobile (375px):**
- [ ] Navigation vertikal und gut klickbar
- [ ] 1 Spalte für Projekte und Skills
- [ ] Texte lesbar ohne Zoom
- [ ] Hero-Buttons untereinander

**Tablet (768px):**
- [ ] Navigation horizontal
- [ ] 2 Spalten für Projekte und Skills
- [ ] Bild und Text in Über-mich nebeneinander
- [ ] Hero-Buttons nebeneinander

**Desktop (1024px):**
- [ ] 3 Spalten für normale Projekte
- [ ] Featured-Projekt nimmt 2x2 Grid-Zellen
- [ ] Über-mich: Sidebar links, Content rechts
- [ ] Container hat max-width von 1200px
- [ ] Alles ist zentriert auf sehr breiten Bildschirmen (1920px+)

**Teste diese Bildschirmbreiten in DevTools:**
- 375px (iPhone SE)
- 768px (iPad Mini)
- 1024px (iPad Pro, kleine Laptops)
- 1440px (Standard Desktop)
- 1920px (Full HD Monitor)

---

## Erfolgskriterien

- [ ] Drei Media Queries vorhanden: Mobile (Basis), Tablet (768px), Desktop (1024px)
- [ ] Projekt-Grid wechselt von 1 Spalte (Mobile) über 2 Spalten (Tablet) zu 3 Spalten (Desktop)
- [ ] Featured-Projekt nimmt auf Desktop 2x2 Grid-Zellen ein
- [ ] Hero-Sektion mit grossem Hintergrundbild auf Desktop
- [ ] Über-mich-Bereich hat zweispaltiges Layout auf Desktop
- [ ] Container hat max-width von 1200px auf sehr breiten Bildschirmen
- [ ] Alle Übergänge zwischen Breakpoints funktionieren flüssig
- [ ] Die Website sieht auf allen drei Gerätetypen professionell aus
- [ ] Performance: Lazy Loading für Bilder aktiviert

---

## Tipps

**Max-Width für Container:** `max-width: 1200px` verhindert, dass deine Inhalte auf riesigen Bildschirmen (z.B. 4K-Monitoren) zu breit werden und unlesbar sind.

**Grid-Gap Scaling:** Grössere Bildschirme vertragen grössere Abstände. Nutze auf Desktop 40px Gap statt 20px auf Mobile.

**Sticky Navigation:** Auf Desktop ist eine Navigation, die beim Scrollen oben bleibt, sehr praktisch. Nutze `position: sticky; top: 0;`.

**Object-Fit:** Bei festen Bildhöhen nutze `object-fit: cover;`, damit Bilder immer den Rahmen ausfüllen, ohne verzerrt zu werden.

**Testing auf echten Geräten:** DevTools sind gut, aber teste deine Seite auch auf echten Smartphones und Tablets, wenn möglich.

---

## Häufige Fehler

**Vergessenes Max-Width:** Ohne `max-width` wird dein Content auf 4K-Monitoren (3840px breit) unlesbar breit.

**Zu viele Spalten:** 4 oder 5 Spalten auf Desktop sehen meist zu gedrängt aus. Bleib bei 3 Spalten für Karten-Layouts.

**Feste Höhen für Text-Container:** Vermeide feste `height`-Werte für Bereiche mit Text. Auf verschiedenen Bildschirmen braucht Text unterschiedlich viel Platz.

**Breakpoints vergessen zu testen:** Teste nicht nur 1024px, sondern auch 1025px, 1200px und 1920px. Überraschungen lauern oft bei ungewöhnlichen Breiten.

**Performance ignorieren:** Grosse Bilder (>2MB) verlangsamen die Seite. Nutze Bildkompression (TinyPNG, Squoosh) und lazy loading.

---

## Reflexionsfragen

1. **Drei Breakpoints:** Du nutzt jetzt Mobile (Basis), Tablet (768px) und Desktop (1024px). Warum sind genau diese Breakpoints Standard in der Webentwicklung?

2. **Max-Width:** Dein Container hat `max-width: 1200px`. Was passiert auf einem 4K-Monitor (3840px breit) ohne dieses max-width?

3. **Grid vs. Flexbox:** Für das Projekt-Layout nutzt du CSS Grid, für die Navigation Flexbox. Kannst du erklären, wann Grid und wann Flexbox die bessere Wahl ist?

4. **Featured Projekt:** Das Featured-Projekt nutzt `grid-column: span 2; grid-row: span 2;`. Erkläre, was dieser Code macht und wie viel Platz das Projekt im Grid einnimmt.

5. **Mobile-First Vorteil:** Du hast mit Mobile-CSS angefangen und dann mit Media Queries erweitert. Welche Vorteile hat dieser Ansatz gegenüber Desktop-First (wo man mit Desktop startet und dann für Mobile anpasst)?

---

## Weiterführende Links

**CSS Grid Advanced:**
- [MDN: CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout)
- [CSS-Tricks: Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid Garden - Lernspiel](https://cssgridgarden.com/#de)

**Responsive Images:**
- [MDN: The Picture Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)
- [Web.dev: Use Imagemin to Compress Images](https://web.dev/use-imagemin-to-compress-images/)

**Performance:**
- [Web.dev: Lazy Loading Images](https://web.dev/lazy-loading-images/)
- [PageSpeed Insights - Google](https://pagespeed.web.dev/)
- [Lighthouse - Performance Testing](https://developer.chrome.com/docs/lighthouse/overview/)

**Container Queries (Future):**
- [MDN: CSS Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries)
- [Can I Use: Container Queries](https://caniuse.com/css-container-queries)

**Design Inspiration:**
- [Awwwards - Portfolio Designs](https://www.awwwards.com/websites/portfolio/)
- [Dribbble - Portfolio Concepts](https://dribbble.com/tags/portfolio-website)

---

⏱️ **Geschätzte Zeit:** 110 Minuten
