# Auftrag 3: Externe Middleware und Error-Handling

## Ziel

Du lernst beliebte externe Middleware-Pakete kennen (Morgan, CORS, Helmet) und implementierst professionelles Error-Handling für deine Portfolio-API. Am Ende hast du einen robusten Server, der Fehler sauber behandelt.

## Beschreibung

In der Praxis nutzt du nicht nur eigene Middleware, sondern auch bewährte Pakete aus der Community. Morgan für Logging, CORS für Cross-Origin-Requests und Helmet für Sicherheit sind Standard in professionellen Anwendungen. Zusätzlich lernst du, wie du Fehler zentral behandelst, statt in jeder Route try-catch zu schreiben.

**Geschätzte Zeit:** 45-60 Minuten  
**Voraussetzung:** Aufträge 1 und 2 abgeschlossen

---

## Teil 1: Morgan - Professionelles Logging (10 Min)

### 1.1 Morgan installieren

```bash
npm install morgan
```

### 1.2 Morgan einbinden

Erstelle **`server-extern.js`** oder erweitere deine bestehende `server.js`:

```javascript
const express = require('express');
const morgan = require('morgan');

const app = express();

// === Morgan-Formate ===

// 'dev' - Farbige, kompakte Ausgabe (gut für Entwicklung)
app.use(morgan('dev'));

// Alternativen:
// app.use(morgan('combined'));  // Apache-Format, detailliert
// app.use(morgan('common'));    // Standard Apache
// app.use(morgan('short'));     // Kurz
// app.use(morgan('tiny'));      // Minimal
```

### 1.3 Morgan-Ausgabe verstehen

**Format 'dev':**
```
GET /api/projects 200 5.432 ms - 234
POST /api/projects 201 12.345 ms - 156
GET /api/projects/99 404 1.234 ms - 42
```

**Bedeutung:**
- `GET` = HTTP-Methode
- `/api/projects` = URL
- `200` = Status-Code (farbig: grün=2xx, gelb=3xx, rot=4xx/5xx)
- `5.432 ms` = Response-Zeit
- `234` = Content-Length in Bytes

### 1.4 Morgan in Datei loggen

```javascript
const fs = require('fs');
const path = require('path');

// Log-Verzeichnis erstellen
const logDir = path.join(__dirname, 'logs');
if (!fs.existsSync(logDir)) {
    fs.mkdirSync(logDir);
}

// Log-Stream erstellen
const accessLogStream = fs.createWriteStream(
    path.join(logDir, 'access.log'),
    { flags: 'a' } // 'a' = append
);

// Morgan für Datei-Logging (im 'combined' Format)
app.use(morgan('combined', { stream: accessLogStream }));

// ZUSÄTZLICH: 'dev' für Konsole
app.use(morgan('dev'));
```

---

## Teil 2: CORS - Cross-Origin Requests (10 Min)

### 2.1 Das CORS-Problem verstehen

