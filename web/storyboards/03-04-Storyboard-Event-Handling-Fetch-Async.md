# Storyboard: Event Handling, Ajax/Fetch und asynchrone Calls

**Thema:** JavaScript Event Handling, Fetch API und asynchrone Programmierung  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Gesamtdauer:** ca. 14-16 Minuten  
**Lernziele:** 
- Events verstehen und mit addEventListener reagieren
- Formulare und Benutzereingaben verarbeiten
- Fetch API für HTTP-Requests nutzen
- Asynchrone Programmierung mit async/await verstehen
- Öffentliche APIs einbinden

---

## Szene 1: Intro & Motivation (35 Sek)

**Sprechertext:**
"Willkommen zurück! Bisher haben wir statische Inhalte mit JavaScript geändert. Jetzt wird es richtig interaktiv. Du lernst, wie deine Website auf Benutzeraktionen reagiert – Klicks, Tastatureingaben, Formulare. Und noch besser: Mit der Fetch API holst du Daten von externen Servern, ohne die Seite neu zu laden. Das ist die Grundlage moderner Web-Apps. Von einfachen Buttons bis zu komplexen API-Integrationen – das alles schauen wir uns heute an."

**Bildschirm:**
- Split-Screen zeigen
- Links: Statische Seite (keine Interaktion)
- Rechts: Interaktive Seite mit:
  - Button-Klicks mit Reaktion
  - Live-Suche
  - API-Daten werden geladen (Wetter, Zitate)
- Cursor zeigt auf verschiedene interaktive Elemente

**Dauer:** 35 Sekunden

---

## Szene 2: Was sind Events? (40 Sek)

**Sprechertext:**
"Ein Event ist eine Benutzeraktion oder ein Browser-Ereignis. Klicks, Tastatureingaben, Mausbewegungen – alles sind Events. Der Browser erkennt diese Events automatisch. Mit JavaScript können wir auf diese Events reagieren. Das nennt man Event Handling. Wir registrieren einen Event Listener, der auf ein bestimmtes Event wartet. Wenn das Event eintritt, führt JavaScript unseren Code aus. Schauen wir uns die wichtigsten Events an."

**Bildschirm:**
- Grafik zeigen: Event-Flow-Diagramm
```
Benutzer klickt Button
        ↓
Browser erkennt Event
        ↓
Event Listener reagiert
        ↓
JavaScript-Funktion wird ausgeführt
```
- Liste wichtigster Events einblenden:
  - click – Mausklick
  - input – Eingabe in Textfeld
  - submit – Formular absenden
  - keydown – Taste drücken
  - load – Seite fertig geladen
  - scroll – Seite scrollen

**Dauer:** 40 Sekunden

---

## Szene 3: Erster Event Listener – Click-Event (50 Sek)

**Sprechertext:**
"Der häufigste Event-Typ: der Click. Ich erstelle einen Button im HTML mit einer ID. In JavaScript hole ich den Button mit getElementById und registriere einen Event Listener mit addEventListener. Die Methode braucht zwei Parameter: den Event-Typ als String und eine Funktion, die ausgeführt wird. Diese Funktion heisst Callback-Funktion. Wichtig: Wir schreiben click ohne on – nicht onclick, sondern click."

**Bildschirm:**
- VS Code Split: HTML links, JavaScript rechts
- HTML live eingeben:
```html
<section id="events-demo">
    <h2>Event Handling Demo</h2>
    
    <button id="klick-button" class="btn-primary">
        Klick mich!
    </button>
    <p id="klick-ausgabe">Noch nicht geklickt...</p>
</section>
```

- JavaScript live eingeben:
```javascript
// Button-Element holen
let button = document.getElementById("klick-button");
let ausgabe = document.getElementById("klick-ausgabe");

// Event Listener registrieren
button.addEventListener("click", function() {
    ausgabe.textContent = "Button wurde geklickt!";
    console.log("Click-Event ausgelöst");
});
```

- Hervorheben:
  - `.addEventListener("click", ...)`
  - Callback-Funktion als zweiter Parameter

**Dauer:** 50 Sekunden

