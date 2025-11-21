# Optional: Fortgeschrittene API-Konzepte

## Ziel

Du lernst moderne API-Konzepte kennen, die in professionellen Anwendungen wichtig sind: async/await für lesbaren Code, robustes Error Handling, Rate Limiting, Authentifizierung mit API-Keys und Optimierungen wie Caching und Debouncing.

## Beschreibung

Bisher haben wir mit `.then()` und `.catch()` gearbeitet. Das funktioniert, aber bei komplexen Anwendungen wird der Code schnell unübersichtlich. Professionelle Entwickler nutzen **async/await** – eine modernere Syntax, die Code lesbarer macht. Ausserdem schauen wir uns wichtige Konzepte wie Error Handling, Authentifizierung und Performance-Optimierungen an.

Dieser Auftrag ist anspruchsvoller und zeigt dir, wie echte Web-Apps gebaut werden.

---

### Teil 1: async/await statt .then() (25 Min)

**Aufgabe:** Konvertiere deine bisherigen fetch()-Calls zu async/await.

**Vergleich: .then() vs. async/await**

**Alte Methode mit .then():**

```javascript
function ladePosts() {
    fetch('https://jsonplaceholder.typicode.com/posts')
        .then(response => response.json())
        .then(posts => {
            console.log(posts);
        })
        .catch(error => {
            console.error(error);
        });
}
```

**Neue Methode mit async/await:**

```javascript
async function ladePosts() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const posts = await response.json();
        console.log(posts);
    } catch (error) {
        console.error(error);
    }
}
```

**Was ist besser?**
- async/await ist lesbarer (sieht aus wie normaler Code)
- Fehlerbehandlung mit try-catch ist einfacher
- Verkettung mehrerer Requests ist übersichtlicher

---

**Deine Aufgabe:** Erstelle `api-advanced.js` und implementiere async/await.

**Anforderungen:**
1. Erstelle `async function ladePostAsync(postId)`
2. Nutze `await` statt `.then()`
3. Nutze `try-catch` statt `.catch()`
4. Prüfe `response.ok` und werfe Fehler bei Problemen

**Grundgerüst:**

```javascript
// =====================================================
// API ADVANCED – Moderne Konzepte
// =====================================================

console.log("=== API ADVANCED ===");

// === ASYNC/AWAIT BASICS ===

// TODO: Erstelle async function
async function ladePostAsync(postId) {
    console.log(`Lade Post ${postId} mit async/await...`);

    try {
        // TODO: Nutze await statt .then()
        const response = await fetch(`.../${postId}`);

        // TODO: Prüfe response.ok
        if (...) {
            throw new Error(`HTTP-Fehler: ${response.status}`);
        }

        // TODO: Parse JSON mit await
        const post = await ...;

        console.log("✅ Post geladen:", post.title);
        return post;

    } catch (error) {
        // TODO: Fehlerbehandlung
        console.error("❌ Fehler:", error.message);
        throw error;
    }
}

// TODO: Rufe die Funktion auf
ladePostAsync(1);
```

