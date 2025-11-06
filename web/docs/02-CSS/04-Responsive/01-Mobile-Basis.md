# Auftrag 1: Mobile Basis – Portfolio für Smartphones optimieren

## Ziel
Du lernst den Mobile-First Ansatz kennen und machst dein Portfolio auf Smartphones perfekt nutzbar. Du verstehst, warum der Viewport Meta-Tag wichtig ist und wie du CSS für kleine Bildschirme schreibst.

## Beschreibung

In diesem Auftrag optimierst du dein Portfolio zuerst für Smartphones. Das ist der erste Schritt zu einem vollständig responsiven Design. Du lernst, warum Mobile-First der professionelle Ansatz ist.

---

### Teil 1: Viewport Meta-Tag einbinden (5 Min)

Ohne diesen Meta-Tag funktioniert Responsive Design nicht richtig. Mobile Browser würden deine Seite wie eine Desktop-Version verkleinert darstellen.

**Öffne deine `index.html` und füge im `<head>` hinzu:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dein Name - Portfolio</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Dein bisheriger Inhalt -->
</body>
</html>
```

**Was bedeutet das?**
- `width=device-width` → Nutze die echte Bildschirmbreite des Geräts
- `initial-scale=1.0` → Zoome nicht automatisch rein oder raus
- Ohne diesen Tag: Browser zeigt Desktop-Version, nur sehr klein

**Test:**
1. Öffne deine Seite im Browser
2. Drücke `F12` (Developer Tools)
3. Klicke auf das Handy-Symbol (Toggle Device Toolbar)
4. Wähle "iPhone 14 Pro" aus
5. Deine Seite sollte jetzt normal gross angezeigt werden

---

### Teil 2: Mobile-optimiertes CSS schreiben (20 Min)

Jetzt schreibst du CSS, das speziell für Smartphones gedacht ist. Das ist dein Basis-CSS, das für alle Geräte gilt – später erweiterst du es für grössere Bildschirme.

**Erstelle oder ergänze `styles.css`:**

```css
/* ==========================================
   MOBILE-FIRST BASIS-STYLES
   Für Bildschirme unter 768px
   ========================================== */

/* Grundlegende Resets */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
    background-color: #FFFFFF;
}

/* Container mit Seitenabstand */
.container {
    width: 100%;
    padding: 0 15px; /* Kleine Abstände links/rechts */
    margin: 0 auto;
}

