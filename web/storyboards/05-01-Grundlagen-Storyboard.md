# Storyboard: GIT – Grundlagen (Init, Add, Commit)

**Modul:** GIT  
**Thema:** Grundlagen (Init, Add, Commit)  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Geschätzte Videolänge:** 8-10 Minuten  
**Autor:** Tim Leibacher

---

## Video-Übersicht

**Lernziele:**
- Verstehen, warum Versionskontrolle wichtig ist
- Ein Git-Repository mit `git init` initialisieren
- Dateien mit `git add` zur Staging Area hinzufügen
- Änderungen mit `git commit` festhalten
- Den Status mit `git status` und die Historie mit `git log` überprüfen

**Benötigte Ressourcen:**
- Terminal (Git Bash auf Windows / Terminal auf Mac)
- VS Code mit Portfolio-Projekt
- Git installiert (Überprüfung mit `git --version`)

---

## Szene 1: Intro & Problem ohne Versionskontrolle (1 Min.)

### Sprechertext
"Willkommen! Stell dir vor, du arbeitest an deinem Portfolio. Du änderst Code, etwas funktioniert nicht mehr, und du möchtest zur vorherigen Version zurück – aber du hast keine Kopie gespeichert. Oder du arbeitest im Team, und zwei Personen ändern dieselbe Datei gleichzeitig. Chaos! Genau hier hilft Git: Ein Versionskontrollsystem, das jede Änderung dokumentiert, dir erlaubt zurückzugehen und ermöglicht professionelle Zusammenarbeit. Fast alle Entwickler nutzen Git täglich. In diesem Video lernst du die drei wichtigsten Befehle: init, add und commit."

### Bildschirmdarstellung
- Zeige Ordner mit Portfolio-Dateien
- Animation: Datei wird bearbeitet → durcheinandergebracht → Fragezeichen erscheint
- Zeige dann Git-Logo mit Text-Overlay: **"Git = Zeitmaschine für deinen Code"**

