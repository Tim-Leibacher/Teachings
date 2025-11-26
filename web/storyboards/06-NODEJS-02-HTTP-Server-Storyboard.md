# Storyboard: Einfache Server-Anwendung mit Node.js HTTP-Modul

**Modul:** Node.js  
**Thema:** Einfache Server-Anwendung  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Geschätzte Videolänge:** 10-12 Minuten  
**Autor:** Tim Leibacher

---

## Video-Übersicht

**Lernziele:**
- HTTP-Modul von Node.js verstehen und importieren
- Einfachen HTTP-Server erstellen und starten
- Auf Browser-Anfragen reagieren (Request/Response)
- Verschiedene URLs unterschiedlich behandeln (Routing)
- HTML-Inhalte und JSON-Daten ausliefern
- Statische Dateien aus dem Dateisystem laden und ausliefern

**Benötigte Ressourcen:**
- Terminal (Bash/PowerShell)
- VS Code mit Node.js installiert
- Portfolio-Projekt aus vorherigen Modulen
- Browser (Chrome/Firefox/Edge)

---

## Szene 1: Intro – Was ist ein HTTP-Server? (45 Sek.)

### Sprechertext
"Willkommen zum Modul über HTTP-Server mit Node.js! Bisher haben wir JavaScript-Dateien im Terminal ausgeführt. Aber wie bringst du deine Website ins Internet? Wie antwortet ein Server auf Browser-Anfragen? Genau hier kommt das HTTP-Modul ins Spiel. HTTP steht für HyperText Transfer Protocol – das Protokoll, das Browser und Server nutzen, um zu kommunizieren. Mit Node.js kannst du in wenigen Zeilen Code einen funktionsfähigen Webserver erstellen, der HTML-Seiten ausliefert, auf verschiedene URLs reagiert und Daten verarbeitet. In diesem Video bauen wir Schritt für Schritt einen Server, der dein Portfolio im Browser anzeigt."

### Bildschirmdarstellung
- BAND-Logo mit Titel: "Node.js HTTP-Server – Dein Portfolio im Web"
- Animation: Browser sendet Anfrage → Server → Antwort
- Text-Overlay:
  - "HTTP = Kommunikation zwischen Browser und Server"
  - "Node.js = Server-Entwicklung mit JavaScript"
  - "Dein Portfolio online verfügbar machen"

### Hinweise
- BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A)
- Fade-In Animation
- Grafik: Browser ↔ Server (Request/Response-Zyklus)

---

## Szene 2: HTTP-Modul importieren (30 Sek.)

### Sprechertext
"Das http-Modul ist direkt in Node.js integriert – du musst es nicht installieren. Mit `require('http')` importierst du es. Das Modul stellt alle Funktionen bereit, die du brauchst, um einen Server zu erstellen, zu starten und auf Anfragen zu reagieren. Schauen wir uns das in der Praxis an."

### Bildschirmdarstellung
VS Code mit neuer Datei **`server.js`**:

```javascript
// server.js - Mein erster HTTP-Server

// HTTP-Modul importieren (eingebaut in Node.js)
const http = require('http');

console.log('HTTP-Modul erfolgreich importiert!');
console.log('Node.js Version:', process.version);
```

Terminal parallel zeigen:

```bash
# Datei ausführen
node server.js
```

**Ausgabe:**
```
HTTP-Modul erfolgreich importiert!
Node.js Version: v20.10.0
```

### Hinweise
- Erkläre: `require()` ist CommonJS-Syntax
- Zeige: Kein `npm install` nötig – http ist eingebaut
- Text-Overlay: "http-Modul = eingebaut in Node.js"

---

## Szene 3: Server erstellen mit createServer() (1 Min. 30 Sek.)

### Sprechertext
"Jetzt erstellen wir den Server mit `http.createServer()`. Diese Funktion nimmt eine Callback-Funktion entgegen, die bei jeder Anfrage ausgeführt wird. Die Callback-Funktion erhält zwei Parameter: `request` – das ist die Anfrage vom Browser mit allen Informationen wie URL und HTTP-Methode. Und `response` – damit schickst du die Antwort zurück. Schauen wir uns das an."

