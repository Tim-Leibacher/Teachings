# Auftrag 1: Erste DOM-Manipulation - Inhalte dynamisch ändern

## Ziel

Du lernst, mit JavaScript auf HTML-Elemente zuzugreifen und deren Inhalte dynamisch zu ändern. Das ist der erste Schritt zu interaktiven Websites.

## Beschreibung

**DOM (Document Object Model)** ist die Brücke zwischen HTML und JavaScript. JavaScript kann damit auf jedes HTML-Element zugreifen und es verändern - ohne die Seite neu zu laden. Das macht Websites interaktiv und dynamisch.

In diesem Auftrag änderst du Text, Bilder und Styles direkt per JavaScript.

---

## Teil 1: HTML vorbereiten - Interaktive Elemente (10 Min)

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

## Teil 2: Erste DOM-Manipulation (20 Min)

Erstelle eine neue Datei **`dom.js`** und löse folgende Aufgaben:

### Aufgabe 2.1: Element finden und Text ändern

**Deine Aufgabe:**
1. Finde das Element mit der ID `demo-text`
2. Ändere den Text zu: "JavaScript hat diesen Text geändert!"

**Wo nachschlagen:**
- [MDN: getElementById](https://developer.mozilla.org/de/docs/Web/API/Document/getElementById)
- [MDN: textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)

**Hinweise:**
- Nutze `document.getElementById("id-name")` um ein Element zu finden
- Nutze `.textContent` um den Text zu ändern
- Teste mit `console.log()` ob du das richtige Element gefunden hast

<details>
<summary>💡 Lösung anzeigen (erst selbst probieren!)</summary>

```javascript
console.log("DOM-Script geladen!");

let demoText = document.getElementById("demo-text");
console.log("Element gefunden:", demoText);
demoText.textContent = "JavaScript hat diesen Text geändert!";
```
</details>

### Aufgabe 2.2: Begrüssung mit querySelector

**Deine Aufgabe:**
1. Finde das Element mit der ID `begruessung` (diesmal mit `querySelector`)
2. Erstelle Variablen für deinen Vornamen und Nachnamen
3. Ändere den Text zu einer persönlichen Begrüssung mit Template Literals

**Wo nachschlagen:**
- [MDN: querySelector](https://developer.mozilla.org/de/docs/Web/API/Document/querySelector)
- [MDN: Template Literals](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Template_literals)

**Hinweise:**
- `querySelector` verwendet CSS-Selektoren: `querySelector("#id-name")`
- Template Literals nutzen Backticks: `` `Text ${variable}` ``

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
let begruessung = document.querySelector("#begruessung");
let vorname = "Sarah";
let nachname = "Müller";

begruessung.textContent = `Willkommen, ${vorname} ${nachname}!`;
```
</details>

**Binde die Datei ein:**
Füge in deiner `index.html` vor `</body>` ein:

```html
<script src="script.js"></script>
<script src="dom.js"></script>
```

---

## Teil 3: Aktuelle Uhrzeit anzeigen (20 Min)

### Aufgabe 3.1: Uhrzeit-Funktion erstellen

**Deine Aufgabe:**
Erstelle eine Funktion `zeigeUhrzeit()`, die:
1. Das aktuelle Datum/Uhrzeit holt (`new Date()`)
2. Stunden, Minuten und Sekunden extrahiert
3. Führende Nullen hinzufügt (z.B. "09" statt "9")
4. Die formatierte Zeit im Element `aktuelle-zeit` anzeigt

**Wo nachschlagen:**
- [MDN: Date](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [MDN: Date.getHours()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getHours)
- [MDN: Ternärer Operator](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Operators/Conditional_operator)

**Hinweise:**
- Nutze `getHours()`, `getMinutes()`, `getSeconds()`
- Für führende Nullen: `stunden < 10 ? "0" + stunden : stunden`
- Template Literals helfen beim Formatieren

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function zeigeUhrzeit() {
    let jetzt = new Date();
    let stunden = jetzt.getHours();
    let minuten = jetzt.getMinutes();
    let sekunden = jetzt.getSeconds();
    
    // Führende Nullen hinzufügen
    stunden = stunden < 10 ? "0" + stunden : stunden;
    minuten = minuten < 10 ? "0" + minuten : minuten;
    sekunden = sekunden < 10 ? "0" + sekunden : sekunden;
    
    let zeitString = `${stunden}:${minuten}:${sekunden}`;
    
    let zeitElement = document.getElementById("aktuelle-zeit");
    zeitElement.textContent = zeitString;
}

// Sofort aufrufen
zeigeUhrzeit();
```
</details>

### Aufgabe 3.2: Automatische Aktualisierung

**Deine Aufgabe:**
Sorge dafür, dass die Uhrzeit jede Sekunde aktualisiert wird.

**Wo nachschlagen:**
- [MDN: setInterval](https://developer.mozilla.org/de/docs/Web/API/setInterval)
- [JavaScript.info: Scheduling](https://javascript.info/settimeout-setinterval)

**Hinweise:**
- `setInterval(funktion, millisekunden)` führt eine Funktion wiederholt aus
- 1000 Millisekunden = 1 Sekunde

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
// Jede Sekunde aktualisieren
setInterval(zeigeUhrzeit, 1000);
```
</details>

---

## Teil 4: Besucher-Zähler mit LocalStorage (20 Min)

### Aufgabe 4.1: Besucher zählen

**Deine Aufgabe:**
Erstelle eine Funktion `zeigeBesucher()`, die:
1. Die aktuelle Besuchernummer aus LocalStorage holt (oder 0 wenn nicht vorhanden)
2. Die Nummer um 1 erhöht
3. Die neue Nummer in LocalStorage speichert
4. Die Nummer im Element `besucher-nr` anzeigt

**Wo nachschlagen:**
- [MDN: LocalStorage](https://developer.mozilla.org/de/docs/Web/API/Window/localStorage)
- [MDN: localStorage.getItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/getItem)
- [MDN: localStorage.setItem](https://developer.mozilla.org/en-US/docs/Web/API/Storage/setItem)
- [MDN: parseInt](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

**Hinweise:**
- LocalStorage speichert nur Strings
- `||` Operator für Default-Werte: `variable || standardwert`
- `parseInt()` wandelt Strings in Zahlen um

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function zeigeBesucher() {
    // Besucher-Nummer aus LocalStorage holen (oder 0)
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
</details>

**Test:** Lade die Seite mehrmals neu (F5) - die Zahl sollte steigen!

**Tipp:** Um den Zähler zurückzusetzen, öffne die Browser-Konsole und gib ein:
```javascript
localStorage.clear()
```

---

## Teil 5: Tagesabhängige Begrüssung (20 Min)

### Aufgabe 5.1: Tageszeit-basierte Begrüssung

**Deine Aufgabe:**
Erweitere die Begrüssung so, dass sie sich je nach Tageszeit ändert:
- 05:00-11:59 → "Guten Morgen"
- 12:00-17:59 → "Guten Tag"
- 18:00-21:59 → "Guten Abend"
- 22:00-04:59 → "Gute Nacht"

**Wo nachschlagen:**
- [MDN: if...else](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/if...else)
- [MDN: Vergleichsoperatoren](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Expressions_and_operators#comparison_operators)

**Hinweise:**
- Nutze `if...else if...else` für mehrere Bedingungen
- Vergleiche mit `>=` und `<`

### Aufgabe 5.2: Wochentag hinzufügen

**Deine Aufgabe:**
Ergänze die Begrüssung um den aktuellen Wochentag.

**Wo nachschlagen:**
- [MDN: Date.getDay()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay)
- [MDN: Array](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array)

**Hinweise:**
- `getDay()` gibt 0-6 zurück (0 = Sonntag)
- Du kannst ein Array nutzen: `["Sonntag", "Montag", ...]`

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
function zeigeTagesbegruessung() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    let tag = jetzt.getDay();
    
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
    let wochentage = ["Sonntag", "Montag", "Dienstag", "Mittwoch", 
                      "Donnerstag", "Freitag", "Samstag"];
    let wochentag = wochentage[tag];
    
    let nachricht = `${begruessung}! Heute ist ${wochentag}.`;
    
    let element = document.querySelector("#begruessung");
    element.innerHTML = `
        <strong>${nachricht}</strong><br>
        <em>Willkommen auf meinem Portfolio!</em>
    `;
}

zeigeTagesbegruessung();
```
</details>

---

## Teil 6: Styles dynamisch ändern (Optional, 15 Min)

### Aufgabe 6.1: Dark Mode nachts

**Deine Aufgabe:**
Erstelle eine Funktion, die nachts (18:00-06:00) automatisch Dark Mode aktiviert:
- Hintergrund: dunkel
- Text: hell

**Wo nachschlagen:**
- [MDN: HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
- [MDN: document.body](https://developer.mozilla.org/en-US/docs/Web/API/Document/body)

**Hinweise:**
- `document.body` ist das `<body>`-Element
- Setze Styles mit `.style.eigenschaft = "wert"`

### Aufgabe 6.2: Animierte Demo-Boxen

**Deine Aufgabe:**
Lass alle `.demo-box` Elemente nacheinander einblenden (Fade-In-Effekt).

**Wo nachschlagen:**
- [MDN: querySelectorAll](https://developer.mozilla.org/de/docs/Web/API/Document/querySelectorAll)
- [MDN: forEach](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN: setTimeout](https://developer.mozilla.org/de/docs/Web/API/setTimeout)

**Hinweise:**
- `querySelectorAll()` findet alle passenden Elemente
- `forEach()` iteriert über alle Elemente
- Nutze `setTimeout()` für verzögertes Einblenden

<details>
<summary>💡 Lösung anzeigen</summary>

```javascript
// Dark Mode je nach Uhrzeit
function anpasseFarben() {
    let jetzt = new Date();
    let stunde = jetzt.getHours();
    
    let body = document.body;
    
    if (stunde >= 6 && stunde < 18) {
        // Tagsüber: Hell
        body.style.backgroundColor = "#f5f5f5";
        body.style.color = "#1a1a1a";
    } else {
        // Nachts: Dunkel
        body.style.backgroundColor = "#1a1a1a";
        body.style.color = "#f5f5f5";
    }
}

anpasseFarben();

// Animierte Demo-Boxen
let demoBoxen = document.querySelectorAll(".demo-box");

demoBoxen.forEach(function(box, index) {
    // Initial unsichtbar
    box.style.opacity = "0";
    box.style.transition = "opacity 0.5s";
    
    // Verzögertes Einblenden
    setTimeout(function() {
        box.style.opacity = "1";
    }, index * 200);
});
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
- [ ] Styles werden dynamisch angepasst (Optional)
- [ ] Keine Fehlermeldungen in der Konsole

---

## Tipps & Troubleshooting

### Debugging-Tipps:
- **Element nicht gefunden?** → Prüfe, ob die ID korrekt geschrieben ist
- **Fehlermeldung in Konsole?** → Lies die Fehlermeldung genau durch
- **Script läuft nicht?** → Prüfe, ob das `<script>`-Tag vor `</body>` steht
- **LocalStorage funktioniert nicht?** → Manche Browser blockieren LocalStorage im "Private Mode"

### DevTools nutzen:
- **F12** öffnet die Developer Tools
- **Console-Tab:** Sieh dir `console.log()` Ausgaben an
- **Elements-Tab:** Inspiziere HTML-Elemente und ihre IDs
- **Application-Tab:** Zeigt LocalStorage-Inhalte an

### Wichtige Konzepte:
- **IDs müssen eindeutig sein:** Jede ID darf nur einmal pro Seite vorkommen
- **Klassen für Mehrfachauswahl:** Nutze `.querySelectorAll(".klasse")` für mehrere Elemente
- **LocalStorage zurücksetzen:** `localStorage.clear()` in der Konsole

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
- [JavaScript.info: Document](https://javascript.info/document)
- [W3Schools: DOM Tutorial](https://www.w3schools.com/js/js_htmldom.asp)

**Timing-Funktionen:**
- [JavaScript.info: Scheduling](https://javascript.info/settimeout-setinterval)
- [MDN: WindowOrWorkerGlobalScope](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope)

**LocalStorage:**
- [MDN: Web Storage API](https://developer.mozilla.org/de/docs/Web/API/Web_Storage_API)
- [JavaScript.info: LocalStorage](https://javascript.info/localstorage)

**Best Practices:**
- [Google: DOM Performance](https://web.dev/dom-size/)
- [MDN: Performance](https://developer.mozilla.org/en-US/docs/Learn/Performance)

---

**⏱️ Geschätzte Zeit:** 90 Minuten  
**📦 Nächster Schritt:** Auftrag 2 - Interaktives Profil mit Bearbeitung