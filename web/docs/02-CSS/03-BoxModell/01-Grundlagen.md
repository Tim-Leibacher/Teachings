# Auftrag 1: Box-Modell Grundlagen – Abstände verstehen und anwenden

## Ziel
Du verstehst die vier Bereiche des Box-Modells (Content, Padding, Border, Margin) und kannst Abstände präzise kontrollieren. Du lernst, wie Padding und Margin dein Layout beeinflussen.

## Beschreibung

Jedes HTML-Element ist eine rechteckige Box mit vier Bereichen: dem Inhalt (Content), Innenabstand (Padding), Rahmen (Border) und Aussenabstand (Margin). In diesem Auftrag experimentierst du mit diesen Bereichen und lernst, sie gezielt einzusetzen.

---

### Teil 1: Padding – Innenabstand (15 Min)

Padding ist der Abstand zwischen dem Inhalt und dem Rand eines Elements. Er vergrössert das Element und übernimmt die Hintergrundfarbe.

**Öffne deine `styles.css` und experimentiere:**

**1. Padding für alle Seiten gleichzeitig:**
```css
/* Füge zu deiner Header-Sektion hinzu */
header {
    background-color: var(--color-primary);
    color: white;
    padding: 60px 20px; /* Oben-Unten: 60px, Links-Rechts: 20px */
    text-align: center;
}
```

**2. Padding für einzelne Seiten:**
```css
.card {
    background-color: #F8F8F8;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    
    /* Verschiedene Paddings für jede Seite */
    padding-top: 20px;
    padding-right: 30px;
    padding-bottom: 20px;
    padding-left: 30px;
}
```

**3. Kurzschreibweisen verstehen:**
```css
/* Ein Wert = alle Seiten gleich */
padding: 20px;

/* Zwei Werte = Oben-Unten, Links-Rechts */
padding: 20px 40px;

/* Drei Werte = Oben, Links-Rechts, Unten */
padding: 10px 20px 30px;

/* Vier Werte = Oben, Rechts, Unten, Links (Uhrzeigersinn) */
padding: 10px 20px 30px 40px;
```

**Experimentiere mit deinen Projekt-Karten:**
```css
article {
    background-color: #F8F8F8;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    padding: 30px; /* Mehr Platz um den Inhalt */
    margin-bottom: 30px;
}

article h3 {
    margin-top: 0; /* Entfernt Standard-Margin oben */
    padding-bottom: 10px; /* Abstand nach unten */
}
```

---

### Teil 2: Margin – Aussenabstand (15 Min)

Margin schafft Abstand zwischen Elementen. Im Gegensatz zu Padding ist Margin transparent und übernimmt keine Hintergrundfarbe.

**1. Margin für Abstände zwischen Elementen:**
```css
section {
    margin-bottom: 60px; /* Abstand zwischen Sektionen */
}

h2 {
    margin-top: 40px;
    margin-bottom: 20px;
}

p {
    margin-bottom: 16px; /* Abstand zwischen Absätzen */
}
```

**2. Zentrieren mit Margin:**
```css
main {
    max-width: 900px;
    margin: 0 auto; /* Zentriert horizontal */
    padding: 40px 20px;
}
```

**Wie funktioniert `margin: 0 auto`?**
- `0` = Kein Margin oben und unten
- `auto` = Browser verteilt den verfügbaren Platz gleichmässig links und rechts
- **Wichtig:** Funktioniert nur bei Elementen mit fester `width` oder `max-width`!

**3. Negative Margins (Advanced):**
```css
/* Bringt Elemente näher zusammen oder überlappend */
.featured-card {
    margin-top: -20px; /* Hebt das Element 20px nach oben */
}
```

---

### Teil 3: Border – Rahmen (10 Min)

Border ist der Rahmen zwischen Padding und Margin. Er hat eine Farbe, Breite und einen Stil.

**1. Einfache Borders:**
```css
h2 {
    border-bottom: 3px solid #45BA98; /* Unterstrich */
    padding-bottom: 10px;
}

.card {
    border: 1px solid #D0D0D0; /* Rundherum */
    border-radius: 8px; /* Abgerundete Ecken */
}
```

**2. Border für einzelne Seiten:**
```css
ul li {
    border-left: 4px solid var(--color-primary);
    padding-left: 20px;
    margin-bottom: 10px;
}
```

**3. Border-Stile:**
```css
/* Verschiedene Stile ausprobieren */
.border-solid {
    border: 2px solid black;
}

.border-dashed {
    border: 2px dashed gray;
}

.border-dotted {
    border: 2px dotted blue;
}

.border-double {
    border: 4px double red;
}
```

---

### Teil 4: Box-Modell mit DevTools verstehen (10 Min)

**1. Öffne deine Portfolio-Seite im Browser**

**2. Drücke `F12` → Elements-Tab**

**3. Klicke auf ein Element (z.B. eine Projekt-Karte)**

**4. Scrolle im Styles-Panel nach unten → Du siehst das Box-Modell visualisiert:**

