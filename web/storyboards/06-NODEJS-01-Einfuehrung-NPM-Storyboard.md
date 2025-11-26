# Storyboard: Einführung in Node.js und NPM

**Gesamtdauer:** ca. 8-10 Minuten  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Voraussetzungen:** JavaScript-Grundlagen, Terminal-Nutzung, VS Code

---

## Szene 1: Intro – Was ist Node.js? (30 Sek.)

### Sprechertext
"Willkommen zum Node.js-Modul! Bisher haben wir JavaScript nur im Browser genutzt. Mit Node.js kannst du JavaScript aber auch auf dem Server ausführen. Das bedeutet: Du kannst mit JavaScript Backend-Anwendungen, APIs, Automatisierungs-Tools und vieles mehr entwickeln. Node.js ist schnell, effizient und wird von Millionen Entwicklern weltweit genutzt. In diesem Video lernst du die Grundlagen von Node.js und NPM, dem Node Package Manager."

### Bildschirmdarstellung
- BAND-Logo mit Titel: **"Node.js und NPM – Einführung"**
- Text-Overlay: 
  - **"JavaScript überall ausführen"**
  - **"Server, Tools, APIs"**
  - **"Von Netflix bis NASA"**

### Hinweise
- Nutze BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A)
- Fade-In Animation

---

## Szene 2: JavaScript im Browser vs. Node.js (1 Min.)

### Sprechertext
"Schauen wir uns den Unterschied an. Im Browser läuft JavaScript in einer Sandbox. Du hast Zugriff auf das DOM, also auf HTML-Elemente, und auf Browser-APIs wie `fetch` oder `localStorage`. Im Node.js fehlt das DOM, weil es keinen Browser gibt. Dafür hast du Zugriff auf das Dateisystem, Netzwerk-Funktionen und kannst Server erstellen. Das bedeutet: Mit Node.js kannst du Dateien lesen und schreiben, HTTP-Server starten und vieles mehr."

### Bildschirmdarstellung
Split-Screen mit zwei Code-Beispielen:

**Links: Browser JavaScript**
```javascript
// Browser – DOM-Manipulation
document.getElementById('button').addEventListener('click', () => {
    console.log('Button geklickt!');
});

// Browser – LocalStorage
localStorage.setItem('name', 'Max');
```

**Rechts: Node.js JavaScript**
```javascript
// Node.js – Dateisystem
const fs = require('fs');
fs.readFileSync('datei.txt', 'utf-8');

// Node.js – HTTP-Server
const http = require('http');
http.createServer((req, res) => {
    res.end('Hello World!');
}).listen(3000);
```

### Hinweise
- Nutze Syntax-Highlighting
- Text-Overlay: **"Browser = DOM | Node.js = Dateisystem + Server"**

---

## Szene 3: Node.js installieren (45 Sek.)

### Sprechertext
"Bevor wir loslegen, muss Node.js installiert sein. Gehe auf nodejs.org und lade die LTS-Version herunter. LTS steht für Long Term Support und ist die stabile Version. Nach der Installation kannst du im Terminal `node --version` eingeben, um zu prüfen, ob alles funktioniert. NPM wird automatisch mit Node.js installiert. Überprüfe das mit `npm --version`."