Wenn dein Frontend (z.B. http://localhost:5173) auf dein Backend (http://localhost:3000) zugreift, blockiert der Browser die Anfrage aus Sicherheitsgründen. CORS (Cross-Origin Resource Sharing) löst dieses Problem.

### 2.2 CORS installieren und einrichten

```bash
npm install cors
```

**Einfache Konfiguration:**

```javascript
const cors = require('cors');

// Alle Origins erlauben (nur für Entwicklung!)
app.use(cors());
```

**Produktions-Konfiguration:**

```javascript
const cors = require('cors');

// Spezifische Konfiguration
const corsOptions = {
    // Erlaubte Origins
    origin: [
        'http://localhost:5173',  // Vite Dev-Server
        'http://localhost:3001',  // Anderer Dienst
        'https://mein-portfolio.ch' // Produktions-Domain
    ],
    
    // Erlaubte HTTP-Methoden
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    
    // Erlaubte Header
    allowedHeaders: ['Content-Type', 'Authorization'],
    
    // Credentials (Cookies) erlauben
    credentials: true,
    
    // Preflight-Cache (Sekunden)
    maxAge: 86400 // 24 Stunden
};

app.use(cors(corsOptions));
```

### 2.3 CORS testen

Erstelle eine einfache HTML-Datei **`test-cors.html`**:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>CORS Test</title>
</head>
<body>
    <h1>CORS Test</h1>
    <button onclick="testAPI()">API aufrufen</button>
    <pre id="result"></pre>
    
    <script>
        async function testAPI() {
            try {
                const response = await fetch('http://localhost:3000/api/projects');
                const data = await response.json();
                document.getElementById('result').textContent = 
                    JSON.stringify(data, null, 2);
            } catch (error) {
                document.getElementById('result').textContent = 
                    'Fehler: ' + error.message;
            }
        }
    </script>
</body>
</html>
```

Öffne die Datei direkt im Browser (file://) und klicke auf den Button. Ohne CORS siehst du einen Fehler, mit CORS funktioniert es.

---

## Teil 3: Helmet - Sicherheits-Header (10 Min)

### 3.1 Helmet installieren

```bash
npm install helmet
```

### 3.2 Helmet einbinden

```javascript
const helmet = require('helmet');

// Basis-Konfiguration (empfohlen)
app.use(helmet());
```

### 3.3 Was macht Helmet?

Helmet setzt verschiedene HTTP-Header für mehr Sicherheit:

```javascript
// Einzelne Helmet-Middleware
app.use(helmet.contentSecurityPolicy());    // Schützt vor XSS
app.use(helmet.crossOriginEmbedderPolicy());
app.use(helmet.crossOriginOpenerPolicy());
app.use(helmet.crossOriginResourcePolicy());
app.use(helmet.dnsPrefetchControl());       // DNS-Prefetch kontrollieren
app.use(helmet.frameguard());               // Clickjacking verhindern
app.use(helmet.hidePoweredBy());            // X-Powered-By entfernen
app.use(helmet.hsts());                     // HTTPS erzwingen
app.use(helmet.ieNoOpen());                 // IE Download-Schutz
app.use(helmet.noSniff());                  // MIME-Sniffing verhindern
app.use(helmet.originAgentCluster());
app.use(helmet.permittedCrossDomainPolicies());
app.use(helmet.referrerPolicy());           // Referrer-Policy setzen
app.use(helmet.xssFilter());                // XSS-Filter
```

### 3.4 Header prüfen

Starte den Server und prüfe die Header:

```bash
curl -I http://localhost:3000/
```

**Ausgabe mit Helmet:**
```
HTTP/1.1 200 OK
Content-Security-Policy: default-src 'self'
Cross-Origin-Embedder-Policy: require-corp
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Resource-Policy: same-origin
X-DNS-Prefetch-Control: off
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
...
```

---

## Teil 4: Error-Handling implementieren (15 Min)

### 4.1 Error-Handler Middleware

Erstelle **`middleware/errorHandler.js`**:

```javascript
// middleware/errorHandler.js - Zentrales Error-Handling

// Eigene Error-Klasse für API-Fehler
class ApiError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.status = statusCode >= 400 && statusCode < 500 ? 'fail' : 'error';
    }
}

// 404-Handler für nicht gefundene Routen
function notFoundHandler(req, res, next) {
    const error = new ApiError(`Route ${req.originalUrl} nicht gefunden`, 404);
    next(error);
}

// Globaler Error-Handler (MUSS 4 Parameter haben!)
function errorHandler(err, req, res, next) {
    // Standard-Werte setzen
    const statusCode = err.statusCode || 500;
    const status = err.status || 'error';
    
    // Entwicklungs-Modus: Detaillierte Fehler
    if (process.env.NODE_ENV !== 'production') {
        console.error('=== ERROR ===');
        console.error(err.stack);
        console.error('=============');
        
        return res.status(statusCode).json({
            status,
            message: err.message,
            stack: err.stack,
            error: err
        });
    }
    
    // Produktions-Modus: Bereinigter Fehler
    return res.status(statusCode).json({
        status,
        message: statusCode === 500 
            ? 'Ein interner Serverfehler ist aufgetreten' 
            : err.message
    });
}

