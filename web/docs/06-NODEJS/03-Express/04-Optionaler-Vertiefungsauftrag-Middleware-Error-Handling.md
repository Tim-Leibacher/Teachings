# Optionaler Auftrag: Middleware verstehen und Error-Handling implementieren

## Ziel

Du verstehst das Middleware-Konzept in Express und implementierst professionelles Error-Handling, Request-Logging und eigene Middleware-Funktionen für dein Portfolio.

## Beschreibung

Middleware ist das Herzstück von Express. Jede Funktion, die Zugriff auf das Request-Objekt (req), das Response-Objekt (res) und die next()-Funktion hat, ist eine Middleware. In diesem Vertiefungsauftrag lernst du, wie Middleware funktioniert, erstellst eigene Middleware und implementierst professionelles Error-Handling.

**Geschätzte Zeit:** 60-90 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzung:** Aufträge 1-3 abgeschlossen

---

## Teil 1: Middleware verstehen (20 Min)

### 1.1 Was ist Middleware?

Middleware-Funktionen werden der Reihe nach ausgeführt, bevor die eigentliche Route erreicht wird:

```
Request → Middleware 1 → Middleware 2 → Middleware 3 → Route → Response
```

Jede Middleware kann:
- Das Request-Objekt verändern
- Das Response-Objekt verändern
- Den Request-Response-Zyklus beenden
- Die nächste Middleware aufrufen (`next()`)

### 1.2 Einfache Middleware erstellen

Erstelle **`server-middleware.js`**:

```javascript
// server-middleware.js - Middleware verstehen

const express = require('express');
const app = express();
const PORT = 3000;

// === Eigene Middleware-Funktionen ===

// Middleware 1: Request-Logger
const requestLogger = (req, res, next) => {
    const timestamp = new Date().toISOString();
    console.log(`[${timestamp}] ${req.method} ${req.url}`);
    next(); // WICHTIG: Nächste Middleware aufrufen
};

// Middleware 2: Request-Zeit messen
const requestTimer = (req, res, next) => {
    req.startTime = Date.now();
    
    // Response-Ende abfangen
    res.on('finish', () => {
        const duration = Date.now() - req.startTime;
        console.log(`  → Antwort in ${duration}ms`);
    });
    
    next();
};

// Middleware 3: Custom Header hinzufügen
const addCustomHeaders = (req, res, next) => {
    res.setHeader('X-Powered-By', 'Express Portfolio Server');
    res.setHeader('X-Request-Id', Date.now().toString(36));
    next();
};

// === Middleware registrieren (Reihenfolge wichtig!) ===
app.use(requestLogger);
app.use(requestTimer);
app.use(addCustomHeaders);

// === Routen ===
app.get('/', (req, res) => {
    res.send('<h1>Middleware-Demo</h1><p>Schau in die Konsole!</p>');
});

app.get('/slow', (req, res) => {
    // Simuliere langsame Verarbeitung
    setTimeout(() => {
        res.send('<h1>Langsame Route</h1><p>Diese Route dauerte 2 Sekunden.</p>');
    }, 2000);
});

app.get('/api/test', (req, res) => {
    res.json({ 
        message: 'API funktioniert',
        requestId: res.getHeader('X-Request-Id')
    });
});

// Server starten
app.listen(PORT, () => {
    console.log(`Middleware-Demo auf http://localhost:${PORT}`);
    console.log('Teste verschiedene Routen und beobachte die Konsole!\n');
});
```

### 1.3 Testen

```bash
node server-middleware.js
```

Rufe verschiedene URLs auf und beobachte die Konsolen-Ausgabe:
- `http://localhost:3000/`
- `http://localhost:3000/slow`
- `http://localhost:3000/api/test`

---

## Teil 2: Professionelles Logging (20 Min)

### 2.1 Strukturierter Logger

Erstelle **`middleware/logger.js`**:

```javascript
// middleware/logger.js - Professionelles Logging

const fs = require('fs');
const path = require('path');

// Log-Ordner erstellen
const LOG_DIR = path.join(__dirname, '..', 'logs');
if (!fs.existsSync(LOG_DIR)) {
    fs.mkdirSync(LOG_DIR, { recursive: true });
}

// Farben für Terminal
const colors = {
    reset: '\x1b[0m',
    green: '\x1b[32m',
    yellow: '\x1b[33m',
    red: '\x1b[31m',
    cyan: '\x1b[36m',
    gray: '\x1b[90m'
};

// Status-Code-Farbe bestimmen
function getStatusColor(status) {
    if (status >= 500) return colors.red;
    if (status >= 400) return colors.yellow;
    if (status >= 300) return colors.cyan;
    return colors.green;
}

// Datum formatieren
function getDateString() {
    const now = new Date();
    return now.toISOString().split('T')[0];
}

// Log-Entry erstellen
function formatLogEntry(data) {
    return JSON.stringify({
        timestamp: new Date().toISOString(),
        ...data
    }) + '\n';
}

// Logger-Middleware
function logger(options = {}) {
    const { 
        logToFile = true, 
        logToConsole = true,
        logBody = false 
    } = options;

    return (req, res, next) => {
        const startTime = Date.now();
        
        // Original end-Funktion speichern
        const originalEnd = res.end;
        
        // end-Funktion überschreiben
        res.end = function(chunk, encoding) {
            // Originale Funktion aufrufen
            originalEnd.call(this, chunk, encoding);
            
            const duration = Date.now() - startTime;
            const statusColor = getStatusColor(res.statusCode);
            
            // Log-Daten
            const logData = {
                method: req.method,
                url: req.url,
                status: res.statusCode,
                duration: `${duration}ms`,
                ip: req.ip || req.connection.remoteAddress,
                userAgent: req.get('User-Agent')
            };
            
            if (logBody && req.body && Object.keys(req.body).length > 0) {
                logData.body = req.body;
            }
            
            // Konsolen-Ausgabe
            if (logToConsole) {
                const timestamp = new Date().toISOString();
                console.log(
                    `${colors.gray}[${timestamp}]${colors.reset} ` +
                    `${statusColor}${res.statusCode}${colors.reset} ` +
                    `${req.method} ${req.url} ` +
                    `${colors.gray}${duration}ms${colors.reset}`
                );
            }
            
            // Datei-Logging
            if (logToFile) {
                const logFile = path.join(LOG_DIR, `access-${getDateString()}.log`);
                fs.appendFileSync(logFile, formatLogEntry(logData));
            }
        };
        
        next();
    };
}

module.exports = logger;
```

### 2.2 Logger in Server einbinden

Aktualisiere **`server.js`**:

```javascript
const express = require('express');
const path = require('path');
const logger = require('./middleware/logger');

const app = express();
const PORT = 3000;

// Logger-Middleware (früh einbinden!)
app.use(logger({
    logToFile: true,
    logToConsole: true
}));

// Weitere Middleware und Routen...
```

---

## Teil 3: Error-Handling (25 Min)

### 3.1 Error-Handler Middleware

Erstelle **`middleware/errorHandler.js`**:

```javascript
// middleware/errorHandler.js - Zentrales Error-Handling

// Eigene Error-Klasse
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
        this.isOperational = true;
        
        Error.captureStackTrace(this, this.constructor);
    }
}

// 404-Handler (für nicht gefundene Routen)
function notFoundHandler(req, res, next) {
    const error = new AppError(`Route ${req.originalUrl} nicht gefunden`, 404);
    next(error);
}

// Globaler Error-Handler
function errorHandler(err, req, res, next) {
    // Default-Werte setzen
    err.statusCode = err.statusCode || 500;
    err.status = err.status || 'error';
    
    // Entwicklungs-Modus: Detaillierte Fehler
    if (process.env.NODE_ENV === 'development') {
        return sendDevError(err, req, res);
    }
    
    // Produktions-Modus: Bereinigter Fehler
    return sendProdError(err, req, res);
}

// Entwicklungs-Fehler (mit Stack-Trace)
function sendDevError(err, req, res) {
    // API-Fehler als JSON
    if (req.path.startsWith('/api/')) {
        return res.status(err.statusCode).json({
            status: err.status,
            error: err,
            message: err.message,
            stack: err.stack
        });
    }
    
    // HTML-Fehler
    return res.status(err.statusCode).send(`
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <title>Fehler ${err.statusCode}</title>
            <style>
                body {
                    font-family: 'Consolas', monospace;
                    background: #1a1a2e;
                    color: #eee;
                    padding: 40px;
                    line-height: 1.6;
                }
                h1 { color: #e94560; }
                .error-box {
                    background: #16213e;
                    padding: 20px;
                    border-radius: 8px;
                    margin: 20px 0;
                    border-left: 4px solid #e94560;
                }
                pre {
                    background: #0f0f23;
                    padding: 15px;
                    overflow-x: auto;
                    border-radius: 4px;
                }
                .back-link {
                    color: #00d9ff;
                    text-decoration: none;
                }
            </style>
        </head>
        <body>
            <h1>Fehler ${err.statusCode}: ${err.status}</h1>
            <div class="error-box">
                <p><strong>Message:</strong> ${err.message}</p>
            </div>
            <h2>Stack Trace:</h2>
            <pre>${err.stack}</pre>
            <p><a href="/" class="back-link">Zurück zur Startseite</a></p>
        </body>
        </html>
    `);
}

// Produktions-Fehler (ohne sensible Daten)
function sendProdError(err, req, res) {
    // Bekannter, operationaler Fehler
    if (err.isOperational) {
        if (req.path.startsWith('/api/')) {
            return res.status(err.statusCode).json({
                status: err.status,
                message: err.message
            });
        }
        
        return res.status(err.statusCode).send(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Fehler ${err.statusCode}</title>
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
                <h1>Fehler ${err.statusCode}</h1>
                <p>${err.message}</p>
                <p><a href="/">Zurück zur Startseite</a></p>
            </body>
            </html>
        `);
    }
    
    // Unbekannter Fehler - nicht an Client senden
    console.error('UNBEKANNTER FEHLER:', err);
    
    if (req.path.startsWith('/api/')) {
        return res.status(500).json({
            status: 'error',
            message: 'Ein unerwarteter Fehler ist aufgetreten'
        });
    }
    
    return res.status(500).send(`
        <h1>500 - Server-Fehler</h1>
        <p>Etwas ist schiefgelaufen. Bitte versuche es später erneut.</p>
    `);
}

module.exports = {
    AppError,
    notFoundHandler,
    errorHandler
};
```

### 3.2 Vollständiger Server mit Error-Handling

Aktualisiere **`server.js`**:

```javascript
// server.js - Express mit Middleware und Error-Handling

const express = require('express');
const path = require('path');
const logger = require('./middleware/logger');
const { AppError, notFoundHandler, errorHandler } = require('./middleware/errorHandler');

const app = express();
const PORT = process.env.PORT || 3000;

// === Middleware ===
app.use(logger({ logToFile: true, logToConsole: true }));
app.use(express.json());
app.use(express.static(path.join(__dirname, 'public')));

// === Daten ===
const projects = [
    { id: 1, title: 'Portfolio', status: 'in-progress' },
    { id: 2, title: 'HTTP-Server', status: 'completed' },
    { id: 3, title: 'Express-Server', status: 'completed' }
];

// === API-Routen ===

app.get('/api/projects', (req, res) => {
    res.json(projects);
});

app.get('/api/projects/:id', (req, res, next) => {
    const id = parseInt(req.params.id);
    
    if (isNaN(id)) {
        return next(new AppError('ID muss eine Zahl sein', 400));
    }
    
    const project = projects.find(p => p.id === id);
    
    if (!project) {
        return next(new AppError(`Projekt mit ID ${id} nicht gefunden`, 404));
    }
    
    res.json(project);
});

// Test-Route für Fehler
app.get('/api/error-test', (req, res, next) => {
    next(new AppError('Das ist ein Test-Fehler', 400));
});

// Test-Route für unerwarteten Fehler
app.get('/api/crash', (req, res) => {
    throw new Error('Simulierter Server-Crash');
});

// === Error-Handler (MÜSSEN am Ende stehen) ===
app.use(notFoundHandler);
app.use(errorHandler);

// === Server starten ===
app.listen(PORT, () => {
    console.log(`\nServer läuft auf http://localhost:${PORT}`);
    console.log('NODE_ENV:', process.env.NODE_ENV || 'development');
    console.log('\nTest-Routes:');
    console.log('  - GET /api/projects');
    console.log('  - GET /api/projects/1');
    console.log('  - GET /api/projects/abc (400 Fehler)');
    console.log('  - GET /api/projects/99 (404 Fehler)');
    console.log('  - GET /api/error-test (Test-Fehler)');
    console.log('  - GET /nicht-vorhanden (404 HTML)\n');
});
```

---

## Teil 4: Weitere nützliche Middleware (15 Min)

### 4.1 Rate-Limiter (Anfragen begrenzen)

Erstelle **`middleware/rateLimiter.js`**:

```javascript
// middleware/rateLimiter.js - Einfacher Rate-Limiter

