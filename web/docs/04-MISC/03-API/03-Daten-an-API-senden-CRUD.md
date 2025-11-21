# Auftrag 3: Daten an API senden – POST, PUT, DELETE

## Ziel

Du lernst, wie du nicht nur Daten von einer API abrufst (GET), sondern auch Daten erstellen (POST), aktualisieren (PUT) und löschen (DELETE) kannst. Das sind die vier CRUD-Operationen: Create, Read, Update, Delete.

## Beschreibung

Bisher haben wir nur Daten von APIs gelesen. Aber moderne Webanwendungen müssen auch Daten senden: neue Posts erstellen, Kommentare bearbeiten, Einträge löschen. In diesem Auftrag erstellst du ein vollständiges CRUD-Interface für Posts – wie ein Mini-CMS (Content Management System).

**CRUD im Detail:**
- **C**reate = POST (neuen Eintrag erstellen)
- **R**ead = GET (Einträge abrufen)
- **U**pdate = PUT (Eintrag aktualisieren)
- **D**elete = DELETE (Eintrag löschen)

---

### Teil 1: HTML-Formular für neuen Post (15 Min)

Erstelle eine neue Sektion für Post-Verwaltung:

```html
<section id="post-verwaltung">
    <h2>Post-Verwaltung (CRUD)</h2>
    
    <!-- Formular für neuen Post -->
    <div class="formular-container">
        <h3>Neuen Post erstellen</h3>
        
        <form id="post-formular">
            <div class="formular-gruppe">
                <label for="post-titel">Titel:</label>
                <input type="text" id="post-titel" required placeholder="Titel des Posts">
            </div>
            
            <div class="formular-gruppe">
                <label for="post-body">Inhalt:</label>
                <textarea id="post-body" rows="5" required placeholder="Schreibe deinen Post..."></textarea>
            </div>
            
            <div class="formular-gruppe">
                <label for="post-userid">User-ID:</label>
                <input type="number" id="post-userid" value="1" min="1" max="10" required>
            </div>
            
            <button type="submit" class="btn-primary">Post erstellen</button>
        </form>
        
        <div id="formular-feedback" class="versteckt"></div>
    </div>
    
    <!-- Liste aller Posts -->
    <div class="posts-verwaltung">
        <h3>Meine Posts</h3>
        <button id="lade-meine-posts" class="btn-secondary">Posts laden</button>
        
        <div id="meine-posts" class="post-liste">
            <!-- Posts werden hier dynamisch eingefügt -->
        </div>
    </div>
</section>
```

---

### Teil 2: CSS für CRUD-Interface (10 Min)

Füge in `styles.css` hinzu:

```css
/* === POST-VERWALTUNG === */
#post-verwaltung {
    padding: 40px 0;
}

.formular-container {
    background: #f8f9fa;
    padding: 30px;
    border-radius: 8px;
    margin-bottom: 40px;
    border: 2px solid #e9ecef;
}

.formular-container h3 {
    color: #212529;
    margin-bottom: 20px;
}

.formular-gruppe {
    margin-bottom: 20px;
}

.formular-gruppe label {
    display: block;
    font-weight: 600;
    color: #495057;
    margin-bottom: 8px;
}

.formular-gruppe input,
.formular-gruppe textarea {
    width: 100%;
    padding: 12px;
    border: 2px solid #dee2e6;
    border-radius: 6px;
    font-size: 1em;
    font-family: inherit;
    transition: border-color 0.2s ease;
}

.formular-gruppe input:focus,
.formular-gruppe textarea:focus {
    outline: none;
    border-color: #0066cc;
}

.formular-gruppe textarea {
    resize: vertical;
    min-height: 100px;
}

.btn-secondary {
    background: #6c757d;
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

.btn-secondary:hover {
    background: #5a6268;
}

#formular-feedback {
    margin-top: 20px;
    padding: 15px;
    border-radius: 6px;
    font-weight: 600;
}

#formular-feedback.erfolg {
    background: #d4edda;
    color: #155724;
    border: 2px solid #c3e6cb;
}

#formular-feedback.fehler {
    background: #f8d7da;
    color: #721c24;
    border: 2px solid #f5c6cb;
}

/* Post-Karte mit Aktionen */
.post-karte-verwaltung {
    background: white;
    border: 2px solid #e9ecef;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 15px;
}

.post-karte-verwaltung h4 {
    color: #212529;
    margin-bottom: 10px;
}

.post-meta-verwaltung {
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 10px;
}

.post-body-verwaltung {
    color: #495057;
    line-height: 1.6;
    margin-bottom: 15px;
}

.post-aktionen {
    display: flex;
    gap: 10px;
    padding-top: 15px;
    border-top: 1px solid #e9ecef;
}

.btn-edit {
    background: #ffc107;
    color: #212529;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 0.9em;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s ease;
}

.btn-edit:hover {
    background: #e0a800;
}

.btn-delete {
    background: #dc3545;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 0.9em;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s ease;
}

.btn-delete:hover {
    background: #c82333;
}

/* Edit-Formular */
.edit-formular {
    margin-top: 15px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 6px;
}

.edit-formular input,
.edit-formular textarea {
    width: 100%;
    padding: 10px;
    border: 2px solid #dee2e6;
    border-radius: 4px;
    font-size: 0.95em;
    margin-bottom: 10px;
}

.edit-formular-aktionen {
    display: flex;
    gap: 10px;
}

.btn-save {
    background: #28a745;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 0.9em;
    font-weight: 600;
    cursor: pointer;
}

.btn-save:hover {
    background: #218838;
}

.btn-cancel {
    background: #6c757d;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 0.9em;
    font-weight: 600;
    cursor: pointer;
}

.btn-cancel:hover {
    background: #5a6268;
}
```