### Bildschirmdarstellung
VS Code – **`server.js`** erweitern:

```javascript
// server.js - HTTP-Server erstellen

const http = require('http');

// Server erstellen
const server = http.createServer((request, response) => {
    console.log('Neue Anfrage erhalten!');
    console.log('URL:', request.url);
    console.log('Methode:', request.method);
    
    // Antwort senden
    response.statusCode = 200;  // HTTP-Status: 200 = OK
    response.setHeader('Content-Type', 'text/plain; charset=utf-8');
    response.end('Hallo vom Node.js-Server!');
});

console.log('Server-Objekt erstellt!');
```

### Bildschirmdarstellung (Fortsetzung)
Split-Screen: Code links, Erklärung rechts

**Erklärung einblenden:**
```
request  → Anfrage vom Browser
           - request.url (z.B. "/about")
           - request.method (z.B. "GET")

response → Antwort an Browser
           - response.statusCode (z.B. 200)
           - response.setHeader() (Content-Type)
           - response.end() (Inhalt senden)
```

### Hinweise
- Betone: Callback wird bei JEDER Anfrage ausgeführt
- Erkläre: HTTP-Statuscode 200 = "Alles OK"
- Text-Overlay: "Request = Anfrage | Response = Antwort"

---

## Szene 4: Server starten mit listen() (1 Min.)

### Sprechertext
"Der Server ist erstellt, aber er läuft noch nicht. Mit `server.listen()` startest du ihn auf einem bestimmten Port. Ein Port ist wie eine Tür auf deinem Computer – der Server wartet dort auf Anfragen. Port 3000 ist ein beliebter Standard für Entwicklungsserver. Sobald der Server läuft, kannst du im Browser `localhost:3000` aufrufen und siehst die Antwort."

### Bildschirmdarstellung
VS Code – **`server.js`** erweitern:

```javascript
// Server auf Port 3000 starten
const PORT = 3000;

server.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
    console.log('Drücke Ctrl+C zum Beenden');
});
```

**Vollständiger Code:**
```javascript
// server.js - Kompletter HTTP-Server

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    response.statusCode = 200;
    response.setHeader('Content-Type', 'text/plain; charset=utf-8');
    response.end('Hallo vom Node.js-Server!');
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

Terminal zeigen:

```bash
node server.js
```

**Ausgabe:**
```
Server läuft auf http://localhost:3000
```

Browser zeigen: `http://localhost:3000`

**Im Browser sichtbar:**
```
Hallo vom Node.js-Server!
```

**Im Terminal (bei jedem Browser-Reload):**
```
GET /
GET /favicon.ico
```

### Hinweise
- Erkläre: Port 3000 = Entwicklungsstandard
- Zeige: Server läuft DAUERHAFT (bis Ctrl+C)
- Betone: Jede Browser-Anfrage erscheint im Terminal
- Erkläre: `favicon.ico` = Browser fragt nach Icon

---

## Szene 5: HTML ausliefern statt Text (1 Min. 30 Sek.)

### Sprechertext
"Einfacher Text ist langweilig – liefern wir HTML aus! Ändere den Content-Type zu `text/html` und schreibe HTML-Code in `response.end()`. Jetzt kann der Browser die Seite richtig rendern mit Überschriften, Absätzen und Formatierung."

### Bildschirmdarstellung
VS Code – **`server.js`** anpassen:

```javascript
const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // HTML ausliefern
    response.statusCode = 200;
    response.setHeader('Content-Type', 'text/html; charset=utf-8');
    
    const html = `
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Mein Portfolio</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 800px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: #f5f5f5;
                }
                h1 {
                    color: #376B8C;
                }
                .info {
                    background: white;
                    padding: 20px;
                    border-radius: 8px;
                    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                }
            </style>
        </head>
        <body>
            <div class="info">
                <h1>Willkommen auf meinem Portfolio-Server!</h1>
                <p>Dieser Server läuft mit Node.js und dem http-Modul.</p>
                <p><strong>Aktuelle Zeit:</strong> ${new Date().toLocaleString('de-CH')}</p>
            </div>
        </body>
        </html>
    `;
    
    response.end(html);
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

Server neu starten:

```bash
# Alten Server stoppen: Ctrl+C
# Neu starten:
node server.js
```

Browser zeigen: `http://localhost:3000`

