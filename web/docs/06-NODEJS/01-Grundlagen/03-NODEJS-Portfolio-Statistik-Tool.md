# Auftrag 3: Portfolio-Statistik-Tool mit mehreren Paketen

## Ziel

Du baust ein interaktives Portfolio-Tool, das mehrere NPM-Pakete kombiniert. Du lernst, wie man mit verschiedenen Paketen arbeitet, Dateien analysiert und Statistiken berechnet. Das Tool zeigt deine Lernfortschritte in einer übersichtlichen, farbigen Ausgabe.

## Beschreibung

In diesem Auftrag kombinierst du mehrere NPM-Pakete zu einem praktischen Tool. Du nutzt `chalk` für farbige Ausgaben, `inquirer` für interaktive Benutzereingaben und das eingebaute `fs`-Modul für Dateizugriff. Das Ziel ist ein Tool, das deine Portfolio-Dateien analysiert und Statistiken anzeigt – z.B. wie viele Zeilen Code du schon geschrieben hast.

**Geschätzte Zeit:** 60 Minuten

---

## Teil 1: Projekt vorbereiten und Pakete installieren (10 Min)

### 1.1 Neues Projekt erstellen

```bash
# Neuen Ordner erstellen
mkdir portfolio-stats
cd portfolio-stats

# NPM initialisieren
npm init -y

# ES6-Module aktivieren
```

Öffne `package.json` und füge hinzu:

```json
{
  "name": "portfolio-stats",
  "version": "1.0.0",
  "type": "module",
  // ... rest
}
```

### 1.2 Benötigte Pakete installieren

Wir nutzen drei Pakete:
1. **chalk** – Farbige Terminal-Ausgaben
2. **inquirer** – Interaktive Menüs und Eingaben
3. **ora** – Lade-Animationen

```bash
# Alle Pakete auf einmal installieren
npm install chalk inquirer ora
```

**Erwartete Ausgabe:**
```
added 15 packages, and audited 16 packages in 3s
found 0 vulnerabilities
```

### 1.3 package.json prüfen

Öffne `package.json` – die Dependencies wurden hinzugefügt:

```json
{
  "dependencies": {
    "chalk": "^5.3.0",
    "inquirer": "^9.2.12",
    "ora": "^8.0.1"
  }
}
```

---

## Teil 2: Basis-Struktur erstellen (15 Min)

### 2.1 Hauptdatei erstellen

Erstelle **`stats.js`**:

```javascript
// stats.js - Portfolio-Statistik-Tool
// Zeigt Statistiken über deine Portfolio-Dateien

import chalk from 'chalk';
import inquirer from 'inquirer';
import ora from 'ora';
import fs from 'fs';
import path from 'path';

// Banner anzeigen
function zeigeBanner() {
    console.clear();
    console.log(chalk.blue.bold('\n╔════════════════════════════════════════╗'));
    console.log(chalk.blue.bold('║   Portfolio-Statistik-Tool v1.0      ║'));
    console.log(chalk.blue.bold('╚════════════════════════════════════════╝\n'));
}

// Hauptfunktion
async function main() {
    zeigeBanner();
    
    console.log(chalk.cyan('Willkommen! Dieses Tool analysiert deine Portfolio-Dateien.\n'));
    
    // Mehr Funktionen kommen hier hin...
}

// Programm starten
main();
```

**Test:**

```bash
node stats.js
```

Du solltest den Banner und die Willkommensnachricht sehen.

### 2.2 Interaktives Menü erstellen

Erweitere `stats.js`:

```javascript
// Nach zeigeBanner()...

async function zeigeMenu() {
    const antworten = await inquirer.prompt([
        {
            type: 'list',
            name: 'aktion',
            message: 'Was möchtest du tun?',
            choices: [
                '📊 Statistiken anzeigen',
                '📁 Dateien auflisten',
                '🔍 Bestimmte Datei analysieren',
                '❌ Beenden'
            ]
        }
    ]);
    
    return antworten.aktion;
}

// In main() nach der Willkommensnachricht:
async function main() {
    zeigeBanner();
    console.log(chalk.cyan('Willkommen! Dieses Tool analysiert deine Portfolio-Dateien.\n'));
    
    let beenden = false;
    
    while (!beenden) {
        const aktion = await zeigeMenu();
        
        switch (aktion) {
            case '📊 Statistiken anzeigen':
                console.log(chalk.green('\nStatistiken werden geladen...\n'));
                break;
            case '📁 Dateien auflisten':
                console.log(chalk.green('\nDateien werden aufgelistet...\n'));
                break;
            case '🔍 Bestimmte Datei analysieren':
                console.log(chalk.green('\nDatei-Analyse...\n'));
                break;
            case '❌ Beenden':
                console.log(chalk.yellow('\nAuf Wiedersehen! 👋\n'));
                beenden = true;
                break;
        }
        
        if (!beenden) {
            await inquirer.prompt([{
                type: 'input',
                name: 'weiter',
                message: 'Drücke Enter um fortzufahren...'
            }]);
        }
    }
}

main();
```

**Test:** Jetzt hast du ein interaktives Menü!

---

## Teil 3: Dateien analysieren (20 Min)

### 3.1 Funktion für Datei-Statistiken

Füge folgende Funktionen hinzu:

```javascript
// Datei-Informationen sammeln
function analysiereDatei(dateipfad) {
    const stats = fs.statSync(dateipfad);
    const inhalt = fs.readFileSync(dateipfad, 'utf-8');
    
    // Zeilen zählen
    const zeilen = inhalt.split('\n').length;
    
    // Zeichen zählen (mit und ohne Leerzeichen)
    const zeichenMitLZ = inhalt.length;
    const zeichenOhneLZ = inhalt.replace(/\s/g, '').length;
    
    // Wörter zählen
    const woerter = inhalt.trim().split(/\s+/).length;
    
    // Code-Zeilen vs. Kommentare vs. Leerzeilen (vereinfacht für JS/HTML/CSS)
    const leerzeilen = (inhalt.match(/^\s*$/gm) || []).length;
    const kommentare = (inhalt.match(/\/\/.*|\/\*[\s\S]*?\*\//g) || []).length;
    
    return {
        name: path.basename(dateipfad),
        pfad: dateipfad,
        groesse: stats.size,
        zeilen: zeilen,
        leerzeilen: leerzeilen,
        codezeilen: zeilen - leerzeilen,
        woerter: woerter,
        zeichen: zeichenMitLZ,
        zeichenOhneLZ: zeichenOhneLZ,
        erstelltAm: stats.birthtime,
        geaendertAm: stats.mtime
    };
}

// Dateien im aktuellen Ordner finden
function findePortfoliodateien() {
    const dateien = [];
    const erlaubteEndungen = ['.html', '.css', '.js', '.json', '.md'];
    
    try {
        const items = fs.readdirSync('.');
        
        for (const item of items) {
            const stats = fs.statSync(item);
            
            if (stats.isFile()) {
                const ext = path.extname(item);
                if (erlaubteEndungen.includes(ext)) {
                    dateien.push(item);
                }
            }
        }
    } catch (error) {
        console.log(chalk.red('Fehler beim Lesen der Dateien:', error.message));
    }
    
    return dateien;
}
```

### 3.2 Statistiken anzeigen

Erweitere die Menü-Optionen:

```javascript
// In der switch-Anweisung:

case '📊 Statistiken anzeigen':
    await zeigeStatistiken();
    break;

// Neue Funktion:
async function zeigeStatistiken() {
    const spinner = ora('Dateien werden analysiert...').start();
    
    // Kurze Verzögerung für Effekt
    await new Promise(resolve => setTimeout(resolve, 800));
    
    const dateien = findePortfoliodateien();
    
    if (dateien.length === 0) {
        spinner.fail('Keine Portfolio-Dateien gefunden!');
        return;
    }
    
    spinner.succeed(`${dateien.length} Dateien gefunden!`);
    
    console.log(chalk.blue.bold('\n📊 Portfolio-Statistiken\n'));
    console.log(chalk.gray('─'.repeat(60)));
    
    let gesamtZeilen = 0;
    let gesamtWoerter = 0;
    let gesamtGroesse = 0;
    
    for (const datei of dateien) {
        try {
            const info = analysiereDatei(datei);
            
            console.log(chalk.cyan(`\n📄 ${info.name}`));
            console.log(`   Zeilen: ${chalk.yellow(info.zeilen)} (${info.codezeilen} Code, ${info.leerzeilen} Leer)`);
            console.log(`   Wörter: ${chalk.yellow(info.woerter)}`);
            console.log(`   Zeichen: ${chalk.yellow(info.zeichen)}`);
            console.log(`   Grösse: ${chalk.yellow(Math.round(info.groesse / 1024))} KB`);
            
            gesamtZeilen += info.zeilen;
            gesamtWoerter += info.woerter;
            gesamtGroesse += info.groesse;
        } catch (error) {
            console.log(chalk.red(`   Fehler: ${error.message}`));
        }
    }
    
    console.log(chalk.gray('\n' + '─'.repeat(60)));
    console.log(chalk.green.bold('\n✨ Gesamt-Statistiken'));
    console.log(chalk.white(`   Dateien: ${chalk.yellow(dateien.length)}`));
    console.log(chalk.white(`   Zeilen: ${chalk.yellow(gesamtZeilen)}`));
    console.log(chalk.white(`   Wörter: ${chalk.yellow(gesamtWoerter)}`));
    console.log(chalk.white(`   Grösse: ${chalk.yellow(Math.round(gesamtGroesse / 1024))} KB`));
    console.log(chalk.gray('─'.repeat(60) + '\n'));
}
```

