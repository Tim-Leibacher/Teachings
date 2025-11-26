# Optionaler Auftrag: Portfolio-Server mit erweiterten Features

## Ziel

Du erweiterst deinen HTTP-Server mit professionellen Features: Request-Logging in Datei, automatische Restart-Funktion, Environment-Variablen, Performance-Monitoring und erweiterte API-Endpoints. Dies ist eine Vertiefung für motivierte Lernende.

## Beschreibung

Dieser Auftrag geht über die Basics hinaus und zeigt dir, wie professionelle Node.js-Server aufgebaut sind. Du implementierst Features, die in echten Produktionsumgebungen genutzt werden. Dies ist eine gute Vorbereitung für das Express.js-Modul.

**Geschätzte Zeit:** 120-150 Minuten  
**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzung:** Aufträge 1-3 abgeschlossen

---

## Teil 1: Request-Logging in Datei (30 Min)

### 1.1 Log-System erstellen

Erstelle eine Datei **`logger.js`**:

```javascript
// logger.js - Professionelles Logging-System

const fs = require('fs');
const path = require('path');

// Log-Ordner erstellen falls nicht vorhanden
const LOG_DIR = path.join(__dirname, 'logs');
if (!fs.existsSync(LOG_DIR)) {
    fs.mkdirSync(LOG_DIR);
}

// Log-Level definieren
const LOG_LEVELS = {
    DEBUG: 0,
    INFO: 1,
    WARN: 2,
    ERROR: 3
};

// Farben für Terminal-Ausgabe
const COLORS = {
    DEBUG: '\x1b[90m',   // Grau
    INFO: '\x1b[36m',    // Cyan
    WARN: '\x1b[33m',    // Gelb
    ERROR: '\x1b[31m',   // Rot
    RESET: '\x1b[0m'     // Reset
};

class Logger {
    constructor(minLevel = 'INFO') {
        this.minLevel = LOG_LEVELS[minLevel] || LOG_LEVELS.INFO;
        this.logFile = path.join(LOG_DIR, `app-${this.getDateString()}.log`);
        this.accessLogFile = path.join(LOG_DIR, `access-${this.getDateString()}.log`);
    }
    
    getDateString() {
        const now = new Date();
        return `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}-${String(now.getDate()).padStart(2, '0')}`;
    }
    
    getTimestamp() {
        return new Date().toISOString();
    }
    
    formatMessage(level, message) {
        return `[${this.getTimestamp()}] [${level}] ${message}\n`;
    }
    
    log(level, message) {
        if (LOG_LEVELS[level] < this.minLevel) return;
        
        const formattedMessage = this.formatMessage(level, message);
        
        // Terminal-Ausgabe mit Farbe
        const color = COLORS[level] || COLORS.RESET;
        console.log(`${color}${formattedMessage.trim()}${COLORS.RESET}`);
        
        // In Datei schreiben
        fs.appendFileSync(this.logFile, formattedMessage);
    }
    
    debug(message) {
        this.log('DEBUG', message);
    }
    
    info(message) {
        this.log('INFO', message);
    }
    
    warn(message) {
        this.log('WARN', message);
    }
    
    error(message) {
        this.log('ERROR', message);
    }
    
    // Speziell für HTTP-Requests
    logRequest(req, res, duration) {
        const logEntry = `${this.getTimestamp()} ${req.method} ${req.url} ${res.statusCode} ${duration}ms\n`;
        fs.appendFileSync(this.accessLogFile, logEntry);
        
        const statusColor = res.statusCode < 400 ? COLORS.INFO : COLORS.ERROR;
        console.log(`${statusColor}${req.method} ${req.url} → ${res.statusCode} (${duration}ms)${COLORS.RESET}`);
    }
}

module.exports = Logger;
```

### 1.2 Logger in Server integrieren

Erstelle **`server-advanced.js`**:

```javascript
// server-advanced.js - Erweiterter Server mit Logging

const http = require('http');
const fs = require('fs');
const path = require('path');
const Logger = require('./logger');

const logger = new Logger('DEBUG');

logger.info('Server wird gestartet...');

const server = http.createServer((request, response) => {
    const startTime = Date.now();
    
    // Logger: Anfrage empfangen
    logger.debug(`Anfrage empfangen: ${request.method} ${request.url}`);
    
    let filePath = request.url === '/' ? '/index.html' : request.url;
    filePath = path.join(__dirname, 'public', filePath);
    
    const extname = path.extname(filePath).toLowerCase();
    const contentTypes = {
        '.html': 'text/html; charset=utf-8',
        '.css': 'text/css',
        '.js': 'application/javascript',
        '.json': 'application/json',
        '.png': 'image/png',
        '.jpg': 'image/jpeg',
        '.jpeg': 'image/jpeg',
        '.gif': 'image/gif',
        '.svg': 'image/svg+xml'
    };
    
    const contentType = contentTypes[extname] || 'application/octet-stream';
    
    // Sicherheitscheck
    const publicPath = path.join(__dirname, 'public');
    const resolvedPath = path.resolve(filePath);
    
    if (!resolvedPath.startsWith(publicPath)) {
        logger.warn(`Sicherheitsverstoß: Versuch, auf ${request.url} zuzugreifen`);
        response.statusCode = 403;
        response.setHeader('Content-Type', 'text/plain');
        response.end('403 Forbidden');
        return;
    }
    
    fs.readFile(filePath, (error, content) => {
        const duration = Date.now() - startTime;
        
        if (error) {
            if (error.code === 'ENOENT') {
                logger.warn(`404: Datei nicht gefunden - ${request.url}`);
                response.statusCode = 404;
                response.setHeader('Content-Type', 'text/html; charset=utf-8');
                response.end('<h1>404 - Nicht gefunden</h1>');
            } else {
                logger.error(`Server-Fehler: ${error.message}`);
                response.statusCode = 500;
                response.setHeader('Content-Type', 'text/plain');
                response.end('500 Internal Server Error');
            }
        } else {
            response.statusCode = 200;
            response.setHeader('Content-Type', contentType);
            response.end(content);
        }
        
        // Request loggen
        logger.logRequest(request, response, duration);
    });
});

const PORT = process.env.PORT || 3000;

server.listen(PORT, () => {
    logger.info(`Server läuft auf http://localhost:${PORT}`);
    logger.info(`Logs werden gespeichert in: ${path.join(__dirname, 'logs')}`);
});

// Graceful Shutdown
process.on('SIGINT', () => {
    logger.info('Server wird heruntergefahren...');
    server.close(() => {
        logger.info('Server erfolgreich gestoppt');
        process.exit(0);
    });
});
```

### 1.3 Testen

```bash
node server-advanced.js
```

**Im `logs/`-Ordner entstehen:**
- `app-2025-11-26.log` – Alle Logs
- `access-2025-11-26.log` – Nur HTTP-Requests

**Teste verschiedene Requests und schaue in die Log-Dateien!**

---

## Teil 2: Automatischer Restart mit Nodemon (20 Min)

### 2.1 Nodemon installieren

```bash
# Global installieren (einmalig)
npm install -g nodemon