**Im Browser:** Formatierte HTML-Seite mit Stil!

### Hinweise
- Zeige: Template Literals (`) für mehrzeiligen HTML-Code
- Betone: Content-Type MUSS `text/html` sein
- Erkläre: Server muss neu gestartet werden nach Änderungen
- Zeige: Dynamischer Inhalt (aktuelle Zeit)

---

## Szene 6: Routing – Verschiedene URLs (2 Min.)

### Sprechertext
"Bisher antwortet der Server auf alle URLs gleich. Professionelle Server reagieren auf verschiedene URLs unterschiedlich. Das nennt man Routing. Mit `request.url` liest du die angeforderte URL aus und entscheidest, was zurückgeschickt wird. Schauen wir uns an, wie wir verschiedene Seiten erstellen."

### Bildschirmdarstellung
VS Code – **`server-routing.js`** (neue Datei):

```javascript
// server-routing.js - Server mit Routing

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    response.setHeader('Content-Type', 'text/html; charset=utf-8');
    
    // Routing: Verschiedene URLs behandeln
    if (request.url === '/' || request.url === '/home') {
        // Startseite
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Startseite</title>
            </head>
            <body>
                <h1>Startseite</h1>
                <nav>
                    <a href="/">Home</a> |
                    <a href="/about">Über mich</a> |
                    <a href="/skills">Skills</a> |
                    <a href="/contact">Kontakt</a>
                </nav>
                <p>Willkommen auf meinem Portfolio-Server!</p>
            </body>
            </html>
        `);
        
    } else if (request.url === '/about') {
        // Über-mich-Seite
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Über mich</title>
            </head>
            <body>
                <h1>Über mich</h1>
                <nav>
                    <a href="/">Home</a> |
                    <a href="/about">Über mich</a> |
                    <a href="/skills">Skills</a> |
                    <a href="/contact">Kontakt</a>
                </nav>
                <p>Ich bin Lernende/r im 1. Lehrjahr Applikationsentwicklung.</p>
                <p>Ich lerne gerade Node.js und HTTP-Server!</p>
            </body>
            </html>
        `);
        
    } else if (request.url === '/skills') {
        // Skills-Seite
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Skills</title>
            </head>
            <body>
                <h1>Meine Skills</h1>
                <nav>
                    <a href="/">Home</a> |
                    <a href="/about">Über mich</a> |
                    <a href="/skills">Skills</a> |
                    <a href="/contact">Kontakt</a>
                </nav>
                <ul>
                    <li>HTML & CSS</li>
                    <li>JavaScript</li>
                    <li>Node.js</li>
                    <li>Git</li>
                </ul>
            </body>
            </html>
        `);
        
    } else if (request.url === '/contact') {
        // Kontakt-Seite
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Kontakt</title>
            </head>
            <body>
                <h1>Kontakt</h1>
                <nav>
                    <a href="/">Home</a> |
                    <a href="/about">Über mich</a> |
                    <a href="/skills">Skills</a> |
                    <a href="/contact">Kontakt</a>
                </nav>
                <p>Email: dein-name@example.com</p>
                <p>GitHub: github.com/dein-username</p>
            </body>
            </html>
        `);
        
    } else {
        // 404 - Seite nicht gefunden
        response.statusCode = 404;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>404 - Nicht gefunden</title>
            </head>
            <body>
                <h1>404 - Seite nicht gefunden</h1>
                <p>Die Seite "${request.url}" existiert nicht.</p>
                <a href="/">Zurück zur Startseite</a>
            </body>
            </html>
        `);
    }
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server mit Routing läuft auf http://localhost:${PORT}`);
});
```

Terminal zeigen:

```bash
node server-routing.js
```

Browser zeigen:
- `http://localhost:3000/` → Startseite
- `http://localhost:3000/about` → Über mich
- `http://localhost:3000/skills` → Skills
- `http://localhost:3000/irgendwas` → 404-Fehler

