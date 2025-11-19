# 03 – Portfolio mit Sicherheits-Checkliste

**Thema:** Diverses – OWASP Top 3 Sicherheitsrisiken  
**Schwierigkeit:** Mittel  
**Geschätzte Zeit:** 35 Minuten

---

## Lernziel

Du erweiterst deine bestehende Portfolio-Seite um ein Kontaktformular und wendest dabei Sicherheits-Best-Practices an. Du erstellst eine Checkliste, mit der du deine gesamte Website auf Sicherheitslücken überprüfen kannst.

---

## Aufgabenstellung

### Vorbereitung

Öffne dein bestehendes Portfolio-Projekt. Falls du noch keine Portfolio-Seite hast, erstelle eine einfache HTML-Seite mit:
- Header mit deinem Namen
- Abschnitt "Über mich"
- Abschnitt "Projekte"
- Footer mit Copyright

---

### Teil 1: Sicheres Kontaktformular (20 Min)

Erstelle eine neue Seite `kontakt.html` in deinem Portfolio-Ordner mit einem Kontaktformular, das Sicherheits-Best-Practices befolgt.

**Anforderungen an das Formular:**

1. **HTML-Struktur:**
   - Name-Feld (Pflichtfeld, nur Buchstaben und Leerzeichen)
   - E-Mail-Feld (Pflichtfeld, muss gültige E-Mail-Adresse sein)
   - Betreff-Feld (Pflichtfeld, max. 100 Zeichen)
   - Nachricht-Feld (Pflichtfeld, max. 500 Zeichen)
   - Absenden-Button

2. **Client-seitige Validation (JavaScript):**
   - Prüfe alle Felder vor dem Absenden
   - Name darf nur Buchstaben, Umlaute und Leerzeichen enthalten
   - E-Mail muss ein `@` und einen Punkt nach dem `@` enthalten
   - Betreff und Nachricht dürfen keine HTML-Tags enthalten (z.B. `<script>`)
   - Zeige aussagekräftige Fehlermeldungen bei ungültigen Eingaben

3. **Sicherheitskommentare:**
   - Füge im Code Kommentare ein, die erklären, warum bestimmte Prüfungen wichtig sind
   - Erwähne, dass in echten Anwendungen auch serverseitige Validierung nötig ist

