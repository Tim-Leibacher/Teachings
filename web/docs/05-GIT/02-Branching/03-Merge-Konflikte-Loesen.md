# Auftrag 3: Merge-Konflikte erkennen und lösen

## Ziel

Du lernst, wie Merge-Konflikte entstehen, wie du sie erkennst und professionell löst. Das ist eine essenzielle Fähigkeit für die Teamarbeit.

## Beschreibung

Merge-Konflikte sind normal und kein Grund zur Panik. Sie entstehen, wenn zwei Branches dieselbe Stelle im Code unterschiedlich ändern. Git kann dann nicht automatisch entscheiden, welche Version korrekt ist – du musst manuell eingreifen. In diesem Auftrag provozierst du absichtlich Konflikte, um zu lernen, wie du sie erkennst und löst.

---

### Teil 1: Konflikte verstehen – Szenario aufbauen (10 Min)

**1.1 Ausgangslage vorbereiten**

```bash
# Sicherstellen, dass du auf main bist
git checkout main

# Status checken
git status
```

**Erwartete Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**1.2 Zwei parallele Branches erstellen**

```bash
# Branch 1: Titel ändern (Version A)
git checkout -b feature/titel-portfolio

# Branch 2: Titel ändern (Version B) – erstellen, aber nicht wechseln
git branch feature/titel-webentwickler
```

**1.3 Branches anzeigen**

```bash
git branch
```

**Ausgabe:**
```
  feature/titel-webentwickler
* feature/titel-portfolio
  main
```

**Szenario:** Du bist im Branch `feature/titel-portfolio` und wirst gleich den Titel ändern. Danach wechselst du zu `feature/titel-webentwickler` und änderst denselben Titel anders. Beim Merge entsteht ein Konflikt.

---

### Teil 2: Konflikte provozieren – Änderung 1 (10 Min)

**2.1 Im Branch `feature/titel-portfolio` arbeiten**

Du bist bereits in diesem Branch. Öffne `index.html` und ändere den Titel:

**Vorher:**
```html
<h1>Mein Portfolio</h1>
```

**Nachher:**
```html
<h1>Portfolio – Dein Name</h1>
```

**Wichtig:** Ersetze "Dein Name" mit deinem echten Namen!

**2.2 Änderung committen**

```bash
git status
git add index.html
git commit -m "Titel mit persönlichem Namen ergänzt"
```

**2.3 Zu main mergen**

```bash
# Zu main wechseln
git checkout main

# Branch mergen
git merge feature/titel-portfolio
```

**Ausgabe (Fast-Forward):**
```
Updating f3a8b21..g7d2e43
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

**Im Browser checken:** Der neue Titel ist sichtbar.

---

### Teil 3: Konflikt erzeugen – Änderung 2 (15 Min)

**3.1 Zu zweitem Branch wechseln**

```bash
git checkout feature/titel-webentwickler
```

**Im Browser checken:** Der Titel ist wieder "Mein Portfolio" – korrekt, weil dieser Branch vor der ersten Änderung erstellt wurde.

**3.2 Denselben Titel ANDERS ändern**

Öffne `index.html` und ändere den Titel:

**Vorher (im Branch):**
```html
<h1>Mein Portfolio</h1>
```

**Nachher:**
```html
<h1>Webentwickler Portfolio – Moderne Weblösungen</h1>
```

**3.3 Änderung committen**

```bash
git status
git add index.html
git commit -m "Titel mit Berufsbezeichnung und Slogan erweitert"
```

**3.4 Merge versuchen → Konflikt!**

```bash
# Zu main wechseln
git checkout main

# Branch mergen → Konflikt!
git merge feature/titel-webentwickler
```

**Ausgabe (KONFLIKT!):**
```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

**Was ist passiert?**
- Git hat versucht, die Änderungen zu mergen
- Beide Branches haben denselben Titel unterschiedlich geändert
- Git kann nicht automatisch entscheiden, welche Version korrekt ist
- Du musst manuell eingreifen

---

### Teil 4: Konflikt analysieren (10 Min)

**4.1 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