---

## Szene 4: Event-Objekt nutzen (45 Sek)

**Sprechertext:**
"Jede Event-Funktion bekommt automatisch ein Event-Objekt übergeben. Dieses Objekt enthält Informationen über das Event. Zum Beispiel: Welches Element wurde geklickt? Wo war die Maus? Welche Taste wurde gedrückt? Ich erweitere das Beispiel: Die Callback-Funktion bekommt einen Parameter – üblicherweise nennen wir ihn e oder event. Mit event.target greife ich auf das Element zu, das das Event ausgelöst hat."

**Bildschirm:**
- VS Code: JavaScript erweitern:
```javascript
button.addEventListener("click", function(event) {
    // Event-Objekt nutzen
    console.log("Event-Typ:", event.type);
    console.log("Geklicktes Element:", event.target);
    console.log("Mausposition X:", event.clientX);
    console.log("Mausposition Y:", event.clientY);
    
    // Element ändern
    event.target.textContent = "Schon geklickt!";
    event.target.style.backgroundColor = "#0066cc";
});
```

- Browser: Konsole zeigen
- Nach Klick: Konsolen-Output zeigen mit allen Informationen
- Hervorheben: `event.target`, `event.clientX/Y`

**Dauer:** 45 Sekunden

---

## Szene 5: Input-Events – Live-Suche (55 Sek)

**Sprechertext:**
"Input-Events reagieren auf Texteingaben. Perfekt für Live-Suche oder Validierung. Ich erstelle ein Suchfeld. Mit dem input-Event wird bei jeder Änderung im Textfeld eine Funktion ausgelöst. Mit event.target.value greife ich auf den aktuellen Wert des Eingabefeldes zu. Jetzt kann ich eine Liste filtern, während der Benutzer tippt. Das ist die Grundlage für Autocomplete und Live-Suche."

**Bildschirm:**
- HTML live eingeben:
```html
<div class="demo-box">
    <h3>Live-Suche</h3>
    <input type="text" id="suche" placeholder="Nach Skills suchen...">
    <p id="such-ergebnis">Gib etwas ein...</p>
</div>
```

- JavaScript live eingeben:
```javascript
// Skills-Liste als Beispiel
let skills = ["HTML", "CSS", "JavaScript", "React", "Node.js", "Python"];

let suchfeld = document.getElementById("suche");
let ergebnis = document.getElementById("such-ergebnis");

suchfeld.addEventListener("input", function(event) {
    let suchbegriff = event.target.value.toLowerCase();
    console.log("Suche nach:", suchbegriff);
    
    // Filtern
    let gefunden = skills.filter(function(skill) {
        return skill.toLowerCase().includes(suchbegriff);
    });
    
    // Ergebnis anzeigen
    if (suchbegriff === "") {
        ergebnis.textContent = "Gib etwas ein...";
    } else if (gefunden.length > 0) {
        ergebnis.textContent = "Gefunden: " + gefunden.join(", ");
    } else {
        ergebnis.textContent = "Keine Ergebnisse";
    }
});
```

- Browser: Live-Demo zeigen – tippen und Ergebnis erscheint sofort

**Dauer:** 55 Sekunden

---

## Szene 6: Formular-Events & Validierung (60 Sek)

**Sprechertext:**
"Formulare sind zentral im Web. Mit dem submit-Event fangen wir das Absenden ab. Wichtig: event.preventDefault verhindert, dass die Seite neu lädt. Das ist die Standard-Aktion bei Formularen. Wir wollen aber die Daten mit JavaScript verarbeiten. Ich baue ein Kontaktformular mit Validierung. Wenn Felder leer sind, zeigen wir eine Fehlermeldung. Wenn alles korrekt ist, bestätigen wir die Eingabe."

**Bildschirm:**
- HTML live eingeben:
```html
<div class="demo-box">
    <h3>Kontaktformular</h3>
    <form id="kontakt-form">
        <input type="text" id="name-input" placeholder="Dein Name" required>
        <input type="email" id="email-input" placeholder="Deine E-Mail" required>
        <textarea id="nachricht-input" placeholder="Deine Nachricht" required></textarea>
        <button type="submit">Absenden</button>
    </form>
    <p id="form-feedback"></p>
</div>
```

