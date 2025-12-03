# Auftrag 2: Eigene Middleware für dein Portfolio entwickeln

## Ziel

Du verstehst das Middleware-Konzept in Express und entwickelst eigene Middleware-Funktionen für Logging, Request-Timing und Validierung. Du lernst, wie der Request-Response-Zyklus funktioniert und wie Middleware diesen beeinflusst.

## Beschreibung

Middleware sind Funktionen, die zwischen dem Eingang eines Requests und dem Senden der Response ausgeführt werden. Jede Middleware hat Zugriff auf das Request-Objekt, das Response-Objekt und die next()-Funktion. In diesem Auftrag entwickelst du drei eigene Middleware-Funktionen, die in professionellen Anwendungen unverzichtbar sind.

**Geschätzte Zeit:** 45-60 Minuten  
**Voraussetzung:** Auftrag 1 abgeschlossen

---

## Teil 1: Middleware-Grundlagen verstehen (10 Min)

### 1.1 Projekt erweitern

Öffne dein Projekt aus Auftrag 1 oder erstelle eine neue Datei **`server-middleware.js`**:

```javascript
// server-middleware.js - Middleware verstehen

const express = require('express');
const app = express();
const PORT = 3000;

// === Einfachste Middleware ===
const einfacheMiddleware = (req, res, next) => {
    console.log('Middleware wurde aufgerufen!');
    next(); // WICHTIG: Ohne next() bleibt der Request hängen
};

// Middleware registrieren
app.use(einfacheMiddleware);

// Test-Route
app.get('/', (req, res) => {
    res.send('Startseite');
});

app.listen(PORT, () => {
    console.log(`Server: http://localhost:${PORT}`);
});
```

### 1.2 Was passiert ohne next()?

Teste folgendes:

```javascript
const ohneNext = (req, res, next) => {
    console.log('Middleware ohne next()');
    // next() fehlt absichtlich
};

app.use(ohneNext);
```

Starte den Server und rufe http://localhost:3000 auf. Was passiert?

**Ergebnis:** Der Browser lädt endlos, bis ein Timeout kommt. Ohne `next()` wird die Middleware-Kette unterbrochen und die Route nie erreicht.

### 1.3 Middleware-Kette visualisieren

```javascript
// Mehrere Middleware hintereinander
const middleware1 = (req, res, next) => {
    console.log('1. Erste Middleware');
    next();
};

const middleware2 = (req, res, next) => {
    console.log('2. Zweite Middleware');
    next();
};

const middleware3 = (req, res, next) => {
    console.log('3. Dritte Middleware');
    next();
};

// Reihenfolge der Registrierung = Ausführungsreihenfolge
app.use(middleware1);
app.use(middleware2);
app.use(middleware3);

app.get('/', (req, res) => {
    console.log('4. Route-Handler');
    res.send('Fertig!');
});
```

**Erwartete Konsolen-Ausgabe:**
```
1. Erste Middleware
2. Zweite Middleware
3. Dritte Middleware
4. Route-Handler
```

---

## Teil 2: Request-Logger entwickeln (15 Min)

### 2.1 Einfacher Logger

Erstelle eine Datei **`middleware/logger.js`** (erstelle zuerst den Ordner `middleware`):

```javascript
// middleware/logger.js - Request-Logger

function requestLogger(req, res, next) {
    const timestamp = new Date().toISOString();
    const method = req.method;
    const url = req.url;
    const ip = req.ip || req.connection.remoteAddress;
    
    console.log(`[${timestamp}] ${method} ${url} - IP: ${ip}`);
    
    next();
}

module.exports = requestLogger;
```

### 2.2 Logger einbinden

In deiner **`server.js`**:

```javascript
const express = require('express');
const requestLogger = require('./middleware/logger');

const app = express();

// Logger früh einbinden (vor anderen Middleware)
app.use(requestLogger);

// Restlicher Code...
```

### 2.3 Logger erweitern - Farbige Ausgabe

Erweitere **`middleware/logger.js`**:

```javascript
// middleware/logger.js - Request-Logger mit Farben

// ANSI-Farbcodes für Terminal
const colors = {
    reset: '\x1b[0m',
    green: '\x1b[32m',
    yellow: '\x1b[33m',
    red: '\x1b[31m',
    blue: '\x1b[34m',
    gray: '\x1b[90m'
};

// Farbe basierend auf HTTP-Methode
function getMethodColor(method) {
    switch (method) {
        case 'GET': return colors.green;
        case 'POST': return colors.yellow;
        case 'PUT': return colors.blue;
        case 'DELETE': return colors.red;
        default: return colors.reset;
    }
}

function requestLogger(req, res, next) {
    const timestamp = new Date().toISOString();
    const method = req.method;
    const url = req.url;
    const methodColor = getMethodColor(method);
    
    console.log(
        `${colors.gray}[${timestamp}]${colors.reset} ` +
        `${methodColor}${method}${colors.reset} ` +
        `${url}`
    );
    
    next();
}

