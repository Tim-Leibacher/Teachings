# Auftrag 2: JSON-APIs und statische Dateien mit Express

## Ziel

Du erstellst eine JSON-API für dein Portfolio und lernst, statische Dateien (HTML, CSS, JavaScript, Bilder) mit Express auszuliefern. Am Ende hast du einen Server, der sowohl eine API als auch eine vollständige Website bereitstellt.

## Beschreibung

Express bietet zwei mächtige Features: `res.json()` für APIs und `express.static()` für statische Dateien. Statt Content-Types manuell zu setzen oder Dateien mit dem fs-Modul zu lesen, übernimmt Express diese Aufgaben automatisch. In diesem Auftrag trennst du dein HTML vom Server-Code und erstellst eine professionelle Projektstruktur.

**Geschätzte Zeit:** 45 Minuten

---

## Teil 1: JSON-API erstellen (15 Min)

### 1.1 API-Routen hinzufügen

Erweitere deine **`server.js`** mit API-Routen. Füge diese vor den HTML-Routen hinzu:

```javascript
// server.js - Express-Server mit JSON-API

const express = require('express');
const app = express();
const PORT = 3000;

// === JSON-API-Routen ===

// API: Persönliche Informationen
app.get('/api/info', (req, res) => {
    const info = {
        name: 'Dein Name',
        role: 'Informatiker/in EFZ Applikationsentwicklung',
        year: 1,
        company: 'Dein Lehrbetrieb',
        email: 'deine.email@example.com',
        github: 'github.com/deinusername'
    };
    res.json(info);
});

// API: Alle Skills
app.get('/api/skills', (req, res) => {
    const skills = {
        frontend: [
            { name: 'HTML', level: 80 },
            { name: 'CSS', level: 70 },
            { name: 'JavaScript', level: 60 }
        ],
        backend: [
            { name: 'Node.js', level: 50 },
            { name: 'Express.js', level: 40 }
        ],
        tools: [
            { name: 'Git', level: 60 },
            { name: 'VS Code', level: 90 },
            { name: 'Terminal', level: 50 }
        ]
    };
    res.json(skills);
});

// API: Alle Projekte
app.get('/api/projects', (req, res) => {
    const projects = [
        {
            id: 1,
            title: 'Portfolio-Website',
            description: 'Persönliche Portfolio-Seite mit Express.js Backend',
            technologies: ['HTML', 'CSS', 'JavaScript', 'Node.js', 'Express'],
            status: 'in-progress',
            github: 'github.com/username/portfolio'
        },
        {
            id: 2,
            title: 'HTTP-Server',
            description: 'Server mit dem Node.js http-Modul',
            technologies: ['Node.js', 'HTTP-Modul'],
            status: 'completed',
            github: null
        },
        {
            id: 3,
            title: 'Todo-App',
            description: 'Einfache Todo-Anwendung mit localStorage',
            technologies: ['HTML', 'CSS', 'JavaScript'],
            status: 'planned',
            github: null
        }
    ];
    res.json(projects);
});

// API: Einzelnes Projekt nach ID
app.get('/api/projects/:id', (req, res) => {
    const projectId = parseInt(req.params.id);
    
    // Projekte-Array (normalerweise aus Datenbank)
    const projects = [
        { id: 1, title: 'Portfolio-Website', status: 'in-progress' },
        { id: 2, title: 'HTTP-Server', status: 'completed' },
        { id: 3, title: 'Todo-App', status: 'planned' }
    ];
    
    const project = projects.find(p => p.id === projectId);
    
    if (project) {
        res.json(project);
    } else {
        res.status(404).json({ 
            error: 'Projekt nicht gefunden',
            requestedId: projectId 
        });
    }
});

// API: Server-Status
app.get('/api/status', (req, res) => {
    res.json({
        status: 'online',
        timestamp: new Date().toISOString(),
        uptime: process.uptime(),
        nodeVersion: process.version
    });
});

// Server starten (vorerst ohne HTML-Routen)
app.listen(PORT, () => {
    console.log(`API-Server läuft auf http://localhost:${PORT}`);
    console.log('API-Endpoints:');
    console.log('  - GET /api/info');
    console.log('  - GET /api/skills');
    console.log('  - GET /api/projects');
    console.log('  - GET /api/projects/:id');
    console.log('  - GET /api/status');
});
```

### 1.2 API testen

Starte den Server und teste die Endpoints im Browser:

```bash
node server.js
```

**Teste diese URLs:**
- `http://localhost:3000/api/info`
- `http://localhost:3000/api/skills`
- `http://localhost:3000/api/projects`
- `http://localhost:3000/api/projects/1`
- `http://localhost:3000/api/projects/99` (sollte 404 zurückgeben)
- `http://localhost:3000/api/status`

