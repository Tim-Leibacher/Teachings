# Storyboard: Von Node.js zu Express.js - Einführung

**Gesamtdauer:** ca. 10-12 Minuten  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Voraussetzungen:** Node.js Grundlagen, HTTP-Server mit dem http-Modul erstellt

---

## Szene 1: Intro - Rückblick und Ausblick (30 Sek.)

### Sprechertext
"Im letzten Modul hast du einen HTTP-Server mit dem eingebauten http-Modul erstellt. Das funktioniert, aber du hast sicher gemerkt: Routing, Content-Types, statische Dateien - alles musst du selbst programmieren. In diesem Video lernst du Express.js kennen. Express ist ein Framework, das dir die Arbeit abnimmt und Server-Entwicklung stark vereinfacht. Am Ende hast du deinen bisherigen Server auf Express umgestellt und wirst sehen, wie viel weniger Code du brauchst."

### Bildschirmdarstellung
- BAND-Logo mit Titel: **"Von Node.js zu Express.js"**
- Text-Overlay:
  - **"HTTP-Modul = mühsam"**
  - **"Express.js = einfach"**
  - **"Weniger Code, mehr Features"**

### Hinweise
- Nutze BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A)
- Fade-In Animation

---

## Szene 2: Das Problem mit dem http-Modul (1 Min. 30 Sek.)

### Sprechertext
"Schauen wir uns nochmal an, was wir bisher gemacht haben. Hier ist ein Server mit dem http-Modul: Für jede Route brauchst du ein if/else, den Content-Type musst du manuell setzen, statische Dateien musst du mit dem fs-Modul selbst lesen. Das ist viel Code für simple Aufgaben. Und wenn das Projekt wächst, wird es schnell unübersichtlich. Bei zehn Routen hast du zehn if/else-Blöcke. Bei hundert Routen - du verstehst das Problem."

### Bildschirmdarstellung
VS Code mit bestehendem Code aus vorherigem Modul:

```javascript
// server.js - HTTP-Server (bisherige Lösung)
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
    // Routing mit if/else - wird schnell unübersichtlich!
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html; charset=utf-8');
        res.end('<h1>Startseite</h1>');
    } else if (req.url === '/about') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html; charset=utf-8');
        res.end('<h1>Über mich</h1>');
    } else if (req.url === '/api/skills') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'application/json');
        res.end(JSON.stringify({ skills: ['HTML', 'CSS', 'JS'] }));
    } else {
        res.statusCode = 404;
        res.end('Seite nicht gefunden');
    }
});

server.listen(3000);
```

Text-Overlay mit Problemliste:
- **Problem 1:** if/else für jede Route
- **Problem 2:** Content-Type manuell setzen
- **Problem 3:** Statische Dateien selbst laden
- **Problem 4:** Kein Middleware-System

### Hinweise
- Code rot markieren bei den Problemstellen
- Zeige, wie unübersichtlich das bei vielen Routen wird

---

## Szene 3: Was ist Express.js? (1 Min.)

### Sprechertext
"Express.js ist das beliebteste Web-Framework für Node.js. Es wurde 2010 veröffentlicht und wird von Millionen Entwicklern genutzt. Express löst genau die Probleme, die wir gerade gesehen haben: Es bietet ein elegantes Routing-System, automatische Content-Type-Erkennung, ein Middleware-Konzept und vieles mehr. Express ist minimal und gibt dir trotzdem alle Werkzeuge, die du brauchst. Grosse Unternehmen wie IBM, Uber und Twitter nutzen Express für ihre Anwendungen."

### Bildschirmdarstellung
**Vorteile von Express.js:**
```
╔═══════════════════════════════════════════════════════════╗
║   Express.js - Warum?                                     ║
╠═══════════════════════════════════════════════════════════╣
║   1. Elegantes Routing     app.get('/route', handler)     ║
║   2. Middleware-System     app.use(middleware)            ║
║   3. Statische Dateien     express.static('public')       ║
║   4. JSON automatisch      res.json({ data: 'value' })    ║
║   5. Einfache Fehlerbehandlung                            ║
║   6. Riesige Community & Ecosystem                        ║
╚═══════════════════════════════════════════════════════════╝
```

Statistik-Overlay:
- **"30+ Millionen Downloads pro Woche"**
- **"Seit 2010 aktiv entwickelt"**
- **"Das Standard-Framework für Node.js"**

