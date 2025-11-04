# Storyboard: HTML Formulare

## Video-Übersicht
- **Gesamtdauer:** ca. 7-8 Minuten
- **Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ
- **Lernziele:** Grundlagen von HTML-Formularen, Input-Typen, Validierung

---

## Szene 1: Einführung – Was sind Formulare?

**Sprechertext:** „Formulare ermöglichen die Interaktion zwischen Nutzern und Webseiten. Jedes Mal, wenn du dich irgendwo anmeldest, etwas suchst oder eine Nachricht sendest, nutzt du ein Formular."

**Bildschirmdarstellung:** Beispiele von bekannten Formularen zeigen (Google-Suche, Login-Seite, Kontaktformular)

**Dauer:** 30 Sekunden

---

## Szene 2: Das `<form>`-Element – Die Basis

**Sprechertext:** „Jedes Formular beginnt mit dem `<form>`-Tag. Das `action`-Attribut bestimmt, wohin die Daten gesendet werden, und `method` legt fest, wie sie übertragen werden – meist GET oder POST."

**Bildschirmdarstellung:** Code-Editor zeigt:
```html
<form action="/kontakt" method="post">
    <!-- Hier kommen die Eingabefelder -->
</form>
```

**Dauer:** 35 Sekunden

---

## Szene 3: Textfelder – `<input type="text">`

**Sprechertext:** „Das häufigste Eingabefeld ist das Textfeld. Mit `type='text'` erstellst du ein einzeiliges Eingabefeld. Das `name`-Attribut identifiziert das Feld, und `placeholder` zeigt einen Hinweistext."

**Bildschirmdarstellung:** 
```html
<label for="vorname">Vorname:</label>
<input type="text" id="vorname" name="vorname" placeholder="z.B. Anna">
```
Browser-Vorschau: Eingabefeld wird gezeigt

**Dauer:** 40 Sekunden

---

## Szene 4: Labels – Beschriftung für Barrierefreiheit

**Sprechertext:** „Jedes Eingabefeld braucht ein Label. Das `<label>`-Tag beschreibt das Feld und verbindet sich über das `for`-Attribut mit der ID des Inputs. Das hilft Screenreadern und macht das Feld anklickbar."

**Bildschirmdarstellung:** Klick auf Label fokussiert das Eingabefeld

**Dauer:** 35 Sekunden

---

## Szene 5: Verschiedene Input-Typen

**Sprechertext:** „HTML5 bietet viele Input-Typen: `email` validiert E-Mail-Adressen, `tel` für Telefonnummern, `date` öffnet einen Kalender, und `number` erlaubt nur Zahlen."

**Bildschirmdarstellung:** Vier Eingabefelder nebeneinander:
```html
<input type="email" placeholder="E-Mail">
<input type="tel" placeholder="Telefon">
<input type="date">
<input type="number" min="1" max="100">
```

**Dauer:** 40 Sekunden

---

## Szene 6: Mehrzeilige Texte – `<textarea>`

**Sprechertext:** „Für längere Texte wie Nachrichten nutzt du `<textarea>`. Mit `rows` und `cols` bestimmst du die Größe, aber das übernimmt später meist CSS."

**Bildschirmdarstellung:**
```html
<label for="nachricht">Deine Nachricht:</label>
<textarea id="nachricht" name="nachricht" rows="5" cols="40"></textarea>
```

**Dauer:** 30 Sekunden

---

## Szene 7: Checkboxen – Mehrfachauswahl

**Sprechertext:** „Mit Checkboxen können Nutzer mehrere Optionen gleichzeitig auswählen. Jede Checkbox braucht ein eigenes Label und einen `value`."

**Bildschirmdarstellung:**
```html
<input type="checkbox" id="html" name="skills" value="html">
<label for="html">HTML</label>

<input type="checkbox" id="css" name="skills" value="css">
<label for="css">CSS</label>
```

**Dauer:** 35 Sekunden

---

## Szene 8: Radio-Buttons – Einzelauswahl

**Sprechertext:** „Radio-Buttons funktionieren wie Checkboxen, aber nur eine Option kann ausgewählt werden. Alle Buttons der gleichen Gruppe brauchen den gleichen `name`."

