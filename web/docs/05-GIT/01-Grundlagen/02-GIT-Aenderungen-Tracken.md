# Auftrag 2: Änderungen tracken und Git-Workflow üben

## Ziel

Du lernst, wie du Änderungen an deinem Portfolio trackst, mehrere Commits erstellst und die Git-Historie nutzt. Du verstehst den Standard-Git-Workflow und wendest ihn praktisch an.

## Beschreibung

In Auftrag 1 hast du dein erstes Repository erstellt. Jetzt geht es darum, den täglichen Git-Workflow zu üben: Änderungen machen, Status checken, zur Staging Area hinzufügen und committen. So arbeitest du in echten Projekten!

Der Standard-Workflow sieht so aus:
1. Dateien ändern
2. `git status` – Status checken
3. `git add .` – Zur Staging Area hinzufügen
4. `git commit -m "Nachricht"` – Commit erstellen
5. Zurück zu Schritt 1

---

### Teil 1: Portfolio erweitern und tracken (15 Min)

**1.1 Kontakt-Sektion hinzufügen**

Öffne deine `index.html` und füge am Ende (vor dem schliessenden `</body>`) eine Kontakt-Sektion hinzu:

```html
<section id="kontakt">
    <h2>Kontakt</h2>
    <p>Möchtest du mit mir in Kontakt treten? Schreib mir eine Nachricht!</p>
    <address>
        <p>
            <strong>Email:</strong> 
            <a href="mailto:dein.name@example.com">dein.name@example.com</a>
        </p>
        <p>
            <strong>LinkedIn:</strong> 
            <a href="https://linkedin.com/in/deinprofil" 
               target="_blank" 
               rel="noopener noreferrer">
                linkedin.com/in/deinprofil
            </a>
        </p>
        <p>
            <strong>GitHub:</strong> 
            <a href="https://github.com/deinusername" 
               target="_blank" 
               rel="noopener noreferrer">
                github.com/deinusername
            </a>
        </p>
    </address>
</section>
```

**Wichtig:** Ersetze die Platzhalter mit deinen echten Daten!

**1.2 Navigation aktualisieren**

Aktualisiere deine Navigation, um den neuen Kontakt-Link einzubinden:

```html
<nav>
    <ul>
        <li><a href="#ueber-mich">Über mich</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projekte">Projekte</a></li>
        <li><a href="#kontakt">Kontakt</a></li>
    </ul>
</nav>
```

**1.3 Änderungen checken**

```bash
# Status anzeigen
git status
```

**Erwartete Ausgabe:**
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

**Was bedeutet das?**
- **Changes not staged for commit:** Dateien wurden geändert, aber noch nicht zur Staging Area hinzugefügt
- **modified: index.html:** Die Datei index.html wurde verändert
- Git sagt dir, was du als nächstes tun sollst!

**1.4 Änderungen zur Staging Area**

```bash
# Geänderte Dateien hinzufügen
git add index.html

# Oder alle Änderungen
git add .

# Status checken
git status
```

**Erwartete Ausgabe:**
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
```

**1.5 Commit erstellen**

```bash
# Commit mit aussagekräftiger Nachricht
git commit -m "Kontakt-Sektion mit Email, LinkedIn und GitHub hinzugefügt"
```

**Erwartete Ausgabe:**
```
[main f8d2a41] Kontakt-Sektion mit Email, LinkedIn und GitHub hinzugefügt
 1 file changed, 23 insertions(+)
```

---

### Teil 2: Mehrere Änderungen gleichzeitig (15 Min)

**2.1 CSS für Kontakt-Sektion erstellen**

Öffne `styles.css` und füge Styling für die Kontakt-Sektion hinzu:

```css
/* Kontakt-Sektion */
#kontakt {
    background: linear-gradient(135deg, #376B8C, #29786A);
    color: white;
    padding: 3rem 2rem;
    text-align: center;
}

#kontakt h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
}

#kontakt address {
    font-style: normal;
    margin-top: 2rem;
}

