# Auftrag 4 (Optional): Git Rebase & professionelle Branching-Strategien

## Ziel

Du lernst fortgeschrittene Git-Techniken wie Rebase, interaktives Rebase und professionelle Branching-Strategien für Teamprojekte. Dieser Auftrag vertieft dein Verständnis für saubere Git-Historien.

## Beschreibung

Merge ist nicht die einzige Möglichkeit, Branches zu integrieren. Mit `git rebase` kannst du eine lineare Historie erstellen, was in professionellen Projekten oft bevorzugt wird. Dieser optionale Auftrag zeigt dir, wie Rebase funktioniert, wann du es nutzen solltest, und welche Branching-Strategien in der Industrie Standard sind (Git Flow, GitHub Flow, Trunk-Based Development).

**Wichtig:** Rebase ist mächtiger, aber auch riskanter als Merge. Nutze es nur, wenn du die Konzepte verstanden hast.

---

### Teil 1: Rebase verstehen – Was ist der Unterschied zu Merge? (10 Min)

**1.1 Merge vs. Rebase – Konzeptueller Unterschied**

**Merge:**
```
main:     A --- B --- C -------- E
                 \              /
feature:          D1 --- D2 ---
```
- Erstellt einen Merge-Commit (E)
- Beide Branch-Historien bleiben erhalten
- Nicht-lineare Historie

**Rebase:**
```
main:     A --- B --- C
                       \
feature:                D1' --- D2'
```
- Verschiebt Feature-Commits auf die Spitze von main
- Lineare Historie (kein Merge-Commit)
- Sauberer, aber verändert Commit-Hashes

**Wann welche Strategie?**
- **Merge:** Für öffentliche Branches, Teamarbeit, Historie bewahren
- **Rebase:** Für lokale Branches, saubere Historie, vor Pull Requests

**1.2 Wichtigste Regel**

**NIEMALS rebasen auf öffentlichen/geteilten Branches!**

Warum? Rebase verändert Commit-Hashes. Wenn andere Entwickler auf denselben Commits arbeiten, entstehen massive Konflikte.

**Sichere Nutzung:**
- Rebase nur lokale Branches, die du noch nicht gepusht hast
- Oder: Rebase nur deine eigenen Feature-Branches, bevor du sie zur Review gibst

---

### Teil 2: Szenario aufbauen für Rebase-Demo (15 Min)

**2.1 Repository vorbereiten**

```bash
# Sicherstellen, dass du auf main bist
git checkout main

# Status checken
git status
```

**2.2 Basis-Commits in main erstellen**

```bash
# Commit 1: README aktualisieren
echo "# Mein Portfolio - Git Branching Demo" > README.md
git add README.md
git commit -m "README mit Projekt-Titel erstellt"

# Commit 2: .gitignore erweitern
echo "node_modules/" >> .gitignore
echo ".DS_Store" >> .gitignore
git add .gitignore
git commit -m "gitignore für Node.js und macOS erweitert"
```

**2.3 Feature-Branch erstellen (vor den neuen main-Commits)**

Jetzt erstellen wir einen Branch, der auf einem älteren Zustand basiert:

```bash
# Einen Commit zurückgehen
git checkout HEAD~2

# Neuen Branch von hier aus erstellen
git checkout -b feature/kontaktformular-styling

# (Alternativ: git checkout -b feature/kontaktformular-styling HEAD~2)
```

**Erklärung:** `HEAD~2` bedeutet "zwei Commits vor dem aktuellen HEAD". Unser Feature-Branch basiert jetzt auf einem älteren Stand von main.

**2.4 Im Feature-Branch arbeiten**

Erstelle/erweitere `styles.css`:

```css
/* Kontaktformular-Styling */
#kontakt form {
    max-width: 600px;
    margin: 2rem auto;
    padding: 2rem;
    background: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

#kontakt label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: bold;
    color: #333;
}

#kontakt input,
#kontakt textarea {
    width: 100%;
    padding: 0.75rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: inherit;
    font-size: 1rem;
}

#kontakt button {
    background-color: #376B8C;
    color: white;
    padding: 0.75rem 2rem;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;
}

#kontakt button:hover {
    background-color: #29786A;
}
```

```bash
git add styles.css
git commit -m "Kontaktformular-Styling mit BAND-Farben implementiert"
```

**2.5 Zweiter Commit im Feature-Branch**

Füge Validierung in `script.js` hinzu:

```javascript
// Formular-Validierung
document.addEventListener('DOMContentLoaded', function() {
    const form = document.querySelector('#kontakt form');
    
    if (form) {
        form.addEventListener('submit', function(event) {
            event.preventDefault();
            
            const name = document.getElementById('name').value.trim();
            const email = document.getElementById('email').value.trim();
            const nachricht = document.getElementById('nachricht').value.trim();
            
            // Einfache Validierung
            if (!name || !email || !nachricht) {
                alert('Bitte fülle alle Felder aus.');
                return;
            }
            
            if (!email.includes('@')) {
                alert('Bitte gib eine gültige Email-Adresse ein.');
                return;
            }
            
            alert('Nachricht wurde erfolgreich gesendet!');
            form.reset();
        });
    }
});
```

```bash
git add script.js
git commit -m "Formular-Validierung mit Client-Side-Check hinzugefügt"
```

**2.6 Situation visualisieren**

```bash
git log --oneline --graph --all
```

**Ausgabe:**
```
* n7f4e21 (HEAD -> feature/kontaktformular-styling) Formular-Validierung mit Client-Side-Check hinzugefügt
* m3d8a19 Kontaktformular-Styling mit BAND-Farben implementiert
| * k9e2b43 (main) gitignore für Node.js und macOS erweitert
| * j5c7d31 README mit Projekt-Titel erstellt
|/  
* h9e5f21 Merge feature/titel-webentwickler - Titel-Konflikt gelöst
```

**Was siehst du?**
- Feature-Branch basiert auf älterem Zustand
- main hat zwei neue Commits
- Die Branches haben sich auseinanderentwickelt

---

### Teil 3: Rebase durchführen (15 Min)

**3.1 Feature-Branch auf main rebasen**

```bash
# Sicherstellen, dass du im Feature-Branch bist
git checkout feature/kontaktformular-styling

# Rebase auf main
git rebase main
```

**Erwartete Ausgabe:**
```
Successfully rebased and updated refs/heads/feature/kontaktformular-styling.
```

**Was ist passiert?**
- Git hat die zwei Feature-Commits "abgehoben"
- Die neuen main-Commits wurden integriert
- Die Feature-Commits wurden auf die neue Spitze von main "aufgesetzt"
- Die Commit-Hashes haben sich geändert!

**3.2 Historie nach Rebase**

```bash
git log --oneline --graph --all
```

**Ausgabe:**
```
* p8g3f42 (HEAD -> feature/kontaktformular-styling) Formular-Validierung mit Client-Side-Check hinzugefügt
* o2d7e31 Kontaktformular-Styling mit BAND-Farben implementiert
* k9e2b43 (main) gitignore für Node.js und macOS erweitert
* j5c7d31 README mit Projekt-Titel erstellt
* h9e5f21 Merge feature/titel-webentwickler - Titel-Konflikt gelöst
```

**Was ist neu?**
- Lineare Historie!
- Feature-Commits sind jetzt "nach" den main-Commits
- Keine Merge-Verzweigung
- Commit-Hashes haben sich geändert (m3d8a19 → o2d7e31)

**3.3 Zu main mergen (Fast-Forward)**

```bash
git checkout main
git merge feature/kontaktformular-styling
```

**Ausgabe:**
```
Updating k9e2b43..p8g3f42
Fast-forward
 script.js  | 21 +++++++++++++++++++++
 styles.css | 35 +++++++++++++++++++++++++++++++++++
 2 files changed, 56 insertions(+)
```

**Perfekt!** Fast-Forward-Merge ohne Merge-Commit – saubere, lineare Historie.

```bash
git branch -d feature/kontaktformular-styling
```

---

### Teil 4: Rebase mit Konflikten (20 Min)

**4.1 Szenario mit Konflikt aufbauen**

```bash
# In main arbeiten
git checkout main

# Datei ändern
echo "footer { background: #333; }" >> styles.css
git add styles.css
git commit -m "Footer-Hintergrund in main geändert"

# Branch erstellen (von älterem Zustand)
git checkout HEAD~1
git checkout -b feature/footer-redesign

# Dieselbe Datei anders ändern
echo "footer { background: #1a1a1a; color: white; }" >> styles.css
git add styles.css
git commit -m "Footer-Design mit dunklem Hintergrund in Branch"
```

**4.2 Rebase mit Konflikt**

```bash
git rebase main
```

**Ausgabe:**
```
Auto-merging styles.css
CONFLICT (content): Merge conflict in styles.css
error: could not apply... Footer-Design mit dunklem Hintergrund in Branch
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply... Footer-Design mit dunklem Hintergrund in Branch
```

**Was ist passiert?**
- Rebase hat einen Konflikt gefunden
- Git hat angehalten und wartet auf deine Lösung
- Du hast drei Optionen:
  1. Konflikt lösen und `git rebase --continue`
  2. Commit überspringen mit `git rebase --skip`
  3. Rebase abbrechen mit `git rebase --abort`