const requests = new Map();

function rateLimiter(options = {}) {
    const {
        windowMs = 60000,       // Zeitfenster: 1 Minute
        maxRequests = 100,      // Max Anfragen pro Zeitfenster
        message = 'Zu viele Anfragen. Bitte warte einen Moment.'
    } = options;

    return (req, res, next) => {
        const ip = req.ip || req.connection.remoteAddress;
        const now = Date.now();
        
        // Alte Einträge aufräumen
        if (!requests.has(ip)) {
            requests.set(ip, []);
        }
        
        const userRequests = requests.get(ip).filter(
            time => now - time < windowMs
        );
        
        if (userRequests.length >= maxRequests) {
            return res.status(429).json({
                error: 'Too Many Requests',
                message: message,
                retryAfter: Math.ceil((windowMs - (now - userRequests[0])) / 1000)
            });
        }
        
        userRequests.push(now);
        requests.set(ip, userRequests);
        
        next();
    };
}

module.exports = rateLimiter;
```

### 4.2 CORS-Middleware

```javascript
// middleware/cors.js - CORS-Header setzen

function cors(options = {}) {
    const {
        origin = '*',
        methods = 'GET,HEAD,PUT,PATCH,POST,DELETE',
        allowedHeaders = 'Content-Type,Authorization'
    } = options;

    return (req, res, next) => {
        res.setHeader('Access-Control-Allow-Origin', origin);
        res.setHeader('Access-Control-Allow-Methods', methods);
        res.setHeader('Access-Control-Allow-Headers', allowedHeaders);
        
        // Preflight-Request
        if (req.method === 'OPTIONS') {
            return res.status(204).end();
        }
        
        next();
    };
}

module.exports = cors;
```

---

## Erfolgskriterien

- [ ] Middleware-Konzept verstanden (Request → Middleware → Response)
- [ ] Eigene Logger-Middleware erstellt
- [ ] Log-Dateien werden in `/logs` geschrieben
- [ ] AppError-Klasse implementiert
- [ ] 404-Handler für nicht gefundene Routen
- [ ] Globaler Error-Handler mit Dev/Prod-Unterscheidung
- [ ] Unterschiedliche Fehler-Formate für API und HTML
- [ ] `next(error)` korrekt verwendet
- [ ] Rate-Limiter verstanden (optional implementiert)
- [ ] Alle Middleware in korrekter Reihenfolge registriert

## Tipps

**Middleware-Reihenfolge:**
1. Logging (ganz früh)
2. Body-Parser (express.json())
3. CORS
4. Rate-Limiter
5. Statische Dateien
6. Routen
7. 404-Handler
8. Error-Handler (ganz am Ende!)

**Debugging:**
```javascript
// Debug-Middleware
app.use((req, res, next) => {
    console.log('--- DEBUG ---');
    console.log('Headers:', req.headers);
    console.log('Body:', req.body);
    console.log('Query:', req.query);
    console.log('Params:', req.params);
    console.log('-------------');
    next();
});
```

**Async Error-Handling:**
```javascript
// Wrapper für async-Funktionen
const catchAsync = fn => {
    return (req, res, next) => {
        fn(req, res, next).catch(next);
    };
};

// Verwendung:
app.get('/api/data', catchAsync(async (req, res) => {
    const data = await fetchData();
    res.json(data);
}));
```

## Reflexionsfragen

1. Warum ist die Reihenfolge der Middleware wichtig?
2. Was passiert, wenn du `next()` vergisst aufzurufen?
3. Warum sollte der Error-Handler vier Parameter haben (err, req, res, next)?
4. Wie unterscheidet sich Error-Handling in Entwicklung und Produktion?
5. Recherchiere: Was macht das npm-Paket `express-rate-limit`?

## Weiterführende Links

- [Express Middleware Guide](https://expressjs.com/en/guide/using-middleware.html)
- [Express Error Handling](https://expressjs.com/en/guide/error-handling.html)
- [Morgan Logger](https://www.npmjs.com/package/morgan) - Beliebter Express-Logger
- [Helmet.js](https://helmetjs.github.io/) - Sicherheits-Middleware
- [express-rate-limit](https://www.npmjs.com/package/express-rate-limit)

---

**Geschätzte Zeit:** 60-90 Minuten  
**Nächster Schritt:** Routen & Middleware im nächsten Modul vertiefen!