#kontakt a {
    color: #FFD700;
    text-decoration: none;
    transition: color 0.3s;
}

#kontakt a:hover {
    color: #FFA500;
    text-decoration: underline;
}
```

**2.2 JavaScript für interaktive Email hinzufügen**

Öffne `script.js` und füge eine kleine Interaktivität hinzu:

```javascript
// Kontakt-Interaktivität
console.log("Kontakt-Sektion geladen");

// Email-Schutz vor Spam-Bots (simple Variante)
document.addEventListener("DOMContentLoaded", function() {
    const emailLinks = document.querySelectorAll('a[href^="mailto:"]');
    
    emailLinks.forEach(link => {
        link.addEventListener('click', function() {
            console.log("Email-Link wurde geklickt");
        });
    });
});
```

**2.3 Alle Änderungen auf einmal committen**

```bash
# Status checken (zwei Dateien geändert!)
git status

# Alle Änderungen zur Staging Area
git add .

# Status nochmal checken
git status

# Commit mit Nachricht
git commit -m "Styling und Interaktivität für Kontakt-Sektion implementiert"
```

**Erwartete Ausgabe:**
```
[main c4b7e93] Styling und Interaktivität für Kontakt-Sektion implementiert
 2 files changed, 31 insertions(+)
```

---

### Teil 3: Git-Historie erkunden (10 Min)

**3.1 Alle Commits anzeigen**

```bash
# Vollständige Historie
git log
```

**Erwartete Ausgabe:**
```
commit c4b7e93d8f2a1b5e6c3d9a7f4e2b8c1d5a6e3f9b
Author: Dein Name <deine.email@example.com>
Date:   Mon Nov 25 15:45:32 2025 +0100

    Styling und Interaktivität für Kontakt-Sektion implementiert

commit f8d2a41e9c3b7d1f5a8e2c6b4d9f7a3e1c8b5d2a
Author: Dein Name <deine.email@example.com>
Date:   Mon Nov 25 15:30:18 2025 +0100

    Kontakt-Sektion mit Email, LinkedIn und GitHub hinzugefügt

commit a3f5e21b8c9d4f6e3a2b1c0d9e8f7a6b5c4d3e2f
Author: Dein Name <deine.email@example.com>
Date:   Mon Nov 25 14:23:10 2025 +0100

    Initiales Portfolio mit HTML, CSS und JavaScript
```

**3.2 Kompakte Historie**

```bash
# Nur eine Zeile pro Commit
git log --oneline
```

**Erwartete Ausgabe:**
```
c4b7e93 Styling und Interaktivität für Kontakt-Sektion implementiert
f8d2a41 Kontakt-Sektion mit Email, LinkedIn und GitHub hinzugefügt
a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

**3.3 Letzte n Commits anzeigen**

```bash
# Nur die letzten 2 Commits
git log --oneline -2

# Nur der letzte Commit
git log --oneline -1
```

**3.4 Detaillierte Änderungen anzeigen**

```bash
# Zeige was in jedem Commit geändert wurde
git log -p

# Zeige Statistiken (wie viele Zeilen geändert)
git log --stat
```

---

### Teil 4: Workflow-Simulation mit mehreren Commits (15 Min)

Jetzt übst du den kompletten Workflow mit mehreren kleinen Änderungen.

**4.1 Änderung 1: Footer hinzufügen**

Füge in `index.html` einen Footer hinzu (vor dem schliessenden `</body>`):

```html
<footer>
    <p>&copy; 2025 Dein Name. Erstellt im Rahmen der Informatik-Lehre bei BAND.</p>
</footer>
```

**Workflow ausführen:**
```bash
git status                           # Was wurde geändert?
git add index.html                   # Zur Staging Area
git commit -m "Footer mit Copyright-Hinweis hinzugefügt"
```

**4.2 Änderung 2: Footer stylen**

Füge in `styles.css` Styling für den Footer hinzu:

```css
/* Footer */
footer {
    background-color: #2C3E50;
    color: white;
    text-align: center;
    padding: 2rem;
    margin-top: 3rem;
}

footer p {
    margin: 0;
    font-size: 0.9rem;
}
```