### Hinweise
- Betone: if/else für verschiedene URLs
- Zeige: Statuscode 404 für nicht gefundene Seiten
- Erkläre: Navigation funktioniert mit normalen Links
- Text-Overlay: "Routing = URL → passende Antwort"

---

## Szene 7: JSON-Daten ausliefern (1 Min. 30 Sek.)

### Sprechertext
"Server liefern nicht nur HTML aus – oft werden Daten als JSON geschickt. Das ist wichtig für APIs. Ändere den Content-Type zu `application/json` und schicke JSON-Daten mit `JSON.stringify()`. Browser und andere Programme können diese Daten dann weiterverarbeiten."

### Bildschirmdarstellung
VS Code – **`server-json.js`** (neue Datei):

```javascript
// server-json.js - Server mit JSON-API

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    if (request.url === '/api/skills') {
        // JSON-Daten zurückgeben
        response.statusCode = 200;
        response.setHeader('Content-Type', 'application/json; charset=utf-8');
        
        const skills = {
            status: 'success',
            data: [
                { name: 'HTML', level: 4, kategorie: 'Frontend' },
                { name: 'CSS', level: 4, kategorie: 'Frontend' },
                { name: 'JavaScript', level: 3, kategorie: 'Frontend' },
                { name: 'Node.js', level: 2, kategorie: 'Backend' },
                { name: 'Git', level: 3, kategorie: 'Tools' }
            ],
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(skills, null, 2));
        
    } else if (request.url === '/api/info') {
        response.statusCode = 200;
        response.setHeader('Content-Type', 'application/json; charset=utf-8');
        
        const info = {
            name: 'Dein Name',
            beruf: 'Lernende/r Applikationsentwicklung',
            lehrjahr: 1,
            skills: ['HTML', 'CSS', 'JavaScript', 'Node.js'],
            hobbies: ['Programmieren', 'Gaming', 'Sport']
        };
        
        response.end(JSON.stringify(info, null, 2));
        
    } else {
        // API-Übersicht
        response.statusCode = 200;
        response.setHeader('Content-Type', 'application/json; charset=utf-8');
        
        const api = {
            message: 'Willkommen zur Portfolio-API',
            endpoints: [
                { url: '/api/info', beschreibung: 'Persönliche Informationen' },
                { url: '/api/skills', beschreibung: 'Liste aller Skills' }
            ]
        };
        
        response.end(JSON.stringify(api, null, 2));
    }
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`JSON-API läuft auf http://localhost:${PORT}`);
});
```

Terminal:

```bash
node server-json.js
```

Browser zeigen:
- `http://localhost:3000/` → API-Übersicht
- `http://localhost:3000/api/skills` → Skills als JSON
- `http://localhost:3000/api/info` → Info als JSON

### Hinweise
- Betone: `JSON.stringify()` konvertiert Objekt → String
- Zeige: Content-Type MUSS `application/json` sein
- Erkläre: Parameter `null, 2` = schöne Formatierung
- Text-Overlay: "JSON = Datenformat für APIs"

---

## Szene 8: Statische Dateien ausliefern (2 Min.)

### Sprechertext
"Professionelle Server liefern auch Dateien aus – HTML, CSS, Bilder. Mit dem `fs`-Modul liest du Dateien aus dem Dateisystem und schickst sie als Antwort. Wichtig ist der richtige Content-Type, damit der Browser weiss, wie die Datei zu interpretieren ist. Schauen wir uns das an."

### Bildschirmdarstellung
VS Code – Projektstruktur zeigen:

```
portfolio-server/
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
└── server-static.js
```

**`public/index.html`** erstellen:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio</title>
    <link rel="stylesheet" href="/style.css">
