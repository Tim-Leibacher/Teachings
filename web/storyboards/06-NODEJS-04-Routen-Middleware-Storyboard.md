# Storyboard: Express.js – Routen & Middleware

**Modul:** Node.js & Express.js  
**Thema:** Routen & Middleware  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Geschätzte Videolänge:** 10-12 Minuten  
**Voraussetzungen:** Express.js Einführung abgeschlossen, einfache Server erstellt  
**Autor:** Tim Leibacher

---

## Video-Übersicht

**Lernziele:**
- Routen-Organisation und Best Practices verstehen
- HTTP-Methoden (GET, POST, PUT, DELETE) anwenden
- Middleware-Konzept verstehen und eigene Middleware schreiben
- Eingebaute und externe Middleware nutzen
- Request-Response-Zyklus verstehen

**Benötigte Ressourcen:**
- VS Code mit Portfolio-Projekt
- Node.js und npm installiert
- Express.js Projekt aus vorherigem Modul
- Terminal/PowerShell
- Browser für Tests

---

## Szene 1: Intro – Wiederholung und Ausblick (30 Sek.)

### Sprechertext
"Im letzten Video hast du Express.js kennengelernt und deinen ersten Server von http-Modul auf Express umgestellt. Du hast Routen mit app.get() erstellt und statische Dateien ausgeliefert. In diesem Video vertiefen wir das Routing und du lernst das wichtigste Konzept in Express: Middleware. Middleware sind Funktionen, die zwischen Request und Response ausgeführt werden. Am Ende kannst du professionelle API-Routen erstellen und verstehst, wie Express Anfragen verarbeitet."

### Bildschirmdarstellung
- BAND-Logo mit Titel: **"Express.js – Routen & Middleware"**
- Text-Overlay:
  - **"Routen organisieren"**
  - **"HTTP-Methoden verstehen"**
  - **"Middleware meistern"**

### Hinweise
- BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A, #E87722)
- Fade-In Animation

---

## Szene 2: Der Request-Response-Zyklus (1 Min.)

### Sprechertext
"Bevor wir tiefer einsteigen, schauen wir uns an, was bei einer HTTP-Anfrage passiert. Der Browser sendet einen Request an deinen Server – zum Beispiel GET /api/skills. Express empfängt diesen Request und durchläuft mehrere Middleware-Funktionen. Jede Middleware kann den Request verändern, etwas loggen oder prüfen. Am Ende erreicht der Request deine Route-Handler-Funktion, die eine Response zurücksendet. Diesen Ablauf nennt man Request-Response-Zyklus."

### Bildschirmdarstellung

**Visualisierung des Zyklus:**
```
┌─────────────────────────────────────────────────────────────┐
│                    Request-Response-Zyklus                   │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   Browser                                                    │
│      │                                                       │
│      ▼ GET /api/skills                                       │
│   ┌──────────────────────────────────────────────┐          │
│   │            Express Server                     │          │
│   │                                               │          │
│   │   Request ──► Middleware 1 ──► Middleware 2   │          │
│   │                                    │          │          │
│   │                                    ▼          │          │
│   │                             Route Handler     │          │
│   │                                    │          │          │
│   │   Response ◄─────────────────────────        │          │
│   └──────────────────────────────────────────────┘          │
│      │                                                       │
│      ▼                                                       │
│   Browser zeigt Daten                                        │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

Text-Overlay:
- **Request** = Anfrage vom Browser
- **Middleware** = Zwischenstationen
- **Response** = Antwort vom Server

### Hinweise
- Animation: Request durchläuft Station für Station
- Pfeil-Animation von Request zu Response
- Betone: Middleware ist wie eine Kette

---

## Szene 3: Routen-Grundlagen vertiefen (1 Min. 30 Sek.)

### Sprechertext
"Du kennst bereits app.get() für GET-Anfragen. Aber HTTP kennt mehr Methoden: POST zum Erstellen, PUT zum vollständigen Aktualisieren, PATCH für teilweise Änderungen und DELETE zum Löschen. In Express nutzt du für jede Methode eine entsprechende Funktion. Schauen wir uns das an einem Beispiel an: Eine API für Projekte in deinem Portfolio."

### Bildschirmdarstellung

VS Code mit Code-Beispiel:

```javascript
// server.js - HTTP-Methoden für Portfolio-API