---

## Teil 4: Einzelne Datei analysieren (15 Min)

### 4.1 Datei-Auswahl implementieren

```javascript
// In der switch-Anweisung:

case '🔍 Bestimmte Datei analysieren':
    await analysiereEinzelneDatei();
    break;

// Neue Funktion:
async function analysiereEinzelneDatei() {
    const dateien = findePortfoliodateien();
    
    if (dateien.length === 0) {
        console.log(chalk.red('\n❌ Keine Dateien gefunden!\n'));
        return;
    }
    
    const antwort = await inquirer.prompt([
        {
            type: 'list',
            name: 'datei',
            message: 'Welche Datei möchtest du analysieren?',
            choices: dateien
        }
    ]);
    
    const spinner = ora('Datei wird analysiert...').start();
    await new Promise(resolve => setTimeout(resolve, 500));
    
    try {
        const info = analysiereDatei(antwort.datei);
        spinner.succeed('Analyse abgeschlossen!');
        
        console.log(chalk.blue.bold(`\n🔍 Detaillierte Analyse: ${info.name}\n`));
        console.log(chalk.gray('─'.repeat(60)));
        
        console.log(chalk.cyan('\n📝 Inhalt:'));
        console.log(`   Zeilen gesamt: ${chalk.yellow(info.zeilen)}`);
        console.log(`   Code-Zeilen: ${chalk.green(info.codezeilen)}`);
        console.log(`   Leerzeilen: ${chalk.gray(info.leerzeilen)}`);
        console.log(`   Wörter: ${chalk.yellow(info.woerter)}`);
        console.log(`   Zeichen (mit Leerzeichen): ${chalk.yellow(info.zeichen)}`);
        console.log(`   Zeichen (ohne Leerzeichen): ${chalk.yellow(info.zeichenOhneLZ)}`);
        
        console.log(chalk.cyan('\n💾 Datei-Informationen:'));
        console.log(`   Grösse: ${chalk.yellow(info.groesse)} Bytes (${Math.round(info.groesse / 1024)} KB)`);
        console.log(`   Erstellt am: ${chalk.yellow(info.erstelltAm.toLocaleString('de-CH'))}`);
        console.log(`   Geändert am: ${chalk.yellow(info.geaendertAm.toLocaleString('de-CH'))}`);
        
        console.log(chalk.cyan('\n📊 Durchschnitte:'));
        console.log(`   Zeichen pro Zeile: ${chalk.yellow(Math.round(info.zeichen / info.zeilen))}`);
        console.log(`   Wörter pro Zeile: ${chalk.yellow(Math.round(info.woerter / info.zeilen))}`);
        
        console.log(chalk.gray('\n' + '─'.repeat(60) + '\n'));
    } catch (error) {
        spinner.fail('Fehler bei der Analyse!');
        console.log(chalk.red(`Fehler: ${error.message}\n`));
    }
}
```

### 4.2 Dateien auflisten

