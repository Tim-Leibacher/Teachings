# Storyboard: API Grundlagen

**Video-Titel:** API Grundlagen – Was ist eine API?  
**Gesamtdauer:** ca. 10-12 Minuten  
**Zielgruppe:** 1. Lehrjahr Informatiker/in EFZ Applikationsentwicklung  
**Voraussetzungen:** JSON-Grundlagen abgeschlossen

---

## Intro (30 Sek.)

### Sprechertext
"Willkommen zum Thema API Grundlagen! APIs sind überall in der modernen Webentwicklung. Wenn du auf Instagram ein Bild hochlädst, beim Online-Shopping bezahlst oder das Wetter auf einer Website siehst – überall stecken APIs dahinter. In diesem Video lernst du, was APIs sind, wie sie funktionieren, und welche Sicherheitsaspekte wichtig sind. Los geht's!"

### Bildschirmdarstellung
Animierter Title-Screen mit BAND Design (Gradient blau-türkis):
```
API Grundlagen
──────────────
Was ist eine API?
REST vs. SOAP
Sicherheitsaspekte
```

### Hinweise
- BAND Farbschema: #0066CC (blau) → #00C9A7 (türkis)
- Font: Aptos
- Musik: Subtiler Tech-Beat (fade in/out)

---

## Szene 1: Was ist eine API? (2 Min)

### Sprechertext
"API steht für Application Programming Interface – auf Deutsch: Programmierschnittstelle. Eine API ist wie ein Kellner im Restaurant. Du als Gast sitzt am Tisch und möchtest etwas bestellen. Der Kellner nimmt deine Bestellung entgegen, bringt sie in die Küche, und kommt mit dem Essen zurück. Die Küche musst du nicht betreten – der Kellner ist die Schnittstelle zwischen dir und der Küche. Genauso funktioniert eine API: Deine App schickt eine Anfrage, die API leitet sie an einen Server weiter, und der Server schickt die Antwort zurück."

### Bildschirmdarstellung

**Animation: Restaurant-Metapher**
```
┌─────────────┐        ┌──────────┐        ┌─────────────┐
│   Du        │ ─────> │  Kellner │ ─────> │   Küche     │
│  (Client)   │ <───── │  (API)   │ <───── │  (Server)   │
└─────────────┘        └──────────┘        └─────────────┘
   Anfrage              Vermittlung           Datenbank
```

**Danach zeigen: Reales Beispiel in VS Code**
```javascript
// Anfrage an eine API senden
fetch('https://api.wetter.com/heute')
  .then(response => response.json())
  .then(data => console.log(data));
```

**In der Browser-Konsole zeigen:**
```json
{
  "temperatur": 18,
  "wetter": "sonnig",
  "stadt": "Bern"
}
```

### Hinweise
- Split-Screen: Animation links (50%), Code rechts (50%)
- Markiere `fetch()` farbig
- Zeige JSON-Response formatiert mit Syntax-Highlighting
- Text-Overlay: "API = Vermittler zwischen Client und Server"

---

## Szene 2: Wie funktioniert eine API? (2 Min)

### Sprechertext
"Eine API funktioniert nach dem Client-Server-Prinzip. Der Client – also deine Website oder App – sendet eine Anfrage. Diese Anfrage geht über das Internet an den Server. Der Server verarbeitet die Anfrage, sucht in der Datenbank nach den gewünschten Informationen, und schickt eine Antwort zurück. Die Daten kommen meist im JSON-Format an – das haben wir bereits kennengelernt. Schauen wir uns ein konkretes Beispiel an."

### Bildschirmdarstellung

**Schritt-für-Schritt-Animation:**

```
Schritt 1: Client sendet Anfrage
┌──────────────┐
│ GET /wetter  │ ───────────────────>
│ Stadt: Bern  │
└──────────────┘

Schritt 2: Server verarbeitet Anfrage
                              ┌─────────────┐
                              │  Datenbank  │
                              │  abfragen   │
                              └─────────────┘

Schritt 3: Server sendet Antwort
                   <─────────────────── ┌──────────────┐
                                         │ JSON-Daten   │
                                         │ zurücksenden │
                                         └──────────────┘
```

