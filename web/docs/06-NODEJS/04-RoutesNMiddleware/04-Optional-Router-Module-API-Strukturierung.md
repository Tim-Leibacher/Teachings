# Optionaler Auftrag: Router-Module und API-Strukturierung

## Ziel

Du lernst, wie du eine Express-API professionell strukturierst, indem du Router-Module verwendest. Du erstellst eine skalierbare Ordnerstruktur, die auch bei wachsenden Projekten übersichtlich bleibt. Zusätzlich implementierst du ein API-Versionierung und erweiterst dein Error-Handling.

## Beschreibung

In realen Projekten wächst der Code schnell. Eine einzelne `server.js` mit 500 Zeilen ist schwer zu warten. Express Router ermöglicht es, Routen in separate Module aufzuteilen. In diesem Auftrag strukturierst du deine Portfolio-API nach dem MVC-Muster (Model-View-Controller) und lernst Best Practices für grössere Anwendungen.

**Geschätzte Zeit:** 60-90 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzung:** Aufträge 1-3 abgeschlossen

---

## Teil 1: Express Router verstehen (15 Min)

### 1.1 Was ist ein Router?

Ein Express Router ist wie eine Mini-App, die eigene Middleware und Routen haben kann. Du kannst mehrere Router erstellen und sie an verschiedenen Pfaden einbinden.

### 1.2 Ersten Router erstellen

Erstelle den Ordner **`routes`** und darin **`routes/projects.js`**:

```javascript
// routes/projects.js - Routen für Projekte

const express = require('express');
const router = express.Router();

// Daten (später aus Controller/Model)
let projects = [
    { id: 1, title: 'Portfolio-Website', status: 'in-progress' },
    { id: 2, title: 'Express-API', status: 'completed' }
];
let nextId = 3;

// GET /api/projects
router.get('/', (req, res) => {
    res.json({ count: projects.length, data: projects });
});

// GET /api/projects/:id
router.get('/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const project = projects.find(p => p.id === id);
    
    if (!project) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    
    res.json(project);
});

// POST /api/projects
router.post('/', (req, res) => {
    const newProject = { id: nextId++, ...req.body };
    projects.push(newProject);
    res.status(201).json(newProject);
});

// PUT /api/projects/:id
router.put('/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === id);
    
    if (index === -1) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    
    projects[index] = { id, ...req.body };
    res.json(projects[index]);
});

// DELETE /api/projects/:id
router.delete('/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === id);
    
    if (index === -1) {
        return res.status(404).json({ error: 'Projekt nicht gefunden' });
    }
    
    const deleted = projects.splice(index, 1)[0];
    res.json({ message: 'Gelöscht', data: deleted });
});

module.exports = router;
```

### 1.3 Router in Server einbinden

In **`server.js`**:

```javascript
const express = require('express');
const projectsRouter = require('./routes/projects');

const app = express();

app.use(express.json());

// Router einbinden unter /api/projects
app.use('/api/projects', projectsRouter);

app.listen(3000);
```

Jetzt erreichst du alle Routen unter `/api/projects/*`.

---

## Teil 2: Professionelle Ordnerstruktur (20 Min)

### 2.1 MVC-Struktur erstellen

```
portfolio-api/
├── src/
│   ├── controllers/
│   │   ├── projectController.js
│   │   └── skillController.js
│   ├── middleware/
│   │   ├── errorHandler.js
│   │   ├── logger.js
│   │   └── validators.js
│   ├── models/
│   │   ├── Project.js
│   │   └── Skill.js
│   ├── routes/
│   │   ├── index.js
│   │   ├── projectRoutes.js
│   │   └── skillRoutes.js
│   └── app.js
├── logs/
├── public/
├── server.js
├── package.json
└── .env
```

### 2.2 Model erstellen

Erstelle **`src/models/Project.js`**:

```javascript
// src/models/Project.js - Daten-Model für Projekte

// Simulierte Datenbank (In-Memory)
let projects = [
    {
        id: 1,
        title: 'Portfolio-Website',
        description: 'Persönliche Portfolio-Seite',
        technologies: ['HTML', 'CSS', 'JavaScript', 'Node.js', 'Express'],
        status: 'in-progress',
        createdAt: new Date('2025-01-01'),
        updatedAt: new Date()
    },
    {
        id: 2,
        title: 'Express-API',
        description: 'RESTful API mit Express',
        technologies: ['Node.js', 'Express'],
        status: 'completed',
        createdAt: new Date('2025-01-10'),
        updatedAt: new Date()
    }
];

let nextId = 3;

// Model-Methoden
const Project = {
    // Alle Projekte abrufen
    findAll(filters = {}) {
        let result = [...projects];
        
        if (filters.status) {
            result = result.filter(p => p.status === filters.status);
        }
        
        if (filters.tech) {
            result = result.filter(p => 
                p.technologies.some(t => 
                    t.toLowerCase().includes(filters.tech.toLowerCase())
                )
            );
        }
        
        return result;
    },
    
    // Einzelnes Projekt finden
    findById(id) {
        return projects.find(p => p.id === id);
    },
    
    // Neues Projekt erstellen
    create(data) {
        const project = {
            id: nextId++,
            title: data.title,
            description: data.description || '',
            technologies: data.technologies || [],
            status: data.status || 'planned',
            createdAt: new Date(),
            updatedAt: new Date()
        };
        projects.push(project);
        return project;
    },
    
    // Projekt aktualisieren
    update(id, data) {
        const index = projects.findIndex(p => p.id === id);
        if (index === -1) return null;
        
        projects[index] = {
            ...projects[index],
            ...data,
            id, // ID nicht überschreiben
            updatedAt: new Date()
        };
        
        return projects[index];
    },
    
    // Projekt löschen
    delete(id) {
        const index = projects.findIndex(p => p.id === id);
        if (index === -1) return null;
        
        return projects.splice(index, 1)[0];
    },
    
    // Anzahl Projekte
    count() {
        return projects.length;
    }
};

module.exports = Project;
```

### 2.3 Controller erstellen

Erstelle **`src/controllers/projectController.js`**:

```javascript
// src/controllers/projectController.js - Business-Logik

const Project = require('../models/Project');
const { ApiError } = require('../middleware/errorHandler');

const projectController = {
    // GET /api/projects
    async getAll(req, res, next) {
        try {
            const filters = {
                status: req.query.status,
                tech: req.query.tech
            };
            
            const projects = Project.findAll(filters);
            
            res.json({
                success: true,
                count: projects.length,
                data: projects
            });
        } catch (error) {
            next(error);
        }
    },
    
    // GET /api/projects/:id
    async getOne(req, res, next) {
        try {
            const id = parseInt(req.params.id);
            
            if (isNaN(id)) {
                throw new ApiError('ID muss eine Zahl sein', 400);
            }
            
            const project = Project.findById(id);
            
            if (!project) {
                throw new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404);
            }
            
            res.json({
                success: true,
                data: project
            });
        } catch (error) {
            next(error);
        }
    },
    
    // POST /api/projects
    async create(req, res, next) {
        try {
            const project = Project.create(req.body);
            
            res.status(201).json({
                success: true,
                message: 'Projekt erstellt',
                data: project
            });
        } catch (error) {
            next(error);
        }
    },
    
    // PUT /api/projects/:id
    async update(req, res, next) {
        try {
            const id = parseInt(req.params.id);
            
            if (isNaN(id)) {
                throw new ApiError('ID muss eine Zahl sein', 400);
            }
            
            const project = Project.update(id, req.body);
            
            if (!project) {
                throw new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404);
            }
            
            res.json({
                success: true,
                message: 'Projekt aktualisiert',
                data: project
            });
        } catch (error) {
            next(error);
        }
    },
    
    // DELETE /api/projects/:id
    async delete(req, res, next) {
        try {
            const id = parseInt(req.params.id);
            
            if (isNaN(id)) {
                throw new ApiError('ID muss eine Zahl sein', 400);
            }
            
            const project = Project.delete(id);
            
            if (!project) {
                throw new ApiError(`Projekt mit ID ${id} nicht gefunden`, 404);
            }
            
            res.json({
                success: true,
                message: 'Projekt gelöscht',
                data: project
            });
        } catch (error) {
            next(error);
        }
    }
};

module.exports = projectController;
```

### 2.4 Routes aktualisieren

Erstelle **`src/routes/projectRoutes.js`**:

```javascript
// src/routes/projectRoutes.js - Routen-Definitionen

const express = require('express');
const router = express.Router();
const projectController = require('../controllers/projectController');
const { validateProject } = require('../middleware/validators');

// Routen definieren
router.get('/', projectController.getAll);
router.get('/:id', projectController.getOne);
router.post('/', validateProject, projectController.create);
router.put('/:id', validateProject, projectController.update);
router.delete('/:id', projectController.delete);

module.exports = router;
```