### 1.3 res.json() verstehen

| Feature | Beschreibung |
|---------|--------------|
| Automatischer Content-Type | `application/json; charset=utf-8` wird gesetzt |
| Automatische Konvertierung | JavaScript-Objekt wird zu JSON |
| Keine Formatierung nötig | `JSON.stringify()` wird intern aufgerufen |

---

## Teil 2: Projektstruktur für statische Dateien (10 Min)

### 2.1 Ordnerstruktur erstellen

Erstelle folgende Struktur in deinem Projektordner:

```
portfolio-express/
├── server.js
├── package.json
├── .gitignore
└── public/
    ├── index.html
    ├── about.html
    ├── skills.html
    ├── projects.html
    ├── contact.html
    ├── css/
    │   └── style.css
    └── js/
        └── app.js
```

Befehle zum Erstellen:

```bash
# public-Ordner mit Unterordnern erstellen
mkdir -p public/css public/js
```

### 2.2 express.static() einrichten

Füge in **`server.js`** nach `const app = express();` hinzu:

```javascript
const path = require('path');

// Statische Dateien aus dem 'public'-Ordner ausliefern
app.use(express.static(path.join(__dirname, 'public')));
```

**Was passiert hier?**
- `path.join(__dirname, 'public')` erstellt den absoluten Pfad zum public-Ordner
- `express.static()` konfiguriert Express, Dateien aus diesem Ordner auszuliefern
- `app.use()` aktiviert die Middleware für alle Anfragen

---

## Teil 3: Statische HTML-Dateien erstellen (15 Min)

### 3.1 public/index.html

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
        <a href="/" class="nav-brand">Mein Portfolio</a>
        <div class="nav-links">
            <a href="/">Home</a>
            <a href="/about.html">Über mich</a>
            <a href="/skills.html">Skills</a>
            <a href="/projects.html">Projekte</a>
            <a href="/contact.html">Kontakt</a>
        </div>
    </nav>

    <main class="container">
        <section class="hero">
            <h1>Willkommen auf meinem Portfolio</h1>
            <p class="lead">Ich bin Lernende/r im 1. Lehrjahr Informatik EFZ Applikationsentwicklung.</p>
            <p>Diese Seite wird mit Express.js ausgeliefert!</p>
        </section>

        <section class="api-demo">
            <h2>API-Demo</h2>
            <p>Dieser Server bietet auch eine JSON-API:</p>
            <div class="api-buttons">
                <button onclick="loadAPI('/api/info')">Info laden</button>
                <button onclick="loadAPI('/api/skills')">Skills laden</button>
                <button onclick="loadAPI('/api/projects')">Projekte laden</button>
                <button onclick="loadAPI('/api/status')">Status laden</button>
            </div>
            <pre id="api-output">Klicke einen Button, um API-Daten zu laden...</pre>
        </section>
    </main>

    <footer class="footer">
        <p>Portfolio erstellt mit Express.js</p>
    </footer>

    <script src="/js/app.js"></script>
</body>
</html>
```

### 3.2 public/css/style.css

```css
/* style.css - Portfolio Stylesheet */

/* === Reset & Grundlagen === */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Arial, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f5f5f5;
}

