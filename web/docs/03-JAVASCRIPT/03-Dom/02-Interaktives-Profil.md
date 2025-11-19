# Auftrag 2: Interaktives Profil mit Bearbeitung

## Ziel

Du erstellst ein interaktives Profil auf deiner Portfolio-Seite, das per JavaScript editiert werden kann. Dabei lernst du, wie Inhalte nicht nur angezeigt, sondern auch vom Benutzer verändert werden können.

## Beschreibung

Bis jetzt hast du gelernt, wie JavaScript Inhalte automatisch ändert. Jetzt machst du den nächsten Schritt: Der Benutzer soll selbst Inhalte bearbeiten können. Das ist die Grundlage für interaktive Formulare, Content-Management-Systeme und moderne Web-Apps.

In diesem Auftrag erstellst du eine Profil-Sektion mit editierbaren Feldern. JavaScript macht die Felder bearbeitbar und speichert Änderungen.

---

## Teil 1: HTML-Struktur für editierbares Profil (10 Min)

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

## Teil 2: CSS für das Profil (10 Min)

**Deine Aufgabe:**
Erstelle oder erweitere deine `styles.css` mit Styles für:
1. Die Profil-Sektion (`#mein-profil`)
2. Den Profil-Container (`.profil-container`)
3. Die einzelnen Felder (`.profil-feld`)
4. Editierbare Elemente (`.editierbar`) mit Hover- und Focus-States
5. Die Buttons (`.profil-aktionen button`)
6. Status-Nachrichten (`.status-nachricht`)

**Gestaltungshinweise:**
- Editierbare Felder sollten beim Hover visuell hervorgehoben werden
- Focus-State sollte sich deutlich abheben
- Buttons sollten ansprechend aussehen
- Status-Nachrichten brauchen Klassen für Erfolg und Warnung

