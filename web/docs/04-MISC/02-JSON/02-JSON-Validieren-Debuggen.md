# Auftrag 2: JSON validieren und debuggen

## Ziel

Du lernst, JSON-Fehler zu erkennen, zu analysieren und zu beheben. Du verstehst typische Fehlermeldungen, nutzt Validierungs-Tools und entwickelst systematische Debugging-Strategien für JSON-Daten.

## Beschreibung

JSON ist strikt – ein einziger Fehler macht die ganze Datei ungültig. In der Praxis wirst du oft mit JSON-Daten arbeiten, die Fehler enthalten oder unerwartete Strukturen haben. Professionelle Entwickler nutzen systematische Methoden, um JSON-Fehler schnell zu finden und zu beheben.

In diesem Auftrag analysierst du fehlerhafte JSON-Dateien, lernst verschiedene Validierungs-Tools kennen und entwickelst ein System zum systematischen Debugging von JSON-Strukturen.

---

### Teil 1: Häufige JSON-Fehler erkennen (20 Min)

Erstelle eine neue Datei **`fehler-beispiele.json`**. Diese Datei enthält ABSICHTLICH Fehler – deine Aufgabe ist es, sie zu finden und zu korrigieren.

**Datei 1: `fehler-beispiele.json` (fehlerhaft):**

```json
{
  'name': 'Sarah Müller',
  "alter": 18,
  "beruf": "Informatikerin EFZ",
  "skills": ["HTML", "CSS", "JavaScript",],
  hobbies: ['Programmieren', 'Fotografie'],
  "adresse": {
    "ort": "Bern",
    "plz": 3000,
  },
  "projekt": {
    "titel": "Portfolio",
    "status": "in Arbeit"
    "fortschritt": 75
  },
  "email": undefined,
  "telefon": null,
  "istAktiv": true,
  // Kommentar: Hier ist ein Kommentar
  "notiz": "Das ist ein Test",
}
```

**Deine Aufgabe:**

