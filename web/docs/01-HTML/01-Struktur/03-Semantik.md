# Auftrag 3: Professionelle Seitenstruktur – Header, Main & Footer

## Ziel
Du gliederst deine Portfolio-Seite in semantische Bereiche und bereitest sie für zukünftige Navigation und Inhalte vor.

## Beschreibung

Professionelle Webseiten haben eine klare Struktur. Du teilst deine Seite jetzt in drei Hauptbereiche:

### 1. **Header** (Kopfbereich)
Hier kommt später die Navigation. Für jetzt:
- Verschiebe deine `<h1>` mit deinem Namen in den `<header>`
- Füge einen Untertitel mit `<p>` hinzu (z.B. "Informatiker/in EFZ in Ausbildung")

### 2. **Main** (Hauptbereich)
Der Inhaltsbereich deiner Seite:
- Verschiebe deinen Begrüssungstext hierhin
- Füge eine `<h2>` hinzu: "Über mich"
- Schreibe 3-4 Sätze über deine Interessen, Hobbies oder Ziele

### 3. **Footer** (Fussbereich)
Der untere Bereich für Kontaktinfos:
- Füge eine `<h2>` hinzu: "Kontakt"
- Schreibe deine E-Mail-Adresse (Ausbildungs-Mail)
- Füge das aktuelle Jahr und "© Dein Name" hinzu

**Beispielstruktur:**
```html
<body>
    <header>
        <h1>Max Mustermann</h1>
        <p>Informatiker EFZ in Ausbildung</p>
    </header>

    <main>
        <h2>Über mich</h2>
        <p>Dein Begrüssungstext...</p>
        
        <p>Ich interessiere mich für Webentwicklung und...</p>
    </main>

    <footer>
        <h2>Kontakt</h2>
        <p>E-Mail: deine.email@firma.ch</p>
        <p>© 2025 Dein Name</p>
    </footer>
</body>
```

## Erfolgskriterien

- [ ] Die Seite ist in drei semantische Bereiche gegliedert: `<header>`, `<main>`, `<footer>`
- [ ] Der Header enthält deinen Namen als `<h1>` und einen Untertitel
- [ ] Im Main-Bereich steht ein "Über mich"-Text mit mindestens 3 Sätzen
- [ ] Der Footer enthält Kontaktinfo und Copyright
- [ ] Alle Überschriften folgen der logischen Hierarchie (h1 → h2)
- [ ] Die Seite validiert ohne Fehler (teste mit F12 → Console)

## Tipps

- **Warum semantisches HTML?** Browser, Screenreader und Suchmaschinen verstehen deine Struktur besser
- Nutze die Entwicklertools (F12) und schau dir den "Elements"-Tab an – du siehst die Struktur visuell
- **Profitrick:** In VS Code kannst du mit `Ctrl+Shift+P` → "Format Document" alles sauber einrücken
- Achte auf die Überschriften-Hierarchie: Nach `<h1>` kommt `<h2>`, nicht direkt `<h3>`

## Reflexionsfragen

1. Was ist der Unterschied zwischen `<div>` und `<header>`? Warum ist `<header>` besser?
2. Öffne die Entwicklertools (F12) und schaue dir die Seitenstruktur an. Erkennst du Header, Main und Footer?
3. Warum sollte es nur eine `<h1>` pro Seite geben?
4. Teste: Lade deine Seite im privaten/Inkognito-Modus. Funktioniert alles?

## Weiterführende Links

- [MDN: Semantisches HTML](https://developer.mozilla.org/de/docs/Glossary/Semantics#semantics_in_html)
- [W3Schools: HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)
- [HTML5 Doctor: Semantic Element Guide](http://html5doctor.com/element-index/)
- [W3C Validator](https://validator.w3.org/) – Prüfe deine Seite auf Fehler!

---

**⏱️ Geschätzte Zeit:** 25-30 Minuten  
**📦 Nächster Schritt:** Optional: Vertiefe dein Wissen über Barrierefreiheit und SEO!
