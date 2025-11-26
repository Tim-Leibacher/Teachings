# Auftrag 2: Paralleles Arbeiten mit mehreren Branches

## Ziel

Du lernst, gleichzeitig an mehreren Features zu arbeiten, indem du parallel mehrere Branches erstellst und zwischen ihnen wechselst. Das ist der professionelle Workflow in der Softwareentwicklung.

## Beschreibung

In echten Projekten arbeitest du selten nur an einem Feature. Während du auf Feedback zu Feature A wartest, beginnst du bereits mit Feature B. Oder du wechselst zwischen einer neuen Funktion und einem Bugfix. Mit Git-Branches ist das kein Problem: Jeder Branch entwickelt sich unabhängig. In diesem Auftrag erstellst du drei parallele Branches für verschiedene Portfolio-Erweiterungen.

---

### Teil 1: Mehrere Feature-Branches erstellen (10 Min)

**1.1 Ausgangslage prüfen**

```bash
# Status checken
git status

# Auf main sein
git checkout main
```

**Erwartete Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**1.2 Drei Feature-Branches erstellen**

```bash
# Branch 1: Footer mit Social Links
git branch feature/footer-social-links

# Branch 2: Skills-Sektion mit Icons
git branch feature/skills-icons

# Branch 3: Impressum-Seite
git branch feature/impressum

# Alle Branches anzeigen
git branch
```

**Ausgabe:**
```
  feature/footer-social-links
  feature/impressum
  feature/skills-icons
* main
```

**Was siehst du?**
- Drei neue Branches existieren
- Du bist noch auf `main`
- Alle zeigen momentan auf denselben Commit

---

### Teil 2: Feature 1 – Footer mit Social Links (15 Min)

**2.1 Zu Branch wechseln**

```bash
git checkout feature/footer-social-links
```

**2.2 Footer erstellen**

Öffne `index.html` und füge vor dem schliessenden `</body>` ein:

```html
<footer>
    <div class="footer-container">
        <div class="footer-info">
            <p>&copy; 2025 Dein Name – Informatiker/in EFZ Applikationsentwicklung</p>
            <p>Erstellt im Rahmen der Ausbildung bei BAND</p>
        </div>
        
        <div class="footer-social">
            <h3>Folge mir</h3>
            <ul class="social-links">
                <li>
                    <a href="https://github.com/deinusername" 
                       target="_blank" 
                       rel="noopener noreferrer"
                       aria-label="GitHub Profil">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/>
                        </svg>
                        GitHub
                    </a>
                </li>
                <li>
                    <a href="https://linkedin.com/in/deinprofil" 
                       target="_blank" 
                       rel="noopener noreferrer"
                       aria-label="LinkedIn Profil">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                        </svg>
                        LinkedIn
                    </a>
                </li>
            </ul>
        </div>
    </div>
</footer>
```

**2.3 Änderungen committen**

```bash
git status
git add index.html
git commit -m "Footer mit Copyright und Social Media Links erstellt"
```

**2.4 Zurück zu main wechseln**

```bash
git checkout main
```

**Im Browser checken:** Der Footer ist NICHT sichtbar (korrekt, weil nur im Branch).

---

### Teil 3: Feature 2 – Skills mit Icons (15 Min)

**3.1 Zu Branch wechseln**

```bash
git checkout feature/skills-icons
```

**3.2 Skills-Sektion erweitern**

Suche in `index.html` die Skills-Sektion und ersetze sie:

```html
<section id="skills">
    <h2>Meine Skills</h2>
    
    <div class="skills-container">
        <div class="skill-card">
            <div class="skill-icon">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polygon points="12 2 2 7 12 12 22 7 12 2"></polygon>
                    <polyline points="2 17 12 22 22 17"></polyline>
                    <polyline points="2 12 12 17 22 12"></polyline>
                </svg>
            </div>
            <h3>HTML5</h3>
            <p>Semantisches HTML, Formulare, Accessibility</p>
            <div class="skill-level">
                <div class="skill-bar" style="width: 75%"></div>
            </div>
        </div>
        
        <div class="skill-card">
            <div class="skill-icon">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect>
                    <circle cx="8.5" cy="8.5" r="1.5"></circle>
                    <polyline points="21 15 16 10 5 21"></polyline>
                </svg>
            </div>
            <h3>CSS3</h3>
            <p>Flexbox, Grid, Responsive Design, Animationen</p>
            <div class="skill-level">
                <div class="skill-bar" style="width: 70%"></div>
            </div>
        </div>
        
        <div class="skill-card">
            <div class="skill-icon">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polyline points="16 18 22 12 16 6"></polyline>
                    <polyline points="8 6 2 12 8 18"></polyline>
                </svg>
            </div>
            <h3>JavaScript</h3>
            <p>ES6+, DOM-Manipulation, Event Handling</p>
            <div class="skill-level">
                <div class="skill-bar" style="width: 60%"></div>
            </div>
        </div>
        
        <div class="skill-card">
            <div class="skill-icon">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="12" cy="12" r="10"></circle>
                    <polyline points="12 6 12 12 16 14"></polyline>
                </svg>
            </div>
            <h3>Git</h3>
            <p>Versionskontrolle, Branching, Merging</p>
            <div class="skill-level">
                <div class="skill-bar" style="width: 65%"></div>
            </div>
        </div>
    </div>
</section>
```

