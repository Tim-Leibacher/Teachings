# Auftrag 2: Interaktives Profil mit Bearbeitung

## Ziel

Du erstellst ein interaktives Profil auf deiner Portfolio-Seite, das per JavaScript editiert werden kann. Dabei lernst du, wie Inhalte nicht nur angezeigt, sondern auch vom Benutzer verändert werden können.

## Beschreibung

Bis jetzt hast du gelernt, wie JavaScript Inhalte automatisch ändert. Jetzt machst du den nächsten Schritt: Der Benutzer soll selbst Inhalte bearbeiten können. Das ist die Grundlage für interaktive Formulare, Content-Management-Systeme und moderne Web-Apps.

In diesem Auftrag erstellst du eine Profil-Sektion mit editierbaren Feldern. JavaScript macht die Felder bearbeitbar und speichert Änderungen.

---

### Teil 1: HTML-Struktur für editierbares Profil (10 Min)

Füge in deiner `index.html` eine neue Sektion für dein Profil ein:

```html
<section id="mein-profil">
    <h2>Mein Profil</h2>
    <p>Klicke auf die Werte, um sie zu bearbeiten.</p>
    
    <div class="profil-container">
        <div class="profil-feld">
            <label>Name:</label>
            <span id="profil-name" class="editierbar">Max Mustermann</span>
        </div>
        
        <div class="profil-feld">
            <label>Beruf:</label>
            <span id="profil-beruf" class="editierbar">Informatiker/in EFZ</span>
        </div>
        
        <div class="profil-feld">
            <label>Wohnort:</label>
            <span id="profil-ort" class="editierbar">Zürich</span>
        </div>
        
        <div class="profil-feld">
            <label>Lehrjahr:</label>
            <span id="profil-lehrjahr" class="editierbar">1. Lehrjahr</span>
        </div>
        
        <div class="profil-feld">
            <label>Lieblings-Technologie:</label>
            <span id="profil-tech" class="editierbar">JavaScript</span>
        </div>
        
        <div class="profil-feld">
            <label>Ziel für 2025:</label>
            <span id="profil-ziel" class="editierbar">Eine eigene Web-App entwickeln</span>
        </div>
    </div>
    
    <div class="profil-aktionen">
        <button id="btn-profil-speichern">💾 Änderungen speichern</button>
        <button id="btn-profil-reset">🔄 Zurücksetzen</button>
    </div>
    
    <p id="speicher-status" class="status-nachricht"></p>
</section>
```

**Wichtig:**
- Jedes Feld hat eine eindeutige ID
- Die Klasse `editierbar` markiert editierbare Elemente
- Buttons für Speichern und Zurücksetzen

---

### Teil 2: CSS für das Profil (5 Min)

Füge in deiner `styles.css` folgende Styles hinzu:

```css
/* === PROFIL-SEKTION === */
#mein-profil {
    background: #f8f9fa;
    padding: 30px;
    border-radius: 8px;
    margin: 40px 0;
}

.profil-container {
    background: white;
    padding: 20px;
    border-radius: 6px;
    margin: 20px 0;
}

.profil-feld {
    display: flex;
    align-items: center;
    padding: 12px;
    border-bottom: 1px solid #e9ecef;
}

.profil-feld:last-child {
    border-bottom: none;
}

.profil-feld label {
    font-weight: 600;
    color: #495057;
    min-width: 200px;
}

.profil-feld span {
    flex: 1;
    padding: 8px 12px;
    color: #212529;
}

.editierbar {
    cursor: pointer;
    border: 2px solid transparent;
    border-radius: 4px;
    transition: all 0.2s ease;
}

.editierbar:hover {
    background: #e7f5ff;
    border-color: #0066cc;
}

.editierbar:focus {
    outline: none;
    background: #fff3cd;
    border-color: #ff6b35;
}

.profil-aktionen {
    display: flex;
    gap: 15px;
    margin-top: 20px;
}

.profil-aktionen button {
    padding: 12px 24px;
    font-size: 1em;
    font-weight: 600;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.2s ease;
}

#btn-profil-speichern {
    background: #0066cc;
    color: white;
}

#btn-profil-speichern:hover {
    background: #0052a3;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 102, 204, 0.3);
}

#btn-profil-reset {
    background: #6c757d;
    color: white;
}

#btn-profil-reset:hover {
    background: #5a6268;
}

.status-nachricht {
    margin-top: 15px;
    padding: 12px;
    border-radius: 4px;
    font-weight: 500;
    text-align: center;
    transition: all 0.3s ease;
}

.status-nachricht.erfolg {
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
}

.status-nachricht.warnung {
    background: #fff3cd;
    color: #856404;
    border: 1px solid #ffeeba;
}
```

