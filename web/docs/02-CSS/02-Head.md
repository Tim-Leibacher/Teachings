# Auftrag 2: Internal Styles – CSS im Head-Bereich

## Ziel
Du lagerst deine CSS-Styles in den `<head>`-Bereich aus und nutzt CSS-Selektoren, um mehrere Elemente gleichzeitig zu stylen. Du verstehst die Vorteile von Internal Styles gegenüber Inline Styles.

## Beschreibung

Inline-Styles funktionieren für einzelne Elemente, aber sie werden schnell unübersichtlich. Die bessere Lösung für einzelne HTML-Seiten: Internal Styles im `<head>`-Bereich mit dem `<style>`-Tag.

---

### Teil 1: Von Inline zu Internal (15 Min)

**Entferne alle Inline-Styles aus deiner `index.html` und erstelle einen `<style>`-Block im `<head>`:**

**Vorher (Inline):**
```html
<h1 style="color: #376B8C; font-size: 48px;">Dein Name</h1>
<h2 style="color: #29786A;">Über mich</h2>
<h2 style="color: #29786A;">Meine Skills</h2>
```

**Nachher (Internal):**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dein Name - Portfolio</title>
    
    <style>
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
    </style>
</head>
<body>
    <h1>Dein Name</h1>
    <h2>Über mich</h2>
    <!-- Weitere Inhalte ohne Inline-Styles -->
</body>
</html>
```

**Siehst du den Unterschied?**
- Alle `<h1>` werden automatisch gleich gestylt
- Alle `<h2>` bekommen denselben Stil
- Du musst nichts mehr kopieren!

---

### Teil 2: Bereiche stylen (20 Min)

**Style deine verschiedenen Sektionen:**

```html
<style>
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
</style>
```

---

### Teil 3: Listen und Projekt-Karten stylen (15 Min)

**Style deine Skills-Liste:**

```html
<style>
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
</style>
```

**Style deine Projekt-Karten:**

```html
<style>
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
</style>
```

---

### Teil 4: Links stylen (10 Min)

```html
<style>
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
</style>
```

---

## Erfolgskriterien

- [ ] Alle Inline-Styles sind entfernt
- [ ] Ein `<style>`-Block existiert im `<head>`
- [ ] CSS-Kommentare strukturieren die verschiedenen Bereiche
- [ ] Header, Navigation, Main und Footer haben eigene Styles
- [ ] Überschriften (h1, h2, h3) werden konsistent gestylt
- [ ] Links haben Hover-Effekte
- [ ] Listen und Projekt-Karten sind gestylt
- [ ] Die Seite sieht professioneller aus als mit Inline-Styles

## Tipps

- **Kommentare nutzen:** Strukturiere dein CSS mit Kommentaren (`/* Kommentar */`)
- **Konsistenz:** Nutze dieselben Farben und Abstände für ein einheitliches Design
- **Hover-Effekte:** Nutze `:hover` für interaktive Elemente
- **DevTools:** Ändere Styles live in den DevTools (F12) und kopiere funktionierende Styles ins CSS
- **Profitipp:** Definiere am Anfang Basis-Styles für `body`, dann werden sie überall angewendet
- Nutze `max-width` für `main`, damit die Seite auf grossen Bildschirmen nicht zu breit wird

## Reflexionsfragen

1. Was ist der Unterschied zwischen `header` (Element-Selektor) und `header h1` (Verschachtelung)?
2. Warum ist `nav a` spezifischer als nur `a`? Was wird zuerst angewendet?
3. Experimentiere: Ändere die Farbe von `h2` auf Rot. Werden alle `<h2>` auf der Seite rot?
4. Was passiert, wenn du dieselbe Eigenschaft zweimal im selben Selektor definierst?
5. Teste: Füge eine neue `<h2>` hinzu. Wird sie automatisch gestylt?

## Weiterführende Links

- [MDN: `<style>` Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style)
- [MDN: CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Tricks: CSS Basics](https://css-tricks.com/guides/beginner/)
- [W3Schools: CSS Tutorial](https://www.w3schools.com/css/)
- [Can I Use](https://caniuse.com/) – Prüfe Browser-Support für CSS-Features

---

**⏱️ Geschätzte Zeit:** 30-35 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 lagern wir das CSS in eine externe Datei aus – die professionelle Lösung!