module.exports = {
    ApiError,
    notFoundHandler,
    errorHandler
};
```

### 4.2 Error-Handler einbinden

In **`server.js`**:

```javascript
const { ApiError, notFoundHandler, errorHandler } = require('./middleware/errorHandler');

// === Routen ===
app.get('/api/projects', (req, res) => {
    res.json(projects);
});

app.get('/api/projects/:id', (req, res, next) => {
    const id = parseInt(req.params.id);
    
    // Ungültige ID
    if (isNaN(id)) {
        return next(new ApiError('ID muss eine Zahl sein', 400));
    }
    
    const project = projects.find(p => p.id === id);
    
    // Nicht gefunden
    if (!project) {
        return next(new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404));
    }
    
    res.json(project);
});

// Test-Route für Fehler
app.get('/api/error-test', (req, res, next) => {
    next(new ApiError('Das ist ein Test-Fehler', 400));
});

// Route für unerwarteten Fehler
app.get('/api/crash', (req, res) => {
    throw new Error('Unerwarteter Serverfehler!');
});

// === Error-Handler (MÜSSEN am Ende stehen!) ===
app.use(notFoundHandler);  // 404 für unbekannte Routen
app.use(errorHandler);     // Alle anderen Fehler
```

### 4.3 Async Error-Handling

Für asynchrone Operationen:

```javascript
// Hilfsfunktion für async-Routen
const asyncHandler = (fn) => (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
};

// Verwendung:
app.get('/api/data', asyncHandler(async (req, res) => {
    const data = await fetchDataFromSomewhere();
    res.json(data);
}));
```

---

## Teil 5: Vollständiger Server (5 Min)

### 5.1 Finale Projektstruktur

```
portfolio-api/
├── middleware/
│   ├── logger.js
│   ├── timer.js
│   ├── validators.js
│   └── errorHandler.js
├── logs/
│   └── access.log
├── server.js
├── test.http
└── package.json
```

### 5.2 Finale `server.js`

```javascript
// server.js - Professionelle Portfolio-API

const express = require('express');
const morgan = require('morgan');
const cors = require('cors');
const helmet = require('helmet');
const path = require('path');
const fs = require('fs');

const { validateProject } = require('./middleware/validators');
const { ApiError, notFoundHandler, errorHandler } = require('./middleware/errorHandler');

const app = express();
const PORT = process.env.PORT || 3000;

// === Logs-Verzeichnis ===
const logDir = path.join(__dirname, 'logs');
if (!fs.existsSync(logDir)) {
    fs.mkdirSync(logDir);
}

// === Middleware (Reihenfolge wichtig!) ===

// 1. Sicherheit
app.use(helmet());

// 2. CORS
app.use(cors({
    origin: ['http://localhost:5173', 'http://localhost:3001'],
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    credentials: true
}));

// 3. Logging
const accessLogStream = fs.createWriteStream(
    path.join(logDir, 'access.log'),
    { flags: 'a' }
);
app.use(morgan('combined', { stream: accessLogStream }));
app.use(morgan('dev'));

// 4. Body-Parser
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// 5. Statische Dateien
app.use(express.static(path.join(__dirname, 'public')));

// === Daten ===
let projects = [
    { id: 1, title: 'Portfolio-Website', status: 'in-progress' },
    { id: 2, title: 'Express-API', status: 'completed' }
];
let nextId = 3;

// === API-Routen ===

// Info-Route
app.get('/api', (req, res) => {
    res.json({
        name: 'Portfolio-API',
        version: '1.0.0',
        endpoints: [
            'GET /api/projects',
            'GET /api/projects/:id',
            'POST /api/projects',
            'PUT /api/projects/:id',
            'DELETE /api/projects/:id'
        ]
    });
});

