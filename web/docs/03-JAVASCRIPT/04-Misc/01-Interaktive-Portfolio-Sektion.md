# Auftrag 1: Interaktive Portfolio-Sektion mit Event Handling

## Ziel

Du lernst, wie deine Website auf Benutzeraktionen reagiert. Mit Event Handling fängst du Klicks, Tastatureingaben und Formulareingaben ab und verarbeitest sie mit JavaScript.

## Beschreibung

**Events** sind Benutzeraktionen wie Klicks, Tastatureingaben oder Formulareingaben. Mit **Event Listeners** reagiert dein JavaScript auf diese Aktionen. Das macht Websites interaktiv. In diesem Auftrag fügst du interaktive Elemente zu deiner Portfolio-Seite hinzu: einen Click-Counter, eine Live-Suche durch deine Skills und ein Kontaktformular mit Validierung.

---

### Teil 1: Click-Events – Interaktiver Button (15 Min)

Füge eine neue Sektion in deine `index.html` ein:

```html
<section id="interaktive-demo">
    <h2>Interaktive Elemente</h2>
    
    <!-- Click Counter -->
    <div class="demo-box">
        <h3>Click Counter</h3>
        <p>Wie oft hast du schon geklickt?</p>
        <button id="click-button" class="btn-primary">
            Klick mich!
        </button>
        <p>Anzahl Klicks: <strong id="click-counter">0</strong></p>
    </div>
</section>
```

Erstelle eine neue Datei **`events.js`** mit folgendem Code:

```javascript
// =====================================================
// EVENT HANDLING
// =====================================================
// Reagiere auf Benutzeraktionen mit Event Listeners

console.log("Event-Script geladen!");

// === CLICK-EVENT ===

// Counter-Variable
let clickCount = 0;

// Elemente holen
let clickButton = document.getElementById("click-button");
let clickCounter = document.getElementById("click-counter");

// Event Listener registrieren
clickButton.addEventListener("click", function(event) {
    // Counter erhöhen
    clickCount++;
    
    // Anzeige aktualisieren
    clickCounter.textContent = clickCount;
    
    // In Konsole ausgeben
    console.log(`Button geklickt! Anzahl: ${clickCount}`);
    
    // Event-Objekt inspizieren
    console.log("Event-Typ:", event.type);
    console.log("Geklicktes Element:", event.target);
    
    // Button-Text ändern nach 5 Klicks
    if (clickCount === 5) {
        clickButton.textContent = "Wow, 5 Klicks!";
        clickButton.style.backgroundColor = "#228B22";
    }
    
    // Button-Text ändern nach 10 Klicks
    if (clickCount === 10) {
        clickButton.textContent = "Du liebst Klicks!";
        clickButton.style.backgroundColor = "#FF6347";
    }
});

console.log("Click-Event Listener registriert");
```

**Wichtig:** Vergiss nicht, die neue JavaScript-Datei im HTML einzubinden:

```html
<!-- Vor </body> einfügen -->
<script src="events.js"></script>
</body>
</html>
```

---

### Teil 2: Input-Events – Live-Suche (20 Min)

Erweitere die Sektion mit einer Live-Suche für Skills:

```html
<!-- In die gleiche Sektion einfügen -->
<div class="demo-box">
    <h3>Skill-Suche</h3>
    <p>Suche nach Skills (z.B. HTML, CSS, JavaScript):</p>
    <input 
        type="text" 
        id="skill-search" 
        placeholder="Skill eingeben..."
        class="form-input"
    >
    <p id="search-result">Gib einen Suchbegriff ein...</p>
</div>
```

Füge CSS in `styles.css` hinzu:

```css
/* === INTERAKTIVE ELEMENTE === */

.demo-box {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    margin-bottom: 20px;
    border: 2px solid #e9ecef;
}

.demo-box h3 {
    color: #0066cc;
    margin-top: 0;
}

.form-input {
    width: 100%;
    padding: 12px;
    border: 2px solid #ced4da;
    border-radius: 6px;
    font-size: 1em;
    margin: 10px 0;
    transition: border-color 0.3s;
}

.form-input:focus {
    outline: none;
    border-color: #0066cc;
}

.btn-primary {
    background-color: #0066cc;
    color: white;
    border: none;
    padding: 12px 24px;
    font-size: 1em;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn-primary:hover {
    background-color: #0052a3;
}

.btn-primary:active {
    transform: scale(0.98);
}

#search-result {
    margin-top: 15px;
    padding: 10px;
    background: white;
    border-radius: 6px;
    min-height: 30px;
}
```