module.exports = requestLogger;
```

Teste verschiedene Requests und beobachte die farbige Ausgabe im Terminal.

---

## Teil 3: Request-Timer entwickeln (10 Min)

### 3.1 Response-Zeit messen

Erstelle **`middleware/timer.js`**:

```javascript
// middleware/timer.js - Request-Timer

function requestTimer(req, res, next) {
    // Startzeit speichern
    const start = Date.now();
    
    // Original res.json überschreiben
    const originalJson = res.json.bind(res);
    res.json = (body) => {
        const duration = Date.now() - start;
        console.log(`  → Response in ${duration}ms`);
        return originalJson(body);
    };
    
    // Original res.send überschreiben
    const originalSend = res.send.bind(res);
    res.send = (body) => {
        const duration = Date.now() - start;
        console.log(`  → Response in ${duration}ms`);
        return originalSend(body);
    };
    
    next();
}

module.exports = requestTimer;
```

### 3.2 Alternative: res.on('finish')

Eine elegantere Methode:

```javascript
// middleware/timer.js - Elegante Version

function requestTimer(req, res, next) {
    const start = Date.now();
    
    // Event-Listener für Response-Ende
    res.on('finish', () => {
        const duration = Date.now() - start;
        const status = res.statusCode;
        
        // Farbe basierend auf Status
        let statusColor = '\x1b[32m'; // Grün
        if (status >= 400) statusColor = '\x1b[31m'; // Rot
        else if (status >= 300) statusColor = '\x1b[33m'; // Gelb
        
        console.log(
            `  → ${statusColor}${status}\x1b[0m in ${duration}ms`
        );
    });
    
    next();
}

module.exports = requestTimer;
```

### 3.3 Timer einbinden

In **`server.js`**:

```javascript
const requestLogger = require('./middleware/logger');
const requestTimer = require('./middleware/timer');

// Reihenfolge: Logger vor Timer
app.use(requestLogger);
app.use(requestTimer);
```

**Erwartete Ausgabe:**
```
[2025-01-15T14:30:00.000Z] GET /api/projects
  → 200 in 5ms
```

---

## Teil 4: Validierungs-Middleware entwickeln (15 Min)

### 4.1 Projekt-Validierung

Erstelle **`middleware/validators.js`**:

```javascript
// middleware/validators.js - Validierung für Projekte

function validateProject(req, res, next) {
    const { title, status, technologies } = req.body;
    const errors = [];
    
    // Titel prüfen
    if (!title || typeof title !== 'string') {
        errors.push('Titel ist erforderlich und muss ein Text sein');
    } else if (title.length < 3) {
        errors.push('Titel muss mindestens 3 Zeichen haben');
    } else if (title.length > 100) {
        errors.push('Titel darf maximal 100 Zeichen haben');
    }
    
    // Status prüfen (falls vorhanden)
    const validStatuses = ['planned', 'in-progress', 'completed', 'paused'];
    if (status && !validStatuses.includes(status)) {
        errors.push(`Status muss einer von: ${validStatuses.join(', ')} sein`);
    }
    
    // Technologies prüfen (falls vorhanden)
    if (technologies && !Array.isArray(technologies)) {
        errors.push('Technologies muss ein Array sein');
    }
    
    // Fehler gefunden?
    if (errors.length > 0) {
        return res.status(400).json({
            error: 'Validierungsfehler',
            details: errors
        });
    }
    
    // Alles okay, weiter zur nächsten Middleware/Route
    next();
}

module.exports = { validateProject };
```

### 4.2 Validierung in Routen einbinden

In **`server.js`**:

```javascript
const { validateProject } = require('./middleware/validators');

// Validierung nur für POST und PUT
app.post('/api/projects', validateProject, (req, res) => {
    // Diese Funktion wird nur erreicht, wenn Validierung erfolgreich
    const newProject = {
        id: nextId++,
        ...req.body
    };
    projects.push(newProject);
    res.status(201).json(newProject);
});

app.put('/api/projects/:id', validateProject, (req, res) => {
    // Aktualisierungslogik...
});
```

### 4.3 Validierung testen

In **`test.http`**:

```http
### Ungültiger Request - Titel fehlt
POST http://localhost:3000/api/projects
Content-Type: application/json

{
    "description": "Ohne Titel"
}

### Ungültiger Request - Titel zu kurz
POST http://localhost:3000/api/projects
Content-Type: application/json

{
    "title": "AB"
}

### Ungültiger Request - Falscher Status
POST http://localhost:3000/api/projects
Content-Type: application/json

{
    "title": "Mein Projekt",
    "status": "ungueltig"
}

### Gültiger Request
POST http://localhost:3000/api/projects
Content-Type: application/json

{
    "title": "Mein neues Projekt",
    "description": "Eine tolle Beschreibung",
    "technologies": ["JavaScript", "Node.js"],
    "status": "planned"
}
```

---

## Teil 5: Vollständiger Server mit allen Middleware (5 Min)

### 5.1 Alles zusammenfügen

**Projektstruktur:**
```
portfolio-api/
├── middleware/
│   ├── logger.js
│   ├── timer.js
│   └── validators.js
├── server.js
├── test.http
└── package.json
```

**Finale `server.js`:**

```javascript
// server.js - Portfolio-API mit Middleware

