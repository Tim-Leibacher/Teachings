# Auftrag 1: Element- und Klassen-Selektoren – Gezielt stylen

## Ziel
Du lernst den Unterschied zwischen Element- und Klassen-Selektoren kennen und verstehst, wann du welchen Selektor verwendest. Du stylst dein Portfolio gezielt mit verschiedenen Selektor-Typen.

## Beschreibung

In den vorherigen Aufträgen hast du bereits Element-Selektoren wie `h1` oder `p` verwendet. Jetzt lernst du Klassen-Selektoren kennen – die flexibelste und am häufigsten genutzte Art, CSS zu schreiben.

---

### Teil 1: Element-Selektoren verstehen (15 Min)

**Element-Selektoren sprechen ALLE Elemente eines Typs an.**

**Öffne deine `styles.css` und prüfe deine bestehenden Element-Selektoren:**

```css
/* ==================
   ELEMENT-SELEKTOREN
   ================== */

/* Spricht ALLE <p>-Tags auf der Seite an */
p {
    color: #666;
    font-size: 16px;
    line-height: 1.6;
    margin-bottom: 15px;
}

/* Spricht ALLE <h2>-Tags auf der Seite an */
h2 {
    color: #29786A;
    font-size: 32px;
    border-bottom: 3px solid #45BA98;
    padding-bottom: 10px;
    margin-top: 40px;
}

/* Spricht ALLE <a>-Tags auf der Seite an */
a {
    color: #376B8C;
    text-decoration: none;
    transition: color 0.3s;
}

a:hover {
    color: #4E9BCC;
    text-decoration: underline;
}
```

**Das Problem mit Element-Selektoren:**
- Was, wenn du EINEN Absatz anders stylen möchtest?
- Was, wenn nicht alle Links gleich aussehen sollen?
- Element-Selektoren sind zu unspezifisch für detailliertes Design

**Teste es:** Füge in deine `index.html` einen Absatz ein, der sich vom Rest unterscheiden soll:

```html
<p>Normaler Absatz mit Standard-Styling.</p>
<p>Dieser Absatz sollte anders aussehen – grösser und fett!</p>
```

Mit Element-Selektoren allein kannst du den zweiten Absatz nicht anders stylen!

---

### Teil 2: Klassen-Selektoren einführen (20 Min)

**Klassen-Selektoren beginnen mit einem Punkt (`.`) und können mehrfach verwendet werden.**

**1. Erstelle verschiedene Klassen für deine Texte:**

**styles.css:**
```css
/* ==================
   KLASSEN-SELEKTOREN
   ================== */

/* Intro-Text: Grösser und hervorgehoben */
.intro {
    font-size: 20px;
    font-weight: 500;
    color: #376B8C;
    line-height: 1.8;
    margin-bottom: 30px;
}

/* Highlight-Text: Mit farbigem Hintergrund */
.highlight {
    background-color: #FFF8DC;
    padding: 15px;
    border-left: 4px solid #CD7A15;
    margin: 20px 0;
}

/* Small-Text: Kleinere Schrift für Nebensächliches */
.small-text {
    font-size: 14px;
    color: #999;
    font-style: italic;
}

/* Bold-Text: Fette Hervorhebung */
.bold {
    font-weight: bold;
    color: #376B8C;
}
```

**2. Wende die Klassen in deinem HTML an:**

```html
<main>
    <section id="ueber-mich">
        <h2>Über mich</h2>
        
        <!-- Intro-Text mit Klasse -->
        <p class="intro">
            Willkommen auf meinem Portfolio! Ich bin Lernende/r im 1. Lehrjahr 
            als Informatiker/in EFZ und zeige hier meine Projekte und Fortschritte.
        </p>
        
        <!-- Normaler Absatz ohne Klasse -->
        <p>
            Seit August 2024 lerne ich bei <span class="bold">Firma XY AG</span> 
            die Grundlagen der Applikationsentwicklung.
        </p>
        
        <!-- Highlight-Box -->
        <p class="highlight">
            Mein Ziel: Eine vollständige Webanwendung mit React und Express erstellen!
        </p>
        
        <!-- Kleiner Zusatztext -->
        <p class="small-text">
            Letzte Aktualisierung: November 2025
        </p>
    </section>
</main>
```

**Siehst du den Unterschied?**
- Mit Klassen kannst du gezielt einzelne Elemente stylen
- Dieselbe Klasse kann mehrfach verwendet werden
- HTML bleibt übersichtlich, CSS übernimmt das Design

---

### Teil 3: Klassen für Buttons erstellen (15 Min)

**Erstelle verschiedene Button-Styles mit Klassen:**

```css
/* ==================
   BUTTON-STYLES
   ================== */

/* Basis-Button */
.btn {
    display: inline-block;
    padding: 12px 24px;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    border-radius: 4px;
    transition: all 0.3s;
    cursor: pointer;
}

/* Primärer Button (Blau) */
.btn-primary {
    background-color: #376B8C;
    color: white;
}

.btn-primary:hover {
    background-color: #4E9BCC;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

/* Sekundärer Button (Türkis) */
.btn-secondary {
    background-color: #29786A;
    color: white;
}

.btn-secondary:hover {
    background-color: #45BA98;
}

/* Outline-Button */
.btn-outline {
    background-color: transparent;
    color: #376B8C;
    border: 2px solid #376B8C;
}

.btn-outline:hover {
    background-color: #376B8C;
    color: white;
}
```

**Wende die Button-Klassen an:**