**Wo nachschlagen?**
- [MDN: async function](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN: await](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/await)
- [JavaScript.info: Async/await](https://javascript.info/async-await)

// === AUFGABE: MEHRERE REQUESTS NACHEINANDER ===

async function ladePostMitUser() {
    console.log("\n=== Post mit User-Info laden ===");

    try {
        // TODO: 1. Lade Post mit ID 1

        // TODO: 2. Lade User basierend auf post.userId

        // TODO: 3. Lade Kommentare basierend auf post.id

        // TODO: Gib Objekt mit { post, user, comments } zurück

    } catch (error) {
        console.error("❌ Fehler:", error.message);
    }
}

// TODO: Rufe Funktion auf

// === AUFGABE: PARALLELE REQUESTS (BONUS) ===

async function ladePostsMitUsersParallel() {
    console.log("\n=== Parallele Requests ===");

    try {
        // TODO: Starte beide Requests gleichzeitig (OHNE await!)
        const postsPromise = fetch('...');
        const usersPromise = fetch('...');

        // TODO: Warte mit Promise.all() bis BEIDE fertig sind
        const [postsResponse, usersResponse] = await Promise.all([...]);

        // TODO: Parse beide Responses zu JSON

        // TODO: Reichere Posts mit Autor-Namen an
        // Tipp: posts.map() + users.find()

    } catch (error) {
        console.error("❌ Fehler:", error.message);
    }
}
```

**Wo nachschlagen?**
- [MDN: Promise.all()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
- [Array.map()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [Array.find()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

**Neue Konzepte:**

- `async`: Markiert Funktion als asynchron
- `await`: Wartet auf Promise-Auflösung
- `try-catch`: Fängt Fehler ab
- `Promise.all()`: Führt mehrere Requests parallel aus
- Spread-Operator `...post`: Kopiert alle Properties

---

### Teil 2: Robustes Error Handling (25 Min)

**Aufgabe:** Implementiere professionelles Error Handling mit spezifischen Fehlermeldungen.

```javascript
// === ROBUSTES ERROR HANDLING ===

async function ladeMitErrorHandling(url) {
    console.log("\n=== Error Handling Demo ===");
    
    try {
        const response = await fetch(url);
        
        // 1. Status-Code prüfen
        if (!response.ok) {
            // Spezifische Fehlermeldungen
            if (response.status === 404) {
                throw new Error("Ressource nicht gefunden (404)");
            } else if (response.status === 401) {
                throw new Error("Nicht autorisiert (401) – API-Key fehlt oder falsch");
            } else if (response.status === 500) {
                throw new Error("Server-Fehler (500) – API ist down");
            } else {
                throw new Error(`HTTP-Fehler: ${response.status}`);
            }
        }
        
        // 2. Content-Type prüfen
        const contentType = response.headers.get('content-type');
        if (!contentType || !contentType.includes('application/json')) {
            throw new Error("Antwort ist kein JSON");
        }
        
        // 3. JSON parsen
        const data = await response.json();
        
        // 4. Daten validieren
        if (!data || typeof data !== 'object') {
            throw new Error("Ungültige Daten erhalten");
        }
        
        console.log("✅ Daten erfolgreich geladen");
        return data;
        
    } catch (error) {
        // Fehlertyp unterscheiden
        if (error instanceof TypeError) {
            console.error("❌ Netzwerk-Fehler:", error.message);
            console.log("Tipp: Internetverbindung prüfen");
        } else {
            console.error("❌ Fehler:", error.message);
        }
        
        // Optional: Fehler an Monitoring-Service senden
        // sendErrorToMonitoring(error);
        
        throw error;  // Fehler weitergeben
    }
}

// === RETRY-MECHANISMUS BEI FEHLER ===

async function ladeWithRetry(url, maxRetries = 3) {
    console.log("\n=== Retry-Mechanismus ===");
    
    for (let versuch = 1; versuch <= maxRetries; versuch++) {
        try {
            console.log(`Versuch ${versuch}/${maxRetries}...`);
            
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            
            const data = await response.json();
            console.log("✅ Erfolgreich beim Versuch", versuch);
            return data;
            
        } catch (error) {
            console.error(`❌ Versuch ${versuch} fehlgeschlagen:`, error.message);
            
            // Letzter Versuch?
            if (versuch === maxRetries) {
                console.error("⚠️ Alle Versuche fehlgeschlagen");
                throw error;
            }
            
            // Warten vor nächstem Versuch (exponentielles Backoff)
            const wartezeit = Math.pow(2, versuch) * 1000;  // 2s, 4s, 8s...
            console.log(`Warte ${wartezeit/1000}s vor nächstem Versuch...`);
            await new Promise(resolve => setTimeout(resolve, wartezeit));
        }
    }
}

// Test mit falscher URL (wird fehlschlagen)
ladeMitErrorHandling('https://jsonplaceholder.typicode.com/posts/99999');

// Test mit Retry (mit falscher URL)
// ladeWithRetry('https://jsonplaceholder.typicode.com/falscher-endpunkt');
```

---

### Teil 3: API-Authentifizierung mit API-Keys (20 Min)

```javascript
// === AUTHENTIFIZIERUNG MIT API-KEY ===

// WICHTIG: Nie echte API-Keys im Frontend-Code!
// Dieses Beispiel ist nur zur Demonstration

const WETTER_API_KEY = 'dein-api-key-hier';  // Nie echte Keys im Code!
const WETTER_API_URL = 'https://api.open-meteo.com/v1/forecast';

async function ladeWetterDaten(latitude, longitude) {
    console.log("\n=== Wetter-Daten laden ===");
    
    try {
        // URL mit Query-Parametern bauen
        const url = new URL(WETTER_API_URL);
        url.searchParams.append('latitude', latitude);
        url.searchParams.append('longitude', longitude);
        url.searchParams.append('current_weather', 'true');
        
        console.log("Request URL:", url.toString());
        
        const response = await fetch(url, {
            headers: {
                // Manche APIs erwarten API-Key im Header
                // 'Authorization': `Bearer ${WETTER_API_KEY}`,
                // Oder als Custom Header
                // 'X-API-Key': WETTER_API_KEY
            }
        });
        
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }
        
        const data = await response.json();
        
        console.log("✅ Wetter-Daten:");
        console.log("Temperatur:", data.current_weather.temperature, "°C");
        console.log("Windgeschwindigkeit:", data.current_weather.windspeed, "km/h");
        console.log("Wetter-Code:", data.current_weather.weathercode);
        
        return data;
        
    } catch (error) {
        console.error("❌ Fehler beim Laden der Wetter-Daten:", error.message);
    }
}