**Was bedeutet das?**
- **You have unmerged paths:** Du bist mitten in einem Merge mit Konflikt
- **both modified:** Beide Branches haben dieselbe Datei geändert
- **fix conflicts and run "git commit":** Git sagt dir, was zu tun ist
- **git merge --abort:** Notausgang – bricht Merge ab und stellt ursprünglichen Zustand wieder her

**4.2 Konflikt-Marker im Code anschauen**

Öffne `index.html` in VS Code. Du siehst etwas wie:

```html
<body>
    <header>
<<<<<<< HEAD
        <h1>Portfolio – Tim Leibacher</h1>
=======
        <h1>Webentwickler Portfolio – Moderne Weblösungen</h1>
>>>>>>> feature/titel-webentwickler
        <p>Willkommen auf meiner Seite!</p>
    </header>
```

**Konflikt-Marker erklärt:**
- `<<<<<<< HEAD` → Anfang der Version im aktuellen Branch (main)
- `=======` → Trennung zwischen den beiden Versionen
- `>>>>>>> feature/titel-webentwickler` → Ende der Version aus dem Feature-Branch

**4.3 VS Code Merge-Tools**

VS Code zeigt über dem Konflikt hilfreiche Buttons:
- **Accept Current Change** – Behalte Version aus `main`
- **Accept Incoming Change** – Behalte Version aus `feature/titel-webentwickler`
- **Accept Both Changes** – Behalte beide Versionen (meist nicht sinnvoll)
- **Compare Changes** – Zeige Unterschiede an

---

### Teil 5: Konflikt lösen – Manuelle Auflösung (15 Min)

**5.1 Entscheidung treffen**

Du hast drei Optionen:
1. Version aus `main` behalten (mit persönlichem Namen)
2. Version aus Branch behalten (mit Berufsbezeichnung)
3. Beide kombinieren (beste Lösung!)

**Wir kombinieren beide Versionen:** Persönlicher Name + Berufsbezeichnung

**5.2 Konflikt manuell auflösen**

Lösche die Konflikt-Marker und schreibe die gewünschte Version:

**Konflikt:**
```html
<<<<<<< HEAD
        <h1>Portfolio – Tim Leibacher</h1>
=======
        <h1>Webentwickler Portfolio – Moderne Weblösungen</h1>
>>>>>>> feature/titel-webentwickler
```

**Lösung (manuell geschrieben):**
```html
        <h1>Tim Leibacher – Webentwickler Portfolio</h1>
```

**Wichtig:**
- Alle Konflikt-Marker (`<<<<<<<`, `=======`, `>>>>>>>`) müssen weg
- Nur eine Version oder eine Kombination bleibt übrig
- Der Code muss syntaktisch korrekt sein

**5.3 Datei speichern**

Speichere die Datei in VS Code (`Cmd/Ctrl + S`).

**5.4 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html
```

**Git weiss noch nicht, dass der Konflikt gelöst ist.**

---

### Teil 6: Konflikt-Lösung committen (10 Min)

**6.1 Gelöste Datei zur Staging Area**

```bash
# Gelöste Datei hinzufügen
git add index.html
```

**6.2 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   index.html
```

**Was hat sich geändert?**
- **All conflicts fixed:** Git erkennt, dass der Konflikt gelöst ist
- **you are still merging:** Der Merge ist noch nicht abgeschlossen
- **use "git commit":** Du musst jetzt den Merge-Commit erstellen

**6.3 Merge-Commit erstellen**

```bash
# Merge-Commit (Git erstellt automatisch eine Nachricht)
git commit
```

**Git öffnet einen Editor mit vorgeschlagener Commit-Nachricht:**
```
Merge branch 'feature/titel-webentwickler'

# Conflicts:
#       index.html
```

**Option 1: Standard-Nachricht übernehmen**
- Speichern und schliessen (`Esc`, dann `:wq` in Vim, oder `Ctrl+X` in Nano)

**Option 2: Nachricht anpassen**
- Füge Details hinzu, z.B.: "Titel-Konflikt gelöst: Name und Berufsbezeichnung kombiniert"
- Speichern und schliessen

