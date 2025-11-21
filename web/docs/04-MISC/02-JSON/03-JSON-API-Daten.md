# Auftrag 3: JSON-API-Daten verarbeiten

## Ziel

Du lernst, JSON-Daten von echten APIs abzurufen, zu verarbeiten und in deinem Portfolio anzuzeigen. Du verstehst, wie moderne Web-Apps mit Backend-Servern kommunizieren und dynamische Inhalte generieren.

## Beschreibung

Der Haupteinsatzzweck von JSON ist der Datenaustausch zwischen Frontend und Backend über APIs. APIs (Application Programming Interfaces) liefern Daten im JSON-Format, die dein JavaScript verarbeitet und als HTML anzeigt. Das ist die Grundlage praktisch jeder modernen Webanwendung.

In diesem Auftrag arbeitest du mit echten öffentlichen APIs, verarbeitest JSON-Responses und baust dynamische Komponenten für dein Portfolio. Du lernst async/await, Error Handling und Best Practices für API-Kommunikation.

---

### Teil 1: GitHub-Profil-Daten laden (30 Min)

GitHub bietet eine öffentliche API, um Profil-Informationen abzurufen.

**Aufgabe:** Erstelle eine Seite, die GitHub-Profildaten lädt und anzeigt.

**API-Dokumentation:**
- GitHub User API: `https://api.github.com/users/{username}`
- Beispiel: `https://api.github.com/users/octocat`
- [Offizielle Dokumentation](https://docs.github.com/en/rest/users/users#get-a-user)

**Schritt 1:** Erstelle eine Datei **`github-integration.html`** mit folgendem Grundgerüst:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub-Integration</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Aptos', Arial, sans-serif;
            background: #f8f9fa;
            padding: 40px 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
        }
        
        h1 {
            color: #005A9C;
            margin-bottom: 30px;
        }
        
        .input-gruppe {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }
        
        input {
            flex: 1;
            padding: 12px;
            border: 2px solid #B3D9EE;
            border-radius: 4px;
            font-size: 16px;
        }
        
        button {
            background: #005A9C;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
        }
        
        button:hover {
            background: #004578;
        }
        
        #loading {
            display: none;
            text-align: center;
            padding: 20px;
            color: #6c757d;
        }
        
        #error {
            display: none;
            background: #f8d7da;
            color: #721c24;
            padding: 15px;
            border-radius: 4px;
            border: 2px solid #f5c6cb;
            margin-bottom: 20px;
        }
        
        .profil-card {
            background: white;
            border-radius: 8px;
            padding: 30px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            display: none;
        }
        
        .profil-header {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            align-items: center;
        }
        
        .profil-bild {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 3px solid #005A9C;
        }
        
        .profil-info h2 {
            color: #005A9C;
            margin-bottom: 5px;
        }
        
        .profil-info p {
            color: #6c757d;
            margin-bottom: 5px;
        }
        
        .profil-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-top: 20px;
        }
        
        .stat-box {
            background: #B3D9EE;
            padding: 15px;
            border-radius: 4px;
            text-align: center;
        }
        
        .stat-zahl {
            font-size: 24px;
            font-weight: bold;
            color: #005A9C;
        }
        
        .stat-label {
            color: #495057;
            font-size: 14px;
            margin-top: 5px;
        }
        
        .repos-liste {
            margin-top: 30px;
        }
        
        .repos-liste h3 {
            color: #005A9C;
            margin-bottom: 15px;
        }
        
        .repo-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 4px;
            margin-bottom: 10px;
            border-left: 4px solid #008C95;
        }
        
        .repo-item h4 {
            color: #005A9C;
            margin-bottom: 5px;
        }
        
        .repo-meta {
            display: flex;
            gap: 15px;
            font-size: 14px;
            color: #6c757d;
            margin-top: 8px;
        }
        
        .repo-meta span {
            display: flex;
            align-items: center;
            gap: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>GitHub-Profil laden</h1>
        
        <div class="input-gruppe">
            <input 
                type="text" 
                id="username" 
                placeholder="GitHub-Username eingeben (z.B. octocat)"
                value="octocat"
            >
            <button onclick="ladeGitHubProfil()">Profil laden</button>
        </div>
        
        <div id="loading">
            <p>Lade Daten...</p>
        </div>
        
        <div id="error"></div>
        
        <div id="profil" class="profil-card">
            <!-- Wird dynamisch gefüllt -->
        </div>
    </div>
    
    <script>
        // =====================================================
        // GITHUB-API-INTEGRATION
        // =====================================================
        
        async function ladeGitHubProfil() {
            const username = document.getElementById('username').value.trim();
            
            if (!username) {
                zeigeError('Bitte einen Username eingeben!');
                return;
            }
            
            // UI zurücksetzen
            document.getElementById('profil').style.display = 'none';
            document.getElementById('error').style.display = 'none';
            document.getElementById('loading').style.display = 'block';
            
            try {
                // GitHub-API aufrufen
                const apiUrl = `https://api.github.com/users/${username}`;
                console.log('Lade:', apiUrl);
                
                const response = await fetch(apiUrl);
                
                // Prüfen ob erfolgreich
                if (!response.ok) {
                    throw new Error(`User nicht gefunden (${response.status})`);
                }
                
                // JSON parsen
                const userData = await response.json();
                console.log('Empfangene Daten:', userData);
                
                // Repositories laden
                const reposResponse = await fetch(userData.repos_url + '?sort=updated&per_page=5');
                const reposData = await reposResponse.json();
                console.log('Repositories:', reposData);
                
                // Profil anzeigen
                zeigeProfil(userData, reposData);
                
            } catch (error) {
                console.error('Fehler:', error);
                zeigeError(`Fehler beim Laden: ${error.message}`);
            } finally {
                document.getElementById('loading').style.display = 'none';
            }
        }
        
        function zeigeProfil(user, repos) {
            const profilDiv = document.getElementById('profil');
            
            // Profil-HTML generieren
            profilDiv.innerHTML = `
                <div class="profil-header">
                    <img 
                        src="${user.avatar_url}" 
                        alt="${user.name || user.login}"
                        class="profil-bild"
                    >
                    <div class="profil-info">
                        <h2>${user.name || user.login}</h2>
                        <p><strong>@${user.login}</strong></p>
                        ${user.bio ? `<p>${user.bio}</p>` : ''}
                        ${user.location ? `<p>📍 ${user.location}</p>` : ''}
                        ${user.blog ? `<p>🔗 <a href="${user.blog}" target="_blank">${user.blog}</a></p>` : ''}
                    </div>
                </div>
                
                <div class="profil-stats">
                    <div class="stat-box">
                        <div class="stat-zahl">${user.public_repos}</div>
                        <div class="stat-label">Repositories</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-zahl">${user.followers}</div>
                        <div class="stat-label">Followers</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-zahl">${user.following}</div>
                        <div class="stat-label">Following</div>
                    </div>
                </div>
                
                <div class="repos-liste">
                    <h3>Neueste Repositories</h3>
                    ${repos.map(repo => `
                        <div class="repo-item">
                            <h4>
                                <a href="${repo.html_url}" target="_blank">
                                    ${repo.name}
                                </a>
                            </h4>
                            <p>${repo.description || 'Keine Beschreibung'}</p>
                            <div class="repo-meta">
                                ${repo.language ? `<span>💻 ${repo.language}</span>` : ''}
                                <span>⭐ ${repo.stargazers_count} Stars</span>
                                <span>🍴 ${repo.forks_count} Forks</span>
                                <span>Aktualisiert: ${formatDatum(repo.updated_at)}</span>
                            </div>
                        </div>
                    `).join('')}
                </div>
            `;
            
            profilDiv.style.display = 'block';
        }
        
        function zeigeError(nachricht) {
            const errorDiv = document.getElementById('error');
            errorDiv.textContent = nachricht;
            errorDiv.style.display = 'block';
        }
        
        function formatDatum(isoString) {
            const datum = new Date(isoString);
            const jetzt = new Date();
            const diff = jetzt - datum;
            
            const tage = Math.floor(diff / (1000 * 60 * 60 * 24));
            
            if (tage === 0) return 'Heute';
            if (tage === 1) return 'Gestern';
            if (tage < 7) return `vor ${tage} Tagen`;
            if (tage < 30) return `vor ${Math.floor(tage / 7)} Wochen`;
            if (tage < 365) return `vor ${Math.floor(tage / 30)} Monaten`;
            return `vor ${Math.floor(tage / 365)} Jahren`;
        }
        
        // Enter-Taste im Input-Feld
        document.getElementById('username').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                ladeGitHubProfil();
            }
        });
        
        // Beim Laden Beispiel-Profil laden
        // window.onload = () => ladeGitHubProfil();
    </script>
