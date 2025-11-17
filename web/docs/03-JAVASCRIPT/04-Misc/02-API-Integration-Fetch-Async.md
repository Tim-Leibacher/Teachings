# Auftrag 2: API-Integration mit Fetch und async/await

## Ziel

Du lernst, wie du mit der Fetch API Daten von externen Servern abrufst. Mit asynchroner Programmierung holst du Informationen wie Zitate, Wetter oder andere Daten und zeigst sie dynamisch auf deiner Portfolio-Seite an.

## Beschreibung

**APIs (Application Programming Interfaces)** sind Schnittstellen, über die Programme miteinander kommunizieren. Mit der **Fetch API** kannst du HTTP-Requests an Server senden und Daten empfangen. **Asynchrone Programmierung** bedeutet: Der Code wartet nicht auf die Antwort, sondern läuft weiter. Mit **async/await** schreibst du asynchronen Code, der wie synchroner Code aussieht.

In diesem Auftrag bindest du externe APIs in deine Portfolio-Seite ein.

---

### Teil 1: Zufällige Zitate laden (20 Min)

Erstelle eine neue Sektion in `index.html`:

```html
<section id="api-demos">
    <h2>API-Integrationen</h2>
    
    <!-- Zufällige Zitate -->
    <div class="api-box">
        <h3>Inspiration des Tages</h3>
        <p>Lade inspirierende Zitate von einer API:</p>
        
        <button id="quote-button" class="btn-primary">
            Neues Zitat laden
        </button>
        
        <div id="quote-display">
            <blockquote id="quote-text">
                Klicke auf den Button für ein inspirierendes Zitat...
            </blockquote>
            <p id="quote-author"></p>
        </div>
        
        <div id="quote-loading" class="loading-spinner versteckt"></div>
    </div>
</section>
```

Füge CSS in `styles.css` hinzu:

```css
/* === API-BOXEN === */

.api-box {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px;
    border-radius: 12px;
    margin-bottom: 30px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2);
}

.api-box h3 {
    margin-top: 0;
    font-size: 1.8em;
}

#quote-display {
    background: rgba(255, 255, 255, 0.1);
    padding: 20px;
    border-radius: 8px;
    margin-top: 20px;
    min-height: 120px;
    backdrop-filter: blur(10px);
}

#quote-text {
    font-size: 1.2em;
    font-style: italic;
    margin: 0;
    line-height: 1.6;
}

#quote-author {
    text-align: right;
    margin-top: 15px;
    font-weight: 600;
    opacity: 0.9;
}

/* Loading Spinner */
.loading-spinner {
    border: 4px solid rgba(255, 255, 255, 0.3);
    border-top: 4px solid white;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
    margin: 20px auto;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.versteckt {
    display: none !important;
}
```

Erstelle eine neue Datei **`api.js`**:

```javascript
// =====================================================
// API-INTEGRATION
// =====================================================
// Daten von externen APIs laden mit Fetch

console.log("API-Script geladen!");

// === ZUFÄLLIGE ZITATE LADEN ===

// Elemente holen
let quoteButton = document.getElementById("quote-button");
let quoteText = document.getElementById("quote-text");
let quoteAuthor = document.getElementById("quote-author");
let quoteLoading = document.getElementById("quote-loading");

// Event Listener für Button
quoteButton.addEventListener("click", ladeZitat);

// Funktion zum Laden eines Zitats (mit async/await)
async function ladeZitat() {
    try {
        // Loading-State anzeigen
        quoteLoading.classList.remove("versteckt");
        quoteButton.disabled = true;
        quoteText.textContent = "Lädt...";
        quoteAuthor.textContent = "";
        
        console.log("Starte API-Request für Zitat...");
        
        // API-Request (await wartet auf Antwort)
        let response = await fetch("https://api.quotable.io/random");
        
        // HTTP-Status prüfen
        if (!response.ok) {
            throw new Error(`HTTP-Fehler! Status: ${response.status}`);
        }
        
        // JSON-Daten extrahieren
        let daten = await response.json();
        
        console.log("Zitat erhalten:", daten);
        
        // Daten anzeigen
        quoteText.textContent = `"${daten.content}"`;
        quoteAuthor.textContent = `— ${daten.author}`;
        
    } catch (fehler) {
        // Fehlerbehandlung
        console.error("Fehler beim Laden des Zitats:", fehler);
        quoteText.textContent = "Fehler beim Laden :(";
        quoteAuthor.textContent = "Bitte versuche es später nochmal";
        
    } finally {
        // Wird immer ausgeführt (Erfolg oder Fehler)
        quoteLoading.classList.add("versteckt");
        quoteButton.disabled = false;
    }
}

// Initiales Zitat beim Laden der Seite
ladeZitat();

console.log("Zitat-Funktion registriert");
```

**HTML einbinden:**

```html
<!-- Vor </body> einfügen -->
<script src="api.js"></script>
</body>
</html>
```

---

### Teil 2: Wetter-API Integration (25 Min)

Erweitere die API-Sektion mit einer Wetter-Suche:

```html
<!-- In die gleiche Sektion einfügen -->
<div class="api-box" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);">
    <h3>Wetter-Informationen</h3>
    <p>Suche nach einer Stadt und erhalte aktuelle Wetter-Daten:</p>
    
    <div class="weather-search">
        <input 
            type="text" 
            id="city-input" 
            placeholder="Stadt eingeben (z.B. Bern)"
            class="form-input"
        >
        <button id="weather-button" class="btn-primary">
            Wetter abrufen
        </button>
    </div>
    
    <div id="weather-loading" class="loading-spinner versteckt"></div>
    
    <div id="weather-display" class="versteckt">
        <h4 id="weather-city"></h4>
        <div class="weather-info">
            <div class="weather-item">
                <span class="weather-icon">🌡️</span>
                <span id="weather-temp"></span>
            </div>
            <div class="weather-item">
                <span class="weather-icon">💨</span>
                <span id="weather-wind"></span>
            </div>
            <div class="weather-item">
                <span class="weather-icon">📍</span>
                <span id="weather-coords"></span>
            </div>
        </div>
    </div>
    
    <div id="weather-error" class="error-message versteckt"></div>
</div>
```

Erweitere das CSS:

```css
/* === WETTER-WIDGET === */

.weather-search {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.weather-search input {
    flex: 1;
}

#weather-display {
    background: rgba(255, 255, 255, 0.1);
    padding: 20px;
    border-radius: 8px;
    margin-top: 20px;
    backdrop-filter: blur(10px);
}

#weather-city {
    font-size: 1.5em;
    margin-top: 0;
    margin-bottom: 15px;
}

.weather-info {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
}

.weather-item {
    background: rgba(255, 255, 255, 0.15);
    padding: 15px;
    border-radius: 8px;
    text-align: center;
}

.weather-icon {
    font-size: 2em;
    display: block;
    margin-bottom: 10px;
}

.error-message {
    background: rgba(255, 0, 0, 0.2);
    color: white;
    padding: 15px;
    border-radius: 8px;
    margin-top: 20px;
    border: 2px solid rgba(255, 0, 0, 0.5);
}
```

Erweitere `api.js`:

```javascript
// === WETTER-API INTEGRATION ===

// Elemente holen
let cityInput = document.getElementById("city-input");
let weatherButton = document.getElementById("weather-button");
let weatherLoading = document.getElementById("weather-loading");
let weatherDisplay = document.getElementById("weather-display");
let weatherError = document.getElementById("weather-error");
let weatherCity = document.getElementById("weather-city");
let weatherTemp = document.getElementById("weather-temp");
let weatherWind = document.getElementById("weather-wind");
let weatherCoords = document.getElementById("weather-coords");

// Event Listener
weatherButton.addEventListener("click", ladeWetter);

// Enter-Taste im Suchfeld
cityInput.addEventListener("keypress", function(event) {
    if (event.key === "Enter") {
        ladeWetter();
    }
});

// Funktion zum Laden der Wetter-Daten
async function ladeWetter() {
    let stadt = cityInput.value.trim();
    
    // Validierung
    if (stadt === "") {
        zeigeWetterFehler("Bitte gib eine Stadt ein");
        return;
    }
    
    try {
        // Loading-State
        weatherLoading.classList.remove("versteckt");
        weatherDisplay.classList.add("versteckt");
        weatherError.classList.add("versteckt");
        weatherButton.disabled = true;
        
        console.log(`Suche Wetter für: ${stadt}`);
        
        // SCHRITT 1: Geocoding (Stadt → Koordinaten)
        let geoUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(stadt)}&count=1&language=de&format=json`;
        
        console.log("Geocoding-Request:", geoUrl);
        
        let geoResponse = await fetch(geoUrl);
        
        if (!geoResponse.ok) {
            throw new Error("Geocoding-Fehler");
        }
        
        let geoDaten = await geoResponse.json();
        
        console.log("Geocoding-Daten:", geoDaten);
        
        // Stadt nicht gefunden
        if (!geoDaten.results || geoDaten.results.length === 0) {
            zeigeWetterFehler(`Stadt "${stadt}" nicht gefunden`);
            return;
        }
        
        let lat = geoDaten.results[0].latitude;
        let lon = geoDaten.results[0].longitude;
        let stadtName = geoDaten.results[0].name;
        let land = geoDaten.results[0].country || "";
        
        console.log(`Koordinaten: ${lat}, ${lon}`);
        
        // SCHRITT 2: Wetter-Daten abrufen
        let wetterUrl = `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true`;
        
        console.log("Wetter-Request:", wetterUrl);
        
        let wetterResponse = await fetch(wetterUrl);
        
        if (!wetterResponse.ok) {
            throw new Error("Wetter-API-Fehler");
        }
        
        let wetterDaten = await wetterResponse.json();
        
        console.log("Wetter-Daten:", wetterDaten);
        
        // Daten extrahieren
        let temperatur = wetterDaten.current_weather.temperature;
        let windgeschwindigkeit = wetterDaten.current_weather.windspeed;
        
        // Anzeige aktualisieren
        weatherCity.textContent = `${stadtName}${land ? ", " + land : ""}`;
        weatherTemp.textContent = `${temperatur}°C`;
        weatherWind.textContent = `${windgeschwindigkeit} km/h`;
        weatherCoords.textContent = `${lat.toFixed(2)}°N, ${lon.toFixed(2)}°E`;
        
        // Display einblenden
        weatherDisplay.classList.remove("versteckt");
        
        console.log("✅ Wetter erfolgreich geladen");
        
    } catch (fehler) {
        console.error("Fehler beim Laden des Wetters:", fehler);
        zeigeWetterFehler("Fehler beim Laden der Wetter-Daten. Bitte versuche es später nochmal.");
        
    } finally {
        weatherLoading.classList.add("versteckt");
        weatherButton.disabled = false;
    }
}