**Alternativ: Nachricht direkt angeben**
```bash
git commit -m "Merge feature/titel-webentwickler - Titel-Konflikt gelöst"
```

**6.4 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**Perfekt!** Der Konflikt ist gelöst, der Merge ist abgeschlossen.

---

### Teil 7: Ergebnis prüfen (5 Min)

**7.1 Im Browser testen**

Öffne `index.html` im Browser – der kombinierte Titel ist sichtbar:
```
Tim Leibacher – Webentwickler Portfolio
```

**7.2 Historie anzeigen**

```bash
git log --oneline --graph
```

**Ausgabe:**
```
*   h9e5f21 (HEAD -> main) Merge feature/titel-webentwickler - Titel-Konflikt gelöst
|\  
| * i3d7a42 (feature/titel-webentwickler) Titel mit Berufsbezeichnung und Slogan erweitert
* | g7d2e43 Titel mit persönlichem Namen ergänzt
|/  
* f3a8b21 Impressum-Seite erstellt und im Footer verlinkt
```

**Was siehst du?**
- Merge-Commit (`h9e5f21`) verbindet zwei Branches
- Grafische Darstellung zeigt die Verzweigung
- Beide Branches wurden integriert

**7.3 Branches aufräumen**

```bash
# Beide Feature-Branches löschen
git branch -d feature/titel-portfolio
git branch -d feature/titel-webentwickler
```

---

### Teil 8: Weiterer Konflikt – CSS-Styling (20 Min)

**8.1 Zweites Szenario aufbauen**

```bash
# Branch 1: Hintergrundfarbe ändern
git checkout -b feature/dark-background

# Branch 2: Hintergrundfarbe anders ändern
git branch feature/light-background
```

**8.2 Im Branch `feature/dark-background` arbeiten**

Öffne `styles.css` (oder erstelle sie, falls nicht vorhanden) und füge hinzu:

```css
body {
    background-color: #1a1a1a;
    color: #f0f0f0;
}
```

```bash
git add styles.css
git commit -m "Dunkler Hintergrund mit hellem Text implementiert"
```

```bash
# Zu main mergen
git checkout main
git merge feature/dark-background
```

**8.3 Im Branch `feature/light-background` arbeiten**

```bash
git checkout feature/light-background
```

Öffne `styles.css` und füge hinzu (gleiche Stelle!):

```css
body {
    background-color: #ffffff;
    color: #333333;
}
```

```bash
git add styles.css
git commit -m "Heller Hintergrund mit dunklem Text implementiert"
```

**8.4 Merge versuchen → Konflikt!**

```bash
git checkout main
git merge feature/light-background
```

**Ausgabe:**
```
Auto-merging styles.css
CONFLICT (content): Merge conflict in styles.css
Automatic merge failed; fix conflicts and then commit the result.
```

**8.5 Konflikt in styles.css anschauen**

```css
<<<<<<< HEAD
body {
    background-color: #1a1a1a;
    color: #f0f0f0;
}
=======
body {
    background-color: #ffffff;
    color: #333333;
}
>>>>>>> feature/light-background
```

**8.6 Konflikt lösen**

**Entscheidung:** Du bevorzugst einen mittleren Weg – nicht zu dunkel, nicht zu hell.

**Lösung:**
```css
body {
    background-color: #f5f5f5;
    color: #2c3e50;
}
```

**8.7 Konflikt committen**

```bash
git add styles.css
git commit -m "Merge feature/light-background - Neutraler Hintergrund gewählt"
```

**8.8 Branches löschen**

```bash
git branch -d feature/dark-background
git branch -d feature/light-background
```

---

### Teil 9: Notausgang – Merge abbrechen (5 Min)

**Szenario:** Was, wenn du den Konflikt nicht sofort lösen kannst oder willst?

**9.1 Konflikt simulieren**

```bash
# Neuen Branch erstellen
git checkout -b feature/test-abort

# Kleine Änderung
echo "Test-Zeile" >> index.html
git add index.html
git commit -m "Test für Merge-Abort"

# Zu main, dort auch ändern
git checkout main
echo "Andere Zeile" >> index.html
git add index.html
git commit -m "Andere Änderung für Konflikt"

# Merge versuchen
git merge feature/test-abort
```

