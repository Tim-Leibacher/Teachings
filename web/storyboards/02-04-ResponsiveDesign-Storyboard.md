# Storyboard: CSS – Responsive Design

## Video-Übersicht
- **Gesamtdauer:** ca. 6-7 Minuten
- **Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ
- **Lernziele:** Media Queries verstehen und responsive Websites erstellen können

---

## Szene 1: Einführung – Warum Responsive Design?

**Sprechertext:** "Stell dir vor, jemand öffnet dein Portfolio auf dem Smartphone – aber die Schrift ist winzig, die Navigation funktioniert nicht, und man muss ständig zoomen. Frustrierend! Genau deshalb gibt es Responsive Design. Deine Website passt sich automatisch an die Bildschirmgrösse an – egal ob Smartphone, Tablet oder Desktop."

**Bildschirmdarstellung:** 
- Zeige dieselbe Portfolio-Website auf drei Geräten nebeneinander:
  - Smartphone (320px breit)
  - Tablet (768px breit)
  - Desktop (1200px breit)
- Alle drei Versionen sehen optimal aus, aber unterschiedlich layoutet

**Dauer:** 35 Sekunden

---

## Szene 2: Das Problem ohne Responsive Design

**Sprechertext:** "Ohne Responsive Design sieht deine Website auf dem Handy chaotisch aus. Texte sind zu klein, Elemente überlappen sich, und die Navigation ist kaum bedienbar. Das führt dazu, dass Besucher die Seite sofort wieder verlassen."

**Bildschirmdarstellung:** 
- Zeige eine Desktop-Website auf einem Smartphone-Bildschirm
- Markiere Probleme visuell:
  - Text zu klein zum Lesen (roter Kreis)
  - Navigation zu klein zum Klicken (roter Kreis)
  - Inhalte laufen über den Bildschirm hinaus (roter Pfeil)
- Zeige frustrierten Nutzer, der versucht zu zoomen

**Dauer:** 30 Sekunden

---

## Szene 3: Der Viewport Meta-Tag – Die Grundlage

**Sprechertext:** "Der erste Schritt zu Responsive Design ist der Viewport Meta-Tag im Head-Bereich. Dieser Tag sagt dem Browser: 'Nutze die echte Gerätebreite und zoome nicht automatisch.' Ohne diesen Tag funktionieren Media Queries nicht richtig."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" 
          content="width=device-width, initial-scale=1.0">
    <title>Portfolio</title>
</head>
```

Split-Screen:
- Links: Ohne Viewport-Tag (alles zu klein)
- Rechts: Mit Viewport-Tag (optimale Grösse)

**Dauer:** 35 Sekunden

---

## Szene 4: Media Queries – CSS für unterschiedliche Bildschirme

**Sprechertext:** "Mit Media Queries kannst du CSS-Regeln definieren, die nur bei bestimmten Bildschirmgrössen gelten. Diese Query hier bedeutet: 'Ab einer Mindestbreite von 768 Pixeln – also ab Tablet-Grösse – nutze diese Styles.' So kannst du das Layout für jedes Gerät optimieren."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
/* Standard: Mobile (unter 768px) */
.container {
    padding: 10px;
    font-size: 16px;
}

/* Ab Tablet (768px und breiter) */
@media (min-width: 768px) {
    .container {
        padding: 20px;
        font-size: 18px;
    }
}

/* Ab Desktop (1024px und breiter) */
@media (min-width: 1024px) {
    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 40px;
    }
}
```

Browser-Vorschau:
- Zeige Bildschirm, der von schmal nach breit animiert wird
- CSS-Eigenschaften ändern sich bei den Breakpoints
- Markiere die Breakpoints (768px, 1024px) visuell

**Dauer:** 40 Sekunden

---

## Szene 5: Mobile-First Ansatz – Von klein nach gross

**Sprechertext:** "Profis nutzen den Mobile-First Ansatz: Du schreibst zuerst CSS für Smartphones und erweiterst dann mit Media Queries für grössere Bildschirme. Das hat einen einfachen Grund: Mobile Geräte haben weniger Leistung, und es ist effizienter, nur das zu laden, was wirklich gebraucht wird."

**Bildschirmdarstellung:** 
Code-Beispiel mit Kommentaren:
```css
/* Mobile First: Basis-Styles (keine Media Query) */
.navigation {
    display: flex;
    flex-direction: column; /* Vertikales Menü */
}

/* Ab Tablet: Horizontales Menü */
@media (min-width: 768px) {
    .navigation {
        flex-direction: row; /* Horizontales Menü */
    }
}
```

Grafik:
- Smartphone → Tablet → Desktop (Pfeil von links nach rechts)
- Text: "CSS wird schrittweise erweitert, nicht reduziert"

**Dauer:** 35 Sekunden

---

## Szene 6: Typische Breakpoints – Mobile, Tablet, Desktop

