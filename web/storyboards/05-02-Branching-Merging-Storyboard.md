# Storyboard: Git – Branching & Merging

**Modul:** Git  
**Thema:** Branching & Merging  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Geschätzte Videolänge:** 10-12 Minuten  
**Autor:** Tim Leibacher

---

## Video-Übersicht

**Lernziele:**
- Konzept von Branches verstehen (paralleles Arbeiten)
- Neue Branches mit `git branch` erstellen
- Zwischen Branches mit `git checkout` wechseln
- Branches mit `git merge` zusammenführen
- Merge-Konflikte erkennen und lösen

**Benötigte Ressourcen:**
- Terminal (Bash/PowerShell)
- VS Code mit Portfolio-Projekt (aus vorherigem Video)
- Git installiert und konfiguriert
- Visualisierungs-Grafiken für Branching-Konzepte

---

## Szene 1: Intro & Warum Branching? (1 Min.)

### Sprechertext
"Willkommen zum Video über Git Branching und Merging! In den letzten Videos haben wir gelernt, wie man Commits erstellt und Änderungen trackt. Aber was passiert, wenn du an einem neuen Feature arbeiten möchtest, ohne den funktionierenden Code zu gefährden? Oder wenn mehrere Personen parallel am gleichen Projekt arbeiten? Hier kommen Branches ins Spiel. Stell dir Branches wie parallele Universen vor: Du kannst in einem Branch experimentieren, während der Hauptzweig stabil bleibt. Am Ende führst du erfolgreiche Experimente zurück in den Hauptzweig. Das ist die professionelle Arbeitsweise in der Softwareentwicklung."

### Bildschirmdarstellung
Zeige Visualisierung eines Git-Branch-Baums:
```
main:     A --- B --- C --- D
                 \           \
feature:          E --- F --- G  (merge)
```

Text-Overlay:
- **main** = Stabiler Hauptzweig (produktionsreif)
- **feature** = Experimenteller Zweig für neue Funktionen
- **merge** = Integration zurück in main

### Animation
- Fade-In für jeden Commit-Kreis
- Puls-Effekt auf dem Merge-Punkt
- Highlight: Feature-Branch in anderer Farbe (z.B. BAND-Türkis)

---

## Szene 2: Branches anzeigen – `git branch` (30 Sek.)

### Sprechertext
"Bevor wir neue Branches erstellen, schauen wir uns an, auf welchem Branch wir gerade sind. Mit `git branch` zeigst du alle lokalen Branches an. Der aktuelle Branch wird mit einem Stern markiert. Standardmässig startest du auf dem `main`-Branch – das ist der Hauptzweig deines Projekts."

### Bildschirmdarstellung
Terminal in Portfolio-Projekt-Ordner:

```bash
# Aktuellen Status anzeigen
git status
```

Ausgabe:
```
On branch main
nothing to commit, working tree clean
```

Dann:

```bash
# Alle Branches anzeigen
git branch
```

Ausgabe:
```
* main
```

**Erklärung einblenden:**
- `*` = Aktueller Branch
- `main` = Hauptzweig (Standard-Name seit Git 2.28)

### Hinweise
- Zeige, dass der Stern (`*`) den aktiven Branch markiert
- Erkläre: `main` ist der Standard-Name für den Hauptzweig
- Erwähne kurz: Früher hiess der Standard-Branch `master`

---

## Szene 3: Neuen Branch erstellen – `git branch <name>` (1 Min.)

### Sprechertext
"Jetzt erstellen wir einen neuen Branch für ein Feature. Angenommen, wir wollen eine Kontaktformular-Sektion zu unserem Portfolio hinzufügen. Wir nennen den Branch `feature/kontaktformular`. Die Namenskonvention `feature/...` ist eine Best Practice – so sieht jeder sofort, worum es geht. Mit `git branch feature/kontaktformular` erstellen wir den neuen Branch. Wichtig: Wir erstellen nur den Branch, wechseln aber noch nicht zu ihm."

### Bildschirmdarstellung
Terminal:

```bash
# Neuen Branch erstellen
git branch feature/kontaktformular

# Branches anzeigen
git branch
```

Ausgabe:
```
  feature/kontaktformular
* main
```

**Visualisierung einblenden:**
```
main:     A --- B --- C
                       |
feature/kontaktformular: (zeigt auf C)
```

Text-Overlay:
- "Branch erstellt, aber noch nicht gewechselt!"
- "Beide Branches zeigen momentan auf denselben Commit"