**Starter-Code:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kontakt – Mein Portfolio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: Aptos, Arial, sans-serif;
            background: #f5f5f5;
            padding: 20px;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        h1 {
            color: #005a73;
            margin-bottom: 30px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #333;
        }
        
        input, textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            font-family: inherit;
        }
        
        input:focus, textarea:focus {
            outline: none;
            border-color: #4eb9cc;
        }
        
        textarea {
            resize: vertical;
            min-height: 150px;
        }
        
        button {
            background: #005a73;
            color: white;
            padding: 15px 40px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
        }
        
        button:hover {
            background: #004558;
        }
        
        .fehler {
            background: #f5a623;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-top: 10px;
            display: none;
        }
        
        .erfolg {
            background: #4eb9cc;
            color: white;
            padding: 15px;
            border-radius: 5px;
            margin-top: 20px;
            display: none;
        }
        
        .hinweis {
            background: #e7f5ff;
            border-left: 4px solid #4eb9cc;
            padding: 15px;
            margin-top: 20px;
            font-size: 14px;
            color: #005a73;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kontakt</h1>
        
        <form id="kontaktformular">
            <!-- TODO: Füge hier die Formular-Felder ein -->
            
            <button type="submit">Nachricht senden</button>
        </form>
        
        <div class="fehler" id="fehlerBox"></div>
        <div class="erfolg" id="erfolgBox">
            ✓ Nachricht erfolgreich validiert!<br>
            <small>In einer echten Anwendung würde sie jetzt an den Server gesendet.</small>
        </div>
        
        <div class="hinweis">
            🔒 <strong>Sicherheitshinweis:</strong> Dieses Formular validiert Eingaben 
            client-seitig mit JavaScript. In einer produktiven Anwendung muss zusätzlich 
            eine serverseitige Validierung erfolgen, da JavaScript vom Nutzer deaktiviert 
            oder manipuliert werden kann.
        </div>
    </div>
    
    <script>
        // TODO: Implementiere hier die Validierungs-Logik
        
        document.getElementById('kontaktformular').addEventListener('submit', function(event) {
            event.preventDefault();  // Verhindert Standard-Absenden
            
            // TODO: Hole die Werte aus den Formular-Feldern
            // TODO: Validiere jeden Wert
            // TODO: Zeige Fehler oder Erfolg an
        });
    </script>
</body>
</html>
```

**Deine Aufgabe:**
1. Vervollständige den HTML-Code (Formular-Felder)
2. Implementiere die JavaScript-Validierung
3. Teste mit verschiedenen Eingaben (gültig und ungültig)

---

### Teil 2: Sicherheits-Checkliste erstellen (15 Min)

Erstelle eine Datei `sicherheits-checkliste.md` in deinem Portfolio-Ordner. Diese Checkliste hilft dir, deine gesamte Website auf Sicherheitsrisiken zu überprüfen.

**Inhalt der Checkliste:**

```markdown
# Sicherheits-Checkliste für mein Portfolio

**Datum der letzten Prüfung:** [Datum eintragen]

---

## 1. Broken Access Control

- [ ] Gibt es Bereiche, die nur für bestimmte Nutzer zugänglich sein sollten?
- [ ] Falls ja: Wird die Berechtigung serverseitig geprüft?
- [ ] Können Nutzer durch URL-Manipulation auf fremde Daten zugreifen?
- [ ] Gibt es Admin-Bereiche ohne Login-Schutz?

**Status:** [z.B. "Keine Login-Funktion vorhanden, daher nicht relevant"]

---

## 2. Cryptographic Failures

- [ ] Nutzt die Website HTTPS statt HTTP?
- [ ] Werden sensible Daten (Passwörter, persönliche Infos) übertragen?
- [ ] Falls ja: Sind diese Daten verschlüsselt?
- [ ] Werden Passwörter gehashed (z.B. mit bcrypt), nicht im Klartext gespeichert?

**Status:** [z.B. "Noch HTTP, HTTPS bei Deployment einrichten"]

---

## 3. Injection

- [ ] Gibt es Formulare auf der Website?
- [ ] Falls ja: Werden Eingaben validiert (client- und serverseitig)?
- [ ] Werden gefährliche Zeichen (`<`, `>`, `'`, `"`, `;`) behandelt?
- [ ] Falls Datenbank vorhanden: Werden Prepared Statements verwendet?

**Status:** [z.B. "Kontaktformular validiert client-seitig"]

---

## 4. Allgemeine Best Practices

- [ ] Sind externe Links mit `target="_blank"` auch mit `rel="noopener"` versehen?
- [ ] Werden externe Ressourcen (CSS, JS, Fonts) von vertrauenswürdigen Quellen geladen?
- [ ] Sind alle Eingabefelder mit `maxlength` begrenzt?
- [ ] Gibt es eine Datenschutzerklärung (falls persönliche Daten gesammelt werden)?

---

## Nächste Schritte

**Was muss ich noch verbessern?**
1. [Liste Punkte auf, die noch nicht erfüllt sind]
2. 
3. 

**Wann plane ich die Verbesserungen?**
[Zeitplan eintragen]
```

**Deine Aufgabe:**
1. Erstelle die Datei `sicherheits-checkliste.md`
2. Gehe deine gesamte Portfolio-Website durch
3. Hake alle zutreffenden Punkte ab
4. Notiere bei jedem Abschnitt den aktuellen Status
5. Liste Verbesserungen auf, die du noch vornehmen möchtest

---

## Erfolgskriterien

Deine Lösung ist vollständig, wenn:

- [ ] Die Datei `kontakt.html` existiert und ein funktionierendes Formular enthält
- [ ] Das Formular validiert alle Felder mit JavaScript
- [ ] Ungültige Eingaben werden mit Fehlermeldungen abgelehnt
- [ ] Der Code enthält aussagekräftige Kommentare zu Sicherheitsaspekten
- [ ] Die Datei `sicherheits-checkliste.md` existiert
- [ ] Du hast alle Punkte der Checkliste für deine Website geprüft
- [ ] Das Kontaktformular ist von deiner Haupt-Portfolio-Seite verlinkt

---

## Häufige Fehler vermeiden

- **Fehler:** Nur `required`-Attribut im HTML, keine JavaScript-Validation  
  **Richtig:** HTML-Validation kann im Browser-DevTools umgangen werden. Nutze zusätzlich JavaScript.

- **Fehler:** Fehlermeldung ist zu allgemein ("Fehler bei der Eingabe")  
  **Richtig:** Sage genau, welches Feld das Problem hat und was erwartet wird.

- **Fehler:** Verlassen auf `input type="email"` ohne eigene Prüfung  
  **Richtig:** Browser-Validierung ist inkonsistent. Prüfe selbst mit einer eigenen Funktion.

---

## Reflexionsfragen

1. **Warum reicht es nicht aus, nur client-seitig (JavaScript) zu validieren?**
2. **Welche Eingaben in deinem Kontaktformular könnten potentiell gefährlich sein?**
3. **Was würde passieren, wenn jemand in das Nachricht-Feld eingibt: `<script>alert('Gehackt!');</script>`?**
4. **Wie würdest du dein Formular erweitern, wenn du es mit einem Server verbinden würdest?**

---

## Weiterführende Links

- **HTML5 Form Validation:** [https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- **Input Sanitization:** [https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
- **HTTPS erklärt:** [https://www.cloudflare.com/learning/ssl/what-is-https/](https://www.cloudflare.com/learning/ssl/what-is-https/)
- **Regular Expressions (Regex) lernen:** [https://regexr.com/](https://regexr.com/)

---

## Tipps für die Lösung

**Validierungs-Funktionen (Beispiele):**

```javascript
// Name validieren: Nur Buchstaben und Leerzeichen
function istGueltigerName(name) {
    const regex = /^[a-zA-ZäöüÄÖÜß\s]+$/;
    return regex.test(name) && name.length >= 2;
}

// E-Mail validieren (einfache Prüfung)
function istGueltigeEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}

