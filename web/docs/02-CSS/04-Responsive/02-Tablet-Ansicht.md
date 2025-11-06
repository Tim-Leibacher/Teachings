# Auftrag 2: Tablet-Ansicht – Media Queries einsetzen

## Ziel
Du lernst Media Queries kennen und erweiterst dein Portfolio für Tablet-Grössen. Du verstehst, wie Breakpoints funktionieren und kannst das Layout für mittlere Bildschirme optimieren.

## Beschreibung

Dein Portfolio sieht auf dem Smartphone jetzt professionell aus. In diesem Auftrag erweiterst du das CSS mit Media Queries, damit auch Tablets (768px bis 1023px) optimal bedient werden. Du lernst, wie man schrittweise vom Mobile- zum Desktop-Layout übergeht.

---

### Teil 1: Media Query Grundlagen verstehen (10 Min)

Eine Media Query ist eine CSS-Regel, die nur unter bestimmten Bedingungen greift – zum Beispiel ab einer bestimmten Bildschirmbreite.

**Grundlegende Syntax:**

```css
/* Dieser Code gilt für ALLE Bildschirme (Mobile First) */
.element {
    font-size: 16px;
}

/* Dieser Code gilt AB 768px Breite (Tablet und Desktop) */
@media (min-width: 768px) {
    .element {
        font-size: 18px;
    }
}
```

**Wichtig:** Das `@media (min-width: 768px)` bedeutet "ab 768 Pixel Breite". Alles, was du dort reinschreibst, gilt zusätzlich zu den Basis-Styles.

**Typische Breakpoints:**
- **Mobile:** 0-767px (keine Media Query nötig, das ist deine Basis)
- **Tablet:** 768px-1023px (`@media (min-width: 768px)`)
- **Desktop:** 1024px+ (`@media (min-width: 1024px)`)

---

### Teil 2: Erste Media Query für Tablets hinzufügen (20 Min)

**Öffne deine `styles.css` und füge am Ende hinzu:**

```css
/* ==========================================
   TABLET-ANSICHT (768px - 1023px)
   ========================================== */

@media (min-width: 768px) {
    
    /* Container: Mehr Seitenabstand */
    .container {
        padding: 0 30px;
    }
    
    /* Header: Grössere Schrift */
    header {
        padding: 50px 30px;
    }
    
    header h1 {
        font-size: 36px;
        margin-bottom: 12px;
    }
    
    header p {
        font-size: 18px;
    }
    
    /* Navigation: Horizontal statt vertikal */
    nav ul {
        flex-direction: row; /* Von column zu row! */
        justify-content: center;
        gap: 0;
    }
    
    nav li {
        width: auto; /* Nicht mehr volle Breite */
    }
    
    nav a {
        padding: 15px 25px;
        border-bottom: none; /* Keine Trennlinien mehr */
        border-right: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    nav li:last-child a {
        border-right: none;
    }
    
    /* Main Content: Mehr Abstand */
    main {
        padding: 40px 30px;
    }
    
    section {
        margin-bottom: 60px;
    }
    
    section h2 {
        font-size: 32px;
        margin-bottom: 20px;
    }
    
    section h3 {
        font-size: 24px;
        margin-bottom: 12px;
    }
    
    /* Projekt-Karten: 2 Spalten */
    .projekte-grid {
        grid-template-columns: repeat(2, 1fr); /* 2 statt 1 Spalte */
        gap: 30px;
    }
    
    .projekt-karte {
        padding: 25px;
    }
    
    /* Skills-Liste: 2 Spalten */
    .skills-liste {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 15px;
    }
    
    /* Formulare: Nicht mehr volle Breite */
    input, textarea, select {
        max-width: 600px;
    }
    
    button {
        width: auto;
        min-width: 200px;
    }
    
    /* Footer: Mehr Abstand */
    footer {
        padding: 30px;
    }
    
    footer p {
        font-size: 15px;
    }
}
```

---

### Teil 3: Navigation optimieren (15 Min)

Die Navigation ist auf Tablets jetzt horizontal, aber wir können sie noch besser machen.

**Ergänze deine Media Query:**

```css
@media (min-width: 768px) {
    /* ... vorheriger Code ... */
    
    /* Navigation: Hover-Effekte anpassen */
    nav a {
        padding: 15px 25px;
        position: relative;
    }
    
    nav a::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        width: 0;
        height: 3px;
        background-color: #FEAF51;
        transition: width 0.3s ease;
    }
    
    nav a:hover::after,
    nav a:focus::after {
        width: 80%;
    }
    
    nav a:hover,
    nav a:focus {
        background-color: rgba(255, 255, 255, 0.05);
    }
}
```

