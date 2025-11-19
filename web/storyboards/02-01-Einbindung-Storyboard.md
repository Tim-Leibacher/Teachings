# Storyboard: CSS – Einbindung von CSS

## Video-Übersicht
- **Gesamtdauer:** ca. 6-7 Minuten
- **Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ
- **Lernziele:** Die drei Arten der CSS-Einbindung verstehen und anwenden können

---

## Szene 1: Einführung – Was ist CSS?

**Sprechertext:** „CSS steht für Cascading Style Sheets und ist die Sprache für das Design von Webseiten. Während HTML die Struktur vorgibt, bestimmt CSS das Aussehen – Farben, Schriften, Abstände und Layout."

**Bildschirmdarstellung:** 
- Zeige zwei Versionen derselben Portfolio-Seite nebeneinander
- Links: Nur HTML (unstyled)
- Rechts: Mit CSS gestylt (professionelles Design)

**Dauer:** 35 Sekunden

---

## Szene 2: Die drei Arten der CSS-Einbindung – Überblick

**Sprechertext:** „Es gibt drei Möglichkeiten, CSS in HTML einzubinden: Inline-Styles direkt im Element, Internal-Styles im Head-Bereich, und External-Styles in einer separaten CSS-Datei. Jede Methode hat ihre Vor- und Nachteile."

**Bildschirmdarstellung:** 
- Grafik mit drei Icons:
  1. Inline (im HTML-Tag)
  2. Internal (im `<head>`)
  3. External (externe .css-Datei)

**Dauer:** 30 Sekunden

---

## Szene 3: Inline-Styles – Direkt im Element

**Sprechertext:** „Die einfachste Methode sind Inline-Styles. Du schreibst das CSS direkt ins HTML-Element mit dem style-Attribut. Das funktioniert schnell für einzelne Änderungen, ist aber unpraktisch für ganze Webseiten."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```html
<h1 style="color: blue; font-size: 32px;">Willkommen</h1>
<p style="color: gray; font-size: 16px;">Dies ist ein Absatz.</p>
```
Browser-Vorschau: Blauer Titel und grauer Text

**Dauer:** 40 Sekunden

---

## Szene 4: Inline-Styles – Nachteile

**Sprechertext:** „Der Nachteil von Inline-Styles: Wenn du 10 Überschriften hast und die Farbe ändern möchtest, musst du jede einzeln anpassen. Das ist fehleranfällig und zeitaufwendig. Deshalb nutzt man Inline-Styles nur für Ausnahmen."

**Bildschirmdarstellung:** 
- Zeige HTML mit vielen wiederholten Inline-Styles
- Markiere die Redundanz visuell
- Zeige, wie mühsam es wäre, überall die Farbe zu ändern

**Dauer:** 35 Sekunden

---

## Szene 5: Internal-Styles – Im Head-Bereich

**Sprechertext:** „Die zweite Methode sind Internal-Styles. Du schreibst dein CSS im Head-Bereich der HTML-Datei in einem style-Tag. So kannst du alle Überschriften gleichzeitig formatieren – viel effizienter!"

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Portfolio</title>
    <style>
        h1 {
            color: blue;
            font-size: 32px;
        }
        p {
            color: gray;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h1>Willkommen</h1>
    <p>Dies ist ein Absatz.</p>
</body>
</html>
```
Browser-Vorschau: Dasselbe Ergebnis wie bei Inline

**Dauer:** 45 Sekunden

---

## Szene 6: Internal-Styles – Vorteile & Nachteile

**Sprechertext:** „Internal-Styles funktionieren gut für einzelne Seiten. Der Nachteil: Wenn du mehrere HTML-Seiten hast und überall dieselbe Formatierung möchtest, musst du den CSS-Code in jede Datei kopieren. Das ist nicht ideal."

**Bildschirmdarstellung:** 
- Zeige drei HTML-Dateien (index.html, about.html, contact.html)
- Zeige denselben `<style>`-Block in allen drei Dateien
- Markiere die Duplikation als Problem

**Dauer:** 30 Sekunden

---

## Szene 7: External-Styles – Die professionelle Lösung

**Sprechertext:** „Die beste Methode für grössere Projekte sind External-Styles. Du erstellst eine separate CSS-Datei und bindest sie mit dem link-Tag ein. So können alle deine HTML-Seiten dasselbe Stylesheet nutzen."