/* === Navigation === */
.navbar {
    background: #376B8C;
    padding: 15px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.nav-brand {
    color: white;
    font-size: 1.5rem;
    font-weight: bold;
    text-decoration: none;
}

.nav-links a {
    color: white;
    text-decoration: none;
    margin-left: 20px;
    transition: opacity 0.3s;
}

.nav-links a:hover {
    opacity: 0.8;
    text-decoration: underline;
}

/* === Container === */
.container {
    max-width: 900px;
    margin: 0 auto;
    padding: 30px 20px;
}

/* === Hero Section === */
.hero {
    background: white;
    padding: 40px;
    border-radius: 8px;
    margin-bottom: 30px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.hero h1 {
    color: #376B8C;
    margin-bottom: 15px;
}

.lead {
    font-size: 1.2rem;
    color: #666;
}

/* === API Demo === */
.api-demo {
    background: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.api-demo h2 {
    color: #29786A;
    margin-bottom: 15px;
}

.api-buttons {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin: 20px 0;
}

.api-buttons button {
    background: #E87722;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    transition: background 0.3s;
}

.api-buttons button:hover {
    background: #d16a1c;
}

#api-output {
    background: #2d2d2d;
    color: #f8f8f2;
    padding: 20px;
    border-radius: 4px;
    overflow-x: auto;
    font-family: 'Consolas', monospace;
    font-size: 14px;
    max-height: 400px;
    overflow-y: auto;
}

/* === Cards === */
.card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    margin-bottom: 20px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.card h3 {
    color: #376B8C;
    margin-bottom: 10px;
}

/* === Skills === */
.skill-bar {
    background: #e0e0e0;
    border-radius: 10px;
    height: 20px;
    margin: 10px 0;
    overflow: hidden;
}

.skill-fill {
    background: linear-gradient(90deg, #376B8C, #29786A);
    height: 100%;
    border-radius: 10px;
    transition: width 0.5s ease;
}

/* === Footer === */
.footer {
    background: #333;
    color: white;
    text-align: center;
    padding: 20px;
    margin-top: 50px;
}

/* === Info Box === */
.info-box {
    background: #f8f9fa;
    border-left: 4px solid #376B8C;
    padding: 15px;
    margin: 15px 0;
}

/* === Status Badge === */
.status {
    display: inline-block;
    padding: 3px 10px;
    border-radius: 12px;
    font-size: 12px;
    font-weight: bold;
}

.status-progress {
    background: #FFF3CD;
    color: #856404;
}

.status-done {
    background: #D4EDDA;
    color: #155724;
}

.status-planned {
    background: #CCE5FF;
    color: #004085;
}
```

### 3.3 public/js/app.js

```javascript
// app.js - Portfolio JavaScript

// API-Daten laden und anzeigen
async function loadAPI(endpoint) {
    const output = document.getElementById('api-output');
    
    try {
        output.textContent = 'Lade Daten...';
        
        const response = await fetch(endpoint);
        const data = await response.json();
        
        // JSON formatiert anzeigen
        output.textContent = JSON.stringify(data, null, 2);
        
        console.log(`API ${endpoint} geladen:`, data);
        
    } catch (error) {
        output.textContent = `Fehler: ${error.message}`;
        console.error('API-Fehler:', error);
    }
}

// Seite geladen
document.addEventListener('DOMContentLoaded', () => {
    console.log('Portfolio geladen!');
    console.log('Express-Server liefert statische Dateien aus.');
});
```

### 3.4 Weitere HTML-Seiten erstellen

Erstelle die restlichen Seiten in **`public/`**. Hier ein Beispiel für **`about.html`**:

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
        <a href="/" class="nav-brand">Mein Portfolio</a>
        <div class="nav-links">
            <a href="/">Home</a>
            <a href="/about.html">Über mich</a>
            <a href="/skills.html">Skills</a>
            <a href="/projects.html">Projekte</a>
            <a href="/contact.html">Kontakt</a>
        </div>
    </nav>

    <main class="container">
        <div class="card">
            <h1>Über mich</h1>
            <div class="info-box">
                <p><strong>Name:</strong> [Dein Name]</p>
                <p><strong>Ausbildung:</strong> Informatiker/in EFZ Applikationsentwicklung</p>
                <p><strong>Lehrjahr:</strong> 1. Lehrjahr</p>
                <p><strong>Lehrbetrieb:</strong> [Dein Lehrbetrieb]</p>
            </div>
            <p>Hier kannst du mehr über dich schreiben...</p>
        </div>
    </main>

    <footer class="footer">
        <p>Portfolio erstellt mit Express.js</p>
    </footer>
</body>
</html>
```

---

## Teil 4: Vollständiger Server (5 Min)

### 4.1 Finale server.js

```javascript
// server.js - Express-Server mit API und statischen Dateien

const express = require('express');
const path = require('path');

const app = express();
const PORT = 3000;

// === Middleware ===

// Statische Dateien aus 'public'-Ordner
app.use(express.static(path.join(__dirname, 'public')));

// JSON-Body parsen (für POST-Requests)
app.use(express.json());

// === JSON-API-Routen ===

app.get('/api/info', (req, res) => {
    res.json({
        name: 'Dein Name',
        role: 'Informatiker/in EFZ Applikationsentwicklung',
        year: 1,
        company: 'Dein Lehrbetrieb'
    });
});

app.get('/api/skills', (req, res) => {
    res.json({
        frontend: [
            { name: 'HTML', level: 80 },
            { name: 'CSS', level: 70 },
            { name: 'JavaScript', level: 60 }
        ],
        backend: [
            { name: 'Node.js', level: 50 },
            { name: 'Express.js', level: 40 }
        ],
        tools: [
            { name: 'Git', level: 60 },
            { name: 'VS Code', level: 90 }
        ]
    });
});

app.get('/api/projects', (req, res) => {
    res.json([
        { id: 1, title: 'Portfolio', status: 'in-progress' },
        { id: 2, title: 'HTTP-Server', status: 'completed' },
        { id: 3, title: 'Todo-App', status: 'planned' }
    ]);
});

app.get('/api/projects/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const projects = [
        { id: 1, title: 'Portfolio', description: 'Portfolio mit Express' },
        { id: 2, title: 'HTTP-Server', description: 'Node.js HTTP-Server' },
        { id: 3, title: 'Todo-App', description: 'Todo-Anwendung' }
    ];
    
    const project = projects.find(p => p.id === id);
    
    if (project) {
        res.json(project);
    } else {
        res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
});

app.get('/api/status', (req, res) => {
    res.json({
        status: 'online',
        timestamp: new Date().toISOString(),
        uptime: Math.floor(process.uptime()) + ' Sekunden'
    });
});

// === Server starten ===
app.listen(PORT, () => {
    console.log(`\nExpress-Server läuft auf http://localhost:${PORT}`);
    console.log('\nStatische Dateien:');
    console.log('  - http://localhost:3000/');
    console.log('  - http://localhost:3000/about.html');
    console.log('  - http://localhost:3000/skills.html');
    console.log('\nAPI-Endpoints:');
    console.log('  - GET /api/info');
    console.log('  - GET /api/skills');
    console.log('  - GET /api/projects');
    console.log('  - GET /api/projects/:id');
    console.log('  - GET /api/status');
});
```

---

## Erfolgskriterien

- [ ] Mindestens 5 API-Endpoints erstellt (/api/info, /api/skills, etc.)
- [ ] `res.json()` wird für alle API-Routen verwendet
- [ ] API-Endpoint mit Parameter erstellt (z.B. /api/projects/:id)
- [ ] 404-Fehler wird als JSON zurückgegeben
- [ ] `public/`-Ordner mit Unterordnern erstellt
- [ ] `express.static()` korrekt eingerichtet
- [ ] Mindestens 2 statische HTML-Seiten erstellt
- [ ] CSS-Datei wird korrekt geladen
- [ ] JavaScript-Datei wird korrekt geladen
- [ ] API-Demo auf der Startseite funktioniert
- [ ] Navigation zwischen Seiten funktioniert

## Tipps

**API im Browser testen:**
JSON wird im Browser oft unformatiert angezeigt. Installiere eine Browser-Extension wie "JSON Viewer" für bessere Lesbarkeit.

**Pfade in HTML:**
Beginne Pfade in HTML mit `/` für absolute Pfade vom Server-Root:
```html
<link rel="stylesheet" href="/css/style.css">
```

**Reihenfolge wichtig:**
`express.static()` sollte vor den API-Routen stehen, damit Express zuerst nach statischen Dateien sucht.

**Debugging:**
```javascript
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
```

## Reflexionsfragen

1. Was ist der Unterschied zwischen `res.send()` und `res.json()`?
2. Warum nutzt man `path.join(__dirname, 'public')` statt einfach `'public'`?
3. Was passiert, wenn ein API-Endpoint und eine statische Datei den gleichen Pfad haben?
4. Teste: Rufe `/api/projects/abc` auf. Was passiert mit `parseInt('abc')`?
5. Wie könntest du Fehler eleganter behandeln (z.B. bei ungültiger ID)?

## Weiterführende Links

- [Express res.json()](https://expressjs.com/en/api.html#res.json) - Dokumentation
- [Express Static Files](https://expressjs.com/en/starter/static-files.html) - Statische Dateien
- [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) - Fetch in JavaScript
- [REST API Design](https://restfulapi.net/) - Best Practices

---

**Geschätzte Zeit:** 45 Minuten  
**Nächster Schritt:** In Auftrag 3 erstellst du eine vollständige Portfolio-Anwendung!