### Hinweise zur Animation
- Nutze BAND-Farben (Türkis #29786A, Blau #376B8C) für Text-Overlays
- Fade-In für Git-Logo

---

## Szene 2: Was ist Git? (30 Sek.)

### Sprechertext
"Git ist ein dezentrales Versionskontrollsystem. Das bedeutet: Jeder Entwickler hat die komplette Projekt-Historie lokal auf seinem Computer. Du kannst offline arbeiten und später deine Änderungen mit anderen synchronisieren. Git wurde von Linus Torvalds entwickelt – dem gleichen Mann, der Linux erschuf. Heute ist Git Standard in der Softwareentwicklung."

### Bildschirmdarstellung
- Zeige Grafik: 
  - Entwickler-Icon → Lokales Git-Repository (auf dem Computer)
  - Pfeil zu → GitHub/GitLab (Online-Repository)
- Text-Overlay: **"Lokal arbeiten → Online synchronisieren"**

### Hinweise
- Nutze einfache Icons für besseres Verständnis
- Animation: Pfeile erscheinen nacheinander

---

## Szene 3: Git installieren & überprüfen (30 Sek.)

### Sprechertext
"Bevor wir starten: Überprüfe, ob Git installiert ist. Öffne das Terminal und gib `git --version` ein. Wenn eine Versionsnummer erscheint, ist Git installiert. Falls nicht, lade Git von git-scm.com herunter und installiere es. Auf dem Mac ist Git oft schon vorinstalliert."

### Bildschirmdarstellung
- Terminal-Fenster zeigen
- Tippe live: `git --version`
- Ausgabe erscheint: `git version 2.41.0`
- Text-Overlay: **"Git installiert ✓"**

### Hinweise
- Zeige Download-Link: [git-scm.com](https://git-scm.com)
- Nutze grossen Font im Terminal für bessere Lesbarkeit

---

## Szene 4: Portfolio-Projekt vorbereiten (30 Sek.)

### Sprechertext
"Wir nutzen dein Portfolio-Projekt für dieses Tutorial. Öffne das Terminal und navigiere in deinen Portfolio-Ordner. Nutze dafür den Befehl `cd`, was für 'Change Directory' steht. Wenn du den Ordner auf dem Desktop hast, gibst du zum Beispiel `cd Desktop/mein-portfolio` ein. Mit `ls` kannst du dir die Dateien im Ordner anzeigen lassen."

### Bildschirmdarstellung
Terminal-Fenster mit folgenden Befehlen:

```bash
# In den Portfolio-Ordner wechseln
cd Desktop/mein-portfolio

# Inhalt anzeigen
ls
```

Ausgabe:
```
index.html
styles.css
script.js
images/
```

### Hinweise
- Zeige beide Betriebssysteme:
  - Windows: `cd Desktop\mein-portfolio`
  - Mac/Linux: `cd Desktop/mein-portfolio`
- VS Code parallel geöffnet zeigen (Split-Screen)

---

## Szene 5: Git-Repository initialisieren – `git init` (1 Min.)

### Sprechertext
"Jetzt initialisieren wir Git mit dem Befehl `git init`. Dieser Befehl erstellt einen versteckten Ordner namens `.git` in deinem Projekt. Hier speichert Git alle Versionsinformationen. Das musst du nur einmal pro Projekt machen. Wichtig: Führe `git init` nur im Hauptordner deines Projekts aus, nicht in Unterordnern."

### Bildschirmdarstellung
Terminal zeigen:

```bash
# Git-Repository initialisieren
git init
```

Ausgabe:
```
Initialized empty Git repository in /Users/username/Desktop/mein-portfolio/.git/
```

Dann VS Code zeigen:
- Datei-Explorer mit neuem `.git/` Ordner (versteckte Dateien einblenden)
- Highlight auf `.git/` Ordner

### Hinweise
- Erkläre, warum `.git` versteckt ist (Punkt am Anfang = versteckter Ordner)
- Warne: **Niemals den `.git/` Ordner löschen – sonst ist die komplette Historie weg!**

---

## Szene 6: Status überprüfen – `git status` (1 Min.)

### Sprechertext
"Mit `git status` siehst du den aktuellen Zustand deines Repositories. Dieser Befehl zeigt dir, welche Dateien geändert wurden, welche bereit zum Committen sind und welche noch nicht von Git verfolgt werden. `git status` ist dein wichtigstes Werkzeug – nutze es oft!"

### Bildschirmdarstellung
Terminal:

```bash
# Status anzeigen
git status
```

Ausgabe:
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html
        styles.css
        script.js
        images/

nothing added to commit but untracked files present (use "git add" to track)
```

Erkläre die Ausgabe:
- **Untracked files** = Git kennt diese Dateien noch nicht
- **"use git add"** = Git sagt uns, was wir als nächstes tun sollen

### Hinweise
- Highlight wichtige Teile der Ausgabe (farbige Markierungen)
- Nutze Pfeile, um auf wichtige Begriffe zu zeigen

---

## Szene 7: Dateien zur Staging Area hinzufügen – `git add` (1 Min. 30 Sek.)

### Sprechertext
"Mit `git add` fügst du Dateien zur sogenannten 'Staging Area' hinzu. Das ist wie eine Vorbereitungszone – du sagst Git, welche Änderungen du im nächsten Commit festhalten möchtest. Es gibt drei Varianten: `git add` mit einer einzelnen Datei, mit mehreren Dateien oder mit einem Punkt für alle Dateien. Schauen wir uns alle drei an."

### Bildschirmdarstellung
Terminal-Demo mit drei Varianten:

**Variante 1: Einzelne Datei**
```bash
# Eine einzelne Datei hinzufügen
git add index.html

# Status checken
git status
```

Ausgabe:
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html

Untracked files:
        styles.css
        script.js
        images/
```

**Variante 2: Mehrere Dateien**
```bash
# Mehrere Dateien gleichzeitig
git add styles.css script.js

# Status checken
git status
```

**Variante 3: Alle Dateien (am häufigsten)**
```bash
# Alle geänderten und neuen Dateien hinzufügen
git add .

# Status checken
git status
```

Ausgabe:
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html
        new file:   styles.css
        new file:   script.js
        new file:   images/logo.png
```

### Hinweise
- Zeige alle drei Varianten live im Terminal
- Erkläre: **"Der Punkt `.` bedeutet: alle Dateien im aktuellen Ordner"**
- Grafik einblenden: Arbeitsbereich → Staging Area → Repository

---

## Szene 8: Änderungen festhalten – `git commit` (2 Min.)

### Sprechertext
"Mit `git commit` speicherst du die Änderungen aus der Staging Area dauerhaft in der Git-Historie. Jeder Commit braucht eine aussagekräftige Nachricht, die beschreibt, was du geändert hast. Nutze dafür `-m` und schreibe die Nachricht in Anführungszeichen. Gute Commit-Nachrichten sind kurz, präzise und beginnen mit einem Verb."

### Bildschirmdarstellung
Terminal:

```bash
# Erster Commit mit Nachricht
git commit -m "Initiales Portfolio mit HTML, CSS und JavaScript"
```

Ausgabe:
```
[main (root-commit) a3f5e21] Initiales Portfolio mit HTML, CSS und JavaScript
 4 files changed, 156 insertions(+)
 create mode 100644 index.html
 create mode 100644 styles.css
 create mode 100644 script.js
 create mode 100644 images/logo.png
```

**Gute vs. Schlechte Commit-Nachrichten:**

Zeige Tabelle:

```
✅ Gute Commit-Nachrichten:
- "Initiales Portfolio mit HTML, CSS und JavaScript"
- "Navigation mit Links hinzugefügt"
- "Responsive Design für mobile Geräte implementiert"
- "Kontaktformular erstellt"

❌ Schlechte Commit-Nachrichten:
- "Update"
- "Fix"
- "asdfgh"
- "Stuff"
- "Änderungen gemacht"
```

### Hinweise
- Erkläre: Commits sind Snapshots des gesamten Projekts
- Best Practice: Committe oft, in kleinen logischen Einheiten
- Nutze Verben wie "Füge hinzu", "Ändere", "Entferne", "Korrigiere"

---

## Szene 9: Historie anzeigen – `git log` (1 Min.)

### Sprechertext
"Mit `git log` siehst du die komplette Commit-Historie. Jeder Commit hat einen eindeutigen Hash, einen Autor, ein Datum und die Commit-Nachricht. Das ist extrem nützlich, um nachzuvollziehen, wer wann was geändert hat. Für eine kompaktere Ansicht nutze `git log --oneline`."

### Bildschirmdarstellung
Terminal:

```bash
# Vollständige Historie
git log
```

Ausgabe:
```
commit a3f5e21b8c9d4f6e3a2b1c0d9e8f7a6b5c4d3e2f
Author: Tim Leibacher <tim.leibacher@band.ch>
Date:   Mon Nov 25 14:23:10 2025 +0100

    Initiales Portfolio mit HTML, CSS und JavaScript
```

Dann:

```bash
# Kompakte Ansicht
git log --oneline
```

Ausgabe:
```
a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

### Hinweise
- Erkläre den Commit-Hash (eindeutige ID)
- Zeige, wie man mit `q` aus dem Log-Modus rauskommt
- Optional: `git log --graph --all` für Branching (Vorschau auf nächstes Video)

---

## Szene 10: Workflow-Zusammenfassung & Praxis (1 Min.)

### Sprechertext
"Fassen wir den Git-Workflow zusammen: Erst initialisierst du Git mit `git init`, dann fügst du Dateien mit `git add` zur Staging Area hinzu, und schliesslich speicherst du mit `git commit` die Änderungen. Nutze `git status`, um den aktuellen Zustand zu checken, und `git log`, um die Historie zu sehen. Das sind die fünf wichtigsten Befehle für den täglichen Gebrauch. In den Aufträgen wirst du diesen Workflow Schritt für Schritt an deinem Portfolio üben. Viel Erfolg!"

### Bildschirmdarstellung
Animierte Grafik mit Git-Workflow:

```
┌─────────────────────────────────────────────┐
│  Git-Workflow                               │
├─────────────────────────────────────────────┤
│                                             │
│  1. git init       → Repository erstellen   │
│  2. (Dateien ändern)                        │
│  3. git status     → Status checken         │
│  4. git add .      → Zur Staging Area       │
│  5. git commit -m  → Änderungen speichern   │
│  6. git log        → Historie anzeigen      │
│                                             │
│  → Wiederhole Schritte 2-5 bei Änderungen  │
└─────────────────────────────────────────────┘
```

Checkliste einblenden:
```
✅ git init einmal pro Projekt
✅ git status oft nutzen
✅ git add . für alle Änderungen
✅ git commit -m mit guter Nachricht
✅ Committe oft, in kleinen Schritten
```

### Hinweise
- Fade-Out mit BAND-Gradient-Hintergrund
- Call-to-Action: "Jetzt selbst ausprobieren!"

---

## Zusatzmaterialien für Video-Produktion

### Terminal-Setup für saubere Aufnahmen

**Empfohlene Einstellungen:**
- Schriftgrösse: 18-20pt
- Font: Monospace (z.B. Consolas, Monaco, Fira Code)
- Farbschema: Hell (für bessere Lesbarkeit)
- Fenstergrösse: 120x30 Zeichen

### Demo-Dateien für Video

**Projekt-Struktur vor Git:**
```
mein-portfolio/
├── index.html
├── styles.css
├── script.js
└── images/
    └── logo.png
```

**Beispiel index.html (stark vereinfacht für Demo):**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mein Portfolio</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Mein Portfolio</h1>
    </header>
    <main>
        <p>Willkommen auf meiner Portfolio-Seite!</p>
    </main>
    <script src="script.js"></script>
</body>
</html>
```

### Häufige Fehler & Lösungen (für Video erwähnen)

| Problem | Lösung |
|---------|--------|
| `git: command not found` | Git ist nicht installiert → git-scm.com |
| `.git` Ordner versehentlich gelöscht | Keine Rettung möglich – git init neu starten |
| Commit ohne Nachricht | Git öffnet Vi-Editor → `:q!` zum Beenden |
| Falsche Commit-Nachricht | `git commit --amend -m "Neue Nachricht"` |

### Weiterführende Ressourcen (am Ende erwähnen)

- [Git Dokumentation](https://git-scm.com/doc)
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Learn Git Branching](https://learngitbranching.js.org/) – Interaktives Tutorial
- [Oh My Git!](https://ohmygit.org/) – Git als Spiel lernen

---

## Technische Hinweise für Videobearbeitung

- Nutze BAND Corporate Design (Aptos Font, Farben: #376B8C, #29786A, Orange)
- Screen-Recording mit 1920x1080 Auflösung
- Terminal und VS Code nebeneinander (Split-Screen)
- Cursor-Highlights für wichtige Befehle
- Text-Overlays für Key-Takeaways
- Background-Musik: Subtil, nicht ablenkend
- Untertitel einbauen (für Barrierefreiheit)

---

**Ende des Storyboards**