# Oder lokal im Projekt
npm init -y
npm install --save-dev nodemon
```

### 2.2 NPM-Scripts einrichten

Erweitere **`package.json`**:

```json
{
  "name": "portfolio-server",
  "version": "1.0.0",
  "description": "HTTP-Server mit Node.js",
  "main": "server-advanced.js",
  "scripts": {
    "start": "node server-advanced.js",
    "dev": "nodemon server-advanced.js",
    "dev:debug": "nodemon --inspect server-advanced.js",
    "logs": "tail -f logs/app-*.log"
  },
  "author": "Dein Name",
  "license": "MIT",
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

### 2.3 Nodemon-Config erstellen

Erstelle **`nodemon.json`**:

```json
{
  "watch": ["*.js", "public/**/*"],
  "ext": "js,json,html,css",
  "ignore": ["logs/*", "node_modules/*"],
  "delay": 500,
  "env": {
    "NODE_ENV": "development",
    "PORT": "3000"
  }
}
```

### 2.4 Nutzen

```bash
# Entwicklungs-Modus mit Auto-Restart
npm run dev

# Jetzt: Ändere eine Datei → Server startet automatisch neu!
```

---

## Teil 3: Environment-Variablen (15 Min)

### 3.1 dotenv installieren

```bash
npm install dotenv
```

### 3.2 .env-Datei erstellen

Erstelle **`.env`**:

```env
# Server-Konfiguration
PORT=3000
NODE_ENV=development
LOG_LEVEL=DEBUG

# Sicherheit
MAX_FILE_SIZE=10485760
ALLOWED_ORIGINS=http://localhost:3000,http://127.0.0.1:3000

# Features
ENABLE_LOGGING=true
ENABLE_CACHE=true
CACHE_MAX_AGE=3600
```

### 3.3 .gitignore erweitern

Erstelle/erweitere **`.gitignore`**:

```gitignore
# Dependencies
node_modules/

# Logs
logs/
*.log

# Environment
.env
.env.local

# OS
.DS_Store
Thumbs.db
```

### 3.4 In Server integrieren

Am Anfang von **`server-advanced.js`**:

```javascript
// Ganz oben, vor allem anderen
require('dotenv').config();

const http = require('http');
const fs = require('fs');
const path = require('path');
const Logger = require('./logger');

// Environment-Variablen nutzen
const PORT = process.env.PORT || 3000;
const LOG_LEVEL = process.env.LOG_LEVEL || 'INFO';
const NODE_ENV = process.env.NODE_ENV || 'production';
const MAX_FILE_SIZE = parseInt(process.env.MAX_FILE_SIZE) || 10 * 1024 * 1024; // 10 MB

const logger = new Logger(LOG_LEVEL);

logger.info(`Umgebung: ${NODE_ENV}`);
logger.info(`Port: ${PORT}`);
logger.info(`Max. Dateigrösse: ${Math.round(MAX_FILE_SIZE / 1024 / 1024)} MB`);
```

---

## Teil 4: Performance-Monitoring (25 Min)

### 4.1 Performance-Modul erstellen

Erstelle **`performance-monitor.js`**:

```javascript
// performance-monitor.js - Performance-Überwachung

class PerformanceMonitor {
    constructor() {
        this.requests = [];
        this.startTime = Date.now();
    }
    
    recordRequest(duration, statusCode, url) {
        this.requests.push({
            duration,
            statusCode,
            url,
            timestamp: Date.now()
        });
        
        // Nur letzte 1000 Requests behalten
        if (this.requests.length > 1000) {
            this.requests.shift();
        }
    }
    
    getStats() {
        const now = Date.now();
        const uptime = Math.round((now - this.startTime) / 1000);
        
        // Requests der letzten 60 Sekunden
        const recentRequests = this.requests.filter(r => 
            now - r.timestamp < 60000
        );
        
        // Durchschnittliche Response-Zeit
        const avgDuration = recentRequests.length > 0
            ? Math.round(recentRequests.reduce((sum, r) => sum + r.duration, 0) / recentRequests.length)
            : 0;
        
        // Langsamste Requests
        const slowest = [...this.requests]
            .sort((a, b) => b.duration - a.duration)
            .slice(0, 5)
            .map(r => ({
                url: r.url,
                duration: r.duration,
                statusCode: r.statusCode
            }));
        
        // Status-Code-Verteilung
        const statusCodes = {};
        recentRequests.forEach(r => {
            const code = r.statusCode;
            statusCodes[code] = (statusCodes[code] || 0) + 1;
        });
        
        return {
            uptime,
            totalRequests: this.requests.length,
            recentRequests: recentRequests.length,
            avgResponseTime: avgDuration,
            slowestRequests: slowest,
            statusCodes,
            memory: {
                used: Math.round(process.memoryUsage().heapUsed / 1024 / 1024),
                total: Math.round(process.memoryUsage().heapTotal / 1024 / 1024),
                unit: 'MB'
            },
            cpu: {
                user: Math.round(process.cpuUsage().user / 1000),
                system: Math.round(process.cpuUsage().system / 1000),
                unit: 'ms'
            }
        };
    }
}

module.exports = PerformanceMonitor;
```

### 4.2 In Server integrieren

In **`server-advanced.js`**:

```javascript
const PerformanceMonitor = require('./performance-monitor');
const perfMonitor = new PerformanceMonitor();

// Im createServer, nach response.end():
const duration = Date.now() - startTime;
perfMonitor.recordRequest(duration, response.statusCode, request.url);

// Neuer API-Endpoint für Performance-Stats
if (request.url === '/api/performance') {
    response.statusCode = 200;
    response.setHeader('Content-Type', 'application/json; charset=utf-8');
    response.end(JSON.stringify(perfMonitor.getStats(), null, 2));
    return;
}
```

### 4.3 Monitoring-Dashboard erstellen

Erstelle **`public/monitoring.html`**:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Server Monitoring</title>
    <link rel="stylesheet" href="/css/style.css">
    <style>
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        .metric-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            text-align: center;
        }
        .metric-value {
            font-size: 36px;
            font-weight: bold;
            color: #376B8C;
        }
        .metric-label {
            color: #666;
            margin-top: 10px;
        }
        .chart {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background: #376B8C;
            color: white;
        }
    </style>
