# Auftrag 4 (Optional): Barrierefreiheit & SEO – Dein Portfolio für alle zugänglich

## 🎯 Ziel
Du machst deine Portfolio-Seite zugänglich für Menschen mit Beeinträchtigungen und optimierst sie für Suchmaschinen. Dieses Wissen ist in der professionellen Webentwicklung unverzichtbar!

## 📋 Beschreibung

### Teil 1: Meta-Tags für SEO (15 Min)

Ergänze im `<head>` folgende Meta-Tags:

```html
<meta name="description" content="Portfolio von [Dein Name] - Informatiker/in EFZ in Ausbildung. Projekte, Skills und Kontakt.">
<meta name="keywords" content="Portfolio, Webentwicklung, Informatik, [Dein Name]">
<meta name="author" content="Dein Name">
```

**Zusätzlich für Social Media (Open Graph):**
```html
<meta property="og:title" content="Dein Name - Portfolio">
<meta property="og:description" content="Portfolio eines/r Informatiker/in in Ausbildung">
<meta property="og:type" content="website">
```

### Teil 2: Barrierefreiheit (ARIA & Landmarks) (20 Min)

Mache deine Seite zugänglich für Screenreader:

1. **ARIA Landmarks hinzufügen:**
```html
<header role="banner">
    <nav role="navigation" aria-label="Hauptnavigation">
        <!-- Navigation kommt später -->
    </nav>
</header>

<main role="main">
    <!-- Dein Hauptinhalt -->
</main>

<footer role="contentinfo">
    <!-- Dein Footer -->
</footer>
```

2. **Skip Link für Tastaturnutzer:**
Füge ganz oben im `<body>` ein:
```html
<a href="#main-content" class="skip-link">Zum Hauptinhalt springen</a>

<!-- Später im Main: -->
<main id="main-content" role="main">
```

3. **Sprache korrekt auszeichnen:**
Falls du Fremdsprachen verwendest:
```html
<p>Ich spreche <span lang="en">English</span> und <span lang="fr">Français</span></p>
```

### Teil 3: Accessibility-Test (15 Min)

**Tastaturnavigation testen:**
- Drücke `Tab` – Kannst du durch alle interaktiven Elemente navigieren?
- Sind Links und Bereiche klar erkennbar?

**Screenreader simulieren:**
- Nutze die Browser-Extension "Accessibility Insights" oder "WAVE"
- Prüfe, ob deine Überschriften-Hierarchie sinnvoll ist

**Kontrast prüfen:**
- Nutze das Tool auf [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- Stelle sicher, dass Text gut lesbar ist (wird wichtig bei CSS!)

### Teil 4: Zusätzliche Best Practices (10 Min)

```html
<!-- Favicon hinzufügen (erstelle später ein einfaches Icon) -->
<link rel="icon" type="image/x-icon" href="favicon.ico">

<!-- Viewport für perfekte mobile Darstellung -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">

<!-- Verhindere automatisches Zoomen auf Inputs (iOS) -->
<meta name="format-detection" content="telephone=no">
```

## ✅ Erfolgskriterien

- [ ] Meta-Description ist vorhanden und beschreibt dein Portfolio in max. 160 Zeichen
- [ ] ARIA-Landmarks sind korrekt gesetzt (banner, main, contentinfo)
- [ ] Skip-Link ist vorhanden (auch wenn noch nicht sichtbar)
- [ ] Die Überschriften-Hierarchie ist logisch (h1 → h2, keine Sprünge)
- [ ] Mindestens ein Accessibility-Tool wurde verwendet und zeigt keine kritischen Fehler
- [ ] Die Seite funktioniert mit Tastaturnavigation (Tab-Taste)

## 💡 Tipps

- **SEO-Tipp:** Die Meta-Description erscheint in Google-Suchergebnissen – schreibe sie ansprechend!
- **Accessibility ist keine Option:** 15% der Weltbevölkerung leben mit einer Behinderung
- Nutze die Browser-Extension "Lighthouse" (in Chrome/Edge) für einen automatischen Audit
- **Profiwissen:** ARIA sollte sparsam eingesetzt werden – nutze zuerst semantisches HTML
- Teste deine Seite mit deaktiviertem CSS – ist sie immer noch verständlich?

## 🤔 Reflexionsfragen

1. Was passiert, wenn jemand deine Seite bei Google teilt? Welcher Text wird angezeigt?
2. Warum ist ein "Skip Link" wichtig für Tastaturnutzer?
3. Teste mit geschlossenen Augen: Kannst du mit Tab und Enter durch deine Seite navigieren?
4. Was bedeutet "role='banner'" und warum ist das für Screenreader-Nutzer wichtig?
5. Recherchiere: Was ist der Unterschied zwischen ARIA und semantischem HTML?

## 🔗 Weiterführende Links

**SEO:**
- [Google: SEO Starter Guide](https://developers.google.com/search/docs/beginner/seo-starter-guide)
- [Moz: Meta Description Best Practices](https://moz.com/learn/seo/meta-description)

**Accessibility:**
- [WebAIM: Introduction to Web Accessibility](https://webaim.org/intro/)
- [MDN: ARIA Basics](https://developer.mozilla.org/de/docs/Web/Accessibility/ARIA)
- [W3C: ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)

**Tools:**
- [WAVE Browser Extension](https://wave.webaim.org/extension/)
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) (in Chrome DevTools integriert)
- [Contrast Checker](https://webaim.org/resources/contrastchecker/)

## 🏆 Bonus-Challenge

- Führe einen Lighthouse-Audit durch (F12 → Lighthouse → Generate Report)
- Versuche, einen Accessibility-Score von mindestens 90/100 zu erreichen
- Dokumentiere: Welche Verbesserungen schlägt Lighthouse vor?

---

**⏱️ Geschätzte Zeit:** 45-60 Minuten  
**🎓 Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächster Schritt:** Weiter zu HTML-Text – gestalte deinen "Über mich"-Bereich aus!

---

**💬 Hinweis:** Dieser Auftrag ist optional, aber das Wissen wird dich die ganze Karriere begleiten. Accessibility und SEO sind keine "Nice-to-haves", sondern professionelle Standards!
