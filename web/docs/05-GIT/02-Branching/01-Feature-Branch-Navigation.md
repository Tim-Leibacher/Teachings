# Auftrag 1: Feature-Branch für erweiterte Navigation

## Ziel

Du erstellst deinen ersten Feature-Branch, arbeitest darin an einer erweiterten Navigation für dein Portfolio und führst den Branch anschliessend zurück in den Hauptzweig.

## Beschreibung

Bisher hast du direkt im `main`-Branch gearbeitet. In der professionellen Softwareentwicklung ist das riskant – ein Fehler könnte den stabilen Code beschädigen. Mit Feature-Branches arbeitest du sicher: Experimentiere im Branch, und merge erst, wenn alles funktioniert. In diesem Auftrag erstellst du einen Branch für eine verbesserte Navigation mit Icons und mobilem Menü.

---

### Teil 1: Ausgangslage prüfen (5 Min)

**1.1 Repository-Status checken**

Öffne dein Terminal im Portfolio-Ordner und prüfe den Status:

```bash
# Aktuellen Branch anzeigen
git status

# Alle Branches anzeigen
git branch
```

**Erwartete Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

Und:
```
* main
```

**Was bedeutet das?**
- Du bist auf dem `main`-Branch (Stern `*`)
- Alle Änderungen sind committed
- Du kannst sauber einen neuen Branch erstellen

**1.2 Falls Änderungen vorhanden sind**

Wenn `git status` Änderungen zeigt:

```bash
# Änderungen committen
git add .
git commit -m "Änderungen vor Branch-Erstellung gesichert"
```

**Wichtig:** Erstelle Branches immer mit sauberem Working Directory!

---

### Teil 2: Feature-Branch erstellen (10 Min)

**2.1 Branch erstellen**

```bash
# Neuen Branch erstellen
git branch feature/navigation-verbessern

# Alle Branches anzeigen
git branch
```

**Erwartete Ausgabe:**
```
  feature/navigation-verbessern
* main
```

**Was siehst du?**
- Der neue Branch existiert
- Du bist aber noch auf `main` (Stern bei main)

**2.2 Zu Feature-Branch wechseln**

```bash
# Zu neuem Branch wechseln
git checkout feature/navigation-verbessern

# Status checken
git branch
```

**Erwartete Ausgabe:**
```
Switched to branch 'feature/navigation-verbessern'
```

Und:
```
* feature/navigation-verbessern
  main
```

**Jetzt bist du im Feature-Branch!** Alle Änderungen passieren hier, `main` bleibt unberührt.

**Shortcut (zum Merken):**
```bash
# Branch erstellen UND wechseln in einem Befehl
git checkout -b feature/navigation-verbessern
```

---

### Teil 3: Navigation erweitern (20 Min)

**3.1 Neue Navigations-Struktur**

Öffne deine `index.html` und ersetze die bestehende `<nav>` mit dieser erweiterten Version:

```html
<nav>
    <div class="nav-container">
        <div class="nav-logo">
            <a href="#home">Mein Portfolio</a>
        </div>
        
        <button class="nav-toggle" aria-label="Navigation umschalten">
            ☰
        </button>
        
        <ul class="nav-menu">
            <li><a href="#home">🏠 Start</a></li>
            <li><a href="#ueber-mich">👤 Über mich</a></li>
            <li><a href="#skills">💡 Skills</a></li>
            <li><a href="#projekte">📁 Projekte</a></li>
            <li><a href="#kontakt">✉️ Kontakt</a></li>
        </ul>
    </div>
</nav>
```

**Was ist neu?**
- Navigation mit Container für besseres Layout
- Logo/Brand-Bereich
- Mobile-Menu-Button (für später mit JavaScript)
- Icons bei den Links (Emojis als Platzhalter)
- Semantische Klassen für CSS

**3.2 Status checken**

```bash
# Was wurde geändert?
git status
```

**Erwartete Ausgabe:**
```
On branch feature/navigation-verbessern
Changes not staged for commit:
        modified:   index.html
```

**3.3 Änderungen committen**

```bash
# Zur Staging Area hinzufügen
git add index.html

# Commit erstellen
git commit -m "Navigation mit Icons und mobilem Menü-Button erweitert"
```

