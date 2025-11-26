# Auftrag 1: Ersten HTTP-Server erstellen

## Ziel

Du erstellst deinen ersten funktionsfähigen HTTP-Server mit Node.js und dem http-Modul. Der Server reagiert auf Browser-Anfragen, liefert HTML-Inhalte aus und läuft dauerhaft, bis du ihn stoppst.

## Beschreibung

Das http-Modul ist direkt in Node.js integriert und ermöglicht es dir, einen Webserver zu erstellen, ohne zusätzliche Pakete zu installieren. In diesem Auftrag lernst du die Grundlagen: Server erstellen, starten, auf Anfragen reagieren und HTML-Inhalte ausliefern.

**Geschätzte Zeit:** 30-40 Minuten

---

## Teil 1: Projekt vorbereiten (5 Min)

### 1.1 Arbeitsordner erstellen

```bash
# Neuen Ordner erstellen
mkdir portfolio-server
cd portfolio-server

# VS Code öffnen
code .
```

### 1.2 Node.js prüfen

```bash
# Node.js Version checken
node --version
```

**Erwartete Ausgabe:** `v20.x.x` oder ähnlich

Falls Node.js nicht installiert ist, gehe zu [nodejs.org](https://nodejs.org) und installiere die LTS-Version.

---

## Teil 2: Ersten Server erstellen (10 Min)

### 2.1 Server-Datei anlegen

Erstelle eine Datei **`server.js`** mit folgendem Inhalt:

```javascript
// server.js - Mein erster HTTP-Server

// HTTP-Modul importieren (eingebaut in Node.js)
const http = require('http');

console.log('HTTP-Modul erfolgreich importiert!');
console.log('Node.js Version:', process.version);
```

**Ausführen:**

```bash
node server.js
```

**Erwartete Ausgabe:**
```
HTTP-Modul erfolgreich importiert!
Node.js Version: v20.10.0
```

### 2.2 Server-Objekt erstellen

Erweitere **`server.js`**:

```javascript
// server.js

const http = require('http');

// Server erstellen mit Callback-Funktion
const server = http.createServer((request, response) => {
    // Diese Funktion wird bei JEDER Anfrage ausgeführt
    console.log('Neue Anfrage erhalten!');
    console.log('URL:', request.url);
    console.log('Methode:', request.method);
    console.log('---');
    
    // Antwort senden
    response.statusCode = 200;  // HTTP-Status: 200 = OK
    response.setHeader('Content-Type', 'text/plain; charset=utf-8');
    response.end('Hallo vom Node.js-Server!');
});

console.log('Server-Objekt erstellt (läuft aber noch nicht).');
```

**Was passiert hier?**
- `http.createServer()` erstellt den Server
- Die Callback-Funktion erhält `request` (Anfrage vom Browser) und `response` (Antwort an Browser)
- `response.statusCode = 200` setzt den HTTP-Status auf "OK"
- `response.setHeader()` definiert den Content-Type
- `response.end()` sendet die Antwort und beendet sie

**Wichtig:** Der Server läuft noch NICHT – wir haben ihn nur erstellt.

### 2.3 Server starten

Erweitere **`server.js`** am Ende:

```javascript
// Server auf Port 3000 starten
const PORT = 3000;

server.listen(PORT, () => {
    console.log(`✅ Server läuft auf http://localhost:${PORT}`);
    console.log('Drücke Ctrl+C zum Beenden');
});
```

**Vollständiger Code bisher:**

```javascript
// server.js - Kompletter HTTP-Server

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    response.statusCode = 200;
    response.setHeader('Content-Type', 'text/plain; charset=utf-8');
    response.end('Hallo vom Node.js-Server!');
});

const PORT = 3000;