</body>
</html>
```

**Schritt 2:** Implementiere die JavaScript-Funktionalität

Erstelle im `<script>`-Bereich folgende Funktionen:

1. **`ladeGitHubProfil()`**:
   - Hole den Username aus dem Input-Feld
   - Rufe die GitHub API auf: `https://api.github.com/users/${username}`
   - Parse die JSON-Response
   - Rufe `zeigeProfil()` auf

2. **`zeigeProfil(userData)`**:
   - Zeige Profilbild, Name, Bio an
   - Zeige Statistiken (Repos, Followers, Following)
   - Nutze `innerHTML` um das HTML zu generieren

**Wo findest du Hilfe?**
- [MDN: Fetch API](https://developer.mozilla.org/de/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN: async/await](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/async_function)
- Schaue dir die API-Response im Browser an: `https://api.github.com/users/octocat`

**Zusatzaufgaben:**
1. Lade auch die Repositories: `https://api.github.com/users/${username}/repos?sort=updated&per_page=5`
2. Zeige "Member since" an (Tipp: `user.created_at` - nutze `new Date()`)
3. Füge Error Handling hinzu: Was passiert bei ungültigem Username?
4. Zeige einen Loading-Indikator während des Ladens

---

### Teil 2: Portfolio-Projekt-Daten dynamisch laden (30 Min)

**Aufgabe:** Erstelle eine dynamische Projekt-Galerie, die Daten aus einer JSON-Datei lädt.

**Schritt 1: JSON-Datei vorbereiten**

Erstelle `meine-projekte.json` mit folgender Struktur. Füge **mindestens 3 Projekte** hinzu:

```json
{
  "meta": {
    "version": "1.0",
    "letzteAktualisierung": "...",
    "autor": "..."
  },
  "projekte": [
    {
      "id": 1,
      "titel": "...",
      "kurzbeschreibung": "...",
      "kategorie": "Webentwicklung",
      "technologien": [
        {"name": "HTML", "farbe": "#E34F26"},
        {"name": "CSS", "farbe": "#1572B6"}
      ],
      "status": "in-arbeit",
      "fortschritt": 75,
      "datum": {
        "start": "2025-09-01",
        "ende": "2025-12-31"
      },
      "bild": {
        "url": "https://via.placeholder.com/600x400/005A9C/ffffff?text=Projekt1",
        "alt": "..."
      },
      "istFeatured": true
    }
  ]
}
```

**Deine Aufgabe:**
- Fülle die `...` mit deinen Daten
- Füge **mindestens 2 weitere Projekte** hinzu
- Verwende verschiedene Kategorien und Status-Werte
- Nutze Placeholder-Bilder: `https://via.placeholder.com/600x400/FARBE/ffffff?text=TITEL`

**Schritt 2: HTML-Seite erstellen**

Erstelle `projekt-galerie.html`:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Projekt-Galerie</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Aptos', Arial, sans-serif;
            background: #f8f9fa;
            padding: 40px 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        h1 {
            color: #005A9C;
            margin-bottom: 10px;
        }
        
        .header-info {
            color: #6c757d;
            margin-bottom: 30px;
        }
        
        .filter-leiste {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        
        .filter-btn {
            padding: 10px 20px;
            background: white;
            border: 2px solid #B3D9EE;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .filter-btn:hover,
        .filter-btn.aktiv {
            background: #005A9C;
            color: white;
            border-color: #005A9C;
        }
        
        .projekt-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 25px;
        }
        
        .projekt-karte {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .projekt-karte:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 102, 204, 0.15);
        }
        
        .projekt-karte.featured {
            border: 3px solid #E65A00;
        }
        
        .projekt-bild {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }
        
        .projekt-inhalt {
            padding: 20px;
        }
        
        .projekt-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 10px;
        }
        
        .projekt-titel {
            color: #005A9C;
            font-size: 1.3em;
            margin-bottom: 5px;
        }
        
        .projekt-status {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85em;
            font-weight: 600;
        }
        
        .status-in-arbeit {
            background: #fff3cd;
            color: #856404;
        }
        
        .status-abgeschlossen {
            background: #d4edda;
            color: #155724;
        }
        
        .status-geplant {
            background: #d1ecf1;
            color: #0c5460;
        }
        
        .projekt-beschreibung {
            color: #6c757d;
            margin-bottom: 15px;
            line-height: 1.6;
        }
        
        .technologien {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 15px;
        }
        
        .tech-badge {
            padding: 4px 10px;
            border-radius: 4px;
            font-size: 0.85em;
            font-weight: 500;
            color: white;
        }
        
        .fortschritt-bar {
            background: #e9ecef;
            height: 8px;
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 10px;
        }
        
        .fortschritt-fill {
            background: linear-gradient(90deg, #005A9C, #008C95);
            height: 100%;
            transition: width 1s ease;
        }
        
        .projekt-meta {
            display: flex;
            justify-content: space-between;
            font-size: 0.9em;
            color: #6c757d;
        }
        
        .featured-badge {
            background: #E65A00;
            color: white;
            padding: 4px 12px;
            border-radius: 4px;
            font-size: 0.75em;
            font-weight: bold;
            margin-bottom: 10px;
            display: inline-block;
        }
        
        #loading {
            text-align: center;
            padding: 40px;
            color: #6c757d;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Meine Projekte</h1>
        <div class="header-info" id="header-info">
            Lade Projekte...
        </div>
        
        <div class="filter-leiste" id="filter-leiste">
            <!-- Filter werden dynamisch generiert -->
        </div>
        
        <div id="loading">Lade Projekt-Daten...</div>
        
        <div class="projekt-grid" id="projekt-grid">
            <!-- Projekte werden hier eingefügt -->
        </div>
    </div>
    
    <script src="projekt-galerie.js"></script>
</body>
</html>
```

**Schritt 3: JavaScript implementieren**

Erstelle `projekt-galerie.js` und implementiere folgende Funktionen:

**Erforderliche Funktionen:**

1. **`ladeProjekte()`** - Beim Laden ausführen
   - Lade `meine-projekte.json` mit `fetch()`
   - Parse JSON mit `.json()`
   - Rufe `zeigeProjekte()` auf

2. **`zeigeProjekte(projekte)`** - Projekte anzeigen
   - Durchlaufe das `projekte`-Array
   - Erstelle HTML für jedes Projekt
   - Füge es in `#projekt-grid` ein

3. **`erstelleFilter()`** - Filter-Buttons generieren
   - Sammle alle Kategorien aus den Projekten
   - Erstelle Button für jede Kategorie
   - Füge Event Listener hinzu

**Hilfestellung:**

```javascript
// Grundstruktur - Implementiere die fehlenden Teile!

let alleProjekte = [];

document.addEventListener('DOMContentLoaded', async function() {
    await ladeProjekte();
});

async function ladeProjekte() {
    try {
        // TODO: Lade meine-projekte.json mit fetch()
        // TODO: Parse die Response zu JSON
        // TODO: Speichere Projekte in alleProjekte
        // TODO: Rufe zeigeProjekte() auf

    } catch (error) {
        console.error('Fehler:', error);
        // TODO: Zeige Fehlermeldung an
    }
}

function zeigeProjekte(projekte) {
    const grid = document.getElementById('projekt-grid');
    grid.innerHTML = '';

    projekte.forEach(projekt => {
        // TODO: Erstelle div mit class="projekt-karte"
        // TODO: Fülle mit Projekt-Daten (Titel, Bild, Technologien, Status)
        // TODO: Füge zu grid hinzu
    });
}

function formatDatum(isoString) {
    const datum = new Date(isoString);
    return datum.toLocaleDateString('de-CH', {
        year: 'numeric',
        month: 'short',
        day: 'numeric'
    });
}
```

**Wo nachschlagen?**
- [MDN: Fetch API](https://developer.mozilla.org/de/docs/Web/API/Fetch_API/Using_Fetch) - Wie lädt man Daten?
- [MDN: Array.forEach()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) - Wie iteriert man über Arrays?
- [MDN: Template Strings](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals) - Wie erstellt man dynamisches HTML?

**Tipp für HTML-Generierung:**
```javascript
const html = `
    <div class="projekt-karte">
        <h3>${projekt.titel}</h3>
        <p>${projekt.kurzbeschreibung}</p>
    </div>
`;
grid.innerHTML += html;
```

**Teste deine Galerie:**
1. Öffne `projekt-galerie.html` im Browser (mit Live Server!)
2. Schaue dir die Konsole an – werden die Daten korrekt geladen?
3. Teste die Filter-Buttons
4. Füge ein weiteres Projekt in `meine-projekte.json` hinzu und lade neu

---

### Teil 3: Error Handling und Loading States (15 Min)

Verbessere dein `projekt-galerie.js` mit professionellem Error Handling:

```javascript
// Erweitere die ladeProjekte-Funktion:

async function ladeProjekte() {
    const loadingDiv = document.getElementById('loading');
    const gridDiv = document.getElementById('projekt-grid');
    
    try {
        loadingDiv.textContent = 'Lade Projekt-Daten...';
        loadingDiv.style.display = 'block';
        gridDiv.innerHTML = '';
        
        const response = await fetch('meine-projekte.json');
        
        // Verschiedene Error-Cases behandeln
        if (response.status === 404) {
            throw new Error('JSON-Datei nicht gefunden. Stelle sicher, dass meine-projekte.json existiert.');
        }
        
        if (response.status === 500) {
            throw new Error('Server-Fehler. Versuche es später erneut.');
        }
        
        if (!response.ok) {
            throw new Error(`HTTP-Fehler: ${response.status} ${response.statusText}`);
        }
        
        // Content-Type prüfen
        const contentType = response.headers.get('content-type');
        if (!contentType || !contentType.includes('application/json')) {
            console.warn('Warnung: Content-Type ist nicht application/json');
        }
        
        const data = await response.json();
        
        // Daten validieren
        if (!data.projekte || !Array.isArray(data.projekte)) {
            throw new Error('Ungültige Datenstruktur: "projekte"-Array fehlt');
        }
        
        if (data.projekte.length === 0) {
            loadingDiv.innerHTML = `
                <p>Noch keine Projekte vorhanden.</p>
                <p style="font-size: 0.9em; margin-top: 10px;">
                    Füge Projekte in meine-projekte.json hinzu.
                </p>
            `;
            return;
        }
        
        alleProjekte = data.projekte;
        aktualisiereHeader(data.meta);
        erstelleFilter(alleProjekte);
        zeigeProjekte(alleProjekte);
        
        loadingDiv.style.display = 'none';
        
        console.log('✓ Erfolgreich geladen:', alleProjekte.length, 'Projekte');
        
    } catch (error) {
        console.error('Fehler beim Laden:', error);
        
        loadingDiv.innerHTML = `
            <div style="
                background: #f8d7da;
                color: #721c24;
                padding: 20px;
                border-radius: 4px;
                border: 2px solid #f5c6cb;
                max-width: 600px;
                margin: 0 auto;
            ">
                <h3 style="margin-bottom: 10px;">Fehler beim Laden</h3>
                <p><strong>Fehler:</strong> ${error.message}</p>
                <p style="margin-top: 15px; font-size: 0.9em;">
                    <strong>Mögliche Lösungen:</strong>
                </p>
                <ul style="margin-top: 10px; font-size: 0.9em;">
                    <li>Prüfe, ob meine-projekte.json existiert</li>
                    <li>Stelle sicher, dass die JSON-Datei valide ist (jsonlint.com)</li>
                    <li>Nutze einen lokalen Server (Live Server in VS Code)</li>
                    <li>Schaue in die Browser-Konsole für Details</li>
                </ul>
            </div>
        `;
    }
}
```

---

## Erfolgskriterien

- [ ] `github-integration.html` erstellt und funktionsfähig
- [ ] GitHub-Profil erfolgreich geladen und angezeigt
- [ ] Browser-Konsole zeigt API-Response korrekt
- [ ] JSON-Struktur der GitHub-API verstanden
- [ ] `meine-projekte.json` erstellt mit mindestens 2 Projekten
- [ ] `projekt-galerie.html` und `projekt-galerie.js` erstellt
- [ ] Projekte werden dynamisch aus JSON geladen
- [ ] Filter-Funktionalität funktioniert
- [ ] Error Handling implementiert mit hilfreichen Fehlermeldungen
- [ ] Loading States sichtbar während Daten geladen werden

---

## Tipps

**Fetch API:**
- `fetch()` gibt ein Promise zurück – nutze `await` oder `.then()`
- `.json()` ist auch async – braucht ebenfalls `await`
- Immer Error Handling mit `try/catch` oder `.catch()`

**API-Tipps:**
- Öffne die API-URL direkt im Browser, um die Struktur zu sehen
- Nutze `console.log()` um API-Responses zu analysieren
- GitHub-API hat Rate Limits (60 Anfragen/Stunde ohne Token)

**JSON-Response analysieren:**
```javascript
fetch('api-url')
  .then(response => response.json())
  .then(data => {
    console.log('Gesamte Response:', data);
    console.log('Typ:', typeof data);
    console.log('Keys:', Object.keys(data));
  });
```

**CORS-Fehler?**
- Tritt auf, wenn du APIs von file:// lädst
- Lösung: Nutze einen lokalen Webserver (Live Server)

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `fetch()` und `JSON.parse()`?**  
   *Wann nutzt du welche Methode? Können beide kombiniert werden?*

2. **Warum ist Error Handling bei API-Calls besonders wichtig?**  
   *Was kann alles schiefgehen? Wie gehst du mit verschiedenen Fehlertypen um?*

3. **Experimentiere: Was passiert, wenn die JSON-Datei ungültig ist?**  
   *Füge einen Syntax-Fehler in meine-projekte.json ein und schaue, welcher Fehler kommt.*

4. **Wie könntest du die GitHub-Integration in dein echtes Portfolio einbauen?**  
   *Welche Daten würdest du anzeigen? Wie oft würdest du sie aktualisieren?*

5. **Recherchiere: Was ist ein API-Token und warum braucht man ihn?**  
   *Wie erhöht ein Token die Rate Limits bei GitHub?*

---

## Weiterführende Links

**APIs & JSON:**
- [GitHub REST API Docs](https://docs.github.com/en/rest)
- [Public APIs List](https://github.com/public-apis/public-apis) – Sammlung öffentlicher APIs
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) – Fake REST API zum Testen

**Fetch API:**
- [MDN: Using Fetch](https://developer.mozilla.org/de/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN: Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)
- [JavaScript.info: Fetch](https://javascript.info/fetch)

**Async/Await:**
- [MDN: async function](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN: await](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/await)
- [JavaScript.info: Async/Await](https://javascript.info/async-await)

**Error Handling:**
- [MDN: try...catch](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/try...catch)
- [Error Handling Best Practices](https://www.freecodecamp.org/news/javascript-error-handling-guide/)

---

**⏱️ Geschätzte Zeit:** 60-70 Minuten  
**📦 Nächster Schritt:** Auftrag 4 (Optional) – JSON-Schema und fortgeschrittene Validierung
