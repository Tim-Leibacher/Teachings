# Auftrag 4 (Optional): Fortgeschrittene Formular-Techniken

## Ziel
Du lernst fortgeschrittene Formular-Features kennen: Datalist für Autocomplete, Multiple File Uploads, Color/Date/Time-Picker und Custom Validierung. Dieses Wissen macht dich fit für komplexe Webanwendungen.

## Beschreibung

Dieser optionale Auftrag vertieft dein Formular-Wissen mit Features, die in modernen Webapps Standard sind. Du erstellst ein "Profil-Editor"-Formular mit vielen fortgeschrittenen Input-Typen.

---

## Teil 1: Datalist – Autocomplete mit Vorschlägen (15 Min)

```html
<fieldset>
    <legend>Programmiersprachen-Kenntnisse</legend>
    
    <label for="sprache1">Hauptsprache:</label>
    <input type="text" 
           id="sprache1" 
           name="sprache1" 
           list="programmiersprachen" 
           placeholder="z.B. JavaScript">
    
    <datalist id="programmiersprachen">
        <option value="HTML">
        <option value="CSS">
        <option value="JavaScript">
        <option value="Python">
        <option value="Java">
        <option value="C#">
        <option value="PHP">
        <option value="Ruby">
        <option value="Swift">
        <option value="Kotlin">
    </datalist>
    
    <label for="sprache2">Weitere Sprache:</label>
    <input type="text" 
           id="sprache2" 
           name="sprache2" 
           list="programmiersprachen" 
           placeholder="z.B. Python">
</fieldset>
```

**Wie funktioniert `<datalist>`?**
- Verknüpfung über `list="id"`
- Zeigt Vorschläge beim Tippen
- Nutzer kann auch freie Eingabe machen
- Besser als `<select>`, wenn viele Optionen existieren

---

## Teil 2: Color Picker & Date/Time Inputs (15 Min)

```html
<fieldset>
    <legend>Personalisierung</legend>
    
    <label for="lieblingsfarbe">Deine Lieblingsfarbe:</label>
    <input type="color" 
           id="lieblingsfarbe" 
           name="lieblingsfarbe" 
           value="#3498db">
    
    <label for="geburtstag">Geburtstag:</label>
    <input type="date" 
           id="geburtstag" 
           name="geburtstag" 
           min="1950-01-01" 
           max="2010-12-31" 
           required>
    
    <label for="startzeit">Bevorzugte Arbeitszeit (von):</label>
    <input type="time" 
           id="startzeit" 
           name="startzeit" 
           min="06:00" 
           max="12:00" 
           value="09:00">
    
    <label for="endzeit">Bevorzugte Arbeitszeit (bis):</label>
    <input type="time" 
           id="endzeit" 
           name="endzeit" 
           min="12:00" 
           max="20:00" 
           value="18:00">
    
    <label for="termin">Nächster Projekt-Termin:</label>
    <input type="datetime-local" 
           id="termin" 
           name="termin">
</fieldset>
```

**Neue Input-Typen:**
- `type="color"` → Öffnet Farbwähler (Browser-native)
- `type="time"` → Zeitauswahl
- `type="datetime-local"` → Datum + Uhrzeit kombiniert
- Alle unterstützen `min` und `max` für Einschränkungen

---

## Teil 3: Multiple File Upload (10 Min)

```html
<fieldset>
    <legend>Dokumente hochladen</legend>
    
    <label for="profilbild">Profilbild:</label>
    <input type="file" 
           id="profilbild" 
           name="profilbild" 
           accept="image/png, image/jpeg" 
           required>
    <small>Max. 5 MB, nur JPG oder PNG</small>
    
    <label for="lebenslauf">Lebenslauf (PDF):</label>
    <input type="file" 
           id="lebenslauf" 
           name="lebenslauf" 
           accept=".pdf">
    
    <label for="zeugnisse">Arbeitszeugnisse (mehrere möglich):</label>
    <input type="file" 
           id="zeugnisse" 
           name="zeugnisse" 
           accept=".pdf,.doc,.docx" 
           multiple>
    <small>Mehrere Dateien auswählbar</small>
</fieldset>
```

