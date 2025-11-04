# Auftrag 3: External Stylesheet – Die professionelle Lösung

## Ziel
Du erstellst eine separate CSS-Datei und verlinkst sie in deinem HTML. Du verstehst, warum externe Stylesheets die beste Lösung für professionelle Webprojekte sind und kannst dein CSS strukturiert organisieren.

## Beschreibung

Internal Styles funktionieren gut für einzelne Seiten, aber was ist mit grösseren Projekten mit mehreren HTML-Seiten? Die Lösung: Eine zentrale CSS-Datei, die von allen Seiten genutzt wird.

---

### Teil 1: CSS-Datei erstellen (10 Min)

**1. Erstelle eine neue Datei `styles.css` im selben Ordner wie deine `index.html`:**

**Projektstruktur:**
```
mein-portfolio/
├── index.html
├── about.html (optional, später)
├── styles.css (NEU!)
└── images/
    └── profil.jpg
```

**2. Kopiere alle Styles aus dem `<style>`-Block in `styles.css`:**

**styles.css:**
```css
/* ==================
   PORTFOLIO STYLESHEET
   Autor: Dein Name
   Datum: November 2025
   ================== */

/* ==================
   ALLGEMEINE STYLES
   ================== */
body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    color: #333;
    margin: 0;
    padding: 0;
}

/* ==================
   ÜBERSCHRIFTEN
   ================== */
h1 {
    color: #376B8C;
    font-size: 48px;
    text-align: center;
    margin-bottom: 10px;
}

h2 {
    color: #29786A;
    font-size: 32px;
    border-bottom: 3px solid #45BA98;
    padding-bottom: 10px;
    margin-top: 40px;
}

h3 {
    color: #376B8C;
    font-size: 24px;
}

/* ==================
   HEADER
   ================== */
header {
    background-color: #376B8C;
    color: white;
    padding: 60px 20px;
    text-align: center;
}

header h1 {
    color: white;
    margin: 0;
}

header p {
    color: #E8F4F8;
    font-size: 18px;
    margin: 10px 0 0 0;
}

/* ==================
   NAVIGATION
   ================== */
nav {
    background-color: #4E9BCC;
    padding: 15px;
    text-align: center;
}

nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

nav ul li {
    display: inline-block;
    margin: 0 15px;
}

nav a {
    color: white;
    text-decoration: none;
    font-weight: bold;
    font-size: 16px;
}

nav a:hover {
    text-decoration: underline;
}

/* ==================
   MAIN CONTENT
   ================== */
main {
    max-width: 900px;
    margin: 0 auto;
    padding: 40px 20px;
}

section {
    margin-bottom: 60px;
}

/* ==================
   LISTEN
   ================== */
ul {
    list-style: none;
    padding-left: 0;
}

ul li {
    background-color: #F8F8F8;
    padding: 12px 20px;
    margin-bottom: 10px;
    border-left: 4px solid #376B8C;
    font-size: 16px;
}

ul li strong {
    color: #376B8C;
    font-size: 18px;
}

/* ==================
   PROJEKT-KARTEN
   ================== */
article {
    background-color: #F8F8F8;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 30px;
}

article h3 {
    margin-top: 0;
    color: #376B8C;
}

article img {
    max-width: 100%;
    height: auto;
    border-radius: 4px;
}

article p {
    color: #666;
    font-size: 16px;
}

/* ==================
   LINKS
   ================== */
a {
    color: #376B8C;
    text-decoration: none;
    transition: color 0.3s;
}

a:hover {
    color: #4E9BCC;
    text-decoration: underline;
}

a:visited {
    color: #29786A;
}

/* ==================
   FOOTER
   ================== */
footer {
    background-color: #1F3B4E;
    color: white;
    text-align: center;
    padding: 30px 20px;
    margin-top: 60px;
}

footer a {
    color: #45BA98;
}
```

---

### Teil 2: CSS in HTML einbinden (5 Min)

**Ersetze den `<style>`-Block in deiner `index.html` durch einen `<link>`-Tag:**

**index.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dein Name - Portfolio</title>
    
    <!-- Externe CSS-Datei einbinden -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Dein HTML-Content bleibt unverändert -->