1. **Kopiere den obigen Code in eine neue Datei `fehler-beispiele.json`**
2. **Validiere die Datei:**
   - Öffne [jsonlint.com](https://jsonlint.com)
   - Kopiere den Code hinein
   - Klicke "Validate JSON"
3. **Notiere alle Fehler in einer Liste**
4. **Korrigiere die Fehler einen nach dem anderen**
5. **Validiere erneut, bis die Datei gültig ist**

**Erstelle eine Fehlerliste:**

Erstelle eine Datei `fehler-analyse.md` und dokumentiere jeden Fehler:

```markdown
# JSON-Fehleranalyse

## Gefundene Fehler in fehler-beispiele.json

### Fehler 1: Einfache Anführungszeichen
- **Zeile:** 2
- **Problem:** `'name': 'Sarah Müller'`
- **Lösung:** Doppelte Anführungszeichen verwenden: `"name": "Sarah Müller"`
- **Regel:** JSON erlaubt nur doppelte Anführungszeichen für Strings

### Fehler 2: Trailing Comma in Array
- **Zeile:** 5
- **Problem:** `["HTML", "CSS", "JavaScript",]`
- **Lösung:** Komma nach letztem Element entfernen: `["HTML", "CSS", "JavaScript"]`
- **Regel:** Kein Komma nach dem letzten Element in Arrays/Objekten

### Fehler 3: Schlüssel ohne Anführungszeichen
- **Zeile:** 6
- **Problem:** `hobbies: ['Programmieren', 'Fotografie']`
- **Lösung:** `"hobbies": ["Programmieren", "Fotografie"]`
- **Regel:** Alle Schlüssel müssen in doppelten Anführungszeichen stehen

(Fahre mit allen weiteren Fehlern fort...)
```

**Tipps zur Fehlersuche:**
- Nutze [jsonlint.com](https://jsonlint.com) - es zeigt dir die **erste** Fehlerzeile an
- Korrigiere **immer nur einen Fehler** und validiere erneut
- VS Code zeigt JSON-Fehler mit roten Wellenlinien
- Die Browser-Console zeigt bei `JSON.parse()` genau an, wo der Fehler ist

**Fragen zum Selbstlernen:**
- Welche Anführungszeichen sind in JSON erlaubt? → [JSON.org](https://www.json.org/json-de.html)
- Was ist ein "Trailing Comma"? → Google: "JSON trailing comma"
- Was ist der Unterschied zwischen `undefined` und `null`? → [MDN: null vs undefined](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/null)

---

### Teil 2: JSON-Validierungs-Tools nutzen (15 Min)

Teste verschiedene Tools zur JSON-Validierung und finde heraus, welches dir am besten gefällt.

**Tool 1: JSONLint (Online)**

1. Öffne [jsonlint.com](https://jsonlint.com)
2. Füge diesen fehlerhaften JSON-Code ein:

```json
{
  "name": "Test",
  "alter": 25,
  "skills": ["HTML", "CSS",]
}
```

3. Klicke "Validate JSON"
4. **Notiere:** Was zeigt die Fehlermeldung?
5. Korrigiere den Fehler
6. Validiere erneut

**Tool 2: VS Code JSON-Validierung**

1. Öffne VS Code
2. Erstelle eine neue Datei `test.json`
3. Füge fehlerhaften JSON-Code ein
4. **Beobachte:** Welche Fehler unterstreicht VS Code rot?
5. Fahre mit der Maus über die rote Wellenlinie
6. **Notiere:** Was steht in der Fehlermeldung?

**Tool 3: Browser DevTools**

Erstelle eine Datei `json-validator.html`:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>JSON Validator</title>
    <style>
        body {
            font-family: 'Aptos', Arial, sans-serif;
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
        }
        
        textarea {
            width: 100%;
            height: 300px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            padding: 10px;
            border: 2px solid #B3D9EE;
            border-radius: 4px;
        }
        
        button {
            background: #005A9C;
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
        }
        
        button:hover {
            background: #004578;
        }
        
        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 4px;
            font-family: monospace;
        }
        
        .success {
            background: #d4edda;
            color: #155724;
            border: 2px solid #c3e6cb;
        }
        
        .error {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #f5c6cb;
        }
        
        .formatted {
            background: #f8f9fa;
            border: 2px solid #B3D9EE;
            padding: 15px;
            overflow-x: auto;
        }
        
        pre {
            margin: 0;
        }
    </style>
</head>
<body>
    <h1>JSON Validator & Formatter</h1>
    <p>Füge deinen JSON-Code ein und validiere ihn:</p>
    
    <textarea id="jsonInput" placeholder='{"name": "Beispiel", "wert": 123}'></textarea>
    
    <button onclick="validateJSON()">JSON validieren</button>
    <button onclick="formatJSON()">JSON formatieren</button>
    <button onclick="clearAll()">Leeren</button>
    
    <div id="result"></div>
    
    <script>
        function validateJSON() {
            const input = document.getElementById('jsonInput').value;
            const resultDiv = document.getElementById('result');
            
            if (!input.trim()) {
                resultDiv.innerHTML = '<div class="error">Bitte JSON-Code eingeben!</div>';
                return;
            }
            
            try {
                // JSON parsen
                const parsed = JSON.parse(input);
                
                // Erfolg
                resultDiv.innerHTML = `
                    <div class="success">
                        <strong>✓ Gültiges JSON!</strong>
                        <br>Typ: ${Array.isArray(parsed) ? 'Array' : typeof parsed}
                        <br>Eigenschaften: ${Object.keys(parsed).length}
                    </div>
                `;
                
                console.log('Geparste Daten:', parsed);
                
            } catch (error) {
                // Fehler
                resultDiv.innerHTML = `
                    <div class="error">
                        <strong>✗ Ungültiges JSON!</strong>
                        <br><br><strong>Fehler:</strong> ${error.message}
                        <br><br><strong>Tipp:</strong> Prüfe Anführungszeichen, Kommas und Klammern.
                    </div>
                `;
                
                console.error('JSON-Fehler:', error);
            }
        }
        
        function formatJSON() {
            const input = document.getElementById('jsonInput').value;
            const resultDiv = document.getElementById('result');
            
            try {
                const parsed = JSON.parse(input);
                const formatted = JSON.stringify(parsed, null, 2);
                
                // Formatiert anzeigen
                resultDiv.innerHTML = `
                    <div class="success">
                        <strong>✓ Formatiert!</strong>
                    </div>
                    <div class="formatted">
                        <pre>${escapeHtml(formatted)}</pre>
                    </div>
                `;
                
                // Auch ins Textfeld schreiben
                document.getElementById('jsonInput').value = formatted;
                
            } catch (error) {
                resultDiv.innerHTML = `
                    <div class="error">
                        <strong>✗ Fehler beim Formatieren!</strong>
                        <br><br>${error.message}
                    </div>
                `;
            }
        }
        
        function clearAll() {
            document.getElementById('jsonInput').value = '';
            document.getElementById('result').innerHTML = '';
        }
        
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }
        
        // Beispiel-JSON einfügen beim Laden
        window.onload = function() {
            document.getElementById('jsonInput').value = `{
  "name": "Sarah Müller",
  "alter": 18,
  "skills": ["HTML", "CSS", "JavaScript"]
}`;
        };
    </script>
</body>
</html>
```

**Teste deinen Validator:**
1. Öffne `json-validator.html` im Browser
2. Füge verschiedene JSON-Beispiele ein
3. Teste sowohl gültige als auch ungültige JSON-Daten
4. Nutze die Formatierungs-Funktion

---

### Teil 3: Systematisches JSON-Debugging (25 Min)

**Aufgabe:** Erstelle eine Datei **`portfolio-data.json`** und füge folgenden Code ein.

**ACHTUNG:** Dieser Code enthält **mindestens 8 Fehler**! Finde und korrigiere sie alle.

```json
{
  "owner": {
    "name": "Sarah Müller",
    "email": "sarah@example.com"
    "rolle": "Informatikerin"
  },
  "projekte": [
    {
      "id": 1,
      "titel": "Portfolio-Website",
      "technologien": ["HTML", "CSS", "JavaScript"],
      "status": "in Arbeit",
      "team": [
        {
          "name": "Sarah",
          "rolle": "Entwicklerin"
        },
        {
          "name": "Tom",
          "rolle": "Designer",
        }
      ]
    },
    {
      "id": 2,
      "titel": "To-Do App",
      "technologien": ['React', 'Node.js'],
      "status": "geplant",
      "team": []
    },
  ],
  "statistik": {
    "projekte": 2,
    "abgeschlossen": 0,
    "inArbeit": 1,
    "zeitTotal": 45,
  }
}
```

**Hinweis:** Nutze systematisches Vorgehen! Korrigiere einen Fehler nach dem anderen.

**Debugging-Strategie:**

1. **Erste Validierung**
   - Kopiere JSON in JSONLint
   - Notiere ERSTEN Fehler
   - Korrigiere NUR diesen einen Fehler
   - Validiere erneut
   - Wiederhole, bis alles gültig ist

2. **Fehler-Log erstellen**

Erstelle `debugging-log.md`:

```markdown
# Debugging-Log: portfolio-data.json

## Debugging-Session: 2025-11-18

### Iteration 1
- **Fehler gefunden:** Fehlendes Komma nach "email" (Zeile 4)
- **Zeile:** 4
- **Fehlermeldung:** "Unexpected token 'r'"
- **Aktion:** Komma hinzugefügt
- **Status nach Fix:** Noch Fehler vorhanden

### Iteration 2
- **Fehler gefunden:** Trailing Comma in team-Array (Zeile 24)
- **Zeile:** 24
- **Fehlermeldung:** "Unexpected token '}'"
- **Aktion:** Komma entfernt
- **Status nach Fix:** Noch Fehler vorhanden

(Fahre mit allen Iterationen fort...)

### Zusammenfassung
- **Gesamt gefundene Fehler:** X
- **Zeit benötigt:** X Minuten
- **Häufigster Fehlertyp:** ...
- **Gelernt:** ...
```

3. **Selbstreflexion nach dem Debugging:**

Erstelle eine Datei `meine-fehleranalyse.md` und beantworte:

```markdown
# Meine JSON-Fehleranalyse

## Welche Fehlertypen habe ich gefunden?
- [ ] Einfache statt doppelte Anführungszeichen
- [ ] Fehlende Anführungszeichen bei Schlüsseln
- [ ] Trailing Commas
- [ ] Fehlende Kommas zwischen Elementen
- [ ] undefined statt null
- [ ] Andere: ...

## Welcher Fehler war am schwierigsten zu finden?
...

## Was habe ich gelernt?
...

## Wie kann ich solche Fehler in Zukunft vermeiden?
...
```

**Hilfreiche Ressourcen:**
- [JSONLint](https://jsonlint.com) - Zeigt Fehlerzeile und -position
- [Common JSON Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/JSON_bad_parse) - Häufige Fehlermeldungen erklärt

---

### Teil 4: JSON-Schema und Validierung (Bonus, 15 Min)

Erstelle eine Datei **`projekt-schema.json`** die definiert, wie ein gültiges Projekt aussehen muss:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Projekt",
  "type": "object",
  "required": ["id", "titel", "status"],
  "properties": {
    "id": {
      "type": "integer",
      "minimum": 1,
      "description": "Eindeutige Projekt-ID"
    },
    "titel": {
      "type": "string",
      "minLength": 3,
      "maxLength": 100,
      "description": "Projekt-Titel"
    },
    "beschreibung": {
      "type": "string",
      "description": "Projekt-Beschreibung"
    },
    "technologien": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "description": "Verwendete Technologien"
    },
    "status": {
      "type": "string",
      "enum": ["geplant", "in Arbeit", "abgeschlossen", "pausiert"],
      "description": "Aktueller Status"
    },
    "fortschritt": {
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "description": "Fortschritt in Prozent"
    },
    "startDatum": {
      "type": "string",
      "format": "date",
      "description": "Startdatum (YYYY-MM-DD)"
    }
  }
}
```

**Teste das Schema online:**
1. Öffne [jsonschemavalidator.net](https://www.jsonschemavalidator.net/)
2. Füge dein Schema links ein
3. Füge Projekt-Daten rechts ein:

```json
{
  "id": 1,
  "titel": "Portfolio",
  "technologien": ["HTML", "CSS"],
  "status": "in Arbeit",
  "fortschritt": 75,
  "startDatum": "2025-09-01"
}
```

4. Schaue, ob die Validierung erfolgreich ist
5. Teste mit ungültigen Daten (z.B. `"status": "fertig"` → nicht im enum!)

---

## Erfolgskriterien

- [ ] Alle Fehler in `fehler-beispiele.json` gefunden und korrigiert
- [ ] `fehler-analyse.md` erstellt mit Dokumentation aller Fehler
- [ ] Korrigierte Version validiert und gültig
- [ ] `json-validator.html` erstellt und funktionsfähig
- [ ] Mindestens 3 verschiedene JSON-Validierungs-Tools getestet
- [ ] `portfolio-data.json` Fehler systematisch gefunden und behoben
- [ ] `debugging-log.md` erstellt mit vollständiger Dokumentation
- [ ] Fehler nach Kategorien sortiert und analysiert
- [ ] JSON-Schema verstanden und getestet (Bonus)

---

## Tipps

**Systematisches Debugging:**
1. Immer NUR EINEN Fehler aufs Mal beheben
2. Nach jeder Änderung neu validieren
3. Fehler dokumentieren (hilft beim Lernen)
4. Von oben nach unten arbeiten

**Häufige Fehlerquellen:**
- Trailing Commas (letztes Element in Array/Objekt)
- Einfache vs. doppelte Anführungszeichen
- Fehlende Kommas zwischen Elementen
- Nicht geschlossene Klammern
- undefined statt null

**VS Code Shortcuts:**
- `Shift + Alt + F` → JSON automatisch formatieren
- `Ctrl + Shift + P` → "Format Document" suchen
- Bracket Pair Colorization aktivieren (Settings)

**Browser DevTools:**
- Wenn `JSON.parse()` einen Fehler wirft, steht die Position im Error
- `JSON.parse('{"test": }')` → "Unexpected token }" bei Position X

---

## Reflexionsfragen

1. **Welches JSON-Validierungs-Tool findest du am nützlichsten und warum?**  
   *Vergleiche: Online-Tools, VS Code, Browser DevTools, JSON-Schema*

2. **Warum ist es wichtig, JSON-Fehler systematisch zu beheben (einer nach dem anderen)?**  
   *Was passiert, wenn du versuchst, mehrere Fehler gleichzeitig zu korrigieren?*

3. **Erstelle eine persönliche Checkliste: Welche JSON-Fehler machst du am häufigsten?**  
   *Wie kannst du sie in Zukunft vermeiden?*

4. **Experimentiere: Kann ein JSON-Objekt KOMPLETT leer sein?**  
   *Teste: Ist `{}` gültiges JSON? Ist `[]` gültig? Ist `null` gültig? Ist `""` gültig?*

5. **Was ist der Vorteil von JSON-Schema?**  
   *Recherchiere: Wo wird JSON-Schema in der Praxis eingesetzt?*

---

## Weiterführende Links

**JSON-Validierung:**
- [JSONLint](https://jsonlint.com/) – Standard-Validator
- [JSON Formatter & Validator](https://jsonformatter.curiousconcept.com/)
- [JSON Editor Online](https://jsoneditoronline.org/)

**JSON-Schema:**
- [JSON Schema](https://json-schema.org/) – Offizielle Dokumentation
- [JSON Schema Validator](https://www.jsonschemavalidator.net/)
- [Understanding JSON Schema](https://json-schema.org/understanding-json-schema/)

**Debugging-Tools:**
- [VS Code JSON Extension](https://marketplace.visualstudio.com/items?itemName=ZainChen.json)
- [Prettier](https://prettier.io/) – Code-Formatter mit JSON-Support

**Fehlersuche:**
- [MDN: JSON.parse() Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/JSON_bad_parse)
- [Common JSON Mistakes](https://jsonlint.com/json-syntax)

---

**⏱️ Geschätzte Zeit:** 60-70 Minuten  
**📦 Nächster Schritt:** Auftrag 3 – JSON-API-Daten verarbeiten
