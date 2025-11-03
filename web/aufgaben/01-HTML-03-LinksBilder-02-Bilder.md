# Auftrag 2: Bilder einbinden – Dein Portfolio wird visuell

## 🎯 Ziel
Du fügst ein Profilbild und weitere Bilder in dein Portfolio ein und lernst, wie man Bilder korrekt, barrierefrei und performant einbindet.

## 📋 Beschreibung

Bilder machen dein Portfolio persönlich und professionell! Du lernst jetzt, wie man Bilder richtig einbindet, optimiert und beschreibt.

---

### Vorbereitung: Bilder organisieren (5 Min)

Erstelle im Projektordner einen Unterordner:
```
mein-portfolio/
├── index.html
└── images/
    ├── profil.jpg
    └── placeholder.jpg
```

**Bilder besorgen:**
- **Profilbild:** Ein professionelles Foto von dir (Gesicht gut sichtbar)
- **Platzhalterbilder:** Nutze [Unsplash](https://unsplash.com) oder [Pexels](https://www.pexels.com) für freie Bilder
- **Wichtig:** Benenne Dateien sinnvoll (keine Leerzeichen, nur Kleinbuchstaben)

---

### Teil 1: Profilbild im Header (15 Min)

**1. Bild einfügen:**

```html
<header>
    <img src="images/profil.jpg" 
         alt="Profilbild von [Dein Name]" 
         width="200" 
         height="200">
    <h1>Dein Name</h1>
    <p>Informatiker/in EFZ in Ausbildung</p>
    <!-- Navigation -->
</header>
```

**Wichtige Attribute:**
- `src` = Source (Pfad zum Bild)
- `alt` = Alternative Text (für Screenreader & wenn Bild nicht lädt)
- `width` & `height` = Abmessungen (verhindert Layout-Shifts)

**2. Alt-Text richtig schreiben:**

✅ **Gut:**
- `alt="Profilbild von Sarah Müller"`
- `alt="Max Mustermann lächelnd vor einem Laptop"`

❌ **Schlecht:**
- `alt="Bild"` (zu vage)
- `alt="IMG_2024.jpg"` (Dateiname)
- `alt="Ein Bild von mir"` (unnötig)

**3. Bild optimieren:**

Bevor du ein Bild hochlädst:
- Maximale Breite: 400-600px für Profilbilder
- Format: JPG für Fotos, PNG für Grafiken mit Transparenz
- Komprimieren mit: [TinyPNG](https://tinypng.com) oder [Squoosh](https://squoosh.app)

---

### Teil 2: Bilder in der "Über mich"-Sektion (15 Min)

**Füge ein passendes Bild zu deinem Werdegang hinzu:**

```html
<section id="ueber-mich">
    <h2>Über mich</h2>
    
    <img src="images/arbeitsplatz.jpg" 
         alt="Mein Arbeitsplatz mit Laptop und Notizen"
         width="600"
         height="400">
    
    <h3>Mein Werdegang</h3>
    <p>Seit August 2024 lerne ich bei...</p>
    <!-- Restlicher Inhalt -->
</section>
```

**Oder mit Figure & Figcaption (empfohlen für Bildunterschriften):**

```html
<figure>
    <img src="images/arbeitsplatz.jpg" 
         alt="Arbeitsplatz mit zwei Monitoren, Tastatur und Notizblock">
    <figcaption>Mein Arbeitsplatz im Büro</figcaption>
</figure>
```

**Vorteile von `<figure>` und `<figcaption>`:**
- Semantisch korrekt (Browser/Screenreader erkennen Zusammenhang)
- Bildunterschrift ist visuell mit Bild verbunden
- Bessere Struktur im HTML

---

### Teil 3: Bild als Link (10 Min)

**Mache dein Profilbild klickbar:**

```html
<a href="#kontakt" title="Zum Kontaktformular">
    <img src="images/profil.jpg" 
         alt="Profilbild von Dein Name">
</a>
```

**Oder verlinke zu einem externen Profil:**

```html
<a href="https://www.linkedin.com/in/deinprofil" 
   target="_blank" 
   rel="noopener noreferrer">
    <img src="images/profil.jpg" 
         alt="Profilbild von Dein Name – Klicke für LinkedIn-Profil">
</a>
```

**Wichtig beim Alt-Text bei verlinkten Bildern:**
- Beschreibe sowohl das Bild als auch das Link-Ziel
- Beispiel: `alt="GitHub-Logo – Link zu meinem GitHub-Profil"`

---

### Teil 4: Responsive Bilder (Bonus, 5 Min)

**Für verschiedene Bildschirmgrössen:**

```html
<picture>
    <source media="(max-width: 600px)" srcset="images/profil-klein.jpg">
    <source media="(min-width: 601px)" srcset="images/profil-gross.jpg">
    <img src="images/profil.jpg" alt="Profilbild von Dein Name">
</picture>
```

**Oder einfacher mit `srcset`:**

```html
<img src="images/profil.jpg"
     srcset="images/profil-klein.jpg 400w,
             images/profil-mittel.jpg 800w,
             images/profil-gross.jpg 1200w"
     sizes="(max-width: 600px) 400px, 800px"
     alt="Profilbild von Dein Name">
```

---

## ✅ Erfolgskriterien

- [ ] Ein Profilbild ist im Header eingebunden
- [ ] Alle Bilder haben aussagekräftige Alt-Texte
- [ ] Mindestens 2-3 Bilder sind auf der Seite verteilt
- [ ] Mindestens ein Bild nutzt `<figure>` und `<figcaption>`
- [ ] Die Bilder sind optimiert (max. 500 KB pro Bild)
- [ ] Alle Bildpfade funktionieren (keine 404-Fehler)
- [ ] Optional: Ein Bild ist als Link umgesetzt

## 💡 Tipps

- **Alt-Texte sind Pflicht!** Sie sind essentiell für Accessibility
- Relative Pfade verwenden: `images/profil.jpg` (nicht `C:/Users/...`)
- **Profitipp:** Nutze WebP-Format für noch kleinere Dateigrössen (Fallback zu JPG)
- Teste mit DevTools (F12) → Network: Wie gross sind deine Bilder?
- **Performance:** Bilder sollten max. 100-200 KB sein für schnelle Ladezeiten
- Nutze `loading="lazy"` für Bilder weiter unten auf der Seite

## 🤔 Reflexionsfragen

1. Warum ist der Alt-Text so wichtig? Wer profitiert davon?
2. Teste: Deaktiviere in den DevTools das Laden von Bildern. Ist die Seite noch verständlich?
3. Was passiert, wenn du `width` und `height` weglässt? Probiere es aus!
4. Vergleiche: Welche Dateigrösse hat dein Originalbild vs. das optimierte Bild?
5. Recherchiere: Was ist der Unterschied zwischen JPG, PNG und WebP?

## 🔗 Weiterführende Links

- [MDN: `<img>` – Bilder einbinden](https://developer.mozilla.org/de/docs/Web/HTML/Element/img)
- [MDN: `<figure>` und `<figcaption>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/figure)
- [WebAIM: Alternative Text](https://webaim.org/techniques/alttext/)
- [web.dev: Bildoptimierung](https://web.dev/fast/#optimize-your-images)

**Bild-Tools:**
- [TinyPNG](https://tinypng.com) – Bilder komprimieren
- [Squoosh](https://squoosh.app) – Bilder optimieren & konvertieren
- [Unsplash](https://unsplash.com) – Kostenlose Stockfotos
- [Pexels](https://www.pexels.com) – Freie Bilder & Videos

---

**⏱️ Geschätzte Zeit:** 20-25 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 erstellst du eine Projekt-Galerie mit mehreren Bildern!
