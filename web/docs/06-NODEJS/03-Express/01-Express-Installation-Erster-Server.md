# Auftrag 1: Express.js installieren und ersten Server erstellen

## Ziel

Du installierst Express.js in deinem Projekt, erstellst deinen ersten Express-Server und verstehst die grundlegenden Unterschiede zum http-Modul.

## Beschreibung

Express.js ist das meistgenutzte Web-Framework für Node.js. Es vereinfacht die Server-Entwicklung erheblich: Routing wird übersichtlicher, Content-Types werden automatisch gesetzt, und viele Aufgaben, die du bisher manuell erledigt hast, übernimmt Express für dich. In diesem Auftrag installierst du Express und erstellst deinen ersten funktionierenden Server.

**Geschätzte Zeit:** 30 Minuten

---

## Teil 1: Projekt vorbereiten (5 Min)

### 1.1 Neuen Projektordner erstellen

Erstelle einen neuen Ordner für dein Express-Portfolio-Projekt:

```bash
# Neuen Ordner erstellen
mkdir portfolio-express
cd portfolio-express

# VS Code öffnen
code .
```

### 1.2 NPM-Projekt initialisieren

```bash
npm init -y
```

Öffne die erstellte **`package.json`** und passe sie an:

```json
{
  "name": "portfolio-express",
  "version": "1.0.0",
  "description": "Mein Portfolio mit Express.js",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Dein Name",
  "license": "ISC"
}
```

---

## Teil 2: Express installieren (5 Min)

### 2.1 Express als Dependency hinzufügen

```bash
npm install express
```

**Erwartete Ausgabe:**
```
added 65 packages in 2s
```

### 2.2 Installation überprüfen

Prüfe, ob Express in der **`package.json`** erscheint:

```json
{
  "dependencies": {
    "express": "^4.21.0"
  }
}
```

Im Ordner sollte nun ein **`node_modules`**-Ordner existieren.

### 2.3 .gitignore erstellen

Erstelle eine **`.gitignore`**-Datei:

```gitignore
# Dependencies
node_modules/

# Logs
npm-debug.log*

# Environment
.env

# OS
.DS_Store
Thumbs.db
```

---

## Teil 3: Erster Express-Server (10 Min)

### 3.1 Server-Datei erstellen

Erstelle eine Datei **`server.js`**:

```javascript
// server.js - Mein erster Express-Server

// Express importieren
const express = require('express');

// Express-Applikation erstellen
const app = express();

// Port definieren
const PORT = 3000;

// Erste Route: Startseite
app.get('/', (req, res) => {
    res.send('<h1>Willkommen auf meinem Portfolio!</h1>');
});

// Server starten
app.listen(PORT, () => {
    console.log(`Express-Server läuft auf http://localhost:${PORT}`);
});
```

### 3.2 Server starten

```bash
node server.js
```

**Erwartete Ausgabe:**
```
Express-Server läuft auf http://localhost:3000
```

Öffne im Browser: `http://localhost:3000`

### 3.3 Code-Erklärung

| Code | Erklärung |
|------|-----------|
| `require('express')` | Express-Modul importieren |
| `express()` | Express-Applikation erstellen |
| `app.get('/', ...)` | GET-Route für Pfad "/" definieren |
| `res.send()` | Antwort an Browser senden |
| `app.listen()` | Server auf Port starten |

---

## Teil 4: Mehrere Routen hinzufügen (10 Min)

### 4.1 Portfolio-Routen erstellen

Erweitere **`server.js`** mit deinen persönlichen Informationen:

```javascript
// server.js - Express-Server mit Portfolio-Routen

const express = require('express');
const app = express();
const PORT = 3000;

// === HTML-Routen ===

// Startseite
app.get('/', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Portfolio - Home</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                nav {
                    background: #376B8C;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 20px;
                }
                nav a {
                    color: white;
                    text-decoration: none;
                    margin-right: 15px;
                }
                nav a:hover {
                    text-decoration: underline;
                }
                h1 { color: #376B8C; }
            </style>
        </head>
        <body>
            <nav>
                <a href="/">Home</a>
                <a href="/about">Über mich</a>
                <a href="/skills">Skills</a>
                <a href="/projects">Projekte</a>
                <a href="/contact">Kontakt</a>
            </nav>
            <h1>Willkommen auf meinem Portfolio</h1>
            <p>Ich bin Lernende/r im 1. Lehrjahr Informatik EFZ Applikationsentwicklung.</p>
            <p>Diese Seite wird mit Express.js ausgeliefert!</p>
        </body>
        </html>
    `);
});

