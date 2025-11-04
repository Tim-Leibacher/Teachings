# Auftrag 2: Anmeldeformular – Verschiedene Input-Typen

## Ziel
Du erweiterst dein Wissen über Formulare und lernst verschiedene Input-Typen kennen: Radio-Buttons, Checkboxen, Dropdown-Menüs und spezielle HTML5-Typen.

## Beschreibung

Formulare können viel mehr als nur Text! Du erstellst jetzt ein Anmeldeformular für ein fiktives Weiterbildungs-Event, bei dem verschiedene Eingabetypen zum Einsatz kommen.

---

### Schritt 1: Neue Seite erstellen (5 Min)

Erstelle eine neue Datei: `anmeldung.html`

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event-Anmeldung</title>
</head>
<body>
    <header>
        <h1>Web-Development Workshop</h1>
        <p>Melde dich jetzt für unseren Workshop an!</p>
    </header>
    
    <main>
        <!-- Formular kommt hier -->
    </main>
    
    <footer>
        <p><a href="index.html">Zurück zum Portfolio</a></p>
    </footer>
</body>
</html>
```

Verlinke von deinem Portfolio aus:
```html
<a href="anmeldung.html">Zum Workshop anmelden</a>
```

---

### Schritt 2: Persönliche Daten mit HTML5-Typen (15 Min)

```html
<form action="#" method="post">
    <fieldset>
        <legend>Persönliche Daten</legend>
        
        <label for="vorname">Vorname:</label>
        <input type="text" id="vorname" name="vorname" required>
        
        <label for="nachname">Nachname:</label>
        <input type="text" id="nachname" name="nachname" required>
        
        <label for="geburtsdatum">Geburtsdatum:</label>
        <input type="date" id="geburtsdatum" name="geburtsdatum" required>
        
        <label for="email">E-Mail:</label>
        <input type="email" id="email" name="email" required>
        
        <label for="telefon">Telefon:</label>
        <input type="tel" id="telefon" name="telefon" placeholder="+41 79 123 45 67">
        
        <label for="teilnehmer">Anzahl Teilnehmer:</label>
        <input type="number" id="teilnehmer" name="teilnehmer" min="1" max="5" value="1">
    </fieldset>
</form>
```

**Neue Input-Typen:**
- `type="date"` → Öffnet Kalender-Widget
- `type="tel"` → Optimiert für Telefonnummern (besonders auf Mobile)
- `type="number"` → Erlaubt nur Zahlen, mit `min` und `max` begrenzt

---

### Schritt 3: Radio-Buttons für Einzelauswahl (10 Min)

```html
<fieldset>
    <legend>Erfahrungslevel</legend>
    <p>Wähle dein aktuelles Niveau:</p>
    
    <input type="radio" id="anfaenger" name="level" value="anfaenger" checked>
    <label for="anfaenger">Anfänger – Keine Vorkenntnisse</label><br>
    
    <input type="radio" id="fortgeschritten" name="level" value="fortgeschritten">
    <label for="fortgeschritten">Fortgeschritten – Grundkenntnisse vorhanden</label><br>
    
    <input type="radio" id="profi" name="level" value="profi">
    <label for="profi">Profi – Mehrjährige Erfahrung</label>
</fieldset>
```

**Wichtig bei Radio-Buttons:**
- Alle Buttons einer Gruppe brauchen den **gleichen `name`**
- Nur **ein** Button kann ausgewählt werden
- `checked` setzt eine Vorauswahl

---

### Schritt 4: Checkboxen für Mehrfachauswahl (10 Min)

```html
<fieldset>
    <legend>Interessengebiete</legend>
    <p>Wähle alle Themen, die dich interessieren:</p>
    
    <input type="checkbox" id="html" name="themen" value="html">
    <label for="html">HTML & Semantik</label><br>
    
    <input type="checkbox" id="css" name="themen" value="css">
    <label for="css">CSS & Layout</label><br>
    
    <input type="checkbox" id="javascript" name="themen" value="javascript">
    <label for="javascript">JavaScript & Interaktivität</label><br>
    
    <input type="checkbox" id="accessibility" name="themen" value="accessibility">
    <label for="accessibility">Barrierefreiheit</label><br>
    
    <input type="checkbox" id="performance" name="themen" value="performance">
    <label for="performance">Performance-Optimierung</label>