**4.3 Konflikt lösen**

Öffne `styles.css` und löse den Konflikt:

```css
footer { background: #1a1a1a; color: white; }
```

```bash
# Konflikt gelöst, Datei markieren
git add styles.css

# Rebase fortsetzen
git rebase --continue
```

**Ausgabe:**
```
Successfully rebased and updated refs/heads/feature/footer-redesign.
```

**4.4 Mergen und aufräumen**

```bash
git checkout main
git merge feature/footer-redesign
git branch -d feature/footer-redesign
```

---

### Teil 5: Interaktives Rebase – Commits aufräumen (20 Min)

**5.1 Szenario: Mehrere unordentliche Commits**

```bash
git checkout -b feature/navigation-fixes

# Mehrere kleine Commits (absichtlich unordentlich)
echo "/* Nav Fix 1 */" >> styles.css
git add styles.css
git commit -m "Nav fix"

echo "/* Nav Fix 2 */" >> styles.css
git add styles.css
git commit -m "Another nav fix"

echo "/* Nav Fix 3 */" >> styles.css
git add styles.css
git commit -m "Final nav fix"

echo "/* Nav Cleanup */" >> styles.css
git add styles.css
git commit -m "Typo fixed"
```

**Problem:** Vier kleine Commits für eine Aufgabe – unübersichtlich!

**5.2 Interaktives Rebase starten**

```bash
# Letzten 4 Commits interaktiv bearbeiten
git rebase -i HEAD~4
```

**Git öffnet einen Editor mit:**
```
pick abc1234 Nav fix
pick def5678 Another nav fix
pick ghi9012 Final nav fix
pick jkl3456 Typo fixed

# Rebase instructions...
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash" but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

**5.3 Commits zusammenfassen (squash)**

Ändere die Datei zu:
```
pick abc1234 Nav fix
squash def5678 Another nav fix
squash ghi9012 Final nav fix
squash jkl3456 Typo fixed
```

**Alternativ (kürzer):**
```
pick abc1234 Nav fix
s def5678 Another nav fix
s ghi9012 Final nav fix
s jkl3456 Typo fixed
```

Speichern und schliessen.

**5.4 Commit-Nachricht anpassen**

Git öffnet einen zweiten Editor:
```
# This is a combination of 4 commits.
# The first commit's message is:
Nav fix

# This is the 2nd commit message:
Another nav fix

# This is the 3rd commit message:
Final nav fix

# This is the 4th commit message:
Typo fixed
```

**Ersetze alles mit einer sauberen Nachricht:**
```
Navigation-Styling vollständig überarbeitet

