# Auftrag 2: Routing und JSON-API erstellen

## Ziel

Du erstellst einen Server mit mehreren Seiten (Routing) und baust eine einfache JSON-API, die Daten im JSON-Format ausliefert. Du lernst, wie professionelle Server auf verschiedene URLs unterschiedlich reagieren.

## Beschreibung

Professionelle Webserver haben nicht nur eine Seite, sondern viele verschiedene URLs mit unterschiedlichen Inhalten. Routing bedeutet: Je nach angeforderter URL (`/`, `/about`, `/skills`) liefert der Server andere Inhalte aus. Zusätzlich lernst du, JSON-Daten auszuliefern – das ist die Basis für APIs.

**Geschätzte Zeit:** 60-75 Minuten

---

## Teil 1: Server mit mehreren Seiten (Routing) (30 Min)

### 1.1 Projekt vorbereiten

Falls noch nicht geschehen:

```bash
mkdir portfolio-server
cd portfolio-server
code .
```

### 1.2 Routing-Server erstellen

Erstelle eine neue Datei **`server-routing.js`**:

```javascript
// server-routing.js - Server mit mehreren Seiten

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // Immer HTML ausliefern
    response.setHeader('Content-Type', 'text/html; charset=utf-8');
    
    // Routing: Verschiedene URLs behandeln
    if (request.url === '/' || request.url === '/home') {
        // STARTSEITE
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Portfolio - Home</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    nav {
                        background: #376B8C;
                        padding: 15px;
                        border-radius: 4px;
                        margin-bottom: 20px;
                    }
                    nav a {
                        color: white;
                        text-decoration: none;
                        margin-right: 20px;
                        font-weight: bold;
                    }
                    nav a:hover {
                        text-decoration: underline;
                    }
                    .content {
                        background: white;
                        padding: 20px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 { color: #376B8C; }
                </style>
            </head>
            <body>
                <nav>
                    <a href="/">Home</a>
                    <a href="/about">Über mich</a>
                    <a href="/skills">Skills</a>
                    <a href="/projects">Projekte</a>
                    <a href="/contact">Kontakt</a>
                </nav>
                
                <div class="content">
                    <h1>Willkommen auf meinem Portfolio!</h1>
                    <p>Mein Name ist [Dein Name] und ich bin Lernende/r im 1. Lehrjahr Applikationsentwicklung.</p>
                    <p>Dieser Server läuft mit Node.js und dem http-Modul.</p>
                    <p>Navigiere über das Menü oben zu den verschiedenen Seiten.</p>
                </div>
            </body>
            </html>
        `);
        
    } else if (request.url === '/about') {
        // ÜBER MICH
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Portfolio - Über mich</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    nav {
                        background: #376B8C;
                        padding: 15px;
                        border-radius: 4px;
                        margin-bottom: 20px;
                    }
                    nav a {
                        color: white;
                        text-decoration: none;
                        margin-right: 20px;
                        font-weight: bold;
                    }
                    nav a:hover {
                        text-decoration: underline;
                    }
                    .content {
                        background: white;
                        padding: 20px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 { color: #376B8C; }
                    .info { margin: 10px 0; }
                </style>
            </head>
            <body>
                <nav>
                    <a href="/">Home</a>
                    <a href="/about">Über mich</a>
                    <a href="/skills">Skills</a>
                    <a href="/projects">Projekte</a>
                    <a href="/contact">Kontakt</a>
                </nav>
                
                <div class="content">
                    <h1>Über mich</h1>
                    <div class="info">
                        <strong>Name:</strong> [Dein Name]
                    </div>
                    <div class="info">
                        <strong>Beruf:</strong> Lernende/r Informatiker/in EFZ Applikationsentwicklung
                    </div>
                    <div class="info">
                        <strong>Lehrjahr:</strong> 1. Lehrjahr
                    </div>
                    <div class="info">
                        <strong>Ausbildungsbetrieb:</strong> [Dein Betrieb]
                    </div>
                    <p style="margin-top: 20px;">
                        Ich lerne gerade die Grundlagen der Webentwicklung mit HTML, CSS, JavaScript und Node.js. 
                        Mein Ziel ist es, moderne Webanwendungen zu entwickeln.
                    </p>
                </div>
            </body>
            </html>
        `);
        
    } else if (request.url === '/skills') {
        // SKILLS-SEITE
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Portfolio - Skills</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    nav {
                        background: #376B8C;
                        padding: 15px;
                        border-radius: 4px;
                        margin-bottom: 20px;
                    }
                    nav a {
                        color: white;
                        text-decoration: none;
                        margin-right: 20px;
                        font-weight: bold;
                    }
                    .content {
                        background: white;
                        padding: 20px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 { color: #376B8C; }
                    .skill {
                        margin: 20px 0;
                    }
                    .skill-name {
                        font-weight: bold;
                        margin-bottom: 5px;
                    }
                    .progress-bar {
                        background: #e0e0e0;
                        height: 20px;
                        border-radius: 10px;
                        overflow: hidden;
                    }
                    .progress-fill {
                        background: #29786A;
                        height: 100%;
                        transition: width 0.3s;
                    }
                </style>
            </head>
            <body>
                <nav>
                    <a href="/">Home</a>
                    <a href="/about">Über mich</a>
                    <a href="/skills">Skills</a>
                    <a href="/projects">Projekte</a>
                    <a href="/contact">Kontakt</a>
                </nav>
                
                <div class="content">
                    <h1>Meine Skills</h1>
                    
                    <div class="skill">
                        <div class="skill-name">HTML - 80%</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 80%;"></div>
                        </div>
                    </div>
                    
                    <div class="skill">
                        <div class="skill-name">CSS - 75%</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 75%;"></div>
                        </div>
                    </div>
                    
                    <div class="skill">
                        <div class="skill-name">JavaScript - 60%</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 60%;"></div>
                        </div>
                    </div>
                    
                    <div class="skill">
                        <div class="skill-name">Node.js - 40%</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 40%;"></div>
                        </div>
                    </div>
                    
                    <div class="skill">
                        <div class="skill-name">Git - 50%</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 50%;"></div>
                        </div>
                    </div>
                </div>
            </body>
            </html>
        `);
        
    } else if (request.url === '/projects') {
        // PROJEKTE-SEITE
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Portfolio - Projekte</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    nav {
                        background: #376B8C;
                        padding: 15px;
                        border-radius: 4px;
                        margin-bottom: 20px;
                    }
                    nav a {
                        color: white;
                        text-decoration: none;
                        margin-right: 20px;
                        font-weight: bold;
                    }
                    .content {
                        background: white;
                        padding: 20px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 { color: #376B8C; }
                    .project {
                        border-left: 4px solid #29786A;
                        padding-left: 15px;
                        margin: 20px 0;
                    }
                    .project h3 {
                        color: #376B8C;
                        margin: 0 0 10px 0;
                    }
                    .project-meta {
                        color: #666;
                        font-size: 0.9em;
                        margin-bottom: 10px;
                    }
                </style>
            </head>
            <body>
                <nav>
                    <a href="/">Home</a>
                    <a href="/about">Über mich</a>
                    <a href="/skills">Skills</a>
                    <a href="/projects">Projekte</a>
                    <a href="/contact">Kontakt</a>
                </nav>
                
                <div class="content">
                    <h1>Meine Projekte</h1>
                    
                    <div class="project">
                        <h3>Portfolio-Website</h3>
                        <div class="project-meta">HTML, CSS, JavaScript | Status: In Arbeit</div>
                        <p>Meine persönliche Portfolio-Website mit HTML, CSS und JavaScript. 
                           Zeigt meine Skills und Projekte.</p>
                    </div>
                    
                    <div class="project">
                        <h3>HTTP-Server mit Node.js</h3>
                        <div class="project-meta">Node.js, HTTP-Modul | Status: In Arbeit</div>
                        <p>Ein selbstgebauter Webserver mit Node.js, der verschiedene Seiten ausliefert 
                           und Routing unterstützt.</p>
                    </div>
                    
                    <div class="project">
                        <h3>Todo-App</h3>
                        <div class="project-meta">HTML, CSS, JavaScript | Status: Geplant</div>
                        <p>Eine Todo-App mit lokalem Speicher und interaktiver Benutzeroberfläche.</p>
                    </div>
                </div>
            </body>
            </html>
        `);
        
    } else if (request.url === '/contact') {
        // KONTAKT-SEITE
        response.statusCode = 200;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>Portfolio - Kontakt</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    nav {
                        background: #376B8C;
                        padding: 15px;
                        border-radius: 4px;
                        margin-bottom: 20px;
                    }
                    nav a {
                        color: white;
                        text-decoration: none;
                        margin-right: 20px;
                        font-weight: bold;
                    }
                    .content {
                        background: white;
                        padding: 20px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 { color: #376B8C; }
                    .contact-item {
                        display: flex;
                        align-items: center;
                        margin: 15px 0;
                        padding: 10px;
                        background: #f5f5f5;
                        border-radius: 4px;
                    }
                    .contact-label {
                        font-weight: bold;
                        width: 100px;
                    }
                </style>
            </head>
            <body>
                <nav>
                    <a href="/">Home</a>
                    <a href="/about">Über mich</a>
                    <a href="/skills">Skills</a>
                    <a href="/projects">Projekte</a>
                    <a href="/contact">Kontakt</a>
                </nav>
                
                <div class="content">
                    <h1>Kontakt</h1>
                    <p>Du erreichst mich über folgende Kanäle:</p>
                    
                    <div class="contact-item">
                        <div class="contact-label">Email:</div>
                        <div>dein-name@example.com</div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="contact-label">GitHub:</div>
                        <div>github.com/dein-username</div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="contact-label">LinkedIn:</div>
                        <div>linkedin.com/in/dein-profil</div>
                    </div>
                </div>
            </body>
            </html>
        `);
        
    } else {
        // 404 - SEITE NICHT GEFUNDEN
        response.statusCode = 404;
        response.end(`
            <!DOCTYPE html>
            <html lang="de">
            <head>
                <meta charset="UTF-8">
                <title>404 - Nicht gefunden</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 50px auto;
                        padding: 20px;
                        text-align: center;
                        background-color: #f5f5f5;
                    }
                    .error-box {
                        background: white;
                        padding: 40px;
                        border-radius: 8px;
                        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                    }
                    h1 {
                        color: #E87722;
                        font-size: 72px;
                        margin: 0;
                    }
                    h2 {
                        color: #376B8C;
                    }
                    a {
                        display: inline-block;
                        margin-top: 20px;
                        padding: 10px 20px;
                        background: #376B8C;
                        color: white;
                        text-decoration: none;
                        border-radius: 4px;
                    }
                    a:hover {
                        background: #29786A;
                    }
                </style>
            </head>
            <body>
                <div class="error-box">
                    <h1>404</h1>
                    <h2>Seite nicht gefunden</h2>
                    <p>Die Seite "${request.url}" existiert nicht.</p>
                    <a href="/">Zurück zur Startseite</a>
                </div>
            </body>
            </html>
        `);
    }
});

