# Auftrag 2: NPM-Projekt erstellen und Pakete installieren

## Ziel

Du erstellst dein erstes NPM-Projekt mit `npm init`, installierst externe Pakete und lernst, wie du die `package.json` verwaltest. Du verstehst den Unterschied zwischen lokalen und globalen Paketen und nutzt NPM-Scripts für häufige Aufgaben.

## Beschreibung

NPM (Node Package Manager) ist das Herzstück des Node.js-Ökosystems. Mit NPM kannst du auf über eine Million fertige Code-Pakete zugreifen, die andere Entwickler erstellt haben. Statt alles selbst zu programmieren, nutzt du bewährte Lösungen und sparst extrem viel Zeit. In diesem Auftrag lernst du die Grundlagen von NPM und baust ein Portfolio-Tool, das farbige Terminal-Ausgaben erstellt.

**Geschätzte Zeit:** 40 Minuten

---

## Teil 1: NPM-Projekt initialisieren (10 Min)

### 1.1 Projekt-Ordner erstellen

Erstelle einen neuen Ordner für dein NPM-Projekt:

```bash
# Neuen Ordner erstellen
mkdir portfolio-tool
cd portfolio-tool

# In VS Code öffnen
code .
```

### 1.2 NPM initialisieren (interaktiv)

NPM-Projekt mit interaktivem Dialog erstellen:

```bash
npm init
```

Du wirst nach verschiedenen Informationen gefragt. Hier sind Vorschläge:

```
package name: (portfolio-tool) portfolio-tool
version: (1.0.0) 1.0.0
description: Ein Tool für mein Portfolio mit farbigen Ausgaben
entry point: (index.js) index.js
test command: (leer lassen, Enter drücken)
git repository: (leer lassen, Enter drücken)
keywords: portfolio, node, cli
author: Dein Name
license: (ISC) ISC
```

Am Ende siehst du eine Zusammenfassung. Bestätige mit `yes`.

**Ergebnis:** Eine Datei namens **`package.json`** wurde erstellt!

### 1.3 package.json verstehen

Öffne `package.json` in VS Code:

```json
{
  "name": "portfolio-tool",
  "version": "1.0.0",
  "description": "Ein Tool für mein Portfolio mit farbigen Ausgaben",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "portfolio",
    "node",
    "cli"
  ],
  "author": "Dein Name",
  "license": "ISC"
}
```