**Wo nachschlagen:**
- [MDN: CSS Selectors](https://developer.mozilla.org/de/docs/Web/CSS/CSS_selectors)
- [MDN: :hover](https://developer.mozilla.org/de/docs/Web/CSS/:hover)
- [MDN: :focus](https://developer.mozilla.org/de/docs/Web/CSS/:focus)
- [CSS-Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

<details>
<summary>💡 CSS-Beispiel anzeigen (erst selbst probieren!)</summary>

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

.profil-feld label {
    font-weight: 600;
    color: #495057;
    min-width: 200px;
}

.editierbar {
    cursor: pointer;
    border: 2px solid transparent;
    border-radius: 4px;
    padding: 8px 12px;
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
}

#btn-profil-reset {
    background: #6c757d;
    color: white;
}

.status-nachricht {
    margin-top: 15px;
    padding: 12px;
    border-radius: 4px;
    font-weight: 500;
    text-align: center;
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
</details>

---

## Teil 3: JavaScript für editierbare Felder (25 Min)

Erstelle eine neue Datei **`profil.js`**.

### Aufgabe 3.1: Standard-Werte definieren

**Deine Aufgabe:**
Erstelle ein Objekt `standardWerte` mit allen Profil-Werten als Backup zum Zurücksetzen.

**Wo nachschlagen:**
- [MDN: Objects](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [JavaScript.info: Objects](https://javascript.info/object)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
console.log("📝 Profil-Script geladen");

const standardWerte = {
    name: "Max Mustermann",
    beruf: "Informatiker/in EFZ",
    ort: "Zürich",
    lehrjahr: "1. Lehrjahr",
    tech: "JavaScript",
    ziel: "Eine eigene Web-App entwickeln"
};
```
</details>

### Aufgabe 3.2: Felder editierbar machen

**Deine Aufgabe:**
1. Finde alle Elemente mit der Klasse `.editierbar`
2. Mache sie mit dem Attribut `contenteditable="true"` editierbar
3. Blockiere die Enter-Taste (soll keinen Zeilenumbruch einfügen)
4. Gib in der Konsole aus, welches Feld gerade bearbeitet wird

**Wo nachschlagen:**
- [MDN: contenteditable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contenteditable)
- [MDN: setAttribute](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)
- [MDN: addEventListener](https://developer.mozilla.org/de/docs/Web/API/EventTarget/addEventListener)
- [MDN: KeyboardEvent](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent)
- [MDN: blur()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/blur)

**Hinweise:**
- `querySelectorAll()` findet alle Elemente mit einer Klasse
- `forEach()` iteriert über alle gefundenen Elemente
- `event.key === "Enter"` prüft ob Enter gedrückt wurde
- `event.preventDefault()` verhindert Standard-Verhalten
- `.blur()` entfernt den Fokus (beendet Bearbeitung)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
let editierbareFelder = document.querySelectorAll(".editierbar");

console.log(`✅ ${editierbareFelder.length} editierbare Felder gefunden`);

editierbareFelder.forEach(function(feld) {
    // contentEditable macht ein Element bearbeitbar
    feld.setAttribute("contenteditable", "true");
    
    // Enter-Taste soll NICHT einen Zeilenumbruch machen
    feld.addEventListener("keydown", function(event) {
        if (event.key === "Enter") {
            event.preventDefault();
            feld.blur(); // Fokus entfernen = Bearbeitung beenden
        }
    });
    
    // Visuelles Feedback beim Fokus
    feld.addEventListener("focus", function() {
        console.log(`📝 Bearbeite: ${feld.id}`);
    });
});
```
</details>

### Aufgabe 3.3: Speichern-Funktion

**Deine Aufgabe:**
Implementiere den Speichern-Button:
1. Sammle alle Werte aus den editierbaren Feldern in ein Objekt
2. Speichere das Objekt als JSON-String in LocalStorage
3. Zeige eine Erfolgs-Nachricht an (grüner Hintergrund)
4. Lass die Nachricht nach 3 Sekunden verschwinden

**Wo nachschlagen:**
- [MDN: JSON.stringify](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN: localStorage.setItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/setItem)
- [MDN: setTimeout](https://developer.mozilla.org/de/docs/Web/API/setTimeout)
- [MDN: Element.className](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)

**Hinweise:**
- LocalStorage kann nur Strings speichern → nutze `JSON.stringify()`
- Nutze `setTimeout()` um die Nachricht nach einer Verzögerung zu löschen

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
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
    
    console.log("✅ Profil gespeichert:", profilDaten);
    
    // Nachricht nach 3 Sekunden ausblenden
    setTimeout(function() {
        statusNachricht.textContent = "";
        statusNachricht.className = "status-nachricht";
    }, 3000);
});
```
</details>

### Aufgabe 3.4: Zurücksetzen-Funktion

**Deine Aufgabe:**
Implementiere den Zurücksetzen-Button:
1. Zeige einen Bestätigungs-Dialog
2. Wenn bestätigt: Setze alle Felder auf die Standard-Werte zurück
3. Lösche die gespeicherten Daten aus LocalStorage
4. Zeige eine Info-Nachricht an

**Wo nachschlagen:**
- [MDN: Window.confirm](https://developer.mozilla.org/en-US/docs/Web/API/Window/confirm)
- [MDN: localStorage.removeItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/removeItem)

**Hinweise:**
- `confirm()` zeigt einen Dialog mit Ja/Nein
- Greife auf die Standard-Werte im `standardWerte` Objekt zu

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
let btnReset = document.getElementById("btn-profil-reset");

btnReset.addEventListener("click", function() {
    let bestaetigung = confirm("Möchtest du wirklich alle Änderungen zurücksetzen?");
    
    if (bestaetigung) {
        console.log("🔄 Setze Profil zurück...");
        
        // Alle Felder auf Standard-Werte setzen
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
```
</details>

### Aufgabe 3.5: Gespeicherte Daten laden

**Deine Aufgabe:**
Erstelle eine Funktion, die beim Laden der Seite prüft, ob gespeicherte Daten existieren und diese lädt.

**Wo nachschlagen:**
- [MDN: localStorage.getItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/getItem)
- [MDN: JSON.parse](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

**Hinweise:**
- `getItem()` gibt `null` zurück wenn nichts gespeichert ist
- `JSON.parse()` wandelt JSON-String zurück in Objekt

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
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
```
</details>

**Binde die Datei ein:**

```html
<script src="dom.js"></script>
<script src="profil.js"></script>
```

---

## Teil 4: Erweiterte Funktionen (Optional, 25 Min)

### Aufgabe 4.1: Zeichen-Zähler für Ziel-Feld

**Deine Aufgabe:**
Füge einen Zeichen-Zähler unter dem Ziel-Feld hinzu, der:
- Die aktuelle Anzahl Zeichen anzeigt
- Bei >80 Zeichen orange wird
- Bei >100 Zeichen rot wird und "zu lang!" anzeigt

**Wo nachschlagen:**
- [MDN: String.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length)
- [MDN: input event](https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event)
- [MDN: createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

**Hinweise:**
- Erstelle ein neues `<p>`-Element mit JavaScript
- Füge es mit `.appendChild()` ein
- Höre auf das `input`-Event für Live-Updates

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
let zielFeld = document.getElementById("profil-ziel");
let zeichenZaehler = document.createElement("p");
zeichenZaehler.style.color = "#6c757d";
zeichenZaehler.style.fontSize = "0.9em";
zeichenZaehler.style.marginTop = "5px";

zielFeld.parentElement.appendChild(zeichenZaehler);

function aktualisiereZeichenZaehler() {
    let text = zielFeld.textContent;
    let laenge = text.length;
    
    zeichenZaehler.textContent = `${laenge} Zeichen`;
    
    if (laenge > 100) {
        zeichenZaehler.style.color = "#dc3545";
        zeichenZaehler.textContent += " (zu lang!)";
    } else if (laenge > 80) {
        zeichenZaehler.style.color = "#ff6b35";
    } else {
        zeichenZaehler.style.color = "#6c757d";
    }
}

zielFeld.addEventListener("input", aktualisiereZeichenZaehler);
aktualisiereZeichenZaehler(); // Initial anzeigen
```
</details>

### Aufgabe 4.2: Validierung

**Deine Aufgabe:**
Erstelle eine Validierungs-Funktion, die vor dem Speichern prüft:
- Name darf nicht leer sein
- Lehrjahr muss "1.", "2.", "3." oder "4." enthalten
- Ziel darf max. 100 Zeichen lang sein

**Wo nachschlagen:**
- [MDN: String.trim()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim)
- [MDN: Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions)
- [MDN: RegExp.test()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)

**Hinweise:**
- Nutze `.trim()` um Leerzeichen zu entfernen
- Regex `/[1-4]\./` prüft auf 1. bis 4.
- Sammle Fehler in einem Array

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function validiereProfilDaten(daten) {
    let fehler = [];
    
    if (daten.name.trim() === "") {
        fehler.push("Name darf nicht leer sein");
    }
    
    if (!/[1-4]\./.test(daten.lehrjahr)) {
        fehler.push("Lehrjahr muss 1., 2., 3. oder 4. enthalten");
    }
    
    if (daten.ziel.length > 100) {
        fehler.push("Ziel ist zu lang (max. 100 Zeichen)");
    }
    
    return fehler;
}

// Im Speichern-Button einbauen:
btnSpeichern.addEventListener("click", function() {
    let profilDaten = {
        // ... Daten sammeln
    };
    
    let fehler = validiereProfilDaten(profilDaten);
    
    if (fehler.length > 0) {
        statusNachricht.textContent = "❌ " + fehler.join(", ");
        statusNachricht.className = "status-nachricht warnung";
        console.error("❌ Validierungsfehler:", fehler);
        return; // Nicht speichern!
    }
    
    // ... Normal speichern
});
```
</details>

### Aufgabe 4.3: Export-Funktion (Bonus)

**Deine Aufgabe:**
Füge einen Button hinzu, der das Profil als JSON-Datei exportiert.

**Wo nachschlagen:**
- [MDN: Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)
- [MDN: URL.createObjectURL](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL_static)
- [MDN: HTMLAnchorElement.download](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAnchorElement/download)

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function exportiereProfil() {
    let profilDaten = {
        name: document.getElementById("profil-name").textContent,
        beruf: document.getElementById("profil-beruf").textContent,
        ort: document.getElementById("profil-ort").textContent,
        lehrjahr: document.getElementById("profil-lehrjahr").textContent,
        tech: document.getElementById("profil-tech").textContent,
        ziel: document.getElementById("profil-ziel").textContent
    };
    
    let json = JSON.stringify(profilDaten, null, 2);
    let blob = new Blob([json], { type: "application/json" });
    let url = URL.createObjectURL(blob);
    let link = document.createElement("a");
    link.href = url;
    link.download = "mein-profil.json";
    link.click();
    
    console.log("✅ Profil exportiert");
}

let btnExport = document.createElement("button");
btnExport.textContent = "📤 Profil exportieren";
btnExport.style.cssText = "padding: 12px 24px; background: #28a745; color: white; border: none; border-radius: 6px; cursor: pointer;";
btnExport.addEventListener("click", exportiereProfil);
document.querySelector(".profil-aktionen").appendChild(btnExport);
```
</details>

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
- [ ] Zeichen-Zähler funktioniert (Optional)
- [ ] Validierung verhindert fehlerhafte Eingaben (Optional)

---

## Tipps & Troubleshooting

### Häufige Fehler:
- **Felder nicht editierbar?** → Prüfe ob `contenteditable="true"` gesetzt ist
- **LocalStorage funktioniert nicht?** → Prüfe ob der Key korrekt ist
- **JSON.parse() Fehler?** → Prüfe ob der gespeicherte String gültiges JSON ist
- **Daten nicht geladen?** → Prüfe ob `ladeGespeichertesDaten()` aufgerufen wird

### DevTools nutzen:
- **Application → Local Storage:** Zeigt gespeicherte Daten an
- **Console:** Sieh dir die Log-Ausgaben an
- **Elements:** Prüfe ob `contenteditable="true"` gesetzt ist

### Wichtige Konzepte:
- **contentEditable:** Macht jedes Element bearbeitbar, nicht nur `<input>`
- **JSON:** Format zum Speichern strukturierter Daten
- **LocalStorage:** Dauerhafter Browser-Speicher
- **Event-Listener:** Reagieren auf Benutzer-Aktionen

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
- [MDN: Web Storage API](https://developer.mozilla.org/de/docs/Web/API/Web_Storage_API)

**Validierung:**
- [MDN: Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [RegexOne Tutorial](https://regexone.com/) - Interaktives Regex-Tutorial

**Events:**
- [MDN: Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)
- [JavaScript.info: Introduction to Events](https://javascript.info/introduction-browser-events)

---

**⏱️ Geschätzte Zeit:** 70 Minuten  
**📦 Nächster Schritt:** Auftrag 3 – Dynamische Projekt-Galerie mit Filter-Funktion