**Sprechertext:** "Es gibt drei Standard-Breakpoints, die sich an realen Geräten orientieren: 768 Pixel für Tablets, 1024 Pixel für kleine Desktops, und 1200 Pixel für grosse Bildschirme. Diese Werte sind in der Webentwicklung Standard und decken die meisten Geräte ab."

**Bildschirmdarstellung:** 
Grafik mit drei Bereichen:
```
📱 Mobile: 0 - 767px
   → Einspaltig, grosse Touch-Targets

📱 Tablet: 768px - 1023px
   → Zweispaltig möglich, kompaktere Navigation

🖥️ Desktop: 1024px+
   → Mehrspaltig, komplexe Layouts
```

Zeige Portfolio-Screenshot in allen drei Ansichten

**Dauer:** 30 Sekunden

---

## Szene 7: Praktisches Beispiel – Responsive Navigation

**Sprechertext:** "Schauen wir uns ein konkretes Beispiel an: Auf dem Smartphone ist die Navigation vertikal und nimmt die volle Breite ein – perfekt zum Tippen. Ab Tablet-Grösse wird sie horizontal und kompakter. So nutzt du den Platz optimal."

**Bildschirmdarstellung:** 
Code-Editor zeigt komplettes Beispiel:
```css
/* Mobile: Vertikale Navigation */
nav {
    background: #376B8C;
}

nav ul {
    display: flex;
    flex-direction: column;
    gap: 0;
}

nav li {
    width: 100%;
}

nav a {
    display: block;
    padding: 15px;
    color: white;
    border-bottom: 1px solid rgba(255,255,255,0.2);
}

/* Ab Tablet: Horizontale Navigation */
@media (min-width: 768px) {
    nav ul {
        flex-direction: row;
        justify-content: center;
        gap: 20px;
    }
    
    nav li {
        width: auto;
    }
    
    nav a {
        border-bottom: none;
        padding: 15px 25px;
    }
}
```

Browser-Demo:
- Zeige Navigation in Aktion
- Ändere Browsergrösse live
- Navigation wechselt von vertikal zu horizontal

**Dauer:** 40 Sekeconds

---

## Szene 8: Grid-Layout – Von 1 zu 3 Spalten

**Sprechertext:** "Ein weiteres typisches Beispiel: Projekt-Karten. Auf dem Smartphone werden sie untereinander angezeigt, auf dem Tablet zweispaltig, und auf dem Desktop dreispaltig. CSS Grid macht das super einfach."

**Bildschirmdarstellung:** 
Code-Editor zeigt:
```css
/* Mobile: Eine Spalte */
.projekte-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
}

/* Tablet: Zwei Spalten */
@media (min-width: 768px) {
    .projekte-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 30px;
    }
}

/* Desktop: Drei Spalten */
@media (min-width: 1024px) {
    .projekte-grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 40px;
    }
}
```

Visuelle Demonstration:
- Zeige Projekt-Karten, die sich neu anordnen
- 1 Spalte → 2 Spalten → 3 Spalten
- Animiere den Übergang

**Dauer:** 35 Sekunden

---

## Szene 9: Responsive Schriftgrössen & Abstände

**Sprechertext:** "Nicht nur das Layout sollte sich anpassen, sondern auch Schriftgrössen und Abstände. Auf dem Smartphone sind kleinere Schriften und engere Abstände sinnvoll, auf grossen Bildschirmen darf alles etwas grosszügiger sein."

**Bildschirmdarstellung:** 
Code-Beispiel:
```css
/* Mobile */
body {
    font-size: 16px;
    line-height: 1.5;
}

h1 {
    font-size: 28px;
}

section {
    padding: 20px 10px;
}

/* Tablet */
@media (min-width: 768px) {
    body {
        font-size: 18px;
        line-height: 1.6;
    }
    
    h1 {
        font-size: 36px;
    }
    
    section {
        padding: 40px 30px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    h1 {
        font-size: 48px;
    }
    
    section {
        padding: 60px 40px;
    }
}
```

Side-by-Side Vergleich:
- Links: Mobile (engere Abstände)
- Rechts: Desktop (grosszügige Abstände)

**Dauer:** 35 Sekunden

---

## Szene 10: Browser Developer Tools – Responsive testen

**Sprechertext:** "Du musst nicht ständig dein Handy rausholen, um die mobile Ansicht zu testen. Die Browser Developer Tools haben einen Responsive-Modus. Drücke F12, klicke auf das Handy-Symbol, und du kannst verschiedene Geräte simulieren."

**Bildschirmdarstellung:** 
Live-Demo in Chrome DevTools:
1. Öffne Portfolio-Website
2. Drücke F12 (Developer Tools öffnen sich)
3. Klicke auf Toggle Device Toolbar (Handy-Symbol)
4. Zeige Dropdown mit Geräteauswahl:
   - iPhone 14 Pro
   - iPad Air
   - Desktop (1920x1080)
