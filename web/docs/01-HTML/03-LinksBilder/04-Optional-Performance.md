# Auftrag 4 (Optional): Performance & Bildoptimierung – Schneller laden, besser performen

## Ziel
Du lernst fortgeschrittene Techniken zur Bildoptimierung und verstehst, wie man eine Website performant macht. Diese Skills sind in der professionellen Webentwicklung unverzichtbar!

## Beschreibung

Eine langsame Website verliert Besucher/innen. Du lernst jetzt, wie du dein Portfolio auf Performance optimierst – besonders die Bilder, die meist die grössten Dateien sind.

---

### Teil 1: Performance messen (15 Min)

**1. Lighthouse-Audit durchführen:**

- Öffne deine Portfolio-Seite im Browser
- Drücke `F12` → "Lighthouse" Tab
- Klicke auf "Generate report"
- Wähle: "Performance", "Accessibility", "Best Practices", "SEO"
- Klicke "Analyze page load"

**Was du sehen wirst:**
- Performance-Score (0-100)
- Ladezeit und Metriken
- Verbesserungsvorschläge

**Ziel für diesen Auftrag:**
- Performance: Mindestens 80/100
- Accessibility: Mindestens 90/100

**2. Network-Analyse:**

- DevTools → "Network" Tab
- Lade die Seite neu (`Ctrl + Shift + R`)
- Schaue dir die Ladezeiten an
- Sortiere nach "Size" → Welche Dateien sind am grössten?

**Typisches Problem:** Bilder sind oft 5-10 MB statt 50-200 KB!

---

### Teil 2: Bildformate & Kompression (20 Min)

**1. Moderne Bildformate verwenden:**

**WebP – Der neue Standard:**
- 30% kleiner als JPG bei gleicher Qualität
- Unterstützt Transparenz (wie PNG)
- Von allen modernen Browsern unterstützt