**Bildschirmdarstellung:** 
Dateistruktur zeigen:
```
mein-portfolio/
├── index.html
├── about.html
└── styles.css
```

Code-Editor zeigt **index.html**:
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Portfolio</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Willkommen</h1>
    <p>Dies ist ein Absatz.</p>
</body>
</html>
```

Code-Editor zeigt **styles.css**:
```css
h1 {
    color: blue;
    font-size: 32px;
}

p {
    color: gray;
    font-size: 16px;
}
```

Browser-Vorschau: Dasselbe Ergebnis

**Dauer:** 50 Sekunden

---

## Szene 8: External-Styles – Vorteile

**Sprechertext:** „Die Vorteile von External-Styles: Ein zentrales Stylesheet für alle Seiten, leichte Wartung, und der Browser kann das CSS zwischenspeichern – das macht deine Webseite schneller. Deshalb nutzen Profis fast immer externe CSS-Dateien."

**Bildschirmdarstellung:** 
- Zeige mehrere HTML-Dateien, die alle auf styles.css verlinken
- Zeige Änderung in styles.css → alle Seiten aktualisieren sich
- Zeige Browser-Cache-Symbol

**Dauer:** 35 Sekunden

---

## Szene 9: Vergleich & Best Practices

**Sprechertext:** „Zusammengefasst: Nutze Inline-Styles nur für Ausnahmen, Internal-Styles für kleine Ein-Seiten-Projekte, und External-Styles für alle professionellen Webseiten. Die meiste Zeit wirst du mit externen Stylesheets arbeiten."

**Bildschirmdarstellung:** 
Vergleichstabelle:

| Methode | Verwendung | Vorteil | Nachteil |
|---------|-----------|---------|----------|
| Inline | Ausnahmen | Schnell | Unübersichtlich |
| Internal | Kleine Projekte | Zentral in einer Datei | Nicht wiederverwendbar |
| External | Professionelle Seiten | Wiederverwendbar | Zusätzliche Datei |

**Dauer:** 40 Sekunden

---

## Szene 10: Praxis-Tipp & Zusammenfassung

**Sprechertext:** „Praxis-Tipp: Beginne mit einer gut organisierten CSS-Datei. Erstelle Kommentare für verschiedene Bereiche wie Navigation, Header, Main-Content. So behältst du auch bei grösseren Projekten den Überblick. Viel Erfolg!"

**Bildschirmdarstellung:** 
Zeige gut strukturierte **styles.css** mit Kommentaren:
```css
/* ==================
   NAVIGATION
   ================== */
nav { ... }

/* ==================
   HEADER
   ================== */
header { ... }

/* ==================
   MAIN CONTENT
   ================== */
main { ... }
```

**Dauer:** 30 Sekunden

---

## Benötigte Ressourcen für Video-Produktion

### Code-Beispiele
1. **inline-example.html** – Portfolio mit Inline-Styles
2. **internal-example.html** – Portfolio mit Internal-Styles
3. **external-example.html** + **styles.css** – Portfolio mit External-Styles

### Grafiken / Animationen
- Icons für die drei CSS-Einbindungsarten
- Vergleichstabelle (Inline vs. Internal vs. External)
- Dateistruktur-Diagramm

### Browser-Demonstrationen
- Dieselbe Seite ohne CSS und mit CSS
- Änderung in external CSS → alle Seiten aktualisieren sich
- DevTools (F12) → Styles-Tab zeigen

---

## Lernziele (nach Video)

Nach diesem Video können Lernende:
- Die drei Arten der CSS-Einbindung benennen und erklären
- Inline-Styles mit dem `style`-Attribut schreiben
- Internal-Styles im `<head>` mit `<style>` erstellen
- Eine externe CSS-Datei erstellen und mit `<link>` einbinden
- Die Vor- und Nachteile jeder Methode verstehen
- Entscheiden, welche Methode für ihr Projekt am besten ist

---

**Gesamtdauer:** ca. 6-7 Minuten  
**Schnitt-Hinweise:** Zwischen Code-Editor und Browser-Vorschau wechseln für besseres Verständnis. Bei External-Styles den Dateiwechsel visuell hervorheben (z.B. mit Zoom oder Highlight).