**Was macht dieser Code?**
- Beim Hover erscheint ein animierter orangener Balken unter dem Link
- Der Hintergrund wird leicht aufgehellt
- Sieht viel professioneller aus als nur ein Farbwechsel

---

### Teil 4: Über-mich-Sektion mit Bild & Text (20 Min)

Auf Tablets haben wir mehr Platz. Wir können Text und Bild nebeneinander anzeigen.

**Erstelle oder ergänze in deiner `index.html`:**

```html
<section id="ueber-mich">
    <h2>Über mich</h2>
    
    <div class="ueber-mich-content">
        <div class="profilbild">
            <img src="images/profil.jpg" alt="Dein Name - Profilbild">
        </div>
        <div class="ueber-mich-text">
            <p>
                Hallo! Ich bin <strong>Dein Name</strong> und befinde mich im 
                ersten Lehrjahr der Ausbildung zum/zur Informatiker/in EFZ mit 
                Fachrichtung Applikationsentwicklung.
            </p>
            <p>
                Meine Leidenschaft für Technologie begann bereits in der Schule, 
                als ich meine erste Website erstellt habe. Seitdem möchte ich 
                verstehen, wie Software entwickelt wird und wie man Probleme mit 
                Code lösen kann.
            </p>
            <p>
                In meiner Freizeit beschäftige ich mich mit Programmier-Projekten, 
                spiele Videospiele und interessiere mich für neue Technologien. 
                Mein Ziel ist es, eines Tages eigene Apps zu entwickeln, die 
                Menschen im Alltag helfen.
            </p>
        </div>
    </div>
</section>
```

**Jetzt das CSS für Tablets:**

```css
/* Basis-CSS (Mobile) */
.ueber-mich-content {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.profilbild img {
    width: 100%;
    max-width: 300px;
    margin: 0 auto;
    border-radius: 50%;
    border: 5px solid #376B8C;
}

/* Tablet-Ansicht: Nebeneinander */
@media (min-width: 768px) {
    .ueber-mich-content {
        flex-direction: row;
        align-items: flex-start;
        gap: 40px;
    }
    
    .profilbild {
        flex-shrink: 0; /* Bild behält seine Grösse */
    }
    
    .profilbild img {
        width: 250px;
        height: 250px;
        object-fit: cover;
    }
    
    .ueber-mich-text {
        flex: 1; /* Text nimmt verfügbaren Platz */
    }
}
```

---

### Teil 5: Testen und Feintuning (15 Min)

**Teste deine Seite in verschiedenen Breiten:**

1. **DevTools öffnen** (F12) und Device Toolbar aktivieren (Ctrl+Shift+M)
2. **Teste verschiedene Tablet-Grössen:**
   - iPad Mini (768 x 1024)
   - iPad Air (820 x 1180)
   - iPad Pro (1024 x 1366)
3. **Ändere die Breite manuell** (oben in DevTools) und beobachte:
   - Bei 767px → Mobile-Ansicht (1 Spalte, vertikale Navigation)
   - Bei 768px → Tablet-Ansicht (2 Spalten, horizontale Navigation)

**Prüfe diese Übergänge:**

**Navigation:**
```
Mobile (767px):           Tablet (768px):
┌─────────────┐           ┌───────────────────┐
│   Home      │           │ Home | About | ... │
│   About     │           └───────────────────┘
│   Projects  │
└─────────────┘
```

**Projekt-Karten:**
```
Mobile (767px):           Tablet (768px):
┌─────────────┐           ┌──────┐  ┌──────┐
│  Projekt 1  │           │ Proj │  │ Proj │
└─────────────┘           │  1   │  │  2   │
┌─────────────┐           └──────┘  └──────┘
│  Projekt 2  │           ┌──────┐  ┌──────┐
└─────────────┘           │ Proj │  │ Proj │
                          │  3   │  │  4   │
                          └──────┘  └──────┘
```

---

### Teil 6: Responsive Bilder optimieren (Optional, 10 Min)

Für Tablets kannst du grössere Bilder laden (auf Mobile würden kleine Bilder reichen).

**HTML mit `srcset` (fortgeschritten):**

```html
<img src="images/projekt1-small.jpg"
     srcset="images/projekt1-small.jpg 400w,
             images/projekt1-medium.jpg 800w,
             images/projekt1-large.jpg 1200w"
     sizes="(max-width: 767px) 100vw,
            (max-width: 1023px) 50vw,
            33vw"
     alt="Portfolio-Website Screenshot">
```

**Erklärung:**
- `srcset` definiert verschiedene Bildgrössen
- `sizes` sagt dem Browser, welche Grösse er laden soll
- Mobile: 100vw (volle Breite)
- Tablet: 50vw (halbe Breite, wegen 2 Spalten)
- Desktop: 33vw (ein Drittel, wegen 3 Spalten)

