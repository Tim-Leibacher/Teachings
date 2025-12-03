# Auftrag 3: Portfolio-Server von http-Modul auf Express umstellen

## Ziel

Du stellst deinen bestehenden HTTP-Server (aus dem vorherigen Modul) auf Express um. Dabei siehst du den direkten Vergleich zwischen beiden Ansätzen und verstehst, warum Express die Entwicklung vereinfacht.

## Beschreibung

In den vorherigen Aufträgen hast du einen HTTP-Server mit dem eingebauten http-Modul erstellt. Jetzt nimmst du diesen Code und schreibst ihn in Express um. Das Ergebnis: Weniger Code, bessere Lesbarkeit, mehr Features. Dieser Auftrag zeigt dir konkret, welche Vorteile Express bietet.

**Geschätzte Zeit:** 30 Minuten

---

## Teil 1: Alten Code analysieren (5 Min)

### 1.1 Dein bisheriger HTTP-Server

So sah dein Server mit dem http-Modul aus (vereinfachte Version):

```javascript
// server-alt.js - HTTP-Server ohne Express
const http = require('http');
const fs = require('fs');
const path = require('path');

const PORT = 3000;

const server = http.createServer((req, res) => {
    
    // Routing mit if/else
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
        res.setHeader('Content-Type', 'application/json; charset=utf-8');
        const skills = { frontend: ['HTML', 'CSS'], backend: ['Node.js'] };
        res.end(JSON.stringify(skills, null, 2));
        
    } else if (req.url.startsWith('/public/')) {
        // Statische Dateien manuell laden
        const filePath = path.join(__dirname, req.url);
        const extname = path.extname(filePath);
        
        const contentTypes = {
            '.html': 'text/html',
            '.css': 'text/css',
            '.js': 'application/javascript'
        };
        
        fs.readFile(filePath, (err, content) => {
            if (err) {
                res.statusCode = 404;
                res.end('Datei nicht gefunden');
            } else {
                res.statusCode = 200;
                res.setHeader('Content-Type', contentTypes[extname] || 'text/plain');
                res.end(content);
            }
        });
        
    } else {
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/html; charset=utf-8');
        res.end('<h1>404 - Seite nicht gefunden</h1>');
    }
});

server.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

### 1.2 Probleme identifizieren

Markiere im Code die problematischen Stellen:

| Problem | Code-Stelle |
|---------|-------------|
| Manuelles Routing | `if (req.url === '/') { ... }` |
| Content-Type setzen | `res.setHeader('Content-Type', ...)` |
| JSON serialisieren | `JSON.stringify(skills, null, 2)` |
| Statische Dateien | Ganzer fs.readFile-Block |
| Status-Code setzen | `res.statusCode = 200` |

---

## Teil 2: Umstellung auf Express (15 Min)

### 2.1 Neue Datei erstellen

Erstelle **`server-express.js`** im gleichen Ordner:

```javascript
// server-express.js - Der gleiche Server mit Express

const express = require('express');
const path = require('path');

const app = express();
const PORT = 3000;

// Statische Dateien (ersetzt den gesamten fs.readFile-Block!)
app.use(express.static(path.join(__dirname, 'public')));

// Startseite
app.get('/', (req, res) => {
    res.send('<h1>Startseite</h1>');
});

// Über mich
app.get('/about', (req, res) => {
    res.send('<h1>Über mich</h1>');
});

// API: Skills (ersetzt JSON.stringify und Content-Type!)
app.get('/api/skills', (req, res) => {
    const skills = { frontend: ['HTML', 'CSS'], backend: ['Node.js'] };
    res.json(skills);
});

// 404-Handler (kommt am Ende)
app.use((req, res) => {
    res.status(404).send('<h1>404 - Seite nicht gefunden</h1>');
});

// Server starten
app.listen(PORT, () => {
    console.log(`Express-Server läuft auf http://localhost:${PORT}`);
});
```

### 2.2 Vergleich: Zeile für Zeile

| Aufgabe | http-Modul | Express |
|---------|------------|---------|
| **Routing** | `if (req.url === '/')` | `app.get('/')` |
| **HTML senden** | `res.setHeader(...); res.end(html)` | `res.send(html)` |
| **JSON senden** | `res.setHeader('Content-Type', 'application/json'); res.end(JSON.stringify(data))` | `res.json(data)` |
| **Status setzen** | `res.statusCode = 404` | `res.status(404)` |
| **Statische Dateien** | 20+ Zeilen mit fs | 1 Zeile: `app.use(express.static())` |

### 2.3 Code-Ersparnis berechnen

- **http-Modul:** ca. 50 Zeilen
- **Express:** ca. 25 Zeilen
- **Ersparnis:** 50% weniger Code

---

## Teil 3: Vollständiges Portfolio umstellen (10 Min)

### 3.1 Dein komplettes Portfolio mit Express

Erstelle eine vollständige Version mit allen Routen aus dem vorherigen Modul:

```javascript
// server.js - Vollständiges Portfolio mit Express

const express = require('express');
const path = require('path');

const app = express();
const PORT = 3000;

// === Middleware ===
app.use(express.static(path.join(__dirname, 'public')));
app.use(express.json());