Erweitere `events.js`:

```javascript
// === INPUT-EVENT: LIVE-SUCHE ===

// Skills-Datenbank
const mySkills = [
    "HTML",
    "CSS",
    "JavaScript",
    "Git",
    "Responsive Design",
    "Flexbox",
    "CSS Grid",
    "DOM Manipulation",
    "Event Handling",
    "Debugging"
];

// Elemente holen
let searchInput = document.getElementById("skill-search");
let searchResult = document.getElementById("search-result");

// Input-Event: Wird bei jeder Eingabe ausgelöst
searchInput.addEventListener("input", function(event) {
    // Aktuellen Wert des Eingabefeldes holen
    let suchbegriff = event.target.value.toLowerCase().trim();
    
    console.log("Suche nach:", suchbegriff);
    
    // Wenn Suchfeld leer ist
    if (suchbegriff === "") {
        searchResult.textContent = "Gib einen Suchbegriff ein...";
        searchResult.style.color = "#6c757d";
        return;
    }
    
    // Skills filtern
    let gefundeneSkills = mySkills.filter(function(skill) {
        return skill.toLowerCase().includes(suchbegriff);
    });
    
    // Ergebnis anzeigen
    if (gefundeneSkills.length > 0) {
        searchResult.textContent = "Gefunden: " + gefundeneSkills.join(", ");
        searchResult.style.color = "#28a745";
    } else {
        searchResult.textContent = "Keine Skills gefunden :(";
        searchResult.style.color = "#dc3545";
    }
    
    console.log("Gefundene Skills:", gefundeneSkills);
});

console.log("Input-Event Listener registriert");
```

---

### Teil 3: Submit-Event – Kontaktformular mit Validierung (25 Min)

Füge ein Kontaktformular hinzu:

```html
<!-- In die gleiche Sektion einfügen -->
<div class="demo-box">
    <h3>Kontaktformular</h3>
    <form id="contact-form">
        <label for="name-input">Name:</label>
        <input 
            type="text" 
            id="name-input" 
            class="form-input"
            placeholder="Dein Name"
            required
        >
        
        <label for="email-input">E-Mail:</label>
        <input 
            type="email" 
            id="email-input" 
            class="form-input"
            placeholder="deine@email.ch"
            required
        >
        
        <label for="message-input">Nachricht:</label>
        <textarea 
            id="message-input" 
            class="form-input"
            placeholder="Deine Nachricht..."
            rows="4"
            required
        ></textarea>
        
        <button type="submit" class="btn-primary">
            Absenden
        </button>
    </form>
    
    <div id="form-feedback"></div>
</div>
```

Füge CSS für das Formular hinzu:

```css
/* === FORMULAR-STYLING === */

form {
    display: flex;
    flex-direction: column;
}

form label {
    font-weight: 600;
    margin-top: 10px;
    margin-bottom: 5px;
    color: #495057;
}

textarea.form-input {
    resize: vertical;
    font-family: inherit;
}

#form-feedback {
    margin-top: 15px;
    padding: 12px;
    border-radius: 6px;
    font-weight: 500;
    display: none;
}

#form-feedback.success {
    display: block;
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
}

#form-feedback.error {
    display: block;
    background: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
}
```

Erweitere `events.js`:

```javascript
// === SUBMIT-EVENT: FORMULAR-VALIDIERUNG ===

let contactForm = document.getElementById("contact-form");
let formFeedback = document.getElementById("form-feedback");

contactForm.addEventListener("submit", function(event) {
    // WICHTIG: Verhindert Standard-Aktion (Seite neu laden)
    event.preventDefault();
    
    console.log("Formular abgesendet (submit-Event)");
    
    // Werte aus Formularfeldern holen
    let name = document.getElementById("name-input").value.trim();
    let email = document.getElementById("email-input").value.trim();
    let message = document.getElementById("message-input").value.trim();
    
    console.log("Name:", name);
    console.log("E-Mail:", email);
    console.log("Nachricht:", message);
    
    // Validierung
    let fehler = [];
    
    // Name validieren (mindestens 2 Zeichen)
    if (name.length < 2) {
        fehler.push("Name muss mindestens 2 Zeichen lang sein");
    }
    
    // E-Mail validieren (einfache Prüfung)
    if (!email.includes("@") || !email.includes(".")) {
        fehler.push("Ungültige E-Mail-Adresse");
    }
    
    // Nachricht validieren (mindestens 10 Zeichen)
    if (message.length < 10) {
        fehler.push("Nachricht muss mindestens 10 Zeichen lang sein");
    }
    
    // Wenn Fehler vorhanden sind
    if (fehler.length > 0) {
        formFeedback.className = "error";
        formFeedback.textContent = "Fehler: " + fehler.join(", ");
        console.error("Validierungsfehler:", fehler);
        return; // Funktion beenden
    }
    
    // Erfolg!
    formFeedback.className = "success";
    formFeedback.textContent = `Danke, ${name}! Deine Nachricht wurde empfangen.`;
    
    console.log("✅ Formular erfolgreich validiert");
    
    // Formular zurücksetzen nach 3 Sekunden
    setTimeout(function() {
        contactForm.reset();
        formFeedback.style.display = "none";
    }, 3000);
});

console.log("Submit-Event Listener registriert");
```