5. Wechsle zwischen den Geräten
6. Zeige, wie sich das Layout anpasst

Tipp einblenden: "Shortcut: Ctrl+Shift+M (Windows) oder Cmd+Shift+M (Mac)"

**Dauer:** 40 Sekunden

---

## Szene 11: Zusammenfassung – Die wichtigsten Punkte

**Sprechertext:** "Fassen wir zusammen: Responsive Design bedeutet, dass deine Website auf allen Geräten funktioniert. Der Viewport Meta-Tag ist die Grundlage. Mit Media Queries passt du CSS an verschiedene Bildschirmgrössen an. Mobile-First bedeutet, von klein nach gross zu denken. Und die Browser Developer Tools helfen dir beim Testen. Jetzt bist du bereit, dein Portfolio responsive zu machen!"

**Bildschirmdarstellung:** 
Checkliste einblenden:
```
✓ Viewport Meta-Tag im <head>
✓ Mobile-First CSS schreiben
✓ Media Queries für Breakpoints:
  - Tablet: 768px
  - Desktop: 1024px
✓ Navigation, Grid & Text anpassen
✓ Mit DevTools testen
```

Zeige finales Portfolio auf allen drei Geräten gleichzeitig

**Dauer:** 35 Sekunden

---

## Benötigte Ressourcen für die Video-Produktion

### Dateien & Code-Beispiele
- **Portfolio-Projekt** mit HTML/CSS aus vorherigen Kapiteln
- **styles.css** mit Basis-Styles
- **Chrome Browser** mit DevTools
- **Code-Editor** (VS Code empfohlen)

### Visuelle Elemente
- **Gerät-Mockups:** Smartphone, Tablet, Desktop (z.B. von Figma oder Sketch)
- **Icons:** 📱 Smartphone, 🖥️ Desktop, 📏 Breakpoint-Lineal
- **Grafiken:** Breakpoint-Übersicht mit Pixel-Werten

### Screen Recordings
- Live-Coding in VS Code
- Browser mit wechselnder Fenstergrösse
- Chrome DevTools Responsive Mode
- Portfolio-Seite in drei Ansichten gleichzeitig

### Text-Overlays
- Breakpoint-Werte (768px, 1024px)
- Keyboard-Shortcuts (F12, Ctrl+Shift+M)
- Checklisten-Punkte
- Code-Kommentare hervorheben

---

## Technische Setup-Anleitung

### Vor dem Dreh vorbereiten:
1. **Portfolio-Projekt** komplett fertig haben (HTML aus vorherigen Kapiteln)
2. **Zwei Browser-Fenster:** Eines mit Code-Editor, eines mit Live-Preview
3. **Screen-Recording-Software** einstellen (z.B. OBS Studio)
4. **Zoom-Level** im Browser auf 100% setzen
5. **Browser-Lesezeichen** ausblenden für saubere Aufnahme

### CSS-Datei für Demo vorbereiten:
Erstelle eine `responsive-demo.css` mit allen Code-Beispielen aus dem Storyboard, damit du sie während der Aufnahme nur noch einblenden musst.

### DevTools optimal nutzen:
- Device Toolbar aktivieren
- Bekannte Geräte vorselektieren (iPhone 14 Pro, iPad Air)
- Zeige Pixel-Werte beim Resize (im DevTools sichtbar)

---

## Post-Production Hinweise

### Schnitt-Punkte:
- Übergänge zwischen Szenen mit kurzem Fade (0.5s)
- Code-Beispiele mindestens 3 Sekunden auf dem Bildschirm lassen
- Bei Live-Coding: Tippfehler rausschneiden

### Text-Einblendungen:
- Wichtige Begriffe als Text-Overlay einblenden:
  - "Media Query"
  - "Breakpoint: 768px"
  - "Mobile-First"
- Immer in der unteren Bildschirmhälfte, um Code nicht zu verdecken

### Musik & Sound:
- Dezente Hintergrundmusik (nicht ablenkend)
- Beim Live-Coding: Leichter Tastatur-Sound
- Bei Übergängen: Subtiler Sound-Effekt

---

## Timing-Übersicht (Gesamtdauer: 6 Minuten 30 Sekunden)

| Szene | Inhalt | Dauer |
|-------|--------|-------|
| 1 | Einführung – Warum Responsive? | 0:35 |
| 2 | Problem ohne Responsive Design | 0:30 |
| 3 | Viewport Meta-Tag | 0:35 |
| 4 | Media Queries erklärt | 0:40 |
| 5 | Mobile-First Ansatz | 0:35 |
| 6 | Typische Breakpoints | 0:30 |
| 7 | Responsive Navigation | 0:40 |
| 8 | Grid-Layout (1-3 Spalten) | 0:35 |
| 9 | Responsive Schriftgrössen | 0:35 |
| 10 | Browser DevTools | 0:40 |
| 11 | Zusammenfassung | 0:35 |
| **Total** | | **6:30** |