server.listen(PORT, () => {
    console.log(`✅ Server läuft auf http://localhost:${PORT}`);
    console.log('Drücke Ctrl+C zum Beenden');
});
```

**Server starten:**

```bash
node server.js
```

**Erwartete Ausgabe:**
```
✅ Server läuft auf http://localhost:3000
Drücke Ctrl+C zum Beenden
```

**Jetzt läuft der Server dauerhaft!**

### 2.4 Im Browser testen

Öffne deinen Browser und gehe zu:

```
http://localhost:3000
```

**Im Browser siehst du:**
```
Hallo vom Node.js-Server!
```

**Im Terminal siehst du (bei jedem Reload):**
```
GET /
GET /favicon.ico
```

**Was ist `favicon.ico`?**  
Der Browser fragt automatisch nach einem Icon für den Tab. Das ist normal und kann ignoriert werden.

---

## Teil 3: HTML statt Text ausliefern (15 Min)

### 3.1 Content-Type ändern

Ändere den Content-Type zu `text/html`:

```javascript
// server.js

const http = require('http');

const server = http.createServer((request, response) => {
    console.log(`${request.method} ${request.url}`);
    
    // HTML ausliefern statt Text
    response.statusCode = 200;
    response.setHeader('Content-Type', 'text/html; charset=utf-8');
    
    const html = `
        <!DOCTYPE html>
        <html lang="de">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Mein Portfolio-Server</title>
        </head>
        <body>
            <h1>Willkommen auf meinem Portfolio-Server!</h1>
            <p>Dieser Server läuft mit Node.js und dem http-Modul.</p>
        </body>
        </html>
    `;
    
    response.end(html);
});

const PORT = 3000;

server.listen(PORT, () => {
    console.log(`✅ Server läuft auf http://localhost:${PORT}`);
});
```

**Server neu starten:**

```bash
# Alten Server stoppen: Ctrl+C
# Neu starten:
node server.js
```

**Im Browser:** Jetzt siehst du eine formatierte HTML-Seite!

### 3.2 Styling hinzufügen

Erweitere den HTML-Code um CSS:

```javascript
const html = `
    <!DOCTYPE html>
    <html lang="de">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Portfolio-Server</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                max-width: 800px;
                margin: 50px auto;
                padding: 20px;
                background-color: #f5f5f5;
            }
            
            h1 {
                color: #376B8C;
            }
            
            .info-box {
                background: white;
                padding: 20px;
                border-radius: 8px;
                box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                margin-top: 20px;
            }
            
            .highlight {
                color: #29786A;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <h1>Willkommen auf meinem Portfolio-Server!</h1>
        
        <div class="info-box">
            <p>Dieser Server läuft mit <span class="highlight">Node.js</span> und dem <span class="highlight">http-Modul</span>.</p>
            <p><strong>Aktuelle Zeit:</strong> ${new Date().toLocaleString('de-CH')}</p>
            <p><strong>Server-Port:</strong> ${PORT}</p>
        </div>
    </body>
    </html>
`;
```

**Neu starten und im Browser ansehen!**

### 3.3 Dynamische Inhalte

Füge weitere dynamische Informationen hinzu:

```javascript
const html = `
    <!DOCTYPE html>
    <html lang="de">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Portfolio-Server</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                max-width: 800px;
                margin: 50px auto;
                padding: 20px;
                background-color: #f5f5f5;
            }
            h1 { color: #376B8C; }
            .info-box {
                background: white;
                padding: 20px;
                border-radius: 8px;
                box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                margin-top: 20px;
            }
            .highlight { color: #29786A; font-weight: bold; }
            .stats { display: flex; gap: 20px; margin-top: 20px; }
            .stat {
                flex: 1;
                background: #376B8C;
                color: white;
                padding: 15px;
                border-radius: 4px;
                text-align: center;
            }
            .stat-value { font-size: 24px; font-weight: bold; }
        </style>
    </head>
    <body>
        <h1>Mein Portfolio-Server</h1>
        
        <div class="info-box">
            <p>Dieser Server läuft mit <span class="highlight">Node.js ${process.version}</span>.</p>
            <p><strong>Aktuelles Datum:</strong> ${new Date().toLocaleDateString('de-CH', { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            })}</p>
            <p><strong>Aktuelle Zeit:</strong> ${new Date().toLocaleTimeString('de-CH')}</p>
        </div>
        
        <div class="stats">
            <div class="stat">
                <div class="stat-value">${PORT}</div>
                <div>Server-Port</div>
            </div>
            <div class="stat">
                <div class="stat-value">${request.method}</div>
                <div>HTTP-Methode</div>
            </div>
            <div class="stat">
                <div class="stat-value">${request.url}</div>
                <div>Angeforderte URL</div>
            </div>
        </div>
        
        <div class="info-box">
            <h2>Server-Informationen</h2>
            <ul>
                <li>Plattform: ${process.platform}</li>
                <li>Node.js Version: ${process.version}</li>
                <li>Arbeitsspeicher: ${Math.round(process.memoryUsage().heapUsed / 1024 / 1024)} MB</li>
                <li>Uptime: ${Math.round(process.uptime())} Sekunden</li>
            </ul>
        </div>
    </body>
    </html>
`;
```

**Server neu starten und staunen!**

---

## Erfolgskriterien

- [ ] Node.js ist installiert und funktioniert
- [ ] `server.js` wurde erstellt
- [ ] HTTP-Modul wurde erfolgreich importiert
- [ ] Server wurde mit `http.createServer()` erstellt
- [ ] Server läuft auf Port 3000 mit `server.listen()`
- [ ] Server antwortet im Browser auf `http://localhost:3000`
- [ ] HTML-Inhalte werden korrekt ausgeliefert (nicht nur Text)
- [ ] CSS-Styling wird angewendet
- [ ] Dynamische Inhalte (Datum, Zeit, Port) werden angezeigt
- [ ] Server läuft dauerhaft, bis er mit `Ctrl+C` gestoppt wird
- [ ] Im Terminal werden alle Anfragen geloggt

