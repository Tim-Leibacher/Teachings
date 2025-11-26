# Auftrag 3: Statische Dateien ausliefern

## Ziel

Du erstellst einen Server, der dein bestehendes Portfolio (HTML, CSS, JavaScript) ausliefert. Du lernst, wie man Dateien aus dem Dateisystem liest, den richtigen Content-Type setzt und Fehler professionell behandelt.

## Beschreibung

Bisher haben wir HTML-Code direkt im Server geschrieben. Professionelle Server liefern aber externe Dateien aus – HTML, CSS, JavaScript, Bilder, PDFs. Mit dem `fs`-Modul (File System) kannst du Dateien lesen und über den Server ausliefern. Das ist die Grundlage für echte Webanwendungen.

**Geschätzte Zeit:** 75-90 Minuten

---

## Teil 1: Projekt-Struktur aufbauen (10 Min)

### 1.1 Ordnerstruktur erstellen

```bash
# Falls noch nicht vorhanden:
mkdir portfolio-server
cd portfolio-server

# Ordner für statische Dateien erstellen
mkdir public
mkdir public/css
mkdir public/js
mkdir public/images
```

**Struktur:**
```
portfolio-server/
├── public/
│   ├── index.html
│   ├── about.html
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── script.js
│   └── images/
│       └── (später: Bilder)
├── server-static.js
└── server-routing.js (aus Auftrag 2)
```

### 1.2 HTML-Dateien erstellen

**`public/index.html`**:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio - Home</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <nav class="navbar">
        <div class="nav-container">
            <a href="/" class="nav-logo">Portfolio</a>
            <ul class="nav-menu">
                <li><a href="/" class="nav-link">Home</a></li>
                <li><a href="/about.html" class="nav-link">Über mich</a></li>
            </ul>
        </div>
    </nav>
    
    <main class="container">
        <section class="hero">
            <h1>Willkommen auf meinem Portfolio!</h1>
            <p class="lead">Mein Name ist [Dein Name] und ich bin Lernende/r im 1. Lehrjahr Applikationsentwicklung.</p>
        </section>
        
        <section class="content-section">
            <h2>Über dieses Projekt</h2>
            <p>Dieser Server läuft mit Node.js und dem http-Modul. Er liefert statische Dateien aus dem <code>public</code>-Ordner aus.</p>
            <p>Die Dateien werden dynamisch aus dem Dateisystem geladen.</p>
        </section>
        
        <section class="content-section">
            <h2>Aktuelle Server-Informationen</h2>
            <div id="server-info">Lädt...</div>
        </section>
        
        <section class="content-section">
            <h2>Interaktiver Test</h2>
            <button id="test-button" class="btn">Klick mich!</button>
            <p id="result"></p>
        </section>
    </main>
    
    <footer class="footer">
        <p>&copy; 2025 [Dein Name] | Portfolio mit Node.js</p>
    </footer>
    
    <script src="/js/script.js"></script>
</body>
</html>
```

**`public/about.html`**:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio - Über mich</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <nav class="navbar">
        <div class="nav-container">
            <a href="/" class="nav-logo">Portfolio</a>
            <ul class="nav-menu">
                <li><a href="/" class="nav-link">Home</a></li>
                <li><a href="/about.html" class="nav-link">Über mich</a></li>
            </ul>
        </div>
    </nav>
    
    <main class="container">
        <section class="hero">
            <h1>Über mich</h1>
        </section>
        
        <section class="content-section">
            <div class="about-grid">
                <div class="about-item">
                    <h3>Name</h3>
                    <p>[Dein Name]</p>
                </div>
                <div class="about-item">
                    <h3>Beruf</h3>
                    <p>Lernende/r Informatiker/in EFZ Applikationsentwicklung</p>
                </div>
                <div class="about-item">
                    <h3>Lehrjahr</h3>
                    <p>1. Lehrjahr</p>
                </div>
                <div class="about-item">
                    <h3>Ausbildungsbetrieb</h3>
                    <p>[Dein Betrieb]</p>
                </div>
            </div>
        </section>
        
        <section class="content-section">
            <h2>Was ich lerne</h2>
            <ul class="skills-list">
                <li>HTML & CSS - Webseiten strukturieren und gestalten</li>
                <li>JavaScript - Interaktivität hinzufügen</li>
                <li>Node.js - Server-Entwicklung</li>
                <li>Git - Versionsverwaltung</li>
                <li>HTTP - Wie das Web funktioniert</li>
            </ul>
        </section>
        
        <section class="content-section">
            <h2>Meine Ziele</h2>
            <p>Ich möchte moderne Webanwendungen entwickeln und die Grundlagen der Full-Stack-Entwicklung beherrschen.</p>
            <p>Aktuell arbeite ich daran, meinen eigenen HTTP-Server zu bauen und zu verstehen, wie Webserver funktionieren.</p>
        </section>
    </main>
    
    <footer class="footer">
        <p>&copy; 2025 [Dein Name] | Portfolio mit Node.js</p>
    </footer>
    
    <script src="/js/script.js"></script>
</body>
</html>
```

