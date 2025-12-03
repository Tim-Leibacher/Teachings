# Auftrag 1: HTTP-Methoden und Route-Parameter für dein Portfolio

## Ziel

Du erstellst eine vollständige API für dein Portfolio mit allen HTTP-Methoden (GET, POST, PUT, DELETE). Du lernst, wie Route-Parameter und Query-Strings funktionieren und wann du welche verwendest.

## Beschreibung

Bisher hast du nur GET-Routen verwendet, um Daten abzurufen. In der Praxis brauchen APIs aber alle HTTP-Methoden: GET zum Lesen, POST zum Erstellen, PUT zum Aktualisieren und DELETE zum Löschen. Diese vier Operationen nennt man CRUD (Create, Read, Update, Delete). In diesem Auftrag baust du eine API für die Projekte in deinem Portfolio.

**Geschätzte Zeit:** 45-60 Minuten

---

## Teil 1: Projekt vorbereiten (5 Min)

### 1.1 Ordner erstellen und initialisieren

Falls du nicht im bestehenden Portfolio-Projekt arbeitest:

```bash
mkdir portfolio-api
cd portfolio-api
npm init -y
npm install express
```

### 1.2 Basis-Server erstellen

Erstelle die Datei **`server.js`**:

```javascript
// server.js - Portfolio-API mit allen HTTP-Methoden

const express = require('express');
const app = express();
const PORT = 3000;

// Middleware für JSON-Body (wichtig für POST/PUT!)
app.use(express.json());

// Test-Route
app.get('/', (req, res) => {
    res.json({ message: 'Portfolio-API läuft!' });
});

app.listen(PORT, () => {
    console.log(`Server läuft auf http://localhost:${PORT}`);
});
```

Starte den Server und teste:

```bash
node server.js
```

Öffne http://localhost:3000 im Browser.

---

## Teil 2: Projekt-Daten und GET-Routen (15 Min)

### 2.1 Datenstruktur definieren

Füge nach der Test-Route deine Projekt-Daten hinzu:

```javascript
// === Daten (später aus Datenbank) ===

let projects = [
    {
        id: 1,
        title: 'Portfolio-Website',
        description: 'Persönliche Portfolio-Seite mit HTML, CSS und JavaScript',
        technologies: ['HTML', 'CSS', 'JavaScript', 'Node.js', 'Express'],
        status: 'in-progress',
        startDate: '2025-01',
        githubUrl: 'https://github.com/dein-username/portfolio'
    },
    {
        id: 2,
        title: 'HTTP-Server',
        description: 'Server mit dem Node.js http-Modul',
        technologies: ['Node.js'],
        status: 'completed',
        startDate: '2024-12',
        githubUrl: null
    },
    {
        id: 3,
        title: 'Express-Server',
        description: 'Umstellung auf Express.js Framework',
        technologies: ['Node.js', 'Express'],
        status: 'completed',
        startDate: '2025-01',
        githubUrl: null
    }
];

// ID-Counter für neue Projekte
let nextId = 4;
```

**Wichtig:** Passe die Daten an deine eigenen Projekte an!

### 2.2 GET-Route für alle Projekte

```javascript
// === API-Routen ===

