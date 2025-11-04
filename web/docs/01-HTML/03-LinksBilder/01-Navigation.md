# Auftrag 1: Navigation – Verlinke deine Portfolio-Bereiche

## Ziel
Du erstellst eine funktionierende Navigation für dein Portfolio und lernst verschiedene Link-Arten kennen (intern, extern, E-Mail, Telefon).

## Beschreibung

Jedes Portfolio braucht eine Navigation! Du erstellst jetzt Links zu deinen verschiedenen Sektionen und fügst externe Kontaktmöglichkeiten hinzu.

---

### Teil 1: Interne Navigation mit Anker-Links (20 Min)

**1. IDs für Sektionen vergeben:**

Füge deinen Hauptsektionen IDs hinzu:

```html
<main>
    <section id="ueber-mich">
        <h2>Über mich</h2>
        <!-- Dein bestehender Inhalt -->
    </section>
    
    <section id="skills">
        <h2>Meine Skills</h2>
        <!-- Dein bestehender Inhalt -->
    </section>
    
    <section id="lernziele">
        <h2>Meine Lernziele</h2>
        <!-- Dein bestehender Inhalt -->
    </section>
    
    <section id="kontakt">
        <h2>Kontakt</h2>
        <!-- Dein bestehender Inhalt -->
    </section>
</main>
```

**2. Navigation im Header erstellen:**

```html
<header>
    <h1>Dein Name</h1>
    <p>Informatiker/in EFZ in Ausbildung</p>
    
    <nav>
        <ul>
            <li><a href="#ueber-mich">Über mich</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#lernziele">Lernziele</a></li>
            <li><a href="#kontakt">Kontakt</a></li>
        </ul>
    </nav>
</header>
```

**Wie es funktioniert:**
- `#ueber-mich` springt zur Sektion mit `id="ueber-mich"`
- Das nennt man "Anker-Link" oder "Jump-Link"
- Perfekt für einseitige Portfolios (Single Page)

---

### Teil 2: Externe Links (10 Min)

Füge in deiner Kontakt-Sektion externe Links hinzu:

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    
    <h3>Finde mich online</h3>
    <ul>
        <li>
            <a href="https://github.com/deinbenutzername" 
               target="_blank" 
               rel="noopener noreferrer">
                GitHub
            </a>
        </li>
        <li>
            <a href="https://www.linkedin.com/in/deinprofil" 
               target="_blank" 
               rel="noopener noreferrer">
                LinkedIn
            </a>
        </li>
    </ul>
</section>
```

**Wichtige Attribute:**
- `target="_blank"` → Öffnet Link in neuem Tab
- `rel="noopener noreferrer"` → Sicherheit (verhindert Zugriff auf deine Seite)

---

### Teil 3: Kontakt-Links (E-Mail & Telefon) (10 Min)

**1. E-Mail-Link:**

```html
<h3>Direkter Kontakt</h3>
<p>
    <strong>E-Mail:</strong> 
    <a href="mailto:deine.email@firma.ch">deine.email@firma.ch</a>
</p>
```

**Mit vorausgefülltem Betreff:**
```html
<a href="mailto:deine.email@firma.ch?subject=Anfrage%20Portfolio">
    Schreib mir eine E-Mail
</a>
```

**2. Telefon-Link:**

```html
<p>
    <strong>Telefon:</strong> 
    <a href="tel:+41791234567">+41 79 123 45 67</a>
</p>
```

**Warum wichtig?**
- Auf Smartphones wird direkt die Telefon-App geöffnet
- Auf Desktops erscheint eine entsprechende Anwendung

---

### Teil 4: "Zurück nach oben"-Link (5 Min)

Füge am Ende deiner Seite einen Link zurück zum Anfang:

```html
<footer>
    <a href="#top" title="Zurück nach oben">↑ Nach oben</a>
    <p>© 2025 Dein Name</p>
</footer>
```

Und im `<body>`-Tag ganz oben:
```html
<body id="top">
```

---

## Erfolgskriterien

- [ ] Eine Navigation mit mindestens 4 internen Links existiert
- [ ] Alle Anker-Links funktionieren und springen zur richtigen Sektion
- [ ] Mindestens 1-2 externe Links sind vorhanden (GitHub, LinkedIn, etc.)
- [ ] Externe Links öffnen in einem neuen Tab (`target="_blank"`)
- [ ] Ein funktionierender E-Mail-Link ist vorhanden
- [ ] Optional: Ein Telefon-Link ist eingebaut
- [ ] Ein "Nach oben"-Link existiert und funktioniert
- [ ] Alle Links sind klar beschriftet (kein "hier klicken")

## Tipps

- **Beschreibende Linktexte:** Schreib "GitHub-Profil" statt "Klick hier"
- **Accessibility:** Screenreader lesen Linktexte vor – sie sollten Sinn ergeben
- `target="_blank"` ohne `rel="noopener"` ist ein Sicherheitsrisiko!
- **Profitipp:** Nutze das `title`-Attribut für zusätzliche Info beim Hover
- Teste alle Links – nichts ist peinlicher als ein kaputter Link im Portfolio

## Reflexionsfragen

1. Was ist der Unterschied zwischen `href="#kontakt"` und `href="kontakt.html"`?
2. Warum ist `target="_blank"` bei externen Links sinnvoll, aber nicht bei internen?
3. Teste: Was passiert, wenn du auf einen E-Mail-Link klickst? Welches Programm öffnet sich?
4. Warum sollte man "Klick hier" als Linktext vermeiden? Was wäre besser?
5. Öffne die DevTools (F12) → Network: Was passiert, wenn du auf einen `#`-Link klickst?

## Weiterführende Links

- [MDN: `<a>` – Der Anker-Tag](https://developer.mozilla.org/de/docs/Web/HTML/Element/a)
- [MDN: `<nav>` – Navigation](https://developer.mozilla.org/de/docs/Web/HTML/Element/nav)
- [WebAIM: Links und Hypertext](https://webaim.org/techniques/hypertext/)
- [rel="noopener" Sicherheit](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/noopener)

---

**⏱️ Geschätzte Zeit:** 25-30 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 fügst du Bilder hinzu – dein Profil wird visuell!
