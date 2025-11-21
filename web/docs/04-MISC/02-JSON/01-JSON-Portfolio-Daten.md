# Auftrag 1: JSON-Portfolio-Daten erstellen

## Ziel

Du lernst die Grundlagen von JSON kennen und erstellst strukturierte Daten für dein Portfolio. Du verstehst die JSON-Syntax mit Objekten, Arrays und Schlüssel-Wert-Paaren und kannst gültiges JSON schreiben.

## Beschreibung

JSON (JavaScript Object Notation) ist das Standard-Format für Datenaustausch im Web. Fast jede moderne Webanwendung nutzt JSON, um Daten zwischen Frontend und Backend zu übertragen. JSON ist einfach zu lesen, kompakt und wird von praktisch jeder Programmiersprache unterstützt.

In diesem Auftrag erstellst du deine ersten JSON-Dateien mit persönlichen Portfolio-Daten. Du lernst die Syntax-Regeln kennen, verstehst die verschiedenen Datentypen und übst das Schreiben von validen JSON-Strukturen.

---

### Teil 1: Persönliche Daten als JSON (15 Min)

Erstelle eine neue Datei **`person.json`** in deinem Portfolio-Ordner:

```
mein-portfolio/
├── index.html
├── styles.css
├── script.js
└── person.json    ← Neue Datei!
```

**Struktur von `person.json`:**

Erstelle eine JSON-Datei mit folgender Struktur. **Fülle sie mit deinen eigenen Daten:**

```json
{
  "vorname": "...",
  "nachname": "...",
  "alter": ...,
  "email": "...",
  "telefon": "...",
  "adresse": {
    "strasse": "...",
    "plz": "...",
    "ort": "...",
    "land": "..."
  },
  "beruf": "...",
  "lehrjahr": ...,
  "lehrbeginn": "...",
  "firma": "...",
  "hobbies": ["...", "...", "..."],
  "sprachen": [
    {
      "sprache": "...",
      "niveau": "..."
    }
  ],
  "portfolio": {
    "website": "...",
    "github": "...",
    "linkedin": "..."
  },
  "istAktiv": ...,
  "profilBild": ...
}
```