</head>
<body>
    <header>
        <h1>Mein Portfolio</h1>
        <nav>
            <a href="/">Home</a>
            <a href="/about.html">Über mich</a>
        </nav>
    </header>
    <main>
        <p>Willkommen auf meinem Portfolio!</p>
        <button id="btn">Klick mich!</button>
    </main>
    <script src="/script.js"></script>
</body>
</html>
```

**`public/style.css`**:

```css
body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: 50px auto;
    padding: 20px;
    background-color: #f5f5f5;
}

h1 {
    color: #376B8C;
}

button {
    background-color: #29786A;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #1d5a4f;
}
```

**`public/script.js`**:

```javascript
document.getElementById('btn').addEventListener('click', () => {
    alert('Hallo vom Node.js-Server!');
});
```

**`server-static.js`**:

```javascript
// server-static.js - Statische Dateien ausliefern

const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // Dateiname aus URL extrahieren
    let filePath = request.url === '/' ? '/index.html' : request.url;
    filePath = path.join(__dirname, 'public', filePath);
    
    // Dateiendung ermitteln
    const extname = path.extname(filePath);
    
    // Content-Type basierend auf Dateiendung
    const contentTypes = {
        '.html': 'text/html; charset=utf-8',
        '.css': 'text/css',
        '.js': 'application/javascript',
        '.json': 'application/json',
        '.png': 'image/png',
        '.jpg': 'image/jpeg',
        '.gif': 'image/gif',
        '.svg': 'image/svg+xml'
    };
    
    const contentType = contentTypes[extname] || 'text/plain';
    
    // Datei lesen und ausliefern
    fs.readFile(filePath, (error, content) => {
        if (error) {
            if (error.code === 'ENOENT') {
                // Datei nicht gefunden
                response.statusCode = 404;
                response.setHeader('Content-Type', 'text/html; charset=utf-8');
                response.end('<h1>404 - Datei nicht gefunden</h1>');
            } else {
                // Server-Fehler
                response.statusCode = 500;
                response.setHeader('Content-Type', 'text/plain; charset=utf-8');
                response.end(`Server-Fehler: ${error.code}`);
            }
        } else {
            // Datei erfolgreich gelesen
            response.statusCode = 200;
            response.setHeader('Content-Type', contentType);
            response.end(content);
        }
    });
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Static File Server läuft auf http://localhost:${PORT}`);
    console.log(`Dateien aus dem Ordner: ${path.join(__dirname, 'public')}`);
});
```

Terminal:

```bash
node server-static.js
```

Browser zeigen:
- `http://localhost:3000/` → Lädt index.html
- index.html lädt automatisch style.css und script.js
- Button klicken → Alert erscheint

Terminal zeigt:

```
GET /
GET /style.css
GET /script.js
```

### Hinweise
- Erkläre: `fs.readFile()` ist asynchron
- Zeige: Content-Type muss zur Dateiendung passen
- Betone: Browser lädt automatisch CSS und JS nach
- Text-Overlay: "Static Files = HTML, CSS, JS, Bilder"

---

## Szene 9: HTTP-Statuscodes verstehen (1 Min.)

### Sprechertext
"HTTP-Statuscodes sagen dem Browser, ob die Anfrage erfolgreich war. 200 bedeutet OK, 404 bedeutet nicht gefunden, 500 ist ein Server-Fehler. Es gibt viele weitere Codes: 301 für Weiterleitung, 403 für keine Berechtigung, 400 für fehlerhafte Anfrage. Als Entwickler solltest du die wichtigsten kennen und richtig einsetzen."

### Bildschirmdarstellung
Text-Overlay mit Tabelle:

```
╔═══════════════════════════════════════════════╗
║   HTTP-Statuscodes (Auswahl)                  ║
╠═══════════════════════════════════════════════╣
║   2xx = Erfolg                                ║
║   200  OK (Anfrage erfolgreich)               ║
║   201  Created (Ressource erstellt)           ║
╠═══════════════════════════════════════════════╣
║   3xx = Weiterleitung                         ║
║   301  Moved Permanently (Dauerhafte URL)     ║
║   302  Found (Temporäre Weiterleitung)        ║
╠═══════════════════════════════════════════════╣
║   4xx = Client-Fehler                         ║
║   400  Bad Request (Fehlerhafte Anfrage)      ║
║   404  Not Found (Seite nicht gefunden)       ║
║   403  Forbidden (Keine Berechtigung)         ║
╠═══════════════════════════════════════════════╣
║   5xx = Server-Fehler                         ║
║   500  Internal Server Error                  ║
║   503  Service Unavailable (Server überlast.) ║
╚═══════════════════════════════════════════════╝
```