**Danach: Reales Beispiel mit öffentlicher API**

VS Code:
```javascript
// Beispiel: Wetter-API
const stadt = "Bern";
const apiUrl = `https://api.open-meteo.com/v1/forecast?latitude=46.95&longitude=7.45&current_weather=true`;

fetch(apiUrl)
  .then(response => response.json())
  .then(data => {
    console.log("Temperatur:", data.current_weather.temperature, "°C");
    console.log("Windgeschwindigkeit:", data.current_weather.windspeed, "km/h");
  });
```

**Browser-Konsole:**
```
Temperatur: 18 °C
Windgeschwindigkeit: 12 km/h
```

### Hinweise
- Animation mit Pfeilen und Kästen
- Zeige echten API-Call mit fetch()
- Markiere JSON-Struktur in der Antwort farbig
- Text-Overlay: "Client → Server → Datenbank → Server → Client"

---

## Szene 3: REST vs. SOAP (2:30 Min)

### Sprechertext
"Es gibt verschiedene Arten von APIs. Die zwei wichtigsten sind REST und SOAP. REST steht für Representational State Transfer – das ist der moderne Standard. REST-APIs nutzen HTTP-Methoden wie GET, POST, PUT und DELETE. Sie sind einfach zu nutzen und arbeiten meist mit JSON. SOAP steht für Simple Object Access Protocol – das ist ein älterer Standard. SOAP-APIs nutzen XML statt JSON und haben striktere Regeln. In der Webentwicklung nutzen wir heute fast ausschliesslich REST-APIs."

### Bildschirmdarstellung

**Vergleichstabelle (animiert, Punkt für Punkt):**

```
┌─────────────────┬──────────────────┬──────────────────┐
│                 │       REST       │       SOAP       │
├─────────────────┼──────────────────┼──────────────────┤
│ Protokoll       │ HTTP             │ HTTP, SMTP, TCP  │
│ Datenformat     │ JSON, XML, HTML  │ Nur XML          │
│ Komplexität     │ Einfach          │ Komplex          │
│ Performance     │ Schnell          │ Langsamer        │
│ Verbreitung     │ Sehr hoch        │ Abnehmend        │
└─────────────────┴──────────────────┴──────────────────┘
```

**Beispiel: REST-API-Anfrage**

VS Code:
```javascript
// REST API – Einfach und modern
fetch('https://api.github.com/users/bitsbeats')
  .then(response => response.json())
  .then(data => {
    console.log("Name:", data.name);
    console.log("Repos:", data.public_repos);
  });
```

Browser-Konsole:
```
Name: Bits Beats
Repos: 42
```

**Beispiel: SOAP-API-Anfrage (nur zeigen, nicht im Detail erklären)**

VS Code:
```xml
<!-- SOAP API – Komplex und veraltet -->
<soap:Envelope>
  <soap:Body>
    <GetUser>
      <UserId>12345</UserId>
    </GetUser>
  </soap:Body>
</soap:Envelope>
```

### Hinweise
- Vergleichstabelle animiert einblenden (Zeile für Zeile)
- REST-Beispiel grün markieren (modern)
- SOAP-Beispiel rot/grau markieren (veraltet)
- Text-Overlay: "REST = modern & einfach | SOAP = veraltet & komplex"

---

## Szene 4: HTTP-Methoden in REST (2 Min)

### Sprechertext
"REST-APIs nutzen vier Hauptmethoden: GET zum Abrufen von Daten, POST zum Erstellen neuer Daten, PUT zum Aktualisieren bestehender Daten, und DELETE zum Löschen von Daten. Diese Methoden entsprechen den vier Grundoperationen: Lesen, Erstellen, Aktualisieren, Löschen. Das nennt man auch CRUD – Create, Read, Update, Delete. Schauen wir uns Beispiele an."

### Bildschirmdarstellung

**Übersichtstabelle:**

```
┌──────────┬─────────────────┬──────────────────────────┐
│ Methode  │  Aktion         │  Beispiel                │
├──────────┼─────────────────┼──────────────────────────┤
│ GET      │  Daten abrufen  │  /users/123              │
│ POST     │  Daten erstellen│  /users (mit Body)       │
│ PUT      │  Daten ändern   │  /users/123 (mit Body)   │
│ DELETE   │  Daten löschen  │  /users/123              │
└──────────┴─────────────────┴──────────────────────────┘
```

**Code-Beispiele:**

VS Code:
```javascript
// GET – Daten abrufen
fetch('https://api.beispiel.com/users/123')
  .then(response => response.json())
  .then(data => console.log(data));