// Über mich
app.get('/about', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Portfolio - Über mich</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                nav {
                    background: #376B8C;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 20px;
                }
                nav a {
                    color: white;
                    text-decoration: none;
                    margin-right: 15px;
                }
                h1 { color: #376B8C; }
                .info-box {
                    background: white;
                    padding: 20px;
                    border-radius: 4px;
                    margin-top: 20px;
                }
            </style>
        </head>
        <body>
            <nav>
                <a href="/">Home</a>
                <a href="/about">Über mich</a>
                <a href="/skills">Skills</a>
                <a href="/projects">Projekte</a>
                <a href="/contact">Kontakt</a>
            </nav>
            <h1>Über mich</h1>
            <div class="info-box">
                <p><strong>Name:</strong> [Dein Name]</p>
                <p><strong>Ausbildung:</strong> Informatiker/in EFZ Applikationsentwicklung</p>
                <p><strong>Lehrjahr:</strong> 1. Lehrjahr</p>
                <p><strong>Betrieb:</strong> [Dein Lehrbetrieb]</p>
            </div>
        </body>
        </html>
    `);
});

// Skills
app.get('/skills', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Portfolio - Skills</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                nav {
                    background: #376B8C;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 20px;
                }
                nav a {
                    color: white;
                    text-decoration: none;
                    margin-right: 15px;
                }
                h1 { color: #376B8C; }
                .skill-category {
                    background: white;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 15px;
                }
                .skill-category h3 {
                    color: #29786A;
                    margin-top: 0;
                }
            </style>
        </head>
        <body>
            <nav>
                <a href="/">Home</a>
                <a href="/about">Über mich</a>
                <a href="/skills">Skills</a>
                <a href="/projects">Projekte</a>
                <a href="/contact">Kontakt</a>
            </nav>
            <h1>Meine Skills</h1>
            <div class="skill-category">
                <h3>Frontend</h3>
                <ul>
                    <li>HTML5</li>
                    <li>CSS3</li>
                    <li>JavaScript</li>
                </ul>
            </div>
            <div class="skill-category">
                <h3>Backend</h3>
                <ul>
                    <li>Node.js</li>
                    <li>Express.js (neu!)</li>
                </ul>
            </div>
            <div class="skill-category">
                <h3>Tools</h3>
                <ul>
                    <li>Git</li>
                    <li>VS Code</li>
                    <li>Terminal</li>
                </ul>
            </div>
        </body>
        </html>
    `);
});