### Hinweise
- Browser kurz [expressjs.com](https://expressjs.com) zeigen
- Zeige npm-Seite mit Download-Statistik

---

## Szene 4: Express installieren (1 Min. 30 Sek.)

### Sprechertext
"Lass uns Express installieren. Erstelle einen neuen Ordner für dein Portfolio-Projekt mit Express. Dann initialisierst du ein NPM-Projekt mit npm init -y und installierst Express mit npm install express. Nach der Installation findest du Express in der package.json unter dependencies und im node_modules-Ordner."

### Bildschirmdarstellung
Terminal zeigen:

```bash
# Neuen Projektordner erstellen
mkdir portfolio-express
cd portfolio-express

# NPM-Projekt initialisieren
npm init -y

# Express installieren
npm install express
```

**Ausgabe zeigen:**
```
added 65 packages in 2s
```

**package.json zeigen:**
```json
{
  "name": "portfolio-express",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "express": "^4.21.0"
  }
}
```

### Hinweise
- Zeige, dass express in dependencies erscheint
- Erwähne kurz node_modules (nicht ins Git!)
- Text-Overlay: **"npm install express"**

---

## Szene 5: Erster Express-Server (2 Min.)

### Sprechertext
"Jetzt erstellen wir unseren ersten Express-Server. Der Unterschied ist sofort sichtbar: Statt http.createServer nutzen wir express() und statt dem Callback haben wir Methoden wie app.get für GET-Requests. Die Response-Methode res.send erkennt automatisch, ob du HTML oder Text sendest. Mit nur wenigen Zeilen Code hast du einen funktionierenden Server."

### Bildschirmdarstellung
VS Code - neue Datei **`server.js`**:

```javascript
// server.js - Erster Express-Server

// Express importieren
const express = require('express');

// Express-App erstellen
const app = express();

// Port definieren
const PORT = 3000;

// Erste Route: Startseite
app.get('/', (req, res) => {
    res.send('<h1>Willkommen auf meinem Portfolio!</h1>');
});

// Server starten
app.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

**Terminal:**
```bash
node server.js
```

**Ausgabe:**
```
Server läuft auf http://localhost:3000
```

**Browser zeigen:** `http://localhost:3000` mit der Willkommensnachricht

### Hinweise
- Vergleiche mit http-Modul Code - deutlich kürzer!
- Text-Overlay: **"express() statt http.createServer()"**
- Text-Overlay: **"app.get() statt if/else"**

---

## Szene 6: Routing in Express (2 Min.)

### Sprechertext
"Routing in Express ist elegant und übersichtlich. Für jede Route nutzt du eine eigene Methode: app.get für GET-Requests, app.post für POST-Requests, und so weiter. Jede Route hat zwei Parameter: den Pfad und eine Handler-Funktion. Die Handler-Funktion erhält request und response als Parameter. Schauen wir uns an, wie wir mehrere Routen für unser Portfolio definieren."

### Bildschirmdarstellung
VS Code - **`server.js`** erweitern:

```javascript
// server.js - Express mit mehreren Routen

const express = require('express');
const app = express();
const PORT = 3000;

// Startseite
app.get('/', (req, res) => {
    res.send(`
        <h1>Mein Portfolio</h1>
        <nav>
            <a href="/">Home</a> |
            <a href="/about">Über mich</a> |
            <a href="/skills">Skills</a> |
            <a href="/projects">Projekte</a> |
            <a href="/contact">Kontakt</a>
        </nav>
        <p>Willkommen auf meiner Portfolio-Seite!</p>
    `);
});

// Über mich
app.get('/about', (req, res) => {
    res.send(`
        <h1>Über mich</h1>
        <p>Ich bin Lernende/r im 1. Lehrjahr.</p>
        <a href="/">Zurück</a>
    `);
});

// Skills
app.get('/skills', (req, res) => {
    res.send(`
        <h1>Meine Skills</h1>
        <ul>
            <li>HTML & CSS</li>
            <li>JavaScript</li>
            <li>Node.js</li>
            <li>Express.js</li>
        </ul>
        <a href="/">Zurück</a>
    `);
});

// Projekte
app.get('/projects', (req, res) => {
    res.send(`
        <h1>Meine Projekte</h1>
        <p>Portfolio-Website (in Arbeit)</p>
        <a href="/">Zurück</a>
    `);
});

// Kontakt
app.get('/contact', (req, res) => {
    res.send(`
        <h1>Kontakt</h1>
        <p>Email: meine.email@example.com</p>
        <a href="/">Zurück</a>
    `);
});

// Server starten
app.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

**Browser demonstrieren:** Navigation zwischen Seiten zeigen

### Hinweise
- Zeige jede Route im Browser
- Text-Overlay: **"1 Route = 1 app.get()"**
- Vergleich: Kein if/else mehr nötig!

---

## Szene 7: JSON-APIs mit res.json() (1 Min. 30 Sek.)

### Sprechertext
"Für APIs nutzt du res.json() statt res.send(). Express setzt automatisch den Content-Type auf application/json und konvertiert dein JavaScript-Objekt in JSON. Du musst JSON.stringify nicht mehr selbst aufrufen. Lass uns eine API für unser Portfolio erstellen, die Skills und Projekte als JSON zurückgibt."

### Bildschirmdarstellung
VS Code - API-Routen hinzufügen:

```javascript
// API-Routen für das Portfolio

// API: Alle Skills
app.get('/api/skills', (req, res) => {
    const skills = {
        frontend: ['HTML', 'CSS', 'JavaScript'],
        backend: ['Node.js', 'Express.js'],
        tools: ['Git', 'VS Code', 'Terminal']
    };
    res.json(skills);
});

// API: Alle Projekte
app.get('/api/projects', (req, res) => {
    const projects = [
        {
            id: 1,
            name: 'Portfolio-Website',
            technologies: ['HTML', 'CSS', 'JavaScript'],
            status: 'In Arbeit'
        },
        {
            id: 2,
            name: 'Express-Server',
            technologies: ['Node.js', 'Express'],
            status: 'In Arbeit'
        }
    ];
    res.json(projects);
});

// API: Einzelnes Projekt nach ID
app.get('/api/projects/:id', (req, res) => {
    const projectId = req.params.id;
    res.json({ 
        message: `Projekt mit ID ${projectId} angefordert`,
        id: projectId 
    });
});
```

**Browser zeigen:**
- `http://localhost:3000/api/skills` - JSON-Ausgabe
- `http://localhost:3000/api/projects` - JSON-Ausgabe
- `http://localhost:3000/api/projects/1` - Dynamischer Parameter

### Hinweise
- Zeige JSON im Browser (formatiert)
- Erkläre `req.params.id` für dynamische Routen
- Text-Overlay: **"res.json() = automatisch JSON"**

---

## Szene 8: Statische Dateien mit express.static() (1 Min. 30 Sek.)

### Sprechertext
"Für statische Dateien wie HTML, CSS, JavaScript und Bilder nutzt du express.static(). Mit einer einzigen Zeile Code teilst du Express mit, aus welchem Ordner statische Dateien ausgeliefert werden sollen. Erstelle einen public-Ordner, lege dort deine Dateien ab, und Express kümmert sich um den Rest - Content-Type, Caching, alles automatisch."

### Bildschirmdarstellung
**Ordnerstruktur zeigen:**
```
portfolio-express/
├── server.js
├── package.json
└── public/
    ├── index.html
    ├── css/
    │   └── style.css
    └── js/
        └── script.js
```

VS Code - **`server.js`** erweitern:

```javascript
const express = require('express');
const path = require('path');

const app = express();
const PORT = 3000;

// Statische Dateien aus dem 'public'-Ordner
app.use(express.static('public'));

// Oder mit absolutem Pfad (empfohlen)
app.use(express.static(path.join(__dirname, 'public')));

// API-Routen bleiben bestehen
app.get('/api/skills', (req, res) => {
    res.json({ skills: ['HTML', 'CSS', 'JavaScript'] });
});

app.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

**public/index.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Mein Portfolio</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <h1>Mein Portfolio</h1>
    <p>Statische Datei wird von Express ausgeliefert!</p>
    <script src="/js/script.js"></script>
</body>
</html>
```

### Hinweise
- Zeige, dass index.html automatisch auf `/` geladen wird
- Erkläre: Express prüft zuerst statische Dateien
- Text-Overlay: **"express.static() = eine Zeile statt 50"**

---

## Szene 9: Vergleich http-Modul vs. Express (1 Min.)

### Sprechertext
"Lass uns den direkten Vergleich machen. Links der Code mit dem http-Modul, rechts mit Express. Der Unterschied ist enorm: Für den gleichen Funktionsumfang brauchst du mit Express nur etwa ein Drittel des Codes. Und der Express-Code ist nicht nur kürzer, sondern auch lesbarer und wartbarer. Bei grösseren Projekten wird dieser Unterschied noch deutlicher."

### Bildschirmdarstellung
Split-Screen:

**Links: http-Modul (40+ Zeilen)**
```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('<h1>Home</h1>');
    } else if (req.url === '/about') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('<h1>About</h1>');
    } else if (req.url === '/api/data') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'application/json');
        res.end(JSON.stringify({ data: 'test' }));
    } else {
        res.statusCode = 404;
        res.end('Not Found');
    }
});

server.listen(3000);
```

**Rechts: Express (15 Zeilen)**
```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/', (req, res) => {
    res.send('<h1>Home</h1>');
});

app.get('/about', (req, res) => {
    res.send('<h1>About</h1>');
});

app.get('/api/data', (req, res) => {
    res.json({ data: 'test' });
});

app.listen(3000);
```

**Statistik-Overlay:**
- **http-Modul:** 40+ Zeilen
- **Express:** 15 Zeilen
- **Ersparnis:** 60%+ weniger Code

### Hinweise
- Rot markieren: if/else, setHeader, JSON.stringify
- Grün markieren: Express-Methoden

---

## Szene 10: Zusammenfassung & Ausblick (45 Sek.)

### Sprechertext
"Fassen wir zusammen: Express.js ist ein Framework, das Server-Entwicklung mit Node.js stark vereinfacht. Statt if/else nutzt du app.get(), app.post() und andere Methoden. JSON wird automatisch mit res.json() serialisiert. Statische Dateien werden mit express.static() mit einer Zeile eingebunden. Express bietet noch viel mehr: Middleware, Fehlerbehandlung, Template-Engines. Das lernst du im nächsten Modul. Jetzt bist du dran - stell dein bestehendes Portfolio-Projekt auf Express um!"

### Bildschirmdarstellung
Zusammenfassung als Checkliste:

```
╔═══════════════════════════════════════════════════════════╗
║   Express.js - Das hast du gelernt                        ║
╠═══════════════════════════════════════════════════════════╣
║   ✓ Express installieren (npm install express)            ║
║   ✓ App erstellen (const app = express())                 ║
║   ✓ Routen definieren (app.get(), app.post())             ║
║   ✓ HTML senden (res.send())                              ║
║   ✓ JSON senden (res.json())                              ║
║   ✓ Statische Dateien (express.static())                  ║
║   ✓ Route-Parameter (req.params)                          ║
╚═══════════════════════════════════════════════════════════╝
```

Text-Overlay:
- **"Nächster Schritt: Middleware & Routen"**
- **"Jetzt selbst ausprobieren!"**

### Hinweise
- Fade-Out mit BAND-Gradient
- Call-to-Action: Aufträge bearbeiten

---

## Zusatzmaterialien für Video-Produktion

### Terminal-Setup

**Empfohlene Einstellungen:**
- Schriftgrösse: 18-20pt
- Font: JetBrains Mono oder Fira Code
- Theme: Dunkel mit guter Lesbarkeit
- Prompt: Verkürzt, nur Ordnername sichtbar

### VS Code Setup

- Theme: Dark+ oder Material Theme
- Font Size: 16-18pt
- Minimap ausblenden
- Extensions: ESLint, Prettier

### BAND Corporate Design

**Farben:**
- Primary Blue: #376B8C
- Secondary Türkis: #29786A
- Accent Orange: #E87722
- Grau: #6B7280
- Background: #F5F5F5

**Typografie:**
- Überschriften: Aptos Bold
- Fliesstext: Aptos Regular
- Code: JetBrains Mono

---

## Benötigte Code-Dateien für Video

Alle Dateien sollten vor der Aufnahme vorbereitet sein:

1. **`server.js`** – Express-Server komplett
2. **`public/index.html`** – Statische HTML-Datei
3. **`public/css/style.css`** – Stylesheet
4. **`public/js/script.js`** – JavaScript-Datei
5. **Alter Code** – http-Modul Server zum Vergleich

---

**Gesamtlänge:** ca. 10-12 Minuten  
**Schwierigkeitsgrad:** Mittel  
**Tempo:** Ruhig und verständlich, mit Pausen zum Nachvollziehen
