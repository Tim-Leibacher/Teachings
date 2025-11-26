# Auftrag 4 (Optional): NPM-Paket veröffentlichen und globale CLI-Tools

## Ziel

Du lernst fortgeschrittene NPM-Konzepte kennen: Wie man eigene Pakete veröffentlicht, globale CLI-Tools erstellt und mit NPM-Scripts komplexe Workflows automatisiert. Dieser Auftrag ist für Lernende gedacht, die tiefer in das Node.js-Ökosystem einsteigen möchten.

## Beschreibung

Bis jetzt hast du NPM-Pakete installiert und genutzt. In diesem optionalen Auftrag gehst du den nächsten Schritt: Du erstellst dein eigenes NPM-Paket, das als globales CLI-Tool installiert werden kann. Du lernst, wie man mit `npx` arbeitet, wie man Binaries definiert und wie man Pakete lokal testet, bevor man sie veröffentlicht.

**Wichtig:** Dieser Auftrag ist optional und setzt gute Kenntnisse von Node.js und NPM voraus. Nimm dir Zeit und experimentiere!

**Geschätzte Zeit:** 90-120 Minuten

---

## Teil 1: Eigenes CLI-Tool erstellen (30 Min)

### 1.1 Projekt-Idee: Portfolio-Validator

Wir erstellen ein Tool, das Portfolio-Projekte auf häufige Probleme überprüft:
- Fehlt die README.md?
- Fehlt die .gitignore?
- Sind alle Links in HTML-Dateien gültig?
- Sind Bilder vorhanden, die in HTML referenziert werden?

### 1.2 Projekt initialisieren

```bash
# Neuen Ordner erstellen
mkdir portfolio-validator
cd portfolio-validator

# NPM initialisieren
npm init
```

**Wichtige Eingaben:**
```
package name: portfolio-validator
version: 1.0.0
description: Ein CLI-Tool zur Validierung von Portfolio-Projekten
entry point: index.js
keywords: portfolio, validator, cli, html
author: Dein Name
license: MIT
```

### 1.3 ES6-Module und Binary definieren

Öffne `package.json` und erweitere sie:

```json
{
  "name": "portfolio-validator",
  "version": "1.0.0",
  "description": "Ein CLI-Tool zur Validierung von Portfolio-Projekten",
  "main": "index.js",
  "type": "module",
  "bin": {
    "portfolio-check": "./cli.js"
  },
  "scripts": {
    "start": "node cli.js",
    "test": "node cli.js ."
  },
  "keywords": ["portfolio", "validator", "cli", "html"],
  "author": "Dein Name",
  "license": "MIT"
}
```

**Neu:** Das `bin`-Feld definiert den Befehl `portfolio-check`, der auf `cli.js` zeigt!

### 1.4 Pakete installieren

```bash
npm install chalk ora commander
```

- **chalk:** Farbige Ausgaben
- **ora:** Lade-Animationen
- **commander:** CLI-Argumente parsen

### 1.5 CLI-Einstiegspunkt erstellen

Erstelle **`cli.js`**:

```javascript
#!/usr/bin/env node

// cli.js - Portfolio-Validator CLI
// Validiert Portfolio-Projekte auf häufige Probleme

import { Command } from 'commander';
import chalk from 'chalk';
import ora from 'ora';
import { validatePortfolio } from './validator.js';

const program = new Command();

program
    .name('portfolio-check')
    .description('Validiert Portfolio-Projekte auf häufige Probleme')
    .version('1.0.0')
    .argument('[pfad]', 'Pfad zum Portfolio-Projekt', '.')
    .option('-v, --verbose', 'Zeige detaillierte Ausgaben')
    .option('-q, --quiet', 'Nur Fehler anzeigen')
    .action(async (pfad, options) => {
        console.log(chalk.blue.bold('\n🔍 Portfolio-Validator v1.0.0\n'));
        
        const spinner = ora('Projekt wird analysiert...').start();
        
        try {
            const ergebnisse = await validatePortfolio(pfad, options);
            spinner.succeed('Analyse abgeschlossen!');
            
            zeigeErgebnisse(ergebnisse, options);
        } catch (error) {
            spinner.fail('Fehler bei der Analyse!');
            console.error(chalk.red(`\n❌ ${error.message}\n`));
            process.exit(1);
        }
    });

program.parse();

function zeigeErgebnisse(ergebnisse, options) {
    console.log(chalk.gray('\n' + '─'.repeat(60)));
    
    // Erfolge
    if (ergebnisse.erfolge.length > 0 && !options.quiet) {
        console.log(chalk.green.bold('\n✅ Erfolge:'));
        ergebnisse.erfolge.forEach(erfolg => {
            console.log(chalk.green(`   ✓ ${erfolg}`));
        });
    }
    
    // Warnungen
    if (ergebnisse.warnungen.length > 0) {
        console.log(chalk.yellow.bold('\n⚠️  Warnungen:'));
        ergebnisse.warnungen.forEach(warnung => {
            console.log(chalk.yellow(`   ⚠ ${warnung}`));
        });
    }
    
    // Fehler
    if (ergebnisse.fehler.length > 0) {
        console.log(chalk.red.bold('\n❌ Fehler:'));
        ergebnisse.fehler.forEach(fehler => {
            console.log(chalk.red(`   ✗ ${fehler}`));
        });
    }
    
    // Zusammenfassung
    console.log(chalk.gray('\n' + '─'.repeat(60)));
    console.log(chalk.bold(`\n📊 Zusammenfassung:`));
    console.log(`   Erfolge: ${chalk.green(ergebnisse.erfolge.length)}`);
    console.log(`   Warnungen: ${chalk.yellow(ergebnisse.warnungen.length)}`);
    console.log(`   Fehler: ${chalk.red(ergebnisse.fehler.length)}`);
    
    if (ergebnisse.fehler.length === 0 && ergebnisse.warnungen.length === 0) {
        console.log(chalk.green.bold('\n🎉 Perfekt! Dein Portfolio hat alle Checks bestanden!\n'));
    } else {
        console.log(chalk.yellow('\n💡 Tipp: Behebe die Fehler und Warnungen für ein professionelles Portfolio.\n'));
    }
}
```

**Wichtig:** Die erste Zeile `#!/usr/bin/env node` ist der Shebang – sie sagt dem System, dass diese Datei mit Node.js ausgeführt werden soll.

### 1.6 Validator-Logik implementieren

Erstelle **`validator.js`**:

```javascript
// validator.js - Validierungs-Logik

import fs from 'fs';
import path from 'path';

export async function validatePortfolio(projektPfad, options) {
    const ergebnisse = {
        erfolge: [],
        warnungen: [],
        fehler: []
    };
    
    // Check 1: Existiert der Pfad?
    if (!fs.existsSync(projektPfad)) {
        ergebnisse.fehler.push(`Pfad existiert nicht: ${projektPfad}`);
        return ergebnisse;
    }
    
    // Check 2: README.md vorhanden?
    const readmePfad = path.join(projektPfad, 'README.md');
    if (fs.existsSync(readmePfad)) {
        ergebnisse.erfolge.push('README.md gefunden');
        
        // Check: README nicht leer?
        const readmeInhalt = fs.readFileSync(readmePfad, 'utf-8');
        if (readmeInhalt.trim().length < 50) {
            ergebnisse.warnungen.push('README.md ist sehr kurz (weniger als 50 Zeichen)');
        }
    } else {
        ergebnisse.fehler.push('README.md fehlt');
    }
    
    // Check 3: .gitignore vorhanden?
    const gitignorePfad = path.join(projektPfad, '.gitignore');
    if (fs.existsSync(gitignorePfad)) {
        ergebnisse.erfolge.push('.gitignore gefunden');
        
        // Check: node_modules ignoriert?
        const gitignoreInhalt = fs.readFileSync(gitignorePfad, 'utf-8');
        if (!gitignoreInhalt.includes('node_modules')) {
            ergebnisse.warnungen.push('.gitignore enthält kein "node_modules/"');
        }
    } else {
        ergebnisse.warnungen.push('.gitignore fehlt');
    }
    
    // Check 4: index.html vorhanden?
    const indexPfad = path.join(projektPfad, 'index.html');
    if (fs.existsSync(indexPfad)) {
        ergebnisse.erfolge.push('index.html gefunden');
        
        const htmlInhalt = fs.readFileSync(indexPfad, 'utf-8');
        
        // Check: DOCTYPE vorhanden?
        if (!htmlInhalt.includes('<!DOCTYPE html>')) {
            ergebnisse.warnungen.push('index.html: DOCTYPE fehlt');
        }
        
        // Check: Charset definiert?
        if (!htmlInhalt.includes('charset')) {
            ergebnisse.warnungen.push('index.html: Charset nicht definiert');
        }
        
        // Check: Title vorhanden?
        if (!htmlInhalt.match(/<title>.*<\/title>/)) {
            ergebnisse.warnungen.push('index.html: Title-Tag fehlt oder ist leer');
        }
        
        // Check: Meta Viewport für Responsive Design?
        if (!htmlInhalt.includes('viewport')) {
            ergebnisse.warnungen.push('index.html: Viewport-Meta-Tag fehlt (nicht responsive)');
        }
    } else {
        ergebnisse.fehler.push('index.html fehlt');
    }
    
    // Check 5: CSS-Datei vorhanden?
    const dateien = fs.readdirSync(projektPfad);
    const cssDatien = dateien.filter(datei => datei.endsWith('.css'));
    
    if (cssDatien.length > 0) {
        ergebnisse.erfolge.push(`${cssDatien.length} CSS-Datei(en) gefunden`);
    } else {
        ergebnisse.warnungen.push('Keine CSS-Dateien gefunden');
    }
    
    // Check 6: JavaScript-Datei vorhanden?
    const jsDatien = dateien.filter(datei => datei.endsWith('.js') && !datei.includes('node_modules'));
    
    if (jsDatien.length > 0) {
        ergebnisse.erfolge.push(`${jsDatien.length} JavaScript-Datei(en) gefunden`);
    } else {
        ergebnisse.warnungen.push('Keine JavaScript-Dateien gefunden');
    }
    
    // Check 7: package.json (falls Node.js-Projekt)
    const packagePfad = path.join(projektPfad, 'package.json');
    if (fs.existsSync(packagePfad)) {
        ergebnisse.erfolge.push('package.json gefunden (Node.js-Projekt)');
        
        const packageJson = JSON.parse(fs.readFileSync(packagePfad, 'utf-8'));
        
        // Check: Dependencies vorhanden?
        if (!packageJson.dependencies || Object.keys(packageJson.dependencies).length === 0) {
            ergebnisse.warnungen.push('package.json: Keine Dependencies definiert');
        }
        
        // Check: Scripts vorhanden?
        if (!packageJson.scripts || Object.keys(packageJson.scripts).length === 0) {
            ergebnisse.warnungen.push('package.json: Keine Scripts definiert');
        }
    }
    
    return ergebnisse;
}
```

---

## Teil 2: Tool lokal testen (20 Min)

### 2.1 Lokal verlinken

Mit `npm link` kannst du dein Paket global verfügbar machen, ohne es zu veröffentlichen:

```bash
# Im portfolio-validator Ordner
npm link
```

**Erwartete Ausgabe:**
```
added 1 package, and audited 4 packages in 1s
```

Jetzt kannst du `portfolio-check` überall im Terminal nutzen!

### 2.2 Tool testen

Erstelle einen Test-Ordner:

```bash
# Neuen Ordner für Test erstellen
mkdir ~/test-portfolio
cd ~/test-portfolio

# Basis-Dateien erstellen
echo "# Mein Portfolio" > README.md
echo "<!DOCTYPE html><html><head><meta charset='UTF-8'><title>Test</title></head><body><h1>Test</h1></body></html>" > index.html
echo "body { margin: 0; }" > style.css
echo "node_modules/" > .gitignore
```

Jetzt das Tool testen:

```bash
# Im test-portfolio Ordner
portfolio-check
```

Du solltest grüne Erfolgs-Meldungen sehen!

### 2.3 Verschiedene Szenarien testen

**Test 1: Ohne README**
```bash
rm README.md
portfolio-check
```

**Test 2: Mit --verbose Flag**
```bash
portfolio-check --verbose
```

**Test 3: Mit --quiet Flag**
```bash
portfolio-check --quiet
```

**Test 4: Anderen Pfad angeben**
```bash
portfolio-check ~/Projekte/mein-portfolio
```

### 2.4 Link entfernen

Wenn du das Tool nicht mehr global brauchst:

```bash
# Im portfolio-validator Ordner
npm unlink
```

---

## Teil 3: NPM-Paket vorbereiten (25 Min)

### 3.1 README.md für NPM erstellen

Erstelle im `portfolio-validator` Ordner eine **`README.md`**:

```markdown
# Portfolio-Validator

Ein CLI-Tool zur Validierung von Portfolio-Projekten für Lernende.

## Installation

```bash
npm install -g portfolio-validator
```

## Verwendung

```bash
# Aktuelles Verzeichnis prüfen
portfolio-check

# Bestimmtes Verzeichnis prüfen
portfolio-check /pfad/zum/projekt

# Mit Optionen
portfolio-check --verbose
portfolio-check --quiet
```

## Was wird geprüft?

- ✅ README.md vorhanden und nicht leer
- ✅ .gitignore vorhanden und enthält node_modules
- ✅ index.html vorhanden mit korrektem DOCTYPE
- ✅ CSS-Dateien vorhanden
- ✅ JavaScript-Dateien vorhanden
- ✅ package.json korrekt konfiguriert (falls vorhanden)

## Optionen

- `-v, --verbose`: Zeige detaillierte Ausgaben
- `-q, --quiet`: Nur Fehler anzeigen
- `-V, --version`: Zeige Version
- `-h, --help`: Zeige Hilfe

## Beispiel-Ausgabe

```
🔍 Portfolio-Validator v1.0.0

✅ Erfolge:
   ✓ README.md gefunden
   ✓ .gitignore gefunden
   ✓ index.html gefunden
   ✓ 1 CSS-Datei(en) gefunden

📊 Zusammenfassung:
   Erfolge: 4
   Warnungen: 0
   Fehler: 0

🎉 Perfekt! Dein Portfolio hat alle Checks bestanden!
```

## Lizenz

MIT
```

### 3.2 .npmignore erstellen

Erstelle **`.npmignore`** (ähnlich wie .gitignore, aber für NPM):

```gitignore
# Development files
node_modules/
test/
*.test.js

# Git
.git/
.gitignore

# Editor
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Logs
npm-debug.log*
```

### 3.3 LICENSE erstellen

Erstelle **`LICENSE`** (MIT-Lizenz):

```
MIT License

Copyright (c) 2025 Dein Name

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Teil 4: Paket veröffentlichen (Optional, 20 Min)

**Wichtig:** Dieser Teil ist optional und erfordert einen NPM-Account. Überlege dir gut, ob du dein Paket wirklich veröffentlichen möchtest.

### 4.1 NPM-Account erstellen

1. Gehe zu [npmjs.com](https://www.npmjs.com)
2. Klicke auf "Sign Up"
3. Erstelle einen Account (E-Mail, Username, Passwort)
4. Bestätige deine E-Mail-Adresse

### 4.2 NPM Login

```bash
npm login
```

Gib deine NPM-Zugangsdaten ein.

### 4.3 Paket-Name prüfen

Prüfe, ob der Name schon vergeben ist:

```bash
npm search portfolio-validator
```

Falls der Name schon existiert, ändere ihn in `package.json` (z.B. `@dein-username/portfolio-validator`).

### 4.4 Paket veröffentlichen

```bash
# Trockenlauf (ohne Veröffentlichung)
npm publish --dry-run