// Projekte
app.get('/projects', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Portfolio - Projekte</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                nav {
                    background: #376B8C;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 20px;
                }
                nav a {
                    color: white;
                    text-decoration: none;
                    margin-right: 15px;
                }
                h1 { color: #376B8C; }
                .project {
                    background: white;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 15px;
                    border-left: 4px solid #E87722;
                }
                .project h3 { margin-top: 0; }
                .status {
                    display: inline-block;
                    padding: 3px 8px;
                    border-radius: 3px;
                    font-size: 12px;
                }
                .status-progress { background: #FFF3CD; color: #856404; }
                .status-done { background: #D4EDDA; color: #155724; }
            </style>
        </head>
        <body>
            <nav>
                <a href="/">Home</a>
                <a href="/about">Über mich</a>
                <a href="/skills">Skills</a>
                <a href="/projects">Projekte</a>
                <a href="/contact">Kontakt</a>
            </nav>
            <h1>Meine Projekte</h1>
            <div class="project">
                <h3>Portfolio-Website</h3>
                <span class="status status-progress">In Arbeit</span>
                <p>Persönliche Portfolio-Seite mit Express.js Backend.</p>
                <p><strong>Technologien:</strong> HTML, CSS, JavaScript, Node.js, Express</p>
            </div>
            <div class="project">
                <h3>HTTP-Server</h3>
                <span class="status status-done">Abgeschlossen</span>
                <p>Server mit dem Node.js http-Modul erstellt.</p>
                <p><strong>Technologien:</strong> Node.js, HTTP-Modul</p>
            </div>
        </body>
        </html>
    `);
});

// Kontakt
app.get('/contact', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Portfolio - Kontakt</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                nav {
                    background: #376B8C;
                    padding: 15px;
                    border-radius: 4px;
                    margin-bottom: 20px;
                }
                nav a {
                    color: white;
                    text-decoration: none;
                    margin-right: 15px;
                }
                h1 { color: #376B8C; }
                .contact-info {
                    background: white;
                    padding: 20px;
                    border-radius: 4px;
                }
            </style>
        </head>
        <body>
            <nav>
                <a href="/">Home</a>
                <a href="/about">Über mich</a>
                <a href="/skills">Skills</a>
                <a href="/projects">Projekte</a>
                <a href="/contact">Kontakt</a>
            </nav>
            <h1>Kontakt</h1>
            <div class="contact-info">
                <p><strong>Email:</strong> deine.email@example.com</p>
                <p><strong>GitHub:</strong> github.com/deinusername</p>
                <p><strong>LinkedIn:</strong> linkedin.com/in/deinprofil</p>
            </div>
        </body>
        </html>
    `);
});

// Server starten
app.listen(PORT, () => {
    console.log(`Express-Server läuft auf http://localhost:${PORT}`);
    console.log('Verfügbare Routen:');
    console.log('  - http://localhost:3000/');
    console.log('  - http://localhost:3000/about');
    console.log('  - http://localhost:3000/skills');
    console.log('  - http://localhost:3000/projects');
    console.log('  - http://localhost:3000/contact');
});
```

### 4.2 Server neu starten und testen

```bash
# Server stoppen (Ctrl+C) und neu starten
node server.js
```

Teste alle Routen im Browser und prüfe die Navigation.

---

## Erfolgskriterien

- [ ] Neuer Projektordner `portfolio-express` erstellt
- [ ] NPM-Projekt mit `npm init -y` initialisiert
- [ ] Express mit `npm install express` installiert
- [ ] Express erscheint in `package.json` unter dependencies
- [ ] `.gitignore` erstellt mit `node_modules/`
- [ ] `server.js` erstellt mit Express-App
- [ ] Mindestens 5 Routen definiert (/, /about, /skills, /projects, /contact)
- [ ] Navigation zwischen allen Seiten funktioniert
- [ ] Server startet ohne Fehler auf Port 3000
- [ ] Persönliche Informationen eingefügt (Name, Skills, etc.)

## Tipps

**Server automatisch neu starten:**
Du musst den Server nach jeder Änderung manuell neu starten. Im nächsten Modul lernst du nodemon kennen, das den Server automatisch neu startet.

**Port bereits belegt?**
```bash
# Anderen Port nutzen
const PORT = 3001;
```

**Konsole nutzen:**
```javascript
app.get('/test', (req, res) => {
    console.log('Route /test wurde aufgerufen');
    console.log('Request-URL:', req.url);
    console.log('Request-Methode:', req.method);
    res.send('Test erfolgreich!');
});
```

**HTML in Template-Strings:**
Nutze Backticks (\`) für mehrzeilige HTML-Strings. So kannst du HTML übersichtlich formatieren.

## Reflexionsfragen

1. Was ist der Hauptunterschied zwischen `http.createServer()` und `express()`?
2. Warum brauchst du bei Express kein `res.setHeader('Content-Type', ...)` für HTML?
3. Was passiert, wenn du eine Route aufrufst, die nicht definiert ist?
4. Vergleiche den Code-Umfang: Wie viele Zeilen hast du mit dem http-Modul für 5 Routen gebraucht vs. mit Express?
5. Teste: Was passiert, wenn du zwei app.get() mit dem gleichen Pfad definierst?

## Weiterführende Links

- [Express.js Dokumentation](https://expressjs.com/) - Offizielle Dokumentation
- [Express Getting Started](https://expressjs.com/en/starter/installing.html) - Einstieg
- [NPM Express](https://www.npmjs.com/package/express) - NPM-Seite
- [MDN Express Tutorial](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs) - MDN Tutorial

---

**Geschätzte Zeit:** 30 Minuten  
**Nächster Schritt:** In Auftrag 2 lernst du JSON-APIs und statische Dateien mit Express!
