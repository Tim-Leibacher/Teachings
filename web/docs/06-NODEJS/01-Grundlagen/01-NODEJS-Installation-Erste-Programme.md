# Auftrag 1: Node.js installieren und erste Programme erstellen

## Ziel

Du installierst Node.js auf deinem Computer, führst erste JavaScript-Programme im Terminal aus und verstehst den Unterschied zwischen JavaScript im Browser und auf dem Server.

## Beschreibung

Bisher hast du JavaScript nur im Browser genutzt. Mit Node.js kannst du JavaScript auch auf dem Server, in der Kommandozeile und für viele andere Zwecke ausführen. In diesem Auftrag installierst du Node.js, überprüfst die Installation und erstellst deine ersten Programme, die direkt im Terminal laufen.

**Geschätzte Zeit:** 30 Minuten

---

## Teil 1: Node.js installieren und prüfen (10 Min)

### 1.1 Installation

1. Gehe auf [nodejs.org](https://nodejs.org)
2. Lade die **LTS-Version** herunter (Long Term Support)
   - Windows: `.msi` Installer herunterladen und ausführen
   - Mac: `.pkg` Installer herunterladen und ausführen
   - Linux: Nutze den Package Manager deiner Distribution

**Warum LTS?**
Die LTS-Version ist die stabile Version, die für Produktivumgebungen empfohlen wird. Sie erhält Updates und Bugfixes über einen längeren Zeitraum.

### 1.2 Installation überprüfen

Öffne das Terminal (Windows: PowerShell oder CMD, Mac/Linux: Terminal) und führe folgende Befehle aus:

```bash
# Node.js Version überprüfen
node --version

# NPM Version überprüfen (wird automatisch mit Node.js installiert)
npm --version
```

**Erwartete Ausgabe:**
```
v20.10.0  (oder ähnlich)
10.2.3    (oder ähnlich)
```

**Fehlerbehebung:**
- Falls `node: command not found` erscheint: Installation wiederholen oder Pfad zur Umgebungsvariable hinzufügen
- Windows: Neues Terminal-Fenster öffnen, damit Änderungen wirksam werden

### 1.3 Node.js REPL testen

Node.js hat eine interaktive Konsole (REPL = Read-Eval-Print Loop):

```bash
# REPL starten
node
```

Du siehst nun `>` als Eingabeaufforderung. Teste ein paar Befehle:

```javascript
> console.log('Hallo Node.js!')
Hallo Node.js!

> 5 + 10
15

> const name = 'Max'
> `Hallo ${name}`
'Hallo Max'

> .exit
```

Mit `.exit` oder `Ctrl+C` (zweimal) verlässt du die REPL.

---

## Teil 2: Erstes Node.js-Programm erstellen (10 Min)

### 2.1 Arbeitsordner vorbereiten

Erstelle einen neuen Ordner für deine Node.js-Experimente:

```bash
# Ordner erstellen und öffnen
mkdir node-basics
cd node-basics
```

Öffne den Ordner in VS Code:

```bash
code .
```

### 2.2 hello.js erstellen

Erstelle eine Datei namens **`hello.js`** mit folgendem Inhalt:

```javascript
// hello.js - Mein erstes Node.js-Programm

console.log('Hallo von Node.js!');
console.log('JavaScript läuft jetzt auf dem Server!');

// Variablen funktionieren wie im Browser
const name = 'Max Muster';
const alter = 17;

console.log(`Ich heisse ${name} und bin ${alter} Jahre alt.`);

// Mathematische Operationen
const geburtsjahr = new Date().getFullYear() - alter;
console.log(`Ich wurde ${geburtsjahr} geboren.`);

// Aktuelle Zeit ausgeben
const jetzt = new Date();
console.log(`\nAktuelles Datum und Zeit:`);
console.log(jetzt.toLocaleString('de-CH'));
```

### 2.3 Programm ausführen

Im Terminal (im Ordner `node-basics`):

```bash
node hello.js
```

**Erwartete Ausgabe:**
```
Hallo von Node.js!
JavaScript läuft jetzt auf dem Server!
Ich heisse Max Muster und bin 17 Jahre alt.
Ich wurde 2008 geboren.

Aktuelles Datum und Zeit:
26.11.2025, 14:45:23
```

**Wichtig:** Im Gegensatz zum Browser gibt es hier kein HTML, kein DOM und keine Browser-APIs. Dafür läuft das Programm direkt im Terminal!

---

## Teil 3: Node.js Module nutzen – Dateisystem (15 Min)

Node.js hat eingebaute Module wie `fs` (File System), mit denen du Dateien erstellen, lesen, ändern und löschen kannst.

### 3.1 Datei erstellen und schreiben

Erstelle eine Datei **`dateien.js`**:

```javascript
// dateien.js - Arbeiten mit dem Dateisystem

// fs-Modul importieren (eingebaut in Node.js)
const fs = require('fs');

// Text definieren
const meinText = `Das ist mein erstes Node.js-Programm!
Ich lerne gerade:
- JavaScript auf dem Server
- Node.js Module
- Dateisystem-Zugriff

Datum: ${new Date().toLocaleDateString('de-CH')}`;

// Datei erstellen und Text schreiben
fs.writeFileSync('portfolio-notiz.txt', meinText, 'utf-8');

console.log('✅ Datei "portfolio-notiz.txt" wurde erstellt!');
```

Programm ausführen:

```bash
node dateien.js
```

**Erwartete Ausgabe:**
```
✅ Datei "portfolio-notiz.txt" wurde erstellt!
```

Schaue in VS Code nach – die Datei `portfolio-notiz.txt` sollte jetzt existieren!

### 3.2 Datei auslesen

Erweitere `dateien.js` um folgenden Code (nach dem writeFileSync):

```javascript
// Datei wieder auslesen
console.log('\n📄 Inhalt der Datei:');
console.log('─'.repeat(50));

const inhalt = fs.readFileSync('portfolio-notiz.txt', 'utf-8');
console.log(inhalt);

console.log('─'.repeat(50));
```

Programm erneut ausführen:

```bash
node dateien.js
```

**Erwartete Ausgabe:**
```
✅ Datei "portfolio-notiz.txt" wurde erstellt!

📄 Inhalt der Datei:
──────────────────────────────────────────────────
Das ist mein erstes Node.js-Programm!
Ich lerne gerade:
- JavaScript auf dem Server
- Node.js Module
- Dateisystem-Zugriff

Datum: 26.11.2025
──────────────────────────────────────────────────
```

### 3.3 Informationen über Dateien abrufen

Erweitere `dateien.js` weiter:

```javascript
// Datei-Informationen abrufen
const stats = fs.statSync('portfolio-notiz.txt');

console.log('\n📊 Datei-Informationen:');
console.log(`Grösse: ${stats.size} Bytes`);
console.log(`Erstellt am: ${stats.birthtime.toLocaleString('de-CH')}`);
console.log(`Zuletzt geändert: ${stats.mtime.toLocaleString('de-CH')}`);
console.log(`Ist Datei: ${stats.isFile()}`);
console.log(`Ist Ordner: ${stats.isDirectory()}`);
```

### 3.4 Ordner erstellen

Füge am Ende von `dateien.js` hinzu:

```javascript
// Ordner erstellen (falls nicht vorhanden)
const ordnerName = 'meine-notizen';

if (!fs.existsSync(ordnerName)) {
    fs.mkdirSync(ordnerName);
    console.log(`\n📁 Ordner "${ordnerName}" wurde erstellt!`);
} else {
    console.log(`\n📁 Ordner "${ordnerName}" existiert bereits.`);
}

// Datei in den neuen Ordner kopieren
fs.copyFileSync('portfolio-notiz.txt', `${ordnerName}/kopie.txt`);
console.log('✅ Datei wurde in den Ordner kopiert!');
```

---

## Erfolgskriterien

- [ ] Node.js ist installiert und `node --version` funktioniert
- [ ] NPM ist installiert und `npm --version` funktioniert
- [ ] Die REPL wurde getestet
- [ ] `hello.js` wurde erstellt und erfolgreich mit `node hello.js` ausgeführt
- [ ] `dateien.js` wurde erstellt und kann Dateien erstellen, lesen und kopieren
- [ ] Die Datei `portfolio-notiz.txt` existiert im Projektordner
- [ ] Der Ordner `meine-notizen` wurde erstellt
- [ ] Du verstehst den Unterschied zwischen JavaScript im Browser und in Node.js

## Tipps

- **Terminal-Shortcuts:**
  - `Ctrl+C` = Programm stoppen
  - `Ctrl+L` oder `clear` = Terminal aufräumen
  - Pfeiltasten hoch/runter = Letzte Befehle wiederholen
- **Fehlersuche:** Nutze `console.log()` für Debugging, genau wie im Browser
- **Dateipfade:** Node.js arbeitet relativ zum aktuellen Verzeichnis im Terminal
- **Module importieren:** `require()` ist für CommonJS-Module, später lernst du auch ES6-Module mit `import`

## Reflexionsfragen

1. Was ist der Hauptunterschied zwischen JavaScript im Browser und in Node.js?
2. Warum braucht Node.js kein `<script>`-Tag wie im HTML?
3. Teste: Was passiert, wenn du versuchst, `document.getElementById()` in Node.js zu nutzen? Warum?
4. Schaue dir die Node.js-Dokumentation für das `fs`-Modul an. Welche weiteren Funktionen gibt es? ([Link zur Doku](https://nodejs.org/docs/latest/api/fs.html))
5. Wofür könnte man Node.js in der echten Welt nutzen? Nenne mindestens 3 Anwendungsfälle.

## Weiterführende Links

- [Node.js Dokumentation](https://nodejs.org/docs/) – Offizielle Dokumentation
- [MDN: Node.js](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework) – Einführung von MDN
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices) – Professionelle Best Practices
- [W3Schools Node.js Tutorial](https://www.w3schools.com/nodejs/) – Anfängerfreundliches Tutorial
- [Node School](https://nodeschool.io/) – Interaktive Tutorials

---

**Geschätzte Zeit:** 30 Minuten