const PORT = 3000;

server.listen(PORT, () => {
    console.log(`✅ Server mit Routing läuft auf http://localhost:${PORT}`);
    console.log('Verfügbare Seiten:');
    console.log('  - http://localhost:3000/');
    console.log('  - http://localhost:3000/about');
    console.log('  - http://localhost:3000/skills');
    console.log('  - http://localhost:3000/projects');
    console.log('  - http://localhost:3000/contact');
});
```

### 1.3 Server testen

```bash
node server-routing.js
```

Teste im Browser:
- `http://localhost:3000/` → Startseite
- `http://localhost:3000/about` → Über mich
- `http://localhost:3000/skills` → Skills mit Fortschrittsbalken
- `http://localhost:3000/projects` → Projekte
- `http://localhost:3000/contact` → Kontakt
- `http://localhost:3000/irgendwas` → 404-Fehler

**Navigation funktioniert!** Klicke auf die Links im Menü.

---

## Teil 2: JSON-API erstellen (30 Min)

### 2.1 API-Server erstellen

Erstelle eine neue Datei **`server-api.js`**:

```javascript
// server-api.js - JSON-API

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // JSON ausliefern
    response.setHeader('Content-Type', 'application/json; charset=utf-8');
    
    if (request.url === '/' || request.url === '/api') {
        // API-ÜBERSICHT
        response.statusCode = 200;
        
        const apiInfo = {
            message: 'Willkommen zur Portfolio-API',
            version: '1.0.0',
            endpoints: [
                {
                    url: '/api/info',
                    method: 'GET',
                    description: 'Persönliche Informationen'
                },
                {
                    url: '/api/skills',
                    method: 'GET',
                    description: 'Liste aller Skills mit Level'
                },
                {
                    url: '/api/projects',
                    method: 'GET',
                    description: 'Liste aller Projekte'
                },
                {
                    url: '/api/stats',
                    method: 'GET',
                    description: 'Statistiken über Skills und Projekte'
                }
            ],
            timestamp: new Date().toISOString()
        };
        
        // JSON mit 2 Spaces Einrückung für bessere Lesbarkeit
        response.end(JSON.stringify(apiInfo, null, 2));
        
    } else if (request.url === '/api/info') {
        // PERSÖNLICHE INFORMATIONEN
        response.statusCode = 200;
        
        const info = {
            status: 'success',
            data: {
                name: 'Dein Name',
                beruf: 'Lernende/r Informatiker/in EFZ Applikationsentwicklung',
                lehrjahr: 1,
                ausbildungsbetrieb: 'Dein Betrieb',
                standort: 'Deine Stadt',
                interessen: ['Programmieren', 'Webentwicklung', 'Gaming', 'Sport'],
                kontakt: {
                    email: 'dein-name@example.com',
                    github: 'github.com/dein-username',
                    linkedin: 'linkedin.com/in/dein-profil'
                }
            },
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(info, null, 2));
        
    } else if (request.url === '/api/skills') {
        // SKILLS-LISTE
        response.statusCode = 200;
        
        const skills = {
            status: 'success',
            data: [
                {
                    id: 1,
                    name: 'HTML',
                    level: 4,
                    maxLevel: 5,
                    kategorie: 'Frontend',
                    beschreibung: 'Struktur von Webseiten'
                },
                {
                    id: 2,
                    name: 'CSS',
                    level: 4,
                    maxLevel: 5,
                    kategorie: 'Frontend',
                    beschreibung: 'Styling und Layout'
                },
                {
                    id: 3,
                    name: 'JavaScript',
                    level: 3,
                    maxLevel: 5,
                    kategorie: 'Frontend',
                    beschreibung: 'Interaktivität und Logik'
                },
                {
                    id: 4,
                    name: 'Node.js',
                    level: 2,
                    maxLevel: 5,
                    kategorie: 'Backend',
                    beschreibung: 'Server-Entwicklung'
                },
                {
                    id: 5,
                    name: 'Git',
                    level: 3,
                    maxLevel: 5,
                    kategorie: 'Tools',
                    beschreibung: 'Versionsverwaltung'
                }
            ],
            count: 5,
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(skills, null, 2));
        
    } else if (request.url === '/api/projects') {
        // PROJEKTE-LISTE
        response.statusCode = 200;
        
        const projects = {
            status: 'success',
            data: [
                {
                    id: 1,
                    titel: 'Portfolio-Website',
                    technologien: ['HTML', 'CSS', 'JavaScript'],
                    status: 'In Arbeit',
                    startdatum: '2025-09',
                    beschreibung: 'Persönliche Portfolio-Website mit allen Projekten und Skills',
                    github: 'github.com/username/portfolio'
                },
                {
                    id: 2,
                    titel: 'HTTP-Server mit Node.js',
                    technologien: ['Node.js', 'HTTP-Modul'],
                    status: 'In Arbeit',
                    startdatum: '2025-11',
                    beschreibung: 'Selbstgebauter Webserver mit Routing und JSON-API',
                    github: 'github.com/username/node-server'
                },
                {
                    id: 3,
                    titel: 'Todo-App',
                    technologien: ['HTML', 'CSS', 'JavaScript'],
                    status: 'Geplant',
                    startdatum: '2025-12',
                    beschreibung: 'Interaktive Todo-App mit localStorage',
                    github: null
                }
            ],
            count: 3,
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(projects, null, 2));
        
    } else if (request.url === '/api/stats') {
        // STATISTIKEN
        response.statusCode = 200;
        
        const stats = {
            status: 'success',
            data: {
                skills: {
                    total: 5,
                    frontend: 3,
                    backend: 1,
                    tools: 1,
                    durchschnittLevel: 3.2
                },
                projekte: {
                    total: 3,
                    inArbeit: 2,
                    abgeschlossen: 0,
                    geplant: 1
                },
                server: {
                    nodeVersion: process.version,
                    platform: process.platform,
                    uptime: Math.round(process.uptime()),
                    memory: {
                        used: Math.round(process.memoryUsage().heapUsed / 1024 / 1024),
                        unit: 'MB'
                    }
                }
            },
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(stats, null, 2));
        
    } else {
        // 404 - ENDPOINT NICHT GEFUNDEN
        response.statusCode = 404;
        
        const error = {
            status: 'error',
            message: 'Endpoint nicht gefunden',
            requestedUrl: request.url,
            availableEndpoints: ['/api', '/api/info', '/api/skills', '/api/projects', '/api/stats'],
            timestamp: new Date().toISOString()
        };
        
        response.end(JSON.stringify(error, null, 2));
    }
});

const PORT = 3001;  // Anderer Port, damit beide Server parallel laufen können

server.listen(PORT, () => {
    console.log(`✅ JSON-API läuft auf http://localhost:${PORT}`);
    console.log('\nVerfügbare Endpoints:');
    console.log(`  - http://localhost:${PORT}/api`);
    console.log(`  - http://localhost:${PORT}/api/info`);
    console.log(`  - http://localhost:${PORT}/api/skills`);
    console.log(`  - http://localhost:${PORT}/api/projects`);
    console.log(`  - http://localhost:${PORT}/api/stats`);
});
```

### 2.2 API testen

```bash
node server-api.js
```

Teste im Browser:
- `http://localhost:3001/api` → API-Übersicht
- `http://localhost:3001/api/info` → Persönliche Infos
- `http://localhost:3001/api/skills` → Skills als JSON
- `http://localhost:3001/api/projects` → Projekte als JSON
- `http://localhost:3001/api/stats` → Statistiken
- `http://localhost:3001/irgendwas` → 404-JSON-Fehler