---

### Teil 3: JavaScript – POST Request (25 Min)

**Aufgabe:** Erstelle `api-crud.js` und implementiere das Erstellen neuer Posts.

**Anforderungen:**
1. Verhindere Standard-Formular-Submit mit `event.preventDefault()`
2. Hole die Formular-Werte (Titel, Body, User-ID)
3. Sende POST-Request mit JSON-Body
4. Zeige Erfolgs- oder Fehlermeldung an

**Grundgerüst:**

```javascript
// =====================================================
// API CRUD – Create, Read, Update, Delete
// =====================================================

console.log("=== API CRUD ===");

// TODO: Hole die notwendigen Elemente
const postFormular = document.getElementById('...');
const feedbackDiv = document.getElementById('...');
const ladePostsButton = document.getElementById('...');
const meinePostsContainer = document.getElementById('...');

// === CREATE: NEUEN POST ERSTELLEN (POST-Request) ===

postFormular.addEventListener('submit', function(event) {
    // TODO: Verhindere Standard-Submit
    event.preventDefault();

    // TODO: Hole die Formular-Werte
    const titel = document.getElementById('...').value;
    const body = ...;
    const userId = ...;

    console.log("Erstelle neuen Post...");

    // TODO: Sende POST-Request
    fetch('...', {  // URL: https://jsonplaceholder.typicode.com/posts
        method: '...',  // POST
        headers: {
            'Content-Type': '...'  // application/json
        },
        body: JSON.stringify({
            // TODO: Objekt mit title, body, userId
        })
    })
    .then(response => ...)
    .then(neuerPost => {
        // TODO: Zeige Erfolgs-Feedback
        // TODO: Setze Formular zurück (postFormular.reset())
        // TODO: Blende Feedback nach 3 Sekunden aus (setTimeout)
    })
    .catch(error => {
        // TODO: Zeige Fehler-Feedback
    });
});
```