---

## Erfolgskriterien

- [ ] Media Query `@media (min-width: 768px)` ist in der CSS-Datei
- [ ] Navigation wechselt bei 768px von vertikal zu horizontal
- [ ] Projekt-Karten werden auf Tablets in 2 Spalten angezeigt
- [ ] Skills-Liste hat auf Tablets 2 Spalten statt 1
- [ ] Über-mich-Sektion zeigt Bild und Text nebeneinander
- [ ] Schriftgrössen und Abstände sind auf Tablets grösser als auf Mobile
- [ ] Der Übergang von 767px zu 768px funktioniert ohne Sprünge oder Bugs
- [ ] Die Seite sieht auf einem iPad (768px) professionell aus

---

## Tipps

**Breakpoint-Testen:** Ziehe das Browser-Fenster langsam von schmal nach breit. So siehst du genau, wo die Media Query greift und ob es harte Sprünge gibt.

**Browser-Caching:** Wenn deine Änderungen nicht sichtbar werden, drücke Ctrl+F5 (Windows) oder Cmd+Shift+R (Mac) für einen Hard-Reload.

**DevTools Responsive Mode:** Du kannst oben die Breite manuell eingeben (z.B. "768") und so genau testen, wann die Media Query greift.

**Mobile-First Debug:** Wenn etwas auf Tablet nicht funktioniert, prüfe zuerst, ob das Mobile-CSS korrekt ist. Tablet-Styles bauen auf Mobile auf!

**Flexbox Debugging:** Nutze `outline: 2px solid red;` temporär, um zu sehen, wie gross deine Flex-Container sind.

---

## Häufige Fehler

**Media Query wird nicht angewendet:** Prüfe, ob der Viewport Meta-Tag im HTML ist. Ohne ihn funktionieren Media Queries nicht.

**Styles werden überschrieben:** CSS-Spezifität! Wenn ein Style nicht greift, könnte ein anderer Selektor spezifischer sein. Nutze die Browser DevTools, um zu sehen, welche Regel gewinnt.

**Falsche Einheit:** `@media (min-width: 768)` funktioniert NICHT. Es muss `768px` sein mit der Einheit!

**Mobile-Styles in Media Query wiederholen:** Du musst nicht alles wiederholen. Die Media Query ERGÄNZT das Mobile-CSS, überschreibt es nicht komplett.

**Zu viele Breakpoints:** Fang mit 2-3 Breakpoints an (Mobile, Tablet, Desktop). Zu viele Breakpoints machen das CSS unübersichtlich.

---

## Reflexionsfragen

1. **Min-Width vs. Max-Width:** Was ist der Unterschied zwischen `@media (min-width: 768px)` und `@media (max-width: 768px)`? Wann würdest du welches nutzen?

2. **CSS-Reihenfolge:** Warum ist es wichtig, dass die Media Query für Tablets NACH dem Mobile-CSS im Stylesheet steht?

3. **Breakpoint 768px:** Warum ist 768px ein Standard-Breakpoint für Tablets? Kannst du recherchieren, welche Geräte ungefähr diese Breite haben?

4. **Performance:** Auf Mobile lädst du eine 400px breite Bilddatei, auf Tablet eine 800px breite. Warum ist das sinnvoll und wie viel Datenvolumen sparst du damit auf Mobile?

5. **Flexbox Direction:** Die Navigation wechselt von `flex-direction: column` zu `flex-direction: row`. Kannst du erklären, was genau Flexbox hier macht und warum es so einfach ist, die Richtung zu ändern?

---

## Weiterführende Links

**Media Queries:**
- [MDN: Using Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [W3Schools: CSS Media Queries](https://www.w3schools.com/css/css3_mediaqueries.asp)
- [CSS-Tricks: A Complete Guide to CSS Media Queries](https://css-tricks.com/a-complete-guide-to-css-media-queries/)

**Breakpoints:**
- [Material Design: Layout - Responsive](https://m3.material.io/foundations/layout/applying-layout/window-size-classes)
- [Bootstrap Breakpoints Documentation](https://getbootstrap.com/docs/5.3/layout/breakpoints/)

**Flexbox:**
- [MDN: Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
- [CSS-Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy - Lernspiel](https://flexboxfroggy.com/#de)

**Responsive Images:**
- [MDN: Responsive Images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
- [Web.dev: Serve Responsive Images](https://web.dev/serve-responsive-images/)

**Testing:**
- [BrowserStack: Responsive Testing](https://www.browserstack.com/responsive)
- [Responsively App - Free Tool](https://responsively.app/)

---

⏱️ **Geschätzte Zeit:** 90 Minuten