- Flexbox-Layout für bessere Ausrichtung
- Responsive Breakpoints hinzugefügt
- Hover-Effekte mit BAND-Farben
- Barrierefreiheit verbessert
```

Speichern und schliessen.

**5.5 Ergebnis prüfen**

```bash
git log --oneline
```

**Vorher:** 4 kleine Commits  
**Nachher:** 1 sauberer Commit

**5.6 Zu main mergen**

```bash
git checkout main
git merge feature/navigation-fixes
git branch -d feature/navigation-fixes
```

---

### Teil 6: Professionelle Branching-Strategien (15 Min)

**6.1 Git Flow – Klassische Strategie für grosse Teams**

**Branch-Typen:**
- `main` (oder `master`) – Produktions-Code
- `develop` – Entwicklungs-Zweig
- `feature/*` – Neue Features
- `release/*` – Release-Vorbereitung
- `hotfix/*` – Dringende Bugfixes

**Workflow:**
1. Features von `develop` abzweigen
2. Features zurück in `develop` mergen
3. Release von `develop` abzweigen
4. Release in `main` UND `develop` mergen
5. Hotfixes von `main` abzweigen, zurück in `main` und `develop` mergen

**Visualisierung:**
```
main:      A ----------- D ----------- G
            \           /             /
release:     \         C             /
              \       /             /
develop:       B -------- E ------- F
                \        /
feature:         X --- Y
```

**Wann nutzen?**
- Grosse Teams
- Mehrere parallele Releases
- Strikte Release-Zyklen

**6.2 GitHub Flow – Einfache Strategie**

**Branch-Typen:**
- `main` – Immer deploybar
- `feature/*` – Alle Features und Fixes

**Workflow:**
1. Feature-Branch von `main` erstellen
2. Commits erstellen
3. Pull Request öffnen
4. Code Review
5. Merge in `main`
6. Deploy automatisch

**Visualisierung:**
```
main:      A --- B --- C ------- D
                \             /
feature:         E --- F ----
```

**Wann nutzen?**
- Continuous Deployment
- Kleine bis mittelgrosse Teams
- Einfache Projekte

**6.3 Trunk-Based Development – Moderne Strategie**

**Prinzip:**
- Alle entwickeln direkt in `main` (oder sehr kurzlebige Branches)
- Feature Flags für unfertige Features
- Sehr häufige Commits (mehrmals täglich)

**Workflow:**
1. Kleine Feature-Branch (<24h Lebensdauer)
2. Schnelles Merge in `main`
3. Feature Flags für Steuerung

**Wann nutzen?**
- Sehr erfahrene Teams
- Starke CI/CD-Pipeline
- Feature-Flag-Infrastruktur vorhanden

---

### Teil 7: Best Practices & Reflexion (10 Min)

**7.1 Dos & Don'ts für Rebase**

**✅ Dos:**
- Rebase lokale Branches vor dem Teilen
- Rebase Feature-Branches vor Pull Requests (für saubere Historie)
- Nutze `git rebase -i` für Commit-Hygiene

**❌ Don'ts:**
- NIEMALS öffentliche/geteilte Branches rebasen
- Kein Rebase, wenn andere auf deinem Branch arbeiten
- Kein Rebase bei Unsicherheit – nutze Merge

**7.2 Wann Merge, wann Rebase?**

**Merge nutzen:**
- Öffentliche Branches
- Teamarbeit
- Historie dokumentieren wichtig
- Bei Unsicherheit

**Rebase nutzen:**
- Lokale Feature-Branches
- Saubere Historie gewünscht
- Vor Pull Requests
- Du bist allein am Branch

**7.3 Kommandoübersicht**

```bash
# Rebase
git rebase main                    # Branch auf main rebasen
git rebase --continue              # Nach Konflikt fortsetzen
git rebase --abort                 # Rebase abbrechen
git rebase -i HEAD~n               # Interaktives Rebase (letzte n Commits)

# Squashing (interaktives Rebase)
git rebase -i HEAD~4               # Letzte 4 Commits bearbeiten
# Im Editor: pick → squash/fixup

# Branching-Strategien
git flow init                      # Git Flow initialisieren (Tool)
git checkout -b feature/...        # Feature-Branch (GitHub Flow)
```

---

## Erfolgskriterien

- [ ] Unterschied zwischen Merge und Rebase verstanden
- [ ] Feature-Branch erfolgreich auf main rebased
- [ ] Rebase mit Konflikt gelöst (`git rebase --continue`)
- [ ] Interaktives Rebase genutzt (`git rebase -i`)
- [ ] Mehrere Commits mit squash kombiniert
- [ ] Git Flow, GitHub Flow und Trunk-Based Development verstanden
- [ ] Vor- und Nachteile der Strategien erkannt
- [ ] Wann Rebase und wann Merge zu nutzen ist klar
- [ ] Lineare Git-Historie nach Rebase erstellt
- [ ] Repository ist aufgeräumt und funktional

## Tipps

- **Rebase-Regel:** Nur lokale Branches rebasen!
- **Squash für Cleanup:** Nutze `git rebase -i` vor Pull Requests
- **Bei Konflikten:** `git rebase --abort` ist dein Freund
- **Visualisierung:** `git log --graph --all` zeigt Historie
- **Profitipp:** Erstelle Alias für häufige Rebase-Befehle
- **Team-Absprache:** Kläre Branching-Strategie im Team
- **Git Flow Tool:** Nutze `git flow` für einfacheren Workflow
- **Commits früh kombinieren:** Vor dem Pushen aufräumen

## Reflexionsfragen

1. Warum ist es gefährlich, öffentliche Branches zu rebasen?
2. Wann würdest du Rebase statt Merge nutzen? Nenne drei Szenarien.
3. Recherchiere: Was ist der Unterschied zwischen `squash` und `fixup` in interaktivem Rebase?
4. Welche Branching-Strategie würdest du für ein kleines Startup wählen? Warum?
5. Was sind Feature Flags und wie helfen sie bei Trunk-Based Development?

## Weiterführende Links

- [Atlassian: Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Git Rebase Documentation](https://git-scm.com/docs/git-rebase)
- [Git Flow Cheat Sheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
- [Interactive Rebase Tutorial](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
- [When to Use Git Rebase vs. Merge](https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase)

---

**⏱️ Geschätzte Zeit:** 100-120 Minuten  
**📦 Nächstes Kapitel:** Node.js & Express – Backend-Entwicklung beginnt!
