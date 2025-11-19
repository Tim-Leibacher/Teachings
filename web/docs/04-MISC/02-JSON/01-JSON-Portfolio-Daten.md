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

**Inhalt von `person.json`:**

```json
{
  "vorname": "Sarah",
  "nachname": "Müller",
  "alter": 18,
  "email": "sarah.mueller@example.com",
  "telefon": "+41 79 123 45 67",
  "adresse": {
    "strasse": "Bahnhofstrasse 1",
    "plz": "3000",
    "ort": "Bern",
    "land": "Schweiz"
  },
  "beruf": "Informatikerin EFZ Applikationsentwicklung",
  "lehrjahr": 1,
  "lehrbeginn": "2025-08-01",
  "firma": "ABC Tech AG",
  "hobbies": ["Programmieren", "Fotografie", "Wandern"],
  "sprachen": [
    {
      "sprache": "Deutsch",
      "niveau": "Muttersprache"
    },
    {
      "sprache": "Englisch",
      "niveau": "B2"
    },
    {
      "sprache": "Französisch",
      "niveau": "A2"
    }
  ],
  "portfolio": {
    "website": "https://sarahmueller.dev",
    "github": "https://github.com/sarahmueller",
    "linkedin": "https://linkedin.com/in/sarah-mueller"
  },
  "istAktiv": true,
  "profilBild": null
}
```

**Wichtige JSON-Regeln:**

1. **Doppelte Anführungszeichen** bei Schlüsseln und String-Werten: `"name": "Sarah"`
2. **Kommas zwischen Paaren** (aber NICHT nach dem letzten Paar!)
3. **Geschwungene Klammern** für Objekte: `{ }`
4. **Eckige Klammern** für Arrays: `[ ]`
5. **Kein Komma nach letztem Element** in Objekten/Arrays

**Ersetze die Beispieldaten mit deinen eigenen:**
- Füge deine persönlichen Informationen ein
- Passe Hobbies, Sprachen und Portfolio-Links an
- Behalte die Struktur bei (Datentypen nicht ändern!)