**3.3 Änderungen committen**

```bash
git status
git add index.html
git commit -m "Skills-Sektion mit Icons und Fortschrittsbalken erweitert"
```

**3.4 Zurück zu main**

```bash
git checkout main
```

**Im Browser checken:** Die neuen Skill-Cards sind NICHT sichtbar (korrekt).

---

### Teil 4: Feature 3 – Impressum-Seite (15 Min)

**4.1 Zu Branch wechseln**

```bash
git checkout feature/impressum
```

**4.2 Neue HTML-Seite erstellen**

Erstelle eine neue Datei `impressum.html`:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Impressum – Dein Name</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <nav>
            <a href="index.html">← Zurück zum Portfolio</a>
        </nav>
        <h1>Impressum</h1>
    </header>
    
    <main>
        <section>
            <h2>Angaben gemäss Schweizer Recht</h2>
            
            <h3>Verantwortlich für den Inhalt</h3>
            <address>
                <strong>Dein Name</strong><br>
                Musterstrasse 123<br>
                3000 Bern<br>
                Schweiz<br><br>
                
                <strong>Email:</strong> <a href="mailto:dein.name@example.com">dein.name@example.com</a><br>
                <strong>Telefon:</strong> +41 XX XXX XX XX
            </address>
            
            <h3>Haftungsausschluss</h3>
            <p>
                Diese Website wurde im Rahmen der Ausbildung als Informatiker/in EFZ 
                Applikationsentwicklung erstellt und dient ausschliesslich zu Lernzwecken. 
                Der Autor übernimmt keine Gewähr für die Richtigkeit, Genauigkeit, 
                Aktualität, Zuverlässigkeit und Vollständigkeit der Informationen.
            </p>
            
            <h3>Urheberrechte</h3>
            <p>
                Die Urheber- und alle anderen Rechte an Inhalten, Bildern, Fotos oder 
                anderen Dateien auf dieser Website gehören ausschliesslich dem Betreiber 
                oder den speziell genannten Rechtsinhabern. Für die Reproduktion 
                jeglicher Elemente ist die schriftliche Zustimmung des Urheberrechtsträgers 
                im Voraus einzuholen.
            </p>
            
            <h3>Datenschutz</h3>
            <p>
                Diese Website sammelt keine personenbezogenen Daten und verwendet keine Cookies. 
                Es werden keine Analyse-Tools oder Tracking-Mechanismen eingesetzt.
            </p>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2025 Dein Name</p>
    </footer>
</body>
</html>
```

**Wichtig:** Ersetze alle Platzhalter mit deinen echten Daten!

**4.3 Link in index.html einfügen**

Öffne `index.html` und füge im Footer einen Link zum Impressum:

```html
<footer>
    <div class="footer-container">
        <!-- Bestehender Footer-Inhalt -->
        
        <div class="footer-links">
            <a href="impressum.html">Impressum</a>
        </div>
    </div>
</footer>
```

**4.4 Änderungen committen**

```bash
git status
git add .
git commit -m "Impressum-Seite erstellt und im Footer verlinkt"
```

---

### Teil 5: Branch-Überblick & Historie (10 Min)

**5.1 Alle Branches anzeigen**

```bash
# Zu main wechseln
git checkout main

# Alle Branches anzeigen
git branch
```

**Ausgabe:**
```
  feature/footer-social-links
  feature/impressum
  feature/skills-icons
* main
```

**5.2 Grafische Historie aller Branches**

```bash
git log --oneline --graph --all
```

**Beispiel-Ausgabe:**
```
* f3a8b21 (feature/impressum) Impressum-Seite erstellt und im Footer verlinkt
| * e7c4d19 (feature/skills-icons) Skills-Sektion mit Icons und Fortschrittsbalken erweitert
|/  
| * d2b9f32 (feature/footer-social-links) Footer mit Copyright und Social Media Links erstellt
|/  
* c4b7e93 (HEAD -> main) Navigation mit Icons und mobilem Menü-Button erweitert
* a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

**Was siehst du?**
- Drei parallele Branches von `main` abzweigend
- Jeder Branch hat eigene Commits
- `main` bleibt auf dem ursprünglichen Stand
- Grafische Darstellung zeigt die Verzweigung

---

### Teil 6: Features nacheinander mergen (20 Min)

**6.1 Feature 1 mergen – Footer**

```bash
# In main sein (falls nicht schon)
git checkout main

# Footer-Branch mergen
git merge feature/footer-social-links
```