```javascript
// In der switch-Anweisung:

case '📁 Dateien auflisten':
    listeDateien();
    break;

// Neue Funktion:
function listeDateien() {
    const dateien = findePortfoliodateien();
    
    if (dateien.length === 0) {
        console.log(chalk.red('\n❌ Keine Dateien gefunden!\n'));
        return;
    }
    
    console.log(chalk.blue.bold('\n📁 Portfolio-Dateien\n'));
    console.log(chalk.gray('─'.repeat(60)));
    
    dateien.forEach((datei, index) => {
        const stats = fs.statSync(datei);
        const groesse = Math.round(stats.size / 1024);
        const icon = datei.endsWith('.html') ? '🌐' :
                    datei.endsWith('.css') ? '🎨' :
                    datei.endsWith('.js') ? '⚡' :
                    datei.endsWith('.json') ? '📦' :
                    datei.endsWith('.md') ? '📝' : '📄';
        
        console.log(chalk.cyan(`${index + 1}. ${icon} ${datei}`) + chalk.gray(` (${groesse} KB)`));
    });
    
    console.log(chalk.gray('─'.repeat(60) + '\n'));
}
```

---

## Teil 5: NPM Script und Testen (10 Min)

### 5.1 Script hinzufügen

Öffne `package.json` und füge Scripts hinzu:

```json
{
  "scripts": {
    "start": "node stats.js",
    "stats": "node stats.js"
  }
}
```

### 5.2 Testdateien erstellen

Erstelle ein paar Test-Dateien im gleichen Ordner:

**test.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Test</title>
</head>
<body>
    <h1>Test-Seite</h1>
</body>
</html>
```

**test.css:**
```css
body {
    font-family: Arial;
    margin: 0;
    padding: 20px;
}

h1 {
    color: blue;
}
```

**test.js:**
```javascript
// Test-Datei
console.log('Hello World!');

function test() {
    return true;
}
```

### 5.3 Tool testen

```bash
npm start
```

**Teste alle Menü-Optionen:**
1. Statistiken anzeigen
2. Dateien auflisten
3. Einzelne Datei analysieren
4. Beenden

---

## Erfolgskriterien

- [ ] Projekt wurde mit `npm init` erstellt
- [ ] Pakete `chalk`, `inquirer` und `ora` wurden installiert
- [ ] `stats.js` wurde erstellt und funktioniert
- [ ] Interaktives Menü mit 4 Optionen funktioniert
- [ ] Statistiken werden korrekt angezeigt (Zeilen, Wörter, Grösse)
- [ ] Einzelne Dateien können analysiert werden
- [ ] Dateien werden aufgelistet mit Grössen-Angabe
- [ ] Lade-Animationen (ora) werden angezeigt
- [ ] NPM-Script `start` wurde definiert
- [ ] .gitignore wurde erstellt mit `node_modules/`

## Tipps

- **Fehlerbehandlung:** Nutze `try-catch` für Datei-Operationen
- **Async/Await:** Inquirer-Prompts sind asynchron – nutze `async`/`await`
- **Performance:** Bei vielen Dateien kann die Analyse langsam werden – zeige Lade-Animation
- **Erweiterungen:** 
  - Analysiere Unterordner rekursiv
  - Exportiere Statistiken als JSON oder CSV
  - Zeige Code-Komplexität an
  - Erkenne verschiedene Programmiersprachen

## Reflexionsfragen

1. Warum nutzen wir `async`/`await` für das Menü?
2. Was ist der Vorteil von `inquirer` gegenüber `prompt()` im Browser?
3. Teste: Erstelle eine sehr grosse Datei (z.B. 10.000 Zeilen). Wie lange dauert die Analyse?
4. Schaue dir die Dokumentation von `ora` an. Welche weiteren Spinner-Stile gibt es?
5. Wie könntest du das Tool erweitern, um auch Git-Statistiken anzuzeigen (Commits, Branches)?

## Weiterführende Links

- [Inquirer.js Dokumentation](https://github.com/SBoudrias/Inquirer.js) – Interaktive Eingaben
- [Ora Dokumentation](https://github.com/sindresorhus/ora) – Terminal-Spinner
- [Node.js fs Modul](https://nodejs.org/api/fs.html) – Dateisystem
- [Commander.js](https://github.com/tj/commander.js) – CLI-Tools erstellen
- [Yargs](https://yargs.js.org/) – Alternative für CLI-Argumente

---

**Geschätzte Zeit:** 60 Minuten