const express = require('express');
const path = require('path');
const requestLogger = require('./middleware/logger');
const requestTimer = require('./middleware/timer');
const { validateProject } = require('./middleware/validators');

const app = express();
const PORT = 3000;

// === Globale Middleware (Reihenfolge wichtig!) ===
app.use(requestLogger);        // 1. Logging
app.use(requestTimer);         // 2. Timing
app.use(express.json());       // 3. JSON-Body parsen

// === Daten ===
let projects = [
    { id: 1, title: 'Portfolio-Website', status: 'in-progress' },
    { id: 2, title: 'Express-API', status: 'completed' }
];
let nextId = 3;

// === Routen ===

app.get('/', (req, res) => {
    res.json({
        message: 'Portfolio-API',
        endpoints: {
            'GET /api/projects': 'Alle Projekte',
            'GET /api/projects/:id': 'Einzelnes Projekt',
            'POST /api/projects': 'Neues Projekt (mit Validierung)',
            'PUT /api/projects/:id': 'Projekt aktualisieren',
            'DELETE /api/projects/:id': 'Projekt löschen'
        }
    });
});

app.get('/api/projects', (req, res) => {
    res.json({ count: projects.length, data: projects });
});

app.get('/api/projects/:id', (req, res) => {
    const project = projects.find(p => p.id === parseInt(req.params.id));
    if (!project) {
        return res.status(404).json({ error: 'Nicht gefunden' });
    }
    res.json(project);
});

// POST mit Validierung
app.post('/api/projects', validateProject, (req, res) => {
    const newProject = { id: nextId++, ...req.body };
    projects.push(newProject);
    res.status(201).json(newProject);
});

// PUT mit Validierung
app.put('/api/projects/:id', validateProject, (req, res) => {
    const index = projects.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ error: 'Nicht gefunden' });
    }
    projects[index] = { id: parseInt(req.params.id), ...req.body };
    res.json(projects[index]);
});

app.delete('/api/projects/:id', (req, res) => {
    const index = projects.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ error: 'Nicht gefunden' });
    }
    const deleted = projects.splice(index, 1)[0];
    res.json({ message: 'Gelöscht', data: deleted });
});

// === Server starten ===
app.listen(PORT, () => {
    console.log('\n========================================');
    console.log('   Portfolio-API mit Middleware');
    console.log('========================================');
    console.log(`Server: http://localhost:${PORT}`);
    console.log('========================================\n');
});
```

---

## Erfolgskriterien

- [ ] Middleware-Konzept verstanden (req, res, next)
- [ ] next() korrekt verwendet
- [ ] Logger-Middleware zeigt alle Requests
- [ ] Timer-Middleware misst Response-Zeit
- [ ] Validierungs-Middleware prüft Eingaben
- [ ] Middleware in separate Dateien ausgelagert
- [ ] Richtige Reihenfolge der Middleware
- [ ] Fehlerhafte Requests werden abgefangen

## Tipps

**Middleware-Reihenfolge:**
1. Logging (ganz früh)
2. Timing
3. Body-Parser (express.json)
4. Eigene globale Middleware
5. Routen mit spezifischer Middleware
6. Error-Handler (ganz am Ende)

**Debugging:**
```javascript
// Debug-Middleware zum Testen
app.use((req, res, next) => {
    console.log('=== DEBUG ===');
    console.log('Headers:', req.headers);
    console.log('Body:', req.body);
    console.log('Query:', req.query);
    console.log('=============');
    next();
});
```

**next() mit Fehler:**
```javascript
// Fehler an Error-Handler weitergeben
if (fehler) {
    return next(new Error('Etwas ist schiefgegangen'));
}
```

## Reflexionsfragen

1. Was passiert, wenn du `next()` nicht aufrufst?
2. Warum ist die Reihenfolge der Middleware wichtig?
3. Wie unterscheidet sich `app.use(middleware)` von `app.get('/route', middleware, handler)`?
4. Wann sollte eine Middleware `return res.status().json()` verwenden statt `next()`?
5. Wie könntest du Logging in eine Datei statt in die Konsole schreiben?

## Weiterführende Links

- [Express Middleware](https://expressjs.com/en/guide/using-middleware.html) - Offizielle Dokumentation
- [Writing Middleware](https://expressjs.com/en/guide/writing-middleware.html) - Middleware schreiben
- [Node.js Console Colors](https://nodejs.org/api/util.html#utilinspectcolors) - ANSI-Farben
- [Express Best Practices](https://expressjs.com/en/advanced/best-practice-performance.html)

---

**Geschätzte Zeit:** 45-60 Minuten  
**Nächster Schritt:** In Auftrag 3 nutzt du externe Middleware und baust Error-Handling ein!
