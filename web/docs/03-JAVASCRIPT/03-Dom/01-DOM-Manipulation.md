# Auftrag 1: Erste DOM-Manipulation - Inhalte dynamisch ändern

## Ziel

Du lernst, mit JavaScript auf HTML-Elemente zuzugreifen und deren Inhalte dynamisch zu ändern. Das ist der erste Schritt zu interaktiven Websites.

## Beschreibung

**DOM (Document Object Model)** ist die Brücke zwischen HTML und JavaScript. JavaScript kann damit auf jedes HTML-Element zugreifen und es verändern - ohne die Seite neu zu laden. Das macht Websites interaktiv und dynamisch.

In diesem Auftrag änderst du Text, Bilder und Styles direkt per JavaScript.

---

### Teil 1: HTML vorbereiten - Interaktive Elemente (10 Min)

Füge in deiner `index.html` eine neue Sektion nach deinem Portfolio-Inhalt ein:

```html
<section id="interaktiv">
    <h2>Interaktive Demo</h2>
    <p>Hier siehst du, wie JavaScript Inhalte dynamisch ändern kann.</p>
    
    <!-- Element 1: Dynamischer Text -->
    <div class="demo-box">
        <h3>Dynamischer Text</h3>
        <p id="demo-text">Dieser Text wird durch JavaScript geändert...</p>
    </div>
    
    <!-- Element 2: Dynamische Zeit -->
    <div class="demo-box">
        <h3>Aktuelle Uhrzeit</h3>
        <p>Es ist jetzt: <span id="aktuelle-zeit">--:--:--</span> Uhr</p>
    </div>
    
    <!-- Element 3: Persönliche Begrüssung -->
    <div class="demo-box">
        <h3>Persönliche Begrüssung</h3>
        <p id="begruessung">Lade Begrüssung...</p>
    </div>
    
    <!-- Element 4: Besucher-Zähler -->
    <div class="demo-box">
        <h3>Besucher-Statistik</h3>
        <p>Du bist Besucher Nummer: <strong id="besucher-nr">0</strong></p>
    </div>
</section>
```

**Wichtig:**
- Jedes Element hat eine eindeutige `id` (z.B. `id="demo-text"`)
- Über diese `id` können wir mit JavaScript darauf zugreifen

---

### Teil 2: Erste DOM-Manipulation (15 Min)

Erstelle eine neue Datei **`dom.js`** mit folgendem Inhalt:

```javascript
// =====================================================
// DOM-MANIPULATION
// =====================================================
// Zugriff auf HTML-Elemente und dynamische Änderungen

console.log("DOM-Script geladen!");

// === METHODE 1: getElementById() ===
// Greift auf ein Element mit bestimmter ID zu

let demoText = document.getElementById("demo-text");
console.log("Element gefunden:", demoText);

// Text ändern mit .textContent
demoText.textContent = "JavaScript hat diesen Text geändert!";

// === METHODE 2: querySelector() ===
// Flexiblere Methode - funktioniert mit CSS-Selektoren

let begruessung = document.querySelector("#begruessung");
let vorname = "Sarah";
let nachname = "Müller";

begruessung.textContent = `Willkommen, ${vorname} ${nachname}!`;

// === METHODE 3: innerHTML ===
// Kann auch HTML-Tags einfügen (Achtung: Sicherheitsrisiko bei Benutzereingaben!)

begruessung.innerHTML = `
    Willkommen, <strong>${vorname} ${nachname}</strong>!<br>
    <em>Schön, dass du da bist.</em>
`;
```

**Neue Konzepte:**
- `document.getElementById("id")` findet ein Element mit bestimmter ID
- `document.querySelector("#id")` findet ein Element (CSS-Selektor-Syntax)
- `.textContent` ändert den Textinhalt (nur Text, kein HTML)
- `.innerHTML` ändert den Inhalt inkl. HTML-Tags (Vorsicht: XSS-Gefahr!)

**Binde die Datei ein:**

```html
<script src="script.js"></script>
<script src="dom.js"></script>
```

---

### Teil 3: Aktuelle Uhrzeit anzeigen (10 Min)

