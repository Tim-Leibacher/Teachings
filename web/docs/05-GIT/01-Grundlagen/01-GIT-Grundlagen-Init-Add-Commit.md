# Auftrag 1: Erstes Git-Repository erstellen

## Ziel

Du initialisierst dein erstes Git-Repository und lernst die grundlegenden Befehle `git init`, `git status`, `git add` und `git commit` kennen. Du verstehst, warum Versionskontrolle wichtig ist und kannst deinen ersten Commit erstellen.

## Beschreibung

Git ist das Standard-Versionskontrollsystem in der Softwareentwicklung. Fast alle Entwickler weltweit nutzen Git täglich, um ihre Code-Änderungen zu verfolgen, im Team zu arbeiten und professionelle Workflows zu etablieren. In diesem Auftrag machst du die ersten Schritte und erstellst dein erstes Git-Repository für dein Portfolio-Projekt.

---

### Teil 1: Git überprüfen und Portfolio vorbereiten (10 Min)

**1.1 Git-Installation überprüfen**

Öffne das Terminal (Windows: Git Bash, Mac: Terminal) und prüfe, ob Git installiert ist:

```bash
git --version
```

**Erwartete Ausgabe:**
```
git version 2.41.0
```

Falls Git nicht installiert ist:
- Lade Git herunter: [git-scm.com](https://git-scm.com/)
- Installiere Git mit den Standard-Einstellungen
- Starte das Terminal neu und prüfe erneut

**1.2 Git konfigurieren**

Beim ersten Mal musst du deinen Namen und E-Mail-Adresse konfigurieren. Diese Infos erscheinen in jedem Commit:

```bash
# Deinen Namen setzen
git config --global user.name "Dein Name"

# Deine E-Mail setzen
git config --global user.email "deine.email@example.com"

# Konfiguration überprüfen
git config --list
```

**Wichtig:** Nutze deine echte E-Mail-Adresse, die du auch für GitHub/GitLab verwenden wirst!

**1.3 In den Portfolio-Ordner navigieren**

```bash
# Auf dem Desktop (passe den Pfad an!)
cd Desktop/mein-portfolio

# Oder direkt mit vollständigem Pfad
cd /Users/username/Desktop/mein-portfolio

# Dateien anzeigen
ls
```

**Erwartete Ausgabe:**
```
index.html
styles.css
script.js
images/
```

---

### Teil 2: Git-Repository initialisieren (10 Min)

**2.1 Repository erstellen**

```bash
# Git-Repository initialisieren
git init
```

**Erwartete Ausgabe:**
```
Initialized empty Git repository in /Users/username/Desktop/mein-portfolio/.git/
```

**Was passiert hier?**
- Git erstellt einen versteckten Ordner `.git/` in deinem Projekt
- In diesem Ordner speichert Git alle Versionsinformationen
- Dein Projekt ist jetzt ein Git-Repository!

**2.2 Versteckten .git-Ordner sichtbar machen (Optional)**

In VS Code:
1. Öffne die Einstellungen (`Cmd/Ctrl + ,`)
2. Suche nach "files.exclude"
3. Entferne den Eintrag für `**/.git`
4. Jetzt siehst du den `.git/` Ordner im Explorer

**Wichtig:** Lösche niemals den `.git/` Ordner – sonst ist deine komplette Git-Historie weg!

**2.3 Status überprüfen**

```bash
# Status des Repositories anzeigen
git status
```

**Erwartete Ausgabe:**
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

**Was bedeutet das?**
- **On branch main:** Du bist auf dem Haupt-Branch (mehr dazu in späteren Videos)
- **No commits yet:** Noch kein Commit erstellt
- **Untracked files:** Git kennt diese Dateien noch nicht
- **"use git add":** Git sagt dir, was als nächstes zu tun ist

---

### Teil 3: Dateien zur Staging Area hinzufügen (10 Min)

Die **Staging Area** ist wie eine Vorbereitungszone. Du sagst Git, welche Änderungen du im nächsten Commit festhalten möchtest.

**3.1 Einzelne Datei hinzufügen**

```bash
# Eine einzelne Datei zur Staging Area
git add index.html

# Status checken
git status
```

**Erwartete Ausgabe:**
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html

Untracked files:
        styles.css
        script.js
        images/
```

**3.2 Mehrere Dateien hinzufügen**

```bash
# Mehrere Dateien gleichzeitig
git add styles.css script.js

# Status checken
git status
```

**3.3 Alle Dateien hinzufügen (empfohlen)**

```bash
# Alle geänderten und neuen Dateien
git add .

# Status checken
git status
```

**Erwartete Ausgabe:**
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html
        new file:   styles.css
        new file:   script.js
        new file:   images/logo.png
```

**Erklärung:**
- `git add .` = Füge alle Dateien im aktuellen Ordner hinzu
- Der Punkt `.` bedeutet "aktueller Ordner"
- Alle Dateien sind jetzt in der Staging Area → Bereit für den Commit

---

### Teil 4: Ersten Commit erstellen (10 Min)

Ein **Commit** ist wie ein Snapshot deines Projekts. Du speicherst den aktuellen Zustand dauerhaft in der Git-Historie.

**4.1 Commit mit Nachricht erstellen**

```bash
# Commit mit aussagekräftiger Nachricht
git commit -m "Initiales Portfolio mit HTML, CSS und JavaScript"
```

**Erwartete Ausgabe:**
```
[main (root-commit) a3f5e21] Initiales Portfolio mit HTML, CSS und JavaScript
 4 files changed, 156 insertions(+)
 create mode 100644 index.html
 create mode 100644 styles.css
 create mode 100644 script.js
 create mode 100644 images/logo.png
```

**Was bedeutet das?**
- **[main (root-commit) a3f5e21]:** 
  - Branch: main
  - Root-Commit: Dein allererster Commit
  - Hash: a3f5e21 (eindeutige ID für diesen Commit)
- **4 files changed:** 4 Dateien wurden hinzugefügt
- **156 insertions:** 156 Zeilen Code hinzugefügt

**4.2 Gute Commit-Nachrichten schreiben**

**Best Practices:**

✅ Gute Commit-Nachrichten:
- "Initiales Portfolio mit HTML, CSS und JavaScript"
- "Navigation mit Links zur Projekt-Sektion hinzugefügt"
- "Responsive Design für mobile Geräte implementiert"
- "Kontaktformular mit Validierung erstellt"
- "Fehler in der Navigation korrigiert"

❌ Schlechte Commit-Nachrichten:
- "Update"
- "Fix"
- "Änderungen"
- "asdfgh"
- "Stuff"

**Regeln für gute Commit-Nachrichten:**
1. Kurz und präzise (max. 50 Zeichen für die erste Zeile)
2. Beginne mit einem Verb (z.B. "Füge hinzu", "Ändere", "Korrigiere")
3. Beschreibe WAS du geändert hast, nicht WIE
4. Nutze Präsens ("Füge hinzu" statt "Hinzugefügt")
5. Keine Emojis in professionellen Projekten

---

### Teil 5: Historie anzeigen (5 Min)

Mit `git log` siehst du die komplette Commit-Historie.

**5.1 Vollständige Historie**

```bash
# Alle Commits mit Details
git log
```

**Erwartete Ausgabe:**
```
commit a3f5e21b8c9d4f6e3a2b1c0d9e8f7a6b5c4d3e2f
Author: Tim Leibacher <tim.leibacher@band.ch>
Date:   Mon Nov 25 14:23:10 2025 +0100

    Initiales Portfolio mit HTML, CSS und JavaScript
```

**5.2 Kompakte Ansicht**

```bash
# Nur eine Zeile pro Commit
git log --oneline
```

**Erwartete Ausgabe:**
```
a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

**5.3 Aus dem Log-Modus raus**

Wenn die Ausgabe länger ist, öffnet Git einen Pager (wie `less`):
- Scrollen: Pfeiltasten
- Beenden: Taste `q`

---

## Erfolgskriterien

- [ ] Git ist installiert und konfiguriert (`git --version` funktioniert)
- [ ] Dein Name und E-Mail sind in Git konfiguriert (`git config --list`)
- [ ] Ein Git-Repository wurde initialisiert (`git init`)
- [ ] Der `.git/` Ordner existiert im Projekt
- [ ] Alle Portfolio-Dateien wurden zur Staging Area hinzugefügt (`git add .`)
- [ ] Ein Commit mit aussagekräftiger Nachricht wurde erstellt
- [ ] `git status` zeigt "nothing to commit, working tree clean"
- [ ] `git log` zeigt deinen ersten Commit

## Tipps

- **`git status` ist dein bester Freund** – nutze es oft, um zu sehen, was gerade passiert
- Committe oft, in kleinen logischen Einheiten (z.B. nach jeder funktionierenden Änderung)
- Nutze `git add .` um alle Änderungen gleichzeitig hinzuzufügen
- **Shortcut:** In VS Code kannst du die Git-Integration nutzen (Quellcodeverwaltung-Tab)
- Falls du einen Fehler machst: `git reset HEAD` entfernt Dateien aus der Staging Area
- **Profitipp:** Erstelle eine `.gitignore`-Datei für Dateien, die Git ignorieren soll (kommt in späteren Aufträgen)

## Reflexionsfragen

1. Warum ist Versionskontrolle wichtig? Nenne drei Vorteile von Git.
2. Was ist der Unterschied zwischen der Staging Area und einem Commit?
3. Teste: Ändere eine Datei (z.B. füge einen Absatz in index.html hinzu) und führe `git status` aus. Was siehst du?
4. Was passiert, wenn du `git add .` zweimal hintereinander ausführst?
5. Recherchiere: Was ist der Unterschied zwischen `git init` und `git clone`?

## Weiterführende Links

- [Git Dokumentation – Getting Started](https://git-scm.com/book/de/v2/Erste-Schritte-Git-Grundlagen)
- [GitHub Git Cheat Sheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf)
- [Learn Git Branching (Interaktiv)](https://learngitbranching.js.org/)
- [Oh My Git! – Git als Spiel lernen](https://ohmygit.org/)
- [Visualizing Git – Siehe was Git macht](https://git-school.github.io/visualizing-git/)

---

**⏱️ Geschätzte Zeit:** 45-50 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 lernst du, wie du weitere Änderungen trackst und die Git-Historie nutzt!