// Beispiel: Bern, Schweiz
ladeWetterDaten(46.9479, 7.4474);

// === SICHERER UMGANG MIT API-KEYS ===

console.log("\n=== API-Key Best Practices ===");
console.log("✅ DO:");
console.log("- API-Keys in Umgebungsvariablen (.env)");
console.log("- Backend-API als Proxy nutzen");
console.log("- Keys regelmässig rotieren");
console.log("- Rate Limiting einbauen");
console.log("");
console.log("❌ DON'T:");
console.log("- Keys im Frontend-Code");
console.log("- Keys in Git committen");
console.log("- Keys in URLs (werden geloggt)");
console.log("- Gleichen Key für alles");
```

---

### Teil 4: Rate Limiting und Caching (25 Min)

```javascript
// === RATE LIMITING (Anfragen begrenzen) ===

class RateLimiter {
    constructor(maxRequests, timeWindow) {
        this.maxRequests = maxRequests;    // z.B. 10
        this.timeWindow = timeWindow;      // z.B. 60000 (1 Minute)
        this.requests = [];
    }
    
    async waitIfNeeded() {
        const jetzt = Date.now();
        
        // Alte Requests entfernen (ausserhalb des Zeitfensters)
        this.requests = this.requests.filter(
            timestamp => jetzt - timestamp < this.timeWindow
        );
        
        // Limit erreicht?
        if (this.requests.length >= this.maxRequests) {
            const aeltesterRequest = this.requests[0];
            const wartezeit = this.timeWindow - (jetzt - aeltesterRequest);
            
            console.log(`⏳ Rate Limit erreicht. Warte ${Math.ceil(wartezeit/1000)}s...`);
            
            await new Promise(resolve => setTimeout(resolve, wartezeit));
            
            // Rekursiv prüfen
            return this.waitIfNeeded();
        }
        
        // Request registrieren
        this.requests.push(jetzt);
    }
}

// Rate Limiter: Max 5 Requests pro 10 Sekunden
const limiter = new RateLimiter(5, 10000);

async function ladeMitRateLimit(url) {
    await limiter.waitIfNeeded();
    
    const response = await fetch(url);
    return response.json();
}

// === CACHING (Daten zwischenspeichern) ===

class APICache {
    constructor(ttl = 60000) {  // Time-To-Live: 60 Sekunden
        this.cache = new Map();
        this.ttl = ttl;
    }
    