### Bildschirmdarstellung
1. Browser zeigen: [nodejs.org](https://nodejs.org)
   - Highlight auf **"LTS"**-Button
2. Terminal-Fenster mit folgenden Befehlen:

```bash
# Node.js Version überprüfen
node --version
# Ausgabe: v20.10.0

# NPM Version überprüfen
npm --version
# Ausgabe: 10.2.3
```

### Hinweise
- Text-Overlay: **"nodejs.org → LTS-Version herunterladen"**
- Zeige Downloads-Ordner mit Installer
- Grosser Font im Terminal für bessere Lesbarkeit

---

## Szene 4: Erstes Node.js-Programm (1 Min. 30 Sek.)

### Sprechertext
"Erstellen wir unser erstes Node.js-Programm! Öffne VS Code und erstelle eine neue Datei namens `hello.js`. Schreibe einfachen JavaScript-Code hinein. Im Gegensatz zum Browser führst du das Programm mit dem Befehl `node hello.js` im Terminal aus. Schau, wie schnell das geht!"

### Bildschirmdarstellung
VS Code mit neuer Datei **`hello.js`**:

```javascript
// hello.js - Erstes Node.js-Programm

console.log('Hallo von Node.js!');
console.log('JavaScript läuft auf dem Server!');

// Einfache Berechnung
const summe = 5 + 10;
console.log(`5 + 10 = ${summe}`);

// Aktuelle Zeit ausgeben
const jetzt = new Date();
console.log(`Aktuelles Datum: ${jetzt.toLocaleString('de-CH')}`);
```

Terminal parallel zeigen:

```bash
# Programm ausführen
node hello.js
```

**Ausgabe:**
```
Hallo von Node.js!
JavaScript läuft auf dem Server!
5 + 10 = 15
Aktuelles Datum: 26.11.2025, 14:32:15
```

### Hinweise
- Split-Screen: VS Code links, Terminal rechts
- Live-Typing für besseres Verständnis
- Text-Overlay: **"`node dateiname.js` führt JavaScript aus"**

---

## Szene 5: Node.js Module nutzen – `fs` (1 Min. 30 Sek.)

### Sprechertext
"Node.js hat eingebaute Module wie `fs` für das Dateisystem. Mit `require` können wir Module importieren. Schauen wir uns an, wie wir eine Datei erstellen und wieder auslesen können. Das wäre im Browser nicht möglich!"

### Bildschirmdarstellung
VS Code mit neuer Datei **`dateien.js`**:

```javascript
// dateien.js - Dateisystem nutzen

// fs-Modul importieren
const fs = require('fs');

// Datei erstellen und Text schreiben
const inhalt = 'Das ist mein erstes Node.js-Programm!\nNode.js ist cool!';
fs.writeFileSync('test.txt', inhalt, 'utf-8');
console.log('✅ Datei test.txt erstellt!');

// Datei auslesen
const gelesen = fs.readFileSync('test.txt', 'utf-8');
console.log('📄 Inhalt der Datei:');
console.log(gelesen);
```

Terminal zeigen:

```bash
# Programm ausführen
node dateien.js
```

**Ausgabe:**
```
✅ Datei test.txt erstellt!
📄 Inhalt der Datei:
Das ist mein erstes Node.js-Programm!
Node.js ist cool!
```

Danach: Zeige die neu erstellte Datei `test.txt` im VS Code Datei-Explorer

### Hinweise
- Erkläre `require()` kurz
- Zeige die erstellte Datei im Explorer
- Text-Overlay: **"fs-Modul = Dateisystem-Zugriff"**

---

## Szene 6: Was ist NPM? (1 Min.)

### Sprechertext
"NPM steht für Node Package Manager. Es ist der grösste Software-Registry der Welt mit über einer Million Paketen. Statt alles selbst zu programmieren, kannst du auf Pakete zugreifen, die andere Entwickler erstellt haben. Willst du mit Farben im Terminal arbeiten? Es gibt ein Paket dafür. HTTP-Anfragen vereinfachen? Es gibt ein Paket dafür. NPM spart dir extrem viel Zeit."

### Bildschirmdarstellung
Browser zeigen: [npmjs.com](https://www.npmjs.com)

**Suchbeispiele:**
- Suche: "colors" → Paket für farbige Terminal-Ausgaben
- Suche: "axios" → Beliebtes HTTP-Client-Paket
- Suche: "express" → Web-Framework für Node.js

Statistik-Overlay zeigen:
- **"Über 1 Million Pakete"**
- **"Milliarden Downloads pro Woche"**
- **"Von der Community für die Community"**

### Hinweise
- Zeige verschiedene Pakete mit Download-Zahlen
- Erkläre, dass alle Pakete Open Source sind

---

## Szene 7: NPM-Projekt initialisieren – `npm init` (2 Min.)

### Sprechertext
"Bevor wir Pakete installieren, initialisieren wir ein NPM-Projekt mit `npm init`. Das erstellt eine Datei namens `package.json`, die alle Informationen über dein Projekt enthält. Du wirst nach dem Namen, der Version, der Beschreibung und mehr gefragt. Du kannst alle Fragen mit Enter überspringen oder mit `npm init -y` direkt eine Standard-package.json erstellen."

### Bildschirmdarstellung
Terminal mit Projektordner **`mein-node-projekt/`**:

```bash
# Neuen Ordner erstellen
mkdir mein-node-projekt
cd mein-node-projekt

# NPM initialisieren (interaktiv)
npm init
```

**Interaktiver Dialog zeigen:**
```
package name: (mein-node-projekt) 
version: (1.0.0) 
description: Mein erstes Node.js-Projekt
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: Dein Name
license: (ISC) 
```

Dann **`package.json`** in VS Code zeigen:

```json
{
  "name": "mein-node-projekt",
  "version": "1.0.0",
  "description": "Mein erstes Node.js-Projekt",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Dein Name",
  "license": "ISC"
}
```

### Hinweise
- Erkläre die wichtigsten Felder kurz
- Text-Overlay: **"package.json = Projektbeschreibung"**

---

## Szene 8: NPM-Paket installieren – `chalk` (2 Min.)

### Sprechertext
"Installieren wir unser erstes Paket! `chalk` ist ein beliebtes Paket für farbige Terminal-Ausgaben. Mit `npm install chalk` wird das Paket heruntergeladen. NPM erstellt automatisch einen Ordner namens `node_modules`, wo alle Pakete gespeichert werden. Ausserdem wird das Paket in der `package.json` unter `dependencies` eingetragen."

### Bildschirmdarstellung
Terminal zeigen:

```bash
# Chalk installieren
npm install chalk
```

**Ausgabe:**
```
added 1 package, and audited 2 packages in 1s
found 0 vulnerabilities
```

VS Code zeigen:
1. **Neuer Ordner:** `node_modules/` mit vielen Unterordnern
2. **Neue Datei:** `package-lock.json`
3. **Aktualisierte `package.json`:**

```json
{
  "name": "mein-node-projekt",
  "version": "1.0.0",
  "description": "Mein erstes Node.js-Projekt",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Dein Name",
  "license": "ISC",
  "dependencies": {
    "chalk": "^5.3.0"
  }
}
```

### Hinweise
- Erkläre `node_modules/` kurz (niemals ins Git!)
- Text-Overlay: **"npm install = Paket herunterladen"**

---

## Szene 9: Chalk nutzen (1 Min. 30 Sek.)

### Sprechertext
"Nutzen wir das Paket! Importiere chalk mit `import` und nutze es, um farbige Ausgaben zu erstellen. Achtung: Ab Chalk Version 5 musst du ES6-Module nutzen. Dafür fügen wir `type: module` in der package.json hinzu."

### Bildschirmdarstellung
**Schritt 1:** `package.json` anpassen:

```json
{
  "name": "mein-node-projekt",
  "version": "1.0.0",
  "type": "module",
  // ... rest
}
```

**Schritt 2:** Neue Datei **`farben.js`** erstellen:

```javascript
// farben.js - Farbige Terminal-Ausgaben

// Chalk importieren
import chalk from 'chalk';

// Farbige Ausgaben
console.log(chalk.blue('Hallo in Blau!'));
console.log(chalk.green('Erfolg: Paket installiert ✅'));
console.log(chalk.red('Fehler: Etwas ging schief ❌'));
console.log(chalk.yellow.bold('Warnung: Vorsicht!'));

// Kombinationen
console.log(chalk.bgBlue.white(' INFO ') + ' Das ist eine Info-Nachricht');
console.log(chalk.bgGreen.black(' SUCCESS ') + ' Alles funktioniert!');
```

Terminal zeigen:

```bash
# Programm ausführen
node farben.js
```

**Ausgabe** (farbig im Terminal):
```
Hallo in Blau!
Erfolg: Paket installiert ✅
Fehler: Etwas ging schief ❌
Warnung: Vorsicht!
 INFO  Das ist eine Info-Nachricht
 SUCCESS  Alles funktioniert!
```

### Hinweise
- Zeige farbige Ausgaben deutlich im Terminal
- Erkläre ES6-Module kurz (`import` statt `require`)

---

## Szene 10: Globale vs. lokale Pakete (1 Min.)

### Sprechertext
"Es gibt zwei Arten von Paketen: Lokale Pakete werden nur in deinem Projekt installiert und stehen in `node_modules`. Globale Pakete werden systemweit installiert und können als Terminal-Befehle genutzt werden. Zum Beispiel kannst du `nodemon` global installieren, um Node.js-Programme automatisch neu zu starten, wenn sich Dateien ändern."

### Bildschirmdarstellung
Terminal mit Vergleich:

**Lokale Installation:**
```bash
# Nur für dieses Projekt
npm install chalk
```

**Globale Installation:**
```bash
# Systemweit verfügbar
npm install -g nodemon

# Nodemon nutzen
nodemon farben.js
# Programm startet und wird bei Änderungen automatisch neu geladen
```

### Hinweise
- Zeige nodemon in Aktion (Datei ändern → automatischer Neustart)
- Text-Overlay: **"Lokal = Projekt | Global = System"**

---

## Szene 11: NPM Scripts (1 Min. 30 Sek.)

### Sprechertext
"In der package.json kannst du eigene Scripts definieren. Das sind Shortcuts für häufig genutzte Befehle. Statt `node farben.js` zu tippen, kannst du einfach `npm run start` ausführen. Das ist besonders nützlich für komplexe Befehle."

### Bildschirmdarstellung
**`package.json`** erweitern:

```json
{
  "name": "mein-node-projekt",
  "version": "1.0.0",
  "type": "module",
  "description": "Mein erstes Node.js-Projekt",
  "main": "index.js",
  "scripts": {
    "start": "node farben.js",
    "dev": "nodemon farben.js",
    "hello": "node hello.js"
  },
  "author": "Dein Name",
  "license": "ISC",
  "dependencies": {
    "chalk": "^5.3.0"
  }
}
```

Terminal zeigen:

```bash
# Scripts ausführen
npm run start
# Führt: node farben.js

npm run dev
# Führt: nodemon farben.js

npm run hello
# Führt: node hello.js
```

### Hinweise
- Erkläre, dass `npm start` ohne `run` funktioniert (Spezialfall)
- Text-Overlay: **"Scripts = Shortcuts für Befehle"**

---

## Szene 12: Dependencies verwalten (1 Min.)

### Sprechertext
"In der package.json siehst du alle installierten Pakete unter `dependencies`. Die Versionsnummern folgen dem Schema `^5.3.0`: Die erste Zahl ist die Major-Version, die zweite die Minor-Version und die dritte die Patch-Version. Das Caret-Symbol `^` bedeutet, dass NPM automatisch Updates für Minor- und Patch-Versionen installiert, aber nicht für Major-Versionen, die Breaking Changes enthalten könnten."

### Bildschirmdarstellung
**`package.json`** zeigen mit Erklärung:

```json
{
  "dependencies": {
    "chalk": "^5.3.0"
    //       ^ │ │ │
    //       │ │ │ └─ Patch (Bugfixes)
    //       │ │ └─── Minor (neue Features)
    //       │ └───── Major (Breaking Changes)
    //       └─────── Updates erlaubt für Minor + Patch
  }
}
```

Terminal zeigen:

```bash
# Alle Pakete aktualisieren
npm update

# Veraltete Pakete anzeigen
npm outdated

# Spezifisches Paket aktualisieren
npm install chalk@latest
```

### Hinweise
- Zeige Beispiel mit `npm outdated`
- Text-Overlay: **"Semver: Major.Minor.Patch"**

---

## Szene 13: node_modules und .gitignore (1 Min.)

### Sprechertext
"Der `node_modules` Ordner kann sehr gross werden und sollte NIEMALS ins Git-Repository. Andere Entwickler installieren die Pakete einfach mit `npm install`, das alle Pakete aus der package.json herunterlädt. Erstelle eine `.gitignore`-Datei und füge `node_modules/` hinzu."

### Bildschirmdarstellung
VS Code zeigen: Neue Datei **`.gitignore`**:

```gitignore
# Dependencies
node_modules/

# Logs
npm-debug.log*

# Environment Variables
.env

# OS Files
.DS_Store
```

Terminal zeigen:

```bash
# Projekt klonen und Pakete installieren
git clone https://github.com/username/mein-node-projekt
cd mein-node-projekt
npm install
# Alle Pakete werden heruntergeladen!
```

### Hinweise
- Zeige Grösse von `node_modules/` (oft 100+ MB)
- Text-Overlay: **"Niemals node_modules/ ins Git!"**

---

## Szene 14: Zusammenfassung (45 Sek.)

### Sprechertext
"Fassen wir zusammen: Node.js erlaubt dir, JavaScript auf dem Server auszuführen. Mit NPM installierst du Pakete, die andere Entwickler erstellt haben. Mit `npm init` erstellst du ein Projekt, mit `npm install` installierst du Pakete. Die package.json verwaltet deine Dependencies und Scripts. Der node_modules Ordner gehört nie ins Git. In den nächsten Modulen werden wir mit Node.js einen echten HTTP-Server erstellen!"

### Bildschirmdarstellung
Zusammenfassung als Checkliste:

```
✅ Node.js = JavaScript überall
✅ NPM = Paketmanager mit 1 Million+ Paketen
✅ npm init = Projekt erstellen
✅ npm install <paket> = Paket installieren
✅ package.json = Projekt-Konfiguration
✅ node_modules/ = Nie ins Git!
✅ Scripts = Shortcuts definieren
```

### Hinweise
- Fade-Out mit BAND-Gradient-Hintergrund
- Call-to-Action: "Jetzt selbst ausprobieren!"

---

## Zusatzmaterialien für Video-Produktion

### Terminal-Setup für saubere Aufnahmen

**Empfohlene Einstellungen:**
- Schriftgrösse: 18-20pt
- Font: Monospace (z.B. Fira Code, Monaco)
- Farbschema: Hell oder Dunkel mit gutem Kontrast
- Fenstergrösse: 120x30 Zeichen

### Projekt-Struktur für Demo

```
mein-node-projekt/
├── .gitignore
├── package.json
├── package-lock.json
├── node_modules/
│   └── chalk/
├── hello.js
├── dateien.js
├── farben.js
└── test.txt
```

### Häufige Fehler & Lösungen (für Video erwähnen)

| Problem | Lösung |
|---------|--------|
| `node: command not found` | Node.js nicht installiert → nodejs.org |
| `Cannot find module 'chalk'` | `npm install` ausführen |
| `ERR! code ENOENT` | package.json fehlt → `npm init` ausführen |
| ES6 Import funktioniert nicht | `"type": "module"` in package.json hinzufügen |

### Weiterführende Ressourcen (am Ende erwähnen)

- [Node.js Dokumentation](https://nodejs.org/docs/)
- [NPM Dokumentation](https://docs.npmjs.com/)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [MDN: JavaScript Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

---

## Technische Hinweise für Videobearbeitung

- Nutze BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A, Orange)
- Screen-Recording mit 1920x1080 Auflösung
- Terminal und VS Code nebeneinander (Split-Screen) für besseres Verständnis
- Cursor-Highlights für wichtige Befehle
- Text-Overlays für Key-Takeaways
- Farbige Terminal-Ausgaben klar sichtbar machen
- Untertitel einbauen (für Barrierefreiheit)

---

**Ende des Storyboards**