- JavaScript live eingeben:
```javascript
let form = document.getElementById("kontakt-form");
let feedback = document.getElementById("form-feedback");

form.addEventListener("submit", function(event) {
    // Verhindert Seiten-Reload
    event.preventDefault();
    console.log("Formular abgesendet");
    
    // Werte auslesen
    let name = document.getElementById("name-input").value;
    let email = document.getElementById("email-input").value;
    let nachricht = document.getElementById("nachricht-input").value;
    
    // Einfache Validierung
    if (name === "" || email === "" || nachricht === "") {
        feedback.textContent = "Bitte alle Felder ausfüllen!";
        feedback.style.color = "red";
        return;
    }
    
    // Erfolg
    feedback.textContent = `Danke, ${name}! Nachricht erhalten.`;
    feedback.style.color = "green";
    
    // Formular zurücksetzen
    form.reset();
});
```

- Hervorheben: `event.preventDefault()`
- Browser: Demo zeigen – Fehler und Erfolg

**Dauer:** 60 Sekunden

---

## Szene 7: Asynchrone Programmierung – Das Problem (50 Sek)

**Sprechertext:**
"Jetzt wird es spannend: Daten vom Server holen. Das Problem: HTTP-Requests dauern Zeit. JavaScript wartet nicht – es läuft einfach weiter. Das nennt man asynchrone Programmierung. Stell dir vor: Du bestellst Pizza. Du wartest nicht an der Tür, bis sie kommt – du machst andere Dinge. Wenn es klingelt, reagierst du. Genauso funktioniert asynchroner Code. Wir starten einen Request, machen weiter, und wenn die Daten da sind, verarbeiten wir sie."

**Bildschirm:**
- Grafik: Synchron vs. Asynchron
```
SYNCHRON (blockierend):
Code 1 → Code 2 → Request (WARTET) → Code 3
                     ⏱️ 2 Sekunden

ASYNCHRON (non-blocking):
Code 1 → Code 2 → Request startet → Code 3
                        ↓ (läuft parallel)
                   Request fertig → Callback
```

- Code-Beispiel für Vergleich:
```javascript
// SYNCHRON (blockiert)
let daten = holeDatenVomServer();  // ⏱️ WARTET 2 Sekunden
console.log(daten);
console.log("Fertig");

// ASYNCHRON (blockiert nicht)
holeDatenVomServer(function(daten) {
    console.log(daten);  // ⏱️ Wird später ausgeführt
});
console.log("Fertig");  // ⏱️ Wird sofort ausgeführt
```

**Dauer:** 50 Sekunden

---

## Szene 8: Fetch API – Daten abrufen (60 Sek)

**Sprechertext:**
"Die Fetch API ist der moderne Standard für HTTP-Requests. Sie arbeitet asynchron mit Promises. Ein Promise ist ein Versprechen: Ich hole dir Daten, aber ich weiss noch nicht, wann ich fertig bin. Mit .then verarbeiten wir die Daten, wenn sie da sind. Ich zeige ein Beispiel: Wir holen ein zufälliges Zitat von einer öffentlichen API. Fetch gibt ein Promise zurück. Das erste .then wandelt die Antwort in JSON um. Das zweite .then verarbeitet die Daten. Mit .catch fangen wir Fehler ab."

**Bildschirm:**
- HTML live eingeben:
```html
<div class="demo-box">
    <h3>Zufälliges Zitat</h3>
    <button id="zitat-button">Neues Zitat laden</button>
    <blockquote id="zitat-ausgabe">
        Klicke auf den Button...
    </blockquote>
    <p id="zitat-autor"></p>
</div>
```