**File Upload Attribute:**
- `accept` = Erlaubte Dateitypen (MIME-Type oder Extension)
- `multiple` = Mehrere Dateien gleichzeitig auswählbar
- Später mit JavaScript: Dateivorschau, Größenvalidierung

---

## Teil 4: Hidden Inputs & Readonly Fields (10 Min)

```html
<fieldset>
    <legend>System-Informationen</legend>
    
    <!-- Hidden Fields für Server-seitige Verarbeitung -->
    <input type="hidden" name="user_id" value="12345">
    <input type="hidden" name="form_version" value="2.1">
    <input type="hidden" name="timestamp" value="2025-11-04T10:30:00">
    
    <label for="user-email">Deine E-Mail (nicht änderbar):</label>
    <input type="email" 
           id="user-email" 
           name="user-email" 
           value="max.muster@example.ch" 
           readonly>
    <small>Du kannst deine E-Mail nicht selbst ändern. Kontaktiere den Support.</small>
    
    <label for="mitglied-seit">Mitglied seit:</label>
    <input type="date" 
           id="mitglied-seit" 
           name="mitglied-seit" 
           value="2024-08-01" 
           disabled>
    <small>Dieses Feld ist deaktiviert und wird nicht übermittelt.</small>
</fieldset>
```

**Unterschied `readonly` vs. `disabled`:**
- `readonly` = Feld ist sichtbar, wird beim Submit übermittelt, aber nicht änderbar
- `disabled` = Feld ist ausgegraut, wird NICHT beim Submit übermittelt

---

## Teil 5: Custom Validierung mit Pattern & Title (15 Min)

```html
<fieldset>
    <legend>Erweiterte Validierung</legend>
    
    <label for="iban">IBAN (Schweiz):</label>
    <input type="text" 
           id="iban" 
           name="iban" 
           pattern="CH[0-9]{2} ?[0-9]{4} ?[0-9]{4} ?[0-9]{4} ?[0-9]{4} ?[0-9]{1}" 
           title="Format: CH12 3456 7890 1234 5678 9"
           placeholder="CH12 3456 7890 1234 5678 9">
    
    <label for="username">Benutzername (nur Kleinbuchstaben, 4-16 Zeichen):</label>
    <input type="text" 
           id="username" 
           name="username" 
           pattern="[a-z]{4,16}" 
           title="Nur Kleinbuchstaben, 4-16 Zeichen"
           placeholder="z.B. maxmuster">
    
    <label for="passwort">Passwort (min. 8 Zeichen, mind. 1 Zahl):</label>
    <input type="password" 
           id="passwort" 
           name="passwort" 
           pattern="(?=.*\d).{8,}" 
           title="Mindestens 8 Zeichen und mindestens 1 Zahl"
           required>
    
    <label for="passwort-wiederholen">Passwort wiederholen:</label>
    <input type="password" 
           id="passwort-wiederholen" 
           name="passwort-wiederholen" 
           required>
    <small>Wichtig: HTML kann nicht prüfen, ob Passwörter übereinstimmen – das macht man mit JavaScript!</small>
</fieldset>
```