Erweitere `dom.js` mit einer Echtzeit-Uhr:

```javascript
// === AKTUELLE UHRZEIT ===

function zeigeUhrzeit() {
    let jetzt = new Date();
    let stunden = jetzt.getHours();
    let minuten = jetzt.getMinutes();
    let sekunden = jetzt.getSeconds();
    
    // Füge führende Nullen hinzu (z.B. 09:05:03 statt 9:5:3)
    stunden = stunden < 10 ? "0" + stunden : stunden;
    minuten = minuten < 10 ? "0" + minuten : minuten;
    sekunden = sekunden < 10 ? "0" + sekunden : sekunden;
    
    let zeitString = `${stunden}:${minuten}:${sekunden}`;
    
    let zeitElement = document.getElementById("aktuelle-zeit");
    zeitElement.textContent = zeitString;
}

// Uhrzeit sofort anzeigen
zeigeUhrzeit();

// Uhrzeit jede Sekunde aktualisieren
setInterval(zeigeUhrzeit, 1000);
```

**Neue Konzepte:**
- `new Date()` gibt das aktuelle Datum/Uhrzeit zurück
- `.getHours()`, `.getMinutes()`, `.getSeconds()` holen einzelne Zeitwerte
- Ternärer Operator: `bedingung ? wennWahr : wennFalsch`
- `setInterval(funktion, millisekunden)` führt eine Funktion wiederholt aus

**Ergebnis:** Die Uhrzeit aktualisiert sich jede Sekunde automatisch!

---

### Teil 4: Besucher-Zähler mit LocalStorage (15 Min)

```javascript
// === BESUCHER-ZÄHLER ===

function zeigeBesucher() {
    // Besucher-Nummer aus LocalStorage holen (oder 0 wenn nicht vorhanden)
    let besucher = localStorage.getItem("besucherNummer") || 0;
    
    // Nummer erhöhen
    besucher = parseInt(besucher) + 1;
    
    // Zurück in LocalStorage speichern
    localStorage.setItem("besucherNummer", besucher);
    
    // Im HTML anzeigen
    let besucherElement = document.getElementById("besucher-nr");
    besucherElement.textContent = besucher;
    
    console.log("Du bist Besucher Nummer:", besucher);
}

// Beim Laden der Seite ausführen
zeigeBesucher();
```

**Neue Konzepte:**
- `localStorage` speichert Daten dauerhaft im Browser
- `.getItem("key")` holt gespeicherte Daten
- `.setItem("key", wert)` speichert Daten
- `parseInt()` konvertiert Text in Zahl

**Test:** Lade die Seite mehrmals neu (F5) - die Zahl steigt!

---

### Teil 5: Tagesabhängige Begrüssung (10 Min)

Erweitere die Begrüssung um eine zeitabhängige Nachricht:

```javascript
// === TAGESABHÄNGIGE BEGRÜSSUNG ===

function zeigeTagesbegruessung() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    let tag = jetzt.getDay(); // 0 = Sonntag, 1 = Montag, ...
    
    let begruessung = "";
    
    // Tageszeit
    if (stunde >= 5 && stunde < 12) {
        begruessung = "Guten Morgen";
    } else if (stunde >= 12 && stunde < 18) {
        begruessung = "Guten Tag";
    } else if (stunde >= 18 && stunde < 22) {
        begruessung = "Guten Abend";
    } else {
        begruessung = "Gute Nacht";
    }
    
    // Wochentag
    let wochentag = "";
    if (tag === 1) wochentag = "Montag";
    else if (tag === 2) wochentag = "Dienstag";
    else if (tag === 3) wochentag = "Mittwoch";
    else if (tag === 4) wochentag = "Donnerstag";
    else if (tag === 5) wochentag = "Freitag";
    else if (tag === 6) wochentag = "Samstag";
    else wochentag = "Sonntag";
    
    let nachricht = `${begruessung}! Heute ist ${wochentag}.`;
    
    let element = document.querySelector("#begruessung");
    element.innerHTML = `
        <strong>${nachricht}</strong><br>
        <em>Willkommen auf meinem Portfolio!</em>
    `;
}

zeigeTagesbegruessung();
```