**Wo nachschlagen?**
- [MDN: fetch() POST-Beispiel](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#supplying_request_options)
- [MDN: JSON.stringify()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN: FormData](https://developer.mozilla.org/de/docs/Web/API/FormData)

**Was passiert beim POST-Request?**

1. Formular-Daten werden ausgelesen
2. `fetch()` sendet POST-Request mit JSON-Body
3. Header `Content-Type: application/json` informiert API über Datenformat
4. `JSON.stringify()` wandelt JavaScript-Objekt in JSON-String um
5. API antwortet mit neuem Post (inkl. ID)
6. Erfolgs-Feedback wird angezeigt

---

### Teil 4: READ – Posts laden (15 Min)

Erweitere `api-crud.js`:

```javascript
// === READ: POSTS LADEN (GET-Request) ===

ladePostsButton.addEventListener('click', function() {
    console.log("Lade Posts von User 1...");
    
    meinePostsContainer.innerHTML = '<p style="color: #6c757d;">Lade Posts...</p>';
    
    ladePostsButton.disabled = true;
    
    // GET-Request: Posts von User 1
    fetch('https://jsonplaceholder.typicode.com/posts?userId=1')
        .then(response => response.json())
        .then(posts => {
            console.log(`✅ ${posts.length} Posts geladen`);
            
            meinePostsContainer.innerHTML = '';
            
            ladePostsButton.disabled = false;
            
            if (posts.length === 0) {
                meinePostsContainer.innerHTML = '<p style="color: #6c757d;">Keine Posts gefunden.</p>';
                return;
            }
            
            posts.forEach(post => {
                erstellePostKarteVerwaltung(post);
            });
        })
        .catch(error => {
            console.error("❌ Fehler:", error);
            meinePostsContainer.innerHTML = '<p style="color: red;">Fehler beim Laden der Posts.</p>';
            ladePostsButton.disabled = false;
        });
});
```

---

### Teil 5: UPDATE – Post bearbeiten (25 Min)

**Aufgabe:** Implementiere die Bearbeitungs-Funktion für Posts.

**Anforderungen:**
1. `starteEdit()` zeigt das Edit-Formular an
2. `abbrechenEdit()` versteckt das Edit-Formular
3. `speichereEdit()` sendet PUT-Request und aktualisiert die UI
4. Nach erfolgreichem Update: Karte kurz grün färben

**Grundgerüst:**

```javascript
// === FUNKTION: POST-KARTE MIT AKTIONEN ERSTELLEN ===

function erstellePostKarteVerwaltung(post) {
    const karte = document.createElement('div');
    karte.className = 'post-karte-verwaltung';
    karte.id = `post-${post.id}`;
    
    karte.innerHTML = `
        <h4>${post.title}</h4>
        <p class="post-meta-verwaltung">Post ID: ${post.id} | User ID: ${post.userId}</p>
        <p class="post-body-verwaltung">${post.body}</p>
        
        <div class="post-aktionen">
            <button class="btn-edit" onclick="starteEdit(${post.id})">Bearbeiten</button>
            <button class="btn-delete" onclick="loeschePost(${post.id})">Löschen</button>
        </div>
        
        <div id="edit-${post.id}" class="edit-formular versteckt">
            <input type="text" id="edit-titel-${post.id}" value="${post.title}">
            <textarea id="edit-body-${post.id}" rows="4">${post.body}</textarea>
            
            <div class="edit-formular-aktionen">
                <button class="btn-save" onclick="speichereEdit(${post.id})">Speichern</button>
                <button class="btn-cancel" onclick="abbrechenEdit(${post.id})">Abbrechen</button>
            </div>
        </div>
    `;
    
    meinePostsContainer.appendChild(karte);
}

// === UPDATE: POST BEARBEITEN (PUT-Request) ===

function starteEdit(postId) {
    console.log(`Bearbeite Post ${postId}...`);
    
    // Edit-Formular anzeigen
    const editFormular = document.getElementById(`edit-${postId}`);
    editFormular.classList.remove('versteckt');
}

function abbrechenEdit(postId) {
    console.log(`Abbrechen für Post ${postId}`);
    
    // Edit-Formular verstecken
    const editFormular = document.getElementById(`edit-${postId}`);
    editFormular.classList.add('versteckt');
}

function speichereEdit(postId) {
    console.log(`Speichere Post ${postId}...`);
    
    // Neue Werte holen
    const neuerTitel = document.getElementById(`edit-titel-${postId}`).value;
    const neuerBody = document.getElementById(`edit-body-${postId}`).value;
    
    // PUT-Request an API senden
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`, {
        method: 'PUT',  // HTTP-Methode für Update
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            id: postId,
            title: neuerTitel,
            body: neuerBody,
            userId: 1
        })
    })
    .then(response => response.json())
    .then(aktualisierterPost => {
        console.log("✅ Post aktualisiert:", aktualisierterPost);
        
        // UI aktualisieren
        const karte = document.getElementById(`post-${postId}`);
        karte.querySelector('h4').textContent = neuerTitel;
        karte.querySelector('.post-body-verwaltung').textContent = neuerBody;
        
        // Edit-Formular verstecken
        const editFormular = document.getElementById(`edit-${postId}`);
        editFormular.classList.add('versteckt');
        
        // Erfolgs-Animation
        karte.style.background = '#d4edda';
        setTimeout(() => {
            karte.style.background = 'white';
        }, 1000);
    })
    .catch(error => {
        console.error("❌ Fehler:", error);
        alert('Fehler beim Speichern der Änderungen.');
    });
}
```

---

### Teil 6: DELETE – Post löschen (20 Min)

**Aufgabe:** Implementiere die Lösch-Funktion für Posts.

**Anforderungen:**
1. Frage mit `confirm()` nach Bestätigung
2. Sende DELETE-Request an `/posts/{id}`
3. Entferne Post mit Animation aus der UI
4. Wenn Container leer: Zeige "Keine Posts" Nachricht

**Grundgerüst:**

```javascript
// === DELETE: POST LÖSCHEN (DELETE-Request) ===