### Hinweise
- Betone: 2xx = Erfolg, 4xx = Client-Problem, 5xx = Server-Problem
- Zeige Beispiele im Browser Developer Tools (Network-Tab)

---

## Szene 10: Zusammenfassung & Ausblick (45 Sek.)

### Sprechertext
"Fassen wir zusammen: Mit dem http-Modul kannst du in Node.js einen vollständigen Webserver erstellen. Du importierst das Modul, erstellst einen Server mit createServer, reagierst auf Anfragen mit Request und Response, und startest den Server mit listen. Du kannst HTML und JSON ausliefern, verschiedene URLs behandeln, statische Dateien laden und HTTP-Statuscodes richtig einsetzen. Das http-Modul ist mächtig, aber auch umständlich. Deshalb gibt es Express.js – ein Framework, das alles vereinfacht. Im nächsten Modul lernst du Express kennen und wirst sehen, wie viel einfacher Serverentwicklung damit wird!"

### Bildschirmdarstellung
Zusammenfassung als Checkliste:

```
✓ HTTP-Modul importieren (require('http'))
✓ Server erstellen (http.createServer)
✓ Request & Response verstehen
✓ Server starten (server.listen)
✓ HTML und JSON ausliefern
✓ Routing (verschiedene URLs)
✓ Statische Dateien laden (mit fs)
✓ HTTP-Statuscodes richtig nutzen
```

Text-Overlay:
- "Nächster Schritt: Express.js"
- "Express = Vereinfachtes Server-Framework"

### Hinweise
- Fade-Out mit BAND-Gradient
- Call-to-Action: "Jetzt selbst ausprobieren!"

---

## Zusatzmaterialien für Video-Produktion

### Terminal-Setup

**Empfohlene Einstellungen:**
- Schriftgrösse: 18-20pt
- Font: JetBrains Mono oder Fira Code
- Theme: Dunkel mit guter Lesbarkeit
- Prompt: Verkürzt, nur Ordnername sichtbar

**PS1 setzen (Bash):**
```bash
export PS1="\[\033[01;34m\]\W\[\033[00m\]\$ "
```

**PowerShell Prompt:**
```powershell
function prompt { "PS $($PWD.Path.Split('\')[-1])> " }
```

### VS Code Setup

- Theme: Dark+ oder Material Theme
- Font Size: 16-18pt
- Minimap ausblenden
- Breadcrumbs einblenden
- Extensions: ESLint, Prettier (für sauberen Code)

### Browser Developer Tools

Zeige bei Bedarf:
- Network-Tab: HTTP-Requests und Statuscodes
- Console: Fehler und Logs
- Elements: HTML-Struktur

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

### Animation Guidelines

- Fade-In-Duration: 0.3s
- Highlight-Color: #E87722 (Orange)
- Code-Highlighting: VS Code Dark+ Theme
- Cursor-Bewegung: Smooth, nicht zu schnell

---

## Benötigte Code-Dateien für Video

Alle Dateien sollten vor der Aufnahme vorbereitet sein:

1. **`server.js`** – Basis-Server
2. **`server-routing.js`** – Server mit Routing
3. **`server-json.js`** – JSON-API
4. **`server-static.js`** – Static File Server
5. **`public/index.html`** – HTML-Datei
6. **`public/style.css`** – CSS-Datei
7. **`public/script.js`** – JavaScript-Datei

---

**Gesamtlänge:** ca. 10-12 Minuten  
**Schwierigkeitsgrad:** Mittel  
**Tempo:** Ruhig und verständlich, mit Pausen zum Nachvollziehen