**Validiere deine JSON-Datei:**
1. Öffne [jsonlint.com](https://jsonlint.com)
2. Kopiere deinen JSON-Code hinein
3. Klicke "Validate JSON"
4. Korrigiere Fehler, falls vorhanden

---

### Teil 2: Skills-Liste als JSON (15 Min)

Erstelle eine neue Datei **`skills.json`**:

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
    },
    {
      "id": 2,
      "name": "CSS",
      "kategorie": "Frontend",
      "level": 3,
      "maxLevel": 5,
      "beschreibung": "Flexbox, Grid, Responsive Design",
      "gelerntAm": "2025-09-15",
      "projekte": ["Portfolio-Website"],
      "istHauptskill": true
    },
    {
      "id": 3,
      "name": "JavaScript",
      "kategorie": "Frontend",
      "level": 2,
      "maxLevel": 5,
      "beschreibung": "Basics, DOM-Manipulation, Events",
      "gelerntAm": "2025-10-01",
      "projekte": ["Portfolio-Website", "Rechner-App"],
      "istHauptskill": true
    },
    {
      "id": 4,
      "name": "Git",
      "kategorie": "Tools",
      "level": 2,
      "maxLevel": 5,
      "beschreibung": "Versionskontrolle, Commits, Branches",
      "gelerntAm": "2025-09-01",
      "projekte": ["Alle Projekte"],
      "istHauptskill": false
    },
    {
      "id": 5,
      "name": "VS Code",
      "kategorie": "Tools",
      "level": 3,
      "maxLevel": 5,
      "beschreibung": "Editor, Extensions, Debugging",
      "gelerntAm": "2025-08-15",
      "projekte": ["Alle Projekte"],
      "istHauptskill": false
    }
  ],
  "statistik": {
    "gesamtSkills": 5,
    "hauptskills": 3,
    "kategorien": ["Frontend", "Tools"],
    "durchschnittLevel": 2.8,
    "letzteAktualisierung": "2025-11-18"
  }
}
```

**Deine Aufgabe:**
1. Füge mindestens **3 weitere Skills** hinzu (z.B. JSON, Debugging, Markdown, Photoshop)
2. Passe die Level-Werte an deine Fähigkeiten an (1 = Anfänger, 5 = Experte)
3. Aktualisiere die Statistik:
   - `gesamtSkills`: Anzahl Skills im Array
   - `hauptskills`: Anzahl mit `"istHauptskill": true`
   - `durchschnittLevel`: Durchschnitt aller Level-Werte
   - `letzteAktualisierung`: Heutiges Datum (Format: YYYY-MM-DD)

**Berechnung Durchschnitt:**
```
(4 + 3 + 2 + 2 + 3) / 5 = 2.8
```

**Neue Konzepte:**
- **Arrays von Objekten**: Jeder Skill ist ein Objekt in einem Array
- **Verschachtelte Daten**: `projekte` ist ein Array innerhalb eines Objekts
- **Verschiedene Datentypen**: String, Number, Boolean, Array

---

### Teil 3: Projekt-Liste als JSON (15 Min)

Erstelle eine neue Datei **`projekte.json`**:

```json
{
  "projekte": [
    {
      "id": 1,
      "titel": "Portfolio-Website",
      "beschreibung": "Meine persönliche Portfolio-Seite mit Projekten, Skills und Kontaktformular",
      "kategorie": "Webentwicklung",
      "technologien": ["HTML", "CSS", "JavaScript", "JSON"],
      "status": "in Arbeit",
      "fortschritt": 75,
      "startDatum": "2025-09-01",
      "geplantesEnde": "2025-12-31",
      "zeitInvestiert": 45,
      "zeitGeplant": 60,
      "schwierigkeitsgrad": "mittel",
      "prioritaet": "hoch",
      "repository": "https://github.com/sarahmueller/portfolio",
      "liveUrl": null,
      "screenshots": [],
      "gelernteSkills": ["HTML", "CSS", "JavaScript", "Git"],
      "herausforderungen": [
        "Responsive Design für verschiedene Geräte",
        "JavaScript DOM-Manipulation",
        "JSON-Datenverwaltung"
      ],
      "naechsteSchritte": [
        "Kontaktformular fertigstellen",
        "Projekt-Galerie erweitern",
        "SEO optimieren"
      ],
      "istSichtbar": true,
      "istAbgeschlossen": false
    },
    {
      "id": 2,
      "titel": "HTML Grundlagen",
      "beschreibung": "Erste Schritte mit HTML: Struktur, Semantik, Formulare",
      "kategorie": "Lernen",
      "technologien": ["HTML"],
      "status": "abgeschlossen",
      "fortschritt": 100,
      "startDatum": "2025-08-15",
      "geplantesEnde": "2025-09-01",
      "zeitInvestiert": 20,
      "zeitGeplant": 20,
      "schwierigkeitsgrad": "einfach",
      "prioritaet": "mittel",
      "repository": null,
      "liveUrl": null,
      "screenshots": [],
      "gelernteSkills": ["HTML"],
      "herausforderungen": [
        "Semantische Tags verstehen",
        "Formular-Validierung"
      ],
      "naechsteSchritte": [],
      "istSichtbar": true,
      "istAbgeschlossen": true
    }
  ],
  "statistik": {
    "gesamtProjekte": 2,
    "aktiv": 1,
    "abgeschlossen": 1,
    "geplant": 0,
    "gesamtZeit": 65,
    "durchschnittFortschritt": 87.5
  }
}
```

**Deine Aufgabe:**
1. Füge mindestens **2 weitere Projekte** hinzu:
   - Ein abgeschlossenes Projekt (z.B. "CSS Layouts lernen")
   - Ein geplantes Projekt (z.B. "To-Do App", "Rechner-App", "Wetter-Dashboard")
   
2. Für geplante Projekte:
   - `status`: "geplant"
   - `fortschritt`: 0
   - `zeitInvestiert`: 0
   - `istAbgeschlossen`: false
   - `startDatum`: Zukünftiges Datum

3. Aktualisiere die Statistik:
   - Zähle Projekte nach Status
   - Berechne Gesamtzeit
   - Berechne Durchschnittsfortschritt

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
