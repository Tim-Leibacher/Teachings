# Auftrag 4 (Optional): .gitignore und GitHub-Integration

## Ziel

Du lernst, wie du mit `.gitignore` bestimmte Dateien von Git ausschliesst und wie du dein lokales Repository mit GitHub verbindest. Du verstehst den Unterschied zwischen lokalem und Remote-Repository und kannst dein Portfolio online veröffentlichen.

## Beschreibung

Nicht alle Dateien sollen in Git verfolgt werden. Temporäre Dateien, Passwörter, grosse Mediendateien oder generierte Dateien gehören nicht ins Repository. Mit einer `.gitignore`-Datei sagst du Git, welche Dateien ignoriert werden sollen.

Zusätzlich lernst du, wie du dein lokales Repository mit GitHub verbindest. GitHub ist die grösste Plattform für Git-Repositories und wird von Millionen Entwicklern weltweit genutzt. Hier kannst du deinen Code speichern, mit anderen teilen und an Open-Source-Projekten mitarbeiten.

**Hinweis:** Dieser Auftrag baut auf den vorherigen Aufträgen auf, geht aber über die Grundlagen hinaus. Er ist optional und für Lernende gedacht, die tiefer einsteigen möchten.

---

## Teil 1: .gitignore verstehen und einrichten (20 Min)

### 1.1 Warum .gitignore?

**Dateien, die NICHT in Git gehören:**
- Passwörter und API-Keys (z.B. `.env`-Dateien)
- Betriebssystem-Dateien (z.B. `.DS_Store` auf Mac, `Thumbs.db` auf Windows)
- Editor-Konfigurationen (z.B. `.vscode/` wenn nicht im Team geteilt)
- Generierte Dateien (z.B. `node_modules/`, `dist/`, `build/`)
- Grosse Binärdateien (Videos, hochauflösende Bilder)
- Temporäre Dateien (z.B. `.log`, `.tmp`)

**Was passiert ohne .gitignore?**
- Dein Repository wird unnötig gross
- Sensible Daten könnten öffentlich werden
- Merge-Konflikte bei generierten Dateien
- Unübersichtliche Git-Historie

### 1.2 .gitignore erstellen

Erstelle eine neue Datei namens **`.gitignore`** im Projektordner (auf gleicher Ebene wie `index.html`):

**Projektstruktur:**
```
mein-portfolio/
├── .git/
├── .gitignore      ← Neue Datei!
├── index.html
├── styles.css
├── script.js
├── images/
└── README.md
```

**Inhalt der `.gitignore`:**

```gitignore
# Betriebssystem-Dateien
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
Desktop.ini

# Editor-Konfigurationen
.vscode/
.idea/
*.swp
*.swo
*~

# Logs und temporäre Dateien
*.log
*.tmp
*.temp
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Umgebungsvariablen (WICHTIG für Passwörter!)
.env
.env.local
.env.*.local

# Dependencies (falls du Node.js nutzt)
node_modules/
package-lock.json

# Build-Ordner
dist/
build/
.cache/

# Backup-Dateien
*.bak
*.backup
*~

# Grosse Mediendateien (anpassen an deine Bedürfnisse)
# *.mp4
# *.mov
# *.avi

# Persönliche Notizen
NOTIZEN.txt
TODO.md
```

**Syntax-Regeln für .gitignore:**
- `dateiname.txt` = Ignoriert diese Datei in allen Ordnern
- `ordner/` = Ignoriert den kompletten Ordner
- `*.log` = Ignoriert alle Dateien mit .log-Endung
- `!wichtig.log` = Ausnahme – diese Datei NICHT ignorieren
- `ordner/*.txt` = Nur .txt-Dateien direkt im Ordner
- `ordner/**/*.txt` = Alle .txt-Dateien rekursiv im Ordner
- `#` = Kommentar

### 1.3 .gitignore testen

**Test 1: Ignorierte Dateien erstellen**

Erstelle Test-Dateien, die ignoriert werden sollen:

```bash
# macOS System-Datei erstellen
touch .DS_Store

# Log-Datei erstellen
echo "Test-Log" > test.log

# Temporäre Datei erstellen
touch temp.tmp

# Status checken
git status
```

**Erwartete Ausgabe:**
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

**Wichtig:** Die Test-Dateien (`.DS_Store`, `test.log`, `temp.tmp`) werden NICHT angezeigt, weil sie ignoriert werden!

**Test 2: .gitignore committen**

```bash
# .gitignore zur Staging Area
git add .gitignore

# Commit erstellen
git commit -m ".gitignore mit Standard-Ausschlüssen hinzugefügt"

# Status checken – sollte sauber sein
git status
```

### 1.4 Bereits getrackte Dateien nachträglich ignorieren

**Problem:** Was, wenn eine Datei schon in Git ist, aber nachträglich ignoriert werden soll?

**Lösung:**