**Erwartete Ausgabe:**
```
[feature/navigation-verbessern a7f3e21] Navigation mit Icons und mobilem Menü-Button erweitert
 1 file changed, 15 insertions(+), 5 deletions(-)
```

---

### Teil 4: Weitere Verbesserungen (15 Min)

**4.1 JavaScript für mobiles Menü**

Erstelle eine neue Datei `navigation.js` oder füge zu deiner bestehenden `script.js` hinzu:

```javascript
// Navigation Toggle für Mobile
document.addEventListener('DOMContentLoaded', function() {
    const navToggle = document.querySelector('.nav-toggle');
    const navMenu = document.querySelector('.nav-menu');
    
    if (navToggle && navMenu) {
        navToggle.addEventListener('click', function() {
            navMenu.classList.toggle('active');
            
            // Aria-Label anpassen
            const isOpen = navMenu.classList.contains('active');
            navToggle.setAttribute('aria-expanded', isOpen);
        });
        
        // Menü schliessen beim Klick auf einen Link
        const navLinks = document.querySelectorAll('.nav-menu a');
        navLinks.forEach(link => {
            link.addEventListener('click', function() {
                navMenu.classList.remove('active');
                navToggle.setAttribute('aria-expanded', 'false');
            });
        });
    }
});
```

**4.2 JavaScript einbinden (falls neue Datei)**

Falls du `navigation.js` erstellt hast, binde sie in `index.html` ein:

```html
<script src="navigation.js"></script>
```

**4.3 Änderungen committen**

```bash
# Status checken
git status

# Alle neuen/geänderten Dateien hinzufügen
git add .

# Commit erstellen
git commit -m "JavaScript für mobiles Menü implementiert"
```

---

### Teil 5: Branch-Historie anzeigen (5 Min)

**5.1 Commit-Historie im Feature-Branch**

```bash
# Kompakte Historie
git log --oneline
```

**Beispiel-Ausgabe:**
```
b8f4e32 (HEAD -> feature/navigation-verbessern) JavaScript für mobiles Menü implementiert
a7f3e21 Navigation mit Icons und mobilem Menü-Button erweitert
c4b7e93 (main) Initiales Portfolio mit HTML, CSS und JavaScript
```

**Was siehst du?**
- Zwei neue Commits im Feature-Branch
- `HEAD ->` zeigt, wo du gerade bist
- `main` ist zwei Commits "hinterher"

**5.2 Grafische Historie (alle Branches)**

```bash
# Visualisierung mit allen Branches
git log --oneline --graph --all
```

**Beispiel-Ausgabe:**
```
* b8f4e32 (HEAD -> feature/navigation-verbessern) JavaScript für mobiles Menü implementiert
* a7f3e21 Navigation mit Icons und mobilem Menü-Button erweitert
* c4b7e93 (main) Initiales Portfolio mit HTML, CSS und JavaScript
```

**Erklärung:**
- `*` zeigt Commits
- Grafische Darstellung zeigt Branch-Struktur
- Noch keine Verzweigung sichtbar (linearer Verlauf)

---

### Teil 6: Feature testen (5 Min)

**6.1 Portfolio im Browser testen**

1. Öffne `index.html` im Browser
2. Prüfe die neue Navigation:
   - Sind die Icons sichtbar?
   - Funktionieren alle Links?
   - Funktioniert der Mobile-Toggle-Button?
3. Teste auf mobilem Viewport (Browser-DevTools: `F12` → Device Toolbar)

**6.2 Fehler gefunden?**

Falls du Fehler findest:
1. Behebe den Fehler
2. `git add .`
3. `git commit -m "Bug in Navigation behoben"`

**Tipp:** Committe oft! Jeder funktionierende Zustand = Ein Commit

---

### Teil 7: Feature in main mergen (10 Min)

**7.1 Zu main wechseln**

```bash
# Zurück zu main
git checkout main
```

**Ausgabe:**
```
Switched to branch 'main'
```

**Jetzt im Browser checken:** Öffne `index.html` – die neue Navigation ist NICHT da! Das ist korrekt, weil du sie nur im Feature-Branch erstellt hast.

**7.2 Feature-Branch mergen**

