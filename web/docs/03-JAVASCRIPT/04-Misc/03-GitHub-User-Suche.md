# Auftrag 3: GitHub-User-Suche mit Datenvisualisierung

## Ziel

Du baust eine vollständige Suchfunktion für GitHub-User mit API-Integration, Datenverarbeitung und visueller Darstellung. Das zeigt, wie moderne Web-Apps funktionieren.

## Beschreibung

In diesem fortgeschrittenen Auftrag kombinierst du alle gelernten Konzepte: Event Handling, Fetch API, async/await, DOM-Manipulation und Datenverarbeitung. Du erstellst eine Suche, die GitHub-User findet und deren Profile mit Repositories, Followern und Statistiken anzeigt.

Die **GitHub API** ist eine der bekanntesten öffentlichen APIs und braucht keinen API-Key für einfache Anfragen. Perfekt zum Üben!

---

### Teil 1: GitHub-User-Suche Grundstruktur (20 Min)

Erstelle eine neue Sektion in `index.html`:

```html
<section id="github-search">
    <h2>GitHub-User-Suche</h2>
    <p>Suche nach GitHub-Usern und sieh deren Profile, Repositories und Statistiken.</p>
    
    <div class="search-container">
        <div class="search-box">
            <input 
                type="text" 
                id="github-username" 
                placeholder="GitHub-Username eingeben (z.B. torvalds)"
                class="form-input"
            >
            <button id="github-search-button" class="btn-primary">
                Suchen
            </button>
        </div>
        
        <div id="github-loading" class="loading-spinner versteckt"></div>
        
        <div id="github-error" class="error-message versteckt"></div>
        
        <div id="github-profile" class="github-profile versteckt">
            <!-- Profil wird hier dynamisch eingefügt -->
        </div>
    </div>
</section>
```

Füge umfangreiches CSS in `styles.css` hinzu:

```css
/* === GITHUB-SUCHE === */

#github-search {
    background: linear-gradient(135deg, #434343 0%, #000000 100%);
    color: white;
    padding: 40px;
    border-radius: 12px;
    margin: 30px 0;
}

.search-container {
    max-width: 800px;
    margin: 0 auto;
}

.search-box {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.search-box input {
    flex: 1;
    background: rgba(255, 255, 255, 0.1);
    border: 2px solid rgba(255, 255, 255, 0.3);
    color: white;
}

.search-box input::placeholder {
    color: rgba(255, 255, 255, 0.6);
}

.search-box input:focus {
    border-color: #2ea44f;
}

/* GitHub Profil */
.github-profile {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
    padding: 30px;
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255, 255, 255, 0.1);
}

.profile-header {
    display: flex;
    gap: 20px;
    align-items: center;
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid rgba(255, 255, 255, 0.1);
}

.profile-avatar {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    border: 4px solid #2ea44f;
}

.profile-info h3 {
    margin: 0 0 10px 0;
    font-size: 2em;
}

.profile-info .username {
    color: #2ea44f;
    font-size: 1.2em;
    margin-bottom: 10px;
}

.profile-info .bio {
    opacity: 0.8;
    line-height: 1.5;
}

.profile-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
    margin-bottom: 30px;
}

.stat-card {
    background: rgba(255, 255, 255, 0.08);
    padding: 20px;
    border-radius: 8px;
    text-align: center;
    border: 1px solid rgba(255, 255, 255, 0.1);
}

.stat-card .stat-number {
    font-size: 2em;
    font-weight: bold;
    color: #2ea44f;
    display: block;
    margin-bottom: 5px;
}

.stat-card .stat-label {
    opacity: 0.7;
    font-size: 0.9em;
}

.profile-links {
    display: flex;
    gap: 10px;
    margin-bottom: 30px;
}

.profile-link {
    background: #2ea44f;
    color: white;
    padding: 10px 20px;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 600;
    transition: background 0.3s;
}

.profile-link:hover {
    background: #2c974b;
}

/* Repositories */
.repositories-section h4 {
    margin-bottom: 20px;
    font-size: 1.5em;
}

.repo-grid {
    display: grid;
    gap: 15px;
}

.repo-card {
    background: rgba(255, 255, 255, 0.08);
    padding: 20px;
    border-radius: 8px;
    border-left: 4px solid #2ea44f;
    transition: transform 0.2s, background 0.2s;
}

.repo-card:hover {
    transform: translateX(5px);
    background: rgba(255, 255, 255, 0.12);
}

.repo-card h5 {
    margin: 0 0 10px 0;
    color: #2ea44f;
    font-size: 1.2em;
}

.repo-card .repo-description {
    opacity: 0.8;
    margin-bottom: 15px;
    line-height: 1.5;
}

.repo-meta {
    display: flex;
    gap: 20px;
    font-size: 0.9em;
    opacity: 0.7;
}

.repo-meta span {
    display: flex;
    align-items: center;
    gap: 5px;
}
```