// === Daten (später aus Datenbank) ===
const portfolioData = {
    info: {
        name: 'Dein Name',
        role: 'Informatiker/in EFZ Applikationsentwicklung',
        year: 1,
        company: 'Dein Lehrbetrieb',
        email: 'deine.email@example.com'
    },
    skills: {
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
    },
    projects: [
        {
            id: 1,
            title: 'Portfolio-Website',
            description: 'Persönliche Portfolio-Seite',
            technologies: ['HTML', 'CSS', 'JavaScript', 'Node.js', 'Express'],
            status: 'in-progress',
            startDate: '2025-01'
        },
        {
            id: 2,
            title: 'HTTP-Server',
            description: 'Server mit dem Node.js http-Modul',
            technologies: ['Node.js'],
            status: 'completed',
            startDate: '2024-12'
        },
        {
            id: 3,
            title: 'Express-Server',
            description: 'Umstellung auf Express.js',
            technologies: ['Node.js', 'Express'],
            status: 'completed',
            startDate: '2025-01'
        }
    ]
};

// === API-Routen ===

// Info
app.get('/api/info', (req, res) => {
    res.json(portfolioData.info);
});

// Skills
app.get('/api/skills', (req, res) => {
    res.json(portfolioData.skills);
});

// Alle Projekte
app.get('/api/projects', (req, res) => {
    res.json(portfolioData.projects);
});

// Einzelnes Projekt
app.get('/api/projects/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const project = portfolioData.projects.find(p => p.id === id);
    
    if (project) {
        res.json(project);
    } else {
        res.status(404).json({ 
            error: 'Projekt nicht gefunden',
            message: `Kein Projekt mit ID ${id} vorhanden`
        });
    }
});

// Server-Status
app.get('/api/status', (req, res) => {
    res.json({
        status: 'online',
        server: 'Express.js',
        timestamp: new Date().toISOString(),
        uptime: `${Math.floor(process.uptime())} Sekunden`,
        endpoints: [
            'GET /api/info',
            'GET /api/skills',
            'GET /api/projects',
            'GET /api/projects/:id',
            'GET /api/status'
        ]
    });
});

// === 404-Handler (muss am Ende stehen) ===
app.use((req, res) => {
    // Prüfen, ob API-Anfrage oder HTML
    if (req.path.startsWith('/api/')) {
        res.status(404).json({
            error: 'Endpoint nicht gefunden',
            path: req.path
        });
    } else {
        res.status(404).send(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>404 - Nicht gefunden</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        text-align: center;
                        padding: 50px;
                        background: #f5f5f5;
                    }
                    h1 { color: #E87722; }
                    a { color: #376B8C; }
                </style>
            </head>
            <body>
                <h1>404 - Seite nicht gefunden</h1>
                <p>Die angeforderte Seite existiert nicht.</p>
                <p><a href="/">Zurück zur Startseite</a></p>
            </body>
            </html>
        `);
    }
});

// === Server starten ===
app.listen(PORT, () => {
    console.log('\n========================================');
    console.log('   Portfolio Express-Server gestartet');
    console.log('========================================');
    console.log(`\nServer: http://localhost:${PORT}`);
    console.log('\nVerfügbare Routen:');
    console.log('  Webseite: http://localhost:3000/');
    console.log('\nAPI-Endpoints:');
    console.log('  GET /api/info');
    console.log('  GET /api/skills');
    console.log('  GET /api/projects');
    console.log('  GET /api/projects/:id');
    console.log('  GET /api/status');
    console.log('\n========================================\n');
});
```

### 3.2 Beide Server vergleichen

Starte beide Server nacheinander und vergleiche:

```bash
# Alt (http-Modul)
node server-alt.js
# Test: http://localhost:3000

# Neu (Express)
node server-express.js
# Test: http://localhost:3000
```

Beide sollten identisch funktionieren - aber der Express-Code ist deutlich kürzer und lesbarer.

---

## Erfolgskriterien

- [ ] Alten HTTP-Server-Code analysiert
- [ ] Problematische Stellen identifiziert
- [ ] Express-Version erstellt (`server-express.js`)
- [ ] Alle Routen funktionieren identisch
- [ ] API-Endpoints liefern JSON
- [ ] Statische Dateien werden ausgeliefert
- [ ] 404-Handler implementiert (für HTML und API)
- [ ] Code-Ersparnis dokumentiert
- [ ] Beide Versionen getestet und verglichen

## Tipps

**Schrittweise umstellen:**
Stelle Route für Route um und teste nach jeder Änderung.

**Reihenfolge beachten:**
1. `express.static()` (statische Dateien zuerst)
2. API-Routen
3. 404-Handler (muss am Ende stehen!)

**Debugging:**
```javascript
// Alle Requests loggen
app.use((req, res, next) => {
    console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
    next();
});
```

**Tipp für Umstellung:**
Behalte den alten Code als Referenz. So kannst du immer vergleichen, ob das Verhalten gleich ist.

## Reflexionsfragen

1. Welche Vorteile hat Express gegenüber dem http-Modul?
2. Warum steht der 404-Handler am Ende?
3. Was macht `next()` in einer Middleware?
4. Wie viel Prozent Code hast du eingespart?
5. In welchen Situationen könnte das http-Modul trotzdem sinnvoll sein?

## Weiterführende Links

- [Express vs. http-Modul](https://expressjs.com/en/guide/migrating-4.html) - Migration Guide
- [Express Middleware](https://expressjs.com/en/guide/using-middleware.html) - Middleware-Konzept
- [Express Best Practices](https://expressjs.com/en/advanced/best-practice-performance.html) - Performance

---

**Geschätzte Zeit:** 30 Minuten  
**Nächster Schritt:** Optionaler Vertiefungsauftrag zu Middleware und Error-Handling
