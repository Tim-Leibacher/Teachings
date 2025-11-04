# Auftrag 3: Feedback-Formular – Validierung und Best Practices

## Ziel
Du erstellst ein Feedback-Formular mit fortgeschrittenen Validierungstechniken, verstehst Pattern-Validierung und setzt Best Practices für benutzerfreundliche Formulare um.

## Beschreibung

Professionelle Formulare validieren Eingaben, bevor sie abgesendet werden. Du lernst jetzt erweiterte Validierungsmethoden und wie man Formulare benutzerfreundlich gestaltet.

---

### Schritt 1: Feedback-Seite erstellen (5 Min)

Erstelle eine neue Sektion in deiner `index.html` oder eine separate Seite:

```html
<section id="feedback">
    <h2>Feedback geben</h2>
    <p>Deine Meinung ist uns wichtig! Teile dein Feedback mit uns.</p>
    
    <form action="#" method="post">
        <!-- Formular-Inhalt -->
    </form>
</section>
```

---

### Schritt 2: Bewertung mit Range-Slider (10 Min)

```html
<fieldset>
    <legend>Deine Bewertung</legend>
    
    <label for="zufriedenheit">Wie zufrieden bist du mit dem Portfolio?</label>
    <input type="range" 
           id="zufriedenheit" 
           name="zufriedenheit" 
           min="1" 
           max="5" 
           value="3" 
           step="1">
    <output for="zufriedenheit">3</output>
    <small>(1 = Unzufrieden, 5 = Sehr zufrieden)</small>
    
    <label for="bewertung">Gesamtbewertung (1-10):</label>
    <input type="number" 
           id="bewertung" 
           name="bewertung" 
           min="1" 
           max="10" 
           required>
</fieldset>
```

**Neu: `<output>`**
- Zeigt den aktuellen Wert eines Range-Sliders an
- Wird später mit JavaScript dynamisch aktualisiert

---

### Schritt 3: Pattern-Validierung (15 Min)

```html
<fieldset>
    <legend>Kontaktdaten</legend>
    
    <label for="plz">Postleitzahl (4 Ziffern):</label>
    <input type="text" 
           id="plz" 
           name="plz" 
           pattern="[0-9]{4}" 
           title="Bitte gib eine 4-stellige Postleitzahl ein"
           placeholder="z.B. 3011"
           required>
    
    <label for="website">Deine Website (optional):</label>
    <input type="url" 
           id="website" 
           name="website" 
           placeholder="https://example.com">
    
    <label for="benutzername">Benutzername (3-16 Zeichen, nur Buchstaben/Zahlen):</label>
    <input type="text" 
           id="benutzername" 
           name="benutzername" 
           pattern="[a-zA-Z0-9]{3,16}" 
           title="3-16 Zeichen, nur Buchstaben und Zahlen"
           required>
</fieldset>
```

**Pattern-Validierung:**
- `pattern="[0-9]{4}"` = Genau 4 Ziffern
- `pattern="[a-zA-Z0-9]{3,16}"` = 3-16 alphanumerische Zeichen
- `title` zeigt Hilfstext bei ungültiger Eingabe

---

### Schritt 4: Kategorien und Feedback-Typen (10 Min)

```html
<fieldset>
    <legend>Feedback-Kategorie</legend>
    
    <label for="kategorie">Worum geht es?</label>
    <select id="kategorie" name="kategorie" required>
        <option value="">-- Bitte wählen --</option>
        <option value="design">Design & Layout</option>
        <option value="inhalt">Inhalte & Texte</option>
        <option value="technik">Technische Aspekte</option>
        <option value="usability">Benutzerfreundlichkeit</option>
        <option value="sonstiges">Sonstiges</option>
    </select>
    
    <p>Art des Feedbacks:</p>
    <input type="radio" id="lob" name="feedback-typ" value="lob" checked>
    <label for="lob">Lob</label><br>
    
    <input type="radio" id="kritik" name="feedback-typ" value="kritik">
    <label for="kritik">Konstruktive Kritik</label><br>
    
    <input type="radio" id="vorschlag" name="feedback-typ" value="vorschlag">
    <label for="vorschlag">Verbesserungsvorschlag</label><br>
    
    <input type="radio" id="bug" name="feedback-typ" value="bug">
    <label for="bug">Fehler melden</label>
</fieldset>
```

---

### Schritt 5: Detailliertes Feedback (10 Min)

