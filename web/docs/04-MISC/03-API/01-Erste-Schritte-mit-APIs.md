# Auftrag 1: Erste Schritte mit APIs

## Ziel

Du lernst, wie du mit JavaScript Daten von einer API abrufst und in der Konsole ausgibst. Du verstehst das grundlegende Prinzip von HTTP-Requests und Responses.

## Beschreibung

APIs sind überall: Wenn du auf Instagram scrollst, beim Online-Shopping einkaufst oder das Wetter checkst – überall werden Daten von APIs geladen. In diesem Auftrag lernst du die Grundlagen: Du rufst Daten von einer Test-API ab und gibst sie in der Konsole aus.

Wir nutzen die **JSONPlaceholder API** – eine kostenlose Test-API mit Posts, Usern und Kommentaren. Kein API-Key nötig, perfekt zum Lernen!

---

### Teil 1: Erste API-Anfrage mit fetch() (20 Min)

**API-Endpunkt:** JSONPlaceholder bietet eine kostenlose Test-API:
- Einzelner Post: `https://jsonplaceholder.typicode.com/posts/1`
- Alle Posts: `https://jsonplaceholder.typicode.com/posts`
- [API-Dokumentation](https://jsonplaceholder.typicode.com/)

**Aufgabe:** Erstelle eine Datei **`api-basics.js`** und implementiere einen API-Call.

**Grundgerüst:**

```javascript
// =====================================================
// API BASICS – Erste Schritte
// =====================================================

console.log("=== API BASICS ===");

// === AUFGABE 1: EINZELNEN POST ABRUFEN ===

console.log("\n1. Einzelnen Post laden...");

// TODO: Verwende fetch() um Post mit ID 1 zu laden
// URL: 'https://jsonplaceholder.typicode.com/posts/1'

fetch('...')
  .then(response => {
    // TODO: Logge den Status-Code
    console.log("Status-Code:", ...);

    // TODO: Wandle Response zu JSON um (return response.json())
    return ...;
  })
  .then(data => {
    // TODO: Gib die Post-Daten in der Konsole aus
    // Zeige: ID, Titel, Text, User-ID
    console.log("Post-Daten:");
    console.log("ID:", ...);
    console.log("Titel:", ...);
    // ... weitere Felder
  })
  .catch(error => {
    // TODO: Fehlerbehandlung
    console.error("❌ Fehler:", ...);
  });
```

**Binde die Datei in dein HTML ein:**
```html
<script src="api-basics.js"></script>
```

**Was passiert hier?**

1. `fetch()` sendet eine GET-Anfrage an die API
2. `.then(response => ...)` verarbeitet die Antwort vom Server
3. `response.json()` wandelt die Antwort in JavaScript-Objekt um
4. `.then(data => ...)` arbeitet mit den JSON-Daten
5. `.catch(error => ...)` fängt Fehler ab

**Öffne die Browser-Konsole und du siehst:**

```
=== API BASICS ===

1. Einzelnen Post laden...
Status-Code: 200
Status OK: true

Post-Daten:
ID: 1
Titel: sunt aut facere repellat provident occaecati excepturi optio reprehenderit
Text: quia et suscipit suscipit recusandae consequuntur...
User-ID: 1
```

---

### Teil 2: Liste von Posts abrufen (20 Min)

**Aufgabe:** Erweitere `api-basics.js` um eine Funktion, die ALLE Posts lädt.

**Anforderungen:**
1. Lade alle Posts von `https://jsonplaceholder.typicode.com/posts`
2. Logge die Anzahl der geladenen Posts
3. Zeige die ersten 5 Posts mit Titel und User-ID an
4. Nutze eine Schleife (`for` oder `.forEach()`)

**Grundgerüst:**

```javascript
// === AUFGABE 2: LISTE VON POSTS ABRUFEN ===

console.log("\n2. Liste von Posts laden...");

fetch('...')  // TODO: URL einfügen
  .then(response => ...)  // TODO: Zu JSON umwandeln
  .then(posts => {
    // TODO: Logge die Anzahl der Posts
    console.log("Anzahl Posts:", ...);

    console.log("\nErste 5 Posts:");

    // TODO: Schleife durch die ersten 5 Posts
    // Tipp: for (let i = 0; i < 5; i++) { ... }
    // Oder: posts.slice(0, 5).forEach(post => { ... })

  })
  .catch(error => {
    console.error("❌ Fehler:", ...);
  });
```

**Wo nachschlagen?**
- [MDN: fetch() API](https://developer.mozilla.org/de/docs/Web/API/Fetch_API)
- [MDN: Array.forEach()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [JSONPlaceholder Guide](https://jsonplaceholder.typicode.com/guide/)

---

### Teil 3: User-Daten abrufen und kombinieren (25 Min)

**Aufgabe:** Lade User-Daten und deren Posts in **verketteten Requests**.

**Anforderungen:**
1. Lade User mit ID 1: `https://jsonplaceholder.typicode.com/users/1`
2. Zeige Name, Email, Stadt und Firma an
3. Lade dann alle Posts dieses Users: `https://jsonplaceholder.typicode.com/posts?userId=1`
4. Zeige die Anzahl und die ersten 3 Post-Titel an

**Grundgerüst:**

```javascript
// === AUFGABE 3: USER-DATEN UND POSTS KOMBINIEREN ===

console.log("\n3. User-Daten laden...");

// TODO: Lade User mit ID 1
fetch('...')
  .then(response => ...)
  .then(user => {
    // TODO: Zeige User-Informationen an
    console.log("\nUser-Informationen:");
    console.log("Name:", ...);
    console.log("Email:", ...);
    console.log("Stadt:", ...);  // Tipp: user.address.city
    console.log("Firma:", ...);  // Tipp: user.company.name

    // TODO: Lade Posts von diesem User
    // Tipp: return fetch(`...?userId=${user.id}`)
    return ...;
  })
  .then(response => ...)
  .then(userPosts => {
    // TODO: Zeige Anzahl Posts an
    console.log("\nAnzahl Posts:", ...);

    // TODO: Zeige erste 3 Post-Titel an
    console.log("\nErste 3 Posts:");
    // Tipp: userPosts.slice(0, 3).forEach(...)
  })
  .catch(error => {
    console.error("❌ Fehler:", ...);
  });
```

**Neue Konzepte:**
- **Verkettete Requests:** Erst User laden, dann Posts basierend auf User-ID
- **Query-Parameter:** `?userId=1` filtert die API-Ergebnisse
- **Verschachtelte Objekte:** `user.address.city` oder `user.company.name`

**Wo nachschlagen?**
- [MDN: Promise Chaining](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Using_promises#chaining)
- [Array.slice()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

**Output:**

```
3. User-Daten laden...

User-Informationen:
Name: Leanne Graham
Username: Bret
Email: Sincere@april.biz
Stadt: Gwenborough
Firma: Romaguera-Crona

Anzahl Posts von diesem User: 10

Erste 3 Posts:
- sunt aut facere repellat provident occaecati excepturi optio reprehenderit
- qui est esse
- ea molestias quasi exercitationem repellat provident
```

---

### Teil 4: Fehlerbehandlung verstehen (15 Min)

**Aufgabe:** Implementiere robuste Fehlerbehandlung für API-Calls.

**Anforderungen:**
1. Teste mit einer **ungültigen** Post-ID: `posts/999999`
2. Prüfe den Status-Code
3. Wenn Status nicht OK (200-299), werfe einen Fehler
4. Fange den Fehler mit `.catch()` ab

**Grundgerüst:**

```javascript
// === AUFGABE 4: FEHLERBEHANDLUNG ===

console.log("\n4. Fehlerbehandlung testen...");

// TODO: Versuche eine ungültige Post-ID zu laden
fetch('...')  // /posts/999999
  .then(response => {
    // TODO: Logge den Status-Code
    console.log("Status:", ...);

    // TODO: Prüfe ob Request erfolgreich war (!response.ok)
    if (...) {
      // TODO: Werfe einen Fehler mit throw new Error(...)
    }

    return response.json();
  })
  .then(data => {
    console.log("Daten:", data);
  })
  .catch(error => {
    // TODO: Fange den Fehler ab und zeige hilfreiche Meldung
    console.error("❌ Fehler:", ...);
  });
```

**Wichtige Status-Codes:**

```
200 = ✅ Erfolg
201 = ✅ Erstellt (nach POST)
400 = ❌ Falsche Anfrage
401 = ❌ Nicht autorisiert (API-Key fehlt)
404 = ❌ Nicht gefunden
500 = ❌ Server-Fehler
```

---

## Erfolgskriterien

- [ ] `api-basics.js` erstellt und eingebunden
- [ ] Einzelnen Post von API geladen
- [ ] Status-Code in Konsole angezeigt
- [ ] Liste von Posts geladen (alle 100)
- [ ] Erste 5 Posts durchlaufen und ausgegeben
- [ ] User-Daten geladen und angezeigt
- [ ] Posts eines Users gefiltert
- [ ] Fehlerbehandlung mit try-catch implementiert
- [ ] Status-Codes verstanden (200, 404, 500)
- [ ] Ausgaben sind übersichtlich formatiert

---

## Tipps

**fetch() Grundstruktur:**
```javascript
fetch(url)
  .then(response => response.json())  // Response → JSON
  .then(data => { /* Daten nutzen */ })
  .catch(error => { /* Fehler behandeln */ });
```

**Promises verstehen:**
- `fetch()` gibt ein **Promise** zurück
- `.then()` wird ausgeführt, wenn Promise erfolgreich ist
- `.catch()` wird bei Fehlern ausgeführt
- Promises sind asynchron – Code läuft weiter während Request läuft

**Häufige Fehler:**

1. **Vergessen, `return response.json()` zu schreiben**
   ```javascript
   .then(response => {
     response.json();  // ❌ Fehlt return!
   })
   ```

2. **Falsche URL**
   ```javascript
   fetch('https://api.beispiel.com')  // ❌ Gibt's nicht
   ```

3. **Keine Fehlerbehandlung**
   ```javascript
   fetch(url).then(...)  // ❌ .catch() fehlt
   ```

**Debugging-Tipps:**
- Öffne Network-Tab in DevTools (F12 → Network)
- Sieh dir die Request-URL an
- Prüfe Status-Code (200 = OK, 404 = nicht gefunden)
- Schau dir die Response-Daten an

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `fetch()` und `console.log()`?**  
   *Tipp: Welcher Code ist synchron, welcher asynchron?*

2. **Warum brauchen wir `.then()` bei fetch()?**  
   *Recherchiere: Was sind Promises in JavaScript?*

3. **Was passiert, wenn die API offline ist?**  
   *Teste es: Ändere die URL zu einer nicht-existierenden Adresse.*

4. **Warum ist Status-Code 200 wichtig?**  
   *Was bedeuten 404, 500, 401? Wann treten sie auf?*

5. **Wie könntest du mehrere API-Calls parallel machen?**  
   *Recherchiere: `Promise.all()` für parallele Requests.*

---

## Weiterführende Links

**fetch() Grundlagen:**
- [MDN: fetch() API](https://developer.mozilla.org/de/docs/Web/API/Fetch_API)
- [MDN: Using fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [JavaScript.info: Fetch](https://javascript.info/fetch)

**Promises verstehen:**
- [MDN: Promises](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [JavaScript.info: Promises, async/await](https://javascript.info/async)

**HTTP Status-Codes:**
- [MDN: HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [HTTP Status Dogs](https://httpstatusdogs.com/) (lustige Erklärung)

**Test-APIs zum Üben:**
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/)
- [ReqRes](https://reqres.in/)
- [Open-Meteo (Wetter-API)](https://open-meteo.com/)

**Videos:**
- [Web Dev Simplified: fetch() in 100 Seconds](https://www.youtube.com/watch?v=cuEtnrL9-H0)
- [The Net Ninja: Async JavaScript Tutorial](https://www.youtube.com/watch?v=ZcQyJ-gxke0)

---

**⏱️ Geschätzte Zeit:** 60 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 zeigst du die API-Daten im HTML – nicht nur in der Konsole!