---

### Teil 3: JavaScript für editierbare Felder (20 Min)

Erstelle eine neue Datei **`profil.js`** mit folgendem Inhalt:

```javascript
// =====================================================
// INTERAKTIVES PROFIL
// =====================================================

console.log("📝 Profil-Script geladen");

// === STANDARD-WERTE SPEICHERN ===
// Diese Werte dienen als "Original" zum Zurücksetzen

const standardWerte = {
    name: "Max Mustermann",
    beruf: "Informatiker/in EFZ",
    ort: "Zürich",
    lehrjahr: "1. Lehrjahr",
    tech: "JavaScript",
    ziel: "Eine eigene Web-App entwickeln"
};

// === ALLE EDITIERBAREN FELDER FINDEN ===

let editierbareFelder = document.querySelectorAll(".editierbar");

console.log(`✅ ${editierbareFelder.length} editierbare Felder gefunden`);

// === FELDER EDITIERBAR MACHEN ===

editierbareFelder.forEach(function(feld) {
    // contentEditable macht ein Element bearbeitbar
    feld.setAttribute("contenteditable", "true");
    
    // Enter-Taste soll NICHT einen Zeilenumbruch machen
    feld.addEventListener("keydown", function(event) {
        if (event.key === "Enter") {
            event.preventDefault(); // Enter blockieren
            feld.blur(); // Fokus entfernen = Bearbeitung beenden
        }
    });
    
    // Visuelles Feedback beim Fokus
    feld.addEventListener("focus", function() {
        console.log(`📝 Bearbeite: ${feld.id}`);
    });
});

// === SPEICHERN-BUTTON ===

let btnSpeichern = document.getElementById("btn-profil-speichern");
let statusNachricht = document.getElementById("speicher-status");

btnSpeichern.addEventListener("click", function() {
    console.log("💾 Speichere Profil...");
    
    // Alle Werte sammeln
    let profilDaten = {
        name: document.getElementById("profil-name").textContent,
        beruf: document.getElementById("profil-beruf").textContent,
        ort: document.getElementById("profil-ort").textContent,
        lehrjahr: document.getElementById("profil-lehrjahr").textContent,
        tech: document.getElementById("profil-tech").textContent,
        ziel: document.getElementById("profil-ziel").textContent
    };
    
    // In LocalStorage speichern (als JSON-String)
    localStorage.setItem("meinProfil", JSON.stringify(profilDaten));
    
    // Status-Nachricht anzeigen
    statusNachricht.textContent = "✅ Profil erfolgreich gespeichert!";
    statusNachricht.className = "status-nachricht erfolg";
    
    // Nach 3 Sekunden ausblenden
    setTimeout(function() {
        statusNachricht.textContent = "";
        statusNachricht.className = "status-nachricht";
    }, 3000);
    
    console.log("✅ Profil gespeichert:", profilDaten);
});

// === ZURÜCKSETZEN-BUTTON ===

let btnReset = document.getElementById("btn-profil-reset");

btnReset.addEventListener("click", function() {
    console.log("🔄 Setze Profil zurück...");
    
    // Warnung anzeigen
    let bestaetigung = confirm("Möchtest du wirklich alle Änderungen verwerfen?");
    
    if (bestaetigung) {
        // Alle Felder auf Standard zurücksetzen
        document.getElementById("profil-name").textContent = standardWerte.name;
        document.getElementById("profil-beruf").textContent = standardWerte.beruf;
        document.getElementById("profil-ort").textContent = standardWerte.ort;
        document.getElementById("profil-lehrjahr").textContent = standardWerte.lehrjahr;
        document.getElementById("profil-tech").textContent = standardWerte.tech;
        document.getElementById("profil-ziel").textContent = standardWerte.ziel;
        
        // Aus LocalStorage löschen
        localStorage.removeItem("meinProfil");
        
        // Status-Nachricht
        statusNachricht.textContent = "🔄 Profil auf Standard zurückgesetzt";
        statusNachricht.className = "status-nachricht warnung";
        
        setTimeout(function() {
            statusNachricht.textContent = "";
            statusNachricht.className = "status-nachricht";
        }, 3000);
        
        console.log("✅ Profil zurückgesetzt");
    }
});

// === GESPEICHERTE DATEN LADEN (beim Seitenstart) ===

function ladeGespeichertesDaten() {
    console.log("📂 Prüfe auf gespeicherte Daten...");
    
    let gespeichert = localStorage.getItem("meinProfil");
    
    if (gespeichert) {
        // JSON-String zurück in Objekt umwandeln
        let profilDaten = JSON.parse(gespeichert);
        
        // Felder mit gespeicherten Daten füllen
        document.getElementById("profil-name").textContent = profilDaten.name;
        document.getElementById("profil-beruf").textContent = profilDaten.beruf;
        document.getElementById("profil-ort").textContent = profilDaten.ort;
        document.getElementById("profil-lehrjahr").textContent = profilDaten.lehrjahr;
        document.getElementById("profil-tech").textContent = profilDaten.tech;
        document.getElementById("profil-ziel").textContent = profilDaten.ziel;
        
        console.log("✅ Gespeicherte Daten geladen:", profilDaten);
        
        // Info-Nachricht anzeigen
        statusNachricht.textContent = "ℹ️ Gespeicherte Daten wurden geladen";
        statusNachricht.className = "status-nachricht erfolg";
        
        setTimeout(function() {
            statusNachricht.textContent = "";
            statusNachricht.className = "status-nachricht";
        }, 2000);
    } else {
        console.log("ℹ️ Keine gespeicherten Daten gefunden");
    }
}

// Beim Laden der Seite ausführen
ladeGespeichertesDaten();

console.log("✅ Profil-Funktionen initialisiert");
```

