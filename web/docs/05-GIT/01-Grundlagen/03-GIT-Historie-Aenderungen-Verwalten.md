# Auftrag 3: Git-Historie nutzen und Änderungen verwalten

## Ziel

Du lernst, wie du die Git-Historie effektiv nutzt, zwischen Commits navigierst, Dateien wiederherstellt und Änderungen rückgängig machst. Du verstehst, wie Git als "Zeitmaschine" für deinen Code funktioniert.

## Beschreibung

Git ist nicht nur zum Speichern von Änderungen da, sondern auch zum Navigieren durch die Projekt-Historie. Du kannst jederzeit zu früheren Versionen zurückspringen, einzelne Dateien wiederherstellen oder Änderungen rückgängig machen. Das ist extrem nützlich, wenn etwas schiefgeht oder du experimentieren möchtest!

In diesem Auftrag lernst du die wichtigsten Befehle kennen, um die Git-Historie zu durchsuchen und Änderungen zu verwalten.

---

### Teil 1: Git-Historie durchsuchen (15 Min)

**1.1 Erweiterte Log-Ansichten**

Git bietet viele Möglichkeiten, die Historie anzuzeigen:

```bash
# Standard-Log
git log

# Kompakte einzeilige Ansicht
git log --oneline

# Mit Grafik (zeigt Branches)
git log --oneline --graph --all

# Nur die letzten 3 Commits
git log --oneline -3

# Commits mit Statistiken (wie viele Zeilen geändert)
git log --stat

# Commits mit vollständigen Änderungen (Diff)
git log -p

# Commits von einem bestimmten Autor
git log --author="Dein Name"

# Commits nach Datum filtern
git log --since="2025-11-01"
git log --since="2 weeks ago"
git log --until="yesterday"
```

**Aufgabe:** Probiere alle Varianten aus und vergleiche die Ausgaben!

**1.2 Bestimmten Commit anschauen**

Jeder Commit hat eine eindeutige Hash-ID. Du kannst einen Commit im Detail anschauen:

```bash
# Zeige Commit-Details (nutze deinen eigenen Hash!)
git show a3f5e21

# Zeige nur die Änderungen in einer Datei
git show a3f5e21:index.html

# Zeige den letzten Commit
git show HEAD

# Zeige den vorletzten Commit
git show HEAD~1

# Zeige den drittletzten Commit
git show HEAD~2
```

**HEAD** ist ein Zeiger auf den aktuellen Commit. `HEAD~1` ist der Commit davor, `HEAD~2` zwei Commits davor, usw.

**1.3 Suche in Commits**

Git kann Commits nach Stichwörtern durchsuchen:

```bash
# Suche nach Commit-Nachrichten mit "Kontakt"
git log --grep="Kontakt"

# Suche nach Commits, die eine bestimmte Datei geändert haben
git log -- index.html

# Suche nach Commits, die bestimmten Code hinzugefügt/entfernt haben
git log -S "Kontakt-Sektion"
```

**Aufgabe:** Suche nach einem Commit, der "Footer" in der Nachricht enthält!

---

### Teil 2: Änderungen vergleichen mit `git diff` (15 Min)

`git diff` zeigt dir genau, was sich geändert hat.

**2.1 Änderungen in der Working Directory**

Ändere zuerst etwas in deiner `index.html` (z.B. füge einen neuen Absatz hinzu):

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    <p>Möchtest du mit mir in Kontakt treten? Schreib mir eine Nachricht!</p>
    <p>Ich freue mich auf deine Nachricht und antworte in der Regel innerhalb von 24 Stunden.</p>
    <!-- ... Rest bleibt gleich ... -->
</section>
```

**Jetzt die Änderungen anschauen:**

```bash
# Zeige alle Änderungen seit dem letzten Commit
git diff
```

**Erwartete Ausgabe:**
```diff
diff --git a/index.html b/index.html
index 8f3a2e1..c9d4b5f 100644
--- a/index.html
+++ b/index.html
@@ -45,6 +45,7 @@
 <section id="kontakt">
     <h2>Kontakt</h2>
     <p>Möchtest du mit mir in Kontakt treten? Schreib mir eine Nachricht!</p>