### Hinweise
- Erkläre Namenskonventionen: `feature/`, `bugfix/`, `hotfix/`
- Betone: Branch erstellen ≠ Branch wechseln
- Zeige, dass der Stern (`*`) noch bei `main` ist

---

## Szene 4: Branch wechseln – `git checkout` (1 Min.)

### Sprechertext
"Um in unserem neuen Branch zu arbeiten, müssen wir zu ihm wechseln. Das machst du mit `git checkout`. Nach dem Wechsel siehst du mit `git branch`, dass der Stern jetzt beim Feature-Branch ist. Alle Änderungen, die du jetzt machst, passieren nur in diesem Branch. Der `main`-Branch bleibt unberührt. Das ist die Magie von Branches: paralleles Arbeiten ohne gegenseitige Störung."

### Bildschirmdarstellung
Terminal:

```bash
# Zu neuem Branch wechseln
git checkout feature/kontaktformular
```

Ausgabe:
```
Switched to branch 'feature/kontaktformular'
```

Dann:

```bash
# Status checken
git branch
```

Ausgabe:
```
* feature/kontaktformular
  main
```

**VS Code einblenden:**
- Zeige unten links in VS Code: Branch-Anzeige "feature/kontaktformular"
- Highlight: VS Code zeigt immer den aktuellen Branch an

### Hinweise
- Erkläre: `git checkout` = Wechseln zwischen Branches
- Zeige VS Code Status Bar (unten links) mit Branch-Name
- Shortcut erwähnen: `git checkout -b <name>` erstellt UND wechselt

---

## Szene 5: Im Feature-Branch arbeiten (1.5 Min.)

### Sprechertext
"Jetzt arbeiten wir im Feature-Branch. Wir fügen eine einfache Kontaktformular-Sektion zu unserem Portfolio hinzu. Schauen wir uns das in der `index.html` an. Ich füge ein `<section>`-Element mit einem Formular hinzu. Dann speichern, zur Staging Area hinzufügen und committen – genau wie gewohnt. Wichtig: Dieser Commit passiert nur im Feature-Branch. Der `main`-Branch bleibt unverändert."

### Bildschirmdarstellung

**VS Code – index.html:**
Füge vor dem schliessenden `</body>` hinzu:

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    <form>
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        
        <label for="nachricht">Nachricht:</label>
        <textarea id="nachricht" name="nachricht" rows="5" required></textarea>
        
        <button type="submit">Senden</button>
    </form>
</section>
```

**Terminal:**

```bash
# Status checken
git status

# Änderungen hinzufügen
git add index.html

# Commit erstellen
git commit -m "Kontaktformular-Sektion hinzugefügt"
```

Ausgabe:
```
[feature/kontaktformular a7f3e21] Kontaktformular-Sektion hinzugefügt
 1 file changed, 15 insertions(+)
```

**Visualisierung einblenden:**
```
main:     A --- B --- C
                       \