```bash
# Datei aus Git entfernen, aber lokal behalten
git rm --cached dateiname.txt

# Oder einen ganzen Ordner
git rm -r --cached ordner/

# Commit erstellen
git commit -m "Sensible Datei aus Repository entfernt"
```

**Wichtig:** Die Datei bleibt auf deinem Computer, wird aber nicht mehr von Git verfolgt!

---

## Teil 2: GitHub-Account erstellen (10 Min)

### 2.1 GitHub-Account registrieren

1. Gehe zu [github.com](https://github.com)
2. Klicke auf "Sign up"
3. Erstelle einen Account mit:
   - Username (professionell, z.B. "max-muster" oder "maxmuster")
   - E-Mail-Adresse (nutze deine berufliche oder Ausbildungs-Email)
   - Passwort (sicher und einzigartig!)
4. Verifiziere deine E-Mail-Adresse

**Tipp:** Wähle einen professionellen Username, den du auch in 10 Jahren noch nutzen kannst!

### 2.2 SSH-Key einrichten (Empfohlen)

SSH-Keys ermöglichen sichere Verbindungen ohne Passwort-Eingabe.

**SSH-Key generieren (Terminal):**

```bash
# SSH-Key erstellen (ersetze Email mit deiner GitHub-Email!)
ssh-keygen -t ed25519 -C "deine.email@example.com"

# Enter drücken bei "Enter file in which to save the key"
# Passwort eingeben (optional, aber empfohlen)

# Key zum SSH-Agent hinzufügen
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Public Key anzeigen (kopieren für GitHub)
cat ~/.ssh/id_ed25519.pub
```

**Key zu GitHub hinzufügen:**
1. Kopiere den kompletten Output von `cat ~/.ssh/id_ed25519.pub`
2. Gehe zu GitHub → Settings → SSH and GPG keys
3. Klicke "New SSH key"
4. Titel: "Mein Laptop" (oder ähnlich)
5. Key einfügen und "Add SSH key" klicken

**SSH-Verbindung testen:**
```bash
ssh -T git@github.com
```

**Erwartete Ausgabe:**
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Teil 3: Repository auf GitHub erstellen (15 Min)

### 3.1 Neues Repository auf GitHub erstellen

1. Gehe zu [github.com/new](https://github.com/new)
2. Fülle das Formular aus:
   - **Repository name:** `mein-portfolio`
   - **Description:** "Meine persönliche Portfolio-Website (Informatik-Lehre)"
   - **Public** oder **Private:** Public (damit andere es sehen können)
   - **NICHT** "Initialize with README" ankreuzen (du hast schon eins!)
3. Klicke "Create repository"

**GitHub zeigt jetzt Anweisungen** – folge der Sektion "push an existing repository from the command line"

### 3.2 Lokales Repository mit GitHub verbinden

**In deinem Terminal (im Portfolio-Ordner):**

```bash
# Remote-Repository hinzufügen (mit SSH)
git remote add origin git@github.com:deinusername/mein-portfolio.git

# Oder mit HTTPS (wenn kein SSH eingerichtet)
git remote add origin https://github.com/deinusername/mein-portfolio.git

# Remote-URL überprüfen
git remote -v
```

**Erwartete Ausgabe:**
```
origin  git@github.com:deinusername/mein-portfolio.git (fetch)
origin  git@github.com:deinusername/mein-portfolio.git (push)
```

### 3.3 Code zu GitHub pushen

```bash
# Branch umbenennen zu "main" (falls noch "master")
git branch -M main

# Code zu GitHub hochladen
git push -u origin main
```

**Erwartete Ausgabe:**
```
Enumerating objects: 25, done.
Counting objects: 100% (25/25), done.
Delta compression using up to 8 threads
Compressing objects: 100% (18/18), done.
Writing objects: 100% (25/25), 4.52 KiB | 4.52 MiB/s, done.
Total 25 (delta 5), reused 0 (delta 0), pack-reused 0
To github.com:deinusername/mein-portfolio.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

**Was bedeutet das?**
- Alle deine Commits wurden zu GitHub hochgeladen
- Branch "main" ist jetzt mit dem Remote-Repository verbunden
- `-u origin main` setzt das Remote-Repository als Standard (bei zukünftigen Pushes reicht `git push`)

### 3.4 Portfolio auf GitHub ansehen

1. Gehe zu `https://github.com/deinusername/mein-portfolio`
2. Du siehst jetzt:
   - Alle deine Dateien
   - Die README.md als Beschreibung
   - Die komplette Commit-Historie
   - Den Code zum Durchsuchen

**Herzlichen Glückwunsch!** Dein Portfolio ist jetzt online auf GitHub! 🎉

---

## Teil 4: Workflow mit GitHub (15 Min)

### 4.1 Änderungen lokal machen und pushen

Jetzt ist dein Workflow:
1. Änderungen lokal machen
2. `git add` → `git commit`
3. `git push` um zu GitHub hochzuladen

**Beispiel:**

Füge eine neue Sektion in `index.html` hinzu:

```html
<section id="github">
    <h2>Meine Projekte auf GitHub</h2>
    <p>Besuche mein GitHub-Profil: 
       <a href="https://github.com/deinusername" target="_blank">
           github.com/deinusername
       </a>
    </p>
</section>
```

**Workflow ausführen:**

```bash
# Status checken
git status

# Zur Staging Area
git add index.html

# Commit erstellen
git commit -m "GitHub-Sektion mit Link zu meinem Profil hinzugefügt"

# Zu GitHub hochladen
git push
```

**Erwartete Ausgabe:**
```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 387 bytes | 387.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
To github.com:deinusername/mein-portfolio.git
   c4b7e93..f8a2d41  main -> main
```

**Überprüfung:** Gehe zu GitHub und lade die Seite neu – dein neuer Commit ist online!

### 4.2 Änderungen von GitHub holen

Wenn du an mehreren Computern arbeitest oder im Team, musst du Änderungen von GitHub holen:

```bash
# Änderungen von GitHub herunterladen
git pull
```

**Was macht `git pull`?**
- Holt alle neuen Commits von GitHub
- Merged sie automatisch in deinen lokalen Branch
- = `git fetch` + `git merge` in einem Befehl

### 4.3 Repository klonen (auf einem anderen Computer)

Um dein Repository auf einem anderen Computer zu öffnen:

```bash
# Repository von GitHub herunterladen
git clone git@github.com:deinusername/mein-portfolio.git

# In den Ordner wechseln
cd mein-portfolio

# Alle Dateien sind da, inklusive kompletter Git-Historie!
git log --oneline
```

---

## Teil 5: GitHub Pages – Portfolio veröffentlichen (Bonus, 10 Min)

GitHub bietet kostenloses Hosting für statische Websites!

### 5.1 GitHub Pages aktivieren

1. Gehe zu deinem Repository auf GitHub
2. Klicke auf "Settings" (oben rechts)
3. Klicke auf "Pages" (linkes Menü)
4. Bei "Source" wähle "main" Branch
5. Klicke "Save"

**Nach 1-2 Minuten:**
- Deine Website ist online unter: `https://deinusername.github.io/mein-portfolio/`
- GitHub zeigt die URL oben im Pages-Bereich an

### 5.2 Custom Domain (Optional)

Wenn du eine eigene Domain hast (z.B. `maxmuster.ch`):
1. Füge einen CNAME-Record bei deinem Domain-Provider hinzu
2. Trage die Domain bei GitHub Pages ein
3. Aktiviere "Enforce HTTPS"

**Dokumentation:** [GitHub Pages Custom Domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

---

## Erfolgskriterien

- [ ] `.gitignore` ist erstellt und funktioniert korrekt
- [ ] Unwichtige Dateien werden von Git ignoriert
- [ ] GitHub-Account ist erstellt
- [ ] SSH-Key ist eingerichtet und funktioniert
- [ ] Repository wurde auf GitHub erstellt
- [ ] Lokales Repository ist mit GitHub verbunden (`git remote -v`)
- [ ] Code wurde erfolgreich zu GitHub gepusht
- [ ] Änderungen können mit `git push` hochgeladen werden
- [ ] Optional: Portfolio ist auf GitHub Pages online

## Tipps

- **Niemals Passwörter committen!** Nutze `.env`-Dateien und füge sie zur .gitignore hinzu
- **Professioneller Username:** Nutze deinen Namen oder eine Variation davon
- **SSH statt HTTPS:** SSH ist sicherer und bequemer (kein Passwort nötig)
- **README.md pflegen:** Gute README-Dateien helfen anderen, dein Projekt zu verstehen
- **GitHub Student Pack:** Als Lernender bekommst du kostenlose Pro-Features → [education.github.com](https://education.github.com)
- **Profitipp:** Nutze GitHub Issues, um Bugs und Features zu tracken

## Reflexionsfragen

1. Warum sollten Passwörter und API-Keys NIEMALS in Git committed werden?
2. Was ist der Unterschied zwischen `git push` und `git pull`?
3. Teste: Klone dein Repository in einen anderen Ordner. Was passiert mit der Git-Historie?
4. Warum ist SSH besser als HTTPS für GitHub-Verbindungen?
5. Recherchiere: Was ist der Unterschied zwischen GitHub, GitLab und Bitbucket?

## Weiterführende Links

- [GitHub Docs – Getting Started](https://docs.github.com/en/get-started)
- [gitignore.io – Generator für .gitignore](https://www.toptal.com/developers/gitignore)
- [GitHub Student Pack](https://education.github.com/pack)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [SSH Key Tutorial (GitHub)](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Awesome READMEs – Inspiration](https://github.com/matiassingers/awesome-readme)

---

**⏱️ Geschätzte Zeit:** 60-80 Minuten  
**📦 Nächstes Kapitel:** Branching & Merging – Arbeite parallel an verschiedenen Features!