    get(key) {
        const eintrag = this.cache.get(key);
        
        if (!eintrag) {
            return null;
        }
        
        // Abgelaufen?
        if (Date.now() - eintrag.timestamp > this.ttl) {
            this.cache.delete(key);
            return null;
        }
        
        console.log("✅ Aus Cache geladen:", key);
        return eintrag.data;
    }
    
    set(key, data) {
        this.cache.set(key, {
            data: data,
            timestamp: Date.now()
        });
        console.log("💾 In Cache gespeichert:", key);
    }
    
    clear() {
        this.cache.clear();
        console.log("🗑️ Cache geleert");
    }
}

// Cache mit 30 Sekunden TTL
const apiCache = new APICache(30000);

async function ladeMitCache(url) {
    // Prüfen ob im Cache
    const cached = apiCache.get(url);
    if (cached) {
        return cached;
    }
    
    // Nicht im Cache → von API laden
    console.log("🌐 Von API laden:", url);
    const response = await fetch(url);
    const data = await response.json();
    
    // In Cache speichern
    apiCache.set(url, data);
    
    return data;
}

// Demo: Mehrfach gleiche Daten laden
async function demoCaching() {
    console.log("\n=== Caching Demo ===");
    
    const url = 'https://jsonplaceholder.typicode.com/posts/1';
    
    // 1. Aufruf: Von API
    await ladeMitCache(url);
    
    // 2. Aufruf: Aus Cache
    await ladeMitCache(url);
    
    // 3. Aufruf: Aus Cache
    await ladeMitCache(url);
    
    // Nach 35 Sekunden: Cache abgelaufen, von API laden
    setTimeout(async () => {
        console.log("\n(35 Sekunden später...)");
        await ladeMitCache(url);
    }, 35000);
}

demoCaching();

// === DEBOUNCING (Verzögerte Ausführung) ===

function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        // Vorherigen Timer löschen
        clearTimeout(timeoutId);
        
        // Neuen Timer starten
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Beispiel: Suche mit Debouncing
const suchFeld = document.createElement('input');
suchFeld.type = 'text';
suchFeld.placeholder = 'Suchen...';

async function sucheInAPI(suchbegriff) {
    if (suchbegriff.length < 3) return;
    
    console.log("🔍 Suche nach:", suchbegriff);
    
    const response = await fetch(
        `https://jsonplaceholder.typicode.com/posts?q=${suchbegriff}`
    );
    const results = await response.json();
    
    console.log("Ergebnisse:", results.length);
}

// Debounced Version: Wartet 500ms nach letzter Eingabe
const debouncedSuche = debounce(sucheInAPI, 500);

suchFeld.addEventListener('input', (event) => {
    debouncedSuche(event.target.value);
});

console.log("\n=== Debouncing Demo ===");
console.log("Suchfeld erstellt (nicht im DOM, nur zur Demo)");
console.log("Ohne Debouncing: Anfrage bei JEDEM Buchstaben");
console.log("Mit Debouncing: Anfrage erst 500ms nach letzter Eingabe");
```

---

### Teil 5: Vollständiges Beispiel – Portfolio-Projekte von externer API (30 Min)

```javascript
// =====================================================
// VOLLSTÄNDIGES BEISPIEL: GITHUB REPOS LADEN
// =====================================================

class GitHubAPIClient {
    constructor(username) {
        this.username = username;
        this.baseUrl = 'https://api.github.com';
        this.cache = new APICache(300000);  // 5 Minuten
        this.limiter = new RateLimiter(10, 60000);  // 10/Minute
    }
    
    async getRepos() {
        const url = `${this.baseUrl}/users/${this.username}/repos`;
        
        // Cache prüfen
        const cached = this.cache.get(url);
        if (cached) return cached;
        
        // Rate Limiting
        await this.limiter.waitIfNeeded();
        
        try {
            const response = await fetch(url, {
                headers: {
                    'Accept': 'application/vnd.github.v3+json'
                }
            });
            
            if (!response.ok) {
                throw new Error(`GitHub API: ${response.status}`);
            }
            
            const repos = await response.json();
            
            // Cache speichern
            this.cache.set(url, repos);
            
            return repos;
            
        } catch (error) {
            console.error("Fehler beim Laden der Repos:", error);
            throw error;
        }
    }
    