- JavaScript live eingeben:
```javascript
let zitatButton = document.getElementById("zitat-button");
let zitatAusgabe = document.getElementById("zitat-ausgabe");
let zitatAutor = document.getElementById("zitat-autor");

zitatButton.addEventListener("click", function() {
    // Loading-State anzeigen
    zitatAusgabe.textContent = "Lade Zitat...";
    zitatAutor.textContent = "";
    
    // API-Request
    fetch("https://api.quotable.io/random")
        .then(function(response) {
            // Antwort in JSON umwandeln
            return response.json();
        })
        .then(function(daten) {
            // Daten verarbeiten
            console.log("Zitat erhalten:", daten);
            zitatAusgabe.textContent = `"${daten.content}"`;
            zitatAutor.textContent = `— ${daten.author}`;
        })
        .catch(function(fehler) {
            // Fehlerbehandlung
            console.error("Fehler:", fehler);
            zitatAusgabe.textContent = "Fehler beim Laden :(";
        });
    
    console.log("Request gestartet (läuft asynchron)");
});
```

- Hervorheben:
  - `fetch(url)` startet Request
  - `.then()` Verkettung
  - `.catch()` für Fehler

**Dauer:** 60 Sekunden

---

## Szene 9: Async/Await – Moderne Syntax (55 Sek)

**Sprechertext:**
"Async/Await macht asynchronen Code lesbarer. Statt .then-Ketten schreiben wir Code, der aussieht wie synchroner Code. Das Keyword async vor einer Funktion markiert sie als asynchron. Mit await warten wir auf ein Promise. Der Code pausiert hier, aber blockiert nicht den Browser. Ich schreibe das Zitat-Beispiel um mit async/await. Viel übersichtlicher! Mit try-catch fangen wir Fehler ab."

**Bildschirm:**
- VS Code: Neuer Code zeigen:
```javascript
// Moderne Variante mit async/await
zitatButton.addEventListener("click", async function() {
    try {
        // Loading-State
        zitatAusgabe.textContent = "Lade Zitat...";
        zitatAutor.textContent = "";
        
        // API-Request (await wartet auf Antwort)
        let response = await fetch("https://api.quotable.io/random");
        let daten = await response.json();
        
        // Daten verarbeiten
        console.log("Zitat erhalten:", daten);
        zitatAusgabe.textContent = `"${daten.content}"`;
        zitatAutor.textContent = `— ${daten.author}`;
        
    } catch (fehler) {
        // Fehlerbehandlung
        console.error("Fehler:", fehler);
        zitatAusgabe.textContent = "Fehler beim Laden :(";
    }
});
```

- Vergleich zeigen:
```
PROMISE-SYNTAX (.then):
fetch(url)
  .then(response => response.json())
  .then(daten => verarbeiten(daten))
  .catch(fehler => behandeln(fehler));

ASYNC/AWAIT-SYNTAX:
try {
  let response = await fetch(url);
  let daten = await response.json();
  verarbeiten(daten);
} catch (fehler) {
  behandeln(fehler);
}
```

**Dauer:** 55 Sekunden

---

## Szene 10: API mit Parametern – Wetter-App (70 Sek)

**Sprechertext:**
"Jetzt bauen wir etwas Praktisches: Eine Wetter-App. Wir nutzen die OpenMeteo API – kostenlos, ohne API-Key. Der Benutzer gibt eine Stadt ein, wir holen die Koordinaten und dann die Wetter-Daten. Das zeigt, wie man APIs mit Parametern nutzt. Query-Parameter werden an die URL angehängt mit Fragezeichen und Ampersand. Ich baue ein Suchfeld für die Stadt. Bei der Eingabe starten wir zwei API-Requests: Erst Geocoding für Koordinaten, dann Wetter-Daten."

**Bildschirm:**
- HTML live eingeben:
```html
<div class="demo-box">
    <h3>Wetter-Suche</h3>
    <input type="text" id="stadt-input" placeholder="Stadt eingeben...">
    <button id="wetter-button">Wetter abrufen</button>
    <div id="wetter-ausgabe"></div>
</div>
```