### 1.3 CSS erstellen

**`public/css/style.css`**:

```css
/* Reset & Base Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f5f5f5;
}

code {
    background: #e0e0e0;
    padding: 2px 6px;
    border-radius: 3px;
    font-family: monospace;
}

/* Navigation */
.navbar {
    background-color: #376B8C;
    padding: 0;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.nav-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.nav-logo {
    color: white;
    font-size: 24px;
    font-weight: bold;
    text-decoration: none;
}

.nav-menu {
    list-style: none;
    display: flex;
    gap: 30px;
}

.nav-link {
    color: white;
    text-decoration: none;
    font-weight: 500;
    transition: color 0.3s;
}

.nav-link:hover {
    color: #E87722;
}

/* Container */
.container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 40px 20px;
}

/* Hero Section */
.hero {
    background: linear-gradient(135deg, #376B8C 0%, #29786A 100%);
    color: white;
    padding: 60px 40px;
    border-radius: 8px;
    margin-bottom: 40px;
    text-align: center;
}

.hero h1 {
    font-size: 36px;
    margin-bottom: 15px;
}

.lead {
    font-size: 20px;
    font-weight: 300;
}

/* Content Sections */
.content-section {
    background: white;
    padding: 30px;
    margin-bottom: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.content-section h2 {
    color: #376B8C;
    margin-bottom: 20px;
    border-bottom: 3px solid #29786A;
    padding-bottom: 10px;
}

.content-section p {
    margin-bottom: 15px;
}

/* About Grid */
.about-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

.about-item {
    background: #f5f5f5;
    padding: 20px;
    border-radius: 4px;
    border-left: 4px solid #29786A;
}

.about-item h3 {
    color: #376B8C;
    font-size: 14px;
    text-transform: uppercase;
    margin-bottom: 10px;
}

.about-item p {
    font-size: 18px;
    margin: 0;
}

/* Skills List */
.skills-list {
    list-style: none;
    padding: 0;
}

.skills-list li {
    background: #f5f5f5;
    padding: 15px;
    margin-bottom: 10px;
    border-radius: 4px;
    border-left: 4px solid #29786A;
}

.skills-list li:before {
    content: "✓ ";
    color: #29786A;
    font-weight: bold;
    margin-right: 10px;
}

/* Button */
.btn {
    background: #376B8C;
    color: white;
    border: none;
    padding: 12px 30px;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
    transition: background 0.3s;
}

.btn:hover {
    background: #29786A;
}

/* Server Info Box */
#server-info {
    background: #f5f5f5;
    padding: 20px;
    border-radius: 4px;
    font-family: monospace;
}

#result {
    margin-top: 15px;
    padding: 15px;
    background: #e8f4f8;
    border-left: 4px solid #376B8C;
    border-radius: 4px;
    min-height: 20px;
}

/* Footer */
.footer {
    background: #333;
    color: white;
    text-align: center;
    padding: 20px;
    margin-top: 40px;
}

/* Responsive */
@media (max-width: 768px) {
    .nav-container {
        flex-direction: column;
        gap: 15px;
    }
    
    .nav-menu {
        flex-direction: column;
        gap: 10px;
        text-align: center;
    }
    
    .hero h1 {
        font-size: 28px;
    }
    
    .lead {
        font-size: 18px;
    }
}
```