</head>
<body>
    <nav class="navbar">
        <div class="nav-container">
            <a href="/" class="nav-logo">Portfolio</a>
            <ul class="nav-menu">
                <li><a href="/" class="nav-link">Home</a></li>
                <li><a href="/monitoring.html" class="nav-link">Monitoring</a></li>
            </ul>
        </div>
    </nav>
    
    <main class="container">
        <section class="hero">
            <h1>Server Performance Monitoring</h1>
        </section>
        
        <div class="metrics-grid" id="metrics-grid">
            <!-- Wird dynamisch gefüllt -->
        </div>
        
        <div class="chart">
            <h2>Langsamste Requests</h2>
            <table id="slowest-table">
                <thead>
                    <tr>
                        <th>URL</th>
                        <th>Dauer (ms)</th>
                        <th>Status</th>
                    </tr>
                </thead>
                <tbody id="slowest-body">
                    <!-- Wird dynamisch gefüllt -->
                </tbody>
            </table>
        </div>
        
        <div class="chart">
            <h2>Status-Code-Verteilung</h2>
            <div id="status-codes"></div>
        </div>
    </main>
    
    <script>
        async function updateMonitoring() {
            try {
                const response = await fetch('/api/performance');
                const stats = await response.json();
                
                // Metriken aktualisieren
                const metricsGrid = document.getElementById('metrics-grid');
                metricsGrid.innerHTML = `
                    <div class="metric-card">
                        <div class="metric-value">${stats.uptime}s</div>
                        <div class="metric-label">Uptime</div>
                    </div>
                    <div class="metric-card">
                        <div class="metric-value">${stats.totalRequests}</div>
                        <div class="metric-label">Total Requests</div>
                    </div>
                    <div class="metric-card">
                        <div class="metric-value">${stats.avgResponseTime}ms</div>
                        <div class="metric-label">Ø Response Time</div>
                    </div>
                    <div class="metric-card">
                        <div class="metric-value">${stats.memory.used} MB</div>
                        <div class="metric-label">Memory Used</div>
                    </div>
                `;
                
                // Langsamste Requests
                const slowestBody = document.getElementById('slowest-body');
                slowestBody.innerHTML = stats.slowestRequests
                    .map(r => `
                        <tr>
                            <td>${r.url}</td>
                            <td>${r.duration}</td>
                            <td>${r.statusCode}</td>
                        </tr>
                    `).join('');
                
                // Status-Codes
                const statusCodesDiv = document.getElementById('status-codes');
                statusCodesDiv.innerHTML = Object.entries(stats.statusCodes)
                    .map(([code, count]) => `
                        <p><strong>${code}:</strong> ${count} Requests</p>
                    `).join('');
                    
            } catch (error) {
                console.error('Fehler beim Laden der Monitoring-Daten:', error);
            }
        }
        
        // Automatisches Update alle 5 Sekunden
        updateMonitoring();
        setInterval(updateMonitoring, 5000);
    </script>