/* Header: Kompakt für Mobile */
header {
    background: linear-gradient(135deg, #376B8C 0%, #29786A 100%);
    color: white;
    padding: 30px 15px;
    text-align: center;
}

header h1 {
    font-size: 28px;
    margin-bottom: 10px;
    font-weight: 700;
}

header p {
    font-size: 16px;
    opacity: 0.9;
}

/* Navigation: Vertikal für Mobile */
nav {
    background-color: #2C5F7D;
    position: sticky;
    top: 0;
    z-index: 100;
}

nav ul {
    list-style: none;
    display: flex;
    flex-direction: column; /* Vertikale Navigation */
}

nav li {
    width: 100%;
}

nav a {
    display: block;
    padding: 15px 20px;
    color: white;
    text-decoration: none;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    transition: background-color 0.3s ease;
}

nav a:hover,
nav a:focus {
    background-color: rgba(255, 255, 255, 0.1);
}

/* Main Content: Volle Breite auf Mobile */
main {
    padding: 20px 15px;
}

section {
    margin-bottom: 40px;
}

section h2 {
    font-size: 24px;
    color: #376B8C;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 3px solid #FEAF51;
}

section h3 {
    font-size: 20px;
    color: #29786A;
    margin-top: 20px;
    margin-bottom: 10px;
}

/* Absätze und Listen */
p {
    margin-bottom: 15px;
}

ul, ol {
    margin-left: 20px;
    margin-bottom: 15px;
}

li {
    margin-bottom: 8px;
}

/* Bilder: Responsive */
img {
    max-width: 100%;
    height: auto;
    display: block;
}

/* Projekt-Karten: Eine Spalte auf Mobile */
.projekte-grid {
    display: grid;
    grid-template-columns: 1fr; /* Nur 1 Spalte */
    gap: 20px;
}

.projekt-karte {
    background-color: #F8F8F8;
    border-left: 4px solid #376B8C;
    padding: 20px;
    border-radius: 8px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.projekt-karte:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.projekt-karte h3 {
    margin-top: 0;
    color: #376B8C;
}

.projekt-karte img {
    margin-bottom: 15px;
    border-radius: 5px;
}

/* Skills-Liste: Kompakt */
.skills-liste {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.skill-item {
    background-color: #E8F4F8;
    padding: 12px 15px;
    border-left: 4px solid #29786A;
    border-radius: 5px;
}

/* Footer: Kompakt */
footer {
    background-color: #2C2C2C;
    color: white;
    text-align: center;
    padding: 20px 15px;
    margin-top: 40px;
}

footer p {
    margin: 0;
    font-size: 14px;
}

/* Links generell */
a {
    color: #376B8C;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

/* Formulare: Touch-freundlich */
input, textarea, select {
    font-size: 16px; /* Verhindert Zoom auf iOS */
    padding: 12px;
    width: 100%;
    border: 2px solid #DDD;
    border-radius: 5px;
    margin-bottom: 15px;
}

button {
    background-color: #376B8C;
    color: white;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    width: 100%;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #29786A;
}
```

---

### Teil 3: Dein HTML-Markup anpassen (15 Min)

Stelle sicher, dass dein HTML die richtigen Klassen nutzt, damit das CSS greift.

**Beispiel für die Projekt-Sektion:**

```html
<section id="projekte">
    <h2>Meine Projekte</h2>
    
    <div class="projekte-grid">
        <article class="projekt-karte">
            <img src="images/projekt1.jpg" alt="Portfolio-Website Screenshot">
            <h3>Portfolio-Website</h3>
            <p><strong>Technologien:</strong> HTML, CSS</p>
            <p>Meine erste professionelle Website mit responsivem Design und modernem Layout.</p>
        </article>
        
        <article class="projekt-karte">
            <img src="images/projekt2.jpg" alt="Platzhalter für zweites Projekt">
            <h3>To-Do App</h3>
            <p><strong>Technologien:</strong> HTML, CSS, JavaScript (geplant)</p>
            <p>Eine interaktive To-Do-Liste zum Lernen von JavaScript und DOM-Manipulation.</p>
        </article>
        
        <article class="projekt-karte">
            <img src="images/projekt3.jpg" alt="Platzhalter für drittes Projekt">
            <h3>API-Projekt</h3>
            <p><strong>Technologien:</strong> HTML, CSS, JavaScript, API (geplant)</p>
            <p>Ein Projekt, das Daten von einer Web-API abruft und anzeigt.</p>
        </article>
    </div>
</section>
```

**Beispiel für Skills-Sektion:**

```html
<section id="skills">
    <h2>Meine Skills</h2>
    
    <div class="skills-liste">
        <div class="skill-item">
            <strong>HTML5</strong> – Semantisches Markup, Formulare, Accessibility
        </div>
        <div class="skill-item">
            <strong>CSS3</strong> – Responsive Design, Flexbox, Grid, Animationen
        </div>
        <div class="skill-item">
            <strong>JavaScript</strong> – DOM-Manipulation, Event Handling (in Arbeit)
        </div>
        <div class="skill-item">
            <strong>Git & GitHub</strong> – Versionskontrolle, Branching, Pull Requests
        </div>
    </div>
</section>
```

---

### Teil 4: Mobile Optimierungen testen (10 Min)

**Teste deine Seite im Responsive-Modus:**

1. **Browser DevTools öffnen** (F12)
2. **Device Toolbar aktivieren** (Handy-Symbol oder Ctrl+Shift+M)
3. **Verschiedene Geräte testen:**
   - iPhone 14 Pro (393 x 852)
   - iPhone SE (375 x 667)
   - Samsung Galaxy S21 (360 x 800)

**Prüfe folgende Punkte:**

- **Navigation:** Funktionieren alle Links? Sind sie gross genug zum Tippen (min. 44x44px)?
- **Text:** Ist alles gut lesbar ohne zu zoomen?
- **Bilder:** Werden sie korrekt skaliert?
- **Abstände:** Sind alle Elemente gut voneinander getrennt?
- **Formulare:** Sind Eingabefelder und Buttons gross genug?

---

## Erfolgskriterien

- [ ] Viewport Meta-Tag ist im `<head>` eingebunden
- [ ] Deine Seite sieht auf einem Smartphone (375px Breite) professionell aus
- [ ] Navigation ist vertikal und alle Links sind gut klickbar
- [ ] Texte sind ohne Zoom lesbar (min. 16px Schriftgrösse)
- [ ] Projekt-Karten werden untereinander angezeigt (1 Spalte)
- [ ] Alle Bilder skalieren korrekt
- [ ] Buttons und Formulare sind touch-freundlich
- [ ] Keine horizontalen Scrollbalken auf schmalen Bildschirmen

---

## Tipps

**Touch-Targets:** Apple und Google empfehlen mindestens 44x44 Pixel für klickbare Elemente auf Touch-Geräten. Deine Links und Buttons sollten diese Grösse haben.

**Font-Size:** Mindestens 16px für Body-Text auf Mobil, damit iOS Safari nicht automatisch reinzoomt, wenn man ein Eingabefeld fokussiert.

**Sticky Navigation:** `position: sticky` sorgt dafür, dass die Navigation beim Scrollen sichtbar bleibt – sehr praktisch auf langen Seiten.

**DevTools-Shortcut:** `Ctrl+Shift+M` (Windows) oder `Cmd+Shift+M` (Mac) aktiviert direkt den Responsive-Modus.

**Performance:** Optimiere deine Bilder für Mobile! Grosse Bilder laden langsam auf mobilen Netzwerken. Nutze Tools wie TinyPNG oder Squoosh.

---

## Häufige Fehler

**Viewport vergessen:** Ohne `<meta name="viewport">` funktioniert nichts. Der Browser zeigt dann die Desktop-Version nur sehr klein an.

**Zu kleine Schrift:** Texte unter 14px sind auf Smartphones schwer lesbar. Bleib bei mindestens 16px für normalen Text.

**Zu enge Abstände:** Buttons, die zu nahe beieinander sind, führen zu Fehlklicks. Mindestens 8-10px Abstand zwischen klickbaren Elementen.

**Horizontales Scrolling:** Wenn Elemente breiter als 100% sind (z.B. ein Bild mit fester Breite von 800px), entsteht ein horizontaler Scrollbalken. Immer `max-width: 100%` für Bilder nutzen!

**Feste Höhen:** Vermeide feste `height`-Werte für Bereiche mit Text. Auf verschiedenen Geräten braucht Text unterschiedlich viel Platz.

---

## Reflexionsfragen

1. **Viewport Meta-Tag:** Warum ist `<meta name="viewport" content="width=device-width, initial-scale=1.0">` im Head notwendig? Was passiert ohne diesen Tag?

2. **Mobile-First:** Du schreibst jetzt CSS zuerst für Mobile. Warum ist dieser Ansatz besser als Desktop-First (wo man später für Mobile anpasst)?

3. **Touch-Targets:** Deine Navigations-Links haben `padding: 15px 20px`. Berechne die minimale Grösse des klickbaren Bereichs. Entspricht das den empfohlenen 44x44 Pixel?

4. **Flexbox vs. Grid:** In diesem Auftrag nutzt du `display: flex` für die Navigation und `display: grid` für die Projekt-Karten. Kannst du erklären, wann du Flexbox und wann Grid nutzen würdest?

5. **Performance:** Ein Nutzer hat langsames mobiles Internet (3G). Welche Teile deiner Website könnten lange laden und wie könntest du das optimieren?

---

## Weiterführende Links

**Responsive Design Grundlagen:**
- [MDN: Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [W3Schools: Responsive Web Design](https://www.w3schools.com/css/css_rwd_intro.asp)

**Viewport & Meta-Tags:**
- [MDN: Viewport Meta-Tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag)
- [Google: Responsive Web Design Basics](https://web.dev/responsive-web-design-basics/)

**Touch-Targets & Mobile UX:**
- [Material Design: Touch Targets](https://m3.material.io/foundations/interaction/gestures)
- [Apple: Human Interface Guidelines - Touch](https://developer.apple.com/design/human-interface-guidelines/touchscreens)

**DevTools & Testing:**
- [Chrome DevTools: Device Mode](https://developer.chrome.com/docs/devtools/device-mode/)
- [Firefox: Responsive Design Mode](https://firefox-source-docs.mozilla.org/devtools-user/responsive_design_mode/)

**Mobile Performance:**
- [TinyPNG - Bildkompression](https://tinypng.com/)
- [Squoosh - Google Image Optimizer](https://squoosh.app/)
- [PageSpeed Insights](https://pagespeed.web.dev/)

---

⏱️ **Geschätzte Zeit:** 50 Minuten