**Wichtige Felder:**
- **name:** Name deines Projekts (einzigartig bei Veröffentlichung auf NPM)
- **version:** Versionsnummer (folgt [Semantic Versioning](https://semver.org/))
- **description:** Kurze Beschreibung des Projekts
- **main:** Einstiegspunkt deiner Anwendung
- **scripts:** Shortcuts für häufige Befehle
- **dependencies:** Installierte Pakete (kommt später)

### 1.4 Schnelle Initialisierung

**Alternative:** Mit `npm init -y` werden alle Fragen mit Standard-Werten übersprungen:

```bash
npm init -y
```

Das ist nützlich für schnelle Experimente.

---

## Teil 2: Erstes Paket installieren – chalk (15 Min)

### 2.1 Was ist chalk?

`chalk` ist ein beliebtes NPM-Paket für farbige und gestylte Terminal-Ausgaben. Statt nur schwarzen Text zu sehen, kannst du Erfolgs-Meldungen grün, Fehler rot und Warnungen gelb darstellen.

**Informationen zu chalk:**
- [NPM-Seite](https://www.npmjs.com/package/chalk)
- Über 100 Millionen Downloads pro Woche
- Sehr einfach zu nutzen

### 2.2 chalk installieren

```bash
npm install chalk
```

**Erwartete Ausgabe:**
```
added 1 package, and audited 2 packages in 1s
found 0 vulnerabilities
```

**Was passiert?**
1. NPM lädt `chalk` von der NPM-Registry herunter
2. Ein Ordner **`node_modules/`** wird erstellt (enthält alle Pakete)
3. Eine Datei **`package-lock.json`** wird erstellt (sperrt Versionen)
4. In `package.json` wird chalk unter **`dependencies`** eingetragen

### 2.3 package.json nach Installation

Öffne `package.json` – es hat sich geändert:

```json
{
  "name": "portfolio-tool",
  "version": "1.0.0",
  "description": "Ein Tool für mein Portfolio mit farbigen Ausgaben",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": ["portfolio", "node", "cli"],
  "author": "Dein Name",
  "license": "ISC",
  "dependencies": {
    "chalk": "^5.3.0"
  }
}
```

**Neu:** Das Feld `dependencies` enthält jetzt `chalk`!

**Versionsnummer verstehen:**
- `^5.3.0` = Version 5.3.0 oder höher (aber nicht 6.0.0)
- `^` = Caret – erlaubt Updates für Minor und Patch, aber nicht für Major
- Mehr dazu: [Semantic Versioning](https://semver.org/)

### 2.4 ES6-Module aktivieren

Ab Chalk Version 5 musst du ES6-Module nutzen. Füge in `package.json` hinzu:

```json
{
  "name": "portfolio-tool",
  "version": "1.0.0",
  "type": "module",  // ← Diese Zeile hinzufügen!
  "description": "Ein Tool für mein Portfolio mit farbigen Ausgaben",
  // ... rest
}
```

### 2.5 chalk nutzen

Erstelle eine Datei **`index.js`**:

```javascript
// index.js - Portfolio Tool mit farbigen Ausgaben

// Chalk importieren (ES6-Modul)
import chalk from 'chalk';

// Titel ausgeben
console.log(chalk.blue.bold('\n=== Mein Portfolio-Tool ===\n'));

// Persönliche Informationen
console.log(chalk.cyan('Name:') + ' Max Muster');
console.log(chalk.cyan('Ausbildung:') + ' Informatiker/in EFZ Applikationsentwicklung');
console.log(chalk.cyan('Lehrjahr:') + ' 1. Lehrjahr bei BAND');

// Skills mit Farben
console.log(chalk.yellow('\n--- Meine Skills ---'));
console.log(chalk.green('✓ HTML & CSS'));
console.log(chalk.green('✓ JavaScript Grundlagen'));
console.log(chalk.green('✓ Git & Versionskontrolle'));
console.log(chalk.yellow('⟳ Node.js (in Arbeit)'));
console.log(chalk.yellow('⟳ Express.js (geplant)'));

// Kontakt
console.log(chalk.magenta('\n--- Kontakt ---'));
console.log(chalk.white('Email: max.muster@example.com'));
console.log(chalk.white('GitHub: github.com/maxmuster'));

// Erfolgs-Nachricht
console.log(chalk.bgGreen.black('\n SUCCESS ') + chalk.green(' Portfolio geladen!\n'));
```

**Programm ausführen:**

```bash
node index.js
```

Du siehst jetzt farbige Ausgaben im Terminal!

### 2.6 Verschiedene Chalk-Farben testen

Erstelle eine Datei **`farben-test.js`**:

```javascript
import chalk from 'chalk';

console.log(chalk.blue('Blau'));
console.log(chalk.red('Rot'));
console.log(chalk.green('Grün'));
console.log(chalk.yellow('Gelb'));
console.log(chalk.magenta('Magenta'));
console.log(chalk.cyan('Cyan'));
console.log(chalk.white('Weiss'));
console.log(chalk.gray('Grau'));

// Kombinationen
console.log(chalk.bold('Fett'));
console.log(chalk.italic('Kursiv'));
console.log(chalk.underline('Unterstrichen'));
console.log(chalk.bold.yellow('Fett und Gelb'));

// Hintergründe
console.log(chalk.bgRed.white(' FEHLER '));
console.log(chalk.bgGreen.black(' ERFOLG '));
console.log(chalk.bgYellow.black(' WARNUNG '));
console.log(chalk.bgBlue.white(' INFO '));
```

Ausführen:

```bash
node farben-test.js
```

---

## Teil 3: node_modules und .gitignore (5 Min)

### 3.1 Was ist node_modules?

Der Ordner `node_modules/` enthält alle installierten Pakete. Schaue in VS Code nach – der Ordner ist gross und enthält viele Unterordner!

**Wichtig:** `node_modules/` kann sehr gross werden (oft 100+ MB). Dieser Ordner gehört **NIEMALS** ins Git-Repository!

### 3.2 .gitignore erstellen

Erstelle eine Datei **`.gitignore`**:

```gitignore
# Dependencies
node_modules/

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Environment Variables
.env
.env.local

# OS Files
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
```

### 3.3 Warum node_modules nicht ins Git?

**Gründe:**
1. Extrem gross (kann mehrere hundert MB werden)
2. Kann jederzeit mit `npm install` neu heruntergeladen werden
3. Enthält kompilierte Binaries, die auf anderen Systemen nicht funktionieren
4. Macht das Repository langsam und unübersichtlich

**Wie andere Entwickler die Pakete bekommen:**
1. Repository klonen
2. `npm install` ausführen
3. NPM lädt alle Pakete aus `package.json` herunter

---

## Teil 4: NPM Scripts nutzen (10 Min)

### 4.1 Scripts definieren

In `package.json` kannst du eigene Befehle definieren. Erweitere den `scripts`-Bereich:

```json
{
  "name": "portfolio-tool",
  "version": "1.0.0",
  "type": "module",
  "description": "Ein Tool für mein Portfolio mit farbigen Ausgaben",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "farben": "node farben-test.js",
    "info": "echo 'Portfolio-Tool v1.0.0 von Dein Name'"
  },
  // ... rest
}
```

### 4.2 Scripts ausführen

```bash
# Script "start" ausführen
npm run start

# Script "farben" ausführen
npm run farben

# Script "info" ausführen
npm run info
```

**Spezialfall:** Das Script `start` kann ohne `run` ausgeführt werden:

```bash
npm start
```

### 4.3 Praktischer Nutzen

Scripts sind nützlich für:
- Häufig genutzte Befehle (z.B. `start`, `test`)
- Komplexe Befehle mit vielen Parametern
- Build-Prozesse (später mit Webpack, Vite, etc.)
- Automatisierung (z.B. Linting, Formatierung)

---

## Erfolgskriterien

- [ ] NPM-Projekt wurde mit `npm init` erstellt
- [ ] `package.json` existiert und enthält korrekte Informationen
- [ ] `chalk` wurde erfolgreich installiert
- [ ] `node_modules/` Ordner existiert
- [ ] `package-lock.json` wurde automatisch erstellt
- [ ] `"type": "module"` wurde in `package.json` hinzugefügt
- [ ] `index.js` nutzt chalk und zeigt farbige Ausgaben
- [ ] `.gitignore` wurde erstellt und enthält `node_modules/`
- [ ] Mindestens 2 NPM-Scripts wurden definiert und getestet
- [ ] Du verstehst, warum `node_modules/` nicht ins Git gehört

## Tipps

- **NPM-Befehle:**
  - `npm list` = Zeigt installierte Pakete
  - `npm outdated` = Zeigt veraltete Pakete
  - `npm update` = Aktualisiert Pakete
  - `npm uninstall <paket>` = Entfernt ein Paket
- **Pakete suchen:** [npmjs.com](https://www.npmjs.com) – die offizielle NPM-Registry
- **package-lock.json:** Diese Datei **sollte** ins Git, da sie exakte Versionen speichert
- **Fehler beheben:**
  - Löschen von `node_modules/` und `package-lock.json`, dann `npm install` erneut ausführen
  - Cache leeren: `npm cache clean --force`

## Reflexionsfragen

1. Warum nutzen wir externe Pakete wie `chalk` statt alles selbst zu programmieren?
2. Was ist der Unterschied zwischen `package.json` und `package-lock.json`?
3. Teste: Lösche den Ordner `node_modules/` und führe `npm install` aus. Was passiert?
4. Schaue dir die [chalk-Dokumentation](https://github.com/chalk/chalk) auf GitHub an. Welche weiteren Styling-Optionen gibt es?
5. Vergleiche die Grösse von `node_modules/` mit der Grösse von `package.json`. Was fällt auf?

## Weiterführende Links

- [NPM Dokumentation](https://docs.npmjs.com/) – Offizielle Dokumentation
- [package.json Felder](https://docs.npmjs.com/cli/v10/configuring-npm/package-json) – Alle verfügbaren Felder
- [Semantic Versioning](https://semver.org/) – Versionsnummern verstehen
- [Chalk auf NPM](https://www.npmjs.com/package/chalk) – Chalk-Paket-Seite
- [npmtrends.com](https://npmtrends.com/) – Vergleiche beliebte Pakete

---

**Geschätzte Zeit:** 40 Minuten