const express = require('express');
const app = express();

// Middleware für JSON-Body
app.use(express.json());

// Projekte-Daten (später aus Datenbank)
let projects = [
    { id: 1, title: 'Portfolio-Website', status: 'in-progress' },
    { id: 2, title: 'HTTP-Server', status: 'completed' }
];

// GET - Alle Projekte abrufen
app.get('/api/projects', (req, res) => {
    res.json(projects);
});

// GET - Einzelnes Projekt abrufen
app.get('/api/projects/:id', (req, res) => {
    const project = projects.find(p => p.id === parseInt(req.params.id));
    if (!project) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    res.json(project);
});

// POST - Neues Projekt erstellen
app.post('/api/projects', (req, res) => {
    const newProject = {
        id: projects.length + 1,
        title: req.body.title,
        status: req.body.status || 'planned'
    };
    projects.push(newProject);
    res.status(201).json(newProject);
});

// PUT - Projekt vollständig aktualisieren
app.put('/api/projects/:id', (req, res) => {
    const index = projects.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    projects[index] = { id: parseInt(req.params.id), ...req.body };
    res.json(projects[index]);
});

// DELETE - Projekt löschen
app.delete('/api/projects/:id', (req, res) => {
    const index = projects.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    projects.splice(index, 1);
    res.status(204).send();
});

app.listen(3000, () => {
    console.log('Server läuft auf http://localhost:3000');
});
```

**HTTP-Methoden-Übersicht einblenden:**
```
┌─────────────┬─────────────────────────┬────────────────┐
│  Methode    │  Verwendung             │  Express       │
├─────────────┼─────────────────────────┼────────────────┤
│  GET        │  Daten abrufen          │  app.get()     │
│  POST       │  Neu erstellen          │  app.post()    │
│  PUT        │  Vollständig ändern     │  app.put()     │
│  PATCH      │  Teilweise ändern       │  app.patch()   │
│  DELETE     │  Löschen                │  app.delete()  │
└─────────────┴─────────────────────────┴────────────────┘
```

### Hinweise
- Code schrittweise zeigen, nicht alles auf einmal
- Betone: express.json() ist wichtig für POST/PUT
- Erkläre req.params.id für dynamische Routen

---

## Szene 4: Route-Parameter und Query-Strings (1 Min.)

### Sprechertext
"Bei Routen gibt es zwei Arten von Parametern: Route-Parameter und Query-Strings. Route-Parameter sind Teil der URL – zum Beispiel /api/projects/1. Die 1 ist ein Parameter. Query-Strings stehen nach dem Fragezeichen – zum Beispiel /api/projects?status=completed. Beide haben unterschiedliche Einsatzzwecke. Route-Parameter identifizieren eine Ressource eindeutig. Query-Strings filtern oder sortieren Ergebnisse."

### Bildschirmdarstellung

VS Code mit Beispielen:

```javascript
// Route-Parameter: /api/projects/1
app.get('/api/projects/:id', (req, res) => {
    const projectId = req.params.id;  // "1"
    console.log('Projekt-ID:', projectId);
    // Projekt mit dieser ID suchen...
});

// Mehrere Route-Parameter: /api/users/5/projects/3
app.get('/api/users/:userId/projects/:projectId', (req, res) => {
    const userId = req.params.userId;      // "5"
    const projectId = req.params.projectId; // "3"
    // Projekt eines bestimmten Users suchen...
});