**Komplexe Regex-Patterns:**
- `(?=.*\d).{8,}` = Mindestens 8 Zeichen UND mindestens eine Zahl
- `[a-z]{4,16}` = Nur Kleinbuchstaben, 4-16 Zeichen
- Teste Patterns auf [regex101.com](https://regex101.com)

---

## Teil 6: Formular-Gruppierung mit Nested Fieldsets (10 Min)

```html
<fieldset>
    <legend>Adresse</legend>
    
    <fieldset>
        <legend>Wohnadresse</legend>
        
        <label for="strasse">Strasse:</label>
        <input type="text" id="strasse" name="strasse" required>
        
        <label for="hausnummer">Hausnummer:</label>
        <input type="text" id="hausnummer" name="hausnummer" size="5" required>
        
        <label for="plz-wohnung">PLZ:</label>
        <input type="text" id="plz-wohnung" name="plz-wohnung" pattern="[0-9]{4}" required>
        
        <label for="ort">Ort:</label>
        <input type="text" id="ort" name="ort" required>
    </fieldset>
    
    <input type="checkbox" id="rechnungsadresse-anders" name="rechnungsadresse-anders">
    <label for="rechnungsadresse-anders">Rechnungsadresse weicht ab</label>
    
    <fieldset id="rechnungsadresse-fields" disabled>
        <legend>Rechnungsadresse</legend>
        
        <label for="r-strasse">Strasse:</label>
        <input type="text" id="r-strasse" name="r-strasse">
        
        <label for="r-hausnummer">Hausnummer:</label>
        <input type="text" id="r-hausnummer" name="r-hausnummer" size="5">
        
        <label for="r-plz">PLZ:</label>
        <input type="text" id="r-plz" name="r-plz" pattern="[0-9]{4}">
        
        <label for="r-ort">Ort:</label>
        <input type="text" id="r-ort" name="r-ort">
    </fieldset>
</fieldset>
```

**Nested Fieldsets:**
- Fieldsets können verschachtelt werden
- Praktisch für komplexe Formulare
- Mit `disabled` auf dem ganzen Fieldset werden alle Felder darin deaktiviert

---

## Teil 7: Accessibility & ARIA (10 Min)

```html
<fieldset>
    <legend>Barrierefreiheit</legend>
    
    <label for="screenreader-info">Zusätzliche Informationen für Screenreader:</label>
    <input type="text" 
           id="screenreader-info" 
           name="screenreader-info" 
           aria-describedby="screenreader-help">
    <small id="screenreader-help">Dieser Text wird von Screenreadern vorgelesen und hilft Nutzern mit Sehbehinderung.</small>
    
    <label for="pflichtfeld-beispiel">Pflichtfeld mit ARIA:</label>
    <input type="text" 
           id="pflichtfeld-beispiel" 
           name="pflichtfeld-beispiel" 
           required 
           aria-required="true" 
           aria-invalid="false">
    
    <div role="group" aria-labelledby="kontaktmethode-label">
        <p id="kontaktmethode-label">Bevorzugte Kontaktmethode:</p>
        <input type="radio" id="kontakt-email" name="kontaktmethode" value="email">
        <label for="kontakt-email">E-Mail</label>
        
        <input type="radio" id="kontakt-telefon" name="kontaktmethode" value="telefon">
        <label for="kontakt-telefon">Telefon</label>
        
        <input type="radio" id="kontakt-post" name="kontaktmethode" value="post">
        <label for="kontakt-post">Post</label>
    </div>
</fieldset>
```

**ARIA-Attribute:**
- `aria-describedby` = Verknüpft Hilfstext mit Input
- `aria-required` = Informiert Screenreader über Pflichtfelder
- `aria-invalid` = Zeigt an, ob Feld ungültig ist (wird mit JavaScript gesetzt)
- `role="group"` und `aria-labelledby` = Gruppiert Radio-Buttons semantisch

---

## Teil 8: Submit-Button mit Zusatzfunktionen (5 Min)

```html
<fieldset>
    <legend>Absenden</legend>
    
    <button type="submit">Profil speichern</button>
    <button type="submit" formnovalidate>Als Entwurf speichern</button>
    <button type="reset">Alle Änderungen verwerfen</button>
    
    <button type="button" onclick="window.print()">Formular drucken</button>
</fieldset>
```

**Button-Attribute:**
- `formnovalidate` = Überspringt Validierung für diesen Submit-Button
- `type="button"` = Sendet Formular nicht ab, nützlich für JavaScript-Aktionen

---

## Erfolgskriterien

- [ ] Mindestens ein `<datalist>` mit Autocomplete-Vorschlägen ist implementiert
- [ ] Color Picker, Time Picker und Date Picker sind vorhanden
- [ ] Multiple File Upload ist funktionsfähig
- [ ] Hidden Fields und `readonly`/`disabled` Felder sind korrekt eingesetzt
- [ ] Mindestens 3 komplexe Pattern-Validierungen existieren
- [ ] Nested Fieldsets strukturieren das Formular logisch
- [ ] ARIA-Attribute verbessern die Barrierefreiheit
- [ ] Mindestens ein Submit-Button mit `formnovalidate` existiert
- [ ] Alle fortgeschrittenen Input-Typen funktionieren in modernen Browsern

---

## Tipps

- **Browser-Kompatibilität:** Teste alle Input-Typen in verschiedenen Browsern (Chrome, Firefox, Safari)
- `<datalist>` funktioniert nicht in allen alten Browsern – biete Fallback an
- **Profitipp:** Kombiniere `type="file"` mit JavaScript für Live-Vorschau
- Pattern-Validierung ist Client-seitig – immer auch Server-seitig validieren!
- **Testing:** Nutze Browser-DevTools → Elements → Properties, um Input-Zustände zu überprüfen
- ARIA sollte sparsam eingesetzt werden – native HTML-Elemente sind oft besser

---

## Reflexionsfragen

1. Teste `<datalist>` in verschiedenen Browsern. Wie unterscheidet sich das Verhalten?
2. Was ist der Vorteil von `type="color"` gegenüber einem einfachen Text-Input?
3. Erstelle ein Pattern für Schweizer Telefonnummern im Format +41 79 123 45 67. Wie sieht der Regex aus?
4. Wann würdest du `readonly` und wann `disabled` verwenden? Gib je 2 Beispiele.
5. Teste: Lade mehrere Dateien mit `multiple` hoch und inspiziere das Formular in DevTools. Wie werden die Dateien übertragen?
6. Recherchiere: Was ist der Unterschied zwischen `aria-label` und `aria-labelledby`?

---

## Weiterführende Links

**Fortgeschrittene Input-Typen:**
- [MDN: HTML Input Types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
- [MDN: `<datalist>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist)
- [Can I Use: Input Types Support](https://caniuse.com/)

**Validierung & Patterns:**
- [Regex101](https://regex101.com/) – Pattern-Tester
- [HTML5 Pattern Library](https://www.html5pattern.com/)
- [MDN: Constraint Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Constraint_validation)

**Accessibility:**
- [W3C: ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM: Forms and ARIA](https://webaim.org/techniques/forms/advanced)
- [MDN: ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)

**Tools:**
- [WAVE Browser Extension](https://wave.webaim.org/extension/) – Accessibility-Check
- [axe DevTools](https://www.deque.com/axe/devtools/) – Accessibility-Testing

---

## Bonus-Challenges

**Challenge 1: Custom File Upload mit Vorschau**
- Erstelle einen schöneren File-Upload mit eigenem Button-Design
- Zeige eine Vorschau des hochgeladenen Bildes (später mit JavaScript)

**Challenge 2: Dynamische Formular-Felder**
- Erstelle ein Formular, bei dem Felder basierend auf vorherigen Eingaben ein-/ausgeblendet werden
- Beispiel: "Rechnungsadresse anders?" aktiviert zusätzliche Felder

**Challenge 3: Passwort-Stärke-Anzeige**
- Füge visuelle Indikatoren für Passwortstärke hinzu (schwach/mittel/stark)
- Zeige Anforderungen an (8 Zeichen, 1 Zahl, 1 Sonderzeichen)

**Challenge 4: Multi-Step-Formular**
- Erstelle ein mehrstufiges Formular mit "Weiter"- und "Zurück"-Buttons
- Zeige Fortschrittsbalken an (später mit JavaScript)

---

**Geschätzte Zeit:** 60-75 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Nächster Schritt:** Glückwunsch! HTML-Formulare sind abgeschlossen. Weiter mit CSS für schöneres Styling!

---

**Hinweis:** Viele dieser Features funktionieren erst vollständig mit JavaScript (z.B. dynamisches Aktivieren von Feldern, Passwort-Matching, File-Vorschau). Du hast jetzt aber die HTML-Grundlage geschaffen!