**Wo findest du Hilfe zur JSON-Syntax?**
- [JSON Datentypen auf MDN](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSON.org - Syntax-Übersicht](https://www.json.org/json-de.html)
- Schaue in die **JSON-Syntax-Regeln** weiter unten

**Wichtige JSON-Regeln:**

1. **Doppelte Anführungszeichen** bei Schlüsseln und String-Werten: `"name": "Sarah"`
2. **Kommas zwischen Paaren** (aber NICHT nach dem letzten Paar!)
3. **Geschwungene Klammern** für Objekte: `{ }`
4. **Eckige Klammern** für Arrays: `[ ]`
5. **Kein Komma nach letztem Element** in Objekten/Arrays

**Deine Aufgabe:**
1. Ersetze **alle `...`** mit deinen eigenen Daten
2. Beachte die **Datentypen**:
   - Text → in `"Anführungszeichen"`
   - Zahlen → ohne Anführungszeichen: `18`
   - Boolean → `true` oder `false` (ohne Anführungszeichen)
   - null → `null` (ohne Anführungszeichen, für leere Werte)
3. Füge **mindestens 3 Sprachen** hinzu
4. Füge **mindestens 3 Hobbies** hinzu

**Validiere deine JSON-Datei:**
1. Öffne [jsonlint.com](https://jsonlint.com)
2. Kopiere deinen JSON-Code hinein
3. Klicke "Validate JSON"
4. Korrigiere Fehler, falls vorhanden

**Häufige Fragen?**
- Welche Datentypen gibt es in JSON? → Siehe [JSON Datentypen](https://www.json.org/json-de.html)
- Wie schreibt man Arrays? → Mit eckigen Klammern `["wert1", "wert2"]`
- Wie schreibt man verschachtelte Objekte? → Mit geschweiften Klammern `{"key": "value"}`

---

### Teil 2: Skills-Liste als JSON (20 Min)

Erstelle eine neue Datei **`skills.json`** mit folgender Struktur:

```json
{
  "skills": [
    {
      "id": 1,
      "name": "HTML",
      "kategorie": "Frontend",
      "level": 4,
      "maxLevel": 5,
      "beschreibung": "Semantisches HTML, Formulare, Strukturierung",
      "gelerntAm": "2025-09-01",
      "projekte": ["Portfolio-Website", "Kontaktformular"],
      "istHauptskill": true
    }
  ],
  "statistik": {
    "gesamtSkills": ...,
    "hauptskills": ...,
    "kategorien": [],
    "durchschnittLevel": ...,
    "letzteAktualisierung": "..."
  }
}
```

**Deine Aufgabe:**
1. Füge **mindestens 7 weitere Skills** hinzu (z.B. CSS, JavaScript, JSON, Git, VS Code, etc.)
2. Nutze verschiedene Kategorien: "Frontend", "Backend", "Tools", "Design"
3. Passe die Level-Werte an deine Fähigkeiten an (1 = Anfänger, 5 = Experte)
4. Berechne und fülle die Statistik:
   - `gesamtSkills`: Wie viele Skills hast du insgesamt?
   - `hauptskills`: Zähle Skills mit `"istHauptskill": true`
   - `kategorien`: Liste alle verwendeten Kategorien auf
   - `durchschnittLevel`: Berechne den Durchschnitt aller Level
   - `letzteAktualisierung`: Heutiges Datum (Format: YYYY-MM-DD)

**Hilfe zur Berechnung des Durchschnitts:**
```
Durchschnitt = (Summe aller Level) ÷ (Anzahl Skills)
```
Beispiel: Skills mit Level 4, 3, 2, 2, 3 → (4+3+2+2+3) ÷ 5 = 2.8

**Wo nachschlagen?**
- [Arrays in JSON](https://www.json.org/json-de.html) - Wie erstellt man Listen?
- [MDN: Working with Objects](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Working_with_Objects)

**Neue Konzepte:**
- **Arrays von Objekten**: Jeder Skill ist ein Objekt in einem Array
- **Verschachtelte Daten**: `projekte` ist ein Array innerhalb eines Objekts
- **Verschiedene Datentypen**: String, Number, Boolean, Array

---

### Teil 3: Projekt-Liste als JSON (20 Min)

Erstelle eine neue Datei **`projekte.json`**.

**Orientiere dich an dieser Beispielstruktur für EIN Projekt:**

```json
{
  "projekte": [
    {
      "id": 1,
      "titel": "Portfolio-Website",
      "beschreibung": "Meine persönliche Portfolio-Seite",
      "kategorie": "Webentwicklung",
      "technologien": ["HTML", "CSS", "JavaScript"],
      "status": "in Arbeit",
      "fortschritt": 75,
      "startDatum": "2025-09-01",
      "geplantesEnde": "2025-12-31",
      "zeitInvestiert": 45,
      "zeitGeplant": 60,
      "schwierigkeitsgrad": "mittel",
      "prioritaet": "hoch",
      "repository": "https://github.com/...",
      "liveUrl": null,
      "gelernteSkills": ["HTML", "CSS", "JavaScript"],
      "herausforderungen": ["...", "..."],
      "naechsteSchritte": ["...", "..."],
      "istSichtbar": true,
      "istAbgeschlossen": false
    }
  ],
  "statistik": {
    "gesamtProjekte": ...,
    "aktiv": ...,
    "abgeschlossen": ...,
    "geplant": ...,
    "gesamtZeit": ...,
    "durchschnittFortschritt": ...
  }
}
```

**Deine Aufgabe:**
1. Füge **mindestens 3 weitere Projekte** hinzu:
   - Ein abgeschlossenes Projekt: `"status": "abgeschlossen"`, `"fortschritt": 100`, `"istAbgeschlossen": true`
   - Ein aktives Projekt: `"status": "in Arbeit"`, `"fortschritt": 30-90`
   - Ein geplantes Projekt: `"status": "geplant"`, `"fortschritt": 0`, `"zeitInvestiert": 0`

2. Beachte bei geplanten Projekten:
   - Setze `startDatum` in die Zukunft
   - Setze `zeitInvestiert: 0`
   - Setze `naechsteSchritte` mit mindestens 2 Einträgen
   - Setze `istAbgeschlossen: false`

3. Fülle die Statistik aus (berechne selbst!):
   - `gesamtProjekte`: Anzahl aller Projekte
   - `aktiv`: Anzahl Projekte mit Status "in Arbeit"
   - `abgeschlossen`: Anzahl Projekte mit Status "abgeschlossen"
   - `geplant`: Anzahl Projekte mit Status "geplant"
   - `gesamtZeit`: Summe aller `zeitInvestiert`-Werte
   - `durchschnittFortschritt`: Durchschnitt aller `fortschritt`-Werte

**Berechnungshilfe Durchschnittsfortschritt:**
```
(Projekt1.fortschritt + Projekt2.fortschritt + ...) ÷ Anzahl Projekte
```

**Wo nachschlagen?**
- Welche Werte kann `status` haben? → Schaue in den Beispielen oben
- Wie formatiert man Datumsangaben? → Format: `"YYYY-MM-DD"` (z.B. `"2025-11-18"`)
- Was ist der Unterschied zwischen `null` und `[]`? → [JSON.org Datentypen](https://www.json.org/json-de.html)

---

### Teil 4: JSON in JavaScript laden (10 Min)

Jetzt verbinden wir JSON mit JavaScript. Erstelle eine neue Datei **`json-test.js`**:

```javascript
// =====================================================
// JSON-DATEN LADEN UND VERARBEITEN
// =====================================================

console.log("=== JSON-TEST ===\n");

// === METHODE 1: JSON.parse() ===
// JSON-String in JavaScript-Objekt umwandeln

let personString = '{"vorname": "Sarah", "nachname": "Müller", "alter": 18}';

console.log("JSON-String:", personString);
console.log("Typ:", typeof personString);  // "string"

// Parsen (String → Objekt)
let person = JSON.parse(personString);

console.log("\nNach JSON.parse():");
console.log("Person-Objekt:", person);
console.log("Typ:", typeof person);        // "object"
console.log("Vorname:", person.vorname);   // "Sarah"
console.log("Alter:", person.alter);       // 18

console.log("\n---\n");

// === METHODE 2: JSON.stringify() ===
// JavaScript-Objekt in JSON-String umwandeln

let meinProjekt = {
  titel: "Portfolio",
  technologien: ["HTML", "CSS", "JavaScript"],
  status: "in Arbeit",
  fortschritt: 75
};

console.log("JavaScript-Objekt:", meinProjekt);

// Stringify (Objekt → String)
let projektJSON = JSON.stringify(meinProjekt);

console.log("\nNach JSON.stringify():");
console.log("JSON-String:", projektJSON);
console.log("Typ:", typeof projektJSON);   // "string"

// Stringify mit schöner Formatierung
let projektFormatiert = JSON.stringify(meinProjekt, null, 2);

console.log("\nFormatiert (mit Einrückung):");
console.log(projektFormatiert);

console.log("\n---\n");

// === METHODE 3: Fetch (JSON-Datei laden) ===
// Echte JSON-Datei laden und verarbeiten

console.log("Lade person.json...");

fetch('person.json')
  .then(response => {
    console.log("Response erhalten:", response.ok);
    return response.json();  // Automatisches JSON.parse()
  })
  .then(data => {
    console.log("\nGeladene Person-Daten:");
    console.log("Name:", data.vorname, data.nachname);
    console.log("Beruf:", data.beruf);
    console.log("Hobbies:", data.hobbies.join(", "));
    console.log("Sprachen:", data.sprachen.length);
  })
  .catch(error => {
    console.error("Fehler beim Laden:", error);
  });

console.log("\n---\n");

// === BEISPIEL 4: Skills verarbeiten ===

console.log("Lade skills.json...");

fetch('skills.json')
  .then(response => response.json())
  .then(data => {
    console.log("\n=== MEINE SKILLS ===");
    
    data.skills.forEach((skill, index) => {
      let prozent = (skill.level / skill.maxLevel) * 100;
      let balken = "█".repeat(skill.level) + "░".repeat(skill.maxLevel - skill.level);
      
      console.log(`\n${index + 1}. ${skill.name} (${skill.kategorie})`);
      console.log(`   Level: ${balken} ${skill.level}/${skill.maxLevel} (${prozent}%)`);
      console.log(`   ${skill.beschreibung}`);
    });
    
    console.log("\n=== STATISTIK ===");
    console.log(`Gesamt: ${data.statistik.gesamtSkills} Skills`);
    console.log(`Durchschnitt: ${data.statistik.durchschnittLevel}/5`);
  });
```

**Binde die Datei in dein HTML ein:**

```html
<script src="json-test.js"></script>
```

**Öffne die Konsole (F12) und schaue dir die Ausgaben an!**

**Wichtig:** Fetch funktioniert nur auf einem Webserver. Nutze einen dieser Wege:
1. VS Code Extension: "Live Server" installieren → Rechtsklick auf HTML → "Open with Live Server"
2. Python-Server: Terminal öffnen, `python -m http.server` ausführen, Browser: `http://localhost:8000`
3. Node.js-Server: `npx http-server` ausführen

---

## Erfolgskriterien

- [ ] `person.json` erstellt mit deinen persönlichen Daten
- [ ] `skills.json` erstellt mit mindestens 5 Skills
- [ ] `projekte.json` erstellt mit mindestens 3 Projekten
- [ ] Alle JSON-Dateien sind valide (getestet mit jsonlint.com)
- [ ] JSON-Syntax-Regeln korrekt angewendet (doppelte Anführungszeichen, Kommas)
- [ ] Verschiedene Datentypen verwendet (String, Number, Boolean, Array, Object, null)
- [ ] Statistik-Werte korrekt berechnet und eingefügt
- [ ] `json-test.js` erstellt und in HTML eingebunden
- [ ] JSON-Dateien erfolgreich geladen und in Konsole ausgegeben
- [ ] Unterschied zwischen JSON-String und JavaScript-Objekt verstanden

---

## Tipps

**VS Code für JSON:**
- VS Code erkennt `.json`-Dateien automatisch
- Syntax-Fehler werden rot unterstrichen
- Auto-Formatierung: `Shift + Alt + F`
- Bracket-Matching: Zeigt zusammengehörige Klammern

**Häufige Fehler:**
- ❌ Einfache Anführungszeichen: `{'name': 'Sarah'}` → Ungültig!
- ✅ Doppelte Anführungszeichen: `{"name": "Sarah"}` → Gültig
- ❌ Komma nach letztem Element: `{"name": "Sarah",}` → Ungültig!
- ✅ Kein Komma am Ende: `{"name": "Sarah"}` → Gültig
- ❌ undefined verwenden: `{"wert": undefined}` → Ungültig!
- ✅ null verwenden: `{"wert": null}` → Gültig

**Debugging:**
1. Konsole öffnen (F12)
2. Schaue nach "SyntaxError" oder "Unexpected token"
3. Zeile und Position des Fehlers prüfen
4. JSON-Validator nutzen (jsonlint.com)

**JSON vs. JavaScript-Objekt:**
```javascript
// JavaScript (flexibel):
let obj = {
  name: "Sarah",     // Ohne "" erlaubt
  greet() {          // Methoden erlaubt
    console.log("Hi");
  }
};

// JSON (strikt):
let json = '{"name": "Sarah"}';  // Nur Daten, keine Funktionen
```

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen einem JSON-String und einem JavaScript-Objekt?**  
   *Tipp: Welchen Datentyp hat jedes? Wie kannst du zwischen beiden konvertieren?*

2. **Warum müssen Schlüssel in JSON immer in doppelten Anführungszeichen stehen, in JavaScript aber nicht?**  
   *Recherchiere: Welche Regeln hat JSON, die JavaScript nicht hat?*

3. **Experimentiere: Was passiert, wenn du `JSON.parse()` auf einen ungültigen JSON-String anwendest?**  
   *Probiere: `JSON.parse("{name: 'Test'}")` – Was ist der Fehler?*

4. **Wie kannst du herausfinden, ob eine JSON-Datei valide ist, bevor du sie in deinem Code verwendest?**  
   *Tipp: Welche Tools oder Online-Validators gibt es?*

5. **Warum ist JSON als Datenaustauschformat so verbreitet?**  
   *Überlege: Welche Vorteile hat JSON gegenüber anderen Formaten wie XML?*

---

## Weiterführende Links

**JSON-Grundlagen:**
- [MDN: JSON](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSON.org](https://www.json.org/json-de.html) – Offizielle JSON-Spezifikation
- [W3Schools: JSON Tutorial](https://www.w3schools.com/js/js_json_intro.asp)

**JSON-Tools:**
- [JSONLint](https://jsonlint.com/) – JSON-Validator
- [JSON Formatter](https://jsonformatter.org/) – JSON formatieren und visualisieren
- [JSON Editor Online](https://jsoneditoronline.org/) – JSON interaktiv bearbeiten

**JSON in JavaScript:**
- [MDN: JSON.parse()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
- [MDN: JSON.stringify()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [JavaScript.info: JSON methods](https://javascript.info/json)

**Fortgeschritten:**
- [MDN: Using Fetch](https://developer.mozilla.org/de/docs/Web/API/Fetch_API/Using_Fetch)
- [JSON Schema](https://json-schema.org/) – JSON-Strukturen definieren und validieren

---

**⏱️ Geschätzte Zeit:** 55 Minuten  
**📦 Nächster Schritt:** Auftrag 2 – JSON validieren und debuggen