---

## Erfolgskriterien

- [ ] Click-Counter funktioniert und zählt Klicks
- [ ] Button ändert Text und Farbe nach 5 und 10 Klicks
- [ ] Live-Suche filtert Skills in Echtzeit
- [ ] Leeres Suchfeld zeigt Standard-Text
- [ ] Keine gefundenen Skills zeigen Fehlermeldung
- [ ] Kontaktformular validiert alle Felder korrekt
- [ ] event.preventDefault() verhindert Seiten-Reload
- [ ] Fehler werden rot angezeigt
- [ ] Erfolg wird grün angezeigt
- [ ] Formular wird nach Erfolg zurückgesetzt
- [ ] Alle console.log-Ausgaben erscheinen in DevTools
- [ ] Keine JavaScript-Fehler in der Konsole

---

## Tipps

- **addEventListener():** Registriert Event Listener – Syntax: `element.addEventListener("eventTyp", funktion)`
- **event.preventDefault():** Verhindert Standard-Aktion (z.B. Formular-Submit, Link-Klick)
- **event.target:** Das Element, das das Event ausgelöst hat
- **.value:** Holt den Wert aus Eingabefeldern
- **.trim():** Entfernt Leerzeichen am Anfang und Ende eines Strings
- **Array.filter():** Erstellt neues Array mit gefilterten Elementen

**Häufige Fehler:**
- Event-Typ falsch geschrieben: `"click"` nicht `"Click"` oder `"onclick"`
- `event.preventDefault()` vergessen bei Submit-Event
- Event Listener vor DOM-Laden registriert (Script im `<head>`)
- `.value` vergessen bei Eingabefeldern

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `click` und `onclick`?**  
   *Tipp: onclick ist ein HTML-Attribut, click ist der Event-Typ für addEventListener. Was ist die moderne Best Practice?*

2. **Warum brauchen wir `event.preventDefault()` beim Submit-Event?**  
   *Was passiert, wenn du es weglässt? Teste es!*

3. **Das Event-Objekt enthält viele Informationen. Welche könnten nützlich sein?**  
   *Öffne die Konsole und gib `console.log(event)` in deinem Event Listener aus. Welche Properties siehst du?*

4. **Die Live-Suche reagiert bei jeder Eingabe. Könnte das bei vielen Daten problematisch sein?**  
   *Recherchiere: Was ist Debouncing und wann nutzt man es?*

5. **Wie könntest du die Validierung erweitern?**  
   *Ideen: Länge der Nachricht, spezielle Zeichen im Namen, internationale E-Mail-Formate*

---

## Weiterführende Links

**Event Handling Grundlagen:**
- [MDN: Introduction to Events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [MDN: addEventListener](https://developer.mozilla.org/de/docs/Web/API/EventTarget/addEventListener)
- [JavaScript.info: Introduction to Browser Events](https://javascript.info/introduction-browser-events)

**Event-Typen:**
- [MDN: Event Reference (alle Events)](https://developer.mozilla.org/en-US/docs/Web/Events)
- [W3Schools: DOM Events](https://www.w3schools.com/jsref/dom_obj_event.asp)

**Form-Validierung:**
- [MDN: Client-side Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [HTML5 Input-Types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types)

**Best Practices:**
- [Google: Event Handling Best Practices](https://web.dev/eventing-deepdive/)
- [Event Delegation Pattern](https://javascript.info/event-delegation)

---

**Geschätzte Zeit:** 60 Minuten  
**Nächster Schritt:** Auftrag 2 – Daten von APIs laden mit Fetch