**Binde die Datei ein:**

```html
<script src="dom.js"></script>
<script src="profil.js"></script>
```

---

### Teil 4: Erweiterte Funktionen (15 Min)

Füge weitere Funktionen hinzu, um das Profil noch interaktiver zu machen:

```javascript
// === ZEICHEN-ZÄHLER FÜR ZIEL-FELD ===

let zielFeld = document.getElementById("profil-ziel");
let zeichenZaehler = document.createElement("p");
zeichenZaehler.id = "zeichen-zaehler";
zeichenZaehler.style.color = "#6c757d";
zeichenZaehler.style.fontSize = "0.9em";
zeichenZaehler.style.marginTop = "5px";

// Nach dem Ziel-Feld einfügen
zielFeld.parentElement.appendChild(zeichenZaehler);

function aktualisiereZeichenZaehler() {
    let text = zielFeld.textContent;
    let laenge = text.length;
    
    zeichenZaehler.textContent = `${laenge} Zeichen`;
    
    // Farbe ändern je nach Länge
    if (laenge > 100) {
        zeichenZaehler.style.color = "#dc3545"; // Rot
        zeichenZaehler.textContent += " (zu lang!)";
    } else if (laenge > 80) {
        zeichenZaehler.style.color = "#ff6b35"; // Orange
    } else {
        zeichenZaehler.style.color = "#6c757d"; // Grau
    }
}

// Bei jeder Eingabe aktualisieren
zielFeld.addEventListener("input", aktualisiereZeichenZaehler);

// Initial anzeigen
aktualisiereZeichenZaehler();

// === VALIDIERUNG BEI SPEICHERN ===

function validiereProfilDaten(daten) {
    let fehler = [];
    
    // Name darf nicht leer sein
    if (daten.name.trim() === "") {
        fehler.push("Name darf nicht leer sein");
    }
    
    // Lehrjahr muss "1.", "2.", "3." oder "4." enthalten
    if (!/[1-4]\./.test(daten.lehrjahr)) {
        fehler.push("Lehrjahr muss 1., 2., 3. oder 4. enthalten");
    }
    
    // Ziel sollte nicht zu lang sein
    if (daten.ziel.length > 100) {
        fehler.push("Ziel ist zu lang (max. 100 Zeichen)");
    }
    
    return fehler;
}

// Speichern-Button mit Validierung erweitern
btnSpeichern.addEventListener("click", function(event) {
    let profilDaten = {
        name: document.getElementById("profil-name").textContent,
        beruf: document.getElementById("profil-beruf").textContent,
        ort: document.getElementById("profil-ort").textContent,
        lehrjahr: document.getElementById("profil-lehrjahr").textContent,
        tech: document.getElementById("profil-tech").textContent,
        ziel: document.getElementById("profil-ziel").textContent
    };
    
    // Validierung
    let fehler = validiereProfilDaten(profilDaten);
    
    if (fehler.length > 0) {
        // Fehler anzeigen
        statusNachricht.textContent = "❌ " + fehler.join(", ");
        statusNachricht.className = "status-nachricht warnung";
        
        console.error("❌ Validierungsfehler:", fehler);
        
        // Nicht speichern!
        event.preventDefault();
        return;
    }
});

// === EXPORT-FUNKTION (Bonus) ===

function exportiereProfil() {
    let profilDaten = {
        name: document.getElementById("profil-name").textContent,
        beruf: document.getElementById("profil-beruf").textContent,
        ort: document.getElementById("profil-ort").textContent,
        lehrjahr: document.getElementById("profil-lehrjahr").textContent,
        tech: document.getElementById("profil-tech").textContent,
        ziel: document.getElementById("profil-ziel").textContent
    };
    
    // Als JSON-String formatieren (schön formatiert)
    let json = JSON.stringify(profilDaten, null, 2);
    
    // In Konsole ausgeben
    console.log("📤 Profil-Export:");
    console.log(json);
    
    // Als Download anbieten
    let blob = new Blob([json], { type: "application/json" });
    let url = URL.createObjectURL(blob);
    let link = document.createElement("a");
    link.href = url;
    link.download = "mein-profil.json";
    link.click();
    
    console.log("✅ Profil exportiert");
}

// Export-Button hinzufügen (Optional)
let btnExport = document.createElement("button");
btnExport.textContent = "📤 Profil exportieren";
btnExport.style.cssText = "padding: 12px 24px; background: #28a745; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: 600;";
btnExport.addEventListener("click", exportiereProfil);

document.querySelector(".profil-aktionen").appendChild(btnExport);
```

