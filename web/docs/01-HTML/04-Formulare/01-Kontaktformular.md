# Auftrag 1: Kontaktformular – Dein Portfolio wird interaktiv

## Ziel
Du erstellst ein funktionales Kontaktformular für dein Portfolio, mit dem Besucher dich erreichen können. Du lernst die Grundlagen von Formularen, Eingabefeldern und Validierung.

## Beschreibung

Jedes professionelle Portfolio braucht eine Kontaktmöglichkeit! Du erweiterst deine Kontakt-Sektion um ein echtes Formular.

---

### Schritt 1: Formular-Grundstruktur (10 Min)

Füge in deiner Kontakt-Sektion ein Formular ein:

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    <p>Hast du Fragen oder möchtest du mit mir zusammenarbeiten? Fülle das Formular aus!</p>
    
    <form action="kontakt-verarbeitung.php" method="post">
        <!-- Hier kommen die Eingabefelder -->
    </form>
</section>
```

**Wichtige Attribute:**
- `action` = Wohin werden die Daten gesendet? (Später mit Backend)
- `method="post"` = Daten werden sicher übertragen (nicht in der URL sichtbar)

**Hinweis:** Für jetzt funktioniert das Formular noch nicht richtig (kein Backend). Du lernst die Struktur!

---

### Schritt 2: Name und E-Mail (15 Min)

Füge die ersten Eingabefelder hinzu:

```html
<form action="#" method="post">
    <fieldset>
        <legend>Deine Daten</legend>
        
        <label for="name">Name:</label>
        <input type="text" 
               id="name" 
               name="name" 
               placeholder="z.B. Anna Müller"
               required>
        
        <label for="email">E-Mail-Adresse:</label>
        <input type="email" 
               id="email" 
               name="email" 
               placeholder="anna.mueller@example.ch"
               required>
    </fieldset>
</form>
```

**Warum diese Attribute?**
- `type="email"` validiert automatisch E-Mail-Format
- `required` macht das Feld zur Pflicht
- `placeholder` zeigt einen Beispieltext
- `id` und `for` verbinden Label und Input

---

### Schritt 3: Betreff und Nachricht (10 Min)

Ergänze Betreff und eine mehrzeilige Nachricht:

```html
<fieldset>
    <legend>Deine Nachricht</legend>
    
    <label for="betreff">Betreff:</label>
    <input type="text" 
           id="betreff" 
           name="betreff" 
           placeholder="Worum geht es?"
           required>
    
    <label for="nachricht">Nachricht:</label>
    <textarea id="nachricht" 
              name="nachricht" 
              rows="6" 
              placeholder="Schreibe deine Nachricht hier..."
              required></textarea>
</fieldset>
```

**`<textarea>` vs. `<input type="text">`:**
- `<textarea>` = Mehrere Zeilen, für längere Texte
- `<input>` = Eine Zeile, für kurze Texte

---

### Schritt 4: Buttons hinzufügen (5 Min)

Füge am Ende des Formulars Buttons hinzu:

```html
<button type="submit">Nachricht senden</button>
<button type="reset">Formular zurücksetzen</button>
```

**Button-Typen:**
- `type="submit"` = Sendet das Formular ab
- `type="reset"` = Löscht alle Eingaben
- Ohne `type` = Verhält sich wie `submit`

---

### Komplettes Beispiel:

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    <p>Hast du Fragen? Fülle das Formular aus und ich melde mich bei dir!</p>
    
    <form action="#" method="post">
        <fieldset>
            <legend>Deine Daten</legend>
            
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" placeholder="z.B. Max Mustermann" required>
            
            <label for="email">E-Mail-Adresse:</label>
            <input type="email" id="email" name="email" placeholder="max@example.ch" required>
        </fieldset>
        
        <fieldset>
            <legend>Deine Nachricht</legend>
            
            <label for="betreff">Betreff:</label>
            <input type="text" id="betreff" name="betreff" placeholder="Worum geht es?" required>
            
            <label for="nachricht">Nachricht:</label>
            <textarea id="nachricht" name="nachricht" rows="6" placeholder="Deine Nachricht..." required></textarea>
        </fieldset>
        
        <button type="submit">Nachricht senden</button>
        <button type="reset">Zurücksetzen</button>
    </form>
</section>
```

---

## Erfolgskriterien

- [ ] Ein `<form>`-Element mit `action` und `method` ist vorhanden
- [ ] Mindestens 2 `<fieldset>` gruppieren die Felder logisch
- [ ] Alle Eingabefelder haben passende `<label>` mit `for`-Attribut
- [ ] Ein `type="email"` Feld validiert E-Mail-Adressen
- [ ] Ein `<textarea>` für längere Nachrichten existiert
- [ ] Mindestens 3 Felder sind mit `required` als Pflichtfelder markiert
- [ ] Submit- und Reset-Button sind vorhanden
- [ ] Formular-Validierung funktioniert (teste mit leerem Formular)

---

## Tipps

- **Labels sind Pflicht!** Sie machen Formulare barrierefrei und anklickbar
- Teste mit leerem Formular – Browser zeigt automatisch Fehlermeldungen
- `action="#"` bedeutet: Formular sendet an sich selbst (Platzhalter für später)
- **Accessibility:** Nutze `<fieldset>` und `<legend>` für logische Gruppierung
- **Profitipp:** Mit `autocomplete="name"` und `autocomplete="email"` kann der Browser Felder automatisch ausfüllen

---

## Reflexionsfragen

1. Was ist der Unterschied zwischen `method="get"` und `method="post"`? Wann nutzt man was?
2. Teste: Was passiert, wenn du ein Pflichtfeld leer lässt und auf "Senden" klickst?
3. Warum ist das `for`-Attribut im Label so wichtig? Teste: Klicke auf ein Label – was passiert?
4. Öffne die DevTools (F12) → Console: Gibt es Fehler oder Warnungen?
5. Recherchiere: Was ist der Unterschied zwischen `<button type="submit">` und `<input type="submit">`?

---

## Weiterführende Links

- [MDN: `<form>` – Formulare](https://developer.mozilla.org/de/docs/Web/HTML/Element/form)
- [MDN: `<input>` – Eingabefelder](https://developer.mozilla.org/de/docs/Web/HTML/Element/input)
- [MDN: `<textarea>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/textarea)
- [MDN: Formular-Validierung](https://developer.mozilla.org/de/docs/Learn/Forms/Form_validation)
- [WebAIM: Accessible Forms](https://webaim.org/techniques/forms/)

---

**Geschätzte Zeit:** 30-35 Minuten  
**Nächster Schritt:** In Auftrag 2 erstellst du ein Anmeldeformular mit verschiedenen Input-Typen!