</fieldset>
```

**Unterschied Checkbox vs. Radio:**
- **Checkbox:** Mehrere Optionen wählbar
- **Radio:** Nur eine Option wählbar

---

### Schritt 5: Dropdown-Menü (10 Min)

```html
<fieldset>
    <legend>Workshop-Details</legend>
    
    <label for="kurs">Workshop wählen:</label>
    <select id="kurs" name="kurs" required>
        <option value="">-- Bitte wählen --</option>
        <option value="webbasics">Web Basics (2 Tage)</option>
        <option value="advanced">Advanced Frontend (3 Tage)</option>
        <option value="fullstack">Fullstack Bootcamp (5 Tage)</option>
    </select>
    
    <label for="standort">Standort:</label>
    <select id="standort" name="standort" required>
        <option value="">-- Bitte wählen --</option>
        <option value="zuerich">Zürich</option>
        <option value="bern">Bern</option>
        <option value="basel">Basel</option>
        <option value="online">Online</option>
    </select>
</fieldset>
```

**Dropdown-Tipps:**
- Erste Option oft ein Platzhalter mit leerem `value`
- `required` funktioniert mit leerer erster Option
- `<optgroup>` gruppiert Optionen (optional)

---

### Schritt 6: Zusätzliche Angaben (5 Min)

```html
<fieldset>
    <legend>Zusätzliche Angaben</legend>
    
    <label for="ernaehrung">Ernährungspräferenzen:</label>
    <select id="ernaehrung" name="ernaehrung">
        <option value="keine">Keine Einschränkungen</option>
        <option value="vegetarisch">Vegetarisch</option>
        <option value="vegan">Vegan</option>
        <option value="glutenfrei">Glutenfrei</option>
    </select>
    
    <label for="anmerkungen">Anmerkungen:</label>
    <textarea id="anmerkungen" name="anmerkungen" rows="4" placeholder="Allergien, besondere Wünsche..."></textarea>
    
    <input type="checkbox" id="newsletter" name="newsletter" value="ja">
    <label for="newsletter">Ich möchte den Newsletter erhalten</label><br>
    
    <input type="checkbox" id="agb" name="agb" value="akzeptiert" required>
    <label for="agb">Ich akzeptiere die <a href="#">AGB</a></label>
</fieldset>
```

---

### Schritt 7: Absenden-Button (5 Min)

```html
<button type="submit">Verbindlich anmelden</button>
<button type="reset">Formular zurücksetzen</button>
```

---

## Erfolgskriterien

- [ ] Eine neue `anmeldung.html` Seite existiert und ist vom Portfolio verlinkt
- [ ] Mindestens 3 verschiedene HTML5-Input-Typen sind verwendet (date, tel, number, etc.)
- [ ] Eine Radio-Button-Gruppe mit mindestens 3 Optionen existiert
- [ ] Mindestens 5 Checkboxen für Mehrfachauswahl sind vorhanden
- [ ] Mindestens 2 Dropdown-Menüs mit `<select>` und `<option>` existieren
- [ ] Alle Eingabefelder haben korrekte Labels
- [ ] Mindestens 5 Felder sind mit `required` als Pflicht markiert
- [ ] Die Formular-Validierung funktioniert beim Absenden

---

## Tipps

- **Mobile-Optimierung:** `type="tel"` und `type="email"` öffnen auf Smartphones die passende Tastatur
- **Vorauswahl:** Mit `checked` (Radio/Checkbox) oder `selected` (Dropdown) kannst du Standardwerte setzen
- **Profitipp:** Gruppiere Radio-Buttons und Checkboxen visuell mit `<fieldset>`
- Teste alle Input-Typen auf verschiedenen Geräten – sie verhalten sich unterschiedlich
- **Accessibility:** Radio-Buttons und Checkboxen sollten mit Pfeiltasten navigierbar sein

---

## Reflexionsfragen

1. Was passiert, wenn zwei Radio-Buttons unterschiedliche `name`-Attribute haben?
2. Teste: Versuche, das Formular ohne Checkbox "AGB akzeptieren" abzusenden. Was passiert?
3. Öffne das Formular auf einem Smartphone (oder simuliere es mit DevTools). Wie unterscheiden sich die Tastaturen bei `type="email"` und `type="tel"`?
4. Warum ist eine leere erste Option (`<option value="">`) bei Dropdowns wichtig?
5. Erstelle ein Radio-Button mit `checked` und ein zweites mit `checked` in der gleichen Gruppe. Was passiert?

---

## Weiterführende Links

- [MDN: `<input type="radio">`](https://developer.mozilla.org/de/docs/Web/HTML/Element/input/radio)
- [MDN: `<input type="checkbox">`](https://developer.mozilla.org/de/docs/Web/HTML/Element/input/checkbox)
- [MDN: `<select>` – Dropdown-Menüs](https://developer.mozilla.org/de/docs/Web/HTML/Element/select)
- [HTML5 Input Types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types)
- [W3C: Accessible Forms](https://www.w3.org/WAI/tutorials/forms/)

---

**Geschätzte Zeit:** 40-45 Minuten  
**Nächster Schritt:** In Auftrag 3 erstellst du ein Feedback-Formular mit fortgeschrittenen Validierungen!