### 2.5 Router-Index für alle Routen

Erstelle **`src/routes/index.js`**:

```javascript
// src/routes/index.js - Zentrale Routen-Konfiguration

const express = require('express');
const router = express.Router();

const projectRoutes = require('./projectRoutes');
// const skillRoutes = require('./skillRoutes');

// API-Info
router.get('/', (req, res) => {
    res.json({
        name: 'Portfolio API',
        version: '1.0.0',
        endpoints: {
            projects: '/api/v1/projects',
            skills: '/api/v1/skills'
        }
    });
});

// Routen einbinden
router.use('/projects', projectRoutes);
// router.use('/skills', skillRoutes);

module.exports = router;
```

---

## Teil 3: API-Versionierung (10 Min)

### 3.1 Warum Versionierung?

Wenn du deine API änderst, können bestehende Clients kaputtgehen. Mit Versionierung kannst du neue Versionen bereitstellen, ohne alte zu brechen.

### 3.2 URL-basierte Versionierung

Erstelle **`src/app.js`**:

```javascript
// src/app.js - Express-App Konfiguration

const express = require('express');
const morgan = require('morgan');
const cors = require('cors');
const helmet = require('helmet');
const path = require('path');

const apiRoutes = require('./routes');
const { notFoundHandler, errorHandler } = require('./middleware/errorHandler');

const app = express();

// === Middleware ===
app.use(helmet());
app.use(cors());
app.use(morgan('dev'));
app.use(express.json());
app.use(express.static(path.join(__dirname, '../public')));

// === API-Routen mit Versionierung ===
app.use('/api/v1', apiRoutes);

// Redirect von /api auf aktuelle Version
app.get('/api', (req, res) => {
    res.redirect('/api/v1');
});

// === Error-Handler ===
app.use(notFoundHandler);
app.use(errorHandler);

module.exports = app;
```

### 3.3 Server-Entry-Point

Aktualisiere **`server.js`**:

```javascript
// server.js - Server-Einstiegspunkt

require('dotenv').config();

const app = require('./src/app');

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
    console.log(`
╔═══════════════════════════════════════════════════╗
║                                                   ║
║   Portfolio API v1.0                              ║
║                                                   ║
║   Server:  http://localhost:${PORT}                  ║
║   API:     http://localhost:${PORT}/api/v1           ║
║   Docs:    http://localhost:${PORT}/api/v1           ║
║                                                   ║
║   Environment: ${process.env.NODE_ENV || 'development'}                     ║
║                                                   ║
╚═══════════════════════════════════════════════════╝
    `);
});
```

### 3.4 Environment-Variablen

Erstelle **`.env`**:

```env
PORT=3000
NODE_ENV=development
```

Installiere dotenv:

```bash
npm install dotenv
```

---

## Teil 4: Rate-Limiting implementieren (10 Min)

### 4.1 Rate-Limiter installieren

```bash
npm install express-rate-limit
```

### 4.2 Rate-Limiter konfigurieren

Erstelle **`src/middleware/rateLimiter.js`**:

```javascript
// src/middleware/rateLimiter.js - Anfragen begrenzen

const rateLimit = require('express-rate-limit');

// Allgemeiner Limiter
const generalLimiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 Minuten
    max: 100, // 100 Anfragen pro IP
    message: {
        success: false,
        error: 'Zu viele Anfragen. Bitte warte 15 Minuten.'
    },
    standardHeaders: true, // Rate limit info in headers
    legacyHeaders: false
});

// Strikterer Limiter für sensible Operationen
const strictLimiter = rateLimit({
    windowMs: 60 * 60 * 1000, // 1 Stunde
    max: 10, // 10 Anfragen pro IP
    message: {
        success: false,
        error: 'Limit erreicht. Bitte warte 1 Stunde.'
    }
});

// API-Limiter
const apiLimiter = rateLimit({
    windowMs: 60 * 1000, // 1 Minute
    max: 30, // 30 Anfragen pro Minute
    message: {
        success: false,
        error: 'API-Limit erreicht. Bitte warte eine Minute.'
    }
});

module.exports = {
    generalLimiter,
    strictLimiter,
    apiLimiter
};
```

### 4.3 Rate-Limiter einbinden

In **`src/app.js`**:

```javascript
const { generalLimiter, apiLimiter } = require('./middleware/rateLimiter');

// Genereller Limiter für alle Routen
app.use(generalLimiter);

// API-spezifischer Limiter
app.use('/api', apiLimiter);
```

---

## Teil 5: Request-Validierung mit Joi (15 Min)

### 5.1 Joi installieren

```bash
npm install joi
```

### 5.2 Validation-Schemas erstellen

Erstelle **`src/validators/projectSchema.js`**:

```javascript
// src/validators/projectSchema.js - Joi-Schemas

const Joi = require('joi');

const projectSchema = Joi.object({
    title: Joi.string()
        .min(3)
        .max(100)
        .required()
        .messages({
            'string.min': 'Titel muss mindestens 3 Zeichen haben',
            'string.max': 'Titel darf maximal 100 Zeichen haben',
            'any.required': 'Titel ist erforderlich'
        }),
    
    description: Joi.string()
        .max(500)
        .optional()
        .messages({
            'string.max': 'Beschreibung darf maximal 500 Zeichen haben'
        }),
    
    technologies: Joi.array()
        .items(Joi.string())
        .optional()
        .messages({
            'array.base': 'Technologies muss ein Array sein'
        }),
    
    status: Joi.string()
        .valid('planned', 'in-progress', 'completed', 'paused')
        .optional()
        .messages({
            'any.only': 'Status muss planned, in-progress, completed oder paused sein'
        }),
    
    githubUrl: Joi.string()
        .uri()
        .optional()
        .allow(null, '')
        .messages({
            'string.uri': 'GitHub-URL muss eine gültige URL sein'
        })
});

module.exports = projectSchema;
```

### 5.3 Validation-Middleware

Aktualisiere **`src/middleware/validators.js`**:

```javascript
// src/middleware/validators.js - Validierungs-Middleware

const projectSchema = require('../validators/projectSchema');
const { ApiError } = require('./errorHandler');

function validateProject(req, res, next) {
    const { error, value } = projectSchema.validate(req.body, {
        abortEarly: false, // Alle Fehler sammeln
        stripUnknown: true // Unbekannte Felder entfernen
    });
    
    if (error) {
        const details = error.details.map(d => d.message);
        return next(new ApiError(`Validierungsfehler: ${details.join(', ')}`, 400));
    }
    
    // Validierte Daten verwenden
    req.body = value;
    next();
}

module.exports = { validateProject };
```

---

## Erfolgskriterien

- [ ] Express Router für Modularisierung genutzt
- [ ] MVC-Ordnerstruktur erstellt
- [ ] Model mit CRUD-Methoden implementiert
- [ ] Controller mit Business-Logik
- [ ] Routes nur für Routing-Definitionen
- [ ] API-Versionierung unter /api/v1
- [ ] Rate-Limiting aktiv
- [ ] Joi-Validierung implementiert
- [ ] Environment-Variablen mit dotenv
- [ ] Alle Komponenten korrekt verbunden

## Tipps

**Dateien importieren:**
```javascript
// Relative Pfade in Node.js
const Project = require('../models/Project');  // Eine Ebene hoch
const validator = require('./validators');      // Gleiche Ebene
```

**Async/Await mit Express:**
Vergiss nicht `try/catch` oder nutze einen Wrapper wie `express-async-handler`.

**Debugging:**
```bash
# Server mit Debug-Output
DEBUG=express:* node server.js
```

## Reflexionsfragen

1. Welche Vorteile hat die MVC-Struktur gegenüber einer einzelnen Datei?
2. Warum sollten Routen und Controller getrennt sein?
3. Wie würdest du eine zweite API-Version (v2) hinzufügen?
4. Wann ist Joi besser als manuelle Validierung?
5. Wie könntest du das Model später auf eine echte Datenbank umstellen?

## Weiterführende Links

- [Express Router](https://expressjs.com/en/guide/routing.html#express-router) - Offizielle Dokumentation
- [Joi Validation](https://joi.dev/) - Schema-Validierung
- [express-rate-limit](https://www.npmjs.com/package/express-rate-limit) - Rate Limiting
- [Node.js Project Structure](https://dev.to/santypk4/bulletproof-node-js-project-architecture-4epf) - Best Practices
- [REST API Versioning](https://restfulapi.net/versioning/) - Versionierungs-Strategien

---

**Geschätzte Zeit:** 60-90 Minuten  
**Nächster Schritt:** RESTful APIs mit Express bauen!