## Tipps

**Server stoppen:**
- `Ctrl+C` im Terminal stoppt den Server
- Ohne Stoppen läuft er endlos weiter

**Änderungen testen:**
- Nach jeder Code-Änderung MUSS der Server neu gestartet werden
- `Ctrl+C` → `node server.js`

**Browser-Cache:**
- Bei Problemen: Hard Reload mit `Ctrl+Shift+R` (Windows) oder `Cmd+Shift+R` (Mac)

**Terminal-Ausgaben:**
- Nutze `console.log()` zum Debugging
- Jede Anfrage erscheint im Terminal

**Port bereits belegt?**
- Ändere `const PORT = 3000` zu einer anderen Zahl (z.B. 3001, 8000, 8080)
- Oder stoppe den laufenden Prozess

**Häufige Fehler:**
- `EADDRINUSE`: Port ist bereits belegt → anderen Port nutzen
- `Cannot GET /`: Server läuft nicht → `node server.js` ausführen
- Änderungen nicht sichtbar: Server neu starten!

## Reflexionsfragen

1. Was ist der Unterschied zwischen `http.createServer()` und `server.listen()`?
2. Warum musst du den Server nach jeder Code-Änderung neu starten?
3. Teste: Was passiert, wenn du `response.setHeader('Content-Type', 'text/plain')` nutzt, aber HTML-Code sendest?
4. Was ist ein Port? Warum braucht der Server einen Port?
5. Öffne die Browser Developer Tools (F12) → Network-Tab. Was siehst du, wenn du die Seite lädst?

## Weiterführende Links

- [Node.js HTTP Dokumentation](https://nodejs.org/docs/latest/api/http.html) – Offizielle Doku
- [MDN: HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) – HTTP-Grundlagen
- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) – Alle Statuscodes
- [Node.js Process](https://nodejs.org/docs/latest/api/process.html) – process-Objekt
- [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) – Mehrzeilige Strings

---

**⏱️ Geschätzte Zeit:** 30-40 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lernst du Routing – verschiedene URLs, verschiedene Antworten!
