# Auftrag 2: API-Daten im HTML anzeigen

## Ziel

Du lernst, wie du API-Daten nicht nur in der Konsole ausgibst, sondern dynamisch im HTML anzeigst. Das ist der Schritt von der Konsole zur echten Website.

## Beschreibung

Daten in der Konsole zu sehen ist nützlich zum Debuggen, aber deine Benutzer sehen die Konsole nicht. Professionelle Websites zeigen API-Daten direkt im HTML – dynamisch geladen und schön formatiert. In diesem Auftrag erstellst du eine User-Galerie und eine Post-Liste, die Daten von der JSONPlaceholder API laden und anzeigen.

---

### Teil 1: HTML-Struktur für User-Galerie (10 Min)

Erstelle eine neue Sektion für User-Daten:

```html
<section id="api-demo">
    <h2>API Demo – User-Galerie</h2>
    
    <!-- Lade-Button -->
    <button id="lade-users" class="btn-primary">Users laden</button>
    
    <!-- Lade-Indikator -->
    <div id="loading" class="versteckt">
        <p>Lade Daten...</p>
    </div>
    
    <!-- User-Container (wird per JavaScript gefüllt) -->
    <div id="user-container" class="user-grid">
        <!-- Users werden hier dynamisch eingefügt -->
    </div>
</section>
```

---

### Teil 2: CSS für User-Karten (10 Min)

Füge in `styles.css` hinzu:

```css
/* === API DEMO === */
#api-demo {
    padding: 40px 0;
}

.btn-primary {
    background: #0066cc;
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 6px;
    font-size: 1em;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s ease;
    margin-bottom: 20px;
}

.btn-primary:hover {
    background: #0052a3;
}

.btn-primary:active {
    transform: scale(0.98);
}

#loading {
    background: #e7f5ff;
    padding: 20px;
    border-radius: 6px;
    text-align: center;
    color: #0066cc;
    font-weight: 600;
    margin-bottom: 20px;
}

.versteckt {
    display: none;
}

/* User-Grid */
.user-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

/* User-Karte */
.user-karte {
    background: white;
    border: 2px solid #e9ecef;
    border-radius: 8px;
    padding: 20px;
    transition: all 0.3s ease;
}

.user-karte:hover {
    border-color: #0066cc;
    box-shadow: 0 6px 12px rgba(0, 102, 204, 0.15);
    transform: translateY(-4px);
}

.user-karte h3 {
    color: #0066cc;
    margin-bottom: 10px;
    font-size: 1.2em;
}

.user-info {
    display: flex;
    flex-direction: column;
    gap: 8px;
    color: #495057;
    font-size: 0.95em;
}

.user-info strong {
    color: #212529;
    font-weight: 600;
}

.user-email {
    color: #0066cc;
    text-decoration: none;
}

.user-email:hover {
    text-decoration: underline;
}

.user-firma {
    background: #f8f9fa;
    padding: 10px;
    border-radius: 4px;
    margin-top: 10px;
    font-size: 0.9em;
    color: #6c757d;
}
```

---

### Teil 3: JavaScript – Users laden und anzeigen (30 Min)

**Aufgabe:** Erstelle `api-display.js` und implementiere die Logik zum Laden und Anzeigen von Users.

**Anforderungen:**
1. Button-Click lädt Users von der API
2. Zeige während des Ladens einen Loading-Indikator
3. Erstelle für jeden User eine Karte mit `erstelleUserKarte()`
4. Fehlerbehandlung bei API-Fehlern

**Grundgerüst:**

```javascript
// =====================================================
// API DISPLAY – Daten im HTML anzeigen
// =====================================================

console.log("=== API DISPLAY ===");

// TODO: Hole die notwendigen Elemente aus dem DOM
const ladeButton = document.getElementById('...');
const loadingDiv = document.getElementById('...');
const userContainer = document.getElementById('...');

// TODO: Event-Listener für Button hinzufügen
ladeButton.addEventListener('click', function() {
    console.log("Lade Users von API...");

    // TODO: Loading-Indikator anzeigen
    // Tipp: loadingDiv.classList.remove('versteckt')

    // TODO: Container leeren
    // Tipp: userContainer.innerHTML = ''

    // TODO: Button während des Ladens deaktivieren
    // Tipp: ladeButton.disabled = true

    // TODO: API-Anfrage senden
    fetch('...')  // URL: https://jsonplaceholder.typicode.com/users
        .then(response => ...)
        .then(users => {
            console.log(`✅ ${users.length} Users geladen`);

            // TODO: Loading verstecken
            // TODO: Button wieder aktivieren
            // TODO: Für jeden User eine Karte erstellen
            // Tipp: users.forEach(user => erstelleUserKarte(user))
        })
        .catch(error => {
            // TODO: Fehlerbehandlung
            // - Loading verstecken
            // - Button aktivieren
            // - Fehlermeldung im userContainer anzeigen
        });
});

// === FUNKTION: USER-KARTE ERSTELLEN ===

function erstelleUserKarte(user) {
    // TODO: Erstelle ein div-Element
    const karte = document.createElement('...');
    karte.className = '...';

    // TODO: Fülle die Karte mit User-Daten
    // Nutze Template Literals und innerHTML
    karte.innerHTML = `
        <h3>${...}</h3>
        <div class="user-info">
            <p><strong>Username:</strong> ${...}</p>
            <p><strong>Email:</strong> ${...}</p>
            <p><strong>Stadt:</strong> ${...}</p>
        </div>
    `;

    // TODO: Füge die Karte zum Container hinzu
    userContainer.appendChild(...);
}
```