// GET /api/projects - Alle Projekte abrufen
app.get('/api/projects', (req, res) => {
    res.json({
        count: projects.length,
        data: projects
    });
});
```

Teste im Browser: http://localhost:3000/api/projects

### 2.3 GET-Route mit Route-Parameter

```javascript
// GET /api/projects/:id - Einzelnes Projekt abrufen
app.get('/api/projects/:id', (req, res) => {
    // Parameter aus URL extrahieren
    const projectId = parseInt(req.params.id);
    
    // Projekt suchen
    const project = projects.find(p => p.id === projectId);
    
    // Fehlerbehandlung
    if (!project) {
        return res.status(404).json({
            error: 'Projekt nicht gefunden',
            requestedId: projectId
        });
    }
    
    res.json(project);
});
```

Teste im Browser:
- http://localhost:3000/api/projects/1 (existiert)
- http://localhost:3000/api/projects/99 (existiert nicht)

---

## Teil 3: POST-Route zum Erstellen (10 Min)

### 3.1 Neue Projekte erstellen

```javascript
// POST /api/projects - Neues Projekt erstellen
app.post('/api/projects', (req, res) => {
    // Daten aus Request-Body
    const { title, description, technologies, status, startDate, githubUrl } = req.body;
    
    // Validierung
    if (!title) {
        return res.status(400).json({
            error: 'Validierungsfehler',
            message: 'Titel ist erforderlich'
        });
    }
    
    // Neues Projekt erstellen
    const newProject = {
        id: nextId++,
        title,
        description: description || '',
        technologies: technologies || [],
        status: status || 'planned',
        startDate: startDate || new Date().toISOString().slice(0, 7),
        githubUrl: githubUrl || null
    };
    
    // Zum Array hinzufügen
    projects.push(newProject);
    
    // 201 Created mit dem neuen Projekt zurückgeben
    res.status(201).json({
        message: 'Projekt erstellt',
        data: newProject
    });
});
```

### 3.2 POST-Request testen

Du kannst POST nicht im Browser testen. Nutze eines dieser Tools:

**Option A: curl im Terminal**
```bash
curl -X POST http://localhost:3000/api/projects \
  -H "Content-Type: application/json" \
  -d '{"title": "Todo-App", "description": "Meine erste Todo-Anwendung", "technologies": ["JavaScript", "HTML", "CSS"]}'
```

**Option B: VS Code Extension "REST Client"**

Erstelle eine Datei **`test.http`**:

```http
### Alle Projekte abrufen
GET http://localhost:3000/api/projects

### Einzelnes Projekt abrufen
GET http://localhost:3000/api/projects/1

### Neues Projekt erstellen
POST http://localhost:3000/api/projects
Content-Type: application/json

{
    "title": "Todo-App",
    "description": "Meine erste Todo-Anwendung",
    "technologies": ["JavaScript", "HTML", "CSS"],
    "status": "planned"
}
```

Klicke auf "Send Request" über jedem Block.

---

## Teil 4: PUT und DELETE implementieren (10 Min)

### 4.1 PUT-Route zum Aktualisieren

```javascript
// PUT /api/projects/:id - Projekt vollständig aktualisieren
app.put('/api/projects/:id', (req, res) => {
    const projectId = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === projectId);
    
    // Projekt nicht gefunden
    if (index === -1) {
        return res.status(404).json({
            error: 'Projekt nicht gefunden',
            requestedId: projectId
        });
    }
    
    // Validierung
    if (!req.body.title) {
        return res.status(400).json({
            error: 'Validierungsfehler',
            message: 'Titel ist erforderlich'
        });
    }
    
    // Projekt aktualisieren (ID bleibt erhalten)
    projects[index] = {
        id: projectId,
        title: req.body.title,
        description: req.body.description || '',
        technologies: req.body.technologies || [],
        status: req.body.status || 'planned',
        startDate: req.body.startDate || projects[index].startDate,
        githubUrl: req.body.githubUrl || null
    };
    
    res.json({
        message: 'Projekt aktualisiert',
        data: projects[index]
    });
});
```

### 4.2 DELETE-Route zum Löschen

```javascript
// DELETE /api/projects/:id - Projekt löschen
app.delete('/api/projects/:id', (req, res) => {
    const projectId = parseInt(req.params.id);
    const index = projects.findIndex(p => p.id === projectId);
    
    // Projekt nicht gefunden
    if (index === -1) {
        return res.status(404).json({
            error: 'Projekt nicht gefunden',
            requestedId: projectId
        });
    }
    
    // Projekt entfernen
    const deletedProject = projects.splice(index, 1)[0];
    
    // 200 OK mit Bestätigung (oder 204 No Content)
    res.json({
        message: 'Projekt gelöscht',
        data: deletedProject
    });
});
```

### 4.3 Testen (in test.http ergänzen)

```http
### Projekt aktualisieren
PUT http://localhost:3000/api/projects/1
Content-Type: application/json

{
    "title": "Portfolio-Website v2",
    "description": "Erweiterte Portfolio-Seite mit Express-Backend",
    "technologies": ["HTML", "CSS", "JavaScript", "Node.js", "Express"],
    "status": "in-progress"
}