function loeschePost(postId) {
    console.log(`Lösche Post ${postId}...`);

    // TODO: Frage mit confirm() nach Bestätigung
    const bestaetigung = confirm('...');

    if (!bestaetigung) {
        return;
    }

    // TODO: Sende DELETE-Request
    fetch(`.../${postId}`, {  // URL: https://jsonplaceholder.typicode.com/posts/{id}
        method: '...'  // DELETE
    })
    .then(response => {
        if (response.ok) {
            console.log("✅ Post gelöscht");

            // TODO: Hole die Karte aus dem DOM
            const karte = document.getElementById(`post-${postId}`);

            // TODO: Fade-Out Animation (opacity, transform, transition)
            karte.style.opacity = '...';
            karte.style.transform = '...';
            karte.style.transition = '...';

            // TODO: Nach Animation: Karte entfernen (setTimeout + karte.remove())
            setTimeout(() => {
                // ... entfernen
                // ... prüfen ob Container leer
            }, 300);
        } else {
            throw new Error('Fehler beim Löschen');
        }
    })
    .catch(error => {
        // TODO: Fehlerbehandlung
    });
}
```

**Wo nachschlagen?**
- [MDN: confirm()](https://developer.mozilla.org/de/docs/Web/API/Window/confirm)
- [MDN: Element.remove()](https://developer.mozilla.org/de/docs/Web/API/Element/remove)
- [MDN: CSS Transitions](https://developer.mozilla.org/de/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

---

## Erfolgskriterien

- [ ] HTML-Formular für neuen Post erstellt
- [ ] CSS für CRUD-Interface hinzugefügt
- [ ] `api-crud.js` erstellt und eingebunden
- [ ] POST-Request funktioniert (neuer Post erstellen)
- [ ] Formular zeigt Erfolgs-Feedback
- [ ] GET-Request funktioniert (Posts laden)
- [ ] Posts werden mit Edit- und Delete-Buttons angezeigt
- [ ] Edit-Formular wird ein-/ausgeblendet
- [ ] PUT-Request funktioniert (Post aktualisieren)
- [ ] UI aktualisiert sich nach Edit
- [ ] DELETE-Request funktioniert (Post löschen)
- [ ] Bestätigungs-Dialog vor Löschen
- [ ] Post verschwindet mit Animation aus UI
- [ ] Fehlerbehandlung für alle Requests vorhanden

---

## Tipps

**POST-Request Struktur:**
```javascript
fetch(url, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(daten)
})
```

**PUT vs. PATCH:**
- PUT: Ersetzt den gesamten Eintrag
- PATCH: Aktualisiert nur einzelne Felder
- JSONPlaceholder unterstützt beide

**DELETE-Request:**
```javascript
fetch(url, { method: 'DELETE' })
    .then(response => {
        if (response.ok) {
            console.log("Gelöscht!");
        }
    });
```

**Häufige Fehler:**

1. **Vergessen, Content-Type zu setzen**
   ```javascript
   headers: { 'Content-Type': 'application/json' }  // Wichtig!
   ```

2. **Vergessen, JSON.stringify() zu nutzen**
   ```javascript
   body: JSON.stringify(objekt)  // JavaScript → JSON
   ```

3. **Event.preventDefault() vergessen**
   ```javascript
   form.addEventListener('submit', function(event) {
       event.preventDefault();  // Verhindert Reload
   });
   ```

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen POST und PUT?**  
   *Tipp: Wann erstellst du etwas Neues, wann aktualisierst du?*

2. **Warum nutzen wir JSON.stringify() bei POST/PUT?**  
   *Was ist der Unterschied zwischen JavaScript-Objekt und JSON-String?*

3. **Was passiert bei DELETE mit den Daten in der Datenbank?**  
   *Sind sie wirklich gelöscht oder nur als gelöscht markiert?*

4. **Wie könntest du Validierung vor dem Senden einbauen?**  
   *Tipp: Prüfe Länge, Format, leere Felder*

5. **Was ist REST? Warum heisst es RESTful API?**  
   *Recherchiere: Representational State Transfer*

---

## Weiterführende Links

**HTTP-Methoden:**
- [MDN: HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [REST API Tutorial](https://restfulapi.net/)

**fetch() mit POST/PUT/DELETE:**
- [MDN: Using Fetch with POST](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#supplying_request_options)
- [JavaScript.info: Fetch](https://javascript.info/fetch)

**JSON und JavaScript:**
- [MDN: JSON.stringify()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN: JSON.parse()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

**RESTful APIs:**
- [What is REST?](https://www.redhat.com/en/topics/api/what-is-a-rest-api)
- [RESTful Web Services Tutorial](https://www.tutorialspoint.com/restful/index.htm)

---

**⏱️ Geschätzte Zeit:** 85 Minuten  
**📦 Nächster Schritt:** Optionaler Auftrag 4 – Fortgeschrittene API-Konzepte (async/await, Error Handling)