**Neue Konzepte:**
- `if...else if...else` Verzweigungen für Bedingungen
- `getDay()` gibt Wochentag zurück (0-6)
- Verschiedene Nachrichten je nach Uhrzeit

---

### Teil 6: Styles dynamisch ändern (10 Min)

JavaScript kann auch CSS-Styles direkt ändern:

```javascript
// === STYLES DYNAMISCH ÄNDERN ===

// Farbe je nach Uhrzeit
function anpasseFarben() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    
    let body = document.body;
    
    if (stunde >= 6 && stunde < 18) {
        // Tagsüber: Heller Hintergrund
        body.style.backgroundColor = "#f5f5f5";
        body.style.color = "#1a1a1a";
    } else {
        // Nachts: Dunkler Hintergrund (Dark Mode)
        body.style.backgroundColor = "#1a1a1a";
        body.style.color = "#f5f5f5";
    }
}

anpasseFarben();

// Highlight-Effekt für Demo-Boxen
let demoBoxen = document.querySelectorAll(".demo-box");

demoBoxen.forEach(function(box, index) {
    // Verzögertes Einblenden
    setTimeout(function() {
        box.style.opacity = "0";
        box.style.transition = "opacity 0.5s";
        box.style.opacity = "1";
    }, index * 200); // 200ms Verzögerung pro Box
});
```

**Neue Konzepte:**
- `.style.eigenschaft = "wert"` ändert CSS-Eigenschaften
- `.querySelectorAll()` findet **alle** passenden Elemente (gibt Array zurück)
- `.forEach()` führt Funktion für jedes Element aus
- `setTimeout()` führt Funktion nach Verzögerung aus

---

### Teil 7: Komplette `dom.js` (Zusammenfassung)

<details>
<summary>Klicke hier für den kompletten Code</summary>

```javascript
// =====================================================
// DOM-MANIPULATION
// =====================================================

console.log("DOM-Script geladen!");

// === EINFACHE TEXT-ÄNDERUNG ===
let demoText = document.getElementById("demo-text");
demoText.textContent = "JavaScript hat diesen Text geändert!";

// === AKTUELLE UHRZEIT ===
function zeigeUhrzeit() {
    let jetzt = new Date();
    let stunden = jetzt.getHours();
    let minuten = jetzt.getMinutes();
    let sekunden = jetzt.getSeconds();
    
    stunden = stunden < 10 ? "0" + stunden : stunden;
    minuten = minuten < 10 ? "0" + minuten : minuten;
    sekunden = sekunden < 10 ? "0" + sekunden : sekunden;
    
    let zeitString = `${stunden}:${minuten}:${sekunden}`;
    
    let zeitElement = document.getElementById("aktuelle-zeit");
    zeitElement.textContent = zeitString;
}

zeigeUhrzeit();
setInterval(zeigeUhrzeit, 1000);

// === TAGESABHÄNGIGE BEGRÜSSUNG ===
function zeigeTagesbegruessung() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    let tag = jetzt.getDay();
    
    let begruessung = "";
    
    if (stunde >= 5 && stunde < 12) {
        begruessung = "Guten Morgen";
    } else if (stunde >= 12 && stunde < 18) {
        begruessung = "Guten Tag";
    } else if (stunde >= 18 && stunde < 22) {
        begruessung = "Guten Abend";
    } else {
        begruessung = "Gute Nacht";
    }
    
    let wochentag = ["Sonntag", "Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag", "Samstag"][tag];
    
    let nachricht = `${begruessung}! Heute ist ${wochentag}.`;
    
    let element = document.querySelector("#begruessung");
    element.innerHTML = `<strong>${nachricht}</strong><br><em>Willkommen auf meinem Portfolio!</em>`;
}

zeigeTagesbegruessung();

// === BESUCHER-ZÄHLER ===
function zeigeBesucher() {
    let besucher = localStorage.getItem("besucherNummer") || 0;
    besucher = parseInt(besucher) + 1;
    localStorage.setItem("besucherNummer", besucher);
    
    let besucherElement = document.getElementById("besucher-nr");
    besucherElement.textContent = besucher;
    
    console.log("Du bist Besucher Nummer:", besucher);
}

zeigeBesucher();

// === STYLES ANPASSEN ===
function anpasseFarben() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    
    let body = document.body;
    
    if (stunde >= 6 && stunde < 18) {
        body.style.backgroundColor = "#f5f5f5";
        body.style.color = "#1a1a1a";
    } else {
        body.style.backgroundColor = "#1a1a1a";
        body.style.color = "#f5f5f5";
    }
}

anpasseFarben();
```