// Query-Strings: /api/projects?status=completed&sort=title
app.get('/api/projects', (req, res) => {
    const status = req.query.status;  // "completed"
    const sort = req.query.sort;      // "title"
    
    let result = projects;
    
    // Nach Status filtern
    if (status) {
        result = result.filter(p => p.status === status);
    }
    
    // Nach Feld sortieren
    if (sort) {
        result = result.sort((a, b) => 
            a[sort].localeCompare(b[sort])
        );
    }
    
    res.json(result);
});
```

**Vergleich einblenden:**
```
┌─────────────────────────────────────────────────────────────┐
│  Route-Parameter vs. Query-Strings                          │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Route-Parameter:                                            │
│  /api/projects/:id  →  req.params.id                        │
│  Beispiel: /api/projects/5                                   │
│  Zweck: Eindeutige Identifikation                           │
│                                                              │
│  Query-Strings:                                              │
│  /api/projects?key=value  →  req.query.key                  │
│  Beispiel: /api/projects?status=completed                   │
│  Zweck: Filtern, Sortieren, Paginieren                      │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Hinweise
- Zeige beide Varianten im Browser
- Betone Unterschied: req.params vs. req.query
- Praxis-Beispiel: Filterung nach Status

---

## Szene 5: Was ist Middleware? (1 Min. 30 Sek.)

### Sprechertext
"Jetzt zum Herzstück von Express: Middleware. Eine Middleware ist einfach eine Funktion mit drei Parametern: request, response und next. next ist eine Funktion, die die nächste Middleware aufruft. Ohne next-Aufruf stoppt die Kette und der Request bleibt hängen. Middleware kann alles machen: Requests loggen, Benutzer authentifizieren, Daten validieren oder Header setzen. Express selbst besteht fast nur aus Middleware."

### Bildschirmdarstellung

**Middleware-Anatomie:**

```javascript
// Anatomie einer Middleware-Funktion
const meineMiddleware = (req, res, next) => {
    // 1. Etwas mit dem Request machen
    console.log('Request erhalten:', req.method, req.url);
    
    // 2. Etwas zum Request hinzufügen
    req.zeitstempel = Date.now();
    
    // 3. WICHTIG: next() aufrufen!
    next();
    
    // Ohne next() → Request bleibt hängen!
};

// Middleware registrieren
app.use(meineMiddleware);
```

**Visualisierung der Middleware-Kette:**
```
Request
   │
   ▼
┌──────────────────┐
│ Middleware 1     │  ──► next() ───┐
│ (Logger)         │                │
└──────────────────┘                │
                                    ▼
                    ┌──────────────────┐
                    │ Middleware 2     │  ──► next() ───┐
                    │ (Auth)           │                │
                    └──────────────────┘                │
                                                        ▼
                                        ┌──────────────────┐
                                        │ Route Handler    │
                                        │ (Response)       │
                                        └──────────────────┘
                                                │
                                                ▼
                                           Response
```

### Hinweise
- Animation: Request durchläuft Middleware-Stationen
- Betone: next() ist entscheidend
- Zeige was passiert ohne next() (Request timeout)

---

## Szene 6: Eingebaute Middleware (1 Min.)

### Sprechertext
"Express bringt einige wichtige Middleware-Funktionen mit. express.json() parsed JSON im Request-Body – ohne das kannst du keine POST-Daten empfangen. express.urlencoded() parsed Formulardaten. Und express.static() lieferst statische Dateien aus – das kennst du schon. Alle drei sind sogenannte Built-in Middleware."

### Bildschirmdarstellung

VS Code:

```javascript
const express = require('express');
const path = require('path');
const app = express();

// === Eingebaute Middleware ===

// 1. JSON-Body parsen (für API-Requests)
app.use(express.json());
// Ermöglicht: req.body bei POST/PUT mit JSON

// 2. URL-encoded Body parsen (für HTML-Formulare)
app.use(express.urlencoded({ extended: true }));
// Ermöglicht: req.body bei Formular-Submits

// 3. Statische Dateien ausliefern
app.use(express.static(path.join(__dirname, 'public')));
// Liefert: HTML, CSS, JS, Bilder aus /public

// === Test-Route für POST ===
app.post('/api/test', (req, res) => {
    console.log('Body erhalten:', req.body);
    res.json({ erhalten: req.body });
});

app.listen(3000);
```