// POST – Neuen User erstellen
fetch('https://api.beispiel.com/users', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name: "Sarah Müller",
    email: "sarah@beispiel.com"
  })
});

// PUT – User aktualisieren
fetch('https://api.beispiel.com/users/123', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name: "Sarah Schmidt"
  })
});

// DELETE – User löschen
fetch('https://api.beispiel.com/users/123', {
  method: 'DELETE'
});
```

### Hinweise
- Tabelle animiert einblenden
- Jede Methode farbig markieren (GET = grün, POST = blau, PUT = orange, DELETE = rot)
- Text-Overlay: "CRUD = Create, Read, Update, Delete"

---

## Szene 5: Sicherheitsaspekte bei APIs (2:30 Min)

### Sprechertext
"Sicherheit ist bei APIs extrem wichtig. Drei zentrale Konzepte: Authentifizierung prüft, wer du bist. Autorisierung prüft, was du darfst. Verschlüsselung schützt die Daten während der Übertragung. Die meisten APIs nutzen API-Keys oder OAuth zur Authentifizierung. HTTPS verschlüsselt die Verbindung – das ist Standard für sichere Kommunikation. Ohne Sicherheit könnten Angreifer Daten stehlen oder manipulieren."

### Bildschirmdarstellung

**Sicherheitskonzepte (animiert):**

```
┌─────────────────────┐
│  Authentifizierung  │ ───> Wer bist du?
│  (Authentication)   │      API-Key, OAuth, JWT
└─────────────────────┘

┌─────────────────────┐
│  Autorisierung      │ ───> Was darfst du?
│  (Authorization)    │      Rollen & Rechte
└─────────────────────┘

┌─────────────────────┐
│  Verschlüsselung    │ ───> HTTPS (TLS/SSL)
│  (Encryption)       │      Sichere Übertragung
└─────────────────────┘
```

**Code-Beispiel: API-Key nutzen**

VS Code:
```javascript
// API-Key in der Anfrage senden
const apiKey = "dein-geheimer-api-key-12345";

fetch('https://api.beispiel.com/daten', {
  headers: {
    'Authorization': `Bearer ${apiKey}`
  }
})
  .then(response => response.json())
  .then(data => console.log(data));
```

**Sicherheits-Checkliste:**

```
✅ HTTPS nutzen (nicht HTTP)
✅ API-Keys geheim halten
✅ Keine sensiblen Daten im Code
✅ Rate Limiting beachten
✅ Fehler richtig behandeln
```

### Hinweise
- Sicherheitskonzepte nacheinander einblenden
- API-Key im Code zensieren (****)
- Checkliste mit grünen Häkchen animieren
- Text-Overlay: "Nie API-Keys im öffentlichen Code!"

---

## Szene 6: Praktisches Beispiel – Öffentliche API nutzen (2 Min)

### Sprechertext
"Schauen wir uns ein praktisches Beispiel an. Wir nutzen die JSONPlaceholder API – eine kostenlose Test-API. Wir rufen eine Liste von Posts ab und zeigen sie in der Konsole. Das ist ein typisches Beispiel für GET-Requests."

### Bildschirmdarstellung

**VS Code – neues HTML-Dokument:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API Demo</title>
</head>
<body>
    <h1>API Grundlagen Demo</h1>
    <button id="lade-posts">Posts laden</button>
    <div id="ausgabe"></div>
    
    <script src="api-demo.js"></script>
</body>
</html>
```