### 1.4 JavaScript erstellen

**`public/js/script.js`**:

```javascript
// script.js - Client-Side JavaScript

console.log('Portfolio-JavaScript geladen!');

// Funktion: Server-Informationen abrufen
async function loadServerInfo() {
    const infoDiv = document.getElementById('server-info');
    
    if (!infoDiv) return;  // Element existiert nur auf index.html
    
    try {
        const response = await fetch('/api/stats');
        const data = await response.json();
        
        infoDiv.innerHTML = `
            <strong>Server-Status:</strong><br>
            Node.js Version: ${data.data.server.nodeVersion}<br>
            Plattform: ${data.data.server.platform}<br>
            Uptime: ${data.data.server.uptime} Sekunden<br>
            Arbeitsspeicher: ${data.data.server.memory.used} ${data.data.server.memory.unit}
        `;
    } catch (error) {
        infoDiv.innerHTML = `
            <strong>Server-Status:</strong><br>
            API nicht verfügbar (starte server-api.js auf Port 3001)
        `;
    }
}

// Button-Event
const testButton = document.getElementById('test-button');
const resultDiv = document.getElementById('result');

if (testButton && resultDiv) {
    testButton.addEventListener('click', () => {
        const now = new Date();
        resultDiv.innerHTML = `
            <strong>Button geklickt!</strong><br>
            Zeit: ${now.toLocaleTimeString('de-CH')}<br>
            JavaScript funktioniert einwandfrei!
        `;
        console.log('Test-Button wurde geklickt!');
    });
}

// Server-Info laden wenn Seite fertig geladen ist
if (document.getElementById('server-info')) {
    loadServerInfo();
}

console.log('Portfolio-Script initialisiert!');
```

---

## Teil 2: Static File Server erstellen (40 Min)

### 2.1 Server implementieren

Erstelle **`server-static.js`**:

```javascript
// server-static.js - Statische Dateien ausliefern

const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // 1. URL bereinigen und Pfad zusammenbauen
    let filePath = request.url;
    
    // Wenn nur "/" angefordert wird → index.html
    if (filePath === '/') {
        filePath = '/index.html';
    }
    
    // Vollständiger Pfad zur Datei
    filePath = path.join(__dirname, 'public', filePath);
    
    // 2. Dateiendung ermitteln für Content-Type
    const extname = path.extname(filePath).toLowerCase();
    
    // 3. Content-Type-Map
    const contentTypes = {
        '.html': 'text/html; charset=utf-8',
        '.css': 'text/css',
        '.js': 'application/javascript',
        '.json': 'application/json',
        '.png': 'image/png',
        '.jpg': 'image/jpeg',
        '.jpeg': 'image/jpeg',
        '.gif': 'image/gif',
        '.svg': 'image/svg+xml',
        '.ico': 'image/x-icon',
        '.pdf': 'application/pdf',
        '.txt': 'text/plain'
    };
    
    const contentType = contentTypes[extname] || 'application/octet-stream';
    
    // 4. Datei lesen und ausliefern
    fs.readFile(filePath, (error, content) => {
        if (error) {
            if (error.code === 'ENOENT') {
                // Datei nicht gefunden → 404
                response.statusCode = 404;
                response.setHeader('Content-Type', 'text/html; charset=utf-8');
                response.end(`
                    <!DOCTYPE html>
                    <html lang="de">
                    <head>
                        <meta charset="UTF-8">
                        <title>404 - Nicht gefunden</title>
                        <style>
                            body {
                                font-family: Arial, sans-serif;
                                max-width: 600px;
                                margin: 100px auto;
                                text-align: center;
                                padding: 20px;
                            }
                            h1 {
                                color: #E87722;
                                font-size: 72px;
                                margin: 0;
                            }
                            h2 { color: #376B8C; }
                            a {
                                display: inline-block;
                                margin-top: 20px;
                                padding: 10px 20px;
                                background: #376B8C;
                                color: white;
                                text-decoration: none;
                                border-radius: 4px;
                            }
                        </style>
                    </head>
                    <body>
                        <h1>404</h1>
                        <h2>Datei nicht gefunden</h2>
                        <p>Die Datei "${request.url}" existiert nicht.</p>
                        <a href="/">Zurück zur Startseite</a>
                    </body>
                    </html>
                `);
            } else if (error.code === 'EISDIR') {
                // Ist ein Ordner, nicht eine Datei
                response.statusCode = 403;
                response.setHeader('Content-Type', 'text/plain; charset=utf-8');
                response.end('403 Forbidden: Verzeichnisse können nicht direkt aufgerufen werden');
            } else {
                // Sonstiger Server-Fehler
                response.statusCode = 500;
                response.setHeader('Content-Type', 'text/plain; charset=utf-8');
                response.end(`500 Internal Server Error: ${error.code}`);
            }
        } else {
            // Datei erfolgreich geladen
            response.statusCode = 200;
            response.setHeader('Content-Type', contentType);
            response.end(content);
        }
    });
});

const PORT = 3000;

server.listen(PORT, () => {
    console.log(`✅ Static File Server läuft auf http://localhost:${PORT}`);
    console.log(`Dateien aus: ${path.join(__dirname, 'public')}`);
    console.log('\nVerfügbare Seiten:');
    console.log(`  - http://localhost:${PORT}/`);
    console.log(`  - http://localhost:${PORT}/about.html`);
});
```

**Was passiert hier?**

1. **URL normalisieren**: `/` wird zu `/index.html`
2. **Pfad zusammenbauen**: `__dirname + '/public' + URL`
3. **Dateiendung ermitteln**: `.html`, `.css`, `.js`, etc.
4. **Content-Type festlegen**: Richtige MIME-Types für Browser
5. **Datei lesen**: Mit `fs.readFile()` asynchron
6. **Fehlerbehandlung**:
   - `ENOENT`: Datei existiert nicht → 404
   - `EISDIR`: Ist ein Ordner → 403
   - Sonstige Fehler → 500

### 2.2 Server starten und testen

```bash
node server-static.js
```

**Im Browser testen:**
- `http://localhost:3000/` → Lädt `index.html`
- `http://localhost:3000/about.html` → Lädt `about.html`
- `http://localhost:3000/css/style.css` → Lädt CSS
- `http://localhost:3000/js/script.js` → Lädt JavaScript
- `http://localhost:3000/nichtda.html` → 404-Fehler

**Im Terminal siehst du:**
```
GET /
GET /css/style.css
GET /js/script.js
```

**Perfekt!** Der Browser lädt automatisch alle verlinkten Dateien nach.

---

## Teil 3: Erweiterte Funktionen (25 Min)

### 3.1 Logging verbessern

Erweitere den Server um besseres Logging:

```javascript
// Am Anfang von server-static.js, nach const http = require('http');

function log(message, type = 'info') {
    const timestamp = new Date().toLocaleTimeString('de-CH');
    const colors = {
        info: '\x1b[36m',    // Cyan
        success: '\x1b[32m', // Grün
        error: '\x1b[31m',   // Rot
        reset: '\x1b[0m'     // Reset
    };
    
    const color = colors[type] || colors.info;
    console.log(`${color}[${timestamp}]${colors.reset} ${message}`);
}

// Dann im createServer:
const server = http.createServer((request, response) => {
    const startTime = Date.now();
    
    // ... bestehender Code ...
    
    // Am Ende jeder Response (nach response.end()):
    response.on('finish', () => {
        const duration = Date.now() - startTime;
        const statusColor = response.statusCode < 400 ? 'success' : 'error';
        log(`${request.method} ${request.url} → ${response.statusCode} (${duration}ms)`, statusColor);
    });
});
```

### 3.2 Sicherheit: Directory Traversal verhindern

Füge Sicherheitscheck hinzu:

```javascript
// Nach: filePath = path.join(__dirname, 'public', filePath);

// Sicherheitscheck: Verhindert Zugriff ausserhalb von public/
const publicPath = path.join(__dirname, 'public');
const resolvedPath = path.resolve(filePath);

if (!resolvedPath.startsWith(publicPath)) {
    response.statusCode = 403;
    response.setHeader('Content-Type', 'text/plain');
    response.end('403 Forbidden: Zugriff verweigert');
    return;
}
```

**Was macht das?**  
Verhindert Angriffe wie `http://localhost:3000/../../../etc/passwd`

### 3.3 Cache-Headers setzen (Optional)

Für bessere Performance:

```javascript
// Nach: response.setHeader('Content-Type', contentType);

// Cache-Header setzen (nur für bestimmte Dateitypen)
if (['.css', '.js', '.png', '.jpg', '.jpeg', '.gif', '.svg'].includes(extname)) {
    // Browser darf 1 Stunde cachen
    response.setHeader('Cache-Control', 'public, max-age=3600');
}
```

---

## Erfolgskriterien

- [ ] Ordnerstruktur mit `public/` erstellt
- [ ] `index.html` und `about.html` erstellt
- [ ] `css/style.css` erstellt mit BAND Corporate Design
- [ ] `js/script.js` erstellt mit interaktiven Funktionen
- [ ] `server-static.js` lädt Dateien aus `public/`
- [ ] Server setzt korrekten Content-Type für HTML, CSS, JS
- [ ] Navigation zwischen Seiten funktioniert
- [ ] CSS wird korrekt geladen und angewendet
- [ ] JavaScript wird geladen und ausgeführt
- [ ] Button-Click-Event funktioniert
- [ ] 404-Fehler wird schön dargestellt
- [ ] Im Terminal werden alle Requests geloggt
- [ ] Sicherheitscheck gegen Directory Traversal implementiert

## Tipps

**Debugging:**
- Nutze Browser DevTools → Network-Tab
- Schaue nach 404-Fehlern bei CSS/JS
- Prüfe Content-Type in den Response-Headers

**Häufige Fehler:**
- CSS lädt nicht: Pfad in `<link>` falsch
- JS lädt nicht: Pfad in `<script>` falsch
- 404 trotz Datei: Pfad ist case-sensitive!

**Performance:**
- Cache-Headers für statische Dateien
- Komprimierung (später mit Express)
- CDN für Bibliotheken

**Sicherheit:**
- NIEMALS Dateien ausserhalb von `public/` ausliefern
- Input-Validierung
- Keine sensiblen Daten im `public/`-Ordner

**Best Practices:**
- `public/` für statische Dateien
- Klare Ordnerstruktur (css/, js/, images/)
- Konsistente Benennung

## Reflexionsfragen

1. Warum ist der Content-Type wichtig? Teste: Was passiert, wenn du CSS mit `text/plain` auslieferst?
2. Was ist der Unterschied zwischen synchronem (`fs.readFileSync`) und asynchronem (`fs.readFile`) Lesen?
3. Schaue dir `path.join()` vs. `path.resolve()` an. Was ist der Unterschied?
4. Teste: Was passiert, wenn du `http://localhost:3000/../server-static.js` aufrufst? Wird der Sicherheitscheck aktiv?
5. Öffne DevTools → Network. Welche HTTP-Headers siehst du bei CSS- und JS-Dateien?

## Weiterführende Links

- [Node.js fs Dokumentation](https://nodejs.org/docs/latest/api/fs.html) – File System
- [Node.js path Dokumentation](https://nodejs.org/docs/latest/api/path.html) – Pfad-Utilities
- [MDN: MIME Types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) – Content-Types
- [OWASP: Directory Traversal](https://owasp.org/www-community/attacks/Path_Traversal) – Sicherheit
- [HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching) – Cache-Headers

---

**⏱️ Geschätzte Zeit:** 75-90 Minuten  
**📦 Nächster Schritt:** Optional: Erweiterte Server-Features wie Datei-Upload oder WebSockets!