**Ausgabe:**
```
Updating c4b7e93..d2b9f32
Fast-forward
 index.html | 28 ++++++++++++++++++++++++++++
 1 file changed, 28 insertions(+)
```

**Branch löschen:**
```bash
git branch -d feature/footer-social-links
```

**Im Browser testen:** Footer ist jetzt sichtbar!

**6.2 Feature 2 mergen – Skills**

```bash
# Skills-Branch mergen
git merge feature/skills-icons
```

**Ausgabe:**
```
Updating d2b9f32..e7c4d19
Fast-forward
 index.html | 45 +++++++++++++++++++++++++++++++++++++++------
 1 file changed, 39 insertions(+), 6 deletions(-)
```

**Branch löschen:**
```bash
git branch -d feature/skills-icons
```

**Im Browser testen:** Neue Skills sind sichtbar!

**6.3 Feature 3 mergen – Impressum**

```bash
# Impressum-Branch mergen
git merge feature/impressum
```

**Ausgabe:**
```
Updating e7c4d19..f3a8b21
Fast-forward
 impressum.html | 54 ++++++++++++++++++++++++++++++++++++++++++++++++++++++
 index.html     |  3 +++
 2 files changed, 57 insertions(+)
 create mode 100644 impressum.html
```

**Branch löschen:**
```bash
git branch -d feature/impressum
```

**Im Browser testen:** Impressum-Link im Footer funktioniert!

---

### Teil 7: Finale Prüfung (5 Min)

**7.1 Alle Branches anzeigen**

```bash
git branch
```

**Ausgabe:**
```
* main
```

**Perfekt!** Nur noch `main` ist übrig, alle Features sind integriert.

**7.2 Vollständige Historie**

```bash
git log --oneline
```

**Ausgabe:**
```
f3a8b21 (HEAD -> main) Impressum-Seite erstellt und im Footer verlinkt
e7c4d19 Skills-Sektion mit Icons und Fortschrittsbalken erweitert
d2b9f32 Footer mit Copyright und Social Media Links erstellt
c4b7e93 Navigation mit Icons und mobilem Menü-Button erweitert
a3f5e21 Initiales Portfolio mit HTML, CSS und JavaScript
```

**7.3 Status checken**

```bash
git status
```

**Ausgabe:**
```
On branch main
nothing to commit, working tree clean
```

**Excellent!** Alle Features sind integriert, alle Branches sind gelöscht, alles ist committed.

---

## Erfolgskriterien

- [ ] Drei Feature-Branches wurden parallel erstellt
- [ ] In jedem Branch wurde mindestens ein Commit erstellt
- [ ] Footer mit Social Media Links wurde implementiert
- [ ] Skills-Sektion mit Icons und Fortschrittsbalken wurde erstellt
- [ ] Impressum-Seite wurde erstellt und verlinkt
- [ ] Alle drei Branches wurden nacheinander in `main` gemergt
- [ ] Alle Feature-Branches wurden nach Merge gelöscht
- [ ] Portfolio funktioniert im Browser mit allen neuen Features
- [ ] `git log --oneline` zeigt vollständige Historie
- [ ] `git status` zeigt "nothing to commit, working tree clean"

## Tipps

- **Parallel arbeiten:** Du kannst jederzeit zwischen Branches wechseln
- **Status vergessen?** `git status` zeigt immer den aktuellen Branch
- **Grafische Übersicht:** `git log --graph --all` zeigt Branch-Struktur
- **Fehler beim Merge?** `git merge --abort` bricht Merge ab
- **VS Code Integration:** Unten links siehst du den aktuellen Branch
- **Profitipp:** Nutze aussagekräftige Branch-Namen mit Präfixen
- **Testen, testen, testen:** Nach jedem Merge im Browser prüfen
- **Commits vergessen?** `git reflog` zeigt alle Actions

## Reflexionsfragen

1. Warum ist paralleles Arbeiten mit Branches besser als sequenzielles Arbeiten im `main`-Branch?
2. Was passiert mit deinen Dateien, wenn du zwischen Branches wechselst?
3. Teste: Erstelle einen Branch, mache Änderungen, wechsle zu `main` und prüfe die Dateien. Was fällt dir auf?
4. Warum solltest du Feature-Branches nach erfolgreichem Merge löschen?
5. Stelle dir vor, du arbeitest im Team: Wie hilft Branching dabei, dass ihr euch nicht gegenseitig stört?

## Weiterführende Links

- [Atlassian Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) – Verschiedene Branching-Strategien
- [GitFlow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) – Professioneller Workflow für Teams
- [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
- [Git Best Practices](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)
- [Oh Shit, Git!?](https://ohshitgit.com/) – Wenn was schiefgeht

---

**⏱️ Geschätzte Zeit:** 80-90 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 lernst du, wie du Merge-Konflikte löst!