// Hilfsfunktion für Fehlermeldungen
function zeigeWetterFehler(nachricht) {
    weatherError.textContent = nachricht;
    weatherError.classList.remove("versteckt");
    weatherDisplay.classList.add("versteckt");
    weatherLoading.classList.add("versteckt");
    weatherButton.disabled = false;
}

console.log("Wetter-Funktion registriert");
```

---

### Teil 3: DevTools-Inspektion (15 Min)

Öffne die Browser-DevTools und untersuche die API-Requests:

1. **Network Tab öffnen:** Drücke F12 → wähle "Network" Tab
2. **Request auslösen:** Klicke "Neues Zitat laden"
3. **Request inspizieren:**
   - Klicke auf den Request in der Liste
   - Schaue dir Headers, Preview und Response an
4. **Console Tab:** Sieh dir alle console.log-Ausgaben an

**Aufgabe:** Beantworte folgende Fragen durch Inspektion:

- Wie lange hat der Request gedauert?
- Welchen HTTP-Status-Code hat die Antwort?
- Welche HTTP-Methode wurde verwendet? (GET, POST, etc.)
- Wie gross ist die Response?

---

## Erfolgskriterien

- [ ] Zitat-Button lädt neue Zitate von der API
- [ ] Loading-Spinner wird während des Requests angezeigt
- [ ] Zitat und Autor werden korrekt angezeigt
- [ ] Fehlerbehandlung funktioniert (teste mit falscher URL)
- [ ] Wetter-Suche findet Städte korrekt
- [ ] Wetter-Daten werden angezeigt (Temperatur, Wind, Koordinaten)
- [ ] Fehlermeldung bei nicht gefundener Stadt
- [ ] Enter-Taste im Suchfeld funktioniert
- [ ] Loading-States verhindern mehrfache Requests
- [ ] Alle console.log-Ausgaben erscheinen in DevTools
- [ ] Network Tab zeigt alle API-Requests
- [ ] Keine JavaScript-Fehler in der Konsole

---

## Tipps

- **fetch(url):** Startet HTTP-Request, gibt Promise zurück
- **async/await:** Moderne Syntax für asynchronen Code
- **try-catch-finally:** Fehlerbehandlung bei async-Funktionen
- **response.ok:** Prüft, ob HTTP-Status 200-299 ist
- **response.json():** Wandelt Response-Body in JavaScript-Objekt um
- **encodeURIComponent():** Kodiert Strings für URLs (wichtig bei Sonderzeichen)

**Häufige Fehler:**
- `await` ohne `async` Funktion
- `response.json()` ohne `await`
- HTTP-Status nicht prüfen (response.ok)
- Fehlerbehandlung vergessen (try-catch)
- CORS-Fehler bei nicht-öffentlichen APIs

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen synchronem und asynchronem Code?**  
   *Warum ist asynchroner Code wichtig für Web-Apps?*

2. **Was ist ein Promise und wie funktioniert es?**  
   *Recherchiere: Welche drei Zustände hat ein Promise?*

3. **Warum brauchen wir zwei fetch-Requests für das Wetter?**  
   *Könnte man das in einem Request lösen?*

4. **Die APIs sind kostenlos und ohne API-Key. Was sind die Nachteile?**  
   *Recherchiere: Rate Limits, API-Keys, Authentication*

5. **Wie würdest du die Wetter-App erweitern?**  
   *Ideen: 5-Tage-Vorhersage, Wetter-Icons, Favoriten speichern*

---

## Weiterführende Links

**Fetch API:**
- [MDN: Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN: fetch() Method](https://developer.mozilla.org/de/docs/Web/API/fetch)
- [JavaScript.info: Fetch](https://javascript.info/fetch)

**Async/Await:**
- [MDN: async function](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN: await](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/await)
- [JavaScript.info: Async/await](https://javascript.info/async-await)

**APIs zum Üben:**
- [Public APIs (GitHub)](https://github.com/public-apis/public-apis) – Riesige Liste kostenloser APIs
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) – Fake REST API
- [Open-Meteo](https://open-meteo.com/) – Kostenlose Wetter-API

**HTTP & REST:**
- [MDN: HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [HTTP Status Codes](https://httpstatuses.com/)
- [REST API Tutorial](https://restfulapi.net/)

---

**Geschätzte Zeit:** 60 Minuten  
**Nächster Schritt:** Auftrag 3 – Erweiterte API-Integration mit Datenverarbeitung