**Tipp:** Installiere die Browser-Extension "JSON Formatter" für schönere JSON-Darstellung!

### 2.3 API mit fetch() nutzen (Optional)

Erstelle **`test-api.html`**:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API Tester</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1000px;
            margin: 50px auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        button {
            background: #376B8C;
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 5px;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background: #29786A;
        }
        #result {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
            white-space: pre-wrap;
            font-family: monospace;
        }
    </style>
</head>
<body>
    <h1>API Tester</h1>
    <p>Klicke auf die Buttons, um die API zu testen:</p>
    
    <button onclick="fetchData('/api')">API-Übersicht</button>
    <button onclick="fetchData('/api/info')">Persönliche Info</button>
    <button onclick="fetchData('/api/skills')">Skills</button>
    <button onclick="fetchData('/api/projects')">Projekte</button>
    <button onclick="fetchData('/api/stats')">Statistiken</button>
    
    <div id="result">Klicke auf einen Button...</div>
    
    <script>
        async function fetchData(endpoint) {
            const resultDiv = document.getElementById('result');
            resultDiv.textContent = 'Lädt...';
            
            try {
                const response = await fetch(`http://localhost:3001${endpoint}`);
                const data = await response.json();
                resultDiv.textContent = JSON.stringify(data, null, 2);
            } catch (error) {
                resultDiv.textContent = `Fehler: ${error.message}`;
            }
        }
    </script>
