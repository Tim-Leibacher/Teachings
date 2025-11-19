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

### Teil 3: JavaScript – Users laden und anzeigen (25 Min)

Erstelle `api-display.js`:

```javascript
// =====================================================
// API DISPLAY – Daten im HTML anzeigen
// =====================================================

console.log("=== API DISPLAY ===");

// Elemente holen
const ladeButton = document.getElementById('lade-users');
const loadingDiv = document.getElementById('loading');
const userContainer = document.getElementById('user-container');

// Event-Listener für Button
ladeButton.addEventListener('click', function() {
    console.log("Lade Users von API...");
    
    // Lade-Indikator anzeigen
    loadingDiv.classList.remove('versteckt');
    
    // Container leeren (falls schon Daten geladen wurden)
    userContainer.innerHTML = '';
    
    // Button deaktivieren während des Ladens
    ladeButton.disabled = true;
    ladeButton.textContent = 'Wird geladen...';
    
    // API-Anfrage senden
    fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => {
            console.log("Status:", response.status);
            return response.json();
        })
        .then(users => {
            console.log(`✅ ${users.length} Users geladen`);
            
            // Lade-Indikator verstecken
            loadingDiv.classList.add('versteckt');
            
            // Button wieder aktivieren
            ladeButton.disabled = false;
            ladeButton.textContent = 'Users neu laden';
            
            // Jeden User als Karte anzeigen
            users.forEach(user => {
                erstelleUserKarte(user);
            });
        })
        .catch(error => {
            console.error("❌ Fehler:", error);
            
            // Lade-Indikator verstecken
            loadingDiv.classList.add('versteckt');
            
            // Button wieder aktivieren
            ladeButton.disabled = false;
            ladeButton.textContent = 'Erneut versuchen';
            
            // Fehlermeldung anzeigen
            userContainer.innerHTML = '<p style="color: red;">Fehler beim Laden der Daten. Bitte versuche es erneut.</p>';
        });
});

// === FUNKTION: USER-KARTE ERSTELLEN ===

function erstelleUserKarte(user) {
    // Karte erstellen
    const karte = document.createElement('div');
    karte.className = 'user-karte';
    
    // Karten-Inhalt
    karte.innerHTML = `
        <h3>${user.name}</h3>
        <div class="user-info">
            <p><strong>Username:</strong> ${user.username}</p>
            <p><strong>Email:</strong> <a href="mailto:${user.email}" class="user-email">${user.email}</a></p>
            <p><strong>Telefon:</strong> ${user.phone}</p>
            <p><strong>Website:</strong> <a href="http://${user.website}" target="_blank">${user.website}</a></p>
            <p><strong>Stadt:</strong> ${user.address.city}</p>
        </div>
        <div class="user-firma">
            <strong>Firma:</strong> ${user.company.name}<br>
            <em>${user.company.catchPhrase}</em>
        </div>
    `;
    
    // Karte zum Container hinzufügen
    userContainer.appendChild(karte);
}
```

**Binde die Datei ein:**

```html
<script src="api-display.js"></script>
```

---

### Teil 4: Post-Liste mit Details anzeigen (25 Min)

Erweitere dein HTML um eine Post-Liste:

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

**JavaScript für Posts erweitern:**

```javascript
// === POSTS LADEN UND ANZEIGEN ===

const ladePostsButton = document.getElementById('lade-posts');
const postContainer = document.getElementById('post-container');

ladePostsButton.addEventListener('click', function() {
    console.log("Lade Posts...");
    
    postContainer.innerHTML = '<p style="color: #6c757d;">Lade Posts...</p>';
    
    ladePostsButton.disabled = true;
    ladePostsButton.textContent = 'Wird geladen...';
    
    // Nur die ersten 10 Posts laden
    fetch('https://jsonplaceholder.typicode.com/posts?_limit=10')
        .then(response => response.json())
        .then(posts => {
            console.log(`✅ ${posts.length} Posts geladen`);
            
            postContainer.innerHTML = '';
            
            ladePostsButton.disabled = false;
            ladePostsButton.textContent = 'Posts neu laden';
            
            posts.forEach(post => {
                erstellePostKarte(post);
            });
        })
        .catch(error => {
            console.error("❌ Fehler:", error);
            postContainer.innerHTML = '<p style="color: red;">Fehler beim Laden der Posts.</p>';
            ladePostsButton.disabled = false;
        });
});

// === FUNKTION: POST-KARTE ERSTELLEN ===

function erstellePostKarte(post) {
    const karte = document.createElement('div');
    karte.className = 'post-karte';
    
    karte.innerHTML = `
        <h3>${post.title}</h3>
        <p class="post-meta">Post ID: ${post.id} | User ID: ${post.userId}</p>
        <p class="post-body">${post.body}</p>
        <div class="post-details">
            <button onclick="ladeKommentare(${post.id}, this)">Kommentare anzeigen</button>
            <div class="kommentare versteckt" id="kommentare-${post.id}"></div>
        </div>
    `;
    
    postContainer.appendChild(karte);
}

// === FUNKTION: KOMMENTARE LADEN ===

function ladeKommentare(postId, button) {
    console.log(`Lade Kommentare für Post ${postId}...`);
    
    const kommentareDiv = document.getElementById(`kommentare-${postId}`);
    
    // Toggle: Wenn bereits geladen, ein-/ausblenden
    if (!kommentareDiv.classList.contains('versteckt')) {
        kommentareDiv.classList.add('versteckt');
        button.textContent = 'Kommentare anzeigen';
        return;
    }
    
    // Button-Text ändern
    button.textContent = 'Lädt...';
    button.disabled = true;
    
    // Kommentare von API laden
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`)
        .then(response => response.json())
        .then(kommentare => {
            console.log(`✅ ${kommentare.length} Kommentare geladen`);
            
            kommentareDiv.innerHTML = `<h4>Kommentare (${kommentare.length}):</h4>`;
            
            kommentare.forEach(kommentar => {
                const kommentarDiv = document.createElement('div');
                kommentarDiv.className = 'kommentar';
                
                kommentarDiv.innerHTML = `
                    <div class="kommentar-autor">${kommentar.name}</div>
                    <div class="kommentar-email">${kommentar.email}</div>
                    <div class="kommentar-text">${kommentar.body}</div>
                `;
                
                kommentareDiv.appendChild(kommentarDiv);
            });
            
            kommentareDiv.classList.remove('versteckt');
            
            button.textContent = 'Kommentare verbergen';
            button.disabled = false;
        })
        .catch(error => {
            console.error("❌ Fehler:", error);
            kommentareDiv.innerHTML = '<p style="color: red;">Fehler beim Laden der Kommentare.</p>';
            button.textContent = 'Erneut versuchen';
            button.disabled = false;
        });
}
```

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