</details>

---

## Erfolgskriterien

- [ ] HTML mit interaktiven Elementen (IDs gesetzt)
- [ ] `dom.js` erstellt und eingebunden
- [ ] Text wird dynamisch mit `.textContent` geändert
- [ ] Aktuelle Uhrzeit wird jede Sekunde aktualisiert
- [ ] Tagesabhängige Begrüssung funktioniert
- [ ] Besucher-Zähler funktioniert (steigt bei jedem Neuladen)
- [ ] Styles werden dynamisch angepasst (z.B. Dark Mode nachts)
- [ ] Keine Fehlermeldungen in der Konsole

---

## Tipps

- **IDs müssen eindeutig sein:** Jede ID darf nur einmal pro Seite vorkommen
- **Klassen für Mehrfachauswahl:** Nutze `.querySelectorAll(".klasse")` für mehrere Elemente
- **DevTools nutzen:** Inspiziere Elemente (Rechtsklick → Untersuchen) um ihre IDs zu sehen
- **LocalStorage zurücksetzen:** `localStorage.clear()` in der Konsole löscht alle gespeicherten Daten
- **Tipp für Profis:** Nutze `dataset`-Attribute für Datenspeicherung in HTML: `<div data-info="wert">`

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `.textContent` und `.innerHTML`?**  
   *Wann würdest du welche Methode nutzen? Was sind Sicherheitsrisiken bei `.innerHTML`?*

2. **Warum steht das `<script>`-Tag vor `</body>` und nicht im `<head>`?**  
   *Was würde passieren, wenn JavaScript versucht, auf ein Element zuzugreifen, das noch nicht existiert?*

3. **Experimentiere: Ändere die Uhrzeit-Aktualisierung von 1000ms auf 100ms. Was passiert?**  
   *Ist das eine gute Idee? Denk an Performance.*

4. **LocalStorage vs. SessionStorage - wo ist der Unterschied?**  
   *Teste: Erstelle `sessionStorage.setItem("test", "wert")` und schliesse den Tab. Was passiert?*

5. **Öffne die DevTools → Elements Tab. Ändere live Styles mit JavaScript. Siehst du die Änderungen?**  
   *Vergleiche mit CSS-Änderungen im Styles-Panel.*

---

## Weiterführende Links

**DOM-Manipulation:**
- [MDN: DOM Introduction](https://developer.mozilla.org/de/docs/Web/API/Document_Object_Model/Introduction)
- [MDN: getElementById](https://developer.mozilla.org/de/docs/Web/API/Document/getElementById)
- [MDN: querySelector](https://developer.mozilla.org/de/docs/Web/API/Document/querySelector)

**Timing-Funktionen:**
- [MDN: setInterval](https://developer.mozilla.org/de/docs/Web/API/setInterval)
- [MDN: setTimeout](https://developer.mozilla.org/de/docs/Web/API/setTimeout)
- [JavaScript.info: Scheduling](https://javascript.info/settimeout-setinterval)

**LocalStorage:**
- [MDN: Web Storage API](https://developer.mozilla.org/de/docs/Web/API/Web_Storage_API)
- [W3Schools: LocalStorage](https://www.w3schools.com/html/html5_webstorage.asp)

**Best Practices:**
- [Google: DOM Performance](https://web.dev/dom-size/)
- [JavaScript.info: Modifying the document](https://javascript.info/modifying-document)

---

**Geschätzte Zeit:** 60 Minuten  
**Nächster Schritt:** Auftrag 4 - Interaktives Profil mit Bearbeitung