**Wo nachschlagen?**
- [MDN: createElement()](https://developer.mozilla.org/de/docs/Web/API/Document/createElement)
- [MDN: innerHTML](https://developer.mozilla.org/de/docs/Web/API/Element/innerHTML)
- [MDN: classList](https://developer.mozilla.org/de/docs/Web/API/Element/classList)
- [MDN: Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)

**Binde die Datei ein:**

```html
<script src="api-display.js"></script>
```

---

### Teil 4: Post-Liste mit Details anzeigen (30 Min)

**Aufgabe:** Erweitere deine Seite um eine Post-Liste, die Kommentare nachladen kann.

**Schritt 1:** Erweitere dein HTML um eine Post-Liste:

```html
<section id="posts-demo">
    <h2>Post-Liste</h2>
    
    <button id="lade-posts" class="btn-primary">Posts laden</button>
    
    <div id="post-container" class="post-liste">
        <!-- Posts werden hier dynamisch eingefügt -->
    </div>
</section>
```

**CSS für Posts:**

```css
/* Post-Liste */
.post-liste {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-top: 20px;
}

.post-karte {
    background: white;
    border: 2px solid #e9ecef;
    border-radius: 6px;
    padding: 20px;
    transition: border-color 0.2s ease;
}

.post-karte:hover {
    border-color: #0066cc;
}

.post-karte h3 {
    color: #212529;
    margin-bottom: 10px;
    font-size: 1.1em;
}

.post-meta {
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 10px;
}

.post-body {
    color: #495057;
    line-height: 1.6;
}

.post-details {
    margin-top: 15px;
    padding-top: 15px;
    border-top: 1px solid #e9ecef;
}

.post-details button {
    background: #6c757d;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 0.9em;
    cursor: pointer;
    transition: background 0.2s ease;
}

.post-details button:hover {
    background: #5a6268;
}

.kommentare {
    margin-top: 15px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 4px;
}

.kommentar {
    padding: 10px;
    background: white;
    border-radius: 4px;
    margin-bottom: 10px;
}

.kommentar:last-child {
    margin-bottom: 0;
}

.kommentar-autor {
    font-weight: 600;
    color: #0066cc;
    margin-bottom: 5px;
}

.kommentar-email {
    font-size: 0.85em;
    color: #6c757d;
    margin-bottom: 8px;
}

.kommentar-text {
    color: #495057;
    font-size: 0.95em;
}
```

**Schritt 2: JavaScript implementieren**

**Anforderungen:**
1. Lade die ersten 10 Posts: `https://jsonplaceholder.typicode.com/posts?_limit=10`
2. Erstelle für jeden Post eine Karte mit `erstellePostKarte()`
3. Implementiere `ladeKommentare()` zum Nachladen von Kommentaren
4. Kommentare-Button soll zwischen "Anzeigen" und "Verbergen" togglen

**Grundgerüst:**

```javascript
// === POSTS LADEN UND ANZEIGEN ===

const ladePostsButton = document.getElementById('...');
const postContainer = document.getElementById('...');

ladePostsButton.addEventListener('click', function() {
    // TODO: Lade die ersten 10 Posts
    // URL: https://jsonplaceholder.typicode.com/posts?_limit=10

    // TODO: Zeige Loading-Nachricht
    // TODO: Deaktiviere Button

    fetch('...')
        .then(...)
        .then(posts => {
            // TODO: Leere Container
            // TODO: Für jeden Post eine Karte erstellen
            // TODO: Button wieder aktivieren
        })
        .catch(error => {
            // TODO: Fehlerbehandlung
        });
});

// === FUNKTION: POST-KARTE ERSTELLEN ===

function erstellePostKarte(post) {
    // TODO: Erstelle Post-Karte mit Titel, Body und Button
    // Button soll ladeKommentare() aufrufen mit Post-ID
    // Tipp: onclick="ladeKommentare(${post.id}, this)"
}

// === FUNKTION: KOMMENTARE LADEN ===

function ladeKommentare(postId, button) {
    // TODO: Hole das Kommentare-Div
    const kommentareDiv = document.getElementById(`kommentare-${postId}`);

    // TODO: Toggle - wenn sichtbar, verstecke es
    if (!kommentareDiv.classList.contains('versteckt')) {
        // ... verstecken und Button-Text ändern
        return;
    }

    // TODO: Lade Kommentare von API
    // URL: https://jsonplaceholder.typicode.com/posts/${postId}/comments

    // TODO: Erstelle für jeden Kommentar ein div
    // Zeige: Name, Email, Text
}
```

**Wo nachschlagen?**
- [Query-Parameter in URLs](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
- [onclick Event-Handler](https://developer.mozilla.org/de/docs/Web/API/GlobalEventHandlers/onclick)

---

## Erfolgskriterien

- [ ] HTML-Sektion für User-Galerie erstellt
- [ ] CSS für User-Karten hinzugefügt
- [ ] `api-display.js` erstellt und eingebunden
- [ ] Button "Users laden" funktioniert
- [ ] Lade-Indikator wird während des Ladens angezeigt
- [ ] Users werden als Karten im HTML angezeigt
- [ ] User-Daten sind korrekt formatiert (Name, Email, Stadt, Firma)
- [ ] Post-Liste mit "Posts laden"-Button erstellt
- [ ] Posts werden dynamisch geladen und angezeigt
- [ ] Button "Kommentare anzeigen" lädt Kommentare nach
- [ ] Kommentare werden ein-/ausgeblendet beim Klick
- [ ] Fehlerbehandlung funktioniert (bei Netzwerkfehler)

---

## Tipps

**DOM-Manipulation mit API-Daten:**
- `createElement()` erstellt neue HTML-Elemente
- `.innerHTML` setzt HTML-Inhalt
- `.appendChild()` fügt Element zum Container hinzu
- Template Literals (`${}`) für dynamische Werte

**Lade-Status anzeigen:**
```javascript
button.disabled = true;      // Button deaktivieren
button.textContent = 'Lädt...';  // Text ändern

// Nach dem Laden:
button.disabled = false;
button.textContent = 'Neu laden';
```

**Fehlerbehandlung:**
```javascript
.catch(error => {
    console.error("Fehler:", error);
    container.innerHTML = '<p>Fehler beim Laden.</p>';
});
```

**Häufige Fehler:**

1. **Vergessen, Element aus DOM zu holen**
   ```javascript
   const button = document.getElementById('mein-button');
   if (!button) {
       console.error("Button nicht gefunden!");
   }
   ```

2. **innerHTML überschreibt vorherigen Inhalt**
   ```javascript
   container.innerHTML = '';  // Erst leeren
   container.appendChild(neuesElement);  // Dann hinzufügen
   ```

3. **Event-Listener vor DOM-Ready**
   ```javascript
   // Script am Ende von <body> oder:
   document.addEventListener('DOMContentLoaded', function() {
       // Hier Code
   });
   ```

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `.innerHTML` und `.textContent`?**  
   *Tipp: Was passiert, wenn du HTML-Code als Text einfügst?*

2. **Warum deaktivieren wir den Button während des Ladens?**  
   *Was könnte passieren, wenn der User mehrmals klickt?*

3. **Wie könntest du eine Suchfunktion für die User-Liste einbauen?**  
   *Tipp: Filter-Array-Methode und Input-Event-Listener*

4. **Was passiert, wenn die API 1000 Users zurückgibt?**  
   *Wie würdest du Pagination (Seitennummerierung) einbauen?*

5. **Wie könntest du die Posts nach Datum sortieren?**  
   *Recherchiere: Array.sort() mit Vergleichsfunktion*

---

## Weiterführende Links

**DOM-Manipulation:**
- [MDN: Document Object Model (DOM)](https://developer.mozilla.org/de/docs/Web/API/Document_Object_Model)
- [MDN: createElement()](https://developer.mozilla.org/de/docs/Web/API/Document/createElement)
- [JavaScript.info: Modifying the document](https://javascript.info/modifying-document)

**Template Literals:**
- [MDN: Template literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)

**Event Handling:**
- [MDN: addEventListener](https://developer.mozilla.org/de/docs/Web/API/EventTarget/addEventListener)

**Loading States:**
- [Web Dev Simplified: Loading States](https://www.youtube.com/watch?v=LyLa7G8kx_Y)

---

**⏱️ Geschätzte Zeit:** 70 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 sendest du Daten AN eine API – POST, PUT, DELETE!