**Übersicht einblenden:**
```
┌─────────────────────────────────────────────────────────────┐
│  Eingebaute Express-Middleware                               │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  express.json()                                              │
│  → Parsed JSON aus Request-Body                              │
│  → Ermöglicht req.body                                       │
│                                                              │
│  express.urlencoded({ extended: true })                      │
│  → Parsed Formulardaten                                      │
│  → Für HTML-Forms                                            │
│                                                              │
│  express.static('public')                                    │
│  → Liefert statische Dateien                                 │
│  → HTML, CSS, JS, Bilder                                     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Hinweise
- Zeige POST-Request mit und ohne express.json()
- Demonstriere req.body = undefined ohne Middleware
- Betone Reihenfolge: Middleware vor Routen

---

## Szene 7: Eigene Middleware schreiben (2 Min.)

### Sprechertext
"Jetzt schreiben wir eigene Middleware. Das erste Beispiel ist ein Logger, der jeden Request protokolliert. Wir erstellen eine Funktion, die Zeitstempel, HTTP-Methode und URL ausgibt. Dann rufen wir next() auf, damit der Request weitergeht. Die zweite Middleware misst, wie lange ein Request dauert – nützlich für Performance-Analysen."

### Bildschirmdarstellung

VS Code – Schritt für Schritt:

```javascript
const express = require('express');
const app = express();

// === Eigene Middleware 1: Request-Logger ===
const requestLogger = (req, res, next) => {
    const timestamp = new Date().toISOString();
    console.log(`[${timestamp}] ${req.method} ${req.url}`);
    next();
};

// === Eigene Middleware 2: Request-Timer ===
const requestTimer = (req, res, next) => {
    const start = Date.now();
    
    // Wird ausgeführt, wenn Response gesendet wird
    res.on('finish', () => {
        const duration = Date.now() - start;
        console.log(`  → Antwort in ${duration}ms`);
    });
    
    next();
};

// === Eigene Middleware 3: Custom Header ===
const addCustomHeaders = (req, res, next) => {
    res.setHeader('X-Powered-By', 'Portfolio-Server');
    res.setHeader('X-Response-Time', Date.now().toString());
    next();
};

// Middleware registrieren (Reihenfolge wichtig!)
app.use(requestLogger);
app.use(requestTimer);
app.use(addCustomHeaders);
app.use(express.json());

// Test-Routen
app.get('/', (req, res) => {
    res.send('<h1>Startseite</h1>');
});

app.get('/api/info', (req, res) => {
    res.json({ name: 'Portfolio-Server', version: '1.0' });
});

app.listen(3000, () => {
    console.log('Server läuft auf http://localhost:3000');
});
```

**Terminal-Ausgabe zeigen:**
```
[2025-01-15T10:30:45.123Z] GET /
  → Antwort in 3ms
[2025-01-15T10:30:48.456Z] GET /api/info
  → Antwort in 1ms
```

### Hinweise
- Code live eintippen, nicht kopieren
- Zeige Terminal-Ausgabe bei Requests
- Erkläre res.on('finish') für Timer

---

## Szene 8: Middleware für bestimmte Routen (1 Min.)

### Sprechertext
"Nicht jede Middleware muss für alle Routen gelten. Du kannst Middleware auf bestimmte Pfade beschränken. Mit app.use('/api', middleware) gilt die Middleware nur für API-Routen. Du kannst auch mehrere Middleware-Funktionen hintereinander in einer Route verwenden. Das ist praktisch für Authentifizierung oder Validierung."

### Bildschirmdarstellung

VS Code:

```javascript
// Middleware nur für /api-Routen
const apiLogger = (req, res, next) => {
    console.log('API-Aufruf:', req.method, req.url);
    next();
};

// Nur für /api/* Routen
app.use('/api', apiLogger);

// Einfache Auth-Middleware (Demo)
const checkAuth = (req, res, next) => {
    const apiKey = req.headers['x-api-key'];
    
    if (!apiKey || apiKey !== 'geheim123') {
        return res.status(401).json({ error: 'Nicht autorisiert' });
    }
    
    next();
};