```html
<fieldset>
    <legend>Dein Feedback</legend>
    
    <label for="titel">Titel deines Feedbacks:</label>
    <input type="text" 
           id="titel" 
           name="titel" 
           minlength="5" 
           maxlength="100" 
           placeholder="Kurze Zusammenfassung"
           required>
    
    <label for="beschreibung">Detaillierte Beschreibung:</label>
    <textarea id="beschreibung" 
              name="beschreibung" 
              rows="6" 
              minlength="20" 
              maxlength="1000" 
              placeholder="Beschreibe dein Feedback so detailliert wie möglich..."
              required></textarea>
    <small>Mindestens 20 Zeichen, maximal 1000 Zeichen</small>
</fieldset>
```

**Neue Attribute:**
- `minlength` / `maxlength` = Zeichenlänge begrenzen
- Funktioniert bei `<input type="text">` und `<textarea>`

---

### Schritt 6: Priorität und Anonymität (5 Min)

```html
<fieldset>
    <legend>Zusätzliche Optionen</legend>
    
    <label for="prioritaet">Priorität:</label>
    <select id="prioritaet" name="prioritaet">
        <option value="niedrig">Niedrig</option>
        <option value="mittel" selected>Mittel</option>
        <option value="hoch">Hoch</option>
    </select>
    
    <input type="checkbox" id="anonym" name="anonym" value="ja">
    <label for="anonym">Feedback anonym absenden</label><br>
    
    <input type="checkbox" id="benachrichtigung" name="benachrichtigung" value="ja" checked>
    <label for="benachrichtigung">Benachrichtige mich bei Änderungen</label>
</fieldset>
```

---

### Schritt 7: Datenschutz und Absenden (5 Min)

```html
<fieldset>
    <legend>Datenschutz</legend>
    
    <input type="checkbox" id="datenschutz" name="datenschutz" value="akzeptiert" required>
    <label for="datenschutz">
        Ich habe die <a href="#" target="_blank">Datenschutzerklärung</a> gelesen und akzeptiere sie.
    </label>
</fieldset>

<button type="submit">Feedback absenden</button>
<button type="reset">Formular zurücksetzen</button>
```

---

## Erfolgskriterien

- [ ] Ein Feedback-Formular mit mindestens 10 Eingabefeldern existiert
- [ ] Mindestens 2 Pattern-Validierungen sind implementiert (`pattern="..."`)
- [ ] Ein Range-Slider (`type="range"`) mit `<output>` ist vorhanden
- [ ] Mindestens 3 Felder nutzen `minlength` oder `maxlength`
- [ ] Ein `type="url"` Feld validiert Website-Adressen
- [ ] Radio-Buttons für Feedback-Typ sind implementiert
- [ ] Ein Dropdown zur Kategorisierung existiert
- [ ] Datenschutz-Checkbox ist Pflichtfeld
- [ ] Alle Felder haben aussagekräftige Labels und Hilfstext
- [ ] Die Validierung funktioniert beim Absenden (teste mit ungültigen Daten)

---

## Tipps

- **Aussagekräftige Fehlermeldungen:** Das `title`-Attribut wird bei Pattern-Fehlern angezeigt
- **Benutzerfreundlichkeit:** Zeige Zeichenzähler mit `<small>` unter Textfeldern
- **Profitipp:** Kombiniere `type="url"` mit `pattern` für noch strengere Validierung
- Teste mit absichtlich falschen Eingaben (z.B. 3-stellige PLZ)
- **Best Practice:** Validiere sowohl Client-seitig (HTML) als auch Server-seitig (später mit Backend)
- `required` bei Checkboxen funktioniert nur, wenn sie gecheckt werden muss (z.B. AGB)

---

## Reflexionsfragen

1. Was ist der Unterschied zwischen Browser-Validierung und Server-Validierung? Warum braucht man beides?
2. Teste: Versuche, eine 3-stellige Postleitzahl einzugeben. Was passiert?
3. Erstelle ein eigenes Pattern für Schweizer Telefonnummern (Format: +41 79 123 45 67). Wie sieht der Regex aus?
4. Warum sollte man `minlength` und `maxlength` bei Textfeldern setzen? Welche Vor-/Nachteile gibt es?
5. Inspiziere das Formular mit DevTools (F12) → Elements: Welche Attribute siehst du bei invaliden Feldern?

---

## Weiterführende Links

- [MDN: Client-Side Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [MDN: HTML Input Pattern](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/pattern)
- [Regex101](https://regex101.com/) – Pattern-Tester
- [HTML5 Pattern Library](https://www.html5pattern.com/)
- [W3C: Forms Best Practices](https://www.w3.org/WAI/tutorials/forms/)

---

**Geschätzte Zeit:** 40-45 Minuten  
**Nächster Schritt:** Optional: Vertiefe dein Wissen über fortgeschrittene Formular-Techniken!