    async getRepoDetails(repoName) {
        const url = `${this.baseUrl}/repos/${this.username}/${repoName}`;
        
        await this.limiter.waitIfNeeded();
        
        const response = await fetch(url);
        return response.json();
    }
}

// Demo
async function demoGitHubAPI() {
    console.log("\n=== GitHub API Demo ===");
    
    const client = new GitHubAPIClient('microsoft');
    
    try {
        const repos = await client.getRepos();
        
        console.log(`✅ ${repos.length} Repositories gefunden`);
        
        // Top 5 nach Stars sortiert
        const topRepos = repos
            .sort((a, b) => b.stargazers_count - a.stargazers_count)
            .slice(0, 5);
        
        console.log("\nTop 5 Repos nach Stars:");
        topRepos.forEach((repo, index) => {
            console.log(`${index + 1}. ${repo.name}`);
            console.log(`   ⭐ ${repo.stargazers_count.toLocaleString()} Stars`);
            console.log(`   🍴 ${repo.forks_count.toLocaleString()} Forks`);
            console.log(`   📝 ${repo.description || 'Keine Beschreibung'}`);
        });
        
    } catch (error) {
        console.error("Fehler:", error.message);
    }
}

demoGitHubAPI();

console.log("\n✅ API Advanced geladen");
```

---

## Erfolgskriterien

- [ ] `api-advanced.js` erstellt mit async/await
- [ ] Mehrere Requests nacheinander funktionieren
- [ ] Parallele Requests mit Promise.all() implementiert
- [ ] Robustes Error Handling mit try-catch
- [ ] Retry-Mechanismus bei Fehlern funktioniert
- [ ] API-Key-Authentifizierung verstanden
- [ ] Rate Limiter implementiert und getestet
- [ ] Caching-System funktioniert
- [ ] Debouncing für Suche implementiert
- [ ] GitHub API Client funktioniert vollständig

---

## Tipps

**async/await Best Practices:**
- Immer try-catch nutzen
- await nur in async-Funktionen
- Parallele Requests mit Promise.all()
- Fehler richtig propagieren

**Performance:**
- Cache für wiederholte Requests
- Debouncing für Suchen
- Rate Limiting beachten
- Parallele Requests wo möglich

**Sicherheit:**
- Nie API-Keys im Frontend
- HTTPS nutzen
- Input validieren
- Fehler nicht zu detailliert zeigen

---

## Reflexionsfragen

1. **Was sind die Vorteile von async/await gegenüber .then()?**  
   *Wann würdest du welche Methode nutzen?*

2. **Warum ist Caching wichtig für APIs?**  
   *Welche Probleme löst es? Welche Nachteile hat es?*

3. **Was ist der Unterschied zwischen Rate Limiting und Throttling?**  
   *Recherchiere: Wie funktioniert API Rate Limiting?*

4. **Warum sollten API-Keys nie im Frontend-Code sein?**  
   *Wie würdest du es richtig machen? (Tipp: Backend-Proxy)*

5. **Was ist exponentielles Backoff bei Retries?**  
   *Warum nicht immer gleiche Wartezeit?*

---

## Weiterführende Links

**async/await:**
- [MDN: async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript.info: Async/await](https://javascript.info/async-await)

**Error Handling:**
- [MDN: Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [Best Practices for Error Handling](https://blog.logrocket.com/error-handling-javascript/)

**API Best Practices:**
- [API Security Best Practices](https://roadmap.sh/best-practices/api-security)
- [REST API Best Practices](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)

**Performance:**
- [Web.dev: Network Performance](https://web.dev/network-performance/)
- [Debouncing and Throttling Explained](https://css-tricks.com/debouncing-throttling-explained-examples/)

---

**⏱️ Geschätzte Zeit:** 115 Minuten  
**🎯 Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächstes Kapitel:** HTTPS Grundlagen – SSL/TLS und Verschlüsselung