feature:                D (Kontaktformular hinzugefügt)
```

### Hinweise
- Zeige den Commit-Hash in der Ausgabe
- Betone: main-Branch ist unverändert
- Erkläre: Du könntest jetzt mehrere Commits im Feature-Branch machen

---

## Szene 6: Zwischen Branches wechseln & Vergleichen (1 Min.)

### Sprechertext
"Jetzt kommt der spannende Teil: Wir wechseln zurück zum `main`-Branch und schauen uns die `index.html` an. Siehst du? Das Kontaktformular ist weg! Das liegt daran, dass wir es nur im Feature-Branch hinzugefügt haben. Wenn wir zurück zum Feature-Branch wechseln, ist es wieder da. So kannst du zwischen verschiedenen Versionen deines Projekts hin- und herwechseln. Das ist extrem nützlich, wenn du mehrere Features parallel entwickelst."

### Bildschirmdarstellung

**Terminal:**

```bash
# Zurück zu main wechseln
git checkout main
```

Ausgabe:
```
Switched to branch 'main'
```

**VS Code – index.html:**
- Zeige die Datei: Kontaktformular ist NICHT vorhanden
- Scrolle zum Ende der Datei: Zeige, dass `<section id="kontakt">` fehlt

**Terminal:**

```bash
# Zurück zu feature wechseln
git checkout feature/kontaktformular
```

**VS Code – index.html:**
- Zeige die Datei: Kontaktformular ist wieder DA
- Highlight: Die Sektion ist zurück

**Split-Screen-Vergleich:**
- Links: main-Branch (ohne Kontaktformular)
- Rechts: feature-Branch (mit Kontaktformular)

### Hinweise
- Erkläre: Git ändert die Dateien beim Wechsel automatisch
- Betone: Keine Angst – nichts geht verloren
- Zeige: VS Code aktualisiert die Dateien in Echtzeit

---

## Szene 7: Feature fertigstellen & Merge vorbereiten (30 Sek.)

### Sprechertext
"Unser Kontaktformular ist fertig und funktioniert gut. Jetzt wollen wir es in den `main`-Branch integrieren. Das nennt man 'Mergen'. Bevor wir das tun, schauen wir uns die Commit-Historie beider Branches an. Mit `git log --oneline --graph --all` siehst du alle Branches und ihre Commits visualisiert. Das hilft dir, den Überblick zu behalten."

### Bildschirmdarstellung

**Terminal (im feature-Branch):**

```bash
# Visualisierte Historie aller Branches
git log --oneline --graph --all
```

Ausgabe:
```
* a7f3e21 (HEAD -> feature/kontaktformular) Kontaktformular-Sektion hinzugefügt
* c4b7e93 (main) Initiales Portfolio mit HTML, CSS und JavaScript
```

**Erklärung einblenden:**
- `HEAD ->` zeigt den aktuellen Branch
- `*` markiert Commits
- Branch-Namen in Klammern

### Hinweise
- Erkläre: `--graph` zeigt visuelle Verbindungen
- Erkläre: `--all` zeigt alle Branches
- Betone: main ist eine Version "hinterher"

---

## Szene 8: Branches mergen – `git merge` (1.5 Min.)

### Sprechertext
"Jetzt integrieren wir das Feature in den Hauptzweig. Mergen ist ein Zwei-Schritt-Prozess: Erst wechselst du zum Ziel-Branch – das ist der Branch, IN DEN du mergen möchtest, in unserem Fall `main`. Dann führst du `git merge` mit dem Quell-Branch aus – das ist der Branch, den du integrieren möchtest, also `feature/kontaktformular`. Git erstellt automatisch einen Merge-Commit. In unserem Fall ist das ein Fast-Forward-Merge, weil keine Konflikte bestehen."

### Bildschirmdarstellung

**Terminal:**

```bash
# Schritt 1: Zu main wechseln (Ziel-Branch)
git checkout main
```

Ausgabe:
```
Switched to branch 'main'
```

```bash
# Schritt 2: Feature-Branch mergen
git merge feature/kontaktformular
```

Ausgabe:
```
Updating c4b7e93..a7f3e21
Fast-forward
 index.html | 15 +++++++++++++++
 1 file changed, 15 insertions(+)
```

**Visualisierung einblenden:**
```
Vorher:
main:     A --- B --- C
                       \
feature:                D

Nachher:
main:     A --- B --- C --- D
                       \   /
feature:                D
```

**VS Code – index.html:**
- Zeige die Datei im main-Branch: Kontaktformular ist jetzt DA!

### Hinweise
- Erkläre: "Fast-forward" bedeutet lineares Vorwärtsbewegen
- Betone: IMMER erst zum Ziel-Branch wechseln
- Zeige: main hat jetzt alle Änderungen aus feature

---

## Szene 9: Branch aufräumen – Branch löschen (30 Sek.)

### Sprechertext
"Nach erfolgreichem Merge ist der Feature-Branch nicht mehr nötig. Es ist Best Practice, ihn zu löschen, um das Repository aufgeräumt zu halten. Mit `git branch -d` löschst du einen Branch sicher – Git prüft, ob der Branch gemergt wurde. Falls nicht, bekommst du eine Warnung. So verlierst du keine Arbeit. Nach dem Löschen bleibt nur noch der `main`-Branch übrig."

### Bildschirmdarstellung

**Terminal:**

```bash
# Branch löschen (sicher)
git branch -d feature/kontaktformular
```

Ausgabe:
```
Deleted branch feature/kontaktformular (was a7f3e21).
```

```bash
# Branches anzeigen
git branch
```

Ausgabe:
```
* main
```

**Visualisierung einblenden:**
```
main:     A --- B --- C --- D
                       
(feature-Branch ist gelöscht)
```

### Hinweise
- Erkläre: `-d` = safe delete (nur wenn gemergt)
- Erwähne: `-D` = force delete (auch wenn nicht gemergt – vorsichtig!)
- Betone: Commits gehen NICHT verloren, nur die Branch-Referenz

---

## Szene 10: Merge-Konflikte verstehen (1.5 Min.)

### Sprechertext
"Bisher lief alles glatt – aber was passiert, wenn zwei Branches dieselbe Stelle im Code ändern? Dann entsteht ein Merge-Konflikt. Git kann nicht automatisch entscheiden, welche Änderung korrekt ist. Du musst manuell eingreifen. Schauen wir uns ein Beispiel an."

### Bildschirmdarstellung

**Szenario-Setup:**

Terminal:

```bash
# Neuen Branch für Konflikt-Demo erstellen
git checkout -b feature/titel-aendern