# Tatsächlich veröffentlichen
npm publish
```

**Gratulation!** Dein Paket ist jetzt auf NPM verfügbar!

### 4.5 Paket aktualisieren

Wenn du Änderungen vornimmst:

```bash
# Version erhöhen (automatisch)
npm version patch   # 1.0.0 → 1.0.1
npm version minor   # 1.0.0 → 1.1.0
npm version major   # 1.0.0 → 2.0.0

# Veröffentlichen
npm publish
```

---

## Teil 5: npx nutzen (15 Min)

### 5.1 Was ist npx?

`npx` ermöglicht es, NPM-Pakete auszuführen, ohne sie zu installieren. Das ist perfekt für CLI-Tools!

### 5.2 Eigenes Tool mit npx testen

```bash
# Tool ausführen ohne Installation
npx portfolio-validator

# Oder mit dem vollständigen Paket-Namen
npx @dein-username/portfolio-validator
```

### 5.3 Beliebte CLI-Tools mit npx

Teste einige bekannte Tools:

```bash
# Projekt-Generator
npx create-react-app my-app

# HTTP-Server
npx http-server

# JSON-Server (Mock-API)
npx json-server --watch db.json

# Code-Formatierung
npx prettier --write .

# Lizenz-Generator
npx license mit
```

---

## Erfolgskriterien

- [ ] CLI-Tool `portfolio-validator` wurde erstellt
- [ ] Tool kann mit `npm link` lokal getestet werden
- [ ] Commander.js wird für CLI-Argumente genutzt
- [ ] Mindestens 6 Validierungs-Checks sind implementiert
- [ ] README.md, LICENSE und .npmignore wurden erstellt
- [ ] Tool funktioniert mit verschiedenen Optionen (--verbose, --quiet)
- [ ] Du verstehst den Unterschied zwischen lokalem und globalem Paket
- [ ] Optional: Paket wurde auf NPM veröffentlicht
- [ ] Du kannst das Tool mit `npx` ausführen

## Tipps

- **Scoped Packages:** Mit `@username/paket-name` vermeidest du Namenskonflikte
- **Semver:** Nutze Semantic Versioning für Versionsnummern
- **Testen:** Teste dein Tool mit verschiedenen Projekten
- **Dokumentation:** Eine gute README ist entscheidend für Nutzer
- **npm unpublish:** Kann nur innerhalb von 72 Stunden nach Veröffentlichung genutzt werden

## Reflexionsfragen

1. Was ist der Unterschied zwischen `npm install` und `npm install -g`?
2. Warum braucht man einen Shebang (`#!/usr/bin/env node`) in CLI-Skripten?
3. Was macht `npm link` genau? Wie funktioniert es intern?
4. Schaue dir beliebte CLI-Tools auf NPM an (z.B. `eslint`, `prettier`). Was haben sie gemeinsam?
5. Wie könnte man das Tool erweitern, um auch Accessibility-Checks durchzuführen?

## Weiterführende Links

- [NPM CLI Dokumentation](https://docs.npmjs.com/cli/) – Alle NPM-Befehle
- [Commander.js](https://github.com/tj/commander.js) – CLI-Framework
- [Semantic Versioning](https://semver.org/) – Versionsnummern richtig nutzen
- [Creating Node.js Command Line Utilities](https://blog.npmjs.org/post/118810260230/building-a-simple-command-line-tool-with-npm) – NPM Blog
- [Awesome CLI Apps](https://github.com/agarrharr/awesome-cli-apps) – Inspiration

---

**Geschätzte Zeit:** 90-120 Minuten