+    <p>Ich freue mich auf deine Nachricht und antworte in der Regel innerhalb von 24 Stunden.</p>
     <address>
```

**Erklärung:**
- **--- a/index.html** = Alte Version
- **+++ b/index.html** = Neue Version
- **Grün (+)** = Hinzugefügt
- **Rot (-)** = Entfernt

**2.2 Änderungen in der Staging Area**

Füge die Änderung zur Staging Area hinzu:

```bash
git add index.html

# Jetzt zeigt git diff nichts mehr an (weil Änderungen schon "staged" sind)
git diff

# Um staged Änderungen zu sehen:
git diff --staged
```

**2.3 Änderungen zwischen Commits vergleichen**

```bash
# Vergleiche zwei Commits (nutze deine eigenen Hashes!)
git diff a3f5e21 c4b7e93

# Vergleiche aktuellen Stand mit einem früheren Commit
git diff HEAD~2

# Vergleiche nur eine bestimmte Datei
git diff HEAD~1 -- index.html
```

**Aufgabe:** Vergleiche deinen ersten Commit mit dem aktuellen Stand!

---

### Teil 3: Änderungen rückgängig machen (20 Min)

**3.1 Änderungen in Working Directory verwerfen**

Manchmal machst du Änderungen, die du nicht behalten möchtest.

**Szenario:** Du hast `index.html` geändert, aber möchtest zur letzten committeten Version zurück.

```bash
# Status checken (zeigt geänderte Dateien)
git status

# Änderungen an einer Datei verwerfen
git restore index.html

# Oder alle Änderungen verwerfen
git restore .
```

**Wichtig:** Das ist NICHT rückgängig zu machen! Die Änderungen sind weg!

**Alternative Methode (ältere Git-Versionen):**
```bash
git checkout -- index.html
```

**3.2 Datei aus Staging Area entfernen**

Du hast eine Datei mit `git add` zur Staging Area hinzugefügt, willst sie aber doch nicht committen.

**Beispiel:**
```bash
# Datei zur Staging Area hinzufügen
git add README.md

# Status checken
git status

# Datei aus Staging Area entfernen (Änderungen bleiben!)
git restore --staged README.md

# Status checken – Datei ist wieder "unstaged"
git status
```

**Alternative Methode (ältere Git-Versionen):**
```bash
git reset HEAD README.md
```

**3.3 Letzten Commit ändern**

Du hast gerade committet, aber vergessen etwas hinzuzufügen oder die Commit-Nachricht ist falsch.

**Szenario 1: Commit-Nachricht ändern**
```bash
# Ändere die Nachricht des letzten Commits
git commit --amend -m "Neue, bessere Commit-Nachricht"
```

**Szenario 2: Vergessene Datei hinzufügen**
```bash
# Du hast eine Datei vergessen
git add vergessene-datei.txt

# Füge sie zum letzten Commit hinzu (keine neue Commit-Nachricht nötig)
git commit --amend --no-edit
```

**Wichtig:** Nutze `--amend` nur für den LETZTEN Commit und nur, wenn du ihn noch nicht gepusht hast!

**3.4 Zu einem früheren Commit zurückkehren (Lesen)**

Es gibt zwei Wege, zu einem früheren Commit zurückzukehren:

**Methode 1: `git reset` (ändert Historie)**
```bash
# VORSICHT: Löscht alle Commits nach diesem!
# Nutze dies nur in deinem lokalen Repository

# Soft Reset: Commits löschen, Änderungen behalten
git reset --soft HEAD~1

# Mixed Reset (Standard): Commits löschen, Staging Area leeren, Änderungen behalten
git reset HEAD~1

# Hard Reset: Alles löschen (Commits UND Änderungen!)
git reset --hard HEAD~1
```

**Methode 2: `git revert` (erstellt neuen Commit)**
```bash
# Erstellt einen neuen Commit, der einen alten rückgängig macht
# Sicherer, weil Historie erhalten bleibt
git revert HEAD
```

**Für Lernende:** Nutze besser `git revert`, da es sicherer ist!

---

### Teil 4: Praktische Übung – Experimentieren mit Sicherheitsnetz (15 Min)

Jetzt übst du den Umgang mit der Git-Historie in einer sicheren Umgebung.

**4.1 Experiment vorbereiten**

Füge eine experimentelle Sektion in `index.html` hinzu:

```html
<section id="experiment">
    <h2>Experimenteller Bereich</h2>
    <p>Dies ist ein Test – wird vielleicht wieder gelöscht!</p>
