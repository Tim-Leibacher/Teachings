# Auftrag 3: Projekt-Galerie – Zeige deine (zukünftigen) Projekte

## 🎯 Ziel
Du erstellst eine Projekt-Sektion in deinem Portfolio, die zukünftige Projekte aufnehmen kann. Mit Bildern, Beschreibungen und Links entsteht eine professionelle Präsentation.

## 📋 Beschreibung

Jedes Portfolio braucht eine Projekt-Sektion! Auch wenn du noch nicht viele Projekte hast, erstellst du jetzt die Struktur dafür. Du kannst Platzhalter-Projekte oder erste kleine Arbeiten zeigen.

---

### Teil 1: Projekt-Sektion erstellen (15 Min)

**Füge eine neue Sektion nach deinen Skills ein:**

```html
<section id="projekte">
    <h2>Meine Projekte</h2>
    <p>Hier zeige ich ausgewählte Projekte aus meiner Ausbildung.</p>
    
    <!-- Hier kommen die Projekt-Karten -->
</section>
```

**Aktualisiere die Navigation:**
```html
<nav>
    <ul>
        <li><a href="#ueber-mich">Über mich</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projekte">Projekte</a></li>
        <li><a href="#lernziele">Lernziele</a></li>
        <li><a href="#kontakt">Kontakt</a></li>
    </ul>
</nav>
```

---

### Teil 2: Projekt-Karten erstellen (25 Min)

Erstelle mindestens **3 Projekt-Karten** mit je:
- Vorschaubild
- Projekttitel
- Kurzbeschreibung (2-3 Sätze)
- Link zum Projekt oder GitHub

**Struktur einer Projekt-Karte:**

```html
<article class="projekt-karte">
    <figure>
        <img src="images/projekt1.jpg" 
             alt="Screenshot des Portfolio-Projekts" 
             width="400" 
             height="300">
        <figcaption>Portfolio-Website</figcaption>
    </figure>
    
    <h3>
        <a href="projekt1.html">Portfolio-Website</a>
    </h3>
    
    <p><strong>Technologien:</strong> HTML, CSS</p>
    
    <p>Meine erste eigene Website, erstellt im Rahmen der Ausbildung. 
    Ziel war es, die Grundlagen von HTML zu verstehen und eine 
    persönliche Online-Präsenz aufzubauen.</p>
    
    <p>
        <a href="projekt1.html">Projekt ansehen →</a> | 
        <a href="https://github.com/username/projekt1" 
           target="_blank" 
           rel="noopener noreferrer">
            Code auf GitHub →
        </a>
    </p>
</article>
```

**Erstelle 3 Projekt-Karten:**

1. **Projekt 1: Dieses Portfolio**
   - Beschreibe dein aktuelles Portfolio-Projekt
   - Screenshot der Seite als Bild
   - Technologien: HTML (später CSS, JavaScript)

2. **Projekt 2: Erste HTML-Seite (Platzhalter)**
   - Deine allererste HTML-Übung
   - Beschreibe, was du gelernt hast
   - Screenshot oder Platzhalter-Bild

3. **Projekt 3: Zukünftiges Projekt**
   - Ein Projekt, das du in Zukunft umsetzen möchtest
   - Nutze ein Platzhalter-Bild
   - Beschreibe deine Idee

**Beispiel für ein zukünftiges Projekt:**

```html
<article class="projekt-karte">
    <figure>
        <img src="images/projekt-placeholder.jpg" 
             alt="Platzhalter für zukünftiges To-Do-App Projekt" 
             width="400" 
             height="300">
        <figcaption>To-Do App (in Planung)</figcaption>
    </figure>
    
    <h3>To-Do App mit JavaScript</h3>
    
    <p><strong>Geplante Technologien:</strong> HTML, CSS, JavaScript</p>
    
    <p>Eine interaktive To-Do-Liste, bei der Aufgaben hinzugefügt, 
    bearbeitet und gelöscht werden können. Ziel ist es, JavaScript 
    und DOM-Manipulation zu lernen.</p>
    
    <p><em>Projekt in Planung – folgt bald!</em></p>
</article>
```

---

### Teil 3: Projekt-Detailseiten erstellen (Optional, 10 Min)

Erstelle für dein Hauptprojekt (dieses Portfolio) eine eigene Seite:

**Datei: `projekt-portfolio.html`**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio-Website – Mein erstes Projekt</title>
</head>
<body>
    <header>
        <h1>Projekt: Portfolio-Website</h1>
        <p><a href="index.html">← Zurück zum Portfolio</a></p>
    </header>
    
    <main>
        <figure>
            <img src="images/portfolio-screenshot.jpg" 
                 alt="Screenshot der kompletten Portfolio-Website">
            <figcaption>Die fertige Portfolio-Seite</figcaption>
        </figure>
        
        <section>
            <h2>Über das Projekt</h2>
            <p><strong>Zeitraum:</strong> Oktober 2025</p>
            <p><strong>Technologien:</strong> HTML5, semantisches Markup</p>
            
            <h3>Projektbeschreibung</h3>
            <p>Mein erstes grösseres Projekt im Rahmen der Ausbildung. 
            Ziel war es, eine persönliche Portfolio-Website zu erstellen, 
            die meine Fähigkeiten und Projekte präsentiert.</p>
            
            <h3>Was ich gelernt habe</h3>
            <ul>
                <li>Semantisches HTML und korrekte Dokumentstruktur</li>
                <li>Verwendung von Listen, Links und Bildern</li>
                <li>Accessibility und Alt-Texte</li>
                <li>Projektstruktur und Dateiverwaltung</li>
            </ul>
            
            <h3>Herausforderungen</h3>
            <p>Die grösste Herausforderung war, die Inhalte logisch zu 
            strukturieren und dabei auf semantisch korrektes HTML zu achten.</p>
        </section>
        
        <section>
            <h2>Links</h2>
            <p>
                <a href="index.html">Live-Version ansehen →</a><br>
                <a href="https://github.com/username/portfolio" 
                   target="_blank" 
                   rel="noopener noreferrer">
                    Code auf GitHub →
                </a>
            </p>
        </section>
    </main>
    
    <footer>
        <p><a href="index.html">← Zurück zum Portfolio</a></p>
    </footer>
</body>
</html>
```

**Verlinke auf der Hauptseite dazu:**
```html
<h3>
    <a href="projekt-portfolio.html">Portfolio-Website</a>
</h3>
```

---

## ✅ Erfolgskriterien

- [ ] Eine "Meine Projekte"-Sektion mit `<h2>` existiert
- [ ] Mindestens 3 Projekt-Karten sind vorhanden
- [ ] Jede Projekt-Karte enthält: Bild, Titel, Beschreibung, Link
- [ ] Alle Bilder haben aussagekräftige Alt-Texte
- [ ] Mindestens ein Projekt nutzt `<figure>` und `<figcaption>`
- [ ] Die Navigation wurde um "Projekte" ergänzt
- [ ] Alle Links funktionieren (auch wenn auf leere Seiten verwiesen wird)
- [ ] Optional: Eine Projekt-Detailseite existiert

## 💡 Tipps

- **Nutze `<article>` für Projekt-Karten** – semantisch korrekt!
- Halte Projektbeschreibungen kurz und prägnant (max. 3 Sätze)
- **Profitipp:** Erstelle einen `projekte/` Ordner für alle Projekt-Detailseiten
- Screenshots erstellen: `F12` → DevTools → `Ctrl + Shift + P` → "Capture full size screenshot"
- Platzhalter-Bilder: [Lorem Picsum](https://picsum.photos/) für automatische Bilder

## 🤔 Reflexionsfragen

1. Warum ist `<article>` für Projekt-Karten besser als nur `<div>`?
2. Teste: Wie wirkt deine Projekt-Galerie auf einem Smartphone? (Browser verkleinern)
3. Was macht ein gutes Vorschaubild aus? Welche Informationen sollte es zeigen?
4. Überlege: Welche Projekte wirst du in Zukunft hier zeigen?
5. Inspiziere Portfolio-Seiten von anderen (z.B. auf Dribbble) – wie sind Projekte dort präsentiert?

## 🔗 Weiterführende Links

- [MDN: `<article>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/article)
- [MDN: `<figure>` & `<figcaption>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/figure)
- [Portfolio-Inspiration: Awwwards](https://www.awwwards.com/websites/portfolio/)
- [GitHub Pages: Kostenlos hosten](https://pages.github.com/)

**Inspiration:**
- [Dribbble: Portfolio Designs](https://dribbble.com/search/portfolio)
- [Behance: Web Design Portfolios](https://www.behance.net/search/projects?search=portfolio)

---

**⏱️ Geschätzte Zeit:** 25-30 Minuten  
**📦 Nächster Schritt:** Optional: Vertiefe dein Wissen über Bildoptimierung und Performance!