**VS Code – api-demo.js:**

```javascript
// =====================================================
// API DEMO – Posts von JSONPlaceholder laden
// =====================================================

console.log("=== API DEMO ===");

// Button-Element holen
const button = document.getElementById('lade-posts');
const ausgabe = document.getElementById('ausgabe');

// Event-Listener für Button
button.addEventListener('click', function() {
    console.log("Lade Posts von API...");
    
    // API-Anfrage senden
    fetch('https://jsonplaceholder.typicode.com/posts')
        .then(response => {
            console.log("Status:", response.status);
            return response.json();
        })
        .then(posts => {
            console.log("Anzahl Posts:", posts.length);
            
            // Erste 5 Posts anzeigen
            posts.slice(0, 5).forEach(post => {
                console.log(`Post ${post.id}: ${post.title}`);
            });
            
            // Im HTML anzeigen
            ausgabe.innerHTML = `<p>${posts.length} Posts geladen!</p>`;
        })
        .catch(error => {
            console.error("Fehler:", error);
        });
});
```

**Browser-Konsole nach Button-Klick:**
```
=== API DEMO ===
Lade Posts von API...
Status: 200
Anzahl Posts: 100
Post 1: sunt aut facere repellat provident
Post 2: qui est esse
Post 3: ea molestias quasi exercitationem
Post 4: eum et est occaecati
Post 5: nesciunt quas odio
```

### Hinweise
- Split-Screen: VS Code links, Browser rechts
- Button-Klick animieren
- Konsolen-Ausgabe Zeile für Zeile einblenden
- Markiere `fetch()`, `.then()`, `.catch()` farbig

---

## Szene 7: Häufige Fehler bei APIs (1:30 Min)

### Sprechertext
"Fehler bei APIs sind normal. Drei häufige Probleme: Erstens, die URL ist falsch geschrieben. Zweitens, die API antwortet nicht oder ist offline. Drittens, du hast keine Berechtigung – der API-Key fehlt oder ist falsch. Die Browser-Konsole zeigt dir den Fehler. Status-Codes helfen: 200 heisst Erfolg, 404 heisst nicht gefunden, 401 heisst keine Berechtigung, 500 heisst Server-Fehler."

### Bildschirmdarstellung

**Fehler-Beispiele in VS Code:**

```javascript
// Fehler 1: Falsche URL
fetch('https://api.beispiel.com/falsche-url')
  .then(response => console.log(response.status))
  .catch(error => console.error("Fehler:", error));

// Fehler 2: Fehlender API-Key
fetch('https://api.beispiel.com/geschützt')
  .then(response => console.log(response.status));
```

**Browser-Konsole:**
```
❌ GET https://api.beispiel.com/falsche-url 404 (Not Found)
❌ GET https://api.beispiel.com/geschützt 401 (Unauthorized)
```

**Status-Code-Übersicht:**

```
┌──────────┬─────────────────────────┐
│  Code    │  Bedeutung              │
├──────────┼─────────────────────────┤
│  200     │  ✅ Erfolg              │
│  201     │  ✅ Erstellt            │
│  400     │  ❌ Falsche Anfrage     │
│  401     │  ❌ Nicht autorisiert   │
│  404     │  ❌ Nicht gefunden      │
│  500     │  ❌ Server-Fehler       │
└──────────┴─────────────────────────┘
```

### Hinweise
- Fehler rot markieren
- Status-Codes farbig (grün = 2xx, rot = 4xx/5xx)
- Text-Overlay: "Status-Codes = Sprache der APIs"

---

## Szene 8: Zusammenfassung & Ausblick (1 Min)

### Sprechertext
"Fassen wir zusammen: APIs sind Schnittstellen zwischen deiner App und einem Server. REST ist der moderne Standard, nutzt JSON und HTTP-Methoden wie GET, POST, PUT, DELETE. Sicherheit ist wichtig – nutze HTTPS und schütze deine API-Keys. Mit `fetch()` rufst du APIs auf. Status-Codes helfen dir, Fehler zu verstehen. Im nächsten Video schauen wir uns HTTPS und Verschlüsselung genauer an. Viel Erfolg bei den Aufträgen!"