</section>
```

**Workflow:**
```bash
git add index.html
git commit -m "Experimentelle Sektion hinzugefügt"
```

**4.2 Experiment rückgängig machen**

Du entscheidest dich, das Experiment zu verwerfen:

```bash
# Letzten Commit rückgängig machen
git revert HEAD

# Ein Editor öffnet sich für die Revert-Nachricht
# Standardnachricht ist OK, speichern und schliessen
```

**Oder als Alternative mit Reset (nur lokal!):**
```bash
# Letzten Commit komplett löschen
git reset --hard HEAD~1
```

**4.3 Historie überprüfen**

```bash
# Schaue die Historie an
git log --oneline

# Mit Revert siehst du:
# abc1234 Revert "Experimentelle Sektion hinzugefügt"
# def5678 Experimentelle Sektion hinzugefügt

# Mit Reset siehst du:
# (Der Commit ist komplett weg)
```

**4.4 Datei aus früherem Commit wiederherstellen**

Angenommen, du hast versehentlich einen wichtigen Teil gelöscht. Du kannst einzelne Dateien aus früheren Commits wiederherstellen:

```bash
# Datei aus einem bestimmten Commit wiederherstellen
git restore --source=HEAD~2 index.html

# Oder aus einem bestimmten Commit-Hash
git restore --source=a3f5e21 index.html

# Änderungen anschauen
git diff

# Wenn OK, committen
git add index.html
git commit -m "Wichtigen Teil aus früherem Commit wiederhergestellt"
```

---

## Erfolgskriterien

- [ ] Du kannst die Git-Historie mit verschiedenen `git log`-Optionen durchsuchen
- [ ] Du verstehst `git diff` und kannst Änderungen vergleichen
- [ ] Du kannst Änderungen in der Working Directory mit `git restore` verwerfen
- [ ] Du kannst Dateien aus der Staging Area mit `git restore --staged` entfernen
- [ ] Du kannst den letzten Commit mit `git commit --amend` ändern
- [ ] Du verstehst den Unterschied zwischen `git reset` und `git revert`
- [ ] Du kannst einzelne Dateien aus früheren Commits wiederherstellen

## Tipps

- **`git status` und `git log` sind deine besten Freunde** – nutze sie oft!
- **Experimentiere lokal:** Solange du nichts gepusht hast, kannst du fast alles rückgängig machen
- **`git reflog` ist dein Rettungsanker:** Zeigt ALLE Aktionen, auch gelöschte Commits
- **VS Code Git Graph Extension:** Visualisiert deine Git-Historie als Baum
- **Backup vor grossen Änderungen:** Erstelle einen Branch für Experimente (kommt im nächsten Kapitel)
- **Profitipp:** Nutze `git stash`, um Änderungen temporär zu speichern (recherchiere selbst!)

## Reflexionsfragen

1. Was ist der Unterschied zwischen `git restore` und `git restore --staged`?
2. Wann würdest du `git revert` nutzen und wann `git reset --hard`?
3. Teste: Erstelle einen Commit, ändere ihn mit `--amend`, und schaue mit `git log` nach. Was fällt dir auf?
4. Warum ist es gefährlich, `git reset --hard` zu nutzen? Was geht dabei verloren?
5. Recherchiere: Was macht `git reflog` und wann ist es nützlich?

## Weiterführende Links

- [Git Basics – Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
- [Git Reset vs Revert – Erklärung](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)
- [Git Reflog – Der Rettungsanker](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)
- [Oh Shit, Git!? – Wenn was schiefgeht](https://ohshitgit.com/)
- [Git Cheat Sheet – Undoing Changes](https://training.github.com/downloads/github-git-cheat-sheet/)

---

**⏱️ Geschätzte Zeit:** 60-70 Minuten  
**📦 Nächster Schritt:** Im nächsten Kapitel (Branching & Merging) lernst du, wie du mit Branches parallel an verschiedenen Features arbeitest!