---

### Teil 2: GitHub API Integration (30 Min)

Erstelle eine neue Datei **`github.js`**:

```javascript
// =====================================================
// GITHUB USER SUCHE
// =====================================================
// Integriere GitHub API für User-Suche und Profil-Anzeige

console.log("GitHub-Script geladen!");

// === KONFIGURATION ===

const GITHUB_API = "https://api.github.com";
const MAX_REPOS = 5; // Maximale Anzahl anzuzeigender Repositories

// === ELEMENTE ===

let usernameInput = document.getElementById("github-username");
let searchButton = document.getElementById("github-search-button");
let loadingSpinner = document.getElementById("github-loading");
let errorMessage = document.getElementById("github-error");
let profileContainer = document.getElementById("github-profile");

// === EVENT LISTENERS ===

searchButton.addEventListener("click", sucheGithubUser);

// Enter-Taste im Suchfeld
usernameInput.addEventListener("keypress", function(event) {
    if (event.key === "Enter") {
        sucheGithubUser();
    }
});

// === HAUPTFUNKTION: USER SUCHEN ===

async function sucheGithubUser() {
    let username = usernameInput.value.trim();
    
    // Validierung
    if (username === "") {
        zeigeFehlermeldung("Bitte gib einen GitHub-Username ein");
        return;
    }
    
    try {
        // UI zurücksetzen
        versteckeAlles();
        loadingSpinner.classList.remove("versteckt");
        searchButton.disabled = true;
        
        console.log(`🔍 Suche GitHub-User: ${username}`);
        
        // User-Daten laden
        let userData = await ladeUserDaten(username);
        
        // Repositories laden
        let repoData = await ladeUserRepositories(username);
        
        // Profil anzeigen
        zeigeProfil(userData, repoData);
        
        console.log("✅ Profil erfolgreich geladen");
        
    } catch (fehler) {
        console.error("❌ Fehler:", fehler);
        
        if (fehler.message.includes("404")) {
            zeigeFehlermeldung(`User "${username}" nicht gefunden`);
        } else if (fehler.message.includes("403")) {
            zeigeFehlermeldung("Rate Limit erreicht. Bitte warte einen Moment.");
        } else {
            zeigeFehlermeldung("Fehler beim Laden der Daten. Bitte versuche es später nochmal.");
        }
        
    } finally {
        loadingSpinner.classList.add("versteckt");
        searchButton.disabled = false;
    }
}

// === API-REQUESTS ===

// User-Daten von GitHub API laden
async function ladeUserDaten(username) {
    let url = `${GITHUB_API}/users/${username}`;
    
    console.log("📡 Request:", url);
    
    let response = await fetch(url);
    
    if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    let daten = await response.json();
    
    console.log("📦 User-Daten:", daten);
    
    return daten;
}

// Repositories von GitHub API laden
async function ladeUserRepositories(username) {
    let url = `${GITHUB_API}/users/${username}/repos?sort=updated&per_page=${MAX_REPOS}`;
    
    console.log("📡 Request:", url);
    
    let response = await fetch(url);
    
    if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    let daten = await response.json();
    
    console.log(`📦 ${daten.length} Repositories geladen`);
    
    return daten;
}

// === PROFIL ANZEIGEN ===

function zeigeProfil(user, repos) {
    // HTML für Profil generieren
    let profilHTML = `
        <div class="profile-header">
            <img 
                src="${user.avatar_url}" 
                alt="${user.name || user.login}"
                class="profile-avatar"
            >
            <div class="profile-info">
                <h3>${user.name || user.login}</h3>
                <div class="username">@${user.login}</div>
                ${user.bio ? `<p class="bio">${user.bio}</p>` : ""}
            </div>
        </div>
        
        <div class="profile-stats">
            <div class="stat-card">
                <span class="stat-number">${formatZahl(user.public_repos)}</span>
                <span class="stat-label">Repositories</span>
            </div>
            <div class="stat-card">
                <span class="stat-number">${formatZahl(user.followers)}</span>
                <span class="stat-label">Followers</span>
            </div>
            <div class="stat-card">
                <span class="stat-number">${formatZahl(user.following)}</span>
                <span class="stat-label">Following</span>
            </div>
            <div class="stat-card">
                <span class="stat-number">${formatZahl(user.public_gists)}</span>
                <span class="stat-label">Gists</span>
            </div>
        </div>
        
        ${user.location ? `<p>📍 ${user.location}</p>` : ""}
        ${user.blog ? `<p>🔗 <a href="${formatUrl(user.blog)}" target="_blank">${user.blog}</a></p>` : ""}
        
        <div class="profile-links">
            <a href="${user.html_url}" target="_blank" class="profile-link">
                GitHub Profil öffnen
            </a>
        </div>
        
        <div class="repositories-section">
            <h4>Neueste Repositories</h4>
            <div class="repo-grid">
                ${generiereRepoCards(repos)}
            </div>
        </div>
    `;
    
    // In Container einfügen
    profileContainer.innerHTML = profilHTML;
    profileContainer.classList.remove("versteckt");
}

// === REPOSITORY-CARDS GENERIEREN ===

function generiereRepoCards(repos) {
    if (repos.length === 0) {
        return "<p>Keine öffentlichen Repositories vorhanden.</p>";
    }
    
    return repos.map(function(repo) {
        return `
            <div class="repo-card">
                <h5>
                    <a href="${repo.html_url}" target="_blank" style="color: #2ea44f; text-decoration: none;">
                        ${repo.name}
                    </a>
                </h5>
                ${repo.description ? `<p class="repo-description">${repo.description}</p>` : "<p class='repo-description'>Keine Beschreibung</p>"}
                <div class="repo-meta">
                    ${repo.language ? `<span>💻 ${repo.language}</span>` : ""}
                    <span>⭐ ${repo.stargazers_count}</span>
                    <span>🍴 ${repo.forks_count}</span>
                    <span>📅 ${formatDatum(repo.updated_at)}</span>
                </div>
            </div>
        `;
    }).join("");
}

// === HILFSFUNKTIONEN ===

// Zahlen formatieren (z.B. 1000 → 1k)
function formatZahl(zahl) {
    if (zahl >= 1000000) {
        return (zahl / 1000000).toFixed(1) + "M";
    }
    if (zahl >= 1000) {
        return (zahl / 1000).toFixed(1) + "k";
    }
    return zahl;
}

// URL formatieren (http hinzufügen falls fehlt)
function formatUrl(url) {
    if (!url.startsWith("http")) {
        return "https://" + url;
    }
    return url;
}

// Datum formatieren (ISO → lesbares Format)
function formatDatum(isoString) {
    let datum = new Date(isoString);
    let jetzt = new Date();
    let diff = jetzt - datum;
    
    // Tage berechnen
    let tage = Math.floor(diff / (1000 * 60 * 60 * 24));
    
    if (tage === 0) return "Heute";
    if (tage === 1) return "Gestern";
    if (tage < 7) return `vor ${tage} Tagen`;
    if (tage < 30) return `vor ${Math.floor(tage / 7)} Wochen`;
    if (tage < 365) return `vor ${Math.floor(tage / 30)} Monaten`;
    return `vor ${Math.floor(tage / 365)} Jahren`;
}

// UI-Elemente verstecken
function versteckeAlles() {
    profileContainer.classList.add("versteckt");
    errorMessage.classList.add("versteckt");
}

// Fehlermeldung anzeigen
function zeigeFehlermeldung(nachricht) {
    errorMessage.textContent = nachricht;
    errorMessage.classList.remove("versteckt");
    profileContainer.classList.add("versteckt");
}

console.log("GitHub-Suche initialisiert ✅");

// === BEISPIEL-SUCHEN FÜR TESTS ===

// Automatische Beispiel-Suche beim Laden (Optional)
// setTimeout(() => sucheGithubUser("torvalds"), 1000);
```