**Konflikt entsteht!**

**9.2 Merge abbrechen**

```bash
# Merge abbrechen und zurück zum Zustand vor Merge
git merge --abort
```

**9.3 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**Perfekt!** Alles ist zurückgesetzt, als hätte der Merge nie stattgefunden.

**9.4 Aufräumen**

```bash
# Test-Branch löschen
git branch -d feature/test-abort
```

**Wichtig:** `git merge --abort` funktioniert nur, solange du noch keinen Commit nach dem Konflikt gemacht hast.

---

### Teil 10: Finale Prüfung (5 Min)

**10.1 Branches anzeigen**

```bash
git branch
```

**Ausgabe:**
```
* main
```

**10.2 Historie anzeigen**

```bash
git log --oneline --graph
```

**Ausgabe zeigt alle Merge-Commits und Konfliktlösungen:**
```
*   k2f9e54 (HEAD -> main) Merge feature/light-background - Neutraler Hintergrund gewählt
|\  
| * j8d3c21 Heller Hintergrund mit dunklem Text implementiert
* | i7e2b43 Dunkler Hintergrund mit hellem Text implementiert
|/  
*   h9e5f21 Merge feature/titel-webentwickler - Titel-Konflikt gelöst
|\  
| * i3d7a42 Titel mit Berufsbezeichnung und Slogan erweitert
* | g7d2e43 Titel mit persönlichem Namen ergänzt
|/  
* f3a8b21 Impressum-Seite erstellt und im Footer verlinkt
```

---

## Erfolgskriterien

- [ ] Mindestens zwei Merge-Konflikte wurden absichtlich provoziert
- [ ] Konflikt-Marker (`<<<<<<<`, `=======`, `>>>>>>>`) wurden erkannt
- [ ] Konflikte wurden manuell im Code gelöst
- [ ] Gelöste Dateien wurden mit `git add` markiert
- [ ] Merge-Commits wurden erfolgreich erstellt
- [ ] `git merge --abort` wurde getestet und verstanden
- [ ] VS Code Merge-Tools wurden ausprobiert
- [ ] Portfolio funktioniert nach Konfliktlösung im Browser
- [ ] Alle Feature-Branches wurden gelöscht
- [ ] `git status` zeigt "nothing to commit, working tree clean"

## Tipps

- **Keine Panik bei Konflikten:** Das ist normal und lösbar
- **Konflikt-Marker genau lesen:** Verstehe, was jede Version macht
- **VS Code hilft:** Nutze die Merge-Tools für einfache Konflikte
- **Manuell besser:** Bei komplexen Konflikten manuell editieren
- **Testen nach Lösung:** Prüfe, ob der Code funktioniert
- **git merge --abort:** Notausgang bei Unsicherheit
- **Kommunikation im Team:** Sprich mit Teamkollegen bei Konflikten
- **Häufige Konflikte vermeiden:** Regelmässig mergen und kleinere Features

## Reflexionsfragen

1. Warum entstehen Merge-Konflikte? Nenne zwei typische Szenarien.
2. Was bedeuten die Konflikt-Marker `<<<<<<<`, `=======` und `>>>>>>>`?
3. Teste: Erstelle absichtlich einen Konflikt in einer anderen Datei. Wie löst du ihn?
4. Wann würdest du `git merge --abort` nutzen?
5. Wie können Teams Merge-Konflikte minimieren? Recherchiere Best Practices.

## Weiterführende Links

- [Atlassian: Merge Conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts)
- [GitHub: Resolving Merge Conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [VS Code: Merge Conflict Resolution](https://code.visualstudio.com/docs/sourcecontrol/overview#_merge-conflicts)
- [Git Documentation: Basic Merge Conflicts](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
- [Oh Shit, Git!? – Merge Conflicts](https://ohshitgit.com/#magic-time-machine)

---

**⏱️ Geschätzte Zeit:** 90-100 Minuten  
**📦 Nächster Schritt:** Optionaler Auftrag – Komplexe Branching-Strategien und Rebase!