### Projekt löschen
DELETE http://localhost:3000/api/projects/2
```

---

## Teil 5: Query-Strings für Filterung (10 Min)

### 5.1 GET-Route mit Filterung erweitern

Ersetze die GET /api/projects Route:

```javascript
// GET /api/projects - Alle Projekte mit optionaler Filterung
app.get('/api/projects', (req, res) => {
    let result = [...projects]; // Kopie erstellen
    
    // Nach Status filtern
    if (req.query.status) {
        result = result.filter(p => p.status === req.query.status);
    }
    
    // Nach Technologie filtern
    if (req.query.tech) {
        const tech = req.query.tech.toLowerCase();
        result = result.filter(p => 
            p.technologies.some(t => t.toLowerCase().includes(tech))
        );
    }
    
    // Sortieren
    if (req.query.sort) {
        const sortField = req.query.sort;
        const order = req.query.order === 'desc' ? -1 : 1;
        
        result.sort((a, b) => {
            if (a[sortField] < b[sortField]) return -1 * order;
            if (a[sortField] > b[sortField]) return 1 * order;
            return 0;
        });
    }
    
    res.json({
        count: result.length,
        filters: {
            status: req.query.status || null,
            tech: req.query.tech || null,
            sort: req.query.sort || null
        },
        data: result
    });
});
```

### 5.2 Filterung testen

Ergänze **`test.http`**:

```http
### Alle Projekte
GET http://localhost:3000/api/projects

### Nach Status filtern
GET http://localhost:3000/api/projects?status=completed

### Nach Technologie filtern
GET http://localhost:3000/api/projects?tech=express

### Sortiert nach Titel
GET http://localhost:3000/api/projects?sort=title

### Kombiniert: Status + Sortierung
GET http://localhost:3000/api/projects?status=in-progress&sort=startDate&order=desc
```

---

## Erfolgskriterien

- [ ] Server startet ohne Fehler
- [ ] GET /api/projects liefert alle Projekte
- [ ] GET /api/projects/:id liefert einzelnes Projekt
- [ ] GET /api/projects/:id gibt 404 bei ungültiger ID
- [ ] POST /api/projects erstellt neues Projekt
- [ ] POST /api/projects validiert Eingaben
- [ ] PUT /api/projects/:id aktualisiert Projekt
- [ ] DELETE /api/projects/:id löscht Projekt
- [ ] Query-Parameter filtern Ergebnisse
- [ ] Eigene Projekt-Daten verwendet

## Tipps

**Status-Codes richtig verwenden:**
- 200 OK: Erfolgreiche GET, PUT, DELETE
- 201 Created: Erfolgreiche POST
- 400 Bad Request: Ungültige Eingaben
- 404 Not Found: Ressource nicht gefunden

**parseInt nicht vergessen:**
```javascript
// req.params.id ist immer ein String!
const id = parseInt(req.params.id);
```

**REST Client Extension:**
Die VS Code Extension "REST Client" ist extrem praktisch für API-Tests. Installiere sie über den Extension Marketplace.

**Daten bleiben nicht gespeichert:**
Bei Server-Neustart sind alle Änderungen weg, weil wir noch keine Datenbank haben. Das ist für jetzt okay.

## Reflexionsfragen

1. Was ist der Unterschied zwischen req.params und req.query?
2. Warum brauchst du express.json() für POST-Requests?
3. Wann verwendest du Status 201 statt 200?
4. Was bedeutet CRUD und welche HTTP-Methoden gehören dazu?
5. Warum sollte die ID beim PUT nicht aus dem Body kommen?

## Weiterführende Links

- [Express Routing](https://expressjs.com/en/guide/routing.html) - Offizielle Dokumentation
- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) - MDN Referenz
- [REST API Design Best Practices](https://restfulapi.net/) - REST-Konzepte
- [REST Client VS Code](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) - Extension für API-Tests

---

**Geschätzte Zeit:** 45-60 Minuten  
**Nächster Schritt:** In Auftrag 2 lernst du, eigene Middleware zu schreiben!