</body>
</html>
```

**Wichtig:**
- `rel="stylesheet"` sagt dem Browser: "Das ist ein Stylesheet"
- `href="styles.css"` ist der Pfad zur CSS-Datei
- Der `<link>`-Tag gehört in den `<head>`

**Teste im Browser:** Die Seite sollte exakt gleich aussehen wie vorher!

---

### Teil 3: Mehrere Seiten mit demselben Stylesheet (15 Min)

**Erstelle eine zweite HTML-Seite, die dasselbe Stylesheet nutzt:**

**about.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Über mich - Dein Name</title>
    
    <!-- Dasselbe Stylesheet wie auf der Hauptseite! -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Über mich</h1>
        <p><a href="index.html" style="color: white;">← Zurück zur Startseite</a></p>
    </header>
    
    <nav>
        <ul>
            <li><a href="index.html">Home</a></li>
            <li><a href="about.html">Über mich</a></li>
            <li><a href="#kontakt">Kontakt</a></li>
        </ul>
    </nav>
    
    <main>
        <section>
            <h2>Mein Werdegang</h2>
            <p>Hier kannst du mehr über deinen Werdegang schreiben...</p>
            
            <h3>Ausbildung</h3>
            <ul>
                <li><strong>Seit 2024:</strong> Informatiker/in EFZ in Ausbildung</li>
                <li><strong>2021-2024:</strong> Sekundarschule</li>
            </ul>
            
            <h3>Hobbies</h3>
            <ul>
                <li>Programmieren</li>
                <li>Gaming</li>
                <li>Musik</li>
            </ul>
        </section>
    </main>
    
    <footer>
        <p>© 2025 Dein Name</p>
    </footer>
</body>
</html>
```

**Aktualisiere die Navigation in `index.html`:**
```html
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">Über mich</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projekte">Projekte</a></li>
        <li><a href="#kontakt">Kontakt</a></li>
    </ul>
</nav>
```

**Der grosse Vorteil:**
- Beide Seiten nutzen `styles.css`
- Änderst du eine Farbe in `styles.css`, ändern sich beide Seiten!
- Du musst das CSS nicht kopieren

---

### Teil 4: CSS-Organisation verbessern (10 Min)

**Füge am Anfang deiner `styles.css` einen Variablen-ähnlichen Kommentarblock hinzu:**

```css
/* ==================
   FARBPALETTE
   ================== */
/*
   Primär:    #376B8C (Blau)
   Sekundär:  #29786A (Türkis)
   Akzent:    #CD7A15 (Orange)
   Hintergrund: #F8F8F8 (Hellgrau)
   Text:      #333 (Dunkelgrau)
*/

/* ==================
   TYPOGRAFIE
   ================== */
/*
   Schrift:   Arial, sans-serif
   H1:        48px
   H2:        32px
   H3:        24px
   Body:      16px
   Line-Height: 1.6
*/
```

**Profitipp:** Später wirst du CSS-Variablen (Custom Properties) lernen, dann kannst du Farben zentral definieren!

---

## Erfolgskriterien

- [ ] Eine separate `styles.css` existiert im Projektordner
- [ ] Der `<style>`-Block ist aus `index.html` entfernt
- [ ] Ein `<link rel="stylesheet" href="styles.css">` ist im `<head>`
- [ ] Die Seite sieht im Browser identisch aus wie vorher
- [ ] Eine zweite HTML-Seite (`about.html`) nutzt dasselbe Stylesheet
- [ ] Die Navigation funktioniert zwischen den Seiten
- [ ] Das CSS ist mit Kommentaren strukturiert
- [ ] Änderungen in `styles.css` wirken sich auf alle Seiten aus

## Tipps

- **Relativer Pfad:** `href="styles.css"` funktioniert, wenn die CSS-Datei im selben Ordner ist
- Für Unterordner: `href="css/styles.css"` (wenn CSS in einem `css/`-Ordner liegt)
- **DevTools:** In den DevTools (F12) → Sources → siehst du alle geladenen Dateien inkl. CSS
- **Cache leeren:** `Ctrl+Shift+R` (Hard Reload) lädt CSS neu, falls Änderungen nicht sichtbar sind
- **Profitipp:** Erstelle einen `css/`-Ordner für mehrere Stylesheets (z.B. `reset.css`, `styles.css`)

## Reflexionsfragen

1. Was passiert, wenn du den Pfad in `href="styles.css"` falsch schreibst? Teste es!
2. Öffne DevTools (F12) → Network → Lade die Seite neu. Siehst du, dass `styles.css` geladen wird?
3. Ändere eine Farbe in `styles.css` und lade `index.html` und `about.html` – ändern sich beide?
4. Was ist besser: Ein grosses `styles.css` oder mehrere kleine CSS-Dateien? Warum?
5. Inspiziere mit DevTools: Wo werden die Styles angewendet? Siehst du `styles.css` als Quelle?

## Weiterführende Links

- [MDN: `<link>` Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link)
- [MDN: CSS File Structure](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing)
- [CSS Guidelines by Harry Roberts](https://cssguidelin.es/)
- [BEM Naming Convention](http://getbem.com/) – Für strukturierte CSS-Klassen
- [CSS Tricks: Organizing CSS](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)

---

**⏱️ Geschätzte Zeit:** 30-35 Minuten  
**📦 Nächster Schritt:** Optional: Vertiefe dein Wissen über CSS-Organisation und Best Practices!