// HTML-Tags entfernen
function entferneHTML(text) {
    return text.replace(/<[^>]*>/g, '');
}

// Gefährliche Zeichen ersetzen
function escapeHTML(text) {
    const map = {
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        '"': '&quot;',
        "'": '&#x27;'
    };
    return text.replace(/[&<>"']/g, (m) => map[m]);
}
```

**Verwendung:**
```javascript
const name = document.getElementById('name').value.trim();

if (!istGueltigerName(name)) {
    zeigeFehler('Bitte gib einen gültigen Namen ein (nur Buchstaben).');
    return;
}

// Bereinige Eingaben
const nachricht = escapeHTML(document.getElementById('nachricht').value);
```

---

## Bonus-Herausforderung (Optional)

Erweitere dein Kontaktformular um eine **Spam-Schutz-Massnahme**:

1. Füge ein verstecktes Feld hinzu (Honeypot):
   ```html
   <input type="text" name="website" style="display:none;" tabindex="-1">
   ```
2. Prüfe bei Absenden: Ist das Feld leer? Wenn ja → echter Nutzer. Wenn nein → wahrscheinlich Bot.
3. Recherchiere, warum diese Technik "Honeypot" heisst und wie sie funktioniert.

---

**Nächste Aufgabe:** 04 – Vertiefung: Security Headers & Best Practices (optional)