**Bildschirmdarstellung:**
```html
<input type="radio" id="anfaenger" name="level" value="anfaenger">
<label for="anfaenger">Anfänger</label>

<input type="radio" id="fortgeschritten" name="level" value="fortgeschritten">
<label for="fortgeschritten">Fortgeschritten</label>
```

**Dauer:** 35 Sekunden

---

## Szene 9: Dropdown-Menüs – `<select>`

**Sprechertext:** „Mit `<select>` und `<option>` erstellst du Dropdown-Menüs. Das spart Platz bei vielen Auswahlmöglichkeiten."

**Bildschirmdarstellung:**
```html
<label for="lehrjahr">Lehrjahr:</label>
<select id="lehrjahr" name="lehrjahr">
    <option value="1">1. Lehrjahr</option>
    <option value="2">2. Lehrjahr</option>
    <option value="3">3. Lehrjahr</option>
</select>
```

**Dauer:** 30 Sekunden

---

## Szene 10: Buttons – Absenden und Zurücksetzen

**Sprechertext:** „Mit `<button type='submit'>` sendest du das Formular ab. `type='reset'` löscht alle Eingaben. Verwende immer aussagekräftige Button-Texte."

**Bildschirmdarstellung:**
```html
<button type="submit">Absenden</button>
<button type="reset">Zurücksetzen</button>
```

**Dauer:** 30 Sekunden

---

## Szene 11: Pflichtfelder – `required`

**Sprechertext:** „Mit dem `required`-Attribut machst du Felder zur Pflicht. Der Browser verhindert das Absenden, wenn Pflichtfelder leer sind."

**Bildschirmdarstellung:** Versuch, Formular ohne ausgefülltes Pflichtfeld abzusenden → Browser zeigt Fehlermeldung

**Dauer:** 30 Sekunden

---

## Szene 12: Formular-Validierung

**Sprechertext:** „HTML validiert automatisch E-Mails, URLs und Zahlen. Mit `pattern` kannst du eigene Validierungen definieren, zum Beispiel für Postleitzahlen oder Telefonnummern."

**Bildschirmdarstellung:**
```html
<input type="email" required>
<input type="text" pattern="[0-9]{4}" placeholder="PLZ (4 Ziffern)">
```

**Dauer:** 35 Sekunden

---

## Szene 13: Fieldset & Legend – Formulare gruppieren

**Sprechertext:** „Mit `<fieldset>` gruppierst du zusammengehörige Felder. `<legend>` gibt der Gruppe einen Titel. Das ist wichtig für komplexe Formulare."

**Bildschirmdarstellung:**
```html
<fieldset>
    <legend>Persönliche Daten</legend>
    <label>Name: <input type="text"></label>
    <label>E-Mail: <input type="email"></label>
</fieldset>
```

**Dauer:** 30 Sekunden

---

## Szene 14: Testing & Best Practices

**Sprechertext:** „Teste dein Formular: Funktionieren Validierungen? Sind alle Felder mit Tastatur erreichbar? Nutze die DevTools, um Formulardaten zu inspizieren."

**Bildschirmdarstellung:** DevTools öffnen → Network-Tab → Formular absenden → POST-Daten anzeigen

**Dauer:** 35 Sekunden

---

## Produktionshinweise

### Benötigte Ressourcen:
- Code-Editor (VS Code)
- Browser (Chrome/Firefox mit DevTools)
- Beispiel-Formulare von bekannten Websites (Screenshots)

### Visueller Stil:
- Split-Screen: Code links, Browser-Vorschau rechts
- Highlighting von wichtigen Attributen im Code
- Cursor-Bewegungen langsam und deutlich
- Fehlermeldungen des Browsers zeigen

### Nachbearbeitung:
- Übergänge zwischen Szenen: 1 Sekunde
- Zoom auf wichtige Code-Teile
- Text-Overlays für wichtige Begriffe (z.B. "required", "pattern")
- Zusammenfassungs-Folie am Ende mit allen Input-Typen

### Qualitätskontrolle:
- Alle Code-Beispiele funktionieren
- Keine Tippfehler im Code
- Audio ist klar und verständlich
- Geschwindigkeit ist angemessen für Anfänger