# Titel in index.html ändern
```

VS Code – index.html:
```html
<h1>Tim Leibacher – Portfolio</h1>  <!-- Vorher: "Mein Portfolio" -->
```

Terminal:
```bash
git add index.html
git commit -m "Portfolio-Titel personalisiert"

# Zurück zu main
git checkout main

# Titel in main ANDERS ändern
```

VS Code – index.html:
```html
<h1>Mein Webentwickler-Portfolio</h1>  <!-- Andere Änderung! -->
```

Terminal:
```bash
git add index.html
git commit -m "Portfolio-Titel mit Berufsbezeichnung"

# Jetzt mergen → Konflikt!
git merge feature/titel-aendern
```

**Ausgabe:**
```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

### Hinweise
- Betone: Konflikt entsteht nur bei Änderungen an derselben Stelle
- Zeige rot markierte Konflikt-Warnung
- Erkläre: Git stoppt und wartet auf deine Entscheidung

---

## Szene 11: Merge-Konflikte lösen (2 Min.)

### Sprechertext
"Git markiert Konfliktstellen im Code mit speziellen Markern. `<<<<<<< HEAD` zeigt deine Version im aktuellen Branch, `=======` trennt die Versionen, und `>>>>>>> feature/titel-aendern` zeigt die Version aus dem Feature-Branch. Du musst entscheiden: Welche Version ist korrekt? Oder kombinierst du beide? Entferne die Marker, behalte die gewünschte Version, und erstelle einen Commit."

### Bildschirmdarstellung

**VS Code – index.html mit Konflikt:**

```html
<body>
    <header>
<<<<<<< HEAD
        <h1>Mein Webentwickler-Portfolio</h1>
=======
        <h1>Tim Leibacher – Portfolio</h1>
>>>>>>> feature/titel-aendern
        <p>Willkommen auf meiner Seite!</p>
    </header>
```

**VS Code mit eingeblendeten Merge-Tools:**
- Zeige: "Accept Current Change" / "Accept Incoming Change" / "Accept Both Changes"
- Klicke auf "Accept Incoming Change"

**Ergebnis:**
```html
<body>
    <header>
        <h1>Tim Leibacher – Portfolio</h1>
        <p>Willkommen auf meiner Seite!</p>
    </header>
```

**Terminal:**

```bash
# Status checken
git status
```

Ausgabe:
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html
```

```bash
# Konflikt gelöst → hinzufügen
git add index.html

# Merge-Commit erstellen
git commit -m "Merge feature/titel-aendern - Titel-Konflikt gelöst"
```

Ausgabe:
```
[main b8f4e32] Merge feature/titel-aendern - Titel-Konflikt gelöst
```

### Hinweise
- Zeige VS Code Merge-Tools (sehr praktisch!)
- Erkläre: Du kannst auch manuell editieren
- Betone: Nach Auflösung IMMER committen

---

## Szene 12: Branching-Strategie & Best Practices (1 Min.)

### Sprechertext
"Fassen wir die wichtigsten Best Practices zusammen. Erstens: Der `main`-Branch sollte immer funktionierenden, stabilen Code enthalten. Nutze Feature-Branches für neue Funktionen, Bugfix-Branches für Fehlerbehebungen. Zweitens: Benenne Branches aussagekräftig mit Präfixen wie `feature/`, `bugfix/` oder `hotfix/`. Drittens: Committe oft im Feature-Branch, merge erst, wenn das Feature fertig ist. Viertens: Lösche Feature-Branches nach erfolgreichem Merge. Und fünftens: Bei Merge-Konflikten nicht paniken – das ist normal. Analysiere ruhig, welche Version korrekt ist."

### Bildschirmdarstellung

**Text-Overlay mit Best Practices:**

```
✅ Best Practices für Git Branching:

1. main = Stabiler, funktionierender Code
2. Feature-Branches für neue Funktionen
3. Aussagekräftige Branch-Namen (feature/..., bugfix/...)
4. Oft committen, selten mergen
5. Branches nach Merge löschen
6. Merge-Konflikte ruhig und strukturiert lösen
7. git log --graph nutzen für Übersicht
```

**Visualisierung (professioneller Workflow):**
```
main:     A --- B ------- E ------- H
               \         /         /