// GET alle Projekte
app.get('/api/projects', (req, res) => {
    res.json({ count: projects.length, data: projects });
});

// GET einzelnes Projekt
app.get('/api/projects/:id', (req, res, next) => {
    const id = parseInt(req.params.id);
    
    if (isNaN(id)) {
        return next(new ApiError('ID muss eine Zahl sein', 400));
    }
    
    const project = projects.find(p => p.id === id);
    
    if (!project) {
        return next(new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404));
    }
    
    res.json(project);
});

// POST neues Projekt
app.post('/api/projects', validateProject, (req, res) => {
    const newProject = { id: nextId++, ...req.body };
    projects.push(newProject);
    res.status(201).json(newProject);
});

// PUT Projekt aktualisieren
app.put('/api/projects/:id', validateProject, (req, res, next) => {
    const id = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === id);
    
    if (index === -1) {
        return next(new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404));
    }
    
    projects[index] = { id, ...req.body };
    res.json(projects[index]);
});

// DELETE Projekt löschen
app.delete('/api/projects/:id', (req, res, next) => {
    const id = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === id);
    
    if (index === -1) {
        return next(new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404));
    }
    
    const deleted = projects.splice(index, 1)[0];
    res.json({ message: 'Projekt gelöscht', data: deleted });
});

// === Error-Handler (am Ende!) ===
app.use(notFoundHandler);
app.use(errorHandler);

// === Server starten ===
app.listen(PORT, () => {
    console.log('\n╔═══════════════════════════════════════╗');
    console.log('║     Portfolio-API gestartet           ║');
    console.log('╠═══════════════════════════════════════╣');
    console.log(`║  Server: http://localhost:${PORT}        ║`);
    console.log('║  Logs:   ./logs/access.log            ║');
    console.log('╚═══════════════════════════════════════╝\n');
});
```

---

## Erfolgskriterien

- [ ] Morgan installiert und konfiguriert
- [ ] Logs werden in Datei geschrieben
- [ ] CORS korrekt eingerichtet
- [ ] Helmet für Sicherheits-Header aktiv
- [ ] ApiError-Klasse implementiert
- [ ] 404-Handler für unbekannte Routen
- [ ] Globaler Error-Handler funktioniert
- [ ] Alle Middleware in richtiger Reihenfolge
- [ ] Server startet ohne Fehler

## Tipps

**Umgebungsvariablen nutzen:**
```javascript
const PORT = process.env.PORT || 3000;

// Starten mit:
// PORT=4000 node server.js
```

**NODE_ENV setzen:**
```bash
# Entwicklung
NODE_ENV=development node server.js

# Produktion
NODE_ENV=production node server.js
```

**Error-Handler erkennen:**
Express erkennt Error-Handler an den 4 Parametern (err, req, res, next). Wenn du nur 3 Parameter hast, wird es als normale Middleware behandelt.

## Reflexionsfragen

1. Warum sollte der Error-Handler ganz am Ende stehen?
2. Was ist der Unterschied zwischen `app.use(cors())` und einer spezifischen CORS-Konfiguration?
3. Welche Sicherheits-Header setzt Helmet automatisch?
4. Warum ist es wichtig, in Produktion keine Stack-Traces auszugeben?
5. Wie erkennst du einen Error-Handler an seiner Signatur?

## Weiterführende Links

- [Morgan Dokumentation](https://www.npmjs.com/package/morgan) - HTTP Request Logger
- [CORS](https://www.npmjs.com/package/cors) - Cross-Origin Resource Sharing
- [Helmet.js](https://helmetjs.github.io/) - Sicherheits-Middleware
- [Express Error Handling](https://expressjs.com/en/guide/error-handling.html) - Offizielle Dokumentation
- [OWASP Security Headers](https://owasp.org/www-project-secure-headers/)

---

**Geschätzte Zeit:** 45-60 Minuten  
**Nächster Schritt:** Der optionale Auftrag zeigt dir Router-Module und fortgeschrittene Muster!