### Bildschirmdarstellung

**Zusammenfassungs-Checkliste (animiert):**

```
✅ API = Schnittstelle zwischen Client & Server
✅ REST = moderner Standard (JSON, HTTP)
✅ CRUD = Create, Read, Update, Delete
✅ GET, POST, PUT, DELETE = HTTP-Methoden
✅ HTTPS = sichere Verbindung
✅ API-Keys = Authentifizierung
✅ Status-Codes = Erfolg oder Fehler
✅ fetch() = JavaScript-Funktion für APIs
```

### Hinweise
- Checkliste Punkt für Punkt einblenden
- Fade-Out mit BAND Design
- Nächstes Video ankündigen: "HTTPS Grundlagen"

---

## Zusatzmaterialien für Video-Produktion

### Demo-API für Video

**JSONPlaceholder API (kostenlos, kein Key nötig):**
```
https://jsonplaceholder.typicode.com/posts
https://jsonplaceholder.typicode.com/users
https://jsonplaceholder.typicode.com/comments
```

**Open-Meteo API (Wetter, kostenlos):**
```
https://api.open-meteo.com/v1/forecast?latitude=46.95&longitude=7.45&current_weather=true
```

### Vollständiges Code-Beispiel für Video

**api-demo.js (Vollständig):**

```javascript
// =====================================================
// API GRUNDLAGEN – Vollständige Demo
// =====================================================

console.log("🌐 API Demo gestartet");

// === 1. EINFACHER GET-REQUEST ===
console.log("\n=== GET-Request ===");

fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    console.log("Status:", response.status);
    console.log("OK:", response.ok);
    return response.json();
  })
  .then(data => {
    console.log("Post-Titel:", data.title);
    console.log("Post-Body:", data.body);
  })
  .catch(error => {
    console.error("❌ Fehler:", error);
  });

// === 2. MEHRERE POSTS LADEN ===
console.log("\n=== Mehrere Posts laden ===");

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json())
  .then(posts => {
    console.log(`✅ ${posts.length} Posts geladen`);
    
    // Erste 3 Posts anzeigen
    posts.slice(0, 3).forEach(post => {
      console.log(`- ${post.id}: ${post.title}`);
    });
  });

// === 3. POST-REQUEST (Neuen Post erstellen) ===
console.log("\n=== POST-Request ===");

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Mein erster Post',
    body: 'Das ist mein erster Post über APIs!',
    userId: 1
  })
})
  .then(response => response.json())
  .then(data => {
    console.log("✅ Neuer Post erstellt:");
    console.log("ID:", data.id);
    console.log("Titel:", data.title);
  });

// === 4. FEHLERBEHANDLUNG ===
console.log("\n=== Fehlerbehandlung ===");

fetch('https://jsonplaceholder.typicode.com/posts/999999')
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP-Fehler: ${response.status}`);
    }
    return response.json();
  })
  .catch(error => {
    console.error("❌ Fehler aufgetreten:", error.message);
  });

console.log("\n✅ API Demo abgeschlossen");
```

---

## Technische Notizen für Produktion

**Screen-Recording-Einstellungen:**
- Auflösung: 1920x1080 (Full HD)
- FPS: 30
- Codec: H.264
- Audio: 44.1kHz, Stereo

**VS Code Theme:**
- Theme: Dark+ (default dark)
- Font: Fira Code oder Consolas
- Font Size: 16px (gut lesbar im Video)

**Browser:**
- Chrome oder Firefox
- DevTools: F12
- Console-Tab geöffnet
- Zoom: 125% (besser lesbar)

**Animationen:**
- Fade-In: 0.5 Sek.
- Slide-In: 0.3 Sek.
- Text-Overlay: 2 Sek. Anzeigedauer

---

**Gesamtdauer:** ca. 10-12 Minuten  
**Schwierigkeitsgrad:** Mittel  
**Nächstes Video:** HTTPS Grundlagen – SSL/TLS, Zertifikate, Verschlüsselung