**Workflow ausführen:**
```bash
git status
git add styles.css
git commit -m "Footer-Styling mit dunklem Hintergrund implementiert"
```

**4.3 Änderung 3: README.md erstellen**

Erstelle eine neue Datei `README.md` im Projektordner:

```markdown
# Mein Portfolio

Persönliche Portfolio-Website erstellt im 1. Lehrjahr der Informatik-Lehre.

## Technologien

- HTML5
- CSS3
- JavaScript (ES6+)
- Git für Versionskontrolle

## Projektstruktur

```
mein-portfolio/
├── index.html
├── styles.css
├── script.js
├── images/
└── README.md
```

## Autor

Dein Name - Informatiker/in EFZ Applikationsentwicklung bei BAND

## Lizenz

Dieses Projekt ist für Lernzwecke erstellt.
```

**Workflow ausführen:**
```bash
git status                          # Neue Datei wird als "untracked" angezeigt
git add README.md
git commit -m "README mit Projektbeschreibung und Technologie-Stack erstellt"
```

**4.4 Historie überprüfen**

```bash
# Alle Commits anzeigen
git log --oneline

# Erwartete Ausgabe (deine Hashes werden anders sein):
# 8a9f2e1 README mit Projektbeschreibung und Technologie-Stack erstellt
# 5d3c7b4 Footer-Styling mit dunklem Hintergrund implementiert
# 2f8e9a6 Footer mit Copyright-Hinweis hinzugefügt
# c4b7e93 Styling und Interaktivität für Kontakt-Sektion implementiert
# f8d2a41 Kontakt-Sektion mit Email, LinkedIn und GitHub hinzugefügt
# a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

---

## Erfolgskriterien

- [ ] Mindestens 6 Commits wurden erstellt (Initiales + 5 neue)
- [ ] Kontakt-Sektion mit HTML, CSS und JS wurde hinzugefügt
- [ ] Footer mit Copyright-Hinweis und Styling existiert
- [ ] README.md wurde erstellt und gecommittet
- [ ] Alle Commits haben aussagekräftige Nachrichten
- [ ] `git log --oneline` zeigt die komplette Historie
- [ ] `git status` zeigt "nothing to commit, working tree clean"

## Tipps

- **Committe oft!** Nach jeder funktionierenden Änderung solltest du committen
- **Eine Änderung = Ein Commit:** Vermeide Mega-Commits mit 10 verschiedenen Änderungen
- **Gute Commit-Nachrichten:** Beginne mit einem Verb, sei konkret
- **`git status` vor jedem Commit:** So siehst du genau, was du committen wirst
- **Fehler gemacht?** 
  - `git restore <datei>` verwirft Änderungen an einer Datei
  - `git restore --staged <datei>` entfernt Datei aus Staging Area
- **VS Code Integration:** Nutze den Quellcodeverwaltung-Tab für einen visuellen Workflow

## Reflexionsfragen

1. Warum ist es besser, viele kleine Commits zu machen statt einen grossen?
2. Was passiert mit deinen Änderungen, wenn du `git add` machst, aber NICHT commitest?
3. Teste: Ändere eine Datei und führe dann `git restore <datei>` aus. Was passiert?
4. Schaue dir `git log -p` an. Was siehst du? Wofür könnte das nützlich sein?
5. Vergleiche: Was ist der Unterschied zwischen `git log` und `git status`?

## Weiterführende Links

- [Git Basics – Recording Changes](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
- [Git Cheat Sheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf)
- [Understanding Git – Data Model](https://www.sbf5.com/~cduan/technical/git/)
- [Pro Git Book (Kostenlos online)](https://git-scm.com/book/de/v2)
- [Git Visualizer – Siehe Commits visuell](https://git-school.github.io/visualizing-git/)

---

**⏱️ Geschätzte Zeit:** 50-60 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 lernst du, wie du zwischen verschiedenen Versionen wechselst und Änderungen rückgängig machst!