**HTML einbinden:**

```html
<!-- Vor </body> einfügen -->
<script src="github.js"></script>
</body>
</html>
```

---

### Teil 3: Rate Limiting verstehen (10 Min)

Die GitHub API hat Rate Limits:
- **Ohne Authentication:** 60 Requests pro Stunde
- **Mit Authentication:** 5000 Requests pro Stunde

**Aufgabe:** Füge eine Funktion hinzu, die das Rate Limit anzeigt.

Erweitere `github.js`:

```javascript
// === RATE LIMIT PRÜFEN ===

async function pruefeRateLimit() {
    try {
        let response = await fetch(`${GITHUB_API}/rate_limit`);
        let daten = await response.json();
        
        let limit = daten.rate.limit;
        let remaining = daten.rate.remaining;
        let reset = new Date(daten.rate.reset * 1000);
        
        console.log("📊 GitHub Rate Limit:");
        console.log(`   Limit: ${limit} Requests/Stunde`);
        console.log(`   Verbleibend: ${remaining}`);
        console.log(`   Reset: ${reset.toLocaleTimeString()}`);
        
        if (remaining < 10) {
            console.warn("⚠️ Nur noch wenige Requests verfügbar!");
        }
        
    } catch (fehler) {
        console.error("Fehler beim Prüfen des Rate Limits:", fehler);
    }
}

// Rate Limit beim Laden prüfen
pruefeRateLimit();
```