```bash
# Feature-Branch in main integrieren
git merge feature/navigation-verbessern
```

**Ausgabe (Fast-Forward-Merge):**
```
Updating c4b7e93..b8f4e32
Fast-forward
 index.html      | 20 +++++++++++++-------
 navigation.js   | 21 +++++++++++++++++++++
 2 files changed, 34 insertions(+), 7 deletions(-)
 create mode 100644 navigation.js
```

**Was bedeutet "Fast-forward"?**
- Git verschiebt `main` einfach vorwärts
- Keine Merge-Konflikte
- Linearer Verlauf bleibt erhalten

**7.3 Im Browser testen**

Lade `index.html` neu im Browser – jetzt ist die neue Navigation da!

**7.4 Feature-Branch löschen**

```bash
# Branch löschen (sicher)
git branch -d feature/navigation-verbessern
```

**Ausgabe:**
```
Deleted branch feature/navigation-verbessern (was b8f4e32).
```

```bash
# Branches anzeigen
git branch
```

**Ausgabe:**
```
* main
```

**Perfekt!** Nur noch `main` ist übrig, aber alle Änderungen sind integriert.

---

### Teil 8: Abschliessende Prüfung (5 Min)

**8.1 Finale Commit-Historie**

```bash
# Vollständige Historie anzeigen
git log --oneline
```

**Erwartete Ausgabe:**
```
b8f4e32 (HEAD -> main) JavaScript für mobiles Menü implementiert
a7f3e21 Navigation mit Icons und mobilem Menü-Button erweitert
c4b7e93 Initiales Portfolio mit HTML, CSS und JavaScript
```

**8.2 Status checken**

```bash
git status
```

**Erwartete Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**Perfekt!** Alles ist committed und gemergt.

---

## Erfolgskriterien

- [ ] Feature-Branch `feature/navigation-verbessern` wurde erstellt
- [ ] Navigation wurde mit Icons und mobilem Menü erweitert
- [ ] JavaScript für Mobile-Toggle wurde implementiert
- [ ] Mindestens 2 Commits wurden im Feature-Branch erstellt
- [ ] Feature-Branch wurde erfolgreich in `main` gemergt
- [ ] Feature-Branch wurde nach Merge gelöscht
- [ ] `git log` zeigt vollständige Historie mit allen Commits
- [ ] Portfolio funktioniert im Browser mit neuer Navigation
- [ ] `git status` zeigt "nothing to commit, working tree clean"

## Tipps

- **Vor Branch-Erstellung:** Immer `git status` checken und aufräumen
- **Branch-Namen:** Nutze Präfixe wie `feature/`, `bugfix/`, `hotfix/`
- **Oft committen:** Jeder funktionierende Zustand = Ein Commit
- **Testen vor Merge:** Stelle sicher, dass alles funktioniert
- **VS Code Integration:** Unten links siehst du den aktuellen Branch
- **Shortcut:** `git checkout -b <n>` erstellt UND wechselt
- **Fehler beim Merge?** `git merge --abort` bricht Merge ab
- **Branch versehentlich gelöscht?** Mit `git reflog` kannst du ihn wiederherstellen

## Reflexionsfragen

1. Warum solltest du nicht direkt im `main`-Branch entwickeln?
2. Was ist der Unterschied zwischen `git branch` und `git checkout`?
3. Teste: Erstelle einen Branch, mache eine Änderung, wechsle zu `main` und schau dir die Datei an. Was fällt auf?
4. Was bedeutet "Fast-Forward-Merge"? Wann passiert das?
5. Warum löscht man Feature-Branches nach erfolgreichem Merge?

## Weiterführende Links

- [Learn Git Branching (Interaktiv)](https://learngitbranching.js.org/) – Übe Branching spielerisch
- [Atlassian Git Branching Tutorial](https://www.atlassian.com/git/tutorials/using-branches)
- [Git Branch Naming Conventions](https://dev.to/varbsan/a-simplified-convention-for-naming-branches-and-commits-in-git-il4)
- [Visualizing Git](https://git-school.github.io/visualizing-git/) – Siehe was Git macht
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

---

**⏱️ Geschätzte Zeit:** 60-75 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 arbeitest du parallel an mehreren Features!