```html
<section id="projekte">
    <h2>Meine Projekte</h2>
    
    <article>
        <h3>Portfolio-Website</h3>
        <p>Meine erste eigene Website mit HTML und CSS.</p>
        
        <!-- Kombiniere mehrere Klassen! -->
        <a href="projekt1.html" class="btn btn-primary">Projekt ansehen</a>
        <a href="https://github.com/username/portfolio" class="btn btn-outline">Code auf GitHub</a>
    </article>
</section>
```

**Wichtig:** Du kannst mehrere Klassen kombinieren: `class="btn btn-primary"`

---

### Teil 4: Container-Klassen für Layout (15 Min)

**Erstelle Klassen für wiederkehrende Layout-Elemente:**

```css
/* ==================
   CONTAINER & LAYOUT
   ================== */

/* Zentrierter Container mit maximaler Breite */
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Enger Container für Text-Inhalte */
.container-narrow {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Card-Container */
.card {
    background-color: #F8F8F8;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 30px;
    transition: transform 0.3s, box-shadow 0.3s;
}

.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

/* Card-Header */
.card-header {
    border-bottom: 2px solid #D0D0D0;
    padding-bottom: 15px;
    margin-bottom: 15px;
}

/* Card-Body */
.card-body {
    color: #666;
    line-height: 1.6;
}

/* Card-Footer */
.card-footer {
    border-top: 1px solid #E0E0E0;
    padding-top: 15px;
    margin-top: 15px;
    text-align: right;
}
```

**Nutze die Container-Klassen:**

```html
<main class="container">
    <section id="projekte">
        <h2>Meine Projekte</h2>
        
        <article class="card">
            <div class="card-header">
                <h3>Portfolio-Website</h3>
            </div>
            <div class="card-body">
                <p>Meine erste eigene Website, erstellt mit HTML5 und CSS3.</p>
                <p>Technologien: HTML, CSS, Responsive Design</p>
            </div>
            <div class="card-footer">
                <a href="#" class="btn btn-primary">Mehr erfahren</a>
            </div>
        </article>
        
        <article class="card">
            <div class="card-header">
                <h3>JavaScript To-Do App</h3>
            </div>
            <div class="card-body">
                <p>Interaktive Aufgabenliste mit Speicherung im Browser.</p>
                <p>Technologien: HTML, CSS, JavaScript, LocalStorage</p>
            </div>
            <div class="card-footer">
                <a href="#" class="btn btn-primary">Mehr erfahren</a>
            </div>
        </article>
    </section>
</main>
```

---

## Erfolgskriterien

- [ ] Du verstehst den Unterschied zwischen Element- und Klassen-Selektoren
- [ ] Mindestens 5 verschiedene Klassen sind in `styles.css` definiert
- [ ] Klassen für Text-Styles (intro, highlight, small-text) sind implementiert
- [ ] Button-Klassen mit verschiedenen Varianten existieren
- [ ] Container- und Card-Klassen sind erstellt und im HTML angewendet
- [ ] Mindestens 10 HTML-Elemente nutzen Klassen
- [ ] Mehrere Klassen können kombiniert werden (z.B. `class="btn btn-primary"`)
- [ ] Die Seite ist visuell strukturierter als vorher

## Tipps

- **Klassen-Namen:** Nutze aussagekräftige Namen (`.card` statt `.box1`)
- **Kebab-Case:** Nutze Bindestriche für mehrteilige Namen (`.btn-primary` statt `.btnPrimary`)
- **BEM-Methodik:** Fortgeschrittenes Namensschema (später relevant)
- **DevTools:** Inspiziere Elemente mit F12 → siehst du die angewendeten Klassen?
- **Profitipp:** Erstelle eine Klasse für ein Design-Element, dann kannst du es überall wiederverwenden
- Klassen können kombiniert werden: `class="card highlight"` wendet beide Styles an

## Reflexionsfragen

1. Wann würdest du einen Element-Selektor verwenden und wann eine Klasse?
2. Experimentiere: Füge einem `<p>` zwei Klassen hinzu (`class="intro highlight"`). Was passiert?
3. Was ist der Vorteil von `.btn-primary` gegenüber `#submit-button` (ID)?
4. Erstelle eine Klasse `.error` für Fehler-Meldungen. Welche Farbe, Grösse und Rahmen würdest du nutzen?
5. Öffne DevTools (F12) → Elements: Kannst du sehen, welche Klassen auf ein Element angewendet sind?
6. Was passiert, wenn zwei Klassen dieselbe Eigenschaft definieren (z.B. beide setzen `color`)? Teste es!

## Weiterführende Links

**Selektoren:**
- [MDN: CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [MDN: Class Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors)
- [CSS Tricks: The Difference Between ID and Class](https://css-tricks.com/the-difference-between-id-and-class/)

**Naming Conventions:**
- [BEM Methodology](http://getbem.com/)
- [CSS Guidelines – Naming](https://cssguidelin.es/#naming-conventions)
- [SMACSS – Scalable CSS](http://smacss.com/)

**Best Practices:**
- [Google CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Airbnb CSS Style Guide](https://github.com/airbnb/css)

**Tools:**
- [CSS Stats](https://cssstats.com/) – Analysiere dein CSS
- [Can I Use](https://caniuse.com/) – Browser-Kompatibilität prüfen

---

**Geschätzte Zeit:** 40-45 Minuten  
**Nächster Schritt:** In Auftrag 2 lernst du das Box-Modell und wie Abstände funktionieren!