feature1:       C --- D          /
                 \              /
feature2:         F --- G ----/
```

### Hinweise
- Zeige typischen Entwicklungs-Workflow visuell
- Betone: In Teams arbeiten oft mehrere Personen parallel
- Erkläre: Branching vermeidet Chaos und Überschreibungen

---

## Szene 13: Zusammenfassung & Ausblick (1 Min.)

### Sprechertext
"Fassen wir zusammen: Branches ermöglichen paralleles Arbeiten ohne gegenseitige Störung. Mit `git branch` erstellst du neue Branches, mit `git checkout` wechselst du zwischen ihnen, und mit `git merge` führst du sie zusammen. Merge-Konflikte sind normal und lösbar – Git gibt dir die Kontrolle. In den Aufträgen wirst du diesen Workflow selbst durchspielen: Du erstellst Feature-Branches für verschiedene Portfolio-Erweiterungen, arbeitest parallel an mehreren Features und lernst, Konflikte zu lösen. Das ist die professionelle Arbeitsweise in der Softwareentwicklung. Viel Erfolg!"

### Bildschirmdarstellung

**Befehlsübersicht:**
```
Wichtigste Befehle:

✅ git branch              → Branches anzeigen
✅ git branch <name>       → Neuen Branch erstellen
✅ git checkout <name>     → Zu Branch wechseln
✅ git checkout -b <name>  → Erstellen UND wechseln
✅ git merge <branch>      → Branch mergen
✅ git branch -d <name>    → Branch löschen

Konflikt-Lösung:
1. Konfliktmarker im Code finden
2. Manuelle Entscheidung treffen
3. Marker entfernen
4. git add <datei>
5. git commit
```

### Hinweise
- Fade-Out mit BAND-Gradient-Hintergrund
- Call-to-Action: "Jetzt selbst ausprobieren!"

---

## Zusatzmaterialien für Video-Produktion

### Demo-Dateien für Konflikt-Szenario

**Datei: conflict-demo.html**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Konflikt-Demo</title>
</head>
<body>
    <h1>Original-Titel</h1>
    <p>Dieser Titel wird in zwei Branches unterschiedlich geändert.</p>
</body>
</html>
```

### Visualisierungs-Grafiken (für Animationen)

**Branch-Modell (SVG-Vorlage):**
- Kreise für Commits (BAND-Blau: #376B8C)
- Linien zwischen Commits
- Branch-Labels (Aptos Bold)
- Merge-Pfeile (BAND-Türkis: #29786A)

**Konflikt-Marker (Code-Highlight):**
- `<<<<<<<` in Rot
- `=======` in Gelb
- `>>>>>>>` in Rot

### Terminal-Setup

**Empfohlene Einstellungen:**
- Schriftgrösse: 18pt
- Font: Fira Code oder Consolas
- Farbschema: Hell (bessere Lesbarkeit)
- Zeige Branch-Name im Prompt (wenn möglich)

**Branch-Anzeige im Prompt:**
```bash
# Bash-Konfiguration für Branch-Anzeige
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[01;31m\]$(__git_ps1 " (%s)")\[\033[00m\]\$ '
```

### Häufige Fehler & Lösungen

| Problem | Lösung |
|---------|--------|
| `error: pathspec 'branch-name' did not match` | Branch existiert nicht, Tippfehler? |
| `error: Your local changes would be overwritten` | Committe oder stashe Änderungen vor Wechsel |
| `CONFLICT (content): Merge conflict` | Normal! Konflikt manuell lösen |
| `error: cannot delete branch` | Branch ist nicht gemergt → nutze `-D` (vorsichtig!) |
| Branch nach Merge noch sichtbar | Normal, erst nach `git branch -d` gelöscht |

### Weiterführende Ressourcen

- [Learn Git Branching (Interaktiv)](https://learngitbranching.js.org/)
- [Atlassian Git Branching Tutorial](https://www.atlassian.com/git/tutorials/using-branches)
- [Git Branching Strategies](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Visualizing Git](https://git-school.github.io/visualizing-git/)

---

## Technische Hinweise für Videobearbeitung

- Split-Screen für Branch-Vergleiche
- Animationen für Branch-Visualisierungen (After Effects)
- Code-Highlighting für Konfliktmarker
- Text-Overlays für wichtige Befehle
- Cursor-Highlights bei wichtigen Terminal-Eingaben
- Background-Musik: Subtil, nicht ablenkend
- BAND Corporate Design: Aptos Font, Farben #376B8C, #29786A
- Untertitel für Barrierefreiheit

---

**Ende des Storyboards**