---

## Erfolgskriterien

- [ ] Profil-Sektion in HTML eingefügt mit allen Feldern
- [ ] CSS für editierbare Felder und Buttons eingefügt
- [ ] `profil.js` erstellt und eingebunden
- [ ] Felder sind editierbar (mit contentEditable)
- [ ] Speichern-Button speichert Daten in LocalStorage
- [ ] Zurücksetzen-Button stellt Standard wieder her
- [ ] Gespeicherte Daten werden beim Neuladen automatisch geladen
- [ ] Status-Nachrichten werden angezeigt
- [ ] Zeichen-Zähler funktioniert beim Ziel-Feld
- [ ] Validierung verhindert fehlerhafte Eingaben

---

## Tipps

- **contentEditable:** Das Attribut macht jedes HTML-Element bearbeitbar, nicht nur `<input>`
- **JSON.stringify() / JSON.parse():** Wandelt Objekte in Strings und zurück für LocalStorage
- **blur():** Entfernt den Fokus von einem Element (beendet Bearbeitung)
- **confirm():** Zeigt einen nativen Browser-Dialog für Bestätigungen
- **preventDefault():** Verhindert Standard-Verhalten (z.B. Enter = Zeilenumbruch)

**Häufige Fehler:**
- Vergessen, contentEditable zu setzen → Felder nicht editierbar
- JSON.parse() auf nicht-JSON-String → Fehler in Konsole
- LocalStorage-Key falsch geschrieben → Daten werden nicht gefunden

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `<input>` und `contentEditable`?**  
   *Wann würdest du welche Methode nutzen? Was sind Vor- und Nachteile?*

2. **Warum muss man Objekte mit `JSON.stringify()` umwandeln, bevor man sie in LocalStorage speichert?**  
   *Was passiert, wenn du versuchst, ein Objekt direkt zu speichern?*

3. **Experimentiere: Was passiert, wenn du `localStorage.setItem()` mit einem sehr langen String aufrufst?**  
   *Gibt es ein Limit? Probiere es aus!*

4. **Die Validierung passiert beim Speichern. Könnte man sie auch direkt beim Tippen machen?**  
   *Wie würdest du das implementieren? Welche Event-Listener brauchst du?*

5. **Bonus-Challenge: Wie könnte man ein Profil-Bild hinzufügen?**  
   *Tipp: FileReader API und base64-Encoding. Recherchiere dazu!*

---

## Weiterführende Links

**contentEditable:**
- [MDN: contentEditable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contenteditable)
- [CSS-Tricks: contentEditable](https://css-tricks.com/almanac/properties/c/contenteditable/)

**LocalStorage & JSON:**
- [MDN: JSON](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JavaScript.info: LocalStorage](https://javascript.info/localstorage)

**Validierung:**
- [MDN: Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [Regular Expressions (Regex)](https://regexr.com/)

**Events:**
- [MDN: Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)
- [JavaScript.info: Introduction to Events](https://javascript.info/introduction-browser-events)

---

**⏱️ Geschätzte Zeit:** 50 Minuten  
**📦 Nächster Schritt:** Auftrag 5 – Dynamische Projekt-Galerie mit Filter-Funktion
