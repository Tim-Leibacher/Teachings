# Auftrag 1: Erste Styles – Experimentiere mit Inline-CSS

## Ziel
Du lernst Inline-Styles kennen und verstehst, warum sie für grössere Projekte unpraktisch sind. Du experimentierst mit ersten CSS-Eigenschaften direkt im HTML-Code.

## Beschreibung

In diesem Auftrag nutzt du die einfachste (aber nicht beste) Methode, um CSS einzubinden: Inline-Styles. Du schreibst CSS direkt in deine HTML-Elemente mit dem `style`-Attribut.

---

### Teil 1: Erste Inline-Styles (15 Min)

**Öffne deine `index.html` und style deine Hauptüberschrift:**

```html
<header>
    <h1 style="color: #376B8C; font-size: 48px; text-align: center;">
        Dein Name
    </h1>
    <p style="color: #666; font-size: 18px; text-align: center;">
        Informatiker/in EFZ in Ausbildung
    </p>
</header>
```

**Experimentiere mit verschiedenen Eigenschaften:**

1. **Farben ändern:**
```html
<h2 style="color: #29786A;">Über mich</h2>
```

2. **Schriftgrössen anpassen:**
```html
<p style="font-size: 16px; line-height: 1.6;">Dein Text...</p>
```

3. **Text ausrichten:**
```html
<p style="text-align: center;">Zentrierter Text</p>
<p style="text-align: right;">Rechtsbündiger Text</p>
```

4. **Hintergrundfarbe setzen:**
```html
<section style="background-color: #F8F8F8; padding: 20px;">
    <h2>Meine Skills</h2>
    <!-- Dein Inhalt -->
</section>
```

---

### Teil 2: Experimentiere mit weiteren Properties (15 Min)

**Probiere folgende CSS-Eigenschaften aus:**

**Schrift-Eigenschaften:**
```html
<p style="font-family: Arial, sans-serif; font-weight: bold;">
    Fetter Text in Arial
</p>

<p style="font-style: italic; text-decoration: underline;">
    Kursiv und unterstrichen
</p>
```

**Abstände:**
```html
<div style="margin: 20px; padding: 15px; background-color: #E8F4F8;">
    Ein Bereich mit Abstand aussen (margin) und innen (padding)
</div>
```

**Ränder:**
```html
<p style="border: 2px solid #376B8C; padding: 10px;">
    Text mit blauem Rahmen
</p>
```

**Kombinationen:**
```html
<h2 style="color: #CD7A15; font-size: 28px; text-align: center; 
           border-bottom: 3px solid #FEAF51; padding-bottom: 10px;">
    Überschrift mit Unterstrich
</h2>
```

---

### Teil 3: Das Problem mit Inline-Styles (10 Min)

Jetzt stylst du mehrere Elemente gleich:

```html
<section>
    <article style="background-color: #F8F8F8; padding: 20px; 
                    margin-bottom: 20px; border-left: 4px solid #376B8C;">
        <h3 style="color: #376B8C; font-size: 22px;">Projekt 1</h3>
        <p style="color: #666; font-size: 16px; line-height: 1.6;">
            Beschreibung...
        </p>
    </article>
    
    <article style="background-color: #F8F8F8; padding: 20px; 
                    margin-bottom: 20px; border-left: 4px solid #376B8C;">
        <h3 style="color: #376B8C; font-size: 22px;">Projekt 2</h3>
        <p style="color: #666; font-size: 16px; line-height: 1.6;">
            Beschreibung...
        </p>
    </article>
</section>
```

**Fällt dir etwas auf?**
- Du kopierst dieselben Styles immer wieder
- Wenn du die Farbe ändern möchtest, musst du sie überall anpassen
- Der HTML-Code wird sehr unübersichtlich

---

## Erfolgskriterien

- [ ] Mindestens 5 verschiedene HTML-Elemente haben Inline-Styles
- [ ] Du hast mit mindestens 8 verschiedenen CSS-Eigenschaften experimentiert
- [ ] Farben, Schriftgrössen, Abstände und Rahmen sind vorhanden
- [ ] Du hast erkannt, dass Inline-Styles bei mehreren Elementen unpraktisch sind
- [ ] Die Seite wird im Browser korrekt dargestellt

## Tipps

- **Farben:** Nutze Hex-Codes (#376B8C), RGB (rgb(55, 107, 140)) oder Farbnamen (blue)
- **Schriftgrössen:** Nutze `px` (Pixel) für fixe Grössen oder `rem` für flexible Grössen
- **Browser DevTools:** Drücke F12 und gehe zu "Elements" → Ändere Styles live!
- **Profitipp:** Kopiere die Styles und ändere nur einzelne Werte zum Experimentieren
- Nutze die **Farbauswahl** in VS Code: Klick auf einen Farbcode und ein Color Picker öffnet sich!

## Reflexionsfragen

1. Was passiert, wenn du zwei verschiedene `color`-Werte im selben `style`-Attribut definierst?
2. Experimentiere: Ändere die Farbe deiner `<h1>` auf 5 verschiedene Werte. Welche gefällt dir am besten?
3. Was ist unpraktisch, wenn du 20 Absätze hast und alle dieselbe Schriftgrösse haben sollen?
4. Öffne DevTools (F12) → Elements → Ändere einen Inline-Style. Was passiert mit dem Original-Code?
5. Warum ist `style="color: blue; color: red;"` problematisch? Welche Farbe wird angezeigt?

## Weiterführende Links

- [MDN: Inline Styles](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/style)
- [MDN: CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [W3Schools: CSS Tutorial](https://www.w3schools.com/css/)
- [CSS Tricks: Getting Started with CSS](https://css-tricks.com/guides/beginner/)
- [Coolors.co](https://coolors.co/) – Farbpaletten-Generator
- [HTML Color Codes](https://htmlcolorcodes.com/) – Farben finden

---

**⏱️ Geschätzte Zeit:** 25-30 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lagern wir die Styles in den `<head>`-Bereich aus – viel übersichtlicher!