```
┌──── Margin (orange) ────┐
│ ┌──── Border (gelb) ────┐ │
│ │ ┌──── Padding (grün) ─┐ │ │
│ │ │ ┌── Content (blau) ─┐ │ │ │
│ │ │ │  300 x 200       │ │ │ │
│ │ │ └──────────────────┘ │ │ │
│ │ └────────────────────────┘ │ │
│ └────────────────────────────┘ │
└────────────────────────────────┘
```

**5. Experimentiere:**
- Klicke auf die Zahlen im Box-Modell → Ändere sie
- Sieh dir die Änderungen live auf der Seite an
- Hover über Elemente im HTML → Box-Modell wird auf der Seite hervorgehoben

---

### Teil 5: Praktische Anwendung (10 Min)

**Style deine Portfolio-Bereiche mit dem Box-Modell:**

```css
/* ==================
   HEADER
   ================== */
header {
    background-color: var(--color-primary);
    color: white;
    padding: 60px 20px;
    text-align: center;
    margin-bottom: 0; /* Kein Abstand nach unten */
}

/* ==================
   NAVIGATION
   ================== */
nav {
    background-color: var(--color-primary-light);
    padding: 15px 0;
    margin-bottom: 40px;
}

nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

nav ul li {
    display: inline-block;
    margin: 0 15px; /* Abstand zwischen Links */
}

/* ==================
   MAIN CONTENT
   ================== */
main {
    max-width: 900px;
    margin: 0 auto; /* Zentriert */
    padding: 40px 20px;
}

section {
    margin-bottom: 60px; /* Abstand zwischen Sektionen */
}

/* ==================
   LISTS
   ================== */
ul li {
    background-color: #F8F8F8;
    padding: 12px 20px; /* Innenabstand */
    margin-bottom: 10px; /* Abstand zwischen Items */
    border-left: 4px solid var(--color-primary);
}

/* ==================
   CARDS
   ================== */
article {
    background-color: white;
    border: 1px solid #D0D0D0;
    border-radius: 8px;
    padding: 30px; /* Viel Platz innen */
    margin-bottom: 30px; /* Abstand zu nächster Card */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* ==================
   FOOTER
   ================== */
footer {
    background-color: var(--color-primary-dark);
    color: white;
    text-align: center;
    padding: 30px 20px;
    margin-top: 60px;
}
```

---

## Erfolgskriterien

- [ ] Mindestens 5 Elemente nutzen Padding
- [ ] Mindestens 5 Elemente nutzen Margin
- [ ] Mindestens 3 Elemente haben einen Border
- [ ] Der Main-Bereich ist mit `margin: 0 auto` zentriert
- [ ] Abstände zwischen Sektionen sind konsistent (z.B. immer 60px)
- [ ] Du hast das Box-Modell mit DevTools inspiziert
- [ ] Alle Kurzschreibweisen (1, 2, 3 oder 4 Werte) wurden ausprobiert
- [ ] Die Seite sieht professioneller und luftiger aus

## Tipps

- **Eselsbrücke für 4 Werte:** "TRouBLe" → **T**op **R**ight **B**ottom **L**eft (Uhrzeigersinn)
- **Padding übernimmt Hintergrundfarbe**, Margin nicht – das ist der wichtigste Unterschied!
- `margin: 0 auto` zentriert nur horizontal, nicht vertikal
- **Profitipp:** Nutze konsistente Abstände (z.B. immer Vielfache von 4px: 8px, 12px, 16px, 20px, 24px, usw.)
- Negative Margins sind mächtig, aber nutze sie sparsam
- **DevTools-Trick:** Klicke auf ein Element und drücke die Pfeiltasten → Ändert Margin/Padding in 1px-Schritten

## Selbsttest

Überprüfe dein Verständnis:

- **Padding vs. Margin unterscheiden:** Ich weiss, dass Padding die Hintergrundfarbe übernimmt und Margin transparent ist
- **Kurzschreibweisen anwenden:** Ich kann `margin: 0 auto` erklären und weiss, wie ich damit Elemente zentriere
- **Box-Modell debuggen:** Ich kann in DevTools (F12) das Box-Modell inspizieren und erkenne, welcher Bereich orange, grün, gelb und blau dargestellt wird
- **Konsistente Abstände schaffen:** Ich verstehe, warum es sinnvoll ist, Abstände in Vielfachen von 4 oder 8 Pixeln zu definieren

## Weiterführende Links

- [MDN: Box-Modell](https://developer.mozilla.org/de/docs/Learn/CSS/Building_blocks/The_box_model)
- [MDN: Padding](https://developer.mozilla.org/de/docs/Web/CSS/padding)
- [MDN: Margin](https://developer.mozilla.org/de/docs/Web/CSS/margin)
- [MDN: Border](https://developer.mozilla.org/de/docs/Web/CSS/border)
- [CSS Tricks: The Box Model](https://css-tricks.com/the-css-box-model/)
- [W3Schools: Box Model](https://www.w3schools.com/css/css_boxmodel.asp)
- [Interactive Box Model Demo](https://www.cssboxmodel.com/)

---

**⏱️ Geschätzte Zeit:** 30-35 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lernst du `box-sizing: border-box` kennen – die Lösung für einfachere Grössenberechnungen!
