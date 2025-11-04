# Auftrag 3: Skills & Interessen – Strukturieren mit Listen

## Ziel
Du erstellst übersichtliche Listen für deine Fähigkeiten und Interessen und lernst, wann ungeordnete bzw. geordnete Listen sinnvoll sind.

## Beschreibung

Listen machen Inhalte scanbar und übersichtlich – perfekt für ein Portfolio! Du fügst jetzt zwei neue Sektionen hinzu.

### Teil 1: Deine Skills (ungeordnete Liste)

Erstelle eine neue Sektion mit `<h2>Meine Skills</h2>` und liste deine Fähigkeiten auf:

**Ungeordnete Liste (`<ul>`) verwenden, weil:**
- Die Reihenfolge keine Rolle spielt
- Es keine Hierarchie gibt
- Alles gleichwertig ist

**Was du auflisten sollst:**
- Technische Skills (z.B. HTML, VS Code, Git)
- Soft Skills (z.B. Teamfähigkeit, Lernbereitschaft)
- Sprachen (z.B. Deutsch, Englisch)
- Aktuell Gelerntes (z.B. "Grundlagen Webentwicklung")

**Beispiel:**
```html
<h2>Meine Skills</h2>

<h3>Technische Fähigkeiten</h3>
<ul>
    <li><strong>HTML & CSS</strong> – Grundlagen der Webentwicklung</li>
    <li><strong>Visual Studio Code</strong> – Täglicher Code-Editor</li>
    <li><strong>Git</strong> – Versionsverwaltung (in Arbeit)</li>
    <li><strong>Microsoft 365</strong> – Teams, SharePoint, Outlook</li>
</ul>

<h3>Persönliche Kompetenzen</h3>
<ul>
    <li>Teamfähigkeit und Kommunikationsstärke</li>
    <li>Lernbereitschaft und Eigeninitiative</li>
    <li>Problemlösungskompetenz</li>
</ul>

<h3>Sprachen</h3>
<ul>
    <li><strong>Deutsch</strong> – Muttersprache</li>
    <li><strong>Englisch</strong> – Gut (B1-B2)</li>
    <li><strong>Französisch</strong> – Grundkenntnisse (A2)</li>
</ul>
```

### Teil 2: Lernziele (geordnete Liste)

Erstelle eine neue Sektion mit `<h2>Meine Lernziele</h2>`:

**Geordnete Liste (`<ol>`) verwenden, weil:**
- Die Reihenfolge wichtig ist
- Es Prioritäten gibt
- Schritte aufeinander aufbauen

**Beispiel:**
```html
<h2>Meine Lernziele</h2>
<p>In den nächsten 6 Monaten möchte ich folgende Ziele erreichen:</p>

<ol>
    <li>HTML & CSS sicher beherrschen und eine vollständige Website erstellen</li>
    <li>JavaScript-Grundlagen erlernen und interaktive Elemente programmieren</li>
    <li>Mein erstes kleines Projekt selbstständig umsetzen</li>
    <li>Git für Versionsverwaltung im Team nutzen können</li>
    <li>Ein funktionales Portfolio mit allen Projekten veröffentlichen</li>
</ol>
```

### Teil 3: Verschachtelte Liste (Bonus)

Erstelle eine verschachtelte Liste für detailliertere Infos:

```html
<h2>Meine Hobbies & Interessen</h2>
<ul>
    <li>
        <strong>Gaming</strong>
        <ul>
            <li>Strategiespiele</li>
            <li>Indie-Games</li>
        </ul>
    </li>
    <li>
        <strong>Sport</strong>
        <ul>
            <li>Fussball (im Verein seit 2018)</li>
            <li>Krafttraining</li>
        </ul>
    </li>
    <li><strong>Fotografie</strong> – besonders Landschaftsfotografie</li>
</ul>
```

## Erfolgskriterien

- [ ] Eine "Meine Skills"-Sektion mit mindestens 3 Kategorien existiert
- [ ] Jede Kategorie nutzt eine `<ul>` mit mindestens 3-4 Punkten
- [ ] Eine "Meine Lernziele"-Sektion mit einer `<ol>` ist vorhanden
- [ ] Die geordnete Liste hat mindestens 4-5 Punkte
- [ ] Optional: Eine verschachtelte Liste ist korrekt umgesetzt
- [ ] Alle Listen sind sauber eingerückt und formatiert
- [ ] Die Seite bleibt übersichtlich und professionell

## Tipps

- **`<ul>` = Unordered List** (Aufzählungspunkte, Bulletpoints)
- **`<ol>` = Ordered List** (Nummerierte Liste, 1, 2, 3...)
- Jedes Listenelement braucht ein `<li>`-Tag (List Item)
- **Profitipp:** Nutze `<strong>` in Listen, um wichtige Begriffe hervorzuheben
- Verschachtelte Listen brauchen saubere Einrückung – nutze `Shift + Alt + F` in VS Code
- **Mobile-Tipp:** Listen sind auf Smartphones besonders gut lesbar

## Reflexionsfragen

1. Wann würdest du eine `<ul>` und wann eine `<ol>` verwenden? Gib je 2 Beispiele.
2. Teste: Was passiert, wenn du ein `<li>` ohne `<ul>` oder `<ol>` schreibst?
3. Vergleiche deine Seite vorher/nachher: Sind die Listen leichter zu lesen als Fliesstext?
4. Öffne die DevTools (F12): Wie werden verschachtelte Listen im HTML-Baum dargestellt?
5. Überlege: Welche Listenart würdest du für ein Rezept verwenden? Warum?

## Weiterführende Links

- [MDN: `<ul>` – Ungeordnete Listen](https://developer.mozilla.org/de/docs/Web/HTML/Element/ul)
- [MDN: `<ol>` – Geordnete Listen](https://developer.mozilla.org/de/docs/Web/HTML/Element/ol)
- [MDN: `<li>` – Listenelemente](https://developer.mozilla.org/de/docs/Web/HTML/Element/li)
- [W3Schools: HTML Lists](https://www.w3schools.com/html/html_lists.asp)

---

**⏱️ Geschätzte Zeit:** 25-30 Minuten  
**📦 Nächster Schritt:** Optional: Vertiefe dein Wissen über Typografie und Textgestaltung!