</body>
</html>
```

Öffne `test-api.html` im Browser (mit Live Server oder `file://`-Protokoll).

---

## Erfolgskriterien

- [ ] `server-routing.js` erstellt mit 5 verschiedenen Seiten
- [ ] Navigation zwischen Seiten funktioniert
- [ ] 404-Seite wird für ungültige URLs angezeigt
- [ ] Verschiedene if/else-Bedingungen für Routing
- [ ] Alle Seiten haben konsistentes Styling
- [ ] `server-api.js` erstellt mit JSON-Ausgabe
- [ ] Mindestens 4 API-Endpoints funktionieren
- [ ] JSON-Daten sind korrekt formatiert
- [ ] Content-Type `application/json` wird gesetzt
- [ ] 404-Fehler werden als JSON zurückgegeben
- [ ] Optional: API mit fetch() aus HTML aufgerufen

## Tipps

**Content-Type wichtig:**
- HTML: `text/html; charset=utf-8`
- JSON: `application/json; charset=utf-8`
- Falsch gesetzt → Browser zeigt falsch an

**JSON.stringify() Parameter:**
- `JSON.stringify(data)` → kompakt
- `JSON.stringify(data, null, 2)` → formatiert mit 2 Spaces

**Routing-Logik:**
- Mit if/else für wenige Routen
- Später: Switch-Case oder Routing-Bibliothek

**Debugging:**
- `console.log(request.url)` zeigt angeforderte URL
- Browser Developer Tools → Network-Tab zeigt Requests

**Beide Server parallel:**
- Routing-Server: Port 3000
- API-Server: Port 3001
- So kannst du beide gleichzeitig testen

## Reflexionsfragen

1. Was ist der Unterschied zwischen einer HTML-Seite und einer JSON-API?
2. Warum brauchen wir verschiedene Content-Types?
3. Teste: Was passiert, wenn du `Content-Type: application/json` setzt, aber HTML auslieferst?
4. Schaue dir `JSON.stringify()` in der MDN-Dokumentation an. Was machen die Parameter?
5. Wie könntest du Routing eleganter lösen als mit vielen if/else?

## Weiterführende Links

- [MDN: HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) – Alle Statuscodes
- [JSON.org](https://www.json.org/json-de.html) – JSON-Spezifikation
- [REST API Best Practices](https://restfulapi.net/) – API-Design-Prinzipien
- [Express.js](https://expressjs.com/) – Framework für eleganteres Routing
- [Postman](https://www.postman.com/) – Tool zum Testen von APIs

---

**⏱️ Geschätzte Zeit:** 60-75 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 lernst du, statische Dateien auszuliefern!