// Middleware in einzelner Route
app.get('/api/protected', checkAuth, (req, res) => {
    res.json({ message: 'Geschützte Daten', secret: 42 });
});

// Ohne Auth
app.get('/api/public', (req, res) => {
    res.json({ message: 'Öffentliche Daten' });
});

// Mehrere Middleware in einer Route
const validateProject = (req, res, next) => {
    if (!req.body.title) {
        return res.status(400).json({ error: 'Titel erforderlich' });
    }
    next();
};

app.post('/api/projects', checkAuth, validateProject, (req, res) => {
    res.json({ message: 'Projekt erstellt', data: req.body });
});
```

**Visualisierung:**
```
┌─────────────────────────────────────────────────────────────┐
│  Middleware-Anwendung                                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  app.use(middleware)                                         │
│  → Gilt für ALLE Routen                                      │
│                                                              │
│  app.use('/api', middleware)                                 │
│  → Gilt nur für /api/*                                       │
│                                                              │
│  app.get('/route', middleware, handler)                      │
│  → Gilt nur für diese eine Route                             │
│                                                              │
│  app.get('/route', mw1, mw2, mw3, handler)                   │
│  → Mehrere Middleware für eine Route                         │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Hinweise
- Zeige Auth-Test mit und ohne Header
- Demonstriere Validierung bei POST
- Betone: return bei res.status() ist wichtig

---

## Szene 9: Externe Middleware – Morgan und CORS (1 Min.)

### Sprechertext
"Die Express-Community hat viele nützliche Middleware-Pakete entwickelt. Morgan ist ein professioneller Logger, der verschiedene Formate unterstützt. CORS ermöglicht Anfragen von anderen Domains – wichtig, wenn dein Frontend auf einer anderen URL läuft als dein Backend. Beide installierst du mit npm und bindest sie mit app.use() ein."

### Bildschirmdarstellung

**Terminal:**
```bash
npm install morgan cors
```

**VS Code:**
```javascript
const express = require('express');
const morgan = require('morgan');
const cors = require('cors');

const app = express();

// Morgan: Professionelles Logging
// Formate: 'dev', 'combined', 'common', 'short', 'tiny'
app.use(morgan('dev'));

// CORS: Cross-Origin Requests erlauben
app.use(cors());

// Oder mit Optionen:
app.use(cors({
    origin: 'http://localhost:5173',  // Nur diese Domain
    methods: ['GET', 'POST'],          // Nur diese Methoden
    credentials: true                  // Cookies erlauben
}));

app.use(express.json());

app.get('/api/test', (req, res) => {
    res.json({ message: 'CORS funktioniert!' });
});

app.listen(3000);
```

**Terminal-Ausgabe (Morgan 'dev'):**
```
GET /api/test 200 3.456 ms - 32
POST /api/projects 201 5.123 ms - 87
GET /api/unknown 404 1.234 ms - 45
```

**Übersicht einblenden:**
```
┌─────────────────────────────────────────────────────────────┐
│  Beliebte Express-Middleware                                 │
├─────────────────────────────────────────────────────────────┤
│  morgan     → HTTP Request Logger                            │
│  cors       → Cross-Origin Resource Sharing                  │
│  helmet     → Sicherheits-Header setzen                      │
│  compression → Response-Komprimierung                        │
│  express-rate-limit → Anfragen begrenzen                     │
└─────────────────────────────────────────────────────────────┘
```

### Hinweise
- Zeige Morgan-Ausgabe in verschiedenen Formaten
- Erkläre CORS-Problem kurz (Browser-Sicherheit)
- Erwähne helmet für Sicherheit

---

## Szene 10: Middleware-Reihenfolge (1 Min.)

### Sprechertext
"Die Reihenfolge der Middleware ist entscheidend. Express führt sie in der Reihenfolge aus, in der du sie registrierst. Logger sollten früh kommen, damit sie alle Requests erfassen. Body-Parser müssen vor Routen stehen, die req.body nutzen. Error-Handler müssen am Ende stehen. Falsche Reihenfolge führt zu schwer zu findenden Bugs."

### Bildschirmdarstellung

```javascript
const express = require('express');
const morgan = require('morgan');
const cors = require('cors');
const path = require('path');

const app = express();

// === RICHTIGE REIHENFOLGE ===

// 1. Logging (ganz früh)
app.use(morgan('dev'));

// 2. Sicherheit und CORS
app.use(cors());

// 3. Body-Parser
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// 4. Statische Dateien
app.use(express.static(path.join(__dirname, 'public')));

// 5. Eigene Middleware
app.use((req, res, next) => {
    req.requestTime = Date.now();
    next();
});

// 6. API-Routen
app.get('/api/info', (req, res) => {
    res.json({ zeit: req.requestTime });
});

// 7. 404-Handler (nach allen Routen)
app.use((req, res, next) => {
    res.status(404).json({ error: 'Route nicht gefunden' });
});

// 8. Error-Handler (GANZ am Ende, mit 4 Parametern!)
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: 'Serverfehler' });
});

app.listen(3000);
```

**Visualisierung:**
```
┌─────────────────────────────────────────────────────────────┐
│  Empfohlene Middleware-Reihenfolge                           │
├─────────────────────────────────────────────────────────────┤
│   1. Logging (morgan)                                        │
│   2. Sicherheit (cors, helmet)                               │
│   3. Body-Parser (express.json, express.urlencoded)         │
│   4. Statische Dateien (express.static)                      │
│   5. Eigene Middleware                                       │
│   6. Routen (app.get, app.post, ...)                        │
│   7. 404-Handler                                             │
│   8. Error-Handler (4 Parameter!)                            │
└─────────────────────────────────────────────────────────────┘
```

### Hinweise
- Betone: Error-Handler hat VIER Parameter
- Zeige Fehler bei falscher Reihenfolge
- 404-Handler muss nach allen Routen stehen

---

## Szene 11: Zusammenfassung (30 Sek.)

### Sprechertext
"Fassen wir zusammen: HTTP-Methoden definieren, was mit Daten passieren soll – GET liest, POST erstellt, PUT aktualisiert, DELETE löscht. Middleware sind Funktionen zwischen Request und Response. Sie können loggen, authentifizieren, validieren und vieles mehr. Die Reihenfolge ist wichtig: Logger früh, Error-Handler spät. In den Aufträgen baust du eine vollständige API mit eigener Middleware für dein Portfolio."

### Bildschirmdarstellung

**Zusammenfassung als Checkliste:**
```
╔═══════════════════════════════════════════════════════════╗
║   Routen & Middleware - Das hast du gelernt               ║
╠═══════════════════════════════════════════════════════════╣
║   ✓ HTTP-Methoden: GET, POST, PUT, DELETE                 ║
║   ✓ Route-Parameter: req.params                           ║
║   ✓ Query-Strings: req.query                              ║
║   ✓ Middleware-Konzept: (req, res, next)                  ║
║   ✓ Eingebaute Middleware: json(), static()               ║
║   ✓ Eigene Middleware schreiben                           ║
║   ✓ Externe Middleware: morgan, cors                      ║
║   ✓ Middleware-Reihenfolge beachten                       ║
╚═══════════════════════════════════════════════════════════╝
```

Text-Overlay:
- **"Nächster Schritt: RESTful APIs bauen"**
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

1. **`server-routes.js`** – Routen-Beispiele
2. **`server-middleware.js`** – Middleware-Beispiele
3. **`server-complete.js`** – Vollständiger Server
4. **`public/index.html`** – Test-HTML-Datei
5. **`package.json`** – Mit allen Dependencies

---

**Gesamtlänge:** ca. 10-12 Minuten  
**Schwierigkeitsgrad:** Mittel  
**Tempo:** Ruhig und verständlich, mit Pausen zum Nachvollziehen
