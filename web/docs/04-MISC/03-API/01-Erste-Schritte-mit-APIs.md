# Auftrag 1: Erste Schritte mit APIs

## Ziel

Du lernst, wie du mit JavaScript Daten von einer API abrufst und in der Konsole ausgibst. Du verstehst das grundlegende Prinzip von HTTP-Requests und Responses.

## Beschreibung

APIs sind überall: Wenn du auf Instagram scrollst, beim Online-Shopping einkaufst oder das Wetter checkst – überall werden Daten von APIs geladen. In diesem Auftrag lernst du die Grundlagen: Du rufst Daten von einer Test-API ab und gibst sie in der Konsole aus.

Wir nutzen die **JSONPlaceholder API** – eine kostenlose Test-API mit Posts, Usern und Kommentaren. Kein API-Key nötig, perfekt zum Lernen!

---

### Teil 1: Erste API-Anfrage mit fetch() (15 Min)

Erstelle eine neue Datei **`api-basics.js`** und binde sie ein:

```html
<script src="api-basics.js"></script>
```

**In `api-basics.js`:**

```javascript
// =====================================================
// API BASICS – Erste Schritte
// =====================================================

console.log("=== API BASICS ===");

// === EINEN EINZELNEN POST ABRUFEN ===

console.log("\n1. Einzelnen Post laden...");

// fetch() sendet eine HTTP-Anfrage an die API
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    // response ist die Antwort vom Server
    console.log("Status-Code:", response.status);
    console.log("Status OK:", response.ok);
    
    // JSON-Daten aus der Response extrahieren
    return response.json();
  })
  .then(data => {
    // data enthält jetzt die JSON-Daten
    console.log("\nPost-Daten:");
    console.log("ID:", data.id);
    console.log("Titel:", data.title);
    console.log("Text:", data.body);
    console.log("User-ID:", data.userId);
  })
  .catch(error => {
    // Falls ein Fehler auftritt
    console.error("❌ Fehler:", error);
  });
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

### Teil 2: Liste von Posts abrufen (15 Min)

Erweitere `api-basics.js`:

```javascript
// === LISTE VON POSTS ABRUFEN ===

console.log("\n2. Liste von Posts laden...");

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json())
  .then(posts => {
    // posts ist ein Array mit allen Posts
    console.log("Anzahl Posts:", posts.length);
    
    console.log("\nErste 5 Posts:");
    
    // Schleife durch die ersten 5 Posts
    for (let i = 0; i < 5; i++) {
      const post = posts[i];
      console.log(`\nPost ${post.id}:`);
      console.log(`Titel: ${post.title}`);
      console.log(`User-ID: ${post.userId}`);
    }
  })
  .catch(error => {
    console.error("❌ Fehler:", error);
  });
```

**Output:**

```
2. Liste von Posts laden...
Anzahl Posts: 100

Erste 5 Posts:

Post 1:
Titel: sunt aut facere repellat provident occaecati excepturi optio reprehenderit
User-ID: 1

Post 2:
Titel: qui est esse
User-ID: 1

Post 3:
Titel: ea molestias quasi exercitationem repellat provident
User-ID: 1

...
```

---

### Teil 3: User-Daten abrufen und kombinieren (20 Min)

Jetzt kombinieren wir Posts mit User-Informationen:

```javascript
// === USER-DATEN ABRUFEN ===

console.log("\n3. User-Daten laden...");

// Zuerst User laden
fetch('https://jsonplaceholder.typicode.com/users/1')
  .then(response => response.json())
  .then(user => {
    console.log("\nUser-Informationen:");
    console.log("Name:", user.name);
    console.log("Username:", user.username);
    console.log("Email:", user.email);
    console.log("Stadt:", user.address.city);
    console.log("Firma:", user.company.name);
    
    // Jetzt Posts von diesem User laden
    return fetch(`https://jsonplaceholder.typicode.com/posts?userId=${user.id}`);
  })
  .then(response => response.json())
  .then(userPosts => {
    console.log("\nAnzahl Posts von diesem User:", userPosts.length);
    
    console.log("\nErste 3 Posts:");
    userPosts.slice(0, 3).forEach(post => {
      console.log(`- ${post.title}`);
    });
  })
  .catch(error => {
    console.error("❌ Fehler:", error);
  });
```

**Neue Konzepte:**

- **Verkettete Requests:** Erst User laden, dann dessen Posts
- **Query-Parameter:** `?userId=1` filtert Posts nach User
- `.slice(0, 3)` nimmt die ersten 3 Elemente aus dem Array
- `.forEach()` durchläuft alle Elemente

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

### Teil 4: Fehlerbehandlung verstehen (10 Min)

Füge Fehlerbehandlung hinzu:

```javascript
// === FEHLERBEHANDLUNG ===

console.log("\n4. Fehlerbehandlung testen...");

// Absichtlich falscher Endpunkt
fetch('https://jsonplaceholder.typicode.com/posts/999999')
  .then(response => {
    console.log("Status:", response.status);
    
    // Prüfen ob Request erfolgreich war
    if (!response.ok) {
      throw new Error(`HTTP-Fehler: ${response.status}`);
    }
    
    return response.json();
  })
  .then(data => {
    console.log("Daten:", data);
  })
  .catch(error => {
    console.error("❌ Fehler aufgetreten:", error.message);
    console.log("Tipp: Prüfe die URL und versuche es erneut.");
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