</body>
</html>
```

---

## Teil 5: Erweiterte API-Endpoints (30 Min)

### 5.1 Vollständige API erstellen

Füge in **`server-advanced.js`** weitere Endpoints hinzu:

```javascript
// API-Routing
if (request.url.startsWith('/api/')) {
    response.setHeader('Content-Type', 'application/json; charset=utf-8');
    
    if (request.url === '/api/health') {
        // Health-Check Endpoint
        response.statusCode = 200;
        response.end(JSON.stringify({
            status: 'ok',
            timestamp: new Date().toISOString(),
            uptime: process.uptime(),
            version: '1.0.0'
        }, null, 2));
        return;
    }
    
    if (request.url === '/api/performance') {
        response.statusCode = 200;
        response.end(JSON.stringify(perfMonitor.getStats(), null, 2));
        return;
    }
    
    if (request.url === '/api/logs') {
        // Letzte 50 Log-Einträge
        const logFile = path.join(__dirname, 'logs', `app-${new Date().toISOString().split('T')[0]}.log`);
        
        if (fs.existsSync(logFile)) {
            const logs = fs.readFileSync(logFile, 'utf-8')
                .split('\n')
                .filter(line => line.trim())
                .slice(-50);
                
            response.statusCode = 200;
            response.end(JSON.stringify({ logs }, null, 2));
        } else {
            response.statusCode = 404;
            response.end(JSON.stringify({ error: 'Keine Logs verfügbar' }));
        }
        return;
    }
    
    if (request.url === '/api/files') {
        // Liste aller Dateien im public-Ordner
        const publicPath = path.join(__dirname, 'public');
        const files = getAllFiles(publicPath, publicPath);
        
        response.statusCode = 200;
        response.end(JSON.stringify({ files }, null, 2));
        return;
    }
    
    // API-Übersicht
    if (request.url === '/api' || request.url === '/api/') {
        response.statusCode = 200;
        response.end(JSON.stringify({
            message: 'Portfolio Server API',
            version: '1.0.0',
            endpoints: [
                { url: '/api/health', description: 'Server-Status' },
                { url: '/api/performance', description: 'Performance-Metriken' },
                { url: '/api/logs', description: 'Server-Logs (letzte 50)' },
                { url: '/api/files', description: 'Liste aller Dateien' }
            ]
        }, null, 2));
        return;
    }
}

// Hilfsfunktion für rekursive Datei-Liste
function getAllFiles(dir, baseDir) {
    let results = [];
    const list = fs.readdirSync(dir);
    
    list.forEach(file => {
        const filePath = path.join(dir, file);
        const stat = fs.statSync(filePath);
        
        if (stat.isDirectory()) {
            results = results.concat(getAllFiles(filePath, baseDir));
        } else {
            results.push({
                path: path.relative(baseDir, filePath),
                size: stat.size,
                modified: stat.mtime.toISOString()
            });
        }
    });
    
    return results;
}
```

---

## Erfolgskriterien

- [ ] Logger-System implementiert mit Datei-Logging
- [ ] Logs werden in `logs/`-Ordner gespeichert
- [ ] Nodemon installiert und konfiguriert
- [ ] Auto-Restart funktioniert bei Dateiänderungen
- [ ] Environment-Variablen mit dotenv konfiguriert
- [ ] `.env` und `.gitignore` korrekt eingerichtet
- [ ] Performance-Monitoring implementiert
- [ ] Monitoring-Dashboard erstellt und funktioniert
- [ ] Mindestens 4 API-Endpoints funktionieren
- [ ] Graceful Shutdown implementiert (Ctrl+C)
- [ ] Server läuft stabil auch unter Last

## Tipps

**Logging:**
- Nutze verschiedene Log-Level (DEBUG, INFO, WARN, ERROR)
- Rotiere Log-Dateien täglich
- Verwende strukturiertes Logging (JSON)

**Performance:**
- Überwache Response-Times
- Setze Limits für Request-Grösse
- Nutze Caching wo möglich

**Sicherheit:**
- Niemals `.env` ins Git
- Validiere alle Eingaben
- Setze Rate-Limiting

**Deployment:**
- Nutze PM2 für Produktion
- Setze `NODE_ENV=production`
- Aktiviere HTTPS (später mit Express)

## Reflexionsfragen

1. Warum ist strukturiertes Logging wichtig?
2. Was sind die Vorteile von Environment-Variablen gegenüber hardcodierten Werten?
3. Wie könnte man das Performance-Monitoring erweitern?
4. Recherchiere: Was macht PM2 und warum nutzt man es in Produktion?
5. Wie würdest du Rate-Limiting implementieren (max. 100 Requests/Minute)?

## Weiterführende Links

- [Winston Logger](https://github.com/winstonjs/winston) – Professionelles Logging
- [PM2](https://pm2.keymetrics.io/) – Process Manager für Produktion
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices) – Best Practices
- [dotenv](https://github.com/motdotla/dotenv) – Environment-Variablen
- [Clinic.js](https://clinicjs.org/) – Performance-Analyse

---

**⏱️ Geschätzte Zeit:** 120-150 Minuten  
**🎯 Nächster Schritt:** Express.js lernen – das macht alles viel einfacher!