**Konvertiere deine Bilder:**
- Nutze [Squoosh.app](https://squoosh.app)
- Lade dein Bild hoch
- Wähle "WebP" als Ausgabeformat
- Stelle Qualität auf 80-85% ein
- Lade die optimierte Datei herunter

**2. Picture-Element mit Fallback:**

```html
<picture>
    <!-- Moderne Browser: WebP -->
    <source type="image/webp" srcset="images/profil.webp">
    <!-- Fallback für ältere Browser: JPG -->
    <img src="images/profil.jpg" 
         alt="Profilbild von Dein Name"
         width="200" 
         height="200">
</picture>
```

**Vorteil:** Moderne Browser laden WebP, ältere Browser JPG.

**3. Responsive Bilder mit srcset:**

Erstelle mehrere Versionen eines Bildes:
- `projekt-klein.jpg` (400px Breite)
- `projekt-mittel.jpg` (800px Breite)
- `projekt-gross.jpg` (1200px Breite)

```html
<img src="images/projekt-mittel.jpg"
     srcset="images/projekt-klein.jpg 400w,
             images/projekt-mittel.jpg 800w,
             images/projekt-gross.jpg 1200w"
     sizes="(max-width: 600px) 400px,
            (max-width: 1200px) 800px,
            1200px"
     alt="Screenshot des Projekts"
     loading="lazy">
```

**Was passiert?**
- Browser wählt automatisch die passende Bildgrösse
- Smartphones laden kleinere Dateien
- Desktop-Bildschirme laden grössere Versionen

---

### Teil 3: Lazy Loading & Preloading (15 Min)

**1. Lazy Loading – Bilder erst laden, wenn sichtbar:**

```html
<!-- Bilder "above the fold" (sofort sichtbar) -->
<img src="images/profil.jpg" 
     alt="Profilbild"
     width="200" 
     height="200">

<!-- Bilder weiter unten auf der Seite -->
<img src="images/projekt1.jpg" 
     alt="Projekt-Screenshot"
     loading="lazy"
     width="600" 
     height="400">
```

**Wann verwenden?**
- ✅ Bilder in Projekt-Galerie (weiter unten)
- ✅ Bilder im Footer
- ❌ Profilbild im Header (sofort sichtbar)
- ❌ Hero-Images (Hauptbilder)

**2. Preloading – Kritische Bilder priorisieren:**

Füge im `<head>` hinzu:

```html
<link rel="preload" 
      href="images/profil.webp" 
      as="image" 
      type="image/webp">
```

**Nutze Preload nur für:**
- Profilbilder, die sofort sichtbar sind
- Hero-Images / Hauptbilder
- Kritische UI-Elemente

**3. Fetchpriority – Ladeprioritäten setzen:**

```html
<!-- Wichtiges Bild: Hohe Priorität -->
<img src="images/profil.jpg" 
     alt="Profilbild"
     fetchpriority="high">

<!-- Unwichtige Bilder: Niedrige Priorität -->
<img src="images/footer-logo.jpg" 
     alt="Logo"
     fetchpriority="low"
     loading="lazy">
```

---

### Teil 4: Image CDN & Caching (10 Min)

**1. Externe Bilder von CDNs nutzen:**

Für Icons oder Logos kannst du CDNs verwenden:

```html
<!-- Statt lokale Dateien: -->
<img src="https://cdn.simpleicons.org/github/white" 
     alt="GitHub Logo"
     width="24" 
     height="24">
```

**Vorteile:**
- Bilder sind weltweit verteilt (schneller)
- Oft schon im Browser-Cache
- Du musst sie nicht hosten

**2. Cache-Control verstehen:**

Füge im `<head>` hinzu (Info für dich, später relevant mit Server):

```html
<!-- Meta-Tag für Browser-Caching -->
<meta http-equiv="Cache-Control" content="public, max-age=31536000">
```

**Was bedeutet das?**
- Browser speichert Bilder lokal
- Beim nächsten Besuch: Sofortiges Laden
- `max-age=31536000` = 1 Jahr Caching

---

### Teil 5: Performance-Best-Practices (10 Min)

**1. Bild-Checkliste erstellen:**

Füge am Ende deiner Seite eine versteckte Kommentar-Sektion ein:

```html
<!--
PERFORMANCE CHECKLIST:
✅ Alle Bilder komprimiert (max. 200 KB)
✅ WebP-Format mit JPG-Fallback
✅ Alt-Texte vorhanden
✅ Width & Height gesetzt
✅ Lazy Loading für Bilder "below the fold"
✅ Responsive Images mit srcset
✅ Lighthouse-Score: Performance >80

BILDOPTIMIERUNG:
- Profilbild: 25 KB (Original: 2 MB) → 98% Ersparnis
- Projekt-Screenshots: je 40-60 KB
- Gesamt-Seitengrösse: < 500 KB

NÄCHSTE SCHRITTE:
- CSS später minifizieren
- JavaScript später defer/async
- Webfonts optimieren
-->
```

**2. Performance-Budget festlegen:**

```html
<!-- Performance-Budget -->
<!--
MAX GRÖSSEN:
- Gesamte Seite: 1 MB
- HTML: 50 KB
- Bilder gesamt: 500 KB
- CSS (später): 100 KB
- JS (später): 200 KB
-->
```

---

## Erfolgskriterien

- [ ] Lighthouse-Audit durchgeführt (Screenshot gemacht)
- [ ] Mindestens 3 Bilder sind WebP mit JPG-Fallback
- [ ] Mindestens 2 Bilder nutzen `srcset` für responsive Versionen
- [ ] Lazy Loading ist bei mindestens 3 Bildern aktiviert
- [ ] Alle Bilder haben `width` und `height` Attribute
- [ ] Performance-Score liegt bei mindestens 80/100
- [ ] Gesamt-Seitengrösse ist unter 1 MB (prüfbar in DevTools → Network)
- [ ] Eine Performance-Checkliste ist im Code dokumentiert

## Tipps

- **Regel:** Bilder sollten nie grösser sein als ihre Anzeigegrösse
- Nutze Online-Tools für Batch-Konvertierung (mehrere Bilder auf einmal)
- **Profitipp:** Erstelle ein Script für automatische Bildoptimierung (später mit Node.js)
- Browser-Cache leeren beim Testen: `Ctrl + Shift + Delete`
- Mobile testen: DevTools → Toggle Device Toolbar (`Ctrl + Shift + M`)

## Reflexionsfragen

1. Führe einen Lighthouse-Audit durch. Was sind die Top 3 Verbesserungsvorschläge?
2. Vergleiche: Wie gross ist deine Seite mit Originalbildern vs. optimierten Bildern?
3. Teste auf langsamem Internet (DevTools → Network → "Slow 3G"). Wie schnell lädt die Seite?
4. Warum sollte man `loading="lazy"` nicht für das Profilbild verwenden?
5. Recherchiere: Was ist der "Core Web Vitals" Standard von Google?

## Weiterführende Links

**Bildoptimierung:**
- [Squoosh](https://squoosh.app) – Bild-Optimizer
- [TinyPNG](https://tinypng.com) – PNG/JPG Kompression
- [ImageOptim](https://imageoptim.com) – Desktop-App (Mac/Win)

**Performance:**
- [web.dev: Performance](https://web.dev/fast/)
- [MDN: Lazy Loading](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading)
- [Google PageSpeed Insights](https://pagespeed.web.dev/)

**Tools & Testing:**
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [WebPageTest](https://www.webpagetest.org/)
- [GTmetrix](https://gtmetrix.com/)

**Responsive Images:**
- [MDN: Responsive Images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
- [CSS-Tricks: Responsive Images](https://css-tricks.com/a-guide-to-the-responsive-images-syntax-in-html/)

---

## Bonus-Challenges

**Challenge 1: Performance-Vergleich**
- Mache einen Lighthouse-Audit VORHER (mit Originalbildern)
- Optimiere alle Bilder
- Mache einen Lighthouse-Audit NACHHER
- Dokumentiere die Verbesserung (z.B. Score von 45 → 92)

**Challenge 2: Automatisierung**
- Recherchiere: Wie kann man Bilder automatisch optimieren?
- Erstelle eine Liste mit Tools (z.B. ImageMagick, Sharp, Gulp)
- Probiere ein Tool aus (später relevant mit Node.js)

**Challenge 3: Mobile-First Testing**
- Teste deine Seite auf echten Smartphones
- Nutze BrowserStack oder ähnliche Tools
- Dokumentiere: Welche Probleme gibt es auf Mobile?

---

**⏱️ Geschätzte Zeit:** 50-70 Minuten  
**🎓 Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächster Schritt:** Glückwunsch! HTML ist abgeschlossen. Weiter mit CSS für das Styling!

---

**💬 Hinweis:** Performance-Optimierung ist ein laufender Prozess. Die hier gelernten Techniken wirst du in jedem professionellen Projekt anwenden. Laut Google verlassen 53% der mobilen Nutzer/innen eine Seite, wenn sie länger als 3 Sekunden lädt – Performance ist also nicht optional!