- JavaScript live eingeben (gekürzt für Video):
```javascript
let wetterButton = document.getElementById("wetter-button");
let stadtInput = document.getElementById("stadt-input");
let wetterAusgabe = document.getElementById("wetter-ausgabe");

wetterButton.addEventListener("click", async function() {
    let stadt = stadtInput.value;
    
    if (stadt === "") {
        wetterAusgabe.innerHTML = "<p>Bitte Stadt eingeben</p>";
        return;
    }
    
    try {
        wetterAusgabe.innerHTML = "<p>Lade Wetter-Daten...</p>";
        
        // 1. Geocoding: Stadt → Koordinaten
        let geoUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${stadt}&count=1&language=de`;
        let geoResponse = await fetch(geoUrl);
        let geoDaten = await geoResponse.json();
        
        if (!geoDaten.results || geoDaten.results.length === 0) {
            wetterAusgabe.innerHTML = "<p>Stadt nicht gefunden</p>";
            return;
        }
        
        let lat = geoDaten.results[0].latitude;
        let lon = geoDaten.results[0].longitude;
        let stadtName = geoDaten.results[0].name;
        
        console.log(`Koordinaten für ${stadtName}:`, lat, lon);
        
        // 2. Wetter-Daten holen
        let wetterUrl = `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true`;
        let wetterResponse = await fetch(wetterUrl);
        let wetterDaten = await wetterResponse.json();
        
        let temp = wetterDaten.current_weather.temperature;
        let windspeed = wetterDaten.current_weather.windspeed;
        
        // Anzeige
        wetterAusgabe.innerHTML = `
            <h4>${stadtName}</h4>
            <p><strong>Temperatur:</strong> ${temp}°C</p>
            <p><strong>Windgeschwindigkeit:</strong> ${windspeed} km/h</p>
        `;
        
    } catch (fehler) {
        console.error("Fehler:", fehler);
        wetterAusgabe.innerHTML = "<p>Fehler beim Laden der Daten</p>";
    }
});
```

- Hervorheben:
  - Query-Parameter: `?name=${stadt}&count=1`
  - Template Literals in URLs
  - Zwei verkettete API-Requests

**Dauer:** 70 Sekunden

---

## Szene 11: Loading States & UX (45 Sek)

**Sprechertext:**
"Wichtig für gute User Experience: Loading States. Während der Request läuft, zeigen wir dem Benutzer, dass etwas passiert. Ich füge einen Spinner hinzu. Bevor der Request startet, zeige ich den Spinner und deaktiviere den Button. Nach dem Request verstecke ich den Spinner wieder. Das verhindert auch mehrfache Requests. Das macht deine App professionell und benutzerfreundlich."

**Bildschirm:**
- CSS für Spinner zeigen:
```css
.loading-spinner {
    border: 3px solid #f3f3f3;
    border-top: 3px solid #0066cc;
    border-radius: 50%;
    width: 30px;
    height: 30px;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.versteckt {
    display: none;
}
```

- JavaScript erweitern:
```javascript
async function ladeWetter() {
    // Spinner anzeigen
    spinner.classList.remove("versteckt");
    wetterButton.disabled = true;
    
    try {
        // ... API-Request ...
    } finally {
        // Spinner verstecken (immer, auch bei Fehler)
        spinner.classList.add("versteckt");
        wetterButton.disabled = false;
    }
}
```

- Browser: Demo mit Spinner zeigen

**Dauer:** 45 Sekunden

---

## Szene 12: Fehlerbehandlung & HTTP-Status (50 Sek)

**Sprechertext:**
"Nicht jeder Request funktioniert. Server können offline sein, URLs falsch, oder du hast Rate Limits überschritten. Fetch wirft nur bei Netzwerkfehlern einen Error – nicht bei HTTP-Statuscodes wie 404 oder 500. Du musst response.ok prüfen. Das ist true bei Status 200-299. Ich zeige dir eine robuste Fehlerbehandlung. Prüfe zuerst response.ok, dann verarbeite die Daten. Im catch-Block fängst du Netzwerkfehler ab. So gibst du dem Benutzer hilfreiche Fehlermeldungen."

**Bildschirm:**
- Code zeigen:
```javascript
async function robusterRequest(url) {
    try {
        let response = await fetch(url);
        
        // HTTP-Status prüfen
        if (!response.ok) {
            throw new Error(`HTTP-Fehler! Status: ${response.status}`);
        }
        
        let daten = await response.json();
        return daten;
        
    } catch (fehler) {
        // Unterschiedliche Fehlertypen behandeln
        if (fehler.name === "TypeError") {
            console.error("Netzwerkfehler:", fehler.message);
            return { fehler: "Keine Verbindung zum Server" };
        } else {
            console.error("API-Fehler:", fehler.message);
            return { fehler: "Daten konnten nicht geladen werden" };
        }
    }
}
```

- Tabelle einblenden:
```
HTTP-Statuscodes:
200-299: Erfolg (OK)
400-499: Client-Fehler (z.B. 404 Not Found)
500-599: Server-Fehler (z.B. 500 Internal Server Error)
```

**Dauer:** 50 Sekunden

---

## Szene 13: DevTools – Network Tab (45 Sek)

**Sprechertext:**
"Die DevTools helfen beim Debugging. Im Network Tab siehst du alle HTTP-Requests. Klicke auf einen Request, um Details zu sehen: URL, HTTP-Methode, Status Code, Response. Du kannst die Response direkt anschauen – super zum Testen. Im Console Tab siehst du deine console.log-Ausgaben und Fehler. Wenn ein Request fehlschlägt, steht hier warum. Nutze die DevTools immer beim Entwickeln!"

**Bildschirm:**
- DevTools öffnen: F12
- Network Tab anklicken
- Request auslösen (Wetter-Button klicken)
- Request in Network Tab zeigen:
  - Name (URL)
  - Status (200 OK)
  - Type (fetch)
  - Size
  - Time
- Request anklicken → Details zeigen:
  - Headers Tab
  - Preview Tab (JSON formatiert)
  - Response Tab (Roh-JSON)
- Console Tab zeigen mit console.log-Ausgaben

**Dauer:** 45 Sekunden

---

## Szene 14: Best Practices & Performance (55 Sek)

**Sprechertext:**
"Ein paar Best Practices: Erstens: Nutze async/await statt .then – besser lesbar. Zweitens: Immer try-catch für Fehlerbehandlung. Drittens: Loading States zeigen – der Benutzer muss wissen, dass etwas passiert. Viertens: Requests debouncing bei Live-Suche – nicht bei jedem Tastendruck einen Request. Warte 300ms nach der letzten Eingabe. Fünftens: API-Keys nie im Frontend-Code – das ist unsicher. Nutze einen Backend-Proxy. Sechstens: Rate Limits beachten – viele APIs limitieren Requests pro Minute."

**Bildschirm:**
- Checkliste einblenden:
```
✓ async/await nutzen
✓ try-catch für Fehler
✓ Loading States zeigen
✓ Debouncing bei häufigen Events
✓ API-Keys im Backend halten
✓ Rate Limits beachten
✓ Response-Daten validieren
✓ Timeouts setzen
```

- Code-Beispiel Debouncing:
```javascript
let timeout;
suchfeld.addEventListener("input", function(e) {
    clearTimeout(timeout);
    timeout = setTimeout(function() {
        // Request erst nach 300ms Pause
        sucheAPI(e.target.value);
    }, 300);
});
```

**Dauer:** 55 Sekunden

---

## Szene 15: Öffentliche APIs – Ressourcen (40 Sek)

**Sprechertext:**
"Es gibt Tausende kostenlose, öffentliche APIs zum Üben. Ich zeige dir die besten Ressourcen. Public APIs auf GitHub – eine riesige Liste nach Kategorien. JSONPlaceholder für Fake-Daten zum Testen. OpenMeteo für Wetter ohne API-Key. The Cat API für zufällige Katzenbilder. PokeAPI für Pokemon-Daten. Experimentiere mit verschiedenen APIs – das ist der beste Weg zu lernen. Achte immer auf Rate Limits und Nutzungsbedingungen."

**Bildschirm:**
- Liste einblenden mit Links:
```
KOSTENLOSE APIs zum Üben:

• Public APIs (GitHub)
  github.com/public-apis/public-apis
  → Kategorisierte Liste mit 1000+ APIs

• JSONPlaceholder
  jsonplaceholder.typicode.com
  → Fake REST API für Testing

• OpenMeteo
  open-meteo.com
  → Wetter-Daten ohne API-Key

• The Cat API
  thecatapi.com
  → Zufällige Katzenbilder

• PokeAPI
  pokeapi.co
  → Pokemon-Daten

• Quotable
  github.com/lukePeavey/quotable
  → Zufällige Zitate
```

**Dauer:** 40 Sekunden

---

## Szene 16: Zusammenfassung & Ausblick (45 Sek)

**Sprechertext:**
"Fassen wir zusammen: Mit addEventListener reagierst du auf Benutzeraktionen. Events wie click, input und submit machen deine Seite interaktiv. Mit der Fetch API holst du Daten von Servern. Promises und async/await ermöglichen asynchrone Programmierung. Du kannst jetzt externe APIs einbinden und dynamische Web-Apps bauen. Das sind die Grundlagen moderner Webentwicklung! In den Aufträgen baust du jetzt eine echte Portfolio-Seite mit API-Integration. Viel Erfolg!"

**Bildschirm:**
- Mind-Map mit Hauptkonzepten:
```
EVENT HANDLING
├── addEventListener()
├── Event-Objekt
├── Click, Input, Submit
└── Formular-Validierung

FETCH API
├── HTTP-Requests
├── Promises
├── .then() / .catch()
└── async/await

BEST PRACTICES
├── Fehlerbehandlung
├── Loading States
├── Debouncing
└── Rate Limits
```

- Vorschau Aufträge zeigen:
  - Interaktive Skill-Bewertung
  - API-Integration (Wetter/Zitate)
  - Formular mit Validierung

- Outro-Animation mit Logo

**Dauer:** 45 Sekunden

---

## Gesamtdauer

Ca. 14-16 Minuten (je nach Tempo)

---

## Benötigte Materialien für Video

### 1. Demo-HTML-Datei
**Datei:** `events-demo.html` (vollständiges Beispiel)

### 2. Demo-JavaScript-Dateien
- **Datei:** `events-basic.js` (Click, Input, Submit Events)
- **Datei:** `fetch-demo.js` (Fetch API mit async/await)
- **Datei:** `wetter-app.js` (Vollständige Wetter-App)

### 3. CSS für Demo
**Datei:** `events-demo.css` (Styling für alle Demos)

### 4. Animationen & Grafiken
- Event-Flow-Diagramm (Benutzer → Browser → Event → JavaScript)
- Synchron vs. Asynchron Vergleich
- HTTP-Statuscodes Tabelle
- Mind-Map für Zusammenfassung
- API-Logos (OpenMeteo, Quotable, etc.)

### 5. Code-Snippets für Overlay-Anzeige
- addEventListener Syntax-Highlight
- Fetch-Verkettung (.then-Chain)
- Async/Await Syntax
- Error Handling Pattern

### 6. Browser-Screenshots
- DevTools Network Tab (mit Request-Details)
- Console mit Fetch-Logs
- JSON-Response-Vorschau

---

## Technische Hinweise für Produktion

- Alle API-Requests live zeigen (nicht fake)
- Internet-Verbindung während Aufnahme testen
- Loading-Zeiten eventuell beschleunigen (Video-Schnitt)
- Konsolen-Logs deutlich sichtbar machen
- Fehler absichtlich provozieren (z.B. falsche URL) für Demo
- Animations-Timing: Spinner-Animation smooth einstellen
- Font-Size in DevTools erhöhen für bessere Lesbarkeit

---

## Weiterführende Demo-Ideen für Video

1. **Button Counter:** Click-Event zählt Klicks
2. **Character Counter:** Input-Event zeigt verbleibende Zeichen
3. **Dark Mode Toggle:** Event ändert Theme
4. **Live-Uhr mit API:** Fetch World Time API
5. **Chuck Norris Witze:** Random Joke API
6. **GitHub-User-Suche:** GitHub API mit Profil-Anzeige

Diese können als Quick-Wins zwischen Hauptszenen gezeigt werden.