---

## Erfolgskriterien

- [ ] GitHub-User-Suche funktioniert
- [ ] Profil wird mit Avatar, Name und Bio angezeigt
- [ ] Statistiken (Repos, Followers, Following) werden angezeigt
- [ ] Top 5 Repositories werden mit Details angezeigt
- [ ] Links zu GitHub-Profil und Repos funktionieren
- [ ] Loading-State während API-Requests
- [ ] Fehlermeldung bei nicht gefundenem User
- [ ] Fehlermeldung bei Rate Limit
- [ ] Enter-Taste im Suchfeld funktioniert
- [ ] Zahlen werden formatiert (1000 → 1k)
- [ ] Datum wird relativ angezeigt (vor X Tagen)
- [ ] Responsive Design funktioniert
- [ ] Keine JavaScript-Fehler in der Konsole

Bonus-Kriterien:
- [ ] Rate Limit wird in Konsole angezeigt
- [ ] Repository-Sprache wird angezeigt
- [ ] Stars und Forks werden angezeigt
- [ ] Links öffnen in neuem Tab

---

## Tipps

- **GitHub API Dokumentation:** [docs.github.com/rest](https://docs.github.com/en/rest)
- **Rate Limits:** Nutze Console-Logs, um Limits zu überwachen
- **Error Handling:** HTTP-Status-Codes 404 (Not Found) und 403 (Forbidden) behandeln
- **Template Literals:** Nutze backticks für mehrzeiliges HTML
- **Array.map():** Perfekt für das Erstellen von Listen aus Daten
- **.join(""):** Verbindet Array-Elemente zu einem String

**Häufige Fehler:**
- Vergessen, URLs zu encodieren (Sonderzeichen in Usernamen)
- Rate Limit überschreiten bei vielen Tests
- Fehlende Null-Checks (z.B. wenn bio null ist)
- Fehlendes http:// bei externen Links

---

## Reflexionsfragen

1. **Warum gibt es Rate Limits bei APIs?**  
   *Was würde ohne Limits passieren? Wie kann man Limits umgehen?*

2. **Die Daten werden bei jedem Request neu geladen. Wie könnte man Caching implementieren?**  
   *Tipp: LocalStorage, SessionStorage oder in-memory Cache*

3. **Was sind die Vor- und Nachteile von öffentlichen APIs ohne API-Key?**  
   *Vergleiche mit authentifizierten APIs*

4. **Die GitHub API gibt noch viel mehr Daten zurück. Was könntest du noch anzeigen?**  
   *Ideen: Languages, Contributions, Activity, Organizations*

5. **Wie würdest du die App erweitern?**  
   *Ideen: Mehrere User vergleichen, Favoriten speichern, GitHub OAuth-Login*

---

## Weiterführende Links

**GitHub API:**
- [GitHub REST API Documentation](https://docs.github.com/en/rest)
- [GitHub API Rate Limiting](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
- [GitHub API Guides](https://docs.github.com/en/rest/guides)

**Erweiterte Konzepte:**
- [JavaScript: Array.map()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)
- [Optional Chaining (?.)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

**API Best Practices:**
- [REST API Best Practices](https://restfulapi.net/rest-api-design-tutorial-with-example/)
- [API Caching Strategies](https://www.keycdn.com/blog/http-cache-headers)

---

**Geschätzte Zeit:** 60 Minuten  
**Nächster Schritt:** Optionaler Auftrag – Erweiterte Features
